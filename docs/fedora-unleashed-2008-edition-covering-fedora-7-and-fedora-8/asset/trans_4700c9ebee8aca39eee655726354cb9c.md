

这行代码定义了特殊的 `localhost` 接口，并将其 IP 地址分配为 `127.0.0.1`。你可能会听到或读到诸如 `localhost`、`loopback` 和 *dummy interface*（虚拟接口）等术语；所有这些术语都指代 IP 地址 127.0.0.1 的用途。术语 `loopback interface` 表示对于 Linux 网络驱动程序而言，这看起来就像机器正在与仅由一台机器组成的网络进行通信；内核在同一台计算机上向自身发送和接收网络流量。*虚拟接口* 表示从外部世界的角度来看，该接口实际上并不存在；它仅对本地机器存在。

局域网（LAN）中每台联网的 Fedora 计算机都将使用相同的 IP 地址作为其 `localhost`。如果由于某种原因 Fedora 计算机没有此接口，请编辑 `/etc/hosts` 文件以添加 `localhost` 条目，然后使用 `ifconfig` 和 `route` 命令以 root 身份创建该接口，操作如下：

```
# ifconfig lo 127.0.0.1
# route add 127.0.0.1 lo
```

这些命令在内存中创建了 `localhost` 接口（所有接口，例如 `eth0` 或 `ppp0`，都是在 Linux 中通过内存创建的），然后将 IP 地址 `127.0.0.1` 添加到一个内部（内存中）的表中，以便 Linux 内核的网络代码可以跟踪到不同地址的路由。

使用前面所示的 `ifconfig` 命令来测试该接口。此时你应该能够使用 `ping` 来检查接口是否正常运行，如下所示（使用 `localhost` 或其 IP 地址均可）：

```
$ ping -c 3 localhost
PING localhost.localhost (127.0.0.1) from 127.0.0.1: 56(84) bytes of data.
64 bytes from localhost.localhost (127.0.0.1): icmp_seq=0 ttl=255 time=212 \usec
64 bytes from localhost.localhost (127.0.0.1): icmp_seq=1 ttl=255 time=80 usec
64 bytes from localhost.localhost (127.0.0.1): icmp_seq=2 ttl=255 time=50 usec

--- localhost.localhost ping statistics ---
3 packets transmitted, 3 packets received, 0% packet loss
round-trip min/avg/max/mdev = 0.050/0.114/0.212/0.070 ms
```

`-c` 选项用于设置 ping 的次数，如果命令成功（如前所述），它将返回有关发送到指定主机的测试数据包往返速度的信息。

## 使用 TCP/IP 进行网络通信

任何基于 UNIX 主机的网络的基本构建模块都是由三个协议组成的 *传输控制协议/互联网协议（TCP/IP）* 套件。该套件由 *互联网协议（IP）*、*传输控制协议（TCP）* 和 *用户数据报协议（UDP）* 组成。IP 是基础协议。TCP/IP 套件是 *基于数据包的*，这意味着数据在发送端被分解成小块以便传输到接收端。将数据分解为可管理的数据包可以实现更快、更准确的传输。在 TCP/IP 中，所有数据都通过 IP 数据包传输，这就是为什么地址被称为 IP 地址的原因。它是该套件的最低层。

TCP 是一种基于连接的协议。在两台机器之间传输数据之前，必须先建立连接。建立连接后，数据流会被发送到 IP，进而被分解为数据包并进行传输。在接收端，数据包会被重新排序并发送到正确的应用程序端口。TCP/IP 构成了互联网的基础；没有它，互联网将会是完全不同的样子，甚至可能根本不存在！

另一方面，UDP 是一种无连接协议。使用该协议的应用程序只需选择其目标并开始发送即可。UDP 通常用于小量数据或在快速可靠的网络上。如果你有兴趣了解 TCP/IP 的内部机制，请参阅本章末尾的“参考文献”部分，寻找更多相关信息。

## Fedora 与网络

你的网卡很可能在 Fedora 安装过程中已经配置好了。然而，你可以使用 shell 提示符下的 `ifconfig` 命令或 Fedora 的图形化网络配置工具（例如 `system-config-network`）来编辑系统的网络设备信息，或添加/移除系统中的网络设备。Fedora 附带数百个网络命令和实用工具——本章无法涵盖所有这些内容，其数量足以编写两三卷书。

几乎所有以太网卡都可以与 Linux 一起使用，许多 PCMCIA 有线和无线网络卡也是如此。好消息是，许多 USB 无线网卡也能在 Linux 上正常工作，而且随着 Linux 内核新版本的出现，更多设备将获得支持。请访问 http://www.linux-usb.org/ 查看 Linux USB 项目的最新进展或验证对你的设备的支持情况。

阅读完本章后，你可能想进一步了解用于 Linux 的其他图形化网络客户端。例如，GNOME etherpeak 客户端可用于监控局域网（LAN）上的所有流量或特定类型的流量。另一个客户端 NmapFE 可用于扫描特定主机的开放端口和其他运行中的服务。

## 高级无线网络

如前所述，自 1990 年代初制定第一项标准以来，Linux 就一直支持无线网络。随着计算机变得越来越小，无线网络的用途日益增加；同时，传输速度也一直在提高。创建无线网络有几种不同的方法。以下几节将介绍你可以在 Fedora 系统上用于初始化、配置和管理无线网络的若干 Linux 命令。

### Fedora 对无线网络的支持

Fedora 附带的 Linux 内核提供了对无线网络的广泛支持。用于配置、管理或显示无线连接信息的相关无线工具包括：

- **`iwconfig`**——设置无线网络接口的网络名称、加密、传输速率及其他功能
- **`iwlist`**——显示无线接口的信息，例如速率、功率级别或使用的频率
- **`iwpriv`**——使用 `i` 设置无线接口的可选功能，例如漫游
- **`iwspy`**——显示多个节点的无线统计信息

无线设备的兼容性各不相同——大多数情况下是以 PCMCIA 适配器的形式出现——尽管现在一些 USB 无线设备也能与 Linux 协同工作。通常，Linux 无线设备软件（通常以内核模块的形式存在）支持创建以太网设备，这些设备可以由传统的接口工具（例如 *ifconfig*）进行管理——而设备的无线功能则由各种无线软件工具管理。

例如，当首次识别并初始化无线网络设备以供使用时，驱动程序通常会报告一个新设备：

```
wlan_cs: WaveLAN/IEEE PCMCIA driver v1.0.6
wlan_cs: (c) Andreas Neuhaus <and@yafsta.fh-dortmund.de>
wlan_cs: index 0x01: Vcc 3.3, irq 3, io 0x0100-0x013f
wlan_cs: Registered netdevice eth0
wlan_cs: MAC address on eth0 is 00 05 5d f3 1d da
```

此输出（来自 *dmesg* 命令）显示 *eth0* 设备已被报告。如果使用了 DHCP，该设备应自动加入最近的无线子网并被自动分配 IP 地址。如果没有，下一步是使用 *iwconfig* 等无线工具来设置无线设备的各种参数。*iwconfig* 命令加上设备名称（本例中为 *eth0*）会显示状态：

```
# iwconfig eth0
eth0    IEEE 802.11-DS  ESSID:"GreyUF0"  Nickname:"Prism I" 
Mode:Managed  Frequency:2.412GHz  Access Point: 00:02:2D:2A:FE:3C 
Bit Rate:2Mb/s  Tx-Power=15 dBm  Sensitivity:1/3
RTS thr:off  Fragment thr:off 
Encryption key:off 
Power Management:off 
Link Quality:92/92 Signal level:-11 dBm Noise level:-102 dBm 
Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0 
Tx excessive retries:0  Invalid misc:4  Missed beacon:0
```

此示例显示了一个连接到名为 `GreyUFO` 的网络的 2Mbps 连接。要更改参数（例如传输速率），请使用 `iwconfig` 命令的行选项，如下所示：

```
# iwconfig eth0 rate 11M
```

`iwconfig` 命令支持的其他选项包括 `essid`，用于按 *名称* 设置网卡连接到特定网络；*mode*，用于启用网卡从接入点自动获取设置或连接到另一个无线主机；以及 *freq*，用于设置用于通信的频率。其他选项还包括 *channel*、*frag*、*enc*（用于加密）、*power* 和 *txpower*。这些选项的详细信息和示例请参阅 `iwconfig` 手册页。

然后你可以使用 `iwconfig` 命令或可能的图形化 Fedora 工具来设置设备网络参数，该接口将像有线局域网一样工作。`iwconfig` 命令的一个有用输出是链路质量输出，可用于 shell 脚本或其他图形工具中进行信号监控目的（有关示例，请参阅第 15 章“使用 SSH 进行远程访问”）。

## TCP/IP 寻址

要理解在 Linux 上进行网络通信，你需要了解 TCP/IP 寻址的基础知识。互联网 IP 地址由美国互联网号码分配机构（American Registry for Internet Numbers，ARIN）分配（适用于美国及部分其他主机），该机构位于 <http://www.arin.net/>。该机构向 *互联网服务提供商*（ISP）分配一个或多个 IP 地址块，然后 ISP 可以将其分配给其用户。

你会很快认出当前的 TCP/IP 寻址形式，即 IPv4（IP 版本 4）。在此方法中，TCP/IP 地址表示为一系列四个十进制数——一个 32 位值，以点分十进制格式表示，例如 192.168.120.135。每组数字称为一个 *八位字节*（八个 1 和 0，例如 10000000 表示 128），范围从 0 到 255。

第一个八位字节通常决定网络所属的 *类别*。网络分为以下三个类别：

- **A 类**——由第一个八位字节范围从 1 到 126 的网络组成。只有 126 个 A 类网络——每个网络由最多 16,777,214 个主机组成。（如果你正在做数学题，潜在共有 16,777,216 个地址，但地址的主机部分不能全为零或 255。）“10.” 网络保留用于本地网络使用，“127.” 网络保留用于 *环回* 地址 127.0.0.1。

> **注意**
>
> 请注意，零不包括在 A 类中。零地址用于网络之间的广播。此外，请注意还有两个其他类别的网络，即 D 类和 E 类。D 类网络保留用于多播地址，不能供网络主机使用。E 类地址被视为实验性，因此不开放用于公共寻址。

