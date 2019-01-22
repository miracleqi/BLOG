title: lua 的 string 函数引发的血案
author: MiracleQi-温柔魔君
tags:
  - lua
  - openresty
categories:
  - Linux
date: 2016-06-21 17:38:00
cover: /img/post-cover/20.jpg
---


## 背景

用 lua 的 string.gmatch 封装了一个字符串分割函数 string_split(str, sep)  
文件上传时，解析请求体，有时解析正常，有时卡住十几秒，并不报错，但解析失败

## 分析原因

代码如下：

```
function string_split(str, sep)
    if not str or not sep then
        return str          
    end          
    local result = {}          
    for m in (str..sep):gmatch("(.-)"..sep) do
        table.insert(result, m)
    end
    return result
end       
```

我们将 str 赋值为:

```
--r5Oj-KL4Wd0Tr7SVmdpM-W9FoBcIa7
Content-Disposition: form-data; name="file"; filename="test.txt"
Content-Type: image/jpeg

1 order by 1

--r5Oj-KL4Wd0Tr7SVmdpM-W9FoBcIa7--
```

sep 赋值为 

```
"--r5Oj-KL4Wd0Tr7SVmdpM-W9FoBcIa7"
```

我们想要得到的结果是

```
result[1] = "" --空字符串
result[2] = 'Content-Disposition: form-data; name="file"; filename="test.txt" \
             Content-Type: image/jpeg \
             \
             1 order by 1 \
             '
result[3] = "--" 
```

但真实结果是 gmatch 卡住十几秒，且匹配失败，返回 nil 

问题的真实原因在于 lua 的 string 操作有特殊字符，其中就包含了 '-'

'-'：是一种匹配模式，表示最短匹配 

要想正常使用那么就要用 '%' 转义 

每次转义都是额外的开销，并不是我们想要的，因此替换成了 ngx.re.find 执行

总结： 
1. 若我们已经清楚要操作的 sep 中未带有特殊字符，或我们能够转义的，可以用 lua的 string 操作，如在 init_by_lua 等未执行请求的阶段 
2. 若处理请求带进来的信息，是否有特殊字符不可控，转义开销太大（用 gsub 替换特殊字符），此时可用 ngx.re.find（此函数要求有 request object，所以请求进来了才可调用） 
3. string.gmatch，string.find 等 string 操作都有此类问题，其他正则函数也有自身特殊字符转换问题，以后要特殊关注，不然会被绕过，同时对性能有所影响。