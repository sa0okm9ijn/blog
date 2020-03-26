---
title: Javascript专题系列
date: 2019-09-19 16:05:08
tags: 
- JavaScript 
categories: JavaScript 
description: 主要写一些特定对象的更全面的用法和讲解,主要包含了渡一课堂的一大点
---

# Console

## console.log

### 占位符

我们平常更多的使用是console.log(string)来输出一个调试信息，不止那些，这还有一种格式：console.log(msg,value)

console.log('%s love %s', 'I', 'you')

会准确的输出你所预期的东西。

I love you

会准确的输出你所预期的东西。

这里的"%s"是占位符,对字符串进行占位,还有

%o 对对象进行占位(object)
%d 对数字类型进行占位(number)

![](2019-09-19_160915.png)

还有一个比较有意思的占位符"%c",被称为css占位符,意味着利用console.log的输出内容是可以带样式的！

```javascript
console.log("i am a %cbutton",'color:white;background-color:orange;padding:2px 5px;border-radius:2px')
```
![](2019-09-19_174221.png)

中间部分显示样式

```javascript
console.log("i am a %cbutton%c not div",'color:white;background-color:orange;padding:2px 5px;border-radius:2px','color:aoto')
```

![](2019-09-19_174325.png)


**此处占位符号有几个,后面需要对应几个来补齐**



## console.dir

console.log清晰的展示了Dom节点信息

console.dir更加对象化的方式去观察元素节点


![](2019-09-19_174946.png)

## console.warn

console.warn 输出会有一抹黄色，高亮你的输出 Vue中部分源码也是用的console.warn

![](2019-09-19_175345.png)

## console.table

console.table方法更偏向于以一种列表展示形式的数据,如

![](2019-09-19_180139.png)

**console.table只有处理最多1000行数据的能力**

## console.assert

console.assert()第一个参数为false时，输出第二个参数，为true时，什么也不做

举个例子，我们看到了关于用户WAL0412的数据问题并且想要展示来自它们的事务，这将会是一个非常简便的方案，

console.aasert(tx.buyer!=='WAL0412',txt)

## console.count()

作为计数器使用

![](2019-09-19_182346.png)


console.count(),不传递参数，使用default调用

**console.countReset()重置计数器**

## console.trance

再简单的数据演示中可能不太适合，但是在你视图找出有问题内部类或者库这一块擅长

demo待补充

## console.time

是专门用于监测操作的时间开销的函数，也是监测JavaScript 细微时间的更好的方式。

```javascript

console.time();
for (i = 0; i < 100000; i++) {
}
console.timeEnd();

```

## console.group

```javascript
var number = 1;
console.group('OutsideLoop');
console.log(number);
console.group('Loop');
for (var i = 0; i < 5; i++) {
    number = i + number;
    console.log(number);
}
console.groupEnd();
console.log(number);
console.groupEnd()
console.log('All done now');

```
![](2019-09-19_200403.png)


# 基线布局

字体基线待完善....


# try-catch能否监听多线程中的错误

## 使用try-catch的建议

try catch的使用，永远应该放在你的控制范围之内，而不应该防范未知的错误。也就是说你很清楚知道这里是有可能”出错“的，

而且你很清楚知道什么前提下会出错，你就是要故意利用报错信息来区分错误，后续的程序会解决所有的出错，让程序继续执行。

如果让用户先发现你根本没预料到的错误，而不是你先发现错误，你是失职的。

## try-catch与多线程

浏览器中的JavaScript确实是以单线程的方式执行的，也就是说JavaScript执行使用一个主线程，但是JavaScript提供了异步操作，

比如定时器(setTimeout、setInterval)事件、Ajax请求、Promise, I/O等。它们将会被放入浏览器的事件任务队列（event loop）中去，

等到JavaScript运行时执行线程空闲时候，事件队列才会按照先进先出的原则被一一执行。

但是对于以上的异步操作过程中，能进行的计时，发送请求，I/O操作都是其他的线程在做的事情，所以说是这里的多线程指的是浏览器(宿主环境做的事情)

即浏览器搞了几个其他线程去辅助JS线程的运行。

1. setTimeout函数

```javascript
try {
    setTimeout(() => {
        console.log(a.b)
    }, 1000);
} catch (error) {
    console.log(error)
}
```

2. Promise函数

```javascript
try {
    var p = new Promise((resolve, reject) => {
        a.b
    })
} catch (error) {
    console.log('error')
}
```

3. Ajax函数

```javascript

function ajax(url) {
    var xhr = window.XMLHttpRequest ? new XMLHttpRequest() : ActiveXObject('microsoft.XMLHttp');
    xhr.open('get', url, true);
    xhr.send()
    xhr.onreadysattechange = () => {
        if (xhr.readystate == 4) {
            if (xhr.status == 200) {
                var data = xhr.responseTEXT;
                return data;
            }
        }
    }
}
try {

    ajax('someurl')
} catch (error) {
    console.log('error')
}

```

## 总结

对于以上几种异步操作，我们看的出来try-catch并未帮我们监听的到里面的错误。

原因是：javaScript引擎对异步方法进行try/catch操作只能捕获当次事件循环内的异常，对call back执行时抛出的异常将无能为力。

但是对于异步操作，只要是代码逻辑没有问题，我们在适当的问题出口把问题暴露出去就可以了，比如Promise的then，Ajax的状态判断等等。



# 深度克隆的算法有哪些

## 深度克隆和浅度克隆

浅层克隆也被称为浅克隆，浅克隆之所以被称为浅克隆，是因为对象只会被克隆最外部的一层,至于更深层的对象,则依然是通过引用指向同一块堆内存.

我们看下面浅层克隆的实现

```javascript
function shallowClone(o) {
    const obj = {};
    for (var i in o) {
        obj[i] = o[i];
    }
    return obj;
}
var oldobj = {
    name: 'pwd',
    list: ['e', 'f', 'g'],
    obj: { h: { i: 2 } }
};
var newObj = shallowClone(oldobj);
console.log(newObj.obj.h === oldobj.obj.h)

=>
true
```

我们可以看到,很明显,虽然oldObj.obj.h被克隆了,但是它还与oldObj.obj.h

相等,这表明他们依然指向同一段堆内存,这就造成了如果对newObj.obj.h

进行修改,也会影响oldObj.obj.h,这就不是一版好的克隆.

javascript提供的浅克隆方法:

**Object.assign**

```javascript
var oldobj = {
    name: 'pwd',
    list: ['e', 'f', 'g'],
    obj: { h: { i: 2 } }
};
var newObj = {};
Object.assign(newObj, oldobj);
console.log(newObj.obj.h === oldobj.obj.h)
=>
true
```

在上面很明显我们想要的克隆，浅层克隆是远远不够的，我们的目标致力于：两个长的一模一样的对象，但是彼此之间没有关联。那么接下来开始我们的重

头戏—---深层克隆

## 常见深层克隆

```javascript

function deepClone(origin, target) {
    var target = target || {},
        toStr = Object.prototype.toString,
        arrStr = "[object Array]";
    for (var prop in origin) {
        //过滤原型属性
        if (origin.hasOwnProperty(prop)) {
            if (origin[prop] !== "null" && typeof (origin[prop]) === 'object') {
                target[prop] = toStr.call(origin[prop]) === arrStr ? [] : {};
                deepClone(origin[prop], target[prop])
            } else {
                target[prop] = origin[prop]
            }
        }
    }
    return target;
}
var obj = {
    name: 'panda',
    sex: 18,
    msg: {
        a: 1,
        b: 2
    },
    list: [1, 2, 3, 4]
}
var obj1 = deepClone(obj);
console.log(obj.msg === obj1.msg)
console.log(obj.list === obj1.list)

=>
false
false

```

以上的克隆对于一般数组和对象有效

1. 可以克隆函数么？不
2. 可以克隆正则，Date对象么？不
3. 可以克隆原型么？不
4. 可以解决循环引用么（环）不

对于以上特殊的几种，我们在看一中简便的方法（江湖流传的妙招）。

### JSON.parse

前几年微博上流传着一个传说中最便捷实现深克隆的方法,JSON对象parse方法可以将JSON字符串反序列化成JS对象，stringify方法可以将JS

对象序列化成JSON字符串,这两个方法结合起来就能产生一个便捷的深克隆.

果然,这是一个实现深克隆的好方法,但是这个解决办法是不是太过简单了.确实,这个方法虽然可以解决绝大部分是使用场景,但是却有很多坑.

1. 他无法实现对函数、RegExp等特殊对象的克隆。
2. 会抛弃对象的constructor,所有的构造函数会指向Object。
3. 对象有循环引用,会报错。

### 基本的深层克隆函数实现

```javascript
function getRegExp(re) {
    var flags = '';
    if (re.global) flags += 'g';
    if (re.ignoreCase) flags += 'i';
    if (re.multiline) flags += 'm';
    returnflags;
};
function isType(obj, type) {
    if (typeof (obj) !== 'object') return false;
    var typeString = Object.prototype.toString.call(obj);
    var flag;
    switch (type) {
        case 'Array':
            flag = typeString === '[object Array]';
            break;
        case 'Date':
            flag = typeString === '[object Date]';
            break;
        case 'RegExp':
            flag = typeString === '[object RegExp]';
            break;
        default:
            flag = false;
    }
    return flag;
}
function clone(parent) {
    //维护两个储存循环引用的数组
    var parents = [];
    var children = [];
    var _clone = parent => {
        if (parent === null) return null;
        if (typeof (parent) !== 'object') return parent;
        var child, proto;
        if (isType(parent, 'Array')) {
            //对数组做特殊处理
            child = [];
        } else if (isType(parent, 'RegExp')) {
            //对正则对象做特殊处理
            child = new RegExp(parent.source, getRegExp(parent));
            if (parent.lastIndex)
                child.lastIndex = parent.lastIndex;
        } else if (isType(parent, 'Date')) {
            //对Date对象做特殊处理
            child = newDate(parent.getTime());
        } else {
            //处理对象原型
            proto = Object.getPrototypeOf(parent);
            //利用Object.create切断原型链
            child = Object.create(proto);
        }
        //处理循环引用
        var index = parents.indexOf(parent);
        if (index != -1) {
            //如果父数组存在本对象,说明之前已经被引用过,直接返回此
            return children[index];
        }
        parents.push(parent);
        children.push(child);
        for (var i in parent) {
            //递归
            if (parent.hasOwnProperty(i)) {//过滤原型属性
                child[i] = _clone(parent[i]);
            }
        }
        return child;
    };
    return _clone(parent);
}

```

//此处待研究









# x==y的判断

## x和y类型相同

1. null==null
2. undefined==undefined
3. +0==-0
4. true==true
5. false==false
6. 对象的引用地址相同则相同
7. 字符串完全相同的字符序列（长度相等且相同字符在相同位置）时返回true。数字相同则为true

不满足以上条件的同类型元素的==式就是false

**对于NaN来说，只要存在NaN就一定是false。**

## x和y类型不同

1. undefined==null值为true这个是规定，不存在类型转换。
2. x和y有一个是boolean类型时,把boolean类型的转成数字进行判断

**转化规则 true==1 false==0**

3. x和y一个是数字另外一个是字符串,把字符串转换成数字在进行比较

4. x和y一个数字另外一个是对象,
   
对象查找valueOf函数,并且返回基本类型值,就是用该值进行强类型转换
如果没有valueOf，或者valueOf返回的不是原始值,继续寻找toString函数
如果toString函数返回的也不是原始值，则会报错

# Javascript访问器属性

大多数情况下我们定义一个对象

```javascript
var person={
    name:'lixiang',
    sayHello:function(){
        console.log('hello')
    }
}
```
通过Object.getOwnPropertyDescriptor把属性特性输出看下

```javascript
Object.getOwnPropertyDescriptor(person,'name')
-->
{value: "lixiang", writable: true, enumerable: true, configurable: true}

```
可以看到不管是字符串还是其他基本类型,它们都有4个属性特性描述
1. [value]:表示属性的数据值。默认值:undefined
2. [writable]:表示能否修改属性的值。默认值:true
3. [enumerable]:表示能否通过for-in,Object.keys()迭代。默认值：true
4. [configurable]:示能否通过delete删除属性，能否修改属性的特性，能否将数据属性和访问器属性互转。默认值true

ES5提供了Object.defineProperty方法，既可以用来定义属性，也可以用来修改属性的特性。

```javascript
Object.defineProperty(person,'name',{writable:false})
```

然后再对person.name赋值的话就无效了。

除了数据属性，还多了访问器属性。

```javascript
var book = {
    _year: 2004,
    edition: 1
}
Object.defineProperty(book, "year", {
    get() {
        return this._year
    },
    set(newValue) {
        if (newValue > 2004) {
            this._year = newValue;
            this.edition += newValue - 2004;
        }
    }
})
```
没有了[Value]和[Writable]，取而代之的是get和set函数。如果set属性没有定义，那么就无法修改book的值。


# dom/bom尺寸相关的属性

## 查看滚动条的滚动距离

1. window窗口滚动条滚动距离

- window.pageYOffset:返回文档再垂直方向已滚动的像素值,只读属性,别名:window.scrollY,pageYOffset支持稍好一些
- window.pageXOffset:返回文档/页面水平方向滚动的像素值,只读属性,别名:window.scrollY,pageXOffset支持稍好一些

ie8及ie8以下

document.body.scrollTop/document.documentElement.scrollTop:返回文档再垂直方向已滚动的像素值
document.body.scrollLeft/document.documentElement.scrollLeft:返回文档/页面水平方向滚动的像素值

由于这两个互斥,一个为0，另一个就是正常值,所以我们可以通过相加来获得很好的支持

兼容性封装如下

```javascript
function getScrollOffset(){
    if(window.pageXOffset){
        return{
            x:window.pageXOffset,
            y:window.pageYOffset
        }
    }else{
        return{
            x:document.body.scrollLeft+document.documentElement.scrollLeft,
            y:document.body.scrollTop+document.documentElement.scrollTop
        }
    }
}
```

`注意javascript中 return后面如果是一个对象,大括号不能写在下一行`


2. dom元素滚动条滚动距离

- Element.scrollLeft 属性可以读取或设置元素滚动条到元素左边的距离。
- Element.scrollTop 属性可以获取或设置一个元素的内容垂直滚动的像素数

## 获取可视区窗口的尺寸

window.innerWidth/window.innerHeight
w3c标准

document.documentElement.clientWidth/document.documentElement.clientHeight
ie8及以下

document.body.clientHeight/document.body.clientHeight
怪异渲染模式(向后兼容,删除第一行就成了怪异渲染)

获取当前渲染模式:document.compatMode

兼容性方法封装

```javascript

function getViewportOffset(){
    if(window.innerWidth){
        return{
            w:window.innerWidth,
            h:window.innerHeight
        }
    }else{
        if(document.compatMode==="BackCompat"){
            return{
                w:document.body.clientWidth,
                h:document.body.clientHeight
            }
        }else{
            return{
                w:document.documentElement.clientWidth,
                h:document.documentElement.clientHeight
            }
        }
    }
}

```

## 查看元素的几何尺寸

1. element.getBoundingClientRect()

该方法返回一个对象，对象里面有left,top,right,bottom等属性。left和top代表该元素左上角的X和Y坐标，right和bottom代表元素右下角的X和Y坐标

height和width属性老版本IE并未实现

返回的结果不是实时的

2. element.clientWidth/element.clientHeight

只读属性 它是元素内部的宽度/高度(单位像素)，包含内边距.但不包括垂直/水平滚动条、边框和外边距

3. HTMLElement.offsetWidth/HTMLElement.offsetHeight

返回一个元素的布局宽度。一个典型的offsetWidth是测量包含元素的边框(border)、水平线上的内边距

(padding)、竖直方向滚动条(scrollbar)（如果存在的话）、以及CSS设置的宽度(width)的值。

4. HTMLElement.offsetLeft/HTMLElement.offsetTop

只读属性，对于无定位父级的元素，返回相对文档的坐标。对于有定位父级的元素，返回相对于最近的有定位的父级的坐标

5. HTMLElement.offsetParent

只读属性，返回最近的有定位的父级，如无，返回body, body.offsetParent 返回null

封装函数,求元素在文档中的坐标

```javascript
function getElementPosition(){

}
```

## 滚动条滚动

### 窗口滚动条滚动

1. window.scroll

滚动窗口至文档中的特定位置。

2. window.scrollTo()

滚动到文档中的某个坐标。同scroll
   
3. window.crollBy()

会在之前的数据基础之上做累加

### 元素滚动条滚动

同窗口滚动条滚动方法

# 查寻计算样式

1. window.getComputedStyle(div,null)[prop]

只读属性,方法返回一个对象，该对象在应用活动样式表并解析这些值可能包含的任何基本计算后报告元素的所有CSS属性的值

ie/ie8不兼容

第二个参数用来获取伪元素样式表

window.getComputedStyle(div,"after").width

2. Element.currentStyle

是一个与 window.getComputedStyle方法功能相同的属性。这个属性实现在旧版本的IE浏览器中.

封装兼容性方法

```javascript
function getStyle(elem,prop){
    if(window.getComputedStyle){
        return window.getComputedStyle(elem,null)[prop];
    }else{
        return elem.currentStyle[prop];
    }
}
```




## 浏览器常驻线程

- js引擎线程 （解释执行js代码、用户输入、网络请求）
- GUI线程 （绘制用户界面、与js主线程是互斥的）
- http网络请求线程 （处理用户的get、post等请求，等返回结果后将回调函数推入任务队列）
- 定时触发器线程 （setTimeout、setInterval等待时间结束后把执行函数推入任务队列中）
- 浏览器事件处理线程 （将click、mouse等交互事件发生后将这些事件放入事件队列中）

![](596947-20160424200428195-1086416163.jpg)


js引擎单线程执行的,它是基于事件驱动的语言.它的执行顺序是遵循一个叫做事件队列的机制.从图中我们可以看出,浏览器有各种各样的线程,比如事件触发器,网络请求,定时器等等.线程的联系都是基于事件的.js引擎处理到与其他线程相关的代码,就会分发给其他线程,他们处理完之后,需要js引擎计算时就是在事件队列里面添加一个任务. 这个过程中,js并不会阻塞代码等待其他线程执行完毕,而且其他线程执行完毕后添加事件任务告诉js引擎执行相关操作.这就是js的异步编程模型.

由此可见官方对于settimeout的定义是有迷惑性的.应该给一个新的定义:

在指定时间内, 将任务放入事件队列,等待js引擎空闲后被执行.

### js引擎与GUI引擎是互斥的

谈到这里,就不得不说浏览器的另外一个引擎---GUI渲染引擎. 在js中渲染操作也是异步的.比如dom操作的代码会在事件队列中生成一个任务,js执行到这个任务时就会去调用GUI引擎渲染.

js语言设定js引擎与GUI引擎是互斥的,也就是说GUI引擎在渲染时会阻塞js引擎计算.原因很简单,如果在GUI渲染的时候,js改变了dom,那么就会造成渲染不同步. 我们需要深刻理解js引擎与GUI引擎的关系,因为这与我们平时开发息息相关,我们时长会遇到一些很奇葩的渲染问题.看这个例子

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
    <table border=1>
        <tr><td><button id='do'>Do long calc - bad status!</button></td>
            <td><div id='status'>Not Calculating yet.</div></td>
        </tr>
        <tr><td><button id='do_ok'>Do long calc - good status!</button></td>
            <td><div id='status_ok'>Not Calculating yet.</div></td>
        </tr>
    </table>    
<script>

function long_running(status_div) {

    var result = 0;
    for (var i = 0; i < 1000; i++) {
        for (var j = 0; j < 700; j++) {
            for (var k = 0; k < 300; k++) {
                result = result + i + j + k;
            }
        }
    }
    document.querySelector(status_div).innerHTML = 'calclation done' ;
}

document.querySelector('#do').onclick = function () {
    document.querySelector('#status').innerHTML = 'calculating....';
    long_running('#status');
};

document.querySelector('#do_ok').onclick = function () {
    document.querySelector('#status_ok').innerHTML = 'calculating....';
    window.setTimeout(function (){ long_running('#status_ok') }, 0);
};

</script>
</body>
</html>
```
我们希望能看到计算的每一个过程,我们在程序开始,计算,结束时,都执行了一个dom操作,插入了代表当前状态的字符串,Not Calculating yet.和calculating....和calclation done.计算中是一个耗时的3重for循环. 在没有使用settimeout的时候,执行结果是由Not Calculating yet 直接跳到了calclation done.这显然不是我们希望的.而造成这样结果的原因正是js的事件循环单线程机制.dom操作是异步的,for循环计算是同步的.异步操作都会被延迟到同步计算之后执行.也就是代码的执行顺序变了.calculating....和calclation done的dom操作都被放到事件队列后面而且紧跟在一起,造成了丢帧.无法实时的反应.这个例子也告诉了我们,在需要实时反馈的操作,如渲染等,和其他相关同步的代码,要么一起同步,要么一起异步才能保证代码的执行顺序.在js中,就只能让同步代码也异步.即给for计算加上settimeout.




# Bind的模拟实现

bind()方法创建一个新的函数，在bind()被调用时，这个新函数的this被bind的第一个参数指定，其余的参数将作为新函数的参数供调用时使用。


```javascript
var list={
    init:function(){
        this.ms='dd';
        this.dom=document.getElement('btn');
        this.bindEvent();
    },
    bindEvent:function(){
        this.dom.onclick=this.showMessage.bind(this);
    },
    showMessage:function(){
        console.show(this);//=>list
    }
}
```
`返回一个新的函数,this指向了list,apply/call直接改变this指向并且执行,bind改变this指向,返回一个新函数,在需要触发的时候执行`


bind()返回的函数通过new 执行

```javascript

function show(){
    console.log(this)
}

var dd={
    x:20
}

var newShow = show.bind(dd)

new newShow()

=>this不会生效


```

模拟实现bind

```javascript

Function.prototype.newBind=function(target){
    var args=[].slice.call(arguments,1);
    var self=this;
    var temp=function(){};
    var f= function(){
        var _arg = [].slice.call(arguments,0)
        return self.apply(this.instanceof tmp ? target||window,args.concat(_arg));
    }
    tmp.prototype=self.prototype;
    f.prototype=new temp()
    return f;
}



Function.prototype.newBind = function (target) {
    var args = [].splice.call(arguments, 1);
    var self = this;
    var tempfunc = Object.create(self.prototype);
    var f = function () {
        var _arg = [].splice.call(arguments, 0);
        return self.apply(tempfunc.constructor.prototype.isPrototypeOf(this) ? this : target || window, args.concat(_arg))
    }
    f.prototype = tempfunc;
    return f;
}
var d = new show();
var bindShow = show.bind(dd);
var newBindShow = show.newBind(dd);

```

# 纯函数

纯函数被定义为不依赖或修改其作用域之外的变量的函数。

使用这个函数来计算用户的鼠标是否在页面的左侧，如果是，则记录 true，否则记录 false。

```javascript
function mouseOnLeftSide(mouseX) {
    return mouseX < window.innerWidth / 2;
}

document.onmousemove = function(e) {
    console.log(mouseOnLeftSide(e.pageX));
};
```

这个函数被赋予了 mouseX，但是没有 window.innerWidth。 这意味着该函数正在访问它没有给出的数据，因此它不是纯数据。

优化后

```javascript
function mouseOnLeftSide(mouseX, windowWidth) {
    return mouseX < windowWidth / 2;
}

document.onmousemove = function(e) {
    console.log(mouseOnLeftSide(e.pageX, window.innerWidth));
};
```

# 函数柯里化

在数学和计算机科学中，柯里化是一种将使用多个参数的一个函数转换成一系列使用一个参数的函数的技术。

```javascript

function FixedParamCurry(fn){
    var _arg=[].slice.call(arguments,1);
    return function(){
        var newArg=_arg.concat([].slice.call(arguments,0));
        return fn.apply(this,newArg);
    }
}

function Curry(fn,length){
    var length=length||fn.length;
    return function(){
        if(arguments.length < length>){
            var combined=[fn].concat([].slice.call(arguments,0));
            return Curry(FixedParameCurry.apply(this,combined),length-arguments.length);
        }
    }
}

```

另外一种实现

```javascript
function curry(func){
    var args=[].slice.call(arguments,1);
    return function(){
        var subArgs=[].slice.call(arguments,0);
        var newArgs=args.concat(subArgs);

        if(newArgs.length >= func.length){
            return func.apply(null,newArgs);
        }else{
            newArgs.unshift(func);
            return func.apply(null,newArgs);
        }
    }
}

/**
    * 创建一个dom元素
    */
function createDom(container, attrs, styles, type, content) {
    //创建一个新的元素，设置指定的属性、样式、内容，将该元素加入到指定的容器中
    var dom = document.createElement(type);
    //添加属性
    for (var prop in attrs) {
        dom[prop] = attrs[prop];
    }
    //添加样式
    for (var prop in styles) {
        dom.style[prop] = styles[prop];
    }
    dom.innerHTML = content;
    container.appendChild(dom);
}
var container = document.querySelector(".container"); //容器
var create1 = curry(createDom, container, {
    className: "item"
}, {
    color: "red",
    background: "#ccc",
    fontSize:"3em"
}); //固定前三个参数

create1("p", "123");
create1("div", "456");
create1("header", "abc");
create1("section", "23422");
create1("div", "12asdfasfasdf3");
```


## 函数管道

函数管道：将多个单参函数(有返回值)进行组合，形成一个新的函数

```javascript
function Pipe() {
    //得到所有的参数（假设所有参数均为单参函数）
    var args = Array.prototype.slice.call(arguments);
    return function (data) {
        for (var i = 0; i < args.length; i++) {
            var func = args[i];
            data = func(data);
        }
        return data;
    }
}

//去掉一个字符串的所有空白字符，返回一个新字符串
function removeEmpty(str) {
    return str.replace(/\s/g, ""); //替换空白字符返回
}

//将每个单词首字母大写
function firstLetterUp(str) {
    return str.replace(/\b(\w)(\w*)\b/g, function($, $1, $2) {
        return $1.toUpperCase() + $2;
    })
}

//将每个单词除首字母外，其他字母小写
function notFirstLetterLower(str) {
    return str.replace(/\b(\w)(\w*)\b/g, function($, $1, $2) {
        return $1 + $2.toLowerCase();
    })
}

//将字符串截取指定的长度
function cutString(start, len, str) {
    return str.substr(start, len);
}
//实现大驼峰命名
var cut = curry(cutString, 0, 8);
var pipe = Pipe(notFirstLetterLower, firstLetterUp, removeEmpty, cut);
console.log(pipe("mY fIrSt    nAmE"));
```


# 浏览器中输入url,网络中会发生什么

至少发出2个请求,先查找dns-ip映射,在直接访问ip

如:url:123.xyz

1. 看浏览器缓存映射,
2. 看本机host
3. 路由器->上级路由、城市的DNS服务器->上级->gDNS服务器有没有缓存映射

# get和post的区别

1. 基于什么前提的?如果什么前提都没有,不使用任何规范,只考虑语法和理论上的http协议,get和post几乎没有什么区别,只有名字不一样
2. 如果是基于RFC规范的
   1)理论上:get和post具有相同语法的,但是有不同的语义,get是用来获取数据的,post是用来发送数据的,其他方面没有区别
   2)实现上:各种浏览器,就是这个规范的实现者。
   常见的不同:
   1)get的数据在url(不一定显示在地址栏)是可见的.post请求不显示在URL中.
   2)get的长度是由限制的,post长度是无限的
   3)get请求的数据可以收藏为书签,post请求到的数据不可收藏为书签
   4)get请求后,按后退按钮、刷新按钮无影响,post数据会被重新提交.
   5)get编码类型:application/x-www-form-url,post的编码类型有很多种,encodeapplication/x-www-form-urlencoded、multipart/form-data
   6)get历史参数会被保留在浏览器里,post不会保存在浏览器中
   7)get只允许ASCII,post没有编码限制,允许发二进制的.
   8)get与post相比,get安全性较差,因为所发的数据是url的一部分


# 网络请求的方式

1. 在浏览器直接输入地址
2. location.href=url 可以发出网络请求,但是页面会发生跳转
3. 带有src属性的标签.请求是可以发出的,服务端是可以处理也是可以返回的.但是返回之后能否被应用,还要看浏览器
4. 带有href属性的标签.请求是可以发出的,服务端是可以处理也是可以返回的.但是返回之后能否被应用,还要看浏览器
5. 带有action属性的标签.例如form表单,但是form表单发出请求之后,也会发生页面跳转
6. ajax

```javascript
var xhr = null;
if(window.XMLHttpRequest){
    xhr=new XMLHttpRequest();
}else{
    xhr=new ActiveXObject("Microsoft.XMLHttp");
}
xhr.open("get","http://developer.duyiedu.com/edu/testAjax");
//写在发送前
xhr.onreadystatechange=function(){
    //==4表示请求完成
    //2**成功
    //3**重定向
    //4**客户端错误
    //5**表示服务器错误
    if(xhr.readyState==4 && xhr.status==200){
        console.log(xhr.responseText);
    }
}
xhr.send();
```

## 跨域访问资源

那些东西属于资源?
js文件算资源,css文件,jpg、png等.可以被跨域请求
src属性的资源都是跨域被跨域请求的.href资源大部分都是可以跨域请求的

## 跨域请求的资源
1. 后端接口的数据
2. 其他域的cookie
3. 其他域的缓存

什么是其他域?怎么样算跨域

页面本身:有协议、域名、端口

协议、域名、端口这三个,有任意一个不一样就算跨域

## 跨域行为发生在那里

1. 即使跨域了,请求也可以发出
2. 服务端也是可以接受的、正常处理的、正常返回数据
3. 浏览器也可以接受到数据
4. 接收到之后,发现当前页面的域和请求的域不一样,判定为跨域
5. 我们的代码在这等着结果呢,但是因为浏览器判定为跨域了,不会把结果传递给我们的代码

## 解决跨域问题

1. 后端是配合我们进行跨域
   1. JSONP(正常的情况,返回的数据都是JSON格式.JSONP是一种特殊的格式) 只能是get方法,JQury如果输入post 会自动转换为get方法 
   2. 后端设置Access-Control-Allow-Origin属性以支持跨域
2. 后端不配合我们进行跨域
   1. iframe(只能显示,不能控制)
   2. 通过后端代理

是不是在jsonp里面只能使用get方法,是不是设置的post方法都会转为get方法？
不是
jquery会先判断同源,如果是同源,那么设置的是get就是get,post就是post
如果不是同源,无论设置什么都改为get.

# josnp原理

script标签,虽然可以引用其他域的资源,浏览器不限制,但是浏览器会将返回的内容,作为js代码执行,利用这个可以返回一个回调函数,然后本地js代码实现回调函数.达到了跨域的目的

1. 判断请求是否同源,同源则发送正常的ajax,就没有跨域的事情了
2. 如果不同源生成一个script标签,生成一个随机的callback名字,设置script的src属性,创建一个名字为callback名字的方法
3. 将callback作为参数拼接到后面
4. 后端收到请求,拼接数据,将要返回的数据用callback的值和括号包裹起来(callback=asd123456,要返回的数据{a:1,b:2},则要返回为asd123456({a:1,b:2})),
5. 浏览器接收到内容,会当作js代码执行,从而执行asd123456()方法

```javascript
var $ = {
    ajax: function (options) {
        var url = options.url;
        var type = options.type;
        var dataType = options.dataType;
        var targetProtocol = "";  //目标接口的协议
        var targetHost = ""; //目标接口的host
        //如果url不带http,访问的一定是相对路径,相对路径一定是同源的
        if (url.indexOf("http://") == 0 || url.indexOf("https://") == 0) {
            var targetUrl = new URL(url);
            targetProtocol = targetUrl.protocol;
            targetHost = targetUrl.host;
        } else {
            targetProtocol = location.protocol;
            targetProtocol = location.host;
        }
        if (dataType == "jsonp") {
            //同源
            if (location.protocol == targetProtocol && location.host == targetHost) {
                //同源的jsonp当作普通ajax发送
            } else {
                var callback = "cb" + Math.floor(Math.random() * 1000000);

                window[callback] = options.success;

                var script = document.createElement("script");

                if (url.indexOf('?') > 0) {
                    script.src = url + "&callback=" + callback;
                } else {
                    script.src = url + "?callback=" + callback;
                }
                script.id = callback;
                document.head.appendChild(script);
            }
        }
    }
}

$.ajax({
    url: "http://developer.duyiedu.com/edu/testJsonp",
    type: "get",
    dataType: "jsonp",
    success: function (data) {
        console.log(data);
    }
});
```



# tcp的三次握手和四次挥手

## 三次握手

三次握手（Three-way Handshake）其实就是指建立一个TCP连接时，需要客户端和服务器总共发送3个包。进行三次握手的主要作用就是为了确认双方的接收能力和发送能力是否正常、指定自己的初始化序列号为后面的可靠性传送做准备。

![](tcphandle.png)

## 四次挥手

建立一个连接需要三次握手，而终止一个连接要经过四次挥手（也有将四次挥手叫做四次握手的）。这由TCP的半关闭（half-close）造成的。所谓的半关闭，其实就是TCP提供了连接的一端在结束它的发送后还能接收来自另一端数据的能力。

TCP 的连接的拆除需要发送四个包，因此称为四次挥手(Four-way handshake)，客户端或服务器均可主动发起挥手动作。

![](tcpnohandle.png)


# 网页性能管理(重排和重绘)

网页的生成过程,大致可以分为五步

1. HTML代码转化成DOM
2. css代码转化为CSSDOM(CSS OBJECT MODEL)
3. 结合DOM和CSSOM，生成一棵渲染树（包含每个节点的视觉信息）
4. 生成布局（layout），即将所有渲染树的所有节点进行平面合成
5. 将布局绘制（paint）在屏幕上

这五步里面，第一步到第三步都非常快，耗时的是第四步和第五步。

**"生成布局"（flow）和"绘制"（paint）这两步，合称为"渲染"（render）。**

以下三种情况，会导致网页重新渲染。

1. 修改DOM
2. 修改样式表
3. 用户事件（比如鼠标悬停、页面滚动、输入框键入文字、改变窗口大小等等）
   
**重新渲染，就需要重新生成布局和重新绘制。前者叫做"重排"（reflow），后者叫做"重绘"（repaint）。**