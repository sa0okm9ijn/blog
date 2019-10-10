---
title: Javascript专题系列
date: 2019-09-19 16:05:08
tags: 
- JavaScript 
categories: JavaScript 
description: 主要写一些特定对象的更全面的用法和讲解
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
