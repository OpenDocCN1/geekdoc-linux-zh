
你也可以使用连接到 SPARC 系统的串口终端来安装 Red Hat Linux/SPARC。任何可以仿真 VT100 的终端（或带有终端仿真软件的计算机）都可以正常工作。按通常方式启动，并在 SILO 提示符处输入：

```
linux serial
```

安装程序在第一个串口上运行，波特率为 9600 波特、8 位数据位、无校验位、1 位停止位（通常称为 9600,8,N,1）。如果你的终端支持颜色，安装程序可以彩色运行。请注意，连接到你 SPARC 系统的运行内核的计算机将以彩色显示。

在串口安装期间的任何提示对话框中（任何带有 OK 按钮的对话框），你都可以按 `Ctrl+Z` 启动子 shell。在提示符处输入 `exit` 可返回安装程序。

安装完成后，只需正常启动，Red Hat Linux 就会出现在你的串口终端上。

## C.8 安装：选择系统组件

（有关系统组件的解释，请参见第 67 页的第 4.6.1 。）

**重要！**在为 Red Hat Linux/SPARC 选择安装的系统组件时，如果不选择软件包而直接选择全部，会导致严重问题，并可能导致 Red Hat Linux/SPARC 系统无法启动。原因如下：

- 最后安装的内核是多处理器内核，它在 `sun4` 上无法工作。
- 默认 X 服务器将是 `XsunMono`，这对于大多数人可能无效。

如果你希望安装**全部**，请也选择**选择软件包**。然后，取消选择除你想安装的内核以外（`kernel-sparc` 适用于大多数情况）以及除硬件以外的所有 X 服务器（双显卡使用 `XsunMono`，所有 8 位显示器使用 `Xsun`，支持的 24 位显示器使用 `Xsun24`）。

## C.9 SILO 配置

SILO 配置与 LILO 配置几乎相同。详情请参见第 82 页的第 5.8 节。

**注意：**与 LILO 不同，SILO 在安装期间无法配置启动其他操作系统。但是，提供了配置 SILO 启动其他操作系统的信息。请在安装后阅读 `/usr/doc/silo*/docs` 中的 README 文件。

## C.10 分区

为 Red Hat Linux/SPARC 分区硬盘需要一个额外的步骤。注意，分区必须是 `ext2` 格式。如果你对新磁盘进行分区，请使用 `fdisk` 创建分区。

### C.10.1 交换分区

除 Jensen 外的所有平台都包含 NCR 810 SCSI 控制器，同时也支持 BusLogic PCI SCSI 控制器（FlashPoint 之外）、Adaptec AHA2940 SCSI 控制器以及 QLogic 1020 ISP 控制器。Jensen 设计使用 AHA1740 SCSI 控制器，它是支持的。

## C.11 X Windows

这种安装方法需要局域网连接以及访问带有 Red Hat Linux/SPARC CD-ROM（或等效文件）的 FTP 站点。如果你只有显示器，则需要 `Xsun`。

## D.3 安装概述

X Window 系统应能在任何带有基于 S3 显卡的机器上运行（射线机器除外）。S3 Virgo 显卡、Matrox Millenium、Millenium II 和 Mystique 均可用，以及大多数 Orchid 和 Number 9 的显卡。大多数 Diamond Stealth TGA 卡（基于 DC2130 芯片）在 8 位模式下受支持，并且提供了为 Mach64 卡提供的 X 服务器。

**注意：** 专门为带有 S3 显卡的 Jensen 系统提供了一个 X 服务器。可以通过 `http://ftp.azartnet.com/pub/linux/axp/jensen` 获取。请注意，该站点由几个较大的 FTP 站镜像，如果您在连接时遇到困难，可以尝试。

在 Alpha 系统上安装 Red Linux 比安装 Red Hat Linux/Intel 稍微复杂，这是由于机器架构的差异以及支持的各种型号导致的。通常情况下，成功安装的主要步骤为：

- 1. 从 Red Hat Linux/Alpha CD 上的镜像创建 MILO、内核和 ramdisk 磁盘。
- 2. 使用 MILO 软盘启动相应的 Linux 内核。
- 3. 加载并运行 Red Hat Linux / Alpha 安装程序。
- 4. 安装完成后，在机器上的一个小磁盘分区上安装 MILO。

**注意：** 虽然大多数 Alpha 系统都支持 MILO，但某些系统不需要直接从 SRM（系统参考手册）控制台启动软盘（或 CD-ROM）。有关此操作的信息可以在 Red Hat 网站 `http://www.redhat.com/linux-info/alpha/faq` 获取。您还应该咨询您的系统文档以获取正确的启动命令语法，但通常，正确的命令如下：

```
boot dva0 -file vmlinux.gz -flags "load_ramdisk=1 prompt_ramdisk=1"
```

## D.4 选择软盘镜像

Red Hat Linux/Alpha 安装过程是基于软盘的。软盘的数量和内容取决于您拥有的 Alpha 系统类型。因此，在创建软盘之前，必须选择合适的镜像文件。请参考下表：

| 系统类型 | MILO 镜像 (位于 milo 目录) | 启动镜像 (位于 images 目录) |
| :--- | :--- | :--- |
| Alcor (ARC 控制台) | 无 | `alcor.img` |
| Alcor (SRM 控制台) | 无 | `alcor-s.img` |
| Alpha-XLT | `xlt.img` | `xlt.img` |
| Cabernet | `cab.img` | `cab.img` |
| EB164 | `eb164.img` | `eb164.img` |
| EB64+ | `eb64p.img` | `eb64p.img` |
| EB66 | `eb66.img` | `eb66.img` |
| EB66+ | `eb66p.img` | `eb66p.img` |
| Miata | `miata.img` | `miata.img` |
| Noname | `noname.img` | `noname.img` |
| PC164 | `pc164.img` | `pc164.img` |
| PC164LX | `lx164.img` | `pc164.img` |
| PC164SX | `sx164.img` | `sx164.img` |

创建启动软盘 如果您的系统支持 MILO，您将在 Red Hat Linux/Alpha CD-ROM 的 `milo/images` 目录中找到相应的镜像。请参阅第 193 页的附录 B 获取将镜像写入软盘的说明。确保将软盘标记为“MILO Diskette”。

请注意：如果您在 MILO 方面遇到问题……

创建启动软盘 您将在 Red Hat Linux/Alpha CD-ROM 的 `images` 目录中找到相应的启动软盘镜像。请参阅第 193 页的附录 B 获取将镜像写入软盘的说明。确保将软盘标记为“Boot Diskette”。

## D.5 安装

创建 Ramdisk 磁盘所有的 Red Hat Linux/Alpha 安装都使用相同的 ramdisk 镜像。它被称为 `ramdisk.img`，可以在 Red Hat Linux/Alpha CD-ROM 的 `images` 目录中找到。请参阅第 193 页的附录 B 获取将镜像写入软盘的说明。确保将软盘标记为“Ramdisk Diskette”。

### D.5.1 启动 MILO 软盘

（如果您的 Alpha 系统不支持 MILO，请跳到下一页的 D.5.2 节）。

在启动 MILO 软盘之前，您需要为 ARC 控制台添加新的启动选项。您可以按照以下步骤为您的 MILO 软盘添加新的启动选项：

- 1. 从启动菜单中选择“Supplementary menu”（补充菜单）。
- 2. 从补充菜单中选择“Set up the system”（设置系统）。
- 3. 从启动选项菜单中选择。
- 4. 使用 MILO 软盘启动相应的 Linux 内核。
- 5. 加载并运行 Red Hat Linux / Alpha 安装程序。
- 6. 安装完成后，在机器上的一个小磁盘分区上安装 MILO。
- 1. 从启动菜单中选择“Supplementary menu”。
- 2. 从补充菜单中选择“Set up the system”。
- 3. 从启动选项菜单中选择。
- 4. 使用 MILO 软盘启动相应的 Linux 内核。
- 5. 加载并运行 Red Hat Linux / Alpha 安装程序。
- 6. 安装完成后，在机器上的一个小磁盘分区上安装 MILO。
- 1. 从启动菜单中选择“Supplementary menu”。
- 2. 从补充菜单中选择“Set up the system”。
- 3. 从启动选项菜单中选择。
- 4. 使用 MILO 软盘启动相应的 Linux 内核。
- 5. 加载并运行 Red Hat Linux / Alpha 安装程序。
- 6. 安装完成后，在机器上的一个小磁盘分区上安装 MILO。
