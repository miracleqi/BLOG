title: WebStorm + TypeScript
author: MiracleQi-温柔魔君
tags:
  - webstorm
  - typescript
categories:
  - Windows
cover: /img/post-cover/14.jpg
date: 2018-07-15 23:06:00
---
WebStorm 安装 + 自动编译 TypeScript 

## 背景

最近公司用 TypeScript 开发前端。虽然我负责后台的工作，但也需为前端提供意见，为了不盲目提意见，因此来简单了解下 TypeScript  

## 安装配置环境

1. 安装 node.js 

    TypeScript 是在 node.js 的环境上，node.js 下载地址：https://nodejs.org/en/download/

2. 安装 TypeScript 

    使用 Node 的 npm 命令安装 TypeScript 编译器，在 cmd 界面里输入：
```
npm install typescript -g
```
可通过 tsc 命令查看是否安装成功
```
tsc -v
```
3. 安装 WebStrom

    WebStrom 官方下载地址： https://www.jetbrains.com/webstorm/

## WebStorm 自动编译 TypeScript

下载的 2018.1.5 版本的 WebStorm 已经提供自动编译的功能了，只是需要设置一下。  
在代码发生变动时，会有提示，是否要编译

![upload successful](/images/pasted-16.png)

设置自动编译：File -> setting，勾选 Recompile on changes  

![upload successful](/images/pasted-15.png)

自动编译功能设置完毕，下面就去尝试第一份代码吧！

## 测试

创建空项目：TypeScriptProgram

File -> New -> Project

![upload successful](/images/pasted-17.png)

右键此项目，创建 tsconfig.json File

![upload successful](/images/pasted-18.png)

添加 ts 文件

![upload successful](/images/pasted-19.png)

填写 ts 文件名

![upload successful](/images/pasted-20.png)

输入测试代码

```
function greeter(person) {
    return "Hello, " + person;
}

let user = "Jane User";

document.body.innerHTML = greeter(user);
```

![upload successful](/images/pasted-21.png)

保存后，自动生成相应的 js 文件

![upload successful](/images/pasted-22.png)

到此，用 WebStrom 开发 TypeScript 的环境已准备好了。