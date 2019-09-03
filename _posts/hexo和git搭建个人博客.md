---
title: hexo和git搭建个人博客
date: 2019-07-24 14:26:48
tags: 
- Hexo
- Git
categories: Git 
description: 
---
## 什么是hexo
Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

## 安装
1、安装Git
Windows：下载并安装：https://git-scm.com/download/win
2、安装Node.js
Windows：下载并安装：https://nodejs.org/en/,安装时，请勾选Add to PATH选项
3、安装Hexo
打开windows PowerShell,输入如下命令,Hexo将会在指定文件夹中新建所需的文件

```
npm install -g hexo-cli
```

安装 Hexo 完成后，请执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件。
```
$ hexo init <folder>
$ cd <folder>
$ npm install
```
新建完成后，指定文件夹的目录如下
```
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```





## 创建存储库
1、创建一个github账户,参考https://sa0okm9ijn.github.io/2019/05/29/一步一步把本地目录放到git仓库/

2、创建存储库,创建一个名为username.github.io 的新存储库，其中username是GitHub上的用户名。如果存储库的第一部分与您的用户名不完全匹配，则无法正常工作，因此请务必正确使用。
![user-repo@2x](user-repo@2x.png)

3、参考https://sa0okm9ijn.github.io/2019/05/29/一步一步把本地目录放到git仓库/,配置本地和服务端的连接

4、配置生成的hexo生成的指定文件夹下的_config.yml,配置如下节点的repo
```
deploy: 
  type: git 
  repo: git@github.com:sa0okm9ijn/sa0okm9ijn.github.io.git  
  branch: master
```
![user-repo@2x](2019-07-24_152710.png)
5、下面就可以用hexo的命令来创建、生成、发布你的博客了。

