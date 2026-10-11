
# Linux 词典

## 点对协议 (PPP) 守护进程
点对协议 (PPP) 提供了一种在串口链路上传输数据报的标准方法，以及链路两端机器的一种标准方法。

链接（“对等节点”）用于协商链路的可选特性。通过 PPP，可以使用串行链路传输 Internet 协议（IP）数据报，允许在对等节点之间建立 TCP/IP 连接。此包内置了 `ppp` PAM 支持，因此 `ppp-pam` 软件包已过时。来自 Debian 3.0r0 APT `http://www.ldp.org/LDP/Linux-Dictionary/html/index.html`。

## PPP
点对点协议（PPP）。源自 Redhat–9–Glossary `http://www.ldp.org/LDP/Linux-Dictionary/html/index.html`。

`PPP` 软件包包含 `PPP`（点对点协议）守护进程和 `PPP` 支持。`PPP` 协议提供了一种在串行点对点链路上传输数据报的方法。`PPP` 通常用于通过调制解调器（调制号器）和电话线拨接入 ISP（互联网服务提供商）或其他机构。源自 Redhat 8.0 RPM `http://www.ldp.org/LDP/Linux-Dictionary/html/index.html`

### PPP (接入点)
ISP 或其他服务的实际所在地。源自《距离教育与互联网术语字典》`http://www.ldp.org/LDP/Linux-Dictionary/html/index.html`

### PPP 点对点
这是通过拨号电话连接将计算机直接到互联网的两种标准之一之一（另一种是 SLIP）。与 SLIP 协议不同，`PPP` 包含了更优的数据协商、压缩和纠错。然而，这些功能为数据和传输增加了开销，当发送和接收端的调制解调器都处理硬件纠错和在线数据修正时，这些功能是不必要的。参见 Linux Internet 协议 (SLIP)。源自 QueCIC `http://www.ldp.org/LDP/Linux-Dictionary/html/index.html`

### PPP (点对点)
最常用的协议，允许计算机使用普通电话线和调制解调器将家庭计算机连接到互联网，建立 TCP/IP 连接并真正真正地接入互联网。源自 Matisse `http://www.ldp.org/LDP/Linux-Dictionary/html/index.html`

通过调制解调器连接到 ISP 的标准协议。“点对点”一词用于将此技术与之前基于“多点”通信的技术进行对比。例如，流行的以太网技术被用于连接单个局域网中的许多计算机。关键：嗅探 PPP 拨号连接非常困难，几乎从没有这样做。源自 Hacking-Lexicon `http://www.ldp.org/LDP/Linux-Dictionary/html/index.html`

这种使用调制解调器实现的相当高速的直接互联网连接。与早期的连接方法（许多人在使用）不同，`PPP` 不受主机计算机现有软件的限制。通过 `PPP`，所有客户端软件（如 Netscape）均在本地计算机上运行。源自 Faculty–of–Education `http://www.ldp.org/LDP/Linux-Dictionary/html/index.html`

一个用于配置 `ppp` 的文本菜单实用。它在每一步都提供解释。`pppconfig` 支持 PAP、CHAP 和身份验证方法。它使用标准的 `ppp` 配置文件，并将 `ppp` 设置为标准的 `pof` 和 `po` 命令以控制 `ppp`。源自 Debian 3.0r0 APT `http://www.ldp.org/LDP/Linux-Dictionary/html/index.html`。

## pppconfig
配置 `pppd`。源自 What `http://www.ldp.org/LDP/Linux-Dictionary/html/index.html`。

## pppd
点对点协议守护进程。源自 whatis `http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

`PPPD`
点对点协议守护进程（PPP）。源自 VERA `http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

`pppdcapliugin`
用于 `pppd` 与具备 CAPI 能力的 ISDN 卡通信的插件。某些 ISDN 卡（特别是 AVM precisa，当加载 AVM 网站时）被 CAPI 实用程序使用。这是一个插件供 `pppd` 守护进程在此类网卡上使用 CAPI 的插件。

查看 `/usr/share/doc/pppdcapliugin/*` 获取某些（基础的）信息。源自 Debian 3.0r0 APT `http://www.ldp.org/LDP/Linux-Dictionary/html/index.html`

`pppdump`
将 PPPD 记录文件转换为可读格式。源自 whatis `http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

`PPPoE`
在以太网帧内部封装 PPP 流的技术。这种技术正在被高速互联网接入提供商（电缆调制解调器、xdsl 等）部署，以便解码来自 ISP 服务的带宽供应。源自 Linux Guide @FirstLinux `http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

`PPPoE`-基于以太网的点对点协议 [协议] (ADSL, RFC 2516)，“PPPoE”。源自 VERA `http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

`pppoe`
以太网上的 PPP 驱动。以太网上的 PPP (`PPPoE`) 是许多互联网服务提供商使用的协议。此包允许你连接到 `PPPoE` 服务提供商。源自 Debian 3.0.r0 APT。

用户空间 `PPPoE` 客户端。源自 Debian 3.0.r0 APT

`pppoe-relay`
用户空间 `PPPoE` 代理。源自 Debian 3.0.r0 APT

`pppoe-server`
用户空间 `PPPoE` 服务器。源自 whatis `http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

`pppoe-sniff`
用户空间 `PPPoE` 帧。源自 whatis `http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

`pppoconf`
配置 `PPPoE` (ADSL)。源自 whatis `http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

配置 `PPPoE` (ADSL)。源自 Debian 3.0r0 `http://www.tldp.org/LDP/Linux-Dictionary/html/index.html` `http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

`ppstats`
打印 PPP 统计信息。源自 whatis `http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

`ppstatus`
基于控制台的 PPP 监控，包括状态、时间、TX/RX 接口等。源自 Debian 3.0r0 APT `http://www.ldp.org/LDP/Linux-Dictionary/html/index.html`

# PPS

## Linux 词典
每秒数据包。源自 VERA `http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

- `PPS`
并行处理系统。源自 VERA `http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

- `PPS`
生产。源自 VERA `http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

- `PPS`
公共包交换 [网络]。源自 VERA `http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

- `PPSN`
公共包交换网络。源自 VERA `http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

- `PPU`
个人打印机池化工具。源自 VERA `http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

- `pphtml`
