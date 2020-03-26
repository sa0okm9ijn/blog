---
title: NetFrameWork-基础知识
date: 2020-03-23 23:25:23
tags: 
- .NET FrameWork基础知识
categories: .NET
description: 
---

## 平台介绍

我们先介绍下.NetFrameWork

![](1.png)

最下层蓝色部分是.NET Framework的基础，也是所有应用软件的基础。.NET Framework不是凭空出来的，实际上API，COM+，和一些相关驱动依然是它的基石。.NET Framework只不过是对这些前辈们进行了系统的封装和扩充，在这个过程中，吸取了Java框架的很多经验。

黄色部分就是.Net给我们封装好的可以调用的API了.如可以做桌面的、WEB的、连接数据的等等.

下面我们一步步引入CLS、CTS、CLR的概念。

.NetFrameWork是基于通用语言基础架构(Common Language Infrastructure，CLI),它是由Microsoft开发的开放规范(技术标准)，由ISO和Ecma标准化，它描述了可执行代码和运行时环境，该环境允许多种高级语言在不同的计算机平台上使用，而不必为特定的体系结构重写。这意味着它是平台无关的。.NetFrameWork(未跨平台)、.NetCore、Mono等是CLI的实现。

CLI规范主要描述了以下三个方面:
1. Common Type System (CTS),所有遵循cts的编程语言共享的一组数据类型和操作。
2. Common Language Specification (CLS),一组基本规则，任何针对CLI的语言都应该遵循这些规则，以便与其他兼容cls的语言进行互操作。CLS规则定义了公共类型系统的一个子集。
3. Virtual Execution System (VES),加载并执行与clic兼容的程序，使用元数据在运行时合并单独生成的代码片段。

所有兼容的语言都编译成通用中间语言(CIL)，这是一种从平台硬件中抽象出来的中间语言。当执行代码时，特定于平台的VES将根据特定的硬件和操作系统将CIL编译成机器语言。

![](2.png)

CLR:微软的CLI的实现被称之为CLR;

CLR中包含的CTS、CLS、CIL、VES等都是为了实现CLI

## 数据类型

### 数值型

- byte 无符号8位(指的转换为二进制的位数)整型,0-255
- sbyte 有符号8位整型 -128-127
- short 16位
- ushort 无符号16位
- int 32位
- uint 无符号32位
- ulong 无符号64位
- long 有符号64位

### 浮点型

- float 单精度
- double 双精度
- decimal 专用于货币
