
注意，你应该将 `0x1234567890` 替换为更具独特性的密钥。

## 27.3.3.4.2 IPSec

`ipsec(4)` 是一种用于跨网络加密数据的更强大、更强大的工具。这绝对是无线无线网络上加密数据的首选方法。你可以在本手册的 IPSec 章节阅读更多关于 `ipsec(4)` 安全以及如何实现它的信息。

## 27.3.3.5 工具

有少量工具可用于调试和设置你的无线网络，在这里我们将尝试描述其中一些工具及其功能。

### 27.3.3.5.1 bsd-airtools 包

`bsd-airtools` 软件包是一个完整的工具集，包含了用于 WEP 密钥破解、接入点检测等的无线审计工具。

`bsdtools` 实用程序将从 `net-mgmt/bsd-airtools` 安装。关于安装端口的信息可以在本手册的第 4 章中找到。

`dumper` 程序是该包中的工具，允许进行接入点发现和信噪比图表。如果你在让接入点启动运行方面遇到困难，`dumper` 可能会帮助你入门。

为了测试你的无线网络安全，你可以选择使用 "`dwutils`"（包含 `dwecrack`, `dweepump` 和 `dwekeygen`）来帮助你判断你的无线网络是否需要安全防护。

## 27.3.5.2 wicontrol, control 和 raycontrol 实用

这些是你用来控制无线网卡在无线网络上行为的工具。在上面的示例中，我们必须使用 `wicontrol(8)`，因为我们的网卡是一个 wifi 接口。如果你有一个 Cisco 无线设备，它将显示为 `an0`，因此你应该使用 `control(8)`。

## 27.3.5.3 ifconfig 命令

`ifconfig` 命令可以执行许多与 `wicontrol(8)` 相同的选项，但它缺少了一些选项。请检查 `ifconfig` 的命令行参数和选项。

## 27.3.3 支持的网卡

### 27.3.3.6.1 接入点

目前支持 BSS（作为接入点模式）设备的唯一网卡是基于 Prism、2.5 或 3 芯片组的。完整列表请参阅 `wi(4)`。

### 27.3.3.6.2 802.11b 客户端

几乎所有的 802.11b 无线网卡目前都受 FreeBSD。大多数基于 Prism, Spectrum24, Hermes, Aeronet 和 Raylink 的网卡可以在 IBSS（ad-hoc、点对点和 BSS）模式下作为无线网卡工作。

### 27.3.3.6.3 802.11a & 802.11g 客户端

`ath(4)` 设备驱动支持 802.11a 和 802.11g。如果你的网卡位于 Atheros 芯片组上，你可能可以使用此驱动程序。

不幸的是，许多供应商不向开源社区提供其驱动程序的规范，因为他们将这些信息视为商业秘密。因此，FreeBSD 和其他操作系统的开发者面临两个选择：通过反向工程开发驱动程序，或者使用适用于 Microsoft Windows 平台的现有驱动程序二进制文件。包括 FreeBSD 在内的大多数开发者都采用了后一种。

得亏 Bill Paul (`wpaul`) 的贡献，从 FreeBSD 5.3-RELEASE 开始，有了对网络驱动程序接口规范 (NDIS) 的“原生”支持。FreeBSD 模拟器（也称为 Project Evil）获取一个 Windows 驱动程序并基本上欺骗它认为自己运行在 Windows 上。此功能是相对新的，但大多数测试用例似乎工作得良好。

为了使用 NDIS，你需要三样东西：
1. 内核源码
2. Windows 二进制文件 (`.SYS`)
3. Windows 配置文件 (`.INF`)

找到你网卡所需的文件。通常，这些文件可以在 CD 或厂商网站上找到。我们将使用 `W32DRIVER.SYS` 和 `W32INF`。下一步是将驱动编译为模块。为了完成这一点，进入 `ifis` 目录并：

```
# cd /usr/src/sys/ifis
```

我们将使用 `-i` 和 `-s` 选项来创建 ndis 驱动：

```
# -i W32DRIVER.SYS -s W32INF
```

为了使用 ndDIS，我们需要使用 is ：

```
isis_data.h
```

默认情况下，蓝牙设备以内核模块的形式。。连接设备之前，你需要加载驱动到：

```
# kldload ubt
```

如果蓝牙设备在启动时存在，请从 `loader.conf` 加：：

```
_load="YES"
```

插入你的蓝牙适配器。控制台（或 syslog）中会出现类似下面的输出：

```
ubt0: vendor 0xa12 product 0x0001, rev 1.10/25, addr 2
ubt0: Interface 0 endpoints: interrupt=0x81, block-in=0x82, block-out=0x2
ubt0: Interface 1 (alt.config 5) endpoints: isoc-in=0x83, isoc-out=0x3, wPacketSize=49, nframes=6, buffer size=294
```

注意：蓝牙栈在 FreeBSD 6.0 上开始手动加载，在 FreeBSD 5.X 5.5 之前也是如此。在 FreeBSD 5.5、6.1 及更高版本中，它通过 `devdev(8)` 自动完成。

为了使用驱动，我们需要加载模块：

```
# kldload if_ndis
```

蓝牙栈由 Lucistnik 编写。

将 `/share/examples/netgraph/bluetooth/rc.bluetooth` 复制到某个方便的地方，例如 `/etc/rc.bluetooth`。此脚本用于启动和停止蓝牙栈。在拔掉设备之前停止栈是一个好主意，但它不（通常）是致命的。在启动栈时，你会收到类似下面的输出：

```
# /etc/rc.bluetooth start ubt0
```

# 第 27 章 高级网络

```
BD_ADDR: 00:02:72:00:d4:1a
Features: 0xff 0xff 00 00 00 00
<3-Slot> <5-Slot> <Encryption> <Slot offset>
<Timing accuracy> <Switch> <Hold mode> <Sniff mode>
<Part mode> <RSPSP1> <Channel quality> <SCO link>
<HV2 packets> <NV3 hosts> <u-law> <A-law log> <CVSD>
<Paging scheme> <Power control> <Transparent SCO data>
Max. ACL packet size: 192 bytes
Number of ACL packets: 8
Max. SCO packet size: 64 bytes
Number of SCO packets: 8
```

## 27.4.3 主机控制器接口 (HCI)

主机控制器接口 (HCI) 为基带控制器和链路管理器提供了命令接口，并允许访问硬件状态和控制寄存器。该接口为访问蓝牙超出功能提供了一种统一的方法。主机上的 HCI 层与蓝牙硬件交换数据和命令。主机控制器传输层（通过物理总线）驱动为两个 HCI 层提供了相互交换的能力。

类型为 `hci` 的单个请求会发现 RF 范围内的蓝牙设备。这种操作被称为查询（inquiry）。查询和 HCI 相关的操作是通过 `hctroll(8)` 工具完成的。示例显示了如何找到范围内有哪些蓝牙设备。您应该在几秒钟收到设备列表。注意，只有当远程设备处于可发现模式时，才会响应查询。更多细节请参阅 `ng_hci(4)` 手页。

```
% hccontrol -n ubt0 inquiry
Inquiry result, num_responses=1
Inquiry result #0
BD_ADDR: 00:80:37:29:19:a4
Page Scan Rep. Mode: 0xl
Page Scan Period: 00
Page Scan Mode: 00
Class: 52:02:04
Clock offset: 0x78ef
Inquiry complete. Status: No error [00]
```

`BD_ADDR` 是蓝牙设备的唯一地址，类似于网卡的 MAC 地址。这对于与设备进行进一步通信是必要的。可以为 `BD_ADDR` 分配人类可读的名称。`/etc/bluetooth/hosts` 文件包含了已知蓝牙主机的信息。以下示例显示了如何获取分配给远程设备的人类可读名称：

```
% hccontrol -n ubt0 remote_name_request 00:80:37:29:19:a4
BD_ADDR: 00:80:37:29:19:a4
Name: Pav's T39
```

如果您对远程蓝牙设备进行查询，它会将您识别为 'your.host.name (ub0)'。本地设备的名称可以随时更改。
