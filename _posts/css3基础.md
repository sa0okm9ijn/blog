---
title: css3基础
date: 2019-11-09 13:02:27
tags: 
- Css 
categories: Css 
description: 

---

# css3兼容前缀

| prefix  | browser  |
|---|---|
| -webkit | chrome和safari  |
| -moz | firefox  |
| -ms | IE  |
| -0 | opera  |

# css3兼容性网站

css3参考手册:[](http://css.doyoe.com/)

css3权威参考手册:http://www.caniuse.com

# 前处理器 pre-processor

按照制定规则的语法,帮助生成css代码

## 插件 
1. sass/less 
2. next-css




# 后处理器 post-processor

写的就是css代码,写完之后会自动加前缀

基于caniuse加前缀,根据浏览器兼容性自动加前缀.

## 插件 
1. autoprefixer



# postCss

插件独立用不了,需要结合postCss使用,

用js实现的css抽象语法树

AST(Abstract Syntax Tree)

剩下的事留给后人来做(插件来做)

# css3选择器

## 关系选择器(Relationship Selectors)

1. 直接子元素选择器

```css
div > span{

}
```

2. 下一个满足条件的兄弟元素节点

```css
div + p{

}
```

3. 下面满足条件的的兄弟元素节点

```css
div ~ p{

}
```

## 属性选择器(Attribute Selectors)


```css
/* div上有class属性的 属性名有一个独立a的 */
div[class~="a"]{

}
/* div上有class属性的,以a开头或以a-开头的 */
div[class|="a"]{

}
/* 以a开头的 */
div[class^="a"]{

}
/* 以a结尾的 */
div[class$="a"]{

}

/* 存在字母a的 */
div[class*="a"]{

}

```

## 伪元素选择器(Pseudo-Element Selectors)

1. placeholder input上的属性placehodler样式

只能改文字颜色

```css
input::placehodler{

}
```

2. selection 选中文字时的样式

```css

/* 只能改这三个样式 */
div::selection{
    background-color:red;
    color:red;
    text-shadow:3px 5px black;
}


```

## 伪类选择器(Pseudo-Classes Selectors)


### 

被选中的元素一种状态

1. not

```css
/* 选中类选择器不是test的 */
div:not(.test){

}
```
2. root

根标签选择器,在htm种跟标签是html,root包含html.换了环境 指的可能就是xml等

```css
和html种html标签是一致的

:root{

}
```

3. target

被锚点标记

```css

div::target{

}

```

### 

都考虑其他元素对他们的影响

1. first-child

第一个子元素
```css
p:first-child{

}
```

2. last-child

最后一个子元素
```css
p:last-child{

}
```
3. only-child

独生子
```css
p:only-child{

}
```
4. nth-child(n) 

符合条件的子元素  n从0开始  css中从1开始  odd 奇数  even 偶数

```css
p:nth-child(2n+1){

}
```

5. nth-last-child(n)

倒着选

```css
p:nth-last-child(n){

}
```


### 

不考虑其他元素对他们的影响

1. first-of-type

第一个某类型子元素
```css
p:first-of-type{

}
```

2. last-of-type

最后一个某类型子元素

```css
p:last-of-type{
    
}
```
3. only-of-type
只有一个某类型的儿子

```css
p:only-of-type{
    
}
```

4. nth-of-type
   
第几个子元素

```css
p:nth-of-type(n+3){
    
}
```

1. nth-of-last-type

倒着第几个子元素

```css
p:nth-of-last-type(n+3){
    
}
```





### 

1. empty

空节点

```css
div:empty{

}
```

2. checked

```css
input:checked + span{

}
```

3. enabled

可用
   
```css
input:enabled{

}
```
1. disabled

禁用的

```css
input:disabled{

}
```

5. read-only

只读的
   
```css
input:read-only{

}
```
6. read-write

可写的
```css
input:read-write{

}
```



## 练习题

手风琴
选项卡


# 边框

## border-radius

圆角

```css
/* 分解写法 */
div{
    border-top-left-radius:10px;
    border-top-right-radius:10px;
    border-bottom-left-radius:10px;
    border-bottom-right-radius:10px;
}
```

进一步分解

```css
/* 水平和垂直方向 */
div{
    
    border-top-left-radius:10px 10px;
}
/* 水平/垂直 */
div{
    border-radius:10px 20px 30px 40px / 10px 20px 30px 40px; 
}
```

## box-shadow

阴影

```css
div{
    /* 水平 垂直  blur模糊(基于边框位置,向两边同时展开模糊) spread增大 颜色 */
    box-shadow:10px 10px  10px 10px  #f30;
    /* 内阴影 */
    box-shadow:inset 10px 10px 10px 10px  #f30;

}

/* 设置四周阴影颜色 */
div{
    box-shadow:0px 0px 3px 0px #f30,
    0px 0px 3px 0px #f30,
    0px 0px 3px 0px #f30,
    0px 0px 3px 0px #f30,
}
```

练习

1. 多值设置

谁先设置谁在上面
文字在阴影的上面,阴影在背景的上面
```css

div{
    box-shadow:inset inset 0px 0px 50px #fff,
                     inset 10px 0px 80px #f0f,
                     inset -10px 0px 80px #0ff,
                     inset 10px 0px 300px #f0f,
                     inset -10px 0px 300px #0ff,
                     0px 0px 50px #fff,
                     -10px 0px 80px #f0f,
                     10px 0px 80px #0ff; 
}

```


## border-image

border-image-source|[border-image-slice,border-image-width,border-image-outset]|border-image-repeat

1. 渐变色
```css
div{
    border-color:lightpink;
    border-image-source:linear-gradient(red,yellow);
    border-image-slice:10;
}
```

2. 图片

```css
div{
    border-image-source:url(source/border.png);
    
    border-image-slice:10;
}
```

3. bordr-image-slice 

分割线 top right bottom left

1到4个值

默认值100%

只可以填百分数和数字 不可以填像素

fill填充内容区

4. border-image-outset

背景图片延申的

4. border-image-width

默认值1

设置border图片背景的宽度

auto  拿的是slice的值 补上px

5. border-image-repeat

stretch、round、repeat、space

可以填写2个值,一个代表水平,一个代表垂直

6. 联合写法

```css
div{
    border-image:source slice repeat
}
```



# 背景

1. 渐变色

linear-gradient

参数:方向,色值1,色值2 

```css
div{
    /* 单一方向 */
  background-image:linear-gradient(to right,#0f0,#ff0);
  /* 组合方向 */
  background-image:linear-gradient(to top right,#0f0,#ff0);
  /* 度数 */
  background-image:linear-gradient(0deg,#0f0,#ff0);

  /* 颜色终止位置 */
  background-image:linear-gradient(0deg,#0f0 20px,#ff0 60px);  

}

```

radial-gradient

参数: 放射形状 放射截至 at 圆心坐标,颜色1,颜色2

```css
div{
    background-image:radial-gradient(ellipse farthest-corner at 50px 50px,#0f0,#fff0)
}
```




```css
div{
    /* 线性渐变 */
    background-image:linear-gradient(#0f0,#f00);
    /* 放射性渐变 */
    background-image:radial-gradient(#0f0,#f00);
}
```

2. 多个背景图片

容错   第一个图显示不了 显示第二个图

```css
div{
    background-image:url(),url(),url();
    background-size:100px 200px,100px 200px;
    background-repeat:no-repeat;
    background-position:0 0,100px 0;
}
```

3. background-origin


border-box、padding-box、padding-box

默认值padding-box

背景图渲染开始位置

background-position根据origin定位

```css
div{
    background-origin:border-box;
}
```

4. background-clip


从那截至显示图片

padding-box、pading-box、content-box、text

默认border-box 

```css
div{
    background-clip:
}
```

文字部分截取图片
```css
div{
    -webkit-backgrond-clip:text;
    background-clip:text;
    -webkit-text-fill-color:transparent;
    text-fill-color:transparent;
}
```

5. background-repeat

no-repeat、repeat-x、repeat-y、round、space

6. background-attachment

scroll:相对于容器定位
local:相对于内容区定位
fixed:相对于视口定位,但是还是在容器内，视口看不见容器了图片也就显示不到了

```css
div{

    background-attachment:fixed;

}
```

5. background-size


cover:一张图片填充背景,一张图片完完整整填充容器,不改变比例,有可能会超出
contain:不改变图片的比例下,填充一张完整的图片

```css
div{

}
```

# 颜色

## RGB

## RGBA

## HSL

## HSLA

## curent

不设置border-color的话,会取color的值

css3会取currentColor的值,currentColor就是color的值

```css
div{

}
```



# text

## text-shadow

参数:x y blur color

可以加多个

```css
div{
    text-shadow:3px 3px 3px #000;
}
```

1. 浮雕效果

```css
div{
    text-shadow:1px 1px #000,-1px -1px #fff;
}
```

2. 镂刻

```css
div{
    text-shadow:-1px -1px #000;
}
```

3. access火焰效果
```css
div{
    text-shadow:0px 0px 10px #0f0,0px 0px 20px #0f0;
}
div:hover{
    text-shadow:0px 0px 10px #f00,0px 0px 20px #f10;
}
div::before{
    content:"No";
}
```

4. 死神来了

backgroun-clip 文字就变成了背景的一部分,阴影会在文字背景的上面

```css
div{

}
```

5. 描边

```css
div{
    font-family:simsun;
    -webkit-text-stoke:2px red;
}
```

## font-face

```css
@font-face{
    font-family:"abc";
    src:url();
}
div{
    font-family:"abc";
}
```

## white-space

文本显示方式

## word-break

换行控制


# columns

```css
div{
    columns:3;
    /* //孔隙 */
    column-gap:10px;
    /* 和border一样 */
    column-rule:border solid 1px;
    /* 合并列 */
    column-span:all;

    -webkit-column-break-before:always;

    column-width:300px;
}
```

作业

小说阅读



# 盒模型

## ie6混杂盒模型

```css
div{
    box-sizing:border-box;
}
```
resize,自己拖动元素大小

结合overflow使用

## 弹性盒模型

2009年，W3C 提出了一种新的方案----Flex 布局，可以简便、完整、响应式地实现各种页面布局。目前，它已经得到了所有浏览器的支持，这意味着，现在就能很安全地使用这项功能。

Flex 是 Flexible Box 的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性。

任何一个容器都可以指定为 Flex 布局。


### 基本概念

采用 Flex 布局的元素，称为 Flex 容器（flex container），简称"容器"。它的所有子元素自动成为容器成员，称为 Flex 项目（flex item），简称"项目"。

![](bg2015071004.png)

容器默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴（cross axis）。主轴的开始位置（与边框的交叉点）叫做``main start``，结束位置叫做``main end``；交叉轴的开始位置叫做``cross start``，结束位置叫做``cross end``。

项目默认沿主轴排列。单个项目占据的主轴空间叫做``main size``，占据的交叉轴空间叫做``cross size``。


### 容器属性

1. flex-direction:属性决定主轴的方向（即项目的排列方向）。
   1. row（默认值）：主轴为水平方向，起点在左端。
   2. row-reverse：主轴为水平方向，起点在右端
   3. column：主轴为垂直方向，起点在上沿。
   4. column-reverse：主轴为垂直方向，起点在下沿。
2. flex-wrap:默认情况下，项目都排在一条线（又称"轴线"）上。flex-wrap属性定义，如果一条轴线排不下，如何换行
   1. nowrap（默认）：不换行。
   2. wrap：换行，第一行在上方
   3. wrap-reverse：换行，第一行在下方。
3. flex-flow:是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap。 
4. justify-content:属性定义了项目在主轴上的对齐方式。
   1. flex-start（默认值）：左对齐
   2. flex-end：右对齐
   3. center： 居中
   4. space-between：两端对齐，项目之间的间隔都相等。
   5. space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。
5. align-items:属性定义项目在交叉轴上如何对齐。
   1. flex-start：交叉轴的起点对齐。
   2. flex-end：交叉轴的终点对齐。
   3. center：交叉轴的中点对齐。
   4. baseline: 项目的第一行文字的基线对齐。
   5. stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。
6. align-content:属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用
   1. flex-start：与交叉轴的起点对齐。
   2. flex-end：与交叉轴的终点对齐。
   3. center：与交叉轴的中点对齐。
   4. space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。
   5. space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
   6. stretch（默认值）：轴线占满整个交叉轴。


### 项目属性

1. order:一个``int``值,定义项目的排列顺序。数值越小，排列越靠前，默认为0。
2. flex-grow:定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大,所有项目的flex-grow属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的flex-grow属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。
3. flex-shrink:定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小。如果一个项目的flex-shrink属性为0，其他项目都为1，则空间不足时，前者不缩小。负值对该属性无效。
4. flex-basis:属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。它可以设为跟width或height属性一样的值（比如350px），则项目将占据固定空间。
5. flex:属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选
6. align-self:属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。该属性可能取6个值，除了auto，其他都与align-items属性完全一致。

# 动画

## trasition

过度 

参数:trasition-property,trasition-duration,trasition-timing-function,trasition-delay

```css
div{
    transition:all 2s linear 1s,height 1s;
    transition:all 2s cubic-bezier(0,0,1,1);
}
```

## animation

动画 

```css
@keyframes run{
    0%{left:0;top:0}
    25%{left:100px;top:0}
    50%{}
    75%{}
    100%{}
}

@keyframes run{
    from{left:0;top:0}
    25%{left:100px;top:0}
    50%{}
    75%{}
    to{}
}
div{

    animation:run 4s cubic-bezier(0,0,1,1) 1s infinite reverse;
    /* 把动画的最后一帧当作结束状态 */
    animation-fill-mode:forwards;
    /* steps少了过度 跳转来实现  每一个动画需要几步 
    start 保留下一帧状态,直到这段动画时间结束
    end   保留当前帧状态,直到这段动画时间结束*/
    animation:run 4s steps(1,end);
}
```

## trasform

### rotate

轴会跟着旋转的

1. rotate()


```css
div{
    /* 旋转度数 */
    transform:rotate(60deg);
    /* 旋转中心 */
    transform-origin:0 0;
}

```

2. rotateX()

```css
div{
    /* 旋转度数 */
    transform:rotateX(60deg);
    /* 旋转中心 */
    transform-origin:0 0;
}

```
2. rotateY()

```css

div{
    /* 旋转度数 */
    transform:rotateY(60deg);
    /* 旋转中心 */
    transform-origin:0 0;
}


```
3. rotateZ()


```css

div{
    /* 旋转度数 */
    transform:rotateZ(60deg);
    /* 旋转中心 */
    transform-origin:0 0;
}


```
4. rotate3d()


```css
div{
    /* xyz用来确定轴的 */
    transform:rotate3d(x,y,z,angle);
}
```

### scale
1. scale()

伸缩的是此元素的变化坐标轴的刻度
```css
div{
    transform:scale(1.5,1.5);

}
```
2. skew()

倾斜坐标轴并且拉申了 

```css
div{
    transform:skew(0deg,0deg);
}
```

### translate
参考自身 移动

1. translateX()
2. translateY()
3. translateZ()

### trasformstyle


指定元素的空间为3d堆叠空间,子级的渲染就成了立体渲染

```css
div{
    trasformstyle:preserve-3d;
}
```


### trasform-origin

空间轴中心


# perspective

景深

一般用在全局,也可以通过transform填在元素本身上（不可以设置中心）

1. 问题
2. 问题


# 响应式网页

响应式网页设计可使网站在不同的设备上浏览时不同分辨率皆有适合的呈现,减少用户进行缩放、平移和滚动的行为

1. 通过meta标签设置

```html
<meta name="viewport" content="width=device-width", initial-scale=1.0>
```

这句话的意思是告诉浏览器:将页面大小 根据不同的分辨率进行响应的调节 以展示给用户的大小感觉差不多

浏览器默认的视口宽度980px  设置了width=device-width之后,视口宽度就变为了device-width了

width-device-width和initial-scale其实是一样的,只是为了解决兼容性问题

width = device-width iphone或ipad上横竖屏的宽度 = 竖屏时候的宽度       不能自适应的问题

initial-scale=1.0  window phone ie浏览器 横竖屏的宽度 = 竖屏时候的宽度 不能自适应的问题

## 响应式网页开发方法

1. 流体网络

可伸缩的网格

2. 弹性图片

图片宽高不固定(可设置min-width:100%)

3. 媒体查询

让网页在不同的终端上面展示效果相同

是向不同的设备提供不同的样式一种方式.它为每种类型的用户提供了最佳的体验


媒体查询不占用权重,一般都放在最后

三种引入方式

如设置:设备宽度小于375 index.css起作用

1) 外部引入

```html

<link rel="stylesheep" media="(max-width:375px)" href="index.css">

```

2) @import

```html
<style>
@import 'index.css' (max-width:375px)
</style>
```

3) css样式引入

```css
@media(max-width:375px){
    body{

    }
}
```

4. 主要断点

设备宽度的临界点

## 单位值

1. rem

css3新增的一个单位,相对的只是html的根元素的font-size大小

```css

```

2. em

相对于本身的font-size大小,font-size是可以继承的

3. vw,vh

相对于视口而言的, 会把视口分成100份


4. vmax,vmin

取视口宽高中最小的一边分成100份




