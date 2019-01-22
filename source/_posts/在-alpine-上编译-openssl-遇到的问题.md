title: 在 alpine 上编译 openssl 遇到的问题
author: MiracleQi-温柔魔君
tags:
  - openssl
  - openwaf
categories:
  - Linux
cover: /img/post-cover/15.jpg
date: 2019-01-08 10:38:00
---
alpine 上编译 openssl (v1.1.1) 遇到 ucontext 报错

## 前言
今天在 alpine 基础上编译 [openwaf](#https://github.com/titansec/openwaf)，编到 openssl 时，报 ucontext 相关错误。

## ucontext 报错
编译 openssl
```
# ./config
# make && make install
```
错误描述：
```
./libcrypto.so: warning: gethostbyname is obsolescent, use getnameinfo() instead.
./libcrypto.so: undefined reference to getcontext' 
./libcrypto.so: undefined reference to setcontext'
./libcrypto.so: undefined reference to `makecontext'
```
## 解决方法
没有使用 no-async 参数，加上之后就可以了。
```
# ./config no-async
# make && make install
```
no-async: 交叉编译工具链没有提供GNU C的ucontext库

PS：[openssl 相关 issue](#https://github.com/openssl/openssl/issues/1607)
## 扩展
openssl 交叉编译过程中会遇到很多问题，这里罗列其他几个参数：
```
no-asm:	在交叉编译过程中不使用汇编代码代码加速编译过程.原因是它的汇编代码是对arm格式不支持的。
shared: 生成动态连接库。
no-async: 交叉编译工具链没有提供GNU C的ucontext库
-–prefix=: 安装路径，编译完成install后将有bin，lib，include等文件夹
-–cross-compile-prefix=: 交叉编译工具
```
