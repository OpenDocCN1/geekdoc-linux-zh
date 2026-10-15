
## Fedora Core 救援 CD 的替代方案

Fedora 救援 CD 可能无法满足你的系统恢复需求；它可能缺少特定的以太设备支持、文件系统支持，以及你成功恢复操作所需的全实用功能。一种替代方案是 H. Peter Anvin 创建的 SuperRescue CD。

本质上，SuperRescue CD 是相当完整且健壮的 Hat 发版（基于 Red Hat 7.2 和 2.4-rc1 内核），它完全从可引导 CD 运行。SuperRescue 最棒的地方是它带有构建脚本，可以非常地添加新软件（软驱动程序或应用程序）并创建新 CD。主页位于 http://freshheat.net/projects/superrescue/，但你可以直接从 http://kernel.org/pub/dist/superrescue/v2/ 获取副本。

## 相关的 Fedora Core 命令

以下命令在 Fedora Core Linux 中执行备份、恢复和还原操作时非常有用：

- `amdump`—Amanda 是一种基于网络的备份系统，由 18 个独立的命令组成，用于 Linux。
- `ark`—一个 KDE 桌面 GUI 归档工具。
- `cp`—复制命令。
- `scp`—安全 shell 复制命令。
- `cpio`—数据归档工具。
- `dd`—数据复制和转换工具。
- `gzip`—GNU 压缩工具。
- `tar`—GNU 磁带归档工具。

## 参考

以下命令在 Fedora Core Linux 中执行备份、恢复和还原操作时非常有用：

- `amdump`—Amanda 是一种基于网络的备份系统，由 18 个独立的命令组成，用于 Linux。
- `ark`—一个 KDE 桌面 GUI 归档工具。
- `cp`—复制命令。
- `scp`—安全 shell 复制命令。
- `cpio`—数据归档工具。
- `dd`—数据复制和转换工具。
- `gzip`—GNU 压缩工具。
- `tar`—GNU 磁带归档工具。

# 第三部分

# 系统服务管理

## 本部分

- 第 12 章 在 Fedora 中进行打印 (35)
- 第 13 章 网络连接性 (381)
- 第 14 章 管理 DNS (439)
- 第 15 章 互联网连接 (485)
- 第 16 章 Apache Web 服务器管理 (505)
- 第 17 章 数据库服务 (551)
- 第 18 章 安全文件传输协议 (FTP) 服务 (581)
- 第 19 章 处理电子邮件 (629)
- 第 20 章 新闻和其他协作通信 (665)

# 第 12 章

# 在 Fedora 中进行打印

Fedora 支持来自 40 多个制造商的 600 多种打印机，并且可以将硬件与较新的计算机混合使用。在本章中，你将学习 Fedora 提供的打印服务。你会发现你的 Linux 系统可以立即作为服务器平台投入使用，供本地或远程 Linux、类 UNIX 系统或 Windows 工作站使用。

在这里，你将学习对于支持 Fedora 打印至关重要的许多程序、文件和目录。本章还展示了配置新打印机的简单技术。你将学习多种快速、方便地让打印机可用的方法，并学习到一些在连接配置不同的打印机和系统硬件时的一些重要工作变通方案。

Fedora 使用通用 UNIX 打印系统 `CUPS`。其他打印系统（如 `LPRng`）也可以作为打印系统，但你可能无法使用 Fedora 自带的某些图形化打印管理工具。本章重点关注 `CUPS`，但有一一小节专门介绍如何使用 `LPRng` 设置远程 Linux 打印机服务器进行打印。

# 互联网打印协议 (IPP)

`CUPS` 支持名为 `IPP` 的互联网打印协议并提供了许多独特功能，例如网络打印机目录（打印机浏览）服务、加密支持以及对 PostScript 打印机描述 `.ppd` 文件的支持。

根据互联网工程任务组 `IETF` 的说法，`IPP` 源于 Novell 在 1996 年的一项提案，旨在创建一个用于互联网的打印协议。从那时，该系统得到了发展并成熟为适用于各种 Linux 和类 UNIX 操作平台的稳定打印系统。

## 本章内容

- Fedora 打印概述
- 配置和管理打印服务
- 创建和配置本地打印机
- 创建网络打印机
- 控制台打印控制
- 使用通用 UNIX 打印系统 `CUPS`
- 避免打印机支持问题
- 参考文献

# Fedora 打印概述

Fedora 的打印过滤系统是启用多种文档打印的主要引擎。该引擎的核心是 Aladdin, Inc 的 Ghostscript 解释器的 GNU GPL 版本，即 `gs` 客户端。系统管理员的打印机配置工具是 `redhat-config-printer-client`。

> Fedora 的打印系统可以打印到本地（连接）或远程（网络）打印机。如果你使用本地打印机，它将由打印机设备表示，例如 `/dev/lp0` 或 `/dev/usb/lp0`（如果你有 USB 打印机）。本地和远程打印机使用系统打印能力数据库 `/etc/printcap` 中定义的打印队列。正在打印的文档被称为打印作业，你可以在打印目录（即 `/var/spool/cups`）中查看并控制你的当前打印作业列表或队列。注意，你可能只能控制自己的打印作业；只有 root 操作员才能控制系统中任何用户的打印作业。

要向你的系统添加打印机，请使用 `redhat-config-printer` 客户端创建、配置并保存打印机定义。该客户端将定义保存为系统打印能力数据库 `/etc/printcap` 中的条目。每个定义都包含一个文本字段，其中有打印机名称、主机和打印队列名称。打印的文档将溢出到 `/var/spool/cups` 目录。示例 `printcap` 定义可能如下：

```
# 此文件由 cupsd(8) 从

# /etc/cups/printers.conf 文件自动生成。对此文件的任何更改

# 都将丢失。

lp|lp:rm=stinky:rp=lp:
```

`CUPS` 在 `/etc/cups` 目录下的一个名为 `printers.conf` 的文件中维护其自己的定义打印机数据库。例如，之前在 `/etc/printcap` 中定义的抽象打印机在 `/etc/cups/printers.conf` 中可能有条目：

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

此示例显示了名为 `lp1` 的打印机定义，以及与其相关的设备、描述、状态和其他信息。该文件中各种可能的字段和条目在 `printer.conf` 手帮助页中有记录。

`CUPS` 使用一个名为 `cupsd` 的打印服务器（守护进程），在 `CUPS` 文档中也称为调度程序。可以像其他 Fedora 服务一样，通过 `service` 命令或 `redhat-config-services` 客户端控制服务器。如果服务器根据其配置文件中的设置运行，则应包含位于 `/etc/cups` 目录下的 `cupsd.conf`。`CUPS` 示例可以在 `/usr/lib/cups` 目录下找到。

`cupsd.conf` 手帮助页记录了服务器的 80 多种不同设置，你可以配置这些设置以匹配你的系统、网络或打印环境。默认的 `CUPS` 相关文件和目录存储在 `/usr/share/cups` 目录下。日志可以设置为七级，有关访问和错误的信息存储在 `/var/log/cups` 目录下的日志文件中。

资源需求可以通过其他设置进行定制，例如通过 `MaxCopies` 设置用户一个打印作业的最大副本数，通过 `MaxJobsPerUser` 设置用户活动打印作业数量的。`RIPcache`（默认为 SMB）控制打印期间用于图形缓存的内存量。

例如，如果你想限制一次只打印 20 份文档或页面，且每个用户同时只允许进行 10 个打印作业，请使用如下设置：

```
MaxCopies 20

MaxJobsPerUser 10
```
