---
title: Mysql数据库笔记记录
date: 2019-05-29 13:10:35
tags: 
- Mysql 
categories: Mysql 
description: 
---
主键索引

一张表只能有一个主键,唯一不能重复，不能为NULL,一般情况下，自增列设置为主键  可以为多列组成主键

唯一索引

可用为 NULL,一张表可以有多个唯一列

作用：约束和索引，加速查找



清空表内容
```
delete from table
```

清空表内容，速度快，自增回到圆雕  
```
truncate table tb1  
```


定长 (查询性能好,浪费空间) 最大255

char

char(7)     ssss开辟7的空间

变长(查找速度慢，节省空间)

varchar  最大255

varchar(7)

ssss开辟4的空间 最大7



union处理重合

union all不处理重合
