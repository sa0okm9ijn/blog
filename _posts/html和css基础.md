---
title: html和css基础
date: 2019-06-14 17:57:22
tags: 
- css 
- html 
categories: css 
description: html超文本标记语言，层叠样式表 (Cascading Style Sheets，缩写为 CSS），是一种 样式表 语言，用来描述 HTML 或 XML（包括如 SVG、MathML、XHTML 之类的 XML 分支语言）文档的呈现。CSS 描述了在屏幕、纸质、音频等其它媒体上的元素应该如何被渲染的问题。
---
>HTML（HyperText Markup Language，超文本标记语言） 是用来定义网页结构的一种描述语言。



```
<meta charset="UTF-8">
```

此特性声明当前文档所使用的字符编码，常用的字符编码有utf-8、gb2312、gbk(繁体)，推荐使用utf-8


## 基本标签
* strong 粗体
* em 斜体
* del 中划线
* address 地址
* ol li 有序列表
* ul li 无序
* a
a标签的作用
1、超链接
2、锚点
3、打电话
4、发邮件

## 单标签
* meta
* br
* hr

## pre标签
预格式化文本元元素
空白折叠:在源代码中连续空白字符(空格、换行、制表)，在页面显示时，会被折叠为一个空格
例外 ：在pre元素内容中不会出现空白折叠
在pre元素内部出现的内容，会按照源代码格式显示到页面上
该元素通常用于在网页中显示一些代码
pre元素功能的本质:他有一个默认的css属性

## html实体
一个HTML 实体 是一段文本（“串”），以与符号（开始&），并用分号（结束;）。实体经常用于显示保留字符（否则将被解释为HTML代码），如&copy代表版权符号。具体参考连接：https://dev.w3.org/html5/html-author/charref


## HTML map
map元素使用具有area元素来定义图像映射（可点击链接区域）。
```
<map name="primary">
    <area shape="circle" coords="433,373,75" href="text.html" alt="">
    <area shape="circle" coords="" href="text1.html" alt="">
</map>
<img src="img/美女_5.jpg" usemap="#primary" alt="">
```

## html figure元素
主要用于html5的语义化
通常用域把图片、图片标题、描述包裹起来,figure里面可以用h等元素
figcaption指标题 里面可以放h等标签
```
<figure>
    <img src="img/美女_5.jpg" alt="A robotic monster over the letters MDN.">
    <figcaption>MDN Logo</figcaption>
</figure>
```

## html 布尔属性
某些元素，只有2种状态:1、不写 2、取值为属性名,这种属性叫布尔属性

## html video 属性
controls:控制控件的显示
autoplay:自动播放
muted:静音播放
loop:循环播放

格式兼容写法

```
<video controls autoplay loop muted style="width: 100px">
    <source src="media/open.mp4">
    <source src="media/open.webm">
    <p>
        对不起你的浏览器不支持
    </p>

</video>
```


## 语义化容器元素

header:页头，也可以用表示文章的头部
footer:页脚，也可以用表示文章的底部
article:通常用于表示整篇文章
section:通常用于表示文章的章节
aside:通常用于表示侧边栏

## html之空格
html中空格代表文本分隔符,主要用来分割英文单词,html中要想用空格,需要一些特殊的转义，如

```
&nbsp;空格
&lt;<
&gt;>
```
### 简单示例1

```
请输入用户名的实现
```

## 主流浏览器
| 名称               | 内核 |
| --------          |:-----|
| ie                |trident|
| firefox           |Gecko|
| google chrome     |webkit/blink|
| safari             |webkit|
| opera              |presto|


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