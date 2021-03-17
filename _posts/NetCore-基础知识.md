---
title: NetCore-基础知识
date: 2020-03-28 18:39:05
tags: 
- .NETCore基础知识
categories: .NETCore
description: 
---

# .NET Core到底是什么

概括的说,.NET Core是一种小型、高效的,可以通过文件复制直接部署的跨平台框架。

.NET Core备受关注的主要原因:
1. .NET Core自身开源,并鼓励更多的.NET项目开源
2. .NET Core跨平台

## 开源的许可协议

当前开源世界有4个较为主流的软件许可协议.
1. GPL
2. Apache
3. BSD
4. MIT

具体协议内容:http://choosealicense.online/appendix/

![](2019-12-18-16-03-02.png)

由微软牵头组建的.NET基金会的重要资产就是.NET Core的源代码以及.NET Core周边的一些开源项目,.NET基金会的开源项目基本上都遵循MIT许可协议。这使得.NET Core的源代码具有极大的开放性和移植性

## .NET Core的重要组件

.NET Core并不是一个开源项目,而是有多个开源项目构成的项目集.其核心的四个支柱项目

1. CoreCLR:.NET公共语言运行时,对应java就是JRE(java虚拟机),由.NETFramework的CLR源代码迁移而来,解构基本一致.
   - Class Loader:负责把磁盘上编译过的中间代码加载到内存,所有引用类型都是通过Class Loader加载到内存中
   - GC:垃圾收集,是.NET Core实现内存自动化管理的重要组件
   - JIT:负责把Class Loader装载到内存中的中间语言代码在进行一次编译,根据当前代码执行的路径、操作系统、硬件情况编译出执行的高效汇编代码.
   - Exception Handler:处理.NET Core代码在运行过程中产生的异常.如果开发者在可能产生异常的地方使用了try-catch,会保证异常被catch处理,否则交给操作系统处理
2. CoreFX:基础类库,它完全由c#语言写成,.NET Core绝大多数代码由.NETFramework迁移而来,这种迁移不是简单的复制,而是争对跨平台特性做了大量的兼容性调整.
为了兼容多个操作系统,c#的``partial``关键字得到了大量的应用.对于需要跨平台兼容的CoreFX类型,都是通过``partial``关键字来声明,讲多平台公用的代码放在一个源代码文件中,具体某个操作系统相关代码放到另一个平台相关的源代码文件中.通过``partial``关键字和条件编译的方法,避免了大量的适配器模式在源代码的应用,同时也提高了执行效率.
3. CLI:集项目文件管理、项目构建和代码运行的容器等功能与一身的,名为dotnet的命令行工具。.NET Core选择编译的二进制文件都是以.dll位扩展名的pe文件.
4. Roslyn:为了更好的支持.NET上的高级编程语言而创建的新一代语言编译器.Roslyn被微软定义为下一代编译平台,除了代码编译,还提供了代码分析以及丰富的API.相比之前的C#编译器``csc.exe``,Roslyn生成的中间语言更加高效,编译器时间也大大缩短.

上述开源项目在.NET基金会组织下都可以找到,http://www.github.com/dotne

# .NET Core编译

## 前言

.NET Core的源代码存放于http://www.github.com/dotnet/组织结构下,并由.NET Core团队保持的更新。通常情况下,通过正式安装的安装方式安装.NET Core运行时和SDK即可.但是有时候为了获得一些新的特性,或者为了调试获得符号表文件(.pdb文件),还需要手动编译.NET Core的源代码

## 在Windows操作系统上的编译

### 环境装备

- 启用长路径:组策略(gpedit.msc)->计算机配置->管理模板->系统->文件系统->启用win32长路径
- git启用长路径:git config --system core.longpaths true(如果安装了git的话)
- 安装Visual Studio
  .NET Core在Windows平台上的编译,需要安装Visual Studio来主要执行具体的编译动作,推荐使用Visual Studio2017以上。打开Visual Studio安装器,可以通过手动选择也可以通过导入配置（）
   1. 手动安装:勾选.NET桌面开发、c++桌面开发
   2. 导入配置:(runtime源码根目录下.vsconfig文件)
- CMake安装:构建程序,下载地址:http://www.cmake.org/download

### 执行编译

在runtime目录下执行``build -? 查看相关命令进行编译``,如我们要编译.Coreclr,执行``.\build -subsetCategory CoreClr``.编译是为了获取debug的运行时(调试源码),编译生成的符号表文件可以用来调试应用.

## Linux环境

按以下命令顺序执行：

```shell
# 1. 安装以下软件包
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates gnupg software-properties-common wget

# 2. 获取签名密钥
wget -O - https://apt.kitware.com/keys/kitware-archive-latest.asc 2>/dev/null | apt-key add -

# 3. 将kitware存储库添加到源列表并进行更新。
sudo apt-add-repository 'deb https://apt.kitware.com/ubuntu/bionic main'
sudo apt-get update

# 4. 安装 kitware 密钥更新包
sudo apt-get install kitware-archive-keyring
sudo apt-key --keyring /etc/apt/trusted.gpg del C1F34CDD40CD72DA

# 5. 安装所有的依赖包
sudo apt-get install locales cmake llvm-9 clang-9 autoconf automake libtool build-essential python curl git lldb-6.0 liblldb-6.0-dev libunwind8 libunwind8-dev gettext libicu-dev liblttng-ust-dev libssl-dev libnuma-dev libkrb5-dev 

# 编译项目
./build.sh -subsetCategory CoreClr
./build.sh -subsetCategory Libraries
./build.sh -subsetCategory Installers

# 安装运行时，注意目录问题
tar zxf /home/runtime/artifacts/packages/Debug/Shipping/dotnet-runtime-5.0.0-dev-linux-x64.tar.gz -C  /usr/share/dotnet
ln -s  /usr/share/dotnet/dotnet /usr/local/bin/dotnet
```

dev 运行时安装包的路径：runtime/artifacts/packages/Debug/Shipping

使用开发版运行时调试的项目配置(csproj)

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp5.0</TargetFramework>
     <!--添加下面两行-->
    <UseAppHost>false</UseAppHost>
    <RuntimeFrameworkVersion>5.0.0-dev</RuntimeFrameworkVersion>
  </PropertyGroup>

</Project>

```




## 在Windows环境调试

1. 安装官网SDK,本地编译的仅为runtime
2. 安装本地编译生成的dev运行时
3. 使用vscode调试
   1. 修改lauch.json,添加justMyCode属性,设置未false
   2. 修改项目文件
   ```c#
   <PropertyGroup>
      <RuntimeFrameworkVersion>5.0.0-dev</RuntimeFrameworkVersion>
      <UseAppHost>false</UseAppHost>
   </ProgertyGroup>
   ```

# .NET Core命令行工具

.NET Core命令行工具简称.NET Core CLI,是开发人员与.NET Core交互的唯一用户界面。.NET Core CLI可以创建、恢复和发布.NET Core引用程序.

.NET Core CLI是一个独立的开源项目,可以独立安装.更多时候是随.NET Core SK一起安装的.

## 创建.NET Core项目

``dotnet new`` 命令用来创建.NET Core的项目相关文件

## .NET Core项目的迁移

对于早期的版本如.NET Core 1.0或者1.1版本的应用程序,dotnet命令行工具提供了``dotnet migrate``命令来帮助开发者从低版本的项目文件迁移到高版本的项目文件

## .NET Core项目的构建

``dotnet build``命令用来构建指定的项目和指定项目的依赖项目.通过构建，得到.NET Core的二进制可执行输出

## .NET Core项目的发布

``dotnet publish``既发布命令.用于将构建产生的二进制输出和依赖库打包输出到运行应用的宿主操作系统文件夹中.

## 对.NET Core项目进行管理

一个功能相对完整的.NET Core应用往往不是只有一个.NET Core项目,而是由一组项目来实现.这就需要实现对项目的组织和项目引用关系的管理。

1. dotnet sln命令用来管理解决方案下的各个项目。功能包括查看、添加和删除解决方案下的项目。
2. dotnet add项目之间的引用管理
3. dotnet add引用已经发布的nuget包
4. dotnet restore项目引用Nuget包的恢复
5. dotnet run运行一个源代码的项目
6. dotnet pack用来把指定的.NET Core代码项目生成NuGet包
7. dotnet nuget push用来将一个NuGet包推送到服务器并向用户进行发布
8. dotnet nuget locals用来查看或删除本机的NuGet包及相关信息
