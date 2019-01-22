title: license 授权机制
author: MiracleQi-温柔魔君
tags:
  - openssl
  - license
categories:
  - Linux
cover: /img/post-cover/30.jpg
date: 2016-09-09 11:22:00
---

# 1、创建私钥

```
openssl genrsa -out rsa_private_key.pem 1024   
//密钥长度，1024 觉得不够安全的话可以用 2048，但是代价也相应增大
```

# 2、创建公钥

```
openssl rsa -in private.pem -pubout -out rsa_public_key.pem
```

# 3、自签署根证书：(未制作）

```
//自签署，就是不通过 CA 认证中心自行进行证书签名，这里用是 x509
openssl x509 -req -in cert.csr -out public.der -outform der -signkey private.pem -days 3650 //10年有效
```

# 4、md5

```
防止他人篡改 public，因此获取 rsa_public_key.pem 文件的 MD5 值：
md5sum rsa_public_key.pem > rsa_public_key.md5
```

# 5、md5 校验

```
使用 MD5 校验文件(待校验文件和md5文件同一目录下)
md5sum -c rsa_public_key.md5
结果显示为 rsa_public_key.pem: OK
```

# 6、license.json

创建一个 license.json 文件，用于描述产品信息及用户权限信息

# 7、license.lic

用私钥对 license.json 加密生成 license.lic 许可证