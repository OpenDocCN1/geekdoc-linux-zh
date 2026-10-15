

## 提示

Linux 内核和网络工具可用于诊断问题或排查有问题的网卡。然而，如果你浏览到 Don Becker 的 Linux Ethercard 状态、诊断和设置工具页面 http://www.scyd.com/ethercard_diag.html，你会发现有二十多种针对各种 PCI 和旧式 ISA 以太网网卡的硬件专用工具。如果你在网卡识别或配置过程中遇到问题，这些工具会非常有帮助。

## 使用 modprobe 手动加载内核模块

你不必使用 /etc/modprobe.conf 条目来为新网络设备初始化内核支持。作为 root 用户（使用 sudo），你可以使用 modprobe 命令连同模块名称手动加载或卸载设备的内核模块。例如，使用以下命令行启用示例 RealTek 网卡：

```
$ sudo modprobe 8139too
```

按下 Enter 后，你将看到该设备从内核环形缓冲区消息中报告，可通过 dmesg 命令显示。以下是该命令输出的一部分：

```
$ dmesg
...
eth0: RealTek RTL8139 Fast Ethernet at 0xce8ee000, 00:30:1b:0b:07:0d, IRQ 11
eth0: Identified 8139 chip type 'RTL-8139C'
eth0: Setting half-duplex based on auto-negotiated partner ability 0000.
...
```

请注意，此时尚未为该设备分配 IP 地址或其他设置。Linux 可使用多个以太网接口，第一个以太网设备将被编号为 eth0，第二个为 eth1，以此类推。内核识别的每个不同的以太网设备可能会根据其内核模块报告额外或不同的信息。例如，

```
$ dmesg
...
eeprom100.c:v1.09j-t 9/29/99 Donald Becker http://cesdis.gsfc.nasa.gov/linux/drivers/eeprom100.html
eeprom100.c: $Revision: 1.36 $ 2000/11/17 Modified by Andrey V. Savochkin <sav@saw.sw.com.sg> and others
PCI: Found IRQ 10 for device 00:0d.0
eth0: Intel Corporation 82557 [Ethernet Pro 100], 00:90:27:91:92:B5, IRQ 10.
Board assembly 721383-007, Physical connectors present: RJ45
Primary interface chip i82555 PHY #1.
General self-test: passed.
Serial sub-system self-test: passed.
```

```
Internal registers self-test: passed.
ROM checksum self-test: passed (0x04f4518b).
...
```

在此示例中，一块 Intel Ethernet Pro 100 网卡已被识别。要禁用对网卡的支持，可以卸载内核模块，但通常只有在设备不再使用后才能卸载。请阅读下一节，了解如何在 Linux 内核识别网卡后配置网卡以及如何控制其行为。

## 使用网络配置工具

如果你在初始安装后添加或更换网络硬件，则必须配置新硬件。你可以使用命令行或图形配置工具进行配置。要使用命令行配置网络客户端主机，可以使用一系列命令或编辑 /etc 目录下的特定文件。要通过图形界面配置硬件，可以使用 Ubuntu 用于 X 的图形工具 network-admin。本节介绍可用于在 Ubuntu 系统上配置网络接口和网络设置的命令行和图形软件工具。你将看到如何控制你的网卡并管理你的系统与网络的交互方式。

如果你是 Linux 新手，使用命令行配置工具可能会显得困难。对于任何网络新手来说，network-admin 图形工具是最佳选择。手动和图形方法都需要 root 权限才能工作。如果你没有 root 权限，请在尝试任何操作之前获取它。你不应编辑系统上由图形网络管理工具使用的任何脚本或设置文件。下次运行该工具，例如 network-admin 时，你的更改将被丢失！要么采用手动方法并编写自己的网络设置脚本，要么坚持使用图形配置实用程序。

## 命令行网络接口配置

你可以使用基本的 Linux 网络实用程序从命令行配置网络接口。你通过使用命令更改当前设置或编辑多个系统文件来使用命令行配置网络客户端主机。两个命令 ifconfig 和 route 用于网络配置。netstat 命令显示有关网络连接的信息。

```
/sbin/ifconfig
```

ifconfig 用于配置你的网络接口。你可以使用它来

- 激活或停用你的网卡或更改你的网卡模式
- 更改你的机器的 IP 地址、网络掩码或广播地址
- 创建 IP 别名以允许在你的网卡上使用多个 IP 地址
- 为点对点连接设置目标地址

