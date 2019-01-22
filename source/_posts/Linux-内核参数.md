title: Linux 内核参数
author: MiracleQi-温柔魔君
tags:
  - kernel
categories:
  - Linux
date: 2016-12-30 13:11:00
cover: /img/post-cover/38.jpg
---
1. net.core.somaxconn

freebsd版本中对应的参数为 kern.ipc.somaxconn

作用：限制接收新 TCP 连接侦听队列的大小

关注点：nginx debug: accept() not ready (11: Resource temporarily unavailable)

详细信息：

对于一个TCP连接，Server与Client需要通过三次握手来建立网络连接.当三次握手成功后,

　　我们可以看到端口的状态由LISTEN转变为ESTABLISHED,接着这条链路上就可以开始传送数据了.

　　每一个处于监听(Listen)状态的端口,都有自己的监听队列.监听队列的长度,与如下两方面有关:

　　- somaxconn参数.

　　- 使用该端口的程序中listen()函数.

　　1. 关于somaxconn参数:

　　定义了系统中每一个端口最大的监听队列的长度,这是个全局的参数,默认值为1024,具体信息为:

　　Purpose:

　　Specifies the maximum listen backlog.

　　Values:

　　Default: 1024 connections

　　Range: 0 to MAXSHORT

　　Type: Connect

　　Diagnosis:

　　N/A

　　Tuning

　　Increase this parameter on busy Web servers to handle peak connection rates.

　　看下FREEBSD的解析：

　　限制了接收新 TCP 连接侦听队列的大小。对于一个经常处理新连接的高负载 web服务环境来说，默认的 128 太小了。大多数环境这个值建议增加到 1024 或者更多。 服务进程会自己限制侦听队列的大小(例如 sendmail(8) 或者 Apache)，常常在它们的配置文件中有设置队列大小的选项。大的侦听队列对防止拒绝服务 DoS 攻击也会有所帮助。

2. 其他：

net.core.wmem_max 最大 socket 写 buffer,可参考的优化值: 873200

3. tt

3. 1 arp_ignore : INTEGER

net.ipv4.conf.all.arp_ignore  

默认为0

定义对目标地址为本地IP的ARP询问不同的应答模式

0 - (默认值): 回应任何网络接口上对任何本地IP地址的arp查询请求（比如eth0=192.168.0.1/24,eth1=10.1.1.1/24,那么即使eth0收到来自10.1.1.2这样地址发起的对10.1.1.1 的arp查询也会回应--而原本这个请求该是出现在eth1上，也该有eth1回应的）

1 - 只回答目标IP地址是来访网络接口本地地址的ARP查询请求（比如eth0=192.168.0.1/24,eth1=10.1.1.1/24,那么即使eth0收到来自10.1.1.2这样地址发起的对192.168.0.1的查询会回答，而对10.1.1.1 的arp查询不会回应）

2 -只回答目标IP地址是来访网络接口本地地址的ARP查询请求,且来访IP必须在该网络接口的子网段内（比如eth0=192.168.0.1/24,eth1=10.1.1.1/24,eth1收到来自10.1.1.2这样地址发起的对192.168.0.1的查询不会回答，而对192.168.0.2发起的对192.168.0.1的arp查询会回应）

3 - 不回应该网络界面的arp请求，而只对设置的唯一和连接地址做出回应(do not reply for local addresses configured with scope host,only resolutions for global and link addresses are replied 翻译地似乎不好，这个我的去问问人)

4-7 - 保留未使用

8 -不回应所有（本地地址）的arp查询

all/ 和{interface}/ 下两者同时比较，取较大一个值生效.

3.2 arp_announce : INTEGER

默认为0

对网络接口上本地IP地址发出的ARP回应作出相应级别的限制:

确定不同程度的限制,宣布对来自本地源IP地址发出Arp请求的接口

0 - (默认) 在任意网络接口上的任何本地地址

1 -尽量避免不在该网络接口子网段的本地地址. 当发起ARP请求的源IP地址是被设置应该经由路由达到此网络接口的时候很有用.此时会检查来访IP是否为所有接口上的子网段内ip之一.如果改来访IP不属于各个网络接口上的子网段内,那么将采用级别2的方式来进行处理.

2 - 对查询目标使用最适当的本地地址.在此模式下将忽略这个IP数据包的源地址并尝试选择与能与该地址通信的本地地址.首要是选择所有的网络接口的子网中外出访问子网中包含该目标IP地址的本地地址. 如果没有合适的地址被发现,将选择当前的发送网络接口或其他的有可能接受到该ARP回应的网络接口来进行发送

all/ 和{interface}/ 下两者同时比较，取较大一个值生效.