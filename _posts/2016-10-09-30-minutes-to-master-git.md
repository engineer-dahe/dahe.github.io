---
layout: post
title: "半个小时学会使用git命令行进行团队协作"
comments: true
keywords: ""
---

在学习git之前,我们先来了解一下git的一些基本概念

1、git工作流程见下图

![](http://7xp1dj.com1.z0.glb.clouddn.com/git-work-flow.png "Javascript中Array常规使用方法")

2、一些基本概念

- **.git**目录：使用`git init`初始化一个git仓库时会生成.git隐藏目录，里面存储的是整个项目的文件改变记录等信息。
- 工作区：可以理解为本地的git仓库所在的目录也就是项目目录。
- 暂存区：所有通过`git add`命令添加的文件都存储在暂存区，其实就是.git目录下面的index索引文件中。
- 版本库：也就是整个git仓库。
- 三者的关系：工作区就是你的开发目录，所有的文件编辑通过`git add`添加到暂存区，然后通过`git commit`命令提交到本地git仓库，然后通过`git push`推送到远程git仓库。

常规的git仓库结构如下

git@git.xxx.com:user/project_name.git <br />
&nbsp;&nbsp;|-master （主分支，和线上代码同步）<br />
&nbsp;&nbsp;|-develop（开发分支，功能开发完成后先合并到develop，然后再讲develop合并到master）<br />
&nbsp;&nbsp;|-feature（临时性分支(功能分支)，比如开发某个功能可以新建一个feature分支，完成后将feature分支合并到develop）<br />
&nbsp;&nbsp;&nbsp;&nbsp;|--------- feature/update_online_pay_api <br />
&nbsp;&nbsp;&nbsp;&nbsp;|--------- feature/add_new_feature.. <br />
&nbsp;&nbsp;&nbsp;&nbsp;|--------- ... <br />
&nbsp;&nbsp;|-release（临时性分支(预发分支)，开发完成提测，新建release分支进行测试，完成后合并进master和develop）<br />
&nbsp;&nbsp;&nbsp;&nbsp;|--------- release/update_online_pay_api <br />
&nbsp;&nbsp;&nbsp;&nbsp;|--------- ... <br />
&nbsp;&nbsp;|-hotfix（临时性分支(热修改分支)，一般用于紧急修改bug等短期任务时建立的分支，修改完成后合并到master和develop）
&nbsp;&nbsp;&nbsp;&nbsp;|--------- hotfix/handler_pay_bug <br />
&nbsp;&nbsp;&nbsp;&nbsp;|--------- ... <br />

关于分支命名规则：见名知意，临时性分支可以使用'/'分隔，也可以使用'-'分隔等，没有强制要求

<br />
<br />
**当你接到一个产品需求，开始着手开发的时候，git流程是这样的：** <br />
首先你需要把远程git仓库中的项目同步到你本地，流程如下：

```
cd ~/workspace/git/ // 进入你个人的工作目录
mkdir project_name // 新建一个目录用于存放代码，名称可以和远程仓库名称一样
cd project_name // 进入你新建的目录
git init // 使用git初始化这个目录为一个git仓库
git remote add origin git@github.com:22th/oh-my-zsh.git // 关联本地仓库到一个远程仓库
git fetch --depth=1 // 更新远程仓库的一些信息到本地，比如分支信息等
git checkout -b master origin/master // 检出一个分支master并关联远程的master分支
git pull // 更新本地仓库代码
```

通过以上流程就可以将远程项目同步到本地，现在默认的是远程的master分支，你不可以在master分支修改代码，一般来说你也没有这个权限。
同步代码到本地之后，你需要根据业务需求，新建一个开发分支，名称更具你的需求来调整，比如你要开发一个新功能，那你就建一个feature-xxx分支，如果你是解决一个bug，你可以建一个hotfix-xxx分支。新建分支不建议从本地建，你应该从git仓库管理后台新建，然后再检出到本地。管理后台新建分支很简单，不说了。

然后你就将你新建的分支check到本地，svn命令如下：
```
git checkout -b feature-xxx origin/feature-xxx
```

接下来就是你愉快的开发过程，在你自己的分支上开发，测试，然后提交，会用到的git命令如下：

```
git add <file> // 将工作区修改添加到暂存区，加上 --all 参数表示将所有修改添加到暂存区
git commit -m “msg” // 将暂存区的修改添加到版本库
git push -u origin feature-xxx // 将本地仓库中的修改推送到远程
git status // 查看当前工作区间状态
git log // 查看历史commit
git checkout -- <file> // 用最后一次commit的文件替换当前工作区间的文件
git reset --hard // 丢弃工作区间所有修改，回滚到上一个commit状态
git checkout <版本号> // 回滚到指定版本
```

**功能开发玩，就需要提测并发布到线上了，流程如下**

1、在git仓库管理后台新建release-xxx分支，基于你的feature-xxx分支，主要用于测试。

2、release-xxx测试OK之后，就可以将其merge到master和develop分支，一般是通过git仓库管理后台提交merge request，等待相关管理人员确认后合并到master，提交merge request之前，先merge一下master分支，保证master上新修改的代码和你同步。合并master的时候可能会产生冲突，找到冲突文件，解决并commit。冲突格式如下：

```
<<<<<<< HEAD
ln -s ../statics xxx
=======
ln -s ../statics statics
>>>>>>> master
```

其中 <<<<<<< HEAD 和 ======= 之间的内容表示是你分支中代码，而 ======= 和 >>>>>>> master 表示的是master分支中的代码。那么手动解决冲突的过程就是确认你要保留的代码，把其他的删除，也就是说如果你要保留你本地的代码，那么就是这样的：

```
<<<<<<< HEAD （删除）
ln -s ../statics xxx （保留）
======= （删除）
ln -s ../statics statics （删除）
>>>>>>> master （删除）
```

保留 <<<<<<< HEAD 和 ======= 中间的代码就OK，解决掉所有的冲突后 `git commit -am “解决冲突”`。

3、好了，其他的工作就是运维人员来处理了。一般是这样的，release-xxx分支测试完成并解决所有冲突后，运维发布人员merge到master分支，然后通过 `git diff 608e120 4abe32e --name-only | xargs zip update.zip` 命令打包差异文件，然后发布这个差异文件包就可以啦，不需要所有文件都覆盖线上文件。

<hr>

到这里，整个git项目开发流程就已经非常清楚了。git还有很多高级功能，比如文件对比、文件历史修改记录、关联多个远程仓库等等需要你慢慢去摸索了。使用git要灵活运用分支，因为git新建切换分支的成本非常低，因为git新建分支不是想svn那样吧整个目录复制一遍，然后通过索引文件等更高级的方式来处理，效率高太多。

在推荐个git图形化管理工具：<br />
source tree， mac和windows都有。