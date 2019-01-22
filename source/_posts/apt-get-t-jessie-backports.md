title: apt-get -t jessie-backports
author: MiracleQi-温柔魔君
tags:
  - apt
  - jessie
categories:
  - Linux
date: 2016-11-30 14:17:00
cover: /img/post-cover/36.jpg
---
# 背景

最近有个需求，openssl 需要在 1.0.2e 版本以上  
但是 apt-get 默认最新版才是 1.0.1h 版  
debian8 更新软件不仅有 jessie 版，还有 jessie-backports 版  
jessie-backports 版的软件都是最新的

# jessie-backports

那么如何使得 apt-get 安装 jessie-backports 版的软件呢

```
1. 更新sources.list
   在 /etc/apt/sources.list 中添加
   deb http://ftp.cn.debian.org/debian jessie-backports main contrib non-free
2. apt-get update
3. 安装所需软件（如openssl）
   apt-get install -t jessie-backports openssl
```
到此，openssl 已从 jessie-bakcports 处更新到了最新版