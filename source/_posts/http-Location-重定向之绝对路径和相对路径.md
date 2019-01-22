title: http Location 重定向之绝对路径和相对路径
author: MiracleQi-温柔魔君
tags:
  - Location
  - http
categories:
  - WEB
date: 2017-01-11 14:27:00
cover: /img/post-cover/39.jpg
---

# 背景

今天同事问我，访问 ip:port/dawv/dawv.html 返回 302，Location 值是 login.html  
为何跳转到 ip:port/dawv/login.html，而不是 ip:port/login.html

# 三种 Location

其实很简单  
如：访问 ip:port/uri/last

1. 绝对路径

 返回的 Location 是绝对路径 "/absolutely_uri"，就和 ip:port 拼接，跳转至ip:port/absolutely_uri

2. 相对路径

 返回的 Location 是相对路径 "relative_uri"，跳转至 ip:port/uri/relative_uri

3. 完整 URL

 返回的Location 是完整的 URL，直接跳转至此 URL （如：http://www.ffamily.cn） 

看到大部分书籍对于 Location 仅仅描述为“重定向的 URI”，没有过多的描述，因此记录，供他人参考