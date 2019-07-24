---
title: JavaScript Dom
date: 2019-05-29 10:40:48
tags: 
- JavaScript 
categories: JavaScript 
description: 
---
## Dom接口

用来操作html和xml功能的一系列对面的集合。

## 查找方法

//ie8 以及ie8 以下不支持
```
document.getElementsByClassName

document.getElementsByTagName
```
//css选择器---非实时
```
document.querySelector

document.querySelectorAll

var div = document.getElementsByClassName("div")[0];

var div2 = document.getElementsByTagName("div")[0];


//不是实时
document.querySelector('div > span strong.demo')//css 选择器
document.querySelectorAll('div > span');//css选择器
```
### 遍历节点树

    
```
//ie9以下都不兼容
//节点包含
//文本节点、注释节点、元素节点
//parentNode--->父节点(最顶端#docuemnt);
//childNodes---->子节点
//firstChild--第一子节点
//lastChild--最后一个节点
//nextSibling--下一个节点
//previousSibling--上一个节点
```

### 遍历元素节点树

    
```
//基于元素节点   ie9以下支支持children
//parentElement--父元素节点
//children-->子元素节点--
//nextElementSibling--下一个元素节点
//previousSibling--上一个元素节点


//nodeName 节点名称
//nodeValue 文本节点和注释节点才有
//nodeType
//元素节点1
//属性节点2----div.attributes
//文本节点3
//注释节点8

//hasChildNodes()  是否有子节点
```
**  示例--不用children查找元素的子元素节点**

    
```
function retElementChild(node) {

        var temp={
            length:0,
            push:Array.prototype.push,
            splice:Array.prototype.splice
        },
            child=node.childNodes,
            len = child.length;

        for(var i = 0; i < len;i++)
        {
            if(child[i].nodeType===1){
                temp.push(child[i]);
            }
        }
        return temp;
    }
```

## Dom结构树

![](584421-20190420153649449-1411688931.png)

以上描述了Dom的原型链。如document继承自HTMLDocument.prototype。HTMLDocument.prototype继承自Document

![](584421-20190420153855373-1549524433.png)

  * getElementById定义在Document.prototype上
  * getElementByName定于在HTMLDocument上，即非html中不可以使用
  * getElementsByTagName定义在Document.prototype和Element.prototype上
  * HtMLDocument.propotype定义上了body,head，直接代表标签
  * documentElement 代替html元素

练习

    
```
//返回子元素节点  不用children
function retElementChild(node) {

    var temp = {
        length: 0,
        push: Array.prototype.push,
        splice: Array.prototype.splice
    },
        child = node.childNodes,
        len = child.length;

    for (var i = 0; i < len; i++) {
        if (child[i].nodeType === 1) {
            temp.push(child[i]);
        }
    }
    return temp;
}


//返回元素elem的第n层父元素
function retParent(elem, n) {
    while (elem && n) {
        elem = elem.parentElement;
        n--;
    }
    return elem
}
//不用children返回子元素节点
Element.prototype.myChildren = function () {
    var child = this.childNodes;
    var len = child.length;
    var arr = [];

    for (var i = 0; i < len; i++) {
        if (child[i].nodeType == 1) {
            arr.push(child[i]);
        }
    }
    return arr;
}



//返回兄弟节点，n可以为负数
function retSibling(e, n) {
    while (e & n) {
        if (n > 0) {
            e = e.nextElementSibling;//ie9以下不支持
            n--;
        }
        else {
            e = e.previousElementSibling;//ie9以下不支持
            n++;
        }
    }
    return e;
}
function retSibling(e, n) {
    while (e & n) {
        if (n > 0) {
            if (e.nextElementSibling) {
                e = e.nextElementSibling
            } else {
                for (e = e.nextSibling; e && e.nodeType != 1; e = e.nextSibling);
            }
            n--;
        }
        else {
            if (e.previousElementSibling) {
                e = e.previousElementSibling;//ie9以下不支持
            } else {
                for (e = e.proviousSibling; e && e.nodeType != 1; e = e.proviousSibling);
            }
            n++;
        }
    }
    return e;
}


//appendChild  剪切操作
//insertBefore(a,b) 增加a在b之前
//removeChild  删除子节点   剪切
//replceChild(new,origin) new替换origin  剪切



Element.prototype.insertAfter = function (targetNode, afterNode) {
    var beforeNode = afterNode.nextElementSibling;
    if(beforeNode==null)
    {
        this.appendChild(targetNode);
    }else{
        this.insertBefore(targetNode,beforeNode);
    }

}
```