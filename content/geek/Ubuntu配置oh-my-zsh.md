---
title: "Ubuntu配置oh-My-Zsh"
date: 2023-02-23T16:31:19+08:00
lastmod: 2023-02-23T16:31:19+08:00
author: ["oldchow"]

categories:
- category 1
- category 2

tags:
- tag ubuntu
- tag zsh

keywords:
- word ubuntu
- word zsh
- word oh-my-zsh

description: "Ubuntu配置oh-My-Zs" # 文章描述，与搜索优化相关
summary: "Ubuntu配置oh-My-Zs" # 文章简单描述，会展示在主页
weight: # 输入1可以顶置文章，用来给文章展示排序，不填就默认按时间排序
slug: ""
draft: false # 是否为草稿
comments: true
showToc: true # 显示目录
TocOpen: false # 自动展开目录
autonumbering: true # 目录自动编号
hidemeta: false # 是否隐藏文章的元信息，如发布日期、作者等
disableShare: true # 底部不显示分享栏
searchHidden: true # 该页面可以被搜索到
showbreadcrumbs: true #顶部显示当前路径
mermaid: true
cover:
    image: "https://static.oldchow.cn/md-oh-my-zsh-logo.png"
    caption: ""
    alt: ""
    relative: false
---

## #1.安装zsh

```bash
sudo apt-get install zsh
```

## #2.安装oh-my-zsh

官网[[Oh My Zsh - a delightful & open source framework for Zsh](https://ohmyz.sh/)]



```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

or

```bash
sh -c "$(wget https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```



## #3.命令提示插件

安装

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

修改zsh配置文件，添加插件

```bash
vi ~/.zshrc
```

添加插件

```bash
plugins=(git zsh-autosuggestions))  # 搜索plugins 在git后面 空格加插件名称
```

生效插件

```bash
source ~/.zshrc
```

