---
title: pythonWeb框架Django基础
date: 2019-11-29 17:23:04
tags: 
- Python django 
categories: Python 
description: 此篇文章是针对有python基础的伙伴们学习django框架,一起进步
---

# 安装python

选择适合自己的版本进行下载,https://www.python.org/downloads/,我这里用的是3.7.4版本

安装完后检测 Python 是否可以正常运行。在命令行输入 ``python -V``(注意这里的V是大写) ，如果输出了 Python 的版本号，说明 Python 已安装成功。


# 使用虚拟环境

虚拟环境是一种 Python 工具，使用它可以创建一个独立的 Python 环境

虚拟环境帮我们从系统的 Python 环境中克隆一个全新的 Python 环境出来，这个环境独立于原来的 Python 环境。我们可以在这个新克隆的环境下安装 django 2.2.x，并且在这个新环境下运行我们的新项目。

我这里使用的是Pipenv使用和管理虚拟环境

## Pipenv 创建和管理虚拟环境

1. ``pip install pipenv``

安装虚拟环境模块pipenv

2. ``pipenv install``

给自己的项目创建虚拟环境

创建项目根目录``C:\WorkSpace\VsCode\Python-Django\demo1``,在根目录下执行命令``pipenv install``,Pipenv 将会为我们做好一切工作,并且会在项目根目录下生成 Pipfile 和 Pipfile.lock 用于管理项目依赖,同时会在默认的路径``C:\Users\Administrator\.virtualenvs``创建程序执行的虚拟环境,此处的目录具体根据项目名称来定,如我的程序执行的虚拟环境目录 ``demo1-_E9ELm2A``

3. ``pipenv --rm``

删除创建的虚拟环境

4. ``pipenv run ``

执行指令的python命令

如``pipenv run python``进入python解释器交互界面

5. ``pipenv install``

安装python模块

如安装django``pipenv install django``

# 建立django工程

在我们进行下面环节时,确保用虚拟环境安装了django模块

## Hello Django

在项目的根目录下执行命令``pipenv run django-admin startproject blogproject`` ,执行完会发现多了一个blogproject的目录

![](2019-11-29_183705.png)

执行指令``pipenv run python manage.py runserver``

```
Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).

You have 17 unapplied migration(s). Your project may not work properly until you apply the migrations for app(s): admin, auth, contenttypes, sessions.
Run 'python manage.py migrate' to apply them.
November 29, 2019 - 18:38:32
Django version 2.2.7, using settings 'blogproject.settings'
Starting development server at http://127.0.0.1:8000/  
```

看到这样的指令,我们就可以访问http://127.0.0.1:8000/这个地址了,到此我们的web服务器启动完成


django默认的语言是英语,我们可以通过修改配置文件,让它支持中文

打开settings.py,修改如下

```python

# 把英文改为中文
LANGUAGE_CODE = 'zh-hans'
 
# 把国际时区改为中国时区（东八区）
TIME_ZONE = 'Asia/Shanghai'

```

## 建立博客应用

Django 鼓励我们把自己编写的代码组织到应用（Application）里，并且最好是一个应用只提供一种功能。例如我们要开发的 django 博客，相关的代码都放在 blog 这个应用里。其实应用也没什么特殊的，不过是把功能相关的代码组织到一个文件夹里，这个文件夹就成了一个应用（姑且可以这样理解）。

运行``pipenv run python manage.py startapp blog``添加一个博客应用,我们还需要注册该应用,找到settings.py 文件添加注册

```python

HelloDjango-blog-tutorial/blogproject/settings.py
 
## 其他配置项...
 
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'blog', # 注册 blog 应用
]
```

## 创建博客的数据库模型

我们的博客初级版本主要包含博客文章，文章会有分类以及标签。一篇文章只能有一个分类，但可以打上很多标签。

### 编写博客模型代码

```python
blog/models.py
 
from django.db import models
from django.contrib.auth.models import User
 
 
class Category(models.Model):
    """
    django 要求模型必须继承 models.Model 类。
    Category 只需要一个简单的分类名 name 就可以了。
    CharField 指定了分类名 name 的数据类型，CharField 是字符型，
    CharField 的 max_length 参数指定其最大长度，超过这个长度的分类名就不能被存入数据库。
    当然 django 还为我们提供了多种其它的数据类型，如日期时间类型 DateTimeField、整数类型 IntegerField 等等。
    django 内置的全部类型可查看文档：
    https://docs.djangoproject.com/en/2.2/ref/models/fields/#field-types
    """
    name = models.CharField(max_length=100)
 
 
class Tag(models.Model):
    """
    标签 Tag 也比较简单，和 Category 一样。
    再次强调一定要继承 models.Model 类！
    """
    name = models.CharField(max_length=100)
 
 
class Post(models.Model):
    """
    文章的数据库表稍微复杂一点，主要是涉及的字段更多。
    """
 
    # 文章标题
    title = models.CharField(max_length=70)
 
    # 文章正文，我们使用了 TextField。
    # 存储比较短的字符串可以使用 CharField，但对于文章的正文来说可能会是一大段文本，因此使用 TextField 来存储大段文本。
    body = models.TextField()
 
    # 这两个列分别表示文章的创建时间和最后一次修改时间，存储时间的字段用 DateTimeField 类型。
    created_time = models.DateTimeField()
    modified_time = models.DateTimeField()
 
    # 文章摘要，可以没有文章摘要，但默认情况下 CharField 要求我们必须存入数据，否则就会报错。
    # 指定 CharField 的 blank=True 参数值后就可以允许空值了。
    excerpt = models.CharField(max_length=200, blank=True)
 
    # 这是分类与标签，分类与标签的模型我们已经定义在上面。
    # 我们在这里把文章对应的数据库表和分类、标签对应的数据库表关联了起来，但是关联形式稍微有点不同。
    # 我们规定一篇文章只能对应一个分类，但是一个分类下可以有多篇文章，所以我们使用的是 ForeignKey，即一
    # 对多的关联关系。且自 django 2.0 以后，ForeignKey 必须传入一个 on_delete 参数用来指定当关联的
    # 数据被删除时，被关联的数据的行为，我们这里假定当某个分类被删除时，该分类下全部文章也同时被删除，因此     # 使用 models.CASCADE 参数，意为级联删除。
    # 而对于标签来说，一篇文章可以有多个标签，同一个标签下也可能有多篇文章，所以我们使用 
    # ManyToManyField，表明这是多对多的关联关系。
    # 同时我们规定文章可以没有标签，因此为标签 tags 指定了 blank=True。
    # 如果你对 ForeignKey、ManyToManyField 不了解，请看教程中的解释，亦可参考官方文档：
    # https://docs.djangoproject.com/en/2.2/topics/db/models/#relationships
    category = models.ForeignKey(Category, on_delete=models.CASCADE)
    tags = models.ManyToManyField(Tag, blank=True)
 
    # 文章作者，这里 User 是从 django.contrib.auth.models 导入的。
    # django.contrib.auth 是 django 内置的应用，专门用于处理网站用户的注册、登录等流程，User 是 
    # django 为我们已经写好的用户模型。
    # 这里我们通过 ForeignKey 把文章和 User 关联了起来。
    # 因为我们规定一篇文章只能有一个作者，而一个作者可能会写多篇文章，因此这是一对多的关联关系，和 
    # Category 类似。
    author = models.ForeignKey(User, on_delete=models.CASCADE)
```

### 迁移操作数据库

运行``pipenv run python manage.py makemigrations`` 此时只是告诉django我们做了哪些改变,变化记录在migrations目录下
运行``pipenv run python manage.py migrate`` 这个时候我们的模型已经对应的生成了数据库表

这里我们使用了 Python 内置的 SQLite3 数据库

django 在 settings.py 里为我们做了一些默认的数据库配置：

```python
 
## 其它配置选项...
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    }
}
## 其它配置选项...
```

1. 存数据

运行命令``pipenv run python manage.py shell``进入python解释器交互界面

存储分类和标签

```python
>>> from blog.models import Category, Tag, Post
>>> c = Category(name='category test')
>>> c.save()
>>> t = Tag(name='tag test')
>>> t.save()
```

运行命令``pipenv run python manage.py createsuperuser``创建python内置用户

存储文章

```python
>>> from blog.models import Category, Tag, Post
>>> from django.utils import timezone
>>> from django.contrib.auth.models import User
 
>>> user = User.objects.get(username='myuser')
>>> c = Category.objects.get(name='category test')
 
>>> p = Post(title='title test', body='body test', created_time=timezone.now(), modified_time=timezone.now(), category=c, author=user)
>>> p.save()
```

2. 取数据

```python
>>> Category.objects.all()
<QuerySet [<Category: Category object>]>
>>> Tag.objects.all()
<QuerySet [<Tag: Tag object>]>
>>> Post.objects.all()
<QuerySet [<Post: Post object>]>
>>>
```

3. 改数据


```python
>>> c = Category.objects.get(name='category test')
>>> c.name = 'category test new'
>>> c.save()
>>> Category.objects.all()
<QuerySet [<Category: test category new>]>
```

4. 删数据

```python
>>> p = Post.objects.get(title='title test')
>>> p
<Post: title test>
>>> p.delete()
(1, {'blog.Post_tags': 0, 'blog.Post': 1})
>>> Post.objects.all()
<QuerySet []>
```



## Django处理Http请求

django  作为一个 Web 框架，它的使命就是接收浏览器发来的 HTTP 请求，返回相应的 HTTP 响应

### Hello World视图函数

#### 绑定url与视图函数

首先 django 需要知道当用户访问不同的网址时，应该如何处理这些不同的网址（即所说的路由）。django 的做法是把不同的网址对应的处理函数写在一个 urls.py 文件里，当用户访问某个网址时，django 就去会这个文件里找，如果找到这个网址，就会调用和它绑定在一起的处理函数（叫做视图函数）

首先在blog应用的目录下创建一个urls.py文件,添加如下内容

```python
from django.urls import path

from . import views

urlpatterns=[
    path('',views.index,name='index'),
]
```

绑定关系的写法是把网址和对应的处理函数作为参数传给 path 函数（第一个参数是网址，第二个参数是处理函数），另外我们还传递了另外一个参数 name，这个参数的值将作为处理函数 index 的别名，这在以后会用到

注意这里我们的网址实际上是一个规则，django 会用这个规则去匹配用户实际输入的网址，如果匹配成功，就会调用其后面的视图函数做相应的处理。

比如说我们本地开发服务器的域名是 http://127.0.0.1:8000，那么当用户输入网址 http://127.0.0.1:8000 后，django 首先会把协议 http、域名 127.0.0.1 和端口号 8000 去掉，此时只剩下一个空字符串，而 '' 的模式正是匹配一个空字符串，于是二者匹配，django 便会调用其对应的 views.index 函数。

### 编写视图函数

blog/views.py

```python
from django.http import HttpResponse

def index(request):
    return HttpResponse("欢迎访问我的博客首页")
```

## 配置项目URL

还差最后一步了，我们前面建立了一个 urls.py 文件，并且绑定了 URL 和视图函数 index，但是 django 并不知道。django 匹配 URL 模式是在 blogproject 目录（即 settings.py 文件所在的目录）的 urls.py 下的，所以我们要把 blog 应用下的 urls.py 文件包含到 blogproject\urls.py 里去，打开这个文件看到如下内容：

修改成如下格式

```python
from django.contrib import admin
from django.urls import path, include
 
urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('blog.urls')),
]
```

此时在运行我们就可以看到djagngo返回的内容了.这基本上就上 django 的开发流程了，写好处理 HTTP 请求和返回 HTTP 响应的视图函数，然后把视图函数绑定到相应的 URL 上。但是我们总不能每次都返回这么一堆字符串,下面我们介绍下django提供的模板系统

## 使用django模板系统

# django Admin介绍

上面我们已经创建了账户,现在我们启动我们开发服务器,访问http://127.0.0.1:8000/admin/,用创建的账户登录,可以看到django管理界面

我们想要我们的博客也可以在也出现在管理界面,只有一件事要做,就是告诉管理员,打开blog/admin.py

```python


```