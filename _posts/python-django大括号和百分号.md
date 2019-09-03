---
title: python 大括号和百分号
date: 2019-05-29 13:25:32
tags: 
- Python django 
categories: Python 
description: 
---

## 报csrf的错误解决方式
```

{% csrf_token%}  可防御跨站攻击 卸载html页面
```

## 禁止渲染

```
{% verbatim %}

{% endverbatim %}
```

## 自定义标签

在项目目录添加templatetags目录，并且添加对应的python文件,，此目录名字不可修改

![](584421-20190402223525237-1648810414.png)

添加自定义标签

    
```
from django import template
from django.utils.safestring import mark_safe

register = template.Library()  #register 固定变量名，不能改变

@register.simple_tag
def my_add100(v1):
    return v1+100
```
 不能用作if语句

 在index.html如下所用

```

{% load myTags %}

<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>

</head>

<body>
    {% my_add100 4 %}

</body>

</html>
```


##  自定义过滤器

如自定义标签，需要把simple_tag换成simple'

![](584421-20190402224255088-1598908357.png)

对应的htme如下

![](584421-20190402224317829-459591958.png)

参数不可以超过2个，第二个参数通过：值传递

