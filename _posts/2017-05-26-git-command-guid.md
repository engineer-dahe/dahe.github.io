---
layout: post
title: "Git常用命令总结"
comments: true
keywords: ""
author: '丁'
---

<h4>基础Git命令</h4>

<p>我们在初始化Git仓库时会用到两种方法，一个是将远程的仓库clone到本地，还有一种是将本地仓库关联致远程仓库。</p>

<p><em>克隆</em></p>

<pre><code>cd 工作目录
git clone git@github.com:1024b/test.git
</code></pre>

<p><em>关联</em></p>

<pre><code>cd 工作目录
mkdir 项目目录
git init
git remote add origin git@github.com:1024b/test.git
git fetch
git checkout master
</code></pre>

<p><em>常用操作</em></p>

<pre><code>git status // 当前分支状态
git add --all &lt;git add &lt;file name&gt;&gt; // 添加修改文件到本地仓库
git commit -m ‘some msg’ // 提交修改到本地仓库
git push / git push origin master // 推送更新到远程仓库
git pull // 更新
git log // 提交记录
git merge &lt;待合并分支名称&gt; // 合并分支
git checkout . // 撤销所有未暂存的修改
git branch // 查看本地分支
git branch -r // 查看远程分支
git remote -v // 查看所有远程关联源
git rm &lt;filename1&gt; … // 从仓库中删除文件
</code></pre>

<p><em>高级操作</em></p>

<p>强制更新代码上一个commit版本（代码已推送到远程仓库）</p>

<pre><code>git log // 查看上一个commit的id
git reset --hard &lt;commit 版本号&gt; // 将本地仓库代码回滚到制定版本并丢弃所有修改
git push -f // 强制将本地代码跟新到远程仓库
</code></pre>

<p>查看最后一次commit修改的文件列表</p>

<pre><code>git log --pretty=format:&quot;&quot; --name-only -1
</code></pre>

<p>查看某个commit修改的文件列表</p>

<pre><code>git log &lt;commit 版本号&gt; --pretty=format:&quot;&quot; --name-only -1
</code></pre>

<p>查看上一次修改的代码</p>

<pre><code>git show
</code></pre>

<p>查看指定commit中的某个文件的修改代码</p>

<pre><code>git show / git show &lt;commit 版本号&gt; &lt;filename&gt;
</code></pre>

<p>比较两个commit中的文件差异</p>

<pre><code>git diff &lt;commit id1&gt; &lt;commit id2&gt; &lt;filename&gt;
</code></pre>

<p>比较两个分支中的文件差异</p>

<pre><code>git diff &lt;分支1&gt; &lt;分支2&gt; &lt;filename&gt;
</code></pre>

<p><em>Git配置</em></p>

<pre><code>git config --global user.name ‘username’
git config --global user.email ‘email’
git config --global alias.co checkout  // git别名，git checkout == git co
</code></pre>

<p>…</p>