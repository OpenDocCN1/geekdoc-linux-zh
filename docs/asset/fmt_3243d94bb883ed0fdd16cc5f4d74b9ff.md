
![](img/7e0718570ccf16ae88870f5f49b7faed_381_0.png)

Fedora 救援 CD 可能无法满足你的系统恢复需求；它可能缺乏特定的以太网支持、文件系统支持，或者你成功恢复操作所需的全实用功能。另一种替代方案是 H. Peter Anvin 创建的 SuperRescue CD。

本质上，SuperRescue CD 是一个相当完整且健壮的红帽发行版（基于 Red Hat 7.2 和 2.4.20-rc1 内核），完全从可引导的 CD 运行。SuperRescue CD 最棒的一点是它带有构建脚本，因此添加新软件（特殊驱动程序或应用程序）并创建新 CD 非常简单。主页位于 http://heatmap.net/projects/superrescue/，但你可以直接从 http://www.kernel.org/pub/dist/superrescue/v2 获取副本。

## 相关命令

以下命令在 Fedora Core 中非常有用：

- `amanda` 是基于网络的备份系统。
- `ark` 是归档工具。
- `cp` 是复制命令。
- `scp` 是安全复制命令。
- `cpio` 是数据归档。
- `dd` 是数据复制。
- `gzip` 是压缩工具。
- `tar` 是 GNU 归档工具。

## 参考

在请求输入后，如果系统不确定如何继续，你将进入 root 身份的命令 shell；这里没有登录或密码。根据你的配置，你可能会或不会得到额外信息的提示。如果你迷路或困惑，可以随时重启。（使用救援模式会有帮助）。

- http://www.ibibio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Ext2fs-Undeletion 是目标文件系统的详细讨论。它涵盖了软磁盘，但这些技术是通用的。
- http://www.ibibio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Ftape-HOWTO.html 是关于软带的 HOWTO。
- http://www.linux.org/USB-guide/x498.html 存储设备的 USB 指南。如果你有 USB 设备并想知道它是否被支持，请查看此处。
- http://www.ibibio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Bootdisk-HOWTO.A18 这是一份 LILO 错误代码列表，用于调试无法启动的系统。
- http://www.backupcentral.com/amanda.html 这是《Unix 备份与恢复》中的章节（由 John R. Jackson 编写，O'Reilly and Associates 出版）。该章节在线可用并涵盖了 Amanda 的方方面。该网站为章节提供了方便的搜索工具
- http://twiki.org/cgi-bin/view/Wikilearn/RsyncLargeFileBeginner 使用 rsync 修复未通过 md5sum 检查的本地 ISO。
- http://www.lycoris.org/sections.php?op=viewarticle8 Lycoris ISO rsync 迷你 HOWTO。关于使用 rsync 文件的分步教程。
- http://www.mikerubel.org/computers/rsync_snapshots/ 使用 rsync 进行的自动化快照式备份。
- http://www.mondorescu.org/ Mondo Rescue 是一个独立于 Fedora Core 的裸机备份/恢复工具，使用 CD、DVD、磁带或 NFS：可以制作可引导的 CD 来恢复系统。
- http://www.cc14.ac.uk/cc14admin/linux-server/mondorescu/dvd_mond.html 使用 MondoRescue 备份 DVD 的 HOWTO。

# 第三部分

# 系统服务管理

# 本部分包含

- 第 12 章 在 Fedora 3.4 中打印 349
- 第 13 章 网络连接 375
- 第 14 章 管理 DNS 433
- 第 15 章 互联网连接 481
- 第 16 章 Apache Web 服务器管理 501
- 第 17 章 数据库服务管理 549
- 第 18 章 安全文件传输协议服务 579
- 第 19 章 电子邮件处理 627
- 第 20 章 新闻和其他协作通信 663
- 第 21 章 用于 Fedora 的 C/C++ 编程工具 693
- 第 22 章 Shell 脚本 715
- 第 23 章 使用 Perl 757
- 第 24 章 内核与模块管理 785
- 第 25 章 效率类应用 811
- 第 26 章 多媒体应用 835

# 第 12 章

# 在 Fedora 中打印

Fedora 支持来自 40 多家制造商的 600 多种打印机，并且可以将硬件与较计算机组合。在本章中，你将学习 Fedora 提供的打印服务。你会发现你的 Linux 系统可以立即作为打印机服务器平台，供本地或远程的 Linux、类 UNIX 或 Windows 工作站使用使用。

在这里，你将学习对支持 Fedora 打印至关重要的许多不同程序、文件和目录。本章还展示了配置新打印机的简单技术。你将学习多种让打印机快速、方便地投入使用的方法，并学习了一些用于连接具有不同端口配置的打印机与系统硬件的重要变通。

Fedora 使用通用 UNIX 打印系统 `CUPS`。其他打印系统（如 `LPRng`）也可以作为打印系统，但你可能无法使用 Fedora 自带的一些图形化工具。本章重点关注使用 `CUPS`，但有一个短小节专门介绍如何使用 `LPRng` 设置远程 Linux 打印机服务器。

# 互联网打印协议

`CUPS` 支持互联网打印协议 `IPP` 并提供了许多独特功能，如网络打印机目录（打印机浏览）服务、加密支持以及对 PostScript 打印机描述 `.ppd` 文件的支持。

根据互联网工程任务组 `IETF`，`IPP` 源于 Novell 在 1996 年的一项提案，旨在创建一种用于互联网的打印协议。从那时起，该系统不断发展并成熟为适用于各种 Linux 和类 UNIX 操作平台的稳定打印系统。

## 本章内容

- Fedora 打印概述
- 配置和管理打印机服务
- 创建和配置本地打印机
- 创建网络打印机
- 控制台打印
- 使用通用 UNIX 打印系统
- 避免打印机支持问题
- 参考文献

# Fedora 打印概述

Fedora 的打印过滤系统是实现多种文档打印的主要引擎。该引擎的核心是 Aladdin, Inc. 的 Ghostscript 解释器的 GPL 版本——`gs` client。系统管理员的打印机配置工具是 `system-config-printer` 客户端。

> 注意
Fedora 的打印系统可以打印到本地（连接）或远程（网络）打印机。如果你使用本地打印机，它将由打印机设备表示，例如 `/dev/lp0` 或 `/dev/usb1`（如果你有 USB 打印机）。本地和远程打印机使用在系统打印数据库 `/etc/printcap` 中定义的打印队列。正在打印的文档被称为作业（job），你可以在溢存目录 `/var/spool/cups` 中查看并控制你的当前打印作业列表或队列。注意，你只能控制自己的打印作业；只有 root 操作员才能控制系统上任何用户的打印作业。

要向系统添加打印机，请使用 `system-config-printer` 客户端来配置并保存打印机定义。该客户端将定义保存为系统打印能力数据库 `/etc/printcap` 中的一个条目。每个定义包含一个带有打印机名称、其主机和打印队列名称的文本字段。打印的文档将溢存到 `/var/spool/cups` 目录。一个示例 `printcap` 定义可能如下：

```text
# 此文件由 cupsd(8) 从
# /etc/cups/printers.conf 文件自动生成。对此文件的任何更改
# 将丢失。
lp1|lp:rm-stinky:rp=lp1:
```

`CUPS` 在 `/etc/cups` 目录下的一个名为 `printers.conf` 的文件中维护其自己的打印机数据库。例如，之前在 `/etc/printcap` 中定义的关联打印机在 `/etc/cups/printers.conf` 中可能有以下条目：

```text
<DefaultPrinter lp1
Info Created by redhat-config-printer 0.6.x
DeviceURI parallel:/dev/lp0
Location HP 648 local printer
State Id
Accepting Yes
JobSheets none none
QuotaPeriod 0
PageLimit 0
KLimit 0
</Printer>
```

此示例显示了名为 1p 的打印机定义，以及其关联的设备、描述、状态和其他信息。文件中各种可能的字段和条目记录在 `printer.conf` 的手册页中。

`CUPS` 使用一个名为 `cupsd` 的打印服务器（守护进程），`CUPS` 文档中也称为调度程序。该服务器可以像其他 Fedora 一样，通过 `service` 命令或系统进行控制。（注：此处原文存在大量重复句子，翻译时已去冗并保留核心逻辑）。

随后，您只需按照提示定义您的打印机并添加本地或远程打印服务。在保存更改之前，您应该打印测试页。可以使用打印机配置客户端，或者从 GNOME 或 KDE 客户端的文件菜单中选择打印项。

> `system-config-printer` 实用是对之前的 Red Hat 发行版中包含的过时 `printtool` 客户端的更新。虽然您可能在系统中也发现相关的工具（符号链接），如 `printtool`、`printconf-tui` 和 `/usr/sbin/printconf-tui`，但在 Fedora 下，您应该使用 `system-config-printer` 客户端来管理打印机。

## 基于控制的打印机快速上手

本地或远程打印服务也可以在本地或没有 X Window 系统的服务器上进行配置。为此地，请使用 Red Hat 的文本 `system-config-printer-tui` 打印机配置工具。您需要以 root 身份运行它：

```
# system-config-printer-tui
```

按下回车键后屏幕将清除，您将看到命令的主对话框。（您将在本章稍后的“基于控制的打印命令”部分看到此屏幕。）

> 如果您在控制台上未使用 X 的情况下以 root 启动 `system-config-printer`，将使用 `system-config-printer-tui` 界面。

您使用 Tab 键和空格键导航对话框并展开设备列表。可以通过高亮“New”按钮并按回车创建新的打印机条目。使用向上或向下光标键选择并高亮现有条目；然后高亮“Edit”按钮并按回车编辑之前定义的打印机。

您可以使用 `lpr` 命令从命令行打印文档，使用 `lpq` 命令查看所有活动作业，并使用 `lrpm` 命令控制打印队列。

## 管理打印服务

在定义打印机后，您可以使用命令行查看并控制您的打印作业，或者在 root 权限下，控制您系统上的所有打印作业和打印机。

表 12.1 包含了 Fedora 包含的 `CUPS` 及相关打印命令和驱动程序的部分列表。

### 表 12.1 打印相关命令和驱动程序

| 名称 | 描述 |
| :--- | :--- |
| a2ps | 为 PostScript 打印格式化文本文件 |
| accept | 控制 CUPS 打印目标 |
| cancel | 取消 CUPS 打印作业 |
| disable | 控制 CUPS 打印机 |
| dvi[lj1,lj4,lj2p,lj4] | 将 DVI 文件转换为特定的 PCL 格式 |
| enable | 控制 CUPS 打印机 |
| encscript | 将文本文件转换为 PostScript |
| escputil | Epson 式喷墨打印机实用程序 |
| gldrop | Canon LBP-4 和 LBP-8 激光打印机的驱动程序 |
| gs | Ghostscript 解释器 |
| gsbj[dj$00,lp] | Ghostscript 喷喷打印机驱动程序 |
| gsdj[dj$00,lj,lp] | Ghostscript 喷射打印机驱动程序 |
| lpadmin | 基于命令行的 CUPS 打印机工具 |
| lp | Berkeley 子集的 CUPS 打印控制客户端 |
| lpc | 通用过滤器打印 |
| lpf | 兼容 Berkeley 的 CUPS 作业队列工具 |
| lprstat | 显示 CUPS 打印作业和打印机状态 |
| mpage | PostScript 文本格式化工具 |
| pbe[2ppma,page,page,to10x,topson,topptx] | 便变位图转换实用程序 |
| pr | 文本格式化命令 |
| psmandup | 非双面打印机的双面打印工具 |
| reject | 控制 CUPS 打印作业目标 |
| setup | 启动打印机配置实用程序 |
| smclient | SMB 打印池进程 |
| smbprint | SMB Shell 脚本 |
| smspool | SMB 打印池进程 |
| thinkjetottopbm | 可变位图到 ThinkJet 打印机的转换工具 |

大多数 Linux 系统使用 PostScript 作为打印的默认文档格式。Fedora 使用 `gs` 命令配合 `CUPS` 来管理本地和远程打印作业以及打印作业期间传输的数据类型。`gs` 命令用于将文档流转换为目标打印机接受的格式（目标打印机很可能使用 HPCL）。

您可以使用 `gs` 解释器配合 `--help` 命令行选项来显示其内置的打印机设备，如下：

```
# gs --help
```

## 注意

Fedora 包含了可以使用查看许多不同类型文档的图形客户端。例如，要显示 PostScript 文档（包括压缩的 PostScript 文档）或 PostScript 图像，可以使用 `gv` 客户端。要显示 PDF 文格式（PDF），可以使用 `ev` 或 PDF 查看器。

`gs` 命令在命令行使用时输出许多行文本，然后列出打印和图形设备。另一种获取这些信息的方法是启动 `gs` 然后使用 `devicename ==` 命令，如下：

```
# gs Ghostscript 7.05 (2002-04-22)
Copyright (C) 2002 artscode LLC, Benicia, CA. All rights reserved.
This software comes with see the file PUBLIC for details.
Loading NimbusRomNoL-Regu from /usr/share/fonts/default/Type1/
n0210031.pfb...
241068 135956 164250 347466 0 done.
Loading NimbusSansL-Regu from /usr/share/fonts/default/Type1/n0190031.pfb...
278528 137933 368564 0 done.
Using NimbusSansL-Regu
```

## 基于控制的打印机配置

本地或远程打印服务也可以在本地或没有 X Window 系统的服务器上进行配置。为此，请使用 Red Hat 的文本 `system-config-printer-tui` 打印机配置工具。您需要以 root 身份运行它：

```
# system-config-printer-tui
```

按下回车键后屏幕将清除，您将看到命令的主对话框。（您将在本章稍后的“基于控制的打印命令”部分看到此屏幕。）

> 如果您在控制台上未使用 X 的情况下以 root 启动 `system-config-printer`，将使用 `system-config-printer-tui` 界面。

您使用 Tab 键和空格键导航对话框并展开设备列表。可以通过高亮“New”按钮并按回车创建新的打印机条目。使用向上或向下光标键选择并高亮现有条目；然后高亮“Edit”按钮并按回车编辑之前定义的打印机

您可以使用 `lpr` 命令从命令行打印文档，使用 `lpq` 命令查看所有活动作业，并使用 `lrpm` 命令控制打印队列。

## 管理打印服务

在定义打印机后，您可以使用命令行查看并控制您的打印作业，或者在 root 权限下，控制您系统上的所有打印作业和打印机。

### 表 12.1 打印相关命令和驱动程序（此处表格内容同上文，已翻译）

大多数 Linux 系统使用 PostScript 作为打印的默认文档格式。Fedora 使用 `gs` 命令配合 `CUPS` 来管理本地和远程打印作业以及打印作业期间传输的数据类型。`gs` 命令用于将文档流转换为目标打印机接受的格式（目标打印机很可能使用 HPCL）。

您可以使用 `gs` 解释器配合 `--help` 命令行选项来显示其内置的打印机设备，如下：

```
# gs --help
```
