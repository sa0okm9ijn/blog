---
title: Docker-基础知识
date: 2020-04-08 10:09:57
tags: 
- Docker 
categories: Docker 
description: 
---


# 前言

``Docker``翻译过来是码头工人的意思.早期的码头上分为码头、码头工人、货物、运输工具.由于货物的多样性,有时候并不能放到一起运输,这时候就得增加运输工具来运输.后来就有了``集装箱``的出现.解决了货物不能一起运输的难题.对我们``Docker``有了字面上的理解我们再回到我们软件.

1. 单机时代

比如我们有一个购物网站.分为商品服务、订单服务、支付服务等三大块.商品服务是由java开发的,订单服务是由python开发的,支付服务是由.Net开发的,部署在同一台电脑上,很容易造成环境冲突、端口冲突等问题.

2. 虚拟机时代

我们可以利用三个虚拟机分别部署上坪服务、订单服务、支付问题.由虚拟机管理工具对虚拟机进行管理.解决了端口冲突和环境冲突的问题.但是虚拟机耗费资源硬件,配置和启动耗时.

3. 容器时代

Docker 使用客户端-服务器 (C/S) 架构模式，使用远程API来管理和创建Docker容器。Docker 容器通过 Docker 镜像来创建。容器与镜像的关系类似于面向对象编程中的对象与类

Docker采用 C/S架构,Docker daemon 作为服务端接受来自客户的请求，并处理这些请求（创建、运行、分发容器）。 客户端和服务端既可以运行在一个机器上，也可通过 socket 或者RESTful API 来进行通信。

Docker daemon 一般在宿主主机后台运行，等待接收来自客户端的消息。 Docker 客户端则为用户提供一系列可执行命令，用户用这些命令实现跟 Docker daemon 交互

![](a.png)


一个完整的``Docker``由以下几个部分组成:
- **DockerClient客户端**
- **Docker Daemon守护进程**
- **容器:**集装箱,相当于我们面向对象中的对象
- **镜像:**集装箱模板,相当用户我们面向对象中的类
- **仓库:**码头,相当于我们面向对象中的程序集,用来存储镜像

![](b.jfif)

**总结**:

1. docker 是一个开源的应用容器引擎,
2. docker 可以让开发者打包他们的应用以及依赖包到一个轻量级、可移植的镜像中,然后发布到任何流行的 Linux 机器上，也可以实现虚拟化。
3. 容器之间不会有任何接口冲突问题,更重要的是容器性能开销极低




# Docker安装

# Docker基本操作

1. 启动

```shell
service docker start
```

1. 重启

```shell
service docker restart
```

3. 版本

```shell
docker version
```

4. 运行状态

```shell
systemctl status docker
```

5. 安装目录

```shell
cd /
cd /var/lib/docker
```

# Docker 管理命令

| 命令  | 描述  |
|---|---|
| builder   | Manage Builds 管理构建  |
| config    | Manage Docker configs 管理配置 |
| container | Manage containers 管理容器 |
| context   | Manage contexts 管理上下文 |
| engine    | Manage the docker engine 管理引擎 |
| image     | Manage images 管理镜像 |
| network   | Manage networks 管理网络 |
| node      | Manage Swarm nodes 管理节点(集群) |
| plugin    | Manage plugins 管理插件 |
| secret    | Manage Docker secrets 管理密钥 |
| service   | Manage services 管理服务 |
| stack     | Manage Docker stacks 管理 |
| swarm     | Manage Swarm 管理集群 |
| system    | Manage Docker 管理系统 |
| trust     | Manage trust on Docker images 管理信任 |
| volume    | Manage volumes 管理数据挂载(数据持久化 === 永久保存) |