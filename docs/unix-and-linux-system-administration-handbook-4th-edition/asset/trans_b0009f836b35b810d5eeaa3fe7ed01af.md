

![](img/14d78e3cecac4581d37024baf1e94cca_940_0.png)

## Exhibit F A “SYN flood” profile for NfSen

安全调查通常发生在触发事件的数小时或数天之后，但如果你例行保存 NetFlow 数据，就能轻松创建一个 NfSen 配置文件，回溯到更早的时间段。这种回顾性视图让你能够识别攻击中涉及的 IP 地址，并追踪可能受影响的其他主机。你还可以设置 NfSen 在非办公时间监控你的流量，并在满足特定条件时触发警报。

## Setting up NetFlow on a Cisco router

要开始使用 NetFlow，首先必须配置网络设备将 NetFlow 数据发送到 nfcapd。本节概述了在 Cisco 路由器上配置 NetFlow 的方法。

NetFlow 数据的导出按接口启用：

```
ios# interface fastethernet 0/0
 ios# ip route-cache flow
```

要告诉路由器将 NetFlow 数据发送到哪里，请输入以下命令：

```
ios# ip flow-export nfcapd-hostname listen-port
```

下面的选项将长寿命流拆分为 5 分钟的段。你可以选择 1 到 60 分钟之间的任意段长，但它应等于或小于 nfdump 的文件轮转周期，默认情况下为 5 分钟。

```
ios# ip flow-export version 5
 ios# ip flow-cache timeout active 5
```

在 Catalyst 6500/7600 上，除了正常的 NetFlow 导出外，还必须启用 NDE（NetFlow Data Export）。

方法如下：

```
ios# mls flow ip interface-full
 ios# mls ipv6 flow interface-full
 ios# mls nde sender version 5
```

在繁忙的路由器上，考虑积极超时小型流：

```
ios# mls aging fast time 4 threshold 2
 ios# mls aging normal 32
 ios# mls aging long 900
```

你仍然需要传统的 NetFlow 配置，包括在每个接口上使用 ip flow ingress 或 ip route-cache flow，以便看到“软件交换”的流，例如流向路由器本身的流。

对于 NetFlow v9，配置可能更长。取决于你的 IOS 版本，你还可以定义自己的模板。随着 Flexible NetFlow（FNF）的引入，NetFlow 环境变得更加复杂。

## 21.14 RECOMMENDED READING

Wikipedia 包含了一个不错的（尽管有些压缩）SNMP 概述，并附有指向 RFC 的链接。这是一个很好的起点。

MAURO, DOUGLAS R., AND KEVIN J. SCHMIDT. Essential SNMP (2nd Edition). Sebastopol, CA: O'Reilly Media, 2005.

SIMPLEWEB. SNMP and Internet Management Site. simpleweb.org.

你可能还会发现以下 RFC 有用。我们用对 RFC 内容的描述替换了 RFC 的实际标题，因为其中一些实际标题是不起作用的流行语和 SNMP 行话的混乱组合。

- RFC1155 – Characteristics of the SNMP data space (data types, etc.)
- RFC1156 – MIB-I definitions (description of the actual OIDs)
- RFC1157 – Simple Network Management Protocol
- RFC1213 – MIB-II definitions (OIDs)
- RFC3414 – User-based Security Model for SNMPv3
- RFC3415 – View-based Access Control Model for SNMPv3
- RFC3512 – Configuring devices with SNMP (best general overview)
- RFC3584 – Practical coexistence between different SNMP versions
- RFC3954 - Cisco Systems NetFlow Services Export Version 9

## 21.15 EXERCISES

**E21.1** 你正在排查网络问题，**netstat -rn** 给出了以下输出。问题是什么，你会使用什么命令来修复它？

| Destination | Gateway | Genmask | Flags | MSS | Window | irtt | Iface |
|---|---|---|---|---:|---:|---:|---|
| 128.138.202.0 | 0.0.0.0 | 255.255.255.0 | U | 40 | 0 | 0 | eth0 |
| 127.0.0.0 | 0.0.0.0 | 255.0.0.0 | U | 40 | 0 | 0 | lo |

☆ **E21.2** 编写一个脚本，监控一组指定的机器，如果某台机器在一段时间内对 ping 无响应，则通过电子邮件通知管理员。不要硬编码机器列表、通知电子邮件地址或判定无响应行为的时间。

☆ **E21.3** 在本地网络上的一台机器上尝试更改子网掩码。它仍然能工作吗？你能访问站点上的所有内容吗？其他机器能访问你吗？广播是否仍然有效（例如 ARP 请求或 DHCP discover 数据包）？解释你的发现。（需要 root 权限。）

☆ **E21.4** 使用 **traceroute** 命令发现网络上的路由路径。

a) 离开你的设施需要多少跳？
b) 你有账号的机器之间是否存在路由器？
c) 你能找到任何瓶颈吗？
d) 你的站点是否多宿主？

☆☆ **E21.5** 设计一个 MIB，其中包含你作为 Linux 系统管理员可能想要查询或设置的所有变量。为 MIB 留出扩展空间，以便包含你忘记的那项重要的新系统管理员变量。

☆☆ **E21.6** 使用 **wireshark** 或 **tshark** 捕获展示以下协议的流量。对于 TCP 会话，请包含并标出初始和最终数据包。提交干净、格式良好的输出。（需要 root。）

a) ARP
b) ICMP echo request and reply
c) SMTP
d) HTTP
e) DNS
f) Samba
g) SSH

☆☆ **E21.7** 设置 Cacti 图表，显示发送到本地路由器和从本地路由器发送的报文。该项目需要一个 SNMP 包来查询路由器，并且你必须知道路由器的只读 community 字符串。

