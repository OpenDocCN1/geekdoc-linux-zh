
本章介绍了几种不同的 Linux 发行版（其中某些包含在本书附的 CD 和 DVD 中），你可以使用它们来尝试不同类型的 Linux 系统。它还告诉你使用哪些工具来各种定制或构建你自己的 live CD。

## 本章内容

- 探索可启动的 Linux
- 选择可启动的 Linux 发行版
- 启动救援发行版
- 启动多媒体发行版
- 启动微型桌面发行版
- 构建和定制可启动的 Linux

# 第五部分：选择和安装不同的 Linux 发行版

### 注意

我建议你使用书中包含并在第 21 章描述的 Puppy 发行版。它将通过描述 `KNOPPIX` 如何工作、如何使用不同的启动项启动它以及跨重启保存更改的方法，帮助你直观地查看可启动 Linux 系统。你也可以查看附录 A，获取书中附带 CD 和 DVD 可启动 Linux 发行版列表。■

### 可启动 Linux 发行版概览

通过使用可移除介质（CD、DVD 甚至 USB 闪存器）并结合开源软件，可启动 Linux 让你能够完全跳过硬盘（如果你愿意的话），并在几乎任何没有硬盘的电脑上运行特殊的 Linux。

可启动 Linux 发行版可以为你提供一些惊人的机会。在可移除介质上，你可以携带：

- 你喜喜欢的操作系统
- 只要介质能容纳的所有你喜喜欢的应用程序
- 只要介质能容纳的所有音乐、视频、文档或其他数据
- 一套完全自定义的功能和配置设置

## 第 28 章：运行可启动的 Linux 发行版

换句话说，如果你愿意构建自己的自定义可启动发行版，可启动 Linux 发行版概念可以随你喜欢的方式进行扩展：你的可启动业务（微 CD）或 CD 可以携带你习惯的所有应用程序，因此你可以从任何一台高级 PC 上使用其中的一个。但它还可以存储你的演示文稿、邮件服务器设置、地址簿、喜欢的背景和屏幕保护程序、个人照片以及你任何其他数据。

大多数主要作为 live CD 创建的可启动 Linux 发行版都是基于通常安装到硬盘的成熟 Linux 发行版。例如，`KNOPPIX` 基于 Debian（即 Debian Linux）。`SLAX` 基于 Slackware。`SystemRescueCD` 基于 Gentoo。因此，例如你想选择一个可启动的 Linux 定定义为个人桌面或服务器，你可能会选择一个基于你熟悉的 Linux 系统的。

近年来，诸如 Fedora、Ubuntu、openSUSE 和 Gentoo 等 Linux 发行版已开始制作自己的 live CD 以展示它们的发行版。诸如 `live-creator` 等工具极大地简化了从 Fedora 仓库的包构建 live CD 的任务。

然而，如果你对你的 live CD 基于哪个发行版没有偏好，你可能仍然想选择一个可启动的 Linux，因为它包含一组专门的……

### 尝试可启动的 Linux

无论你选择书中附带的任何一个发行版，我都建议你访问以下网站：

- FreeCD List — freecd.com 列出了 300 多种发行版。Wikipedia List of Liveos — http://en.wikipedia.org/wiki/List_of_Live_distributions
- Linuxlinks.com 这里有一个微发行版列表：www.linuxlinks.com/Distributions/
- DistroWatch — DistroWatch 维护着发行版列表：http://distrowatch.com/dwres.php?resource=cd
- Knoppix Customizations — knppix Customizations 页面（www.knoix.net/wiki/Knoppix_Customizations）列出了约 100 个基于 knppix 的发行版

如果在运行任何发行版时遇到困难，尝试向启动提示符添加选项。由于许多发行版基于 `KNOPPIX`，请参考第 21 章描述的 `KNOPPIX` 选项（也称为代码代码），让你的 Linux 系统以你喜欢的方式启动。在 knoppix.net/wiki/Cheat_Codes 查看这些代码。

本书包含了几个可启动的发行版，你可以在附录 A 中找到它们。你可以通过关注网站链接获取感兴趣发行版的最新版本。

### 注意

许多可启动 Linux 发行版是由个人创建的，应被视为实验性的。质量差异很大，且控制不像红帽企业级 Linux 等商业系统那样严格。你可以通过以下操作来限制风险，例如将所有硬盘分区安装为只读（通常默认如此，但并非总是如此），记住此软件是在不带担保的情况下分发的。

## 第 28 章：运行可引导的 Linux 发行版

它们被称为 live spins（https://www.fedoraproject.org/wiki/CustomSpins）。使用 live CD 创建工具构建的特殊 live CD 包括游戏发行版、电子实验室版、开发者版和 Xfce 发行版。桌面上有一个安装图标。

- Gentoo CDs — Gentoo（www.gentoo.org/main/en/where.xml）提供了 live CD 和 DVD。这些介质的构建版本可在八种架构上运行。每张 CD 和 DVD 都包含一个安装程序。
- Mepis live CDs — Mepis 项目（www.mepis.org/mirrors）提供了 SimplyMEpis live CD，该系统也可用于安装桌面版 Mepis 系统。Mepis 的分支项目 Mepis AntiX 还提供了一种专为在低端电脑上良好运行而设计的 CD。
- SUSE live — 你可以使用来自 openSUSE 项目（software.opensuse.org）的 GNOME 和 KDE live CD 及 DVD，分别适用于 x86、x86-64 和 PowerPC 架构。这些介质还包含了将其内容安装到硬盘的工具。

当你使用 live CD 时，可以通过 Internet 安装额外的软件包以尝试其他功能。请记记，由于运行 live CD 所需的 RAM 比相同系统从硬盘运行时所需的内存更多，因此许多 Linux 发行版在您将其内容安装到硬盘后运行得会更好。

## 在 DVD 上

随书提供的 DVD 包含 Ubuntu、Fedora、Gentoo、AntiX、PCILinux 和 openSUSE live CD。关于这些 live CD 的信息请查看附录 A。

## 安全与救援引导

修复损坏的系统和诊断网络问题是可引导 Linux 最流行的用途之一。在某些时刻，你的硬盘可能无法访问；可引导的救援 CD 或 DVD 实际上可以拯救损坏或受感染的计算机。某些救援工具包被誉为完整的安全工具，提供了广泛的工具来监控 Linux 或 Windows 系统、扫描病毒、调试和法证分析。

如果网络中有 DHCP 服务器，大多数可引导的 Linux 系统都可以在你的网络上启动。如果没有，使用 `netconfig` 工具手动设置以太网卡。因此，当你的电脑启动并通过可引导的 Linux 连接到网络后，你就可以检查、修复、备份以及其他方式控制本地计算机以及网络上的其他计算机。

### 注意

某些 live CD 项目提到，其 live CD 所选的工具部分源自 Insecure.org 的“前 100 网络安全工具”列表（http://sectools.org）。该列表是根据 nmap-hackers 邮件列表上调查的 3,200 多份回复汇总而成的。

## 第五部分：选择和安装不同的 Linux 发行版

基于许多此类发行版包含的开源软件，以下是关于使用大多数 Linux 安全/救援 CD 的建议：

- **评估漏洞** — 用于评估计算机漏洞的工具包括允许共享 Windows SMB 文件夹的（`nbtscan`）、CGI 脚本（`nscript` 和 `screamingCobra`）、计算机端口（`nmap`）以及针对病毒的（`clamAV`）。你还可以检查是否使用 rootkit 替换了关键系统文件（`chkrootkit`），或者使用扫描调度（`warscan`）在大量机器上测试任何漏洞。
- **在 Windows 机器上运行法证** — 如果你认为 Windows 系统已被入侵，有很多工具可以用来发现并纠正问题。启动安全 CD（如 `KNOPPIX-STD`），你可以恢复 Internet Explorer Cookie（`galletta`）、将 Outlook Dbx 文件恢复为 mbox 格式（`readbs` 和 `derobe`）、检查系统完整性（`ftimes`）以及检查 Windows 回收箱（`rifuti`）。
- **恢复数据** — 如果 Windows或其他操作系统无法启动或受损，你可以从计算机中提取数据。你可以使用 `rsync`、`scp` 从网络复制文件，或备份到 CD 或磁带（`cpio`、`tar` 或其他）。你可以从磁盘镜像恢复文件（`foremost`）并恢复丢失的分区（`testdisk`）。
