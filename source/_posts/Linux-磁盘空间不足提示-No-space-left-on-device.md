title: Linux 磁盘空间不足提示 No space left on device
author: MiracleQi-温柔魔君
tags:
  - du
categories:
  - Linux
date: 2016-06-21 17:50:00
cover: /img/post-cover/21.jpg
---
Linux 提示 No space left on device 使用 du 排查原因

df 显示确实磁盘空间已满

这种情况下最快速的解决办法就是：



1.进入根目录
```
du -h --max-depth=1|grep G|sort -n  找不到结果还可以把 grep G 换成 grep M
```
此时得到
```
2.6G    ./opt
3.8G    ./var
5.2G    ./usr
5.5G    ./soft
18G     .
```

进入 /opt，再次执行 ```du -h --max-depth=1|grep G|sort -n``` 得知是 lampp 的日志占了 1.2G

经过多次处理，最终处理完，结果为：
```
1.1G    ./var
1.2G    ./opt
5.2G    ./usr
5.5G    ./soft
14G     .
 ```

瞬间减少了4G (/usr和/soft并未处理)

PS: 若报错，可去除 --max-depth 参数