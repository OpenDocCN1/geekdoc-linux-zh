

如果需要正确配置你的 NIC，可以通过一个或多个选项条目将其他参数传递给内核模块。关于如何使用这些条目，请参阅 `modprobe.conf` 手册页以获取更多详细信息。有关 NIC 内核模块的更多细节，请检查模块的源代码，因为不存在相应的手册页（这对于愿意编写文档的人来说是一个很好的机会）。

> **提示**
> Linux 内核和网络工具可用于诊断问题或排查故障 NIC。然而，如果你访问 Don Becker 的 [Linux 以太网卡状态、诊断和设置工具](http://www.scyld.com/ethercard_diag.html) 页面，你会发现针对各种 PCI 和传统 ISA 以太网网络卡的二十多种特定硬件工具。如果你在 NIC 识别或配置过程中遇到问题，这些工具会非常有帮助。

## 使用 modprobe 手动加载内核模块

你不需要使用 `/etc/modprobe.conf` 条目来初始化对新网络设备的内核支持。作为 root 用户，你可以使用 `modprobe` 命令和模块名称手动加载或卸载该设备的内核模块。例如，使用以下命令行来启用示例 RealTek NIC：

```bash
# modprobe 8139too
```

按下回车后，你会看到内核环形缓冲区消息报告此设备，这些信息可以通过 `dmesg` 命令显示。以下是该命令输出的一部分：

```bash
$ dmesg
...
eth0: RealTek RTL8139 Fast Ethernet at 0xce8ee000, 00:30:1b:0b:07:0d, IRQ 11
eth0: Identified 8139 chip type 'RTL-8139C'
eth0: Setting half-duplex based on auto-negotiated partner ability 0000.
...
```

请注意，此时尚未为该设备分配 IP 地址或其他设置。Linux 可以使用多个以太网接口，第一个以太网设备编号为 eth0，第二个为 eth1，依此类推。内核识别出的每个不同的以太网设备可能根据其中的内核模块报告额外或不同的信息。例如，

```bash
$ dmesg
...
eepro100.c:v1.09j-t 9/29/99 Donald Becker
http://cesdis.gsfc.nasa.gov/linux/drivers/eepro100.html
eepro100.c: $Revision: 1.36 $ 2000/11/17 Modified by Andrey V. Savochkin
<saw@saw-sw.com.sg> and others
PCI: Found IRQ 10 for device 00:0d.0
eth0: Intel Corporation 82557 [Ethernet Pro 100], 00:90:27:91:92:B5, IRQ 10.
Board assembly 721383-007, Physical connectors present: RJ45
Primary interface chip i82555 PHY #1.
General self-test: passed.
Serial sub-system self-test: passed.
Internal registers self-test: passed.
ROM checksum self-test: passed (0x04f4510b).
```

在此示例中，系统已识别出一个 Intel 以太网 Pro 100 NIC。要禁用对 NIC 的支持，可以卸载内核模块，但通常只有在该设备不再被使用时才可行。阅读下一节以了解如何在 Linux 内核识别 NIC 后对其进行配置以及如何控制其行为。

## 使用网络配置工具

如果在初始安装后添加或更换了网络硬件，你必须配置新硬件。你可以通过命令行或图形配置工具来做到这一点。要通过命令行配置网络客户端主机，你可以使用一系列命令的组合或编辑 `/etc/sysconfig` 目录下的特定文件。

要通过图形界面配置硬件，你可以使用 Fedora 的 X11 图形工具 `system-config-network` 或基于控制台的 `netconfig` 命令。

本节介绍了可用于在 Fedora 系统上配置网络接口和网络设置的命令行和图形软件工具。你将看到如何控制你的 NIC 并管理你的系统与网络之间的交互。

如果你是 Linux 的新手，使用命令行配置工具可能会显得困难。对于网络新手来说，`system-config-network` 图形工具是最佳选择。手动和图形方法都需要 root 访问权限才能工作。如果你没有 root 访问权限，在尝试这些操作之前请先获取。你不应该编辑你的系统中图形网络管理工具使用的任何脚本或设置文件。因为下次运行像 `system-config-network` 这样的工具时，你的更改将会丢失！要么使用手动方法并编写你自己的网络设置脚本，要么坚持使用图形配置实用程序。

本节描述的网络配置过程适用于客户端主机。你在安装期间无法执行服务器网络配置，例如域名系统 (DNS) 和 DHCP。（有关配置 DNS 的更多信息，请参阅第 27 章“管理 DNS”；有关该项的更多信息，请参阅本章后面的“DHCP”部分。）

### 命令行网络接口配置

你可以使用基本的 Linux 网络实用程序从命令行配置网络接口。你通过命令行使用命令更改当前设置或编辑多个系统文件来配置网络客户端主机。两个命令 `ifconfig` 和 `route` 用于网络配置。`netstat` 命令显示有关网络连接的信息。

```bash
/sbin/ifconfig
```

`ifconfig` 用于配置网络接口。你可以使用它来：

- 激活或禁用你的 NIC 或更改你的 NIC 模式
- 更改你机器的 IP 地址、子网掩码或广播地址
- 创建 IP 别名以允许你的 NIC 拥有多个 IP 地址
- 为点对点连接设置目标地址

你可以用一条命令更改这些选项中的任意多项或极少项。该命令的基本结构如下：

```bash
/sbin/ifconfig [network device] options
```

表 18.1 显示了 `ifconfig` 选项的子集及其使用示例。

**表 18.1 `ifconfig` 选项**

| 用途 | 选项 | 示例 |
|---|---|---|
| 创建别名 | `[network device]:[number]` | `ifconfig eth0:0 10.10.10.10` |
| 更改 IP 地址 | `[IP address]` | `ifconfig eth0 10.10.10.12` |
| 更改子网掩码 | `netmask [netmask]` | `ifconfig eth0 netmask 255.255.255.0` |
| 更改广播地址 | `broadcast [address]` | `ifconfig eth0 broadcast 10.10.10.255` |
| 关闭接口 | `down` | `ifconfig eth0 down` |
| 启动接口 | `up` (添加 IP 地址) | `ifconfig eth0 up` 或 `ifconfig eth0 10.10.10.10` |
| 设置 NIC 混杂模式开 [关] | `[-]promisc` | `ifconfig eth0 promisc` 或 `ifconfig eth0 -promisc` |
| 设置多播模式开 [关] | `[-]allmulti` | `ifconfig eth0 allmulti` 或 `ifconfig eth0 -allmulti` |
| 启用 [禁用] 点对点地址 | `[-]pointopoint [address]` | `ifconfig eth0 pointopoint 10.10.10.20` |

`ifconfig` 手册页显示了其他选项，允许你的机器与许多网络类型进行交互，如 AppleTalk、Novell、IPv6 等。同样，请阅读手册页了解这些网络类型的详细信息。

如果没有给出参数，`ifconfig` 会显示活动接口的状态。例如，在没有参数且有一个活动且已配置的 NIC 的情况下，`ifconfig` 的输出看起来类似于这样：

```bash
# /sbin/ifconfig

eth0      Link encap:Ethernet  HWaddr 00:30:1B:0B:07:0D
          inet addr:192.168.2.7 Bcast:192.168.2.255 Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:127948 errors:0 dropped:0 overruns:0 frame:0
          TX packets:172675 errors:0 dropped:0 overruns:0 carrier:0
          collisions:7874 txqueuelen:100
          RX bytes:19098389 (18.2 Mb)  TX bytes:68739080 (65.5 Mb)
          Interrupt:11 Base address:0x2000

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          UP LOOPBACK RUNNING  MTU:16436  Metric:1
          RX packets:215214 errors:0 dropped:0 overruns:0 frame:0
          TX packets:215214 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:68739080 (65.5 Mb)  TX bytes:68739080 (65.5 Mb)
```

输出很容易理解。`inet` 条目显示接口的 IP 地址。`UP` 表示接口已准备好使用，`BROADCAST` 表示接口连接到支持广播消息的网络（以太网），`RUNNING` 表示接口正在运行，`LOOPBACK` 显示哪个设备 (`lo`) 是回环地址。eth0 上的 *最大传输单元* (MTU) 是 1500 字节。这决定了可以通过此接口传输的最大数据包大小（有时为了增强性能会“调整”为其他值）。Metric 是一个从 0 到 3 的数字，与放置在路由表中的接口信息量有关。数字越小，信息量越小。

`ifconfig` 命令可用于使用表 18.1 中列出的命令来显示特定接口的信息或控制该接口。例如，要停用主机上的第一个以太网设备，请使用 `ifconfig` 命令、接口名称和 `down` 命令，如下所示：

```bash
# ifconfig eth0 down
```

