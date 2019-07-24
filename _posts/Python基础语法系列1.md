---
title: Python基础语法系列1
date: 2019-06-30 11:33:53
tags: 
- python  
categories: python  
description: 
---

## 知识一:print()函数、算数运算符

学编程第一步干嘛，当然是问一句"世界,你好"咯

### print('')/print("")直接打印内容
```
print('hello,world')
运行结果 > hello,world
```

### pint()让计算机读懂括号里面的内容,打印最终内容

```
print(2+1) #加法
运行结果> 3

print(2-1) #减法
运行结果> 1

print(2*1) #乘法
运行结果> 2

print(2/1) #除法
运行结果> 2

print(2**3) #次方
运行结果> 8

print(10%3) #取余
运行结果> 1

print(10//3) #取整
运行结果> 3

```








### print()函数输出不换行
```
print('hello',end='')
print('world')
运行结果 > helloworld


print('hello',end='  ')
print('world')

运行结果 > hello world


print('hello',end='!')
print('world')

运行结果 > hello!world
```

### print()函数输出换行

```
print('') #相当于回车

print('''
123
456
789       '''') #内部自动换行

```

### 算数运算符

![](image.png__thumbnail)



## 知识二:转义字符
在编程语言中，我们用转义字符表示不能直接显示的字符，比如换行键、后退键，回车键等。

![](SdWvvy1GOYIF3aQz.png)


## 知识三:变量和赋值
* 只能是一个词
* 只能包含字母、数字、下划线
* 不能以数字开头
* 尽量描述包含的内容

name = '小千'

## 知识四:数据类型
最常用的数据类型有三种——字符串(str)、整数(int)和浮点数(float)

### 字符串
只要是被【单/双/三引号】这层皮括起来的内容，不论那个内容是中文、英文、数字甚至火星文。只要是被括起来的，就表示是字符串类型。

```
slogan = '命运！不配做我的对手！'
attack = "308"
achieve = "First Blood!"
```

### 整数
是正整数、负整数和零的统称，是没有小数点的数字

```
number1 = 1
number2 = -1
number3 = 0
```

### 浮点数
带小数点的数字，就是浮点数

```
number = 0.33
```

## 知识五:type()查看数据类型

python中数字不能直接和字符串拼接，必须先转换字符串类型在拼接

```
gain = '获得'
number = 5
print(type(gain))
print(type(number))

运行结果>>>
<class 'str'>
<class 'int'>
```

## 知识六:数据转换

* str()函数
* int()函数
对于浮点数，int()函数会做取整处理。但是，同我们平时对小数四舍五入的处理方法不同，int()函数会直接抹零，直接输出整数部分
* float()函数

## 知识七:条件判断

python中用缩进来包含一段内容。如其他语言中的{}

### 单向判断

```
if xxxx:
    print(xxxx)
```

### 双向判断

```
if xxxx: 
    print(xxxx) 
else:
    print(xxxx)
```

### 多行判断

```
if xxxx: 
    print(xxxx) 
elif:
    print(xxxx)
else:
    print(xxxx)
```

## 知识八:if嵌套
![](a.png)

## 知识九:input()函数

* 收集信息

用来收集信息，并且一定要在终端处输入数据。input()函数的输入值（搜集到的回答），永远会被强制性地转换为字符串类型。

* input()_赋值

```
name = input('内容')
```

* input()_数据类型转换

```
choice = int(input('请输入您的选择：'))
```

## 补充知识:格式化字符串

* {}

```
print('{}--{}'.format(1,2))
```

* %

如图

![](b.png)







