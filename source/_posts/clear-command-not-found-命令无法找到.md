title: 'clear: command not found 命令无法找到'
author: MiracleQi-温柔魔君
tags:
  - clear
categories:
  - Linux
date: 2017-07-25 15:40:00
cover: /img/post-cover/44.jpg
---
# 1. 安装 ncurses-bin

```
sudo apt-get install ncurses-bin
```

此时尝试执行 'clear' 命令，若失败，执行第二步（重新安装 ncurses-bin）

# 2. 重新安装 ncurses-bin

```
sudo apt-get --reinstall install ncurses-bin
```

此时 'clear' 命令即可成功执行