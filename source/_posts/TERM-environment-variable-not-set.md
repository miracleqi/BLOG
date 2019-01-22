title: TERM environment variable not set
author: MiracleQi-温柔魔君
tags:
  - clear
  - TERM
  - ncurses-bin
categories:
  - Linux
date: 2016-10-10 19:16:00
cover: /img/post-cover/33.jpg
---
这几天装的 debian docker 发现没有 clear 指令

安装 ncurses-bin，发现已经是最新的了

which clear，结果是 /usr/bin/clear

此时 clear 指令报错如下：TERM environment variable not set

set | grep TERM 结果是：TERM=dumb

有关 TERM 的知识请参考：

http://blog.csdn.net/ly890700/article/details/53229063


最终 export TERM=xterm 解决了问题