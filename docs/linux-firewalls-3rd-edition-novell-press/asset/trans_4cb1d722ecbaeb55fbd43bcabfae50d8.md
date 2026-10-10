
## 检查输入、输出和转发规则

| # | Pkts | Bytes | Target | Proto | Opt | In | Out | Source/Destination | Detail |
|---|---|---|---|---|---|---|---|---|---|
| 9 | 0 | 0 | ACCEPT | tcp | -- | any | eth1 | choke.dmz.lan | \ |
| | | | | mail.lan | tcp | | sport: 1024:65535 | dport: smtp state NEW |
| 10 | 0 | 0 | ACCEPT | udp | -- | any | eth1 | timeserver.edu | \ |
| | | | | udp | | | sport: 1024:65535 | dport: ntp state NEW |
| 11 | 0 | 0 | ACCEPT | icmp | -- | any | eth1 | choke.dmz.lan | \ |
| | | | | anywhere | | | | icmp fragmentation-needed |
| 12 | 0 | 0 | ACCEPT | icmp | -- | any | eth0 | router.private.lan | \ |
| | | | | .private.lan | | | | icmp echo-request |
| 13 | 0 | 0 | ACCEPT | icmp | -- | any | eth0 | router.private.lan | \ |
| | | | | .private.lan | | | | icmp echo-reply |
| 14 | 0 | 0 | ACCEPT | icmp | -- | any | eth1 | choke.dmz.lan | \ |
| | | | | .dmz.lan | | | | icmp echo-request |
| 15 | 0 | 0 | ACCEPT | icmp | -- | any | eth1 | choke.dmz.lan | \ |
| | | | | firewall.dmz.lan | | | | icmp echo-reply |
| 16 | 0 | 0 | ACCEPT | tcp | -- | any | eth0 | router.private.lan | \ |
| | | | | jet.private.lan | | | | tcp dport:printer state NEW |
| 17 | 0 | 0 | ACCEPT | tcp | -- | any | any | anywhere | \ |
| | | | | anywhere | | | | tcp flags:RST/RST |
| 18 | 0 | 0 | LOG | all | -- | any | any | anywhere | \ |
| | | | | anywhere | | | | LOG level warning |

OUTPUT 链的默认策略是 DROP。被拒绝的数据包会被直接丢弃，不会向本地程序返回任何通知。该链上共有 18 条规则：

- **第 1 行** — 允许任何经由环回接口发出的数据包。
- **第 2 行** — 任何被识别为属于先前已建立（ESTABLISHED）连接或交换的一部分的数据包，或与之一相关（RELATED）的数据包，均被允许。
- **第 3 行** — 允许转发给 DMZ 中本地名称服务器的本地 DNS 请求（服务器到服务器）。
- **第 4 行** — 允许本地 DNS 客户端通过 UDP 向 DMZ 中的本地名称服务器发送请求。
- **第 5 行** — 允许本地 DNS 客户端通过 TCP 向 DMZ 中的本地名称服务器发送请求。
- **第 6 行** — 允许本地主机（即 LAN 路由器）与私有 LAN 中的本地 SSH、HTTP、HTTPS、auth 和 FTP 服务器之间已建立的连接。
- **第 7 行** — 允许本地主机（即 choke 防火墙）与 DMZ 中的本地 SSH 服务器之间已建立的连接。
- **第 8 行** — 允许本地主机（即 choke 防火墙）与任何位置的 SSH、HTTP、HTTPS、auth 和 FTP 服务器之间已建立的连接。
- **第 9 行** — 允许本地主机（即 choke 防火墙）向 DMZ 中的邮件网关发送邮件。
- **第 10 行** — 允许本地主机（即 choke 防火墙）向特定远程服务器发送客户端 **ntp** 时间请求。
- **第 11 行** — 允许本地主机（即 choke 防火墙）在任何位置发送 ICMP 类型 3 **需要分片（fragmentation-needed）** 消息，作为 MTU 大小发现的一部分。
- **第 12 行** — 允许本地主机（即 LAN 路由器）向私有 LAN 中的主机发送 ICMP **ping** 请求。
- **第 13 行** — 允许本地主机（即 LAN 路由器）向私有 LAN 中的主机发送 ICMP **ping** 响应。
- **第 14 行** — 允许本地主机（即 choke 防火墙）向 DMZ 中的主机发送 ICMP **ping** 请求。
- **第 15 行** — 允许本地主机（即 choke 防火墙）向 DMZ 与互联网之间的公共防火墙发送 ICMP **ping** 响应。
- **第 16 行** — 允许本地主机（即 LAN 路由器）访问私有 LAN 中的网络打印机。
- **第 17 行** — 允许本地主机向任何位置发送 TCP RST 消息。
- **第 18 行** — 所有其他出站数据包在被默认策略丢弃之前都会被记录日志。

### 检查转发规则

转发规则适用于通过机器路由或转发的数据包。被转发的数据包仅由定义在 FORWARD 链中的规则进行检查。这些数据包不会根据 INPUT 或 OUTPUT 链中的规则进行检查。如果数据包的目的地址不是数据包到达的接口的地址，则该数据包由 FORWARD 链进行检查。如果数据包匹配 FORWARD 接受规则，则在经过任何为 POSTROUTING 链定义的规则检查后，该数据包会从相应的接口发出。

为了说明目的，下面显示的防火墙规则对会将来自内部网络的所有 TCP 连接进行转发。UDP 流量不会被路由。相关的 ICMP 流量会被路由：

```bash
iptables -A FORWARD -p tcp -m state --state ESTABLISHED,RELATED -j ACCEPT
iptables -A FORWARD -i $LAN_INTERFACE -o $EXTERNAL_INTERFACE -p tcp \
    -s $INTERNAL_LAN_ADDRESSES -m state --state NEW -j ACCEPT
```

本节基于转发规则的代表性样本。当默认策略为 DROP 时，INPUT 和 OUTPUT 规则大多是 ACCEPT 规则。默认情况下，一切都将被拒绝，而您需明确定义哪些内容将被接受：

```bash
iptables -v -L FORWARD
```

```text
Chain FORWARD (policy DROP 0 packets, 0 bytes)

pkt bytes target prot opt in out source/destination

1 67 6050 ACCEPT all -- any anywhere any anywhere  \
state RELATED, ESTABLISHED

2 0 0 ACCEPT tcp -- eth1 eth0 selected.remote.host \
host1.private.lan tcp spts:1024:65535 dpts:ssh \
flags:SYN,RST,ACK,SYN state NEW

3 0 0 ACCEPT tcp -- eth0 eth1 .private.lan \
mailserver.dmz.lan multiportdports smtp,pop3 tcp spts:1024:65535 \
flags:SYN,RST,ACK,SYN state NEW

4 1 60 ACCEPT tcp -- eth0 eth1 .private.lan \
web-proxy.dmz.lan multiportdports http,https tcp spts:1024:65535 \
flags:SYN,RST,ACK,SYN state NEW

5 1 60 ACCEPT tcp -- eth0 eth1 .private.lan \
anywhere tcp spts:1024:65535 dpts:ssh \
flags:SYN,RST,ACK,SYN state NEW

6 0 0 ACCEPT tcp -- eth0 eth1 .private.lan \
news-server.net tcp spts:1024:65535 dpt:nttp \
flags:SYN,RST,ACK,SYN state NEW

7 0 0 REJECT tcp -- eth1 any anywhere \
.private.lan tcp spts:1024:65535 dpt:auth \
reject-with icmp-port-unreachable

8 0 0 ACCEPT icmp -- any any anywhere \
anywhere icmp fragmentation-needed

9 2 168 ACCEPT icmp -- eth0 eth1 .private.lan \
anywhere icmp echo-request

10 0 0 ACCEPT tcp -- any any anywhere \
anywhere tcp flags:FIN,ACK,FIN,ACK

11 0 0 ACCEPT tcp -- any any anywhere \
anywhere tcp flags:RST,RST

12 0 0 LOG all -- any any anywhere \
anywhere LOG level warning
```

FORWARD 链的默认策略是 DROP。被拒绝的数据包会被直接丢弃，不会向本地或远程程序返回任何通知。该链上共有 12 条规则：

- **第 1 行** — 任何被识别为属于先前已建立（ESTABLISHED）连接或交换的一部分的数据包，或与之一相关（RELATED）的数据包，均允许双向通过。
- **第 2 行** — 允许来自特定远程主机的传入 SSH 连接连接到私有 LAN 中的 host1。
- **第 3 行** — 允许向 DMZ 中的邮件网关和 pop 服务器发起的出站客户端连接。
- **第 4 行** — 允许向 DMZ 中的 Web 代理发起的出站客户端连接（包括 HTTP 和 HTTPS）。
- **第 5 行** — 允许向任何位置的远程 SSH 服务器发起的出站客户端连接。
- **第 6 行** — 允许向特定远程新闻服务器发起的出站客户端连接。
- **第 7 行** — 拒绝向本地 ident 服务器发起的传入 auth 请求。
- **第 8 行** — 允许双向的 ICMP 类型 3 需要分片（fragmentation-needed）消息，作为 MTU 大小发现的一部分。
- **第 9 行** — 允许向任何位置发送出站 ping ICMP echo-request。
- **第 10 行** — 双向接受 FIN/ACK 数据包。
- **第 11 行** — 双向接受 TCP RST 数据包。
- **第 12 行** — 所有其他双向数据包在被默认策略丢弃之前都会被记录日志。

在这种情况下，-v 选项通常有助于查看传入和传出网络接口名称。eth0 是连接到 .private.lan 网络的内部接口。eth1 是连接到 .dmz.lan 及其后互联网的外部接口。请记住，无论是否有 NAT，都需要 FORWARD 规则。还要记住，任何 NAT 规则都是在 nat 表中定义的。这些规则是在默认的 filter 表中定义的。

## 针对防火墙规则测试单个数据包

规则检查命令，即 ipchains 中的 -C 命令，尚未在 iptables 中实现。

## 解释系统日志

syslogd 是记录系统事件的服务守护进程。syslogd 的主要系统日志文件是 /var/log/messages。许多程序使用 syslogd 的标准日志服务。其他程序，如 Apache Web 服务器，维护自己单独的日志文件。

## syslog 配置

并非所有日志消息都同等重要——甚至有趣。这正是 /etc/syslog.conf 发挥作用的地方。配置文件 /etc/syslog.conf 允许您根据需求调整日志输出。

