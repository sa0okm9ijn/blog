---
title: html和css基础
date: 2019-06-14 17:57:22
tags: 
- Css 
- Html 
categories: HTML 
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









## 和picture元素联用

picture通过包含零或多个source元素和一个 img 元素来为不同的显示/设备场景提供图像版本。浏览器会选择最匹配的子 source 元素，如果没有匹配

的，就选择 img 元素的 src 属性中的URL。然后，所选图像呈现在img元素占据的空间中。

```html
<picture>
    <source
        srcset="/some/_1170x658_crop_center-center/man-with-a-dog.webp 1170w,
                /some/_970x545_crop_center-center/man-with-a-dog.webp 970w,
                /some/_750x562_crop_center-center/man-with-a-dog.webp 750w,
                /some/_320x240_crop_center-center/man-with-a-dog.webp 320w"
        sizes="100vw"
        type="image/webp"
    />
    <source
        srcset="/some/_1170x658_crop_center-center/man-with-a-dog.jpg 1170w,
                /some/_970x545_crop_center-center/man-with-a-dog.jpg 970w,
                /some/_750x562_crop_center-center/man-with-a-dog.jpg 750w,
                /some/_320x240_crop_center-center/man-with-a-dog.jpg 320w"
        sizes="100vw"
    />
    <img
        src="/some/man-with-a-dog-placeholder.jpg"
        alt="Man with a dog"
        style="object-fit: cover;"
        loading="lazy"
    />
</picture>
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

## 基本样式

1. color

元素内部的文字颜色

**预设值**：定义好的单词

**三原色，色值**：光学三原色（红、绿、蓝），每个颜色可以使用0-255之间的数字来表达，色值。

```
rgb表示法：
rgb(0, 255, 0)
hex（16进制）表示法：
#红绿蓝
```

淘宝红：#ff4400, #f40
黑色：#000000，#000
白色：#ffffff, #fff
红：#ff0000, #f00
绿：#00ff00, #0f0
蓝：#0000ff, #00f
紫：#f0f
青：#0ff
黄：#ff0
灰色：#ccc

2. background-color

元素背景颜色

3. font-size

元素内部文字的尺寸大小

1）px：像素，绝对单位，简单的理解为文字的高度占多少个像素
2）em：相对单位，相对于父元素的字体大小
每个元素必须有字体大小，如果没有声明，则直接使用父元素的字体大小，如果没有父元素（html），则使用基准字号（浏览器设置的字体大小）。

> user agent，UA，用户代理（浏览器）

4. font-weight

文字粗细程度，可以取值数字，可以取值为预设值

> strong，默认加粗。

5. font-family

文字类型

必须用户计算机中存在的字体才会有效。

使用多个字体，以匹配不同环境

sans-serif，非衬线字体（每个操作系统都有一个默认的非衬线字体.一般写在最后）

6. font-style

字体样式，通常用它设置斜体

> i元素，em元素，默认样式，是倾斜字体; 实际使用中，通常用它表示一个图标（icon）

7. text-decoration

文本修饰，给文本加线。

> a元素
> del元素：错误的内容
> s元素：过期的内容

8. text-indent

首行文本缩进

9. line-height

每行文本的高度，该值越大，每行文本的距离越大。

设置行高为容器的高度，可以让单行文本垂直居中(单行文本行高设置)

行高可以设置为纯数字，表示相对于当前元素的字体大小(多行文字行高设置)

10. width

宽度

11. height


高度

12. letter-space

文字间隙

13. text-align
 
元素内部文字的水平排列方式

## 更多样式

1. 透明度

1. opacity，它设置的是整个元素的透明，它的取值是0 ~ 1
2. 在颜色位置设置alpha通道(rgba )

2. 鼠标

使用cursor设置

3. 盒子隐藏

1. display:none，不生成盒子
2. visibility:hidden，生成盒子，只是从视觉上移除盒子，盒子仍然占据空间。

4. 背景图

img元素是属于HTML的概念

背景图属于css的概念

1. 当图片属于网页内容时，必须使用img元素
2. 当图片仅用于美化页面时，必须使用背景图


5. 背景图涉及的css属性

1. background-image

2. background-repeat

默认情况下，背景图会在横坐标和纵坐标中进行重复

3. background-size

预设值：contain、cover，类似于object-fit
数值或百分比

4. background-position

设置背景图的位置。

预设值：left、bottom、right、top、center

数值或百分比

雪碧图（精灵图）（spirit）

5. background-attachment

通常用它控制背景图是否固定。

6. 背景图和背景颜色混用

7. 速写（简写）background

# 选择器

选择器：帮助你精准的选中想要的元素

## 简单选择器

1. ID选择器
2. 元素选择器 
3. 类选择器
4. 通配选择器

*，选中所有元素

5. 属性选择器

根据属性名和属性值选中元素

```css
/**选择所有有href属性的元素**/
[href] {
    width: 100px;
    height: 100px;
    background: red;
}
/* 所有href属性等于www.baidu.com的元素 */
[href='www.baidu.com'] {
    width: 100px;
    height: 100px;
    background: red;
}
```

6. 伪类选择器

选中某些元素的某种状态

1）link: 超链接未访问时的状态

2）visited: 超链接访问过后的状态

3）hover: 鼠标悬停状态

4）active：激活状态，鼠标按下状态

爱恨法则：love hate

7. 伪元素选择器

before

after

伪元素天生存在标签中，通过css显示出来，天生的行级元素

iconfont 字体图标库,里面的图标通过伪元素content属性把图标显示到界面上,我们可以通过改变伪元素为定位元素来改变位置

```css
div::before{

}
div::after{

}
```

## 选择器的组合

1. 并且 - **.**

```css
/* p标签且class等于red的元素 */
p.red {
    color: red;
}
```
2. 后代元素 - **空格 此处找子元素不一定找一级**
3. 子元素 - **>  直接子元素选择器**
4. 相邻兄弟元素 - **+**
5. 后面出现的所有兄弟元素 - **~**

## 选择器的并列

多个选择器, 用逗号分隔

## 选择器的查找顺序

![](2019-08-13_090752.png)

**选择器查找标签结构从右向左找,这样查找效率高**




## 更多的伪类选择器
1. :first-child表示一组同级元素中的第一元素

2. :first-of-type表示一组兄弟元素中其类型的第一个元素

``` html
<article>
  <div>This `div` is first!</div>
  <div>This <span>nested `span` is first</span>!</div>
  <div>This <em>nested `em` is first</em>, but this <em>nested `em` is last</em>!</div>
  <div>This <span>nested `span` gets styled</span>!</div>
  <b>This `b` qualifies!</b>
  <div>This is the final `div`.</div>
</article>

```

```css

article :first-of-type {
  background-color: pink;
}
```
此处注意选择器之间的空格，代表的意思是artilce 后代的所有第一个元素背景变色

2. :last-child 表示一组同级元素中的最后一个元素


3. :nth-child 匹配基于其一组的兄弟姐妹中位置的元素(计算位置，不考虑匹配元素类型，只看是第几个)

4  :nth-of-type 匹配基于其一组的兄弟姐妹中位置的元素（计算位置，只考虑匹配元素类型）



odd
表示在一系列兄弟姐妹中的数字位置为奇数的元素：1,3,5等。
even
表示在一系列兄弟姐妹中的数字位置是偶数的元素：2,4,6等。



>如最初定义的那样，所选元素必须具有父元素。从Selectors Level 4(W3C  选择器标准 第四版--css next)开始，不再需要。



## 更多的伪元素选择器

1. first-letter

选中元素中的第一个字母

2. first-line

选中元素中第一行的文字

3. selection

选中被用户框选的文字

# 层叠

声明冲突：同一个样式，多次应用到同一个元素

层叠：解决声明冲突的过程，浏览器自动处理（权重计算）

## 比较重要性

重要性从高到底：

> 作者样式表：开发者书写的样式

1） 作者样式表中的!important样式
2)  作者样式表中的普通样式
3)  浏览器默认样式表中的样式

## 2. 比较特殊性

看选择器

总体规则：选择器选中的范围越窄，越特殊

具体规则：通过选择器，计算出一个4位数（x x x x）

1. 千位：如果是内联样式，记1，否则记0
2. 百位：等于选择器中所有id选择器的数量
3. 十位：等于选择器中所有类选择器、属性选择器、伪类选择器的数量
4. 个位：等于选择器中所有元素选择器、伪元素选择器的数量

## 3. 比较源次序

代码书写靠后的胜出

**总结**

!important最高 > 其次是内联样式  > 然后计算特殊性 > 书写的原次序  > 通配符选择器

![](hundrod.png)![](ten.png)![](single.png)

以上选择器数量都是一个，如果是多个一起则会在对应位置上显示对应的数量，通过这个数量来比较元素的优先级

## 应用

1. 重置样式表

书写一些作者样式，覆盖浏览器的默认样式

重置样式表 -> 浏览器的默认样式

常见的重置样式表：normalize.css、reset.css、meyer.css

2. 爱恨法则

link > visited > hover > active

在同一时刻会有，可能会有多个状态，这个写法符合源次序的规则

# 继承

子元素会继承父元素的某些CSS属性

通常，跟文字内容相关的属性都能被继承

# 属性值的计算过程

一个元素一个元素依次渲染，顺序按照页面文档的树形目录结构进行

![](2019-05-17-12-27-14.png)

渲染每个元素的前提条件：该元素的所有CSS属性必须有值

一个元素，从所有属性都没有值，到所有的属性都有值，这个计算过程，叫做属性值计算过程
特殊的两个CSS取值：

- inherit：手动（强制）继承，将父元素的值取出应用到该元素
- initial：初始值，将该属性设置为默认值

下图是属性值的计算过程

![](stack.gif)

# 盒模型

box：盒子，每个元素在页面中都会生成一个矩形区域（盒子）

盒子类型：

1. 行盒，display等于inline的元素
2. 块盒，display等于block的元素

行盒在页面中不换行、块盒独占一行

display默认值为inline

浏览器默认样式表设置的块盒：容器元素、h1~h6、p

常见的行盒：span、a、img、video、audio

## 盒子的组成部分

无论是行盒、还是块盒，都由下面几个部分组成，从内到外分别是：

![](2019-06-26_225531.png)

1. 内容  content

width、height，设置的是盒子内容的宽高

内容部分通常叫做整个盒子的**内容盒 content-box**

2. 填充(内边距)  padding

盒子边框到盒子内容的距离

padding-left、padding-right、padding-top、padding-bottom

padding: 简写属性

padding: 上 右 下 左

填充区+内容区 = **填充盒 padding-box**

3. 边框  border

边框 = 边框样式 + 边框宽度 + 边框颜色

边框样式：border-style
边框宽度：border-width
边框颜色：border-color

边框+填充区+内容区 = **边框盒 border-box**

4. 外边距  margin

边框到其他盒子的距离

margin-top、margin-left、margin-right、margin-bottom

# 盒模型应用

## 改变宽高范围

默认情况下，width 和 height 设置的是内容盒宽高。

> 页面重构师：将psd文件（设计稿）制作为静态页面

衡量设计稿尺寸的时候，往往使用的是边框盒，但设置width和height，则设置的是内容盒

1. 精确计算
2. CSS3：box-sizing

## 改变背景覆盖范围

默认情况下，背景覆盖边框盒

可以通过background-clip进行修改

## 溢出处理

overflow，控制内容溢出边框盒后的处理方式

单行文本溢出显示...的实现

```css
white-space: nowrap;
overflow: hidden;
text-overflow: ellipsis;
```

## 断词规则

word-break，会影响文字在什么位置被截断换行

normal：普通。CJK字符（文字位置截断），非CJK字符（单词位置截断）

break-all：截断所有。所有字符都在文字处截断

keep-all：保持所有。所有文字都在单词之间截断 通过空格来区分是否一个单词


# 行盒的盒模型

常见的行盒：包含具体内容的元素

span、strong、em、i、img、video、audio

## 显著特点

1. 盒子沿着内容沿伸
2. 行盒不能设置宽高

调整行盒的宽高，应该使用字体大小、行高、字体类型，间接调整。

**凡是带有inline的元素，都有文字特性，如元素之间的间隙**

3. 内边距（填充区）

水平方向有效，垂直方向仅会影响背景，垂直方向不会实际占据空间。

4. 边框

水平方向有效，垂直方向不会实际占据空间。

5. 外边距

水平方向有效，垂直方向不会实际占据空间。

## 行块盒

display：inline-block 的盒子

1. 不独占一行
2. 盒模型中所有尺寸都有效


## 空白折叠

空白折叠，发生在行盒（行块盒）内部 或 行盒（行块盒）之间

## 可替换元素 和 非可替换元素

大部分元素，页面上显示的结果，取决于元素内容，称为**非可替换元素**

少部分元素，页面上显示的结果，取决于元素属性，称为**可替换元素**

可替换元素：img、video、audio

绝大部分可替换元素均为行盒。

可替换元素类似于行块盒，盒模型中所有尺寸都有效。

# 常规流

盒模型：规定单个盒子的规则

视觉格式化模型（布局规则）：页面中的多个盒子排列规则

视觉格式化模型，大体上将页面中盒子的排列分为三种方式：

1. 常规流
2. 浮动
3. 定位

## 常规流布局

常规流、文档流、普通文档流、常规文档流

所有元素，默认情况下，都属于常规流布局

总体规则：块盒独占一行，行盒水平依次排列

包含块（containing block）：每个盒子都有它的包含块，包含块决定了盒子的排列区域。

绝大部分情况下：盒子的包含块，为其父元素的内容盒

**块盒**

1. 每个块盒的总宽度，必须刚好等于包含块的宽度

宽度的默认值是auto

margin的取值也可以是auto，默认值0

auto：将剩余空间吸收掉

width吸收能力强于margin

若宽度、边框、内边距、外边距计算后，仍然有剩余空间，该剩余空间被margin-right全部吸收

在常规流中，块盒在其包含快中居中，可以定宽、然后左右margin设置为auto。 宽度定了 就有margin来吸收 最后居中

```css
.father{
    padding: 30px;
    height: 800px;
    border: solid 1px red;
}
.son {
    height: 100px;
    background: red;
    border: 2px solid;
    margin: auto;
}
```

```html
<div class="father">
    <div class="son"></div>
</div>
```

2. 每个块盒垂直方向上的auto值

height:auto， 适应内容的高度

margin:auto， 表示0

3. 百分比取值

padding、宽、margin可以取值为百分比

以上的所有百分比相对于包含块的宽度。


高度的百分比：

1）. 包含块的高度是否取决于子元素的高度，设置百分比无效（包含块没有设置高度，无效）
2）. 包含块的高度不取决于子元素的高度，百分比相对于父元素高度

# 浮动

## 应用场景

1. 文字环绕
2. 横向排列

## 浮动的基本特点

修改float属性值为：

- left：左浮动，元素靠上靠左
- right：右浮动，元素靠上靠右

默认值为none

1. 当一个元素浮动后，元素必定为块盒(更改display属性为block)
2. 浮动元素的包含块，和常规流一样，为父元素的内容盒

## 盒子尺寸

1. 宽度为auto时，适应内容宽度(浮动盒子里面有内容)
2. 高度为auto时，与常规流一致，适应内容的高度(浮动盒子里面有内容)
3. margin为auto，为0.
4. 边框、内边距、百分比设置与常规流一样

## 盒子排列

1、浮动元素产生了浮动流
2、所有产生了浮动流的元素，块级元素看不到他们，
3、产生了bfc的元素和文本类属性(inline)的元素以及文本都能看到浮动元素
4、清除浮动流.clear:both  解决父级包住浮动流方法
5、清除浮动的必须是块级元素，可以通过伪元素来处理 ，可以不改变html结构
6、浮动最开始用法   图片环绕文字

产生了bfc的元素和文本类属性(inline)的元素都可以解决浮动包裹的问题

但是 position:absoulute float:left/righ元素转换成iniline-block;宽高就由内容决定了。所以设置这些之后宽高取决于内容

> 如果文字没有在行盒中，浏览器会自动生成一个行盒包裹文字，该行盒叫做匿名行盒。

## 高度坍塌

高度坍塌的根源：常规流盒子的自动高度，在计算时，不会考虑浮动盒子

清除浮动，涉及css属性：clear

清除浮动的必须是块级元素，可以通过伪元素来处理 ，可以不改变html结构

- 默认值：none
- left：清除左浮动，该元素必须出现在前面所有左浮动盒子的下方
- right：清除右浮动，该元素必须出现在前面所有右浮动盒子的下方
- both：清除左右浮动，该元素必须出现在前面所有浮动盒子的下方

## 浮动位置
左浮动的盒子向上向左排列

右浮动的盒子向上向右排列

浮动盒子的顶边不得高于上一个盒子的顶边

若剩余空间无法放下浮动的盒子，则该盒子向下移动，直到具备足够的空间能容纳盒子，然后再向左或向右移动

![](float.gif)

# 定位

定位：手动控制元素在包含块中的精准位置

涉及的CSS属性：position

## position属性

- 默认值：static，静态定位（不定位）
- relative：相对定位
- absolute：绝对定位
- fixed：固定定位

一个元素，只要position的取值不是static，认为该元素是一个定位元素。

定位元素会脱离文档流（相对定位除外）

一个脱离了文档流的元素：

1. 文档流中的元素摆放时，会忽略脱离了文档流的元素
2. 文档流中元素计算自动高度时，会忽略脱离了文档流的元素

## 相对定位

不会导致元素脱离文档流，只是让元素在原来位置上进行偏移。

可以通过四个CSS属性对设置其位置：

- left
- right
- top
- bottom

盒子的偏移不会对其他盒子造成任何影响。

## 绝对定位

1. 宽高为auto，适应内容
2. 包含块变化：找祖先中第一个定位元素，**该元素的填充盒为其包含块**。若找不到，则它的包含块为**整个网页**（初始化包含块）
3. 脱离原来定位 相对于最近的父级有定位的元素进行定位，如果没有，那么由文档进行定位

## 固定定位

其他情况和绝对定位完全一样。

包含块不同：**固定为视口**（浏览器的可视窗口）

## 定位下的居中

某个方向居中：

1. 定宽（高）
2. 将左右（上下）距离设置为0
3. 将左右（上下）margin设置为auto

绝对定位和固定定位中，margin为auto时，会自动吸收剩余空间

## 多个定位元素重叠时

堆叠上下文

设置z-index，通常情况下，该值越大，越靠近用户

只有定位元素设置z-index有效

z-index可以是负数，如果是负数，则遇到常规流、浮动元素，则会被其覆盖

## 补充

- 绝对定位、固定定位元素一定是块盒
- 绝对定位、固定定位元素一定不是浮动
- 没有外边距合并




# 两个经典bug

## margin塌陷

父子标签，垂直方向的margin 粘合在一起取 取最大的margin定位

```html
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
**父级触发bfc拉解决此问题**

## margin合并

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
**可以通过把需要解决的元素放到bfc的元素中，来解决此问题，但是这样就会改变了html结构，所以不解决，可以通过数学方法设置合适的像素。**

# BFC

> 官方解释,块格式化上下文（Block Formatting Context，BFC）,它是一块独立的渲染区域，它规定了在该区域中，常规流块盒的布局

常规流块盒布局

1. 常规流块盒在水平方向上，必须撑满包含块

2. 常规流块盒在包含块的垂直方向上依次摆放

3. 常规流块盒若外边距无缝相邻，则进行外边距合并

4. 常规流块盒的自动高度和摆放位置，无视浮动元素

渲染区域

1. 根元素

2. 浮动和绝对定位元素

3. overflow不等于visible的块盒

独立的

1. 不同的BFC区域，它们进行渲染时互不干扰

2. 创建BFC的元素，隔绝了它内部和外部的联系，内部的渲染不会影响到外部

具体规则

创建BFC的元素，它的自动高度需要计算浮动元素(类似清除浮动的效果)

创建BFC的元素，它的边框盒不会与浮动元素重叠(会避开浮动盒子)

创建BFC的元素，不会和它的子元素进行外边距合并()



# iframe元素

框架页

通常用于在网页中嵌入另一个页面

iframe 可替换元素

1. 通常行盒
2. 通常显示的内容取决于元素的属性
3. CSS不能完全控制其中的样式
4. 具有行快盒的特点



# 在页面中使用flash

object

embed

它们都是可替换元素

MIME(Multipurpose Internet Mail Extensions)

多用途互联网邮件类型：

比如，资源是一个jpg图片，MIME：image/jpeg

```html
<!-- 兼容的写法 -->
<object data="./example.swf" type="application/x-shockwave-flash">
    <param name="quality" value="high">
    <embed quality="high" src="./example.swf" type="application/x-shockwave-flash">
</object>
```





# 表单元素

一系列元素，主要用于收集用户数据

## input元素

输入框

- type属性：输入框类型

type: text， 普通文本输入框
type：password，密码框
type: date, 日期选择框，兼容性问题
type: search, 搜索框，兼容性问题
type: number，数字输入框
type: checkbox，多选框
type: radio，单选框

- value属性：输入框的值
- placeholder属性：显示提示的文本，文本框没有内容时显示


input元素可以制作按钮

当type值为reset、button、submit时，input表示按钮。

## select元素

下拉列表选择框

通常和option元素配合使用

## textarea元素

文本域，多行文本框

## 按钮元素

button

type属性：reset、submit、button，默认值submit

## 表单状态

readonly属性：布尔属性，是否只读，不会改变表单显示样式

disabled属性：布尔属性，是否禁用，会改变表单显示样式


## 配合表单元素的其他元素

### label

普通元素，通常配合单选和多选框使用

- 显示关联

可以通过for属性，让label元素关联某一个表单元素，for属性书写表单元素id的值

```html
<input id='radMale' type='radio' />
<label for='radMale'>男</lable>  //这样在点击男的时候也会有radio的效果了
```

- 隐式关联

```html
<label>
   <input type='radio'/>
   男
</label>

```

### datalist

数据列表

该元素本身不会显示到页面，通常用于和普通文本框配合


```html
<p>
    请输入你常用的浏览器：
    <input list="userAgent" type="text">
</p>

<datalist id="userAgent">
    <option value="Chrome">谷歌浏览器</option>
    <option value="IE">IE浏览器</option>
    <option value="Opera">欧鹏浏览器</option>
    <option value="Safari">苹果浏览器</option>
    <option value="Fire fox">火狐浏览器</option>
</datalist>
```

### form元素

通常，会将整个表单元素，放置form元素的内部，作用是当提交表单时，会将form元素内部的表单内容以合适的方式提交到服务器。

form元素对开发静态页面没有什么意义。

### fieldset元素

表单分组

``` html
<h1>修改用户信息</h1>
<fieldset>
    <legend>账号信息</legend>
    <p>
        用户账号：
        <input type="text" value="aaaaa" readonly>
    </p>
    <p>
        用户密码：
        <input type="password">
    </p>
</fieldset>

<fieldset>
    <legend>基本信息</legend>
    <p>
        用户姓名：
        <input disabled value="袁进" type="text">
    </p>
    <p>
        城市：
        <select disabled name="" id="">
            <option value="">Lorem.</option>
            <option value="">Vel!</option>
            <option value="">Dolore?</option>
            <option value="">Autem?</option>
            <option value="">Nulla?</option>
            <option value="">Aliquam?</option>
            <option value="">Obcaecati!</option>
            <option value="">Nulla!</option>
            <option value="">Totam.</option>
            <option value="">Ipsum.</option>
        </select>
    </p>
</fieldset>
```

# 美化表单元素

## 新的伪类

1. focus

元素聚焦时的样式

```css
input:focus {
    outline: 1px solid #008c8c;
    outline-offset: 0;
    color: #000;
}   
```

2. checked

单选或多选框被选中的样式

```css
input:checked+label {
    color: red;
}
```

## 常见用法

1. 重置表单元素样式

2. 设置textarea是否允许调整尺寸

css属性resize：

- both：默认值，两个方向都可以调整尺寸
- none：不能调整尺寸
- horizontal: 水平方向可以调整尺寸
- vertical：垂直方向可以调整尺寸

3. 文本框边缘到内容的距离

4. 控制单选和多选的样式

```html
<style>
    .radio-item .radio {
        width: 12px;
        height: 12px;
        border: 1px solid #999;
        border-radius: 50%;
        cursor: pointer;
        display: inline-block;
    }

    .radio-item input:checked+.radio{
        border-color: #008c8c;
    }

    .radio-item input:checked~span{
        color:#008c8c;
    }

    .radio-item input:checked+.radio::after {
        content: "";
        display: block;
        width: 5px;
        height: 5px;
        background: #008c8c;
        margin-left: 3.5px;
        margin-top: 3.5px;
        border-radius: 50%;
    }

    .radio-item input[type="radio"]{
        display: none;
    }
</style>


<p>
    请选择性别：
<label class="radio-item">
    <input name="gender" type="radio">
    <span class="radio"></span>
    <span>男</span>
</label>

<label class="radio-item">
    <input name="gender" type="radio">
    <span class="radio"></span>
    <span>女</span>
</label>
</p>
```

# 表格元素

在css技术出现之前，网页通常使用表格布局。

后台管理系统中可能会使用表格。

前台：面向用户

后台：面向管理员。对界面要求不高，对功能性要求高。

表格不再适用于网页布局？表格的渲染速度过慢。

# 其他元素

1. abbr

缩写词

```html
<p>
    <abbr title="cascading style sheet">CSS</abbr> 是用于为页面添加样式
</p>
```

2. time

提供给浏览器或搜索引擎阅读的时间

```html
<p>
    <time datetime="2019-5-1">今年5月</time>  我录制了HTML 和 CSS的课程
</p>
```

3. b  （bold）

以前是一个无语义元素，主要用于加粗字体

4. q

一小段引用文本

5. blockquote

大段引用的文本

6. br

无语义
主要用于在文本中换行

7. hr

无语义
主要用于分割

8. meta

还可以用于搜索引擎优化（SEO）

9.  link

链接外部资源（CSS、图标）

rel属性：relation，链接的资源和当前网页的关系

type属性：链接的资源的MIME类型

设置网站的图片,如下设置或者放到网站根目录

```
<link rel='shortcut icon' type='image/x-icon' href='123.ico' />
```

# @规则

at-rule: @规则、@语句、CSS语句、CSS指令

1. import

@import "路径";

导入另外一个css文件

2. charset

@charset "utf-8";

告诉浏览器该CSS文件，使用的字符编码集是utf-8，必须写到第一行


# web字体和图标

## web字体

用户电脑上没有安装相应字体，强制让用户下载该字体，临时安装

使用@font-face指令制作一个新字体

```css
/* 制作一个新的字体，名称叫做good night */
@font-face {
    font-family: "good night";
    src: url("./font/晚安体.ttf");
}

p {
    font-family: "good night";
}

/* 字体文件过大，可能会影响性能 */

```

## 字体图标

利用了web字体特性，把字体设置成了各种图标

做的比较好的,阿里的iconfont.cn

这里生成的字体，只考虑我们用到的图标的字体，所以性能可以忽略。

1. 在线方式

```css
<link rel="stylesheet" href="//at.alicdn.com/t/font_1206816_qshsac4925m.css">
```

2. 离线方式

3. unicode

```css
<style>
    @font-face {
        font-family: 'iconfont';
        /* project id 1206816 */
        src: url('//at.alicdn.com/t/font_1206816_qshsac4925m.eot');
        src: url('//at.alicdn.com/t/font_1206816_qshsac4925m.eot?#iefix') format('embedded-opentype'),
            url('//at.alicdn.com/t/font_1206816_qshsac4925m.woff2') format('woff2'),
            url('//at.alicdn.com/t/font_1206816_qshsac4925m.woff') format('woff'),
            url('//at.alicdn.com/t/font_1206816_qshsac4925m.ttf') format('truetype'),
            url('//at.alicdn.com/t/font_1206816_qshsac4925m.svg#iconfont') format('svg');
    }

    .iconfont {
        font-family: "iconfont";
        font-style: normal;
    }
</style>

<p>
    <i class="iconfont">
        &#xe62e;
    </i>
</p>
```

# 布局

## 多栏布局

两栏布局

左栏浮动，主区域overflow:hiddne，间距通过左栏的margin-right

三栏布局

侧边栏左浮动，右浮动，主区域overflow:hidden,间距通过侧边栏的margin

## 等高

1. CSS3的弹性盒
2. JS控制
3. 伪等高

## 元素书写顺序

## 后台页面的布局

主区域固定定位，宽高100%。

# 行高的取值

line-height

1. px, 像素值

2. 无单位的数字(多行文本通常采用这个)

行高为字体大小的两倍 

先继承，再计算 

3. em单位

行高为字体大小的两倍 

先计算像素值，再继承 

4. 百分比

# body背景

**画布 canvas**

一块区域

特点：

1. 最小宽度为视口宽度
2. 最小高度为视口高度

**HTML元素的背景**

覆盖画布

**BODY元素的背景**

如果HTML元素有背景，BODY元素正常（背景覆盖边框盒）

如果HTML元素没有背景，BODY元素的背景覆盖画布

**关于画布背景图**

1. 背景图的宽度百分比，相对于视口
2. 背景图的高度百分比，相对于网页高度
3. 背景图的横向位置百分比、预设值，相对于视口
4. 背景图的纵向位置百分比、预设值，相对于网页高度


# 行盒的垂直对齐

## 多个行盒垂直方向上的对齐

给没有对齐元素设置vertical-align

预设值

数值

## 图片的底部白边

图片的父元素是一个块盒，块盒高度自动，图片底部和父元素底边之间往往会出现空白。

1. 设置父元素的字体大小为0
2. 将图片设置为块盒

# 堆叠上下文

堆叠上下文（stack context），它是一块区域，这块区域由某个元素创建，它规定了该区域中的内容在Z轴上排列的先后顺序。

## 创建堆叠上下文的元素

1. html元素（根元素）
2. 设置了z-index（非auto）数值的定位元素

## 同一个堆叠上下文中元素在Z轴上的排列

从后到前的排列顺序：

1. 创建堆叠上下文的元素的背景和边框

2. 堆叠级别(z-index, stack level)为负值的堆叠上下文
3. 常规流非定位的块盒
4. 非定位的浮动盒子
5. 常规流非定位行盒
6. 任何 z-index 是 auto 的定位子元素，以及 z-index 是 0 的堆叠上下文
7. 堆叠级别为正值的堆叠上下文

每个堆叠上下文，独立于其他堆叠上下文，它们之间不能相互穿插。


# svg

svg: scalable vector graphics，可缩放的矢量图

1. 该图片使用代码书写而成
2. 缩放不会失真
3. 内容轻量

## 怎么使用

svg可以嵌入浏览器，也可以单独成为一个文件

xml语言，svg使用该语言定义

## 书写svg代码

### 矩形:rect

### 圆形：circle

### 椭圆：ellipse

### 线条：line

### 折线：polyline

### 多边形：polygon

### 路径：path

M = moveto
L = lineto
H = horizontal lineto
V = vertical lineto
C = curveto
S = smooth curveto
Q = quadratic Belzier curve
T = smooth quadratic Belzier curveto
A = elliptical Arc
Z = closepath

A
半径1    
半径2     
顺时针旋转角度    
小弧（0）或大弧（1）   
顺时针（1）逆时针（0）

### 例子

画太极图

# 数据链接

data url

## 如何书写

数据链接：将目标文件的数据直接书写到路径位置

语法：data:MIME,数据

## 意义

优点：

1. 减少了浏览器中的请求

请求

响应

减少了请求中浪费的时间

2. 有利于动态生成数据

缺点：

1. 增加了资源的体积

导致了传输内容增加，从而增加了单个资源的传输时间

2. 不利于浏览器的缓存

浏览器通常会缓存图片文件、css文件、js文件。

3. 会增加原资源的体积到原来的4/3

应用场景：

1. 但请求单个图片体积较小，并且该图片因为各种原因，不适合制作雪碧图，可以使用数据链接。

2. 图片由其他代码动态生成，并且图片较小，可以使用数据链接。

## base64

一种编码方式

通常用于将一些二进制数据，用一个可书写的字符串表示。


# 浏览器兼容性

## 问题产生原因

- 市场竞争
- 标准版本的变化

## 厂商前缀

> 比如：box-sizing， 谷歌旧版本浏览器中使用-webkit-box-sizing:border-box

- 市场竞争，标准没有发布
- 标准仍在讨论中（草案），浏览器厂商希望先支持

IE： -ms-
Chrome，safari:  -webkit-
opera： -o-
firefox: -moz-

> 浏览器在处理样式或元素时，使用如下的方式：
> 当遇到无法识别的代码时，直接略过。


1. 谷歌浏览器的滚动条样式

实际上，在开发中使用自定义的滚动条，往往是使用div+css+JS实现的

2. 多个背景图中选一个作为背景

## css hack

根据不同的浏览器（主要针对IE），设置不同的样式和元素

1. 样式

IE中，CSS的特殊符号

- *属性，兼容IE5、IE6、IE7
- _属性，兼容IE5~IE6
- 属性值\9，兼容IE5~IE11
- 属性值\0，兼容IE8~IE11
- 属性值\9\0，兼容IE9~IE10

> IE5、6、7的外边距bug，浮动元素的左外边距翻倍

2. 条件判断

## 渐近增强 和 优雅降级

两种解决兼容性问题的思路，会影响代码的书写风格

- 渐近增强：先适应大部分浏览器，然后针对新版本浏览器加入新的样式

书写代码时，先尽量避免书写有兼容性问题的代码，完成之后，再逐步加入新标准中的代码。

- 优雅降级：先制作完整的功能，然后针对低版本浏览器进行特殊处理

书写代码时，先不用特别在意兼容性，完成整个功能之后，再针对低版本浏览器处理样式。

## caniuse

查找css兼容性

[caniuse.com](https://caniuse.com/)


# 居中总结

居中：盒子在其包含块中居中

## 行盒（行块盒）水平居中

直接设置行盒（行块盒）父元素text-align:center

## 常规流块盒水平居中

定宽，设置左右margin为auto

## 绝对定位元素的水平居中

定宽，设置左右的坐标为0（left:0, right:0），将左右margin设置为auto

> 实际上，固定定位（fixed）是绝对定位（absolute）的特殊情况

## 单行文本的垂直居中

设置文本所在元素的行高，为整个区域的高度

## 行块盒或块盒内多行文本的垂直居中

没有完美方案

设置盒子上下内边距相同，达到类似的效果。

## 绝对定位的垂直居中

定高，设置上下的坐标为0（top:0, bottom:0），将上下margin设置为auto


# 样式补充

## display:list-item

设置为该属性值的盒子，本质上仍然是一个块盒，但同时该盒子会附带另一个盒子

元素本身生成的盒子叫做主盒子，附带的盒子称为次盒子，次盒子和主盒子水平排列

涉及的css：

1. list-style-type

设置次盒子中内容的类型

2. list-style-position

设置次盒子相对于主盒子的位置

3. 速写属性list-style

**清空次盒子**

list-style:none

## 图片失效时的宽高问题

如果img元素的图片链接无效，img元素的特性和普通行盒一样，无法设置宽高

## 行盒中包含行块盒或可替换元素

行盒的高度与它内部的行块盒或可替换元素的0高度无关

## text-align:justify

text-align:

- left: 左对齐
- right：右对齐
- center：居中
- justify：除最后一行外(添加空的伪元素,设置为行块盒)，分散对齐

## 制作一个三角形

```
div{
    width: 0;
    height: 0;
    border: 10px solid transparent;
    border-left-color: red;
}
```

## direction 和 writing-mode

开始 start -> 结束 end
左 left -> 右 end

开始和结束是相对的，不同国家有不同的习惯

左右是绝对的

direction设置的是开始到结束的方向

writing-mode：设置文字书写方向

## utf-8字符

css中 "\59EC\6210";

网页中通过 &#x8881;&#x8FDB;



