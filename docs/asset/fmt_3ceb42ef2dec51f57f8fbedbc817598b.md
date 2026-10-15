
LINUX 提供了一系列 `NETWORKING` 命令来支持网络故障排除、IP 配置和路由任务。本章涵盖 `ifconfig`、`route`、`ping`、`traceroute`、`arp`、`netstat` 和 `tcpdump`。除了 `tcpdump` 之外，这些命令很可能会随大多数 Linux 发行版的标准安装一起提供。这些命令（再次除外 `tcpdump`）源自早期版本的 BSD 和 AT&T 的 System V 命令。

## ifconfig

`ifconfig` 是用于将接口投入服务并指定第 1 层到第 3 层属性的命令，例如媒体类型、速度和网络地址。（第 1 层涵盖网络的物理方面，例如双绞线或同轴电缆，第 2 层涵盖数据层，包括媒体相关网络，例如以太网帧和以太网网络中的媒体访问控制。）`ifconfig` 通常位于 `/sbin/` 目录中，但非 root 用户也可以运行该程序。然而，只有 root 才能进行配置更改。在大多数 Linux 版本中，`ifconfig` 命令由 `net-tools` 分发提供，可在 `http://www.tazenda.demon.co.uk/phil/net-tools/` 获取。

除了接口配置之外，`ifconfig` 还用于报告接口状态；因此，`ifconfig` 的功能可以分为两个部分：接口报告和接口配置。

### Interface Reporting

最常见的是 `ifconfig` 用于接口报告，以协助网络故障排除。

不带任何参数的基本命令非常有用：

```
[root@lefty /sbin]# /sbin/ifconfig
et0      Link encap:Ethernet  HWaddr 00:E9:29:4B:AC:0C
          inet addr:192.168.1.254  Bcast:192.168.1.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:9833  errors:0  dropped:0  overruns:0  frame:0
          TX packets:10195 errors:0  dropped:0  overruns:0  carrier:0
          collisions:306  txqueuelen:100 
          Interrupt:10  Base address:0xb800

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          UP LOOPBACK RUNNING  MTU:3924  Metric:1
          RX packets:18  errors:0  dropped:0  overruns:0  frame:0
          TX packets:18  errors:0  dropped:0  overruns:0  carrier:0
          collisions:0  txqueuelen:0
```

`ifconfig` 已报告内核识别并配置为使用的所有接口。（Linux `ifconfig` 与其他版本的 UNIX 不同，不需要额外参数即可查看所有接口。）在 `eth0` 上，我们可以很容易地确定接口基于接口名称（`eth0`）、`Link encap:Ethernet` 以及 6 字节（48 位）地址是以太网。下一行报告了 IP 地址以及使用的广播地址和网络掩码。

第三行报告接口当前正在运行（`UP`），这意味着它可以发送和响应网络流量。它以广播方式运行（以太网的标准），并且还配置为侦听多播流量。多播配置是必需的，以允许内核和 `RIP-2` 等用户应用程序检查多播流量，因为 `RIP-2` 使用 RIP 多播地址 `224.0.0.9`。

最大传输单元（MTU）为 1500 字节，这是以太网帧的标准长度，`ifconfig` 已报告这是内核配置的大小。正如名称最大传输单元所暗示的那样，这是将从该接口传输的最大数据包大小。如果管理员手动降低 MTU 的大小，它只会影响传出数据包，这意味着系统仍会识别在拓扑支持的最大 MTU 范围内的传入数据包。常见的 MTU 大小如表 9.1 所示。

## 表 9.1 网络拓扑和最大传输单元

| Topology | MTU |
|---|---|
| Ethernet | 1500 |
| Fiber Distributed Data Interface (FDDI) | 4352 |
| Point-to-Point (PPP) | 1500 |
| Serial Line IP (slip) | 1006 |
| Token Ring | 4464 |

第 4 行到第 6 行报告了对排查网络问题非常有用的流量统计信息。在这里，根据流量来看碰撞数量似乎很高，这可能意味着 Linux 路由器与以太网交换机之间存在半双工和全双工端口不匹配。最后一行报告了网络接口卡为低级设备驱动程序支持所使用的资源。此特定 NIC 使用中断 10 与 CPU 通信，并具有从 `0xb800` 开始的内存段。

由于以太网的流行，上面描述的 `ifconfig` 输出在大多数企业网络中非常典型，但对 Linux 支持的其他硬件进行更仔细的检查显示了 Linux 对网络拓扑的广泛支持。

## 硬件类型

表 9.2 列出了 Linux 操作系统支持的硬件类型。

## 表 9.2 Linux 和 ifconfig 支持的网络媒体（硬件）类型

| Media | hwtype abbreviation |
|---|---|
| Adaptive Serial Line IP | Adaptive |
| Amateur NET/ROM | netrom |
| Amateur ROSE | rose |
| Amateur X.25 | ax25 |
| ARCnet | arcnet |
| Ash | ash |
| Cisco HDLC | hdlc |
| Compressed Serial Line IP | cslip |
| Compressed Serial Line IP 6 bit | cslip6 |
| Econet | Ec |
| Ethernet | ether |
| Fiber Distributed Data Interface | fddi |
| Frame Relay Access Device | frad |
| Frame Relay DLCI | dlci |
| High-Performance Parallel Interface | hippi |
| IP in IP Tunneling | tunnel |
| IPv6 in IPv4 Tunneling | sit |
| IrLAP | irda |
| LAPB | lapb |
| Local Loopback | loop |
| Point-to-Point Protocol | ppp |
| Serial Line IP | slip |
| Serial Line IP 6 bit | slip6 |
| Token Ring | tr |

接下来将更详细地介绍更常见的接口。

### 串行线路 IP—slip

`slip`（参见 RFC 1055，“通过串行线路传输 IP 数据报的非标准：Slip”）是一种串行面向连接的协议，在大多数网络中已被 PPP 取代。Linux 支持的 `slip` 变体包括 `cslip`，它是一种基于 RFC 1144 “低速串行链路的 TCP/IP 标头”中描述的压缩技术压缩的串行线路 IP，也称为作者姓名：Van Jacobson 压缩。另一个变体是 `slip6` 以及 `slip6` 的压缩版本，恰当地命名为 `cslip6`。

### 点对点协议（PPP）

`PPP` 是串行链路连接的事实标准，并已扩展到其他网络拓扑，包括 SONET 上的 IP。`PPP`（在第 7 章“内核支持工具”中进行了全面介绍）。

### IP over IP 隧道（IPIP）

IP over IP 隧道通常用于通过 transit 网络连接自治网络。IP over IP 也可用于创建虚拟专用网络（VPN）。

### 逻辑环回设备—Loop

环回接口的存在是为了允许需要网络连接的应用程序与驻留在本地主机上的服务通信，而无需或通过物理接口。

### 令牌环（TR）—（IEEE 802.5）

令牌环以 4 或 16Mbps 速率运行，其早期优势在于不依赖于广播域。这一优势已被以太网速度的提升和以太网交换技术所克服。然而，令牌环在许多组织中仍然得到支持——尤其是银行和金融机构等行业，IBM 在这些行业中渗透很强。（IBM 销售了大量令牌环，因为其早期的大型机不支持以太网。）

回到前面列出的 `ifconfig` 输出，注意到 IP 地址是 IP 版本 4。除了 IPv4，Linux 还支持其他协议及其寻址。一些更流行的协议及其 `ifconfig` 对应的输出显示在表 9.3 中。
