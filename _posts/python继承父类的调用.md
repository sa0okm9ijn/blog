---
title: python继承父类的调用
date: 2019-05-29 13:50:24
tags: 
- Python  
categories: Python  
description: 
---
python中的一个派生类集成多个基类时候。实例化派生类对象后调用方法。如下代码

    
``` 
class BaseRequest:
    pass

class RequestHandler(BaseRequest):
    def process_request(self):
        print("RequestHandler.process_request")

    def serve_forever(self):
        print("RequestHandler.serve_forever")
class Minx:
    def process_request(self):
        print("minx.process_request")
class Son(Minx,RequestHandler):
    pass

obj=Son()
obj.process_request()

```
 示例中Son派生类分别继承Minx和RequestHandler,当调用父类中的方法时候查找顺序如下图所示

![](584421-20180717195250503-1148197544.png)

如果所示从左开始找找不到返回从头开始找右继承开始查找





同一个根的时候最后查找根

