title: utrace 安装
author: MiracleQi-温柔魔君
tags:
  - nginx
  - utrace
categories:
  - Linux
date: 2016-06-21 17:55:00
cover: /img/post-cover/22.jpg
---
debian 上安装 utrace

## 背景

今天安装 nginx-systemtap-toolkit 时需要安装 utrace （内核版本为 debian3.2，无内嵌的 utrace）

## 安装

下载 https://github.com/utrace/linux/branches 对应的 linux-utrace-3.2 版本

```
7za x linux-utrace-3.2.zip
cd linux-utrace-3.2
make allyesconfig     -- 用来生成 .config 文件
cp .config include/config/auto.conf
make oldconfig && make prepare
make && make install
```
## 安装时遇到的问题

下载 https://github.com/utrace/linux/branches 对应的 linux-utrace-3.2 版本

```
7za x linux-utrace-3.2.zip
```

PS: 第一次用 unzip 时报错，提示文件名过长，改用 7za 问题解决

```
cd linux-utrace-3.2
make 
```

此时提示无 ```include/config/auto.conf```

```make oldconfig``` 又会有很多新的选项（上千条）需要手动选择

因此执行 ```make allyesconfig``` 生成 ```.config```

```
cp .config include/config/auto.conf
```

此时再 ```make```，提示 ```generated/autoconf.h: No such file or directory```

运行 ```make oldconfig && make prepare``` 进行修复

再次 ```make && make install``` 成功