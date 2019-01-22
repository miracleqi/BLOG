title: svn 游记
author: MiracleQi-温柔魔君
tags:
  - svn
  - patch
  - diff
categories:
  - Linux
date: 2017-03-28 15:59:00
cover: /img/post-cover/41.jpg
---

# 前言

公司之前用 svn 管理项目代码，我一直用的 windows 版本

近期想要搭建知识库云平台，需要在 linux 上使用 svn 管理代码，因此做些笔记

直接使用公司搭建好的 svn服务器

## 1. 客户端安装

```
yum install -y subversion   或

apt-get install subversion
```

# 2. 同步代码至本地

```
svn checkout https://192.168.xxx.xxx/xxx
```

# 3. 同步代码至最新版

```
svn update
```

# 4. 显示版本列表

```
svn log
```

# 5. 显示不同版本之间的不同

```
svn diff -r A           --显示当前版本 (working copy) 与 A 版本的不同
svn diff -r A:B         --显示 A 版本与 B 版本的不同
svn diff -r A  text.c   --显示当前版本 (working copy) 与 A 版本指定文件的不同
svn diff -r A:B text.c  --显示 A 版本与 B 版本指定文件的不同
```

# 6. 打 patch
```
svn diff 将结果输出到 test.patch 文件中
patch -p NUM < patch file
若 patch 文件更新的是 a/b/c.txt
则
  patch -p0 < test.patch   更新 a/b/c.txt 文件
  patch -p1 < test.patch   更新 b/c.txt 文件
  patch -p2 < test.patch   更新 c.txt 文件
```