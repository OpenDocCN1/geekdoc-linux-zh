
安装程序在第一个串口上运行，波特率为 9600，8 位数据位，无校验位，1 个停止位（通常称为 9600, 8, N, 1）。如果你的串口终端支持颜色，安装程序可以彩色运行。注意，运行 `remit` 并连接到你 SPARC 系统的计算机将以彩色显示。

在串口安装期间的提示对话框（任何带有 OK 按钮的对话框）中，你可以按 `Ctrl+Z` 启动子 shell。要返回安装程序，请在 shell 提示符处输入 `exit`。

安装完成后，只需正常启动，Red Hat Linux 将出现在你的串口终端上。

## C.8 安装：选择系统组件

（有关系统组件的说明，请参阅第 67 页第 4.6.1 节。）

**重要！** 在为 Red Hat Linux/SPARC 选择安装系统组件时，选择安装全部（Everything）而不选择“选择单个软件包”（Select individual packages）可能会导致严重问题，并可能导致 Red Hat Linux/SPARC 系统无法启动。原因如下：

- 最后安装的内核将是多处理器内核，它将在 sun4 机器上运行失败。
- 默认的 X 服务器将是 `XsunMono`，这对于大多数人来说可能无法工作。

如果你希望安装“全部”，请同时选择“选择单个软件包”。然后，取消选中除你想安装的一个内核以外的所有内核（`kernel-sparc` 适用于（大多数）机器）以及除你硬件对应的所有 X 服务器（bwtwo 视频卡使用 `XsunMono`，所有8 位显示器使用 `Xsun`，以及支持的 24 位显示器使用 `Xsun24`）。

## C.9 SILO 配置

SILO 配置与 LILO 配置几乎相同。详情请见第 82 页第 5.8 节。

**注意：** 与 LILO 不同，SILO 不能配置启动其他操作系统。有关配置 SILO 启动其他操作系统的信息，请阅读 `/usr/doc/silo*` 文件。

## C.10 分区

为 Red Hat Linux/ARC 分区时需要一个额外的步骤。记住你的系统类型，因为我们将在安装过程后期提到它。除 Jensen 之外的所有平台都包含 NCR 810 控制器，尽管 BusLogic PCI 控制器（FlashPoint 除）、Adaptec AHA2940 控制器以及 Qlogic 1020 控制器也是支持的。Jensen 设计使用了支持的 AHA1740 控制器。NE2000、DE422、DE4x5 以及 DE500 (PCI) 以太网卡是支持的，UDB 的内部以太网也是支持的。令牌环支持也包含在内核中。

### C.10.1 交换分区

- 用于 Red Hat Linux/ARC 的硬盘。记住你的系统类型，因为我们将在安装过程后期提到它。除 Jensen 之外的所有平台都包含 NCR 810 控制器，尽管 BusLogic PCI 控制器（FlashPoint 除）、Adaptec AHA2940 控制器以及 Qlogic 1020 控制器也是支持的。Jensen 设计使用了支持的 AHA1740 控制器。

## C.11 X Windows

- 用于 Red Hat Linux/ARC 的硬盘。记住你的系统类型，因为我们将在安装过程后期提到它。除 Jensen 之外的所有平台都包含 NCR 810 控制器，尽管 BusLogic PCI 控制器（FlashPoint 除）、Adaptec AHA2940 控制器以及 Qlogic 1020 控制器也是支持的。Jensen 设计使用了支持的 AHA1740 控制器。

## D.1 引言

本附录介绍了 Red Hat Linux/Alpha 和 Red Hat Linux 安装之间的差异。虽然它对这些差异提供了很好的概述，但你会发现顺序阅读第 2、3 和 6 章会更容易。

## D.2 支持的硬件

Red Hat Linux/Alpha 支持基于 Alpha 处理器和 PCI 总线的硬件。以下列表是制作本手册时的现状，并包含了系统类型（**加粗**）：

- Alcor - AlphaStation 600
- Cabrio - AlphaPCI64, AlphaPCI64; Aspen Telluride
- EB164 - Aspen Avalanche, Timberline, Summit; Microwave Screamer
- EB64+ - Aspen Alpine
- EB66 - NekoTech Mach 1
- EB66+
- Miata - Digital Workstation, a-Series and au-Series
- Mikasa - AlphaServer 1000; AlphaServer 1000A 不支持
- Noname - AspPC133, Universal Desktop Box, Multia
- PC164 - Aspen Durango
- PC164LX - Aspen II
- Alpha-XLT - XL 233, XL 266, XL 300, XL 366, AlphaStation 500; Maverick, Brett, AlphaStation 200, 205, 250, 255, 400

Jensen – (DEC PC150, 2000 Model 300, 2000 Model 500, Cullean)

**注意：**记住你的系统类型，因为我们将在安装过程后期提到它。除 Jensen 之外的所有平台都包含 NCR 810 控制器，尽管 BusLogic PCI 控制器（FlashPoint 除）、Adaptec AHA2940 控制器以及 Qlogic 1020 控制器也是支持的。Jensen 设计使用了支持的 AHA1740 控制器。

NE2000, DE422, DE4x5, 以及 DE500 (PCI) 以太网卡是支持的，UDB 的内部以太网也是支持的。

## D.3 安装概述

X Window 系统应能够在任何带有 S 系列显卡的机器上运行（Jensen 机器除外）。S3 Virge 显、Matrox Millenium、Millenium II 以及 Mystique 均可用，Orchid 和 Number 9 的多数卡也可用。大多数 Diamond Stealth 显同样受支持。Digital TGA 卡（基于 DC21030 芯片）支持 8 位模式，并且还为 Mach64 卡提供了 X 服务器。

**请注意：** 专门为带有 S3 卡的 Jensen 机器提供了可用的 X 服务器。可以通过 `ftp://ftp.azstarnet.com/pub/linux/axp/jensen` 获取。请注意，如果在连接时遇到困难，几个较大的 FTP 站点都有该站点的镜像。

## D.3 安装概述

在 Alpha 系统上安装 Red Hat Linux 比安装 Red Hat Linux/Intel 稍微复杂，这主要是由于机器架构的差异以及支持的各种型号造成的。通常情况下，成功安装的主要步骤为：

- 1. 从 Red Hat Linux/Alpha CD 上的镜像创建 MILO、内核和 ramdisk 磁盘软。
- 2. 使用 MILO 磁盘软启动适当的 Linux 内核。
- 3. 加载并运行 Red Hat Linux/Alpha 安装程序。
- 4. 安装完成后，在机器上的一个小磁盘分区上安装 MILO。

**请注意：** 虽然大多数 Alpha 系统都支持 MILO，但那些不支持的系统需要直接从 SRM（系统参考手册）控制台从启动软盘（或 CD-ROM）启动。有关此操作的信息可以访问 Red Hat 软件网站 `http://www.redhat.com/linux-info/alpha/faq`。您还应该咨询系统文档以获取正确的启动命令语法，但通常情况下，正确的命令看起来如下：

```
boot dva0 -file vmlinux.gz -flags "load_ramdisk=1 prompt_ramdisk=1"
```
