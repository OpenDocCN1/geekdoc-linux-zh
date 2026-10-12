
c. 每周执行。

14. 如果路由器使用 NAT，你需要使用多少条命令来确保交换机可用？交换机连接网络上的。

## 636 第 16 章 管理任务

## 配置和监控局域网

本章内容

- 设置硬件 ................................ 38
- 路由器 ................................ 38
- NIC：网络接口卡 ............ 39
- 配置系统 ................. 41
- 设置服务器 ................................ 46
- Cacti 简介 ................. 64

网络允许计算机通信并共享资源。局域网（LAN）连接一个站点（如办公室、家庭或图书馆），并共享打印机。本章介绍了配置局域网的两个方面：设置硬件和配置软件。

## 设置硬件

LAN上的每个系统或节点都需要网络接口卡。每个系统必须连接到一个集线器或交换机。如果 LAN 连接到另一个网络，还需要一个路由器。

## 连接计算机

计算机通过电缆（有线，375页）或无线电波（无线或 Wi-Fi，376）连接到网络。电缆可以连接各种设备，其中一些在本节中介绍。参见第 375 页的“LAN：局域网”获取集线器、交换机和路由器的解释。

在图 17-1 所示的简单网络中，四台计算机连接到一个集线器或交换机。假设计算机 1 和 2 与 3 和 4 同时通信。使用集线器（375页），每次通信都被限制为网络带宽的一半。使用交换机（375页），每次通信理论上可以使用全部网络带宽。

集线器通常比交换机便宜，尽管交换机正在变得越来越便宜且越来越稀缺。如果你计划将网络用于 Internet 连接和轻量文件共享，集线器可能足够快。

> > 无线接入点（WAP）将无线网络连接到有线网络。通常 WAP充充透明桥，在网络之间转发数据包。如果你将多个 WAP 连接到同一个有线网络，无线客户端可以在 WAP 之间漫游。

## 路由器

路由器（377页）将 LAN 连接到另一个网络，如 Internet。路由器可以执行多种功能，最常见的是允许多个系统共享单个 Internet 连接和 IP 地址（NAT，881页）。当路由器使用 NAT 时，来自 LAN 上每个系统的数据包似乎来自同一个 IP 地址；路由器将返回包传递给正确的系统。路由器还可以充当防火墙。

你对几种路由器选择：

- 简单的硬件路由器相对便宜，并能满足小型网络的大部分需求。

### 硬件设置 639

![](img/f67bdb23d5a8cb457175c8ce91ec36c2_678_0.png)

图 17-1 一个简单的网络

- 你可以把 Ubuntu 系统配置为路由器。Linux 内核可以使用 `gufw`（第 876 页）和 `iptables`（第 880 页）来实现防火墙以保护你的系统。
- 你可以使用为路由器用途定制的专用发行版/操作系统。例如，SmoothWall（www.smoothwall.org）、pfSense（www.pfsense.com）和 m0wall（mt00.ch/wall）提供了类似于硬件路由器的基于浏览配置。

## NIC：网络接口卡

每个系统的 NIC 可能是单独的以太网卡（有线或无线），也可能是集成在主板上的。

支持的 NIC：Linux 支持大多数有线以太网卡和许多无线以太网卡。

不支持的无线 NIC：如果 Linux 不直接支持某个无线以太网卡，你可能可以通过 `NdsWrapper`（sourceforge.net/projects/ndswrapper/ndswrapper-common, ndswrapper-utils-1.9 和 ndisk 包）使其工作，这些包使用了 Win32 驱动。`NdsWrapper` 是一个提供 Windows 网络驱动 API 子集的内核模块。请参考 `ubuntu.com/community/WifiDocs/Driver/NdsWrapper` 获取在 Windows 上安装的说明。

无线桥接器：有线桥接器的替代方案是无线桥接器。无线桥接器在有线和无线接口之间转发数据包，无需无线驱动。这个简单设备具有一个插入 NIC 的以太网端口和一个 802.11（无线）控制器。虽然移动用户通常不携带，但无线桥接器是将桌面电脑迁移到无线配置的简单方法。

### 640 第17 章 配置与监控 LAN

Ad hoc（自持）与基础模式：无线网络以 ad hoc模式或基础模式运行。在 ad hoc模式下，网络中的各个节点之间直接通信。在基础模式下，节点通过 WAP（第 638 页）通信。如果 WLAN 必须与有线局域网通信，基础模式通常更可靠。

如果你不想使用 WAP，可能设置 WLAN 卡使其充当 WAP。请咨询 NIC/驱动文档获取更多信息。

## 工具

本节描述了你可以用于检查系统硬件的两个工具。

## lspci：列出 PCI 信息

`lspci` 列出 PCI 设备信息：

```
$ lspci
00:00.0 Host bridge: NVIDIA nforce2 AGP (different version?) (rev c1)
00:00.1 RAM memory: NVIDIA nforce2 Memory Controller 1 (rev c1)
00:00.2 RAM memory: NVIDIA nforce2 Memory Controller 2 (rev c1)
00:00.3 RAM memory: NVIDIA nforce2 Memory Controller 3 (rev c1)
00:00.4 RAM memory: NVIDIA nforce2 Memory Controller 4 (rev c1)
00:00.5 RAM memory: NVIDIA nforce2 Memory Controller 5 (rev c1)
00:01.0 TSA bridge: NVIDIA nforce2 ISA Bridge (rev a4)
00:02.1 SMBus: NVIDIA Corporation nforce2 SMBus (MCP) (rev a2)
00:02.0 USB Controller: NVIDIA Corporation nforce2 USB Controller (rev a4)
```

使用 `-vv` 选项，`lspci` 输出会更详细。你可以使用 `-vv` 或 `-vvv` 选项显示更多信息。

```
$ lspci -v
00:00.0 Host bridge: NVIDIA Corporation nforce2 AGP (different version?) (rev c1)
Subsystem: ASUS Computer Corp. Unknown device 1c00
Memory at 0xe00000 (32-bit, prefetchable) [size=4M]
Capabilities: <access denied>

00:00.1 RAM memory: NVIDIA Corporation nforce2 Memory Controller 1 (rev c1)
Subsystem: NVIDIA Corporation Unknown device 0c17
Flags: 64MHz, Fast devel

00:00.2 RAM memory: NVIDIA Corporation nforce2 Memory Controller 4 (rev c1)
Subsystem: NVIDIA Corporation Unknown device 0c17
Flags: 64MHz, Fast devel
```

## lshw：列出硬件信息

`lshw` 列出本地系统的硬件配置。以 root 权限运行此实用程序可以显示更详细的报告。`short` 选项显示简要报告。

```
$ sudo lshw short
H/W path | Device | Class | Description |

| --- | --- | --- | --- |

| system | VMware Platform | | Desktop Platform |

| /0 | bus | | 87K BIOS |

| /0 | processor | | Athlon 64 Core Processor |

| /0/4/1c | memory | | 16KB L1 cache |

| /0/4/0 | memory | | 128KB L1 cache |

| /0/1 | memory | | 1MB L2 cache |

| /0/100/f | display | | SVGA Adapter |

| /0/100/10 | scsi | storage | SVGA Adapter Fusion-M SCSI |

| /0/100/10.0 | dev/sda | volume | Ultra320GB EXT4 volume |

| /0/100/10.0.2 | dev/sda | volume | Extended partition |
```
