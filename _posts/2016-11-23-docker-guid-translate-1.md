---
layout: post
title: "Docker用户文档翻译(1)"
comments: true
description: ""
keywords: ""
---

原文: [Install Docker and run hello-world](https://docs.docker.com/engine/getstarted/step_one/#/docker-for-linux)

## 安装Docker主要分为以下三个步骤：
* 步骤1：获取Docker
* 步骤2：安装Docker
* 步骤3：验证安装

### 步骤1：获取Docker

**Docker for Mac** <br>
Docker for Mac是我们提供的最新的Mac版本。它是一个使用xhyve虚拟Docker引擎环境和Linux核心特性为Docker守护程序的Mac应用程序。

系统要求 <br>

* 2010年或之后的Mac产品，cpu支持内存管理单元虚拟化
* 系统为macOs10.10.3 或者更高版本
* 至少4G内存
* 确保VirtualBox4.3.30之前的版本没有被安装（与Mac版本Docker不兼容），否则在这种情况下安装Docker会报错，请删除老版本的VirtualBo并尝试重新安装

Docker Toolbox For Mac <br>
如果您使用的是早期版本的Mac或者你的设备不能满足以上条件，请尝试使用Docker Toolbox。
[点击查看Docker Toolbox描述获取安装帮助](https://docs.docker.com/toolbox/overview/)

**Docker for Windows** <br>
Docker for Windows是我们提供的最新的PC版本。它是一个使用Hyper-v虚拟Docker引擎环境和Linux核心特性为Docker守护程序的Windows应用程序。

系统要求 <br>

* 64为Window 10 pro，企业版或教育版（安装了十一月更新，基于10586或更早版本构建）。未来我们会支持更多的Windows版本。
* Hyper-v必须打开，必要时Docker在安装时会帮你打开它。（重启后生效）

Docker Toolbox For Windows <br>
如果您使用的是早期版本的Windows将不能满足以上条件，请尝试使用Docker Toolbox。
[点击查看Docker Toolbox描述获取安装帮助](https://docs.docker.com/toolbox/overview/)

**Docker for Linux** <br>
Docker引擎原生可以在各个Linux发行版中运行。
获取更全面的Docker在各个Linux发行版中的安装指令说明，[请点击这里](https://docs.docker.com/engine/installation/)

### 步骤2：安装Docker
* Mac安装说明，[点击这里](https://docs.docker.com/docker-for-mac/)
* Windows安装说明，[点击这里](https://docs.docker.com/docker-for-windows/)
* Docker Toolbox安装说明，[点击这里](https://docs.docker.com/toolbox/overview/)
* Linux安装说明 - [点击查看](https://docs.docker.com/engine/getstarted/linux_install_help/)在Ubuntu中安装Docker实例，更多其他版本Liunx安装说明请[查看这里](https://docs.docker.com/engine/installation/)

### 步骤3：验证安装
1、打开命令行终端，输入Docker指令来验证Docker是否安装正确。尝试使用`docker version`去检查你最终安装的Docker版本，`docker ps`去查看当前正在运行的容器（获取没有，应该你才刚刚入门）。
2、输入`docker run hell-world`并敲回车，命令开始被执行，如果一切顺利的话，你会看到命令行输出内容如下：

```
 $ docker run hello-world
 Unable to find image 'hello-world:latest' locally
 latest: Pulling from library/hello-world
 535020c3e8ad: Pull complete
 af340544ed62: Pull complete
 Digest: sha256:a68868bfe696c00866942e8f5ca39e3e31b79c1e50feaee4ce5e28df2f051d5c
 Status: Downloaded newer image for hello-world:latest

 Hello from Docker.
 This message shows that your installation appears to be working correctly.

 To generate this message, Docker took the following steps:
 1. The Docker Engine CLI client contacted the Docker Engine daemon.
 2. The Docker Engine daemon pulled the "hello-world" image from the Docker Hub.
 3. The Docker Engine daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker Engine daemon streamed that output to the Docker Engine CLI client, which sent it
    to your terminal.

 To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

 Share images, automate workflows, and more with a free Docker Hub account:
 https://hub.docker.com

 For more examples and ideas, visit:
 https://docs.docker.com/userguide/
```
3、执行`docker ps -a`显示系统中存在的所有容器。

```
 $ docker ps -a

 CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS               NAMES
 592376ff3eb8        hello-world         "/hello"            25 seconds ago      Exited (0) 24 seconds ago                       prickly_wozniak
```
你将会看到`hello-world`显示在你执行`docker ps -a`命令后出现的容器列表中。
`docker ps`仅显示当前正在运行中的容器。因为`hello-world`已经运行并结束，所以执行`docker ps`时它不会被显示。

下一篇：<br>
在当前文章中，你已经成功的安装了Docker，关掉当前Docker快速命令入门窗口。现在，我们继续前往下一页去阅读[关于Docker images和容器的剪短说明](https://docs.docker.com/engine/getstarted/step_two/)。
