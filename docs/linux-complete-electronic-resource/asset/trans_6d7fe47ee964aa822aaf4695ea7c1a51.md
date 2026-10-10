

## 第4章

### 安装 LINUX

本章描述了如何安装 Linux 软件。这是新用户开始使用 Linux 时应当阅读的第一份文档。它涵盖了硬件和软件要求、安装前需要采取的准备步骤，以及硬盘重新分区和启动 Linux 系统的具体细节。

本章转载自 1998 年 11 月 20 日版本的 Linux 安装 HOWTO（版本 4.15），作者为 Eric S. Raymond。

### 简介

本文档假设您已听说过并了解 Linux，现在希望将其运行起来。文档主要关注基于 Intel 的版本，这是最流行的版本，但其中的许多建议同样适用于 PowerPC、Sparc 和 Alpha 架构的机器。

### 其他信息来源

如果您是 Linux 的新手，有几处可以获取关于该系统基本信息来源。查找这些信息的最佳地点是位于 `http://MetaLab.unc.edu/LDP/linux.html` 的 Linux 文档项目（LDP）主页。您可以在 `http://MetaLab.unc.edu/LDP/HOWTO/Installation-HOWTO.html` 找到本章的最新版本。

您可能应该从浏览“通用 Linux 信息”下的资源开始：Linux INFO-SHEET（`http://MetaLab.unc.edu/LDP/HOWTO/INFO-SHEET.html`）和 Linux META-FAQ（`http://MetaLab.unc.edu/LDP/HOWTO/LINUX-FAQ.html`）。Linux 常见问题解答文档包含许多关于 Linux 的常见问题（以及答案！）——这是新用户必读的内容。

您可以在 USENET 新闻组 comp.os.linux.help 和 comp.os.linux.announce 上找到常见问题的帮助。

Linux 文档项目正在编写一套关于 Linux 的手册和书籍，所有这些都可以在网络上自由分发，并可在 LDP 主页上获取。

书籍《*Linux 安装与入门*》是一份完整的指南，涵盖了获取和安装 Linux 的方法，以及安装后如何使用该系统。书中包含了一份关于使用和运行系统的完整教程，以及比此处包含的更多信息。您可以从 LDP 主页（`http://MetaLab.unc.edu/LDP/`）浏览或下载副本。

最后，还有一份相当技术性的 x86 自举指南（`http://www.paranoia.com/~vax/boot.html`）。该文档侧重于 NetBSD 而非 Linux，但包含了关于多操作系统设置下磁盘配置和启动管理器的有用资料。

### 本文档的新版本

Linux 安装 HOWTO 的新版本将定期发布到 comp.os.linux.help、comp.os.linux.announce 和 news.answers 中。它们也将上传到各种 Linux WWW 和 FTP 站点，包括 LDP 主页。

您也可以在世界万维网 http://MetaLab.unc.edu/LDP/HOWTO/Installation-HOWTO.html 上查看本文档的最新版本。

### 反馈与更正

如果您对本文档有任何疑问或意见，请随时将邮件发送至 Eric S. Raymond 的 esr@thyrus.com。我欢迎任何建议或批评。如果您发现本文档有错误，请告知我，以便我在下一版中更正。谢谢。

请不要就安装过程中遇到的硬件问题如何解决给我发送邮件。请参阅《Linux 安装与入门》，联系您的供应商，或查阅 Linux 新闻组 comp.os.linux.setup。本 HOWTO 旨在作为常规安装的快速、无痛指南——关于硬件问题和诊断的独立 HOWTO 正在编写中。

## 最简单的选择：购买，而非构建

Linux 已经足够成熟，现在有一些系统集成商可以为您组装工作站，安装和配置 Linux，并在发货前进行严格的烤机测试以确保其稳定性。如果您比时间更富余，或者您对可靠性或性能有严格要求，这些集成商通过确保您不会得到容易出故障或使用两天就死机的硬件，提供了宝贵的服务。

有几家此类公司。我个人知道唯一一家这样的机构是 VA Research（http://www.varesearch.com）。

这些好心人用精美的 Tux（企鹅）标志在正面组装高端、高质量的 Linux 工作站。他们与 Linux 社区有着密切的联系（Debian 项目，http://www.debian.org，运行在他们后台的一台机器上，Linus 拥有他们的一台机器，他们偶尔还会向我们这位卑微的 HOWTO 维护者提供资源支持）。

对于像我们这样没有奢侈预算的人来说，本 HOWTO 的其余部分讲的是如何自己安装 Linux。

![](img/a3584dae761d2e3abed8bf40d7637389_108_0.png)

## 开始之前

在能够安装 Linux 之前，您需要确保您的机器具备运行 Linux 的能力，并选择要安装的 Linux 版本。Linux 安装前检查清单（http://members.tripod.com/~alogog/lnxchk.htm）可以帮助您在开始之前整理配置数据。

### 硬件要求

运行 Linux 需要什么类型的系统？这是一个好问题；系统的实际硬件要求会定期变化。Linux 硬件 HOWTO，http://Metalab.unc.edu/LDP/HOWTO/Hardware-HOWTO.html，提供了（大致）完整的受 Linux 支持的硬件列表。Linux INFO-SHEET，http://Metalab.unc.edu/LDP/HOWTO/INFO-SHEET.html，提供了另一个列表。

对于 Intel 版本的 Linux，任何 80386、80486、Pentium 或 Pentium II 处理器都可以。80386 及更高版本的非 Intel 克隆芯片通常也能工作。您不需要数学协处理器，但有一个会更好。

支持 ISA、EISA、VESA 局部总线（VLBUS）和 PCI 总线架构。MCA 总线架构（见于 IBM PS/2 机器）在最新的开发（2.1.x）内核中得到支持，但可能尚未完全准备好投入生产使用。

您的机器中至少需要 4 MB 内存。从技术上讲，Linux 只需要 2 MB 即可运行，但大多数安装和软件需要 4 MB。内存越多，您会越满意。如果您打算使用 X-Windows，我建议 8 或 16 MB。

当然，您需要一个硬盘和 AT 标准驱动器控制器。所有 MFM、RLL 和 IDE 驱动器及控制器应该都能工作。许多 SCSI 驱动器和适配器也得到支持；Linux SCSI-HOWTO 包含有关 SCSI 的更多信息。如果您是从零开始组装一台运行 Linux 的系统，SCSI 带来的额外性能 and 可靠性使其增加的少量成本物有所值。

您需要一个 3.5 英寸软驱。虽然 Linux 支持 5.25 英寸软盘，但它们很少使用，因此您不应指望磁盘镜像一定能容纳在它们上面。（简化版的 Linux 实际上可以运行在单个软盘上，但这仅用于安装和某些故障排除任务。）

您还需要 MDA、Hercules、CGA、EGA、VGA 或 Super VGA 显卡和显示器。一般来说，如果您的显卡和显示器在 MS-DOS 下工作正常，它们在 Linux 下也应该工作。但是，如果您希望运行 X-Windows，对支持的视频硬件还有其他限制。Linux XFree86-HOWTO，http://MetaLab.unc.edu/LDP/HOWTO/XFree86-HOWTO.html，包含有关运行 X 及其要求的更多信息。

您会想要一个 CD-ROM 驱动器。如果是 ATAPI、SCSI 或真正的 IDE，您应该没有使其工作的问题（但要注意那些宣传“IDE”接口但并非真正 IDE 的廉价驱动器）。如果您的 CD-ROM 使用专用接口卡，您即将从软盘启动的安装内核可能无法识别它——而一个无法访问的 CD-ROM 会使安装陷入僵局。此外，连接到并口的 CD-ROM 根本无法工作。如有疑问，请参阅 Linux CD-ROM HOWTO，http://MetaLab.unc.edu/LDP/HOWTO/CDROM-HOWTO.html，以获取受支持硬件的列表和详细信息。

所谓的即插即用（Plug’n’Play）无跳线卡可能会带来问题。对这些卡的支持正在积极开发中，但在 2.0.25 内核中尚未完善。幸运的是，这通常只可能是声卡或网卡的问题。

如果您运行的是使用 Motorola 68k 处理器（包括 pre-PowerPC 的 Macintosh、Amiga、Atari 或 VMEbus 机器）的机器，请参阅 http://www.clark.net/pub/1awrencec/linux/faq/Faq.html 处的 Linux m68k FAQ，以了解最低要求及移植状态的信息。FAQ 现在称 m68k Linux 的稳定性和可用性已与 Intel 版本相当。

### 空间要求与共存

您需要为硬盘上的 Linux 预留空闲空间。所需空间的量取决于您计划安装多少软件。大多数安装需要大约 200 到 500 MB 的空间。这包括软件空间、交换空间（用作机器的虚拟 RAM）、用户的空闲空间等。

理论上，您可以在 80 MB 或更少的空间内运行一个最小化的 Linux 系统（这在 Linux 发行版较小时很常见），也可以为所有 Linux 软件使用 500 MB 甚至更多的空间。数量的差异很大，取决于您安装软件的量以及您需要的空间量。我稍后将更详细地讨论这一点。

第一部分

