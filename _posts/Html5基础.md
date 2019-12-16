---
title: Html5基础
date: 2019-11-23 07:16:51
tags: 
- Html5 
categories: HTML 
---


# 新增属性

## type



## contenteditable

没有兼容性问题

最好不要嵌套使用

## draggable

设置可拖拽属性,chorme,safari可以正常使用,firefox下不可以使用

a、img标签默认可拖拽

所有的标签元素,当拖拽结束,默认事件回到原处


拖拽的声明周期:拖拽的开始、拖拽进行中、拖拽结束

拖拽的组成:被拖拽的物体、目标区域

1. 被拖拽的物体

```javascript

var oDragDiv=document.querySelector(".div");

var beginX=0;
var beginY=0;
oDragDiv.ondragstart=function(e){
    beginX=e.clientX;
    beginY=e.clientY;
}

oDragDiv.ondragend=function(e){
    var x = e.clientX-beginX;
    var y = e.clientY-beginY;
    oDragDiv.style.left=oDragDiv.offsetLeft+x+"px";
    oDragDiv.style.top=oDragDiv.offsetTop+y+"px";
}

```

2. 目标区域

```javascript

var oDragDiv=document.querySelector(".div");

oDragDiv.ondragstart=function(e){

}

oDragDiv.ondrag=function(e){

}

oDragDiv.ondragend=function(e){

}

var oDragTarget=document.querySelector("target");
//不是元素图形进入触发,而是拖拽的鼠标进入触发
oDragTarget.ondragenter=function(e){

}
//进入不停的触发
oDragTarget.ondragover=function(e){

}
//离开区域触发
oDragTarget.ondragleave=function(e){

}
//执行ondrop需要 阻止ondragover的默认事件 e.preventDefault()
oDragTarget.onDrop=function(e){

}

```

拖拽指针的设置(兼容性不好)

e.dataTransfer;

# 新增标签

## 语义化标签

全是div只是有不同的含义

```html
<header></header>
<footer></footer>
```  

```html
<nav></nav>
```

```html
<section></section>
<article></article>
```

```html 
<!-- 不常用 -->
<aside></aside>
```




## canvas


### 画线

closepath针对的是一条线的闭合


```html
<canvas id="can" width="500px" height="300px"></canvas>
```

```javascript
var canvas= document.getElementById("can");
var ctx=canvas.getContext("2d");
ctx.moveTo(100,100); //一个画笔的起始
ctx.lineTo(200,100);
ctx.stroke();//画线

```

### 画矩形

```javascript
var canvas= document.getElementById("can");
var ctx=canvas.getContext("2d");

// ctx.rect(100,200,200,100);
// ctx.fill()
// ctx.stroke()

//ctx.strokeRect(100,200,200,100);
//ctx.fillRect(100,200,200,100);
```

矩形移动

```javascript

var canvas= document.getElementById("can");
var ctx=canvas.getContext("2d");

var height=100;
var timer=setInterval(function(){
    ctx.clearRect(0,0,500,300);
    ctx.fillRect(100,height,200,100);
    height+=2;
},1000/60)


```




### 画圆

```javascript
var canvas= document.getElementById("can");
var ctx=canvas.getContext("2d");

// 圆心坐标,半径,其实弧度,结束弧度,顺时针(0)还是逆时针(1)
ctx.arc(100,100,50,0,Math.PI/2,0);
ctx.stroke();
```

### 画圆角矩形

```javascript


var canvas= document.getElementById("can");
var ctx=canvas.getContext("2d");

// 110 让出最后一条线画的弧度
ctx.moveTo(100,110)
// B(x,y),C(x,y) 圆角大小 c只提供方向xy没意义
ctx.arcTo(100,200,200,200,10);
ctx.arcTo(200,200,200,100,10);
ctx.arcTo(200,100,100,100,10);
ctx.arcTo(100,100,100,200,10);
ctx.stroke();

```

### 贝塞尔曲线

```javascript
var canvas= document.getElementById("can");
var ctx=canvas.getContext("2d");
ctx.beginPath()

ctx.moveTo(100,100);

// 二次贝塞尔曲线
// ctx.quadraticCuveTo(200,200,300,100);

// 三次贝塞尔曲线
// ctx.bezierCurveTo(200，200，300，100，400，200);




ctx.stroke();

```

### 平移旋转缩放

平移和旋转是全局的


```javascript
var canvas= document.getElementById("can");
var ctx=canvas.getContext("2d");
// ctx.beginPath();
// ctx.rotate(Math.PI/6); //旋转 根据画布坐标轴的原点旋转
// ctx.translate(100,100) //平移坐标轴,改变原点
// ctx.moveTo(0,0);
// ctx.lineTo(100,100);
// ctx.stroke();



ctx.beginPath();
ctx.scale(2,2);  // 缩放,每个点都乘以这个系数
ctx.strokeRect(100,100,100,100);

```



### save和restore

```javascript
var canvas= document.getElementById("can");
var ctx=canvas.getContext("2d");

ctx.save()  //保存坐标轴的平移、缩放、旋转

ctx.beginPath();
ctx.tranlate(100,100);
ctx.rotate(Math.PI/4);
ctx.strokeRect(0,0,100,50);

ctx.beginPath();
ctx.restore();//还原基础状态
ctx.translate(100,100);
ctx.fillRect(200,0,100,50);

```


### 背景填充

```javascript

var canvas= document.getElementById("can");
var ctx=canvas.getContext("2d");




var img= new Image();

img.src="";

img.onload=function(){
    ctx.beginPath();
    ctx.translate(100,100);
    var bg = ctx.createPattern(img,"no-repeat");//以坐标原点开始填充的 所以有时候需要改变坐标系
    // ctx.fillStyle="blue";//填充的颜色
    ctx.fillStyle=bg; //填充背景图片
    ctx.fillRect(100,100,200,100);
    
}

```




### 线性渐变

```javascript

var canvas= document.getElementById("can");
var ctx=canvas.getContext("2d");

ctx.beginPath();

var bg = ctx.createLineGradient(0,0,200,0);//x1,y1,x2,y2  线性渐变起点为坐标系的原点,需要translate
//从0-1
bg.addColorStop(0,"white");
bg.addColorStop(1,"black");
ctx.fillStyle=bg;
ctx.translate(100,100);
ctx.fillRect(0,0,200,100);

```

### 辐射渐变

关于相离和相切的图案

```javascript

var canvas= document.getElementById("can");
var ctx=canvas.getContext("2d");

ctx.beginPath();

var bg = ctx.createRadiaGradient(0,0,0,0,0,100);//x1,y1,r1,x2,y2,r2;
bg.addColorStop(0,"white");
bg.addColorStop(1,"black");
ctx.fillStyle=bg;
ctx.fillRect(0,0,200,200);

```




### 阴影

```javascript

var canvas= document.getElementById("can");
var ctx=canvas.getContext("2d");

ctx.beginPath();

ctx.shadowColor="blue"; 
ctx.shadowBlue=10;
ctx.shadowOffsetX=15;//阴影默认骑在线上
ctx.shadowOffsetY=15;
ctx.strokeRect(0,0,200,200);

```

### 渲染文字

```javascript

var canvas= document.getElementById("can");
var ctx=canvas.getContext("2d");

ctx.beginPath();


ctx.fillStyle="red";
ctx.font="30px Georgia";

ctx.strokeText('panda',200,100);    //文字描边 //空心字


ctx.fillText("monkey",200,300);  //输出普通文字  实心字

```

### 线端样式

```javascript

var canvas= document.getElementById("can");
var ctx=canvas.getContext("2d");

ctx.beginPath();


ctx.lineWidth=15;
ctx.moveTo(100,100);
ctx.lineTo(200,100);
// ctx.lineCap="round"； //两边添加一块区域 square、round、butt

ctx.lineTo(100,150);

ctx.lineJoin="round"; //线相交处的处理 round、bevel、miter
ctx.miterLimit=5;  //相交出现的尖处理
ctx.stroke();

```




## svg

svg:矢量图,放大不会失真,适合大面积的贴图,通常动画较少或者较简单 标签和css去画
canvas:适合用于小面记得绘图,适合动画


### 画线和矩形


svg中所有闭合的图形,都是默认充满并且画出来,所以不需要stroke
```css
line{
    stroke:black;
    stroke-width:3px;
}
```

```html
<!-- rx ry圆角 -->
<svg width="500px" height="300px" style="border:solid 1px solid">
    <line x1="100" y1="100" x2="200" y2="100"></line>
    <rect height="50" width="100" x="0" y="0" rx="10" ry="10"></rect> 
</svg>
```


### 圆、椭圆、折线


折线:收尾不会相连
```css
polyline{
    fill:transparent;
    stroke:blueviolet;
    stroke-width:3px;
}
```

```html
<svg width="500px" height="300px" style="border:solid 1px solid">
    <circle r="50" cx="50" cy="200"></circle>
    <ellipse rx="100" ry="30" cx="400" cy="200"></ellipse>
    <polyline points="0 0,50 50,50 100,100 100, 100 50"></polyline>
</svg>
```


### 多边形和文本

polygon 会自动收尾相连
```html
<svg width="500px" height="300px" style="border:solid 1px solid">
   <polygon points="0 0,50 50,50 100,100 100, 100 50"></polygon>
   <text x="300" y ="50">halou</text>
</svg>
```

### 透明度与先线条样式

```css

polyline{
    stroke-opacity:0.5;
    fill-opacity:0.3;
    stroke-linegap:round;
    stroke-lineJoin：round;
}
```

### path标签

```css
path{
    fill:transparent;
    stroke:red;
}
```

```html

大写绝对位置,小写字母表示相对位置(M-L)

<svg width="500px" height="300px" style="border:solid 1px solid">
    <path d="M 100 100 L 200 100"></path>
    <path d= "M 100 100 H 200 V 100 Z"></path>
</svg>

```

### path 画弧


取大弧还是小弧的参数比较

```html

大写绝对位置,小写字母表示相对位置(M-L)

<svg width="500px" height="300px" style="border:solid 1px solid">
    <path d="M 100 100 A 100 50 0 1 1 150 200"></path>
</svg>

```

### 线性渐变

```html

<svg width="500px" height="300px" style="border:solid 1px solid">
    <defs>
      <lineGradient id= "bg1" x1="0" y1="0" x="0" y2="100%">
         <stop offset=0% style="stop-color:rgb(255,255,0)"></stop>
         <stop offset=0% style="stop-color:rgb(255,0,0)"></stop>
      </lineGradient>
    </defs>

    <rect x= "100" y ="100" width="200" height="100" style="fill:url(#bg1)"></rect>
</svg>

```

### 高斯模糊


```html

<svg width="500px" height="300px" style="border:solid 1px solid">
    <filter id="Gaussian">
        <feGaussianBlue in="SourceGraphic" stdDeviation="20"></feGaussianBlue>
    </filter>
     <rect x= "100" y ="100" width="200" height="100" style="fill:url(#bg1);filter:url(#Gaussian)" ></rect>
</svg>

```


### 虚线及简单动画

 dashoffset 简单的小动画

```css
/* 参数一次排  之间的间隙 交替循环设置参数*/
line{
    stroke-dasharray:10px 20px; 
    stroke-dashoffset:10px;
}
```

```html

<svg width="500px" height="300px" style="border:solid 1px solid">

    <line x1="100" y1="100" x2="200" y2="100"></line>


</svg>

```

### viewBox

比例尺

```html

<svg width="500px" height="300px" viewBox="0,0,250,150" style="border:solid 1px solid">

    <line x1="100" y1="100" x2="200" y2="100"></line>

</svg>

```

## audio与video

