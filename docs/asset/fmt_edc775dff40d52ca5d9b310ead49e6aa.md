
在使用 `parted` 交互时，按 `?` 或输入 `help` 后跟命令关键字以获取帮助。`parted` 命令具有其他有用的功能，例如能够直接从一个分区复制文件系统到另一个分区。

最后，您可以通过使用可启动的 Linux 发行版（例如 LNX Bootable Business Card，可在 http://www.lnx-bbc.org/ 获取）启动系统，然后使用 `fdisk` 等原生 Linux 工具对驱动器进行分区，从而在安装前准备分区。

#### TIP

您可以使用第一张 Ubuntu CD 或 DVD 执行除安装 Linux 之外的其他任务。CD-ROM/DVD 具有救援模式，也可用于使用上述描述的 `fdisk` 对硬盘进行分区并为 Linux 做准备。

#### NOTE

可以创建双启动配置，这允许选择启动 Ubuntu 和另一个操作系统，例如 Windows XP。要将系统配置为双启动，您必须先安装 Windows，然后安装 Linux。请注意，许多 Windows 系统还原 CD-ROM 会清除硬盘上的所有数据，包括 Linux。在安装 Ubuntu 期间，您会自动将 GRUB Linux 启动加载程序安装到主驱动器的主引导记录或 MBR 中。当配置正确时，GRUB 允许您的系统重新启动到 Windows 或 Linux。浏览至 http://www.gnu.org/software/grub/manual/ 以在线阅读 GRUB 手册。

### CAUTION

在开始分区驱动器之前，请做好安全保障。首先，备份所有关键数据！对系统硬盘或操作系统的任何更改都会使现有数据面临风险。为了防止数据丢失后不可避免的时间和资源损失，请在对系统进行任何更改之前进行完整备份。在安装过程中创建启动盘（在安装完成前会提示您），这样如果出现问题，您至少能够启动 Linux。

## 选择分区方案

与部署和安装 Linux 一样，将硬盘分区以接受 Ubuntu 需要一些事先考虑，尤其是如果目标计算机将用于除作为家庭 PC 学习 Linux 之外的用途。如果 Linux 是唯一的驻留操作系统，您可以让安装程序根据安装过程中选择的安装类型自动创建并使用分区方案。如果您计划建立双启动系统，可以在其中启动 Linux 或其他操作系统，则必须在安装前以及可能在安装过程中手动分区硬盘。

Linux 系统最简单、最基本的分区方案需要一个 Linux 原生根分区和一个交换分区。在一个具有 12GB 存储和 512MB RAM 的单驱动器系统上，该方案可能如下所示：

| 硬盘分区 | 挂载点 | 大小 |
|---|---|---|
| `/dev/sda1` | `/` | 10.74GB |
| `/dev/sda2` | swap | 1GB |

在运行 Windows 的系统上，该方案可能如下所示：

| 硬盘分区 | 挂载点 | 大小 |
|---|---|---|
| `/dev/sda1` | `/media/dos` | 4GB |
| `/dev/sda2` | `/` | 7.74GB |
| `/dev/sda3` | swap | 1GB |

> CAUTION
> 笔记本用户在分区时应谨慎。某些笔记本使用一个等于安装 RAM 大小的特殊分区来执行挂起到磁盘或其他休眠操作。如果配置双启动系统，请务必检查计算机的初始分区方案，并保持该特殊分区不变！一种规避此问题的方法是使用 www.suspend2.net/ 上概述的软件挂起方法。

## 在单独分区上托管 Linux 文件系统的部分内容

您选择的特定分区方案将取决于 Ubuntu 的使用方式。在为扩展、更大容量或托管额外软件或用户的能力而设计的系统上，您可以使用单独的分区来托管 Linux 文件系统的各个部分。以下目录可作为这些单独分区的候选：

- `/home`—用户将在其目录下存储数百兆字节的数据。这是重要数据，甚至可能比系统本身更重要。使用单独的分区（在不同卷上）来存储此用户数据有助于使数据更易于查找，并将用户数据与系统数据隔离开来。您必须提前决定为用户分配多少存储空间。对于单台工作站，您应预留数 GB 的存储空间。
- **`/opt`**—作为额外软件包的主目录，此目录可以拥有自己的分区或远程文件系统。Ubuntu 不会填充此目录，但它可能被您以后安装的其他软件包使用。一 GB 的存储空间应该足够，具体取决于要安装的应用程序。
- **`/tmp`**—此目录可被用户用作临时存储，尤其是在执行磁盘配额时；因此，它可以放在自己的分区上。此目录可以小至 100MB。
- **`/usr`**—此目录包含 Ubuntu 系统上几乎所有的软件，如果添加额外软件，尤其是工作站配置，可能会变得相当大。使用单独的分区是有意义的。完整安装至少需要 6GB 用于此目录，如果添加额外软件则需要更多。
- **`/var`**—将此目录（或其中某些子目录）放在单独的分区上可能是一个好主意，尤其是因为安全日志、邮件和打印排队都在此树下进行。您应为 `/var` 预留至少一 GB 的存储空间，尤其是如果将 Ubuntu 用作打印服务器（因为排队文档将驻留在 `/var/spool` 下）。

#### TIP

作为一般规则，将用户数据与系统数据分离是一个好主意。尽管 Linux 系统可以快速恢复，但用户数据具有更大的价值，并且可能更难以替换。分离数据可以使备份和恢复工作变得容易得多。如果您在访问分区时遇到任何问题，我们建议您获取优秀的 Knoppix 发行版，它完全从 CD 启动并运行。这将使您能够访问分区并进行必要的修复。

#### Reference

- http://www.yale.edu/pclt/BOOT/DEFAULT.HTM—一个基本分区入门教程，不特定于操作系统。
- http://www-1.ibm.com/linux/—IBM Linux 主页，提供产品、服务和下载的链接。
- http://www-124.ibm.com/developerworks/opensource/linux390/—IBM S/390 Linux 解决方案主页。
- http://www.dell.com/linux/—Dell Computer 的 Linux 信息页面。
- http://hardware.redhat.com/hcl/—Red Hat 硬件兼容性数据库的入口点。
- http://www.linux1394.org/—Linux FireWire 项目主页，提供有关该端口驱动程序和设备的状态信息。

- http://www.linux-usb.org/—Linux USB 项目的主页，提供支持的设备列表和驱动程序链接。
- http://elks.sourceforge.net/—Linux for x286 及以下 CPU 的主页，ELKS Linux。
- http://www.lnx-bbc.org/—可启动名片的主页，这是一款 50MB 的压缩 Linux 发行版，提供数百种网络客户端、实时 X 会话、网页浏览、PDA 备份、无线网络、救援会话和文件恢复功能。
- http://www.coyotelinux.com/—多个紧凑型 Linux 发行版的主页，提供防火墙和 VPN 服务。基于软盘的发行版在老旧 PC 上运行效果相当不错，且无需硬盘。
- http://www.freesco.org/—基于软盘的 Linux 路由器解决方案的主页，可在 386 PC 上运行，仅需 6MB RAM，并提供桥接、防火墙、IP 伪装、DNS、DHCP、网页、telnet、打印、时间及远程访问功能。
- http://www.bitwizard.nl/sig11/—对 Linux 信号 11 错误的一些根本原因的详细概述。
- http://www.gnu.org/software/parted/parted.html#introduction—GNU parted 工具的主页。
- http://www.linux.org/vendors/systems.html—可查询附近供应商是否在 PC、笔记本、服务器或硬盘上预装销售 Linux 的地方之一。

## APPENDIX C

## Ubuntu 和 Linux 互联网资源

Linux 拥有丰富的互联网支持，包括提供技术信息、特定程序文档、针对性白皮书、错误修复、用户体验、第三方商业技术支持，甚至免费的专业、精细调校的克隆发行版的网站。

本附录列出了许多可用于获取有关 Ubuntu 副本的更多信息和帮助的支持网站、FTP 仓库、Usenet 新闻组和电子邮件列表。

## 如果您需要 24/7 帮助

如果您是小型企业、企业级或企业级 Ubuntu 用户，请不要忘记您始终可以求助于源头 Canonical，或提供商业技术支持的第三方公司，他们可提供 24/7 现场、电话、电子邮件甚至按事件计费的商业技术支持。Canonical Software 为其软件产品提供一系列支持选项。您可以在 Ubuntu 网站上阅读有关支持选项的更多信息：
http://www.ubuntu.com/support/paid.

本附录分为以下几个部分：

- 按类别排列的 Linux 信息网站
- 与 Linux 相关的 Usenet 新闻组
- 提供 Linux 用户和开发者讨论的邮件列表
- 用于 Linux 信息的 Internet Relay Chat 群组

## 本附录内容

- 网站和搜索引擎
- Usenet 新闻组
- 邮件列表
- Internet Relay Chat

本附录还列出了在使用 Ubuntu 或特定组件（如 Xorg）时可能具有一般兴趣的网站。已尽最大努力确保 URL 的准确性，但请记住互联网始终处于变化之中！

## 保持最新

了解错误修复、安全更新和其他勘误对于 Ubuntu 系统的成功和健康至关重要。为了跟上使用 Ubuntu 时最重要的发展，请务必注册 Ubuntu Announcements 邮件列表。从那里，您将了解到已发布哪些更新以及因此修复了什么。前往 https://lists.ubuntu.com/mailman/listinfo/ubuntu-security-announce 注册此邮件列表。您还应留意 Update Manager 通知，以便跟上错误修复、新软件包和安全更新。

## 网站和搜索引擎

 literally 有数千个网站提供有关 Linux 和 Ubuntu 的信息。立即获得所需答案的关键在于使用最佳的搜索引擎和技术。知道如何搜索可以在排除故障时在挫败感和成功之间产生差异。本节提供一些互联网搜索技巧，并按各种主题列出与 Ubuntu 和 Linux 相关的网站。列表并不全面，但在撰写本文时已进行了核查并且可用。

## Web 搜索技巧

通过搜索网络来排除 Linux 问题可以是一种高效且富有成效的获取棘手问题答案的方法。进行有效搜索的最基本规则之一是使用特定的搜索词来查找特定的答案。例如，如果您简单地搜索“Ubuntu Linux”，您将得到太多链接和太多信息。如果您搜索“Ubuntu sound”，您更有可能找到所需的信息。如果您收到错误消息，请使用它；否则，请使用 Linux 内核诊断消息作为搜索标准。

其他有效技术包括以下内容：

- 在搜索字符串中使用符号，例如加号 (+) 来强制匹配包含两个字符串的网页（如果网页搜索站点使用的搜索引擎支持此类功能）
- 在返回结果中进行搜索
- 对结果进行排序（通常按日期排序以获取最新信息）
- 搜索相关信息
- 词干搜索；例如，指定不仅返回“link”还返回“linking”和“linked”的结果

花些时间尝试使用你最喜欢的搜索引擎的功能，结果将带来更高效的搜索。除了磨炼你的搜索技能，还要花时间选择最适合你需求的搜索引擎。

## 谷歌是你的朋友

网络上一些最快、最全面的搜索引擎由 Linux 驱动，因此使用最好的可用资源是明智之举。在众多提供搜索引擎的网站中，http://google.com 脱颖而出，每月拥有数百万用户。该网站利用先进的硬件和软件为你的搜索带来速度和效率。如果你在寻找特定的 Linux 答案，可以访问谷歌的 Linux 页面 http://google.com/linux。

为什么谷歌（以一个数学数字命名）如此强大？你可以从 http://www.google.com/technology/ 上的谷歌员工那里获得一个快速概览。它的成功部分归功于出色的算法、优秀的编程和简单的界面设计；但大多数用户似乎确实很欣赏谷歌那种不可思议的能力，能在搜索结果的第一页就提供你正在寻找的链接。谷歌早期的成功也得益于该网站在数千台运行 Red Hat Linux 版本的 PC 集群上运行其搜索引擎！还有传言称，谷歌的台式机使用基于 Ubuntu 的发行版，据说名为 Goobuntu。

谷歌拥有网络上所有搜索引擎中最大的数据库，已搜索并索引超过 80 亿个网页。数据库的大小很重要，因为空的搜索结果对在线用户毫无用处，而在冷门主题上返回命中结果的能力可能决定成败，或决定是满意还是沮丧。谷歌的一些功能包括：在结果页面上通过 GoogleScout 链接返回类似页面；能够查看搜索引擎返回的网页精确版本（即缓存功能）；高级搜索；以及最近新增的指向活跃 Usenet 新闻源的链接！

为了更好地了解谷歌能为你提供什么，请访问 http://www.google.com/options/。你会找到许多不同服务和工具的链接，涵盖专业搜索、数据库、信息链接、翻译器以及其他有用的浏览工具。

## Ubuntu 软件包列表

使用 `synaptic`，你可以快速轻松地查看 Ubuntu 系统上已安装软件包的列表，以及每个软件包的简短描述。

`synaptic` 还会显示每个软件包的描述，以便你可以决定是否安装。有关 `synaptic` 的更多信息，请参阅第31章“管理软件”。

## 认证

Linux 认证课程是快速发展的信息技术培训行业的一部分。如今，数百家不同的供应商提供关于 Linux 技能集的课程和测试。然而，由于 Linux 是开源软件，对于认证需要什么知识或专业水平，没有正式的规则或强制要求。如果你对认证感兴趣，并想从事相关职业或在使用 Linux 的公司就业，那么你真的应该寻求培训。你可以在 http://www.ubuntu.com/training/ 找到一份按地理区域划分的、可提供培训的公司的详细列表。

## 商业支持

对 Ubuntu 的商业支持是 Linux 在企业界和商业界取得成功的关键要素。尽管有数百甚至数千名精通 Linux 和 UNIX 的顾问可以提供有偿服务，但以下是几家最知名的 Linux 支持提供商：

- http://www.ubuntu.com/support/paid——直接前往源头获取一系列支持选项。你可以直接从 Canonical 软件或当地支持提供商那里获得 Ubuntu 帮助。
- http://www.hp.com/linux——HP 提供全面的 Linux 服务和硬件组合，几乎涵盖你想做的一切，包括咨询、业务解决方案、硬件规格和实施。
- http://www.ibm.com/linux/——IBM 提供的 Linux 服务包括电子商务解决方案、开源咨询、数据库迁移、集群、服务器和支持。

除了以服务为导向的支持公司外，几乎每个商业 Linux 发行商都提供某种易于购买商业支持的形式。利用支持服务的方式有多种（例如远程管理、现场咨询、设备驱动程序开发等），但需求会因客户情况和安装环境而异。

## 加入 Linux 用户组的好处

加入当地的 Linux 用户组（LUG）！加入并参与当地的 LUG 有许多好处。你将能够获得帮助、交流信息，并学到许多关于 Linux 的新奇而美妙的知识。大多数 LUG 不收取会员费，而且许多 LUG 经常赞助由顶尖 Linux、GNU 和开源专家主讲的定期讲座和讨论。一个很好的起点是访问 http://www.lug.org/luglist.html。

## 文档

几乎所有 Linux 发行版都包含数千页的文档，形式包括手册页、HOWTO 文档（有各种格式，如文本和 HTML）、mini-HOWTO 文档或软件包文档（通常位于 `/usr/share/doc/` 目录下）。然而，阅读这些文档最新版本的权威网站是 Linux 文档项目，网址为 http://www.tldp.org。

## Linux 指南

如果你正在寻找关于某个 Linux 主题更广泛、更详细的资料，可以尝试阅读众多 Linux 指南中的一本。这些指南针对多个主题，涵盖技术话题的深度和节奏比 HOWTO 更详细、更从容。你可以找到以下内容的副本：

- “Advanced Bash-Scripting Guide,” by Mendel Cooper; a guide to shell scripting using bash
- “LDP Author Guide,” by Mark F. Komarinski; how to write LDP documentation
- “Linux Administration Made Easy,” by Steve Frampton
- “Linux Consultants Guide,” by Joshua Drake; a worldwide listing of commercial Linux consultants
- “Linux from Scratch,” by Gerard Beekmans; creating a Linux distribution from software
- “Linux Kernel Module Programming Guide,” by Peter Salzman, Michael Burian, and Ori Pomerantz; a good guide to building 2.4 and 2.6 series modules
- “Securing and Optimizing Linux,” by Gerhard Mourani
- Linux Certification
- “The Linux Network Administrator’s Guide, Second Edition,” by Olaf Kirch and Terry Dawson; a comprehensive Net admin guide

## Ubuntu

- http://www.ubuntu.com—Home page for Ubuntu, Canonical’s community-based free Linux distribution. Ubuntu is the main release of this Linux distribution and includes thousands of software packages that form the core of an up-to-date, cutting-edge Linux-based desktop. You can also find links to the other *buntus, such as Kubuntu, Xubuntu, and edubuntu.
- http://www.ubuntuforums.org—A good place to go if you need specific Ubuntu support.

## Mini-CD Linux 发行版

Mini-CD Linux 发行版用于许多不同的目的。有些发行版用于启动到只读的防火墙配置；其他发行版用于提供尽可能完整的救援环境；而另一些则用于安装或帮助启动完整发行版的安装。Mini-CD 有多种尺寸可供选择，例如 3" CD-R（或 CD-RW），大小范围从 185MB 到 210MB。你也可以下载一个 `.iso` 镜像并制作一张 Linux 可启动的名片，通常可容纳在 40MB 或 50MB 的信用卡大小的 CD-R 上。 （如果您想经常升级发行版，请考虑使用 mini-CDRW。）以下是这些发行版的一些链接：

- http://www.lnx-bbc.com—Home page for the Linux BBC, a 40MB image hosting a rather complete live Linux session with X, a web browser, and a host of networking tools.
- http://crux.nu/—Home page of the CRUX i686–optimized Linux distribution.
- http://www.smoothwall.org—The 69MB SmoothWall distribution is used to install a web-administered firewall, router, or gateway with SSH, HTTP, and other services.

## 各种基于 Intel 的 Linux 发行版

为基于 Intel 的 PC 选择 Linux 发行版（distro）通常是个人偏好或需求的问题。许多 Linux 用户因其出色的支持、商业支持选项以及在全球范围内的广泛使用而偏爱 Red Hat 的发行版。然而，有许多不同的 Linux 发行版可供下载。寻找新发行版或你喜爱的发行版新版本时，最好的起点之一是 http://www.distrowatch.com。

- http://www.xandros.net—Home of the original and improved version of Corel’s Debian-based Linux
- http://www.debian.org—The Debian Linux distribution, consisting only of software distributed under the GNU GPL license. Ubuntu, itself, is based upon Debian.
- http://www.slackware.com—Home page for download of the newest version of one of the oldest Linux distributions, Slackware
- http://www.opensuse.org—Home page for SUSE Linux, also available for the PowerPC and x86 64 platforms
- http://www.mepis.org—An increasingly popular distribution based on Debian
- http://www.mandrivalinux.com—A Pentium-optimized, RPM-based distribution, originally based on Red Hat’s Linux distribution

## 基于 PowerPC 的 Linux 发行版

- http://penguinppc.org/—Home page for the PowerPC GNU/Linux distribution
- http://www.opensuse.org—SUSE PPC Linux
- http://www.yellowdoglinux.com—Home page for Terra Soft Solution’s Yellow Dog Linux for the PowerPC, which is based on Fedora

## 笔记本电脑和PDA上的Linux

获取在笔记本电脑上运行Linux信息的一个权威网站是Kenneth Harker的Linux Laptop网站。尽管更新不像过去那样频繁，该网站（http://www.linux-laptop.net）仍包含世界上最大的Linux和笔记本电脑信息集，并提供指向用户体验和特定笔记本型号详情的链接。

另一个可查阅的网站是Werner Heuser的Tuxmobil-Mobile UNIX网站（http://www.tuxmobil.org）。你将在其中找到链接到如IrDA、Linux PDA和手机等信息。Linux Zaurus PDA用户可浏览http://www.openzaurus.org下载适用于Zaurus 5000和5500型号的完整开源替代操作系统。

## X窗口系统

尽管因特网上有很多关于X窗口系统的技术信息，但在故障排查时找到具体问题的答案可能会很困难。如果你使用X时遇到问题，首先尝试确定问题是软件还是硬件相关的。在搜索或寻求帮助时（例如在Usenet的comp.os.linux.x新闻组，你可以通过Google的Groups链接访问；下一节有其他有用的Linux新闻组），请尽量具体。充分评估一个问题所需的一些关键因素或信息包括：使用的Linux发行版；使用的内核版本；使用的X版本；你的显卡的品牌、名称和型号；你的显示器和其他相关硬件的名称、品牌和型号。

本节仅列出Linux X用户的一些基本资源。关于X的权威技术信息可从http://www.X.org获取：

- http://www.lesslif.org/—GPL授权的OSF/Motif克隆Less'tif的主页
- http://www.rahul.net/kenton/index.shtml—Ken Lee的X和Motif网站，提供大量关于X的教程、开发和其他信息的链接
- http://www.x.org—X.org的主页，Ubuntu中使用的X服务器
- http://www.xig.com/—Linux的X商业版本（以及其他软件产品）的主页

## Usenet新闻组

如果你在使用Linux时遇到麻烦，Linux相关的Usenet新闻组是另一个好的信息来源。如果你的ISP不提供全面的Linux新闻组选择，你可以浏览http://groups.google.com/。

主要的Linux及与Linux相关的新闻组如下：

- alt.os.linux.dial-up—使用PPP进行拨号
- alt.os.linux.mandriva—有关Mandriva Linux的一切
- alt.os.linux.slackware—使用Slackware Linux
- alt.os.linux.ubuntu—使用Ubuntu Linux
- comp.os.linux.advocacy—关于Linux及其他相关问题热议的讨论
- comp.os.linux.alpha—在Alpha CPU上使用Linux
- comp.os.linux.announce—一般Linux公告
- comp.os.linux.answers—新的Linux常见问题解答及其他信息的发布
- comp.os.linux.development.apps—使用Linux开发工具
- comp.os.linux.development.system—构建Linux内核
- comp.os.linux.embedded—Linux嵌入式设备开发
- comp.os.linux.hardware—为各种硬件设备配置Linux
- comp.os.linux.m68k—在摩托罗拉68K系CPU上使用Linux
- comp.os.linux.misc—杂项Linux主题
- comp.os.linux.networking—网络与Linux
- comp.os.linux.portable—在笔记本电脑上使用Linux
- comp.os.linux.powerpc—使用PPC Linux
- comp.os.linux.security—Linux安全问题
- comp.os.linux.setup—Linux安装主题
- comp.os.linux.x—Linux和X窗口系统
- comp.windows.x.apps—使用基于X的客户端
- comp.windows.x.i386unix—用于Unix PC的X
- comp.windows.x.intrinsics—X工具箱库主题
- comp.windows.x.kde—使用KDE和X的讨论
- comp.windows.x.motif—有关Motif编程的一切
- comp.windows.x—关于X的讨论
- linux.admin.*—两个面向Linux管理员的新闻组
- linux.debian.*—30个关于Debian的新闻组

- `linux.dev`—25 or more Linux development newsgroups
- `linux.help`—Get help with Linux
- `linux.kernel`—The Linux kernel

## Mailing Lists

Mailing lists are interactive or digest-form electronic discussions about nearly any topic. To use a mailing list, you must generally send an email request to be subscribed to the list, and then verify the subscription with a return message from the master list mailer. After subscribing to an interactive form of list, each message sent to the list will appear in your email inbox. However, many lists provide a digest form of subscription in which a single- or half-day's traffic is condensed in a single message. The digest form is generally preferred unless you have set up electronic mail filtering.

The main Ubuntu mailing lists are detailed here, but there are quite a few Linux-related lists. You can search for nearly all online mailing lists by using a typical mailing list search web page, such as the one at http://www.lsoft.com/lists/list_q.html.

| GNOME and KDE Mailing Lists |
|---|
| GNOME users and developers should know that more than two dozen mailing lists are available through http://mail.gnome.org/. KDE users will also benefit by perusing the KDE-related mailing lists at http://www.kde.org/mailinglists.html. |

## Ubuntu Project Mailing Lists

The Ubuntu Project is always expanding, as many new users continue to find Ubuntu for the first time. You will find many other knowledgeable users with answers to your questions by participating in one of Ubuntu’s many mailing lists. The lists are focused on using, testing, and developing and participating in Ubuntu’s development:

- http://lists.ubuntu.com/mailman/listinfo/ubuntu-security-announce—来自 Ubuntu 开发者的安全公告
- http://lists.ubuntu.com/mailman/listinfo/ubuntu-announce—关于 Ubuntu 的公告
- http://lists.ubuntu.com/mailman/listinfo/ubuntu-users—Ubuntu 版本用户之间的讨论
- http://lists.ubuntu.com/mailman/listinfo/ubuntu-devel—Ubuntu 测试版的开发者和测试者的查询和报告

##### Internet Relay Chat

*Internet Relay Chat (IRC)* is a popular form and forum of communication for many Linux developers and users because it allows an interactive, real-time exchange of information and ideas. To use IRC, you must have an IRC client and the address of a network and server hosting the desired chat channel for your discussions.

You can use the irc.freenode.net IRC server, or one listed at http://www.freenode.net/ to chat with other Ubuntu users. Some current channels are as follows:

- #Ubuntu—关于 Ubuntu 的 general 聊天
- #edubuntu—关于 EdUbuntu 的 general 聊天
- #xubuntu—关于 Xubuntu 的 general 聊天
- #kubuntu—关于 Kubuntu 的 general 聊天

For more channels to look at head on over to https://help.ubuntu.com/community/InternetRelayChat for an exhaustive list of "official" channels.

However, Google can help you find other channels to explore. Simply enter in the distro name and IRC into the search options to retrieve information on any IRC channels relevant to your requirements. To get help with getting started with IRC, browse to http://www.irchelp.org/. Some of the channels of interest might be

- #linux—关于 Linux 的 general 讨论
- #linuxhelp—面向新用户的帮助聊天讨论

Most IRC networks provide one or more Linux channels, although some providers require signup and registration before you can access any chat channel.

## Index

## SYMBOLS

& (ampersands)
  && (double ampersands) number comparison operators, 260
  shell background processing, 238
* (asterisks), 77
  * operator (Python), 552
  shell pattern-matching searches, 236
  wildcards, 448
/ (backslashes) as escape characters, 251
` (backticks), replacing strings with output, 251
: (colons), as slices, 554
$ (dollar signs)
  $* built-in variable, 248
  $# built-in variable, 248
  $? built-in variable, 248
  $0 built-in variable, 248
= (equal signs)
  == (double equal signs) string comparison operators, 257
  number comparison operators, 258
  string expression operators, 252
! (exclamation points)
  !=
    is not equal symbol (SQL), 493
    string comparison operators, 257
    string expression operators, 252
    logical comparison operators, 256
    number comparison operators, 260
< (greater than) number comparison operators, 258

758 Apache Server

+ >（小于）数字比较运算符，258
+ |（管道）
+ |（bar 运算符），238
+ ||（双竖线）
+ 数字比较运算符，260
+ 字符串连接函数，493
+ + 运算符（Python），552-553
+ #（井号）
+ # run-parts 行（/etc/crontab 文件），231
+ #!（shebang 行），241-243，527
+ ?（问号），shell 模式匹配搜索，236
+ ’（引号）
+ ”（双引号），在包含嵌入空格的 shell 字符串中解析变量，249-250
+ 保持 shell 字符串中未展开的变量，250

## NUMBERS

+ 00-INDEX 文件，691
+ 3D 视频卡，185
+ 10BASE-T NIC（网络接口卡），320
+ 64 位 Ubuntu，721
+ 100BASE-T NIC（网络接口卡），321
+ 1000BASE-T NIC（网络接口卡），321
+ 1000BASE-X，321
+ 1000BASE-X NIC（网络接口卡），321

## A

+ -a 逻辑比较运算符，256
+ a2p 过滤器，544
+ a2ps 命令，175
+ AbiWord（GNOME Office），136-137，141
+ aci 命令，205，217
+ accept 命令，175，181

+ 访问控制指令（ftpaccess 配置文件）
+ 阻止主机服务器访问，434
+ 配置 wu-ftpd 服务器，433-436
+ 定义用户类，434
+ 限制
+ 匿名用户访问，434
+ 无效密码输入次数，436
+ 基于个人 ID 的权限，435
+ 限制
+ 类中用户数量，435-436
+ 基于组 ID 的权限，435
+ 访问权限（文件），通过 chmod shell 命令更改，655
+ 访问点，无线网络安全，629
+ ACID（原子性一致性隔离持久性），数据库合规性比较，495-496
+ ACL（访问控制列表），Squid 代理服务器，477-481
+ ACPI（高级配置和电源接口），Ubuntu 电源管理，41
+ 操作（PHP 循环），579
+ Adblock Plus，107
+ 后缀插件，446
+ 前缀插件，446
+ 添加/删除应用程序，软件管理，677
+ 基于地址的虚拟主机，416
+ 管理
+ FTP 服务器命令，449-454
+ LDAP，520-521
+ 管理员模式按钮（kdm），66
+ ADSL 调制解调器，348
+ adsl-stop 命令，349
+ afio 备份软件，302
+ alias 命令，443-444
+ 别名，myenv shell 脚本，239
+ allow 指令（Apache Web 服务器），406-407
+ AllowOverrides 配置指令（Apache Web 服务器），405-406

ALSA（高级 Linux 声音架构）声卡驱动，161
Amanda 备份应用程序，301-302
AMD 处理器，721
amdump 命令，308
美国互联网号码注册机构网站，314
与号（&）
  双与号（&&）数字比较运算符，260
  shell 后台处理，238
AND 语句（SQL），493
anon mkdir 写启用设置（vsftpd 服务器匿名访问控制），429
anon other 写启用设置（vsftpd 服务器匿名访问控制），429
anon upload 启用设置（vsftpd 服务器匿名访问控制），430
匿名访问 vsftpd 服务器，控制，430
anonymous enable 设置（vsftpd 服务器匿名访问控制），429
匿名 FTP 服务器，423
  与经过身份验证的 FTP 服务器的比较，424
  配置，433
Apache Group 网站，392
Apache Server
  开发，391，392
  文档网站，392
  下载，392-393
  文件系统
    访问控制，406-407，410
    身份验证，407-409
  安装
    文件位置，396
    来自 APT，393-394
  Internet 安全，406
  日志
    常用日志格式，418
    CustomLog 指令，420
mod_access 模块，411
mod_alias 模块，411
mod_asis 模块，411
mod_auth 模块，412
mod_auth_anon 模块，412
mod_auth_dbm 模块，412
mod_auth_digest 模块，412
mod_autoindex 模块，413
mod_cgi 模块，413
mod_dir 模块，413
mod_env 模块，413
mod_expires 模块，413
mod_headers 模块，413
mod_include 模块，414
mod_info 模块，414
mod_log_config 模块，414
mod_mime 模块，414
mod_mime_magic 模块，414
mod_negotiation 模块，414
mod_proxy 模块，414
mod_rewrite 模块，414
mod_setenvif 模块，415
mod_ssl 模块，415
mod_speling 模块，415
mod_status 模块，415
mod_unique_id 模块，415
mod_userdir 模块，415
mod_usertrack 模块，416
mod_vhost_alias 模块，416
优化，642-644
快速入门指南，396-397
运行时配置
  配置指令，400-406
  httpd.conf 配置文件，400
  MPM，403-404
安全报告网站，393
源代码，构建，395-396

启动/停止
  手动启动，397-398
  通过 /etc/init.d/apache2 脚本，398-399
升级，文件位置，394
使用统计，391
版本信息，392-393
虚拟主机
  基于地址的主机，416
  内网网站，418
  基于名称的主机，417-418
Apache 软件基金会，392
apachectl 命令，421
追加运算符，237
Application.Run() 方法，619
应用程序
  商务，726-728
  电子邮件，107
    Evolution，108-109
    KMail，112
    Thunderbird，111
  Firefox，106, 113
游戏
  Battle for Wesnoth，190
  DOOM 3，186
  安装视频驱动程序，184-185
  概述，183-184
  使用 Cedega 玩 Windows 游戏，190-191
  Quake 4，188-189
  Unreal Tournament 2004，187-188
  Wolfenstein: Enemy Territory，188-189
GetCodecs，167
家庭商务，720
即时通讯（使用 Pidgin），114-115
IRC，115-117
Konqueror，107
多媒体，143
  刻录 CD/DVD，154-161
  数码相机，150
F-Spot，152-153
GIMP，146-150
手持数码相机，151
Rhythmbox，144-145
声卡，161-164
视频，164-169
Pan 新闻客户端与新闻阅读器，119-120
办公效率，123
  Calc（OpenOffice.org），130-135
  配置 OpenOffice.org，126-127
  办公工具（OpenOffice.org），135-139
  OpenOffice.org，124-125
  Windows，141
  Writer（OpenOffice.org），127-129
RSS 阅读器，113-114
system-config-display，55
文本编辑器，87
  emacs，89-90
  vi，88
Ubuntu 商务，719-720
Usenet 新闻/新闻组，117-118
视频会议（使用 Edge），120-121
应用程序菜单，添加/删除应用程序，677
apropos 主题命令，76
APT（高级软件包工具）
Apache 服务器安装，393-394
deb 文件存储，684
软件管理，681
日常使用，682-685
查找软件，685
apt-cache 搜索工具，685
apt-get 命令，687, 748
apt-get dist-upgrade 命令，683
apt-get remove 命令，684
apt-get install 命令，684
apt-get update 命令，682-684
ar 命令，608
arch 目录（/usr/src/linux-2.6 目录），692
归档，77

- ark 备份工具，300
- ark 命令，308
- 数组，567-569
  - Perl，528-529
  - PHP 函数
    - array keys()，586
    - array unique()，585
    - array values()，586
    - arsort()，586
    - asort()，586
    - extract()，586-587
    - krsort()，586
    - ksort()，586
    - shuffle()，585
- arsort() 数组函数，586
- ars 命令，608
- asort() 数组函数，586
- 评估备份需求，289-290
- 分配
  - 权限，91-92
  - 值赋给
    - Python 字符串，550
    - shell 脚本变量，243
- 星号（*），77
  - * 运算符（Python），552
  - shell 模式匹配搜索，236
  - 通配符，448
- at 命令，计划任务，228-230
- ATAPI（AT 附件包接口），44
- ATI 驱动程序，安装，184-185
- atime（文件），为文件系统优化而禁用，641
- 原子性（ACID），数据库合规性比较，495
- at 命令，查看批处理作业编号，230
- atrm 命令，删除批处理作业，230
- 音频。请参阅声卡
- 音频格式常见问题解答，164

- 认证
  - Apache Web 服务器文件系统，407-409
  - FTP 服务器，423-424
  - PAM，208
- AuthGroup 指令（Apache 服务器），409
- AuthName 指令（Apache 服务器），409
- AuthType 指令（Apache 服务器），409
- AuthUserFile 指令（Apache 服务器），409
- autoconf 命令，608
- autoconfig 工具（C/C++ 编程语言），603
- 自动入侵，626
- 自动化任务
  - 计划任务
    - at 命令，228-230
    - batch 命令，229-230
    - cron 守护进程，231-233
  - shell 脚本
    - 别名，239
    - 内置变量，243, 248
    - 命令，239
    - 注释，239
    - 环境变量，243
    - 执行，240
    - 位置参数，244-246
    - 使用原因，238
    - shebang 行（#!），241-243
    - 特殊字符列表，248-249
    - 存储以供系统范围访问，241
    - 测试，247
    - 文本换行，239
    - 木马脚本，241
    - 用户变量，243
    - 变量，访问值，244
    - 变量，赋值，243
    - 变量，在其中存储字符串，244
  - shell
    - 后台处理，238
    - 反斜杠（\）作为转义字符，251

## B

- bash shells，233-234
  - backticks (\`)，用输出替换字符串，251
  - 更改，241
  - 表达式比较
    - 文件比较，255-256
    - 逻辑比较，256-257
    - 数字比较，254-255
    - 字符串比较，252-253
  - Fedora Core shells 列表，233-234
  - 输入/输出重定向，234，237
  - job-control 命令，234-235
  - 维护包含未展开变量的 shell 字符串，250
  - man 手册页，234
  - 模式匹配，234-236
  - 管道 (|)，234，238
  - 位置参数，244-246
  - 在包含嵌入空格的字符串中解析变量，249-250
  - shell 命令行，234-238
  - test 命令
    - 文件比较，255-256
    - 逻辑比较，256-257
    - 数字比较，254-255
    - 字符串比较，252-253
- system services
  - 启动到默认运行级别，223
  - 启动到非默认运行级别，224
  - 启动到运行级别，222
  - 更改运行级别，225
  - init 脚本，224-225
  - 启动引导过程，220-221
  - 加载 Linux 内核，221
  - 手动启动/停止，228
  - 运行级别故障排除，226-227
- autoresponders（电子邮件），471
- avi 文件，167
- awk，shell 模式匹配搜索，236
- Axis Linux-based cameras 网站，150
- background processing，后台处理，238
- backgrounds（桌面），更改，31
- backreferencing，反向引用，592-593
- backslashes (`\`) 作为转义字符，251
- backticks (\`)，用输出替换字符串，251
- backups，备份，287
  - CD-RW 驱动器，295
  - 配置文件，288
  - 顾问，289
  - 数据丢失原因，288
  - FireWire（IEEE-1394）驱动器，295
  - 频率，确定，289-290
  - 完整备份
    - 增量备份策略，293
    - tar 命令行备份软件，297
  - 增量备份
    - 完整备份策略，293
    - tar 命令行备份软件，297
  - kernel，701
  - 级别，292
  - MBR，306-307
  - NAS，295
  - 需求评估，289-290
  - 资源可用性，289
  - 从备份恢复文件，298
  - 安全，629
  - 软件
    - afio，302
    - Amanda 备份应用程序，301-302
    - ark，300
    - cdbbackup，302
    - File Roller，299
    - flexbackup，302
    - kdat，300
    - tar，297-298
  - 良好实践，290
  - 策略
    - 选择，294
    - 评估，291-293
    - 家用策略，291
    - 继承，292
    - 大型企业策略，291
    - 数据镜像，293
    - 原则，290
    - RAID 数组，293
    - 小型企业策略，291
    - 小型办公室策略，291
    - 磁带驱动器，295
    - USB 驱动器，295
- badblocks 命令，文件系统优化，641
- bak 文件扩展名，25
- Balsa（GNOME Office），137
- bar operator（|），238
- Base（OpenOffice.org），125
- batch 命令，调度任务，228-230
- Battle for Wesnoth，安装，190
- Beagle，Mono 库，617-620
- beep codes，蜂鸣代码，221
- Behlendorf，Ben，Apache Server 开发，391
- /bin 目录，78
- /bin/netstat 网络配置工具，331
- BIOS（Basic Input Output System）
  - 蜂鸣代码，221
  - 启动引导过程，220
  - 硬盘优化，638
- .bmp 图像文件格式，148
- boot loaders
  - 启动引导过程，220-221
  - BootMagic，221
  - GRUB，221
  - 启动系统服务到非默认运行级别，224
  - 密码，224，629
  - 系统启动，307
  - LILO，221
- booting systems
  - 从通用软盘启动，307
  - 重启，99
- BootMagic，221
- Bootp 协议，335
- break 关键字（Python），控制循环，558
- break 语句（PHP），270
  - 循环，581
  - switch/case 块，579
- Breezy Badger，719
- bridges，桥接，324，631
- broadcast addressing，广播寻址，319
- brute-forcing，暴力破解，359
- Bsdftpd-ssl 服务器，425
- Bt 系列视频芯片组（Brooktree），165
- BugTraq 邮件列表，634
- built-in shell 命令，101
- built-in variables（shell 脚本），243，248
- Bullet Proof X，56
- bunzip2 命令，77
- burning CDs/DVDs，刻录 CD/DVD，154
  - 命令行，158-161
  - 图形客户端，155-157
- business applications，企业应用，719-720，726-728
- Bynari，472
- bzdisk 指令，内核编译，702
- bzip2 指令，内核编译，702
- bzip2 命令，77，698

## C

- C 编程语言，开发，599-600
- C#
  - Mono，614-615
  - 网站，622
- C/C++ 编程语言
  - 开发，600
  - gcc（GNU C 编译器），605-606
  - 图形开发工具，606-607
  - 项目管理工具
    - autoconf 工具，603
    - 调试工具，604-605
    - make 命令，600-602
    - Subversion 系统，603-604
- cable（网络）
  - 光纤，323
  - UTP，322
- Calc（OpenOffice.org），124，130-135
- cameras，摄像机，150
  - F-Spot，152-153
  - GIMP，146
  - 捕获屏幕图像，150
  - 图像文件格式，148-150
  - 扫描仪，147-148
  - 手持式，151
- cancel 命令，175，181
- Canonical Software，718
- capturing screen images，捕获屏幕图像，150
- caricatures，漫画，199
- cdbackup 备份软件，302
- cdrecord 命令，158
- cdrecord -scanbus 命令，154
- CDs
  - 启动引导过程，221
  - 刻录，154
  - 从命令行创建，158-161
  - 使用图形客户端创建，155-157
  - 命令行创建，158
  - Rhythmbox，144-145
  - Ubuntu 安装，11-12
  - 用途，154
- Cedega，使用 Windows 游戏，190-191
- certification course 网站，749-750
- cervisia 命令，608
- chage 命令，217
- chat，IRC，115-117
- chattr 命令，文件系统优化，641
- checklists
  - 清单，738-740
  - 部署前规划，730
- chfn 命令，95，217
- chgrp 命令，198，217
- chmod 命令，93，198，217，655
- chown 命令，198，217
- chpasswd 命令，217
- chsh 命令，203，217，272

+   chmod 命令，655
+   命令，组合，671-673
+   cp 命令，655
+   d u 命令，656-657
+   find 命令，657-659
+   grep 命令，659-660
+   less 命令，660-662
+   ln 命令，663-664
+   locate 命令，664
+   ls 命令，664-666
+   man 命令，666
+   mkdir 命令，667
+   mv 命令，667
+   ps 命令，667-668
+   使用原因，650-651
+   rm 命令，668-669
+   screen 命令，673-674
+   tail 命令，669
+   top 命令，669-671
+   which 命令，671
+   客户端
+   光盘/DVD，通过图形客户端创建，155-157
+   客户端/服务器数据库模型，486
+   displayconfiggtk，61-63
+   电子邮件，107
+   Evolution，108-109
+   KMail，112
+   Thunderbird，111
+   Glade 客户端，607
+   GNOME，51
+   gs，171
+   IRC，115-117，211
+   KDE 监控，285
+   KDevelop 客户端，606-607
+   Pan 新闻客户端 新闻阅读器，119-120
+   终端，55
+   X，概述，53-54
+   xcpustate，283
+   CN（通用名称），514，517
+   代码，符号调试，605
+   编解码器 ()，167
+   冒号 (:) 作为切片，554
+   颜色（桌面），更改，32
+   列类型（SQL），490
+   列级权限（MySQL），498
+   组合命令，671-673
+   命令行，71-73
+   基本命令列表，651-652
+   /bin 和 /sbin 目录，78
+   cat 命令，652-653
+   cd 命令，653-655
+   光盘/DVD，从中创建，158-161
+   chmod 命令，655
+   命令，组合，671-673
+   cp 命令，655
+   数据库客户端，504
+   d u 命令，656-657
+   文件系统，导航，74-76
+   文件
+   压缩，77-78
+   编辑，78-79
+   管理，76-77
+   find 命令，657-659
+   grep 命令，659-660
+   /home 目录，79
+   less 命令，660-662
+   ln 命令，663-664
+   locate 命令，664
+   ls 命令，664-666
+   man 命令，666
+   mkdir 命令，667
+   Mono，612-614
+   mv 命令，667
+   /proc 目录，79-81
+   处理，Perl 编码示例，544
+   ps 命令，667-668

Python
条件语句，条件检查，556
字典，555
for 循环，556
函数，558-559
无限循环，557
安装，547
交互式解释器，548
列表，552-554
循环，557-558
数字处理，549-550
OOP，559-563
运算符重载，553
脚本执行，548
字符串，550-552
非官方脚本/插件网站，563
使用原因，650-651
rm 命令，668-669
screen 命令，673-674
软件管理，APT，681-685
tail 命令，669
top 命令，669，671
Ubuntu 更新，26-27
/usr 目录，81
/var 目录，81
which 命令，671
注释
PHP，571
shell 脚本，239
商业支持网站，750
通用日志格式（Apache Server），418
Common Unix Printing System。参见 CUPS（Common Unix Printing System）
CommuniGate Pro，472
表达式比较
pdksh shell 与 bash shell
文件比较，255-256
逻辑比较，256-257
数字比较，254-255
字符串比较，252-253
tcsh shell
文件比较，259-260
逻辑比较，260-261
数字比较，258-259
字符串比较，257
比较运算符（Perl），530
兼容性，检查硬件，733-734
编译
内核，700
BzDisk 指令，702
bzimage 指令，702
多个内核版本，698
保留当前内核版本，701
加速，702
故障排除，709
zImage 指令，702
语言，600
Compiz 窗口管理器，51-52
复合运算符（Perl），531
压缩
目录，tar 命令行备份软件，304
文件，77-78
CONCAT() 函数，492
在 Python 中连接字符串，552
条件语句
Perl，533-534
PHP，575-577
Python 条件检查，556
条件（PHP 循环），579
/configs 子目录（/usr/src/linux-2.6 目录），690
configure 脚本，构建 Apache Server 源代码，395

配置
  匿名 FTP 服务器，433
  Apache Server，配置指令，400
  AllowOverrides，405-406
  DirectoryIndex，403
  DocumentRoot，403
  Group，401-402
  Listen，401
  ServerAdmin，402
  ServerName，402
  ServerRoot，401
  User，401-402
  UserDir，403
  MPM，403-404
  磁盘配额，216-217
  Evolution，108-109
  文件备份，创建，288
  防火墙，632
  FTP 服务器，文件转换操作，445-447
  GNOME，51,52
  即时消息（使用 Pidgin），114-115
  IRC，115-117
  内核
    make config 实用程序，703
    make menuconfig 实用程序，703-704
    make xconfig 实用程序，704-705
    RAM 磁盘映像，708-709
    选择内核类型，693
    子部分，705-708
  KMail，112
  MySQL，496-497
  OpenOffice.org，126
    Calc，130-135
    办公工具，135-139
    Writer，127-129
  Pan 新闻客户端 新闻阅读器，119-120
  权限，90
    分配，91-92
    目录，92-94
    suid，94-95
  PostgreSQL，初始化数据目录，500-502
  打印，173-176
    基于 GUI 的打印机，174
    本地打印机，176，179-181
    root 账户，97-98
  RSS 阅读器，113-114
  Squid 代理服务器
    ACL，477-481
    客户端配置，476
    示例，482-483
    指定客户端 IP 地址，481-482
  Thunderbird，111
  Ubuntu
    CD/DVD 驱动器，44-45
    日期/时间重置，42-43
    防火墙，47
    首次更新，26-27
    调制解调器，39-41
    电源管理，41
    软件仓库，28
    sudo 命令，25
    故障排除，24
    无线网络，46-47
  Usenet 新闻组，117-118
  视频会议（使用 Edge），120-121
  vsftpd 服务器，429-432
  Windows 生产力应用程序，141
  wu-ftpd 服务器，432-444
  X Window System，60
    displayconfig-gtk 客户端，61-63
  xorg.conf 文件，63
  xinetd daemons 用于 wu-ftpd 服务器，428
  显示已连接用户信息（FTP 服务器），449-450

连接类型对话框，177
一致性（ACID），数据库合规性比较，495
控制台
  基本命令列表，651-652
  cat 命令，652-653
  cd 命令，653-655
  chmod 命令，655
  命令组合，671-673
  cp 命令，655
  du 命令，656-657
  find 命令，657-659
  grep 命令，659-660
  less 命令，660-662
  ln 命令，663-664
  locate 命令，664
  ls 命令，664-666
  man 命令，666
  mkdir 命令，667
  监控，275-276
    磁盘配额，282
    磁盘空间，281
    kill 命令，277-278
    优先级调度，278-280
    查看内存，280
  mv 命令，667
  ps 命令，667-668
  使用原因，650-651
  rm 命令，668-669
  screen 命令，673-674
  tail 命令，669
  top 命令，669-671
  which 命令，671
Console.WriteLine() 方法，615
常量（PHP），570
构造函数方法（Python），561
continue 关键字（Python），控制循环，558
控制中心对话框（kdm），64
控制结构。参见循环结构（Perl）

无控制器调制解调器，故障排除，734
convert 实用程序，149
在 Python 中转换数字类型，550
复制
  刻录 CD/DVD，154
  从命令行创建，158-161
  通过图形客户端创建，155-157
目录结构，tar 命令行备份软件，304
文件
  cp 命令，304-305，655
  mc 命令行文件管理软件，305
  远程服务器，357
  tar 命令行备份软件，303-304
列表，554
MBR，306
在服务器之间复制多个文件，358-359
远程文件，358
cp 命令，308，655
  配置文件备份，288
  复制文件，304-305
cp file1 file2 命令，77
CPAN（Comprehensive Perl Archive Network，综合 Perl 档案网络），539-541
cpio 命令，308
CPU（中央处理器），故障排除，736
crackers 与 hackers 的区别，626
CREATE DATABASE 语句
  MySQL，498
  PostgreSQL，502
CREATE 语句（SQL），490
CREATE USER 语句（PostgreSQL），503
createdb 命令（PostgreSQL），510
createuser 命令（PostgreSQL），510
cron 守护进程
  crontab 文件，读取，232
  反复运行任务，231-233
  调度任务，228

- crontab 文件
  - cron 守护进程，读取，232
  - 编辑，233
- CrossOver Office，141
- CUPS（Common UNIX Printing System，通用 UNIX 打印系统），171
  - 文档，172
  - 网络打印
    - 在局域网上启用，381
    - 创建打印机条目，383
    - SMB 打印，382
- cups 守护进程，174
  - 当前目录，通过 ls shell 命令列出文件，664-666
- 自定义 Ubuntu
  - 桌面
    - 背景，31
    - 颜色，32
  - 输入设备
    - 键盘布局，37-39
    - 键盘快捷键，37
    - 鼠标配置，39
  - 首选应用程序，35
  - 可移动驱动器和媒体，36
- CustomLog 指令（Apache Web 服务器），420
- cvs 命令，608

## D

- -d 文件比较运算符，255，259
- 守护进程
  - cups，174
  - 邮件，471
  - smbd，374
  - xinetd 守护进程，为 wu-ftpd 配置，428
- Dapper Drake，719
- 数据目录
  - MySQL，496-497
  - PostgreSQL，500-502

- 数据完整性，数据库比较，495-496
- 数据锁定，数据库比较，494
- 数据丢失，原因，288
- 数据镜像，293
- 数据绘图，133
- RDBMS 中的数据存储，487
- 数据库管理员。参见 DBA（数据库管理员）
- 数据库客户端
  - 命令行客户端，504
  - 本地 GUI 数据库访问，506
  - 中间件，507
- MySQL
  - 命令行客户端，508
  - 图形客户端，510
- PostgreSQL 命令行客户端，509
- SSH 数据库访问，505-506
- Web 数据库访问，507
- 数据库
  - 访问/权限问题，505
  - 客户端/服务器模型，486
  - 比较
    - ACID 合规性，495-496
    - 数据锁定，494
    - 过程语言，496
    - 速度，494
    - SQL 子查询，496
    - 触发器，496
  - 平面文件，486-487
- MySQL
  - 添加用户账户，499
  - 创建，498
  - 数据目录，496-497
  - 授权表，496
  - 授予/撤销权限，498-499
  - 安装，496-497
  - 权限，498
  - root 用户密码，497

770    数据库

PostgreSQL
- 创建数据库用户，502-503
- 创建数据库，502
- 删除数据库用户，503
- 退出 psql 命令行客户端，503
- 授予/撤销权限，504
- 初始化数据目录，500-502
- 安装，500
- RPM 发行版，500
- 启动 postmaster 程序，501

RDBMS
- 数据存储，487
- SQL 基础，489-493
- 表关系，488-489

- **date 命令**，42，278
- **date/time 重置**，42-43
- **DBA（数据库管理员）**，485-486
- **dd 命令**，308
- **de Icaza, Miguel**，50
- **deb 文件**，684
- **Debian Linux 发行版**，716

**调试**
- C/C++ 编程语言，604-605
- 符号调试，605

- **声明（PHP 循环）**，579
- **删除**
  - 批处理作业，230
  - 通过 rm shell 命令删除目录，668-669
  - 通过 rm shell 命令删除文件，668-669
  - PostgreSQL 数据库用户，503
  - 从 root 账户删除用户，98

- **拒绝服务（DOS）攻击**，80
- **deny 指令（Apache Server）**，406-407
- **依赖检查**，601
- **部署**，717
  - 硬件要求，731-732
  - 应用清单，739-740
  - 硬盘存储，733
  - 旧硬件，732
  - 测试兼容性，733-734
  - 故障排除，734-736

规划
- 业务应用，726-728
- 检查清单，730
- 安装，731
- 系统考虑，728-729
- 用户考虑，729

- **depmod 命令，模块化内核管理**，694
- **description 字段（ftpconversions 文件）**，447
- **designer 命令**，608
- **桌面**
  - 背景，更改，31
  - 颜色，更改，32

GNOME，51
- File Roller，299
- 优化，642

KDE，68
- ark 备份工具，300
- kdat 备份工具，300
- Konqueror 网页浏览器，为 Squid 代理服务器配置，476
- 优化，642

Xfce，69

- **析构方法（Python）**，561
- **开发版发行（内核）与稳定内核**，697
- **设备驱动**，692
- **Device 部分，xorg.conf 文件**，59
- **devices.txt 文件**，691
- **df 命令**，235，281
- **dhclient 命令**，335，338
- **DHCP（动态主机配置协议）**，319
  - 启动时激活，337
  - 优点/缺点，336
  - DHCP Server，339
  - dhcpd.conf 文件，340-342
  - 识别信息对，336
  - 安装时激活，337
IP 地址注册，337
LAN，341
租约，336
NT 服务器，341
服务器配置，339-341
DHCP Handbook 网站，The，342
DHCP Server，339
dhcpd.conf 文件，340-342
Dia（OpenOffice.org），125
拨号上网连接，手动配置，350-352
字典（Python），555
die 函数（Perl），542
数码相机
F-Spot，152-153
GIMP 146-147
捕获屏幕图像，150
图像文件格式，148-150
扫描仪，147-148
手持式，151
目录。另见文件
/bin，78
cd shell 命令，通过其更改，653-655
/etc，编辑文件，78-79
/etc/cup，172
文件，通过 ls shell 命令列出，664-666
/home，79
mkdir shell 命令，通过其创建，667
导航，75-76
权限，92-94
/proc，79-81
rm shell 命令，通过其删除，668-669
/sbin，78
tar 命令行备份软件
通过其压缩，304
通过其复制结构，304
/usr，81
/var，81
DirectoryIndex 配置指令（Apache Server），403
dirlst enable 设置（vsftpd 服务器默认设置），432
dirmessage enable 设置（vsftpd 服务器默认设置），432
dmesg 命令，故障排除 Ubuntu 配置，24
DN（Distinguished Names），514-515
do，until 循环（Perl），536
do，while 循环，536，581
文档，721-723
阅读，99-100
Documentation 目录（/usr/src/linux-2.6 目录），691

DocumentRoot 配置指令（Apache 服务器），403

文档
HOWTO，722
打印
配置，173-176
基于 GUI 的打印机，174
本地打印机，176，179-181
概述，171-173
Writer（OpenOffice.org），127-129

美元符号（$）
$* 内置变量，248
$# 内置变量，248
$? 内置变量，248
$0 内置变量，248

Don Becker 的 Linux 网卡状态、诊断和设置工具网站，326

DOOM 3，安装，186

DOS（拒绝服务）攻击，80

点分十进制格式，314

双与号（&&）数字比较运算符，260

双等号（==）字符串比较运算符，257

双竖线（||）数字比较运算符，260

双引号（"）在包含空格的 Shell 字符串中解析变量，249-250

DROP USER 语句（PostgreSQL），503

dropdb 命令（PostgreSQL），510

dropuser 命令（PostgreSQL），503，510

du Shell 命令，656-657

双主机无网卡网络，320

哑网关。参见网桥

虚拟接口，312

持久性（ACID），数据库合规性比较，496

DVD 驱动器
分配，检查，44-45
配置，44

DVD+RW/RW 驱动器，295

DVD
刻录，154
从命令行创建，158-161
使用图形客户端创建，155-157
DVD+RW，可重写限制，160
格式，159
播放器，169
Ubuntu 安装，11-12

dvi 命令，175

动态 IP 地址，346

## E

-e 文件比较运算符，259

e2fsck 命令，文件系统优化，641

echo 命令，80，235

Edge，视频会议，120-121

编辑
crontab 文件，233
/etc/modprobe.conf 文件，325
文件，78-79
FTP 服务器文件，430

/etc/resolv.conf 网络配置文件 773

- httpd.conf Apache 服务器配置文件，401-403
- 打印机设置，180-181
- 系统作业，231-232
- 文本编辑器，87
  - emacs，89-90
  - vi，88
- **edquota 命令**，216
- **elinks**，421
- **emacs 文本编辑器**，87-90，715
- **电子邮件**，107
  - 别名，Postfix MTA，465
  - 自动回复器，471
  - 守护进程，471
  - Evolution 电子邮件客户端，108-109，137，519
  - 转发，Postfix MTA，465
  - KMail，112
  - maildir 电子邮件目录格式，460
  - mbox 电子邮件目录格式，460
  - MDA，460
    - 选择，469
    - Fetchmail，465-469
    - Procmail，470
    - Spamassassin，470
    - Squirrelmail，470-471
    - 病毒扫描器，471
  - MTA
    - 选择，460
    - Exim，459
    - Postfix，458，462-465
    - Qmail，459-460
    - Sendmail，459
  - MUA，460-461
  - pine 目录格式，460
  - 以 root 身份读取，465
  - 发送/接收
    - 概述，457
    - 通过 Perl，540-541
  - Thunderbird，111，520

- **enable 命令**，175，181
- **加密**，无线网络，47
- **enscript 命令**，175
- **无限循环**，263
- **env 命令**，84
- **环境变量**
  - 登录，83-86
  - Shell 脚本，243
- **epiphany 命令**，454
- **-eq 数字比较运算符**，254
- **等号（=）**
  - 双等号（==）字符串比较运算符，257
  - 数字比较运算符，258
  - 字符串表达式运算符，252
- **错误检查**，Mono，616
- **转义字符**
  - 反斜杠（\）作为，251
  - 引号，单引号（'），250
- **转义序列**，PHP，571-572
- **escript 命令**，175
- **/etc 目录，编辑文件**，78-79
- **/etc/at.deny 文件**，230
- **/etc/crontab 文件**，231
- **/etc/cups 目录**，172
- **/etc/dhcp/dhcpd.conf 文件，DHCP 服务器配置**，339
- **/etc/dhcp/dhcpd.leases 文件**，339
- **/etc/fstab 文件**，215
- **/etc/host.conf 网络配置文件**，333
- **/etc/hosts 网络配置文件**，332
- **/etc/init.d/apache2 脚本，启动/停止 Apache 服务器**，398-399
- **/etc/inittab 文件，确定运行级别**，223
- **/etc/modprobe.conf 文件**，325，695
- **/etc/nsswitch.conf 网络配置文件**，333
- **/etc/passwd 文件**，206-207
- **/etc/printcap，手动编辑**，173
- **/etc/resolv.conf 网络配置文件**，333

- /etc/samba/smb.conf 文件，第370-373页
- /etc/services 网络配置文件，第332页
- /etc/squid/squid.conf 配置文件，第477页
- /etc/vsftpd.banned emails 配置文件，第430页
- /etc/vsftpd.chroot list 配置文件，第430页
- /etc/vsftpd.user list 配置文件，第430页
- Ethereal 工具，第282页
- Evolution 电子邮件客户端，第108-109、137、519页
- Exchange Server（微软）的替代方案，第471-473页
- 感叹号（!）
  - != 是不等于符号（SQL），第493页
  - 字符串比较运算符，第257页
  - 字符串表达式运算符，第252页
  - 逻辑比较运算符，第256页
  - 数字比较运算符，第260页
- 执行权限，第198-199页
- 执行运算符（PHP），第577页
- Exim MTA（邮件传输代理），第459页
- exit 命令，第82页
- exit 语句，第270页
- 表达式（比较），第77、234页
  - pdksh shell 与 bash shell
    - 文件比较，第255-256页
    - 逻辑比较，第256-257页
    - 数字比较，第254-255页
    - 字符串比较，第252-253页
  - tcsh shell
    - 文件比较，第259-260页
    - 逻辑比较，第260-261页
    - 数字比较，第258-259页
    - 字符串比较，第257页
- 外部命令（ftpconversions 文件），第446页
- 外部计算机攻击的定义，第625-626页
- extract() 数组函数，第586-587页
- 额外版本级别（内核），第697页

## F

- \-f 文件比较运算符，第255、259页
- F-Spot 照片管理，第152-153页
- 传真，第387页
- fclose() 文件函数，第589页
- FDDI（光纤分布式数据接口）网络，第321页
- Feisty Fawn，第719页
- Fetchmail MDA（邮件投递代理），第465页
  - 全局配置选项，第466页
  - 安装，第466页
  - 邮件服务器选项，第467页
  - 用户账户，第467-469页
- 光纤电缆，第323页
- 光纤 NIC（网络接口卡），第321页
- file 命令（用于确定文件压缩方法），第686页
- file_get_contents() 文件函数，第587页
- file_put_contents() 文件函数，第587页
- File Roller，第299页
- 文件系统
  - 托管，第744-745页
  - 导航，第74-76页
  - 优化，第640-641页
  - sync 命令，第640页
  - 虚拟，第79页
- 文件转换操作（配置 FTP 服务器），第445-447页
- 文件名通配符，第77页
- 文件。另请参阅目录
  - 访问权限（通过 chmod shell 命令更改），第655页
  - avi，第167页
  - 从备份恢复，第298页
  - 比较（表达式的比较），第255-256、259-260页
  - 压缩，第77-78页
  - 通过 cat shell 命令打印内容，第652-653页
  - 复制
    - cp 命令，第304-305页
    - cp shell 命令，第655页
    - mc 命令行文件管理软件，第305页
    - 服务器之间的多个文件，第358-359页
    - tar 命令行备份软件，第303-304页
  - 通过 ls shell 命令列出当前目录，第664-666页
  - 通过 rm shell 命令删除，第668-669页
  - DVIx，第167页
  - 编辑，第78-79页
  - /etc/fstab，第215页
  - /etc/passwd，第206-207页
  - FTP 服务器文件（编辑），第430页
  - 图形格式，第148-150页
  - 句柄，第589页
  - 头文件，第600页
  - 包含文件，第600页
  - 通过 ln shell 命令链接，第663-664页
  - 管理，第76-77页
  - mov 文件，第167页
  - 通过 mv shell 命令移动，第667页
  - MP3 文件，第163页
  - MPEG 文件，第163、167页
  - ogg，第163页
  - 通过 less shell 命令分页查看输出，第660-662页
  - 权限，第90、198-199页
    - 分配，第91-92页
    - 目录，第92-94页
    - suid/sgid，第94-95页
  - PHP 函数
    - fclose()，第589页
    - file_get_contents()，第587页
    - 文件句柄，第589页
    - file_put_contents()，第587页
    - filesize()，第589页
    - fopen()，第588-589页
    - fread()，第589页
    - fwrite()，第589页
  - ppd，第171页
  - 通过 tail shell 命令打印最后几行，第669页
  - qt，第167页
  - raw，第162页
  - 远程文件（复制）
    - 本地，第358页
    - 远程服务器，第358页
  - 复制到远程服务器，第357页
  - 搜索
    - 通过 locate shell 命令从索引搜索，第664页
    - 通过 find shell 命令搜索，第657-659页
  - 共享
    - NFS，第366-368页
    - Samba，第369-378页
  - 声音格式，第162-164页
  - 访问变量数据，第81页
  - 视频格式，第167页
  - wav，第163页
  - xorg.conf，第55-60、63页
- xorg.conf 文件中的 Files 部分，第57页
- filesize() 文件函数，第589页
- find 命令，第297、657-659页
- find2perl 实用程序，第544页
- finger 信息字段，第206页
- Firefox，第106、113、421、476页
- Firestarter，第47页
- 防火墙
  - 配置，第47、632页
  - 作为主机，第317页
- FireWire（IEEE-1394）驱动器，第295页
- Flash 插件（Macromedia），第168页
- 平面文件数据库，第486-487页
- flexbackup 备份软件，第302页
- 浮点数值（Python），第549页
- 软盘（系统启动），第307页
- fopen() 文件函数，第588-589页
- for 循环，第579页
  - Perl，第534页
  - Python，第556-557页
- for 语句，第261-262页
- foreach 循环，第535、580页
- 格式化
  - GIMP，第146页
    - 捕获屏幕图像，第150页
    - 图形文件格式，第148-150页
    - 扫描仪，第147-148页
  - 用户组，第199-202页
  - 密码，第206页
    - /etc/passwd 文件，第206-207页
    - 影子密码，第207-209页
    - 系统策略，第206页
    - 用户，第209页
  - 声音，第162-164页
  - 电子表格（OpenOffice.org），第132页
  - 用户账户，第195页
    - 文件权限，第198-199页
    - 超级用户/root 用户，第196-198页
    - UIDs/GIDs，第198页
    - 用户
      - 添加，第203-204页
      - 监控，第204-205页
      - 工具，第202-203页
  - 生产力应用程序，123
    - OpenOffice.org，124-125
      - Calc，130-135
      - 配置，126-127
      - 办公工具，135-139
      - Writer，127-129
    - Windows，141
  - 生产力套件，141-142
  - 编程语言
    - C 编程语言，开发，599-600
    - C/C++
      - 开发，600
      - 图形化开发工具，606-607
      - 项目管理工具，600-605

project management tools, C/C++ programming language
autoconfig，603
debugging tools，604-605
make 命令，600-602
Subversion 系统，603-604
Project Planner（GNOME Office），139
Promiscuous 模式，328，631
提示符，交互式解释器（Python），548
printf/fax/scan 设备，387
printenv 命令，84
打印机名称对话框，177
打印机
  命令，388
  驱动程序/打印机支持交叉引用网站，179
  故障排除，387-388
[printers] 部分（/etc/samba/smb.conf 文件），370，373
打印
  命令位置，通过 top shell 命令，671
  配置，173-175
    基于 GUI 的打印机，174
    本地打印机，176，179-181
  磁盘使用情况，du shell 命令，656-657
  文件内容，cat shell 命令，652-653
  基于 GUI 的打印机，174
  文件的最后几行，通过 tail shell 命令，669
  Mono 参数，615
  网络打印机
    CUPS GUI，383
    LAN，启用，380-381
    SMB 打印，382
  概述，171-173

## programming languages

+   参考，182
+   资源使用情况，通过 top shell 命令，669-671
+   优先级调度，控制进程，278-280
+   权限
+     授予，210-215
+     MySQL，498-499
+     PostgreSQL，授予/撤销，504
+   /proc 目录，79-81
+   过程式语言，数据库比较，496
+   进程 ID（PIDs），276
+   进程列表视图，283
+   进程
+     控制台监控，275-276
+     磁盘配额，282
+     磁盘空间，281
+     kill 命令，277-278
+     优先级调度，278-280
+     查看内存，280
+     图形化，系统管理工具，282-285
+     列出，通过 ps shell 命令，667-668
+   Procmail MDA（邮件投递代理），470
+   生产力应用程序，123
+     OpenOffice.org，124-125
+       Calc，130-135
+       配置，126-127
+       办公工具，135-139
+       Writer，127-129
+     Windows，141
+   生产力套件，141-142
+   编程语言
+     C 编程语言，开发，599-600
+     C/C++
+       开发，600
+       图形化开发工具，606-607
+       项目管理工具，600-605

## Q - R
-qe 数字比较运算符，254
Qmail MTA（邮件传输代理），459-460
qt 文件，167
-qt 数字比较运算符，254
Quake 4，安装，188-189
查询缓存，MySQL 优化，646
问号（?），shell 模式匹配搜索，236
队列（打印），创建，177-180
问号（?），shell 模式匹配搜索，236
quotacheck 命令，216
quotaoff 命令，216

quotaon 命令, 216

引号（''）
双引号（'"'），在含嵌入空格的 shell 字符串中解析变量，249-250
保持未展开变量的 shell 字符串，250

-f 文件比较运算符，255, 259

广播电台（因特网），144

RAID 阵列，293

RAM 磁盘映像（内核），708-709

RARP（反向地址解析协议），319

原始文件，162

rc.sysinit 脚本，222

RDBMS（关系数据库管理系统）
数据存储，487
SQL
命令，空白字符，490
CREATE 语句，490
创建表，489-491
INSERT 语句，491
向表中插入数据，491
保留关键字，491
从数据库检索数据，492-493
SELECT 语句，492
表关系，488-489

读取权限，198-199

读取手册页，通过 man shell 命令，666

阅读文档，99-100

重启，99

恢复模式，启动进入，308

恢复计划，633-634

重定向，234, 237

redo 语句（Perl），536

引用（PHP），570

正则表达式，415, 537

reject 命令，175

关系数据库。参见 RDBMS（关系数据库管理系统）

中继电子邮件，Postfix MTA，463

远程访问
基于密钥的登录，359
登录，82,83
SSH 服务器，356-359
Telnet 服务器，配置，355
VNC，361-362
XDMCP 361

远程客户端，X Window 系统支持，54

远程文件，复制，358

远程服务器
将文件复制到，357
安全性，359-360

可移动驱动器和介质，36

可移动存储介质，295

资源使用情况，通过 top shell 命令打印，669-671
资源（PHP），568
恢复
从备份恢复文件，tar 命令行备份软件，298
MBR，306
Restricted Drivers Manager，185
从 SQL 数据库检索数据，492-493
投资回报率（ROI），717
REVOKE 语句
PostgreSQL，504
SQL，499
撤销权限
MySQL，498-499
PostgreSQL，504
Rhythmbox，144-145
翻录音乐曲目，154
rm file 命令，77
rm shell 命令，668-669
rmdir dir 命令，77
rmmod 命令，模块化内核管理，694
ROI（投资回报率），717
根账户，96-99
重启，99
远程服务器安全性，360
系统关机，98-99
用户，97-98
根权限，授予，212-213
根用户（LDAP），196-198
分配密码给，515
定义，514
根用户（MySQL），密码，497
route 网络配置工具，330-331
路由器，324
rpm 命令，构建 Apache 服务器源代码，396
rsh shell，234
RSS 阅读器，113-114
Run() 方法，619
run-parts 命令，231
运行级别，64, 220
更改，225
默认运行级别，启动到，223
定义，222
非默认运行级别，启动到，224
故障排除，226-227
运行时错误（内核），故障排除，710

## S

-s 文件比较运算符，255
s2p 过滤器，544
Samba
连接状态报告，374
安装，369
通过 /etc/samba/smb.conf 文件手动配置，370-373
挂载共享，375
SMB 协议，369
smbd 守护进程，启动，374
SWAT，369, 375-378
通过 testparm 命令测试，373
包含入站和出站日志记录的示例 /var/log/xferlog 文件清单（20.5），454
SANE（扫描仪访问现在易用），147
/sbin 目录，78
/sbin/ifconfig 网络配置工具，327-329
/sbin/route 网络配置工具，330-331
标量（Perl），528
scanbus 命令，154
扫描仪访问现在易用（SANE），147
扫描仪，147-148, 387
调度程序，172
调度优先级，控制进程，278-280

调度任务
at 命令，228-230
batch 命令，229-230
cron 守护进程，231-233
方案，选择分区，744
施瓦茨变换，543
scp 命令，308, 357-358
屏幕抓取，150
Screen 部分，xorg.conf 文件，60
screen shell 命令，673-674
脚本目录（/usr/src/linux-2.6 目录），692
SCSI 磁盘驱动程序，693
Seamonkeychat，116
select 语句，265-266
SELECT 语句（SQL），492
选择
备份策略，294
内核类型，693
分区方案，744
SendAsync() 方法，619
通过 Perl 发送电子邮件，540-541
sendmail 命令（Perl），539-540
Sendmail MTA（邮件传输代理），459
序列，切片，551
串口调制解调器，检测/配置，39
ServerAdmin 配置指令（Apache 服务器），402

ServerLayout 部分，xorg.conf 文件，56
ServerName 配置指令（Apache 服务器），402
ServerRoot 配置指令（Apache 服务器），401
服务器
匿名 FTP 服务器，配置，433
FTP 服务器
管理命令，449-454
Bsdftpd-ssl 服务器，425
选择，423-424
已连接用户信息，449-450
文件转换操作，445-447
NcFTPd 服务器，424-425
软件包，424
LDAP 配置，514-515
远程，安全性，359-360
SSH 服务器
配置，356-357
禁用 SSH1，357
ftp 命令，357
rcp 命令，357
scp 命令，357-358
sftp 命令，358-359
ssh-keygen 命令，359
与 Telnet 服务器对比，356
Telnet 服务器，355-356
vsftpd 服务器，424
匿名访问控制，430
配置，429-432
Web。另请参阅 Apache 服务器
Sun ONE，420
Zeus，网站，421
Zope，网站，420
wu-ftpd 服务器
配置，432-444
xinetd 守护进程配置，428
X，概述，53-54
服务，打印
配置，173-176
基于 GUI 的打印机，174
本地打印机，176，179-181
会话写入，DVD 刻录，160
设置对话框，180
setup 命令，175
sftp 命令，358-359，454
sgid 权限，94-95
sh shell，234
影子密码文件 ftp 用户条目列表（20.1），427
影子密码，207-209，426-427
shar 命令，272
shebang 行（#!），241-243，527
SHELL 行（/etc/crontab 文件），231
shell
通过 Perl 访问，537-538
bash，233-234，252
基本命令列表，651-652
break 语句，270
case 语句，268-270
cat 命令，652-653
cd 命令，653-655
更改，241
chmod 命令，655
命令行
后台处理，238
输入/输出重定向，234，237
作业控制命令，235
模式匹配，234-236
管道（|），234，238
位置参数，244-246
命令，组合，671-673
表达式比较，test 命令
文件比较，255-256
逻辑比较，256-257
数字比较，254-255
字符串比较，252-253
cp 命令，655
du 命令，656-657
无限循环，263
转义字符，\（反斜杠）作为，251
exit 语句，270
Fedora Core shell 列表，233-234
文件，管理，76-77
find 命令，657-659
for 语句，261-262
grep 命令，659-660
if 语句，267-268
作业控制命令，234
ksh，234
less 命令，660-662
ln 命令，663-664
locate 命令，664
ls 命令，664-666
man 命令，666
man 手册页，234
mkdir 命令，667
mv 命令，667
pdiksh，234
select 语句，265-266
test 命令，252
位置参数，243
位置参数，244-246
ps 命令，667-668
使用原因，650-651
repeat 语句，265
rm 命令，668-669
rsh，234
screen 命令，673-674
脚本
内置变量，243，248
命令作为脚本，239
环境变量，243
执行，240
函数，270-271
位置参数，244-246
使用原因，238
shebang 行（#!），241-243
特殊字符列表，248-249
startx 命令，239
任务，自动化，246-247
测试，247
木马脚本，241
用户变量，243
变量，243-244
编写，239
select 语句，265-266
sh，234
shift 语句，266
包含嵌入空格的字符串，解析其中的变量，249-250
包含未展开变量的字符串，保留，250
tail 命令，669
tcsh，234
repeat 语句，265
test 命令，257-261
top 命令，669-671
until 语句，264-265
which 命令，671
while 语句，263-264
zsh，234，251
shift 语句，266
快捷方式
cd 命令，74
键盘，37
shred 命令，663
shuffle() 数组函数，585
shutdown 命令，98-99，444
关机文件，魔法 cookie，444-445
关闭 Ubuntu，21
简单备份策略，292
单引号（'），包含未展开变量的 shell 字符串，250
Skolnick, Cliff，Apache 服务器开发，391
slappasswd 工具，515
Slashdot.org 网站，643
切片（），在 Python 中复制列表，554
切片（序列），551
小型企业备份策略，291
小型办公室备份策略，291
小型办公室/家庭办公室（SOHO），716，720
智能网关。参见路由器
智能主机，Postfix MTA，463
SMB（会话消息阻塞）协议，369，382
smbclient，454
smbclient 命令，175，374，454
smbd 守护进程，启动，374
smbprint 命令，175
smbspool 命令，175
smbstatus 命令，Samba 连接状态报告，374
SMP（对称多处理器），719
SMTP（简单邮件传输协议），MDA，460
套接字，331
软链接。参见符号链接
软件
备份
afio，302
Amanda 备份应用程序，301-302
ark，300
cdbbackup，302
File Roller，299
flexbackup，302
kdat，300
tar，297-298
FTP 软件，安装，425-426
管理
添加/删除应用程序，677
APT，681-685
Synaptic，678-680
tar 包，686
更新管理器，680-681
软件仓库，配置，28
软件调制解调器，Linux 支持，350
SOHO（小型办公室/家庭办公室），716，720
声卡，161-164
源代码
检查，604
内核源代码，位于 /usr/src/linux-2.6 目录，692
源代码树（内核），makefiles，690
sox 命令，164
Spamassassin MDA（邮件投递代理），470
速度，数据库比较，494
split 命令，604，608
split() 方法，Python 列表，555
电子表格，Calc（OpenOffice.org），130-135
字符串
在 Python 中为其赋值，550
Python 中的内置方法，552
比较
表达式比较，252-253，257
运算符（Perl），列表，530
在 Python 中连接，552
Python 中的不可变序列，550
在 Python 中索引，551
Perl 常量，532
PHP 572-573，582-585
在 Python 中重复，552
搜索，grep shell 命令，659-660
存储在 shell 脚本变量中，244
去掉后缀，445
去掉前缀，445
strlen() 字符串函数，582
strpos() 字符串函数，584-585
StumbleUpon，107
su 命令，210-212，217
子级别编号部分（内核），697
子网掩码。参见 netmasks
子网划分，318
子查询（SQL），数据库比较，496
substr() 字符串函数，583
Subversion 系统（C/C++ 编程语言），603-604
sudo 命令，25，97，212-213，217
suid 权限，94-95
汇总数据（Calc），133
Sun ONE Web 服务器，420
超级用户，196-198
超级用户账户，96-99
支持（商业），网站，750
svg 图形文件格式，149
svn 命令，608
SWAT（Samba Web 管理工具），369，375-378
switch/case 块（PHP），578-579

交换机，上行端口，323

开关列表，gcc（GNU C 编译器），605

符号调试，605

符号链接（内核），更改，698

symlinks，663-664

对称多处理器（SMP），719，736

SYN 泛洪，80

SYN Stealth 扫描（Nmap），628

Synaptic，687

查看已安装软件包列表，749

软件管理，678-680

sync 命令，文件系统同步，640

sysctl 命令，Linux 内核，710

优化，641-642

安全，625

sysrq.txt 文件，691

授予系统管理员权限，210-215

系统从通用软盘启动，307

系统作业，231-232

系统日志

指令，440-441

通过 Perl，526

系统监控工具，280，285

系统密码策略，206

系统救援，306-307

系统服务

系统监控工具，275

基于控制台的监控，275-276

磁盘配额，282

磁盘空间，281

kill 命令，277-278

优先级调度，278-280

查看内存，280

图形化进程，282-285

KDE，285

## T

表缓存，MySQL 优化，647

表级权限（MySQL），498

表

RDBMS 中的关系，488-489

SQL 表，489-491

tail shell 命令，669

磁带归档，77

磁带驱动器备份，295

tar 命令，77，295，298，308

tar 命令行备份软件

压缩目录，304

复制目录结构，304

复制文件，303-304

任务，自动化
调度任务，228-233
shell 脚本，246-247
#!（shebang 行），241-243
内置变量，243，248
命令作为，239
环境变量，243
执行，240
位置参数，244-246
使用原因，238
特殊字符，列表，248-249
存储以供系统范围访问，241
测试，247
特洛伊脚本，241
用户变量，243
变量，243-244
编写，239
shells
反斜杠（/）作为转义字符，251
反引号（`），用输出替换字符串，251
更改，241
Fedora Core shells 列表，233-234
作业控制命令，234
维护包含未展开变量的 shell 字符串，250
man 手册页，234
在包含嵌入空格的字符串中解析变量，249-250
shell 命令行，后台处理，235-238，244-246
系统服务
更改运行级别，225
手动启动/停止，228
故障排除运行级别，226-227
系统服务在启动时的操作
启动，222-224
init 脚本，224-225
启动引导加载过程，220-221
加载 Linux 内核，221

泰勒，戴维，161
TCP/IP（传输控制协议/互联网协议），网络，313
类，315
IP 伪装，316
IPv4 地址，314-316
IPv6 地址，316
端口，317
tcpdump 命令，混杂模式，631
tcsh shells，234，265
表达式比较
文件比较，259-260
逻辑比较，260-261
数字比较，258-259
字符串比较，257
test 命令
文件比较，259-260
逻辑比较，260-261
数字比较，258-259
字符串比较，257
telinit 命令，运行级别，更改，225
Telnet 服务器，335-336
终端客户端，55
终端多路复用器。参见 screen shell 命令
终端，多终端，673-674
三元运算符（PHP），576
test 命令
文件比较，255-256，259-260
逻辑比较，256-257，260-261
数字比较，254-255，258-259
字符串比较，252-253，257
测试
硬件兼容性，733-734
程序（内核），在 /usr/src/linux/2.6 目录中，692
shell 脚本，247
testparm 命令，测试 Samba，373
文本，Writer（OpenOffice.org），127-129

文本编辑器，87
  emacs，89-90
  vi，88，544
文本换行，shell 脚本，239
基于文本的控制台登录，82
thinkjettopbm 命令，175
Thunderbird 电子邮件客户端，111，520
tif 图形文件格式，149
time 命令，278
time-admin 客户端，时间/日期设置，43
时间/日期重置，42-43
timewarp，205
Tivo，169
令牌环网卡（NIC，网络接口卡），320
工具
  命令行
    /bin 和 /sbin 目录，78
    压缩文件，77-78
    编辑文件，78-79
    /home 目录，79
    管理文件，76-77
    浏览文件系统，74-76
    概述，71-74
    /proc 目录，79-81
    /usr 目录，81
    /var 目录，81
data pilots，133
ethereal，282
GKrellM，282
gnome-nettool，282
gnome-system-monitor，283
组管理，200-203
kdf，285
ksysguard，285
Mono，612-614
netpbm，149
system-config-printer，174-177
系统监控
  基于控制台的监控，275-277
磁盘配额，282
磁盘空间，281
图形化进程，282-285
KDE，285
kill 命令，277-278
优先级调度，278-280
查看内存，280
vmstat，280
vncviewer，282
top 命令，279，669-671
Torvalds，Linus，690，715
touch 命令，90
跟踪，函数时间，605
Transmeta 公司，715
触发器，数据库比较，496
trim() 字符串函数，582
Tripwire 安全工具，630-631
特洛伊木马，630
特洛伊脚本，241
故障排除
  硬件，734-736
  Internet 连接，352-353
  内核编译，709
  内核运行时错误，710
  网络连接，324
  网卡（NIC），326
  打印机，387-388
  运行级别，226-227
  Ubuntu 配置，24
tune2fs 命令，文件系统优化，640
TuxMobil-Mobile Unix 网站，753
电视硬件，164-166
twm（标签窗口管理器），67
类型转换，Python 数字类型转换，550
types 字段（ftponversions 文件），446

## U

- Ubuntu
  - 64 位，721
  - 商业应用程序，726-728
  - 配置
    - CD/DVD 驱动器，44-45
    - 日期/时间重置，42-43
    - 防火墙，47
    - 首次更新，26-27
    - 调制解调器，39-41
    - 电源管理，41
    - 软件仓库，28
    - sudo 命令，25
    - 故障排除，24
    - 无线网络，46-47
  - 自定义
    - 桌面背景，31
    - 桌面颜色，32
    - 输入设备，37-39
    - 鼠标配置，39
    - 首选应用程序，35
    - 可移动驱动器和介质，36
  - 部署，规划，726
  - 文档，721-723
  - 用于商业，719-720
  - 用于家庭使用，720
  - 历史，718
  - 安装
    - 基于 CD 的安装，11-12
    - CD-ROM 要求，11
    - 发行版选项，10
    - 基于 DVD 的安装，11-12
    - 首次更新，19
    - 从 CD-ROM 安装，741-742
    - GRUB，11
    - 硬件要求，10-11
    - 分区，10-11, 15, 742-745
  - 密码，16
  - 规划，731
  - 准备，740-741
  - 分步指南，13-15, 18
  - 网络，314
  - 概述，718
  - PPC，721
  - 部署前检查清单，730
  - 救援光盘，306
  - 关机，21
  - 系统注意事项，728-729
  - 用户注意事项，729
  - 版本，719
- UDP（通用数据报协议），313
- UID（用户 ID），198
- 未展开的变量（shell），250
- 单播寻址，319
- 芬兰赫尔辛基大学，715
- Unix，备份级别，292
- unless 条件语句（Perl），534
- 虚幻竞技场 2004，安装，187-188
- unset() 函数，590
- until 循环（Perl），536
- until 语句，264-265
- 更新管理器
  - 软件管理，680-681
  - Ubuntu 首次更新，19
- update-manager，软件包更新，687
- 更新
  - 网络安全，634
  - 软件管理，680-681
  - Ubuntu，首次更新，19, 26-27
- 升级 Apache 服务器，文件位置，394
- 上行链路端口，323

### USB

- **USB（通用串行总线）**
  - 打印机，故障排除，388
  - 扫描仪，148
  - 故障排除，735
- **use 函数（Perl），539**
- **已用内存，查看，280**
- **Usenet，帖子（Perl 编码示例），542-543**
- **Usenet 新闻组，117-118**
- **Usenet 新闻组网站，754-755**
- **用户账户，72**
  - Fetchmail，配置，467-469
  - MySQL，添加，499
- **User 配置指令（Apache 服务器），401-402**
- **用户目录，保护内容，79**
- **用户 ID（UID），198**
- **用户信息**
  - FTP 服务器，显示，449-450
  - wu-ftpd 服务器，配置，436-440
- **用户信息指令（ft_paccess 配置文件）**
  - 显示管理员电子邮件地址，440
  - 显示文件，437-439
  - 显示序言横幅，436-437
  - 最后修改日期通知，440
- **用户作业，231-232**
- **用户变量（shell 脚本），243**
- **useradd -D 命令，202**
- **useradd -G 命令，200**
- **useradd 命令，97, 202, 217**
- **userdel 命令，203**
- **UserDir 配置指令（Apache 服务器），403**
- **usermod -G 命令，200**
- **usermod 命令，203, 217**
- **用户**
  - 账户
    - 创建，195-196
    - 文件权限，198-199
  - 超级用户/根用户，196-198
  - UID/GID，198
  - 磁盘配额，215-217
  - FTP 用户，426-428
  - 管理，202-205
  - 修改，210-212
  - 密码，管理，209
  - 特权，授予，210-215
  - 根账户，97-98
- **/usr 目录，55, 81**
- **/usr/bin 目录，55**
- **/usr/include 目录，55**
- **/usr/lib 目录，55**
- **/usr/lib/modules 目录，55**
- **/usr/lib/X11 目录，55**
- **/usr/src/linux-2.6 目录**
  - arch 目录，692
  - /configs 目录，690, 701
  - Documentation 目录，691
  - 内核源代码，692
  - 内核测试程序，692
  - scripts 目录，692
  - 声卡文档目录，162
- **/usr/X11/man 目录，55**
- **UTP（非屏蔽双绞线）电缆，322**

## V

- values 函数，Perl 哈希，529
- van Rossum，Guido，547
- /var 目录，81
- var dump() 函数，591-592
- /var/log/vsftpd.log 配置文件，430
- /var/log/xferlog 文件，字段列表，453-454
- /var/spool/cron 目录，232
- 变量数据文件，访问，81
- 变量替换（PHP），573

variables
  Python 中的类对象变量，560
  环境，登录，83-86
  交互式解释器（Python），在其中处理，548
  Mono，创建，615-616
  Perl 变量，528-529
  PHP 变量，566
    数组，567-569
    资源，568
    类型，567
  变量替换，573
shell scripts
  内置，243，248
  环境，243
  存储字符串，244
  用户，243
  值，243-244
shells，未展开的变量，250
Vaults of Parnassus 网站，563
versions
  Linux，716
  Ubuntu，719
vi 命令，272
vi 文本编辑器，88，544
video
  驱动程序，安装，184-185
  DVD/视频播放器，169
  格式，167
  个人视频记录器，168
  电视硬件，164-166
  观看，167-168
video cards，X Window System 更新，60
videoconferencing with Edge，120-121
VideoLAN HOWTO，169
viewing
  批处理作业编号，230
  内置变量，248
  显示管理器，63，66
  内存，280
  视频，167-169
vim，87
virtual file systems，79
virtual hosts，Apache Server，416-418
virus scanners，471，632
viruses，Linux 安全，632
visudo 命令，213
vmstat 工具，280
VNC（Virtual Network Computing），361-362
vncviewer 工具，282
volume，修改，162-163
vsftpd 命令，454
vsftpd 服务器，424
  控制匿名访问，430
  配置，429-432
vulnerability assessments（security），627-628
W
w 命令，235
-w 文件比较运算符，255，259
Wall，Larry，608
wallpaper，更改，31
war driving，629
wav 文件，163
weaknesses，评估（安全），627-628
Web searches
  Google 网站，749
  技巧，748
Web servers
  Apache
    构建源代码，395-396
    开发，391-392
    文档网站，392
    下载，392-393
    文件系统访问控制，410
    优化，642-644
    快速入门指南，396-397
    运行时配置，400-406
    安全报告网站，393
    源代码网站，395
    启动/停止，397-399
    升级，文件位置，394
    使用统计，391
    版本信息，392-393
    虚拟主机，416-418
  Sun ONE，420
  通过 allow/deny 指令
    文件系统身份验证，407-409
  安装，393-396
  Internet 安全，406
  日志记录，418-420
  mod_access 模块，411
  mod_alias 模块，411
  mod_asis 模块，411
  mod_auth 模块，412
  mod_auth_anon 模块，412
  mod_auth_dbm 模块，412
  mod_auth_digest 模块，412
  mod_autoindex 模块，413
  mod_cgi 模块，413
  mod_dir 模块，413
  mod_env 模块，413
  mod_expires 模块，413
  mod_headers 模块，413
  mod_include 模块，414
  mod_info 模块，414
  mod_log_config 模块，414
  mod_mime 模块，414
  mod_mime_magic 模块，414
  mod_negotiation 模块，414
  mod_proxy 模块，414
  mod_rewrite 模块，414
  mod_setenvif 模块，415
  mod_ssl 模块，415
  mod_speling 模块，415
  mod_status 模块，415
  mod_unique_id 模块，415
  mod_userdir 模块，415
  mod_usertrack 模块，416
  mod_vhost_alias 模块，416
  Zeus，网站，421
  Zope，网站，420
webcam 命令，454
welcome.msg 文件，439
WEP 加密，47
whatis 命令，76
WHERE 子句，SELECT 语句，492
WHERE 语句（SQL），493
whereis 命令，76，86
which shell 命令，671
while 循环，535，557-579
while 语句，263-264
whitespace，SQL 命令，490
wildcard searches，77。另见 pattern-matching
window managers，修改，66-67
Windows
  游戏，使用 Cedega 游玩，190-191
  生产力应用程序，141
  Wine，141
WinModems，笔记本配置，40-41
wireless networking，321
  优点，344
  选择可用协议，344-345
  配置，46-47
  加密，47
  安全，628-629
  支持，342-343
  war driving，629
wish 命令，242
WITH PASSWORD 段（CREATE USER 语句），503
Wolfenstein: Enemy Territory，安装，188-189
word processors，Writer（OpenOffice.org），404
WPA Personal 加密，47
write permissions，198-199
WriteLine() 方法，615
Writer（OpenOffice.org），124，127-129
writing，shell scripts，239
wu-ftpd 服务器
  配置，432-444
  权限控制，配置，442-443
  系统日志，配置，440-441
  用户信息，配置，436-440
  xinetd 守护进程，为其配置，428

## X
-x 文件比较运算符，255，259
X Window System
  应用，54-55
  组件列表，56
  组件，55
  配置，60-63
  显示管理器，54
  分布式处理，54
  发行版组件，54
  特性，54
  硬盘需求，55
  Module 部分，58
  Monitor 部分，59
  概述，53-54
  参考，70
  ServerLayout 部分，57
  启动，63，66
  通过显示管理器，64
  xorg.conf 文件，55-60
X Window System 网站，753
X-Chat，116
x-x，shell 模式匹配搜索，236
X.Org Foundation，716
X11。参见 X Window System
xcpustate 客户端，283
xdm 显示管理器，应用，66
XDMCP（X Display Manager Control Protocol），361
Xfce 桌面，69，642
Xine，169
xinetd 守护进程，wu-ftpd 服务器，428
xorg.conf 文件
  元素，55
    Device 部分，59
    Files 部分，57
    InputDevice 部分，58
    Module 部分，57
    Monitor 部分，58
    Screen 部分，60
    ServerLayout 部分，56
  X Window System 配置，63
Xsane 扫描仪，148
xxx，shell 模式匹配搜索，236

## Y - Z
-z
  文件比较运算符，259
  字符串表达式运算符，252
Zeus Web server 网站，421
zImage 指令，内核编译，702
Zope Web server 网站，420
zsh shell，234

## DVD 上有什么

该书的 DVD 包含 Ubuntu 7.10 的二进制版本——相当于至少四张 CD。

## 桌面环境

- X.Org 7.2.5
- GNOME 2.20.0

## 无障碍功能

- GNOME 屏幕键盘
- 屏幕阅读器和放大镜

## 附件

- Alacarte 菜单编辑器
- Ark
- 计算器
- 字符映射表
- 词典
- GVim 文本编辑器
- KAlarm
- KArm
- Katapult
- KCalc
- KjbViewer
- Klipper
- KNotes
- KPager
- KPilot
- KSig
- KTip
- Mousepad
- 屏幕截图
- SpeedCrunch
- 终端
- 文本编辑器
- Tomboy 笔记
- Xarchiver
- Xfburn
- Xfce 4 应用查找器

## 教育

- Kalzium
- Kanagram
- Kbruch
- KEduca
- KHangMan
- Kig
- KLatin
- KLettres

## 教育（续）

- KmPlot
- KPercentage
- KStars
- KTouch
- KTurtle
- Kverbos
- KVocTrain
- GROMMACS

### 游戏

- Ace of Penguins
- Atlantik
- Atlantik Designer
- Atomix
- Chess
- 教育套件 gcompris
- 四子棋
- FreeCell 扑克牌
- KAsteroids
- KAtomic
- KBackgammon
- KBattleship
- KBlackBox
- KBounce
- Kenolaba
- KFouEggs
- KGoldrunner
- KJumpingCube
- Klickety
- KMahjongg
- KMines
- Kolf
- Konquest
- KPoker
- KReversi
- KSirtet
- KSmileTris
- KSnakeRace
- KSokoban
- KSpaceDuel
- KTron
- KWin4
- Lieutenant Skat
- Mahjongg

## 游戏（续）

- Mines
- Patience
- Potato Guy
- Robots
- SameGame
- Shisen-Sho
- Sudoku
- TuxMath
- TuxTyping
- Zatacka

## 图像

- Dia
- digiKam
- 文档查看器
- FontForge
- F-Spot 照片管理器
- GIMP 图像编辑器
- GNU Paint
- GQview
- gThumb 图像查看器
- Gwenview
- 图像查看器
- Inkscape 矢量插画师
- KFaxView
- KGhostView
- Kooka
- KPDF
- Krita
- KSnapshot
- OpenOffice.org 绘图
- QCad
- Scribus
- XaoS
- XSane 图像扫描仪

## 互联网

- Akregator
- BitTorrent
- Bluetooth
- Bluetooth OBEX 客户端
- Bluetooth OBEX 服务器
- Ekiga 软电话
- Epiphany 网页浏览器

```
