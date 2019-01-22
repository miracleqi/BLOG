title: ngx.re.match 正则表达式长度限制
author: MiracleQi-温柔魔君
tags:
  - nginx
  - regex
categories:
  - Linux
cover: /img/post-cover/35.jpg
date: 2016-11-10 13:58:00
---
captures, err = ngx.re.match(subject, regex, options?, ctx?, res_table?)

今天用 ngx.re.match，结果返回nil，查看err发现，regex正则表达式过长导致的

那么最长是多少呢？经过测试发现，当regex最大可为30947 字节，再大返回就是nil了

因此，regex最好控制在30720（30k）以内即可