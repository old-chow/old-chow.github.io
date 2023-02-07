---
title: "自建Syncthing 多端同步神器"
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

## 一、Syncthing部署

前提：想要能够相互联通各个客户端，最基础的要求就是需要一个公网ip（动态也行）或者一个有公网ip的服务器。但是如果是纯粹局域网同步的话就不需要考虑这个点了。

我这边