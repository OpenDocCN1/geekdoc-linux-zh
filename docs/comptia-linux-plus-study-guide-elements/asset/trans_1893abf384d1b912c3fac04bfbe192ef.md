
还有一些编号目标分布在多个章节中，因此当你注意到序列中的缺失或重复时，请不要惊慌。）在每一章的末尾，你会发现两个部分，可以帮助你为考试做准备：

**考试要点** 本节总结了章节中涵盖的重要信息。你应该能够执行各项任务或传达所请求的信息。

**复习题** 每章都以20道复习题结尾。你应该回答这些问题，并与题目后提供的答案进行核对。如果你无法正确回答至少80%的这些问题，请回去复习该章节，或者至少复习那些似乎给你造成困难的部分。

![](img/a78bc63f22351f522ba5ec1fa0c060d2_24_0.png)

> 本教程中的复习题、评估测试和其他测试元素*并非*源自 CompTIA Linux+ 考试题目，因此不要死记硬背这些问题的答案，并认为这样做就能让你通过 Linux+ 考试。你应该学习书中正文描述的底层主题。这将让你能够回答本教程提供的问题*并且*通过考试。学习底层主题也是在工作中最有益的方法——这也是像 Linux+ 这样的认证考试的终极目标。

为了最大限度地利用本教程，你应该从头到尾阅读每一章，然后使用章节末尾的要素来检查你的记忆和理解。即使你已经熟悉某个主题，你也应该浏览该章节；Linux 足够复杂，完成任务往往有多种方法，因此即使你已经在某个领域很熟练，你仍可能学到新东西。

## 附赠 CD-ROM 内容

本教程附带一张 CD-ROM，其中包含若干附加内容。CD-ROM 上可用的项目包括：

**书籍内容的 PDF 文件** 整本教程均可作为完全可搜索的 PDF 文件获取，可以在大多数操作系统上阅读，包括 Linux 和 Windows。

**电子“卡片”** CD-ROM 包含 150 道“卡片”格式的问题（一个问题后跟一个正确答案）。你可以使用这些卡片来复习你对 Linux+ 考试目标的了解。

**示例测试** 本教程中的所有问题都出现在 CD-ROM 上——包括本介绍末尾的 30 题评估测试，以及由每章 20 道“复习题”组成的 12 个部分共计 240 道题。此外，还有两场 65 题的附加考试。

## 本教程中的排版惯例

本教程使用某些排版风格，以帮助你快速识别重要信息，并避免对诸如屏幕提示等词语含义产生混淆。特别是：

- *斜体文本*表示在章节中首次详细描述的关键术语。（斜体也用于强调。）
- 等宽字体表示配置文件的内容、文本模式 Linux shell 提示符下显示的消息、文件名、文本模式命令名称以及 Internet URL。
- *斜体等宽文本*表示变量——从一个系统或命令运行到另一个系统或命令有所不同的信息，例如客户机计算机的名称或进程 ID 号。
- **粗体等宽文本**是你应输入到计算机中的信息，通常是在 Linux shell 提示符下。此文本也可以*斜体化*，以表示你应该为你的系统替换适当的值。（当命令单独成行时，命令前是非粗体等宽的 $ 或 # 命令提示符。）

除了这些可以适用于单个单词或整个段落的文本惯例外，还有几种惯例用于突出显示文本片段。

![](img/a78bc63f22351f522ba5ec1fa0c060d2_25_0.png)

![](img/a78bc63f22351f522ba5ec1fa0c060d2_25_1.png)

![](img/a78bc63f22351f522ba5ec1fa0c060d2_25_2.png)

![](img/a78bc63f22351f522ba5ec1fa0c060d2_25_3.png)

## 实际应用场景

实际应用场景是一个侧边栏，提供特别基于现实世界的信息。此类文本可能基于我自身的经验，或者提供在阅读有关主题的基本事实时可能并不显而易见的实用信息。

## 示例

## 考试目标

在每个计算机行业的考试背后，你都可以肯定地发现考试目标——考试开发者希望你具备能力的广泛主题。Linux+ 考试的官方 CompTIA 目标列于此。（它们也印刷在涵盖它们的章节开头。）

> 考试目标可能会随时更改，且无需提前通知，完全由 CompTIA 自行决定。请访问 CompTIA 网站的 Linux+ 认证页面（http://www.comptia.org/certifications/listed/linux.aspx）获取最新的考试目标列表。

### 领域 1.0 安装与配置

- 1.1 比较和对比安装源（物理安装介质：CD-ROM、DVD；网络类型：HTTP、FTP、NFS）。
- 1.2 使用以下工具和实践实施分区方案和文件系统布局（LVM、RAID、fdisk、parted、mksfs）。
- 1.3 解释使用以下文件系统类型的目的（本地：EXT2、EXT3、Reiser、FAT、NTFS、VFAT、ISO9660。网络：NFS、SMBFS/CIFS）。
- 1.4 执行文件系统的常规挂载和卸载（mount、umount、/etc/fstab）。
- 1.5 解释为以下任何目录使用单独分区或卷的优势（/boot、/home、/tmp、/usr、/var、/opt）。
- 1.6 解释以下目录的用途（/、/bin、/dev、/etc、/mnt、/proc、/root、/sbin、/usr/bin、/usr/local、/usr/lib、/usr/lib64、/usr/share、/var/log）。
- 1.7 配置引导过程，包括以下内容（GRUB：/boot/grub/grub.conf、/boot/grub/menu.lst、grub-install、grub）。
- 1.8 执行以下包管理功能（安装、删除和更新程序：rpm [rpm -Uvh、rpm -qa、rpm -e、yum]、deb [dpkg -i、dpkg - r、apt-get、apt-cache search]、source [./configure、make、make install、make uninstall、tar、make clean、autoconf、make test、tar.gz、INSTALL、bzip、gzip]）；解决依赖项；添加和删除存储库；
- 1.9 在全局范围和用户级别配置配置文件和环境变量（PS1、PS2、PATH、EDITOR、TERM、PAGER、HOME、PRINTER）。
- 1.10 使用以下工具排查引导问题（内核选项、单用户模式 [包括恢复 root 用户]、Rescue——live CD、DVD 和 USB 键、dmesg）。
- 1.11 使用以下工具管理设备（lsub、lspci、lsmod、/sys、modprobe、/proc、/etc/modules.conf、/etc/modprobe.conf、硬件兼容性列表 [HCL]）。

### 领域 2.0 系统维护与操作

- 2.1 给定场景，使用以下基本 Linux 工具、技术和资源（目录导航：cd、ls、pushd、popd、pwd；文件命令：file、test、find、locate、slocate、which、whereis、ln、ls -F、mknod、touch、mkdir、mv、cp、rm、cd；文件类型 [硬链接、软链接、目录、设备文件、常规文件、命名管道]；使用 Vi 进行文件编辑；进程管理：ps、kill、top、istat、pstree、nice、renice、signals、PID、PPID；I/O 重定向：<、>、>=、>、|、；tee、xargs、STDIN、STDOUT、STDERR；特殊设备：/dev/null、/dev/random、/dev/zero、/dev/urandom；系统文档：Man 页面 [man、apropos、make whatis、whatis]、Info 页面、/usr/share/docs]；虚拟控制台；内核/架构信息：cat、/proc/version、uname、常见 sysctl 设置、/etc/sysctl.conf))。
- 2.2 使用 BASH 执行基本任务（脚本基础 [仅限：执行权限、#!/bin/bash、sh script]；Shell 特性：history、标签完成）。
- 2.3 给定场景，分析系统和应用程序日志以排查 Linux 系统问题（常见日志文件：/var/log/messages、/var/log/syslog、/var/log/mail.log、/var/log/secure、/var/log/lastlog；轮换的日志；搜索和解释日志文件：grep、tail -f、awk、sed）。
- 2.4 执行和管理备份和恢复操作（复制数据：rsync 和 ftp；归档和恢复命令：cpio、tar、dump、restore、dd；写入可移除介质：CD-RW、DVD-RW）。
- 2.5 解释 X11 的以下特性和概念（启动和停止 X11、X11 客户端和服务器之间的区别、窗口管理器和显示管理器 [KDM、GDM]、多桌面、X11 配置文件 [xorg.conf]、终端模拟器 [xterm、等等]）。
- 2.6 解释运行级别及其用途的区别（命令：init；运行级别：0 – 关机、1 – 单用户模式、2 – 带网络的单用户模式、3 – 网络多用户模式、4 – 用户可配置、5 – X11 多用户模式、6 – 重新启动）。

