---
title: Python基础语法系列3
date: 2019-06-30 11:33:53
tags: 
- python  
categories: python  
description: 
---



## for...in..循环

循环的这个过程，在Python中的学名叫做【遍历】，以下列举了遍历的三种数据类型

* 列表遍历

```
for i in [1,2,3,4,5]:  #列表
    print(i)


运行结果>>>
1
2
3
4
5
```

* 字典遍历

```
dict = {'日本':'东京','英国':'伦敦','法国':'巴黎'}  #字典，i会遍历字典中的每一个【键】
for i in dict:
    print(i)

 运行结果>>>
日本
英国
法国
```

* 字符串遍历

```
for i in '风变编程':#字符串
    print(i)

运行结果>>>
风
变
编
程
```

* range(x)函数遍历

```
for i in range(3):
    print(i)

运行结果>>>
0
1
2
```

## 知识二:while循环

while循环有2个要点：1）放行条件；2）办事流程。当条件被满足时，就会循环执行while内部的代码（while子句）。

```
a = 0
while a < 5:
    a = a + 1
    print(a)
运行结果>
1
2
3
4
5
```


## 知识三:两种循环的对比

### 什么时候用for循环，什么时候用while循环？

* 知道循环次数的时候优先用for循环；

* 不知道循环次数的时候用while；

* 把一件事重复N遍，两种循环方式都可以用

```
# 乘法表
for i in range(1,10):
    for j in range(1,i+1):
        print( '%d X %d = %d' % (j,i,i*j),end = ' ' )
    print(' ')
```
