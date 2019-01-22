title: nginx add dynamic module
author: MiracleQi-温柔魔君
tags:
  - nginx
  - openresty
categories:
  - WEB SERVER
date: 2016-06-21 09:56:00
cover: /img/post-cover/19.jpg
---
nginx 动态添加模块

## 前言

1.9.11 版本前的 nginx 增加一个第三方模块，需要重新编译源代码，所有的模块都是用静态链接的形式组织起来的。而 Tengine 可以实现运行时动态加载模块，而不用每次都要重新编译Tengine。  
Nginx 官方发布的 Nginx-1.9.11 版本，增加了此[功能](#http://nginx.org/en/CHANGES)。  
openresty 的 1.9.15.1 版本增加了此[功能](#http://openresty.org/cn/changelog-1009015.html)。

今天我将代码也更新到了 1.9.15.1 版本，试着动态加载自己编写的第三方模块

参考官方文档：

[Converting Static Modules to Dynamic Modules](#https://www.nginx.com/resources/wiki/extending/converting)

[Old Config Shell File](#https://www.nginx.com/resources/wiki/extending/old_config)

[New Config Shell File](#https://www.nginx.com/resources/wiki/extending/new_config)

## Converting a config file

### old-config

```
ngx_addon_name=ngx_http_xxx_filter_module
HTTP_AUX_FILTER_MODULES="$HTTP_AUX_FILTER_MODULES\              
                    ngx_http_xxx_filter_module"
NGX_ADDON_SRCS="$NGX_ADDON_SRCS \
                   $ngx_addon_dir/ngx_http_xxx_filter_module.c"
```

### new-config

要考虑nginx版本，也要考虑是否为动态模块

```
ngx_addon_name=ngx_http_xxx_filter_module
#nginx version >= 1.9.11
if test -n "$ngx_module_link"; then   
    if [ $ngx_module_link = ADDON ] ; then          
        ngx_module_type=HTTP_AUX_FILTER   
    fi       
    ngx_module_name=ngx_http_xxx_filter_module    
 ngx_module_srcs="$ngx_addon_dir/ngx_http_xxx_filter_module.c"       
    . auto/module  
#nginx version < 1.9.11
else   
    HTTP_AUX_FILTER_MODULES="$HTTP_AUX_FILTER_MODULES \               
                     ngx_http_xxx_filter_module"    
     NGX_ADDON_SRCS="$NGX_ADDON_SRCS \           
                    $ngx_addon_dir/ngx_http_xxx_filter_module.c"
fi
```
## Compiling a Dynamic Module

A new configure option has been created to add a module as a dynamic module. Instead of using ```--add-module``` you use ```--add-dynamic-module```. For example:

```
./configure --add-dynamic-module=/opt/source/ngx_http_xxx_filter_module/
```

Modules are compiled along with NGINX by running the ```make``` command. Alternatively you can ask NGINX to just build the modules by doing:

```
$ make -f objs/Makefile modules
```

With NGINX 1.9.13 the following is another way of doing this:

```
$ make modules
```
    
## Loading a Dynamic Module

Modules can be loaded into NGINX with the new ```load_module``` directive.

For example:(main级别)
```
load_module modules/ngx_http_xxx_filter_module.so;
```

ps: 虽说是 main 级别的，但是要其他块之上，如：

```
    user root root;
    worker_processes 2;
    pid /var/run/nginx.pid;

    load_module modules/ngx_http_xxx_filter_module.so;

    events {
        ...​
    }​
    http {
        ...​
    }​
```
若 load_module 用在 events 与 http 之间，则会提示：

```
"load_module" directive is specified too late
```

## note

1. There is a hard limit of 128 dynamic modules that can be loaded at one time, as defined by NGX_MAX_DYNAMIC_MODULES in the NGINX source. This hard limit can be increased by editing this constant.

2. 新旧模块的兼容

 上面已经提到了新旧模块编译脚本的兼容

 同时也要考虑 c 语言层面的兼容，要关注动态模块对于 Nginx 框架的调整

 例如之前凡是用到全局变量 ngx_modules 的地方，要修改为 cycle->modules
```
    #if defined(nginx_version) && nginx_version >= 1009011
        modules = cf->cycle->modules;
    #else
        modules = ngx_modules;
    #endif
```