
`mtu` 参数允许管理员更改 MTU 的大小。时不时会有论文讨论通过调整各种操作系统上的 MTU 来提高性能，但在 Linux 路由器上，该参数唯一可能的实际用途，是在一个因多种介质类型而产生 MTU 发现问题的网络中强制兼容。一个例子是将令牌环网的 MTU 设置为以太网大小，以绕过不支持正确分片、或在数据包设置了不分片（DF）位时不回送“请分片”消息的路由器。

`broadcast` 参数允许指定一个不同于由接口 IP 地址和网络掩码确定的广播地址。这主要是出于历史原因；早期版本的 BSD 实际上使用网络地址（全零）作为广播地址。此外，某些 IP over ATM 实现也使用全零地址进行广播。

## route 命令

`route` 命令是用于访问 Linux 内核路由表的接口。`route` 命令以三种模式运行：显示、添加和删除。当用于从路由表添加或删除路由时，其用途通常仅限于添加和移除静态路由条目。

### 使用 route 显示路由信息

当不附带任何参数使用 `route` 时，`route` 命令会将路由表打印到 stdout：

```
[root@lefty /root]# route
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
Lefty           *               255.255.255.255 UH    0      0        0 eth0
192.168.1.0     *               255.255.255.0   U     0      0        0 eth0
127.0.0.0       *               255.0.0.0       U     0      0        0 lo
default         192.168.1.1     0.0.0.0         UG    0      0        0 eth0
```

Destination（目标）列与 Genmask（即目标网络的网络掩码）结合，标识要路由的网络条目。Gateway（网关）列标识用于特定网络的网关，前提是 Flags 列中设置了 G（网关）标志。Flags 列告知管理员内核将如何解释该路由条目。表 9.5 总结了各种标志及其含义。

#### 表 9.5 route 标志

| 标志 | 描述 |
|------|-------------|
| I | 拒绝此网络的学习路由。 |
| A | 由 addrconf（一种 IPv6 地址配置协议）添加的路由。(http://www.ietf.cnri.reston.va.us/proceedings/95apr/charters/addrconf-charter.html) |
| C | 缓存条目。 |
| D | 由路由守护进程（D）或 ICMP 重定向创建的路由。 |
| G | 对于发往路由条目中标识的网络的数据流量，使用 Gateway 列中标识的网关（G）。 |
| M | 路由已被路由守护进程或 ICMP 重定向修改（M）。 |
| R | 恢复路由以允许对此特定路由条目进行路由更新。 |
| U | 网络路由已创建（up），内核将使用它来做出路由决策。 |

不带任何参数的 `route` 命令等同于本章后面介绍的 `netstat -r` 命令。

#### -C

`-C` 选项显示路由条目的缓存统计信息以及直连主机。带 `-C` 的 `route` 命令的输出还会显示触发路由查找的源地址和目标地址。`-C` 参数用于查看路由条目是否处于活动状态并被使用。下面是 `route -C` 实际运行的示例：

```
[root@lefty /root]# route -C
Kernel IP routing cache
Source      Destination     Gateway         Flags Metric Ref    Use Iface
lefty       host4.some.com  192.168.1.1     0     0      10    eth0
lefty       192.168.1.102   192.168.1.102   0     2      4     eth0
lefty       host4.some.com  192.168.1.1     0     0      10    eth0
```

#### -n

`-n` 选项用于关闭名称解析，这样使用 `route` 命令打印的所有条目都会以 IP 地址而非主机名显示。

#### -v

`-v` 选项最初用于 `route` 命令以提供附加信息——最显著的是路由条目的网络掩码，然而当前版本的 `route` 命令无需 `-v` 也能提供这些附加信息。此处介绍它仅作参考，以防你使用的是较旧版本的 Linux 或 `route` 命令。

#### -V

`-V` 选项显示 `route` 的版本，以及 net-tools 的版本和所支持的协议：

```
[root@lefty /root]# route -V
net-tools 1.54
route 1.96 (1999-01-01)
+NEW_ADDR +RTF_IRTT +RTF_REJECT +I18N
AF: (inet) +UNIX +INET +INET6 +AX25 +NETROM +ATALK +ECONET +ROSE
HW: +ETHER +ARC +SLIP +PPP +TUNNEL +TR +AX25 +NETROM +FR +ROSE +ASH +SIT
+FDDI +HIPPI +HDLC/LAPB
```

### 使用 route 添加路由条目

`route` 命令的真正强大之处在于添加静态路由，这些路由会影响本地节点上的路由选择；如果该本地节点上运行着路由守护进程，还会影响自治系统内的流量。

#### 添加网络路由

用于添加路由的 `route` 命令采用以下格式：

```
route add -net destination netmask gw gateway address
```

例如，要将所有发往 10.1.1.0/24 的流量路由到位于 192.168.1.253 的路由器，可以使用：

```
[root@lefty /root]# route add -net 10.1.1.0 netmask 255.255.255.0 gw 192.168.1.253
```

若要为特定主机添加路由条目，可使用 `-host` 参数，且该路由条目不需要 netmask 参数。要为 192.168.1.200 添加一条经 192.168.1.1 的路由，`route` 命令如下所示：

```
[root@lefty /root]# route add -host 192.168.1.200 gw 192.168.1.1
```

随后，当不带任何参数输入 `route` 命令时，所创建的路由条目将显示如下：

```
[root@lefty /root]# route
Kernel IP routing table
```

| 目标 | 网关 | 网络掩码 | 标志 | 度量 | 引用 | 使用 | 接口 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 192.168.1.200 | 192.168.1.1 | 255.255.255.255 | UGH | 0 | 0 | 0 | eth0 |

对于 PPP 网络，有时需要或更倾向于将路由指向网络接口，而非网关地址。这样做可以在不为串行连接使用 IP 转接网络的情况下节省 IP 地址，也可以在采用非广播网络时创建路由。下面是一个示例，但该主题将在第 7 章“内核支持工具”中更全面地讨论。

```
[root@lefty /root]# route add -net 10.10.10.0 netmask 255.255.255.0 ppp0
```

## ping

`ping` 是一种网络故障排查工具，用于报告远程节点是否可达。`ping` 向远程节点发送 ICMP 回显请求，远程节点应回应 ICMP 回显应答。由于 `ping` 和 ICMP 可以非常有效地用于绘制网络拓扑，许多网络数据包过滤器和防火墙被配置为丢弃 ICMP 数据包，以提供更严格的安全保障。

除了检查节点是否响应（或其他简单的连通性问题）之外，`ping` 还可用于排查其他与网络相关的问题。本节介绍 `ping` 的一些较高级且文档记录较少的参数。这些参数基于 Alexey Kuznetsov 编写的 iputils 软件包中的 `ping` 命令，该软件包可在 `ftp://ftp.sunet.se/pub/Linux/ip-routing/` 获取。大多数 Linux 版本都自带了 iputils。

### -d

要查看 `ping` 命令提供的额外调试信息，可以使用 `-d` 参数。它会让 `ping` 报告通常看不到的额外消息，例如 ICMP 网络不可达消息。这些额外信息通常有助于深入了解导致 `ping` 失败的网络状况。

### -f 泛洪
