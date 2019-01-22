title: linux 查看系统开机时间
author: MiracleQi-温柔魔君
tags:
  - time
categories:
  - Linux
date: 2018-07-10 18:01:00
cover: /img/post-cover/51.jpg
---
有时候需要查看Linux系统运行了多久时间，此时需要知道上次开机启动时间；  
有时候由于断电或供电故障突然停机，需要查看Linux开机时间/重启时间；  
下面总结一些查看Linux开机关机时间的方法（非常全面）

# 1. who 命令查看

`who -b` 查看最后一次系统启动的时间。  
`who -r` 查看系统是以哪一级别启动的。
```
[root@DB-Server ~]# who -b
      system boot May 11 09:27
[root@DB-Server ~]# who -r
      run-level 5 May 11 09:27
```

# 2. last reboot

如下所示 last reboot 可以看到 Linux 系统历史启动的时间。 重启一下操作系统后，然后
```
[root@DB-Server ~]# last reboot
reboot system boot 2.6.9-42.ELsmp Thu May 29 15:25 (00:07)
reboot system boot 2.6.9-42.ELsmp Sun May 11 09:27 (18+05:55)

wtmp begins Mon May 5 16:18:57 2014
```

如果只需要查看最后一次 Linux 系统启动的时间
```
[root@DB-Server ~]# last reboot | head -1
reboot system boot 2.6.9-42.ELsmp Thu May 29 15:25 (00:08)
```
# 3. TOP 命令查看

如下截图所示，up后表示系统到目前运行了多久时间。反过来推算系统重启时间

![upload successful](/images/pasted-34.png)

# 4. w 命令查看

如下截图所示，up后表示系统到目前运行了多久时间。反过来推算系统重启时间

![upload successful](/images/pasted-35.png)

# 5. uptime 命令查看

```
root@ADG-T6-254:~# uptime
 18:05:33 up 46 days,  4:19,  2 users,  load average: 0.02, 0.02, 0.05
```
# 6. 查看 /proc/uptime
```
[root@DB-Server ~]# cat /proc/uptime
1415.59 1401.42
[root@DB-Server ~]# date -d "`cut -f1 -d. /proc/uptime` seconds ago"
Thu May 29 15:24:57 CST 2014
[root@DB-Server ~]# date -d "$(awk -F. '{print $1}' /proc/uptime) second ago" +"%Y-%m-%d %H:%M:%S"
2014-05-29 15:24:57
```

[原文链接](#https://www.cnblogs.com/kerrycode/p/3759395.html)，我修改了 `who -r` 说明
