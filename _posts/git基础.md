---
title: git基础
date: 2019-09-18 09:58:25
tags: 
- Git 
categories: Git 
description: 
---

# 安装git

Windows 用户:下载[Git](https://git-scm.com/download/win)

建议使用默认安装，安装完成之后就可以用shell(命令行窗口)来执行git相关命令了,

执行git--version 如下  则安装成功。否则可能需要检查下是不是需要配置环境变量

![](2019-09-18_102139.png)

# 检出仓库

git clone path

path 找到你想要检出的项目，如下图  git clone git@github.com:sa0okm9ijn/iosWatch.git

![](2019-09-18_100744.png)

# 创建新仓库

创建新文件夹，打开，然后执行 git init 以创建新的 git 仓库。

>下面每一步中，你都可以通过 git status 来查看你的 git 仓库状态。

![](trees.png)

# 工作流

你的本地仓库由 git 维护的三棵“树”组成。第一个是你的 工作目录，它持有实际文件；第二个是 缓存区（Index），它像个缓存区域，临时保存你的改动；最后是 HEAD，指向你最近一次提交后的结果。

>事实上，第三个阶段是 commit history 的图。HEAD 一般是指向最新一次 commit 的引用。现在暂时不必究其细节


# 添加与提交

你可以计划改动（把它们添加到缓存区），使用如下命令：


```git
git add < filename >
git add *
```
这是 git 基本工作流程的第一步。使用如下命令以实际提交改动：

```
git commit -m "代码提交信息"
```

现在，你的改动已经提交到了 HEAD，但是还没到你的远端仓库。

>在开发时，良好的习惯是根据工作进度及时 commit，并务必注意附上有意义的 commit message。创建完项目目录后，第一次提交的 commit message 一般为「Initial commit.」

# 推送改动

你的改动现在已经在本地仓库的 HEAD 中了。执行如下命令以将这些改动提交到远端仓库：

```
git push origin master

```

可以把 master 换成你想要推送的任何分支。

如果你还没有克隆现有仓库，并欲将你的仓库连接到某个远程服务器，你可以使用如下命令添加：

```

git remote add origin <server>
```

如此你就能够将你的改动推送到所添加的服务器上去了。


> 这里 origin 是 < server > 的别名，取什么名字都可以，你也可以在 push 时将 < server > 替换为 origin。但为了以后 push 方便，我们第一次一般都会先 remote add。
> 如果你还没有 git 仓库，可以在 GitHub 等代码托管平台上创建一个空（不要自动生成 README.md）的 repository，然后将代码 push 到远端仓库。



