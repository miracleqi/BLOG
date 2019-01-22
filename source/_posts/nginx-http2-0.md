title: nginx http2.0
author: MiracleQi-温柔魔君
tags:
  - nginx
  - http2.0
categories:
  - Linux
date: 2016-07-11 17:00:00
cover: /img/post-cover/25.jpg
---
nginx 有关 http2.0 的配置

# 背景

今天在 openresty 测试 http2.0

# 编译参数

首先需要编译时指定 v2 模块，```--with-http_v2_module```

# 配置

1. listen 指定 http2

2. ssl_protocols 需要包含 TLSv1.2

# 示例

```
server {
    listen 443 ssl http2;
    server_name _;

    ssl_certificate nginx.crt;
    ssl_certificate_key  nginx.key;
    ssl_protocols TLSv1.2;

    #或省略 ssl_protocols，默认为 sslv3 TLSv1 TLSv1.1 TLSv1.2
    #或 ssl_protocols TLSv1.1 TLSv1.2;
    #总之 ssl_protocols 要包含 TLSv1.2
}
```

如此在接入日志可以看到 http2.0 生效