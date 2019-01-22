title: influxdb 注意事项
author: MiracleQi-温柔魔君
tags:
  - influxdb
categories:
  - influxdata
cover: /img/post-cover/29.jpg
date: 2016-08-30 11:35:00
---
剖析 influxdb 日志记录失败原因

# 前言

最近公司想让引擎日志通过 udp 直接发送至 influxdb  
influxdb [使用文档](#https://docs.influxdata.com/influxdb)在此，不详细描述了  
期间遇到几个需要注意的事项，会使日志记录失败。

# 同一时间仅有一条日志记录成功

中间遇到一个坑，一条日志中多个 points，结果日志入库后，只有最后一个 point，

多次测试后得出结论：

一条日志多个 points，给的时间戳都是一致的，必须保证 tags 中不一致才可都入库

失败案例1：

    seclog fileds=1 1472525632000000000

    seclog fileds=2 1472525632000000000

失败案例2:

    seclog,tags=1 fileds=1 1472525632000000000

    seclog,tags=1 fileds=2 1472525632000000000

成功案例:

    seclog,tags=1 fileds=1 1472525632000000000​

    seclog,tags=2 fileds=2 1472525632000000000

ps: 默认时间戳单位为"纳秒"


# 保持值的类型不变

还遇到一个问题：值的类型

如果第一条日志中，a=1，那么 a 的值就为数字类型

若之后日志中，a="b",那么会提示 a 的类型是字符串，但已经存在数字类型的 a，并且日志入库失败