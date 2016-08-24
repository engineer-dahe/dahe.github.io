---
layout: post
title: "Github 协作流程"
comments: true
description: "如何在Github上为开源项目贡献自己的代码"
keywords: ""
---

下面和大家分享一下如何在Github上为开源项目贡献自己的代码。

### 协作流程
- **fork** 需要协作项目
- **克隆/关联** 你 fork 的项目到本地
- 新建分支（branch）并检出（checkout）新分支
- 添加本项目到你的本地 git 仓库作为上游（upstream）
- 变基（衍合 rebase）你的分支到上游 master 分支
- **push** 你的本地仓库到 GitHub
- 在 Github 上提交 **pull requests**
- 等待管理员（你需要贡献的开源项目管理员）处理，并及时 rebase 你的分支到上游 master分支（若上游 master 分支有修改）
- 若有必要，可以 git push -f 强行推送 rebase 后的分支到自己的 GitHub fork

### 详细说明
- fork 项目说明：当我们去 fork 别人的一个项目，这就在自己的GitHub生成了一个与原作者互不影响的副本，自己可以将自己Github上的这个项目再clone到本地进行修改，修改后再push，只有自己Github上的项目会发生改变，而原作者项目并不会受影响，避免了原作者项目被污染。
- 不同步问题产生的原因：如果原作者在不断更新他的项目，自己的Github上的项目是不会进行同步的，解决方案：

进入本地项目目录，输入 `git remote -v`，此时会现在本项目在GitHub上的URL。其中，在 origin 两栏显示的url是我们fork后Github上的项目，upstream 两栏显示的url是原作者项目。如果没有 upstream，即没有原作者项目的url，需要自己添加： `git remote add upstream <原作者项目的URL>`，原作者项目url地址可从Github网站上找出。然后再将原作者项目更新的内容同步到我的本地项目（不是我们Github网上的项目）。

> - 获取从上游仓库（原作者的项目）的各分支，提交到我们本地项目的主分支。使用命令如下：`git fetch upstream`
> - 切换本地项目的主分支(master)。使用命令如下：`git checkout master`
> - 接下来就是合并这两个分支，将原作者项目的修改同步到自己这里（注意还是指本地项目，不是自己Github空间里的项目），使用命令如下：`git merge upstream/master`。至此我们本地的项目就和原作者的项目同步了。
> - 如果想让我们本地的项目同步到github上，使用命令如下:`git remote add origin master <该项目在你Github上的URL>`