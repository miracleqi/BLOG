title: 工具安装 Intellij Idea + GO SDK + GO Plugin
author: MiracleQi-温柔魔君
tags:
  - idea
  - go
categories:
  - Windows
date: 2018-07-02 19:13:00
cover: /img/post-cover/54.jpg
---
# 一、 安装 Intellij Idea

我选择的是 [Ultimate](#http://www.jetbrains.com/idea/download/#section=windows) 版本，[永久激活可参考我之前的文档](#https://www.w3cschool.cn/project/notebook/notebook-q6v82rym.html)

# 二、 安装 GO
1. 下载 GO  
 可从 [GoLang 中国](#https://www.golangtc.com/download)下载 GO SDK，我这里下载的是 [go1.9.2.windows-amd64](#https://www.golangtc.com/download) 版本（1.9.2）

2. 安装  
 解压至无中文无空格的目录，比如 `D:\go`

3. 配置环境变量  
 依次点击，我的电脑，属性，高级系统设置，环境变量，系统变量  
 点击新建按钮，变量名输入 `GOROOT`，变量值输入 `D:\go`
 找到 `PATH` 变量，在末尾加入 `;%GOROOT%\bin;` 注意分号（Win10不需加分号）
 
4. 验证  
 按组合键，`win+R`，输入`cmd`，按回车，即可打开命令行窗口  
 在命令行窗口输入 `go version` 即可看到相应信息
![upload successful](/images/pasted-37.png)
到此，GO 安装成功！

# 三、 安装 GO Plugin

![upload successful](/images/pasted-38.png)

![upload successful](/images/pasted-39.png)

如上两张图

1. 打开 Intellij Idea，选择右下角的 configure -> plugins （已进入 Intellij Idea，可通过 File -> setting -> plugins 安装插件）

2. 输入 go，即可安装（我这里已安装）

在线安装后，会提示重启 Intellij Idea 

# 四、关联 GO SDK

![upload successful](/images/pasted-40.png)

![upload successful](/images/pasted-41.png)

![upload successful](/images/pasted-42.png)

如上三张图

1. 打开 Intellij Idea，选择右下角的 configure -> setting （已进入 Intellij Idea，可通过 File -> setting 进行设置）

2. 安装好 GO plugin 插件，即可在 Languages & Frameworks 中找到 Go

3. 配置 GOROOT，如图选择 SDK

4. 配置 GOPATH，如图选择 go 的 src 目录 （也可在 windows 环境变量设置 GOPATH）

PS：别忘了右下角的 Apply 哦！

至此，Intellij Idea + GO SDK + GO Plugin 全部安装完毕！

误区：

当初安装 GO SDK 时，按照他人的方式，需要在 File -> Project Structure 中添加 SDK，如下图

图丢了。。。

但无论如何安装，这里总是没有 Go SDK 选项。

经证明，只要在 Intellij Idea 中设置过 GOROOT 和 GOPATH 即可。

# 四、 测试

1. 新建项目/工程  
 Create New Project 或 File -> New -> Project
![upload successful](/images/pasted-43.png)
![upload successful](/images/pasted-44.png)
2. 新建 Module  
 File -> New -> Module
![upload successful](/images/pasted-45.png)
![upload successful](/images/pasted-46.png)
![upload successful](/images/pasted-47.png)
![upload successful](/images/pasted-48.png)
![upload successful](/images/pasted-49.png)
3. 创建 go 文件
![upload successful](/images/pasted-50.png)
![upload successful](/images/pasted-51.png)
4. 编译测试
![upload successful](/images/pasted-52.png)
![upload successful](/images/pasted-53.png)

运行结果正确！  
误区：（没用过开发工具，你们尽情的嘲笑吧）  
第一次照葫芦画瓢写代码时，输入 import "fmt"，鼠标定位至其他行，代码会消失。  
代码中用到 fmt，会自动添加 import "fmt" 代码（有开发工具就是好）