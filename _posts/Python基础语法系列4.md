---
title: Python基础语法系列4
date: 2019-06-30 11:33:53
tags: 
- python  
categories: python  
description: 
---


## 知识一:布尔值

1. 用数据逻辑做判断的过程叫【布尔运算】
2.【布尔运算】会产生【布尔值】
3. 布尔值分为True和False
4. True和False就像开关一样，决定if语句和while循环语句是否运行。

## 知识二:布尔运算

### 比较运算符
![](a.png)


###真假判断

None，它代表的是【空值】，自成一派，数据类型是NoneType。要注意它和0的区别，0是整数0，可并非什么都没有。

![](b.png)

```
print('以下数据判断结果都是【假】：')
print(bool(False))
print(bool(0))
print(bool(''))
print(bool(None))


print('以下数据判断结果都是【真】：')
print(bool(True))
print(bool(1))
pprint(bool('abc'))

```

### 五种运算：and、or、not、in、not in

* 布尔值的运算_and运算

![](c.png)

* 布尔值的运算_or运算

![](d.png)

* 布尔值的运算_not

```
a =True
print(not a) #判断为假
```

* 布尔值的运算_in、not in

a.【in】的意思是“判断一个元素是否在一堆数据之中”，【not in】反之；
b. 如果涉及到的数据集合是字典的话，【in】和【not in】就可以用来判断字典中是否存在某个【键】


## 知识三:break语句

break的意思是“打破”，是用来结束循环的，一般写作if...break；

## 知识四:continue语句

continue的意思是“继续”。这个子句也是在循环内部使用的。当某个条件被满足的时候，触发continue语句，将跳过之后的代码，直接回到循环的开始；

## 知识五:pass语句

常用在if语句下，表示跳过，如果没有pass来占据一个位置表示“什么都不做”

## 知识六:else语句

else不但可以和if配合使用，它还能跟for循环和while循环配合使用，如果正常结束循环（没有遇到break）就执行else语句

```
for i in range(5):
    a = int(input('请输入0结束循环，你有5次机会:'))
    if a == 0:
        print('你触发了break语句，导致else语句不会生效。')    
        break
else:
    print('5次循环你都错过了，else语句生效了。')
```

