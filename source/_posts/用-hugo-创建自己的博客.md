title: 用 hugo 创建自己的博客
author: MiracleQi-温柔魔君
tags:
  - hugo
categories:
  - BLOG
cover: /img/post-cover/11.jpg
date: 2019-01-04 14:27:00
---
如何用 hugo 搭建自己的博客

## 前言
前两天，hexo 打开了自建博客的道路。今天看到了 hugo，准备研究一下。   
hugo 是用 go 语言开发的，优势在于编译速度快。如果博客文章达到七八百篇，hexo 可能要几十分钟，但 hugo“眨眼”就完成。而且自学过 go 的基础语法，对 go 的项目挺感兴趣的。下面一起来看看，如何用 hugo 创建属于自己的博客。

参考自 [hugo 官网安装文档](https://gohugo.io/getting-started/installing/#source)

## 安装依赖
### Git
Git Bash 并不是必要的，但不太喜欢在 cmd 中操作各种命令，所以挑了这个比较好使的Git Bash, 我的是windows环境，所以下载 [windows版本](https://git-for-windows.github.io/) 并安装就可以了。

安装步骤：双击下载好的 exe 文件，一路 next 就好啦

安装好后，打开 gitbash，查看版本：
```
$ git version
git version 2.20.1.windows.1
```
然后你就可以在这里发挥你的聪明才智了
### go
直接去[官网](https://golang.org/dl/)选择对应版本即可（当前 hugo 要求 go 的最低版本为 1.11）。我这里选择的是 [go1.11.4.windows-amd64.msi](https://dl.google.com/go/go1.11.4.windows-amd64.msi)

安装步骤：双击下载好的 msi 文件，一路 next 就好啦

安装好后，打开 gitbash，查看版本：
```
$ go version
go version go1.11.4 windows/amd64
```
## 安装 hugo
用官网的安装方式，多次安装失败，最后直接上 github 找到对应版本下载安装。
### 成功安装
[github 找到对应版本](https://github.com/gohugoio/hugo/releases)。  
我这里选择 hugo_extended_0.53_Windows-64bit.zip  
1. 解压。下载后，解压缩至想要安装的目录（如 d:\hugo）  
2. PATH。再将此目录添加至 PATH （我的电脑→属性→高级->环境变量）  
3. 验证。打开新的 cmd 或 gitbash ，查看 hugo 版本信息

```
$ hugo.exe version
Hugo Static Site Generator v0.53/extended windows/amd64 BuildDate: unknown
```
至此，hugo 安装完毕！

### 失败安装
官方安装方式：
```
mkdir $HOME/src
cd $HOME/src
git clone https://github.com/gohugoio/hugo.git
cd hugo
go install --tags extended
```
难题：git 超时  
hugo 共有 63.13 MB，从 github 上 clone，速度只有 6 KB/s，下载到百分之十几就超时断开了(就算不断开，也要 3 个小时才完成)，即使用浏览器从github 上下载 zip 源文件，也是一样的结果。  
解决方法：借用 gitee  
先在gitee(开源中国)下新建仓库 hugo，然后从选择从已有仓库导入，hugo 代码 2 分钟就从 github 到了 gitee。然后从 gitee 上 git clone 即可，速度达到 386 KiB/s，2 分钟就搞定了。

不想在 gitee 创建仓库，可以从魔君这里 git clone。
```
cd d:    # 我在 D 盘安装的 hugo
git clone https://gitee.com/miracleqi/hugo.git
cd hugo
go install --tags extended
```
go install 这一步，各种异常（从 github 拉取各种依赖包，超时，认证失败等），放弃此安装方式。