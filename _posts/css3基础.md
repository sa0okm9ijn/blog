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

1. 父级

```css
div{
    display:flex/inline-flex;
    /* 设置主轴 垂直方向 */
    flex-direction:column;
    /* 不伸缩换行 */
    flex-wrap:wrap;
     /* 作用单行 基础主轴对齐 */
    justify-content:flex-start;
    /* 作用单行 基于交叉轴对齐 */
    align-items:flex-start;
    /* 作用多行 基于交叉轴居中 */
    align-content:center;

}
```

2. 子级

```css
div{

    /* 越小的在前面 默认值0  所以一般用负数来排 */
    order:-2;
    /* 基于交叉轴的分配状况 优先级高于父级align-items 小于align-content */
    align-self:flex-start;
    /* 基于主轴 按照设置比例分配剩余空间  伸 */
    flex-grow:1;
    /* 覆盖子项width   
    在你不设置width的时候,flex-basis等于元素的最小宽度 
    同时设置的话  flex-basis是元素的最小宽度  widht是元素的最大宽度
     */
    flex-basis:150px;
    /* 按照设置的比例 缩 */
    /* 压缩计算公式 加权值 = (真实内容区高度  * shrink + ***)   压缩值: (真实内容区高度/加权值 * 超出部分)    
    无论什么情况下 被不换行的内容撑开的容器,不会被压缩计算*/
    flex-shrink:1;

}
```


3. 应用

居中

```css
div{
    display:flex;
    justify-content:center;
    align-items:center;
}
```


导航栏

```css
div{
    display:flex; 
}
.item{
    flex:1 1 auto;

}
```


等分布局

```css
div{

}
```

圣杯布局

```css
div{
    
}
```


流式布局

```css
div{

}
```

作业  

神马人员介绍




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




