---
title: VisualStudio2017离线安装
date: 2019-05-29 13:52:13
tags: 
- VisualStudio2017 
categories: VisualStudio2017 
description: 
---

下载引导程序后，使用命令行来创建本地缓存，然后用本地缓存安装Visual Studio

## 步骤1-下载Visual Studio引导程序

选择你想要下载的版本，[点此进入](https://visualstudio.microsoft.com/zh-hans/downloads/)进行选择下载

版本 | File  
---|---  
Visual Studio Community(社区) |[vs_community.exe](https://visualstudio.microsoft.com/zh-hansthank-you-downloading-visual-studio/?sku=community&rel=15utm_medium=microsoftutm_source=docs.microsoft.comutm_campaign=offline+install&utm_content=download+vs2017rr=https%3A%2F%2Fdocs.microsoftcom%2Fen-us%2Fvisualstudio%2Finstall%2Fcreate-an-offline-installation-of-visual-studio%3Fview%3Dvs-2017)  
Visual Studio Professional |[vs_professional.exe](https://visualstudio.microsoft.com/zh-hans/thank-you-downloading-visual-studio/?sku=professional&rel=15&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=offline+installutm_content=download+vs2017&rr=https%3A%2F%2Fdocs.microsoft.com%2Fen-us%2Fvisualstudio%2Finstall%2Fcreate-an-offline-installation-of-visual-studio%3Fview%3Dvs-2017)  
Visual Studio Enterprise(企业) |[vs_enterprise.exe](https://visualstudio.microsoft.com/zh-hans/thank-you-downloading-visual-studio/?sku=enterprise&rel=15&utm_medium=microsoft&utm_source=docs.microsoft.comutm_campaign=offline+install&utm_content=download+vs2017&rr=https%3A%2F%2Fdocs.microsoft.com%2Fen-us%2Fvisualstudio%2Finstall%2Fcreate-an-offline-installation-of-visual-studio%3Fview%3Dvs-2017)  
  
  

## 步骤二-创建本地缓存

打开命令提示符并使用以下示例中的一个命令，此处列出的示例假定您使用的是Visual Studio
Enterprise（要防止出错，请确保完整安装路径少于80个字符。），应保证命令提示符所在目录包含引导文件。

  * 对于.NET Web和.NET桌面开发，请运行：

    
    
    1 E:\Users\sa\Downloads\vs_enterprise.exe --layout d:\vs2017layout --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Microsoft.VisualStudio.Workload.NetWeb --add Component.GitHub.VisualStudio --includeOptional --lang en-US

  * 对于c++桌面开发，请运行：     

    
    
    1 E:\Users\sa\Downloads\vs_enterprise.exe --layout c:\vs2017layout --add Microsoft.VisualStudio.Workload.NativeDesktop --includeRecommended --lang en-US

  * 要创建包含所有功能的完成本地布局（这需要很长时间），请运行：  

    
    
    1 E:\Users\sa\Downloads\vs_enterprise.exe --layout c:\vs2017layout --lang en-US

引导程序后后跟的参数，[点此进入](https://docs.microsoft.com/en-us/visualstudio/install/use-
command-line-parameters-to-install-visual-studio?view=vs-2017)查看

如果要安装除了英语-en-us以外的语言，参考以下

语言区域 | 语言  
---|---  
CS-CZ | 捷克  
DE-DE | 德语  
EN-US | 英语  
ES-ES | 西班牙语  
FR-FR | 法国  
IT-IT | 意大利  
JA-JP | 日本  
KO-KR | 朝鲜  
PL-PL | 波兰语  
PT-BR | 葡萄牙-巴西  
RU-RU | 俄语  
TR-TR | 土耳其  
ZH-CH | 简体中文  
ZH-TW | 繁体中文
