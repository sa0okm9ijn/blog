---
title: html和css基础
date: 2019-06-14 17:57:22
tags: 
- css 
- html 
categories: css 
description: html超文本标记语言，层叠样式表 (Cascading Style Sheets，缩写为 CSS），是一种 样式表 语言，用来描述 HTML 或 XML（包括如 SVG、MathML、XHTML 之类的 XML 分支语言）文档的呈现。CSS 描述了在屏幕、纸质、音频等其它媒体上的元素应该如何被渲染的问题。
---

# HTML & CSS课程概述

## 术语

1.web

互联网

2.w3c

万维网联盟，非盈利的组织:w3.org，为互联网提供各种标准

3.xml

可扩展的标记语言：extension markup language，用于定义文档结构

```
请在每周周一下午两点，从人人网下载最新美剧《权力的游戏》
```

```xml
<任务>
    <执行日期> 每周一 </执行日期>
    <执行时间> 下午两点 </执行时间>
    <下载地址> 人人网 </下载地址>
    <下载目标> 最新版《权力的游戏》 </下载目标>
</任务>
```

## 什么是HTML

HTML：是w3c组织定义的语言标准，（HyperText Markup Language，超文本标记语言） 是用来定义网页结构的一种描述语言。

## 什么是CSS

CSS：是w3c定义的语言标准，层叠样式表(Cascading Style Sheets，缩写为 CSS），CSS 描述了在屏幕、纸质、音频等其它媒体上的元素应该如何被渲染的问题

## 执行HTML CSS

HTML、CSS -> 浏览器内核 -> 页面

浏览器：

1.shell：外壳
2.core：内核(js执行引擎，渲染引擎)

| 名称               | 内核 |
| --------          |:-----|
| ie                |Trident|
| firefox           |Gecko|
| google chrome     |webkit/blink|
| safari             |webkit|
| opera              |presto|



# 第一个网页

## 元素

> 其他叫法:标签、标记

元素 = 起始标记（begin tag） + 结束标记（end tag） + 元素内容 + 元素属性

属性 = 属性名 + 属性值

属性的分类：

- 局部属性：某些元素特有的属性
- 全局属性：所有元素通用

有些元素没有结束标记，这样的元素叫做：**空元素**

空元素的两种写法：

```
<meta charset="UTF-8">
<meta charset="UTF-8" />
```
此特性声明当前文档所使用的字符编码，常用的字符编码有utf-8、gb2312、gbk(繁体)，推荐使用utf-8


## 标准的文档结构

```html
<!DOCTYPE html>
```

文档声明，告诉浏览器，当前文档使用的HTML标准是HTML5。

不写文档声明，将导致浏览器进入怪异渲染模式。

```html
<html lang="en">
</html
```

根元素，一个页面最多只能一个，并且该元素是所有其他元素的父元素或祖先元素。

HTML5版本中没有强制要求书写该元素

lang属性：language，全局属性，表示该元素内部使用的文字是使用哪一种自然语言书写而成的。

```html
<head>

</head>
```

文档头，文档头内部的内容，不会显示到页面上。

```html
<meta>
```

文档的元数据：附加信息。

```html
<title>Document</title>
```

网页标题

```html
<body>
</body>
```

文档体，页面上所有要参与显示的元素，都应该放置到文档体中。


html最终的初始结构
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>淘宝购物车</title>
</head>

<body>
</body>
</html>
```








# 语义化

## 什么是语义化

1.每一个html元素都有具体的含义

a元素：超链接

p元素：段落

h1元素：一级标题

2.所有元素与展示效果无关

元素展示到页面中的效果，应该由CSS决定。

因为浏览器带有默认的CSS样式，所以每个元素有一些默认样式。


**重要：选择什么元素，取决于内容的含义，而不是显示出的效果**

## 为什么需要语义化？

1. 为了搜索引擎优化（SEO）

搜索引擎：百度、搜搜、Bing、Google

每隔一段时间，搜索引擎会从整个互联网中，抓取页面源代码

2. 为了让浏览器理解网页

阅读模式、语音模式


# 文本元素

## h 

标题,h1~h6表示1级标题~6级标题

## p 

段落

>lorem,乱数假文,主要的目的为测试文章或文字在不同字型、版型下看起来的效果，通常网站还没建设好时会出现这段文字

## span 

无语义

仅用于设计样式

>以前：某些元素在显示时会独占一行（块级元素），而某些元素不会（行级元素）
>到了HTML5，已经弃用这种说法。在 HTML5，这种区别被一个更复杂的[内容类别](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Content_categories)代替

## pre

预格式化文本元素

空白折叠：在源代码中的连续空白字符（空格、换行、制表），在页面显示时，会被折叠为一个空格

例外:在pre元素中的内容不会出现空白折叠

该元素通常用于在网页中显示一些代码。

pre元素功能的本质：它有一个默认的css属性

> 显示代码时，通常外面套code元素，code表示代码区域。

```js
<code style="white-space:pre">
    var i = 2;
    if(i){
        console.log(i);
    }
</code>
```

# HTML实体

[实体字符](https://dev.w3.org/html5/html-author/charref)， HTML Entity

一个HTML 实体 是一段文本（“串”），以与符号（开始&），并用分号（结束;）。实体经常用于显示保留字符（否则将被解释为HTML代码），实体字符通常用于在页面中显示一些特殊符号。

- 小于符号

```
&lt;
```

- 大于符号

```
&gt;
```

- 空格符号

```
&nbsp;
```

- 版权符号

```
&copy;
```

- &符号

```
&amp;
```


# a元素

超链接

## href属性

通常表示跳转地址

1.普通链接

```html
<a href="https://www.baidu.com">百度</a>
```

2.锚链接

```html
<!--让文章内容尽可能的多，出现滚动条后点击 可以出现想要明显的效果-->
<a href="#chapter1">章节1</a>
<a href="#chapter2">章节2</a>


<h2 id="chapter1">章节1</h2>
<p>Lorem ipsum dolor sit amet</p>
<h2 id="chapter2">章节1</h2>
<p>Lorem ipsum dolor sit amet</p>
```

3.功能链接
点击后，触发某个功能

- 执行JS代码，javascript:
- 发送邮件，mailto:
- 拨号，tel:

```html
<a href="javascript:alert('你好！')">
    弹出：你好！
</a> -->

<a href="mailto:234234324324@qq.com">
    点击给我发送邮件
</a> 

<a href="tel:14354663333">
    点击给我拨打电话
</a>
```

## target属性

表示跳转窗口位置。

target的取值：

- _self：在当前页面窗口中打开，默认值
- _blank: 在新窗口中打开

```html
<a href="https://douyu.com" target="_blank" >
    斗鱼直播
</a>
```

# 路径的写法

## 站内资源和站外资源

站内资源：当前网站的资源

站外资源：非当前网站的资源

## 绝对路径和相对路径

站外资源：绝对路径

站内资源：相对路径

1.绝对路径

绝对路径的书写格式：

url地址：

```
协议名://主机名:端口号/路径
schema://host:port/path
```

当跳转目标和当前页面的协议相同时，可以省略协议

2.相对路径

以./开头，./表示当前资源所在的目录

可以书写../表示返回上一级目录

相对路径中：./可以省略


# 图片元素

## img元素

image缩写,空元素

src属性:source

alt属性:当资源失效时,将使用该属性的文字代替图片

## 和a元素联用


```html
<a target="_blank" href="https://baike.baidu.com/item/%E5%A4%AA%E9%98%B3%E7%B3%BB/173281?fr=aladdin">
            <img usemap="#solarMap" src="./img/solar.jpg" alt="这是一张太阳系的图片">
</a>
```


## 和map元素联用

map：地图

map的子元素：area

衡量坐标时，为了避免衡量误差，需要使用专业的衡量工具：

map元素使用具有area元素来定义图像映射（可点击链接区域）。

ps、pxcook

```html
<a target="_blank" href="https://baike.baidu.com/item/%E5%A4%AA%E9%98%B3%E7%B3%BB/173281?fr=aladdin">
    <img usemap="#solarMap" src="./img/solar.jpg" alt="这是一张太阳系的图片">
</a>
<map name="solarMap">
    <area shape="circle" coords="360,204,48" href="https://baike.baidu.com/item/%E6%9C%A8%E6%98%9F/222105?fr=aladdin" target="_blank">
    <area shape="rect" coords="323,282,395,320" href="https://baike.baidu.com/item/%E6%9C%A8%E6%98%9F/222105?fr=aladdin" target="_blank">
    <area shape="poly" coords="601,371,645,312,678,338,645,392" href="https://baike.baidu.com/item/%E5%86%A5%E7%8E%8B%E6%98%9F/137498?fr=aladdin" target="_blank">
</map>
```

## 和figure元素联用

指代、定义，通常用于把图片、图片标题、描述包裹起来

子元素：figcaption

主要用于html5的语义化

通常用域把图片、图片标题、描述包裹起来,figure里面可以用h等元素

figcaption指标题 里面可以放h等标签

```html
 <figure>
    <a target="_blank" href="https://baike.baidu.com/item/%E5%A4%AA%E9%98%B3%E7%B3%BB/173281?fr=aladdin">
        <img usemap="#solarMap" src="./img/solar.jpg" alt="这是一张太阳系的图片">
    </a>
    <figcaption>
        <h2>太阳系</h2>
    </figcaption>
    <p>
        太阳系是以太阳为中心，和所有受到太阳的引力约束天体的集合体。包括八大行星（由离太阳从近到远的顺序：水星、金星、地球、火星、木星、土星、天王星、海王星）、以及至少173颗已知的卫星、5颗已经辨认出来的矮行星和数以亿计的太阳系小天体,和哈雷彗星。
    </p>
</figure>
```








# 多媒体元素

video 视频

audio 音频

## video

controls: 控制控件的显示，取值只能为controls

某些属性，只有两种状态：1. 不写   2. 取值为属性名，这种属性叫做布尔属性

布尔属性，在HTML5中，可以不用书写属性值

autoplay: 布尔属性，自动播放。

muted: 布尔属性，静音播放。

loop: 布尔属性，循环播放

## audio

和视频完全一致

## 兼容性


1. 旧版本的浏览器不支持这两个元素
2. 不同的浏览器支持的音视频格式可能不一致

```html
<video controls autoplay loop muted style="width: 100px">
    <source src="media/open.mp4">
    <source src="media/open.webm">
    <p>
        对不起你的浏览器不支持
    </p>
</video>
```


# 列表元素

## 有序列表

ol: ordered list

li：list item 

## 无序列表

把ol改成ul

ul：unordered list

无序列表常用于制作菜单 或 新闻列表。


## 定义列表

通常用于一些术语的定义

dl: definition list

dt: definition title

dd: definition description


# 容器元素

容器元素：该元素代表一个块区域，内部用于放置其他元素

## div元素

没有语义

## 语义化容器元素

header: 通常用于表示页头，也可以用于表示文章的头部

footer: 通常用于表示页脚，也可以用于表示文章的尾部

article: 通常用于表示整篇文章

section: 通常用于表示文章的章节

aside: 通常用于表示侧边栏

# 元素包含关系

以前：块级元素可以包含行级元素，行级元素不可以包含块级元素，a元素除外

元素的包含关系由元素的内容类别决定。

例如，查看h1元素中是否可以包含p元素

总结：

1. 容器元素中可以包含任何元素
2. a元素中几乎可以包含任何元素
3. 某些元素有固定的子元素（ul>li，ol>li，dl>dt+dd）
4. 标题元素和段落元素不能相互嵌套，并且不能包含容器元素


# 为网页添加样式

## 术语解释

```css
h1{
    color:red;
    background-color:lightblue;
    text-align: center;
}
```

CSS规则 = 选择器 + 声明块


### 选择器

选择器：选中元素

1. ID选择器：选中的是对应id值的元素
2. 元素选择器
3. 类选择器

### 声明块

出现在大括号中

声明块中包含很多声明（属性），每一个声明（属性）表达了某一方面的样式。

## CSS代码书写位置

1. 内部样式表

书写在style元素中

2. 内联样式表，元素样式表

直接书写在元素的style属性中

3. 外部样式表[推荐]

将样式书写到独立的css文件中。

1). 外部样式可以解决多页面样式重复的问题
2). 有利于浏览器缓存，从而提高页面响应速度
3). 有利于代码分离（HTML和CSS），更容易阅读和维护


# 常见样式声明


## css选择器
html部分代码

```
<div id="divgame" class="classgame" att="">
    <span>1</span>
    <span class="cs cst">1</span> 
    <span class="csf css">2</span>
</div>
```

* id选择器 

```
#divgame {
    width: 100px;
    height: 100px;
    background: red;
}
```

* class选择器 

```
.classgame {
    width: 100px;
    height: 100px;
    background: red;
}
```

* 属性选择器 

```
[att] {
    width: 100px;
    height: 100px;
    background: red;
}
```

* 标签选择器

```
div {
    width: 100px;
    height: 100px;
    background: red;
}
```

* 通配符

```
*{
    margin:0;
    padding:0;
}
```

* 父子选择器/派生选择器

```
div span {
    color: red;
}
```

此处可以是以上任意标签的，不一定非要标签，此处找子元素不一定找一级

* 直接子元素选择器

```
div > span{
    color:red;
}
```
此处子元素只找子一级

* 并列选择器

```
span.cs.cst{
    color: red;
}
```

* 分组选择器

```
.cs,
.csf{
    color: red;
}
```

* 伪类选择器 

```
a:hover{
  background:red;
}
```

* 伪元素

```
div::before{

}
div::after{

}
```
伪元素天生存在标签中，通过css显示出来，天生的行级元素


**选择器查找标签结构从右向左找,这样查找效率高**

## 选择器优先级

* 简单选择器的比较

**!important > 行间样式 > id > class|属性选择器 > 标签选择器 > 通配符选择器**

* 复杂选择器的比较

通过计算对各个选择器的权重值(256进制)加起来的和进行比较

| 选择器               | 权重值 |
| --------             |:-----|
| !important Infinity  |正无穷大|
| 行间样式              |1000|
| id                   |100|
| class、属性、伪类      |10|
| 标签、伪元素            |1|
| 通配符                 |0|

## 简单示例2

```
border 画三角
```


## 文本类

* 垂直居中

```
height=line-height
```

* 首行缩进

```
text-indent:2px;
```

## 单位em

```
1em=1font-size(指的高);
```

## html中元素分类

* 行级元素

内容决定所占位置，不可以通过css改变宽高，如span、strong、em、a、del,display:inline为行级元素

* 块级元素

独占一行，可以通过css改变宽高，如div、p、ul、li、ol、form、address,display:block为块级元素

* 行级块元素

内容决定大小，可以改变宽高，display:inline-block为行级块元素

**凡是带有inline的元素，都有文字特性，如元素之间的间隙**


## html中的模型

* 盒子模型

![](html和css基础/2019-06-26_225531.png)

一个盒子包含了border、padding、(width+height)=content、margin

margin的符合属性

```

margin:上 右 下 左;
margin:上 (左右) 下;
margin：(上下) (左右)

```

* 层模型

1.position:absolute

脱离原来定位 相对于最近的父级有定位的元素进行定位，如果没有，那么由文档进行定位

2.position:relative

保留原来的位置进行定位，相对于自己原来的位置定位

3.position:fixed


* 浮动模型

float:  left/right

可以让元素向左或向右排成一行显示，换行依据为父元素的宽度

```
<style>
    .wrapper {
        width: 300px;
        height: 300px;
        border: solid 1px red;
    }

    .content {
        /**从左开始战队，换行依据为父元素的宽度**/
        float: left; 
        width: 100px;
        height: 100px;
        color: #fff;
        background-color: black;
    }
</style>


<div class="wrapper">
    <div class="content">123</div>
    <div class="content">123</div>
    <div class="content">132</div>
</div>
```
### 浮动元素特点
1、浮动元素产生了浮动流
2、所有产生了浮动流的元素，块级元素看不到他们，
3、产生了bfc的元素和文本类属性(inline)的元素以及文本都能看到浮动元素
4、清除浮动流.clear:both  解决父级包住浮动流方法
5、清除浮动的必须是块级元素，可以通过伪元素来处理 ，可以不改变html结构
6、浮动最开始用法   图片环绕文字

此处box产生了浮动流，后面的块级元素看不到他就会占据box的位置
```
.box{
    float: left;
    width: 100px;
    height: 100px;
    background-color:black;
    opacity: 0.5;

}
.demo{
    width: 150px;
    height: 150px;
    background-color: green;

}
<div class="box"></div>
<div class="demo"></div>
```

清除浮动解决父级元素包裹不住子元素的问题
```
<style>
    .wrapper {
        border: solid 1px red;
    }

    .content {
        /**块级元素看不到浮动元素，所以父级就包不住conten了，**/
        float: left;
        width: 100px;
        height: 100px;
        color: #fff;
        background-color: black;
    }
    p{
        border-top: 0px solid green;  
        clear: both;    
    
    }
</style>

<div class="wrapper">
    <div class="content">123</div>
    <div class="content">123</div>
    <div class="content">132</div>
    <p></p>
</div>
```

利用伪元素来清除浮动


```
.wrapper {
  border: solid 1px red;
}

.content {
  /**块级元素看不到浮动元素，所以父级就包不住conten了，**/
  float: left;
  width: 100px;
  height: 100px;
  color: #fff;
  background-color: black;
}
.wrapper::after{
  content: "";
  clear: both;
  display: block;
}

<div class="wrapper">
    <div class="content">123</div>
    <div class="content">123</div>
    <div class="content">132</div>
</div>

```

产生了bfc的元素和文本类属性(inline)的元素都可以解决浮动包裹的问题。但是position:absoulute float:left/righ元素转换成iniline-block;宽高就由内容决定了。所以设置这些之后宽高取决于内容

## 触发bfc(bfc block format context)

正常盒子都一个规则，触发bfc 规则失效,遵循另一套规则

1、position:absolute
2、display:inline-block
3、float
4、overflow:hidden

## 2个bug

1、margin塌陷

父子标签，垂直方向的margin 粘合在一起取 取最大的margin定位

```
<style>
    .wrapper{
        margin-left: 100px;
        margin-top: 100px;
        width: 100px;
        height: 100px;
        background: black;
    }
    .content{
        /* 此处的margin-top 并没有相对wrapper top 50px 这就是margin塌陷  此时的margin-top取最大值  父子元素一起移动*/
        margin-top: 50px;    
        width: 50px;
        height: 50px;
        background-color: green;
    }
</style>
<div class="wrapper">
    <div class="content"></div>
</div>
```
父级触发bfc拉解决此问题
2、margin合并

兄弟结构，垂直方向margin合并

```

<style>
    .box1 {
        background-color: red;
        margin-right: 100px;
    }

    .box2 {
        background-color: green;
        /**不能共用区域一共间隔150px**/
        margin-left: 50px;
    }

    .demo1 {
        background-color: red;
        margin-bottom: 200px;
    }

    .demo2 {
        background-color: green;
        /**此处公用了一块区域  一共间隔200px**/
        margin-top: 100px;
    }
</style>
<span class="box1">123</span>
<span class="box2">234</span>


<div class="demo1">123</div>
<div class="demo2">456</div>
```

也可以通过把需要解决的元素放到bfc的元素中，来解决此问题，但是这样就会改变了html结构，所以不解决，可以通过数学方法设置合适的像素。

## 简单示例3

```
五环   经典 2栏布局
```



## 文本类 

1、溢出文字打点处理

```
//单行文本
white-space:nowrap;
overflow:hidden;
text-overflow:ellipsis;
```


## 2个规则

p不能套div
a不能套a

## 网页设计没有css解决图片该汉字显示的问题

第一种方法
text-indent:200px;
white-space:nowrap;
overflow:hidden;

第二种方法
heigth:0;
paddint-top:
overflow:hidden;
、











## :hover伪类
:hover可以任何伪元素上使用。在触摸屏上 :hover 有问题，基本不可用。不同的浏览器上:hover 伪类表现不同。 可能从不会触发；或者在触摸某元素后触发了一小会儿；或者总是触发即使用户不在触摸了，直到用户触摸别的元素。 触摸屏非常普遍，所以网页开发人员不要让任何内容只能通过悬停才能展示出来，不然这些内容对于触摸屏使用者来说很难或者说不可能看到。

## 语法

```
:hover
```

## 示例

```
:link:hover { outline: dotted red; }

.foo:hover { background: gold; }

```

### 下拉按钮

使用:hover 伪类可以创建复杂的层叠机制。一个常见用途，比如，创建一个纯CSS的下拉按钮（不使用JavaScript）。 本质是创建如下的CSS：

```
div.menu-bar ul ul {
  display: none;
}

div.menu-bar li:hover > ul {
  display: block;
}

```

HTML内容如下

```
<div class="menu-bar">
  <ul>
    <li>
      <a href="example.html">Menu</a>
      <ul>
        <li>
          <a href="example.html">Link</a>
        </li>
        <li>
          <a class="menu-nav" href="example.html">Submenu</a>
          <ul>
            <li>
              <a class="menu-nav" href="example.html">Submenu</a>
              <ul>
                <li><a href="example.html">Link</a></li>
                <li><a href="example.html">Link</a></li>
                <li><a href="example.html">Link</a></li>
                <li><a href="example.html">Link</a></li>
              </ul>
            </li>
            <li><a href="example.html">Link</a></li>
          </ul>
        </li>
      </ul>
    </li>
  </ul>
</div>
```