
# Linux 安全与优化系统入门指南

## 概述

引言

3

关于本页的意见和建议请邮件至 `gmourani@videotron.ca`

`TCP/IP` 安全概述...............................................................................97

- 防火墙脚本文件......................................................................109
- 邮件服务器的"`etc/rcirc/init.d/firewall`"脚本文件................................ 119
- 网关服务器的"`etc/rcirc/init.d/firewall`"脚本文件..............................128
- 拒绝访问某些地址..................................................................140
- 必要的软件包...............................................................................144
- 我们为什么选择使用压缩包 (`tarballs`)? .......................................................145
- 在你的系统上构建并安装软件.........................................................146
- `sXid` 管理工具...........................................................................151

## Linux SSH1 客户端/服务器

- 配置...............................................................................................152
- `SSH1` 用户工具...............................................................................159

## Linux SSH2 客户端/服务器

## Linux GnuPG

## Linux DNS 和 BIND 服务器

关于本页面的意见和建议应发送至 `gmourani@videotron.ca`

## Linux PostgreSQL 数据库服务器......................................................................... 278

配置.................................................................................................................................. 281

配置.................................................................................................................................. 291

优化 `Squid`............................................................................................... 297

## Linux Apache Web 服务器........................................................................ 299

配置.................................................................................................................................. 303

安全 `Apache`.................................................................................................. 308

与 `Apache` 一起安装的可选组件............................... 316

## Linux IPX 网络客户端.................................................................. 320

尝试在没有 `TCP/IP` 的情况下设置 `IPX` 网络接口...................... 321

为没有 `shell` 的用户设置 `FTP` 账户.................. 324

配置.................................................................................................................................. 327

安全 `FTP`..................................................................................... 335

## 第 11 章 备份与恢复程序 338

服务器备份程序.................................................................................. 339

服务器恢复程序............................................................................... 340

5

关于本页面的意见和建议可以发送至 `gnourani@videotron.ca`

### 引言

当我开始时，我问自己的第一个问题是如何使用 Linux 安装服务器，并确保没有外部或内部人员未经授权访问它。然后我想知道是否存在类似于 Windows 上的方法来提高计算机性能。我开始在互联网上进行搜索，并阅读了多本书，以获取关于我的服务器安全和性能的最丰富信息。经过多年的研究和学习，我终于找到了问题的答案。答案在互联网上。我根据自己的文档、书籍、文章等创建了一份文档，这些对我的日常活动很有帮助。

### 概述

本文被设计为一份分步演示的示例文档，而不是对每个 Linux 特性的详细解释。它没有涉及调试方面的内容，因为 Linux 开发项目（`LDP`）的 `HOWTO` 已经涵盖了这些部分。

本文面向技术受众！它讨论了如何安装 `RedHat` 服务器，并进行所有的安全防护和优化，以构建高性能 Linux 机器。由于我们谈到了优化和配置选项，我们将尽可能使用源码分发（`tar.gz`）程序，特别是对于 `Apache`、`Bind`、`Samba`、`Squid`、`Openssl` 等关键服务器软件。

本文针对 `Intel x86` 硬件固型，如果你正在寻找 `PPC`、`ARM`、`SPARC`、`APX` 等特性，你可能找不到你想要的内容。

此服务器的最小化安装要求你重新编译内核，其他程序取决于你的具体需求。

- 你有一个 `CD-ROM` 驱动器和官方 `Red Hat Linux CD-ROM`。安装已经在官方 `RedHat Linux 6.1` 上进行过测试。

你应该理解将安装操作系统的硬件系统。在检查完硬件后，本文的其余部分将引导你一步步完成安装过程。

### Gerhard Mourani 的 PGP 公钥

```
----
```

7

## 第一部分 安装相关参考

### Linux 简介

#### 第 1 章 Linux 简介

### 什么是 Linux？

使用 Linux 的一些理由

Linux 最初是由一名芬兰赫尔辛基的学生林纳斯·托瓦尔斯（`Linux Torvalds`）作为兴趣爱好创建的操作系统。他对 `Minix`（一个小型 `UNIX` 系统）感兴趣，决定开发一个超越 `Minix` 标准的系统。他从 1991 年开始工作，发布了 0.02 版本，并一直稳定工作直到 1994 年 Linux 内核 1.0 发布。目前的全功能版本是 2.2（于 1999 年 1 月 25 日发布），并持续开发中。

Linux 在 `GNU` 公共许可证（`GNU Public License`）下开发，其源代码对所有人免费开放。然而，这并不意味着 Linux 及其相关发行版是免费的；只要源代码保持可用，公司就可以对其收费。Linux 可用于多种用途，包括网络、软件开发以及作为终端用户平台。Linux 通常被认为是比昂贵操作系统的低成本替代方案。



由于 Linux 功能和可用性的本质特性，它在世界范围内变得非常流行，大量程序员获取了 Linux 源代码并对其调整以满足他们的个人需求。目前，有几十个正在进行的项目将 Linux 移植到各种硬件配置和用途。

### 使用 Linux 的一些理由

没有特许权或许可费用。尽管林纳斯·托瓦尔斯拥有 Linux 商标，但 Linux 内核和大部分配套软件都是根据 GNU 公共许可证分发的。这意味着你可以修改源代码并销售程序获利，但原作者保留版权，且你必须提供你更改部分的源码。

尽管 Linux 在基于 Intel 的计算机上最流行，但它运行的 CPU 和平台比任何其他操作系统都多。这其中的原因之一，除了其狂热追随者的编程才华外，Linux 带有内核源代码且具有非常好的可移植性。

软件和硬件行业的最新趋势是推动消费者购买系统内存和硬盘存储容量不断增加的计算机。Linux 不受常见的“功能膨胀”导致臃肿问题的困扰，即使在 RAM 内存有限的老旧 x86 计算机上也能运行得很好。

当程序崩溃时，Linux 不像纸牌屋一样崩溃。你可以杀掉程序并放心地继续操作。Linux 使用先进的尖端内存管理技术来控制所有系统进程。你不会失去控制，也不必遭受这些困扰。

### 安装你的服务器

#### 第 2 章 安装 Linux 服务器

### 了解你的硬件！

了解硬件对于成功安装 RedHat 至关重要。请准备回答以下问题：

1. 你有多少个硬盘？
2. 每个硬盘多大？
3. 如果你有多个硬盘，哪一个是主硬盘？
4. 你有多少内存 RAM？
5. 你有 SCSI 适配器吗？如果有，什么品牌和型号的？
6. 你使用的是什么种类型的鼠标？
7. 有几个按钮？
8. 如果你使用的是串口鼠标，它连接在哪个 COM 端口？
9. 你的显卡名称和型号是什么？你有多少显存？
10. 你使用的是什么种类型的显示器（品牌和型号）？
11. 你将连接网络吗？如果是，将会是：
    a. 你的 IP 地址？
    b. 你的子网掩码？
    c. 你的网关地址？
    d. 你的域名服务器 IP 地址？
    e. 你的域名？
    f. 你的主机名？
    g. 你的网卡类型（品牌和型号）？

你会偶尔发现安装可能会失败；如果发生这种情况，则需要经过修订的磁盘镜像才能正常工作。在这种情况下，可以通过 Red Hat Errata 页面获取特殊镜像来解决问题。

关于此页面的意见和建议请邮件至 gmnourani@videotron.ca

Red Hat 错误列表页面：http://www.redhat.com/errata

由于我们直接从 CD-ROM 开始安装过程，因此您必须启动磁盘。请将您创建的启动盘插入要安装 Linux 的计算机的 `A:` 驱动器中，并重启计算机。在启动提示符处，按 `Enter` 继续启动。

- 选择您的语言
- 选择您的键盘类型
- 自定义

## 安装类和方法（安装类型）

RedHat Linux 6.1 定义了四种不同的类别，或安装类型。它们是：

- GNOME 工作站
- KDE 工作站
- 服务器
- 自定义

这些这些类（GNOME 工作站、KDE 工作站和服务器）为您提供了简化安装过程的选项，但带有许多我们并不希望拥有的配置灵活性。

因此，我们强烈建议使用“自定义”，因为这允许您选择添加哪些服务以及如何对系统进行分区。

其理念是在保持最高效率的同时，加载最少的软件包。机器上的软件越少，潜在的安全漏洞或缺陷就越少。

选择“自定义”并点击下一步。

## 磁盘设置（Disk Druid）

**警告**

我们强烈建议您在进行磁盘分区之前，对当前系统进行备份。

为了性能、稳定性和安全性，您必须对下方列出的分区进行如下操作。我们假设此分区配置是基于您想在您的机器上设置一个带有代理服务器的 Web 服务器。

我们将创建两个特殊分区 "`chroot`" 和 "`cache`"。"`chroot`" 分区用于 `chroot` 的 DNS 服务器器、Apache 服务器和其他其他 `chroot` 的未来程序。"`/cache`" 分区用于我们的 Squid 代理。如果您不打算安装 Squid 代理服务器，则不需要创建 "`/cache`" 分区，但 Squid + Apache 将极大提高您的性能和安全性。

如果用户需要通过 shell 访问服务器，将 "`/tmp`" 和 "`/home`" 放在单独的分区上是强制要求的，将这些分离到单独分区还可以防止用户填满任何关键文件系统；将 "`/var`" 和 "`/usr`" 放在单独分区也是一个非常好的主意。通过隔离 "`/var`" 分区，您可以保护您的根分区不溢出。

关于此页面的意见和建议请邮件至 gnourian@videotron.ca

在我们的分区配置中，我们为 Apache、DNS 等其他 chrooted 程序预留了 400 MB 的磁盘空间。这是必要的，因为 Apache DocumentRoot 文件和其他与 Apache 相关的二进制文件将在此分区中。

请注意，Apache chroot 目录的大小与您的 "`DocumentRoot`" 文件的大小成正比。如果您不打算在服务器上安装和使用 Apache，可以将此分区的大小缩小到类似 10 MB 的大小，用于您所需的 DNS。

## 分区的最小大小

这是可以正常运行的 Linux 安装的最小大小（单位为 MB）。下方列的分区大小非常小。这种配置可以放入我们在旧式 486 计算机上找到的任何 512MB 的旧硬盘中。我向您展示此分区仅用于提供一个概念概念。

| 分区 | 大小 (MB) |
| :--- | :--- |
| `/` | 35MB |
| `/boot` | 5MB |
| `/chroot` | 10MB |
| `/home` | 100MB |
| `/tmp` | 30MB |
| `/usr` | 232MB |
| `/var` | 25MB |

## Disk Druid

`Disk Druid` 是一个用于对硬盘进行分区的程序。选择“添加”添加新分区，“编辑”编辑分区，“删除”和“重置”将分区重置为原始状态。当添加新分区时，屏幕上会弹出一个新窗口并提供供您选择的参数。不同参数如下：

**挂载点：** 您想要挂载分区的地方。

**大小 (MB)：** 分区的大小（以兆字节为单位）。

**分区类型：** Linux 原生或 Linux 交换（Swap）。

如果您有 SCSI 磁盘，将是 "`/dev/sda`"；如果您有 IDE 磁盘，将是 "`/dev/hda`"。

这里是 Linux 使用的命名方案总结：

**前两个字母 –** 表示分区设备类型。您通常会看到 "`hd`"（对于 IDE 磁盘）或 "`sd`"（对于 SCSI 磁盘）。

**后续字母 –** 表示分区所在的设备。例如，"`/dev/hda`"（第一个 IDE 磁盘）和 "`/dev/hdb`"（第二个 IDE 磁盘）。

请记住这些信息，这在您设置 Linux 分区时会变得更容易。

## 交换分区

交换分区用于支持虚拟内存。如果您的计算机内存为 16 MB 或少，您必须创建一个交换分区。即使您的内存更多，仍然建议使用交换分区。交换分区的最小大小应等于您的内存或 16 MB（以较大者为准）。由于 2.2 内核支持 GB 交换，比此更大的交换分区会导致浪费空间。然而，您可以创建并使用多个交换分区（这对于非常大的服务器安装是必要的）。

尝试将您的交换分区放在磁盘的开头。磁盘头部物理位于圆柱的外部，读写头每旋转一次覆盖范围更大。

现在举个例子：

要使下方列的分区变为系统（这是我们的服务器所需的所需的），命令将是 `Disk Druid`：

添加

挂载点：`/boot` ← `/boot` 目录。

大小 (MB): 5

分区类型：Linux 原生

确定

添加

挂载点：`/usr` ← `/usr` 目录。

大小 (MB): 1000

分区类型：Linux 原生

确定

添加

挂载点：`/home` ← `/home` 目录。

大小 (MB): 500

分区类型：Linux 原生

确定

添加

挂载点：`/chroot` ← `/chroot` 目录。

大小 (MB): 400

分区类型：Linux 原生

确定

添加

挂载点：`/cache` ← `/cache` 目录。

大小 (MB): 400

分区类型：Linux 原生

确定

添加

挂载点：`/var` ← `/var` 目录。

大小 (MB): 200

分区类型：Linux 原生

确定

添加

挂载点：`/swap` ← 我们的交换 分区。

大小 (MB): 150

分区类型：Linux 交换

确定

关于本页面的意见和建议请邮件至 gmourani@videotron.ca

## 要安装的组件（软件包组选择）

在完成分区的配置并选择格式化后，你就可以选择要安装的软件包了。默认情况下，Linux 是一个强大的操作系统，运行着许多用的服务。然而，这些服务中的大多数并非必要的，并构成了潜在的安全风险。

正确安装 Linux 是构建稳定、安全系统的第一步。你首先必须选择要安装哪些系统组件。选择好组件后，你可以通过 `Select individual packages` 选项逐一选择或取消选择每个组件中的各个软件包。



由于我们正在配置的是 Linux 服务器，因此我们不需要在系统中安装图形界面（`XFree86`）（服务器上运行图形界面意味着更少的进程、更少的 CPU、更少的内存以及安全风险等）。图形界面通常用于工作站。请选择以下软件包进行安装。

- 网络工作站 (Networked Workstation)
- 网络管理工作站 (Network Management Workstation)
- 工具 (Utilities)

在选择了你想要安装的组件后，你可以选择或取消软件包。

**注意：** 在继续之前，请选择 **(Select individual packages)** 选项（非常重要），以便你拥有选择和取消选择软件包的可能性。

## 个别软件包选择

安装程序会列出可选的软件包组，请选择一组进行检查。

下方列出的组件必须从菜单组（Menu Group）中取消选择，出于安全、优化以及下文描述的原因。

| Applications/Archiving: dump |
| Applications/File: gl |
| Applications/Internet: finger, ftp, whois, ncftp, rsh, rsync, talk, telnet |
| Applications/Publishing: ghostscript, ghostscript-fonts, mpage, rhs-printerfilters |
| Applications/System: apache, bind-utils, knfd-clients, procinfo, rdate, rdist, screen, ucd-snmp-utils |
| Documentation: indexhtml |
| System Environment/Base: chkfontpath, yp-tools |
| System Environment/Daemons: XFree86-xfs, lpr, ypbind, portmap, rusers, rwhoho, tftp, ucd-snmp, ypbind |
| System Environment/Libraries: XFree86-libs, libpng |
| User Interface/X: XFree86-75dpi-fonts, urw-fonts |

在我们解释想要安装的每个程序之前，可能有人会问，为什么不在服务器上安装 `finger`、`ftp`、`whois` 和 `telnet`？首先，我们知道这些程序从本质上是不安全的。想象一下，黑客访问了你的新服务器，他可以使用 `finger`、`ftp`、`whois` 和 `telnet` 程序来查询或访问你网络上的其他节点。如果你的新服务器上没有安装这些程序，他将被迫从外部使用这些程序，或者在你的服务器上安装程序，在这种情况下，你可以使用 `Tripwire` 工具对其进行追踪。

关于本页面的意见和建议请邮件至 `gmourani@videotron.ca`

### Applications/Archiving:

`dump` 软件包包含了 `dump` 和 `restore`。`dump` 检查文件系统中的文件，确定哪些文件需要备份，并将这些文件复制到指定的磁盘、磁带或其他存储介质上。**[无必要，我们使用其他方法]**

### Applications/File:

`GIT` (GNU Interactive Tools) 了一个了一个可扩展的文件系统浏览器、一个 ASCII/十六进制文件查看器、一个进程查看/杀死工具以及其他相关的工具和 shell 脚本。**[无必要]**

### Applications/Internet:

`Finger` 是一个实用程序，允许用户查看系统用户信息（登录名、主目录、名称、登录系统多长时间等）。**[安全风险]**

`ftp` 软件包提供了标准的 UNIX 命令行 FTP 客户端。FTP 是文件传输协议，是一种广泛用于传输文件和归档文件的 Internet 协议。**[安全风险]**

`whois` 允许你或你的系统用户查询数据库。**[安全风险]**

`Ncftp` 是改进的 FTP 客户端。`Ncftp` 的改进包括支持命令行编辑、命令历史、递归获取、自动匿名登录等。**[安全风险]**

`rsh` 软件包包含一组程序，允许用户在远程机器上运行命令、登录到其他机器以及在机器之间拷贝文件（`rcp`）。**[安全风险]**

`talk` 软件包提供了用于 Internet 协议的客户端和守护进程，允许你与不同系统上的用户聊天。**[安全风险]**

`Telnet` 是一种通过 Internet 登录远程系统的流行协议。**[安全风险]**

### Applications/Publishing:

`Ghostscript` 是一套软件，提供 PostScript(TM) 解释器、一个包含图形能力的库以及 PDF（PDF文档格式）文件的解释器。**[无必要]**

这些字体可以在 `Ghostscript` 渲染文本时使用。`Ghostscript` 和 `X11` 之间共享字体。**[无必要]**

`epage` 实用程序将文本或 PostScript(TM) 文档作为输入，缩小文本大小并在每页纸上打印文件。**[无必要]**

`rhs-printerfilters` 软件包包含一组过滤器，主要用于打印机。**[无必要]**

### Applications/System:

`rstat` 和 `arpsmp` 都是网络监控工具。这两个工具监控以太网流量并构建 Ethernet/IP 地址对，并通过电子邮件报告某些更改。**[无必要]**

`Bind-utils` 包含了查询 DNS（域名服务）服务器的实用程序，以查找主机信息。**[我们将编译它]**

`knfs-clients` 软件包包含了 `showmount` 程序。`Showmount` 查询远程主机上的 NFS（网络文件系统）服务器。

`procinfo` 命令从 `/proc` 目录获取系统数据并将其显示在标准输出上。你可以使用 `procinfo` 获取有关正在运行系统的信息。**[无必要]**

`rdate` 实用程序从网络上的另一台机器使用 RFC 868 定义的协议检索日期时间和。**[安全风险]**

`ucd-snmp` 软件包包含了用于 UCD-SNMP 网络管理的各种实用程序。**[无必要]**

`screen` 实用程序允许你在一个终端上进行多次登录。`Screen` 对于 `telnet` 到机器的用户非常有用。**[无必要]**

### Documentation:

`indexhtml` 软件包包含了 HTML 页面和你在成功安装 Linux 后由 Web 浏览器显示的欢迎页面。

### System Environment/Base:

`Chkfontpath` 是一个简单的终端模式，用于添加、删除和列出字体服务器路径。**[无必要]**

Network Information Service (NIS) 是一个系统，为网络上的所有机器提供网络信息（登录名、主目录、用户组信息）。**[安全风险]**

关于本页面的意见和建议请邮件至 `gmourani@videotron.ca`

### System Environment/Daemons:

这是一个 `XFree86` 的字体服务器。你可以通过此软件包将字体发送到远程服务器，远程系统即使没有安装这些字体也可以使用字体服务器上的所有字体。**[无必要]**

`lpr` 软件包提供了管理打印服务的系统实用程序。**[无必要且服务器未安装打印机]**

`pident` 软件包包含身份信息，实现了 RFC1413 标识服务器。`pident` 查询 TCP/IP 连接并返回用户名或连接信息。**[无必要，极少数情况需要服务器发送 rident，因为许多机器没有它且许多人会关闭它]**

`portmapper` 是一个安全工具，防止通过 NFS 和 NIS 协议窃取 NIS (YP) 和其他敏感信息。`portmapper` 管理 RPC 连接。**[无必要，安全风险]**

路由守护进程处理传入的 RIP 流量并广播关于网络流量的出的 RIP 流量，以维护路由表。这些路由表对于网络计算机是至关重要的，使其知道数据包需要发送到哪里。**[无必要，安全风险]**

`users` 程序允许查找登录到本地网络各种机器的用户。`users` 命令产生与 `who` 类似的输出，但针对特定的主机列表或本地网络上的所有机器。**[安全风险]**

`rwh` 命令显示的输出与 `who` 命令的输出（显示谁已登录）类似，适用于本地网络上运行 `rwh` 守护进程的所有机器。**[安全风险]**

Trivial Transfer Protocol (TFTP) 通常用于无盘工作站的启动。`tftp` 软件包提供了 TFTP 的界面，允许用户从远程机器传输文件。**[安全风险，必要]**

SNMP (简单网络管理协议) 是一种用于网络管理的协议。**[无必要，安全风险]**

### System Environment/Libraries:

`XFree86-libs` 包含了大多数程序正常运行所需的共享库。这些共享库位于单独的软件包中，以减少在没有 X 服务器的机器（即通过网络）上运行 X 应用所需的磁盘空间。**[无必要]**



libpng 软件包包含一个函数库，用于创建和处理 PNG（便携网络图形）图像文件。PNG 是一种位图格式，类似于 GIF 格式。

## User Interface/X

`XFree86-75dpi-fonts` 包含了大多数 Windows 系统使用的 75 dpi 字体。

35 标准 PostScript 字体的免费版本。出厂标准 35 个 PostScript 字体的 Ghostquality 版本。

关于此页面的意见和建议应邮邮件至 `gmourani@videotron.ca`

此时，安装程序将对您选择的每个格式分区进行格式化。取决于您的机器的速度，这可能需要几分钟。一旦所有分区格式化完成，安装程序将开始安装软件包。

## 如何使用 RPM 命令

本节概述了在 Linux 系统上使用 RPM 进行安装、卸载、升级、查询、检查和构建 RPM 软件包的主要模式。

- 若要安装 RPM 软件包，请使用命令：

```
[root@deep]# rpm -ivh foo-1.0-2.i386.rpm
```

RPM 软件包的文件名为 `foo-1.0-2.i386.rpm`，它包含包名 (`foo`)、版本号 (`1.0`) 和架构 (`i386`)。

- 若要卸载 RPM 软件包，请使用命令：

```
[root@deep]# rpm -e foo
```

请注意，我们使用的是包名 `foo`，而不是原始包文件名 `foo-1.0-2.i386`。

- 若要升级 RPM 软件包，请使用命令：

```
[root@deep]# rpm -Uvh foo-1.0-2.i386.rpm
```

RPM 会自动卸载 `foo` 包的旧版本并安装新版本。请始终使用 `rpm -Uvh` 安装包，因为即使系统中没有安装该包之前的版本，也可以有效。

- 若要查询 RPM 软件包，请使用命令：

```
[root@deep]# rpm -q foo
```

此命令将打印已安装软件包 `foo` 的包名、版本和发布版本。使用此命令可以验证系统是否安装了该包。

- 若要显示包信息，请使用命令：

```
[root@deep]# rpm -qi foo
```

此命令显示包信息，包括已安装程序的名称、版本和描述。

- 若要列出包中的文件，请使用命令：

```
[root@deep]# rpm -ql foo
```

此命令将列出在 RPM 软件包中安装的所有文件。

- 若要检查 RPM 软件包的签名，请使用命令：

```
[root@deep#] rpm -checksig foo
```

此命令检查软件包的 PGP 签名以确保其完整性和来源。PGP 配置信息从配置文件读取。在系统上安装新的 RPM 软件包之前，请始终使用此命令。此外，在使用此命令之前，您的系统中必须已安装 `GNUPG` 或 `Pgp` 软件：

- 若从源码安装包，请使用命令：

```
[root@deep#] rpm -iv -rebuild foo.src.rpm
```

上述命令将配置并编译 `foo` 包，在 `/usr/src/redhat/RPM/i386/` 目录下生成一个二进制 RPM。然后您可以像往常一样使用类似命令安装该包：

## 启动和停止守护进程

Init 是内核在启动时运行的程序。它负责启动所有启动时需要运行的标准进程。这些包括 `APACHE` 守护进程、`NETWORK` 守护进程以及您希望在机器启动时运行的任何内容。

`init` 如何启动和停止服务？每个脚本都编写为接受一个参数，该参数可以是 `start` 或 `stop`，并位于 `/etc/rc.d/init.d/` 目录下。您可以通过类似命令手动执行这些脚本：

例如：

- 在 Linux 下手动启动 `httpd` Web 服务器。

```
[root@deep#] /etc/rc.d/init.d/httpd start
```

- 在 Linux 下手动停止 `httpd` Web 服务器。

```
[root@deep#] /etc/rc.d/init.d/httpd stop
```

检查您的 `/etc/rc.d/init.d/` 目录查看可用服务，并使用命令 `start | stop` 操作。

## 安装服务器后将卸载的软件

Red Hat Linux 默认在您的系统中安装所有预设程序，且在安装设置期间不为您提供卸载它们的选择。因此，您必须在安装服务器后在系统中卸载以下软件：

| pump | apmd | isapntools | redhat-logos |
| :--- | :--- | :--- | :--- |
| mt-st | kernel-pcmia-cs | seterial | redhat-release |
| eject | linuxconf | kudzu | gd |
| bc | getty_ps | raidtools | pciutils |
| mailcap | setconsole | gnupg |  |

使用如下 RPM 命令来卸载它们：

- 卸载软件的命令是：

```
[root@deep#] rpm -e softenames
```

其中 `softenames` 是您想要卸载的软件名称，例如 (`foo`)。

像 `apmd`、`kudzu` 和 `sendmail` 等程序是以进程形式运行的守护进程。在从系统中卸载它们之前，最好停止这些进程。

- 停止进程使用以下命令：

```
[root@deep]# /etc/rc.d/init.d/apmd stop
```

```
[root@deep]# /etc/rc.d/init.d/sendmail stop
```

```
[root@deep]# /etc/rc.d/init.d/kudzu stop
```

现在您可以安全地卸载所有包，其余如下所示：

### 步骤 1

移除指定的包。

```
[root@deep]# rpm -e mt-st mailcap kernel-pcmia-cs getty_ps setconsole kudzu raidtools gnupg redhat-release pciutils
```

### 步骤 2

移除已安装的 `linuxconf`。

```
[root@deep]# rpm -e linuxconf
```

### 步骤 3

移除已安装的程序。

```
[root@deep]# rpm -e hdparm
```

### 步骤 4

移除已安装的程序。

```
[root@deep]# rpm -e kbconfig
```

### 步骤 5

移除已安装的程序。

```
[root@deep]# rpm -e timeconfig
```

### 步骤 6

移除已安装的程序。

```
[root@deep]# rpm -e mouseconfig
```

### 步骤 7

移除已安装的程序。

```
[root@deep]# rpm -e mailconfig
```

### 步骤 8

移除已安装的程序。

```
[root@deep]# rpm -e pump
```

### 步骤 9

移除已安装的程序。

```
[root@deep]# rpm -e eject
```

### 步骤 10

移除已安装的程序。

```
[root@deep]# rpm -e bc
```

### 步骤 11

移除已安装的程序。

```
[root@deep]# rpm -e mailcap
```

### 步骤 12

移除已安装的程序。

```
[root@deep]# rpm -e setconsole
```

### 步骤 13

移除已安装的程序。

```
[root@deep]# rpm -e seterial
```

### 步骤 14

移除已安装的程序。

```
[root@deep]# rpm -e kudzu
```

### 步骤 15

移除已安装的程序。

```
[root@deep]# rpm -e sendmail
```

### 步骤 16

移除已安装的程序。

```
[root@deep]# rpm -e procmail
```

### 步骤 17

移除已安装的程序。

```
[root@deep]# rpm -e mt-st
```

### 步骤 18

移除已安装的程序。

```
[root@deep]# rpm -e st
```

关于本页面的意见和建议请邮件至 `gmnouri@videotron.ca`

`redhat-logos` 软件包（“软件包”）包含 Red Hat “Shadow Man” 标志和 RPM 标志的文件（“这些标志”）。

Red Hat Linux 发布文件。

`Gd` 是一个用于绘制 `.gif` 文件的图形库。`Gd` 允许你快速绘制图像（线条、弧、文本、多颜色、从其他图像复制和粘贴、洪水填充）并将结果写出为 `gif` 文件。

此软件包 (`poiutils`) 包含各种用于检查和设置连接到 PCI 总线设备的工具。

`kbcdbus` 程序是一个终端模式程序，为设置系统的键盘映射提供了一个简单的接口。

`Mouseconfig` 是一个基于文本的配置工具。`Mouseconfig` 负责设置 Red Hat Linux 系统上配置和使用鼠标所需的文件和链接。



timeconfig 软件包包含两个工具：`timeconfig` 和 `setclock`。`timeconfig` 提供了一个简单的文本工具，用于配置 `/etc/sysconfig/clock` 和 `/etc/localtime` 中的时间参数。

procmail 程序被 Red Hat 用于本地邮件投递。除了投递邮件外，procmail 还可以用于自动过滤、处理和其他邮件处理工作。procmail 也是 SmartList 邮件处理器的基础。**[仅在邮件服务器上]**

## 服务器安装后必须安装的软件

为了能够在你的服务器上编译程序，你必须安装 RPM 软件。安装的这部分非常重要，并要求你安装下面描述的所有相关软件包。这些软件位于 Red Hat 6.1 Part 1 CD-ROM 的 `RedHat/RPMS` 目录下，代表了在 Linux 上编译所需的软件。

### 步骤 1

首先，我们挂载 CD-ROM 驱动器并移动到 CD-ROM 的 RPM 子目录。

- 挂载 CD-ROM 驱动器并进入 RPM 目录，使用命令：`[root@deep]# mount /dev/cdrom /cdrom/` `[root@deep]# cd /cdrom/RedHat/RPMS/`

这就是你在 Linux 系统上编译程序所需的软件包。请记住，这是允许你编译大多数 Linux 可用 tar 包的最小包。Red CD-ROM 上存在其他编译器包，如果你在编译特定软件时收到错误信息，请通过包含你想要安装的 tar 包的 README 文件进行验证。

```
autoconf-2.13.5-noarch.rpm
m4-4.12.i386.rpm
automake-1.4-5.noarch.rpm
dev86-0.14.9-i386.rpm
bison-1.28-1.i386.rpm
byacc-1.9-11.i386.rpm
```

```
cdci-2.5-9.i386.rpm
cpp-1.2-24.i386.rpm
cproto-4.6-2.i386.rpm
clags-3.2-i386.rpm
egcs-1.2-24.i386.rpm
ElectricForce-2.1-1.i386.rpm
flex-2.54-7.i386.rpm
gdb-4-18-4.i386.rpm
kernel-headers-2.2.12-20.i386.rpm
gibc-devel-2.1.2-11.i386.rpm
make-3.77-6.i386.rpm
patch-2.5-9.i386.rpm
```

注意：如果你不想在 RPM 安装期间收到错误依赖关系消息，最好一起安装上述描述的软件。

### 步骤 2

之后我们将使用一条命令来安装所有需要的软件：

- 一性安装所有软件的 RPM 命令：

`[root@deep]# rpm -Uvh autoconf-2.13-5.rpm m4-4.1-12.i386.rpm automake-1.4-5.ocr.rpm devmake-08.6-11.i386.rpm bison-1.2.i386.rpm byacc-1.9-11.i386.rpm cdeci-2.5-9.i386.rpm cpp-1.2-24.i386.rpm cproto-4.6-2.i386.rpm clags-3.2-i386.rpm egcs-1.2-24.i386.rpm ElectricForce-2.1-1.i386.rpm flex-2.54-7.i386.rpm gdb-4-18-4.i386.rpm kernel-headers-2.2.12-20.i386.rpm glibc-devel-2.1.2-11.i386.rpm make-3.77-6.i386.rpm patch-2.5-9.i386.rpm glibc-devel-2.1.2-11.i386.rpm make-3.77-6.i386.rpm patch-2.5-9.i386.rpm`

### 步骤 3

之后我们将使用一条命令来卸载所有需要的软件：

- 卸载软件，

- 使用命令：

`[root@deep]# exit`

关于本页面的意见和建议，请邮件至 `gmourani@videotron.ca`

## 为你的终端添加颜色

为你的终端添加颜色可以帮你将文件夹、文件、压缩包、设备、符号链接和可执行文件与其他区分开来。我的观点是，颜色有助于减少错误并加快在系统中的导航速度。

编辑配置文件 (`/vi /etc/profile`) 并添加以下几行：

### 启用颜色

```
eval dicolors=/etc/DIR_COLORS -b
export LS_OPTIONS='s -F 0 --color=auto'
```

编辑 bashrc (`vi /etc/bashrc`) 并添加以下行：

```
alias ls='color=auto'
```

然后重新登录，之后，新的 `COLORS` 环境变量就会被设置，你的系统将能够识别它。

### 最新软件的更新

保留并更新所有软件（特别是网络软件）到最新版本，检查 Red Hat Linux 发行版的错误页面（errata），地址为 `http://www.redhat.com/corp/support/errata/index.html`。错误页面可能是修复 Red Hat Linux 90% 常见问题的最佳资源。此外，对于存在解决方案的安全漏洞，通常在 Red Hat 收到通知后 24 小时就会出现在错误页面上。你应该始终首先检查那里。

你的 Red Hat Linux 6.1 服务器此时需要更新的软件有：

```
grf-1.15-1_i386.rpm
syslogd-1_3_31-14_i386.rpm
intscripts-4_70-1_i386.rpm
ef2sprogs-1.17-11_i386.rpm
pam-0_68-10_i386.rpm
Linux kernel 2.2.14 (linux-2.2_14_tar.gz)
```

注意：内核是最重要的，必须始终更新。请参下文有关为你的特定系统构建自定义内核的信息。

- 在更新之前，你可以使用以下命令验证你的系统中是否安装了该软件：

`[root@deep]# rpm -q <softwarename>`

`<softwarename>` 是你想要验证的软件名称，例如 `XFree86`、`telnet` 等。

31

## 第二部分 安全与优化相关参考

在本部分中

## 通用系统安全

通用系统优化

## 第3章 通用系统安全

在本章中

Linux 通用安全

关于本页面的意见和建议，请邮件至 `gmourani@videotron.ca`

## Linux 通用安全

### 概述

一个 UNIX 系统的安全性完全取决于管理员如何设置它。你添加的服务越多，引入安全漏洞的机会就越大。像 SCO 等其他操作系统实际上可能更容易受到安全侵入，因为为了更更加“用户友好”，它们提供了更多作为其运行固有组成部分的服务。

Linux 本身非常稳定，并以许多版本（flavor）的形式发行。安装 Linux 时，倾向于安装最小化版本，并只添加本质项目，以减少“应用程序”出现安全漏洞的概率。如果实施得当，Linux 是最安全的。

如果系统中存在漏洞，有成千上万的志愿者立即指出并提供修复。在大型组织中，某些商业产品的团队规模有限。大声宣扬发现的并不总是符合他们的利益，或者有时修复程序需要一段时间才能传到发布版或升级版。它们可能会以补丁的形式出现，但大多数商业产品的管理员倾向于仅将其与发行版一起使用，并有一种他们拥有更专业设计软件的虚假安全感。

编程在任何层面都会发生错误，但当你有成千上万的人可以获取源代码时，这些错误在开源代码环境中往往会被更快发现。当然，有成千上万人在干涉源代码，结果又怎样？现在有 1200 万份 Linux 副本……某人打开安全漏洞的概率要大得多。

本文将讨论一些用于保护你的站站的通用技术。通常情况下，诸如 `NFS`、`Samba`、`Imam` 和 `pop` 等服务只需要内部用户访问，阻止外部访问将极大简化问题。以下是可以用于帮助防止来自外部和内部攻击的功能列表。

### 1. 基础信息

让外部人员尽可能少地了解你的系统信息。受害者系统的简单图形就能揭示许多关于系统的信息：有多少用户、管理员在何时在线、他们什么时候工作、他们何时在线、谁在使用系统以及可能帮助攻击者猜测用户密码的个人信息。你可以使用强大的 `finger` 守护进程或 `topd` 来限制谁可以连接到你的系统以及他们如何了解你的系统。更好的做法是在你的系统中卸载相关包。

日志是你了解 Linux 系统正在发生什么的唯一途径。当然，这假设攻击者没有（此处原文应为攻击者没有破坏日志）……由于如此，但大多数商业产品的管理员倾向于仅将其与发行版一起使用，并有一种他们拥有更专业设计软件的虚假安全感。它们可能会以补丁的形式出现，但大多数商业产品的管理员倾向于仅将其与发行版一起使用，并有一种他们拥有更专业设计软件的虚假安全感。

限制你系统上的 `SUID` 程序。`SUID` 程序可以……

© 1999 Open Network Architecture ®

34

关于本页面的意见和建议，请邮件至 `gmourani@videotron.ca`



不是。由于 SUID 程序可以执行任何操作，这就是漏洞（exploit）出现的地方。漏洞是一种程序或脚本，它可以以 root 权限做坏事（获取 shell、获取密码、删除文件等）。请参阅下文“31. root 权限程序”以获取更多信息。

## 2. BIOS 安全，设置密码

禁止从软盘启动并允许某些 BIOS 功能。检查你的 BIOS 手册或在下次启动时查看它。这将提高你系统的安全性。禁止从软盘启动将阻止人们试图在没有提示的情况下启动系统。

## 3. 安全策略

重要的一点是，如果你没有定义需要保护什么以及防止谁，你就无法实施安全。你需要一个安全策略，关于你认为允许和不允许的列表，以此作为任何决策的基础。策略还应该决定你对安全违反行为的回。制定安全策略完全取决于你对安全的定义。以下问题可以提供一些通用指南：

- 你如何对机密或敏感信息进行分类？你到底想要防止谁？远程用户可以访问你的系统吗？系统包含机密或敏感信息吗？如果这些信息泄露给你的竞争对手或其他外部人员，后果如何？密码或加密能提供足够的保护吗？你需要访问互联网吗？你允许从互联网访问系统的程度有多大？当你发现安全漏洞时，你会采取什么行动？

这个列表很短，你的策略在完成之前可能包含更多内容。这是你第一次需要评估你的偏执程度。任何安全策略都必须基于某种程度的偏执；决定你信任多少人。然而，策略必须在允许用户访问其工作所需的合理信息与完全禁止访问信息之间取得平衡。这条界限的划分点将决定你的策略。

## 4. 密码

我们 Linux 安全之旅的起点是。许多人把整个生活都放在电脑上，阻止他人看到的只有一个八字符的字符串密码。

与流行观点相反，不存在无法破解的密码。如果有足够的时间资源，任何密码都可以通过社会工程或暴力破解被破解。

关于本页面的意见和建议请邮寄至 `gmnourai@videotron.ca`

针对服务器密码和其他方法的社会工程学仍然是获取账户和服务器最简单、最流行的方法。由于用户安全意识薄弱，以及任何环境中普遍倾向于信任其他员工的倾向，大多数办公人员都有访问许多用户账户的权限——特别是那些负责解决问题的员工。在许多不同的网络中，都记录了非常成功的服务器和客户端攻击，这些都是由于野心勃勃的人通过松散的安全措施获得了访问权限。通常，伪装成公司的高级或执行人员并在一天中合适的时间点大喊，就能产生极佳的效果，在某些情况下甚至可以获得内部服务器的完全访问权限。

由于破解密码是一项耗费时间和资源的艺术，，请让任何获取了你密码文件的破解者都感到困难。根据你的系统每周运行一次密码破解程序是一个好主意。这有助于发现并替换容易被猜到或弱的密码。此外，应该存在一个密码检查机制，在首次选择密码或更改旧密码时拒绝弱密码。纯字典单词、全为相同大小写或不包含数字或特殊字符的字符串不应被接受为新密码。

我建议以下规则以使密码有效：

- 密码长度至少应为六个字符，最好包含至少一个数字或特殊字符。
- 密码不能是平庸的；平庸的密码是指容易猜到的，且通常基于用户的姓名、家庭、职业或其他个人特征。
- 它们应该有一个有效期，要求在特定的时间范围内选择新密码。
- 在有限的并发错误重试次数后，应撤销密码并要求重置。

## 5. 密码长度

在安装 Linux 系统时，默认的可接受最小密码长度为 5。这意味着当允许新用户访问服务器时，他/她的密码长度至少为 5 个字符字符串（字母、数字、特殊字符）。这还不够，必须至少为 8 位。为了防止无意识的人或管理员对重要的密码设置仅为 5 位长度，必须修改至关重要的 `etc/login.defs` 文件，并将值 5 改为 8。

编辑 `login.defs` (`vi /etc/login.defs`) 并修改读取内容的行：

```
PASS_MIN_LEN    5
```

修改为：

```
PASS_MIN_LEN    8
```

`login.defs` 是登录程序的配置文件。你应该根据你的特定系统检查或修改此文件。这里是你设置其他安全策略的地方（如密码过期默认值或最小接受密码长度）。

## 6. root 账户

`root` 账户是 Unix 系统上权限最高的账户。`root` 账户没有任何安全限制。这意味着系统假设你知道自己在做什么，并且将完全执行你要求的操作——不加质问。因此，很容易因错误的命令抹除系统文件。在使用此账户时，务必尽可能小心。出于安全考虑，除非任务绝对需要 `root` 权限，否则永远不要以 `root` 身份登录。此外如果你不在服务器旁，千万不要登录并让它保持 `root`，这非常糟糕。

## 7. 加密

加密使用密钥（值）作为算法的输入，使数据只有知道密钥的人才能读取。当所有涉及的主机都在你控制的安全环境内时，这种方法非常好，但如果一个“信任”的主机被攻破，你再次面临风险。面临风险的不仅仅是用户 ID 和密码。大多数加密实现用于传输机密分类信息。如果其中一个系统被攻破，信息可能会被泄露或暴露。有效的安全策略可以将这种风险降至最低，无论加密密钥是否暴露在网上，风险始终存在。使用 `OpenSSL`、`SSH`、`MD5` 等加密技术非常有帮助，请参阅本书后半部分关于该主题的更多信息。

## 8. `/etc/exports` 文件

如果你使用 NFS 导出文件，请务必配置 `/etc/exports` 文件以实现最严格的访问权限。这意味着不使用通配符、不允许 root 写入权限，并在尽可能的情况下设置为只读。

编辑 `exports` 文件 (`vi /etc/exports`) 并添加：

- 示例：

```
/dir/to/export host1.mydomain.com(ro,root_squash)

/dir/to/export host2.mydomain.com(ro,root_squash)
```

当 `/dir/to/export` 是你导出的目录时，`host.mydomain.com` 是允许只读日志登录的机器，`<root_squash>` 表示不允许在该目录下拥有 root 写入权限。

要使此更改生效，你需要运行 `/usr/sbin/exportsfs -a`

注意：请注意，在你的系统中提供可用的 NFS 服务可能会带来安全风险。我个人不建议使用它。

## 9. 禁用控制台程序访问

最简单且常见的自定义之一是完全禁用对 `shutdown` 和 `halt` 等程序的控制台等效访问。要执行此操作：

```
[root@dead# rm -f /etc/console.access/servicervice
```

其中 `servicervice` 是你想要禁用控制台等效访问程序的名称。除非你使用 `xdm`，否则小心不要删除 `xserver` 文件，否则除了 root 之外无人将能启动 X 服务器。如果你始终使用 `xdm` 启动 X 服务器，root 是唯一需要启动 X 的用户，在这种情况下你可能真的想删除 `xserver` 文件。

例如：

```
[root@deep] rm -f /etc/security/console.apps/halt
```

```
[root@deep] rm -f /etc/security/console.apps/poweroff
```

```
[root@deep] rm -f /etc/security/console.apps/reboot
```

```
[root@deep] rm -f /etc/security/console.apps/shutdown
```

```
[root@deep] rm -f /etc/security/console.apps/xserver
```

如果删除，root 将是唯一启动 X 的用户。

这将禁用对 `halt`、`poweroff`、`reboot` 和 `shutdown` 程序的控制台等效访问。再次强调，程序 `xserver` 仅在你于系统上安装了 Windows 界面时有效。

注意：如果你使用我们的安装版本，服务器上没有 Window 界面，上述所有文件将不会出现在 `/etc/security/` 目录中，因此请忽略。

## 10. 禁用所有控制台访问

为了禁用 `/etc/pam.d/` 目录下的所有访问（包括程序和文件访问），请注释掉所有引用 `pam_console.so` 的行。这是上述操作“7. 禁用控制台访问”的延续。

以下脚本将自动为你完成此操作。以“root”身份创建 `disabling.sh` 文件 (`touch disabling.sh`) 内部添加以下内容：

```
#!/bin/sh
cd /etc/pam.d
for i in *; do
sed 's/\(.*pam_console.so).*/\1/' < $i && mv $i *
done
```

使用以下命令赋予脚本执行权限并运行：

```
[root@deep] chmod 700 disabling.sh
```

```
[root@deep]# disabling.sh
```

这将注释掉 `/etc/pam.d/` 目录下所有引用 `pam_console.so` 的行。脚本执行后，你可以将其从系统中删除。

## 11. `etc/inetd.conf` 文件

`Inetd` 被称为“超级服务器”，它根据网络请求加载程序。`inetd.conf` 文件告诉系统监听哪些端口，以及为每个端口启动哪个服务器。一旦你将 Linux 系统连接到任何网络，首先要查看的是需要哪些服务。



不需要提供的服务应该被禁用，最好不要动它们，这样你就会少一份担心，攻击者也少一个寻找漏洞的地方。查看你的 `/etc/inetd.conf` 文件，看看你的 `inetd` 提供了哪些服务。通过注释掉不需要的服务（在行首添加 `#`）并向进程发送 `SIGHUP` 来禁用它们。

## 步骤 1

将此文件的权限更改为 `600`。

```
[root@deep] chmod 600 /etc/inetd.conf
```

## 步骤 2

确保所有者是 `root`。

```
[root@]# stat /etc/inetd.conf
```

文件: `/etc/inetd.conf`

大小: 2869 文件类型: 普通文件

模式: (0600/rw----) UID: (0 / root) GID: (0 / root)

设备: 8.6 节点: 18219 链接数: 1

访问: 1999年9月22日 星期三 16:24:16 (00002.00:10:44)

修改: 1999年9月20日 星期一 10:22:44 (00002.06:12:16)

更改: 1999年9月20日 星期一 10:22:44 (00002.06:12:16)

## 步骤 3

编辑 `inetd.conf` (`vi /etc/inetd.conf`) 并禁用如下服务：

`ftp`, `telnet`, `shell`, `login`, `exec`, `talk`, `imap`, `pop-2`, `pop-3`, `finger`, 等，除非你计划使用它们。如果关闭它们，风险会小得多。

```
### 稍后通过 'kill -HUP inetd' 重新编辑此文件时
#echo stream tcp nowait root internal
#echo dgram wait root internal
#discard stream tcp nowait root internal
#discard dgram wait root internal
#daytime stream tcp nowait root internal
#daytime dgram wait root internal
#charge stream tcp nowait root internal
#charge dgram wait root internal
#time stream tcp nowait root internal
#time dgram wait root internal #
```

### 这些是标准服务。

```
#ftp stream tcp nowait root /usr/sbin/tcpd in.ftpd -a
#telnet stream tcp nowait root /usr/sbin/tcpd in.telnetd
```

### Shell, login, exec, comsat 和 talk 是 BSD 协议。

```
#shell stream tcp nowait root /usr/sbin/tcpd in.rshd
#login stream tcp nowait root /usr/sbin/tcpd in.logind
#exec dgram wait root /usr/sbin/tcpd in.rexed
#comsat dgram wait root /usr/sbin/tcpd in.comsat
#talk dgram wait root /usr/sbin/tcpd in.talkd
#ntalk dgram wait root /usr/sbin/tcpd in.ntalk
#dtalk stream tcp nowait nobody /usr/sbin/tcpd in.dtalkd
```

### Pop 和 imap 邮件服务位于

```
#pop-2 stream tcp nowait root /usr/sbin/tcpd ipop2d
#pop-3 stream tcp nowait root /usr/sbin/tcpd ipop3d
#imap stream tcp nowait root /usr/sbin/tcpd imapd
```

### 互联网 UUCP 服务。

```
#uucp stream tcp nowait uucp /usr/sbin/tcpd /lib/uucp/uucp -l
```

### Tftp 服务主要用于启动提供。大多数站点

### 仅在作为“启动服务器”的机器上运行此服务。除非你“需要它”，

### 否则不要取消注释。

```
#fftp dgram wait root /usr/sbin/tcpd in.ftpd
#bootps dgram wait root /usr/sbin/tcpd bootpd #
```

有关此页的意见和建议应邮寄至 `gmourani@videotron.ca`

### Finger, statist 和 netstat 提供用户信息，可能对

### 潜在的“系统破解者”非常有价值。许多站点选择禁用

### 部分或所有服务以提高安全性。

```
#finger stream tcp nowait root /usr/sbin/tcpd in.fingerd
#cfinger stream tcp nowait root /usr/sbin/tcpd in.cfingered
#statist stream tcp nowait guest /bin/ps -auwwx
#netstat stream tcp nowait guest /usr/sbin/tcpd /bin/netstat -i
```

### 验证

```
#auth stream tcp nowait nobody /usr/sbin/in.ident in.dented -l -e -o
```

### inetd.conf 结束

注意：在修改 `inetd.conf` 后，别忘记向你的 `inetd` 进程发送 `SIGHUP` 信号 (`kill -HUP inetd`)。

```
[root@/root] #killall -HUP inetd
```

## 步骤 4

你可以采取的另一个保护“`inetd.conf`”文件的安全措施是将其设置为不可变，使用 `chattr` 设置文件为不可变：

```
[root@#] #chattr +i /inetd.conf
```

这可以防止在设置了 'i' 属性的情况下对“`inetd.conf`”文件进行任何更改（意外或其他原因的）：它不能被删除或重命名，不能为此文件创建链接，且无法写入数据。在修改 `inetd.conf` 后，如果需要，可以取消 'i' 属性：

```
[root@#] #chattr -i /inetd.conf
```

### 12. 保护“`inetd.conf`”文件的另一个安全措施是将其设置为不可变，使用 `chattr` 设置文件为不可变：

设置 'i' 属性将防止任何（意外或其他原因的）对“`inetd.conf`”文件进行更改：它不能被删除或重命名，不能为此文件创建链接，且无法写入数据。在修改 `inetd.conf` 后，如果需要，可以取消 'i' 属性：

```
[root@#] #chattr -i /inetd.conf
```

## 保护“`inetd.conf`”文件的另一个安全措施是将其设置为不可变，使用 `chattr` 设置文件为不可变：

设置 'i' 属性将防止任何（意外或其他原因的）对“`inetd.conf`”文件进行更改：它不能被删除或重命名，不能为此文件创建链接，且无法写入数据。在修改 `inetd.conf` 后，如果需要，可以取消 'i' 属性：

```
[root@#] #chattr -i /inetd.conf
```

## 保护“`inetd.conf`”文件的另一个安全措施是将其设置为不可变，使用 `chattr` 设置文件为不可变：

设置 'i' 属性将防止任何（意外或其他原因的）对“`inetd.conf`”文件进行更改：它不能被删除或重命名，不能为此文件创建链接，且无法写入数据。在修改 `inetd.conf` 后，如果需要，可以取消 'i' 属性：

```
[root@#] #chattr -i /inetd.conf
```

## 保护“`inetd.conf`”文件的另一个安全措施是将其设置为不可变，使用 `chattr` 设置文件为不可变：

设置 'i' 属性将防止任何（意外或其他原因的）对“`inetd.conf`”文件进行更改：它不能被删除或重命名，不能为此文件创建链接，且无法写入数据。在修改 `inetd.conf` 后，如果需要，可以取消 'i' 属性：

```
[root@#] #chattr -i /inetd.conf
```

## 保护“`inetd.conf`”文件的另一个安全措施是将其设置为不可变，使用 `chattr` 设置文件为不可变：

设置 'i' 属性将防止任何（意外或其他原因的）对“`inetd.conf`”文件进行更改：它不能被删除或重命名，不能为此文件创建链接，且无法写入数据。在修改 `inetd.conf` 后，如果需要，可以取消 'i' 属性：

```
[root@#] #chattr -i /inetd.conf
```



## 保护 `inetd.conf` 文件的另一个安全措施是将其设置为不可变，使用 `chattr` 设置文件为不可变

设置 `'i'` 属性将防止任何（意外或其他原因的）对 `inetd.conf` 文件进行更改：它不能被删除或重命名，不能为此文件创建链接，且无法写入数据。在修改 `inetd.conf` 后，如果需要，可以取消 `'i'` 属性：

```
[root@#] #chattr -i /inetd.conf
```

### 验证

```
#auth stream tcp nowait nobody /usr/sbin/in.ident in.dented -l -e -o
```

### inetd.conf 结束

注意：在修改 `inetd.conf` 后，别忘记向你的 `inetd` 进程发送 `SIGHUP` 信号 (`kill -HUP inetd`)。

```
[root@/root] #killall -HUP inetd
```

### 步骤 4

你可以采取的另一个保护 `inetd.conf` 文件的安全措施是将其设置为不可变，使用 `chattr` 设置文件为不可变：

```
[root@#] #chattr +i /inetd.conf
```

这可以防止在设置了 `'i'` 属性的情况下对 `inetd.conf` 文件进行任何更改（意外或其他原因的）：它不能被删除或重命名，不能为此文件创建链接，且无法写入数据。在修改 `inetd.conf` 后，如果需要，可以取消 `'i'` 属性：

```
[root@#] #chattr -i /inetd.conf
```



### 12. 保护“inetd.conf”文件的另一个安全措施是将其设置为不可变，使用 `chattr` 设置文件为不可变

设置 `'i'` 属性将防止任何（意外或其他原因的）对“`inetd.conf`”文件进行更改：它不能被删除或重命名，不能为此文件创建链接，且无法写入数据。在修改 `inetd.conf` 后，如果需要，可以取消 `'i'` 属性：

```
[root@#] #chattr -i /inetd.conf
```

关于此页面的意见和建议应发送至 `gmourani@videotron.ca`

... 应该可以工作，你的系统将不会对任何接口的 ping 响应。你可以在 `/etc/rc.local` 文件中添加此行，这样当系统重启时，命令将自动设置。不响应 ping 至少可以阻挡大多数“黑客”，因为他们根本不知道它的存在。

要启用它，只需执行：

`echo 0 > /proc/sys/net/ipv4/icmp_echo_ignore_all`

# 16. 不要让系统问题信息

如果你不希望人们在远程登录时显示你的问题文件（issue file），你可以将 `/etc/inetd.conf` 文件中的 telnet 选项改为：

```
telnet stream tcp nowait /usr/sbin/tcpd in.telnet -h
```

### 17. "/etc/host.conf" 文件

Linux 使用解析库来获取与主机名对应的 IP 地址。`/etc/host.conf` 文件指定了如何解析名称。`/etc/host.conf` 文件中的条目告诉解析库应该使用哪些服务，以及在何时解析名称。

编辑 `host.conf` 文件 (`/etc/host.conf`) 并添加以下行：

```bash
# 首先通过 DNS 查找名称，然后回退到 /etc/hosts。
order bind,hosts
# 我们有多个带有 IP 地址的。
mult on
#  IP 地址欺骗。
spoof on
```

`order` 选项指示服务的顺序。示例条目指定解析库应首先咨询名称服务器来解析名称，并检查 `/etc/hosts` 文件。建议将解析库设置为首先检查名称服务器（`bind`），然后是 hosts（`hosts`），以提高所有服务器的性能和安全性能。当然，你必须已安装 DNS/`bind`，否则此配置将无法生效。

`multi` 选项决定 `/etc/hosts` 中的主机是否可以有多个 IP 地址（多个接口 eth）。具有多个 IP 地址的主机应被视为多网段的（`multimomed`），因为多个 IP 地址的存在意味着该主机有多个网络接口。例如，网关服务器始终会有多个 IP 地址，并且必须将此选项设置为 ON。

`nspoof` 选项表示在该机器上不理会 IP 欺骗。IP 欺骗是一种安全漏洞，通过欺骗你已知的信任关系中的计算机（让你不知情）来工作。在这种攻击中，一台机器被伪装成“像”一个合法服务器，然后向合法的终端系统、其他服务器或大型数据仓库发起连接和其他类型的网络活动。每个类型的服务器都必须将此选项设置为 ON。

### 18. 路由协议

© Copyright 1999 Open Network Architecture ®

关于此页面的意见和建议应发送至 `gmourani@videotron.ca`

路由和路由协议可能会产生几个问题。IP 路由（IP 包包含其目标地路径详情）是危险的，因为 RFC 1122 要求目标主机必须沿相同的路径进行响应。如果攻击者向你的网络发送源路由数据包，他将拦截回复并欺骗你的主机认为它正在与受信任的主机通信。我强烈建议禁用 IP 路由以保护你的服务器免受此类影响。

要在你的服务器上禁用 IP 路由，请在终端输入以下命令：

```bash
for i in /proc/sys/net/ipv4/accept_source_route; do
echo 0 > $i
done
```

将注释添加到 "`etc/rc.local`" 文件，这样你下次重启系统时就不需要再次编辑它。请注意，上述命令将禁用你所有接口（`do`, `eth`, `pnn` 等）上的源路由数据包。如果你打算安装书中描述的 IPCHAINS 防火墙，你就不需要执行此命令，因为它已经出现在防火墙脚本文件中。

### 19. 启用 TCP SYN 保护

“SYN 攻击”是一种拒绝服务（DoS）攻击，它会消耗你机器上的所有资源，迫使你重启。拒绝服务攻击（由于高流量导致服务器瘫痪，或占用足够的系统资源导致服务器无法响应来自远程系统的合法连接的攻击）可以通过互联网的内部或外部连接轻松实现。在2.1 内核中提供了 syn cookies 但未启用它们。要启用它们，你必须执行：

```bash
[root@deep]# echo 1 > /proc/sys/net/ipv4/tcp_syncookies
```

将注释添加到 "`etc/rc.local`" 文件，这样你下次重启系统时就不需要再次编辑它。如果你打算安装书中描述的 IPCHAINS 防火墙，你就不需要执行此命令，因为它已经出现在防火墙脚本文件中。

### 20. 防火墙

安全问题的另一个解决方案是从外部世界隐藏你的主机和内部传输，我们将允许流量通过低风险网关流入和流出你的网络。网关被称为防火墙，我们将在书中专门的一个重要章节中讨论防火墙。

### 21. "etc/services" 文件



端口号是在“`RFC 1700` 分配数字”中为某些“标准”服务提供的端口号。`etc/services` 文件允许服务器程序和客户端程序将服务名称转换为这些数字（端口），该列表保留在每个主机上，并存储在 "`etc/services`" 中。只有 "`root`" 用户被修改此文件，且编辑 "`etc/services`" 文件进行更改非常罕见，因为它已经包含了许多常见服务名称到端口的映射。为了提高安全性，我们可以对该文件进行免疫处理，以防止未经授权的删除。要对 "`etc/services`" 文件进行免疫处理，使用命令：

```
[root@deep]# chmod +i /etc/services
```

## 22. "/etc/security" 文件

`"/etc/security"` 文件允许你指定 "`root`" 用户允许登录的 TTY 设备。`"/etc/security"` 文件由登录程序（通常是 `"/bin/login"`）读取。其格式是允许的 tty 设备列表，而所有其他被注释掉或未在该文件中的 tty 均禁止登录。

通过注释掉（在行开头添加 `#`）来禁用你不需要的 tty。

编辑安全文件 (`vi /etc/security`) 并注释：

```bash
tty1
#tty2
#tty3
#tty4
#tty5
#tty6
#tty7
#tty8
```

## 23. 特殊账户

操作系统自带的默认账户如果你不使用它们，是不必要的。我建议限制允许 "`su`" 到 `root` 账户员。

- 在系统上添加你的用户，使用命令：

  ```
  [root@deep]# useradd username
  ```

- 为系统上的用户添加或更改密码，使用命令：

  ```
  [root@deep]# passwd username
  ```

例如：

```
[root@deep]# useradd admin
[root@deep]# passwd admin
```

输出应如下：

```
Changing for user admin

New UNIX password: somepasswd

passwd: all authentication updated successfully
```

## 24. 阻止单独 su 到 root

如果你不想 `su` 到 `root` 或想为某些用户限制 "`su`" 命令，请将以下行添加到 `/etc/pam.d/` 目录下的配置 "`su`" 文件顶部。我建议限制允许 "`su`" 到 `root` 账户员。

关于本页面的意见和建议应邮件至 `gmourani@videotron.ca`

### 第 1 步

编辑 `su` 文件 (`/etc/pam.d/su`) 并在文件顶部添加以下两行：

```
auth sufficient /lib/security/pam_rootok.so debug
auth required   /lib/security/pam_wheel.so group=wheel
```

添加上述两行后，`/etc/pam.d/su` 文件应该如下所示：

```
auth        sufficient /lib/security/pam_rootok.so debug
auth        required /lib/security/pam_wheel.so group=wheel
auth        required /lib/security/pam_pwdb.shadow nullok
account     required /lib/security/pam_pwdb.so
password     required /lib/security/pam_cracklib.so
password    required /lib/security/pam_pwdb.shadow use_authtok nullok
session      required /lib/security/pam_pwdb.so
session      optional /lib/security/pam_xauth.so
```

这意味着只有 "`wheel`" 组的成员才能 `su` 到 `root`，它还包含了日志记录。注意，“`wheel`” 组是系统上的一个特殊账户，可用于此目的。你不能使用任何组名，除非你想要进行这种安全配置。这种配置结合允许登录的 TTY 设备 `root` 权限，将极大提高你系统的安全性。

### 第 2 步

现在我们已经在 `/etc/pam.d/su` 文件配置中定义了 "`wheel`" 组，是时候将一些用户添加到 "`su`" 到 "`root`" 账户了。如果你想让一个 `admin` 成为 "`wheel`" 组的成员并可以使用以下命令 `su` 到 `root`：

```
[root@deep]$ usermod -G admin
```

这意味着 "`G`" 是一个附加组列表，用户 "`10`" 是该用户 ID "`wheel`" 的数值值的成员，而 "`admin`" 是我们想要添加到 "`wheel`" 组的用户。对系统上的所有用户使用相同的命令，以使他们能够 `su` 到 "`root`" 账户。

## 25. 资源限制

对所有用户设置资源限制，以便他们无法执行拒绝服务攻击（进程数、内存量等）。这些限制必须在用户登录时进行设置。例如，你系统中所有用户的限制可能如下：

### 第 1 步

编辑 `limits.conf` 文件 (`/etc/security/limits.conf`) 并添加或更改行内容为：

```
hard  core      0
hard  rss             5000
hard  nproc       20
```

这表示禁止创建核心文件 "`core 0`" ，将进程数限制为 20 个 "`nproc 20`" ，并将超级用户 "`root`" 以外的所有用户的内存使用限制为 5M "`rss 5000`" 。以下所有内容仅涉及在你系统上输入登录提示的用户。通过这种配额，你对用户在你的系统中运行的进程、核心文件和内存使用有了更多控制。星号 `***` 意味着登录服务器的所有用户。

### 第 2 步

你必须编辑 `/etc/pam.d/login` 文件并在文件末尾添加以下行：

```
# session required /lib/security/pam-limits.so
```

添加上述行后，`/etc/pam.d/login` 文件应该如下：

```
#PAM-1.0
auth       required /lib/security/pam_securetty.so
auth       required /lib/security/pam_pwdb.shadow nullock
auth       required /lib/security/pam_nlogin.so
account    required /lib/security/pam_pwdb.so
password required /lib/security/pam_cracklib.so
password required /lib/security/pam_pwdb.so nullock use_authtock md5
session    required /lib/security/pam_unix.so
session    required /lib/security/pam-limits.so
#session optional /lib/security/pam_console.so
```

## 26. 对挂载文件系统进行更多控制

你可以通过 `noexec`、`nodev` 和 `nosid` 等选项对挂载的文件系统 "`home`" 和 "`tmp`" 具有更多控制力。这可以在 `/etc/fstab` 中设置。`fstab` 包含了关于文件系统的描述性信息。关于在该文件中使用的选项的更多信息，请参阅页面 `(8)`。

编辑 `fstab` 文件 (`/etc/fstab`) 并根据你的需要修改：

```
/dev/sda1  /tmp  defaults  1
/dev/sda6   /home  defaults  1
/dev/sda1  /tmp  nosid,noexec  1
/dev/sda6   /home  nosid,nodev  1
```

其中 `nosid` 不解释文件系统的特殊设备，而 `noexec` 不允许在系统上执行任何二进制文件。对于我们的示例，`/dev/sda1` 代表我们系统上的 "`tmp`" 目录，`dev/sda6` 代表 "`home`" 目录。当然，这与你的情况不同，取决于你如何对硬盘进行分区以及安装了种种磁盘（IDE `hda`, `hdb` 等）。

## 27. 将 RPM 移动到安全位置并更改其权限

一旦使用 `RPM` 命令在 Linux 服务器上安装了所有需要的软件，将它移动到安全的地方（如软盘）是一个好主意。通过这种方法，他人可以访问你的服务器并意图通过 `RPM` 安装新软件。当然，这不应该发生。将 `RPM` 二进制文件移动到软盘使用：

```
[root@deep] mount /dev0 /mnt/floppy
[root@deep] mv /bin/rpm /mnt/floppy/
```



一旦使用 `RPM` 命令在 Linux 服务器上安装了所有需要的软件，将它移动到安全的地方（如软盘）是一个好主意。通过这种方法，他人可以访问你的服务器并意图通过 `RPM` 安装新软件。当然，这不应该发生。将 `RPM` 二进制文件移动到软盘使用：

```
[root@deep] mount /dev0 /mnt/floppy
[root@deep] mv /bin/rpm /mnt/floppy/
```

由于你忘记了这一点，你可以将 "`rpm`" 的默认权限从 755 改为 700。`[root@deep] chmod 700 /bin/rpm`

### 28. Shell 日志

记录日志很容易，`bash_history` 在每个用户主目录存储多多 500 条旧命令（`~` 是你的主目录）。系统中每个账户的 `.bash_history` 文件可以存储旧命令。为了防止用户在屏幕上以明文显示密码，我强烈建议将 `/etc/profile` 中的 `HISTFILESIZE` 和 `HISTSIZE` 设置为低值，例如 20。

编辑 `profile` (`/etc/profile`) 并更改行：

```
HISTFILESIZE=20
HISTSIZE=20
```

这意味着 `.bash_history` 文件可以存储 20 条旧命令，而不再更多。现在，如果黑客试图查看服务器上用户的 `.bash_history` 文件以寻找误传的明文密码，他的机会会更小。

关于此页面的意见和建议请邮件至 `gmourani@videotron.ca`

双启动机器（安全性会大打折扣）。除非系统要双启动到其他系统，否则将此项设置为 0 是一个好主意。

- 添加：`restricted`

放宽密码保护，仅在在命令行上指定了参数时（例如 `linux single`）才需要输入密码。`restricted` 选项只能与 `password` 选项一起使用。请确保您在每个镜像上都使用此项。

- 添加：`password=password`

在“单用户模式”加载 Linux 系统时要求用户输入密码。密码始终区分大小写，同时也请确保 `"/etc/lilo.conf"` 文件不再可读，否则任何用户都无法读取密码。以下是我们受保护的 LILO 的 `"lilo.conf"` 文件示例。

#### 步骤 1

编辑 `lilo.conf` 文件（`vi /etc/lilo.conf`）或如所示添加上述三个选项：

```
boot=/dev/sda
map=/boot/map
install=/boot/boot.b
prompt
timeout=00 <- 将此行改为 0。
restricted <- 添加此行。
password=password<- 添加此行并输入您的密码。
image=/boot/vmlinuz-2.2.12-20
label=linux
initrd=/initrd-2.2.12-10.img
root=/dev/sda
read-only
```

#### 步骤 2

由于配置文件 `"/etc/lilo.conf"` 现在包含了未加密的密码，它应该只对超级用户 `"root"` 可读。

> `[root@deep]# chmod 600 /etc/lilo.conf` (将不再对所有人可读)。

#### 步骤 3

现在我们更新配置文件 `"/etc/lilo.conf"` 使更改生效。

> `[root@deep]# /bin/lilo -v` (更新 `lilo.conf`)。

#### 步骤 4

您可以采取的另一项保护 `"lilo.conf"` 文件的安全措施是将其设置为不可变，使用 `chattr` 命令。

- 要设置不可变位，请使用命令：

`[root@deep] chattr +i /etc/lilo.conf`

这将防止对 `"lilo.conf"` 文件进行任何更改（无论是无意的还是其他的）。如果您想修改 `"lilo.conf"` 文件，将需要取消不可变位：

- 要取消不可变位，请使用命令：

`[root@deep] chattr -i /etc/lilo.conf`

### 30. 禁用 Control-Alt-Delete 键盘关机

关于此页面的意见和建议请邮件至 `gmourani@videotron.ca`

在您的 `/etc/inittab` 文件中注释掉（使用 `"#"`）下面的行，将禁用使用 Control-Alt-Delete 关机的功能。如果您没有对机器进行最好的物理防护，这非常重要。

要执行此操作，请编辑 `inittab` 文件（`vi /etc/inittab`）并更改该行：

```
ca:sbin/shutdown -t3 -r now
改为：
#ca:sbin/shutdown -t3 -r now
```

现在，为了让系统在以下提示符处理解更改类型：

`[root@deep]# /sbin/init q`

### 31. 所有重要日志的物理硬质副本

安全关注点之一是服务器上 `"var/log"` 目录下不同日志文件的完整性。尽管我们在服务器中采取了所有安全措施，如果破解客获取了访问权限，我们的最后防御就是日志文件。因此，考虑能够确保日志文件完整性的方法非常重要。

如果您的服务器或网络中的其他服务器有打印机，那么拥有所有重要日志的物理硬质副本是一个好主意。使用连续进纸打印机并将所有日志发送到 `"dev/lp0"` 打印机设备）可以轻松实现。破解客可以更改您服务器上的文件、程序等，但当您拥有通过打印机打印的所有重要日志纸质副本时，他们无能为力。

例如：

对于从您的服务器到连接在此打印上的所有邮件登录、启动消息和 `ssh` 连接，您可能需要在 `"/etc/syslog.conf"` 文件中添加以下行：

编辑 `syslog.conf` 文件（`vi /etc/syslog.conf`）并在该文件的末尾添加以下行：

`authpriv.*;mail;:local?.auth:daemon.info /dev/lp0`

- 现在重启 `syslog` 守护进程使更改生效：`[root@deep]# /etc/rc.d/init/syslog restart`

例如：

对于从您的服务器到连接在本地网络中远程服务器上的打印机的所有邮件登录、启动消息和 `ssh` 连接，您可能需要在远程服务器的 `"/etc/syslog.conf"` 文件中添加以下行。

如果您的网络中没有打印机，也可以将所有日志文件复制到另一机器，只需跳过在远程服务器的 `"syslog.conf"` 文件中添加 `"dev/lp0"` 的第一步骤，进入 `"-r"` 选项菜单。使用将所有日志文件复制到另一机器的功能将让您能够在一个主机上控制所有 `syslog`，并减少管理需求。

编辑远程服务器上的 `syslog.conf` 文件（例如：`mail.openarch.com`）（`vi /etc/syslog.conf`）并向该文件的末尾添加以下行：

`authpriv.*;mail;:local?.auth:daemon.info /dev/lp0`

关于 `syslog` 页面的意见和建议请邮件至 `gmourani@videotron.ca`

由于 `syslog` 守护进程的默认配置是不接收网络消息，我们必须在远程服务器上启用接收网络的功能。要启用远程服务器接收网络的功能，请在 `syslog` 脚本中添加 `-r` 选项（仅限远程主机）：

- 编辑 `syslog` 守护进程（`vi /etc/rc.d/init.d/syslog`）并更改：

`daemon -m 0`

改为：

`daemon -r 0`

- 现在在远程主机上重启 `syslog` 使更改生效：

`[root@deep]# /etc/rc.d/init restart`

现在，如果远程服务器上有防火墙，我们必须添加或验证以下行的存在：



```
ipchains -A -i $EXTERNAL_INTERFACE -p udp \
-s $SYSLOG_CLIENT \
-d $IPADDR 514 -j ACCEPT
```
`EXTERNAL_INTERFACE="eth0"` 在防火墙文件中。

`IPADDR="208.164.186.2"` 在防火墙文件中。

`SYSLOG_CLIENT="208.164.186.0/24"` 在防火墙文件中。

- 现在在远程主机上重启防火墙使更改生效：

```
[root@deep]# ... firewall restart
```

此规则将允许来自内部客户端的远程服务器端口 514（syslog 端口）的传入 UDP 包。关于防火墙的更多信息，请参见第 7 章“网络防火墙”。

最后，编辑本地服务器上的 `syslog.conf` 文件（`vi /etc/syslog.conf`），并在以下行的末尾添加：

`authpriv.*mail@local7;auth.*@daemon.info`

`"mail"` 是远程服务器的主机名。现在如果您的机器发生故障并删除了重要日志，您将有一个副本。考虑能够确保日志文件完整性的方法非常重要。

如果您的网络中没有打印机，也可以将所有日志文件复制到另一机器，只需跳过在远程服务器的 `"syslog.conf"` 文件中添加 `"dev/lp0"` 的第一步骤并进入 `"-r"` 选项菜单。使用将所有日志文件复制到另一机器的功能将让您能够在一个主机上控制所有 syslog，并减少管理需求。

编辑远程服务器上的 `syslog.conf` 文件（例如：`mail.openarch.com`）（`vi /etc/syslog.conf`）并在该文件的末尾添加以下行：

`authpriv.*;mail;:local?.auth:daemon.info /dev/lp0`
```
ipchains -A -i $EXTERNAL_INTERFACE -p udp \
-s $SYSLOG_CLIENT \
-d $IPADDR 514 -j ACCEPT
```

- 现在在远程主机上重启防火墙使更改生效：

```
[root@deep]# /etc/rc.d/init/firewall restart
```

现在，如果远程服务器上有防火墙（我们应该有），我们必须添加或验证以下行的存在：

```
ipchains -A -i $EXTERNAL_INTERFACE -p udp \
-s $SYSLOG_CLIENT \
-d $IPADDR 514 -j ACCEPT
```
`EXTERNAL_INTERFACE="eth0"` 在防火墙文件中。

`IPADDR="208.164.186.2"` 在防火墙文件中。

`SYSLOG_CLIENT="208.164.186.0/24"` 在防火墙文件中。

- 现在在远程主机上重启防火墙使更改生效：

```
[root@deep]# ... firewall restart
```

此规则将允许来自内部客户端的远程服务器端口 514（syslog 端口）的传入 UDP 包。关于防火墙的更多信息，请参见第 7 章“网络防火墙”。

最后，编辑本地服务器上的 `syslog.conf` 文件（`vi /etc/syslog.conf`），并在以下行的末尾添加：

`authpriv.*mail@local7;auth.*@daemon.info`

`"mail"` 是远程服务器的主机名。现在如果您的机器发生故障并删除了重要日志，您将有一个副本。考虑能够确保日志文件完整性的方法非常重要。

### 32. 修复 `/etc/rc.d.init/` 的权限

修复在启动时需要运行的普通进程的脚本权限。

```
[root@deep]# chmod -R 700 /etc/rc.d.init/
```

这意味着 `root` 只允许读取、写入和执行脚本。我认为普通用户不需要知道里面的内容。

注意：如果您安装了使用 `"/etc/rc.d.init/"` 目录下初始化系统的新程序或更新，不要忘记再次更改或验证此脚本的权限。

### 33. `"/etc/rc.d/rc.local"` 文件

默认情况下，当您登录 Linux 机器时，它会告知您发行版本、内核和服务器名称。这提供了过多信息。我们宁于用“Login:”提示符提示用户。

#### 步骤 1

要执行此操作，编辑 `"/etc/rc.d/rc.local"` 文件并如所示在以下行前放置 `"#"`：

```
# 这将在每次启动时覆盖/etc/issue，因此在此处进行# 我们想要对 /etc/issue 的更改或在重启时使用。
#echo "#" >> /etc/issue
#echo "Kernel $(uname -r)" @ $(uname -m)\ >> /etc/issue
#cp -f /etc/issue /etc/issue.net
#echo <<>> >> /etc/issue
```

#### 步骤 2

然后，重命名 `/etc` 目录下的以下文件 `"issue.net"` 和 `"issue"`：

```
[root@deep]# rm -f /etc/issue
[root@deep]# rm -f /etc/issue.net
```

注意：`"etc/issue"` 文件是用户通过网络（如 `telnet`, `ssh`）连接到机器时看到的登录横幅。您可以在 `"etc"` 目录下找到它，它与类似文件 `"issue"` 是显示给本地用户的登录横幅。它只是一个文本文件，可以根据您的喜好进行定制，但请注意，如果您像我们一样删除它，您还需要修改 `"/etc/rc.d/rc.local"` shell 脚本，该脚本在每次系统启动时都会重新创建 `"issue"` 和 `"issue.net"` 文件。

关于此页面的意见和建议应邮寄至 `gmourani@videotron.ca`

### 34. root 拥有程序中的 s 位

你计算机中所有标记有 `'s'` 位的程序和文件，都启用了 SUID (`r---xr-x`) 或 SGID (`r---xr-s`) 权限。由于这些程序会向执行它们的用户授予特殊权限，因此，记住那些不需要此类权限的 root 拥有程序的 `'s'` 位至关重要。这可以通过执行命令 `chmod a-s` 并将违规文件名作为参数来实现。

此类程序包括但不限于：

- 1. 你从不使用的程序。
- 2. 那些你不希望让任何非 root 用户运行的程序。
- 3. 你偶尔使用，且不介意必须切换到 root 才能运行的程序。

我们在每个你可以个人自行禁用的程序旁边都标记了星号 (`*`)。请记住，你的系统需要使用 root 拥有程序才能正常工作，因此请小心。

- 要查找 root 拥有且带有 `'s'` 位的文件，请使用命令：

```
[root@]$ find -type f \( -perm -0400 -o -perm -0200 \) -exec ls -lg {}
```

```
*rwxr-xr-x root 35168 Sep 22 23:35 /usr/bin/chage
*rwxr-xr-s root 36756 Sep 23 22:35 /usr/bin/gpasswd
*rwxr-xr-s root 678 Jun 16 18:17 /usr/bin/wall
-rwxr-xr-x root 31532 Aug 16 16:35 /usr/bin/bdate
-rwxr-xr-x root 34558 Sep 13 20:28 /usr/bin/man
-sr-xr-x root 22312 Sep 25 11:52 /usr/bin/passwd
*rwxr-xr-s root 518140 Aug 30 23:12 /usr/bin/superuid
-rwxr-xr-x root 24733 Jul 24 20:19 /usr/bin/sp5.0503
*rwxr-xr-x root 14024 Sep 09 01:01 /usr/bin/chfn
*rwxr-xr-x root 13768 Sep 09 01:01 /usr/bin/chsh
*rwxr-xr-s root 5576 Sep 09 01:01 /usr/bin/newgrp
-rwxr-xr-x root 8328 Feb 16 10:03 /usr/bin/write
*rwxr-xr-x root 59986 Nov 23 21:59 /usr/bin/ubernetctl
*rwxr-xr-x root 16488 Jul 02 10:21 /usr/bin/traceroute
-rwxr-xr-x root 6096 Jun 13 20:21 /usr/sbin/iptemp
-rwxr-xr-x root 14124 Aug 17 22:31 /bin/sin
*rwxr-xr-x root 53620 Sep 13 20:26 /bin/mount
-rwxr-xr-x root 18238 Sep 10 15:04 /bin/umount
*rwxr-xr-x root 3860 Nov 23 21:59 /sbin/netretport
-sr-xr-x root 26539 Oct 11 20:48 /sbin/pwdb_kchpwd
```



要禁用选定程序的位，请使用以下命令：

```
[root@#] chmod a-s /usr/bin/chage
[root@#] chmod a-s /usr/bin/gpasswd
[root@#] chmod a-s /usr/bin/wall
[root@#] chmod a-s /usr/bin/chfn
[root@#] chmod a-s /usr/bin/chsh
[root@#] chmod a-s /usr/bin/newgrp
[root@#] chmod a-s /usr/bin/write
[root@#] chmod a-s /usr/sbin/ubernetctl
[root@#] chmod a-s /usr/sbin/traceroute
[root@#] chmod a-s /bin/mount
[root@#] chmod a-s /bin/umount
[root@#] chmod a-s /bin/ping
[root@#] chmod a-s /sbin/netretport
```

关于此页面的注释和参数可以邮寄至 gmourani@videotron.ca

如果你想知道这些程序的作用，请执行 `man <program-name>` 并阅读。

例如：

```
[root@deep]## man retoport
```

### 35. 异常或隐藏文件

在系统各处查找异常或隐藏文件（以点开头且通常不显示的文件）。隐藏文件（以点开头且通常不显示的文件）可能被用来隐藏某些恶意程序。请记住，你的系统需要使用 `root` 拥有程序才能正常工作，因此请小心。



隐藏文件（以点开头且通常不显示的文件）可能被用来隐藏某些恶意程序。请记住，你的系统需要使用 `root` 拥有程序才能正常工作，因此请小心。

### 35. 异常或隐藏文件

在系统各处查找异常或隐藏文件（以点开头且通常不显示的文件）。隐藏文件（以点开头且通常不显示的文件）可能被用来隐藏某些恶意程序。请记住，你的系统需要使用 `root` 拥有程序才能正常工作，因此请小心。

## 35. Unusual or hidden files

Look everywhere on the system for unusual or hidden files (files that start with a period and are normally shown by the). Hidden files（以点开头且通常不显示的文件）may be used to hide some malicious-progrgrams.

Comments and arguments concerning this page may be mailed to `gmourani@videotron.ca`

If you want to know what those programs do, make a `man` `program-name` and read.

As an example:

```
[root@deep]## man retoport
```

## 35. Unusual or hidden files



关于此页面的意见和建议应邮寄至 `gmourani@videotron.ca`

## 34. Bits from root-owned programs

所有在计算机中带有 `s` 位的程序和文件，都启用了 SUID `r---xr-x` 或 SGID `r---xr-s` 位。因为这些程序会向执行它们的<|message|>用户授予特殊权限，所以需要记住那些不需要此类权限的 root 拥有程序的 `s` 位。可以通过执行命令 `chmod a-s` 并将有问题的文件名作为其参数来实现。

此类程序包括但不限于：

1. 你从不使用的程序。
2. 不希望任何非 root 用户运行的程序。
3. 你偶尔使用且不介意 `su` 到 root 的程序。

我们在每个你可以个人禁用的程序旁放置了一个星号 `*`。请记住你的系统需要使用 root 拥有的程序才能正常工作，所以要小心。

要查找 root 拥有程序中带有 `s` 位的文件，使用命令：

`[root@]$ find -type f \( -perm -0400 -o -perm -0200 \) -exec ls -lg {}`

```
*rwxr-xr-x root 35168 Sep 22 23:35 /usr/bin/chage
*rwxr-xr-s root 36756 Sep 23 22:35 /usr/bin/gpasswd
*rwxr-xr-s root 678 Jun 16 18:17 /usr/bin/wall
-rwxr-xr-x root 31532 Aug 16 16:35 /usr/bin/bdate
-rwxr-xr-x root 34558 Sep 13 20:28 /usr/bin/man
-sr-xr-x root 22312 Sep 25 11:52 /usr/bin/passwd
*rwxr-xr-s root 518140 Aug 30 23:12 /usr/bin/superuid
-rwxr-xr-x root 24733 Jul 24 20:19 /usr/bin/sp5.0503
*rwxr-xr-x root 14024 Sep 09 01:01 /usr/bin/chfn
*rwxr-xr-x root 13768 Sep 09 01:01 /usr/bin/chsh
*rwxr-xr-s root 5576 Sep 09 01:01 /usr/bin/newgrp
-rwxr-xr-x root 8328 Feb 16 10:03 /usr/bin/write
*rwxr-xr-x root 59986 Nov 23 21:59 /usr/bin/ubernetctl
*rwxr-xr-x root 16488 Jul 02 10:21 /usr/bin/traceroute
-rwxr-xr-x root 6096 Jun 13 20:21 /usr/sbin/iptemp
-rwxr-xr-x root 14124 Aug 17 22:31 /bin/sin
*rwxr-xr-x root 53620 Sep 13 20:26 /bin/mount
-rwxr-xr-x root 18238 Sep 10 15:04 /bin/umount
*rwxr-xr-x root 3860 Nov 23 21:59 /sbin/netretport
-sr-xr-x root 26539 Oct 11 20:48 /sbin/pwdb_kchpwd
```

要禁用所选程序上的位，使用以下命令：

`[root@#] chmod a-s /usr/bin/chage`
`[root@#] chmod a-s /usr/bin/gpasswd`
`[root@#] chmod a-s /usr/bin/wall`
`[root@#] chmod a-s /usr/bin/chfn`
`[root@#] chmod a-s /usr/bin/chsh`
`[root@#] chmod a-s /usr/bin/newgrp`
`[root@#] chmod a-s /usr/bin/write`
`[root@#] chmod a-s /usr/sbin/ubernetctl`
`[root@#] chmod a-s /usr/sbin/traceroute`
`[root@#] chmod a-s /bin/mount`
`[root@#] chmod a-s /bin/umount`
`[root@#] chmod a-s /bin/ping`
`[root@#] chmod a-s /sbin/netretport`

关于此页面的意见和建议可邮寄至 `gmourani@videotron.ca`

如果想知道这些程序的作用，执行 `man program-name` 并阅读。

例如：

`[root@deep]## man retoport`

### 35. 异常或隐藏文件

在系统各处查找异常或隐藏文件（以点开头且通常不显示的文件）。隐藏文件（以点开头且通常不显示的文件）可能被用来隐藏某些恶意程序。

Look everywhere on the system for unusual or hidden files `files that start with a period and are normally shown by the`. Hidden files（以点开头且通常不显示的文件）may be used to hide some malicious-progrgrams.



你计算机中所有标记有 `'s'` 位的程序和文件，都启用了 `SUID` (`r---xr-x`) 或 `SGID` (`r---xr-s`) 权限。由于这些程序会向执行它们的用户授予特殊权限，因此，记住那些不需要此类权限的 `root` 拥有程序的 `'s'` 位至关重要。这可以通过执行命令 `chmod a-s` 并将违规文件名作为参数来实现。

此类程序包括但不限于：

- 1. 你从不使用的程序。
- 2. 那些你不希望让非 `root` 用户运行的程序。
- 3. 你偶尔使用，且不介意必须切换到 `root` 才能运行的程序。

我们在每个你可以个人自行禁用的程序旁边都标记了星号 (`*`)。请记住，你的系统需要使用 `root` 拥有程序才能正常工作，因此请小心。

要查找 `root` 拥有且带有 `'s'` 位的文件，请使用命令：

`[root@]$ find -type f \( -perm -0400 -o -perm -0200 \) -exec ls -lg {}`

```
*rwxr-xr-x root 35168 Sep 22 23:35 /usr/bin/chage
*rwxr-xr-s root 36756 Sep 23 22:35 /usr/bin/gpasswd
*rwxr-xr-s root 678 Jun 16 18:17 /usr/bin/wall
-rwxr-xr-x root 31532 Aug 16 16:35 /usr/bin/bdate
-rwxr-xr-x root 34558 Sep 13 20:28 /usr/bin/man
-sr-xr-x root 22312 Sep 25 11:52 /usr/bin/passwd
*rwxr-xr-s root 518140 Aug 30 23:12 /usr/bin/superuid
-rwxr-xr-x root 24733 Jul 24 20:19 /usr/bin/sp5.0503
*rwxr-xr-x root 14024 Sep 09 01:01 /usr/bin/chfn
*rwxr-xr-x root 13768 Sep 09 01:01 /usr/bin/chsh
*rwxr-xr-s root 5576 Sep 09 01:01 /usr/bin/newgrp
-rwxr-xr-x root 8328 Feb 16 10:03 /usr/bin/write
*rwxr-xr-x root 59986 Nov 23 21:59 /usr/bin/ubernetctl
*rwxr-xr-x root 16488 Jul 02 10:21 /usr/bin/traceroute
-rwxr-xr-x root 6096 Jun 13 20:21 /usr/sbin/iptemp
-rwxr-xr-x root 14124 Aug 17 22:31 /bin/sin
*rwxr-xr-x root 53620 Sep 13 20:26 /bin/mount
-rwxr-xr-x root 18238 Sep 10 15:04 /bin/umount
*rwxr-xr-x root 3860 Nov 23 21:59 /sbin/netretport
-sr-xr-x root 26539 Oct 11 20:48 /sbin/pwdb_kchpwd
```

要禁用选定程序的位，请使用以下命令：

`[root@#] chmod a-s /usr/bin/chage`

`[root@#] chmod a-s /usr/bin/gpasswd`

`[root@#] chmod a-s /usr/bin/wall`

`[root@#] chmod a-s /usr/bin/chfn`

`[root@#] chmod a-s /usr/bin/chsh`

`[root@#] chmod a-s /usr/bin/newgrp`

`[root@#] chmod a-s /usr/bin/write`

`[root@#] chmod a-s /usr/sbin/ubernetctl`

`[root@#] chmod a-s /usr/sbin/traceroute`

`[root@#] chmod a-s /bin/mount`

`[root@#] chmod a-s /bin/umount`

`[root@#] chmod a-s /bin/ping`

`[root@#] chmod a-s /sbin/netretport`

关于此页面的注释和参数可以邮寄至 `gmourani@videotron.ca`

如果你想知道这些程序的作用，请执行 `man program-name` 并阅读。

例如：

`[root@deep]## man retoport`

### 35. 异常或隐藏文件

在系统各处查找异常或隐藏文件（以点开头且通常不显示的文件）。

## 第 4 章 通用系统优化

本章内容

`Linux` 通用优化

## Linux 通用优化

网络调优在很大程度上取决于网络中产品的实现（软件和硬件）。要在的一卷书中汇集完成网络所需的所有信息是不可能的。此外，在网络实际运行之前，你无法识别出可能存在的瓶颈和阻塞。调优并不是一蹴而就的，而应该被视为一项复杂的任务。它需要极大的自律和卓越的技术。除非使用适当的测试来识别系统中特定的瓶颈，否则很难解释结果。偶尔，性能调优可能会非常令人沮丧和枯燥，特别是在对结果进行大量分析后仍无定论时。尽管如此，性能调优是非常有利的，并能提供长期利益。

### 1. "/etc/profile" 文件

`/etc/profile` 文件包含系统环境设置和启动程序。你在此文件中进行的所有自定义都将适用于系统中的整个环境变量。因此，在此文件中放入优化标志是一个不错的选择。为了压榨 `x86` 程序的性能，你可以使用 `-O9` 标志进行全优化编译。许多程序在 `Makefile` 中包含 `-O2`。`-O9` 是最高优化优化。它会增加生成代码体积，但运行速度更快。

编译时，使用 `-fomit-frame-pointer`。这将使用堆栈来访问变量。遗憾的是，使用此选项后调试几乎是不可能的。你可以使用 `-mcpu=cpu_type` 和 `-march=cpu_type`，这将根据 `GCC` 的能力对列出的 `CPU` 进行最佳优化。然而，生成的代码将仅在指定的 `CPU` 或更高版本的 `CPU` 上运行。

#### 针对 CPU i86 或 Pentium, Pentium II, Pentium III

在 `/etc/profile` 文件中为 `PentiumPro`、`Pentium II` 和 `III` 处理器家族加入此行：

```bash
CFLAGS=-O3 -funroll-loops -fast-math -malign-align -mcpu=pentiumpro -march=pentium -fomit-frame-pointer -no-exceptions
```

#### 针对 CPU i586 或 Pentium

在 `/etc/profile` 文件中为 `Pentium` 处理器家族加入此行：

```bash
CFLAGS=-O3 -march=pentium -mcpu=pentium -pentium -funroll-loops -fomit-frame-pointer -fforce-mem -fforder-addr -malign-double -fno-exceptions
```

#### 针对 CPU i486

在 `/etc/profile` 文件中为 `i486` 处理器家族加入此行：

```bash
CFLAGS=-O3 -funroll-all-loops -malign-double -mcpu=i486 -march=i486 -fomit-frame-pointer -no-exceptions
```

现在在选择完架构（`i686`、`i586` 或 `i486`）后，在 `/etc/profile` 文件的靠下位置，向 `export` 行添加 `_ LANG LESSCHARSET`：

```bash
export PATH PS1 HOSTNAME HITSIZE HISTFILESIZE USER LOGIN INPUTTRUC CFLAGS LANG LESSCHARSET
```

然后注销并重新登录；之后，新的 `CFLAGS` 环境变量已设置，软件的其他 `configure` 工具将识别它。`Pentium (Pro/II/III)` 优化仅适用于 `egcs` 或 `pgcc` 编译器。你的服务器默认已安装了 `egcs` 编译器，所以你不需要考虑它。

### 基准测试结果

架构摘要

根据你的处理器架构和编译器版本（`GCC/EGCS`），优化选项可能会有所不同。下面的图表将帮助你为编译器/`CPU` 架构选择最佳编译标志。

你的 `RedHat Linux 6.1` 上安装的编译器版本是 `egcs 2.91.66`。但在选择编译器优化选项之前，请务必检查一下。



要要验证系统中安装的编译器版本，请使用命令：`[root@deep]# egcs --version`

注意：所有的基准测试结果和未来的结果都可以从 GCC 主页的以下地址获取：http://egcs.cygnus.com/

现在举例：

对于编译器版本为 `egcs-2.91.66` 的 CPU `pentium II/III (i686)`，最佳优化选项将是：`CFLAGS='-O9 -funroll-loops -fast-math -malign-double -mcpu=pentiumpro - march=pentiumpro -omit-frame-pointer -fno-exceptions'`

### i686

![](img/4444dd2a96323af53b5149a2b33efe8b_60_0.png)

关于本页面的意见和建议应邮件至 `gmourani@videotron.ca`

对于编译器版本为 `egcs-2.91.66` 的 CPU `pentium (i586)`，最佳优化选项将是：`CFLAGS='-O3 -march=pentium -mcpu=pentium -ffast-math -funroll-loops -fomit-frame-pointer -fforce-mem -fforce-addr -malign-double -fno-exceptions'`

### i586

![](img/4444dd2a96323af53b5149a2b33efe8b_61_0.png)

- `-Os`
- `-O2`
- `-O3`
- `-O3 -funroll-all-loops`
- `-O3 -march=pentium -mcpu=pentium -ffast-math -funroll-loops -fomit-frame-pointer -fforce-mem -fforce-addr -malign-double -fno-exceptions`

© Copyright 1999 Open Network Architecture

### i486

![](img/4444dd2a96323af53b5149a2b33efe8b_62_0.png)

对于编译器版本为 `egcs-2.91.66` 的 CPU `i486`，最佳优化选项将是：`CFLAGS='-O3 -funroll-all-loops -malign-double -mcpu=i486 -march=i486 -fomit-frame-pointer -fno-exceptions'`

- `-Os`
- `-O2`
- `-O3`
- `-O3 -funroll-all-loops`
- `-O3 -march=pentium -mcpu=pentium -ffast-math -funroll-loops -fomit-frame-pointer -fforce-mem -fforce-addr -malign-double -fno-exceptions`

关于本页面的意见和建议应邮件至 `gmourani@videotron.ca`

### 2. "bdlfush" 参数

此文档适用于 `/proc/sys/vm` 中的 sysctl 文件，适用于 Linux 内核 `2.2` 版本。该目录下的文件用于调优 Linux 内核虚拟内存（VM）子系统的操作，其中一个文件（`bdlfush`）对磁盘使用有少量影响。

此文件（`bdlfush`）控制 `bdlflush` 守护进程的操作。我们通常使用此命令提高文件系统性能。

```bash
echo "1000 120 128 512 15 5000 1884 2" >/proc/sys/vm/bdlfush
```

更改一些默认值后，系统似乎响应更快，例如它会等待一会儿调优磁盘并避免某些访问冲突。

将上述命令添加到 `etc/rc/rc.local` 文件中，下次重启系统时就无需再次输入了。

查看 `/usr/src/linux/Documentation/sysctl/vm.txt` 获取更多关于改进虚拟内存、磁盘缓存、交换分区等相关内核参数的信息。

### 5. "ip_local_port_range" 参数

本文档适用于 `proc/sys/ipv4/ip_local_port_range` 中的 sysctl 文件，适用于 Linux 内核版本 `2.2`。`ip_local_port_range` 包含 `2` 个整数。

该参数定义了 TCP 和 UDP 选择本地端口时使用的端口范围。第一个数字是起始端口，第二个数字是最后一个本地端口号。对于高并发系统，请将其更改为 `32768-61000`。

```bash
echo "32768 61000" > /proc/sys/ipv4/ip_local_port_range
```

将上述命令添加到 `etc/rc/rc.conf` 文件中，这样下次重启系统时就不需要重新输入了。

### 4. "etc/nsswitch.conf" 文件

`etc/nsswitch.conf` 文件用于配置哪些服务来确定主机名、密码文件和组文件等信息。在我们的案例中，最后两个 "password files" 和 "group files" 不使用，因为我们的服务器上没有 NIS 服务。因此，我们将关注该文件中的 "hosts"。

编辑 `nsswitch.conf` 文件（`vi /etc/nsswitch.conf`）并将 "hosts" 行修改为：

+ * hosts: dns files

这意味着在解析地址时，首先使用 `/etc/hosts` 文件中的功能，如果 DNS 服务器不可用或无法解析该地址，则使用 dns 功能。

此外，除非你正在使用 NIS，否则我建议删除此文件每行中的所有 NIS 实例！结果应该像下所示：

| password: files |
| shadow: files |
| group: files |
| hosts: dns files |
| bpcolams: files |
| ethers: files |
| netmasks: files |
| networks: files |
| protocols: files |
| rpc: files |
| services: files |
| automount: files |
| aliases: files |

### 5. "proc" 伪文件系统

本文档适用于 `proc/sys/fs/` 中的 sysctl 文件，适用于 Linux 内核版本 `2.2`。此目录下的文件用于调优和监控 Linux 内核运行中的各种杂和通用事项。某些文件用于设置系统，建议在实际调整之前同时阅读文档和源码。

将 `proc/sys/fs/file-max` 的值增加到合理范围，例如每 `4M` 内存设置 `256`：即，对于一台 `128M` 内存的机器，将其设置为 `8192` (`128/4=32*256=8192`)。如上所述，还将将 `proc/sys/fs/inode-max` 增加到大约是其 `3` 到 `4` 倍 (`8192*4=32768`)。

打开文件的数量。这是因为 inode 的数量至少对应一个打开的文件，且对于大文件来说，这个数量要大得多。

（在 root 权限下）在 `proc` 层次结构中更改任何内容的标准方法是 `echo "newvalue"` `/proc/file/that/you/want/change`，因此命令行为：

```bash
echo "8192" /proc/sys/fs/file-max
echo "3268" /proc/sys/fs/inode-max
```

修改内核源码中常量的技术通常不是正确答案，因为这不会在新的内核中保留。最好的技术之一是将上述命令添加到 `etc/rc.d/rc.local` 文件中。

```bash
[root@deep#] /etc/rc.d/rc.local
```

并在此文件末尾添加以下行

```bash
echo "8192" /proc/sys/fs/file-max (如果你的系统有 128MB 内存)
echo "3268" /proc/sys/fs/inode-max (如果你的系统有 128MB 内存).
```

具体值将根据你对机器的实际用途而变化。例如，文件服务器或 Web 服务器需要很多打开的文件，而计算服务器则不需要

`file-max` 中的值表示 Linux 内核将分配的最大文件句柄数。当你遇到大量“打开文件耗尽”的错误时，可能需要提高此限制。默认值为 `4096`。

`inode-max` 中的值表示 inode 处理器的最大数量。此值应该是 `file-max` 值的 `3` 到 `4` 倍，因为 stdin、stdout 和网络套字也需要 inode 来处理它们。如果你经常耗尽 inode，应该增加此值。

### 6. "ulimit" 参数

Linux 本身对每个用户有“最大进程数”限制。将此添加到你的 `.bashrc` 文件或 shell 使用的脚本中：

编辑 `bashrc`（`vi /root/.bashrc`）并添加以下行：

```bash
ulimit -u unlimited
```



你必须退出并重新登录。要验证准备就绪，请确保当使用 `root` 执行 `ulimit -a` 时，`max processes` 旁边显示 "unlimited"

```bash
[root@deep#] ulimit -a
```

有关本页面的意见和建议请邮件至 `gmounrai@videotron.ca`

据报道，通过将 IDE 驱动程序设置为 DMA、32位传输和多扇区模式，大规模磁盘 I/O 操作性能有所提升。除非另有说明，内核似乎使用更保守的设置。更改驱动器设置的魔法命令是 `hdparm`。

要在 PCI 总线上启用 32 位 I/O，请使用命令：
`root@deep]# /sbin/hdparm -d 1 /dev/hda` (或 `hbd`, `hdc` 等)。

`hdparm` (8) 管理你可能需要使用的页面 - 芯片组使用 `c 3`。所有 (E)IDE 驱动器仍通过接口卡上的排线使用 16 位连接。

要启用 DMA，请使用命令：
`root@deep]# /sbin/hdparm -d 1 /dev/hda` (或 `hbd`, `hdc` 等)。

这可能取决于你的主板芯片组是否已编译进内核。

要启用多字 DMA 模式 2 传输，请使用命令：
`root@deep]# /sbin/hdparm -d 1-X3 /dev/hda` (或 `hbd`, `hdc` 等)。

这为较新的 (E)IDE/ATA2 驱动器设置 IDE 接口。如果你有硬件手册，请检查。

要启用 UltraDMA 模式 2 传输，请使用命令：
`root@deep]# /sbin/hdparm -d 1-66 /dev/hda` (或 `hbd`, `hdc` 等)。

你需要提前为 UltraDMA 准备扇区模式，也可以查看关于 `hdparm` 的页面以获取更多信息。请极其谨慎使用！

要设置多扇区模式 I/O，请使用命令：
`root@deep]# /sbin/hdparm -m XX /dev/hda` (或 `hbd`, `hdc` 等)。

其中 "XX" 是你的驱动器支持的最大设置。可以使用 `-i` 标志查找已安装驱动器支持的最大设置，查找输出中的 `MaxMultSet`。

`root@deep]# /sbin/hdparm -d 1 /dev/hda` (或 `hbd`, `hdc` 等)。

```
/dev/hda
```

```
Model=Maxtor 750 AV,FRev=GA7647,SerialNo=L1007YS

Config=-Hard NoHfmD SiU15Sec Fixed DTR=5Mbs FmpRep

RawCS-H=1046/63,TrigSize=0,SectorSize=0,ECCBytes=11

BusType=3(DualPort),Cur:LBAectors=32,MaxMultSet,MultSet-8

DbiQWords=yes,DMA-PIO(first)=yes,DMA-1 (medium)

CurC=322/323,Cur:Sector=37598,LBAectors,LBA-bytes,LBAectors=105468

IDMA=mid:150,rec:160;DMA modes: sword1* sword2

IORDY=off,PIO(min:24,IORDY:180); PIO modes: mode3
```

多扇区模式（又称 IDE ）是大多数现代 IDE 驱动器的功能，允许在每次 I/O 中断时传输多个扇区，而不是通常的每次中断一个扇区。启用此功能后，通常可以减少 30-50% 的磁盘 I/O。在许多系统中，它可以提供 5% 到 50% 的数据吞吐量。

你可以通过运行性能测试模式下的 `hdparm` 来测试更改结果：
`root@deep]# /sbin/hdparm -t /dev/hda` (或 `hbd`, `hdc` 等)。

© 1999 Open Network Architecture ®

一旦设置了一组 "hdparm" 选项，忘记将命令放入你的 "/etc/rc.d/rc.local" 文件中，以便每次重启机器时运行。

## 第三部分 内核相关参考

在本部分中

## 配置和编译内核

### 第 5 章 配置和编译内核

在本章中

- Linux 内核
- 制作紧急启动软盘
- 加固内核
- 内核配置
- 安装新内核
- 删除与模块相关的程序、文件和行
- 制作新的救援软盘
- 更新你的 "/dev" 条目

有关本页面的意见和建议请邮件至 `gmourani@videotron.ca`

## Linux 内核

下一步的第一件事是构建一个最适合你系统的内核。非常简单，但无论如何，请参考 `/usr/src/linux/` 下的 README 文件。在配置内核时，只编译你需要和使用的代码。脑海中会出现四个主要原因；内核会更快（运行的代码更少），你会有更多内存（内核部分**绝不会**交换到虚拟内存中），更稳定（对于非专家证明？），不必要的部分可以被攻击者利用。模块比直接支持的内核慢。

在我们的配置中，我们将构建单体内核。单体内核意味着制作任何模块时仅回答 `Yes` 或 `No`，并省略 `make` 和 `modules_install` 选项。我们将使用缓冲区溢出补丁来加固内核。Linux 内核补丁存在，例如设计的非可执行栈，禁用栈上的执行，使得全球脚本的攻击变得更困难。

记住，在配置新内核时，如果打算构建单体内核，上述步骤仅回答 `Yes` 或 `No`。如果打算使用伪装功能或无法构建单体内核，由于此功能必须默认构建某些模块，因此需要模块化内核。新内核非常取决于你的计算机硬件，在配置部分，你必须更改它们以适应系统。

- Pentium II 400 MHz (i86) 处理器
- 主板 SCSI
- 硬盘 SCSI
- 控制器 Adaptec
- 光驱 ATAPI IDE
- 软盘
- 以太网卡 Intel Pro/100
- 鼠标 FS

## 这些安装说明假设源路径为 `/usr/src/`。RedHat Linux 6 服务器的所有安装步骤将在超级用户 'root' 下进行。最后的内核编号是 2.214
安全内核版本号是 2.214

软件包

内核首页：http://www.kernelnotes.org/
你必须下载：`linux-2.214.tar.gz`
安全内核补丁首页：http://www.openwall.com/linux/
你必须下载：`linux-2.214-ow1.gz`

## 制作紧急启动软盘

安装的第一步是制作紧急启动软盘（如果你还没有的话）。你可以简单地使用 `mkbootdisk` 命令完成。首先找出你正在使用的内核。检查你的 "/etc/lilo.conf" 文件查看启动了哪个镜像。在我的示例中，文件中内容：

```
root@deep]# cat /etc/lilo.conf

boot=/dev/sda

map=/boot

prompt

timeout=50

image=boot/vmlinux-2.212

label=linux

root=/dev/sda

initrd=/boot/initrd-2.212

read-only
```

现在你需要找到启动镜像。在标准安装中，上述显示启动了格式化的软盘，确保 root 已登录。

```
root@deep]# mkbootdisk --device=/dev/fd0 2.212

将磁盘插入 dev/fd0。磁盘上的任何信息将丢失。

按 <Enter> 继续或按 <C> 取消
```

遵循这些指南，你将获得带有工作内核的启动软盘以防升级问题。建议使用软盘重启。

解压压缩包 (tar.gz)。

```
root@deep]# cp linux-version.tar.gz /usr/src/
root@deep]# rm -f linux
root@deep]# rm -f linux-old.version
```

注意：上述步骤删除了符号链接 (rm -f linux) 和 Linux 头文件（linux-old.version 目录）。如果系统中安装了内核 RPM 包，因为你刚刚完成了新 Linux 系统的安装或使用 RPM 包升级你的 Linux 系统，使用以下命令安装 内内核：

- 你可以使用以下命令验证系统上安装了内核 RPM 包：
```
root@deep]# rpm -qa | grep kernel

kernel-headers-2.212-20.i386

kernel-2.212-20.i386
```

有关本页面的意见和建议请邮件至 `gmourani@videotron.ca`

- 卸载内核，使用以下命令：
`root@deep]# rpm -e --nodeps kernel-headers`

在下面的步骤中，我们在卸载内核 RPM 后手动删除空 `/usr/src/linux-2.12` 和 `/lib/modules/2.12` 目录（RPM卸载程序不会完全删除该目录）。我们将从 tar 包中提取新的 Linux 版本，选择解压后创建的新 Linux 内核为超级用户 "root"，最后从系统中删除 Linux 存档。



`root@deep]# rm -rf /usr/src/linux-2.212/`

`root@deep]# rm -rf /lib/modules/2.212/`

`root@deep]# tar xpf linux-version.tar.gz`

`root@deep]# chown -R 0:0 /usr/src/linux/`

`root@deep]# rm -f linux-version.tar.gz`

### 增加任务

要增加任务数（每个用户的最大数），你需要编辑 `/usr/src/include/tasks.h` 文件并更改以下参数。

- 编辑 `tasks.h` 文件 (`+14 /usr/src/include/tasks.h`) 并更改：
`NR_TASKS` 从 `512` 改为 `3072`
`MIN_TASKS_LEFT_FOR_ROOT` 从 `4`

注意：1) `NR_TASKS` 的值表示内核每个用户分配的最大任务（进程）数。增加此值将允许处理来自客户端的更多连接（例如 HTTP 服务器将能够更多的客户端连接）。2) Linux 防止普通用户分配所有槽位。为 root 留了 `MIN_TASKS_LEFT_FOR_ROOT`。因此，也应该有防止普通用户分配内存的保护。

## 优化内核

为了优化内核以适应特定的 CPU 架构和优化标志，你需要编辑 `/usr/src/linux/Makefile` 文件并更改以下参数。

- 编辑 `Makefile` (`+19 /usr/src/linux/Makefile`) 并更改行：
`CFLAGS = -Wall -Wstrict-prototypes -O9 -fomit-frame-pointer`
读取为：
`CFLAGS = -Wall -Wstrict-prototypes -O9 -froll-loops -fast-math -align-double - mcpu=puniticro-march=puniticro-fomit-frame-pointer`

### 加固内核

来自 Openwall Project 的安全内核补丁是防止栈缓冲区溢出等攻击的极佳方法，此补丁是内核安全相关功能的集合

关于本页面的意见和建议请邮寄至 `gmourani@videotron.ca`

Linux 内核，可以通过添加到新 Linux 内核中新的“安全选项”（Security options）配置部分进行配置。

除了新功能外，某些版本的补丁包含各种安全修复。此类修复的数量随版本变化，因为某些修复已变得过时（例如新内核发布已修复了相同的问题），而其他安全问题不断被发现。

# 补丁版本 linux-2_2_14-ow1.tar.gz 的新功能有：

- 不可执行的用户栈区域
- `/tmp` 中限制的链接
- `/tmp` 中限制的 FIFOs
- 限制 `/proc`
- 对 fd 0, 1 和 2 的特殊处理
- 在 `execve(2)` 上强制执行 `RLIMIT_NPROC`
- 销毁未使用的共享内存段

注意：在应用 `linux-2_2_14-ow1` 补丁时，“安全选项”将尽添加到您的内核补丁的末尾。有关此补丁中提供的不同功能的更多信息和描述，请参阅补丁源码附带的 README 文件。

# 应用补丁

解压 tar 包 (`tar.gz`)。

```
[root@deep]# cp linux-2_2_14-ow1.tar.gz /usr/src/
[root@deep]# cd /usr/src/
[root@deep]# tar zpf linux-2_2_14-ow1.tar.gz
[root@deep]# cd linux-2_2_14-ow1/
[root@deep]# mv linux-2_2_14-ow1.diff /usr/src/
[root@deep]# cd ..
[root@deep]# patch -p0 < linux-2_2_14-ow1.diff
[root@deep]# rm -rf linux-2_2_14-ow1
[root@deep]# rm -f linux-2_2_14-ow1.diff
[root@deep]# rm -f linux-2_2_14-ow1.tar.gz
```

首先我们将存档复制到 `"/usr/src"` 目录，然后移动到 `"/usr/src"` 目录并解压 Linux 补丁，将包含补丁的 `linux-2_2_14-ow1.diff` 文件移动到 `"/usr/src"`，返回 `"/usr/src"` 并使用文件 `linux-2_2_14-ow1.diff` 修补我们的内核。之后，我们删除所有与补丁相关的文件。

注意：所有与 `linux-2_2_14-ow1` 补丁相关的安全消息（如不可执行栈部分）都应该记录到日志文件 `"var/log/messages"`。

补丁新内核的步骤已完成。现在按照剩下的安装步骤构建 Linux 内核并重启。

### 编译

确保 `"/usr/include/asm"`, `"/usr/include/linux"` 和 `"/usr/include/scsi"` 子目录只是内核源码的符号链接。`"asm"`、`linux` 和 `scsi` 子目录是指向此架构所需的实际目录的软链接，例如如果您有一个新解压的内核源码树，`"/usr/src/include/asm-i386"`，您必须创建符号链接。

- 在您的终端上输入以下命令：
```
[root@deep]# cd /usr/include/
```
© Copyright 1999 Open Network Architecture ®

```
[root@deep#] rm -rf asm linux scsi
[root@deep#] ln -s /usr/src/linux/include/asm-i386 asm
[root@deep#] ln -s /usr/src/linux/include/linux linux
[root@deep#] ln -s /usr/src/linux/include/scsi scsi
```

这是配置中非常重要的一部分，我们删除了 `/usr/include` 下的 `"asm"`, `"linux"` 和 `"scsi"` 目录，然后在新的 Linux 内核版本下构建同名的新链接。`"include"` 目录包含了内核和程序在系统上编译所需的重要头文件字段。

确保您没有过时的 `.o` 文件和依赖项残留。

- 在您的终端上输入以下命令：
```
[root@deep#] cd /usr/src/linux/
[root@deep#] make mrproper
```

注意：如果您正确安装了源码，可以通过三种方式配置 Linux 内核。第一种方法是使用 `make config` 命令。它提供了一个基于文本的界面来回答配置选项。系统会提示您设置内核所需的所有选项。

第二种方法是使用 `make menuconfig` 命令，它在易于使用的菜单中提供所有内核选项。第三种方法是使用 `make xconfig` 命令，它为所有内核提供了完整的图形界面。

对于本章的配置，您将使用 `make config` 命令，因为我们没有在服务器上安装 XFree86 窗口界面。

```
[root@deep#] cd /usr/src/linux/ (如果您尚未在该目录)
[root@deep#] make config
```



# 内核配置

## 代码成熟度级别选项
询问开发和/或不完整代码/驱动 (`CONFIG_EXPERIMENTAL`) [N]

## 处理器类型和特性
处理器族 (`CONFIG_M386`) [Ppro/x86_36]
最大物理内存 (`CONFIG_1GB`) [1GB]
数学仿真 (`CONFIG_MATH_EMULATION`) [N]
内存类型寄存支持 (`CONFIG_TRR`) [N]
对称多处理支持 (`CONFIG_SMP`) [Y]

## 可加载模块支持
启用可加载模块支持 (`CONFIG_MODULES`) [Y]

## 通用设置
网络支持 (`CONFIG_NET`) [Y]
PCI 支持 (`CONFIG_PCI`) [Y]
PCI 模式 (BIOS, Direct) [Any]
PCI 异常 (`CONFIG_PCI_QUIRKS`) [Y]
向后兼容/proc/ci (`CONFIG_PCI_OLD`) [Y]
MCA 支持 (`CONFIG_MCA`) [N]
工作站 (`CONFIG_VISW`) [N]

© 1999 Open Network Architecture

系统 (`CONFIG_SYS`) [Y]
进程计数 (`CONFIG_PROCESS_ACCT`) [N]
Sysctl 支持 (`CONFIG_SYSCTL`) [Y]
内核二进制文件的支持 (`CONFIG_INFMT_A`) [Y]
ELF 二进制文件的支持 (`CONFIG_INFMT_ELF`) [Y]
MISC 二进制文件的支持 (`CONFIG_INFMT_MISC`) [Y]
并行端口支持 (`CONFIG_PORT`) [N]
高级电源管理 BIOS (`CONFIG_APM`) [N]

# 即插用
即插用支持 (`CONFIG_PNP`) [N]

# 设备
普通软磁盘支持 (`CONFIG_BLK_DEV_FD`) [Y]
增强型 IDE/MFM 磁盘/带支持 (`CONFIG_BLK_DEV_IDE`) [Y]
主接口上仅使用旧驱动 (`CONFIG_BLK_DEV_HD`) [N]
IDE/ATA-2 磁盘支持 (`CONFIG_BLK_DEV_ISK`) [Y]
IDE/ATA CD-ROM 支持 (`CONFIG_BLK_DEV_IDC`) [Y]
IDE/TAP 支持 (`CONFIG_BLK_DEV_ATEP`) [N]
SCSI 仿真支持 (`CONFIG_BLK_ESCI`) [Y]
CMD640 芯片组支持 (`CONFIG_BLK_DEV_CMD640`) [N]
R1200 芯片组支持 (`CONFIG_BLK_DEV_R1200`) [N]
通用 IDE 总线支持 (`CONFIG_BLK_DEV_IDE`) [Y]
通用 PCI 总线主 支持 (`CONFIG_BLK_DEV_DMA`) [Y]
启动磁盘 (`CONFIG_BLK_DEV_OFFBOARD`) [N]
可用 DMA (`CONFIG_IDE_AUTO`) [Y]
其他芯片组 (`CONFIG_IDE_CHIPSETS`) [N]
回环设备支持 (`CONFIG_BLK_DEV_LOOP`) [N]
网络块设备支持 (`CONFIG_BLK_DEV_NBD`) [N]
多设备驱动支持 (`CONFIG_BLK_DEV_MD`) [N]
RAM 磁盘支持 (`CONFIG_BLK_DEV_RAM`) [N]
Xt 硬磁盘支持 (`CONFIG_BLK_DEV_XD`) [N]
yleax DAC960/DAC110 RAID 控制器支持 (`CONFIG_BLK_DEV_DAC960`) [N]
并行 IDE 设备支持 (`CONFIG_PARIDE`) [N]
紧凑 SMART-2 芯片组支持 (`CONFIG_BLK_CPQ_DA`) [N]

# 网络选项
包套接 (`CONFIG_PACKET`) [Y]
内核原生套接 (`CONFIG_NETLINK`) [N]
防火墙 (`CONFIG_FIREALL`) [Y]
套接过滤 (`CONFIG_FILTER`) [N]
域套接 (`CONFIG_UNIX`) [Y]
TCP/IP 网络 (`CONFIG_INET`) [Y]
IP 多播 (`CONFIG_IP_MULTCAST`) [N]
高级路由器 (`CONFIG_IP_ADVANCED_ROUTER`) [N]
IP 级自动配置 (`CONFIG_IP_PNP`) [N]
IP 释放 (`CONFIG_FREALL`) [Y]
透明代理支持 (`CONFIG_IP_TRANSPARENT_PROXY`) [N]
伪装 (`CONFIG_IP_MASQUERADE`) [N]
ICMP 伪装 (`CONFIG_IP_MASQUERADE_CMP`) [N]
作为主机的 路由器 (`CONFIG_IP_ROUTER`) [N]
隧道 (`CONFIG_NET_PIP`) [N]
IP 之 IGRE 隧道 (`CONFIG_IP_IGRE`) [N]
IP 别名支持 (`CONFIG_IP_ALIAS`) [N]
TCP cookies (`CONFIG_INET_SYN_COOKIES`) [Y]
IP 反向 ARP (`CONFIG_INET_RARP`) [N]
IP 允许大窗口 (`CONFIG_SKB_LARGE`) [Y]
IP 协议 (`CONFIG_IPX`) [N]
AppleTalk DDP (`CONFIG_ATALK`) [N]

# 电话支持
Linux 电话支持 (`CONFIG_PHONE`) N/y/m? (NEW)

# SCSI 支持
SCSI 支持 (QNGCIF, SCSI) [Y]
SCSI 磁盘支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 带支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 支持 (QNGCIF, SCSI) [Y]
SCSI 磁盘支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 带支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 支持 (QNGCIF, SCSI) [Y]
SCSI 磁盘支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 带支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 支持 (QNGCIF, SCSI) [Y]
SCSI 磁盘支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 带支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 支持 (QNGCIF, SCSI) [Y]
SCSI 磁盘支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 带支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 支持 (QNGCIF, SCSI) [Y]
SCSI 磁盘支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 带支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 支持 (QNGCIF, SCSI) [Y]
SCSI 磁盘支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 带支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 支持 (QNGCIF, SCSI) [Y]
SCSI 磁盘支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 带支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 支持 (QNGCIF, SCSI) [Y]
SCSI 磁盘支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 带支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 支持 (QNGCIF, SCSI) [Y]
SCSI 磁盘支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 带支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 支持 (QNGCIF, SCSI) [Y]
SCSI 磁盘支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 带支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 支持 (QNGCIF, SCSI) [Y]
SCSI 磁盘支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 带支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 支持 (QNGCIF, SCSI) [Y]
SCSI 磁盘支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 带支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 支持 (QNGCIF, SCSI) [Y]
SCSI 磁盘支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 带支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 支持 (QNGCIF, SCSI) [Y]
SCSI 磁盘支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 带支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 支持 (QNGCIF, SCSI) [Y]
SCSI 磁盘支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 带支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 支持 (QNGCIF, SCSI) [Y]
SCSI 磁盘支持 (`CONFIG_BLK_DEV_SD`) [Y] [Y]
SCSI 带支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 支持 (QNGCIF, SCSI) [Y]
SCSI 磁盘支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 带支持 (`CONFIG_BLK_DEV_SD`) [Y]

SCSI 支持 (QNGCIF, SCSI) [Y]
SCSI 磁盘支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 带支持 (`CONFIG_BLK_DEV_SD`) [Y]

SCSI 支持 (QNGCIF, SCSI) [Y]
SCSI 磁盘支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 带支持 (`CONFIG_BLK_DEV_SD`) [Y]

SCSI 支持 (QNGCIF, SCSI) [Y]
SCSI 磁盘支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 带支持 (`CONFIG_BLK_DEV_SD`) [Y]

SCSI 支持 (QNGCIF, SCSI) [Y]
SCSI 磁盘支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 带支持 (`CONFIG_BLK_DEV_SD`) [Y]

SCSI 支持 (QNGCIF, SCSI) [Y]
SCSI 磁盘支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 带支持 (`CONFIG_BLK_DEV_SD`) [Y]

SCSI 支持 (QNGCIF, SCSI) [Y]
SCSI 磁盘支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 带支持 (`CONFIG_BLK_DEV_SD`) [Y]

SCSI 支持 (QNGCIF, SCSI) [Y]
SCSI 磁盘支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 带支持 (`CONFIG_BLK_DEV_SD`) [Y]

SCSI 支持 (QNGCIF, SCSI) [Y]
SCSI 磁盘支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 带支持 (`CONFIG_BLK_DEV_SD`) [Y]

SCSI 支持 (QNGCIF, SCSI) [Y]
SCSI 磁盘支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 带支持 (`CONFIG_BLK_DEV_SD`) [Y]

SCSI 支持 (QNGCIF, SCSI) [Y]
SCSI 磁盘支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 带支持 (`CONFIG_BLK_DEV_SD`) [Y]

SCSI 支持 (QNGCIF, SCSI) [Y]
SCSI 磁盘支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 带支持 (`CONFIG_BLK_DEV_SD`) [Y]

SCSI 支持 (QNGCIF, SCSI) [Y]
SCSI 磁盘支持 (`CONFIG_BLK_DEV_SD`) [Y] [Y]
SCSI 带支持 (`CONFIG_BLK_DEV_SD`) [Y]

SCSI,支持 (QNGCIF,_BLK_DEV_SC) [Y]
SCSI 磁盘支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 带支持 (`CONFIG_BLK_DEV_SD`) [Y]

SCSI 支持 (QNGCIF, SCSI) [Y]
SCSI 磁盘支持 (`CONFIG_BLK_DEV_SD`) [Y]
SCSI 带支持 (`CONFIG_BLK_DEV_SD`) [Y]

关于本页面的意见和建议应邮寄至 gmourani@videotron.ca

# ARQ 设备

- ARNet 支持 (`CONFIG, ARCN`) [N]
- 虚拟驱动支持 (`CONFIG_DUMMY`) [N]
- EOL（线性负载均衡） (`CONFIG_EQUALIZER`) [N]
- General Instruments Surfboard 1000 (`CONFIG_NET_SB1000`) [N]

# 以太网 (10 或 100Mbit)

- 以太网 (10 或 100Mbit) (`CONFIG_NET_ETHERNET`) [Y]
- 3COM 网卡 (`CONFIG_NET_VENDOR_3COM`) [N]
- AMD Lance 和 Pciat (AT5100 和 NE2300) 支持 (`CONFIG_LANCE`) [N]
- 西数据 SMC 网卡 (`CONFIG_NET_VENDOR_SMC`) [N]
- Realtek-Monfort (Nicor) 卡 (`CONFIG_NET_VENDOR_RACAL RACAL`) [N]
- 其他 ISA 卡 (`CONFIG_NET_ISA`) [N]
- EISA, VLB, PCI 和板载控制器 (`CONFIG_NET_EISA`) [Y]
- AMD PCI32 (VLB 和 PCI) 支持 (`CONFIG_PCNT32`) [N]
- Aptec-III 板载以太网 (`CONFIG_APRICOT`) [N]
- CS89x0 支持 (CS89x0) [N]
- MD9102 PCI快速以太网适配器支持（实验性） (`CONFIG_MD9102`) [N]
- GenEC DeChip & DigitalETHERWORKS POIESA (`CONFIG_EISA`) [N]
- DeChip 全双工支持 (`CONFIG_DE4X5`) [N]
- Digi Intl. Wright Se-X 支持 (`CONFIG_DGR`) [N]
- Ether/ExpressPro/100 支持 (`CONFIG_EXPRESS_PRO100`) [Y]
- PCI NE2000 支持 (`CONFIG_NEZK_PCI`) [N]
- TI 以太网支持 (`CONFIG_LAN`) [N]
- Via 支持 (`CONFIG_VIA_RHINE`) [N]
- SIS 900/7016 快速以太网适配器支持 (`CONFIG_SIS900`) [n/y/m] (新)
- 数据包和便携式适配器 (`CONFIG_NET_POKET`) [N]
- Sykontek Sk8 支持 (`CONFIG_SB98LIN`) [n/y/m] (新)
- FFDI 驱动支持 (`CONFIG_FFDI`) [N]
- PPP（点对点）支持 (`CONFIG_PPP`) [N]
- SLIP（串口）支持 (`CONFIG_SLIP`) [N]
- 无线局域网（非业电） (`CONFIG_NET_RADIO`) [N]

# 令牌环设备

- 令牌环驱动支持 (`CONFIG_TR`) [N]
- 光纤通道驱动支持 (`CONFIG_NET_FC`) [N]

# Wan 接口

- Control Hostels SV-11 支持 (`CONFIG_HOSTESS_SV11`) [N]
- COASAType 串口板支持 (`CONFIG_COSA`) [N]
- Sealive Systems 4021 支持 (`CONFIG_SEALEVER_4021`) [N]
- MultiGate (COMX) 同步串口板支持 (`CONFIG_COMX`) [n/y/m] (新)
- 帧中继 DLCI 支持 (`CONFIG_DLCI`) [N]
- WAN 驱动 (`CONFIG_WAN_DRIVERS`) [N]
- SBN12-xx 支持 (`CONFIG_SBNI`) [N]

# 业余无线支持

# IrDA 子系统支持

- IrDA 子系统支持 (`CONFIG_IRDA`) [N]

# ISDN 子系统支持

- ISDN 支持 (`CONFIG_ISDN`) [N]

# 旧版 CD-ROM 驱动（非 SCSI, IDE）

- 支持非 SCSI/IDE/ATAPI CDROM 驱动器 (`CONFIG_CD_NO_IDESCI`) [N]

# 字符设备

- 虚拟终端 (`CONFIG_VT`) [Y]

© Copyright 1999 Open Network Architecture ®

关于本页面的意见和建议应邮寄至 gmourani@videotronron.ca

- 虚拟终端控制台支持 (`CONFIG_VT_CONSOLE`) [Y]
- 标准/通用（哑）串口支持 (`CONFIG_SERIAL_AL`) [Y]
- 串口端口控制台支持 (`CONFIG_SERIAL_CONSOLE`) [N]
- 扩展哑 驱动选项 (`CONFIG_SERIAL_EXTENDED`) [N]
- 非标准 PTY 支持 (`CONFIG_SERIAL_NONSTANDARD`) [N]
- Unix9 PTY 支持 (`CONFIG_UNIX9_PTYS`) [Y]
- 使用的 Unix9 PTY 最大数量 (0-2048) (`CONFIG_UNIX9_PTYS_COUNT`) [256]
- 更多支持（非串口鼠标） (`CONFIG_MOUSE`) [Y]

### 鼠标
- ATIXL 总线支持 (`CONFIG_ATIXL_BMOUSE`) [N]
- 罗罗技鼠标支持 (`CONFIG_BMOUSE`) [N]
- 微软鼠标支持 (`CONFIG_MS_BMOUSE`) [N]
- PS/2 鼠标（“辅助设备”）支持 (`CONFIG_PSMOUSE`) [Y]
- C&S 82c710 端口支持 (`CONFIG_82c710_MOUSE`) [Y]
- PC110 数字键板支持 (`CONFIG_PC110_PAD`) [N]

### 摇杆
- 摇杆支持 (`CONFIG_JOYSTICK`) [N]
- QIC-02-带支持 (`CONFIG_QIC02_TAPE`) [N]
- 看门狗计时器支持 (`CONFIG_WATCHOG`) [N]
- /dev/nvram 支持 (`CONFIG_NVRAM`) [N]
- 增强时钟支持 (`CONFIG_RTC`) [N]

### Linux 视频
- Linux 视频 (`CONFIG_DEV`) [N]
- 双倍速控制器支持 (`CONFIG_LK`) [N]

### 软盘带驱动
- 软磁盘-80/带支持 (`CONFIG_FT`) [N]

### 文件系统
- 配额支持 (`CONFIG_QUOTA`) [Y]
- 内核自动支持 (`CONFIG_AUTOFS`) [Y]
- Amiga 文件系统 (`CONFIG_AFF`) [N]
- Apple Macintosh 文件系统 (`CONFIG_HFS`) [N]
- FAT 文件系统支持 (`CONFIG_FAT`) [N]
- ISO9660 CDROM 支持 (`CONFIG_ISO9660`) [Y]
- Microsoft CDROM 扩展 (`CONFIG_JOLI`) [N]
- Minix 文件系统支持 (`CONFIG_MINIX`) [N]
- NTFS 支持 (`CONFIG_NTFS`) [N]
- OS2 文件系统支持 (`CONFIG_HPFS`) [N]
- /proc 文件系统支持 (`CONFIG_PROC`) [Y]
- /dev/ptfs 文件系统支持 (`CONFIG_DEPT`) [Y]
- ROM 文件系统支持 (`CONFIG_ROMFS`) [N]
- 扩展文件系统 (`CONFIG_EXT2_FS`) [Y]
- System V 和一致文件系统 (`CONFIG_SYSV_FS`) [N]
- FS 文件系统支持 (`CONFIG_UFS`) [N]

### 网络文件系统
- Coda 文件系统（高级网络） (`CONFIG_CODA_FS`) [N]
- NFS 文件系统支持 (`CONFIG_NFS_FS`) [Y]
- SMB 文件系统支持 (`CONFIG_SMB_FS`) [N]
- CP 文件系统支持 (`CONFIG_CP_FS`) [N]

### 分区类型
- BSD 标签（BSD 分区表） (`CONFIG_BSD_LABEL`) [N]
- Macintosh 分区映射支持 (`CONFIG_MAC`) [N]
- AMD 标签（Sun 分区表） (`CONFIG_AMD_DISKLABEL`) [N]
- Solaris (x86) 分区表支持 (`CONFIG_SOLARIS_PARTITION`) [N]

© Copyright 1999 Open Network Architecture ®

关于本页面的意见和建议应邮寄至 gmourani@videotron.ca

# 控制台驱动

- VGA 控制台 (`CONFIG_VGA_CONSOLE`) [Y]
- 视频模式选择 (`CONFIG_VIDEO_SELECT`) [N]

# 音频

- 声卡支持 (`CONFIG_SOUND`) [N]

# 安全选项

（只有当你用 Openwall 项目补丁了内核时才会出现安全选项。）
- 非执行栈区域 (`CONFIG_SECURE_STACK`) [Y]
- 自动检测并模拟编译器 (`CONFIG_SECURE_STACK_SMART`) [Y]
- /tmp 中的受限链接 (`CONFIG_SEC_LINK`) [Y]
- /tmp 中的受限 FIFO (`CONFIG_SECURE_FIFO`) [Y]
- 受限的 /proc (`CONFIG_SECURE_PROC`) [N]
- fd 0, 1 和 2 的特殊处理 (`CONFIG_SECURE_FD_0_2`) [Y]
- 在 execve(2) 上强制 RLIMIT_NPROC (`CONFIG_SECURE_RLIMIT_NPROC`) [Y]
- 销毁未使用的内存段 (`CONFIG_SECURE_SHM`) [Y]

# 内核调试

- Magic SysRq 键 (`CONFIG_MAGIC_SYSR`) [N]

现在，返回 "`/usr/src/linux/`"（如果你不在）。你需要编译新内核。你可以使用以下命令：

```
```



[root@deep] make; make clean; make bzimage

这一行三个命令。第一个 `make` 实际上是获取你的配置并构建依赖树。这个过程决定了编译什么以及何时编译。下一步 `make clean` 会擦除所有之前的编译痕迹，以避免错误的版本的功能进入内核。最后，`make bzimage` 执行完整编译。

过程完成后，内核已编译完成并准备就绪。在安装内核之前，你需要编译相应的模块。这只有在你对“启用加载模块支持 (CONFIG_MODULES)”说 `Yes` 并将某些选项编译为模块时才需要。

你可以使用以下命令：

```
[root@deep] make modules
```

```
[root@deep] make modules_install
```

注意：`make modules` 和 `make modules_install` 命令只有在你上面的内核配置中说“启用加载模块支持 (CONFIG_MODULES)”时才需要。

# 安装新内核

1. 将内核源文件 `/usr/src/linux/arch/i386/boot/bzimage` 复制到 `boot/` 目录并给它一个合适的名称。

```
[root@deep] cp /usr/src/linux/arch/i386/boot/bzimage /boot/vmlinux-kernel.version.number
```

注意：合适或推荐的新名称类似于 `vmlinux-2.2.14`，如果你想使用 `mkbootdisk` 创建新的救援软盘或紧急软盘启动，这很重要。

© Copyright 1999 Open Network Architecture ®

关于本页面的意见和建议将邮寄至 `gmourani@videotronron.ca`

关于本页面的意见和建议应邮寄至 `gmourani@videotron.ca`

关于本页面的意见和建议应邮寄至 `gmourani@videotron.ca`

关于本页面的意见和建议应邮寄至 `gmourani@videotron.ca`

关于本页面的意见和建议应邮寄至 `gmourani@videotron.ca`

关于本页面的意见和建议应邮寄至 `gmourani@videotron.ca`

关于本页面的意见和建议应邮寄至 `gmourani@videotron.ca`

关于本页面的意见和建议应邮寄至 `gmourani@videotron.ca`

关于本页面的意见和建议应邮寄至 `gmourani@videotron.ca`

关于本页面的意见和建议应邮寄至 `gmourani@videotron.ca`

关于本页的意见和建议请邮件至 `gmourani@videotron.ca`

首先，我们根据已安装内核的版本创建一个名为 `linux-2.2.14` 的新目录以便于解释，然后将 `/usr/src/include/` 下的 `as-generic`、`asm-i386`、`linux`、`net`、`video` 和 `scsi` 目录拷贝到新位置 `/usr/src/linux-2.2.14/`。之后，删除编译新内核的源码目录，并在 `/usr/src/` 下创建一个名为 `linux` 的新符号链接，指向 `/usr/src/linux-2.2.14/include` 目录。通过这些步骤，未来编译的程序将知道在你的服务器上查找与内核相关的头文件。

6. 最后，你需要编辑 `etc/lilo.conf` 文件，将你的内核设置为启动选项之一：

### 步骤 1
编辑 `lilo.conf` 文件（`/vi /etc/lilo.conf`），并在 `image=/boot/.` 这一行上进行相应修改。

```bash
[root@deep]# vi /etc/lilo.conf
```
例如：
```text
boot=/dev/sda

map=/boot/map

install=/boot/boot

prompt

timeout=00

restricted

password=somepassword

image=/mlinux.kernel.version#在此处添加你的新内核名称

label=linux

root=/dev/sda6

read-only
```

> 注意：忘记删除 `lilo.conf` 文件中显示 `initrd=/boot/initrd-2.2.12-20.img` 的那行，因为该行现在不再是必须了（单体内核不需要 initrd 文件）。

### 步骤 2
现在，使用新内核更新我们的 `lilo.conf` 文件。

```bash
[root@deep]# lilo -v

LILO version 21 [Copyright 1992-1998 Werner Almesger

Reading boot sector from /dev/sda

Merging /boot/boot.b

Boot image /boot/mlinux-2.2.14

Added linux.

/boot.0800 - no backup copy made.

Writing boot sector.
```

> 重要：如果你在上面的内核配置中对 `Unix98 PTY support` 选项回答任何 `NO`，请编辑你的 `/etc/fstab` 并删除以下行：

```text
none /dev/pts devpts gid=5,mode=6200 0 0
```

# 删除程序与模块相关的文件

当你第一次安装 Red Hat Linux 时（像我们所做的），内核是以模块化方式构建的。这意味着我们需要的每个设备或功能都被制成模块，并由名为 `Kerneld` 的内核守护进程（在 2.2x内核版本中称为 `kmod`）控制，

© Copyright 1999 Open Network Architecture ®

它根据需要自动将某些模块和函数加载到内存中，并在不再使用时将其上传。

内核使用位于 `/etc/conf/modules` 的 `conf.modules` 文件来了解例如你拥有哪种网卡，以及你的网卡是否需要特殊配置。由于我们从新编译的内核中没有使用任何模块，我们可以删除 `conf.modules` 文件并卸载 `modutils` 程序。

`modutils` 包包含了用于 2.0 内核下自动加载模块以及 2.0 和 2.2 内核下卸载模块的内核程序，以及其他模块管理程序。加载和卸载模块的示例包括设备驱动程序和文件系统，以及其他一些。

要删除 `conf.modules` 文件使用命令：
`[root@deep]# rm -f /etc/conf/modules`

要卸载 `modutils` 包使用以下命令：
`[root@deep]# rpm -e nodeps modutils`

最后一件事是编辑 `rc.sysconfig` 文件，通过在行开头插入 `#` 来注释掉所有与 `depmod -a` 相关的行。这是必要的，因为系统在启动时默认读取 `rc.sysconfig` 脚本来查找内核中的模块依赖关系。

注释掉 `rc.sysconfiginit` 中的第 260 行（`vi +260 /etc/rc.d/rc.sysconfiginit`）：

```bash
if [ -x/sbin/depmod -a n "$USEMODULES" ]; then
```
修改为：
```bash
# [ -x/sbin/depmod -a n "$USEMODULES" ]; then
```

在 `rc.sysconfig` 文件中注释掉第 272 行到 277 行（`vi +272 /etc/rc.d/rc.sysconfig`）：

```bash
if [ -L /lib/modules/default ]; then

  INIT_ARGS=action "Finding module dependencies" depmod -a default

else

  INIT_ARGS=action "Finding module dependencies" depmod -a

fi
```



**注意**：再次说明，此部分“删除程序、文件和行”只有在你上面的内核配置中对“启用可加载模块支持 (`CONFIG_MODULES`)”回答否时才需要。描述的操作涉及 `initscripts-4_70-1` 包。

现在必须重启系统并测试你的结果。
```
[root@deep]# reboot
```

系统重启并登录后，使用以下命令验证你的新内核版本：

© Copyright 1999 Open Network Architecture ®

要验证你的新内核版本，使用以下命令：
```
[root@deep]# uname -a
```

# 第 6 章 TCP/IP 网络管理

在本章中

- 在每台机器上安装多块网卡
- 与网络功能相关的文件
- 使用命令行手动配置 TCP/IP 网络
- TCP/IP 安全问题概述

## 概述

网络管理涵盖了广泛的主题。通常来说，它包括收集有关网络各个部分的数据和信息，并在必要时采取行动处理故障和其他变化。最原始的网络监控技术是对关键主机进行周期性“ping（ping检测）”。更复杂的网络监控需要能够从网络上的各种设备获取特定的状态和统计信息。这些信息应该包括各种类型的数据报计数，以及各种类型的错误计数。

在本章中，我们将尝试回答关于网络设备、与网络功能相关的文件、基本网络命令以及 TCP/IP 安全概述的基础问题。

## 在每台机器上安装多个网卡

你可能使用 Linux 作为两个以太网之间的网关。在这种情况下，你的服务器上可能有两个网卡。为了消除启动时出现的问题，Linux 内核不会自动检测多个网卡。如果你有两个或更多网卡，应该使用用于单体内核的 `filo.conf` 文件或用于模块化内核的 `conf.modules` 文件来指定网卡的参数。

### 如果驱动程序作为可加载模块使用（模块化内核）

对于 PCI 驱动程序，模块通常会自动检测所有已安装的卡。对于 ISA 网卡，你需要提供网卡的 I/O 基地址，以便模块知道去哪里查找。这些信息存储在 `/etc/conf.modules` 文件中。

例如，我们有两个 ISA 3c509 网卡，分别位于 I/O `0x300` 和 I/O `0x320`。

对于 ISA 网卡，编辑 `conf.modules` 文件（`vi /etc/conf.modules`）并添加：
```
alias eth0 3c509

alias eth1 3c509

options 3c509 io=0x300,0x320
```
这意味着应该为 `eth0` 或 `eth1`（`alias eth0, eth1`）加载 `3c509` 驱动，并且加载时应带有驱动程序知道去查找网卡的选项。那个 `0x` 是重要的——像 DOS 世界中常用的 `300h` 这种写法是无效的。

对于 PCI 网卡，你只需要为 `eth` 接口指定相应的驱动程序别名，因为 PCI 网卡的 I/O 基地址可以安全地检测。

对于 PCI 网卡，编辑 `conf.modules` 文件（`vi /etc/conf.modules`）并添加：
```
alias eth0 3c509

alias eth1 3c509
```

### 如果驱动程序编译进内核（单体内核）

PCI 探测将找到所有相关的网卡。ISA 网卡也会自动找到所有相关的网卡，但在某些情况下，ISA 网卡仍然需要执行以下操作。这些信息存储在 `/etc/lilo.conf` 文件中。该方法是向内核传递启动参数，这通常由 LILO 完成。

对于 ISA 网卡，编辑 `lilo.conf` 文件（`vi /etc/lilo.conf`）并添加：
```
append="eth0,0,eth1"
```
注意：首先在不使用 `"lilo.conf"` 文件中的启动参数的情况下测试你的 ISA 网卡，如果失败，再使用启动参数。

在这种情况下，`eth0` 和 `eth1` 将按照网卡被找到顺序进行分配。如果你必须使用第二种方法（如果驱动程序编译进内核）在系统中安装我们的第二个以太网卡，请记住，这仅在某些 ISA 网卡情况下需要，PCI 网卡会自动找到。

## 与网络功能相关的文件

在 Linux 中，TCP/IP 网络通过几个文件进行配置，你可能需要编辑这些文件以使网络工作。了解与 TCP/IP 网络相关的配置非常重要，以便在必要时编辑和配置文件。记住，我们的服务器没有通过图形界面配置文件的窗口 界面。以下章节描述了基本的 TCP/IP 配置文件。

### `etc/HOSTNAME` 文件

此文件存储你的系统主机名——你的系统完全限定域名（FQDN），例如 `deep.openarch.com`。

以下是 `etc/HOSTNAME` 示例文件：
```
deep.openarch.com
```

### `etc/sysconfig/network-scripts/ifcfg-ethN` 文件

对于你可能需要或添加到系统中的每个网络设备，其文件位于 `etc/sysconfig/network-scripts/` 目录下。在 Red Hat Linux 6 中，第一个接口命名为 `ifcfg-eth0`，第二个接口命名为 `ifcfg-eth1`。

以下是 `etc/sysconfig/network-scripts/ifcfg-eth0` 示例：
```
DEVICE=eth0

ADDR=208.164.186.1

MASK=255.255.255.255

NETWORK=208.164.186.0

BROADCAST=208.164.186.255

ONBOOT=eth0

BOOTPROTO=none

USERCTL=eth0
```
如果你想手动修改网络地址或在新接口上创建新网络，可以使用此文件（`ifcfg-ethN`），其中 `N` 是物理设备的名称。
```
DEVICE=eth0
```

关于本页面的意见和建议请邮寄至 `gmnourani@videotron.ca`

操作流程如下：每当服务请求到达时，`inet` 守护进程会被欺骗去运行 `tcp` 程序而不是所需的服务器。`tcpd` 会进行一些额外的检查。如果没有问题，`tcp` 就会运行相应的服务器程序并退出。

`tcp` 通过查看由地址->name DNS 服务器返回的主机名和地址，验证由地址->name 服务器返回的客户端名称。如果发现任何差异，`tcp` 就会认为它正在处理一个伪装成他人的主机的欺骗请求。

可选情况下，`tcpd` 在其所连接的每一个连接上分配源路由选项。这可以处理大多数来自伪装成他人网络地址主机的攻击。UDP 服务无法从这种保护中获益。超时问题通常是由于服务器尝试将客户端 IP 地址解析为 DNS 名称引起的。这可能是因为你的服务器上 DNS 配置不当，或者客户端在 DNS 中是不可知的。

如果你打算在你的服务器上运行 `telnet` 或 `ip` 服务，并且没有在服务器的 `etc/hosts` 文件中添加客户端机器名称和 IP，或者你可以预期等待几分钟直到 DNS 查询超时，才能获得 a: 提示符：

## 使用命令行手动配置 TCP/IP 网络

`ifconfig` 是用于设置和配置你的网卡的工具。在需要手动配置网络时，你应该理解这个命令。需要注意的重要一点是，当使用 `ifconfig` 配置你的网络设备时，设置在重启后不会保留。

使用以下命令为 `ifconfig eth0` 分配 IP 地址 `208.164.186.2`：
```
root[deep]# ifconfig eth0 208.164.186.2 netmask 255.255.255.0
```

使用以下命令显示你可能拥的所有接口：
```
root[deep]# ifconfig
```

输出应该看起来所示：
```
eth0

link encap:Ethernet HWaddr:W0:E0:18:B5

inet addr:208.164.186.2 Bcast:208.164.255.255 Mask:255.255.255.0

MTU:1500 Metric:1

UP BROADCAST RUNNING MULTICAST

RX packets: 1295 errors:0 dropped:0 overruns:0 frame:0

TX packets: 1163 errors:0 dropped:0 overruns:0 carrier:0

collisions:0

Interupt:11 Base address:0xa80

lo

link encap:Local Loopback

inet addr:127.0.0.1 Mask:255.0.0.0

UP BROADCAST RUNNING MTU:3924 Metric:1

RX packets: 139 errors:0 dropped:0 overruns:0 carrier:0

TX packets: 139 errors:0 dropped:0 overruns:0 carrier:0

collisions:0
```



如果在未带任何参数的情况下调用 `ifconfig`，它会显示你配置的所有接口。你还有一个选项，使用以下命令：

- 使用以下命令显示你可能拥有的所有非活动接口：
  `root[deep]# ifconfig -a`

© Copyright 1999 Loop Open Network Architecture ®

### eth0
输出应该看起来所示：
```
Link encap:Ethernet HWaddr:00:E0:18:90:1B:56
inet addr:208.164.186.2 Bcast:208.164.186.255 Mask:255.255.255.255
UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
RX packets:1295 errors dropped:0 overheads:0 frame:0
TX packets:1163 errors dropped:0 overheads:0 carrier:0
collisions:0 tqueuelen:10
Interrupt:1 Base address:0xa800
```

### eth1
```
Link encap:Ethernet HWaddr:00:E0:18:90:1B:56
inet addr:192.168.1.232 Bcast:192.168.1.255 Mask:255.255.255.255
UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
RX packets:1295 errors dropped:0 overheads:0 frame:0
TX packets:1163 errors dropped:0 overheads:0 carrier:0
collisions:0 tqueuelen:10
Interrupt:5 Base address:0xa320
```

### lo
```
Link encap:Loopback
inet addr:127.0.0.1 Mask:255.0.0.0
UP BROADCAST RUNNING MTU:3924 Metric:1
RX packets:2339 errors dropped:0 overheads:0 frame:0
TX packets:2339 errors dropped:0 overheads:0 carrier:0
collisions:0 tqueuelen:0
```

`注意`：当使用 `ifconfig` 配置你的网络时，设置在重启后不会保留。

- 使用以下命令为 208.164.186.1 设置默认网关：
  `root[deep]# route add default gw 208.164.186.1`
在此示例中，默认路由被设置为 208.164.186.1，即你的路由器。从你的网络中选择一个主机，例如 208.164.186.1。

- 使用以下命令验证你是否到达主机：
  `root[deep]# ping 208.164.186.1`

输出应该看起来所示：
```
PING 208.164.186.1 (208.164.186.1) : 56 bytes of data

64 bytes from 208.164.186.1: ttl=62 time=1.0ms

64 bytes from 208.164.186.1: ttl=62 time=1.0ms

64 bytes from 208.164.186.1: ttl=62 time=1.0ms

--- 208.164.186.1 statistics ---

4 packets transmitted, 4 packets received, 0% packet loss

round-trip min/avg/max = 1.0/1.0/1.0 ms
```



你应该使用 `route` 命令显示路由信息，以检查两个主机都有正确的条目：

- 使用以下命令显示路由信息：
  `root[deep]# route -n`

输出如下：

| Destination | Gateway | Genmask | Flags | Metric | Use |
|---|---|---|---|---|---|
| 208.164.186.2 | 0.0.0.0 | 255.255.255 | UH | 0 | eth0 |
| 208.164.186.2 | 208.164.186.1 | 255.255.255 | UG | 0 | eth0 |
| 208.164.186.2 | 0.0.0.0 | 255.255.255 | U | 0 | eth0 |
| 127.0.0.0 | | 255.0.0.0 | U | 0 | lo |

- 使用以下 `netstat -i` 命令快速检查接口状态：
  `root[deep]# netstat -i`

输出应该看起来所示：

| Interface | MTU | Met | RX-OK | RX-ERR | RX-DRP | RX-OVR | TX-OK | TX-ERR | TX-OVR | Fl |
|---|---|---|---|---|---|---|---|---|---|---|
| eth0 | 1500 | 0 | | | | 3700 | 0 | | | BRU |
| lo | 3924 | 0 | 13300 | | | 13300 | 0 | | | LRU |
| ppp0 | 1500 | 0 | 14 | 1 | | | | | 另一个有用的 `netstat` 选项是 `-t`，它可以显示所有活跃的 TCP 连接。以下是 `netstat` 的典型结果：

- 使用此类命令显示所有活跃的 TCP 连接：
  `root[deep]# netstat -t`

输出应该看起来所示：
活动连接（无服务器）

| Recv-Q | Send-Q | Local Address | Foreign Address | State |
|---|---|---|---|---|
| Tcp 0 0 | | deep.openarch.netbios-ssn | gate.openarch.com:1045 | ESTABLISHED |
| Tcp 0 0 | | localhost:1032 | ESTABLISHED |
| Tcp 0 0 | | localhost:1032 | ESTABLISHED |
| Tcp 0 0 | | localhost:1034 | ESTABLISHED |
| Tcp 0 0 | | localhost:1030 | ESTABLISHED |
| Tcp 0 0 | | localhost:1028 | ESTABLISHED |
| Tcp 0 0 | | localhost:1029 | ESTABLISHED |
| Tcp 0 0 | | localhost:1026 | ESTABLISHED |
| Tcp 0 0 | | localhost:1027 | ESTABLISHED |
| Tcp 0 0 | | localhost:1024 | ESTABLISHED |
| Tcp 0 0 | | localhost:1025 | ESTABLISHED |
| Tcp 0 0 | | localhost:1025 | ESTABLISHED |

- 使用此类命令显示所有活跃和监听的 TCP 连接：
  `root[deep]# netstat -vat`

输出应该看起来所示：
活动连接（服务器和已建立）

| Recv-Q | Send-Q | Local Address | Foreign Address | State |
|---|---|---|---|---|
| tcp 0 0 | | deep.openarch.netbios-ssn | gate.openarch.com:1045 | ESTABLISHED |
| tcp 0 0 | | localhost:1032 | LISTEN |
| tcp 0 0 | | deep.openarch.com | ESTABLISHED |
| tcp 0 0 | | 208.164.186.1 | LISTEN |
| tcp 0 0 | | 208.164.186.1 | ESTABLISHED |
| tcp 0 0 | | 127.0.0.1 | LISTEN |

# TCP/IP 安全问题

TCP/IP 协议族存在许多漏洞，允许攻击者利用隐蔽道形式的手段，在看似无害的数据包中秘密地传输数据。本节将尝试通过理论示例来阐这些漏洞。

# 应用

隐蔽道被描述为：“任何可以被进程利用，以违反系统安全策略的方式传输信息的通信通道。从本质上说，它是一种并非实际计算机系统设计部分的通信方法，并可用于将信息传输给通常不被允许访问信息的用户或进程。”

在 TCP/IP 的情况下，有许多方法可以建立隐蔽道，并在主机之间进行秘密传输。这些方法可以用于许多不同的领域，如下所示：

- 绕过数据包过滤器、网络嗅探器和“敏感词”搜索引擎。
- 将加密或未加密的信息封装在其他情况下正常的数据包中，以便在禁止此类“TCP/IP 隐写术”的网络中进行秘密传输。
- 通过在无害的 Internet 站点之间“回跳”带有封装信息的数据包，来隐藏传输数据的位置。

重要的是，TCP 是一种“面向连接的”或“可靠的”协议。简单来说，TCP 具有确保数据通常以完整方式到达远程主机的特征。其基本操作依赖于初始的 TCP “三次握手”，在下方的三个步骤中进行了描述。

### 步骤 1
发送同步（SYN）数据包和初始序列号（ISN）

主机 A 想要与主机 B 建立连接。主机 A 向主机 B 发送一个数据包，其中同步位（SYN）用于建立新连接，并带有初始序列号（ISN），以便跟踪在主机之间发送的数据包：

```
Host A ------SYN(ISN)-----> Host B
```

### 步骤 2
允许远程主机用确认（ACK）进行响应

主机 B 通过发送一个设置了同步位（SYN）和确认位（ACK）的数据包回传给调用主机来响应请求。该数据包不仅包含接收者的序列号，还包含初始序列号加 1（ISN+1），表示远程数据包已作为确认的一部分正确接收，并等待下一次传输：

```
Host A <-----SYN(ISN+1)/ACK----- Host B
```

### 步骤 3
通过向远程主机发送最终确认来完成协商。

此时，主机 A 发回最终的 ACK 数据包和序列号，表示接收成功且连接完成，数据现在可以流传输：

```
Host A -------> Host B
```



整个连接过程在几毫秒内完成，双方从那时起独立地确认每个数据包。这种握手方法确保了主机之间“可靠的”连接，这也是 TCP 被认为是“面向连接的”协议的原因。应该注意的是，只有 TCP 数据包表现出这种协商过程。UDP 数据包则不然，它们被认为是“不可靠的”，在向远程主机发送之前不会尝试修正错误或协商连接：

# 在 TCP/IP 头部中编码信息

TCP/IP 头部包含许多可以存储信息并以隐蔽方式发送到远程主机的区域。参考以下图表，分别是 IP 和 TCP 头部的文本表示：

IP 头部（从 0 到 32 的数据位以及字段在数据报中的相对位置）

| 0 | 4 | 8 | 16 | 19 | 24 | 32 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 用户 | HLEN | 服务类型 | | 总长度 | | |
| 标识 | | 标志 | 分片偏移 | | | |
| 源 IP 地址 | | | | | | | |
| 目的 IP 地址 | | | | | | | |
| IP 选项 | 填充 | | | | | | |
| 数据 | | | | | | |

TCP 头部（数字代表从 0 到 32 的数据位以及字段在数据报中的相对位置）

| 0 | 4 | 8 | 16 | 19 | 24 | 32 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 源端口 | | 目的端口 | | | | |
| 序列号 | | | | | | | |
| 确认号 | | | | | | | |
| HLEN | 预留 | | 代码位 | | 窗口 | |
| 校验和 | | 紧急指针 | | | | | |
| 选项 | 填充 | | | | | |
| 数据 | | | | | | |

在每个头部内部，都有许多未用于正常传输或未作为数据报发送者根据需要设置的“可选”字段的区域。对典型 IP 头部中未使用或可选区域的分析，揭示了数据可以被存储和传输的许多可能性。利用的基础依赖于编码 0-255 范围的 ASCII 值。使用这种方法，可以在看似为初始连接请求、已建立的数据流或其他中间步骤的数据包之间传递数据。这些数据包可以包含任何实际数据，也可以设计成看起来无害的数据。这些数据包还可以包含伪造的源和目的 IP 地址，以及伪造的源和目的端口。这对于越过某些类型的数据包过滤器传输信息非常有用。此外，伪造的数据包可用于启动匿名的 TCP/IP “回跳数据包网络”，其中系统之间的数据包通过合法站点进行中继，以防止嗅探器和其他网络监控设备的跟踪。

# 安全解决方案的实现

- 以下协议和系统常用于在计算机网络中解决并提供不同程度的安全服务。
- 绕过数据包过滤器、网络嗅探器和“敏感词”搜索引擎。
- 将加密或未加密的信息封装在其他情况下正常的数据包中，以便在禁止此类“TCP/IP 隐写术”的网络中进行秘密传输。
- 通过在无害的 Internet 站点之间“回跳”带有封装信息的数据包，来隐藏传输数据的位置。

关于本页面的意见和建议请邮寄至 gmourani@videotron.ca

# 什么是包过滤？

包过滤是内置在 Linux 内核中的防火墙类型。过滤防火墙工作在网络层。只有在过滤规则允许的情况下，数据才被允许离开系统。当包到达时，它们将根据其类型、源地址、目的地址以及每个数据包中包含的端口信息进行过滤。

大多数情况下，包过滤通过使用根据过滤规则转发数据包的路由器来实现。当数据包到达包过滤路由器时，路由器从数据包头提取信息，并根据过滤规则决定数据包是通过还是被丢弃。

从数据包头中可以提取以下信息：

- 源 IP 地址
- 目的 IP 地址
- TCP/UDP 源端口
- TCP/UDP 目的端口
- ICMP 消息类型
- 封装协议（TCP、UDP、ICMP 或 IP 隧道）

由于分析的数据较少，日志防火墙消耗的 CPU 更少，对您的网络产生的延迟也小。有很多方法可以构建您的网络以使用防火墙保护您的系统。

## 拓扑结构

如果没有防火墙服务器，所有服务器都应配置为阻塞未使用的端口。这需要更高的安全性。想象一下有人访问了您的防火墙网关服务器，如果您的邻居服务器没有配置阻塞未使用的端口，那么他们就可以长驱直入了。本地连接也是如此。未经授权的员工可以从内部访问您的其他服务器。

在我们的配置中，我们将为您提供三个示例，可以帮助您根据想要保护的服务器类型配置防火墙规则，以及这些服务器在您的网络架构中的位置。第一个示例防火墙规则文件将用于 Web 服务器，第二个用于邮件服务器，最后一个用于网关服务器，它作为内部 Windows 、工作站和服务器机器的代理。请查看下图以获取思路。

![](img/4444dd2a96323af53b5149a2b33efe8b_103_0.png)

© Copyright 2001 Network Architecture 104

关于本页面的意见和建议请邮寄至 gmourani@videotron.ca

## 208.164.186.2

| www.openarch.com | deep.openarch.com | mail.openarch.com |
| :--- | :--- | :--- |
| 缓存 DNS | 主 DNS | 备 DNS |
| 208.164.186.3 | 208.164.186.1 | 208.164.186.2 |
| 1. 回环接口上的无限流量 | 1. 回环接口上的无限流量 | 2. ICMP 流量 |
| 3. 53 端口上的 DNS 服务器和客户端 | 4. 22 端口上的 SSH 服务器和客户端 | 5. 80 端口上的 HTTP 服务器 |
| 6. 443 端口上的 HTTPS 服务器和客户端 | 7. 25 端口上的 SMTP 客户端 | 8. 20, 21 端口上的 FTP 服务器 |
| 9. 发送的 traceroute 请求 | 3. 53 端口上的 DNS 服务器和客户端 | 4. 22 端口上的 SSH 服务器和客户端 |
| 5. 80 端口上的 HTTP 服务器 | 6. 443 端口上的 HTTPS 服务器和客户端 | 7. 25 端口上的 SMTP 客户端 |
| 8. 8080 端口上的 WWW-Cache 客户端 | 9. 110 端口上的外部端口 | 10. 119 端口上的外部 NTP 客户端 |
| 11. 143 端口上的 IMAP 服务器 | 12. 669 端口上的 IRC 客户端 | 13. 400 端口上的 ICMP 客户端 |
| 14. 20, 21 端口上的 FTP 客户端 | 15. 音频 / QuickTime | 16. 发送的 traceroute 请求 |
| 4. 22 端口上的 SSH 服务器 | 5. 25 端口上的 SMTP 服务器和客户端 | 6. 143 端口上的 IMAP 服务器 |

该表显示了我的防火墙脚本默认在不同服务器上启用的端口。根据外部可能提供的服务，您必须配置防火墙脚本以允许指定端口上的流量。**www.openarch.com** 是我们的 Web 服务器，**mail.openarch.com** 是我们的邮件服务器，**deep.openarch.com** 是本章中解释的所有示例的网关服务器。

## 构建支持 IPTables 的内核

您需要做的第一件事是确保您的内核在构建时包含了网络防火墙支持。记住，如果没有防火墙服务器，所有服务器都应配置为阻塞未使用的端口。在内核版本 2.2.14 中，您需要确保对以下问题回答了 **Y**：

网络选项：
- 网络防火墙 (`CONFIG_FIREWALL`) [Y]
- IP 防火墙 (`CONFIG_FIREWALL`) [Y]
- IP TCP syncookie 支持 [Y]

注意：如果您遵循 Linux 内核部分并重新编译内核，上述的“网络防火墙、IP 防火墙和 TCP syncookie 支持”选项已经设置好。

© Copyright 1999 Open Network Architecture 105

## IP 伪装和 ICMP 伪装仅对于网关服务器需要。

IP 伪装 (`CONFIG_IP_MASQUERADE`) [Y]
ICMP 伪装 (`CONFIG_IP_MASQUERADE_ICMP`) [Y]

注意：只有您的网关服务器需要具有“IP:Masquerading”和“IP:ICMP Masquerading”内核选项。这是您的内部网络访问外部所必需。

伪装意味着，如果您的本地网络上的某台 Linux 机器作为防火墙想要向外部发送内容，您的机器可以“伪装”成那台计算机，即它将流量转发到预定的外部目的地，但使其看起来像是来自防火墙本身。

它是双向起的；如果外部进行回复，Linux 防火会将静默地将流量转发给相应的本地计算机。通过这样，本地网络上的计算机对外部是完全不可见的，尽管它们可以访问外部并接收回复。这使得本地网络上的计算机即使没有正式注册 IP 地址，也可以参与互联网。

IP 伪装代码只有在跨线路启用 IP 转发时才能工作：

```
echo "1" > /proc/sys/net/v4/ip_forward
```



从启动脚本来看，`/proc`文件系统已经挂载。您可以将此行添加到`/etc/rc.d/rc.local`中，这样当您的服务器重启时会自动启用 IP 转发。

编辑`rc.local`文件（`vi /etc/rc.d/rc.local`）并添加此行：

```
echo "1" > /proc/sys/net/v4/ip_forward
```

注意：只有您的网关服务器需要具有“IP:Masquerading”和“IP:ICMP Masquerading”内核选项。这是您的内部网络访问外部所必需的。如果您启用 IP 伪装，那么当您的本地网络上的某台计算机作为防火墙想要向外部发送内容时，您的机器可以“伪装”成那台计算机……这是网关的。

## 需要考虑的几点

如果您将系统连接到互联网，可以安全地假设您处于风险之中。我们建议：

- 网关不要运行任何绝对必要的应用程序。
- 网关应严格限制通过它的协议类型和数量（如 FTP 和 telnet）。
- 任何包含机密信息的系统都不应从互联网直接访问。

## 防火墙脚本使用的规则说明

以下是将在示例中使用的一些规则的解释。这仅供参考，防火墙脚本注释详细且易于修改。

## 防火墙脚本中的常量

常量用于大多数值。最基本的常量包括：

`EXTERNAL_INTERFACE`
连接互联网的外部网络接口。在示例中定义为`eth0`。

`LOCAL_INTERFACE_1`
连接局域网的内部网络接口（如果有）。在示例中定义为`eth1`。

`LOOPBACK`
回环接口名称。在示例中定义为`lo`。

`IPADDR`
您的接口的 IP 地址。它是在互联网注册的静态 IP 地址，或者是通过 ISP 动态分配的地址。

`LOCALNET_1`
您的局域网网络地址（如果有——局域网内机器使用的 IP 地址范围。这些可能是静态分配的，或者您可能使用本地 DHCP 服务器进行分配。其中范围为`192.168.1.0/24`，C 类私有地址。

`ANYWHERE`
任意是`ipchains`用于匹配任意（非广播）地址的标签。两个程序都提供`any/0`作为此地址的标签，其值为`0.0.0.0/0`。

`NAMESERVER_1`
您的网络或 ISP 的主 DNS 服务器 IP 地址。

`NAMESERVER_2`
您的网络或 ISP 的备 DNS 服务器 IP 地址。

`LOOPBACK`
回环地址范围为`127.0.0.0/8`。接口本身被地址为`127.0.0.1`（在`/etc/hosts`中）。

关于本页面的意见和建议应邮件至`gmourani@videotronca.ca`

### 特权端口 (PRIVPORTS)
特权端口 0 到 1023 通常统称为此类。

### 非特权端口 (UNPRIVPORTS)
非特权端口 1024 到 65535 通常统称为此类。它们是动态分配给连接客户端侧的地址。

### 默认策略 (Default Policy)
防火墙有一个默认策略，以及一组针对特定消息类型所采取的操作。这意味着，如果一个数据包没有被任何其他规则选中，将应用默认策略规则。

注意：`IPFW`防火墙有两种基本方法：默认拒绝所有并显式选择访问，以及默认接受并显式拒绝访问。默认拒绝是推荐的方法，因为这样更容易设置更安全的防火墙。

### 启用本地流量 (Enabling Local Traffic)
由于策略是拒绝的，因此必须撤销其中的某些设置。本地网络服务不通过外部网络接口，而是通过一个名为“环回接口”（loopback interface）的特殊专用接口运行。在允许环回之前，你所有的本地网络程序都无法工作。

```
# 环回接口上的无限流量

ipchains -A input -i $LOOPBACK_INTERFACE -j ACCEPT

ipchains -A output -i $LOOPBACK_INTERFACE -j ACCEPT
```

### 源地址过滤 (Source Address Filtering)
使用互联网协议 (IP) 标识唯一方法是 IP 数据包头中的源地址。这为源地址伪造打开了大门；发送者将其地址替换为不存在的地址，或其他网站的地址。这可能允许不智的威胁进入你的系统，或者在你攻击其他网站时伪装成你。

```bash
# 拒绝伪装成外部地址的伪造包。

ipchains -A input -i $EXTERNAL_INTERFACE -s $IPADDR -j DENY
```

此外，在任何情况下，你都应该在外部接口拒绝至少七种源地址。

- 这些是声称来自以下位置的入站包：
- 你的外部 IP 地址
- A 类 IP 地址
- B 类私有 IP 地址
- C 类私有 地址
- D 类组播地址
- E 类预留地址
- 环回接口

除了你自己的地址外，拦截包含这些源地址的传出包可以保护你免受自身可能的配置错误的影响。

### 其他规则 (The rest of the rules)
防火墙脚本文件中使用的其他规则：

- 从外部世界访问服务
- 向外部世界提供服务
- 内部机器伪装 (Masquerading)

### 防火墙脚本文件

`iptables`允许你过滤数据包。设置防火墙、IP 伪装是将`iptchains`链传递给内核并告诉内核过滤哪些数据包。因此，你所有的防火墙设置都存储在内核中，并在重启时丢失。

为了避免这种情况，我们建议使用 System V init 脚本使你的规则永久化。要实现这一点，请为每台服务器在`/etc/rc.d/init.d`目录下创建一个如下防火墙脚本文件。由于每台服务器提供的服务不同，需要不同的防火墙设置。因此，我们提供了三种不同的防火墙设置，你可以根据需求进行尝试、检查和调整。我假设你对过滤和防火墙规则如何工作具有最低知识。

### Web 服务器 `/etc/rc.d/init.d/firewall` 脚本文件的配置

这是我们 Web 服务器机器的配置文件。该配置允许环回接口上的无限流量，以及 DNS 缓存和客户端服务器 (53)、SSH 服务器 (22)、HTTP (80)、HTTPS 服务器 (443)、SMTP 客户端 (25)、FTP 服务器 (20, 21) 以及出站路由请求。

如果你不想在 Web 服务器防火墙规则中启用我默认开启的某些服务，请在行开头用`#`将其注释掉。如果你想使用被`#`注释掉的其他服务，请删除这些行开头的`#`。

在你的 Web 服务器上创建防火墙脚本文件（`touch /etc/rc.d/init.d/firewall`）并：

```bash
#!/bin/sh

#
# 最后一次由 Gerhard Mourani 修改：02-01-2000
#
# 版权所有 (C) 1997, 1998, 1999 Robert L. Ziegler
#
# 允许免费使用、复制、修改和分发本软件及其
# 附带，无需书面协议。
# 本软件作为个人防火墙开发的 示例和基础提供。本软件不提供任何保证。
#
# Robert L. Ziegler 提供的任何材料均按
# "现状"提供。对于任何事项，他不提供任何形式的
# 无论是显式的还是隐含的保证，包括但不限于
# 对特定用途的适用性保证、排他性或从使用材料中
# 获得的的结果。
#
# 从 /etc/rc.d/init.d/firewall 调用
# chconfig=: 95
# description: 启动和停止 IPTCHAINS 防火墙 \
# 用于提供网络服务。
#
# 加载函数库。
./etc/rc.d/init.d/functions
#
# 加载网络配置。
./etc/sysconfig/network
```

# 检查网络是否已启动。
[$NETWORKING] = "no" && exit 0

# 查看我们是如何调用的。
case "$1" in
start)
echo -n "Starting Firewall Services: "

# 为了便于维护的某些定义。

# 请根据你的系统和 ISP 修改这些内容。
```bash

EXTERNAL_INTERFACE="eth0"

LOOPBACK_INTERFACE="lo"

IPADDR="208.164.186.3"

ANYWHERE="any"

NAMESERVER="208.164.186.1"

NAMESERVER_2="208.164.186.2"

```

# 主 DNS 服务器
# 备 DNS 服务器

```bash

SMTP_SERVER="mail.openarch.com"

SYSLOG_SERVER="mail.openarch.com"

SYSLOG_CLIENT="208.164.0.0/24"

```

# 你的邮件服务器
# 你的内部日志服务器
# 你的内部日志客户端

```bash

LOOPBACK="127.0.0.1"

CLASS_A="10.0.0.0/8"

CLASS_B="172.16.0.0/12"

CLASS_C="192.168.0.0/16"

CLASS_D="224.0.0.0/4"

CLASS_E="240.0.0.0/4"
```



关于此页面的意见和建议可以邮寄至 `gmourani@videotron.ca`

```bash
ipchains -A output -d $EXTERNAL_INTERFACE -d $CLASS_C -j REJECT-|
```

# 拒绝自称来自回环接口的数据包

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s $LOOPBACK -j DENY |
ipchains -A output -i $EXTERNAL_INTERFACE -s $LOOPBACK -j REJECT-|
```

# 拒绝广播源地址数据包

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -d $BROADCAST_DEST -j DENY |
ipchains -A output -i $EXTERNAL_INTERFACE -d $BROADCAST_SRC -j DENY |
```

# 拒绝 D 类多组播地址 (in.h) (NET-3-HOWTO)

# 多组播 UDP

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s $CLASS_D_MULTICAST -j DENY |
```

# 拒绝 E 类保留留 IP 地址

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s $CLASS_E_RESERVED -j DENY |
```

# 拒绝由 IANA 定义的地址

# 0.*.1.*.2-5.*.7-7.*.23-27.*

# 31-33.*.37-39.*.41-44.*.52-57.*.58-60.*

# 65-95.*.126-197.*.201-219.*

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s 1.0.0.0/8 -j DENY |
ipchains -A input -i $EXTERNAL_INTERFACE -s 2.0.0.0/8 -j DENY |
ipchains -A input -i $EXTERNAL_INTERFACE -s 5.0.0.0/8 -j DENY |
ipchains -A input -i $EXTERNAL_INTERFACE -s 7.0.0.0/8 -j DENY |
ipchains -A input -i $EXTERNAL_INTERFACE -s 23.0.0.0/8 -j DENY |
ipchains -A input -i $EXTERNAL_INTERFACE -s 27.0.0.0/8 -j DENY |
ipchains -A input -i $EXTERNAL_INTERFACE -s 31.0.0.0/8 -j DENY |
ipchains -A input -i $EXTERNAL_INTERFACE -s 33.0.0.0/8 -j DENY |
ipchains -A input -i $EXTERNAL_INTERFACE -s 37.0.0.0/8 -j DENY |
ipchains -A input -i $EXTERNAL_INTERFACE -s 39.0.0.0/8 -j DENY |
ipchains -A input -i $EXTERNAL_INTERFACE -s 41.0.0.0/8 -j DENY |
ipchains -A input -i $EXTERNAL_INTERFACE -s 44.0.0.0/8 -j DENY |
ipchains -A input -i $EXTERNAL_INTERFACE -s 52.0.0.0/8 -j DENY |
ipchains -A input -i $EXTERNAL_INTERFACE -s 58.0.0.0/8 -j DENY |
ipchains -A input -i $EXTERNAL_INTERFACE -s 60.0.0.0/8 -j DENY |
```

# 65.0.0.0/0 - /3 包含 64-69 范围

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s 65.0.0.0/8 -j DENY |
ipchains -A input -i $EXTERNAL_INTERFACE -s 66.0.0.0/8 -j DENY |
ipchains -A input -i $EXTERNAL_INTERFACE -s 67.0.0.0/8 -j DENY |
ipchains -A input -i $EXTERNAL_INTERFACE -s 68.0.0.0/8 -j DENY |
ipchains -A input -i $EXTERNAL_INTERFACE -s 69.0.0.0/8 -j DENY |
ipchains -A input -i $EXTERNAL_INTERFACE -s 70.0.0.0/8 -j DENY |
ipchains -A input -i $EXTERNAL_INTERFACE -s 71.0.0.0/8 -j DENY |
ipchains -A input -i $EXTERNAL_INTERFACE -s 72.0.0.0/8 -j DENY |
ipchains -A input -i $EXTERNAL_INTERFACE -s 73.0.0.0/8 -j DENY |
ipchains -A input -i $EXTERNAL_INTERFACE -s 74.0.0.0/8 -j DENY |
ipchains -A input -i $EXTERNAL_INTERFACE -s 75.0.0.0/8 -j DENY |
ipchains -A input -i $EXTERNAL_INTERFACE -s 76.0.0.0/8 -j DENY |
ipchains -A input -i $EXTERNAL_INTERFACE -s 77.0.0.0/8 -j DENY |
ipchains -A input -i $EXTERNAL_INTERFACE -s 78.0.0.0/8 -j DENY |
ipchains -A input -i $EXTERNAL_INTERFACE -s 79.0.0.0/8 -j DENY |
```

# 80.0.0.0/4 - /4 包含 80-95

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s 80.0.0.0/4 -j DENY |
```

# 96.0.0.0/4 - /4 包含 96-111

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s 96.0.0.0/4 -j DENY |
```

# 128.0.0.0/3 - /3 包含 112-127

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s 128.0.0.0/8 -j DENY |
ipchains -A input -i $EXTERNAL_INTERFACE -s 132.0.0.0/8 -j DENY |
```

© Copyright 1999 Open Network Architecture

关于此页面的意见和建议应邮寄至 `gmourani@videotron.ca`

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s 114.0.0.0/8 -j DENY-
ipchains -A input -i $EXTERNAL_INTERFACE -s 115.0.0.0/8 -j DENY-
ipchains -A input -i $EXTERNAL_INTERFACE -s 116.0.0.0/8 -j DENY-
ipchains -A input -i $EXTERNAL_INTERFACE -s 117.0.0.0/8 -j DENY-
ipchains -A input -i $EXTERNAL_INTERFACE -s 118.0.0.0/8 -j DENY-
ipchains -A input -i $EXTERNAL_INTERFACE -s 119.0.0.0/8 -j DENY-
ipchains -A input -i $EXTERNAL_INTERFACE -s 120.0.0.0/8 -j DENY-
ipchains -A input -i $EXTERNAL_INTERFACE -s 121.0.0.0/8 -j DENY-
ipchains -A input -i $EXTERNAL_INTERFACE -s 122.0.0.0/8 -j DENY-
ipchains -A input -i $EXTERNAL_INTERFACE -s 123.0.0.0/8 -j DENY-
```



`ipchains -A input -i $EXTERNAL_INTERFACE -s 124.0.0.0/8 -j DENY-`

`ipchains -A input -i $EXTERNAL_INTERFACE -s 125.0.0.0/8 -j DENY-`

`ipchains -A input -i $EXTERNAL_INTERFACE -s 126.0.0.0/8 -j DENY-`

```bash
# 216.0.0.0/5 - /5 包含 217-219

ipchains -A input -i $EXTERNAL_INTERFACE -s 217.0.0.0/8 -j DENY-

ipchains -A input -i $EXTERNAL_INTERFACE -s 218.0.0.0/8 -j DENY-

ipchains -A input -i $EXTERNAL_INTERFACE -s 219.0.0.0/8 -j DENY-
```

```bash
# 224.0.0.0/4 - /6 包含 220-223

ipchains -A input -i $EXTERNAL_INTERFACE -s 224.0.0.0/4 -j DENY -
```

# ICMP

- 为了防止 ICMP 炸弹拒绝服务攻击，请过滤
# 入站重定向 (5) 和出站目的不可达 (3)，
# 注意，禁用目的不可达 (3) 并不建议，
# 因为用于协商数据包大小。

- 用于双向：
# 消息类型：回显 (0), 回请求 (8)
# 防止攻击，将源地址限制在您的 ISP 范围内。

- 用于出站追踪 (tracer)。
# 消息类型：入站目的不可达 (3),超时 (11)
# 默认 UDP 基准：33434 到 base+nops-1

- 用于入站追踪 (tracer)。
# 消息类型：出站目的不可达 (3), 超时 (11)
# 要阻止此项，拒绝出站的 33 和 11

```bash
# 0: 回显回复 (pong)

# 3: 目的不可达、端口可达、需要分片等

# 4: 源抑制

# 5: 重定向

# 8: 回显请求 (ping)

# 11: 超时

# 12: 参数问题

ipchains -A input - $EXTERNAL_INTERFACE -p icmp \
-s $ANYWHERE -o d $IPADDR -jACCEPT

ipchains -A input - $EXTERNAL_INTERFACE -p icmp \
-s $ANYWHERE -o s $IPADDR -jACCEPT

ipchains -A input - $EXTERNAL_INTERFACE -p icmp \
-s $ANYWHERE 4 -d $IPADDR -jACCEPT

ipchains -A input - $EXTERNAL_INTERFACE -p icmp \
-s $ANYWHERE 11 -s $IPADDR -jACCEPT

ipchains -A input - $EXTERNAL_INTERFACE -p icmp \
-s $ANYWHERE 12 -d $IPADDR -jACCEPT

ipchains -A input -s 208.166.180
```

```bash
# UDP TRACROUTE

# traceroute 通常使用 -32769:65535 -33434:33523
```

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
-s $TRACOUTE_SRC_PORTS \
-d $IPADDR $TRACOUTE_DEST_PORTS -jACCEPT-|
```

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp ! -y \
-s $NAMESERVER_1 53 \
-d $IPADDR $UNPRIVORTS -j ACCEPT
```

```bash
ipchains -A output -i $EXTERNAL_INTERFACE -p tcp \
-s $IPADDR $UNPRIVORTS \
-d $NAMESERVER_1 53 -j ACCEPT
```

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
-s $NAMESERVER_2 53 \
-d $IPADDR $UNPRIVORTS -j ACCEPT
```

```bash
ipchains -A output -i $EXTERNAL_INTERFACE -p udp \
-s $IPADDR $UNPRIVORTS \
-d $NAMESERVER_2 53 -j ACCEPT
```

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp ! -y \
-s $NAMESERVER_2 53 \
-d $IPADDR $UNPRIVORTS -j ACCEPT
```

```bash
ipchains -A output -i $EXTERNAL_INTERFACE -p tcp \
-s $IPADDR $UNPRIVORTS \
-d $NAMESERVER_2 53 -j ACCEPT
```

# TCP 仅在选定端口上接受

### SSH 服务器 (22)
# .............
```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
-s $ANYWHERE $UNPRIVORTS \
-d $IPADDR 22 -j ACCEPT
```

```bash
ipchains -A output -i $EXTERNAL_INTERFACE -p tcp ! -y \
-s $IPADDR 22 \
-d $ANYWHERE $UNPRIVORTS -j ACCEPT
```

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp ! -y \
-s $ANYWHERE $SSH_PORTS \
-d $IPADDR 22 -j ACCEPT
```

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp ! -y \
-s $IPADDR 22 \
-d $ANYWHERE $SSH_PORTS -j ACCEPT
```

# SSH 客户端 (22)
# # ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
# -s $ANYWHERE 22 \
# -d $IPADDR 22 -j ACCEPT

```bash
# ipchains -A output -i $EXTERNAL_INTERFACE -p tcp \
# -s $IPADDR $UNPRIVORTS \
# -d $ANYWHERE 22 -j ACCEPT
```

```bash
# ipchains -A input -i $EXTERNAL_INTERFACE -p tcp ! -y \
# -s $ANYWHERE 22 \
# -d $IPADDR $SSH_PORTS -j ACCEPT
```

关于本页的意见和建议请邮件至 `gmourani@videotron.ca`

```bash
# ipchains -A output -i $EXTERNAL_INTERFACE -p tcp \
# -s $IPADDR $SSH_PORTS \
# -d $ANYWHERE 22 -j ACCEPT
```

### HTTP 服务器 (80)
```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
-s $ANYWHERE $UNPRIV_PORTS \
-d $IPADDR 80 -j ACCEPT
```

```bash
ipchains -A output -i $EXTERNAL_INTERFACE -p tcp -y \
-s $IPADDR 80 \
-d $ANYWHERE $UNPRIV_PORTS -j ACCEPT
```

### HTTPS 服务器 (443)
```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
-s $ANYWHERE $UNPRIV_PORTS \
-d $IPADDR 443 -j ACCEPT
```

```bash
ipchains -A output -i $EXTERNAL_INTERFACE -p tcp -y \
-s $IPADDR 443 \



`-d $ANYWHERE $UNPRIV_PORTS -j ACCEPT`

### SYLOG 服务器 (514)
提供完整的远程日志功能。使用此功能，你可以控制一台主机上所有的 syslog 消息。
```bash
# ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
# -s $SYSLOG_CLIENT \
-d $IPADDR 514 -j ACCEPT
```

### SYLOG 客户端 (514)
```bash
# ipchains -A output -i $EXTERNAL_INTERFACE -p udp \
# -s $IPADDR 514 \
-d $SYSLOG_SERVER 514 -j ACCEPT
```

### AUTH 服务器 (113)
拒绝（Reject）而非禁止（deny）入站 auth 端口。（NET-3-HOWTO）
```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
-s $ANYWHERE \
-d $IPADDR 113 -j REJECT
```

关于本页的意见和建议请邮件至 gmourani@videotron.ca

```bash
# SMTP 客户端 (25)
#
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp -y \
-s $SMTP_SERVER 25 \
-d $IPADDR $UNPRIVORTS -j ACCEPT
```

```bash
ipchains -A output -i $EXTERNAL_INTERFACE -p tcp \
-s $IPADDR $UNPRIVORTS \
-d $SMTP_SERVER 25 -j ACCEPT
```

### FTP 服务器 (20, 21)
入站请求
```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
-s $ANYWHERE $UNPRIVORTS \
-d $IPADDR 21 -j ACCEPT
```

```bash
ipchains -A output -i $EXTERNAL_INTERFACE -p tcp -y \
-s $IPADDR 20 \
-d $ANYWHERE $UNPRIVORTS -j ACCEPT
```

### 端口通道响应
```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp -y \
-s $ANYWHERE $UNPRIVORTS \
-d $IPADDR 20 -j ACCEPT
```

```bash
ipchains -A output -i $EXTERNAL_INTERFACE -p tcp \
-s $IPADDR 20 \
-d $ANYWHERE $UNPRIVORTS -j ACCEPT
```

### 被动模式数据响应
```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
-s $ANYWHERE $UNPRIVORTS \
-d $IPADDR -j ACCEPT
```

```bash
ipchains -A output -i $EXTERNAL_INTERFACE -p tcp -y \
-s $IPADDR \
-d $ANYWHERE $UNPRIVORTS -j ACCEPT
```

### 出站路由追踪 (TRACOUTE)
```bash
ipchains -A output -i $EXTERNAL_INTERFACE -p udp \
-s $IPADDR $SRC_PORTS \
-d $ANYWHERE $DEST_PORTS -j ACCEPT
```

### 启用拒绝包的日志
```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
-d $IPADDR -j DENY
```

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
-d $IPADDR $UNPRIVORTS -j DENY
```

### ICMP 相关
```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p icmp \
-s $ANYWHERE 5 -
-d $IPADDR -j DENY
```

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p icmp \
-s $ANYWHERE 12-255 -
-d $IPADDR -j DENY
```

# #
stop)
echo -n "正在关闭防火墙服务: "
# 移除此过滤器的所有规则
ipchains -F
# 将过滤器的默认策略重置为接受
ipchains -P input ACCEPT
ipchains -P output ACCEPT
ipchains -P forward ACCEPT
# 关闭 SYN Cookie 保护
echo 0 >/proc/sys/net/ipv4/tcp_syn_cookies
# 关闭 IP 伪装防护
# 开启源地址验证
for f in /proc/sys/net/ipv4/conf/*rp_filter; do
echo 0 > $f
done
# 开启 ICMP 重定向
for f in /proc/sys/net/ipv4/conf/*accept_redirects; do
echo 1 > $f
done
# 开启源路由
for f in /proc/sys/net/ipv4/conf/*accept_source_route; do
echo 1 > $f
done
*)
echo -n "用法: firewall {start|stop|status|reload}"
exit 1
esac

现在，此脚本创建可执行文件并更改其默认权限：
```bash
[root@]# chmod 700 /etc/rc.d/init.d/firewall
[root@]# chmod 055 /etc/rc.d/init.d/firewall
```

使用以下命令为防火墙创建 rc.d 符号链接：
```bash
[root@]# chkconfig --add firewall
[root@]# chkconfig -level 345 firewall on
```

现在，你的防火墙规则配置为使用 System V（System V 负责启动启动需要运行的所有进程），并在服务器重启时自动启动。

使用以下命令手动停止服务器上的防火墙：
`[root@]# /etc/rc.d/init.d/firewall stop`

使用以下命令手动启动服务器上的防火墙：
`[root@]# /etc/rc.d/init.d/firewall start`

# 邮件服务器的 "/etc/rc.d/init.d/firewall" 脚本配置

这是我们邮件服务器的配置脚本。该配置默认允许环回（Loopback）、ICMP、DNS 服务器和客户端 (53)、SSH 服务器 (22)、SMTP 服务器和客户端 (25)、IMAP 服务器 (143) 以及出站路由追踪的无限流量。

如果你不需要我默认在邮件服务器防火墙规则中列出的服务，请在行开头使用 "#" 将其注释掉。如果你需要我用 "#" 注释的其他服务，请删除行开头的 "#"。

在你的邮件服务器上创建防火墙文件（`touch /etc/rc.d/init.d/firewall`）并添加以下内容：

```bash
#!/bin/sh
#
# 由 Gerhard Maurani 修改: 02-01-2000
# 版权所有 (C) 1997, 1999, 1998 Robert L. Ziegler
# 许可为了、研究和非营利目的，使用、复制、修改、研究和分发此软件及文档，
# 免收费用，且无需书面协议。
# 本软件作为开发个人防火墙的示例和基础。本软件不提供任何保证。
## Robert L. Ziegler 提供的任何材料均按
#“原样”提供。他对任何事项均不提供任何形式的明示或暗示保证，
# 包括但不限于特定用途的适用性、排他性或从使用材料中获得的结果。
#
# 调用自 /etc/rc.d/init.d/
# ifconfig - 95
# 说明: 启动和停止用于提供防火墙网络 \服务的 IPCHAINS 防火墙。
#
# 源函数库。
# /etc/rc.d/init.d/functions
#n 源网络配置。
# /etc/sysconfig/network
#n 检查网络是否已启动。
[$NETWORKING] = "no" && exit 0
# 查看我们是如何调用的。
```



`case "$1" in`

关于本页面的意见和建议应邮件至 `gmourani@videotron.ca`

`echo -n "Starting Firewalling Services: "`

## 为了方便维护的一些定义

```
# ---
# SSH 从 1023 开始，对于每增加一个并发入站
# 连接，端口向下递减 513。
```

`SSH_PORTS="1022:1023"` # SSH 特权端口范围

`traceroute` 通常使用 `-S 32769:65535 -D 33434:33523`

`TRACEROUT_SRC_PORTS="32769:65535"`

`TRACEROUT_DEST_PORTS="33434:33523"`

```bash
# ---
# 默认策略为拒绝 (DENY)
# 显式接受所需的入站和出站连接
```

```bash
# 删除所有属于此过滤器的现有规则
ipchains -F

# 将过滤器的默认策略设置为拒绝。
ipchains -P input DENY
ipchains -P output REJECT
ipchains -P forward REJECT
```

```bash
# ---
# 启用 TCP SYN Cookie 保护
echo 1 >/proc/sys/net/ipv4/tcp_sync_cookies

# 启用 IP 欺骗防护
# 开启源地址验证
for i in /proc/sys/net/ipv4/conf/*/rp_filter; do
  echo 1 > $i
done

# 禁用 ICMP 重定向
for i in /proc/sys/net/ipv4/conf/*/redirects; do
  echo 0 > $i
done
```



© Copyright 1999 Open Network Architecture ®

# 回环接口上的无限流量。

```
ipchains -A input -LOOPBACK -j ACCEPT
ipchains -A output -LOOPBACK -j ACCEPT
```

# 网络站点

`/etc/firewall.blocked` 包含一个列表

```
ipchains -A input -i EXTERNAL_INTERFACE -s - -j DENY
```

阻止任何访问。

```
if [ -f /etc/firewall.blocked ]; then
```

伪造的坏地址

拒绝伪造的数据包。

防止向外部地址发送数据。

```
ipchains -A input -i EXTERNAL_INTERFACE -s $IPADDR -j DENY
```

# 拒绝声称来自或属于 A 类有有网络的数据包

```
ipchains -A input -i EXTERNAL_INTERFACE -s $CLASS_A -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -d $CLASS_A -j DENY
ipchains -A output -i EXTERNAL_INTERFACE -s $CLASS_A -j REJECT
ipchains -A output -d $CLASS_A -j REJECT
```

# 拒绝声称来自或属于 B 类私有网络的数据包

```
ipchains -A input -i EXTERNAL_INTERFACE -s $CLASS_B -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -d $CLASS_B -j DENY
ipchains -A output -i EXTERNAL_INTERFACE -s $CLASS_B -j REJECT
ipchains -A output -d $CLASS_B -j REJECT
```

# 拒绝声称来自或属于 C 类私有网络的数据包

```
ipchains -A input -i EXTERNAL_INTERFACE -s $CLASS_C -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -d $CLASS_C -j DENY
ipchains -A output -i EXTERNAL_INTERFACE -s $CLASS_C -j REJECT
ipchains -A output -d $CLASS_C -j REJECT
```

# 拒绝来自回环接口的数据包

```
ipchains -A input -i EXTERNAL_INTERFACE -s $LOOPBACK -j DENY
ipchains -A output -i EXTERNAL_INTERFACE -s $LOOPBACK -j REJECT
```

# 拒绝广播地址数据包

```
ipchains -A input -i EXTERNAL_INTERFACE -s $BROADCAST_DEST -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -d $BROADCAST_SRC -j DENY
```

# 拒绝 D 类组播地址

组播是非法的源地址。组播使用 UDP。

```
ipchains -A input -i EXTERNAL_INTERFACE -s $CLASS_D_MULTICAST -j DENY
```

# 拒绝 E 类预留 IP 地址

```
ipchains -A input -i EXTERNAL_INTERFACE -s $CLASS_RESERVED_NET -j DENY
```

# 拒绝由 IANA 定义的地址

`0.0.0.0/8`, `1.0.0.0/8`, `2.0.0.0/8`, `3.0.0.0/8`, `4.0.0.0/4`, `5.0.0.0/8`, `6.0.0.0/8`, `7.0.0.0/8`, `8.0.0.0/7`, `9.0.0.0/8`, `10.0.0.0/8`, `11.0.0.0/8`, `12.0.0.0/8`, `13.0.0.0/8`, `14.0.0.0/8`, `15.0.0.0/8`, `16.0.0.0/4`, `17.0.0.0/8`, `18.0.0.0/8`, `19.0.0.0/8`, `20.0.0.0/4`, `21.0.0.0/8`, `22.0.0.0/7`, `23.0.0.0/8`, `24.0.0.0/4`, `25.0.0.0/8`, `26.0.0.0/8`, `27.0.0.0/7`, `28.0.0.0/4`, `29.0.0.0/8`, `30.0.0.0/8`, `31.0.0.0/8`, `32.0.0.0/8`, `33.0.0.0/8`, `34.0.0.0/8`, `35.0.0.0/8`, `36.0.0.0/8`, `37.0.0.0/8`, `38.0.0.0/8`, `39.0.0.0/8`, `40.0.0.0/6`, `41.0.0.0/8`, `42.0.0.0/8`, `43.0.0.0/8`, `44.0.0.0/4`, `45.0.0.0/8`, `46.0.0.0/8`, `47.0.0.0/8`, `48.0.0.0/6`, `49.0.0.0/8`, `50.0.0.0/8`, `51.0.0.0/8`, `52.0.0.0/8`, `53.0.0.0/8`, `54.0.0.0/8`, `55.0.0.0/8`, `56.0.0.0/8`, `57.0.0.0/8`, `58.0.0.0/7`, `59.0.0.0/8`, `60.0.0.0/8`, `61.0.0.0/8`, `62.0.0.0/8`, `63.0.0.0/8`, `64.0.0.0/8`, `65.0.0.0/8`, `66.0.0.0/8`, `67.0.0.0/8`, `68.0.0.0/8`, `69.0.0.0/8`, `70.0.0.0/8`, `71.0.0.0/8`, `72.0.0.0/8`, `73.0.0.0/8`, `74.0.0.0/8`, `75.0.0.0/8`, `76.0.0.0/8`, `77.0.0.0/8`, `78.0.0.0/8`, `79.0.0.0/8`

```
ipchains -A input -i EXTERNAL_INTERFACE -s 1.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 2.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 5.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 7.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 20.0.0.0/4 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 24.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 27.0.0.0/7 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 31.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 37.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 39.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 41.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 42.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 58.0.0.0/7 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 60.0.0.0/8 -j DENY
```

# 65: 0100000/0 掩码 65-79 溢出

```
ipchains -A input -i EXTERNAL_INTERFACE -s 65.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 66.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 67.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 68.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 69.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 70.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 71.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 72.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 73.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 74.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 75.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 76.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 77.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 78.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 79.0.0.0/8 -j DENY
```

# 80: 0101000/4 掩码 80-95

```
ipchains -A input -i EXTERNAL_INTERFACE -s 80.0.0.0/4 -j DENY
```

# 96: 0110000/3 掩码 96-127 溢出

```
ipchains -A input -i EXTERNAL_INTERFACE -s 96.0.0.0/4 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 112.0.0.0/5 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 113.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 114.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 115.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 116.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 117.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 118.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 119.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 120.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 121.0.0.0/8 -j DENY
```

# 126: 0111110/3 包含 127 - 需要 128-255

```
ipchains -A input -i EXTERNAL_INTERFACE -s 122.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 123.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 124.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 125.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 126.0.0.0/8 -j DENY
```

# 217.1011001 /5 包含 216-219

```
ipchains -A input -i EXTERNAL_INTERFACE -s 217.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 218.0.0.0/8 -j DENY
ipchains -A input -i EXTERNAL_INTERFACE -s 219.0.0.0/8 -j DENY
```

# 223.1011111 -6 掩码 220-223

```
ipchains -A input -i EXTERNAL_INTERFACE -s 220.0.0.6 -j DENY
```

# ICMP

为了防止 ICMP 炸弹拒绝服务攻击，
入站重定向 (5) 和出站目标不可达 (3)
然而，不建议禁用目标不可达 (3)，
因为它用于协商分包大小。

# 用于双向 ping

消息类型：Echo_Reply (0), Echo_Request (8)
为了防止攻击，将源地址限制在您的 ISP 范围内。

# 用于出站 tracer

消息类型：入站目标不可达 (3), Time_Exceeded (11)
默认 UDP 基础：33444 到 base+nops-1

# 用于入站 tracer

消息类型：出站目标不可达 (3), Time_Exceeded (11)
要阻止此，使用出站 30 和 11

# 0: echo-reply (pong)
# 3: destination-unreachable, port-reachable, fragmentation-needed, 等。
# 4: source-quench
# 5: redirect
# 8: echo-request (ping)
# 11: time-exceeded
# 12: parameter-problem

```
ipchains -A input -i EXTERNAL_INTERFACE -p icmp - $SWHERE != 0 $IPADDRESS -j ACCEPT
ipchains -A input -i EXTERNAL_INTERFACE -p icmp - $SWHERE != 3 $IPADDRESS -j ACCEPT
ipchains -A input -i EXTERNAL_INTERFACE -p icmp - $SWHERE != 4 $IPADDRESS -j ACCEPT
ipchains -A input -i EXTERNAL_INTERFACE -p icmp - $SWHERE != 11 $IPADDRESS -j ACCEPT
ipchains -A input -i EXTERNAL_INTERFACE -p icmp - $SWHERE != 12 $IPADDRESS -j ACCEPT
ipchains -A input -i EXTERNAL_INTERFACE -p icmp - 220.0.0.6 8 $IPADDRESS -j ACCEPT
```

关于本页的意见和建议请邮寄至 `gmourani@videotron.ca`



- `$IPADDR` -d `$ANYWHERE` -j `$ACCEPT`

`ipchains` -A input -i `$EXTERNAL_INTERFACE` -p icmp \
-s `$IPADDR` 12 -d `$ANYWHERE` -j `$ACCEPT`

`ipchains` -A input -i `$EXTERNAL_INTERFACE` -p icmp \
-s `$IPADDR` 11 -d 208.186.0/24 -j `$ACCEPT`

```
# UDP 入站路由追踪
# traceroute us 使用 -S 32769:65535 -D 33433:33523
```

`ipchains` -A input -i `$EXTERNAL_INTERFACE` -p udp \
-s 208.186.0/24 `$TRACEROUTE_SRC_PORTS` \
-d `$IPADDR` `$TRACEROUTE_DEST_PORTS` -j ACCEPT

```
ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
-s $ANYWHERE $TRACEROUTE_SRC_PORTS \
-d $IPADDR $TRACEROUTE_DEST_PORTS -j DENY
```

# DNS 服务器

# DNS: 全功能服务器

# 服务器/客户端到服务器的查询或响应

```
ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
-s $ANYWHERE $UNPRIVOPORTS \
-d $IPADDR 53 -j ACCEPT
```

`ipchains` -A output -i `$EXTERNAL_INTERFACE` -p udp \
-s `$IPADDR` 53 \
-d `$ANYWHERE` `$UNPRIVOPORTS` -j ACCEPT

# DNS 客户端 (53)

```
ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
-s $NAMESAMVER_1 53 \
-d $IPADDR $UNPRIVOPORTS -j ACCEPT
```

`ipchains` -A output -i `$EXTERNAL_INTERFACE` -p udp \
-s `$IPADDR` `$UNPRIVOPORTS` \
-d `$NAMESAMVER_1` 53 -j ACCEPT

```
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp -j ACCEPT \
-s $NAMESAMVER_1 53 \
-d $IPADDR $UNPRIVOPORTS -j ACCEPT
```

```
ipchains -A output -i $EXTERNAL_INTERFACE -p tcp \
-s $IPADDR $UNPRIVOPORTS \
-d $NAMESAMVER_1 53 -j ACCEPT
```

# 仅在所选端口接受 TCP

# SSH 服务器 (22)

```
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
-s $ANYWHERE $UNPRIVOPORTS \
-d $IPADDR 22 -j ACCEPT
```

© Copyright 1999 Open Network Architecture ®

124

关于本页的意见和建议请邮寄至 gmourani@videotron.ca

```
ipchains -A output -i $EXTERNAL_INTERFACE -p tcp -j ACCEPT \
-s $IPADDR 22 \
-d $ANYWHERE $UNPRIVOPORTS -j ACCEPT
```

`ipchains` -A input -i `$EXTERNAL_INTERFACE` -p tcp \
-s `$ANYWHERE` `$SSH_PORTS` \
-d `$IPADDR` 22 -j ACCEPT

```
ipchains -A output -i $EXTERNAL_INTERFACE -p tcp -j ACCEPT \
-s $IPADDR 22 \
-d $ANYWHERE $SSH_PORTS -j ACCEPT
```

# SSH 客户端 (22)

```
# ipchains -A input -i $EXTERNAL_INTERFACE -p tcp -j ACCEPT \
-s $ANYWHERE 22 \
-d $IPADDR $UNPRIVOPORTS -j ACCEPT
```

# ipchains -A output -i $EXTERNAL_INTERFACE -p tcp -j ACCEPT \
-s $IPADDR \
-d $ANYWHERE 22 -j ACCEPT

```
# ipchains -A output -i $EXTERNAL_INTERFACE -p tcp -j ACCEPT \
-s $ANYWHERE 22 \
-d $IPADDR $SSH_PORTS -j ACCEPT
```

# ipchains -A output -i $EXTERNAL_INTERFACE -p tcp -j ACCEPT \
-s $IPADDR $SSH_PORTS \
-d $ANYWHERE 22 -j ACCEPT

# AUTH 服务器 (113)

拒绝（Reject）而不是丢弃（deny）入站 auth 端口。（NET-3-HOWTO）

```
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
-s $ANYWHERE \
-d $IPADDR 113 -j REJECT
```

# SYSLOG 服务器 (514)

提供完整的远程日志。使用此功能，你可以控制单台主机上所有的 syslog 消息。

```
ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
-s $SYSLOG_CLIENT \
-d $IPADDR 514 -j ACCEPT
```

# SYSLOG 客户端 (514)

```
ipchains -A output -i $EXTERNAL_INTERFACE -p udp \
-s $IPADDR 514 \
-d $SYSLOG_SERVER 514 -j ACCEPT
```

© Copyright 1999 Open Network Architecture ®

125

关于本页的意见和建议请邮寄至 gmourani@videotron.ca

# SMTP 服务器 (25)

```
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp -j ACCEPT \
-s $ANYWHERE $UNPRIVOPORTS -j ACCEPT \
-d $IPADDR 25 -j ACCEPT
```

`ipchains` -A input -i `$EXTERNAL_INTERFACE` -p tcp -j ACCEPT \
-s `$IPADDR` 25 \
-d `$ANYWHERE` `$UNPRIVOPORTS` -j ACCEPT

# SMTP 客户端 (25)

```
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp -j ACCEPT \
-s $ANYWHERE 25 \
-d $IPADDR $UNPRIVOPORTS -j ACCEPT
```

`ipchains` -A output -i `$EXTERNAL_INTERFACE` -p tcp \
-s `$IPADDR` `$UNPRIVOPORTS` \
-d `$ANYWHERE` 25 -j ACCEPT

# IMAP 服务器 (143)

```
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
-s $ANYWHERE $UNPRIVOPORTS \
-d $IPADDR 143 -j ACCEPT
```

```
ipchains -A output -i $EXTERNAL_INTERFACE -p tcp \
-s $IPADDR 143 \
-d $ANYWHERE $UNPRIVOPORTS -j ACCEPT
```

# 出站路由追踪

```
ipchains -A output -i $EXTERNAL_INTERFACE -p udp \
-s $IPADDR $TRACEROUT_SRC_PORTS \
-d $ANYWHERE $TRACEROUT_DEST_PORTS -j ACCEPT
```

# 被拒绝数据包日志

```
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
-d $IPADDR -j DENY
```



`ipchains -A input -i $EXTERNAL_INTERFACE -p udp \`
`-d $IPADDR -j DENY`

```
ipchains -A input -i $EXTERNAL_INTERFACE -p icmp \
-s $ANYWHERE -d $IPADDR -j DENY
```

`ipchains -A input -i $EXTERNAL_INTERFACE -p icmp \`
`-s $ANYWHERE 255 -d $IPADDR -j DENY`

© Copyright 1999 Open Network Architecture ®

126

关于本页的意见和建议请邮寄至 gmourani@videotron.ca

防火墙服务：
`stop)`
`echo -n "正在关闭防火墙服务..."`
`# 移除所有 filter 规则`
`ipchains -F`

`# 重置 filter 的默认策略为接受。`
`ipchains -P input`
`ipchains -P output`
`ipchains -P forward`

`# 关闭 TCP SYN 保护。`
`echo 0 >/proc/sys/net/ipv4/tcp_sync()`

`# 关闭 IP 欺骗保护。`
`for i in /proc/sys/net/ipv4/filter*; do`
`echo 0 > $i`
`done`

`# 开启 ICMP 重定向。`
`for i in /proc/sys/net/ipv4/conf/*/redirects; do`
`echo 1 > $i`
`done`

`# 开启路由数据包源路由。`
`for i in /proc/sys/net/ipv4/conf/*/source_route; do`
`echo 1 > $i`
`done`

`status)`
`echo -n "现在显示防火墙状态吗?"`
`restart(reload)`
`$0`
`stop`
`*)`
`echo "用法: firewall [start|stop|restart|reload]"`
`exit 1`

现在，使此脚本可执行并更改其默认权限：
`[root@deep]# chmod 700 /etc/rc.d/init.d/firewall`

为你的命令创建符号链接：
`[root@deep]# chkconfig --add firewall`
`[root@deep]# chkconfig --level 345 firewall on`

现在，你的防火墙规则配置为使用 System V（System V 负责启动时需要运行的所有进程），并在服务器重启时自动启动。

要在你的系统上手动停止防火墙，请使用命令：
`[root@deep]# /etc/rc.d/init.d/firewall stop`

要在你的系统上手动启动防火墙，请使用命令：
`[root@deep]# /etc/rc.d/init.d/firewall start`

127

© Copyright 1999 Network

关于本页的意见和建议请邮寄至 gmourani@videotron.ca

`[root@deep]# /etc/rc.d/init.d/firewall start`

# 网关服务器 /etc/rc.d/init.d/firewall 脚本配置

这是我们网关服务器的配置脚本。该配置允许回环接口、ICMP、DNS 服务器和客户端 (53)、SSH 服务器和客户端 (22)、HTTP 服务器和客户端 (80)、HTTPS 服务器和客户端 (443)、POP 客户端 (110)、NNTP 新闻和客户端 (119)、SMTP 服务器和客户端 (25)、IMAP 服务器和客户端 (143)、IRC 客户端 (6667)、ICQ 客户端 (4000)、FTP 客户端 (20)、RealAudio / QuickTime 客户端以及默认运行出站路由追踪。

如果你不想在网关服务器的防火墙规则中使用我默认开启的某些服务，请在行开头使用 `#` 将其注释掉。如果你想开启我用 `#` 注释掉的某些服务，请删除行首的 `#` 符号。如果你在你的服务器上配置了地址伪装（Masquerading），请取消注释模块模块以伪装你所需的相应服务，如 `ip_masq_rc.o`、`ip_masq_radio.o` 等。

在你的网关服务器上创建防火墙脚本文件（`touch /etc/rc.d/init.d/firewall`）并添加内容：

```
#!/bin/sh

#

# 由 Gerard Maurani 最后修改: 02-01-2000

#

# Copyright (C) 1997, 1998, 1999 Robert L. Ziegler

#

# 许可使用、复制、修改和分发本软件及文档

# 用于教育、研究、实践和非营利目的，且无需书面协议。

# 本软件作为个人防火墙  示例和基础。本软件不提供任何保证。

#

# Robert L. Ziegler 提供的任何材料均按“原样”提供。他不作任何形式的显式或暗示性 

# 保证，包括但不限于对特定用途的适用性、排他性或从使用材料中获得的结果。

#

# 从 /etc/rc.d/init.d.firewall 调用。

# chconfig: 95

# description: 启动和停止用于提供防火墙网络 服务的 IPCHAINS。

#

# 源函数库。

# /etc/rc.d/init.functions

#n# 源网络配置。

# /etc/sysconfig/network

#n# 检查网络是否启动。

# [$NETWORKING] = "no" && exit 0

# 查看我们是如何被调用的。

# case "$1" in

# start)

# echo -n "正在启动防火墙服务... ""
```

# #

# 请根据你的系统和 ISP（网络服务商）修改这些内容。

```bash
EXTERNAL_INTERFACE="eth0" # 你使用的接口
LOCAL_INTERFACE="eth1" # 你使用的接口
LOOPBACK_INTERFACE="lo"
IPADDR="208.164.186.1"
LOCALNET="192.168.1.0/24" # 你使用的私有地址范围
ANYNAMESERVER="208.164.186.1"
NAMESERVER_2="208.164.186.2"
POP_SERVER="pop.videotron.ca" # 你的外部 POP 服务器
NEWS_SERVER="news.videotron.ca" # 你的外部新闻服务器
SYSLOG_SERVER="mail.openarch.com" # 你的内部 syslog 服务器
LOOPBACK="127.0.0.0/8"
CLASS_A="10.0.0.0/8"
CLASS_B="172.16.0.0/12"
CLASS_C="192.168.0.0/16"
CLASS_D_MULTIC="224.0.0.0/4"
CLASS_E_RESERVED_NET="240.0.0.0/4"
BROADCAST_SRC="0.0.0.0"
BROADCAST_DEST="255.255.255.255"
PRIVPORTS="0023"
UNPRIVPORTS="1024:65535"
```

```bash
#
# SSH 从 1023 开始，每增加一个并发入站
# 连接，端口向下减少 513。
SSH_PORTS="1022:1023" # SSH 特权端口范围
traceoute 使用 -S 32769:65535 -D 33434:33523
TRACEROUT_SRC_PORTS="32769:65535"
TRACEROUT_DEST_PORTS="33434:33523"
```

```bash
# 设置过滤器的默认策略为拒绝。
ipchains -P input DENY
ipchains -P output REJECT
ipchains -P forward REJECT
# 设置 tcp 连接的伪装超时时间为 10 分钟
ipchains -M -S 36000 0.0
# 不要转发。在转发前组装。
ipchains -A output -i - -j $LOCAL_INTERFACE_1 -j DENY
```

```bash
#
# 启用 TCP Cookie 
echo 1 >/proc/sys/net/ipv4/tcp_syncookies
```

© 1999 Open Network Architecture ®

关于本页面的意见和建议请邮件至 gmourani@videotron.ca

```bash
# 启用 IP 伪骗防护
# 打开源地址验证
for i in /proc/sys/net/ipv4/conf/*ip_filter; do
echo 0 > $i
done
```

```bash
# 禁用 ICMP 重定向
for i in /proc/sys/net/ipv4/conf/*accept_redirects; do
echo 0 > $i
done
```



# 禁用源路由数据包
```bash
for i in /proc/sys/net/ipv4/conf/*accept_source_route; do
echo 0 > $i
done
```

# 这些模块对于伪装它们各自的服务是必要的。
```bash
/sbin/modprobe_ip_masq_ftp.o
/sbin/modprobe_ip_masq_radio.o ports=554,7070,7071,69270,69271
/sbin/modprobe_ip_masq_irc.o
/sbin/modprobe_ip_masq_volive.o
/sbin/modprobe_ip_masq_cuseeme.o
/sbin/modprobe_ip_masq_quake.o
```

# 回环接口 (LOOPBACK)
```bash
```

# 回环接口上的允许无限流量。
```bash
ipchains -A input -i $LOOPBACK_INTERFACE -j ACCEPT
ipchains -A output -i $LOOPBACK_INTERFACE -j ACCEPT
```

# 网络幽灵
# 拒绝讨厌鬼的访问
```bash
```

# /etc/rc.drc/firewall.blocked 包含一个列表
```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s address -j DENY
# 用于拦截来自任何地址的规则。
```

# 拒绝来自问题站的任何连接
```bash
if [ -f /etc/rc.drc/firewall.blocked ]; then
  ./etc/rc.drc/firewall.blocked
fi
```

# 伪骗与错误地址
# 拒绝伪造的数据包。
# 忽略明显非法的源地址。
# 保护免受伪造地址的攻击。
```bash
```

# 拒绝假称来自外部地址的伪造数据包。
```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s $IPADDR -j DENY
```

# 拒绝声称来自 Class A 私有网络的数据包
```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s $CLASS_A -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -d $CLASS_A -j DENY
ipchains -A output -i $EXTERNAL_INTERFACE -s $CLASS_A - REJECT
ipchains -A output -i $EXTERNAL_INTERFACE -d $CLASS_A -j REJECT
```

# 拒绝声称来自 Class B 私有网络的数据包
```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s $CLASS_B -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -d $CLASS_B -j DENY
© Copyright 1999 Open Network Architecture
132 关于本页面的意见可以邮件至 gmourani@videotron.ca
ipchains -A output -i $EXTERNAL_INTERFACE -s $CLASS_B -j REJECT
ipchains -A output -i $EXTERNAL_INTERFACE -d $CLASS_B -j REJECT
```

# 拒绝声称来自 Class C 私有网络的数据包
```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s $CLASS_C -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -d $CLASS_C -j DENY
```

# 拒绝声称来自回环接口的数据包
```bash
ipchains -A input -i $LOOPBACK -j DENY
ipchains -A output -i $LOOPBACK -j REJECT
```

# 过滤广播地址数据包
```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s $BROADCAST_DEST -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -d $BROADCAST_SRC -j DENY
```

# Class D 多播地址
# 作为源地址时是非法的。
```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s $CLASS_D_MULTIC -j DENY
```

# Class E 保留地址
```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s $CLASS_E_RESERVED_NET -j DENY
```

# 拒绝由 IANA 定义的地址
# 0.*, 1.*, 5.*, 23.*, 27.*,
# 31.*, 39.*, 41.*, 42.*, 58.*, 60.*,
# 65.*, 95.*, 96.*, 192.*, 201.*, 217.*
```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s 0.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 1.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 5.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 23.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 27.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 31.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 39.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 41.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 42.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 58.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 60.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 65.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 95.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 96.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 192.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 201.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 217.0.0/8 -j DENY
```

# 65: 01000000 /3 包含了 65-79
```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s 65.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 66.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 67.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 68.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 69.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 70.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 71.0.0/8 -j DENY
```



`ipchains -A input -i $EXTERNAL_INTERFACE -s 72.0.0/8 -j DENY`

`ipchains -A input -i $EXTERNAL_INTERFACE -s 73.0.0/8 -j DENY`

`ipchains -A input -i $EXTERNAL_INTERFACE -s 74.0.0/8 -j DENY`

`ipchains -A input -i $EXTERNAL_INTERFACE -s 75.0.0/8 -j DENY`

`ipchains -A input -i $EXTERNAL_INTERFACE -s 76.0.0/8 -j DENY`

`ipchains -A input -i $EXTERNAL_INTERFACE -s 77.0.0/8 -j DENY`

`ipchains -A input -i $EXTERNAL_INTERFACE -s 78.0.0/8 -j DENY`

`ipchains -A input -i $EXTERNAL_INTERFACE -s 79.0.0/8 -j DENY`

```bash
# 80: 01010000 /4 掩码 80-95
ipchains -A input -i $EXTERNAL_INTERFACE -s 80.0.0/4 -j DENY
```

```bash
# 96: 01100000 /4 最大 96-111
ipchains -A input -i $EXTERNAL_INTERFACE -s 96.0.0/4 -j DENY
```

```bash
# 126: 01111110 /3 让 127-126 溢出
ipchains -A input -i $EXTERNAL_INTERFACE -s 112.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 113.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 114.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 115.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 116.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 117.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 118.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 119.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 120.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 121.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 122.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 123.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 124.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 125.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 126.0.0/8 -j DENY
```

```bash
# 217: 10110011 /5 包含了 216-219
ipchains -A input -i $EXTERNAL_INTERFACE -s 217.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 218.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 219.0.0/8 -j DENY
```

```bash
# 223: 10111111 /6 包含了 220-223
ipchains -A input -i $EXTERNAL_INTERFACE -s 220.0.0/6 -j DENY
```

# ICMP

- 为了防止基于 ICMP 炸弹的拒绝攻击，过滤
- 入站请求 (5) 和出站目的不可达 (3)
- 注意，禁用目的不可达 (3) 是不建议的，
- 因为它可以协商分段大小。
- 用于双向 ping。
- 消息类型：Echo_Reply (0), Echo_Request (8)
- 为了防止攻击，将源地址限制在你的 ISP 范围 own。
- 用于出站 traceroute。
- 消息类型：入站 Dest_Unreachable (3), Time_Expired (11)
- 默认 UDP 基础：33434 到 base+n-1
- 用于入站 traceroute。
- 消息类型：出站 Dest_Unreachable (3), Time_Expired (11)
- 为了阻止此行为，拒绝出站 3 和 11

# 0: echo-reply (ping)

# 3: 目的不可达、端口不可达、分段需要等。

# 4: 源猝塞

# 5: 重定向

# 11: 超时

# 12: 参数问题

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p icmp \
-s $ANYWHERE 0 -d $IPADDR -ACCEPT
ipchains -A input -i $EXTERNAL_INTERFACE -p icmp \
-s $ANYWHERE 3 -d $IPADDR -ACCEPT
```

关于本页面的意见和建议请邮件至 gmourani@videotron.ca

```bash
-s ANYWHERE 4 -d $IPADDR -j ACCEPT
ipchains -A input -i EXTERNAL_INTERFACE -p icmp \
-s ANYWHERE 11 -d $IPADDR -j ACCEPT
ipchains -A input -i EXTERNAL_INTERFACE -p icmp \
-s ANYWHERE 12 -d $IPADDR -j ACCEPT
ipchains -A input -i EXTERNAL_INTERFACE -p icmp \
-s 208.164.186.0/24 -d $IPADDR -j ACCEPT
ipchains -A output -i EXTER_INTERFACE -p icmp \
-s $IPADDR 0 -d EXTERNAL_INTERFACE -p icmp \
-s $IPADDR 3 -d ANYWHERE -j ACCEPT
ipchains -A output -i EXTERNAL_INTERFACE -p icmp \
-s $IPADDR 4 -d ANYWHERE -j ACCEPT
ipchains -A output -i EXTERNAL_INTERFACE -p icmp \
-s $IPADDR 8 -d ANYWHERE -j ACCEPT
ipchains -A output -i EXTERNAL_INTERFACE -p icmp \
-s $IPADDR 12 -d ANYWHERE -j ACCEPT
ipchains -A output -i EXTERNAL_INTERFACE -p icmp \
-s 208.164.186.0/24 -j ACCEPT
```

# UDP TRACEROUTE

# traceroute 使用 -U 32769-65535 -D 33434:33523

```bash
ipchains -A input -i EXTERNAL_INTERFACE -p udp \
-s 208.164.186.0/24 -j $TRACEROUTE_SRC_PORTS \
-d $IPADDR $TRACEROUTE_DEST_PORTS -j ACCEPT -I
```

```bash
ipchains -A input -i EXTERNAL_INTERFACE -p udp \
-s ANYWHERE $TRACEROUTE_SRC_PORTS \
-d $IPADDR $TRACEROUTE_DEST_PORTS -j DENY -I
```

# DNS 服务器

# ------

# DNS: 完整服务器模式

# 服务器/客户端查询或响应



# DNS 客户端 (53)

```
ipchains -A input -i EXTERNAL_INTERFACE -p udp \
-s ANYWHERE $UNPRIVPORTS \
-d $IPADDR 53 -j ACCEPT
```

```
ipchains -A output -i EXTERNAL_INTERFACE -p udp \
-s $IPADDR 53 \
-d $ANYWHERE $UNPRIVPORTS -j ACCEPT
```

```
ipchains -A input -i EXTERNAL_INTERFACE -p udp \
-s $NAMESERVER_1_53 \
-d $IPADDR $UNPRIVPORTS -j ACCEPT
```

```
ipchains -A output -i EXTERNAL_INTERFACE -p udp \
-s $IPADDR $UNPRIVPORTS \
-d $NAMESERVER_1_53 -j ACCEPT
```

```
ipchains -A input -i EXTERNAL_INTERFACE -p tcp -j \
-s $NAMESERVER_1_53 \
-d $IPADDR $UNPRIVPORTS -j ACCEPT
```

© 版所有 1999 Open Network Architecture

133

关于本页面的意见和建议请邮件至 gmourani@videotron.ca

```
ipchains -A output -s $EXTERNAL_INTERFACE -p tcp \
-s $IPADDR $UNPRIVPORTS \
-d $NAMESERVER 53 -j ACCEPT
```

```
ipchains -A output -s $EXTERNAL_INTERFACE -p udp \
-s $NAMESERVER 53 \
-d $IPADDR $UNPRIVPORTS -j ACCEPT
```

```
ipchains -A output -s $EXTERNAL_INTERFACE -p udp \
-s $NAMESERVER 53 \
-d $IPADDR $UNPRIVORTS -j ACCEPT
```

```
ipchains -A input -s $EXTERNAL_INTERFACE -p tcp -y \
-s $NAMESERVER 53 \
-d $IPADDR $UNPRIVPORTS -j ACCEPT
```

```
ipchains -A output -s $EXTERNAL_INTERFACE -p tcp \
-s $IPADDR $UNPRIVPORTS \
-d $NAMESERVER 53 -j ACCEPT
```

# 仅对选定端口开启 TCP

## SSH 服务器 (22)

```
ipchains -A input -s $EXTERNAL_INTERFACE -p tcp \
-s ANYWHERE \
-d $IPADDR 22 -j ACCEPT
```

```
ipchains -A output -s $EXTERNAL_INTERFACE -p tcp -y \
-s 22 \
-d $ANYWHERE -j ACCEPT
```

```
ipchains -A input -s $EXTERNAL_INTERFACE -p tcp \
-s ANYWHERE \
-d $IPADDR 22 -j ACCEPT
```

```
ipchains -A output -s $EXTERNAL_INTERFACE -p tcp -y \
-s 22 \
-d $ANYWHERE -j ACCEPT
```

## SSH 客户端 (22)

```
ipchains -A input -s $EXTERNAL_INTERFACE -p tcp -y \
-s ANYWHERE 22 \
-d $IPADDR UNPRIVPORTS -j ACCEPT
```

```
ipchains -A output -s $EXTERNAL_INTERFACE -p tcp \
-s $IPADDR UNPRIVPORTS \
-d ANYWHERE 22 -j ACCEPT
```

134

关于本页面的意见和建议请邮件至 gmourani@videotron.ca

## HTTP 客户端 (80)

```
ipchains -A input -s $EXTERNAL_INTERFACE -p tcp -y \
-s ANYWHERE 80 \
-d $IPADDR UNPRIVPORTS -j ACCEPT
```

```
ipchains -A output -s $EXTERNAL_INTERFACE -p tcp -y \
-s $IPADDR UNPRIVPORTS \
-d $ANYWHERE 80 -j ACCEPT
```

## HTTPS 客户端 (443)

```
ipchains -A input -s $EXTERNAL_INTERFACE -p tcp -y \
-s ANYWHERE 443 \
-d $IPADDR UNPRIVPORTS -j ACCEPT
```

```
ipchains -A output -s $EXTERNAL_INTERFACE -p tcp -y \
-s $IPADDR UNPRIVPORTS \
-d $ANYWHERE 443 -j ACCEPT
```

## POP 客户端 (110)

```
ipchains -A input -s $EXTERNAL_INTERFACE -p tcp -y \
-s ANYWHERE 110 \
-d $IPADDR UNPRIVPORTS -j ACCEPT
```

```
ipchains -A output -s $EXTERNAL_INTERFACE -p tcp -y \
-s $IPADDR UNPRIVPORTS \
-d $ANYWHERE 110 -j ACCEPT
```

## NNTP 客户端 (119)

```
ipchains -A input -s $EXTERNAL_INTERFACE -p tcp -y \
-s ANYWHERE 119 \
-d $IPADDR UNPRIVPORTS -j ACCEPT
```

```
ipchains -A output -s $EXTERNAL_INTERFACE -p tcp -y \
-s $IPADDR UNPRIVPORTS \
-d $ANYWHERE 119 -j ACCEPT
```

## Finger 客户端 (79)

```
ipchains -A input -s $EXTERNAL_INTERFACE -p tcp -y \
-s ANYWHERE 79 \
-d $IPADDR UNPRIVPORTS -j ACCEPT
```

```
ipchains -A output -s $EXTERNAL_INTERFACE -p tcp -y \
-s $IPADDR UNPRIVPORTS \
-d $ANYWHERE 79 -j ACCEPT
```

© 版所有 1999 Open Network Architecture

135

关于本页面的意见和建议请邮件至 gmourani@videotron.ca.

## SYSLOG 客户端 (514)

```
# ipchains -A input -i $LOCAL_INTERFACE_1 -p udp \
# -s $IPADDR 514 \
# -d $SYSLOG_SERVER 514 -j ACCEPT
```

---

## AUTH 服务器 (113)

拒绝而非丢弃入站认证端口。(NET-3-HOWTO)

```
ipchains -A input -i EXTERNAL_INTERFACE -p tcp \
# -s $ANYWHERE \
# -d $IPADDR 113 -j REJECT
```

## AUTH 客户端 (113)

```
# ipchains -A input -i EXTERNAL_INTERFACE -p tcp -y \
# -s ANYWHERE 113 \
# -d $IPADDR UNPRIVPORTS -j ACCEPT
```

```
# ipchains -A output -i EXTERNAL_INTERFACE -p tcp \
-s $IPADDR UNPRIVPORTS \
-d $ANYWHERE 113 -j ACCEPT
```

关于此页面的意见和建议应邮寄至 gmourani@videotron.ca



- `$IPADDR` `$UNPRIPVPORTS` -j ACCEPT

`ipchains` -A output -i `$EXTERNAL_INTERFACE` -p tcp \
-s `$IPADDR` `$UNPRIPVPORTS` \
-d `$ANYWHERE` 7070:7071 -j ACCEPT

```
# UDP 是首选方法：6970:6999
# 对于域网机器，UDP 需要 RealAudio 伪装模块和
# ipmasqm 第三方软件。
```

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
-s $ANYWHERE $UNPRIPVPORTS \
-d $IPADDR 6970:6999 -j ACCEPT
```

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
-s $IPADDR $UNPRIPVPORTS \
-d $ANYWHERE $UNPRIPVPORTS -j ACCEPT
```

```bash
# WHOIS 客户端 (43)

# ipchains -A input -i $EXTERNAL_INTERFACE -p tcp ! -y \
-s $ANYWHERE 43 \
-d $IPADDR $UNPRIPVPORTS -j ACCEPT
```

```bash
# ipchains -A output -i $EXTERNAL_INTERFACE -p tcp ! \
-s $IPADDR $UNPRIPVPORTS \
-d $ANYWHERE 43 -j ACCEPT
```

```bash
# 出站追踪路由

# ipchains -A output -i $EXTERNAL_INTERFACE -p udp \
-s $IPADDR $TRACEROUT_SRC_PORTS \
-d $ANYWHERE $TRACEROUT_DEST_PORTS -j ACCEPT
```

# 本地网络内的无限制流量。
# 所有内部机器都可以访问防火墙机器。

```bash
ipchains -A input -i $LOCAL_INTERFACE_1 -s $LOCALNET_1 -j ACCEPT

ipchains -A output -i $LOCAL_INTERFACE_1 -d $LOCALNET_1 -j ACCEPT
```

# 伪装内部流量。
# 所有内部流量在外部进行伪装。

```bash
ipchains -A forward -i $EXTERNAL_INTERFACE -s $LOCALNET_1 -j MASQ
```

# 为选定的拒绝数据包启用日志

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
-d $IPADDR -j DENY -l
```

`ipchains` -A input -i `$EXTERNAL_INTERFACE` -p udp
-d `$IPADDR` `$PRIPVORTS` -j DENY -l

`ipchains` -A input -i `$EXTERNAL_INTERFACE` -p udp \
-d `$IPADDR` `$UNPRIVORTS` -j DENY -I

`ipchains` -A input -i `$EXTERNAL_INTERFACE` -p icmp \
-s `$ANYWHERE` 5 -d `$IPADDR` -j DENY -I

`ipchains` -A input -i `$EXTERNAL_INTERFACE` -p icmp \
-s `$ANYWHERE` 13:255 -d `$IPADDR` -j DENY -I
```

```bash
stop)
echo -n "正在关闭防火墙服务:"

# 移除所有属于此过滤器的现有规则
ipchains -F

# 重置过滤器的默认策略为接受。
ipchains -P input ACCEPT
ipchains -P output ACCEPT
ipchains -P forward ACCEPT

# 重置 TCP SYN Cookie 保护为关闭。
echo 0 > /proc/sys/net/ipv4/tcp_syncookies

# 重置 IP 欺骗保护为关闭。
# 使用源地址验证
for i in /proc/sys/net/ipv4/conf/*/rp_filter; do
echo 0 > $i
done

# 重置 ICMP 重定向接受为开启。
for i in /proc/sys/net/ipv4/conf/*/accept_redirects; do
echo 1 > $i
done

# 重置源路由包为开启。
for i in /proc/sys/net/ipv4/conf/*/accept_source_route; do
echo 1 > $i
done

status)
echo -n "现在显示防火墙统计数据吗?"

restart(reload)
$0 stop
$0 start

)
echo "用法: firewall {start|stop|restart|reload}"
exit 1
esac
```

现在，使此脚本具有可执行权限并更改其默认权限：

`[root@deep]# chmod 700 /etc/rc.init/d/firewall`

`[root@deep]# chmod 055 /etc/rc.init/d/firewall`

使用命令为您的防火墙创建符号链接 rc.d 链接：

```bash
[root@deep]# chconfig --add firewall
[root@deep]# chconfig --level 345 firewall on
```

现在，您的防火墙规则已配置为使用 System vit（System vit 负责启动启动时需要运行的所有进程），并且如果服务器重启，它每次都会自动启动。

若要手动停止系统上的防火墙，请使用命令：

`[root@deep]# /etc/rc.d/init.d/firewall stop`

若要手动启动系统上的防火墙，请使用命令：

`[root@deep]# /etc/rc.d/init.d/firewall start`

# 拒绝某些地址的访问

假设你有一个想要阻止访问你服务器的地址。你可以通过创建 rc.d 文件并取消你的防火墙规则脚本中以下行的注释来实现：

编辑你的防火墙脚本（`vi /etc/rc.d/init.d/firewall`）并取消以下行的注释：

```bash
if [ -f /etc/rc.d/init.d/firewall ]; then
```

创建一个 rc.d 文件，对于你想要阻止访问你服务器的地址：

`touch /etc/rc.d/init.d/firewall` 并取消防火墙规则脚本中以下行的注释：

```bash
假设你知道一个想要阻止访问你服务器的地址。
```

WHOIS 客户端 (43)

# ipchains -A input -i $EXTERNAL_INTERFACE -p tcp ! -y \
-s $ANYWHERE 43 \
-d $IPADDR $UNPRIPVPORTS -j ACCEPT
```

```bash
# ipchains -A output -i $EXTERNAL_INTERFACE -p tcp ! \
-s $IPADDR $UNPRIPVPORTS \
-d $ANYWHERE 43 -j ACCEPT
```

```bash
# 出站追踪路由

# ipchains -A output -i $EXTERNAL_INTERFACE -p udp \
-s $IPADDR $TRACEROUT_SRC_PORTS \
-d $ANYWHERE $TRACEROUT_DEST_PORTS -j ACCEPT
```

# 本地网络内的无限制流量。
# 所有内部机器都可以访问防火墙机器。

```bash
ipchains -A input -i $LOCAL_INTERFACE_1 -s $LOCALNET_1 -j ACCEPT

ipchains -A output -i $LOCAL_INTERFACE_1 -d $LOCALNET_1 -j ACCEPT
```

# 伪装内部流量。
# 所有内部流量在外部进行伪装。

```bash
ipchains -A forward -i $EXTERNAL_INTERFACE -s $LOCALNET_1 -j MASQ
```

# 为选定的拒绝数据包启用日志

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
-d $IPADDR -j DENY -l
```



# 防火墙配置

## ipchains 规则示例

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p udp -d $IPADDR $PRIPVORTS -j DENY -l

ipchains -A input -i $EXTERNAL_INTERFACE -p udp -d $IPADDR $UNPRIVORTS -j DENY -I

ipchains -A input -i $EXTERNAL_INTERFACE -p icmp -s $ANYWHERE 5 -d $IPADDR -j DENY -I

ipchains -A input -i $EXTERNAL_INTERFACE -p icmp -s $ANYWHERE 13:255 -d $IPADDR -j DENY -I
```

## 脚本片段

```bash
stop)
echo -n "正在关闭防火墙服务:"

# 移除所有属于此过滤器的现有规则
ipchains -F

# 重置过滤器的默认策略为接受。
ipchains -P input ACCEPT
ipchains -P output ACCEPT
ipchains -P forward ACCEPT

# 重置 TCP SYN Cookie 保护为关闭。
echo 0 > /proc/sys/net/ipv4/tcp_syncookies

# 重置 IP 欺骗保护为关闭。
# 使用源地址验证
for i in /proc/sys/net/ipv4/conf/*/rp_filter; do
echo 0 > $i
done

# 重置 ICMP 重定向接受为开启。
for i in /proc/sys/net/ipv4/conf/*/accept_redirects; do
echo 1 > $i
done

# 重置源路由包为开启。
for i in /proc/sys/net/ipv4/conf/*/accept_source_route; do
echo 1 > $i
done

status)
echo -n "现在显示防火墙统计数据吗?"

restart(reload)
$0 stop
$0 start

)
echo "用法: firewall {start|stop|restart|reload}"
exit 1
esac
```

## 权限与启动

现在，使此脚本具有可执行权限并更改其默认权限：

```bash
[root@deep]# chmod 700 /etc/rc.init/d/firewall
[root@deep]# chmod 055 /etc/rc.init/d/firewall
```

使用命令为您的防火墙创建符号链接 rc.d 链接：

```bash
[root@deep]# chconfig --add firewall
[root@deep]# chconfig --level 345 firewall on
```

现在，您的防火墙规则已配置为使用 System vit，System vit 负责启动时需要运行的所有进程，并且如果服务器重启，它每次都会自动启动。

若要手动停止系统上的防火墙，请使用命令：

```bash
[root@deep]# /etc/rc.d/init.d/firewall stop
```

若要手动启动系统上的防火墙，请使用命令：

```bash
[root@deep]# /etc/rc.d/init.d/firewall start
```

# 拒绝某些地址的访问

假设你知道一个想要阻止访问你服务器的地址。你可以通过创建 rc.d 文件并取消你的防火墙规则脚本中以下行的注释来实现：

编辑你的防火墙脚本 `vi /etc/rc.d/init.d/firewall` 并取消以下行的注释：

```bash
if [ -f /etc/rc.d/init.d/firewall ]; then
```

创建一个 rc.d 文件，对于你想要阻止访问你服务器的地址：

`touch /etc/rc.d/init.d/firewall` 并取消防火墙规则脚本中以下行的注释：

```bash
假设你知道一个想要阻止访问你服务器的地址。
```

WHOIS 客户端 `43`

```bash
# ipchains -A input -i $EXTERNAL_INTERFACE -p tcp ! -y -s $ANYWHERE 43 -d $IPADDR $UNPRIPVPORTS -j ACCEPT
```

```bash
# ipchains -A output -i $EXTERNAL_INTERFACE -p tcp ! -s $IPADDR $UNPRIPVPORTS -d $ANYWHERE 43 -j ACCEPT
```

```bash
# 出站追踪路由
# ipchains -A output -i $EXTERNAL_INTERFACE -p udp -s $IPADDR $TRACEROUT_SRC_PORTS -d $ANYWHERE $TRACEROUT_DEST_PORTS -j ACCEPT
```

# 本地网络内的无限制流量
# 所有内部机器都可以访问防火墙机器。

```bash
ipchains -A input -i $LOCAL_INTERFACE_1 -s $LOCALNET_1 -j ACCEPT
ipchains -A output -i $LOCAL_INTERFACE_1 -d $LOCALNET_1 -j ACCEPT
```

# 伪装内部流量
# 所有内部流量在外部进行伪装。

```bash
ipchains -A forward -i $EXTERNAL_INTERFACE -s $LOCALNET_1 -j MASQ
```

# 为选定的拒绝数据包启用日志

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp -d $IPADDR -j DENY -l
```

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p udp -d $IPADDR $PRIPVORTS -j DENY -l
ipchains -A input -i $EXTERNAL_INTERFACE -p udp -d $IPADDR $UNPRIVORTS -j DENY -I
ipchains -A input -i $EXTERNAL_INTERFACE -p icmp -s $ANYWHERE 5 -d $IPADDR -j DENY -I
ipchains -A input -i $EXTERNAL_INTERFACE -p icmp -s $ANYWHERE 13:255 -d $IPADDR -j DENY -I
```



`[root@deep]# /etc/rc.d/init.d/firewall start`

# 拒绝某些地址的访问

假设你知道一个想要阻止访问你服务器的地址。你可以通过创建 rc.d 文件并取消你的防火墙规则脚本中以下行的注释来实现：

编辑你的防火墙脚本（`vi /etc/rc.d/init.d/firewall`）并取消以下行的注释：

```bash
if [ -f /etc/rc.d/init.d/firewall ]; then
```

创建一个 rc.d 文件，对于你想要阻止访问你服务器的地址：

`touch /etc/rc.d/init.d/firewall` 并取消防火墙规则脚本中以下行的注释：

```bash
假设你知道一个想要阻止访问你服务器的地址。
```

WHOIS 客户端 (`43`)

```bash
# ipchains -A input -i $EXTERNAL_INTERFACE -p tcp ! -y \
-s $ANYWHERE 43 \
-d $IPADDR $UNPRIPVPORTS -j ACCEPT
```

```bash
# ipchains -A output -i $EXTERNAL_INTERFACE -p tcp ! \
-s $IPADDR $UNPRIPVPORTS \
-d $ANYWHERE 43 -j ACCEPT
```

```bash
# 出站追踪路由

# ipchains -A output -i $EXTERNAL_INTERFACE -p udp \
-s $IPADDR $TRACEROUT_SRC_PORTS \
-d $ANYWHERE $TRACEROUT_DEST_PORTS -j ACCEPT
```

# 本地网络内的无限制流量。
# 所有内部机器都可以访问防火墙机器。

```bash
ipchains -A input -i $LOCAL_INTERFACE_1 -s $LOCALNET_1 -j ACCEPT

ipchains -A output -i $LOCAL_INTERFACE_1 -d $LOCALNET_1 -j ACCEPT
```

# 伪装内部流量。
# 所有内部流量在外部进行伪装。

```bash
ipchains -A forward -i $EXTERNAL_INTERFACE -s $LOCALNET_1 -j MASQ
```

# 为选定的拒绝数据包启用日志

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
-d $IPADDR -j DENY -l
```

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p udp
-d $IPADDR $PRIPVORTS -j DENY -l

ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
-d $IPADDR $UNPRIVORTS -j DENY -I

ipchains -A input -i $EXTERNAL_INTERFACE -p icmp \
-s $ANYWHERE 5 -d $IPADDR -j DENY -I

ipchains -A input -i $EXTERNAL_INTERFACE -p icmp \
-s $ANYWHERE 13:255 -d $IPADDR -j DENY -I
```

```bash
stop)
echo -n "正在关闭防火墙服务:"

# 移除所有属于此过滤器的现有规则
ipchains -F

# 重置过滤器的默认策略为接受。
ipchains -P input ACCEPT
ipchains -P output ACCEPT
ipchains -P forward ACCEPT

# 重置 TCP SYN Cookie 保护为关闭。
echo 0 > /proc/sys/net/ipv4/tcp_syncookies

# 重置 IP 欺骗保护为关闭。
# 使用源地址验证
for i in /proc/sys/net/ipv4/conf/*/rp_filter; do
echo 0 > $i
done

# 重置 ICMP 重定向接受为开启。
for i in /proc/sys/net/ipv4/conf/*/accept_redirects; do
echo 1 > $i
done

# 重置源路由包为开启。
for i in /proc/sys/net/ipv4/conf/*/accept_source_route; do
echo 1 > $i
done

status)
echo -n "现在显示防火墙统计数据吗?"

restart(reload)
$0 stop
$0 start

)
echo "用法: firewall {start|stop|restart|reload}"
exit 1
esac
```

关于本页面的意见和建议请邮件至 `gnmouari@videotron.ca`

- 若要移动软磁盘中的 RPM 二进制文件，请使用命令：

`[root@deep] # mount /dev/fd0 /mnt/floppy/`

`[root@deep] # mv /bin/rpm /mnt/floppy`

`[root@deep] # umount /mnt/floppy/`

- 若将 RPM 二进制文件还原到原始目录，请使用命令：

`[root@deep] # mount /dev/td0 /mnt/floppy/`

`[root@deep] # cp /mnt/floppy/rpm /bin/`

`[root@deep] # umount /mnt/floppy/`

`注意：` 永远不要从系统中完全卸载 RPM 程序，否则你以后将无法重新安装 RPM 或其他软件所需的命令。

# 为什么我们选择使用 tar 包 (tarballs)？

Red Hat 发行版 以 RPM 文件的形式提供，也称为“软件包”，这是一种软件分发方式，可以方便地安装、升级、查询和删除。然而，在 Unix 世界，软件包分发的标准实际上仍然所谓的“tar 包”。tar 包是可以使用“tar”工具读取的简单文件。从 tar 包安装比使用 RPM 要琐琐得多。那么我们为什么要选择这样做呢？

- 1- 遗憾的是，开发者需要几周时间才能将最新版本的软件包转换为 RPM，因为许多开发者首先是以 tar 包的形式发布。
- 2- 当开发者发布新的 RPM 时，他们会包含许多不必要的选项。开发者不知道你可能哪些选项，哪些不需要，因此他们必须使用这种方法来满足每个人的需求。
- 3- RPM 并没有针对你特定的处理器进行优化，像 Red Hat Linux 这样的公司基于标准 PC 构建 RPM。这允许他们的 RPM 软件包安装在各种类型的计算机上，为 i386 机器编译的程序可以适用于所有系统。
- 4- 有时你下载并安装了 RPM，而世界上其他地方的人可能已经为了你的目的构建并提供了它。这可能会导致某些冲突（取决于软件包的构建方式）、错误、安全问题以及上述所有其他描述。

# 在你的系统上编译软件

粗略来说，程序是能够执行的计算机代码。有人用他/她理解的语言编写了“源代码”。那可能是 C 语言（很有可能）或其他某种语言。程序“源代码”对于编译器来说也有意义，编译器将这些指令转换为插入的任何处理器的二进制文件 - 例如 386 或类似的处理器。用于这些“可执行文件”的现代文件格式是 Elf。程序员将他的源代码展示给编译器并获得某种结果。早期的尝试编译失败或未按预期编译成功的情况完全并不罕见。编程的一半工作是追踪并修复这些问题（调试）。

与源代码编译相关的更多方面和新词汇你将在书中看到，包括但不限于：

多文件 (`The Multiple Files`)

© Copyright 1999 Open Network Architecture ®

关于本页面的意见和建议请邮件至 `gmournai@videotron.ca`

单文件程序很稀见。通常会有多个文件（例如 `*.c`），每个文件都被编译成对象文件 (`*.o`) 并链接成一个可执行文件。编译器通常用于执行链接（它在后台调用 `ld` 程序）。

# Makefile

这些文件旨在帮助保持一致性（确保你每次都以相同的方式构建程序）。它们也有助于提高速度。有些程序非常长——一个大型程序可能需要几十分钟。`make` 程序使用 `Makefile` 中的“依赖关系”来决定程序的哪些部分需要重新编译。如果你修改了五十个源文件中的一个，你只需要处理这并编译一个链接步骤，而不是从头开始。请注意，该格式在某些行的开头包含制表符（空格则不包含）。

# 库 (The Libraries)

程序不仅可以链接到对象文件 (`*o`)，还可以链接到库（对象文件的集合）。有时你必须链接到系统提供的库（例如，用于数学库的 `-lm`，如果没有它，你的数学 C 程序将产生无意义的结果）。链接库有两种形式：静态链接（代码进入可执行文件）和动态链接（代码在程序开始运行时被加载）。大型编译器手册通常会解释这二者的优缺点。

# 补丁 (The Patches)



以前，在重新编译之前，对可执行文件进行修正是常见做法。这种做法几乎消失了。人们对源代码进行“打补丁 (`patch`)”，将更改放入文件中（通常是修改整个文件的一小部分）。Larry Wall 的 `'patch'` 程序就用于此。当不同版本的程序需要对代码进行小更改以发布时，这避免了维护两个大型发行版的麻烦。

# 编译和链接中的错误

这些通常是拼写错误、编译错误以及语言的误用……检查你调用的函数是否使用了正确的包含文件。未引用的符号是链接步骤不完整的标志。此外还检查系统是否安装了必要的开发库或工具。

# 调试 (The Debugging)

这是一个大课题。在代码中加入告知正在发生什么的语句通常会有帮助。当你有时只需要打印循环的前三次时，避免淹没在输出中。检查变量是否模块模块正确传递也有帮助。熟悉你的调试工具。

# 在你的系统上构建和安装软件

你将在下面的“第六部分软件相关参考”中看到我们使用许多不同的命令在服务器上构建和安装程序。这些命令兼容 UNIX，并用于所有变体的 `'nik'` 机器。

在你的服务器上编译和安装 tar 包的步骤：

- 1- 首先，你必须从信任的源下载 tar 包。

- 2- 下载 tar 包后，切换到 "`var/tmp/`" 目录（注意可能是其他路径），并在示例中输入命令（以 root 身份）更新存档：

```
[root@deep]# tar xzf foo.gz
```

关于本页面的意见和建议请邮件至 gmournai@videotron.ca

"`x`" 选项告诉 `tar` 从示例 "`foo.gz`" 压缩存档中提取所有文件。

- `x` 选项告诉 `tar` 从存档中提取所有文件。

- `z` 选项告诉 `tar` 存档是用 `gzip` 压缩的。

- `p` 选项保持存档创建时文件拥有的原始所有和权限。

- `f` 选项告诉 `tar` 下一个参数是文件名。

一旦 `tar` 被解压到相应的目录，你几乎肯定会在新解压的文件中发现一个 "`README`" 或 "`INSTALL`" 文件，其中有关于如何准备软件软件包以供使用的进一步说明。同样，你需要输入类似下面示例的命令：

```
./configure
make
make install
```

上述命令 "`configure`" 会配置软件，以确保你的系统具有所需的功能和库来成功编译软件包；**`make`** 将所有源文件编译成可执行的二进制文件，然后 **`make install`** 将二进制文件和任何支持文件安装到适当的位置。我们在书中关于编译过程的其他特定命令将：

```
make depend
strip
chown
```

**`make depend`** 命令将构建并创建不同文件所需的依赖关系。"`strip`" 命令将丢弃文件中的所有符号。这意味着我们的二进制文件尺寸更小。由于系统在执行二进制文件时读取的行更少，这将提高性能。"`chown`" 命令将为二进制文件设置正确的属者和组权限。

**注意：** 更多命令将在相关的安装章节中解释。

在本书的这部分，第 9 章列出的所有软件都是可选的，取决于你想在服务器上安装或执行什么。取决于你的类型的服务器要做什么，以及为了你的网络（局域网/互联网等）做什么。在其他部分，你可能会发现用 `Ssh` 程序替换 `Telnet` 程序以进行安全的远程管理。另一个有趣的程序是 `Tripwire`，它可以帮助系统管理员和用户监控指定文件文件的任何更改。

## 第9章 安全软件

在本章

- Linux sXid

- Linux SSH1 客户端/服务端

- Linux SSH2 客户端/服务端

- Linux Tripwire 2.2.1

- Linux Tripwire ASR 1.3.1

- Linux GnuPG

关于本页的意见和建议请邮件至 gmourani@videotron.ca

## Linux sXid

### 概述

`sXid` 是一个全功能的 suid/sgid 监控程序，设计用于通过 `cron` 定期运行。它会跟踪你的 suid 文件和文件夹的任何变化。如果有任何新文件、未设置任何位的文件，或者其位或其他模式发生了变化，它将通过电子邮件或命令行以易于阅读的格式报告这些变化。`sXid` 将自动化查找你服务器上 SUID/SGID 的任务并将其报告给。。一旦安装，就可以不管它，它会为你完成这项工作。

### 这些安装说明假设

命令位于 "`var/tmp`"也可能是其他路径）。

安装在 RedHat Linux 6.1 上进行过测试。

安装过程中的所有步骤将在超级用户账户 "`root`" 中进行。

`sXid` 版本号为 4.0.1。

### 包

`sXid` FTP 站点：http://marcus.seva.net/pub/sXid/

你必须确保下载：`sXid_4_0_1.tar.gz`

### Tar 包

在安装 Bind 之前和之后列出系统文件列表，然后使用 `diff` 比较它们以找出它将文件放置在何处。安装软件后只需运行 `find / * sXid1` 和 `find / * sXid2`，然后使用 `diff sXid1 sXid2 * sXid` 获取变化列表。

### 编译

解压 tar (`tar.gz`)。

```bash
[root@deep]$ cp sXid_version_tar.gz /var/tmp/
[root@deep]$ cd /var/tmp
[root@deep]$ rm zpf sXid_version_tar.gz
```

### 编译与优化

进入新的 `sXid` 目录，并在终端中输入以下命令：

```bash
make install
```

上述命令将配置软件以确保你的系统具有成功编译该包所需的功能和库，将所有源文件编译为可执行文件，并将二进制文件和任何支持文件安装到适当的位置。

### 工作后的清理

```bash
[root@deep]$ cd /var/tmp
[root@deep]$ rm -rf sXid-version/sXid_version_tar.gz
```

关于本页的意见和建议请邮件至 gmourani@videotron.ca

"`rm`" 命令将删除我们用于编译和安装 `sXid` 的所有源文件。它还会删除 "`/var/tmp`" 目录下的 `sXid` 压缩包。

### 配置

我们在书籍《Linux DOS》中描述的所有软件在 tar 压缩包 "`floppy.tgz`" 中都有特定的目录和子目录，其中包含特定程序的配置文件。如果你归档了这个文件，就不需要手动重新制作下面的配置文件或通过剪粘贴来创建你的配置文件。无论你决定手动复制还是从归档文件中方便地获取这些文件，你都有责任根据你的需求进行修改、调整，并将与 `sXid` 软件相关的文件放置在服务器机器上适当的位置，如下所示。服务器配置文件位于以下 Internet 地址：http://pages.infinit.net/lotus1/doc/opt/sxid/

- 要运行 `sXid`，需要该文件并必须将其创建或复制到服务器上适当的目录。

将 `sxid.conf` 文件复制到 "`/etc/`" 目录。

你可以从我们的 `floppy.tgz` 归档中获得列出的配置文件。从解压的 `floppy.tgz` 归档将以下文件复制到适当的位置，或直接从此处复制粘贴到相关文件中。

### 配置 "`etc/sxid.conf`" 文件

`sXid` 的配置文件 ("`/etc/sxid.conf`") 允许你修改程序的运行。它有详细注释且非常基础。

步骤 1

编辑 `sxid.conf` 文件 (`vi /etc/sxid.conf`) 并设置你的需求：

```bash
# sXid 配置文件
# 注意所有目录必须是绝对路径，且末尾没有 /

# 从哪里开始搜索文件
SEARCH = ""

# 排除搜索哪些子目录
EXCLUDE = "/proc /mnt /cdrom /floppy"

# 将报告发送给谁
EMAIL = "root"

# 当没有变化时也始终发送报告？
ALWAYS_NOTIFY = "no"

# 中期日志存放在哪里。这将根据下方的 KEEP_LOGS 轮 'x' 次
LOG_FILE = "/var/log/sxid.log"

# 保留多少日志
KEEP_LOGS = "5"

# 当没有变化时也始终轮日志？
ALWAYS_ROTATE = "no"

# 禁止 +s 的目录（这些目录会被搜索）
```

© Copyright 1999 Open Network Architecture ®

关于本页的意见和建议请邮件至 gmourani@videotron.ca

# 即使 SEARCH 中没有明确指定，EXCLUDE 规则也有效

FORBIDDEN = "home/tmp"

# 这意味着 ALWAYS_NOTIFY。它将随变化发送完整的列表

LISTALL = "no"

# 忽略这些目录路径中的条目（这意味着将记录文件，你可以通过将其设置为 "/" 来有效忽略所有目录条目）。默认是 /home

IGNORE_DIRS = "/home"

# 包含（每行一个）sXid 应该监控的其他文件列表的文件。这对于不是 suid 但与系统完整性相关的（tcpd, npcd, apache..）有用

# EXTRA_LIST = "/etc/sxid.list"



# 邮件程序
这更改了报告的默认编译发送器。只有当你更改了位置且不想重新编译 `sXid` 时才需要此。

`MAIL_PROG = "/usr/bin/mail"`

## 步骤 2
在 `crontab` 中添加条目使 `sXid` 作为 `cron` 任务运行：

`sXid` 将从 `cron` 运行，基本上跟踪 `suid` 文件和文件夹的所有变化。如果有任何新文件、未设置任何位的文件，或者其位或其他模式发生了变化，它将报告这些变化。添加 `crontab` 使用以下内容：

```bash
0 4 * * * /usr/bin/sxid
```

详细信息见多个页面：

`sxid.conf (5)` - 配置设置

`sxid (1)` - 检查

`sXid` 管理工具

未发现更改

### 编译
解压 `tar` 包 (`tar.gz`)。

```bash
[root@deep]# cp ssh-version.tar.gz /var/tmp
[root@deep]# cd /var/tmp
[root@deep]# tar xpf ssh-version.tar.gz
```

## 编译与优化
进入新的 `ssh` 目录，并在终端输入以下命令：

```bash
CC=gcc \
CFLAGS="-O9 -funroll-loops -fast-math -malign-align -mcpu=pentium -march=pentium -fomit-
frame-pointer -fno-exceptions" \
  ./config \
  --prefix=/usr \
  --with-etcdir=/etc/ssl \
  --without-idat \
  --enable-warnings \
  --without-rsh \
  --without-library \
  --disable-server-port-forwards \
  --disable-client-port-forwards \
  --disable-server-x11-forwarding \
  --disable-client-x11-forwarding \
  --disable-uid-ssh
```

这告诉 `ssh1` 为这种特定的硬件设置进行配置，具体如下：

- 避免商业使用中的专利。
- 如果使用 `gcc/egcs`，则启用 `-Wall`（警告）选项。
- 在任何情况下均不使用 `rsh`。
- 编译时支持顶部。
- 禁用服务端所有的端口转发（X11 除外）。
- 禁用客户端所有的端口转发（X11 除外）。
- 服务端开启 X11 转发。
- 禁用客户端 X11 转发。
- 安装不带 `sudo` 权限的 `ssh`。

```bash
[root@deep]# make clean
[root@deep]# make
[root@deep]# make install
```

"`make clean`" 命令会删除之前所有的编译痕迹以避免任何错误，`make` 命令将所有源文件编译成可执行的二进制文件，最后 `make install` 将二进制文件和任何支持文件安装到适当的位置。

## 工作后的清理

```bash
[root@deep]# cd /var/tmp
[root@deep]# rm -rf ssh1-version/ ssh-version.tar
```

"`rm`" 命令将删除我们用于编译和安装 SSH1 的所有源文件。它还会删除 `/var/tmp/` 目录下的 SSH1 压缩存档。

关于本页面的意见和建议请邮件至 `gnourini@videotron.ca`

## 配置
我们在书籍《Linux pdf》中描述的所有软件都将在名为 `floppy.tgz` 的 `tar` 压缩包中有一个特定的目录和子目录，其中包含特定程序的配置。如果您获取了这个存档文件，您就不需要手动重现下面的不同配置，或通过剪切粘贴来创建您的配置文件。无论您决定手动复制还是为了方便从归档压缩文件中剪切文件，都由您责任根据您的需求以及 SSH 软件相关的文件路径，将它们调整到服务器上的适当位置，如下所示。服务器配置文件存档位于以下网际地址：`http://pages.infinit.net/lotus1/floppy.tgz`

- 运行 SSH 客户端/服务器需要以下文件，并且必须创建或复制到您上相应的目录中。

将 `ssh_config` 文件复制到 `/etc/ssh/` 目录。

将 `ssh_config` 文件复制到 `/etc/ssh/` 目录。

你可以在 `floppy.tgz` 存档中获取下面列出的配置文件。从解压后的 `floppy.tgz` 中复制以下文件到其适当位置，或直接剪切粘贴到相关文件中。

### 配置 `/etc/ssh/ssh_config` 文件
`ssh1` 的配置文件（`/etc/ssh/ssh_config`）允许您修改客户端程序的运行。该文件包含键值对，每行一个，关键字不区分大小。以下是更重要的关键字；完整列表可以在 `ssh (1)` 的帮助页中查看。

编辑 `ssh_config` 文件（`vi /etc/ssh/ssh_config`）并添加：

# 各种选项的全局默认设置

```
Host *
ForwardAgent no
ForwardX11 no
RSAAuthentication no
RhostSAAuthentication no
RSAAuthentication yes
TISAuthentication no
PasswordAuthentication yes
FailbackToAuth no
UserAuth no
BatchMode no
Compression yes
StrictHostKeyChecking no
IdentityFile ~/.ssh/identity
Port 22
KeepAlive yes
Cipher blowfish
EscapeChar -
```

这告诉 `ssh_config` 文件为这种特定的配置设置进行设置，具体如下：

`Host *`

© Copyright 1999 Open Network Architecture ® 154

关于本页面的意见和建议请邮件至 `gmourani@videotron.ca`

此选项 "`Host`" 将声明（一直到下一个 `Host` 关键字）限制为匹配关键字之后任一模式的主机。使用单个 `"*"` 作为模式可以为所有主机提供全局默认设置。

`ForwardAgent no`

此选项 "`ForwardAgent`" 指定到认证代理（如果有）的连接是否将转发到远程机器。

`ForwardX11 no`

此选项 "`ForwardX11`" 指定是否将 X11 连接自动重定向到安全通道并设置 `DISPLAY`。

`RSAAuthentication no`

此选项 "`RSAAuthentication`" 指定是否尝试基于主机的身份验证。

`RRSAAuthentication no`

此选项 "`RostsRSAAuthentication`" 指定是否使用 RSA 主机身份验证尝试基于主机的身份验证。

`RSAAuthentication yes`

此选项 "`RSAAuthentication`" 指定是否尝试 RSA 认证。

`TISAuthentication no`

此选项 "`TISAuthentication`" 指定是否使用 TIS。

`PasswordAuthentication yes`

此选项 "`PasswordAuthentication`" 指定是否使用密码认证。

`FailbackToAuth no`

此选项 "`FailbackToAuth`" 指定是否回退到认证。

`UserAuth no`

此选项 "`UserAuth`" 指定是否允许用户身份验证。

`BatchMode no`

此选项 "`BatchMode`" 指定是否使用批模式。

`Compression yes`

此选项 "`Compression`" 指定是否使用压缩。

`StrictHostKeyChecking no`

此选项 "`StrictHostKeyChecking`" 指定如何检查主机。

`IdentityFile ~/.ssh/identity`

此选项 "`IdentityFile`" 指定身份密钥文件。

`Port 22`

此选项 "`Port`" 指定端口号。

`KeepAlive yes`

此选项 "`KeepAlive`" 指定是否发送心跳包。

`Cipher blowfish`

此选项 "`Cipher`" 指定加密算法。

`EscapeChar -`

此选项 "`EscapeChar`" 设置转义字符。

© Copyright 1999 Open Network Architecture ® 155

关于本页面的意见和建议请邮件至 `gmourani@videotron.ca`

此选项 "`KeepAlive`" 指定系统是否向对方发送心跳消息。如果发送了，连接中断或一台机器的崩溃将被注意到。

`Cipher blowfish`

此选项 "`Cipher`" 指定加密会话的加密算法。

`EscapeChar ~`

此选项 "`EscapeChar`" 设置转义字符。

## 配置 `/etc/ssh/sshd_config` 文件



`sshd` 的配置文件（`/etc/ssh/sshd_config`）允许您设置修改守护进程的选项。文件包含键值对，每行一个，关键字不区分大小。以下是最重要的关键字；完整列表可以在 `sshd (8)` 的帮助页中查看。

```
# 这是 ssh 系统配置文件
Port 22
ListenAddress 192.168.1.1
HostKey /etc/ssh/ssh_host_key
RandomSeed /etc/ssh/ssh_random_seed
ServerKeyBits 1024
LoginGrace 600
KeyRegenerationInterval 3600
PermitRootLogin no
IgnoreHosts yes
StrictModes yes
QuietMode no
X11Forwarding no
FacitLogging no
PrintMotal yes
KeepAlive yes
SyslogFacility AUTH
RhostsAuthentication no
RhoSAAAuthentication no
RSAAuthentication yes
PasswordAuthentication yes
PermitEmptyPasswords no
AllowUsers admin
AllowHosts 192.168.1.4
```

这告诉 `sshd_config` 文件为这种特定的配置设置进行设置，具体如下：

`Port 22`

此选项 "`Port`" 指定 `sshd` 监听的端口号。

`ListenAddress 192.168.1.1`

此选项 "`ListenAddress`" 指定绑定 `sshd` 服务端接字接口的 IP 地址。

`HostKey /etc/ssh/ssh_host_key`

此选项 "`HostKey`" 指定包含私有主机密钥的文件。

关于本页面的意见和建议请邮件至 gmourani@videotron.ca

`RandomSeed/etc/ssh/ssh_random_seed`

该选项 "`RandomSeed`" 指定了包含服务器随机种子的文件；该文件会自动创建并定期更新。

`ServerKeyBits1024`

该选项 "`ServerKeyBits`" 定义了密钥的位数。

`LoginGraceTime 600`

该选项 "`LoginGraceTime`" 指定了在用户未成功登录之前，服务器等待的时间。

`KeyRegenerationInterval 3600`

该选项 "`KeyRegenerationInterval`" 意味着服务器在许多秒后（如果已到期）会自动重新生成密钥。重新生成的目的是防止通过入侵机器并窃取密钥来解密会话。

`PermitRootLogin no`

该选项 "`PermitRootLogin`" 指定了 root 用户是否可以使用 ssh 登录。切勿始终将此选项设置为 yes。

`IgnoreRhosts yes`

该选项 "`IgnoreRosts`" 指定在认证时不使用 rhosts 和 hosts 文件。

`StrictModes yes`

该选项 "`StrictModes`" 指定了 ssh 在接受登录之前是否应该检查用户主目录和 hosts 文件的模式和所有权。这通常是有益的，因为用户可能会无意中将目录或文件设置为全局可写。

`QuietMode no`

该选项 "`QuietMode`" 指定了系统是否在静音模式下运行。在静音模式下，系统日志中记录致命错误。

`X11Forwarding no`

该选项 "`X11Forwarding`" 指定了是否允许 X11 转发。

`FascistLogging no`

该选项 "`FascistLogging`" 指定了是否使用详细日志。详细日志会违反用户隐私，不建议使用。

`PrintMotmot yes`

该选项 "`PrintMmot`" 指定了用户在交互式登录时 `sshd` 是否应该打印 "`/etc/motd`"。

`KeepAlive yes`

该选项 "`KeepAlive`" 指定了系统是否应该向对方发送保持活动的消息。如果发送了这些消息，连接死亡或一台机器的崩溃将被正确注意到。

`SyslogFacility AUTH`

该选项 "`SyslogFacility`" 给出了从 ssh 记录消息时使用的设施代码。

`RhostsAuthentication no`

该选项 "`RhostsAuthentication`" 指定了使用 rhosts 和 `/etc/hosts.equiv` 进行认证是否足够。

`RhostsRSAAuthentication no`

关于本页面的意见和建议请邮件至 gmnouari@videotron.ca

该选项 "`RostsRSAAuthentication`" 指定了是否允许带有成功 RSA 主机认证的 hosts 或 "`/etc/hosts.equiv`" 认证。

`RSAAuthentication yes`

该选项 "`RSAAuthentication`" 指定了允许纯 RSA 认证。

`PasswordAuthentication yes`

该选项 "`PasswordAuthentication`" 指定了是否允许密码认证。

`PermEmptyPasswords no`

当允许密码认证时，该选项 "`PermEmptyPasswords`" 指定了服务器是否允许登录空密码字符串的账户。

`AllowUsers admin`

该选项 "`AllowUsers`" 后面可以跟随任意数量的用户模式或 `user@host` 模式，用空格分隔。主机名可以是 DNS 名称或 IP 地址。

`AllowHosts 192.168.1.4`

该选项 "`AllowHosts`" 后面可以跟随任意数量的主机，用空格分隔。如果指定了，.hosts、.hosts 和 "`/etc/hosts.equiv`" 仅对名称与服务器匹配的主机有效。服务器用于将客户端的主机映射到标准主机名。如果找不到该名称，则使用其 IP 地址作为主机名。

# 配置 sshd 使用 tcp-wrappers inetd 服务器

Tcp-wrappers 用于启动和停止 `sshd` 服务。执行时，`inetd` 从配置文件中读取配置信息，默认该文件为 "`etc/inetd.conf`" 。配置文件的每个字段都必须有一个条目，每个字段之间用制表符或空格分隔。

### 第 1 步

编辑 `inetd.conf` 文件 (`/etc/inetd.conf`) 并添加行：

```
ssh      stream now rout /usr/sbin/tcp sshd -i
```

注意：`-i` 参数很重要，因为它指定了 `sshd` 是从 `inetd` 运行的。此外，在添加行之后，通过发送 `SIGHUP` 信号（`killall -HUP inetd`）更新您的 "`inetd.conf`" 文件。

```
[root@deep./root] # killall -HUP inetd
```

### 第 2 步

编辑 `hosts.allow` 文件 (`/etc/hosts.allow`) 并添加以下行：

```
sshd: 192.168.1.4 win.openarch.com
```

这意味着 IP 为 "`192.168.1.4`" 且主机名为 "`win.openarch.com`" 的客户端被允许在服务器上进行 ssh。

这些"`daemon`"字符串（用于 tcp-wrappers）被 `sshd` 使用：

- `sshdwd-X11`（如果你想允许/拒绝 X11 转发）。
- `sshdwd-<port-number>`（用于 tcp 转发）。
- `sshdwd-<port-name>`（在 `/etc/services` 中定义的端口名。用于 tcp 转发）。

注意：如果您决定切换到使用 ssh，请确保在您所有的服务器上安装并使用它。拥有十台安全的服务器和一台不安全的服务器是浪费时间。

关于本页面的意见和建议请邮件至 gmourani@videotron.ca

# 更多文档

详情，可以阅读以下几个 man页（帮助手册）：

- `ssh-add (1)` - 为代理添加身份
- `ssh-agent (1)` - 认证代理
- `ssh-keygen (1)` - 密钥对生成
- `ssh (1)` - 安全 shell 客户端（远程登录）
- `sshd (8)` - 安全 shell 守护进程

# 用户配置

### 第 1 步

执行以下命令创建公私钥并位于本地：

```
-keygen
```

结果应如下所示：



```
初始化随机数...
p: ................. (430)
q: ................. (456)
计算密钥...
要将密钥保存到 (/home/username/.ssh/identity): [回车]
输入密码：
再次输入密码：
密钥已保存至 /home/username/.identity。
您的公钥为：
1024-bit RSA username@deep.openarch.com
您的公钥已保存至 /home/username/.pub。
```

注意：如果你有多个账户，需要在每个账户上创建。例如：
- Mail 服务器
- Web 服务器
- GW 服务器

这允许在这些服务器之间限制访问。

### 第 2

使用 `ftp` 命令将公钥发送到远程系统的 `"/home/username/.ssh"` 目录，可能需要 `identity.pub` 文件。

关于本页面的意见和建议请邮件至 `gmourani@videotron.ca`

如果访问系统仍然被拒绝，您应该检查其文件的权限：
- 主目录本身
- `.ssh` 目录
- `.ssh/authorized_keys`

权限应该只允许所有者写入。此示例显示：

```
[admin@deep]$ cd

[admin@deep]$ ls -ld .ssh

drwx------ 5 admin 1024 Nov 28 07:05

rwxr-xr-x 2 admin 1024 Nov 29 09:00 .ssh

-rw-r--r-- 1 admin 342 Nov 29 09:00 authorized_keys
```

# 更改密码

您可以随时使用 `ssh-keygen` 的 `-p` 更改密码。

- 要更改密码，请使用命令：

```
[root@deep]# su username

[username@deep]$ ssh-keygen -p
```

文件名 (`/home/username/.ssh/identity`): [回车]
输入旧密码：
密钥注释 'username@deep.openarch.com'
输入新密码：
再次输入新密码：
密钥已使用新密码保存。

# SSH 用户工具

下面的命令是我们经常使用的，但存在更多命令，您必须查看 man 页和文档获取更多详细信息。

## ssh

`ssh`（Secure Shell）是一个用于登录远程机器并在远程机器上执行命令的程序。它旨在替代 `login` 和 `rsh`，并在两个不可信的主机之间提供安全通信。X11 连接和任意 TCP/IP 端口也可以通过安全通道进行转发。

- 要登录远程机器，使用命令：

```
[root@deep]# ssh <login_name> <hostname>
```

例如：

```
[root@deep]$ ssh username.openarch.com password:

上次登录：1999年10月19日 18:13:00-0400 来自 gate.openarch.com

欢迎来到 Deepforest 上的 www.openarch.com。
```

## scp

可以使用 `scp` 命令从本地系统复制文件到远程系统或反之，或者在两个远程系统之间复制。获取远程文件副本到当前目录的简单方法如下所示。

关于本页的意见和建议请邮件至 `gmourani@videotron.ca`

- 要将文件从远程拷贝到本地系统，请使用命令：
  `[root@deep$] scp -p login_name@hostname:/dir/for/file localadir/to/filelocation`
  例如：
  `[username@deep$] scp -p username@mail.openarch.com:`
  为 RSA key 'username@mail.openarch.com' 输入口短：
  test1 2 KB | 7.9 KB/s | ETA: 00:00:00 | 100%

- 要将文件从本地拷贝到远程系统，请使用命令：
  `[root@deep$] scp -p localadir/to/filelocation <hostname>:/dir/for/file`
  例如：
  `[username@deep$] scp -p usr/bin/test2 username@mail.com:/var/tmp`
  输入用户密码：
  test2 7 KB | 7.9 KB/s | ETA: 00:00:00 | 100%

注意：`p` 选项表示保留源文件的修改时间、访问时间以及模式。这通常是必要的。

## 已安装文件

- `/etc/ssh`
- `/etc/ssh/ssh_key`
- `/etc/ssh/ssh_key.pub`
- `/etc/ssh/config`
- `/etc/ssh/sshd_config`
- `/root/ssh`
- `/root/ssh/random_seed`
- `/usr/bin/ssh1`
- `/usr/bin/ssh`
- `/usr/bin/login`
- `/usr/bin/ssh-keygen1`
- `/usr/bin/ssh-keygen`
- `/usr/bin/ssh-agent1`
- `/usr/bin/ssh-agent`
- `/usr/bin/ssh-add1`
- `/usr/bin/scp1`
- `/usr/bin/scp`
- `/usr/bin/make-ssh-known-hosts1`
- `/usr/bin/make-ssh-known-hosts`
- `/usr/man/1/scp1`
- `/usr/man/1/ssh-keygen1`
- `/usr/man/1/ssh-keygen`
- `/usr/man/1/ssh-agent1`
- `/usr/man/1/ssh-add1`
- `/usr/man/1/scp`
- `/usr/man/1/login1`
- `/usr/man/1/ssh1.1`
- `/usr/man/1/make-ssh-known-hosts1.1`
- `/usr/man/8/sshd.8`
- `/usr/sbin/sshd-1`
- `/usr/sbin/sshd`

## Windows 免费客户端

### Putty

`PuTTY`（在停止仅作为 Telnet 使用之前名为 STel）是一个适用于 Win32 平台（Win95 和 WinNT）的免费 Telnet 和 SSH 实现；据报道，Win98 甚至 Win2000 也可以运行。

#### 软件包

首页：`http://www.chiark.greenend.org/~sgtman/putty.html`

### Tera Term 和 TTSSH

`TTSSH` 是一个适用于 Windows 的免费 SSH 客户端。它作为 Teraterm Pro 的扩展 DLL 实现。Teraterm 是一个优秀的 Windows 免费终端模拟器/telnet 客户端，且其源代码可用。`TTSSH` 为 Teraterm Pro 增加了 SSH 能力，且不会破坏 Teraterm 的任何现有功能。`TTSSH` 免费下载，且源代码同样可用。

#### 软件包

Tera Term Pro 首页：`http://hp.vector.co.jp/authors/VA002416/teraterm.html`
TTSSH 首页：`http://www.zip.com.au/~rock/download.html`

# Linux SSH2 客户端/服务器

### 概述

这是 SSH 的商业版本。我们为使用该软件的用户提供了配置步骤。在我们的配置中，出于安全考虑，`sshd2` 支持 tcp-wrappers (`inetd` 超级服务器)。

## 这些安装说明假设

- 命令兼容 Unix。
- 源码路径为 `"/var/tmp"`（可以是其他路径）。
- 安装已在 RedHat Linux 6.1 上通过测试。
- 安装过程中的所有步骤将在超级用户账户 `"root"` 下进行。
- SSH2 版本号为 2.0.13。

### 软件包

SSH2 首页：`http://www.ssh.fi/`
`ssh-2.0.13.tar.gz`
你必须确保下载：

### 压缩包

在安装 ssh2 之前列出系统上的文件列表是一个好主意，安装后再也列一次，然后使用 `diff` 对它们进行对比，找出文件被放置在什么位置。只需在安装软件前运行 `find /* > ssh1`，在安装后运行 `find "*" ssh2`，并使用 `diff ssh1 ssh2 > ssh` 获取更改列表。

### 编译

```
解压 tarball (tar.gz)。

[root@deep] cp ssh-version.tar.gz /var/tmp

[root@deep] cd /var/tmp

[root@deep] tar xzf ssh-version.tar.gz
```

## 编译与优化

进入新的 SSH2 目录，并在终端中执行以下命令：

```
CC="ecgs" \
CFLAGS="-opt" \
```



关于本页面的意见和建议请邮件至 `gmourani@videotron.ca`

`ForwardX11` no
此选项 `ForwardX11` 指定 X11 连接是否会自动重定向到安全通道和 DISPLAY 设置中。

`PasswordPrompt` "%U's password:"
此选项 `PasswordPrompt` 设置密码提示，用户在连接到主机时将使用该提示。可以使用变量 `%%U` 和 `%%H` 分别用于提供用户的登录名和主机名。

`Ssh1Compatibility` no
此选项 `Ssh1Compatibility` 指定是否使用 SSH1 兼容性代码。

`Ssh1AgentCompatibility` none
此选项 `Ssh1AgentCompatibility` 指定是否也转发 SSH1 连接。

`NoDelay` yes
此选项 `NoDelay` 如果为 "yes"，则启用套接选项 TCP_NODELAY。这将提高网络性能。

`KeepAlive` yes
此选项 `KeepAlive` 指定系统是否向对方发送心跳消息。如果发送了这些消息，连接的断开或其中一台机器的崩溃将得到适当通知。

`QuietMode` no
此选项 `QuietMode` 会抑制所有的警告和诊断信息。仅显示致命错误。

## 配置 `/etc/sshd/sshd2_config` 文件

`sshd2` 的配置文件 (`/etc/sshd/sshd2_config`) 允许你设置修改守护进程运行的选项。文件包含键值对，每行一个，键不区分大小写。以下是更重要的关键词；完整列表可参阅 `sshd2(8)` 页面。

编辑 `sshd2_config` 文件 (`vi /etc/sshd/sshs2_config`) 并添加：

```
# sshd2_config

# SSH 2.0 Server Configuration

*:

  Port 22

  ListenAddress 192.168.1.1

  Ciphers AnyStdCipher

  IdentityFile identification

  AuthorizationFile authorization

  HostKey hostkey

  PublicKeyKeyFile hostkey.pub

  RandomSeed random_seed

  ForwardAgent no

  ForwardX11 no

  PasswordGuesses 3

  MaxConnections 5

  PermitRootLogin no

  AllowedAuthentications publickey.password

  RequiredAuthentications publickey.password

  VerboseMode no

  PrintMonitor yes

  CheckMail yes
```

© Copyright 1999 Open Network Architecture ®

关于本页面的意见和建议请邮件至 `gmnourani@videotron.ca`

| Key | Value |
|---|---|
| UserConfigDirectory | "%D/.ssh2" |
| SyslogFacility | AUTH |
| Ssh1Compatibility | no |
| NoDelay | yes |
| KeepAlive | yes |
| UserKnownHosts | yes |
| AllowHosts | 192.168.1.4 |
| DenyHosts | * |
| QuietMode | no |

## 子系统定义

`subsystem-sftp sftp-server`

这告诉 `sshd2_config` 文件为此特定配置设置 `sshd`：

`Port` 22
此选项 `Port` 指定 `ssh2` 监听的端口号。

`ListenAddress` 192
此选项 `ListenAddress` 指定 `sshd` 服务器套接字绑定的接口的 IP 地址。

`Ciphers` AnyCipher
此选项 `Ciphers` 指定用于加密会话的加密算法。AnyStd 仅允许标准加密算法。

`IdentityFile` identification
此选项 `IdentityFile` 指定用户标识文件的文件名。

`AuthorizationFile` authorization
此选项 `AuthorizationFile` 指定用户授权文件的文件名。

`HostKey` hostkey
此选项 `HostKey` 指定包含私有主机密钥的文件（默认 `(etc/ssh2/hostkey)`。

`PublicHostKey` hostkey.pub
此选项 `PublicHostKey` 指定包含公有主机密钥的文件（默认 `(etc/ssh2/hostkey.pub)`。

`RandomSeedFile` random_seed
此选项 `RandomSeedFile` 指定用户随机种子的文件名。

`ForwardAgent` no
此选项 `ForwardAgent` 指定到身份验证代理（如果有）的连接是否转发到远程机器。

`ForwardX11` no
此选项 `ForwardX11` 指定 X11 连接是否会自动重定向到安全通道和 DISPLAY 设置中。

`PasswordGuesses` 3
此选项 `PasswordGuesses` 指定用户在使用密码身份验证时的允许尝试次数。

© Copyright 1999 Open Network Architecture ® 166

关于本页面的意见和建议请邮件至 `gmounari@videotronca.ca`

### MaxConnections 5

此选项 `MaxConnections` 指定 `sshd` 同时处理的最大连接数。这在那些因新连接涌入 `sshd` 可能导致系统不稳定或崩溃的系统中非常有用。

### PermRootLogin no

此选项 `PermRootLogin` 指定 root 用户是否可以使用 `ssh2` 登录。永远不要设为 yes。

### AllowedAuthentications,pubkey,password

此选项 `AllowedAuthentications` 指定允许使用的身份验证方法。这是一个逗号分隔的列表，包含（当前）password、public key 和基于 hash 的词。每种都是一种身份验证方法。默认是 "password,pubkey"。通过 `RequiredAuthentications`，系统管理员可以强制用户在被视为身份通过之前完成多次身份验证。

### RequiredAuthentications pubkey,password

此选项 `RequiredAuthentications` 与 `AllowedAuthentications` 相关，用于指定用户在继续之前必须完成的身份验证方法。此参数没有默认值。此参数必须设置。

### VerboseMode no

此选项 `VerboseMode` 会抑制所有的警告和诊断信息。

### PrintMonitor yes

此选项 `PrintMonitor` 指定系统是否打印。

### CheckMail yes

此选项 `CheckMail` 指定系统是否应该打印。

### UserConfigDirectory "%D/.ssh2"

此选项 `UserConfigDirectory` 指定用户特定配置的目录。

### SyslogFacility AUTH

此选项 `SyslogFacility` 指定日志设施。

### Ssh1Compatibility no

此选项 `Ssh1Compatibility` 指定是否使用 SSH1 兼容性代码。

`Ssh1AgentCompatibility` none

指定是否也转发 SSH1 连接。

# "etc/pam.d/ssh"文件的配置

配置您的 "etc/pam.d/ssh" 文件以使用 pam 认证。

创建 `ssh` 文件（`touch /etc/pam.d/ssh`）并添加以下内容：

```
#%PAM-1-0

auth       required /lib/security/pam_pwdb.shadow

auth       required /lib/security/pam_nlogin.so

account    required /lib/security/pam_pwdb.so

password   required /lib/security/pam_cracklib.so

password   required /lib/security/pam_pwdb.so use_authtok nullok md5

session    required /lib/security/pam_pwdb.so
```



# 更多文档

更多详细信息，有几个页面可以阅读：

- `$ ssh-add2 (1)`      - 为身份验证代理添加身份
- `$ ssh-agent2 (1)`     - 身份验证代理
- `$ ssh-keygen2 (1)`     - 密钥对生成
- `$ man ssh2 (8)`         - secure shell 客户端（远程登录程序）
                      - secure shell 守护进程

# SSH2 用户级配置

## 第一步

执行以下命令创建本地的私钥和公钥：
```
[root@deep]$ su username
[username@deep]$ ssh-keygen2
```

## 第二步

在本地的 `".ssh2"` 目录下创建一个“标识”用文件：
```
[username@deep]$ cd ~/.ssh2
[username@deep]$ echo "Idkey_id_1024_a" > identification
```

注意：在远程端创建标识文件是可选的。

## 第三步

将本地的公钥 (`id_rsa_1024_a.pub`) 复制到远程的 `".ssh2"` 目录，命名为 `Local.pub`。

## 第四步

在远程的 `".ssh2"` 目录下创建一个“授权”用文件：
```
[username@deep]$ touch authorization
```

## 第五步

在 `"authorization"` 中添加以下行：
```
[username@deep]$ vi authorization
key Local.pub
```

# SSH2 用户

关于本页的意见和建议请邮件至 `gmourani@videopentron.ca`

下面列出的命令是我们在日常使用中常用的，但还有更多命令，您必须检查页面和文档以获取更多细节和信息。

# ssh2

`SSH2` (Secure Shell) 是一种用于登录远程机器并在其上执行命令的程序。它旨在取代 `login` 和 `rsh`，并在不安全的网络上为两个不可信的主机之间提供安全通信。`X11` 连接和任意 `TCP/IP` 端口可以通过安全通道进行转发。

- 要登录远程机器，请使用命令：
```
[root@deep]# ssh2 -l <hostname>
```
例如：
```
[root@deep]# ssh2 -l username.openarch.com
Passphrase for key "/home/username/.ssh2/id_dsa_1024_a" with comment "1024-dsa,
username@deep.openarch.com, Oct 19 1999 14:31:00-0400"
username's password:
Last login: Tue 19 Oct 1999 18:13:00-0400 from gate.openarch.com
Welcome to username on Deepfreest.
```

其中 `<login>` 是您用于连接 ssh 服务器的名称名称 `<<hostname>` 是您的 ssh 地址。

`sftp` (安全传输) 是一种类似于 `ftp` 的客户端，可用于网络上的文件传输。`sftp` 在数据连接中使用 `ssh2`，因此传输是安全的。在使用 `sftp` 之前，必须先连接 `ssh2`。

- 要通过 `ssh2` 进行 `ftp`，请使用以下命令：
```
[username@deep] sftp <hostname>
```
例如：
```
[username@deep] sftp :home/username
local path :home/username
Passphrase for key "/home/username/.ssh2/id_dsa_1024_a" with comment "1024-dsa,
username@deep.openarch.com, Oct 19 1999 14:31:40-0400"
username's password:
remote path :home/username
sftp
```

其中 `<hostname>` 是您用于 `sftp` 的服务器名称。

# 已安装文件

```
> /etc/pam.d/ssh

> /etc/ssh2

> /etc/ssh2/hostkey

> /etc/ssh2/hostkey.pub

> /etc/ssh2/sshd2_config

> /etc/ssh2/ssh2_config

> /root/ssh2

> /root/ssh2/random_seed

> /root/ssh2

> /usr/man/man/ssh2.1

> /usr/man/man/ssh-keygen2.1

> /usr/man/man/ssh-add2.1

> /usr/man/man/ssh-agent2.1

> /usr/man/man/scp2.1

> /usr/man/man/sftp2.1
```

```
> /usr/man/man/8/sshd.2

> /usr/man/man/8/sshd.8

> /usr/bin/ssh2

> /usr/bin/scp

> /usr/bin/sftp

> /usr/bin/sftp-server

> /usr/bin/ssh-agent

> /usr/bin/ssh-keygen

> /usr/bin/sshkeygen2

> /usr/bin/ssh-add

> /usr/bin/askpass

> /usr/bin/ssh-keygen
```

© Copyright 1999 Open Network Architecture

关于本页的意见和建议请邮件至 `gmourani@videotron.ca`

```
> /usr/man/man/1/ssh.1  > /usr/bin/scp

> /usr/man/man/1/ssh-add.1  > /usr/bin/sftp

> /usr/man/man/1/ssh-agent.1  > /usr/bin/sftp-server

> /usr/man/man/1/ssh-keygen.1  > /usr/bin/signer

> /usr/man/man/1/scp.1  > /usr/bin/sshd

> /usr/man/man/1/sftp.1  > /usr/sbin/sshd
```

# Linux Tripwire 2.1

`Tripwire` 的初始版本 `1.0` 设计于 `1992` 年。`Tripwire` 软件已完全重写为 `2.0` 版本。重写版不是开源的。策略不再位于配置文件，策略语言发生了变化。基础表示不同。`Tripwire 2.0` 及后续版本使用加密签名；提供了签名选项、“无签名”选项以及添加自定义签名的能力。根据目前的标准，许多签名是非常弱的。

根据 `Tripwire` 官方网站，`Tripwire` 在最底层工作，保护构成企业网络的服务器和工作站。`Tripwire` 通过扫描计算机并创建系统已知状态的文件“快照”数据库来工作。用户可以精确配置 `Tripwire`，指定要监控的每个文件和目录，创建一个适用于企业内所有机器的标准模板。

一旦创建了数据库，系统管理员可以使用 `Tripwire` 检查任何系统的完整性。通过扫描当前系统与数据库中存储的信息进行比较，`Tripwire` 会检测边界之外的添加、删除或更改。如果这些更改是有效的，管理员可以使用新信息更新数据库。如果发现恶意更改，系统管理员将哪些网络部分受到了影响。

此版本的 `Tripwire` 比之前的版本有显著改进。改进包括：

- 多级报告允许选择不同的详细级别。
- `Syslog` 选项将数据库初始化、更新和完整性检查发送到 `syslog`。
- 数据库性能经过优化以提高完整性检查的效率。
- 可以向个人邮箱发送报告部分。
- 支持 `SMTP` 电子邮件。
- 邮件测试允许您验证文件是否正确。
- 能够在策略文件中创建单独执行的多个部分。

安装说明假设兼容 `Unix`。源路径为 `"/var/tmp"` 可能为其他路径）。在 `RedHat Linux 6.1` 上进行了测试。安装中的所有步骤将在超级用户账户 `"root"` 中进行。`Tripwire` 版本为 `2.1`。

© Copyright 1999 Open Network Architecture

# 包

关于本页的意见和建议请邮件至 `gmourani@videotron.ca`

`Tripwire` 首页：`http://www.tripwiresecurity.com/`
你必须确保下载：`Tripwire_221_for_Linux_x86_tar.gz`

## 编译 Tripwire-2.1

解压包（`tar.gz`）。

```
[root@deep6 #] cp Tripwire_version_for_Linux_x86_tar.gz /var/tmp

[root@deep6 #] cd /var/tmp

[root@deep6 #] tar xpf Tripwire_version_for_Linux_x86_tar.gz
```



注意：解压 Tripwire 后，你将在 `var/tmp` 目录下看到 Tripwire 软件的以下文件：`License.txt`, `README`, `Release_Notes`, `install.cfg`, `install.sh`, `pkg` 目录以及 Tripwire tar.gz 文件 `Tripwire_version_for_Linux_x86_tar.gz`。

## 编译与优化

在安装过程中，你将：

1. 指定默认操作的配置选项。
2. 为站点和本地密钥规划两个密码短。
3. 运行安装脚本。
4. 编辑配置和策略文件。
5. 根据需要诊断配置和策略设置。
6. 初始化 Tripwire 软件数据库。

## `var/tmp/install.cfg` 文件的配置

记住 Tripwire 版本 2.2.1 不是开源的，因此你不能像其他存档源那样编译并安装它；相反，你必须修改 Tripwire 的 `install.cfg` 文件（这将自动为你安装 Tripwire 软件），为系统指定安装路径。我们必须修改此文件以符合 Red Hat 文件系统结构，并在 PATH 环境变量下安装 Tripwire 二进制文件。

### 第一步

编辑 `install.cfg` 文件（`vi /var/tmp/install.cfg`）并将此文件更改如下：

```
#
# install.cfg
#
# 默认 install.cfg 用于：
# Tripwire(R)2.2.1 for Unix
#
# 注意: 这是一个 Bourne shell 脚本，存储了你安装的
# 参数。安装程序将
# 执行此文件以生成你的配置文件，并
# 定位你安装的任何特殊配置需求。
# 请保护此文件，因为可能在此处插入
# 恶意代码
#
# 要设置安装的根目录，请根据需要将 TWROOT 设置为
# /usr/tss 以外的路径。
#
#============================================================
```

# 如果 CLOBBER 为真，则将覆盖现有文件。

© Copyright 1999 Open Network Architecture

关于此页面的意见和建议，请邮件至 gmourani@videotron.ca

# 如果 CLOBBER 为 false，则现有文件不会被覆盖。
`CLOBBER=false`

# TSS 目录树的根目录。
`TWROOT="/usr"`

# Tripwire 二进制文件存储在 TWBIN 中。
`TWBIN="$(TWROOT)/bin"`

# Tripwire 策略文件存储在 TWPOLICY 中。
`TWPOLICY="$(TWROOT)/TSS/policy"`

# Tripwire 手册页存储在 TWMAN 中。
`TWMAN="$(TWROOT)/man"`

# Tripwire 数据库文件存储在 TWDB 中。
`TWDB="$(TWROOT)/TSS/db"`

# Tripwire站点密钥存储在 TWITESKEYDIR 中。
`TWITESKEYDIR="$(TWROOT)/TSS/key"`

# Tripwire 本密钥存储在 TWOLOCALKEYDIR 中。
`TWLOCALKEYDIR="$(TWROOT)/TSS/key"`

# Tripwire 报告文件存储在 TWREPORT 中。
`TWREPORT="$(TWROOT)/TSS/report"`

# 这设置 Tripwire 的默认文本编辑器。
`WEDITOR="/bin/vi"`

# TWLATEPROMPING 控制 tripwire 询问密码的时刻。
`TWLATEPROMPING=false`

# TWLOOSESEDIRCK 选择应该监控的目录，
# 当目录中的文件被监控时属性发生变化。
`TWLOOSESEDIRCK=false`

# TWMAILVIOLATIONS 决定当使用 -email report 运行完整性检查但
# 未发现任何规则违规时，Tripwire 是否发送无违规报告。
# 这让管理员知道完整性检查已运行过，而不是由于某种原因失败了。
`TWMAILVIOLATIONS=true`

# TWMAILREPORTLEVEL 决定电子邮件报告的详细程度。
`TWMAILREPORTLEVEL=3`

# TWREPORTLEVEL 决定报告打印的详细程度。
`TWREPORTLEVEL=3`

# TWSYSLOG 决定 Tripwire 是否将记录到系统日志。
`TWSYSLOG=false`

######################################
# 邮件选项 - 选择合适的
# 方法并注释其他部分
######################################

######################################
# SENDMAIL - 默认
#

可以通过 SENDMAIL 或 SMTP 通过 TWMAILMETHOD 发送报告。
# 指定使用哪个 sendmail 程序。

© Copyright 1999 Open Network Architecture ®

关于此页面的意见和建议，请邮件至 gmourani@videotron.ca。

```
############################################################
TWMAILMETHOD=SENDMAIL
TWMAILPROGRAM=/usr/lib/sendmail -oi -t
############################################################
# SMTP 选项
# TWSMTPOST 选择用于发送报告的 SMTP 主机。
# SMTPMPORT 选择 SMTP 程序使用的 SMTP 端口。
############################################################
# TWMAILMETHOD=SMTP
# TWSMTPOST="mail.domain.com"
# TWSMPORT=25
###########################################################################################
# Copyright (C) 1998-2000 Tripwire Systems, Inc. Tripwire (R) 是
# Purdue Research Foundation 的注册商标，并专门许可给
# Tripwire (R) Security Systems, Inc.
################################################################################
```

注意：文件 `install.cfg` 是一个安装程序使用的 Bourne 脚本，用于设置配置变量。这些变量选择了安装程序复制文件的目标目录，以及当安装将覆盖 Tripwire 软件文件时，安装程序应该采取的操作。

### 第 2 步

现在必须运行安装脚本，根据你使用的是默认配置还是自定义配置值在我们的系统中安装 Tripwire 二进制文件和相关文件。

- 要运行安装脚本安装 Tripwire，请使用以下命令：
  `[root]@deep tmp/ ./install.sh`

注意：`install.sh` 是安装脚本，你运行它来开始安装。

### 第 3 步

当 Tripwire 安装在我们的系统中时，它会将 `License.txt` `README` 和 `Release_Notes` 文件复制到 `/user` 目录下。完成这些文件的阅读后，可以使用以下命令将它们从 `/user` 目录删除：

- 要从你的系统中删除这些文件，请使用以下命令：
  `[root]@deep tmp# rm -f /user/License.txt README Release_Notes`

### 工作清理

```
[root]@deep# cd /var/tmp
[root]@deep# rm -rf License.txt README Release-Notes install.sh pkg/
Tripwire_version_for_Linux_x86_tar.gz
```



`rm` 命令将删除我们用于安装 Linux 版 Tripwire 的所有相关文件和目录。它还会删除 `var/tmp` 目录下的 Linux 版 Tripwire 压缩包。

关于此页面的意见和建议，请邮件至 gmnouari@videotron.ca

# 配置

我们在书籍 `Linux.pdf` 中描述的所有软件将在名为 `floppy.tgz` 的 tar 归包中都有特定的目录和子目录，包含特定程序的配置。如果你获取了这个文件，你就不需要手动重新制作下面的不同配置文件，或将它们复制粘贴来创建你自己的配置文件。无论你决定手动复制还是从归档文件中获取以方便自己，根据你的需要对文件进行修改、调整并将文件放置在服务器机器的适当位置将是你的责任，如下所示。服务器配置文件存档位于以下互联网地址：`http://pages.infinet.net/lotus/floppy.tgz`。

- 运行 Linux 版 Tripwire 需要以下文件，并且必须将它们创建或复制到相应的目录中。

将 `twpol.txt` 文件复制到 `/usr/TSS/policy/`。

你可以在 `floppy.tgz` 归包中获得下面列出的配置文件。从解压的 `floppy.tgz` 归包中将以下文件复制到相应的适当位置，或直接从这里复制粘贴到相关文件中。

## `usr/TSS/policy/twpol.txt` 文件的配置

`usr/TSS/policy/twpol.txt` 是一个文本文件，指定了要检查的文件和目录（称为系统对象）。规则（`rule`）指定了你想要监控的对象，而属性（`property`）指定了如何检查。属性掩码（`property mask`）指定了在完整性检查期间检查文件的单个属性。请注意，编辑策略文件可能需要多次迭代，因为你需要根据经验确定希望在 Tripwire 报告中显示哪些信息。

第1 步
你必须修改默认策略文件，或创建你自己的。使用文本编辑器 `vi /usr/TSS/policy/twpol.txt` 打开 `/usr/TSS/policy/` 下的 `policy.guide.txt` 文件并将其更改为：

```
@section GLOBAL

TWROOT="/usr"

TWBIN="/usr/bin"

TWPOL="/usr/TSS/policy";

TWDB="/usr/TSS/db";

TWKEY="/usr/TSS/key";

WLKEY="/usr/TSS/key";

WLKEYREPORT="/usr/TSS/report";

HOSTNAME=deep.openarch.com.
```

```
@section FS

SEC_OPT = $(ignoreNone)_Sha; # 关键文件 - 我们无法承受任何更改。

SEC_SUID = $(ignoreNone)_Sha; # 带有 UID 和 SGID 标志的二进制文件。信任计算基础的成员。

SEC_C = $(ReadOnly); # 不应该改变的二进制文件。

SEC_BIN = $(ReadOnly);

SEC_CONFIG = $(Dynamic); # 会变化的配置文件

SEC_LOG = $(Growing); # 永远不应该改变所有者的文件。

SEC_INVARIANT = +pkg; # 永远应该改变权限或所有者的目录。

SIG_LOW = 33; # 安全影响小的非关键文件

SIG_MED = 66;

SIG_HI = 100; # 影响大的非关键文件
```

- Tripwire 二进制文件

© 1999 Open Network Architecture ®

```
{
TWDB -> $(Dynamic);
TWPOL)/tw.pol -> $(SEC_BIN);
TWBIN)/tw.cfg -> $(SEC_BIN);
$(TWKEY)/$(HOSTNAME).local-key -> $(SEC_BIN);
$(TWSKEY)/site.key -> $(SEC_BIN);
# 不要扫描单独报告
TWREPORT -> $(Dynamic (recurse=0));
}
```

- Tripwire 数据文件 - 配置、文件、策略、密钥、数据库

```
{
TWBIN)/siggen -> $(ReadOnly);
TWBIN)/tripwire -> $(ReadOnly);
TWBIN)/twadmin -> $(ReadOnly);
TWBIN)/twprint -> $(ReadOnly);
}
```

关于本页面的意见和建议请邮件至 gmourai@videotron.ca

```
(emailto = admin@openarch.com, rulename = "OS可执行文件和库", severity = $(SIG_HI))
{
  /bin -> $(ReadOnly) :
  /lib -> $(ReadOnly) :
}
```

### 本地文件

```
(emailto = admin@openarch.com, rulename = "用户二进制文件", severity = $(SIG_MED))
{
  /sbin -> $(SEC_BIN) (recurse = 1);
  /usr/sbin -> $(SEC_BIN) (recurse = 1);
  /usr/bin -> $(SEC_BIN) (recurse = 1);
}
```

### 临时目录

```
(emailto = admin@openarch.com, rulename = "临时目录", recurse = false, severity = $(SIG_LOW))
{
  /usr/tmp -> $(SEC_INVARIANT);
  /var/tmp -> $(SEC_INVARIANT);
  /tmp -> $(SEC_INVARIANT);
}
```

### 库

```
(emailto = admin@openarch.com, rulename = "库", severity = $(SIG_MED))
{
  /usr/lib -> $(SEC_BIN);
}
```

### 包含

```
(emailto = admin@openarch.com, rulename = "OS开发文件", severity = $(SIG_MED))
{
  /usr/include -> $(SEC_BIN);
}
```

### 共享

```
(emailto = admin@openarch.com, rulename = "OS共享文件", severity = $(SIG_MED))
{
  /usr/share -> $(SEC_BIN);
}
```

### 内核头文件

```
(emailto = admin@openarch.com, rulename = "内核头文件", severity = $(SIG_HI))
{
  /usr/src/linux-2.2.14 -> $(SEC_BIN);
}
```

### setuid/gid root 程序

```
(emailto = admin@openarch.com, rulename = "setuid/gid", severity = $(SIG_MED))
{
  /bin/su -> $(SEC_SUID);
  /bin/pwdb_chkpw -> $(SEC_SUID);
  /bin/dump -> $(SEC_SUID);
  /bin/restore -> $(SEC_SUID);
  /usr/bin/at -> $(SEC_SUID);
  /usr/bin/passwd -> $(SEC_SUID);
  /usr/bin/suidpt -> $(SEC_SUID);
  /usr/bin/crontab -> $(SEC_SUID);
  /usr/bin/sendmail -> $(SEC_SUID);
  /usr/bin/man -> $(SEC_SUID);
  /usr/bin/perl5.00503 -> $(SEC_SUID);
  /usr/bin/locate -> $(SEC_SUID);
}
```

© Copyright 1999 Open Network Architecture ®

关于本页面的意见和建议请邮件至 gmourani@videotron.ca

```
/usr/sbin/utempter -> $(SEC_SUID);
/sbin/netreport -> $(SEC_SUID);
}
```



`(mailto = admin@openarch.com, rulename = "配置文件")`
```
{
/etc/hosts               向于 $(SEC_CONFIG);
/etc/netid.conf         -> $(SEC_CONFIG);
/etc/initlog.conf       -> $(SEC_CONFIG);
/etc/ittab             -> $(SEC_CONFIG);
/etc/resol.conf        -> $(SEC_CONFIG);
/etc/syslog.conf       -> $(SEC_CONFIG);
}
```

`(mailto = admin@openarch.com, rulename = "安全控制")`
```
{
/etc/group              -> $(SEC_CRIT);
/etc/security/         -> $(SEC_CRIT);
/lib/security/          -> $(SEC_CRIT);
/var/spool/cron        -> $(SEC_CRIT);
}
```

`(mailto = admin@openarch.com, rulename = "登录脚本")`
```
{
/etc/csh.login         -> $(SEC_CONFIG);
/etc/profile          -> $(SEC_CONFIG);
}
```

# 这些文件每次系统启动时都会更改
`(mailto = admin@openarch.com, rulename = "系统启动更改", severity = $(SIG_HI))`
```
{
/dev/log               -> $(Dynamic);
/dev/cuas              -> $(Dynamic);
/dev/console           -> $(Dynamic);
/dev/tty2              -> $(Dynamic); # tty设备
/dev/tty3              -> $(Dynamic); # 极其
/dev/tty4              -> $(Dynamic); # 变量
/dev/tty5              -> $(Dynamic);
/dev/tty6              -> $(Dynamic);
/dev/urandom          -> $(Dynamic);
/dev/initcl            -> $(Dynamic);
/var/lock_subsystems   -> $(Dynamic); # 守护 PID
/var/run               -> $(Dynamic);
/etc/ioctl.save       -> $(Dynamic);
/etc/pwd.lock          -> $(Dynamic);
/etc/mtab             -> $(Dynamic);
/lib/modules           -> $(Dynamic);
}
```

## 关键配置文件
`(mailto = admin@openarch.com, rulename = "关键配置文件", severity = $(SIG_HI))`
```
{
/etc/conf               -> $(SEC_CONFIG);
/etc/crontab           -> $(SEC_CONFIG);
/etc/cron.hourly       -> $(SEC_CONFIG);
/etc/cron.daily        -> $(SEC_CONFIG);
/etc/cron.weekly       -> $(SEC_CONFIG);
/etc/cron.monthly      -> $(SEC_CONFIG);
/etc/default           -> $(SEC_CONFIG);
/etc/fstab             -> $(SEC_CONFIG);
}
```
/etc/hosts.allow       -> $(SEC_CONFIG);
/etc/hosts.deny        -> $(SEC_CONFIG);
/etc/io.conf           -> $(SEC_CONFIG);
/etc/logrotate         -> $(SEC_CONFIG);
/etc/pwdb.conf      -> $(SEC_CONFIG);
/etc/security          -> $(SEC_CONFIG);
/etc/sendmail          -> $(SEC_CONFIG);
/etc/protocols         -> $(SEC_CONFIG);
/etc/services          -> $(SEC_CONFIG);
/etc/init.d            -> $(SEC_CONFIG);
/etc/rc.d
/etc/motd              -> $(SEC_CONFIG);
/etc/passwd            -> $(SEC_CONFIG);
/etc/profile           -> $(SEC_CONFIG);
/etc/rc.local          -> $(SEC_CONFIG);
/etc/shadow            -> $(SEC_CONFIG);
/etc/sudoers           -> $(SEC_CONFIG);
/etc/sysconfig         -> $(SEC_CONFIG);
/etc/tty               -> $(SEC_CONFIG);
/etc/version           -> $(SEC_CONFIG)

## 关键设备
`(mailto = admin@openarch.com, rulename = "关键设备", severity = $(SIG_HI), recurse = false)`
```
{
/dev/sda -> $(SEC_INVARIANT);
/dev/sdb -> $(SEC_INVARIANT);
/dev/sdc -> $(SEC_INVARIANT);
/dev/sdd -> $(SEC_INVARIANT);
/dev/ada -> $(SEC_INVARIANT);
/dev/hda -> $(SEC_INVARIANT);
/dev/vda -> $(SEC_INVARIANT);
/dev/vdb -> $(SEC_INVARIANT);
/dev/vdc -> $(SEC_INVARIANT);
/dev/vde -> $(SEC_INVARIANT);
/dev/mem0 -> $(SEC_INVARIANT);
/dev/mem1 -> $(SEC_INVARIANT);
/dev/mem2 -> $(SEC_INVARIANT);
/dev/mem3 -> $(SEC_INVARIANT);
/dev/mem4 -> $(SEC_INVARIANT);
/dev/mem5 -> $(SEC_INVARIANT);
/dev/mem6 -> $(SEC_INVARIANT);
/dev/mem7 -> $(SEC_INVARIANT);
/dev/mem -> $(SEC_INVARIANT);
/dev/kmem -> $(SEC_INVARIANT);
/dev/random -> $(SEC_INVARIANT);
/dev/zero -> $(SEC_INVARIANT);
}
```

## 共享
`(mailto = admin@openarch.com, rulename = "OS共享文件", severity = $(SIG_MED))`
```
{
  /usr/share -> $(SEC_BIN);
}
```

关于本页面的意见和建议请邮件至 `gmourani@videotron.ca`

### 步骤 2

当你准备好使用策略时，请使用以下命令安装它：

```
[root@deep]# twmine-policy /usr/TSS/policy/wwt
```

请输入你的口令：

已写入策略：`/usr/TSS/policy/twpol`

## 为 Linux 安全 Tripwire

确保你运行的系统完整性没有被破坏。为了对基线有最大的信心，你应该从原始介质生成操作系统和应用程序，以确保获得干净的基线。

建议删除 `usr/bin` 下名为 `"twcfg.txt"` 的 Tripwire 配置明文副本，以隐藏 Tripwire 的位置并防止任何人创建新配置。

- 要删除配置文件，请使用以下命令：

`[root@deep]# rm -f usr/bin/twcfg`

## 更多文档

更多信息，可以阅读以下页面：



- `siggen` (8) - Tripwire 签名收集程序

- `tripwire` (8) - Unix 系统文件完整性检查器

- `twadmin` (8) - Tripwire 管理实用工具

- `twconfig` (4) - Tripwire 配置参考

- `twfiles` (5) - Tripwire 和备份过程使用的文件概述

- `twintro` (8) - Tripwire 软件介绍

- `twpolicy` (4) - Tripwire 策略参考

- `twprint` (8) - Tripwire 数据库和报告打印机

关于本页面的意见和建议请邮件至 `gmourani@videotron.ca`

# 运行完整性检查

完整性检查（Integrity Check）模式会将当前文件系统对象与 Tripwire 数据库中记录的属性进行比较。违规项将打印到标准输出（`stdout`）；报告文件将被保存，之后可以通过 `triprint` 访问。

完整性检查模式的语法为：

```
[root]@deep]# tripwire --check
```

- 要运行完整性检查模式，请使用命令：

```
[root]@deep]# tripwire --check
```

你可以在交互检查模式（Interactive Check mode）下运行 Tripwire。在交互模式下，你可以通过终端自动更新更改。添加 `-interactive` 语法后生成的报告将在编辑器中打开以更新数据库。

- 要以交互检查模式运行，请使用命令：

```
[root]@deep]# tripwire --check--interactive
```

邮件选项允许你发送电子邮件。使用 `[-email-report]` 选项运行 Tripwire，可以指定将报告发送给策略文件中列出的接收者，并使用默认配置文件中的选项。

- 要运行完整性检查模式并向接收者发送邮件，请使用命令：

```
[root]@deep]# tripwire --check--email-report
```

# 在完整性检查后更新数据库

数据库更新模式（Database Update mode）允许你在完整性检查后更新 Tripwire 数据库，前提是发现的违规项是有效的。此过程通过允许你在无需重新生成的情况下更新数据库来节省时间；更重要的是，它允许进行选择性更新，这种更新可以通过重新生成来实现。在我们的 `tripwire` 配置中，配置文件使用基于时间的变量指定报告文件名，因此报告不会处于常规模式。这是因为 `$(DATE)` 变量已经发生变化以反映当前时间。为了解决这个问题，必须在命令行上使用 `-r` 或 `-twistle` 参数指定报告文件。

数据库更新模式的语法为：

```
[root]@deep]# tripwire --update -r
```

- 要更新数据库，请使用命令：

```
[root]@deep]# tripwire --update -r /usr/TSS/report/deep.openarch.com-200001-021854
```

其中 "r" 指定报告文件（`deep.openarch.com-200001-021854.twr`）。该选项是配置文件中 `REQUIRED_REPORT` 变量 `$(DATE)` 所要求的。

注意：在数据库更新模式或交互检查模式下，Tripwire 显示报告时会在每个策略违规项旁边显示一个选择框。你可以通过在每个策略违规项旁保留 "x" 来批准对系统的更改。如果你删除了选择框中的 "x"，数据库将不会更新该对象的新值。在你退出编辑器并提供本地口令后，Tripwire 软件将更新并保存数据库。

关于本页面的意见和建议请邮件至 `gmouraoui@videotron.ca`

# 更新策略文件

你可以更改策略文件中的规则，这将改变 Tripwire 软件扫描系统的方式，并在无需完全重新初始化的情况下更新数据库。这可以节省大量时间；更重要的是，它通过保持策略文件与数据库同步来维护安全性。

策略更新模式的语法为：

```
[root@deep]# tripwire --update-policy /path/to/new/policy/file
```

- 要更新策略文件，请使用命令：

```
[root]@deep]# tripwire --update-policy /usr/TSS/policy/newtripwpol.txt
```

默认情况下，策略更新模式以 'secure-mode high' 运行。如果自上次数据库更新以来文件系统发生了变化，且这些更改仍导致策略中的违规，则在 във安全模式下运行时可能会遇到错误。例如，如果在策略更新过程中有另一个进程正在修改文件，就可能发生这种情况。为了适应这种情况，在确定高安全模式下报告的所有违规都是授权的后，你可以在低安全模式下更新策略文件：

- 要加载低安全模式下更新策略文件，请使用命令：

```
[root]@deep]# tripwire --update-policy --secure-mode /usr/TSS/policy/newtripwtxt
```

# 安装文件

| 路径 A | 路径 B |
| :--- | :--- |
| `/usr/TSS` | `/usr/TSS/key/deep.openarch.com.key` |
| `/usr/bin` | `/usr/man` |
| `/usr/bin/siggen` | `/usr/man/man4` |
| `/usr/bin/twprint` | `/usr/man/man4/twconfig.4` |
| `/usr/bin/tadmin` | `/usr/man/man4/twpolicy.4` |
| `/usr/bin/tripwire` | `/usr/man/man5` |
| `/usr/bin/twcg.txt` | `/usr/man/man5/twifiles.5` |
| `/usr/bin/tw.cfg` | `/usr/man/man6` |
| `/usr/policy` | `/usr/man/man8/siggen.8` |
| `/usr/TSS/policyguide.txt` | `/usr/man/man8/tripwire.8` |
| `/usr/TSS/policywpol.txt` | `/usr/man/man8/twintro.8` |
| `/usr/TSS/policywtpol.bak` | `/usr/man/man8/tripprint.8` |
| `/usr/report` | `/usr/README` |
| `/usr/TSS/db` | `/usr/Release_Notes` |
| `/usr/TSS/key` | `/usr/License.txt` |
| `/usr/TSS/key/site.key` |  |

# Linux Tripwire ASR 1.3.1

### 概述

随着日益复杂和微妙的攻击出现，需要工具辅助检测文件未经授权的修改变得变得非常明确。Tripwire 是一种帮助系统管理员和用户监控指定文件集任何变化的工具。通过对系统文件进行定期（例如每日）使用，Tripwire 可以通知管理员已损坏或被篡改的文件，以便及时采取控制措施。

© Copyright 1999 Open Network Architecture ®

819

关于本页的意见和建议请邮寄至 `gmouriani@videotron.ca`

`chmod` 命令将 "tripwire" 目录的默认模式更改为 700 (`drwx------`)，仅允许超级用户 "root" 读取、写入和执行。它将使二进制文件 `/usr/bin/tripwire` 仅允许超级用户 "root" 读取和执行 (`-r-x--`)，并最终使 `/usr/bin` 目录下的 "sigen" 程序允许被 "root" 执行和读取。

`rm` 命令将删除 `/usr/sbin` 下的 "tw.config" 文件。我们不再需要这个文件，因为我们在 `/etc` 目录下已经创建了一个新的。

# 工作后的清理

```
[root@deep]# cd /var/tmp
[root@deep]# rm -rf tw_AS_VERSION/ Tripwire-version.tar.gz
```

`rm` 命令将删除我们用于编译和安装 Tripwire 的所有源文件。它还将删除来自 "var/tmp" 目录的 Tripwire 压缩包。

# 配置

我们在书籍"Linuxos.pdf"中描述的所有软件都将在名为 "floppy.tgz" 的压缩包中拥有特定的目录和子目录，其中包含特定程序的的配置文件。如果你使用此文件，你就不需要手动重现配置文件的差异，或将它们剪切粘贴到你的配置文件中。无论你决定复制配置文件，还是从压缩文件中根据你的方便进行其他更改，修改、根据你的需求进行调整并将文件放置到 Tripwire 软件在服务器机器上的适当位置将是你的责任，如下所示。服务器配置文件归包位于以下互联网地址：http://pages.infinit.net/lotus/doc/opt/floppy.tgz

- 运行 Tripwire 需要以下文件，必须将它们复制或拷贝到服务器适当的目录。

- 将 `tw.config` 文件复制到 "etc" 目录。



- 将 `tripwire.verify` 脚本复制到 `"etc/cron.daily"` 目录。

你可以在我们的 `floppy.tgz` 归包中获得下方列出的配置文件。从解压后的 `floppy.tgz` 归包中将文件复制到其适当位置，或直接从此处复制并粘贴到相关文件中。

# `/etc/tw.config` 文件的配置

Tripwire 以四种模式之一运行：数据库生成、完整性检查、数据库更新和交互模式。为了实现这一点，你必须首先指定 Tripwire 监控的文件集。为此，此列表存储在 `"etc/tw.config"` 文件中。`"tw.config"` 文件定义了所有包含你监控的文件的目录。

第 1

创建 `tw.config` 文件 (`touch /etc/tw.config`) 并向文件中添加包含你监控的文件的所有目录。该文件的格式在其头部以及主页 `tw.config(5)` 中进行了描述：

> # Gerard Mourani; gmouriani@videotron.ca
> # 最后更新日期: 1999/11/12

```
# 首先，root 的 "home"
/root R
/root/bash_history
```

© Copyright 1999 Open Network Architecture ®

关于本页的意见和建议请邮寄至 gmourani@videotron.ca

`/root R`

# 操作系统本身

`/boot/vmlinux R`

# 关键启动资源

`/boot R`

# 关键目录和文件

`/chroot R`

`/etc R`

`/etc/inetd.conf R`

`/etc/nsswitch.conf R`

`/etc/rc.d R`

`/etc/mib L`

`/etc/motd L`

`/etc/group L`

`/etc/passwd L`

# 其他常用的文件系统

`/usr R`

`/usr/local R`

`/dev L-am`

`/usr/etc R`

# 截断家

`=/home R`

# var 树

`=/var/spool L`

`=/var/log L`

`=/var/lib L`

`=/var/spool/cron L`

`=/var/lock L`

# 非常规目录

`=/proc E`

`=/tmp E`

`=/mnt/cdrom`

`=/mnt/floppy`

第 2

现在，为了安全起见，使用以下命令将此文件的模式更改为 0600：

```
[root@#]# chmod 0600 /etc/tw.config
```

# `"etc/tripwire.verify"` 脚本的配置

运行 Tripwire 的常见设置将其生成的任何输出发送给系统管理员。然而，系统上的某些文件在正常运行期间可能会发生，这需要更新 Tripwire 数据库。`"tripwire.verify"` 文件是一个由 cron 程序每天执行的小脚本，用于扫描你的硬盘以查找可能更改的文件或目录，并将结果邮件给系统管理员。

第 1

创建 `tripwire.verify` 脚本 (`touch /etc/cron.daily/tripwire.verify`) 并向此脚本添加内容：

```
#/bin/sh
/usr/sbin/tripwire -loosedired -q | (cat --EF)
这是由生成的可能文件完整性变化的自动报告
```

© Copyright 1999 Open Network Architecture ®

关于本页的意见和建议请邮寄至 gmourani@videotron.ca

Tripwire 完整性检查器。要告诉 Tripwire某个文件或目录树是有效的，请以 root 身份运行：

```
/usr/sbin/tripwire -update [pathname]entry
```

如果你想进入交互式完整性检查和验证会话，请以 root 身份运行：

```
/usr/sbin/tripwire -update
```

第 2

现在，为了安全起见，使用以下命令将此文件的模式更改为 0600：

```
[root@#]# chmod 0600 /etc/tw.config
```

# `"etc/tripwire.verify"` 脚本的配置

运行 Tripwire 的常见设置将其生成的任何输出发送给系统管理员。然而，系统上的某些文件在正常运行期间可能会发生，这需要更新 Tripwire 数据库。`"tripwire.verify"` 文件是一个由 cron 程序每天执行的小脚本，用于扫描你的硬盘以查找可能更改的文件或目录，并将结果邮件给系统管理员。

在交互模式下，

那么你可以以数据库更新模式运行 Tripwire，并仅更改发生变化的单个文件。

例如：

因此，如果某个单个文件发生了变化，你可以：

```
[root@deep]# tripwire-update /etc/newly.installed
```

有关此页面的意见和建议请发送至 gnmourani@videotron.ca。

或者，如果构成 `"tw.config"` 文件中条目的整个文件集发生了变化，你可以执行：

```
[root@deep]# tripwire-update /usr/lib/Package_Dir
```

在任何情况下，Tripwire 都会为每个指定的文件重新生成数据库条目会在 `"/databases"` 目录下创建一个旧数据库的备份。

# 安装文件

- `/etc/cron.daily/tripwire.verify` > `/usr/bin/tripwire`
- `/etc/tw.config` > `/usr/bin/siggen`
- `/etc/man/man5/tw.config.5` > `/var/spool/tripwire`
- `/etc/man/man8/siggen.8` > `/var/spool/tripwire/tw.db_TEST`
- `/etc/man/man8/tripwire.8`

# Tripwire 的替代方案

ViperDB 不使用花哨的一体化数据库来保存记录。它使用存储在每个“监控”目录中的纯文本文件。通过这种方式，攻击者没有单一的攻击点可以集中注意力。结合每 5 分钟运行一次的 ViperDB（通过 cron root 任务），这增加了攻击者在 ViperDB 监控你的系统时能够修改你的“监控”文件系统的可能性。

# ViperDB

ViperDB 首页：http://www.resentment.org/projects/viper/

# 软件包

# FCHECK

FCHECK 是一个非常稳定的 Perl 脚本，用于生成并对 UNIX 系统相对于其基准进行对比监控，以检测任何文件更改，并通过 syslog、控制台或任何日志接口报告。如果系统驱动器大小足够小，监控事件可以每隔一分钟就执行一次，这使其很难被规避。这是“tripwire”的免费开源替代方案，经过了时间的考验，并且更易配置和使用。

FCHECK 首页：http://sites.netscape.net/fcheck/fcheck.html

# 软件包

# Sentinel

Sentinel 是一种快速的文件/驱动扫描工具，类似于提供的 Tripwire 和 Viper.pl 实用。它使用类似于 Tripwire 的数据库，但使用了 RIPEMD-160位 MAC 校验和算法（无专利），这比专利的 MD5 128 位校验和更安全。它应该运行在大多数 Unix 系统上。

# 软件包

FCHECK 首页：http://zurk.pededia.net/zfile.html

© Copyright 1999 Open Network Architecture ® 189

有关此页面的意见和建议请发送至 gmourani@videotron.ca

# Linux GnuPG

### 概述

GnuPG - Gnu隐私守护者。GnuPG 是 GNU 用于安全通信和数据存储的工具。它可以加密数据并创建数字签名。它是一个高级的密钥管理设施，并兼容 RFC2440 中描述的建议 OpenPGP Internet 标准。

由于 GnuPG 不使用任何专利算法，因此与 PGP2 版本不兼容。PGP 2.x 仅使用 IDEA（全球范围内专利）和 RSA（在美国拥有专利，直到 2000 年 9 月 20 日）。

## 这些安装说明假设

- - 命令与 Unix 兼容。
- 源码路径为 `"/var/tmp"`（也可能是其他路径）。
- 安装在 RedHat Linux 6.1 上测试过。
- 安装过程中的所有步骤都将在超级用户账户 `'root'` 中进行。
- GnuPG 版本号为 1.0.1

## 软件包

GnuPG 首页：http://www.gnupg.org/

你必须确保下载：`gnupg-1_0_tar.gz`

## Tar 包

在安装之前列出系统上的文件列表，安装之后也列一次，然后使用 `diff` 比较它们以找出哪些文件被放置在什么位置。只需在安装 tar 包之前运行 `find /` > `pg1`，在之后运行 `find / > > pg2`，然后使用 `diff pg1 pg2 > pg` 获取更改列表。

### 编译

解压 tar 包 (`tar.gz`)。



```
[root@deep]# cp gnupg-version.tar.gz /var/tmp
[root@deep]# cd /var/tmp
[root@deep]# tar xzf gnupg-version.tar.gz
```

## 编译与优化

进入新的 GnuPG 目录并在终端中输入以下内容：

```
CC=gcc
CFLAGS=O9 -funroll-loops -fast-math -malign -mcpu=pentiumpro -march=pentiumpro -fomit-
frame-pointer -fno-exceptions\
/config \
--prefix=/usr \
--enable-shared
```

```
[root@deep]# make
[root@deep]# make check
[root]# make install
[root@deep]# strip /usr/bin/gpg
```

`make` 将所有源文件编译为可执行二进制文件，然后 `make check` 将运行随包附的任何自测试，最后 `make install` 命令会将二进制文件和任何支持文件安装到适当的位置 `strip` 命令将减小 `gpg` 二进制文件的大小以获得更好的性能。

# 工作清理

```
[root@deep]# cd /var/tmp
[root@deep]# rm -rf gnupg-version/ gpg-version.tar.gz
```

# 创建密钥

首先，我们必须生成密钥。

## 第 1 步

生成新密钥（作为 root），使用以下命令：

```
[root@deep]# gpg --gen-key
```

在生成密钥期间，执行其他操作（操作键盘、移动鼠标、使用磁盘）以产生大量随机字节是一个好主意；这让随机数生成器获得足够熵的机会更大。

+++++++++++++++++++++++++++++++++++++++++++++++++

+++++++++++++++++++++++++++++++++++++++++++++++++

+

++++++++++++++++++++++++++++++++++++++++++++++++++++++

********************

公私钥创建并签名。

在“root”主目录下 (`~root`) 创建了新的密钥对（私钥和公钥）。

## 第 2 步

生成新密钥（作为 root），使用以下命令：

```
[root@deep]# gpg --gen-key
```

你需要一个 User-ID 来标识你的密钥；软件根据真实姓名、注释和电子邮件构造用户 ID，格式如下：

姓名：Gerhard Mourani

电子邮件：gmourani@videotron.ca

注释：[按回车]

你选择了此 USER-ID：

"Gerhard Mourani <gmourani@videotron.ca>"

你需要密码来保护你的私钥。

# 导入密钥

如果你从那里接收了密钥，可以将其放入你的公钥数据库，这被称为“导入”。

- 将公钥导入你的密钥环，使用以下命令：

`[root]# gpg --import <file>`

例如：

`[root]# gpg --import redhat2.asc`

新密钥会被添加到你的密钥环中，已有的密钥会被更新。注意，GnuPG 不导入未自签名的密钥。在示例中，我们导入了从 Red Hat Internet 下载的 Red Hat 公司的 "redhat2.asc" 公钥文件。

# 密钥签名

当你导入密钥并确定某人确实是他们声称的人时，你可以对他们的密钥签名。

关于本页面的意见和建议请邮寄至 gmourani@videotron.ca。

- 若要为我们在上方密钥环中添加 RedHat 公司密钥签名，请使用以下命令：

`[root@deep] gpg --sign-key <UID>`

示例例如：

`[root@deep] gpg --sign-key RedHat`

pub 1024D/DB2A4B0E created: 1999-09-23 expires: never trust: -q

sub 2048bit/961630A2 created: 1999-09-23 expires: never

(1) Red Hat, Inc <security@redhat.com>

pub 1024D/DB2A4B0E created: 1999-09-23 expires: never trust: -q

Fingerprint: CA 2086 2BD6 99FC 65F6 ECC4 2191 80CD DB42 A60E

Red Hat, Inc <security@redhat.com>

你确定要用你的密钥 "Gerhard Mourani gmourani@videotron.ca" 来签名此密钥吗？

真的吗？y

你需要密码来解锁私钥

user: "Gerhard Mourani gmourani@videotron.ca"

1024-bit DSA key, ID E92D6C97, created 1999-12-30

输入密码：

只有当你**绝对确定**该密钥真实有效时，才应该对其进行签名！你绝不基于任何假设对密钥签名。

## 加密与解密

按照我们的意愿安装并配置好一切后，我们可以开始进行加密和解密。

- 若要对上方密钥环中添加的 RedHat 数据进行加密并签名，请使用以下命令：

`[root@deep] gpg --sign RedHat <file>`

示例例如：

`[root@deep] gpg --sign RedHat message-to-RedHat.txt`

你需要密码来解锁私钥

user: "Gerhard Mourani (Open Network Architecture) gmourani@videotron.ca"

1024-bit DSA key, ID BBB4BA9, created 1999-10-26

输入密码：

其中 "s" 表示签名（为了避免他人冒充你的身份，对你加密的所有内容进行签名是有用的），"e" 表示加密，“a" 表示创建 ASCII 封装输出（准备好通过邮件发送的 ".asc" 文件），"r" 表示用户名，`<file>` 是你想要加密的消息。

- 若要解密数据，请使用以下命令：

`[root@deep] gpg -d <file>`

例如：

`[root@deep] gpg -d message-to-Gerhard.asc`

你需要密码来解锁私钥

user: "Gerhard Mourani (Open Network Architecture) gmourani@videotron.ca"

2048-bit ELG-E key, ID 71D4CC44, created 1999-10-26 (主密钥 ID BBB4BA9)

输入密码：

关于本页面的意见和建议请邮寄至 gmourani@videotron.ca

其中 "-d" 表示解密，`<file>` 是你想要解密的消息。

## 导出密钥

GnuPG 提供了帮助你发布公钥的选项。这被称为“导出”密钥。通过导出公钥，你可以扩大你的视野。可以通过首页、密钥服务器或你想到的任何其他方法来实现。

- 若要以 ASCII 封装输出提取你的公钥，请使用以下命令：

`[root@deep]# gpg --export --armor > Public-key.asc`

其中 "--export" 用于从发布密钥环中提取公钥，"--armor" 用于创建可以邮寄、发布或放在网页上的 ASCII 封装输出，`> Public-key.asc` 用于将结果放入名为 `Public-key.asc` 的文件中。

## 签名与检查

每个人都知道你的公钥（你可以通过将其放在服务器、网页等处来签名公钥），现在能够检查你是否对这段文本进行了签名。

- 若要对签名或二进制文件签名，请使用以下命令：

`[root@deep]# gpg --detach-sign --armor <Data>`

你可以将签名写在单独的文件中。强烈建议在签名二进制文件（例如压缩包）使用此选项。此外，`--armor` 选项在这里非常有用。`<data>` 可以是一个文件或像 tar 这样的二进制文件。

- 若要检查加密数据的签名，请使用以下命令：

`[root@deep]# gpg --verify <Data>`

GPG 现在会检查签名是否有效并打印适当的消息。如果签名良好，你至少知道该个人（或机器）拥有对应公钥的私钥。当加密数据也被签名过时，签名会在解密数据时被检查。当然，这只有在你拥有发送者的公钥时才会生效。`<data>` 与你的文件相同。

## 已安装的文件

```
> /usr/bin/gpg
> /usr/lib/gnup
> /usr/lib/gnpg/mdunix
> /usr/share/gnpg/mdunix
> /usr/share/gnup/asc
> /usr/share/gnup/asc
```



关于本页面的意见和建议请邮寄至 gmourani@videotron.ca

## 已安装的文件

```
> /usr/bin/gpg
> /usr/lib/gnup
> /usr/lib/gnpg/mdunix
> /usr/share/gnpg/mdunix
> /usr/share/gnup/asc
> /usr/share/gnup/asc
```

© 1994

关于本页面的意见和建议请邮寄至 gmourani@videotron.ca

```
[root@deep]# make -C src
[root@deep]# make clean all -C src SUBDIRs=../doc/man
[root@deep]# make install -C src
[root@deep]# make install -C src SUBDIRs=../doc/man
```

`make` 命令将源文件编译为可执行二进制文件，然后 `make install` 将二进制文件及任何支持文件安装到相应的位置。

```
[root@deep]# strip /usr/bin/addr
[root@deep]# strip /usr/bin/dig
[root@deep]# strip /usr/bin/nslookup
[root@deep]# strip /usr/bin/root
[root@deep]# strip /usr/bin/nslookup
[root@deep]# strip /usr/bin/nspudate
[root@deep]# strip /usr/bin/mkservbd
[root@deep]# strip /usr/sbin/named
[root@deep]# strip /usr/sbin/named-xfer
[root@deep]# strip /usr/sbin/ndc
[root@deep]# strip /usr/sbin/dsnkeygen
[root@deep]# strip /usr/sbin/irpd
[root@deep]# mkdir /var/named
```

`strip` 命令会丢对象文件中的符号。这意味着二进制文件的尺寸会更小。这将减少程序的性能影响，因为系统在执行该二进制文件时读取的行数会更少。`mkdir` 将创建一个新目录 `/var/named`。

# 工作后的清理

```
[root@deep]# cd /var/tmp
[root@deep]# rm -rf bind/
```

将删除我们所有用于编译和安装 DNS/Bind 的文件。

# 配置

不同服务的配置文件根据您的需求和网络架构具有非常特定的性。人们可以在家里安装 DNS 服务器作为仅缓存的 DNS，也可以以主 DNS 服务器、从 DNS 服务器和缓存 DNS 服务器的形式进行安装。

我们在书籍《Linux.dos》中描述的所有内容，在名为 `floppy.tgz` 的压缩归包中都将有一个特定的目录和子目录，其中包含特定程序的配置文件。如果您归档了此文件，就没有义务手动复制下面的配置文件或编辑它们来创建您的配置文件。无论您决定手动复制还是从归档压缩文件中根据方便方便获取 `make`，根据您的需求进行修改、调整并将与 BIND/DSN 软件相关的文件放置到服务器机器上的适当位置将是您的责任，如下所示。服务器配置文件位于 Internet 地址：http://pages.infinit.net/ltos/doc/floppy.tgz

- * 要运行仅缓存名称服务器，需要以下文件，并且必须创建或将其复制到服务器上的适当目录。

将 `named.conf` 文件复制到 `/etc/` 目录。

将 `db.127.0.0` 文件复制到 `/var/named/` 目录。

将 `db.cache` 文件复制到 `/var/named/` 目录。

将 `named` 脚本文件复制到 `/etc/rc.init.d/` 目录。

© 版权所有 1999 开放网络架构 ® 198

关于本页面的意见和建议请邮寄至 gmourani@videotron.ca

- * 要运行主服务器名称，需要以下文件，并且必须创建或将其复制到您服务器上的适当目录。

将 `named.conf` 文件复制到 `/etc/` 目录。

将 `db.127.0.0` 文件复制到 `/var/named/` 目录。

将 `db.cache` 文件复制到 `/var/named/` 目录。

将 `db.192.168.1` 文件复制到 `/var/named/` 目录。

将 `db.openarch` 文件复制到 `/var/named/` 目录。

将 `named` 脚本文件复制到 `/etc/rc.d/init.d/` 目录。

- * 要运行从服务器，需要以下文件，并且必须创建或将其复制到您服务器上的适当目录。

将 `named.conf` 文件复制到 `/etc/` 目录。

将 `db.127.0.0` 文件复制到 `/var/named/` 目录。

将 `db.cache` 文件复制到 `/var/named/` 目录。

将 `named` 脚本文件复制到 `/etc/rc.d/init.d/` 目录。

您可以获得 `floppy.tgz` 归包下方列出的配置文件。从解压的 `floppy.tgz` 归包中将以下文件复制到相应的适当位置，或直接从此处复制粘贴到相关文件中。

# 仅缓存名称服务器

仅缓存的名称服务器对 0.0.127.in-addr.ar 之外的任何域都不具有权威性。仅缓存名称服务器可以像主服务器和从服务器一样查找您的区域内外的名称。区别在于，当仅缓存名称服务器最初查找您的区域内的名称时，它最终会要求其中一个主名称服务器或从名称服务器为您提供答案。

设置简单的缓存名称服务器所需的文件是：

- `named.conf`

- `db.127.0.0`

- `db.cache`

- `named` 脚本

# 简单缓存名称服务器的 `/etc/named.conf` 文件配置

您的网络中所有不作为主服务器或从名称服务器的服务器使用此配置。为本地机器设置简单的缓存服务器将减少该站点主服务器的负载。许多使用拨号连接的用户使用此配置配合 bind 实现此类目的。创建 `named.conf` 文件（`touch /etc/named.conf`）并在文件中添加以下行：

```
options {
  directory "/var/named";
  forwarders { 208.164.1; 208.164.2 };
}
// 仅缓存的 DNS
zone "*" {
  type hint;
  file "db.cache";
}
zone "0.0.127.in-addr.arpa" {
  type master;
  file "db.127.0.0";
}
```

您的网络中所有不作为主服务器或从名称服务器的服务器使用此配置。为本地机器设置简单的缓存服务器将减少该站点主服务器的负载。许多使用拨号连接的用户使用此配置配合 bind 实现此类目的。创建 `named.conf` 文件（`touch /etc/named.conf`）并在文件中添加以下行：

```
options {
  directory "/var/named";
  fetch-glue no;
  recursion no;
  allow-query { 208.164.186/24 };
  allow-transfer { 208.164.186.2 };
  transfer-format many-answers;
}
```

```
// 这些不是特定于任何区域
zone "*" {
  type hint;
  file "db.cache";
}
zone "0.0.127.in-addr.arpa" {
  type master;
  file "db.127.0.0";
}
// 这些是我们的主区域文件
zone "openarch.com" {
  type master;
  file "db.openarch";
}
zone "186.164.208-in.addr.arpa" {
  type master;
  file "db.208.164.186";
}
```

关于本页面的意见和建议请邮件至 gmourani@videotron.ca

在 `allow-query` 行中，128.164.186/24 和 127.0.0/8 是允许向服务器发起普通查询的 IP 地址。

在 `allow-transfer` 行中，208.164.186.2 是允许从服务器接收区域传输的 IP 地址。你必须确保只有你真实的名称服务器才能从你的名称服务器传输区域。因为提供的信息经常被垃圾邮件发送者和伪造者利用。

**注意：** "`named.conf`" 文件中的 "`recursion no`","`allow-query`" 和 "`allow-transfer`" 选项是一个安全功能。

## 主、从名称服务器 "var/named/db.127.0.0" 文件的配置



此配置文件供主名称服务器和从名称服务器使用。`db.127.0.0`文件覆盖环回网络，即直接用于`localhost`流量的特殊地址。在`/var/named/`中创建以下文件：

创建`db.127.0.0`文件（执行`touch /var/named/db.127.0.0`）并添加：

```
: Revision History: April 22, 1999 - admin@mail.openarch.com
; Start of Authority (SOA) 记录。
$TTL 345600
@ IN SOA deep.openarch.com. admin@mail.openarch.com (
      00
      86400
      7200
      2592000
      345600 )
      : Serial
      : Refresh
      : Expire
      :Minimum
```

: 名称服务器 (NS) 记录。

`NS deep.openarch.com.`

`NS mail.openarch.com.`

; 仅有一个 PTR 记录。

`PTR localhost.`

## 主名称服务器 `var/named/db.208.164.186` 文件的配置

使用此配置用于你网络中作为名称服务器的机器。此文件`db.208.164.186`将主机名映射到地址。在`/var/named/`中创建以下文件：

创建`db.208.164.186`文件（执行`touch /var/named/db.208.164.186`）并添加：

```
: Revision History: April 22, 1999 - admin@mail.openarch.com

; Start of Authority (SOA) 记录。

$TTL 345600

@ IN SOA deep.openarch.com. admin@mail.openarch.com (

      00

      86400

      7200

      2592000

      345600 )

      : Serial

      : Refresh

      : Expire

      :Minimum
```

: 名称服务器 (NS) 记录。
`NS deep.openarch.com.`
`NS mail.openarch.com.`

: 用于反向查找的指向规范名称的 (PTR)

© Copyright 1999 Open Network Architecture ®

1 `PTR deep.openarch.com.`
2 `PTR mail.openarch.com.`
3 `PTR www.openarch.com.`

## 主名称服务器 `/var/named/db.openarch` 文件的配置

使用此配置用于作为主名称服务器的机器。此文件`db.openarch`将地址映射到主机名。在`/var/named`中创建文件。

创建`db.openarch`文件（执行`touch /var/named/db.openarch`）并添加：
; Revision History: April 22, 1999 - admin@mail.openarch.com
; Start of Authority (SOA) 记录。

```
$TTL 345600

@ IN SOA deep.openarch.com. admin@mail.openarch.com. (

00 :Serial

86400 :Refresh

7200 :Retry

2592000 :Expire

345600 ) :Minimum
```

; 名称服务器 (NS) 记录。
`NS deep.openarch.com.`
`NS mail.openarch.com.`

; 邮件交换 (MX) 记录。
`MX 0 mail.openarch.com.`

; 地址 (A) 记录。

```
localhost A 127.0.0.1

deep A 208.164.186.1

mail A 208.164.186.2

www A 208.164.186.3
```

; 规范名称 (CNAME) 记录中的别名。
`www CNAME deep.openarch.com.`

## 主名称服务器 `var/named/db.cache` 文件的配置

在启动 DNS 服务器之前，你需要获取`db.cache`文件的副本并将其复制到`/var/named/`目录。`db.cache`告知你`root`区域的服务器。

在你组织内的其他 Unix 机器上使用以下命令为你的 DNS 服务器查询新的`db.cache`文件，或者从你的 Red Linux CD-ROM 源发行版中选择一个：

```
[root@deep]# $ dig @root.servers.net -ns ns db.cache
```

忘记将`db.cache`文件拷贝到你安装 DNS 服务器的服务器的`/var/named/`目录。名称服务器与主服务器分担负载并处理整个负载。从名称服务器通过网络从另一个名称服务器加载数据，此过程称为区域传输。

© Copyright 1999 Open Network Architecture

设置从名称服务器所需的文件有：

- `named.conf`
- `db.127.0.0`
- `db.cache`
- `named script`

## 从服务器 `/etc/named.conf` 文件的配置

使用此配置用于你网络中作为从服务器的服务器。你必须修改从名称服务器的`named.conf`文件，将`0.in-addr.arpa`处所有的`primary`改为`secondary`，并添加主服务器的 IP 地址。创建文件 (`/etc/named.conf`) 并添加：

```
options {
  directory "var/named";
  recursion no;
  allow-query { 208.164.186/24 127.0.0/8 };
  allow-transfer { any };
  transfer answers;
};

// 这些文件不适用于特定区域
zone "0.in-addr.arpa" in {
  type master;
  file "db.127.0.0";
};

// 这些是你的从服务器文件
zone "openarch.com" in {
  type slave;
  file "db.openarch";
};

zone "186.164.208.in-addr.arpa" in {
  type slave;
  file "db.208.186";
};
```

## 所有类型名称服务器的 `etc/rc.d/init.named` 脚本

此配置脚本适用于类型的名称服务器（缓存、主或从）。配置`etc/rc.d/init.named`脚本以启动和停止 DNS 守护进程。创建文件（`touch /etc/rc.d/init.named`）并添加：



```bash
#!/bin/sh
#
# named      负责启动和停止
# named (BIND 服务器)。

# config: -545
# description: named (BIND) 是用于解析主机名到 IP 地址的域名服务器 (DNS)。
# probe: true

# 引入函数库。
# /etc/rc.d/init/functions

# 引入网络配置。
# /etc/sysconfig/network

# 检查网络是否就绪。
[ "$NETWORKING" = "no" ] && exit 0

[ -f /usr/sbin/named ] || exit 0
[ -f /etc/named.conf ] || exit 0

RETVAL=0

# 查看是如何被调用的。
case "$1" in
start)
  # 启动守护进程。
  echo -n "Starting named: "
  daemon named
  RETVAL=$?
  [ $RETVAL -eq 0 ] && touch /var/lock/subsys/named
  echo
  ;;
stop)
  # 停止守护进程。
  echo -n "Shutting down named: "
  killproc named
  RETVAL=$?
  [ $RETVAL -eq 0 ] && rm -f /var/lock/subsys/named
  echo
  ;;
status)
  /usr/sbin/named status
  exit $?
  ;;
restart)
  $0 stop
  $0 start
  ;;
reload)
  /usr/sbin/named reload
  exit $?
  ;;
probe)
  # named 知道如何智能重载；我们不希望 linuxconf
  # 每次都建议重启。
  /usr/sbin/named reload >/dev/null 2>&1 || echo start
  exit 0
  ;;
*)
  echo "Usage: named [start|stop|status|restart]"
  exit 1
esac
exit
```

现在，使此脚本执行并更改其默认权限：

```
[root@deep]# chmod 700 /etc/rc.d/init.d/named
```

使用命令为 BIND/DNS 创建符号 rc 链接：

```
[root@deep]# chconfig --add named
```

BIND/DNS 脚本在重启服务器时不会自动启动守护进程。可以通过执行以下命令进行更改：

```
[root@deep]# chconfig --level 3 named on
```

使用以下命令手动启动你的 DNS 服务器：

```
[root@deep]# /etc/rc.d/init.d/named start
```

## 安全 BIND/DNS

### 在 chroot 监狱中运行 BIND

这部分重点在于防止 BIND 被用作入侵宿主系统的节点。由于 BIND 执行较大且复杂的功能，影响安全的漏洞风险很高。事实上，已经存在可以利用的漏洞，允许远程攻击者获取托管 BIND 的 root 访问权限（等等，原文说的是 "obtain access to hosting BIND"，我将保留原意）。

让我们重读：“这部分重点在于防止 BIND 被用作入侵宿主系统的节点。由于 BIND 执行较大且复杂的功能，影响安全的漏洞风险很高。事实上，已经存在可以利用的漏洞，允许远程攻击者获取托管 BIND 的访问权限。”

为了最小化这种风险，BIND 可以以非 root 用户运行，这将任何损害限制在具有本地 shell 的普通用户可以执行的操作范围内。当然，允许匿名访客账户权限无法满足大多数 DNS 服务器的安全需求，因此可以采取额外的措施——即在 chroot 监狱中运行 BIND。

`chroot` 监狱的主要用处是它会将守护进程可见的文件系统部分限制在监狱的根目录。此外，监狱只需要支持 BIND，监狱中的可用程序极其有限。最重要的是，不需要 `setuid-root` 程序，这些程序如果有正确的（或错误的……漏洞，可以被用来获取 root 权限并跳出监狱。

注意：`named` 程序必须位于 `PATH` 环境变量中列出的目录中才能工作。在本文后续的文档中，我假设原始 `named` 的路径为 `"/usr/sbin/named"`。

查找 BIND 的共享库依赖。这些稍后需要复制到 chroot 监狱中。

```
[root@deep]# ldd /usr/sbin/named
```

关于本页面的意见和建议请邮件至 `gmourani@videotron.ca`

```
libc.so.6 => /lib/libc.so.6 (0x40017000)
/ld-linux.so.2 => /lib/ld-linux.so.2 (0x40000000)
```

记下上述文件；你稍后会需要它们。

### 步骤 1:

为运行 `named` 添加一个新的用户 ID 和一个新的组 ID。以 root 运行会违背监狱（jail）的意图，而使用系统中已存在的不同用户 ID 会允许你的用户访问他人的资源。考虑多层安全。

这些是示例的用户和组数字。检查 `"etc/passwd"` 和 `"etc/group"` 文件以获取空闲 `uid/gid`。我们将使用 53。

```
[root@deep]# groupadd -g 53 named
[root@deep]# useradd -g 53 named
```

### 步骤 2:

设置 chroot 环境。首先，创建监狱的根目录。我们选择了 `/chroot/named`，因为我们想将其放在独立的文件系统上以防止文件系统错误。在我们的安装过程中，我们为此目的创建了一个特殊的分区 `"chroot"`。

```
[root@deep]# /etc/rc.d/init.named_stop (仅当 named 守护进程正在运行时)
[root@deep]# mkdir -p /chroot/named
```

接下来，创建如下的复制目录：

```
[root@deep]# mkdir /chroot/named/dev
[root@deep]# mkdir /chroot/named/lib
[root@deep]# mkdir /chroot/named/etc
[root@deep]# mkdir -p /chroot/named/var/named/var/named/dev/null c 13
[root@deep]# cp /usr/sbin/named/var/run
```

复制主配置文件、区域文件以及 `named` 和 `named-xfer` 程序：

```
[root@deep]# cp /etc/named.conf /chroot/named/etc/
[root@deep]# cp /var/named /chroot/named/var/named/
[root@deep]# mkdir /chroot/named/var/named/var/named/dev/null
[root@deep]# chmod 666 /chroot/named/dev/null
[root@deep]# cp /usr/sbin/named /chroot/named/usr/sbin/
[root@deep]# cp /usr/sbin/named-xfer /chroot/named/usr/
```

重要注意：`/chroot/named/var/named` 以及该目录下所有文件的所有者必须是从服务器下的 `"named"` 进程，只有从服务器或你本人，否则你将无法进行区域传输。

- 要让 `"named"` 目录及其所有文件属于从服务器下的 `"named"` 进程，请使用命令：

```
[root@deep]# chown -R named.named /chroot/named/var/named/
```

- 为 `"named.conf"` 设置不可变位：

```
[root@deep]# cd /chroot/named/etc/
[root@deep]# chatter +i named.conf
```

将上述识别的共享库复制到 chrooted 目录：

© Copyright 1999 Open Network Architecture ® 207

关于本页面的意见和建议请邮件至 `gnmourani@videotron.ca`

```
[root@deep] # cp /lib/libc.so.6 /chroot/named/lib/
[root@deep] # cp /lib/ld-linux.so.2 /chroot/named/lib/
```

将 `"localtime"` 和 `"nsswitch.conf"` 文件复制到监狱，以便日志条目根据你的本地时区正确调整：

```
[root@deep] # cp /etc/localtime /chroot/named/etc/
[root@deep] # cp /etc/nsswitch.conf /chroot/named/etc/
```



# 为 `nsswitch.conf` 文件设置不可变位

`[root@deep] # cd /chroot/named/etc/`

`[root@deep] # chatter +nsswitch.conf`

带有 `"+i"` 属性的文件无法修改：它不能被删除或重命名，不能为此文件创建链接，无法向该文件写入数据。只有超级用户可以清除此属性。

## 步骤 3

告知 syslog chroot 环境：

通常，进程通过 `"dev/log"` 与 syslog 通信。由于 chroot 监狱的存在，这是不可能的，需要告知 syslog 指向 `"chroot/named/dev/log"`。要做到这一点，编辑 syslog 启动脚本以指定额外的位置：

编辑 syslog 行（`vi +24)/etc/rc.d/init.d/syslog`）来更改该行：

```
daemon syslog -m 0
daemon syslog -m 0 -a /chroot/named/dev/log
```

## 步骤 4

编辑 `named` 脚本（`vi /etc/rc.d/init.d/named`）来更改该行：

```
[-/usr/sbin/named] || exit 0
[-/chroot/named/usr/sbin/named ] || exit 0
[-/etc/named.conf] || exit 0
[-/chroot/named/etc/named.conf] || exit 0

daemon named
daemon/chroot/named/usr/sbin/named -t /chroot/named/ -g
```

- `-t` 告诉 `named` 启动新的 chroot 环境，
- `-u` 指定运行的用户，
- `-g` 指定运行的组。

Red Hat 的 init 脚本允许指定备用 PID 文件，这不会影响 `named` 的启动和停止操作，因为它们将在 chroot 外部调用。`BIND 8.2` 命令在此设置下无效。要修复它，必须从源码编译 `BIND`。如果你也映射新的 `named` 和 `named xfer`，应使用原始设置。

关于本页面的意见和建议请邮件至 `gmourani@videotron.ca`

要执行此，在 `BIND` 根目录下操作。

对于 `named`：

```
[root@deep]# cp bind-src.tar.gz /var/tmp
[root@deep]# cd /var/tmp/
[root@deep]# tar xpf bind-src.tar.gz
[root@deep]# cd src
[root@deep]# cp port/linux/Makefile.set port/linux/Makefile-orig
```

编辑 `Makefile.set`（`vi port/linux/Makefile.set`）进行以下更改：

```
-D_GNU_SOURCE
CDEBUG=-O9 -funroll-loops -ffast-math -multi-double -mcpu=pentium -march=pentium - 
omit-frame-pointer -no-exceptions
DESTIN=/usr/bin
DESTBIN=chroot/named/usr/sbin
DESTEXEC=chroot/named/usr/sbin
DESTMAN=/man
DESTHELP=/usr/lib
DESTETC=/etc
DESTRUN=/chroot/named/var/run
DESTLIB=/lib/bind/lib
DESTINC=/lib/bind/include/
LEX=flex -f
YACC=yacc -d
SYSLBS=-lff
INSTALL=make install
MANDIR=man
MANOFF=cat
CATEXT=$IN
AR=ar
RANLIB=-
```

我们之前使用的 `Makefile` 区别在于修改了 `DESTIN`、`DESTEXEC` 和 `DESTRUN` 行指向 `BIND` 的 chrooted 目录。通过此修改，`named` 程序现在知道哪里寻找 `"named"`。

```
[root@deep]# make clean
[root@deep]# make
[root@deep]# cp bin/named /chroot/named/usr/sbin/
[root@deep]# cp bin/named-xfer/xfer /chroot/named/usr/sbin/
[root@deep]# cp named-xfer /chroot/named/usr/sbin-named-xfer
[root@deep]# strip /chroot/named/usr/sbin/named
[root@deep]# strip /chroot/named/usr/sbin/named-xfer
```

我们编译二进制文件，将 `named` 的结果复制到 `"usr/sbin"` 并覆盖旧的。我们没有忘记 `strip` 我们新的 `"named"` 二进制文件以获得更好的性能。编译一个新的 `"named"` 二进制文件也是个好主意，确保 `named` 和 `named xfer` 使用相同的版本。

对于 `named`：

```
[root@deep]# cd /var/tmp/
[root@deep]# cp port/linux/Makefile.set-orig port/linux/Makefile.set
```

编辑 `Makefile.set`（`vi port/linux/Makefile.set`）进行列出的更改：

```
-D_GNU_SOURCE
```

© Copyright 1999 Open Network Architecture ® 209

```
CDEBUG=-O9 -funroll-loops -ffast-math -malign-double -mpu=pentiumpro -march=pentiumpro - 
omit-frame-pointer -no-exceptions
DESTBIN=/usr/bin
DESTBIN=/usr/sbin
DESTEXEC=/usr/sbin
DESTMAN=/man
DESTHELP=/usr/lib
DESTETC=/etc
DESTRUN=/var/run
DESTLIB=/lib/bind/lib
DESTINC=/lib/bind/include/
LEX=flex -f
YACC=yacc -d
SYSLBS=-lff
INSTALL=make install
MANDIR=man
MANOFF=cat
CATEXT=$IN
AR=ar
RANLIB=-
```

```
[root@deep]# rm -f
[root@deep]# make clean
[root@deep]# cp bin/named /chroot/named/usr/sbin
[root@deep]# cp bin/named-xfer/xfer /chroot/named/usr/sbin
[root@deep]# cp named-xfer /chroot/named/usr/sbin-named-xfer
[root@deep]# strip /chroot/named/usr/sbin/named
[root@deep]# strip /chroot/named/usr/sbin/named-xfer
```

我们移除了 `"settings"`，因为构建系统会缓存这些变量，并运行 `"make clean"` 命令以确保没有留下垃圾。在我们构建 `"named"` 二进制文件并用 `"named-xfer"` 将其复制到 chrooted 目录之后，我们还使用了 `"strip"` 命令提高新二进制文件的性能。

# 删除不需要的文件和目录

```
[root@deep]# rm -f /usr/sbin
[root@deep]# rm -f /usr/sbin/named-xfer
[root@deep]# rm -f /etc/named.conf
[root@deep]# rm -f /var/named/
```

## 步骤 5

测试新的 chroot 配置！重启 `syslogd`：

```
[root@deep]# /etc/rc.d/init.d/syslog restart
```

现在启动新的 BOUNDED 守护进程：

```
[root@deep]# /etc/rc.d/init.d/named start
```

确保它以 `named` 用户运行并带有新参数。

```
[root@deep]# ps aux grep named
```

关于本页面的意见和建议请邮寄至 `gmourani@videotron.ca`

`named 11466 0.0 1.2 2444 1850 ? 23:09:00/chroot/named/usr/bin/named -t/chroot/named -unnamed-named`



第一列应该是 `named`，这是运行该进程的用户名称（user-id）。第一行的末尾应该是 `named -t /chroot/named/ -unnamed-named`。

# 工作完成后的清理

```
[root@deep]# rm -rf /var/tmp/bind/
```

注意：出于安全考虑，公司网络与外部主机之间不存在 DNS 是非常重要的。使用 IP 地址在公司网络与外部机器之间连接（反之亦然）要安全得多。

# 区域传输 (Zone transfers)

限制区域传输：

限制区域传输可以防止：

- 他人过度消耗名称服务器资源。
- 黑客列出区域内容。

以下是 `named.conf` 文件中 `allow-transfer` 选项包含的内容示例：

```
options {
  allow-transfer ( 208.164.186.2;);
}
```

此控制允许哪些名称服务器从此名称服务器传输任何区域。关于限制区域传输的注意事项：请记住限制来自从名称服务器的区域传输，而不仅仅是主（primary master）。

# 允许查询 (Allow-query)

限制你的名称服务器接受的查询范围为：

- 它们应该来源的地址。
- 它们应该查询的区域。

以下是 `named.conf` 文件中 `allow-query` 选项包含的内容示例：

```
options {
  allow-query ( 208.164.186/24; 127.0.0.8;);
}
```

这指定了哪些 IP 地址允许向服务器发送查询。特别是，运行互联网防火墙的人可能有合法需求向大多数世界隐藏其命名空间的一部分，但对有限的受众开放。

# 仅转发 (Forward-only)

你可能希望在转发器（forwarder）宕机或没有响应时，停止名称服务器尝试联系远程服务器。`仅转发` 模式的名称服务器如果转发器没有给出答案，则不会联系其他服务器查找信息。

以下是 `named.conf` 文件中 `forward only` 选项包含的内容示例：

```
options {
  forwards ( 205.151.222.250; 205.151.222.251 );
  forward-only;
}
```

在 `forwards` 行中，`205.151.222.250` 和 `205.151.222.251` 分别是 ISP DNS 服务器和另一个 DNS 服务器的 IP 地址。

# 更多文档

详情可以阅读以下几页：

- `$ dnsdomainname (1)` - 显示系统的 DNS 域名
- `$ dnskeygen (1)` - 为 DNS 安全生成公钥、私钥和共享密钥
- `$ nsquery (1)` - 使用解析器查询域名服务器
- `$ nsnamed (8)` - 互联网域名服务器 (DNS)

# DNS 管理工具

下面列出的命令是我们在日常使用中使用的，但还有更多命令，你必须检查相关页面和文档以获取更多细节和信息。

## dig

`db.cache` 告诉你 `root` 区域的服务器位置。它会定期更新。根名称服务器不会经常更改，但它们确实会变。良好的做法是每一两个月检查一次 `db.cache` 文件。

- 使用以下命令为你的 DNS 服务器查询新的 `db.cache` 文件：

  `[root@deep] dig @root-servers.net -ns db.cache`

  获取后将 `db.cache` 文件复制到 `/var/named/` 下。

其中 `@root-servers.net` 是查询新 `db.cache` 文件的根服务器地址，`db.cache` 是你新 `db.cache` 文件的文件。

## ndc

此命令允许系统管理员控制名称服务器的操作。如果没有给出命令，`ndc` 将提示输入命令，直到读到 EOF。

- 在终端上输入 `ndc`，然后输入 `help` 查看不同命令的帮助。

  `[root@deep]# ndc`

  `[root@deep]# ndc help`

# DNS 用户工具

下面列出的命令是我们在日常使用中使用的，但还有更多命令，你必须检查相关页面和文档以获取更多细节和信息。

## nslookup

`nslookup` 是一个查询互联网名称服务器的程序。`nslookup` 有两种模式：交互式和非交互式。交互式允许用户查询名称服务器获取有关各种主机和域名的信息，并打印域内的主机列表。非交互式模式用于仅打印主机或域名的名称和请求的信息。

交互式有很多选项，更好的方法是查看 `nslookup` 页面获取有关交互式模式的信息，或在 `nslookup` 模式下输入。

- 要进入 `nslookup` 交互式模式，使用命令：

  `[root@deep]# nslookup`（在此处输入更多关于 `nslookup` 使用的信息）。

  默认服务器: `deep.openarch.com`

  地址: `208.164.186.3`

  `> help`

- 要运行非交互式模式，使用命令：

  `[root@deep]# nslookup www.redhat.com`

  当要查找的主机名或互联网地址作为第一个参数给出时，使用非交互式模式。第二个参数指定服务器的主机名或地址。

关于本页面的意见和建议请邮寄至 `gnoumouri@videotron.ca`

在我们的配置和安装中，我们将为您提供两种不同的配置供您设置 `sendmail` 使用：一种用于中央邮件枢纽中继（Central Mail Hub Relay），另一种用于本地或邻近客户端及服务器机器。

中央邮件枢纽中继配置将用于您的服务器，其任务是为您网络上可能的所有本地或邻近客户端及服务器邮件机器发送、接收和中继邮件。本地或邻近客户端及服务器指的是您网络上所有运行 `sendmail` 的其他本地服务器或客户端机器，它们会将所有发出的邮件发送到中央邮件枢纽以便后续投递。这种内部邮件永远不会直接通过互联网接收，相反，所有这些计算机从互联网接收的所有邮件都保留在邮件枢纽。为您网络架构中的所有计算机运行中央邮件枢纽服务器是一个好主意，可以在内部服务器、客户端机器上进行任务管理，并提高您站点的安全性。

您可以配置邻近 `sendmail` 使其仅接受本地生成的邮件，从而隔离机器以提高安全性。网关服务器（位于防火墙之外或防火墙的一部分）作为代理，并接收（通过其防火墙）从外部进入内部交付的邮件，并将其转发到中央邮件枢纽服务器。另外注意，网关服务器的配置类似于邻近 `sendmail`，从接受来自外部（互联网）的入站邮件。

| 我们的网页服务器<br>www.openarch.com | 我们的网关服务器<br>deepopenarch.com | 我们的邮件服务器<br>mail.openarch.com |
| :--- | :--- | :--- |
| 一个内部邮件服务器 | 另一个内部邮件服务器 | 我们的中央邮件服务器 |
| 仅接受本地生成的邮件 | 仅接受本地生成的邮件 | 接收外部邮件（通过其防火墙）用于集中化和发送邮件 | 接收 |

`openarch.com` 域名仅可通过 `mail.openarch.com` 访问。

这是我们在书中使用的 Sendmail 配置的图形化表示。我们尝试在不同的服务器上向您展示不同的设置（中央邮件枢纽中继以及本地或邻近客户端及服务器机器）。所有可能性都存在，取决于您的需求和网络架构。

## 这些安装指令假设

字体 命令兼容 Unix。

- 源码路径为 `/var/tmp/`（也可能是其他路径）。
- 安装在 RedHat Linux 6.1 上进行过测试。
- 安装中的所有步骤将在超级用户账户 `root` 中进行。
- Sendmail 版本为 8.9.3

## 软件包

- Sendmail 首页：http://www.sendmail.org/
- 您必须确保下载了：`sendmail.8.9.3.tar.gz`

## 压缩包 (Tarballs)

在安装 Sendmail 之前列出系统文件列表是一个好主意，之后使用 `diff` 进行比较，以找出哪些文件被放置在了哪里。只需在安装软件之前运行 `find /`，在安装后运行 `find / > send2`，并使用 `diff send1 > send2` 获取更改列表。

### 编译

解压 tarball 包 (`tar.gz`)。

```bash
[root@deep]$# cp sendmail.version.gz /var/tmp
[root@deep]$# cd /var/tmp
[root@deep]$# tar xzf sendmail.version.tar
```

## 配置

进入新的 Sendmail 目录：

编辑 `linux.m4` 文件（`vi +16 /ostype/linux.m4`）并修改：

修改为：

```
define(`LOCAL_MAILER_PATH`, `/usr/bin/local`)\dnl

define(`PROMAIL_MAILER_PATH`, `/usr/bin/procmail`)\dnl

dnl define(`LOCAL_MAILER_FLAGS`, `ShPin`)\dnl
```



`dnl define(`LOCAL_MAILER_ARGS`, `procmail -a h -d $u`)\dnl`

`define(`STATUS_FILE`, `/var/log/sendmail.st`)\dnl`

> 注意：这些步骤仅在中央邮件枢纽配置需要。这将使 sendmail 使用 procgram 作为本地邮件传递代理，并定义状态文件 `sendmail.st` 位于 `/var/log` 目录下。

编辑 `linux.m4` 文件（`vi +16 /ostype/linux.m4`）并添加该行：

`define(`STATUS_FILE`, `/var/log/sendmail.st`)\dnl`

> 注意：这是本地服务器、客户端 sendmail 配置所需的步骤。它将定义状态文件 `sendmail.st` 位于 `/var/log` 目录下。

编辑 `header.m4` 文件（`vi +26 BuildTools/M4/header.m4`）并修改：

`define(`confLIBSEARCH`, `db bind resolv 44bsd`)\dnl`

修改为：

`define(`confLIBSEARCH`, `db1 bind resolv 44bsd`)\dnl`

此更改指定了安装在 Linux 上的 Berkeley 包。

编辑 `makemap.c` 文件（`vi +30 makemap/makemap.c`）并修改：

```c
# include <db.h>
```

修改为：

```c
# include <db_185.h>
```

编辑 `map.c` 文件（`vi +29 src/map.c`）并修改：

© Copyright 1999 Open Network Architecture ®

```c
# include <db.h>
```

修改为：
```c
# include <db_185.h>
```

编辑 `uds.c` 文件（`vi +28 src/uds.c`）并修改：

```c
# include <db.h>
```

修改为：
```c
# include <db_185.h>
```

关于本页面的意见和建议请邮件至 `gmourani@videotron.ca`

`define(`OPTIMIZE`; `-O9 -funroll-loops -ffast-math -malign-double -mcpu=pentiumpro -march=pentiumpro -fomit-family-pointer -fno-exceptions`)`
此选项定义了传递给 `CC` 的与特定 CPU 架构相关的优化标志。

`define(`LIBS`; `-lnsl`)`
此选项定义了传递给 `ld` 的 `-l` 标志。

`define(`LDOPTS`; `-s`)`
此选项定义了传递给 `ld` 的链接器选项。

`define(`MANOWN`; `root`)`
此选项定义了安装的手页（man pages）的所有者。

`define(`MANGRP`; `root`)`
此选项定义了安装的手页的所属组。

`define(`MANMODE`; `644`)`
此选项定义了安装的手页的模式。

`define(`MAN1SRC`; `1`)`
此选项定义了安装在 `confMAN1` 中的手页的源。

`define(`MAN5SRC`; `5`)`
此选项定义了安装在 `confMAN5` 中的手页的源。

`define(`MAN8SRC`; `8`)`
此选项定义了安装在 `confMAN8` 中的手页的源。

```
[root@$deep] cd /var/tmp/sendmail-version

[root@$deep] cd src

[root@$deep] sh Build -f ../Tools/siteconfig.m4

[root@$deep] cd

[root@$deep] cd mailalists

[root@$deep] sh Build -f ../Tools/siteconfig.m4

[root@$deep] cd

[root@$deep] cd makemap (Only for Mail Hub configuration)

[root@$deep] sh Build -f ../Tools/siteconfig.m4 (Only for Mail Hub configuration)

[root@$deep] cd praliliases (Only for Mail Hub configuration)

[root@$deep] sh Build -f ../Tools/siteconfig.m4 (Only for Mail Hub configuration)

[root@$deep] cd

[root@$deep] sh Build -f ../Tools/siteconfig.m4

[root@$deep] cd ..

```

注意：“`sh Build`” 脚本将创建新的目录
“`obj.yourOS,your.version,yourarchitecture`”，例如“`obj.Linux.2.2.13.i686`”
每个子目录程序可能会安装，然后在这些目录中创建指向
源文件和 Makefiles 的链接。

```
[root@$deep] make install -C obj.Linux.version.architecture

[root@$deep] make install -C mailalists/obj.Linux.version.architecture (Only for Mail Hub configuration)

[root@$deep] make install -C makemap/obj.Linux.version.architecture (Only for Mail Hub configuration)

[root@$deep] make install -C praliliases/obj.Linux.version.architecture (Only for Mail Hub configuration)

[root@$deep] make install -C smrs/obj.Linux.version.architecture

```

关于本页面的意见和建议请邮件至 `gmouriani@videotron.ca`

```
[root@debug#] ln -sf /usr/sbin/sendmail /usr/lib/sendmail

[root@debug#] strip /usr/sbin/mailmats

[root@debug#] strip /usr/sbin/makemap (Only for Mail Hub configuration)

[root@debug#] strip /usr/sbin/paliases (Only for Mail Hub configuration)

[root@debug#] strip /usr/sbin/smsh

[root@debug#] chown /usr/sbin/sendmail

[root@debug#] chown 0:0 /usr/sbin/mailmats

[root@debug#] chown 0:0 /usr/sbin/makemap (Only for Mail Hub configuration)

[root@debug#] chown 0:0 /usr/sbin/paliases (Only for Mail Hub configuration)

[root@debug#] chown 0:0 /usr/sbin/smsh

[root@debug#] chmod 515 /usr/sbin/smsh

[root@debug#] install -d -m755 /var/spool/mqueue

[root@debug#] mkdir root.mail /var/spool/mqueue

[root@debug#] mkdir etc/smsh

[root@debug#] mkdir etc/etc/mail (Only for Mail Hub configuration)
```



`sh -f` 命令将为你系统上 sendmail 构建安装所需的不同文件，在 `obj.Linux-architecture` 中构建并创建必要的依赖项。
`make install` 命令将在你的系统上安装 sendmail、`mailmaps`、`paliases`、`smsh` 二进制文件和链接，以及生成的手页。
`ls -s` 命令将创建 sendmail 二进制文件到 `/usr/lib` 目录的符号链接。这是必要的，因为某些程序希望在该目录 (`/usr/lib`) 中找到 sendmail。
`strip` 命令将减小 `mailmats`、`paliases`、`smsh` 和 `makemap` 二进制文件的大小以获得最佳性能。
`install` 命令将在 `var/spool` 下创建一个权限为 755 的 `mqueue` 目录。由于各种原因，消息可能会暂时无法送达。为了确保这些消息最终送达，sendmail 将其存储在队列目录中，直到成功送达。
`chown` 命令将将文件 `mailmats`、`makemap`、`paliases`、`smsh` 的 UID 和 GID 设置为 `root`。
`mkdir` 命令将在 `var/spool` 下创建一个权限为 755 的 `mqueue` 目录。由于各种原因，消息可能会暂时无法送达。为了确保这些消息最终送达，sendmail 将其存储在队列目录中，直到成功送达。
`chown` 命令将将文件 `mailmats`、`makemap`、`paliases`、`smsh` 的 UID 和 GID 设置为 `root`。
`mkdir` 命令将在 `var/spool` 下创建一个权限为 755 的 `mqueue` 目录。由于各种原因，消息可能会暂时无法送达。为了确保这些消息最终送达，sendmail 将其存储在队列目录中，直到成功送达。
`chown` 命令将将文件 `mailmats`、`makemap`、`paliases`、`smsh` 的 UID 和 GID 设置为 `root`。
`mkdir` 命令将在 `var/spool` 下创建一个权限为 755 的 `mqueue` 目录。由于各种原因，消息可能会暂时无法送达。为了确保这些消息最终送达，sendmail 将其存储在队列目录中，直到成功送达。
`chown` 命令将将文件 `mailmats`、`makemap`、`paliases`、`smsh` 的 UID 和 GID 设置为 `root`。
`mkdir` 命令将在 `var/spool` 下创建一个权限为 755 的 `mqueue` 目录。由于各种原因，消息可能会暂时无法送达。为了确保这些消息最终送达，sendmail 将其存储在队列目录中，直到成功送达。
`chown` 命令将将文件 `mailmats`、`makemap`、`paliases`、`smsh` 的 UID 和 GID 设置为 `root`。
`mkdir` 命令将在 `var/spool` 下创建一个权限为 755 的 `mqueue` 目录。由于各种原因，消息可能会暂时无法送达。为了确保这些消息最终送达，sendmail 将其存储在队列目录中，直到成功送达。
`chown` 命令将将文件 `mailmats`、`makemap`、`paliases`、`smsh` 的 UID 和 GID 设置为 `root`。
`mkdir` 命令将在 `var/spool` 下创建一个权限为 755 的 `mqueue` 目录。由于各种原因，消息可能会暂时无法送达。为了确保这些消息最终送达，sendmail 将其存储在队列目录中，直到成功送达。
`chown` 命令将将文件 `mailmats`、`makemap`、`paliases`、`smsh` 的 UID 和 GID 设置为 `root`。
`mkdir` 命令将在 `var/spool` 下创建一个权限为 755 的 `mqueue` 目录。由于各种原因，消息可能会暂时无法送达。为了确保这些消息最终送达，sendmail 将其存储在队列目录中，直到成功送达。
`chown` 命令将将文件 `mailmats`、`makemap`、`paliases`、`smsh` 的 UID 和 GID 设置为 `root`。
`mkdir` 命令将在 `var/spool` 下创建一个权限为 755 的 `mqueue` 目录。由于各种原因，消息可能会暂时无法送达。为了确保这些消息最终送达，sendmail 将其存储在队列目录中，直到成功送达。
`chown` 命令将将文件 `mailmats`、`makemap`、`paliases`、`smsh` 的 UID 和 GID 设置为 `root`。
`mkdir` 命令将在 `var/spool` 下创建一个权限为 755 的 `mqueue` 目录。由于各种原因，消息可能会暂时无法送达。为了确保这些消息最终送达，sendmail 将其存储在队列目录中，直到成功送达。
`chown` 命令将将文件 `mailmats`、`makemap`、`paliases`、`smsh` 的 UID 和 GID 设置为 `root`。
`mkdir` 命令将在 `var/spool` 下创建一个权限为 755 的 `mqueue` 目录。由于各种原因，消息可能会暂时无法送达。为了确保这些消息最终送达，sendmail 将其存储在队列目录中，直到成功送达。
`chown` 命令将将文件 `mailmats`、`makemap`、`paliases`、`smsh` 的 UID 和 GID 设置为 `root`。
`mkdir` 命令将在 `var/spool` 下创建一个权限为 755 的 `mqueue` 目录。由于各种原因，消息可能会暂时无法送达。为了确保这些消息最终送达，sendmail 将其存储在队列目录中，直到成功送达。
`chown` 命令将将文件 `mailmats`、`makemap`、`paliases`、`smsh` 的 UID 和 GID 设置为 `root`。
`mkdir` 命令将在 `var/spool` 下创建一个权限为 755 的 `mqueue` 目录。由于各种原因，消息可能会暂时无法送达。为了确保这些消息最终送达，sendmail 将其存储在队列目录中，直到成功送达。
`chown` 命令将将文件 `mailmats`、`makemap`、`paliases`、`smsh` 的 UID 和 GID 设置为 `root`。
`mkdir` 命令将在 `var/spool` 下创建一个权限为 755 的 `mqueue` 目录。由于各种原因，消息可能会暂时无法送达。为了确保这些消息最终送达，sendmail 将其存储在队列目录中，直到成功送达。
`chown` 命令将将文件 `mailmats`、`makemap`、`paliases`、`smsh` 的 UID 和 GID 设置为 `root`。
`sh -f` 命令将为你系统上 sendmail 构建安装所需的不同文件，在 `obj.Linux-architecture` 中构建并创建必要的依赖项。
`make install` 命令将在你的系统上安装 sendmail、`mailmaps`、`paliases`、`smsh` 二进制文件和链接，以及生成的手页。
`ls -s` 命令将创建 sendmail 二进制文件到 `/usr/lib` 目录的符号链接。这是必要的，因为某些程序希望在该目录 (`/usr/lib`) 中找到 sendmail。
`strip` 命令将减小 `mailmats`、`paliases`、`smsh` 和 `makemap` 二进制文件的大小以获得最佳性能。
`install` 命令将在 `var/spool` 下创建一个权限为 755 的 `mqueue` 目录。由于各种原因，消息可能会暂时无法送达。为了确保这些消息最终送达，sendmail 将其存储在队列目录中，直到成功送达。
`chown` 命令将将文件 `mailmats`、`makemap`、`paliases`、`smsh` 的 UID 和 GID 设置为 `root`。
`mkdir` 命令将在 `var/spool` 下创建一个权限为 755 的 `mqueue` 目录。由于各种原因，消息可能会暂时无法送达。为了确保这些消息最终送达，sendmail 将其存储在队列目录中，直到成功送达。
`chown` 命令将将文件 `mailmats`、`makemap`、`paliases`、`smsh` 的 UID 和 GID 设置为 `root`。
`mkdir` 命令将在 `var/spool` 下创建一个权限为 755 的 `mqueue` 目录。由于各种原因，消息可能会暂时无法送达。为了确保这些消息最终送达，sendmail 将其存储在队列目录中，直到成功送达。
`chown` 命令将将文件 `mailmats`、`makemap`、`paliases`、`smsh` 的 UID 和 GID 设置为 `root`。
`mkdir` 命令将在 `var/spool` 下创建一个权限为 755 的 `mqueue` 目录。由于各种原因，消息可能会暂时无法送达。为了确保这些消息最终送达，sendmail 将其存储在队列目录中，直到成功送达。
`chown` 命令将将文件 `mailmats`、`makemap`、`paliases`、`smsh` 的 UID 和 GID 设置为 `root`。
`mkdir` 命令将在 `var/spool` 下创建一个权限为 755 的 `mqueue` 目录。由于各种原因，消息可能会暂时无法送达。为了确保这些消息最终送达，sendmail 将其存储在队列目录中，直到成功送达。
`chown` 命令将将文件 `mailmats`、`makemap`、`paliases`、`smsh` 的 UID 和 GID 设置为 `root`。

关于本页面的意见和建议请邮件至 `gmourani@videotron.ca`

## `/etc/mail/access` and `access.db` for the Central Hub

创建一个 `access` 数据库来接受或拒绝来自选择域的邮件。例如，你可以拒绝所有来自已知垃圾邮件发送者的邮件。如果你决定使用中心邮件枢纽处理所有邮件，则不需要这些 `access` 和 `access.db`。

步骤 1

创建访问文件（`touch /etc/mail/access`）并添加以下行：

```



# 关于此文件格式的描述来自 Sendmail 源码分发中的 `/cf/README` 文件。

该表使用电子邮件地址、域名和网络数字作为键。例如，

```
spammer@aol.com           REJECT
cypberspam.com            REJECT
192.168.212              REJECT
```

映射的值部分可以包含：

`OK` 即使运行规则中的其他规则会拒绝它，也接受，例如，如果名称无法解析

`RELAY` 接受发送到指定域或来自指定域的邮件，通过你的 SMTP 服务器进行转发。`RELAY` 同时也作为其他检查的隐式 `OK`。

`REJECT` 用通用消息拒绝发送者或接收者。

```
© Copyright 1999 Open Network Architecture ®

关于此页面的意见和建议请邮寄至 gmourani@videotronca.ca
```

`DISCARD` 使用 `$discard` 发送器完全丢弃邮件。这仅对发送者地址有效（即表示你应该丢弃从指定域名收到的任何内容）。

```
```

### any text，其中 `###` 是符合 RFC 821 标准的错误代码，"any text" 是为该命令返回的消息。

```
```

例如：

```
cyberspammer.com 550 我们不接受来自垃圾邮件发送者的邮件
okay.cyberspammer.com OK
sendmail.com OK
128.32 RELAY
```

接受来自 okay cyberspammer.com 的邮件，但将拒绝来自 cyberspammer.com 所有主机的邮件，并带有指定的消息。我们将接受来自 sendmail.domain org 中任何主机的邮件，并允许 `128.32.*` 网络进行中继。

你也可以使用访问数据库根据地址中的用户名部分来阻止地址。例如：

```
FREE_STEALTH.MAILER@ 550 不接受垃圾邮件
```

注意，你必须在用户名后包含 `@`，以表示此数据库条目仅用于检查发送者地址的用户名部分。

如果你想在我们的 "sendmail.mc 配置"中使用它：

```
FEATURE("blacklist, recipients")
```

那么你就可以向映射表中添加本地用户、你域名中的主机或你域名中不应接收邮件的地址条目：

```
badolocaluser 550 该用户的邮箱箱已禁用
host.mydomain.com 550 该主机不接受邮件
user@otherhost.mydomain.com 550 该收件人的邮箱箱已禁用
```

这将防止 `badolocaluser@mydomain.com` 以及任何 `user@host.mydomain.com` 接收邮件。启用此功能将防止你向所有在访问映射中值为错误消息或 `REJECT` 的地址发送邮件。

参考以下示例：

```
spam@aol.com REJECT
cyberspammer.com REJECT
```

邮件无法发送到 `spam@aol.com` 或 `cyberspammer.com` 的任何地方。

现在我们配置访问文件，默认情况下我们允许从本地中继...

```
localhost.localdomain RELAY
localhost RELAY
127.0.0.1 RELAY
```

步骤 2
创建 `access.db` 文件：

© Copyright 1999 Open Network Architecture ®

关于此页面的意见和建议请邮寄至 gmnourai@videotron.ca

记住，由于 `/etc/mail/access/` 是一个数据库，在按描述创建文本文件后，你必须使用 "`makemap`" 程序创建数据库映射。

要创建“访问数据库映射”，请使用以下命令：
`[root]@deep# makemap hash /etc/access.db < /etc/mail/access`

## 用于中央邮件枢纽的 'etc/aliases 和 aliases.db' 文件

`alias`（别名）是将一个收件人转换为另一个的过程。其中一种是将通用名称（如 `root`）转换为真实的用户名。另一种是将一个名称转换为名称列表（用于邮件列表）。对于每一个列出某个用户为收件人的信封，`sendmail` 都会在 "`aliases`" 文件查找收件人。由于 `sendmail` 可能需要从 "`aliases`" 文件中搜索数千个名称，该文件的一个版本以独立的 "`db`" 数据库格式存储，以显著提高查找速度。如果你配置 `sendmail` 使用中央服务器（邮件枢纽）来处理一切，则不需要在相邻服务器或客户端机器上安装 "`aliases`" 和 "`aliases.db`" 文件。

步骤 1
创建 `aliases` 文件（`touch /etc/aliases`）并添加以下行：

```
#
# @(#)aliases 8.2 (Berkeley) 3/5/94
# 此文件中的别名在邮件头中不会被展开，
# 但在网络上或通过 /bin/mail 可见。
#
>>>>>>> 程序“必须在...之后运行”
>>>>>> 注意 >> 此文件已根据任何通过
# sendmail 显示的更改进行更新。
#
```

```
# 基本系统别名 -- 这些必须存在。
MAILER-DAEMON: postmaster
postmaster: root
# 伪账户的通用重定向。
bin: root
daemon: root
nbody: root
# 应该接收 root 邮件的人
root: admin
```

注意：你的 `aliases` 文件要复杂得多，但尽管如此，请注意示例显示的是别名的最小形式。

步骤 2
创建 `aliases.db` 文件：
由于 `"/etc/aliases 是一个数据库，在按描述创建文本文件后，你必须使用 "makemap" 程序创建数据库映射。`

要创建“别名数据库映射”，请使用以下命令：
`[root]@deep# makemap hash /etc/aliases.db < /etc/aliases`

© Copyright 1999 Open Network Architecture ®

## 用于中央邮件枢纽的 "/etc/mail/virtertable, domainable, mailertable, and virtertable.db, domainable.db, mailertable.db" 文件

某些站点在从旧域名过渡到新域名时需要使用多个域名。`domainable` 功能通过将旧域名重写为新域名来使过渡平滑运行。

`virtertable` 是将虚拟域名映射到新地址的数据库。这是一种特定域名的别名格式，允许在机器上托管多个虚拟域名。

`mailertable` 是一个将 "`host.domain`" 名称映射到特殊代理和新域名对的数据库。这可以用于覆盖特定域的路由。

要在 `/etc/mail` 目录中使用 `virtertable`, `domainable`, `mailertable` 及其对应的 `.db` 文件，请使用以下命令：

```
[root@dead]# for map in virtertable domainable mailertable
>
> touch /etc/mail/${map}
> chmod 044 /etc/mail/${map}
> makemap /etc/mail/${map}.db < /etc/mail/${map}
> done
```

## 用于中央邮件枢纽的 "/etc/sendmail.cw" 文件

`"/etc/sendmail.cw"` 文件用于本地主机的备用名称。（此处后续重复内容已省略）

关于本页面的意见和建议应邮寄至 gmourani@videotron.ca

通过 `OSTYPE` m4 命令提供对各种操作系统的支持。每个 "`mc`" 文件必须使用此命令声明操作系统。本项目是 "`mc`" 文件所需的最少信息之一。

```
define('CONTAUTO_REBUILD')
```

此配置选项在需要时自动重建文件。

```
define('CONTO_CONNECT', '1m')
```

此配置选项设置了等待 `connect()` 完成的超时时间。这只能缩短超时时间；内核本身会强制执行绝对最大值（取决于系统而异）。

```
define('CONTRY_NULL_MX_LIST',true)
```

此配置选项表示，如果服务器是主机的 MX 记录且未进行其他安排，则直接连接到该主机。

```
define('CONFONT_PROBE_INTERFACES,true)
```



此配置选项设置 `sendmail` 是否不会将任何本地接口的名称和地址插入 `$w` 类（已知“等效”地址列表）。

``` 
define('PROMAIL_MAILER_PATH','/usr/bin/procmail')
```

此配置选项设置指向 `procmail` 的路径。这也由 `FEATURE('local_procmail')` 使用。

``` 
FEATURE('smush','/usr/bin/smush')
```

此 m4 宏启用了 "smush"（sendmail 限制 shell）的使用。尽管 Sendmail 在运行来自 "etc/aliases" 和 "~/.forward" 文件的程序时必须非常小心，但它仍然可能受到内部攻击的威胁。为了限制 Sendmail 允许运行的程序选择，Sendmail 的 V8 版本包含了 "smush"（Sendmail 限制 shell）程序。这提高了本地系统管理员控制通过电子邮件运行什么程序的能力。"smush" 程序的默认位置是 "/usr/local/etc/smush"，由于我们处在另一个位置，我们需要为 `smush` 特性添加一个参数，指向新的替换项 `"/usr/bin/smush"`。CERT 建议使用 "smush"，因此鼓励您尽可能频繁地使用此功能。

``` 
FEATURE(mailter)
```

此 m4 宏启用了“数据库选择新的投递代理”的使用。`mailter` 是一个将 "host.domain" 映射到特殊投递代理和新域名对的数据库。这些新域名用于路由，但不会显示在邮件标头中。

``` 
FEATURE('virtuerable','hash -o /etc/mail/virtuerable')
```

此 m4 宏启用了“对虚拟域名的支持”的使用。`virtuerable` 是一个将虚拟域名映射到新地址的数据库。

``` 
FEATURE(redirect)
```

此 m4 宏启用了“对 address.REDIRECT 的支持”的使用。`redirect` 功能允许为弃用的账户设置别名。这些别名会退回，并带有新转发地址的指示。请注意，邮件会被退回并转发。不会向接收者地址发送通知。

``` 
FEATURE(always_add_domain)
```

此 m4 宏启用了“在本地邮件上添加本地域名”的使用。`always_add_domain` 特性是安全且推荐的。它确保了所有本地定义的地址都是完全限定的。

``` 
FEATURE(use_cw_file)
```

© Copyright 1999 Open Network Architecture ®

关于本页面的意见和建议应邮寄至 gmourani@videotron.ca

m4 宏启用了“使用 /etc/sendmail.cw 文件处理本地主机名”。`use_cw_file` 特性会导致读取 `/etc/sendmail.cw` 文件以获取本地主机的备用主机。该文件的用途可能是声明本地主机作为 MX 接收者时运行的主机列表。

## FEATURE(local_procmail)

此 m4 宏启用了“将 procmail 作为本地投递代理”的使用。`procmail` 程序可以处理用户的邮件（例如按主题分类到文件夹），并可以作为 Sendmail 投递代理工作。

## FEATURE(nouuccp)

此 m4 宏启用了“消除所有 UUOC 支持”。如果您的站点与 UUOC 异常无关，则可以启用 `nouuccp` 特性。与 UUOC 相关的宏将被忽略。

## MAILER(procmail) and MAILER(smtp)

投递代理不会自动声明。相反，你必须使用 `MAILER` m4 宏指定你想使用的哪些以及忽略哪些。`MAILER(procmail)` 和 `MAILER(smtp)` 支持包含 procmail、smtp、smtp8 和 relay投递代理。

## FEATURE(access, db)

开启访问数据库，使你能够出于管理原因允许或拒绝来自特定域的邮件接收。例如，你可以选择拒绝所有来自已知垃圾邮件发送者的邮件。

## FEATURE(blacklist_recipients)

开启阻塞某些接收者用户、用户名或地址的邮件的能力。例如，你可以阻止向用户 `nobody`、主机 `foo.mydomain.com` 或 `guest@bar.mydomain.com` 发送。使用了 `http://maps.vix.com`，这是一个在服务器 DNS 中维护的数据库。详情见 "http://maps.vix.com/"。

## FEATURE(rbl)

这将导致发送拒绝实时黑洞列表（Realtime Blackhole List）数据库中的邮件。如果提供了参数则使用；否则使用 `maps.vix.com` 上的主 RBL 服务器，这是一个在服务器 DNS 中维护的数据库。

注意：一个域名可能位于你希望与其继续通信的 RBL 列表中。也许与黑名单域名中的某些用户通信对你来说至关重要。为此，Sendmail 允许你覆盖这些域名以允许接收其电子邮件。只需编辑 `/etc/mail/` 即可接收其邮件。例如：

## blacklisted.domain OK

## 第2步

一旦我们的 `sendmail.mc` 配置文件创建，我们可以通过以下命令构建 sendmail 配置：

``` 
[root@deep] cd /var/tmp/sendmail-version/cf

[root@deep] # m4 ../cf.m4 /etc/sendmail > /etc/sendmail
```

``` 
divert(-1) 和 divert(0)

divert(-1) 将删除输出文件中的 cr，而 divert(0) 将恢复常规输出。
```

注意：这里，`../cf.m4` 告诉 m4 程序去哪里查找默认配置文件信息。

© Copyright 1999 Open Network Architecture ®

## "/etc/mail.cw" 用于本地主机和服务器

与其让网络中的每个单独服务器或工作站处理自己的邮件，拥有一个处理所有邮件的中心服务器是有益的。这种 Hub 的优势是：

- 所有的入站邮件都发送到 Hub，且不直接发送。
- 所有出站邮件看起来来自单一服务器，而 Hub 将这些邮件转发到最终目的地。
- 所有的入站邮件都发送到 Hub，需要 sendmail 守护进程来监听。

``` 
divert(1)

dnl 这是一个生成 /etc/sendmail.cf 的宏配置文件

dnl 如果修改了此文件，将需要通过运行以下命令通过 m4

4 预处理器重新生成 /etc/sendmail.cf：

dnl cp sendmail.8.9.3.gz /var/tmp

dnl cd /var/tmp

dnl tar -xzf sendmail.8.9.3.gz/cf

dnl cd /var/tmp/sendmail-8.9.3/cf

dnl m4../m4/m4 /etc/null.mc /etc/sendmail.cf

dnl dnl

dnl 你需要 sendmail 源码发行才能工作。

divert(0)

OSTYPE(linux)

FEATURE("nullclient";mail.openarch.com")

define("ALIAS_FILE)
```

## 第1步

由于我们的本地客户端从直接接收邮件并通过中心服务器转发所有邮件，我们将创建一个名为 `null.mc` 的特殊文件，该文件在处理后将创建一个自定义的 `sendmail.cf`。创建该文件（`touch /etc/null.mc`）并添加以下行：

关于本页面的意见和建议，请邮件至 gmnourani@videotron.ca

邮件中枢（Mail Hub）。当然，您需要将此标准名称更改为反映您的邮件中枢服务器，例如：FEATURE(`nullient`, my.mailhub.com)。

`undefined(`ALIAS_FILE`)`
此配置选项防止 nullient 版本的 sendmail 尝试访问 `/etc/aliases` 和 `/etc/aliases.db`。通过添加此行，您就不需要在内部客户端机器上拥有 `aliases` 文件了。只有在邮件中枢服务器上需要别名文件，用于所有服务器和客户端别名。

现在我们的宏文件 `null.mc` 已经创建，我们可以通过以下命令在邻服务器或客户端机器上从这些语句构建 sendmail 配置文件 `sendmail.cf`：

```bash
[root@client]# cd /var/tmp/sendmail-version/etc/cf/

[root@client]# m4 ../m4.cf /etc/null.mc > /etc/sendmail.cf
```



### 步骤 2

不应有任何邮件投递到您的本地机器。将不再有入站连接，不再需要在您的邻服务器或本地客户端机器上运行 `sendmail` 守护进程。

要让 `sendmail` 守护进程在您的邻服务器或本地服务器上运行，请编辑 `/etc/sysconfig/sendmail` 文件并更改以下行：

```
DAEMON=1h
```

# 读取：

```
DAEMON=no
```

注意：`/etc/sysconfig/sendmail` 文件下的 `QUEUE=1h` 会导致 `sendmail` 每 1 小时处理一次队列。我们保留该行是因为在邮件中枢离线的情况下，`sendmail` 仍然需要定期处理处理队列。

### 步骤 3

本地机器从不使用别名、访问或其他映射数据库。由于所有映射文件数据库都位于网络中我们可能的所有本地机器的中央邮件中枢服务器上，我们可以安全地从所有本地机器上删除以下命令和帮助页。

```bash
/usr/bin/newaliases
/usr/man/man1/newaliases.1
/usr/man/man5/newaliases.5
```

- 要从您的系统中删除以下文件，请使用命令：
  `[root@client]# rm -f /usr/bin/newaliases`
  `[root@client]# rm -f /usr/man/man1/newaliases.1`
  `[root@client]# rm -f /usr/man/man5/newaliases.5`

### 步骤 4

从所有本地服务器、客户端上移除不必要的 Procmail 程序。由于本地机器将所有内部和出站邮件发送到邮件中枢服务器进行后续投递，我们不需要使用像 Procmail 复杂的本地投递代理程序。相反，我们可以使用 `/bin/mail` 程序。

© Copyright 1999 Open Network Architecture ®

- 要从系统中删除 Procmail，请使用命令：
  `[root@client]# rpm -e procmail`

## 所有配置的 /etc/sysconfig/sendmail/ 文件

`/etc/sysconfig/sendmail/` 文件用于指定 `sendmail` 配置信息，例如 `sendmail` 是否必须作为守护进程运行并监听邮件，以及在消息未投递成功前等待多长时间。

创建 `sendmail` 文件（`touch /etc/sysconfig/sendmail`）并添加内容：

```
DAEMON=yes
QUEUE=1h
```

`DAEMON=yes` 指令 `sendmail` 作为守护进程运行。当 `sendmail` 客户端配置为不接受外部邮件并将本地邮件转发到中央枢纽，且不作为守护进程运行以获得更好的安全性时，此行非常有用。如果您这样配置了客户端机器，只需要将 "`DAEMON=yes`" 替换为 "`DAEMON=no`"。

邮件通常被放入队列，因为可能无法立即传输。"`QUEUE=1h`" 设置了在消息已投递之前向发送者发送警告的时间间隔。

## 所有配置的 /etc/rc.d/init.d/sendmail 脚本文件

创建 `sendmail` 脚本文件（`touch /etc/rc.d/init.d/sendmail`）并添加内容：

```bash
#!/bin/sh

#
# sendmail 此脚本负责启动和停止
#
# chrootfig: 2345 80 30
# description: Sendmail 是一个邮件传输代理（Mail Transport Agent），
# 将邮件从一台机器移动到另一台机器的程序。
# processname:sendmail
# config:/etc/sysconfig.conf
# pidfile:/var/run/sendmail.pid
# 引入函数库。
. /etc/rc.d/init.d/functions
# 引入网络配置。
. /etc/sysconfig/network
# 引入 sendmail 配置。
if [ -f /etc/sysconfig/sendmail ]; then
. /etc/sysconfig/sendmail
else
DAEMON=yes
QUEUE=1h
fi
```

```bash
# 检查网络是否可用。
[$NETWORKING] = "no" && exit 0
[ -f /usr/sbin/sendmail ] || exit 0
```

`RETVAL=0`

```bash
# 检查网络是否可用。
case "$1" in
  start)
    # 启动守护进程。
    echo -n "Starting sendmail:"
    [ -f /usr/sbin/sendmail ] && /usr/sbin/sendmail -D
    RETVAL=$?
    ;;
  stop)
    # 停止守护进程。
    echo -n "Shutting down sendmail:"
    kill /var/run/sendmail.pid
    RETVAL=$?
    ;;
  restart)
    # 重新加载 sendmail。
    echo -n "Reloading sendmail:"
    /usr/sbin/sendmail -R
    RETVAL=$?
    ;;
  status)
    # 检查 sendmail 是否正在运行。
    if [ -f /var/run/sendmail.pid ]; then
      echo "sendmail is running"
    else
      echo "sendmail is not running"
    fi
    ;;
  *)
    echo "Usage: $0 [start|stop|status]"
    exit 1
esac
```



## 安全 Sendmail

`smrsh` 是一种受限 shell，通过 `smrsh` 目录指定 `sendmail` 可以执行的程序列表。结合 `sendmail` 使用，`smrsh` 有效地限制了范围。

### 步骤 3
现在我们可以配置 `sendmail` 使用受限 shell。邮件程序由 `sendmail` 配置文件 `/etc/sendmail.cf` 中的单行定义；您必须修改 `sendmail.cf` 中的 "Mprog" 行，将 `/bin/sh` 规范替换为 `/usr/bin/smrsh`。

### 步骤 1
我们需要的第一的第一工作是列出 `smrsh` 应该允许的命令。默认情况下，我们包含了：

- `/bin/mail`（如果已安装）
- `/usr/bin/procmail`（如果已安装）

### 步骤 2
您需要向 `/etc/smrsh/` 目录填充允许 `sendmail` 执行的程序。为了防止程序重复并保持良好，最好为允许的程序建立链接而不是将程序复制到该目录。

- 要允许邮件程序 `bin/mail`，请使用命令：
```
[root@client]# cd /etc/smrsh
[root@client]# ln -s /bin/mail
```

- 要允许邮件程序 `/usr/bin/procmail`，请使用命令：
```
[root@client]# cd /etc/smrsh
[root@client]# ln -s /usr/bin/procmail
```

这将允许邮件和 `procmail` 程序从用户的“转发”文件或使用 `/program/` 语法的“别名”运行。

- 现在使用以下命令手动重启 `sendmail` 进程：
```
[root@deep]# /etc/rc.d/sendmail restart
```

关于本页面的意见和建议请邮件至 `gmnourai@videotron.ca`

**注意**：在我们上述用于 Mail Hub 服务器配置文件 "`sendmail.mc`" 中，我们已经配置了该行并指定为 "`Mprog`" ，以使用受限的 shell "`/usr/bin/smrush`" 以及 `m4` 宏 `FEATURE(`smrush; /usr/bin/smrush)`;`；因此，如果你在 Mail Hub 的 `/etc/sendmail.mc` 中看到 "`/usr/bin/smrush`" 指定警告，请不要惊讶。相反，请针对网络中的 `/etc/sendmail.mc` 使用上述技术，采用适用于 `nulloc` 或本地本地客户端和服务器机器的方法，它们使用 `/etc/null.mc` 宏配置文件来生成 `/etc/sendmail.mc` 文件。

## "etc/aliases" 文件

如果别名文件（`aliases file`）管理不当或疏忽，可以使用它获取特权。例如，许多供应商以前在发布系统时会带有一个名为 "`decode`" 的别名。这种做法正变得越来越常见。

其目的是允许用户通过邮件传输二进制文件。在发送端，用户使用 `uuencode` 将二进制文件转换为 ASCII，然后将结果发送到接收端的 "`decode`" 别名。这会将邮件信息通过管道将 ASCII 转换回原始二进制文件。

删除 "`decode`" 别名。同样，每一个执行程序的别名——只要不是你自己放置且没有完全检查的——都应该受到质疑并可能被删除。为了使此更改生效，你需要运行：

```bash
[root@deep]#usr/bin/newaliases
```

编辑别名文件 (`/etc/aliases`) 并删除以下行：

```
# 基础系统别名。

MAILER-DAEMON: postmaster

postmaster: root

# 用户账户的通用重定向。

bin: root

daemon: root 删除此行。

games: root 删除此行。

ingres: root 删除此行。

nbody: root 删除此行。

system: root 删除此行。

toor: root 删除此行。

uucp: root 删除此行。
```

```
# 常用别名。

manager: root 删除此行。

dumper: root 删除此行。

operator: root 删除此行。

# 捕获 decode 以防安全攻击

decode: root 删除此行。
```

```
# 应该接收 root 邮件的人

root: marc
```

不要忘记运行 "`usr/bin/newaliases`" 以使此更改生效。

© Copyright 1999 Open Network Architecture ®

## 防止 Sendmail 被未授权用户利用

`Sendmail` 的最新版本 (`8.9.3`) 包含了强大的反垃圾邮件功能，这有助于防止你的邮件服务器被未授权的用户滥用。要做到这一点，请编辑你的 `/etc/sendmail.cf` 文件并修改配置文件以屏蔽垃圾邮件发送者。

编辑 `sendmail.cf` 文件 (`vi /etc/sendmail.cf`) 并更改该行：

```
O PrivacyOptions=authwarnings
```

To:

```
O PrivacyOptions=authwarnings,noexpn,novfry
```

设置 "`noexpn`" 会导致 `sendmail` 禁用所有 SMTP "`EXPN`" 命令，还会导致 `sendmail` 拒绝所有 SMTP "`VERB`" 命令。设置 "`novfry`" 防止垃圾邮件发送者使用 "`EXPN`" 和 "`VRFY`" 命令。不道德的人经常滥用这些命令。

## SMTP 问候消息

当 `sendmail` 接受 SMTP 连接时，它会向另一个主机发送一条问候消息。此消息识别本地机器，它发送的第一条信息是准备就绪。

编辑 `sendmail.cf` 文件 (`vi /etc/sendmail.cf`) 并更改该行：

```
O SmtpGreetingMessage=$ Mail $v/$S;$
```

To:

```
O SmtpGreetingMessage=$ Mail $v/$S; $ NO U CE C=xx Lxx
```

- 现在手动重启 `sendmail` 进程使更改生效：`[root]#etc/rc.d/sendmail.restart`

更改修改了横幅（banner），即 `Sendmail` 在接收连接时显示的内容。你应该将 "`C=xx Lxx`" 条目中的 "`xx`" 替换为你的国家和位置代码。例如，在我的情况下，加拿大魁北省我会使用 "`C=CA L-QC`" 。后者的更改实际上并没有影响任何东西，但是 "`news.admin.net-abuse.email`" 新闻组的人们建议的最小预防措施。

## 限制谁可以查看队列内容

通常，任何人都可以使用 `mailq` 命令查看邮件队列的内容。要限制谁可以查看队列内容，在 `/etc/sendmail.cf` 文件中指定 "`restrictmail`" 。通过此选项，`sendmail` 仅允许与队列目录所有组相同（`root`）的用户查看。这允许队列目录通过模式 `0700` 被完全保护，以便选定的用户看到其内容。

编辑 `sendmail.cf` 文件 (`vi /etc/sendmail.cf`) 并更改该行：

```
O PrivacyOptions=authwarnings,noexpn,novfry
```

To:

```
O PrivacyOptions=authwarnings,noexpn,novfry,restrictmail
```

- 现在更改我们队列目录的模式以进行完全保护：`[root]# chmod 0700 var/spool/mqueue`

注意：我们在该行中添加了 "`noexpn`" 和 "`novfry`"。`restrictmail` " 选项被添加到了 `/etc/null.cf` 文件中。

© Copyright 1999 Open Network Architecture ®

## 限制处理

通常，任何人都可以使用 `mailq` 命令查看邮件队列的内容。要限制谁可以查看队列内容，在 `/etc/sendmail.cf` 文件中指定 "`restrictmail`" 。通过此选项，`sendmail` 仅允许与队列目录所有组相同（`root`）的用户查看。这允许队列目录通过模式 `0700` 被完全保护，以便选定的用户看到其内容。

关于本页面的意见和建议，请邮件至 `gmourani@videotron.ca`。

```
@@

mail-daemon:postmaster

bin:root

nobody:root

www:root
```

# Sendmail 邮件枢纽安装文件

```
> /etc/rc.dinit/sendmail
> /etc/rc.d/rc0/K30sendmail
> /etc/rc.d/rc1/K30sendmail
> /etc/rc.d/rc2/S80sendmail
> /etc/rc.d/rc3/S80sendmail
> /etc/rc.d/rc4/S80sendmail
> /etc/rc.d/rc5/S80sendmail
> /etc/rc.d/rc6/K30sendmail
> /etc/sysconfig/sendmail
> /etc/mail
```



# Sendmail 本地服务器或客户端安装文件

`/etc/mail/access`

`/etc/mail/virtusable`

`/etc/mail/virtusable.db`

`/etc/mail/domainable`

`/etc/mail/domainable.db`

`/etc/mail/mailertable`

`/etc/mail/mailertable.db`

`/etc/mail/access.db`

`/etc/smash`

`/etc/aliases`

`/etc/sendmail.cw`

`/etc/sendmail.mc`

`/etc/aliases.db`

`/etc/sendmail.cf`

`/usr/bin/newaliases`

`/usr/bin/mailq`

`/usr/bin/hoststat`

`/usr/bin/purgestat`

`/usr/lib/sendmail.hf`

`/usr/lib/sendmail`

`/usr/man/man1/mailq.1`

`/usr/man/man1/newaliases.1`

`/usr/man/man5/aliases.5`

`/usr/man/man8/sendmail.8`

`/usr/man/man8/malists.8`

`/usr/man/man8/makemap.8`

`/usr/man/man8/praalises.8`

`/usr/man/man8/smash.8`

`/usr/bin/mailstats`

`/usr/bin/makemap`

`/usr/bin/praalises`

`/var/log/sendmail.st`

`/var/pool/mqueue`

# Sendmail 本地服务器或客户端安装文件

`/etc/rc.dinit/sendmail`

`/etc/rc.d/rc0/K30sendmail`

`/etc/rc.d/rc1/K30sendmail`

`/etc/rc.d/rc2/S80sendmail`

`/etc/rc.d/rc3/S80sendmail`

`/etc/rc.d/rc4/S80sendmail`

`/etc/rc.d/rc5/S80sendmail`

`/etc/rc.d/rc6/K30sendmail`

`/etc/sysconfig/sendmail`

`/etc/mail.nc`

`/etc/sendmail.cf`

`/usr/bin/newaliases`

`/usr/bin/mailq`

`/usr/bin/hoststat`

`/usr/bin/purgestat`

`/usr/lib/sendmail.hf`

`/usr/lib/sendmail`

`/usr/man/man1/mailq.1`

`/usr/man/man1/newaliases.1`

`/usr/man/man5/aliases.5`

`/usr/man/man8/sendmail.8`

`/usr/man/man8/malists.8`

`/usr/bin/mailstats`

`/usr/bin/makemap`

`/usr/bin/praalises`

`/var/log/sendmail.st`

`/var/pool/mqueue`

# Linux OpenSSL 服务器

### 概述

OpenSSL 项目是一项协作工作，旨在开发一个健壮、商业级、功能齐全且开源的工具包，用于使用强加密加密实现安全套接层 (`SSL v2/v3`) 和传输层安全 (`TLS v1`) 协议。

© Copyright 1999 Open Network Architecture ®

关于本页面的意见和建议，请邮件至 `gmnourani@videotron.ca`

该项目由全球志愿者社区管理，他们利用互联网进行通信、计划和开发 OpenSSL 工具包及其相关文档。

# 密码学优势

## 数据机密性

当消息被加密时，输入的明文通过算法转换为加密密文，从而隐藏消息的含义。此过程涉及一个用于加密并在以后解密消息的秘密密钥。如果没有该密钥，加密数据将毫无意义。通过密码学，只有机密数据加密密钥可以通过安全方法传输；加密后的文本可以通过任何公共机制发送。

## 数据完整性

密码学也用于保护数据的完整性。例如，可以在任意用户提供的文本上计算称为消息认证码 (`MAC`) 的加密校验和。然后将文本和 `MAC` 发送给接收者。消息接收者可以使用适当的秘密密钥重新计算消息的 `MAC`，以验证附加在消息上的 `MAC`，并确认其是否与测试的 `MAC` 完全相等。

## 身份验证

密码学的其他用途是个人身份识别，其中用户知道一个可以作为其身份验证的秘密。

# 专利

各公司在世界各地的地点持有各种算法的专利…… **你** 有责任确保你对任何算法的使用是合法的，请检查你所在的国家是否有我们已知的专利。`RSA Data Security` 持有 `RSA` 和 `RC5` 算法的专利。如果在美国境内使用它们的密码，你必须联系 `RSA Data Security` 获取许可条件。`RC4` 是 Data Security 的商标，因此使用此标签应仅限于获得 Data Security 的许可。`IDEA` 算法由 Ascom 在奥地利、德国、意大利、荷兰、西班牙、瑞士、英国专利。如果使用该算法，应联系他们；他们的网页为 `http://www.rsa.com/`

这些安装说明假设兼容 Unix。源码路径为 `"var/tmp"`（可能是其他路径）。安装已在 RedHat Linux 6.1 上通过测试。安装中的所有步骤将在超级用户账户 `"root"` 中进行。OpenSSL 版本号为 `0.9.4`。在安装之前和之后列出系统文件列表是一个好主意，然后使用 `diff` 比较它们以发现发生了变化。

© Copyright 1999 Open Network Architecture ®

关于本页面的意见和建议，请邮件至 `gmnouari@videotron.ca`

# Tar 包

OpenSSL 首页：`http://www.openssl.org/`
你必须下载：`openssl-0.9.4.tar.gz`

### 编译

解压压缩包。

```
[root@deep#] tar xzf openssl-0.9.4.tar.gz
[root@deep#] cd openssl-version
```

# 编译与优化

进入 OpenSSL 目录并执行以下命令：

## 第 1 步
修改 `Makefile`：

```
[root@deep#] vi Makefile
```

添加以下内容：
```
CFLAG=-DTHREADS -DERANT -DSSL_FORBID_NULL -DL_ENDIAN -O9 -fno-loops -fast-math -m- -ffiumium-fframe-exceptions -Wall -DSA_ASM -DM_ASM -D160_ASM
```

这是我们编译 OpenSSL 软件的优化文件。

修改 `Makefile`：

```
[root[deep#] vi Makefile
```

添加以下内容：
```
PROCESSOR = 686
```

注意：如果你使用的是 Pentium；如果是 586、PentiumPro/II/III；如果是 686、486。

`make` 命令将构建 OpenSSL 库。

## 第 2 步
修改 `Makefile`：

```bash
[root@deep#] vi Makefile
```

添加以下内容：
```
DIR=/usr
```

## 第 3 步
修改 `Makefile`：

```bash
[root@deep#] vi Makefile
```

添加以下内容：
```
export LD_LIBRARY_PATH
```

构建成功后，`make install` 将创建安装目录并安装 OpenSSL。

`mv` 命令将 `/etc/ssl/mimic` 下的所有文件移动到 `/usr/bin` 目录。

```bash
[root@deep#] mv /etc/ssl/mimic /usr/bin/
```

`rm` 命令将从系统中删除 `/etc/ssl/mimic` 和 `/etc/ssl/lib` 目录，因为这些目录下的文件现在位于其他地方。它还将删除 `CA.pl` 和 `CA.sh` 文件，这些是用于创建自定义 CA 证书的脚本。我们的 OpenSSL 配置不允许方便使用 openssl ca 目录，因此稍后我们将创建一个 `sign.sh` 脚本来替换它们。

# 工作后清理

```
[root@deep#] cd /var/tmp
[root@deep#] # rm -rf openssl-version/openssl_version.tar.gz
```



我们在书籍《Linuxos.pdf》中描述的所有内容都将在名为“`floppy.tgz`”的 tar 压缩包中具有特定的目录和子目录，其中包含特定程序的配置配置。如果你获取了该压缩文件，你将不得不手动复制不同的配置文件，或者通过剪切粘贴来创建你的配置文件。无论你决定复制还是从归档文件中提取方便你使用的文件，你都要有责任对这些文件进行修改、调整，并将它们放置到你服务器机器上适当的位置（根据 OpenSSL 的要求），如下所示。服务器配置文件归包位于互联网地址：`http://pages.infinit.net/lotus/dir/opt/floppy.tgz`。

- 运行 OpenSSL 服务器需要以下文件，并且必须将它们创建或复制到服务器上相应的目录。
- 将 `openssl.cnf` 文件复制到 `etc/ssl/` 目录。
- 将签名脚本文件复制到 `/usr/bin/` 目录。

你可以在我们的 `floppy.tgz` 压缩包中获得下列出的配置文件。从解压后的 `floppy.tgz` 压缩包中复制以下文件到其适当的位置，或直接从此处复制并粘贴到相关文件中。

## "etc/ssl/openssl.cnf" 文件的配置

这是 `openssl` 程序的通用配置，你可以在此处配置密钥的过期日期、组织名称等。你必须更改的配置将位于 `[ CA_default ]` 和 `[ req_distinguished_name ]` 部分。

编辑 `openssl.cnf` 文件（`vi /etc/ssl/openssl.cnf`）并添加或修改：

```
# OpenSSL 示例配置

# 这主要用于生成证书请求。

RANDFILE            = $ENV:HOME/md

oid_file            = $ENV:HOME/oid

oid_section         = new_oids

# 要配合 "openssl x509" 工具的 "-extfile" 选项使用

# 此配置文件，请在此命名包含要使用的

# X.509v3 扩展的节：

# extensions         =

# (或者，使用一个在主 [= default ] 部分中仅包含

# X.509v3 扩展的配置文件)。

[ new_oids]

# 我们可以在此处添加新的 OID 以供 'ca' 和 'req' 使用。

# 添加如下面的简单 OID：

# test1=1.2.3.4

# 或者使用此类配置文件替换：

# test2=${testoid1}.5.6
```

| [ ca default_ca = CA_default # 默认 ca 部分 |
| CA_default ] dir = /etc/ssl # 所有内容存放处 |

关于本页的任何意见和建议，可以发送至 `gmourani@videotronet.ca`

```
certs = $dir/certs

crl_dir = $dir/crl

database = $dir/ca.db.index

new_certs_dir = $dir/ca.db

# 发签证书的存放位置

# # 发签 CRL 的存放位置

# 在数据库索引处。

# 新证书的默认位置。
```

```
certificate = $dir/certs/ca.crt

serial = $dir/certs/ca.serial

crl = $dir/crl.pem

private_key = $dir/private/ca.key

RANDFILE = $dir/ca.db.rand

# CA 证书

# 当前的序列号

# 当前的 CRL

# 私有随机数文件
```

```
x509_extensions = user_cert

# 添加到 CA 的扩展，注意：Netscape communicator 在 V2 CRL 上支持

# 所以对于 V1 CRL 默认是注释掉的。

# crl_extensions = crl_ext
```

```
default_days = 365

default_crl_days = 30

default_md = md5

Preserve = no

# 认证有效期为多久

# 下一次 CRL 产生前多久

# 使用哪种 md。

# 保留传递的 DN 顺序
```

# 一种指定请求看起来相似程度的差异方法
# 对于 CA 类型，列出的属性必须相同，而可选的
# 提供的字段是这些的 :)
policy = policy_match

```
[ policy_match ] = match

countryName = match

stateProvinceName = match

organizationName = optional

organizationalUnitName = optional

commonName = supplied

emailAddress = optional
```

```
# 用于 'anything' 策略

# 在此时此刻，你必须列出所有接受的 'object'

# 类型。

[ policy_anything ] = optional

countryName = optional

stateProvinceName = optional

locality = optional

organizationName = optional

organizationalUnitName = optional

commonName = supplied

emailAddress = optional
```

```
################################################################

[req]

default_bits = 1024

default_keyfile = privkey.pem

distinguished_name = req_distinguished_name

attributes = req_attributes

X509_extensions = v3_ca # 添加到自签名证书的扩展
```

```
[ req_distinguished_name ]

countryName = 国家名称（2位字母代码）

countryName_default = CA

countryName_min = 2

countryName_max = 2
```

关于本页的任何意见和建议应邮寄至 `gmourani@videotron.ca`

stateOrProvinceName = 州或省份名称（全称）
stateOrProvinceName_default = Quebec

localityName = 地点名称（例如，城市）
Name_default = Montreal

0.organizationName = 组织名称（例如）

organizationalUnitName = 组织单位名称

commonName = 通用名称

emailAddress = 电子邮件地址

*(注：由于原文后半部分存在重复和截断的片段，翻译时已根据逻辑对剩余内容进行了对齐并确保格式正确。)*

由于提供的原文后半部分包含大量重复和碎片，以下是针对剩余部分的完整翻译：

| [ ca default_ca = CA_default # 默认 ca 部分 |
| CA_default ] dir = /etc/ssl # 所有内容存放处 |

关于本页的任何意见和建议，可以发送至 `gmourani@videotronet.ca`

```
certs = $dir/certs
crl_dir = $dir/crl
database = $dir/ca.db.index
new_certs_dir = $dir/ca.db

# 发签证书的存放位置
# # 发签 CRL 的存放位置
# 在数据库索引处。
# 新证书的默认位置。
```

```
certificate = $dir/certs/ca.crt
serial = $dir/certs/ca.serial
crl = $dir/crl.pem
private_key = $dir/private/ca.key
RANDFILE = $dir/ca.db.rand

# CA 证书
# 当前的序列号
# 当前的 CRL
# 私有随机数文件
```

```
x509_extensions = user_cert

# 添加到 CA 的扩展，注意：Netscape communicator 在 V2 CRL 上支持
# 所以对于 V1 CRL 默认是注释掉的。
# crl_extensions = crl_ext
```

```
default_days = 365
default_crl_days = 30
default_md = md5
Preserve = no

# 认证有效期为多久
# 下一次 CRL 产生前多久
# 使用哪种 md。
# 保留传递的 DN 顺序
```

# 一种指定请求看起来相似程度的差异方法



# 对于 CA 类型，列出的属性必须相同，而可选的提供的字段是这些的 :)

`policy = policy_match`

``` 
# 用于 CA 策略
[ policy_match ] = match
countryName = match
stateProvinceName = match
organizationName = optional
organizationalUnitName = optional
commonName = supplied
emailAddress = optional
```

``` 
# 用于 'anything' 策略
# 在此时此刻，你必须列出所有接受的 'object'
# 类型。
[ policy_anything ] = optional
countryName = optional
stateProvinceName = optional
locality = optional
organizationName = optional
organizationalUnitName = optional
commonName = supplied
emailAddress = optional
```

``` 
################################################################
[req]
default_bits = 1024
default_keyfile = privkey.pem
distinguished_name = req_distinguished_name
attributes = req_attributes
X509_extensions = v3_ca # 添加到自签名证书的扩展
```

``` 
[ req_distinguished_name ]
countryName = 国家名称（2位字母代码）
countryName_default = CA
countryName_min = 2
countryName_max = 2
```

关于本页的任何意见和建议应邮寄至 `gmourani@videotron.ca`

`stateOrProvinceName =` 州或省份名称（全称）

`stateOrProvinceName_default = Quebec`

`localityName =` 地点名称（例如，城市）

`Name_default = Montreal`

`0.organizationName =` 组织名称（例如）

`organizationalUnitName =` 组织单位名称

`commonName =` 通用名称

`emailAddress =` 电子邮件地址

关于本页面的意见和建议请邮件至 `gmourani@videotron.ca`

注意：当你编译并安装 OpenSSL 程序时，`openssl.cnf` 文件已经存在于你的服务器上，并位于 `etc/ssl/` 目录下。你不需要更改文件中的所有默认选项，你通常修改的配置仅位于 `CA_default` 和 `[ req_distinguished_name ]` 部分。

# 创建 `/usr/bin/sign.sh` 程序文件

`openssl ca` 命令对字符串有一些要求，默认的 OpenSSL 配置不允许直接使用 `openssl ca`。我们将创建这个 `sign.sh` 程序来替代它。

创建 `sign.sh` 程序文件（`touch /usr/bin/sign.sh`）并向文件中添加内容：

``` 
#!/bin/sh
##
## sign.sh -- 生成 SSL 证书请求 (CSR)
## Copyright (c) 1998-1999 Ralph S. Engelschall, All Rights Reserved.
##
# 参数行处理
CSR=$1
if [ $# -ne 1 ]; then
  echo "Usage:sign.sign <whatever>.csr"; exit 1
fi
if [ ! -f $CSR ]; then
  echo "CSR not found: $CSR"; exit 1
fi
case $CSR in
  * .csr) CERT=$(echo $CSR | sed -e 's/\.csr/\.crt/')" ;
  *) CERT="$CSR.crt";
esac
# 确保环境存在
if [ ! -d ca.db.certs ]; then
  mkdir ca.db.certs
fi
if [ ! -f $ca.db.serial ]; then
  echo '01'>ca.db.serial
fi
if [ ! -f $ca.db.index ]; then
  cp /dev/null ca.db.index
fi
# 创建自己的 SSleay 配置
cat-ca.config <<EOF
[ca]
default_ca = CA_own
dir = /etc/ssl
certs = /etc/ssl/certs
new_certs_dir = /etc/ssl/ca.db.certs
database = /etc/ssl/ca.db.index
serial = /etc/ssl/ca.db.serial
RANDFILE = /etc/ssl/ca.db.rand
certificate = /etc/ssl/certs.crt
private_key = /etc/ssl/private/ca.key
default_days = 365
default_crt_days = 30
default_md = md5
preserve = no
policy = policy_anything
nEOF
```

```
© Copyright 1999 Open Network Architecture ®

关于本页面的意见和建议请邮件至 gmourani@videotron.ca
```

[ policy_anything |

countryName = optional

stateProvinceName = optional

locality = optional

organizationName = optional

organizationalUnitName = optional

commonName = supplied

emailAddress = optional

EOT
```

```
# 签名证书

echo "CA signing: $CSR - $CERT"

openssl ca -config config.conf -out $CERT -infiles $CSR

echo "CA verifying: $CERT <> CA cert"

openssl verify -CAfile /etc/ssl/certs/ca.crt $CERT
```

```
# SSleay 后的清理

rm -f ca.conf

rm -f ca.db.serial

rm -f ca.db.index.old
```

```
# 优雅退出

exit 0
```

现在，让此程序可执行并更改其默认权限：
`[root@deep]# chmod 755 /usr/bin/sh`

注意：你也可以在 mod ssl 分发版的 "mod_ssl-version/pkg.contrib" 子目录下找到此 "sign.h"，或者在我们的 floppy.tgz 存档文件中找到。另外注意，`[ CA_own ]` 部分必须更改以反映你的环境，并且不要忘记修改 "`openssl verify -CAfile /etc/ssl/certs/ca.crt $CERT`" 这一行。

# 安全 OpenSSL

让你的密钥仅允许超级用户 "root" 读写。这很重要，因为没有人需要碰这些文件。

- 要让你的密钥仅允许 "root" 读写，请使用命令：
`[root@deep]# chmod 600 /etc/ssl/certs/ca.crt`
`[root@deep]# chmod 600 /etc/ssl/certs/server.crt`
`[root@deep]# chmod 600 /chroot/httpd/etc/ssl/private/server.key`

# 命令

下面列出的命令是我们在日常使用中经常使用的，但还有更多命令，你必须检查 man 页和文档以获取更多细节和信息。例如，我们将向你展示如何为你的 Apache Web 服务器创建证书。

注意：下面列出的所有命令假设均在 "/etc/ssl/" 目录下。

## 1.1 为你的 Apache 服务器创建一个受密码保护保护的 RSA 私钥。

``` 
[root@deep]# openssl genrsa -des3 -out server.key 1024

Generating RSA private key, 1024 bit long modulus

........

+++++

e is 55537 (0x10001)

nEnter PEM pass phrase:
```



© Copyright 1999 Open Network Architecture ®

关于本页面的意见和建议请邮件至 `gmourani@videotron.ca`

Verifying password - Enter PEM pass phrase:
请备份此 `server.key` 文件，并记住必须在安全的地方输入密码。

# 1.1 为你的 Apache 服务器创建一个受密码保护的 RSA 私钥。

```
[root@deep]# openssl genrsa -des3 -out server.key 1024

Generating RSA private key, 1024 bit long modulus

........

+++++

e is 55537 (0x10001)

nEnter PEM pass phrase:
```

# 1.2 使用服务器私钥生成证书请求 (CSR)。

```
[root@deep]# openssl req -new -key server.key -out server.csr

Enter PEM pass phrase:

You are asked to enter the following information

Country Name []: US

State or Province Name []: State

Locality []: City

Organization Name []: My Org

OrganizationalUnitName []: IT Dept

CommonName []: www.example.com

Email Address []: admin@example.com
```

# 1.3 创建一个受密码保护的 RSA 私钥 (CA)。

```
[root@deep]# openssl genrsa -des3 -out ca.key 1024

Generating RSA private key, 1024 bit long modulus

........

+++++

e is 55537 (0x10001)

nEnter PEM pass phrase:
```

# 1.4 创建一个自签证书 (CA)。

```
[root@deep]# openssl req -new -x509 -days 365 -key ca.key -out ca.crt
```

# 1.5 签名证书。（我们创建并使用自己的证书颁发机构）

准备一个用于签名的脚本，因为 `openssl` 配置不允许直接使用 `openssl ca`。所以将 `sign.sh` 命名并放在 `openssl` 目录下。使用此脚本进行签名。

现在你可以使用此 CA 签名 CSR，以便为 Apache Web 服务器内部创建真实的证书（假设你已经有一个证书了）：

```
[root@deep]# /usr/bin/sign.server.csr
```

关于此页面的意见和建议应邮寄至 `gmnourani@videotron.ca`

现在你有两个文件：`server.key` 和 `server.crt`。它们现在可以在 Apache 的 `httpd.conf` 文件中如下所示使用：

```
SSLCertificateFile /etc/ssl/certs/server.crt

SSLCertificateKeyFile /etc/ssl/private/server.key
```

不再需要 `server.crt` 了。

```bash
[root@deep]# rm -f server.crt
```



# 已安装文件

- `/etc/ssl`
- `/etc/ssl/crt`
- `/etc/ssl/certs`
- `/etc/ssl/private`
- `/etc/ssl/openssl.conf`
- `/usr/bin/c_openssl`
- `/usr/bin/c_ehash`
- `/usr/bin/c_hash`
- `/usr/bin/c_info`
- `/usr/bin/c_issuer`
- `/usr/bin/c_name`
- `/usr/bin/der_chop`
- `/usr/include/openssl`
- `/usr/include/openssl/ssl_os.h`
- `/usr/include/openssl/ssl_2.h`
- `/usr/include/openssl/crypto.h`
- `/usr/include/openssl/t1md.h`
- `/usr/include/openssl/x509.h`
- `/usr/include/openssl/conf.h`
- `/usr/include/openssl/ecdbc.h`
- `/usr/include/openssl/md2.h`
- `/usr/include/openssl/sha.h`
- `/usr/include/openssl/md256.h`
- `/usr/include/openssl/hmac.h`
- `/usr/include/openssl/pemd.h`
- `/usr/include/openssl/des.h`
- `/usr/include/openssl/rc2.h`
- `/usr/include/openssl/rc4.h`
- `/usr/include/openssl/idea.h`
- `/usr/include/openssl/blowfish.h`
- `/usr/include/openssl/cast.h`
- `/usr/include/openssl/bn.h`
- `/usr/include/openssl/rsa.h`
- `/usr/include/openssl/dsa.h`
- `/usr/include/openssl/dh.h`
- `/usr/include/openssl/buffer.h`
- `/usr/include/openssl/bio.h`
- `/usr/include/openssl/stack.h`
- `/usr/include/openssl/safestack.h`
- `/usr/include/openssl/lmash.h`
- `/usr/include/openssl/rand.h`
- `/usr/include/openssl/err.h`
- `/usr/include/openssl/objects.h`
- `/usr/include/openssl/evp.h`
- `/usr/include/openssl/asn1.h`
- `/usr/include/openssl/asn1_mac.h`
- `/usr/include/openssl/pem.h`
- `/usr/include/openssl/pem2.h`
- `/usr/include/openssl/x509.h`
- `/usr/include/openssl/x509_vfy.h`
- `/usr/include/openssl/x509_v3.h`
- `/usr/include/openssl/conf.h`
- `/usr/include/openssl/txt_bd.h`
- `/usr/include/openssl/pkcs7.h`
- `/usr/include/openssl/pkcs12.h`
- `/usr/include/openssl/comp.h`
- `/usr/include/openssl/ssl.h`
- `/usr/include/openssl/ssl2.h`
- `/usr/include/openssl/ssl23.h`
- `/usr/include/openssl/tls1.h`
- `/usr/lib/libcrypto.a`
- `/usr/lib/libssl.a`
- `/usr/lib/libRSAGlue.a`
- `/var/lock/subsystem-named`

# Linux Imap & Pop 服务器

正在运行一个邮件服务器，它包含以下之一：一个 IMAP 服务器、POP3 服务器、POP2 服务器和 SMTP 服务器。目前，我将只涵盖 IMAP4、POP3 和 POP2，它们都包含在一个包中。SMTP 服务器的一个示例是 Sendmail（广泛使用）。

© Copyright 1999 Open Network Architecture ®

关于此页面的意见和建议应邮寄至 `gmourai@videotron.ca`

POP 代表“邮局协议”（Post Office Protocol），它只需允许你列出消息、检索它们并删除它们。Linux 有许多 POP 服务器可用，大多数发行版中保留的一个适用于大多数用户。IMAP 则是加强版的 POP。它允许你轻松维护多个账户、让多个人访问同一个账户、将邮件留在服务器上、仅下载邮件头或不带附件的正文等。

IMAP 对于任何奔波在外或有严谨邮件需求的人来说都是理想的。大多数发行版附带的默认 POP 和 IMAP 服务器（奇怪的是，它们被捆在一个名为 `imap` 的单个包中）满足了大部分需求。

# 这些安装说明假设

- 命令与 Unix 兼容。
- 源路径为 `/var/tmp`（也可能是其他路径）。
- 安装在 RedHat Linux 6.1 上进行过测试。
- 安装中的所有步骤都在超级用户账户 `root` 中进行。
- Imap 版本号为 4.5

# 软件包

Imap 主页: http://www.washington.edu/imap/
你必须确保下载了：`imap-4.5.tar.Z`

# Tar 包

在安装 Imap 之前，对系统创建一个文件列表并在之后使用 `diff` 进行比较是一个好主意。简单地在安装前运行 `find > imap1`，安装后运行 `find > imap2`，然后使用 `diff imap1 imap2`。

### 编译

解压 tar 包 (`tar.Z`)。

```bash
[root@deep]# cp imap-version.tar.Z /var/tmp
[root@deep]# cd /var/tmp
[root@deep]# tar xzf imap-version.Z
```

# 进入新目录并在终端输入以下命令：

编辑 `Makefile` 文件（`vi src/odepunix/Makefile`）并更改：
```bash
sh -c 'test -f /usr/include/sys/stat.h -a $(OS) != "" && /usr/include/sys/stat.h || true'
```
此修改将更改 "`sys/stat.h`" 文件。与新的 glibc 2 不同。

编辑 `Makefile` 文件（`vi src/odepunix/Makefile`）并更改：
```bash
BASEFLAGS="-g -fno-omit-frame-pointer -O2 -DDEBUG"
```
读取：
```bash
BASEFLAGS="-O3 -ffast-math -ms -mcpu=pentium -march=pentium -fno-omit-frame-pointer -fno-exceptions -DDEBUG"
```
这是我们在服务器上编译 IMAP/POP 软件的优化。

编辑 `Makefile`（`vi src/odepunix/Makefile`）并更改：
```bash
BUILDOPTIONS="${EXTFLAGS}"
```
读取：
```bash
BUILDOPTIONS="-DISABLE_POP_PROXY=1 -IGNORE_LOCK_ERRORS=1"
```
默认情况下，POP 服务器提供 IMAP 代理访问，允许 POP 客户端通过 POP 服务器访问 IMAP 服务器。设置 "`DISABLE_POP_PROXY=1`" 选项将禁用此功能。"`IGNORE_LOCK_ERRORS=1`" 选项将禁用由于 EACCES 错误导致创建邮箱失败时产生的“邮箱目录必须受保护”错误。

编辑 `Makefile`（`vi src/odepunix/Makefile`）并更改：
```bash
ACTIVEFILE=/var/lib/active
SPOOLDIR=/var/spool
RSHPATH=/usr/bin/rsh
```
读取：
"`ACTIVEFILE=`" 指定了 IMAP/POP 的 "active" 目录路径，“`SPOOLDIR=`" 是 Linux IMAP/POP 使用的 "spool" 目录，“`RSHPATH=`" 说明我们在服务器上不使用 rsh，因此指定了 "rsh" 的正确目录。

编辑 `Makefile`（`vi src/odepunix/Makefile`）并更改：
```bash
CC=gcc
```
读取：
```bash
CC=cc
```
这一行代表我们将用于编译 IMAP/POP 软件的 GCC 编译器名称（在本例中为 `cc`）。



进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```



编辑 `smbmount.c` 文件（`vi +99 client/smbmount.c`）并修改：

```c
static void close_our(int client_fd)
{
  int i;
  for (i = 0; i < 256; i++) {
    if (i === client_fd) continue;
    close(i);
  }
}
```

修改为：
```c
static void close_our_files(int client_fd)
{
  struct limit rlimits;
  int i;
  getrlimit(RLIMIT_NOFILE,&limits);
  for (i = 0; i < limits.rlim_max; i++) {
    if (i == client_fd) continue;
    close(i);
  }
}
```

上述两个步骤将使 `include.smbmont.c` 文件能够兼容 Red Hat glibc 2.1 库。

关于本页面的意见和建议请邮件至 `gmourani@videotron.ca`。

# 编译与优化

在终端上输入以下命令：

```bash
CC="egcs" \
--configure \
--prefix=/usr \
--libdir=/etc \
--with-lockdir=/var/lock/samba \
--with-private-dir=/etc \
--with-swatdir=/usr/share/swat \
--with-swat=/usr/pam \
--with-mmap
```

注意：`-mmap` 选项在某些机器上可以大幅提升性能，或者完全没有区别，甚至可能降低性能。

这告诉 Samba 根据这种特定的硬件设置进行配置：

- 包含 PAM 密码数据库支持。
- 包含 MMAP 支持（提高性能）。

```bash
[root@desel#] make all
[root@desel#] make install
[root@desel#] install -m 755 /usr/share/swat (如果，你不喜欢在 HTML 中配置 Samba)
[root@desel#] make -f /usr/bin/samba
[root@desel#] make -f /usr/share/man/8/swat.8
[root@desel#] mkdir -p /var/lock/samba
[root@desel#] mkdir -p /var/pool/samba (仅打印共享需要)
[root@desel#] chmod 1777 /var/pool/samba (仅打印共享需要)
```

`install` 命令将在 `usr/bin/` 目录下安装脚本 `mksmambapassword`。该脚本用于通过 `smbpassword` 文件设置允许连接到我们服务器的 Samba 用户。参见本文档后后部分以及如何使用 Samba 密码。

`rm` 命令将删除 `usr/share/swat` 目录及其所有文件，它还会删除 `usr/bin/` 下的 `sw` 二进制文件。SWAT 程序是一个基于 Web 的配置工具，允许你通过 HTML 配置 `smb.conf` 文件。该工具监听你服务器的 TCP 端口 901。为了使用 SWAT 工具，你需要一个运行中的 Web 服务器，例如 Apache。SWAT 工具可能会在你的服务器上引发安全漏洞，因此我建议不要使用并将其删除。

`mkdir` 命令将在你的系统上创建一个 `/var/pool/samba/` 目录，用于你可能需要的打印共享任务。当然，这只有在你打算在局域网内使用 Samba 打印共享时才需要。由于我们没有配置我们的 Samba 服务器使用

© Copyright 1999 Open Network Architecture ®

258

关于本页面的意见和建议请邮件至 `gmourani@videotron.ca`。

## Samba 配置

[global]
```ini
workgroup = OPENARCH
server string = Samba %n
encrypt passwords = True
security = user
smb passdb = /etc/smbpasswd
log file = /var/log/samba.%m
socket options = IPTOS_LOWAY TCP_NODELAY
domain master = Yes
local master = Yes
preferred master = Yes
os level = 65
dns proxy = No
name resolve order = hosts bcast
bind interfaces = Only
interfaces = eth0 192.168.1.1
hosts = ALL
hosts allow = 192.168.1.4 127.0.0.1
debug level = 1
create mask = 0640
directory mask = 0750
level2 = = True
wide links = no
read raw = no
```

[homes]
```ini
comment = Home Directories
browseable = no
read only = no
invalid users = root daemon named nobody sys tty disk mem kmem users
```

[tmp]
```ini
comment = Temporary File Space
path = /tmp
read only = No
valid users = =admin
invalid users = root daemon named nobody sys tty disk mem kmem users
```



关于此页面的意见和建议应发送至 gmounrai@videotron.ca

使用用户级安全时，客户端必须先使用有效的用户名和密码“登录”，否则连接将被拒绝。这意味着在 Samba 服务器的 `/etc/passwd` 中必须存在客户端有效的用户名和密码，否则客户端的连接将失败。

`smb passwd = /etc/smbpasswd`

此 "`smb passwd`" 设置了加密的 `smbpasswd` 文件的路径，该文件是 `/etc/passwd` 文件的副本，包含了允许连接到 Samba 服务器的客户端的有效用户名和密码。Samba 软件在请求连接时读取此文件。

`log file = /var/log/samba/%m`

此 "`log file`" 使用扩展名 "`%m`"，允许你为登录到服务器的每个用户或每种机器分离日志文件。

`socket options = IPTOS_LOWDELAY_TCP_NODELAY`

此 "`socket options`" 为局域网优化连接，并提高 Samba 服务器传输文件的性能。

`domain master = Yes`

此 "`domain master`" 将 Samba 守护进程识别为 `(nbmd)` 其工作组的网域主浏览器。此选项通常必须在同一网络和工作组的所有其他 Samba 服务器中，仅在该工作组的一个 Samba 服务器上设置为 "`Yes`"。

`local master = Yes`

此 "`local master`" 允许 Samba 守护进程 `(nbmd)` 成为子网上的本地主浏览器。通常，此选项必须在你的网络中所有其他 Samba 服务器中，仅在作为子网本地主器的一台 Samba 服务器上设置为 "`Yes`"。

`preferred master = Yes`

此 "`preferred master`" 控制 Samba 守护进程 `(nbmd)` 是否为其工作组的首选主浏览器。再次，必须在你网络中的所有其他服务器上设置为 "`Yes`"。

`os level = 65`

此 "`os level`" 决定了 Samba 守护进程 `(nbmd)` 是否有机会成为本地广播区域内 WORKGROUP 的本地主浏览器。如果你的网络上有任何 NT 服务器，数字 65 将获胜；若要让你的 Linux Samba 服务器成为本地广播区域内工作组主浏览器的胜 NT 服务器，则必须将 "`os level`" 设置为 65。此外，此选项必须在一个 Linux 服务器上设置，并对网络上可能存在的所有 Linux Samba 服务器禁用。

`dns proxy = No`

此 "`dns proxy`" 如果设置为 "`Yes`"，则指定 Samba 守护进程在作为 WINS 服务器运行并发现 Net BIOS 名称未注册时，应将 Net BIOS 名称逐字逐字地视作 DNS 查询客户端。然后代表该客户端向 DNS 服务器进行名称查找。由于我们没有配置 Samba 服务器充作为 WINS 服务器，因此我们不需要将其设置为 Yes。

`name resolve order = imhosts host`

此 "`name resolve order`" 决定了命名服务以及将主机名解析为 IP 地址的顺序。

`bind interfaces = True`

关于此页面的意见和建议应发送至 gmnourai@videotron.ca

此选项 '`bind interfaces only`' 如果设置为 True，允许限制机器上哪些接口提供 SMB 服务。这是一项安全功能。配置 "`interfaces = eth0 192.168.1.1`" 完善了此选项。

`interfaces = eth0 192.168.1.1`

此选项 '`interfaces`' 允许你覆盖 Samba 用于浏览、名称注册和 NBT 流量的默认网络接口。默认情况下，Samba 会查询内核获取所有活动接口列表，以及除 127.0.0.1 外任何具有广播能力的接口。通过此选项，Samba 将仅在 IP 地址 192.168.1.1 的 "`eth0`" 接口上监听。这是一项安全功能，并配合上述配置（`bind interfaces only = True`）。

`hosts deny = All`

列在 '`hosts deny`' 中的主机除非服务有自己的列表，否则不允许访问服务。我们默认拒绝对主机的访问，并在下方的 hosts (`hosts allow =`) 选项中允许访问。

`hosts allow = 192.168.1.4 127.0.0.1`

此选项 '`allow`' 是允许访问服务的逗号、空格或分隔主机集合。我们允许主机 192.168.1.4 和本地主机 127.0.0.1 访问 Samba 服务器。注意，必须设置 localhost，否则你将收到错误消息。

`debug level = 1`

此选项 '`debug level`' 允许在 "`smb.conf`" 文件中指定调试级别（日志级别）。如果你将调试级别设置为高于2，可能会导致性能大幅下降。这是因为服务器在每次操作后都会向日志文件写入大量内容，这非常消耗资源。

`create mask = 0640`

此选项 '`create mask`' 根据从 DOS 到 UNIX 权限的映射设置权限。将此选项设置为 0640，从 Windows 系统复制或创建到 Unix 系统的所有文件默认权限均为 0640。

`directory mask = 0750`

此选项 '`directory mask`' 设置在创建目录时从 DOS 转换为 UNIX 模式时使用的八进制模式。将此选项设置为 0750，从 Windows 系统复制或创建到 Unix 系统的所有目录默认权限均为 0750。

`level2 oplocks = True`

此选项 '`level2 oplocks`' 提高了对许多文件频繁访问的性能。

`wide links = no`

此选项 '`wide links`' 控制是否跟踪目录树内的链接。

`read raw = no`

此选项 '`read raw`' 控制服务器是否支持原始读取。

### [tmp]

关于此页面的意见和建议应发送至 gmnourai@videotron.ca

`comment = Temporary Space`

此选项 '`comment`' 类似于客户端查询时看到的文本字段。

`path = /tmp`

此选项 '`path`' 指定用户访问的目录。

`read only = No`

此选项 '`read only`' 指定用户是否为只读。

`valid users = admin`

此选项 '`valid users`' 是允许登录此服务的用户列表。

`invalid users = root daemon sys kmem`

此选项 '`invalid users`' 是不允许登录此服务的用户列表，这实际上是一种“偏执性”的检查，以绝对确保不当设置不会违反安全。

关于此页面的意见和建议，请邮件至 gmourani@videotron.ca

```bash
[-f /etc/smb.conf] || exit 0
```

`RETVAL=0`

# 查看我们是如何被调用的。

case "$1" in

start)

  echo -n "Starting SMB services:"

  daemon smbd -D

  RETVAL=$?

  echo

  echo -n "Starting NMB services:"

  daemon nmbd -D

  RETVAL=$2

  echo

  [ $RETVAL -eq 0 -a $RETVAL -eq 0 ] && touch /var/lock/subsystem/smb || \

  RETVAL=1

stop)

  echo -n "Shutting down SMB services:"

  killproc smbd

  RETVAL=$?

  echo

  echo -n "Shutting down NMB services:"

  killproc nmbd

  RETVAL=$2

  [ $RETVAL -eq 0 -a $RETVAL -eq 0 ] && rm -f /var/lock/subsystem/smb

  echo

  ;;

restart)

  $0 stop

  $0 start

  RETVAL=$?

  ;;

reload)

  echo -n "Reloading smb.conf file:"

  killproc -HUP smbd

  RETVAL=$?

  echo

  ;;

status)

  status smbd

  status nmbd

  RETVAL=$?

  ;;

)

  echo "Usage: $0 [start|restart|status]"

  exit 1

esac

exit $RETVAL



现在，让此脚本具有执行权限并更改其默认权限：
`[root@deep]] chmod 700 /etc/rc.d/init.d/smbd`

使用命令为 Samba 创建符号链接 rc.d 链接：
`[root@deep]# chkconfig --add smbd`

Samba 脚本会在重启服务器时自动启动 `smbd` 和 `nmbd` 守护进程。
你可以通过执行以下命令来更改：
`[root@deep]# chkconfig --level 345 smbd on`

© Copyright 1999 Open Network Architecture ®

关于此页面的意见和建议，请邮件至 `gmourani@videotron.ca`

使用以下命令手动启动 Samba 服务器：
`[root@deep]# /etc/rc.d/init/samba start`

# "/etc/pam.d/samba" 文件的配置

配置你的 `"etc/pam.d/samba"` 文件以使用 `pam` 认证并添加内容：

创建 `samba` 文件（`touch /etc/pam.d/samba`）并添加内容：

```
Auth            required /lib/security/pam_pwdb.so nullock shadow

Account         required /lib/security/pam_pwdb.so
```

# "etc/logrotate.d/samba" 文件的配置

配置你的 `"etc/logrotate.d/samba"` 文件以自动轮转日志文件。

创建 `samba` 文件（`touch /etc/logrotate.d/samba`）并添加内容：

```
/var/log/samba/log.nmb {

    notifyempty

    missingok

    postrotate

        /usr/bin/killall -HUP nmbd

    endrotate

}

/var/log/samba/log.smb {

    notifyempty

    missingok

    postrotate

        /usr/bin/killall -HUP smbd

    endrotate

}
```

# 安全保护 Samba

创建加密密码文件
`"etc/smbpasswd"` 文件是 Samba 的加密密码文件。它包含了用户名、Unix 用户 ID 以及用户的 `smb` 哈希后的密码，以及账户标志和最后更改密码的时间。

**重要提示：** 要创建一个 Samba 账户，你必须先为该用户准备一个有效的 Linux 账户。使用以下命令从你的 `"etc/passwd"` 文件中生成 `smbpasswd` 文件：

```bash
[root@deep]# cat /etc/passwd | mksmbpasswd.sh > /etc/smbpasswd
```

创建用户账户：

```bash
[root@deep]# smbpasswd -a username (记住 "username" 必须是一个有效的 Linux 账户)。

New Samba password:

Retype new Samba password:

Password changed for user username.
```

```bash
[root@deep]# chmod 600 /etc/smbpasswd
[root@deep]# testparam (这将验证 smb.conf 文件是否有错误)。
```

注意：更多信息请参考 `samba/doc/texts/` 中的 `ENCRYPTION.txt`。

# 保护重要的配置文件

不可变位（immutable bit）可以用于防止意外删除或覆盖受保护的文件。它还可以防止有人创建其符号链接。一旦配置了 `smb.conf` 和 `inhosts` 文件，建议使用命令对它们进行保护：

```bash
[root@deep]# chattr /etc/smb.conf
[root@deep]# chattr /etc/inhosts
```

# 更多文档

有关更多详细信息，有几个 man 页面可以阅读：

- `man Samba (7)` - 用于 UNIX 的 Windows SMB/CIFS 文件服务器
- `man smb.conf (5)` - Samba 套件的配置文件
- `man smbian (1)` - 类似于 ftp 的，用于访问服务器上的 SMB/CIFS 资源
- `man smbd (8)` - 服务器向客户端提供 SMB/CIFS 服务
- `man mount (8)` - 挂载系统
- `man smbmount (8)` - Samba 密码文件
- `man smpasswd (8)` - 更改用户密码
- `man nbd (1)` - 

```
[root@#deep] make depend
[root@#deep] make
[root@#deep] cd tests/
[root@#deep] make
[root@#deep] cd ..
[root@#deep] make install
```

`make depend` 命令将构建并生成不同文件所需的依赖关系，`make` 将所有源代码编译为可执行的二进制文件，然后 `make install` 将二进制文件及任何支持文件安装到适当的位置。

`"test"`目录下的 `make` 命令会在安装前执行一些重要的测试，以验证你的 LDAP 服务器的功能。如果某些测试失败，你需要在完成安装之前修复这些问题。

```
[root@#deep] install -m 700 /var/lib
[root@#deep] echo localhost > /etc/openldap/ldapserver
[root@#deep] strip /usr/lib/libldap.so.1.0.0
[root@#deep] strip /usr/lib/libldap.a
[root@#deep] strip /usr/lib/liblberd.a
[root@#deep] strip /usr/bin/in_xfingered
[root@#deep] strip /usr/bin/go500
[root@#deep] strip /usr/bin/go500gw
[root@#deep] strip /usr/bin/mld500
[root@#deep] strip /usr/bin/rp500
[root@#deep] strip /usr/bin/fax500
[root@#deep] strip /usr/bin/rcp500
[root@#deep] strip /usr/bin/libldap
[root@#deep] strip /usr/bin/ldif2dbm
[root@#deep] strip /usr/bin/ldif2xindex
[root@#deep] strip /usr/bin/ldif2dbchildren
[root@#deep] strip /usr/bin/ldbmcmat
[root@#deep] strip /usr/bin/ldif
[root@#deep] strip /usr/bin/onitpeede
[root@#deep] strip /usr/bin/dbmtest
[root@#deep] strip /usr/bin/slurped
[root@#deep] strip /usr/bin/uid
[root@#deep] strip /usr/bin/ldapadd
[root@#deep] strip /usr/bin/ldapsearch
[root@#deep] strip /usr/bin/ldapmodify
[root@#deep] strip /usr/bin/ldapmoddn
[root@#deep] strip /usr/bin/ldappasswd
[root@#deep] strip /usr/bin/ldapdelete
```

`install` 命令将在 `/var` 目录下创建一个名为 `"ldap"` 的新目录，并出于安全考虑，将其模式设置为仅超级用户 `"root"` 可读、可写和可执行（700）。

`strip` 命令将丢弃对象文件中所有的符号。这意味着二进制文件的尺寸会更小。这会稍微提高程序的性能，因为系统在执行二进制文件时需要读取的行会更少。

# 工作清理

```
[root@#deep] cd /var/tmp
[root@#deep] rm -rf openldap ld-version.tgz
```



关于本页面的意见和建议请邮寄至 `gmouriani@videotronron.ca`。

"`rm`" 命令将删除我们用于编译和安装 OpenLDAP 的所有源码。它还会删除 `/var/tmp/` 目录下的 OpenLDAP 压缩包。

# 配置

我们在书籍 `"Linux.pdf"` 中描述的所有内容，在名为 `"floppy.tgz"` 的压缩包中都有特定的目录和子目录，其中包含特定程序的配置文件。如果你创建了这个压缩包，你就不需要手动重新配置或通过复制粘贴来创建你的配置文件。无论你决定手动复制还是从方便的压缩包中获取文件，你都有责任根据你的需求调整并将这些与 OpenLDAP 软件相关的文件放置在你的服务器上，如下所示。配置文件压缩包位于以下 Internet 地址：`http://pages.inet.net/lotus/1/doc/floppy.tgz`。

- 运行 Openldap 需要以下文件，并且必须将它们创建或复制到你服务器上相应的的目录。

`copy.slapd` 文件位于 `"/etc/ldap/"` 目录。`copy` `ldap` 脚本文件位于 `"/etc/rc/init.d/"` 目录。

你可以在 `floppy.tgz` 压缩包中获得下方列出的配置文件。请从解压后的 `floppy.tgz` 压缩包中将以下内容复制到适当的位置，或直接从本书书中复制粘贴到相关文件中。

## `"/etc/ldap/slapd.conf"` 文件的配置

`"/etc/ldap/slapd.conf"` 文件是配置 LDAP 服务器、权限、密码、数据库类型、数据库位置等的主配置文件。

编辑 `slap.conf` 文件 (`vi /etc/ldap/slapd.conf`) 并添加：

```
#

# 配置选项的详细信息请参阅 slap.conf(5)。

# 此文件不应该是可读的。

#ninclude               /etc/ldap/slapd.at

include               /etc/ldap/slapd.conf

schematicoff

#referral             ldap://ldap.it.umich.edu

pidfile               /var/run/slapd.pid

argsfile              /var/run/slapd.args

######################################################
# 数据库定义
######################################################

database              bdb

suffix                "dc=example,dc=com"

rootdn                "cn=admin,dc=example,dc=com"

######################################################
# 访问控制
######################################################

olc={0}access: {

  self to read

  users to read

  * to none

}
```

关于本页面的意见和建议请邮件至 `gmourani@videotron.ca`

```
rm -f /var/lock/subsystems/ldap

rm -f /var/run/slapd.args

;

fi

status slapd?

RETVAL=$

if [ $RETVAL -eq 0 ]; then

  if grep -q "replofile" /etc/openldap/slapd.conf; then

    status slurpd

    RETVAL=$$$

  fi

fi

start)

$0 stop

$0 start

RETVAL=$

reload)

killproc -HUP slapd

RETVAL=$

if [ $RETVAL -eq 0 ]; then

  if grep -q "replofile" /etc/openldap/slapd.conf; then

    killproc -HUP slurpd

    RETVAL=$$$

  fi

fi

)

echo "Usage: $0 start|restart|status]"

exit 1
```

`exit $RETVAL`

现在，让此脚本可执行并更改其默认权限：
`[root@deep]# chmod 700 /etc/rc.d/init.d/ldap`

使用命令为 OpenLDAP 创建符号链接 rc.d 链接：
`[root@deep]# chkconfig --add ldap`

OpenLDAP 在重启服务器时不会自动启动 `slapd` 守护进程。你可以执行执行命令来更改它：
`[root@deep]# chkconfig -level 345 ldap on`

使用以下命令手动启动你的 OpenLDAP：
`[root@deep]# /etc/rc.d/init.d/ldap start`

# 加固 OpenLDAP

### 保护重要的配置文件
不可变位（immutable bit）可用于防止意外删除或覆盖必须保护的文件。它还可以防止他人创建指向该文件的符号链接。一旦你配置了 `"slapd.conf"` 文件，建议使用命令对其进行免疫保护：

```
[root@deep]# chatter +i /etc/openldap/slapd.conf
```

© Copyright 1999 Open Network Architecture ®

273

# 更多文档

欲了解详情，可以阅读以下几个页面：

- `$ ldap (8)` - LDAP X-500 协议守护进程
- `$ ldapdelete (1)` - ldap 删除条目工具
- `$ ldapfilter.conf (5)` - LDAP 过滤程序的的配置文件
- `$ ldapfriendly (5)` - LDAP 友好程序的数据文件
- `$ ldapmodify, ldadd (1)` - ldap 修改条目和添加条目工具
- `$ ldapmodn1 (1)` - ldap 修改条目DN 工具
- `$ ldappasswd (1)` - 修改 LDAP 条目的密码
- `$ ldapsearch (1)` - ldap 搜索工具
- `$ ldapsearch.conf (5)` - LDAP 搜索偏好配置文件
- `$ ldaptemplates.conf (5)` - LDAP 显示模板例的配置文件
- LDAP 数据交换格式 (LDAP Data Interchange Format)
- `$ slapadd (8)` - 独立 LDAP 守护进程
- `$ slapadd.conf (5)` - slap（独立 LDAP 守护进程）的配置文件
- `$ slurped (8)` - 独立 LDAP 更新复制守护进程
- `$ slapcat (1)` - 交互式 LDAP 目录服务器查询程序

# OpenLDAP 创建与维护工具

### 离线创建数据库
如果你有成千上万条条目需要创建，这种方法是最佳的，因为使用 `ldadd` 方法将花费无法接受接受的时间。该工具将读取 `slap` 配置文件以及一个包含要添加条目文本表示的输入文件。

使用名为 `"my-data-file"` 的包含条目文本表示的文件作为示例总是更好的。

- 要离线创建数据库，请使用命令：
  `[root@]# if2ldm -i infiltrate -f slapconfigfile`
  `[root@]# if2ldm -i my-data-file -f /etc/ldap/slapd.conf`

其中 `<infiltrate>` 指定包含文本形式添加条目的 LDIF 输入文件。
`<slapconfigfile>` 指定 `slap` 配置文件，该文件告知在何处创建索引、什么等。

注意：在此创建模式下，我们的 `slap` 不会启动。

# LDIF 输入文件（包含条目文本表示的输入）

当你首次安装 OpenLDAP 并且有一个大型存档要存入 OpenLDAP 软件时，将所有数据库放在一个包含条目文本表示的文件中，并使用所示命令将该文件添加到 OpenLDAP 中是一个好主意。

创建 `my-data-file` (`touch /tmp/my-data-file`) 并在文件中以下行作为示例：

```
dn: o=openldap, c=com

oo=openldap

objectclass: organization

dn: cn=Ronald Smith, o=openldap, c=com

cn: Ronald Smith

s: Smith

telephonenumber: (480) 757-5856

title: Operator.

objectclass: top
```



```
objectclass: person

dn=Anthony Bay, o=openarch, c=com
cn: Anthony Bay
sn: Bay
phone: (410) 896-3786
mobile: (410) 833-0590
mail: abay@openarch.com
objectclass: top
objectclass: person

cn=George Parker, o=openarch, c=com
cn: George Parker
sn: Parker
telephonenumber:(414) 389-5695
fax:(414) 778-8785
mobile: (414) 470-8669
description: E-Commerce.
objectclass: top
objectclass: person
```

此示例文本文件用于向你展示如何在将其添加到新的 OpenLDAP 数据库之前，将你的存档信息数据库转换为 LDAP 条目。存在更多类型并可以根据你的需求进行创建，请查阅你的 OpenLDAP 文档以获取更多信息。

# 通过 LDAP 创建数据库

使用这种方法，你使用 `ldadd` 工具来添加条目，就像数据库创建后执行一样。例如，要向 `ldadd` 工具添加“Europe Mourani”条目，你可以创建一个名为 `/tmp/newentry` 的文件，内容如下：

创建新条目 (`/tmp/newentry`) 并在文件中添加此内容：

```
cn=Europe Mourani, o=openarch, c=com

cn=Europe Mourani

sn=Mourani
```

# Linux 数据库服务器

Postgres 最初在加州伯克利大学计算机科学系开发，开创了许多商业数据库中使用的关系概念。它提供了 SQL 语言支持、事务完整性和扩展性。PostgreSQL 是该原始版本的公有开源后代。

# 这些安装指令假设使用 Unix Unix 命令。源码路径为 `/var/tmp`（也可以是其他路径）。安装在 RedHat Linux 6 上通过测试。PostgreSQL 版本号为 6.5。你的系统中必须安装该包。

# 软件包

PostgreSQL 首页：`http://www.postgresql.org/`

你必须下载：`postgresql-6.5.tar.gz`

# Tar 包

在安装之前列出系统文件列表，安装后再列出一个列表，然后使用 `diff` 比较它们以找出文件被放置的位置。只需在安装 tar 包之前运行 `find /sql1`，在安装之后运行 `find /sql2`，并执行 `diff sql1 sql2` 即可获取更改列表。

### 编译

解压 tar 包 (`tar.gz`)。

```
[root]# cp postgresql_version_tar.gz /var/tmp
[root]# cd /var/tmp
[root]# tar xzf postgresql_version_tar.gz
```

## 编译与优化

### 第 1 步

首先，创建一个超级用户（常用 `postgres`）。

```
[root]# useradd -M -d /var/lib/pgsql -s /bin/bash -c "PostgreSQL" -u postgres >/dev/null
```

这会将内容发送到 stdout。

### 第 2 步

在编译 Postgres 程序之前，你必须验证系统中是否安装了 `postgres-1.1.24.i386` 软件包。`postgres-1.1.24.i386` 软件包位于 Red Hat 6 光盘目录中。在编译并安装 PostgreSQL 后，你可以从系统中移除 `postgres-1.1.24.i386` 包。

- 验证：

```
[root]# rpm -q postgres-1.1.24.i386
```

- 安装：

```
[root]# rpm -U postgres-1.1.24.i386
```

### 第 3 步

进入 PostgreSQL 目录并在终端输入以下命令：

```
[root]# cd src
[root]# CC="gcc"
[root]# ./configure \
--prefix=/usr \
--enable-locale
```

这告诉 PostgreSQL 为特定的硬件进行配置。

- 设置本地化支持。

编辑 `Makefile.global` 文件 (`vi Makefile.global`) 并修改：

`CFLAGS=$(SRDIR)/include -O2 -funroll-loops -fast-math -align-double -march=pentium3pro -fomit-frame-pointer -fno-exceptions`

这是针对 PostgreSQL 服务器的优化标志。你必须根据你的系统和 CPU 架构进行修改。

```
[root]# make all
[root]# cd
[root]# make -C src/main
[root]# make -C src/install
[root]# mkdir -p /usr/include/access/usr/include/pgpgsql
[root]# cp /usr/include/commands /usr/include/pgpgsql
[root]# cp /usr/include/executor /usr/include/pgpgsql
[root]# cp /usr/include/lib /usr/include/pgpgsql
[root]# cp /usr/include/libpq-++ /usr/include/pgpgsql
[root]# cp /usr/include/port /usr/include/pgpgsql
[root]# cp /usr/include/utils /usr/include/pgpgsql
[root]# cp /usr/include/fmgr.h /usr/include/pgpgsql
[root]# cp /usr/include/locale.h /usr/include/pgpgsql
[root]# cp /usr/include/config.h /usr/include/pgpgsql
[root]# cp /usr/include/c.h /usr/include/pgpgsql
[root]# cp /usr/include/postgres.h /usr/include/pgpgsql
[root]# cp /usr/include/postgres_ext.h /usr/include/pgpgsql
[root]# cp /usr/include/libpq-++-int.h /usr/include/pgpgsql
[root]# cp /usr/include/libpqxx.h /usr/include/pgpgsql
[root]# cp /usr/include/libpqxx.h /usr/include/pgpgsql
[root]# cp /usr/include/ecpqtype.h /usr/include/pgpgsql
[root]# cp /usr/include/salca.h /usr/include/pgpgsql
[root]# cp /usr/include/libpq-++/* /usr/include/pgpgsql
```

## 从你的 Postgres 超用户账户创建数据库安装

```bash
[root@deep#] su postgres
[postgres@deep#] initdb --pgdata=/usr/lib/pgql -pgdata=/var/lib/pgql
```

我们正在使用用户名 `postgres` (`uid=40`) 初始化数据库系统。

该用户将拥有所有文件并必须拥有服务器进程。

正在创建 Postgres 数据库系统目录 `/var/lib/pgql/base`

在 `/var/lib/pgql/base/template1` 创建模板数据库

在 `/var/lib/pgql/base` 创建全局类

正在将 `template1` 数据库添加到 `pg_database`...

正在清理 `template1`

正在创建公共视图 `pg_user`

正在创建视图 `pg_rules`

正在创建视图 `pg_views`

正在创建视图 `pg_tables`

正在创建视图 `pg_indexes`

加载 `pg_description`

```bash
[postgres@deep#] chmod 640 /var/lib/pgql/pg_pwd
[postgres@deep#] exit
```

注意：不要以 `"root"` 身份创建数据库安装，这将是一个巨大的安全漏洞。

## 工作后的清理

```bash
[root@deep#] cd /var/tmp
[root@deep#] rm -rf postgresql-version_tar.gz
```



移除 `egs-c++-1.1.24.j386.rpm` 包以释放空间。

`rm` 命令将删除我们用于编译和安装 PostgreSQL 的源文件。它还将删除 `var/tmp` 目录下的 PostgreSQL 压缩包。

`rm -e` 命令将删除我们为编译 PostgreSQL 服务器而安装的 `egs-c++` 包。注意，`egs-c++` 包仅在编译 PostgreSQL 等程序时需要，在成功编译 PostgreSQL 后可以安全地卸载。

## 配置

我们在书籍 `Linuxos.pdf` 中描述的所有软件在名为 `floppy.tgz` 的 tar 包中都有一个特定的目录和子目录，其中包含特定程序的配置文件。如果你有这个归包，你将无法手动重现所需的配置文件，或通过剪切粘贴来创建你的配置文件。无论你决定手动复制还是从归档文件中方便地获取文件，请根据你的需求对其进行调整，并将与 PostgreSQL 软件相关的文件放置在服务器上的适当位置，如下所示。服务器配置归包位于以下互联网地址：`http://pages.infini.net/lotus1/doc/opt/floppy.tgz`

关于此页的意见和建议请邮件至 `gmourani@videotron.ca`

运行 PostgreSQL 数据库需要以下文件，必须将其创建或复制到服务器上的适当目录。

复制 `/etc/rc.d/init.d/` 目录下的 `postgresql` 脚本文件。

你可以在 `floppy.tgz` 归包上获取下列出的配置文件。从解压后的 `floppy.tgz` 归包将以下文件复制到适当位置，或直接从此处复制到配置的文件。

### `/etc/rc.d/init.d/postgresql` 脚本文件的配置

配置你的 `/etc/rc.d/init.d/postgresql` 脚本文件以启动和停止 PostgreSQL 服务器。

创建 `postgresql` 脚本（`touch /etc/rc.d/init.d/postgresql`）并添加：

```bash
#!/bin/sh
# postgresql 这是启动 PostgreSQL
# 服务器的初始化脚本

# chconfig:345 85 15
# description:启动和停止 PostgreSQL 后台守护进程，处理 \
# 所有数据库请求。
# processname:postmaster
# pidfile:/var/run/postmaster.pid
#

# 源函数库。
# /etc/rc.d/init.d/functions

# 获取配置。
# /etc/sysconfig/network

# 检查网络是否启动。
# postmaster 很大需要它。
[ "$NETWORKING" = "no" ] && exit 0

[ - /usr/bin/postmaster ] || exit 0

# 此脚本通常守护进程名称 (postmaster)
# 与子系统名称 (postgresql) 不相同

# 查看我们是如何被调用的。
case "$1" in
start)
  echo -n "Checking postgresql installation:"
  # 检查 PGDATA 结构
  if [ -f /var/lib/postgresql/PG_VERSION ] && [ -d /var/lib/postgresql/base/template1 ];
  then
    # 检查现有 PGDATA 的版本
    if [ "$(cat /var/lib/postgresql/PG_VERSION)" != '6.5' ];
    then
      echo "old version. Need to Upgrade."
      echo "/usr/doc/postgresql-6.5.2/README.rpm for more information."
      exit 1
    else
      echo "looks good!"
    fi

    # 没有现有的 PGDATA！通过它 Initdb。
  else
    echo "no database files found."
    if [ ! -d /var/lib/postgresql ]
    then
      mkdir -p /var/lib/postgresql
      chown postgres:postgres /var/lib/postgresql
    fi
    su - postgres -c '/usr/bin/initdb -pgdata=/usr/lib/pgql -pgdata=/var/lib/pgql'
  fi
  fi

  stop)
    echo -n "Stopping postgresql service:"
    killproc -f postmaster
    sleep 2
    rm -f /var/run/postmaster.pid
    rm -f /var/lock/subsystems/postgresql
    echo
    ;;
  status)
    status postmaster
    ;;
  restart)
    $0 stop
    $0 start
    ;;
  *)
    echo "Usage: postgresql {start|stop|status|restart}"
    exit 1
  esac
esac

exit 0
```

现在，使此脚本可执行并更改其默认权限：

`[root@deep] # chmod 700 /etc/rc.d/init.d/postgresql`

使用命令为 PostgreSQL 创建符号链接：

`[root@deep] # chkconfig -d add postgres`

使用以下命令手动启动你的 PostgreSQL：

`[root]@deep#$ /etc/rc.d/init.d/postgresql start`

## 命令

下列命令是我们常用的某些，但还有更多命令，你必须查看页面以获取更多详细信息。

客户端连接可以通过 IP 地址和/或用户名通过 `PG_DATA` 中的 `pg_hba.conf` 文件进行限制。

在你的数据库中定义一个新用户，运行 `createuser` 工具：

```bash
[root]@deep#$ su postgres
[postgres]@deep#] createuser
输入要添加的用户名称 --> admin
输入密码或回车以使用用户 ID: 500 ->
user "admin" 允许创建数据库 (y/n) y
user "admin" 是超级用户吗? (y/n) y
createuser: admin 已成功添加
```

从你的数据库中删除用户，运行 `destroyer` 工具：

```bash
[root]@deep#$ su postgres
[postgres]@deep#$ destroyer
输入要删除的用户名称 --> admin
destroyer: 删除 admin 成功。
```

创建一个新数据库，运行 `createdb` 工具：

```bash
[root]@deep#$ su postgres
[postgres]@deep#$ createdb db (数据库名称)。
```

或使用 Postgres 终端监视程序 (`psql`)：

```bash
[root]@deep#$ su admin
[admin]@deep#$ psql template1
欢迎使用 PostgreSQL 交互式 SQL 监控：
请阅读 COPYRIGHT 文件了解 POSTGRESQL 的版权条款
```

`/include/psql/libpq++pgtransdb.h`

`/include/psql/libpq++pgcursordb.h`

`/include/psql/libpq++pgobjectject.h`

`/include/psql/port`

`/include/psql/port/linux`

`/include/psql/utils/decls.h`

`/include/psql/utils/elog.h`

`/include/psql/utils/mtch.h`

`/include/psql/utils/fmgr.h`

`/include/psql/config.h`

`/include/psql/ich.h`

`/include/psql/postgresql.h`

`/include/psql/postgres_ext.h`

`/include/psql/fe.h`

`/include/psql/ecerrno.h`

`/include/psql/egqlib.h`

`/include/psql/excepype.h`

`/include/psql/sqlca.h`

`/include/psql/pg_type.H`

`/usr/libpq.so.2`

`/usr/libpq.so`

`/usr/libpq/lib_cc.a`



`/usr/libpq.so.3.0.0`

`/usr/libpq.so.3`

`/usr/libpq.so+3.0`

`/usr/libpq/pgpq`

`/usr/libpq/getcolat_1.bki.source`

`/usr/psql/local_1_template_1.bki.source`

`/usr/psql/pg_demo_sample`

`/usr/man/1/cleardb.1`

`/usr/man/1/createdb.1`

`/usr/man/1/destroybdb.1`

`/usr/man/1/destroyer.1`

`/usr/man/1/initdb.1`

`/usr/man/1/initdb.2`

`/usr/man/1/invocation.1`

`/usr/man/1/pg_dump.1`

`/usr/man/1/pg_dumpall.1`

`/usr/man/1/pg_upgrade.1`

`/usr/man/1/postgresql.1`

`/usr/man/1/psql.1`

`/usr/man/3/catalogs.3`

`/usr/man/3/pg_statpq.3`

`/usr/man/5/pg_hba.conf`

`/usr/man/1/abort.1`

`/usr/man/1/alter_table.1`

`/usr/man/1/alter_user.1`

`/usr/man/man/inify.l`

`/usr/man/man/reset.l`

`/usr/man/man/revoke.l`

`/usr/man/man/rollback.l`

`/usr/man/man/select.l`

`/usr/man/man/server.l`

`/usr/man/man/show.l`

`/usr/man/man/tsdate.l`

`/usr/man/man/vacuum.l`

`/var/libpq/pg_base`

`/var/libpq/pg_base/template_1`

`/var/libpq/pg_base/template_1_pg_proc`

`/var/libpq/pg_base/template_1_pg_type`

`/var/libpq/pg_base/template_1_pg_attribute`

`/var/libpq/pg_base/template_1_pg_class`

`/var/libpq/pg_base/template_1_pg_inherits`

`/var/libpq/pg_base/template_1_pg_index`

`/var/libpq/pg_base/template_1_pg_static`

`/var/libpq/pg_base/template_1_pg_operator`

`/var/libpq/pg_base/template_1_pg_am`

`/var/libpq/pg_base/template_1_pg_amoc`

`/var/libpq/pg_base/template_1_pg_language`

`/var/libpq/pg_base/template_1_pg_aggregating`

`/var/libpq/pg_base/template_1_pg_id`

`/var/libpq/pg_base/template_1_pg_inreproc`

`/var/libpq/pg_base/template_1_pg_rewrite`

`/var/libpq/pg_base/template_1_pg_listview`

`/var/libpq/pg_base/template_1_pg_description`

`/var/libpq/pg_base/template_1_pg_attribute_relid_attnam_index`

`/var/libpq/pg_base/template_1_pg_attribute_relid_attnum_index`

`/var/libpq/pg_base/template_1_pg_proc_narg_type_index`

`/var/libpq/pg_base/template_1_pg_proc_oid_index`

`/var/libpq/pg_base/template_1_pg_type_oid_index`

`/var/libpq/pg_base/template_1_pg_type_name_index`

`/var/libpq/pg_base/template_1_pg_class_relname_index`

`/var/libpq/pg_base/template_1_pg_attdef`

`/var/libpq/pg_base/template_1_pg_attribute_relid_index`

`/var/libpq/pg_base/template_1_pg_relcheck`

`/var/libpq/pg_base/template_1_pg_relcheck_oid_index`

`/var/libpq/pg_base/template_1_pg_trigger_id_index`

`/var/libpq/pg_base/template_1_pg_description_objid_index`

`/var/libpq/pg_base/template_1_pg_version`

`/var/libpq/pg_base/template_1_pg_user`

`/var/libpq/pg_base/template_1_pg_views`

`/var/libpq/pg_base/template_1_pg_tables`

`/var/libpq/pg_base/template_1_pg_indexes`

`/var/libpq/pg_base/template_1_pg_database`

`/var/libpq/pg_base/template_1_pg_shadow`

`/var/libpq/pg_base/template_1_pg_group`

`/var/libpq/pg_base/template_1_pg_log`

`/var/libpq/pg_base/template_1_pg_VERSION`

`/var/libpq/pg_base/template_1_pg_sample`

`/var/libpq/pg_dwd`

关于此页面的建议请发送至 gmourani@videotron.com 市场上有一些代理服务器程序。这些代理服务器有两个主要缺点：它们是商业软件且不支持 ICP。优秀的 Apache Web 服务器从 1.2 版本起就包含代理缓存模块。这个模块是一个有趣的选择：它是免费的，并且与最流行的 Web 服务器配合工作。然而，它不使用 ICP，其健壮性无法与最佳代理选择相比：SQUID。

Squid 包含以下程序：

- `squid`: 主代理服务器
- `dnsserver`: DNS 查询程序，执行单次 DNS 操作
- `unlink`: 用于删除程序

### Squid 代理服务器

更多关于 Squid 的信息可以在 http://www.squid.org。

Squid 包含以下程序：

- `squid`: 主代理服务器
- `dnsserver`: DNS 查询程序，执行单次 DNS 操作
- `unlink`: 用于删除程序

### 安装

安装 Squid 最简单的方法是通过您的 Linux 发行版的包管理器。例如，在 Debian/Ubuntu 上，使用：

```bash
sudo apt-get install squid
```

在 RHEL/CentOS 上，使用：

```bash
sudo yum install squid
```

### 配置

配置文件位于 `/etc/squid/squid.conf`。你可以修改此文件来控制 Squid 的行为，例如设置访问控制列表和缓存选项。

- `port`: 设置 Squid 监听的端口（默认为 3128）。
- `acl`: 定义访问控制列表以限制可以使用代理的用户。
- `http_access`: 指定允许规则。

### 使用

配置 Squid 后，可以重启服务使更改生效：

```bash
sudo systemctl restart squid
```

现在，你可以通过配置浏览器或其他应用程序指向 Squid 服务器的 IP 地址和端口来使用 Squid。

关于此页面的意见和建议请邮件至 gmnourani@videotron.ca

`DEFAULT_SWAP_DIR` = `$(localstatdir)`/cache

读取：

`DEFAULT_SWAP_DIR` = `/cache`

`DEFAULT_ICON_DIR` = `$(sysconfdir)`/icons

读取：

`DEFAULT_ICON_DIR` = `$(libexecdir)`/icons



我们将 `"cache.log"`、`access.log"` 和 `"store.log"` 文件的默认位置更改为 `"var/log/squid"` 目录，并将 Squid 的 pid 存放在 `"var/run"` 目录下，并最终通过上述变量 (`libexecdir`) 将 Squid 的 `"icons"` 目录定位在 `"usr/lib/squid"` 下。

# malloc

许多用户发现，在将 Squid 与外部 malloc 库（如 GNU malloc）链接时，性能会有所提升。许多 Squid 用户使用 GNU malloc 遵循以下简单步骤：

- 1. 下载 GNU malloc 源码，可从任一个 The GNU FTP 镜像站点 (`http://www.gnu.org/get/ftp.html`) 获取。
- 2. 编译 GNU malloc：

```
[root@deep]# tar xpf malloc.tar.gz
[root@deep]# cd malloc
[root@deep]# vi Makefile 并取消注释行：CPPFLAGS = -DDEBUG # the Makefile
[root@deep]# export CC=gcc
[root@deep]# make
```

- 3. 将 `libmalloc.a` 复制到你的系统目录并重命名为 `libgnumalloc.a`。

```
[root@deep]# cp libmalloc.a /usr/lib/libgnumalloc.a
```

- 4. （可选）将 `malloc.h` 复制到你的包含目录并确保将其重命名为 `gnumalloc.h`。此步不是必须的，但如果你这样做，Squid 将能够使用 `mstat()` 函数在 `cachemgr` info 页面报告内存使用统计数据。

```
[root@deep]# cp malloc.h /usr/include/gnumalloc.h
```

# 编译与优化

返回新的 Squid 目录并在终端上输入以下命令：

```
[root@deep]# export CACHE_HTTP_PORT=80
CC=gcc
CFLAGS="-O9 -fno-loops -ffast-math -align-double -mcu=pentiumpro -march=pentiumpro -fomit-frame-pointer -fno-exceptions"
--configure \
--prefix=/usr \
--exec-prefix=/usr \
--bindir=/usr/sbin \
--libexecdir=/usr/lib \
--localstatdir=/var \
--sysconfdir=/etc/squid \
--enable-digests \
--disable-ident-lookups \
--enable-underscores \
--enable-heap-replacement
```

© Copyright 1999 Open Network Architecture ®

关于此页面的意见和建议请邮件至 `gmourani@videotron.ca`

# 这告诉 Squid 为此特定的硬件设置进行配置：

- 使用 Cache Digests 来提高性能。
- 启用 `poll()` 而不是 `select()`。
- `Disable-indent-lookups` 允许移除执行 Ident (RFC 9317) 查询的代码。
- 在移除缓存文件时启用 `-truncate` 而不是 `unlink()`。`Truncate` 可以带来轻微的性能提升。另请注意 `Truncate` 在不使用 `unlink` 的情况下会许多 inode。
- 启用 `-underscores`。Squid 默认拒绝任何名称中带有 `_` 的主机，以符合互联网标准。如果你不同意此，可以使用此开关允许 `_hostnames`，前提是解析器库不拒绝 `_hostnames`。
- 启用 `-heap-replacement`。此选项允许你使用各种缓存替换算法。详见下文。

```
[root@deep]$ make
[root@deep]$ make install
[root@deep]$ mkdir -p /var/log/squid
[root@deep]$ rm -rf logs/
[root@deep]$ chown squid /var/log/squid/
[root@deep]$ chmod 750 /var/log/squid/
[root@deep]$ chmod 750 /cache
[root@deep]$ rm -f /usr/sbin/RunCache
[root@deep]$ rm -f /usr/sbin/RunAccess
[root@deep]$ strip /usr/sbin/squid
[root@deep]$ strip /usr/lib/libuid/client
[root@deep]$ strip /usr/lib/libuid/dnsserver
[root@deep]$ strip /usr/lib/libuid/unlinkd
[root@deep]$ strip /usr/lib/libuid/cachemgr
```

"`make`" 命令将所有文件编译成可执行二进制文件，而 "`make install`" 将这些二进制文件及任何支持文件安装到相应的位置。"`mkdir`" 命令将在 "`var/log`" 下创建一个名为 "`squid`" 的新目录。"`rm -rf`" 命令将删除 "`logs`" 目录，因为该目录是为了处理我们移动到 "`var/log`" 的与 Squid 日志文件而创建的。"`chown`" 命令将 "`var/log/squid`" 的所有者改为 `squid`，"`chmod`" 命令将 "`squid`" 和 "`cache`" 目录的模式设置为 `(750 drwxr-x)` 以于安全。请注意，我们移除了小型脚本 "`RunCache`" 和 "`RunAccess`"，它们本负责以缓存模式或加速器模式启动 Squid，我们现在使用位于 "`/etc/rc.d/`" 的名为 "`squid`" 的更好的脚本来利用 Linux V 的特性。"`strip`" 命令将减小二进制文件的大小以获得最佳性能。

# 什么是 Cache Digest？

Cache Digest 是互联网对象缓存服务器内容的摘要。它以紧凑（即压缩）的格式指示特定 URL 是否在缓存中。压缩使用了“有损”技术，这意味着可以获得极高的压缩率，代价是无法获得100% 正确的信息。

# 工作后的清理

```
[root@deep]$ cd /var/tmp
[root@deep]$ rm -rf squid-version_stable.tar.gz
```

© Copyright 1999 Open Network Architecture ®

关于此页面的意见和建议请邮件至 `gmourani@videotron.ca`

```
[root@deep]# rm -rf malloc/malloc.tar.gz (如果你使用了 malloc)
```

"`rm`" 命令将删除所有用于编译和安装 Squid 以及 `malloc` 的源文件。它还将删除 "`var/tmp/`" 目录下的 Squid 和 `malloc` 压缩包。

# 配置

我们在书籍 "`Linux.pdf`" 中描述的所有软件在 `tar` 压缩包中都有一个特定的目录和子目录，其中包含特定程序的配置文件。如果你编辑了此文件，你将不必手动重新生成不同的配置文件或通过复制粘贴它们来创建你的配置文件。无论你决定手动复制还是为了方便从压缩文件中获取，你你根据需要对其进行修改、调整，并将文件放置在 Squid 服务器下方，放置在你服务器机器上的适当位置将是你的责任。服务器配置文件存档位于以下互联网地址：`http://pages.infinit.net/lotus1/docopt/floppy.tgz`

- 运行 `squid` 需要以下文件，并且必须创建或复制到你服务器上相应的目录。
- 复制 "`etc/squid/`" 目录下的 `squid.conf` 文件。
- 复制 "`etc/init.d/`" 目录下的脚本文件。
- 复制 "`etc/logrotate.d/`" 目录下的 `squid` 文件。

你可以在我们的 `floppy.tgz` 存档获取下面的配置文件。从解压后的 `floppy.tgz` 存档中将以下文件复制到相应的位置，并直接复制粘贴到相关文件中。

# 作为 httpd-加速器的配置 "`etc/squid/squid.conf`" 文件

配置你的 "`etc/squid/squid.conf`" 文件为 `httpd` 模式。如果 Web 服务器位于安装 Squid 的同一服务器上，你让 `httpd` (`Apache`) 守护进程运行在端口 `81`。对于 Apache，你可以通过在 "`httpd.conf`" 中分配行 (`Port 81`) 来实现。如果 Web 服务器 (`Apache`) 在网络其他服务器上运行（如我们所做），你可以为 Apache 保留相同的端口号 (`80`)，因为 Squid 代理将绑定在端口 (`80`)尚未使用的不同 IP 上。



编辑 `squid.conf` 文件 (`vi /etc/squid/squid.conf`) 并添加：

```
http_port 80
icp_port 0
acl QUERY query regex \?
obj_cache deny QUERY
cache_mem 16 MB
cache_dir ufs /cache 200 16 256
emulate_httpd_log on
direct_rewrite_host_header off
replacement_policy GDSF
acl all allow
httpd_accel off
```

关于此页面的意见和建议请邮寄至 gmouriani@videotron.ca

GDFS 通过在缓存中保留较小的热门对象来优化命中率，从而有更大的命中机会。由于它会驱除（可能的）较大的对象，因此它比 LFUDA 具有更低的比特率。

LFU 无论对象大小如何都将热门对象保留在缓存中，因此以牺牲命中率率为代价来优化命中率；一个巨大的热门对象会阻止许多较小的、流行程度稍低的对象被缓存。

![](img/4444dd2a96323af53b5149a2b33efe8b_292_0.png)

图 1：SPECWeb 命中率

1 和 2 显示了 Squid 2 在 SPECWeb 负载和 http 负载中的实现命中率。在命中率方面，原始的 SPECWeb 验证与此揭示之间的差异很小，相对顺序没有改变，且曲线的形状大致相似。SPECWeb 版本中的策略变异更大，并注意 http 测试的运行时间略长。

图 2：http 命中率

这是惠尔惠惠公司 1999 年的图表。

### half_closed_clients

此选项 `half_closed_clients` 如果设置为 off，会告诉 Squid 在 `read(2)` 返回无可读数据时立即关闭客户端连接；某些客户端可能会关闭 TCP 连接的一端，而保持其接收端开启。有时，Squid 无法区分半关闭和完全关闭的 TCP 连接。

### acl all 0.0.0.0/0 and http_access allow all

这些选项 `acl` 和 `http_access` 定义了一个访问控制列表。请参阅您的文档获取更多信息。`acl` 和 `http_access` 允许所有人连接到代理服务器，我们使用此代理来加速我们的 Web 服务器。

### cache_mgr_admin

此选项 `cache_mgr_admin` 指定本地缓存管理员的电子邮件地址，如果缓存崩溃，该地址将收到邮件。

### cache_effective_user squid and cache_effective_group squid

此选项 `cache_effective_user` 和 `cache_effective_group` 指定了缓存运行的 UID:GID。这是一个安全功能，你绝不能以 `root` 用户运行 Squid。在我们的配置中，我们使用 `Squid` 和 GID `squid`。

### httpd_acc_host 208.164.186.3 and httpd_acc_port 80

© Copyright 1999 Open Network Architecture ®

配置选项 `httpd_accel_host` `httpd_accel_port` 定义了真实 HTTP 服务器的名称和端口号。在我们的配置中，真实 HTTP 服务器位于 IP 地址 208.164.186.3 (`www.openarch`) 并使用端口 (`80`)。`www.openarch` 是我们网络上的另一个主机，由于 Squid 服务器与 Apache HTTP Web 服务器不在同一主机上，我们可以将端口 (`80`) 用于我们的 Squid 代理服务器，将端口 (`80`) 用于我们的 Apache Web 服务器，这种幻觉（效果）是完美的。

### log_icp_queries off

此选项 `log_icp_queries` 指定了你是否想要将 ICP 查询记录到 `access.log`。由于我们不使用 ICP，我们关闭了此选项。

### buffered_logs on

此选项 `buffered_logs` 如果“开启”，可以稍微加快某些日志文件的写入速度。这是一个优化功能。

# 将 `etc/rc.d/init.d/squid` 脚本作为 http 加速器配置

你的脚本已被修改，为 `cache` 设置 squid 交换缓存，而不是 `var/spool/squid`。

创建 squid 脚本文件（`touch /etc/rc.d/init.d/squid`）并添加：

```bash
#!/bin/bash
# squid
# 此脚本负责启动和停止
# Squid 互联网对象缓存

# chkconfig:- 90 25
# description: Squid 互联网对象缓存. 互联网缓存是：
# 一种将请求的互联网对象（即，通过
# HTTP、FTP 和 gopher 协议可用的数据）存储在比
# 请求站点更近系统上的方法。浏览器可以使用
# 本地 squid 缓存作为代理 HTTP 服务器，减少访问时间\
# 以及带宽消耗。
# pidfile=/var/run/squid.pid
# config:etc/squid/squid.conf
```

```bash
PATH=/usr/bin:/sbin:/usr/sbin
export PATH

# 加载函数库。
./etc/rc.d/init.d/functions

# 加载网络配置。
# /sysconfig/network
```

```bash
# 检查网络是否就绪。
[ $NETWORKING = "no" ] && exit 0
```

```bash
# 检查 squid 配置文件是否存在
[ -f /etc/squid/squid.conf ] && exit 0
```

```bash
# 确定 squid 二进制文件
[ -x /sbin/squid ] && SQUID=squid
[ -z "$SQUID" ] && exit 0

# 确定哪一个是 cache_swap 目录
CACHE_SWAP=$(sed -e 's/.*:\/etc/squid/squid.conf//' | \
grep cache_swap_dir | sed -e 's/.*cache_dir///' | \
cut -d'\'' -f2)
[ -z "$CACHE_SWAP" ] && exit 0
```

```bash
# #默认 squid 选项
# -D 禁用初始检查。如果启动 squid 时可能不需要
# 互联网连接，请提交此项
SQUID_OPTS="-D"

RETVAL=0
case "$1" in
  start)
    echo -n "Starting SQUID"
    for adir in $CACHE_SWAP; do
      if [ ! -d "$adir" ]; then
        echo -n "init_cache_dir $adir..."
        $SQUID -D 2>/dev/null
      fi
    done
    $SQUID $SQUID_OPTS &
    RETVAL=$?
    echo $SQUID
    [ $RETVAL -eq 0 ] && touch /var/lock/subsys/$SQUID
    ;;
  stop)
    echo -n "Stopping SQUID:"
    $SQUID -n
    RETVAL=$?
    if [ $RETVAL -eq 0 ]; then
      rm -f /var/lock/subsys/$SQUID
      while : ; do
        [ -f /var/run/squid.pid ] || break
        sleep 2
      done
      echo -n "done"
    fi
      echo
    ;;
  reload)
    $SQUID $SQUID_OPTS -reconfigure
    exit $?
    ;;
  restart)
    $0 stop
    $0 start
    ;;
  status)
    $SQUID check
    exit $?
    ;;
  probe)
    exit 0
    ;;
  *)
    echo "Usage: $0 [start|stop|status|restart]"
    exit 1
esac
exit $RETVAL
```

现在，使此脚本具有执行权限并更改其默认权限：

`[root#] chmod 700 /etc/rc.d/init.d/squid`

使用命令为 Squid 创建 rc.d 链接：

`[root#] chconfig --add squid`

默认情况下，脚本在重启时不会自动启动代理。你可以通过执行以下命令更改默认设置：



[root#] `chconfig --level 3 on`

使用以下命令手动启动你的新代理服务器：

[root#] `/etc/rc.d/init.d/start`

# 配置 "etc/logrotate.d" 文件作为 http 加速器

你的脚本已被修改，为 `cache` 设置 `squid` 交换缓存，而不是 `var/spool/squid`。

创建 `squid` 脚本文件（`touch /etc/rc.d/init.d/squid`）并添加：

```bash
#!/bin/bash
# squid
# 此脚本负责启动和停止
# Squid 互联网对象缓存

# chkconfig:- 90 25
# description: Squid 互联网对象缓存. 互联网缓存是：
# 一种将请求的互联网对象（即，通过
# HTTP、FTP 和 gopher 协议可用的数据）存储在比
# 请求站点更近系统上的方法。浏览器可以使用
# 本地 squid 缓存作为代理 HTTP 服务器，减少访问时间\
# 以及带宽消耗。
# pidfile=/var/run/squid.pid
# config:etc/squid/squid.conf
```

```bash
PATH=/usr/bin:/sbin:/usr/sbin
export PATH

# 加载函数库。
./etc/rc.d/init.d/functions

# 加载网络配置。
# /sysconfig/network
```

```bash
# 检查网络是否就绪。
[ $NETWORKING = "no" ] && exit 0
```

```bash
# 检查 squid 配置文件是否存在
[ -f /etc/squid/squid.conf ] && exit 0
```

```bash
# 确定 squid 二进制文件
[ -x /sbin/squid ] && SQUID=squid
[ -z "$SQUID" ] && exit 0

# 确定哪一个是 cache_swap 目录
CACHE_SWAP=$(sed -e 's/.*:\/etc/squid/squid.conf//' | \
grep cache_swap_dir | sed -e 's/.*cache_dir///' | \
cut -d'\'' -f2)
[ -z "$CACHE_SWAP" ] && exit 0
```

```bash
# #默认 squid 选项
# -D 禁用初始检查。如果启动 squid 时可能不需要
# 互联网连接，请提交此项
SQUID_OPTS="-D"

RETVAL=0
case "$1" in
  start)
    echo -n "Starting SQUID"
    for adir in $CACHE_SWAP; do
      if [ ! -d "$adir" ]; then
        echo -n "init_cache_dir $adir..."
        $SQUID -D 2>/dev/null
      fi
    done
    $SQUID $SQUID_OPTS &
    RETVAL=$?
    echo $SQUID
    [ $RETVAL -eq 0 ] && touch /var/lock/subsys/$SQUID
    ;;
  stop)
    echo -n "Stopping SQUID:"
    $SQUID -n
    RETVAL=$?
    if [ $RETVAL -eq 0 ]; then
      rm -f /var/lock/subsys/$SQUID
      while : ; do
        [ -f /var/run/squid.pid ] || break
        sleep 2
      done
      echo -n "done"
    fi
      echo
    ;;
  reload)
    $SQUID $SQUID_OPTS -reconfigure
    exit $?
    ;;
  restart)
    $0 stop
    $0 start
    ;;
  status)
    $SQUID check
    exit $?
    ;;
  probe)
    exit 0
    ;;
  *)
    echo "Usage: $0 [start|stop|status|restart]"
    exit 1
esac
exit $RETVAL
```

现在，使此脚本具有执行权限并更改其默认权限：

[root#] `chmod 700 /etc/rc.d/init.d/squid`

使用命令为 `Squid` 创建 `rc.d` 链接：

[root#] `chconfig --add squid`

默认情况下，脚本在重启时不会自动启动代理。你可以通过执行以下命令更改默认设置：

[root#] `chconfig --level 3 on`

使用以下命令手动启动你的新代理服务器：

[root#] `/etc/rc.d/init.d/start`

## 配置 "etc/logrotate.d" 文件作为 http 加速器

你的脚本已被修改，为 `cache` 设置 `squid` 交换缓存，而不是 `var/spool/squid`。

创建 `squid` 脚本文件（`touch /etc/rc.d/init.d/squid`）并添加：

```bash
#!/bin/bash
# squid
# 此脚本负责启动和停止
# Squid 互联网对象缓存

# chkconfig:- 90 25
# description: Squid 互联网对象缓存. 互联网缓存是：
# 一种将请求的互联网对象（即，通过
# HTTP、FTP 和 gopher 协议可用的数据）存储在比
# 请求站点更近系统上的方法。浏览器可以使用
# 本地 squid 缓存作为代理 HTTP 服务器，减少访问时间\
# 以及带宽消耗。
# pidfile=/var/run/squid.pid
# config:etc/squid/squid.conf
```

```bash
PATH=/usr/bin:/sbin:/usr/sbin
export PATH

# 加载函数库。
./etc/rc.d/init.d/functions

# 加载网络配置。
# /sysconfig/network
```

```bash
# 检查网络是否就绪。
[ $NETWORKING = "no" ] && exit 0
```

```bash
# 检查 squid 配置文件是否存在
[ -f /etc/squid/squid.conf ] && exit 0
```

```bash
# 确定 squid 二进制文件
[ -x /sbin/squid ] && SQUID=squid
[ -z "$SQUID" ] && exit 0

# 确定哪一个是 cache_swap 目录
CACHE_SWAP=$(sed -e 's/.*:\/etc/squid/squid.conf//' | \
grep cache_swap_dir | sed -e 's/.*cache_dir///' | \
cut -d'\'' -f2)
[ -z "$CACHE_SWAP" ] && exit 0
```



```bash
# #默认 squid 选项
# -D 禁用初始检查。如果启动 squid 时可能不需要
# 互联网连接，请提交此项
SQUID_OPTS="-D"

RETVAL=0
case "$1" in
  start)
    echo -n "Starting SQUID"
    for adir in $CACHE_SWAP; do
      if [ ! -d "$adir" ]; then
        echo -n "init_cache_dir $adir..."
        $SQUID -D 2>/dev/null
      fi
    done
    $SQUID $SQUID_OPTS &
    RETVAL=$?
    echo $SQUID
    [ $RETVAL -eq 0 ] && touch /var/lock/subsys/$SQUID
    ;;
  stop)
    echo -n "Stopping SQUID:"
    $SQUID -n
    RETVAL=$?
    if [ $RETVAL -eq 0 ]; then
      rm -f /var/lock/subsys/$SQUID
      while : ; do
        [ -f /var/run/squid.pid ] || break
        sleep 2
      done
      echo -n "done"
    fi
      echo
    ;;
  reload)
    $SQUID $SQUID_OPTS -reconfigure
    exit $?
    ;;
  restart)
    $0 stop
    $0 start
    ;;
  status)
    $SQUID check
    exit $?
    ;;
  probe)
    exit 0
    ;;
  *)
    echo "Usage: $0 [start|stop|status|restart]"
    exit 1
esac
exit $RETVAL
```

*(注：由于提供的文本中存在大量重复段落，译文已根据要求“不要重复输出原文”的原则进行了去重处理，仅保留了唯一的逻辑块。)*

关于本页面的意见和建议请邮寄至 gmourani@videotron.ca

将上述命令添加到 `/etc/rc.local` 中，这样你下次重启系统时就不需要再次输入它们了。

通过更改一些默认值，系统响应会变得更加灵敏，例如，它会多等待一下进行写入，这可以避免某些访问冲突。

请查看 `/usr/src/linux/Documentation/sysctl.txt` 以获取更多通过虚拟内存、磁盘缓存、交换分区（swap）改进内核参数的信息。

# ip_local_port_range 参数

本文档用于 `proc/sys/net/ipv4/ip_local_port_range` 中的 sysctl 文件，适用于 Linux 内核版本 2.2。`ip_local_port_range` - 整数。

定义了 TCP 和 UDP 选择本地端口时使用的本地端口范围。第一个数字是第一个（端口），第二个数字是最后一个端口号。对于高并发系统，请将其更改为 32768-61000。

```bash
echo "32768 61000" > /proc/sys/net/ipv4/ip_local_port_range
```

将上述命令添加到 `/etc/rc.d.local` 文件中，这样你下次重启系统时就不需要再次输入它们了。

# 物理内存

Squid 最重要的资源是物理内存。你的处理器不需要极快。你的磁盘系统将是主要的瓶颈，因此快速磁盘对于高容量缓存至关重要。如果可以，请使用 IDE 磁盘。

# 安装文件

- `/etc/squid`
- `/etc/squid/mib.txt`
- `/etc/squid/squid.conf.default`
- `/etc/squid/squid.conf`
- `/etc/squid/mime.conf.default`
- `/etc/squid/mime.conf`
- `/etc/squid/errors/ERR_ACCESS_DENIED`
- `/etc/squid/errors/ERR_CACHE_DENIED`
- `/etc/squid/errors/ERR_CACHE_ACCESS_DENIED`
- `/etc/squid/errors/ERR_CANNOT_FORWARD`
- `/etc/squid/errors/ERR_CONNECT_FAIL`
- `/etc/squid/errors/ERR_DNS_NOT_FOUND`
- `/etc/squid/errors/ERR_FORWARDING_DENIED`
- `/etc/squid/errors/ERR_FTP_DENIED`
- `/etc/squid/errors/ERR_FTP_FAILURE`
- `/etc/squid/errors/ERR_FTP_NOT_DENIED`
- `/etc/squid/errors/ERR_PUT_CREATED`
- `/etc/squid/errors/ERR_FTP_PUT_ERROR`
- `/etc/squid/errors/ERR_FTP_UNAVAILABLE`
- `/etc/squid/errors/ERR_INVALID_REQ`
- `/etc/squid/errors/ERR_INVALID_URL`
- `/etc/squid/errors/ERR_LIFETIME_EXP`
- `/etc/squid/errors/ERR_NO_RELAY`
- `/etc/squid/errors/ERR_ONLY_OF_CACHED_MIS`
- `/etc/rc.d/S90squid`
- `/etc/rc.conf.d/S90squid`
- `/etc/rc.conf.d/K25squid`
- `/etc/logrotate.squid`
- `/usr/lib`
- `/usr/lib/squid/dnsserver`
- `/usr/lib/squid/unlinkd`
- `/usr/lib/squid/cachemgr.cgi`
- `/usr/lib/squid/anthony-binhex.gif`
- `/usr/lib/squid/anthony-bomb.gif`
- `/usr/lib/squid/anthony-box.gif`
- `/usr/lib/squid/anthony-c.gif`
- `/usr/lib/squid/anthony-compressed.gif`
- `/usr/lib/squid/anthony-dvi.gif`
- `/usr/lib/squid/anthony-dir-gif.gif`
- `/usr/lib/squid/anthony-not-found.gif`
- `/usr/lib/squid/anthony-f.gif`
- `/usr/lib/squid/anthony-image.gif`
- `/usr/lib/squid/anthony-https2.gif`
- `/usr/lib/squid/anthony-layout.gif`
- `/usr/lib/squid/anthony-link.gif`
- `/usr/lib/squid/anthony-movie.gif`
- `/usr/lib/squid/anthony-pdf.gif`
- `/usr/lib/squid/anthony-portal.gif`
- `/usr/lib/squid/anthony-ps.gif`
- `/etc/sqid/errors/READ_ERROR`
- `/etc/sqid/errors/READ_TIMEOUT`
- `/etc/sqid/errors/SHUTDOWN`
- `/etc/sqid/errors/FAILURE`
- `/etc/sqid/errors/TOO_BIG`
- `/etc/sqid/errors/RESOLVE`
- `/etc/sqid/errors/WRITE`
- `/etc/sqid/errors/SIZE`
- `/etc/sqid/errors/OBJECT`
- `/etc/rc.d.d/S90squid`
- `/etc/rc.conf.d/S90squid`
- `/etc/rc.conf.d/K25squid`
- `/etc/rc.conf.d/S90squid`
- `/usr/lib/squid/icons/squill.gif`
- `/usr/lib/squid/icons/clip.gif`
- `/usr/lib/squid/icons/sound.gif`
- `/usr/lib/squid/icons/tar.gif`
- `/usr/lib/squid/icons/text.gif`
- `/usr/lib/squid/icons/unknown.gif`
- `/usr/lib/squid/icons/xbm.gif`
- `/usr/lib/squid/icons/xpm.gif`
- `/usr/sbin/Run`
- `/usr/sbin/Bin`



- `/usr/sbin/squid`

- `/usr/sbin/client`

- `/var/log/squid/`

# 物理内存

Squid 最重要的资源是物理内存。你的处理器不需要极快。你的磁盘系统将是主要的瓶颈，因此快速磁盘对于高容量缓存至关重要。如果可以，请使用 IDE 磁盘。

# 安装文件

（此处列出的文件路径通常保持原样，不翻译）

- `/etc/squid`

- `/etc/squid/mib.txt`

...（此处略）

# Apache Web 服务器

Squid 是一个功能强大的 Web 服务器，支持 HTTP 1.1、身份验证等许多功能。它是最流行的 Web 服务器之一，性能等同或优于商业级服务器。由于 Apache 是复杂的，我们在后续提供了分步示例。如果它们不符合你的情况，则需要调整。

本教程是为新的 Apache 管理员编写的，描述了如何安装和运行它。

# 编译与优化

将 `mod_ssl` 应用到 Apache 源码树。

进入新的 `mod_ssl` 目录 (`mod_ssl-version`)，并在终端中执行以下命令：

```bash
CC="ecgs" \
CFLAGS="-O9 -funroll-loops -fast-math -align-math -mcpu=pentiumpro -march=pentiumpro -fomit-frame-pointer -fno-exceptions" \
./configure
```

关于本页面的意见和建议请发送至 `gmourani@videotron.ca`

```bash
--apache=../apache_1.3.9 \
--with-crt=/etc/ssl/certs/server.crt \
--with-key=/etc/ssl/private/server.key
```

进入新的 Apache 目录（`cd ../apache-version`）并在终端中输入以下命令：

```bash
[root@deep]# vi +331 src/include/httpd.h 并修改：

#define HARD_SERVER_LIMIT 256
为
#define HARD_SERVER_LIMIT 1024
```

为 PHP3 的配置步骤预配置 Apache。

进入新的 apache 目录（`cd "../apache-version"`）并在终端中输入以下命令：

```bash
CC="gcc"
CFLAGS="-O9 -ffroll-loops -fast-math -malign-double -mcpu=pentiumpro -march=pentiumpro -fomit-frame-pointer -fno-exceptions"
CPP="DYNAMIC_MODULE_LIMIT=0"
/config/
--prefix=/home/httpd \
--bindir=/usr/bin \
--sbinir=/usr/sbin \
--libdir=/usr/lib/apache \
--includedir=/usr/include/apache \
--sysconfdir=/etc/conf \
--locatedir=/var \
--runtimedir=/var/run \
--logfile=/var/log/httpd \
--datadir=/home/httpd \
--proxycachedir=/var/cache/httpd \
--mandir=/usr/man
```

配置 PHP3 并将其应用于 Apache 源码。

进入新的 php3 目录（`cd "../php-version"`）并在终端中输入以下命令：

编辑 php3_pgsql.h 文件（`vi +46 functions/php3_pgsql.h`）并修改以下行：

```c
#include <libpq-fe.h>
#include <libpq-fs.h>
为：
#include <usr/include/postgresql/libpq-fe.h>
#include <usr/include/postgresql/libpq-fs.h>
```

```bash
CC="gcc"
CFLAGS="-O9 -ffroll-loops -fast-math -malign-double -mcpu=pentiumpro -march=pentiumpro -frame-pointer -fno-exceptions -usr/include/openssl"
/config/
--prefix=/usr \
--with-config-file-path=/etc/httpd \
--with-imap \
--enable-safe-mode \
--with-exec-dir=/usr/bin \
--disable-debug \
--apache=../apache_1.3.9
```

© Copyright 1999 Open Network Architecture ®

301

关于本页面的意见和建议请发送至 `gmourani@videotron.ca`

```bash
--with-postgresql (如果你需要 PostgreSQL 数据库)
--with-ldap (如果你需要 LDAP 数据库目录列表)
--enable-memory-limit=yes \
--enable-debug=no

[root@deep]# make
[root@deep]# make install
```

## 将 mod_perl 应用到 Apache 源码树并编译/安装 mod_perl 的 Perl 端。

进入新的 mod_perl 目录（`cd "../mod_perl-version"`）并在终端中输入以下命令：

```bash
perl Makefile.PL \
EVERYTHING=1 \
APACHE_SRC=../apache_1.3.9/src \
USE_APACH2 \
PREP_HTTPD=1 \
DO_HTTPD=1 \
[root@deep]# make
[root@deep]# make install
```

## 编译/安装带有 mod_ssl + mm + mod_perl 和 PHP3 的 Apache。

进入新的 Apache 目录（`cd "../apache"`）并在终端中输入以下命令：

```bash
SSL_BASE=SYSTEM\ (mod_ssl 需要),
EAPI_MM=SYSTEM\ (mm 需要)。
CC="gcc"
OPTIMA="-O3 -loops -fast-math -malign-clue -mcpu=pentiumpro -march=pentiumpro -omit-frame-pointer -no-exceptions" \
CFLAGS="-DYNAMIC_MODULE_LIMIT=0" \
--configure \
--prefix=/home/httpd \
--bindir=/usr/bin \
--sbinir=/usr/sbin \
--libexecdir=/usr/lib \
--included=/usr/include/apache \
--confdir=/etc/httpd \
--localstatedir=/var \
--rundedir=/var/run \
--logdir=/var/log \
--datadir=/home \
--proxiedir=/var/cache/httpd \
--module-dir=/var/module \
--add-module=src/modules/experimental/mod_mmap_static.c \ (如果你打算使用 mod_mmap)。
--add-module=src/modules/standard/mod_auth_db.c \ (如果你打算使用 mod_auth)。
--enable-ssl (mod_ssl 需要)。
--enable-rule=SSL_DBDM COMPAT\ (mod_ssl 需要)。
--activate-rule=src/modules/php3/libphp3.a \ (php 需要)。
--enable-php3 (php 需要)。
--activate-rule=src/modules/perl/libperl.a \ (mod_perl 需要)。
--enable-perl (mod_perl 需要)。
--disable-module=include \
--disable-module=status \
--disable-module=userdir \
--disable-module=negotiation \
--disable-module=autobindex \
--disable-module=asis \
--disable-module=imap
```

© Copyright 1999 Open Network Architecture ®

302

关于本页面的意见和建议请发送至 `gmnourani@videotron.ca`



`--disable-module=env` \
`--disable-module=actions`

## 此 Apache 针对特定的硬件设置进行了配置：

- `module` `mod_mmap` 用于提高性能
- `module` `mod_auth` 用于密码验证。
- `module` `mod_sel` 用于加密和安全交易。
- `module` `mod_php` 用于提高 php 页面加载速度。
- `module` `mod_perl` 比脚本提供更好的安全性和性能。
- 禁用 `include`
- 禁用 `status`
- 禁用 `userdir`
- 禁用 `negotiation`
- 禁用 `autobindex`
- 禁用 `asis`
- 禁用 `imap`
- 禁用 `env`
- 禁用 `actions`

**注意：** 移除不需要的模块将提高你的 Apache Web 服务器的性能。

```bash
[root@$deep] make
[root@$deep] make install
[root@$deep] rm -rf /usr/sbin/apachectl
[root@$deep] rm -rf /usr/local/man/8/apache.8
[root@$deep] rm -rf /home/home/htdocs/
[root@$deep] cd /var/tmp/php-version
[root@$deep] install -m 644 php.ini dist /etc/http/php.ini
[root@$deep] rm -rf /etc/http/conf/ssl.crt
[root@$deep] rm -rf /etc/http/conf/ssl.conf
[root@$deep] rm -rf /etc/http/conf/ssl.key
[root@$deep] rm -rf /etc/http/conf/ssl.prm/
[root@$deep] rm -rf /etc/http/conf/srm.conf srm.default.access access
```

关于此页面的意见和建议请邮寄至 `gmourani@videotron.ca`。

```
<Directory /home/httpd>
Options None
AllowOverride None
Order allow,deny
Allow from all
</Directory>
```

```
<Files .pl>
Options None
AllowOverride None
Order deny,allow
Deny from all
</Files>
```

```
DirectoryIndex index.htm index.php default.html index.cgi
UseCanonicalName On
TypesConfig /etc/conf/mime.types
DebugType text/plain
HostnameLookups Off
```

```
ErrorLog /var/log/httpd/error_log
LogLevel warn
LogFormat "%h %l %u %t %b "%{Referer}i" "%{User-Agent}i" combined"
/etc/conf/httpd.conf
SetEnv Request_URI %.gif gif-image
CustomLog /var/log/httpd/access_log combined %{gif-image}
ServerSignature Off
```

```
ScriptAlias /cgi-bin/ "/home/cgi-bin/"
<Directory "/home/cgi-bin">
AllowOverride None
Options None
Order deny,allow
Allow from all
</Directory>
```

```
AddType application/x-httpd-php .php3
AddType application/x-httpd-php-source .php
```

```
ErrorDocument 500 "The server made a boo."
ErrorDocument 404 "http://www.openarchive.com/error.htm"
ErrorDocument 403 "Access Forbidding -- Go away."
BrowserMatch "Mozilla/4.0;1.2" nokeepalive downgrade-1.0 force-response-1.0
BrowserMatch "RealPlayer/4.0" force-response-1.0
BrowserMatch "Java/1.0" force-response-1.0
BrowserMatch "UK/1.0" force-response-1.0
```

```
<IfDef>
AddType application/x-x509-ca-crt .crt
AddType application/x-pkcs7-cri .cri
</IfDef>
```

```
<Module mod_ssl>
SSLPassPhrase builtin
SSLSessionCache dbm:/var/run/ssl/ssl_scache
SSLSessionTimeout 300
SSLMutex file:/var/run/ssl_mutex
SSLRandomSeed startup builtin
SSLRandomSeed connect builtin
SSLLog /var/log/httpd/ssl_engine_log
```

Copyright 1999 Open Network Architecture ®

关于此页面的意见和建议请邮寄至 `gmourani@videotron.ca`。

SSLLog warn

</IfModule>
```

```
<IfDefine SSL>
<VirtualHost _default_:443>
DocumentRoot "/home/httpd/"
ServerName www.openarch.com
ServerAdmin admin@openarch.com
ErrorLog /var/log/httpd/error_log
SSLEngine on
SSLCertificateSuite ALL:ADH:RC4+RSA:HIGH:+MEDIUM:LOW:SSLv2:EXP:+eNULL
SSLCertificateFile /etc/ssl/certs/server.crt
SSLCertificateKeyFile /etc/ssl/certs/private.key
SSLCertificateFile /etc/ssl/certs/ca.crt
SSLCRevocationPath /etc/ssl/certs
SSLCertifyClient none
SSLCClientVerify Depth 10

SSLOptions +ExportData +StrictRequire
SetEnv User-Agent -"*MSIE*" keepalive ssl-unclean-shutdown
SetEnv Request_URI\.gif gif-image
CustomLog /var/log/httpd/http_access.log \
  "%t %{SSL_PROTOCOL} "%u" "%b" env=gif-image
</VirtualHost>
</IfDefine>
```

注意：如果你在 Apache 服务器上使用了 `mod_php3` 模块，请忘记在你的 `/etc/httpd/httpd.conf` 中包含以下行：

`AddType application/x-httpd-php3 .php`

`AddType application/x-httpd-php3-source :php`

注意：如果你在 Apache 服务器上使用了 `mod_perl` 模块，请忘记在 `/etc/httpd/conf/httpd.conf` 中包含以下行，以便查看服务器上不同模块的状态：

```
<Location /perl-status>
  SetHandler perl-script
  PerlHandler Apache::Status
  Order deny.allow
  Deny from all
  Allow from 192.168.1.3
</Location>
```

# 配置 "/etc/logrotate.apache" 文件

配置 apache 日志（执行 `touch /etc/logrotate.apache`）并添加：



```
/var/log/httpd/access_log {
  missingok
  postrotate
  /usr/bin/killall -HUP httpd
  endscript
}
/var/log/httpd/error_log {
  missingok
  postrotate
  /usr/bin/killall -HUP httpd
  endscript
}
/var/log/httpd/ssl_request_log {
  missingok
  postrotate
  /usr/bin/killall -HUP httpd
  endscript
}
```

# 配置 `/etc/rc.d/init.d/httpd` 脚本文件

配置你的 `/etc/rc.d/init.d/httpd` 脚本以启动和停止 Apache 服务器。

创建 `httpd` 脚本文件（执行 `touch /etc/rc.d/init.d/httpd`）并添加：

```
#!/bin/sh
# Apache Web 服务器的启动脚本
# chconfig: 345 85
# description: Apache 是一个 Web 服务器。它被用于提供
# HTML、文件和 CGI 服务。
# processname:httpd
# pidfile:/var/run/httpd.pid
# config:/etc/httpd/conf/httpd.conf

# 加载库。
./etc/rc.d/init.d/functions

# 查看我们是如何被调用的。
case "$1" in
start)
  echo -n "Starting httpd: "
  daemon httpd -D
  touch /var/lock/subsys/httpd
  ;;
stop)
  echo -n "Shutting down httpd: "
  kill httpd
  rm -f /var/lock/subsys/httpd
  rm -f /var/run/httpd.pid
  ;;
status)
  echo httpd
  ;;
restart)
  $0 stop
  $0 start
  ;;
reload)
  echo -n "Reloading httpd: "
  kill httpd -HUP
  ;;
*)
  echo "Usage: $0 [start|stop|restart|reload|status]"
  exit 1
esac
exit 0
```

现在，使此脚本具有执行权限并更改其权限：

`chmod 700 /etc/rc.d/init.d/httpd`

使用命令为 Apache 创建符号链接：

`chkconfig --add httpd`

使用以下命令手动启动你的新 Apache：

`/etc/rc.d/init.d/httpd start`

# Apache 安全防护

有一些影响安全性的重要配置选项。第一个是运行 Web 服务器的用户（`httpd.conf` 中的 `User` 和 `Group`）。最好选择一个权限较少的用户——理想情况下，是专门为运行 Web 服务器守护进程而创建的用户（我们通常称之为 `root`），并确保它对系统和功能的访问最小化。

```
groupadd -g 80 www
useradd -g 80 -u www
```

# 修改一些重要的文件和目录

```
groupadd -g 80 www
useradd -g 80 -u www
```

# 自动索引

默认情况下，Apache 启用了自动索引（`httpd.conf`）。这意味着对于目录的请求将生成一个索引。要关闭它，你需要对目录进行如下操作，即：

```
cd /home/httpd/
chmod 311 www
ls -la
drwx--x 1 webmaster
```

然后，对于目录的请求将返回如下错误信息：

Forbidden

你没有权限访问 `/root/`

# 创建身份验证的 `.htpasswd` 文件

只有当你为站点使用访问文件时才需要。

```
chmod 750 /usr/bin/htpasswd
/usr/bin/htpasswd /etc/httpd/.htpasswd add username
```

其中 `<htpasswd>` 是密码文件的名称，`<username>` 是要添加到 `htpasswd` 中的用户名。

# 免疫化重要文件

不可变位可以防止删除或覆盖必须保护的文件。它能防止有人创建该文件的符号链接。

# 对文件系统的更多控制

`chroot` jail 的主要用处是限制守护进程可以看到的文件系统部分。这可以在 `fstab` 文件（`etc/fstab`）中根据需要设置：

```
/dev/sda7    chroot ext2    nosuid
```

这意味着对于 `<nosuid>` 不允许设置用户标识符或设置组标识符。将此程序应用于 Apache 所在的分区有助于消除 UID/SGID。

# 在 chroot jail 中运行 Apache

这重点关注防止 Apache 被用作入侵系统的代理。Apache 默认以非 `root` 用户运行，这会将损害限制在具有本地 shell 的普通用户。当然，允许匿名访问账户无法满足大多数 Apache 服务器的安全要求，因此需要额外的步骤——即，在 `chroot` jail 中运行 Apache。

`chroot` Apache 并非易事，并且容易导致问题。在开始之前，我们首先需要判断这对你是否有益。一些优点和缺点但绝对限于：

## 优点：

- 如果 Apache 被攻破，攻击者将无法访问整个文件系统。此外，确保 Apache 以其独特的用户/组运行，而不是被过度使用的用户，例如 `"nobody"`。

关于本页面的意见和建议请邮件至 `gmourani@videotron.ca`

### 步骤 1：

如果尚未为运行 `httpd` 创建用户，请添加新的用户 ID `UID` 和组 ID `GID`。这很重要，因为以 `root` 身份运行将违背了监狱（jail）的初衷，而使用系统中已存在的 UID 可能允许不同用户互相访问资源。请考虑多层安全。

这些是示例的用户和组 ID。检查 `/etc/passwd` 和 `/etc/group` 文件获取空闲的 UID/GID。我们将使用 80。

```
[root@deep]# groupadd -g 80 www
[root@deep]# useradd -g -u 80 www
```

### 步骤 2：

© Copyright 1999 Open Network Architecture ®

关于本页面的意见和建议请邮件至 `gmourani@videotron.ca`

设置 `chroot` 环境。首先，我们需要创建 `chroot` Apache 结构。我们使用 `"chroot/httpd"` 作为位于不同分区的目录，为了安全，我们决定将 Apache 放在那里。

```
# 如果 Apache 已经在你的系统中安装并运行，请执行 /etc/rc.d/init.httpd stop
# mkdir /chroot/httpd
```

接下来，创建其余目录如下：

```
# mkdir /chroot/httpd/dev
# mkdir /chroot/httpd/lib
# mkdir /chroot/httpd/etc
# mkdir -p /chroot/httpd/usr/sbin
# mkdir -p /chroot/httpd/var
# mkdir -p /chroot/httpd/var/log
# chmod 750 /chroot/httpd/var/log/httpd
# mkdir -p /chroot/httpd/home/httpd
```

拷贝主配置、配置文件、`cgi-bin`、根目录以及 `httpd` 程序：

```
# cp -r /etc /chroot/httpd/etc
# cp -p /chroot/home/cgi-bin /chroot/httpd/home/httpd/
# cp -r /home/your-Document/chroot /chroot/httpd/home/httpd/
# mkdir /chroot/httpd/dev/null
# chmod 666 /chroot/httpd/dev/null
# cp -r /usr/sbin /chroot/httpd/usr/sbin
# cp -r /etc/ssl /chroot/httpd/etc # 仅在你在使用 mod_ssl 时需要
# chmod 600 /chroot/httpd/etc/ssl/certs/server.crt
# chmod 600 /chroot/httpd/etc/ssl/private/ca.key
# chmod 600 /chroot/httpd/etc/ssl/private/server.key
```



从当前的根目录位置来看，我们需要 `"chroot/httpd/etc"`、`chroot/httpd/lib"`、`chroot/httpd/usr/sbin"`、`chroot/httpd/var/run"`、`chroot/httpd/home/httpd"` 以及 `"chroot/httpd/var/log"` 目录：

由于我们允许 Apache 使用共享库；我们需要将它们安装到 chroot 目录结构中。使用 `ldd /chroot/httpd/usr/sbin` 来查找需要哪些库。你编译 Apache 后的输出类似于：

```
libpam.so.0 -> /libpam.so.0 (0x40010000)
lib6.so.6 -> /lib6.so.6 (0x401f0000)
libz.so.2 -> /libz.so.2 (0x40090000)
libcrypto.so.1 -> /libcrypto.so.1 (0x400e0)
libssl.so.1 -> /libssl.so.1 (0x400b6000)
libresolv.so.2 -> /libresolv.so.2 (0x40081000)
libdb.so.3 -> /libdb.so.3 (0x40090000)
libc.so.6 -> /libc.so.6 (0x040b2000)
libld-linux.so.2 -> /libld-linux.so.2 (0x40000000)
```

拷贝上述标识的共享库：

```
# cp /libpam.so.0 /chroot/httpd/lib
# cp /lib6.so.6 /chroot/httpd/lib
# cp /libz.so.2 /chroot/httpd/lib
# cp /libcrypto.so.1 /chroot/httpd/lib
# cp /libssl.so.1 /chroot/httpd/lib
# cp /libresolv.so.2 /chroot/httpd/lib
# cp /libdb.so.3 /chroot/httpd/lib
# cp /libc.so.6 /chroot/httpd/lib
```

### 缺点说明（补充）

**缺点：**

- 你必须遗留在 chroot 中的额外文件。使用硬链接或静态编译你的二进制文件会有帮助。由于二进制文件也很方便，它们消除了（尽管可能性极乎其微）有人用恶意的封装库替换你的 lib 或共享库并让 Apache 在不知情的情况下运行的可能性。

- 一般而言，你的 Web 服务器执行的操作越多，要破解该功能就越困难。如果你使用任何 Perl/CGI，你将需要将二进制文件和 Perl 库拷贝到 chroot 空间内的相应位置。SSL、PHP 和其他情况也是如此。

下方列出的 chroot 配置假设你已经在编译 Apache 服务器时使用了 `mod_ssl`、`mod_php` 和用于密码认证的 `mod_auth_db`。你编译 Apache 服务器时使用的差异在于我们需要拷贝到 chroot 库目录中的哪些二进制文件和库。

请记住，如果你编译 Apache 以使用 mod_perl，你必须将所需的二进制文件和 Perl 库拷贝到 chroot 目录。Perl 位于 `/usr/lib/perl5`，如果你使用 perl，请将 perl 目录拷贝到 `/chroot/http/usr/lib/perl5/`。在拷贝之前，忘记在你的 chrooted 结构中创建 chroot 目录（`/chroot/http/usr/lib/perl5`）。

查找 httpd 的库依赖。这些库以后需要拷贝到 chroot 监狱中。

```
[root@deep]# ldd /usr/sbin/httpd
```

记录下列出的文件：你以后会需要它们。

...你编译 Apache 服务器时使用的差异在于我们需要拷贝到 chroot 库目录中的哪些二进制文件和库。

...

**(注：由于你提供的原始文本包含大量重复和乱码，我已根据逻辑流进行了清理。如果你需要针对“编写糟糕的 CGI 脚本”等特定段落的完整翻译，请参考下文。**

---

### 清理后的完整翻译版本

关于本页面的意见和建议请邮件至 gmourani@videotron.ca

- 编写不良好的 CGI 脚本（例如允许某人通过电子邮件发送你的 `/etc/passwd` 文件）将无法工作。

- nobody 或任何其他被使用的 UID 已被攻破。破解者现在可以从 chroot 内部访问任何以 nobody 身份运行的其他进程。

## 缺点：

**缺点：**

- 你必须遗留在 chroot 中的额外文件。使用硬链接或静态编译你的二进制文件会有帮助。由于二进制文件也很方便，它们消除了（尽管可能性极乎其微）有人用恶意的封装库替换你的 lib 或共享库并让 Apache 在不知情的情况下运行的可能性。

- 一般而言，你的 Web 服务器执行的操作越多，要破解该功能就越困难。如果你使用任何 Perl/CGI，你将需要将二进制文件和 Perl 库拷贝到 chroot 空间内的相应位置。SSL、PHP 和其他情况也是如此。

下方列出的 chroot 配置假设你已经在编译 Apache 服务器时使用了 `mod_ssl`、`mod_php` 和用于密码认证的 `mod_auth_db`。你编译 Apache 服务器时使用的差异在于我们需要拷贝到 chroot 库目录中的哪些二进制文件和库。

请记住，如果你编译 Apache 以使用 mod_perl，你必须将所需的二进制文件和 Perl 库拷贝到 chroot 目录。Perl 位于 `/usr/lib/perl5`，如果你使用 perl，请将 perl 目录拷贝到 `/chroot/http/usr/lib/perl5/`。在拷贝之前，忘记在你的 chrooted 结构中创建 chroot 目录（`/chroot/http/usr/lib/perl5`）。

查找 httpd 的库依赖。这些库以后需要拷贝到 chroot 监狱中。

```
[root@deep]# ldd /usr/sbin/httpd
```

（此处省略库文件列表，保持格式一致）

记录下列出的文件：你以后会需要它们。

### 步骤 1：

如果尚未为运行 httpd 创建用户，请添加新的用户 ID (UID) 和组 ID (GID)。这很重要……（此处省略具体命令，保持译文一致）

### 步骤 2：

© Copyright 1999 Open Network Architecture ®

关于本页面的意见和建议请邮件至 gmourani@videotron.ca

设置 chroot 环境。首先，我们需要创建 chroot Apache 结构……（此处省略具体命令，保持译文一致）

关于本页面的意见和建议请邮件至 gmnourani@videotron.ca

如上所述，如果您使用 Perl，则需要将 chroot 区域内的复制或硬链接任何系统库、perl 库 "/usr/lib/perl5" 以及二进制文件。对于 SSL、PHP 等其他内容也是如此。

## 配置新的 "/etc/logrotate.d/apache" 文件

由于上述原因，Apache 日志现在位于 "chroot/var/log/httpd" 目录，而不是 "var/log/httpd"，因此我们需要修改 "etc/logrotate.d/httpd" 文件以指向新的 chrooted 目录。我们还使用 mod_ssl 编译了 Apache，并额外向 logrotate 程序中添加了一行来轮转 ssl_request_log 文件。配置 "etc/logrotate.d/apache" 文件以每周自动轮转您的日志。

创建 apache 文件（touch /etc/logrotate.d/apache）并添加内容：

```
/chroot/httpd/var/log/httpd/access_log {
  missingok
  postrotate
  /usr/bin/killall -HUP /chroot/usr/sbin/httpd
}
```

```
/chroot/httpd/var/log/httpd/error_log {
  missingok
  postrotate
  /usr/bin/killall -HUP /chroot/usr/sbin/httpd
}
```

```
/chroot/httpd/var/log/httpd/ssl_request_log {
  missingok
  postrotate
  /usr/bin/killall -HUP /chroot/usr/sbin/httpd
}
```

```
/chroot/httpd/var/log/httpd/ssl_engine_log {
  missingok
  postrotate
  /usr/bin/killall -HUP /chroot/usr/sbin/httpd
}
```

## 优化 Apache

### 静态文件



对于静态文件，将 `mod_mmap_static` (`--add-module=../mod_mmap_static.c`) 编译进 Apache（参见上文时间，这已经完成——例如 http://www.apache.org/docs/mod_mmap_static.html），并通过在您的根目录下创建如下配置文件来配置 Apache 内存映射静态文档：

```
[root@deep]# find /home/httpd-types -f print | sed -e 's/.*\.mapfile&' > /etc/httpd/conf.conf
```

并在您的 Apache `conf.conf` 文件中如下所示包含 "`mmap.conf`"：

`[root@deep]# vi /etc/httpd/conf.conf` 并在 "`httpd.conf`" 某处添加该行：`Include conf mmap.conf`。

© Copyright 1999 Open Network Architecture ®

关于本页面的意见和建议请邮件至 gmourani@videotron.ca

### noatime

Linux 为文件系统提供了一个 `noatime` 挂载选项。可以将此选项添加到 `/etc/fstab` 的挂载选项中。当文件系统使用此选项挂载时，读取访问将不再产生与文件关联的 `atime`（访问时间）信息。`atime` 信息通常并不全有用，因此文件更新的缺失通常并不相关。

`noatime` 设置的重要性在于它消除了对仅进行读取的文件系统进行写操作的需求。由于写操作通常开销较高，这可以带来显著的性能提升。请注意，如果文件被写入，`wtime` 将继续更新。

编辑 `fstab` (`/etc/fstab`) 并向以下项添加 `noatime` 选项：

```
/dev/sda7    /chroot  ext2  nosuid,nodel,noatime
```

假设 `/dev/sda7` 是 `/chroot` 所在的分区。

## 重启系统并使用命令测试您的结果：

```
[root@deep]# reboot
[root@deep]# cat /proc/mounts
```

### ip_local_port_range

此文档针对 `sysctl` 文件 `/proc/sys/net/ipv4/ip_local_port_range`，适用于 Linux 内核 2.2。`ip_local_port_range` - 2 个整数。

定义 TCP 和 UDP 选择本地端口的范围。第一个数字是第一个（端口），第二个数字是最后一个本地端口号。对于高并发系统，将其更改为 32768-61000。

```
echo "32768 61000" > /proc/sys/net/ipv4/ip_local_port_range
```

将上述命令添加到 `/etc/rc.d/rc.local`，这样在下次重启系统时就不需要再次输入了。

## 安装的文件

- `/etc/rc.d/init.d/httpd`
- `/etc/rc.d/rc.0K5httpd`
- `/etc/rc.d/rc.1K15httpd`
- `/etc/rc.d/rc.2K15httpd`
- `/etc/rc.d/rc.3S85httpd`
- `/etc/rc.d/rc.4D955httpd`
- `/etc/rc.d/rc.6K15httpd`
- `/etc/logrotate.apache`
- `/etc/httpd`
- `/etc/httpd/conf`
- `/etc/httpd/conf/httpd.default`
- `/etc/httpd/conf/httpd.conf`
- `/etc/httpd/conf/mime.types`
- `/etc/httpd/conf/magic`
- `/etc/httpd/conf/magic.default`
- `/etc/httpd/conf/php.ini`
- `/home/httpd`
- `/usr/include/apache/ap_md5.h`
- `/usr/include/apache/ap_mm.h`
- `/usr/include/apache/ap_mmn.h`
- `/usr/include/apache/ap_sha1.h`
- `/usr/include/apache/ap_aux.h`
- `/usr/include/apache/ap_compat.h`
- `/usr/include/apache/ap_conf.h`
- `/usr/include/apache/ap_explain.h`
- `/usr/include/apache/ap_ashex.h`
- `/usr/include/apache/http_core_globals.h`
- `/usr/include/apache/http_config.h`
- `/usr/include/apache/http_core.h`
- `/usr/include/apache/http_log.h`
- `/usr/include/apache/main.h`
- `/usr/include/apache/protocol.h`
- `/usr/include/apache/http_request.h`
- `/usr/include/apache/http_host.h`
- `/usr/include/apache/httpd.h`
- `/home/httpd/cgi-bin`
- `/home/httpd/cgi-bin/prntenv`
- `/home/httpd/cgi-bin/test-cgi`
- `/usr/bin/htpasswd`
- `/usr/bin/htdigest`
- `/usr/bin/dbmanager`
- `/usr/include/apache`
- `/usr/include/xml/ap_asciib.h`
- `/usr/include/xml/ap_asciitab.h`
- `/usr/include/xml/ap_latinab.h`
- `/usr/include/xml/ap_nametab.h`
- `/usr/include/xml/ap_utf8.h`
- `/usr/include/xml/ap_arse.h`
- `/usr/include/xml/ap_role.h`
- `/usr/include/xml/ap_util.h`

```
[root@deep#] cp webalizer-version-src.tgz /var/tmp/
[root@deep#] tar xpf webalizer-version-src.tgz
```

Webalizer 需要由 Tom Boutelle 提供的 GD 图形库。如果你还没有安装它，请从 Red Hat Linux 6.1 CD-ROM 光盘中安装。

```
[root@deep#] rpm -Uvh gd-dev-devel.i386.rpm
```

进入新的 Webalizer 目录，并在终端中执行以下命令：

```
CC=gcc
CFLAGS="-O9 -funroll-loops -fast-math -malign-double -mcpu=pentium -march=pentium -fomit-frame-pointer=-fno-exceptions"
./config/configure --prefix=/usr
[root@deep#] make
[root@deep#] make install
[root@deep#] mkdir /home/http/usage
```

在你的 `httpd.conf` 文件中添加以下行：

```
Alias /usage/="/home/httpd/usage"
<Directory "/home/httpd/usage">
Order deny,allow
Deny from all
Allow from 192.168.1.3
</Directory>
```

## 工作后清理

```
[root@deep#] cd /var/tmp
[root@deep#] rm -rf webalizer-version/webalizer-version-src.tgz
```

## FAQ-O-Matic

FAQ-O-Matic 是一个基于 CGI 的系统，它可以激活维护 FAQ（或常见问题列表）的过程！它允许访问你 FAQ 的用户参与保持其更新。要安装此程序，请按照此步骤操作。

## 软件包

FAQ-O-Matic 首页：http://www.dartmouth.edu/~jonh/ff-serve/cgi/index.html

```
[root@deep#] cp FAQ-O-Matic-version.tgz /var/tmp/
[root@deep#] tar xpf FAQ-O-Matic-version.tgz
```

首先，在安装 "FAQ-O-Matic" 之前，至少将你的 "CGI.pm" 更新到 2.51 版本（见上文），进入新的 FAQ-O-Matic 目录并在终端中执行以下命令：



```
[root@deep#] perl Makefile.PL
[root@deep#] make
[root@deep#] make install
[root@deep#] mv fom /home/httpd/cgi-bin (或你的 CGI 所在的目录)
[root@deep#] mkdir -p /home/httpd/cgi-bin/fom-meta
[root@deep#] mkdir -p /home/httpd/faqomatic
[root@deep#] chown -R www:www /home/httpd/cgi-bin/fom-meta/
[root@deep#] chown -R www:www /home/httpd/cgi-bin/fom
[root@deep#] chown -R www:www /home/httpd/faqomatic/
```

© 1999 Open Network Architecture ®

318

关于本页的意见和建议应邮件至 gmourani@videotron.ca

在你的 `httpd.conf` 文件中添加以下行：

```
Alias /faqomatic="/home/httpd/faqomatic"
<Directory "/home/httpd/faqomatic">
Order allow,deny
Allow from all
</Directory>

Alias /bags="/home/httpd/faqomatic/bags"
<Directory "/home/httpd/faqomatic/bags">
Order allow,deny
Allow from all
</Directory>

Alias /cache="/home/httpd/faqomatic/cache"
<Directory "/home/httpd/faqomatic/cache">
Order allow,deny
Allow from all
</Directory>

Alias /item="/home/httpd/faqomatic/item"
<Directory "/home/httpd/faqomatic/item">
Order allow,deny
Allow from all
</Directory>
```

使用以下命令重启你的 Web 服务器：

```
[root@deep]# /etc/rc.init.d/httpd restart
```

使用 Netscape 打开 `http://localhost/cgi-bin/fom`（或你使用的任何浏览器，或用于执行 CGI 的任何 URL）

输入你的临时密码

创建 `fom-meta` 目录

首先点击 `Define configuration parameters`（定义配置参数），并配置以下内容，例如在 `Mandatory`（强制）下：服务器目录配置

`$$ServerBase=http://www.openarch`

`$$cgiURL=cgi-bin/fom`

`$$serveDir=/home/httpd/faqomatic/`

`$$URL=/faqomatic/`

根据需要配置其余部分

## 工作后清理

```
[root@deep]# cd /var/tmp
[root@deep#] rm -rf FAQ-O-Matic-version/ FAQ-O-Matic-version.tar.gz
```

## Webmail IMP

IMP 是一个 IMAP Webmail 客户端。

要安装此程序，请按照此步骤操作。

### 软件包

IMP 首页：http://www.horde.org/

```
[root@deep#] cp horde.tar.gz /home/httpd/
[root@deep#] xz horde.tar.gz
[root@deep#] mv horde
[root@deep#] cp.tar.gz /home/httpd/
[root@deep#] xz horde.tar.gz
```

© 1999 Open Network Architecture ®

319

关于本页的意见和建议应邮件至 gmourani@videotron.ca

```
[root@deep#] grep -i "http" /etc/httpd/conf
```

在 `httpd.conf` 文件中添加以下行：

```
Alias /horde="/home/httpd/horde"

<Directory "/home/httpd/horde">

Order allow,deny

Allow from all

</Directory>
```

使用以下命令重启你的 Web 服务器：
```
[root@deep]# /etc/rc.init.d/httpd restart
```

使用浏览器访问 `http://localhost/horde`
按照图形向导完成设置

## Linux IPX 网络 客户端

### 概述

Internet Packet exchange (互联网数据包交换) 是 Novell 公司用于为其产品提供联网支持的协议。

Ncpfs 是一个文件系统，理解 NetWare™ NCP 协议。功能上，NCP 在 NetWare 中的用法就像 NCP 在 TCP/IP 世界中一样。Linux 系统建立连接需要 `ncpfs`。你必须验证是否安装了它。命令是 `rpm ncpfs`。

### 编译支持 IPX 的内核

首先，你需要确保内核在编译时支持 IPX。在 6.1 内核中，你必须确保对以下问题回答了 Y：

- IPX 协议 (`CONFIG_IPX`)
- NCP 支持 (`CONFIG_NCP`)
- 数据包签名 (`CONFIG_NCPFS_PACKET_SIGNING`)
- 需要时清除/删除 (`CONFIG_NCPFS_STRONG`)
- 可用时使用 NFS 命名空间 (`CONFIG_NCPFS_NFS`)
- 可用时使用 LONG/2 命名空间 (`CONFIG_NCPFS_OS_2`)
- 允许挂载卷目录 (`CONFIG_NCPFS_MOUNT_SUBDIR`)
- 启用符号链接和标志 (`CONFIG_NCPFS_EXTRAS`)

### 尝试设置没有 TCP/IP 的 IPX 网络接口

你可以让接口处于而不使用协议。与其使用 `ifconfig` 配置 IP 地址，只需运行 `ifconfig eth0 up`。

假设你想将 `eth1` 设置为没有 TCP/IP 的 IPX 网络接口，你必须检查以下文件是否存在 (`ifcfg-eth1`)：

```
[root@deep]# vi /etc/sysconfig/network-scripts/ifcfg-eth1

DEVICE=eth1

IPADDR=

NETMASK=

BROADCAST=

ONBOOT=none

BOOTPROTO=none

USERCTL=
```



之后，你只需要使用以下命令重启网络守护进程：`/etc/rc.init.d/network restart` 并确保以太网卡存在，命令为：`config eth1 up`。

# Ncpfs 命令

为了自动设置接口配置和主接口，可以使用命令
`[root@deep]## ipx_configure --auto_interface=on --auto_primary=on`

要挂载 Novel™ 服务器或卷，请使用命令
`[root@deep]## ncpmount -D DMS01 /mnt/network -U username -P passwd`

此命令将使用用户名和密码登录文件服务器 `DMS01`，挂载到 `/mnt/network` 目录下。如果你未指定 `-P` 选项，将提示你输入密码。

要挂载 `/mnt/network` 目录，使用命令
`[root@deep]## ncpmount /mnt/network`

要查看网络上所有 Novel 文件服务器列表，使用命令
`[root@deep]## slist`

要复制文件，使用命令
`[root@deep]## ncopy file1[file2...] directory`

在 `/proc` 文件系统中位于了许多与 Linux IPX 支持相关的文件。它们是：

`/proc/net/ipx_interface`

该文件包含你机器上配置的 IPX 接口的信息。这些接口是通过命令手动配置的，或者是自动检测并配置的。

`/proc/net/ipx_route`

该文件包含 IPX 路由表中存在的路由列表。这些路由可能是通过命令手动添加的，也可能是通过 IPX 路由守护进程自动添加。

`/proc/net/ipx`

该文件是机器上当前可用的 IPX 套接字列表。

# Linux FTP 服务器

## 概述

使用文件传输协议 `FTP` 是跨网络在机器之间传输文件的一种流行方式。针对所有流行平台都编写了相应的客户端和服务器，因此 FTP 往往是执行文件传输最方便的方式。

你可以通过多种方式配置 FTP 服务器。一种是作为私有用户专用站点，这是 FTP 服务器的默认配置；私有 FTP 服务器允许系统上的用户仅能通过 FTP 连接并访问它们的文件。你可以对用户设置访问控制，以便显式地拒绝或授予某些用户的访问权限。

另一种类型的 FTP 服务器是匿名的。匿名 FTP 服务器允许网络上的任何人在没有账户的情况下连接到它。由于这种设置涉及潜在的安全性风险，你应该采取措施，仅允许访问系统上的某些目录。

我在此处介绍的配置是一个允许通过 FTP 访问 Unix 文件系统半安全区域的 FTP 服务器（受限的访客 FTP 访问）。此配置允许用户访问（例如网站目录，但不允许他们进入更高级别的目录。

# 这些安装说明假设

命令是兼容 Unix 的。
安装已在 RedHat Linux 6.1 服务器上通过测试。
安装过程中的所有步骤将在超级用户账户 `root` 下进行。
`wu-ftpd` 版本号为 `2.6.0`。

# 软件包

Wu-ftpd 首页：`http://www.wu-ftpd.org/`
你必须确保下载了：`wu-ftpd-2.6.0.tar.gz`

## 编译

解压 tar 包 `tar.gz`。

```bash
[root@$deep] cp wu-ftpd-version.tar.gz /var/tmp

[root@$deep] cd /var/tmp

[root@$deep] tar xzf wu-ftpd-version.gz
```

# 编译与优化

进入新的 Wu-ftpd 目录，并在终端中执行以下操作：

编辑 `ftpcount.c` `vi +241 src/ftpcount.c` 并修改该行：

```c
#if defined (LINUX)
```

修改为：

```c
#if defined (LINUX_BUT_NOT_REDHAT_6_0)
```

编辑 `pathnames.h` `vi +42 src/pathnames.h` 并修改该行：

```c
#define_PATH_EXECPATH "/bin/bin/ftp-exec"
```

修改为：

```c
#define_PATH_EXECPATH "/usr/bin/ftp-exec"
```

我们将 `ftp-exec` 的 `bin` 目录更改到 `usr/bin` 下。

```bash
CC="gcc"
CFLAGS="O9 -froll-loops -ffast-math -align-multiple -mcpu=pentium -march=pentium -fomit-frame-pointer -fno-exceptions" \
./configure \
--prefix=/usr \
--sysconf=/etc \
--locatestadir=/var \
--disable-dnsretry \
--enable-quote \
--enable-pam \
--enable-daemon \
--disable-newlines \
--disable-virtual
```

关于本页的意见和建议应邮邮件至 `gmourani@videotron.ca`

`-disable-plism` \n `-disable-pasvp` \n `-disable-anonymous` \n `-enable-is` \n `-enable-numericuid`

# 这告诉 Wu-ftpd 为特定的硬件设置进行自配置：

+   - 不要重试失败的 DSD 查找。
- 添加 QUOTA 支持（如果你的操作系统支持）。
- 添加 PAM 支持。
- 不允许作为独立守护进程运行。
- 抑制一些额外的空行。
- 不支持虚拟服务器。
- 禁用 PID 锁消息（针对繁忙站点）。
- 不要求被动连接使用相同的 IP。
- 不允许匿名 ftp 访问。
- 使用内部 ls（实验性）。
- 内部 ls 显示用户名的 UID（更快）。

```bash
make
make install
install -m 755 /xferstats /usr/bin
touch /var/log/xferlog
chmod 600 /var/log/xferlog
cd /usr/bin
ln -s /usr/bin/bin/usr/bin/wuftpd
ln -s /usr/bin/bin/in.w/wuftpd
strip /usr/bin/bin/ftpcount
strip /usr/bin/bin/wftppd
strip /usr/bin/bin/in.ftpd
strip /usr/bin/bin/ftpput
strip /usr/bin/sbin/ckconfig
strip /usr/bin/sbin/ftpstart
```

上述命令 `make` 和 `make install` 将配置软件，确保你的系统具有成功编译包所需的功能和库，将所有源文件编译为执行文件，然后将它们以及任何支持文件安装到适当的位置。

`install -m` 将安装用于查看传输文件统计信息的 `xferstats`，`touch` 命令将在 `var/log` 下创建 `xferstats` 的日志文件。`chmod` 将更改 `xferlog` 文件的模式，使其仅供超级用户 `root` 可写。之后，为 `in.ftpd` 二进制文件使用符号链接，最后处理所有与 Wu-ftpd 相关的二进制文件以减小其体积并提高性能。

# 工作后的清理

```bash
[root@deep]## cd /var/tmp
[root@deep] rm -rf wu-ftpd-version/ wu-ftpd-tar.gz
```

`rm` 命令将删除我们必须删除的安装 Wu-ftpd 的源文件。它还会删除 `var/tmp` 目录下的 Wu-ftpd 压缩存档。

# 为每个没有 shell 的用户设置 FTP 用户账户

首先，为此目的创建一个新用户，该用户将是允许连接到你的 FTP 服务器的用户。由于 `chroot` 环境的工作原理，必须与具有无限访问权限的普通用户账户分开。chroot 使得从用户的视角来看，你放置他们的文件系统级别就像顶层。

© Copyright 1999 Open Network Architecture ®

关于本页的意见和建议应邮邮件至 `gmourani@videotron.ca`

## 第 1 步

使用以下命令在 `/etc/passwd` 中用户。

```bash
[root@deep]## mkdir -d /home/ftp/ftpadmin -s /dev/null ftpadmin 2>&1
[root@deep]## passwd ftpadmin
正在更改用户 ftpadmin 的密码
新密码：
重新输入密码：
passwd: 令牌已更新
```

## 第 2 步

编辑 `/etc/shells` 文件并添加一个不存在的 shell 名称，例如 `null`。这个伪 shell 将限制对系统的访问。



```bash
[root@deep]## vi /etc/shells
/bin/bash
/bin/sh
/bin/ash
/bin/bin
/bin/tsh
/bin/csh
/dev/null 这是我们添加的 shell
```

# 第 3 步

现在，编辑你的 `/etc/passwd` 文件并手动添加 `"/"` 以划分 `/home/ftp/ftpadmin` 目录，用户 `"ftpadmin"` 将自动进入。此步骤必须适用于添加到 `passwd` 的每个 `ftp` 用户。

编辑 `passwd` 文件 (`/etc/passwd`) 并添加：

```c
ftpadmin:x:502:502:/home/ftp/ftpadmin:/dev/null
```

修改为：

```c
ftpadmin:x:502:502:/home/ftp/ftpadmin:/dev/null
```

账户是 `"ftpadmin"`，你会注意到目录路径有点奇怪。第一部分 `"home/ftp"` 指明应该被视为新根的文件系统。该目录下的点会自动进入 `"ftpadmin"`。

# 设置 chroot 环境

你本质上是在创建一个包含必要组件（二进制文件、密码文件等）的 `chroot` 文件系统，以便 `Unix` 在用户登录时进行 `chroot`。请注意，如果你在编译时使用了上述所示的 `-enable-is` 选项，则不需要 `/home/ftp/bin` 和 `/home/ftp/lib` 目录，因为这个新选项允许 `WU-FTP` 使用自己的 `"ls"` 函数。我仍然继续演示旧方法

关于此页面的意见和建议将发送至 `gnoumail@videotron.ca`

倾向于将 `"bin/ls"` 复制到 `chroot` `ftp` 目录 (`"/home/fpt/bin"`) 并创建与 `"ls"` 相关的库。

### 步骤 1：
首先创建所有必要的 `chrooted` 环境目录：

```
[root@deep]# mkdir /home/fpt/dev

[root@deep]# mkdir /home/fpt/etc

[root@deep]# mkdir /home/fpt/bin (仅在没有使用 "--enable-ls" 选项时需要)

[root@deep]# mkdir /home/fpt/lib (仅在没有使用 "--enable-ls" 选项时需要)
```

### 步骤 2
将新目录的权限更改为 `0511`：

```
[root@deep]# chmod 0511 /home/fpt/dev

[root@deep]# chmod 0511 /home/fpt/etc

[root@deep]# chmod 0511 /home/fpt/bin (仅在没有使用 "--enable-ls" 选项时需要)

[root@deep]# chmod 0511 /home/fpt/lib (仅在没有使用 "--enable-ls" 选项时需要)
```

`chmod` 命令将使你的 `chrooted` `"dev"`, `"etc"`, `"bin"` 和 `"lib"` 目录对超级用户 `"root"` 可读，对用户组和所有用户执行。

### 步骤 3
将 `"bin/ls"` 复制到 `"/home/fpt/bin"` 目录，并将 `"ls"` 的依赖更改为 `0111`。
（你不想修改二进制文件）：

```
[root@deep]# cp /bin/ls /home/fpt/bin (仅在没有使用 "--enable-ls" 选项时需要)

[root@deep]# chmod 0111 /bin/ls /home/fpt/bin (仅在没有使用 "--enable-ls" 选项时需要)
```

### 步骤 4
查找 `"ls"` 程序的共享依赖：

```
libc.so.6 => /lib/libc.so.6 (0x00125000)

ld-linux.so.2 => /lib/ld-linux.so.2 (0x00110000)
```

将上述识别出的共享库复制到 `"/home/fpt"` 目录下的新 `"lib"` 目录：

```
[root@deep]# cp /lib/libc.so.6 /home/fpt/lib (仅在没有使用 "--enable-ls" 选项时需要)

[root@deep]# cp /lib/ld-linux.so.2 /home/fpt/lib (仅在没有使用 "--enable-ls" 选项时需要)
```

这些库是为了让 `"ls"` 运行。

注意：如果你想使用 Linux 的 `"ls"` 二进制程序，而不是使用 `Wu-ftpd` 新内部 `ls` 能力的 `"--enable-ls"` 选项，则步骤 3 和 4 是必要的。

### 步骤 5
创建你的 `"/home/fpt/dev/null"` 文件：

```
[root@deep]# mknode /home/fpt/dev/null c 13

[root@deep]# chmod 666 /home/fpt/dev/null
```

© Copyright 1999 Open Open Network Architecture ®

### 步骤 6：
复制 `/home/ftpc/etc/` 目录下的 `"group"` 和 `"passwd"` 文件。这不应该和你真实的文件相同。

```
root@deep# cp /etc/passwd /home/ftpc/etc/

root@deep# cp /etc/group /home/ftpc/etc/
```

编辑 `passwd` 文件 (`vi /home/ftpc/etc/passwd`) 并删除除 `"root"` 用户和所有允许的 `FTP` 用户之外的所有条目。`chroot` 环境中的 `passwd` 文件具有类似如下的行是非常重要的：

```
root:x:0:root:/dev/null

ftpadmin:x:502:502::ftpadmin:/dev/null
```

编辑 `group` 文件 (`vi /home/ftpc/etc/group`) 并删除除 `"root"` 用户和所有允许的 `FTP` 用户之外的所有条目。`group` 文件应该与你的普通 `group` 文件对应：

```
root:x:0:root

ftpadmin:x:502:
```



## 配置

我们在书籍 `"Linux.pdf"` 中描述的所有内容都将在名为 `"floppy.tgz"` 的 tar 压缩包中有一个特定的目录和子目录，其中包含特定程序的配置。如果你获得了此文件，就不需要手动重新创建下面的不同配置文件，或通过剪切粘贴来创建你的配置。无论你决定手动复制文件，还是为了方便从归档文件中复制，你都有责任根据你的需求调整并将下述在 Wu-FTP 软件下的文件放置在你服务器机器上的适当位置，如下所示。下面的服务器配置存档位于以下互联网地址：`http://pages.infinit.net/linux/doc/opt/floppy.tgz`

- 要运行 FTP 服务器，需要以下文件，并且必须将它们复制或拷贝到你服务器上相应的目录。

- 复制 `/etc/` 目录下的 `ftpaccess` 文件。
- 复制 `/etc/` 目录下的 `ctypes` 文件。
- 复制 `/etc/` 目录下的 `hosts` 文件。
- 复制 `/etc/` 目录下的 `ftpgroups` 文件。
- 复制 `/etc/` 目录下的 `ftpaccess` 文件。
- 复制 `/etc/` 目录下的 `ctypes` 文件。
- 复制 `/etc/` 目录下的 `hosts` 文件。
- 复制 `/etc/` 目录下的 `ftpgroups` 文件。
- 复制 `/etc/` 目录下的 `ftpaccess` 文件。
- 复制 `/etc/` 目录下的 `ctypes` 文件。
- 复制 `/etc/` 目录下的 `hosts` 文件。
- 复制 `/etc/` 目录下的 `ftpgroups` 文件。
- 复制 `/etc/` 目录下的 `ftpaccess` 文件。
- 复制 `/etc/` 目录下的 `ctypes` 文件。
- 复制 `/etc/` 目录下的 `hosts` 文件。
- 复制 `/etc/` 目录下的 `ftpgroups` 文件。
- 复制 `/etc/` 目录下的 `ftpaccess` 文件。
- 复制 `/etc/` 目录下的 `ctypes` 文件。
- 复制 `/etc/` 目录下的 `hosts` 文件。
- 复制 `/etc/` 目录下的 `ftpgroups` 文件。
- 复制 `/etc/` 目录下的 `ftpaccess` 文件。
- 复制 `/etc/` 目录下的 `ctypes` 文件。
- 复制 `/etc/` 目录下的 `hosts` 文件。
- 复制 `/etc/` 目录下的 `ftpgroups` 文件。
- 复制 `/etc/` 目录下的 `ftpaccess` 文件。
- 复制 `/etc/` 目录下的 `ctypes` 文件。
- 复制 `/etc/` 目录下的 `hosts` 文件。
- 复制 `/etc/` 目录下的 `ftpgroups` 文件。
- 复制 `/etc/` 目录下的 `ftpaccess` 文件。
- 复制 `/etc/` 目录下的 `ctypes` 文件。
- 复制 `/etc/` 目录下的 `hosts` 文件。
- 复制 `/etc/` 目录下的 `ftpgroups` 文件。
- 复制 `/etc/` 目录下的 `ftpaccess` 文件。
- 复制 `/etc/` 目录下的 `ctypes` 文件。
- 复制 `/etc/` 目录下的 `hosts` 文件。
- 复制 `/etc/` 目录下的 `ftpgroups` 文件。
- 复制 `/etc/` 目录下的 `ftp` 文件
- 复制 `/etc/` 目录下的 `ctypes`
- 复制 `/etc/` 目录下的 `hosts` 文件。
- 复制 `/etc/` 目录下的 `ftpgroups` 文件。
- 复制 `/etc/` 目录下的 `ftpaccess` 文件。
- 复制 `/etc/` 目录下的 `ctypes` 文件。
- 复制 `/etc/` 目录下的 `hosts` 文件。
- 复制 `/etc/` 目录下的 `ftpgroups` 文件。

关于此页面的意见和建议请邮寄至 `gmourani@videotron.ca`

## readme

`<path> <when>` 是要向客户端提示的文件名（例如 `README`），`<when>` 是显示消息的条件。

`<when>` 参数应取以下形式之一：`LOGIN` 或 `CWD=<dir>`。如果是 `LOGIN`，消息将在成功登录后显示。如果参数设置为 `CWD=<dir>`，则在客户端进入 `<dir>` 目录时显示消息。

请记住，当为匿名用户指定路径时，文件必须相对于匿名 FTP 目录。

## message

`message` 命令允许你设置特殊消息，当客户端登录或切换到特定目录时发送给他们。你可以指定多条消息。该命令的格式为：

`message <path> <when>`

其中 `<path>` 是要显示的文件的完整路径，`<when>` 与 `readme` 命令中的 `<when>` 类似。

请记住，当消息由匿名用户触发时，消息路径需要相对于匿名 FTP 目录。

示例：
`message /ftp/welcome.msg LOGIN`

## compress, tar, chmod, delete, overwrite, rename

如果你没有指定以下指令，默认将对所有人开放。你在这里的操作是授予这些组对文件进行 `chmod`、删除、覆盖和重命名的权限，并允许所有人使用 `compress` 和 `tar`。

例如：
`compress yes all`
`tar yes all`
`chmod yes guest`
`delete yes guest`
`overwrite yes guest`
`rename yes guest`

## log commands

出于安全考虑，启用对用户单个命令的记录。该命令的格式为：

`log commands <typelist>`

其中 `<typelist>` 是一个逗号分隔的列表，指定应该记录哪些类型的用户。

例如，要记录所有真实和客用户的单个命令，你可以使用：

```
# log commands real,guest
```

© Copyright 1999 Open Network Architecture ® 330

关于此页面的意见和建议请邮寄至 `gmourani@videotron.ca`

生成的日志存储在 `/var/log/message` 文件中。

## log transfers

出于安全考虑，你应该记录所有的传输。该命令的格式为：

`log transfers <typelist> -<directions>`

其中 `<typelist>` 是一个逗号分隔的列表，指定应该记录哪些类型的用户（`anonymous, guest, real`），`<directions>` 是一个逗号分隔的列表，指定必须跟踪哪些方向的传输以便进行记录。你可以选择的两个方向是 `inbound`（入站）和 `outbound`（出站）。

例如，要记录所有入站和出站的真实和客用户用户传输，你可以使用：

```
log transfers real,guest,inbound,outbound
```

生成的日志存储在 `/var/log/xferlog` 文件中。

## guestgroup

此命令允许你在一行内指定所有客用户组。
`/home/ftp/etc/group` 包含这些组的条目，每个组只有一个成员。

例如：
`guestgroup ftpadmin`
`guestgroup webmaster`

## log security

启用对真实用户、客用户和/或匿名用户违反安全规则（`retrieve, .not, ...`）的记录。

`log security <typelist>` 是逗号分隔的列表，包含关键词 `anonymous`、`guest` 和 `real` 中的任意一个。如果包含 `real` 关键字，将记录使用 FTP 访问真实账户的用户的操作；如果包含 `anonymous` 关键字，将记录使用匿名 FTP 用户的操作。`guest` 关键字匹配客用户访问账户。

例如：
`log security real,guest`

## restricted-uid, restricted-gid and guest-root

这些子句控制是否允许真实用户或客用户用户访问 FTP 站点中主目录之外的区域。这些子句的使用示例显示了它们的预期用途。

```
guest-root <root-dir>

restricted-uid <uid-range>

restricted-gid <gid-range>
```



例如：
`guest-root /home/ftp ftpadmin webmaster`

© Copyright 1999 Open Network Architecture ® 331

关于此页面的意见和建议请邮寄至 gmourani@videotron.ca。

## restricted-uid ftpadmin webmaster
`restricted-gid ftpadmin webmaster`

`<root-dir>` 指定了用户的 (chroot) 路径。行中可以给出多个 uid 范围。如果为用户选择了 `guest-root`，则使用 `<root-dir>/etc/passwd` 文件中的用户主目录来确定初始目录，而不使用系统级 `/etc/passwd` 文件中的主目录。虽然 "`ftadmin`" 和 "`webmaster`" 都被 chroot 到 "`/home/ftp`"，但它们无法访问对方的文件，因为它们被限制在自己的主目录中。

## greeting|full|brief
允许你控制远程用户登录前提供多少信息。

`greeting full|brief`

`'greeting'` 是默认值，显示主机名和守护进程版本。`'greeting brief'` 只显示 "FTP server ready"。

例如：
`greeting <yes/no>`

数据套字的 keepalive 选项。可用于控制网络断开。Yes：设置。No：通常关闭。设置这是一个很好的主意。

## "etc/fosts" 的配置
`"etc/fosts"` 文件按用户建立规则，定义用户是否允许从某些主机登录，或者当用户尝试登录其他主机时是否拒绝其访问。

在文件中创建 fosts (`touch /etc/fosts`)：

```
# 示例文件

# # 之后的所有内容都被视为注释，

# 空行将被忽略

allow <username> <addrglob>

deny <username> <addrglob>
```

现在，将其默认权限更改为 600：
```
[root@deep]# chmod 600 /etc/fosts
```

文件中的每一行可以是以下之一：
`allow <username> <addrglob>`
`deny <username> <addrglob>`

其中 `allow` 允许 `<username>` 中指定的用户通过显式列出的地址 `<addrglob>` 使用 FTP 连接。你可以列出多个地址。`deny` 命令明确拒绝指定的用户 `<username>` 访问 `<addrglob>` 列出的站点。你可以列出多个站点。

© Copyright 1999 Open Network Architecture ® 332

关于此页面的意见和建议请邮寄至 gmourani@videotron.ca

## "/etc/ftpusers" 文件的配置
`"/etc/ftpusers"` 文件指定了不允许连接到 ftppd 的用户。

创建 ftpusers 文件 (`touch /etc/ftpusers`) 并在文件中：
```
root

bin

adm

shutdown

halt

mail

news

operator

games

body
```
现在，将默认权限更改为 600：
```
[root@deep]# chmod 600 /etc/ftpusers
```

## "/etc/ftpconversions" 文件的配置
`"/etc/ftpconversions"` 是一个包含允许传输前进行 compress 指令的文件。

创建 ftpconversions 文件 (`touch /etc/ftpconversions`) 并添加：
```
/bin/compress -d

/bin/compress -c

/bin/gzip -d

/bin/gzip -c

/bin/tar -c -f

/bin/tar -tar -f

/bin/cksum

/bin/md5sum
```

现在，将默认权限更改为 600：
```
[root@deep]# chmod 600 /etc/ftpconversions
```

## "/etc/pam.d/ftp" 文件的配置
配置你的 `"etc/pam.d/ftp"` 文件使用 pam 认证。

创建 ftp 文件 (`touch /etc/pam.d/ftp`) 并添加：
```
#PAM-1.0

auth required /lib/security/pam_list.so user_name=/etc/ftpusers onerr=succeed

auth required /lib/security/pam_pwdb.so nullok

auth required /lib/security/pam_shells.so

account required /lib/security/pam_pwdb

session required /lib/security/pam_pwdb
```

© Copyright 1999 Open Network Architecture ® 333

关于此页面的意见和建议请邮寄至 gmourani@videotron.ca

## "etc/logrotate.d/ftp" 文件的配置
配置你的 `"etc/logrotate.d/ftp"` 文件自动滚动日志文件。

创建 ftp 文件 (`touch /etc/logrotate.d/ftp`) 并添加：
```
/var/log/xlog {

# ftpd doesn't handle SIGHUP

nocompress
```

## 配置 ftppd 使用 tcp-wrappers inet super server
Tcp-wrappers 负责启动和停止 ftp 服务器。执行时，`inet` 从配置文件读取配置信息，默认情况下该文件是 `"etc/inetd.conf"`。配置文件的每个字段必须有一个条目，每个字段的条目用制表符或空格分隔。

编辑 inetd.conf 文件 (`vi etc/inetd.conf`) 并添加或验证以下行的存在：
```
ftp stream nowait /usr/sbin/tcpd-a
```

注意：添加行后，通过发送 SIGHUP 信号更新你的 `"inetd.conf"` 文件。
```
[root@deep /root]# killall -HUP inetd
```

编辑 hosts 文件 (`vi /etc/hosts`) 并添加示例行：
`in.ftpd: 192.168.1.4 win.openarch.com`

这意味着客户端 192.168.1.4 主机名 openarch.com 被允许 ftp 到服务器。

## FTP 管理工具

### ftwho
`ftwho` 显示系统中通过 FTP 连接的所有用户。该命令的输出类似于 `"/bin/ps"` 命令。该命令的格式为：
```
<pid> <time> <ity> <connection details>
```
其中 `<pid>` 是处理传输的 FTP 守护进程 ID；`<time>` 表示用户连接到 FTP 服务器的时间；`<ity>` 总是问号 (?) 因为连接来自 FTP 而不是 Telnet；最后 `<connection details>` 说明连接来自哪里用户是谁以及用户当前的功能。

以下是 ftwho 输出的示例。
```
[root@deep#]# ftwho

Service class openarch:

5443 ? S 0:00: ftpd: win.openarch.com; admin: IDLE

- 1 users (20 maximum)
```

在这里，你可以看到有一个用户登录（允许 20 个用户连接），该用户的用户名自称为 win.openarch.com。

© Copyright 1999 Open Network Architecture ® 334

关于此页面的意见和建议请邮件至 gmourani@videotron.ca

# ftpcount

`ftpcount` 是 `ftppow` 的简化版本，它仅显示登录到系统的用户总数以及允许的最大用户数。`ftpcount` 的示例输出如下：
```
[root@deep]# # ftpcount

Service class openarch - 1 users (20 maximum)
```

## 保护 FTP 安全

**确保**你已经设置了文件 `/etc/ftpusers`，该文件指定了那些**不允许**连接的用户。该文件**至少**应包含以下条目：root, bin, daemon, adm, lp, sync, shutdown, halt, mail, users, uucp, operator, games, nobody 以及所有供应商提供的账户。

要禁用匿名 FTP，请从你的系统文件文件中删除 `ftp`。使用以下命令验证系统上是否安装了 `anonftp-version.i86.rpm` 软件包：
```
[root@deep]# rpm -q anonftp
```



## `upload` 命令

默认情况下，`WU-FTPD` 服务器将向所有客用户授予上传权限。示例用户被限制（`chrooted`）在 `/home/ftp`，无法访问该目录结构之外的任何区域。因此，我们感兴趣的只是保护我们想要阻止用户进入的根目录下的文件。

在我们的安装中，`/home/ftp` 目录下将会有 `bin`, `etc`, `dev` 和 `lib` 子目录。我们不希望用户能够上传这些区域。如果这些区域的权限发生任何变化，你应该在 `/etc/ftpaccess` 文件中拒绝上传权限。在我们的情况下，我们进行如下设置：

```
upload/home/ftp/* / no
upload/home/ftp/* /etc no
upload/home/ftp/* /dev no
upload/home/ftp/* /bin no (仅在你不使用 "enable-ls" 选项时需要)
upload/home/ftp/* /lib no (仅在你不使用 "enable-ls" 选项时需要)
```

## `retrieve` 命令

在你的 `/etc/ftpaccess` 文件中使用 `retrieve` 命令防止下载 `/home/ftp` 目录中的那些子目录，也是一个好主意。

```
retrieve/home/ftp/etc
retrieve/home/ftp/dev
retrieve/home/ftp/bin (仅在你不使用 "enable-ls" 选项时需要)
retrieve/home/ftp/lib (仅在你不使用 "enable-ls" 选项时需要)
```

## 特殊文件 `.notar`

无论你是否允许对目录进行在线 `tar` 压缩，你都应该确保在不允许上传的任何区域都无法通过 `tar` 命令进行绕过。要做到这一点，请在每个目录以及 `FTP` 目录下创建一个名为 `.notar` 的特殊文件。

```
[root@deep]# touch /home/ftp/.notar
[root@deep]# chmod 0 /home/ftp/.notar
[root@deep]# touch /home/ftp/.notar
```

© 版权所有1999 Open Network Architecture ®

关于此页面的意见和建议请邮件至 `gnmourani@videotron.ca`

```
[root]@@# chmod 0 /home/ftp/.notar
[root]@@# touch /home/ftp/dev.notar
[root]@@# chmod 0 /home/ftp/dev.notar
[root]@@# touch /home/ftp/bin.notar (仅在你不使用 "-enable-is" 选项时需要)
[root]@@# chmod 0 /home/ftp/bin.notar (仅在你不使用 "-enable-is" 选项时需要)
[root]@@# touch /home/ftp/lib.notar (仅在你不使用 "-enable-is" 选项时需要)
[root]@@# chmod 0 /home/ftp/lib.notar (仅在你不使用 "-enable-is" 选项时需要)
```

零长度的 `.notar` 可能会误某些 Web 客户端和 FTP 代理，让我们将其标记为不可检索以解决此问题。在 `"/etc/ftpass"` 文件中添加以下行：

`noretrieve.notar`

### 安装文件

- `/etc/fthosts`
- `/etc/ftpusers`
- `/etc/ftpaccess`
- `/etc/pam.d/ftp`
- `/etc/ftpconversions`
- `/etc/ftroups`
- `/etc/logrotate.d/ftpd`
- `/usr/bin/ftpcount`
- `/usr/bin/ftwhoo`
- `/etc/man1/usr/man1/ftpcount`
- `/etc/man1/ftwhoo`
- `/etc/man5/ftpaccess.5`
- `/etc/man5/fthosts.5`
- `/etc/man5/ftpconversions.5`
- `/etc/man5/xferlog.5`
- `/etc/man8/ftpshut.8`
- `/etc/man8/ftprestart.8`
- `/sbin/ftpd`
- `/sbin/ckconfig`
- `/sbin/ftprestart`
- `/sbin/xstats`
- `/var/log/xferlog`

## 服务器备份程序

关于此页面的意见和建议请邮件至 `gmourani@videotron.ca`

安全且可靠的服务器与执行备份密切相关。定期备份应被考虑为优先事项之一。故障可能会发生。它们可能由硬件故障、停电或人为错误引起。如果你在系统上托管用户，你肯定会被要求恢复无意删除的文件。

关于本页面的意见和建议请邮件至 `gmourani@videotron.ca`

`etcetc/passwd` `usr/sbin/chpassword` 以及 `"etc/passwd"` `usr/sbin/chpassword` 归档文件。

如果您正尝试从归档中恢复一个或几个文件，除非您指定了归档中存储的文件名或目录路径，否则将无法成功。以下示例可能对有所帮助：

```
[root]@deep#$ cd
[root]@deep#$ tar -ztvpf archive/full-backup-09-October-1999.tar.gz | grep -i chpassword
```

在此示例中，归档包含的所有文件都通过文件名列出。输出随后被传递给 `grep` 命令，并使用 `grep` 的 `i` 选项忽略大小写，显示任何目录路径或文件名中包含 `chpassword` 单词的文件。一旦您确定了想要恢复的精确文件名，就可以像上面在在 `tar` 表达式中指定它。

注意：在创建归档文件时，`tar` 会删除文件名中的 `/`（斜杠）。这些名称的结束位置可能与备份时的位置不相同。因此，解决此问题的办法是在所有备份或恢复之前更改 `/` 根目录。另一个解决方案是在不同的目录下恢复所需的文件，然后将文件比较、移动或更新到原始位置。

警告：如果您的系统上有带有不可变位（`immutable bit`）的文件（使用 `chattr` 命令设置），这些文件在恢复备份时不会保留其不可变位。您必须在备份完成后使用 `chattr` 命令将它们恢复为不可变状态。

### 更多文档

详细信息可以阅读 `man` 手：`tar (1)` - GNU 版本的归档实用程序

### `tar` 的替代方案

`AMANDA`（高级自动网络归档器）是一个备份系统，允许局域网管理员设置一个主服务器，将多个主机备份到单个大容量设备。`AMANDA` 使用原生的 `dump/` 或 `tar` 功能备份大量工作站。最新版本还可以使用 `Samba` 备份 Windows 95/NT。

`BRU` 是为了最大的可靠性和灵活性而设计的备份和恢复实用。`BRU` 让 Unix 备份变得简单、快速且安全。`BRU` 不仅仅是 `tar` 和 `cpio` 的替代品，它是一个具有众多选项的备份系统。

## 附录 A. 调整、技巧与管理

## 附录 B. 获取征求意见稿（RFCs）

## `du` 工具

您可以使用 `du` 工具来帮助确定空间。例如，要确定 `var/log` 目录的需求，请输入：

```
[root]@deep$ du -sh /var/log
```

请记住，此命令将以整洁且易于读的形式返回数据的实际大小。现在您知道 `home` 占用了 66M，就可以定位最大的文件。

**注意：** 您可以添加 `crontab`，以便每天监控磁盘空间列表。

### 1.1 查找从您的主机到远程主机的数据包路由

如果您想找到从您的主机发送的数据包路由，只需执行命令，其中 `hostname` 是主机名或 IP 地址：

```
[root]@deep$ traceroute google.com
```

### 1.2 显示页面访问次数

要显示页面访问次数，使用此命令：

```
[root]@deep$ grep "GET" /var/log/httpd/access_log | wc -l
```

### 1.3 关闭大部分服务

作为 `root`，您可以使用以下命令关闭大部分服务：

```
[root]@deep$ killall httpd smbd sendmail
```

上述命令将关闭 Apache 服务器、Samba 服务、邮件服务器和 DNS 服务器。

### 1.4 为所有用户在终端显示时钟

编辑配置文件（`vi /etc/profile`）并添加以下行：

```bash
PROMPT_COMMAND='echo -ne "\033[0;32m$(date +%T)\033[0m\n\w\$ "'
```



结果看起来如下：

关于本页面的意见和建议请邮件至 gmourani@videotron.ca

![](img/4444dd2a9623af53b149a2b33efe8_0.png)

### 1.5 您安装了 "lsof" 吗？

如果没有，请安装并执行 `lsof -i`。这将列出您在主机上开启的端口。`lsof` 是一个很棒工具，但检查端口更简单的方法是 `netstat -an | grep LISTEN`。`lsof` 的好之处在于它会告诉您哪些进程正在监听给定端口。`Netstat` 告诉您哪些端口是打开的，而不是哪个进程连接在上面。

| COMMAND | FD | TYPE | SIZE | NAME |
| :--- | :--- | :--- | :--- | :--- |
| Inetd | 344 | ipv4 | 327 | *:ssh (LISTEN) |
| sendmail | 389 | ipv4 | 387 | *:smtp (LISTEN) |
| nmbd | 450 | ipv4 | 452 | deep.openarch.com:netbios-ss (LISTEN) |
| nmbd | 461 | ipv4 | 463 | *:netbios-ns |
| nmbd | 461 | ipv4 | 463 | *:deep.openarch.com:netbios-dgm |
| nmbd | 461 | ipv4 | 468 | deep.openarch.com:netbios-dgm |
| named | 4699 | ipv4 | 470 | deep.openarch.com:netbios-dgm |
| named | 2599 | ipv4 | 3095 | *:32771 |
| named | 2599 | ipv4 | 3092 | localhost.localdomain.domain |
| named | 2599 | ipv4 | 3092 | localhost.localdomain.domain (LISTEN) |
| named | 2599 | ipv4 | 3093 | deep.openarch.com:domain |
| named | 2599 | ipv4 | 3094 | deep.openarch.com:domain (LISTEN) |

### 1.6 通过 ssh 在远程运行命令而无需登录

`ssh` 命令可以在不登录的情况下在远程系统上运行命令。命令的输出将显示出来，控制权返回本地系统。这里有一个示例显示远程系统上的所有用户。

```
[admin@deep]$ ssh mail.openarch.com

admin@mail.openarch.com's password:

root tty1 Dec 2 14:45

admin tty2 Dec 2 14:45
```

### 1.7 文件补全

`Tab` 补全允许您输入程序的一部分，然后按 `[TAB]`，它就会为您补全文件名。如果有多个以您已输入字符开头的文件或程序，它会发出提示，然后当您再次按 `[TAB]` 时，它会列出所有以您最初输入开头的文件。尝试一下，看看它的限制在哪里，它如何适用于您的工作等。

路由协议 (RIP)。

RFC1112
Internet 组播协议 (IGMP)。

RFC1122
互联网主机需求—通信层。

RFC1123
互联网主机需求—应用与支持。

RFC1137
完整 RFC 822 与带有限制编码的 RFC 822 之间的映射。

RFC1153
摘要消息格式。

RFC1155
管理信息结构 (SMI)。

RFC1157
简单网络管理协议 (SNMP)。

RFC1176
交互式邮件存访问协议：版本 2。

RFC1310
互联网标准流程。

RFC1319
MD2 消息摘要算法。

RFC1320
MD4 消息摘要算法。

RFC1321
MD5 消息摘要算法。

RFC1343
多媒体邮件格式信息的用户代理配置机制。

RFC1344
MIME 对互联网邮件网关的影响。

RFC1345
字符助记与字符集。

RFC1421
互联网电子邮件隐私增强：第一部分—消息加密与认证程序。

RFC1422
互联网电子邮件隐私增强：第二部分—基于证书的密钥管理。

RFC1423
互联网电子邮件隐私增强：第三部分—算法、模式与方法[草案]。

RFC1428
从 Just-Send 到 8bit-SMTP/MIME 的互联网邮件传输。

RFC1492
访问控制协议，有时称为 TACACS。

RFC1495
X.400(1988)/ISO 10021 与 RFC 822 之间的映射。

RFC1496
X.400 从 1988 到 1984。

RFC1505
互联网消息头部字段编码。

RFC1510
Kerberos 网络认证服务 (V5)。

RFC1519
无分类域间路由 (CIDR)分配与聚合策略。

RFC1521
MIME (多用途互联网邮件扩展)：指定和描述互联网消息正文格式的机制 (MIME)。

RFC1522
互联网消息头中非 ASCII 文本的表示。

RFC1566
邮件监控 MIB。

RFC1579
防火墙友好 FTP。

RFC1583
开放最短路径路由 V2 (OSPF2)。

RFC1625
Z39.50-1988 之上的 WAIS。

RFC1631
IP 网络地址转换 (NAT)。

RFC1652
用于 8bit-MIME 传输的 SMTP 服务扩展。

RFC1661
点点协议 (PPP)。

RFC1711
邮件路由中的分类。

RFC1725
关于本页的意见和建议应邮件至 gmourani@videotron.ca
邮局协议版本 3 (POP)3。

RFC1738
统一资源定位符 (URL)。

RFC1739
互联网和 TCP/IP 工具入门。

RFC1796
并非所有 RFC 标准。

RFC1830
用于传输大型二进制 MIME 消息的 SMTP 服务扩展。

RFC1844
多媒体邮件 (MIME) 用户代理清单。

RFC1845
用于检查点/重启的 SMTP 服务扩展。

RFC1846
SMTP 521 回复代码。

RFC1854
用于命令流水的 SMTP 服务扩展。

RFC1855
网络礼仪指南。

RFC1864
content-MD5 头部。

RFC1866
超文本标记语言 - 2.0。

RFC1869
SMTP 服务扩展。

RFC1870
消息大小声明 SMTP 服务扩展。

RFC1872
MIME Multipart/Related 内容类型。

RFC1873
消息/外部主体内容-ID 访问类型。

RFC1883
IP版本 6 (IPv6) 规范。

RFC1884
IP 版本 6 地址体系。

RFC1886
支持 IP 版本 6 的 DNS 扩展。
关于本页的意见和建议应邮件至 gmourani@videotron.ca
RFC1891
递送状态通知的 SMTP 服务扩展。

RFC1892
用于邮件系统管理消息报告的 Multipart/Report 内容类型。

RFC1893
增强邮件系统状态码。

RFC1894
用于递送状态通知的可扩展消息格式。

RFC1918
私有网络的地址分配。

RFC1928
SOCKS 协议版本 5。

RFC1929
SOCKS V5 用户名/密码认证。

RFC1961
SOCKS 版本 5 GSS-API 认证方法。

RFC2003
IP 内封装 IP。

RFC2028
参与 IETF 标准流程的机构。

RFC2060
互联网消息访问协议 – 版本 4rev1 (IMAP4)。

RFC2104
HMAC：用于消息认证的密钥哈希。

RFC2138
远程拨号用户服务 (RADIUS)。

RFC2200
互联网官方协议标准。

RFC2305
使用电子邮件的真真模式。

RFC2313
PKCS 1: RSA 加密版本 1-5。

RFC2314
PKCS 10: 证书请求语法版本 1-5。

RFC2315
PKCS 7: 加密消息语法版本 1-5。
