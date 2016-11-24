---
layout: post
title: "Docker用户文档翻译(1)"
comments: true
description: ""
keywords: ""
---

原文: [Install Docker and run hello-world](https://docs.docker.com/engine/getstarted/step_two/)

Docker引擎为镜像和容器提供了核心技术。在上一篇文章中，你安装Docker的最后，执行了`docker run hello-world`命令，这条命令包含以下三个部分：

![](http://7xp1dj.com1.z0.glb.clouddn.com/container_explainer.png)

* docker: 告诉操作系统你将使用docker程序
* run: 子命令，运行一个docker容器
* hello-world: 告诉docker需要加载此镜像到容器中

镜像（image）是一个运行时所需要的文件系统和参数的集合，它没有状态并且不会被改变。容器（container）是镜像（image）运行的一个实例。当你执行这条命令是，Docker引擎会做一下工作：

* 检查你是否包含有hello-world镜像
* 从Docker Hub下载该镜像（更多关于hub会在后面介绍）
* 加载改镜像到容器并运行改容器

依赖于他们的构建方式，一个镜像可能运行一个简单的、单一的命令后结束，这也正是hello-world镜像运行后所做的。

一个Docker镜像可以胜任更多的工作。一个镜像可以启动一个如数据库这般复杂的软件，等待去添加、存储数据并给你或者下一个人去使用。

谁创建了hello-world镜像呢？在这个案例下，Docker不可以创建，但是其他人都可以。Docker引擎允许个人或者公司通过Docker镜像创建并分享软件。使用Docker引擎，你不必担心你的电脑是否可以运行该Docker镜像，任何一个Docker容器都可以运行它。

接下来我们将要 <br>
看，是否很快就看完了？现在，你将乐意使用Docker去做一些更有趣的事情，来看下一部分[寻找并运行whalesay镜像](https://docs.docker.com/engine/getstarted/step_three/)。
