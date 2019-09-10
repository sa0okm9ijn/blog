---
title: Python爬虫系列
date: 2019-09-03 17:15:05
tags: 
- Python爬虫轻松学 
categories: Python  
description:  
---

# HTTP协议之请求

![](2019-09-04_063054.png)

## 重要的几个参数

1. method：这个字段是用来指明请求的方法是哪一种的，常用的请求方法有GET、POST


```python
import requests

response=requests.get('https://www.zhihu.com')

```

```python
import requests
data={
    'username':'shiyue',
    'password':'shiyue'
    }
response=requests.post('https://www.wzhihu.com',data=data)
```

2. Accept：这个字段是用来通知服务器，用户代理（浏览器等客户端）能够处理的媒体类型及媒体类型的相对优先级。可以使用type/subtype这种形式，一次可指定多种

>媒体类型。常用的媒体类型有以下几类：

>文本文件：text/html，text/plain，text/css，application/xhtml+xml，application/xml...

>图片文件：image/jpeg，image/gif，image/png...

>视频文件：video/mpeg，vedio/quicktime...

>应用程序使用的二进制文件：application/octer-stream，application/zip...

3. Cookie：客户端发起请求时，服务器会返回一个键值对形式的数据给浏览器，下一次浏览器再访问这个域名下的网页时，就需要携带这些键值对数据在Cookie中，用来记录用户在当前域名下的历史行为的。

这个字段很重要，在爬虫中经常会用到，因为有的数据只有携带了Cookie才能够爬取到，所以经常会根据前次访问得到cookie数据，然后添加到下一次的访问请求头中

```python
import requests

url='https://www.baidu.com'

headers={
        'cookie':'PSTM=1496322685;BIDUPSID=BC36002F7DA142E6674AE290CD5A38DB;__cfduid=ddf4836dd1f1ac99eeea8ef0f140493301522406372;BAIDUID=5FA7A2B4FDDA3CECC6BE9B74FDCD00B8:FG=1;sugstore=1;BDUSS=1hvT3VoQmc5TDl5bFE1c2NjcGpOenBycnJTOEstZ0ZKcGs5UnB1dzVyU1hpYXRiQVFBQUFBJCQAAAAAAAAAAAEAAABCcYSYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAJf8g1uX~INbR;BD_UPN=12314753;MCITY=‐340%3A;delPer=0;BD_CK_SAM=1;PSINO=7;BDRCVFR[Dq4jqEr7erC]=mk3SLVN4HKm;H_PS_PSSID=;BDORZ=FFFB88E999055A3F8A630C64834BD6D0;H_PS_645EC=216feJgh%2BnAm%2BJD6G3sw10RBbYN1O%2FeCJqUhgtRyZ3OuJO0EOqbXUwL8Kgf8zhqXH7RWxBnn;BDSVRTM=0;ispeed_lsm=6'
    }
```

4. Refer:这个字段用来记录浏览器上次访问的URL，有的网站会通过请求中有没有携带这个参数来判断是不是爬虫，从而确定是否限制访问。所以有时候也需要在headers中添加上这个参数。

5. User-Agent:是用来标识请求的浏览器身份的，大部分网站都会通过请求中有没有携带这个参数来判断是不是爬虫，从而确定是否限制访问。所以有时候也需要在headers中添加上这个参数。我们要爬取的数据量比较大的时候，仅仅用一个user-agent是不够的

```python
import requests，random

agent_list=['Mozilla/5.0(WindowsNT10.0;WOW64)AppleWebKit/537.36(KHTML,likeGecko)Chrome/66.0.3359.139Safari/537.36',
           'Mozilla/5.0(Macintosh;U;IntelMacOSX10_6_8;en‐us)AppleWebKit/534.50(KHTML,likeGecko)Version/5.1Safari/534.50',
           'Mozilla/5.0(compatible;MSIE9.0;WindowsNT6.1;Trident/5.0',
            'Mozilla/4.0(compatible;MSIE6.0;WindowsNT5.1)'
        ]

headers={
    'user‐agent':random.choice(agent_list)
    }
```

# HTTP协议之响应

![](2019-09-04_065148.png)

## 重要的几个参数

1. apparent_encoding 这个属性能够很好地帮助我们确认网页源码的编码方式，避免获取到的内容乱码

```python

#实现功能，避免获取到的网页源码是乱码
import requests

res=requests.get('https://www.baidu.com')
res.encoding=res.apparent_encoding
#这样，我们就不需要去关心获取到的网页源码的编码格式具体是什么
print(res.text)
f=open('baidu.com','w',encoding=res.encoding)
f.write(res.text)
f.close()

```
2. cookies 该属性保存了用户的cookie值，我们有的时候可以通过获取到上一个请求的cookie，作为请求头的一个cookie参数传入到请求中
   
3. headers 这个属性中记录了响应头中的相关内容
   
4. request 这个属性记录了请求的相关信息
   
5. status_code 这个属性表示响应的状态码，当我们一次性爬取的url数量过多的时候，就需要用status_code来过滤掉请求失败的url

# 爬虫伦理

服务器在通常情况下，对搜索引擎是欢迎的态度，但是，这是有条件的，而这些条件会写在Robots协议。在进行爬虫操作的时候，要有所为，也要有所不为，要用爬虫做有意义的事，不去破坏规则。

查看规则如淘宝,https://www.taobao.com/robots.txt

# 数据简单处理的常用方法

1. strip
2. replace
3. split
4. startswith
5. endswith
6. jon
7. 列表去重

# 爬虫开始

## 数据获取

安装requests库来获取数据
>pip install requsets

```python
import requests 
res = requests.get('https://res.pandateacher.com/2018-12-18-10-43-07.png')
```

res是一个对象，属于requests.models.Response类

![](crawler-l0-17-1-2019110.png)

## 数据解析

安装BeautifulSoup
>pip install BeautifulSoup4

```python

import requests
from bs4 import BeautifulSoup
#引入BS库
res = requests.get('https://localprod.pandateacher.com/python-manuscript/crawler-html/spider-men5.0.html') 
html = res.text
soup = BeautifulSoup(html,'html.parser') #把网页解析为BeautifulSoup对象


```

![](2019-01-23-16-36-57.png)

![](crawler-l2-16-201919.png)


**浏览器分析标签示意**

![](crawler-l3-9-201914.png)

**请求头**

```python

headers = {
    'origin':'https://y.qq.com',
    # 请求来源，本案例中其实是不需要加这个参数的，只是为了演示
    'referer':'https://y.qq.com/n/yqq/song/004Z8Ihr0JIu5s.html',
    # 请求来源，携带的信息比“origin”更丰富，本案例中其实是不需要加这个参数的，只是为了演示
    'user-agent':'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36',
    # 标记了请求从什么设备，什么浏览器上发出
    }

```










## 数据保存


### csv

```python

import csv
#引用csv模块。
csv_file = open('demo.csv','w',newline='',encoding='utf-8')
#调用open()函数打开csv文件，传入参数：文件名“demo.csv”、写入模式“w”、newline=''、encoding='utf-8'。
writer = csv.writer(csv_file)
# 用csv.writer()函数创建一个writer对象。
writer.writerow(['电影','豆瓣评分'])
#调用writer对象的writerow()方法，可以在csv文件里写入一行文字 “电影”和“豆瓣评分”。
writer.writerow(['银河护卫队','8.0'])
#在csv文件里写入一行文字 “银河护卫队”和“8.0”。
writer.writerow(['复仇者联盟','8.1'])
#在csv文件里写入一行文字 “复仇者联盟”和“8.1”。
csv_file.close()
#写入完成后，关闭文件就大功告成啦！

```


### excel

```python

import openpyxl 
wb=openpyxl.Workbook() 
sheet=wb.active
sheet.title='new title'
sheet['A1'] = '漫威宇宙'
rows= [['美国队长','钢铁侠','蜘蛛侠'],['是','漫威','宇宙', '经典','人物']]
for i in rows:
    sheet.append(i)
wb.save('Marvel.xlsx')

```

## 带有cookies数据获取


### 存储cookie

```python

import requests,json
#引入requests和json模块。
session = requests.session()   
url = ' https://wordpress-edu-3autumn.localprod.oc.forchange.cn/wp-login.php'
headers = {
'User-Agent':'Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36'
}
data = {
'log': input('请输入你的账号:'),
'pwd': input('请输入你的密码:'),
'wp-submit': '登录',
'redirect_to': 'https://wordpress-edu-3autumn.localprod.oc.forchange.cn/wp-admin/',
'testcookie': '1'
}
session.post(url, headers=headers, data=data)

cookies_dict = requests.utils.dict_from_cookiejar(session.cookies)
#把cookies转化成字典。
print(cookies_dict)
#打印cookies_dict
cookies_str = json.dumps(cookies_dict)
#调用json模块的dumps函数，把cookies从字典再转成字符串。
print(cookies_str)
#打印cookies_str
f = open('cookies.txt', 'w')
#创建名为cookies.txt的文件，以写入模式写入内容。
f.write(cookies_str)
#把已经转成字符串的cookies写入文件。
f.close()
#关闭文件。

```

### 读取cookie

```python

import requests,json
session = requests.session()
#创建会话。
headers = {
'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.110 Safari/537.36'
}
#添加请求头，避免被反爬虫。
try:
#如果能读取到cookies文件，执行以下代码，跳过except的代码，不用登录就能发表评论。
    cookies_txt = open('cookies.txt', 'r')
    #以reader读取模式，打开名为cookies.txt的文件。
    cookies_dict = json.loads(cookies_txt.read())
    #调用json模块的loads函数，把字符串转成字典。
    cookies = requests.utils.cookiejar_from_dict(cookies_dict)
    #把转成字典的cookies再转成cookies本来的格式。
    session.cookies = cookies
    #获取cookies：就是调用requests对象（session）的cookies属性。

except FileNotFoundError:
#如果读取不到cookies文件，程序报“FileNotFoundError”（找不到文件）的错，则执行以下代码，重新登录获取cookies，再评论。

    url = ' https://wordpress-edu-3autumn.localprod.oc.forchange.cn/wp-login.php'
    #登录的网址。
    data = {'log': input('请输入你的账号:'),
            'pwd': input('请输入你的密码:'),
            'wp-submit': '登录',
            'redirect_to': 'https://wordpress-edu-3autumn.localprod.oc.forchange.cn/wp-admin/',
            'testcookie': '1'}
    #登录的参数。
    session.post(url, headers=headers, data=data)
    #在会话下，用post发起登录请求。

    cookies_dict = requests.utils.dict_from_cookiejar(session.cookies)
    #把cookies转化成字典。
    cookies_str = json.dumps(cookies_dict)
    #调用json模块的dump函数，把cookies从字典再转成字符串。
    f = open('cookies.txt', 'w')
    #创建名为cookies.txt的文件，以写入模式写入内容
    f.write(cookies_str)
    #把已经转成字符串的cookies写入文件
    f.close()
    #关闭文件

```



## selenium

selenium它可以用几行代码，控制浏览器，做出自动打开、输入、点击等操作，就像是有一个真正的用户在操作一样

```python

# 本地Chrome浏览器设置方法
from selenium import webdriver #从selenium库中调用webdriver模块
driver = webdriver.Chrome() # 设置引擎为Chrome，真实地打开一个Chrome浏览器

```

![](crawler-l9-9-0-2019118.png)

![](2019-03-25-16-26-33.png)


**操作浏览器**


```python

.send_keys() # 模拟按键输入，自动填写表单
.click() # 点击元素

```


## 定时功能


```python

import schedule
import time
#引入schedule和time

def job():
    print("I'm working...")
#定义一个叫job的函数，函数的功能是打印'I'm working...'

schedule.every(10).minutes.do(job)       #部署每10分钟执行一次job()函数的任务
schedule.every().hour.do(job)            #部署每×小时执行一次job()函数的任务
schedule.every().day.at("10:30").do(job) #部署在每天的10:30执行job()函数的任务
schedule.every().monday.do(job)          #部署每个星期一执行job()函数的任务
schedule.every().wednesday.at("13:15").do(job)#部署每周三的13：15执行函数的任务

while True:
    schedule.run_pending()
    time.sleep(1)    
#13-15都是检查部署的情况，如果任务准备就绪，就开始执行任务。

```