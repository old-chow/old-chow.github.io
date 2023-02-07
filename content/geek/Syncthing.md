---
title: "【Docker】自建Syncthing 多端同步神器"
date: 2023-02-07T02:14:14Z
lastmod: 2023-02-07T02:14:14Z
author: ["oldchow"]

tags:
- Docker
- Geek
- Syncthing

keywords:
- Syncthing
- Docker
- self-host

description: "自建Syncthing 多端同步神器" # 文章描述，与搜索优化相关
summary: "自建Syncthing 多端同步神器" # 文章简单描述，会展示在主页
weight: # 输入1可以顶置文章，用来给文章展示排序，不填就默认按时间排序
slug: ""
draft: false # 是否为草稿
comments: true
showToc: true # 显示目录
TocOpen: false # 自动展开目录
autonumbering: true # 目录自动编号
hidemeta: false # 是否隐藏文章的元信息，如发布日期、作者等
disableShare: true # 底部不显示分享栏
searchHidden: false # 该页面可以被搜索到
showbreadcrumbs: true #顶部显示当前路径
mermaid: true
cover:
    image: "https://static.oldchow.cn/md-Syncthing-logo.svg"
    caption: ""
    alt: "syncthing logo"
    relative: false
---

## 一、前提相关

前提：想要能够相互联通各个客户端，最基础的要求就是需要一个公网ip（动态也行）或者一个有公网ip的服务器。但是如果是纯粹局域网同步的话就不需要考虑这个点了。

我这边有nas以及公网ip，所以我这边直接在nas上使用Docker部署Syncthing，并且将端口暴露出去，作为一中心节点，存储数据已经提供网络环境。

Syncthing官方地址：[https://syncthing.net/](https://syncthing.net/)

Syncthing Github地址：[https://github.com/syncthing/syncthing](https://github.com/syncthing/syncthing)

Docker镜像地址：[https://hub.docker.com/r/linuxserver/syncthing](https://hub.docker.com/r/linuxserver/syncthing)

## 二、Docker部署

docker命令行：

``` 
docker run -d \
    -p 8384:8384 -p 22000:22000/tcp \
    -p 22000:22000/udp -p 21027:21027/udp \
    -v /xxxxxx:/config \
    -v /xxxxxx:/Documents  \
    --hostname=my-syncthing \
    syncthing/syncthing:latest
```

docker compose:

```yml
version: "2.1"
services:
  syncthing:
    image: lscr.io/linuxserver/syncthing
    container_name: syncthing
    environment:
      - PUID=0
      - PGID=0
      - TZ=Asia/Shanghai
    volumes:
      - /xxxxx:/config
      - /xxxxx:/Documents
    ports:
      - 8384:8384
      - 22000:22000/tcp
      - 22000:22000/udp
      - 21027:21027/udp
    restart: unless-stopped
```

自行替换配置文件以及数据存储位置. 相关配置请参考下图，可以在docker镜像链接找到相应信息
![](https://static.oldchow.cn/md-syncthing-docker-explain.png)

## 三、Syncthing配置

Syncthing不像icloud、群晖和威联通等其他软件一样智能，只拉取文件索引，占据小部分空间，只有当你需要的时候再通过网络下载。Syncthing是全量同步，当你设置同步文件夹的时候，务必考虑清楚数据的存储位置。我这边选择将所有文件存储到nas上面，并且由于有公网ip，所以是所有端的的中心节点。

### 1.暴露端口

能够让其他端添加nas位远程设备，需要将22000端口暴露出去，允许公网访问，协议可以为tcp/udp