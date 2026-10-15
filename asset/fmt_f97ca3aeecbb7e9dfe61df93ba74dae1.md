
# Red Hat Linux 7.1 精通指南

这是一份关于常用 Linux 命令的快速指南。书中包含了每个命令的语法大纲、重要的选项和标志，随后是关于该命令用途的描述。如需查阅所有命令的详细参考（包括选项和标志的说明），请参阅附录 C，“命令参考”。

### kill

```
kill [-s signal] -p pid
kill -t
```

`kill` 命令向一个或多个正在运行的进程发送信号。

## less

```
less [-aeEG1nrsS$]
```

`less` 命令一次显示一个文本文件，同时允许搜索和滚动。

## cat

```
cat [-bVETAE] [--number] [--number-nonblank] [--squeeze-blank] [--show-printing] [--show-ends] [--tabs] [--show-all] [...]
```

`cat` 命令合并一个或多个文件并在标准输出上显示它们。如果没有提供文件，默认则从标准输入读取。

## ln

```
ln [-bis] [--backup] [--interactive] [--symbolic] source [dest]
ln [-bis] [--backup] [--interactive] [--symbolic] source ...
```

`ln` 命令在文件之间建立链接。当指定了链接时，每个源会在指定的目录中创建一个同名的文件。

## chmod

```
chmod [-rcf] [--recursive] [--changes] [--silent] [--quiet] [--verbose] mode file...
```

`chmod` 命令更改一个或多个文件或目录的权限。

## chown

```
chown [-R] [--recursive] [--changes] [--silent] [--quiet] [owner] [::]group file...
```

`chown` 命令更改文件或目录的所有者和/或组。

## cp

```
cp [options] destination source ...
```

`cp` 命令复制文件和目录。

## lpq

```
lpq [-q] [-Pprinter] job ... [user]
```

`lpq` 命令检查并显示打印队列的当前状态。如果没有指定打印机，则查询默认打印机。查询的打印机中，普通作业是未签名的作业号。如果指定了用户，则仅显示该打印机上这些用户的打印作业。

## df

```
df [-T] -t ftype [-x ftype] [-all] [-inodes] [--ftype] [--exclude-ftype] [--print-type] [--filename...]
```

`df` 命令显示一个或多个磁盘或分区上的可用空间。如果没有指定文件（或目录），则显示所有挂载的文件系统。如果指定了文件名，则显示包含每个文件的所在文件系统的可用空间。

## lpr

`lpr` 命令将一个或多个文件打印到指定的打印机队列。如果没有指定打印机，则将标准输入发送到默认打印机。

## lp

```
lrm [-Pprinter] job ... [user]
```

`lrm` 命令从打印队列中删除一个或多个作业。如果没有指定打印机，它将尝试从默认打印队列中删除作业。如果指定了用户名，将删除该用户的所有作业（除非指定了特定的作业）。

## gunzip

```
gunzip [-f] [-stdout] [--stdout] [--force]
[-list] [--recursive] [--test] [name ...]
[-stdout] [--force] [--list] [--recursive] [--test]
name ...
```

`gunzip` 命令使用 `gzip` 命令（以及 `zip` 命令）解压缩文件。结果将替换原始压缩文件，并带有 `.gz` 扩展名。

## gzip

```
gzip [-cdflrt] [-decompress] [--uncompressed] [--stdout]
[--stdout] [--force] [--list] [--recursive] [--test]
name ...
```

`gzip` 命令使用 Lempel-Ziv 编码压缩文件。结果将替换原始压缩文件并带有。

## ls

```
ls [-acdlRsStux] [-al] [--time] [--status]
[--directory] [-format=long] [--format=verbose]
[--reverse] [-recursive] [-size] [--sort-sort]
[--time=atime] [--time] ...
```

`ls` 命令列出文件和目录。如果没有指定文件或目录，则显示当前目录的内容。默认按字母顺序排序。

## man

```
man command
```

`man` 命令显示指定命令的页面。

### mdltree

```
mdltree msdosdirectory [msdosdirectory ...]
```

`mdltree` 命令删除一个或多个 MS-DOS 目录。它类似于 DOS 的 DELETE 命令。

## mkdir

```
mkdir [-p] [-m] [--parents] [--mode=mode]
[--help] [--version] directory ...
```

`mkdir` 命令创建一个或多个目录。

## mount

```
mount [-a [-rw] [-t vfstype] [...] device dir
mount [-rw] [-t vfstype] [-o options] device dir
```

`mount` 命令将文件系统挂载到指定的目录。

### nlookup

```
nlookup [host | [server]]
```

`nlookup` 命令查询 DNS 服务器。它可以在交互模式下运行。如果没有提供主机，程序将进入交互模式。默认情况下，使用 `/etc/resolv.conf` 中指定的 DNS 服务器，除非另有指定。如果你想指定服务器但不查询目录，`nlookup` 在名称列表中提供。

## passwd

```
passwd [-S] [-d-list] [file...]
```

`passwd` 命令更改用户的密码。当由 root 用户运行时，可以通过提供用户名作为参数来更改特定用户的密码。

## ping

```
ping [-F] [-c number] [-i seconds]
[-s packets] host
```

`ping` 命令向网络主机发送回显包，以检查其在网络上是否可访问。

### ps

```
ps [username] [pid] ...
```

`ps` 显示当前运行进程的状态。通过给定特定的进程 ID 作为参数，`ps` 提供有关该进程的信息。在没有选项的情况下，`ps` 显示当前用户。

## pwd

```
pwd
```

`pwd` 命令显示当前目录的名称。

## rm

```
rm [-F] [--interactive] [--recursive] file ...
```

`rm` 命令删除一个或多个文件或目录。

## rmdir

```
rmdir [-p] [--parents] directory
```

`rmdir` 命令删除空目录。

## rsh

```
rsh [-l] username [command]
```

`rsh` 命令执行远程命令。

## su

```
su [-l] [-c]
```

`su` 命令切换用户身份。

## tar

```
tar [options] archivefile [file ...]
```

`tar` 命令用于创建、提取和维护归档文件。

## find

```
find [path ...] [expression]
```

`find` 命令在目录层次中搜索文件。

## grep

```
grep [options] pattern [file ...]
```

`grep` 命令在文件中搜索指定的模式。

## sed

```
sed [options] script [file ...]
```

`sed` 命令是一种流编辑器，用于文本转换。

## awk

```
awk [options] program [file ...]
```

`awk` 是一种强大的文本处理语言。

## sort

```
sort [options] [file ...]
```

`sort` 命令对文件内容进行排序。

## diff

```
diff [options] file1 file2
```

`diff` 命令比较两个文件之间的差异。

本图书及随附的任何其他当前或未来提供的材料均包含程序和/文本文件（以下简称“软件”），用于与本书结合使用。SYBEX 授予您使用该软件的许可，须遵循以下条款。您对软件的购买、接受或使用将构成您对此类条款的接受。

SYBEX 保证介质在购买后九十（90）天内无物理缺陷。SYBEX 不以书中附带或发布在 www.syex.com 上的其他形式或介质提供软件。如果您在保修期内发现介质有缺陷，您可以获得：

## 拷贝保护

软件的整体或部分可能未复制保护或加密。然而，在所有情况下，除非其中的所有者另有规定，否则严禁授权转售或重新分发这些文件。

致所有使用 GNU 和 Linux 帮助缩小数字鸿沟的人。

欲了解更多信息，请访问 www.digitaldividenetwork.org。

## 致谢

## 目录摘要

引言 xxii

索引 928

# 目录

引言 xxxii

- 什么是发行版？ 14

- 显示分区表 82

- 使用空空间添加分区 82

- 修改分区类型 83

- 删除分区 84

- 提交你的更改 84

- 展望 85

- 什么是 X Windows？ 90

- Xnumeric 190

- 复制和删除文件 330

- 日日志 414

- 展望 531

- 设置名称服务器 (DNS) 645

- Laser5 Linux 820

- Vine Linux 820

- 葡语版 Linux 821

- Conectiva Linux 821

- 俄罗斯版 Linux 821

- 西班牙语版 Linux 822

- Blue Linux 823

- Gelecek Linux 823

- S.u.S.E. Linux 826

- 附录：如何将这些条款应用于你的新程序 920

## E 非 Intel 硬件上的 Linux

- 针对 Compaq Alpha 处理器的 Linux 924

- 嵌入式 Linux 924

- 针对 Motorola 680x0 处理器的 Linux 925

- 针对 MIPS 处理器的 Linux 926

- 针对 Power Macintosh 的 Linux 926

- 针对 PowerPC 处理器的 Linux 927

- 针对 SPARC 处理器的 Linux 927

索引 928

## 引言

感谢购买本书，欢迎来到 Linux 世界。作为廉价桌面级个人电脑上微软操作系统的少数替代方案之一，Linux 已经声名远噪，并且最近获得了赞誉，成为一群充满动力的人员在没有任何财务激励的情况下所成就的典范。

Linux 是一个免费分发、高效且快速的操作系统，它将 Unix 的强大（曾是昂贵服务器和工作站的领域）带到了预算型家庭电脑用户负担得起的硬件上。这在计算机世界引发了一场小型革命，导致人们在广泛的任务中接受免费软件——从任务关键的 Web 网站、创建信息系统基础设施到教育应用程序。

本书旨在介绍基于 Red Hat Linux 7.1 的 Linux 安装和使用。Red Hat Linux 7.1 是一个被广泛使用的 Linux 版本，非常适用于服务器系统，以及 Linux 工作站和桌面电脑。任何提供像 Linux 这样广泛功能和能力的操作系统都无法在一本书中完全涵盖。尽管如此，本书仍提供了用户所需的坚实 Linux（特别是 Red Hat）知识，让用户在日常工作中使用 Linux 时，能够继续并自主学习更多知识。

## 谁应该读这本书？

本书实际上是为任何使用 PC 的人设计的。虽然 Linux 可能没有像 Windows 95/98 和 Mac OS 等商业桌面操作系统那样的所有易用性改进，但几乎任何人都可以使用 Linux，并且任何精通 Windows 的人都能掌握它。

尽管如此，如果你已经具备了一些基础计算机知识，学习使用任何操作系统总是更容易的，包括理解硬盘和内存（RAM）之间的区别，理解外设（在 Windows 中）显卡和声卡的基本配置，以及对计算机如何组织和存储数据的感知（例如目录、子目录和文件之间的区别）。

本书旨在为普通计算机用户开启 Linux 的世界。在此，我们假设读者对 Windows（或 Mac OS）和基础 PC 硬件有一定程度的熟悉。如果没有这一假设，本书将成为基础计算概念的入门读物，而不是对 Linux 操作系统的实实介绍。

如果你已经熟练使用 Windows 或 Macintosh 系统，并且还没有尝试过 DOS 提示符，那么深入探索 Linux 世界将会有帮助，在那里，命令行比 Windows 区域更强大，因此使用得更频繁。

如果你已经是 Windows 的高级用户，那么你已经准备好成为 Linux 的高级用户了。正如本书将让普通计算机用户熟练使用 Linux 完成工作一样，它也将帮助你成为一名高级 Linux 用户。

本书对于 SO（小型办公室/家庭办公室）用户或小型网络管理员也有一些东西可读。你将学习如何在办公室环境的许多情况下使用 Linux，涵盖的角色包括文件服务器、内网 Web 服务器和路由器。

## 使用本书具备的条件

要使用本书，你需要一台具有上述最低配置的个人计算机：

- 奔腾（Pentium）CPU 或更高型号（从理论上讲，你可以在 386 系统上运行 Linux，但性能可能足够糟糕，对大多数用户来说不值得尝试。）

- 32MB 或更多内存（RAM）（你会发现 Linux 在拥有 64MB 或更多内存时，性能会有显著提升。）

- 具有至少 1GB 空闲磁盘空间的硬盘；对于工作站或笔记本电脑配置需要 1.5GB（如果你能负担得起 3GB 或更多，这将极大增强你实验 Linux 及 Linux 应用程序的自由。）

## 简介

- CD-ROM 驱动器（优选 ATAPI/IDE CD-ROM 或 SCSI CD-ROM 驱动器）

- 你当前系统的备份，以防你需要恢复现有数据或程序

- 显卡和 VGA 或更高规格显示器

- 键盘和鼠标

你可能还想要准备以下选项：

- 打印机（如果有选择，请选择 PCL 或 PostScript 打印机）

- 声卡扬声器

- 电话调制解调器、ISDN 调制解调器或其他高速连接

## 本书结构

本书分为七部分：

**欢迎来到 Linux** 这一部分向你介绍作为操作系统的以及 GNU 通用公共许可证软件模型基础的 Linux。它介绍了最流行的 Linux 发行版（版本），并帮助你安装 Linux 做准备。

**安装 Red Hat Linux 7.1** 这一部分涵盖了独立 Linux 系统的安装。它包含了如何安装 Linux 以及特殊安装（如无 CD-ROM 的系统）。

**在 Red Hat Linux 7.1 中使用桌面环境** 这一部分介绍了带有 GNOME 桌面管理器（Red Hat Linux 标准 GUI）的 X Windows 使用。该讨论包括对某些 Windows 应用程序的概述。

**精通要素** 这一部分描述了真正精通 Linux 所需的一系列基本技能。涵盖的内容包括文件管理、系统配置以及打印机和其他设备。

**基础连接** 这一部分解释了如何使用拨号连接将 Linux 系统连接到互联网。涵盖的内容包括访问万维网和处理电子邮件。

**在小型办公室/家庭办公室 (SOHO) 中使用 Linux** 作为一种廉价且强大的计算环境，Linux 非常适合许多小型办公室任务。这一部分介绍了在网络环境中安装 Red Hat Linux 7.1，以及将 Linux 作为 Unix 和 Windows 网络的文件或打印服务器的使用，这将使你意识到在网络环境中使用 Linux 的基本安全问题。最后，本部分检查了 Linux 中 DOS 和 Windows 的兼容性和集成，这使得许多组织能够在不放弃现有软件和应用程序投资的情况下从 Windows 环境迁移到 Linux。

**Red Hat Linux 7.1 作为 Web 和电子邮件服务器** 除了是 SOHO 的理想文件和打印服务器外，Linux 还可以用于创建强大的企业级 Web 和邮件服务器。这一部分描述了如何设置基于 Linux 的 Web 和邮件服务器。

# 第一章

## 什么是 Linux？

- Linux 历史

- 作为操作系统的 Linux

- 作为自由软件的 Linux

- Linux 的商业应用

如果你已经读到了这里——购买了这本书，翻阅了前言并看了目录——那么你可能对 Linux 以及 Linux 现象已经有了初步了解。如果你还不了解，请继续读下去。

Linux 是计算机领域中一个真正令人惊叹的发展。它表明，优质软件并不一定依赖于商业软件行业的资金扶持。Linux 的历史说明了自由软件如何演变、成长，并成为你们大多数人所熟悉的商业软件软件包极具吸引力的替代方案。

此外，Linux 的技术卓越性展示了为什么它能成为微软、苹果、诺瓦尔（Novell）和 IBM 等竞争操作系统的强有力竞争者。由于它还能处理高需求应用程序，因此对于大型企业而言，它也是 Solaris、HP-UX 和 SCO-Unix 等竞争性 Unix 派生操作系统的强有力竞争者。

本章简要概述了 Linux 的历史，然后介绍了让 Linux 成为适用于各种技术应用的强大操作系统的关键特性。最后，本章将探讨自由软件模型，并分析了它对整个软件行业的影响。

## Linux 历史
