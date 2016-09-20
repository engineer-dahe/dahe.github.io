---
layout: post
title: "如何在Github上为开源项目贡献自己的代码"
comments: true
description: "如何在Github上为开源项目贡献自己的代码"
keywords: ""
---

下面和大家分享一下如何在Github上为开源项目贡献自己的代码。

### 主要分为一下几个步骤
- **fork**需要协作项目
- **克隆/关联**fork的项目到本地
- 新建分支（branch）并检出（checkout）新分支
- 在新分支上完成代码开发
- 开发完成后将你的代码合并到master分支
- 添加原作者的仓库地址作为一个新的仓库地址
- 合并原作者的master分支到你自己的master分支,用于和作者仓库代码同步
- **push**你的本地仓库到GitHub
- 在Github上提交 **pull requests**
- 等待管理员（你需要贡献的开源项目管理员）处理

### 补充详细说明
- fork 项目说明：当我们去 fork 别人的一个项目，这就在自己的GitHub生成了一个与原作者互不影响的副本，自己可以将自己Github上的这个项目再clone到本地进行修改，修改后再push，只有自己Github上的项目会发生改变，而原作者项目并不会受影响，避免了原作者项目被污染
- 如果原作者在不断更新他的项目，自己的Github上的项目是不会进行同步的，解决方案：
    > - 进入本地项目目录，输入 `git remote -v`，此时会现在本项目在GitHub上的URL。其中，在 origin 两栏显示的url是我们fork后Github上的项目，upstream 两栏显示的url是原作者项目。如果没有 upstream，即没有原作者项目的url，需要自己添加： `git remote add upstream <原作者项目的URL>`，原作者项目url地址可从Github网站上找出。然后再将原作者项目更新的内容同步到我的本地项目(不是我们Github网上的项目)
    > - 获取从上游仓库（原作者的项目）的各分支，提交到我们本地项目的主分支。使用命令如下：`git fetch upstream`
    > - 切换本地项目的主分支(master)。使用命令如下：`git checkout master`
    > - 接下来就是合并这两个分支，将原作者项目的修改同步到自己这里（注意还是指本地项目，不是自己Github空间里的项目），使用命令如下：`git merge upstream/master`。至此我们本地的项目就和原作者的项目同步了
    > - 使用`git remote rm <name>`删除某个仓库地址
    > - 使用`git checkout upstream/master`可以检出upstream（这里是原作者）下的master分支