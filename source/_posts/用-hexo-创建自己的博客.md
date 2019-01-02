---
title: 用 hexo 创建自己的博客
tags:
  - hexo
categories:
  - BLOG
author: MiracleQi-温柔魔君
date: 2018-12-29 16:41:00
cover: /img/post-cover/0.jpg
---
用 hexo 创建属于自己的博客  

## 前言
想要创建自己的博客由来已久。之前偶尔写点东西，记录在了新浪和w3cschool。  
随着需要记录的文章越来越多，下定决心搭建一个属于自己的博客。现在大家用 hexo 比较多，也比较方便，并且能使用的主题也很多，所以魔君在这里记录 hexo 的搭建历程。  
PS：魔君对前端（甚至html）都是一窍不通的。。。

本篇为从零开始的基础篇，感谢[visugar](http://visugar.com/2017/05/04/20170504SetUpHexoBlog/)的分享

### 1. 安装 Git Bash
Git Bash 并不是必要的，但不太喜欢在cmd中操作各种命令，所以挑了这个比较好使的Git Bash, 我的是windows环境，所以下载[windows版本](https://git-for-windows.github.io/)并安装就可以了。

安装步骤：双击下载好的 exe 文件，一路 next 就好啦

安装好后，打开 gitbash，查看版本：
```
$ git version
git version 2.20.1.windows.1
```
然后你就可以在这里发挥你的聪明才智了
### 2. 安装 NodeJs
Hexo 是基于 [nodeJS](https://nodejs.org/en/) 环境的静态博客，里面的 npm 工具很有用啊，所以还是老老实实把这玩意儿装了吧。

安装步骤：反正下载好 msi 文件后，双击打开安装，也是一路  next，不过在Custom Setup 这一步记得选 Add to PATH ,这样你就不用自己去配置电脑上环境变量了，装完在按 win + r 快捷键调出运行，然后输入 cmd 确定，在 cmd 中输入 path 可以看到你的 node 是否配置在里面（环境变量），没有的话你就自由发挥吧。

查看版本：

```
$ node -v
v8.11.3
```
又到自由发挥的时候了
### 3. 安装 Hexo
看到这么多安装，千万不要紧张，一定要稳住，别怕，因为后面的东西都是在 gitbash 中用 npm 工具安装就好了。

先创建一个文件夹（用来存放所有blog的东西），然后 cd 到该文件夹下。

安装 hexo:
```
$ npm i -g hexo
```
hexo 初始化:
```
$ hexo init
```

初始化完成之后打开所在的文件夹可以看到以下文件：

![upload successful](/images/pasted-0.png)
解释一下：

node_modules：是依赖包  
public：存放的是生成的页面  
scaffolds：命令生成文章等的模板  
source：用命令创建的各种文章  
themes：主题  
_config.yml：整个博客的配置  
db.json：source解析所得到的  
package.json：项目所需模块项目的配置信息  

做好这些前置工作之后接下来的就是各种配配配置了。

### 4. 生成 SSH 并添加到 github
将博客部署在自己的服务器（如ECS），可跳过此步骤。这里我将博客部署在 github pages。没账号的创建 github 账号，有账号的看下面。

创建一个 repo，名称为 yourname.github.io, 其中 yourname 是你的 github 名称，按照这个规则创建才有用，如下：
![upload successful](/images/pasted-1.png)
如我的名称为 miracleqi，创建的 repo 为 miracle.github.io

回到 gitbash 中，配置 github 账户信息（YourName 和 YourEail 都替换成你自己的）：
```
$ git config --global user.name "username"
$ git config --global user.email "email"
```
查看刚刚配置的账户信息是否正确
```
$ git config user.name
$ git config user.email
```
创建SSH
```
$ ssh-keygen -t rsa -C "youremail@example.com
$ cd ~/.ssh
```
将 .ssh 目录下的 id_rsa.pub 文件内容添加至 github 中
![upload successful](/images/pasted-2.png)
在gitbash中验证是否添加成功：
```
$ ssh -T git@github.com
Hi miracleqi! You've successfully authenticated, but GitHub does not provide shell access.
```
完成下一步你就成功啦！
### 5. 部署项目
用编辑器打开你的 blog 项目，修改_config.yml 文件的一些配置(冒号之后都是有一个半角空格的)：
```
deploy:
  type: git
  repo: https://github.com/YourgithubName/YourgithubName.github.io.git
  branch: master
```
第一次启动服务需要安装 hexo-server
```
npm i hexo-server
```
进入你的blog目录后，分别执行以下命令：
```
$ hexo clean
$ hexo generate
$ hexo server
```
打开浏览器输入：http://localhost:4000  
接着你就可以遇见天使的微笑了~
### 6. 上传到 Github
先安装一波：hexo-deployer-git，这样才能将你写好的文章部署到 github 服务器上并让别人浏览到
```
npm install hexo-deployer-git --save
```
执行命令(建议每次都按照如下步骤部署)：

```
hexo clean
hexo generate
hexo deploy
```
注意deploy的过程中要输入你的 username 及 passward (不是每次都需输入)

在浏览器中输入 https://yourgithubname.github.io 就可以看到你的个人博客啦，是不是很兴奋！

欢迎查看我的博客 [https://miracleqi.github.io](https://miracleqi.github.io)

感觉 gitbash 中东西太多的时候输入 clear 命令清空。
### 7. 绑定个人域名
不想绑定的自行忽略

第一步购买域名：随便在哪个网站买一个就好了，魔君是在阿里云购买的ffamily.cn。

第二步添加 CNAME：在项目的source文件夹下新建一个名为 CNAME 的文件，在里面添加你购买的域名，比如我添加的是www.ffamily.cn，只能添加一个地址。
![upload successful](/images/pasted-3.png)
第三步：到DNS中添加一条记录：
![upload successful](/images/pasted-4.png)
记录类型为 CNAME，记录值为 github pages 域名

接着再次部署一次
```
hexo clean
hexo generate
hexo deploy
```
用你购买的域名打开，就可以看到你的博客啦~  
PS：DNS 变更可能要10分钟以上，耐心等待


