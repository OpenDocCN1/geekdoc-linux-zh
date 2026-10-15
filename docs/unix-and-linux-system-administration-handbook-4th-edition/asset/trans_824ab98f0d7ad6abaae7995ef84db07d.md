

## iptables 防火墙设置

在你能够使用 iptables 作为防火墙之前，必须启用 IP 转发并确保各种 iptables 模块已加载到内核中。有关启用 IP 转发的更多信息，请参阅第 421 页的 Tuning Linux kernel parameters 或第 492 页的 Security-related kernel variables。安装 iptables 的软件包通常包含启动脚本来实现此启用和加载。

Linux 防火墙通常实现为包含在 rc 启动脚本中的一系列 iptables 命令。单个 iptables 命令通常采用以下形式之一：

```
iptables -F chain-name
iptables -P chain-name target
iptables -A chain-name -i interface -j target
```

第一种形式（-F）会清空链中的所有先前规则。第二种形式（-P）为链设置默认策略（即 target）。我们建议你将默认链目标设置为 DROP。第三种形式（-A）将当前规范追加到链中。除非你使用 -t 参数指定表，否则你的命令适用于 filter 表中的链。-i 参数将规则应用于指定接口，-j 标识目标。iptables 接受许多其他子句，其中一些显示在表 22.3 中。

**表 22.3 iptables 过滤器的命令行标志**

| 子句 | 含义或可能值 |
|---|---|
| -p proto | 按协议匹配：tcp、udp 或 icmp |
| -s source-ip | 匹配主机或网络源 IP 地址（CIDR 记法可用） |
| -d dest-ip | 匹配主机或网络目标地址 |
| --sport port# | 按源端口匹配（注意双破折号） |
| --dport port# | 按目标端口匹配（注意双破折号） |
| --icmp-type type | 按 ICMP 类型代码匹配（注意双破折号） |
| ! | 否定一个子句 |
| -t table | 指定命令适用的表（默认是 filter） |

### 一个完整示例

下面我们拆解一个完整示例。我们假设 eth1 接口通往互联网，而 eth0 接口通往内部网络。eth1 的 IP 地址是 128.138.101.4，eth0 的 IP 地址是 10.1.1.1，且两个接口的网络掩码均为 255.255.255.0。此示例使用无状态数据包过滤来保护 IP 地址为 10.1.1.2 的 Web 服务器，这是保护互联网服务器的标准方法。示例后面我们将展示如何使用有状态过滤来保护桌面用户。

我们的第一组规则初始化 filter 表。首先，表中的所有链都被清空，然后 INPUT 和 FORWARD 链的默认目标被设置为 DROP。与任何其他网络防火墙一样，最安全的策略是丢弃你未明确允许的任何数据包。

```
iptables -F
iptables -P INPUT DROP
iptables -P FORWARD DROP
```

由于规则按顺序评估，我们将最繁忙的规则放在前面。¹¹ 第一条规则允许所有源自受信任网络的连接通过防火墙。FORWARD 链中的接下来的三条规则允许连接通过防火墙到 10.1.1.2 上的网络服务。具体来说，我们允许 SSH（端口 22）、HTTP（端口 80）和 HTTPS（端口 443）通过到我们的 Web 服务器。

```
iptables -A FORWARD -i eth0 -p ANY -j ACCEPT
iptables -A FORWARD -d 10.1.1.2 -p tcp --dport 22 -j ACCEPT
iptables -A FORWARD -d 10.1.1.2 -p tcp --dport 80 -j ACCEPT
iptables -A FORWARD -d 10.1.1.2 -p tcp --dport 443 -j ACCEPT
```

我们仅允许到防火墙主机（10.1.1.1）的 TCP 流量为 SSH，这对于管理防火墙本身很有用。下面列出的第二条规则允许回环流量，该流量保留在主机本地。管理员在无法 ping 默认路由时会感到紧张，因此这里的第三条规则允许来自内部 IP 地址的 ICMP ECHO_REQUEST 数据包。

```
iptables -A INPUT -i eth0 -d 10.1.1.1 -p tcp --dport 22 -j ACCEPT
iptables -A INPUT -i lo -d 127.0.0.1 -p ANY -j ACCEPT
iptables -A INPUT -i eth0 -d 10.1.1.1 -p icmp --icmp-type 8 -j ACCEPT
```

对于任何 IP 主机要在互联网上正常工作，必须允许某些类型的 ICMP 数据包通过防火墙。以下八条规则允许最小的 ICMP 数据包集到达防火墙主机，以及到达其后面的网络。

```
iptables -A INPUT -p icmp --icmp-type 0 -j ACCEPT
iptables -A INPUT -p icmp --icmp-type 3 -j ACCEPT
iptables -A INPUT -p icmp --icmp-type 5 -j ACCEPT
iptables -A INPUT -p icmp --icmp-type 11 -j ACCEPT
iptables -A FORWARD -d 10.1.1.2 -p icmp --icmp-type 0 -j ACCEPT
iptables -A FORWARD -d 10.1.1.2 -p icmp --icmp-type 3 -j ACCEPT
iptables -A FORWARD -d 10.1.1.2 -p icmp --icmp-type 5 -j ACCEPT
iptables -A FORWARD -d 10.1.1.2 -p icmp --icmp-type 11 -j ACCEPT
```

我们接下来向 nat 表的 PREROUTING 链添加规则。尽管 nat 表并不用于数据包过滤，但其 PREROUTING 链对于反欺骗过滤特别有用。如果我们在 PREROUTING 链中放置 DROP 条目，则无需在 INPUT 和 FORWARD 链中重复它们，因为 PREROUTING 链应用于进入防火墙主机的所有数据包。将条目放在一个地方更干净，而不是重复它们。

> 请参阅第 473 页了解有关 IP 欺骗的更多信息

