title: '关于 PHP 默认 Expires: Thu, 19 Nov 1981... 的故事'
author: MiracleQi-温柔魔君
tags:
  - PHP
categories:
  - WEB
cover: /img/post-cover/28.jpg
date: 2016-08-15 09:53:00
---
PHP 与 Expires 1981 的故事

# 背景

最近看到 Expires 显示 1981 年，以为是攻城狮设置错误。问了后才发现，攻城狮并没有设置此字段。

为何 PHP 不设置 Expires 头的时候, 默认输出如下的缓存头呢？
```
Expires: Thu, 19 Nov 1981 08:52:00 GMT
```

# 开发者的生日

原因在于：

```
It's an attempt to disable caching.  
这是用于尝试禁用浏览器缓存 PHP 请求的
The date is the birthday of the developer Sascha Schumann who added the code.   
这个日期是这个块代码开发者 Sascha Schumann 的生日
File: session.c
Authors: Sascha Schumann < sascha@schumann.cx >
Andrei Zmievski < andrei@php.net >
```

```
// ...
CACHE_LIMITER_FUNC(private)
{
    ADD_HEADER("Expires: Thu, 19 Nov 1981 08:52:00 GMT");
    CACHE_LIMITER(private_no_expire)(TSRMLS_C);
}
```
以后看到 Expires: Thu, 19 Nov 1981 08:52:00 GMT 就可以认为这程序是 PHP 写的啦!

原文地址 https://segmentfault.com/a/1190000002475770