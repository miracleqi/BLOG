title: VMRC 控制台的连接已断开
author: MiracleQi-温柔魔君
tags:
  - vm
categories:
  - Windows
date: 2018-07-06 17:55:00
cover: /img/post-cover/50.jpg
---
# 1. 背景

在使用 vSphere Client 的时候，远程一台 XP 虚拟机。之前使用一切正常，但在一次添加新的网卡重启后，控制台报错！

![upload successful](/images/pasted-33.png)

PS：vSphere Client 版本: 5.5

# 2. 解决方法

查找资料后，需要重启电脑，需要卸载 VSphere Client，太过于繁琐。

下面是我的处理方法：

## 2.1 关闭 DEP 策略

用管理员身份在 CMD 窗口执行：`bcdedit.exe /set nx AlwaysOff`

## 2.2 关闭 vmware-vmrc.exe 进程

关闭 vSphere Client，在任务管理器中结束 vmware-vmrc.exe

到此，开启 vSphere Client 后，控制台恢复正常。