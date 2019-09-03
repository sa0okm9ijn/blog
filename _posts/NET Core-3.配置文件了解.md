---
title: .Net Core MVC配置文件了解
date: 2019-03-07 09:36:00
tags: 
- .NET Core简易入门
categories: .NET
description: .net core 配置文件的变化
---
## 1、appsettings.json配置文件

当我们用dotnet new 命令创建了一个MVC项目后，系统就自动帮我们创建好appsettings.json配置文件,其默认内容如下：
```
{
  "Logging": {
    "LogLevel": {
      "Default": "Warning"
    }
  },
  "AllowedHosts": "*"
}
```
我们做如下改变：
``` 
{
  "Logging": {
    "LogLevel": {
      "Default": "Warning"
    }
  },
  "AllowedHosts": "*",
  "title":"第一个MVC项目"
}
```
在控制器Controllers\HomeController.cs中读取该节点作为首页的标题
```
public IActionResult Index([FromServices]IConfiguration cfg)
{
      ViewData["Title"]=cfg["title"];
      return View();
}
```
**注意添加Microsoft.Extensions.Configuration引用**

启动网站，浏览如下

![](584421-20190307151832836-96437523.png)

为了方便使用，我们可以把节点配置为实体对象
```
{
  "Logging": {
    "LogLevel": {
      "Default": "Warning"
    }
  },
  "AllowedHosts": "*",
  "title":"第一个MVC项目",
  "Person":{
    "name":"jack",
    "age":15
  }
}
```


 添加实体类
```
public class Person
{
      public string name{get;set;}
      public int age{get;set;}
}
```


转化实体类，得到内容

![](584421-20190307152500145-1093395512.png)

## 2、hosting.json文件

hosting.json配置文件可以用来配置网站的端口，我们先在项目根目录下创建一个hosting.json文件，输入以下内容：
```
{
    "server.urls":"http://127.0.0.1:8085;http://127.0.0.1:8086;"
}
```


修改Program.cs
```
public static IWebHostBuilder CreateWebHostBuilder(string[] args)
{
            var hostConfiguration = new ConfigurationBuilder().AddJsonFile("hosting.json").Build();
            return WebHost.CreateDefaultBuilder()
            .UseStartup<Startup>()
            .UseConfiguration(hostConfiguration);
}
```


.NET Core 工具的开发过程中实施了一项重要的设计更改，即不再支持  _project.json_  文件，而是将 .NET Core 项目转移到
MSBuild/csproj 格式。

为了我们可以读到hosting.json配置文件，在编译的时候需要把这个文件输出到bin\debug目录下面，如此我们修改.csproj文件如下
```
<ItemGroup>
    <None Include="hosting.json" CopyToOutputDirectory="Always" />
</ItemGroup>
```


##### 删除 Properties 目录下的 launchSettings.json 文件

**dotnet run**

![](584421-20190307173501496-946237566.png)

如此我们成功启动了自己定义的端口。



