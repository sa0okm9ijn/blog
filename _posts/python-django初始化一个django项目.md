---
title: Python 初始化一个django项目
date: 2019-05-29 13:22:16
tags: 
- Python django 
categories: Python 
description: 
---
## 首先我们需要安装django

    
```  
pip3 install django
```
django 会安装在python安装目录下面的Scripts目录下面，在这里我们需要设置该目录为环境变量

## 初始化django项目

我们建立一个FirstDjango，初始化一个mysite的django项目


```
django-admin startproject mysite
```
![](584421-20190403164203454-684629174.png)

此时在我们的FirstDjango目录下面会生成这么一个目录

## 初始化app

我们可以为我们的项目添加多个app，比如博客、论坛、商城、后台等

初始化一个app

![](584421-20190403164551144-877485596.png)

需要先进入有manage.py的目录，然后执行以上命令，生成如下目录

![](584421-20190403164653367-1397180343.png)

此时我们的一个django项目就算初始完成了，然后可以定义我们的路由。以及model的逻辑

## 启动django项目

    
```
python manage.py runserver 8080
```
浏览器访问127.0.0.1：8080![](584421-20190403165734608-1538962570.png)




