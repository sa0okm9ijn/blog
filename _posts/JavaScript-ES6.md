---
title: JavaScript-ES6
date: 2020-01-05 09:25:53
tags: 
- JavaScript 
categories: JavaScript 
description: JavaScript ( JS ) 是一种具有函数优先的轻量级，解释型或即时编译型的编程语言。虽然它是作为开发Web 页面的脚本语言而出名的，但是它也被用到了很多非浏览器环境中，例如 Node.js、 Apache CouchDB 和 Adobe Acrobat。JavaScript 是一种基于原型编程、多范式的动态脚本语言，并且支持面向对象、命令式和声明式（如函数式编程）风格。
---

# ES6 课程概述

1. ECMAScript、JavaScript、NodeJs，它们的区别是什么？

ECMAScript：简称ES，是一个语言标准（循环、判断、变量、数组等数据类型）

JavaScript：运行在浏览器端的语言，该语言使用ES标准。 ES + web api = JavaScript

NodeJs：运行在服务器端的语言，该语言使用ES标准。 ES + node api = NodeJs

无论JavaScript，还是NodeJs，它们都是ES的超集（super set）

2. ECMAScript有哪些关键的版本？

ES3.0： 1999

ES5.0:  2009

ES6.0:  2015, 从该版本开始，不再使用数字作为编号，而使用年份

ES7.0:  2016

3. 为什么ES6如此重要？

ES6解决JS无法开发大型应用的语言层面的问题。


# 块级绑定

## 申明变量的问题

使用var声明变量
1. 允许重复的变量声明：导致数据被覆盖
```javascript
var a = 1;
function print(){
    console.log(a)
}
//假设这里有一千行代码
var a = 2;
print();
```
2. 变量提升：怪异的数据访问、闭包问题
```javascript
//怪异数据访问
if (Math.random() < 0.5) {
    var a = "abc";
    console.log(a);
}
else {
    console.log(a);
}
console.log(a);
//变量提升：闭包问题
var div = document.getElementById("divButtons")

for (var i = 1; i <= 10; i++) {
    var btn = document.createElement("button");
    btn.innerHTML = "按钮" + i;
    div.appendChild(btn);
    btn.onclick = function () {
        console.log(i); //输出11
    }
}
```
3. 全局变量挂载到全局对象：全局对象成员污染问题
```js
var console = "abc";
console.log(console)
```

### 使用let申明变量

ES6不仅引入let关键字用于解决变量声明的问题，同时引入了块级作用域的概念

块级作用域：代码执行时遇到花括号，会创建一个块级作用域，花括号结束，销毁块级作用域

声明变量的问题

1. 允许重复的变量声明：导致数据被覆盖 
```js
let a = 123;

let a = 456; // 检查到，当前作用域（全局作用域）已声明了变量a
```
    let声明的变量，不允许当前作用域范围内重复声明

2. 变量提升：怪异的数据访问、闭包问题
```js
//怪异数据访问
if (Math.random() < 0.5) {
    let a = 123; //定义在当前块级作用域
    console.log(a) //当前块级作用域中的a
}
else {
    //这是另外一个块级作用域，该作用域中找不到a
    console.log(a)
}
//变量提升：闭包问题
let div = document.getElementById("divButtons");

for (let i = 1; i <= 10; i++) {
    let button = document.createElement("button")
    button.innerHTML = "按钮" + i;
    button.onclick = function () {
        console.log(i) //使用的是当前作用域中的i
    }
    div.appendChild(button)
}
```
    底层实现上，let声明的变量实际上也会有提升，但是，提升后会将其放入到“暂时性死区”，如果访问的变量位于暂时性死区，则会报错：``Cannot access 'a' before initialization``。当代码运行到该变量的声明语句时，会将其从暂时性死区中移除。

    在循环中，用let声明的循环变量，会特殊处理，每次进入循环体，都会开启一个新的作用域，并且将循环变量绑定到该作用域（每次循环，使用的是一个全新的循环变量）
    在循环中使用let声明的循环变量，在循环结束后会销毁
1. 全局变量挂载到全局对象：全局对象成员污染问题
    let声明的变量不会挂载到全局对象

### 使用const申明变量
const和let完全相同，仅在于用const声明的变量，必须在声明时赋值，而且不可以重新赋值。
实际上，在开发中，应该尽量使用const来声明变量，以保证变量的值不会随意篡改，原因如下：

1. 根据经验，开发中的很多变量，都是不会更改，也不应该更改的。
2. 后续的很多框架或者是第三方JS库，都要求数据不可变，使用常量可以一定程度上保证这一点。

注意的细节：

1. 常量不可变，是指声明的常量的内存空间不可变，并不保证内存空间中的地址指向的其他空间不可变。
```js
const a = {
    name: "kevin",
    age: 123
};
a.name = "abc";
console.log(a)
```
2. 常量的命名
   1. 特殊的常量：该常量从字面意义上，一定是不可变的，比如圆周率、月地距地或其他一些绝不可能变化的配置。通常，**该常量的名称全部使用大写，多个单词之间用下划线分割**
   2. 普通的常量：使用和之前一样的命名即可
3. 在for循环中，循环变量不可以使用常量(``for in`` 可以)

# 字符串和正则表达式

## 更好的unicode支持

早期，由于存储空间宝贵，Unicode使用16位二进制来存储文字。我们将一个16位的二进制编码叫做一个码元（Code Unit）。
后来，由于技术的发展，Unicode对文字编码进行了扩展，将某些文字扩展到了32位（占用两个码元），并且，将某个文字对应的二进制数字叫做码点（Code Point）。

由于js长时间没有更新,es6之前js认为一个码点就是一个码元,因此取字符串长度是按照码元来取的,在正则表达式也是按照码元来匹配的.

```js
const text='𠮷'//占用2个码元
console.log(text.length);//输出长度为2
console.log(/^.$/.test(text));//输出为false
//==>2
```

ES6为了解决这个困扰，为字符串提供了方法：codePointAt，根据字符串码元的位置得到其码点。

```js
console.log(test.codePointAt(0))//获取第一个码点,如果该字符串由2个码元组成,则返回2个码元的组成.
console.log(text.codePointAt(0))//正常返回第二个码点
```

同时，ES6为正则表达式添加了一个flag: u，如果添加了该配置，则匹配时，使用码点匹配
```js
console.log(`使用正则测试:`,/^.$/u.test(test))
```

**应用**

```js
function is32Bit(char,i){
 	return char.codePointAt(i) > 0xffff; 
}
function getLengthOfCodePoint(str){
	var len = 0;
  	for(let i = 0;i<str.length;i++){
        //碰到𠮷是32位置的多加一位置,下一次循环就到a了
    	if(is32Bit(str,i)){
        	i++;
        }
      	len++;
    }
  	return len;
}
console.log('𠮷是否是32位的:',is32Bit('𠮷',0))
console.log("ab𠮷ab的码点长度：", getLengthOfCodePoint("ab𠮷ab"))
```



## 更多的字符串API

以下均为字符串的实例（原型）方法

- includes

判断字符串中是否包含指定的子字符串

- startsWith

判断字符串中是否以指定的字符串开始

- endsWith

判断字符串中是否以指定的字符串结尾

- repeat

将字符串重复指定的次数，然后返回一个新字符串。

```js
const text="挺简单的哦";
console.log("是否包含`哦`：", text.includes("哦"));
console.log("是否以“挺简”开头：", text.startsWith("挺简"));
console.log("是否以“哦”结尾：", text.endsWith("哦"));
console.log("重复4次：", text.repeat(4));
```

## 正则中的粘连标记

标记名：y

含义：匹配时，完全按照正则对象中的lastIndex位置开始匹配，并且匹配的位置必须在lastIndex位置。

```js
const text='Hello World';

const reg=/W\w+/y;
reg.lastIndex = 6;
console.log("reg.lastIndex:", reg.lastIndex)
console.log(reg.test(text))
```

## 模板字符串

S6之前处理字符串繁琐的两个方面：

1. 多行字符串
2. 字符串拼接


在ES6中，提供了模板字符串的书写，可以非常方便的换行和拼接，要做的，仅仅是将字符串的开始或结尾改为 ` 符号

如果要在字符串中拼接js表达式，只需要在模板字符串中使用```${JS表达式}```

```js
var love1 = "秋葵";
var love2 = "香菜";

var text = `邓哥喜欢${love1}
邓哥也喜欢${love2}
表达式可以是任何有意义的数据${1 + 3 * 2 / 0.5}
表达式是可以嵌套的：${`表达式中的模板字符串${love1 + love2}`}
\n\n
奥布瓦的发顺丰
在模板字符串中使用\${JS表达式}可以进行插值
`;

console.log(text);
```

## 模板字符串标记
在模板字符串书写之前，可以加上标记:

```js
标记名`模板字符串`
```

标记是一个函数，函数参数如下：

1. 参数1：被插值分割的字符串数组
2. 后续参数：所有的插值

```js
var love1 = "秋葵";
var love2 = "香菜";

var text = myTag`邓哥喜欢${love1}，邓哥也喜欢${love2}。`;

//相当于： 
// text = myTag(["邓哥喜欢", "，邓哥也喜欢", "。"], "秋葵", "香菜")

function myTag(parts) {
    const values = Array.prototype.slice.apply(arguments).slice(1);
    let str = "";
    for (let i = 0; i < values.length; i++) {
        str += `${parts[i]}：${values[i]}`;
        if (i === values.length - 1) {
            str += parts[i + 1];
        }
    }
    return str;
}

console.log(text);
```

输出转义标记
```js
var text = String.raw`abc\t\nbcd`;

console.log(text);
```

**示例**
```js
//html
<p>
    <textarea name="" id="txt" cols="30" rows="10"></textarea>
    <button id="btn">设置div内容</button>
</p>
<div id="container">

</div>
//js
const container = document.getElementById("container");
const txt = document.getElementById("txt");
const btn = document.getElementById("btn");
btn.onclick = function () {
    container.innerHTML = safe`<p>${txt.value}</p><h1>${txt.value}</h1>`;
}
function safe(parts) {
    const values = Array.prototype.slice.apply(arguments).slice(1);
    let str = "";
    for (let i = 0; i < values.length; i++) {
        const v = values[i].replace(/</g, "&lt;").replace(/>/g, "&gt;");
        str += parts[i] + v;
        if (i == values.length - 1) {
            str += parts[i + 1];
        }
    }
    return str;
}
```

# 函数

## 参数默认值

### 使用

在书写形参时，直接给形参赋值，附的值即为默认值

这样一来，当调用函数时，如果没有给对应的参数赋值（给它的值是undefined），则会自动使用默认值。

```js
function sum(a, b = 1, c = 2) {
    return a + b + c;
}
console.log(sum(10, undefined, undefined))
console.log(sum(11))
console.log(sum(1, undefined, 5))
```

### 对arguments的影响

只要给函数加上参数默认值，该函数会自动变量严格模式下的规则：arguments和形参脱离
```js
function test(a,b=1){
	console.log("arugments", arguments[0], arguments[1]);
  	console.log("a:", a, "b:", b);
  	a=3;
  	console.log("arugments", arguments[0], arguments[1]);
  	console.log("a:", a, "b:", b);
}
test(2);
```

### 留意暂时性死区
形参和ES6中的let或const声明一样，具有作用域，并且根据参数的声明顺序，存在暂时性死区。

```js
function test(a,b=a){
    console.log(a,b)
}
test(1)
function test(a=b,b){
    console.log(a,b)
}
//如果第一个a=b,则会出现错误
```

## 剩余参数

arguments的缺陷：

1. 如果和形参配合使用，容易导致混乱
2. 从语义上，使用arguments获取参数，由于形参缺失，无法从函数定义上理解函数的真实意图

ES6的剩余参数专门用于收集末尾的所有参数，将其放置到一个形参数组中。

语法:

```js
function (...形参名){

}
```

**细节：**

1. 一个函数，仅能出现一个剩余参数
2. 一个函数，如果有剩余参数，剩余参数必须是最后一个参数

```js
function sum(...args) {
    //args收集了所有的参数，形成的一个数组
    let sum = 0;
    for (let i = 0; i < args.length; i++) {
        sum += args[i];
    }
    return sum;
}

console.log(sum())
console.log(sum(1))
console.log(sum(1, 2))
console.log(sum(1, 2, 3))
console.log(sum(1, 2, 3, 4))
```

## 展开运算符

使用方式：```  ...要展开的东西  ```

### 对数组展开 ES6

对于剩余参数的展开
```js
const arr=[1,2,3,4,5,6];

function sum(...args){
	let sum=0;
  	for(let i = 0 ; i < args.length;i++){
    	sum+=args[i];
    }
  	return sum;
}

console.log(sum(...arr));
console.log(sum(1,2,3,...arr,4,5,6))
```

克隆数组
```js
const arr1=[3,67,8,5];
const arr2=[0,1,2,...arr1,4];
console.log(arr2,arr1===arr2)
```

### 对对象展开 ES7

对象克隆

```js
const obj1={
	name:"ggbond",
  	age:12,
  	address:{
    	country:"中国",
      	province:"陕西",
      	city:"西安"
    }
};

const obj2={
	...obj1,
  	name:'ge',
  	address:{
		...obj1.address
	}
};

console.log(obj2,obj1.address===obj2.address);
```


## 剩余参数和展开运算符练习


```js

//函数柯里化

function cal(a,b,c,d){
	return a+b*c-d;
};

function curry(func,...args){
	return function(...subargs){
    	const allArgs = [...args,...subargs];
      	if(allArgs.length >= func.length){
        	return func(...allArgs);
        }else{
        	return curry(func,...allArgs);
        }
    }
}

const newCal = curry(cal, 1, 2)

console.log(newCal(3, 4)) // 1+2*3-4
const newCal2 = newCal(8)

console.log(newCal2(9)); // 1+2*8-9

```

## 明确函数的双重用途

ES6提供了一个特殊的API，可以使用该API在函数内部，判断该函数是否使用了new来调用

```js
new.target 
//该表达式，得到的是：如果没有使用new来调用函数，则返回undefined
//如果使用new调用函数，则得到的是new关键字后面的函数本身
```

```js
function Person(firstName,lastName){
    // //过去的判断方式
    // if (!(this instanceof Person)) {
    //     throw new Error("该函数没有使用new来调用")
    // }
    if(new.target === undefined){
        throw new Error('该函数没有使用new来调用');
    }
    this.firstName=firstName;
    this.lastName=lastName;
}
```

## 箭头函数

回顾：this指向

1. 通过对象调用函数，this指向对象
2. 直接调用函数，this指向全局对象
3. 如果通过new调用函数，this指向新创建的对象
4. 如果通过apply、call、bind调用函数，this指向指定的数据
5. 如果是DOM事件函数，this指向事件源

### 使用语法

箭头函数是一个函数表达式，理论上，任何使用函数表达式的场景都可以使用箭头函数

* 完整语法：
```js
const obj = {
    count: 0,
    start: function () {
        setInterval(() => {
            this.count++;
            console.log(this.count);
        }, 1000)
    },
    regEvent: function () {
        window.onclick = () => {
            console.log(this.count);
        }
    },
    print: function () {
        console.log(this)
        console.log(this.count)
    }
}

// obj.start();
// obj.regEvent();
obj.print();
```

* 如果参数只有一个，可以省略小括号
```js
const print = num => {
    console.log("给我的数字是：", num)
}
print(2);
```

* 如果箭头函数只有一条返回语句，可以省略大括号，和return关键字
```js
const isOdd = num => num % 2 !== 0;
```
* 返回对象
```js
const sum = (a, b) => ({
    a: a,
    b: b,
    sum: a + b
});

```


### 注意细节
- 箭头函数中，不存在this、arguments、new.target，如果使用了，则使用的是函数外层的对应的this、arguments、new.target
```js
const func = () => {
    console.log(this)
}

const obj = {
    method: function(){
        const func = () => {
            console.log(this)
            console.log(arguments)
        }
        func()
    }
}
obj.method(234);

//指向obj和method方法里的arguments

const func = () => {
    console.log(this)
}
//指向window
```
- 箭头函数没有原型
- 箭头函数不能作用构造函数使用

### 应用场景

1. 临时性使用的函数，并不会刻意调用它，比如：
   1. 事件处理函数
   2. 异步处理函数
   3. 其他临时性的函数
2. 为了绑定外层this的函数
3. 在不影响其他代码的情况下，保持代码的简洁，最常见的，数组方法中的回调函数

# 对象

## 对象字面量写法
```js
const user = {
    name: "姬成",
    age: 100,
    sayHello(){
        console.log(this.name, this.age)
    }
}

user.sayHello();
```

1. 成员速写
如果对象字面量初始化时，成员的名称来自于一个变量，并且和变量的名称相同，则可以进行简写
```js
function createUser(loginId, loginPwd, nickName) {
    const sayHello = function () {
        console.log("loginId", this.loginId, "nickname", this.nickName)
    }
    return {
        loginId,
        loginPwd,
        nickName,
        sayHello,
        id: Math.random()
    }
}
const u = createUser("abc", "123", "aaa");
u.sayHello();
```
2. 方法速写
对象字面初始化时，方法可以省略冒号和function关键字
```js
var obj = {
	print(){
    	console.log('123')
    }
}
obj.print()
```
3. 计算属性名
有的时候，初始化对象时，某些属性名可能来自于某个表达式的值，在ES6，可以使用中括号来表示该属性名是通过计算得到的。
```js
const prop1 = "name2";
const prop2 = "age2";
const prop3 = "sayHello2";

const user = {
    [prop1]: "姬成",
    [prop2]: 100,
    [prop3](){
        console.log(this[prop1], this[prop2])
    }
}

user[prop3]();

console.log(user)
```

## Object新增的API

1. Object.is
用于判断两个数据是否相等，基本上跟严格相等（===）是一致的，除了以下两点：
1) NaN和NaN相等
2) +0和-0不相等
```js
console.log(NaN===NaN)//false
console.log(+0===-0)//true

console.log(Object.is(NaN,NaN))//true
console.log(Object.is(+0,-0))//false
```

2. Object.assign
用于混合对象
```js
const obj1 = {
    a: 123,
    b: 456,
    c: "abc"
}
const obj2 = {
    a: 789,
    d: "kkk"
}
const obj = Object.assign({}, obj1, obj2);
```

3. Object.getOwnPropertyNames

Object.getOwnPropertyNames方法之前就存在，只不过，官方没有明确要求，对属性的顺序如何排序，如何排序，完全由浏览器厂商决定。

ES6规定了该方法返回的数组的排序方式如下：

- 先排数字，并按照升序排序
- 再排其他，按照书写顺序排序

```js
const obj = {
    d: 1,
    b: 2,
    a: 3,
    0: 6,
    5: 2,
    4: 1
}
const props = Object.getOwnPropertyNames(obj)
console.log(props)
//["0", "4", "5", "d", "b", "a"]
```

4. Object.setPrototypeOf
该函数用于设置某个对象的隐式原型
比如： Object.setPrototypeOf(obj1, obj2)，
相当于：  ``` obj1.__proto__ = obj2 ```
```js
const obj1 = {
    a: 1
}
const obj2 = {
    b: 2
}
Object.setPrototypeOf(obj1, obj2)
console.log(obj1)
```

## 面向对象简介

面向对象：一种编程思想，跟具体的语言


对比面向过程：

- 面向过程：思考的切入点是功能的步骤
```js
//1. 冰箱门打开
function openFrige(){

}
openFrige();

//2. 大象装进去
function elephantIn(){

}

elephantIn();

//3. 冰箱门关上
function closeFrige(){

}

closeFrige();
```
- 面向对象：思考的切入点是对象的划分
```js
/**
 * 大象
 */
function Elephant() {

}

/**
 * 冰箱
 */
function Frige() {

}

Frige.prototype.openDoor = function () {

}

Frige.prototype.closeDoor = function () {

}

Frige.prototype.join = function(something){
    this.openDoor();
    //装东西

    this.closeDoor();
}
var frig = new Frige();

frig.join(new Elephant());
```

【大象装冰箱】

## 类

构造函数的语法糖

### 传统的构造函数的问题

1. 属性和原型方法定义分离，降低了可读性
```js
//面向对象中，将 下面对一个对象的所有成员的定义，统称为类

//构造函数  构造器
function Animal(type, name, age, sex) {
    this.type = type;
    this.name = name;
    this.age = age;
    this.sex = sex;
}
//定义实例方法（原型方法）
Animal.prototype.print = function () {
    console.log(`【种类】：${this.type}`);
    console.log(`【名字】：${this.name}`);
    console.log(`【年龄】：${this.age}`);
    console.log(`【性别】：${this.sex}`);
}

```
2. 原型成员可以被枚举
```js
const a = new Animal("狗", "旺财", 3, "男");
a.print();

for (const prop in a) {
    console.log(prop)
}
```
3. 默认情况下，构造函数仍然可以被当作普通函数使用
```js
Animal()
```

### 类的特点

1. 类声明不会被提升，与 let 和 const 一样，存在暂时性死区
2. 类中的所有代码均在严格模式下执行
3. 类的所有方法都是不可枚举的
4. 类的所有方法都无法被当作构造函数使用
5. 类的构造器必须使用 new 来调用
```js
class Animal{
    constructor(type,name,age,sex){
        this.type = type;
        this.name = name;
        this.age = age;
        this.sex = sex;
    }
    print(){
        console.log(`【种类】：${this.type}`);
        console.log(`【名字】：${this.name}`);
        console.log(`【年龄】：${this.age}`);
        console.log(`【性别】：${this.sex}`);
    }
}
const a = new Animal("狗", "旺财", 3, "男");
a.print();

for (const prop in a) {
    console.log(prop)
}
```

## 类的其他书写方式

1. 可计算的成员名
```js
const printName = "print";
class Animal {
    constructor(type, name, age, sex) {
        this.type = type;
        this.name = name;
        this.age = age;
        this.sex = sex;
    }

    [printName]() {
        console.log(`【种类】：${this.type}`);
        console.log(`【名字】：${this.name}`);
        console.log(`【年龄】：${this.age}`);
        console.log(`【性别】：${this.sex}`);
    }
}
const a = new Animal("狗", "旺财", 3, "男");
a[printName]();
```

2. getter和setter
Object.defineProperty 可定义某个对象成员属性的读取和设置
用getter和setter控制的属性，不在原型上
```js
const printName = "print";
class Animal {
    constructor(type, name, age, sex) {
        this.type = type;
        this.name = name;
        this.age = age;
        this.sex = sex;
    }
    //创建一个age属性，并给它加上getter，读取该属性时，会运行该函数
    get age() {
        return this._age + "岁";
    }

    //创建一个age属性，并给它加上setter，给该属性赋值时，会运行该函数
    set age(age) {
        if (typeof age !== "number") {
            throw new TypeError("age property must be a number");
        }
        if (age < 0) {
            age = 0;
        }
        else if (age > 1000) {
            age = 1000;
        }
        this._age = age;
    }

    [printName]() {
        console.log(`【种类】：${this.type}`);
        console.log(`【名字】：${this.name}`);
        console.log(`【年龄】：${this.age}`);
        console.log(`【性别】：${this.sex}`);
    }
}
var a = new Animal("狗", "旺财", 3, "男");
```

3. 静态成员
构造函数本身的成员
使用static关键字定义的成员即静态成员
```js
class Chess {
    constructor(name) {
        this.name = name;
    }

    static width = 50;

    static height = 50;

    static method() {

    }
}
console.log(Chess.width)
console.log(Chess.height)
Chess.method();
```

4. 字段初始化器（ES7）
注意：
    1). 使用static的字段初始化器，添加的是静态成员
    2). 没有使用static的字段初始化器，添加的成员位于对象上
```js
class Test {
    static a = 1;
    b = 2;
    c = 3;

    constructor() {
        this.d = this.b + this.c;
    }
}
const t = new Test();
console.log(t)
```
    3). 箭头函数在字段初始化器位置上，指向当前对象
```js
class Test {
    constructor() {
        this.a = 123;
    }
    print = () => {
        console.log(this.a)
    }
}
const t1 = new Test();
const t2 = new Test();
t1.print()
t2.print()
console.log(t1.print === t2.print)
```
5. 类表达式
类本质上是一个函数,所以也可以写成一个表达式
```js
const A = class { //匿名类，类表达式
    a = 1;
    b = 2;
}
const a = new A();
console.log(a)
```
6. [扩展]装饰器（ES7）(Decorator)
装饰器的本质是一个函数
```js
class Test {

    @Obsolete
    print() {
        console.log("print方法")
    }
}

function Obsolete(target, methodName, descriptor) {
    // function Test
    // print
    // { value: function print(){}, ... }
    // console.log(target, methodName, descriptor);
    const oldFunc = descriptor.value
    descriptor.value = function (...args) {
        console.warn(`${methodName}方法已过时`);
        oldFunc.apply(this, args);
    }
}
```

## 类的继承

如果两个类A和B，如果可以描述为：B 是 A，则，A和B形成继承关系

如果B是A，则：

1. B继承自A
2. A派生B
3. B是A的子类
4. A是B的父类

如果A是B的父类，则B会自动拥有A中的所有实例成员。


新的关键字：

- extends：继承，用于类的定义
- super
  - 直接当作函数调用，表示父类构造函数
  - 如果当作对象使用，则表示父类的原型

注意：ES6要求，如果定义了constructor，并且该类是子类，则必须在constructor的第一行手动调用父类的构造函数

如果子类不写constructor，则会有默认的构造器，该构造器需要的参数和父类一致，并且自动调用父类构造器

```js

class Animal {
    constructor(type, name, age, sex) {
        this.type = type;
        this.name = name;
        this.age = age;
        this.sex = sex;
    }

    print() {
        console.log(`【种类】：${this.type}`);
        console.log(`【名字】：${this.name}`);
        console.log(`【年龄】：${this.age}`);
        console.log(`【性别】：${this.sex}`);
    }

    jiao(){
        throw new Error("动物怎么叫的？");
    }
}

class Dog extends Animal {
    constructor(name, age, sex) {
        super("犬类", name, age, sex);
        // 子类特有的属性
        this.loves = "吃骨头";
    }

    print(){
        //调用父类的print
        super.print();
        //自己特有的代码
        console.log(`【爱好】：${this.loves}`);
    }


    //同名方法，会覆盖父类
    jiao(){
        console.log("旺旺！");
    }
}
```


【冷知识】

- 用JS制作抽象类
  - 抽象类：一般是父类，不能通过该类创建对象
```js
class Animal {
    constructor(type, name, age, sex) {
        if (new.target === Animal) {
            throw new TypeError("你不能直接创建Animal的对象，应该通过子类创建")
        }
        this.type = type;
        this.name = name;
        this.age = age;
        this.sex = sex;
    }

    print() {
        console.log(`【种类】：${this.type}`);
        console.log(`【名字】：${this.name}`);
        console.log(`【年龄】：${this.age}`);
        console.log(`【性别】：${this.sex}`);
    }

    jiao() {
        throw new Error("动物怎么叫的？");
    }
}
//只能字类来创建，animal不可以直接创建
```
- 正常情况下，this的指向，this始终指向具体的类的对象


# 解构

使用ES6的一种语法规则，将一个对象或数组的某个属性提取到某个变量中

**解构不会对被解构的目标造成任何影响**

## 对象解构
```js
const obj = {
    name:'ge',
    age:1
}
let {name,age}=obj
let name,age;
({name,age}=obj)
```

### 在解构中使用默认值
```js
const obj = {
    name:'ge',
    age:1
}
//当没有address的时候用默认值
let {name,age,address='北京'}=obj
console.log(name,age,address)
```

### 非同名属性解构
```js
const obj = {
    name:'ge',
    age:1,
  	sex:'男'
}
//声明了name,age,address,gender4个变量,并obj同名属性赋值,sex值赋给gender
let {name,age,address='北京',sex:gender}=obj
console.log(name,age,address,gender)
```

### 深层次解构
```js
const obj = {
    name:'ge',
    age:1,
  	sex:'男',
  	wife:{
    	wifename:'bea',
      	wifesex:'女'
    }
}

let {name,wife:{ wifesex }}=obj;
console.log(name,wifesex);
```

### 剩余项解构

只能是最后一项

```js
const obj={
    name:'ge',
    age:1,
    sex:0
}
const {name,...obj2}=obj;
//obj中name放到name中,其余项组成obj2对象
```

## 数组解构

其他用法参考对象

```js
const arr=["a","b","c"]
const {0:n1,1:n2}=arr;
console.log(n1,n2)

const arr=["a","b"];

//简便写法
const [n1,n2]=arr;

let n1,n2;
([n1,n2]=arr);
console.log(n1,n2)
(n1,,n2)=arr;

```

**解构实现交换**

```js
let a = 1, b=2;
[b,a]=[a,b]
```

## 参数解构

1. 基本用法
```js
function print({name,age,sex,address:{province,city}}){
    console.log(`姓名:${name}`);
}
const User={
    name:'kevin',
    age:11,
    sex:'0',
    address:{
        province:'陕西',
        city:'西安'
    }
}
print(User)
```
2. 不传参数的处理-参数解构不能从undefined解构,给默认值为{}
```js
function ajax({
    method = 'get',
    url = '/'
} = {}) {
    console.log(method, url);
}
ajax();
```

# 符号

符号是ES6新增的一个数据类型，它通过使用函数 ```Symbol(符号描述)``` 来创建
符号设计的初衷，是为了给对象设置私有属性
私有属性：只能在对象内部使用，外面无法使用

符号具有以下特点:
- 没有字面量
- 使用 typeof 得到的类型是 symbol
- **每次调用 Symbol 函数得到的符号永远不相等，无论符号名是否相同**
```js
const syb1=Symbol("abc");
const syb2 = Symbol("abc");

console.log(syb1,syb2);//Symbol(abc) Symbol(abc)
console.log(typeof(syb1)=== "symbol",typeof(syb2)==="symbol")//true,true
console.log(syb1 === syb2)//false
```
- 符号可以作为对象的属性名存在，这种属性称之为符号属性
  - 开发者可以通过精心的设计，让这些属性无法通过常规方式被外界访问
  - 符号属性是不能枚举的，因此在 for-in 循环中无法读取到符号属性，Object.keys 方法也无法读取到符号属性
  - Object.getOwnPropertyNames 尽管可以得到所有无法枚举的属性，但是仍然无法读取到符号属性
  - ES6 新增 Object.getOwnPropertySymbols 方法，可以读取符号
```js
const syb1 = Symbol("用于对象属性的符号")
const obj = {
a: 1,
b: 2,
[syb1]: 3
}
console.log(obj);
for(const prop in obj){
console.log(prop);
}
console.log(Object.keys(obj));
console.log(Object.getOwnPropertyNames(obj));
//得到的是一个符号属性的数组
const sybs = Object.getOwnPropertySymbols(obj);
console.log(sybs);
console.log(sybs, sybs[0] === syb1)
//类的方式声明 隐藏成员
const Hero = (() => {
    const getRandom = Symbol();
    return class {
        constructor(attack, hp, defence) {
            this.attack = attack;
            this.hp = hp;
            this.defence = defence;
        }

        gongji() {
            //伤害：攻击力*随机数（0.8~1.1)
            const dmg = this.attack * this[getRandom](0.8, 1.1);
            console.log(dmg);
        }

        [getRandom](min, max) {
            return Math.random() * (max - min) + min;
        }
    }
})()
const h = new Hero(3, 6, 3);
console.log(h);
//获取sym符号属性
const sybs= Object.getOwnPropertySymbols(Hero.prototype);
const prop=sybs[0];
console.log(h[prop](3,5));
```
- 符号无法被隐式转换，因此不能被用于数学运算、字符串拼接或其他隐式转换的场景，但符号可以显式的转换为字符串，通过 String 构造函数进行转换即可，console.log 之所以可以输出符号，是它在内部进行了显式转换

## 共享符号
根据某个符号名称（符号描述）能够得到同一个符号

1. 基本用法
```js
//Symbol.for("符号名/符号描述")  //获取共享符号
const syb1 = Symbol.for('abc');
const syb2 = Symbol.for('abc');
console.log(syb1 === syb2);

const obj1={
    a:1,
    b:2,
    [syb1]:3
}

const obj2={
    a:1,
    b:2,
    [syb1]:3
}

console.log(obj1,obj2);
```
2. 语法糖
```js
const obj = {
    a: 1,
    b: 2,
    [Symbol.for("c")]: 3
}
console.log(obj[Symbol.for("c")]);
```

3. 自己实现一个共享符号
```js
const SymbolFor = (() => {
    const global = {}; //用于记录有哪些共享符号
    return function (name) {
        console.log(global);
        if (!global[name]) {
            global[name] = Symbol[name];
        }
        console.log(global);
        return global[name];
    }
})();
const syb1 = SymbolFor("abc");
const syb2 = SymbolFor("abc");
console.log(syb1 === syb2);
```

## 知名符号

知名符号是一些具有特殊含义的共享符号，通过 Symbol 的静态属性得到

ES6 延续了 ES5 的思想：减少魔法，暴露内部实现！

**魔法:搞不清楚的实现,不能插手的事情以及一些内部的实现**

因此，ES6 用知名符号暴露了某些场景的内部实现


1. Symbol.hasInstance

该知名符号影响 instanceof 的判定,
```js
//以前我们无法改变instanceof的判断结果,现在我们就可以通过hasInstance符号来改变
function A() {

}

Object.defineProperty(A, Symbol.hasInstance, {
    value: function (obj) {
        return false;
    }
})
const obj = new A();
console.log(obj instanceof A);//返回false
console.log(A[Symbol.hasInstance](obj));
```

2. [扩展] Symbol.isConcatSpreadable

该知名符号会影响数组的 concat 方法

```js
const arr=[3];
const arr2=[5,6,7,8];

arr2[Symbol.isConcatSpreadable] = false;

const result = arr.concat(56,arr2);
console.log(result)

const arr = [1];
const obj={
    0:3,
    1:4,
    length:2,
    [Symbol.isConcatSpreadable]:true
}

const result=arr.concat(2,obj);
console.log(result);
```

3. [扩展] Symbol.toPrimitive

该知名符号会影响类型转换的结果

```js
class Temperature {
    constructor(degree) {
        this.degree = degree;
    }

    [Symbol.toPrimitive](type) {
        console.log(type);
        if (type === 'default') {
            return this.degree + '摄氏度'
        } else if (type === 'number') {
            return this.degree
        } else if (type === "string") {
            return this.degree + "℃";
        }
    }
}

const t = new Temperature(30);

console.log(t + "!"); //先调用默认的转换行为  valueof  在tostring
console.log(t / 2); //转换为数字
console.log(String(t)); //转换为string
```

4. [扩展] Symbol.toStringTag

该知名符号会影响 Object.prototype.toString 的返回值

```js
class Person{
    [Symbol.toStringTag] = "Person"
}

const p = new Person();
const arr=[3243,432,32];

console.log(Object.prototype.toString.apply(p)); //p.toString()//被重写了
console.log(Object.prototype.toString.apply(arr));//arr.toString() //被重写了
```

5. 其他知名符号

# 异步处理

## [回顾]事件循环

JS运行的环境称之为宿主环境。

执行栈：call stack，一个数据结构，用于存放各种函数的执行环境，每一个函数执行之前，它的相关信息会加入到执行栈。函数调用之前，创建执行环境，然后加入到执行栈；函数调用之后，销毁执行环境。

JS引擎永远执行的是执行栈的最顶部。

异步函数：某些函数不会立即执行，需要等到某个时机到达后才会执行，这样的函数称之为异步函数。比如事件处理函数。异步函数的执行时机，会被宿主环境控制。

浏览器宿主环境中包含5个线程：

1. JS引擎：负责执行执行栈的最顶部代码
2. GUI线程：负责渲染页面 
3. 事件监听线程：负责监听各种事件
4. 计时线程：负责计时
5. 网络线程：负责网络通信

当上面的线程发生了某些事请，如果该线程发现，这件事情有处理程序，它会将该处理程序加入一个叫做事件队列的内存。当JS引擎发现，执行栈中已经没有了任何内容后，会将事件队列中的第一个函数加入到执行栈中执行。

JS引擎对事件队列的取出执行方式，以及与宿主环境的配合，称之为事件循环。


事件队列在不同的宿主环境中有所差异，大部分宿主环境会将事件队列进行细分。在浏览器中，事件队列分为两种：

- 宏任务（队列）：macroTask，计时器结束的回调、事件回调、http回调等等绝大部分异步函数进入宏队列
- 微任务（队列）：MutationObserver，Promise产生的回调进入微队列

> MutationObserver用于监听某个DOM对象的变化
```js
let count = 1;
const ul = document.getElementById("container");
document.getElementById("btn").onclick = function () {
    setTimeout(() => {
        console.log('添加了一个li');
    }, 0);//宏队列
    var li = document.createElement("li");
    li.innerText = count++;
    ul.appendChild(li);
}
const observer = new MutationObserver(function B() {
    console.log('ul元素发生了变化');//微队列
});
observer.observe(ul, {
    attributes: true,//监听属性的变化
    childList: true,//监听子元素的变化
    subtree: true //监听子树的变化
})
```
当执行栈清空时，JS引擎首先会将微任务中的所有任务依次执行结束，如果没有微任务，则执行宏任务。

## 事件和回调函数的缺陷

我们习惯于使用传统的回调或事件处理来解决异步问题

事件：某个对象的属性是一个函数，当发生某一件事时，运行该函数

回调：运行某个函数以实现某个功能的时候，传入一个函数作为参数，当发生某件事的时候，会运行该函数。

本质上，事件和回调并没有本质的区别，只是把函数放置的位置不同而已。

一直以来，该模式都运作良好。

直到前端工程越来越复杂...

目前，该模式主要面临以下两个问题：

1. 回调地狱：某个异步操作需要等待之前的异步操作完成，无论用回调还是事件，都会陷入不断的嵌套
- 事件产生回调地狱
```js
//html
<button id="btn1">按钮1:给按钮2注册点击事件</button>
<button id="btn2">按钮2:给按钮3注册点击事件</button>
<button id="btn3">按钮3:点击后弹出hello</button>
//js
const btn1 = document.getElementById("btn1"),
      btn2 = document.getElementById("btn2"),
      btn3 = document.getElementById("btn3");
    btn1.addEventListener("click", function () {
    btn2.addEventListener("click", function () {
        btn3.addEventListener("click", function () {
            alert('hello');
        })
    })
});
```
- 回调产生回调地狱
   - 回调函数在参数
```js
/*
表白女神,王麻子跟女神表白,如果女神拒绝,则向第二个女神表白,直到所有的女神都拒绝,或有一个女神同意为止
*/
function biaobai(god, callback) {
    console.log(`王麻子向女神${god}发了表白短信`);
    setTimeout(() => {
        if (Math.random() < 0.1) {
            callback(true);//同意
        } else {
            callback(false);//拒绝
        }
    }, 1000);
}
biaobai('女神1', function (result) {
    if (result) {
        console.log('女神1答应了');
    } else {
        biaobai('女神2', function (result) {
            if (result) {
                console.log('女神2答应了');
            } else {
                biaobai("女神3", function (result) {
                    if (result) {
                        console.log("女神3答应了");
                    } else {
                        console.log("邓哥表示生无可恋!!");
                    }
                })
            }
        })
    }
}) 
```
   - 回调函数在对象参数中 ,ajax参考jquery实现
```js
ajax({
    url: './data/students.json',
    success: function (data) {
        for (let i = 0; i < data.length; i++) {
            if (data[i].name === '李华') {
                const cid = data[i].classId;
                ajax({
                    url: './data/classes.json',
                    success: function (data) {
                        for (let i = 0; i < data.length; i++) {
                            if (data[i].id === cid) {
                                const tid = data[i].teacherId;
                                ajax({
                                    url: './data/teachers.json',
                                    success: function (data) {
                                        for (let i = 0; i < data.length; i++) {
                                            if (data[i].id === tid) {
                                                console.log(data[i]);
                                            }
                                        }
                                    }
                                })
                            }
                        }
                    }
                })
            }
        }
    }
})
```
2. 异步之间的联系：某个异步操作要等待多个异步操作的结果，对这种联系的处理，会让代码的复杂度剧增
```js
/*
    隔壁老王心中有二十个女神，他决定用更加高效的办法
    他同时给二十个女神表白，如果有女神同意，就拒绝其他的女神
    并且，当所有的女神回复完成后，他要把所有的回复都记录到日志进行分析
    用代码模拟上面的场景
*/
function biaobai(god, callback) {
    console.log(`隔壁老王向女神【${god}】发出了表白短信`);
    setTimeout(() => {
        if (Math.random() < 0.05) {
            //女神同意拉
            callback(true);
        } else {
            callback(false);
        }
    }, Math.floor(Math.random() * (3000 - 1000) + 1000));
}
let agreeGod = null; //第一个同意的女神
const results = [];
for (let i = 0; i < 20; i++) {
    biaobai(`女神${i}`, result => {
        results.push(result);
        if (result) {
            console.log(`女神${i}同意了`)
            if (agreeGod) {
                console.log(`隔壁老王回复女神${i}: 滚蛋`);
            } else {
                agreeGod = `女神${i}`;
                console.log(`隔壁老王终于找到了真爱`);
            }
        } else {
            console.log(`女神${i}拒绝了`)
        }
        if (results.length === 20) {
            console.log("日志记录", results)
        }
    })
} 
```


## 异步处理的通用模型

ES官方参考了大量的异步场景，总结出了一套异步的通用模型，该模型可以覆盖几乎所有的异步场景，甚至是同步场景。

值得注意的是，为了兼容旧系统，ES6 并不打算抛弃掉过去的做法，只是基于该模型推出一个全新的 API，使用该API，会让异步处理更加的简洁优雅。

理解该 API，最重要的，是理解它的异步模型

1. ES6 将某一件可能发生异步操作的事情，分为两个阶段：**unsettled** 和 **settled**

![](2019-10-18-17-28-30.png)

- unsettled： 未决阶段，表示事情还在进行前期的处理，并没有发生通向结果的那件事
- settled：已决阶段，事情已经有了一个结果，不管这个结果是好是坏，整件事情无法逆转

事情总是从 未决阶段 逐步发展到 已决阶段的。并且，未决阶段拥有控制何时通向已决阶段的能力。

2. ES6将事情划分为三种状态： pending、resolved、rejected
- pending: 挂起，处于未决阶段，则表示这件事情还在挂起（最终的结果还没出来）
- resolved：已处理，已决阶段的一种状态，表示整件事情已经出现结果，并是一个可以按照正常逻辑进行下去的结果
- rejected：已拒绝，已决阶段的一种状态，表示整件事情已经出现结果，并是一个无法按照正常逻辑进行下去的结果，通常用于表示有一个错误

既然未决阶段有权力决定事情的走向，因此，未决阶段可以决定事情最终的状态！

我们将 把事情变为resolved状态的过程叫做：**resolve**，推向该状态时，可能会传递一些数据

我们将 把事情变为rejected状态的过程叫做：**reject**，推向该状态时，同样可能会传递一些数据，通常为错误信息

**始终记住，无论是阶段，还是状态，是不可逆的！**

![](2019-10-18-18-10-18.png)

3. 当事情达到已决阶段后，通常需要进行后续处理，不同的已决状态，决定了不同的后续处理。

- resolved状态：这是一个正常的已决状态，后续处理表示为 thenable
- rejected状态：这是一个非正常的已决状态，后续处理表示为 catchable

后续处理可能有多个，因此会形成作业队列，这些后续处理会按照顺序，当状态到达后依次执行

![](2019-10-18-18-10-38.png)

4. 整件事称之为Promise

![](2019-10-18-18-15-52.png)

**理解上面的概念，对学习Promise至关重要！**

## Promise的基本使用

1. 基本语法
```js
const pro = new Promise((resolve,reject)=>{
    // 未决阶段的处理
    // 通过调用resolve函数将Promise推向已决阶段的resolved状态
    // 通过调用reject函数将Promise推向已决阶段的rejected状态
    // resolve和reject均可以传递最多一个参数，表示推向状态的数据
})
pro.then(data=>{
    //这是thenable函数，如果当前的Promise已经是resolved状态，该函数会立即执行
    //如果当前是未决阶段，则会加入到作业队列，等待到达resolved状态后执行
    //data为状态数据
},err=>{
    //这是catchable函数，如果当前的Promise已经是rejected状态，该函数会立即执行
    //如果当前是未决阶段，则会加入到作业队列，等待到达rejected状态后执行
    //err为状态数据
})
```

**细节**

1. 未决阶段的处理函数是同步的，会立即执行
2. thenable和catchable函数是异步的，就算是立即执行，也会加入到事件队列中等待执行，并且，加入的队列是微队列
```js
const pro = new Promise((resolve, reject) => {
    console.log('a');
    resolve(1);
    setTimeout(() => {
        console.log('b');
    }, 0);//宏队列
})
pro.then(data => {
    console.log(data);//微队列
})
console.log("c");
//ac1b
```
3. pro.then可以只添加thenable函数或添加thenable和catchable函数，pro.catch可以单独添加catchable函数
```js
//一起添加
ajax({
    url: './data/students.json?name=李华'
}).then(resp => {
    console.log(resp)
}, err => {
    console.log(err)
})
//单独添加
pro.then(data => {
    console.log(data);
})
pro.catch(err => {
    console.log(err);
})
```
4. 在未决阶段的处理函数中，如果发生**未捕获**的错误，会将状态推向rejected，并会被catchable捕获
```js
//未捕获的错误 
const pro = new Promise((resolve, reject) => {
    //pro rejected
    throw new Error('123');
})
pro.then(data => {
    console.log(data);
})
pro.catch(err => {
    console.log(err);
})
//捕获的错误
const pro = new Promise((resolve, reject) => {
    //pro resolve
    try{
        throw new Error('123');
    }catch{
        
    }
    resolve(1);
    
})
pro.then(data => {
    console.log(data);
})
pro.catch(err => {
    console.log(err);
})
```
5. 一旦状态推向了已决阶段，无法再对状态做任何更改
6. **Promise并没有消除回调，只是让回调变得可控**

## Promise的串联

当后续的Promise需要用到之前的Promise的处理结果时，需要Promise的串联

Promise对象中，无论是then方法还是catch方法，它们都具有返回值，返回的是一个全新的Promise对象，它的状态满足下面的规则：
1. 如果当前的Promise是未决的，得到的新的Promise是挂起状态
2. 如果当前的Promise是已决的，会运行响应的后续处理函数，并将后续处理函数的结果（返回值）作为resolved状态数据，应用到新的Promise中；如果后续处理函数发生错误，则把返回值作为rejected状态数据，应用到新的Promise中。

**后续的Promise一定会等到前面的Promise有了后续处理结果后，才会变成已决状态**

如果前面的Promise的后续处理，返回的是一个Promise，则返回的新的Promise状态和后续处理返回的Promise状态保持一致。

```js
const pro = ajax({
    url: "./data/students.json"
})
pro.then(resp => {
    for (let i = 0; i < resp.length; i++) {
        if (resp[i].name === "李华") {
            return resp[i].classId; //班级id
        }
    }
}).then(cid => {
    return ajax({
        url: "./data/classes.json?cid=" + cid
    }).then(cls => {
        for (let i = 0; i < cls.length; i++) {
            if (cls[i].id === cid) {
                return cls[i].teacherId;
            }
        }
    })
}).then(tid => {
    return ajax({
        url: "./data/teachers.json"
    }).then(ts => {
        for (let i = 0; i < ts.length; i++) {
            if (ts[i].id === tid) {
                return ts[i];
            }
        }
    })
}).then(teacher => {
    console.log(teacher);
})
```

## Promise的其他api
### 原型成员 (实例成员)
- then：注册一个后续处理函数，当Promise为resolved状态时运行该函数
- catch：注册一个后续处理函数，当Promise为rejected状态时运行该函数
- finally：[ES2018]注册一个后续处理函数（无参），当Promise为已决时运行该函数

```js
const pro = new Promise((resolve, reject) => {
    reject(1);
});
pro.finally(() => console.log("finally1"))
pro.finally(() => console.log("finally2"))
pro.then(resp => console.log("then1", resp * 1));
pro.then(resp => console.log("then2", resp * 2));
pro.catch(resp => console.log("catch1", resp * 1));
pro.catch(resp => console.log("catch2", resp * 2));
```

### 构造函数成员 （静态成员）

- resolve(数据)：该方法返回一个resolved状态的Promise，传递的数据作为状态数据
  - 特殊情况：如果传递的数据是Promise，则直接返回传递的Promise对象  
- reject(数据)：该方法返回一个rejected状态的Promise，传递的数据作为状态数据
```js
// const pro = new Promise((resolve, reject) => {
//     resolve(1);
// })
//等效于：
// const pro = Promise.resolve(1);

// const pro = new Promise((resolve, reject) => {
//     reject(1);
// })
//等效于：
// const pro = Promise.reject(1);

const p = new Promise((resolve, reject) => {
    resolve(3);
})
const pro = Promise.resolve(p);
//等效于
//const pro = p;
console.log(pro === p)
```
- all(iterable)：这个方法返回一个新的promise对象，该promise对象在iterable参数对象里所有的promise对象都成功的时候才会触发成功，一旦有任何一个iterable里面的promise对象失败则立即触发该promise对象的失败。这个新的promise对象在触发成功状态以后，会把一个包含iterable里所有promise返回值的数组作为成功回调的返回值，顺序跟iterable的顺序保持一致；如果这个新的promise对象触发了失败状态，它会把iterable里第一个触发失败的promise对象的错误信息作为它的失败错误信息。Promise.all方法常被用于处理多个promise对象的状态集合。
```js
function getRandom(min, max) {
    return Math.floor(Math.random() * (max - min) + min);
}
const proms = [];
for (let i = 0; i < 10; i++) {
    proms.push(new Promise((resolve, reject) => {
        setTimeout(() => {
            if (Math.random() < 0.5) {
                console.log(i, '完成');
                resolve(i);
            } else {
                console.log(i, '失败')
                reject(i);
            }
        }, getRandom(1000, 5000));
    }))
}
const pro = Promise.all(proms);
pro.then(datas => {
    console.log('有人完成了', datas);
})
pro.catch(datas => {
    console.log('有人失败了', datas);
})
```
- race(iterable)：当iterable参数里的任意一个子promise被成功或失败后，父promise马上也会用子promise的成功返回值或失败详情作为参数调用父promise绑定的相应句柄，并返回该promise对象

## 手写Promise

我们通过引入``MyPromise.js``来加载,通过``new MyPromise((reslove,reject)=>{})``调用,下面分以下几步实现最终Promise的效果.

1. 状态改变的实现
```js
const MyPromise = (() => {
    const MyPromiseStatus = Symbol("MyPromiseStatus");
    //当前Promise状态
    const MyPromiseValue = Symbol("MyPromiseValue");
    //当前Promise传递的后续值
    const changeStatus = Symbol("changeStatus");
    //改变状态函数
    const PENDING = "pending";
    //挂起状态
    const RESOLVED = "resolved";
    //reslved状态
    const REJECTED = "rejected";
    //REJECTED状态        
    return class MyPromise {
        /**
         * 构造函数
         * @param {*} 实例化MyPromise的时候立刻执行的函数 
         */
        [changeStatus](newstatus, data) {
            //状态不可逆 防止resolve之后在调用rejecte或reject之后在调用resolve
            if (this[MyPromiseStatus] !== PENDING) {
                return;
            }
            this[MyPromiseStatus] = newstatus;
            this[MyPromiseValue] = data;
        }
        constructor(handler) {
            if (typeof (handler) !== "function") {
                throw new Error("MyPromise params must be Function!");
            }
            this[MyPromiseStatus] = PENDING;
            this[MyPromiseValue] = undefined;
            let resolve = data => {
                this[changeStatus](RESOLVED, data);
            }
            let reject = err => {
                this[changeStatus](REJECTED, err);
            }
            handler(resolve, reject);
        }
    }
})();
```
2. 后续处理
```js
//后续处理
const MyPromise = (() => {
    //......
    //REJECTED状态
    const thenables = Symbol["thenables"];
    //resolved后续处理的队列
    const catchables = Symbol("catchables");
    //rejected后续处理的队列       
    return class MyPromise {
        /**
         * 构造函数
         * @param {*} 实例化MyPromise的时候立刻执行的函数 
         */
        [changeStatus](newstatus, data, queue) {
            //状态不可逆 防止resolve之后在调用rejecte或reject之后在调用resolve
            if (this[MyPromiseStatus] !== PENDING) {
                return;
            }
            this[MyPromiseStatus] = newstatus;
            this[MyPromiseValue] = data;
            queue.forEach(handler => handler(data))
        }
        constructor(handler) {
            if (typeof (handler) !== "function") {
                throw new Error("MyPromise params must be Function!");
            }
            this[MyPromiseStatus] = PENDING;
            this[MyPromiseValue] = undefined;
            this[thenables] = [];
            this[catchables] = [];
            let resolve = data => {
                this[changeStatus](RESOLVED, data, this[thenables]);
            }
            let reject = err => {
                this[changeStatus](REJECTED, err, this[catchables]);
            }
            handler(resolve, reject);
        }

        then(thenable, catchable) {
            //如果同步函数立即执行
            if (this[MyPromiseStatus] === RESOLVED) {
                //此处仿造Promise的进入为队列
                setTimeout(() => {
                    thenable(this[MyPromiseValue]);
                }, 0);
            } else {
                this[thenables].push(thenable);
            }
            this.catch(catchable);
        }

        catch (catchable) {
            if (typeof (catchable) !== "function") {
                return;
            }
            //如果同步函数立即执行
            if (this[MyPromiseStatus] === REJECTED) {
                //此处仿造Promise的进入为队列
                setTimeout(() => {
                    catchable(this[MyPromiseValue]);
                }, 0);
            } else {
                this[catchables].push(catchable);
            }
        }
    }
})();
```

3. 后续代码提取处理
```js
//...
const settleHandler = Symbol("settleHandler");
//后续处理函数提取
[settleHandler](handler, immediatelyStatus, queue) {
    if (typeof (handler) !== "function") {
        return;
    }
    if (this[MyPromiseStatus] === immediatelyStatus) {
        setTimeout(() => {
            handler(this[MyPromiseValue]);
        }, 0);
    } else {
        queue.push(handler);
    }
}
then(thenable, catchable) {
    this[settleHandler](thenable, RESOLVED, this[thenables]);
    this.catch(catchable);
}

catch (catchable) {
    this[settleHandler](catchable, REJECTED, this[catchables]);
}
```

4. Promise串联(链式编程)
```js
//...
const linkPromise = Symbol("linkPromise");
[linkPromise](thenable, catchable) {
    return new MyPromise((resolve, reject) => {
        this[settleHandler](data => {
            try {
                const result = thenable(data);
                resolve(result);
            } catch (err) {
                reject(err)
            }

        }, RESOLVED, this[thenables])

        this[settleHandler](err => {
            try {
                const result = catchable(err);
                resolve(result);
            }catch(err){
                reject(err);
            }

        }, REJECTED, this[catchables])
    })
}

then(thenable, catchable) {
    return this[linkPromise](thenable, catchable);
}

catch (catchable) {
    return this[linkPromise](undefined, catchable);
}
```

5. Promise串联优化和提取
```js
[linkPromise](thenable, catchable) {
    function exec(data, handler, resolve, reject) {
        try {
            const result = handler(data);
            if (result instanceof MyPromise) {
                result.then(d => {
                    resolve(d)
                }, err => {
                    reject(err);
                })
            } else {
                resolve(result);
            }
        } catch (err) {
            reject(err);
        }
    }
    return new MyPromise((resolve, reject) => {
        this[settleHandler](data => {
            exec(data, thenable, resolve, reject);

        }, RESOLVED, this[thenables])

        this[settleHandler](err => {
            exec(err, catchable, resolve, reject);

        }, REJECTED, this[catchables])
    })
}
```

# async 和 await

async 和 await 是 ES2016 新增两个关键字，它们借鉴了 ES2015 中生成器在实际开发中的应用，目的是简化 Promise api 的使用，并非是替代 Promise。

## async

目的是简化在函数的返回值中对Promise的创建

async 用于修饰函数（无论是函数字面量还是函数表达式），放置在函数最开始的位置，被修饰函数的返回结果一定是 Promise 对象。

```js

async function test(){
    console.log(1);
    return 2;
}

//等效于

function test(){
    return new Promise((resolve, reject)=>{
        console.log(1);
        resolve(2);
    })
}

```

## awaits

**await关键字必须出现在async函数中！！！！**

await用在某个表达式之前，如果表达式是一个Promise，则得到的是thenable中的状态数据。

```js

async function test1(){
    console.log(1);
    return 2;
}

async function test2(){
    const result = await test1();
    console.log(result);
}

test2();
```

等效于

```js

function test1(){
    return new Promise((resolve, reject)=>{
        console.log(1);
        resolve(2);
    })
}

function test2(){
    return new Promise((resolve, reject)=>{
        test1().then(data => {
            const result = data;
            console.log(result);
            resolve();
        })
    })
}

test2();

```



## 示例demo

1. 前面的获取老师信息改写
```js
async function getTeacher() {
    const stus = await ajax({
        url: "./data/students.json"
    })
    let cid;
    for (let i = 0; i < stus.length; i++) {
        if (stus[i].name === "李华") {
            cid = stus[i].classId;
        }
    }
    const cls = await ajax({
        url: "./data/classes.json"
    })
    let tid;
    for (let i = 0; i < cls.length; i++) {
        if (cls[i].id === cid) {
            tid = cls[i].teacherId;
        }
    }
    const ts = await ajax({
        url: "./data/teachers.json"
    })
    for (let i = 0; i < ts.length; i++) {
        const element = ts[i];
        if (element.id === tid) {
            console.log(element);
        }
    }
}
getTeacher();
```

# FetchApi

## Fetch Api 概述 

**XMLHttpRequest的问题**

1. 所有的功能全部集中在同一个对象上，容易书写出混乱不易维护的代码
2. 采用传统的事件驱动模式，无法适配新的 Promise Api

**Fetch Api 的特点**

1. 并非取代 AJAX，而是对 AJAX 传统 API 的改进
2. 精细的功能分割：头部信息、请求信息、响应信息等均分布到不同的对象，更利于处理各种复杂的 AJAX 场景
3. 使用 Promise Api，更利于异步代码的书写
4. Fetch Api 并非 ES6 的内容，属于 HTML5 新增的 Web Api
5. 需要掌握网络通信的知识

## 基本使用 

使用 ```fetch``` 函数即可立即向服务器发送网络请求

```js
async function getProvinces() {
    const url = 'xxxxx';
    const resp = await fetch(url);
    const result = await resp.json();
    console.log(result);
}
getProvinces();
```

### 参数

该函数有两个参数：

1. 必填，字符串，请求地址
2. 选填，对象，请求配置

**请求配置对象**

- method：字符串，请求方法，默认值GET
- headers：对象，请求头信息
- body: 请求体的内容，必须匹配请求头中的 Content-Type
- mode：字符串，请求模式
  - cors：默认值，配置为该值，会在请求头中加入 origin 和 referer
  - no-cors：配置为该值，不会在请求头中加入 origin 和 referer，跨域的时候可能会出现问题
  - same-origin：指示请求必须在同一个域中发生，如果请求其他域，则会报错
- credentials: 如何携带凭据（cookie）
  - omit：默认值，不携带cookie
  - same-origin：请求同源地址时携带cookie
  - include：请求任何地址都携带cookie
- cache：配置缓存模式
  - default: 表示fetch请求之前将检查下http的缓存.
  - no-store: 表示fetch请求将完全忽略http缓存的存在. 这意味着请求之前将不再检查下http的缓存, 拿到响应后, 它也不会更新http缓存.
  - no-cache: 如果存在缓存, 那么fetch将发送一个条件查询request和一个正常的request, 拿到响应后, 它会更新http缓存.
  - reload: 表示fetch请求之前将忽略http缓存的存在, 但是请求拿到响应后, 它将主动更新http缓存.
  - force-cache: 表示fetch请求不顾一切的依赖缓存, 即使缓存过期了, 它依然从缓存中读取. 除非没有任何缓存, 那么它将发送一个正常的request.
  - only-if-cached: 表示fetch请求不顾一切的依赖缓存, 即使缓存过期了, 它依然从缓存中读取. 如果没有缓存, 它将抛出网络错误(该设置只在mode为”same-origin”时有效).

### 返回值

fetch 函数返回一个 Promise 对象

- 当收到服务器的返回结果后，Promise 进入resolved状态，状态数据为 Response 对象
- 当网络发生错误（或其他导致无法完成交互的错误）时，Promise 进入 rejected 状态，状态数据为错误信息

**Response对象**

- ok：boolean，当响应消息码在200~299之间时为true，其他为false
- status：number，响应的状态码
- text()：用于处理文本格式的 Ajax 响应。它从响应中获取文本流，将其读完，然后返回一个被解决为 string 对象的 Promise。
- blob()：用于处理二进制文件格式（比如图片或者电子表格）的 Ajax 响应。它读取文件的原始数据，一旦读取完整个文件，就返回一个被解决为 blob 对象的 Promise。
- json()：用于处理 JSON 格式的 Ajax 的响应。它将 JSON 数据流转换为一个被解决为 JavaScript 对象的promise。
- redirect()：可以用于重定向到另一个 URL。它会创建一个新的 Promise，以解决来自重定向的 URL 的响应。

## Request对象

除了使用基本的fetch方法，还可以通过创建一个Request对象来完成请求（实际上，fetch的内部会帮你创建一个Request对象）

```js
new Request(url地址, 配置)
```

注意点：

尽量保证每次请求都是一个新的Request对象

```js
let req;
function GetRequestInfo(){
    if(!req){
        const url='xxxx';
        req = new Request(url,{});
    }
    return req.clone();
}    

async function GetProvinces(){
    const resp=await fetch(GetRequestInfo());
    const result = await resp.json();
    console.log(result);
}
GetProvinces();
```

## Response对象
```js
const resp = new Response(`[
    {"id":1, "name":"北京"},
    {"id":2, "name":"天津"}
]`, {
    ok: true,
    status: 200
})
var data = await resp.json();
console.log(data);
```

## Headers 对象

在Request和Response对象内部，会将传递的请求头对象，转换为Headers

Headers对象中的方法：

- has(key)：检查请求头中是否存在指定的key值
- get(key): 得到请求头中对应的key值
- set(key, value)：修改对应的键值对
- append(key, value)：添加对应的键值对
- keys(): 得到所有的请求头键的集合
- values(): 得到所有的请求头中的值的集合
- entries(): 得到所有请求头中的键值对的集合


```js
let req;
function getColumnHeaders(){
    return new Headers({
        a:1,
        b:2
    })
}

function getRequestInfo(){
    if(!req){
        const url = "http://101.132.72.36:5100/api/local";
        const headers = getColumnHeaders();
        req = new Request(url,{
            headers
        });

    }
    return req.clone();
}

async function getProvinces(){
    const resp = await fetch(getRequestInfo());
    const data = await resp.json();
    console.log(data);
}
getProvinces();
```

## 示例文件上传

流程：

1. 客户端将文件数据发送给服务器
2. 服务器保存上传的文件数据到服务器端
3. 服务器响应给客户端一个文件访问地址

请求方法：POST
请求的表单格式：multipart/form-data
请求体中必须包含一个键值对，键的名称是服务器要求的名称，值是文件数据

> HTML5中，JS仍然无法随意的获取文件数据，但是可以获取到input元素中，被用户选中的文件数据
> 可以利用HTML5提供的FormData构造函数来创建请求体

```js
async function upload() {
    const inp = document.getElementById("avatar");
    if (inp.files.length === 0) {
        alert("请选择要上传的文件");
        return;
    }

    const formData = new FormData();
    formData.append("imagefile", inp.files[0]);
    const url = "http://101.132.72.36:5100/api/upload";
    const resp = await fetch(url, {
        method: "post",
        body: formData
    });
    const result = await resp.json();
    return result;
}
document.querySelector("button").onclick = async function () {
    const result = await upload();
    const img = document.getElementById("imgAvatar")
    img.src = result.path;
}
```

# 迭代器和生成器

## 迭代器

1. 什么是迭代？

从一个数据集合中按照一定的顺序，不断取出数据的过程

2. 迭代和遍历的区别？

迭代强调的是依次取数据，并不保证取多少，也不保证把所有的数据取完

遍历强调的是要把整个数据依次全部取出

3. 迭代器

对迭代过程的封装，在不同的语言中有不同的表现形式，通常为对象

4. 迭代模式

一种设计模式，用于统一迭代过程，并规范了迭代器规格：

- 迭代器应该具有得到下一个数据的能力
- 迭代器应该具有判断是否还有后续数据的能力

## JS中的迭代器

JS规定，如果一个对象具有next方法，并且该方法返回一个对象，该对象的格式如下：
```js
{value: 值, done: 是否迭代完成}
```

则认为该对象是一个迭代器

含义：

- next方法：用于得到下一个数据
- 返回的对象
  - value：下一个数据的值
  - done：boolean，是否迭代完成

```js
//斐波拉且数列
function createFeiBoIterator() {
    let prev1 = 1,
        prev2 = 2,//当前位置的前1位和前2位
        n = 1;//当前是第几位
    return {
        next() {
            let value;
            if (n <= 2) {
                value = 1;
            } else {
                value = prev1 + prev2;
            }
            const result = {
                value,
                done: false
            };
            prev2 = prev1;
            prev1 = result.value;
            n++;
            return result;
        }
    }
}
const iterator = createFeiBoIterator();
```

## 可迭代协议与for-of循环

### 可迭代协议

**概念回顾**

- 迭代器(iterator)：一个具有next方法的对象，next方法返回下一个数据并且能指示是否迭代完成
- 迭代器创建函数（iterator creator）：一个返回迭代器的函数

**可迭代协议**

ES6规定，如果一个对象具有知名符号属性```Symbol.iterator```，并且属性值是一个迭代器创建函数，则该对象是可迭代的（iterable）

> 思考：如何知晓一个对象是否是可迭代的？
> 思考：如何遍历一个可迭代对象？

**数组和NodeList(dom对象集合)本身也是可迭代对象**

### for-of 循环

for-of 循环用于遍历可迭代对象，格式如下

```js
//迭代完成后循环结束
for(const item in iterable){
    //iterable：可迭代对象
    //item：每次迭代得到的数据
}
var obj = {
    a: 1,
    b: 2,
    [Symbol.iterator]() {
        const keys = Object.keys(this);
        let i = 0;
        return {
            next: () => {
                const propName = keys[i];
                const propValue = this[propName];
                const result = {
                    value: {
                        propName,
                        propValue
                    },
                    done: i >= keys.length
                }
                i++;
                return result;
            }
        }
    }
}
for (const item of obj) {
    console.log(item);
}
```

### 展开运算符与可迭代对象

展开运算符可以作用于可迭代对象，这样，就可以轻松的将可迭代对象转换为数组。

```js
const arr = [5, 7, 8, 5, 5];
const arr1 = [...arr];
 
function test(...p){
    console.log(p);
}
test(...arr)
```

## 生成器

1. 什么是生成器？

生成器是一个通过构造函数Generator(js内部引擎调用)创建的对象，生成器既是一个迭代器，同时又是一个可迭代对象

2. 如何创建生成器？

生成器的创建，必须使用生成器函数（Generator Function）

3. 如何书写一个生成器函数呢？

```js
//这是一个生成器函数，该函数一定返回一个生成器
function* method(){

}
```

4. 生成器函数内部是如何执行的？

生成器函数内部是为了给生成器的每次迭代提供的数据

每次调用生成器的next方法，将导致生成器函数运行到下一个yield关键字位置

yield是一个关键字，该关键字只能在生成器函数内部使用，表达“产生”一个迭代数据。

- 示例一,基本的生成器函数
```js
function *test(){
    console.log('第一次运行');
    yield 1;
    console.log('第二次运行');
    yield 2;
    console.log('第三次运行')
}    
const generator = test();

for(const item of generator){
    console.log(item);
}
```
- 示例二,数组生成器创建
```js

function *createIterator(arr){
    for(const item of arr){
        yield item;
    }
}
const arr1 = [1, 2, 3, 4, 5];
const iter1 = createIterator(arr1);
```
- 示例三,斐波拉且数列生成器创建
```js
function* createFeiboIterator() {
    let prev1 = 1,
        prev2 = 1,
        n = 1;
    while (true) {
        if (n <= 2) {
            yield 1;
        } else {
            const newValue = prev1 + prev2;
            yield newValue;
            prev2 = prev1;
            prev1 = newValue;
        }
        n++;
    }
}
const iterator = createFeiboIterator();
```

5. 有哪些需要注意的细节？
1). 生成器函数可以有返回值，返回值出现在第一次done为true时的value属性中
2). 调用生成器的next方法时，可以传递参数，传递的参数会交给yield表达式的返回值
3). 第一次调用next方法时，传参没有任何意义
4). 在生成器函数内部，可以调用其他生成器函数，但是要注意加上*号


6. 生成器的其他API

- return方法：调用该方法，可以提前结束生成器函数，从而提前让整个迭代过程结束
- throw方法：调用该方法，可以在生成器中产生一个错误

## 生成器应用-异步任务控制

在async(es7的东西)没出来之前,通过生成器到达异步的效果

```js
function* task() {
    const resp = yield fetch("http://101.132.72.36:5100/api/local")
    const result = yield resp.json();
    console.log(result);
}
run(task);
function run(generatorFunc) {
    const generator = generatorFunc();
    let result = generator.next();//开始迭代

    handlerResult();

    function handlerResult() {
        if (result.done) {
            return;
        }
        if (typeof (result.value.then) === 'function') {
            result.value.then(data => {
                result = generator.next(data);
                handlerResult();
            })
        }else{
            result = generator.next(result.value);
            handlerResult();
        }
    }
}
```

# 更多的集合类型

## set集合
> 一直以来，JS只能使用数组和对象来保存多个数据，缺乏像其他语言那样拥有丰富的集合类型。因此，ES6新增了两种集合类型（set 和 map），用于在不同的场景中发挥作用。

**set用于存放不重复的数据**
1. 如何创建set集合

```js
new Set(); //创建一个没有任何内容的set集合

new Set(iterable); //创建一个具有初始内容的set集合，内容来自于可迭代对象每一次迭代的结果

```

2. 如何对set集合进行后续操作

- add(数据): 添加一个数据到set集合末尾，如果数据已存在，则不进行任何操作
  - set使用Object.is的方式判断两个数据是否相同，但是，针对+0和-0，set认为是相等
- has(数据): 判断set中是否存在对应的数据
- delete(数据)：删除匹配的数据，返回是否删除成功
- clear()：清空整个set集合
- size: 获取set集合中的元素数量，只读属性，无法重新赋值

3. 如何与数组进行相互转换

```js
const s = new Set([x,x,x,x,x]);
// set本身也是一个可迭代对象，每次迭代的结果就是每一项的值
const arr = [...s];
```
4. 如何遍历

1). 使用for-of循环
2). 使用set中的实例方法forEach

注意：set集合中不存在下标，因此forEach中的回调的第二个参数和第一个参数是一致的，均表示set中的每一项

## set应用
```js
const arr1 = [33, 22, 55, 33, 11, 33, 5];
const arr2 = [22, 55, 77, 88, 88, 99, 99];

console.log('并集', [...new Set([...arr1, ...arr2])]);
console.log('交集', [...new Set(arr1)]).filter(item => arr2.indexOf(item) >= 0)
console.log("差集", [...new Set([...arr1, ...arr2])].filter(item => cross.indexOf(item) < 0))
```

## 手写set
```js
class MySet {
    constructor(iterator = []) {
        if (typeof (iterator[Symbol.iterator]) !== 'function') {
            throw new TypeError(`你提供的${iterator}不是一个可迭代的对象`);
        }
        this._datas = [];
        for (const item of iterator) {
            this.add(item);
        }

    }

    get size() {
        return this._datas.length;
    }



    add(data) {
        if (!this.has(data)) {
            this._datas.push(data);
        }
    }
    has(data) {
        for (const item of this._datas) {
            if (this.isEqual(data, item)) {
                return true;
            }
        }
    }
    delete(data) {
        for (let i = 0; i < this._datas.length; i++) {
            const element = this._datas[i];
            if (this.isEqual(element, data)) {
                this._datas.slice(i, 1);
                return true;
            }
        }
        return false;
    }
    clear() {
        this._datas.length = 0;
    }

    *[Symbol.iterator]() {
        for (const item of this._datas) {
            yield item;
        }
    }
    forEach(callback) {
        for (const item of this._datas) {
            callback(item, item, this);
        }
    }
    isEqual(data1, data2) {
        if (data1 == 0 && data2 == 0) {
            return true;
        }
        return Object.is(data1, data2);
    }
}
```

## map集合
键值对（key value pair）数据集合的特点：键不可重复
map集合专门用于存储多个键值对数据。

在map出现之前，我们使用的是对象的方式来存储键值对，键是属性名，值是属性值。

使用对象存储有以下问题：

1. 键名只能是字符串
2. 获取数据的数量不方便
3. 键名容易跟原型上的名称冲突

1. 如何创建map

```js
new Map(); //创建一个空的map
new Map(iterable); //创建一个具有初始内容的map，初始内容来自于可迭代对象每一次迭代的结果，但是，它要求每一次迭代的结果必须是一个长度为2的数组，数组第一项表示键，数组的第二项表示值
```

2. 如何进行后续操作

- size：只读属性，获取当前map中键的数量
- set(键, 值)：设置一个键值对，键和值可以是任何类型
  - 如果键不存在，则添加一项
  - 如果键已存在，则修改它的值
  - 比较键的方式和set相同
- get(键): 根据一个键得到对应的值
- has(键)：判断某个键是否存在
- delete(键)：删除指定的键
- clear(): 清空map

3. 和数组互相转换
```js
const mp = new Map([["a", 3], ["b", 4], ["c", 5]]);
const result = [...mp];
console.log(result);
```
4. 遍历

- for-of，每次迭代得到的是一个长度为2的数组
- forEach，通过回调函数遍历
  - 参数1：每一项的值
  - 参数2：每一项的键
  - 参数3：map本身


## 手写map
```js
class MyMap {
    constructor(iterable = []) {
        //验证是否是可迭代的对象
        if (typeof iterable[Symbol.iterator] !== "function") {
            throw new TypeError(`你提供的${iterable}不是一个可迭代的对象`)
        }
        this._datas = [];
        for (const item of iterable) {
            // item 也得是一个可迭代对象
            if (typeof item[Symbol.iterator] !== "function") {
                throw new TypeError(`你提供的${item}不是一个可迭代的对象`);
            }
            const iterator = item[Symbol.iterator]();
            const key = iterator.next().value;
            const value = iterator.next().value;
            this.set(key, value);
        }
    }

    set(key, value) {
        const obj = this._getObj(key);
        if (obj) {
            obj.value = value;
        } else {
            this._datas.push({
                key,
                value
            })
        }
    }
    get(key) {
        const item = this._getObj(key);
        if (item) {
            return item.value;
        }
        return undefined;
    }

    get size() {
        return this._datas.length;
    }

    delete(key) {
        for (let i = 0; i < this._datas.length; i++) {
            const element = this._datas[i];
            if (this.isEqual(element.key, key)) {
                this._datas.splice(i, 1);
                return true;
            }
        }
        return false;
    }
    clear() {
        this._datas.length = 0;
    }
    has(key) {
        return this._getObj(key) !== undefined;
    }
    _getObj(key) {
        for (const item of this._datas) {
            if (this.isEqual(item.key, key)) {
                return item;
            }
        }
    }
    isEqual(data1, data2) {
        if (data1 === 0 && data2 === 0) {
            return true;
        }
        return Object.is(data1, data2);
    }

    *[Symbol.iterator]() {
        for (const item of this._datas) {
            yield [item, key, item, value];
        }
    }
    forEach(callback) {
        for (const item of this._datas) {
            callback(item.value, item.key, this);
        }
    }
}
```

## WeakSet和WeakMap

### WeakSet

使用该集合，可以实现和set一样的功能，不同的是：

1. **它内部存储的对象地址不会影响垃圾回收**
2. 只能添加对象
3. 不能遍历（不是可迭代的对象）、没有size属性、没有forEach方法

```js
let obj = {
    name: "yj",
    age: 18
};
let obj2 = obj;
const set = new WeakSet();
set.add(obj);

obj = null;
obj2 = null;
console.log(set)
```

### WeakMap

类似于map的集合，不同的是：

1. **它的键存储的地址不会影响垃圾回收**
2. 它的键只能是对象
3. 不能遍历（不是可迭代的对象）、没有size属性、没有forEach方法

```js
const wmap = new WeakMap();
let lis = document.querySelectorAll("li");
for (const li of lis) {
    wmap.set(li, {
        id: li.innerText,
        name: `姓名${li.innerHTML}`
    })
}
lis[0].remove();
lis = null;
console.log(wmap);
```

# 代理与反射

## 回顾属性描述符

Property Descriptor 属性描述符  是一个普通对象，用于描述一个属性的相关信息

通过```Object.getOwnPropertyDescriptor(对象, 属性名)```可以得到一个对象的某个属性的属性描述符

- value：属性值
- configurable：该属性的描述符是否可以修改
- enumerable：该属性是否可以被枚举
- writable：该属性是否可以被重新赋值

> ```Object.getOwnPropertyDescriptors(对象)```可以得到某个对象的所有属性描述符

如果需要为某个对象添加属性时 或 修改属性时， 配置其属性描述符，可以使用下面的代码:

```js
Object.defineProperty(对象, 属性名, 描述符);
Object.defineProperties(对象, 多个属性的描述符)
```

### 存取器属性

属性描述符中，如果配置了 get 和 set 中的任何一个，则该属性，不再是一个普通属性，而变成了存取器属性。

get 和 set配置均为函数，如果一个属性是存取器属性，则读取该属性时，会运行get方法，将get方法得到的返回值作为属性值；如果给该属性赋值，则会运行set方法。

存取器属性最大的意义，在于可以控制属性的读取和赋值。

## Reflect

1. Reflect是什么？

Reflect是一个内置的JS对象，它提供了一系列方法，可以让开发者通过调用这些方法，访问一些JS底层功能

由于它类似于其他语言的**反射**，因此取名为Reflect

2. 它可以做什么？

使用Reflect可以实现诸如 属性的赋值与取值、调用普通函数、调用构造函数、判断属性是否存在与对象中  等等功能

3. 这些功能不是已经存在了吗？为什么还需要用Reflect实现一次？

有一个重要的理念，在ES5就被提出：减少魔法、让代码更加纯粹

这种理念很大程度上是受到函数式编程的影响

ES6进一步贯彻了这种理念，它认为，对属性内存的控制、原型链的修改、函数的调用等等，这些都属于底层实现，属于一种魔法，因此，需要将它们提取出来，形成一个正常的API，并高度聚合到某个对象中，于是，就造就了Reflect对象

因此，你可以看到Reflect对象中有很多的API都可以使用过去的某种语法或其他API实现。

4. 它里面到底提供了哪些API呢？

- Reflect.set(target, propertyKey, value): 设置对象target的属性propertyKey的值为value，等同于给对象的属性赋值
- Reflect.get(target, propertyKey): 读取对象target的属性propertyKey，等同于读取对象的属性值
- Reflect.apply(target, thisArgument, argumentsList)：调用一个指定的函数，并绑定this和参数列表。等同于函数调用
- Reflect.deleteProperty(target, propertyKey)：删除一个对象的属性
- Reflect.defineProperty(target, propertyKey, attributes)：类似于Object.defineProperty，不同的是如果配置出现问题，返回false而不是报错
- Reflect.construct(target, argumentsList)：用构造函数的方式创建一个对象
- Reflect.has(target, propertyKey): 判断一个对象是否拥有一个属性
- 其他API：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect

## Proxy 代理

代理：提供了修改底层实现的方式

```js
const obj = {
    a: 1,
    b: 2
}

const proxy = new Proxy(obj, {
    set(target, propertyKey, value) {
        // console.log(target, propertyKey, value);
        // target[propertyKey] = value;
        Reflect.set(target, propertyKey, value);
    },
    get(target, propertyKey) {
        if (Reflect.has(target, propertyKey)) {
            return Reflect.get(target, propertyKey);
        } else {
            return -1;
        }
    },
    has(target, propertyKey) {
        return false;
    }
});
// console.log(proxy);
// proxy.a = 10;
// console.log(proxy.a);

console.log(proxy.d);
console.log("a" in proxy);
```

## 应用-观察者模式
有一个对象，是观察者，它用于观察另外一个对象的属性值变化，当属性值变化后会收到一个通知，可能会做一些事。
## 应用-偷懒的构造函数
## 应用-可验证的函数参数

# 增强的数组功能

## 静态方法

- Array.of(...args): 使用指定的数组项创建一个新数组
- Array.from(arg): 通过给定的类数组 或 可迭代对象 创建一个新的数组。

## 实例方法

- find(callback): 用于查找满足条件的第一个元素
- findIndex(callback)：用于查找满足条件的第一个元素的下标
- fill(data)：用指定的数据填充满数组所有的内容
- copyWithin(target, start?, end?): 在数组内部完成复制
- includes(data)：判断数组中是否包含某个值，使用Object.is匹配



## [扩展]类型化数组

### 数字存储的前置知识

1. 计算机必须使用固定的位数来存储数字，无论存储的数字是大是小，在内存中占用的空间是固定的。

2. n位的无符号整数能表示的数字是2^n个，取值范围是：0 ~ 2^n - 1

3. n位的有符号整数能表示的数字是2^n个，取值范围是：-2^(n-1) ~ 2^(n-1) - 1

4. 浮点数表示法可以用于表示整数和小数，目前分为两种标准：
   1. 32位浮点数：又称为单精度浮点数，它用1位表示符号，8位表示阶码，23位表示尾数
   2. 64位浮点数：又称为双精度浮点数，它用1位表示符号，11位表示阶码，52位表示尾数

5. JS中的所有数字，均使用双精度浮点数保存

### 类型化数组

类型化数组：用于优化多个数字的存储

具体分为：

- Int8Array： 8位有符号整数（-128 ~ 127）
- Uint8Array： 8位无符号整数（0 ~ 255）
- Int16Array: ...
- Uint16Array: ...
- Int32Array: ...
- Uint32Array: ...
- Float32Array:
- Float64Array

1. 如何创建数组

```js

new 数组构造函数(长度)

数组构造函数.of(元素...)

数组构造函数.from(可迭代对象)

new 数组构造函数(其他类型化数组)

```


2. 得到长度

```js
数组.length   //得到元素数量
数组.byteLength //得到占用的字节数
```

3. 其他的用法跟普通数组一致，但是：

- 不能增加和删除数据，类型化数组的长度固定
- 一些返回数组的方法，返回的数组是同类型化的新数组


## ArrayBuffer

ArrayBuffer：一个对象，用于存储一块固定内存大小的数据。

```js

new ArrayBuffer(字节数)

```

可以通过属性```byteLength```得到字节数，可以通过方法```slice```得到新的ArrayBuffer

### 读写ArrayBuffer

1. 使用DataView

通常会在需要混用多种存储格式时使用DataView

2. 使用类型化数组

实际上，每一个类型化数组都对应一个ArrayBuffer，如果没有手动指定ArrayBuffer，类型化数组创建时，会新建一个ArrayBuffer

## 制作黑白图片