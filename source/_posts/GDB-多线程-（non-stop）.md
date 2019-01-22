title: GDB 多线程 （non-stop）
author: MiracleQi-温柔魔君
tags:
  - gdb
categories:
  - Linux
date: 2018-03-21 15:43:00
cover: /img/post-cover/45.jpg
---
# 1. 背景

这几天在扩展 ngx_lua 模块，但 gdb 定位时，提示：Thread debugging using libthread_db enabled。

# 2. GDB non-stop 配置

把以下3行添加到 ~/.gdbinit 来打开 non-stop 模式

```
set target-async 1
set pagination off
set non-stop on
```

PS：无 ~/.gdbinit 文件，可以创建此文件，或修改 /etc/gdb 下对应文件

# 3. 文件更新立即生效

```
source ~/.gdbinit
```

参考文章: https://www.cnblogs.com/dongzhiquan/archive/2011/07/09/2101578.html