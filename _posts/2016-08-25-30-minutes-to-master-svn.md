---
layout: post
title: "半个小时学会使用svn命令行进行团队协作"
comments: true
description: "半个小时学会使用svn命令行进行团队协作"
keywords: ""
---


我尽量用最简洁明了的方式告诉大家如何使用svn命令行进行团队协作

### 一个基础的、正规的svn仓库目录结构是这样的

http://xx.xxx.xx/.../project_name <br />
&nbsp;&nbsp;|-branches （包含所有开发者分支）<br />
&nbsp;&nbsp;&nbsp;&nbsp;|--------- coder_1 <br />
&nbsp;&nbsp;&nbsp;&nbsp;|--------- coder_2 <br />
&nbsp;&nbsp;&nbsp;&nbsp;|--------- ... <br />
&nbsp;&nbsp;|-tags（每一次上线前都会打一个tag，方便回滚）<br />
&nbsp;&nbsp;&nbsp;&nbsp;|--------- project_name_v1.0 <br />
&nbsp;&nbsp;&nbsp;&nbsp;|--------- project_name_v2.0 <br />
&nbsp;&nbsp;&nbsp;&nbsp;|--------- ... <br />
&nbsp;&nbsp;|-trunk（主分支，和线上代码同步）<br />


当你接到一个产品需求，开始着手开发的时候，svn流程是这样的：
首先以当前线上分支trunk为基准，在仓库下的**branches**目录中建一个属于你的开发分支，你可以命名成这样 **ryan_20160923** ,或者和需求相关的，比如这样**edit_user_template**等等，新建分支的svn命令如下：

```
svn cp -m "create branch” http://svn_server/xxx_repository/trunk http://svn_server/xxx_repository/branches/ryan_20160923
```
这行代码可以这样理解：复制trunk目录下的文件到branches下的ryan_20160923目录中。不错，你可能已经发现了，svn下面的分支的概念其实就是一个分支一个文件夹，这比git蠢很多，导致切分支成本很高。

然后你就将你新建的分支check到本地，svn命令如下：

```
svn checkout http://svn_server/xxx_repository/branches/ryan_20160923
```

接下来就是你愉快的开发过程，在你自己的分支上开发，测试，然后提交，会用到的svn命令如下：

```
svn add <file> // 添加文件到工作区间，默认新建的文件是不会自动添加到版本库的，需要手动使用svn add命令添加
svn st | grep '^\?' | tr '^\?' ' ' | sed 's/[ ]*//' | sed 's/[ ]/\\ /g' | xargs svn add // 添加所有新增文件，强大的脚本
svn commit -m “msg” // 提交更新到远程仓库
svn update // 更新远程仓库的修改到本地
svn info // 查看当前仓库的svn信息，如svn地址等
svn st // 查看当前工作区间状态
```

功能开发、测试完成，就需要发布到线上了，那么这里我们有几步工作要做：

1、合并trunk分支代码到自己的开发分支
首先保证一下当前目录是你的个人开发分支目录，运行

```
svn merge http://svn_server/xxx_repository/trunk —dry-run
```
—dry-run参数是先模拟合并，控制台会打印合并信息，如果有错误也会打印出来，合并前先 —dry-run 一下是一个好的习惯。确认没有问题之后运行

```
svn merge http://svn_server/xxx_repository/trunk
```
合并trunk分支代码。如果有冲突，控制台会输出冲突文件信息，并给你一个交互问你如何处理，选择 p 稍后手动合并即可。


2、 合并trunk分支后可能会产生冲突，这时候就要手动合并冲突了。原则是自己改动的代码仔细检查，以自己的为准，其他自己没有修改过的文件全部以trunk为准。文件产生冲突的时候svn会帮我们生成和冲突文件同名但文件后缀不同的3个文件，分别是 a.php.l10(10代表版本号)，a.php.r11(11代表版本号) 和 a.php.work，分别代表前一个版本的代码，后一个版本的代码，当前工作区间的代码。我一般解决自己没有修改的冲突文件采用的是直接使用文件a.php.l11内容替换a.php文件里面的内容，也就是用当前线上的文件内容替换，一般不会有问题。文件冲突的时候，svn会自动帮我们标识出来位置，格式如下：

```
<<<<<<< .work

     echo “hello world”;

=======

     echo “hello china”;

>>>>>>> .r2
```
其中 <<<<<<< .work 和 ======= 包含的代码表示的是你本地的代码， ======= 和 >>>>>>> .r2（2是版本号）表示的是线上的代码。那么手动解决冲突的过程就是确认你要保留的代码，把其他的删除，也就是说如果你要保留你本地的代码，那么就是这样的：

```
<<<<<<< .work（删除）

     echo “hello world”;

=======（删除）

     echo “hello china”;（删除）

>>>>>>> .r2（删除）
```

保留 <<<<<<< .work 和 ======= 中间的代码就OK，解决掉所有的冲突后别忘了把svn自动生成的那几个特殊文件也删除了。然后 `svn commit -m “解决冲突”`。

3、刚才是吧trunk分支合并到了我们的开发分支，现在我们还要把开发分支合并到trunk分支，因为所有的发布都是从trunk打tag，然后发布这个tag。合并流程如上，因为我们在开发分支上已经合并了trunk分支，所以再把开发分支合并到trunk的时候一般不会产生冲突。

4、好了，我们的代码已经合并到trunk分支，现在就差发布到线上了。我们的发布流程是先从trunk分支打一个tag，然后再发布这个tag到线上。这样能够保证我们这个功能有问题的时候能切换到上一个tag或者上几个tag。打tag在svn里面其实就是拷贝分支，哈哈。命令如下：

```
svn copy http://svn_server/xxx_repository/trunk http://svn_server/xxx_repository/tags/release-1.0 -m "1.0 released"
```

5、现在就可以吧我们刚刚打好的这个tag发布到线上了，发布成功之后，记得使用 `svn rm <分支地址>` 删除开发分支。

到这里，整个svn项目开发流程就已经非常清楚了。svn还有很多高级功能，比如文件对比、文件历史修改记录等等需要你慢慢去摸索了，上面讲的在日常开发中基本已经够用了。svn分支的理解可以解释为文件的备份，和git相比还是笨很多。git切分支几乎没有成本，分布式仓库管理模式也是svn所不具备的。

在推荐几个svn图形化管理工具：
windows： TortoiseSVN   很强大，谁用谁知道，我一把用他来查看文件历史修改记录
mac：Cornerstone