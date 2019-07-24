---
title: JavaScript this
date: 2019-05-29 10:45:09
tags: 
- JavaScript 
categories: JavaScript 
description: 与其他语言相比，函数的 this 关键字在 JavaScript 中的表现略有不同，此外，在严格模式和非严格模式之间也会有一些差别。 
---

在绝大多数情况下，函数的调用方式决定了this的值。this不能在执行期间被赋值，并且在每次函数被调用时this的值也可能会不同。ES5引入了bind方法来设置函数的this值，而不用考虑函数如何被调用的


## 全局环境

是否在严格模式下，在全局执行环境中（在任何函数体外部）this 都指向全局对象。

```
// 在浏览器中, window 对象同时也是全局对象：
console.log(this === window); // true

a = 37;
console.log(window.a); // 37

this.b = "MDN";
console.log(window.b)  // "MDN"
console.log(b)         // "MDN"

```

## 函数运行内环境
this 的值默认指向全局对象。
```
function f1(){
  return this;
}
//在浏览器中：
f1() === window;  //true   //在浏览器中，全局对象是window

```

## call apply

如果想把this的指向改变，就要用call或者apply方法

```
    var obj = {
        a:"Custom"
    };
    var a  ="global";
    function whatsThis(arg){
        return this.a;
    }
    console.log(whatsThis());//"global";
    console.log(whatsThis.call(obj)); //Custom
    console.log(whatsThis.apply(obj)); //Custom
    
```
call和apply调用的时候，传递参数

```
    function add(c, d) {
        return this.a + this.b + c + d;
    }
    var o = {
        a: 1,
        b: 3
    }
    //第一个参数是做为this使用的对象
    //后续参数作为参数传递给函数使用
    add.call(o, 5, 7);

    //第一个参数是做为this使用的对象
    //第二个参数是一个数组,数组里的元素作用域函数调用中的参数
    add.apply(o,[5,7])

```

## bind
ECMAScript 5 引入了 Function.prototype.bind。bind()方法创建一个新的函数，在调用时设置this关键字为提供的值。

```
    this.x = 9;
    var module = {
        x: 81,
        getX: function () {
            return this.x;
        }
    }
    module.getX();  //81
    var retrieveX = module.getX;
    retrieveX();//9--因为函数在全局作用域中调用的


    //创建一个新函数 把this绑定到module对象
    var boundGetX = retrieveX.bind(module);
    boundGetX(); //81

```

bind只可生效一次

```
    function f() {
            return this.a;
        }
    var g = f.bind({ a: "1" });  //bind只可生效一次  不可传递绑定
    var h = g.bind({ a: "2" });
    var i = h.bind({ a: "3" });
    console.log(g()) //1
    console.log(h()) //1
    console.log(i()) //1

```

谁调用this指向谁

```
    function f() {
            return this.a;
        }

    var g = f.bind({ a: "azerty" });
    console.log(g()); // azerty

    var h = g.bind({ a: 'yoo' }); // bind只生效一次！
    console.log(h()); // azerty

    var o = { a: 37, f: f, g: g, h: h };
    //o.f()  this指向o
    console.log(o.f(), o.g(), o.h()); // 37, azerty, azerty

```








