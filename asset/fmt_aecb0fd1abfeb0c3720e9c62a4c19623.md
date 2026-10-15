
在救援模式下，你可以可以使用许多命令行工具，但没有提供 GUI 工具。对于网络，你使用 `ifconfig`、`route`、`rcp`、`login`、`gzip` 和 `ftp` 命令。对于归档（恢复归档），有 `cpio`、`uncpio`、`gzip`、`gunzip`、`zcat` 和 `mdsum` 命令。对于编辑器，由 `busybox` 和 `pico` 启用，`jmac` 和 `joe` 由 joe 编辑器提供。还有其他系统命令。仔细观察这些命令可以发现，它们都是指向 http://www.busybox.net/ 上名为 busybox 程序的链接。

BusyBox 为任何小型或嵌入式系统提供了一个合理的 POSIX 环境。BusyBox 中的工具通常比功能齐全的 GNU 选项少；然而，包含的选项“提供了预期的功能，并且行为与它们的 GNU 非常相似”。这意味着你应该先测试救援模式，看看它是否能恢复你的数据以及你有哪些可用选项，因为 BusyBox 版本与完整的 GNU 版本略有不同。（某些选项缺失了；某些选项的工作方式不同——你需要在紧急情况发生前知道这是否会影响你。）

使用救援模式时有一些实用的技巧需要了解。如果系统功能正常，你可以按照这种方式使用 `chroot` 命令将根文件系统从 CD 切换到你的系统：

```bash
# chroot /mnt/sysimage
```

你会发现一个新的命令提示符，并且所有的文件——希望的话——都在正确的位置。你熟悉的工具——完好无损——应该是可用的。如果你退出 chroot 环境，使用 `exit` 命令返回救援提示符。如果你再次使用 `exit` 命令，系统将重启。

救援环境提供了一组良好的网络命令和支持网络的工具，如 `scp`、`sftp` 以及一些迭代工具。它还提供了 `rpm`，可以通过网络连接获取包。如果你想将它们安装在挂载于 `/mnt/sysimage` 的文件系统中而不是 `/`，那么安装它们将很复杂。为了实现这一点，使用 `--root` 参数设置备选的根路径：

```bash
# rpm -iv --root /mnt/sysimage ftp://location/package.rpm
```

### FEDORA 救援 CD 的替代方案

Fedora Core 救援 CD 可能无法满足你的系统需求；它可能缺少特定的以太网设备、文件系统支持，或者你成功恢复操作所需的完整功能。一种替代方案是由 H. Peter Erwin 创建的 SuperRescue CD。本质上，SuperRescue CD 是一个非常健壮的 Red Hat 发行版（基于 Red Hat 7.2 和 2.4.0-1 内核），完全从可引导 CD 运行。（那个 SuperRescue CD 的最好之处是它带有构建脚本，因此非常容易添加新软件（该驱动程序或应用程序）并创建新的 CD。）主页位于 http://freshmeat.net/projects/superrescue/，但你可以直接在 http://www.kernel.org/pub/dist/superrescue/v2/ 获取副本。

## 相关的 FEDORA CORE 命令

这些命令在 Fedora Core Linux 中执行备份、恢复和重建操作非常有用：

- `amdump`—Amanda 是一个基于网络的备份系统，由 18 个独立的命令组成，供 Linux 使用。
- `ark`—一个 KDE 桌面归档工具。
- `cp`—拷贝命令。
- `scp`—安全 shell 拷贝命令。
- `cpio`—数据归档工具。
- `dd`—数据拷贝和转换工具。
- `gzip`—GNU 压缩工具。
- `tar`—GNU 归档工具。

### 引用

- `amdump`—Amanda 是一个基于网络的备份系统，由 18 个独立的命令组成，供 Linux 使用。
- `ark`—一个 KDE 桌面归档工具。
- `cp`—拷贝命令。
- `scp`—安全 shell 拷贝命令。
- `cpio`—数据归档工具。
- `dd`—数据拷贝和转换工具。
- `gzip`—GNU 压缩工具。
- `tar`—GNU 归档工具。

（注：原文文本中存在大量重复内容，译文已根据逻辑结构进行了去重处理。）

# 第三部分

## 系统服务管理

本部分包含

- 第 12 章 在 Fedora 34 上进行打印 349
- 第 13 章 网络连接 375
- 第 14 章 { DNS 433
- 第 15 章 互联网连接 479
- 第 16 章 Apache Web 服务器管理 499
- 第 17 章 数据库服务管理 545
- 第 18 章 安全文件传输协议 (FTP) 服务 575
- 第 19 章 电子邮件处理 623
- 第 20 章 新闻和其他协作通信 659

# 第 12 章

## 在 Fedora 上进行打印

Fedora 支持来自 40 多个制造商的 600 多种打印机，并且可以将硬件与新计算机进行混合搭配。在本章中，你将学习 Fedora 提供的打印服务。你会发现你的 Linux 系统可以立即作为打印服务器平台投入使用，供本地或远程的 Linux、类 Unix 或 Windows 工作站使用。

在这里，你将学习支持 Fedora 下打印功能不可或缺的不同程序、文件和目录。本章还展示了配置新打印机的简单技术。你将学习多种快速方便地让打印机可用的方法；并学习一些连接具有不同端口配置的打印机与系统硬件的重要替代方案。

Fedora 使用通用 UNIX 打印系统 (CUPS)。可以使用其他打印系统（如 LPRng），但你可能无法使用 Fedora 自带的一些图形打印管理工具。本章重点关注 CUPS，但有一短节介绍了如何使用 LPRng 设置远程 Linux 打印服务器。

## 本章内容

- Fedora 打印概述
- 配置和管理打印服务
- 创建和配置本地打印机
- 创建网络打印机
- 控制台打印控制
- 使用通用 UNIX 打印系统 (CUPS)
- 避免打印机支持问题
- 参考

# 互联网打印协议 (IPP)

CUPS 支持名为 IPP 的互联网打印协议，提供了许多独特功能，例如网络打印机目录（打印机浏览）服务、对加密的支持以及对 PostScript 打印机描述 `.ppd` 文件的支持。

根据互联网工程任务组 (IETF) 的规定，IPP 源于 Novell 在 1996 年提出的一个用于在互联网上使用打印协议的建议。从那时起，该系统不断发展，并已成为一个适用于各种 Linux 和类 Unix 操作平台的稳定打印系统。

### 第 12 章 在 Fedora 上进行打印

## Fedora 打印概述

Fedora 的打印过滤系统是实现多种类型文档打印的主要引擎。该引擎的核心是 Aladdin, Inc Ghostscript 解释器的 GNU GPL 版本，即 `gs` 客户端。系统管理员的打印机配置工具是 `system-config-printer` 客户端。

注意

Fedora 的打印系统可以打印到本地（外接）或远程（网络）打印机。如果你使用本地打印机，它将由打印机设备表示，例如 `/dev/lp0` 或 `/dev/usb/lp0`（如果你有 USB 打印机）。本地和远程打印机使用在系统打印能力数据库 `/etc/printcap` 中定义的打印队列。文档被称为打印作业，你可以在 spool 目录（即 `/var/spool/cups`）中查看并控制你的当前打印作业列表或队列。请注意，你只能控制自己的打印作业；root 操作员可以控制系统上任何用户的打印作业。

要向系统添加打印机，请使用 `system-config-printer` 客户端创建、配置并保存你的打印机定义。该客户端将定义保存为系统打印能力数据库 `/etc/printcap` 中的一个条目。每个定义都包含一个文本字段，其中有打印机名称、主机和打印队列名称。打印的文档将溢流到 `/var/spool/cups` 目录。一个 `printcap` 定义示例如下：

```
# 此文件由 cupsd(8) 从
# /etc/cups/printers.conf 文件自动生成。对此文件的任何更改
# 将丢失。
lp1:lp=stinky;rp=lp1:
```

CUPS 在 `/etc/cups` 目录下通过名为 `printers.conf` 的文件维护自己的定义打印机数据库。例如，之前在 `/etc/printcap` 中定义的关联打印机在 `/etc/cups/printers.conf` 中可能有以下条目：

```
<DefaultPrinter lp1
Info Created by redhat-config-printer 0.6.x
DeviceURI parallel:/dev/lp0
Location HP 648 local printer
State Idle
Accepting Yes
JobSheets none none
QuotaPeriod 0
PageLimit 0
KLimit 0
</Printer>
```
