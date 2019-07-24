---
title: Python基础语法系列2
date: 2019-06-30 11:33:53
tags: 
- python  
categories: python  
description: 
---


什么时候需要用到列表和字典？
>需要将数据收纳起来的时候。

什么时候用到列表，什么时候用字典？
>当数据需要 依次放好 的时候用到列表，就像把一堆东西堆起来的手拿方式。
>当数据需要 打上标签 放好的时候用字典，就像图书馆的书架用标签分类。

列表和字典的常见用法？
>用于 存数据 和 取数据，可以相互嵌套。
>用于 for循环 ，依次遍历列表或字典。

## 知识一:列表
一个列表需要用中括号[ ]把里面的各种数据框起来，里面的每一个数据叫作“元素”。每个元素之间都要用英文逗号隔开。
### 定义一个列表

```
list = [1,2,3,4,5,6,7,8]
list = ['风','变','编','程']
```

### 打印列表

```
print( list ) #打印列表list
print( len ( list ) ) #打印列表list的长度
print( type ( list ) ) #打印列表list的类型
```

### 列表_提取单个元素

```
print( list[0:4] )  #打印列表list的第0、1、2、3个元素
print( list[1:3] )  #打印列表list的第1、2、个元素
print( list[1:] )  #打印列表list的第1个元素起的所有元素
print( list[:2] )  #打印列表list的第2个元素之前对的所有元素
```

### 列表添加

```
list.append('赞') #把元素‘赞’放进列表list的尾部
```

### 列表删除

```
del list[4] #删除列表list的第5个元素
```


### 列表_合并

```
list1.append(list3) #把list3当成元素添加到list1尾部
list2.extend(list3) #把list3元素添加到list2中
```


### 列表_extend的用法

```
num2.extend(['ABCDE'])
num2.extend('ABCDE')  # extend后面是列表的话会将其合并，后面是字符串的话会将每个字符当成一个列表中的元素。
print(num2)

运行结果>>>
[ 'ABCDE', 'A', 'B', 'C', 'D', 'E']
```


### 列表去重

补充知识：集合（set）是一个无序的不重复元素序列，set()可以去重，然后生成一个集合。

```
list1 = [1,2,3]
list2 = [1,1,2]
print(set(list1))
print(set(list2))  # 去重，删去了重复的“1”。
```

### 列表生成式

```
list1 = [i for i in range(3)]  # 规定列表中元素的范围
print(list1)

list2 = [m+n for m in ['天字', '地字'] for n in '一二']  # 列表元素可以是组合，分别规定范围。
print(list2)

list3 = [n*n for n in range(1,11) if n % 3 == 0]  # 元素既可规定范围，也可附加条件。
print(list3)

运行结果>>>
[0, 1, 2]
['天字一', '天字二', '地字一', '地字二']
[9, 36, 81]
```

普通方法生成上面列表

```
list1 = []
for i in range(3):
    list1.append(i)
print(list1)

list2 = []
for m in ['天字', '地字']:
    for n in '一二':
        list2.append(m+n)
print(list2)

list3 = []
for i in range(1,11):
    if i % 3 == 0:
        list3.append(i*i)
print(list3)
```


## 知识二:字典

* 列表中的元素是自成一体的，而字典的元素是由一个个键值对构成的，用英文冒号连接；
* 唯一的键和对应的值形成的组合，我们就叫做【键值对】；

### 字典_定义


```
scores = {'小明':95,'小红':90,'小刚':90}
```

### 字典_打印某个值

```
scores = {'小明': 95, '小红': 90, '小刚': 90}
print(scores['小明'])
```


### 字典_添加

```
scores['小美'] = 85
```


### 字典_删除

```

del scores['小刚']
```

### 字典_遍历

```
dict.items()
```


### 遍历字典的键值对

```
for k,v in DictName.items():
#k对应键，v对应值，k,v 的名字可以自己取，DictName是字典名
```

### 字典_直接遍历字典所有的值

```
for value in DictName.values(): print(value)  # value的名字可以自行另取 # DictName是要遍历的字典的名称 # .values():是固定的用法
```



