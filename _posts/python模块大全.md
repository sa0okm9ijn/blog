---
title: python模块大全
date: 2019-07-25 10:35:54
tags: 
- python
categories: python
description: python内置模块以及第三方模块用法，持续更新。。。
---

## 模块通用
1、这模块有哪些函数可用（可以通过dir()函数查询）
2、有哪些属性和方法可用(网上查看文档)
3、使用格式是什么(网上查看文档)

```
import time
print(dir(time))
```

## time模块
该模块提供了各种时间相关的函数,可以通过索引和属性名访问值

* **time.struct_time类**

| 索引  | 属性  | 值  |
|---    |---   | --- |
| 0 | tm_year | 如:1993 |
| 1 | tm_mon | [1,12] |
| 2 | tm_mday | [1,31]] |
| 3 | tm_hour | [0,23]] |
| 4 | tm_min | [0,59]] |
| 5 | tm_sec | [0,61]] |
| 6 | tm_wday | [0,6] 周一为0 |
| 7 | tm_yday | [1,366] |
| 8 | tm_isdst | 0,1,-1 |

61是闰秒，具体百度我也没搞懂
索引为8的暂时不考虑吧

* **time.time()**

返回浮点数的秒数(自epoch以来的秒数)，epoch和平台有关，比如window平台，epoch是1970年1月1日00:00:00
```
print(time.time())  
#1564030999.4895782   返回从1970年到现在的秒数
```

* **time.gmttime(secs)**

返回将secs转化为UTC时区的struct_time类,如果未提供 secs 或为 None ，则使用由 time() 返回的当前时间

```
print(time.gmtime()) 
# 返回UTC时区时间 time.struct_time(tm_year=2019, tm_mon=7, tm_mday=25, tm_hour=5, tm_min=5, tm_sec=43, tm_wday=3, tm_yday=206, tm_isdst=0)
```

* **time.strftime(format,t)**

t为一个元组或为structime类型，根据t返回format指定格式的时间字符串，如果未提供t，则使用由localtime()返回的当前时间

```
print(time.strftime('%y-%m-%d %H:%M:%S'))
# 返回当地时间19-07-25 13:13:52 指定格式
```

常用format指令，以下为了方便把类似指令放在一行，实际在使用中是一个一个用的

| 指令   |  意义 |   字符串   |
|---|--- |---    |
| %a/%A  |  返回当地星期几的英文返回    |   如星期四:Thu/Thursday   | 
| %b/%B  |  返回当地月份的英文返回    |   如4月:Jul/July   | 
| %c  |  本地化的日期和时间显示    |   如:Thu Jul 25 13:23:56 2019   | 
| %d  |  当月第几天    |   如:25    |
| %H  |  返回当前小时(24小时制)    |   如:13    |
| %I  |  返回当前小时(12小时制)   |   如:01    |
| %j  |  当年第几天   |   如:206    |
| %m/%M  |  返回月份/分钟   |   如:07/29    |
| %p  |  返回PM或AM   |   如:PM    |
| %S  |  返回秒   |   如:34    |
| %x-%X  |  本地化的适当日期表示/本地化的适当时间表示   |   如:07/25/19-13:33:39    |
| %y/%Y  |  不带世纪年/带世纪年   |   如:19/2019    |
| %U  |  表示的一年中的周数（星期日作为一周的第一天）作为。在第一个星期日之前的新年中的所有日子都被认为是在第0周。   |   如:29    |
| %w  |  十进制数 [0(星期日),6] 表示的周中日   |   如:4    |
| %W  |  表示的一年中的周数（星期一作为一周的第一天）作为。在第一个星期一之前的新年中的所有日子被认为是在第0周。   |   如:29    |

* **time.localtime(secs)**

与 gmtime() 相似但转换为当地时间。如果未提供 secs 或为 None ，则使用由 time() 返回的当前时间,返回类型为structtime

```
print(time.localtime()) 
#返回去当地时间 time.struct_time(tm_year=2019, tm_mon=7, tm_mday=25, tm_hour=13, tm_min=5, tm_sec=43, tm_wday=3, tm_yday=206, tm_isdst=0)
```

## os模块

该模块提供了一些方便使用操作系统相关功能的函数

* **os.getcwd()**   

返回当前工作目录
```
print(os.getcwd()) #返回当前工作目录
```

* **os.listdir(path)**   

返回path指定的文件夹包含的文件或文件夹的名字的列表
```
print(os.listdir(path)) #返回path指定的文件夹包含的文件或文件夹的名字的列表
```

* **os.mkdir(path)** 

创建文件夹
```
os.mkdir(path)  # 创建文件夹
```

* **os.path.abspath(path)**

返回绝对路径
```
print(os.path.abspath(path)) # 返回绝对路径
```

* **os.path.basename(path)** 

返回文件名
```
print(os.path.basename(filepath) # 返回文件名带后缀
```

* **os.path.isfile(path)** 

判断路径是否为文件
```
os.path.isfile(path)   # 判断路径是否为文件
```

* **os.path.isdir(path)**

判断路径是否为目录
```
os.path.isdir(path)   # 判断路径是否为目录
```



