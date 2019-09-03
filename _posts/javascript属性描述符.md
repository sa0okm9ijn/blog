---
title: javascript属性描述符
date: 2019-07-12 06:33:31
tags: 
- JavaScript
categries: JavaScript
description: 属性描述符（Property Descriptor）是 ES5 之后出现的概念，顾名思义，它用于描述属性应该是什么样，例如是否只读，能否枚举，能否可配置等。所有对象属性均可使用属性描述符来定义。
---

## 属性描述符

我们的在js中创建的对象平常用的的属性一般都是元数据，即metadata,描述数据的数据。
如:
```
var obj = {
    att1:1,
    att2:2
}
```
有时候因为特殊的需要可能需要一些特殊的对象，这个时候我们就需要属性描述符来实现了。下面我就以下两个问题展开属性描述符的概念

1、为什么div.innerText就会让界面显示了内容
2、为什么循环div的时候拿不到innerText这个属性

属性描述符（Property Descriptor）是 ES5 之后出现的概念，顾名思义，它用于描述属性应该是什么样，例如是否只读，能否枚举，能否可配置等。所有对象属性均可使用属性描述符来定义。
对象里目前存在的属性描述符有两种主要形式：数据描述符和存取描述符。数据描述符是一个具有值的属性，该值可能是可写的，也可能不是可写的。存取描述符是由getter-setter函数对描述的属性。描述符必须是这两种形式之一；不能同时是两者。

描述符可同时具有的键值

|   | configuration | enumerable | value | writable | get | set |
|---|---            |---         |---    |---       |---  |---  |   
|数据描述符   | Yes  | Yes        | Yes   | Yes      | No  | No  |
|存取描述符   | Yes  | Yes        | No    | No       | Yes | Yes |


属性描述符定义属性通过defineProperty

### 示例1 控制年龄的输入
```
<script>
    var user = {
        name: 'xxx',
        __age: 0
    }
    //通过属性描述符定义一个属性
    Object.defineProperty(user, 'age', {
        get: function () {
            return this.__age;
        },
        set: function (val) {
            if (val < 0 || val > 100) {
                throw new Error("赋值的数据" + val + "不在可用的范围中，可用的范围是：0~100");
            }
            this.__age = val;
        }
    });
    user.age=101;
    console.log(user.age);
</script>
```
我们可以控制我们年龄范围为1-99，如果设置年龄除了范围，则会抛出异常，如图
![2019-07-12_112104](2019-07-12_112104.png)


### 示例2 圆的自由滚动

```
<script>
    function Circle() {
        this.width = 100;
        this.height = 100;
        this.dom = document.querySelector(".circle");
        this.__left = 0;
        this.__top = 0;
        this.xDis = 2;
        this.yDis = 2;
        Object.defineProperty(this, "left", {
            get: function () {
                return this.__left;
            },
            set: function (val) {
                if (val < 0) {
                    this.xDis = -this.xDis;
                    val = 0;
                }
                else if (val > document.documentElement.clientWidth - this.width) {
                    val = document.documentElement.clientWidth - this.width;
                    this.xDis = -this.xDis;
                }
                this.__left = val;
                this.dom.style.left = val + "px";
            }
        });
        Object.defineProperty(this, "top", {
            get: function () {
                return this.__top;
            },
            set: function (val) {
                if (val < 0) {
                    this.yDis = -this.yDis;
                    val = 0;
                } else if (val > document.documentElement.clientHeight - this.height) {
                    val = document.documentElement.clientHeight - this.height;
                    this.yDis = -this.yDis;
                }
                this.__top = val;
                this.dom.style.top = val + "px";
            }
        });
    }
    var circle = new Circle();
    setInterval(() => {
        circle.left += circle.xDis;
        circle.top += circle.yDis;
    }, 10);
</script>
```

可以发现当我们设置了属性left之后小球就会移动，这也就解释了上面的第一个问题设置了innerText界面会刷新值的问题


下面我们说说描述符的具有的键值

```
var obj = {};

Object.defineProperty(obj,"abc",{
    enumerable:true,//是否可以遍历
    value:123,//该属性的值
    writable:false //该值是否可以重新赋值
})
```
由上
```
Object.defineProperty(Object.prototype, "toString", {
    enumerable: true
})

for(var prop in Object.prototype){
    console.log(prop);
}
```
上面结果会打出打出toString,所以上面的第二个问题我们也有了结果，div的innerText属性描述符为不可遍历，所以循环打不出来