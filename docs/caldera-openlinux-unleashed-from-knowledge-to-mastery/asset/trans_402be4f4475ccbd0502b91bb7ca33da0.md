
# 使用 nslookup

本文件列出了整个互联网上的 13 个根域名服务器，这些信息是从 `ftp://ftp.rs.internic.net/domain/named.root` 获取的。（我们展示的是该文件的一个略有编辑的版本。）

```text
;       This file is made available by InterNIC
;       registration services
;       under anonymous FTP as
;           file          /domain/named.root
;       on server         FTP.RS.INTERNIC.NET

.               3600000   IN NS   A.ROOT-SERVERS.NET.
A.ROOT-SERVERS.NET. 3600000   A   198.41.0.4
.               3600000   NS B.ROOT-SERVERS.NET.
B.ROOT-SERVERS.NET. 3600000   A   128.9.0.107
.               3600000   NS C.ROOT-SERVERS.NET.
C.ROOT-SERVERS.NET. 3600000   A   192.33.4.12
.               3600000   NS D.ROOT-SERVERS.NET.
D.ROOT-SERVERS.NET. 3600000   A   128.8.10.90
.               3600000   NS E.ROOT-SERVERS.NET.
E.ROOT-SERVERS.NET. 3600000   A   192.203.230.10
.               3600000   NS F.ROOT-SERVERS.NET.
F.ROOT-SERVERS.NET. 3600000   A   192.5.5.241
.               3600000   NS G.ROOT-SERVERS.NET.
G.ROOT-SERVERS.NET. 3600000   A   192.112.36.4
.               3600000   NS H.ROOT-SERVERS.NET.
H.ROOT-SERVERS.NET. 3600000   A   128.63.2.53
.               3600000   NS I.ROOT-SERVERS.NET.
I.ROOT-SERVERS.NET. 3600000   A   192.36.148.17
.               3600000   NS J.ROOT-SERVERS.NET.
J.ROOT-SERVERS.NET. 3600000   A   198.41.0.10
.               3600000   NS K.ROOT-SERVERS.NET.
K.ROOT-SERVERS.NET. 3600000   A   193.0.14.129
.               3600000   NS L.ROOT-SERVERS.NET.
L.ROOT-SERVERS.NET. 3600000   A   198.32.64.12
.               3600000   NS M.ROOT-SERVERS.NET.
M.ROOT-SERVERS.NET. 3600000   A   202.12.27.33
```

在配置缓存域名服务器时，你应该从 InterNIC 服务器获取该文件。此处显示的版本自 1997 年 8 月以来未发生过变化，但不能保证它未来不会改变。尽管如此，在紧急情况下，你大概可以像上面那样键入该文件的内容来使其运行起来。`named` 应该会自动更新该文件（假设它确实能够联系到某个根域名服务器）。

`nslookup` 程序执行 DNS 查询，并可用于调试 DNS 配置问题。

要启动 `nslookup`，请输入：

```bash
$ nslookup
Default Server: shishi.roaringpenguin.com
Address: 192.168.2.3
>
```

该程序会打印出它正在使用的域名服务器的名称和 IP 地址（这取自 `/etc/resolv.conf`）并提示用户输入。

要查找主机名的 IP 地址，只需输入该主机名：

```bash
> scruffy.roaringpenguin.com
Server: shishi.roaringpenguin.com
Address: 192.168.2.3
Name: scruffy.roaringpenguin.com
Address: 192.168.2.2
```

`nslookup` 会打印出你查询的主机的名称和地址。（它还会打印服务器名称和 IP 地址；从今以后我们将省略这些行。）

如果你想进行反向查找，你必须先告诉 `nslookup` 你关注的是 PTR 记录，然后输入 `in-addr.arpa` 域名：

```bash
> set type=PTR
> 1.2.168.192.in-addr.arpa
1.2.168.192.in-addr.arpa name = shevy.roaringpenguin.com
2.168.192.in-addr.arpa nameserver = shishi.roaringpenguin.com
shishi.roaringpenguin.com internet address = 192.168.2.3
```

`nslookup` 会打印出该主机的名称，以及 `2.168.192.in-addr.arpa` 域的域名服务器名称和 IP 地址。

你可以使用 `nslookup` 查看某个域的 SOA 记录：

```bash
> set type=SOA
> roaringpenguin.com
roaringpenguin.com
origin = shishi.roaringpenguin.com
mail addr = dfs.roaringpenguin.com
serial = 1999060501
refresh = 10000 (3H)
retry = 3600 (1H)
expire = 604800 (1W)
minimum ttl = 86400 (1D)
```

`set type` 命令中的类型可以是任何 RR 类型或单词 ANY。ANY 记录类型返回与主机或域名相关联的所有记录。如果你已连接到互联网，你可以对任何主机或域进行这些查找。这验证了你的域名服务器配置对于它非权威的其他域也能正常工作。在此示例中，我们从作者的网络查找出版商的信息：

```bash
> set type=ANY
> mcp.com

Non-authoritative answer:
mcp.com nameserver = NS1.IQUEST.NET
mcp.com nameserver = NS2.IQUEST.NET
mcp.com nameserver = NS2.mcp.com

Authoritative answers can be found from:
mcp.com nameserver = NS1.IQUEST.NET
mcp.com nameserver = NS2.IQUEST.NET
mcp.com nameserver = NS2.mcp.com

NS1.IQUEST.NET internet address = 198.70.36.70
NS2.IQUEST.NET internet address = 198.70.36.95
NS2.mcp.com internet address = 204.95.224.200
```

要退出 `nslookup`，请输入文件结束字符（通常是 Ctrl-D）。

有关 `nslookup` 的更多信息，请参见手册页 `nslookup(8)`。

# 摘要

在本章中，你学习了 DNS 如何作为一个全球分布式数据库进行设置。你学习了 DNS 查询是如何执行的，以及域名服务器缓存对于高效的 DNS 运行至关重要。接下来，你了解了各种 DNS 记录类型，以及如何在 Linux 上设置 `named` DNS 服务器。最后，你学习了如何使用 `nslookup` 进行交互式 DNS 查询。

![](img/df365d352a104b50fea29e59a052de4d_344_0.png)
![](img/df365d352a104b50fea29e59a052de4d_344_1.png)

# 配置 PPP

## 本章内容

- PPP 背景 308
- 串行端口配置 309
- 运行 pppd 310
- 使用 chat 建立连接 312
- IP 配置选项 314
- PPP 认证 314
- 连接到 ISP 316
- 设置拨入 PPP 服务器 317
- 通过 PPP 链路路由 319
- 自动启用 PPP 链路 320
- kppp 324

大多数人没有享受高速互联网连接的奢侈条件。相反，他们依赖通过电话线路的调制解调器连接来访问互联网。

PPP（点对点协议）是一种在串行线上传输数据包的网络协议。以太网通常用于连接彼此靠近的计算机，而串行线通常用于连接相距甚远的网络。PPP 需要廉价的硬件（串行端口、调制解调器和电话线）来提供两个网络之间或本地网络与互联网之间的连接。

使用 PPP，Linux 既可以用作拨号客户端，也可以用作拨入服务器。因此，Linux 机器可以作为网关，将本地网络连接到互联网，或为拨入用户提供远程访问服务。

## PPP 背景

PPP 是一个相当复杂的协议。除了处理 IP 流量外，PPP 还为其他网络协议（如 Novell 的 IPX 和 AppleTalk）提供了规定。我们将集中讨论如何在 PPP 链路上路由 IP 流量。

PPP 由一整套协议组成。最低层是高级数据链路控制（HDLC），它定义了原始 PPP 数据帧的帧格式并提供校验和。HDLC 是一个国际标准，类似于原始以太网帧。

链路控制协议（LCP）位于 HDLC 之上。它负责协商与数据链路本身相关的选项，例如 MTU 以及双方是否应定期发送回显请求以确定链路是否仍然处于活动状态。

对于 PPP 链路上支持的每种网络协议，都有相应的控制协议。例如，对于 IP 链路，有互联网协议控制协议（IPCP），它协商 IP 链路的各个方面，例如双方将使用哪个 IP 地址。

Linux 的 PPP 实现分为两部分。在内核中，低层 PPP 驱动程序处理 HDLC 帧处理以及数据包的实际传输和接收。`pppd` 程序（它是一个普通程序——不是内核的一部分）处理选项协商、认证等。`pppd` 相当复杂，具有许多选项；我们将讨论其中最常见的选项。在你阅读完本章并理解 PPP 如何工作后，你应该能够在使用手册页 `pppd(8)` 之后对 `pppd` 进行微调。

## 串行端口配置

要使用 PPP，你必须配置计算机上的串行端口。Linux 中的串行端口命名为 `/dev/ttyS#`。例如，第一个串行端口（对应于 DOS 的 COM1:）是 `/dev/ttyS0`，第三个串行端口是 `/dev/ttyS2`。

### 串行硬件

Linux 支持标准的 PC 串行端口硬件以及用于将许多调制解调器连接到远程访问服务器的多端口串行板。在本书中，我们只讨论标准的 PC 串行硬件。

标准 PC 串行端口支持 RS-232 串行标准。这是一个广泛使用的标准，规定了串行端口上各种信号的含义及其电压级别。

串行链路至少需要三根线：用作电压参考的地线、用于发送数据的线以及用于接收数据的线。由于串行端口相对较慢，因此使用额外的线进行流量控制：调制解调器可以要求计算机暂停发送，以免丢失数据。类似地，计算机可以要求调制解调器停止向它发送数据。实现此目的的线条称为清除发送（CTS）和请求发送（RTS）。出于此原因，RS-232 硬件流量控制有时被称为 RTS/CTS。

调制解调器使用额外的线来表示载波的存在。通常，如果载波丢失，计算机应该挂断调制解调器并断开链路。

从 PC 端来看，串行端口有一个 I/O 地址和 IRQ 线。I/O 地址是计算机用于发送或接收数据的地址。IRQ（中断请求）线用于在收到数据时通知计算机。

串行端口上有一个称为 UART 的特殊芯片，它负责将串行数据转换为计算机可读的并行数据，反之亦然。几乎所有调制解调器串行数据都使用 16550A 芯片（或其克隆芯片）。旧计算机可能使用 16450 芯片。16550A 有一个 16 字节的缓冲区，使其可以比 16450 运行得更快。

大多数内置调制解调器模拟串行端口。从计算机的角度来看，内置调制解调器只是另一个串行端口。

![](img/df365d352a104b50fea29e59a052de4d_346_0.png)

