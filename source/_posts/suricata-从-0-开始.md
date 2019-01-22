title: suricata 从 0 开始
author: MiracleQi-温柔魔君
tags:
  - suricata
categories:
  - Linux
date: 2018-01-31 17:36:00
cover: /img/post-cover/43.jpg
---
# 背景

OpenWAF 是在 openresty 基础上发布的，但安全不仅仅是针对 HTTP 协议的防护，而是全方位立体化的防护。  
因此，为了防护更多的协议，开始接触 suricata，用熟后，争取将 OpenWAF 集成到 suricata 上，再扩展其他协议防护。  
如果成功，那么将 OpenWAF 独立出来，形成单独的防护库，即支持 openresty（nginx） 又支持 suricata

# 《suricata简介》

Suricata 是一个高性能的网络 IDS，IPS 和网络安全监控引擎。  

IPS：入侵预防系统(IPS: Intrusion Prevention System)是电脑网络安全设施，是对防病毒软件（Antivirus Programs）和防火墙(Packet Filter, Application Gateway)的补充。 入侵预防系统(Intrusion-prevention system)是一部能够监视网络或网络设备的网络资料传输行为的计算机网络安全设备，能够即时的中断、调整或隔离一些不正常或是具有伤害性的网络资料传输行为。是新一代的侵入检测系统（IDS）。

Suricata 是一个网络入侵检测和防护引擎，由开放信息安全基金会及其支持的厂商开发。该引擎是多线程的，内置支持 IPV6。可加载现有的 Snort 规则和签名，支持 Barnyard 和 Barnyard2 工具.

IDS：英文“Intrusion Detection Systems”的缩写，中文意思是“入侵检测系统”。依照一定的安全策略，通过软、硬件，对网络、系统的运行状况进行监视，尽可能发现各种攻击企图、攻击行为或者攻击结果，以保证网络系统资源的机密性、完整性和可用性。

Barnyard：知名的开源IDS的日志工具，具有快速的响应速度，优异的数据库写入功能，是做自定义的入侵检测系统不可缺少的插件。

至于IDS和IPS的区别，可以查看下网络中其他文章，本人理解：

IDS只是发现攻击、产生报警，而 IPS 不但可以发现攻击，更重要的是针对攻击采取行动。

<<span style="box-sizing: border-box; margin: 0px; padding: 0px; color: rgb(255, 0, 0); font-size: 24px; font-family: 微软雅黑, 黑体; line-height: 20px;">suricata编译安装>

想到研究 suricata 只读源码估计还不凑效，需要了解下真实环境下怎么应用，这样理解起来估计会更有感觉，于是在自己本地虚拟机中安装编译一下：

1、虚拟机操作系统Linux Debian7.0  
2、下载suricata源码  
    wget -c https://www.openinfosecfoundation.org/download/suricata-4.0.3.tar.gz