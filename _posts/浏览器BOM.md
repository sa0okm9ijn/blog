---
title: 浏览器BOM
date: 2019-10-11 12:40:20
tags: 
- JavaScript 
categories: JavaScript 
description: BOM是browserobjectmodel的缩写，简称浏览器对象模型。主要处理浏览器窗口和框架，描述了与浏览器进行交互的方法和接口，可以对浏览器窗口进行访问和操作，譬如可以弹出新的窗口，回退历史记录，获取url……
---

# BOM

BOM是browserobjectmodel的缩写，简称浏览器对象模型。主要处理浏览器窗口和框架，描述了与浏览器进行交互的方法和接口，可以对浏览器窗口进行访问和操作，譬如

可以弹出新的窗口，回退历史记录，获取url……

# BOM和DOM

1. javacsript是通过访问BOM对象来访问、控制、修改浏览器
2. BOM的window包含了document，因此通过window对象的document属性就可以访问、检索、修改文档内容与结构。
3. document对象又是DOM模型的根节点。

因此，BOM包含了DOM，浏览器提供出来给予访问的是BOM对象，从BOM对象再访问到DOM对象，从而js可以操作浏览器以及浏览器读取到的文档

# BOM对象包含以下内容

1. Window:JavaScript层级中的顶层对象，表示浏览器窗口。
2. Navigator包含客户端浏览器的信息。
3. History包含了浏览器窗口访问过的URL。
4. Location包含了当前URL的信息。
5. Screen包含客户端显示屏的信息。

## window 对象属性

1. innerHeight:返回视口的高度
2. innerWidth:返回视口的宽度
3. window.pageXOffset:设置或返回当前页面相对于窗口显示区左上角的X位置。
4. window.pageYOffset:设置或返回当前页面相对于窗口显示区左上角的Y位置。
5. window.screenLeft(window.screenX):声明了窗口的左上角在屏幕上的的x坐标
6. window.screenRight(window.screenY):声明了窗口的左上角在屏幕上的y坐标
7. window.alert():显示带有一段消息和一个确认按钮的警告框
8. window.confirm():显示带有一段消息以及确认按钮和取消按钮的对话框
9. window.prompt():显示可提示用户输入的对话框
10. window.onbeforeunload():当窗口即将被卸载（关闭）时,会触发该事件.
11. window.open('https://www.baidu.com','duyi','width=200,height=200'):打开一个新的浏览器窗口或查找一个已命名的窗口
    

## navigator

1. userAgent:返回由客户机发送服务器的user-agent头部的值。
2. online:返回指明系统是否处于脱机模式的布尔值。


![](navigator.jpg)

## history

go方法
back方法
forword方法

## location

![](location.jpg)
