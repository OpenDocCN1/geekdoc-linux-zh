# Ubuntu 20.04 核心：Ubuntu 20.04 桌面版与服务器版指南



![](img/ubuntu_20.04_front_cover_large.png)



ISBN-13: 978-1-951442-05-7






## 1. 引言

Ubuntu 可能是当今最受推崇和最广泛使用的 Linux 发行版之一。Ubuntu 以其易用性和可靠性深受赞誉，同时也拥有一批忠实的 Linux 用户群和一个活跃的开发者社区。

《Ubuntu 20.04 基础》旨在提供有关 Ubuntu 20.04 发行版安装、使用和管理的详细信息。对于初学者，本书涵盖了操作系统安装、GNOME 桌面环境基础、配置电子邮件和 Web 服务器以及安装软件包和系统更新等主题。书中还涵盖了额外的安装主题，如与 Microsoft Windows 的双系统启动，以及配置防火墙、用户和组管理等所有重要的安全主题。

对于经验丰富的用户，书中还详细介绍了远程桌面访问、Cockpit Web 界面、逻辑卷管理 (LVM)、磁盘分区、交换空间管理、KVM 虚拟化、Secure Shell (SSH)、Linux 容器以及使用 Samba 和 NFS 进行文件共享等主题，以对这一企业级操作系统提供全面的概述。

### 1.1 超用户规范

Ubuntu 与大多数 Linux 相同，有两种类型的用户账户：一种是标准用户账户，对操作系统的许多管理文件和功能的访问受限；另一种是具有特权权限的超级用户（root）账户。通常，用户可以通过登录为 root 用户或使用 `su -` 命令并输入 root 密码来获取 root 权限。在下面的示例中，用户通过 `su -` 命令获取 root 权限：

```bash[neil@demo-server ~]$ su -

Password:

[root@demo-server ~]#
```

注意，普通用户的命令提示符以 `$` 符号结尾，而 root 用户则为 `#` 字符。在命令行操作时，这是一个实用的指示，用于判断你是否正在以 root 用户身份发布命令。

如果 `su -` 命令失败，系统上的 root 账户可能出于安全原因已被禁用。在这种情况下可以使用下文所示的 `sudo` 命令。

使用 `sudo`，非 root 用户可以执行需要 root 权限的单个命令。考虑以下使用最新补丁和软件包更新操作系统的尝试：

```bash
$ apt update

Reading package lists... Done

E: Could not open lock file /var/lib/apt/lists/lock - open (13: Permission denied)
```

可选地，可以配置用户账户使其拥有 root 级权限。用户不再使用 `su -` 命令首先获取 root 权限，而是具有管理权限的用户账户可以使用 `sudo` 运行其他情况下受限的命令。

```bash
$ sudo apt update

[sudo] password for demo:

Hit:1 http://us.archive.ubuntu.com/ubuntu bionic InRelease
```

为了在不反复使用 `sudo` 命令的情况下执行多个命令，可以通过以下方式访问具有持久超级用户权限的命令提示符：

```bash
[neil@demo-server]$ sudo su -

[neil@demo-server]#
```

在本书如此早阶段提出这个问题的原因是，书中概述的许多命令行示例都需要 root 权限。我们不再重复地在每个命令行示例前加上“以 root 身份运行命令”的说明，而是使用行首的命令提示符来指示是否需要以 root 身份执行命令。如果命令可以作为普通用户运行，命令将以 `$` 命令提示符为开头，如下：

```bash
$ date
```

相反，如果命令需要 root 权限，则命令将以 `#` 命令提示符为开头：

```bash
## apt install openssh-server
```

### 1.2 打开终端窗口

如果你正在运行带有 GNOME 桌面的 Ubuntu 并需要访问命令提示符，你将需要打开一个终端窗口。可以通过右键点击桌面背景并选择“打开终端”（Open Terminal）菜单选项来实现，如图 1-1 所示：

![](img/ubuntu_20.04_gnome_desktop_menu.jpg)

图 1-1

也可以使用 `Ctrl-Alt-T` 快捷键在 GNOME 桌面打开终端窗口。

### 1.3 编辑文件

配置 Linux 系统通常涉及编辑文件。对于 Linux 新手来说，由于他们可能不清楚应该使用哪种编辑器。如果你正在运行终端会话且还没有首选的编辑器，我们建议使用 `nano` 编辑器。要在终端窗口中启动 `nano` 只需输入以下命令：

```bash
## nano <file>
```

其中 `<file>` 替换为你想要编辑的文件路径。例如：

```bash
## nano /etc/passwd
```

加载后，`nano` 将出现。完成文件编辑后，按 `Ctrl-S` 保存文件，按 `Ctrl-X` 退出。

如果你喜欢在 GNOME 桌面中使用图形化编辑器，`gedit` 是基础任务的良好起点。要在桌面启动 `gedit`，按下 `Alt-F2` 显示运行窗口，如图 1-3 所示：

![](img/ubuntu_18.04_enter_command.jpg)

图 1-3

在文本框中输入 `gedit` 并按下 `Enter` 键。稍后`gedit` 将加载并准备打开、创建和编辑文件：

![](img/ubuntu_18.04_gedit.jpg)

图 1-4

或者，从终端窗口启动 `gedit`，带或不带文件路径：

```bash
## gedit
## gedit /etc/passwd
```

### 1.4 反馈

我们希望你对本书满意。如果在书中发现任何错误，或有任何意见、问题或担忧，请通过邮件联系我们：feedback@ebookfrenzy.com。

### 1.5 更新

虽然我们努力确保书中内容的准确性，但对于如此规模和复杂的主题，不可避免会出现某些错误和遗漏。书中的已知问题将与解决方案列在以下 URL：

[`www.ebookfrenzy.com/errata/ubuntu2004.html`](https://www.ebookfrenzy.com/errata/ubuntu2004.html)

如果你发现了未列在更新中的错误，请通过邮件告知我们的支持团队：feedback@ebookfrenzy.com。

## 2. Linux 简史

Ubuntu Linux 是 Linux 操作系统众多变体（也称为发行版）之一，是英国公司 Canonical Ltd. 的产物。该公司由 Mark Shuttleworth 于 1994 年创立。然而，Linux 的起源可以追溯到更早。本章将概述 Linux 操作系统和 Ubuntu 的历史。

### 2.1 到底什么是 Linux？




Linux 是一个操作系统，就像 Windows 是操作系统一样（尽管 Linux 和 Windows 之间没有任何相似之处）。“操作系统”一词被描述为作为计算机硬件与我们日常运行的应用程序之间中间层的软件。当程序员编写应用程序时，他们通过与操作系统交互来执行诸如将文件写入硬盘驱动以及在屏幕上显示信息等任务。如果没有操作系统，每位程序员都必须编写代码来直接访问系统硬件。此外，程序员必须能够支持曾经创建过的每一件硬件，以确保应用程序可以在任何可能的硬件配置上运行。由于操作系统处理了所有的硬件复杂性，应用程序开发变成了一项简单得多的任务。Linux 是如今许多不同操作系统之一。

## 2.2 UNIX 的起源

要理解 Linux 的历史，我们首先必须追溯到 20 世纪 60 年代末的 AT&T 实验室。当时，AT&T 停止了对名为 Multics 的新操作系统的开发。两位 AT&T 工程师肯·汤普森（Ken Thompson）和丹尼斯·里奇（Dennis Ritchie）决定将他们在 Multics 项目中学学到的知识，创建一个名为 UNIX 的新操作系统，该系统迅速在企业和学术机构中流行并被广泛采用。

各种专有的 UNIX 实现最终进入市场，包括由 IBM (AIX)、惠尔士惠普 (HP-UX) 和太阳微系统 (SunOS 和 Solaris) 创建的版本。此外，安德鲁·S·塔南鲍（Andrew S. Tanenbaum）创建了一个名为 MINIX 的类 UNIX 操作系统，旨在教学，并向大学提供源代码。

### 2.3 谁创建了 Linux？

Linux 的起源可以追溯到两个人的工作和哲学。Linux 操作系统的核心是一个被称为“内核”（kernel）的东西。这是操作系统运行所需的核心功能集。内核管理系统资源并处理硬件与应用程序之间的通信。Linux 内核是由林纳斯·托瓦尔斯（Linus Torvalds）开发的，由于不喜欢 MS-DOS，并且由于不急于让 MINIX 在新的 Intel 80386 微处理器上可用，他决定编写自己的类 UNIX 内核。当他完成内核的第一版本时，他以开源许可发布了它，这允许任何人下载源代码并自由使用和修改它，而无需向林纳斯支付任何费用。

大约同一时间，自由软件基金会的自由和开源软件的有力倡导者理查德·斯托曼（Richard Stallman）正在开发他自己的开源操作系统。然而，斯托曼最初并没有专注于内核，而是决定从开发使用和维护操作系统所必需的所有 UNIX 工具、实用程序和编译器的开源版本开始。当他完成这些基础设施的开发时，显而易见的解决方案是将他的工作与林纳斯写的内核相结合，创建一个完整的操作系统。这种组合被称为 GNU/Linux。纯洁者坚持认为 Linux 应该被称为 GNU/Linux（事实上，曾有一段时间，理查德·斯托曼拒绝接受未将 Linux 称为 GNU/Linux 的出版物的采访）。考虑到自由软件基金会开发的 GNU 工具构成了 GNU/Linux 重要且关键的一部分，这并不是 unreasonable。遗憾的是，大多数人和出版物简单地将其称为 Linux，这种情况可能会一直持续下去。

### 2.4 Ubuntu 的历史

如前所述，Ubuntu 是许多 Linux 发行版之一。构成 Ubuntu 发行版的源代码源于一个备受推崇的 Linux 发行版 Debian，是由伊恩·默多奇（Ian Murdoch）创建的。

一位名叫马克·舒特尔沃（Mark Shuttleworth）的南非互联网大亨（他通过将公司卖给 VeriSign 大约获得了 5 亿美元的财富）决定是时候需要一个更易于使用的 Linux 了。他采用了 Debian 发行版，并使其成为一个更友人类的发行版，他将其命名为 Ubuntu。随后他成立了名为 Canonical Ltd 的公司来推广和提供 Ubuntu 支持。

如果你是 Linux 新手，或者已经在使用 Linux 并想尝试不同的 Linux 发行版，你可能找不到比 Ubuntu 更好的选择了。

### 2.5 “Ubuntu”这个词是什么意思？

“Ubuntu”是一个古老的祖鲁语和科萨萨语词汇，意思是“对他人的人性”。Ubuntu 也意味着“因为我们大家的存在，我才是我”。选择它是因为这些情感准确地描述了 Ubuntu 发行版的精神。

### 2.6 总结

Linux 操作系统的起源可以追溯到林纳斯·托瓦尔斯和理查德·斯托曼的工作，形式为 Linux 内核结合 GNU 项目构建的工具和编译器。

多年来，Linux 的开源特性导致了各种不同 Linux 发行版的发布。其中一种发行版就是 Ubuntu，它基于 Debian Linux 发行版，并由马克·舒特尔沃创立的公司 Canonical Ltd 创建。

## 3 在空白磁盘驱动器上安装 Ubuntu

现在有三种方法部署 Ubuntu 系统。一种方法是购买新硬件，或重新利用现有的计算机系统以在上面安装和运行操作系统。或者，可以使用 VirtualBox 或 VMware 等虚拟化平台，在现有操作系统的虚拟机内部安装并运行 Ubuntu。另一种选择是使用 Amazon AWS、Google Cloud 或 Microsoft Azure（仅列部分）等服务创建云操作系统实例。由于云实例通常是通过选择预先配置、准备就绪且已针对云平台优化的操作系统镜像，并以此作为 Ubuntu 系统的基础，在这种情况下不需要执行手动操作系统安装。

另一方面，如果你计划在自己的硬件上安装 Ubuntu 或使用虚拟化环境，那么学习 Ubuntu 路径的第一步涉及安装操作系统。

Ubuntu 可以安装在洁净磁盘环境中（清除整个磁盘上的任何现有分区并将其完全用于 Ubuntu），也可以安装在双启动环境中，在双启动环境中，Ubuntu 与磁盘上的另一个操作系统共存（通常是微软 Windows 操作系统家族的成员）。

在本章中，我们将介绍从本地或远程安装介质进行洁净磁盘安装的方法。与 Windows 10 系统的双启动安装将在《在 Windows 上双启动 Ubuntu》中介绍。

### 3.1 Ubuntu 安装选项

可以从以下网页免费下载 Ubuntu：

`https://ubuntu.com/download`

该页面提供了若干下载选项，取决于如何安装和使用操作系统：

•Ubuntu Desktop - 下载操作系统桌面版的安装介质。该版本旨在供需要图形化桌面环境的台式式电脑和笔记本电脑使用，且仅适用于 64 位 x86 系统。桌面版可以以 ISO 镜像的形式下载，然后可以使用本章稍后概述的步骤将其写入 USB 驱动器。启动后，桌面介质将允许你在执行安装之前运行 Live Ubuntu 会话来测试 Ubuntu。




## Ubuntu Server

下载该操作系统服务器版本的安装介质。此镜像用于在不需要图形桌面环境的服务器上进行安装，适用于 x86、ARM、IBM POWER (PowerPC) 和 s390x (IBM System z 主机) 系统。安装介质不包含安装前尝试 Ubuntu 的选项，并使用基于文本的安装器而不是 Ubuntu 桌面版使用的图形安装器。这允许 Ubuntu 安装在没有图形控制台的系统上。

下载 Ubuntu Server 版本时，有以下可用选项：

- **标准 Live Server ISO 镜像 (Standard Live Server ISO Image)** - 包含安装 Ubuntu Server 的所有内容。这允许在不需要网络或互联网连接的情况下进行安装。
- **网络安装器 ISO 镜像 (Network Installer ISO Image)** - 包含开始安装过程所需的最小内容，在此期间将根据配置阶段的选择下载额外的软件包。网络安装器将在“使用网络安装器安装 Ubuntu”章节中进行详细介绍。

Live Server 和网络安装器镜像也可用于执行预启动执行环境 (PXE) 网络安装。使用 PXE 安装 Ubuntu 时，Ubuntu 镜像将安装在特殊配置的服务器（称为 PXE 启动服务器）上。要安装 Ubuntu 的客户端系统将配置为通过网络从 PXE 启动服务器上的镜像启动（假设客户端硬件支持 PXE）以启动安装。

### 3.2 服务器版 vs. 桌面版

在开始安装之前，显然需要在桌面版和服务器版镜像之间做出决定。如果你想在安装之前先尝试 Ubuntu，那么桌面版是最佳解决方案，因为它允许你从安装介质启动 Ubuntu，而无需先将其安装到磁盘驱动器上。如图 3-1 所示，此选项允许从实时会话内部启动安装：

![](img/ubuntu_20.04_install_or_try.jpg)

图 3-1

如果不需要图形桌面环境，且目标系统没有互联网访问或图形控制台，则推荐 Live Server ISO 镜像，因为这可以在不需要下载任何额外软件包的情况下构建功能完全的服务器。

无论选择何种安装方法，在安装后都可以向系统添加或删除软件包，以根据特定需求配置系统。

### 3.3 获取 Ubuntu 安装介质

为了本章的目的，将使用图形安装器安装 Ubuntu 桌面环境。因此，请从以下 URL 下载 Ubuntu Desktop 20.04 ISO 镜像：

[`ubuntu.com/download/desktop`](https://ubuntu.com/download/desktop)

DVD ISO 镜像是自包含的，包含了安装 Ubuntu 系统所需的所有软件包，并采用以下约定命名：

`ubuntu-<version>-<edition>-<architecture>.iso`

例如，适用于 64 位 Intel/AMD 系统的 Ubuntu 20.04 桌面版 ISO 镜像命名如下：

`ubuntu-20.04-desktop-amd64.iso`

下载好镜像后，可以将其刻录到磁盘，或使用下一节中的步骤将介质写入 USB 驱动器，并配置你的虚拟化环境将其视为 DVD 驱动器。

### 3.4 将 ISO 安装镜像写入 USB 驱动器

如今，操作系统的安装更有可能通过 USB 驱动器执行，而非 DVD。。下载了 Ubuntu 的 ISO 安装镜像后，将该镜像写入 USB 驱动器的步骤将取决于该驱动器连接到 Linux、macOS 还是 Windows 系统。本节剩余部分的概述步骤假设 USB 驱动器是新的，或者已经重新格式化以删除任何现有数据或分区：

### 3.4.1 Linux

在 Linux 上将 ISO 镜像写入 USB 驱动器的第一步是识别设备名称。在插入 USB 驱动器之前，通过列出 `/dev` 中的设备来识别系统中已检测存储设备：

```bash
ls /dev/sd*
```

`/dev/sda /dev/sda1 /dev/sda2`

将 USB 驱动器连接到 Linux 系统并运行 `dmesg` 命令获取最近系统消息列表，其中一个将是检测到 USB 驱动器的报告，类似于以下：

```
[445597.988045] sd 6:0:0:0: [sdb] Attached SCSI removable disk
```

此输出告诉我们，应该预期设备名称包含 `sdb`，我们可以通过再次列出 `/dev` 中的设备名称来确认这一点：

```bash
ls /dev/sd*
```

`/dev/sda /dev/sda1 /dev/sda2 /dev/sdb`

从此输出我们可以知道 USB 驱动器已被分配到 `/dev/sdb`。在将 ISO 镜像写入设备之前的下一步是运行 `findmnt` 命令以确保它没有被自动挂载：

```bash
findmnt /dev/sdb?
```

`TARGET SOURCE FSTYPE OPTIONS`
`/media/demo/C24E-6727 /dev/sdb1 vfat rw,nosuid,nodev, ...`

如果 `findmnt` 命令指示 USB 驱动器已挂载，请在继续之前将其卸载：

```bash
umount /media/demo/C24E-6727
```

一旦文件系统已卸载，使用如下的 `dd` 命令将 ISO 镜像写入驱动器：

```bash
dd if=/path/to/<image>.iso of=/dev/sdb
```

写入过程可能需要一些时间（最长 15 分钟），取决于镜像大小和系统速度。写入完成后，将出现类似下面的输出，此时 USB 驱动器可以使用。

### 3.4.2 macOS

在 macOS 上将 ISO 镜像写入 USB 驱动器的第一步是使用 `diskutil` 工具识别设备。在连接 USB 驱动器之前，打开终端窗口并运行：

```bash
diskutil list
```

`/dev/disk0 (internal):`
`#: TYPE NAME IDENTIFIER`
`0: GUID_partition_scheme *1.0 TB disk0`
`1: EFI 209.7 MB disk0s1`
`2: Apple_FS Container 999 GB disk0s2`

`/dev/disk1 (external):`
`#: TYPE NAME IDENTIFIER`
`0: GUID_partition_scheme 28.0 GB disk1`
`1: EFI 314.6 MB disk1s1`
`2: Apple_APFS Container 27.7 GB disk1s2`

在上面的示例中，USB 驱动器已被分配到 `/dev/disk3`。在继续之前，按如下方式卸载磁盘：

```bash
diskutil unmountDisk /dev/disk3
```

`Unmount of all volumes on disk3 was successful`

最后，使用 `dd` 命令将 ISO 镜像写入设备，注意引用原始磁盘设备（/dev/rdisk3`）并在提示时输入用户密码：

```bash
sudo dd if=/path/to/iso/image.iso of=/dev/rdisk3 bs=1m
```

### 3.4.3 Windows

Windows 上有许多免费工具可以将 ISO 镜像写入 USB 驱动器，但一种专门为写入 Linux ISO 镜像编写的工具是 Fedora Media Writer，它可以通过以下 URL 下载：

[`getfedora.org/en/workstation/download/`](https://getfedora.org/en/workstation/download/)





安装完成后，启动写入工具并选择如图 3-2 所示亮出的“自定义”（Custom）镜像选项：

![](img/fedora_31_media_writer.jpg)

图 3-2

在出现的文件选择对话框中，导航并选择 Ubuntu 安装 ISO 镜像，然后点击`打开`Open）按钮。选择镜像后将弹出一个对话框，其中可以将镜像写入 USB 驱动器。在点击`写入磁盘`Write to Disk）按钮之前，请从设备菜单中选择目标 USB 驱动器：

![](img/ubuntu_20.04_fedora_writer.jpg)

图 3-3

一旦镜像写入设备，该设备即可准备好执行安装。

### 3.5 从 Ubuntu USB 镜像启动

将 Ubuntu 安装介质插入相应的驱动器并启动系统。如果系统尝试从硬盘启动，你将需要进入电脑的 BIOS 设置并更改启动顺序，以便首先从安装介质驱动器启动。在启动过程的前几秒内，会出现一个大程度上空白的屏幕，底部边缘会显示以下图像：

![](img/ubuntu_18.04_first_boot_screen.jpg)

图 3-4

在此处采取任何操作，Ubuntu 将进入现场会话（Live session），并提供选项：要么在不安装 的情况下尝试 Ubuntu，要么如上方的图 3-1 所示开始安装过程。或者，按下键盘上的`Esc`键将进入启动菜单系统，从图 3-5 所示的语言选择界面开始：

![](img/ubuntu_18.04_boot_menu_language.jpg)

图 3-5

使用键盘方向键导航并按`回车`Enter 键选择语言，随后将显示所示的 Ubuntu 启动菜单屏幕：

![](img/ubuntu_20.04_install_menu.jpg)

图 3-6

再次提供了尝试 Ubuntu 现场会话或开始安装过程的选项。如果你在尝试启动或安装 Ubuntu 时遇到黑屏，请重启系统并尝试使用其中一个安全图形选项。也可以检查安装介质和系统内存是否存在缺陷，或从安装在计算机系统的主硬盘启动系统（假设其包含可引导的操作系统镜像）。一系列`功能`键选项提供了访问设置的方法，例如更改辅助选项、访问帮助以及指定特殊的启动参数。

### 3.6 安装 Ubuntu

在现场会话或启动菜单中，选择开始 Ubuntu 安装的选项，并等待安装程序的初始屏幕出现：

![](img/ubuntu_20.04_install_language_selection.jpg)

图 3-7

在欢迎屏幕上，点击`继续`Continue 按钮之前选择你首选的语言以进入下一个屏幕：

![](img/ubuntu_20.04_install_keyboard_type.jpg)

图 3-8

选择你的键盘布局，或者如果你不确定，点击`检测键盘布局`Detect Keyboard Layout 按钮，通过一些步骤识别你的键盘，然后点击`继续`Continue。在下一个屏幕上，选择执行`标准`Normal 还是`最小化`Minimal 安装：

![](img/ubuntu_20.04_install_type.jpg)

图 3-9

如果你有足够的磁盘空间，并希望探索 Ubuntu 包含的主要应用程序和实用程序，而无需以后手动安装它们，请选择`标准`Normal 选项。或者，为了避免用你可能永远需要的软件占用系统，请选择`最小化`Minimal 选项。无论在这里做出什么选择，如果将来需要，Ubuntu 的所有软件都可以在任何时候轻松地安装或删除。

安装过程中还提供了在更新组成 Ubuntu 发行版的软件包的选项。Ubuntu 与大多数受到活跃支持的操作系统一样，在向公众发布很长时间后仍继续通过错误修复和安全补丁进行更新。如果选择此选项且系统连接到互联网，安装程序将下载自 Ubuntu 安装镜像发布以来发布的所有更新，并在安装期间将其应用到系统。如果你选择在安装过程中不执行此更新，这些更新可能在安装完成后的任何时间仍然应用。

第二个选项提供了选择是否安装第三方非开源软件的选项，以支持特定的硬件设备并在系统上播放专有媒体文件。某些用户强烈反对使用任何未在公用许可下发布的软件。如果你是这些人中的一一员，请不要选择此选项。相反，如果你只想获得 Ubuntu 安装的最佳体验，则建议选择此选项。

做出适当选择后，点击`继续`Continue 按钮进入磁盘分配屏幕：

![](img/ubuntu_20.04_install_disk_options.jpg)

图 3-10

假设这是一块没有现有操作系统的新磁盘，安装程序将提供擦除整个磁盘并将其用于 Ubuntu 的选项（在这种情况下，安装程序将计算并实施一种典型且推荐的分区布局）。或者，若要定义你自定义的磁盘布局，请选择`其他`Something else 选项，手动创建并调整包含操作系统和数据的磁盘分区。

点击`高级功能`Advanced Features 按钮将提供使用逻辑卷管理（LVM）的选项。强烈建议使用 LVM 以使系统磁盘和分区的管理更加容易，该主题在向 Ubuntu 卷组添加逻辑卷中进行了详细介绍：

![](img/ubuntu_20.04_install_disk_features.jpg)

图 3-11

如果磁盘上存储数据的安全性至关重要，请选择加密 Ubuntu 安装。如果选择了此选项，下一个屏幕将提示你选择安全密钥，该密钥在每次系统启动时都需要输入。

还提供了使用`ZFS`文件系统的选项。ZFS 是一种高级文件系统，内置了逻辑卷管理的许多功能，以及一系列其他功能，例如创建磁盘快照和影子功能（写时复制）。尽管 ZFS 已经存在多年，但在 Ubuntu 上的实现在现阶段被认为是实验性的，不应在生产环境中使用。

做出选择后，点击`现在安装`Install Now 按钮开始安装过程，此时系统将确认对磁盘驱动器的更改：

![](img/ubuntu_20.04_install_write_changes.jpg)

图 3-12

在安装过程中，安装程序将询问你的地理位置信息，以便配置时区设置：

![](img/ubuntu_20.04_install_where_are_you.jpg)

图 3-13

接下来，安装程序将要求你为系统的第一个账户提供用户名和密码：

![](img/ubuntu_20.04_install_user_setup.jpg)

图 3-14

还提供了一个选项，规定用户在每次想要登录系统时是否指定密码。默认情况下，每次 Ubuntu 启动时都会出现需要用户名和密码凭据的登录屏幕。如果你是系统的唯一用户并希望跳过此屏幕并在系统每次启动时自动登录，请务必在继续之前勾选`自动登录`Log in automatically 复选框。




当所有问题都回答后，安装程序将继续进行安装。根据你的系统速度以及你是否选择在安装期间下载更新，此过程可能需要一些时间。要查看安装程序正在执行的步骤的详细信息，请点击进度条上方状态标题：

![](img/ubuntu_20.04_install_details.jpg)

图 3-15

安装完成后，将弹出一个对话框通知系统已准备好重启：

![](img/ubuntu_20.04_install_complete.jpg)

图 3-16

当你准备好重启时，按下 `Restart Now`（立即重启）按钮。安装程序可能会提示你移除安装介质，系统将花费几秒钟关机。此时，移除 USB 闪盘并按 `Enter` 键继续。

### 3.7 访问 Ubuntu 桌面

系统启动后，如果启用了密码要求选项，GNOME 显示管理器（`GDM`）登录屏幕（图 3-17

图 3-17

或者，如果安装配置为直接登录桌面，则在系统重启后，GNOME 桌面（图 3-18

图 3-18

### 3.8 安装更新

与现今大多数操作系统一样，Ubuntu 发行版的每个特定版本在发布后都会持续演进。这通常表现为错误修复和安全更新，偶尔还会有可以通过互联网下载并安装到系统中的新功能。

最佳实践建议安装 Ubuntu 后的第一步是确保将任何可用的更新应用到系统。这可以通过 Terminal（终端）窗口中的命令行提示符使用 `apt` 软件包管理器工具来实现。要检查可用更新，右键点击桌面背景，并从弹出的菜单中选择 `Open in Terminal`（在终端中打开）选项：

![](img/ubuntu_20.04_desktop_open_in_terminal.jpg)

图 3-19

在 Terminal 窗口中，运行以下命令以获取 root 权限并更新包列表：

```bash
$ sudo su -
## apt update
```

如果有可更新的软件包，命令将显示类似下面的输出：

```
Reading package lists... Done
Building dependency tree
Reading state information... Done
103 packages can be upgraded. Run ‘apt list --upgradable’ to see them.
```

任何待处理的更新可以使用 `apt` 工具应用：

```bash
## apt upgrade
```

执行后，`apt` 工具将提供一份可用更新的软件包列表，并请求执行更新的权限：

```
103 upgraded, 7 newly installed, 0 to remove and 0 not upgraded.
Need to get 75.2 MB/286 MB of archives.
After this operation, 352 MB of additional disk space will be used.
Do you want to continue? [Y/n]
```

一旦升级完成，安装基本上结束了。

### 3.9 显示启动消息

在启动过程中，系统将显示 Ubuntu 启动界面，该界面会隐藏系统加载时生成的所有启动消息。若要在启动过程中显示这些消息（如图 3-20 所示），只需在系统启动时按下键盘上的 `Esc` 键即可：

![](img/ubuntu_18.04_boot_messages.jpg)

图 3-20

可以更改默认行为，通过编辑 `/etc/default/grub` 文件并更改 `GRUB_CMDLINE_LINUX` 设置，使其默认始终显示消息，该设置默认类似于如下内容：

```
GRUB_CMDLINE_LINUX="... rhgb quiet"
```

如果你是 Linux 新手且不熟悉可用的编辑器，请参考“引言”章节中概述的编辑器建议。例如，要使用 `nano` 编辑器，输入以下命令启动编辑器并加载 grub 文件：

```bash
## nano /etc/default/grub
```

要移除图形化启动界面以便在不按 `Esc` 键的情况下显示消息，请从设置中移除“splash”和“quiet”选项：

```
GRUB_CMDLINE_LINUX=""
```

此更改将导致系统显示其生成的所有启动消息。

一旦完成更改，运行以下命令生成新的启动配置，以便在下次系统启动时生效：

```bash
## grub-mkconfig --output=/boot/grub/grub.cfg
```

### 3.10 总结

使用 Ubuntu 的第一步是安装操作系统。对于云服务器而言，此任务通常在根据云服务提供商提供的系列选项为系统选择操作系统镜像时自动完成。然而，在您自己的硬件或虚拟机上安装，则涉及下载 ISO 镜像形式的安装介质，并将该镜像写入适当的存储设备中。

## 4. 使用网络安装器安装 Ubuntu

上一章探讨了安装 Ubuntu 的各种选项，重点讨论了使用图形化安装程序。本章将详细介绍使用网络安装镜像安装 Ubuntu。

### 4.1 网络安装器的优势

网络安装器（也称为 Netboot）镜像提供了一个较小的镜像（与 Desktop 镜像相比，大小约为 50MB），用于安装服务器或桌面 Ubuntu 环境。此选项需要连接互联网在安装期间下载额外的软件包，并使用基于文本的安装程序。

虽然 Server 和 Desktop 镜像在安装期间提供的配置选择非常少，但网络安装器在安装期间提供了大量预定义的软件包集合供选择。例如，Ubuntu Desktop 镜像只会安装 GNOME 桌面环境。而网络安装器允许你安装包括 KDE Plasma (Kubuntu) 和 LXQt (Lubuntu) 在内的多种桌面环境。还可以选择安装基础服务器环境以及可选的服务器相关软件包，如 Web 服务器、邮件服务器和数据库软件。

使用 Server 和 Desktop 镜像在安装完成后也可以添加或删除任何软件包，但如果你希望使用可以快速写入 USB 闪盘并允许预安装许多软件依赖的小型安装镜像，网络安装器是一个理想选择。

### 4.2 获取网络安装镜像

Ubuntu 20.04 的网络安装镜像可以从以下网页下载：

[`archive.ubuntu.com/ubuntu/dists/focal/main/installer-amd64/current/legacy-images/netboot/mini.iso`](http://archive.ubuntu.com/ubuntu/dists/focal/main/installer-amd64/current/legacy-images/netboot/mini)

下载后，按照“在空白硬盘上安装 Ubuntu”章节中的步骤将 `mini.iso` 镜像写入 USB 闪盘。

### 4.3 从安装镜像启动





插入 Ubuntu 安装介质并启动系统。如果系统尝试从硬盘启动，你将需要进入计算机的 BIOS 设置并更改启动顺序，使系统首先从安装介质驱动器启动。一旦系统启动，将显示图 4-1 所示的屏幕：

![](img/ubuntu_18.04_network_install_boot_menu.jpg)

图 4-1

### 4.4 执行安装

在菜单中，选择 `Install`（安装）选项并按下键盘 `Enter` 键开始安装过程。在接下来的几个屏幕中，使用键盘方向键和 `Enter` 键选择你偏好的语言和键盘类型。

在完成配置选择后，安装程序程序将扫描设备硬件以寻找网络接口：

![](img/ubuntu_18.04_network_install_detect_network.jpg)

图 4-2

一旦检测到网络连接，系统将需要分配一个主机名，以便其在网络上显示。在提示时，输入主机名，然后使用 `Tab` 键导航到 `Continue`（继续）按钮，最后按下 `Enter` 键进入下一个屏幕。

在安装期间，安装程序将仅下载匹配你在安装过程中所做的软件选择所需的软件包。这些 Ubuntu 软件包托管在世界各地的镜像服务器上。为了确保最佳的下载性能，请选择系统所在的国家：

![](img/ubuntu_18.04_network_install_choose_mirror.jpg)

图 4-3

在下一个屏幕上，继续之前请选择一个镜像服务器：

![](img/ubuntu_18.04_network_install_choose_mirror_site.jpg)

图 4-4

如果执行安装的计算机位于基于代理的防火墙之后，请在图 4-5 所示的屏幕上输入代理信息。代理服务防火墙位于互联网和计算机内部网络之间，充当这两个环境之间的中间介。在有了代理服务的情况下，内部客户端计算机不会直接连接到外部资源。相反，它们连接到代理服务器，由代理服务器代表客户端连接外部资源，从而掩盖客户端的内部 IP 地址。来自外部资源的任何响应都将由代理服务处理，并将其传递给最初请求数据的客户端：

![](img/ubuntu_18.04_network_install_proxy.jpg)

图 4-5

如果不需要代理信息，请直接留空此字段并进入下一个屏幕。

在此处，安装程序将下载一些启动安装所需的基础软件包。完成后，将出现一系列屏幕，要求输入要添加到系统的第一个用户的全名、用户名和密码。一旦提供了这些信息，安装程序将根据互联网连接的外部 IP 地址识别系统的地理位置。如果安装程序正确检测到了位置，请接受该位置；否则请手动进行选择。

### 4.5 磁盘分区

安装设置的下一阶段涉及如何分区和管理磁盘驱动器：

![](img/ubuntu_18.04_network_install_disk_partitioning.jpg)

图 4-6

假设这是一块没有安装现有操作系统的新磁盘，安装程序将提供擦除整个磁盘并将其用于 Ubuntu 的选项（在这种情况下，安装程序将计算并实施典型且推荐的分区布局）。如果存储在磁盘上的数据安全性至关重要，请选择加密 Ubuntu 安装的选项。如果选择了此选项，稍后的屏幕将提示你选择安全密钥，之后每次启动系统时都需要输入该密钥。

强烈建议使用逻辑卷管理（`LVM`）选项，以便更容易管理系统上的磁盘和分区，该主题在“向 Ubuntu 组和逻辑卷添加新磁盘”章节中有详细介绍。

或者，要定义你自定义的磁盘布局或实施 RAID 等高级配置，请选择 `Manual`（手动）选项：

![](img/ubuntu_18.04_network_install_disk_partitioning_manual.jpg)

图 4-7

除非你有特定需求，否则选择执行引导式 LVM 安装的选项，并按照步骤确认目标磁盘驱动器并选择分配给分区的可用空间大小。最后，检查分区配置摘要，并选择图 4-8 所示的 `Finish partitioning and write changes to disk`（完成分区并将更改写入磁盘）菜单选项：

![](img/ubuntu_18.04_network_install_disk_write_partition.jpg)

图 4-8

提供最终确认，然后等待创建分区并安装基础系统。

![](img/ubuntu_18.04_network_install_base_system.jpg)

图 4-9

在下一个屏幕上，选择你为运行中的系统安装更新的偏好选项。通常建议自动安装更新，但如果你倾向于控制何时安装更新，也可以使用手动选项。相反，如果你正在使用 Landscape Web 管理环境管理多个 Ubuntu 系统，请从菜单中选择 `Landscape` 选项：

![](img/ubuntu_18.04_network_install_choose_updates.jpg)

图 4-10

### 4.6 软件集合选择

网络安装的最后一步是选择要安装的软件集合。这在图 4-11 所示的屏幕中进行：

![](img/ubuntu_18.04_install_software_selection.jpg)

图 4-11

根据你的需求选择你需要的集合（记住可以在运行系统中随时添加或删除软件包）。

一旦在你需要的项目上标记了星号，选择 `Continue`（继续）选项并等待所选软件包的下载和安装。软件完成后，将出现一个屏幕寻求确认可以修改磁盘上的主引导记录以添加 Ubuntu 启动选项。最后，安装程序将确认系统是否使用协调世界时（`UTC`）。除非系统与 Windows 双启动，否则不应选择此选项。

安装完成后，移除安装介质，按下 `Enter` 键并等待系统重启。

### 4.7 系统设置后安装软件集合

一旦系统运行，上述图 4-11 中列出的任何软件集合都可以在运行的 Ubuntu 系统中使用 `tasksel` 工具手动安装。该工具可以在终端窗口中使用以下命令安装：

```bash
apt install tasksel
```

安装后，按如下命令运行：

```bash
tasksel
```

### 4.8 总结





Ubuntu 网络安装提供了一种使用较小的 ISO 镜像安装 Ubuntu 的方法。这要求目标系统具有活跃的网络连接，以便在安装过程中用于安装软件包，并将安装过程限制在文本模式下进行（尽管仍然可以安装图形桌面）。与桌面版和服务器版安装镜像不同，网络安装程序还允许选择不同的软件集合进行安装，从而对安装过程提供更大的控制，并产生一个配置更精细的操作系统。

## 5. 与 Windows 实现双启动 Ubuntu

Ubuntu 与绝大多数 Linux 发行版一样，可以很方便地与几乎任何版本的 Windows 共存在于硬盘驱动器上。这种概念被称为“双启动”。本质上，当你启动电脑时，将看到一个菜单，提供启动 Ubuntu 或 Windows 的选项。显显然，你一次只能运行一个操作系统，但值得注意的是，无论你的磁盘驱动器 Windows 分区是使用 NTFS、FAT16 还是 FAT32 格式格式化的，你都可以从 Ubuntu 访问磁盘驱动器上 Windows 分区中的文件。

在安装过程中，Ubuntu 安装程序将检测驱动器上的 Windows 安装，并提供删除它并将整个磁盘用于 Ubuntu，或与 Windows 共享磁盘的选项。在后一种情况下，你将指定用于 Ubuntu 的磁盘百分比。

根据 Ubuntu 文档，安装完整的 Ubuntu 桌面版至少需要 25 GB 的磁盘空间，以及更多的空间来存储你随后可能创建的任何文件。一旦选择了 Ubuntu 的磁盘空间，安装程序将调整 Windows 分区的大小（且不会破坏任何数据），并将磁盘的剩余部分用于 Ubuntu。

本章将演示如何设置 Ubuntu 和 Windows 10 的双启动系统，如何更改计算机系统启动时的默认启动系统，并概述如何从 Ubuntu 内部访问位于磁盘 Windows 分区上的文件。

在本章中，假设已遵循上一章中列出的步骤，使用 Ubuntu 桌面安装镜像创建了可启动的 Ubuntu 安装 USB 驱动器，并且系统已配置为启动时从 USB 驱动器启动。

### 5.1 开始安装 Ubuntu

要开始安装，插入 Ubuntu USB 驱动器并重启你的电脑系统。如果系统再次加载了 Windows，你将需要在系统设置中更改启动顺序。如何执行此操作的具体细节取决于系统，并在上一章中简要介绍过。

一旦 Ubuntu 加载，你将看到所示图 5-1 中的屏幕。

![](img/ubuntu_20.04_install_or_try1.jpg)

图 5-1

点击 `Install Ubuntu` 按钮开始安装，等待安装程序的初始屏幕出现，如图 5-2 所示：

![](img/ubuntu_20.04_install_keyboard_type1.jpg)

图 5-2

选择你的键盘布局，或者如果你不确定，点击 `Detect Keyboard Layout` 按钮，通过一些步骤来识别你的键盘，然后点击 `Continue`。在下一个屏幕上，选择执行“常规（Normal）”还是“最小化（Minimal）”安装：

![](img/ubuntu_20.04_install_type1.jpg)

图 5-3

如果你有足够的磁盘空间，并希望探索 Ubuntu 包含的主要应用程序和实用程序而无需稍后手动安装它们，请选择 `Normal` 选项，否则使用 `Minimal` 选项。

该选项还提供了在安装期间更新构成 Ubuntu 发行版的软件包的功能。如果选择了此选项且系统连接到互联网，安装程序将下载自 Ubuntu 安装镜像发布以来发布的任何更新，并在安装期间将它们应用到系统。如果你选择在安装过程中不进行此类更新，这些更新可能在安装完成后的任何时间仍然应用。

第二个选项提供了是否安装第三方非开源开源软件的选项，用以支持特定的硬件设备以及在系统上播放专有媒体文件。除非你倾向于避免使用非开源软件，否则建议使用此选项。

在做出适当选择后，点击 `Continue` 按钮进入磁盘分配屏幕。此时，安装程序将已检测到目标磁盘驱动器上存在现有 Windows 操作系统，并就如何使用磁盘来容纳 Ubuntu 安装提供多个选项：

![](img/ubuntu_20.04_install_with_windows.jpg)

图 5-4

考虑到我们的意图是配置双启动系统，`Install Ubuntu alongside Windows`（在 Windows 旁安装 Ubuntu）选项是理想的选择。选中此选项后，点击 `Continue` 按钮继续。随后的屏幕允许配置分配给每个操作系统（在此例中为 Windows 和 Ubuntu）的磁盘空间：

![](img/ubuntu_20.04_install_windows_disk_share.jpg)

图 5-5

此时，必须决定你希望将 Windows 分区的多少部分分配给 Ubuntu 安装。移动滑块（位于图中 Windows 和 Ubuntu 分区之间），直到 Ubuntu 分区的分配大小达到你感到舒适的程度。对于完整的 Ubuntu 桌面安装，至少应提供 25GB 的空间。

当你选定 Ubuntu 分区的大小后，点击 `Install Now` 按钮继续进行安装。当警告对话框出现时，仔细阅读，如果你确定要继续，请点击 `Continue`。

![](img/ubuntu_20.04_install_windows_write_changes.jpg)

图 5-6

安装进行过程中，安装程序将询问你的地理位置以配置时区设置：

![](img/ubuntu_20.04_install_where_are_you.jpg)

图 5-7

接下来，安装程序将要求为系统的第一个账户提供用户名和密码：

![](img/ubuntu_20.04_install_user_setup.jpg)

图 5-8

该选项还用于规定用户想要登录系统时是否必须指定密码。默认情况下，每次启动 Ubuntu 都会显示一个请求用户名和密码凭据的登录界面。如果你是系统的唯一用户，并希望跳过此屏幕并在每次系统启动时自动登录，请在继续之前勾选 `Log in automatically` 复选框。

一旦回答了所有问题，安装程序将继续安装。根据系统速度以及你是否选择在安装期间下载更新，此过程可能需要一段时间。要查看安装程序正在执行步骤的更详细视图，请点击进度条上方的标题：

![](img/ubuntu_20.04_install_details.jpg)

图 5-9

安装完成后，将出现对话框通知你系统准备好重启：

![](img/ubuntu_20.04_install_complete.jpg)

图 5-10

当你准备好重启时，按下 `Restart Now` 按钮。安装程序可能会提示移除安装介质，系统将关闭几秒钟。此时移除 USB 闪盘并按下 `Enter` 键继续。

### 5.2 首次启动 Ubuntu

当系统重启时，将出现类似下图所示的屏幕，提供启动 Windows 或 Ubuntu 的选项：

![](img/ubuntu_20.04_windows_boot.jpg)

图 5-11





按回车键启动 Ubuntu。如果您想启动 Windows，请使用键盘方向键选择 Windows 选项。如果您选择启动 Ubuntu，操作系统将加载并出现 Ubuntu 登录界面（除非选择了自动登录选项）。输入您在安装过程中设置的用户名和密码，您将登录到 Ubuntu 桌面环境。

### 5.3 更改默认启动选项

系统启动时，会出现启动选项屏幕，并等待 10 秒让用户选择操作系统。如果在超时结束前未进行任何选择，将启动默认操作系统。对于新配置的系统，默认操作系统将是标准的 Ubuntu 镜像。然而，这可以在 Ubuntu 内部更改此默认设置。

一系列启动配置选项（包括 10 秒超时和在 "在洁净硬盘驱动上安装 Ubuntu"中概述的启动设置）均可以在 `/etc/default/grub` 文件中声明，新安装时的该文件内容如下：

```
GRUB_DEFAULT=0
GRUB_TIMEOUT_STYLE=hidden
GRUB_TIMEOUT=10
GRUB_DISTRIBUTOR=`lsb_release -i -s 2> /dev/null || echo Debian`
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
GRUB_CMDLINE_LINUX=""
```

更改默认启动系统的第一步是在文件中声明 `GRUB_SAVEDEFAULT` 设置，并将 `GRUB_DEFAULT` 设置更改为 `saved`：

```
GRUB_DEFAULT=saved
GRUB_SAVEDEFAULT=true
GRUB_TIMEOUT_STYLE=hidden
GRUB_TIMEOUT=10
```

此设置允许在启动配置中保存一个新的默认值。接下来，运行 `grub-set-default` 命令，使用从 0 开始的第一个选项计数系统来更改默认设置。例如，如果 Windows 10 选项位于菜单的第 5 位，则将 Windows 10 设置为默认启动选项的命令将如下：

```bash
## grub-set-default 4
```

运行以下命令检查新设置是否生效：

```bash
## grub-editenv list
saved_entry=4
```

注意 `saved_entry` 的值现在已设置为 4。更改默认设置后，按照如下方式重新生成启动配置文件：

```bash
## grub-mkconfig --output=/boot/grub/grub.cfg
```

重启系统并验证启动菜单是否默认选择 Windows 10 选项，以及 Windows 在超时过期后是否加载。

### 5.4 从命令行访问 Windows 分区

在双引导配置下运行 Ubuntu 时，仍然可以访问位于 Windows 分区上的文件。这可以通过命令行手动挂载分区，或使用“磁盘”（`gnome-disks`）图形化工具从桌面挂载分区来实现。

在从命令行操作时，此过程的第一步是创建一个目录作为我们 Windows 分区的挂载点。在本例中，我们将创建一个名为 `/mnt/windows` 的目录：

```bash
## mkdir /mnt/windows
```

为了识别分配给 Windows 分区的设备名称，请如下所示使用 `fdisk` 命令：

```bash
## fdisk -l
```

```
Disk /dev/sda: 50 GiB, 53687091200 bytes, 104857600 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x7ef44412
Device Boot Start End Sectors Size Id Type
/dev/sda1 * 2048 1187839 1185792 579M 7 HPFS/NTFS/exFAT
/dev/sda2 1187840 59770533 58582694 28G 7 HPFS/NTFS/exFAT
/dev/sda3 59770878 104855551 45084674 21.5G 5 Extended
```

### 5.5 从桌面访问 Windows 分区

在双引导配置下运行 Ubuntu 时，仍然可以访问位于 Windows 分区上的文件。这可以通过命令行手动挂载分区，或使用“磁盘”（`gnome-disks`）图形化工具从桌面挂载分区来实现。

在从命令行操作时，此过程的第一步是创建一个目录作为我们 Windows 分区的挂载点。在本例中，我们将创建一个名为 `/mnt/windows` 的目录：

```bash
## mkdir /mnt/windows
```

为了识别分配给 Windows 分区的设备名称，请如下所示使用 `fdisk` 命令：

```bash
## fdisk -l
```

（为了简洁起见，省略剩余文本，逻辑相同……）

### 5.6 总结

通过创建双引导环境，Ubuntu 可以与 Windows 操作系统在同一硬盘器上安全共存。这涉及在安装期间缩小 Windows 系统占据的空间为 Ubuntu 腾出空间。一旦安装了 Ubuntu，就可以修改启动菜单配置来更改默认操作系统。硬盘驱动器上的 Windows 分区可以通过命令行或桌面磁盘工具从 Ubuntu 访问。




## 6.3 格式化未分配的磁盘分区

为了让新分区适用于 Ubuntu 使用，需要在其上创建文件系统。当前 Ubuntu 版本推荐的文件系统是 XFS，它将在“向 Ubuntu 系统添加新硬盘”章节中进行更详细的介绍。文件系统的创建使用 `mkfs.xfs` 命令执行如下（如有必要请安装 `xfsprogs` 包）：

```
apt install xfsprogs
mkfs.xfs /dev/sda1
```



接下来，我们需要挂载新分区。在本例中，我们将将其挂载到名为 `/data` 的目录中。不过，你也可以使用任何所需的有效挂载点来挂载新分区，或将其作为逻辑卷的一部分（详细信息请参阅向 Ubuntu 卷组和逻辑卷添加新磁盘 章节）。首先，我们需要创建一个目录作为挂载点：

```bash
mkdir /data
```

其次，我们需要编辑 `/etc/fstab` 中的文件挂载表，以便在每次系统启动时自动挂载该分区。在 `/etc/fstab` 文件的末尾添加以下行来挂载新分区（请修改 `/dev/sda1` 设备以匹配你的环境）：

```
/dev/sda1 /data xfs defaults 0 0
```

最后，我们可以手动挂载新分区（注意，在随后的重启中将不再需要这样做，因为由于我们在上面 `/etc/fstab` 文件中添加的设置，分区将自动挂载）。

```bash
mount /data
```

要检查分区，运行以下命令显示可用空间：

```bash
df -h /data
```

Filesystem Size Used Avail Use% Mounted on

/dev/sda1 29G 62M 29G 1% /data

## 6.5 编辑启动菜单

下一步是修改 Ubuntu 启动菜单。由于这最初是一个双启动系统，因此菜单被配置为提供启动 Windows 或 Ubuntu 的选项。现在 Windows 分区已经删除，我们需要删除此启动选项。在 Ubuntu 上，可以通过运行如下的 `update-grub` 命令来实现这一点：

```bash
update-grub
```

```
Sourcing file `/etc/default/grub`

Generating grub configuration file ...

Found linux image: /boot/vmlinuz-5.3.0-42-generic

Found initrd image: /boot/initrd.img-5.3.0-42-generic

Found linux image: /boot/vmlinuz-5.3.0-28-generic

Found initrd image: /boot/initrd.img-5.3.0-28-generic

Found memtest86+ image: /boot/memtest86+.elf

Found memtest86+ image: /boot/memtest86+.bin
```

由于现在只有一个操作系统需要启动，系统将在下次重启时自动启动 Ubuntu，而不会显示启动菜单。如果你需要访问此启动菜单（例如使用高级启动选项），只需在启动过程的初始阶段按下 Esc 键即可。

## 6.6 使用 GNOME 磁盘 ks 工具

`gnome-disks` 工具提供了一个用户友好的图形界面方案，用于从命令行恢复 Windows 分区。由于此处使用的示例将把 Windows NTFS 分区转换为 XFS 格式，第一步是按照如下安装 `xfsprogs` 包：

```bash
apt install xfsprogs
```

安装包后，打开终端窗口并启动 `gnome-disks` 工具：

```bash
gnome-disks
```

稍等片刻，`gnome-disks` 工具将如图 6-1 所示：

![](img/ubuntu_20.04_windows_partition_mounted.jpg)

图 6-1

在上面的示例中，磁盘包含两个需要删除的 Windows NTFS 分区。磁盘图中显示带有星号的任何 NTFS 分区（如上图高亮分区所示）在删除之前都需要先卸载。这可以通过选择分区并点击卸载按钮来实现，如译文的图 6-2 所示：

![](img/ubuntu_20.04_windows_partition_unmount_button.jpg)

图 6-2

所有 NTFS 分区都卸载后，下一步是删除它们。选择磁盘图中左侧的分区，并点击如图 6-3 所示的删除按钮：

![](img/ubuntu_20.04_gnome-disks_delete_partition.jpg)

图 6-3

在点击删除按钮提交更改之前，请检查确认对话框中的信息。一旦删除了第一个分区，对任何剩余的 NTFS 分区重复此步骤。

一旦删除了 NTFS 分区，磁盘图中的空间应该显示为空闲。

现在需要创建一个新分区来利用这些空闲空间。选中空间后，点击新分区按钮（如图 6-4 所示）：

![](img/ubuntu_20.04_gnome-disks_new_partition_button.jpg)

图 6-4

在“创建分区”对话框中，选择分区是否占用所有可用空间，或者如果你计划将该空间用于多个分区，则减小尺寸：

![](img/ubuntu_20.04_gnome-disks_create_partition.jpg)

图 6-5

点击下一步，在随后的屏幕上，为新分区命名，并选择分区是否应该格式化。文件系统类型通常为 ext4 或 XFS。由于我们要使用 XFS，选择 XFS 后点击下一步：

![](img/ubuntu_20.04_gnome-disks_format.jpg)

图 6-6

如果 XFS 选项被禁用，请退出。`gnome-disks` 工具将开始格式化过程并显示状态：由于 XFS 的用处，选择 Other 后点击创建按钮：

![](img/ubuntu_20.04_gnome-disks_create.jpg)

图 6-7

一旦分区准备就绪，可以通过命令行或使用 `gnome-disks` 进行挂载。要配置挂载点，选择分区并点击如图 6-9 所示的设置按钮：

![](img/ubuntu_20.04_gnome-disks_settings.jpg)

图 6-9

从设置菜单中选择编辑挂载选项项以显示如图 6-10 所示的对话框：

![](img/ubuntu_20.04_gnome-mount_options.jpg)

图 6-10

关闭用户会话开关并根据你的配置挂载点。在上面的图中，分区在启动时挂载并标识为“Data”。

设置完成后，点击 OK。该卷已挂载并可以使用：

```bash
$ df -h /data
```

Filesystem Size Used Avail Use% Mounted on

/dev/sda1 29G 62M 29G 1% /data
```

最后，按照上述第 6.5 节的说明更新启动菜单以移除 Windows。

## 6.7 总结

双启动配置中的 Windows 分区可以随时删除，为 Ubuntu 系统腾出空间。删除后，可以使用空闲空间创建新的文件系统并进行挂载以供 Ubuntu 系统使用。最后的任务是从启动菜单中删除 Windows 选项。这些任务可以通过命令行使用 fdisk 完成，也可以在桌面环境中使用 gnome-disks 完成。

## 7 GNOME 3 桌面导览

Ubuntu 20.04 包含了 GNOME 3 桌面环境。虽然不像 Windows 和 macOS 桌面复杂，但 GNOME 3 提供了一个简洁且直观的桌面环境，提供了窗口环境的所有基本功能，优点是易于学习。

在本章中，我们将涵盖 GNOME 桌面的主要功能，并概述如何执行基本任务。

### 7.1 安装 GNOME 桌面

如果在安装 Ubuntu 20.04 的过程中使用了 Ubuntu Desktop 镜像，则 GNOME 桌面已经安装，并在每次系统启动时都会自动启动。





如果在 Ubuntu 20.04 安装过程中选择了任何其他软件配置，则系统安装的软件包中将不包含 GNOME 桌面。对于没有连接显示器的服务器系统，安装图形化桌面环境的想法可能看起来是多余的。然而，值得注意的是，远程访问 GNOME 桌面也是可行的，因此即使在所谓的“无头服务器”（即缺少显示器、键盘和鼠标的服务器）上，安装 GNOME 桌面软件包可能仍有益益。关于建立远程桌面访问的话题将在本书的后续章节中详细介绍。

如果安装配置未包含 GNOME 桌面，可以随时使用以下命令进行安装：

```bash
apt install tasksel
tasksel install ubuntu-desktop
```

安装完成后，系统下次重启时将出现桌面登录界面。

### 7.2 GNOME 3 桌面概览

下方的图 7-1 所示屏幕显示了在启动任何其他程序或进行配置更改之前，典型的新启动 GNOME 桌面会话的外观：

![](img/ubuntu_20.04_ubuntu_desktop.jpg)
图 7-1

主桌面区域（标记为 A）是启动应用程序和工具时窗口出现的地方。

屏幕顶部的栏（B）称为顶栏（top bar），它包含活动菜单（C）、日期和时间，以及一组按钮和图标，包括网络状态、音频量、电池电量以及其他状态账户设置。当前运行在桌面上的活动应用程序的菜单也会出现在顶栏中。例如，图 7-2 显示了 `Terminal` 程序的应用程序菜单：

![](img/ubuntu_20.04_gnome_desktop_terminal_menu.jpg)
图 7-2

### 7.3 启动活动

应用程序和工具通过“活动”概览仪表板（称为 dash）启动，可以通过点击顶栏中的“活动”（Activities）按钮或按下键盘上的特殊键来显示它。在 Windows 键盘上，该键是 Windows 键；在 macOS 上是 Command 键；在 Chromebook 上是显示放大镜的键。

显示时，dash 将如图 7-3 所示：

![](img/ubuntu_20.04_gnome_desktop_dash.jpg)
图 7-3

默认情况下，dash 将显示一组预定义的常用应用程序的图标，并包含任何当前运行的应用程序的图标。如果应用程序正在运行，它将在图标左侧显示带有一个圆点标记；如果运行了多个副本，则每个实例都会显示一个圆点。

要启动应用程序，只需点击 dash 中的图标即可。

要找到 dash 中未包含的应用程序，一种方法是选择最底部的图标（由九个点组成的正方形）来显示可浏览的应用程序列表，如图 7-4 所示：

![](img/ubuntu_20.04_gnome_desktop_app_list.jpg)
图 7-4

注意，可以通过选择屏幕底部中央的按钮来过滤列表，显示所有应用程序或仅显示频繁使用的应用程序。此外，要意识到列表中的某些条目实际上是存放其他应用程序的文件夹。

浏览应用程序的另一种方法是使用搜索栏进行搜索，点击“活动”菜单时会显示搜索栏，如图 7-5 所示：

![](img/ubuntu_20.04_gnome_desktop_search.jpg)
图 7-5

随着在搜索框中输入文本，可能的匹配列表将不断精简。

为了更方便地访问将应用程序添加到 dash，找到该应用程序的图标，右键点击它并选择 `Add to Favorites`（添加到收藏）菜单选项：

![](img/ubuntu_20.04_gnome_desktop_add_to_favorites.jpg)
图 7-6

要从 dash 中移除应用，右键点击 dash 中的图标并选择 `Remove from Favorites`（从收藏中移除）。

### 7.4 管理窗口

与其他桌面环境一样，在 GNOME 上运行的应用程序都在窗口中。当打开多个应用程序窗口时，使用 `Super + Tab` 键盘快捷键将显示切换面板（图 7-7），允许选择不同的窗口作为当前活动窗口（`Super` 键是 Windows 键，或者在 Mac 键盘上是 `Cmd` 键）：

![](img/ubuntu_20.04_gnome_desktop_tasks.jpg)
图 7-7

要在切换器中的图标之间反向循环，请使用 `Shift + Tab` 键盘快捷键。

要最大化窗口以填充整个屏幕，点击标题栏并将窗口拖动到屏幕顶部。要将窗口恢复原始大小，点击标题栏并向下拖动。或者，只需双击标题栏即可在窗口大小之间切换。同样，将窗口拖到屏幕的左侧或右侧将使窗口填充屏幕的半部分。

### 7.5 使用工作区

显示应用程序窗口的区域被称为工作区（workspace），GNOME 3 允许配置多个工作区。要创建一个新的工作区，显示“活动”概览并将指针移动到屏幕右侧显示工作区面板：

![](img/ubuntu_20.04_gnome_desktop_workspaces.jpg)
图 7-8

要切换到不同的面板，只需从列表中选择。要将窗口从一个工作区移动到另一个，显示工作区面板并将应用程序窗口（当前工作区的实际窗口或工作区面板中的缩图）拖放到目标工作区。当窗口被添加到空白工作区时，工作区面板会添加一个新的空白工作区，从而创建多个工作区。要删除工作区，请关闭该工作区的所有窗口，或将其移动到另一个工作区。

### 7.6 日历与通知

当系统需要通知您事件（例如系统或应用程序更新）时，顶部会出现一个弹出面板。点击顶栏中的日期和时间可以访问日历和任何之前的通知，如图 7-9 所示：

![](img/ubuntu_20.04_gnome_desktop_calendar.jpg)
图 7-9

### 7.7 桌面设置

要访问设置应用程序，点击顶栏最右侧的箭头，并选择图 7-10 所示工具图标按钮：

![](img/ubuntu_20.04_gnome_desktop_control_panel.jpg)
图 7-10

设置应用程序提供了广泛的选项，例如以太网和 WiFi 连接、屏幕背景自定义选项、屏幕锁定和电源管理控制以及语言偏好。要探索每个类别中的可用设置，只需从设置窗口左侧面板选择一个选项：

![](img/ubuntu_20.04_gnome_desktop_settings.jpg)
图 7-11

上述[图 7-10]所示的菜单还包括切换用户、调整音量、切换到不同的 WiFi 网络以及注销、重启或关机选项。

### 7.8 定制 dash

dash（也称为 dock）的大小、位置和行为可以在设置应用中通过选择`Appearance`选项更改，如图 7-12 所示：

![](img/ubuntu_20.04_gnome_desktop_dock_settings.jpg)
图 7-12




位置可以设置为屏幕的四边之一，同时 `Icon` 大小可用于减小 dock 栏的大小。最后如果启用了 `auto-hide` dock 选项，dock 栏将从视图中隐藏，直到鼠标指针移动到它当前所在的屏幕边缘。

### 7.9 切换到深色模式

除了提供 dock 设置外，`Settings` 应用的 `Appearance` 面板还允许在亮色、标准和深色模式之间切换桌面。例如，图 7-13 显示了深色模式：

![](img/ubuntu_20.04_gnome_desktop_dark_mode.jpg)

图 7-13

### 7.10 安装 Ubuntu 

与 macOS、Windows、iOS 和 Android 等其他操作系统相同，Ubuntu 拥有以 `Ubuntu Software` 工具形式存在的“应用商店”。图标通常放置在 dash 中，如图 7-14 所示：

![](img/ubuntu_20.04_gnome_desktop_ubuntu_software_icon.jpg)

图 7-14

一旦加载，该工具将提供一个可在系统上安装的应用程序列表，并根据类别、推荐和编辑精选进行分组。也可以对可用应用程序库进行搜索以查找特定项目：

![](img/ubuntu_20.04_gnome_desktop_ubuntu_software.jpg)

图 7-15

要安装应用程序，只需在 `Ubuntu Software` 窗口中选择它并点击 `Install` 按钮：

![](img/ubuntu_20.04_gnome_desktop_install_software.jpg)

图 7-16

### 7.11 基础自定义之外

`GNOME 3` 桌面在设计上是一个简洁且不杂乱的环境，自定义选项极少。然而，这并不意味着无法对桌面进行额外的更改。事实上，`GNOME Project` 开发了一个名为 `GNOME Tweaks` 的工具专门用于实现这一目的。请使用以下命令安装并运行该工具：

```
apt install gnome-tweaks
```

```
gnome-tweaks
```

一旦 `GNOME Tweaks` 加载，将出现图 7-17 所示的界面：

![](img/ubuntu_20.04_gnome_tweaks.jpg)

图 7-17

现在提供了广泛的桌面自定义选项。事实上，选项多到在本章中无法涵盖，因此请在进入下一章之前花些时间尝试这些设置。

### 7.12 总结

Ubuntu 包含了 `GNOME 3` 桌面环境，该环境可以在初始期间包含，也可以在之后使用 `tasksel` 命令行工具安装。与大多数其他桌面环境不同，`GNOME 3` 旨在提供一个简洁且易用的窗口用户界面。`GNOME 3` 桌面的关键区域包括顶栏、`Activities` 概述和 dash。此外，`GNOME 3` 支持多个工作空间，使运行中的应用程序保持整齐，屏幕整洁。`Settings` 应用中还有多种配置选项，包括桌面背景设置、音频、网络配置和 WiFi 网络选择。

## 8. Ubuntu Cockpit Web 界面概述

尽管 Ubuntu 配备最新的 Linux 桌面环境，但它很大程度上是一个服务器操作系统，因此大多数 Ubuntu 部署要么是远程物理服务器，要么是云端虚拟机实例。不可避免的是，这些系统在没有键盘、鼠标或显示器的情况下运行，仅可以通过网络连接上的命令行提示符直接访问。这在从远程位置管理系统方面带来了挑战。虽然通过远程访问命令行和桌面环境确实可以实现很多，但对于像 Ubuntu 这样的企业级操作系统上每天需要执行的管理和监控任务来说，这远不是一个一致且统一的解决方案。

这个问题通过引入 `Cockpit` 基于 Web 的管理界面得到了解决。本章将解释如何安装、配置和访问 `Cockpit` 界面，同时还将提供 `Cockpit` 关键功能的概述，其中许多功能将在后面的章节中进行更详细的介绍。

### 8.1 Cockpit 概述

`Cockpit` 是一个量级的基于 Web 的界面，允许远程执行常规系统管理任务。安装并配置后，系统管理员只需打开本地浏览器窗口并导航到远程服务器上的 `Cockpit` 端口。在浏览器中加载 `Cockpit` 界面并登录后，可以使用管理和监控工具以视觉化方式执行广泛的任务。

在后台，`Cockpit` 使用与在命令行工作时相同的工具执行任务，并自动更新以反映系统其他处发生的变化。这允许 `Cockpit` 与其他管理工具和技术结合使用，而没有一种方法覆盖另一种方法的的风险。`Cockpit` 还可以配置为访问多个服务器，允许通过单个浏览器会话同时管理和监控多个服务器。

`Cockpit` 默认安装并已捆绑了一系列工具。然而，`Cockpit` 也允许根据需要安装额外的扩展插件。`Cockpit` 的设计还允许你结合 `HTML` 和 `JavaScript` 创建自己的扩展，以添加缺失或自定义机功能。

`Cockpit` 的模块化设计还允许许多功能嵌入到其他基于 Web 的应用程序中。

### 8.2 安装并启用 Cockpit

Ubuntu 默认不安装 `Cockpit`，但可以通过几个简单的步骤进行设置和启用。第一步按照如下方式安装 `Cockpit` 包：

```
apt install cockpit
```

接下来，需要启用 `Cockpit` 套字服务：

```
systemctl enable --now cockpit.socket
```

最后，如果你的系统启用了防火墙，则需要在防火墙上打开必要的端口，以允许远程浏览器连接到达 `Cockpit`（有关防火墙的详情，请参考章节 Ubuntu Firewall Basics）。

如果启用了 `ufw`：

```
ufw allow 9090
```

如果启用了 `firewalld`：

```
firewall-cmd --add-service=cockpit --permanent
firewall-cmd --reload
```

### 8.3 访问 Cockpit

如果你可以访问安装了 `Cockpit` 的服务器桌面环境，请打开浏览器窗口并导航到 `https://localhost:9090` 以访问 `Cockpit` 登录屏幕。如果服务器是远程的，只需使用域名或 IP 地址访问服务器（例如 `https://myserver.com:9090`）。

建立连接时，浏览器可能会发出连接安全的警告。这是因为 `Cockpit` 服务使用了自签名证书。可以选择继续访问网站，或者为了以后避免此消息，可以选择高级选项并为服务器地址添加异常。

连接后，浏览器将加载下方图 8-1 所示的登录页面：

![](img/ubuntu_20.04_cockpit_login.jpg)

图 8-1

使用 `root` 或你的用户账户凭据登录 `Cockpit` 界面。请注意，以用户身份登录时，除非你在登录前启用“使用我的密码执行特权任务”选项，否则 `Cockpit` 界面中的某些任务将受到权限限制。登登录后，`Cockpit` 将显示 `System` 屏幕。

### 8.4 概述

`Overview` 屏幕提供了当前系统的概述，包括 `CPU` 和 `memory` 的实时性能指标。此屏幕还包含系统信息，包括底层硬件、主机名、系统时间以及系统软件是否已为最新版本。还提供了重启或关机系统的选项。




例如，图 8-2 显示了 Cockpit 界面的概览页：

![](img/ubuntu_20.04_cockpit_overview.jpg)

图 8-2

要获取特定分类分类信息，请点击相应的链接。例如，图 8-3 显示了系统使用图：

![](img/ubuntu_20.04_cockpit_usage_graphs.jpg)

图 8-3

## 8.5 日志

选择 `Logs`（日志）类别时，Cockpit 会显示 `systemd` 日志的内容。选择一个日志条目将显示整个日志消息。日志条目按顺序排序，最新的在最上方，并包含菜单用于根据不同的时间段和消息严重程度过滤日志。

![](img/ubuntu_20.04_cockpit_logs.jpg)

图 8-4

## 8.6 存储

选择 `Storage`（存储）选项可以查看和管理系统上的存储，包括磁盘、分区和卷组、网络文件系统 (NFS) 挂载以及 RAID 存储。此屏幕还可以实时监控磁盘 I/O 活动，并列出用于查询和管理存储设备的系统 `udisksd` 服务日志输出。

![](img/ubuntu_20.04_cockpit_storage.jpg)

图 8-5

## 8.7 网络

`Networking`（网络）屏幕提供了各种网络相关配置和服务的信息，包括网络接口和防火墙设置，并允许进行配置更改，例如创建网桥或设置虚拟网络。

![](img/ubuntu_20.04_cockpit_networking.jpg)

图 8-6

## 8.8 账户

选择此选项可查看系统上配置的当前用户账户，并为额外用户创建账户。用户管理主题将在本章名为管理 Ubuntu 用户和组的章节中介绍。

![](img/ubuntu_20.04_cockpit_accounts.jpg)

图 8-7

点击现有账户查看详情并进行更改。用户账户详情页还可用于查看并向用户的账户添加公共 SSH 密钥，以便远程访问服务器，正如名为在 Ubuntu 上配置基于 SSH 密钥的身份验证的章节概述所示。

## 8.9 服务

此屏幕显示运行在服务器上的系统服务列表，并允许对这些服务进行添加、删除、停止和启动。

![](img/ubuntu_20.04_cockpit_services.jpg)

图 8-8

服务主题将在名为管理 Ubuntu systemd 单元的章节中详细介绍。

## 8.10 应用程序

如前所述，可以通过扩展的形式向 Cockpit 添加额外的功能。这些扩展可以是自主开发的扩展，也可以是第三方提供的。`Applications`（应用程序）屏幕列出了已安装的扩展，并允许添加或删除扩展。

![](img/ubuntu_20.04_cockpit_applications.jpg)

图 8-9

如果 cockpit 界面中没有可用的 `Applications` 选项，可以通过以下方式安装：

```
apt install cockpit-packagekit
```

## 8.11 虚拟机

虚拟化允许多个操作系统实例同时在单台计算机系统上运行，每个系统运行在自己的虚拟机内部。`Virtual Machines`（虚拟机）Cockpit 扩展提供了一种创建和管理安装在服务器上的虚拟机客户的方法。

![](img/ubuntu_20.04_cockpit_machines.jpg)

图 8-10

`Virtual Machines` 扩展默认不安装，但可以通过 Cockpit `Applications` 屏幕或运行以下命令进行添加：

```
apt install cockpit-machines
```

在 Ubuntu 中使用虚拟化从名为虚拟化技术概述的章节开始介绍。

## 8.12 软件更新

如果系统有任何可用软件更新，它们将列在此屏幕上。如果有可用更新，可以从此屏幕进行安装：

![](img/ubuntu_20.04_cockpit_updates.jpg)

图 8-11

如果不可用 `Cockpit Software Updates` 屏幕，可以通过以下方式安装：

```
apt install cockpit-packagekit
```

## 8.13 终端

顾其实名，`Terminal`（终端）屏幕提供了命令行提示符的访问。

![](img/ubuntu_20.04_cockpit_terminal.jpg)

图 8-12

## 8.14 连接到多个服务器

可以将 Cockpit 配置为在单个会话中管理多个服务器。这要求在主系统（即建立初始 Cockpit 会话的系统）上安装 dashboard。如果尚未安装仪表板，请运行以下命令：

```
apt install cockpit-dashboard
```

一旦安装了仪表板，请退出 Cockpit 然后重新登录。仪表板现在出现在 Cockpit 界面中，如图 8-13 所示：

![](img/ubuntu_18.04_cockpit_dashboard_tab.jpg)

图 8-13

选中仪表板页面将显示当前系统的性能图，并提供已连接系统的列表：

![](img/ubuntu_20.04_cockpit_dashboard.jpg)

图 8-14

要添加另一个系统，请点击图 8-14 所示的 `+` 按钮，输入另一个系统的 IP 地址或主机名，并选择一种颜色以区分服务器，然后点击添加：

![](img/ubuntu_20.04_cockpit_dashboard_add.jpg)

图 8-15

输入连接其他系统时使用的用户名密码，然后点击登录。新添加的服务器现在将出现在列表中并以之前的颜色显示：

![](img/ubuntu_20.04_cockpit_two_systems.jpg)

图 8-16

在使用 Cockpit 切换系统时，只需使用下方图 8-17 所示的下拉菜单：

![](img/ubuntu_20.04_cockpit_select_system.jpg)

图 8-17

## 8.15 总结

Cockpit 界面允许在浏览器中执行远程系统管理任务，而无需依赖命令行提示符和工具。一旦安装并启用，系统管理员只需打开浏览器、连接到远程服务器并登录 Cockpit。在后台，Cockpit 使用与通过命令行提示符提供的相同的工具，允许使用两种选项而不产生配置冲突风险。Cockpit 使用模块化框架，允许添加额外的扩展，并开发和集成自定义扩展。Cockpit 会话可以用于管理单个服务器，也可以配置为访问多个服务器。

## 9 在 Ubuntu 上使用 Bash Shell

学习 Ubuntu（以及一般的 Linux 发行版）的重要部分是熟练使用 shell 环境。虽然 Linux 包含的 GNOME 等图形桌面环境提供了友好的操作系统界面，但在实践中，shell 环境提供了比使用图形桌面工具实现的得多的功能、灵活性自动化。shell 环境还提供了在没有桌面环境的情况下与操作系统交互的方法；这在处理 Ubuntu 这类基于服务器的操作系统或无法完全启动的损坏系统时很常见。

因此，本章的目标是概述 Ubuntu 上默认的 shell 环境（特别是 Bash shell）。

### 9.1 什么是 Shell？




Shell 是一个交互式命令解释器环境，用户可以在提示符处输入命令，也可以以脚本的形式将命令写入文件并进行执行。Shell 的起源可以追溯到 UNIX 操作系统的早期。事实上，在 Linux 引入图形化桌面之前的早期，Shell 是用户与操作系统交互的唯一方式。

多年来，人们开发了多种 Shell 环境。第一个被广泛使用的 Shell 是由贝尔实验室的 Stephen Bourne 编写的 `Bourne shell`。

另一个早期产物是 `C shell`，它与 `C 编程语言` 在语法上具有某些相似之处，并引入了如命令行编辑和历史记录等易用性增强功能。

`Korn shell`（由贝尔实验室的 David Korn 开发）基于了 `Bourne shell` 和 `C shell` 提供的特性。

Ubuntu 默认的 Shell 是 `Bash shell`（`Bourne Again SHell` 的缩写）。该 Shell `Bash` 起初是 `Bourne shell` 的一个开源版本，由 Brian Fox 为 `GNU Project` 开发，并基于 `Bourne shell` 和 `C shell` 提供的特性。

### 9.2 获取 Shell 的访问权限

在 GNOME 桌面环境中，可以通过 `Terminal` 窗口访问 Shell 提示符，方法是选择顶部栏中的 `Activities`（活动）选项，在搜索栏中输入 `Terminal` 并点击 `Terminal` 图标。

在远程登录 Ubuntu 服务器时（例如使用 `SSH`），用户也会看到一个 Shell 提示符。关于使用 `SSH` 访问远程服务器的细节将在标题为在 Ubuntu 上配置基于密钥的身份验证的章节中介绍。在启动未安装桌面环境的服务器系统时，用户在物理控制台终端或远程登录话完成登录程序后，会立即进入 Shell。

### 9.3 在提示符处输入命令

在 Shell 命令提示符处，只需输入命令并按回车键即可输入。虽然某些命令会静默执行任务，但大多数命令在返回提示符之前都会显示某种形式的输出。例如，`ls` 命令可以显示当前工作目录下的文件和目录：

```
$ ls
Desktop Documents Downloads Pictures Public Templates Videos
```

可用的命令要么内置在 Shell 内部，要么位于物理文件系统中。可以使用 `which` 命令识别命令在文件系统中的位置。例如，要查找 `ls` 可执行文件在文件系统中的位置：

```
$ which ls
alias ls=’ls --color=auto’
/usr/bin/ls
```

显然，`ls` 命令位于 `/usr/bin` 目录。另注意还配置了 `alias`（别名），该主题将在本章稍后部分介绍。使用 `which` 命令定位内置于 Shell 的命令路径将导致一条显示找不到可执行文件的消息。例如，尝试查找 `history` 命令的位置（它实际上是内置在 Shell 中的，而不是作为文件系统上的可执行文件存在），将产生类似下面的输出：

```
$ which history
/usr/bin/which: no history in (/home/demo/.local/bin:/home/demo/bin:/home/share/Modules/bin:/home/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin)
```

### 9.4 获取有关命令的信息

Linux Shell 的许多命令起初看起来可能晦涩难懂。要查找有关某个命令的作用以及如何使用的详细信息，请使用 `man` 命令并将命令名称作为参数。例如，要了解更多关于 `pwd` 命令的信息：

```
$ man pwd
```

当执行上述命令时，将显示 `pwd` 命令的详细描述。许多命令在带有 `--help` 命令行选项运行时也会提供额外信息：

```
$ wc --help
```

### 9.5 Bash 命令行编辑

早期的 Shell 环境不提供任何形式的行（line editing）能力。这意味着如果你在正在输入的长命令行开头发现错误，你必须删除之后的所有字符，纠正错误然后重新输入命令的剩余部分。幸运的是，`Bash` 提供了丰富的命令行编辑选项，如下表所示：

| 组合键序列 | 动作 |
| --- | --- |
| `Ctrl-b` 或 `左箭头` | 将光标向后移动一位 |
| `Ctrl-f` 或 `右箭头` | 将光标向前移动一位 |
| `Delete` | 删除当前光标下方的字符 |
| `Backspace` | 删除光标左侧的字符 |
| `Ctrl-_` | 撤销上一次更改（可以重复操作以撤销所有之前的更改） |
| `Ctrl-a` | 将光标移动到行首 |
| `Ctrl-e` | 将光标移动到行尾 |
| `Meta-f` 或 `Esc` 然后 `f` | 将光标向前移动一个单词 |
| `Meta-b` 或 `Esc` 然后 `b` | 将光标向后移动一个单词 |
| `Ctrl-l` | 清除当前命令以外的所有屏幕内容 |
| `Ctrl-k` | 从当前光标位置删除到行尾 |
| `Meta-d` 或 `Esc` 然后 `d` | 删除到当前单词结束 |
| `Meta-DEL` 或 `Esc` 然后 `DEL` | 删除开头到当前单词 |
| `Ctrl-w` | 从当前光标位置删除到上一个空格 |

表 9-1

### 9.6 使用 Shell 历史记录

除了命令行编辑功能外，`Bash shell` 还提供了命令历史支持。可以使用 `history` 命令查看已执行的命令列表：

```
$ history
    1 ps
    2 ls
    3 ls –l
    4 ls
    5 man pwd
    6 apropos
```

此外，可以使用 `Ctrl-p`（或 `上箭头`）和 `Ctrl-n`（或 `下箭头`）在历史命令之间滚动。当显示出所需的历史命令时，按回车键执行。

另一种选项是输入 `!` 字符，后跟要重复命令的前几个字符，然后按回车键。

### 9.7 文件名简写

许多 Shell 命令接受一个或多个文件名作为参数。例如，要显示名为 `list.txt` 的文本文件的内容，可以使用 `cat` 命令：

```
$ cat list.txt
```

同样，可以通过指定所有文件名作为参数来显示多个文本文件的内容：

```
$ cat list.txt list2.txt list3.txt list4.txt
```

与其输入每个名称，可以使用模式匹配来指定符合某些标准的文件。例如，可以使用 `*` 通配符来简化上面的示例：

```
$ cat *.txt
```

上述命令将显示所有以 `.txt` 结尾的文件内容。这可以进一步限制为以 `list` 开头并以 `.txt` 结尾的文件：

```
$ cat list*.txt
```

可以使用 `?` 字符指定单字符匹配：

```
$ cat list?.txt
```

### 9.8 文件名和路径补全

与其输入整个文件名或路径，或使用模式匹配来减少输入，Shell 提供了文件名补全功能。要使用文件名补全，只需输入文件名或路径的前几个字符，然后双击 `Esc` 键。Shell 将根据你输入的字符为你补全目录中第一个匹配的文件名或路径。输入前几个字符后按 `Esc` 获取可能的匹配列表。

### 9.9 输入和输出重定向

如前所述，许多 Shell 命令在执行时会输出信息。默认情况下，这些输出去向名为 `stdout` 的设备文件，这本质上是运行 Shell 的终端窗口或控制台。相反，Shell 从名为 `stdin` 的设备文件获取输入，默认情况下是键盘。




可以使用 `>` 字符将命令的输出从标准输出（stdout）重定向到文件系统的物理文件。例如，要将 `ls` 命令的输出重定向到名为 `files.txt` 的文件，需要以下命令：

```bash
ls *.txt > files.txt
```

完成后，`files.txt` 将包含当前目录下的文件列表。同样，可以将文件的内容作为标准输入（stdin）馈给命令。例如，要将文件的内容重定向为作为命令的输入：

```bash
wc –l < files.txt
```

上述命令将显示 `files.txt` 文件包含的行数。

需要注意的是，`>` 重定向操作符在使用时会创建一个新文件，或者截断现有文件。若要向现有文件追加内容，请使用 `>>` 操作符：

```bash
ls *.dat >> files.txt
```

除了标准输出外，shell 还通过 `stderr` 提供了标准错误输出。当命令的输出重定向到 `stdout` 时，命令生成的任何错误消息都将重定向到 `stderr`。这意味着如果 `stdout` 被重定向到文件，错误消息仍然会显示在终端中。这通常是期望的行为，尽管如果需要，也可以使用 `2>` 操作符重定向 `stderr`：

```bash
ls dkjfnvkjdnf 2> errormsg
```

命令执行完成后，一个报告找不到名为 `dkjfnvkjdnf` 文件的错误将包含在 `errormsg` 文件中。

可以使用 `&>` 操作符将 `stderr` 和 `stdout` 同时重定向到同一个文件：

```bash
ls /etc dkjfnvkjdnf &> alloutput
```

执行完成后，`alloutput` 文件将包含 `/etc` 目录内容的列表，以及与尝试列出不存在的文件相关的错误消息。

### 9.10 在 Bash Shell 中使用管道

除了 I/O 重定向外，shell 还允许将一个命令的输出直接通过管道作为另一个命令的输入。通过在命令行中的两个或多个命令之间放置 `|` 字符来实现管道操作。例如，要统计系统上运行的进程数，可以将 `ps` 命令的输出管道传递给 `wc` 命令：

```bash
ps –ef | wc –l
```

命令行上可以执行的管道操作数量没有限制。例如，要找到文件中包含名称 "Smith" 的行数：

```bash
cat namesfile | grep Smith | wc –l
```

### 9.11 配置别名 (Aliases)

随着你对 shell 环境越来越熟练，你可能会发现自己频繁执行带有相同参数的命令。例如，你可能经常带有 `l` 和 `t` 使用 `ls` 命令：

```bash
ls –lt
```

为了减少执行命令时的打字量，可以创建一个映射到命令和参数的别名。例如，要创建一个别名，使得输入字母 `l` 就会执行 `ls –lt` 命令，可以使用以下语句：

```bash
alias l="ls –lt"
```

现在在命令提示符输入 `l` 将执行原始语句。

### 9.12 环境变量

Shell 环境变量提供了数据和配置设置的临时存储。shell 本身设置了一些环境变量，用户可以更改这些变量来修改 shell 的行为。可以使用 `env` 命令获取当前定义的变量列表：

```bash
env
SSH_CONNECTION=192.168.0.1 61231 192.168.0.28 22
MODULES_RUN_QUARANTINE=LD_LIBRARY_PATH
LANG=en_US.UTF-8
HISTCONTROL=ignoredups
HOSTNAME=demo-pc.ebookfrenzy.com
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

也许最有用的环境变量是 `PATH`。它定义了 shell 搜索命令提示符处输入的命令的目录，以及搜索的顺序。新安装的 Ubuntu 系统上用户账户的 `PATH` 环境变量可能配置如下：

```bash
echo $PATH
/home/demo/.local/bin:/home/demo/bin:/usr/share/Modules/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin
```

另一个有用变量是 `HOME`，它指定了当前用户的家目录。例如，如果你想让 shell 在你家目录下的 scripts 目录中查找命令，你可以如下所示修改 `PATH` 变量：

```bash
export PATH=$PATH:$HOME/scripts
```

可以使用 `echo` 命令显示现有环境变量的当前值：

```bash
echo $PATH
```

你可以使用 `export` 命令创建自己的环境变量。例如：

```bash
export DATAPATH=/data
```

一个实用的技巧是使用反引号将命令的输出赋值给环境变量。例如，将当前日期时间赋值给名为 `NOW` 的环境变量：

```bash
export NOW=`date`
echo $NOW
Tue Apr 2 13:48:40 EDT 2020
```

### 9.13 编写脚本

到为止，我们一直关注 shell 的交互性。交互意味着在提示符处逐个输入命令。事实上，这只是 shell 能力的一小部分。可以说 shell 最强大的方面之一是创建脚本。脚本本质上是包含可以在 shell 中执行的语句序列的文本文件。除了执行命令的能力，shell 还提供了许多编程结构，如 `for` 和 `do` 循环以及 `if` 语句，你可以在脚本语言中发现它们。

遗憾的是，对脚本的详细概述超出了本章的范围。然而，有很多专门介绍脚本的书籍和网络资源可以更好地介绍该主题。因此，在本节中，我们仅提供简单的尝试。

创建脚本的第一步创建一个文件（在本示例中我们将命名为 `simple.sh`），并在第一行添加如下：

```bash
#!/bin/sh
```

`#!` 称为“bang”，是一个特殊序列，指示执行脚本所需的解释器路径是该行的下一个项目（在本例中为位于 `/bin` 的 `sh`）。这同样可以是，例如 `/bin/csh`，取决于你想使用的解释器。

下一步是编写一个简单的脚本：

```bash
#!/bin/sh
for i in *
do
    echo $i
done
```

此脚本的作用遍历当前目录下的所有文件并显示每个文件的名称。可以通过将脚本名称作为参数传递给 `sh` 来执行：

```bash
sh simple.sh
```

为了使文件变为可执行（从而不再需要将其传递给 `sh` 命令），可以使用 `chmod` 命令：

```bash
chmod +x simple.sh
```

一旦在文件权限上设置了执行位，就可以直接执行。例如：

```bash
./simple.sh
```




在《Ubuntu Essentials》的这一章中，我们对 `Bash` shell 环境进行了简要概览。在图形化桌面环境中，人们很容易忘记，操作系统的真正威力和灵活性通常只有通过放弃用户友好的桌面界面并使用 shell 环境才能发挥。此外，当需要管理和维护没有安装桌面的服务器系统，或者尝试修复受损到导致桌面或 `Cockpit` 界面都无法启动的系统时，熟悉 shell 是非常有必要的。

shell 的功能远超本章涵盖的范围。如果你是 shell 的初级用户，我们强烈建议你寻找额外的资源。一旦熟悉了这些概念，你很快就会发现，在终端窗口中使用 shell 执行许多任务，比在桌面上层翻阅菜单和对话框要快得多。

## 10. 管理 Ubuntu 用户和组

在安装 Ubuntu 的过程中，安装程序提供了为系统创建用户账户的机会。我们不应该忽视这样一个事实：Ubuntu 实际上是一个企业级、多用户且多任务的操作系统。因此，为了充分利用 Ubuntu 的优势，可能需要为多个用户访问权限。每个用户应该有自己的用户账户登录名、密码、主目录和权限。

为了方便管理，用户被进一步划分为不同的组，这些组可以拥有不同级别的权限。例如，你可能有一组在财务部门工作的。在这种环境下，你可能希望创建一个 `accounts` 组并将所有财务部门的用户分配到该组。

在本章中，我们将介绍在 Ubuntu 系统上添加、删除和管理用户及组的步骤。管理 Ubuntu 用户和组的方法有很多，最常用的选项是命令行工具和 `Cockpit` Web 。在本章中，我们将介绍这两种用户管理方法。

### 10.1 命令行用户管理

可以通过 `useradd` 工具通过命令行向 Ubuntu 系统添加新用户。要创建一个新用户账户，请输入类似下面的命令：

```bash
## adduser john
```

正在添加用户 `john` ...

正在添加新组 `john` (1001) ...

正在添加新用户 `john` (1001) 组为 `john` ...

主目录 `/home/john` 已存在。未从 `/etc/skel` 复制。

输入新的 UNIX 密码：

重新输入新的 UNIX 密码：

`passwd: password updated successfully`

正在更改 john 的用户信息

输入新值，或按回车键使用默认值

全名 []:

房间号 []:

工作电话 []:

家庭电话 []:

其他信息 []:

该信息正确吗？[Y/n] Y

默认情况下，这将在 `/home` 目录下为该用户创建一个主目录（在本例中为 `/home/john`）。要指定不同的主目录，在创建账户时使用 `--home` 命令行选项：

```bash
## adduser --home /users/johnsmith john
```

账户创建后，可以使用 `passwd` 工具随时更改密码：

```bash
## passwd john
```

正在更改用户 john 的密码。

新密码：

重新输入新密码：

`passwd: all authentication tokens updated successfully.

可以通过 `deluser` 工具通过命令行删除已有的用户。虽然这将删除账户，但用户的文件和数据将留在系统中保持完好：

```bash
## deluser john
```

也可以在删除过程中同时移除用户的主目录和邮件邮件池（mail spool）：

```bash
## deluser --remove-home john
```

Ubuntu 系统上的所有用户都是一个或多个组的成员。默认情况下，新用户会被添加到与用户名同名的私有组中（在上面的示例中，为用户 `john` 创建的账户是一个同名为 `john` 的私有组的成员）。作为管理员，将用户组织成更有逻辑的组是有意义的。例如，所有销售人员可能属于 `sales` 组，而财务人员可能属于 `accounts` 组，以此此类推。可以使用 `addgroup` 命令行工具从命令行添加新组，例如：

```bash
## addgroup accounts
```

使用 `adduser` 工具将用户添加到现有组中：

```bash
# adduser john accounts
```

要从组中移除用户，请按如下方式使用 `deluser` 命令：

```bash
# deluser john accounts
```

可以使用 `delgroup` 工具从系统中删除已有的组：

```bash
## delgroup accounts
```

注意，如果要删除的组是任何用户的初始组或主组，则无法删除。必须先删除该用户，或者使用 `usermod` 命令分配一个新的主组，才能移除该组。可以使用 `usermod -g` 选项将用户分配给新的主组：

```bash
# usermod -g sales john
## delgroup accounts
```

要查找用户所属的组，只需运行 `groups` 命令。例如：

```bash
$ groups john
```

`john : accounts support`

默认情况下，只有 Ubuntu 系统上创建的第一个用户账户有权使用 `sudo` 命令执行特权任务。如果新添加的用户尝试使用 `sudo`，将显示类似下面的消息：

`john is not in the sudoers file. This incident will be reported.`

要将用户添加到 sudoers 文件，只需将用户加入 `sudo` 组：

```bash
# adduser john sudo
```

## 10.2 使用 Cockpit 管理用户

如果系统安装并启用了 `Cockpit` Web 界面（该主题在“Ubuntu Cockpit Web 界面概览”章节中介绍），可以在图 10-1（User_Management.xhtml__idTextAnchor174）所示的账户屏幕内执行许多用户管理任务：

![](img/ubuntu_20.04_cockpit_users.jpg)

该屏幕将显示系统上已有的用户账户，并提供添加额外账户的按钮。要创建新账户，点击 ` New Account` 按钮并在弹出的对话框中输入所需信息（图 10-2，User_Management.xhtml__idTextAnchor175）。注意，该选项也可以创建账户但在稍后锁定：

![](img/ubuntu_20.04_cockpit_new_account.jpg)

图 10-2

要修改用户账户，从主屏幕选择该账户并对账户进行任何修改：

![](img/ubuntu_20.04_cockpit_user_details.jpg)

图 10-3

此屏幕允许执行多种操作，包括锁定或解锁账户、更改密码或强制用户配置新密码。如果选择了 `Server Administrator`，用户将被加入 `sudo` 组并允许使用 `sudo` 执行管理任务。还提供了一个从系统中删除用户的按钮。

如果用户将使用密钥加密的 `SSH` 连接远程访问系统，可以在此屏幕内添加用户的公钥。`SSH` 访问和验证将在后的“在 Ubuntu 上配置 SSH 密钥认证”中介绍。

## 10.3 使用设置应用管理用户

第三种用户账户管理选项通过 GNOME 桌面设置应用可用。可以通过点击 GNOME 桌面右上角的向下箭头并选择 `Settings` 选项来访问该应用，如图 10-4（User_Management.xhtml__idTextAnchor177）所示：

![](img/ubuntu_20.04_desktop_settings_menu_option.jpg)

图 10-4





当主设置界面出现时，点击左侧导航面板中的 `Users`（用户）选项。默认情况下，设置将被锁定，且无法对系统上的用户账户进行任何更改。要解锁设置应用，请点击下方图 10-5 所示的 `Unlock`（解锁）按钮并输入您的密码。请注意，只有当以具有 `sudo` 权限的用户身份登录时，才能解锁设置：

![](img/ubuntu_20.04_desktop_settings_unlock.jpg)

图 10-5

应用解锁后，标题栏将出现一个标记为 `Add User...`（添加用户...）的绿色按钮。点击此按钮将显示下方图 10-6 所示的对话框：

![](img/ubuntu_20.04_desktop_settings_add_user.jpg)

图 10-6

为新用户分配 `sudo` 权限，请选择 `Administrator`（管理员）账户，否则保持选中 `Standard`（标准）。输入用户的全名和用户名，并现在分配密码，或允许用户在首次登录账户时设置密码。信息输入完成后，点击 `Add`（添加）按钮创建账户。

可以通过如图 10-7 所示，在 `Users` 界面中选择相应的图标，随时查看、修改现有用户的设置或删除该账户。此外还可以查看用户的登录活动选项。请注意，在对账户进行任何更改之前，需要再次解锁 `Settings` 应用：

![](img/ubuntu_20.04_desktop_settings_user_details.jpg)

图 10-7

### 10.4 总结

作为一种多用户操作系统，Ubuntu 的设计初衷是支持对多个用户的受控访问。在安装过程中，系统会创建一个单一用户账户。可以使用一组命令行工具、通过 `Cockpit` Web 界面或使用 `GNOME` 设置应用向系统添加额外的用户账户。除了用户账户外，Linux 还实现了组（groups）的概念。可以使用命令行工具添加新组并将用户分配到这些组中，且每个用户必须至少属于一个组。默认情况下，标准非 root 用户没有权限执行特权任务。然而，特殊 `sudo` 组的成员可以通过 `sudo` 命令执行特权任务。

## 11 管理 Ubuntu systemd 单元（Units）

为了精通 Ubuntu 系统管理，理解 `systemd` 单元的概念至关重要，特别关注名为 `targets`（目标）和 `services`（服务）的两种特定类型。因此，本章的目标是提供 Ubuntu 支持的不同 `systemd` 单元的基本概述，并概述如何配置运行在运行 Linux 系统后台的许多服务。

### 11.1 理解 Ubuntu systemd 目标

Ubuntu 可以被配置为启动到若干状态中的一种（称为 `targets`），每种状态都旨在提供特定层面的操作系统功能。系统默认启动的目标由系统管理员根据系统的实际用途进行配置。例如，桌面系统最可能被配置为使用图形用户界面目标启动，而云服务器系统则更有可能启动到多用户目标层级。

在启动过程中，名为 `systemd` 的进程会在 `/etc/systemd/system` 文件夹中查找默认目标设置。识别出默认目标后，它将启动与该目标相关的 `systemd` 单元，以便系统在运行所有必要进程的情况下启动。

对于熟悉旧版本 Ubuntu 的用户来说，`systemd` 目标是旧运行级别（runlevel）系统的替代品。

### 11.2 理解 Ubuntu systemd 服务

服务本质上是一个进程，通常在后台运行并提供特定功能。例如，`sshd` 服务是提供系统安全 shell 访问的后台进程（也称为守护进程/daemon）。不同的 `systemd` 目标被配置为自动启动不同的服务集合，取决于该目标需要提供的功能。

目标（Targets）和服务（Services）是 `systemd` 单元的类型，该主题将在章稍后部分介绍。

### 11.3 Ubuntu systemd 目标描述

如前所述，Ubuntu 可以启动到若干目标层级中的一种。系统配置的默认启动目标反过来将决定启动哪些 `systemd` 单元。与系统启动和关机相关的目标可以总结如下：

- `poweroff.target` - 系统关机的目标。出于显然原因，你不太希望将其作为默认目标。
- `rescue.target` – 导致系统以单用户模式启动，此时只有 root 用户可以登录。在此模式下，系统不会启动任何网络、图形用户界面或多用户服务。此运行级别是系统管理员执行系统维护或修复活动的理想选择。
- `multi-user.target` - 将系统启动到具有文本控制台登录能力的多用户模式。
- `graphical.target` - 将系统启动到具有 X Window 系统能力的联网、多用户状态。默认情况下，图形桌面环境将在启动过程结束时启动。这是桌面或工作站最常用的运行级别。
- `reboot.target` - 重启系统。另一个出于显然原因，你不太可能将其作为默认目标。

除了上述目标外，系统还包含了约 70 个其他目标，其中许多本质上是上述目标的子目标。在后台，例如，`multi-user.target` 会启动一个名为 `basic.target` 的目标，该目标反过来会启动 `sockets.target` 单元，这确保了多用户目标所依赖的所有服务在启动过程中都会启动。

指定目标所依赖的目标列表可以通过在终端中运行以下命令来查看：

```bash
# systemctl list-dependencies <target>
```

图 11-1 例如，显示了多用户目标 `systemd` 单元依赖的部分列表（完整列表包含功能完整的多用户系统所需的 120 多个目标和服务）：

![](img/ubuntu_18.04_systemctl_argets.jpg)

图 11-1

列表以分级树的形式呈现，说明某些依赖具有自己的子依赖。滚动到列表底部，例如会发现多用户目标依赖于 `local-fs.target`，其具有自己的服务和目标子依赖：

![](img/ubuntu_18.04_systemctl_local-fs.jpg)

图 11-2

列表左侧的彩色点表示该服务或目标的当前状态如下：

- 绿色 - 服务或目标已激活并运行。
- 白色 - 服务或目标未激活（已停止）。通常是因为服务或目标尚未启用、由于某些原因已停止，或服务或目标依赖的条件未满足。
- 红色 - 服务或目标因致命错误启动失败。

要获取有关 `systemd` 单元状态的更多详细信息，使用 `systemctl status` 命令后跟单元名称，如下所示：

```bash
# systemctl status systemd-machine-id-commit.service
```

```
◉ systemd-machine-id-commit.service - Commit a transient machine-id on disk
  Loaded: loaded (/usr/lib/systemd/system/systemd-machine-id-commit.service; static; vendor preset: disabled)
  Active: inactive (dead)
```





条件：启动条件于 Thu 2019-02-14 15:27:47 EST 失败；1h 14min 前

未满足 `ConditionPathIsMountPoint=/etc/machine-id`

文档：`man:systemd-machine-id-commit.service(8)`

### 11.4 识别和配置默认目标

可以使用 `systemctl` 命令识别 Ubuntu 系统的当前默认目标：

```bash
systemctl get-default
```

`multi-user.target`

在上述情况下，系统配置为默认使用 `multi-user.target` 启动。可以使用 `systemctl` 命令配合 `set-default` 随时更改默认设置。以下示例将默认目标更改为下次系统启动时启动图形用户界面：

```bash
systemctl set-default graphical.target
```

删除 `/etc/systemd/system/default.target`。

创建软链接 `/etc/systemd/system/default.target` → `/usr/lib/systemd/system/graphical.target`。

默认更改操作的输出显示了 `systemctl` 命令在后台执行以实施更改的步骤。当前默认值是通过从位于 `/etc/systemd/system` 的 `default.target` 文件建立符号链接，指向 `/usr/lib/systemd/system` 文件夹中相应的目标文件（在本例中为 `graphical.target` 文件）来配置的。

## 11.5 理解 systemd 单元和单元类型

如前所述，目标（targets）和服务（services）都是 systemd 单元。`/usr/lib/systemd/system` 文件夹中的所有文件都被称为 systemd 单元配置文件，每个文件代表一个 systemd 单元。每个单元被归类为特定的单元类型。Ubuntu 支持 12 种单元类型，包括本章已涵盖的目标和服务单元类型。

单元文件的类型由下表 [11-1] 所示的文件扩展名表示：

| 单元类型 | 文件扩展名 | 类型描述 |
| :--- | :--- | :--- |
| Service | `.service` | 系统服务。 |
| Target | `.target` | systemd 单元组。 |
| Automount | `.automount` | 文件系统自动挂载点。 |
| Device | `.device` | 内核识别的设备文件。 |
| Mount | `.mount` | 文件系统挂载点。 |
| Path | `.path` | 文件系统中的文件或目录。 |
| Scope | `.scope` | 外部创建的进程。 |
| Slice | `.slice` | 管理系统进程的层次结构单元组。 |
| Snapshot | `.snapshot` | systemd 管理器的保存状态。 |
| Socket | `.socket` | 进程间通信套接字。 |
| Swap | `.swap` | 交换设备或交换文件。 |
| Timer | `.timer` | systemd 定时器。 |

表 11-1

目标单元类型与其他不同之处在于，它本质由一组 systemd 单元（如服务或其他目标）组成。

### 11.6 动态更改当前目标

上述 `systemctl set-default` 命令指定了下次启动时将使用的目标，但不会更改当前运行系统的状态。要动态切换到不同的目标，请再次使用 `systemctl` 命令，这次使用 `isolate` 选项后接目标目标。例如，要在不重启的情况下将当前系统切换到图形目标，可以使用以下命令：

```bash
systemctl isolate graphical.target
```

执行后，系统将启动图形桌面环境。

## 11.7 启用、禁用和屏蔽 systemd 单元

新安装的 Ubuntu 系统将包含基础 systemd 服务单元，但不太可能包含系统进入生产环境后最终需要的所有服务。例如，基本的 Ubuntu 安装通常不会包含运行 Apache Web 服务器所需的包，其关键元素之一是 `apache2.service` 单元。

系统管理员将通过使用以下命令安装必要的 Apache 包来解决此问题：

```bash
apt install apache2
```

配置好 Web 服务器后，下一个任务将是检查 `apache2.service` 单元的状态，以识别它是否作为安装过程的一部分被激活：

```bash
systemctl status apache2.service
```

```
● apache2.service - The Apache HTTP Server
  Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: enabled)
  Drop-In: /lib/systemd/system/apache2.service.d
               └─apache2-systemd.conf
  Active: active (running) since Wed 2020-04-08 14:34:54 EDT; 34s ago
  Main PID: 3513 (apache2)
  Tasks: 55 (limit: 4915)
  CGroup: /system.slice/apache2.service
              ├─3513 /usr/sbin/apache2 -k start
              ├─3515 /usr/sbin/apache2 -k
```

### 11.8 在 Cockpit 中使用 systemd 单元

除了本章目前概述的命令行技术外，还可以在 Cockpit Web 界面内部查看和管理 systemd 单元。假设 Cockpit 已按照“Ubuntu Cockpit Web 界面概览”章节所述的方法进行了安装和设置，可以通过登录 Cockpit 并选择左侧导航面板中图 11-3 所示标记为 A 的 Services 选项来访问系统的 systemd 单元列表。





标记为 B 的按钮在标记为 C 的主区域中显示特定类型的单元，其中每个单元的当前状态在 State 列中列出。

从列表中选择一个单元将显示详细信息。例如，图 11-4 显示了 `apparmor.service` 实例的详细界面，包括服务日志 (A) 和用于执行启动、停止、启用/禁用以及屏蔽/取消屏蔽单元等任务的菜单选项 (B)。

![](img/ubuntu_20.04_cockpit_service_details.jpg)

图 11-4

### 11.9 总结

新安装的 Ubuntu 系统包含一组基础 systemd 单元（units），其中许多单元在后台运行，以提供系统的大部分功能。这些单元按类型进行分类，其中最常见的是目标（targets）和服务单元（services）。目标单元简单来说，是一组要集体启动的其他单元的集合。系统有一个默认的目标单元，它定义了每次系统启动时要启动的其他单元。最常见的目标是那些将系统引导到多用户模式或图形模式的目标。`systemctl` 命令行工具为执行 systemd 单元配置任务提供一系列选项，其中许多选项也可以通过 Cockpit Web 界面可用。

### 12. Ubuntu 软件包管理与更新

新安装的 Ubuntu 系统极不可能包含执行其预设任务所需的所有软件包。即使已经安装了所有所需的软件，几乎可以肯定，在系统的生命周期内，许多此类包的更新版本将会发布。在某些情况下，您将需要确保系统上安装了这些最新的软件包版本，以修复漏洞和安全问题。

本章介绍了 Ubuntu 软件管理的基本概念，解释了如何解决这些问题，引入了仓库（repositories）和软件包的概念，同时探索了如何列出、安装和删除构成运行 Ubuntu 系统的软件包。

### 12.1 仓库

Linux 本质上由一组基础包组成，这些包提供了操作系统的核心功能，以及一系列其他包和模块，这些包在基础操作系统之上增加了功能和特性。

在首次安装 Ubuntu 时，将根据安装阶段选择的软件选项安装许多不同的软件包。然而，一旦系统开始运行，就可以根据需要安装额外的软件。通常，所有属于 Ubuntu 的软件（换句话说，不是由第三方供应商提供的软件）都是使用高级软件包工具（`apt`）下载并安装到系统上的。正如我们在前面的章节中看到的，这通常涉及在命令行提示符输入类似下面的命令：

```
# apt install apache2
```

当执行此类命令时，请求的软件将从远程仓库下载并安装在本地系统上。默认情况下，Ubuntu 配置为从多个不同的仓库下载软件：

- `main` - 包含由 Ubuntu 官方支持、测试和更新的核心包集。
- `restricted` - 对于没有开源替代方案的硬件设备的专有驱动程序。
- `universe` - 包含 Canonical Ubuntu 团队未官方支持的软件包。然而，这些包由 Ubuntu 社区维护，并包含主仓库中不可用的软件包。
- `multiverse` - 由于版权或其他法律问题，这些软件包可能不符合 Ubuntu 发布时遵循的开源许可条款。

Ubuntu 系统上当前启用的仓库列表包含在 `/etc/apt/sources.list` 文件，可以将其加载到编辑器中查看和修改。可以手动将文件加载到编辑器，或使用以下命令通过可选的编辑器进行编辑：

```
# apt edit-sources
```

该文件的前几行通常引用 main 和 restricted 仓库，例如：

```
deb http://us.archive.ubuntu.com/ubuntu/ bionic main restricted
```

在上面的示例中，列表配置允许从 main 和 restricted 仓库下载软件包。universe 和 multiverse 仓库的条目也会包含在文件中：

> **注意：此仓库中的软件可能没有主发布版中包含的软件那样经过测试，尽管它包含了一些应用程序的更新版本，这些版本可能提供有用的功能。**
>
> **此外，请注意，backports 中的软件将不会收到来自 Ubuntu 安全团队的任何审查或更新。**

```
deb http://us.archive.ubuntu.com/ubuntu/ bionic-backports main restricted universe multiverse
```

要禁用某个仓库使其不再用于下载软件包，只需在行首加一个“#”字符将该行将其注释掉即可：

```
# deb http://us.archive.ubuntu.com/ubuntu/ bionic-backports main restricted universe multiverse
```

除了标准仓库外，还有许多第三方仓库。如果您需要使用其中之一，只需为 `sources.list` 文件添加其对应的条目即可。

其中一个示例是 partners 仓库，它包含在 `sources.list` 文件中但默认被注释掉了：

```
# deb http://archive.canonical.com/ubuntu bionic partner
```

要启用此仓库，只需删除“#”注释字符并保存文件即可。

#### 12.2 使用“软件与更新”管理仓库

作为使用命令行的替代方案，可以在 GNOME 桌面环境中使用“软件与更新”（Software & Updates）应用程序配置仓库。要启动此应用，按下键盘上的特殊键（Windows 键盘上是 Windows 键，macOS 上是 Command 键，Chromebook 上显示放大镜的键），并在搜索栏中输入 `Software Updates`。在结果面板中点击相应的图标。或者，打开一个终端窗口并运行以下命令：

```
$ update-manager
```

当应用加载时，点击如图 12-1 所示的“设置”按钮：

![](img/ubuntu_20.04_software_manager.jpg)

图 12-1

在设置界面上，启用或禁用“从互联网下载”标题下的所需仓库：

![](img/ubuntu_20.04_software_manager_settings.jpg)

图 12-2

要启用伙伴 仓库，选择如图 12-3 所示的“其他软件”选项卡：

![](img/ubuntu_20.04_software_manager_other.jpg)

图 12-3

要添加其他第三方仓库，点击“添加...”按钮并在弹出的对话框中输入仓库信息：

![](img/ubuntu_20.04_software_manager_add_repo.jpg)

图 12-4

#### 12.3 使用 APT 管理软件包

`apt` 工具提供了一种直接从命令行执行大多数软件包管理任务的方法。在本节中，我们将探索一些更常用的 `apt` 命令行选项。

Ubuntu 系统保留最新软件包信息的本地副本，因此，建议在执行任何其他 apt 操作之前按照如下方式更新此列表：

```
## apt update
```

最常用的 apt 活动之一是执行软件包安装：

```
## apt install package_name
```

同样，可以使用 `remove` 选项从系统中删除已安装的软件包：

```
## apt remove package_name
```



当以这种方式删除包时，与包相关的配置文件将保留在系统上。这允许在以后重新安装该包而不会丢失任何自定义配置设置。若要在删除过程中或删除操作执行后删除这些文件，请使用 `purge` 选项：

```
apt purge package_name
```

要获取可安装的软件包列表，请按如下方式使用 `apt`：

```
apt list
```

或者，若要仅列出已安装的软件包，请配合 `--installed` 标志使用 `list` 选项：

```
apt list --installed
```

要检查系统是否已安装特定软件包，请将 `list` 选项与包名结合：

```
apt list package_name
```

使用 `search` 选项列出符合特定标准的软件包。例如，列出所有与 Apache Web 服务器相关的包：

```
apt search apache
```

要找到哪个软件包包含某个特定文件，请使用 `apt-file` 命令。例如，列出包含名为 `gimp` 文件的包名：

```
apt-file --package-only list gimp
```

要查看软件包的详细信息，运行带有 `show` 选项的 `apt`：

```
apt show apache2
```

运行上述命令的典型输出如下：

```
Package: apache2
Version: 2.4.29-1ubuntu4.13
Priority: optional
Section: web
Origin: Ubuntu
Maintainer: Ubuntu Developers <ubuntu-devel-discuss@lists.ubuntu.com>
Original-Maintainer: Debian Apache Maintainers <debian-apache@lists.debian.org>
Bugs: https://bugs.launchpad.net/ubuntu/+filebug
Installed-Size: 535 kB
Provides: httpd, httpd-cgi
Pre-Depends: dpkg (>= 1.17.14)
Depends: lsb-base, procps, perl, mime-support, apache2-bin (= 2.4.29-1ubuntu4.13), apache2-utils (= 2.4.29-1ubuntu4.13), apache2-data (= 2.4.29-1ubuntu4.13), perl:any
Recommends: ssl-cert
Suggests: www-browser, apache2-doc, apache2-suexec-pristine | apache2-suexec-custom, ufw
Conflicts: apache2.2-bin, apache2.2-common
Replaces: apache2.2-bin, apache2.2-common
Homepage: http://httpd.apache.org/
Task: lamp-server
Supported: 5y
Download-Size: 95.1 kB
APT-Sources: http://us.archive.ubuntu.com/ubuntu bionic-updates/main amd64 Packages
Description: Apache HTTP Server
The Apache HTTP Server Project 的目标是构建一个符合标准的开源软件、安全、高效且可扩展的 HTTP 服务器。其结果长期以来一直是互联网上第一大 Web 服务器。
安装此包将导致完整安装，包括配置文件、初始化脚本和支持脚本。
```

### 12.4 执行更新

在基础操作系统和已安装软件包的生命周期内，将发布多次更新以解决问题并添加功能。要从命令行手动下载并安装任何待处理的更新，第一步是使用带有 `update` 选项的 `apt` 更新本地系统上存储的包信息：

```
apt update
```

一旦包信息已更新，就可以执行升级。这将从 `sources.list` 文件配置的存储库下载当前已安装包的任何更新并将其安装到系统中：

```
apt upgrade
```

作为命令行的替代方案，可以使用“软件与更新”（Software & Updates）GNOME 桌面应用程序更新系统。如果有可用更新，将出现如图 12-5 所示的对话框，提供查看可用更新信息和执行升级的选项：

![](img/ubuntu_20.04_software_update_install_updates.jpg)

图 12-5

### 12.5 启用自动更新

上一节查看了如何手动安装包升级。Ubuntu 系统也可以配置为自动安装升级。这既可以通过命令行配置，也可以在“软件与更新”工具内部配置。

在“软件与更新”工具内部，如之前所述打开“设置”屏幕并点击“更新”选项卡，显示图 12-6 所示的屏幕：

![](img/ubuntu_18.04_software_updater_auto_updates.jpg)

选择系统应多频繁地检查更新（每天、隔日、每周等）。接下来，选择当有可用更新时做什么（仅下载、下载并安装，或在桌面上显示通知）。你还可以配置更新程序，在有 Ubuntu 新版本可用时通知你。

要从命令行配置自动更新，请遵循以下步骤：

1. 安装 `unattended-upgrades` 包：

```
apt install unattended-upgrades
```

2. 编辑 `/etc/apt/apt.conf.d/50unattended-upgrades` 文件并找到以下行：

```
"${distro_id}ESMApps:${distro_codename}-apps-security";
"${distro_id}ESM:${distro_codename}-infra-security";
```

（注意：移除 `//` 注释以启用它们）。

3. 移除要自动更新的存储库类型的 `//`。

4. 编辑 `/etc/apt/apt.conf.d/20autoupgrades` 文件并声明检查更新的频率（天）：

```
APT::Periodic::Update-Lists "1";
APT::Periodic::Upgradeable "1";
APT::Periodic::Autoclean "0";
APT::Periodic::Unattended-Upgrade "1";
```

5. 执行一次运行更新以确保设置有效：

```
unattended-upgrades --dry-run
```

配置自动更新几天后，检查日志文件以确认更新正在进行：

```
cat /var/log/unattended-upgrades/unattended-upgrades.log
```

### 12.6 启用 Livepatch

Linux 历史章节解释了内核如何作为 Linux 操作系统的基础，管理系统资源并处理硬件与应用程序之间的通信。

与任何软件一样，内核也会更新以修复漏洞并解决安全问题。虽然大多数软件包可以在重启的情况下更新，但内核历史上并非如此。随着 Livepatch 的引入，对于 Ubuntu 来说不再如此。

Livepatch 是 Canonical 提供的一项服务，允许在运行 Ubuntu 系统时对内核补丁而无需重启系统。该服务对个人用户免费提供最多三台系统，并对于付费 Ubuntu 订阅的用户支持更多系统。

配置 Livepatch 的第一步是在以下 URL 创建 Ubuntu 账户（如果你还没有）：

[`login.ubuntu.com/`](https://login.ubuntu.com/%20)

一旦创建了账户，留在浏览器窗口并导航到以下 URL：

[`auth.livepatch.canonical.com/`](https://auth.livepatch.canonical.com/%20)

页面加载后，选择用户类型（如果你不是付费 Ubuntu 用户，只需选择 Ubuntu User ）：

![](img/ubuntu_18.04_livepatch_user_type.jpg)

图 12-7

接下来，点击“Get your Livepatch token”按钮。在后续屏幕上，使用你的 Ubuntu One 凭据登录。

会出现一个页面，包含你的 Livepatch 密钥要在 Ubuntu 系统上运行的命令。复制这些命令，打开终端窗口并运行：

```
snap install canonical-livepatch
canonical-livepatch enable your_key_here
```

注意，上述安装没有使用 `apt`，而是使用了 Snap 包管理系统，主题将在下一节 Ubuntu Snap 包管理中介绍。

要检查 Livepatch 状态，只需运行以下命令：





# canonical-livepatch 状态

上次检查：2 分前

内核：`5.3.0-46.38~20.04.1-generic`

服务器签到：成功

补丁状态：此内核尚不需要实时补丁

### 12.7 总结

Ubuntu 操作系统由数千个软件软件包组成，这些软件包从主、受限、universe、multiverse、partner 合作伙伴以及第三方存储库下载并安装。

软件软件包使用高级软件包工具 (`apt`) 或若干图形化桌面工具之一进行安装，并从 `sources.list` 文件中定义的存储库下载。

除了安装和删除软件软件包外，`apt` 还可以用于将这些软件包升级到最新更新。这些软件升级可以手动进行，也可以配置为自动更新。

在过去，操作系统内核的更新需要重启系统。随着 Livepatch 的引入，Ubuntu Linux 内核现在可以在不中断系统的情况下进行动态更新。

## 13 Ubuntu Snap 软件包管理

上一章节探讨了如何使用高级软件包工具 (`APT`) 在 Ubuntu 系统上安装和更新软件软件包。近年来，Canonical, Ltd. 的 Ubuntu 团队一直在开发一种名为 `Snap` 的新软件包管理系统。虽然没有官方计划完全用 `Snap` 替换 `APT`，但现在可以安装为“snaps”的软件包列表仍在不断增长。

本章的目标是介绍 `Snap` 系统，突出它优于 `APT` 系统的主要优势，并概述如何使用 `snap` 命令行工具安装和管理基于 snap 的软件软件包。

### 13.1 使用 Snap 管理软件

`apt` 工具安装封装在 `.deb` 文件中的软件。使用 `apt` 安装的软件包通常依赖于其他软件包，这些软件包也需要安装才能正常运行。在安装过程中，`apt` 还会下载并安装这些额外的软件包依赖项。

考虑一个依赖于特定图像库的图形设计应用。在安装期间，`apt` 在安装图形应用软件包的同时，还会安装包含其所依赖的库的软件包。现在，假设用户决定安装另一个同样于相同图形库的图形工具。通常这不会成为问题，因为两个应用程序将共享同一个库，但如果两个应用程序依赖于不同版本的库，可能会出现问题。因此，安装第二个应用程序可能会导致第一个应用程序无法正常工作。

`apt` 和 `.deb` 软件包的另一个局限性是，很难在系统中并行安装同一工具或应用的两个不同版本。例如，用户可能想在保留图形应用 1.0 版本安装的同时，尝试 2.0 版本的最新测试版。在尝试过 2.0 版本后，用户可能想删除 1.0 版本并只保留新版本，这一任务使用 `apt` 是很难实现的。

`snap` 系统专门设计用于解决此类缺陷。`snap` 工具安装 `.snap` 软件包，这些软件包包含了软件运行所需的所有库和资源。这避免了将任何依赖项作为单独独立的软件包进行安装的需求。一旦安装了 snap，它会被放置在一个自包含的位置，因此不会与其他软件包共享任何依赖项。例如，我们假设的图形应用各拥有其应用开发者所使用的精确图像库版本的副本，该版本无法被删除、被不兼容的版本替换或被任何其他软件包安装覆盖。

当然，使用 snaps 会导致软件包文件较大，从而导致下载时间变长、安装性能变慢以及磁盘空间占用增加。尽管如此，这些缺点通常被 snap 软件包的优势所抵消。

`Snap` 还支持通道（channels）的概念，这允许应用开发者发布同一应用程序的不同版本。Snap 通道是多个版本的同一软件能够并行安装的机制。

### 13.2 基础 Snap 命令

尽管许多软件包仍以 `.deb` 格式提供并使用 `apt` 安装，但现在以 snap 格式提供的应用和工具数量正在迅速增加。事实上，Ubuntu Software 工具中列出的所有软件（在本文名为“GNOME 3 桌面导览”的章节中概述过）都是使用 `snap` 封装和安装的。基于 snap 的软件也可以使用 `snap` 命令行工具安装，本节将涵盖其基础知识。

要列出特定类别软件的可用 snap 软件包，请运行类似下面的命令：

```
# snap find "image editor"
```

名称 版本 发布者 备注 摘要

gimp 2.10.18 snapcrafters - GNU 图像处理程序

paintsupreme-3d 1.0.41 braindistrict - PaintSupreme 3D

.

.

上述命令将列出所有可下载和安装的、与图像编辑软件相关的 snap 软件包。其中一个结果是 gimp 图像编辑器。关于 `gimp` snap 的详细信息如下：

```
$ snap info gimp
```

name: gimp

summary: GNU 图像处理程序

publisher: Snapcrafters

store-url: https://snapcraft.io/gimp

contact: https://github.com/snapcrafters/gimp/issues

license: GPL-3.0+

description: |
  无论你是图形设计师、摄影师、插画师还是科学家，GIMP 都提供了复杂的工具来完成工作。得益于许多自定义选项和第三方插件，你可以通过 GIMP 进一步提高生产力。

  此 snap 由 Snapcrafters 社区维护，并不一定

  由上游开发者认可或维护。

  上游项目: https://www.gimp.org/

  snapcraft.yaml 定义:
  https://github.com/snapcrafters/gimp/blob/master/snapcraft.yaml

snap-id: KDHYbyZukmLhiogKiUksByRhXD2gY

channels:
  latest/stable: 2.10.18 2020-03-03 (252) 182MB -
  latest/candidate: ↑
  latest/beta: ↑
  latest/edge: 2.11.02 2020-04-28 (265) 184MB -

`snap find` 命令还可以通过名称查找特定软件包，以及提供类似功能的软件包。例如，搜索 VLC 播放器应用也会列出类似的软件包：

```
# snap find vlc
```

名称 版本 发布者 备注 摘要

vlc 3.0.10 videolan - 终极播放器

mjpg-streamer 2.0 ogra - UVC 摄像头流工具

audio-recorder 3.0.5+rev1432+pkg-7b07 brlin - Linux 免费录音器（极其不稳定）

tundra 0.1.0 m4tx - MyAnimeList 同步器

dav1d 0.6.0 videolan - VideoLAN 的 AV1 解码器

peerflix v0.39.0+git1.df28e20 pmagill - Node.js 种子流客户端

要获取系统中已安装的 snap 软件包列表，可以使用 `snap list` 选项：

```
$ snap list
```

名称 版本  发布者 备注

canonical-livepatch 9.5.5 95 latest/stable canonical

core 16-2.44.3 9066 latest/stable canonical

core18 20200427 1754 latest/stable canonical

gnome-3-28-1804 3.28.0-16-g27c9498.27c9498 116 latest/stable canonical

.

.

要安装 snap 软件包（例如安装 Remmina 远程桌面工具），请运行 `snap` 命令并后跟要安装的软件包名称：

```
$ snap install remmina
```

要删除 snap 软件包，只需在运行 `snap` 的 `remove` 选项时指定软件包名称：

```
# snap remove remmina
```

### 13.3 使用 Snap 通道





在执行安装时如果没有指定通道，`snap` 将默认使用稳定（stable）通道。这确保了安装的是软件的最新可靠版本。若要从不同的通道进行安装，请先使用 `snap info` 选项识别所需的包当前可用通道：

```bash
snap info remmina

name: remmina
summary: Remote Desktop Client
.
.
channels:
  latest/stable: v1.4.3+git13.688f5f75 2020-04-20 (4139) 37MB -
  latest/candidate: ↑
  latest/beta: ↑
  latest/edge: v1.4.3+git27.1bd753df 2020-05-01 (4150) 37MB -
```

从上述输出中可以看出，虽然 Remmina 应用的稳定版本是 `v1.4.3+git13.688f5f75`，但在 `edge` 通道中提供了更更新的版本。

当然，`candidate`、`beta` 和 `edge` 通道提供了不稳定性不断增加的软件形式（称为风险级别），但如果你想尝试某个包即将发布的功能的早期访问版本，请从更高风险的通道进行安装。例如：

```bash
snap install --channel=edge remmina
```

通道选择也可以缩写为 `--stable`、`--candidate`、`--beta` 或 `--edge`，例如：

```bash
snap install --edge remmina
```

如果该包已经安装，可以使用 `switch` 选项更改风险级别：

```bash
snap switch channel=edge remmina
```

这将更改 `snap` 跟踪该特定包的通道。可以使用 `snap info` 命令识别包当前正在跟踪的通道：

```bash
snap info remmina

name: remmina
.
.
tracking: latest/edge
.
.
```

仅运行 `snap switch` 命令不会立即刷新包以使用新通道。为了理解其工作原理，探索 snap 刷新调度将有所帮助。

## 13.4 Snap 刷新调度

snap 系统包含一个名为 `snapd` 的后台服务，负责根据已安装 snap 所跟踪的通道来刷新它们。默认情况下，`snapd` 以固定间隔执行刷新操作（通常每天四次）。要识别上一次刷新的时间以及下一次到期的时间，运行以下命令：

```bash
snap refresh --time

timer: 00:00~24:00/4
last: today at 07:23 EDT
next: today at 14:25 EDT
```

上述输出还包含了计时器信息，表明刷新将在每个 24 小时内执行四次：

.
.
timer: 00:00~24:00/4
.
.

还可以使用 `snap` 命令强制刷新所有已安装的 snap 包，如下：

```bash
snap refresh
```

或者，刷新特定包：

```bash
snap refresh remmina
```

若要在不等待下次 `snapd` 服务刷新的情况下将包切换到不同的通道，只需如下所示运行 `snap refresh` 命令并指定目标通道：

```bash
snap refresh remmina --channel=edge
```

snap 系统还有一组四个属性，可以通过修改这些属性来调整 `snapd` 使用的刷新调度：

- `refresh.timer`：存储当前的刷新调度和频率。
- `refresh.hold`：用于将刷新操作延迟到指定的日期和时间（RFC 3339 格式）。
- `refresh.metered`：当网络访问通过计费连接（如移动数据连接）进行时，暂停刷新操作。
- `refresh.retain`：用于配置每个 snap 安装需要保留的版本数量。

例如，安排刷新在工作日的凌晨 1:00 到凌晨 2:00 之间发生：

```bash
snap set system refresh.timer=mon-fri,1:00-2:00
```

同样，以下命令将配置为每天两次刷新，分别发生在早上 6:00 到 7:00 以及晚上 10:00 到 11:00 之间：

```bash
snap set system refresh.timer=6:00-7:00,22:00-23:00
```

关于计时器格式和语法的完整说明可以在以下 URL 在线找到：
[`snapcraft.io/docs/timer-string-format`](https://snapcraft.io/docs/timer-string-format)

在更改计时器后，务必按照如下方式检查设置：

```bash
snap refresh --time

timer: mon-fri,1:00-2:00
last: today at 07:23 EDT
next: tomorrow at 01:00 EDT
```

要暂停刷新，必须使用 RFC 3339 格式指定恢复刷新的日期和时间，详情可以在以下 URL 找到：
[`tools.ietf.org/html/rfc3339`](https://tools.ietf.org/html/rfc3339)

摘要，日期和时间应使用以下格式：
`YYYY-MM-DDTHH:MM.SS<UTC offset>`

例如，将刷新安排在 2020 年 10 月 12 日凌晨 3:20（纽约时间），其格式如下：
`2020-10-12T03:20:00-05:00`

由于纽约使用的是东部时间 (EST)，它与协调时 (UTC) 有 -5 小时的偏移。格式化如下：
`2020-10-12T03:20:00-05:00`

要检查当前锁定，使用 `snap` 配合 `system get` 选项：

```bash
snap get refresh.hold
2020-10-12T03:20:00-05:00
```

要移除锁定，只需为属性分配 `null` 值：

```bash
snap set system refresh.hold=null
```

`refresh.retain` 属性可以设置为 0 到 20 之间的任何值，例如：

```bash
snap set system refresh.retain=10
```

最后，要在通过计费连接时暂停更新，将 `refresh.metered` 属性设置为锁定：

```bash
snap set system refresh.metered=hold
```

与锁定属性一样，通过为属性分配 `null` 值来禁用此设置：

```bash
snap set system refresh.metered=null
```

## 13.5 Snap 服务

注意，某些 snap 包在安装时包含在后台运行的服务（类似于“管理 systemd ”章节中描述的 systemd 服务）。要获取系统中当前运行的 snap 服务列表，执行带有 `services` 选项的 `snap` 命令：

```bash
snap services

Service Startup Current Notes
canonical-livepatch.canonical-livepatchd enabled -
```

上述输出表明该 snap 服务已启用并激活。要启动或停止服务，可以使用以下 `snap` 命令：

```bash
snap start canonical-livepatch.canonical-livepatch
snap stop canonical-livepatch.canonical-livepatch
```

同样，可以使用 `enable` 和 `disable` 选项控制服务是否在系统启动时自动启动：

```bash
snap enable canonical-livepatch.canonical-livepatch
snap disable canonical-livepatch.canonical-livepatch
```

如果 snap 服务生成了日志文件，可以如下查看该文件：

```bash
snap logs canonical-livepatch

2020-05-06T13:21:58Z canonical-livepatch[763]: No payload available.
2020-05-06T13:21:58Z canonical-livepatch[763]: during refresh: cannot check: No machine-token. Please run ‘canonical-livepatch enable’!
```

.
.

仍然可以使用 `systemctl` 命令来管理 snap 服务。这通常需要在服务名称前加上 `snap.`。例如：

```bash
systemctl status snap.canonical-livepatch.canonical-livepatchd
```

### 13.6 总结




直到最近，所有的 Ubuntu 软件包都存储在 `.deb` 文件中并使用高级软件包工具 (`APT`) 进行安装。现在，有越来越多的软件包可以使用 `Snap` 安装，`Snap` 是由 Canonical, Ltd. 开发的包管理系统。与 `apt` 软件包不同，`snap` 将软件包的所有依赖项封装成单个 `.snap` 文件。这确保了软件软件包是自包含的，拥有运行其所需的所有库和资源的副本。这避免了不同软件包因依赖不同版本的相同共享资源和库而可能产生的冲突。Snap 系统还允许并行安装同一软件包的不同版本。Ubuntu 软件工具列出的所有软件都以 snap 包的形式提供。此外，还可以使用命令行 `snap` 来安装、删除和管理软件包。

## 14 Ubuntu 网络管理

很难想象一个至少没有一个网络连接的 Ubuntu 系统，而设想这样一个孤立的系统能如何产生多大的实用价值则更加困难。事实证明是，Ubuntu 的设计目的是通过网络和互联网连接提供企业级服务。学习如何管理 Ubuntu 系统的关键部分涉及学习如何配置和管理安装在系统上的网络接口。

本章旨在概述 Ubuntu 网络管理，包括 `NetworkManager` 服务和工具，以及其他一些实用程序。

### 14.1 NetworkManager 简介

`NetworkManager` 是一个服务和一组工具，专门用于简化 Linux 系统上的网络配置管理，它是 Ubuntu 桌面安装的默认网络管理服务。

除了在后台运行的服务外，`NetworkManager` 还包含以下工具：

- `nmcli`: 一个通过命令行与 `NetworkManager` 交互的工具。在无法访问图形环境时该工具非常有用，也可以用于脚本中进行网络配置更改。
- `nmtui`: 用于管理 `NetworkManager` 的基本文本用户界面。该工具可以在任何终端窗口中运行，允许通过选择菜单和输入数据进行更改。虽然对于执行基本任务很有用，但 `nmtui` 缺乏 `nmcli` 工具提供的许多功能。
- `nm-connection-editor`: 一个全图形化管理工具，提供了访问大多数 `NetworkManager` 配置选项的。
- `GNOME Settings`: GNOME 桌面设置应用程序中的“网络”屏幕允许执行基础网络管理任务。
- `Cockpit Network Settings`: Cockpit Web 界面的网络屏幕允许执行一系列网络管理任务。

虽然有多种方法可以管理 Ubuntu 系统上的网络环境，但为了本章的目的，我们将关注 `nmcli` 命令。虽然在你有桌面环境访问或启用 Cockpit 时，图形化工具确实有用，但在只有命令提示符可用的情况下，理解命令行界面至关重要。此外，图形化工具（包括 Cockpit）并不包含 `nmcli` 工具的所有功能。最后，一旦你熟悉了 `NetworkManager` 和 `nmcli`，这些技能在这些更直观的工具选项时可以很容易地转换。图形化工具选项则并非如此。例如，如果你只用过 `nm-connection-editor`，那么使用 `nmcli` 就会变得困难。

### 14.2 安装并启用 NetworkManager

如果使用了桌面安装镜像，大多数 Ubuntu 安装默认都已安装 `NetworkManager`。使用 `apt` 命令查看是否需要安装：

```bash
apt -qq list network-manager
```

network-manager/bionic-updates,now 1.22.10-1ubuntu1 amd64 [installed,automatic]

```

如有必要，按照以下方式安装软件包：

```bash
apt install network-manager
```

一旦安装了软件包，就需要启用 `NetworkManager` 守护进程，以便在每次系统启动时启动：

```bash
systemctl status network-manager
```

最后，启动服务并检查状态以验证启动是否成功：

```bash
systemctl status network-manager
```

● NetworkManager.service - Network Manager
   Loaded: loaded (/lib/systemd/system/NetworkManager.service; enabled; vendor preset: enabled)
   Active: active (running) since Wed 2020-04-08 14:31:58 EDT; 19h ago
      Docs: man:NetworkManager(8)
   Main PID: 704 (NetworkManager)
   Tasks: 4 (limit: 4915)
   CGroup: /system.slice/NetworkManager.service
              ├─704 /usr/sbin/NetworkManager --no-daemon

## 14.3 基本 nmcli 命令

`nmcli` 工具将作为 `NetworkManager` 软件包的一部分安装，可以使用以下语法从命令行执行：

```bash
nmcli [Options] Object {Command | help}
```

在上述语法中，`Object` 将是 `general`、`networking`、`radio`、`connection`、`monitor`、`device` 或 `agent` 之一，所有都可以缩写为单词的几个字母（例如 connection 缩写为 `con`，甚至只是字母 `c`）。例如，以下所有命令都将输出与 `device` 对象相关的帮助信息：

```bash
nmcli device help
nmcli dev help
nmcli d help
```

要检查系统上 `NetworkManager` 的整体状态，使用以下命令：

```bash
nmcli general status
```

STATE CONNECTIVITY WIFI-HW WIFI WWAN
connected full enabled enabled

要检查系统中安装的设备状态，可以使用以下命令：

```bash
nmcli dev status
```

DEVICE TYPE CONNECTION
eno1 ethernet connected
wlxc8a3517 wifi connected
virbr0 bridge connected
lo loopback unmanaged
virbr0-nic tun unmanaged

可以使用 `-p` (pretty) 选项修改输出，使其更符合人类习惯：

```bash
nmcli -p dev status
```

=====================
  Status of devices
=====================
DEVICE TYPE STATE
---------------------------------------------------------------
eno1 ethernet connected
1xc8a3517 wifi connected
virbr0 bridge connected
lo loopback unmanaged
virbr0-nic tun unmanaged



相反，可以使用 `-t` 选项使输出更简洁，适用于自动化处理：

```bash
nmcli -t dev status
```

eno1:ethernet:connected
wlxc8a3517:wifi:connected
virbr0:bridge:connected
lo:loopback:unmanaged

```

从状态输出中，我们可以看到系统有两个物理设备，一个是以太网，另一个是 WiFi 设备。桥 (`virbr`) 条目是为虚拟机提供网络的虚拟设备。回环接口 (`lo`) 是允许系统与自身通信的特殊虚拟设备，通常用于执行网络诊断。

在使用 `NetworkManager` 时，理解设备（device）和连接（connection）的区别很重要。如上所述，设备是物理或虚拟网络设备，而连接是设备连接的网络配置。

以下命令显示系统上配置的连接信息：

```bash
nmcli con show
```

NAME UUID TYPE DEVICE
zoneone bbd6e294-5d0c-4eac-b3c2-4dfd44becc9c wifi wlxc8a35cad17
Wired connection 1 56f32c14-a4d2-32c8-9391-f51967efa173 ethernet eno1
virbr0 f2d3494f-6ea4-4c90-936c-5eda9ac96a85 bridge virbr0
zonetwo f2a20df5-aa5e-4576-8379-579d154c3e0d wifi --
zonethree 45beac50-8741-41a6-abff-415640e24071 wifi --




从上述输出，我们可以看到 WiFi 设备（`wlxc83a35cad517`）连接到了名为 `zoneone` 的无线网络，而以太网设备（`eno1`）连接到了名为 `Wired connection 1` 的连接。除了 `zoneone` 外，`NetworkManager` 还列出了两个名为 `zonetwo` 和 `zonethree` 的 WiFi 连接，它们目前都没有连接设备。

要查找分配给连接的 IP 地址，可以使用 `ip` 工具配合 `address` 选项：

```
ip address
```

这也可以简写为：

```
ip a
```

.
.

3: wlxc83a35cad517: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether c8:3a:35:ca:d5:17 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.121/24 brd 192.168.86.255 scope global dynamic noprefixroute wlxc83a35cad517
        valid_lft 86076sec preferred_lft 86076sec
.
.

`ip` 命令将输出系统上检测到的所有设备的信息。上述输出显示 WiFi 设备已分配了 IP 地址 `192.168.1.121`。

如果我们只想列出活跃的连接，可以使用 `nmcli` 命令配合 `-a` 选项：

```
nmcli con show -a
```

NAME UUID TYPE DEVICE
zoneone bbd6e294-5d0c-4eac-b3c2-4dfd44becc9c wifi wlxc83a35cad517
Wired connection 1 56f32c14-a4d2-32c8-9391-f51967efa173 ethernet eno1
virbr0 f2d3494f-6ea4-4c90-936c-5eda9ac96a85 bridge virbr0

将 WiFi 设备连接从 `zoneone` 切换到 `zonetwo`，我们可以运行以下命令：

```
nmcli device wifi connect zonetwo -ask
```

密码：

`-ask` 标志会导致 `nmcli` 提示用户输入 WiFi 网络的密码。要在命令行中包含 WiFi 密码（特别是在脚本中执行命令时非常有用），请使用 `password` 选项：

```
nmcli device wifi connect zonetwo password <password here>
```

`nmcli` 工具也可以按如下方式扫描可用的 WiFi 网络：

```
nmcli device wifi list
```

IN-USE SSID MODE CHAN RATE SIGNAL BARS SECURITY
    zoneone Infra 6 195 Mbit/s 80 WPA2
* zonetwo Infra 11 130 Mbit/s 74 WPA1 WPA2

一个当前活跃的连接可以按如下方式停用：

```
nmcli con down <connection name>
```

同样，可以随时重新恢复非活跃的连接：

```
nmcli con up <connection name>
```

当连接被断开时，`NetworkManager` 会自动搜索另一个连接，激活它并将其分配到之前建立连接的设备上。为了防止在这种情况下使用连接，请按如下方式禁用 `autoconnect` 选项：

```
nmcli con mod <connection name> connection.autoconnect no
```

可以使用以下命令获取关于特定连接的附加信息。这包括所有连接属性的当前值：

```
nmcli con show "Wired connection 1"
```

connection.id: Wired connection 1
connection.uuid: 56f32c14-a4d2-32c8-9391-f51967efa173
connection.stable-id: --
connection.type: 802-3-ethernet
connection.interface-name: --
connection.autoconnect: yes
connection.autoconnect-priority: -999
connection.autoconnect-retries: -1 (default)
connection.auth-retries: -1
connection.timestamp: 1586442354
connection.read-only: no
connection.permissions: --
connection.zone: --
connection.master: --
connection.slave-type: --
connection.autoconnect-slaves: -1 (default)
.
.

所有这些属性都可以使用 `nmcli` 配合 `modify` 选项通过以下语法进行修改：

```
nmcli con mod <connection name> connection.<property name> <setting>
```

## 14.4 使用连接配置文件

到目前为止，我们探索了连接的使用，但还没有解释如何配置连接。连接的配置被称为连接配置文件，存储在 `/etc/NetworkManager/system-connections` 目录下的文件中，其内容如下：

```
ls /etc/NetworkManager/system-connections
```

zoneone.nmconnection zonetwo.nmconnection zonethree.nmconnection

每个文件都是一个接口配置文件，包含连接的配置文件。

考虑假设的 `zoneone` 连接的内容如下：

```
[connection]
id: Wired connection 1
uuid: 56f32c14-a4d2-32c8-9391-f51967efa173
stable-id: --
type: 802-3-ethernet
interface-name: --
autoconnect: yes
autoconnect-priority: -999
autoconnect-retries: -1 (default)
auth-retries: -1
timestamp: 1586442354
read-only: no
permissions: --
zone: --
master: --
slave-type: --
autoconnect-slaves: -1 (default)
```

每个文件都是一个接口配置文件，包含连接的配置文件。




`uuid=6e03666b-26a1-476e-b5b2-77c8eac6006c`

`type=ethernet`

`interface-name=enp0s3`

`permissions=`

[ethernet]
`mac-address-blacklist=`

[ipv4]
`address1=192.168.1.200/24,192.168.1.1`
`dns-search=`
`method=manual`

[ipv6]
`addr-gen-mode=stable-privacy`
`dns-search=`
`method=auto`

添加新连接的命令可以稍微微调，以便同时分配 IPv4 和 IPv6 静态地址：

```
nmcli con add type ethernet con-name static_ip ifname enp0s3 ip4 192.168.1.200/24 gw4 192.168.1.1 gw4 192.168.1.1 ip6 cabf::4532 gw6 2010:dfa::1
```

### 14.5 交互式编辑

除了使用命令行选项的 `nmcli` 外，该工具还包含一个交互模式，用于创建和修改连接配置文件。例如，下面的输出显示了如何使用交互模式创建一个名为 `demo_con` 的新以太网连接：

```
nmcli con edit
```

可用的连接类型：`6lowpan`, `802-11-olpc-mesh (olpc-mesh)`, `802-11-wireless (wifi)`, `802-3-ethernet (ethernet)`, `adsl`, `bluetooth`, `bond`, `bridge`, `cdma`, `dummy`, `generic`, `gsm`, `infiniband`, `ip-tunnel`, `macsec`, `macvlan`, `ovs-bridge`, `ovs-interface`, `ovs-port`, `ppoe`, `team`, `tun`, `vlan`, `vpn`, `vxlan`, `wimax`, `wpan`, `bond-slave`, `bridge-slave`, `team-slave`

输入连接类型：`ethernet`

```
===| nmcli interactive connection editor |===
正在添加新的 ‘802-3-ethernet’连接

输入 ‘help’ 或 ‘？’ 查看可用命令。
输入 ‘print’ 显示所有连接属性。
输入 ‘describe [<setting>.<prop>]’ 获取详细的属性描述。

你可以编辑以下设置：connection, `802-3-ethernet (ethernet)`, `802-1x`, `dcb`, `sriov`, `ethtool`, `match`, `ipv4`, `ipv6`, `tc`, `proxy`

nmcli> set connection.id demo_con
nmcli> set connection.interface enp0s8
nmcli> set connection.autoconnect yes
nmcli> set ipv4.method auto
nmcli> set 802-3-ethernet.mtu auto
nmcli> set ipv6.method auto
nmcli> save

正在保存设置了 ‘autoconnect=yes’ 的连接。这可能会导致连接立即激活。

你仍然想要保存吗？(yes/no) [yes] yes

连接 ‘demo_con’ (cb837408-6c6f-4572-9548-4932f88b9275) 已保存。

nmcli> quit
```

相反，下面的输出修改了之前创建的 `static_ip` 连接配置文件，使用与原始指定不同的静态 IP 地址：

```
nmcli con edit static_ip
```

```
===| nmcli interactive connection editor |===
正在编辑现有的 '802-3-ethernet'连接：'static_ip'

输入 'help' 或 '?' 查看可用命令。
输入 'print' 显示所有连接属性。
输入 'describe [<setting>.<prop>]' 获取详细的属性描述。

你可以编辑以下设置：connection, `802-3-ethernet (ethernet)`, `802-1x`, `dcb`, `sriov`, `ethtool`, `match`, `ipv4`, `ipv6`, `tc`, `proxy`

nmcli> print ipv4.addresses
ipv4.addresses: 192.168.1.200/24
nmcli> set ipv4.addresses 192.168.1.201/24
nmcli> save

连接 'static_ip' (3fccafb3-e761-4271-b310-ad0f28ee8606) 已更新。

nmcli> quit
```

在修改现有连接后，请记得指示 NetworkManager 重新加载配置文件：

```
nmcli con reload
```

在使用交互模式时，了解有一个广泛的内置帮助系统可以学习如何使用该工具是非常有用的。可以通过在 `nmcli >` 提示符下输入 `help` 或 `?` 来访问帮助主题：

```
nmcli> ?
```

------------------------------------------------------------------------------
---[ 主菜单 ]---

`goto [<setting> | <prop>]` :: 跳转到某个设置或属性
`remove <setting>[.<prop>] | <prop>` :: 移除设置或重置属性值
`set [<setting>.<prop> <value>]` :: 设置属性和值
`describe [<setting>.<prop>]` :: 描述属性
`print [all | <prop>]` :: 显示属性
`verify [all | <prop>]` :: 验证连接
`save` :: 保存
`activate [<ifname>]` :: 激活连接
`back` :: 返回上一级
`help [<command>]` :: 帮助
`nmcli` :: nmcli
`quit` :: 退出
------------------------------------------------------------------------------

### 14.6 配置 NetworkManager

除了使用命令行选项 `nmcli` 外，该工具还允许指定权限。例如，下面的命令限制了连接：

```
nmcli mod static_ip
```

在连接重新加载后，只有具有权限的用户才能更改。

### 14.7 总结

Ubuntu 上的网络管理由 NetworkManager 处理。NetworkManager 将网络视为由设备和连接组成。设备可以是物理的或 WiFi。连接代表设备连接的网络，并在其他设置外定义了连接是静态还是动态地址、网关的 IP 地址以及启动时是否应建立连接。

可以使用 `nmcli` 和 `nmtui` 命令行工具，以及 Cockpit 的网络设置部分。

## 15. Ubuntu 防火墙基础

防火墙是保护个人计算机系统或网络免受外部攻击的重要组件。任何直接连接到互联网的计算机都理想情况下运行防火墙。同样，任何内部网络在与互联网之间都应该某种形式的防火墙。

Ubuntu 提供了名为 `iptables` 的强大防火墙技术。关于 `iptables` 甚至写了整本书的书。如果你想学习 `iptables`，我们推荐：

https://www.linuxtopia.org/Linux_Firewall_iptables/index.html

本章的目标是介绍防火墙、TCP/IP 端口和服务的一些基本概念。Ubuntu 防火墙配置将在“使用 gufw 和 ufw 配置 Ubuntu 防火墙”中介绍。

### 15.1 理解端口和服务

如今使用的主要的网络通信协议是 TCP/IP。它是互联网使用的协议，因此取代了以前大多数流行的用于局域网（LAN）的协议。

TCP/IP 定义了共 65535 个端口，其中 1023 个被认为是已知端口。重要的是，这些不是插入网络电缆的物理端口，而是每个网络连接上的虚拟端口，应用程序和服务可以通过这些端口在 TCP/IP 网络上进行通信。事实上，流行的网络客户端和服务所使用的端口仅是已知端口组的一个更小的子集。




操作系统可以提供许多不同的 TCP/IP 服务。本章末尾的表格提供了此类服务的完整列表，这些服务包括用于运行安全 Web 服务器的 `HTTPS`、用于允许文件传输的 `FTP`、用于提供安全远程登录访问及文件传输的 `SSH` 以及用于传输电子邮件消息的 `SMTP`。每个服务随后被分配给一个标准的 TCP/IP 端口。例如，`HTTPS` 被分配给端口 `443`，而 `SSH` 通信在端口 `22` 上进行。

## 15.2 端口和服务的安全

服务器安全工作的很大一部分涉及定义角色，并根据角色定义应该启用哪些服务和端口。例如，仅作为 Web 服务器运行的服务器应该只运行 `HTTPS` 服务（可能还包括用于远程管理访问的 `SSH`）。所有其他服务都应该被禁用，并且理想情况下，应该直接从操作系统中完全删除（这使得入侵者更难重新启用该服务）。

系统安全涉及从操作系统中移除任何不必要的服务，并确保使用防火墙拦截与非本质服务相关的端口。定义哪些端口在什么情况下可以访问的规则是使用 `iptables` 定义的。

许多操作系统在安装时默认安装并激活了许多服务。在安装新的操作系统之前，必须对安装进行仔细的计划。这涉及到决定哪些服务是不需要的，并识别哪些服务是默认安装并启用的。部署新操作系统的安装过程绝不能仓忙。系统上可的服务和开放端口越少，攻击者的攻击面和机会就越小。

## 15.3 Ubuntu 服务和 iptables 规则

默认情况下，新安装的 Ubuntu 系统没有定义任何 `iptables` 规则来限制端口访问。要查看当前的 `iptables` 设置，可以在终端窗口中执行以下命令：

```bash
# iptables -L

Chain INPUT (policy ACCEPT)
target prot opt source destination

Chain FORWARD (policy ACCEPT)
target prot opt source destination

Chain OUTPUT (policy ACCEPT)
target prot opt source destination
```

如上述输出所示，目前没有定义任何规则。虽然这看起来是一个不安全的配置，但重要的是，新安装的 Ubuntu 系统默认运行的服务很少，这使得端口对潜在的攻击者来说基本上是无用的。例如，无法远程登录新安装的 Ubuntu 系统或访问 Web 服务器，原因仅仅是因为 `ssh` 或 Web 服务器服务默认没有安装或运行。然而，一旦系统上开始激活服务，通过定义 `iptables` 规则来建立防火墙策略将变得至关重要。

有很多方法可以定义 `iptables` 规则，包括使用命令行工具和配置文件。例如，要阻止来自 IP 地址 `192.168.2.76` 访问端口 `25`（`SMTP` 邮件传输协议使用），可以在终端窗口中发布以下命令：

```bash
# iptables -A INPUT -s 192.168.2.76 -p tcp --destination-port 25 -j DROP
```

如果我们现在检查当前规则，将发现这条规则已列在其中：

```bash
# iptables -L

Chain INPUT (policy ACCEPT)
target prot opt source destination
DROP tcp -- 192.168.2.76 anywhere tcp dpt:smtp

Chain FORWARD (policy ACCEPT)
target prot opt source destination

Chain OUTPUT (policy ACCEPT)
target prot opt source destination
```

随后可以按如下方式移除该规则：

```bash
# iptables -D INPUT -s 192.168.2.76 -p tcp --destination-port 25 -j DROP
```

考虑到 `iptables` 的复杂性，因此创建了许多用户友好的图形化配置工具来简化规则创建过程。其中一种工具就是是不复杂的防火墙（Uncomplicated Firewall），它带有 `ufw` 命令行工具和对应的图形化版本（`gufw`），这将在[使用 gufw 和 ufw 配置 Ubuntu 防火墙]章节中介绍。对于更高级的防火墙配置，`firewalld` 将在“使用 firewalld 进行基础 Ubuntu 防火墙配置”中介绍。

## 15.4 常用端口和服务

在继续介绍更复杂的防火墙规则之前，值得花时间概述一下 Ubuntu 系统可以提供的一些关键服务以及对应的端口号：

| 端口 | 分配 | 描述 |
| :--- | :--- | :--- |
| 20 | `FTP` | 文件传输协议（数据） - `FTP` 分配了两个端口（`20` 和 `21`）。端口 `20` 原本是数据传输端口。 |
| 21 | `FTP` | 文件传输（控制） - 端口 `21` 分配控制信息。 |
| 22 | `SSH` | 安全外壳 - `SSH` 提供安全的、加密的远程登录会话。它取代了 Telnet 并提供了安全复制协议 (`SCP`）和安全文件传输协议 (`SFTP`）的基础。 |
| 23 | `Telnet` | Telnet - `Telnet` 是一种终端仿真协议，提供了登录远程系统的能力。因为它以明文传输数据，因此不建议使用。 |
| 25 | `SMTP` | 简单邮件传输协议 - `SMTP` 定义了电子邮件从一个网络主机发送到另一个网络主机的机制。 |
| 53 | `DNS` | 域名服务器 - TCP/IP 网络用于将主机名和完全限定域名 (FQDN) 转换为 IP 地址的服务。 |
| 69 | `TFTP` | 简易文件传输协议 - `TFTP` 是 `FTP` 的精简版本，使用 `UDP` 传输数据。 |





| 端口 | 协议 | 描述 |
| :--- | :--- | :--- |
| 80 | HTTP | 超文本传输协议 - `HTTP` 是用于从 Web 服务器向 浏览器下载文本、图形和多媒体的协议。本质上，它定义了浏览器和服务器之间的命令和控制机制，定义了客户端请求和服务器响应。`HTTP` 基于 `TCP` 传输协议，因此是一种面向连接的协议。 |
| 110 | POP3 | 邮局协议 - `POP3` 协议是一种用于从服务器存储和检索入站邮件消息的机制。在大多数企业环境中，入站邮件存储在邮件服务器上，并在用户检查邮件时下载到运行在用户桌面或笔记本电脑上的电子邮件客户端。`POP3` 将所有新消息下载到客户端，且不为用户提供选择下载哪些消息、查看邮件头或仅下载消息部分的选项。正因如此，`IMAP` 协议正越来越多地被取代 `POP3`。 |
| 119 | NNTP | 网络新闻传输协议 - 负责在 Usenet 新闻服务器（即托管在远程服务器上的新闻组和讨论论坛）之间发布和检索消息的协议。`NNTP` 运行在 OSI 栈的应用层，并使用 `TCP` 确保无错误的消息检索和传输。 |
| 123 | NTP | 网络时间协议 - 一种旨在将计算机时与外部时间源同步的协议。使用此协议，操作系统或应用程序可以从远程 `NTP` 服务器请求当前时间。远程 `NTP` 服务器通常基于原子钟提供的时间。`NTP` 对于确保网络中的所有系统都设置为相同的、准确的当日时间非常有用。这在安全情况下特别重要，例如，当客户端或服务器上文件被访问或修改的时间存在疑问时。 |
| 143 | IMAP4 | 互联网消息访问协议第 4 版 - `IMAP4` 是一种先进且安全的邮件检索协议。`IMAP` 与 `POP3` 相似，都为用户提供了一种访问存储在邮件服务器上的邮件消息的机制，但 `IMAP` 包含了许多额外功能，例如选择性下载消息、查看消息头、搜索消息和下载部分消息的能力。`IMAP4` 使用身份验证并完全支持 `Kerberos` 认证。 |
| 161 | SNMP | 简单网络管理协议 - 提供了一种机制，网络管理员能够收集有关网络设备（如集线器、网桥器、路由器和交换机）的信息。`SNMP` 协议允许运行在网络设备上的代理向中央管理器报告状态，反之允许管理器向设备代理发送新的配置参数。可以进一步配置代理在发生某些事件（称为陷阱 traps）时通知管理器。`SNMP` 使用 `UDP` 发送和接收数据。 |
| 443 | HTTPS | 安全超文本传输协议 - 标准的 `HTTP`（非安全）协议以明文传输数据（即无加密，且任何可能拦截流量的人可见）。虽然这对于大多数网页浏览用途是可以接受的，但当需要从浏览器传输信用卡详情等敏感信息到 Web 服务器时，会产生严重的安全风险。`HTTPS` 通过使用安全套接层（`SSL`）在客户端和服务器之间发送加密数据来解决这个问题。 |

| 2049 | NFS | 网络文件系统 - 最初由 Sun Microsystems 开发，随后被业界广泛采用，`NFS` 允许另一个系统通过网络访问远程系统上的文件系统，就像该文件系统位于本地磁盘驱动器一样。`NFS` 广泛用于 `UNIX` 和 `LINUX` 操作系统。后版本的 Microsoft Windows 也拥有访问基于 `UNIX` 和 `LINUX` 系统的 `NFS` 共享文件系统的能力。 |

### 15.5 总结

新安装的 Ubuntu 系统通常被认为是安全的，因为系统端口上没有运行的服务。然而，一旦系统开始配置使用，通过实施防火墙来保护其免受攻击是非常重要的。在配置防火墙时，了解各种端口及其相应的服务非常重要。

有许多防火墙选项可用，基础的是对 `iptables` 防火墙接口进行命令行配置。通过 Uncomplicated Firewall (`ufw`) 和 `firewalld` 可更直观、高级的选项，它们将在后续章节介绍。

## 16. 使用 gufw 和 ufw 配置 Ubuntu 防火墙

在上一章中，我们查看了 Ubuntu 系统上的端口和服务。我们还简要查看了 Ubuntu 上的 `iptables` 防火墙规则，包括从命令行创建几个非常简单的规则。在本章中，我们将学习使用名为 `gufw` 和 `ufw` 的两个工具进行更用户友好的 `iptables` 配置。正如我们将看到的，`gufw` 和 `ufw` 对入站和出站网络流量及连接提供了高层控制，而无需理解底层的 `iptables` 语法。

### 16.1 gufw 和 ufw 概述

Ubuntu 包含一个名为 `ufw` 的包，它是 Uncomplicated Firewall（简易防火墙）的缩写。该包提供了一个命令行界面，用于管理和配置基于 Netfilter `iptables` 的防火墙规则。`gufw` 工具为 `ufw` 提供了一个用户友好的图形界面，旨在实现在不需要在命令行中发布 `ufw` 命令的情况下进行防火墙管理。

### 16.2 在 Ubuntu 上安装 gufw

虽然 Ubuntu 默认安装了 `ufw`，但没有安装 `gufw` 包。因此，要安装 `gufw`，请打开终端窗口（`Ctrl-Alt-T`）并在提示符输入以下命令：

```bash
apt install gufw
```

### 16.3 运行和启用 gufw

安装后，在 GNOME 桌面内按下 `Alt-F2` 并输入 `gufw` 来启动 `gufw`。首次调用时，防火墙可能处于禁用状态，如图图 16-1 所示。

要启用防火墙，将状态开关（`A`）移动到开启位置。默认情况下，主面板（`D`）将显示 `gufw` 首页，包含有关工具的基本信息。从按钮行选择选项（`C`）将更改面板显示的内容。例如，选择“规则”按钮来添加、删除和查看规则。

`gufw` 工具提供了一组预配置的配置文件，适用于工作、家庭和公共环境。要更改配置并查看设置，只需从菜单（`B`）中选择配置。要修改现有配置，从菜单中选择它并使用入站和出站菜单更改选择。这些更改将应用于当前选中的配置。

![](img/ubuntu_20.04_gufw_main.jpg)

图 16-1

当前选择配置决定了防火墙在没有特定策略规则的情况下如何处理流量。例如，默认的家庭配置配置为拒绝所有入站流量并允许所有出站流量。这些默认策略设置通过“入站:”和“出站:”菜单（`E`）进行更改。




另一方面，如果入站策略更改为 `Allow all traffic`（允许所有流量），则所有入站流量都将被允许，除非为必须拦截的特定类型连接创建了规则。不出所料，这些规则被称为黑名单。黑名单/名单方法同样适用于入站和出站连接。

### 16.4 创建新配置

虽然可以修改预定义的配置，但创建一个或多个配置来根据你的特定需求配置防火墙通常更有意义。通过选择`Edit`（编辑）->`Preferences...`（首选项...）菜单项可以显示图 16-2 所示的对话框：

![](img/ubuntu_20.04_gufw_preferences.jpg)
图 2

要添加新配置，点击配置列表下方的`+`按钮。列表中将出现名为 `Profile 1` 的新配置。要为配置命名更具描述性的名称，请双击条目进入编辑模式并输入新名称：

![](img/ubuntu_20.04_gufw_new_profile.jpg)
图 16-3

配置创建并命名后，点击`Close`（关闭）按钮返回主界面，并在`Profile`（配置）菜单中选择它：

![](img/ubuntu_20.04_gufw_enabled.jpg)
图 16-4

选中自定义配置后，即可设置自定义规则来覆盖默认的入站和出站设置。

## 16.5 添加预配置防火规则

通过点击`Rules`（规则）按钮以及位于规则面板底部的`+`按钮创建新规则，如图 16-5 所示：

![](img/ubuntu_20.04_gufw_add_rule.jpg)
图 16-5

一旦选择，将出现如图 16-6 所示的对话框，且默认选中的（显示为已选）`Preconfigured`（预配置）选项卡。`Preconfigured`面板允许选择匹配特定应用程序和服务的规则。例如，可以通过从`Application`（应用程序）菜单中选择项目，并相应地选择`Policy`（策略）和`Direction`（方向）菜单，来限制或允许来自`Skype`和`BitTorrent`等工具的流量。

为了帮助找到特定的应用程序或服务，请使用`Category`（类别）和`Subcategory`（子类别）菜单来过滤`Application`菜单中出现的项目。或者，只需在`Application Filter`（应用程序过滤器）字段中输入应用程序或服务的名称来过滤菜单项：

![](img/ubuntu_20.04_gufw_rule_settings.jpg)
图 16-6

`Policy`（策略）菜单为控制所选应用程序或服务的流量提供以下选项：

- `Allow` – 允许端口上的流量。
- `Deny` – 不允许端口上的流量。请求系统不会收到拒绝的通知。数据包被直接丢弃。
- `Reject` - 不允许端口上的流量。数据包被丢弃，并通知请求系统已被拒绝。
- `Limit` - 如果同一个 IP 地址在 30 秒内尝试建立 6 次或更多连接，则拒绝该连接。

一旦定义了规则，点击`Add`（添加）按钮将实施该规则，关闭`Add Rule`对话框，新规则将列在`gufw`工具的主界面上（包含 IPv4 和 IPv6 协议的规则）：

![](img/ubuntu_20.04_gufw_rule_added.jpg)
图 16-7

要删除规则，请在列表中选择它并点击对话框底部的`-`按钮。同样，通过选择现有规则并点击`-`按钮右侧的齿轮按钮来编辑现有规则。

### 16.6 添加简单防火墙规则

预配置规则允许根据已知的服务和应用程序配置防火墙，而`Add Rule`对话框的`Simple`（简单）选项卡允许通过引用相应的 TCP/IP 端口简单地定义入站和出站规则。已知应用程序和服务使用的端口仅代表了应用程序可用端口的一小部分，而对于这些端口可能需要定义防火墙规则。例如，第三方应用程序可能会使用端口 `5700` 与远程服务器通信。在这种情况下，可能需要使用`Simple`面板允许此特定端口的流量：

![](img/ubuntu_20.04_gufw_simple_rule.jpg)
图 16-8

该规则可以配置为过滤 `TCP`、`UDP` 或两种类型的流量。此外，端口可以指定为单个端口号或端口范围，起始和结束端口之间用冒号分隔（例如，`1000:1500` 将规则适用于 1000 到 1500 之间的所有端口）。或者，输入与端口关联的服务名称（例如 `https` 或 `ssh`）。

### 16.7 添加高级规则

到此为止，我们查看了仅控制要拦截流量类型的规则（例如端口 `22` 上的入站流量），而不考虑流量的源或地。然而，通常需要定义规则以根据 IP 地址或 IP 地址范围来允许或拒绝流量。

作为示例目的，假设本地系统的 IP 地址为 `192.168.0.102`。防火墙可以配置为仅允许来自 IP 地址为 `192.168.0.102` 的系统的 `22` 端口访问。

### 16.8 使用 ufw 从命令行配置防火墙

通过图形界面 `gufw` 工具可用的所有防火墙配置选项也可以通过底层命令行使用 `ufw` 使用。

要启用或禁用防火墙：

```bash# ufw enable
# ufw disable
```

使用`status`选项可以获取防火墙的当前状态：

```bash# ufw status
```
Status: active
To Action From
-- ------ ----
22 ALLOW 192.168.86.30
```

为了获取更详细的状态信息，将上述命令与`verbose`选项结合：

```bash
# ufw status verbose
```
Status: active
Logging: on (full)
Default: deny (incoming), allow (outgoing), deny (routed)
New profiles: skip
To Action From
-- ------ ----
22 ALLOW IN 192.168.86.30
```

要更改这些默认设置之一，请使用`ufw`命令配合`default`选项使用以下语法：

```bash
# ufw default <policy> <direction>
```





例如，默认允许所有入站连接：

```bash
ufw default allow incoming
```

要对特定端口允许或阻止流量，请使用以下语法：

```bash
ufw <policy> <port number>/<optional protocol>
```

例如，允许端口 30 上的所有 TCP 和 UDP 入站流量：

```bash
ufw allow 30
```

同样地，拒绝端口 5700 上的入站 TCP 流量：

```bash
ufw deny 5700/tcp
```

规则也可以通过引用与端口对应的服务名称来声明。例如，在端口 22 上启用 SSH 访问：

```bash
ufw allow ssh
```

与 `guf` 工具类似，`ufw` 也允许从特定的外部 IP 地址控制访问。例如，允许来自 IP 地址 `192.168.0.20` 的所有入站流量：

```bash
ufw allow from 192.168.0.20
```

要特定拒绝来自某个 IP 地址的流量：

```bash
ufw deny 192.168.0.20
```

将 IP 地址 `192.168.0.20` 的访问限制为仅端口 22：

```bash
ufw allow from 192.168.0.22 to any port 22
```

要进一步限制该 IP 地址的访问仅限 TCP 数据包，请使用以下语法：

```bash
ufw allow from 192.168.0.20 to any port 22 proto tcp
```

可以使用 `insert` 选项声明新规则在现有规则列表中的位置。例如，创建一个新规则并将其插入到规则列表的第 3 位置：

```bash
ufw insert 3 allow from 192.168.0.123 to any port 2
```

显示带有相关编号的规则列表：

```bash
ufw status numbered
```

Status: active

```
      To Action From
      -- ------ ----
[ 1] 22 ALLOW IN 192.168.86.30
[ 2] 30 ALLOW IN Anywhere
[ 3] 22 ALLOW IN 192.168.0.123
[ 4] 5700/tcp DENY IN Anywhere
[ 5] 22/tcp ALLOW IN Anywhere
[ 6] Anywhere ALLOW IN 192.168.0.20
[ 7] 22 ALLOW IN 192.168.0.4
[ 8] 30 (v6) ALLOW IN Anywhere (v6)
[ 9] 5700/tcp (v6) DENY IN Anywhere (v6)
[10] 22/tcp (v6) ALLOW IN Anywhere (v6)
```

一旦确定了分配给规则的数字，可以使用该数字从防火墙中删除规则：

```bash
ufw delete 4
```

要获取 `ufw` 工具功能的完整列表，请运行带有 `--help` 参数的命令：

```bash
ufw help
```

可以使用 `logging` 命令行选项启用和禁用防火墙活动的日志记录：

```bash
ufw logging on
ufw logging off
```

`ufw` 执行的日志记录数量也可以开启日志时声明，包括低、中、高或全设置，例如：

```bash
ufw logging on low
```

`ufw` 日志文件位于：

`/var/log/ufw.log`

使用 `reload` 选项重启防火墙并重新加载所有当前设置：

```bash
ufw reload
```

最后，将防火墙重置为默认设置（从而删除所有现有规则和设置）：

```bash
ufw reset
```

### 16.9 总结

任何通过内部网络或互联网连接到其他系统的计算机系统都应该实现某种形式的防火墙，以降低攻击风险。Ubuntu 提供的简易防火墙（Uncomplicated Firewall）提供了一个简单而有效的防火墙，允许使用命令行或图形化 `gufw` 工具定义基本规则。本章概述了启用防火墙和配置防火墙规则的基础。

## 17. 使用 firewalld 进行基础 Ubuntu 防火墙配置

所有 Linux 发行版都提供了某种形式的防火墙解决方案。在 Ubuntu 的情况下，这表现为上一章概述的简易防火墙。本章将介绍适用于 Ubuntu 的以 `firewalld` 形式提供的更高级防火墙解决方案。

### 17.1 firewalld 简介

`firewalld` 服务最初为基于 Red Hat 的 Linux 发行版开发，它使用一组规则来控制入站网络流量，并定义哪些流量应该被阻止，哪些允许通过系统，它构建在名为 `iptables` 的更复杂的防火墙工具之上。

`firewalld` 系统提供了一种管理入站流量的灵活方法。例如，防火墙可以配置为阻止来自特定外部 IP 地址的流量，或阻止到达特定 TCP/IP 端口的所有流量。还可以定义规则以将入站流量转发到不同的系统，或作为互联网网关来保护网络上的其他计算机。

与常见的安全实践一致，默认的 `firewalld` 安装配置为阻止所有访问，但 SSH 远程登录和系统用于获取 IP 地址的 DHCP 服务除外。Ubuntu 防火墙配置的关键元素是区域、接口、端口。

### 17.1.1 区域 (Zones)

默认情况下，`firewalld` 安装时带有一预配置的区域。区域是一组可以应用于系统的预配置规则集，以便快速实现特定场景的防火墙配置。例如，`block` 区域阻止所有流量，而 `home` 区域假设系统运行在安全环境中。Ubuntu 可用的区域：

| 区域 | 描述 |
| --- | --- |
| drop | 最安全的区域。仅允许出站连接，所有入站连接都被丢弃且无通知。 |
| block | 与 drop 区域类似，但入站连接会收到 `icmp-host-prohibited` 或 `icmp6-prohibited` 通知。 |
| public | 供公共区域使用。你不信任网络上的其他计算机不会损害你的计算机。仅允许特定的入站连接。 |
| external | 当系统作为网络的互联网网关时，将此区域应用于连接互联网的接口。该区域在实现伪装或网络地址转换 (NAT) 时与 `internal` 区域配合使用。 |
| internal | 与 `external` 区域配合使用，并应用于连接内部网络的接口。假设内部网络上的计算机是信任的。 |
| dmz | 用于军事化区 (DMZ)。这些区域通常计算机是公开访问的，但与内部网络的其他部分隔离。 |
| work | 用于在工作环境的网络上运行系统，此时其他计算机是信任的。 |
| home | 用于在家庭网络上运行系统，此时其他计算机是信任的。 |
| trusted | 安全性最低的区域。接受所有入站连接。 |

要查看区域的特定设置，请参考位于 `/usr/lib/firewalld/zones` 目录下对应的 XML 配置文件。以下列出了 `public.xml` 区域配置的内容：

```xml<?xml version="1.0" encoding="utf-8"?>
<zone>
  <short>Public</short>
  <description>供公共区域使用。你不信任网络上的其他计算机不会损害你的计算机。仅允许特定的入站连接。</description>
  <service name="ssh"/>
  <service name="mdns"/>
  <service name="dhcpv6-client"/>
</zone>
```

### 17.1.2 接口 (Interfaces)





任何连接到互联网或网络（或两者都有）的 Ubuntu 系统都包含至少一个以物理或虚拟网络设备形式存在的接口。当 `firewalld` 激活时，这些接口中的每一个都会被分配到一个区域（zone），允许为不同的接口分配不同级别的防火墙安全策略。考虑一个拥有两个接口的服务器，一个连接到外部互联网，另一个连接到内部网络。在这种情况下，面向外部的接口很可能会被分配到限制更严格的外部区域（external zone），而内部接口可能会使用内部区域（internal zone）。

### 17.1.3 服务
TCP/IP 定义了一组在标准端口上通信的服务。例如，安全的 HTTPS 网页连接使用端口 `443`，而 SMTP 邮件服务使用端口 `25`。为了有选择性地启用针对服务的服务的入站流量，可以在区域中添加 `firewalld` 规则。例如，家庭区域（home zone）默认不允许入站 HTTPS 连接。可以通过向区域添加规则以允许入站 HTTPS 连接来启用此类流量，而无需引用特定的端口号。

### 17.1.4 端口
虽然在添加 `firewalld` 规则时可以引用常见的 TCP/IP 服务，但也会出现需要在一个未分配给服务的特定端口上允许入站连接的情况。可以通过添加引用特定端口而非服务的规则来实现。

### 17.2 检查 firewalld 状态
`firewalld` 服务通常不会在所有 Ubuntu 安装中默认安装并启用。可以通过以下命令检查服务的状态：

```bash
systemctl status firewalld
```

```
● firewalld.service - firewalld -动态防火墙守护
    Loaded: loaded (/lib/systemd/system/firewalld.service; enabled; vendor preset: enabled)
    Active: active (running) since Fri 2020-04-10 10:17:54 EDT; 20s ago
      Docs: man:firewalld(1)
  Main PID: 4488 (firewalld)
    Tasks: 2 (limit: 4915)
    CGroup: /system.slice/firewalld.service
              └─4488 /usr/bin/python3 -Es /usr/sbin/firewalld --nofork --nopid
Apr 10 10:17:54 demo-server systemd[1]: Starting firewalld -动态防火墙守护进程...
Apr 10 10:17:54 demo-server systemd[1]: Started firewalld -动态防火墙守护进程.
```

如有必要，可以如下安装 `firewalld` 服务：

```bash
apt install firewalld
```

`firewalld` 服务默认已启用，因此在安装完成后以及每次系统启动时都会自动启动。

### 17.3 使用 firewall-cmd 配置防火墙规则
`firewall-cmd` 命令行工具允许在终端窗口中查看 `firewalld` 配置信息，并对区域和规则进行更改。

在更改防火墙设置时，意识到运行时（runtime）和永久（permanent）配置的概念非常重要。默认情况下，任何规则更改都被视为运行时配置更改。这意味着虽然更改会立即生效，但它们在下次系统重启或 `firewalld` 服务重载时（例如通过执行以下命令）将会丢失：

```bash
firewall-cmd --reload
```

要使更改永久生效，必须使用 `--permanent` 命令行选项。永久更改在 `firewalld` 服务重载之前不会生效，但在手动更改之前将一直有效。

### 17.3.1 识别和更改默认区域
要识别默认区域（换句话说，除非专门选择了不同的区域，否则所有接口将被分配到的区域），请按如下方式使用 `firewall-cmd` 工具：

```bash
firewall-cmd --get-default-zone
```
public

将默认区域改为不同的区域：

```bash
firewall-cmd --set-default-zone=home
```
success

### 17.3.2 显示区域信息
列出系统中所有可用区域：

```bash
firewall-cmd --get-zones
```
block dmz drop external home internal public trusted work

按如下方式获取当前激活的区域及其分配的接口列表：

```bash
firewall-cmd --get-active-zones
```
external
  interfaces: eth0
internal
  interfaces: eth1

```

可以如下所示列出为特定区域配置的所有规则：

```bash
firewall-cmd --zone=home --list-all
```
home (active)
  target: default
  icmp-block-inversion: no
  interfaces: eth0
  sources:
  services: cockpit dhcpv6-client http mdns samba-client ssh
  ports:
  protocols:
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:

使用以下命令列出当前可包含在 firewalld 规则的服务：

```bash
firewall-cmd --get-services
```
RH-Satellite-6 amanda-client amanda-k5-client amqp amqps apcupsd audit bacula bacula-client bgp bitcoin bitcoin-rpc bitcoin-testnet bitcoin-testnet-rpc ceph ceph-mon cfengine cockpit

列出当前为某个区域启用的服务：

```bash
firewall-cmd --zone=home --list-services
```
cockpit dhcpv6-client http

可以如下所示获取区域启用的端口列表：

```bash
firewall-cmd --zone=public --list-ports
```
9090/tcp

### 17.3.3 添加和删除区域服务
要为某个区域启用服务，使用 `--add-service` 选项。在此例中添加到 public 区域，使用以下命令：

```bash
firewall-cmd --zone=public --add-service=https
```
success

默认情况下这是运行时更改，因此在系统重启后将丢失。要使更改在下次系统启动时生效，请使用 `--permanent` 标志：

```bash
firewall-cmd --zone=public --permanent --add-service=https
```
success

要验证服务已永久添加，请确保包含 `--permanent` 标志：

```bash
firewall-cmd --zone=public --permanent --list-services
```
cockpit dhcpv6-client http

注意，作为永久更改，该规则在系统重启或 firewalld 重载之前不会生效：

```bash
firewall-cmd --reload
```

使用 `--remove-service` 选项从区域中删除服务。由于这是运行时更改，下次系统重启时将恢复：

```bash
firewall-cmd --zone=public --remove-service=https
```

要永久删除服务，请使用 `--permanent` 标志，并记住如果需要更改立即生效，则重载防火墙：

```bash
firewall-cmd --zone=public --permanent --remove-service=https
```

### 17.3.4 使用基于端口的规则
要启用特定端口，使用 `--add-port` 选项。注意在手动定义端口时，需要提供端口号和协议（`TCP` 或 `UDP`）：

```bash
firewall-cmd --zone=public --permanent --add-port=5000/tcp
```

向区域添加规则时也可以指定端口范围：

```bash
firewall-cmd --zone=public --permanent --add-port=5900-5999/udp
```

### 17.3.5 创建新区域
可以通过运行以下命令创建一个全新的区域。一旦创建，就可以像任何预定义区域一样管理该区域：

```bash
firewall-cmd --permanent --new-zone=myoffice
```
success

在添加新区域后，需要重启 firewalld 使该区域可用：

```bash
firewall-cmd --reload
```
success

### 17.3.6 更改区域/接口分配
如前所述，系统上的每个接口必须分配到一个区域。可以使用 `firewall-cmd` 工具更改接口分配的区域。在下述示例中，将 `eth0` 接口分配给 `public` 区域：

```bash
firewall-cmd --zone=public --change-interface=eth0
```
success

### 17.3.7 伪装 (Masquerading)




伪装（Masquerading）在网络管理领域更为广为人知的网络地址翻译（NAT）。当使用 Ubuntu 系统作为计算机网络访问互联网的网关时，伪装允许所有内部系统在通过互联网通信时使用该 Ubuntu 系统的 IP 地址。这样做的好处是可以向恶意的外部实体隐藏任何系统的内部 IP 地址，并且避免了为网络上的每台计算机分配公网 IP 地址的必要性。

使用以下命令检查防火墙上是否已经启用了伪装：

```bash
firewall-cmd --zone=external --query-masquerade
```

使用以下命令启用伪装（如果希望更改永久生效，请记得使用 `--permanent` 标记）：

```bash
firewall-cmd --zone=external --add-masquerade
```

### 17.3.8 添加 ICMP 规则

互联网控制消息协议（ICMP）用于网络上的客户端系统向彼此发送错误消息等信息。它也是 `ping` 命令的基础，网络管理员和用户都使用它来检测特定客户端在网络上是否存活。ICMP 类别允许阻止特定的 ICMP 消息类型。例如，管理员可能会选择阻止入的 ping（Echo Request）ICMP 消息，以防止基于 ping 的拒绝服务（DoS）攻击的可能性（即服务器被恶意的大量 `ping` 消息轰炸，导致其无法响应合法请求）。

要查看可以包含在 firewalld 规则中的 ICMP 类型，请以下命令：

```bash
firewall-cmd --get-icmptypes
```

`address-unreachable bad-header beyond-scope communication-prohibited destination-unreachable echo-reply ...`

例如，以下命令永久地为公共区域（public zone）添加规则以阻止 echo-reply（ping 请求）消息：

```bash
firewall-cmd --zone=public --permanent --add-icmp-block=echo-reply
```

### 17.3.9 实现端口转发

当 Ubuntu 系统作为内部计算机系统的互联网网关时，端口转发与伪装配合使用。端口转发允许通过互联网从特定端口到达防火墙的流量转发到内部网络上的特定系统。这通过示例来描述可能是最好的方式。

假设一个 Ubuntu 系统作为内部计算机网络的防火墙，且网络上的一个系统被配置为 Web 服务器。假设该 Web 服务器系统的 IP 地址为 `192.168.2.20`。托管在该系统上的网站的域名记录配置了 Ubuntu 防火墙系统背后的公网 IP 地址。当 HTTP Web 页面请求到达端口 80 时，作为防火墙的 Ubuntu 系统需要知道如何处理它。通过配置端口转发，可以将所有 Web 流量引导到托管 Web 服务器的内部系统（在这种情况下，IP 地址为 `192.168.2.20`），可以继续使用端口 80，也可以将流量重定向到目标服务器上的不同端口。事实上，端口转发甚至可以配置为将流量转发到防火墙所在系统上的不同端口（这一概念被称为本地转发）。

要使用端口转发，首先按照以下方式启用伪装（在这种情况下，假设连接到互联网的接口已分配给外部区域）：

```bash
firewall-cmd --zone=external --add-masquerade
```

要从一个端口转发到另一个不同的本地端口，将使用类似下面的命令：

```bash
firewall-cmd --zone=external --add-forward-port=port=22:proto=tcp:toport=2750
```

在上面的示例中，任何到达端口 22 的 TCP 流量将将转发到本地系统的端口 2750。另一方面，以下命令将本地系统上的端口 20 转发到 IP 地址为 `192.168.0.19` 的系统的端口 22：

```bash
firewall-cmd --zone=external \
             --add-forward-port=port=20:proto=tcp:toport=22:toaddr=192.168.0.19
```

同样，以下命令将本地端口 20 转发到 IP 地址为 `192.168.0.18` 的系统的端口 2750：

```bash
firewall-cmd --zone=external --add-forward-port=port=20:proto=tcp:toport=2750:toaddr=192.168.0.18
```

### 17.4 使用 firewall-config 管理 firewalld

如果您可以访问图形桌面环境，还可以使用 `firewall-config` 工具配置防火墙。虽然默认没有安装，但可以通过以下方式安装 `firewall-config`：

```bash
apt install firewall-config
```

启动后，会出现主 `firewall-config` 界面，如图 17-1

图 17-1

该工具的关键区域可以总结如下：

**A** - 显示所有当前活动的接口以及它们所属的区域。要将接口分配到不同的区域，请从此面板中选择它，点击 Change Zone（更改区域）按钮并从生成的对话框中选择所需的区域。

**B** - 控制显示的信息和任何更改是应用于运行时还是永久规则。

**C** - 系统上配置的区域、服务或 IPSets 列表。此面板的内容取决于 F 的选择。

**D** - 包含 E 内容的主面板。在此示例中，显示的是公共区域的服务。每个服务旁边的复选框控制该服务是否启用。可以在这些类别面板中添加或删除规则。

**E** - 控制 D 的内容。

**F** - 控制 C 的列表。

`firewall-config` 工具简单直观易于使用，允许在图形环境中完成可以使用 `firewall-cmd` 的许多任务。

### 17.5 总结

精心规划和实施的防火墙是任何安全系统的重要组成部分。在 Ubuntu 的情况下，firewalld 服务提供了一个灵活且易于管理的防火墙系统。

## 18. 在 Ubuntu 上配置 SSH 密钥认证

当 Ubuntu 系统首次安装时，默认未配置通过 Secure Shell（SSH）连接进行远程命令行访问。安装后，SSH 为 root 账户以及安装期间添加的任何其他用户提供密码保护和加密访问。这种安全性水平远不够，应尽快升级为 SSH 密钥认证。

本章将概述通过实施密钥对认证来增加 Ubuntu 系统安全性的步骤。

### 18.1 Secure Shell (SSH) 概述





SSH 设计用于允许安全地远程访问系统，以获取 shell 访问并传输文件和数据。正如在“使用 Vino 进行 Ubuntu 桌面访问” 中介绍的，SSH 还可以用于提供一个安全隧道，通过网络连接实现远程访问 GNOME 桌面。

基础 SSH 配置由一个客户端（用于建立连接的计算机）和一个服务器（运行在要连接的系统上）组成。例如，用户可以使用运行在 Linux、Windows 或 macOS 系统上的 SSH 客户端连接到运行在 Ubuntu 系统上的 SSH 服务器，以获取 shell 命令行提示的访问或执行文件传输。客户端与服务器之间的所有通信（包括为了访问而输入的密码）都经过了加密，以防止第三方截获数据。

基础 SSH 实现的固有弱点是它完全取决于分配给系统账户的密码强度。如果恶意方能够识别出账户的密码（无论是通过猜测、欺骗还是暴力攻击），系统就会变得脆弱。通过实施 SSH 密钥身份验证，可以解决这一弱点。

### 18.2 SSH 密钥身份验证

SSH 密钥身份验证利用非对称公钥加密为远程系统访问增加了一层额外的安全性。公钥加密的概念由 Whitfield Diffie 和 Martin Hellman 于 1975 年发明，它基于使用一对密钥（一个私钥和一个公钥）的概念。

在公钥加密系统中，公钥用于加密数据，而数据只能由私钥的所有者进行解密。

在 SSH 密钥身份验证的情况下，私钥由位于 SSH 客户端所在的主机持有，而相应的公钥则位于运行 SSH 服务器的系统上。保护私钥至关重要，因为密钥的所有权将允许任何人登录远程系统。因此，作为额外的保护层，私钥还可以被加密并由密码保护，每次建立与服务器的连接时必须输入该密码。

### 18.3 设置密钥身份验证

设置 SSH 密钥身份验证有四个步骤，可以总结如下：

1. 生成公钥和私钥。
2. 将公钥安装到服务器上。
3. 测试身份验证。
4. 在服务器上禁用基于密码的身份验证。

本章的其余部分将为 Linux、macOS 和 Windows 客户端操作系统详细概述这些步骤。

### 18.4 安装并启动 SSH 服务

如果系统尚未安装并运行 SSH 服务器，可以使用以下命令添加：

```bash
apt install openssh-server
```

```bash
systemctl start sshd.service
```

```bash
systemctl enable sshd.service
```

### 18.5 从 Linux 和 macOS 客户端进行 SSH 密钥身份验证

设置 SSH 密钥身份验证的第一步是在客户端系统上生成密钥对。如果客户端系统运行 Linux 或 macOS，则可以使用 `ssh-keygen` 工具实现：

```bash
ssh-keygen
```

这将产生类似下方的输出：

```
Generating public/private rsa key pair.
Enter file in which to save the key (/home/<username>/.ssh/id_rsa):
按 Enter 键接受密钥文件的默认位置。这将在当前用户主目录下的 .ssh 子目录下放置两个文件。私钥将存储在名为 `id_rsa` 的文件中，而公钥将保存在命为 `id_rsa.pub` 的文件中。
```

接下来，`ssh-keygen` 将提示输入短语（passphrase）以保护私钥。如果提供了短语，则私钥将在本地磁盘上被加密，并且在访问远程系统时需要该短语。为了更好的安全，建议使用短语。

```
Enter passphrase (empty for no passphrase):
```

最后，`ssh-keygen` 工具将生成以下输出，表示密钥已生成：

```
Your identification has been saved in /home/neil/.ssh/id_rsa.
Your public key has been saved in /home/neil/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:FOLGWEEGFIjWnCT5wtTOv5VK4hdimzWghZizUEMYbfo <username>@<hostname>
The key’s randomart image is:
+---[RSA 2048]----+
|.BB+=+*.. |
|o+B= * . . |
|===.. + . |
|*+ * . . |
|.++ o S |
|..E+ * o |
| o B * |
| + + |
| . |
+----[SHA256]-----+
```

下一步是将公钥安装到远程服务器系统上。可以使用 `ssh-copy-id` 工具按照如下方式实现：

```bash
ssh-copy-id username@remote_hostname
```

例如：

```bash
ssh-copy-id neil@192.168.1.100
```

```
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/neil/.ssh/id_rsa.pub"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
neil@192.168.1.100's password:
```

```
Number of key(s) added: 1
```

现在测试身份验证是否有效：

```bash
ssh <username><hostname>
```

### 18.6 管理多个密钥

存在多个私钥并不常见，每个密钥访问不同的服务器。在建立连接时，有多种选项可以选择特定的密钥。例如，可以在启动 `ssh` 客户端时指定要使用的私钥文件如下：

```bash
ssh -l neilsmyth -i ~/.ssh/id_work 35.194.18.119
```

或者，可以使用 SSH 客户端用户配置文件将密钥文件与服务器关联。配置文件名为 `config`，必须位于用户主目录下的 `.ssh` 目录，并可用于配置各种选项，包括私钥文件、连接时使用的默认端口、默认用户名以及引用服务器的快捷别名。以下示例配置文件为两个服务器定义了不同的密钥文件，并通过 `home` 和 `work` 别名进行引用。

```text
Host work
  HostName 35.194.18.119
  IdentityFile ~/.ssh/id_work
  User neilsmyth

Host home
  HostName 192.168.0.21
  IdentityFile ~/.ssh/id_home
```





```bash
$ ssh -l neilsmyth -i ~/.ssh/id_work 35.194.18.119
```

现在，命令可以缩短为如下：

```bash
$ ssh work
```

运行以下命令可以找到配置文件选项的完整列表：

```bash
$ man ssh_config
```

### 18.7 来自 Windows 10 客户端的 SSH 密钥认证

最近版本的 Windows 10 包含了 OpenSSH 实现的一个子集，大多数 Linux 和 macOS 系统作为 Windows PowerShell 部分使用它。这允许通过与上述 Linux 和 macOS 类似的步骤，在 Windows 10 客户端上设置 SSH 密钥认证。

在 Windows 10 系统上打开 Windows PowerShell，请按下 `Win+X` 组合键并从菜单中选择，或者从开始菜单中找到并选择它。运行后，PowerShell 窗口将如 图 18-1 所示：

![](img/windows_10_powwershell.jpg)

图 18-1

如果你已经从另一个客户端系统拥有一个私钥，只需将 `id_rsa` 文件复制到 Windows 10 系统上名为 `.ssh` 的文件夹中。一旦文件到位，在 PowerShell 窗口中按如下方式测试认证：

```bash
$ ssh -l <username>@<hostname>
```

例如：

```bash
PS C:\Users\neil> ssh -l neil 192.168.1.101
```

`Enter passphrase for key 'C:\Users\neil/.ssh/id_rsa':`

在提示时输入密码短语并完成认证过程。

如果不存在现有的私钥，请在 PowerShell 窗口中使用 `ssh-keygen` 工具生成一组新的私钥和公钥对，步骤与为 Linux 和 macOS 说明的步骤相同。密钥生成后，它们将再次位于当前用户主目录下的 `.ssh` 目录中，公钥文件 `id_rsa.pub` 需要安装在远程 Ubuntu 系统上。遗憾的是，Windows PowerShell 并不包含 `ssh-copy-id` 工具，因此此任务需要手动完成。

在 PowerShell 窗口中，切换目录到 `.ssh` 子目录并显示公钥文件 `id_rsa.pub` 的内容：

```bash
PS C:\Users\neil> cd .ssh
PS C:\Users\neil\.ssh> type id_rsa.pub
```

```text
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDFgx1vzuzu59lll6/uQw7FbmKVsQ3fzLz9MW1fgo4sdsxXp81wCHNAlqcjx1Pgr9BJPXWUMInQOi7BQ5I+vc2xQ2AS0kMq3ZH9ybWuQe/U2GjueXZd0FKrEXrT55wM36Rm6Ii3roUCoGCzGR8mn95JvRB3VtCyDdzTWSi8JBPK5gV5oOxNTNPsewlLzouBlCT1qW3CKwEiIwu8S9MTL7m3nrcaNeLewTTHevvHw4QDwzFQ+B0PDg96fzsYoTXVhzyHSWyo6H0gqrft7aK+gILBtEIhWTkSVEMAzy1piKtCr1IYTmVK6engv0aoGtMUq6FnOeGp5FjvKkF4aQkh1QR28r neil@DESKTOP-S8P8D3N
```

高亮文件内容并使用快捷键 `Ctrl-C` 将其复制。

留在 PowerShell 窗口中，使用密码认证登录远程系统：

```bash
PS C:\Users\neil\.ssh> ssh -l <username> <hostname>
```

登录后，检查是否存在 `.ssh` 子目录。如果不存在，按如下方式创建它：

```bash
$ mkdir .ssh
```

切换目录到 `.ssh` 并检查是否已名为 `authorized_keys` 的文件。如果不存在，创建它并将来自 Windows 10 系统的公钥文件内容粘贴其中。

如果 `authorized_keys` 文件已存在，它很可能已经包含了其他密钥。如果是这样，编辑该文件并将新的公钥粘贴在文件末尾。例如，以下文件包含两个密钥：

```text
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCzRWH27Xs8ZA5rIbZXKgxFY5XXauMv+6F5PljBLJ6j+9nkmykVe3GjZTp3oD+KMRbT2kTEPbDpFD67DNL0eiX2ZuEEiYsxZfGCRCPBGYmQttFRHEAFnlS1Jx/G4W5UNKvhAXWyMwDEKiWvqTVy6syB2Ritoak+D/Sc8nJflQ6dtw0jBs+S7Aim8TPfgpi4p5XJGruXNRScamk68NgnPfTL3vT726EuABCk6C934KARd+/AXa8/5rNOh4ETPstjBRfFJ0tpmsWWhhNEnwJRqS2LD0ug7E3yFI2qsNKGEzvAYUC8Up45MRP7liR3aMlCBil1tsy9
```

## 18.9 使用 PuTTYgen 生成私钥

上一节探讨了在使用 PuTTY 时现有私钥和公钥的使用。如果密钥不存在，可以使用 `PuTTYgen` 工具创建，该工具包含在 PuTTY 主程序中。

要创建新密钥，启动 PutyGen 并点击 图 18-4 中高亮的 Generate 按钮：

![](img/windows_puttygen_main1.jpg)

图 18-4





按照指示移动鼠标指针以生成随机数据，然后输入一个可选的口令来加密私钥。一旦生成密钥，请使用 `Save public key`（保存公钥）和 `Save private key`（保存私钥）按钮将文件保存到合适的位置。如上一节所述，私钥可以在 `PuTTY`中使用。要在远程服务器上安装公钥，请参考前面的章节中关于在 Windows 10 的 PowerShell 中使用 SSH 介绍的步骤。

### 18.10 为 Google Cloud 实例安装公钥

如果你的 Ubuntu 系统托管在 Google Cloud 上（例如作为 Compute Engine 实例），有多种不同的方法可以使用基于密钥的身份验证获取 SSH 访问。可能最简单的方法是将你的公钥添加到 Google Cloud 账户的元数据（Metadata）中。这将使得公钥对你在 Google Cloud 内部创建的所有虚拟机实例都可用。要添加公钥，请登录 Google Cloud Platform 控制台，从左侧导航面板中选择如图 18-5 所示的高亮的 `Metadata` 选项，然后点击 `SSH keys` 选项卡：

![](img/google_cloud_ssh_key_list.jpg)

图 18-5

在 SSH Keys 屏幕上，点击 `Edit` 按钮（如图 18-5 所示的高亮显示）来编辑密钥列表。滚动到当前列表底部并点击 `+ Add Item` 按钮。将出现一个新字段，你需要将 `id_rsa.pub` 文件中显示的完整公钥粘贴到其中。输入密钥后，点击 `Save` 按钮添加密钥。

公钥现在将显示在 SSH Keys 列表中。请注意，该密钥条目还包含用户名，在登录任何 Google Cloud 实例时必须使用该用户名：

![](img/google_cloud_ssh_key_added.jpg)

图 18-6

一旦将公钥添加到元数据中，理论上就可以从任何安装了相应私钥且拥有该用户账户的客户端访问任何虚拟机实例。事实上，在幕后，Google Cloud 为实现这一点所做的唯一工作，是将公钥添加到任何存在该账户的虚拟机家目录下的 `.ssh/authorized_keys` 文件中。

### 18.11 总结

对 Ubuntu 系统的任何远程访问都必须以提供高安全性的方式来实现。默认情况下，SSH 允许使用基于密码的身份验证进行远程系统访问。这使得系统对于任何能够猜到密码或其他手段获取密码的人来说变得脆弱。因此，建议使用基于密钥的身份验证来保护系统访问。基于密钥的身份验证使用了涉及公钥和私钥的公钥加密概念。实施后，用户只有在使用的客户端私钥与服务器上的公钥匹配时，才能连接到服务器。作为额外的安全层，私钥还可以被加密并进行密码保护。一旦实现了基于密钥的加密，服务器系统将会被配置为禁用安全性较低的基于密码的身份验证。

本章概述了 SSH 基于密钥的身份验证，并概述了在 macOS、Linux 和 Windows 上生成密钥和配置客户端的步骤，此外还有在 Ubuntu 服务器上安装和管理公钥的方法。

## 19. 使用 Vino 进行 Ubuntu 远程桌面访问

可以配置 Ubuntu 以通过网络或互联网连接提供图形化桌面环境的远程访问。虽然默认未启用，但从网络或互联网上的任何其他系统显示并访问 Ubuntu 桌面是相对简单的。无论该系统运行的是 Linux、Windows 还是 macOS，都可以实现这一点。事实上，甚至有适用于 Android 和 iOS 的应用程序，允许你在几乎任何有数据信号的地方访问 Ubuntu 桌面。

远程桌面访问在许多场景下都非常有用。它允许你或他人（例如）从同一网络或互联网上的另一台计算机系统查看并与你的 Ubuntu 桌面环境交互。当你离开座位（例如旅行时）需要使用电脑工作时，这非常有用。在同事或 IT 支持人员需要访问你的桌面来解决问题的情况下，它同样有用。

Ubuntu 远程桌面功能基于名为虚拟网络计算（`VNC`）的技术，在本章和下一章中，我们将涵盖在 Ubuntu 内配置和使用远程桌面的关键方面。

### 19.1 远程桌面访问类型

在开始之前，了解本质上有两种类型的远程桌面访问是非常重要的。本章涵盖的方法对于你主要将 Ubuntu 作为桌面操作系统并需要对你常用的桌面会话进行远程访问的情况非常有用。配置完成后，你将接管你的桌面会话并远程对其进行查看和控制。

第二种选择将在下一章（标题为 [ ]）中介绍，它适用于需要在基于服务器的远程系统上启动并访问一个或多个远程桌面会话的情况，无论远程系统是否连接了图形控制台。这允许你在远程系统的后台启动多个桌面会话，并通过网络或互联网连接对这些桌面进行查看和控制。

### 19.2 安全与不安全的远程桌面访问

在本章中，我们将涵盖安全和不安全的远程桌面访问方法。假设你是在安全内部网络的上下文中从一个系统访问另一个系统，那么使用不安全的访问方法通常是安全的。反之，如果你计划通过任何公共网络远程访问你的桌面，则必须使用安全的访问方法，以避免你的系统和数据受到破坏。

### 19.3 在 Ubuntu 上启用远程桌面访问

Ubuntu 的远程桌面访问由 `Vino` 包提供。`Vino` 是一个专为 GNOME 桌面开发的 VNC 服务器。

启用远程访问的第一步是安装此包：

```
apt install vino
```

安装 `Vino` 后，下一步是在 GNOME 内部启用远程桌面访问。首先打开如图 19-1 所示的设置程序：

![](img/ubuntu_20.04_gnome_settings.jpg)

图 19-1

在设置应用程序中，选择 `Sharing` 选项（如图 19-2 所示的 A）：

![](img/ubuntu_20.04_gnome_remote_desktop_setting.jpg)

图 19-2

打开 `Sharing` 开关（B）并点击 `Screen Sharing` 选项（C），显示下方图 19-3 所示的对话框：

![](img/ubuntu_20.04_gnome_screen_sharing_preferences.jpg)

图 19-3

Screen Sharing 对话框提供了以下配置选项来管理远程桌面访问：

- `允许连接控制屏幕`：如果启用，远程会话将可以使用鼠标和键盘与桌面环境进行交互。如果禁用，远程会话将仅允许查看桌面。
- `新连接必须请求访问权限`：当选中此项时，主机屏幕上将弹出一个提示，询问是否允许远程用户访问桌面。如果你计划远程访问屏幕且主机系统旁没有人接受连接请求，则请勿选择此选项。
- `需要密码`：要求用户在访问桌面之前输入指定的密码。





- `Networks`: 允许远程访问的主机系统上的网络连接。

配置好设置后，关闭“屏幕设置”和“设置”对话框。

### 19.4 连接到共享桌面

虽然许多操作系统都有 VNC 查看器实现，但当从 Ubuntu 或其他基于 Linux 的系统连接时，建议使用 Remmina 客户端等工具。`Remmina` 是一个具有图形界面的友好工具，它支持 `Vino` 使用的加密，以确保远程连接的安全。

要安装此工具，打开 Ubuntu 软件应用程序，搜索并安装 `Remmina`：

![](img/ubuntu_20.04_install_remmina.jpg)

图 19-4

安装并启动 `Remmina` 后，将连接类型菜单（在图 19-5 中标记为 A）更改为 `VNC`，并在地址字段 (B) 输入要连接的远程系统的 IP 地址或主机名：

![](img/ubuntu_20.04_remmina_main.jpg)

图 19-5

要建立连接，按下键盘上的 `Enter` 键开始连接过程。稍等后，将出现第二个屏幕，请求桌面访问密码（如果在在本章较早启用屏幕共享时输入了密码）：

![](img/ubuntu_20.04_remmina_password.jpg)

图 19-6

输入密码后，点击 `OK` 访问远程屏幕：

![](img/ubuntu_20.04_remmina_running.jpg)

图 19-7

`Remmina` 的默认设置优先考虑速度而非图像质量。如果您发现桌面渲染质量差到无法接受，请点击远程查看器窗口中左侧工具栏中的设置按钮（图 19-8），并尝试不同的设置，直到找到性能与图像质量之间的理想平衡：

![](img/ubuntu_20.04_remmina_quality.jpg)

图 19-8

### 19.5 从非 Linux 客户端连接

上一节假设是从 Linux 或 UNIX 系统访问远程桌面的。需要理解的是，`Vino` 默认要求远程连接必须加密以确保安全。使用 `Remmina` 的原因之一是它完全支持 `Vino` 使用的加密。

如果您需要从 Windows 或 macOS 等非 Linux 系统连接，则需要安装第三方 `VNC` 查看器，例如 `TightVNC`、`TigerVNC` 或 `RealVNC`。遗憾的是，这些查看器不支持 `Vino` 默认使用的加密。要体验此操作，请从以下 URL 下载适用于 macOS 或 Windows 系统的 `RealVNC` 查看器：

[`www.realvnc.com/en/connect/download/viewer/`](https://www.realvnc.com/en/connect/download/viewer/)

安装完成后，启动查看器并输入您的远程 Ubuntu 系统的主机名或 IP 地址。尝试连接时，将出现类似于图 19-9 所示的失败对话框：

![](img/ubuntu_18.04_vnc_encyption_not_supported.jpg)

图 19-9

为了允许从非 Linux 系统建立连接，必须关闭远程桌面连接的加密要求。要执行此操作，请 Ubuntu 系统上打开终端窗口并运行以下命令（使用您的账户且不带 `sudo` 权限）：

```bash
gsettings set org.gnome.Vino require-encryption false
```

在禁用 `Vino` 加密要求后，再次尝试从 `RealVNC` 查看器连接。此时将出现一个警告，指示连接未加密：

![](img/ubuntu_18.04_vnc_not_encypted.jpg)

图 19-10

点击 `Continue` 按钮将关闭警告对话框并建立远程连接。

很显然，使用本节中的步骤连接到远程 `VNC` 服务器会导致客户端和服务器之间产生不安全的、未加密的连接。这意味着在远程会话期间传输的数据容易被截获。若要从 Ubuntu 系统到非 Linux 客户端建立安全且加密的连接，还需要额外的步骤。

### 19.6 建立安全的远程桌面会话

上一节中 macOS 和 Windows 的远程桌面连接被认为是不安全的，因为没有使用加密。当远程连接不延伸到防火墙保护的内部网络之外时，这是可以的。然而，当需要在互联网连接上进行远程会话时，则需要更安全的选项。这可以通过安全外壳 (`SSH`) 连接对远程桌面进行隧道来实现。本节将介绍如何在 Linux、UNIX 和 macOS 客户端上执行此操作。

当 Ubuntu 系统上调用远程桌面会话时，将使用 `TCP/IP` 网络端口 `5900` 建立。为了证明这一点，在主机名或 IP 地址之后引用端口 `5900` 连接到您的远程 Ubuntu 系统，并注意连接仍然建立：

`192.168.86.218:5900`

为非 Linux 系统实现加密的远程桌面会话。

如果您的 Ubuntu 系统上尚未安装 SSH 服务器，请参阅标题为“在 Ubuntu 上配置基于密钥的 SSH 身份验证 的章节。

假设 SSH 服务器已安装并运行，是时候到另一个系统了。在另一个系统上，使用以下命令登录远程系统，这将建立两个系统之间的安全隧道。这假设客户端系统正在运行 macOS、Linux 或 UNIX（Windows 系统的说明将在下一节介绍）：

```bash
ssh -l <username> -L 5900:localhost:5900 <remotehost>
```

在上面的示例中，`<username>` 指配置了 `VNC` 访问的远程用户账户，`<remotehost>` 是远程系统的主机名或 IP 地址，例如：

```bash
ssh -l demo -L 5900:localhost:5900 192.168.86.218
```

在提示时，使用账户密码登录。安全连接建立后，是时候启动 `vncviewer` 以使用安全隧道了。在终端窗口中保留 `SSH` 会话，启动 `vnc viewer` 并在地址字段输入以下内容：

`localhost:5900`

如果需要，`vncviewer` 会话将提示密码，然后启动 `vnc viewer` 为您的桌面提供安全访问。





如果你是从防火墙外部连接到远程桌面，请记住 SSH 连接的 IP 地址将是你的 ISP 或云托管提供商提供的外部 IP 地址，而不是远程系统的局域网（LAN）IP 地址（该地址对于防火墙外的人是不可见的）。你还需要配置防火墙，将端口 `22`（用于 SSH 连接）转发到运行桌面的系统 IP 地址。没有必要转发端口 `5900`。执行端口转发的步骤在不同防火墙之间有所不同，请参考你的防火墙、路由器或无线基站的文档以获取适用于你配置的详细信息。

### 19.7 使用 PuTTY 在 Windows 上建立安全隧道

从 Windows 系统到 Ubuntu 服务器建立安全桌面会话也采用了类似的方法。假设你已经安装了如 `TightVNC` 等 VNC 客户端，剩余的唯一要求是一个 Windows SSH 客户端（在本例中为 `PuTTY`）。

一旦下载并安装 `PuTTY`，第一步是在配置适当隧道的情况下，在 Windows 系统与远程系统之间建立安全连接。启动 `PuTTY` 后，将显示以下屏幕：

![](img/rhel_8_vnc_putty_main.jpg)
图 19-11

输入远程主机的 IP 地址或主机名（如果你是从防火墙外部连接，请输入网关的外部 IP 地址）。下一步是设置隧道。点击对话框左侧 `Category` 树中 `SSH` 旁的 `+` 号，并点击 `Tunnels`。随后屏幕应显示如下：

![](img/rhel_8_vnc_putty_tunnels.jpg)
图 19-12

在 `Source port` 中输入 `5900`，在 `Destination` 中输入 `localhost:5900`，然后点击 `Add` 按钮。最后，通过点击 `Session` 类别返回主界面。在 `Saved Sessions` 文本字段中为会话输入名称并按 `Save`。点击 `Open` 建立连接。将出现一个终端窗口，显示来自远程系统的登录提示。输入相应的用户登录凭据和密码。

现在 SSH 连接已建立。启动 VNC 查看器，在 `VNC Server` 文本字段中输入 `localhost:5900` 并点击 `Connect`。查看器将建立连接、提示输入密码并显示桌面。你现在正在通过安全的 SSH 隧道从 Windows 访问 Linux 系统的远程桌面。

### 19.8 总结

可以通过虚拟网络计算（VNC）启用对 Ubuntu 系统 GNOME 桌面环境的远程访问。VNC 由运行在远程服务器上的 VNC 服务器和本地主机上相应的客户端组成，允许远程访问运行在服务器上的多个桌面实例。

GNOME 桌面的标准远程服务器解决方案是 `Vino`。一旦安装，就可以使用 `Remmina` 等远程桌面查看器从其他 Linux 系统建立远程桌面会话。

当从 Windows 或 macOS 等非 Linux 系统连接时，有必要禁用 `Vino` 的加密要求。禁用后，应使用 SSH 隧道建立来自客户端系统的连接。

当在禁用 `Vino` 加密的情况下通过公共连接使用 VNC 连接时，建议在连接时使用 SSH 隧道，以确保客户端与服务器之间的通信加密且安全。

## 20 使用 VNC 访问 Ubuntu 远程桌面

标题为 “Ubuntu Remote Desktop with Vino” 的章节探讨了使用 `Vino` 服务器远程访问 Ubuntu GNOME 桌面，这种方法仅适用于远程系统已运行 GNOME 桌面会话的情况。在本章中，我们将介绍启动和访问在后台运行的 GNOME 桌面会话，允许远程访问多个桌面会话，包括未连接图形控制台的服务器级系统。

### 20.1 安装 GNOME 桌面环境

当然，只有在安装了桌面本身的情况下才可以访问桌面环境。例如，如果系统最初配置为服务器，则可能没有安装桌面包。安装运行 GNOME 桌面所需包的最简单方法是通过以下 `apt` 命令：

```bash
apt install ubuntu-gnome-desktop
```

为了防止桌面在每次系统重启时尝试自动启动，请将默认的 `systemd` 目标改回 `multi-user`：

```bash
systemctl set-default multi-user.target
```

如果系统连接了图形显示器，可以使用以下命令启动桌面：

```bash
startx
```

反，如果系统是没有直接连接显示器的服务器，运行和访问桌面的唯一方法是在系统上配置 VNC 支持。

### 20.2 在 Ubuntu 上安装 VNC

访问远程桌面需要在远程系统上安装 VNC 服务器，在建立连接的系统中安装 VNC 查看器，并可选一个安全的 SSH 连接。虽然有多种 VNC 服务器和查看器实现，但本章将使用 `TigerVNC`，它为基于 Linux 的操作系统提供了服务器和查看器组件。非 Linux 平台的 VNC 查看器客户端包括 `RealVNC` 和 `TightVNC`。

要在 Ubuntu 上安装 `TigerVNC` 服务器包，只需运行以下命令：

```bash
apt install tigervnc-standalone-server
```

如果需要，也可以如下所示安装 `TigerVNC` 查看器：

```bash
apt install tigervnc-viewer
```

一旦安装了服务器，系统需要配置运行一个或多个 VNC 服务并在防火墙上开启端口。

### 20.3 配置 VNC 服务器

安装 VNC 服务器包后，下一步是配置服务器。第一步是为访问远程的用户指定密码。以 root 登录（或具有超级用户权限），执行 `vncpasswd` 命令（假设用户名为 `demo`）：

```bash
su - demo
demo@demos~$ vncpasswd
Password:
Verify:
Would you like to enter a view-only password (y/n)? n
A view-only password is not used
```

上述命令会在用户的 `.vnc` 目录下创建一个名为 `passwd` 的文件。接下来，进入 `.vnc` 目录并创建一个名为 `xstartup` 的文件，内容如下：

```bash
#!/bin/sh
# Start Gnome 3 Desktop
[ -x /etc/vnc/xstartup ] && exec /etc/vnc/xstartup
[ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources
vncconfig -iconic &
dbus-launch --exit-with-session gnome-session &
```

这些是在启动 VNC 服务器时将执行以启动 GNOME 桌面的命令。

### 20.4 启动 VNC 服务器

以用户身份运行且无超级用户权限：

```bash
vncserver
```

这将启动系统上的第一个桌面会话。由于这是第一个会话，它将被配置使用端口 `5901`（可以简写为 `:1`）。在第一个会话运行时再次运行该命令将在端口 `5902` (:2) 上创建一个 VNC 服务器。可以使用以下命令获取当前运行的桌面会话列表：

```bash
vncserver -list
```
TigerVNC server sessions:
X DISPLAY # PROCESS ID
:1 1607
:2 4726

要终止会话，使用 `vncserver` 命令配合 `-kill` 选项引用相应的端口。例如：

```bash
vncserver -kill :2
```
Killing Xtigervnc process ID 4726... success!

或者，使用以下命令杀死所有当前运行的 VNC 服务器会话：

```bash
vncserver -kill :*
```
Killing Xtigervnc process ID 1607... success!
Killing Xtigervnc process ID 5287... success!





要手动指定 VNC 服务器会话使用的端口，请在命令行中包含如下所示的数字：

```bash
vncserver :5
```

在上述示例中，会话将在端口 `5905` 上监听远程连接。

### 20.5 连接到 VNC 服务器

有关如何从另一个系统远程连接到桌面会话的详细信息，请遵循上一章中标题为“建立安全的远程桌面会话和“在 Windows 上使用 PuTTY 建立安全隧道的节概述步骤。

### 20.6 总结

在本章和前一章中，我们探索了两种远程访问 Ubuntu 系统 GNOME 桌面环境的方法。前一章探索了对现有桌面会话的访问，而本章侧重于将 GNOME 桌面会话作为后台进程启动，从而允许远程访问多个桌面会话。对于在“无显示器”服务器系统上运行和远程访问桌面会话来说，这是一种特别实用的技术。

## 21 远程显示 Ubuntu （X11 转发）

在上一章中，我们查看了如何在远程计算机上显示整个 Ubuntu 桌面。虽然当你实际上需要远程显示整个桌面时这种方法很好用，但如果你只想显示单个应用程序，这可能被认为大材小用。因此，在本章中，我们将查看如何在远程系统上显示单个应用程序。

### 21.1 远程显示 Ubuntu 应用程序的要求

为了在一个 Ubuntu 系统上运行应用程序并在另一个系统上显示它，需要满足几个前提条件。首先，显示应用程序的系统必须运行 X 服务器。如果该系统是运行着桌面环境的 Linux 或类 Unix 系统，则没有问题。然而，如果系统运行的是 Windows 或 macOS，则你必须在从远程系统显示应用程序之前在上面安装 X 服务器。此用途有许多商业和免费的 Windows 版 X 服务器可供选择，网页搜索可以为你提供选项列表。

其次，运行应用程序的系统（而不是显示应用程序的系统）必须配置为允许 SSH 访问。在 Ubuntu 系统上配置 SSH 的详细信息可以在标题为在 Ubuntu 上配置基于密钥的身份验证的章节中找到。该系统必须运行来自 `X.org` 的 X Window 系统而不是 `Wayland`。要确定使用的是哪种系统，请运行：

```bash
echo $XDG_SESSION_TYPE
```

如果上述命令输出 `wayland` 而不是 `x11`，请编辑 `/etc/gdm3/custom.conf` 文件并取消内容的注释：

```text
Wayland=false
```

最后，SSH 必须配置为允许转发。这通过编辑 `/etc/ssh/sshd_config` 文件并取消取消注释来实现：

```text
X11Forwarding yes
```

进行更改后，重启服务：

```bash
systemctl restart sshd
```

### 21.2 远程显示 Ubuntu 应用程序

远程显示应用程序的第一步是运行 X 服务器。安装 X 服务器后，将出现一个名为 `XLaunch` 的应用程序。启动 `XLaunch` 并选择一个显示选项（最灵活的是 `Multiple windows` 选项）。

一旦运行，`XLaunch` 将出现在任务栏中。启动 PuTTY，输入远程主机的连接信息或加载以前保存的会话配置。在建立连接之前，需要启用 X11 转发。

```bash
ssh -X user@hostname
```

登录后，后续输出应类似于以下内容：

```text
localhost:10.0
```

### 21.3 可信 X11 转发

可信 X11 转发比不可信转发稍快，但安全性较低。要使用可信转发，请使用 `-Y` 标记：

```bash
ssh -Y user@hostname
```

### 21.4 压缩 X11 转发

当使用较慢的连接时，可以使用 `-C` 标记压缩 X11 数据以提高性能：

```bash
ssh -C user@hostname
```

### 21.5 在 Windows 上显示 Ubuntu 

要在 Windows 上显示 Ubuntu 应用，需要安装 SSH 客户端和 X 服务器。在 X 服务器方面，流行的选择似乎是 `VcXsrv`，可以从此处免费获取：`https://sourceforge.net/projects/vcxsrv/`。

一旦安装了 `VcXsrv`，桌面上会出现 `XLaunch`。启动 `XLaunch` 并选择显示选项。如果出现 Windows Defender 对话，点击按钮允许访问你所选的网络。





在 `PuTTY` 会话窗口中登录 Ubuntu 系统并运行一个桌面应用程序。稍等片，该程序将以独立窗口的形式出现在 Windows 桌面上。该程序打开的任何对话框也将出现在独立的窗口中，就像它们在 Ubuntu GNOME 桌面上显示的一样。例如，图 21-5 显示了在 Windows 10 系统上显示的 Ubuntu `nm-connection-editor` 工具：

![](img/win_10_xserver_app_displayed.jpg)

图 21-5

### 21.6 总结

对于需要远程访问单个 Ubuntu 桌面应用程序而非整个 GNOME 桌面的情况，X11 转发为远程显示图形应用程序提供了一种轻量级的解决方案。显示应用程序的系统必须运行基于 X Window 系统的桌面环境（如 `GNOME`），或者已安装并运行 X 服务器。一旦在远程服务器上启用了 X11 转发，并从本地系统使用 X11 转发选项建立了安全的 `SSH` 连接，大多数应用程序就可以在本地 X 服务器上远程显示。

## 22. 使用 NFS 与远程系统共享 Ubuntu 文件

Ubuntu 提供了两种机制与网络上的其他系统共享文件和文件夹。一种方法是使用名为 `Samba` 的技术。`Samba` 基于 Microsoft Windows 文件夹共享，允许 Linux 系统让 Windows 系统可以访问文件夹，并允许从 Linux 访问基于 Windows 的文件夹共享。这种方法也可用于在其他 Linux 和 UNIX 系统之间共享文件夹，只要这些系统也安装并配置了 `Samba` 支持。这目前是异构网络环境中共享文件夹最流行的方法。使用 `Samba` 共享文件夹的主题在 使用 Samba 在 Ubuntu 和 Windows 系统之间共享文件 中有所介绍。

另一个专门针对 Linux 和 UNIX 系统之间共享文件夹的选项使用了名为网络文件系统（`NFS`）的技术。`NFS` 允许另一台 Linux 或 UNIX 系统通过网络连接访问一台 Linux 计算机上的文件系统。`NFS` 由 Sun Microsystems（现属于 `Oracle Corporation`）于 20 世纪 80 年代开发，至今一直是共享远程 Linux/UNIX 文件系统的标准机制。

`NFS` 与 `Samba` 使用的 Windows SMB 资源共享技术非常不同。在本章中，我们将学习使用 `NFS` 在 Ubuntu 与其他 UNIX/Linux 系统之间进行基于网络的文件夹共享。

### 22.1 确保 NFS 服务在 Ubuntu 上运行

首要任务是验证你的 Ubuntu 系统上是否安装并运行了 `NFS` 服务。这可以通过命令行实现，也可以使用 `Cockpit` 界面实现。

首先通过在终端窗口运行以下命令安装 `NFS` 服务：

```bash
apt install nfs-kernel-server
```

接下来，配置服务在启动时自动启动：

```bash
systemctl enable nfs-kernel-server
```

一旦启用了该服务，按照以下方式启动它：

```bash
systemctl start nfs-kernel-server
```

### 22.2 配置 Ubuntu 防火墙允许 NFS 



，需要配置防火墙以允许 `NFS` 流量。

如果启用了简单的防火墙（UFW），运行以下命令添加规则以允许 `NFS` 流量：

```bash
ufw allow nfs
```

相反，如果你使用的是 `firewalld`，请运行以下 `firewall-cmd`：

```bash
firewall-cmd --add-service=nfs --permanent
```

### 22.3 指定要共享的文件夹

现在 `NFS` 正在运行且防火墙已配置，我们需要指定文件系统的哪些部分可以导出。

### 22.4 访问共享文件夹

可以通过手动挂载的方式从客户端系统访问共享文件夹。在尝试挂载远程文件夹之前，应先在客户端上安装 `nfs-common` 包：

```bash
apt install nfs-common
```

要从命令行挂载远程文件夹，打开终端并创建一个你想挂载远程文件夹的目录：

```bash
mkdir /home/tmp
```

接下来，使用远程服务器的 IP 地址或主机名输入挂载远程文件夹的命令，例如：

```bash
mount -t nfs 192.168.1.115:/tmp /home/tmp
```

### 22.5 在系统启动时挂载 NFS 文件系统

编辑 `/etc/fstab` 文件，也可以配置 Ubuntu 系统在每次启动时都自动挂载远程文件系统。当加载到编辑器时，它可能看起来如下：

```text
UUID=84982a2e-0dc1-4612-9ffa-13baf91ec558 / ext4 errors=remount-ro 0 1
swapfile none swap 0 0
```

为了将位于 IP 地址为 `192.168.1.115` 的系统中路径为 `/tmp` 的文件夹挂载到本地路径为 `/home/tmp` 的文件夹（注意该文件夹必须已经存在），向 `/etc/fstab` 文件添加以下行：

```text
192.168.1.115:/tmp /home/tmp nfs rw 0 0
```

### 22.6 卸载 NFS 挂载点

一旦使用 `NFS` 挂载了远程文件系统，可以使用 `umount` 命令以本地挂载点作为命令行参数进行卸载。例如，以下命令将卸载我们的示例文件系统挂载点：

```bash
umount /home/tmp
```

### 22.7 在 Cockpit 中访问 NFS 文件系统





除了使用命令行在客户端上挂载远程 NFS 文件系统外，也可以在 Cockpit Web 界面中执行挂载操作。假设客户端系统上已经安装并配置了 Cockpit，请在网络浏览器中登录 Cockpit 界面，并从左侧导航面板中选择 `Storage`（存储）选项。如果没有列出 `Storage` 选项，则需要安装 `cockpit-storaged` 软件包：

```bash
apt install cockpit-storaged
```

一旦 `Cockpit` 服务重启，重新登录 Cockpit 界面，此时 `Storage` 选项就应该是可见的。

选择该选项后，主存储页面将包含一个部分，列出所有当前挂载的 NFS 文件系统，如图 22-1 所示：

![](img/ubuntu_18.04_cockpit_nfs_mounts.jpg)

图 22-1

要挂载远程文件系统，点击上方高亮的 `+` 按钮，并在弹出的对话框中输入远程 NFS 服务器和文件系统共享的信息，以及本地挂载点和任何必要的选项，最后点击 `Add`（添加）按钮：

![](img/ubuntu_18.04_cockpit_new_nfs_mount.jpg)

图 22-2

要修改、卸载或删除 NFS 文件系统共享，请在 NFS Mounts 列表中选择相应的挂载项（上方的图 22-1），以显示下方图 22-3 所示的页面：

![](img/ubuntu_18.04_cockpit_nfs_mount_details.jpg)

图 22-3

### 22.8 总结

网络文件系统（NFS）是一种基于客户端/服务器的系统，最初由 Sun Microsystems 开发，为 Linux 和 Unix 系统提供了通过网络共享文件系统的方法。NFS 允许客户端系统访问（在权限允许的情况下）修改位于远程服务器上的文件，就像这些文件存储在本地文件系统中一样。本章概述了 NFS 的概述，并列出了使用命令行或 Cockpit Web 界面配置客户端和服务器系统的可用选项。

## 23. 使用 Samba 在 Ubuntu 和 Windows 系统之间共享文件

尽管 Linux 在桌面市场取得了一席之地，但它的起源和未来很大程度上是基于服务器的。因此，Ubuntu 能够作为文件服务器并不意外。在网络环境中，Ubuntu 和 Windows 系统并肩使用也非常常见。因此，一个常见的需求是 Ubuntu 系统上的文件可以通过网络连接被 Linux、UNIX 和基于 Windows 的访问。同样，位于 Windows 系统上的共享文件夹和打印机可能也需要从基于 Ubuntu 系统访问。

Windows 系统使用名为 Server Message Block（SMB）的协议共享文件系统和打印机等资源。为了让 Ubuntu 系统通过网络向 Windows 系统提供此类资源反之亦然，它必须支持 SMB。这是通过使用 Samba 技术实现的。除了提供 Linux 和 Windows 系统之间的集成外，Samba 还可以用于在 Linux 系统之间提供文件夹共享（作为上一章介绍的 NFS 的替代方案）。

在本章中，我们将学习在 Ubuntu 系统上与远程 Windows 和 Linux 系统共享文件系统资源和打印机的必要步骤，以及从 Ubuntu 访问 Windows 资源。

### 23.1 从 GNOME 桌面访问 Windows 资源

在深入了解 Samba 共享的细节之前，值得注意的是，如果你只是想从 Ubuntu GNOME 桌面访问 Windows 共享文件夹，那么 GNOME Files（文件）应用程序已经提供了支持。`Files` 位于程序栏中，如图 23-1 所示：

![](img/ubuntu_20.04_gnome_files_icon.jpg)

图 23-1

启动后，在左侧导航面板中选择 `Other Locations`（其他位置），然后在主面板中点击 Windows 网络图标，以浏览可用的 Windows 资源：

![](img/ubuntu_20.04_gnome_files_windows_network.jpg)

图 23-2

### 23.2 Samba 和 Samba Client

Samba 允许 Ubuntu 资源与 Windows 系统共享，也允许 Windows 资源与 Ubuntu 系统共享。Ubuntu 使用 `Samba` 客户端访问 Windows 资源。另一方面，Ubuntu 通过安装和配置 `Samba` 服务将其资源与 Windows 系统共享。

### 23.3 在 Ubuntu 系统上安装 Samba

Ubuntu 安装过程中使用的默认设置通常不会安装必要的 Samba 软件包。除非你特别要求安装 Samba，否则你的系统中很可能没有安装 Samba。要检查是否安装了 Samba，打开终端窗口并运行以下命令：

```bash
apt -qq list samba-common samba smbclient
```

可以使用 `apt` 命令行工具安装任何缺失的软件包：

```bash
apt install samba-common samba smbclient
```

### 23.4 配置 Ubuntu 防火墙以启用 Samba

接下来，需要配置当前保护 Ubuntu 系统的防火墙以允许 Samba 流量。

如果你正在使用 Uncomplicated Firewall (`ufw`)，运行以下命令：

```bash
ufw allow samba
```

或者，如果你正在使用 `firewalld`，按如下方式运行 `firewall-cmd` 命令：

```bash
firewall-cmd --permanent --add-port={139/tcp,445/tcp}
firewall-cmd --reload
```

在启动 Samba 服务之前，需要进行若干配置步骤来定义 Ubuntu 系统如何显示以及共享哪些资源。大多数配置任务都在 `/etc/samba/smb.conf` 中完成。

### 23.5 配置 smb.conf 文件

Samba 是一个高度灵活且可配置的系统，为网络资源共享提供了许多选项。这种灵活性可能会让人认为 Samba 使用起来非常复杂。然而，实际上，典型的安装并不需要许多配置选项，设置基础配置的学习曲线实际上很短。

在本章中，我们将研究如何将 Ubuntu 系统加入 Windows 工作组，并设置一个供特定用户访问的共享目录。这种配置被称为独立 Samba 服务器。更高级的配置（如在 Active Directory 环境中集成）也是可能的，但这些超出了本书的范围。

配置 Samba 的第一步是编辑 `/etc/samba/smb.conf` 文件。

#### 23.5.1 配置 [global] 部分

`smb.conf` 文件由部分组成。第一部分是 `[global]` 部分，可以在其中指定全局设置。虽然这些是全局设置，但每个选项可以在配置的其他部分被覆盖。

第一个任务是定义共享 Ubuntu 资源的 Windows 工作组名称。这通过 `[global]` 部分的 `workgroup` 指令控制，默认配置如下：

```ini
workgroup = WORKGROUP
```

如有必要，将其更改为实际的工作组名称。

除了工作组设置外，其他设置表示这是一个独立服务器，共享资源将受用户密码保护。在继续配置要共享的之前，还需要向 `[global]` 部分添加其他参数：

```ini
[global]
.
.
      netbios name = LinuxServer
.
.
```

`netbios name` 属性指定了服务器在网络上可见的名称。

#### 23.5.2 配置共享资源





下一步是配置共享资源（换句话说，就是从 Windows 网络上的其他系统访问的资源）。为了实现这一点，需要为该节指定一个名称，在共享时引用该名称。例如，如果我们计划共享 Ubuntu 系统的 `/sampleshare` 目录，我们可以将该节命名为 `[sampleshare]`。在此节中可以使用多种配置选项。然而，为了本示例的目的，我们将简单定义要共享的目录，指定该目录为可浏览且可写，并声明该资源为公共，以便客用户能够访问：

```
[sampleshare]
        comment = Example Samba share
        path = /sampleshare
        browseable = Yes
        public = yes
        writable = yes
```

要限制特定用户的访问，可以使用 `valid users` 属性，例如：

`valid users = demo, bobyoung, marcewing`

### 23.5.3 移除不需要的共享

`smb.conf` 文件预先配置了共享打印机和系统用户主文件夹的节。如果不需要共享这些资源，可以将相应的节注释掉，以便 Samba 忽略它们。在接下来的示例中，`[homes]` 节已被注释掉：

```
#[homes]
# comment = Home Directories
# valid users = %S, %D%w%S
# browseable = No
# read only = No
# inherit acls = Yes
```

### 23.6 创建 Samba 用户

任何需要访问 Samba 共享资源的用户都必须配置为 Samba 用户并分配密码。此任务通过使用 `smbpasswd` 命令行工具完成。例如，假设需要一个名为 `demo` 的用户能够从 Windows 系统访问 Ubuntu 系统的 `/sampleshare` 目录。为了满足这一要求，我们必须按照如下方式添加 `demo` 为 Samba 用户：

```bash
# smbpasswd -a demo
New SMB password:
Retype new SMB password:
Added user demo.
```

现在我们已经完成了一个非常基础的 Samba 服务器的配置，是时候测试我们的配置文件并启动 Samba 服务了。

### 23.7 测试 smb.conf 文件

可以使用 `testparm` 命令行工具按照所示检查 `smb.conf` 文件中的设置是否存在错误：

```bash
# testparm
Load smb config files from /etc/samba/smb.conf
rlimit_max: increasing rlimit_max (1024) to minimum Windows limit (16384)
WARNING: The "syslog" option is deprecated
Processing section "[printers]"
Processing section "[print$]"
Processing section "[sampleshare]"
Loaded services file OK.
Server role: ROLE_STANDALONE
Press enter to see a dump of your service definitions
```

```
# Global parameters
[global]
dns proxy = No
log file = /var/log/samba/log.%m
map to guest = Bad User
max log size = 1000
netbios name = LINUXSERVER
obey pam restrictions = Yes
pam password change = Yes
panic action = /usr/share/samba/panic-action %d
passwd chat = *Enter\snew\s*\spassword:* %n\n *Retype\snew\s*\spassword:* %n\n *password\supdated\ssuccessfully* .
passwd program = /usr/bin/passwd %u
security = USER
server role = standalone server
server string = %h server (Samba, Ubuntu)
syslog = 0
unix password sync = Yes
usershare allow guests = Yes
wins support = Yes
idmap config * : backend = tdb
[printers]
browseable = No
comment = All Printers
create mask = 0700
path = /var/spool/samba
printable = Yes
[print$]
comment = Printer Drivers
path = /var/lib/samba/printers
[sampleshare]
comment = Example Samba share
guest ok = Yes
path = /sampleshare
read only = No
```

### 23.8 启动 Samba 和 NetBIOS 名称服务

为了让 Ubuntu 服务器在 Windows 网络中运行，必须启动 Samba (SMB) 和 NetBIOS 名称服务 (NMB)。可选，还可以启用这些服务，以便它们在每次系统启动时自动启动：

```bash
# systemctl enable smbd
# systemctl start smbd
# systemctl enable nmbd
# systemctl start nmbd
```

在尝试从 Windows 系统连接之前，使用 `smbclient` 工具来验证共享是否已配置：

```bash
# smbclient -U demo -L localhost
Enter WORKGROUP\demo’s password:
Sharename Type Comment
--------- ---- -------
print$ Disk Printer Drivers
sampleshare Disk Example Samba share
IPC$ IPC IPC Service (demo-server2 server (Samba, Ubuntu))
Officejet_Pro_8600_C7C718_ Printer
Officejet_6600_971B9B_ Printer
Reconnecting with SMB1 for workgroup listing.
Server Comment
--------- -------
Workgroup Master
--------- -------
WORKGROUP LINUXSERVER
```

### 23.9 访问 Samba 共享

现在 Samba 资源已经配置且服务正在运行，是时候从 Windows 系统访问共享资源了。在与 Ubuntu 系统处于同一工作组的适当 Windows 系统上，访问共享资源。

### 23.10 从 Ubuntu 访问 Windows 共享

正如前面提到的，Samba 是双向的，不仅允许 Windows 系统访问托管 Ubuntu 系统上的文件和打印机，还允许 Ubuntu 系统访问 Windows 上的共享资源。这是通过在本章开始时安装的 `smbclient` 包实现的。如果尚未安装，请从终端窗口进行安装：

```bash
# apt install smbclient
```

Windows 上的共享资源可以通过 Ubuntu 桌面上的“文件”应用程序访问，也可以通过命令行提示使用 `smbclient` 和挂载工具访问。本节中的步骤假设 Windows 系统上已启用适当的网络共享设置。

若要使用 GNOME 桌面访问 Windows 系统上的任何共享资源，首先启动“文件”应用程序并选择“其他位置”（Other Locations）选项。这将显示所示屏幕，其中包含 Windows 网络图标（如果检测到的话）：

![](img/rhel_8_connect_to_windows_share.jpg)
图 23-7

选择“网络”选项将显示网络上检测到的 Windows 系统并允许访问任何共享资源。





![](img/rhel_8_files_windows_10_share.jpg)

图 23-8

或者，可以使用“连接服务器”（Connect to Server）选项连接到特定系统。请注意，远程系统的名称或 IP 地址必须以 `smb://` 为前，并且可能后跟特定共享资源的路径，例如：

```
smb://WinServer10/Documents
```

### 23.11 总结

在本章中，我们学习了如何配置 `Ubuntu` 系统使其同时作为 `Samba` 客户端和服务器，从而允许与 Windows 系统共享资源。涵盖的主题包括 `Samba` 客户端和服务器包的安装，以及将 `Samba` 配置为独立服务器。

## 24. 虚拟化技术概述

虚拟化广义上被定义为在单台计算机系统上同时运行多个操作系统的能力。虽然这不一定是一个新概念，但虚拟化在近年来变得非常突出，因为它提供了一种充分利用服务器系统 `CPU` 和资源容量的方法，同时又了稳定性（即如果一个虚拟机客户系统崩溃，主机和任何其他客户系统也将继续运行）。

虚拟化在尝试不同的操作系统而无需配置双启动环境方面也有用。例如，你可以在虚拟机中运行 `Windows`，而无需重新划分磁盘、关闭 `Ubuntu` 然后从 `Windows` 启动。你只需要启动一个虚拟化版本的 `Windows` 作为客户操作系统即可。同样，虚拟化还允许你在 `Ubuntu` 系统内部运行其他 Linux 发行版，从而提供对两个操作系统的并发访问。

在决定实现虚拟化的最佳方法时，清楚了解现有的不同虚拟化解决方案是重要的。因此，本章的目的是通俗地描述目前常用的虚拟化技术。

### 24.1 客户操作系统虚拟化

客户操作系统虚拟化（也称为基于应用程序的虚拟化）可能是最容易理解的概念。在这种情况下，物理主机计算机系统运行标准的未修改的操作系统，如 `Windows`、`Linux`、`UNIX` 或 `macOS`。运行在该操作系统上的是虚拟化应用程序，它的执行方式与系统上运行的任何应用程序（如文字处理器或电子表格）相同。在该化应用程序内部创建了一个或多个虚拟机，以便在主机计算机上运行客户操作系统。

虚拟化应用程序负责启动、停止和管理每个虚拟机，并本质上代表每个虚拟机控制对物理硬件资源的访问。虚拟化应用程序还参与一种名为“二进制重写”（binary rewriting）的过程，这涉及扫描执行中的客户系统的指令流，并将任何特权指令替换为安全的仿真。这种效果使得客户系统认为它是直接运行在系统硬件上，而不是应用程序内的虚拟机中。

下面的图提供了基于客户操作系统的虚拟化说明：

![](img/guest_os_virtualization.jpg)

图 24-1

如上述图所示，客户操作系统在虚拟化应用程序的虚拟机中运行，而虚拟机又运行在主机操作系统之上，方式与其他任何其他应用程序相同。显然，客户操作系统与底层主机硬件之间的多层抽象不利于实现高水平的虚拟机性能。然而，这种技术的优势在于，不需要对主机或客户操作系统进行任何更改，也不需要特殊的 `CPU` 硬件虚拟化支持。

### 24.2 监控程序（Hypervisor）虚拟化

在 Hypervisor 虚拟化中，监控程序的任务是为虚拟机处理资源和内存分配，并为高级管理和监控工具提供接口。基于 Hypervisor 的解决方案分为 Type-1 和 Type-2。

Type-2 Hypervisor（有时称为宿主型 Hypervisor）作为软件应用程序安装并运行在主机操作系统之上，通过协调客户虚拟机对 `CPU`、内存和网络等资源的访问来提供虚拟化能力。图 24-2 展示了使用 Type-2 Hypervisor 虚拟系统的典型架构：

![](img/type-2_hypervisor_virtualization.jpg)

图 24-2

为了理解 Type-1 Hypervisor 如何工作，稍微了解一下 Intel x86 处理器架构会有帮助。`x86` 系列的 `CPUs` 提供了一系列称为“环”（rings）的保护级别，代码可以在其中执行。`Ring 0` 具有最高级特权，操作系统内核通常运行在这个环中。在 `ring 0` 中执行的代码被称为运行在系统空间、内核模式或监视模式下。所有其他代码（如运行在操作系统上的应用程序）运行在权限较低的环中，通常是 `ring 3`。

与 Type-2 Hypervisor 不同，Type-1 Hypervisor（也称为裸机或原生 Hypervisor）直接运行在主机系统的硬件上的 `ring 0` 中。显然，由于 Hypervisor 占据了 `CPU` 的 `ring 0`，运行在系统上的任何客户操作系统的内核必须运行在权限较低的 CPU 环中。遗憾的是，大多数操作系统内核被显式编写为运行在 `ring 0`，简单原因是它们需要执行只有在该环中才具备的任务，例如执行特权 `CPU` 指令和直接操作内存的能力。近年来针对这个问题设计了许多不同的解决方案，每种方案均在下所示：

### 24.2.1 半虚拟化（Paravirtualization）

在半虚拟化下，客户操作系统的内核经过专门修改以运行在 Hypervisor 上。这通常涉及将任何只在 `CPU` 的 `ring 0` 中运行的特权操作替换为对 Hypervisor 的调用（称为 `hypercalls`）。随后，Hypervisor 反而代表客户内核执行该任务。这通常将支持限制在开源操作系统（如 `Linux`，它们可以自由修改）以及已同意进行必要的代码修改以针对特定 Hypervisor 的专有操作系统。尽管存在这些问题，客户内核与 Hypervisor 直接通信的能力使其比其他虚拟化方法具有更高的性能水平。

### 24.2.2 全虚拟化（Full Virtualization）

全虚拟化为未修改的客户操作系统提供支持。“未修改”一词指的是没有为了运行在 Hypervisor 上而进行更改的操作系统内核，因此它们仍然像在 `CPU` 的 `ring 0` 中运行一样执行特权操作。在这种情况下，Hypervisor 提供 CPU 仿真来处理和修改客户操作系统内核发出的特权和保护 CPU 操作。遗憾的是，这种仿真过程运行需要时间和系统资源，导致其性能水平低于半虚拟化提供的性能。





# 硬件虚拟化

硬件虚拟化利用了 Intel 和 AMD 最新几代 CPU 内置的虚拟化功能。这些技术分别被称为 `Intel VT` 和 `AMD-V`，它们为运行未修改的客户虚拟机提供了必要的扩展，且避免了全虚拟化 CPU 仿真所固有的开销。简单来说，这些处理器在 `ring 0` 之上提供了一个额外的权限模式（称为 `ring -1`），虚拟机监控程序（hypervisor）可以在该模式下运行，从而将 `ring 0` 留给未修改的客户操作系统。

下图展示了 Type-1 虚拟机监控程序的虚拟化方法：

![](img/type-1_hypervisor_virtualization.jpg)

图 24-3

如上述图所示，除了虚拟机之外，管理操作系统和/或管理控制也运行在虚拟机监控程序之上，允许系统管理员对虚拟机进行管理。

### 24.3 虚拟机网络

虚拟机不可避免需要连接到网络才能具有实际用途。一种之一是让客户连接到主机计算机操作系统内部运行的虚拟网络。在这种配置下，虚拟网络上的任何虚拟机都可以相互可见，但对外部网络的访问通过网络地址转换（NAT）提供。当使用虚拟网络和 NAT 时，每个虚拟机都使用主机系统的 IP 地址在外部网络（主机所连接的网络）上进行表示。这是 `Ubuntu` 上 `KVM` 虚拟化的默认行为，且通常不需要额外配置。通常，默认会创建一个虚拟网络，名称为 `default`，设备为 `virbr0`。

为了让客户机在外部网络上显示为独立且各个系统（即拥有自己的 IP 地址），它们必须配置为共享主机上的物理网络接口。实现这一目标最快的方法是将虚拟机配置为使用“直接连接”网络配置选项（也称为 `MacVTap`），这将为客户系统提供一个与主机相同网络上的 IP 地址。遗憾的是，虽然这允许虚拟机访问网络上的其他系统，但在使用 `MacVTap` 驱动时，无法在客户和主机之间建立连接。

更好的选项是在主机系统上配置一个网络桥接接口，客户可以连接到该接口。这为虚拟机提供了外部网络上的 IP 地址，同时允许客户和主机进行通信，该主题将在标题为“创建 Ubuntu KVM 网络桥接接口”的章节中介绍。

### 24.4 总结

虚拟化被定义在单个主机操作系统内运行多个客户操作系统。已经开发了多种虚拟化方法，包括客户操作系统虚拟化虚拟机监控程序虚拟化。虚拟机监控程序虚拟化分为 Type-1 和 Type-2 两类。Type-2 虚拟化解决方案分为半虚拟化、全虚拟化和硬件虚拟化，后者利用某些 `Intel` 和 `AMD` 处理器模型的特殊虚拟化功能。

虚拟机客户操作系统在网络方面有多种选择，包括 NAT、直接连接（`MacVTap`）和网络桥接配置。

## 25. 在 Ubuntu 上安装 KVM 虚拟化

早期版本的 `Ubuntu` 以内核虚拟机（`KVM`）和 `Xen` 的形式提供了两个虚拟化平台。在最近的发布中，对 `Xen` 的支持已被移除，留下 `KVM` 作为 `Ubuntu` 提供的唯一捆绑虚拟化选项。除了 `KVM`，还有如 `VMware` 和 `Oracle VirtualBox` 等产品的第三方解决方案。但由于 `KVM` 是随 `Ubuntu` 提供的，因此本章及后续章节将涵盖这一虚拟化解决方案。

在深入安装和运行 `KVM` 之前，值得花一点时间讨论它如何与上一章概述的各种虚拟化类型相结合。

### 25.1 KVM 概述

`KVM` 被归为 Type-1 虚拟机监控程序虚拟化解决方案，它通过 `Intel VT` 和 `AMD-V` 硬件虚拟化支持，实现了支持未修改客户操作系统的全虚拟化。

`KVM` 与许多其他 Type-1 解决方案的区别在于，它将主机 `Linux` 操作系统本身变成了虚拟机监控程序，从而在运行完整的企业级主机操作系统的同时实现了裸金属虚拟化。

### 25.2 KVM 硬件要求

在开始本项目之前，我们需要花时间讨论在 `KVM` 环境中运行虚拟机的硬件要求。首先，`KVM` 虚拟化仅适用于某些类型的处理器。如前所述，这些处理器必须包含 `Intel VT` 或 `AMD-V` 技术。

要检查虚拟化支持，请在终端窗口中运行以下命令：

```
lscpu | grep Virtualization:
```

如果系统包含支持 `Intel VT` 的 CPU，上述命令将提供以下输出：

```
Virtualization: VT-x
```

或者，当检测到支持 `AMD-V` 的 CPU 时，将显示以下输出：

```
Virtualization: AMD-V
```

如果 CPU 不虚拟化，上述 `lscpu` 命令将不显示任何输出。

注意，虽然上述命令仅报告处理器是否支持相应功能，但它并不表示该功能当前已在 `BIOS` 中启用。在实践中，大多数系统的 `BIOS` 通常默认禁用虚拟化支持。因此，建议您在继续本教程之前检查您的 `BIOS` 设置，以确保已启用适当的虚拟化技术。

与双启动环境不同，虚拟化环境涉及在单台计算机上运行两个或多个完整的操作系统。这意味着系统必须有足够的内存、磁盘空间和 CPU 处理能力来舒适地并行这些系统。在开始配置和安装之前，请检查 `Ubuntu` 和您选择的客户操作系统的最低要求，并验证主机系统资源充足。

### 25.3 准备 Ubuntu

与 `Xen` 不同，不需要运行特殊内核来支持 `KVM`。因此，通过安装 `KVM` 内核模块，标准内核已经可以支持 `KVM`，从而消除了安装和从特殊内核启动的需求。

然而，为了避免冲突，如果系统当前运行启用了 `Xen` 的内核，请重启系统并在启动菜单中选择非 `Xen` 内核，然后再继续本章后续内容。

设置和维护基于 `KVM` 的虚拟化系统所需的工具默认未安装，除非在 `Ubuntu` 安装过程中专门选择。要从命令行安装 KVM 工具，请在终端窗口中执行以下命令：

```bash
apt install qemu-kvm libvirt-clients libvirt-daemon-system bridge-utils
```

如果您可以使用图形桌面环境，还建议安装 `virt-manager` 包：

```bash
apt install virt-manager
```

### 25.4 验证 KVM 安装

在继续之前，检查 KVM 安装是否正确。当 KVM 安装并运行时，将有两个模块加载到内核中。可以在终端窗口中运行以下命令验证这些模块的存在：

```bash
lsmod | grep kvm
```




假设安装成功，上述命令应该生成类似下面的输出：

```bash
lsmod | grep kvm
kvm_intel 237568 0
kvm 737280 1 kvm_intel
irqbypass 16384 1 kvm
```

注意，如果系统包含 AMD 处理器，`kvm` 模块可能会读取到 `kvm_amd` 而不是 `kvm_intel`。

安装过程还应该配置了 `libvirtd` 守护进程在后台运行。再次使用终端窗口，运行以下命令以确保 `libvirtd` 正在运行：

```bash
systemctl status libvirtd
libvirtd.service - Virtualization daemon
    Loaded: loaded (/usr/lib/systemd/system/libvirtd.service; enabled; vendor preset: enabled)
    Active: active (running) since Wed 2019-03-06 14:41:22 EST; 3min 54s ago
```

如果该进程未运行，可以通过以下方式启动：

```bash
systemctl enable --now libvirtd
systemctl start libvirtd
```

如果可用桌面环境，可以通过选择“活动”（Activities）并在搜索框中输入“virt”来运行 `virt-manager` 工具。当“虚拟机管理器”（Virtual Machine Manager）图标出现时，点击它进行启动。加载完成后，管理器将如如下所示：

![](img/ubuntu_20.04_virt-manager_main.jpg)
图 25-1

如果没有列出 `QEMU/KVM` 项，选择“文件 -> 添加连接”（File -> Add Connection）菜单选项，并在弹出的对话框中，点击“连接”（Connect）按钮之前选择 `QEMU/KVM` 虚拟机程序：

![](img/ubuntu_20.04_virt-manager_add_connection.jpg)
图 25-2

如果管理器当前未连接到虚拟化进程，右键点击列出的项并从弹出菜单中选择“连接”（Connect）。

### 25.5 总结

KVM 是一种 Type-1 虚拟化解决方案，它利用 `Intel VT` 和 `AMD-V` 硬件虚拟化支持实现全虚拟化，并支持对未经修改的客户端操作系统。它是 Ubuntu 自带的默认虚拟化解决方案，可以在任何具有适当处理器支持的 Ubuntu 系统上快速方便地安装。在安装并启用了 `KVM` 支持后，接下来的几章将概述在 Ubuntu 主机上安装和管理虚拟机的某些选项。

## 26 使用 Cockpit 和 virt-manager 创建 KVM 虚拟机

在 Ubuntu 上，可以使用 `virt-install` 命令行工具、`virt-manager` 图形界面工具或 `Cockpit` Web 控制台的“虚拟机”（Virtual Machines）模块轻松地配置基于 KVM 的虚拟机。在本章中，我们将使用 `Cockpit` 和 `virt-manager` 工具，在 Ubuntu 主机上作为 `KVM` 客户机安装 Fedora 发行版。

命令行创建虚拟机的方法将在下一个章节中介绍，标题为“使用 virt-install 和 virsh 创建 KVM 虚拟机”。

### 26.1 安装 Cockpit 虚拟机模块

默认情况下，标准的 `Cockpit` 安装可能不包含虚拟机模块。假设 `Cockpit` 已安装并配置完成，可以如下所示安装虚拟机模块：

```bash
apt install cockpit-machines
```

安装完成后，下次登录 `Cockpit` 界面时，导航面板中会出现“虚拟机”（Virtual Machines）选项（在图 26-1 中标记为 `A`）：

![](img/ubuntu_20.04_cockpit-virtual_machines.jpg)
图 26-1

### 26.2 在 Cockpit 中创建虚拟机

在 `Cockpit` 中创建虚拟机，只需点击图 26-1 中标记为 `B` 的“创建虚拟机”（Create VM）按钮，即可显示创建对话框。

在对话框中，为机器输入一个名称，并选择安装介质是可以通过 `URL` 访问的 `ISO` 形式，还是本地文件系统路径。理想情况下，还应为客户机选择供应商和操作系统类型信息。虽然这不是必需的，但这将有助于系统为客户机优化虚拟机。

还要指定用于操作系统安装的虚拟磁盘驱动器的大小以及分配给虚拟机的内存量：

![](img/ubuntu_20.04_cockpit-virtual_machines_new.jpg)
图 26-2

注意，`Cockpit` 提供了使用“会话”（Session）或“系统”（System）连接运行客户机的选择。可以选择 `system` 选项，客户机将连接到已经在后台以 root 权限运行的 `libvirtd` 服务系统实例。然而，`session` 选项会启动由当前用户所有的新 `libvirtd` 服务，然后将主机连接到它。默认情况下，会话客户机将使用用户账户本地存储池（例如 `/home/demo/.local/share/libvirt/images`），并且仅供所有者访问。另一方面，系统会话允许所有具有相应权限的用户访问，并默认使用位于 `/var/lib/libvirt/images` 的存储。

对于本示例，选择 `System` 选项，不勾选“立即启动虚拟机”（Immediately VM）选项，并在虚拟机配置完成后点击“创建”（Create）按钮构建虚拟机。创建完成后，虚拟机将如图 26-3 所示显示在 `Cockpit` 中：

![](img/ubuntu_20.04_machine_running.jpg)
图 26-3

### 26.3 开始安装

要启动虚拟机并从指定的介质开始安装操作系统，点击图 26-3 中高亮的“安装”（Install）按钮。`Cockpit` 将启动虚拟机并切换到“控制台”（Consoles）视图，客户机屏幕将会出现：

![](img/ubuntu_18.04_running.jpg)
图 26-5

如果安装失败，检查消息是否如下：

```
unsupported configuration: CPU mode ‘custom’ for x86_64 kvm domain on x86_64 host is not supported by hypervisor
```

要解决此问题，请删除新虚拟机，重启系统然后重新创建。

或者，检查消息是否如下：

```
Could not open '<path to iso image>': Permission denied
```

域安装似乎失败。通常是因为 QEMU 模拟器以 `qemu` 用户身份运行，而该用户没有访问 ISO 镜像所在目录的权限。要解决此问题，打开终端窗口（如果是远程系统则通过 `SSH` 连接），切换到 ISO 镜像所在的目录，并将 `qemu` 用户添加到父目录的访问控制列表（ACL）中：

```bash
cd /path/to/iso/directory
setfacl --modify u:qemu:x ..
```

进行更改后，按如下所示检查：

```bash
getfacl ..
# file: ..
# owner: demo
# group: demo
user::rwx
user:qemu:--x
group::---
mask::--x
other::---
```

完成这些更改后，再次点击“安装”（Install）按钮完成安装。

安装完成后，在“控制台”（Consoles）视图中与屏幕进行交互，就像在物理硬件上安装操作系统一样。




`virt-viewer` 工具也适用于 Windows 系统，并可以从以下 URL 下载：

[`virt-manager.org/download/`](https://virt-manager.org/download/)

要连接到运行在本地主机上的虚拟机，只需运行 `virt-viewer` 并在弹出的对话框中选择你想要连接的虚拟机即可：

![](img/ubuntu_20.04_virt-viewer_guests.jpg)
图 26-6

上述命令将列出基于系统的虚拟机。要列出并访问基于会话（session）的虚拟机，请按如下方式启动 `virt-viewer`：

```bash
virt-viewer --connect qemu:///session
```

或者，也可以指定虚拟机名称并完全跳过选择对话框，例如：

```bash
virt-viewer myFedoraGuest
virt-viewer --connect qemu:///session myFedoraGuest
```

要使用 `SSH` 将 `virt-viewer` 实例连接到运行在远程主机上的虚拟机，可以使用命令：

```bash
virt-viewer --connect qemu+ssh://<user>@<host>/system <guest name>
```

例如：

```bash
virt-viewer --connect qemu+ssh://root@192.168.1.122/system MyFedoraGuest
```

在使用此技术时，需要注意的是，在完全建立连接之前，会提示你输入用户密码。

虚拟机创建完成后，可以使用 `Cockpit` 界面来监控机器并执行重启、关机或删除客户系统等任务。`Disks`（磁盘）面板上还包含一个选项，可以向虚拟机配置添加额外的磁盘。

### 26.4 使用存储卷和存储池

当创建虚拟机时，它通常会关联一个虚拟磁盘驱动器。代表这些虚拟磁盘驱动器的镜像存储在存储池（storage pools）中。存储池可以是本地文件系统上的现有目录、文件系统分区、物理磁盘设备、逻辑卷管理 (`LVM`) 卷组甚至是远程网络文件系统 (`NFS`)。

每个存储池被分为一个或多个存储卷（storage volumes）。存储卷通常是单个镜像文件，每个代表一个虚拟磁盘驱动器，也可以采取物理磁盘分区、整个磁盘驱动器或 `LVM` 卷组的形式。

当使用前面的步骤创建虚拟机时，会创建一个默认存储池，虚拟机镜像可以存储在其中。该默认存储池占用根文件系统的空间，可以通过 `Cockpit Virtual Machine` 界面查看，选择上方标记为 C 的面板顶部的图 26-1 中的 `Storage Pools` 。

选中后，将出现下方图 26-7 所示的屏幕，其中包含当前在系统上配置的存储池列表：

![](img/ubuntu_20.04_cockpit-storage_pools.jpg)
图 26-7

在上面的示例中，默认存储池位于根文件系统，并将虚拟机镜像存储在 `/var/lib/libvirtd/images` 目录下。要查看池中包含的存储卷，请选择图 26-8 中亮显示的 `Storage Volumes`（存储卷）选项卡：

![](img/ubuntu_20.04_cockpit-storage_volumes.jpg)
图 26-8

在 Fedora 客户机的情况下，存储卷以名为 `myFedoraGuest.qcow2` 的镜像文件形式存在。要确定特定虚拟机使用哪个存储卷，返回虚拟机 Cockpit 主屏幕，选择该虚拟机并按如图 26-9 所示显示 Disks 面板：

![](img/ubuntu_20.04_cockpit-vm_disks.jpg)
图 26-9

虽然出于测试和早期实验之目的，使用默认存储池是可以接受的，但建议为通用虚拟化用途创建额外的池。要创建新的存储池，请在 `Cockpit` 中显示 `Storage Pools` 屏幕并点击 `Create New Storage Pool`（创建新存储池）按钮，显示如图 26-10 所示的对话框：

![](img/fedora_cockpit_vm_create_pool.jpg)
图 26-10

在上面的示例中，正在创建一个名为 `MyPool` 的新存储池，该池使用本地文件系统中挂载为 `/MyPool` 的文件系统分区（磁盘驱动器、分区和挂载点的主题将在本章标题为“向 Ubuntu 系统添加新磁盘驱动器”的章节中讨论）。一旦创建，该池现在将列在 `Cockpit` 存储池屏幕中，并可以在创建新虚拟机时用于包含存储卷。

在编写本文时，尚无法在 `Cockpit` 界面内从自定义存储池中创建新的存储卷。然而，可以像下一节所示，在虚拟机管理器中执行此操作。

### 26.5 使用 virt-manager 创建虚拟机

需要注意的是，一旦 `Virtual Machines Cockpit` 扩展完全实现，`virt-manager` 可能会在未来停止。本章的剩余部分将探索使用该工具创建虚拟机。

### 26.6 启动虚拟机管理器

通过终端窗口在命令行运行 `virt-manager` 来启动虚拟机管理器。加载后，虚拟机管理器会提示输入当前用户的密码，然后显示如下屏幕：

![](img/ubuntu_20.04_virt-manager_main.jpg)
图 26-11

主屏幕列出了系统上运行的虚拟机。默认情况下，管理器应该连接到系统的 `libvirtd` 实例。如果不是，通过右键点击列表中的项并选择 `Connect` 连接主机系统。要管理基于会话的虚拟机，选择 `File -> Add Connection...` 菜单显示如图 26-12 所示的对话框：

![](img/ubuntu_20.04_virt-manager_add_connection.jpg)
图 26-12

在此对话框中，从 `Hypervisor` 菜单选择 `QEMU/KVM user session` 并点击 `Connect` 按钮。返回 `virt-manager` 主屏幕后，现在列出了用户会话：

![](img/ubuntu_20.04_virt-manager_user_session.jpg)
图 26-13

要创建新的虚拟机系统，点击新建虚拟机按钮（工具栏最左侧的按钮），或右键点击 Hypervisor 项并在弹出的菜单中选择 `New`，显示新虚拟机向导的第一个屏幕。

在 `Name` 字段中为虚拟机系统输入一个描述性的名称。在此屏幕上，还要选择用于安装客户操作系统的介质。可以是 CD 或 DVD 驱动器、本地主机可访问 ISO 镜像文件、使用 `HTTP`、`FTP`、`NFS` 或 `PXE` 网络安装，或现有虚拟机的磁盘镜像：

![](img/ubuntu_20.04_virt-manager_media.jpg)
图 26-14

### 26.7 配置 KVM 虚拟机系统

点击前进将显示一个寻求安装过程信息的屏幕。显示的屏幕和所需的信息取决于在前一个屏幕中的选择。例如，如果选择了 CD、DVD 或 ISO，此屏幕将询问 ISO 文件或物理介质的具体位置。此屏幕还根据指定的安装介质识别要安装的客户操作系统类型和版本（例如 Windows 版本或 Linux 发行版）。如果无法识别，取消勾选 `Automatically detect from installation media / source` ，输入操作系统名称的前几个字符并从可能的匹配列表中选择一个选项：

![](img/ubuntu_20.04_virt-manager-iso.jpg)
图 26-15





完成这些设置后，点击 `Forward`（前进）按钮来配置 CPU 和内存设置。最佳设置取决于主机上 CPU 的数量、物理内存的大小，并结合与新虚拟机并行运行的其他应用程序和虚拟机的需求：

![](img/ubuntu_20.04_virt-manager_cup_memory.jpg)
图 26-16

在下一个屏幕上，可以使用可用选项创建指定大小的镜像磁盘、选择已有的卷，或创建指定格式（raw、vmdk、ISO 等）的存储卷。除非您有使用特定格式的特殊需求（例如，您之后可能需要使用 `vmdk` 迁移到基于 VMware 的虚拟化环境）或需要使用专用磁盘或分区，否则在此屏幕上只需指定大小通常就足够了：

![](img/ubuntu_20.04_virt-manager-storage.jpg)
图 26-17

如果在此处默认设置，虚拟机将使用默认存储池中的存储卷作为虚拟磁盘驱动器。要使用本章之前创建的自定义“MyPool”存储池，请在点击 `Manage...`（管理...）按钮之前启用 `Select`（选择）或创建自定义存储选项。

在存储卷对话框中，在左侧面板中选择 `MyPool` 条目，然后点击主面板中的 `+` 按钮创建一个新的存储卷：

![](img/ubuntu_20.04_virt-manager_storage_volume.jpg)
图 26-18

注意，位于对话框左下角的 `+` 按钮也可以用于创建新的存储池，作为使用 Cockpit 界面的替代方案。

在配置屏幕（图 26-19）中，命名存储卷，选择卷的大小并点击 `Finish`（完成）按钮来创建卷并将其分配给虚拟机：

![](img/ubuntu_20.04_virt-manager_new_storage_volume.jpg)
图 26-19

配置好设置后，选择新卷并点击 `Choose Volume`（选择卷）按钮。再次点击 `Forward` 按钮。最后一个屏幕显示配置摘要。检查所显示的信息。还可以高级选项来更改客机的虚拟网络配置，如图 26-20 所示：

![](img/ubuntu_20.04_virt-manager_network.jpg)
图 26-20

### 26.8 启动 KVM 虚拟机

点击 `Finish` 按钮开始创建过程。虚拟化管理器将在启动客体系统之前创建磁盘并配置虚拟机。新虚拟机将出现在 virt-manager 主窗口中，状态设置为 `Running`（运行中），如图 26-21 所示：

![](img/ubuntu_20.04_virt-manager-main-runnings.jpg)
图 26-21

默认情况下，虚拟机的控制台应该出现在虚拟机查看器窗口中。要在以后任何时间查看运行中的机器控制台，请确保它在虚拟机列表中被选中，并选择工具栏上的 `Open`（打开）按钮。虚拟机查看器应准备好开始安装过程：

![](img/ubuntu_20.04_virt-manager-guest_running.jpg)
图 26-22

从现在开始，只需按照操作系统的安装指令在 KVM 虚拟机中安装客体操作系统。

### 26.9 总结

本章概述了在 Ubuntu 主机系统上创建新 KVM 虚拟机的两种方法。第一种方案涉及使用 Cockpit Web 界面来创建和管理虚拟机。这种方法的优点是不需要访问运行在主机系统上的桌面环境。另一种方案是使用 `virt-manager` 图形工具。在涵盖这些基础知识后，下一章将介绍如何从命令行创建虚拟机。

## 27. 使用 virt-install 和 virsh 创建 KVM 虚拟机

在上一章中，我们探索了如何在 Ubuntu 主机上使用 Cockpit 和 `virt-manager` 图形工具创建 KVM 客体操作系统。在本章中，我们将把注意力转移到使用 `virt-install` 和 `virsh` 命令行工具创建基于 KVM 的虚拟机。这些工具提供了 `virt-manager` 和 Cockpit 选项的所有功能，并且额外优点是它们可以在脚本中使用以自动化虚拟机的创建。此外，`virsh` 命令允许根据配置文件中的规范创建虚拟机。

`virt-install` 工具允许通过提供一系列命令行选项来创建新虚拟机。本章假设已安装必要的 KVM 工具。有关这些要求的详情，请阅读标题为“在 Ubuntu 上安装 KVM 虚拟化”的章节。

### 27.1 运行 virt-install 构建 KVM 客体系统

`virt-install` 工具接受大量的参数，用于提供与创建的虚拟机相关的配置信息。某些命令行选项是强制性的（特别是必须提供名称、内存和磁盘存储），而其他是可选的。

至少，`virt-install` 命令通常需要以下参数：

- `--name` - 分配给虚拟机的名称。
- `--memory` - 分配给虚拟机的内存量。
- `--disk` - 用于虚拟机的镜像文件名和位置。除非指定了 `--import` 选项，否则该文件将在 `virt-install` 创建虚拟机期间创建。
- `--cdrom` 或 `--location` - 指定包含客体系统安装媒体的本地路径或远程 ISO 镜像 URL。

使用 `virt-install` 可用的所有参数摘要可以在 man 手页找到：

```
$ man virt-install
```

### 27.2 一个 Ubuntu virt-install 命令示例

参考上述命令行列表，我们现在可以查看一个使用 virt-install 的命令行示例。

注意，为了能够显示虚拟机并完成安装，虚拟机启动后需要连接一个 virt-viewer 实例到虚拟机。默认情况下，`virt-install` 会在虚拟机启动后尝试自动启动 `virt-viewer`。如果没有 `virt-viewer`，`virt-install` 将等待建立 `virt-viewer` 连接。如果主机系统具有图形桌面，则 `virt-viewer` 会话可以在本地运行，也可以像“使用 Cockpit 和 virt-manager 创建 KVM 虚拟机”章节所示从远程客户端建立连接。

以下命令创建一个配置为 KVM 半虚拟化运行 Fedora 的 KVM 虚拟机。它创建一个新的 10GB 磁盘镜像，为虚拟机分配 1024MB 内存，并为安装媒体 ISO 配置虚拟光驱：

```
virt-install --name MyFedora --memory 1024 --disk path=/tmp/myFedora.img,size=10 --network network=default --os-variant fedora28 --cdrom /tmp/Fedora-Server-dvd-x86_64.iso
```

在创建过程运行时，`virt-install` 命令将显示创建进度的状态更新：

Starting install...
Allocating ‘MyFedora.img’ | 10 GB 00:00:01
Domain installation still in progress. Waiting for installation to complete.

一旦客体系统创建，将出现 virt-viewer 屏幕，其中操作系统安装程序：

![](img/ubuntu_20.04_virt-install_guest.jpg)
图 27-1

从现在开始，按照操作系统的标准安装程序进行。





### 27.3 从命令行启动和停止虚拟机

既然你已经从命令行创建了虚拟机，那么理所当然，你将来可能也需要从命令行启动它。这可以通过 `virsh` 命令行工具实现，并引用在创建过程中为虚拟机分配的名称。例如：

```
virsh start MyFedora
```

同样地，可以通过以下方式向虚拟机发送关闭信号：

```
virsh shutdown MyFedora
```

如果虚拟机对关闭信号没有响应且没有开始平稳关机，可以使用 `destroy` 指令销毁虚拟机（这将伴随数据丢失的风险）：

```
virsh destroy MyFedora
```

### 27.4 从配置文件创建虚拟机

`virsh create` 命令可以接受配置文件的名称作为参数，基于该文件来创建新的虚拟机。配置文件使用 XML 格式。可以认为，创建配置文件最简单的方法是导出现有虚拟机的配置，并针对新虚拟机对其进行修改。这可以使用 `virsh dumpxml` 命令实现。以下命令将名为 `MyFedora` 的虚拟机域的配置数据输出到名为 `MyFedora.xml` 的文件中：

```
virsh dumpxml MyFedora > MyFedora.xml
```

文件生成后，将其加载到编辑器中以检查并更改新虚拟机的设置。

至少必须更改 `<name>`、`<uuid>` 和镜像文件路径 `<source file>`，以避免与获取配置的虚拟机发生冲突。对于 UUID，可以简单地从文件中删除该行。

根据需要，还可以更改虚拟化类型、内存分配和 CPU 数量等部分选项。一旦文件经过了修改，就可以按照如下方式创建新的虚拟机：

```
virsh create MyFedora.xml
```

### 27.5 总结

KVM 提供了 `virt-install` 和 `virsh` 命令行工具，可以作为使用 Cockpit 和 `virt-manager` 工具创建和管理虚拟机实例的快速高效的替代方案。这些工具的优势可以在脚本内部使用，以自动化虚拟机的创建和管理。`virsh` 命令还包含了从基于 XML 的配置文件创建 VM 实例的选项。

## 28. 在 Ubuntu 上创建 KVM 网络桥接接口

默认情况下，Ubuntu 上的 KVM 虚拟化环境会创建一个虚拟网络，虚拟机可以连接到该网络。也可以使用 MacVTap 驱动配置直接连接，尽管正如“虚拟化技术概述”章节所述，这种方法不允许主机和客机系统进行通信。

本章的目标是介绍在 Ubuntu 上创建网络桥接的步骤，使用客系统共享主机系统的一个或多个物理网络连接，同时允许客机和主机系统相互通信。

在本章的剩余部分中，我们将解释如何配置供基于 KVM 的客机操作系统使用的 Ubuntu 网络桥接。

### 28.1 识别网络管理系统

创建网络桥接的步骤取决于主机系统使用 `Network Manager` 还是 `Netplan` 进行网络管理。如果你使用桌面安装媒体安装了 Ubuntu，那么你很可能拥有运行 `Network Manager` 的系统。相反，如果你是从服务器或网络安装镜像安装的，那么你的系统很可能正在使用 `Netplan`。

要识别正在使用哪种网络系统，打开终端窗口并运行以下命令：

```
networkctl status
```

如果上述命令产生类似下面的输出，则系统正在使用 `Netplan`：

```
networkctl status
● State: routable
          Address: 192.168.86.242 on enp0s3
                      fe80::a00:27ff:fe52:69a9 on enp0s3
          Gateway: 192.168.86.1 (Google, Inc.) on enp0s3
              DNS: 192.168.86.1
Search Domains: lan
May 04 15:46:09 demo systemd[1]: Starting Network Service...
May 04 15:46:09 demo systemd-networkd[625]: Enumeration completed
```

如果，出现了类似下面的输出，则 `Netplan` 没有在运行：

```
networkctl status -a
WARNING: systemd-networkd is not running, output will be incomplete.
Failed to query link bit rates: Unit dbus-org.freedesktop.network1.service not found.
```

要识别 `NetworkManager` 是否正在运行，切换目录到 `/etc/netplan`。如果你使用 `NetworkManager`，此目录将包含一个名为 `01-network-manager-all.yaml` 的文件，内容如下：

```yaml
Let NetworkManager manage all devices on this system
network:
  version: 2
  renderer: NetworkManager
```

识别出你的网络管理系统后，请按照本章剩余部分中的相应步骤操作。

### 28.2 获取 Netplan 网络设置

在基于 `Netplan` 的系统上创建网络桥接之前，首先使用如下 `networkctl` 命令获取当前网络的信息：

```
networkctl status -a
● 1: lo
          Link File: /lib/systemd/network/1.link
          Network File: n/a
          Type: loopback
          State: unmanaged
          Address: 127.0.0.1
                      ::1
● 2: eno1
          Link File: /lib/systemd/network/2.link
          Network File: /run/systemd/network/eno1
          Type: ether
          State: routable
          Address: 192.168.86.242
                      fe80::a00:27ff:fe52:69a9
          Gateway: 192.168.86.1 (Google, Inc.)
              DNS: 192.168.86.1
          Search Domains: lan
● 3: virbr0
          Link File: /lib/systemd/network/3.link
          Network File: /run/systemd/network/virbr0
          Type: bridge
          State: configured
          Address: 192.168.122.1
● 4: virbr0-nic
          Link File: /lib/systemd/network/4.link
          Network File: n/a
          Type: ether
          State: off (unmanaged)
```

在上面的输出中，我们可以看到主机通过名为 `eno1` 的设备建立了以太网连接，以及名为 `virbr0` 的默认桥接接口，该接口为 KVM 客机系统连接的基于 NAT 的虚拟网络提供访问。输出还列出了回环接口`lo`）。

### 28.3 创建 Netplan 网络桥接

在基于 `Netplan` 的系统上创建网络桥接，涉及向 `/etc/netplan/01-netcfg.yaml` 或 `/etc/netplan/00-installer-config.yaml` 文件添加项。使用你喜欢的编辑器打开文件，并在当前内容下方添加 `bridges` 项（将 `eno1` 替换为你系统上的连接名称）：

```yaml
network:
  ethernets:
    eno1:
      dhcp4: true
  version: 2
  bridges:
    br0:
      interfaces: [eno1]
      dhcp4: yes
```

注意 `bridges:` 行必须缩进两个空格。如果没有此缩进，`netplan` 工具将失败并报错错误：

```
Error in network definition: unknown key ‘bridges’
```

更改完成后，使用以下命令应用更改：

```bash
netplan apply
```





请注意，此命令将网络从当前连接切换到桥接，这将导致 DHCP 服务器为系统分配不同的 IP 地址。如果您通过远程 SSH 会话连接，这将导致您失去与服务器的联系。如果您希望为桥接连接分配静态 IP 地址，请按照如下方式修改桥接声明（确保同时关闭 IPv4 和 IPv6 的 DHCP）：

```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    eno1:
      dhcp4: no
      dhcp6: no
  bridges:
    br0:
      interfaces: [eno1]
      dhcp4: no
      addresses: [192.168.86.230/24]
      gateway4: 192.168.86.1
      nameservers:
        addresses: [192.168.86.1]
```

运行 `netplan apply` 命令后，检查桥接是否已配置并准备好在 KVM 虚拟机中使用：

```
# networkctl status -a

● 1: lo
      Link File: /lib/systemd/network/99-default.link
      Network File: n/a
      Type: loopback
      State: carrier (unmanaged)
      Address: 127.0.0.1
             ::1
● 2: eno1
      Link File: /lib/systemd/network/99-default.link
      Network File: /run/systemd/network/10-netplan-eno1.network
      Type: ether
      State: carrier (configured)
      Path: pci-0000:00:19.0
      Driver: e1000e
      Vendor: Intel Corporation
      Model: 82579LM Gigabit Network Connection (Lewisville)
      HW Address: fc:4d:d4:3b:e4:0f (Universal Global Scientific Industrial Co.,

● 5: br0
      Link File: /lib/systemd/network/99-default.link
      Network File: /run/systemd/network/10-netplan-br0.network
      Type: ether
      State: routable (configured)
      Driver: bridge
      HW Address: b6:56:ed:e9:d5:75
      Address: 192.168.86.230
             fe80::b456:edff:fee9:d57
      Gateway: 192.168.86.1
      DNS: 192.168.86.1```

## 获取当前网络设置

可以使用 NetworkManager 命令行接口 (`nmcli`) 创建网络桥接。NetworkManager 在 Ubuntu 桌面系统中默认安装并启用，负责检测网络设备并提供配置接口。

主机当前的网络连接列表显示如下：

```
# nmcli con show
NAME UUID TYPE DEVICE
Wired connection 1 56f32c14-a4d2-32c8-9391-f5196efa73 ethernet eno1
virbr0 59bf4111-e0d2-4e6c-b8d4-cb70fa6d95e bridge
```

在上述输出中，可以看到主机通过名为 `eno1` 的设备建立了名为 `virbr0` 的默认桥接，该桥接为虚拟机提供了基于 NAT 的网络访问。同样，可以使用以下命令识别系统上当前配置的设备（包括虚拟和物理）：

```
# nmcli device show
GENERAL.DEVICE: eno1
GENERAL.TYPE: ethernet
GENERAL.HWADDR: FC:4D:D4:3B:E4:0F
GENERAL.MTU: 1500
GENERAL.STATE: 100 (connected)
GENERAL.CONNECTION: Wired connection 1
GENERAL.CON-PATH: /org/freedesktop/NetworkManager/ActiveConnection/1
WIRED-PROPERTIES.CARRIER: on
IP4.ADDRESS[1]: 192.168.122.1/24
IP4.GATEWAY: --
IP4.ROUTE[1]: dst = 192.168.122.0/24, nh = 0.0.0
```

上述部分输出表明执行命令的主机系统包含物理以太网设备 (`eno1`) 和虚拟桥接 (`virbr0`)。也可以使用 `virsh` 命令列出系统上配置的虚拟网络：

```
# virsh net-list --all
 Name      State    Autostart  Persistent
------------------------------------------
 default   active   yes        yes
```

此时，唯一的虚拟网络是 `virbr0` 提供的默认网络。获取当前网络配置的基本信息后，下一步是创建一个连接到物理网络设备（在本例中名为 `eno1` 的设备）的网络桥接。

### 28.5 从命令行创建 Network Manager 桥接

创建网络桥接的第一步向网络配置中添加新连接。可以使用 `nmcli` 工具指定连接为桥接并为连接和接口提供名称：

```
# nmcli con add ifname br0 type bridge con-name br0
```

添加连接后，需要在物理设备 `eno1`（从设备）和桥接连接 `br0`（主设备）之间建立桥接从接口：

```
# nmcli con add type bridge-slave ifname eno1 master br0
```

此时，NetworkManager 连接列表应如下：

```
# nmcli con show
NAME UUID TYPE DEVICE
Wired connection 1 56f32c14-a4d2-32c8-9391-f5196efa73 ethernet eno1
br0 8416607e-c6c1-4abb-8583-1661689b95a9 bridge br0
virbr0 dffab88d-1588-4e69-8d1c-2148090aa5ee bridge virbr0
bridge-slave-eno1 43383092-6434-448f-b735-0cbea39eb3f ethernet
```

下一步是启动桥接接口。如果通过网络连接（例如通过 SSH）执行配置桥接的步骤，这一可能会可能会问题，因为在启动桥接连接之前必须关闭当前的 `eno1` 连接，这可能导致远程主机无法访问。

如果您远程访问主机系统，可以通过创建一个脚本来执行网络更改以避免此问题。这将确保在禁用 `eno1` 接口后启用桥接口。首先创建一个包含以下内容的 `bridge.sh` 脚本：

```bash
#!/bin/bash
nmcli con down "Wired connection 1"
nmcli con up br0
```

创建脚本后，执行执行：

```
# sh ./bridge.sh
```

当脚本执行时，`eno1` 连接关闭时将会丢失。但在等待几秒钟后，一旦 `br0` 连接激活，就可以重新连接到主机。

如果您在主机上本地操作，可以在终端窗口中运行这两个 `nmcli` 命令而无丢失连接的风险：

```
# nmcli con down "Wired connection 1"
# nmcli con up br0
```

一旦桥接启动，连接列表现在应该包含桥接和桥接从设备连接：

```
# nmcli con show
NAME UUID TYPE DEVICE
Wired connection 1 56f32c14-a4d2-32c8-9391-f5196efa73 ethernet eno1
br0 8416607e-c6c1-4abb-8583-1661689b95a9 bridge br0
bridge-slave-eno1 43383092-6434-448f-b735-0cbea39eb3f ethernet
```

请注意，Wired Connection 1 连接仍在列表中，但实际上已不再处于激活状态。要从列表中排除非活动连接，只需在请求列表时使用 `--active` 标志即可：

```
# nmcli con show --active
NAME UUID TYPE DEVICE
br0 8416607e-c6c1-4abb-8583-1661689b95a9 bridge br0
```





bridge-slave-eno1 43383092-6434-448f-b735-0cbea39eb38f ethernet eno1

virbr0 dffab88d-1588-4e69-8d1c-2148090aa5ee bridge virbr0

### 28.6 声明 KVM 桥接网络

此时，桥接连接已存在于系统中，但在 KVM 环境中不可见。运行 `virsh` 命令仍然会将默认网络列为唯一的可用网络选项：

```bash
virsh net-list --all
```

名称 状态 自动启动 持久性
----------------------------------------------------------
default 激活 是 是否
```

在虚拟机可以使用网桥之前，必须对其进行声明并将其添加到 KVM 网络配置中。这涉及创建一个定义文件，并且再次使用 `virsh` 命令行工具。

首先，为桥接网络创建一个名为 `bridge.xml` 的定义文件，内容如下：

```xml
<network>
  <name>br0</name>
  <forward mode="bridge"/>
  <bridge name="br0" />
</network>
```

接下来，使用该文件来定义新网络：

```bash
virsh net-define ./bridge.xml
```

一旦定义了网络，请启动它，并在需要时将其配置为每次系统重启时自动启动：

```bash
virsh net-start br0
virsh net-autostart br0
```

再次列出网络，以验证桥接网络现在 KVM 环境内是否是可用的：

```bash
virsh net-list --all
```

名称 状态 自动启动 持久性
----------------------------------------------------------
br0 激活 是 是
default 激活 是 是
```

### 28.7 在虚拟机中使用桥接网络

要创建一个使用桥接网络的虚拟机，请使用 `virt-install --network` 选项并指定 `br0` 网桥名称。例如：

```bash
virt-install --name MyFedora --memory 1024 --disk path=/tmp/myFedora.img,size=10 --network network=br0 --os-variant fedora28 --cdrom /home/demo/Downloads/Fedora-Server-dvd-x86_64-29-1.2.iso
```

当客体系操作系统运行时，它将出现在与主机系统相同的物理网络上，而不再位于基于 NAT 的虚拟网络上。

要修改现有虚拟机以使用网桥，请使用 `virsh edit` 命令。该命令将 XML 定义文件加载到编辑器中，可以在其中进行更改并保存：

```bash
virsh edit GuestName
```

默认情况下，文件将加载到 `vi` 编辑器中。要使用不同的编辑器，只需更改 `$EDITOR` 环境变量，例如：

```bash
export EDITOR=gedit
```

要从默认虚拟网络更改，请找到文件的 `<interface>` 部分，对于 NAT 配置，其内容如下：

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

要使用网桥，在保存文件之前，将源网络属性更改为如下：

```xml
<interface type='network'>
      <mac address='<your mac address here>'/>
      <source network='br0'/>
      <model type='virtio'/>
      <address type='pci' domain='0x0000' bus='0x01' slot='0x00' function='0x0'/>
</interface>
```

如果虚拟机已经在运行，更改在重启之前将不会生效。

### 28.8 使用 nm-connection-editor 创建桥接网络

如果主机系统可以使用本地或远程桌面访问，大部分网桥配置过程可以使用 `nm-connection-editor` 图形工具完成。要使用此工具，在桌面内打开终端窗口并输入以下命令：

```bash
nm-connection-editor
```

当工具加载后，将出现如图 28-1 所示的窗口，列出当前配置的网络连接（本质上与 `nmcli con show` 命令生成的输出相同）：

![](img/ubuntu_18.04_nm-connection-editor-main.jpg)
图 28-1

要创建新连接，点击左下角的 `+` 按钮。在图 28-2 中，从菜单中选择 Bridge（桥接）：

![](img/ubuntu_18.04_nm-connection-editor-type.jpg)
图 28-2

选择桥接选项后，点击 `Create`（创建）：

![](img/ubuntu_18.04_nm-connection-editor-create.jpg)
图 28-3

现在将一个对话框，需要配置从接连接。在图 28-4 中，选择网桥连接的物理网络（例如 `eno1`）：

![](img/ubuntu_18.04_nm-connection-editor-slave.jpg)
图 28-4

点击 `Save`（保存）按钮应用更改并返回编辑对话框。在此对话框中，点击 `Save` 创建网桥：

![](img/ubuntu_18.04_nm-connection-editor-br0.jpg)
图 28-5

返回主窗口后，现在应该列出网桥和从接连接：

![](img/ubuntu_18.04_nm-connection-editor-br0-added.jpg)
图 28-6

剩下的工作是关闭 `eno1` 连接并按照前面的步骤启动 `br0` 连接（如果是远程访问，请记得在脚本中执行这些步骤）：

```bash
nmcli down "Wired connection 1"
nmcli up br0
```

正如之前使用命令行创建网桥一样，还需要将此网桥添加到 KVM 网络配置中。要这样做，只需重复上述声明 KVM 桥接网络中的步骤。完成此步骤后，网桥即可供虚拟机使用。

### 28.9 总结

默认情况下，KVM 虚拟机连接到使用 NAT 提供主机所在网络访问的网络。如果要求虚拟机以自己的 IP 地址出现在网络上，则需要配置虚拟机共享主机的物理接口。本章所述，可以使用 `nmcli` 或 `nm-connection-editor` 工具创建网桥接口。

## 29. 使用 virsh 命令行工具管理 KVM

在之前的章节中，我们涵盖了在 Ubuntu 上安装和配置基于 KVM 的虚拟机操作系统。本章专注于 `virsh` 工具的一些之前未涵盖的领域，以及如何从命令行管理基于 KVM 的虚拟机操作系统。

### 29.1 virsh Shell 和命令行

`virsh` 工具既是一个命令行工具，也是一个交互式 shell 环境。在命令行模式下使用，只需在命令提示符处输入适用于执行任务的任务参数。

要将选项作为命令行参数使用，请如下例所示在终端命令提示符中使用：

```bash
virsh <option>
```





要在 `virsh` shell 中运行命令，请执行以下命令：

# virsh

```bash
virsh

Welcome to virsh, the virtualization interactive terminal.

Type: ‘help’ for help with commands
      ‘quit’ to quit

virsh #
```

在 `virsh #` 提示符下输入你想运行的选项。例如，下面的 `virsh` 会话列出了当前的虚拟机，启动了一个名为 `FedoraVM` 的虚拟机，然后获取另一个列表以验证该虚拟机正在运行：

```bash
virsh

Welcome to virsh, the virtualization interactive terminal.

Type: ‘help’ for help with commands
      ‘quit’ to quit

virsh # list

  Id Name State
----------------------------------------------------
 8 RHEL8VM running
 9 CentOS7VM running

virsh # start FedoraVM

Domain FedoraVM started
virsh # list

  Id Name State
----------------------------------------------------
 8 RHEL8VM running
 9 CentOS7VM running
10 FedoraVM running
virsh#
```

`virsh` 工具支持广泛命令，可以使用帮助选项获取完整的命令列表：

```bash
virsh help
```

通过在帮助指令后指定命令，可以获取每个命令语法的更多细节：

```bash
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

在本章的剩余部分中，我们将更详细地查看这些命令中的一些。

### 29.2 列出客机系统状态

在 Ubuntu 虚拟化主机上，可以使用 `virsh` 工具的 `list` 选项随时查看客机系统的状态。例如：

```bash
virsh list
```

上述命令将显示输出，其中每个客机系统对应一行，如下所示：

```bash
virsh # list

  Id Name State
----------------------------------------------------
 8 RHEL8VM running
 9 CentOS7VM running
10 FedoraVM running
```

### 29.3 启动客机系统

可以使用 `virsh` 工具结合 `start` 选项以及要启动的客机操作系统的名称来启动操作系统。例如：

```bash
virsh start myGuestOS
```

### 29.4 关闭客机系统

`virsh` 工具的 `shutdown` 选项顾顾名用于关闭客机操作系统：

```bash
virsh shutdown guestName
```

注意，`shutdown` 允许客机操作系统在接收到关闭指令时执行有序关闭。要立即停止客机操作系统，可以使用 `destroy` 选项（存在文件系统损坏和数据丢失的风险）：

```bash
virsh destroy guestName
```

### 29.5 挂起和恢复客机系统

可以使用 `virsh` 工具的 `suspend` 和 `resume` 选项挂起和恢复客机系统。例如，挂起特定系统：

```bash
virsh suspend guestName
```

同样，恢复已挂起的系统：

```bash
virsh resume guestName
```

注意，如果重启主机系统，挂起的会将会将会。此外，请注意挂起的系统仍然驻留在内存中。要保存会话使其不再占用内存并能够恢复到其精确状态（即使在重启后），则需要保存并恢复客机。

### 29.6 保存和恢复客机系统

可以使用 `virsh` 实用程序保存和恢复正在运行的客机操作系统。保存时，客机操作系统的当前状态被写入磁盘并从系统内存中移除。保存的系统随后可以在任何时间恢复（包括在主机系统重启后）。

保存客机：

```bash
virsh save guestName path_to_save_file
```

恢复保存的客机操作系统会话：

```bash
virsh restore path_to_save_file
```

### 29.7 重启客机系统

重启客机操作系统：

```bash
virsh reboot guestName
```

### 29.8 配置分配给 Guest OS 的内存

要配置分配给 Guest OS 的内存，使用 `virsh` 命令的 `setmem` 选项。例如，以下命令将给客机系统的内存减少到 256MB：

```bash
virsh setmem guestName 256
```

注意，允许的内存设置必须在当前 `Domain` 可用的内存范围内。可以使用 `setmaxmem` 选项增加此限制。

### 29.9 总结

`virsh` 工具提供了创建、监控和管理客机虚拟机的多种选项。如本章所述，该工具可以在命令行或交互式模式下使用。

## 30. Linux 容器简介

前面的章节涵盖了虚拟化概念，特别强调了使用 `KVM` 创建和管理虚拟机。本章将以 Linux 容器（Linux Containers）的形式介绍一种相关技术。虽然虚拟机和容器之间有一些相似之处，但也有一些关键区别，本章将概述这些区别并介绍 Linux 容器的原理和优势。本章还将概述容器管理工具。

### 30.1 Linux 容器与内核共享

简单来说，容器可以被视为虚拟化的轻量级替代方案。在虚拟化环境中，创建一个包含并运行整个操作系统的虚拟机。虚拟机反运行在诸如虚拟机程序的环境之上，由虚拟机程序管理对主机物理资源的访问。

容器通过使用被称为内核共享的概念工作。

为了理解内核共享和容器如何工作，有助于首先理解 Linux 或 Unix 系统的两个主要组件。操作系统的核心是内核。简单来说，内核处理操作系统与物理硬件之间所有的交互。第二个关键组件是根文件系统，它包含了操作系统运行所需的所有库、文件和实用程序。利用这种结构，容器都有自己的根文件系统，但共享主机操作系统的内核。

这种资源共享通过内核能够动态更改当前根文件系统（称为 `change root` 或 `chroot`）的能力变为，而无需重启整个系统。Linux 容器本质上是这种能力的扩展，并结合了容器运行时，其职责是为主机系统上的执行和管理容器提供接口。许多容器运行时可用，包括 `Docker`、`lxd`、`containerd` 和 `CRI-O`。

### 30.2 容器的用途和优势

容器的主要优势是它们比虚拟化所需的资源开销小得多，允许在单个服务器上同时运行许多实例，并根据需求水平快速高效地启动和停止。容器原生运行在主机系统上，提供了虚拟机无法比拟的性能。





容器具有极强的移植性，可以在系统之间快速、方便地迁移。当与 `Docker`、`OpenShift` 和 `Kubernetes` 等容器管理系统结合时，可以在跨多个服务器和云平台的大范围内部署并管理容器，可能运行数千个容器。

容器经常用于为应用程序创建轻量级执行环境。在这种场景下，每个容器都提供了一个隔离的环境，包含了应用程序以及该程序运行所需的所有运行时和支持文件。然后，容器可以部署到任何其他支持容器执行的兼容宿主机系统，而无需担心目标系统可能缺少应用程序所需的运行时配置——应用程序的所有依赖项已经包含在容器中了。

容器在桥接开发和生产环境之间的差距时也非常有用。通过在容器中进行开发和 QA（质量保证）工作，可以将这些容器传递到生产环境并安全地启动，因为知道应用程序运行在与其开发和测试时相同的容器环境中。

容器还促进了大型复杂解决方案的模块化部署方法。与其将应用程序开发为单一的单体结构实体，不如使用容器将应用程序设计为一组相互作用的模块，每个模块运行在独立的容器中。

容器的一个可能的缺点是客户操作系统必须与正在共享的内核版本兼容。例如，无法在 Linux 系统上的容器中运行 Microsoft Windows。同样，为 2.6 版本内核设计的 Linux 客户系统无法共享 2.4 版本的内核。然而，这些要求并不是容器的设计初衷。因此，不应将这些视为限制，而应视为容器在提供简单、可扩展且可靠的部署平台方面的关键优势之一。

### 30.3 Ubuntu 容器工具

在 Ubuntu 上有许多创建和管理容器的。一种方法是下载并安装 `Docker` 提供的标准工具。然而，在书中，我们将关注一组由 Red Hat, Inc. 开发的新工具，这些工具广泛用于 `CentOS`、`Fedora` 和 Red Hat Enterprise Linux 等其他 Linux 发行版。选择它们有几个原因。首先，这些工具与 `Docker` 提供的工具完全兼容（包括相同的命令行选项）。更重要的是，这些工具的优势在于可以在无需运行 `Docker` 守护进程的情况下使用。该容器工具集由以下程序组成：

* `buildah` – 用于构建容器镜像的命令行工具。
* `podman` – 基于命令的容器运行时和管理工具。执行诸如从远程仓库下载容器镜像、检查镜像、启动和停止镜像等任务。
* `skopeo` – 用于转换容器镜像、在仓库之间复制镜像以及在不需要下载的情况下检查存储在仓库中的镜像的命令行程序。
* `runc` – 用于从命令行启动和运行容器的轻量级容器运行时。

上述所有工具都符合开放容器倡议 (OCI)，这是一组旨在确保容器在不同竞争性工具和平台之间遵循相同标准的规范。

### 30.4 Docker 仓库 (Registry)

尽管 Ubuntu 提供了一套设计用于替代 `Docker` 提供的工具的工具，但这些工具在构建容器时仍需要访问 Ubuntu 镜像以供使用。出于此目的，Ubuntu 团队在 `Docker Hub` 中维护了一套 Ubuntu 容器镜像。`Docker Hub` 是一个由多个仓库组成的在线容器仓库，每个仓库都包含许多供在构建容器时下载的容器镜像。仓库中的每个镜像都分配有一个仓库标签（例如，`20.04`、`latest` 等），在执行镜像下载时可以引用它。例如，以下是 `Docker Hub` 中 Ubuntu 20.04 镜像的 URL：

```
docker://docker.io/library/ubuntu:20.04
```

除了从 `Docker` 和其他第三方托管仓库下载容器镜像（在容器术语中称为“拉取”）外，你还可以使用仓库来存储自己的镜像。这可以通过托管自己的仓库，或者利用现有服务来实现，例如 `Docker`、`Amazon AWS`、`Google Cloud`、`Microsoft Azure` 和 `IBM Cloud` 等服务。

## 30.5 容器网络

默认情况下，容器使用容器网络接口 (CNI) 桥接网络栈到网络。在桥接配置中，运行在服务器上的所有容器属于同一个子网，因此能够相互通信。容器还通过桥接宿主机系统的网络连接到外部网络。同样，宿主机可以通过虚拟网络接口（通常命名为 `cni0`）访问容器，该接口是在容器工具安装过程中创建的。

### 30.6 总结

Linux 容器提供了虚拟化的轻量级替代，并利用了 Linux 和 Unix 操作系统的结构。Linux 容器本质上共享主机操作系统的内核，每个容器都有自己的根文件系统，其中包含文件、库和应用程序。容器高效且可扩展，为构建和部署模块化企业级解决方案提供了理想平台。有许多工具和平台用于构建、部署和管理容器，包括第三方解决方案和 Ubuntu 提供的工具。

## 31 在 Ubuntu 上使用容器

既然上一章已经涵盖了 Linux 容器的基础知识，本章将演示如何在 Ubuntu 上使用 `Podman`、`Skopeo` 和 `Buildah` 工具创建和管理容器。目的是在本章结束时，你将更清楚地理解如何在 Ubuntu 上创建和管理容器，并为继续探索 Linux 容器的力量奠定基础。

### 31.1 安装容器工具

在开始之前，第一步是安装上一章列出的所有容器工具。

```bash
# apt install curl
# /etc/os-release
# sh -c "echo 'deb https://download.opensuse.org/repositories/devel/kubic/stable/xUbuntu_${VERSION_ID}/ /' > /etc/apt/sources.list.d/devel:kubic:stable.list"
# curl -L https://download.opensuse.org/repositories/devel/kubic/stable/xUbuntu_${VERSION_ID}/Release.key | sudo apt-key add -
## apt update
# apt install podman skopeo buildah
```

### 31.2 拉取容器镜像

在本例中，将从仓库拉取最新的 Ubuntu 版本。然而，在拉取镜像之前，可以使用 `skopeo` 工具获取镜像信息，例如：

```bash
$ skopeo inspect docker://docker.io/ubuntu
```

```json
{
  "Name": "docker.io/library/ubuntu",
  "Digest": "sha256:bec5a272be7fff3d308193cfde3491f8fba1a2ba392b7546b43a051853a341",
  "RepoTags": [
    "10.04",
    "12.04.5",
    "12.04",
    "12.10",
    "13.04",
    "13.10",
    "14.04.1",
    "14.04.2",
    "14.04.3",
    "14.04.4",
    "14.04.5",
    "14.04",
    "14.10",
    "15.04"
  ],
  "Created": "2020-03-20T19:20:22.835345724Z"
}
```




```json
{
    "DockerVersion": "18.09.7",
    "Labels": null,
    "Architecture": "amd64",
    "Os": "linux",
    "Layers": [
        "sha256:5bed26d33875e6da1d9ff9a1054c5fef3bbeb22ee979e2acf72528de007b",
        "sha256:f11b29a9c7306674a9479158c1b4259938af11b979ac02030cc1095e9ed1",
        "sha256:930bda195c84cf132344bf38edcad255317380503fef234a9ce3bff0f4dd",
        "sha256:78bf9a5ad49eae42a83f4995ade4efc08fd38299cf05bc041e8cdda2a36"
    ],
    "Env": [
        "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
    ]
}
```

例如，要拉取最新的 Ubuntu 镜像：

```bash
$ podman pull docker://docker.io/ubuntu:latest
```

正在拉取 `docker://docker.io/ubuntu:latest`...

获取镜像源签名
正在复制 blob 5bed26d33875 done
正在复制 blob f11b29a9c730 done
正在复制 blob 78bf9a5ad49e done
正在复制 blob 930bda195c84 done
正在复制 config 4e5021d210 done
正在将清单写入镜像目标位置
存储签名
4e5021d210f65ebe915670c7089120120bc0a303b90208592851708c1b8c04bd

通过让 `podman` 列出所有本地镜像来验证该镜像是否已存储：

```bash
$ podman images
```

REPOSITORY 标签 镜像 ID 创建时间 大小
docker.io/library/ubuntu latest 4e5021d210f6 3 weeks ago 66.6 MB

可以通过运行 `podman inspect` 命令获取有关本地镜像的详情：

```bash
$ podman inspect ubuntu:latest
```

此命令的输出应与在本章之前对远程镜像执行的 `skopeo` 命令信息相同。

## 31.3 在容器中运行镜像

从仓库拉取的镜是一个完全可运行的镜像，可以在不作修改的情况下在容器中运行。要运行镜像，请使用 `podman run` 命令。在这种情况下，将指定 `--rm` 选项，表示我们要在容器中运行镜像，执行一条命令后让容器退出。在这种情况下，将使用 `cat` 工具输出位于容器根文件系统的 `/etc/passwd` 文件的内容：

```bash
$ podman run --rm ubuntu:latest cat /etc/passwd
```

```
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
_apt:x:100:65534::/nonexistent:/usr/sbin/nologin
```

将容器内的 `/etc/passwd` 文件内容与主机系统上的 `/etc/passwd` 文件内容进行比较，并注意它缺少主机上存在的所有用户，这证实了 `cat` 命令是在容器环境中执行的。还要注意，容器的启动、命令执行和退出都在几秒钟内完成的。与启动一个完整的操作系统、执行任务并关闭虚拟机所需的时间相比，你将开始体会容器的速度和效率。

要启动容器并保持其运行并访问 shell，可以使用以下命令：

```bash
$ podman run --name=mycontainer -it ubuntu:latest /bin/bash
```




注意：在移除镜像之前，必须先移除基于该镜像的所有容器。

### 31.7 移除容器

即使容器已经退出或被停止，它仍然存在，并且可以随时重启。如果容器不再需要，可以在停止容器后使用 `podman rm` 命令将其删除，如下所示：

```
podman rm mycontainer2
```

### 31.8 使用 Buildah 构建容器

`Buildah` 允许从现有容器、镜像或完全从零构建新容器。`Buildah` 还包含了挂载容器文件系统的功能，以便从宿主机上对其进行访问和修改。

例如，以下 `buildah` 命令将从 `Ubuntu Base` 镜像构建容器（如果镜像尚未从注册仓库拉取，`buildah` 将在创建容器之前下载它）：

```bash
buildah from docker://docker.io/library/ubuntu:latest
```

运行此命令的结果将得到一个名为 `ubuntu-working-container` 的容器，并已准备就绪：

```bash
buildah run ubuntu-working-container cat /etc/passwd
```

### 31.9 总结

本章介绍了如何在 Ubuntu 上使用 `podman`、`skopeo` 和 `buildah` 工具创建和管理 Linux 容器。

# 32. 搭建 Ubuntu Web 服务器

在构成 Ubuntu 操作系统的许多软件包中，包含了 `Apache` Web 服务器。事实上，Ubuntu 的可扩展性和韧性使其成为托管即使是流量最大的网站的理想平台。

在本章中，我们将解释如何使用 `Apache` 配置 Ubuntu 系统以作为 Web 服务器，包括安全的（HTTPS）配置和不安全的（HTTP）配置。

### 32.1 配置 Ubuntu Web 服务器的要求

要建立你自己的网站，你需要一台计算机（或云服务器实例）、一个操作系统、一个 Web 服务器、一个域名、一个名称服务器以及一个 IP 地址。

在操作系统方面，我们自然假设你正在使用 Ubuntu。如前所述，Ubuntu 支持 `Apache` Web 服务器，一旦操作系统运行，就可以轻松安装。域名可以在任何域名注册服务处进行注册。

如果你在云实例上运行 Ubuntu，提供商分配的 IP 地址将列在服务器概览信息中。如果你在托管自己的自己的服务器，并且你的互联网服务提供商（ISP）分配了静态 IP 地址，那么你需要将你的域名与该地址关联。这是通过使用名称服务器实现的，所有域名注册服务都会为你提供此服务。

如果你没有静态 IP 地址（即你的 ISP 提供一个经常变化的动态地址），你可以使用许多免费的动态 DNS（简称 `DDNS` 或 `DynDNS`）服务之一，这些服务可以将你的动态 IP 地址映射到你的域名。

一旦你配置了域名和名称服务器，下一步是安装并配置你的 Web 服务器。

### 32.2 安装 Apache Web 服务器软件包

Ubuntu 的当前版本通常不会默认安装 `Apache` Web 服务器。要检查服务器是否已安装，请运行以下命令：

```bash
apt -qq list apache
```

如果 `apt` 生成了类似下面的输出，说明 `apache` 服务器已经安装：

```
apache2/bionic-updates,bionic-security,now 2.4.29-1ubuntu4.13 amd64 [installed]
```

如果 `apt` 输出未列出软件包或未包含 `[installed]` 状态，请在命令行提示符处运行以下命令执行 `Apache` 安装：

```bash
apt install apache2
```

### 32.3 配置防火墙

在启动和测试 `Apache` Web 服务器之前，需要修改防火墙以允许 Web 服务器与外部世界通信。默认情况下，`HTTP` 和 `HTTPS` 协议分别使用端口 `80` 和 `443`，因此，根据所使用的协议，需要打开这些端口中的一个或两个。如果你的 Ubuntu 系统受 Uncomplicated Firewall（简单防火墙）的保护，可以使用以下命令仅启用不安全的 Web 流量（HTTP）：

```bash
ufw allow Apache
```

仅启用安全的（HTTPS）流量：

```bash
ufw allow 'Apache Secure'
```

或者，按照如下方式同时启用安全和不安全的 Web 流量：

```bash
ufw allow 'Apache Full'
```

如果你使用 `firewalld`，可以使用以下命令打开 `HTTP` 和 `HTTPS` 端口。在打开端口时，务必指定适用于面向互联网的网络连接的防火墙区域：

```bash
firewall-cmd --permanent --zone=<zone> --add-port=80/tcp
firewall-cmd --permanent --zone=<zone> --add-port=443/tcp
```

打开必要的端口后，务必重新加载防火墙设置：

```bash
firewall-cmd --reload
```

在云托管服务器上，可能还需要在云控制台中为服务器实例启用相应的端口。请检查云提供商的文档以获取如何操作的步骤。

### 32.4 端口转发

如果托管 Web 服务器的 Ubuntu 系统位于受防火墙保护的网络上（另一台运行防火墙的计算机，或者带有内置防火墙保护的路由器或无线基站），你需要配置防火墙将端口 `80` 和/或端口 `443` 转发到你的 Web 服务器系统。执行此操作的机制因防火墙而异，请查阅文档了解如何配置端口转发。

### 32.5 启动 Apache 服务器

在安装 `Apache` 服务器并配置防火墙后，下一步是验证服务器正在运行并启动它。

要从命令行检查 `Apache` 服务的状态，输入以下命令：

```bash
systemctl status apache2
```

如果上述命令指示 `httpd` 服务未运行，可以通过以下方式启动：

```bash
systemctl start apache2
```

如果你希望 `httpd` 服务在系统启动时自动启动，请运行以下命令：

```bash
systemctl enable apache2
```

### 32.6 测试 Web 服务器

安装完成后，下一步是验证 Web 服务器是否已启动。

如果你可以本地或远程访问服务器的桌面环境，只需启动 Web 浏览器并在地址栏中输入 `http://127.0.0.1`（`127.0.0.1` 是回环网络地址，告诉系统连接到本地）。如果一切设置正确，浏览器应加载如[图 32-1]所示的页面：

![](ubuntu_18.04_apache_test_page.jpg

图 32-1

如果没有桌面环境，请通过同一本地网络上的其他系统连接，或者使用分配给系统的外部 IP 地址连接。

### 32.7 为你的域名配置 Apache Web 服务器

设置 Web 服务器的下一步是为你的域名配置它。要配置 Web 服务器，首先切换目录到 `/etc/apache2`，该目录同样包含许多文件和子目录。主配置文件名为 `apache2.conf`，作为组织子目录中模块化配置文件的中心点。例如，`apache2.conf` 文件包含一行用于导入在 `sites-enabled` 文件夹中声明的配置设置：

```apache
# Include the virtual host configurations:
IncludeOptional sites-enabled/*.conf
```

同样，`apache2.conf` 文件导入了 `ports.conf` 文件，该文件定义了 Apache 服务器监听网络流量的端口。





## 配置

将默认文件复制到一个与你的域名匹配名称的新文件中。例如：

```bash
cp 000-default.conf myexample.conf
```

使用你喜喜欢的编辑器编辑 `myexample.com` 文件，其内容将如下：

```apache
<VirtualHost *:80>
    # ServerName 指令设置了服务器用于识别身份的请求方案、
    # 主机名和端口。这用于创建
    # 重定向 URL。在虚拟主机的上下文中，ServerName
    # 指定了请求的 Host: 头部中必须出现的主机名，以便
    # 此虚拟主机。对于默认虚拟主机（此文件），
    # 值不是决定性的，因为无论如何它都会作为最后的备选主机。
    # 但是，对于任何进一步的虚拟主机，你必须显式设置它。
    #ServerName www.example.com
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html
    # 可用的日志级别：trace8, ..., trace1, debug, info, notice, warn,
    # error, crit, alert, emerg。
    # 也可以为特定 
    # 模块配置日志级别，例如：
    #LogLevel info ssl:warn
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
    # 对于来自 conf-available/ 的大多数配置文件（
    # 它们在全局范围内启用或禁用），可以
    # 为某一个特定的虚拟主机包含一行。例如，
    # 下面行仅在此主机启用 CGI 配置，
    # 在通过“a2disconf”全局禁用它之后。
    #Include conf-available/serve-cgi-bin.conf
</VirtualHost>
```

`ServerAdmin` 指令为想要联系网站管理员的人定义了一个管理邮箱地址。将其更改为可以联系你的适当邮箱地址：

```apache
ServerAdmin webmaster@myexample.com
```

接下来，需要取消 `ServerName` 指令的注释（即删除前面的 `#` 字符）并定义，以便 Web 服务器知道此配置文件指向哪个虚拟主机：

```apache
ServerName myexample.com
```

在下一个阶段，我们需要使用 `DocumentRoot` 指令定义网站文件所在的位置。传统做法是 `/var/www/domain-name`：

```apache
DocumentRoot /var/www/myexample.com
```

完成更改后，我们现在需要如下所示启用站点：

```bash
a2ensite myexample.conf
```

此命令从 `sites-available` 目录下的 `myexample.conf` 文件到 `sites-enabled` 文件夹创建一个符号链接。

启用站点后，运行以下命令禁用默认测试站点：

```bash
a2dissite 000-default.conf
```

接下来，创建 `/var/www/myexample.com` 目录并在其中放置一个 `index.html` 文件。例如：

```html
<html>
<title>Sample Web Page</title>
<body>
Welcome to MyExample.com
</body>
</html>
```

完成这些更改后，运行 `apache2ctl` 命令检查配置文件是否存在错误：

```bash
apache2ctl configtest
```

Syntax OK

如果没有报告任何错误，请重新加载 Apache Web 服务器以确保它摄取了我们的新设置：

```bash
systemctl reload apache2
```

最后，通过打开浏览器窗口并使用域名而不是 IP 地址访问站点，检查服务器配置是否正常工作。加载的网页应该是应该是上面创建的 `index.html` 文件中定义的那个。

## 32.8 安全网站的基础

本章到目前为止创建的 Web 服务器和网站使用 80 端口上的 HTTP 协议，因此被认为是不安全的。问题在于 Web 服务器与客户端（通常是用户的 浏览器）之间的流量是以明文传输的。换句话说，数据未加密且容易被拦截。虽然对于一般的网页浏览来说这不是问题，但在执行登录网站或传输敏感信息等任务时，这是一个严重的缺陷。

## 32.9 为 Apache 配置 HTTPS

默认，Apache 服务器不包含实现 HTTPS 所需的模块。因此，第一步是启用 `mod_ssl` 模块：

```bash
a2enmod ssl
```

安装后重启 httpd 加载新模块：

```bash
systemctl restart apache2
```

使用以下命令检查模块是否已加载到服务器：

```bash
apache2ctl -M | grep ssl
```

一旦安装了模块，重复上一节的步骤来创建配置文件，这次使用 `sites-available/default-ssl.conf` 作为模板。

## 32.10 获取 SSL 证书

网站的证书必须从证书颁发机构（CA）获取。在不同的价格范围内有多种选择。然而，目前最好的选项是从 Let’s Encrypt 获取免费证书。从 Let’s Encrypt 获取证书的过程仅涉及安装和运行 `certbot` 工具。该工具将扫描服务器上的 Apache 配置文件，并提供为系统上配置的任何虚拟主机生成证书的选项。它将生成证书并向 Apache 配置添加虚拟主机条目。

使用以下步骤在你的 Ubuntu 系统上安装 `certbot` 工具：

```bash
apt update
apt install software-properties-common
add-apt-repository universe
add-apt-repository ppa:certbot/certbot
apt install certbot python-certbot-apache
```

安装 `certbot` 后，按如下方式运行它：

```bash
certbot --apache
```




在 `/etc/apache2/sites-available/myexample-le-ssl.conf` 创建了 SSL 虚拟主机

正在向虚拟主机 `/etc/apache2/sites-available/myexample-le-ssl.conf` 部署证书

启用可用站点：`/etc/apache2/sites-available/myexample-le-ssl.conf`

`Certbot` 还在 `/etc/apache2/sites-available` 目录下创建了一个名为 `myexample-le-ssl.conf` 的新文件，该文件包含每个已生成证书并启用的域名的安全虚拟主机条目，并启用了该站点（在 `/etc/apache2/sites-enabled` 目录下创建了指向该文件的链接）。这些条目类似于：

```apache
<IfModule mod_ssl.c>
<VirtualHost *:443>
.
.
    ServerName myexample.com
    ServerAdmin webmaster@myexample.com
    DocumentRoot /var/www/myexample.com
.
.
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
.
.
SSLCertificateFile /etc/letsencrypt/live/myexample.com/fullchain.pem
SSLCertificateKeyFile /etc/letsencrypt/live/myexample.com/privkey.pem
Include /etc/letsencrypt/options-ssl-apache.conf
</VirtualHost>
</IfModule>
```

最后，`Certbot` 将询问服务器是否应将未来的 HTTP Web 请求重定向到 HTTPS。换之，如果用户尝试访问 `http://www.myexample.com`，Web 服务器会将用户重定向到 `https://www.myexample.com`：

请选择是否将 HTTP 流量重定向到 HTTPS 并移除 HTTP 访问。

- `1`: 不重定向 - 不对 Web 服务器配置做任何进一步更改。
- `2`: 重定向 - 将所有请求重定向到安全的 HTTPS 访问。对于新站点或如果你确定站点在 HTTPS 上运行正常请选择此项。你可以通过编辑 Web 服务器配置来撤销此更改。

选择相应的数字 `[1-2]` 然后按 `[enter]`（按 ‘c’ 可消）：`2`

如果你目前正在测试 HTTPS 配置并希望稍后之前保留 HTTP 版本，请选择“不重定向”选项。否则，通常建议重定向到 HTTPS。

一旦证书安装完成，在浏览器中访问以下 URL 进行测试（将 `myexample.com` 替换为你自己的域名）：
`https://www.ssllabs.com/ssltest/analyze.html?d=www.myexample.com`

如果证书配置成功，SSL Labs 将提供高评分，如图 32-2 所示：

![](img/rhel_8_ssl_labs_report.jpg)
图 32-2

作为最后的测试，打开浏览器窗口并使用 `https://` 前缀导航到你的域名。页面应像以前一样加载，浏览器应指示浏览器与服务器之间的连接是安全的（通常由地址栏中的锁图标指示，点击它可以查看更多信息）：

![](img/rhel_8_web_site_secure.jpg)
图 32-3

### 32.1 总结

可以通过安装 Apache Web 服务器来使用 Ubuntu 系统托管网站。Ubuntu 上可以部署不安全的 (HTTP) 和安全的 (HTTPS) 网站。安全的网站使用安全套接层 (SSL) 或传输层安全协议 (TLS)，通过公共、私有和会话加密以及由受信任证书颁发机构发布的证书，在 Web 服务器和客户端之间建立加密通信。

### 33 配置 Ubuntu Postfix 电子邮件服务器

除了作为 Web 服务器，电子邮件是 Ubuntu 系统的主要用途之一，特别是在业务环境中。鉴于电子邮件的重要普及，某些人发现 Linux 系统上的电子邮件结构如此复杂会感到惊讶，这种复杂性对于 Ubuntu 新手来说往往可能有些无从心。

好消息是，大部分复杂性是为了让丰富的电子邮件管理员能够为大型企业安装实现复杂的配置。事实上，对于大多数 Linux 管理员来说，设置一个基础电子邮件系统以便用户能够发送和接收邮件是相对直接的。

在《Ubuntu 基础》本章中，我们将解释基于 Linux 的电子邮件配置的基础知识，并逐步配置基础电子邮件环境。为了提供核心要点，我们将电子邮件系统的复杂性留给关于该主题的进级书籍。

#### 33.1 电子邮件系统的结构

一个完整的电子邮件系统由多个组件组成。以下是每个组件的简要描述：

##### 33.1.1 邮件用户代理 (MUA)

这是普通用户最熟悉的系统部分。邮件用户代理 (`MUA`) 或邮件客户端，是用于撰写、发送和读取电子邮件消息的应用程序。Linux 上典型的 `MUA` 有 `Evolution`、`Thunderbird` 和 `KMail`。对于偏好文本格式邮件的用户，还有 `pine`。

##### 33.1.2 邮件传输代理 (MTA)

邮件传输代理 (`MTA`) 是电子邮件系统的一部分，负责大部分将消息从一台计算机传输到另一台计算机的工作（在同一网络内或通过互联网传输到远程系统）。一旦配置正确，大多数用户将不会与所选的 `MTA` 有直接交互。有很多 `MTA` 可选，包括 `sendmail`、`Postfix`、`Fetchmail`、`Qmail` 和 `Exim`。

##### 33.1.3 邮件投递代理

另一个对用户隐藏的部分，邮件投递代理 (`MDA`) 位于 `MTA` 和邮件客户端 (`MUA`) 之间，对电子邮件消息进行过滤。最常见的 `MDA` 形式是用于垃圾邮件的过滤器。流行的 `MDA` 有 `Spamassin` 和 `Procmail`。需要注意的是，某些 `MUA` 应用程序（如 `Evolution`、`Thunderbird` 和 `KMail`）自带 `MDA` 过滤功能，而其他的（如 `Pine`）则没有。这会让 Linux 初学者感到困惑。

##### 33.1.4 SMTP

`SMTP` 是简单邮件传输协议的缩写。这是电子邮件系统在服务器之间传输邮件消息的协议。该协议本质上是 `MTA` 之间通信并往来传输消息的语言。

##### 33.1.5 SMTP 中继

`SMTP Relay` 是一种允许使用外部 `SMTP` 服务器发送电子邮件而不是托管本地 `SMTP` 服务器的协议。这通常涉及使用 `MailJet`、`SendGrid` 或 `MailGun` 等服务。

#### 33.2 配置 Ubuntu 电子邮件服务器

许多系统使用 `Sendmail` `MTA` 传输电子邮件，在许多 Linux 发行版中这是默认的邮件传输代理。然而，`Sendmail` 是一个复杂的系统，对于初学者和资深用户来说都难以理解和配置。由于它认为其处理电子邮件消息的速度慢于许多较新的 `MTA`，它也正在失去青睐。

许多系统管理员现在使用 `Postfix` 或 `Qmail` 来处理电子邮件。它们都比 `Sendmail` 更快且更于配置。

因此，为了本章的目的，我们将 `Postfix` 作为一种 `MTA`，因为它简单且流行。如果你更倾向于使用 `Sendmail`，有许多专门研究该主题的书籍，它们比我们本章的内容要深入得多。



作为第一步，本章将介绍如何配置 Ubuntu 系统以作为一个全邮件服务器。在章节的后半部分，还将介绍如何使用 SMTP 中继服务的步骤。

## 33.3 Postfix 安装前的准备工作

在安装 Postfix 之前的第一步是确保你的系统中没有在运行 `Sendmail`。你可以使用以下命令进行检查：

```
systemctl status sendmail
```

如果系统中没有安装 `sendmail`，该工具将显示一条与以下内容类似的消息：

`Unit sendmail.service could not be found.`

如果 `sendmail` 正在你的系统上运行，则在安装和配置 Postfix 之前必须停止它。要停止 `sendmail`，请运行以下命令：

```
systemctl stop sendmail
```

下一步是确保在系统重启时 `sendmail` 不会重新启动：

```
systemctl disable sendmail
```

现在，`Sendmail` 已经关闭，并且已被配置为在系统启动时不自动启动。可选情况下，若要从系统中完全删除 `sendmail`，请运行以下命令：

```
apt remove sendmail
```

## 33.4 防墙/路由器配置

由于邮件消息的收发涉及网络连接，因此需要配置防火墙允许 SMTP 流量。如果 `firewalld` 处于激活状态，请如下方式使用 `firewall-cmd` 工具：

```
firewall-cmd --permanent --add-service=smtp
```

或者，如果启用了 `ufw`，使用以下命令配置其允许 SMTP 流量：

```
ufw allow Postfix
```

此外，配置服务器与互联网之间的任何其他防火墙或路由器以允许端口 25、143 和 587 的连接也是重要的，并在必要时为这些端口配置端口转发到邮件服务器上相应的端口。

完成这些初始步骤后，我们现在可以安装 Postfix 了。

## 33.5 在 Ubuntu 上安装 Postfix

默认情况下，Ubuntu 的安装过程会在大多数配置中安装 `postfix`。要验证 `postfix` 是否已安装，请使用以下 `apt` 命令：

```
apt -qq list postfix
```

如果 `apt` 报告 `postfix` 未安装，则可以通过以下方式安装：

```
apt install postfix
```

在大多数情况下，“Internet Site”（互联网站点）选项将是最有用的选项。这将配置一些基础设置，用于发送和接收与你的网站域名相关的消息。选择此选项后，按下 `Enter` 键继续到下一个屏幕：

![](img/ubuntu_18.04_postfix_setup_domain.jpg)

图 33-1

在上面的屏幕上，在再次按下 `Enter` 键之前输入你的域名。

## 33.6 配置 Postfix

`postfix` 的主要配置设置位于 `/etc/postfix/main.cf` 文件中。互联网上有许多资源提供了关于 `postfix` 的详细信息，因此本节将重点关注让邮件运行起来所需的基础选项。尽管 `apt` 安装设置了一些基础配置选项，但它往往会漏掉某些设置，并对其他设置进行错误的猜测，因此请务必仔细检查 `main.cf` 文件。

`main.cf` 文件中的关键选项是：

```
myhostname = mta1.domain.com
mydomain = domain.com
myorigin = $mydomain
mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain
inet_interfaces = $myhostname
mynetworks = subnet
```

其他设置要么已由安装过程为你设置好，要么除非你觉得好奇并想配置一个更复杂的邮件系统，否则是不需要的。

`myhostname` 的格式为 `host.domain.extension`。例如，如果你的 Linux 系统名为 `MyLinuxHost` 且你的互联网域名为 `MyDomain.com`，你将如下设置 `myhostname` 选项：

```
myhostname = mylinuxhost.mydomain.com
```

`mydomain` 设置仅仅是上述设置的域名部分。例如：

```
mydomain = mydomain.com
```

`myorigin` 设置定义了输出邮件在到达收件人收箱时看起来发自的域名名称，它应设置为你的域名：

```
myorigin = $mydomain
```

也许最关键的参数之一 `mydestination` 与入站邮件有关，它声明此服务器作为最终投递地地的域名。任何发往不在此列表中的域名入站邮件都将被视为中继请求，根据 `mynetworks` 设置（下文概述），这通常会导致投递失败。

`inet_interfaces` 设置定义了系统上允许 `postfix` 接收邮件的网络接口，通常被设置为 `all`：

```
inet_interfaces = all
```

`mynetworks` 设置定义了哪些外部系统被信任可以使用服务器作为 SMTP 中继。该设置的可能值如下：

* `host` - 仅本地系统受信任。所有外部客户端尝试使用服务器作为中继的尝试将被拒绝。
* `subnet` - 仅允许同一网络子网上的系统使用服务器作为中继。例如，如果服务器的 IP 地址为 `192.168.1.29`，IP 地址为 `192.168.1.30` 的客户端系统将能够使用服务器作为中继。
* `class` - 同一 IP 地址类内的系统可以使用服务器作为中继。

信任的地址也可以通过手动指定子网、地址范围或引用文件来定义。以下示例声明了本地和子网 `192.168.0.0/24` 为信任地址。

对于此示例，将属性设置为 `subnet` 以以便网络上的任何其他系统发送邮件。

`main.cf` 中的关键设置可能所示：

```
biff = no
append_dot_mydomain = no
readme_directory = no
compatibility_level = 2
smtpd_banner = $myhostname (Ubuntu)
myhostname = hostname.myexample.com
alias_maps = hash:/etc/aliases
alias_database = hash:/etc/aliases
mydomain = myexample.com
myorigin = $mydomain
mydestination = $myhostname, myexample.com, localhost.localdomain, localhost
relayhost = 
mynetworks = subnet
mailbox_size_limit = 0
recipient_delimiter = +
inet_interfaces = all
inet_protocols = all
smtpd_cert_file = /etc/ssl/certs/ssl-snakeoil.pem
smtpd_key_file = /etc/ssl/private/ssl-snakeoil.key
smtpd_use_tls = yes
smtpd_relay_restrictions = permit_mynetworks permit_sasl_authenticated defer_unauth_destination
```

## 33.7 在 Ubuntu 系统上启动 Postfix

一旦 `/etc/postfix/main.cf` 文件配置了正确的设置，现在是启动 Postfix 的时间了。可以通过如下命令行来实现实现：

```
systemctl start postfix
```

如果 Postfix 已经在运行，请使用以下命令加载配置更改：

```
systemctl reload postfix
```

若要配置 Postfix 在系统启动时自动启动，请运行以下命令：

```
systemctl enable postfix
```



Postfix 进程现在应该启动了。验证一切运行正常的最佳方法是检查您的邮件日志。这通常位于 `/var/log/mail.log` 文件中，现在应该包含一条类似于下面的输出的条目：

```
Mar 25 11:21:48 demo-server postfix/postfix-script[5377]: starting the Postfix mail system
Mar 25 11:21:48 demo-server postfix/master[5379]: daemon started -- version 3.3.1, configuration /etc/postfix
```

只要没有记录错误信息，你就已经成功安装并启动了 postfix，并准备好测试 postfix 配置了。

# 33.9 测试 Postfix

测试 postfix 配置的一种简单方法是在系统的本地用户之间发送电子邮件消息。若要进行快速测试，请按照如下方式使用 `mail` 工具（其中 `name` 和 `mydomain` 分别替换为系统上的用户名和您的域名名）：

```
# mail name@mydomain.com
```

如果无法使用 `mail` 工具，可以通过以下方式安装：

```
# apt install mailutils
```

在提示时，为邮件消息输入主题，然后输入消息正文。。要发送邮件消息，只需按 `Ctrl-D`。例如：

```
# mail demo@mydomain.com

Subject: Test email message

This is a test message.

EOT
```

再次运行 `mail` 命令，这次使用另一个用户，并验证消息是否已发送并接收：

```
$ mail
"/var/mail/demo": 1 message 1 new
>N 1 demo Wed Apr 15 15:30 13/475 Test email message
?
```

如果消息没有出现，请检查日志文件（`/var/log/mail.log`）查看是否存在错误。成功的邮件投递将如下所示显示在日志文件中：

```
Mar 25 13:41:37 demo-server postfix/pickup[7153]: 94FAF61E8F4A: uid=0 from=<root>
Mar 25 13:41:37 demo-server postfix/cleanup[7498]: 94FAF61E8F4A: message-id=<20190325174137.94FAF61E8F4A@demo-server.mydomain.com>
Mar 25 13:41:37 demo-server postfix/qmgr[7154]: 94FAF61E8F4A: from=<root@mydomain.com>, size=450, nrcpt=1 (queue active)
Mar 25 13:41:37 demo-server postfix/local[7500]: 94FAF61E8F4A: to=<neil@mydomain.com>, relay=local, delay=0.12, delays=0.09/0.01/0/0.02, dsn=2.0.0, status=sent (delivered to mailbox)
Mar 25 13:41:37 demo-server postfix/qmgr[7154]: 94FAF61E8F4A: removed
```

一旦本地邮件工作正常，尝试向外部地址（如 GMail 账户）发送邮件。此外，通过外部账户向您域名上的用户发送邮件，以测试接收邮件是否正常。在每种情况下，请检查 `/var/log/mail.log` 文件以获取任何错误的解释。

# 33.10 通过 SMTP 中继服务器发送邮件

配置邮件服务器处理发出的邮件消息的替代方案是使用 SMTP 中继服务。如之前讨论过的，有许多可用服务，其中大多数可以通过网络搜索“SMTP Relay Service”来找到。这些服务中的大多数将要求您以某种方式验证您的域名，并提供 MX 记录以更新您的 DNS 设置。您还将获得一个用户名和密码，这些需要被添加到 postfix 配置中。本节其余部分假设 postfix 已经安装在您的系统中，并且您选择的 SMTP 中继提供商所需的所有初始步骤已完成。

开始编辑 `/etc/postfix/main.cf` 文件，并使用您的域名配置 `myhostname` 参数：

```
myhostname = mydomain.com
```

接下来，在 `/etc/postfix` 中创建一个名为 `sasl_passwd` 的新文件，并添加一行包含中继服务提供的邮件服务器主机、用户名和密码的行。例如：

```
[smtp.myprovider.com]:587 neil@mydomain.com:mypassword
```

注意，上面的条目也指定了端口 `587`。如果没有此设置，postfix 将默认使用端口 `25`，而该端口被大多数 SMTP 中继服务提供商默认锁定。

创建密码文件后，使用 `postmap` 工具生成包含邮件凭据的哈希数据库：

```
# postmap /etc/postfix/sasl_passwd
```

在继续之前，采取额外步骤来保护您的 postfix 凭据：

```
# chown root:root /etc/postfix/sasl_passwd /etc/postfix/sasl_passwd.db
# chmod 0600 /etc/postfix/sasl_passwd /etc/postfix/sasl_passwd.db
```

再次编辑 `main.cf` 文件并添加条目以指定中继主机：

```
relayhost = [smtp.myprovider.com]:587
```

在 `main.cf` 文件中添加以下行以配置 SMTP 验证：

```
smtp_use_tls = yes
smtp_sasl_auth_enable = yes
smtp_sasl_password_maps = hash:/etc/postfix/sasl_passwd
```

最后，重启服务：

```
# systemctl restart postfix
```

# 33.11 总结

完整的端到端系统由邮件用户代理 (MUA)、邮件传输代理 (MTA)、邮件交付代理 (MDA) 组成。本章概述了如何在 Ubuntu 上安装、配置和测试 postfix。

# 34. 为 Ubuntu 添加硬盘

用户遇到的第一个问题之一是系统磁盘空间不足。在接下来的章节中，我们将查看使用磁盘所需的步骤。

## 34.1 挂载文件系统或逻辑卷

在 Ubuntu 上配置新磁盘有两种方法。一种方法是在硬盘上创建一个或多个分区，在分区上创建文件系统，然后将其挂载到特定的挂载点。这种方法将在本章介绍。

另一种方法是将空间添加到现有的卷组。当安装 Ubuntu 时选择逻辑卷时，会创建一个名为 `vgubuntu` 的卷组。该卷组有两个名为 `root` 和 `swap_1` 的逻辑卷，分别用于 `/` 和交换分区。通过将新磁盘配置为卷组的一部分，我们可以增加现有逻辑卷的可用磁盘。通过这种方法，我们能够通过分配新磁盘上的部分或全部空间来增加 `/home` 文件系统的大小。

## 34.2 寻找硬盘

本教程假设一个新的物理或虚拟硬盘已安装在系统中并对操作系统可见。一旦添加，新硬盘应被操作系统自动检测。通常，系统中的磁盘驱动被分配以 `sd` 开头加上表示设备数字字母的设备名称。例如，第一个设备可能是 `/dev/sda`，第二个可能是 `/dev/sdb`，依此类推。

以下是一个只有一个硬盘连接到 SATA 控制器的典型系统的输出：

```
# ls /dev/sd*
/dev/sda /dev/sda1 /dev/sda2
```

这显示由 `/dev/sda` 表示的磁盘驱动本身被分为 2 个分区，由 `/dev/sda1` 和 `/dev/sda2` 表示。

以下是安装第二个硬盘驱动后，同一系统的输出：

```
# ls /dev/sd*
/dev/sda /dev/sda1 /dev/sda2 /dev/sdb
```

如所示，新硬盘已被分配给设备文件 `/dev/sdb`。目前该硬盘没有显示分区（因为我们尚未创建任何分区）。





此时，我们有两种选择：在新驱动器上创建分区和文件系统并挂载它们以便访问，或者将磁盘作为物理卷添加到卷组中。若要执行前者，请继续本章节；否则，请阅读向 Ubuntu 卷组和逻辑卷添加新磁盘以了解配置逻辑卷的详情。

## 34.3 创建 Linux 分区

下一步是在新磁盘驱动器上创建一个或多个 Linux 分区。这是通过 `fdisk` 工具实现的，它将要分区的设备作为命令行参数传递：

```
fdisk /dev/sdb
```

```
Welcome to fdisk (util-linux 2.32.1).
更改将保留在内存中，直到你决定写入它们。
在使用 write 命令前请小心。
设备未包含识别的分区表。
Created a new DOS disklabel with disk identifier 0xbd09c991.
Command (m for help):
```

要查看磁盘上的当前分区，请输入 `p` 命令：

```
Command (m for help): p
Disk /dev/sdb: 8 GiB, 8589934592 bytes, 16777216 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0xbd09c991
```

如从上面的 fdisk 输出中所示，磁盘目前没有分区，因为它是一个之前未使用的磁盘。下一步是在磁盘上创建一个新分区，该任务通过输入 `n`（代表新分区）和 `p`（代表主分区）来完成：

``````
Command (m for help): n
Partition type
   p primary (0 primary, 0 extended, 4 free)
   e extended (container for logical partitions)
Select (default p): p
```

在示例示例中，我们只计划创建一个分区，它将是分区 1。接下来，我们需要指定分区的起始和结束位置。由于这是第一个分区，我们需要它从第一个可用扇区开始，并且因为我们要使用整个磁盘，因此我们将最后一个扇区指定为结束位置。注意，如果你想创建多个分区，可以通过扇区、字节、千字节或兆字节来指定每个分区的大小。

```
Partition number (1-4, default 1): 1
First sector (2048-16777215, default 2048):
Last sector, +sectors or +size{K,M,G,T,P} (2048-16777215, default 16777215):
Created a new partition 1 of type ‘Linux’ and of size 8 GiB.
Command (m for help):
```

现在我们已经指定了分区，需要使用 `w` 命令将其写入磁盘：

```
Command (m for help): w
```

分区表已修改。
正在调用 `ioctl()` 重新读取分区表。
正在同步磁盘。

如果我们现在再次查看设备，将看到新分区作为 `/dev/sdb1` 可见：

```
ls /dev/sd*
/dev/sda /dev/sda1 /dev/sda2 /dev/sdb /dev/sdb1
```

下一步是在我们的新分区上创建文件系统。

## 34.4 在磁盘上创建文件系统

现在我们已经安装了一个新磁盘，它对 Ubuntu 可见，并且我们在磁盘上配置了一个 Linux 分区。下一步是在分区上创建一个文件系统，以便操作系统可以使用它存储文件和数据。在分区上创建文件系统的简单方法是使用 `mkfs.xfs` 工具：

```
apt install xsprogs
mkfs.xfs /dev/sdb1
```

在这种情况下，我们创建了一个 XFS 文件系统。XFS 是一种高性能文件系统，在 I/O 性能和日志使用方面许多优势。

## 34.5 日志文件系统概述

日志文件系统会在磁盘写入期间对文件系统所做的更改保留日志或记录，这些日志可以用于快速恢复由于系统崩溃或停电等事件可能导致的损坏。

使用日志文件系统有很多优势。多年来，存储在磁盘驱动器上的数据大小和都在增长。非日志文件系统的问题是，崩溃后必须运行 `fsck`（文件系统一致性检查）工具。`fsck` 工具将扫描整个文件系统，验证所有条目并确保块被正确分配和引用。如果它发现损坏的条目，它将尝试修复问题。这里的问题有两个方面：首先，`fsck` 工具并不总是能够修复损坏，你最终会在 `lost+found` 目录中得到数据，而系统不再知道它们原来在哪里。另一个问题是时间问题。在大文件系统上完成 `fsck` 过程可能需要很长时间，可能导致不可接受的停机时间。

相反，日志文件系统在磁盘的日志区域记录信息（日志和记录不需要在同一设备上），这是在每次写入期间进行的。日志记录的信息是可配置的，范围从从不记录任何内容到记录元数据（例如所有权、时间戳等），以及写入文件系统的实际块。一旦日志更新，系统就会在文件系统中标记数据已提交。崩溃后可以使用日志非常快速地恢复在线，从而将使用 `fsck` 需要几分钟的时间缩短到几秒钟，此外如此。

## 34.6 挂载文件系统

现在我们已经在新磁盘的 Linux 分区上创建了文件系统，我们需要挂载它以便访问和使用。为了这一点，我们需要创建一个挂载点。挂载点简单来说就是挂载文件系统的目录或文件夹。为了本示例，我们将创建一个 `/backup` 目录以匹配文件系统（尽管这些值并不匹配）：

```
mkdir /backup
```

然后可以使用 `mount` 命令手动挂载文件系统：

```
mount /dev/sdb1 /backup
```

不带任何参数运行 `mount` 命令将显示所有已挂载的文件系统（包括我们的新文件系统）：

```
mount
sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime,seclabel)
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
.
.
/dev/sdb1 on /backup type xfs (rw,relatime,attr2,inode64,logbufs=8,logbsize=32k,noquota)
```

## 34.7 配置 Ubuntu 自动挂载文件系统

为了设置系统在启动时自动挂载新文件系统，需要在 `/etc/fstab` 文件中添加条目。`fstab` 条目的格式如下：

`<device> <dir> <type> <options> <dump> <fsck>`

这些条目可以总结如下：

- `<device>` - 要挂载文件系统的设备。
- `<dir>` - 作为文件系统挂载点的目录。
- `<type>` - 文件系统类型（xfs, ext4 等）。
- `<options>` - 额外的文件系统挂载选项，例如使文件系统变为只读或控制哪些用户可以挂载文件系统。运行 `man mount` 查看完整的选项列表。将此值设置为默认值将使用文件系统的默认设置（rw, suid, dev, exec, auto, nouser, async）。





- `dump` - 决定文件系统内容是否包含在由 `dump` 工具执行的任何备份中。此设置很少使用，可以使用值 `0` 禁用。
- `fsck` - 决定在系统崩溃后是否由 `fsck` 对文件系统进行检查，以及检查文件检查的顺序。对于诸如 `XFS` 等带日志的文件系统，应将此项设置为 `0`，以表示不需要检查。

以下示例显示了一个配置好的 `fstab` 文件，该文件将我们的 `/backup` 分区自动挂载到 `/dev/sdb1` 分区（分区）上：

```
/dev/mapper/vgubuntu-root / ext4 errors=remount-ro 0 1
/dev/mapper/vgubuntu-swap_1 none swap sw 0 0
/dev/sdb1 /backup xfs defaults 0 0
```

现在，`/backup` 文件系统将在每次系统重新启动时自动挂载。

## 34.8 使用 Cockpit 添加磁盘

除了使用本章概述的命令行工具进行存储操作外，还可以使用 Cockpit Web 控制台配置新的存储设备。要查看当前的存储配置，请登录 Cockpit 控制台并选择 `Storage`（存储）选项，如图图 34-1 所示：

![](img/ubuntu_20.04_cockpit_storage1.jpg)

图 34-1

找到新添加的存储，滚动到 `Storage` 页面的底部直到 `Drives`（驱动器）部分可见（注意 `Drives` 部分也可能位于屏幕的右上角）：

![](img/ubuntu_20.04_cockpit_storage_disks.jpg)

图 34-2

在上述图中，新驱动器是 10 GiB 的驱动器。选择新驱动器以显示 `Drive` 屏幕，如图图 34-3 所示：

![](img/ubuntu_20.04_cockpit_storage_disk_details.jpg)

图 34-3

点击 `Create Partition Table`（创建分区表）按钮，在弹出的对话框中，接受默认设置后点击 `Format`（格式化）按钮：

![](img/ubuntu_20.04_cockpit_storage_format.jpg)

图 34-4

返回主 `Storage` 屏幕，点击 `Create Partition`（创建分区）按钮并使用对话框指定分配给此分区的空间大小、文件系统类型（推荐 `XFS`）以及可选的标签、文件系统挂载点和挂载选项。注意，如果此新分区未使用所有可用空间，随后可以在驱动器上添加附加分区。要更改文件系统是否为只读或在启动时挂载等设置，请将 `Mounting`（挂载）菜单选项更改为 `Custom`（自定义）并调整切换按钮设置：

![](img/ubuntu_20.04_cockpit_storage_create_partition.jpg)

图 34-5

一旦选择设置，点击 `Create partition` 按钮提交更改。创建完成后，新分区将添加到磁盘，创建相应的文件系统并挂载到指定的挂载点，同时对 `/etc/fstab` 文件进行相应更改。

## 34.9 总结

本章涵盖了为现有 Ubuntu 系统添加额外的物理或虚拟磁盘驱动器的主题。这是一个相对简单的过程，只需确保操作系统检测到新驱动器，在驱动器上创建一个或多个分区，然后在这些分区上创建文件系统。虽然 Ubuntu 上有多种不同的文件系统类型，但通常推荐使用 `XFS`。一旦文件系统准备就绪，它们可以使用 `mount` 命令进行挂载。为了让新创建的文件系统在系统启动时自动挂载，可以在 `/etc/fstab` 配置文件中进行添加。

## 35. 向 Ubuntu 卷组和逻辑卷添加新磁盘

在上一章中，我们查看了向 Ubuntu 系统添加新磁盘驱动器、创建分区和文件系统，然后挂载该文件系统以便访问磁盘。创建固定分区和文件系统的替代方案是使用逻辑卷管理 (`LVM`）来创建由一个或多个物理或虚拟磁盘或分区的空间组成的逻辑磁盘。使用 `LVM` 的优势在于可以根据需要向逻辑卷中添加或删除空间，而无需将数据分散在多个文件系统上。

让我们以基于 Ubuntu 的服务器的根（`/`）文件系统为例。如果没有 `LVM`，该文件系统在安装操作系统时将以特定大小创建。如果安装了新磁盘驱动器，没有方法将该空间的任何部分分配给 `/` 文件系统。唯一的选项是在新磁盘上创建新文件系统并将其挂载到特定的挂载点。在这种情况下，你在新文件系统上有充足的空间，但 `/` 文件系统仍然几乎是满的。唯一的选择是将文件移动到新文件系统。通过 `LVM`，可以将新磁盘（或其部分）分配给包含根文件系统的逻辑卷，从而动态地扩展可用空间。

在本章中，我们将查看向卷组和逻辑卷添加新磁盘空间所需的步骤，其目的是为 Ubuntu 系统的根文件系统添加额外空间。

### 35.1 逻辑卷管理 (LVM) 概述

`LVM` 提供了一种灵活管理空间的方法。不是将每个磁盘驱动器划分为创建固定大小文件系统的固定分区，`LVM` 提供了一种将空间组合成逻辑卷的方法，可以轻松调整大小和移动。此外`LVM` 允许通过分配不同的卷组或逻辑卷来精细控制分配给用户的磁盘空间。

LVM 由以下组件组成：

#### 35.1.1 卷组 (Volume Group)
`Volume Group` 是包含一个或多个逻辑卷和物理卷的高层容器。

#### 35.1.2 物理卷 (Physical Volume)
`Physical Volume` 代表磁盘驱动器或其他存储介质。

#### 35.1.3 逻辑卷 (Logical Volume)
`Logical Volume` 相当于磁盘分区，作为分区，它可以包含文件系统。

#### 35.1.4 物理区 (Physical Extent)
每个物理卷 (`PV`) 被划分为称为物理区的等大小块。

#### 35.1.5 逻辑区 (Logical Extent)
每个逻辑卷 (`LV`) 被划分为称为逻辑区的等大小块。

假设我们要创建一个名为 `VolGroup001` 的新卷组。该卷组需要磁盘空间运行，因此我们分配三个磁盘分区 `/dev/sda1`、`/dev/sdb1` 和 `/dev/sdb2`。这些成为 `VolGroup001` 中的物理卷。随后我们在由这些物理卷组成的卷组内创建一个名为 `LogVol001` 的逻辑卷。

如果 `LogVol001` 空间不足，只需添加更多磁盘分区作为物理卷并将其分配给卷组和逻辑卷即可。

## 35.2 获取逻辑卷信息

作为在 Ubuntu 中使用 `LVM` 的示例，我们将通过为标准 Ubuntu 安装的 `/` 文件系统添加空间的示例。考虑到根分区大小的灵活性需求（当然，假设在 Ubuntu 安装过程中选择了 LVM 分区选项），Ubuntu 将 `/` 文件系统设置为名为 `vgubuntu` 的卷组内的逻辑卷（名为 `root`）。然而，在对 `LVM` 设置进行任何更改之前，收集信息是重要的。

运行 `mount` 命令将输出范围挂载点的信息，包括根文件系统的条目：

```
/dev/mapper/vgubuntu-root on / type ext4 (rw,relatime,errors=remount-ro)
```

可以使用 `vgdisplay` 命令获取卷组信息：

```
# vgdisplay

--- Volume group ---
  VG Name vgubuntu
  System ID
  Format lvm2
  Metadata Areas 1
```



# 元数据序列号 3

VG 访问：读/写

VG 状态：可调整

最大 LV 0

当前 LV 2

打开 LV 2

最大 PV 0

当前 PV 1

活动 PV 1

VG 大小 <73.75 GiB

PE 大小 4.00 MiB

总 PE 18879

已分配 PE / 大小 18879 / <73.75 GiB

空闲 PE / 大小 0 / 0

VG UUID hqaagb-OgB5-3DhK-qLoN-bRHU-jsFm-LrdXtT

如上面的示例所示，`vgubuntu` 卷组的物理区大小为 `4.00MiB`，总共有约 73GB 的可用空间分配给逻辑卷。目前已分配了 18879 个物理区，等同于总容量。因此，如果我们想增加分配给 `vgubuntu` 卷组中任何逻辑卷的空间，我们需要添加一个或多个物理卷。`vgs` 工具也用于快速显示系统中卷组中可用空间的概述：

```
# vgs

VG #PV #LV #SN Attr VSize VFree
vgubuntu 1 2 0 wz--n- <73.75g 0
```

同样，可以使用 `lvdisplay` 命令获取卷组中逻辑卷的信息：

```
# lvdisplay

--- Logical volume ---
LV Path /dev/vgubuntu/root
LV Name root
VG Name vgubuntu
LV UUID iLfsLf-pVzy-yCfd-wKim-EdbW-efvm-J6p1f4
LV 写入访问：读/写
LV 创建：主机，时间 ubuntu, 2020-04-06 11:17:53 -0400
LV 状态：可用
# open 1
LV Size <72.79 GiB
当前 LE 18634
段 1
分配继承：是
预读扇区：自动
- 当前设置为 256
块设备 253:0
--- Logical volume ---
LV Path /dev/vgubuntu/swap_1
LV Name swap_1
VG Name vgubuntu
LV UUID 14Cr74-x5EW-V1k1-c5z8-8NUn-DTqC-PLEg7F
LV 写入访问：读/写
LV 创建：主机，时间 ubuntu, 2020-04-06 11:17:54 -0400
LV 状态：可用
# open 2
LV Size 980.00 MiB
当前 LE 245
段 1
分配继承：是
预读扇区：自动
- 当前设置为 256
块设备 253:1
```

如上面的示例所示，卷组 `vgubuntu` 中约 72 GiB 的空间被分配给逻辑卷 `root`（用于 `/` 文件系统），980 MiB 分配给了 `swap_1`（用于交换空间）。

现在我们知道了使用了哪些空间，了解哪些设备提供了这些空间（即哪些设备被用作物理卷）通常很有帮助。要获取这些信息，我们需要运行 `pvdisplay` 命令：

```
# pvdisplay

--- Physical volume ---
PV Name /dev/sda1
VG Name vgubuntu
PV Size <73.75 GiB / 不可用 2.00 MiB
可分配：是（但已满）
PE Size 4.00 MiB
总 PE 18879
空闲 PE 0
已分配 PE 18879
PV UUID nwp55K-Chay-x5eB-kZcc-sonL-cm3E-3SWnKG
```

显然，逻辑卷 `vgubuntu` 控制的空间是通过位于 `/dev/sda1` 的物理卷提供的。

现在我们对自己的 LVM 配置有了进一步的了解，可以开始向卷组及其包含的逻辑卷添加空间的过程了。

## 35.3 从命令行向卷组添加额外空间

与之前收集 Ubuntu 系统当前逻辑卷管理信息的步骤一样，对此配置的更改可以通过命令行进行。

在本章的剩余部分中，我们假设系统已添加了一个新磁盘，并且操作系统将其识别为 `/dev/sdb`。我们还假设这是一块不包含任何现有分区的空磁盘。如果存在现有分区，应先对其进行备份，然后使用 `fdisk` 实用程序从磁盘删除分区。例如，假设表示 `/dev/sdb` 的设备包含如下分区：

```bash
# fdisk -l /dev/sdb

Disk /dev/sdb: 10 GiB, 10737418240 bytes, 20971520 sectors
Units: 扇区 of 1 * 512 = 512 bytes
扇区大小（逻辑/物理）:512 bytes / 512 bytes
I/O 大小（最小/最优）:512 bytes / 512 bytes
磁盘类型: gpt
磁盘标识符: 6C7E15CA-C9B1-4FEB-B10A-BE75F8B6D483
Device Start End Sectors Size Type
/dev/sdb1 2048 20971186 20969439 10G Linux filesystem
```

一旦此分区上的任何文件系统已卸载，就可以按照以下方式删除它们：

```bash
# fdisk /dev/sdb

Welcome to fdisk - /dev/sdb is new.
Disk /dev/sdb: 10 GiB, 10737418240 bytes, 20971520 sectors
Units: 扇区 of 1 * 512 = 512 bytes
扇区大小（逻辑/物理）:512 bytes / 512 bytes
I/O 大小（最小/最优）:512 bytes / 512 bytes
磁盘类型: gpt
磁盘标识符: 6C7E15CA-C9B1-4FEB-B10A-BE75F8B6D483
Device Start End Sectors Size Type
/dev/sdb1 2048 20971486 20969439 10G Linux filesystem
```

（注：由于提供的原文中存在大量重复和乱码，译文已根据逻辑结构进行了清理和翻译。）



维护 Ubuntu 系统性能的一个重要部分是确保有足够的交换空间（swap space），以与系统的内存需求相匹配。因此，本章的目标是概述 Ubuntu 交换空间管理。

## 36.1 什么是交换空间？

计算机系统具有有限的物理内存，并供操作系统使用。当操作系统接近可用内存限制时，它会通过将内存页写入磁盘来释放空间。当操作系统需要这些任何一个页时，它们会被重新读回内存。为此任务分配的磁盘区域被称为交换空间。

## 36.2 Ubuntu 推荐的交换空间

Ubuntu 推荐的交换空间取决于多个因素，包括系统内存的大小、内存内存的工作负载以及系统是否需要支持休眠。Ubuntu 交换空间的当前指南如下：

| 安装的内存容量 | 推荐的交换空间 | 启用休眠时的推荐交换空间 |
| :--- | :--- | :--- |
| 1GB | 1GB | 2GB |
| 2GB | 1GB | 3GB |
| 3GB | 2GB | 5GB |
| 4GB | 2GB | 6GB |
| 5GB | 2GB | 7GB |
| 6GB | 2GB | 8GB |
| 8GB | 3GB | 11GB |
| 12GB | 3GB | 15GB |
| 16GB | 4GB | 32GB |
| 24GB | 5GB | 48GB |

表 36-1

对于内存配置超过 24GB 的系统，请参考以下网页以获取交换空间指南：

[`help.ubuntu.com/community/SwapFaq`](https://help.ubuntu.com/community/SwapFaq%20)

当系统进入休眠时，当前的系统状态会被写入硬盘，主机将关闭。当机器随后开机时，系统状态将从硬盘恢复。这与挂起（suspension）不同，在挂起状态下系统状态存储在 RAM 中。机器进入睡眠状态，系统 RAM 保持供电而其他设备关闭。

## 36.3 识别当前交换空间的使用情况

可以使用多种方法识别 Ubuntu 系统当前使用的交换空间。一种方法是输出 `/proc/swaps` 文件：

```bash
cat /proc/swaps
```

文件名 类型 大小 使用 优先级
/dev/dm-1 分区 4169724 41484 -2

或者，可以使用 `swapon` 命令：

```bash
swapon
```

名称 类型 大小 使用 优先级
/dev/dm-1 分区 4G 40.5M -2

若要查看相对于总可用 RAM 的交换空间大小，可以使用 `free` 命令：

```bash
free
      total used free shared buff/cache available
Mem: 4035436 1428276 2224596 21968 382564 2360172
Swap: 4169724 41484 4128240
```

## 36.4 为 Ubuntu 系统添加交换文件

可以通过创建一个文件并将其分配为交换空间来为系统添加额外的交换空间。首先使用 `dd` 命令创建交换文件。可以通过调整 `count=` 变量来更改文件的大小。例如，以下命令行创建了一个 2.0 GB 的文件：

```bash
dd if=/dev/zero of=/newswap bs=1024 count=2000000
```

2000000+0 records in
2000000+0 records out
2048000000 bytes (2.0 GB, 1.9 GiB) copied, 3.62697 s, 565 MB/s

在将文件转换为交换文件之前，务必确保该文件设置了安全的权限：

```bash
chmod 0600 /newswap
```

一旦创建了合适的文件，就需要使用 `mkswap` 命令将其转换为交换文件：

```bash
mkswap /newswap
```

设置交换空间版本 1, 大小 = 1.9 GiB (2047995904 bytes)
no label, UUID=4ffc238d-7fde-4367-bd98-c5c46407e535

创建并配置交换文件后，可以使用 `swapon` 实用程序将其实时添加到系统中：

```bash
swapon /newswap
```

再次运行 `swapon` 现在应该会报告新文件正被用作交换：

```bash
swapon
```

名称 类型 大小 使用 优先级
/dev/dm-1 分区 4G 0B -2
/newswap 文件 1.9G 0B -3
```

可以使用 `swapoff` 实用程序动态移除交换空间，如下：

```bash
swapoff /newswap
```

最后，修改 `/etc/fstab` 文件，通过添加以下行在系统启动时自动添加新的交换空间：

`/newswap swap swap defaults 0 0`

## 36.5 将分区作为交换

作为指定文件为交换空间的替代方案，也可以将整个磁盘分区指定为交换。实现此目的步骤与添加文件大相同。

```bash
mkswap /dev/db1
```

一旦分区格式化完成，可以使用 `swapon` 激活它：

```bash
swapon /dev/db1
```

要移除交换分区，请使用 `swapoff`：

```bash
swapoff /dev/db1
```

最后，将条目添加到 `/etc/fstab` 以确保持久性：

`/dev/db1` swap `swap` `defaults` 0 0`



上述输出表示卷组（volume group）内没有可用空间。然而，假设我们需要为系统的交换分区（swap）添加 8 GB 空间。显然，这需要向卷组添加更多空间。为了本示例，我们假设有一个大小为 8 GB 且表示为 `/dev/sdb` 的磁盘可添加到卷组。第一步是将此分区转换为物理卷（physical volume）：

```
# pvcreate /dev/sdb
```
物理卷 `/dev/sdb` 已成功创建。

如果创建失败并显示类似“Device `/dev/sdb` excluded by a filter”（设备被过滤器排除）的消息，则可能需要在创建物理卷之前擦除磁盘：

```
# wipefs -a /dev/sdb
```

```/dev/sdb: 8 bytes were erased at offset 0x00000200 (gpt): 45 46 49 20 50 41 52 54
/dev/sdb: 8 bytes were erased at offset 0x1fffffe00 (gpt): 45 46 49 20 50 41 52 54
/dev/sdb: 2 bytes were erased at offset 0x000001fe (PMBR): 55 aa
/dev/sdb: calling ioctl to re-read partition table: Success
```

接下来，需要扩展卷组以使用此额外的物理卷：

```
# vgextend vgubuntu /dev/sdb
```
卷组 "vgubuntu" 已成功扩展

此时，`vgs` 命令应该报告卷组已添加了 10 GB 的空间：

```
# vgs
  VG #PV #LV #SN Attr VSize VFree
  vgubuntu 2 2 0 wz--n- 83.74g <10.00g
```

既然卷组中已经有了可用空间，就可以扩展交换逻辑卷（swap logical volume）以利用该空间。首先，使用 `swapoff` 工具关闭交换：

```
# swapoff /dev/vgubuntu/swap_1
```

接下来，扩展逻辑卷以使用新空间：

```
# lvextend -L+9.7GB /dev/vgubuntu/swap_1
```
Rounding size to boundary between physical extents: 9.70 GiB.
Size of logical volume `vgubuntu/swap_1` changed from 980.00 MiB (245 extents) to 10.66 GiB (2729 extents).
Logical volume `vgubuntu/swap_1` successfully resized.

在逻辑卷上重新创建交换：

```
# mkswap /dev/vgubuntu/swap_1
```

```
mkswap: /dev/vgubuntu/swap_1: warning: wiping old swap signature.
Setting up swapspace version 1, size = 10.7 GiB (11446251520 bytes)
no label, UUID=447fb9e5-5473-4f2c-96f8-839b1457d3ed
```

接下来，重新开启交换：

```
# swapon /dev/vgubuntu/swap_1
```

最后，使用 `swapon` 命令验证系统已添加的交换空间：

```
# swapon
```

```
NAME TYPE SIZE USED PRIO
/dev/dm-1 partition 10.7G 0B -2
```

## 36. 总结

交换空间是处理内存资源受限情况时几乎任何操作系统的至关重要的组件。通过将内存区域交换到磁盘，系统能够继续运行并满足运行在其上的进程和应用程序的需求。

Ubuntu 提供了一套指南，根据系统安装的 RAM 数量建议分配的磁盘交换空间大小。在这些建议被证明不足的情况下，可以为系统添加额外的交换空间，通常不需要重启。正如本章概述，交换空间可以通过文件、磁盘或磁盘分区的形式添加，也可以通过扩展已配置为交换空间的现有逻辑卷来添加。

## 37. Ubuntu 系统和进程监控

运行和管理 Ubuntu 系统的一个重要部分涉及从内存、交换、存储和处理器使用方面监控系统的整体状况。这包括如何检查和管理在后台运行的系统进程和用户进程。本章将概述用于监控 Ubuntu 系统资源和进程的一些工具和实用程序。

### 37.1 管理进程

即使 Ubuntu 系统看起来处于空闲状态，许多系统进程也会在后台静静运行，以保持操作系统的功能。每当你执行命令或启动应用程序时，都会启动用户进程，它们将一直运行到相关任务完成。

要获取当前在单个终端或命令行提示符会话中运行的活动用户进程列表，如下所示使用 `ps` 命令：

```
$ ps
  PID TTY TIME CMD
10395 pts/1 00:00:00 bash
13218 pts/1 00:00:00 ps
```

`ps` 命令的输出显示，当前终端窗口或命令行提示符会话中当前有两个用户进程运行，即执行命令的 bash shell。

*(注：由于原文文本中存在大量重复的 `ps` 描述，此处已根据指令翻译并保留了核心逻辑。)*



要更改列出的进程（例如列出所有进程或仅列出您自己的进程），请使用图 37-3 所示的菜单：

![](img/ubuntu_20.04_system_monitor_menu.jpg)

图 37-3

要过滤进程列表，请点击标题栏中的搜索按钮并在搜索字段中输入进程名称：

![](img/ubuntu_20.04_system_monitor_search.jpg)

图 37-4

要显示特定进程的附加信息，请从列表中选择该进程并点击对话框右下角的按钮（在图 37-5 中标记为 A）：

![](img/ubuntu_20.04_system_monitor_details.jpg)

图 37-5

点击该按钮后，将出现一个与上方标记为 B 类似的对话框。要终止进程，请从列表中选择该进程并点击“结束进程”（End Process）按钮 (C)。

要监控 CPU、内存、交换分区和网络使用，只需点击标题栏中的“资源”（Resources）按钮，即可显示图 37-6 所示的屏幕：

![](img/ubuntu_20.04_system_monitor_resources.jpg)

图 37-6

同样，通过选择“文件系统”（File Systems）工具栏按钮，可以查看系统存储空间摘要：

![](img/ubuntu_20.04_system_monitor_filesystems.jpg)

图 37-7

## 37.2 使用 htop 进行实时系统监控

如“Ubuntu Cockpit Web 界面概述”章节所述，可以使用 Cockpit Web 界面执行一些基础系统监控。前一节还解释了如何使用 GNOME 系统监视工具来监控进程和系统资源。在本章中，我们还探索了如何使用 `ps` 命令提供 Ubuntu 系统上正在运行进程的快照视图。然而，`ps` 命令无法提供系统进程和资源使用的实时视图。要从命令行提示符实时监控系统资源和进程，`htop` 命令是一个理想工具。尽管它通常没有默认安装，但可以通过以下方式安装：

```
apt install htop
```

安装完成后，按如下方式启动 `htop`：

```bash
htop
```

运行时，`htop` 将按系统资源使用情况列出系统上运行的进程（资源需求最大的进程位于顶部）。屏幕上半部分显示了一个图表，显示内存和交换分区的使用信息，以及所有 CPU 核心的数据。所有这些输出都会不断更新，允许对系统进行实时监控：

![](img/ubuntu_18.04_htop.jpg)

图 37-8

要将显示的信息限制为属于特定用户的进程，可以使用 `-u` 选项后用户名启动 `htop`：

```bash
htop -u john
```

要查看 `htop` 可用功能的完整列表，请按键盘 F1 键或参考 man 页：

```bash
man htop
```

## 37.3 命令行磁盘和交换空间监控

当然，磁盘空间既可以在 Cockpit 内部监控，也可以使用 GNOME 系统监视器监控。然而，要从命令行识别磁盘使用情况，`df` 命令提供了实用的概述：

```bash
df -h
```

Filesystem Size Used Avail Use% Mounted on
udev 1.8G 0 1.8G 0% /dev
tmpfs 374M 1.7M 372M 1% /run
/dev/sda5 92G 7.2G 80G 9% /
tmpfs 1.9G 0 1.9G 0% /dev/shm
tmpfs 5.0M 4.0K 5.0M 1% /run/lock
tmpfs 1.9G 0 1.9G 0% /sys/fs/cgroup
```

在上述输出中，根文件系统 (`/`) 当前仅使用 7.2GB 空间，留下了 80GB 可用空间。

要查看当前的交换分区和内存使用情况，运行 `free` 命令：

```bash
free
```

```
              total used free shared buff/cache available
Mem: 3823720 879916 1561108 226220 1382696 2476300
```

要持续监控内存和交换分区，使用带有 `-s` 选项的 `free` 命令，指定每次更新之间的秒数（请注意，`htop` 工具提供了更好的实时查看此类数据的方法）：

```bash
free -s 1
```

```
Mem: 3823720 879472 1561532 226220 1382716 2476744
Swap: 2097148 0 2097148
```

要从命令行监控磁盘 I/O，可以考虑使用 `iotop`，它可以通过以下方式安装：

```bash
apt install iotop
```

安装并运行（使用 root 权限运行 iotop）后，该工具将按进程显示实时磁盘 I/O 列表：

![](img/ubuntu_20.04_htop.jpg)

图 37-9

## 37.4 总结





# Shell
- 命令行编辑 [78]
- 环境变量 [82]
- 文件名缩写 [80]
- 历史 [79]
- I/O 重定向 [80]
- 路径补全 [80]
- 模式匹配 [80]
- 管道 [81]
- shell 脚本 [83]

# Systemd
- basic.target [92]

# 启动菜单
- 编辑 [49]

# Bourne shell [77]

# 容器
- buildah [253]

# C
- CA [266]
- canonical-livepatch [106]
- Canonical Ltd [7], [8]
- cat [80]
- 证书授权 (CA) [266]
- 更改 root [251]
- chmod [84]
- chroot [251]
- CNI [254]

# Cockpit
- 访问 [68]
- 账户管理 [71]
- 添加磁盘 [283]
- 应用程序 [72]
- 创建虚拟机 [215]
- 仪表板 [74]
- 启用 [68]
- 扩展 [67], [72]
- 安装 [68]
- 日志 [70]
- 多台服务器 [74]
- 网络 [71]
- NFS 管理 [192]
- 概览 [67]
- 端口 [68]
- 服务 [71]
- 存储 [70]
- 系统 [69]
- systemd 单元 [96]
- 终端访问 [73]
- 用户管理 [87]
- 虚拟机 [72]
- 虚拟机模块 [215]

# 网络管理
- 连接配置 [122]

# 容器
- containerd [251]
- 容器网络接口 (CNI) [254]
- 容器运行时 [251]
- 容器 [251]
- buildah [253]
- 更改 root [251]
- chroot [251]
- CNI [254]
- cni0 [254]
- containerd [251]
- 容器运行时 [251]
- CRI-O [251]
- Docker [251]
- 内核共享 [251]
- lxd [251]
- 网络 [254]
- 概览 [251]
- podman [253]
- 拉取镜像 [255]
- runc [253]
- 运行中的镜像 [257]
- 保存为镜像 [259]
- 范围 [253]
- CRI-O [251]
- C shell [77]

# D
- 守护进程 [91]
- 深色模式 [62]
- dd [12], [294]
- Debian [8]
- default.target 文件 [94]
- df 命令 [304]

# 磁盘
- 添加 [279]
- 检测 [279]
- 磁盘 I/O
- 监控 [305]

# 磁盘分区
- 格式化 [48]

# 磁盘使用
- df 命令 [304]
- diskutil [12]
- dmesg [11]

# DNS MX 记录 [276]
# Docker [251]
- 双系统启动 [45]

# E
- 邮件服务器 [271]
- 配置 [272]
- MX 记录 [276]

# 邮件系统
- 概览 [271]
- env [82]
- 环境变量 [82]
- 错误列表 [5]
- 导出 [82]

# F
- fdisk [45], [280], [290]
- Fedora Media Writer [13]

# 文件系统
- 创建 [281]
- 挂载 [282]
- findmnt [12]

# 防火墙
- gufw [137]
- ufw [137]

# 防火墙
- 邮件设置 [273]
- 概览 [147]
- Web 服务器设置 [262]
- firewall-cmd [150]
- NFS 设置 [190]
- Samba 设置 [196]
- firewall-config [154]

# firewalld
- 默认区域 [150]
- 显示区域信息 [150]
- firewall-cmd [150]
- firewall-config [154]
- ICMP 规则 [153]
- 接口 [147], [149]
- 列出服务 [151]



# 概述
- 概述
- 永久性设置
- 端口转发
- 端口规则
- 端口
- 重载
- 运行时设置
- 服务
- 状态
- 区域创建
- 区域/接口分配
- 区域
- 区域服务
- 释放
- free 命令
- 自由软件基金会
- fsck
- 全虚拟化

# G
- GDM
- GNOME
- 深色模式
- GNOME 3
- GNOME 桌面
- 安装
- GNOME 桌面
- 安装
- 安装
- 启动
- GNOME 显示管理器
- gnome-system-monitor
- GNU/Linux
- GNU 项目
- Google Cloud
- graphical.target
- groupdel
- 组
- 列出成员
- 移除
- 客户机虚拟化
- gufw
- 添加简单规则
- 高级规则
- 允许
- 拒绝
- 启用
- 安装
- 限制
- 预配置规则
- 配置文件
- 拒绝
- 运行

# H
- 硬件虚拟化
- 惠普
- 休眠
- 历史记录
- HOME
- 托管型虚拟机监控程序
- HP-UX
- htop
- 安装
- 用户进程
- httpd-le-ssl.conf
- httpd.service
- HTTPS
- 超调用
- 虚拟机管理器虚拟化
- Type-1
- Type-2

# I
- Ian Murdoch
- IBM
- id_rsa
- id_rsa.pub
- 安装
- 清理磁盘
- Intel VT
- 检查可用性
- iotop 命令
- 安装
- iptables
- ISO 镜像
- 写入 USB 驱动

# J
- 日志文件系统

# K
- 内核
- 内核共享
- kill 命令
- KILL 信号
- kvm
- 会话虚拟机
- 系统虚拟机
- KVM
- 在 Cockpit 中创建虚拟机
- 硬件要求
- 安装
- kvm_amd
- kvm_intel
- libvirtd
- 网络桥接接口
- 概述
- 验证
- virsh
- virt-manager
- virt-viewer
- kvm_amd
- kvm_intel

# L
- Landscape
- libvirtd
- Linus Torvalds
- Linux 容器。参见 容器
- Livepatch
- 启用
- 获取令牌
- 状态
- 逻辑区
- 逻辑卷
- 扩展
- 获取信息
- 管理
- `ls`




`lvdisplay` 289, 295

`lvextend` 292

`LVM` 287

`lxd` 251

## M

macOS

将 ISO 写入 USB 驱动器 12

邮件传输代理 (MDA) 272

邮件传输代理 (MTA) 271

邮件用户代理 (MUA) 271

`main.cf` 文件 274

`man` 78

Mark Shuttleworth 7, 8

Martin Hellman 157

MDA 272

内存

free 304

裸机 Hyper 管理器 207

MINIX 7

`mkfs.xfs` 48

`mkswap` 294, 295

`mount` 288

MTA 271

MUA 271

`multi-user.target` 92

MX 记录 276

## N

NAT 209

原生 Hyper 管理器 207

NetBIOS 名称服务 200

网络地址转换 209

网络桥接接口 233

网络文件系统 (NFS) 189

网络安装程序 25

下载镜像 25

执行安装 26

软件集合 30

`NetworkManager` 117

检查状态 118

连接配置 122

连接 119

设备 119

设备状态 118

启用 118

安装 118

管理连接 121

修改连接 121

`nmcli` 117

`nm-connection-editor` 117

`nmtui` 117

权限 126

`NFS` 189

Cockpit 管理 192

导出文件系统 190

防火墙设置 189

挂载文件系统 191

启动服务 189

卸载文件系统 191

`MB` 200

`nmcli` 117, 237

基础命令 118

连接权限 126

连接配置 122

交互式编辑 125

管理连接 121

网络桥接创建 239

权限 126

显示连接 121

Wi-Fi 扫描 121

`nm-connection-editor` 117, 242

网络桥接接口 242

`nmtui` 117

`NTFS` 46

## P

半虚拟化 207

分区 48

合作伙伴库 100

`PATH` 82

物理范围 288

物理卷 287

创建 291

`podman` 253

`attach` 258

`exec` 258

列出镜像 256

`pause` 259

`ps -a` 258

`rm` 259

`start` 259

`unpause` 259

端口转发 153

postfix

配置 272, 274

安装 273

日志文件 276

`main.cf` 文件 274

SMTP 继继服务器 277

启动 276

测试 277

`Postfix` 271

`poweroff.target` 91

预启动执行环境 (PXE) 10

进程

在系统监控中 301

列出所有 300

列出活动状态 299

派生 301

系统 299

用户 299

`ps` 81

`ps command` 299

公钥加密 157

`PuTTY` 163

安全隧道 176

`PuTTYgen` 163, 164

`pvcreate` 291

`pvdisplay` 290

`pwd` 78

`PXE` 10

## Q

`QEMU/KVM` 213

## R

RealVNC 173, 179





- `reboot.target` 92
- Red Hat, Inc. 7
- Remmina 桌面客户端 171
- 远程桌面访问 169, 170, 179
    - 启用 170
    - 安全与不安全 169
- 软件库 99
    - 禁用 100
    - 主 99
    - 管理 100
    - 多重宇宙 100
    - 限制 99
    - 源列表 100
    - 宇宙 99
- `rescue.target` 91
- `resize2fs` 292
- RFC 3339 114
- Richard Stallman 8
- root 用户 1
- `runc` 253
- `runlevel` 91

# S
- 安全图形模式 15
- Samba 195
    - 客户端 196
    - 配置共享资源 198
    - 创建用户 198
    - 防火墙设置 196
    - 安装 196
    - NetBIOS 名称服务 200
    - NMB 200
    - `samba-client` 202
    - `smb://` 203
    - `smbclient` 200
    - `smb.conf` 文件 197
    - 测试 `smb.conf` 文件 199
    - 工作组 197
    - `samba-client` 202
    - Samba 客户端 196
- SATA 控制器 279
- 安全传输层层 (SSL) 265
    - 安全网站
        - 配置 265
- SELinux
    - `smbpasswd` 198
- 服务器消息块 195
- 服务 91
    - 禁用 96
    - 启用 95
    - 掩码 96
    - 启动 95
    - 停止 95
    - `sh` 84
    - 历史 79
    - 概述 77
    - 脚本 83
    - 容器作用域 253, 255
    - 获取镜像 255
    - `smb://` 203
    - SMB 195
    - `smbclient` 200
    - `smb.conf` 199
    - `smb.conf` 文件 197
    - 全局区域 197
    - 测试 199
    - `smbpasswd` 198
- SMTP 272
    - SMTP 中继 272
    - SMTP 中继服务器 277
    - 配置 277
- snap
    - 频道 112
    - 命令 110
    - 禁用 115
    - 启用 115
    - 查找 110
    - 信息 110, 112
    - 安装 111
    - 列表 111
    - 日志 115
    - 概述 109
    - 软件包 109
    - 刷新 113
    - 刷新锁定 113
    - 流量流量 113
    - 刷新保留 113
    - 刷新定时器 113
    - 移除 111
    - 服务 115
    - 设置系统 113
    - 启动 115
    - 停止 115
    - 切换 112
- `sockets.target` 92
- 软件集合
    - 安装 31
    - Solaris 7
    - `sources.list` 文件 100
    - 生成 301
- SSH 157
    - SSH 认证 158
        - 来自 Linux 158
        - 来自 macOS 158
        - 来自 Windows 161
    - Google 云 165
    - 多多个密钥 160
    - PuTTY 163
    - PuTTYgen 163, 164
    - `ssh_config` 文件 160
    - `ssh-copy-id` 159
    - `ssh-keygen` 158
    - `ssh_config` 文件 160
    - `ssh-copy-id` 159
    - `sshd.service` 160
    - `ssh-keygen` 158
- SSL 265
    - SSL 证书 266
- `startx` 179, 181
- `stderr` 81
- `stdin` 80
- `stdout` 80
- 存储设备
    - 识别 11





# 命令
- `su - command` [1]
- `sudo` [2]
- SunOS [7]
- 超用户 [1]
- `swapoff` [295], [297]
- `swapon` [294], [298]

## 交换空间
- 添加分区 [295]
- 添加交换文件 [294]
- 添加到卷组 [297]
- 当前用量 [294]
- 扩展逻辑交换卷 [295]
- 释放 [304]
- 推荐 [293]

## systemd
- `systemctl` [92], [93]
- 默认目标 [91]
- 目标 [91]
-  [91]

### systemd 目标
- `basic.target` [92]
- 动态更改 [94]
- 获取默认 [93]
- `graphical.target` [92]
- 列出依赖项 [92]
- `multi-user.target` [92]
- `poweroff.target` [91]
- `reboot.target` [92]
- `rescue.target` [91]
- 设置默认 [93]
- `sockets.target` [92]

### systemd 单元
- 配置文件 [94]
- 禁用 [95]
- 启用 [95]
- 锁定 [95]
- 状态 [93]
- 类型 [94]
- systemd 单元 [91]

## 系统监器
- 系统监器 [301]
- 系统监控 [299]
- 磁盘 I/O [305]
- 空闲内存 [304]
- 空闲交换空间 [304]
- `gnome-system-monitor` [301]
- `htop` [303]
- `iotop` [305]
- 系统进程 [299]

## T
- 目标 [91]
- `tasksel`, [31]
- `TERM` 信号 [300]
- TigerVNC [179]
- TightVNC [176], [179]

- `TLS` (传输层安全) [266]
- 类型 1 虚拟化 [206]
- 类型 2 虚拟化 [206]

## Ubuntu
- 历史 [8]
- 含义 [8]
- `ufw` [137], [143]
- 命令行选项 [143]
- 禁用 [143]
- 启用 [143]
- 日志 [145]
- 重新加载 [145]
- 重置 [145]
- 状态 [143]
- `umount` [12]
- 简单防火墙 [137]
- UNIX [7]
- 起源 [7]
- `update-manager` [100]
- 更新 [103]
- 自动 [104]

## USB 驱动器
- 设备名称 [11]
- `useradd` [85]
- `userdel` [86]
- 用户进程 [299]

## 用户
- 添加和删除 [86]
- 用户与组 [85]

## V
- `VcXsrv` [185]
- `vgdisplay` [288]
- `vgextend` [291]
- `Vino` [170]
- 禁用加密 [174]
- 安装 [170]

### virsh
- 交互模式 [247]
- 重启虚拟机 [250]
- 恢复虚拟机 [249]
- 恢复恢复虚拟机 [249]
- 保存虚拟机 [249]
- `setmem` [250]
- shell [247]
- 挂起虚拟机 [249]
- `virt-install` [215]
- `virt-manager` [212], [213], [222]
- 创建虚拟机 [222]
- 会话连接 [222]
- 启动虚拟机 [226]

## 虚拟化
- 虚拟化 [205]
- AMD-V [208]
- 全虚拟化 [208]
- 客户 OS 虚拟化 [205]
- 硬件虚拟化 [208]
- 宿主机虚拟机程序 [206]
- 超调用 [207]
- 虚拟机程序虚拟化 [206]
- Intel VT [208]
- KVM [211]
- 裸金属虚拟机程序 [207]
- 原生虚拟机程序 [207]
- 半虚拟化 [207]

## VNC
- `virt-viewer` [218]
- 安装 [218]
- 远程 SSH 连接 [219]
- 会话虚拟机 [219]





# Ubuntu
- 连接到服务器 [181]
- 端口 [180]
- 安全访问 [175]
- 服务器安装 [179]
- `vncpasswd` [180]
- `vncserver` [180]
- 终止会话 [181]
- 列出会话 [180]
- 卷组 [287]

# W
- `wc` [81]
- Web 服务器 [261]
- `which` [78]
- 惠特菲德·迪菲 (Whitfield Diffie) [157]

# Windows
- 将 ISO 写入 USB 驱动 [13]
- Windows 分区
- 文件系统访问 [40]
- 回收空间 [45]
- 卸载 [45]
- Windows PowerShell [161]
- Windows SMB [189]
- Windows 系统分区 [46]
- `wipefs` [291]

# X
- X11 转发 [183]
- 压缩 [184]
- 可信 [184]
- XFS 文件系统 [281]
- `xfs_growfs` [292]

# Z
- ZFS 文件系统 [18]

