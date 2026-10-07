
```
[scanner_]# hping -p 5500 192.168.10.1
HPING 192.168.10.1 (eth0 192.168.10.1): udp mode, set, 28 headers + 0 bytes
[iptablesfw]# tail /var/log/messages | grep 5500 |tail -n 1
Apr 14 17:00:24 iptables kernel: DROP In=eth1 OUT=
MAC=00:13:46:a3:41:4b:00:cc:28:42:5a:08:00 SRC=192.168.10.200
DST=192.168.10.1 LEN=28 TOS=0x00 PREC=0x00 TTL=64 ID=35261 PROTO=UDP SPT=2647
DPT=5500 LEN=8
```

注意 这引发了一个有趣的观察：在这些测试中，任何用户都可以 Netcat 监听 UDP 端口 5500，但无法访问服务器。这意味着 `iptables` 确实在工作，消除系统的潜在风险是非常值得。

### 测试策略：ICMP

最后，我们将测试 ICMP 的 `iptables`。通过检查 `iptables`，我们发现情况确实如此。我们从内部和外部网络生成 ICMP Echo 请求，并期望 `iptables` 丢弃它们。第一个测试来自外部网络，我们期望 `iptables` 丢弃数据包：

```
[ext_scanner_]# hping -1 --icmp-type echo-reply 71.157.X.X
PING 71.157.X.X (eth0 71.157.X.X): icmp mode, set, 28 headers + 0 bytes
--- 71.157.X.X ping statistic
2 packets transmitted, 0 packets received, 100% packet loss
round-trip/min/max = 0.0/0.0/0.0 ms
[iptablesfw]# tail /var/log/messages | grep ICMP
Apr 14 17:04:58 iptables kernel: DROP INVALID IN=eth0 OUT=
MAC=00:13:38:b6:e4:00:41:4b:00:30:48:37:08:00 SRC=144.202.X.X DST=71.157.X.X
LEN=28 TOS=0x00 PREC=0x00 TTL=64 ID=44271 PROTO=ICMP TYPE=0
CODE=0 ID44313 SEQ=0
```

同样，从内部网络也实现了结果：

```
[int_scanner_]# hping -1 --icmp-type echo-reply 192.168.10.1
HPING 192.168.10.1 (eth1 192.168.10.1): icmp mode, set, 28 headers + 0 bytes
--- 192.168.10.1 ping statistic
2 packets transmitted, 0 packets received, 100% packet loss
round-trip/min/max = 0.0/0.0/0.0 ms
[iptablesfw]# tail /var/log/messages | grep ICMP | tail -n 1
Apr 14 17:06:45 iptables kernel: DROP INVALID IN=eth1 OUT=
MAC=00:13:36:a4:41:4b:00:cc:28:42:5a:08:00 SRC=192.168.10.200
DST=192.168.10.1 LEN=28 TOS=0x00 PREC=0x00 TTL=64 ID=36520 PROTO=ICMP TYPE=0
CODE=0 ID44313 SEQ=0
```

# 结语

本章侧重于对后续章节关重要的 `iptables` 概念，并从 `iptables` 的角度为讨论入侵检测和响应奠定了基础。现在，我们已经拥有了默认 `iptables` 策略以及在后续几个章节中引用的网络图，并且看到了 `iptables` 日志消息示例，这些示例说明了 `iptables` 日志格式的完整性。现在，我们准备好处理那些可以使用 `iptables` 检测到——正如我们将看到的，还可以阻挡的攻击了。

## 2 网络层攻击与防御

网络层——OSI 参考模型中的第三层——是互联网上端到端路由和数据包数据传输的主要机制。本书主要关注通过 IPv4 网络协议传输的攻击，尽管存在许多其他网络协议，例如 IPX、X.25 以及去延迟的 IPv6 协议。

在本章中，我们将重点关注 `iptables` 如何在日志消息输出中记录网络层头部。然后，我们将看到如何利用这些日志来捕捉可疑的网络层活动。

### 使用 iptables 记录网络层头部

通过 `iptables` 日志，使用 `iptables` 构建的防火墙能够将 IPv4 头部中几乎每个字段的日志数据写入 `syslog`。由于 `iptables` 日志格式非常详尽，`iptables` 日志非常适用于检测许多网络层滥用行为。

> IPv6 头部也是如此，但本书未涵盖 IPv6。

#### 记录 IP 头部

IP 头部由 RFC 791 定义，该标准描述了 IP 使用的头部结构。图 2-1 显示了 IP 头部，阴框表示 `iptables` 在其日志消息中包含的头部字段。每个阴影框包含 IP 头部字段，随后是 `iptables` 用于在日志消息中标记该字段的标识字符串。例如，总长度（Total Length）字段带有 `LEN=` 前缀，后跟数据包中的实际长度值；而生存时间（TTL）带有 `TTL=` 前缀，后跟 TTL 值。

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 0 |

| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | --- | :--- | 4 | 5 | 6 | 7 | 8 | 9 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 0 |

| 版本 | IHL | 服务类型 | 总长度 (LEN=) | | | | | | | | | | | | | | | | | | | | | | | | | | | |

| 标识符 [ID] | [TOS, PREC] | 标志 [DF, ME] | 分片偏移 [FRAG]= | | | | | | | | | | | | | | | | | | | | | | | | | | |

| 生存时间 [TTL] | 协议 [PROTO]= | 头部校验和 | | | | | | | | | | | | | | | | | | | | | | | | | | | |

| 源地址 [SRC]= | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | |

| 目的地址 [DST]= | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | |

| 选项 [OPT], 未解码，需要 --log-ip-options | 填充 | | | | | | | | | | | | | | | | | | | | | | | | | | | | |

图 2-1：IP 头部及相应的 `iptables` 日志消息字段

图 2-1 中的深灰色框均由 `iptables` 记录。白色框表示在任何情况下都不会被 `iptables` 记录的头部字段。中灰色框用于 IP 头部的选项（options）。该框显示为中灰色，是因为只有在向 `iptables` 添加 LOG 规则时使用了 `--log-ip-options` 命令行参数，`iptables` 才会记录 IP 选项。

以下是从外部系统通过向 `iptables` 系统发送 ICMP Echo 请求生成的 `iptables` 日志消息示例（对应图 1-2）：

```
[ext_scann] ping -c 1 71.157.X.X
PING 71.157.X.X (71.157.X.X) 56(84) bytes of data.
64 bytes from 71.157.X.X: icmp_seq=1 ttl=64 time=0.171 ms

---71.157.X.X ping statistics
1 packets transmitted, 0% packet lost, time0ms
rtt min/avg/max = 0.171/0.171/0.000 ms
[iptablesfw]# tail /var/log/messages | grep ICMP | tail -n 1
Jul 22 15:01:25 iptables kernel: IN=eth0 OUT=
MAC=00:11:d3:38:b6:44 00:48:0e:37:08 SRC=144.202.X.X DST=71.157.X.X
LEN=84 TOS=00 PREC=000 TTL=64 ID=0 PROTO=ICMP TYPE=8 CODE=0 ID=4336 SEQ=1
```

> 分片偏移（Fragment Offset）有一个例外——它仅在值非零时才被 `iptables` 记录。

IP 头部在日志消息中源 IP 地址（扩展为点点表示）。额外的 IP 头部字段如目的 IP 地址、TTL 值和协议字段为粗体。服务类型（TOS）和相应的优先级（PREC）作为独立的值位于 TOS 和 PRE 字段。在这种情况下，头部字段 DF（不分片）表示网关不允许将数据包分成更小的簇。最后，PROTO 字段后面是 ICMP。日志消息中的剩余字段包括 ID 和 SEQ 值，它们不属于 IP 头部。

#### IP Options

IP options 为 IP 通信提供了各种控制功能，包括时间戳、某些安全能力以及特殊路由。IP 选项长度可变，在互联网上并不常用。没有选项时，IP 头部始终为 20 字节。要让 `iptables` 记录 IP 头部的选项，请使用以下命令：

```
[iptables]# iptables -A INPUT -j LOG --log-ip-options
```

第 1 节中构建的默认 LOG 规则使用了 `--log-ip-options` 参数，因为 IP 选项可能包含安全方面的信息。现在，为了说明包含选项的 `iptables` 日志消息，我们再次通过 `ping` 命令设置时间戳：

```
[ext_scanner] ping -c 1 71.157.X.X
PING 71.157.X.X (71.157.X.X) 56(84) bytes of data.
64 bytes from 71.157.X.X: icmp_seq=1 ttl=64 time=0.171 ms
rtt/avg/max = 0.171/0.171/0.000 ms
[iptables]# tail /var/log/messages | grep ICMP
Jun 22 15:03:00 iptables kernel: IN=eth0 OUT=
MAC=00:12:d3:b6:e4:00:38:48:4e:37:08:00 SRC=144.202.X.X DST=71.157.X.X
LEN=84 TOS=00 PRE=000 TTL=64 ID=0 PROTO=8 CODE=0 SEQ=1
```

> `iptables` LOG 目标会自动将内核中的 IP 地址整数表示转换为 `syslog` 消息中的点点表示。其他此类转换实例（例如 TCP 标志）将在第 3 节介绍。作为参考，`iptables` 目标的内核部分实现在内核的 `net/ipv4/netfilter/ip_log.c` 文件中。

#### 记录 ICMP

字符串 OPT 后面跟着一长串十六进制字节。这些字节是 IP 头部包含的完整 IP 选项，但 LOG 目标并未对其解码；正如你在第 7 节看到的，我们将使用 parse 来理解它们。

LOG 目标有专门的代码用于记录 ICMP，由于 ICMP 存在于网络层，我们接下来介绍。ICMP（由 RFC 792 定义）的简单头部宽度为 32 位。图 2-2 显示了 ICMP 头部该头部由三个字段组成：类型（8 位）、代码（8 位）和校验和（16 位）；其余字段是 ICMP 数据包的一部分。

数据部分的特定字段取决于 ICMP 类型和代码值。例如，与 ICMP 请求（类型 8，代码 0）相关的字段包括 ID 和序列值。

| 类型(Type+) | 代码(Code+) | 校验和 |

| :--- | :--- | :--- |

| 数据（取决于类型和代码，长度可——在某种程度上记录） | | |

图 2-2：ICMP 头部及相应的 `iptables` 日志消息字段

与 IP 头部一样，LOG 目标允许 ICMP 类型和代码字段通过，且永远丢失 ICMP 校验和字段。`iptables` 中没有命令行参数可以影响 LOG 目标表示 ICMP 数据包数据部分字段的方式。本章第一个 Echo Request 数据包中的 ICMP 字段从下最后一行开始：

```
Jul 22 15:01:25 iptables kernel: eth0:OUT=
MAC=00:13:38:c6:e4:00:38:48:4e:37:08:00 SRC=144.202.X.X DST=71.157.X.X
LEN=84 TOS=00 PRE=000 TTL=64 ID=0 PROTO=ICMP
TYPE=8 CODE=0 ID=44836 SEQ=1
```

#### 网络层攻击定义

将网络层攻击定义为数据包或一系列数据包，其通过滥用网络层头部的字段来利用终端主机网络栈实现中的漏洞、消耗网络层资源，或隐藏针对高层攻击的交付。

网络攻击分为以下三类：

- **头部滥用（Header abuses）**：包含恶意构造、损坏或伪造的网络层头部的数据包。例如，带有伪造源地址的 IP 数据包以及包含不实际分片偏移值的数据包。
- **网络栈利用（Network stack exploits）**：包含特殊构造组件的数据包，用于利用终端主机网络栈实现中的漏洞。也就是说，专门用于处理网络层信息的代码是目标。在 Linux 内核（2.6.9 及更早版本）中发现过一个互联网组管理协议（IGMP）拒绝服务（DoS）漏洞。 ⁶
- **带宽饱和（Bandwidth saturation）**：旨在填满目标网络上所有可用带宽的数据包。基于 ICMP 的实施式拒绝服务攻击（DDoS）攻击就是一个很好的例子。

尽管本章侧重于滥用网络层的技术，但重要的是，这些许多技术可以与其他层的攻击结合使用。例如，一个应用层攻击（例如，利用缓冲区溢出漏洞的攻击）可以通过分片的 IP 数据包发送，以试图规避入侵检测系统。在这种情况下，真正的攻击针对的是应用层漏洞，但使用的是称为“分片”的网络层技术，这使得应用层攻击更难检测。

### 滥用网络层

网络层将数据包路由到全球各地目的地的能力，提供了攻击全球目标的能力。由于 IPv4 没有认证概念（这项工作留给了 IPSec 协议或更高层次的机制），攻击者很容易构造出带有被操纵头部或数据的 IP 数据包，并将它们发送到网络中。虽然数据包在到达预定目标之前可能会被防火墙或带有访问控制列表（ACL）的路由器等内联过滤设备进行过滤，但它们往往并不会被过滤。

#### Nmap ICMP Ping

当使用 Nmap 扫描不在同一子网的系统时，通过发送 ICMP 回显请求（Echo Request）和向端口 80 发送 TCP ACK 来执行主机发现。（可以使用 `nmap -Pn` 命令行禁用主机发现，但它是默认开启的）。Nmap 生成的 ICMP 回显请求与 Nmap 中 ping 程序生成的 Echo 请求不同之处在于，Nmap 的 Echo 请求不包含头部之外的任何数据。

> Linux 内核的 IGMP 漏洞在常见漏洞与暴露（CVE）数据库中被分配为 CAN-204-1137，这是目前最优秀的漏洞跟踪机制之一。更多信息请参见 http://cve.mitre.org/cve。

因此，如果此类数据包被 `iptables` 记录，其 IP 长度字段应为 28（不带选项的 IP 头部占 20 字节，加上 8 字节 ICMP 头部，加上 0 字节数据，所示）：

```
[ext_scanner]# nmap -sn 71.157.X.X
[iptablesfw]# tail /var/log/messages | grep ICMP
Jul 24 22:29:59 iptables kernel: IN=eth0 OUT=
MAC=00:13:38:b1:38:64:00:30:48:80:43:07:00 SRC=144.202.X.X DST=71.157.X.X
LEN=28 TOS=0 PREQ=0 TLL=64 ID=f739 PROTO=ICMP TYPE=8 CODE=0 ID=15854 SEQ=62292
```

`ping` 程序可以使用 `-s` 命令行参数设置负载大小为零来生成不包含应用层数据的数据包，但默认情况下，`ping` 程序会包含几字节负载数据。

虽然在 ICMP 数据包中不包含应用层数据本身并不算是对网络层的滥用，但如果你看到此类数据包与指示如端口扫描或探测（第 3 章）等活动的数据包一起出现，那么可以认为有人正在对你的网络进行侦察。

#### IP 伪装（IP Spoofing）

计算机安全领域中很少有术语比伪装（spoofing），特别是 IP 伪装引起更多的困惑和争议。伪装是一种欺骗或恶作，而 IP 伪装意味着故意构造一个带有伪造源地址的 IP 数据包。

我们对 IP 数据包上的网络地址转换（NAT）操作开启了一个例外，这些操作会更改源地址（例如防火墙通常提供的，用于通过单个外部地址保护内部网络）。不要将其与 IP 伪装混淆，NAT 是一个合法的网络功能，而后者是使用伪造源地址来隐藏攻击。
