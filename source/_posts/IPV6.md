title: IPV6
author: MiracleQi-温柔魔君
tags:
  - IPV6
categories:
  - 网络
date: 2018-06-19 15:48:00
cover: /img/post-cover/46.jpg
---
# 前言
2017 年 11 月 26 日，中共中央办公厅、国务院办公厅印发了《推进互联网协议第六版（IPv6）规模部署行动计划》

# 现状
据 APNIC Labs 提供的全球 IPv6 用户数（估计）及 IPv6 用户普及率的数据，截至 2017 年 11 月，全球 IPv6 用户数排名前十位的国家/地区，依次是印度、美国、德国、日本、巴西、英国、法国、加拿大、比利时、越南等，中国 IPv6 用户数排在第 13 位，如表 1 所示。而全球 IPv6 用户普及率排在前十位的国家/地区，依次是比利时、印度、德国、美国、希腊、瑞士、卢森堡、英国、葡萄牙、日本等，中国 IPv6 用户普及率仅有 0.38%，排在第 67 位。

<center> 表1 全球IPv6用户数（估值）排名 </center>
![upload successful](/images/pasted-26.png)

<center> 表2 Ipv6域名情况 </center>

Ipv6域名状态 | 政府部门 | 其他行业
---- | ---- | ----
可使用 | 41% | 2%
过渡中 | 43% | 54%
不可使用 | 16% |  44%

# 目标
《行动计划》指出，将用 5 到 10 年时间，形成下一代互联网自主技术体系和产业生态，建成全球最大规模的 IPv6 商业应用网络，实现下一代互联网在经济社会各领域深度融合应用，成为全球下一代互联网发展的重要主导力量。

1．到 2018 年末，市场驱动的良性发展环境基本形成，IPv6 活跃用户数达到 2 亿，在互联网用户中的占比不低于 20%，并在以下领域全面支持 IPv6：国内用户量排名前 50 位的商业网站及应用，省部级以上政府和中央企业外网网站系统，中央和省级新闻及广播电视媒体网站系统，工业互联网等新兴领域的网络与应用；域名托管服务企业、顶级域运营机构、域名注册服务机构的域名服务器，超大型互联网数据中心（IDC），排名前5位的内容分发网络（CDN），排名前10位云服务平台的50%云产品；互联网骨干网、骨干网网间互联体系、城域网和接入网，广电骨干网，LTE网络及业务，新增网络设备、固定网络终端、移动终端。

 2．到 2020 年末，市场驱动的良性发展环境日臻完善，IPv6 活跃用户数超过 5 亿，在互联网用户中的占比超过 50%，新增网络地址不再使用私有 IPv4 地址，并在以下领域全面支持 IPv6：国内用户量排名前 100 位的商业网站及应用，市地级以上政府外网网站系统，市地级以上新闻及广播电视媒体网站系统；大型互联网数据中心，排名前 10 位的内容分发网络，排名前 10 位云服务平台的全部云产品；广电网络，5G 网络及业务，各类新增移动和固定终端，国际出入口。

 3．到 2025 年末，我国 IPv6 网络规模、用户规模、流量规模位居世界第一位，网络、应用、终端全面支持 IPv6，全面完成向下一代互联网的平滑演进升级，形成全球领先的下一代互联网技术产业体系。
 
# 总结

按通知要求，2018 年是涉及工信部相关 IPV6 任务的重要时间节点。我司生产的安全防护产品也要全面支持 IPV6。因此，在这里归纳 IPV6 开发中遇到的问题及解决方案。

# 认识IPv6地址

IPv4 地址是类似 A.B.C.D 的格式，它是32位，用 . 分成四段，用10进制表示；而IPv6地址类似 X:X:X:X:X:X:X:X 的格式，它是128位的，用 : 分成 8 段，用 16 进制表示；可见，IPv6 地址空间相对于 IPv4 地址有了极大的扩充。

RFC2373 中详细定义了 IPv6 地址，按照定义，一个完整的IPv6地址的表示法：xxxx:xxxx:xxxx:xxxx:xxxx:xxxx:xxxx:xxxx

例如： 2001:0000: 1F 1F :0000:0000:0100: 11A 0:ADDF

为了简化其表示法， rfc2373 提出每段中前面的 0 可以省略，连续的 0 可省略为 ::，但只能出现一次。例如：

```
1080:0:0:0:8:800: 200C : 417A 可简写为 1080::8:800: 200C : 417A
FF01:0:0:0:0:0:0:101 可简写为 FF01::101
0:0:0:0:0:0:0:1 可简写为 ::1
0:0:0:0:0:0:0:0 可简写为 ::
```

类似于 IPv4中的 CDIR 表示法，IPv6 用前缀来表示网络地址空间，比如：

2001:251:e000::/48 表示前缀为48位的地址空间，其后的80位可分配给网络中的主机，共有2的80次方个地址。

为了使您更好的理解 IPv6，在这里给出一个表格，以比较IPv4和IPv6地址对应关系和区别。

IPv4地址 | IPv6地址
---- | ----
组播地址（ 224.0.0.0/4）| IPv6组播地址（FF00::/8）
广播地址 | 无，只有任播（ anycast）地址
未指定地址为 0.0.0 .0 | 未指定地址为 ::
回路地址为 127.0.0.1 | 回路地址为 ::1
公用 IP地址 | 可汇聚全球单播地址
私有地址（ 10.0.0 .0/8、172.16.0.0/12和192.168.0.0/16） | 本地站点地址（ FEC0::/48）
Microsoft自动专用IP寻址自动配置的地址（169.254.0.0/16） | 本地链路地址（ FE80::/64）
表达方式：点分十进制 |表达方式：冒号十六进制式（取消前置零、零压缩）
子网掩码表示：以点阵十进制表示法或前缀长度表示法（ CIDR） | 子网掩码表示：仅使用前缀长度表示法（ CIDR）

# IPv6地址作用域和地址分类

*  IPv6 地址指定给接口，一个接口可以指定多个地址。
*  IPv6 地址有作用域：  
   link local地址 本链路有效  
   site local地址 本区域（站点）内有效，一个site通常是个校园网  
   global地址 全球有效，即可汇聚全球单播地址
*  IPv6 地址分类：  
	unicast 单播（单点传送）地址  
	multicast 组播（多点传送）地址  
	anycast 任播（任意点传送）地址  

IPv6 没有定义广播地址，其功能由组播地址替代

# 常见的IPv6地址及其前缀
*  ::/128   即 0:0:0:0:0:0:0:0，只能作为尚未获得正式地址的主机的源地址，不能作为目的地址，不能分配给真实的网络接口。
*  ::1/128 即 0:0:0:0:0:0:0:1，回环地址，相当于IPv4中的localhost（127.0.0.1），ping locahost 可得到此地址。
*  2001::/16  全球可聚合地址，由 IANA 按地域和ISP进行分配，是最常用的IPv6地址，属于单播地址。
*  2002::/16  6 to 4 地址，用于 6to4 自动构造隧道技术的地址，属于单播地址。
*  3ffe::/16   早期开始的 IPv6 6bone 试验网 地址，属于单播地址。
*  fe80::/10   本地链路地址，用于单一链路，适用于自动配置、邻机发现等，路由器不转发以fe80开头的地址。
*  ff00::/8  组播地址。
*  ::A.B.C.D  兼容 IPv4 的 IPv6 地址，其中 <A.B.C.D> 代表 IPv4 地址。自动将 IPv6 包以隧道方式在 IPv4 网络中传送的 IPv4/IPv6 节点将使用这些地址。
*  ::FFFF:A.B.C.D 是 IPv4 映射过来的 IPv6 地址，其中 <A.B.C.D> 代表 IPv4 地址，例如 ::ffff:202.120.2.30 ，它是在不支持IPv6的网上用于表示 IPv4 节点。

# 综合组网技术

在目前 IPv6 和 IPv4 共存的情况下，实现 V4 和 V6 互联互通的综合组网技术和策略有：双栈策略和隧道策略

## 双栈策略

双栈策略是指在网元中同时具有 IPv4和IPv6两个协议栈，它既可以接收、处理、收发IPv4的分组，也可以接收、处理、收发IPv6的分组。对于主机（终端）来讲，“双栈”是指其可以根据需要来对业务产生的数据进行IPv4封装或者IPv6封装。对于路由器来讲，“双栈”是指在一个路由器设备中维护IPv6和IPv4两套路由协议栈，使得路由器既能与IPv4主机也能与IPv6主机通信，分别支持独立的IPv6和IPv4路由协议，IPv4和IPv6路由信息按照各自的路由协议进行计算，维护不同的路由表。IPv6数据报按照IPv6路由协议得到的路由表转发，IPv4数据报按照IPv4路由协议得到的路由表转发。

## 隧道策略

隧道策略是 IPv4/v6 综合组网技术中经常使用到的一种机制。所谓“隧道”，简单地讲就是利用一种协议来传输另一种协议的数据技术。隧道包括隧道入口和隧道出口（隧道终点），这些隧道端点通常都是双栈节点。在隧道入口以一种协议的形式来对另外一种协议数据进行封装，并发送。在隧道出口对接收到的协议数据解封装，并做相应的处理。在隧道的入口通常要维护一些与隧道相关的信息，如记录隧道 MTU 等参数。在隧道的出口通常出于安全性的考虑要对封装的数据进行过滤，以防止来自外部的恶意攻击。

隧道的配置方法分为手工配置隧道和自动配置隧道，而自动配置隧道又可以分为兼容地址自动隧道、 6to4 隧道、6over4、ISATAP、MPLS 隧道、GRE 隧道等，这些隧道的实现原理和技术细节都不相同，相应的，其应用场景也就不同。

PMTU（Path MTU，路径最大传输单元）是在源节点和目的节点之间的路径上的任一链路所能支持的链路 MTU 的最小值。

在IPv6网络中，分段不在中间路由器上进行。当需要传送的数据报文长度比链路 MTU 大时，只由源节点本身对数据报文进行分段，中间路由器不对数据报文进行再次分段。这就要求源节点在发送数据报文前能够发现整个发送路径上的所有链路的最小 MTU，然后以该 MTU 值发送数据报文，这就是 PMTU 发现。

![upload successful](/images/pasted-27.png)

PMTU发现过程如上图所示，图中各步骤含义如下：

（1）源节点向目的节点发送一个 IPv6 数据报文，其长度为 1500 字节。  
（2）中间路由器 RTA 的链路 MTU 值为 1400字节，所以它会用 ICMPv6 数据报文超长消息向源节点应答，告诉源节点"路径上的 MTU 值为 1400 字节"。  
（3）源节点向目的节点发送一个 IPv6 数据报文，其长度为 1400 字节。  
（4）中间路由器 RTB 的链路 MTU 值为 1300 字节，所以它会用 ICMPv6 数据报文超长消息向源节点应答，告诉源节点"路径上的 MTU 值为 1300 字节"。  
（5）源节点向目的节点发送一个I Pv6 数据报文，其长度为 1300 字节。

# 网络

Debian 配置 IPV6

```
vi /etc/network/interfaces

# /etc/network/interfaces -- configuration file for ifup(8),ifdown(8)
# The loopback interface
# automatically added when upgrading

auto lo
iface lo inet loopback

auto eth0
iface eth0 inet6 static
address 2001:da8:2:10d::2
netmask 64
up route -A inet6 add default gw 2001:da8:2:10d::1 dev $IFACE
iface eth0 inet static
address 58.1.4.74
netmask 255.255.255.0
up route add default gw 58.1.4.1 dev $IFACE
```

# WEB服务器

## nginx

1. 编译

    nginx 编译时需添加 --with-ipv6

2. 配置 - listen
```
listen [::]:80;
listen [::]:80 ipv6only=on;
```
以上两种配置方式，均表示只监听 IPV6 地址的 80 端口，因为 ipv6only 默认值为 on

	```
listen [::]:80 ipv6only=off;
```

	```
listen 80;
listen [::]:80 ipv6only=on;
```

 同时监听 IPV4 和 IPV6 地址。建议使用后者，若使用前者，nginx 获取的 remote_addr 值均为 ipv6（如客户端地址10.1.1.1，变量值为::ffff:10.1.1.1）。
 
 ```
 listen [fe80::20c:29ff:fe39:fded]:80;
```

 监听指定 IPV6 地址
 
3. 配置 - upstream

 ```
    upstream lbserver {
        server [2001:da8:2:10d::2]:8088;
    }
```

 不支持代理 fe80 开头的本地链路地址。
 
4. 配置 - proxy_pass

 ```
 proxy_pass http://[2001:da8:2:10d::2]:8088;
```

 同 upstream，不支持代理 fe80 开头的本地链路地址。
 
# 工具
## ping & ping6

版本1，若 ping 及 ping6 用法如下：

```
ping

Usage: ping [-aAbBdDfhLnOqrRUvV] [-c count] [-i interval] [-I interface]
            [-m mark] [-M pmtudisc_option] [-l preload] [-p pattern] [-Q tos]
            [-s packetsize] [-S sndbuf] [-t ttl] [-T timestamp_option]
            [-w deadline] [-W timeout] [hop1 ...] destination

ping6
Usage: ping6 [-aAbBdDfhLnOqrRUvV] [-c count] [-i interval] [-I interface]
             [-l preload] [-m mark] [-M pmtudisc_option]
             [-N nodeinfo_option] [-p pattern] [-Q tclass] [-s packetsize]
             [-S sndbuf] [-t ttl] [-T timestamp_option] [-w deadline]
             [-W timeout] destination
```

则，ping IPV6 用法如下：

```
ping6 -I eth0 fe80::20c:29ff:fe39:fded
PING fe80::20c:29ff:fe39:fded(fe80::20c:29ff:fe39:fded) from fe80::20c:29ff:fe39:fded eth0: 56 data bytes
64 bytes from fe80::20c:29ff:fe39:fded: icmp_seq=1 ttl=64 time=0.036 ms
64 bytes from fe80::20c:29ff:fe39:fded: icmp_seq=2 ttl=64 time=0.044 ms
```

版本1，不支持带有 [ ] 的 IPV6 地址，且只有 ping6 生效。  
版本2，若 ping 及 ping6 用法如下：  

```
ping
BusyBox v1.22.0.git (2013-12-31 13:39:13 CST) multi-call binary.

Usage: ping [OPTIONS] HOST

Send ICMP ECHO_REQUEST packets to network hosts

        -4,-6           Force IP or IPv6 name resolution
        -c CNT          Send only CNT pings
        -s SIZE         Send SIZE data bytes in packets (default:56)
        -t TTL          Set TTL
        -I IFACE/IP     Use interface or IP address as source
        -W SEC          Seconds to wait for the first response (default:10)
                        (after all -c CNT packets are sent)
        -w SEC          Seconds until ping exits (default:infinite)
                        (can exit earlier with -c CNT)
        -q              Quiet, only displays output at start
                        and when finished

ping6
BusyBox v1.22.0.git (2013-12-31 13:39:13 CST) multi-call binary.
Usage: ping6 [OPTIONS] HOST
Send ICMP ECHO_REQUEST packets to network hosts
        -c CNT          Send only CNT pings
        -s SIZE         Send SIZE data bytes in packets (default:56)
        -I IFACE/IP     Use interface or IP address as source
        -q              Quiet, only displays output at start
                        and when finished
```

则，ping IPV6 用法如下：

```
ping -I eth2 fe80::20c:29ff:fe39:fded
PING fe80::20c:29ff:fe39:fded (fe80::20c:29ff:fe39:fded): 56 data bytes
64 bytes from fe80::20c:29ff:fe39:fded: seq=0 ttl=64 time=4.279 ms
64 bytes from fe80::20c:29ff:fe39:fded: seq=1 ttl=64 time=0.501 ms

ping -I eth2 [fe80::20c:29ff:fe39:fded]
PING [fe80::20c:29ff:fe39:fded] (fe80::20c:29ff:fe39:fded): 56 data bytes
64 bytes from fe80::20c:29ff:fe39:fded: seq=0 ttl=64 time=0.657 ms
64 bytes from fe80::20c:29ff:fe39:fded: seq=1 ttl=64 time=0.543 ms

ping -6 -I eth2 fe80::20c:29ff:fe39:fded
PING fe80::20c:29ff:fe39:fded (fe80::20c:29ff:fe39:fded): 56 data bytes
64 bytes from fe80::20c:29ff:fe39:fded: seq=0 ttl=64 time=0.679 ms
64 bytes from fe80::20c:29ff:fe39:fded: seq=1 ttl=64 time=0.557 ms

ping -6 -I eth2 [fe80::20c:29ff:fe39:fded]
PING [fe80::20c:29ff:fe39:fded] (fe80::20c:29ff:fe39:fded): 56 data bytes
64 bytes from fe80::20c:29ff:fe39:fded: seq=0 ttl=64 time=0.658 ms
64 bytes from fe80::20c:29ff:fe39:fded: seq=1 ttl=64 time=0.619 ms

ping6 -I eth2 fe80::20c:29ff:fe39:fded
PING fe80::20c:29ff:fe39:fded (fe80::20c:29ff:fe39:fded): 56 data bytes
64 bytes from fe80::20c:29ff:fe39:fded: seq=0 ttl=64 time=0.698 ms
64 bytes from fe80::20c:29ff:fe39:fded: seq=1 ttl=64 time=0.547 ms

ping6 -I eth2 [fe80::20c:29ff:fe39:fded]
PING [fe80::20c:29ff:fe39:fded] (fe80::20c:29ff:fe39:fded): 56 data bytes
64 bytes from fe80::20c:29ff:fe39:fded: seq=0 ttl=64 time=0.561 ms
64 bytes from fe80::20c:29ff:fe39:fded: seq=1 ttl=64 time=0.693 ms
```

版本2，带不带 -6 和 [] 均是兼容的，但必须指定一个用来发送数据包的网络接口。  
版本1 和 版本2 通用格式如下：ping6 -I eth0 fe80::20c:29ff:fe39:fded  
PS：如果 ping6 的目标不是以 fe80 开头的本地链路地址，则不需要使用 -I 参数

# 其他待整理

* 查看网络配置 ifconfig，同ipv4
* 配置ip地址，ifconfig eth0 inet6 add 2001:da8:da8:da8:16fe:b5ff:fed9:b533/80，eth0 网卡可以和 ipv4 共用
* 删除ip地址，ifconfig eth0 inet6 del 2001:da8:da8:da8:16fe:b5ff:fed9:b533/80
* 查看路由表，route -A inet6 –n
* 添加删除路由类似 ipv4，如：  
 route -A inet6 add default gw 2001:da8:da8:da8:16fe:b5ff:fed9:b534  
 route -A inet6 del default gw 2001:da8:da8:da8:16fe:b5ff:fed9:b534
* 查看 arp 表，ip -6 neigh，arp 命令不支持 ipv6 的arp查询
* 万能命令 ip，只要加上 -6，所有 ipv4 下的命令都可以执行。
* 使用 ping6，类似于 ipv4 下的 ping，如果 ping6 的目标是链路本地地址，则需要使用 -I 参数
* 使用 traceroute6，类似 ipv4 下的 traceroute
* 网络抓包 tcpdump，本身就支持 v4 和 v6 的数据包，只是平时 v6 的数据包比较少而已，为了只看 v6 的数据包，可以加上协议字段，如  
 tcpdump -nn host 2001:da8:da8:da8:16fe:b5ff:fed9:b534  
 tcpdump -nn ip6  
 tcpdump -nn icmp6
* 使用 ssh 和 scp  
 ssh -P22 2001:da8:da8:da8:16fe:b5ff:fed9:b534，-6 只是强制使用 v6 地址，没有 -6 的时候如果对端是 v6 地址，则也可以正常使用。  
 scp -P22 [2001:da8:da8:da8:16fe:b5ff:fed9:b534]:/tmp/a /tmp/，注意需要使用中括号，因为 v6 地址中的 : 会和 ip 后面的 : 混淆掉。
* 使用 mtr，用法同 v4，加上 -6 则强制使用v6地址
* 使用 curl，用法同 v4，-6 则强制使用v6地址（不支持访问本地链路地址）  
 curl http://2001:da8:da8:da8:16fe:b5ff:fed9:b534/
* 使用 fping6，使用方法同 fping  
 fping6 2001:da8:da8:da8:16fe:b5ff:fed9:b534
* 使用 telnet，方法同 ipv4，注意目标地址不能为链路本地地址  
 telnet fe80::216:3eff:fe56:aff8 22
* 使用 wget，方法同 ipv4，-6 强制使用 v6 地址  
 wget  http://lvs.lxdns.net/testcdn.htm -e http-proxy=http://[2001:da8:da8:da8:16fe:b5ff:fed9:b534]
* 使用 netstat，方法同 ipv4
* 使用 ip6tables，方法同 iptables