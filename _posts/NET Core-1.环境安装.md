---
title: .Net Core 环境安装
date: 2019-03-06 07:34:00
tags: 
- .NET Core简易入门
categories: .NET
description: 
---
## 运行环境

[点击进入](https://dotnet.microsoft.com/download)，选择对应平台进行下载。

**.Net Core SDK    软件开发工具包。包含.Net Core Runtime**

**.Net Core Runtime 运行时仅包含.Net Core 应用程序运行需要的资源**

## 开发IDE

[点击进入](https://code.visualstudio.com/),选择对应平台下载，我在这里用的是Visual Studio Code
IDE，当然也可以使用别的。

## 安装c#扩展

如图所示安装c#扩展

![](584421-20190306152414905-995368132.png)

## 第一个Hello World程序

菜单栏->Terminal->New Terminal,在新打开的终端中输入dotnet --version（查看版本），dotnet new
console -o HelloWorld

![](584421-20190306152922672-1601072562.png)



 接下来定位到程序目录-->编译-->运行

![](584421-20190306153327514-598734178.png)



 到此，第一个.Net Core的程序运行成功。

