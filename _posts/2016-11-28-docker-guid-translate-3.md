---
layout: post
title: "Docker用户文档翻译(3)"
comments: true
description: ""
keywords: ""
---

原文: [Find and run the whalesay image](https://docs.docker.com/engine/getstarted/step_three/)

找到并运行whalesay镜像
全世界的朋友们都可以创建Docker镜像。你可以通过浏览器打开Docker hub并在这里找到它们。下面的内容将告诉你如何搜索并使用Docker镜像。

###步骤1 定位whalesay镜像
1. 打开浏览器并访问[Docker Hub](https://hub.docker.com/)
2. Docker Hub包含大量个人（比如你）、官方组织机构（比如红帽、IBM、Google）的镜像。
3. 在搜索条中输入whalesay关键词
4. 在搜索结果中点击docker/whalesay
<br />每个镜像仓库包含这个镜像的的信息，它可能包含的信息包括这个镜像的特性以及如何去使用它。你可能会注意到whalesay基于Linux分支Ubunut。下一步你将在你的机器上运行whalesay。

###步骤2 运行whalesay镜像
确保Docker以及运行，在Mac或者Windows中运行Docker，你将能从系统状态栏中看到Docker巨鲸图标。
<br />
1、代码命令提示符窗口
2、敲出`docker run docker/whalesay cowsay boo`并按Enter键，这条命令将在一个容器中运行whalesay。你的终端将会有一下输出：

```
 $ docker run docker/whalesay cowsay boo
 Unable to find image 'docker/whalesay:latest' locally
 latest: Pulling from docker/whalesay
 e9e06b06e14c: Pull complete
 a82efea989f9: Pull complete
 37bea4ee0c81: Pull complete
 07f8e8c5e660: Pull complete
 676c4a1897e6: Pull complete
 5b74edbcaa5b: Pull complete
 1722f41ddcb5: Pull complete
 99da72cfe067: Pull complete
 5d5bd9951e26: Pull complete
 fb434121fc77: Already exists
 Digest: sha256:d6ee73f978a366cf97974115abe9c4099ed59c6f75c23d03c64446bb9cd49163
 Status: Downloaded newer image for docker/whalesay:latest
  _____
 < boo >
  -----
     \
      \
       \
                     ##        .
               ## ## ##       ==
            ## ## ## ##      ===
        /""""""""""""""""___/ ===
   ~~~ {~~ ~~~~ ~~~ ~~~~ ~~ ~ /  ===- ~~~
        \______ o          __/
         \    \        __/
           \____\______/
```
当你第一次运行一个软件镜像时，docker命令会在你的本地系统中搜索。如果没有找到，docker将会去Docker Hub中寻找并获取到本地。
<br />
3、任然在命令终端输入`docker images`命令并按回车，这条命令将会列出所有你本地镜像。你将会从列表中看到docker/whalesay。

```
 $ docker images
 REPOSITORY           TAG         IMAGE ID            CREATED            SIZE
 docker/whalesay      latest      fb434121fc77        3 hours ago        247 MB
 hello-world          latest      91c95931e552        5 weeks ago        910 B
```
当你在容器中运行一个镜像时，Docker将会将这个镜像下载到本地，你运行时的知识本地的一个副本。当Docker Hub中此镜像发生改变时，Docker会再次下载它。你当然可以删除你下载的镜像，你将在后面学习到更多，现在我们留在当前镜像应为我们接下来还会使用到它。
<br />
4、花一些时间去控制并使用whalesay容器
尝试运行whalesay并附带上一个单词或者短语。尝试长或者短的句子，你能破坏这头奶牛吗？😄😄

###接下来
在这个页面，你学会了如何在Docker Hub中搜索镜像。你通过命令运行了一个镜像。想想看，你再你的Mac电脑上有效的运行了一个Liunx软件，你学会了在你的电脑中运行一个奖项副本。现在，你将准备创建自己的Docker镜像，点击进入下一部分 - [去创建你自己的镜像](https://docs.docker.com/engine/getstarted/step_four/)