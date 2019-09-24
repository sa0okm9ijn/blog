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


