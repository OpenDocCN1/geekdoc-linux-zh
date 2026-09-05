
# Red Hat Enterprise Linux 9 核心指南

## 1. 引言

毫无疑问，当今最受推崇和广泛使用的企业级操作系统之一是红帽企业 Linux（通常缩短为 `RHEL`，发音为 `rell`）发行。它不仅被认为是最稳定、可靠的操作系统之一，而且得到了红帽公司（Red Hat, Inc.）大量的资源和技术支持。《红帽企业 Linux 9 核心教程》旨在提供有关红帽企业 Linux 9 发版安装、使用和管理的详细信息。对于初学者，本书涵盖了操作系统安装、`GNOME` 桌面环境基础知识、配置电子邮件和 Web 服务器以及使用 `App Streams` 安装软件包和系统更新等主题。此外还涵盖了如与 Microsoft Windows 双引导等其他安装主题，以及所有重要的安全主题，如配置防火墙以及用户和组管理。

对于经验丰富的用户，书中还详细介绍了远程桌面访问、`Cockpit` Web 界面、逻辑卷管理（`LVM`）、磁盘分区、交换空间管理、KVM 虚拟化、安全外壳（`SSH`）、Linux 容器以及使用 Samba 和 NFS 进行文件共享，以提供对这一企业级操作系统的全面概述。

### 1.1 超级用户规范

RHEL 9 与通用 Linux 一样有两种类型的用户账户：一种是标准用户账户，对操作系统的许多管理文件和功能的访问受限；另一种是具有提升权的超级用户（`root`）账户。通常情况下，用户可以通过登录 `root` 用户或使用 `su -` 命令并输入 `root` 密码获取 `root` 权限。在下面的示例中，用户通过 `su -` 命令获取 `root` 权限：

```
[neil@demo-server ~]$ su -
Password:
[root@demo-server ~]#
```

注意，普通用户的命令提示符以 `$` 符号结尾，而 `root` 用户则是 `#` 字符。在命令行操作时，这是判断你当前是否以 `root` 用户身份发布命令的有用指示。

如果 `su -` 命令失败，系统上的 `root` 账户可能出于安全原因被禁用。在这种情况下，可以使用下述的 `sudo` 命令。

使用 `sudo`，非 `root` 用户可以执行需要 `root` 权限的单个命令。考虑以下使用最新补丁和软件包更新操作系统的尝试：

```
[neil@demo-server ~]$ dnf update
Not root, Subscription Management repositories not updated
Error: This command has to be run under the root user.
```

可选，可以配置用户账户使其拥有 `root` 级权限。无需使用 `su -` 命令先获取 `root` 权限，具有管理权限的用户账户可以使用 `sudo` 运行原本受限的命令：

```
[neil@demo-server]$ sudo dnf update
```

我们相信你已经听过本地系统管理员的常规教育。这通常归结为以下三点：

1. 尊重他人的隐私。
2. 在输入之前先思考。
3. 能力越大，责任越大。

```
[sudo] password for neil:
```

执行多项任务时请使用 `sudo`。对于任何问题，示例如下：

```
[neil@demo-server]$ sudo -
```

### 1.2 打开终端窗口

如果你正在使用 `GNOME` 桌面并需要访问 `Terminal`（终端），要执行此操作，可以按下 `Super` 键或点击屏幕左上角的 `Activities`（活动）按钮，然后如图 1 所示选择 `Terminal`：

![](img/gnome_terminal_in_dock.png)

图 1-1

### 1.3 编辑文件

配置 Linux 系统通常涉及编辑文件。对于 Linux 新手来说，由于没有首选编辑器，我们建议使用 `nano` 编辑器。在终端中启动 `nano` 只需输入以下命令：

```
# nano <file>
```

其中 `<file>` 替换为编辑的文件路径。例如：

```
# nano /etc/passwd
```

一旦加载，`nano` 将如图 2 所示出现：

![](img/ubuntu_18.04_nano.png)

图 1-2

创建新文件只需运行：

```bash
# nano
```

当你完成文件编辑后，输入 `Ctrl+S` 保存文件，然后按 `Ctrl+X` 退出。要打开现有文件，请使用键盘快捷键 `Ctrl+R`。

如果你喜欢在 `GNOME` 环境中使用图形化编辑器，`gedit` 是执行基础编辑任务的良好起点。要从桌面启动 `gedit`，按下 `Alt+F2` 显示如图 3 所示的命令窗口：

![](img/gnome_run_command.png)

图 1-3

在文本框中输入 `gedit` 并按回车键。稍后，`gedit` 将加载并准备好打开、创建和编辑文件：

![](img/gnome_gedit.png)

图 1-4

或者，也可以从终端窗口启动 `gedit`，无论带不带打开的文件路径：

```bash
# gedit
# gedit /etc/passwd
```

### 1.4 反馈

我们希望你对购买本书满意。如果你在书中发现任何错误，或有任何意见、问题或担忧，请通过邮件联系我们：`feedback@ebookfrenzy.com`。

### 1.5 勘误

虽然我们尽力确保内容的准确性，但涵盖如此规模和复杂领域的书籍，不可避免包含某些错误和遗漏。书中任何已知问题将同解决方案一起列在以下 URL：

`https://www.ebookfrenzy.com/errata/rhel9.html`

如果你发现了勘误列表中未列出的错误，请通过电子邮件告知我们的支持团队：`feedback@ebookfrenzy.com`。

## 2. 红帽 Linux 简史

红帽企业 Linux（Red Hat Enterprise Linux）是 Linux 操作系统的多种变体（也称为发行版）之一，是由总部位于美国卡罗来纳州罗利市的红帽公司（Red Hat, Inc.）的产品。该公司成立于 20 世纪 90 年代中期，由当时由 Marc Ewing 和 Bob Young 拥有的两个公司合并而成立。然而，Linux 的起源可以追溯到更早的时期。本章将简述 Linux 操作系统和红帽公司的历史。

### 2.1 到底什么是 Linux？

Linux 是一个操作系统，就像 Windows 是一个操作系统一样（尽管 Linux 和 Windows 之间存在许多相似之处）。“操作系统”一词用于描述在计算机硬件与我们日常运行的应用程序之间充当中间层的软件。当程序员编写应用程序时，他们与操作系统交互以执行诸如将文件写入硬盘和在屏幕上显示信息等任务。如果没有操作系统，每位程序员都必须编写代码来直接访问系统的硬件。此外，程序员必须能够支持曾经创建过的每一件硬件，以确保应用程序能够在任何硬件配置上运行。由于操作系统处理了所有这些硬件复杂性，应用程序开发变成了一项简单得多的任务。Linux 只是现今许多不同操作系统之一。

### 2.2 UNIX 的起源

要理解 Linux 的历史，我们首先必须追溯 20 世纪 60 年代后期的 AT&T 贝尔实验室。当时，AT&T 停止了名为 Multics 的新操作系统的开发。然而，两位 AT&T 工程师 Ken Thompson 和 Dennis Ritchie 决定将他们在 Multics 项目中学到的知识结合，创建一个名为 UNIX 的新操作系统，该系统迅速在企业和学术机构中流行起来并被广泛采用。

各种专有的 UNIX 实现陆续上市，包括由 IBM（`AIX`）、惠尔罗-普惠（`HP-UX`）和太阳微系统（`SunOS` 和 `Solaris`）创建的版本。此外，Andrew S. Tanenbaum 创建了一个名为 `MINIX` 的类 UNIX 操作系统，专为教学用途设计，并向大学提供源代码。

### 2.3 谁创建了 Linux？

Linux 的起源可以追溯到两个人的工作和哲学。Linux 操作系统的核心是被称为“内核”（kernel）的东西。这是操作系统运行所需的核心功能集。内核管理系统资源，并处理硬件与应用程序之间的通信。Linux 内核由 Linus Torvalds 开发，由于不喜欢 `MS-DOS`，并且对 `MINIX` 在新的 Intel 80386 微处理器上的可用性等待感到不耐烦，他决定编写自己的类 UNIX 内核。当他完成内核的第一版本时，他以开源许可发布了它，允许任何人下载源代码并自由使用和修改它，而无需向 Linus 支付费用。

大约同一时间，自由软件基金会（Free Software Foundation）的 Richard Stallman（自由和开源软件的坚定拥护者）正在开发他自己的开源操作系统。然而，Stallman 最初并没有专注于内核，而是从开发使用和维护操作系统所需的所有 UNIX 工具、实用程序和编译器的开源版本开始。当他完成这些基础设施的开发后，显而易见的解决方案是将他的工作与 Linus 编写的内核相结合，创建一个完整的操作系统。这种组合被称为 `GNU/Linux`。纯主义者坚持认为 Linux 应该始终被称为 `GNU/Linux`（事实上，曾有一段时间，Richard Stallman 拒绝接受任何不将 Linux 称为 `GNU/Linux` 的出版物的媒体采访）。鉴于自由软件基金会开发的 GNU 工具构成了 `GNU/Linux` 很大且至关重要的部分，这并不是没有道理。遗憾的是，大多数人和出版物简单地将 Linux 称为 Linux，这种情况可能会一直持续。

### 2.4 红帽的早期

1993 年，Bob Young 创建了一家名为 `ACC Corporation` 的公司，根据 Young 的说法，他在“妻子的缝纫衣橱”经营这家公司。`ACC` 这个名字本意代表目录业务，也是他妻子经营的一家名为“Antiques and Collectibles of Connecticut”的小型企业的缩写。通过 `ACC` 目录业务销售的物品包括 Linux 光盘和相关的开源软件。

大约同一时间，Marc Ewing 创建了自己的 Linux 发行版公司，并将其命名为红帽 Linux（源自他在卡内基·梅隆大学学习期间喜欢戴红色棒球帽）。

1995 年，`ACC` 收购了红帽，采用了 Red Hat, Inc. 的名称，并经历了快速且巨大的增长。Bob Young 在公司于 1999 年 8 月上市后不久就辞去了 CEO 职位，从那以后从事了许多商业和慈善活动，包括经营一家名为 `Lulu` 的按需图书出版公司以及拥有两支加拿大职业运动队。2018 年，IBM 以 340 亿美元的交易价值收购了 Red Hat, Inc.。

### 2.5 红帽支持

早期的红帽 Linux 通过软盘和 CD 交付给客户（当然，这早于宽带互联网连接的广泛普及）。当用户在使用软件时遇到问题时，他们只能通过电子邮件联系红帽。事实上，Bob Young 经常开玩笑说，这对于限制支持请求非常有效，因为当客户意识到他们需要帮助时，他们的计算机通常无法运行，因此无法用它发送电子邮件向红帽支持团队寻求帮助。在随后的几年里，红帽提供了与付费订阅挂钩的更高级别，现在提供了从“自救”（无支持）到高级支持的各种支持级别。

### 2.6 开源

红帽企业 Linux 9 版（Red Hat Enterprise Linux 9）是红帽目前的商业产品，主要针对企业级、任务关键型部署。它也是红帽提供的不断扩展的产品和服务生态系统的基石。RHEL 是一个开源产品，因为如果你愿意，可以免费下载源代码并自己构建软件（这项任务并非轻而易举）。然而，如果你想下载预构建的、现成的即可安装的二进制版本（无论是否带支持），你就必须付费。

### 2.7 Fedora 项目

红帽还赞助 Fedora 项目（Fedora Project），其目标是以 Fedora Linux 的形式提供免费的 Linux 操作系统（包括源码版和二进制发行版）。Fedora Linux 还是许多新功能的试验场，这些功能最终会被采纳到红帽企业 Linux 操作系统族和 CentOS 衍生版中。

### 2.8 CentOS Stream——免费替代方案

对于无法负担红帽企业 Linux 订阅的用户，另一个选择是 CentOS Stream 操作系统。CentOS 项目最初是一个社区驱动的努力，但现在由红帽拥有，它获取红帽企业 Linux 的源代码，移除红帽标识和订阅要求，进行编译并提供发行版供下载。与 Fedora 类似，CentOS Stream 在新的操作系统功能包含在未来的 RHEL 版本之前对其进行现场测试。因此，它可能缺乏稳定性，但提供了获取前沿功能的机会。

### 2.9 总结

Linux 操作系统的起源可以追溯到 Linus Torvalds 和 Richard Stallman 的工作，形式为 Linux 内核结合 GNU 项目构建的工具和编译器。

多年来，Linux 的开源特性导致了各种不同 Linux 发行版的发布。其中一种就是红帽企业 Linux（Red Hat Enterprise Linux），它由 Bob Young 和 Mark Ewing 的 Red Hat 公司创建。红帽公司致力于提供企业级的 Linux 软件解决方案，并结合广泛的技术支持服务。

## 3. 在空白磁盘驱动器上安装 RHEL 9

现在有两种部署 RHEL 9 系统的方法。一种方法是购买新硬件，或者重新利用现有的计算机系统以在上面安装和运行操作系统。另一种选择是使用 Amazon AWS、Google Cloud 或 Microsoft Azure（仅列举几个）等服务创建云端操作系统实例。由于云实例通常是通过选择一个预配置、即插即用、且已针对云平台进行优化的操作系统镜像，并以此作为 RHEL 系统的基础创建的，因此在这种情况下无需执行手动安装操作系统。

另一方面，如果你计划在自己的硬件上安装 RHEL 9，那么学习红帽企业 Linux 9 道路上的第一步就涉及安装该操作系统。

RHEL 可以安装在空白磁盘环境中（清除整个磁盘上的所有现有分区并将其完全用于 RHEL），也可以安装在双启动环境中（RHEL 与磁盘上的另一个操作系统共存，通常是 Microsoft Windows 家族的成员）。

本章将介绍从本地或远程安装介质进行空白磁盘安装的方法。与 Windows 11 系统的双启动安装将在“在 Windows 上双启动 RHEL 9”中进行介绍。

### 3.1 获取 RHEL 9 安装介质

虽然 RHEL 是一个开源操作系统，因此源代码是可以免费访问的，但二进制安装镜像仅作为付费红帽企业 Linux 订阅的一部分提供。除了访问 RHEL 的安装镜像外，还有不同级别的订阅可以为该操作系统提供技术支持。如果你已经拥有了付费订阅，请登录你的红帽账户下载操作系统。如果你想在购买之前尝试 RHEL，红帽提供了 30 天的试用期。要注册试用版，请访问以下地址的红帽网站：

`https://www.redhat.com/en/technologies/linux-platforms/enterprise-linux/try-it`

红帽开发者计划成员也可以获得 RHEL 9。加入该计划的详情可以在红帽开发者网站 `https://developers.redhat.com` 上找到。

RHEL 9 支持 Intel 64 位（`x86_64`）和 ARM64（`AArch64`）CPU 架构族。可以下载每种架构的 DVD 或启动 ISO 镜像。DVD ISO 镜像是自包含的，包含了安装 RHEL 系统所需的所有包，其命名规范如下：

`rhel-baseos-<version>-<architecture>-dvd.iso`

例如，适用于 64 位 Intel 系统的 RHEL 9.1 DVD 镜像命名如下：

`rhel-baseos-9.1-x86_64-dvd.iso`

另一方面，启动 ISO 镜像仅包含开始安装所需的文件，并且访问远程服务器上的完整安装介质。启动镜像还可以对现有的 RHEL 系统执行救援操作。启动 ISO 的命名规范如下：

`rhel-baseos-<version>-<architecture>-boot.iso`

例如，适用于 AArch64 的 RHEL 9.1 启动镜像命名如下：

`rhel-baseos-9.1-x86_64-boot.iso`

下载镜像后，可以将其刻录到磁盘，或使用下一节中的步骤将介质写入 USB 闪盘，配置你的虚拟化环境将其视为 DVD 驱动器，或者使用本章后面概述的步骤通过网络连接访问安装镜像。

### 3.2 将 ISO 安装镜像写入 USB 闪盘

如今，从 USB 闪盘执行操作系统安装比从 DVD 更常见。在下载了 RHEL 9 的 ISO 安装镜像后，将镜像写入 USB 闪盘的步骤取决于该驱动器连接到 Linux、macOS 还是 Windows 系统。本节剩余部分的步骤假设 USB 闪盘是新的，或者已经重新格式化以删除任何现有数据或分区。

#### 3.2.1 Linux

在 Linux 上向 USB 闪盘写入 ISO 镜像的第一步是识别设备名称。在插入 USB 闪盘之前，通过列出 `/dev` 中的设备来识别系统已检测到的存储设备：

```bash
ls /dev/sd*
```

```text
/dev/sda /dev/sda1 /dev/sda2
```

将 USB 闪盘连接到 Linux 系统并运行 `dmesg` 命令获取最近系统消息列表，其中一个将是检测到 USB 闪盘的报告，类似于以下：

```
[ 406.241717] sd 6:0:0:0: [sdb] Attached SCSI removable disk
```

此输出告诉我们应该预期设备名称包含“sdb”，我们可以通过再次列出 `/dev` 中的设备名称来确认这一点：

```bash
ls /dev/sd*
```

```text
/dev/sda /dev/sda1 /dev/sda2
```

此输出显示 USB 闪盘已被分配给 `sdb`。在写入 ISO 镜像之前的下一步，是再次列出 `/dev` 中的设备名称以确认：

```bash
ls /dev/sd*
```

```text
/dev/sda /dev/sda1 /dev/sda2
```



此输出显示 USB 闪盘已分配到 `sdb`。在向设备写入 ISO 之前，运行 `findmnt` 命令检查它是否已挂载：

```bash
findmnt /dev/sdb
```

如果 `findmnt` 命令显示该设备已挂载，在继续之前请卸载它：

```bash
umount /run/media/neil/d6bf9574-e31-4f5c
```

使用以下 `dd` 命令写入镜像：

```bash
dd if=/path/to/image of=/dev/sdb bs=512
```

写入过程可能需要一些时间（取决于镜像大小和速度）。完成后，会出现类似下面的输出，且 USB 闪盘已准备好安装 RHEL：

```
5956+0 records in
5956+0 records out
```

### 3.2.2 macOS

在 macOS 系统上向连接的 USB 闪盘上写入 ISO 镜像的第一步是使用 `diskutil` 工具识别设备。在连接 USB 设备之前，打开终端（Terminal）窗口并运行以下命令：

```bash
diskutil list
```

```
/dev/disk0 (internal, physical):
  # TYPE NAME IDENTIFIER
  0: GUID_partition_scheme *1.0 TB disk0
  1: EFI 209.7 MB disk0s1
  2: Apple_APFS Container disk2 1000.0 GB disk0s2
/dev/disk1 (internal):
  # TYPE NAME IDENTIFIER
  0: GUID_partition_scheme 28.0 GB disk1
  1: EFI 314.6 MB disk1s1
  2: Apple_APFS Container disk2 27.7 GB disk1s2
/dev/disk2 (synthesized):
  # TYPE NAME IDENTIFIER
  0: APFS Container Scheme -1.0 TB disk2
      Physical Stores disk1s2, disk0s2
  1: APFS Volume Macintosh HD 473.6 GB disk2s1
  2: APFS Volume Preboot 42.1 MB disk2s2
  3: APFS Volume Recovery 517.0 MB disk2s3
  4: APFS Volume VM 1.1 GB disk2s4
/dev/disk3 (external, physical):
  # TYPE NAME IDENTIFIER
  0: *16.0 GB disk3
```

在上述示例中，USB 闪盘已被分配给 `/dev/disk3`。在继续之前，按以下命令卸载磁盘：

```bash
diskutil unmountDisk /dev/disk3
```

```
Unmount of all volumes on disk3 was successful
```

最后，使用 `dd` 命令将 ISO 镜像写入设备，请注意引用原始磁盘设备（`/dev/rdisk3`），并在提示时输入你的用户密码：

```bash
sudo dd if=/path/to/iso/image.iso of=/dev/rdisk3 bs=1m
```

一旦镜像写入完成后，USB 驱动器即准备就绪。

### 3.2.3 Windows/macOS

Windows 和 macOS 提供了多种免费工具可以将 ISO 镜像写入 USB 驱动器，但一个专门为写入 Linux ISO 镜像而编写的工具是 Fedora Media Writer，您可以从以下 URL 下载：

[`getfedora.org/en/workstation/download/`](https://getfedora.org/en/workstation/download/)

安装后，插入目标 USB 驱动器，启动写入工具，并选择如图 3-1 所示的 `Select .iso file` 选项：

![](img/fedora_media_writer.png)

图 3-1

点击“Next”（下一步）进入“写入选项”屏幕，并在点击 `Select...` 按钮之前选择 USB 驱动器：

![](img/fedora_media_writer_write_options.png)

图 3-2

在弹出的文件选择对话框中，导航并选择 RHEL 9 安装 ISO 镜像，然后点击 `Open`（打开）按钮。最后，点击 `Write`（写入）按钮开始将镜像写入 USB 驱动器：

![](img/fedora_media_writer_writing.png)

图 3-3

一旦镜像写入设备，该设备即已准备好执行安装。

## 3.3 安装 Red Hat Enterprise Linux 9

将 RHEL 9 安装介质插入相应的驱动器并启动系统。如果系统尝试从硬盘启动，您将需要进入计算机的 BIOS 设置并更改启动顺序，使其首先从安装介质驱动器启动。一旦系统启动，您将看到以下屏幕：

![](img/rhel9_install_boot_menu.png)

图 3-4

使用方向键在各个选项之间导航，并使用 `<Enter>` 键进行选择。例如，如果选择了 `Troubleshooting`（故障排除）选项，将出现如图 3-5 所示的屏幕，其中包含从本地驱动器上的当前操作系统（如果已安装）启动、测试系统内存或救援已安装的 RHEL 9 系统的选项。还有一个选项可用于在没有图形控制台的系统上以基础图形模式进行安装：

![](img/rhel9_install_troubleshooting_menu.png)

图 3-5

如果您安装的是 ARM64 镜像，则故障排除屏幕上可能没有从本地驱动器启动和运行内存测试的选项。

在主屏幕上选择安装 Red Hat Enterprise Linux 的选项，稍等后，将出现图形化安装程序的第一个屏幕：

![](img/rhel9_install_choose_language.png)

图 3-6

在第一个屏幕上选择您偏好的语言，然后点击 `Continue`（继续）进入如图 3-7 所示的主安装屏幕：

![](img/rhel9_install_summary.png)

图 3-7

首先选择 `Network & Host Name`（网络和主机名）选项，在系统上启用网络设备，并在点击 `Apply`（应用）按钮之前输入主机名：

![](img/rhel9_install_network.png)

图 3-8

如果您的网络连接需要额外设置，点击 `Configure...`（配置...）按钮访问如图 3-9 所示的高级网络设置屏幕：

![](img/rhel9_install_network_configure.png)

图 3-9

一旦定义了主机名并启用了网络连接，点击 `Done`（完成）返回主屏幕。

如果您想更改键盘、语言或时间和日期设置，请从主屏幕的“Localization”（本地化）列中选择相应的选项。在 `Time & Date`（时间和日期）屏幕上，选择与您的地理位置相应的选项。还提供了使用 `Network Time`（网络时间）的选项，它可以自动与外部网络时间协议服务器同步。

由于安装是从本地介质进行的，因此不需要更改 `Installation Source`（安装源）设置。要完成来自远程服务器上介质的安装，请选择 `Installation Source`，启用 `On the network`（在网上）选项，然后指定安装介质的位置和所使用的 URL 类型。例如，安装介质可以是安装在远程 Web 服务器上的 ISO 镜像，也可以是本地网络上使用 `NFS` 的系统（NFS 文件共享主题将在“在 RHEL 9 上使用 NFS 与远程系统共享文件”章节中详细介绍），或者是远程存储库的 URL（存储库本质上是组成操作系统的软件、软件包和应用程序的在线集合，可以从中在本地系统上进行安装）。

默认情况下，安装程序将对 RHEL 9 执行 `Server with GUI`（带 GUI 的服务器）安装。这将包含运行操作系统和图形桌面环境所需的最少软件包。要选择不同的安装配置，选择 `Software Selection`（软件选择）选项以显示所示屏幕：

![](img/rhel_8_installation_software_selection.png)

图 3-10

使用左侧面板选择基础配置，使用右侧面板添加您系统启动后需要的任何软件包。如果不需要桌面环境且不确定安装哪些软件包，请使用 `Minimal install`（最小安装）选项，并在系统启动后按需安装。这避免了安装任何可能永远需要的软件包。

`Security Policy`（安全策略）选项允许在系统中安装额外的安全软件包，以便实施符合安全自动化协议（SCAP）标准的限制。虽然从列表中选择配置文件会安装必要的软件包，但策略限制在运行系统中启用之前不会生效。除非您在要求此类安全级别的实体或公司，否则在此屏幕上选择策略是可选的。

`Kdump` 功能启用后会在系统崩溃时输出操作系统内核的状态。此转储文件有助于识别崩溃原因，但在启用时会占用内存。除非您的系统内存有限，否则可以保持开启状态。

配置好基本设置的下一步是决定如何对硬盘进行分区以适应操作系统。

## 3.4 为 RHEL 9 分区

当选择 `Installation Destination`（安装目标）选项时，安装程序将显示一个类似于图 3-11 所示的屏幕：

![](img/rhel9_install_destination.png)

图 3-11

默认情况下，安装程序配置为使用当前选择磁盘驱动器的可用空间自动安装操作系统，并配置标准分区大小。如果磁盘之前包含另一个操作系统，这些现有的分区将不会被删除，这可能会在 RHEL 9 安装后驱动器上留下未使用的空间。要删除任何现有分区以便 RHEL 9 回收并使用，请启用 `I would like to make additional space available`（我想提供更多可用空间）选项并点击 `Done`（完成）按钮显示如图 3-12 所示的对话框：

![](img/rhel9_install_reclaim_space.png)

图 3-12

要回收空间，请选择一个不再需要的分区，并点击 `Delete` 按钮将其标记为删除。一旦选取了所有要删除的分区，点击 `Reclaim Space` 按钮执行删除。回收的空间现在将由 RHEL 9 安装程序自动使用。

若要根据可用空间的分配方式手动配置磁盘布局，请将 `Storage Allocation` 设置从 `Automatic` 更改为 `Custom`，并点击 `Done` 显示 `Manual Partitioning`（手动分区）界面（图 3-13）：

![](img/rhel9_install_partitioning.png)

图 3-13

手动分区界面允许使用逻辑卷管理（`LVM`）或标准分区来配置磁盘。`LVM` 是推荐的选项，因为它在系统运行后提供了管理分区大小的灵活性（有关 LVM 的细节将在“向 RHEL 9 卷组和逻辑卷中添加新磁盘”章节中进行详细介绍）。

一旦选定了分区方案，最后一步是确定分区大小以及相应的文件系统挂载点。通常情况下，`Click here to create them automatically` 选项提供的默认配置可以满足大多数系统需求。然而，若要手动创建分区并分配挂载点，请点击 `+` 按钮手动声明并分配分区。

另一个选项是选择自动创建分区，然后使用生成的界面根据需要手动更改分区配置。例如，图 3-14 显示了选择自动创建选项定义的分区配置，并允许在对磁盘进行任何更改之前修改每个分区的设置：

![](img/rhel9_install_automatic_partions.png)

图 3-14

磁盘配置好后，点击 `Done`，检查对磁盘所做的更改摘要（图 3-15），然后点击 `Accept Changes` 按钮：

![](img/rhel9_install_partion_summary.png)

图 3-15

### 3.5 磁盘加密

RHEL 9 还允许通过加密保护磁盘内容。这需要在每次系统启动时输入密码。要启用加密，在主 Installation Destination（安装目标）屏幕上选择 `Encrypt my data` 选项，点击 `Done` 按钮后，在图 3-16 显示的对话框中输入密码：

![](img/rhel_8_installation_disk_encryption.png)

图 3-16

### 3.6 用户设置

在完成安装之前，你必须创建一个 root 密码和一个可选的用户账户。root（或超级用户）是具有系统管理权限的特殊用户。虽然你通常会使用自己的账户登录系统，但你需要 root 权限来配置系统并执行其他管理任务。

选择 `Root Password` 选项并输入一个足够安全的密码。还有选项可以锁定 root 账户使其无法访问，以及允许通过密码认证远程连接到系统并访问 root 账户。通常，建议保持 root 账户未锁定状态，但不允许使用密码进行远程 SSH 访问。如果需要远程 root 访问，应使用 SSH 密钥身份验证来实现，该主题将在本书的“在 RHEL 9 上配置 SSH 密钥身份验证”章节中介绍。

接下来，选择 `User Creation` 选项并输入用户名和密码。如果你希望此用户能够使用 `sudo` 命令执行管理任务，请也勾选 `Make this user administrator` 复选框。如果未启用此选项，用户必须使用 `su` 命令并输入 root 密码来获得 root 权限（假设上述锁定 root 账户的选项未启用）。如果你添加的用户需要执行管理任务，`sudo` 是推荐选项，应当启用该复选框。

### 3.7 注册系统

安装过程完成后且系统运行时，在进行任何更新或安装额外软件包之前，必须向 Red Hat 注册系统。在编写本文时，在不先注册的情况下安装 ARM64 版本的 RHEL 9 是可能的，但 X86_64 版本要求在安装前注册。要注册系统，选择 `Connect to Red Hat` 选项，根据你获取 RHEL 许可的方式选择 `Account` 或 `Activation key` 选项。输入信息后，点击 `Register` 按钮完成注册过程。

### 3.8 物理安装

在选择了适当软件包后，点击 `Begin Installation` 将开始分区磁盘并安装与所选安装设置匹配的软件包。在此阶段，将显示图 3-17 所示安装进度屏幕：

![](img/rhel9_installing.png)

图 3-17

所有系统软件包安装并配置完成后，移除安装媒体并点击 `Reboot System` 重启系统。

### 3.9 最终配置步骤

系统启动时控制台上显示的内容取决于在软件选择安装屏幕上选择了 `Workstation`（工作站）还是 `Server with GUI`（带 GUI 的服务器）选项。如果在安装期间选择了这些选项之一，将出现 GNOME 显示管理器（`GDM`）登录界面。相反，如果选择了最小或服务器配置，将显示文本登录提示符。无论何种配置，请使用安装过程期间创建的用户登录系统。

对于 Workstation 或 Server with GUI 安装，GNOME 初始化设置工具将启动并提供桌面环境的引导。

如果你在启动安装前没有注册系统，可以在命令行提示符或桌面环境下终端窗口中进行。要在桌面启动终端会话，点击菜单栏中的 `Activities`，然后点击屏幕底部的面板上的 `Terminal` 图标，如图 3-18 所示：

![](img/rhel9_terminal_icon.png)

图 3-18

在提示符处，使用 `sudo` 命令获取 root 权限并输入你的用户密码：

```bash
sudo su -
```

接下来，使用 `subscription-manager` 工具向 Red Hat 注册系统，并在提示输入你的 Red Hat Access 用户名和密码：

```bash
subscription-manager register
```

```
Registering to: subscription.rhsm.redhat.com:443/subscription

Username: myusername

Password:

系统已注册，ID 为：22f0ca3f-8d03-4933-be95-d6c4d8e3fe1a

注册系统名为：rhelserver1
```

最后，通过以下命令将系统附加到订阅服务：

```bash
subscription-manager attach --auto
```

```
已安装产品状态：

Product Name: Red Hat Enterprise Linux for x86_64

Status: Subscribed
```

### 3.10 安装更新

与现在的大多数操作系统一样，RHEL 发行版的特定版本在发布给公众后继续演进。这通常表现为错误修复、安全更新，并且偶尔会有新功能，这些功能可以通过互联网下载并安装到你的系统中。

最佳实践规定，安装 RHEL 后第一步是确保将所有可用的更新应用到系统。这可以通过终端窗口中的命令行提示符使用 `dnf` 软件包管理器工具来实现。要检查是否有可用更新，请运行以下命令：

```bash
dnf check-update
```

可以再次使用 `dnf` 工具应用任何待处理的更新：

```bash
dnf update
```

执行后，`dnf` 工具将提供可用更新的包列表，并提示权限以执行更新。更新完成后，安装基本上已经完成，RHEL 9 即可准备好使用。

### 3.11 显示启动消息

在启动过程中，RHEL 9 将显示红帽图形化启动（RHGB）屏幕，该屏幕会隐藏系统在加载时生成的所有启动消息。要在启动过程中使这些消息可见（如图 3-19 所示），请在系统启动时按下键盘上的 `Esc` 键：

![](img/rhel_9_boot_messages.png)

图 3-19



可以通过编辑`/etc/default/grub`文件并更改`GRUB_CMDLINE_LINUX`设置来更改默认行为，使其默认始终显示消息，该设置默认类似于：

```bash
GRUB_CMDLINE_LINUX="... rhgb quiet"
```

要删除图形化启动屏幕，以便在无需按`Esc`键的情况下看到消息，请从设置中删除“rhgb”选项：

```bash
GRUB_CMDLINE_LINUX="... quiet"
```

此更改将导致系统仅显示生成的启动消息子集。要显示系统生成的所有消息，还要删除“quiet”选项：

```bash
GRUB_CMDLINE_LINUX="..."
```

一旦完成更改，运行以下命令以生成新的启动配置，以便在下次系统启动时生效：

```bash
grub2-mkconfig --output=/boot/grub2/grub.cfg
```

### 3.12 总结

使用 RHEL 9 工作的第一步是安装操作系统。对于云服务器，此任务通常在根据云服务提供商提供的系列选项为系统选择操作系统镜像时自动完成。然而，在自己的硬件上安装则涉及下载 ISO 镜像的安装媒体、将该镜像写入 DVD 或 USB 驱动器等合适的存储设备，并从其启动。运行后，安装过程允许配置一系列选项，包括网络、安装应从本地介质还是通过远程服务器或仓库进行、要安装的软件包以及磁盘分区。安装完成后，安装任何自原始安装镜像创建以来可能发布的操作系统更新是非常重要的。

## 4. 与 Windows 双启动 RHEL 9

与大多数 Linux 发行版一样，红帽企业级 Linux 9 可以很乐意地与从 Windows 到包括 Windows 11 在内的几乎任何版本的 Windows 在硬盘器上共存。这种概念被称为“双启动”。当你启动系统时，你将看到一个菜单，提供启动 RHEL 9 安装或 Windows 的选项。显然，你一次只能运行一个操作系统。尽管如此，值得注意的是，无论你的硬盘 Windows 分区是使用 NTFS、FAT16 还是 FAT32 格式化的，你都可以从 RHEL 9 访问 Windows 分区上的文件。

这种安装方法涉及缩小现有 Windows 分区的大小，然后在回收的空间中安装 RHEL 9。本章假设 RHEL 9 正在安装在当前运行 Windows 11 的系统上。

## 4.1 分区大小调整

为了在已包含 Windows 安装的硬盘上容纳 RHEL，第一步涉及缩小 Windows 分区以腾出空间。建议的操作是使用 Windows 磁盘管理界面在尝试安装 RHEL 9 之前缩小分区大小。

要在 Windows 11 上访问磁盘管理，右键点击单击菜单，并从生成的菜单中选择选项，如图 4-1 所示：

![](img/windows_start_menu.png)

图 4-1

加载后，磁盘管理工具将显示系统检测到的硬盘的图形表示：

![](img/windows_disk_management.png)

图 4-2

右键点击你想要缩小大小的分区，从弹出菜单中选择“收缩卷...”（Shrink Volume...）。该工具将计算在不丢失数据的情况下卷大小可以减少的最大量（取决于分区的总大小，此过程可能需要几分钟）。一旦分析完成，将出现一个与下方图 4-3 所示类似的对话框：

![](img/windows_disk_management_shrink_volume.png)

图 4-3

在“输入要收缩的空间量（MB）”字段中指定一个值并点击“收缩”（Shrink）按钮继续。一旦调整操作完成，使用 RHEL 9 安装媒体重启（如“在洁净硬盘上安装 RHEL 9”）在`/etc/default/grub`文件中声明，新安装时如下：

```bash
GRUB_TIMEOUT=5
GRUB_DISTRIBUTOR="$(sed 's, release .*,g' /etc/system-release)"
GRUB_DEFAULT=saved
GRUB_DISABLE_SUBMENU=true
GRUB_TERMIN_OUTPUT="console"
GRUB_CMDLINE_LINUX="crashkernel=1G-4G:192M,4G-64G:256M,64G-:512M resume=/dev/mapper/rhel-swap rd.lvm.lv=rhel/root rd.lvm.lv=rhel/swap rhgb quiet"
GRUB_DISABLE_RECOVERY="true"
GRUB_ENABLE_BLSCFG=true
```

更改默认系统的第一步是在此文件中声明`GRUB_SAVEDEFAULT`设置：

`s, release .*,g' /etc/system-release`替换后添加`GRUB_SAVEDEFAULT=true`

此设置在启动配置中保存了一个新的默认值。接下来，运行`grub2-set-default`命令更改默认设置，使用从第一个选项算作 0 的计数系统。例如，如果 Windows 11 选项是菜单中的第 3 个，将 Windows 11 设置为默认启动选项的命令如下：

```bash
grub2-set-default 2
```

运行以下命令检查新设置是否生效：

```bash
grub2-editenv list
```

```text
saved_entry=f862181be19a40ae921f10fc572174d3-5.14.0-162.23.1.el9_1.x86_64
menu_auto_hide=1
boot_success=1
boot_indeterminate=0
save_default=true
```

请注意`saved_entry`值现在已设置为 Linux 启动分区。更改默认值后，按照如下命令重新生成启动配置文件：

```bash
grub2-mkconfig --output=/boot/grub2/grub.cfg
```

重启系统并验证启动菜单默认选择 Windows 选项，且 Windows 在超时过期后正常加载。

## 4.3 从 RHEL 9 访问 Windows 分区

在双启动配置下运行 RHEL 时，可以通过从命令行手动挂载分区来访问位于 Windows 分区的文件。但是，在此之前，需要在系统上安装一些额外的软件包。首先，需要下载并安装`fuse`内核模块：

```bash
dnf install fuse
modprobe fuse
```

接下来，需要安装 Fuse NTFS 驱动。遗憾的是，该包未包含在标准的 RHEL 9 仓库中，因此需要如下向系统添加 Extra Packages for Enterprise Linux (EPEL) 仓库：

```bash
subscription-manager repos --enable codeready-builder-for-rhel-9-$(arch)-rpms
dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm
```

添加 EPEL 仓库后，现在可以安装驱动程序：

```bash
dnf install ntfs-3g
```

一旦安装了所需的软件包，下一步是创建一个目录作为我们 Windows 分区的挂载点。在本示例中，我们将创建一个名为`/mnt/windows`的目录：

```bash
mkdir /mnt/windows
```

使用`fdisk`命令识别分配给 Windows 分区的设备名称：

```bash
fdisk -l
```

```text
设备 起 结束 扇区 大 类型

/dev/nvme0n1p1 2048 206847 204800 100M EFI System

/dev/nvme0n1p2 206848 239615 32768 16M Microsoft reserved

/dev/nvme0n1p3 239616 49362943 49123328 23.4G Microsoft basic data

/dev/nvme0n1p4 132933632 134213631 1280000 625M Windows recovery environment

/dev/nvme0n1p5 49362944 51460095 2097152 1G Linux filesystem

/dev/nvme0n1p6 51460096 132933631 81473536 38.8G Linux LVM
```

在上面的输出中，包含我们需要访问的文件的主 Windows 分区由`/dev/nvme0n1p3`表示。接下来，我们需要按照如下方式运行`mount`命令（假设 Windows 分区为`/dev/nvme0n1p3`）：

```bash
mount /dev/nvme0n1p3 /mnt/windows
```

列出挂载点根目录的内容来检查挂载是否成功：

```bash
ls /mnt/windows
```

```text
'$Recycle.Bin' ProgramData swapfile.sys

'Documents and Settings' 'Program Files' 'System Volume Information'

pagefile.sys 'Program Files (x86)' Users

PerfLogs Recovery Windows
```

为了在每次系统启动时自动挂载，请向`/etc/fstab`文件中添加适当的挂载行：

```text
/dev/nvme0n1p3 /mnt/windows ntfs defaults 0 0
```

要随时卸载 Windows 文件系统：

```bash
umount /mnt/windows
```

## 4.4 总结

RHEL 9 可以通过创建双启动环境与 Windows 操作系统在同一块硬盘上安全共存。这涉及到在安装之前缩小 Windows 系统空间为 RHEL 9 留出空间。一旦安装了 RHEL，必须修改启动菜单配置以包含从 Windows 启动的选项。要在 RHEL 内部访问 Windows 文件系统，需要安装 Fuse NTFS 驱动并使用它来挂载 Windows 分区。

## 5. 在 RHEL 9 中删除 Windows 分区

在上一章中，我们查看了在与 Windows 相同的磁盘上安装 Red Hat Enterprise Linux 9。这种所谓的“双启动”配置允许用户在单个硬盘上安装两个操作系统，并在系统开机时可以选择启动其中一个。

本章适用于那些已经决定足够喜欢 RHEL 9，从而从磁盘上完全删除 Windows 并将空间用于 Linux 的用户。在接下来的章节中，我们将逐步完成这一过程。

### 5.1 卸载 Windows 分区

如果按照“与 Windows 双启动 RHEL 9”章节中的步骤从 RHEL 9 内部挂载了 Windows 分区，则在继续本章之前应采取措施卸载分区。假设 Windows 分区被挂载为`/mnt/windows`，可以如下进行卸载：

```bash
umount /mnt/windows
```

如果之前添加过`/etc/fstab`文件，也应对其编辑以移除`/mnt/windows`自动挂载。

### 5.2 从磁盘上删除 Windows 分区

为 RHEL 释放 Windows 分区的第一步是删除该分区。在此之前，必须备份 Windows 和 RHEL 分区中的任何数据。完成此操作后即可继续本章。要删除 Windows 分区，首先需要使用`fdisk`工具识别它们所在的磁盘：

```bash
fdisk -l
设备 起 结束 扇区 大 类型
/dev/nvme0n1p1 2048 206847 204800 100M EFI System
/dev/nvme0n1p2 206848 239615 32768 16M Microsoft reserved
/dev/nvme0n1p3 239616 49362943 49123328 23.4G Microsoft basic data
/dev/nvme0n1p4 132933632 134213631 1280000 625M Windows recovery environment
/dev/nvme0n1p5 49362944 51460095 2097152 1G Linux filesystem
/dev/nvme0n1p6 51460096 132933631 81473536 38.8G Linux LVM
```

在上面的示例中，系统包含一个由设备名称`/dev/nvme0n1`引用的物理磁盘。该磁盘上分别通过`/dev/nvme0n1p1`到`/dev/nvme0n1p6`分区。根据 Types 列的值，存在三个 Windows 相关分区。第一个是 Windows 系统分区，第二个较大的分区包含 Windows 操作系统和数据，随后是 Windows 恢复分区。

要删除分区，使用包含分区的磁盘名称（在本例中为`/dev/nvme0n1`）启动`fdisk`工具，并按照指示再次显示分区和扇区信息：

```bash
fdisk /dev/nvme0n1

欢迎使用 fdisk (util-linux 2.37.4)。

更改将仅留在内存中，直到你决定写入。

在使用 write 命令前要小心。

命令 (m for help): p

磁盘 /dev/nvme0n1: 64 GiB, 68719476736 字节, 13421728 扇区

磁盘模型: VMware Virtual NVMe Disk

单位: 1 * 512 = 512 字节

扇区大小 (逻辑/物理): 512 字节 / 512 字节

I/O 大小 (最小/最优): 512 字节 / 512 字节

磁盘标签: gpt

磁盘标识符: 7A38CD86-091E-4781-BFB0-928FD3C935

设备 起 结束 扇区 大 类型

/dev/nvme0n1p1 2048 206847 204800 100M EFI System

/dev/nvme0n1p2 206848 239615 32768 16M Microsoft reserved

/dev/nvme0n1p3 239616 49362943 49123328 23.4G Microsoft basic data

/dev/nvme0n1p4 132933632 134213631 1280000 625M Windows recovery environment

/dev/nvme0n1p5 49362944 51460095 2097152 1G Linux filesystem

/dev/nvme0n1p6 51460096 132933631 81473536 38.8G Linux LVM

分区表项不是按磁盘顺序。

命令 (m for help):
```

在继续之前，请记住我们将删除的分区的起始和结束地址（即`/dev/nvme0n1p2`的起始处以及`/dev/nvme0n1p5`起始之前的扇区）。

在命令提示符处，删除 Windows 分区（即示例系统中的 2、3 和 4 号分区）：

```text
命令 (m for help): d

分区编号 (1-6, 默认 6): 2

分区 2 已删除。

命令 (m for help): d

分区编号 (1,3-6, 默认 6): 3

分区 3 已删除。

命令 (m for help): d

分区编号 (1,4-6, 默认 6): 4

分区 4 已删除。
```

既然我们已经删除了 Windows 分区，我们需要在腾出的磁盘空间中创建新的`RHEL`分区。分区编号必须与删除的第一个分区编号匹配（在本例中为`2`）。此外，有必要精确输入与旧分区报告一致的分区起始扇区和结束扇区（尽管`fdisk`通常会默认提供正确的值，但双重检查是明智的）。如果系统提示要删除 NTFS 签名，请输入 Y：

```text
Command (m for help): n

Partition number (2-4,7-128, default 2): 2

First sector (206848-134217694, default 206848):

Last sector, +/-sectors or +/-size{K,M,G,T,P} (206848-49362943, default 49362943):

Created a new partition 2 of type 'Linux filesystem' and of size 23.4 GiB.

Command (m for help):
```

完成这些更改后，下一步是检查设置是否正确：

```text
Command (m for help): p

Disk /dev/nvme0n1: 64 GiB, 68719476736 bytes, 134217728 sectors

Disk model: VMware Virtual NVMe Disk

Units: sectors of 1 * 512 = 512 bytes

Sector size (logical/physical): 512 bytes / 512 bytes

I/O size (minimum/optimal): 512 bytes / 512 bytes

Disklabel type: gpt

Disk identifier: 7A38CD86-091E-4781-BFB0-928FD383C935

Device Start End Sectors Size Type

/dev/nvme0n1p1 2048 206847 204800 100M EFI System

/dev/nvme0n1p2 206848 49362943 49156096 23.4G Linux filesystem

/dev/nvme0n1p5 49362944 51460095 2097152 1G Linux filesystem

/dev/nvme0n1p6 51460096 132933631 81473536 38.8G Linux LVM
```



为了提交更改，我们现在需要将新的分区信息写入磁盘并退出`fdisk`工具：

```
Command (m for help): w
```

分区表已更改。  
正在同步磁盘。

## 5.3 格式化未分配磁盘分区

为了使新分区适用于`RHEL 9`使用，需要在其上创建一个文件系统。当前版本`RHEL`推荐的文件系统类型是`XFS`，它将在标题为向 RHEL 9 系统中添加新磁盘驱动器的章节中详细介绍。使用以下`mkfs.xfs`命令创建文件系统：

```
# mkfs.xfs -f /dev/nvme0n1p2
```

```
meta-data=/dev/nvme0n1p2 isize=512 agcount=4, agsize=1536128 blks
        = sectsz=512 attr=2, projid32bit=1
        = crc=1 finobt=1, sparse=1, rmapbt=0
        = reflink=1 bigtime=1 inobtcount=1
data = bsize=4096 blocks=6144512, imaxpct=25
        = sunit=0 swidth=0 blks
naming =version 2 bsize=4096 ascii-ci=0, ftype=1
log =internal log bsize=4096 blocks=3000, version=2
        = sectsz=512 sunit=0 blks, lazy-count=1
realtime =none extsz=4096 blocks=0, rtextents=0
```

## 5.4 挂载新分区

接下来，我们需要挂载新分区。在本例中，我们将将其挂载到名为`/data`的目录中。然而，你可以使用任何所需的有效挂载点挂载新分区，或将其作为逻辑卷的一部分（详细信息将在标题为向 RHEL 9 卷组和逻辑卷中添加新磁盘的章节中介绍）。首先，我们需要创建作为挂载点的目录：

```
# mkdir /data
```

其次，我们需要编辑`/etc/fstab`中的挂载表，以便分区在每次系统启动时自动挂载。在`/etc/fstab`最后添加以下行来挂载新分区（修改`/etc/fstab`）：

```
/dev/nvme0n1p2 /data xfs defaults 0 0
```

最后，我们可以手动挂载新分区：

```
# mount /data
```

运行以下命令检查分区情况：

```bash
# df -h
```

## 5.5 总结

Red Hat Enterprise Linux 9 包含了 GNOME 桌面。

## 6.1 安装 GNOME 桌面

如果在安装期间选择了`Workstation`（工作站）或`Server with GUI`（带图形界面的服务器）配置，则每次系统启动时都可以使用 GNOME 桌面。如果选择了任何其他软件配置，则不会包含 GNOME 桌面。值得注意的是，远程访问桌面也是可行的；即使在无头服务器上（即缺少显示器、键盘和鼠标的服务器），安装 GNOME 桌面可能仍然大益。建立远程桌面的主题将在使用 VNC 访问 RHEL 9 远程桌面中进行详细介绍。

如果安装配置未包含 GNOME 桌面，可以随时使用以下命令进行安装：

```
# dnf groupinstall workstation
```

安装完成后，可以从命令行提示符启动桌面环境：

```
$ startx
```

## 6.2 GNOME 桌面概述

图 6-1 所示显示了新启动的 GNOME 桌面在启动任何程序或进行配置之前的界面：

主桌面区域（标记为 A）是应用程序和工具窗口出现的地方。与其他桌面环境不同，无法将文件或应用程序拖到桌面，这提供了一个整洁无杂的工作空间。

屏幕顶部的条（B）称为顶栏，包含活动菜单（C）、日期和时间，以及一组按钮和图标，包括网络状态、音频量、电池电源和其他状态和账户设置。此外，当前在桌面运行的活动应用程序的菜单也会出现在顶栏中。

## 6.3 活动概览

应用程序和工具通过活动概览进行启动，可以通过点击顶栏中的活动按钮或按下键盘上的特殊键来显示。在 Windows 键盘上，这是`Windows`键；在 macOS 上是`Command`键，在 Chromebook 上是带有放大镜的按键。

显示时，活动概览将类似于图 6-3 所示。

概览的中央区域（上方图 6-3 中标记为 A）显示了所有当前打开的应用程序窗口。屏幕底部（B）是启动器（也称为 dash），可以通过它启动应用程序。默认情况下，启动器将显示一组预定义的常用应用程序图标，以及任何当前正在运行的应用程序的图标。如果应用程序正在运行，则图标下方将显示一个圆点。要启动应用程序，只需点击启动器中的图标即可。

要查找未包含在启动器中的应用程序，一种方法是选择右侧的网格图标（由九个点组成的正方形），以显示可浏览的应用程序列表，如图图 6-4 所示：

![](img/rhel_9_gnome_activities_grid.png)

图 6-4

同样重要的是，列表中的某些项目是包含其他应用程序的文件夹。可以通过拖动并释放图标来重新排列网格中的项目。要将应用程序添加到文件夹，请在网格中找到它并将其拖入文件夹。此外，拖动一个图标并将其释放到另一个图标上将创建一个包含这两个应用程序的新文件夹，并可以向其中添加其他应用程序。

浏览应用程序的替代方案是使用搜索栏进行搜索（上方图 6-3 中标记为 C），并在图中显示了操作过程：

![](img/rhel_9_gnome_activities_search.png)

图 6-5

随着在搜索框中输入文本，可能的匹配项列表将不断精简。

为了更方便地访问将应用程序添加到启动器，请找到应用程序的图标，右键点击它，并选择“添加到收藏夹”菜单选项：

![](img/rhel_9_gnome_add_to_favorites.png)

图 6-6

要从启动器中删除应用程序，右键点击启动器中的图标并选择“从收藏夹中移除”。或者，通过在启动器与外部之间拖放图标来添加和删除它们。

## 6.4 管理窗口

与其他桌面环境一样，在 GNOME 上运行的应用程序以窗口形式存在。当打开多个应用程序窗口时，使用`Super + Tab`快捷键将显示切换面板（图 6-7），允许选择不同的窗口作为当前活动窗口（`Super`键可以是 Windows 键，或者在 Mac 键盘上是`Cmd`键）：

![](img/rhel_9_gnome_switcher.png)

图 6-7

如果一个应用程序打开了多个窗口，切换器将在第二个面板中显示这些窗口，以便选择特定窗口：

![](img/rhel_9_gnome_switcher_multi_windows.png)

图 6-8

要在切换器中的图标上反向循环切换，请使用`Shift+Tab`快捷键。

要最大化窗口以填满整个屏幕，点击标题栏并将窗口拖动到屏幕顶部。要将窗口恢复到原始大小，点击标题栏并将其向下拖动。或者，双击标题栏可以在窗口大小之间切换。同样，将窗口拖到屏幕的左侧或右侧将使窗口填充屏幕的半部分。

## 6.5 使用工作区

显示应用程序窗口的屏幕区域被称为工作区，GNOME 40 允许配置多个工作区。GNOME 桌面启动时会有两个工作区，您可以使用`Super+Alt+Left`和`Super+Alt+Right`键组合在之间切换。当窗口被添加到空白工作区时，工作区面板会添加另一个空白工作区，从而创建更多工作区。

当前工作区的缩略图出现在活动概览中搜索字段下方，如图图 6-9 所示：

![](img/rhel_9_gnome_workspaces.png)

图 6-9

要切换到不同的工作区，请选择相应的缩略图。要将窗口从一个工作区移动到另一个工作区，显示工作区面板并将应用程序窗口（当前工作区的实际窗口或工作区面板中的缩略窗口）拖放到目标工作区。要删除工作区，请关闭所有窗口或将其移动到另一个工作区。

## 6.6 日历与通知

当系统需要通知您事件（例如系统或应用程序更新可用），弹出面板将出现在工作区的顶部。此外，通过点击顶栏上的日期和时间可以访问日历和任何之前的通知，如图图 6-10 所示：

![](img/rhel_9_gnome_date_time.png)

图 6-10

## 6.7 GNOME 桌面设置

要访问“设置”应用程序，点击顶栏右侧的图标行并选择“设置”，如图图 6-11 所示：

![](img/rhel_9_gnome_settings_menu_low_res.png)

图 6-11

设置应用程序提供了许多选项，例如以太网和 WiFi 连接、屏幕背景自定义选项、屏幕锁定和电源管理以及语言设置。要探索每个类别中的可用设置，请从设置窗口左侧面板中选择选项：

![](img/rhel_9_gnome_settings.png)

图 6-12

上述图 6-11 中的菜单还包括切换用户、调整音量、切换到不同网络以及注销、重启或关机选项。

## 6.8 基础自定义之外

GNOME 40 桌面在设计上是一个洁净、整洁的环境，自定义选项极少。然而，可以对桌面进行额外的更改。GNOME 项目开发了一个名为`GNOME Tweaks`的工具用于此目的。使用以下命令安装并运行此工具：

```
# dnf install gnome-tweaks
$ gnome-tweaks
```

一旦 GNOME Tweaks 加载，将出现如图图 6-13 所示的界面：

![](img/rhel_9_gnome_tweaks.png)

图 6-13

现在提供了大量的自定义桌面选项。本章无法全部涵盖，因此在进入下一章节之前，请尝试这些设置。

## 6.9 总结

RHEL 9 包含了 GNOME 40 桌面环境，可以在初始安装时包含，也可以使用`dnf`组软件包功能以后安装。与其他桌面环境相比，GNOME 40 旨在提供一个简洁且易用的窗口用户界面。GNOME 40 桌面的关键区域包括顶栏、活动概览和启动器。此外，GNOME 40 支持多个工作区，使运行的应用程序保持井然有序且屏幕整洁。设置应用程序提供了多种配置选项，包括桌面背景、音频、网络配置和 WiFi 网络选择。

## 7. Cockpit Web 界面概述

尽管配备了最新的 Linux 桌面环境，Red Hat Enterprise Linux 9 仍然是一个服务器操作系统。因此，大多数 RHEL 部署是针对远程物理服务器或云虚拟机实例的。通常情况下，这些系统在没有键盘、鼠标或显示器的情况下运行，只能通过网络连接使用命令行提示进行直接访问。这在从远程管理系统方面带来了挑战。

Cockpit 基于 Web 的管理界面提供了此功能。本章将解释如何安装、配置和访问 Cockpit 界面，同时提供 Cockpit 关键功能的概述，其中许多功能将在后面的章节中详细介绍。

## 7.1 Cockpit 概述

Cockpit 是一个轻量级的基于 Web 的界面，允许远程执行常规系统管理任务。安装并配置完成后，系统管理员打开本地浏览器窗口并导航到远程服务器上的 Cockpit 端口。在浏览器中加载 Cockpit 界面并登录后，可以使用管理和监控工具视觉化地执行各种任务。

在后台，Cockpit 使用与在命令行工作时相同的工具执行任务，并自动更新以反映系统其他地方发生的变化。这意味着 Cockpit 可以与其他管理工具和技术配合使用，而无一种方法覆盖另一种方法的风险。Cockpit 还可以配置为访问多个服务器，允许通过单个浏览器会话同时管理和监控多个服务器。

Cockpit 默认安装并捆绑了系列工具，允许根据需要安装额外的扩展插件。Cockpit 的设计还允许您结合 HTML 和 JavaScript 创建自己的扩展，以添加缺失或自定义制功能。

Cockpit 的模块化设计还允许许多功能嵌入到其他基于 Web 的应用程序中。

## 7.2 安装并启用 Cockpit

RHEL 9 默认不安装 Cockpit，但可以通过简单的步骤进行设置和启用。第一步是按照如下方式安装 Cockpit 包：

```
dnf install cockpit
```

接下来，需要启用 Cockpit socket 服务：

```
systemctl enable --now cockpit.socket
```

最后，如果您的系统上启用了防火墙，则需要在防火墙上打开必要的端口，以允许远程浏览器连接到达 Cockpit（有关防火墙的详情，请参阅“RHEL 9 防火墙基础”章节）。

```
firewall-cmd --add-service=cockpit --permanent
firewall-cmd --reload
```

## 7.3 访问 Cockpit

如果您可以访问安装了 Cockpit 的服务器桌面环境，请打开浏览器窗口并导航到`https://localhost:9090`以访问 Cockpit 登录界面。相反，如果服务器是远程的，请使用域名或 IP 地址访问服务器（例如，`https://myserver.com:9090`）。

当建立连接时，浏览器可能会警告连接不安全。这是因为 Cockpit 服务使用了自签名证书。选择继续访问网站选项，或者为了以后避免出现此消息，选择高级选项并为服务器地址添加异常。

一旦连接成功，浏览器将加载下方图 7-1 所示的登录页面：

![](img/rhel_cockpit_login.png)

图 7-1

使用 root 身份或您的用户账户凭据登录 Cockpit 界面。请注意，由于权限限制，以用户身份登录时，某些任务在 Cockpit 界面内受限。在这种情况下，Cockpit 控制台将显示标记为“受限访问”的按钮，如图 7-2](#Ubuntu_Cockpit_Overview.xhtml__idTextAnchor126)所示：

![](img/rhel_cockpit_limited_access.png)

图 7-2

要提升权限，请点击受限访问按钮并在提示时输入您的密码：

![](img/rhel_cockpit_access_password.png)

图 7-3

登录后，Cockpit 将显示概览屏幕。

## 7.4 概述

概览屏幕提供了系统的概述，包括对 CPU、内存、存储和网络活动性能指标的访问。此屏幕还包含有关系统的信息，包括底层硬件、主机名、系统时间以及系统软件是否为最新。还提供了重启或关闭系统的选项。

例如，图 7-4 显示了 Cockpit 界面的概览页：

![](img/rhel_cockpit_overview.png)

图 7-4

要获取特定类别的更多信息，请点击相应的链接。例如，图 7-5 显示了系统使用和指标屏幕：

![](img/rhel_cockpit_usage_metrics.png)

图 7-5

## 7.5 日志

当选择日志（Logs）类别时，Cockpit 会显示 systemd journal 日的内容。选择一个日志条目将显示整个日志消息。日志条目按时间排序，最新的在顶部，并包含了菜单，用于根据不同的时间段和消息严重程度过滤日志。

![](img/rhel_cockpit_logs.png)

图 7-6

## 7.6 存储

选择存储（Storage）选项以查看和管理系统的存储，包括磁盘、分区和卷组、网络文件系统（NFS）挂载以及 RAID 存储。此屏幕还可以监控磁盘 I/O 活动，并列出用于查询和管理设备的`udisks`服务输出：

![](img/rhel_cockpit_storage.png)

图 7-7

## 7.7 网络

网络界面提供了各种网络配置和服务的信息，包括网络接口和防火墙设置。此外，它还允许配置更改，例如创建网桥或设置虚拟网络：

![](img/rhel_cockpit_networking.png)

图 7-8

## 7.8 账户

选择此选项查看配置在系统上的用户并为额外用户创建账户。用户管理将在管理 RHEL 9 用户和组章节中介绍：

![](img/rhel_cockpit_accounts.png)

图 7-9

点击现有账户查看详细信息并更改。账户详细页还可用于向用户添加 SSH 公钥，以便远程访问服务器，如在 RHEL 9 上配置 SSH 密钥认证章节所示。

## 7.9 服务

此屏幕显示运行在服务器上的系统服务列表，并允许对这些服务进行添加、删除、停止和启动。

![](img/rhel_cockpit_services.png)

图 7-0

服务的主题将在管理 RHEL 9 systemd 单元章节中详细介绍。

## 7.10 应用程序

可以通过扩展为 Cockpit 添加附加功能。这些可以是自开发的，也可以是第三方提供的。应用程序界面列出了已安装的扩展并允许添加或删除扩展：

![](img/rhel_cockpit_applications.png)

图 7-11

## 7.11 虚拟机

虚拟允许在单一计算机系统上同时运行多个操作系统实例，每个系统运行在自己的虚拟机中。Cockpit 虚拟机扩展提供了创建和管理安装在服务器上的虚拟机客户的方法：

![](img/rhel_8_cockpit_virtual_machines.png)

图 7-12

虚拟机扩展默认不安装，但可以通过 Cockpit 应用程序界面或运行以下命令进行添加：

```
dnf install cockpit-machines
```



RHEL 9 的虚拟化使用将从虚拟化技术概述章节开始介绍。

## 7.12 软件更新

如果系统有任何可用软件更新，它们将列在此处并可以从此屏幕进行安装：

![](img/rhel_cockpit_updates.png)

图 7-13

### 7.13 终端

如名称所示，`Terminal`屏幕提供了命令行提示符的访问：

![](img/rhel_cockpit_terminal.png)

图 7-14

### 7.14 连接到多个服务器

可以配置 Cockpit 以在单个会话中管理多个服务器。要向 Cockpit 会话添加另一个主机，请点击上方图 7-15 中亮显示的按钮以显示`Hosts`（主机）面板：

![](img/rhel_cockpit_hosts.png)

图 7-15

点击`Add new host`添加新主机）按钮，输入其他系统的 IP 地址或主机名，并在点击`Add`（添加）按钮之前选择一种区分此服务器与之前添加到 Cockpit 的其他服务器的颜色：

![](img/rhel_cockpit_add_new_host.png)

图 7-16

如果您是首次连接到远程服务器，Cockpit 将要求您接受新的`SSH key`。在接受密钥后，系统将提示您输入上方图 7-16 中指定的用户名密码。系统还提供了设置并授权受密码保护的`SSH key`的选项，以便在下次需要访问第二个主机系统时能够启用自动登录：

![](img/rhel_cockpit_remote_login.png)

图 7-17

若要在主机之间切换，请显示`Hosts`面板（见上方的图 7-15）并选择所需的系统。

### 7.15 启用存储的指标

在标准安装中，Cockpit 不保留图表覆盖的短时间窗口之外的任何性能指标数据。为了保留 Cockpit 收集的数据，需要安装`Cockpit Co-Pilot`（`PCP`）包。按照以下方式安装 `cockpit-pcp` 包：

```
dnf install cockpit-pcp
```

安装 `cockpit-pcp` 后，注销当前 Cockpit 会话并重新登录。

接下来，显示`Metrics`和`history`屏幕，点击`Metrics`设置按钮显示如图 7-18 所示的屏幕，开启`Collect metrics`（收集指标）选项并点击`Save`（保存）：

![](img/rhel_cockpit_collect_metrics.png)

图 7-18

经过足够的时间让 Cockpit 收集数据后，指标信息将如图 7-19 所示出现，并按小时块分类：

![](img/rhel_cockpit_stored_metrics.png)

图 7-19

### 7.16 总结

Cockpit Web 界面允许在浏览器内通过可视化方式执行远程系统管理任务，而无需依赖命令行提示符和命令行工具。一旦安装并启用，系统管理员只需打开浏览器，连接到远程服务器并登录 Cockpit 界面。在后台，Cockpit 使用与通过命令行提示符提供的相同的命令行工具，允许使用两种方式而不会产生配置冲突的风险。此外，Cockpit 使用模块化框架，允许添加额外的扩展，并能够开发和集成自定义扩展。Cockpit 会话可用于管理单个服务器，也可配置为同时访问多个服务器。

# 8. 在 RHEL 9 上使用 Bash Shell

学习与 RHEL 9 以及通用 Linux 发行版工作的一个基本部分是熟练掌握在 shell 环境中工作。虽然 Linux 包含的`GNOME` 等图形桌面环境为操作系统提供了用户友好的界面，但 shell 环境提供了比使用图形桌面工具能实现的更强大的功能、灵活性和自动化。shell 环境还为没有桌面环境的情况下提供了一种与操作系统交互的手段，这在处理如 RHEL 9 这样基于服务器的操作系统或无法完全启动的损坏系统时是常见情况。

因此，本章旨在提供 RHEL 9 上默认 shell 环境（特别是`Bash` shell）的概述。

## 8.1 什么是 Shell？

Shell 是一个交互式命令解释器环境，可以在其中提示符处输入命令，或将命令输入文件作为脚本执行。Shell 的起源可以追溯到 UNIX 操作系统的早期。事实上，在 Linux 早期，引入图形桌面之前，shell 是用户与操作系统交互的唯一方式。

多年来，开发了多种 shell 环境。第一个被广泛使用的 shell 是由 Stephen Bourne 在贝尔实验室编写的`Bourne shell`。

另一个早期产物是`C shell`，它与`C 语言`在某些语法上具有相似之处，并引入了命令行编辑和历史记录等易用性增强。

`Korn shell`（由 David Korn 在贝尔实验室开发）基于`Bourne` 和 `C` shell 提供的特性。

RHEL 9 上的默认 shell 是`Bash shell`（Bourne Again SHell 的缩写）。这种 shell 起初是 `Bourne shell` 的开源版本，由 Brian Fox 为 `GNU Project` 开发，并基于`Bourne shell` 和 `C shell` 提供的特性。

## 8.2 获取 Shell 访问

在`GNOME` 桌面环境中，可以通过`Terminal`窗口访问 shell 提示符，方法是选择顶部栏中的`Activities` 选项，在搜索栏中输入`Terminal` 并点击 `Terminal` 图标。

例如，当远程登录 RHEL 9 服务器时（例如使用`SSH`），用户将看到 shell 提示符。标题为“在 RHEL 9 上配置基于密钥的身份验证”的章节将介绍使用 `SSH` 访问远程服务器的细节。在启动未安装桌面环境的服务器系统时，用户在物理控制台或远程登录会话完成登录程序后立即进入 shell。

## 8.3 在提示符处输入命令

在 shell 命令行提示符处，只需输入命令并按`Enter`键即可输入命令。虽然某些命令静默执行任务，但大多数命令在返回提示符之前都会显示某种形式的输出。例如，`ls` 命令可显示当前目录下的文件和文件夹：

```
ls

Desktop Downloads Music Public Templates Videos
```

可用命令要么内置于 shell 中，要么存在于物理文件系统中。可以使用`which` 命令识别命令在文件系统中的位置。例如，查找 `ls` 可执行文件在文件系统中的：

```
which ls

alias ls='ls --color=auto'

/usr/bin/ls
```

显然，`ls` 命令位于 `/usr/bin` 目录。此外还配置了别名，该主题将在本章稍后介绍。使用`which` 命令定位内置于 shell 的命令路径将导致找不到可执行文件的消息。例如，尝试查找`history` 命令的位置（它是内置于 shell 的，而不是文件系统上的可执行文件）将得到类似下面的输出：

```
which history

/usr/bin/which: no history in (/home/demo/.local/bin:/home/demo/bin:/usr/share/Modules/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin)
```

## 8.4 获取命令信息

Linux shell 可用的许多命令看起来很晦涩。要获取有关命令的功能以及如何使用的详细信息，请使用`man` 命令并将命令名作为参数。例如，了解更多关于 `pwd` 命令的信息：

```
man pwd
```

执行上述命令后，将显示 `pwd` 命令的详细描述。许多命令在带有 `--help` 命令行选项运行时也会提供额外信息：

```
$ wc --help
```

## 8.5 Bash 命令行编辑

早期的壳（shell）环境不提供任何形式的行编辑功能。这意味着如果你在输入一条长命令行的开头发现错误，你必须删除之后的所有字符，纠正错误然后重新输入命令的剩余部分。幸运的是，Bash 丰富的命令行编辑选项，如下表所示：

| 按键序列 | 动作 |
| :--- | :--- |
| Ctrl-b 或 左箭头 | 将光标向后移动一位 |
| Ctrl-f 或 右箭头 | 将光标向前移动一位 |
| Delete | 删除光标当前位置下方的字符 |
| Backspace | 删除光标左侧的字符 |
| Ctrl-_ | 撤销上一次更改（可以重复操作以撤销所有之前的更改） |
| Ctrl-a | 将光标移动到行首 |
| Ctrl-e | 将光标移动到行尾 |
| Meta-f 或 Esc 后 f | 光标向后移动一个单词 |
| Meta-b 或 Esc 后 b | 光标向后移动一个单词 |
| Ctrl-l | 清除屏幕上当前命令以外的所有内容 |
| Ctrl-k | 从当前光标位置删除到行末尾 |
| Meta-d 或 Esc 后 d | 删除到当前单词的结束 |
| Meta-DEL 或 Esc 后 DEL | 删除到当前单词的开始 |
| Ctrl-w | 从当前光标位置删除到上一个空白符 |

表 8-1

## 8.6 使用 Shell 历史记录

除了命令行编辑功能外，Bash 壳还提供了命令行历史支持。可以使用 `history` 命令查看之前执行过的命令列表：

```
$ history

    1 ps

    2 ls

    3 ls –l /

    4 ls

    5 man pwd

    6 man apropos
```

此外，可以使用 `Ctrl-p`（或向上箭头）和 `Ctrl-n`（或向下箭头）在之前输入的命令之间来回滚动。最后，当历史记录显示了所需的命令时，按 `Enter` 键执行它。

另一个选项是输入 `!` 字符，后跟要重复的命令的前几个字符，然后按 `Enter` 键。

## 8.7 文件简写

许多 shell 命令接受一个或多个文件名作为参数。例如，要显示名为 `list.txt` 的文本文件的内容，可以使用如下方式使用 `cat` 命令：

```
$ cat list.txt
```

同样，可以通过指定所有文件名作为参数来显示多个文本文件的内容：

```
$ cat list.txt list2.txt list3.txt list4.txt
```

与其输入每个名称，不如使用模式匹配来指定所有符合特定标准的文件。例如，可以使用 `*` 通配符字符来简化上面的示例：

```
$ cat *.txt
```

上述命令将显示所有以 `.txt` 扩展的文件的内容。这可以进一步限制为任何以 `list` 开头并 `.txt` 结尾的文件名：

```
$ cat list*.txt
```

可以使用 `?` 字符指定单字符匹配：

```
$ cat list?.txt
```

## 8.8 文件名和路径补全

与其输入完整的文件名或路径，或使用模式匹配来减少输入量，shell 提供了文件名补全功能。要使用文件名补全，输入文件或路径名的前几个字符，然后按两次 `Esc` 键。shell 将根据目录中匹配你输入字符的第一个文件或路径名为你完成文件名。要获取可能的匹配项列表，在输入前几个字符后按 `Esc =`。

## 8.9 输入和输出重定向

如前所述，许多 shell 命令在执行时会输出信息。默认情况下，这些输出去向名为 `stdout` 的设备文件，它本质上是运行 shell 的终端窗口或控制台。相反，shell 从名为 `stdin` 的设备文件接收输入，默认是键盘。

可以使用 `>` 字符将命令的输出从 `stdout` 重定向到文件系统的物理文件。例如，要将 `ls` 命令的输出重定向到名为 `files.txt` 的文件，需要以下命令：

```
$ ls *.txt > files.txt
```

完成后，`files.txt` 将包含当前目录下的文件列表。同样，可以将文件内容作为 `stdin` 喂给命令中。例如，要将文件内容作为输入重定向到命令：

```
$ wc –l < files.txt
```

上述命令将显示 `files.txt` 文件中的行数。

需要注意的是，使用 `>` 重定向运算符会创建一个新文件或截断现有文件。要向现有文件追加内容，请使用 `>>` 运算符：

```
$ ls *.dat >> files.txt
```

除了标准输出外，shell 还使用 `stderr` 提供标准错误输出。当命令的输出重定向到 `stdout` 时，命令生成的任何错误信息都会重定向到 `stderr`。这意味着如果 `stdout` 重定向到文件，错误信息仍然出现在终端中。这通常是期望的行为，但也可以通过 `2>` 运算符重定向 `stderr`：

```
$ ls 2> errsg
```

执行完成后，关于找不到文件 `dkjfnf` 的错误信息将位于 `errsg` 中。

`stderr` 和 `stdout` 都可以使用 `&>` 运算符重定向到同一个文件：

```
$ ls /etc &> alloutput
```

执行完成后，`alloutput` 文件将包含

## 8.10 在 Bash Shell 中使用管道

除了 I/O 重定向，Bash shell 还允许将一个命令的输出直接管道到另一个命令的输入。管道操作通过在命令行之间放置 `|` 字符来实现。例如，为了统计系统中运行的进程，可以将 `ps` 命令的输出管道通过 `wc` 命令：

```
$ ps –ef | wc –l
```

命令行上可以执行的管道操作没有限制。例如，查找包含 `Smith` 名称的文件行数：

```
$ cat namesfile | grep Smith | wc –l
```

## 8.11 配置别名

随着你熟悉 shell 环境，你可能会频繁使用带有参数的命令。例如，你可能经常带有 `l` 和 `t` 参数使用 `ls` 命令：

```
$ ls –lt
```

为了减少执行命令时的输入量，可以创建一个映射到命令和参数的别名。例如，为了创建一个别名使得输入字母 `l` 执行 `ls –lt` 命令，可以使用以下语句：

```
$ alias l="ls –lt"
```

现在提示符处输入 `l` 将执行原始语句。

## 8.12 环境变量

Shell 环境变量提供了数据和配置设置的临时存储。shell 本身设置了几个环境变量，用户可以更改这些变量来修改 shell 的行为。可以使用 `env` 命令获取当前定义的变量列表：

```
$ env

    SSH_CONNECTION=192.168.0.19 61231 192.168.0.28 22

    MODULES_RUN_QUARANTINE=LD_LIBRARY_PATH

    LANG=en_US.UTF-8

    HISTCONTROL=ignoredups

    HOSTNAME=RHELdemo-pc.ebookfrenzy.com

    XDG_SESSION_ID=15

    MODULES_CMD=/usr/share/Modules/libexec/modulecmd.tcl

    USER=demo

    ENV=/usr/share/Modules/init/profile.sh

    SELINUX_ROLE_REQUESTED=

    PWD=/home/demo

    HOME=/home/demo

    SSH_CLIENT=192.168.0.19 61231 22

    SELINUX_LEVEL_REQUESTED=
```

也许最有用的环境变量是 `PATH`。它定义了 shell 在命令行提示符下搜索输入命令的目录列表，以及搜索的顺序。在新安装的 RHEL 9 系统上，用户账户的 `PATH` 环境变量可能配置如下：

```bash
$ echo $PATH
```

```
/home/demo/.local/bin:/home/demo/bin:/usr/share/Modules/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin
```

另一个有用的变量是 `HOME`，它指定当前用户的家目录。例如，如果你希望 shell 也在家目录下的 `scripts` 目录中查找命令，你可以如下所示修改 `PATH` 变量：

```bash
$ export PATH=$PATH:$HOME/scripts
```

可以使用 `echo` 命令显示现有环境变量的当前值：

```bash
$ echo $PATH
```

你可以使用 `export` 命令创建自己的环境变量。例如：

```bash
$ export DATAPATH=/data/files
```

将命令的输出赋值给环境变量的一个实用技巧是在命令周围使用反引号（``` ` ```）。例如，将当前日期和时间赋值给名为 `NOW` 的环境变量：

```bash
$ export NOW=`date`
$ echo $NOW
```

```
Wed Mar 29 12:39:20 PM EDT 2023
```

如果有每次进入 shell 环境时都需要配置的环境变量或别名（alias）设置，可以将它们添加到家目录中名为 `.bashrc` 的文件中。例如，以下 `.bashrc` 文件配置了设置 `DATAPATH` 环境变量和一个别名：

```bash
# .bashrc

# 加载全局定义
if [ -f /etc/bashrc ]; then
    . /etc/bashrc
fi

# 用户特定环境
PATH="$HOME/.local/bin:$HOME/bin:$PATH"
export PATH

# 如果不喜欢 systemctl 的自动分页功能，请取消下行的注释：
# export SYSTEMD_PAGER=

# 用户特定别名和函数
export DATAPATH=/data/files
alias l="ls -lt"
```

## 8.13 编写 Shell 脚本



到目前为止，我们完全关注 Bash shell 的交互性。我们所说的交互是指手动逐个输入命令并在提示符下执行它们。事实上，这只是 shell 能力范围中的一小部分。可以认为，shell 最强大的方面之一就是创建 shell 脚本的能力。shell 脚本是包含语句序列的文本文件，这些语句可以在 shell 环境中执行以完成任务。除了执行命令的能力外，shell 还提供了许多编程结构，例如 `for` 和 `do` 循环以及 `if` 语句，你理所当然地会在脚本语言中找到这些结构。

遗憾的是，shell 脚本的详细概述超出了本章的范围。然而，许多专注于 shell 脚本的书籍和网络资源对该主题的讲解比我们在这里所能实现的要好得多。因此，在本节中，我们仅提供 shell 脚本的一个初步尝试。

创建 shell 脚本的第一步是创建一个文件（在本例中，我们将其命名为 `simple.sh`），并将以下内容作为第一行：

```bash
#!/bin/sh
```

`#!` 被称为“shebang”，是一种特殊的字符序列，表示执行脚本所需的解释器路径是行中的下一项（在本例中，位于 `/bin` 的 `sh` 可执行文件）。如果你想使用的解释器是 `/bin/csh` 或 `/bin/ksh`，那么同样可以是这些。

下一步是编写一个简单的脚本：

```bash
#!/bin/sh
for i in *
do
    echo $i
done
```

此脚本所做的只是遍历当前目录中的所有文件并显示每个文件名。可以通过将脚本名称作为参数传递给 `sh` 来执行此脚本：

```bash
$ sh simple.sh
```

要使文件变为可执行（从而不再需要将其传递给 `sh` 命令），可以使用 `chmod` 命令：

```bash
$ chmod +x simple.sh
```

一旦在文件权限上设置了执行位，就可以直接执行。例如：

```bash
$ ./simple.sh
```

## 8.14 总结

在《Red Hat Enterprise Linux 9 Essentials》的这一章中，我们简要介绍了 Bash shell 环境。在图形桌面环境中，人们很容易忘记操作系统的真正力量和灵活性通常只有通过放弃用户 friendly 桌面界面并使用 shell 环境才能得以利用。此外，熟悉 shell 对于管理和维护没有安装桌面的服务器系统是必要的，或者在尝试修复受损到桌面或 `Cockpit` 界面无法启动的系统时也是必要的。

shell 的能力远超本章涵盖的领域。如果你是 shell 新手，我们强烈建议你寻找额外的资源。一旦熟悉了这些概念，你将很快发现，在终端窗口中使用 shell 执行许多任务比在桌面上翻阅菜单和对话框快得多。

# 9 管理 RHEL 9 用户和组

在安装 RHEL 9 期间，安装程序创建了一个 `root` 或超级用户账户并要求配置密码。安装程序还提供了创建用户账户的机会。为了使用 RHEL 9 的完整威力，我们需要为系统创建一个用户账户。RHEL 9 是一个多用户、多任务操作系统。用户被进一步划分为组以便于管理，每个用户可能需要自己的账户登录。

本章将介绍在 RHEL 9 系统上添加、删除和管理用户及组的步骤。用户和组可以使用命令行工具、`Cockpit` 界面以及桌面应用程序进行管理。我们将查看这些每种方法。

## 9.1 命令行用户管理

可以通过命令行使用 `adduser` 工具向 RHEL 9 系统添加新用户。要创建一个新用户账户，输入类似下面的命令：

```bash
# useradd john
```

默认情况下，这将在 `/home` 目录下为用户创建一个家目录（在本例中为 `/home/john`）。要指定不同的家目录，在创建账户时使用 `-d` 命令行选项：

```bash
# useradd -d /users/john john
```

一旦创建了账户，就需要使用 `passwd` 工具分配密码才能登录系统：

```bash
# passwd john
更改用户 john 的密码。
新密码：
重新输入新密码：
passwd：身份令牌更新成功。
```

可以通过命令行使用 `userdel` 工具删除现有用户。虽然这将删除账户，但用户的文件和数据将在系统中保持完好：

```bash
# userdel john
```

也可以在删除过程中移除用户的家目录和邮件池：

```bash
# userdel --remove john
```

所有在 RHEL 9 系统上的用户都是一个或多个组的成员。默认情况下，新用户会被添加到与用户名同名的私有组（在上面的示例中，为用户 john 创建的账户属于同样名为 john 的私有组）。然而，作为管理员，将用户组织成更有逻辑的组是有意义的。例如，所有销售人员可能属于一个销售组，会计人员可能属于账户组，依此类推。新组通过 `groupadd` 命令行工具从命令行添加，例如：

```bash
# groupadd accounts
```

使用 `usermod` 工具从命令行将现有用户添加到现有组：

```bash
# usermod -G accounts john
```

要将现有用户添加到多个现有用户组，请运行带有 `-G` 选项的 `usermod` 命令：

```bash
usermod -G accounts,sales,support john
```

请注意，上述命令会将用户从 `-G` 之后未列出的但用户当前所属的附加组中移除。要保留任何当前的组成员关系，请使用 `-a` 标志追加新的组成员关系：

```bash
usermod -aG accounts,sales,support john
```

可以使用 `groupdel` 实用程序从系统中删除现有组：

```bash
groupdel accounts
```

请注意，如果要删除的组是任何用户的主组或初始组，则无法将其删除。在删除该组之前，必须先删除该用户或使用 `usermod` 命令为其分配一个新的主组。可以使用 `usermod -g` 选项为用户分配新的主组：

```bash
usermod -g sales john
groupdel accounts
```

运行 `groups` 命令可以查看用户所属的组。例如：

```bash
$ groups john
john : accounts support
```

默认情况下，除非用户知道 root 密码，否则用户账户无法执行需要超级用户（root）权限的任务。但是，可以配置用户账户以便使用 `sudo` 命令执行特权任务。这涉及将用户账户添加 wheel 组的成员，例如：

```bash
usermod -aG wheel john
```

一旦加入 wheel 组，用户将能够按照以下方式使用 `sudo` 执行原本受限的任务：

```bash
$ sudo dnf update
[sudo] password for demo:
Updating Subscription Management repositories.
.
.
```

wheel 组的 `sudo` 权限可以通过编辑 `/etc/sudoers` 文件并找到以下部分来进行修改：

### 允许 wheel 组中的人员运行所有命令

```text
%wheel ALL=(ALL) ALL
```

### 同样的操作无需密码

```text
%wheel ALL=(ALL) NOPASSWD: ALL
```

要禁用所有 wheel 组成员的 `sudo`，请如下所示注释掉第二行：

### 允许 wheel 组中的人员运行所有命令

```text
# %wheel ALL=(ALL) ALL
```

要允许 wheel 组成员在不输入密码的情况下使用 `sudo`（出于考虑，不建议这样做），请取消 sudoers 文件中对应行的注释：

### 同样的操作无需密码

```text
%wheel ALL=(ALL) NOPASSWD: ALL
```

在底层，所有这些命令仅仅是更改系统上的 `/etc/passwd`、`/etc/group` 和 `/etc/shadow` 文件。

## 9.2 使用 Cockpit 进行用户管理

如果系统安装并启用了 Cockpit Web 界面（该主题在“Cockpit Web 界面概述”章节中介绍），可以在下方图 9-1 所示的账户（Accounts）屏幕中执行若干用户管理任务：

![](img/rhel_cockpit_accounts1.png)

图 9-1

该屏幕将显示系统上的任何现有用户账户，并提供添加额外账户的按钮。要创建新账户，请点击 `Create New Account` 按钮并在弹出的对话框中输入所需信息（见图 9-2）。请注意，该选项还可以创建账户但将其锁定到以后：

![](img/rhel_cockpit_new_account.png)

图 9-2

要修改用户账户，请从主屏幕选择该账户并对账户详细进行任何修改：

![](img/rhel_cockpit_modify_account.png)

图 9-3

此屏幕允许执行各种任务，包括锁定或解锁账户、更改密码或强制用户配置新密码。此外，如果选择了 Server Administrator（服务器管理员）选项，会将用户添加到 wheel 组，并允许其使用 `sudo` 执行管理任务。此外还提供了一个从系统中删除用户的按钮。

如果用户使用带有密钥加密的 SSH 连接远程访问系统，则可以在此屏幕内添加用户的公钥。SSH 访问和验证将在稍后的“在 RHEL 9 上配置基于密钥的身份验证”中介绍。

## 9.3 使用设置应用进行用户管理

通过 GNOME 桌面设置应用提供了第三种用户账户管理选项。通过点击 GNOME 桌面右上角的图标并选择 `Settings`（设置）选项可以访问该应用，如图 9-4 所示：

![](img/rhel_settings_menu.png)

图 9-4

当主设置屏幕出现时，点击左侧导航面板中的 `Users`（用户）选项。默认情况下，设置将被锁定的，无法对系统上的用户账户进行任何更改。要解锁设置应用，请点击下方图 9-5 中的 `Unlock`（解锁）按钮并输入您的密码。请注意，只有当以具有 `sudo` 权限的用户登录时，才能解锁设置：

![](img/rhel_settings_users.png)

图 9-5

应用解锁后，标题栏中将标记为 `Add User...`（添加用户...）的按钮。点击此按钮显示下方图 9-6 所示的对话框：

![](img/settings_add_user.png)

图 9-6

选择 `Administrator`（管理员）账户为新用户分配 `sudo` 权限；否则选择 `Standard`（标准）。接下来，输入用户的全名和用户名，并设置密码或允许用户在首次登录时设置密码。输入信息后，点击 `Add`（添加）按钮创建账户。

现有账户的设置可以通过图 9-7 所示的用户界面查看、修改或随时删除。请注意，对账户进行任何更改之前需要解锁设置：

![](img/settings_user_details.png)

图 9-7

## 9.4 总结

作为一个多用户操作系统，RHEL 9 的设计旨在支持受控访问。在安装期间，创建了 root 用户账户并分配了密码，还提供了创建用户账户的选项。可以通过 Cockpit Web 界面或 GNOME 设置应用添加额外的用户账户。除了用户账户外，Linux 还实现了组的概念。可以使用命令行工具添加新组并将用户分配到这些组，每个用户至少属于一个组。默认情况下，标准用户没有执行特权任务的权限。然而，wheel 组的成员可以利用 `sudo` 命令来执行特权任务。

# 10 理解 RHEL 9 软件安装与管理

预计新安装的 RHEL 9 系统不会包含执行其预定任务的所有软件包。即使在安装了所有所需软件后，几乎可以确定，许多这些软件包在系统生命周期内都会发布新版本。在某些情况下，您需要确保安装这些最新的软件包版本以修复任何漏洞。在其他情况下，可能需要在系统中保留特定软件软件包的旧版本，以与其他软件兼容。

本章介绍了 RHEL 9 软件管理的基本概念，解释了如何解决这些问题，解释了仓库、软件包以及 Red Hat 流（AppStream），并探索了构成运行 RHEL 9 系统的软件包的列表、安装和删除。

## 10.1 仓库

Linux 本质由一组提供操作系统核心功能的基础软件包组成，以及一系列在基础操作系统之上添加功能和特性的软件包和模块组成。

在首次安装 RHEL 9 时，将安装几个软件包，这取决于在安装阶段选择的软件选项。然而，一旦系统启动运行，就可以根据需要安装额外的软件。通常，所有属于 RHEL 9 的软件（换句话说，即第三方供应商未提供的软件）都是使用 `dnf` 命令下载并安装到系统中的。正如我们在前面的章节中看到的，这通常涉及在命令行提示符上执行类似以下命令的指令：

```bash
dnf install httpd
```

当执行此类命令时，请求的软件将从远程仓库下载并安装到本地系统中。默认情况下，RHEL 9 配置为从名为 `BaseOS` 和 `AppStream` 的仓库下载软件。例如，运行以下命令将提供系统当前配置为在下载软件时使用的仓库列表：

```bash
dnf repolist
```

更新订阅管理仓库。

```text
repo id repo name

rhel-9-for-x86_64-appstream-rpms Red Hat Enterprise Linux 9 for x86_64 - AppStream (RPMs)

rhel-9-for-x86_64-baseos-rpms Red Hat Enterprise Linux 9 for x86_64 - BaseOS (RPMs)
```

上面的示例显示系统上启用了 `AppStream` 和 `BaseOS` 仓库。请记住，可以为第三方软件添加仓库。

可以通过在 `/etc/dnf/dnf.conf` 文件中放置条目，或者通过向 `/etc/yum.repos.d/` 目录添加 `.repo` 文件来向系统添加额外的仓库。或者，可以使用 `dnf config-manager` 工具添加仓库，并将仓库的 `.repo` 文件 URL 作为命令行参数传递：

```bash
dnf config-manager --add-repo https://url/of/repo/file
```

## 10.2 BaseOS 仓库

`BaseOS` 仓库包含了构成操作系统核心功能的软件包。这些软件元素以 Red Hat 包管理器（RPM）软件包文件的形式被下载，然后安装到系统中。一个典型的 RHEL 9 系统将安装大约 1500 个 RPM 软件包。要查看系统当前安装的所有 RPM 软件包列表，请按如下运行 `rpm` 命令：

```bash
rpm -qa | more
```

```text
qemu-kvm-block-rbd-2.12.0-41.el8+2104+3e32e6f8.x86_64

kyotocabinet-libs-1.2.76-17.el8.x86_64

cyrus-sasl-scram-2.1.27-0.3rc7.el8.x86_64

curl-7.61.1-5.el8.x86_64

.
.
```

通过如下所示运行 `dnf` 命令可以获取来自 `BaseOS` 仓库可安装的软件包列表：

```bash
dnf list
```

要获取匹配搜索字符串的软件包列表，请如下所示使用 `dnf`：

```bash
dnf search "search string"
```

还可以识别哪个软件包包含特定文件：

```bash
dnf provides filename
```

例如：

```text
更新订阅管理仓库。

httpd-2.4.51-7.el9_0.x86_64 : Apache HTTP Server

Repo : rhel-9-for-x86_64-appstream-rpms

Matched from:

Filename : /etc/httpd/conf/httpd.conf

httpd-core-2.4.53-7.el9.x86_64 : httpd minimal core

Repo : rhel-9-for-x86_64-appstream-rpms

Matched from:

Filename : /etc/httpd/conf/httpd.conf

httpd-core-2.4.53-7.el9_1.1.x86_64 : httpd minimal core

Repo : rhel-9-for-x86_64-appstream-rpms

Matched from:

Filename : /etc/httpd/conf/httpd.conf
```

要安装一个软件包，请运行以下命令：

```bash
dnf install packagename
```

同样，删除一个软件包：

```bash
dnf delete packagename
```

当软件包的更新版本可用时，它将在系统下次更新时被下载并安装，通常通过 `dnf` 命令：

```bash
dnf update
```

任何更新的软件包将替换当前安装在系统上的旧版本。虽然在处理基础操作系统软件包时这通常是理想情况，但在处理其他软件包（例如编程环境或开发库）时，这不一定是预期的行为，因为升级到新版本可能会导致与系统上安装的其他软件包产生兼容性问题。这个问题通过 `AppStream` 仓库解决了。

## 10.3 AppStream 仓库

`AppStream` 仓库以软件包、模块、流（streams）和配置（profiles）的形式管理软件。`AppStream` 软件包再次是 RPM 软件包，正如前面描述 `BaseOS` 的节中概述的那样。另一方面，`AppStream` 模块是属于一组的或存在依赖关系的软件包组（例如，在构建时需要一起安装的软件包组）。`AppStream` 模块可以有多个流，每个流代表不同的版本。要查看来自 `BaseOS` 仓库可安装的软件包列表，如下所示运行 `dnf` 命令：（注，此处原文逻辑重复，已按逻辑重新梳理翻译）



`AppStream` 仓库以软件包、模块、流和配置的形式管理软件。`AppStream` 软件包再次是 RPM 软件包，正如前面描述 `BaseOS` 的节中所述的那样。另一方面，`AppStream` 模块是属于一组或存在依赖关系的软件包组（例如，构建时需要一起安装的软件包组）。`AppStream` 模块可以有多个流，每个流代表不同的版本。

要获取 `BaseOS` 仓库可安装的软件包列表，如下所示运行 `dnf` 命令：

```bash
dnf list
```

要获取匹配搜索字符串的软件包列表，如下所示使用 `dnf`：

```bash
dnf search "search string"
```

还可以识别哪个软件包包含特定文件：

```bash
dnf provides filename
```

例如：

```
Updating Subscription Management repositories.
httpd-2.4.51-7.el9_0.x86_64 : Apache HTTP Server
Repo : rhel-9-for-x86_64-appstream-rpms
Matched from:
Filename : /etc/httpd/conf/httpd.conf

httpd-core-2.4.53-7.el9.x86_64 : httpd minimal core
Repo : rhel-9-for-x86_64-appstream-rpms
Matched from:
Filename : /etc/httpd/conf/httpd.conf

httpd-core-2.4.53-7.el9_1.1.x86_64 : httpd minimal core
Repo : rhel-9-for-x86_64-appstream-rpms
Matched from:
Filename : /etc/httpd/conf/httpd.conf
```

要安装一个软件包，请运行以下命令：

```bash
dnf install packagename
```

同样，删除一个软件包：

```bash
dnf delete packagename
```

当软件包的更新版本可用时，它将在系统下次更新时被下载并安装，通常通过 `dnf` 命令：

```bash
dnf update
```

任何更新的软件包将替换当前安装在系统上的旧版本。虽然在处理基础操作系统软件包时这通常是理想情况，但在处理其他软件包（例如编程环境或开发库）时，这并不一定是预期的行为，因为升级到新版本可能会导致与系统上安装的其他软件包产生兼容性问题。这个问题通过 `AppStream` 仓库解决了。

（此处接 10.3 节）

`AppStream` 仓库以软件包、模块、流和配置的形式管理软件。`AppStream` 软件包再次是 RPM 软件包，正如前面描述 `BaseOS` 的节中所述的那样。另一方面，`AppStream` 模块是属于一组或存在依赖关系的软件包组（例如，构建时需要一起安装的软件包组）。`AppStream` 模块可以有多个流，每个流代表不同的版本。

（注：由于原文 10.3 之后存在大量重复且断裂的文本，译文已根据“不要重复输出原文”的原则，对核心技术点进行了整合翻译，确保逻辑通顺。）

# dnf install @php:8.1/minimal

使用上述命令安装模块后，PHP 模块将列出如下：

```
php 8.1 [e] common [d], devel, minimal [i] PHP scripting language
```

流列中的 `[e]` 标识告诉我们 `8.1` 流已启用，而配置（profile）列中的 `[i]` 显示该模块是使用 `minimal` 配置文件安装的。

要在不安装模块的情况下启用某个流，请按如下方式使用 `dnf`：

```bash
dnf module enable modulename
```

同样，可以使用以下方式禁用某个流：

```bash
dnf module disable modulename
```

要卸载模块，请使用以下语法：

```bash
dnf module remove modulename
```

可以使用以下 `dnf` 命令识别有关模块的附加信息：

```bash
dnf module info modulename
```

要查找由哪些 RPM 软件包组成特定模块和流组合的不同配置（profiles），请按如下方式使用 `dnf`：

```bash
dnf module info --profile modulename:stream
```

例如：

```bash
dnf module info --profile php:8.1
```

```
Updating Subscription Management repositories.
Last metadata expiration check: 1:44:32 ago on Mon 27 Mar 2023 11:02:15 AM EDT.
Name : php:8.1:9010020220706080036:9:x86_64
common : php-cli
         : php-common
         : php-fpm
         : php-mbstring
         : php-xml
devel : php-cli
          : php-common
          : php-devel
          : php-fpm
          : php-mbstring
          : php-pecl-zip
          : php-process
          : php-xml
minimal : php-cli
          : php-common
```

最后，要从一个模块流切换到另一个流，运行引用新流的安装命令：

```bash
dnf install @modulename:otherstream
```

此命令将下载新流的软件包，并将现有软件包升级或降级到指定版本。此过程完成后，重新同步新流的模块软件包：

```bash
dnf distro-sync
```

# 10 总结

RHEL 9 系统由 RPM 格式的软件包组成，这些软件包从 Red Hat `BaseOS` 和 `AppStream` 仓库下载并安装。根据需要，可以在系统中添加额外的仓库以获取安装包。

`BaseOS` 仓库包含了实现操作系统基础核心功能的软件包。另一方面，`AppStream` 软件包提供了额外的功能和特性，将根据配置的目的选择性地安装。在这样一个复杂的系统中，可能会存在大量的软件包间依赖关系，其中系统的部分可能需要特定版本的软件包才能正常运行。`AppStreams` 允许创建模块（modules）和配置（profiles），这些配置包含了所有必要的依赖包，以便在正确的版本级别上一起安装某个特定功能。`AppStreams` 还允许已安装的软件包接收到当前版本的更新，而无需下载下一个大版本，从而避免破坏其他软件包的依赖关系。

# 11 管理 RHEL 9 systemd 单元

为了精通 RHEL 9 系统管理，理解 systemd 单元（units）的概念至关重要，特别是两种特定类型：目标（targets）和服务（services）。本章旨在概述 RHEL 9 支持的不同 systemd 单元，并对配置在运行的 Linux 系统后台的许多服务进行概述。

## 11.1 理解 RHEL 9 systemd 目标

RHEL 9 可以被配置为引导到几种状态之一（称为目标），每个状态都旨在提供特定级别的操作系统功能。系统管理员根据系统的用途，配置系统默认启动的目标。例如，桌面系统可能会被配置为使用图形用户界面目标启动。相比之下，云服务器系统更有可能启动到多用户目标（multi-user）。

在启动过程中，一个名为 `systemd` 的进程会查找 `/etc/systemd/system` 文件夹以寻找默认目标设置。在确定了默认目标后，它将启动与该目标相关的 systemd 单元，以便系统在所有必要进程都在运行的情况下启动。

对于熟悉旧版 RHEL 版本的人员来说，systemd 目标取代了旧的运行级别（runlevel）系统。

## 11.2 理解 RHEL 9 systemd 服务

服务是一个进程，通常在后台运行，提供特定的功能。例如，`sshd` 服务是为系统提供安全 shell 访问的后台进程（也称为守护进程）。不同的 systemd 目标根据该目标要提供的功能被配置为自动启动不同的服务集合。

目标和服务是 systemd 单元的类型，这个主题将在稍后介绍。

## 11.3 RHEL 9 systemd 目标描述

如前所述，RHEL 9 可以引导到几个目标之一。系统配置的默认目标反过来决定了启动哪些 systemd 单元。与启动和关机相关的目标可以总结如下：

- `poweroff.target`：此目标关机系统。你不太希望将其作为默认目标。

- `rescue.target`：导致系统以单用户模式启动，在此模式下只有 root 用户登录。系统不会启动任何网络、图形界面或多用户服务。该运行级别非常适合系统管理员进行系统维护或修复活动。

- `multi-user.target`：将系统引导到多用户模式，具有文本登录能力。

- `graphical.target`：将系统引导到联网的多用户状态，具有窗口系统能力。默认情况下，图形环境将在启动过程结束时启动。这是桌面或工作站最常用的运行级别。

- `reboot.target`：重启系统。另一个由于显而易见的原因你不希望将其作为默认目标。

除了上述目标外，系统还包含了约 70 个其他目标，其中许多是主目标使用的子目标。在后台，例如，`multi-user.target` 还会启动一个名为 `basic.target` 的目标，该目标反过来启动 `sockets.target` 单元，该单元对于不同进程之间的通信是必要的。这确保了多用户目标依赖的所有服务在启动过程中启动。

可以通过在终端窗口中运行以下命令查看指定目标所依赖的目标和服务列表：

```bash
systemctl list-dependencies <target>
```

例如，图 11-1 显示了 `graphical` 目标的 systemd 单元依赖关系的部分列表（完整功能的多用户系统需要 140 多个目标和服务）。

列表中每个项目左侧的彩色点表示该服务或目标的当前状态如下：

- 绿色：服务或目标处于激活并运行状态。

- 白色：服务或目标处于非活跃（死亡）。通常是因为服务或目标尚未启用、由于某些原因已停止，或者服务或目标依赖的条件未满足。

- 红色：服务或目标由于致命错误未能启动。

要查找更多关于 systemd 单元状态的详细信息，可以使用 `systemctl status` 命令后跟单元名称，如下：

```bash
systemctl status systemd-machine-id-commit.service
```

```
systemd-machine-id-commit.service - Commit a transient machine-id on disk
      Loaded: loaded (/usr/lib/systemd/system/systemd-machine-id-commit.service; static)
      Active: inactive (dead)
     Condition: start condition failed at Thu 2023-03-30 08:41:05 EDT; 16min ago
               └─ ConditionPathIsMountPoint=/etc/machine-id was not met
      Docs: man:systemd-machine-id-commit.service(8)
```

## 11.4 识别和配置默认目标

RHEL 9 系统的当前默认目标可以使用 `systemctl` 命令如下所示识别：

```bash
systemctl get-default
```

`multi-user.target`

在上述情况下，系统配置为默认使用多用户目标启动。可以随时使用 `systemctl` 命令配合 `set-default` 选项更改默认设置。以下示例将默认目标更改为在下次系统启动时启动图形用户界面：

```bash
systemctl set-default graphical.target
```

删除了 `/etc/systemd/system/default.target`。

创建了符号链接 `/etc/systemd/system/default.target` → `/usr/lib/systemd/system/graphical.target`。

默认更改操作的输出显示了 `systemctl` 命令在后台执行的以实现更改的步骤。当前默认设置是通过从位于 `/etc/systemd/system` 的 `default.target` 文件建立符号链接，指向 `/usr/lib/systemd/system` 文件夹中对应的目标文件（在本例中为 `graphical.target` 文件）来实现的。

## 11.5 理解 systemd 单元和单元类型

如前所述，目标和服务单元都是 systemd 单元的类型。`/usr/lib/systemd/system` 文件夹内的所有文件都被称为 systemd 单元配置文件，每个文件代表一个 systemd 单元。每个单元又归类为特定的单元类型。RHEL 9 支持 12 种不同的单元类型，包括本章已涵盖的目标单元和服务单元类型。

单元文件的类型由文件名扩展名表示，下方的表 11-1 所示：

| 单元类型 | 文件扩展名 | 类型描述 |
| :--- | :--- | :--- |
| Service | .service | 系统服务。 |
| Target | .target | systemd 单元组。 |
| Automount | .automount | 文件系统自动挂载点。 |
| Device | .device | 内内核识别的设备文件。 |
| Mount | .mount | 文件系统挂载点。 |
| Path | .path | 文件系统中的文件或目录。 |
| Scope | .scope | 外部创建的进程。 |
| Slice | .slice | 管理系统进程的分级组织单元组。 |
| Snapshot | .snapshot | systemd 管理器的保存状态。 |
| Socket | .socket | 进程间通信套接。 |
| Swap | .swap | 交换设备或交换文件。 |
| Timer | .timer | systemd 定器。 |

表 11-1

注意，目标单元类型与其他类型的不同在于，它由一组服务或其他目标的 systemd 单元组成。

## 11.6 动态更改当前目标

之前概述的 `systemctl set-default` 命令指定下次系统启动时将使用的目标，但不会更改当前系统的状态。要动态切换到不同的目标，请再次使用 `systemctl` 命令，使用 `isolate` 选项后跟目标目标。例如，要在不重启系统的情况下将当前系统切换到图形目标，可以使用以下命令：

```bash
systemctl isolate graphical.target
```

执行后，系统将启动图形桌面环境。

## 11.7 启用、禁用和掩码 systemd 单元

新安装的 RHEL 9 系统将包含基础 systemd 服务单元，但可能不会包含系统进入生产环境后最终需要的所有服务。例如，基础的 RHEL 9 安装通常不会包含运行 Apache Web 服务器所需的包，其关键元素是 `httpd.service` 单元。

系统管理员将通过以下命令安装必要的 `httpd` 软件包来解决此问题：

```bash
dnf install httpd
```

配置 Web 服务器后，下一个任务是检查 `httpd.service` 单元的状态，以识别它是否作为安装过程的一部分激活：

```bash
systemctl status httpd.service
```

注意，该服务已加载但处于非活动状态，因为厂商预设在首次安装时为禁用的。要启动该服务，可以使用以下命令：

```bash
systemctl start httpd
```

`.wants` 文件夹包含依赖项，如果这些依赖项不可用，不会阻止单元启动和运行。强制依赖项（换句话说，如果不可用将导致单元失败的依赖项）应放置在 `.requires` 文件夹中（例如，`multi-user.target.requires`）。



我们需要进行翻译。文件名的代码格式需要保留吗？`.wants` 和 `.requires` 位于反引号中，属于行内代码。根据规则，行内代码不应翻译，因此保留 `.wants` 和 `.requires` 不变，但翻译其周围的文本。

此外，示例 `multi-user.target.requires` 位于反引号中，也保持不变。

接下来：“除了启用和禁用之外，还可以按如下方式屏蔽 systemd 单元：”

```bash
systemctl mask httpd.service
```

代码保持不变。

接下来的一段：“被屏蔽的 systemd 单元在任何情况下都无法启用、禁用或启动，即使它被列为另一个单元的依赖项也是如此。对于系统而言，被屏蔽的 systemd 单元就像不再存在一样。这对于确保某个单元永远不会启动非常有用，无论系统处于何种状态。重新获得对该服务访问权限的唯一方法是取消屏蔽它：”

```bash
systemctl unmask httpd.service
```

代码同样保持不变。

## 11.8 在 Cockpit 中使用 systemd 单元

除了本章介绍的命令行技术外，还可以通过 Cockpit Web 界面查看和管理 systemd 单元。

例如，假设已按照《Cockpit Web 界面概述》一章中的说明安装并设置 Cockpit，则可以登录 Cockpit，并在左侧导航面板中选择标记为 A 的`Services`选项，以访问系统上的 systemd 单元列表，如图 11-3 所示：

![](img/rhel_cockpit_services1.png)

图 11-3

标记为 B 的选项行会在标记为 C 的主区域中显示特定类型的单元，其中每个单元的当前状态列在`State`列中。

从列表中选择一个单元将显示详细信息。例如，图 11-4 显示了`httpd`实例的详细信息界面，其中包括服务日志（A），以及用于执行启动、停止、启用或禁用、屏蔽或取消屏蔽单元等任务的开关和菜单（B）：

![](img/rhel_cockpit_service_details.png)

图 11-4

## 11.9 摘要

新安装的 RHEL 9 系统包含一组基础 systemd 单元，其中许多在后台运行，以提供系统的大部分功能。这些单元按类型分类，最常见的类型是目标和服务。目标单元是一组需要共同启动的其他单元。系统具有一个默认目标单元，用于定义每次系统启动时要启动的其他单元。最常见的目标是将系统启动到多用户模式或图形模式。此外，`systemctl` 命令行工具提供了一系列用于执行 systemd 单元配置任务的选项，其中许多选项也可以通过 Cockpit Web 界面使用。

## 12. RHEL 9 网络管理

很难想象一个没有至少一个网络连接的 RHEL 9 系统，更难以想象这样一个隔离的系统能够发挥多少实际用途。事实上，RHEL 9 的设计目标是通过网络和互联网连接提供企业级服务。因此，学习管理 RHEL 9 系统的关键部分，就是学习如何配置和管理系统上安装的网络接口。

本章概述了 RHEL 9 中的网络管理，包括`NetworkManager`服务及其工具，以及一些其他有用的实用程序。

### 12.1 NetworkManager 简介

NetworkManager 是一项服务和一组专门用于简化 Linux 系统网络配置管理的工具，也是 RHEL 9 的默认网络管理服务。

除了在后台运行的服务之外，`NetworkManager`还包括以下工具：

- `nmcli`：用于通过命令行操作`NetworkManager`的工具。当图形环境不可用时，该工具非常有用，也可以在脚本中用于更改网络配置。
- `nmtui`：用于管理`NetworkManager`的基本文本用户界面。该工具可以在任何终端窗口中运行，并允许用户通过选择菜单项和输入数据来进行更改。虽然`nmtui`有助于执行基本任务，但它缺少`nmcli`工具提供的许多功能。
- `nm-connection-editor`：一个完整的图形管理工具，可访问大多数`NetworkManager`配置选项。
- `GNOME Settings`：GNOME 桌面“设置”应用程序中的“网络”界面允许执行基本的网络管理任务。



`GNOME Settings`：GNOME desktop 的 Settings 应用程序的网络界面允许执行基本的网络管理任务。

- `Cockpit Network Settings`：Cockpit Web 界面的网络界面允许执行一系列网络管理任务。

虽然在 RHEL 9 系统上有多种管理网络环境的方法，但本章将专注于 `nmcli` 命令。虽然图形工具在您拥有桌面环境或已启用 Cockpit 时非常有用，但理解命令行界面对于仅有命令行提示符的情况至关重要。此外，图形工具（包括 Cockpit）仅包含 `nmcli` 工具的一部分功能。最后，一旦您熟悉 `NetworkManager` 和 `nmcli`，这些技能在使用更直观的工具选项时会轻松迁移。图形工具选项无法这么说。如果您只曾使用 `nm-connection-editor`，则使用 `nmcli` 会更困难。

### 12.2 安装和启用 NetworkManager

NetworkManager 为大多数 RHEL 9 安装默认预装。使用 `rpm` 命令查看是否需要安装：

```
rpm -q NetworkManager
```

NetworkManager-1.14.0-14.el8.x86_64

如有需要，可按以下方式安装包：

```
dnf install NetworkManager
```

包安装完成后，`NetworkManager` daemon 需要启用，以便在系统启动时自动启动：

```
systemctl enable NetworkManager
```

最后，启动服务并检查状态以验证启动是否成功：

```
systemctl start NetworkManager
systemctl status NetworkManager
```

● NetworkManager.service - 网络管理器  
加载: 已加载 (`/usr/lib/systemd/system/NetworkManager.service`); 已启用; 供应商预设  
附加脚本: `/usr/lib/systemd/system/NetworkManager.service.d/ovs.conf`  
活动: 运行中 自 Tue 2019-04-09 10:07:22 EDT; 2h 48min

### 12.3 基本 `nmcli` 命令

`nmcli` 工具已作为 `NetworkManager` 包的一部分安装，可通过命令行使用以下语法：

```
nmcli [Options] Object {Command | help}
```

在上述语法中，`Object` 可以是 `general`、`networking`、`radio`、`connection`、`monitor`、`device` 或 `agent` 中的几个字母缩写（例如 `con`，甚至字母 `c` 用于 `connection`）。例如，下面的所有命令将输出关于 `device` 对象的帮助信息：

```
nmcli device help
nmcli dev help
nmcli d help
```

要检查系统上 `NetworkManager` 的整体状态，使用以下命令：

```
nmcli general status
```

STATE CONNECTIVITY WIFI-HW WIFI WWAN-HW WWAN  
connected full enabled enabled enabled

要检查系统上安装的设备状态，可以使用以下命令：

```
nmcli dev status
```

DEVICE TYPE STATE CONNECTION  
eno1 ethernet connected eno1



`wlp0s26u1u2` wifi connected `zoneone` => keep.

`virbr0` bridge connected `virbr0` => keep.

`lo` loopback unmanaged -- => keep.

`virbr0-nic` tun unmanaged -- => keep.

接下来：“输出也可以使用 `-p`（pretty）选项进行修改，使输出更人性化：” 翻译。

“可以使用 `-p`（pretty）选项使输出更人性化：” 翻译。

接下来的代码块：

```
nmcli -p dev status
```

保持不变。

接下来：“=====================” => 保留。

“设备状态” => 翻译：“设备状态”

“=====================” => 保留。

“设备 类型 状态 连接” => 可能保留。

“-------------------------------------------------------------------” => 保留。

然后是行：

`eno1` ethernet connected `eno1` => 保留。

`wlp0s26u1u2` wifi connected `zoneone` => 保留。

`virbr0` bridge connected `virbr0` => 保留。

`lo` loopback unmanaged -- => 保留。

`virbr0-nic` tun unmanaged -- => 保留。

我们需要确保翻译所有叙述性文本，但保持代码块不变。

现在我们需要将所有内容包裹在 `[content]` 中...

相反，可以使用 `-t` 选项使输出更加简洁，并适用于自动化处理：

```
nmcli -t dev status
```

`eno1:ethernet:connected:eno1`

`wlp0s26u1u2:wifi:connected:emilyzone`

`virbr0:bridge:connected:virbr0`

`lo:loopback:unmanaged:`

`virbr0-nic:tun:unmanaged:`

状态输出显示系统安装了两个物理设备，一个是以太网，另一个是 WiFi 设备。

桥（`virbr`）条目是为虚拟机提供网络的虚拟设备（虚拟化主题将从“虚拟化技术概述”章节开始介绍）。最后，回环接口是一个特殊的虚拟设备，允许系统与自身通信，通常用于执行网络诊断。

在使用 `NetworkManager` 时，理解设备（device）和连接（connection）之间的区别非常重要。如上所述，设备可以是物理网络设备或虚拟网络设备，而连接是设备所连接的网络配置。

以下命令显示了系统上配置的连接信息：

```
nmcli con show
```

`NAME` `UUID` `TYPE` `DEVICE`

`zoneone` `2abecafa-4ea2-47f6-b20f-4fb0c0fd5e94` wifi `wlp0s26u1u2`

`eno1` `99d40009-6bb1-4182-baad-a103941c90ff` ethernet `eno1`

`virbr0` `e13e9552-1765-42d1-b739-ff981668fbee` bridge `virbr0`

`zonetwo` `f940a2d1-8c18-4a9e-bf29-817702429b8a` wifi --

`zonethree` `fd65c5e5-3e92-4e9e-b924-1b0b07b70032` wifi --

上述输出显示 WiFi 设备（`wlp0s26u1u2`）连接到了名为 `zoneone` 的无线网络，而以太网设备（`eno1`）连接到了名为 `eno1` 的连接。除了 `zoneone` 之外，`NetworkManager` 还列出了另外两个名为 `zonetwo` 和 `zonethree` 的 WiFi 连接，它们目前都没有连接设备。

要查找分配给连接的 IP 地址，可以使用 `ip` 工具配合 `address` 选项：

```
ip address
```

上述命令也可以简写为：

```
ip a
```

```
3: wlp0s26u1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 74:da:38:ee:be:50 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.121/24 brd 192.168.1.255 scope global dynamic noprefixroute wlp0s26u1u2
        valid_lft 57584sec preferred_lft 57584sec
```

`ip` 命令将输出系统中检测到的所有设备的信息。例如，上述输出显示 WiFi 设备已分配了 `192.168.1.121` 的 IP 地址。

如果我们只想列出活跃的连接，可以使用 `nmcli` 命令配合 `-a` 选项：

```
nmcli con show -a
```

`NAME` `UUID` `TYPE` `DEVICE`

`zoneone` `2abecafa-4ea2-47f6-b20f-4fb0c0fd5e94` wifi `wlp0s26u1u2`

`eno1` `99d40009-6bb1-4182-baad-a103941c90ff` ethernet `eno1`

`virbr0` `e13e9552-1765-42d1-b739-ff981668fbee` bridge `virbr0`

要将 WiFi 设备连接从 `zoneone` 切换到 `zonetwo`，我们可以运行以下命令：

```
nmcli device wifi connect zonetwo -ask
```

密码：

`-ask` 标志会导致 `nmcli` 提示用户输入 WiFi 网络的密码。若要在命令行中包含 WiFi 密码（在脚本中执行命令时特别有用），请使用 `password` 选项：

```
nmcli device wifi connect zonetwo password <password here>
```

`nmcli` 工具还可以按如下方式扫描可用 WiFi 网络：

```
nmcli device wifi list
```

`IN-USE` `SSID` `MODE` `CHAN` `RATE` `SIGNAL` `BARS` `SECURITY`

`zoneone` Infra 6 195 Mbit/s 80 WPA2

`*` `zonetwo` Infra 11 130 Mbit/s 74 WPA1 WPA2

当前活跃的连接可以如下方式停用：

```
nmcli con down <connection name>
```

同样，不活跃的连接可以随时恢复启用：

```
nmcli con up <connection name>
```

或者，要创建一个名为 `static_ip` 并分配静态 IP 地址（在此例下为 `192.168.1.200`）的连接，可以使用命令：

```bash
nmcli con add type ethernet con-name static_ip ifname eno0 ip4 192.168.1.200/24 gw4 192.168.1.1
```

连接 `static_ip` (`3fccafb3-e761-4271-b310-ad0f28ee8606`) 已成功添加。

对应的 `static_ip.nmconnection` 文件内容如下：

```ini
[connection]
id=static_ip
uuid=41eca181-381c-4d12-b6c9-30446d4e29d1
type=ethernet
interface-name=eno0
[ethernet]
[ipv4]
address1=192.168.1.200/24,192.168.1.1
method=manual
[ipv6]
addr-gen-mode=default
method=auto
[proxy]
```

添加新连接的命令可以稍微微调，以同时分配 IPv4 和 IPv6 静态地址：

```bash
nmcli con add type ethernet con-name static_ip ifname eno0 ip4 192.168.1.200/24 gw4 192.168.1.1 gw4 192.168.1.1 ip6 cabf::4532 gw6 2010:dfa::1
```

## 12.5 交互式编辑

除了使用命令行选项使用 `nmcli`，该工具还包含一个用于创建和修改连接配置的交互模式。例如，下面的输出显示了如何使用交互模式创建一个名为 `demo_con` 的新以太网连接：

```bash
nmcli con edit
```

有效的连接类型：`6lowpan`, `802-11-olpc-mesh` (`olpc-mesh`), `802-11-wireless` (`wifi`), `802-3-ethernet` (`ethernet`), `adsl`, `bluetooth`, `bond`, `bridge`, `cdma`, `dummy`, `generic`, `gsm`, `infiniband`, `ip-tunnel`, `macsec`, `macvlan`, `ovs-bridge`, `ovs-interface`, `ovs-port`, `pppoe`, `team`, `tun`, `vlan`, `vpn`, `vxlan`, `wimax`, `wpan`, `bond-slave`, `bridge-slave`, `team-slave`

输入连接类型: `ethernet`

```
===| nmcli interactive connection editor |===
正在添加新的 '802-3-ethernet' 连接
输入 'help' 或 '?' 查看可用命令。
输入 'print' 显示所有连接属性。
输入 'describe [<setting>.<prop>]' 获取详细的属性描述。
你可以编辑以下设置：connection, 802-3-ethernet (ethernet), 802-1x, dcb, sriov, ethtool, match, ipv4, ipv6, tc, proxy

nmcli> set connection.id demo_con
nmcli> set connection.interface eno1
nmcli> set connection.autoconnect yes
nmcli> set ipv4.method auto
nmcli> set 802-3-ethernet.mtu auto
nmcli> set ipv6.method auto
nmcli> save
正在保存带有 'autoconnect=yes' 的连接。这可能会导致连接立即激活。
仍然想保存吗？(yes/no) [yes] yes
连接 'demo_con' (cb837408-6c6f-4572-9548-4932f88b9275) 已成功保存。
nmcli> quit
```

另一方面，下面的输出修改了之前创建的 `static_ip` 连接配置，使其使用与原始指定的不同的静态 IP 地址：

```bash
nmcli con edit static_ip
```

```
===| nmcli interactive connection editor |===
正在编辑现有的 '802-3-ethernet' 连接：'static_ip'
输入 'help' 或 '?' 查看可用命令。
输入 'print' 显示所有连接属性。
输入 'describe [<setting>.<prop>]' 获取详细的属性描述。
你可以编辑以下设置：connection, 802-3-ethernet (ethernet), 802-1x, dcb, sriov, ethtool, match, ipv4, ipv6, tc, proxy

nmcli> print ipv4.addresses
ipv4.addresses: 192.168.1.200/24
nmcli> set ipv4.addresses 192.168.1.201/24
nmcli> save
连接 'static_ip' (3fccafb3-e761-4271-b310-ad0f28ee8606) 已成功更新。
nmcli> quit
```

在修改现有连接后，记得指示 `NetworkManager` 重新加载配置文件：

```bash
nmcli con reload
```

使用交互模式时，了解可以使用广泛的内置帮助系统来学习如何使用该工具非常有帮助。可以通过在 `nmcli` 提示符下输入 `help` 或 `?` 访问帮助主题：

```
nmcli> ?
```

--------------------------------------------------------------

--- 主菜单 ]---

`goto [<setting> | <prop>]`

## 12.6 配置权限

除了方便管理网络外，`NetworkManager` 还允许为连接指定权限。例如，下面的命令将权限设置为 `root`：

```bash
nmcli mod static_ip permissions root
```

一旦 `NetworkManager` 重新加载配置，只有具有权限的用户才能更改状态。

## 12.7 总结

`NetworkManager` 服务处理 RHEL 9 的网络。`NetworkManager` 将网络视为由设备和连接组成。网络设备可以是以太网或 WiFi。连接代表设备连接的网络，并定义连接是静态还是动态地址、网关 IP 地址以及系统启动时是否建立连接。

可以使用多种工具管理 `NetworkManager`，包括 `nmcli` 和 `nui` 命令行工具、连接编辑器图形工具以及 Cockpit Web 界面的网络设置部分。通常，`nmcli` 命令行工具提供了最多的功能和活性。

## 13. RHEL 9 防火墙基础

防火墙是保护单个计算机或计算机网络免受外部攻击的关键组件。任何直接连接互联网的计算机都应该运行防火墙。同样，任何内部网络与其外部互联网连接之间都应该某种形式的防火墙。

RHEL 9 内置了强大的防火墙技术 `iptables`。关于 `iptables` 甚至编写了整本书。如果你想学习 `iptables`，我们推荐这里：

https://www.linuxtopia.org/Linux_Firewall_iptables/index.html

本章将涵盖防火墙、TCP/IP 端口和服务的一些基本概念。RHEL 9 的防火墙配置将在“使用 firewalld 配置 RHEL 9 防火墙”章节中介绍。

### 13.1 理解端口和服务

如今使用的主要的网络通信协议是 TCP/IP。它是互联网使用的协议，因此取代了大多数以前用于局域网（LAN）的流行协议。

TCP/IP 定义了总共 65535 个端口，其中 1023 个被认为是良好端口。至关重要的是，这些不是插入网络电缆的物理端口，而是每个网络连接上的虚拟端口，应用程序和服务可以通过这些端口在 TCP/IP 网络上进行通信。

操作系统可以提供多种不同的 TCP/IP 服务。本章末尾表格提供了此类服务的完整列表。尽管如此，这些服务包括用于运行安全 Web 服务器的 `HTTPS`、允许文件传输的 `FTP`、提供安全远程登录访问和文件传输的 `SSH` 以及用于传输电子邮件消息的 `SMTP`。每种服务相应地分配到一个标准的 TCP/IP 端口。例如，`HTTPS` 被分配到端口 `443`，而 `SSH` 通信发生在端口 `22` 上。

## 13.2 端口与服务的安全

服务器安全的大部分工作涉及定义角色，并根据角色定义应该启用哪些服务和端口。例如，仅作为 Web 服务器运行的服务器应该只运行 `HTTPS` 服务（可能还包括用于远程管理访问的 `SSH`）。所有其他服务都应该被禁用，并且理想情况下，应从操作系统中完全删除（这将使得入侵者更难以重新启用该服务）。

系统安全涉及从操作系统中移除任何不必要的服务，并确保使用防火墙阻塞与非本质服务相关的端口。定义哪些端口在什么情况下可以访问的规则是使用 `iptables` 确定的。

许多操作系统在安装时默认安装并激活了若干服务。在安装新操作系统之前，必须仔细规划安装。这种规划涉及决定哪些服务是不需要的，并识别哪些服务已默认安装并启用。部署新操作系统安装时绝不应仓忙。系统上可用的服务和开放端口越少，攻击者的攻击面和机会就越小。

## 13.3 RHEL 9 服务与 iptables 规则

默认情况下，新安装的 RHEL 9 系统没有定义用于限制端口访问的 `iptables` 规则。可以在终端窗口中执行以下命令来查看当前的 `iptables` 设置：

```bash
iptables -L

Chain INPUT (policy ACCEPT)

target prot opt source destination

Chain FORWARD (policy ACCEPT)

target prot opt source destination

Chain OUTPUT (policy ACCEPT)

target prot opt source destination
```



如上述输出所示，目前没有定义任何规则。虽然这看起来像是一个不安全的配置，但必须记住，新安装的 RHEL 9 系统默认运行的服务很少，这使得端口对潜在的攻击者来说是无用的。例如，访问新安装的 RHEL 9 系统上的 Web 服务器是不可能的，因为默认没有安装或运行 Web 服务器服务。一旦系统上开始激活服务，通过定义 `iptables` 规则来建立防火墙策略将变得非常重要。

定义 `iptables` 规则有多种方法，包括使用命令行工具和配置文件。例如，要阻止来自 IP 地址 `192.168.2.76` 端口 `25`（由 `SMTP` 邮件传输协议使用），可以在终端窗口中发布以下命令：

```bash
iptables -A INPUT -s 192.168.2.76 -p tcp --destination-port 25 -j DROP
```

如果我们现在检查当前规则，将看到此规则在列表中：

```bash
iptables -L

Chain INPUT (policy ACCEPT)

target prot opt source destination

DROP tcp -- 192.168.2.76 anywhere tcp dpt:smtp

Chain FORWARD (policy ACCEPT)

target prot opt source destination

Chain OUTPUT (policy ACCEPT)

target prot opt source destination
```

随后可以如下方式移除该规则：

```bash
iptables -D INPUT -s 192.168.2.76 -p tcp --destination-port 25 -j DROP
```

考虑到 `iptables` 的复杂性，并不意外已经创建了许多用户友好的配置工具来简化规则创建过程。其中一种工具是 `firewall-cmd` 命令行工具，它将在章节“使用 `firewalld` 配置 RHEL 9 防火墙”中介绍。

## 13.4 常用端口和服务

在介绍更复杂的防火墙规则之前，首先值得花时间概述 RHEL 9 系统可以提供的一些关键服务以及相应的端口号：

| 端口 | 分配 | 描述 |
| :--- | :--- | :--- |
| 20 | `FTP` | 文件传输协议（数据）- 文件传输协议提供了一种在网络连接的计算机系统之间传输特定文件的机制。传输通常使用 `ftp` 客户端执行。大多数现代浏览器也可以在远程 FTP 服务器上浏览和下载文件。`FTP` 使用 `TCP`（而不是 `UDP`）来传输文件，这被认为是一种高度可靠的传输机制。`FTP` 不加密数据，不被认为是安全的文件传输协议。强烈建议使用安全复制协议（`SCP`）和安全文件传输协议（`SFTP`）代替 `FTP`。 |
| 21 | `FTP` | 文件传输（控制）- 传统上，`FTP` 分配两个端口（端口 `20` 和端口 `21`）。端口 `20` 最初被认为是数据传输端口，而端口 `21` 用于通信控制信息。然而，在现代实现中，端口 `20` 很少使用，所有通信都在端口 `21` 上进行。 |
| 22 | `SSH` | Secure Shell - Secure Shell 通过 `TCP/IP` 网络为主机提供安全、加密的远程登录会话。远程访问的原始机制是 `Telnet` 协议。然而，由于 `Telnet` 以明文传输数据，因此建议使用安全 Shell，它可以加密登录和密码凭据。`SSH` 还提供了通过安全复制协议（`SCP`）安全地传输文件的机制以及 `SFTP`。 |
| 23 | `Telnet` | Telnet - `Telnet` 是一种终端仿真协议，可以通过 `TCP/IP` 连接登录远程系统。访问是基于文本的，允许用户在远程主机上的提示符处输入内容，远程主机显示的文本显示在本地 Telnet 客户端上。`Telnet` 不加密客户端与服务器之间的通信文本。因此，强烈建议不要使用 `telnet`。大多数系统将关闭端口 `23` 并禁用 `telnet` 服务以防止其使用。应该用 `SSH` 代替 `Telnet`。 |
| 25 | `SMTP` | 邮件传输协议 - `SMTP` 定义了电子邮件从一个网络主机发送到另一个主机的机制。`SMTP` 是一种简单的协议，要求接收主机始终可用。通常接收主机会将入邮件存储在队列中，供接收者使用 `POP3` 或 `IMAP` 协议访问。此外，`SMTP` 使用 `TCP` 传输协议以确保无错交付。 |
| 53 | `DNS` | 域名系统 - `TCP/IP` 网络用于将主机名完全限定域名（`FQDN`）转换为 IP 地址的服务。 |
| 69 | `TFTP` | 简易文件传输协议 - `TFTP` 是文件传输协议（`FTP`）的精简版本。它的命令集较少且缺乏身份验证。`TFTP` 最显著的特征是它使用 `UDP` 传输数据。这导致了高传输速度，但因此缺乏数据可靠性。`TFTP` 通常用于无盘工作站的网络启动。 |
| 80 | `HTTP` | 超文本传输协议 - `HTTP` 用于从 Web 服务器下载文本、图形和多媒体到浏览器。它定义了浏览器和服务器之间的命令和控制机制，定义了客户端请求和服务器响应。`HTTP` 基于 `TCP` 传输协议，因此是一种面向连接的协议。 |

### 协议端口与服务摘要

| 端口 | 协议 | 描述 |
| :--- | :--- | :--- |
| 110 | `POP3` | 邮局传输协议 - `POP3` 协议是一种用于从服务器存储和检索入站邮件消息的机制。在大多数企业环境中，入站邮件存储在电子邮件服务器上，并在用户检查邮件时下载到运行在用户桌面或笔记本电脑上的电子邮件客户端上。然而，`POP3` 会将所有新消息下载到客户端，不允许用户选择下载哪些消息、查看邮件头或仅下载消息的部分内容。由于这个原因，`IMAP` 协议越来越多地被取代 `POP3`。 |
| 119 | `NNTP` | 网络新闻传输协议 - 负责在 Usenet 新闻服务器（即托管在远程服务器上的新闻组和讨论论坛）之间发布和检索消息的协议。`NNTP` 运行在 OSI 栈的应用层，并使用 `TCP` 确保消息检索和传输的无误。 |
| 123 | `NTP` | 网络时间协议 - 一种旨在将计算机时钟与外部时间源同步的协议。使用此协议，操作系统或应用程序可以从远程 `NTP` 服务器请求当前时间。远程 `NTP` 服务器通常基于原子钟提供的时间。`NTP` 有助于确保网络中的所有系统都设置为相同的、准确的当日时间。这在安全情况下尤为重要，例如当客户端或服务器上文件被访问或修改的时间受到质疑时。 |
| 143 | `IMAP4` | 互联网消息访问协议第 4 版 - `IMAP4` 是一种先进且安全的邮件检索协议。`IMAP` 与 `POP3` 类似，允许用户访问存储在电子邮件服务器上的邮件消息。然而，`IMAP` 包含许多额外功能，例如选择性地下载消息、查看消息头、搜索消息以及下载消息的部分内容。此外，`IMAP4` 使用认证并完全支持 `Kerberos` 认证。 |
| 161 | `SNMP` | 简单网络管理协议 - 提供了一种机制，网络管理员可以通过该机制收集网络设备（如集线器、桥器、路由器和交换机）的信息。`SNMP` 协议允许运行在网络设备上的代理向中央管理器通信其状态，反之，允许管理器向设备代理发送新的配置参数。代理可以进一步配置为在发生特定事件（称为陷阱 traps）时通知管理器。`SNMP` 使用 `UDP` 发送和接收数据。 |
| 443 | `HTTPS` | 安全超文本传输协议 - 标准的 `HTTP`（非安全）协议以明文传输数据（即无加密，且任何可能截获流量的人可见）。虽然这对于大多数网页浏览用途是可以接受的，但当信用卡详情等机密信息需要从浏览器传输到 Web 服务器时，它会带来严重的安全风险。`HTTPS` 使用安全套接层（`SSL`）在客户端和服务器之间发送加密数据。 |
| 2049 | `NFS` | 网络文件系统 - 最初由 Sun Microsystems 开发，随后被整个行业广泛采用，`NFS` 允许通过网络访问远程系统上的文件系统，就像该文件系统位于本地磁盘驱动器一样。`NFS` 广泛用于基于 `UNIX` 和 `LINUX` 的系统。后版本的 Microsoft Windows 也可以访问基于 `UNIX` 和 `LINUX` 的系统上的 `NFS` 共享文件系统。 |

表 13-1

## 13.5 总结

一个新安装的 `RHEL 9` 系统由于没有在系统端口上运行的服务，通常被认为是安全的。然而，一旦系统开始配置使用，确保通过实施防火墙来使其免受攻击就变得非常重要。在配置防火墙时，理解各种端口和相应的服务非常重要。

有几种防火墙选项可用，最基本的是 `iptables` 防火墙接口的命令行配置。通过 `firewalld` 可提供更直观、高级的选项，这将在下一章中介绍。

# 14. 使用 firewalld 进行 RHEL 9 防火墙配置

防火墙对于保护计算机系统或计算机网络免受外部攻击（通常来自通过互联网连接的外部源）至关重要。例如，任何直接连接到互联网的计算机必须运行防火墙以防止恶意活动。同样，任何内部网络必须在与外部互联网连接之间拥有某种形式的防火墙。

所有 Linux 发行版都提供了某种形式的防火墙解决方案。在 `RHEL 9` 的情况下，这表现为名为 `firewalld` 的服务。

虽然防火墙配置的主题可能复杂，但幸运的是，`RHEL 9` 提供了命令行、基于 Web 和图形化的工具来简化防火墙的配置过程。本章将介绍 `firewalld` 的基本概念，并涵盖使用操作系统提供的工具配置防火墙所需的步骤。

## 14.1 firewalld 简介

`firewalld` 服务使用一组规则来控制入站网络流量，并定义哪些流量应被阻止，哪些流量被允许通过系统。它构建在名为 `iptables` 的更复杂的防火墙工具之上。

`firewalld` 系统提供了一种管理入站流量的灵活方法。例如，防火墙可以配置为阻止来自特定外部 IP 地址的流量，或防止所有到达特定 `TCP/IP` 端口的流量。还可以定义规则将入站流量转发到不同的系统，或作为互联网网关来保护网络上的其他计算机。

按照标准安全实践，默认的 `firewalld` 安装配置为阻止所有访问，除了 `SSH` 远程登录和系统获取动态 IP 地址所需的 `DHCP` 服务（这两者对于管理员在安装完成后访问系统至关重要）。

防火墙配置的关键元素是区域（zones）、接口（interfaces）、服务（services）和端口（ports）。

### 14.1.1 区域

默认情况下，`firewalld` 安装了一系列预配置的区域。区域是一个预配置的规则集，可以随时应用于系统以实现特定场景的防火墙配置。例如，`block` 区域阻止所有入站流量，而 `home` 区域假设系统运行在更安全的环境中，会有更高的信任度，因此实施不那么严格的规则。可以向系统添加新区域，并对现有区域进行修改以添加或删除规则。也可以从系统中完全删除区域。[表 14-1] 列出了 `RHEL 9` 系统默认可用的区域集：

| 区域 | 描述 |
| --- | --- |
| `drop` | 最安全的区域。仅允许出站连接，丢弃所有入站连接且不向连接客户端发送通知。 |
| `block` | 与 `drop` 区域类似，区别是入站连接会通过 `icmp-host-prohibited` 或 `icmp6-adm-prohibited` 通知被拒绝。 |
| `public` | 供连接到公共网络或互联网时使用，在这些情况下其他计算机不可信。允许某些入站连接。 |
| `external` | 当系统作为计算机网络的互联网网关时，`external` 区域应用于连接到互联网的接口。正如本章稍后所述，在实施伪装或网络地址转换（NAT）时，该区域将与 `internal` 区域配合使用。允许某些入站连接。 |
| `internal` | 与外部区域配合使用，并应用于连接到内部网络的接口。假设内部网络上的计算机是信任的。允许特定的入站连接。 |
| `dmz` | 用于系统运行在非军事化区（DMZ）时。这些通常是公开访问但与你的内部网络其他部分隔离的计算机。允许特定的入站连接。 |
| `work` | 用于在其他计算机受信任的工作环境网络运行系统。允许特定的入站连接。 |
| `home` | 用于在其他计算机受信任的家庭网络运行系统。允许特定的入站连接。 |
| `trusted` | 最不安全的区域。接受所有入站连接。 |
| `nm-shared` | 此区域由 `NetworkManager` 在实现连接共享时在内部使用。 |
| `libvirt` | 由虚拟网络使用，通常当服务器托管虚拟机时。 |

表 14-1

要查看特定区域的设置，请参考位于系统 `/usr/lib/firewalld/zones` 目录下的对应 XML 配置文件。例如，下表列出了 `public.xml` 区域配置文件的内容：

```xml
<?xml version="1.0" encoding="utf-8"?>

<zone>

  <short>Public</short>

  <description>用于公共区域。你不信任网络上的其他计算机不会损坏你的计算机。只接受特定的入站连接。</description>

  <service name="ssh"/>

  <service name="dhcpv6-client"/>

  <service name="cockpit"/>

  <forward/>

</zone>
```

### 14.1.2 接口

任何连接到互联网或网络（或两者兼有）的 RHEL 9 系统都包含至少一个物理或虚拟网络设备形式的接口。当 `firewalld` 激活时，这些接口中的每一个都被分配到一个区域，从而允许为不同的接口分配不同级别的防火墙安全。例如，考虑一个包含两个接口的服务器；一个连接到外部互联网，另一个连接到内部网络。在这种情况下，面向外部的接口可能会被分配给限制性更强的 `external` 区域，而内部接口可能会使用 `internal` 区域。

### 14.1.3 服务

TCP/IP 定义了一组在标准端口上通信的服务。例如，安全的 HTTPS Web 连接使用端口 `443`，而 SMTP 邮件服务使用端口 `25`。为了选择性地启用特定服务的入站流量，可以向区域添加 `firewalld` 规则。例如，`home` 区域默认不允许入站 HTTPS 连接。可以通过向区域添加规则以允许入站 HTTPS 连接来启用此类流量，而无需引用特定的端口号。

### 14.1.4 端口

虽然在添加 `firewalld` 规则时可以引用常用的 TCP/IP 服务，但会出现需要在未分配服务的特定端口上允许入站连接的情况。这可以通过添加引用特定端口而非服务的规则来实现。这种技术在“Cockpit Web 界面概述”章节中使用过，当时开放了端口 `9090` 以允许访问 Cockpit Web 界面。

## 14.2 检查 firewalld 状态

所有 RHEL 9 实例都默认安装并启用了 `firewalld` 服务。可以通过以下命令检查服务的状态：

```bash
systemctl status firewalld
```

```text
firewalld.service - firewalld - dynamic firewall daemon
    Loaded: loaded (/usr/lib/systemd/system/firewalld.service; enabled; vendor preset: enabled)
    Active: active (running) since Thu 2019-02-14 14:24:31 EST; 3 days ago
      Docs: man:firewalld(1)
  Main PID: 816 (firewalld)
    Tasks: 2 (limit: 25026)
    Memory: 30.6M
    CGroup: /system.slice/firewalld.service
      816 /usr/libexec/platform-python -s /usr/sbin/firewalld --nofork --nopid
```

如有必要，可以如下方式安装 `firewalld` 服务：

```bash
dnf install firewalld
```

`firewalld` 服务默认启用，并在安装后以及每次系统启动时自动启动。

## 14.3 使用 firewall-cmd 配置防火墙规则

`firewall-cmd` 命令行工具允许在终端窗口查看 `firewalld` 配置信息，并对区域和规则进行更改。

在更改防火墙设置时，意识到运行时（runtime）配置和永久（permanent）配置的概念非常重要。默认情况下，任何规则更改都被视为运行时配置更改。这意味着虽然更改会立即生效，但在下一次系统重启或 `firewalld` 服务重载时（例如通过执行以下命令），将会丢失：

```bash
firewall-cmd --reload
```

必须使用 `--permanent` 命令行选项使更改永久化。永久更改在 `firewalld` 服务重载之前不会发生，但在手动更改之前将一直保持有效。

### 14.3.1 识别和更改默认区域

要识别默认区域（换句话说，除非专门选择了不同的区域，否则所有接口将分配到该区域），请使用 `firewall-cmd` 工具：

```bash
firewall-cmd --get-default-zone
```

更改默认区域：

```bash
firewall-cmd --set-default-zone=home
```

### 14.3.2 显示区域信息

列出所有区域：

```bash
firewall-cmd --get-zones
```

列出分配了接口的活动区域：

```bash
firewall-cmd --get-active-zones
```

列出特定区域当前配置的规则：



```bash
firewall-cmd --zone=home --list-all
```

列出区域当前开启的服务：

```bash
firewall-cmd --zone=public --list-services
```

获取端口规则列表：

```bash
firewall-cmd --zone=public --list-ports
```

#### 14.3.3 添加和删除区域服务

向区域添加服务，在此例中向`public`区域添加`https`，使用以下命令：

```bash
firewall-cmd --zone=public --add-service=https
```

默认情况下，这是运行时更改，因此添加的规则将在系统重启后丢失。要永久添加服务以便在下次系统重启时生效，请使用`--permanent`标记：

```bash
firewall-cmd --zone=public --permanent --add-service=https
```

要验证服务是否已永久添加，请求服务列表时要包含`--permanent`标记：

```bash
firewall-cmd --zone=public --permanent --list-services
```

注意，作为永久更改，此新规则在系统重启或`firewalld`重载之前不会生效：

```bash
firewall-cmd --reload
```

使用`--remove-service`选项从区域删除服务。由于这是运行时更改，该规则在下次系统重启时将重新恢复：

```bash
firewall-cmd --zone=public --remove-service=https
```

要永久删除服务，请使用`--permanent`标记，如果需要更改立即生效，请记住重载`firewalld`：

```bash
firewall-cmd --zone=public --permanent --remove-service=https
```

### 14.3.4 使用基于端口的规则

要启用特定端口，请使用`--add-port`选项。注意，在手动定义端口时，需要提供端口号和协议（`TCP`或`UDP`）：

```bash
firewall-cmd --zone=public --permanent --add-port=5000/tcp
```

在向区域添加规则时，也可以指定一个端口范围：

```bash
firewall-cmd --zone=public --permanent --add-port=5900-5999/udp
```

### 14.3.5 创建新区域

运行以下命令可以创建一个全新的区域。一旦创建，就可以像管理任何预定义区域一样来管理该区域：

```bash
firewall-cmd --permanent --new-zone=myoffice
```

success

在添加新区域后，在区域变为可用之前，需要重启`firewalld`：

```bash
firewall-cmd --reload
```

success

### 14.3.6 更改区域/接口分配

如前所述，系统上的每个接口都必须分配到一个区域。可以使用`firewall-cmd`工具更改接口所属的区域。在以下示例中，将`eth0`接口分配到`public`区域：

```bash
firewall-cmd --zone=public --change-interface=eth0
```

success

### 14.3.7 伪装

伪装（Masquerading）在网络管理领域广为人知的网络地址转换（NAT）。当使用`RHEL 9`系统作为计算机网络访问互联网的网关时，伪装允许所有内部系统在互联网通信时使用该`RHEL 9`系统的 IP 地址。这样做的好处可以向恶意外部实体隐藏任何系统的内部 IP 地址，并避免了为网络上的每台计算机分配公网 IP 地址的性。

使用以下命令检查防火墙是否已启用了伪装：

```bash
firewall-cmd --zone=external --query-masquerade
```

使用以下命令启用伪装（如果需要使更改永久生效，请记得使用`--permanent`标志）：

```bash
firewall-cmd --zone=external --add-masquerade
```

### 14.3.8 添加 ICMP 规则

网络控制消息协议（ICMP）用于网络上的客户端系统之间相互发送信息（例如错误消息）。它也是`ping`命令的基础，网络管理员和用户都使用它来检测特定客户端在网络上是否活跃。`ICMP`允许阻止特定的`ICMP`消息类型。例如，管理员可能会选择阻止传入的`ping`（回显请求）`ICMP`消息，以防止基于`ping`的拒绝服务（DoS）攻击的可能性（即服务器被恶意的大量 ping 消息冲击，导致无法响应合法请求）。

要查看可包含`firewalld`规则的`ICMP`类型，请运行以下命令：

```bash
firewall-cmd --get-icmptypes
```

`address-unreachable bad-header beyond-scope communication-prohibited destination-unreachable echo-reply ...`

例如，以下命令为`public`区域永久添加一条规则来阻止`echo-reply`（ping 请求）消息：

```bash
firewall-cmd --zone=public --permanent --add-icmp-block=echo-reply
```

### 14.3.9 实现端口转发

当`RHEL 9`系统作为内部计算机网络到互联网的网关时，端口转发通常与伪装结合使用。端口转发允许通过互联网从特定端口到达防火墙的流量转发到内部网络上的特定系统。这通过示例来描述可能最为恰当。

假设一个`RHEL 9`系统作为内部计算机网络的防火墙，网络上的其中一个系统被配置为 Web 服务器。假设该 Web 服务器系统的 IP 地址为`192.168.2.20`。托管在该系统上的网站的域名记录配置为位于`RHEL 9`防火墙系统后的公网 IP 地址。当 HTTP 网页请求从端口`80`到达时，作为防火墙的`RHEL 9`系统需要知道如何处理它。通过配置端口转发，可以将所有网络流量重定向到托管 Web 服务器的内部系统（在此例中，IP 地址为`192.168.2.20`），可以继续使用端口`80`，也可以将流量重定向到目标服务器上的不同端口。事实上，端口转发甚至可以配置将流量转发到防火墙相同系统的不同端口（此概念被称为本地转发）。

要使用端口转发，首先按照如下方式启用伪装（在此例中，假设连接到互联网的接口已分配给`external`区域）：

```bash
firewall-cmd --zone=external --add-masquerade
```

从一个端口转发到不同的本地端口，将使用类似下面的命令：

```bash
firewall-cmd --zone=external --add-forward-port=port=22:proto=tcp:toport=2750
```

在上面的示例中，任何位于端口`22`的`TCP`流量都将转发到本地系统的端口`2750`。另一方面，以下命令将 IP 地址为`192.168.0.19`的系统上的端口`20`转发到`22`：

```bash
firewall-cmd --zone=external \
             --add-forward-port=22
```

### 14.4 通过 Cockpit 界面管理 fireld

到目前为止，本章提供了`firewalld`的概述，并探索了使用`firewall-cmd`命令行工具管理区域和接口。虽然`firewall-cmd`提供了管理配置的最灵活方式，但也可以在 Cockpit 控制台中查看和管理默认区域的服务。

要访问防火墙设置，请登录 Cockpit 界面并从侧边栏选择`Networking`。在网络页面上，如图 14-1 所示找到`Firewall`部分并点击`Edit rules and zones`按钮：

`Firewall`页面显示了默认区域配置的服务（并允许删除服务）、向区域添加新服务以及开启和关闭防火墙。

### 14.5 使用 firewall-config 管理 firewalld

如果你可以使用图形桌面环境，可以使用`firewall-config`工具配置防火墙。虽然默认未安装，但可以通过以下方式安装`firewall-config`：

```bash
dnf install firewall-config
```

启动后，将如图 14-3 所示的`firewall-config`主界面：

工具的关键区域总结如下：

- A：显示所有当前活动接口及其分配的区域。要将接口分配到不同的区域，请在此面板中选择它，点击`Change Zone`按钮并从弹出对话框中选择所需的区域。
- B：控制显示的信息以及工具内所做的任何更改是应用于运行时规则还是永久规则。
- C：系统上配置的区域、服务或`Sets`列表。此面板中的信息取决于工具栏 F 中的选择。从此列表中选择项目将更新标记为 D 的主面板。
- D：主面板包含有关工具栏 E 当前选择类别的信息。在此示例中，面板显示了`public`区域的服务。每个服务旁边的选择框控制该服务是否在防火墙中启用。在这些类别面板中可以添加新规则或对现有规则进行配置或删除。
- E：控制面板 D 中显示的内容。从此栏中选择项目将显示所选类别的当前规则。
- F：控制面板 C 中显示的列表。

`firewall-config`工具使用简单直观，它允许在图形环境中执行许多可以使用`firewall-cmd`完成的任务。

## 14.6 总结

一个精心规划和实施的防火墙对于任何安全系统都至关重要。对于`RHEL 9`而言，`firewalld`服务提供了一个既灵活又易于管理的防火墙系统。

`firewalld`服务使用“区域”（zones）的概念将一组组防火墙规则分组，并包含了一系列预定义的区域，旨在满足各种防火墙保护需求。可以对这些区域进行修改以添加或删除规则，也可以创建并配置全新的区域。系统上连接到网络或互联网的网络设备称为接口（interfaces）。每个接口反会被分配到一个区域。用于`firewalld`的主要工具是`firewall-cmd`命令行工具和`firewall-config`图形实用程序。Cockpit Web 界面也提供少量的防火墙管理选项。

## 15. 在 RHEL 9 上配置基于密钥的 SSH 身份验证

首次安装 RHEL 9 系统时，默认配置允许通过 Secure Shell (SSH) 连接进行远程命令行访问。SSH 为 root 账户以及安装期间添加任何其他用户提供了受密码保护和加密的系统访问。然而，这种安全级别是不够的，应该尽快升级为基于密钥的身份验证。

本章将概述通过实现基于密钥的 SSH 身份验证来提高 RHEL 9 系统安全性的步骤。

## 15.1 Secure Shell (SSH) 概述

SSH 设计用于安全远程访问系统以获取 shell 访问并传输文件和数据。正如在使用 VNC 进行 RHEL 9 远程桌面中提到的，SSH 还可以提供安全隧道，通过网络连接实现对 GNOME 桌面的远程访问。

基本的 SSH 配置由一个客户端（用于建立连接的计算机）和一个服务器（运行在要连接的系统上）组成。用户可以使用运行在 Linux、Windows 或 macOS 系统上的 SSH 客户端连接到运行在 RHEL 9 系统上的 SSH 服务器，以获取 shell 命令行提示符或执行文件传输。客户端和服务器之间的所有通信（包括获取访问时输入的密码）都经过加密，以防止外部人员拦截数据。

基础 SSH 实现的固有弱点是它完全依赖于分配给系统账户的密码强度。如果恶意方能够识别出账户的密码（通过猜测、欺骗或暴力破解攻击），系统就会变得脆弱。通过实现基于密钥的 SSH 验证可以解决这一弱点。

## 15.2 基于密钥的身份验证

基于密钥的 SSH 身份验证使用非对称公钥加密为远程系统访问增加额外的安全性。公钥加密的概念由 Whitfield Diffie 和 Martin Hellman 于 1975 年发明，基于使用私钥和公钥对。

在公钥加密系统中，公钥用于加密数据，这些数据只能由私钥的所有者解密。

在基于密钥的 SSH 身份验证中，主机持有 SSH 客户端所在的私钥，而相应的公钥则存储在运行 SSH 服务器的系统上。因此，保护私钥至关重要，因为拥有密钥的所有权将允许任何人登录远程系统。作为额外的保护，私钥还可以被加密并受密码保护，每次建立到服务器的连接时必须输入该密码。

### 15.3 设置基于密钥的身份验证

设置基于密钥的 SSH 身份验证有四个步骤，总结如下：

1. 生成公钥和私钥。
2. 在服务器上安装公钥。
3. 测试身份验证。
4. 在服务器上禁用基于密码的身份验证。

本章的其余部分将为 Linux、macOS 和基于 Windows 的客户端操作系统详细介绍这些步骤。

## 15.4 安装并启动 SSH 服务

如果系统上尚未安装并运行 SSH 服务器，可以使用以下命令添加：

```bash
dnf install openssh-server
systemctl start sshd.service
systemctl enable sshd.service
```

### 15.5 从 Linux 和 macOS 客户端进行基于密钥的身份验证

设置基于密钥的身份验证的第一步是在客户端系统上生成密钥对。如果客户端系统运行的是 Linux 或 macOS，则使用`ssh-keygen`工具来实现：

```bash
ssh-keygen
```

该命令将产生类似下面的输出：

```
Generating public/private rsa key pair.
Enter file in which to save the key (/home/<username>/.ssh/id_rsa):
```

按 Enter 键接受密钥文件的默认位置。这将在当前用户主目录的`.ssh`子目录下放置两个文件。私钥将存储在名为`id_rsa`的文件中，而公钥将存在于名为`id_rsa.pub`的文件中。

接下来，`ssh-keygen`将提示输入用于保护私钥的短语（passphrase）。如果提供了短语，私钥将在本地磁盘上加密，访问远程系统时需要该短语。为了更好的安全，建议使用短语。

```
Enter passphrase:
```

最后，`ssh-keygen`工具将生成以下输出，表示密钥已生成：

```
Your identification has been saved in /home/neil/.ssh/id_rsa
Your public key has been saved in /home/neil/.ssh/id_rsa.pub
The fingerprint is: SHA256:FOLEEGjWnCT5wtTO5hdimzUEMYfo <username>@hostname>
The key’s randomart image is:
+---[RSA 2048----+
|.BB+=*..
|o+B *
|===.. +
|* * |
|| o |
|+ +
| .
```

下一步是将公钥安装到远程服务器上。可以使用`ssh-copy-id`工具来实现：

```bash
ssh-copy-id username@remote_hostname
```

例如：

```bash
ssh-copy-id neil@192.168.1.100
```

```
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/neil/.ssh/id_rsa.pub"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
neil@192.168.1.100’s password:
Number of key(s) added: 1
```

现在尝试使用`ssh 'neil@192.168.1.100'`登录机器，并检查是否只添加了需要的密钥。

一旦安装完成，通过使用`ssh`客户端尝试远程登录来测试身份验证是否有效：

```bash
ssh -l <username> <hostname>
```

如果私钥加密并受短语保护，在提示时输入短语以完成身份验证并建立到 RHEL 9 系统的远程访问：

```
Enter passphrase for key '/home/neil/.ssh/id_rsa':
```

对服务器上需要远程访问的其他账户重复这些步骤。如果还需要从其他客户端系统访问，请将`id_rsa`私钥文件复制到其他系统主目录下的`.ssh`子目录。

按照目前的配置，仍然可以使用安全性较低的密码认证访问远程系统。一旦你确认了基于密钥的认证工作正常，就需要在系统上禁用密码认证。要了解如何更改此设置，请先打开`/etc/ssh/sshd_config`文件并找到以下行：

`Include /etc/ssh/sshd_config.d/*.conf`

这告诉我们`sshd`配置设置是由`/etc/ssh/sshd_config.d`目录下的文件控制的。这些文件名必须以数字开头，并具有`.conf`文件扩展名，例如：

`01-permitrootlogin.conf`

`50-redhat.conf`



数字前缀指定了文件相对于文件夹中其他文件的优先级，其中 `01` 优先级最高。这确保了如果某个配置文件包含与另一个文件冲突的设置，优先级最高的那个将始终具有优先权。

在 `/etc/ssh/sshd_config.d` 文件夹中，创建一个名为 `02-nopasswordlogin.conf` 的新文件，内容如下：

```
PasswordAuthentication no
```

保存文件并重启 `sshd` 服务以实施更改：

```bash
systemctl restart sshd.service
```

从现在起，将仅允许使用 SSH 密钥认证远程访问系统，并且在这样做时，你不需要输入密码。

## 15.6 管理多个密钥

客户端系统中存在多个私钥是常见现象，每个密钥提供对不同服务器的访问。因此，在建立连接时有多种选项可以选择特定的密钥。例如，可以在启动 `ssh` 客户端时如下指定要使用的私钥文件：

```bash
ssh -l neilsmyth -i ~/.ssh/id_work 35.194.18.119
```

或者，`ssh` 客户端用户配置文件可以将密钥文件与服务器关联。该配置文件名为 `config`，必须位于用户主目录下的 `.ssh` 目录，并可用于配置广泛选项，包括私钥文件、连接时使用的默认端口、默认用户名以及用于引用服务器的简短别名。下面的示例配置文件为两个服务器定义了不同的密钥文件，并允许通过 `home` 和 `work` 别名引用它们。对于工作系统，该文件还指定了认证时使用的用户名：

```text
Host work
  HostName 35.194.18.119
  IdentityFile ~/.ssh/id_work
  User neilsmyth
Host home
  HostName 192.168.0.21
  IdentityFile ~/.ssh/id_home
```

在设置配置文件之前，用户本会使用以下命令连接到工作系统：

```bash
ssh -l neilsmyth -i ~/.ssh/id_work 35.194.18.119
```

现在，命令可以缩短为：

```bash
ssh work
```

运行以下命令可以找到配置文件选项的完整列表：

```bash
man ssh_config
```

# 15.7 从 Windows 客户端进行 SSH 密钥认证

最近的 Windows 版本包含了大多数 Linux 和 macOS 系统所使用的 OpenSSH 实现子集，部分位于 Windows PowerShell。这允许按照为 Linux 和 macOS 概述的步骤，从 Windows 客户端设置基于密钥的认证。

在 Windows 上，搜索 `Windows PowerShell` 并选择它。运行后，将出现 PowerShell 窗口。

如果你已经有一个来自另一个系统的私钥，请将 `id_rsa` 文件复制到 Windows 系统上名为 `.ssh` 的文件夹中。文件到位后，在 PowerShell 窗口中按如下测试认证：

```bash
ssh -l <username>@<hostname>
```

例如：

```powershell
PS:\Users\neil> ssh -l neil 192.168.1.100
```

在提示时输入 `C:\Users\neil\ssh\id_rsa` 的口令。

如果私钥不存在，请在 PowerShell 窗口中使用 `ssh-keygen` 按相同的步骤生成新的公钥对。密钥生成后，它们将位于当前用户主目录的 `.ssh` 目录中，公钥文件 `id_rsa.pub` 需要安装在远程 RHEL 9 系统上。遗憾的是，Windows PowerShell 不包含 `ssh-copy`，因此此任务必须手动执行。在 PowerShell 窗口中，切换到 `.ssh` 目录并显示公钥 `id_rsa.pub` 的内容：

```powershell
PS:\Users\neil> cd .ssh
PS:\Users\neil\ssh> type id_rsa.pub
```

选中文件内容并使用 `Ctrl-C` 复制。留在 PowerShell 窗口中，使用密码认证登录远程系统：

```powershell
PS:\Users\neil\.ssh> ssh -l <username> <hostname>
```

登录成功后，检查 `.ssh` 目录是否存在。如果不存在，按如下方式创建它：

```bash
mkdir .ssh
```

检查是否存在名为 `authorized_keys` 的文件。如果不存在，创建它并将来自 Windows 系统的公钥内容粘贴到其中。如果 `authorized_keys` 文件已存在，它可能包含其他密钥。如果是这样，编辑该文件并将新公钥粘贴到文件末尾。

# 15.8 使用 PuTTY 进行 SSH 密钥认证

对于没有可用 OpenSSH 的 Windows 系统，或作为使用 PowerShell 更灵活的替代方案，PuTTY 工具是一种广泛使用的替代方案。使用 PuTTY 的第一步是在需要 SSH 客户端的 Windows 系统上下载并安装它。PuTTY 是一个免费工具。

在为所有账户设置并验证了基于密钥的认证后，按照上一节最后在 RHEL 9 系统上禁用密码认证。

接下来，需要使用 `PuTTYgen` 工具将私钥文件转换为 PuTTY 私钥格式文件。在 Windows 开始菜单的搜索栏中输入“PuTTY Key Generator”查找该实用程序并启动它：

![](img/putty_key_generator.png)

图 15-2

-ce

启动后，点击位于 `Actions` 部分的 `Load` 按钮，并导航到之前复制到 `.ssh` 文件夹的私钥文件（注意，可能需要将文件类型过滤器更改为 `All Files (*.*)` 才能看到密钥文件）。找到后，选择该文件并加载到 `PuttyGen`。在出现提示时，输入最初用于加密该文件的口令（passphrase）。导入私钥后，点击 `Save Private Key` 按钮将其保存为 PuTTY 密钥文件。为了保持一致性，请将密钥文件保存到 `.ssh` 文件夹，但赋予一个不同的名称以与原始密钥文件区分开。

从开始菜单启动 `PuTTY`，在主界面输入远程服务器的 IP 地址或主机名，然后选择左侧面板中的 `Connection -> SSH -> Auth -> Credentials` 类别，如图 15-3 所示：

![](img/putty_credentials.png)

图 15-3

点击 `Private key for authentication` 字段旁边的 `Browse` 按钮，导航并选择之前保存的 PuTTY 私钥文件。然后（可选），滚动到左侧面板顶部，选择 `Session`，并在 `Saved Sessions` 字段中为会话输入名称，最后点击 `Save` 按钮。这将保存会话配置，以便以后使用，而无需每次重新输入设置。

最后，点击 `Open` 按钮建立与远程服务器的连接，在提示时输入用户名和口令以完成身份验证。

## 15.9 使用 PuTTYgen 生成私钥

上一节探讨了在操作 `PuTTY` 时使用现有的私钥和公钥。如果没有密钥，可以使用包含在 `PuTTY` 主安装程序中的 `PuTTYgen` 工具创建。

要创建新密钥，启动 `PuttyGen` 并点击图 15-4 中高亮的 `Generate` 按钮：

![](img/putty_key_generator_generate.png)

图 15-4

按照指示移动鼠标指针生成随机数据，然后输入可选的口令来加密私钥。密钥生成后，使用 `Save public key` 和 `Save private key` 按钮将文件保存到合适的位置。如上一节所述，私钥可用于 `PuTTY`。要在远程服务器上安装公钥，请参考早期章节中关于在 Windows 的 `PowerShell` 中使用 `SSH` 的步骤。

## 15.10 总结

对 `RHEL 9` 系统的任何远程访问必须以提供高安全性的方式来实现。默认情况下，`SSH` 允许使用基于密码的验证进行远程系统访问。然而，这使得系统受到任何能猜密码或或其他手段获取密码的人的影响。因此，建议使用基于密钥的验证来保护系统访问。基于密钥的验证使用涉及公钥和私钥的公钥加密。实施后，只有当用户使用的客户端私钥与服务器上的公钥匹配时，才能连接到服务器。作为额外的安全层，私钥还可以进行加密并密码保护。一旦实施了基于密钥的加密，服务器系统将配置为禁用安全性较低的基于密码的验证。

本章提供了 `SSH` 密钥验证的概述，并概述了在 macOS、Linux 和 Windows 上生成密钥和配置客户端的步骤，以及在 `RHEL 9` 服务器上安装和管理公钥的步骤。

# 16. 使用 VNC 进行 RHEL 9 远程桌面访问

`RHEL 9` 可以配置为通过网络或互联网连接提供图形化桌面环境的远程访问。虽然默认未启用，但从网络或互联网上的其他系统显示并访问 `RHEL 9` 桌面是相对简单的。无论该系统运行 Linux、Windows 还是 macOS，都可以实现这一点。甚至有适用于 Android 和 iOS 的应用程序，可以让你从几乎任何有数据信号的地方访问 `RHEL 9` 桌面。

远程桌面访问在许多场景下都很有帮助。例如，它允许你或其他人从同一网络或互联网上的另一台计算机系统查看并与你的 `RHEL 9` 桌面环境交互。当你由于离开座位（例如旅行期间）需要在电脑上工作时，这非常有用。当同事或 IT 支持人员需要访问你的桌面来解决问题时，它也有帮助。

当 `RHEL 9` 系统运行在云服务器上时，它还允许访问桌面环境，作为使用命令行提示符或 `Cockpit` Web 控制台执行管理任务的替代。

`RHEL 9` 远程桌面功能基于名为虚拟网络计算（VNC）的技术。本章将涵盖在 `RHEL 9` 中配置和使用远程桌面的关键方面。

## 16.1 安全与安全的远程桌面访问

在本章中，我们将涵盖安全和不安全的远程桌面访问方法。假设你在安全的内部网络从一个系统访问另一个系统，使用不安全的访问方法通常是安全的。但如果你计划通过任何公共网络远程访问桌面，必须使用安全的访问方法，以避免系统和数据被破坏。

## 16.2 安装 GNOME 桌面环境

当然，只有在安装了桌面本身的情况下，才能访问桌面环境。例如，如果系统最初被配置为服务器，则可能没有安装桌面包。运行 `GNOME` 桌面所需的软件包的简单方法是执行组安装。安装包组以启用特定功能的关键是知道该组的名称。在编写时，`RHEL 9` 上有两个安装桌面的组：`Server with GUI` 和 `Workstation`。由于组名称可能会从一个 RHEL 版本变为另一个版本，因此使用 `dnf` 工具获取已安装或可用的组列表是有帮助的，如下：

```bash
dnf grouplist
```

更新订阅管理存储。

可用的环境组：

- Server with GUI
- Minimal Install
- Workstation
- Custom Operating System
- Virtualization Host

已安装的环境组：

- Server

已安装的组：

- Container Management
- Headless Management

可用的组：

- Legacy UNIX Compatibility
- Graphical Administration Tools
- Smart Card Support
- RPM Development Tools
- .NET Development
- System Tools
- Development Tools
- Console Internet Tools
- Security Tools
- Network Servers
- Scientific Support

在上述示例中，`Workstation` 环境组显示可用（因此未安装）。要在安装之前获取有关组内容的更多信息，请使用以下命令：

```bash
dnf groupinfo workstation
```

更新订阅管理存储。

环境组：Workstation

描述：Workstation 是适用于笔记本电脑和 PC 的易用桌面系统。

强制组：

- Common NetworkManager submodules
- Core
- Fonts
- GNOME
- Guest Desktop Agents
- Hardware Support
- Internet Browser
- Multimedia
- Printing Client
- Standard
- Workstation product core
- base-x

可选组：

- Backup Client
- GNOME Applications
- Headless Management

### 办公套件与效率工具

### 远程桌面客户端

### 智能卡支持

在确认这是正确的组后，可以按照以下方式安装：

```bash
dnf groupinstall workstation
```

安装完成后，假设系统已添加了显示器，可以使用以下 `startx` 命令启动桌面：

```bash
startx
```

另一方面，如果系统是没有直接连接显示器的服务器，那么运行和访问桌面的唯一方法是在系统上配置 VNC 支持。

## 16.3 在 RHEL 9 上安装 VNC

访问远程桌面需要在远程系统上安装 VNC 服务器，在发起连接的系统上安装 VNC 查看器，并（视情况而定）需要一个安全的 SSH 连接。虽然有多种 VNC 服务器和查看器实现，但红帽公司已统一采用 `TigerVNC` 作为标准，它为基于 Linux 的操作系统提供了服务器和查看器组件。非 Linux 平台的 VNC 查看器客户端包括 `RealVNC` 和 `TightVNC`。

要在 RHEL 9 上安装 `TigerVNC` 服务器包，请运行以下命令：

```bash
dnf install tigervnc-server
```

如果需要，也可以按照以下方式安装 `TigerVNC` 查看器：

```bash
dnf install tigervnc
```

安装服务器后，必须配置系统以运行一个或多个 VNC 服务，并在防火墙上打开相应的端口。

## 16.4 配置 VNC 服务器

安装 VNC 服务器包后，下一步是配置服务器。第一步是为远程桌面环境用户指定密码。以 root 身份登录时，执行 `vncpasswd` 命令（假设用户名为 `demo`）：

```bash
su - demo
[demo@demoserver ~]$ vncpasswd
Password:
Verify:
Would you like to enter a view-only password (y/n)? n
A view-only password is not used
[demo@demoserver ~]$ exit
```

接下来，需要在 `/etc/systemd/system` 目录下创建一个名为 `vncserver@.service` 的 VNC 服务器配置文件。该文件的内容如下，其中所有的 `<USER>` 实例应替换为设置 VNC 密码时引用的用户名：

```ini
[Unit]
Description=Remote desktop service (VNC)
After=syslog.target network.target

[Service]
Type=forking
WorkingDirectory=/home/<USER>
User=<USER>
Group=<USER>
ExecStartPre=/bin/sh -c ‘/usr/bin/vncserver -kill %i > /dev/null 2>&1 || :’
ExecStart=/usr/bin/vncserver -autokill %i
ExecStop=/usr/bin/vncserver -kill %i
Restart=on-success
RestartSec=15

[Install]
WantedBy=multi-user.target
```

接下来，需要配置防火墙以为远程 VNC 查看器实例提供对 VNC 服务器的外部访问，例如：

```bash
firewall-cmd --permanent --zone=public --add-port=5901/tcp
firewall-cmd --reload
```

创建服务配置文件后，需要如下方式启用并启动服务：

```bash
systemctl daemon-reload
systemctl start vncserver@:1.service
systemctl enable vncserver@:1.service
```

注意，服务名称中包含 `:1` 表示这是 VNC 服务器显示器 1 的服务。这与之前在防火墙中打开的 5901 端口匹配。

按照如下方式检查服务是否成功启动：

```bash
systemctl status vncserver@:1.service
```

如果服务启动失败，运行 `journalctl` 命令检查错误消息：

```bash
journalctl -xe
```

此外，尝试重启系统后重试。如果服务持续失败，可以通过登录指定用户并运行 `vncserver` 命令来手动启动 VNC 服务器：

```bash
vncserver :1
```

## 16.5 连接到 VNC 服务器

VNC 查看器适用于多种操作系统。因此，快速在互联网搜索可能会提供许多关于如何在您选择的平台上获取和安装此工具的详细链接。

在安装了 `TigerVNC` 等 VNC 查看器的 Linux 系统桌面上，可以通过终端窗口如下所示建立远程桌面连接：

```bash
vncviewer <hostname>:<display number>
```

在上面的示例中，`<hostname>` 是远程系统的主机名或 IP 地址，而 `<display number>` 是 VNC 服务器桌面的显示编号，例如：



```bash
vncviewer 192.168.1.115:1
```

或者，在不带任何选项的情况下运行命令，根据提示输入远程服务器详细信息：

![](img/rhel_vnc_authentication_dialog.png)

图 16-1

在 VNC 服务器字段中输入主机名或 IP 地址，后跟显示编号（例如 `192.168.1.115:1`），并点击连接按钮。查看器将提示输入用户的 VNC 密码以完成连接，此时，一个包含远程桌面的新窗口将会出现。

本节假设是从 Linux 或 UNIX 系统访问远程桌面；相同的步骤适用于大多数其他操作系统。

使用本节中的步骤连接到 VNC 服务器会产生不安全的未加密连接。这意味着在远程会话期间传输的数据是易受截获的。因此，需要额外的步骤来建立安全的加密连接。

## 16.6 建立安全的远程会话

本章介绍的远程桌面配置是不安全的，因为没有使用加密。当远程连接受防火墙保护的内部网络时是可以接受的。然而，对于互联网连接需要更安全的选项。这通过通过安全壳（SSH）隧道远程桌面来实现。本节将涵盖如何在 Linux、UNIX 和 macOS 上进行操作。

SSH 服务器在 RHEL 9 系统上通常默认安装并激活。如果您的系统并非如此，假设 SSH 服务器已安装，可以使用如下命令登录远程系统以建立安全隧道：

```bash
ssh -l <username> -L 5901:localhost:5901 <remotehost>
```

在上面的示例中，`<username>` 是配置了 VNC 访问的远程系统账户，`<remotehost>` 是远程系统的主机名或 IP 地址，例如：

```bash
ssh -l neilsmyth -L 5901:localhost:5901 192.168.1.115
```

在提示时使用账户密码登录。建立安全连接后，是启动 `vncviewer` 来使用安全隧道。在另一个终端窗口中保留 SSH 会话，启动另一个终端并输入以下命令：

```bash
vncviewer localhost:5901
```

如果需要，`vncviewer` 会话将提示密码，然后启动 VNC 查看器提供对桌面环境的安全访问。

尽管连接现在是安全的且加密的，VNC 查看器很可能会报告连接是不安全的。例如，图 16-2 显示了在 macOS 系统上运行的 `RealVNC` 查看器显示的警告框：

![](img/rhel_8_vnc_viewer_not_encrypted.png)

图 16-2

遗憾的是，尽管连接现在是安全的，但 VNC 查看器软件无法得知这一点，因此继续发出警告。然而，请放心，只要使用了 SSH 隧道，连接确实是安全的。

上述命令将提示输入服务器的密码，然后在后台建立连接，留下终端窗口供其他任务使用。如果你从防火墙外部连接远程桌面，请记住 SSH 连接的 IP 地址将由 ISP 或云托管商提供的外部 IP 地址，而不是系统的 IP 地址（因为它在防火墙外是不可见的）。因此，你还需要配置防火墙转发端口 `22`（用于 SSH 连接）到运行桌面的系统。不需要转发端口 `5900`。端口转发步骤在不同防火墙之间有所不同，请参考您的防火墙文档。

## 16.7 使用 PuTTY 建立安全隧道

在 Windows 系统上通过 PuTTY 建立安全桌面会话的方法类似。假设你已经安装了 VNC 客户端，剩下的要求是 SSH 客户端。一旦下载并安装了 `PuTTY`，第一步是在 Windows 系统与 RHEL 9 系统之间建立安全连接。启动后，显示如下屏幕：

![](img/home_screen.png)

图 16-3

输入远程主机的 IP 地址或主机名（如果你从防火墙外部连接）。下一步是设置隧道。点击左侧树形结构中 `SSH` 旁边的 `+`，选择 `Tunnels`。随后应出现屏幕：

![](img/tunnels_screen.png)

图 16-4

输入 `5901` 作为 `Source`（源），`localhost:5901` 作为 `Destination`（目的），并点击 `Add`。最后，通过点击 `Session` 返回主屏幕。在 `Saved Sessions` 字段中输入会话名称并按 `Save`。点击 `Open` 建立连接。终端窗口将弹出远程系统的登录凭据。SSH 连接已建立。启动 `TightVNC` 查看器，在 `VNC Server` 字段中输入 `localhost:5901`，然后点击 `Connect`。查看器将建立连接并提示密码，然后显示 Linux 系统的远程桌面。

## 16.8 关闭桌面会话

要关闭 VNC 服务器托管的桌面会话，请使用命令行选项 `--kill` 加上要终止的桌面编号。例如：

```bash
vncserver –kill :1
```

## 16.9 排除 VNC 连接故障

由于后台有许多活动，VNC 有时看起来可能不透明，特别是当出现问题导致服务器无法启动或连接并产生错误消息时。不过有一些跟踪和解决 VNC 问题的方法：

如果 VNC 服务启动失败，检查服务的 `systemctl status` 错误消息：

```bash
systemctl status vncserver@:1.service
```

要获取更详细的信息，通过运行 `journalctl` 命令检查 `systemd` 日志：

```bash
journalctl -xe
```

额外信息可能位于日志文件中：

`/home/<username>/.vnc/<hostname>:<display number>.log`

例如：

`/home/neilsmyth/.vnc/rhelserver01.localdomain:1.log`

如果 `systemd` VNC 服务仍然启动 VNC 服务器，尝试使用以下命令手动启动：

```bash
vncserver :<display number>
```

例如：

```bash
vncserver :1
```

检查输出和日志文件是否有有助于识别问题的错误。然后，如果服务器成功启动，尝试再次连接 VNC 查看器。

如果 VNC 服务器似乎正在运行，但从查看器的连接失败，可能值得检查正确的防火墙端口是否打开。通过以下方式识别默认区域：

```bash
firewall-cmd --get-default-zone
```

```text
public
```

获取默认区域后，检查必要的端口是否打开：

```bash
firewall-cmd --permanent --zone=public --list-ports
```

```text
5901/tcp
5900/tcp
```

如果 VNC 使用的端口未打开，按如下方式添加端口：

```bash
firewall-cmd --permanent --zone=public --add-port=<port number>/tcp
```

## 16.10 总结

可以使用虚拟网络计算（VNC）启用 RHEL 9 系统的 GNOME 桌面环境的远程访问。VNC 由运行在远程服务器上对应的本地客户端组成，允许远程访问服务器上的多个桌面实例。

当通过公共连接使用 VNC 连接时，建议使用 SSH 隧道以确保客户端和服务器之间的通信加密且安全。

# 17. 远程显示 RHEL 9 应用程序（X11 转发）

在上一节中，我们看了如何在远程计算机上显示整个 RHEL 9 桌面。虽然当你需要远程显示整个桌面时这种方法很好，但如果你只想显示单个应用程序，这可能被认为是大材小用。因此，本章将查看远程系统中显示单个应用程序。

## 17.1 远程显示 RHEL 9 应用程序的要求

在一个系统上运行应用程序并在另一个系统显示它有几个先决条件。首先，显示应用程序的系统必须运行 X 服务器。如果是一个带有桌面环境的 Linux 或 Unix 系统，则没有这个问题。然而，如果系统是 Windows 或 macOS，你必须安装一个 X 服务器才能从远程显示。有很多可用的商业和免费 Windows 版 X 服务器。

其次，运行应用程序的系统（而非显示应用程序的系统）必须配置允许 SSH 访问。在 RHEL 9 上配置 SSH 的详情可以参见基于密钥的 SSH 认证。该系统还需要运行 Xorg 而不是 Wayland。要启用 Xorg 系统，编辑 `/etc/gdm/custom.conf` 文件并取消 `WaylandEnable` 行的注释并重启系统：

```ini
# 取消下面注释以强制登录界面使用 Xorg
WaylandEnable=false
```

最后，SSH 必须配置允许 X11 转发。这通过在发生转发的 SSH 配置中添加以下指令来实现。在 RHEL 9 默认情况下，`/etc/sshd_config` 文件包含一个指令来包含 `/etc/ssh/sshd_config.d` 目录中的所有配置文件：

```text
Include /etc/ssh/sshd_config.d/*.conf
```

在新安装的系统中，文件夹中会创建一个名为 `50-redhat.conf` 文件。编辑此文件并确保 `X11Forwarding` 属性启用：

```ini
X11Forwarding yes
```

更改后，保存文件并重启 SSH 服务：

```bash
systemctl restart sshd
```

## 17.2 远程显示 RHEL 9 应用程序

远程显示应用程序的第一步是移动到显示应用程序的系统。在该系统中，与远程系统建立 SSH 连接以便获得命令行提示符。这可以使用 `ssh` 命令来实现。在使用 `ssh` 命令时，我们需要使用 `-X` 标志告诉它我们计划通过连接隧道 X11 流量：

```bash
$ ssh -X user@hostname
```

在上面的示例中，`user` 是用于登录远程系统的用户名，而 `hostname` 是远程系统的主机名或 IP 地址。在登录提示符处输入您的密码，登录后，运行以下命令查看 `DISPLAY` 设置：

```bash
$ echo $DISPLAY
```

该命令的输出应类似于下面的内容：

```text
localhost:10.0
```

如需显示应用程序，请从命令行提示符运行它。例如：

```bash
$ gedit
```

执行上述命令时，该命令应在远程系统上运行 `gedit` 工具，但在本地系统上显示用户界面。

## 17.3 可信的 X11 转发

如果远程系统上的 `/etc/ssh/sshd_config.d/50-redhat.conf` 文件包含以下行，则可以使用可信的 X11 转发：

```text
ForwardX11Trusted yes
```

可信的 X11 转发速度比不可信的转发稍快一点，但安全性较低，因为它没有参与 X11 安全控制。在使用可信的 X11 转发时，需要使用 `-Y` 标志：

```bash
$ ssh -Y user@hostname
```

## 17.4 压缩的 X11 转发

在使用较慢的连接时，可以使用 `ssh -C` 标志对 X11 数据进行压缩以提高性能：

```bash
$ ssh -X -C user@hostname
```

## 17.5 在 Windows 上显示远程 RHEL 9 应用

要在 Windows 上显示基于 RHEL 9 的应用程序，必须在 Windows 系统上安装 SSH 客户端和 X 服务器。关于在 Windows 上安装和使用 `PuTTY` 客户端的主题已在书中之前的“在 RHEL 9 上配置基于密钥的认证”章节中介绍。如果您尚未在 Windows 系统上安装 `PuTTY`，请参考该章节。

在 X 服务器方面，有多个选项可用，尽管其中一个流行的选择似乎是 `VcXsrv`，它可以通过以下 URL 免费获取：

[`sourceforge.net/projects/vcxsrv/`](https://sourceforge.net/projects/vcxsrv/)

一旦安装了 `VcXsrv` X 服务器，桌面和开始菜单上将出现名为 `XLaunch` 的应用程序。启动 `XLaunch` 并选择一个显示选项（最灵活的是“Multiple windows”选项，它允许每个客户端应用在它自己的窗口中出现）：

![](img/vcxsrvr_xlaunch_settings.png)

图 17-1

点击 `Next` 按钮继续后续屏幕，并接受默认配置设置。在最后一个屏幕上，点击 `Finish` 按钮启动 X 服务器。如果出现 Windows Defender 对话框，请点击该按钮允许访问您所选的网络。

运行后，`XLaunch` 将显示在任务栏中，可以通过右键点击图标并选择 `Exit...` 菜单选项退出：

![](img/vcxsrvr_xlaunch_menu.png)

图 17-2

在安装并运行 X 服务器后，启动 `PuTTY`，并输入远程主机的连接信息，或者加载之前保存的会话配置。但是，在建立连接之前，需要启用 X11 转发。因此，在 `PuTTY` 主窗口中，向下滚动左侧面板中的选项，展开 `SSH` 部分并选择 `X11` 选项，如图 17-3 所示：

![](img/win_10_putty_ssh.png)

图 17-3

勾选图 17-4 中突出显示的 `Enable X11 forwarding` 复选框，返回会话屏幕并打开连接（如果您计划再次使用，请提前保存会话）：

![](img/putty_enable_x11_forwarding.png)

图 17-4

在 `PuTTY` 会话窗口中登录 RHEL 9 系统并运行桌面应用程序。稍等片，该程序将以自己的窗口显示在 Windows 桌面上。应用程序打开的任何对话框也将出现在独立的窗口中，就像它们在 RHEL 9 GNOME 桌面上的显示一样。例如，图 17-5 显示了在 Windows 11 系统上显示的 RHEL 9 `nm-connection-editor` 工具：

![](img/x11_windows_forwarding.png)

图 17-5

## 17.6 总结

对于需要远程访问单个 RHEL 9 桌面应用程序而非整个 GNOME 桌面的情况，X11 转发提供了一种远程显示图形应用程序的轻量级解决方案。显示程序的系统必须运行基于 X Window 系统的桌面环境（如 GNOME）或安装并运行 X 服务器。一旦在远程服务器上启用了 X11 转发，并从本地系统使用 X11 转发选项建立了安全的 SSH 连接，大多数应用程序就可以在本地 X 服务器上显示。

# 18. 在 RHEL 9 上使用 NFS 与远程系统共享文件

RHEL 9 提供了两种与网络上其他系统共享文件和文件夹的机制。一种方法是使用名为 `Samba` 的技术。`Samba` 基于 Windows 文件夹共享，允许 Linux 系统让 Windows 系统访问文件夹，并反之亦然。另一种方法是专门用于在 Linux 和 UNIX 系统之间共享文件夹的网络文件系统（`NFS`）。`NFS` 允许一台计算机上的文件系统通过网络被另一台计算机访问。

## 18.1 确保 RHEL 9 上运行 NFS 服务

第一个任务是验证您的 RHEL 9 系统上是否安装并运行了 NFS 服务。这可以通过命令行或 Cockpit 界面实现。在后台，NFS 使用远程过程调用（`RPC`）在网络上共享文件系统。首先通过运行以下命令安装 `rpcbind` 和 `nfs-utils`：

```bash
# dnf install rpcbind nfs-utils
```

接下来，配置这些服务以便启动时自动运行：

```bash
# systemctl enable rpcbind
# systemctl enable nfs-server
```

一旦启用了服务，按以下方式启动它们：

```bash
# systemctl start rpcbind
# systemctl start nfs-server
```

## 18.2 配置 RHEL 9 防火墙允许 NFS 流量

接下来，需要配置防火墙允许 NFS 流量。为了实现此目标，运行以下 `firewall-cmd` 命令，并将 `<zone>` 替换为适用于您的防火墙区域：

```bash
# firewall-cmd --zone=<zone> --permanent --add-service=mountd
# firewall-cmd --zone=<zone> --permanent --add-service=nfs
# firewall-cmd --zone=<zone> --permanent --add-service=rpc-bind
# firewall-cmd --reload
```

## 18.3 指定要共享的文件夹

现在 NFS 已经运行且防火墙已配置好，我们需要指定 RHEL 9 文件系统的哪些部分可以被远程 Linux 或 UNIX 系统访问。这些设置可以在 `/etc/exports` 文件中声明，必须修改该文件以导出用于远程访问的目录。

在上述行中，`<export>` 被替换为要导出的目录，`<host1>` 是授予访问权限的系统名称或 IP 地址，而 `<options>` 代表要对该访问施加的限制（只读、读写等）。如果需要，可以将多个主机和选项条目放在同一行上。例如，下行向 IP 地址为 `192.168.2.38` 的主机授予 `/datafiles` 目录的只读权限：

```text
/datafiles 192.168.2.38(ro)
```

允许使用通配符将导出应用到多个主机。例如，下行允许所有外部主机对 `/home/demo` 具有读写权限：

```text
/home/demo *(rw)
```

通过查阅 `exports` 的 `man` 帮助页（man page），可以找到 `exports` 文件支持的完整选项列表：

```bash
# man exports
```

在本章中，我们将如下所示配置 `/etc/exports` 文件：

```text
/tmp *(rw,sync) own/vol1 192.168.86.42(ro,sync)
```

配置完成后，需要使用 `exportfs` 命令根据最新的 `/etc/exports` 设置更新由 NFS 服务器维护的导出文件系统表：

```bash
# exportfs -a
```



也可以使用`exportfs`工具从命令行查看当前的共享设置：

```
#exportfs
```

上述命令将生成以下输出：

```
/vol1 192.168.86.42
/tmp <world>
```

## 18.4 访问共享文件夹

用户可以通过从命令行手动挂载共享文件夹，从而在客户端系统上访问这些共享文件夹。但是，在尝试挂载远程 NFS 文件夹之前，必须先在客户端系统上安装`nfs-utils`包：

```
#dnf install nfs-utils
```

要从命令行挂载远程文件夹，请打开终端窗口并创建一个你想挂载远程共享文件夹的目录：

```
$mkdir /home/demo/tmp
```

接下，使用远程 NFS 服务器的 IP 地址或主机名输入挂载远程文件夹的命令，例如：

```
$sudo mount -t nfs 192.16.86.24:/tmp /home/demo/tmp
```

远程`/tmp`文件夹随后将挂载到本地系统上。挂载后，`/home/demo/tmp`文件夹将包含远程文件夹及其所有内容。

在挂载远程 NFS 文件系统时，也可以指定选项。例如，以下命令挂载了相同的文件夹，但将其配置为只读：

```
$sudo mount -t nfs -o ro 192.168.86.24:/tmp /home/demo/tmp
```

## 18.5 在系统启动时挂载 NFS 文件系统

也可以通过编辑`/etc/fstab`文件，配置 RHEL 9 系统在每次启动时自动挂载远程文件系统。当将其加载到编辑器中时，它可能看起来如下：

```
/dev/mapper/rhel-root / xfs defaults 0 0
UUID=c4ba0b0f-777a-42a8 /boot xfs defaults 0 0
UUID=052D-19D8 /boot/efi vfat umask=0077,shortname=winnt 0 2
/dev/mapper/rhel-swap none swap defaults 0 0
```

例如，为了将路径为`/tmp`的文件夹（位于 IP 地址为`192.168.86.24`的系统上）挂载到本地路径`/home/demo/tmp`（注意该文件夹必须已存在），向`/etc/fstab`文件中添加以下行：

```
192.168.86.24:/tmp /home/demo/tmp nfs rw 0 0
```

下次系统重启时，远程系统上的`/tmp`文件夹将挂载到本地的`/home/demo/tmp`挂载点。此时，访问远程文件夹中的所有文件就像它们存在本地硬盘上一样。

## 18.6 卸载 NFS 挂载点

一旦使用 NFS 挂载了远程文件系统，可以使用`umount`命令并将本地挂载点作为命令行参数进行卸载。例如，以下命令将卸载我们的示例文件系统挂载点：

```
$sudo umount /home/demo/tmp
```

## 18.7 在 Cockpit 中访问 NFS 文件系统

除了使用命令行在客户端挂载远程 NFS 文件系统外，也可以在 Cockpit Web 界面中执行挂载操作。假设客户端系统已安装并配置了 Cockpit，从浏览器登录 Cockpit 界面，并从左侧导航面板选择`Storage`（存储）选项。如果没有`Storage`选项，则需要安装`cockpit-storaged`包：

```
#dnf install cockpit-storaged
#systemctl restart cockpit.socket
```

一旦 Cockpit 服务重启，再次登录 Cockpit 界面，此时`Storage`选项应该是可见的。

选中后，主存储页面将包含一个列出已挂载 NFS 文件系统的部分，如图 18-1 所示：

![](img/cockpit_nfs.png)

图 18-1

要挂载文件系统，点击上方显示的`+`按钮并输入远程 NFS 服务器和共享的信息。

## 18.8 总结

网络文件系统（NFS）是一种客户端/服务器系统，最初由 Sun 公司开发，为 Linux 和 Unix 系统提供了共享文件系统的方法。NFS 允许客户端访问和修改远程文件，就像它们存储在本地硬盘上一样。

# 19. RHEL9 与 Windows 系统之间的文件共享

尽管 Linux 已经在桌面市场取得了一定进展，但其起源和未来主要是面向服务器的。因此，并不意外，RHEL 9 可以作为文件服务器。因此，一个常见的需求是 RHEL 9 系统上的文件可以被 Linux、Unix 和 Windows 系统访问。同样，Windows 系统上的共享文件夹和打印机可能也需要从 RHEL 9 系统进行访问。

Windows 系统使用名为 Server Message Block（SMB）的协议共享资源和打印机。为了让 RHEL 9 系统通过网络向 Windows 系统提供此类资源以及反之，必须支持 SMB。这是通过 Samba 技术实现的。

## 19.1 从 GNOME 桌面访问 Windows 资源

在详细介绍 Samba 共享之前，值得注意的是，如果你只是想从 GNOME 桌面访问 Windows 共享文件夹，那么 GNOME Files 应用已经提供了这种支持。Files 应用如图 19-1 所示位于程序栏中：

![](img/file_in_dashboard.png)

图 19-1

启动后，选择左侧导航面板中的`Other Locations`（其他位置）选项，然后点击主面板中的`Windows Network`（Windows 网络）图标即可浏览可用的 Windows 资源。

![](img/rhel_files_windows.png)

图 19-2

## 19.2 Samba 与 Samba Client

Samba 允许 RHEL 9 资源与 Windows 系统共享，同时也允许 Windows 资源与 RHEL 9 系统共享。RHEL 使用`Samba`客户端访问 Windows 资源。相反，RHEL 资源通过安装和配置`Samba`服务来与 Windows 系统共享。

## 19.3 在 RHEL 9 上安装 Samba

RHEL 9 安装过程中使用的默认设置通常不会安装必要的 Samba 软件包。除非你特别请求了安装 Samba，否则你的系统中很可能没有安装 Samba。要检查是否安装了 Samba，打开终端窗口并运行以下命令：

```bash
rpm -q samba samba-common samba-client
```

可以使用`dnf`命令行工具安装任何缺失的软件包：

```bash
dnf install samba samba-common samba-client
```

## 19.4 配置 RHEL 9 防火墙以启用 Samba

接下来，必须配置保护 RHEL 9 系统的防火墙以允许 Samba 流量。可以使用以下`firewall-cmd`命令实现：

```bash
firewall-cmd --permanent --add-port={139/tcp,445/tcp}
firewall-cmd --reload
```

在启动 Samba 服务之前，需要执行一些配置步骤来定义 RHEL 系统如何向 Windows 系统显示以及与远程客户端共享的资源。大多数配置任务在`/etc/samba/smb.conf`文件中完成。

## 19.5 配置 smb.conf 文件

Samba 是一个高度灵活且可配置的系统，为控制 Windows 网络上的资源共享方式提供了许多选项。遗憾的是，这种灵活性可能会导致人们认为 Samba 过于复杂。然而实际上，典型的安装不需要许多配置选项，设置基础配置的学习曲线相对较短。

在本章中，我们将查看如何将 RHEL 9 系统加入 Windows 工作组，并设置一个目录作为特定用户可以访问的共享资源。这种配置被称为独立 Samba 服务器。虽然也提供了更高级的配置，例如将 Samba 集成到活动目录（Active Directory）环境中，但这些内容超出了本书的范范围。

配置 Samba 的第一步是编辑`/etc/samba/smb.conf`文件。

### 19.5.1 配置 [global] 段

`smb.conf`文件分为多个段。第一个段是`[global]`段，可以在此处指定适用于整个 Samba 配置的设置。虽然这些设置是全局的，但每个选项都可以在其他配置文件的段中被覆盖。

第一个任务是定义 RHEL 9 资源将要共享的 Windows 工作组名称。这通过`[global]`段的`workgroup`指令进行控制，其默认配置如下：

```ini
workgroup = SAMBA
```

如有必要，首先将其更改为实际的工作组名称。

除了`workgroup`设置外，其他设置表明这是一个独立服务器，用户密码将保护共享资源。在继续配置要共享的资源之前，还需要将以下参数添加到`[global]`段中：

```ini
[global]
.
.
    netbios name = LinuxServer
```

“netbios name”属性指定了服务器在网络上其他系统可见的名称。

### 19.5.2 配置共享资源

下一步步骤是配置共享资源（换句话说，即从 Windows 网络上的其他系统可以访问的资源）。为了实现这一点，需要为该段命名，以便在共享时引用。例如，如果我们计划共享 RHEL 9 系统的`/sampleshare`目录，我们可以将该段命名为`[sampleshare]`。在此段中，可以使用各种配置选项。然而，对于此示例，我们只需定义要共享的目录，指示该目录既可浏览又可写，并声明该资源为公共以便访客用户访问：

```ini
[sampleshare]
    comment = Example Samba share
    path = /sampleshare
    browseable = Yes
    public = yes
    writable = yes
```

要限制特定用户的访问，可以使用“valid users”属性，例如：

```ini
valid users = demo, bobyoung, marcewing
```

### 19.5.3 不必要的共享

`smb.conf`文件预先配置了共享打印机和系统用户主目录的段。如果不需要共享这些资源，可以注释掉相应的段，以便 Samba 忽略它们。在接下来的示例中，`[homes]`段已被注释：

```ini
.
.
#[homes]
# comment = Home Directories
# valid users = %S, %D%w%S
# browseable = No
# read only = No
# inherit acls = Yes
.
.
```

## 19.6 为 Samba 配置 SELinux

SELinux 是默认集成到所有 RHEL 9 系统 Linux 内核中的一个系统，为操作系统和用户文件提供了额外的安全保护。

从传统上讲，Linux 安全基于允许用户决定谁可以访问他们的文件和其他拥有的其他资源。例如，考虑一个位于特定用户主目录并由该用户拥有的文件。该用户可以控制该文件的访问权限。这种类型的安全被称为自主访问控制，因为资源访问由用户决定。

然而，通过 SELinux，访问由系统控制且不能被用户覆盖。这被称为强制性访问控制，是由 SELinux 策略定义的。继续之前的示例，只有当 SELinux 策略（由系统或管理员定义）允许时，文件所有才能执行操作。

RHEL 9 上的 SELinux 状态可以使用`sestatus`工具识别：

```text
SELinux status: enabled
SELinuxfs mount: /sys/fs/selinux
SELinux root directory: /etc/selinux
Loaded policy name: targeted
Current mode: enforcing
Mode from config file: enforcing
Policy MLS: enabled
Policy deny_unknown status: allowed
Memory protection checking: actual (secure)
Max kernel policy version: 33
```

SELinux 可以以强制（enforcing）或许可（permissive）模式运行。启用时，强制模式会拒绝所有 SELinux 策略不允许的操作。相反，许可模式允许通常会被拒绝的操作继续，但会记录在日志文件中。

SELinux 安全基于上下文标签。系统上的所有资源（包括进程和文件）都分配了由用户、角色、类型和可选安全级别组成的 SELinux 上文标签。例如，可以查看文件或文件夹的 SELinux 上文：

```bash
$ ls -Z /home/demo
unconfined_u:object_r:user_home_t:s0 Desktop
  unconfined_u:object_r:user_home_t:s0 Documents
```

同样，可以使用`ps`命令识别运行进程的上下文，在此例为`ls`命令：

```bash
$ ps -eZ | grep ls
unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.1023 14311 tty1 00:00:18 ls
```

当进程（例如上述`ls`命令）尝试访问文件或文件夹时，SELinux 系统将检查策略以识别是否允许访问。现在考虑 Samba 服务的上下文：

```bash
$ ps -eZ | grep smb
system_u:system_r:smbd_t:s0 14129 ? 00:00:00 smbd
system_u:system_r:smbd_t:s0 14132 ? 00:00:00 smbd-notifyd
```

SELinux 实现安全的多种方式，最常见的是称为类型强制。基本上，当进程尝试对对象（例如写入文件）执行操作时，SELinux 会检查进程和对象的上下文类型，并验证安全策略是否允许该操作进行。Suppose a process of type `A`, for example, attempts to write to a file of type `B`. In that case, it will only be permitted if SELinux policy states explicitly that a process of type `A` may perform a write operation to a file of type `B`. In SELinux enforcement, all actions are denied by default unless a rule specifically allows the action to be performed.

SELinux 实现安全的多种方式，最常见的是称为类型强制。基本上，当进程尝试对对象（例如写入文件）执行操作时，SELinux 会检查进程和对象的上下文类型，并验证安全策略是否允许该操作进行。假设一个类型为`A`（例如）的进程尝试写入类型为`B`的文件，则只有在 SELinux 政策明确说明进程类型`A`可以对类型`B`的文件执行写入操作时才会被允许。在 SELinux 强制模式下，除非规则明确允许，否则所有操作默认被拒绝。

The issue with SELinux and Samba is that SELinux policy is not configured to allow processes of type `smb_t` to perform actions on files of any type other than `samba_share_t`. For example, the`/home/demo`目录 listed above will be inaccessible to the Samba service because it has a type of`user_home_t`. To make files or folders on the system accessible to the Samba service, the enforcement type of those specific resources must be changed to`samba_share_t`.

SELinux 与 Samba 之间的问题在于 SELinux 政策未配置为允许类型为`smb_t`的进程对除`samba_share_t`之外的任何文件类型执行操作。例如，上述`/home/demo`目录的类型为`user_home_t`，因此 Samba 服务无法访问该目录。要使系统中的文件或文件夹可供 Samba 服务访问，必须将这些特定资源的强制类型更改为`samba_share_t`。

For this example, we will create the`/sampleshare`目录 referenced previously in the`smb.conf`文件 and change the enforcement type to make it accessible to the Samba service. Begin by creating the directory as follows：

```bash
mkdir /sampleshare
```

Next, check the current SELinux context on the directory：

```bash
$ ls -aZ /sampleshare/
unconfined_u:object_r:root_t:s0 .
```



In this instance, the context label of the folder has been assigned a type of `root_t`. To make the folder sharable by Samba, the enforcement type needs to be set to `samba_share_t` using the `semanage` tool as follows:

```bash
semanage fcontext -a -t samba_share_t "/sampleshare(/.*)?"
```

Note the use of a wildcard in the `semanage` command to ensure that the type is applied to any sub-directories and files contained within the `/sampleshare` directory. Once added, the change needs to be applied using the `restorecon` command, making use of the `-R` flag to apply the change recursively through any sub-directories:

```bash
restorecon -R -v /sampleshare
```

Relabeled `/sampleshare` from `unconfined_u:object_r:default_t:s0` to `unconfined_u:object_r:samba_share_t:s0`

Once these changes have been made, the folder is configured to comply with SELinux policy for the `smb` process and is ready to be shared by Samba.

## 19.7 创建 Samba 用户

Any user that requires access to a Samba shared resource must be configured as a Samba User and assigned a password. This task is achieved using the `smbpasswd` command-line tool. Consider, for example, that a user named `demo` is required to be able to access the `/sampleshare` directory of our RHEL 9 system from a Windows system. To fulfill this requirement, we must add `demo` as a Samba user as follows:

```bash
smbpasswd -a demo
```

New SMB password:

Retype new SMB password:

Added user `demo`.

Now that we have completed the configuration of an elementary Samba server, it is time to test our configuration file and then start the Samba services.

## 19.8 测试 smb.conf 文件

The settings in the `smb.conf` file may be checked for errors using the `testparm` command-line tool as follows:

```bash
testparm
```

Load smb config files from `/etc/samba/smb.conf`

Loaded services file OK.

Weak crypto is allowed

Server role: ROLE_STANDALONE

Press enter to see a dump of your service definitions

```ini
# Global parameters
[global]
log file = /var/log/samba/%m.log
netbios name = LINUXSERVER
printcap name = cups
security = USER
wins support = Yes
idmap config * : backend = tdb
cups options = raw

[sampleshare]
comment = Example Samba share
guest ok = Yes
path = /sampleshare
read only = No

[homes]
browseable = No
comment = Home Directories
inherit acls = Yes
read only = No
valid users = %S %D%w%S

[printers]
browseable = No
comment = All Printers
create mask = 0600
path = /var/tmp
printable = Yes
```

## 19.9 启动 Samba 和 NetBIOS 名称服务

For a RHEL 9 server to operate within a Windows network, the Samba (SMB) and NetBIOS nameservice (NMB) services must be started. Optionally, also enable the services so that they start each time the system boots:

```bash
systemctl enable smb nmb
systemctl start smb nmb
```

Before attempting to connect from a Windows system, use the `smbclient` utility to verify that the share is configured:

```bash
smbclient -U demo -L localhost
```

Enter `WORKGROUP\demo`’s password:

```text
Sharename Type Comment

--------- ---- -------

sampleshare Disk Example Samba share

print$ Disk Printer Drivers

IPC$ IPC IPC Service (Samba 4.9.1)

demo Disk Home Directories
```

## 19.10 访问 Samba 共享

Now that the Samba resources are configured, and the services are running, it is time to access the shared resource from a Windows system. On a suitable Windows system on the same workgroup as the RHEL 9 system, open Windows Explorer and navigate to the Network panel. At this point, Explorer should search the network and list any systems using the SMB protocol that it finds. The following figure illustrates a RHEL 9 system named `LINUXSERVER` located using Windows Explorer on a Windows system:

![](img/rhel_8_connect_to_windows_share.png)

Figure 19-5

Double-clicking on the `LINUXSERVER` host will prompt for the name and password of a user. In this case, it is the `demo` account we configured using `smbpasswd`:

![](img/rhel_8_windows_login.png)

Figure 19-6

Entering the username and password will result in the shared resources appearing in the Explorer window, including the previously configured `/sampleshare`:

![](img/rhel_8_folder_windows.png)

Figure 19-7

Double-clicking on the `/sampleshare` shared resource will display a listing of the files and directories therein.

If you are unable to see the Linux system or have problems accessing the shared folder, try mapping the Samba share to a local Windows drive as follows:

1. Open Windows File Explorer, right-click on the Network entry in the left-hand panel, and select **Map network drive...** from the resulting menu.
2. Select a drive letter from the Map Network Drive dialog before entering the path to the shared folder. For example: `\\LinuxServer\sampleshare`
3. Enable the checkbox next to **Connect using different credentials**. For example, if you do not want the drive to be mapped each time you log into the Windows system, turn off the corresponding check box:

   ![](img/windows_map_drive.png)

With the settings entered, click the **Finish** button to map the drive, entering the username and password for the Samba user when prompted. After a short delay, the content of the Samba share will appear in a new File Explorer window.

## 19.11 从 RHEL 9 访问 Windows 共享

As previously mentioned, Samba is a two-way street, allowing not only Windows systems to access files and printers hosted on a RHEL 9 system but also allowing the RHEL 9 system to access shared resources on Windows systems. This is achieved using the `samba-client` package, installed at this chapter’s start. If it is not currently installed, install it from a terminal window as follows:

```bash
dnf install samba-client
```

Shared resources on a Windows system can be accessed from the RHEL desktop using the Files application or from the command-line prompt using the `smbclient` and `mount` tools. The steps in this section assume that the Windows system has enabled appropriate network-sharing settings.

To access any shared resources on a Windows system using the GNOME desktop, launch the Files application and select the **Other Locations** option. This will display the screen shown in Figure 19-7 below, including an icon for the Windows Network (if one is detected):

![](img/rhel_8_connect_to_windows_share.png)

Figure 19-7

...

硬件虚拟化利用了 Intel 和 AMD 最新几代 CPU 内置的虚拟化功能。这些技术分别称为 `Intel VT` 和 `AMD-V`，它们为运行未修改的虚拟机提供了必要的扩展，且避免了全虚拟化 CPU 仿真所固有的开销。简单来说，这些处理器在 `ring 0` 之上提供了一个额外的特权模式（`ring -1`），虚拟机程序（hypervisor）可以在其中运行，从而将 `ring 0` 留给未修改的虚拟机操作系统。

下图展示了 Type-1 虚拟机程序的虚拟化方法：

![](img/type-1_hypervisor_virtualization.png)

图 20-3

如上述图所示，除了虚拟机之外，管理操作系统或管理控制也运行在虚拟机程序之上，允许系统管理员对虚拟机进行管理。

## 20.3 虚拟机网络

虚拟机不可需要连接到网络以发挥实际用途。一种方案是让连接到运行在主机操作系统内部的虚拟网络。在这种配置下，虚拟网络上的任何虚拟机都可以相互看到，但网络地址转换（`NAT`）提供了对外部网络的访问。当使用虚拟网络和 `NAT` 时，每个虚拟机都使用主机系统的 IP 地址在外部网络（主机所连接的网络）上表示。这是 `RHEL 9` 上 `KVM` 虚拟化的默认行为，且通常不需要额外配置。通常，默认会创建一个虚拟网络，名称为 `default`，设备为 `virbr0`。

为了让虚拟机在外部网络上显示为独立的个体系统（即拥有自己的 IP 地址），它们必须配置为共享主机上的物理网络接口。实现此点的快速方法是配置虚拟机使用“直接连接”网络配置选项（也称为 `MacVTap`），这将为虚拟机系统提供一个与主机相同网络上的 IP 地址。遗憾的是，虽然这允许虚拟机访问网络上的其他系统，但使用 `MacVTap` 驱动无法在虚拟机和主机之间建立连接。

更好的选项是在主机系统上配置网络桥接接口并让虚拟机连接。这为虚拟机提供了外部网络上的 IP 地址，同时允许虚拟机和主机进行通信，该主题在创建 RHEL 9 KVM 网络桥接接口章节中有所介绍。

## 20.4 总结

虚拟化是在单个主机操作系统内运行多个虚拟机操作系统的能力。目前已开发出多种虚拟化方法，包括虚拟机操作系统虚拟化和虚拟机程序虚拟化。虚拟机程序虚拟化分为两类：Type-1 和 Type-2。Type-2 虚拟化解决方案分为半虚拟化、全虚拟化硬件虚拟化，后者使用了某些 Intel 和 AMD 处理器型号的特殊虚拟化功能。

虚拟机客操作系统在网络方面有多种选择，包括 `NAT`、直接连接（`MacVTap`）和网络桥配置。

# 21. 在 RHEL 9 上安装 KVM 虚拟化

早期版本的 `RHEL` 两个虚拟化平台：基于内核的虚拟机（`KVM`）和 `Xen`。在最近的发布中，对 `Xen` 的支持已被移除，留下 `KVM` 作为 `RHEL 9` 提供的唯一内置虚拟化选项。除了 `KVM` 之外，`VMware` 和 `Oracle VirtualBox` 等产品也提供第三方解决方案。由于 `KVM` 是随 `RHEL 9` 提供的，此虚拟化解决方案将在在本章及后续章节中介绍。

在深入安装和运行 `KVM` 之前，值得讨论它是如何融入上一节中概述的各种虚拟化类型中的。

## 21.1 KVM 概述

`KVM` 被归类 Type-1 虚拟机程序虚拟化解决方案，它通过 `Intel VT` 和 `AMD-V` 硬件虚拟化支持实现了支持未修改虚拟机操作系统的全虚拟化。

`KVM` 与许多其他 Type-1 解决方案不同，它将主机 Linux 操作系统转换为虚拟机程序，允许在运行完整企业级主机操作系统的同时实现裸金属虚拟化。

### 21.2 KVM 硬件要求

在继续本章之前，我们必须讨论在 `KVM` 环境中运行虚拟机的硬件要求。首先，`KVM` 虚拟化仅适用于某些类型的处理器。如前所述，这些处理器必须包含 `Intel VT` 或 `AMD-V` 技术。

要检查虚拟化支持情况，请在终端窗口中运行 `lscpu` 命令：

```bash
lscpu | grep Virtualization:
```



如果系统包含支持 `Intel VT` 的 CPU，上述命令将提供以下输出：

```text
Virtualization: VT-x
```

或者，当检测到支持 `AMD-V` 的 CPU 时，将显示以下输出：

```text
Virtualization: AMD-V
```

如果 CPU 不支持虚拟化，上述 `lscpu` 命令将没有任何输出。

请注意，虽然上述命令仅报告处理器是否支持相应功能，但它并不表示在 BIOS 中已启用。这是因为在实践中，大多数系统的 BIOS 默认禁用了虚拟化支持。因此，在继续本教程之前，您应该检查 BIOS 设置，以确保启用了适当的虚拟化技术。

与双启动环境不同，虚拟化环境涉及在单个计算机系统上并发运行两个或多个完整的操作系统。这意味着系统必须具有足够的物理内存、磁盘空间和 CPU 处理能力，以舒适地并行处理所有系统。因此，在开始配置和安装过程之前，请检查 `RHEL 9` 和您选择的虚拟机系统的最低系统要求，并验证您的主机系统有足够的资源来处理这两个系统的需求。

### 21.3 为 KVM 虚拟化准备 RHEL 9

与 `Xen` 不同，不需要运行特殊版本的内核来支持 `KVM`。因此，通过安装 `KVM` 内核模块，标准内核已支持使用 `KVM`，从而消除了安装和从特殊内核启动的需求。

然而，为了避免冲突，如果系统当前运行着启用 `Xen` 的内核，请在继续本章其余内容之前重启系统并在启动菜单中选择非 `Xen` 内核。

设置和维护基于 `KVM` 的虚拟化系统所需的工具只有在 `RHEL 9` 安装过程中显式选择时才会默认安装。要从命令行提示安装 `KVM` 工具，请在终端窗口中执行以下命令：

```bash
dnf install qemu-kvm qemu-img libvirt virt-install libvirt-client
```

如果您可以使用图形桌面环境，还建议安装 `virt-manager` 软件包：

```bash
dnf install virt-manager
```

### 21.4 验证 KVM 安装

在继续之前，检查 `KVM` 安装是否正确工作很有意义。当 `KVM` 安装并运行时，将有两个模块加载到内核中。可以通过在终端窗口中运行 `lsmod` 命令来验证这些模块是否存在：

```bash
lsmod | grep kvm
```

假设安装成功，上述命令应产生类似下面的输出：

```text
kvm_intel 237568 0
kvm 737280 1 kvm_intel
irqbypass 16384 1 kvm
```

注意，如果系统包含 AMD 处理器，`kvm` 模块可能会读取 `kvm_amd` 而不是 `kvm_intel`。

安装过程也应该配置了 `libvirtd` 守护进程在后台运行。再次使用终端窗口，运行以下命令以确保 `libvirtd` 正在运行：

```bash
systemctl status libvirtd
```

```text
libvirtd.service - Virtualization daemon

   Loaded: loaded (/usr/lib/systemd/system/libvirtd.service; enabled; vendor preset: enabled)

   Active: active (running) since Wed 2019-03-06 14:41:22 EST; 3min 54s ago
```

如果该进程未运行，可以通过以下方式启动：

```bash
systemctl enable --now libvirtd
systemctl start libvirtd
```

如果可以使用桌面环境，可以通过选择“活动”（Activities）并在搜索框中输入“virt”来运行 `virt-manager` 工具。当“虚拟机管理器”图标出现时，点击它进行启动。加载完成后，管理器应如下图所示：

![](img/virt-manager_main.png)

图 21-1

如果没有列出 `QEMU/KVM` 项，选择“文件 -> 添加连接”菜单选项，并在弹出的对话框中，点击“连接”按钮之前选择 `QEMU/KVM` 虚拟机程序：

![](img/virt-manager_add_connection.png)

图 21-2

如果管理器当前未连接到虚拟化进程，右键点击列出的项并从弹出菜单中选择“连接”。

## 21.5 总结

`KVM` 是一种 Type-1 虚拟机虚拟化解决方案，它利用 `Intel VT` 和 `AMD-V` 硬件虚拟化支持实现对未修改客操作系统的完全虚拟化。它是 `RHEL 9` 自带的默认虚拟化解决方案，可以在任何具有适当处理器支持的 `RHEL 9` 系统上快速方便地安装。在安装并启用 `KVM` 支持后，后续章节将概述在 `RHEL 9` 主机上安装和管理虚拟机的某些选项。

## 22. 使用 Cockpit 在 RHEL 9 上创建 KVM 虚拟机

可以使用 `virt-install` 命令行工具、`virt-manager` GUI 工具或 Cockpit Web 控制台的虚拟机模块在 `RHEL 9` 上轻松配置基于 `KVM` 的虚拟机。本章将使用 Cockpit 在 `RHEL 9` 主机上作为 `KVM` 虚拟机安装操作系统。名为“使用 `virt-manager` 在 `RHEL 9` 上创建 KVM 虚拟机”的章节将介绍使用 `virt-manager` 工具创建新的虚拟机。

下一章“使用 `virt-install` 和 `virsh` 创建 KVM 虚拟机”将介绍命令行创建虚拟机的方法。

### 22.1 安装 Cockpit 虚拟机模块

标准的 Cockpit 安装默认情况下可能不包含虚拟机模块。假设 Cockpit 已经安装并配置，可以通过以下方式安装虚拟机模块：

```bash
dnf install cockpit-machines
```

安装完成后，下一次登录 Cockpit 界面时，“虚拟机”选项（在图 22-1 中标记为 A 处）将显示在导航面板中：

![](img/rhel_cockpit_vm.png)

图 22-1

## 22.2 在 Cockpit 中创建虚拟机

要在 Cockpit 中创建虚拟机，点击图 22-1 中标记为 B 的“创建虚拟机”按钮以显示创建对话框。

在对话框中，为机器输入名称，并选择安装介质是通过 URL 访问的 ISO 格式还是本地文件系统路径，或者为虚拟机请求选择供应商和操作系统类型信息，并选择“下载操作系统”选项以便在安装过程中自动下载安装镜像。如果您打算使用操作系统下载选项将 `RHEL` 作为虚拟机安装，必须首先生成 RHSM 令牌，并将其复制粘贴到虚拟机创建屏幕的“离线令牌”（Offline token）字段中。您可以通过在浏览器中打开以下链接、登录 Red Hat 账户并选择令牌生成按钮来获取令牌：

<https://access.redhat.com/management/api>

此外，指定用于操作系统安装的虚拟磁盘驱动的大小以及分配给虚拟机的内存量：

![](img/rhel_cockpit_create_vm.png)

图 22-2

点击“创建并编辑”按钮来构建虚拟机。创建过程完成后，新虚拟机的详细信息将显示在 Cockpit 中，如图 22-3 所示：

![](img/rhel_cockpit_vm_overview.png)

图 22-3

正如“虚拟化技术概述”，`KVM` 为虚拟机在网络配置方面提供了多个选项。要查看并更改虚拟机的网络设置，请滚动到“虚拟机概述”屏幕的“网络接口”部分并点击“编辑”按钮：

![](img/rhel_cockpit_vm_network.png)

图 22-4

在弹出的对话框中，可以使用“网络类型”菜单更改网络类型，例如，从“虚拟网络 (NAT)”更改到“直接附加 (MacVTap)”或“桥接到局域网”。

### 22.3 开始安装

要启动新虚拟机并从指定的安装介质安装操作系统，请点击概述页顶部的“安装”按钮。Cockpit 将启动虚拟机并滚动到“控制台”视图，在那里将出现操作系统屏幕：

![](img/rhel_cockpit_console.png)

图 22-5

如果安装失败，检查消息查看在打开安装镜像时发生了错误。这通常是因为 QEMU 模拟器以 `qemu` 用户身份运行，该用户对目录没有访问权限。要解决此问题，打开终端窗口（如果是远程系统请通过 SSH 连接），切换到 ISO 所在的目录，并将该目录的访问控制列表 (ACL) 添加给 `qemu` 用户，如下：

```bash
cd /path/to/iso/directory
setfacl --modify u:qemu:x ..
```

更改后，通过以下命令检查设置：

```bash
getfacl ..
```

输出应显示 `user:qemu:x`。

完成更改后，再次点击“安装”按钮完成安装。

要完成安装，像在物理硬件上安装操作系统一样与控制台屏幕进行交互。如果控制台太小无法容纳整个系统屏幕，点击右上角的“展开”按钮。

可以使用 `virt-viewer` 工具从 Cockpit 浏览器会话外部连接并显示虚拟机的图形控制台。要在 `RHEL 9` 系统上安装 `virt-viewer`，运行命令：

```bash
dnf install virt-viewer
```

`virt-viewer` 工具适用于 Windows 系统，可以通过以下 URL 下载：

<https://virt-manager.org/download/>

要连接本地主机上运行的虚拟机，运行 `virt-viewer` 并在弹出的对话框中选择要连接的虚拟机：

![](img/rhel_virt_viewer_vm_list.png)

图 22-6

上述命令将列出系统级虚拟机。要列出并访问会话级虚拟机，请如下所示启动 `virt-viewer`：

```bash
virt-viewer --connect qemu:///session
```

或者也可以指定虚拟机名称并完全跳过选择对话框，例如：

```bash
virt-viewer demo-vm-guest
```

要使用 SSH 将 `virt-viewer` 实例连接到远程主机上运行的虚拟机，可以使用以下命令：

```bash
virt-viewer --connect qemu+ssh://<user>@<host>/system guest-name
```

```bash
$ virt-viewer --connect qemu+ssh://root@192.168.1.122/system demo_vm_guest
```

在使用此技术时，需要注意的是，在完全建立连接之前，系统会提示两次输入用户密码。

一旦创建了虚拟机，就可以通过 `Cockpit` 接口监控机器并执行重启、关机或删除客机系统等任务。`Disks`（磁盘）面板上还包含一个选项，用于向虚拟机配置中添加磁盘。

### 22.4 使用存储卷和存储池

当创建虚拟机时，它通常至少会有一个虚拟磁盘驱动器。代表这些虚拟磁盘驱动器的镜像被存储在存储池（Storage Pools）中。存储池可以是本地文件系统上的现有目录、文件系统分区、物理磁盘设备、逻辑卷管理（`LVM`）卷组，甚至是远程网络文件系统（`NFS`）。

每个存储池被划分为一个或多个存储卷（Storage Volumes）。存储卷通常是单个镜像文件，每个文件代表一个虚拟磁盘驱动器，但它们也可以以物理磁盘分区、整个磁盘驱动器或 `LVM` 卷组的形式存在。

当使用前面的步骤创建虚拟机时，系统会创建一个默认存储池来存储虚拟机镜像。该默认存储池占用根文件系统的空间，可以通过 `Cockpit Virtual Machine`（虚拟机）界面进行查看，方法是在上方标记为 `C` 的面板顶部选择 `Storage Pools`（存储池）选项，参见图 22-1。

选中后，屏幕将出现如下图 22-7 所示的界面，其中包含当前在系统上配置的存储池列表：

![](img/rhel_cockpit_vm_storage_pools.png)

图 22-7

在上面的示例中，默认存储池位于根文件系统，并将虚拟机镜像存储在 `/var/lib/libvirtd/images` 目录下。要查看池中包含的存储卷，请选择图 22-8 中高亮的 `Storage Volumes`（存储卷）选项卡：

![](img/rhel_cockpit_vm_storage_volumes.png)

图 22-8

对于演示客机，存储卷以名为 `demo-vm-guest.qcow2` 的镜像文件形式存在。此外，池还包含安装 ISO 镜像的存储卷。要确定特定虚拟机使用的是哪个存储卷，请返回 `Virtual Machine Cockpit` 主屏幕，选择该虚拟机并滚动到 `Disks` 面板，如图 22-9 所示：

![](img/rhel_cockpit_vm_disks.png)

图 22-9

虽然为了测试目的和早期实验，使用默认存储池是可以接受的，但建议为通用虚拟化用途创建额外的池。要创建新的存储池，请在 `Cockpit` 中显示 `Storage Pools` 屏幕并点击 `Create storage pool`（创建存储池）按钮，显示如图 22-10 所示的对话框：

![](img/rhel_cockpit_vm_create_pool.png)

图 22-10

在上面的示例中，正在创建一个名为 `MyPool` 的新存储池，该池使用了本地文件系统中挂载为 `/MyPool` 的文件系统分区（磁盘驱动器、分区和挂载点的主题将在本章后面的“向 RHEL 9 系统添加新磁盘驱动器”章节介绍）。一旦创建，该池将列在 `Cockpit` 存储池屏幕中，并在创建新虚拟机时包含存储卷。

## 22.5 总结

本章概述了如何使用 `Cockpit` Web 界面创建和管理基于 `KVM` 的虚拟机。`Cockpit` 接口的优势是不需要访问主机系统运行的桌面环境。另一种选项是使用下一章概述的 `virt-manager` 图形工具。

## 23. 在 RHEL 9 上使用 virt-manager 创建 KVM 虚拟机

上一章探讨了如何使用 `Cockpit` Web 工具在 `RHEL 9` 上创建 `KVM` 虚拟机。尽管考虑到一旦 `Virtual Machines Cockpit` 扩展完全实现，`virt-manager` 可能会停止使用，但本章将介绍使用该工具创建新虚拟机。

### 23.1 启动虚拟机管理器

如果你尚未安装，请按照以下方式安装 `virt-manager` 软件包：

```bash
# dnf install virt-manager
```



接下来，在终端窗口中运行`virt-manager`，从命令行启动`Virtual Machine Manager`（虚拟机管理器）。加载后，虚拟机管理器将在显示以下屏幕之前提示当前活动用户的密码：

![](img/rhel_virt-manager_home.png)

图 23-1

主屏幕列出了系统上运行的当前虚拟机。默认情况下，管理器应该连接到系统的`libvirtd`实例。如果没有连接，请右键点击列表中的项，并从弹出菜单中选择`Connect`（连接）到主机系统。要管理基于会话的虚拟机，请选择`File -> Add Connection...`（文件 -> 添加连接...）菜单选项，显示如图 23-2。

图 23-2

从`Hypervisor`菜单中选择`QEMU/KVM session`，并点击对话框中的`Connect`（连接）按钮。返回`virt-manager`主屏幕后，`QEMU/KVM`会话应如图 23-1 所示。要创建虚拟机，点击虚拟机按钮（工具栏最左侧的按钮），显示向导的第一个屏幕。在`Name`（名称）字段中为虚拟机输入一个描述性名称。在此屏幕上，还要选择安装操作系统的媒介。这可以是 CD 或 DVD 驱动器、主机可访问的 ISO 文件、使用`HTTP`、`FTP`、`NFS`或`PXE`进行网络安装，或现有虚拟机的磁盘镜像：

![](img/virt-manager_select_media.png)

图 23-3

## 23.2 配置 KVM 虚拟机

点击`Forward`（下一步）将显示寻求过程信息的屏幕。显示的屏幕和所需信息取决于初始屏幕上的选择。例如，如果选择了 CD、DVD 或 ISO，此屏幕将询问 ISO 文件或物理介质的具体位置。此屏幕还会尝试根据指定的安装介质识别客操作系统的类型和版本（例如 Windows 版本或 Linux 发行版）。如果无法识别，取消勾选`Automatically detect from installation media/source`（从安装介质/源自动检测）选项，输入操作系统名称的前几个字符，并从匹配列表中选择一个选项：

![](img/virt-manager_choose_iso.png)

图 23-4

完成这些设置后，点击`Forward`（下一步）按钮配置`CPU`和`memory`设置。最佳设置取决于主机存在的`CPU`数量和物理内存量，以及与新虚拟机并行运行的其他虚拟机的需求：

![](img/virt-manager_memory.png)

图 23-5

在下一个屏幕上，提供了选项创建指定大小的镜像磁盘、选择现有卷或创建指定格式（`raw`、`vmdk`、`ISO`等）的存储卷。除非你有使用特定格式的需要（例如，以后可能需要使用`vmdk`迁移到基于 VMware 的虚拟化环境），或需要使用专用磁盘或分区，否则在此屏幕上指定大小通常足够了：

![](img/virt-manager_disk.png)

图 23-6

如果在此处使用默认设置，虚拟机将使用默认存储池中的存储卷作为虚拟磁盘驱动器。要使用在本节较早创建的自定义“MyPool”存储池，请在点击`Manage...`按钮之前，启用`Select`或创建自定义存储选项。

在存储卷对话框中，在左侧面板中选择`MyPool`条目，然后点击主面板中的`+`按钮创建一个新的存储卷：

![](img/virt-manager_storage_volumes.png)

图 23-7

注意，对话框左下角的`+`按钮也可以用于创建新的存储池，作为使用`Cockpit`接口的备选方案。

在配置屏幕（图 23-8）中，为存储卷命名，选择卷大小，并点击`Finish`按钮创建卷并将其分配给虚拟机：

![](img/virt-manager_volume_details.png)

图 23-8

一旦配置了这些设置，选择新卷并点击`Choose Volume`按钮。然后再次点击`Forward`按钮。最终屏幕显示配置摘要。检查显示的信息。还有高级选项可以更改客户机的虚拟网络配置，如图 23-9 所示：

![](img/virt-manager_network.png)

图 23-9

## 23.3 启动 KVM 虚拟机

点击`Finish`按钮开始创建过程。虚拟化管理器将在启动客户系统之前创建磁盘并配置虚拟机。最后，新的虚拟机将出现在主`virt-manager`窗口中，状态设置为`Running`，如图 23-10 所示：

![](img/virt-manager_vm_running.png)

图 23-10

默认情况下，虚拟机的控制台应该出现在虚拟机查看器窗口中。若要在今后的任何时间查看运行机器的控制台，请确保它在虚拟机列表中被选中，并选择工具栏上的`Open`按钮。虚拟机查看器应准备好开始安装过程：

![](img/virt-manager_vm_display.png)

图 23-11

从现在起，按照安装说明在 KVM 虚拟机中安装操作系统。

## 23.4 总结

在 RHEL 9 宿主机系统上创建新的 KVM 虚拟机有多种方法。本章使用`virt-manager`图形工具来创建、配置和运行客户操作系统，包括创建新的存储卷。在涵盖这些基础知识后，下一章将介绍如何从命令行创建虚拟机。

## 24. 使用 virt-install 和 virsh 创建 KVM 虚拟机

在之前的章节中，我们探索了如何使用`Cockpit`和`virt-manager`图形工具在 RHEL 9 宿主机上创建 KVM 客户操作系统。本章将重点介绍如何使用`virt-install`和`virsh`命令行工具创建基于 KVM 的虚拟机。这些工具提供了`virt-manager`和`Cockpit`选项的所有功能，并具有在脚本中使用以自动创建虚拟机的额外优势。此外，`virsh`命令允许根据配置文件包含的规范创建虚拟机。

`virt-install`工具允许通过提供命令行选项列表来创建新的虚拟机。本章假设已安装了必要的 KVM 工具。有关这些要求的详细信息，请阅读章节在 RHEL 9 上安装 KVM 虚拟化。

### 24.1 运行 virt-install 构建 KVM 客户系统

`virt-install`实用程序接受广泛的命令行参数，提供与正在创建的虚拟机相关的配置信息。某些命令行选项是强制性的（明确要求必须提供`name`、`memory`和`disk`存储），而其他是可选的。

至少，`virt-install`命令通常需要以下参数：

- `--name`：分配给虚拟机的名称。
- `--memory`：分配给虚拟机的内存量。
- `--disk`：虚拟机存储镜像文件的名称和位置。`virt-install`将在创建虚拟机期间创建此文件，除非指定了`--import`选项，指示要使用现有镜像文件。
- `--cdrom`或`--location`：指定包含客户操作系统安装介质的本地路径或远程 ISO 镜像的 URL。

使用`virt-install`时所有可用参数的摘要可以在 man 手页中找到：

```bash
man virt-install
```

### 24.2 一个 RHEL 9 virt-install 命令示例

参考上述命令行参数列表，我们现在可以查看使用`virt-install`工具的命令行结构示例。

注意，为了显示虚拟机并完成安装，在`virt-install`实用程序启动后，必须有一个`virt-viewer`实例连接到虚拟机。默认情况下，`virt-install`将在虚拟机开始运行后尝试启动`virt-viewer`。然而，如果`virt-viewer`不可用，`virt-install`将等待直到建立`virt-viewer`。例如，如果宿主机具有图形界面，可以在本地运行图形会话，或者从远程客户端建立连接，如使用 virt-manager 在 RHEL 9 上创建 KVM 虚拟机章节所示。

以下命令创建一个使用 KVM 虚拟化运行 RHEL 9 的虚拟机。它创建一个新的 10GB 磁盘，为虚拟机分配 2048MB 内存，并为安装介质配置虚拟光驱：

```bash
virt-install --name demo_vm_guest --memory 2048 --disk path=/tmp/demo_vm_guest.img,size=10 --network network=default --cdrom /tmp/rhel-baseos-9.1-x86_64-dvd
```

在创建过程中，`virt-install`命令将显示创建进度的状态更新：

```text
Starting install...

Allocating ‘demo_vm_guest.img’ | 10 GB 00:00:01

Running graphical console command: virt-viewer --connect qemu:///system --wait demo_vm_guest
```

一旦客户系统创建，`virt-viewer`屏幕将显示从指定的安装介质加载的操作系统安装程序：

![](img/virt_install_screen.png)

图 24-1

从现在开始，按照标准的安装程序操作。

### 24.3 从命令行启动和停止虚拟机

从命令行创建虚拟机后，可能也需要从命令行启动它。这可以通过`virsh`命令行工具实现，并引用创建时分配的名称。例如：

```bash
virsh start demo_vm_guest
```

同样，可以通过以下方式向虚拟机发送关闭信号：

```bash
virsh shutdown demo_vm_guest
```

假设虚拟机未响应关闭信号且未开始正常关闭。在这种情况下，可以使用`destroy`指令销毁虚拟机（伴随数据丢失的风险）：

```bash
virsh destroy demo_vm_guest
```

## 24.4 从配置文件创建虚拟机

`virsh create`命令可以接受一个配置文件的名称作为参数，并基于该文件创建新的虚拟机。该配置文件使用 XML 格式。创建配置文件最简单的方法是导出现有虚拟机的配置，并针对新虚拟机对其进行修改。这可以通过`virsh dumpxml`命令实现。例如，以下命令将一个名为`demo_vm_guest`的虚拟机域的配置数据输出到名为`demo_vm_guest.xml`的文件中：

```bash
virsh dumpxml demo_vm_guest > demo_vm_guest.xml
```

一旦生成了该文件，将其加载到编辑器中，以检查并更改新虚拟机的设置。

至少，必须更改`<name>`、`<uuid>`和镜像文件路径`<source file>`，以避免与获取配置的虚拟机发生冲突。对于`UUID`，可以从文件中删除此行。

根据需要，也可以更改虚拟化类型、内存分配和 CPU 数量（这仅是其中的部分选项）。一旦修改了文件，可以按照以下方式创建新虚拟机：

```bash
virsh create demo_vm_guest.xml
```

## 24.5 总结

`KVM`提供了`virt-install`和`virsh`命令行工具，作为使用`Cockpit`和`virt-manager`工具创建和管理虚拟机实例的快速高效替代方案。这些工具的优势在于可以在脚本内部使用来实现虚拟机的自动化创建和管理。`virsh`命令还包含基于 XML 配置文件创建 VM 实例的选项。

## 25. 创建 RHEL 9 KVM 网络桥接接口

默认情况下，RHEL 9 上的`KVM`虚拟化环境创建一个虚拟网络，虚拟机可以连接到该网络。也可以使用`MacVTap`驱动配置直接连接。但是正如[虚拟化技术概述](#Virtualization_Overview.xhtml__idTextAnchor312)章节所述，这种方法不允许主机和客户系统进行通信。

本章旨在涵盖在 RHEL 9 上创建网络桥接的步骤，允许客户系统共享主机的一个或多个物理网络连接，同时允许客户和主机系统进行通信。

在本章的剩余部分，我们将解释如何为基于`KVM`的客户操作系统配置 RHEL 9 网络桥接。

### 25.1 获取当前的 Network Manager 设置

可以使用`NetworkManager`命令行界面工具（`nmcli`）创建网络桥接。`NetworkManager`在 RHEL 9 系统上默认安装并启用，负责检测和连接网络设备，并为管理网络配置提供接口。

主机系统当前的网络连接列表显示如下：

```bash
nmcli con show
```

```text
NAME UUID TYPE DEVICE
eno1 99d40009-6bb1-4182-baad-a103941c90ff ethernet eno1
virbr0 7cb1265e-ffb9-4cb3-aaad-2a6fe5880d38 bridge virbr0
```

上述输出显示主机已通过名为`eno1`的设备建立了以太网网络连接，并有一个名为`virbr0`的默认桥接接口，该接口提供了对`KVM`客户系统默认连接的基于虚拟网络的访问。

同样，可以使用以下命令识别系统上当前配置的设备（虚拟和物理设备）：

```bash
nmcli device show
```

```text
GENERAL.DEVICE: eno1
GENERAL.TYPE: ethernet
GENERAL.HWADDR: AC:16:2D:11:16:73
GENERAL.MTU: 1500
GENERAL.STATE: 100 (connected)
GENERAL.CONNECTION: eno1
GENERAL.CON-PATH: /org/freedesktop/NetworkManager/ActiveConnection/1
WIRED-PROPERTIES.CARRIER: on
IP4.ADDRESS[1]: 192.168.86.59/24
IP4.GATEWAY: 192.168.86.1
IP4.ROUTE[1]: dst = 0.0.0.0/0, nh = 192.168.86.1, mt = 100
IP4.ROUTE[2]: dst = 192.168.86.0/24, nh = 0.0.0.0, mt = 100
IP4.DNS[1]: 192.168.86.1
IP4.DOMAIN[1]: lan
IP6.ADDRESS[1]: fe80::6deb:f739:7d67:2242/64
IP6.GATEWAY: --
IP6.ROUTE[1]: dst = fe80::/64, nh = ::, mt = 100
IP6.ROUTE[2]: dst = ff00::/8, nh = ::, mt = 256, table=255
GENERAL.DEVICE: virbr0
GENERAL.TYPE: bridge
GENERAL.HWADDR: 52:54:00:59:30:22
GENERAL.MTU: 1500
GENERAL.STATE: 100 (connected)
GENERAL.CONNECTION: virbr0
GENERAL.CON-PATH: /org/freedesktop/NetworkManager/ActiveConnection/2
IP4.ADDRESS[1]: 192.168.86.59/24
...
```

### 25.2 从命令行创建网络桥接

创建桥接的第一步是添加新连接。这可以通过`nmcli`实现，指定该连接为桥接并提供：

```bash
nmcli con add type bridge con-name br0 master eno1
```

一旦添加了连接，连接列表应显示：

```bash
nmcli con show
```

```text
NAME UUID TYPE DEVICE
eno1 99d40009-6bb1-4182-baad-a103941c90ff ethernet eno1
virbr0 7cb1265e-ffb9-4cb3-aaad-2a6fe5880d38 bridge virbr0
```

下一步是启动桥接接口。指定`br0`和主设备`eno1`：

```bash
nmcli con up br0
```

如果通过网络连接（例如通过 SSH）执行桥接配置步骤，此步骤可能会有问题，因为在启用桥接连接之前必须关闭当前的`eno1`连接。这意味着远程主机可能无法访问。

如果您远程访问主机，可以通过创建一个脚本来执行更改以避免此问题。这将确保在`eno1`接口关闭后启用桥接接口。首先创建一个包含以下命令的`bridge.sh`脚本文件：

```bash
#!/bin/bash

nmcli con down eno1

nmcli con up br0
```

一旦创建了脚本，按如下方式执行：

```bash
sh ./bridge.sh
```

当脚本执行时，当`eno1`连接关闭时连接将会丢失。但在几秒钟后，一旦`br0`连接激活，就可以重新连接到主机。

如果您在主机本地操作，可以在终端窗口中运行两个`nmcli`命令而无丢失连接的风险：

```bash
nmcli con down eno1

nmcli con up br0
```

一旦桥接运行，连接列表现在应该包含桥接和桥接从设备连接：

```bash
nmcli con show
```



```text
NAME UUID TYPE DEVICE
br0 59b6631c-a283-41b9-bbf9-56a60ec75653 bridge br0
bridge-slave-eno1 395bb34b-5e02-427a-ab31-762c9f878908 ethernet eno1
virbr0 0fa934d5-0508-47b7-a119-33a232b03f64 bridge virbr0
eno1 66f0abed-db43-4d79-8f5e-2cbf8c7e3aff ethernet --
```

注意，`eno1` 连接仍然列在其中，但已不再活动。若要从列表中排除非活动连接，请请求列表时使用 `--active` 标记：

```bash
nmcli con show --active
```

```text
NAME UUID TYPE DEVICE
br0 c2fa30cb-b1a1-4107-80dd-b1765878ab4f bridge br0
bridge-slave-eno1 21e8c945-cb94-4c09-99b0-17af9b5a7319 ethernet eno1
virbr0 a877302e-ea02-42fe-a3c1-483440aae774 bridge virbr0
```

## 25.3 声明 KVM 桥接网络

此时，桥接连接已在系统上，但对 KVM 环境不可见。运行 `virsh` 命令仍然会将默认网络列出为唯一的可用网络选项：

```bash
virsh net-list --all
```

```text
Name State Autostart Persistent
----------------------------------------------------------
default active yes yes
```

在虚拟机使用桥接之前，必须对其进行声明并将其添加到 KVM 网络配置中。这涉及创建一个定义文件，并再次使用 `virsh` 命令行工具。

首先为名为 `bridge.xml` 的桥接网络创建一个定义文件，内容如下：

```xml
<network>
  <name>br0</name>
  <forward mode="bridge"/>
  <bridge name="br0" />
</network>
```

接下来，使用该文件定义新网络：

```bash
virsh net-define ./bridge.xml
```

一旦定义了网络，即可启动它，并在需要时将其配置为在每次系统重启时自动启动：

```bash
virsh net-start br0
virsh net-autostart br0
```

再次列出网络，以验证桥接网络现在是否在 KVM 环境内可用：

```bash
virsh net-list --all
```

```text
Name State Autostart Persistent
----------------------------------------------------------
br0 active yes yes
default active yes yes
```

## 25.4 在虚拟机中使用桥接网络

要创建一个使用桥接网络的虚拟机，请使用 `virt-install --network` 并指定 `br0` 桥接名称。例如：

```bash
virt-install --name demo_vm_guest --memory 1024 --disk path=/tmp/demo_vm_guest.img,size=10 --network network=br0 --cdrom /home/demo/rhel-baseos-9.1-x86_64-dvd.iso
```

当客户操作系统运行时，它将出现在与主机系统相同的物理网络上，而不再位于基于 NAT 的虚拟网络上。

也可以通过在 Cockpit 界面中编辑虚拟机、找到“网络接口”部分并点击“编辑”按钮（如下方的图 25-1 所示），为虚拟机选择桥接网络：

![](img/cockpit_network_interface.png)

图 25-1

在生成的接口设置对话框中，将“接口类型”菜单更改为“Bridge to LAN”（桥接到局域网），并将“源”设置为 `br0`，如图 25-2 所示：

![](img/cockpit_kvm_bridge.png)

图 25-2

同样，当使用 `virt-manager` 工具创建新虚拟机时，桥将在“网络”选择菜单中可用：

![](img/virt-manager_bridge.png)

图 25-3

若要修改现有虚拟机以使用桥接，请使用 `virsh edit` 命令。该命令将 XML 定义文件加载到编辑器中，可以在其中进行更改并保存：

```bash
virsh edit GuestName
```

默认情况下，文件将加载到 `vi` 编辑器中。若要使用不同的编辑器，请更改 `$EDITOR` 环境变量，例如：

```bash
export EDITOR=gedit
```

要更改默认虚拟网络，请找到文件的 `<interface>` 部分，对于 NAT 基配置，其内容如下：

```xml
<interface type='network'>
  <mac address='<your mac address here>'/>
  <source network='default'/>
  <model type='virtio'/>
  <address type='pci' domain='0x0000' bus='0x01' slot='0x00' function='0x0'/>
</interface>
```

或者，如果虚拟机使用的是直接连接，条目可能如下：

```xml
<interface type='direct'>
  <mac address='<your mac address here>'/>
  <source dev='eno1' mode='vepa'/>
  <model type='virtio'/>
  <address type='pci' domain='0x0000' bus='0x01' slot='0x00' function='0x0'/>
</interface>
```

若要使用桥接，在保存文件之前，将源网络属性更改为如下：

```xml
<interface type='network'>
  <mac address='<your mac address here>'/>
  <source network='br0'/>
  <model type='virtio'/>
  <address type='pci' domain='0x0000' bus='0x01' slot='0x00' function='0x0'/>
</interface>
```

## 25.5 使用 `nm-connection-editor` 创建桥接网络

若可以通过本地或远程桌面访问主机，可以使用 `nm-connection-editor` 完成大部分桥接配置。要使用该工具，在桌面打开终端并输入：

```bash
nm-connection-editor
```

当工具加载后，如图 25-4 所示的窗口将列出当前配置的网络：

![](img/connection_home.png)

图 25-4

要创建新连接，点击窗口左侧的 `+` 按钮。然后，在图 25-5 所示的对话框中，选择“Bridge”选项：

![](img/connection_type.png)

图 25-5

选中桥接选项后，点击“创建”按钮进入桥接配置界面。首先将连接和接口名称更改为 `br0`，然后点击如图 25-6 所示的“添加”按钮：

![](img/connection_edit_br0.png)

图 25-6

现在会出现另一个对话框，需要在其中配置桥接从。在此对话框中，从“设备”菜单选择桥接要连接的物理网络（例如，`eno1`）：

![](img/connection_port.png)

图 25-7

点击“保存”按钮应用更改并返回如图 25-6 所示的编辑 br0 对话框。在图 25-8，将菜单设置更改为“Ethernet”（以太网），然后点击“创建”按钮：

![](img/connection_ethernet_type.png)

图 25-8

返回主窗口后，新的桥接和从接连接现在应列在其中：

![](img/connection_bridge_added.png)

图 25-9

## 25.6 总结

默认情况下，KVM 虚拟机连接到使用 NAT 提供访问主机所在网络能力的虚拟网络。如果要求虚拟机以自己的 IP 地址出现在网络上，则需要配置它们共享主机的物理接口。本章概述了可以使用 `nmcli` 或 `nm-connection-editor` 工具创建桥接接口。

一旦完成此步骤，桥接即可供客户虚拟机使用。剩下的只需按照上一章概述的步骤停止原始 `eno1` 连接并启动 `br0` 连接（如果是远程访问主机，请在 shell 脚本中执行这些步骤）：

```bash
nmcli con down eno1
nmcli con up br0
```

正如使用命令行工具创建桥接时，还需要将此桥接添加到 KVM 网络配置中。要执行操作，请重复上述[声明 KVM 桥接网络](##KVM_Network_Bridge.xhtml__idTextAnchor361）节的步骤。

## 26. 使用 `virsh` 命令行工具管理 KVM

在之前的章节中，我们已经涵盖了在 RHEL 9 上安装和配置基于 KVM 的客户端操作系统。本章将探索 `virsh` 工具中之前章节未涵盖的其他领域，以及如何使用它从命令行管理基于 KVM 的客户端操作系统。

## 26.1 `virsh` Shell 与命令行

`virsh` 工具既是命令行工具，也是交互式 shell 环境。在命令行模式下使用时，通过命令提示符输入一组适用于任务的参数来发布命令。

要将选项作为命令行参数使用，请在终端命令提示符中使用，例如所示：

```bash
virsh <option>
```

`virsh` 工具在 shell 模式下使用时，提供了一个交互环境，可以在其中执行系列命令。

要在 `virsh` shell 中运行命令，请执行以下命令：

```text
virsh

Welcome to virsh, the virtualization interactive terminal.

Type: 'help' for help with commands

      'quit' to quit

virsh #
```

在 `virsh #` 提示符处，输入想要运行的选项。例如，下面的 `virsh` 会话列出了当前的虚拟机，启动一个名为 `FedoraVM` 的虚拟机，然后获取另一个列表以验证该虚拟机正在运行：

```text
virsh

Welcome to virsh, the virtualization interactive terminal.

Type: 'help' for help with commands

      'quit' to quit

virsh # list

 Id Name State

----------------------------------------------------

 8 RHEL9VM running

 9 CentOS9VM running

virsh # start FedoraVM

Domain FedoraVM started

virsh # list

 Id Name State

----------------------------------------------------

 8 RHEL9VM running

 9 CentOS9VM running

10 FedoraVM running

virsh#
```

`virsh` 工具支持广泛的命令，可以使用帮助选项获取其完整列表：

```bash
virsh help
```

通过在帮助指令后指定命令，可以获取有关每个命令语法的更多细节：

```text
virsh help restore

  NAME

    restore - restore a domain from a saved state in a file

  SYNOPSIS

    restore <file> [--bypass-cache] [--xml <string>] [--running] [--paused]

  DESCRIPTION

    Restore a domain.

  OPTIONS

    [--file] <string> the state to restore

    --bypass-cache avoid file system cache when restoring

    --xml <string> filename containing updated XML for the target

    --running restore domain into running state

    --paused restore domain into paused state
```

在本章的剩余部分，我们将详细地查看其中一些命令。

## 26.2 列出客户系统状态

可以使用 `virsh` 工具的 `list` 选项随时查看 RHEL 9 虚拟化主机上客户系统的状态。例如：

```bash
virsh list
```

上述命令将显示输出，其中每个客户系统都占有一行，类似于下所示：

```text
virsh # list

 Id Name State

----------------------------------------------------

 8 RHEL9VM running

 9 CentOS9VM running

10 FedoraVM running
```

## 26.3 启动客户系统

可以使用 `virsh` 工具结合 `start` 选项后跟要启动的客户操作系统的名称来启动客户操作系统。例如：

```bash
virsh start myGuestOS
```

## 26.4 关闭客户系统

`virsh` 工具的 `shutdown` 选项顾名思义，用于关闭客户操作系统：

```bash
virsh shutdown guestName
```

注意，`shutdown` 允许客户操作系统在接收到指令时执行有序关。要立即停止客户操作系统，可以使用 `destroy`（存在文件系统损坏和数据丢失的风险）：

```bash
virsh destroy guestName
```

## 26.5 挂起和恢复客户系统

可以使用 `virsh` 工具的 `suspend` 和 `resume` 选项挂起和恢复客户系统。例如，挂起特定系统：

```bash
virsh suspend guestName
```

同样，恢复挂起的系统：

```bash
virsh resume guestName
```

如果主机系统重启，挂起的会话将丢失。此外，请注意挂起的系统仍然留在内存中。因此，为了保存会话使其不再占用内存并能恢复到精确状态（即使在重启后），有必要保存并恢复客户机。

## 26.6 保存和恢复客户系统

可以使用 `virsh` 实用程序保存和恢复运行中的客户操作系统。保存时，客户系统的当前状态被写入磁盘并从系统内存中移除。保存的系统随后可以随时恢复（包括在主机系统重启后）。

保存客户机：

```bash
virsh save guestName path_to_save_file
```

恢复保存的客户操作系统会话：

```bash
virsh restore path_to_save_file
```

## 26.7 重启客户系统

重启客户操作系统：

```bash
virsh reboot guestName
```

## 26.8 配置分配给客户操作系统的内存

使用 `virsh` 命令的 `setmem` 选项配置分配给客户操作系统的内存。例如，以下命令将分配给系统的内存减少到 256MB：

```bash
virsh setmem guestName 256
```



注意，允许的内存设置必须在可用内存范围内。可以使用`setmaxmem`选项增加。

## 26.9 总结

`virsh`工具提供了创建、监控和管理虚拟机的各种选项。正如本章所述，该工具可以在命令行或交互式模式下使用。

## 27. Linux 容器简介

之前的章节涵盖了虚拟化概念，重点讨论了使用 KVM 创建和管理虚拟机。本章将引入容器形式的相关技术。虽然虚拟机和容器之间存在某些相似之处，本章将概述它们的关键区别，并介绍 Linux 容器的概念和优势。本章还将概述 RHEL 9 容器管理工具。在本章介绍容器的基础知识后，下一章将通过实例演示如何在 RHEL 9 上创建和运行容器。

### 27.1 Linux 容器与内核共享

简单来说，Linux 容器是虚拟化的轻量级替代方案。虚拟机在虚拟环境中包含并运行整个客户操作系统。虚拟机则运行在虚拟机程序等环境之上，虚拟机程序管理对主机物理资源的访问。

容器通过使用称为内核共享的概念来工作，这利用了 Linux 和基于 Unix 操作系统的体系设计。

要理解内核共享和容器的工作原理，首先有助于理解 Linux 或 Unix 操作系统的两个主要组件。操作系统的核心是内核。简单来说，内核处理操作系统与物理硬件之间的所有交互。第二个关键组件是根文件系统，它包含了操作系统运行所需的所有库、文件和实用程序。利用这种结构，每个容器都有自己的根文件系统，但共享主机操作系统的内核。这种结构在下方的图 27-1 架构图中所示。

这种类型的资源共享是通过内核能够动态地将当前根文件系统（该概念称为切换根或`chroot`）更改到不同的根文件系统，而无需重启整个系统来实现。这种能力是 Linux 容器的基础，并结合了容器运行时。容器运行时的职责是为宿主机系统提供执行和管理容器的接口。目前有多种容器运行时可用，包括`Docker`、`lxd`、`containerd`和`CRI-O`。早期的 RHEL 版本默认使用`Docker`，但在 RHEL 9 中`Podman`已取代其成为默认工具。

![](img/linux_container_diagram.png)

图 27-1

### 27.2 容器的用途与优势

容器的主要优势是它们比虚拟化所需的资源开销少得多，这允许在单个服务器上同时运行许多容器实例。它们可以根据需求水平快速高效地启动和停止。此外，容器在宿主机上原生运行，提供了虚拟机无法比拟的性能。

容器还具有高度的可移植性，可以轻松在系统之间迁移。结合`Docker`、`OpenShift`和`Kubernetes`等容器管理系统，可以在跨越多个服务器和云平台的大规模范围内部署和管理容器，可能运行成千上万个容器。

容器经常用于为应用程序创建轻级执行环境。在这种场景下，每个容器都提供了一个隔离的环境，其中包含了应用程序以及该运行所需的所有运行时和支持文件。然后可以将容器部署到任何其他支持容器执行的兼容宿主机系统上运行，且无需担心目标系统可能缺少应用程序所需的运行时配置——应用程序的所有依赖项都已经在容器中了。

在桥接开发环境和生产环境之间的差距时，容器非常有帮助。通过在容器中进行开发和测试（QA）工作，可以将它们安全地传递到生产环境并启动，因为应用程序在开发和测试时相同的容器环境中运行。

容器还促进了部署大型复杂解决方案的模块化方法。与其将应用程序开发为单一的整体实体，可以使用容器将应用程序设计为一组相互作用的模块，每个模块运行在单独的容器中。

的一个的一个缺点是，客户操作系统必须与共享的内核版本兼容。例如，无法在 Linux 系统的容器中运行微软 Windows。同样，为 2.6 版本内核设计的 Linux 客户系统无法共享 2.4 版本的内核。然而，这些要求并不是容器的设计初衷。与其将这些限制视为局限性，不如将这些限制视为容器提供简单、可扩展且可靠部署平台的某些关键优势。

### 27.3 RHEL 9 容器工具

RHEL 9 提供了多种用于创建、检查和管理容器工具。主要工具如下：

- `buildah` – 一个用于构建容器镜像的命令行工具。
- `podman` – 一个基于命令行的容器运行时和管理工具。执行诸如从远程仓库下载容器镜像，以及检查、启动和停止镜像等任务。
- `skopeo` – 一个命令行实用程序，用于转换容器镜像、在仓库之间复制镜像以及在不下载的情况下检查存储在仓库中的镜像。
- `runc` – 一种轻级容器运行时，用于从命令行启动和运行容器。
- `OpenShift` – 一个企业级容器应用程序管理平台，由命令行和基于 Web 的工具组成。

上述所有工具都符合开放容器倡议（`OCI`），这是一套旨在确保容器在竞争性的工具和平台之间遵循相同规范。

### 27.4 容器目录、存储库和注册表

红帽容器目录（`RHCC`）提供了一系列由红帽测试过的预构建镜像，这些镜像可以被下载并作为自定义容器镜像的基础。可以通过以下 URL 访问 RHCC：

`https://catalog.redhat.com/software/containers/search`

完成搜索后，目录将显示匹配的存储库列表。在此语境下，存储库是相关镜像的集合。例如，图 27-2 显示了适用于 RHEL 9 相关容器的可用容器镜像存储库部分列表。

![](img/rhel_container_search.png)

图 27-2

从列表中选择存储库将显示有关该存储库的详细信息。在目录中查看存储库时，关键信息是存储库名称和存储该存储库的注册表位置。在下载容器镜像使用时，必须引用这两个项规范。

### 27.5 容器网络

默认情况下，容器使用容器网络接口（`CNI`）桥接网络栈连接到网络。在桥接配置中，运行在服务器上的所有容器都属于同一个子网，因此可以相互通信。容器还通过桥接宿主机系统的网络连接到外部网络。同样，宿主机可以通过虚拟网络接口（通常命名为`podman0`）访问容器，该接口作为容器工具安装的一部分而被创建。

### 27.6 总结

Linux 容器提供了虚拟化的化的替代方案，并利用了 Linux 和 Unix 操作系统的结构。Linux 容器共享主机操作系统的内核，每个容器都有自己的包含文件、库和应用程序的根文件系统。因此，容器是高效且可扩展的，为构建和部署模块化企业级解决方案提供了理想平台。此外，还有多种工具和平台用于构建、部署和管理容器，包括第三方解决方案和红帽提供的解决方案。

# 28. 在 RHEL 9 上使用容器

在上章中涵盖了 Linux 容器的基础知识，本章将演示如何在 RHEL 9 上使用`Podman`、`Skopeo`和`Buildah`工具创建和管理容器。在本章结束时，你将对 RHEL 9 上创建和管理容器有更清晰的理解。此外，你将获得继续探索 Linux 容器能力的知识基础。

## 28.1 安装容器工具

在开始使用容器之前，第一步是使用以下命令安装上一章概述的所有容器工具：

```bash
dnf install container-tools
```

## 28.2 登录红帽容器注册表

首先，将使用红帽容器注册表中提供的现有镜像创建一个容器。然而在从注册表拉取镜像到本地系统之前，必须必须使用现有的红帽凭据通过`podman`工具登录注册表：

```bash
podman login registry.redhat.io
```

用户名：`yourusername`

密码：`yourpassword`

登录成功！

## 28.3 拉取容器镜像

本例将从注册表拉取 RHEL 9 通用基础镜像（`UBI`）。在拉取镜像之前，可以使用`skopeo`工具获取镜像存储库的信息，例如：

```bash
skopeo inspect docker://registry.redhat.io/ubi9/ubi-init
```

```json
{
    "Name": "registry.redhat.io/ubi9/ubi-init",
    "Digest": "sha256:82352ed85d5dd55efd8d32a7eae998afded2769fc1b517cc4383301da1936a58",
    "RepoTags": [
        "9.1.0-15",
        "9.1.0-12",
        "9.0.0-16",
        "9.0.0-19",
        "9.1.0",
        "9.0.0",
        "9.0.0-16.1655192132",
        "9.0.0-26.1666626006",
        "9.0.0-26.166507205",
        "9.0.0-16.1655192132-source",
        "9.1.0-5.166963213-source",
        "9.0.0-26.1666626006-source",
        "9.1.0-2-source",
        "9.1.0-5.1669025017-source",
        "9.1.0-5.166963213",
        "9.0.0-26.166507205-source",
        "9.1.0-5.1669025017",
        "9.1",
        "9.0.0-28",
        "9.0.0-29",
        "9.1.0-12.167578985-source",
        "9.0.0-23",
        "9.0.0-26",
        "9.0.0-26-source",
        "9.0.0-28-source",
        "9.1.0-5-source",
        "9.0.0-29-source",
        "9.1.0-15-source",
        "9.1.0-5",
        "9.0.0-19-source",
        "9.0.0-16-source",
        "9.0.0-23-source",
        "9.1.0-12.167578985",
        "latest"
    ],
    "Created": "2023-02-22T13:55:53.95767647Z",
    "DockerVersion": "",
    "Labels": {
        "architecture": "x86_64",
        "build-date": "2023-02-22T13:54:21",
        "com.redhat.component": "ubi9-init-container",
        "com.redhat.license_terms": "https://www.redhat.com/en/about/red-hat-end-user-license-agreements#UBI",
        "description": "The Universal Base Image Init is designed to run an init system as PID 1 for running multi-services inside a container. This base image is freely redistributable, but Red Hat only supports Red Hat technologies through subscriptions for Red Hat products. This image is maintained by Red Hat and updated regularly."
    }
}
```

此`ubi-init`镜像是用于构建最小化操作系统容器的 RHEL 9 基础镜像，并将作为本章示例的基础。在确认这确实是正确的镜像后，将使用以下`podman`命令将镜像拉取到本地系统：

```bash
podman pull docker://registry.redhat.io/ubi9/ubi-init
```

正在拉取`docker://registry.redhat.io/ubi9/ubi-init`……正在获取镜像源签名

```text
Copying blob 340ff6d7f58c done
Copying blob 0e8ea260d026 done
Copying blob c3bd58a6898a done
Copying config a4933472b1 done
Writing manifest to image destination
Storing signatures
a4933472b168b6bd21bc492dc1e72bb2805d4174399f5a213
```

通过让`podman`列出所有本地镜像来验证镜像已存储：

```bash
podman images
```

```text
REPOSITORY TAG IMAGE ID CREATED SIZE
registry.redhat.io/ubi9/ubi-init latest a4933472b168 6 weeks ago 254 MB
```

通过运行`podman inspect`命令可以获取有关本地镜像的详细信息：

```bash
podman inspect registry.redhat.io/ubi9/ubi-init
```

此命令输出的信息应与本章稍之前对远程镜像执行的`skopeo`命令输出相同。

## 28.4 在容器中运行镜像

从仓库拉取的镜是一个完全可运行的镜像，可以在无需修改的情况下在容器中运行。要运行镜像，请使用`podman run`命令。在这种情况下，将指定`--rm`选项，表示我们要在容器中运行镜像、执行一个命令并让容器退出。在这种情况下，将使用`cat`工具输出容器文件系统上的`/etc/passwd`文件内容：

```bash
podman run --rm registry.redhat.io/ubi9/ubi-init cat /etc/passwd
```

```text
root:x:0:0:/root:/bin/bash
bin:x:1:1:/bin:/sbin/nologin
daemon:x:2:2:/daemon:/sbin/nologin
adm:x:3:4:/adm:/sbin/nologin
lp:x:4:7:/var/spool/lp:/sbin/nologin
sync:x:5:0:/sync:/bin/sync
shutdown:x:6:0:/shutdown:/sbin/shutdown
halt:x:7:0:/halt:/sbin/halt
```

一旦按照你的要求配置了容器客体系统，你很可能想要创建并运行多个这种特定类型的容器。要实现这一点，需要将容器保存为镜像到本地存储中，以作为其他容器实例的基础。这通过使用`podman commit`命令结合容器的名称或 ID 以及存储该镜像的名称来实现，例如：

```bash
podman commit mycontainer myrhel_image
```

镜像保存好后，检查它现在是否出现在本地存储库的镜像列表中：

```bash
podman images
```

```text
REPOSITORY TAG IMAGE ID CREATED SIZE
localhost/myrhel_image latest 4d207635db6c 9 seconds ago 239 MB
registry.redhat.io/ubi9/ubi-init latest a4933472b168 6 weeks ago 254 MB
```

现在可以使用保存的镜像来创建与原始容器相同的容器：

```bash
podman run --name=mycontainer2 -it localhost/myrhel_image /bin/bash
```

## 28.5 从本地存储中删除镜像

当镜像不再需要时，要从本地存储中删除，请运行`podman rmi`命令，引用`podman images`命令输出的镜像名称或 ID。例如，要删除上一节创建的名为`myrhel_image`的镜像，请如下运行`podman`：

```bash
podman rmi localhost/myrhel_image
```

在删除镜像之前，必须先删除基于该镜像的所有容器。

## 28.6 删除容器

即使容器已经退出或停止，它仍然存在并可以随时重启。如果容器不再需要，可以在容器停止后使用`podman rm`命令按如下删除：

```bash
podman rm mycontainer2
```

## 28.7 使用 Buildah 构建容器

Buildah 允许从现有容器、镜像或完全从零开始构建新容器。Buildah 还包含了挂载容器文件系统的功能，以便从宿主机上对其进行访问和修改。

例如，以下`buildah`命令将从 RHEL 9 基础镜像构建容器（如果镜像尚未从存储库拉取，`buildah`将在创建容器之前下载它）：

```bash
buildah from registry.redhat.io/ubi9/ubi-init
```

运行此命令的结果将得到一个名为`ubi-init-working-container`的就绪运行的容器：

```bash
buildah run ubi-init-working-container cat /etc/passwd
```

## 28.8 从零构建容器

从零构建容器会创建一个空容器。一旦创建，就可以安装软件包以满足容器的要求。在创建一个仅需要安装最软件包的容器时，这种方法非常有用。

从零开始构建的第一步是运行以下命令来构建空容器：

```bash
buildah from scratch
```

```text
working-container
```

构建完成后，将创建一个名为`working-container`的新容器：

```bash
buildah containers
```

```text
CONTAINER ID BUILDER IMAGE ID IMAGE NAME CONTAINER NAME
```



`dbed2be11730 * cb642e6a9917 registry.redhat.io/ubi9/ubi:latest dbed2be1173000c099ff29c96eae59aed297b82412b240a8ed29ecec4d39a8ba`

`17df816ea0bb * a4933472b168 registry.redhat.io/ubi9/ubi-init:latest ubi-init-working-container`

`65b424a31039 * scratch working-container`

空容器现在准备好安装一些软件包了。遗憾的是，这不能在容器内执行，因为甚至不存在 `bash` 或 `dnf` 工具。因此，需要将容器文件系统挂载到宿主机系统，并使用 `dnf` 安装软件包，并将系统根设置为挂载的容器文件系统。通过如下挂载容器的文件系统开始此过程：

```bash
buildah mount working-container
```

`/var/lib/containers/storage/overlay/20b46cf0e2994d1ecdc4487b89f93f6ccf41f72788da63866b6bf80984081d9a/merged`

如果文件系统挂载成功，`buildah` 将输出容器文件系统的挂载点。现在我们有了容器文件系统的访问权限，可以使用 `dnf` 命令通过 `--installroot` 选项指向挂载的容器文件系统向容器安装软件包。例如，以下命令在容器文件系统中安装 `bash`、`CoreUtils` 和 `dnf` 软件包（其中 `<container_fs_mount>` 是之前 `buildah mount` 命令输出的挂载路径）：

```bash
dnf install --releasever=9.1 --installroot <container_fs_mount> bash coreutils dnf
```

注意，`--releasever` 选项指示 `dnf` 在容器内安装 RHEL 9.1 的软件包。

安装完成后，如下卸载文件系统：

```bash
buildah umount working-container
```

一旦 `dnf` 完成安装，就可以运行容器并如下访问 `bash` 提示符：

```bash
buildah run working-container bash
```

## 28.11 容器桥接网络

如上一节所述，容器网络通过容器网络接口（CNI）桥接栈实现。以下命令显示了宿主机上运行容器的典型配置：

```bash
ip a
```

```text
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
   link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
   inet 127.0.0.1/8 scope host lo
      valid_lft forever preferred_lft forever
   inet6 ::1/128 scope host
      valid_lft forever preferred_lft forever

2: eno1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc qcodel state UP group default qlen 1000
   link/ether 00:23:24:52:57:ff brd ff:ff:ff:ff:ff altp0s25
   inet 192.168.86.35/24 brd 192.168.86.255 scope global eno1
      valid_lft 68525 preferred_lft 68525
   inet6 fd7f:886f:716a:0:223:24ff:fe52:557/64 scope dynamic noprefix
      valid_lft 1619 preferred_lft 1619
   inet6 fe80::223:24ff:fe52:557/64 scope link noprefix
      valid_lft forever preferred_lft forever

3: veth1d7e073@if2: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master podman state UP group default qlen 1000
   link/ether 3e:3a:54:b8:d8:e1 brd ff:ff:ff:ff:ff:ff link-netns netns-658a3069-5c69-185f-ef34-621107daa71
   inet6 fe80::3c3a:54ff:feb8:d8e1/64 scope link
      valid_lft forever preferred_lft forever

6: podman0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
   link/ether 3e:3a:54:b8:d8:e1 brd ff:ff:ff:ff:ff:ff
   inet 10.88.0.1/16 brd 10.88.255.255 scope global podman0
      valid_lft forever preferred_lft forever
   inet6 fe80::45e:83ff:fe68:4067/64 scope link
      valid_lft forever preferred_lft forever
```

在示例中，宿主机有一个名为 `eno1` 的接口连接到外部网络，IP 地址为 `192.168.86.35`。此外，还创建了一个名为 `podman0` 的虚拟接口并分配了 IP 地址 `10.88.0.1`。在宿主机运行的容器上运行相同的 `ip` 命令可能会如下输出：

```bash
ip a
```

```text
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
   link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
   inet 127.0.0.1/8 scope host lo
      valid_lft forever preferred_lft forever
   inet6 ::1/128 scope host
      valid_lft forever preferred_lft forever

2: eth0@if3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
   link/ether b6:fb:88:16:8b:5e brd ff:ff:ff:ff:ff:ff link-netnsid 0
   inet 10.88.0.8/16 brd 10.88.255.255 scope global eth0
      valid_lft forever preferred_lft forever
   inet6 fe80::b4fb:88ff:fe16:8b5e/64 scope link
      valid_lft forever preferred_lft forever
```

在这种情况下，容器的 IP 地址为 `10.88.0.8`。在宿主机上运行 `ping` 命令可以验证宿主机和容器确实在同一个网段内：

```bash
ping 10.88.0.8
```

```text
PING 10.88.0.8 (10.88.0.8) 56(84) bytes of data.
64 bytes from 10.88.0.28: icmp_seq=1 ttl=64 time=0.056 ms
64 bytes from 10.88.0.28: icmp_seq=2 ttl=64 time=0.039 ms
.
.
```

我们还可以使用 `podman network ls` 命令来获取主机系统上当前可用容器网络列表：

```bash
podman network ls
```

```text
NETWORK ID NAME DRIVER
2f259bab93aa podman bridge
```

可以使用以下命令显示有关容器网络的详细信息，在本例中，即上述 `podman` 网络：

```bash
podman network inspect podman
```

```json
[
    {
        "name": "podman",
        "id": "2f259bab93aaaaa2542ba43ef33eb990d0999ee1b4b557b7be53c0b7a1bb9",
        "driver": "bridge",
        "network_interface": "podman0",
        "created": "2023-04-11T08:49:20.489892751-04:00",
        "subnets": [
            {
                "subnet": "10.88.0.0/16",
                "gateway": "10.88.0.1"
            }
        ],
        "ipv6_enabled": false,
        "internal": false,
        "dns_enabled": false,
        "ipam_options": {
            "driver": "host-local"
        }
    }
]
```

使用以下语法创建新的容器网络：

```bash
podman network create <network name>
```

例如，要创建一个名为 `demonet` 的新网络，可以使用以下命令：

```bash
podman network create demonet
```

可以使用 `podman network ls` 命令来验证新网络是否存在：

```bash
podman network ls
```

```text
NETWORK ID NAME DRIVER
9692930055dc demonet bridge
2f259bab93aa podman bridge
```

一旦创建了网络，可以如下所示将其分配给容器：

```bash
podman network connect demonet mycontainer
```

相反，可以使用 `podman network disconnect` 命令将容器从网络断开：

```bash
podman network disconnect demonet mycontainer
```

当创建新的容器网络时，在 `/etc/containers/networks` 目录下会生成一个名为 `<network name>.json` 的配置文件。在上面的示例中，将创建一个名为 `demonet.json` 的文件，内容如下：

```json
{
    "name": "demonet",
    "id": "9692930055dc6ceea5cc4d0720df548daa521fe62e23ca3659a9815664bca2f6",
    "driver": "bridge",
    "network_interface": "podman1",
    "created": "2023-04-10T16:54:35.618056082-04:00",
    "subnets": [
        {
            "subnet": "10.89.0.0/24",
            "gateway": "10.89.0.1"
        }
    ],
    "ipv6_enabled": false,
    "internal": false,
    "dns_enabled": true,
    "ipam_options": {
        "driver": "host-local"
    }
}
```

可以对此文件进行修改以更改设置，例如子网地址范围、IPv6 支持和网络类型（本例设置为 `bridge`），以实现不同的配置。最后，我们可以使用以下命令删除自定义网络：

```bash
podman network rm demonet
```

## 28.12 在 Cockpit 中管理容器

除了本章概述的命令行工具外，还可以使用 Cockpit Web 界面创建和管理 Linux 容器。假设系统已安装并启用了 Cockpit，并且已完成登录 Red Container Registry 的步骤，登录 Cockpit 并选择 Podman Containers 选项。如果 Cockpit 中未安装 Podman 模块，打开终端窗口并运行以下命令：

```bash
dnf install cockpit-podman
```

如有必要，点击按钮启动 Podman 服务，此时屏幕应类似于图 28-1 所示。第一步是下载一个镜像作为容器的基础（除非已使用命令行工具下载了镜像）。要执行下载，点击上方图 28-1 中由箭头标记的菜单按钮，并选择 Download image 选项。当搜索对话出现时，在搜索框中输入关键词。图 28-2 显示了搜索 RHEL 9 通用镜像的结果。

一旦找到镜像，选择它并点击 Download 按钮从仓库中拉取。下载完成后，它将出现在镜像列表中，如下。

## 28.13 总结

本章介绍了如何使用 `podman`、`skopeo` 和 `buildah` 工具以及 Cockpit Web 界面在 RHEL 上创建和管理容器，包括从仓库获取镜像以及从零构建新镜像。

# 29. 在 RHEL 9 上设置服务器

Apache 服务器是 RHEL 9 许多软件包之一。RHEL 9 的扩展性和韧性使其成为托管高流量网站的理想平台。本章将解释如何在 RHEL 9 上配置 Apache 作为 Web 服务器，包括安全（HTTPS）和不安全（HTTP）配置。

## 29.1 配置 RHEL 9 服务器的要求

要设置自己的网站，您需要计算机（或云服务器实例）、操作系统、Web 服务器、域名、名称服务器以及一个 IP 地址。在操作系统方面，我们假设使用的是 RHEL 9。如前所述，RHEL 9 支持 Apache 服务器，在操作系统启动后可以轻松安装。此外，可以使用任何域名注册服务注册域名。

如果你在云实例上运行 RHEL 9，提供商分配的 IP 地址将位于服务器概况中。然而，如果你托管自己的服务器且互联网服务提供商（ISP）分配了静态 IP 地址，你必须将域名与该地址关联。这是通过名称服务器实现的。

如果你没有静态 IP 地址（即 ISP 提供的是经常变化的动态地址），可以使用若干免费的动态 DNS（DDNS 或简称 DynDNS）服务将您的动态 IP 地址映射到您的域名。

一旦配置了域名和名称服务器，下一步是安装并配置 Web 服务器。

### 29.2 安装 Apache 服务器软件包

当前版本的 RHEL 默认不安装 Apache Web 服务器。要检查是否已安装，运行以下命令：

```bash
rpm -q httpd
```

如果 `rpm` 生成了类似下面的输出，则表示 Apache 服务器已经安装：

```text
httpd-2.4.53-7.el9_1.5.x86_64
```

或者，如果 `rpm` 生成了“package httpd is not installed”的消息，下一步是安装它。要安装 Apache，请在命令行提示符中运行以下命令：

```bash
dnf install httpd
```

## 29.3 配置防火墙

在启动和测试 Apache Web 服务器之前，必须修改防火墙以允许 Web 服务器与外部世界通信。默认情况下，`HTTP` 和 `HTTPS` 协议分别使用端口 80 和 443，因此，取决于所使用的协议，需要打开其中一个或两个端口。在打开端口时，请务必指定适用于面向互联网的网络连接的防火墙区域：

```bash
firewall-cmd --permanent --zone=<zone> --add-port=80/tcp
firewall-cmd --permanent --zone=<zone> --add-port=443/tcp
```

打开必要的端口后，请务必重载防火墙设置：

```bash
firewall-cmd --reload
```

在云托管服务器上，可能还需要在云控制台中为服务器实例启用相应的端口。请检查云提供商的文档以获取执行此步骤。

## 29.4 端口转发

假设托管 Web 服务器的 RHEL 9 系统位于受防火墙保护的网络中（另一台运行防火墙的计算机、路由器或包含内置防火墙保护的无线基站）。情况下，你必须配置防火墙将端口 80 和 443 转发到你的 Web 服务器系统。执行此操作的机制在防火墙和设备之间不同，因此请检查您的文档了解如何配置端口转发。

## 29.5 启动 Apache Web 服务器

一旦安装了 Apache 并配置了防火墙，下一步是验证服务器正在运行并在时启动它。

要从命令行检查 Apache 服务的状态，请在命令行提示符输入以下内容：

```bash
systemctl status httpd
```

如果上述命令指示 `httpd` 服务未运行，可以按如下方式从命令行启动它：

```bash
systemctl start httpd
```



如果您希望 Apache `httpd` 服务在系统启动时自动启动，请运行以下命令：

```bash
systemctl enable httpd
```

## 29.6 测试 Web 服务器

安装完成后，下一步是验证 Web 服务器是否正在运行。

如果您可以（本地或远程）访问服务器的桌面环境，请启动浏览器并在地址栏中输入 `http://127.0.0.1`（`127.0.0.1` 是回环网络地址，告诉系统连接到本地机器）。如果所有设置正确，浏览器应该加载如图 29-1 所示的测试页面：

![测试页面](img/rhel_apache_test_page.png)

图 29-1

如果无法使用桌面环境，请从服务器所在的同一局域网中的另一个系统连接，或者如果是远程托管的，请使用分配给系统的外部 IP 地址。

## 29.7 为您的域名配置 Apache Web 服务器

设置 Web 服务器的下一步是为您的域名进行配置。要配置 Web 服务器，首先更改目录到 `/etc/httpd`，该目录包含若干文件和子目录。进入 `conf` 子目录，你将在其中找到一个名为 `httpd.conf` 的文件，其中包含 Apache 服务器的配置设置。

使用具有超级用户权限的您常用的编辑器编辑 `httpd.conf` 文件，以确保你有权限访问并修改该文件。加载文件后，需要更改几项设置以匹配您的环境。

为特定域名配置 Apache 的最方法是在 `httpd.conf` 文件中添加虚拟主机条目。这允许单个 Apache 服务器通过为每个站点域名添加虚拟主机条目来支持多个网站。在 `httpd.conf` 文件中，按如下所示为您的域名添加虚拟主机条目：

```apache
<VirtualHost *:80>
    ServerAdmin feedback@myexample.com
    ServerName www.myexample.com
    DocumentRoot /var/www/myexample
    ErrorLog logs/myexample_error_log
    CustomLog logs/myexample_access_log combined
</VirtualHost>
```

上述虚拟主机条目中的 `ServerAdmin` 指令定义了想要联系您站点 Web 管理员的人员电子邮件地址。请将其更改为可以联系到您的适当电子邮件地址。

接下来，声明 `ServerName`，以便 Web 服务器知道与此虚拟主机关联的域名。

由于服务器支持的每个网站将有自己的文件，因此使用 `DocumentRoot` 设置来指定该网站域名文件的位置。传统上使用 `/var/www/domain-name`，例如：

```apache
DocumentRoot /var/www/myexample
```

最后，为访问历史和错误日志文件添加条目。

按照 `httpd.conf` 文件中的声明创建 `/var/www/<domain name>` 目录，并在其中放置一个包含基础 HTML 的 `index.html` 文件。例如：

```html
<html>
<title>Sample Web Page</title>
<body>
Welcome to MyExample
</body>
</html>
```

最后一步是重启 `httpd` 服务以确保新设置生效：

```bash
systemctl restart httpd
```

最后，通过浏览器访问域名（而不是 IP 地址）来检查服务器工作正常。加载的页面应该是上面创建的 `index.html`。

## 29.8 安全网站的基础

本章创建的 Web 服务器和网站使用端口 80 上的 `HTTP` 协议，因此被认为是不安全的。问题在于服务器与客户端（通常是用户的浏览器）之间的流量是明文传输的。也就是说，数据未加密且易被截获。在执行登录网站或传输敏感信息等任务时，这是一个严重的缺陷。

如今，网站预计使用 `HTTPS`，它建立了安全的加密通信。这种安全性通过公钥、私钥和会话加密的使用来实现。

为了支持 `HTTPS`，网站必须拥有由受信任权威（CA）颁发的证书。当浏览器连接到安全网站时，Web 服务器会发送网站的 SSL 证书，其中包含网站的公钥。浏览器随后验证证书的真实性。

如果证书有效，浏览器使用发送的公钥加密会话密钥并传递给服务器。服务器使用私钥解密密钥以发送加密确认。一旦完成此过程，浏览器和服务器在使用会话密钥加密后续数据。

## 29.9 为 Apache 配置 HTTPS

默认情况下，Apache 服务器不包含实现安全 HTTPS 网站所需的模块。因此，第一步是在服务器系统上安装 Apache `mod_ssl` 模块：

```bash
dnf install mod_ssl
```

安装完成后重启 `httpd` 将新模块加载到 Apache 服务器中：

```bash
systemctl restart httpd
```

使用以下命令检查模块是否已加载到服务器：

```bash
httpd -M | grep ssl_module
```

```text
ssl_module (shared)
```

一旦 `ssl_module` 安装完成，重复本章上一节的步骤为网站创建配置文件，这次使用 `sites-available/default-ssl.conf` 文件作为站点配置文件的模板。

假设模块已安装，下一步是为网站生成 SSL 证书。

## 29.10 获取 SSL 证书

网站的证书必须从证书颁发机构（Certificate Authority）获取。有多种价格范围的选择供选择。然而，到目前为止最好的选项是从以下 URL 从 Let’s Encrypt 获取免费证书：

[letsencrypt.org](https://letsencrypt.org/)

从 Let’s Encrypt 获取证书涉及安装和运行 `Certbot` 工具。该工具将扫描服务器上的 Apache 配置文件，并提供为系统上配置的任何虚拟主机生成证书的选项。随后，它将生成证书并为相应的网站在 Apache 配置文件中添加虚拟主机条目。

按照 Let’s Encrypt 网站上的步骤在您的 RHEL 9 系统上下载并安装 `Certbot`，然后按照如下方式运行 `certbot` 工具来生成并安装证书：

```bash
certbot --apache
```

在请求电子邮箱地址并寻求接受服务条款后，`certbot` 将列出在 `httpd.conf` 文件中找到域名，并允许选择一个或多个需要安装证书的站点。`Certbot` 然后在获取并将证书安装到系统之前将执行一些检查：

您想为哪些名称激活 HTTPS？

```text
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

1: www.myexample.com

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

用逗号和/或空格分隔适当的数字，或留空输入以选择显示的所有选项（按 ‘c’ 取消）：1

获取新证书

正在执行以下挑战：

针对 www.myexample.com 的 http-01 挑战

等待验证...

正在清理挑战

在 `/etc/httpd/conf/httpd-le-ssl.conf` 创建了 SSL 虚拟主机

将证书部署到虚拟主机 `/etc/httpd/conf/httpd-le-ssl.conf`

通过向根配置中添加 Include 来启用站点 `/etc/httpd/conf/httpd-le-ssl.conf`
```

`Certbot` 还会在 `/etc/httpd/conf/` 目录下创建一个名为 `httpd-le-ssl.conf` 的新文件，其中包含每个已生成证书的域名的安全虚拟主机条目。这些条目将类似于：

```apache
<IfModule mod_ssl.c>

<VirtualHost *:443>
    ServerAdmin feedback@myexample.com
    ServerName www.myexample.com
    DocumentRoot /var/www/myexample
    ErrorLog logs/myexample_error_log
    CustomLog logs/myexample_access_log combined
SSLCertificateFile /etc/letsencrypt/live/www.myexample.com/fullchain.pem
SSLCertificateKeyFile /etc/letsencrypt/live/www.myexample.com/privkey.pem
Include /etc/letsencrypt/options-ssl-apache.conf
</VirtualHost>
</IfModule>
```

最后，`Certbot` 将询问服务器是否将未来的 HTTP Web 请求重定向到 HTTPS。换句话说，如果用户尝试访问 `http://www.myexample.com`，Web 服务器将用户重定向到 `https://www.myexample.com`：

请选择是否将 HTTP 流量重定向到 HTTPS 以移除 HTTP 访问。

```text
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

1: 不重定向 - 不对 Web 服务器配置进行进一步更改。

2: 重定向 - 将所有请求重定向到安全的 HTTPS 访问。对于新站点或如果您确定您的站点在 HTTPS 上运行良好，请选择此项。您可以通过编辑 Web 服务器的配置来撤销此更改。

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

选择适当的数字 [1-2] 然后按 [enter]（按 ‘c’ 取消）：2
```

如果您正在测试 HTTPS 配置并希望稍后保留 HTTP 版本，请选择“不重定向”选项。否则，通常建议重定向到 HTTPS。

证书安装后，请在浏览器中访问以下 URL 进行测试（将 `myexample.com` 替换为您自己的域名）：

[www.ssllabs.com/ssltest/analyze.html?d=www.myexample.com](https://www.ssllabs.com/ssltest/analyze.html?d=www.myexample.com)

如果证书配置成功，SSL Labs 将提供高评分，如图图 29-2 所示：

![SSL Labs 报告](img/rhel_8_ssl_labs_report.png)

图 29-2

作为最后的测试，打开浏览器窗口并使用 `https://` 前缀导航到域名。页面应像以前一样加载，浏览器应指示浏览器与服务器之间的连接是安全的（通常由地址栏中的锁图标指示，点击它可以查看更多信息）：

![SSL Labs](img/rhel_8_ssl_labs.png)

图 29-3

## 29.11 总结

网站的证书必须从证书颁发机构获取。有多种价格范围的选择供选择。然而，到目前为止最好的选项是从以下 URL 从 Let’s Encrypt 获取免费证书：

[letsencrypt.org](https://letsencrypt.org/)

从 Let’s Encrypt 获取证书涉及安装和运行 `Certbot` 工具。该工具将扫描服务器上的 Apache 配置文件，并提供为系统上配置的任何虚拟主机生成证书的选项。随后，它将生成证书并为相应的网站在 Apache 配置文件中添加虚拟主机条目。

按照 Let’s Encrypt 网站上的步骤在您的 RHEL 9 系统上下载并安装 `Certbot`，然后按照如下方式运行 `certbot` 工具来生成并安装证书：

```bash
certbot --apache
```

在请求电子邮箱地址并寻求接受服务条款后，`certbot` 将列出在 `httpd.conf` 文件中找到域名，并允许选择一个或多个需要安装证书的站点。`Certbot` 然后在获取并将证书安装到系统之前将执行一些检查：

假设模块已安装，下一步是为网站生成 SSL 证书。

## 30.1 邮件系统结构

多个组件构成了一个完整的邮件系统。以下是对每个组件的简要描述：

### 30.1.1 邮件代理

典型用户可能最熟悉系统的这部分。邮件代理（MUA），或邮件客户端，是用于编写、发送和读取邮件的应用程序。任何在计算机上编写和发送过邮件的人都使用过某种类型的邮件代理。

Linux 上典型的 MUA 有 `Evolution`、`Thunderbird` 和 `KMail`。对于那些偏好文本邮件客户端的用户，还有传统的 `Pine`。

### 30.1.2 邮件传输代理

邮件传输代理（MTA）是邮件系统中负责将邮件从一台计算机传输到另一台计算机的部分（无论是局域网内还是通过互联网到远程系统）。一旦配置正确，大多数用户只会直接与他们选择的 `MTA` 交互。Linux 许多许多 MTA 选择，包括 `Sendmail`、`Postfix`、`Fetchmail`、`Qmail` 和 `Exim`。

### 30.1.3 邮件投递代理

另一个对用户隐藏的部分，邮件投递代理（MDA）在后台运行，并在邮件传输代理和邮件客户端（MUA）之间执行邮件过滤。最常见的 MDA 形式是垃圾邮件过滤器，在邮件到达用户收件箱之前从系统中移除所有不需要的邮件。流行的 MDA 有 `Spamassassin` 和 `Procmail`。需要注意的是，某些邮件代理应用程序（如 `Evolution`、`Thunderbird` 和 `KMail`）内置了 `MDA` 过滤功能。

### 30.1.4 SMTP

SMTP 是 `Simple Mail Transport Protocol`（简单邮件传输协议）的缩写。邮件系统使用该协议将邮件从一个服务器传输到另一个服务器。该协议是 `MTAs` 用于相互通信和往返传输消息的语言。

### 30.1.5 SMTP 中继（SMTP Relay）

SMTP 中继是一种允许外部 SMTP 服务器发送邮件而不是托管本地 SMTP 服务器的协议。这通常涉及使用如 `Mailjet`、`SendGrid` 或 `MailGun` 等服务。这些服务避免了配置和维护自己的 SMTP 服务器，并且通常还能提供分析等额外优势。

## 30.2 配置 RHEL 9 邮件服务器

许多系统使用 `Sendmail` MTA 来传输邮件消息；在许多 Linux 发行版中，它是默认的 `Mail Transfer Agent`（邮件传输代理）。遗憾的是，`Sendmail` 是一个复杂的系统，对于初学者和经验丰富的用户都可能难以理解和配置。它也逐渐失去流行，因为它被认为处理邮件消息的速度比许多较新的可用 `MTAs` 都要慢。

许多系统管理员现在使用 `Postfix` 或 `Qmail` 来处理邮件。两者都比 `Sendmail` 更快且更容易配置。

因此，在本章中我们将 `Postfix` 作为一种 MTA，因为它的简单性和流行。然而，如果你倾向于使用 `Sendmail`，有很多专门研究该主题的书籍，它们对该主题的讲解将比本章要深入得多。

作为第一步，本章将介绍如何配置 RHEL 9 系统作为一个完整的邮件服务器运行。在本章的后后部分，还将介绍使用 SMTP 中继服务的步骤。

## 30.3 Postfix 安装前的步骤

在安装 `Postfix` 之前的第一步是确保系统中已经没有在运行 `Sendmail`。你可以使用以下命令进行检查：

```bash
systemctl status sendmail
```

如果未安装 `sendmail`，该工具将显示一条类似下所示的消息：

```text
Unit sendmail.service could not be found.
```

如果 `sendmail` 运行在你的系统上，则在安装和配置 `Postfix` 之前有必要停止它。要停止 `sendmail`，请运行以下命令：

```bash
systemctl stop sendmail
```

下一步是确保在系统重启时 `sendmail` 不会自动重启：

```bash
systemctl disable sendmail
```

`Sendmail` 现在已关闭并配置为在系统启动时不自动启动。可选情况下，要彻底从系统中删除 `sendmail`，请运行以下命令：

```bash
dnf remove sendmail
```

## 30.4 防火墙/路由器配置

由于发送和接收邮件消息涉及网络连接，必须配置防火墙以允许 SMTP 流量。如果 `firewalld` 已激活，请如下所示使用 `firewall-cmd` 工具：

```bash
firewall-cmd --permanent --add-service=smtp
```

配置服务器与互联网之间的任何其他防火墙或路由器以允许端口 25、143 和 587 的连接也是必要的，并在将这些端口转发到邮件服务器上相应的端口。

完成这些初始步骤后，我们现在可以安装 `Postfix`。

## 30.5 在 RHEL 9 上安装 Postfix

默认情况下，RHEL 9 的安装过程会在大多数配置中安装 `postfix`。要验证 `postfix` 是否已安装，请使用以下 `rpm` 命令：

```bash
rpm -q postfix
```

如果 `rpm` 报告 `postfix` 未安装，则可以通过以下方式安装：

```bash
dnf install postfix
```

`dnf` 工具将下载并安装 `postfix`，并在 `/etc/passwd` 文件中配置一个特殊的 `postfix` 用户。

## 30.6 配置 Postfix



`postfix` 的主要配置设置位于 `/etc/postfix/main.cf` 文件中。互联网上的许多资源提供了关于 `postfix` 的详细信息，因此本节将侧重于让邮件运行所需的基础选项。尽管 `dnf` 安装设置了一些基础配置选项，但它倾向于漏掉某些设置并对其他设置进行错误的猜测，因此请仔细检查 `main.cf` 文件。

`main.cf` 文件中的关键选项如下：

```
myhostname = mta1.domain.com
mydomain = domain.com
myorigin = $mydomain
mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain
inet_interfaces = $myhostname
mynetworks = subnet
```

其他设置要么已经由安装过程为你设置好，要么只有在你感到冒险并想要配置一个更复杂的邮件系统时才需要。

`myhostname` 的格式为 `host.domain.com`。例如，如果你的系统名为 `Host` 且域名为 `Domain.com`，你会将 `myhostname` 设置为：

```
myhostname = host.domain.com
```

`mydomain` 设置只是上述的域名部分。例如：

```
mydomain = domain.com
```

`myorigin` 设置定义了邮件在到达收件人收件箱时看起来源自的域名名称，它应该设置为你的域名：

```
myorigin = $mydomain
```

最关键的参数之一 `mydestination` 与此服务器作为最终终点的域名有关。任何不在此列表中的入邮件都将导致投递失败：

```
mydestination = $myhostname
```

`inet_interfaces` 设置定义了允许允许 `postfix` 接收邮件的系统网络接口，通常设置为 `all`：

```
inet_interfaces = all
```

`mynetworks` 设置定义了哪些外部系统被信任可以使用该服务器作为中继。此设置的可能值如下：

- `host`：仅信任本地系统。拒绝所有外部客户端将服务器作为中继的尝试。
- `subnet`：只有同一网络上的系统可以使用服务器作为中继。例如，如果服务器的 IP 地址为 `192.168.1.29`，则 IP 地址为 `192.168.1.30` 的客户端系统可以使用服务器作为中继。
- `class`：同一地址类（A、B、C 类）内的任何系统都可以使用服务器作为中继。

可以通过手动指定子网、地址范围或引用模式文件来手动定义信任的 IP 地址。以下示例将本地主机和子网 `192.168.0.0/24` 声明为信任 IP 地址：

```
mynetworks = 192.168.0.0/24, 127.0.0.0/8
```

对于此示例，将属性设置为 `subnet`，以便局域网上的任何其他系统都可以服务器作为中继。相比之下，外部系统被禁止这样做：

```
mynetworks = subnet
```

## 30.7 配置 DNS MX 记录

当你向注册商注册并配置域名时，DNS 设置中已经配置了一些默认值。其中之一就是所谓的邮件交换器（MX）记录。该记录定义了发往域名的邮件应该发送到哪里，它通常被设置为注册商提供的邮件服务器。如果你在托管自己的邮件服务器，`MX` 记录应设置为你的域名或邮件服务器的 IP 地址。进行此更改的步骤取决于域名注册商，但通常涉及编辑域名的 DNS 信息并添加或编辑 `MX` 记录以指向你的邮件服务器。

## 30.8 在 RHEL 9 系统上启动 Postfix

一旦 `/etc/postfix/main.cf` 文件配置了正确的设置，现在是启动 `postfix` 的时候了。可以通过以下命令行实现：

```
# systemctl start postfix
```

如果 `postfix` 已经在运行，请使用以下命令加载配置更改：

```
# systemctl reload postfix
```

要配置 `postfix` 在系统启动时自动启动，请运行以下命令：

```
# systemctl enable postfix
```

Postfix 进程现在应该启动了。验证一切工作正常的最佳方法是检查你的邮件日志。该日志通常位于 `/var/log/maillog` 文件中，现在应该包含一条类似于下面输出的条目：

```
Mar 25 11:21:48 demo-server postfix/postfix-script[5377]: starting the Postfix mail system
Mar 25 11:21:48 demo-server postfix/master[5379]: daemon started -- version 3.3.1, configuration /etc/postfix
```

只要日志中没有记录错误信息，你就已成功安装并启动了 postfix，并准备好测试 postfix 配置。

## 30.9 测试 Postfix

测试 postfix 配置的一种简单方法是在系统上的本地用户之间发送电子邮件。要进行快速测试，请按照如下方式使用 `mail` 工具（其中将 `name` 和 `mydomain` 分别替换为系统上的用户名和你的域名）：

```
# mail name@mydomain.com
```

在出现提示时，输入邮件的主题，然后输入邮件正文内容。要发送邮件，按 `Ctrl-D`。例如：

```
# mail demo@mydomain.com
Subject: Test email message
This is a test message.
EOT
```

再次运行 `mail` 命令，这次使用另一个用户身份，并验证邮件是否已发送和接收：

```
$ mail
Heirloom Mail version 12.5 7/5/10\. Type ? for help.
"/var/spool/mail/demo": 1 message 1 new
>N 1 root Mon Mar 25 13:36 18/625 "Test email message"
&
```

如果邮件没有出现，请检查日志文件（`/var/log/maillog`）是否存在错误。成功的邮件投递将将如下所示显示在日志文件中：

```
Mar 25 13:41:37 demo-server postfix/pickup[7153]: 94FAF61E8F4A: uid=0 from=<root>
Mar 25 13:41:37 demo-server postfix/cleanup[7498]: 94FAF61E8F4A: message-id=<20190325174137.94FAF61E8F4A@demo-server.mydomain.com>
Mar 25 13:41:37 demo-server postfix/qmgr[7154]: 94FAF61E8F4A: from=<root@mydomain.com>, size=450, nrcpt=1 (queue active)
Mar 25 13:41:37 demo-server postfix/local[7500]: 94FAF61E8F4A: to=<neil@mydomain.com>, relay=local, delay=0.12, delays=0.09/0.01/0/0.02, dsn=2.0.0, status=sent (delivered to mailbox)
Mar 25 13:41:37 demo-server postfix/qmgr[7154]: 94FAF61E8F4A: removed
```

一旦本地邮件功能正常，尝试向向外部地址（如 GMail 账户）发送邮件。此外，通过从外部账户向你域名上的用户发送邮件来测试接收邮件是否正常。在每情况下，请检查 `/var/log/maillog` 文件以获取任何错误的解释。

## 30.10 通过 SMTP 中继服务器发送邮件

SMTP 中继服务是配置邮件服务器来处理出站邮件的另一种替代方案。正如之前讨论的，有多种服务可用，其中大多数可以通过在网络上搜索“SMTP Relay Service”来找到。这些服务中的大多数将要求你以某种方式验证你的域名，并提供 MX 记录以更新你的 DNS 设置。你还将获得用户名和密码，这些信息必须添加到 postfix 配置中。本节的剩余部分假设你的系统中已安装了 postfix，并且已完成所选 SMTP 中继提供商要求的所有初始步骤。

从编辑 `/etc/postfix/main.cf` 文件开始，用你的域名配置 `myhostname` 参数：

```
myhostname = mydomain.com
```

接下来，在 `/etc/postfix` 中创建一个名为 `sasl_passwd` 的新文件，并添加包含中继服务提供的邮件服务器主机、用户名和密码的行。例如：

```
[smtp.myprovider.com]:587 neil@mydomain.com:mypassword
```

注意上述条目中指定了端口 `587`。如果没有此设置，postfix 将默认使用端口 `25`，而该端口被大多数 SMTP 中继服务提供商默认拦截。

创建密码文件后，使用 `postmap` 工具生成包含邮件凭据的哈希数据库：

```
# postmap /etc/postfix/sasl_passwd
```

在继续之前，采取额外步骤来保护你的 postfix 凭据：

```
# chown root:root /etc/postfix/sasl_passwd /etc/postfix/sasl_passwd.db
# chmod 0600 /etc/postfix/sasl_passwd /etc/postfix/sasl_passwd.db
```

再次编辑 `main.cf` 文件并添加条目以指定中继服务器：

```
relayhost = [smtp.myprovider.com]:587
```

在 `main.cf` 中继续添加内容以启用身份验证：

```
sasl_auth_maps = hash:/etc/postfix/sasl_passwd
sasl_password_maps = hash:/etc/postfix/sasl_passwd
sasl_security_mechanism = plain
```

启用 TLS（可选）：

```
smtp_tls_auth = yes
```

最后，重启 postfix 服务：

```
# systemctl restart postfix
```

一旦服务重启，尝试使用 `mail` 工具发送并接收邮件。

此时，我们可以在新驱动器上创建分区和文件系统，并将其挂载以进行访问，或者将磁盘作为物理卷作为卷组的一部分。要执行前者，请继续阅读本章；否则，请阅读“向 RHEL 9 卷组和逻辑卷添加新磁盘”了解配置逻辑卷的详情。

## 31.3 创建 Linux 分区

下一步是在新磁盘驱动器上创建一个或多个 Linux 分区。这是通过使用 `fdisk` 工具实现的，它接受要分区的设备作为命令行参数：

```
# fdisk /dev/sdb
Welcome to fdisk (util-linux 2.37.4).
更改将仅保留在内存中，直到你决定写入它们。
在使用 write 命令之前请务必小心。
设备不包含识别的分区表。
已创建标识符为 0x64d68d00 的新 DOS 磁盘标签。
Command (m for help):
```

查看磁盘上的当前分区，输入 `p` 命令：

```
Command (m for help): p
Disk /dev/sdb: 14.46 GiB, 15525216256 bytes, 30322688 sectors
Disk model: USB 2.0 FD
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x64d68d00
```

从上面的 fdisk 输出中可以看出，磁盘目前没有分区，因为它之前未被使用。下一步是在磁盘上创建一个新分区，该任务通过输入 `n`（表示新分区）和 `p`（表示主分区）完成：

```
Command (m for help): n
Partition type
   p primary (0 primary, 0 extended, 4 free)
   e extended (container for logical partitions)
Select (default p): p
Partition number (1-4, default 1):
```

在本示例中，我们只计划创建一个分区，它将是分区 `1`。接下来，我们需要指定分区的起始和结束位置。由于这是第一个分区，我们需要它从第一个可用扇区开始，并且由于我们想使用整个磁盘，我们将最后一个扇区指定为结束。请注意，如果你想创建多个分区，可以通过扇区、字节、千字节或兆字节来指定每个分区的大小：

```
Partition number (1-4, default 1): 1
First sector (2048-30322687, default 2048):
Last sector, +/-sectors or +/-size{K,M,G,T,P} (2048-30322687, default 303226687):
Created a new partition 1 of type 'Linux' and of size 14.5 GiB.
Command (m for help):
```

现在我们已经指定了分区，需要使用 `w` 命令将其写入磁盘：

```
Command (m for help): w
The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.
```

如果现在再次查看设备，我们将看到新分区显示为 `/dev/sdb1`：

```
# ls /dev/sd*
/dev/sda /dev/sda1 /dev/sda2 /dev/sdb /dev/sdb1
```

下一步是在我们的新分区上创建文件系统。

## 31.4 在 RHEL 9 磁盘分区上创建文件系统

现在我们安装了一个新磁盘，它对 RHEL 9 可见，并且我们已经在磁盘上配置了一个 Linux 分区。下一步是在分区上创建一个 Linux 文件系统，以便操作系统可以使用它来存储文件和数据。在分区上创建文件系统的简单方法是使用 `mkfs.xfs` 工具：

```
# mkfs.xfs -f /dev/sdb1
meta-data=/dev/sdb1 isize=512 agcount=4, agsize=947520 blks
          = sectsz=512 attr=2, projid32bit=1
          = crc=1 finobt=1, sparse=1, rmapbt=0
          = reflink=1 bigtime=1 inobtcount=1
data = bsize=4096 blocks=3790080, imaxpct=25
          = sunit=0 swidth=0 blks
naming =version 2 bsize=4096 ascii-ci=0, ftype=1
log =internal log bsize=4096 blocks=2560, version=2
          = sectsz=512 sunit=0 blks, lazy-count=1
realtime =none extsz=4096 blocks=0, rtextents=0
```

在这种情况下，我们创建了一个 XFS 文件系统。XFS 是一种高性能文件系统，是 RHEL 9 的默认文件系统类型，在并行 I/O 性能和日志的使用方面具有若干优势。

## 31.5 日志文件系统概述

日志文件系统记录了在向文件系统写入期间所更改的日志，可以快速恢复由于系统崩溃或断电等事件导致的损坏。使用日志文件系统有几个优势。首先，存储在磁盘上的数据量呈指数级增长。非日志文件系统的问题是，在崩溃后必须运行 `fsck`（文件系统一致性检查）工具。`fsck` 工具将扫描整个文件系统，验证块是否正确分配和引用。问题有两个：首先，`fsck` 工具并不总是能够修复损坏，你会得到 `lost+found` 目录。应用程序可以使用这些数据，但系统知道它们在哪里。

## 31.6 挂载文件系统

现在我们在新分区上创建了文件系统，需要将其挂载以便访问和使用。为了做到这一点，我们需要创建一个挂载点。挂载点只是挂载文件系统的目录或文件夹。在本示例中，我们将创建一个 `/backup` 目录：

```
# mkdir /backup
```

然后可以使用 `mount` 命令手动挂载文件系统：

```
# mount /dev/sdb1 /backup
```

运行无参数的 `mount` 命令可以显示所有挂载的文件系统（包括我们的新文件系统）：

```
# mount
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime,seclabel)
/dev/sdb1 on /backup type xfs (rw,relatime,seclabel,attr2,inode64,logbufs=8,logbsize=32k,noquota)
```

## 31.7 配置 RHEL 9 自动挂载文件系统



为了设置系统启动时自动挂载新文件系统，需要在`/etc/fstab`文件中添加条目。`fstab`条目的格式如下：

`<device> <dir> <type> <options> <dump> <fsck>`

这些条目总结如下：

- `<device>`：文件系统的设备。
- `<dir>`：作为文件系统挂载点的目录。
- `<type>`：文件系统类型（`xfs`、`ext4`等）。
- `<options>`：额外的文件系统挂载选项，例如将文件系统设置为只读或控制任何用户都可以挂载该文件系统。运行`man mount`查看完整的选项列表。将此值设置为默认值将使用文件系统的默认设置（`rw`、`suid`、`dev`、`exec`、`auto`、`nouser`、`async`）。
- `<dump>`：决定在执行`dump`工具执行的备份时，是否包含文件系统的内容。此设置很少使用，可以使用`0`值禁用。
- `<fsck>`：在系统崩溃后是否由`fsck`对文件系统进行检查，以及检查文件系统的顺序。对于如`XFS`等带日志的文件系统，应将其设置为`0`，以表示不需要检查。

以下示例显示了配置的`fstab`文件，用于自动挂载位于`/dev/sdb1`分区上的`/backup`分区：

```
/dev/mapper/rhel-root / xfs defaults 0 0
UUID=b4fc85a1-0b25-4d64-8100-d50ea23340f7 /boot xfs defaults 0 0
/dev/mapper/rhel-home /home xfs defaults 0 0
/dev/mapper/rhel-swap swap swap defaults 0 0
/dev/sdb1 /backup xfs defaults 0 0
```

现在，`/backup`文件系统将在每次系统重启时自动挂载。

## 31.8 使用 Cockpit 添加磁盘

除了使用本章概述的命令行工具进行存储操作外，还可以使用`Cockpit` Web控制台配置新的存储设备。要查看当前的存储配置，请登录`Cockpit`控制台并选择如图31-1所示的`Storage`选项：

![](img/cockpit_storage.png)

图31-1

要找到新添加的存储，请滚动到`Storage`页面的底部，直到`Drives`部分进入视野（注意，`Drives`部分也可能位于屏幕的右上角）：

![](img/cockpit_drives.png)

图31-2

在上述图中，新硬盘是15.5 GB的硬盘。选择新硬盘以显示如图31-3所示的`Drive`屏幕：

![](img/cockpit_drive_details.png)

图31-3

点击`Create partition`按钮并使用对话框指定分配给此分区的空间、文件系统类型（推荐使用`XFS`）以及可选的标签、文件系统挂载点和挂载选项。注意，如果此新分区没有使用所有可用空间，可以在硬盘上添加额外的分区。要更改设置（例如文件系统是否为只读或是否在启动时挂载），请在`Mount options`部分中更改设置：

![](img/cockpit_drive_create_partition.png)

图31-4

一旦选好设置，点击`Create partition`按钮提交更改。创建过程完成后，新分区将被添加到磁盘中，创建相应的文件系统并挂载到指定的挂载点，同时对`/etc/fstab`文件进行相应的更改。

## 31.9 总结

本章涵盖了如何向现有的RHEL 9系统添加物理或虚拟磁盘驱动器。这是一个相对简单的过程，即确保操作系统检测到新硬盘、在硬盘上创建一个或多个分区，然后在这些分区上创建文件系统。虽然RHEL 9提供了多种文件系统类型，但通常推荐使用`XFS`。一旦文件系统准备就绪，就可以使用`mount`命令进行挂载。为了让新创建的文件系统在系统启动时自动挂载，可以在`/etc/fstab`配置文件中进行添加。

# 32 为 RHEL 9 逻辑卷组和逻辑卷添加新磁盘

在上一章中，我们查看了向RHEL 9系统添加新磁盘驱动器、创建分区和文件系统，然后挂载该文件系统以访问磁盘。创建固定分区和文件系统的替代方案是使用`逻辑卷管理 (LVM)`创建由一个或多个物理或虚拟磁盘（或分区）的空间组合成的逻辑磁盘。使用`LVM`的优势是，可以在逻辑卷中添加或删除空间，而无需将数据分布在多个文件系统上。

让我们以基于RHEL 9的服务器根（`/home`）文件系统为例。如果没有`LVM`，该文件系统会在安装操作系统时以特定大小创建。如果安装了新的磁盘驱动器，则无法将该任何空间分配给`/home`文件系统。唯一的选项是在新磁盘上创建新的文件系统并将其挂载到特定的挂载点。在这种情况下，虽然新文件系统上有充足的空间，但`/home`文件系统仍然几乎满额。唯一的选择是将文件移动到新文件系统。有了`LVM`，新硬盘（或其部分）可以分配包含根文件系统的逻辑卷，从而动态扩展可用空间。

在本章中，我们将介绍向卷组和逻辑卷添加新磁盘空间所需的步骤，以便为RHEL 9系统的根文件系统添加额外空间。

## 32.1 逻辑卷管理 (LVM) 概述

`LVM`提供了一种灵活且高级的磁盘空间管理方法。与其将每个磁盘驱动器划分为固定大小的分区并在创建固定大小的文件系统，`LVM`提供了一种将磁盘空间分组逻辑卷的方法，这些逻辑卷可以轻松调整大小。此外，`LVM`允许通过分配不同的卷组或逻辑卷来精确控制分配给用户的空间。当分配给卷的空间耗尽时，管理员可以添加更多空间。

`LVM`由以下组件组成：

- **32.1.1 卷组 (VG)**：`卷组`是一个或多个逻辑卷和物理卷的高级容器。
- **32.1.2 物理卷 (PV)**：`物理卷`代表存储设备，如磁盘驱动器。
- **32.1.3 逻辑卷 (LV)**：`逻辑卷`等同于分区，与分区一样，它可以包含文件系统。
- **32.1.4 物理区 (PE)**：每个`物理卷`（`PV`）被划分为称为物理区的等大小块。
- **32.1.5 逻辑区 (LE)**：每个`逻辑卷`（`LV`）被划分为称为逻辑区的等大小块。

假设我们要创建一个名为`VolGroup01`的新卷组。该卷组需要物理磁盘空间才能运行，因此我们分配三个分区`/dev/sda1`、`/dev/sdb1`和`/dev/sdb2`。然后，我们会在卷组内创建一个名为`LogVol01`的逻辑卷。如果`LogVol01`空间不足，我们将更多磁盘分区作为物理卷并将其分配给卷组和逻辑卷。

## 32.2 获取逻辑卷信息

作为在RHEL 9中使用`LVM`的示例，我们将为标准RHEL 9安装的`/`文件系统添加空间。考虑到根分区大小的灵活性，RHEL 9将`/`文件系统设置为名为`rhel`的卷组内的逻辑卷（名为`root`）。但在对`LVM`设置进行任何更改之前，首先收集信息是关重要的。

运行`mount`命令将输出有关挂载点的信息，对应的如下：

```
dev/mapper/rhel-root on / type xfs (rw,relatime,seclabel,attr2,inode64,logbufs=8,logbsize=32k,noquota)
```

可以使用`vgdisplay`命令获取卷组信息：

```
vgdisplay

--- Volume group ---
  VG Name rhel
  System ID
  Format lvm2
  Metadata Areas 1
  Metadata Sequence No 4
  VG Access read/write
  VG Status resizable
  MAX LV 0
  Cur LV 3
  Open LV 3
  Max PV 0
  Cur PV 1
  Act PV 1
  VG Size <297.09 GiB
  PE Size 4.00 MiB
  Total PE 76054
  Alloc PE / Size 76054 / <297.09 GiB
  Free PE / Size 0 / 0
  VG UUID 8vZKNE-v6nY-uII2-NKk1-StmF-EkNp-NNKa9b
```

如上面的示例所示，`rhel`卷组的物理区大小为4.00 MiB，总共有297.09 GB可用空间分配给逻辑卷。当前，已分配了76054个物理区，等于总容量。因此，我们必须添加一个或多个物理卷来增加分配给`rhel`卷组中任何逻辑卷的空间。`vgs`工具也有助于快速查看系统中卷组可用空间的概述：

### vgs

```
  VG #PV #LV #SN Attr VSize VFree
  rhel 1 0 wz-- <297.09g
```

同样，可以使用`lvdisplay`命令获取卷组中逻辑卷的信息：

### lvdisplay

```
  --- Logical volume ---

  LV Path /dev/rhel/swap
  LV Name swap
  VG Name rhel
  LV UUID Rck8-T5Or-vZ9-Er1e-qW7-f9cpj
  LV Write Access read/write
  LV Creation host, time demoserver, 2023-04-10 14:11:15 -0400
  LV Status available
  # open 2
  LV Size 3.75 GiB
  Current LE 960
  Segments 1
  Allocation inherit
  Read ahead auto
  - currently set to 256
  Block device 253:1
  --- Logical volume ---

  LV Path /dev/rhel/home
  LV Name home
  VG Name rhel
  LV UUID MMpQ05-ry0-9g-zvGQ-Dszn-kd-ZpaK6
  LV Write Access read/write
  LV Creation host, time demoserver, 2023-04-10 14:11:15 -0400
  LV Status available
  # open 1
  LV Size <223.34 GiB
  Current LE 57174
  Segments 1
  Allocation inherit
  Read ahead auto
  - currently set to 256
  Block device 253:2
  --- Logical volume ---

  LV Path /dev/rhel/root
  LV Name root
  VG Name rhel
  LV UUID OFqAB0-azjy-47DO-bzRo-ha2O-sHz5-jjcF
  LV Write Access read/write
  LV Creation host, time demoserver, 2023-04-10 14:11:17 -0400
  LV Status available
  # open 1
  LV Size 70.00 GiB
  Current LE 17920
  Segments 1
  Allocation inherit
  Read ahead auto
  - currently set to 256
  Block device 253:0
```

如上所示，卷组`rhel`中的70 GiB空间分配给了逻辑卷`root`（`/`系统），大约223.34 GiB分配给了`home`卷组（`/home`），以及3.75 GiB分配给了`swap`（交换空间）。现在我们知道了哪些空间被使用了，但了解哪些设备提供了空间（换句话说，哪些设备被用作物理卷）通常很有帮助。要获取此信息，需要运行`pvdisplay`命令：

### pvdisplay

```
  --- Physical volume ---

  PV Name /dev/sda2
  VG Name rhel
  PV Size 297.09 GiB / usable 4.00 MiB
  Allocatable yes (but full)
  PE Size 4.00 MiB
  Total PE 76054
  Free PE 0
  Allocated PE 76054
  PV UUID siTC2-fq47-LXTG-VWtc-Ma33
```

显然，逻辑卷`rhel`控制的空间通过位于`/dev/sda2`的物理卷提供。现在我们知道了更多LVM配置，可以向卷组及其包含的逻辑卷添加空间。

## 从命令行向卷组添加额外空间

与之前获取RHEL 9当前逻辑卷配置信息的步骤相同，可以通过命令行进行此配置。在本章的剩余部分，我们将假设添加了一个新磁盘，操作系统将其识别为`/dev/sdb`。我们还假设这是一个没有现有分区的磁盘。如果存在现有分区，应对其进行备份，然后使用`fdisk`工具从磁盘上删除分区。例如，假设由`/dev/sdb`表示的设备包含两个分区：

```
# fdisk -l /dev/sdb
Disk /dev/sdb: 14.46 GiB, 1552516256 bytes, 3032688 sectors
Disk model: USB2.0
Units: sectors of 512 = 512 bytes
Sector size (logical/physical): 512 bytes
I/O size (minimum/optimal): 512 bytes
Disklabel: dos
Disk identifier: 0x4c3306b
Device Start End Sectors Type
/dev/sdb1 2048 3032687 14.5 Linux
```

一旦卸载了这些分区上的任何文件系统，即可删除它们：

```
# fdisk /dev/sdb
Welcome to fdisk (util-linux 2.37).
更改将仅留在内存中，直到你决定写入它们。
在使用写入命令前要小心。
Command (m for help): d
选择了分区 1
分区 1 已删除。
Command (m for help): w
分区表已更改。
正在调用 ioctl() 重新读取分区表。
正在同步磁盘。
```

在移动到下一步之前，删除`/etc/fstab`中这些文件系统的条目，以免系统在下次重启时尝试挂载它们。一旦磁盘准备就绪，下一步是使用`pvcreate`命令将磁盘转换为物理卷（如果存在dos签名）：

```
# pvcreate /dev/sdb
WARNING: dos signature detected on /dev/sdb at offset 510. Wipe it? [y/n]: y
正在擦除 /dev/sdb 上的 dos 签名。
物理卷 "/dev/sdb" 已创建。
```

如果创建失败并显示“`<device>`被过滤器排除”的消息，则可能需要在创建物理卷之前使用`wipefs`命令擦除磁盘：

```
# wipefs -a /dev/sdb
/dev/sdb: 8 bytes were erased at offset 0x0000200 (gpt): 45 46 29 20 50 41 54
/dev/sdb: 8 bytes were erased at offset 0x1ffff00 (gpt): 45 46 29 20 50 41 54
/dev/sdb: 2 bytes were erased at offset 0x00001fe (PMBR): 55 aa
/dev/sdb: calling ioctl() to re-read partition table: Success
```

创建物理卷后，我们现在需要使用`vgextend`命令将其添加到卷组（在本例中为`rhel`）：

```
# vgextend rhel /dev/sdb
卷组 "rhel" 已成功扩展
```

现在新物理卷已添加到卷组，并准备好分配给逻辑卷。执行此操作，我们运行`lvextend`工具并提供我们想要扩展卷的大小。在本例中，我们想要扩展`home`卷的大小14 GB。注意，我们需要提供逻辑卷的路径，可以通过`lvdisplay`命令获取（在本例中`/dev/rhel/home`）：

```
# lvextend -L+14G /dev/rhel/home
Size of logical volume rhel/home changed from <223.34 GiB (57174 extents) to <237.34 GiB (60758 extents).
逻辑卷 rhel/home 已成功调整大小。
```

最后一步是调整逻辑卷上的文件系统以使用额外的空间。执行方式取决于文件系统类型，可以通过以下`df`命令识别类型列：

```
# df -T /home
Filesystem Type 1K-blocks Available Use% Mounted on
/dev/mapper/rhel-home xfs 234070356 1669596 232400760 1% /home
```

如果`/home`使用XFS文件系统格式化，可以使用`xfs_growfs`工具对其进行调整大小：



```bash
# xfs_growfs /home
meta-data=/dev/mapper/rhel-home isize=512 agcount=4 agsize=14636544 blks
       = sectsz=512 attr=2, projid32bit=1
       = crc=1 finobt=1 sparse=1, rmapbt=0
       = relink=1 bigtime=1 inobtcount=1
data = bsize=4096 blocks=58546176, imaxpct=25
       = sunit=0 swidth=0 blks
naming =version 2 bsize=4096 ascii-ci=0, ftype=1
log =internal log bsize=4096 blocks=28587, version=2
       = sectsz=512 sunit=0 blks, lazy-count=1
realtime =none extsz=4096 blocks=0, rtextents=0
atatdata blocks changed from 58546176 to 62216192
```

除了本章为止概述的命令行工具外，还可以通过 Cockpit Web 界面中的“存储”（Storage）页面访问逻辑卷信息，并对卷组和逻辑卷进行更改，如图 32-1 所示：

![](img/cockpit_storage1.png)

图 32-1

如果没有列出“存储”选项，则需要安装 `cockpit-storaged` 包并按照如下方式重启 cockpit 服务：

```bash
dnf install cockpit-storaged
# systemctl restart cockpit.socket
```

一旦 Cockpit 服务重启，请重新登录 Cockpit 界面，此时“存储”选项应该是可见的。

若要从 Cockpit 控制台中向现有卷组添加新磁盘驱动器，请从上述“存储”页面开始，在上方标记为 A 的列表中点击与要扩展的卷组关联的文件系统。

在生成的屏幕上，点击下方图 32-2 所示的高亮显示的 `+` 按钮以添加物理卷：

![](img/cockpit_storage_add_physical_volume.png)

图 32-2

选择要添加到卷组的新驱动器，并点击 `Add`（添加）按钮：

![](img/cockpit_storage_physical_volume_selected.png)

图 32-3

返回卷组屏幕后，滚动到要扩展的逻辑卷并点击它以展开更多信息。例如，图 32-4 显示了 home 逻辑卷的详情：

![](img/cockpit_home_logical_volume.png)

图 32-4

要使用新空间扩展逻辑卷，点击 `Grow`（扩展）按钮，并使用生成的对话框中的滑块来选择应向卷添加多少空间。然后，点击 `Grow` 按钮提交更改（如果需要，可用空间可以在不同的卷组之间共享）：

![](img/cockpit_home_logical_volume_grow.png)

图 32-5

一旦完成这些步骤后，卷组将配置为使用新添加的空间。

## 32.5 总结

卷组和逻辑卷在 RHEL 9 系统的物理存储设备之上提供了一个抽象层，为分配多个磁盘驱动器提供的空间提供灵活的方法。这允许动态地进行和更改磁盘空间分配，无需重新划分磁盘驱动器并在文件系统之间移动数据。本章概述了卷组以及逻辑卷和物理卷的基本概念，并演示了如何使用命令行工具和 Cockpit Web 界面管理这些内容。

# 33 添加和管理 RHEL 9 交换空间（Swap Space）

维护 RHEL 9 系统性能的一个重要部分是确保有足够的交换空间，以与系统对内存的需求相匹配。因此，本章提供了 RHEL 9 上交换空间管理的概述。

## 33.1 什么是交换空间？

计算机系统为操作系统提供的可用物理内存数量是有限的。当操作系统接近可用内存限制时，它会通过将内存页写入磁盘来释放空间。当操作系统需要其中任何一个页时，它们会被读回内存。为此任务分配的磁盘区域称为称为交换空间（swap space）。

## 33.2 RHEL 9 建议的交换空间

RHEL 9 建议的交换空间取决于多个因素，包括系统中的内存量、施在内存上的工作负载，以及系统是否需要支持休眠。RHEL 9 交换空间的当前指南如下：

| 已安装 RAM 的数量 | 建议的交换空间 | 启用休眠时的建议交换空间 |
| :--- | :--- | :--- |
| 2GB 或更少 | 已安装 RAM x 2 | 已安装 RAM x 3 |
| 2GB - 8GB | 已安装 RAM x 1 | 已安装 RAM x 2 |
| 8GB - 64GB | 至少 4GB | 已安装 RAM x 1.5 |
| 64GB 或更多 | 至少 4GB | 不建议休眠 |

表 33-1

当系统进入休眠时，当前系统状态写入硬盘，主机关闭。当机器随后开机时，系统状态将从硬盘中恢复。这与挂起（suspension）不同，挂起时系统状态存储在 RAM 中。机器随后进入睡眠状态，此时系统 RAM 保持供电，而其他设备被关闭。

## 33.3 识别当前交换空间的使用情况

RHEL 9 系统当前使用的交换空间量可以通过多种方式识别。一种方法是输出 `/proc/swaps` 文件：

```bash
cat /proc/swaps
```

```text
Filename Type Size Used Priority

/dev/dm-1 partition 3932156 0 -2
```

或者，可以使用 `swapon` 命令：

```bash
swapon
```

```text
NAME TYPE SIZE USED PRIO

/dev/dm-1 partition 3.7G 0B -2
```

要查看交换空间相对于总可用 RAM 的量，可以使用 `free` 命令：

```bash
free
```

```text
              total used free shared buff/cache available
Mem: 3601420 1577696 1396172 404412 1273236 2023724
Swap: 3932156
```

## 33.4 为 RHEL 9 添加交换文件

向 RHEL 9 添加交换空间的一种方法是创建一个文件并将其分配为交换空间。首先输出 `/proc/swaps` 文件：

```bash
cat /proc/swaps
```

```text
Filename Type Size Used Priority
/dev/dm-1 partition 3932156 0 -2
```

或者，可以使用 `swapon` 命令：

```bash
swapon
```

```text
NAME TYPE SIZE USED PRIO
/dev/dm-1 partition 3.7G 0B -2
```

要查看交换空间相对于总可用 RAM 的量，可以使用 `free` 命令：

```bash
free
```

```text
              total used free shared buff/cache available

Mem: 3601420 1577696 1396172 404412 1273236 2023724

Swap: 3932156
```

## 33.5 作为分区添加交换空间

作为指定文件作为交换的替代方案，整个分区也可以被指定为交换空间。实现此目的步骤与添加交换文件相同。在将分区分配给交换之前，请确保相应文件系统上的现有数据已备份或不再需要，并且该文件系统已卸载。

假设磁盘驱动器上存在由 `/dev/sdb1` 表示的分区，例如，第一步将使用 `mkswap` 工具将其转换为交换空间：

```bash
mkswap /dev/sdb1
```

接下来，将新分区添加到系统交换中并验证其确实已添加：

```bash
swapon /dev/sdb1
```

```bash
swapon
```

```text
NAME TYPE SIZE USED PRIO
/dev/dm-1 partition 3.7G 996K -2
/dev/sdb1 partition 14.5G 0B -3
```

再次，可以修改 `/etc/fstab` 文件以便在启动时自动添加交换分区，如下：

```text
/dev/sdb1 swap swap defaults 0 0
```

## 33.6 为 RHEL 9 LVM 交换卷添加空间

对于使用逻辑卷管理（LVM）的系统，除了通过文件或分区添加交换外，另一种方法是扩展用于交换空间的逻辑卷。

第一步是使用 `lvdisplay` 工具识别当前可用的交换空间（swap）以及用于交换空间的卷组（volume group）和逻辑卷（logical volume）。有关 LVM 的更多信息，请参阅标题为向 RHEL 9 卷组和逻辑卷中添加新磁盘的章节：

### `lvdisplay`

```text
  --- Logical volume ---

  LV Path /dev/rhel/swap00
  LV Name swap00
  VG Name rhel
  LV UUID EbOScj-1qXw-bB9d-LU61-ZjdC-L7u5-Uhj8De
  LV Write Access read/write
  LV Creation host, time demoserver, 2023-04-12 09:34:29 -0400
  LV Status available
  # open 2
  LV Size 3.75 GiB
  Current LE 960
  Segments 1
  Allocation inherit
  Read ahead sectors auto
  - currently set to 256
  Block device 253:1
```

很明显，交换空间位于名为 `swap00` 的逻辑卷上，该卷是名为 `rhel` 的卷组的一部分。下一步是验证卷组中是否有可用空间可以分配给交换卷：

### `vgs`

```text
  VG #PV #LV #SN Attr VSize VFree
  rhel 2 3 0 wz--n- 197.66g <22.00g
```

如果可用空间足以满足额外的交换需求，请关闭交换并扩展交换逻辑卷，以尽可能使用所需的可用空间来满足系统的交换需求：

```bash
swapoff /dev/rhel/swap
lvextend -L+8GB /dev/rhel/swap
```

`Logical volume rhel/swap successfully resized.`

接下来，重新格式化交换卷并重新开启：

```text
mkswap /dev/rhel/swap
mkswap: /dev/rhel/swap: warning: wiping old swap signature.
Setting up swapspace version 1, size = 12 GiB (12754874368 bytes)
no label, UUID=241a4818-e51c-4b8c-9bc9-1697fc2ce26e
swapon /dev/rhel/swap
```

完成更改后，检查交换空间是否已经增加：

```text
swapon
NAME TYPE SIZE USED PRIO
/dev/dm-1 partition 12G 0B -2
```

# 33. 向卷组中添加交换空间

在上面的节中，我们扩展了交换逻辑卷以使用卷组中已有的空间。如果卷组中没有可用空间，则在扩展交换之前必须添加空间。

从检查卷组的状态开始：

```text
vgs
  VG #PV #LV #SN Attr VSize VFree
  rhel 1 3 0 wz--n- <297.09g 0
```

上述输出表明卷组内没有可用空间。然而，假设我们有为系统交换添加 14 GB 空间的需求。这需要向卷组添加更多空间。在本示例中，假设有一个大小为 16 GB 且由 `/dev/sdb` 表示的磁盘可添加到卷组。因此，第一步是使用 `pvcreate` 将此分区转换为物理卷（physical volume）：

```text
pvcreate /dev/sdb
  Physical volume "/dev/sdb" successfully created.
```

如果创建失败并显示类似“Device /dev/sdb excluded by a filter”get 信息，则可能必要在创建物理卷之前先擦除磁盘：

```text
wipefs -a /dev/sdb
/dev/sdb: 8 bytes were erased at offset 0x00000200 (gpt): 45 46 49 20 50 41 52 54
/dev/sdb: 8 bytes were erased at offset 0x1fffffe00 (gpt): 45 46 49 20 50 41 52 54
/dev/sdb: 2 bytes were erased at offset 0x000001fe (PMBR): 55 aa
/dev/sdb: calling ioctl to re-read partition table: Success
```

接下来，需要扩展卷组以使用此额外的物理卷：

```text
vgextend rhel /dev/sdb
  Volume group "rhel" successfully extended
```

此时，`vgs` 命令应该报告来自 `/dev/sdb` 的空间已添加到卷组：

```text
vgs
  VG #PV #LV #SN Attr VSize VFree
  rhel 2 3 0 wz--n- 311.54g <14.46g
```

现在卷组中已有了可用空间，可以扩展交换逻辑卷来利用这些空间。但在之前，先关闭交换：

```bash
swapoff /dev/rhel/swap
```

接下来，扩展逻辑卷：

```bash
lvextend -L+8GB /dev/rhel/swap
```

`Logical volume rhel/swap successfully resized.`

## 34 监控 RHEL 9 进程

要列出系统上运行的所有进程（包括所有用户和系统进程），请执行以下命令：

```bash
$ ps -ax

PID TTY STAT TIME COMMAND
  1 ? Ss 0:22 /usr/lib/systemd/systemd rhgb --switched-root
  2 ? S 0:00 [kthreadd]
  3 ? I< 0:00 [rcu_gp]
  4 ? I< 0:00 [rcu_par_gp]
  5 ? I< 0:00 [netns]
```

要列出所有进程并包含所有者、CPU 和内存使用信息，请使用 `-aux` 参数执行 `ps` 命令：

```bash
$ ps -aux

USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND
root 2 0.0 0.0 0 0 ? S 09:59 0:00 [kthreadd]
root 3 0.0 0.0 0 0 ? I< 09:59 0:00 [rcu_gp]
root 4 0.0 0.0 0 0 ? I< 09:59 0:00 [rcu_par_gp]
root 5 0.0 0.0 0 0 ? I< 09:59 0:00 [netns]
root 7 0.0 0.0 0 0 ? I< 09:59 0:00 [kworker/0:0H-events_highpri]
root 9 0.0 0.0 0 0 ? I< 09:59 0:00 [kworker/0:1H-events_highpri]
.
demo 9788 0.1 1.4 763248 50480 ? Ssl 15:05 0:00 /usr/libexec/gnome-terminal-serv
demo 9814 0.0 0.1 224108 5664 pts/2 Ss 15:05 0:00 bash
demo 9849 0.0 0.0 222412 3588 pts/2 S+ 15:06 0:00 nano
demo 9873 0.0 0.1 233416 6280 pts/1 R+ 15:08 0:00 ps -aux
```

Linux 进程可以启动自己的子进程（称为派生），从而导致进程之间产生分级的父子关系。要查看进程树，请使用 `ps` 命令并包含 `-H` 参数。以下是执行 `ps -aH` 命令的树状输出部分：

```bash
$ ps -aH

PID TTY TIME CMD
10036 pts/3 00:00:00 ps
  6350 pts/0 00:00:00 sudo
  6354 pts/0 00:00:00 su
  6355 pts/0 00:00:00 bash
  5442 tty2 00:00:00 gnome-session-b
```

进程信息也可以通过 GNOME 桌面上的“系统监视器”（System Monitor）工具查看。该工具可以在桌面环境中搜索“System Monitor”来启动，也可以通过以下命令行启动：

```bash
$ gnome-system-monitor
```

一旦启动系统监视器，选择工具栏上的“进程”（Processes）按钮来列出系统上运行的进程，如下方的图 34-1 所示：

![](img/system_monitor_processes.png)

图 34-1

要更改列出的进程（例如，列出所有进程或仅列出自己的进程），可以使用如图 34-2 所示的菜单：

![](img/system_monitor_menu.png)

图 34-2

要过滤进程列表，点击标题栏上的搜索按钮并在搜索字段中输入进程名称：

![](img/system_monitor_search.png)

图 34-3

要显示有关特定进程的附加信息，从列表中选择该进程并点击对话框右下角的按钮（在图 34-4 中标记为 A）：

![](img/system_monitor_process_details.png)

图 34-4



点击该按钮后，会出现一个与图中标记为 B 类似的对话框。从列表中选择一个进程并点击“结束进程”（End Process）按钮（C）来将其终止。

要监控 CPU、内存、交换分区和网络使用，点击标题栏上的“资源”（Resources）按钮以显示如[图 34-5]所示的屏幕：

![](img/system_monitor_resources.png)

图 34-5

同样，通过选择“文件系统”（File Systems）工具栏按钮可以查看系统使用的存储空间摘要：

![](img/system_monitor_filesystems.png)

图 34-6

## 34.2 使用`top`进行实时系统监控

正如“Cockpit Web 界面概述”章节概述出的，Cockpit Web 界面可以执行基本的系统监控。上一节还解释了如何使用 GNOME 系统监视器工具来监控进程和系统资源。本章还探索了`ps`命令如何提供 RHEL 9 系统上运行进程的快照。然而，`ps`命令无法提供进程和系统资源使用的实时视图。`top`命令是从命令行实时监控系统资源和进程的理想工具。

运行时，`top`将根据系统资源使用情况列出系统运行的进程（需求最大的进程位于顶部）。屏幕的上部显示内存和交换分区的使用情况。所有输出都会不断更新，允许实时监控系统：

![](img/top_running.png)

图 34-7

要限制显示属于特定用户的进程，请使用`-u`参数启动`top`并加上用户名：

```bash
$ top -u john
```

要查看完整的功能列表，按下键盘`h`或参考 man 页面：

```bash
$ man top
```

## 34.3 命令行磁盘和交换分区监控

可以通过 Cockpit 和 GNOME 系统监视器监控磁盘空间。然而，要在命令行识别磁盘使用情况，`df`命令提供了一个实用的概述：

```bash
$ df -h
```

## 路径

- `/etc/httpd` [225]
- `/etc/passwd` [71]
- `/etc/samba/smb.conf` [150]
- `/etc/shadow` [71]
- `/etc/sshd_config` [137]
- `/etc/ssh/sshd_config.d` [137]
- `/etc/sudoers` [71]
- `/etc/systemd/system` [88]、[130]
- `/etc/yum.repos.d/` 78
- `/home` [69]
- `/proc/swaps` [257]
- `.requires` [89]
- `.ssh` [118]、[120]
- `/usr/lib/systemd/system` [88]
- `/var/log/maillog` [236]
- `.wants` [88]

## A

- ACC 公司 [8]
- 活动概览 [42]
- `adduser` [69]
- AIX [7]
- `alias` [65]
- 别名 [65]
- AMD-V [164]
- Andrew S. Tanenbaum [7]

## Apache

- `mod_ssl` [227]
- Apache Web 服务器 [223]

## 应用程序流 77

- AppStream 77、79
- 模块 79
- 软件包 79
- 配置文件 79
- AppStream 仓库 77
- `authorized_keys`文件 [122]

## B

- BaseOS 仓库 77、78

## Bash

- 脚本 [67]
- Bash Shell [61]
- 别名 [65]
- `.bashrc` [67]
- `chmod` [68]
- 命令行编辑 [62]
- do 循环 [67]
- `echo` [66]
- 环境变量 [66]
- 文件名补全 [64]
- 文件名简写 [64]
- for 循环 [67]
- 历史 [63]
- `HOME` [66]
- 输入和输出重定向 [64]
- `PATH` [66]
- 路径补全 [64]
- 管道 [65]
- `sh` [68]
- `stderr` [65]
- `stdin` [64]
- `stdout` [65]
- `basic.target` [84]
- 贝尔实验室 [61]
- Bourne Again SHell [61]
- Bourne shell [61]
- Brian Fox [61]
- `buildah` [207]
- 容器 [214]
- 来自镜像仓库 [214]
- 从零开始 [214]
- `installroot` [215]
- `run` [215]
- `umount` [215]
- `Buildah` [209]

## C

- CA [226]
- `cat` [64]
- `certbot` [227]
- 证书颁发机构 [226]
- 根 [205]
- `chmod` [68]
- `chroot` [205]
- `cifs`文件系统 [159]
- `CNI` [208]、[215]
- `Cockpit` [89]
- 访问 [50]
- 账户管理 [54]
- 应用程序 [55]
- `cockpit-machines` [171]
- `cockpit-storaged` [146]
- 创建虚拟机 [171]
- 驱动器 [244]
- 启用 [50]
- 扩展 [49]、[55]
- 防火墙管理 [114]
- 安装 [50]
- 日志 [52]
- 多台服务器 [57]
- 网络 [54]
- `NFS` [146]
- 概览 [49]
- 持久化指标 [58]
- Podman 容器 [218]
- 端口 [50]
- 选择桥接 [195]
- 服务 [54]、[89]
- 存储 [53]、[243]
- 系统 [51]
- `systemd` [89]
- 终端访问 [56]
- 用户管理 [71]
- 虚拟机 [55]
- 卷组 [253]
- `cockpit-machines` [171]
- `cockpit.socket` [50]
- `cockpit-storaged` [146]、[253]
- 压缩 X11 转发 [138]
- 连接配置 [96]
- `containerd` [205]
- 容器网络接口 [208]、[215]

## 容器

- 挂载镜像 [212]
- 桥接网络 [215]
- `buildah` [214]
- 网络 [215]
- 网络接口 [215]
- 概览 [205]
- 拉取镜像 [209]
- 删除镜像 [214]
- 运行镜像 [211]
- 保存为镜像 [213]
- 停止 [213]

# 索引

- 上下标签 153
- CRI-O 205
- C shell 61

## D

- 守护进程 83
- dash 43
- David Korn 61
- `dd` 13
- DDNS 223
- 默认启动项 31
- `default.target` [86]
- `df` 252、268
- 自主访问控制 152
- 磁盘驱动器
  - 检测磁盘 239
- 磁盘 I/O 269
- 磁盘分区
  - 格式化 38
- 磁盘使用情况 268
- `diskutil` 13
- `DISPLAY`变量 138
- `dmesg` 12
- `dnf` 25
- `groupinfo` 128
- `groupinstall` 128
- `grouplist` 128
- `dnf.conf`文件 78
- DNS 104
- DNS MX 记录 235
- Docker 205、206
- do 循环 67
- 域名服务器 104
- 双系统 35
- 双系统启动 29
- 动态 DNS 223
- DynDNS 223

## E

- `echo` 66
- 邮件服务器 231
- 加密
  - 磁盘 22
- 环境变量 66
- EPEL 32
- 错误列表 5
- `export` 66
- `exportfs` 144
- `ext2` 253
- `ext3` 253
- `ext4` 253
- 企业级 Linux 额外软件包 32

## F

- FAT16 29
- FAT32 29
- `fdisk` 33、35、240、251
- 创建分区 240
- 列出分区 240
- Fedora Linux 9
- Fedora 媒体写入 14
- Fedora 项目 9
- 文件名简写 64
- 文件系统
  - 创建 241
  - 挂载 242
- 文件传输（控制）103
- 文件传输（数据）103
- `findmnt` 12

### 防火墙

- 接口 109
- 概述 101、107
- 端口转发 113
- 端口 109
- 服务 109
- Web 服务器设置 224
- 区域 107
- `firewall-cmd` 103、110、130
- 启用 NFS 144
- 邮件设置 233
- Web 服务器设置 224
- `firewall-config` 115

### firewalld

- 默认区域 110
- 显示区域信息 110
- `firewall-cmd` 110
- `firewall-config` 115
- ICMP 规则 113
- 接口 107、109
- 列出服务 111
- 概述 107
- 永久设置 110
- 端口转发 113
- 端口规则 111、112
- 端口 107、109
- 重载 110
- 运行时设置 110
- 服务 107、110
- 状态 109
- 区域创建 112
- 区域/接口分配 112
- 区域 107
- 区域服务 111
- 用于 67
- `ForwardX11Trusted` 138
- `free` 258
- `-s`标记 268
- 自由软件基金 8
- `fsck` 242
- `fstab` 145、243
- FTP 101、103
- 全虚拟化 164
- Fuse NTFS 驱动 32

## G

- GDM 24
- gedit 138
- `getfacl` 174
- GNOME 桌面 41
- 活动概览 42
- dash 43
- `gnome-tweaks` 48
- 设置 47
- 启动 41
- 切换器 45
- 优化 48
- 窗口 44

# 工作空间 [45]

# GNOME 桌面环境 [127]

# GNOME 显示管理器 [24]

# `gnome-system-monitor` [265]

# `gnome-tweaks` [48]

# GNU/Linux [8]

# GNU 项目 [9]

# `graphical.target` [84]

# `groupadd` [70]

# `groupdel` [70]

# `groups` [70]

# `grub2-set-default` [32]

# `GRUB_SAVEDEFAULT` [31]

# 宾客操作系统虚拟化 [161]

# H

# 硬件虚拟化 [164]

# 惠普罗络（Hewlett-Packard）[7]

# `history` [62]、[63]

# `HOME` [66]

# HP-UX [7]

# HTTP [105]、[226]

# `httpd` [223]、[227]

# `httpd.conf` [225]、[227]

# `httpd-le-ssl.conf` [228]

# HTTPS [101]、[106]、[109]、[226]

# `hypercalls` [163]

# 超文本传输协议 [105]

# 安全超文本传输协议 [106]

# 虚拟机监控器（Hypervisor）[162]

# `hypercalls` [163]

# type-1 [162]

# type-2 [162]

# 虚拟机监控器虚拟化 [162]

# I

# IBM [7]

# ICMP [113]

# `id_rsa`文件 [118]、[120]、[121]

# `id_rsa.pub`文件 [118]、[122]

# if 语句 [67]

# IMAP4 [105]

# 输入/输出重定向 [64]

# 安装

## 磁盘分区 [20]

# 安装

## 清理磁盘 [11]

## 安装软件包

### 列出 78

# Intel VT [164]

# Intel x86

## 环 [163]

# 互联网控制消息协议 [113]

# 互联网消息访问协议版本 4 [105]

# 互联网服务提供商 [223]

# I/O 重定向 [65]

# `iotop` [269]

# `installing` [269]

## IPs [116]

## `iptables` [101]、[103]、[107]

## `tool` [102]

## `ip`工具 [94]

## ISO 镜像

写入 USB 盘 [12]

## ISP [223]

# J

## `journalctl` [130]、[135]

## 志日志文件系统 [242]

# K

## `dump` [19]

## `kernel` [7]

## `kill` [264]

## `-9`标志 [264]

## Korn shell [61]

## Kubernetes [206]

# KVM

## 硬件要求 [167]

## 安装 [168]

## 概述 [167]

## `virt-manager` [168]

## `kvm_amd` [168]

## `kvm_intel` [169]

## KVM 虚拟化 [165]

# L

## LE [248]

## Let’s Encrypt [227]

## `libvirtd` [179]

## `libvirtd`进程 [169]

## 林纳斯·托瓦尔斯（Linus Torvalds）[8]

## Linux 容器

### 逻辑区 [248]

## 逻辑卷 [248]

## 逻辑卷管理 [247]

## 回环接口 [93]

## `lost+found` [242]

## `ls` [62]、[65]

## `lscpu` [167]

## `lsmod` [168]

## LV [248]

## `lvdisplay` [249]、[252]、[259]

## LVM [247]

## `lxd` [205]

# M

## macOS

将 ISO 写入 USB 盘 [13]

## MacVTap [165]

## 邮件投递代理 [231]

## 邮件交换器 [235]

## 邮件传输代理 [231]

## 邮件用户代理 [231]

## `main.cf` [233]

## `man` [62]

## 强制访问控制 [152]

## 马克·尤因（Marc Ewing）[8]

## 马丁·赫尔曼（Martin Hellman）[117]

## MDA [231]

## MINIX [7]

## `mkfs.xfs` [38]、[241]

## `mkswap` [258]、[259]

## `mod_ssl` [227]

## `mount` [33]、[145]、[158]、[242]、[248]

## MTA [231]

# MUA [231]

# `multi-user.target` [84]

# MX [235]

# N

- `NAT` [165]、[173]
- NetBIOS [155]
- NetBIOS 名称服务 [155]
- 网络地址转换 [165]
- 网络桥接接口 [191]
- 网络文件系统 [106]

## NetworkManager

- 连接配置文件 [96]
- 启用 [92]
- 安装 [92]
- 权限 [99]
- 网络新闻传输协议 [105]
- 网络时间协议 [105]
- NFS [106]
- Cockpit [146]
- 防火墙设置 [144]
- `nfs-client.target` [84]
- NFS 服务 [143]
- `nfs-utils` [145]
- NMB [155]
- `nmcli` [91]、[193]
- 激活连接 [95]
- 添加桥接 [193]
- 添加连接 [97]
- 命令行选项 [92]
- 取消连接 [95]
- 删除连接 [97]
- 设备状态 [93]
- General 状态 [92]
- 交互式 [98]
- 修改连接 [95]
- 权限 [99]
- 重新加载 [96]
- 显示连接 [93]
- 切换连接 [94]
- Wi-Fi 扫描 [95]
- `nm-connection-editor` [91]
- 创建桥接 [197]
- `nmtui` [91]
- NNTP [105]
- NTFS [29]
- NTP [105]

# O

- OCI [207]
- 开放容器标准 [207]
- OpenShift [206]、[207]
- OSI 栈 [105]

# P

- 半虚拟化 [163]、[164]

## Partition

- 挂载 [38]
- `passwd` [69]
- `PATH` [66]
- 路径补全 [64]
- PE [248]
- 物理范围 [248]
- 物理卷 [247]
- 管道 [65]
- `podman` [207]、[209]
- `attach` [212]



- `commit` [213]
- `exec` [212], [213]
- `images` [211], [214]
- `inspect` [211]
- 网络命令 [217]
- 网络连接 [218]
- 网络创建 [217]
- 网络断开 [218]
- 网络检查 [217]
- 网络列出 [217]
- 网络删除 [218]
- 暂停 [213]
- `ps -a` [212]
- `pull` [211]
- `rm` [214]
- `run` [211]
- `stop` [213]
- `unpause` [213]
- `Podman` [205], [209]
- POP3 [105]
- 端口转发 [113], [224]

## Ports

- 加固 [101]
- Postfix [231], [232]
- 配置 [233]
- 安装 [233]
- `main.cf` [233]
- `postmap` [236]
- `sasl_passwd` [236]
- 启动 [235]
- 测试 [235]
- `postmap` [236]
- 邮局协议 [105]
- `poweroff.target` [83]
- PowerShell [121]
- 私钥 [117]
- `ps` [65], [153], [263]
- `-a flag` [263]
- `-aux flags` [264]
- `-H flag` [265]
- `TERM signal` [264]
- `-u flag` [263]
- 公钥 [117]
- 公钥加密 [117]
- PuTTY [123]
- 安全隧道 [133]
- X11 转发 [139]
- `PuTTYgen` [123]
- PuTTY 密钥生成器 [123]
- `PV` [247]
- `pvcreate` [252], [261]
- `pvdisplay` [250]
- `pwd` [62]

# Q

- QEMU [180]
- QEMU/KVM 虚拟机 [169]
- Qmail [232]

# R

- RealVNC [129]

# 索引

- `reboot.target` [84]
- Red Hat Container Registry [209]
- Red Hat Enterprise Linux
- 下载 [11]
- Red Hat, Inc. [7]
- Red Hat Package Manager 78
- Red Hat Support [8]

## 远程桌面访问

- 不安全 [127]
- 安全 [127]
- `remote-fs.target` [84]
- 远程安装 [18]
- 远程过程调用 [143]

## 仓库 77

- `rescue.target` [83]
- `resize2fs` [253]
- `restorecon` [154]
- RHGB [31]
- `RHSM token` [172]
- Richard Stallman [8]
- root 密码
- 在安装期间指定 [23]
- root 用户 [1]
- RPC [143]
- `rpcbind` [143]
- `rpm` 78
- RPM 78
- `runc` [207]

## S

### Samba [143], [150]

- 添加用户 [154]
- 防火墙设置 [150]
- 安装 [150]
- NetBIOS [155]
- `samba_share_t` [153]
- SELinux [152]
- `smbclient` [155], [158]
- `smb.conf` [150]
- `smbpasswd` [154]
- `smb_t` [153]
- `testparm` [155]
- Samba Client [150]
- `samba_share_t` [153]
- `sasl_passwd` [236]
- SATA [239]
- 安全文件传输协议 [103]
- Secure Shell [104], [117]
- 安全套接层 [226]
- Secure Sockets Layer [106]
- 安全隧道 [133]

### SELinux

- 上下文标签 [153]
- `restorecon` [154]
- Samba [152]
- `sestatus` [152]
- 类型强制 [153]

### SELinux

- 强制模式 [153]
- 允许模式 [153]
- Sendmail [231], [232]
- 服务器块 [149]
- 带 GUI 的服务器 [127]

### 服务

- 加固 [101]
- `sestatus` [152]
- `setfacl` [174]
- 设置应用 [73]
- 用户 [73]
- SFTP [103]
- `sh` [68]
- 脚本 [67]
- 简单邮件协议 [104]
- 简单邮件传输 [232]
- 简单网络管理 [106]
- `skopeo` [207], [209]
- Skopeo [209]
- `SMB` [149]
- `smbclient` [155], [158]
- `smb.conf` [150]
- 测试 [154]
- `testparm` [154]
- `smbpasswd` [154]
- `smb_t` [153]
- `SMTP` [101], [104], [109], [232]
- SMTP 继 [232], [236]
- `SNMP` [106]
- `sockets.target` [84]
- Solaris [7]
- 派生 [265]

### ssh

- `-C` 参数 [138]
- X11 转发 [138]
- `-X` 参数 [138]
- `SSH` [101], [104], [117]
- 微软 Windows [121]
- 多密钥 [120]
- VNC [132]
- `ssh client` [119]
- `ssh-copy-id` [119], [122]
- `sshd_config.d` [137]
- `sshd_config.d directory` [120]
- `sshd_config file` [120]
- `sshd service` [120]
- `ssh-keygen` [118]

### SSH 服务

- 安装 [118]
- [118]
- SSH 隧道 [132]
- `SSL` [106], [226]
- `SSL certificate` [226], [227]
- `SSL Labs` [229]
- `startx` [41], [129]
- `stderr` [65]
- `stdin` [64]
- `stdout` [64]

### 存储设备

- 识别 [12]
- 存储池 [176]
- 存储卷 [176]

### 订阅

- 绑定 [25]
- `subscription-manager` [25]
- `su -` 命令 [1]
- `sudo` [2]
- wheel 组 [70]
- SunOS [7]

# 超用户

# 交换分区 (Swap)

- 当前大小
- 空闲
- 逻辑卷
- `lvdisplay`
- `mkswap`
- `/proc/swaps`
- `pvcreate`
- 建议
- `swapoff`
- `swapon`

# 系统 (system)

- 单元
- 单元类型
- `systemctl`
- `daemon-reload`
- `systemd`
- 服务
- 目标 (targets)

# 系统监控 (System Monitor)

- 系统进程

# T

- TCP/IP
- 常用端口
- Telnet
- 终端窗口
- `TERM` 信号
- `testparm`
- `smb.conf`
- TFTP
- TigerVNC
- 安装
- 查看器
- TightVNC
- TLS
- `top`
- `-u` 参数
- 传输层安全
- 简单文件传输协议
- 可信的 X11 转发
- 第一型虚拟机管理程序
- 第二型虚拟机管理程序
- 类型强制执行

# U

- UBI
- `ubi-init`
- UDP
- `umount`
- 通用基础镜像
- UNIX
- 来源
- USB 设备名称
- `userdel`
- `usermod`
- 用户进程
- 用户与组

# V

- `VcXsrv`
- `VG`
- `vgdisplay`
- `vgextend`
- `vgs`
- `virbr0`
- `virsh`
- `destroy`
- `dumpxml`
- `edit`
- `help`
- `list`
- `reboot`
- `restore`
- `resume`
- `save`
- `setmem`
- `setmemmax`
- `shell`
- `shutdown`
- `start`
- `suspend`
- `virt-install`
- `virt-manager`
- 安装
- 新虚拟机向导
- 存储池
- VirtualBox
- 虚拟化
- AMD-V
- 完整的
- 客户机
- 硬件
- 超调用 (hypercalls)
- 虚拟机管理程序 (hypervisor)
- Intel VT
- KVM 虚拟化
- MacVTap
- 第一型
- 第二型
- `virt-manager`
- 虚拟机网络
- 虚拟网络计算
- `virt-viewer`
- VMware
- VNC
- 防火墙设置
- 安装
- PuTTY
- 安全
- 服务器关机
- 启动服务器
- 故障排除
- `vncpasswd`

# VNC 服务器

- `vncserver`
- `vncserver@.service`
- `vncpasswd`
- `vncserver`

# 配置

- `vncserver@.service`
- `vncviewer`

# 卷组 (Volume Group)

# W

- Wayland
- `wc`
- Web 服务器
- 测试

# 常用端口

- wheel 组 (wheel group)
- `which`
- 惠尔德·迪菲 (Whitfield Diffie)
- 通配符
- 通配符

# Windows

- 从 Linux 访问分区
- 磁盘管理 (Disk Management)
- 双启动
- 缩小卷
- 将 ISO 写入 USB 驱动器

## Windows 分区

- 回收
- 卸载

## Windows PowerShell

- `wipefs`

# 工作空间 (Workspaces)

- 工作站

# X

- X11 转发 (X11 Forwarding)
- 压缩
- `X11Forwarding`
- x86 家族
- `Xen`
- XFS 文件系统
- XFS 文件系统
- `xfs_growfs`
- `XLaunch`
- `X.org`
- X Window 系统

# Y

- `yum.repos.d` 目录
