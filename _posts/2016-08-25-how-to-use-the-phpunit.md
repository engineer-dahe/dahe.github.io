---
layout: post
title: "配置并使用PHPUnit测试框架进行单元测试"
comments: true
description: "配置并使用PHPUnit测试框架进行单元测试"
keywords: ""
---

PHPUnit是一个面向PHP程序员的测试框架，这是一个xUnit的体系结构的单元测试框架。下面和大家分享一下如何配置使用PHPUnit对自己的代码进行单元测试。**[官方网址](http://www.phpunit.cn/)** **[官方文档](http://www.phpunit.cn/manual/current/zh_cn/installation.html#installation.composer)**

### PHPUnit的安装与配置
PHPUnit可以通过两种方式进行安装，第一种是 **PHP 档案包（PHAR）**，它将 PHPUnit 所需要的所有必要组件（以及某些可选组件）捆绑在单个文件中。另一种是通过 **Composer** 方式进行安装。

#### PHAR安装
**Linux**下配置安装PHPUnit

```shell
 //全局安装：
 $ wget https://phar.phpunit.de/phpunit.phar
 $ chmod +x phpunit.phar
 $ sudo mv phpunit.phar /usr/local/bin/phpunit
 $ phpunit --version

 //直接使用PHAR文件
 $ wget https://phar.phpunit.de/phpunit.phar
 $ php phpunit.phar --version
```

**Windows**下配置安装PHPUint

- 为 PHP 的二进制可执行文件建立一个目录，例如 C:\bin并将 ;C:\bin 附加到 PATH 环境变量中
- 下载 https://phar.phpunit.de/phpunit.phar 并将文件保存到 C:\bin\phpunit.phar
- 打开命令行（例如，按 Windows+R » 输入 cmd » ENTER)
- 建立外包覆批处理脚本（最后得到 C:\bin\phpunit.cmd）

```shell
 C:\Users\username> cd C:\bin
 C:\bin> echo @php "%~dp0phpunit.phar" %* > phpunit.cmd
 C:\bin> exit
```

- 新开一个命令行窗口，确认一下可以在任意路径下执行 PHPUnit

```shell
 C:\Users\username> phpunit --version
```

- 对于 Cygwin 或 MingW32 (例如 TortoiseGit) shell 环境，可以跳过上一步。 取而代之的是，把文件保存为 phpunit （没有 .phar 扩展名），然后用 chmod 775 phpunit 将其设为可执行。

#### Composer安装
首先请确保你的开发机器中已经安装配置好了Composer，我个人比较喜欢使用Composer方式进行安装。

- 修改composer.json文件,在require-dev中加入phpunit选项。

```php
 {
    "require-dev" : {
        "phpunit/phpunit": "5.5.*"
    }
 }
```
- 执行 `composer update` 进行安装。如果要进行系统级安装，可以执行 `composer global require "phpunit/phpunit=5.5.*"`。
- 安装完成后项目目录下 `vendor/bin/` 目录中有 **phpunit** 文件。
- 最后可以执行 `project_dir/vendor/bin/phpunit phpfile_name` 进行代码测试。

### PHPUint使用实例
PHPUnit详细使用方式可以参考 **[官方文档](http://www.phpunit.cn/manual/current/zh_cn/installation.html#installation.composer)**，我在Github上维护了一个简单的 **[Demo](https://github.com/vim22th/DP)**，给大家做一个参考。