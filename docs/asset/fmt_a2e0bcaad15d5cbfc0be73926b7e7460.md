
# 在交互式使用时获取帮助

最后，你可以通过使用实时 Linux 发行版（例如 `LNX Bootable Business Card`，可用处）启动系统，在安装前准备分区。

# 选择分区方案

你对特定分区方案的选择将取决于 Ubuntu 如何使用。对于旨在扩展、更大容量或托管更多软件或用户的系统，可以使用单独分区来托管 Linux 文件系统的各个部分。

如果 Linux 是唯一的操作系统，你可以根据安装类型自动创建分区。如果你计划拥有双启动系统，你必须在安装之前或期间手动对硬盘进行分区。Linux 最简单且基础的分区方案需要原生根分区和一个交换分区。对于具有 12GB 存储和 512MB 内存的单硬盘系统，方案如下：

| 硬盘分区 | 挂载点 | 大小 |
|---|---|---|
| `/dev/sda1` | `/` | 10.7GB |
| `/dev/sda2` | swap | 1GB |

在运行 Windows 的系统上，方案如下：

| 硬盘分区 | 挂载点 | 大小 |
|---|---|---|
| `/dev/sda1` | `/media/dos` | 4GB |
| `/dev/sda2` | | 7.7GB |
| `/dev/sda3` | swap | 1GB |

# 在单独分区上托管 Linux 文件系统的部分

这些单独分区的候选包括：

- `/home`——用户在他们的目录下存储了数百兆字节的数据。这些是重要数据，甚至超过系统本身。使用单独分区（在不同的卷上）来存储这些用户数据有助于更容易找到数据并隔离用户和系统数据。你必须预先为用户分配多少存储空间。
- `/opt`——用于存放额外软件包的家目录级目录，该目录可以有自己的分区或远程文件系统。Ubuntu 不会填充此目录，但它可能会被以后安装的其他软件包使用。根据要安装的应用程序，1 兆字节的存储空间应该是足够的。
- `/tmp`——如果执行了磁盘配额，用户可以使用此目录作为临时存储空间；因此，它可以被放置在单独的分区。此目录可以小到 100MB。
- `/usr`——此目录保存了 Ubuntu 系统上几乎所有的软件，如果增加了额外的存储空间，它可能会变得很大，特别是在工作站配置上。使用单独分区是有意义的。完整安装或添加额外软件时，此目录至少需要 6GB 空间。
- `/var`——将此目录（或其某些子目录）放置在单独分区上是一个好主意，特别是因为安全日志、邮件和打印缓存处理都在该树下进行。你应该为 `/var` 预留至少 1GB 的存储空间，特别是当使用 Ubuntu 作为打印服务器时（因为打印队列的文件将位于 `/var/spool` 下）。

> **提示**
> 作为一条通用规则，将用户和系统数据分离是一个好主意。虽然 Linux 系统可以快速恢复，但用户数据的价值更高，且更难替换。分离数据可以使备份和恢复工作变得简单得多。如果你在访问分区时遇到问题，我们建议你使用完全从 CD 启动并运行的 Knoppix 分发版。这将允许你访问分区并进行任何必要的修复。

# 参考

- <http://www.yale.edu/pclt/BOOT/DEFAULT.HTM>——关于分区的入门教程，不特定于操作系统。
- <http://www.ibm.com/linux/>——IBM 的 Linux 主页，包含指向产品、服务和下载的链接。
- <http://www-124.ibm.com/developerworks/opensource/linux390/>——IBM S/390 Linux 解决方案主页。
- <http://www.dell.com/>——电脑的 Linux 信息页面。
- <http://hardware.redhat.com/hcl>——红帽硬件兼容性数据库的入口。
- <http://www.linux1394.org/>——Linux 火线（FireWire）项目主页，包含有关该端口驱动和设备状态的信息。
- <http://www.linux-usb.org/>——Linux USB 项目主页，包含支持的设备列表和驱动程序链接。

# 附录 B 安装资源

- <http://elks.sourceforge.net/>——针对 x286 及以下 CPU 的 Linux（ELKS Linux）主页。
- <http://www.lnx-nbc.org/>——可启动业务卡（Bootable Business Card）主页，这是一种 50MB 的压缩 Linux 分发版，提供了数百个网络客户端、实时会话、网页浏览、PDA 备份、无线网络、救援会话和文件恢复功能。
- <http://www.cotoyelinux.com/>——若干紧凑 Linux 分发版的主页，提供防火墙和 VPN 服务。基于软盘的分发版在旧款 PC 上运行良好，且不需要硬盘。
- <http://www.freesco.org/>——基于软盘的 Linux 路由器解决方案主页，该方案可在 386 PC 上运行，仅需 6MB 内存，并提供桥接、防火墙、IP 伪装、DNS、DHCP、Web、telnet、打印、时间以及远程访问功能。
- <http://www.bitwizard.nl/sig11/>——关于 Linux Signal 11 错误某些根源的详细概述。
- <http://www.gnu.org/software/parted/parted.html#introduction>——GNU `parted` 工具的主页。
- <http://www.linux.org/vendors/systems.html>——Linux 供应商系统页面。

# 附录 C 安装资源

# Ubuntu 和 Linux 资源

### 网站和搜索引擎
- 新闻组（Usenet Newsgroups）
- 邮件列表（Mailing Lists）
- 网络聊天（Internet Relay Chat）

Ubuntu 拥有丰富的互联网支持，形式包括技术信息的网站、程序文档、错误补丁、用户经验、第三方商业支持，甚至是针对特定问题的集合。

本附录列出了许多支持网站、FTP 仓库、Usenet 群组和电子邮件列表，你可以通过它们获取更多信息和帮助。

| 如果你需要 24/7 的帮助 |
| :--- |
| 如果你是小型企业、公司或企业级 Ubuntu 用户，不要忘记你始终可以寻求源头 Canonical 或提供 Ubuntu 支持的第三方公司。Canonical 软件为其产品提供一系列支持方案，包括 24/7 现场、电话、电子邮件甚至按事件付费。你可以通过 Ubuntu 网站获取更多关于支持的信息：<http://www.ubuntu.com/support/paid>。 |

附录分为以下几个部分：

- 按分类的 Linux 信息网站
- 与 Linux 相关的 Usenet 群组
- 提供 Linux 用户和开发者讨论的邮件列表

## Ubuntu 和 Linux 互联网资源

- 用于 Linux 信息的网络聊天组

本附录还列出了在使用 Ubuntu 时可能感兴趣的网站。

### 保持更新
互联网上一些最快、最全面的搜索引擎都是由 Linux 驱动的，因此使用最好的工具是有意义的。

### 网站和搜索引擎
在众多网站中，`google.com` 脱颖而出，每月拥有数百万用户。该网站利用先进的硬件和软件带来了速度和效率。如果你正在寻找特定的 Linux，请利用这些。

### 网页搜索技巧
解决 Linux 的问题可能是成功与挫败的关键。Google 的一些功能包括 Google Scout（用于在搜索引擎中返回相似页面的链接，即缓存功能）、高级搜索，以及最近的。

### Google 是你的朋友
Google 拥有互联网上任何搜索引擎中最大的数据库，搜索并索引了超过 8 亿个网页。数据库的大小非常重要，因为空搜索对在线用户是无用的，而返回冷门问题的能力可以决定成败。

如果你对认证感兴趣，并希望通过使用 Linux 的公司追求职业生涯或获得就业，你真的应该寻求培训。你可以在 <http://www.ubuntu.com/training/> 找到一份良好的培训提供商列表，并按地理区域进行划分。

# 商业支持

Ubuntu 的商业支持是 Linux 在企业和商业界取得成功的关键要素。尽管有成百上千甚至数万名精通 Linux 和 UNIX 的顾问可以按付费提供服务，但以下是一些知名的 Linux 支持提供者的简短列表：

- <http://www.ubuntu.com/support/paid>——前往源获取多种支持选项。你可以直接从 Canonical 软件获取 Ubuntu 帮助，也可以从本地支持提供商处获取。
- <http://hp.com/linux>——HP 提供了一套全面的 Linux 服务和硬件包，涵盖了你可能想要进行的所有内容，包括咨询、服务器咨询、业务解决方案以及硬件规范和实施。
- <http://ibm.com/linux>——IBM 提供的 Linux 服务包括电子商务解决方案、开源咨询、数据库迁移、集群、服务器和支持。

除了服务导向型的支持公司外，几乎每个 Linux 商业发行版商都提供某种形式的易于购买的商业支持。有很多方法可以利用支持服务（如远程管理、现场咨询、设备驱动开发等），但需求会根据客户的情况和安装环境而异。

# 加入 Linux 用户组的好处

加入当地的 Linux 用户组 (LUG)！加入并参与本地 LUG 有许多好处。你将能够获得帮助、交换信息，并学习许多关于 Linux 的奇妙事物。大多数 LUG 不收会员费，而且许多小组经常赞助由领先 Linux、GNU 和开源专家举办的定期讲座和讨论。一个极佳的起点是，请访问 <http://www.tuk.org/luglist.html>。

# 文档

几乎所有的 Linux 发行版都包含了数千页文档，形式包括手册页（manual pages）、HOWTO 文档（各种格式，如文本和 HTML）、小型-HOWTO 文档或软件包文档（通常位于 `/usr/share/doc/` 目录下）。然而，阅读这些文档最新版本的权威网站是 Linux 文档项目（Linux Documentation Project），位于 <http://www.tldp.org>。

# 网站与搜索引擎

# Linux 指南

如果你正在寻找有关 Linux 主题的更广泛、更详细的信息，请尝试阅读许多 Linux 指南之一。这些指南适用于许多主题，它们对技术主题的阐述比 HOWTO 更详尽，且节奏也更从容。你可以找到以下内容的副本：

- *“Advanced Bash-Scripting Guide，”*由 Mendel Cooper 编写；一份使用 bash 进行 shell 脚本编写的指南
- *“LDP Author Guide，”*由 Mark F. Komarinski 编写；如何编写 LDP 文档
- *“Linux Administration Made Easy，”*由 Steve Frampton 编写
- *“Linux Consultants，”*由 Joshua Drake 编写；一份全球性的商业 Linux 顾问列表。
- *“Linux from Scratch，”*由 Gerard Beekmans 编写；从软件创建 Linux 发行版。
- *“Kernel Module Programming Guide，”*由 Peter J Salzman、Michael Burian 和 Ori Moriomerz 编写；构建 2.4 和 2.6 系列模块的良好指南。
- *“Securing and Optimizing Linux，”*由 Gerhard Mourani 编写
- *Linux 认证
- *“The Linux Network Administrator’s Guide, Second Edition，”*由 Olaf Kirch 和 Terry Dawson 编写；全面的网络管理员指南。

# Ubuntu

- <http://www.ubuntu.com>——Ubuntu 官网，Canonical 基于社区的免费发行版。Ubuntu 是该 Linux 发行版的主版本，包含了数千个软件包，它们构成了最新的、尖端的 Linux 桌面的核心。你也可以找到其他 buntu，如 Kubuntu、Ubuntu 和 ubuntu。
- <http://www.ubuntuforums.org>——如果你需要特定的 Ubuntu 支持，这是一个很好的地方。

# Mini-CD Linux 发行版

Mini-CD Linux 发行版用于许多不同的用途。某些发行版用于启动只读防火墙配置；另一些用于提供尽可能完整的救援环境；而另一些则用于安装或帮助启动完整发行版的安装。Mini-CD 有多种尺寸可选，例如 3 英制 CD-Rs（或 CD-RW），大小从 185MB 到 210MB 不等。你还可以下载 iso 镜像并创建一个 Linux 启动盘，通常可以容纳在 40MB 或 50MB 信用卡大小的 CD-R 上。（考虑使用 mini-CD-RW，特别是如果你想升级你的发行版系统的话。）以下是这些发行版的链接：

- <http://www.lnx-bbc.com>——Linux BBC 首页，一个 40MB 的镜像，托管了带有 X、浏览器和大量网络工具的完整 Linux 会话。
- <http://crux.nu/>——CRUX 1686 优化版 Linux 发行版首页。
- <http://www.smoothwall.org>——69MB 的 SmoothWall 发行版用于安装带有 SSH、HTTP 其他服务的 Web 管理防火墙、路由器或网关。

# 各种基于 Intel 的 Linux 发行版

为基于 Intel 的 PC 选择 Linux 发行版通常取决于个人偏好或需求。许多 Linux 用户偏好 Red Hat 的发行版，因为其卓越的支持、商业支持选项以及在全球的广泛使用。然而，许多不同的 Linux 发行版可以下载。寻找发行版的最佳地方之一是 <http://www.distrowatch.com/>。

- <http://www.andros.net>——Corel
- <http://www.mepis.org>——Ubuntu
- <http://www.debian.org>——Debian
- <http://www.slackware.com>——Slackware
- <http://www.opensuse.org>——SUSE
- <http://www.mandriv.com>——Mandriva
- <http://www.penguinpp.org>——PowerPC

# 附录 C Ubuntu 和 Linux 资源

# PowerPC 发行版

- <http://www.penguinpp.org>——PPC 首页
- <http://www.opensuse.org>——SUSE
- <http://www.yellowdog.com>——Yellow Soft Solutions

# 笔记本电脑上的 Linux

获取笔记本信息的权威网站之一是 Kenneth Harker 的网站。虽然不像过去那样活跃，但该网站 (<http://www.linux-laptop.net>) 仍然包含了笔记本信息。

另一个可以检查的网站是 Werner Heuser 的 Tuxmobil 网站 <http://www.tuxmobil.org>。你可以在那里找到关于 PDA 和手机的信息。Zaurus 用户可以访问 <http://www.openzaurus.org> 下载适用于 5000 和 5500 型号完整开源操作系统。

# X 系统

尽管网上有很多关于 X 系统的技术信息，但寻找特定问题的答案可能会困难。如果你在使用 X 时遇到问题，首先尝试判断是软件问题还是硬件问题。在搜索或寻求帮助（例如 Usenet 的 `comp.os.linux.x` 新组，你可以通过 Google Groups 访问）时，请尽量具体。为了充分评估问题，一些关键因素或信息包括使用的 Linux 发行版；使用的内核；使用的 X 版本；显卡的品牌、名称和型号；显示器和其他硬件的名称、品牌和型号。

本节列出了 Linux 用户的一些基础资源。关于 X 的权威技术信息可以通过 <http://www.x.org> 获取：

- <http://www.harul.net/kenton/index.shtml>
- <http://www.x.org>——X.org 首页，Ubuntu 使用的 X 服务器
- <http://www.x.com/>——Linux 商业 X 版本（以及其他软件产品）

# Usenet 新闻组

如果你遇到 Linux 问题，Linux 相关 Usenet 新闻组是另一个良好的信息来源（例如通过 Google Groups `comp.os.linux.x` 新闻组，见下一节查看其他新闻组）。如果你的互联网服务提供商（ISP）没有提供全面的 Linux 新闻组，你可以访问 <http://groups.google.com/>。

主要的 Linux 和 Linux 相关新闻组如下：

- `alt.os.linux.dial-up`——使用 PPP 拨号
- `alt.os.linux.mandriva`——关于 Mandriva Linux 的一切
- `alt.os.linux.slackware`——使用 Slack Linux
- `alt.os.linux.ubuntu`——使用 Ubuntu Linux
- `comp.os.linux.advocacy`——关于 Linux 及其他相关问题的激烈讨论
- `comp.os.linux.alpha`——在 Alpha CPU 上使用 Linux
- `comp.os.linux.announce`——通用 Linux 通告
- `comp.os.linux.answers`——新的 Linux FAQ 及其他发布
- `comp.os.linux.development.apps`——使用 Linux 开发工具
- `comp.os.linux.development.system`——构建 Linux 内核
- `comp.os.linux.embedded`——Linux 嵌入式设备开发
- `comp.os.linux.hardware`——为各种硬件设备配置 Linux
- `comp.os.linux.m68k`——在 Motorola 68K 系列 CPU 上运行 Linux
- `comp.os.linux.misc`——杂项 Linux 主题
- `comp.os.linux.networking`——网络与 Linux
- `comp.os.linux.portable`——在笔记本电脑上使用 Linux
- `comp.os.linux.powerpc`——使用 PPC Linux
- `comp.os.linux.security`——Linux 安全问题
- `comp.os.linux.setup`——Linux 安装主题
- `comp.os.linux.x`——Linux 与 X Window 系统
- `comp.windows.x.apps`——使用基于 X 的客户端
- `comp.windows.x.i386unix`——Unix PC 上的 X
- `comp.windows.x.intrinsics`——X Toolkit 库讨论
- `comp.windows.x.kde`——关于 KDE 和 X 的讨论
- `comp.windows.x.motif`——关于 Motif 编程的一切
- `comp.windows.x`——关于 X 的讨论
- `linux.admin.*`——面向 Linux 管理员的两个新闻组
- `linux.debian.*`——关于 Debian 的 30 个新闻组
- `linux.dev.*`——25 个或更多 Linux 开发新闻组
- `linux.help`——获取 Linux 帮助
- `linux.kernel`——Linux 内核

# 邮件列表

邮件列表是关于几乎任何主题的交互式或摘要形式的电子讨论。要使用邮件列表，通常必须发送电子邮件请求以订阅列表，并通过主列表邮件发送器的回复消息验证订阅。在订阅交互式列表后，发送的每条消息都会出现在你的邮箱收箱中。然而，许多列表提供了摘要形式的订阅，将一天或半天的流量压缩在单条消息中。除非你设置了电子邮件过滤，否则通常更倾向于摘要。

主要的 Ubuntu 邮件列表在此列出，但与 Linux 相关的列表较少。你可以通过邮件列表搜索网页搜索几乎所有的在线邮件列表，例如 <http://ls.soft.com/lists/list_q.html> 页面。

### GNOME 和 KDE 邮件列表

GNOME 用户和开发者应该知道通过 <http://mail.ubuntu.org/> 有超过两的邮件列表可用。KDE 用户通过查阅 <http://www.kde.org/mailinglists.html> 上 KDE 相关的邮件列表也将受益。

# Ubuntu 项目邮件列表

Ubuntu 项目一直在不断扩大，因为有许多新用户继续首次使用 Ubuntu。通过参与 Ubuntu 的邮件列表之一，你将发现许多博学的用户可以为你的问题提供答案。这些列表侧重于使用、测试、开发以及参与 Ubuntu 的开发：

- <http://lists.ubuntu.com/mail/listinfo/ubuntu-security-announce>——来自 Ubuntu 开发者的安全通告
- <http://lists.ubuntu.com/mail/listinfo/ubuntu-announce>——关于 Ubuntu 的通告
- <http://lists.ubuntu.com/mail/listinfo/ubuntu-users>——Ubuntu 版本用户之间的讨论
- <http://lists.ubuntu.com/mail/listinfo/ubuntu-dev>——来自 Ubuntu 测试版开发者和测试者的查询与报告

# 互联网中继聊天 (IRC)

互联网中继聊天 (IRC) 是许多 Linux 开发者和用户常用的通信形式和论坛，因为它允许实时交互交换信息和想法。要使用 IRC，你必须拥有 IRC 客户端以及托管你所需聊天道的网络和服务器地址。

你可以使用 `irc.freenode.net` IRC 服务器，或 <http://www.freenode.net/> 列出的服务器与其他 Ubuntu 用户聊天。当前的一些频道如下所示：

- `#Ubuntu`——关于 Ubuntu 的通用聊天
- `#ubuntu`——关于 EdUbuntu 的通用聊天
- `#xubuntu`——关于 Xubuntu 的通用聊天
- `#kubuntu`——关于 Kubuntu 的通用聊天

查看更多频道，请访问 <https://help.ubuntu.com/community/InternetRelayChat> 获取详尽的“官方”频道列表。

然而，Google 可以帮助你找到其他可探索的频道。只需在搜索选项中输入发行版名称和 IRC，即可检索与其需求相关的任何 IRC 频道的信息。要获取入门 IRC 的帮助，请访问 <http://www.irchelp.org/>。感兴趣的频道可能包括：

- `linux`——关于 Linux 的通用讨论
- `linuxhelp`——面向新用户的帮助聊天

大多数 IRC 网络提供一个或多个 Linux 频道，尽管某些提供者要求在访问任何聊天频道之前进行注册。

# 索引

# 符号与数字

- `&` (`&`)，shell 后台处理，252-253
- `*` (星号)，566
  - shell 模式匹配搜索，250
  - 通配符，463
- `&&` (`&&`)，shell 表达式，255
- `==` (等号)，272
- `=` (等号)，275
- `!` (感叹号)，271
- `"` (双引号)，264
- `'` (单引号)，265
- `?` (问号)，270
- `#` (井号)，256
- `+` (加号)，258
... (索引其余部分遵循提供的 OCR 模式)

# Apache 服务器 771

- Apache Web 服务器文件系统，控制，422–425
- 管理员模式按钮 (`kdm`)，73
- ADSL 调制解调器，363
- `adsl-stop` 命令，365
- 高级 Linux 声音架构 (ALSA)
  - 声卡驱动，154–177
- `afilio` 备份软件，316
- `alias` 命令，459
- 别名，`myenv` shell 脚本，254
- `allow` 指令 (Apache Web 服务器)，422–423
- `AllowOverrides` 配置指令 (Apache Web 服务器)，421
- Amanda 备份应用，315
- `admump` 命令，222
- 美国互联网数字注册机构网站，329
- 符号 (`&`)，shell 后台处理，252–253
- AND 语句 (SQL)，506–507
- 另一个 midir 写入启用设置 (`vsstpd` 服务器)
- 匿名访问控制，445
- 另一个写入启用设置 (`vsstpd` 服务器)
- 另一个上传启用设置 (`vsstpd` 服务器)
- 匿名访问控制，445
- 匿名访问，控制 `vsstpd` 服务器，446
- 匿名启用设置 (`vsstpd` 服务器)
- 匿名访问控制，445
- 匿名 FTP 服务器，439–440
  - 配置，448
- Calc (OpenOffice.org)，141
  - 环境变量，92–95
  - 登录，90
  - 远程访问，91
  - 文本式控制台，90
- Writer (OpenOffice.org)，138
- 访问控制，配置 `wu-ftpd` 服务器，449–452
- 访问控制指令 (授权文件)
  - 匿名用户访问，限制，449
  - 主机服务器访问，拦截，450
  - 无效密码条目，限制数量，451–452
  - 类中的用户数量，451
  - 权限，根据组 ID 限制，450
  - 用户类，定义，449–450
- 访问权限 (文件)，更改，669
- 访问点，无线网络安全，643
- ACID (原子性、一致性、隔离性、持久性)，数据库合性比较，509
- ACLs (访问控制列表)，Squid 代理服务器，491–495
- ACPI (高级配置和电源接口)，Ubuntu 电源管理，340
- 动作 (PHP 钩子)，594
- Adblock Plus，115
- 附加修复/前缀，461
- 添加/删除应用程序，软件管理，689
- 添加 `sudo` 命令，229
  - 用户，218–219
- 基于地址的虚拟主机，432
- 管理工具，LDAP，532–533
- Apache 组网站，408
- Apache 服务器
  - 安装位置，412
    - 来自 APT，409
    - 来自 APT，410
    - 快速启动指南，412
  - 运行时
    - 配置指令，`DirectoryIndex`，419
    - 配置指令，`DocumentRoot`，418
    - 配置指令，`Listen`，417
    - 配置指令，`ServerAdmin`，418
    - 配置指令，`ServerName`，418
    - 配置指令，`ServerRoot`，417
    - 配置指令，`User`，417–418
    - 配置指令，`UserDir`，419
    - 配置指令，416–418，420
  - `httpd.conf` 文件，416
  - MPM，419
  - 安全报告网站，409
  - 源代码网站，410
  - 源码，编译
    - 通过 `configure` 脚本，411
    - 通过 `In` 命令，411–412
    - 通过 `rpm` 命令，411–412
  - 启动/停止
    - 手动启动，413–414
    - 通过 `/init.d/apache2` 脚本，414–416
  - 升级位置，410
- Apache Foundation，408
- Apache Web 服务器
  - 开发，407–408
  - 文档网站，408
  - 下载，409
  - 文件系统访问控制，425
    - 通过 `allow`/`deny` 指令，422–423
  - 文件系统身份验证
    - `AuthGroupFile` 指令，425
    - `AuthName` 指令，425
    - `AuthType` 指令，425
    - `AuthFile` 指令，425
    - `htpasswd` 命令，424
  - 网络安全，222
  - 日志
    - 通用日志格式，434
    - `CustomLog` 指令，435
  - `mod_access_module`，427
  - `mod_alias_module`，427
  - `mod_auth_module`，427
  - `mod_auth_module`，428
  - `mod_auth_anon_module`，428
  - `mod_auth_dbm_module`，428
  - `mod_auth_digest_module`，428
  - `mod_autoindex_module`，429
  - `mod_cgi_module`，429
  - `mod_dir_module`，429
  - `mod_env_module`，429
  - `mod_expires_module`，429
  - `mod_headers_module`，429
  - `mod_include_module`，429
  - `mod_log_config_module`，430
  - `mod_mime_module`，430
  - `mod_mime_magic_module`，430
  - `mod_negotiation_module`，430
  - `mod_proxy_module`，430
  - `mod_rewrite_module`，430
  - `mod_setenv_module`，430
  - `mod_ssl_module`，431
  - `mod_status_module`，431
  - `mod_unique_module`，431
  - `mod_user_module`，431
  - `mod_vhost_module`，431
  - `mod_vhost_alias_module`，432
  - 优化，656–658
  - 运行时
    - 配置指令，`Allow`，421
    - 配置指令，`Group`，417–481
    - 配置指令，`Options`，420
    - 统计信息，407
  - `autoconf` 命令，773
  - 数组，600
  - 排序()，600
  - 信息，409
  - 虚拟主机
  - 提取()，601
  - 虚拟主机
    - 基于地址的，432
    - 内部网，333
    - 基于名称的，334
  - 数组，582–583
  - `apachectl` 命令，739
  - 附加，251
  - 应用程序，689
  - shell 脚本，57
  - 自动化任务
  - 调度，242–244
  - 任务命令，243
  - `cron` 守护进程，245
  - shell 脚本
    - `#!` (shebang 行)，256–258
    - 内置命令，248–263
    - 环境变量，258
    - 执行，254–255
    - 位置参数，259–261
    - 使用原因，253
    - 特殊字符列表，263–264
    - 系统级访问，255–256
    - 测试，262
    - 木马脚本，255
    - 用户，258
    - 变量访问，259
    - 变量赋值，258
    - 在字符串中存储，259
    - 写入别名，254
    - 写入注释，253
    - 写入换行，253
- 嵌入空格，264–265
- shell 命令行，后台处理，252–253
- shell 命令行，输入/输出重定向，248,251–252
- shell 命令行，作业控制命令，249
- shell 命令行，模式匹配，248,250
- shell 命令行，管道，248,252
- shell 命令行，位置参数，259–261
- `` ` `` (反引号)，用输出替换字符串，266
- 系统服务
  - 更改运行级别，240
  - 手动启动/停止，241–242
  - 故障排除运行级别，240–241
- 系统服务启动操作
  - 启动到默认运行级别，237
  - 启动到非默认运行级别，237–238
  - 启动到运行级别，236
  - 通过管理工具控制服务，239
  - `init` 脚本，238–239
  - 启动加载过程，234–235
  - 加载 Linux 内核，235–236
- `+ shells`
  - `/` (反斜杠) 转义字符，266
  - 更改，256
  - Fedora Core 列表，247–248
  - 作业控制命令，249
  - 维护带变量的 shell 字符串，265–266
  - 手页，248
  - 解析字符串中的变量，248

- `autopers own` (邮件)，485
- `avi` 文件，180
- Axis 基于 Linux 的摄像头网站，168

## 反引号 (`'`)，用输出替换字符串，226 份备份

- 作为安全，643
- 配置文件，302
- 顾问，303
- 数据丢失，原因，302
- 频率，确定，303
- 全量备份，`tar` 命令行备份软件，311
- 硬件，307
- CD-RW 驱动器，308
- FireWire (IEEE-1394) 驱动器，308
- NAS，309
- 磁带机，309
- USB 驱动器，308
- 增量备份
  - 全量备份策略，306
  - `tar` 命令行备份软件，311
  - 内核，312
  - 级别，305-306
  - MBR，320
- 需求评估，303
- 资源，可用性，303
- 从...恢复文件，311-312
- `afio`，316
- Amanda 备份应用，315
- `ark`，313
- `cdbackup`，316
- File Roller，312
- `flexbackup`，316
- `kndat`，313
- `tar`，命令行选项，310
- `tar`，`find` 命令，311
- `tar`，全量备份，311
- `tar`，增量备份，311
- `tar`，从备份恢复文件，311-312
- 良好实践，304
- 策略
  - 选择，307
  - 评估，304-306
  - 家庭用户策略，305
  - 继承，305
  - 大型企业策略，305
  - 数据镜像，307
  - 原则，304
  - RAID 阵列，307
  - 小企业策略，305
  - 小型办公室策略，305
- `badblocks` 命令，文件系统优化，655
- `bak` 文件扩展名，27
- `alsa` (GNOME Office)，161
- 管道运算符 (`|`)，管道，252
- Base (OpenOffice.org)，135
- `bash` 壳，247-248
- 表达式比较
  - 文件比较，270-271
  - 逻辑比较，271
  - 逻辑比较，272
  - 数字比较，268-270
  - 字符串比较，267-268
  - 表达式比较，267
- `test` 命令
  - 文件比较，270-271
  - 逻辑比较，271-272
  - 数字比较，268-270
  - 字符串比较，267-268
  - `test` 命令，267
- `batch` 命令，任务调度，242-244
- Beagle，搜索 Mono 库，631-634
- 蜂鸣码，235

## Behlendorf, Brian, Apache Web 服务器

- Behlendorf, Brian, Apache Web 服务器开发，407
- 内置变量 (壳脚本)，258, 263
  - 查看，263
- 基准测试，硬盘优化，652
- BIOS (基本输入/输出系统)
  - 蜂鸣码，235
  - 启动过程，启动，234
  - 硬盘优化，652
  - `mp` 图形文件，166
- 引导加载程序 (Boot Loader)，13
- 引导加载程序
  - 启动过程，启动，235
  - GRUB
    - 系统服务到非默认运行级别，237-238
    - 密码，238
    - 系统启动，231
  - 启动过程
    - 启动，234-235
    - 通过 CD，235
    - 从通用软磁盘启动系统，320–321
- 引导加载程序，密码，643
- `Bootp` 协议，350, 173–174
- Brasero，(`Python`)，循环控制，556
- `break` 关键字，语句，285
- 循环 (`PHP`)，595
- `switch/case` 块 (`PHP`)，593
- Breezy Badger，731
- 网络安全，645
- 广播地址，334
- 浏览器，114
- 暴力破解，375
- `Bsftp-ssl` 服务器，441
- `Bt` 系列视频芯片组 (Brooktree)，178–179
- BugTraq 邮件列表，648
- 内置壳命令，109
- Bullet Proof X，57
- Bynari，486
- `bzdisk` 指令，内核编译，714
- `bzmage` 指令，内核编译，714
- `bzip2` 实用，710
- C 语言
  - C# 程序
    - Mono，628–629
    - 网站，636
  - C++ 语言
    - 开发，613-614
    - `gcc` (GNU 编译器)，619–620
    - 图形化工具，620–621
    - 项目管理工具
      - `autoconf` 工具，617
      - 调试工具，618–617
      - `make` 命令，615–617
      - Subversion 系统，617–618
    - 项目管理工具，614
  - 电缆 (网络)
  - 光纤，338
  - UTR，337
  - Calc (OpenOffice)，134
  - `camel` 命令，194
  - Canonical Software，730
  - 屏幕截屏，168
  - 形象画，213
  - `case` 语句，283–284
  - `cat` 命令，888
  - `cat` 壳命令，666–667
  - CD 驱动器
    - 赋值，47
    - 配置，46
- 命令组合，777

- `cd` 壳命令，667-668
- CD-RW 驱动器，308
  - 赋值，47
  - 配置，46
- `cdbackup` 软件，316
- `cdrecord` 命令，175
- `cdrecord-scan` 命令，171
- CDs
  - 更改目录，`cd` 壳命令，667-668
  - 文件访问权限，`chmod` 命令，669
  - 内核符号链接，310
  - 运行级别，240
  - 壳，256
- `chattr` 命令，文件系统优化，655
- 清单，749
- `chfn` 命令，103
- `chgrp` 命令，212
- `chmod` 命令，101, 212
- `chmod` 壳命令，269
- 备份策略，314
- `chown` 命令，212
- `chsh` 命令，286
- 类
  - 在 `Python` 中定义，573
  - 继承 (`Python`)，575–577
  - 在 `Python` 中创建，573
  - 方法，573
  - 对象变量 (`Python`)，574
  - 类 (网络)，子掩码，329-330
  - CLI (命令行)
    - 基础命令列表，665–666
    - `cat` 命令，666–667
    - `cd` 命令，667-668
    - `chmod` 命令，669
    - 命令组合，684–685
    - `cp` 命令，669
    - `du` 命令，669–670
    - `find` 命令，670–672
    - `grep` 命令，673–674
    - `less` 命令，674–676
    - `locate` 命令，677
    - `ls` 命令，678–679
    - `man` 命令，679
    - 管理，85–86
    - `mkdir` 命令，680
    - `mv` 命令，680
    - `ps` 命令，680–681
    - 使用原因，664-665
    - `rm` 命令，681
    - `screen` 命令，686–687
    - `tail` 命令，682
    - `top` 命令，682–684
    - `which` 命令，684
- 命令行
  - 命令行，79-82
  - `/bin` 和 `/sbin` 目录，87
  - `/home` 目录，87
  - `/proc` 目录，87
  - `/tmp` 目录，89
  - `/usr` 目录，89
  - `/var` 目录，89-90
  - 基础命令列表，665–666
  - `cat` 命令，666–667
  - `cd` 命令，667–668
  - `chmod` 命令，669
  - 命令组合，684–685
  - `cp` 命令，669
  - `du` 命令，669–670
  - 编辑，87
  - `find` 命令，670–672
  - `grep` 命令，673–674
  - `less` 命令，674–676
  - `locate` 命令，677
  - `ls` 命令，678–679
  - `man` 命令，679
  - 管理，85–86
  - `mkdir` 命令，680
  - `mv` 命令，680
  - `ps` 命令，680–681
  - 使用原因，664-665
  - `rm` 命令，681
  - `screen` 命令，686–687
  - `tail` 命令，682
  - `top` 命令，682–684
  - `which` 命令，684
- `Python` 脚本编写
  - 条件语句，检查检查，570
  - 字典，定义，569
  - 字典，索引，569
  - 字典，可变性，569
  - 字典，569
  - `for` 循环，570
  - 函数定义，572
  - 函数，573
  - 无限循环，571
  - 挂起，561
  - 交互式解释器，提示，562
  - 交互式解释器，变量处理，562
  - 列表，内置方法，566
  - 列表，拷贝，569
  - 列表，可变性，567
  - 列表，567
  - 循环块，571
  - `break` 关键字，572
  - `continue` 关键字，572
  - 多行循环，571
  - 嵌套列表，567
  - 数字处理，浮点值，563
  - 数字处理，整数，563
  - 数字处理，大数字，564
  - 数字处理，转换，564
  - 数字处理运算符，563
  - 运算符重载，567
  - 脚本执行，562
  - 字符串作为不可变值，564
  - 字符串，赋值，564
  - 字符串，内置方法，566
  - 字符串，拼接，566
  - 字符串，索引，565
  - 字符串，重复，566
  - 非官方脚本/插件网站，577
  - `while` 循环，571
- `Python` 编程
  - 类定义，573
  - 类继承 (`Python`)，575–577
  - 类方法，573
  - 类对象变量，574
  - 类构造函数/析构函数，575
  - 类创建实例，573
  - 标准库模块，577
  - 使用原因，664-665
  - `rm` 命令，681
  - `screen` 命令，686–687
  - 软件管理，APT，694–698
  - `tail` 命令，682
  - `top` 命令，682–684
  - Ubuntu 更新，28–30
  - `which` 命令，684

# 780 条命令

- `lftp`，469
- `locate file`，85
- `location`，通过 `top` command 打印，684
- `logname`，231
- `lp`，194
- `lpc`，194
- `lplq`，194
- `lprm`，194
- `lpstat`，194
- `make`，622
- `mv file1 file2`，85
- `autilus`，470
- `cfpt`，470
- `newusers`，231
- `oocalc`，151
- `ooimpress`，151
- `passive`，447
- `passwd`，217, 231
- `patch`，622
- `planner`，151
- `printenv`，92
- `quotacheck`，230
- `quotaoff`，230
- `quotan`，230
- `repquote`，230
- `rm file`，85
- `rmdir dir`，85
- `sftp`，470
- `smbclient`，470
- `snsplint`，622
- `split`，618
- `su`，231
- `sudo`，231
- `svn`，622
- `tar`，86
- `touch`，99
- `useradd -D`，216
- `useradd -G`，214
- `useradd`，216, 231
- `userdel`，217
- `usermod -G`，214
- `usermod`，217, 231
- `vi`，97
- `visudo`，227
- `vsftpd`，470
- `webcam`，470
- `whatis`，85
- `whereis`，85, 94

# 注释

- shell 脚本中，253
- `PHP`，585

# 商业支持，网站，762

- 通用日志格式 (Apache Web 服务器)，234
- 通用 Unix 打印系统 (Common Unix Printing System)，185
- CommuniGatePro，486

# 表达式比较

| `pdksh` shells | `bash` shells |
| :--- | :--- |
| 文件比较，270-271 | |
| 逻辑比较，271-272 | |
| 数字比较，268-270 | |
| 字符串比较，267-268 | |

- `tcshell`
  - 文件比较，274-275
  - 逻辑比较，275
  - 数字比较，273
  - 字符串比较，272

# 比较操作符 (Perl)

- 数字比较操作符列表，542-543
- 字符串比较操作符列表，853

# 编译语言，614

- 编译内核，712
- 磁盘指令，714

# 配置 781

- `bzlimage` 指令，714
- 配置指令，`ServerName`，418
- 多个内核版本，710
- 保留当前内核版本，713
- 配置指令，`ServerRoot`，
- 加速，713
- 配置指令，`User`，417-418
- 故障排除，721
- 配置指令，`UserDir`，419
- `zlimage` 指令，714
- 配置指令，416-420
- Compiz 窗口管理器，53–54
- `http` 配置文件，416
- 组件，SANE，165
- MPM，419
- 复合操作符 (`Perl`)，543
- 磁盘配额，230–231
- 压缩指令，`tar` 命令行
- 防火墙，646
- 备份软件，317
- FTP 服务器，文件转换操作，460–462
- `CONCAT()` 函数，506
- `Python` 中的字符串拼接，566
- `make` 配置工具，714
- `make menunconfig` 工具，715–716
- `make xconfig` 工具，716–717
- 检查检查 (`Python` 条件语句)，570
- RAM 磁盘映像的条件 语句，720
- `Perl` 选择内核类型，705
- `if/else`，546
- ...的子节，717–720
- 概述，545
- `unless`，546
- `PHP` 589–592
- `Python` 条件检查，570
- 条件 (`PHP` 循环)，594
- 配置文件，创建备份，302
- 数据目录所有权，510
- 构建 Apache 服务器，514–515
- 510
- 配置 脚本，`code.` 411
- 配置 ACL，491–495
- 匿名 FTP 服务器，448
- Apache 服务器 示例，496–497
- 配置指令，`AllowOverrides`，421
- 配置指令，`DirectoryIndex`，419
- 配置指令，`DocumentRoot`，418
- 配置指令，`Group`，417–418
- 配置指令，`Listen`，417
- 配置指令，`Options`，420–421
- 配置指令，`ServerAdmin`，418
- CD/DVD 驱动器分配，46–87
- 日/时间重置，44–46
- 首次更新，28–30
- 调制解调器，42–43
- 电源管理，30
- `sudo` 命令，27
- 无线网络，48–49
- `Console.WriteLine()` 方法，629
- 常量 (`PHP`)，584
- 继续 (`Python`)，572
- 控制结构，547
- 转换工具，167
- `Python` 中的类型转换，564
- 并集，464–465
- 连接 (FTP 服务器)，63
- 一致性 (ACID)，509
- 基本命令列表，665–666
- `cd` 命令，667–668
- `cp` 命令，669
- `find` 命令，670–672
- `grep` 命令，673–774
- `In` 命令，676–679
- `is` 命令，677–679
- `locate` 命令，679
- `man` 命令，678–679
- `mkdir` 命令，680
- `mv` 命令，680–681
- `rm` 命令，664–665
- `screen` 命令，686–687
- `tail` 命令，682–684
- `top` 命令，682–684
- `which` 命令，284
- 目录结构，`tar-`命令行备份软件，316–317
- `cp` 命令，318
- `mc` 命令行文件管理，318–319
- `tar` 到远程服务器，374
- 服务器间的多个文件，374–375
- 远程文件到远程服务器，374
- 配置备份，302
- 拷贝文件，318
- `cpio` 命令，322
- CPAN (Comprehensive Perl Archive Network)，551–552
- `Perl` 中的模块，553–854
- CPU (中央处理器)，故障排除，748
- `rackers`，640
- `CREATE DATABASE` 语句 (`PostgreSQL`)，516
- `CREATE DATABASE` 语句 (`MySQL`)，511
- `CREATE` 语句 (`SQL`)，504
- `CREATE USER` 语句 (`PostgreSQL`)，516
- `createdb` 命令 (`PostgreSQL`)，524
- `createuser` 命令 (`PostgreSQL`)，524
- 数据目录 (`MySQL`)，初始化，510
- `cron` 守护进程，重复任务，245–248
- 任务调度，242
- 数据目录 (`PostgreSQL`)，初始化，514–515
- `contrab` 文件，编辑，226–247
- CrossOver Office 数据完整性，比较，509
- 数据锁定，比较，508
- 数据丢失，原因，302
- CUPS (Common Unix Printing System)，185
- 网络打印，LAN 启用，397–399
- 打印机项，创建，400
- SMB，`cupsd` 守护进程，187
- 数据镜像，307
- 数据试点，143
- RDBMS 中的数据存储，501
- 数据库管理员 (DBAs)，当前目录，通过 `ls` shell 列文件，678–679
- 数据完整性，500
- 数据库客户端安装/维护，499
- 数据库安全，500
- 桌面背景，34
- 桌面颜色，35
- 输入设备，键盘布局，40–41
- 键盘快捷键，40
- 鼠标配置，41
- 作为中间件的数据库客户端，520
- 命令行客户端，518
- 本地 GUI 数据库访问，520
- 首选应用程序，37–38
- 可移动驱动器和介质，39
- `CustomLog` 指令 (Apache Web 服务器)，435
- `cvs` 命令，622
- SSH 数据库访问，518–520
- Web 数据库访问权限 (`MySQL`)，512
- 数据库访问/权限问题，518
- 客户端/服务器模型，500
- `cupsd` 守护进程，187
- 邮件，485
- `smbd`，444
- `smbstatus` 命令，390
- 拒绝服务 (DOS) 攻击，88
- `denyery` 指令 (Apache Web 服务器)，422–423
- 依赖检查，615
- 部署，应用清单，749–752
- 业务应用，738–741
- 检查清单，740–742
- 安装，742–743
- 规划，738
- 系统考虑，741–742
- 故障排除，746–748
- 用户考虑，742
- `date` 命令，重置日期设置，44
- 日/时间重置，44
- `date` 命令，25
- `hwclock` 命令，45
- `time-admin` 客户端，46
- 数据库管理员 (DBAs)，职责，499–500
- `dd` 命令，322
- `decca`，Miguel，52
- `deb` 文件，696
- Debian 发行版，352
- GNOME
  - File Roller，312
  - 优化，656
- KDE
  - `ark` 备份工具，313
  - `kdat` 备份工具，313
  - Konqueror 浏览器，配置 Squid 服务器，490
  - 优化，656
- 调试工具
  - C/C++ 编程语言，618–689
  - 符号调试，619
  - 声明 (`PHP` 循环)，594
  - 定义
  - `Python` 中的类，573
  - 字典，669
  - `Python` 函数，572
  - 删除
  - 批量作业，244
  - 通过 `rm` 命令，681
  - `PostgreSQL` 用户，517
  - 拒绝服务 (DOS) 攻击，88
  - `denyery` 指令 (Apache Web 服务器)，422–423
  - 依赖检查，615
  - 部署
  - 应用清单，749–752
  - 业务应用，738–741
  - 检查清单，740–742
  - 安装，742–743
  - 规划，738
  - 系统考虑，741–742
  - 故障排除，746–748
  - 用户考虑，742

## `dmesq` 命令，Ubuntu 配置排排除 785

- 桌面，417
- 背景，更改，34
- `ServerAdmin`，418
- 颜色，更改，35
- `ServerName`，418
- GNOME，53
- `ServerRoot`，417
- `Python` 中的析析构方法，575
- `User`，417–418
- 开发发行版 (内核) 与扩展性内核，709
- `UserDir`，419
- 目录，85
- 设备驱动程序，704
- `cd` shell 命令，更改，667–668
- `devices.txt` 文件，703
- 通过 `mkdir` shell 命令创建，680
- `df` 命令，249
- 通过 `rm` shell 命令删除，681
- `dhclient`，配置选项，353
- `dhclient` 命令，369
- 通过 `ls` shell 命令列出，678–689
- DHCP (动态主机配置协议)，334
- 结构，拷贝，317
- 在启动时激活
- `tar` 命令行备份软件，压缩，317
- 优点/缺点，352
- `DirectoryIndex` 配置指令 (`Apache` 服务器)，419
- DHCP 服务器，354
- `dirlist` 启用设置 (`vsftpd` 服务器默认设置)，448
- `dhcpd.conf` 文件，355–357
- `dimessage` 启用设置 (`vsftpd` 服务器默认设置)，448
- 标识信息对，351
- 禁用命令，194
- 禁用
- IP 地址注册，352
- 局域网 (LAN)，356
- `atime` (文件)，文件系统优化，655
- 租约，351
- 多用户登录功能，66
- NT 服务器，356
- SSH 服务器中的 SSH1，373
- 服务器配置，354–356
- 灾难恢复计划，647–648
- `DHCP Handbook` 网站，357
- 磁盘配额，229–231
- DHCP 服务器，354
- 磁盘使用情况，打印，669–670
- `dhcpd.conf` 文件，355–357
- 显示横幅，455
- `Dia` (OpenOffice.org)，135
- 显示设置屏幕 (`system-config-display`)，64
- 拨号连接，手动配置，365–368
- 显示
- `Python` 中的字典，569
- 连接用户信息，464–866
- `die` 函数 (`Perl`)，555
- 内核版本信息，709
- 指令 (配置)，Apache 运行时配置
- 分布式系统，180
- `AllowOverrides`，421
- `DivX` 文件，180
- `DirectoryIndex`，419
- `DocumentRoot`，418
- `dmesq` 命令，Ubuntu 配置排排除，26

我们如何让此索引更有用？请发送邮件至 indexes@sampublishing.com

## DN (区分名称)

- DN (`distinguished names`)，526-572
- `do...until` 循环 (`Perl`)，549
- `do...while` 循环 (`Perl`)，549, 595
- 文档目录 (`/usr/src/linux-2.6` 目录)，703
- `DocumentRoot` 配置指令 (`Apache` 服务器)，418
- 文档，HOWTO，734
- Don Beck 的 Linux 以太网状态、诊断和设置工具可能包含，341
- 点分进制格式，329
- 双和符号 (`&&`) 数字比较运算符，275
- 双等号 (`==`) 字符串比较运算符，272
- 双管道 (`|`) 数字运算符，275
- 双引号 (`"`)，带有空格的字符串，解析变量，264-265
- 下载启用设置 (`vsftpd` 服务器默认设置)，448
- 下载 Apache Web 服务器，409
- `Draw` (OpenOffice.org)，135
- CD
  - 检查，37
  - 配置，46
- CD-RW
  - 检查，37
  - 配置，46
- DVD
  - 检查，37
  - 配置，46
- DVD+RW/-RW 驱动，177, 308
- DVDs
  - 从命令行创建，176
  - 格式，176
- 动态 IP 地址，361

## E

- `e2fsck` 命令，文件系统优化，655
- `echo` 命令，249
- 编辑
  - `/etc/modprobe.conf` 文件，340
  - `cronab` 文件，245
  - FTP 服务器文件，446
  - `http.conf` 服务器 配置文件 `DirectoryIndex` 配置指令，419
  - `DocumentRoot` 配置指令，418
  - `Group` 配置指令，417
  - `ServerAdmin` 配置指令，418
  - `ServerName` 配置指令，418
  - `ServerRoot` 配置指令，417
  - `UserDir` 配置指令，419
  - `http.conf` 服务器 配置文件，417
- 打印机设置，192
- 系统作业，245
- 表达式，787
- 转义字符
  - `/` (反斜杠) 作为，266
  - `emacs`，96
  - `'` (单引号) 作为，265
- 转义序列，`PHP`，585–586
- 以太工具，296
- 评估备份策略，304–305
- 定期性，306
- 镜像数据，307
- RAID 阵列，307
- 简单备份策略，306
- Evolution (GNOME Office)，147
- Evolution 邮件客户端，531
- Exchange 服务器 (Microsoft)，替代方案，485–487
- 邮件
  - 自动回复，485
  - 守护进程，485
  - Evolution，531
  - `maildir` 目录格式，473
  - `mbox` 目录格式，474
  - MDA，474
  - 选择，483
  - Fetchmail，479–483
  - Procmail，483–484
  - Spamassassin，484
  - Squirrelmail，484
  - 病毒扫描器，484
- MTA
  - 选择，474
  - 逻辑运算符，271
  - 数字比较运算符，275
- 执行 shell 脚本，254–255
- 执行运算符 (`PHP`)，591
- MTA (邮件传输代理)，473
- MUA，474
- 退出语句，285
- 现有 `psql` 命令行客户端 (`PostgreSQL`)，517
- 表达式，485
- 表达式比较
  - 通过 `Perl`，553–584
- Thunderbird，532
- `env` 命令，92
- 环境变量 (`shell` 脚本)，258
- `epiphany` 命令，369
- 等号 (`=`)，字符串表达式运算符，267
- 错误检查，Mono，630–631

## external commands (`ftpconversion file`)

- 外部命令 (`ftpconversion file`)，461
- 外部计算机攻击，定义，640
- `extract()` 函数，601
- 外向性级别 (内核)，709
- `file put contents()` 文件，602
- File Roller，312
- 文件共享
  - 客户端配置，384-385
  - 安装，386
  - 服务器配置，383-383
  - 启动/停止，382
- 传真，403
- `close()` 文件函数，603–604
- FDDI (光纤分布式数据接口) 网络，336
- Feisty Fawn，731
- Fetchmail MDA (邮件投递代理)，479
- 确定
  - 通过 SWAT 配置，392–394
  - 挂起，386
  - 通过 `/etc/samba/smbd.conf` 配置，387–389
  - 共享，391–392
- SMB 协议，385
  - 启动 `smbd` 守护进程，390–391
- SWAT，385
  - 全局选项，480
- 邮件服务器选项，381
- 用户账户，481–483
- 挂起，479
- 光纤缆，338
- 光纤 NIC (网卡)，335
- 字段
  - `/var/log/xferlog`，468–669
- `ftp` 命令，464
- 文件压缩
- 文件命令，463
- 表达式比较，270–275
- 文件扩展，回
- 系统，180
- `badblocks`，655
- 禁用 `atime`，655
- `e2fsck` 命令，655
- `tune2fs` 命令，654
- `sync` 命令，654
- 文件函数 (`PHP`)
- `close()`，603–604
- `contents()`，602
- `fopen()`，602–603
- `size()`，602,–603
- `read()`，603
- `write()`，603
- `get contents()` file，602
- File Transfer Protocol (FTP)，439
- 连接操作，配置 FTP 服务器，460–462
- 命令列表，469
- `find2per` utility，557
- 示例，462–463
- 字段字段，220
- 安装，441–442
- Firefox 浏览器，Squid 代理，490

## FTP (File Transfer Protocol)

- FTP (File Transfer Protocol)，439
- `find` shell 命令，670–622
- 通过 Wu-FTP 服务器管理
- `locate` shell 命令，677
- 连接数，465
- 显示连接用户信息，464–465
- `suid/sgid`，103–104
- 调度服务器停机，466
- `filesize()` 函数，603
- 查看服务器事务日志，467
- `find` 命令，`tar` 命令行备份软件，311
- 通过 `ftphosts` 文件允许/拒绝连接，463
- 表达式比较，270–275
- 文件扩展，回
- 系统，180
- `badblocks`，655
- 禁用 `atime`，655
- `e2fsck` 命令，655
- `tune2fs` 命令，654
- `sync` 命令，654
- 文件函数 (`PHP`)
- `close()`，603–604
- `contents()`，602
- `fopen()`，602–603
- `size()`，602,–603
- `read()`，603
- `write()`，603
- `get contents()` file，602
- File Transfer Protocol (FTP)，439
- 连接操作，配置 FTP 服务器，460–462
- 命令列表，469
- `find2per` utility，557
- 示例，462–463
- 字段字段，220
- 安装，441–442
- Firefox 浏览器，Squid 代理，490

## flex 文件管理

- 纯文本数据库，506
- `flexbackup` 软件，316
- `Python` 中的浮点数，563
- `FROM` 子句，`SELECT` 语句，505

## 电子表格格式 (OpenOffice)，142

- 通过 `less` shell 命令分页输出，674–776
- 使用别名转发邮件，Postfix MTA，478
- 权限，99
- `free()` 文件函数，603
- 通过 `tail` shell 命令打印行，682
- `free` 命令，249
- 远程文件，拷贝到远程服务器，374
- 自由软件基金会，728

## 从备份恢复，`tar` 命令行备份软件，311–332

- 纯文本数据库，506
- `flexbackup` 软件，316
- `Python` 中的浮点数，563
- `FROM` 子句，`SELECT` 语句，505

## 搜索

- FTP (File Transfer Protocol)，439
- `find` shell 命令，670–622
- 通过 Wu-FTP 服务器管理
- `locate` shell 命令，677
- 连接数，465
- 显示连接用户信息，464–465
- `suid/sgid`，103–104
- 调度服务器停机，466
- `filesize()` 函数，603
- 查看服务器事务日志，467
- `find` 命令，`tar` 命令行备份软件，311
- 通过 `ftphosts` 文件允许/拒绝连接，463
- 表达式比较，270–275
- 文件扩展，回
- 系统，180
- `badblocks`，655
- 禁用 `atime`，655
- `e2fsck` 命令，655
- `tune2fs` 命令，654
- `sync` 命令，654
- 文件函数 (`PHP`)
- `close()`，603–604
- `contents()`，602
- `fopen()`，602–603
- `size()`，602,–603
- `read()`，603
- `write()`，603
- `get contents()` file，602

## FTP (文件传输协议)

- 连接的用户信息，464–465
- 编辑文件，446
- 文件转换动作，460–462
- NcFTPd 服务器，440–441
- 软件包，440
- `vsftpd` 服务器，440, 445–448
- `wu-ftpd` 服务器，448–460
- 用户，442–444

## `Perl`
- `die`，555
- `use`，552
- `Python`，定义，572–573
- shell 脚本和，286

## functions (`PHP`)

- 数组函数，600
- 文件函数
    - `close()`，603–604
    - `file_get_contents()`，602
    - 文件句柄，603
    - `file_put_contents()`，602
    - `filesize()`，603
    - `fopen()`，602
    - `fopen()`，603
    - `read()`，603
    - `write()`，603
    - `isset()`，604
- `vsftpd` 服务器，默认设置，448
- `xineted` 守护进程，为 `wu-ftpd` 配置
- 服务器，444

- `ftp` 命令，373, 469
- FTP 站点，`ftp.kernel.org`，709
- `ftpaccess` 文件，
- 配置 `wu-ftpd` 服务器，448–410
- `ftcpconversions` Wu-FTPd 服务器配置
- 文件，448
- `ftpcopy` 命令，469
- `ftpcount` 命令，464
- `ftpcp` 命令，469

## PCRE functions

- 用于拒绝用户列出的 `fthosts` 配置文件 (20.3)，463
- `fthosts` 文件，允许/拒绝 FTP 服务器连接，463
- `fthposts` Wu-FTPd 服务器配置文件，447
- `ftprestart` 命令，464–467
- `ftshut` 命令，464
- `preg match()`，606
- `preg match()`，605
- `preg replace()`，606
- 字符串函数
    - `str replace()`，597
    - `strlen()`，596
    - `strpos()`，599–600
    - `substr()`，597
    - `trim()`，597

- FTP 服务器，调度停机时间，446
- 魔法饼干 (`magic cookies`)，467
- `ftpusers` 文件，`ftpaccess` 配置文件，450
- `ftpo -V` 命令输出列表 (20.3)，465
- `ftpwho` 命令，显示连接的用户信息，464–465
- 全量备份，306–307
- `unset()`，604
- `var dump()`，605
- `var dump()`，606
- `write()` 文件函数，703

- `tar` 命令行备份软件，311

- 函数时间，跟踪，619
- functions. 参见 functions (`PHP`)
- 作为 `Python` 中的类方法，573

## 游戏
- Battle for Wesnoth，204
- DOOM 3，200

## 图形 791

- 安装，199
- GNU 命令，85
- 概述，197-198
- GNU 编译器集合 (`gcc`)，613
- Quake 4，202
- GNU 通用许可证，727
- Unreal Tournament 2004，201-202
- Numeric (GNOME Office)，147
- 视频驱动程序，198–199
- `gnumeric` 命令，151
- Windows，使用 Cedega 玩，204-205
- `gocr` 光学识别客户端，165
- Wolfenstein: Enemy Territory，203
- Google BrowserSync，115
- `gcc` (GNOME 编译器)，613, 619–722
- Google 网站，761
- `gdb` 命令 (C/C++ 编程语言)，619, 622
- 内内核错误，故障排除，722
- Ubuntu 配置的故障排除，26
- `gdm` (GNOME 显示器管理器)，配置，66–67, 71
- GPL (GNU 通用许可证)，727
- `gprof` (分析) 命令 (C/C++ 编程语言)，619, 622
- `gdmsetup` 客户端，66
- Gracen CDDB 识别服务，172
- Gecko 引擎，115
- GetCodecs，189
- `GRANT` 语句 (`PostgreSQL`)，517
- `gftp` 命令，469
- `GRANT` 语句 (`SQL`)，512–513
- Ghostscript，版本，189
- `grant` 表 (`MySQL`)，初始化，510
- `gif` 图形格式，166
- 千兆以太网，336
- `gimp` 工具，151
- 图形视图，298
- Glade 客户端，621
- 图形数据库 (`MySQL`)，523
- 图形开发工具，C++，620–621
- `glade-3` 命令，222
- 图形转换，167
- 全局级权限 (`MySQL`)，512
- GNOME (网络对象环境) 桌面环境，52
- 文件格式，167
- 配置，53–54
- F-Spot，169
- File Roller，312
- GIMP (图像处理程序)，147
- Glade 客户端，621
- GTK (`imp Tool Kit`) 控件，146
- 邮件列表，767
- 手持，168
- 优化，656
- GNOME 办公，146–149
- 菜单导航，164
- `gnome-app-install` (GUL 包管理器)，699
- 扫描仪，164–166
- `gnome-nett-tool`，296
- 屏幕截图，168
- 网站，183
- `gnome-volume-properties`，39
- 如何让此索引更有用？联系我们 indexes@publishing.com
- 图形驱动程序，安装
- 大于 (`>`) 运算符，273
- Green, Andy，Telnet 服务器，372
- 问候命令，隐藏信息，453
- `grep` 命令，249
- `grep` shell 脚本，261–262
- `grep string(s)` 命令，85
- `greplog` 脚本，261
- `Group` 配置 (`Apache` 服务器)，417–418
- GRUB (统一引导加载程序) 安装，13
- 系统启动，到非默认运行级别，237–238
- `gs` 列表，186
- `gs` 命令，189
- `gThumb`，169
- GT+，创建 GUI，634–635
- `guides` (Linux)，763
- GUIs，创建，634–635
- Gutsy Gibbon，731
- `gv` 命令，189
- `gzip` 包，322
- `gzip` 软件包，710

## H

- 黑客，640
- 硬盘，优化，652
- BIOS 调整，652
- 文件系统调整，645–655
- `hdparam` 命令，653
- 硬链接，676
- 硬件备份清单，749–752
- CD-RW 驱动器，308
- DVD+/RW/- 驱动器，308
- FireWire (IEEE-1394)，驱动器，308
- NAS，309
- 磁带驱动器，309
- 备份，307
- 硬盘存储，744
- 传统硬件备份，743–744
- 兼容性测试，745–746
- 故障排除，746–748
- Ubuntu 安装，12
- 硬件选项卡 (`system-config-client`)，64
- 哈希 (`Peri`)，501–540
- `hdparam` 命令，硬盘优化，653
- `hdx=ide-scsi` 命令，硬盘优化，652
- `here` 运算符，251
- 隐藏进程，298
- Hoary Hedgehog，731
- 主用户备份策略，305
- 托管文件系统，756–757
- HOWTO 文档，734
- DVD+/RW/+R/-[W]，176
- LILO 配置，722
- 网络启动和奇异根，643
- HTML，`PHP`，607–608
- `httppasswd` 命令 (Apache Web 服务器)，创建用户文件，424
- `httpd`，437
- `httpd.conf` Apache 服务器配置文件，编辑，416
- `DirectoryIndex` 配置指令，419
- `DocumentRoot` 配置指令，418
- `Group` 配置指令，417–418

## 安装 793

- 索引
- `Listen` 配置指令，417
- 字典，569
- 无限循环，593
- 信息/技术，729
- `Python` 中的继承 (类)，575–577
- 继承环境，225
- `hwclock`，重置时间，459

## I

- IBM 商业软件，762
- IDE 驱动器作为 SCSI 模拟器，172
- 识别网络硬件，399
- 编辑 `/etc/modprobe.conf` 文件，340
- 手动加载内核模块，341
- 发起启动过程，234–235
- `autotune` 命令，硬盘优化，652
- 布局，40–41
- 快捷键，40
- 鼠标配置，41
- `Python` 中的整数，563
- 基于 Intel 的 Linux 发行版网站，422
- 交互式解释器 (`Python`)，562
- 接口
    - GUIs，创建，634–635
    - Konqueror，115
    - 内部计算机攻击，639–640
    - 内部网络网站，Apache 服务器
    - 虚拟托管，433
- Internet. 参见 Internet connectivity
- IP (网协议)，328

## IP 地址

- DHCP 352
- 动态，361
- Squid 代理服务器，495–499
- 静态，361

## IP 伪装，331

- IPP (打印协议)，185
- IPv4 (Internet 协议 4) 地址，329–331
- IPv6 (Internet 协议 6) 地址，331

- 邮件，115
- 邮件，120
- Evolution，116–118
- Firefox，114–115, 122
- 即时通讯 (带 Pidgin)，123–125

- IRC (Internet 聊天)，225, 767–768

# 内核 795

IS/IT（信息服务/信息技术）环境，729

# K

- ISC（互联网服务联盟）网站，354
- `kdat` 备份工具，313
- KDE 桌面环境，77
- 隔离 (ACID)，数据库合性比较，509
- `ark` 备份工具，313
- `kdat` 备份工具，313
- ISP（互联网服务提供商）
- Konqueror 浏览器，为 Squid 代理服务器配置，490
- ADSL 调制调器，363
- 邮件列表，767
- 分配，361
- 优化，256
- 动态 IP，361
- `KDevloop` 客户端，620–621
- Linux 支持，360
- `kde` 命令，622
- 静态 IP 地址，361
- `kdf` 工具，299
- `isset()`，604
- `kdm` (KDE 显示管理器)，配置，内核
- 迭代语句
- `#!` (shebang 行)，256–258
- `break`，285
- 备份，712
- C 语言语言，614
- 编译，712
- `bZDisk` 指令，714
- `for`，276–277
- `bzlmage` 指令，714
- `if`，281–282
- 保留当前内核版本，713
- `repeat`，280
- 加速，713
- `select`，280
- 故障排除，721
- `shift`，281
- `zlmage` 指令，714
- `until`，279–290
- 配置
- `iwconf` 命令，369
- 无线网络，357–358
- `make config` 工具程序，714
- `make config` 工具程序，715–716
- `iwlist` 命令，无线网络，357
- `make xconfig` 工具程序，716–717

# J

- 任务号（批量任务），查看，244
- RAM 磁盘镜像，720
- 作业控制命令，249
- ...的子章节，717–720
- `joe`，96
- 开发，702
- `Python` 中的字符串拼接，566
- 开发版本，709
- Joy, Bill，96
- 设备驱动程序，704
- `jpg` 图形文件格式，1666
- 内联内核，705
- Linux 内核，安全，639
- 管理模块，707
- 模块化内核，705

我们如何能让这个索引更有用？请发送邮件至：indexes@sampublishing.com

# 内核

- `/etc/modprobe.conf` 文件，707
- 加载模块，708
- 管理，706–707
- 模块，手动加载，341
- 单体内核，705
- 多版本，编译，710
- 优化，655–656
- 概述，702
- 补丁内核，708–710
- 多个内核版本，711
- 补丁方法，711
- ID，235
- 预编译内核，安装，708
- 重新编译，708
- 运行时错误，故障排除，402
- SCSI 磁盘驱动程序，705
- `/usr/src/linux-2.6` 目录，704
- 源码树 Makefile，702
- 源码，获取
- `bzip2` 工具程序，710
- `gzip` 包，710
- 源码，获取，709
- 稳定内核，709
- 符号链接，更改，311
- 在 `/usr/src/linux-2.6` 目录下的测试程序，704
- 类型，选择，705
- 版本，708
- 显示版本信息，709
- `kibitz` 命令，286
- `kill-SIGHUP` 命令，495
- KOffice，149
- `konqueror` 命令，437, 469
- Conqueror 浏览器 (KDE)，为 Squid 代理服务器配置，490
- K 调度程序 (KOffice)，150
- `koshell` 命令，151
- `sh` shell，247
- `ksort()` 数组，600
- `kSpread` (KOffice)，149
- `spread` 命令，151
- `ksysguard` 工具，299
- `KWord` (KOffice)，149

# 局域网

- DHCP，356
- 网络打印，启用，397–398
- 安全，332
- 信息性网站，765
- 模型配置，42–43
- 大型企业备份策略，305
- 最后语句 (`Perl`)，548
- LDAP (轻量级目录访问协议)
- 向添加人员，528–530
- CN，526
- DN，526–527
- Evolution，531
- 管理，532–533
- Thunderbird，532
- 功能，525
- `ldap` 命令，529
- `search` 命令，530
- `kernel-parameters.txt` 文件，703
- 基于密钥的登录，375–376
- 布局，40–41
- 键功能，`Perl` 哈希表，541
- 关键字，保留 SQL，504

# 本地主机接口

- LDIF，528
- 非特定搜索，527
- 概述，727–728
- 使用原因，729–730
- 软件现代支持，366
- 版本，728
- 病毒，646
- `LDAPAdmin` 工具，533
- Linux Foundation 网站，727
- Linux Zaurus PDA 网站，765
- 为...分配密码，527
- 定义，526
- 服务器配置，526–527
- `Listen` 配置 (`Apache` 服务器)，417
- 当前目录下的文件，678–689
- 进程，680–681
- `ldapd` 命令，529
- LDIF (`LDAP` 数据交换格式)，528
- 租约，351
- 旧式打印机，故障排除，403–404
- `less` 命令，108
- `less` 命令，674–676
- 小于，279
- `ldap` 命令，469
- 库，Mono，631–635
- 内核参数，703
- `kernel-parameters.txt` 文件，703
- 基于密钥的登录，375–376
- 布局，40–41
- 键功能，`Perl` 哈希表，541
- 关键字，保留 SQL，504

# 本 接口

- LDIF，528
- 非特定搜索，527
- 概述，727–728
- 使用原因，729–730
- 软件现代支持，366
- 版本，728
- 病毒，646
- `LDAPAdmin` 工具，533
- Linux Foundation 网站，727
- Linux Zaurus PDA 网站，765
- 为...分配密码，527
- 定义，526
- 服务器配置，526–527
- `Listen` 配置 (`Apache` 服务器)，417
- 当前目录下的文件，678–689
- 进程，680–681
- `ldapd` 命令，529
- LDIF (`LDAP` 数据交换格式)，528
- 租约，351
- 旧式打印机，故障排除，403–404
- `less` 命令，108
- `less` 命令，674–676
- 小于，279
- `ldap` 命令，469
- 库，Mono，631–635
- 内核参数，703
- `kernel-parameters.txt` 文件，703
- 基于密钥的登录，375–376
- 布局，40–41
- 键功能，`Perl` 哈希表，541
- 关键字，保留 SQL，504

# 本 接口

- LDIF，528
- 非特定搜索，527
- 概述，727–728
- 使用原因，729–730
- 软件现代支持，366
- 版本，728
- 病毒，646
- `LDAPAdmin` 工具，533
- Linux Foundation 网站，727
- Linux Zaurus PDA 网站，765
- 为...分配密码，527
- 定义，526
- 服务器配置，526–527
- `Listen` 配置 (`Apache` 服务器)，417
- 当前目录下的文件，678–689
- 进程，680–681
- `ldapd` 命令，529
- LDIF (`LDAP` 数据交换格式)，528
- 租约，351
- 旧式打印机，故障排除，403–404
- `less` 命令，108
- `less` 命令，674–676
- 小于，279
- `ldap` 命令，469

# 
- KOffice，149
- `konqueror` 命令，437, 469
- Conqueror 浏览器 (KDE)，为 Squid 代理服务器配置，490
- K 调度程序 (KOffice)，150
- `koshell` 命令，151
- `sh` shell，247
- `ksort()` 数组，600
- `kSpread` (KOffice)，149
- `spread` 命令，151
- `ksysguard` 工具，299
- `KWord` (KOffice)，149

# LANS

- DHCP，356
- 网络打印，启用，397–398
- 安全，332
- 信息性网站，765
- 模型配置，42–43
- 大型企业备份策略，305
- 最后语句 (`Perl`)，548
- LDAP (轻量级目录访问协议)
- 向添加人员，528–530
- CN，526
- DN，526–527
- Evolution，531
- 管理，532–533
- Thunderbird，532
- 功能，525
- `ldap` 命令，529
- `search` 命令，530
- `kernel-parameters.txt` 文件，703
- 基于密钥的登录，375–376
- 布局，40–41
- 键功能，`Perl` 哈希表，541
- 关键字，保留 SQL，504

# localhost 接口

- `/etc/modprobe.conf` 文件，707
- 加载模块，708
- 管理，706–707
- 模块，手动加载，341
- 单体内核，705
- 多版本，编译，710
- 优化，655–656
- 概述，702
- 补丁内核，708–710
- 多个内核版本，711
- 补丁方法，711
- ID，235
- 预编译内核，安装，708
- 重新编译，708
- 运行时错误，故障排除，402
- SCSI 磁盘驱动程序，705
- `/usr/src/linux-2.6` 目录，704
- 源码树 Makefile，702
- 源码，获取
- `bzip2` 工具程序，710
- `gzip` 包，710
- 源码，获取，709
- 稳定内核，709
- 符号链接，更改，311
- 在 `/usr/src/linux-2.6` 目录下的测试程序，704
- 类型，选择，705
- 版本，708
- 显示版本信息，709
- `kibitz` 命令，286
- `kill-SIGHUP` 命令，495
- KOffice，149
- `konqueror` 命令，437, 469
- Conqueror 浏览器 (KDE)，为 Squid 代理服务器配置，490
- K 调度程序 (KOffice)，150
- `koshell` 命令，151
- `sh` shell，247
- `ksort()` 数组，600
- `kSpread` (KOffice)，149
- `spread` 命令，151
- `ksysguard` 工具，299
- `KWord` (KOffice)，149

# LANS

- DHCP，356
- 网络打印，启用，397–398
- 安全，332
- 信息性网站，765
- 模型配置，42–43
- 大型企业备份策略，305
- 最后语句 (`Perl`)，548
- LDAP (轻量级目录访问协议)
- 向添加人员，528–530
- CN，526
- DN，526–527
- Evolution，531
- 管理，532–533
- Thunderbird，532
- 功能，525
- `ldap` 命令，529
- `search` 命令，530
- `kernel-parameters.txt` 文件，703
- 基于密钥的登录，375–376
- 布局，40–41
- 键功能，`Perl` 哈希表，541
- 关键字，保留 SQL，504

# localhost 接口

- LDIF，528
- 非特定搜索，527
- 概述，727–728
- 使用原因，729–730
- 软件现代支持，366
- 版本，728
- 病毒，646
- `LDAPAdmin` 工具，533
- Linux Foundation 网站，727
- Linux Zaurus PDA 网站，765
- 为...分配密码，527
- 定义，526
- 服务器配置，526–527
- `Listen` 配置 (`Apache` 服务器)，417
- 当前目录下的文件，678–689
- 进程，680–681
- `ldapd` 命令，529
- LDIF (`LDAP` 数据交换格式)，528
- 租约，351
- 旧式打印机，故障排除，403–404
- `less` 命令，108
- `less` 命令，674–676
- 小于，279
- `ldap` 命令，469

## 方法

- `Application.Run()`，633
- `Python` 中的类方法，573
- `Console.WriteLine()`，629
- `Python` 中的构造方法，575
- `Python` 中的析析构方法，575
- 在列表中，568
- `Main()`，628
- `Run()`，633
- `SendAsync()`，633
- `Python` 中的字符串方法，566
- `WriteLine()`，629

- 模块化内核，705
- `/etc/modprobe.conf` 文件，707
- 加载模块，708
- 管理，706–707

### 模块
- 加载，708

- `Perl`
- 从 CPAN 安装，553–554
- `Mail::Sendmail`，555–554
- 标准模块列表，访问，552
- `Python` 标准库模块，577

- Microsoft Exchange Server，替代方案，485–487
- Microsoft Exchange Server/Outlook 客户端，486
- 中间件，作为数据库客户端，520
- Mini CD Linux 发行版数据库，764
- 小版本章节 (内核)，709
- 镜像数据，307
- `mkbootdisk` 命令，722
- `mkdir` 命令，101
- `mkdir` shell 命令，680
- `mkinitrd` 命令，722
- `mikosfs` 命令，174–175
- 调制调器，检测/配置
- 串口端口模块，42
- WinModem 笔记本电脑配置，42–43

- 修改
- `su` 命令，225–226
- 系统字体，36
- 视觉效果，37

- `modinfo` 命令，模块化内核管理，706
- `modprobe` 命令
- 手动加载内核模块，341
- 模块化内核管理，706

- `mod_access` 模块 (`Apache Web 服务器`)，427
- `mod_alias` 模块 (`Apache Web 服务器`)，427
- `mod_asm` 模块 (`Apache Web 服务器`)，428
- `mod_auth_anon` 模块 (`Apache Web 服务器`)，428
- `mod_auth_dbm` 模块 (`Apache Web 服务器`)，428
- `mod_auth_digest` 模块 (`Apache Web 服务器`)，428–429
- `mod_cgi` 模块 (`Apache Web 服务器`)，429
- `mod_dir` 模块 (`Apache Web 服务器`)，429
- `mod_env` 模块 (`Apache Web 服务器`)，429
- `mod_expires` 模块 (`Apache Web 服务器`)，429
- `mod_headers` 模块 (`Apache Web 服务器`)，429
- `mod_include` 模块 (`Apache Web 服务器`)，429
- `mod_info` 模块 (`Apache Web 服务器`)，430
- `mod_log_config` 模块 (`Apache Web 服务器`)，430
- `mod_mime` 模块 (`Apache Web 服务器`)，430
- `mod_mime_magic` 模块 (`Apache Web 服务器`)，430
- `mod_negotiation` 模块 (`Apache Web 服务器`)，430
- `mod_proxy` 模块 (`Apache Web 服务器`)，430
- `mod_rewrite` 模块 (`Apache Web 服务器`)，430
- `mod_setenv` 模块 (`Apache Web 服务器`)，430
- `mod_speling` 模块 (`Apache` 服务器)，431
- `mod_ssl` 模块 (`Apache Web 服务器`)，431
- `mod_status` 模块 (`Apache Web 服务器`)，431
- `mod_unique_id` 模块 (`Apache Web 服务器`)，431
- `mod_userdir` 模块 (`Apache Web 服务器`)，431
- `mod_ertrack` 模块 (`Apache Web 服务器`)，431
- `mod_vhost_alias` 模块 (`Apache Web 服务器`)，431–432
- 监控用户，219–220
- `moditors`，修改，62

- MPM (多进程模块)，Apache 服务器配置，419
- `mpm_common` MPM (多进程模块)，Apache 服务器配置，419
- MS-DOS 环境，80
- MTA (邮件传输代理)
- 选择，474
- Exim，473
- `mbox` 邮件目录格式，474
- `pine` 目录格式，474
- Postfix
- 配置，476–477
- 使用别名转发邮件，478
- 伪装，477
- 消息投送间隔，设置，477–478
- 邮件中继，478
- 智能主机，477
- Postfix，472
- Qmail，`mail` 邮件目录格式，473
- Sendmail，473
- MUA (邮件用户代理)，474–475
- 多会话 CD，创建，175
- 多播地址址，334
- 多播模式 (网卡)，343

## 多媒体

- Mono
- 优势，625–626
- C# 程序，628–629
- 命令行工具，626–627
- 错误检查，630–631
- GUI，创建，634–635
- 库，搜索，631–635
- MonoDev，627–628
- 网站，636
- 参数，输出，629
- 参考文献，636
- 变量，创建，629–630
- 网站，636

- MonoDev，627–628
- 单体内核，705
- 主板，故障排除，741
- 网站，636
- `mount` 命令，挂载 Samba，391–392
- `mov` 文件，180
- 通过 `mkdir` shell 移动文件，680
- Mozilla Thunderbird，118
- MP3 文件，155, 177
- MPEG 文件，156, 177, 180
- MPlayer，182
- 格式，156, 177
- 硬件，180
- 相关命令，182
- 存储容量，176
- TV/视频，178
- 网站，182–183
- 多媒体应用
- 捕获屏幕图像，186
- CD/DVD，刻录，170–172
- 从命令行创建，174–177
- 使用图形客户端创建，172
- 文件格式，180–181
- 格式化，156–157
- 修改卷容量，155, 177
- 个人视频录影机，181–182
- Rhythmbox，162
- 扫描仪，166–167
- 声卡，154, 174
- 电视硬件，178–180
- 视频，181
- 多媒体应用，153
- 多个文件，复制，374–375
- 多个内核版本，37
- 编译，710
- 补丁，711
- 多个登录，禁用，66
- 多个终端，屏幕，686–687
- 可变性，567
- `Python` 字典，569
- `mv` shell 命令，680
- 执行，254–255
- 多个数据，创建，255
- MySQL 访问，518
- MySQL 命令行客户端，518
- MySQL 图形界面，523
- MySQL 挂载，521–522
- MySQL 数据库创建，512
- MySQL 网站，636
- MySQL 安装，510
- MySQL 配置，510–511
- MySQL 优化，510
- MySQL 缓存，510
- MySQL 索引，558–559
- MySQL 查询，560–561
- MySQL 触发器，562
- MySQL 权限，563
- MySQL 列权限，564
- MySQL 表权限，565
- MySQL 全局权限，566
- MySQL 用户权限，567
- MySQL 账户，添加，568
- MySQL 密码，569
- MySQL 登录，570
- MySQL 实例，571
- MySQL 备份，572
- MySQL 恢复，573
- MySQL 迁移，574
- MySQL 导出，575
- MySQL 导入，576
- MySQL 复制，577
- MySQL 优化，578
- MySQL 索引，579
- MySQL 维护，580
- MySQL 性能，581
- MySQL 监控，582
- MySQL 架构，583
- MySQL 扩展，584
- MySQL 插件，585
- MySQL 驱动，586
- MySQL 存储，587
- MySQL 安全，588
- MySQL 扩展，589
- MySQL 集群，590
- MySQL 高可用，591
- MySQL 复制，592
- MySQL 故障，593
- MySQL 审计，594
- MySQL 日志，595
- MySQL 分析，596
- MySQL 备份，597
- MySQL 同步，598
- MySQL 调度，599
- MySQL 负载，600
- MySQL 扩展，601
- MySQL 优化，602
- MySQL 性能，603
- MySQL 存储，604
- MySQL 缓存，605
- MySQL 索引，606
- MySQL 查询，607
- MySQL 接口，608
- MySQL 驱动，609
- MySQL 扩展，610
- MySQL 维护，611
- MySQL 部署，612

- MySQL 命令行，613
- MySQL 客户端，614
- MySQL 服务器，615
- MySQL 监控，616
- MySQL 扩展，617
- MySQL 优化，618
- MySQL 性能，619
- MySQL 存储，620
- MySQL 缓存，621
- MySQL 索引，622
- MySQL 查询，623
- MySQL 接口，624
- MySQL 驱动，625
- MySQL 扩展，626
- MySQL 维护，627
- MySQL 部署，628

- N
- 字节，329
- NAS (网络附加存储)，309
- NAT (网络地址转换)，332
- 网络
- 桥接，84
- 广播，333
- 交换机，338–339
- 纤，336
- `/etc/dhcp.conf` 文件，340
- 启动时激活，341
- 客户端，342–343
- 连接，344
- 故障排除，345
- 纤，346
- `/etc/hosts` 文件，347
- 纤，348
- `/etc/interfaces` 文件，349
- 索引，350
- 密钥，351
- 激活，352
- 局域，353
- 局域，354
- 局域，355
- 局域，356
- 局域，357
- 局域，358
- 局域，359
- 局域，66
- 协议，360
- 路由，361
- 路由器，362
- 终端，363
- 隧道，364
- 上行，365
- 无线，366

- O
- 字节，574
- OCR (光学字符识别)，165
- 字节，329
- 一行 `Perl` 示例，555
- `oalloc` 命令，151
- 文件，156, 177
- `oprint` 命令，151

## OOP (面向对象编程)

- `Python`
- 类定义，573
- 类方法，573
- 实例化类，573
- 类的继承，575–577
- 类的变量，574
- 构造/析构方法，564

- 新 按钮
- 新打印，548
- 下一个语句 (`Perl`)，548

- NFS (网络文件系统)
- 客户端配置，384–385
- 服务器配置，383–384
- 启动/停止，382

- NIC (网络接口卡)
- 100BASE-T，335
- 100BASE-T，335
- 1000BASE-T，336
- 1000BASE-X，336
- 光纤，336
- 多播模式，343
- 混杂模式，343, 645
- 环网，335
- 故障排除，341

- `owwriter` 命令，151
- 开源系统 (OSS) 声卡驱动，154, 177
- Open-Xchange，486
- OpenLDAP，525

- 文件权限，530
- 管理工具，532–539
- OpenOffice.org
- Calc，140–144
- 配置，136–137
- 开发，135–136
- 办公工具，144–149

passwords 805

overview of，134

`hdparm` command，653

spelling/hyphenation dictionaries，137

KDE desktop environment，656

Writer，137–140

Linux kernel，655–656

OpenSSH，440

MySQL
  - servers，372
  - measuring key buffer usage，658–659
  - tools，wireless network security，643
  - query caches，660–661
  - query optimization，661
  - operators (`PHP`)，589
  - read buffers，661
  - table caches，661
  - ternary operators，591
- configuration (Apache Web)，420–421
- conversions list，462
- numeric comparison list，542–543
- OR (SQL)，506–507
- string comparison list，543
- compound operators，543
- output redirection，248–252
- overclock，748
- miscellaneous operators，544
- optical recognition (OCR)，196
- `dvd+rw-tools`，176
- Apache web server，656–658
- FTP servers，440
- packet writing，DVD burning，177
- paging through file output，`less` command，674–676
- disabling at，555
- PAM (Pluggable Authentication Modules)，223
- `tune2fs` command，654
- Ubuntu installation options，12–13, 17
- GNOME desktop environment，656
- `passive` command，447
- passwords
  - benchmarks，652
  - bootloaders，643
  - brute-forcing，375
  - FTP servers，442
  - GRUB，238
  - LDAP root users，signing to，527
  - MySQL root users，511
  - PostgreSQL database users，creating，516
  - Ubuntu installation，18–19

How can we make this index more useful? Email us at indexes@publishing.com

- `badblocks`，806
- `patch` command，622
- `patch` command，652
- patched kernels，708–711
- pattern-matching，248–250
- command，655
- `de-fragment-blocks` command，hard disk optimization，652
- PCRE (Perl-Compatible Regular Expressions)，functions
  - `pre match all()`，606
  - `pre match()`，605
  - `pre replace()`，606
- `pcregrep` utility，655
- Linux kernel，655–660
- `pcx` graphics file format，166
- `pdksh` shells，247
- measuring key buffer usage，658–659
- query caches，660–661
- query optimization，661
  - file commands，270–271
  - logical comparisons，271–272
  - number comparisons，268–270
  - string comparisons，268–268
  - `select` statements，280
- comparison of expression，267

- `Perl`
  - `#!` (she-bang)，539
  - appeal of，537
  - code examples
  - command-line processing，556
  - one-liners，556
  - posting to Usenet，555–556
- PEAR:DB (`PHP`)，608–610
- purging logs，553–554
- performance tuning
  - sending email，553–554
  - Apache Web server，656–658
  - file systems
- conditional statements
  - `badblocks` command，655
  - disabling `atime`，655
  - `e2fsck` command，655
  - `tune2fs` command，654
- development of，537
- GNOME desktop environment，656
- functions
  - `die`，555
  - `use`，552
- constructs
  - `do...while` loops，549
  - `for` loops，547
  - `foreach` loops，547
  - `last` statements，548
  - `redo` statements，548
  - `until` loops，549
  - allow users to change file permissions，457
  - allowing users to rename files，458
  - assigning users to overwrite permissions，458
  - user-created file permissions，458
  - `while` loops，549
- configuration file，459–549
- comparison operators，542–543
- compound operators，544
- miscellaneous operators，544
- `chmod` command，669
- OpenLDAP，530
- regular expressions，549
- `sendmail` command，550–551
- simple programming example，538–540
- system logging，538
- access (`PostgreSQL`)，524
- `pg_ctl` command (`PostgreSQL`)，524
- Photoshop (Adobe)，coming to GIMP，164
- arrays，540–541
- hashes，540–541
- scalars，540
- special variables，541
- versions of，538
- array functions
  - `array keys()`，600
  - `array values()`，600
  - `arsort()`，600
  - `asort()`，600
  - `extract()`，601
  - `krsort()`，600
  - `ksort()`，600
  - `shuffle()`，600
  - backreferencing，606–607
  - comments，585
  - conditional statements，589–832
  - constants，584
  - development of，579
  - entering/exiting，580
- `perl` (`Perl` compiler)，557
- `perldoc` (`Perl` documentation utility)，540, 557
- document，accessing，540

## 810 打印

- 磁盘占用，`du` shell 命令，669–670
- 文件内容，`cat` shell 命令，666–667
- 基于 GUI 的打印机，187
- 文件末尾，通过 `tail` shell 命令，682
- 本地打印机，189, 192
- Mono 参数，629
- 网络打印机
    - CUPS GUI，399–400
    - LAN，启用，397–398
    - SMB 打印机，398
    - 概述，185–187
    - 参考文献，195
- 资源使用，通过 `top` shell 命令，682–684
- 权限
    - MySQL
    - 列级权限，512
    - 数据库级权限，512
    - 全局级权限，512, 512–513
    - 授予/撤销，512
    - 表级权限，512
- PostgreSQL，授予/撤销，517–518
- 过程语言，数据库比较，510
- 进程列表查看，297
- 进程，通过 `ps` shell 命令列出，680–681
- Procmda (邮件投代理)，483–484
- 生产力应用，133–134
- 生产力套件
    - 相关命令，151
    - 网站，152
- 编程语言，C/C++
    - 开发，613–614
- 图形化开发工具，620–621
- 项目管理工具，614–619
- 项目管理工具，C/C++ 编程语言，614
    - `autoconfig`，617
    - 调试工具，618–619
    - `make` 命令，615–617
    - Subversion 系统，617–618
- Project Planner (GNOME Office)，149
- 混杂模式 (NIC)，343, 645
- 提示符，交互式解释器 (`Python`)，562
- 协议，FTP，439
    - 服务器
    - 定义，489
    - Squid
    - ACL，491–495
    - 客户端配置，490
    - 配置示例，496–497
    - 杀-SIGHUP 命令，495
    - 指定客户端 IP 地址，495–496
    - 用途，489
- `ps` 命令，290
- `ps` shell 命令，680–681
- `ps` 客户端程序，创建 `PostgreSQL` 数据库，516
- `ps` 命令 (`PostgreSQL`)，524
- `ps` 命令行客户端，退出，517
- 清理日志，`Perl` 代码示例，555–555
- `pword` 命令，183
- PXE，235
- `Python`
    - 运算符，566
    - 运算符，566–567
    - 条件语句，条件检查，570
    - 字典，569
    - `for` 循环，570
    - 函数，定义定义，572–573
    - 无限循环，571

## 811 重定向

- 安装，561
- `while` 循环，571
- 交互式解释器，562
- Qmal MTA (邮件传输代理)，473
- 列表
- `qt` 文件，180
    - 内置方法，568
- 查询缓存，MySQL 优化，660–661
    - 复制，568
- 问号 (`7`)，shell 模式匹配
    - 可变性，567
    - 搜索，250
    - 嵌套列表，567
- 队列 (打印机)，190–193
    - 运算符重载，567

## R

- 循环块，571
- RAID 数组，307
    - 循环
- RAM 磁盘镜像 (内核)，720
    - `break` 关键字，572
- RARP (反地址解析协议)，334
    - `continue` 关键字，572
    - 多行，571
    - 数字处理
- 原始文件，156, 177
- `rc.sysinit` 脚本，236
- `rcp` 命令，SSH 服务器，373
    - 浮点值，563
    - 整数，563
- RDBMS (关系型数据库管理系统)
    - 数字类型转换，564
    - 数据存储，504
    - 大数字，564
    - 数值运算符，563
- SQL
    - 命令，空格，504
    - 类定义，573
- `CREATE` 语句，504
    - 类方法，573
- 创建表，503
    - 类，创建实例，573
- 创建表，504
    - 类，继承，575–577
    - 类，对象变量，574
- `INSERT` 语句，504–505
- 插入数据，504–505
- 留留关键字，504
    - 构造函数/析构方法，575
    - 脚本，执行，562
    - 标准库模块，577
    - 赋值给，564
    - 内置方法，566
    - 不变序列，564
    - 索引，565
    - 重复，566
    - 非官方插件，577
    - Guido，561
- 恢复模式，进入，322
- 恢复计划，647
- 重定向，248–252
- 正则表达式，430, 549–550
- 关系型数据库，501
-  Relay，Postfix MTA，478
- 远程访问
    - 基于密钥的登录，375–376
    - 配置，372–373
    - 禁用 SSH，373
    - `ftp` 命令，373
    - `rpc` 命令，373
    - `scp` 命令，374
    - `sftp` 命令，374–375
    - `ssh-keygen` 命令，375–386
    - Telnet 服务器，配置，371
    - VNC，378
- 远程客户端，X Window，345
    - 复制到其他服务器，374
    - 安全，375–376
- 可移除驱动器和介质，308
- 可移除存储介质，308
- 移除模块，207
- `renice` 命令，292, 298
- 重复语句，280
- 存储库 (软件)，配置，30–343
- 救援光盘，320
- 重置日期/时间，44
- 资源使用，通过 `top` shell 命令，682–684
- 资源 (`PHP`)，582
- 从 SQL 数据库检索数据，505–507
- 投资回报率 (ROI)，729
- `REVOKE` 语句 (`PostgreSQL`)，517–518
- `REVOKE` 语句 (`SQL`)，513
- 撤销权限
    - MySQL，512–513
    - PostgreSQL，157–161
- RhythmBox，171
- 提取音乐轨道，171
- `rm` shell 命令，681
- `rmmod` 命令，内核管理，706
- ROI (投资回报率)，729
- `root` 账户，104
    - 创建，105–106
    - 删除，107
    - 重启，101
    - 远程服务器安全，376
    - 系统关机，106–107
- `root` 权限，授予，227
- `root` 用户
    - 在 LDAP 中
    - 分配密码，527
    - 定义，526
    - 密码，511
- 网络配置工具，345–346
- 路由器，339
    - `rpm` 命令，构建 Apache 源码，411–412
    - `rsh`，247

## 813 安全

- `Run()` 方法，633
- `at` 命令，244-244
- `run-parts` 命令，245
- `batch` 命令，243–244
- 运行级别，234–236
- `cron` 守护进程，245–247
- 更改，240
- 调度任务，242
- 默认运行级别，进入，237
- Schwartzian 变换，556
    - 定义，236
- `scp` 命令，322, 374
- 非致命运行级别，进入，237–238
- 截图，168
- 故障排除，240–241
- `screen` shell 命令，686–687
- 运行时错误 (内核)，故障排除，722
- 脚本目录 (`/usr/src/linux-2.6` directory)，704

## S

- `s2p` 过滤器，555
- SCSI 磁盘驱动程序，705
- Samba
- Seamonkeychat，124
- 搜索，250
- 连接状态，390
- 安装，561
- `find` 命令，670–672
- 用户目录，388
- 模式匹配，248–250
- 手动配置，387–388
- 挂载共享，391–392
- Google 搜索，671
- Mono 库，631–634
- 打印机，389
- 配置文件，397
- `smbd` 守护进程，启动，390
- 安全焦点，648
- `for` 循环，570
- `while` 循环，571
- 交互式解释器，562
- Qmal MTA (邮件传输代理)，473
- 列表
- `qt` 文件，180
    - 内置方法，568
- 查询缓存，MySQL 优化，660–661
    - 复制，568
- 问号 (`7`)，shell 模式匹配
    - 可变性，567
    - 嵌套列表，567
    - 运算符重载，567
- 网络配置工具，345–346
- 路由器，339
    - `rpm` 命令，构建 Apache 源码，411–412
    - `rsh`，247

## 814 `redo` 语句 (`Perl`)

- 基于密钥的登录，375–376
- Linux，534
- 资源使用，通过 `top` shell 命令，682–684
- 资源 (`PHP`)，582
- 从 SQL 数据库检索数据，505–507
- 投资回报率 (ROI)，729
- `REVOKE` 语句 (`PostgreSQL`)，517–518
- `REVOKE` 语句 (`SQL`)，513
- 撤销权限
    - MySQL，512–513
    - PostgreSQL，157–161
- RhythmBox，171
- 提取音乐轨道，171
- `rm` shell 命令，681
- `rmmod` 命令，内核管理，706
- ROI (投资回报率)，729
- `root` 账户，104
    - 创建，105–106
    - 删除，107
    - 重启，101
    - 远程服务器安全，376
    - 系统关机，106–107
- `root` 权限，授予，227
- `root` 用户
    - 在 LDAP 中
    - 分配密码，527
    - 定义，526
    - 密码，511
- 网络配置工具，345–346
- 路由器，339
    - `rpm` 命令，构建 Apache 源码，411–412
    - `rsh`，247

## 815 S

- `s2p` 过滤器，555
- SCSI 磁盘驱动程序，705
- Samba
- Seamonkeychat，124
- 搜索，250
- 连接状态，390
- 安装，561
- `find` 命令，670–672
- 用户目录，388
- 模式匹配，248–250
- 手动配置，387–388
- 挂载共享，391–392
- Google 搜索，671
- Mono 库，631–634
- 打印机，389
- 配置文件，397
- `smbd` 守护进程，启动，390
- 安全焦点，648
- `for` 循环，570
- `while` 循环，571
- 交互式解释器，562
- Qmal MTA (邮件传输代理)，473
- 列表
- `qt` 文件，180
    - 内置方法，568
- 查询缓存，MySQL 优化，660–661
    - 复制，568
- 问号 (`7`)，shell 模式匹配
    - 可变性，567
    - 嵌套列表，567
    - 运算符重载，567

## shells (815)

- `vs-ftpd` servers
  - 配置，448–460
- `xinetd` daemon configuration，444

### shell command line
- 后台处理，252–253
- 输入/输出重定向，248–252
- 作控制命令，249
- 模式匹配，248–250
- 管道，248–252
- 会话写入，DVD 刻录，176
- 设置对话框，192
- `sftp` shell command，374–375, 470
- `sh` shell，247

### positional parameters，accessing/retrieving
- 命令行变量，259–261

### Shadow Password Ftp User Entry listing
- (20.1)，442
- shadow passwords，FTP users，442–443
- `shar` command，286

### shell scripts
- `#!` (shebang line)，256–258
- 内置变量，查看，258
- 作为命令，253
- 环境变量，258
- 执行，254–255
- 脚本中的函数，285–286

### SharpDevel，636
- `she` lines (`#`)，256, 258, 539
- shell commands，参见 shell command line; shell scripts; shells
- 基础命令列表，665–666
- `cat` command，666–667
- `cd` command，667–668
- `chmod` command，669
- commands，组合，684–685
- `cp` command，669
- `du` command，669–674
- `find` command，670–672
- `grep` command，673
- `less` command，674–677
- `in` command，676–677
- `locate` command，677
- `ls` command，678–679
- `man` command，679
- `mkdir` command，680
- `mv` command，680
- `ps` command，680–681
- `rm` command，681
- `screen` command，686–682
- `tail` command，682
- `top` command，682, 684
- `which` command，684
- positional parameters，访问/检索
- 命令行变量，259–261
- 使用用例，253
- 特殊字符，列表，263–264
- `startx` command，253
- 任务，操作，261–262
- 测试，262
- 特洛马脚本，255
- 用户变量，258

### variables
- 值，259
- 给变量赋值，258
- 在其中存储字符串，259

### writing
- 别名，254
- 注释，253
- 换行，253

### shells
- `bash`
  - 表达式比较，267
  - `test` command，文件比较，270–271
  - `test` command，逻辑比较，271–272
  - `test` command，数字比较，268, 270
  - `test` command，字符串比较，267–268
  - `test` command，267
- `bash`，247–248
- `break` statements，255
- `case` statements，283–284
- 更改，256
- 无限循环，277–278
- 转义字符，作为 `\` (反斜杠)，266
- `exit` statements，285
- Fedora Core shells list，247–248
- `for` statements，276–277
- `if` statements，281–282
- 作控制命令，249
- `ksh`，247
- `man` pages，248
- `pdksh`，247
- 表达式比较，267
- `select` statements，280
- `test` command，267
- `test` command，文件比较，270–271
- `test` command，逻辑比较，271–272
- `test` command，数字比较，268–270
- `test` command，字符串比较，267–268
- 位置参数，258
- `repeat` statements，280
- `rsh`，247
- `select` statements，280
- `sh`，247

### shell command line
- 后台处理，252–253
- 输入/输出重定向，248–252
- 作业控制命令，249
- 模式匹配，248–250
- 管道，248–252
- `shift` statements，281

### strings
- 嵌入空格，在其中解析变量，264–265
- 未展开的变量，维护，265–266

### `tsch`
- `repeat` statements，280
- `test` command，文件比较，274–275
- `test` command，逻辑比较，275
- `test` command，数字比较，273
- `test` command，字符串比较，292
- `tsch`，247
- `until` statements，279–280
- `while` statements，277–279
- `zsh`，247
- `` ` `` (反引号)，用输出替换字符串，266
- `shift` statements，281
- 快捷键 (键盘)，40
- `shard` command，676
- `shuffle()` function，600
- `shutdown` command，460
- `shutdown` files，魔法 cookies，460
- `shift down`，24
- 简单备份策略，306
- 单引号 (`'`)，用未展开变量维护，265–266
- Skolnik, Cliff，407
- `slash.org` website，657
- `slices` (序列)，565
- `Python` 列表拷贝，568
- 小企业备份策略，305
- 小办公室备份策略，305
- 小办公室/家庭办公室 (SOHO)，729
- 智能网关，339
- 智能主机，Postfix MTA，477
- SMB (Session Blocking) 协议，385
- `smbclient` command，Samba 连接，391
- `smbclient` command，470
- `smb` daemon，390–391
- `smbstatus` command，Samba 状态，390
- SMPs (对称处理器)，331
- SMTP: MDA，374
- 软链接，676

### software
- 备份
  - Amanda 应用，316
  - `ark`，313
  - `cdbbackup`，316
  - `flexbackup`，316
  - `dkat`，313
  - `tar`，命令行选项，310
  - `tar`，`find` command，311
  - `tar`，全量备份，311
  - `tar`，增量备份，311
  - `tar`，从备份恢复，311–312
  - `tar`，310
- FTP software，安装，441–442
- 管理
  - 添加/删除应用程序，689
  - APT，694–698
  - Synaptic，691–692
  - `tarballs`，698
- Update Manager，693
- 存储库，配置，30–36
- 软件调制调器，Linux 支持，366
- SOHO (小办公室/家庭办公室)，729
- 源码
  - 检查，618
  - `/usr/src/linux-2` 目录内核源码，704
  - 树 (内核)，makefiles，702
- Spam MDA (邮件投递代理)，484
- 速度，数据库比较，507
- `split` command (C/C++ 编程语言)，618, 622
- `split()` method，`Python` 列表，569

### SQL (结构查询语言)
- `!=` (不等于) 语句，506
- `AND` statements，506–507
- 命令，空格，504
- `CREATE` statements，504
- 数据库，从中检索数据，505–507
- `INSERT` statements，504–505
- `OR` statements，506–507
- 留关键字，504
- 语句，优化，661
- 子查询，数据库比较，509
- 表
  - 创建，503–504
  - 插入数据，504–505
  - `WHERE` statements，506

### Squid 代理服务器
- ACL，491–495
- 客户端配置，490
- 客户端 IP 地址，指定，495–496
- 配置示例，496–497
- 安装，490
- `kill-SIGKILL` command，495
- Squirrelmail MDA (邮件投递代理)，894

### SSH 服务器
- 配置，372–373
- `ftp` command，373
- `rpc` command，373
- `scp` command，374
- `sftp` command，374–375
- `ssh-keygen` command，375–376
- SSH1，禁用，373
- 与 Telnet 服务器，372

### strings
- 赋值，564
- 内置方法，566
- 拼接，566
- 不变序列，566
- 索引，565

### `PHP`
- `ssh-keygen` command，SSH 服务器，375–376

### 稳定内核对比内核开发
- 发布，709
- Stalliman, Richard M.，97, 728

### starting
- 启动/停止
  - 定义，587
  - 变量替换，587
  - 重复，566
  - 搜索，`grep` command，673–684
  - 存储在 `shell` 变量，259

### Apache Server
- `/etc/init/apache2` script，414–416
- 手动启动，413–414
- `postmaster` 程序 (`PostgreSQL`)，515
- 系统服务，手动启动/
  - 存储，241–242
- `startx` command

### shell command line
- 后台处理，252–253
- 输入/输出重定向，248–252
- 作业控制命令，249
- 模式匹配，248–250
- 管道，248–252
- `shift` statements，281

### strings
- 嵌入空格，在其中解析变量，264–265
- 未展开的变量，维护，265–266

### `tsch`
- `repeat` statements，280
- `test` command，文件比较，274–275
- `test` command，逻辑比较，275
- `test` command，数字比较，273
- `test` command，字符串比较，292
- `tsch`，247
- `until` statements，279–280
- `while` statements，277–279
- `zsh`，247

# `tar` 命令行备份软件

- 选项，310
- Fedora 核心 列表，247–248
- 从备份恢复文件，311–322
- 任务控制命令，249
- `tar` 命令，309–311, 322
- 带有意外变量的字符串维护，265–266
- `tar` 流，317
- `man` 页面，248
- `tar` 包，86, 698
- 解析带有嵌入空格的字符串中的变量，264–265
- 目标，创建 `makefiles`，615–616
- shell 命令行，输入/输出，248–252
- 任务，自动化
- shell 命令行，任务控制命令，249
    - 批处理作业号，查看，248
    - 调度任务
    - `at` 命令，242–244
    - 批处理命令，243–254
    - `cron` 守护进程，245–247
    - 调度任务，242
    - shell 脚本，261–262
    - `#` (shebang 行)，256–258
    - 内置变量，查看，263
    - 作为命令，253
    - 环境变量，258
    - 执行，254–255
    - 位置参数，访问/检索命令行变量，259–261
    - 使用原因，253
    - 特殊字符，列表 of，263–264
    - 存储供系统级访问，255–456
    - 测试，262
    - 特木马脚本，255
    - 用户变量，258
    - 变量，访问值，259
    - 变量，赋值，258
    - 变量，存储在其中，259
    - 写入，别名，254
    - 写入，注释，253
    - 写入，文本折行，253
- shell 命令行，模式匹配，248–250
- shell 命令行，管道，248–252
- shell 命令行，位置参数，259–261
- 系统服务在启动时的运行
    - 启动到非默认运行级别，237–238
    - 启动到运行级别，236
    - 更改运行级别，240
    - 通过管理工具控制服务，239
    - `init` 脚本，238
    - `init` 脚本，239
    - 启动加载过程，234–235
    - Linux 内核，235–236
    - 手动启动/停止，241–242
    - 运行级别的故障排除，240–241
- 系统服务在启动时的运行，234
- Taylor，154, 177
- TCP/IP (传输控制协议)/Internet协议，网络，328
    - 类，329–330
    - IP 伪装，331
    - IPv4 体系，329–331
    - IPv6 体系，331
    - 端口，332
- Shells
    - `` ` `` (反引号)，用输出替换字符串，266
    - `/` (反斜杠) 作为转义字符，266
    - 更改，256

# 故障排除

- `tcpdump` 命令，混杂模式，645
- `tcsh` shell，247
- `tif` 图形文件格式，166
- `time` 命令，292
- `time-admin` 客户端，更改时间/日期设置，46
- 表达式比较
    - 文件比较，274–275
    - 逻辑比较，275
    - 数字比较，273
    - 字符串比较，272
- 时间/日期重置
    - `date` 命令，45
    - `hwclock` 命令，45
    - `time-admin` 客户端，45
- 重复语句，280
- `test` 命令
    - 文件比较，274–275
    - 逻辑比较，275
    - 数字比较，273
    - 字符串比较，272
- 时间/日期重置，44
- `timewarp`，219
- TIVo，182
- 令牌环 NIC (网接口卡)，335
- 工具
- `telinit` 命令，更改运行级别，240
- `telnet` 服务
    - 配置，371
    - 对比 SSH 服务器，372
- 终端客户端，56
- 终端复用器，686
- 终端，`screen` 命令，668–687
- 三元运算符 (`PHP`)，591
- `test` 命令
    - 660–627
    - `netprbm`，169
    - `system-config-printer`，189–190
- `top` 命令，293
- `top` shell，682–684
- Torvalds, Linus，702, 727
- `touch` 命令，99
- 获取函数执行时间，619
- Transmeta, Inc.，727
- 触发器，数据库比较，510
- `trim()` 字符串函数，597
- Tripwire 安全工具，644–653
- 特木马，644
- 特木马脚本，255
    - 文件比较，270–275
    - 逻辑比较，271–275
    - 数字比较，268–273
    - 字符串比较，267–272
    - `test` 命令，267
- 故障排除
    - (内核) `/usr/src/linux-2.6` 目录，704
    - shell 脚本，262
    - `testparam` 命令，390
    - 测试 Samba，390
- Internet 连接，368
- 内核编译，721
- 内核运行时错误，722
- 网络连接，339
- NIC，341
- 文本编辑器
    - `emacs`，98–99
    - `vi`，95–97, 557
    - 文本折行，shell 脚本，253
- Thunderbird 客户端，532
- 打印机
    - 旧式打印机，403–404
    - 打印/传真设备，203
    - USB 打印机，403–404

# 故障排除

    - 运行级别，240–241
    - Ubuntu 配置，26
    - `tune2fs` 命令，文件系统优化，654
    - Ubuntu-Mobile 网站，765
    - `Python` 类型转换，564
    - 类型 (`ftpversions`)，462
    - DVD 安装版，13
    - Ubuntu 更新，20–22
    - GRUB，13
    - 分区选项，12–13
    - 密码，18–19
    - 分步指南，14–20
    - 网络中的，329
    - 概述，730
    - PPC，733
    - 关，24
    - Ubuntu 64-位，733
    - CD/DVD 驱动器，46–47
    - 日期/时间重置，44–46
    - Ubuntu 更新，28–30
    - 调制调器，42–43
    - 电源管理，43
    - 软件仓库，30–33
    - 无线网络，48–49
    - 桌面背景，34
    - 桌面颜色，35
    - 输入设备，40–41
    - 鼠标配置，41
    - 优选应用程序，37–38
    - 可移动驱动和媒体，39
    - 文档，733–735
    - 商业用，731
    - 家庭用，732–733
    - 历史，730
    - CD 安装版，312
    - Ubuntu 项目，335
    - 邮件列表，767
    - Ubuntu 救援系统，320
    - UDP (用户数据报协议)，328
    - 单播地址，334
    - 芬兰赫尔辛基大学，727
    - Unix 运行级别，305–306
    - 条件语句 (`Perl`)，856
    - `unset()` 函数，648
    - 循环 (`Perl`)，548
    - 语句，279–280
    - 包更新，699
    - Ubuntu 更新，20–22
    - 网络安全，648
    - 软件管理，693
    - Apache 服务器文件位置，410
    - 上行端口，338

# USB (通用总线)

    - 打印机，故障排除，403–404
    - 扫描仪，166
    - Usenet 组，766
    - 用户账户，81
    - Fetchmail 配置，481–483
    - 添加到 MySQL，512
    - FTP 服务器，显示，464–465
    - 管理员邮箱地址，455
    - 登录幅，352
    - 上传文件，453–455
    - 最后修改日期，455–456
    - `/var/spool/cron` 目录，246
    - 运行，245
    - 用户命令，105
    - FTP 用户，422–444
    - 授权，224–229
    - `UserDir` 配置 (`Apache` 服务器)，419
    - UTP (非屏蔽双绞) 电缆，337
    - `dump()` 函数，605–606
    - 变量替换 (`PHP`)，587
    - `Python` 中的类对象，574
    - 交互式解释器 (`Python`)，处理，562
    - Mono，629–630
    - `Perl` 变量，540–550
    - 特殊变量，541
    - 类型，581
    - 数组，582–583
    - shell 脚本
        - 内置，258–263
        - 内置，查看，263
        - 环境，258
        - 存储字符串，259
        - 用户，258
        - 访问值，259
        - 赋值，258
        - 未扩展的变量，265–266
    - 批处理作业号，244
    - `vi` 命令，286
    - `vi` 编辑器，557
    - `vim`，96
    - 视频卡 X Window 系统，861
    - VideoLAN HOWTO，182
    - 虚拟文件系统，878
    - Apache Web 服务器虚拟主机，432
    - 值函数，`Perl` 哈希表，541
    - van Rossum, Guido，561

# Apache Web 服务器虚拟主机

- 内网网站，433
- 文档网站，408
- 基于名称的主，432–434
- 下载，409
- 病毒扫描仪，484, 646
- 文件系统访问控制，422–425
- 视觉效果，修改，377
- 文件系统身份验证，423–425
- `visudo` 命令，227
- 安装文件位置，412
- `vmstat` 工具，294
- 从 APT 安装，409–410
- VNC (虚拟网络计算)，378
- `vncviewer` 工具，296
- 网络安全，422
- `vsftpd` 命令，470, 440
- 日志，常用格式，434
- 日志，`CustomLog` 指令，435
- 匿名访问，控制，446
- 配置，445–448
- `mod_access` 模块，427
- `vsftpd`，470, 440
- `mod_alias` 模块，427
- 漏洞评估 (安全)
- `mod_aside` 模块，427
- Nessus，641–642
- `mod_auth` 模块，428
- Nmap，642
- `mod_auth_anon` 模块，428

# 编写 脚本 825

- `mod_userdir` 模块，431
- `mod_usertrack` 模块，431
- `mod_vhost_alias` 模块，409
- `mod_vhost_alias` 模块，372
- 优化，655-658
- 快速上手指南，412
- 运行时配置，配置指令，416-421
- 运行时配置，`httpd` 配置，416
- 运行时配置，MPM，419
- 安全报告网站，409
- 源代码网站，410
- 启动/停止，手动启动，413-414
- 启动/停止，`/etc/init.d/apache2` 脚本，414–416
- 升级，文件位置，410
- 使用统计，407
- 版本信息，409
- 通过 `allow`/`deny` 条目，422–432
- 虚拟主机，基于地址的主机，432–433
- 虚拟主机，基于名称的主机，432–434
- Sun ONE，436
- Zeus，网站，436
- Zope，网站，436
- `webcam.msg` 文件，470
- `welcome.msg` 文件，45
- WEP 加密，409
- `whatis` 命令，85
- `WHERE` 子句，`SELECT` 语句，505
- `WHERE` 语句 (`SQL`)，506
- `whereis` 命令，85, 94
- `which` shell 命令，684
- `while` 循环，593
- `Perl`，548
- `Python`，571
- `while` 语句，277-279
- 空格，SQL 命令，504
- 通配符，85, 250
- 窗口管理器，修改，73-76
- Windows，生产力应用，150–151
- Wine，150-151
- WinModems，笔记本电脑配置，42–43
- 无线网络，336
- 优势，359
- 选择可用协议，359–360
- 弄清楚，48–49
- 加密，49
- 安全，642
- 接入点，643
- OpenSSH 工具，643
- 支持
- `iwconfig` 命令，357–358
- `iwlist` 命令，357
- `ipriv` 命令，357
- `iwspy` 命令，357
- 无线驱动，643
- `wish` 命令，257
- `WITH PASSWORD` 段 (`CREATE` 语句)，516
- `worker` MPM (多进程模块)，Apache 服务器配置，419
- WPA Personal 加密，49
- `WriteLine()` 方法，629
- Writer (`OpenOffice.org`)，134
- 选项，139
- 样式和格式，139-140

## 编写脚本
- 别名，254
- 注释，253
- 文本换行，253

我们如何让这个索引更有用？请发送邮件至 indexes@sampsublic.com

## 826 `wu-fptd` 服务器

`wu-fptd` 器

`Xfce` 桌面，78, 656
- 访问控制，配置，449–452
- `ftprocess` 文件命令，449–480
- 权限控制，配置，457–459
- 系统日志，配置，456–457
- 用户信息，配置，452–455
- `xinetd` 守护进程，配置，444

`Xine`，182
- `xinetd` 守护进程，针对 `wu-fptd` 服务器配置，444

## `xorg.conf` 文件
- 设备部分 (`Device section`)，60–61
- 文件部分 (`Files section`)，58
- 输入设备部分 (`InputDevice section`)，59
- 模块部分 (`Module section`)，59–60
- 屏幕部分 (`Screen section`)，61–62

## X-Y-Z

### X Window 系统
- 应用，56–57
- 组件列表，57–58
- 组成，57
- 配置，62
- 显示管理器 (`display managers`)，56
- `displayconfig gtk` 客户端，63–64
- 分布式处理，55
- 分发组件，56
- 元素，55–59, 62
- 硬盘要求，56
- 模块部分 (`Module section`)，59
- 监控器部分 (`Monitor section`)，56
- 概述，55
- 参考文献，78
- 布局部分 (`ServerLayout section`)，58
- 启动，64
- 通过显示管理器，65
- 网站，765

X Window 系统配置，64

`Xsane` 扫描仪，165–166

### Zeus Web 服务器
- 网站，436

### `zimage` 指令
- 内核编译，714

### Zope Web 服务器
- 网站，436

### `zsh` shell，247

`X-Chat`，124–125
`x-x`，shell 模式匹配搜索，250
`X.Org Foundation`，728
`X11`，51
`xdm` 显示管理器，应用，73
`XDMCP` (`X` 显示器协议)，68, 71, 377

## 相关 Linux 和开源书籍

- `Fedora Unleashed 2008`，Andrew 和 Paul Hudson，ISBN-13: 978-0-672-32977
- `openSUSE Unleashed`，Michael McCallister，ISBN-13: 978-0-672-32945
- `FreeBSD 6 Unleashed`，Brian Tiemann，ISBN-13: 978-0-672-32875
- `Red Hat Enterprise Linux 5 Administration`，Tammy Fox，ISBN-13: 978-0-672-32892
- `Sams Teach Yourself PHP, MySQL and Apache All in One`，Julie Meloni，ISBN-13: 978-0-672-32976
- `PHP Phrasebook`，Christian Wenz，ISBN-13: 978-0-672-32817
- `Linux Firewalls`，第三 Edition，Steve Suehring 和 Robert L. Ziegler，ISBN-13: 978-0-672-32711
- `Linux Phrasebook`，Scott Granmann，ISBN-13: 978-0-672-32838
- `Apache Phrasebook`，Daniel Lopez，ISBN-13: 978-0-672-32836
- `Linux Kernel Development`，Robert Love，ISBN-13: 978-0-672-32720
- `MySQL Phrasebook`，Zak Green 和 Chris Newman，ISBN-13: 978-0-672-32839
- `SUSE Linux Enterprise Server 9's Handbook`，Peter Kuo 和 Jacques Jaqués，ISBN-13: 978-0-672-32735
