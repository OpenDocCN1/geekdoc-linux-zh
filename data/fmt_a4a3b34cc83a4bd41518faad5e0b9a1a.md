
## 救援系统

当你需要知道无法轻易挂载的驱动器或磁盘上的内容（可能是非 Linux 格式，或包含原始数据）时，使用...（此处由于原文逻辑重复，根据指令已翻译已包含后续的重复内容）。

（注：根据您的指令，原文中存在大量逻辑重复的句子和段落，如“计算机上的引导程序是损坏的，或者是错误的”等，已按原文逻辑翻译。由于文件系统出现错误，或者在无意中更改文件导致系统无法启动。）

# 第 11 章 备份、恢复与还原

## 使用通用软盘启动系统

如果你未能制作启动软盘，或者找不到之前制作的软盘，任何 Linux 启动软盘（稍旧的版本或从朋友那里借来的）都可以派上用，因为它们的内核版本相当相似。（主版本和次版本号——例如，`2.4.13` 可能适用于任何 `2.4` 系统，但不能适用于 `2.2` 系统。）通过手动指定之前过的 root 和 boot 分区，你可以启动系统。虽然几乎会收到一些错误信息，但你至少可以运行一个足够替换文件并恢复系统的基础系统。

## 特殊驱动程序

在两种情况下，都假设不需要任何文件系统或设备驱动来访问根分区。如果需要，请在 LILO 行添加 `initrd=` 参数。如果你不知道 `initrd` 文件的确切名称，那么 LILO 将无能为力，请学习使用 GRUB。

## 使用 GRUB 启动软盘

统一引导加载程序 `GRUB` 在尝试从带有自定义启动软盘的系统启动时可以成为救星。`GRUB` 镜像可以从 `ftp://alpha.gnu.org/gnu/grub/grub-0.90-i386-pc.ext2fs` 下载。或者，如果你有一个现有的使用 `GRUB` 的启动软盘，使用 `write.exe` 也是可以。

> 注意
> `alpha.gnu.org` 似乎已经离线。文件的临时位置已建立在 `http://www.gnu.org/software/grub/grub-download.html`。

`GRUB` 拥有自己的 shell、文件系统驱动程序和搜索功能（类似于 bash shell）。可以使用 `GRUB` 启动软盘检查驱动分区，并搜索内核和 `initrd` 镜像，以此启动系统。作为它独立的一章，`GRUB` 文档非常详尽：除了 `info GRUB`（`info` 系统类似于 `man` 系统），`GRUB` 文档还包含值得阅读的教程。`GRUB` 的灵活性和功能受到 Red Hat Linux 默认引导加载程序的影响。

![](img/446debe02348607fde57245cfa3ff_388_0.png) 图 11.5 `GRUB` 引导加载程序在启动未知系统时提供了惊人的灵活性。

## 使用安装盘进行恢复

如前面的示例所示，在启动提示符输入 `linux rescue` 命令进入救援模式。救援模式运行一个独立于你系统的 Red Hat 版本。当根分区因某些错误而无法启动时，它允许你挂载根分区进行维护。Red Hat 在不断改进恢复功能。

进入救援模式后，你可以选择语言和键盘布局。最小操作系统尝试将你的 Red Hat 安装挂载到 `/mnt/sysimage`；这一步可以跳过（你可能还没有挂载任何内容），并将你带入 shell。

如果你选择挂载安装，会被要求确认根分区。救援功能还支持软件 RAID 数组（RAID 0、1 和5），以及格式为 `ext2`、`ext3`、`reiserfs`、`vfat`、`fat` 和 `mdfs` 的 IDE 或 SCSI 分区。在不确定如何继续后，你最终会命令 shell；根据你的配置，可能会看到或看不到额外信息的提示。

如果你需要连接性，`ne2k-pci` 和 `8390` 模块作为 `ifconfig`、`route`、`rcp`、`login`、`rsh` 和 `ftp` 命令可用。对于归档（还原归档），有 `cpio`、`uncpio`、`gzip`、`gunzip`、`dd`、`zcat` 和 `md5sum` 命令。对于编辑器，`vi` 和 `pico` 也作为其他实用命令可用。仔细观察这些命令可以发现，它们都是指向一个名为 `busybox` 的程序的链接（首页：`http://busybox.org/`）。

`BusyBox` 为任何小型或嵌入式系统提供了相当完整的 POSIX 环境。`BusyBox` 中的工具通常比其功能全的 GNU 选项少；然而，包含的选项“提供了预期的功能，并且行为与 GNU 版本非常相似”。这意味着你应该测试救援模式，看看是否可以恢复数据以及有哪些可用选项，因为 `BusyBox` 版本的行为与完整的 GNU 版本略有不同。（某些选项缺失；某些选项工作不完全相同——你需要在紧急情况发生前知道这将如何影响你）。

## Red Hat 救援 CD 的替代方案

Red Hat 救援 CD 可能无法满足你的系统恢复需求；它可能缺少以太网支持、文件系统支持或成功恢复所需的完整工具功能。H. Peter Anvin 创建的 SuperRescue CD 是一个替代方案。

本质上，SuperRescue CD 是一个相当完整且健壮的 Red Hat 发行版（基于 Red Hat 7.2 和 `2.4.18-preac3` 内核），完全从 CD 运行。SuperRescue CD 最棒的一点是它带有脚本，因此非常容易使用。

## 相关 Red Hat 和 Linux 命令

以下命令在备份、恢复和还原中很有用：

- `amdump`: Amanda 是一个基于网络的备份系统。
- `cp`: 安全拷贝命令。
- `scp`: 安全外壳命令。
- `cpio`: 数据归档工具。
- `dd`: 数据复制和转换工具。
- `gzip`: GNU 压缩工具。
- `tar`: GNU 归档工具。

## 参考文献

`http://www.tldp.org/HOWTO/Filesystems-HOWTO.html`：如果你正在处理不熟悉的文件系统，Filesystems HOWTO 是一个很好的开始。

`http://www.tldp.org/Bootdisk-HOWTO/index.html`：Linux Bootdisk HOWTO 涵盖了启动的设计和构建。它提供了大量关于启动过程的信息，帮助你解决问题。

`http://www.tldp.org/Bootdisk-HOWTO/a139.html`：这是一个 LILO 启动代码列表，帮助你调试无法启动的系统。

`http://metalab.unc.edu/pub/Linux/system/boot/lilo/lilo-u-21.gz`：如果系统中没有安装 LILO，这就是 LILO 用户文档。

`http://www.freshmeat.net`：Freshmeat 网站提供稳定的 Linux公告和信息，并提供搜索功能。

`http://www.google.com/linux/`：Google 的 Linux 部分有助于消除无用的提示。

`http://kmself1.home.net.com/Linux/FAQs/backups.html`：Linux Backups-FAQ 包含关于备份媒体、加密和安全的一些简短评论。

`http://www.tldp.org`：Linux 文项目提供了关于备份和磁盘恢复的实用 HOWTO 文档。

`http://www.tldp.org/mini/Ext2fs-Undeletion.html`：如果你需要从 `ext2/3` 文件系统删除文件，Ext2fs Undeletion mini-HOWTO 是适合你的文档。练习就会成功。

`http://www.tldp.org/mini/Ext2fs-Undeletion-Dir-Struct/index.html`：Ext2fs Undeletion Directory Structures 是 Linux Ext2fs mini-HOWTO 的配套文档，帮助你应对误删 `rm -rf *`。

`http://www.tldp.org/FAQ/Ftape-FAQ.html`：这是软盘带设备驱动程序的常见问题；它有点旧了。

`http://www.linux-usb.org/USB-guide/x498.html`：大容量存储设备的 USB 指南。如果你有 USB 设备并想知道它是否支持，请查看此处。

`http://www.tld.org/HOWTO/LILO-crash-rescue-HOWTO.html`—此 HOWTO 描述了如何使用基于软盘的恢复磁盘，但这些技术是通用的。文中涵盖的技术包括检查目标文件系统的完整性。内容稍显单薄，但其相关的 URL 链接值得关注。

`http://www.backupcentral.com/amanda.html`—这是在线可用的《UNIX 备份与恢复》中的 Amanda 章节；该网站为该章节提供了搜索工具。

# 第三部分

# 系统服务管理

# 本部分内容

+ 第 12 章 打印服务 359
+ 第 13 章 网络连接性 389
+ 第 14 章 管理 DNS 445
+ 第 15 章 互联网连接 485
+ 第 16 章 Apache Web 服务器管理 503
+ 第 17 章在 Red Hat Linux 中管理数据库服务 551
+ 第 18 章 安全文件传输协议 FTP 服务 581
+ 第 19 章处理电子邮件 627
+ 第 20 章 新闻和其他协作通信 659

# 第 12 章

# 打印服务

## 本章内容

- Red Hat Linux 打印概述
- 配置和管理打印服务
- 创建和配置本地打印机
- 创建网络打印机
- 控制台打印控制
- 使用通用 Unix 打印系统 CUPS
- 避免打印机支持问题
- 参考

Red Linux 支持来自 60 多个制造商的 600 多种打印机，并且可以将打印硬件与较新的计算机混合使用。在本章中，你将学习 Red Hat Linux 提供的打印服务。你会发现 Linux 可以立即作为打印平台投入使用，供本地或远程 Linux、UNIX 或 Windows 工作站使用。

你将学习 Red Hat Linux 内部用于支持打印的许多程序、文件和目录。本章还展示了在 Red Hat Linux 中配置新打印机的简单技术。你将学习多种在 Red Hat Linux 中快速方便地让打印机可用的方法，并学习一些用于连接具有不同端口配置的打印机和系统硬件的重要变通方法。

Red Hat 提供了两种用于打印文件的不同打印系统：LPRng 和通用 Unix 打印系统 CUPS。在使用 Red Hat 时，你可以使用其中一种，但不能两者都作为打印的基础。本章重点关注 LPRng 的使用，但有一个专门的章节介绍设置、配置、管理和使用 CUPS 进行打印。你可以通过 Red Hat 的图形化 `redhat-switch-printer` 实用（在本章稍后的部分讨论）在 LPRng 和 CUPS 之间切换。

# Red Hat Linux 打印概述

Red Hat 新且经过修订的打印过滤器系统是使用 Linux 许多类型文档的主要引擎。该引擎的核心是 Aladdin, Inc. gs 客户端的 GNU GPL 版本。Red Hat 系统管理员的打印机配置工具是 `redhat-config-printer` 客户端。

# 第 12 章 打印服务

> 注意
> Hat 的打印系统可以用于打印到本地（连接）或远程（网络）打印机。如果你使用本地打印机，它将由打印设备表示，例如 `/dev/lpd0` 或 `/dev/usb/lpd0`（如果你有 USB 打印机）。本地和远程打印机定义（称为打印队列）包含在系统的打印机能力数据库 `/etc/printcap` 中。此数据库中列出的每个打印机都将在 `/var/spool/lpd` 下有一个对应的打印队列缓存区，其名称为打印机名称。正在打印的文档被称为打印作业，你可以在缓存区目录中查看队列列表或当前打印作业的列表。

要向你的 Red Hat Linux 系统添加打印机，请使用 `redhat-config-printer` 客户端来创建、配置和定义打印机。该客户端将定义保存为系统打印机能力数据库 `/etc/printcap` 中的一个条目。每个定义包含一个指向 `/var/spool/lpd` 下相应命名缓存区的文本字段。此缓存区将保存等待打印的打印文档副本。

与缓存区一起，打印机的 `printcap` 列表包含一个指向 `/usr/share/printconf/mf/wrapper` 的条目。该文件是一个调用 `/usr/bin/magicfilter` 实用程序的脚本。

带有 `if:` 条目的示例打印机描述如下：
