title: Microsoft Search 磁盘空间不足
author: MiracleQi-温柔魔君
tags:
  - Windows
categories:
  - 生活
cover: /img/post-cover/1.jpg
date: 2018-12-30 01:46:00
---
Microsoft Search 导致 C 盘空间不足.

## 前言

Windows Search的功能是为我们电脑中的文件、电子邮件和其他内容提供内容索引、属性缓存和搜索结果。Windows Search默认是开机启动的，它会利用计算机的空闲时间来建立索引，加大对计算机硬盘的使用率。  
最近家中电脑总是报 C 盘空间不足，利用软件清理空间时，发现 Microsoft Search 索引文件达到 73.7 GB，使用软件无法清理掉此文件（需管理员权限）  
此文件就在 C:\ProgramData\Microsoft\Search\Data\Applications\Windows\Windows.edb  
删除此文件，过一段时间又恢复，无法根治。
魔君为大家带来以下三种方案：
1. 关闭 search 服务，用 everything search 等第三方搜索软件替代
2. 缩小索引范围，我选择了此方案
3. 索引文件转移到其他磁盘

## 方案1：关闭 search 服务
1. 桌面右键“我的电脑”-选择“管理”
![upload successful](/images/pasted-5.png)
2. 在弹出的窗口中选择“服务”
![upload successful](/images/pasted-6.png)
3. 找到“windows search”并选择
![upload successful](/images/pasted-7.png)
4. 右键-属性，选择“禁用”即可停用服务
![upload successful](/images/pasted-8.png)

## 方案2：缩小索引范围
1. 在开始菜单的搜索栏直接搜索「索引选项」
![upload successful](/images/pasted-9.png)
或者打开控制面板，搜索“索引选项”  
2. 点击「修改」，去掉“用户”
![upload successful](/images/pasted-10.png)
一般只需要保留「开始」菜单即可  
视情况而定，我的台式机，为一万多项建立索引，就有 73.7 GB，去掉“用户”后，索引仅有 8MB。  
然鹅，我的笔记本，为 五万多项建立索引，仅有 200多MB。手动滑稽。
3. 点击「高级」，重建索引
![upload successful](/images/pasted-11.png)
到此，73.7GB 减少为 8MB，好开森！

## 方案3：索引文件转移至其他磁盘
虽然 SSD 空间少，但 HDD 空间多啊，经常用到 windows 索引的小伙伴，可以将索引文件转移至空间多的磁盘  
1. 在开始菜单的搜索栏直接搜索「索引选项」
![upload successful](/images/pasted-9.png)
或者打开控制面板，搜索“索引选项”
2. 点击「高级」，选择新位置
![upload successful](/images/pasted-12.png)
3. 重建索引
![upload successful](/images/pasted-11.png)
由于文件过大，建议有充足时间（如睡前）再重建  
或手动删除原 Windows.edb，windows 会在空闲时自动在新位置生成新的索引文件