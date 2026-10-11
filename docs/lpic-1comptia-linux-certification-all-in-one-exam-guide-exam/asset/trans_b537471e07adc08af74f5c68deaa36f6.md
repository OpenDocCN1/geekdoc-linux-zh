

## 110.3 使用加密保护数据
执行基本的 OpenSSH 2 客户端配置和使用（第 18 章，第 718 页）
了解 OpenSSH 2 服务器主机密钥的作用（第 18 章，第 716 页）
执行基本的 GnuPG 配置和使用（第 18 章，第 730 页）
理解 SSH 端口隧道（包括 X11 隧道）（第 18 章，第 721 页）

以下是所使用文件、术语和实用程序的简要列表：

- /etc/nologin（第 17 章，第 664 页）
- /etc/passwd（第 9 章，第 337 页；第 17 章，第 660 页）
- /etc/shadow（第 9 章，第 338 页；第 17 章，第 660 页）
- /etc/xinetd.d/*（第 17 章，第 691 页）
- /etc/xinetd.conf（第 17 章，第 689 页）
- /etc/inetd.d/*（第 17 章，第 692 页）
- /etc/inetd.conf（第 17 章，第 693 页）
- /etc/inittab（第 6 章，第 204 页）
- /etc/init.d/*（第 6 章，第 207 页）
- /etc/hosts.allow（第 17 章，第 692 页）
- /etc/hosts.deny（第 17 章，第 692 页）
- ssh（第 18 章，第 718 页）
- ssh-keygen（第 18 章，第 726 页）
- ssh-agent（第 18 章，第 728 页）
- ssh-add（第 18 章，第 728 页）
- ~/.ssh/id_rsa 和 id_rsa.pub（第 18 章，第 726 页）
- ~/.ssh/id_dsa 和 id_dsa.pub（第 18 章，第 726 页）
- /etc/ssh/ssh_host_rsa_key 和 ssh_host_dsa_key.pub（第 18 章，第 716 页）
- /etc/ssh/ssh_host_dsa_key 和 ssh_host_dsa_key.pub（第 18 章，第 716 页）
- ~/.ssh/authorized_keys（第 18 章，第 726 页）
- /etc/ssh/known_hosts（第 18 章，第 716 页）
- gpg（第 18 章，第 731 页）
- ~/.gnupg/*（第 18 章，第 733 页）

# 关于光盘

随书附带的光盘包含完整的 MasterExam 模拟考试软件、作者的视频培训、CompTIA 的 LX0-101 和 LX0-102 考试目标列表，以及本书的 PDF 副本。该软件易于在任何 Windows 2000/XP/Vista/Windows 7 计算机上安装，必须安装软件才能访问 MasterExam 功能。但是，您可以直接通过光盘浏览本书的 PDF 副本和视频培训，无需安装。要注册免费的 MasterExam，只需点击主启动页面上的 Bonus MasterExam 链接，并按照说明进行免费在线注册。

## 系统要求

软件需要 Windows 2000 或更高版本、Internet Explorer 6.0 或更高版本，以及完整安装所需的 20MB 硬盘空间。本书的 PDF 副本需要 Adobe Reader。

## 在 Linux 中访问 MasterExam 模拟测试

MasterExam 模拟测试以 PDF 格式提供在光盘中，供不愿安装 MasterExam 软件的 Linux 用户使用。Linux 上有很多可用的 PDF 阅读器，包括以下：

- **Adobe Reader** Adobe Reader 提供最佳的 PDF 文件支持。您可以从 http://get.adobe.com/reader/ 下载副本。选择“您是否有不同的语言或操作系统？”；然后在步骤 1 下拉列表中选择 Linux，在步骤 2 下拉列表中选择您的*语言*。从步骤 3 下拉列表中选择适合您发行版的软件包（.rpm、.deb、.tar.gz 或 .tar.bz2）。如果您选择了软件包，请使用您发行版相应的包管理实用程序进行安装，例如 rpm、yum 或 dpkg。如果您选择了源码包文件，请使用本书第 8 章中的步骤从源码安装 Adobe Reader。
- **Xpdf** Xpdf 是一个极简的 PDF 阅读器应用程序，在某些发行版中默认安装。如果您想使用此 PDF 阅读器，请使用适当的包管理实用程序（例如 rpm、yum 或 dpkg）从您的发行版介质或发行版网络仓库安装 xpdf-tools 软件包。
- **Evince** Evince 是一个基于 GNOME 的 PDF 阅读器应用程序。与 Xpdf 一样，Evince 在许多 Linux 发行版中通常默认安装。如果您想使用此 PDF 阅读器，请使用适当的包管理实用程序（例如 rpm、yum 或 dpkg）从您的发行版介质或发行版网络仓库安装 evince 软件包及其所有依赖项。
- **KPDF** KPDF 是一个功能更齐全的 PDF 阅读器应用程序，为 KDE 桌面环境开发。如果您想使用此 PDF 阅读器，请使用适当的包管理实用程序（例如 rpm、yum 或 dpkg）从您的发行版介质或发行版网络仓库安装 kdegraphics 软件包及其所有依赖项。

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_813_0.png)

> **注意** 请参阅本书第 8 章，查看使用 rpm、yum 和 dpkg 命令的具体说明。

您可以使用 Linux 访问光盘 `/Programs/eBook/PracticeExams` 目录中的所有 PDF 格式的模拟测试。

## 安装和运行 MasterExam

如果您的计算机光驱设置为自动运行，插入光盘时光盘将自动启动。从打开的屏幕，您可以通过点击 MasterExam 链接来安装 MasterExam。这将开始安装过程并创建一个名为 LearnKey 的程序组。要运行 MasterExam，请使用 开始 | 所有程序 | LearnKey | MasterExam。如果自动运行功能未启动您的光盘，请浏览到光盘并点击 LaunchTraining.exe 图标。

## MasterExam

MasterExam 为您提供实际考试的模拟。题目数量、题目类型和允许时间旨在准确反映考试环境。您可以选择参加开卷考试（包括提示、参考答案和答案）、闭卷考试，或限时 MasterExam 模拟。

当您启动 MasterExam 时，屏幕右下角会出现一个数字时钟显示。时钟可以持续倒数至零，除非您选择在时间用尽之前结束考试。

## 视频培训片段

MP4 视频片段以音频/视频格式详细展示了关键认证目标，内容直接来自本书作者。这些片段逐步指导您完成各种系统管理任务。您可以通过点击主启动页面上的 Videos 链接，直接从视频目录中访问这些片段。

## 本书的 PDF 副本

考试指南的全部内容均以 PDF 形式提供。光盘中包含了 Adobe Acrobat Reader。

## 帮助

主页左下角的帮助按钮提供了一个帮助文件。MasterExam 中也提供了单独的帮助功能。

## 删除安装

MasterExam 安装在您的硬盘上。为了获得最佳的程序移除效果，请使用 开始 | 所有程序 | LearnKey | Uninstall 选项来移除 MasterExam。

## 技术支持

如需咨询关于本书 PDF 副本内容、MasterExam 或视频的问题，请访问 www.mhprofessional.com 或发送邮件至 customer.service@mcgraw-hill.com。对于美国 50 个州以外的客户，请发送邮件至：international_cs@mcgraw-hill.com。

## LearnKey 技术支持

如需咨询软件的技术问题（安装、操作、删除安装），请访问 www.learnkey.com，发送邮件至 techsupport@learnkey.com，或拨打免费电话 1-800-482-8244。

# 索引

## 符号
- / (forward slash), 在 man 页中搜索信息，38
- | (pipes). 参见 pipes
- & (ampersand), 用于在后台运行程序，492
- $ (dollar sign) 字符，用于变量名的语法，45
- * (asterisk), 搜索和匹配的通配符，102, 503
- ?/search_term 命令，vi 文本编辑器，82

## 数字
- 0 命令，vi 文本编辑器，81
- 1 命令，vi 文本编辑器，81
- 3DES (Triple Data Encryption Standard)，711, 731

## A
- a 命令，vi 文本编辑器，81
- A 命令，vi 文本编辑器，81
- absolute path, 使用 cd 命令时，107
- access control. 另参见 user access
    - in account management, 331–332
    - controlling access to operating system, 653–655
    - Exam LX0-101, 759
- accessibility options
    - Braille devices, 260–261
    - Exam LX0-102, 762
    - exercise working with, 262–263
    - high-contrast, large text themes, 261–262
    - keyboard options, 254–256
    - mouse options, 256–257
    - overview of, 253
    - screen magnifiers, 257–260
    - screen readers, 257
- AccessX, 用于键盘无障碍功能，254
- account management
    - access control and, 331–332
    - Exam LX0-102, 762
    - group accounts. 参见 groups
    - overview of, 329–331
    - Q&A, 353–356
    - review, 350–353
    - user accounts. 参见 user accounts
- active termination, of SCSI devices, 438
- Adobe Reader, as PDF viewer, 769
- Advanced Encryption Standard (AES)
    - GPG supporting, 731
    - types of symmetric encryption, 712
- Advanced Package Tool, utilities. 参见 apt (Advanced Package Tool) utilities
- AES (Advanced Encryption Standard)
    - GPG supporting, 731
    - types of symmetric encryption, 712
- alias name="command", 50
- aliases
    - configuring for MTA program, 630–632
    - using, 50–51
    - using with commands, 105
- ALTER TABLE 命令，SQL, 633
- anonymous-user account, MySQL, 634
- application layer, directory for, 99
- Application layer, of OSI Reference Model, 558
- application platform, functions of operating systems, 2
- apropos utility, searching man pages with, 38
- apt (Advanced Package Tool) utilities
    - commands, 308
    - installing packages with apt-get, 310–312
    - managing packages with aptitude, 312–313
    - viewing package information with apt-cache, 308–309
- aptitude, managing packages with, 312–313
- architecture
    - CPUs, 138, 285
    - Exam LX0-102, 751
- archive files
    - creating with cpio utility, 391–392
    - creating with tar utility, 389–390
    - overview of, 299
- ARP, mapping IP addresses to MAC addresses, 562
- asymmetric encryption
    - GPG and, 730–731
    - OpenSSH and, 716
    - overview of, 712–715
- ATA (AT Attachment) drives
    - PATA drives, 433
    - SATA drives, 435–436
    - speeds of, 435
- atd (at daemon)
    - Exam LX0-102, 763
    - scheduling processes, 498–501
    - starting, 496

