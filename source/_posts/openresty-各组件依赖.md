title: openresty 各组件依赖
author: MiracleQi-温柔魔君
tags:
  - openresty
  - nginx
  - modsecurity
  - gd
categories:
  - Linux
date: 2016-06-17 10:45:00
cover: /img/post-cover/18.jpg
---
openresty 各组件(modsecurity、zlib、openssl、pcre、lua、gd、tools等)安装。

## openresty

https://openresty.org/download/openresty-1.9.15.1.tar.gz

目前最新版本 1.9.15.1 支持动态加载模块

## nginx 依赖

### openssl -- ssl依赖

http://www.openssl.org/source/openssl-1.0.2h.tar.gz  

目前最新版本 1.0.2h

```
./config  
make && make install
openssl version      # 验证版本
```

### pcre -- 正则依赖

http://sourceforge.net/projects/pcre/files/pcre/8.38/pcre-8.38.tar.gz  

目前最新版本是 8.38

```
./configure --enable-jit  
make && make isntall
pcre-config --version      # 验证版本
```

### zlib -- 压缩依赖

http://zlib.net/zlib-1.2.8.tar.gz

最新版本是 1.2.8，13 年更新

```
./configure  
make && make install
```

如果没有达到目的，还可以

```
apt-get install zlib1g zlib1g-dev
```

## 上传

### ssdeep

暂时用不到，已改成 lua_ssdeep

### clamav

```
apt-get install clamav
```

### lua_gd

#### gd

https://bitbucket.org/libgd/gd-libgd/downloads

手动下载libgd-2.1.1

ps:尝试apt-get install libgd3 但编译时提示找不到gd.h

```
./configure
make && make install
```

#### jpeg

http://www.ijg.org/files/

下载最新的 jpegsrc.v9b.tar.gz

```
./configure
make && make install
```

这里直接 apt-get install libjpeg-dev

#### lpng  & freetype

http://jaist.dl.sourceforge.net/project/libpng/

这里下载 libpng16/1.6.16/libpng-1.6.16.tar.gz

```
./configure
make && make install
```

http://ftp.twaren.net/Unix/NonGNU/freetype/

这里下载 freetype-2.5.5.tar.gz

```
./configure
make && make install
```

或者直接 apt-get install libfreetype6-dev 会自动安装依赖 libpng12-dev

#### libtiff

```
apt-get install libtiff5-dev
```

实测 lua_gd 处理 tiff 图片无效，因此不需安装

#### libgif

```
apt-get install libgif-dev
```

gd 对 gif 处理并不友好，因此需要处理 gif 图片，推荐 imagick

#### 其他

```
apt-get install libvpx-dev
apt-get install libxpm-dev
apt-get install libfontconfig1-dev

我这里都用不到，就不安装了
```

## libinjection

编译 libinjection 需要 swig 支持

```
apt-get install swig
```

## modsecurity

### apxs

```
apt-get install apache2-dev (apxs)
```

### pcre

同上

### apr

http://apr.apache.org/download.cgi  下载 apr 与 apr-util

#### apr-1.5.2  

```
 ./configure   
make && make install
```

#### apr-util-1.5.4

```
./configure --with-apr=/soft/apr-1.5.2 
make && make install
```

### ./autogen.sh 依赖

 libtoolize autoreconf autoheader automake autoconf 均为 not found

#### libtool

ftp://ftp.gnu.org/gnu/libtool/

本次下载libtool-2.4.6.tar.gz

```
./configure
make && make install
```
#### automake

ftp://ftp.gnu.org/gnu/automake/

本次下载automake-1.9.tar.gz

```
./configure
make && make install
```

#### autoconf

包含 autoheader、autoreconf 与 autom4te 等

http://ftp.gnu.org/gnu/autoconf/

本次下载autoconf-2.69.tar.gz

```
./configure
make && make install
```

#### yajl

http://lloyd.github.io/yajl/

本次下载 yajl-2.1.0.tar.gz

```
./configure
make && make install
```
依赖 cmake

https://cmake.org/download/

本次下载 cmake-3.6.0-rc2.tar.gz

```
./configure
make &＆ make install
```

#### lua5.1

http://www.lua.org/ftp/

当前最新版本 5.3.3，本次下载 5.1

```
make linux && make install
```

若提示找不到readline头文件
```
apt-get install libreadline6 libreadline6-dev
```

若提示找不到-lncurses

```
apt-get install libncurses5 libncurses5-dev
```

ps:若需要重编 lua，要先 make clean

#### libxml2

```
apt-get install libxml2 libxml2-dev
```

ps: ./autogen.sh 时，提示 PKG_PROG_PKG_CONFIG 找不到

在确认 pkg-config 安装，且有 pkg.m4 后意识到系统有两套 automake

终端输入aclocal --print-ac-dir

得到 /usr/share/aclocal

但是 libtool.m4 却在 /usr/local/share/aclocal

如果无法去掉“非标准的”automake，只需

```
ACLOCAL_PATH=/usr/share/aclocal ./autogen.sh
```

或者 
```
export ACLOCAL_PATH=/usr/share/aclocal
./autogen.sh
```

但需要的文件可能分别在两个路径下，

因此我先将 /usr/local/share/aclocal/ 下文件拷贝到 /usr/share/aclocal 下

[ACLOCAL参考文档](#http://www.gnu.org/software/automake/manual/html_node/Macro-Search-Path.html#Macro-Search-Path)

#### 编译 modsecurity

https://github.com/SpiderLabs/ModSecurity/tree/nginx_refactoring

最新版本 2.9.1

```
./configure --with-apxs=/usr/bin/apxs  --with-pcre=/usr/local/bin/pcre-config --enable-pcre-match-limit=1500 --enable-pcre-match-limit-recursion=1500 --enable-pcre-study  --enable-twaf-var  --enable-pcre-jit  --enable-lua-cache --enable-standalone-module  --with-apr=/usr/local/apr  --with-lua --with-lua=/usr/local/lua​  with-apu=/usr/bin/apu-1-config --disable-mlogc
```

## openresty tools

### nginx-systemtap-toolkit & stapxx

https://github.com/openresty/openresty-systemtap-toolkit

https://github.com/openresty/stapxx

#### systemtap

systemtap 要求版本在 2.1 以上

https://sourceware.org/systemtap/ftp/releases/systemtap-2.6.tar.gz

systemtap [安装详细](http://openresty.org/en/build-systemtap.html)（包括依赖）

1. kernel-debuginfo

  https://packages.debian.org/jessie/amd64/linux-image-3.16.0-4-amd64-dbg/download  
 或：
 ```
 apt-get install linux-image-$(uname -r)-dbg
 ```
2. kernel-devel

```
apt-get install linux-headers-$(uname -r)
```

#### utrace

Linux kernels 版本低于 3.5​，则需打utrace patch

#### perl

perl 要求版本在 5.6.1 以上

#### kernel-debuginfo & kernel-devel

要对应 kernel 版本

### FlameGraph

http://dtrace.org/blogs/brendan/2011/12/16/flame-graphs/​

或者

https://github.com/brendangregg/FlameGraph

制作火焰图

## redis

http://redis.io/

目前最新版本为3.2.1

```
make
./src/redis-server redis.conf
```
