title: 要想 lua 中调用 c 函数，c 文件如何修改？
author: MiracleQi-温柔魔君
tags:
  - lua
categories:
  - Linux
cover: /img/post-cover/17.jpg
date: 2016-02-25 09:27:00
---
## 背景

想要像 cjson，gd，libinjection 一样，代码是用 c 实现的，却在 openresty 的 lua 模块中被调用。  
下面以添加 ssdeep.so 为例，其中有 fuzzy_hash_buf 和 fuzzy_compare 两个接口函数。  
lua 版本为 5.1.4，openresty 版本为 1.9.7.1  

## 实践

### 添加头文件

```
//#include <lua.hpp>
#include <lauxlib.h>
//#include <lualib.h>
```
某些资料中显示要添加三个头，不过编译时显示lua.hpp找不到

我添加的 ssdeep 只需要 lauxlib.h 即可

### 修改接口函数

原有 fuzzy_hash_buf 函数如下:

```
char* fuzzy_hash_buf(const unsigned char *buf, uint32_t buf_len)
{
     ......
     return result;
}
```

现改为

```
int fuzzy_hash_buf_m(lua_State* L) {  //前期加上了extern "C"，但是会报错
    const unsigned char *buf = (const unsigned char *)lua_tostring(L, 1);
    uint32_t buf_len = (uint32_t)lua_tonumber(L, 2); 
    char   result[FUZZY_MAX_RESULT];
    .......
    lua_pushstring(L, result); //返回result值
    return 1; //返回结果的数量
}
```

注解:  
所有注册到 Lua 中的接口函数都具有相同的原型，该原型就是定义在 lua.h 中的 lua_CFunction:

```
typedef int (*lua_CFunction) (lua_State *L);
```

接口函数返回值表示返回结果的数量  
返回值通过 lua_pushstring 或者 lua_pushnumber 注入 L 中

### 接口函数列表

```
static LuaL_reg libs[] = { //开始为LuaL_Reg会报错，原因是lua版本的问题
    {"fuzzy_hash_buf", fuzzy_hash_buf},  
    {NULL, NULL} 
 
};
```

### 主函数

```
int luaopen_ssdeep(lua_State* L)  
{  
    const char* libName = "ssdeep";    
    luaL_register(L, libName, libs);   
    return 1; 
}
```

luaL_register 根据给定的名称 ("ssdeep") 创建（或复用）一个 table，并用数组 libs 中的信息填充这个 table。在 LuaL_register 返回时，会将这个 table 留在栈中。最后返回 1，表示将这个 table 返回给 lua。

### 编译及调用

C 模块完成后，必须将其链接到解释器。如果 Lua 解释器支持动态链接的话，那么最简便的方法就是使用动态链接机制。在这种情况中，必须将 C 代码编译成动态链接库，并将这个库放入 C 路径（LUA_CPATH）中。然后便可以用 require 从 Lua 中加载这个模块: require  "ssdeep" 会将动态库 ssdeep 链接到 Lua，并会寻找 luaopen_ssdeep 函数，将其注册为一个 Lua 函数，然后调用它以打开模块。

如果解释器不支持动态链接，那么就必须用新的模块来重新编译 Lua。此外，还需要以某种方式来告诉解释器，它应在打开一个新状态的同时打开这个模块。最简单的做法是，将 luaopen_ssdeep 加到 luaL_openlibs 会打开的标准库列表中，这个列表在文件 linit.c中。