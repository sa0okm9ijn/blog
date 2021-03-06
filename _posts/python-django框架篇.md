---
title: Python 框架篇
date: 2019-05-29 13:29:37
tags: 
- Python django 
categories: Python 
description: 
---
框架即FrameWork，旨在更快的解决共性问题。

对于所有的web应用，本质就是一个socke服务端和socke浏览器客户端

## 自己封装的一个简单web框架

    
```
import socket

def handle_request(conn):
    buf = conn.recv(1024)
    conn.send("HTTP/1.1 200 OK\r\n\r\n".encode("utf8"))
    conn.send("<h1 style='color:red'>Hello World</h1>".encode("utf8"))


def main():
    sock = socket.socket(socket.AF_INET,socket.SOCK_STREAM)
    sock.bind(('localhost',8001))
    sock.listen(5)

    while True:
        connection,address = sock.accept()
        handle_request(connection)
        connection.close()

if __name__ == "__main__":
    main()
```
我们监听一个8001端口，当浏览器访问该端口，我们返回一个h标签给客户端。这就实现了一个简单的请求响应，但是具体的解析http请求，发送http响应，这都需要专业的http技能，

所以，需要一个统一的接口，这个接口就是WSGI：Web Server Gateway Interface。

## python wsgi接口web框架

```

#框架示例demo 显示当前时间  示例web框架的解析
from wsgiref.simple_server import make_server
import time

def current_time(request):
    cur_time=time.ctime(time.time())
    f=open("current_time.html","rb")
    data=f.read()
    data=str(data,"utf8").replace("!cur_time!",str(cur_time))
    return [data.encode("utf8")]

def routes():
    urlpatterns=(
        ('/current_time',current_time),
    )
    return urlpatterns



def application(environ,start_response):
    start_response("200 OK",[('Content-Type','text/html')])
    path=environ["PATH_INFO"]

    urlpatterns=routes()
    func=None
    for item in urlpatterns:
        if item[0] == path:
            func=item[1]
            break;
    if func:
        return func(environ)

    else:
        return ["<h1>404</h1>".encode("utf8")]
    return [b'<h1>Hello,World</h1>']




httpd = make_server('',8080,application)
print("serving http on port 8080...")
httpd.serve_forever()

```


