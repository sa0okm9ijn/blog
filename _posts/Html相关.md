---
title: Html相关
date: 2019-05-29 10:11:33
tags: 
- Html 
categories: Html 
description: 
---
### <!DOCTYPE html>标签

如果你的页面添加了<!DOCTYPE html>,那么浏览器就会按照正常模式渲染.你的页面在所有的浏览器里显示的就都是一个样子了。这就是<!DOCTYPE
html>的作用。

如果你的页面没有DOCTYPE的声明，那么compatMode默认就是BackCompat,浏览器按照自己的方式解析渲染页面，那么，在不同的浏览器就会显示不同的样式。

    
```
window.top.document.compatMode：
//BackCompat：怪异模式，浏览器使用自己的怪异模式解析渲染页面。 
//CSS1Compat：标准模式，浏览器使用W3C的标准解析渲染页面。
```
### head标签

#### meta

 meta标签的组成：meta标签共有两个属性，它们分别是http-equiv属性和name 属性

* name
```
<meta name="keywords" content="关键字"> //搜索引擎识别的

<meta name="description" content="描述"> //网站描述
```
* http-equiv
```
<meta http-equiv="Refresh" content="2;URL=https://www.baidu.com">//指定秒数跳转指定页面

<meta http-equiv="content-Type" charset=UTF8"> //编码的作用

<meta http-equiv = "X-UA-Compatible" content = "IE=EmulateIE7" /> //兼容
```
#### Link
```
<link rel="icon" href="http://www.jd.com/favicon.ico">  //显示标题前的图片
```
### 块级元素(block)和内联元素(inline)

#### 块级元素

  * 总是在新行上开始；
  * 宽度缺省是它的容器的100%，除非设定一个宽度。
  * 它可以容纳内联元素和其他块元素

#### 内联元素

  * 和其他元素都在一行上；
  * 宽度就是它的文字或图片的宽度，不可改变
  * 内联元素只能容纳文本或者其他内联元素
