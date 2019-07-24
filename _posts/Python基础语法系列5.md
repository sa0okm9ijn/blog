---
title: Python基础语法系列5
date: 2019-07-15 16:40:14
tags: 
- python  
categories: python  
description: 
---


## 知识一:函数
函数是组织好的、可以重复使用的、用来实现单一功能的代码
### 定义函数
```
def 函数名(参数):
    函数体
    return 语句
```
### 参数类型
#### 位置参数

```
def menu(appetizer,course):
    pass
```
#### 默认参数
默认参数必须放在位置参数之后
```
def menu(appetizer,course,dessert='绿豆沙'):
    pass
```
#### 不定长参数
不定长参数以星号，为元组(tuple)类型,元组是可迭代对象，这意味着我们可以用for循环来遍历它
```
def menu(*barbeque):
    return barbeque
```


### 返回值
函数，不仅可以支持输入多个参数，而且也可以同时输出多个值

返回值同样为元组类型
```
def coupon():
    return 'test1','test2'
```

### 函数作用域
1、一个在函数内部赋值的变量仅能在该函数内部使用（局部作用域），它们被称作【局部变量】
2、在所有函数之外赋值的变量，可以在程序的任何位置使用（全局作用域），它们被称作【全局变量】
3、global语句一般写在函数体的第一行，它会告诉Python,把该变量声明全局变量


## 知识二:面向对象编程

### 类的创建

```
class Computer:
    pass
```

### 类的实例化(对象)

```
my_computer = Computer()#实例化
```

### 初始化函数(构造函数)

```
class chinese:
    def __init__(self, name, birth, region)
        self.name = name   # self.name = '吴枫' 
        self.birth = birth  # self.birth = '广东'
        self.region = region  # self.region = '深圳'
```

### 继承

#### 多层继承

```
class B(A):
class C(B):
```
多层继承（纵向）时，子类创建的实例可调用所有层级父类的属性和方法。
### 多重继承

```
class A(B,C,D):
```

多重继承（横向）时，根据与子类的相关顺序从左往右排，A是B,C,D三个父类的子类，但是在调用类方法和类属性时，优先从B中找，找不到再去C（就近原则）。