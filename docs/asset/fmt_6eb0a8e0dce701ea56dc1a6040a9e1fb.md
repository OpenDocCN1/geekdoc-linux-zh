
transproxy 程序将接收旨在到达外部服务器的所有连接，并将它们传递给本地代理（修复差异）。

## 7.9. IPv6

正当你认为开始理解 IP 网络时，规则改变了！IPv6 是互联网协议第 6 版本的缩写。开发 IPv6 主要是为了克服互联网社区的担忧。用户担心没有足够的 IP 地址可以分配。IPv6 地址长度为 16 字节（128 位）。IPv6 包含了一些变化，大部分是简化，这将 IPv6 网络比 IPv4 网络更易管理。

Linux 在 2.2 * 系列内核中已经有了可工作（但不完整）的 IPv6 实现。

## 7.10. IPv6 Linux 资源

- IPv6–HOWTO
- Linux IPv6
- Linux IPv6 RPM 项目
- IPv6 FAQ/HOWTO

## 7.11. 移动 IP (Mobile IP)

“IP 移动性”术语描述了主机将其网络连接从互联网一点移动到另一点（而不更改 IP 地址或丢失连接）的能力。通常当 IP 主机更改连接点时，它也会更改其 IP 地址。IP Mobility 通过为移动主机分配固定 IP 地址来解决这个问题。它还使用 IP 封装（隧道）和自动路由来确保数据目标路由到它当前使用的实际 IP 地址。

一个项目正在为 Linux 提供完整的 IP 移动工具集。可以从以下位置获取这些工具。

## 7.12. 多组播 (Multicast)

IP 多组播允许不同 IP 网络上的任意数量 IP 主机同时接收 IP 数据报。这种机制被用于提供互联网“广播”材料，以及音频和视频传输以及其他新应用。

内核选项：

```
网络选项 --->
[*] TCP/IP 网络
...
[*] IP: 多组播
```

需要一组工具和一些细微的网络配置。请查看 Multicast–HOWTO 获取更多关于 Linux 支持多组播的信息。

## 7.13. 流量整形器 (Traffic Shaper) – 修改允许的带宽

流量整形器是一种创建新接口设备的驱动程序。这些设备可以以用户定义的方式对流量进行限制。它们依赖物理网络设备进行实际传输，并可以作为网络流量的输出路由。

流量整形器在 Linux–2.1.15 中引入，并被反移植到 Linux–2.0.36（出现在 2.0.36-pre-patch-2 中），该版本由流量整形器设备作者、Linux–2.0 维护者 Alan Cox 分发。

流量整形器只能作为模块编译。它通过 `shapeifcfg` 程序进行配置。相关命令如文所示：

```
shapeifcfg attach shaper0 eth0
shapeifcfg speed shaper0 64000
```

整形器设备只能控制出站流量的带宽（因为数据包是通过整形器传输的；仅根据路由表）。在使用 Linux 路由器时，`按源地址路由`功能有助于限制特定主机的总带宽。

Linux–2.2 已经支持这种路由方式。如果你在 Linux–2.0 上需要此功能，请检查 ftp.invlogic.com 上 Mike McLagan 提供的补丁。请参考 Documentation/networking/shaper.txt 获取有关整形器的更多信息。

如果你想尝试对入站数据包进行（实验性的）整形，请尝试 ftp.system.it 的 rshaper–1.01（或更高版本）。本节是否有帮助？为什么不捐赠 $2.50 呢？

## 章 DHCP 和 DHCPD

DHCP 是动态主机配置协议（Dynamic Host Configuration Protocol）的缩写。DHCP 的出现使得在多个主机上配置网络变得简单。你不需要单独配置每个主机，而是可以通过 DHCP 服务器分配所有常用的主机参数。

每当主机启动时，都会向网络广播一个数据包。该数据包向位于同一段的任何 DHCP 服务器发出请求，以配置主机。

DHCP 在分配每个主机的 IP 地址、子网掩码和网关等项目中非常有用。

### 8.1. LinuxConf 用户的 DHCP 客户端设置

当你进入 Linux 时，以 "root" 用户身份登录，启动 linuxconf 程序。该程序带有所有版本的 redhat，并可与 X Caldera 配合使用。它也适用于 SuSe 和 Caldera。

选择网络 (Networking)

基础主机信息 (Basic Host Information)

选择启用 (Select Enable)

设置配置模式 (Set Config Mode) DHCP

本节是否有帮助？为什么不捐赠 $2.50 呢？

### 8.2. Linux DHCP 服务器设置

获取 DHCPD（如果机器尚未安装）。获取 DHCP。

注意：确保你在内核中已启用多播 (MULTICAST)。

如果你的 Linux 版本没有二进制发行版，则必须手动编译 DHCP。

编辑 `/etc/rc.d.local` 以反映针对 255.255.255.255 的路由添加。

为了让 DHCP 与挑剔的客户端（例如 Windows 95）正常工作，它必须能够发送目标 IP 地址为 255.255.255.255 的包。不幸的是，Linux 坚持将 255.255.255.255 修改为子网广播地址（在这种情况下，地址将变为 192.5.5.223）。这导致了违反 DHCP 协议。虽然许多 DHCP 客户端不会注意到这个问题（例如所有的微软 DHCP 客户端），但它们会识别出违规行为。出现此问题的客户端似乎看不到来自服务器的 DHCPPOFFER 消息。

以 root 身份输入以下：

```
route add --255.255.255.255 eth0
```

如果出现消息：

# Linux Networking HOWTO

255.255.255.255: Unknown host

尝试在你的 `/etc/hosts` 文件中添加以下条目：

255.255.255.255 dhcp

然后，尝试：

```
route add --host dhcp dev eth0
```

### 8.2.1. DHCPD 选项

现在你需要配置 DHCPd。为了做到，你需要创建或编辑 `/etc/dhcpconf.conf`。在 linuxconf 下有一个 dhcpd 配置的图形化界面。这使得配置和管理 DHCPD 变得极其简单。

如果你想手动配置，应遵循下面的说明。我建议一次性手动配置。这有助于进行 GUI 无法提供的诊断工作。不幸的是，微软并不相信这一点！

分配 IP 地址的最简单方法是随机分配。下面显示了一个显示此类设置的示例配置文件：

```
# Sample /etc/dhcpd.conf
# (在此处添加你的注释)
default-lease-time 1200;
max-lease-time 9200;
option subnet-mask 255.255.255.0;
option broadcast-address 192.168.1.255;
option routers 192.168.1.254;
option domain-name-servers 192.168.1.1, 192.168.1.2;
option domain-name "mydomain.org";
subnet 192.168.1.0 netmask 255.255.255.0 {
  range 192.168.1.100 192.168.1.200;
  option subnet-mask 255.255.255.0;
  option broadcast-address 192.168.1.255;
  option routers 192.168.1.254;
  option domain-name-servers 192.168.1.1, 192.168.1.2;
}
```

## 9.2. 使用新的 ip 工具添加路由

在上一节中，我们谈论了路由表，并讨论了该列表的基本含义。坦率地说，输出结果与你手动实现精确路由表时将使用的语法非常相似。

```
ip route add 207.149.43.62 dev eth0 scope link
ip route add 207.149.43.0/24 dev eth0 proto kernel scope src 207.149.43.62
ip route add 127.0.0.0/8 dev lo scope link
ip route add default via 207.149.43.1 dev eth0
```

如你所见

**注意：** 我们意识到路由 2.2 的文档极度缺乏细节。我认为**每个人**都意识到了！如果你在在这方面有任何经验，请通过以下邮箱与我们联系：poet@linuxports.com 我们希望获得任何可能帮助我们加强文档的信息！

本节对你有帮助吗？为什么不捐赠 2.50 美元呢？

## 9.3. 在内核 2.2 中使用 NAT

网络地址转换（NAT）功能几乎是 IP 伪装（IP Masquerade）功能的标准“大哥”。它在 RFC-1631（可在你最近的 RFC 归档中找到）中有详细说明。NAT 提供了 IP 伪装所具备的功能（这使其完全适用于企业防火墙路由器和更大规模的实现）。

Michael.Hastenstein 为 Linux 2.0.29 内核开发了 NAT 的 alpha 实现。Michael.Hasten@informatik.tu-chemnitz.de。Michael 的文档和实现可以从以下处获取：

Linux IP Address Web Page

Linux 2.2 内核改进的 TCP/IP 栈内置了 NAT 功能。这项功能似乎被 Michael Hastenstein 认为已经过时（Michael.Hasten@informatik.tu-chemnitz.de）。

要让其工作，你需要在内核中启用 `CONFIG_IP_ADVANCED_ROUTER`、`CONFIG_IP_MULTIPLE_TABLES`（作为路由）以及 `CONFIG_IP_ROUTE_NAT`（即 NAT）。如果你想使用细粒度的 NAT 规则，可能需要开启防火墙（`CONFIG_IP_FIREWALL`）和 `CONFIG_IP_ROUTE_FWMARK`。要实际操作这些内核功能，你需要来自 ftp://ftp.in.ac.ru/ip-routing/ 的 Alexei Kuznetsov 的“ip”路由。

入站数据报 NAT

现在，使用以下命令来翻译入站数据报的地址：

```
ip route add nat <ext-addr>/<masklen> via <int-addr>
```

# Linux 网络 HOWTO

这将使目标为“ext-addr”（从外部互联网可见的地址）的入站数据包的目的地址重写为“int-addr”（你内部网络中、位于网关/防火墙后的地址）。然后数据包将根据本地路由表进行路由。你可以翻译单个主机地址或整个地址块。示例如：

```
ip route add nat 195.113.148.34 via 192.168.0.2
ip route add nat 195.113.148.32/27 via 192.168.0.0
```

第一个命令将使内部地址 192.168.0.2 可以作为 195.113.148.34 使用。第二个示例显示了将地址块 192.168.0.0–31 映射到 195.113.148.32–63。

## 第 10 章 内核 2.2 IP 命令参考

(进行中)

### 10.1. ip

如果你安装了 iproute2 工具，执行 ip 命令将显示基本语法。

```
[root@id4 Net4]# ip OBJECT | COMMAND | help
用法: ip [ 选项 ] OBJECT { COMMAND | addr | neigh | tunnel |
where OBJECT := { link | addr | monitor |
OPTIONS := { -V[version] | -s[statistics] | -r[resolve] | -f[family] { inet | inet6 | dnet | link } | -o[eline] }
```

- -V，打印你正在使用的 ip 版本并退出。
- -s，获取有关指定设备的更多输出。你可以多次使用此选项以增加显示的信息量。
- -f，后接协议标识符，如：inet, inet6 或 link。指定要使用的协议。使用 IPv4（例如，当前 Internet），inet6 使用 IPv6（地面，从未实现的 Internet），以及 link（物理链路）。如果你不提供该选项，将对协议进行猜测。如果有足够的信息，它将退回到默认值。
- -o，用单行显示每个设备记录。
- -r，使用系统解析器（例如 DNS）打印实际数字。OBJECT 是从中检索信息的对象（设备），你也可以管理该设备。类型有：
- 网络设备，例如；eth0 或 ppp0
- 指定设备上的 IP (IPv4 或 IPv6) 地址。
- neigh ARP 或 NDIS 缓存。
- route 路由表条目。
- rule 数据库中的规则。
- address 多播地址。
- route 多播路由缓存。
- tunnel 是否通过 IP 建立隧道。

## 第 11 章 使用常用 PC 硬件

### 11.1. ISDN

集成业务数字网络（ISDN）是一系列指定通用数字网络的标准。ISDN 通话创建一个同步点对点数据服务。通常通过高速链路提供。这种服务可以提供电话（通过数字化语音）或数据服务到你的家庭或企业。在这种情况下，客户不需要进行任何特殊更改。

内核编译选项：

```
ISDN subsystem -->
<*> ISDN 支持
[ ] 支持同步 PPP
[ ] 支持通过 ISDN 的音频
<> ICN 2B 和 4B 支持
<> PCBIT-D 支持
<> Teles/NICCY1016PC/Creatix 支持
```

ISDN 实现支持多种类型的内部 ISDN 卡。这些列在内核配置中：

- ICN 2B 和 4B
- 八路 PCBIT-D
- Teles ISDN 卡及兼容卡

某些卡需要下载软件才能运行。有一个独立的实用程序允许下载到：

有关如何配置 ISDN 服务的详细信息可以从 `/usr/src/linux/Documentation/isdn/` 获取。你也可以查看针对 isdn4linux 的常见问题解答：它是

# Linux 网络 HOWTO

可在 www.lrz-muenchen.de 获取。（您可以点击英文国旗以获取英文版本）。

关于 PPP 的说明。PPP 协议族可以在异步或同步串行线上运行。Linux 常用的分发 PPP 守护进程 `pppd` 仅支持异步模式。如果你想在你的 ISDN 服务上运行 PPP 协议，你需要一个经过特殊修改的版本。关于在哪里找到该版本的详细信息，请参阅上述的文档。本节对你有帮助吗？为什么不捐赠 $2.50 ？

## 11.2. Linux PLIP–2.0

PLIP 设备名称为 `plip0`、`plip1` 和 `plip2`。

### 内核编译选项：

```
Network device support --->
<*> PLIP (parallel port) support
```

PLIP（并行线 IP）与 SLIP 类似，它们都用于在两台机器之间提供点对点网络。然而，你可以使用机器上的并行打印端口。它不使用串口端口（本文后文的接线图中包含一张接线图）。由于并行端口可以一次传输多个位，因此可以使用 PLIP 接口获得更高的速度。PLIP 获得的速度将高于使用标准设备的速度。此外，即使是最简单的并行打印端口也可以使用（而无需你为你的串口购买相当昂贵的 16550AFN）。PLIP 使用大量的 CPU 来转换为串行链路。例如，如果你能获得一些网卡，那么它不是一个好的选择。但是，当所有资源都可用时，它可以工作（而且运行得相当不错）。当链路运行时，你应该获得大约每秒 20 千字节的数据传输率。

PLIP 驱动程序与并行设备驱动程序竞争并行端口硬件。如果你想同时使用这两个驱动程序，应该将它们编译为模块。这确保了你能够选择想要用于 PLIP 的端口，并可以为打印机驱动程序选择哪些端口。有关内核模块配置的更多信息，请参阅“Modules-HOWTO”。
