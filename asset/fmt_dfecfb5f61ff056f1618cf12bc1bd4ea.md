
可以使用一个或多个选项项将其他参数传递给内核模块，以正确配置你的 NIC。有关条目的更多信息，请参阅 `modprobe.conf` 手页。关于 NIC 内核模块的细节，请检查模块的源代码，因为没有相应的帮助页（这对任何想编写文档的人来说都是很好的机会）。

# 第 18 章 网络连接

> 提示
> 
> Linux 内核和网络工具可诊断或排除出现问题的 NIC。然而，如果你访问 Don Becker 的 Linux 以太网状态、诊断和设置工具页面 http://www.scyld.com/ethercard_diag.html，你将发现几十针对各种 PCI 和传统 ISA 以太网卡的硬件特定工具。如果在 NIC 识别或配置过程中遇到问题，这些工具将非常有帮助。

## 使用 modprobe 手动加载内核模块

你不需要使用 `/etc/modprobe.conf` 来为你的新网络设备初始化内核支持。作为 root 用户（使用 `sudo`），你可以使用 `modprobe` 命令配合模块名称手动加载或卸载设备内核模块。例如，使用以下命令行启用示例中的 RealTek NIC：

```
$ sudo modprobe 8139
```

按下回车键后，你将看到内核环形缓冲区消息报告的设备，可以通过 `dmesg` 命令显示。以下是该命令输出的一部分：

```
$ dmesg
```

eth0: RealTek RTL8139 Fast Ethernet at 0ce8ee00, 00:30:1b:0b:07:d0, IRQ 11

eth0: Identified 8139 chip type 'RTL-8139C'

eth0: Setting half-duplex based on auto-negotiated partner ability 0000.

注意，此时尚未为设备分配 IP 地址或其他设置。Linux 可以可以使用以太网接口，第一个以太网设备将命名为 `eth0`，第二个命名为 `eth1`，依此类推。内核识别的每个不同以太网设备可能会根据其内核模块报告额外的或不同的信息。例如：

```
$
```

eeop100-c.v100.9j-t 9/29/99 Donald Becker http://cesdis.gsfc.nasa.gov/linux/
--drive

```
rs/eeop100.c:$Version: 1.36 $2000/11/17 Modified by Andrey V. Savchokin <saw@saw.sw.com.sg> and others
```

PCI: Found IRQ 10 for device 00:0d.0

0: Intel Corporation 82557 [Ethernet Pro 100], 00:90:27:91:B2:B5, IRQ 10.

Board assembly 721383-007, Physical connectors present: RJ45

Primary interface chip i82555 PHY #1.

```
General self-test: passed.
Serial sub-system-test: passed.
Internal registers self-test: passed.
ROM checksum self-test: passed (0x04f4518b).
```

在这个示例中，识别到了一个 Intel Ethernet Pro 100 NIC。要禁用此 NIC，可以卸载内核模块。下一节将显示如何配置你的 NIC。

## 使用网络配置

如果你添加或替换了硬件，必须配置 NIC。本节显示如何配置你的 NIC。

## 命令行配置

你可以通过一个命令更改你想要更改的任何选项。命令的基本结构如下：

```
ifconfig [network device]
```

- 激活或禁用你的 NIC
- 更改你的 IP 地址
- 创建 IP 别名
- 为点对点设置目标地址

表 18.1 显示 `ifconfig` 选项的部分和示例。

| 表 18.1 ifconfig 选项 | 用途 | 示例 |
| --- | --- | --- |
| 创建别名 | [network device] | ifconfig eth0:10.10 |
| 更改 IP 地址 | | ifconfig eth0 10.10.10 |
| 更改子掩码 | [netmask] | ifconfig eth0 mask 255.255.255.0 |
| 更改广播地址 | [address] | ifconfig eth0 broadcast 10.10.255 |
| 禁用接口 | down | ifconfig eth0 down |
| 启用接口 | up (add IP address) | ifconfig eth0 up (ifconfig eth0 10.10) |
| 设置混杂模式 | [-]promisc | ifconfig eth0 promisc mode on |
| 设置组播 | [-]allmulti | ifconfig eth0 on allmulti |
| 启用 [禁用] [address] | [-]pointpoint eth0 | ifconfig eth0 point-to-point address 10.10.20 |

`ifconfig` 页面显示了其他允许你的机器与多种网络类型（如 AppleTalk、Novell、IPv6 等）交互的选项。再次阅读帮助页获取详情。

> 注意
> 
> 混杂模式会导致 NIC 接收网络上的所有数据。它通常用于网络嗅探。组播使 NIC 接收网络上的所有组播流量。

如果不提供参数，`ifconfig` 将显示活动接口的状态。例如，在不带参数且有一个活动并配置好的 NIC 的情况下，`ifconfig` 的输出如下：

# $ ifconfig

```
eth0
Link encap:Ethernet Haddr 00:0F:EA:B2:53:85
inet addr:192.168.2.5 192.168.2.255 Mask:255.255.255.0
inet6 addr fe80::20f:ffeb:25384/64 Scope:Link
```

# 使用网络配置工具 417

```
UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
RX packets:471 errors:0 dropped:0 overruns:0 frame:0
TX packets:695 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 tqueuelen:1000
RX bytes:160637 (156.8 KB) TX bytes:86193 (84.1 KB)
Interrupt:185 Base address:0x6000
```

```
Link encap:Local Loopback
inet addr:127.0.0.1 Mask:255.255.0.0
inet6 addr::1/128 Scope:Host
UP LOOPBACK MTU:16436 Metric:1
RX packets:19 errors:0 dropped:0 overruns:0 frame:0
TX packets:19 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 tqueuelen:0
RX bytes:1336 (1.3 KB) TX bytes:1336 (1.3 KB)
```

输出结果易于理解。链接条显示了接口的 IP 地址。`UP` 表示接口已就绪，`BROADCAST` 表示网络支持广播消息（以太网），`RUNNING` 表示接口正在运行，而 `LOOPBACK` 显示哪个设备（lo）是环回地址。eth0 上的最大传输单元（MTU）为 1500 字节。这决定了可以在此接口上传输的最大数据包的大小（有时为了提高性能会将其“调整”为其他值）。`Metric` 是一个 0 到 3 的数字，与从接口放入路由表的信息量有关。数字越小，信息量越少。

可以使用 `ifconfig` 命令通过表 18.1 列出的命令来显示或控制特定接口的信息。例如，若要禁用主机上的以太网设备，可以使用 `ifconfig` 命令、接口名称和 `down` 命令，如下：

```bash
$ sudo ifconfig eth0 down
```

你可以通过指定主机名或 IP 地址以及网络信息来配置并激活该设备。例如，要使用特定的 IP 地址配置并激活（“启动”）eth0 接口，请如下使用 `ifconfig` 命令：

```bash
$ sudo ifconfig eth0 192.168.2.9 netmask 255.255.255.0 up
```

如果你在系统的 `/etc/hosts` 文件中定义了主机（本章稍后部分的“网络配置文件”章节），你可以根据定义的名称配置并激活接口：
