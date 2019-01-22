title: test nginx lua
author: MiracleQi-温柔魔君
tags:
  - nginx
  - lua
  - openresty
categories:
  - Linux
date: 2016-12-20 09:38:00
cover: /img/post-cover/37.jpg
---
1. 安装test nginx
```
git clone https://github.com/openresty/test-nginx.git
cd test-nginx
perl Makefile.PL
make && make install
PATH=/usr/local/openresty/nginx/sbin/nginx:$PATH
```

2. 编写测试文件

 此处暂时忽略

3. 进行测试

	```
cd test-nginx
prove -Ilib -r ../t
```

PS: 
1. 调用 prove 进行测试必须要进入 test-nginx 目录下，不然会报错（找不到TEST/Base.pm），目前还没找到解决方式