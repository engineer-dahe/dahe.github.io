---
layout: post
title: "Git常用命令总结"
comments: true
keywords: ""
author: '丁'
---

#### 基础Git命令
我们在初始化Git仓库时会用到两种方法，一个是将远程的仓库clone到本地，还有一种是将本地仓库关联致远程仓库。

*克隆*
```
cd 工作目录
git clone git@github.com:1024b/test.git
```

*关联*
```
cd 工作目录
mkdir 项目目录
git init
git remote add origin git@github.com:1024b/test.git
git fetch
git checkout master
```

*常用操作*
```
git status // 当前分支状态
git add --all <git add <file name>> // 添加修改文件到本地仓库
git commit -m ‘some msg’ // 提交修改到本地仓库
git push / git push origin master // 推送更新到远程仓库
git pull // 更新
git log // 提交记录
git merge <待合并分支名称> // 合并分支
git checkout . // 撤销所有未暂存的修改
git branch // 查看本地分支
git branch -r // 查看远程分支
git remote -v // 查看所有远程关联源
git rm <filename1> … // 从仓库中删除文件
```

*高级操作*

强制更新代码上一个commit版本（代码已推送到远程仓库）
```
git log // 查看上一个commit的id
git reset --hard <commit 版本号> // 将本地仓库代码回滚到制定版本并丢弃所有修改
git push -f // 强制将本地代码跟新到远程仓库
```

查看最后一次commit修改的文件列表
```
git log --pretty=format:"" --name-only -1
```

查看某个commit修改的文件列表
```
git log <commit 版本号> --pretty=format:"" --name-only -1
```

查看上一次修改的代码
```
git show
```

查看指定commit中的某个文件的修改代码
```
git show / git show <commit 版本号> <filename>
```


比较两个commit中的文件差异
```
git diff <commit id1> <commit id2> <filename>
```

比较两个分支中的文件差异
```
git diff <分支1> <分支2> <filename>
```

*Git配置*
```
git config --global user.name ‘username’
git config --global user.email ‘email’
git config --global alias.co checkout  // git别名，git checkout == git co
...
```

