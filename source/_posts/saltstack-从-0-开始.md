title: saltstack 从 0 开始
author: MiracleQi-温柔魔君
tags:
  - salt
categories:
  - Linux
date: 2017-03-15 11:11:00
cover: /img/post-cover/40.jpg
---
# 1. 安装

```
//salt-master安装（环境：OS-debian，IP-120.25.255.213）
# apt-get install -t jessie-backports salt-master
//salt-minion安装（环境：OS-debian，IP-192.168.36.44）
# apt-get install -t jessie-backports salt-minion
```

# 2. 接入

## 2.1 minion操作

```

# vi /etc/salt/minion             -- 编辑minion配置文件
    master: 120.25.255.213        -- 指定master地址
    id: test-36.44                -- minion ID标识
# service salt-minion restart     -- 重启服务
```

## 2.2 master操作

```
# salt-key -a test-36.44       -- accept minion
# salt '*' test.ping           -- 测试所有的minion是否正常接入
test-36.44:
    True                       -- test-36.44 接入成功
```

# 3. 操作


## 3.1 下推文件

```
# salt test-36.44 cp.get_file salt://agent.log /root/agent.log
PS：
  1）. salt默认 file_roots 的目录是 /srv/salt，因此将 agent.log (准备下推的文件)放到 /srv/salt 目录下（支持文件夹）
  2）. 若文件目录的格式不是 salt://，则 minion 端会报错（如下）
    specified file /var/log/agent.log is not present to generate hash: Unsupported path: /var/log/agent.log
```

# 4. 问题

## 4.1 由于证书导致的'No response'

master 端执行 salt '*' test.ping，返回结果是 No response

查看 minion 端日志(/var/log/salt/minion)，如下：

```
The Salt Master has cached the public key for this node, this salt minion will wait for 10 seconds before attempting to re-authenticate
```

出现这个问题的原因是，minion 之前接入到其他的 master，旧的证书被缓存

解决方法：

```
rm -rf /etc/salt/pki/minion/minion_master.pub  -- 删除证书
service salt-minion restart                    -- 重启minion
```
总结：换 master 时，不仅仅改 master 的地址，还要删除旧的证书