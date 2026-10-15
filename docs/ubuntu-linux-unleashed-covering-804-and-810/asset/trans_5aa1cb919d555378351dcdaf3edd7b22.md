

## DHCP 的其他用途

dhcpd.conf 中可以使用大量选项：整本书都专门讲解 DHCP！最全面的书籍是《The DHCP Handbook》，可在 http://www.dhcp-handbook.com/ 获取。你可以定义 NIS 域、配置 NETBIOS、设置子网掩码、定义时间服务器，或许多其他类型的服务器——仅举几个可用的 DHCP 选项。前面示例将使你的 DHCP 服务器和客户端运行起来。

DHCP 服务器发行版包含一个可作为网络模板使用的 dhcpd.conf 文件示例。该文件展示了基本配置，可帮助你入门并对所用选项进行说明。

## 无线网络

如前所述，Linux 自 1990 年代初首个标准制定以来就支持无线网络。随着计算机越来越小，无线网络的使用日益增加；与此同时，传输速度也在不断提高。有多种方式可以创建无线网络。以下各节将介绍可在 Ubuntu 系统上用于初始化、配置和管理无线网络的多个 Linux 命令。

### Ubuntu 中对无线网络的支持

随 Ubuntu 发货的 Linux 内核为无线网络提供了广泛支持。用于配置、管理和显示无线连接信息的相关无线工具包括

- iwconfig—设置无线网络接口的网络名称、加密、传输速率和其他功能
- iwlist—显示无线接口的信息，例如速率、功率电平或使用的频率
- iwpriv—使用它来设置无线网络接口的可选功能，例如漫游
- iwspy—显示多个节点的无线统计信息

无线设备的支持程度各不相同，但大多数现代（即 2005 年后）的无线设备都应能与 Ubuntu 配合使用。一般来说，Linux 无线设备软件（通常以内核模块形式存在）支持创建可由传统接口工具（如 ifconfig）管理的以太网设备——无线设备的无线功能由各种无线软件工具管理。

例如，当无线网络设备首次被识别并初始化使用时，驱动程序很可能会报告一个新设备：

```
zd1211rw 5.4:1.0: firmware version 4725
zd1211rw 5-4.1.0: zd1211b chip 056d:705c v4810 \
high 00-17-3f AL2230_RF pa0 g--NS
zd1211rw 5-4.1.0: eth2
usbcore: registered new interface driver zd1211rw
```

此输出（来自 dmesg 命令）显示 eth2 设备已被报告。如果使用 DHCP，设备应自动加入最近的无线子网并自动分配 IP 地址。如果不使用，则下一步是使用 iwconfig 等无线工具设置无线设备的各种参数。iwconfig 命令连同设备名称（本例中为 eth2）将显示状态：

```
$ iwconfig eth2
eth2      IEEE 802.11b/g  ESSID:"SKY35120"  Nickname:"zd1211"
          Mode:Managed  Frequency:2.462 GHz  \
          Access Point: 00:18:4D:06:8E:2A
          Bit Rate=24 Mb/s
          Encryption key:0EFD-C1AF-5CBD-B2C6-7A89-3790-07A7-AC64-0AB5\
-C36E-D1E9-A230-1D89-2D27-2E86-0D6B  Security mode:open
          Link Quality=100/100  Signal level=-82/100
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:0  Missed beacon:0
```

此示例显示了与名为 SKY35120 的网络的 24Mbps 连接。要更改参数，例如传输速率，请使用 iwconfig 命令的命令行选项，如下所示：

```
$ sudo iwconfig eth0 rate 11M
```

iwconfig 命令支持的其他选项包括 essid，用于按名称将 NIC 设置为连接到特定网络；mode，用于使 NIC 自动从接入点检索设置或连接到另一台无线主机；或 freq，用于设置通信使用的频率。其他选项还包括 channel、frag、enc（用于加密）、power 和 txpower。这些选项的详细信息和示例可在 iwconfig 手册页中找到。

然后你可以使用 ifconfig 命令或 Ubuntu 的图形工具设置设备网络参数，接口将像有线局域网一样工作。iwconfig 命令的一个方便输出是链路质量输出，可用于 shell 脚本或其他图形实用程序以进行信号监控。

### 无线网络的优势

无线网络的优势在于其移动性和潜在覆盖范围。如果拥有足够大的天线网络，你的网络可延伸数英里。这将是一个昂贵的网络，但它很容易突破办公室的砖石限制。

