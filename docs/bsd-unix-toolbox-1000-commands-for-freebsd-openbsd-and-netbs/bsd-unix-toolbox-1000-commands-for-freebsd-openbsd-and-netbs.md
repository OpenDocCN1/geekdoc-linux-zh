
# BSD UNIX 工具箱：FreeBSD、OpenBSD 和 NetBSD 高级用户的 1000+ 条命令

## 关于作者

Christopher Negus 编写了多本畅销书，包括《Linux Bible》（第8版）。自 2003 年以来，他一直致力于 Linux 社区。他是一名 Red Hat 认证工程师。

François Caen 编写了多本书籍，包括《Linux Bible》（第8版）。他一直致力于 Linux 社区。

## 致谢

我将本书献给我的妻子 Sheree。

## 关于编辑

Wiley 标志及相关商标是 John Wiley & Sons, Inc. 及其或其关联公司在美国及其他国家的商标或注册商标，未经书面许可不得使用。

## 制作团队

- 采购编辑：Jenny Watson
- 执行编辑：Joseph Wikert
- 开发编辑：Thomas Blader
- 项目协调：Laurie Stewart
- 技术编辑：Daniel Parise
- 校对：Melanie Belkin
- 编者：Michael Koch
- 制作编辑：Mary Wakefield
- 制作经理：Tim Swadle

## 关于出版

Wiley Publishing, Inc. 提供多种格式的书。

## 目录

致谢 xix

引言 xxi

# 第 5 章：处理文本 71

使用正则表达式匹配文本 71

编辑文本文件 72

+ 使用 `JOE` 编辑器 73
+ 使用 `Pico` 和 `Nano` 编辑器 76
+ 图形化文本编辑器 78

## 列出、排序和更改文本 78

+ 列出文本文件 78
+ 分页查看文本 79
+ 使用 `pr` 对文本文件分页 80
+ 使用 `grep` 搜索文本 81
+ 使用 `sed` 替换文本 83
+ 使用 `tr` 翻译或删除字符 84
+ 使用 `diff` 检查两个文件的差异 85
+ 使用 `awk` 和 `cut` 处理列 87
+ 将文件转换为不同的格式 88

## 总结 88

# 第 6 章：多媒体玩 89

## 处理音频 89

+ 从音频开始 89
+ 播放音乐 90
+ 调整音频电量 91
+ 刻录 CD 音乐 92
+ 音乐编码 93
+ 转换音频文件 96

## 图像 97

+ 获取图像信息 97
+ 转换图像 98
+ 批量转换图像 100

## 总结 101

# 第 7 章：文件系统管理 103

## 理解文件系统基础 103

+ 初始磁盘设置 104
+ 检查你的磁盘设置 104
+ 理解文件系统类型 106

## 创建和管理文件系统

+ 硬盘分区 107
- 使用 Linux 兼容的文件系统 114
- 创建内存磁盘文件系统 116
- 创建和使用交换分区 117

## 挂载和卸载文件系统

+ 从 `fstab` 文件挂载文件系统 118
- 使用 `mount` 命令挂载文件系统 120
- 使用 `umount` 卸载文件系统 121

## 检查文件系统

## 了解文件系统使用情况

+ 总结 126

# 第 8 章：备份和可移动媒体

## 将数据备份到压缩存档

+ 使用 `tar` 创建备份归档 127
- 使用压缩工具 129
- 列出、合并和向 `tar` 归档添加文件 132

## 通过网络备份

+ 通过 `ssh` 备份归档 133
- 使用 `rsync` 备份文件 134
- 使用 `unison` 备份 136
- 备份到可移动媒体 137
- 使用 `mkisofs` 创建备份镜像 137
- 使用 `cdrecord` 刻录备份镜像 140
- 使用 `growisofs` 制作并刻录 DVD 141
+ 总结 142

# 第 9 章：检查和管理运行进程

## 列出活动进程

+ 使用 `ps` 查看活动进程 144
- 使用 `top` 监控活动进程 150

## 查找和控制进程

+ 使用 `pgrep` 查找进程 152
- 使用 `fuser` 查找进程 152
+ 总结 159

# 第 10 章：系统管理

+ 监控资源 161

监控内存占用 162

监控 CPU 使用率 164

监控存储设备 166

精通时间 168

更改时区 169

显示和设置你的时间和日期 169

使用网络时间协议 (NTP) 设置日期时间 170

检查运行时间 (`uptime`) 172

管理启动过程 172

使用 `boot0` 引导程序 173

使用 `bsdlabel` 检查分区 176

切换到 `GRUB` 引导程序 176

控制系统服务 178

启动和停止你的系统 179

直接进入内核 179

接触硬件 182

总结 183

# 第 11 章：管理网络连接

（注：原文中此章节重复多次，已去重）

# 引言

`BSD UNIX Toolbox` 为你提供了超过 1,000 种特定的命令行，帮助你成为 BSD 进阶用户。无论你是系统管理员还是桌面用户，本书都将向你展示如何创建文件系统、排查网络故障、锁定安全性，以及挖掘你感兴趣的关于 BSD 系统的任何信息。

在你的 BSD 命令行之旅中，本书的关注重点是 `FreeBSD`，它是世界上最受欢迎的 BSD 衍生版本之一。掌握运行这些系统所需的技能，可以帮助你处理你自己的 BSD 系统，并学习你作为 BSD 专业人士所需要的的知识。

## 谁应该读这本书

本书适用于任何想要以系统管理员或用户身份访问 BSD 系统强大功能的人。你可能是一个自由和开源软件（`FOSS`）爱好者、一个 BSD 专业人士，也可能是一个计算机专业人士，你发现自己数据中心中的 `Windows` 系统正日益被 BSD 和 `Linux` 机器所取代。

核心要点是，你希望找到快速、高效的方法，让 `FreeBSD`、`NetBSD` 和 `OpenBSD` 系统以最佳性能运行。这些系统可能是你工作中的几台桌面系统、你学校的文件和打印服务器，或者是你为了兴趣搭建的家庭 `Web` 服务器。

在理想情况下，你应该已经拥有 BSD、`Linux` 或其他 `Unix` 类系统的经验。然而，如果你是一个拥有管理其他类型操作系统（如 `Windows`）技能的计算机专业人士，你应该能够轻松地调整你的知识，以使用书中涵盖的特定命令。

## 本书涵盖的内容

这不是一本面向初学者的 BSD `UNIX` 书。在开始之前，你最好已经对 BSD 以及其他 `Unix` 系统是什么、壳（`shell`）如何工作，以及进程、文件系统和网络接口具有基本的运作知识。随后，本书将为你提供执行以下活动所需的信息，补充这些知识：

- 获取软件 —— `FreeBSD` 在 `ports` 数据库中同时提供二进制软件包和源码包，可用于从源代码下载、构建和安装软件。通过 `pkg_info`、`pkg_add` 和 `pkg_delete` 等工具，你将学习从命令行查找、下载、安装以及其他管理软件的最佳方法。

- 访问应用程序 —— 查找 `FreeBSD` 发行的可用程序，然后使用 `sysinstall` 工具选择并安装你需要的程序。

- 使用 `shell` —— 查找 `shell` 的精妙技巧和提示。

- 玩转多媒体 —— 在你的电脑上播放和处理多媒体内容。你还可以修改音频和图像，并将这些文件的内容转换为不同的格式。

- 处理文件 —— 在 BSD 系统中使用、操作、转换和保护各种类型的文件。

- 管理文件系统 —— 访问、格式化、分区和监控你的文件存储硬件（硬盘、`CD`/刻驱动器、软磁盘、`USB` 闪盘等）。然后在这些硬件设备上创建、格式化和检查文件系统。

- 备份恢复数据 —— 使用命令将你的文件收集、存档并压缩为高效的备份存档。然后将其存储在本地或远程计算机上。

- 处理进程 —— 以多种方式列出运行进程，例如 `CPU` 使用率、处理器使用或进程 `ID`。更改运行进程使其在后台或前台运行。向进程发送信号使其重新读取配置文件、停止和恢复处理，或完全停止（终止）。

- 管理系统 —— 运行命令检查系统资源，如内存使用、启动加载程序和内核模块。

- 监控网络 —— 启动和关闭有线、无线和拨号网络连接。检查路由、`DNS` 和主机信息。监控网络流量。

- 获取网络资源 —— 使用 `FTP`、`NFS` 和 `Samba` 工具连接 BSD 和 `Windows` 远程文件系统。使用基于 `shell` 的命令浏览网页。

- 执行远程管理 —— 使用远程登录（`ssh`、`telnet` 等）和屏幕访问并管理其他计算机。学习远程管理接口，如 `SWAT` 和 `CUPS`。

- 锁定安全性 —— 设置防火墙和系统日志以确保你的安全。

*(注：原文后半部分存在大量重复段落，译文已根据“不要重复输出原文”的要求进行了去重处理，保留了核心内容)*

## 引言

书中描述的许多命令在其他 `UNIX` 和 `Linux` 系统上同样适用。由于本书侧重于 `FreeBSD` 以及其他基于 BSD 的发行版，因此其描述与其他类 `Unix` 系统的区别最显著之处体现在软件包、安装和 `GUI` 管理工具方面。

# 约定

为了帮助你从文本中获取最大信息并跟踪操作进度，我们在整本书中使用了许多约定。特别是，我们为显示命令创建了样式，以便在书中尽可能容纳更多的命令行行。

在带有命令示例的情况下，命令输出（`shell` 提示符和消息）用普通等宽字体显示，计算机输入（你输入的内容）用粗体等宽字体显示，而简短描述（如果有）则以斜体显示。以下是一个示例：

```
$ ls *jpg          列出当前目录下的 JPEG 文件
hat.jpg
dog.jpg
...
```

为了节省空间，输出会被截断（或完全跳过）。三个点（`...`）有时用于表示额外的输出被截断了。如果一个命令特别长，每行末尾会出现反斜杠，表示输入将延续到下一行。以下是一个示例：

```
# oggencSong.wav -o NewSong.ogg \
-a Bernstein -G Classical \
-d 06/15/1972 -t "Simple Song" \
-1 "Bernsteins Mass" \
-c info-*"From Kennedy Center"
```

在刚才展示的示例中，你可以输入反斜杠将所有信息包含在单个命令中。或者，你也可以将所有信息放在一行（不包括反斜杠）。注意，命令提示符以两种方式之一显示：

```
$          表示普通用户提示符
#          表示 root 用户提示符
```

如所述，当出现美元符号提示符 (`$`) 时，任何用户都可以运行该命令。当出现井号提示符 (`#`) 时，你可能需要作为 `root` 用户才能运行命令。

注释和警告显示如下：

NOTE: 警告和注释会偏移并以斜体显示，如下所示。

关于文中的样式：

- 我们在引入新术语和重要词汇时使用斜体进行突出显示。

- 我们这样显示键盘输入：`Ctrl+A`。如果命令要求你输入大写字母，组合键将显示为：`Ctrl+Shift+A`。

- 我们在文中这样显示文件名、`URL` 和代码：`persistence.properties`。

我们使用的最后一种技术是突出显示描述即将出现的命令用途的文本。例如，我们可能会说：“使用以下命令来**显示文件的内容。**”我们以这种样式设计描述，是为了为读者提供快速的视觉提示，让你能够轻松扫描页面并找到你刚刚知道在那里的命令。

## 从 BSD 系统开始

无论你是每天使用 BSD 系统，还是只是偶尔进行调整，一本提供高效方法来使用、检查、修复、保护和增强系统的书籍都将是一份无价的资源。

《BSD UNIX Toolbox》就是这一资源。

《BSD UNIX Toolbox》主要面向 BSD 高级用户和系统管理员。为了提供你所需的内容，我们将教你如何快速定位并获取软件、监控系统的健康和安全、使用图标以及访问网络资源。简而言之，我们直击核心，介绍了使用 BSD 系统的最有效方法。

《BSD UNIX Toolbox》的目标是将许多用于系统的有用信息封装在一个你可以随身携带的小型包中。为此，我们描述了：

- 命令：大量的命令行示例，帮助以实用且清晰的方式使用 BSD 系统

- `GUI` 工具：快速配置系统的图形化管理工具指南

- 软件包：查找和下载大量应用程序的简短步骤

- 在线资源：寻找 BSD 论坛、邮件列表、`IRC` 通道和其他在线资源的最佳位置列表

- 本地文档：用于从帮助页（`man` pages）、`doc` 目录、帮助命令以及 BSD 系统上的其他资源中收集更多信息的工具

由于你不是 BSD 系统的初学者，你不会看到很多窗口、图标和菜单的截图。然而，你将看到的是获取所需信息以充分利用你的 BSD 系统的最快路径。

如果这听起来对你有用，请继续阅读。

## 关于 FreeBSD、NetBSD、代码和 OpenBSD

在 20 世纪 70 年代初，`AT&T` 将 `UNIX` 源代码发布给几所学院大学，让他们能够根据意愿开始修改、调整和改进这些代码。这一决定导致了每一个主要的自由和开源操作系统的开发，其中许多系统基于伯克利软件发行版（`BSD`）。

如果你对 BSD 曲折的历史感兴趣，很容易在 `Google` 上搜索。对于我们的目的，只需说：

- BSD 起初是 `AT&T` 第六版 `UNIX` 的一套软件插件。

- 多年来，BSD 开发人员开启了自己的开发路线，重写软件旨在取代所有受 `AT&T` 版权保护的代码。

- 20 世纪 90 年代初，`AT&T` 的 `Unix` 实验室起诉 BSD 开发人员（`Berkeley Software Design, Inc.`）侵犯版权。

- 1995 年，伯克利发布的最后一个版本的 BSD 以 `4.4BSD-Lite` 的名称发布。如今的 BSD 操作系统（包括 `FreeBSD`、`NetBSD` 和 `OpenBSD`）在某种程度上都基于 `4.4BSD-Lite`。

# 第 1 章：从 BSD 系统开始

如果你以前用过 `Linux`，那么过渡到 BSD 系统不应该太难。然而，BSD 系统的行为往往更像旧的 `UNIX` 而不是 `Linux`。许多界面是基于文本的

以下是仍在开发的流行的基于 BSD 的操作系统列表：



`FreeBSD` (`freebsd.org`) 是 BSD 发行版中最受欢迎的。它可以作为服务器、工作站运行，也被用于网络设备。它以极高性能闻名。

`NetBSD` (`netbsd.org`) 以非常受欢迎而闻名，其版本可作为嵌入式系统运行。`NetBSD` 可以运行在从 32 位和 64 位 PC 到个人数字助理（PDA）的任何设备上。

`OpenBSD` (`openbsd.org`) 是网络服务器的流行系统，尽管也可以作为工作站运行。`OpenBSD` 的目标是实现最大的安全性。与受 BSD 许可证保护的 `FreeBSD` 和 `NetBSD` 不同，`OpenBSD` 主要受互联网系统协会 (ISC) 许可证保护。

`DragonFly BSD` (`dragonfly.org`) 最初基于 `FreeBSD`。它的目标是在对称多处理和并发等领域开发与 `FreeBSD` 不同的技术。其重点在于扩展内核功能。

其他基于 BSD 的自由（指无成本，且可以自由地对代码做任何事）操作系统包括 `Darwin`（`Mac OS X` 基于此）以及面向桌面的系统如 `PC-BSD` 和 `DesktopBSD`。`FreeBSD` 是一个 Live CD BSD 系统。源自 BSD 的专用操作系统包括：

`Mac OS X` (`apple.com/macos`) 由 Apple 生产，侧重于添加易于使用的图形化界面以随其系列电脑销售。还有 `Mac OS X Server` 产品可用。尽管 `Mac OS X` 最初基于 `Darwin`，但它被认为是一种带有开源组件的闭源操作系统。

# 第1章：从 BSD 系统开始

你可以在 DistroWatch 网站（`http://distrowatch.com/search.php?category=BSD`）找到更详尽的 BSD 发行版列表。除了提供这些 BSD 发行版的描述外，你还可以找到购买或下载这些软件的链接。

## 寻找 BSD 资源

尽管现在仍然存在一个 BSD 网站（`www.bsd.org`），但它很大程度上仅充当指向与特定 BSD 发行版相关资源的指针。以下章节包含了与 `FreeBSD`、`NetBSD` 和 `OpenBSD` 相关的有用链接。

## FreeBSD 资源

以下是来自 `FreeBSD` (`www.freebsd.org`) 的有用资源链接：

- `FreeBSD` 支持 (`freebsd.org/support.html`) — 你可以在这里找到 `FreeBSD` 社区和商业支持的联系。

- 获取 `FreeBSD` 软件 (`freebsd.org/where.html`) — 该网站列出了下载或购买 `FreeBSD` 安装 CD 或 DVD 的信息。这包括不同架构（`i386`, `amd64`, `powerpc` 等）的软件。

- `FreeBSD` 特性列表 (`freebsd.org/about.html`) — 描述了 `FreeBSD` 的关键特性。

- `FreeBSD` 新闻 (`freebsd.org/news/`) — 这是 `FreeBSD` 新闻的聚集地。这里有新闻提要、新闻稿、文章和开发状态的链接。你还可以找到与 `FreeBSD` 以及通用 BSD 相关的开发站点和论坛链接。

- `FreeBSD` 项目 (`freebsd.org/projects/`) — 提供有关 `FreeBSD` 开发项目的信息。除了 `FreeBSD` 的基础开发项目外，你还可以找到特殊项目（如 `Google Summer of Code`）以及与现有开源项目（如 `Java`, `GNOME`, `KDE` 和 `OpenOffice.org`）相关的 `FreeBSD` 计划的链接。

## NetBSD 资源

以下是来自 `NetBSD` 网站 (`www.netbsd.org`) 的有用资源链接：

- `NetBSD` 支持 (`netbsd.org/support`) — 提供有关社区和专业支持、支持的硬件、漏洞提交和安全的信息。

- 获取 `NetBSD` 软件 (`netbsd.org/releases`) — 该网站列出了下载 `NetBSD` CD 或 DVD 的信息。提供了通过 `Torrent`、`FTP` 和 `HTTP` 方法下载软件。

- 关于 `NetBSD` (`netbsd.org/about`) — 描述了 `NetBSD` 的关键特性。

- `NetBSD` 新闻 (`netbsd.org/changes/`) — 包含 `NetBSD` 的最新新闻。这包括 `NetBSD` 开发变更的持续列表。

- 软件包 (`netbsd.org/docs/software/packages.html`) — 查找有关 `NetBSD` 软件包集合 (`pkgsrc`) 的信息。这包括可用软件包、文档和支持平台的信息。

## OpenBSD 资源

以下是来自 `OpenBSD` 网站 (`www.openbsd.org`) 的有用资源链接：

- `OpenBSD` 支持 (`openbsd.org/support.html`) — 提供全球范围内适用于 `OpenBSD` 的商业支持和咨询信息。

- 获取 `OpenBSD` 软件 (`openbsd.org/ftp.html`) — 通过 `FTP`、`HTTP`、`ASF` 和 `RSYNC` 提供下载 `OpenBSD` CD 或 DVD 的信息链接。

- `OpenBSD` 项目目标 (`openbsd.org/project.html`) — 描述了 `OpenBSD` 项目的目标。

- `OpenBSD` 新闻 (`openbsd.org/press.html`) — 包含 `OpenBSD` 的媒体报道链接。

- 常见问题 (`cvs.openbsd.org/faq`) — 包含 `OpenBSD` 的常见问题 (`FAQ`) 列表。

## BSD 社区连接

如果你想与 `FreeBSD`、`OpenBSD` 或 `NetBSD` 社区交流，表 1-1 显示了与这些项目相关的最常用交流地的快速列表。

## 表 1-1：连接 BSD 社区的在线资源

| BSD 活动 | 互联网站点 |
|---|---|
| 邮件列表 | `lists.freebsd.org/maillist/listinfo`<br>`www.openbsd.org/mail.html`<br>`www.netbsd.org/mailinglists` |
| `IRC` 聊天 | `www.netbsd.org/community/#chat`<br>`www.freebsd.org/community/irc.html` |
| 论坛 | `www.bsdforums.org`<br>`www.bsdnexus.com`<br>`www.freebsdwiki.net` |
| 博客 | `planet.freebsdish.org` |

表 1-1：连接 BSD 社区的在线资源（续）

| BSD 活动 | 互联网站点 |
|---|---|
| 社区 `Wiki` | `wiki.netbsd.se` |
| `Usenet` 新闻组 | `News:comp.unix.bsd.freebsd.misc`<br>`News:comp.unix.bsd.freebsd.announce`<br>`News:comp.unix.bsd.netbsd.announce`<br>`News:comp.unix.bsd.netbsd.misc`<br>`News:comp.unix.bsd.misc` |
| 文档 | `www.freebsd.org/docs.html`<br>`www.openbsd.org/cgi-bin/man.cgi`<br>`netbsd.org/docs` |
| 新闻 | `news.vejas.lt` |

## 聚焦 BSD 命令

如今，BSD 中的许多重要任务既可以通过图形界面完成也可以通过命令行完成。然而，命令行一直以来并仍然是 BSD 高级用户的首选界面。

图形用户界面 (`GUI`) 看起来可能是直观的。有了一定的经验后，你可能可以弄出，例如如何添加用户、更改日期以及为 `GUI` 配置声卡。对于这些情况，我们会提到需要使用哪种图形工具。对于以下情况，你可能需要命令行：

- 几乎在出现任何问题时通过在线论坛提问来解决问题。此外，命令行工具提供更多反馈。

- 远程系统，如果你在管理服务器，你可能可以使用图形工具。尽管远程访问（使用 `X` 应用或 `VNC`）可能是可用的，但

- `GUI` 工具不支持的功能倾向于提供执行任务最基本的方法。更复杂的操作通常需要仅适用于：

- `GUI` 损坏或未安装——如果没有图形界面，或者安装的 `GUI` 运行不正常，你可能被迫从命令行工作。`GUI` 损坏可能由许多原因引起，例如当你使用仅二进制驱动程序时，内核升级导致驱动程序不兼容。此外，BSD 服务器甚至没有安装 `GUI`。

底线情况是，要释放你 BSD 系统的全部威力，你必须能够使用 `shell` 命令。成千上万的命令可用于监控和管理系统的各个方面。

但无论你是 BSD 大师还是新手，一个巨大的挑战横在面前。你该如何记住你所需的关键命令和选项，当命令 `shell` 可能只向你：

`BSD UNIX 工具箱` 不仅仅是另一个命令参考书或手册页的重述。相反，本书按照你使用命令的方式介绍了 BSD 系统中的命令。换句话说，我们没有按字母顺序列出命令，而是将用于文件系统、连接网络和管理进程的命令分在不同的章节中，以便你根据你想做什么来访问命令，而不仅仅根据它们是如何命名的。

同样，我们不会提供每个命令可用选项的列表。相反，我们将向你展示使用每个命令的最重要且实用的选项的运行示例。从那里，如果你需要更多选项，我们将告诉你快速查找的方法，即通过手册页、`info` 设施和 `help` 选项。

## 寻找命令

书中描述的所有命令在你运行它们时可能并未安装。你可能输入一个命令并看到类似下面的消息：

```
mycommand: command not found
```

这可能由以下原因引起：

- 你拼写错误了命令名称。

- 命令不在你的 `PATH` 中。

- 你可能需要 `root` 用户权限命令才会出现在 `PATH` 中。

- 你的电脑上没有安装该命令。

表 1-2 显示了一些你可以运行的命令，用于查找你想使用的命令。

## 第一章：从 BSD 系统开始

| 表 1-2：查找命令 |
| :--- | :--- |

| 命令与示例输出 | 描述 |
| :--- | :--- |
| `$ type mount`<br>`mount is /sbin/mount` | 显示 `PATH` 中第一个 `mount` 命令。 |
| `$ whereis mount`<br>`mount:/sbin/mount`<br>`/usr/share/man/man/mount.8.gz` | 显示 `mount` 的二进制文件和帮助页（`man page`）。 |
| `$ locate xrdb.1.gz`<br>`/usr/local/man/manl/xrdb.1.gz` | 在文件系统的任何地方查找 `xrdb.1.gz`。 |
| `$ which umount`<br>`/sbin/umount` | 在你的 `PATH` 或别名中查找 `umount` 命令。 |
| `$ pkg_info -W convert`<br>`/usr/local/bin/convert`<br>`installed by package ImageMagick-6.3.6.9` | 查找 `convert` 命令来自哪个软件包。 |

如果你怀疑所需的命令没有安装，可以搜索 `ports` 数据库查找该命令所属的包。如果你找到了正确的包（例如 `bzflag`）但它尚未安装，可以以 `root` 身份输入以下命令从互联网安装：

```bash
# find /usr/ports | grep ImageMagick
/usr/ports/graphics/ImageMagick

# pkg_add -r ImageMagick
```

刚刚显示的命令从 BSD 软件仓库获取 `ImageMagick` 二进制包（`tar bzip2` 格式）并从本地系统进行安装。有关安装软件的其他方法（例如使用 `ports` 系统），请参阅第二章。

## BSD 中的命令参考信息

原始的 BSD、Linux 和 UNIX 文档都是通过手动页（manual pages）完成的，通常称为 `man`。稍后 `info` 设施引入了一项稍微复杂的文档工作。在每个命令内部，几乎总是可以找到帮助消息。

这些参考信息是面向组件的——换句话说，BSD 系统的每个命令、文件格式、系统调用、设备和其他组件都有单独的 `man` 页。与整个软件软件包结合得更紧密的文档通常存储在 `/usr/local/share/doc` 目录的子目录下。

三个参考功能——`man` 页、`info` 文档和帮助消息——在 BSD 系统中均可用。

## 第一章：从 BSD 系统开始

### 使用帮助消息

`-h` 或 `--help` 选项通常用于显示命令的帮助消息。示例说明了如何显示 `ogg123` 命令的帮助：

```bash
$ ogg123 --help | less
ogg123 from vorbis-tools 1.1.1
by the Xiph. Foundation (http://www.xiph.org/)

Usage: ogg123 [<options>] <input file> ...

-h, --help this help
-V, --version display Ogg123 version
-d, --device d uses 'd' as an output device
Possible devices are ('=live, '=file):
oss* null* raw@ au
-f, --file=filename Set the output filename for a previously
specified file device (with -d).
```

之前的输出显示了如何使用 `ogg123` 命令并列出了可用的选项。将输出通过到 `less` 命令可以让你对内容进行分页查看。

### 使用 man 页

假设你想查找与某个单词相关的命令的 `man` 页。使用 `apropos` 命令搜索 `man` 数据库。这会显示 `NAME` 行中包含 `crontab` 的 `man` 页：

```bash
$ apropos crontab
contab(1) - maintain crontab files for individual users (V3)
contab(5) - tables for driving cron
```

`apropos` 的输出在这里显示了包含 `crontab` 的每个 `NAME` 行。数字显示了 `man` 页所在的章节（我们稍后会讨论这些章节）。

`whatis` 命令是仅单独显示包含你输入单词的命令的 `NAME` 行的方法：

```bash
$ whatis cat
cat (1) - concatenate files and print on the standard output
```

显示某个术语 `man` 页的最简单方法是使用 `man` 命令和 `man` 名称。例如：

```bash
$ man
FIND(1) FreeBSD General Commands FIND(1)
NAME walk -- a file hierarchy
```

## 第一章：从 BSD 系统开始

语法 (`SYNOPSIS`)

```
find [-H] [-L] [-P] [-Exdsx] [-f pathname] [pathname ...] expression
```

上面的命令显示了 `find` 命令的 `man` 页。正如你在之前的示例中看到的，某些术语有多个 `man` 页。例如，`crontab` 命令有一个 `man` 页，`crontab` 文件也有一个。`man` 页被组织在不同的章节中，如表 1-3 所示。

### 表 1-3：man 页章节

| 章节 | 描述 |
| --- | --- |
| 1 | 通用用户命令 |
| 2 | 系统调用 |
| 3 | 编程例程 / 库函数 |
| 4 | 设备 |
| 5 | 配置文件和文件格式 |
| 6 | 游戏 |
| 7 | 其他 |
| 8 | 管理命令和守护进程 |
| 9 | 内核接口 |

下面的代码显示了 `man` 命令的一些其他有用选项示例。

```bash
$ man -a mount               显示与组件相关的所有 man 页
$ man 5 crontab             显示组件的第 5 节 man 页
$ man mount -P more          使用 more 而不是 less 进行分页
$ man -f mount                与 whatis 命令相同
$ man -k mount               与 apropos 相同
```

互联网上也可以找到 `man` 页：

```
http://freebsd.org/man
http://openbsd.org/man
http://netbsd.org/man
```

## 第一章：从 BSD 系统开始

### 使用 info 文档

遵循早期 UNIX 系统的传统，`FreeBSD` 提供了一个名为 `sysinstall` 的文本安装设施。该安装程序面向关注功能和灵活性而非图形界面的人士。初始化后运行 `sysinstall` 可以添加更多包并配置网络设置。

```bash
$ info ls
```

### 表 1-4：info 移动

| 按键 | 移动 |
| --- | --- |
| `?` | 显示帮助 |
| `L` | 返回上一页 |
| `n, p, u` | 进入下一页 |
| `Tab` | 进入下一项 |
| `Enter` | 进入光标处 |
| `R` | 遵循交叉引用 |
| `Q` | 退出 |

软件包中特别丰富的文本包括 `gimp`, `festival`, `libc`, `automake`, `zsh`, `sed`, `tar` 和 `bash`，存储在 `/usr/share`。

## 总结

尽管你可以从头到尾阅读这本书，但这旨在作为 BSD 系统中对高级用户最有用的数百个功能的参考。

事实上，下一章将介绍如何获取和安装软件。

## 2

# 安装 FreeBSD 和添加软件

### 本章内容

* 安装 `FreeBSD`
* 获取软件包
* 使用 `ports` 获取和安装软件

## 安装 FreeBSD 之前



你可以从 `www.freebsd.org/where.html` 的 Getting FreeBSD 页面获取 FreeBSD 安装软件。从该页面找到购买 FreeBSD CD 或 DVD 的地方。例如，你可以从 FreeBSD Mall (`freebsdmall.com`) 购买四 CD 套或单 DVD，带或不带 FreeBSD 手册。

# 第 2 章：安装 FreeBSD 和 Android 软件

你可以从“获取 FreeBSD”页面了解从支持的 FreeBSD 架构下载 FreeBSD ISO。支持的架构包括：`Intel i386`、`Alpha/AXP`、`AMD 64 位`（`Athlon64`、`Athlon64-FX` 或 `Opteron`）、`i64`、`PowerPC` 和 `Sparc6`。例如，可以从 `ftp.freebsd.org/pub/FreeBSD/ISO-IMAGES-i386` 获取多个 FreeBSD 版本的下载内容。

通过 `http://FreeBSD.org/docs.html` 页面，你可以访问 FreeBSD 文档，如果在安装过程中遇到困难，这些文档可以为你提供帮助。例如，关于安装提示、支持的硬件、启动加载程序以及你入门所需的其他主题的 FAQ。

为了安装 FreeBSD 而擦除计算机硬盘上的所有内容，你不需要提前准备硬盘。如果你想保留硬盘上的任何数据，请在继续操作之前进行备份。如果你想保留硬盘上的现有数据并添加 FreeBSD，你可能需要调整现有分区的大小并重新划分磁盘。有关磁盘调整大小和分区命令的信息，请参阅第 7 章。

> 注意：如果你从同一台计算机启动多个操作系统，那么这些系统的安装顺序至关重要。如果你想在机器上使用 Windows，请先安装它，否则它将覆盖你的启动管理器并导致 FreeBSD 暂时无法启动。Linux 系统安装程序通常会询问你是否安装启动加载程序，并可能让你配置该启动加载程序以启动 FreeBSD。如果启动管理器被擦除，请擦除 FreeBSD 文件系统，并从 CD 的工具目录运行 `bootinst.exe boot.bin` 来重新安装 FreeBSD 启动管理器。

## 安装 FreeBSD

本节描述的 FreeBSD 安装过程使用三光盘 FreeBSD 安装集。本文描述的计算机具有 `x86` 架构，并且可以连接到网络（用于添加 CD 上没有的软件）。此过程已在 FreeBSD 7 和 6.3 上通过了测试。

## 启动安装盘

将第一张 CD 插入驱动器并重启。当 FreeBSD 启动屏幕出现时，按照以下步骤在你的计算机上安装 FreeBSD：

欢迎使用 FreeBSD！

```
+ 1. 启动 FreeBSD [默认]

2. 禁用 ACPI 启动 FreeBSD

3. 在安全模式下启动 FreeBSD

4. 在单用户模式下启动 FreeBSD

5. 以详细日志模式启动 FreeBSD

6. 退出到加载器提示符

7. 重启

选择选项，按 [Enter] 默认
或按 [Space] 暂停计时
```

# 第 2 章：安装 FreeBSD 并添加软件

按下空格键（暂停计时）或让默认安装开始（按 Enter 或等待超时）。如果你想查看或更改启动设置，请按 `6`。当你看到 `OK` 提示符时，输入 `?` 查看可用命令。*这里是一些你可以从启动提示符运行的命令：*

- `boot`: 启动安装过程

- `show`: 列出启动变量

- `set xx=?`: 设置启动变量（例如，使用 `set acpi_load=NO` 在安装期间关闭 ACPI）

- `unset xx`: 取消选定的启动变量设置

- `lsdev`: 列出潜在的启动设备名称

- `lsmod`: 列出已加载的模块

- `ls`: 列出文件

- `load`: 加载选定的内核或模块

- `smap`: 翻页文件（例如，`more README.txt`）

要启用内核中的功能，请将它们添加到 `kernel_options=` 变量中。当你准备好继续安装过程时，输入 `boot`。

## 开始安装过程

FreeBSD 提供了基于文本/菜单的安装过程。在整个安装过程中，使用这些按键：`Space`（切换项目）或 `Enter`（完成项目）。此外，使用向上箭头（上一个项目）、向下箭头（下一个项目）、向右箭头（下一个项目或组）或向左箭头（上一个项目或组）。要滚动，选择 `Page Up`（向上一页）、`Page Down`（滚动文本框一页）和 `FI`（显示帮助文本）。

1. 选择国家。默认国家是美国。出现 `sysinstall` 主菜单，显示安装类型和其他选项列表。

2. 选择安装类型。要进行安装，请选择 `Standard`（推荐）、`Express`（专家的快速安装）或 `Custom`（专家的自定义安装）。本过程描述的是 `Standard` 安装。如果显示你一个用于分区你的硬盘（s）的屏幕，请继续下一步。

3. 磁盘分区。安装程序为你提供了一个面向界面的 `FDISK` 来对你的硬盘进行分区。（有关使用 `FDISK` 分区的详情，请参阅第 7 章。）以下是你的选项：

`A` = 整个磁盘
`G` = 设置几何结构
`C` = 创建切片
`F` = `'DD'` 模式
`D` = 删除切片
`Z` = 切换大小单位
`S` = 设置启动
`|` = 向导
`T` = 更改类型
`U` = 撤销所有更改
`Q` = 完成

假设你想在整个磁盘上安装 FreeBSD，使用方向键高亮任何旧切片并输入 `D` 将其删除。然后你可以选择以下磁盘分区方法之一：

- `A`: 使用整个硬盘用于 FreeBSD，这会在切片开头留出空间，以便你将来可以添加启动管理器。如果你想从本地计算机上安装并启动多个操作系统，添加启动管理器（如 `LILO` 或 `GRUB`）将让你能够实现。此项用于多系统启动和家庭 PC。

- `F`: 要将计算机完全留给 FreeBSD，选择 `F` 并在被问是否希望保持硬盘与其他操作系统兼容时选择 `No`。这种方法分配了用于 FreeBSD 的 `400MB` 空间。此项用于多系统启动和家庭 PC。

# 第 2 章：安装 FreeBSD 和添加软件

将系统启用为 NFS 服务器允许你共享本地目录，网络上的其他计算机可以挂载它们。

NFS 客户端？**是**

将系统启用为 NFS 客户端允许你挂载网络上其他计算机共享目录。

自定义系统控制台设置？**否**

你可以更改系统控制台设置，例如字体、键位和终端类型。

设置时区？**是**

为机器设置 Linux 二进制兼容性。

Linux 二进制兼容？**是**

通过安装 Linux 应用程序所需的组件，允许你在 FreeBSD 上运行 Linux 软件。

PS/2、串口或总线鼠标？**否**

如果你的电脑有鼠标且你想启用它，请选择是。然后你可以选择测试并运行鼠标守护进程，以确保其正常工作。

现在浏览软件集合？**是**

使用方向键高亮你想要安装的包并按回车。当你看到与每个包相关的包列表时，高亮每个想要的项目（使用方向键）并按空格键标记每个应用程序进行安装。检查你选择的应用程序并选择确定。

添加初始用户账户？**是**

为系统的每个用户添加一个普通用户账户。你也可以向系统添加组。

root 用户密码

为 root 用户分配密码。

访问配置菜单以进行最后的选项？**否**

这将带你进入 FreeBSD 配置菜单，在安装期间你可以在那里更改设置（包、分区、时区、鼠标等）。

返回 sysinstall 界面（完成后退出）**否**

如果你想返回 `sysinstall` 主菜单，此时可以进行操作。你也可以在重启系统后的任何时间运行 `sysinstall` 命令，以对你的配置进行进一步更改。

重启？是

移除安装介质并重启系统，以从硬盘运行新安装的系统。

当系统重启时，你可以使用在安装期间设置的用户名和密码登录。

## 添加、删除和管理软件

安装 FreeBSD 之后，你可以使用 Ports（程序集）或 Packages（包）安装额外的软件。FreeBSD ports 集合方法允许你从源代码安装软件。Packages 方法允许你安装预先构建为二进制文件的应用程序。专家经常使用 ports 系统来获取最新软件。新用户可能更倾向于使用 Packages，只要构建过程中的错误已经得到解决。

对于安装二进制文件，`sysinstall` 工具让你选择从何处（CD、DVD、FTP 等），然后选择要安装哪些包。如果某个包已经在你的电脑上，你可以使用 `pkg_add`、`pkg_delete` 和 `pkg_info` 等命令来处理该包。使用 ports 系统构建包，你需要使用 `make` 命令。

## 查找软件

你随时可以使用 FreeBSD Ports 搜索页面（`www.freebsd.org/ports`）查找哪些软件在 FreeBSD 中是可用的。如果你知道某个组件（命令、系统调用、文件格式等），但不知道它属于哪个包，可以从 FreeBSD 网站（`www.freebsd.org/cgi/man.cgi`）的页面进行搜索。你也可以使用 `pkg_info` 获取已安装软件的信息。

若要在 FreeBSD Ports 系统中搜索特定的软件包，请访问搜索页面 `www.freebsd.org/ports`。输入要搜索的术语、描述区域搜索词以及特定的软件类别。你将看到按类别和包名列出的结果。

```
Search for: md5sum All All Sections Submit
Category security cfv-1.18.1
Utility to test and create .sfv, csv and md5sum files
 description : Sources : Changes : Download
Maintained by: ports@FreeBSD.org
Requires: py25-fchksum-1.7,1, python25-2.5.1_1
```

在安装之前阅读有关可用命令、文件格式和其他内容的，请使用 FreeBSD 超文本手册页（`www.freebsd.org/cgi/man.cgi`）。通过手册名称或关键词搜索。此示例搜索了 `pkg_info` 手册页：

- Man Page or Keyword Search: `pkg_info` | Submit | Reset |
- Man | All Sections | FreeBSD Ports |
- Apropos Keyword Search (all sections) | html | Output format
- home | help

`PKG_INFO(1)` FreeBSD General Commands Manual `PKG_INFO(1)`

NAME

`pkg_info` - 用于显示软件信息的实用

你可以使用 `pkg_info` 命令检查某个包是否已经安装，并列出已安装包的信息。（取决于你使用的 shell 类型，你可能需要用引号将通配符括起来，例如 `pkg_info "cdtools*"`）。以下是示例：

- `# pkg_info | less` 显示所有包的名称/索引行
- `# pkg_info -i gnome* | less` 显示匹配包的名称/索引行
- `# pkg_info cdtools* | less` 显示已安装包 `cdtools` 的信息
- `# pkg_info -d cdtools* | less` 显示包的详细描述
- `# pkg_info -c cdtools* | less` 显示包的注释行
- `# pkg_info -f cdtools* | less` 显示包中的文件列表
- `# pkg_info -L cdtools* | less` 显示包中文件的完整路径
- `# pkg_info -l gnome-game* | less` 显示包的安装脚本（如果有的话）
- `# pkg_info -k kdebase* | less` 显示包的卸载脚本

你可以使用 `pkg_info` 命令查找依赖关系。以下是示例：

- `# pkg_info -R cdtools* | less` 显示已安装包所需的包
- `# pkg_info -r cdtools* | less` 显示依赖于 `cdtools` 的包

如果你想搜索包或文件的特征，可以使用 `locate` 命令搜索整个系统。前提是你已经配置了 `locate` 数据库包含整个系统的内容。第 4 章包含了如何创建 `locate` 数据库的信息。

在安装之前，浏览可用组和包最直观的方法是查看下一节提到的 `sysinstall` 页面。

## 安装软件包（二进制）

你可以使用菜单界面（`sysinstall`）或命令行界面（`pkg_add`）安装预编译的二进制包。`sysinstall` 和 `pkg_add` 都会尝试获取并安装你请求的包以及你选择的依赖包。

安装 FreeBSD 之后，你可以运行 `sysinstall` 工具来添加更多软件包。作为 `root` 用户，输入 `/usr/sbin/sysinstall` 显示 `sysinstall` 主菜单。然后选择配置，并选择你想从中安装的菜单（CD/DVD、FTP、HTTP 等）。你还需要选择位置和网络接口以访问选择的软件。图 2-1 显示了 `sysinstall` 工具包选择界面的示例。

![](img/a8f0676d6e7f319a693ce1963202001e_48_0.png)

图 2-1：使用 `sysinstall` 工具安装软件包。

如果你喜欢命令行而不是菜单界面，可以使用 `pkg_add` 命令将包添加到你的 BSD 系统中。你请求的包可以在本地目录中或 BSD 仓库中。以下是示例：

```
# pkg_add bsdtris-1.1.7.tbz
```
从本地目录安装 `bsdtris`

# 第 2 章：安装 FreeBSD 和添加软件

```
# pkg_add -r freebsd-games    从网络下载/安装 freebsd-games
# pkg_add -r -K xmines           下载/安装 xmines，将包保存到本地目录
# pkg_add -r lsof-4.79D.tz       以详细模式安装 lsof
请求空间: 452500 字节，空闲空间: 1155632500 字节
位于 /var/tmp/instmp.0JSi
extract: 包名为 lsof-4.79D
extract: 当前目录切换到 /usr/local
extract: /usr/local/sbin/lsof
...
```

在安装包之前验证其内容，你可以使用 `pkg_add` 的 `-M` (Master) 选项。使用 `-M` 后，程序不会安装包，而是将包的内容复制到 `/var/tmp` 的子目录中，你可以在那里对其进行检查。例如，使用本地目录中的 `memdump-1.01.tbz`，输入以下命令：

```
# pkg_add -M memdump-1.01.tbz 将内容放入 /var/tmp 以检查
```

包进入 `/var/tmp` 目录后，你现在可以检查包的内容了。寻找名为 `instmp.??????` 的目录，其中每个 `?` 被字母或数字替换。`-M` 选项可以与 `-S` (Slave) 模式配合使用。

## 删除软件包（二进制）

要删除以前安装的软件包，你可以使用 `pkg_delete` 命令。以下是使用 `pkg_delete` 删除包的一些示例：

```
# pkg_delete -n 'dbus-0.93_3'  在删除包前检查会发生什么
pkg_delete: 包 'dbus-0.93_3' 被这些其他包依赖
并且可能无法卸载
dbus-glib-0.71
avahi-0.6.14
policykit-0.1.200605014_2
hal-0.5.8.20060917_2
```

```
pkg_delete: 1 个包删除失败
```

`pkg_delete` 的 `-n` 选项显示了实际运行 `pkg_delete` 时会发生什么，而不会真的执行它。在实际删除包之前运行 `pkg_delete -n` 是一个好主意。这会告诉你该包的依赖关系（如果有的话），但不会实际删除该包。如果没有依赖关系，它将显示将要删除的确切文件，以便你可以查看是否漏掉了任何内容。

使用 `pkg_delete` 删除包时还有其他实用的选项：

- `# pkg_delete xmines*` 使用通配符删除包
- `# pkg_delete -i akode*` 删除一组包，并确认每个包的删除
  `akode-2.0.1,1? y`
- `# pkg_delete -v xmines*` 详细输出并删除
  `pkg_delete: 未安装包 'xmines*'`
  `pkg_delete: 1 个包删除失败`

在配合 `pkg_delete` 使用以下任何选项之前，请先进行思考。第一个示例会强制删除指定的包，即使该包有有其他包依赖于它。在第二个示例中，所有已安装的包都会被删除，我推测这会将系统还原为仅留基础系统（我不会亲自尝试，但提到它是因为有该选项）：

- `# pkg_delete -f metacity*` 强制移除包（不进行依赖检查）
- `# pkg_delete -a` 危险！危险！这将移除所有已安装的包

另一个有点危险但可能实用的选项是 `-r` 选项。如果你想删除一个包以及所有依赖于它的包，可以使用此选项。在使用此选项之前，进行一些非破坏性的尝试是明智的。例如：

- `# pkg_delete -n gstreamer*` 非破坏性测试
- `# pkg_delete -r gstreamer*` 危险！递归删除包

## 使用 Ports 安装软件（源码）

Ports 集合包含了用于编译和安装 FreeBSD 所需的文件、补丁和信息。通常情况下，从源码构建包更受专家用户青睐，因为源码本身位于压缩包中。在构建过程中，你会从站点获取源码。当你安装 Ports 集合时，它位于 `/usr/ports`。

在 FreeBSD 上获取 Ports 集合有几种方法。包括 `sysinstallall`、`portsnap`。在这三种方法中，`sysinstallall` 方法是最直观的，但 `portsnap` 非常简单。使用 `portsnap` 获取 ports：



### 1. 创建 ports 目录（如果不存在）

```
# mkdir /usr/ports
```

### 2. 如果尚未安装，安装 portsnap

```
# pkg_add -r portsnap
```

### 3. 下载 ports 集合

```
# portsnap fetch
```

### 4. 更新现有的 ports 集合

```
# portsnap update
```

无论你使用哪种方法获取 `ports`，后续章节都提供了说明。

# 第 2 章：安装 FreeBSD 和添加软件

## 通过 Ports 获取并应用程序

`ports` 集合中的应用程序可以通过端口 skeleton 获取。端口 skeleton 是 `/usr/ports` 下的一个目录，包含了编译和安装所需的组件。基本上，源码包含在 tar 包中。在构建过程中，你会获取 `distfile`。

以下是使用 skeleton 使用 `ftcopy` 应用程序：

```
# cd /usr/ports/ftp/ftcopy    切换到 ftcopy 目录
# ls -CF                               列出 ftcopy 内容
Makefile             distinfo      files/ pkg-desc  pkg-list
```

`Makefile` 由 `make` 命令用于描述如何编译应用程序。`distinfo` 文件包含了检查下载文件的 `md5` 和 `sha256` 校验和。`files` 目录包含了应用程序的任何补丁，用于在 FreeBSD 上运行或修复安全问题。

`pkg-desc` 文件包含了包描述以及创建该项目的网站。`pkg-list` 文件标识了从应用程序的文件以及它们在文件系统中的位置。除了可执行命令（例如 `ftp`、`ftpcopy`），文件可能包含库、图像或文档（如 `ChangeLog`、`README` 或其他文档）。

## 快速构建

对于最基本的应用程序安装，你只需要运行几个命令。以 `ftcopy` 应用程序为例，这里是如何使用 `ports` 集合安装应用程序：

```
# cd /usr/ports/ftp/ftcopy    切换到 ftcopy 目录
# make build                               下载并构建 ftcopy 应用程序
=> ftcopy-0.6.7.tar.gz 似乎不存在 /usr/ports/distfiles/
=> 尝试从 http://www.ohse.de/uwe/ftcopy/ 获取
=> 正在提取 ftcopy-0.6.7
=> MD5 校验通过 ftcopy-0.6.7.tar.gz
=> SHA256 校验通过 ftcopy-0.6.7.tar.gz
=> ftcopy-0.6.7 依赖文件: /usr/local/bin/perl5.8.8 - 
=> 正在打补丁 ftcopy-0.6.7
=> ftcopy-0.6.7 依赖文件: /usr/local/bin/perl5.8.8 - 
```

```
==> 正在为 ftpcpcopy 应用 FreeBSD 补丁
==> ftpcpcopy-0.6.7 依赖于:/usr/local/bin/perl5.8.8 已找到
==> 正在配置 ftpcpcopy-0.6.7
==> 正在编译 ftpcpcopy-0.6.7

# make install               安装 Ftpcpcopy 二进制文件和文档
==> 正在安装 ftpcpcopy-0.6.7
==> 正在生成临时打包列表
==> 检查 ftpcpcopy 是否已安装
cd /usr/share/ports/ftp/ftpcpcopy/web/ftpcpcopy-0.6.7&compile && install -s -o root
-g wheel -m 555 ftpcpcopy ftpls /usr/local/bin/ && install -o root -g wheel -m
444 ftpcp1.1 ftcp1.1 ftpls /usr/local/man/man && install -o root -g wheel
-m 555 ftpcp- /usr/local/man/man && cd
/bin/mdir -p /usr/local/share/doc/ftpcpcopy
/usr/share/ports/ftp/ftpcpcopy/ftpcpcopy-0.6.7&compile && install -o root
- wheel -m 444 ChangeLog README ftpcpcopy.html
/usr/local/share/doc/ftpcpcopy
==> 正在为 ftpcpcopy-0.6.7 压缩手册页
==> 正在注册 ftpcpcopy-0.6.7 的安装
# make clean               清理构建留下的文件
==> 正在清理 perl5.8.8
==> 正在清理 ftpcpcopy-0.6.7
```

```
# pkg_info ftpcpcopy* 检查 ftpcpcopy 包是否已安装
ftpcpcopy-0.6.7 用于列出和镜像的命令行 ftp 工具
```

```
# pkg_info -L ftpcpcopy 列出 ftpcpcopy 包中的文件
```

`ftpcpcopy-0.6.7` 的信息：

文件：

`/usr/local/man/man1/ftpcpcopy.1.gz`

`/usr/local/man/man1/ftpcp1.1.gz`

`/usr/local/bin/man1/ftpls.1.gz`

`/usr/local/bin/ftpcpcp`

`/usr/local/bin/ftpcpcopy`

`/usr/local/bin/ftpls`

`/usr/local/share/doc/ftpcpcopy/ChangeLog`

`/usr/local/share/doc/ftpcpcopy/NEWS`

...

在更改代表你想要安装的应用程序的目录后，运行三个 `make` 命令。`make` 命令下载软件包（源码目录），运行检查以验证其有效性，应用补丁，满足依赖关系并留下二进制文件（命令）。

`make install` 命令将应用程序放入对应位置，压缩手册页并注册安装。

`make clean` 命令清理构建留下的文件。

# 第 2 章：安装 FreeBSD 和添加软件

## 清理 Ports 集合 (Ports Collection)

每次从 `ports` 系统安装包后，通常最好的方法是运行 `make` 命令来删除构建过程中产生的临时文件。如果你忘记这样做，许多未使用的文件会占用你的磁盘空间。你可以使用 `portsclean` 命令一次清理 `ports` 集合中的组未使用文件（`portsclean` 包含在 `portupgrade` 软件包中：`pkg_add -r portupgrade`）。

尽管在运行 `make` 命令时工作文件会被清理，但下载到 `/usr/ports/distfiles` 的 `distfiles`（今天的源码）不会被清理。取决于你安装的 `ports` 数量，此目录可能会变得很大。你可以使用 `portsclean` 的 `-D` 选项删除未被任何端口号引用的 `ports`：

```
# portsclean -D    移除未引用的 distfiles
Detecting unreferenced distfiles...
```

同样，你可以让 `portsclean` 检查所有 `distfiles`，并删除任何未被已安装端口 所引用的 `distfiles`：

```
# portsclean -DD    移除未安装端口的未引用的 distfiles
Detecting unreferenced distfiles...
[Updating the pkgdb <format=bdb_btree> in /var/db/pkg ...
- 440 packages found (0 + 2) .. done]
Delete /usr/ports/distfiles/LPrng-3.8.28.tgz
```

你可以使用 `-C` 选项一次清理所有的工作文件：

```
# portsclean -C    移除 ports 工作文件
Cleaning out /usr/ports/*/*work...
Delete /usr/ports/ftp/ftpcopy/work
Delete /usr/ports/net/samba-nmblookup/work
```

未被任何其他包引用的包（称为叶包）可以使用 `pkg_cutleaves` 命令进行交互式删除（以 `root` 身份输入此命令：`pkg_add -r pkg_cutleaves`）。列出未引用的包，输入以下命令：

```
# pkg_cutleaves -lc    列出未引用的包
3dm-2.04.00.018.1 - 3ware RAID 控制监控守护进程和 Web 服务器
...
```

你可以按照如下方式删除未引用的包：

```
# pkg_cutleaves    逐个处理未引用包列表（保留或删除）
package 1 of 147
3dm-2.04.00.018.1 - 3ware RAID 控制监控守护进程和 Web 服务器
3dm-2.04.00.018.1 - [keep](d)elete/(f)lush marked pkgs/(a)bort d
3dm-2.04.00.018.1 - 3ware RAID 控制监控守护进程和 Web 服务器
```

`package 2 of 147:`

`44bsd-more-20000521 - 在 less(1) 之前随 FreeBSD 安装的分页器`

`44bsd-more-20000521 - [keep](d)elelete/(f)lush marked pkgs/(a)bort? f`

`Deleting 3dm-2.04.00.018,1 (package 1 of 1)。`

`继续处理新的叶包 ((yy)/es/[no]) no`

`** Deinstalled packages:`

`3dm-2.04.00.018,1`

`** Number of deinstalled packages: 1`

当显示每个未引用的包时，你可以将其标记为保留（按回车）或删除（`d`）。在你标记了一些包后，可以通过输入 `f` 来刷新它们。你可以随时输入 `a` 取消退出。

## 总结

尽管没有图形化安装程序，FreeBSD 也提供了一些复杂的工具用于安装和处理软件包。初始安装使用 `sysinstall` 实用程序完成。系统安装后，你可以选择从二进制包或源代码安装额外的软件包。

对于二进制包，你可以使用 `pkg_add`、`pkg_delete` 和 `pkg_info`。对于从源码构建包，你可以使用 `make` 命令并带有多种选项。

有许多工具可以管理你计算机的 `ports` 集合。你可以使用 `portupgrade` 更新集合中的部分或全部 `ports`。如果你对计算机有安全顾虑，`portaudit` 命令可以下载所有已安装的包并报告软件中包含的潜在安全漏洞。

由于从 `ports` 安装大量应用程序时，临时目录中的文件会随时间堆积，你可以使用 `portcollection` 和 `pkg_cutleaves` 等命令来清理不需要的文件。通过 `portcollection`，你可以清理残留文件的工作目录。通过 `pkg_cutleaves`，你可以移除未被任何其他包引用的包。

# 第 3 章：使用 Shell

## 命令解释器概述

命令解释器（通常称为 `shell`）的使用可以追溯到第一个 UNIX 系统的早期。除了运行命令的明显用途外，`shell` 还有许多内置功能，如环境变量、别名和各种编程函数。

BSD 系统上有几款 `shell` 可供选择。默认情况下，`root` 用户被分配使用 C `shell` (`csh`)，普通用户被分配使用 Bourne `shell` (`sh`)。大多数用户使用 Bourne Again `Shell` (`bash`)。还有其他可用的 `shell`（如 `zsh`、`ksh` 和 `tcsh`）。

本章提供了帮助你使用通用 BSD `shell` 尤其是 `bash` `shell` 的信息。

## 本章内容

- 访问 `shell`
- 使用 `shell`
- 获取超级用户权限
- 使用环境变量
- 创建简单的 `shell` 脚本

## 终端窗口 (Terminal Windows)

从 BSD 界面访问 `shell` 的常用方法是使用终端窗口。在图形界面中，通常可以访问虚拟终端来进入 `shell`。在没有图形界面的基于文本的登录后，通常进入 `shell`。

## 使用终端窗口

从 GNOME 打开终端窗口，选择“终端 (Terminal)”。这将打开 `gnome-terminal` 并显示 `bash` 提示符。从 XFce 桌面，从面板选择终端。从 KDE 选择终端启动 `konsole` 窗口。图 3-1 显示了 `gnome-terminal` 的示例。

```
bash-2.0$ echo SHELL /usr/local/bin/bash

bash-2.0$ whoami chris

bash-2.0$ pwd /home/
```

图 3-1 显示当前 `shell` 是 `bash` (`/usr/local/bin/bash`)，当前用户是 `chris`，当前目录是 (`/home/chris`)。用户名 (`chris`) 和主机名 (`localhost`) 显示在标题栏中。`gnome-terminal` 不仅让你访问 `shell`，还有管理窗口的控制功能。例如，点击 `Ctrl+Shift+` 在另一个标签页上打开 `shell`，点击 `Ctrl+Shift+` 打开新窗口，或选择 `Title` 设置新名称。你还可以使用按键序列来操作终端窗口。控制终端窗口的其他按键序列包括 `F1` 进入全屏模式。输入 `Ctrl++` 放大（增大字体）或 `Ctrl+-` 缩小（减小字体）。使用 `Ctrl+PageUp` 和 `PageDown` 切换标签（上一个和下一个），或使用 `Alt+1`、`Alt+2`、`Alt+3` 进入二、三（以此此类推）。输入 `Ctrl+D` 退出 `shell`，关闭当前标签或终端（如果是最后一个标签）。

`gnome-terminal` 还支持配置 (Edit Current Profile)。某些配置是装饰性的（允许粗文本、光标闪烁、终端铃、颜色、透明度）。其他设置是功能性的。例如，默认情况下终端保存 500 行历史（318 kilobytes）。有些人希望能够回溯更多并愿意提供更多内存。

如果你手动启动 `gnome-terminal`，可以添加选项。这里是一些示例：

```
# gnome-terminal -x alisamixer      启动显示 alisamixer 的终端

# gnome-terminal --tab --tab --tab      启动三个标签的终端

# gnome-terminal --geometry 80x20      启动 80 列 20 行的终端

# gnome-terminal --zoom=2               启动大字体的终端
```

除了 `gnome` 之外，你还可以使用许多其他终端。这里是一些示例：`xterm`（随 X 安装的基础模拟器）、`aterm`（系统 VT12 模拟器）和 `console`（随 KDE 桌面提供的模拟器）。`Enlightenment` 项目提供了 `ether` 终端（包含屏幕消息日志等功能）。每个终端窗口命令只需安装同名的软件包即可，`console` 除外，它在 `kdebase` 软件包中。

## 使用终端 (Terminals)

当 FreeBSD 以多用户模式启动时，会创建基于文本登录的八个虚拟控制（由控制窗口和虚拟终端 `tty0` 到 `tty7` 表示）。如果正在运行 X 系统，X 可能在虚拟控制 8 中运行。虚拟控制 1 是显示消息的地方。如果 X 未运行，你看到的是虚拟控制 2。

从 X，你可以通过 `Ctrl+Alt+F1`、`Ctrl+Alt+F2` 直 `F8` 切换到另一个控制。对于虚拟控制，你可以使用 `Alt+F1`、`Alt+F2` 等。按 `Alt+F9` 返回 X GUI。每个控制允许使用不同的用户账户登录。切换查看另一个控制不会影响其中任何一个正在运行的进程。当你切换到六之前的虚拟终端，你会看到类似下面的登录提示符：

`FreeBSD/i386 (localhost) (tty1)`
`login:`

独立的 `getty` 进程管理每个虚拟终端。如果你在终端窗口中，在登录任何虚拟终端之前查看 `getty` 进程的样子：

```
# ps | grep -v grep | grep getty

780 v1  Is+    0:00:01 /usr/lib/execec/getty tty1

782 v2  Is+    0:00:01 /usr/lib/execec/getty tty2

782 v3  Is+    0:00:01 /usr/lib/execec/getty tty3

783 v4  Is+    0:00:01 /usr/lib/execec/getty tty4

784 v5  Is+    0:00:01 /usr/lib/execec/getty tty5

785 v6  Is+    0:00:01 /usr/lib/execec/getty tty6

786 v7  Is+    0:00:01 /usr/lib/execec/getty tty7
```

在第一个控制台上登录后，`getty` 会处理你的登录，然后启动一个 `shell`：

```
# ps awx | grep -v grep | grep v0

780 v0      Is      0:00.04 login (pam)

2300 v0     S       0:00.02 -sh (sh)
```

虚拟控制台在 `/etc/ttys` 文件中配置。你可以通过在该文件中添加或删除行，来增加或减少虚拟终端的数量。（请查找 `Virtual` 章节）。输入以下命令查看配置了哪些 `ttys`：

```
# grep tty /etc/ttys
```



`tty0` `"/usr/libexec/getty Pc*"` `cons25 on secure`

## 使用 Shell

当你打开一个 shell 后（无论通过基于文本的登录还是 `Terminal` 窗口），shell 环境都将根据启动 shell 的用户进行设置。每个用户的默认 shell 由 `/etc/passwd` 文件中的用户条目分配。默认情况下，用户的密码被设置为 `csh` (`/bin/csh`)，普通用户设置为 `sh` (`/bin/sh`)。要使用 `bash` shell，你可以将 shell 设置为 `/usr/local/bin/bash`。本节中的示例都将使用 `bash` shell。

所有用户 shell 的 `bash` 设置位于 `/etc/profile` 中。特定用户的设置由从用户家目录下的几个点文件（如果存在）中执行的命令决定：`.bash_profile`、`.bash_login` 和 `.profile`。当 shell 关闭时，`~/.bash_logout` 文件中的任何命令都会永久更改用户的 shell 设置，但不会影响已经在运行的 shell。（其他 shell 使用不同的配置文件。）

有多种方法可以列出并更改你的 shell 环境。其中最重要的方法之一是更改你的用户身份；特别是成为超级用户（参见本章稍后介绍“获取超级用户权限”章节）。

## 使用 Bash 历史记录

`Bourne Again Shell (bash)` 被许多 UNIX 类系统使用。与所有其他 shell 一样，`bash` 内置了一项历史记录功能，它允许你查看、修改和重用过去运行过的命令。

当 `bash` 启动时，它会读取 `~/.bash_history` 文件并将其加载到内存中。该文件由 `$HISTFILE` 的值设置。在 `bash` 会话期间，命令会被添加到内存中。当 `bash` 退出时，内存中的历史记录会被写回 `.bash_history` 文件。`bash` 会话期间保留的命令数量由 `$HISTSIZE` 设置，而实际存储在历史文件中的命令数量由 `$HISTFILES` 设置：

```bash
$ echo $HISTFILE $HISTSIZE $HISTFILES

/home/fcaen/.bash_history 500 500
```

要列出所有历史记录，输入 `history`。要列出指定数量的历史命令，在 `history` 后紧跟一个数字。这将列出你历史记录中之前的五个命令：

```bash
$ history 5

mkdir extras

mv *doc extras/

ls -CF

vi house.txt

history
```

要移动历史记录中的命令，请使用向上箭头和向下箭头。当显示命令时，你可以像处理任何其他命令一样使用键盘编辑当前命令：左箭头、右箭头、`Delete`、`Backspace` 键等。以下是从 `bash` 历史记录中召回并运行命令的其他其他方法：

```bash
$ !! 执行上一个命令

$ 1997 执行历史记录中的第 997 号命令

ls -CF

$ 1997 *doc 在历史记录的第 997 号命令后附加 *doc

ls -CF *doc

$ !CF7? 执行包含 CF 字符串的上一行命令

ls -CF *doc

$ !!ls 执行上一个 ls 命令

ls -CF *doc

$ !!ls:CF/1 执行上一个 ls 命令，将 CF 替换为 l

ls -1 -doc
```

编辑命令的另一种方法是使用编辑器。通过 `fc`，你可以使用 `vi` 编辑器打开历史记录中指定的命令。编辑后的命令会在退出编辑器时运行。可以通过设置 `FCEDIT` 变量（例如 `FCEDIT=gedit`）或在 `fc` 命令行切换到不同的编辑器。例如：

```bash
$ fc 978 编辑第 978 号命令，然后运行它

$ fc 编辑上一个命令，然后运行它

$ fc -e /usr/local/bin/nano 989 使用 nano 编辑第 989 号命令
```

（如果尚未安装编辑器，请使用 `pkg_add -r` 安装你需要的编辑器。第 5 章描述了多种文本编辑器及其所属的软件包。）

使用 `Ctrl+r` 在历史记录中搜索字符串。例如，输入 `Ctrl+r` 后跟 `ss` 会导致以下结果：

```text
# <Ctrl+r>

(reverse-i-search)`: sudo /usr/bin/less /var/log/messages
```

重复按下 `Ctrl+r` 在你的历史列表中反向搜索 `ss` 字符串的其他出现处。

> 注意：默认情况下，`bash` 命令编辑使用 `emacs` 风格的命令。如果你更喜欢 `vi` 编辑器，可以使用 `set` 命令将编辑器设置为 `vi`，从而使用 `vi` 风格的历史记录。输入如下：`set -o vi`。

## 命令行补全

你可以使用 `Tab` 键完成命令行上不同类型的信息。以下是一些示例，你输入部分名称后按 `Tab` 键，让 `bash` 完成输入：

```bash
$ /usr/bin/le<Tab>

/usr/bin/less

/usr/bin/lessx
```

```bash
$ /usr/bin/ls<Tab>

/usr/bin/ls
```

```bash
$ /etc/pass<Tab>

/etc/passwd

/etc/passwd.d
```

## 重定向标准输入和输出

默认情况下，所有输出都指向屏幕。大于号 (`>`) 将输出重定向到文件。更具体地说，你可以重定向 `stderr`。以下是一些示例：

```bash
$ ls /tmp > output.txt
```

```bash
$ ls /tmp > output.txt 2>&1
```

在第一个示例中，`stdout` 被重定向到 `output.txt`，而 `stderr` 仍然指向屏幕。在第二个示例中，`stderr`（流 `2`）被重定向到 `output.txt`。在最后一个示例中，两者合并。要追加到文件而不是覆盖，使用两个大于号：

```bash
$ ls /tmp >> output.txt
```

如果你不想看到输出，可以将输出重定向到特殊位文件 (`/dev/null`)：

```bash
# ls /tmp > /dev/null
```

> 提示：运行 `cron` 任务时，你可能还需要重定向 `stderr`。你可以将 `stderr` 重定向到发送给 `cron` 所有者的邮件。

就像你可以从命令重定向标准输出一样，你也可以向命令重定向标准输入。例如，以下命令将 `/etc/hosts` 文件发送给本地系统中名为 `chris` 的用户：

```bash
$ mail chris < /etc/hosts
```

使用管道，你可以将输出从一个进程重定向到另一个进程，而不仅仅是文件。这里有一个将 `ls` 命令管道到 `sort` 命令以排序输出的示例：

```bash
# ls /tmp | sort
```

在下一个示例中，管道和重定向结合在一起（`ls` 命令的 `stdout` 被重定向，而 `stderr` 被丢弃到管道中）：

```bash
$ ls /tmp/ 2> /dev/null | sort
```

管道可以用于许多事情：

```bash
# pkg_info | grep -i gnome | wc -l

# ps aux | grep firefox

# ps aux | less

# whereis -m pkg_add | awk '{print $2}'
```

`Firefox` 进程（假设 `Firefox` 浏览器正在运行）。第三条命令行允许你分页查看进程列表。最后一行显示 `pkg_add:` 单词，后面紧跟着 `pkg_add` 帮助页的路径，然后只显示帮助页的路径（该行的第二个元素）。

使用反引号（backticks），你可以先执行命令的一个部分，并将该命令的输出传递给命令的其余部分。以下是示例：

```bash
# pkg_info -W 'which mkisof'

/usr/local/bin/mkisof was installed by package cdtools-2.01_6

# ls -l 'which traceroute'

-sr-xr-x 1 root wheel 19836 Jan 15 18:33 /usr/bin/traceroute
```

示例中的第一条命令行找到了 `mkisof` 命令的完整路径并找到了包含它的包。第二条命令行找到了 `traceroute` 的完整路径，并对该命令执行了详细列表（`ls -l`）。

获取一个命令的输出并作为参数传递给另一个命令更高级且强大的方法是使用 `xargs` 命令。例如，在安装 `cdtools` 包后，我运行了以下命令：

```bash
# find /usr/local/bin | grep iso | xargs ls

/usr/local/bin/growisof /usr/local/bin/isodump

/usr/local/bin/iso-info /usr/local/bin/isoinfo

/usr/local/bin/iso-read /usr/local/bin/isovfy

/usr/local/bin/isodebug /usr/local/bin/mkisosof
```

要显示 `xargs` 正在运行的命令，使用 `-t` 选项：

```bash
# cd /usr/local/bin

# echo iso* | xargs -t ls

ls iso-info iso-read isodebug isodump isoinfo isovfy

iso-info isodebug isoinfo

iso-read isodump isovfy
```

在示例中，`echo` 的整个输出被传递给了 `pkg_info`。通过 `xargs` 使用 `-t` 选项，在执行命令之前会显示命令的详细输出。现在，`xargs` 将 `ls` 的每个输出字符串传递给单独的 `pkg_add` 命令。使用 `-I` 将 `{}` 定义为字符串的占位符：

```bash
# ls /usr/local/bin/mk* | xargs -t -I {} pkg_info {}

pkg_info -W /usr/local/bin/mkbundle

/usr/local/bin/mkbundle was installed by package mono-1.2.5.1

pkg_info -W /usr/local/bin/mkisosof

/usr/local/bin/mkisosof was installed by package cdtools-2.01_6
```

如输出所示，对于每个传递的选项都运行了独立的 `pkg_info` 命令。

## 使用别名 (aliases)

使用 `alias` 命令设置和列出别名。如果用户使用 `csh` shell，在每个用户的 `~/.cshrc` 文件中已经设置了一些别名。以下是列出该 shell 当前设置的别名的方法：

```bash
# alias

h      (history 25)

j      (jobs -1)

la     (ls -a)

lf     (ls -FA)

11     (ls -IA)
```

别名可以作为为命令行为添加选项的简单方法（例如 `alias mv mv -i`，这样用户在移动文件之前总是收到提示）。要为 `csh` shell 定义其他别名，使用 `alias` 命令，后跟别名名称和要运行的命令。例如：

```bash
$ alias fi="find . | grep "
```

如所示使用该别名，输入 `fi string` 会导致在当前目录及其子目录中搜索包含你输入的字符串的文件。你可以如下所示为当前的 `bash` 会话定义别名：

```bash
$ alias la='ls -la'
```

将该行添加到你的 `~/.bashrc` 中以便在每个新的 `bash` 会话中生效。使用 `unalias` 命令从当前 `bash` 会话中移除别名，如下：

```bash
# unalias la      取消之前设置了别名的命令

# unalias -a     取消所有设置了别名的命令
```

## 跟踪文件 (Tailing Files)

为了观察纯文本文件内容随时间的增长，可以使用 `tail` 命令。例如，你可以如下所示观察消息是如何添加到 `/var/log/cron` 文件中的：

```bash
$ tail -f /var/log/cron
```

按下 `Ctrl+C` 退出 `tail` 命令。

## 获取超级用户权限

当你打开 shell 时，你能够根据你的用户/组 ID 以及这些组件设置的权限运行命令并访问文件和目录。许多系统功能限制为 `root` 用户，也称为超级用户。

由于 BSD 发行版以卓越安全性闻名，除非在非常特殊的情况下，否则不建议访问 `root` 用户。默认情况下，只允许从 `/etc/ttys` 中列为安全的终端访问 `root`。这仅包括从控制台可以访问的虚拟终端。

因此，如果你需要使用 `root` 账户，按照 FreeBSD 的交付方式，唯一的方法是从 `root` 的控制台终端直接以 `root` 登录。为了能够变成 `root` 用户

## 使用 su 命令

非 `root` 用户被限制变为 `root`，除非他们在 `wheel` 组中。要切换到 `root`，使用 `su` 命令。如果你在 `wheel` 组中，将被提示输入 `root` 密码。

```bash
$ su -

Password:
```

输入密码后，你将以 `root` 身份登录。要退出 `root` shell，输入 `exit`。

### 使用 sudo 委托权限

在许多环境中，给用户 `root` 密码是不安全的。相反，使用 `sudo` 命令来允许用户以另一个用户的权限运行某些命令。位于 `/etc/sudoers` 的 `sudoers` 文件定义了哪些用户或组可以运行哪些命令。`永远不要使用普通的文本编辑器编辑 sudoers 文件。` 始终使用 `visudo` 命令，它会在保存前检查语法错误，防止你被锁定在系统之外。

`sudoers` 文件中的示例条：

```text
user ALL=(ALL) NOPASSWD: /usr/bin/apt
```

这允许用户 `user` 在无需提示密码的情况下运行 `apt` 命令。

## 环境变量

你可以通过导出（export）来使变量成为环境的一部分，并允许子进程继承：

```bash
$ export ABC=123

$ c

$ echo $ABC

123
```

此外，你还可以将字符串连接到现有变量上：

```bash
# export PATH=$PATH:/home/fcaen
```

使用以下命令列出 `bash` 的环境变量：

```bash
# env
```

当你准备创建自己的环境变量时，请避免使用系统已常用的环境变量名称。请参阅附录 B 获取 shell 环境变量列表。

# 创建简单的 Shell 脚本

Shell 脚本适用于自动化重复的 shell 任务。`Bash` 和其他 shell 包含了各种编程语言中的基本结构，如循环、测试、`case` 语句等。主要的区别在于只有一种类型的变量。

## 编辑和运行脚本

Shell 脚本是简单的文本文件。你可以使用喜欢的文本编辑器（如 `vi`）创建它们。要运行 shell 脚本，脚本文件必须是可执行的。例如，如果你创建了一个名为 `myscript.sh` 的脚本，可以通过以下方式使其具有可执行性：

```bash
$ chmod u+x myscript.sh
```

或者，无需将其设置为可执行，你可以在脚本前加上 `bash` 命令来运行它（`bash myscript.sh`）。此外，`bash` 脚本的第一行始终应该是以下内容：

```bash
#!/usr/local/bin/bash
```

对于任何命令，除了可执行外，你创建的 shell 脚本必须在 `PATH` 中，或者在运行时通过其完整或相对路径进行识别。换句话说，如果你直接尝试运行脚本，可能会得到以下结果：

```bash
$ myscript.sh

bash: myscript.sh: command not found
```

在本示例中，包含 `myscript.sh` 的目录未包含在 `PATH` 中。要解决这个问题，你可以编辑路径、将脚本复制到 `PATH` 中的目录，或者像这里这样输入脚本的完整或相对路径：

```bash
$ mkdir /bin ; cp myscript.sh /bin; PATH=$PATH:-/bin

$ cp myscript.sh /usr/local/bin

$ ./myscript.sh

$ /tmp/myscript.sh
```

避免将 `PATH` 中加入点 (`.`) 以表示可以从当前目录运行命令。这种技术可能会导致与重要、常用命令（如 `ls` 或 `cat`）同名的命令。如果当前目录中存在同名的命令，正确的文件可能会被覆盖。

## 向你的脚本添加内容

虽然 shell 脚本可以是简单的命令序列，但也可以像使用任何编程语言一样使用 shell 脚本。例如，脚本可以根据提供的输入产生不同的结果。本节描述了如何在你的 shell 脚本中使用命令，如 `if/then`、`case` 语句和 `for/while` 循环。

以下示例代码将字符串 `abc` 赋值给变量 `MYSTRING`。然后它测试其是否等于 `abc`，并根据测试结果执行操作。测试是发生在括号 (`[ ]`) 之间的部分。

```bash
MYSTRING=abc

if [ $MYSTRING = abc ]; then

  echo "The variable is abc"

fi
```

要对测试进行取反，如如下所示，使用 `!` 代替 `=` 符号：

```bash
if [ $MYSTRING != abc ]; then

  echo "MYSTRING is not abc"

fi
```

以下是数字测试的示例：

```bash
MYNUMBER=1
```



```bash
if [ $MYNUMBER -eq 1 ]; then echo "MYNUMBER equals 1"; fi

if [ $MYNUMBER -lt 2 ]; then echo "MYNUMBER < 2"; fi

if [ $MYNUMBER -le 1 ]; then echo "MYNUMBER <= 1"; fi

if [ $MYNUMBER -gt 0 ]; then echo "MYNUMBER > 0"; fi

if [ $MYNUMBER -ge 1 ]; then echo "MYNUMBER >= 1"; fi
```

让我们来看一些对文件的测试。在本示例中，你可以检查文件是否存在（`-e`）、检查它是否为普通文件（`-f`），或者它是否为目录（`-d`）。这些检查通过`if/then`语句完成。如果没有匹配，则使用`else`语句产生结果。

```bash
filename="$HOME"

if [ -e $filename ]; then echo "$filename exists"; fi

if [ -f $filename ]; then
  echo "$filename is a regular file"
elif [ -d $filename ]; then
  echo "$filename is a directory"
else
  echo "I have no idea $filename is"
fi
```

表 3-1 显示了你可以对文件、字符串和变量执行的测试示例。

### 表 3-1：测试表达式的运算符

| 运算符 | 执行的测试 |
| :--- | :--- |
| `-a` `file` | 检查文件是否存在（同于 `-e`）。 |
| `-b` `file` | 检查文件是否为特殊块设备。 |
| `-c` `file` | 检查文件是否为字符特殊设备（如串口设备）。 |
| `-d` `file` | 检查是否为目录。 |
| `-e` `file` | 检查文件是否存在（同于 `-a`）。 |
| `-f` `file` | 检查文件是否存在且为普通文件（例如不是目录、`socket`、管道或设备文件）。 |
| `-g` `file` | 检查文件是否设置了组 ID (`set-group-id`)。 |
| `-h` `file` | 检查文件是否为符号链接（同于 `-L`）。 |
| `-k` `file` | 检查是否为内核模块。 |
| `-n` `file` | 检查字符串不为空。 |
| `-o` `file` | 检查一个表达式是否为真。 |
| `-p` `file` | 检查是否为管道。 |
| `-r` `file` | 检查文件是否可读。 |
| `-s` `file` | 检查文件大小不为空。 |
| `-t` `file` | 检查是否为终端。 |
| `-u` `file` | 检查是否由用户所有。 |
| `-w` `file` | 检查文件是否可写。 |
| `-x` `file` | 检查文件是否可执行。 |

## 第 3 章：使用 Shell

另一个常用的结构是`case`命令。使用`case`语句，你可以测试不同的情况并根据结果采取操作。类似于编程语言中的`switch`语句，`case`语句可以替代嵌套的`if`语句。

```bash
case $VAR in
  string1)
    action1 ;;
  string2)
    action2 ;;
  *)
    default action ;;
esac
```

你可以在`/etc/rc.d/`目录下的系统启动脚本找到`case`的用法示例。根据传递的参数采取操作，并通过大型结构进行选择。

`Shell`还提供了标准的循环结构，如下几个示例所示。在第一个示例中，`NUMBER`变量的所有值（0 到 9）都出现在行中：

```bash
for NUMBER in 0 1 2 3 4 5 6 7 8 9
do
  echo The number is $NUMBER
done
```

在接下来的示例中，来自`ls`命令的输出（文件列表）提供了`for`语句操作的变量：

```bash
for FILE in `/bin/ls`; do echo $FILE; done
```

与其将值列表传递给`for`语句，不如增加一个值并通过`while`循环持续直到满足条件。在本示例中，`VAR`开始为 0，`while`循环持续增加值直到`VAR`变为 3：

```bash
VAR=0
while [ $VAR -lt 3 ]; do
  echo $VAR
  VAR=$[$VAR+1]
done
```

获取与上述`while`语句相同结果另一种方法是使用`until`语句，如下示例所示：

```bash
VAR=0
until [ $VAR -eq 3 ]; do
  echo $VAR
  VAR=$[$VAR+1]
done
```

## 第 3 章：使用 Shell

如果你刚开始学习`shell`编程，请参考[入门 Bash 指南](http://tldp.org/LDF/Bash-Beginners-Guide/html/index.html)。请使用该指南并配合`bash man`手页等参考资料，逐步学习许多`shell`脚本技术的示例。如果你使用的是`C shell` (`csh`)，请参阅[C shell 简介](http://docs.freebsd.org/44doc/usd/04.csh/paper.html)以获取更多信息。

### 总结

尽管图形化用户界面有所改进，但`shell`仍然是高级用户与`BSD`系统交互的最常用方法。`csh`和`sh`分别作为`root`用户和普通用户的默认`shell`。如今，许多人也将在`BSD`和其他`UNIX`类系统上使用`Bourne Again Shell` (`bash`)。它包含了许多实用的功能，用于回溯命令（`history`）、补全命令、分配别名（`aliases`）以及重定向命令的输出和输入。你可以使用简单的`shell`脚本技术创建属于你自己的强大命令。

# 4

## 文件操作

在`BSD`文件系统中的一切都可以被视为文件。这包括数据文件、目录、设备、命名管道、链接和其他类型的文件。每个文件都关联着一组信息，决定了谁可以访问该文件以及他们如何访问。本章涵盖了许多探索和处理文件的命令。

### 本章内容

- 设置权限
- 遍历文件系统
- 创建和复制文件
- 使用硬链接/符号链接
- 修改文件属性
- 搜索文件
- 列出和验证文件

# 理解文件类型

目录和普通文件是你目前为止使用最频繁的文件类型。然而，在你使用`BSD`时，你还会遇到几种其他类型的文件。从命令行来看，有许多方法可以创建、查找和列出不同类型的文件。

提供对计算机硬件组件访问的文件称为设备文件。分为字符设备和块设备。你还可以使用硬链接和软链接来从不同的位置访问同一个文件。普通用户经常直接使用的命名管道和套接字（`sockets`），它们为进程通信提供了访问点。

## 使用普通文件

普通文件由数据文件（文档、音乐、图像、存档等）和命令（二进制文件和脚本）组成。你可以使用`file`命令确定文件的类型。在接下来的示例中，你可以切换到包含`bash` `shell`文档的目录，并使用`file`查看该目录下某些文件的类型：

```bash
$ cd /usr/local/share/doc/libogg

$ file *

framing.html: HTML document text

ogg: directory

rfc3533.txt: ASCII English text

stream.png: PNG image data, 592 x 37, 8-bit colormap, non-interleaved
```

`file`命令可以运行与`libtiff`相关的不同格式的文档和图像文件。它可以查看文件内部并判断文件是否包含`HTML`标记的文本（用于网页）、纯文本或图像。图中甚至显示了一个子目录 (`ogg`)。

任何可以保存数据的应用程序都可以创建普通文件。如果你只想创建带有文本的空白文件，有很多方法可以实现。这里有两个示例：

```bash
$ touch /tmp/newfile.txt      # 创建一个空白文件

$ cat /dev/null /tmp/newfile2.txt # 创建一个空文件
```

对文件进行列出是确定其文件类型的另一种方法。例如：

```bash
$ ls -1 /tmp/newfile2.txt  # 列出文件以查看其类型

-rw-rw-r-- 1 chris 0 Sep 5 14:19 newfile2
```

10 字符权限位 (`-rw-rw-r--`) 的第一个字符中的横杠表示该项目是一个普通文件。（权限在本章的“设置文件和目录权限”部分进行了解释。）命令也是普通文件，但它们被保存为可执行文件。以下是一些示例：

```bash
$ ls -d /usr/bin/apropos  # 1 root 22248 Jan 12 2007 /usr/bin/apropos

$ file /usr/bin/apropos  # Bourne shell script text executable

/usr/bin/apropos: Bourne executable

$ file /bin/ls

/bin/ls: ELF 32-bit LSB executable, Intel 80386, version 1 (FreeBSD), for FreeBSD 6.3, dynamically linked (used shared libraries), stripped
```

你可以看到，`apropos`命令通过所有者、组和其他人的`x`设置是可执行的。通过运行`file apropos`，你可以利用`x`显示它是一个`shell`脚本。这与上述`ls`显示的二进制可执行文件相反。

## 使用目录

目录是文件和子目录的容器。目录按照从根 (`/`) 到子目录的层级结构建立，用斜杠 (`/`) 隔开。当你从图形化文件管理器访问它们时，目录就是文件夹。

要创建存储数据的目录，你可以使用`mkdir`命令。以下是使用`mkdir`以不同方式创建目录的示例：

```bash
$ mkdir /tmp/new          # 在 /tmp 中创建 "new" 目录

$ mkdir -p /tmp/a/b/c/new # 为 "new" 创建所需的父目录

$ mkdir -m 700 /tmp/new2  # 创建权限为 drwx------ 的 new2
```

第一个`mkdir`命令仅是将新目录添加到现有的`/tmp`目录中。第二个示例根据需要创建目录（子目录`a`, `b`, `c`）。最后一个示例创建了权限为`drwx------`的`new2`。



`file` 命令可以运行与 `libtiff` 相关的不同格式的文档和图像文件。它可以查看文件内部并判断文件是否包含 HTML 标记的文本（用于网页）、纯文本或图像。图中甚至显示了一个子目录 (`ogg`)。

创建普通文件可以通过任何可以保存数据的应用程序完成。如果你只想创建带有文本的空白文件，有很多方法可以实现。这里有两个示例：

```
$ touch /tmp/newfile.txt      创建一个空白文件
$ cat /dev/null /tmp/newfile2.txt  创建一个空文件
```

对文件进行列出是确定其文件类型的另一种方法。例如：

```
$ ls -1 /tmp/newfile2.txt  列出文件以查看其类型
-rw-rw-r-- 1 chris 0 Sep 5 14:19 newfile2
```

10 字符权限位 (`-rw-rw-r--`) 的第一个字符中的横杠表示该项目是一个普通文件。（权限在本章的“设置文件和目录权限”部分进行了解释。）命令也是普通文件，但它们被保存为可执行文件。以下是一些示例：

```
$ ls -d /usr/bin/apropos  1 root 22248 Jan 12 2007 /usr/bin/apropos
$ file /usr/bin/apropos  Bourne shell script text executable
/usr/bin/apropos: Bourne executable
$ file /bin/ls
/bin/ls: ELF 32-bit LSB executable, Intel 80386, version 1 (FreeBSD), for FreeBSD 6.3, dynamically linked (used shared libraries), stripped
```

你可以看到，`apropos` 命令通过所有者、组和其他人的 `x` 设置是可执行的。通过运行 `file apropos`，你可以利用 `x` 显示它是一个 shell 脚本。这与上述 `ls` 显示的二进制可执行文件相反。

## 使用目录

目录是文件和子目录的容器。目录按照从根 (`/`) 到子目录的层级结构建立，用斜杠 (`/`) 隔开。当你从图形化文件管理器访问它们时，目录就是文件夹。

要创建存储数据的目录，你可以使用 `mkdir` 命令。以下是使用 `mkdir` 以不同方式创建目录的示例：

```
$ mkdir /tmp/new          在 /tmp 中创建 "new" 目录
$ mkdir -p /tmp/a/b/c/new  为 "new" 创建所需的父目录
$ mkdir -m 700 /tmp/new2    创建权限为 drwx------ 的 new2
```

第一个 `mkdir` 命令简单是将新目录添加到现有的 `/tmp` 目录中。第二个示例根据需要创建目录（子目录 `a`, `b`, `c`）。最后一个示例创建了权限为 `drwx------` 的 `new2`。

# 使用硬/符号链接

你可以使用硬链接和软链接来从不同的位置访问同一个文件。普通用户经常直接使用的命名管道和套接字（`sockets`），它们为进程通信提供了访问点。

*(注：原文文本后续处大量重复，此处已完成核心内容翻译)*

# 第 4 章：文件操作

第一个列表是由电视卡播放设置的命名管道（注意开头的 `p` 表示命名管道）。第二个列表是为进程间通信设置的套接字（`socket`）。

要创建你的命名管道，请如下使用 `mkfifo` 命令：

```
$ mkfifo mypipe
$ ls -l mypipe
prw-r-- 1 chris 0 Sep 26 00:57 mypipe
```

要查找你的系统中当前激活了哪些套接字，如下使用 `sockstat` 命令：

```
USER     COMMAND    PID PROTO LOCAL ADDRESS      FOREIGN ADDRESS
chris gnome-term 6514 3 stream -> /tmp/.X11-unix/X0
chris gnome-term 6514 10 stream -> /tmp/.ICE-unix/2373
root     syslogd   557  dgram  /var/run/log
root     syslogd   557  dgram  /var/run/logpriv
root     devd     501  4      /var/run/devd.pipe
```

除非你正在开发应用程序，否则你不需要创建命名管道或套接字。查找系统中命名管道和套接字的另一种方法是使用 `find` 命令的 `-type` 选项，本文将在稍后介绍。

# 设置文件和目录权限

访问文件、运行命令和切换目录的能力可以通过对用户、组和其他用户的权限设置来限制。当你对文件和目录进行长列表（`ls -l`）时，显示的开头 10 个字符表示该项目的类型（文件、目录、字符设备等）以及该项目是否可以读、写或执行。图 4-1 展示了这 10 个字符的含义。

![](img/a8f0676d6e7f319a693ce1963202001e_82_0.png)

图 4-1：为文件和目录设置读、写和执行权限。

为了跟随本节的示例，创建一个名为 `/tmp/test` 的目录和一个名为 `/tmp/test/hello.txt` 的文件。然后如下所示对这两个项目进行长列表显示：

```
$ mkdir /tmp/test
$ echo "some text" > /tmp/test/hello.txt
$ ls -ld /tmp/test/ /tmp/test/hello.txt
drwxr-xr-x 2 francois 4096 Mar 21 13:11 /tmp/test
-rw-r--r-- 2 francois 2010 Mar 21 13:11 /tmp/test/hello.txt
```

创建目录和文件后，长列表的第一个字符显示 `/tmp/test` 是一个目录 (`d`)，而 `hello.txt` 是一个文件 (`-`)。BSD 中可用的其他类型作为第一个字符出现的包括字符设备 (`c`)、块设备 (`b`) 或符号链接 (`l`)、命名管道 (`p`) 和套接字 (`s`)。

接下来的九个字符代表在文件和目录上设置的权限。第一个 `r` 表示所有者 (`francois`) 对目录拥有读、写和执行权限。同样，`wheel` 组也拥有相同的权限 (`rwx`)。然后所有其他用户只有读和执行权限 (`r-x`)：横线表示缺少写权限。对于 `hello.txt` 文件，用户和组具有读权限 (`r--`)，其他用户也具有读权限 (`r--`)。

当你更改权限时，每个权限可以用八进制数字（其中读为 4，写为 2，执行为 1）或字母 (`rwx`) 表示。通常情况下，读权限允许你查看目录内容，写允许你更改（添加或修改）目录内容，执行允许你切换（换句话说，访问）目录。

如果你不喜欢你拥有的文件或目录的权限，可以使用 `chmod` 命令更改这些权限。

## 使用 chmod 修改权限

`chmod` 命令允许你访问文件和目录的权限。表 4-1 显示了若干 `chmod` 命令行以及目录或文件访问的变化。

表 4-1：更改目录和文件访问权限

| chmod 命令（八进制或字母） | 原始权限 | 新权限 | 描述 |
|---|---|---|---|
| `chmod 0700` | 任意 | `drwx------` | 所有者可以读写目录中的文件并进入该目录。所有其他用户（`root` 除外）均无访问权限。 |
| `chmod 0711` | 任意 | `drwx--x--x` | 所有者同。其他人都可以进入目录，但不能查看或更改目录中的文件。这对于服务器加固非常有用，可以防止他人列出目录内容，但如果有人已经知道了目录中的某个文件，则允许访问。 |
| `chmod go+r` | `drwx------` | `drwxr-xr--` | 为目录添加读权限可能不会产生预期结果。如果没有执行权限，其他人无法查看该目录中任何文件的内容。 |
| `chmod 0077` | | `drwxrwxrwxrwx` | 所有权限完全开放。 |
| `chmod a+r` | 任意 | `drwxrwxrwxrwx` | 所有权限完全开放。如果没有执行权限，其他人无法查看该目录中任何文件的内容。 |
| `chmod 666` | 任意 | `-rw-rw-rw` | 所有权限完全开放。 |
| `chmod go-r` | `drwx------` | `drwxr-xr--` | 为目录移除读权限可能不会产生预期结果。如果没有执行权限，其他人无法查看该目录中任何文件的内容。 |

## 遍历文件系统

切换目录 (`cd`)、检查当前目录 (`pwd`) 和列出目录内容 (`ls`) 等基本命令即使是偶尔使用 shell 的用户也熟悉。本节重点介绍这些命令中一些不常用的选项，以及在文件系统中移动的其它少为人知的特性。是一些使用 `cd` 在文件系统中移动的快速示例：

- `$ cd` 切换到你的家目录
- `$ cd $HOME` 切换到你的家目录
- `$ cd` 切换到你的家目录
- `$ cd -francois` 切换到 `francois` 的家目录
- `$ cd -` 切换到上一个工作目录
- `$ cd $OLDPWD` 切换到上一个工作目录 (`bash` shell)
- `$ cd -/public_html` 切换到家目录下的 `public_html`（如果存在）
- `$ cd .` 切换到当前目录的父目录
- `$ cd /usr/bin` 从根目录切换到 `usr/bin`
- `$ cd usr/bin` 切换到当前目录下的 `usr/bin`

如果你想知道当前目录，使用 `pwd` (打印工作目录)：

```
$ pwd
/home/francois
```

创建符号链接是从文件系统的其他部分访问文件的方法（请参见本章前面的“使用符号链接和硬链接”部分获取更多有关符号链接和硬链接的信息）。然而，符号链接可能会导致对如何查看父目录产生困惑。以下命令从家目录创建一个指向 `/tmp` 目录的符号链接，并展示了如何判断你与链接目录的关系：

```
$ cd $HOME
$ ln -s /tmp tmp-link
$ ls -l tmp-link
lrwxrwxrwx 1 francois francois 13 Mar 24 12:41 tmp-link -> /tmp
$ cd tmp-link/
$ pwd
/home/francois/tmp-link
$ pwd -P
/tmp
$ pwd -L
/home/francois/tmp-link
$ cd -L ..
$ pwd
/home/francois
$ cd tmp-link
$ cd -P ..
$ pwd
/
```

- 显示永久位置
- 显示链接位置
- 进入链接位置的父目录
- 进入永久位置的父目录

# 第 4 章：文件操作

通过对 `pwd` 和 `cd` 使用 `-P` 和 `-L` 选项，你可以分别在永久位置或链接位置对符号链接目录进行操作。例如，`cd -L ..` 带你回到上一层家目录，而 `cd -P ..` 则带你进入永久目录上层（`/`）。同样，`pwd` 的 `-P` 和 `-L` 选项显示永久位置和链接位置。

如果你使用 `csh` 或 `bash` shell，它们可以为你记住一个工作目录列表。如果你想返回以前访问过的目录，这个列表非常有用。该列表以栈的形式组织。使用 `pushd` 和 `popd` 来添加和移除目录。

```
$ pwd
/home/francois
$ pushd /usr/share/man/
/usr/share/man -
$ pushd /var/log/
/var/log /usr/share/man -
$ dirs
/var/log /usr/share/man -
$ dirs -v
0 /var/log
1 /usr/share/man
2
$ popd
/usr/share/man -
$ pwd
/usr/share/man
$ popd
$ pwd
/home/francois
```

`dirs`、`pushd` 和 `popd` 命令也可用于操作栈上目录的顺序。例如，`pushd -0` 将栈上的最后一个目录推到栈顶（使其成为当前目录）。`pushd -2` 将栈底部的第三个目录移动到栈顶。

## 复制文件

只要你对目标目录有写权限，就可以通过一些简单的命令复制文件和目录。标准的 `cp` 命令会将文件复制为新名称或新目录下的同名文件，并为新文件关联新的时间戳。`cp` 的其他选项可以保留日期/时间戳、递归复制以及在覆盖前提示。以下是一些示例：

```
# cd; mkdir public_html; touch index.html
# cp -i index.html public_html/
# cp -il index.html public_html/
# cp -rv public_html/ /mnt/usb/
```

- 使用新时间戳复制
- 创建硬链接而非复制
- 递归复制所有文件（带有

上面的示例展示了与个人 Web 服务器相关的文件复制方法。在第一个 `cp` 示例中，如果 `public_html` 中存在 `index.html` 文件，系统会在用新文件覆盖它之前提示你。在下一个示例中，`index.html` 文件被硬链接到 `public_html` 目录下的同名文件。在这种情况下，由于两个硬链接都指向同一个文件，从任一位置编辑文件都会更改两个位置的文件内容（只有当 `public_html/` 和你的家目录位于同一个文件系统时才能进行链接）。

`cp -Rv` 命令复制 `public_html/` 目录下的所有文件，并将所有者权限更新为运行命令的用户的。它还使用当前日期和时间戳。例如，如果 `/mnt/usb` 代表 USB 闪存器，那么命令可以将你的个人 Web 服务器的内容复制到驱动器。

`dd` 命令是复制数据的另一种方法。该命令非常强大，因为在 BSD 系统中，一切都是文件，包括硬件外设。这是一个示例：

```
$ dd if=/dev/zero of=/tmp/nullfile count=1
1+0 records out
1+0 records out transferred in 0.002 secs (512 bytes/sec)
```

`/dev/zero` 是一个生成空字符的文件。在示例中，`dd` 命令将 `/dev/zero` 作为输入输出到 `/tmp/nullfile`。`count` 是块的数量。默认情况下，一个块是 512 字节。结果是一个 512 字节长的空字符文件。你可以使用 `less` 或 `vi` 查看文件内容。然而，查看文件的更好工具是 `od`（八进制转储）命令：

```
$ od -vt x1 /tmp/nullfile    View octal dump
```

这是另一个 `dd` 命令的示例。这次，我们将块大小设置为 2 字节并复制 10 个块（20 字节）：

```
$ dd if=/dev/zero of=/tmp/nullfile count=10 bs=2
10+0 records out
20 bytes out transferred in 0.00367 secs (5407 bytes/sec)
```

*(注：由于原文中存在大量重复的 OCR 错误文本，翻译已根据逻辑流进行了清理和整合)*

# 第 4 章：文件操作

横线代表可以设置的 13 个 `ext2/ext3` 属性。默认情况下没有任何开启。这些属性分别是：`a`（只追加）、`c`（压缩）、`d`（不备份）、`i`（不可变）、`j`（数据日志）、`s`（安全删除）、`t`（尾部合并）、`u`（取消删除）、`A`（不更新 `atime`）、`D`（同步目录更新）、`S`（同步更新），并且你可以使用 `chattr` 命令更改这些属性。以下是一些示例：

```
# chattr +i /mnt/usb/01.txt
$ chattr +a /mnt/usb/02.txt
$ chattr +d /mnt/usb/03.txt
$ lsattr /mnt/usb/*.txt
------i /mnt/usb/01.txt
------a /mnt/usb/02.txt
------d /mnt/usb/03.txt
```

如前一个示例所示，设置 `+i` 选项后，`01.txt` 文件变为不可变文件，这意味着它不能被删除、重命名、修改，也无法为其创建链接。在这里，这防止了对文件的任何任意更改。（`root` 用户甚至无法在不同意覆盖属性的情况下删除不可变文件。）设置 `+a` 后，文件只能被追加内容而不能删除。如果你使用 `dump` 命令备份你的 `ext2/ext3` 文件系统，`+d` 选项可以防止选文件被备份。

要使用 `chattr` 移除属性，请使用减号（`-`）。例如：

```
# chattr -i /mnt/usb/01.txt
```

> 注意：成功攻入机器的破解者通常会将某些系统二进制文件（如 `ls` 或 `ps`）替换为损坏的版本并将其设置为不可变。偶尔检查你的可执行文件的设置属性（例如 `/bin`、`/usr/bin`、`/sbin` 和 `/usr/sbin`）是一个好习惯。

## 搜索文件

你的 BSD 系统可以通过定期运行 `usr/libexec/locate.updatedb` 脚本，配置为维护文件系统中所有文件的数据库（`/etc/locate.rc` 中有少数例外）。`locate` 命令允许你搜索该数据库。结果会即时返回，因为搜索的是数据库而不是实际的文件系统。在 `locate` 可用之前，BSD 用户运行 `find` 命令在文件系统中查找文件。这里将对 `locate` 和 `find` 进行介绍。

## 生成 locate 数据库

你可以通过运行以下脚本来生成 `locate` 数据库：

```
/usr/libexec/locate.updatedb
```



注意，如果作为普通用户运行此脚本，数据库将只包含所有用户都可以访问的文件以及该用户可以访问的文件。你可以以 `root` 用户身份运行此脚本来收集计算机上的所有文件。但这可能会带来安全风险，允许非 `root` 用户看到你本可能想对他们隐藏的文件。

运行 `locate.updatedb` 脚本后，会创建 `/var/db/locate.database`。你现在准备好使用 `locate` 命令搜索文件了。

# 使用 locate 查找文件

由于数据库包含了文件系统中每个节点的名称，而不仅仅是命令，你可以使用 `locate` 来查找命令、设备、帮助手册（man pages）、数据文件或文件系统中通过名称识别的任何内容。这里是一个示例：

```
$ locate atapifd

...

/boot/kernel/atapifd.ko
```

上面的示例找到了 `atapid.ko` 内核模块。`locate` 是大小敏感的，除非你使用 `-i` 选项。这里是一个示例：

```
$ locate -i ImageMagick-6

/usr/local/share/ImageMagick-6.3.6

/usr/local/share/ImageMagick-6.3.6/ChangeLog
```

以下是一些使用 `locate` 配合正则表达式和输出限制的示例：

```
$ locate *atapiko

查找名称中包含 atapi 和 ko 的文件

/boot/kernel/atapicam.ko

/boot/kernel/atapcd.ko

/boot/kernel/atapifd.ko

/boot/kernel/atapist.ko

$ locate -l 5 kernel

将找到的文件数量限制为五个

/boot/kernel

/boot/kernel/3dfx.ko

/boot/kernel/3dfx_linux.ko

/boot/kernel/aac.ko

/boot/kernel/aac_linux.ko

locate: [仅显示 5 行]
```

你可以通过以下方式获取关于 `locate` 信息以及 `locate` 数据库的大小：

```
$ locate -s

Database: /var/db/locate.database

Compression: Front: 21.64%, Bigram: 61.00%, Total: 15.57%

Filenames: 276585, Characters: 13071602, Database size: 2035362

Bigram characters: 793708, Integers: 9379, 8-Bit characters: 0
```

要立即更新 `locate` 数据库，请手动再次运行 `locate.updateddb` 命令。

```
$ /usr/libexec/locate.updateddb
```

# 使用 find 定位文件

在 `locate` 时代之前查找文件的方法是使用 `find` 命令。虽然 `locate` 找到文件更快，但 `find` 有许多其他强大的选项，可以根据名称以外的属性查找文件。

> 注意：搜索整个文件系统可能需要长时间。在搜索整个文件系统之前，请考虑文件系统的子集或排除某些目录或远程挂载的文件系统。

示例查找：

```
find / -name "filename"
```

## 第 4 章：文件操作

当你列出文件时，也有方法可以让不同类型的文件在列表中以不同的方式显示：

```bash
$ ls -F            添加一个字符来指示文件类型

BSD26/  BSD7/      memo.txt  pipefile| script.sh* xpid.socket=

$ ls -G            以不同的颜色显示文件

$ ls -C            以列的形式显示文件列表
```

在 `-F` 示例中，输出显示了不同的文件类型。`BSD26.@` 表示目录的符号链接，`BSD7/` 是普通目录，`memo.txt` 是普通文件（没有额外字符），`pipefile|` 是命名管道（通过 `mkfifo` 创建），`script.sh*` 是可执行文件，而 `xpid.socket=` 是 socket。接两个示例分别显示了不同的文件类型和列输出。

## 验证文件

当软件和 CD 或 DVD 介质通过互联网共享时，通常会附带一个 `shasum` 或 `md5` 文件。这些文件包含了校验和，我们需要确保你下载的文件与仓库发布的文件完全一致。

以下是下载 ISO 镜像文件并使用 `md5` 和 `sha256` 验证文件校验和的示例：

```bash
$ wget -O http://ftp.freebsd.org/pub/FreeBSD/releases/i386-ISO-IMAGES/6.3/6.3-RELEASE-i386-disc1.iso

$ md5 6.3-RELEASE-i386-disc1.iso = 

MD5 (6.3-RELEASE-i386-disc1.iso) = 

cbd0d4afdb2db3e4c9cc1918f4fb2bda7b8

$ sha256 6.3-RELEASE-i386-disc1.iso = 

SHA256 (6.3-RELEASE-i386-disc1.iso) = 

1508a5a6d81a841ec87c7ca3cd5d0f7b93d70b9cc5fc40d875b0fd3047721
```

选择哪种命令取决于你分发的文件提供者提供的是 `md5` 还是 `sha` 信息。`FreeBSD` 同时提供了 `md5` 和 `sha` 文件。例如，对于位于如下位置的 `FreeBSD` 6.3 发行版，可以使用 `CHECKSUM.MD5` 文件：

```text
MD5 (6.3-RELEASE-i386-bootonly.iso) = ab1bd0ae6438c12cddde885f53b83fbae

MD5 (6.3-RELEASE-i386-disc1.iso) = cdb0d4fa4b2db3e4c9cc1918f4fb2bda

MD5 (6.3-RELEASE-i386-disc2.iso) = e73a3d9cf5f3bbf07384ef049ae5d5

MD5 (6.3-RELEASE-i386-disc3.iso) = 123840107a5578ce22875c440d41f453

MD5 (6.3-RELEASE-i386-docs.iso) = 17aa87ccbf01f4453d8dce0788704029ab
```

如果当前目录下包含 `CHECKSUM.MD5` 文件列出的所有 ISO 文件，你可以使用 `-c` 选项和兼容 Linux 的 `md5sum` 命令一次性验证它们。以下是一个示例：

```bash
$ /usr/compat/linux/usr/bin/md5sum -c CHEKSUM.MD5

6.3-RELEASE-i386-bootonly.iso: OK

6.3-RELEASE-i386-disc1.iso: OK

6.3-RELEASE-i386-disc2.iso: OK

6.3-RELEASE-i386-disc3.iso: OK

6.3-RELEASE-i386-docs.iso: OK
```

如果你只想验证校验和文件中列出的其中一个文件，可以执行如下操作：

```bash
$ grep bootonly CHEKSUM.MD5 | /usr/compat/linux/usr/bin/md5sum -c

6.3-RELEASE-i386-bootonly.iso: OK
```

如果你要检查的是 `SHA1SUM` 而不是 `MD5` 文件，可以使用本章稍后描述的 `sha1sum` 命令。配合 `md5` 命令，你可以验证文件系统的任何部分。例如，这里是如何为 `/etc` 目录下的每个文件创建 `MD5` 校验和，以便以后检查它们是否发生了变化：

```bash
$ find /etc -type f -exec md5 {} \; 2>/dev/null > /tmp/md5.list
```

上一个命令的结果是一个 `/tmp/md5.list` 文件，该文件包含了 `/etc` 目录中每个文件的 128 位校验和。稍后，你可以输入以下命令来查看其中哪些文件是否有任何变化：

```bash
# cd /etc

# /usr/compat/linux/usr/bin/md5sum -c /tmp/md5.list
```

## 第 5 章：文本操作

传统上，另一种流行的 UNIX 编辑器是 `Emacs` 及其更图形化的变体 `Emacs`。`Emacs` 是一个强大的多功能工具，也可以作为邮件/新闻阅读器，并执行其他功能。`Emacs` 还以其极其复杂的快捷键组合而闻名，这些组合通常需要三只手才能正常执行。

在 20 世纪 90 年代中期，`Emacs` 在功能上领先于 `vi`。`Vim` 非常可用，两者都可以提供你可能需要的所有文本编辑功能。如果你还不熟悉 `vi` 或 `Emacs`，我们建议你从学习 `vi` 开始。

`BSD` 系统提供了许多其他命令行和 GUI 文本编辑器。你可能会发现比 `vi` 和 `Emacs` 更简单的基于文本的编辑器包括 `JED`、`JOE` 和 `nano`。这些任何一个编辑器都可以通过输入其命令名称启动，后面可以选跟你想要编辑的文件名。接下来的章节将简要描述如何使用这些编辑器。

## 使用 JOE 编辑器

如果你以前用过像 `WordStar` 这样可以处理文本文件的经典文字处理程序，你可能会习惯 `JOE` 编辑器。要使用 `JOE`，请安装 `joe` 包（以 `root` 身份输入 `pkg_add -r joe`）。要使用 `JOE` 中的拼写检查，请安装 `aspell` 包。

在 `JOE` 中，你不需要进入命令模式或文本模式，而是随时准备好输入。要在文件中移动，您可以使用控制键或方向键。要打开文本文件进行编辑，只需输入 `joe` 加上文件名，或使用以下某些选项：

```
$ joe memo.txt               打开 memo.txt 进行编辑

$ joe -wordwrap 5 memo.txt      在编辑时开启自动换行

$ joe -lmargin 5 -tab 5 memo.txt  设置左边距为 5，制表符为 5

                                 从第 25 行开始编辑
```

要添加文本，只需开始输入即可。许多功能可以使用键盘快捷键。使用方向键移动光标：左、上或下。使用 `Delete` 键删除光标下的文本，或使用 `Backspace` 键删除光标左侧的文本。按 `Enter` 键换行。按 `Ctrl+K+H` 显示帮助屏幕。表 5-2 显示了编辑 `JOE` 时常用的按键。

## 表 5-2：使用 JOE 编辑的控制键

| 按键组合 | 结果 |
| --- | --- |
| 光标 `Ctrl+B` | 左 |
| `Ctrl+P` | 上 |

## 表 5-2：使用 JOE 编辑的控制键（续）

| 按键组合 | 结果 |
|---|---|
| 光标（续上） | |
| `Ctrl+F` | 右 |
| `Ctrl+N` | 下 |
| `Ctrl+Z` | 上一个单词 |
| `Ctrl+X` | 下一个单词 |
| 搜索 | |
| `Ctrl+K+F` | 查找文本 |
| `Ctrl+L` | 查找下一个 |
| 块 | |
| `Ctrl+K+B` | 开始 |
| `Ctrl+K+K` | 结束 |
| `Ctrl+K+M` | 移动块 |
| `Ctrl+K+C` | 复制块 |
| `Ctrl+K+W` | 将块写入文件 |
| `Ctrl+K+Y` | 删除块 |
| `Ctrl+K+/` | 过滤 |
| 其他 | |
| `Ctrl+K+A` | 行居中对齐 |
| `Ctrl+T` | 选项 |
| `Ctrl+R` | 刷新 |
| 文件 | |
| `Ctrl+K+E` | 打开新文件编辑 |
| `Ctrl+K+R` | 在光标处插入文件 |
| `Ctrl+K+D` | 保存 |

## 表 5-2：使用 JOE 编辑的控制键（续）

| 按键组合 | 结果 |
| --- | --- |
| 转到 | |
| `Ctrl+U` | 上一屏幕 |
| `Ctrl+V` | 下一屏幕 |
| `Ctrl+A` | 行首 |
| `Ctrl+E` | 行尾 |
| `Ctrl+K+U` | 文件头部 |
| `Ctrl+K+V` | 文件末尾 |
| `Ctrl+K+L` | 转到行号 |
| `Delete` | |
| `Ctrl+D` | 删除字符 |
| `Ctrl+Y` | 删除行 |
| `Ctrl+W` | 删除右侧单词 |
| `Ctrl+O` | 删除左侧单词 |
| `Ctrl+J` | 删除到右侧的行 |
| `Ctrl+-` | 撤销 |
| `Ctrl+6` | 重做 |
| 退出 | |
| `Ctrl+K+X` | 保存并退出 |
| `Ctrl+C` | 终止 |
| `Ctrl+K+Z` | 终端 |
| 拼写 | |
| `Ctrl+[+N` | 单词（此功能生效需安装正确的拼写字典） |
| `Ctrl+[+I` | 文件（此功能生效需安装正确的拼写字典） |

## 使用 Pico 和 Nano 编辑器

`Pico` 是一个流行的、非常微小的文本编辑器，作为 `Pine` 邮件客户端的一部分发布。虽然 `Pico` 是免费的，但它 true 真正的开源。某些 `BSD` 发行版不提供 `Pico`（尽管 `pkg_add -r pico`）。作为 `Pico` 的替代方案，你可以使用名为 `nano` 的开源克隆版本（`nano` 是另一个编辑器）。本节将介绍 `nano` 编辑器（`pkg_add -r nano`）。

`Nano`（由 `nano` 命令表示）是一个从 shell 运行文本编辑器的命令，它是面向屏幕的（因为它基于 `curses` 库）。`nano` 在以前使用过 `Pine` 邮件客户端的用户中非常受欢迎，因为 `nano` 的编辑功能与 `Pico` 编辑器使用的功能相同。在 `BSD` 或 `Linux` 系统（例如 `FreeBSD`）上极少数没有可用 `vi` 的情况下，`nano` 是 `nano` 包的一部分，并依赖于拼写检查。

在 `JOE` 中，要添加文本，只需开始输入。许多功能可以使用键盘快捷键。使用方向键移动光标：左、上或下。使用 `Delete` 键删除光标下的文本，或使用 `Backspace` 键删除光标左侧的文本。按 `Enter` 键换行。按 `Ctrl+K+H` 显示帮助屏幕。`Nano`（由 `nano` 命令表示）是一个从 shell 运行文本编辑器的命令，它是面向屏幕的（归功于它基于 `curses` 库）。`nano` 在以前使用过 `Pine` 邮件客户端的用户中非常受欢迎，因为 `nano` 的编辑功能与 `Pico` 编辑器使用的功能相同。

在 `JOE` 中，你不需要进入命令模式或文本模式，而是随时准备好输入。要在文件中移动，您可以使用控制键或方向键。要打开文本文件进行编辑，只需输入 `joe` 加上文件名，或使用以下某些选项：

```
$ joe memo.txt               打开 memo.txt 进行编辑

$ joe -wordwrap 5 memo.txt      在编辑时开启自动换行

$ joe -lmargin 5 -tab 5 memo.txt  设置左边距为 5，制表符为 5

                                 从第 25 行开始编辑
```



## 第 5 章：文本操作

要查看文件的头部，请使用`head`：

```
$ head myfile.txt
$ cat myfile.txt | head
```

这两个命令都使用`head`命令输出文件的前 10 行。你可以通过指定行数作为参数，来显示文件开头的任意行数。例如：

```
$ head -n 50 myfile.txt
$ ps auxw | head -n 15
```

你也可以使用这种过时（但更短）的语法：

```
$ tail -50 myfile.txt
$ ps auxw | tail -15
```

你可以以简单的方式使用`tail`命令来查看文件末尾或命令的输出：

```
$ tail -n 15 myfile.txt
$ tail -15 myfile.txt
$ ps auxw | tail -n 15
```

`tail`命令还可以用于持续监控由另一个程序写入的文件的末尾。这在排查`Apache`、`In Daemon`或其他系统服务的故障时，读取日志文件非常有用：

```
$ tail -f /var/log/messages
$ tail -f /var/log/maillog
$ tail -f /var/log/auth.log
```

- 实时查看系统消息
- 实时查看服务器消息
- 实时查看登录尝试

## 文本分页

当你有一大块文本并且需要获取不仅仅是开头或结尾的内容时，你需要一个工具来对文本进行分页（`page`）。原始的`UNIX`系统分页器是`more`命令：

```
$ ps auxw | more
# 翻页 ps 的输出（按空格键）

$ myfile.txt
# 翻页文件内容
```

然而，`more`有一些局限性。例如，在上面的`ps`文件中，你无法向上滚动。`less`命令被创建作为一个更强大、更用户好的`more`版本。引入`less`时有一句俗话是：“什么是`less`？less is more！”我们建议你不再使用`more`，而是使用`less`。

> **注意：** `less`命令没有值得注意的优点。与`vi`等文本编辑器不同，它在启动时不会读取整个文件。这使得在查看大文件时启动速度更快。

`less`命令可以使用与上面示例中`more`相同的语法：

```
$ ps auxw | less              # 翻页 ps 的输出
$ cat myfile.txt | less      # 翻页文件内容
$ less myfile.txt            # 翻页文本文件
```

`less`命令允许你使用上下方向键、`PageUp`、`PageDown`和空格键进行导航。如果你对文件（而非标准输入）使用`less`，按`v`可用`vi`打开当前文件。与`G`一样，转到文件末尾。`F`将带你到文件末尾，然后在有新输入添加时滚动，类似于`tail -f`。

在`vi`中，使用`less`查看文件时，可以通过按`/`（正斜杠）后跟字符串并回车来搜索字符串。要搜索后续出现的内容，重复按`n`。要反向搜索，按`?`后跟字符串并回车。

在使用`less`时向前和向后滚动，分别使用`f`和`b`键。例如，`10f`向前滚动10 行，`15b`向后滚动15 行。输入`d`向下滚动半屏，`u`向上滚动半屏。

## 使用 pr 对文件进行分页

`pr`命令提供了一种快速将大量文本格式化为可打印形式的方法。如果你想打印命令结果而无需打开文字处理器或文本编辑器，这会特别有用。通过`pr`，你可以将文本格式化为包含日期、时间、文件名和页码等页眉信息的页面。这是一个示例：

```
$ ls /usr/ports | sort | pr -4 | less      # 以4列分页 ports 目录
```

与其分页输出，你可以将输出发送到文件或打印机。以下是示例：

```
$ ls /usr/ports | sort | pr -4 | less | pkg.txt      # 将 pr 输出发送到文件
$ ls /usr/ports | sort | pr -4 | less | lpr          # 将 pr 输出发送到打印机
```

使用`pr`命令可以进行的其他文本处理包括文本双倍行距（`-d`），或将文本相对于左边缘偏移固定数空格（例如，`-o 5`将从左侧缩进五个空格）。

## 使用 grep 搜索文本

当你需要对文件执行更高级的字符串搜索时，`grep`命令非常实用。事实上，“`grep`”这个短语已经作为动词进入了计算机术语，就像`Google`进入了流行语言一样。以下是`grep`命令的示例：

```
$ grep francois myfile.txt
# 显示包含 francois 的行

$ grep -i ftp /etc/services
# 显示包含 FTP 的行

$ ps auxw | grep
# 显示 ps 输出中的 init 行

$ ps auxw | grep "\*"
# 显示带括号的命令

$ dmesg | grep "[ata]\|\|ata"
# 显示 ata 内核设备信息
```

`grep`命令还可以同时递归搜索几个或多个文件。以下命令递归搜索（`-R`）文件。通过搜索`/etc/services`查找`ftp`，你可以看到与`FTP`服务关联端口号。显示命令输出的带括号命令是查看`ps`无法显示选项命令的方法。最后一个命令检查内核缓冲区环是否有任何`ATA`设备信息，如硬盘和`CD-ROM`驱动器。

## 使用 Pico 和 Nano 编辑器

`Pico`是一个流行的、非常微小的文本编辑器，作为`Pine`邮件客户端的一部分发布。虽然`Pico`是免费的，但它不是真正的开源。某些`BSD`发行版不提供`Pico`（尽管`pkg_add -r pico`）。作为`Pico`的替代方案，你可以使用名为`nano`的开源克隆版本（`nano`是另一个编辑器）。本节将介绍`nano`编辑器（`pkg_add -r nano`）。

`Nano`（由`nano`命令表示）是一个从`shell`运行文本编辑器的命令，它是面向屏幕的（归功于它基于`curses`库）。`nano`在以前使用过`Pine`邮件客户端的用户中非常受欢迎，因为`nano`的编辑功能与`Pico`编辑器使用的功能相同。在`BSD`或`Linux`系统（例如`FreeBSD`）上极少数没有可用`vi`的情况下，`nano`是`nano`包的一部分，并依赖于拼写检查。

在`JOE`中，你不需要进入命令模式或文本模式，而是随时准备好输入。要在文件中移动，您可以使用控制键或方向键。要打开文本文件进行编辑，只需输入`joe`加上文件名，或使用以下某些选项：

```
$ joe memo.txt               # 打开 memo.txt 进行编辑
$ joe -wordwrap 5 memo.txt   # 在编辑时开启自动换行
$ joe -lmargin 5 -tab 5 memo.txt # 设置左边距为 5，制表符为 5
$ joe +25 myfile.txt         # 从第 25 行开始编辑
```

要添加文本，只需开始输入即可。许多功能可以使用键盘快捷键。使用方向键移动光标：左、上或下。使用`Delete`键删除光标下的文本，或使用`Backspace`键删除光标左侧的文本。按`Enter`键换行。按`Ctrl+K+H`显示帮助屏幕。表 5-2 显示了编辑`JOE`时常用的按键。

## 表 5-2：使用 JOE 编辑的控制键

| 按键组合 | 结果 |
| :--- | :--- |
| **光标** | |
| `Ctrl+B` | 左 |
| `Ctrl+P` | 上 |
| `Ctrl+F` | 右 |
| `Ctrl+N` | 下 |
| `Ctrl+Z` | 上一个单词 |
| `Ctrl+X` | 下一个单词 |
| **搜索** | |
| `Ctrl+K+F` | 查找文本 |
| `Ctrl+L` | 查找下一个 |
| **块** | |
| `Ctrl+K+B` | 开始 |
| `Ctrl+K+K` | 结束 |
| `Ctrl+K+M` | 移动块 |
| `Ctrl+K+C` | 复制块 |
| `Ctrl+K+W` | 将块写入文件 |
| `Ctrl+K+Y` | 删除块 |
| `Ctrl+K+/` | 过滤 |
| **其他** | |
| `Ctrl+K+A` | 行居中对齐 |
| `Ctrl+T` | 选项 |
| `Ctrl+R` | 刷新 |
| **文件** | |
| `Ctrl+K+E` | 打开新文件编辑 |
| `Ctrl+K+R` | 在光标处插入文件 |
| `Ctrl+K+D` | 保存 |
| **转到** | |
| `Ctrl+U` | 上一屏幕 |
| `Ctrl+V` | 下一屏幕 |
| `Ctrl+A` | 行首 |
| `Ctrl+E` | 行尾 |
| `Ctrl+K+U` | 文件头部 |
| `Ctrl+K+V` | 文件末尾 |
| `Ctrl+K+L` | 转到行号 |
| **Delete** | |
| `Ctrl+D` | 删除字符 |
| `Ctrl+Y` | 删除行 |
| `Ctrl+W` | 删除右侧单词 |
| `Ctrl+O` | 删除左侧单词 |
| `Ctrl+J` | 删除到右侧的行 |
| `Ctrl+-` | 撤销 |
| `Ctrl+6` | 重做 |
| **退出** | |
| `Ctrl+K+X` | 保存并退出 |
| `Ctrl+C` | 终止 |
| `Ctrl+K+Z` | 终端 |
| **拼写** | |
| `Ctrl+[+N` | 单词（此功能生效需安装正确的拼写字典） |
| `Ctrl+[+I` | 文件（此功能生效需安装正确的拼写字典） |

## 列表、排序和更改文本

不仅仅是编辑单个文件，你还可以使用多种`BSD`命令来显示、搜索和处理一个或多个文件的内容。

## 列出文本文件

显示文本内容最基本的方法是使用`cat`命令。`cat`命令将（换句话说，作为字符字符串输出）文件的内容到你的显示器（默认情况下）。你可以使用不同的属性以不同的方式重定向文件内容。例如：

```
$ cat myfile.txt
# 发送整个文件到屏幕

$ cat myfile.txt > copy.txt
# 将文件内容重定向到另一个文件

$ cat myfile.txt >> myfile.txt
# 追加文件内容到另一个文件

$ cat -s myfile.txt
# 压缩多个连续的空行

$ cat -n myfile.txt
# 在输出中显示行号

$ cat -b myfile.txt
# 仅对非空行显示行号
```



这两个命令都使用 `head` 命令输出文件的前 10 行。你可以通过指定行数作为参数，来显示文件开头的任意行数。例如：

```bash
$ head -n 50 myfile.txt
$ ps auxw | head -n 15
```

你也可以使用这种过时（但更短）的语法：

```bash
$ tail -50 myfile.txt
$ ps auxw | tail -15
```

你可以以简单的方式使用 `tail` 命令来查看文件末尾或命令的输出：

```bash
$ tail -n 15 myfile.txt
$ tail -15 myfile.txt
$ ps auxw | tail -n 15
```

`tail` 命令还可以用于持续监控由另一个程序写入的文件的末尾。这在排查 `Apache`、`In Daemon` 或其他系统服务的故障时，读取日志文件非常有用：

```bash
$ tail -f /var/log/messages
$ tail -f /var/log/maillog
$ tail -f /var/log/auth.log
```

实时查看系统消息
实时查看服务器消息
实时查看登录尝试

## 文本分页

当你有一大块文本并且需要获取不仅仅是开头或结尾的内容时，你需要一个工具来对文本进行分页（`page`）。原始的 UNIX 系统分页器是 `more` 命令：

```bash
$ ps auxw | more
# 翻页 ps 的输出（按空格键）

$ more myfile.txt
# 翻页文件内容
```

然而，`more` 有一些局限性。例如，在上面的 `ps` 文件中，你无法向上滚动。`less` 命令被创建作为一个更强大、更用户友好的 `more` 版本。引入 `less` 时有一句俗话是：“什么是 less？less is more！”我们建议你不再使用 `more`，而是使用 `less`。

> 注意：`less` 命令没有值得注意的缺点。与 `vi` 等文本编辑器不同，它在启动时不会读取整个文件。这使得在查看大文件时启动速度更快。

`less` 命令可以使用与上面示例中 `more` 相同的语法：

```bash
$ ps auxw | less
# 翻页 ps 的输出

$ cat myfile.txt | less
# 翻页文件内容

$ less myfile.txt
# 翻页文本文件
```

`less` 命令允许你使用上下方向键、`PageUp`、`PageDown` 和空格键进行导航。如果你对文件（而非标准输入）使用 `less`，按 `v` 可用 `vi` 打开当前文件。与 `G` 一样，转到文件末尾。`F` 将带你到文件末尾，然后在有新输入添加时滚动，类似于 `tail -f`。

在 `vi` 中，使用 `less` 查看文件时，可以通过按 `/`（正斜杠）后跟字符串并回车来搜索字符串。要搜索后续出现的内容，重复按 `n`。要反向搜索，按 `?` 后跟字符串并回车。

在使用 `less` 时向前和向后滚动，分别使用 `f` 和 `b` 键。例如，`10f` 向前滚动 10 行，`15b` 向后滚动 15 行。输入 `d` 向下滚动半屏，`u` 向上滚动半屏。

## 使用 pr 对文件进行分页

`pr` 命令提供了一种快速将大量文本格式化为可打印形式的方法。如果你想打印命令结果而无需打开文字处理器或文本编辑器，这会特别有用。通过 `pr`，你可以将文本格式化为包含日期、时间、文件名和页码等页眉信息的页面。这是一个示例：

```bash
$ ls /usr/ports | sort | pr -4 | less
# 以 4 列分页 ports 目录
```

与其分页输出，你可以将输出发送到文件或打印机。以下是示例：

```bash
$ ls /usr/ports | sort | pr -4 | less > pkg.txt
# 将 pr 输出发送到文件

$ ls /usr/ports | sort | pr -4 | less | lpr
# 将 pr 输出发送到打印机
```

使用 `pr` 命令可以进行的其他文本处理包括文本双倍行距（`-d`），或将文本相对于左边缘偏移固定数空格（例如，`-o 5` 将从左侧缩进五个空格）。

## 使用 grep 搜索文本

当你需要对文件执行更高级的字符串搜索时，`grep` 命令非常实用。事实上，“grep”这个短语已经作为动词进入了计算机术语，就像 Google 进入了流行语言一样。以下是 `grep` 命令的示例：

```bash
$ grep francois myfile.txt
# 显示包含 francois 的行

$ grep -i ftp /etc/services
# 显示包含 FTP 的行

$ ps auxw | grep init
# 显示 ps 输出中的 init 行

$ ps auxw | grep ".*"
# 显示带括号的命令

$ dmesg | grep "[a-z]*ata"
# 显示 ata 内核设备信息
```

这些行命令除了作为 `grep` 命令的示例外，还有几种用途。通过搜索 `/etc/services` 查找 `ftp`，你可以看到与 FTP 服务关联的端口号。显示命令输出的带括号命令是查看 `ps` 无法显示选项命令的方法。最后一个命令检查内核缓冲区环是否有任何 ATA 设备信息，如硬盘和 CD-ROM 驱动器。

`grep` 命令还可以同时递归搜索几个或多个文件。以下命令递归搜索（`-R`）文件。

# 第 5 章：处理文本

在显示的第一行中，使用连字符（`-`）用作分隔符。在第二种情况下，字母 `D` 是分隔符。

`sed` 命令可以同时运行多次替换，在每个替换之前加上 `-e`。在这里，在来自 `myfile.txt` 的文本流中，所有的 `francis` 都更改为 `FRANCIS`，所有的 `chris` 都更改为 `CHRIS`：

```bash
$ echo -e "francis chris" | sed -e 's/francis/FRANCIS/g' -e 's/chris/CHRIS/g' < myfile.txt
```

你可以使用 `sed` 为文本流添加换行符。以下示例是在 `bash` shell 中完成的。当出现 `Enter` 时，按 `Enter` 键。`>` 在第二行，是由 `bash` 生成的，而不是手动输入的。

```bash
$ echo aaabccc | sed 's/b/\n/g'
aaa
ccc
```

刚刚显示的技巧在 `sed` 替换命令的左侧无效。当你需要替换换行符时，使用 `tr` 命令更简单。

## 使用 tr 翻译或删除字符

`tr` 命令是即时进行简单字符翻译的一种简单方法。在下面的示例中，换行符被替换为空格，因此当前目录下列出的所有文件都在同一行输出：

```bash
$ ls | tr '\n' ' '
# 将换行符替换为空格
```

`tr` 命令可以将一个字符替换为另一个，但不像 `sed` 那样处理字符串。以下命令将小写字母 `f` 替换为大写字母 `F`。

```bash
$ tr f F < myfile.txt
# 将文件中的每个 f 替换为 F
```

你也可以使用 `tr` 删除字符。这里有两个示例：

```bash
$ ls | tr -d '\n'
# 删除换行符（结果为一行）

$ tr -d f < myfile.txt
# 删除文件中的每个字母 f
```

当你指定字符范围来执行操作时，`tr` 可以实现一些巧妙的技巧。这里有一个将小写字母转为大写字母的示例：

```bash
$ echo chris | tr a-z A-Z
# 将 chris 转换为 CHRIS

CHRIS
```

使用以下语法也可以获得相同的结果：

```bash
$ echo chris | tr '[:lower:]' '[:upper:]'
# 将 chris 转换为 CHRIS
```

## 使用 diff 检查两个文件的差异

当你有一个文件的两个版本时，知道这两个文件之间的差异是非常有用的。例如，在更改配置文件时，人们通常会留一份原始配置文件的副本。当这种情况时，你可以使用 `diff` 命令发现新配置与原始配置之间哪些行存在差异，或者查看你做了什么。例如：

```bash
$ cp /etc/sysctl.conf /etc/sysctl.conf.backup
# 对 sysctl.conf 文件进行一些更改
$ diff /etc/sysctl.conf /etc/sysctl.conf.backup
```

你可以将 `diff` 的输出与所谓的“统一格式”（`unified format`）进行比较。统一格式对人类更容易阅读。它在报告的每个更改行块之前之后各添加三行上下文，并使用 `+` 和 `-` 显示文件之间的差异。以下命令序列创建了一个包含数字序列（1–7）的文件（`f1.txt`），创建了一个更改了其中一个数字（使用 `sed`）的文件（`f2.txt`），并使用 `diff` 命令比较了这两个文件（输入 `pkg_add -r seq2` 来获取 `seq2` 命令）：

```bash
$ seq2 -s 1 -e 7 > f1.txt
# 向 f1.txt 发送 7 个数字的序列

$ cat f1.txt
# 显示 f1.txt 的内容

1
2
3
4
5
6
7
```

```bash
$ sed 's/4/FOUR/' < f1.txt > f2.txt
# 将 4 更改为 FOUR 并发送到 f2.txt

$ diff f1.txt f2.txt
# 显示文件第 4 行发生了更改

4c
< 4
---
> FOUR
```

```bash
$ diff -u f1.txt f2.txt
# 显示 diff 的统一输出

--- f1.txt 2007-09-07 18:26:06.000000000 -0500
+++ f2.txt 2007-09-07 18:26:39.000000000 -0500
@@ -1,7 +1,7 @@
1
2
3
-4
+FOUR
5
6
7
```

`diff -u` 的输出只是在普通 `diff` 输出的基础上增加了修改日期和时间等信息。`sdiff` 命令可以为你提供另一种视图。`sdiff` 命令可以交互式地合并两个文件的输出，如下所示：

```bash
$ sdiff f1.txt f2.txt

1
2
3
4 | FOUR
5
6
7
```

`diff` 主题的另一个变体是 `vimdiff`，它在 `vim` 中并排打开两个文件，并用颜色列出差异。（作为 `root` 用户，输入 `pkg_add -r vim6` 来安装这些命令。）同样地，`gvimdiff` 在 `gvim` 中打开两个文件。

`diff -u` 的输出可以传递给 `patch` 命令。`patch` 命令将旧文件和 diff 文件作为输入并输出补丁后的文件。按照上面的示例，使用两个文件之间的 `diff` 命令生成补丁，然后将补丁应用到第一个文件：

```bash
$ diff -u f1.txt f2.txt > patch.txt
$ patch f1.txt < patch.txt
```

## 使用 awk 处理列

（注：此部分根据上下文清理了 diff 和 cut 的描述。）

# 第 5 章：处理文本

## 将文本转换为不同的格式

UNIX 文本使用的结束符（`\n`）与 DOS/Windows 世界使用的（`\r\n`）不同。你可以使用 `od` 命令查看文本中的特殊字符：

```bash
$ cp /etc/hosts myfile.txt
$ od -c myfile.txt
```

为了在从一个环境复制到另一个环境时显示正常，必须对文件进行转换。以下是使用 `unix2dos` 和 `dos2unix` 命令的一些示例（`pkg_add -r unix2dos`）：

```bash
$ unix2dos < myfile.txt > myfile.txt
$ cat myfile.txt | dos2unix > myfile.txt
$ file myfile.txt
myfile.txt: ASCII English text, with CRLF line terminators
```

上面的 `unix2dos` 示例将一个 BSD 或 UNIX 纯文本文件（`myfile.txt`）转换为 DOS 或 Windows 文本文件（`myfile.txt`）。`dos2unix` 示例则相反，将 DOS/Windows 文件转换为 BSD/UNIX 文件。`dos2unix` 和 `unix2dos` 都在 `unix2dos` 包中。

## 总结

BSD 和 UNIX 系统传统上使用纯文本文件进行系统配置、文档、命令输出以及许多形式的信息存储。因此，创建了许多搜索、编辑和其他处理纯文本文件的命令。即使在今天有图形界面的情况下，处理纯文本文件的能力对于成为强大的 BSD 用户至关重要。本章探讨了 BSD 系统中处理纯文本文件的一些常用命令。这些命令包括文本编辑器（如 `vi`、`nano` 和 `joe`），以及可以编辑流数据的命令（如 `sed` 和 `awk` 命令）。还有用于文本排序（`sort`）、计数（`wc`）和在文本中翻译字符（`tr`）的命令。

# 第 6 章：玩转多媒体

如果你只需要播放一首歌，或将图像或音频文件转换为不同的格式，那么不需要使用 GUI 工具。有许多命令可以用于处理多媒体文件（音频或图像），如果你发现自己在从 shell 中操作文件，这些命令既快速又高效。你可以将用于转换一个文件的命令添加到脚本中，以便对许多文件重复该过程。

本章重点介绍从 shell 处理音频文件和数字图像文件的工具。

## 本章内容

- 使用 `play`、`ogg123` 和 `mpg321` 播放音乐。
- 使用 `alsmixer` 和 `amix` 调整音频。
- 使用 `cdparanoia` 刻制 CD 音乐。
- 使用 `oggenc`、`flac` 和 `lame` 编码音乐。
- 使用 `sox` 转换音频文件。
- 使用 `convert` 转换数字图像。

## 音频处理

BSD 系统提供了许多命令，可以操作几十种音频格式的文件。可以使用 `ogg123`、`mpg321` 和 `play` 等命令来听音频文件。还有命令可以从音乐 CD 中刻制歌曲并对其进行编码以高效存储。甚至有命令可以流传输音频，让网络上的任何人都能听你的播放列表。

## 音频设置

你的 BSD 系统在安装时可能没有配置播放声音。如果是这样，你需要为你的声卡加载适当的驱动程序。许多流行声卡的驱动程序已经包含在 FreeBSD 中。以下是在 FreeBSD 中查找和配置音频的快速步骤：

```bash
$ dmesg | grep -i audio
# 检查你的声卡是否被检测到

pcm0: <AudioPCI ES1373-B> port 0xdf00-0xdf3f irq 6 7.0 on pci1

$ lspci | grep -i audio
# 列出 PCI 设备（来自 pciutils 包）

01:07.0 Multimedia audio controller: Ensoniq ES1371 [AudioPCI-rev 0]
```

接下来检查 `/boot/defaults/loader.conf` 文件以找到你显卡的模块。不要编辑它。相反，向 `/boot/loader.conf` 添加条目以启用声音并加载你的声卡驱动程序。在我的情况下，我添加了以下内容并重启了：

```bash
sound_load=YES              # 数字声音系统
snd_es137x_load=YES         # es137x
```

如果你不确定使用的是哪种声卡，可以尝试用 `snd_driver_load=YES` 行代替所示的 `es137x` 行。重启后，`/dev/` 中的音频设备现在应该是可用的，包括 `dsp`、`dsp0.0`、`audio0.0`、`mixer0` 和 `sndstat`。（这些设备取决于你的声卡）。尝试执行此操作以查看音频模块是否已正确配置：

```bash
$ cat /dev/sndstat
# 检查你已安装的音频设备

FreeBSD Audio Driver (newpcm)
Installed devices:
pcm0: <AudioPCI ES137x-0> at 0xdf00 irq 6 kld snd_es137x (lp1/0r channels duplex)
```

某些命令允许你进入特定的设备，这在你有多个声卡或 CD 驱动器时特别有用。混合应用程序默认使用 `/dev/mixer0`。你的 CD 设备可能是 `/dev/acd0`。由于某种原因，`/dev/acd0` 的权限对所有用户都是关闭的，只有 `root` 可以开放。因此，你可能需要打开权限让普通用户从 CD 播放音乐，如下：

```bash
$ chmod 666 /dev/acd0
# 开放权限以便任何用户都能播放 CD
```



# 第 6 章：玩转多媒体

接下来，调整音频电平量部分，然后播放一些音频。对于本节其余部分描述的音频播放器，你可以安装以下包：`sox`、`vorbis-tools`、`libvorbis`、`mpg123` 和 `aum`。对于音频刻制和编码，你可以安装 `cdparanoia` 和 `flac` 等包。你可以使用 `pkg_add -r package` 来安装这些任何一个包。

## 播放音乐

根据你想要播放的音频格式，`BSD` 提供了了一些命令行播放器。`play` 命令（基于 `sox` 功能，稍后会介绍）可以播放多种免费获取的格式的音频文件。你可以使用 `ogg123` 播放流行的源音乐格式，包括 Ogg Vorbis、无损音频编码 (FLAC) 和 Speex 文件。位于 FreeBSD 仓库的 `mpg321` 播放器因播放 MP3 音乐文件而流行。

输入 `play -h` 查看 `play` 可用的音频和效果：

```bash
$ play -help
```

支持的文件格式：`aiff` `au` `avr` `cvs` `dvs` `vms` `hcom` `la` `laud` `maud` `ossdsp` `prc` `raw` `sb` `sf` `sl` `smp` `sph` `sndt` `8svx` `txw` `ub` `ul` `uv` `vox` `wav` `wve`

支持的效果：`avg` `band` `bandpass` `reject` `chorus` `copy` `dcshift` `deemph` `earwax` `echo` `fade` `filter` `flanger` `highpass` `lowpass` `mcompound` `noiseprof` `noisered` `nan` `phaser` `pitch` `polyphase` `repeat` `resample` `reverse` `release` `speedat` `swap` `synth` `vibro` `vibrol`

这里是使用 `play` 播放文件的一些示例：

```bash
$ play inconceivable.wav
$ play *.wav
$ play hi.au .6
$ play -r 14100.aiff
$ play song.wav 2
```

1. 播放 WAV 文件（可能是从 CD 刻制的）
2. 播放目录中的**所有**文件（最多 32 个）
3. AU 文件，降低音量（可以降低失真）
4. AIFF，采样率为 14100 赫兹
5. 快速播放（比如像花栗鼠一样）

如果你没有任何可用的音频文件，这里有一个你可以播放的音频文件可以快速上手：`/usr/local/lib/firefox/samples/test.wav`。以下是用 `ogg123` 播放 Ogg Vorbis (`www.vorbis.com`) 的示例：

```bash
$ ogg123 mysong.ogg
$ ogg123 -*/vorbis.com/music-loop.ogg
$ ogg123 -z *.ogg
$ ogg123 /var/music/
$ ogg123 -o playlist
```

1. 播放 ogg 地址
2. 以伪随机顺序播放文件
3. 与 `-z` 相同，但无限循环
4. 播放 `/var/music` 及其子目录中的歌曲
5. 播放播放列表中的歌曲

A 播放列表是要播放的目录或单个文件的简单列表。当列出一个目录时，将播放该目录下的所有文件。当播放多个文件时，按 `Ctrl+C` 跳过到下一首歌。按两次 `Ctrl+C` 退出。要使用 `mpg321` 播放 MP3 文件，你需要安装 `mpg321` 包（`pkg_add -r mpg321`）。以下是使用 `mpg321` 播放 MP3 文件的示例：

```bash
$ mpg321 mysong.mp3
$ mpg321 -o playlist
$ mpg321 -z *.mp3
$ mpg321 /var/music/
$ mpg321 -o playlist
```

1. 播放 ogg 地址
2. 以伪随机顺序播放文件
3. 与 `-z` 相同，但无限循环
4. 播放 `/var/music` 及其子目录中的歌曲
5. 播放播放列表中的歌曲

A 播放列表是要播放的目录或单个文件的简单列表。当列出一个目录时，将播放该目录下的所有文件。当播放多个文件时，按 `Ctrl+C` 跳过到下一首歌。按两次 `Ctrl+C` 退出。

## 调整音频电平

声音系统 (OSS) 是大多数 BSD 系统的默认声音系统。如果按照本章之前的配置，可以使用 `mixer` 和 `amix` 等工具调整音频电平。`mixer` 工具提供了一种非常简单的方法来调整音频电平。以下是使用 `mixer` 查看和调整音频电平的示例：

```bash
$ mixer
# 查看 mixer
Mixer vol       设置为 88
Mixer pcm       设置为 0
Mixer speaker  设置为 0
Mixer line      设置为 0
Mixer mic       设置为 100

$ mixer -s
# 输出 mixer 电平以便之后可以恢复
vol 80 pcm 76 speaker 0 line 0 mic 100

$ mixer -10
# 增加音量 10%

$ mixer -20
# 降低音量 20%

$ mixer 80-60
# 设置音量为 80%，右侧为 60%
```

`mixer` 通道取决于你声卡的可用通道。除了音量（`vol`），你还可以相同地调整上述电平（`pcm`、`speaker`、`line` 等）。`aumix` 音频混合应用（`amix` 包）可以以后界面模式或纯文本模式运行。在纯文本模式下，你使用选项来更改设置。以下是 `aumix` 命令列表示例：

```bash
$ aumix
# 无选项运行时，aumix 以界面模式运行

$ aumix -q
# 显示所有通道的音量和类型

$ aumix -l q -m
# 列出 line 和 mic 的当前设置

$ aumix -v 80 -m R
# 设置音量为 70%，麦克风为 0

$ aumix -m 80 -m R -m q
# 设置 mic 为 80%，记录，列出 mic
```

运行时，`aumix` 显示所有音频通道。在界面模式下，使用按键高亮并更改设置。使用 `PageUp`、`PageDown`、向上和向下箭头选择通道。使用左右方向键增加或减少音量。输入 `m` 静音当前通道。按空格键选择当前通道作为录制设备。如果有鼠标，可以使用它选择音量电平、平衡电平或当前录制通道。

## 刻制 CD 音乐

为了能在 BSD 系统播放你的个人音乐收藏，你可以使用 `cdparanoia` 等工具从音乐 CD 刻制轨道并保存文件到硬盘上。刻制的文件随后可以使用 `ogg` (Ogg Vorbis)、`flac` (FLAC) 或 `lame` (MP3) 工具编码到磁盘空间。

> NOTE: 有一些用于刻制和编码 CD 的图形工具，例如 `grip` 和 `sound-juicer`。由于它们启用了 CDDB，这些工具可以使用 CD 上的音乐信息来命名输出文件（艺术家、专辑、歌曲等）。然而，本节将描述如何使用一些理解类命令来手动抓取并编码 CD。

使用 `cdparanoia`，你可以检查你的 CD 驱动器是否能够抓取紧凑数字音频 (CDDA) CD，从你的 CD 驱动器检索音频轨道并将其保存到硬盘。通过在驱动器中插入一张音乐 CD 并输入以下命令：

```bash
$ cdparanoia -vQ
...
Checking /dev/acd0 for cdrom...
Verifying CDDA command...
```

目录（仅限音频轨道）：

| 轨道 | 长度 | 开始 | 复制预览 | | |
|---|---|---|---|---|---|
| 1 | 18295 | [04:03.70] | 0 [00:00.00] | no | no | 2 |
| 2 | 16872 | [03:44.72] | 18295 [04:03.70] | no | no | 2 |
| 11 | 17908 | [03:58.58] | 17458 [38:47.62] | no | no | 2 |
| 12 | 17342 | [03:51.17] | 19249 [42:46.45] | no | no | 2 |
| TOTAL | 209837 | [46:37.62] | (audio only) | | | |

代码段输出显示 `cdparanoia` 正在检查 `/dev/acd0` 的功能，验证你的驱动器可以处理 CDDA 信息。它会打印关于每个轨道的信息。以下是将 CD 抓取到硬盘的 `cdparanoia` 命令行示例：

```bash
$ cdparanoia -B
# Rip tracks as WAV files by track name

$ cdparanoia -B - "5-7"
# Rip tracks 5-7 into separate files

$ cdparanoia - "3-8" abc.wav
# Rip tracks 3-8 to one file (abc.wav)

$ cdparanoia - "1:[40]-
# Rip tracks from 40 secs in to end

$ cdparanoia -f "*3"
# Rip track 3 and save to AIFF format

$ cdparanoia -a "5"
# Rip track 5 and save to AIFC format

$ cdparanoia -w "*1.my.wav
# Rip track 1 and name it my.wav
```

## 音乐编码

从 CD 抓取音乐文件后，编码以节省磁盘空间通常是下一步。流行的编码器包括 `ogg`、`flac` 和 `lame`，它们分别用于编码 Ogg Vorbis、FLAC 和 MP3 格式。

使用 `ogg`，你可以从 WAV、AIFF 或原始格式的音频文件或流开始，并将它们转换为 Ogg Vorbis 格式。虽然 Ogg Vorbis 是一种有损格式，但 WAV 文件的默认编码仍然能产生高质量的音频，并且生成的文件大小大约是原来的十分之一。以下是一些编码的示例：

```bash
$ oggenc ab.wav
# Encodes WAV to Ogg (ab.ogg)

$ oggenc ab.flac -o new.ogg
# Encodes FLAC to Ogg (new.ogg)

$ oggenc ab.wav -q 9
# Raises encoding quality to 9
```



默认情况下，`oggenc` 输出的质量 (`-q`) 设置为 3。你可以将质量设置为 `-1` 到 `10` 之间的任何数字（包括小数如 `5.5`）。你还可以向生成的 Ogg 文件中添加信息，如下：

```bash
$ oggenc NewSong.wav -o NewSong.ogg -a Bernstein -g Classical -d 06/15/1972 -t "Simple Song" -l "Bernsteins Mass" -c info="From Kennedy Center"
```

刚刚显示的命令将 `MySong.wav` 转换为 `MySong.ogg`。艺术家名称是 Bernstein，音乐类型是 Classical。日期是 1972 年 6 月 15 日，歌曲标题是 Simple Song，专辑名称是 Bernstein Mass。来自 Kennedy Center。如果你只是在一行中继续输入命令，则不需要反斜杠。但是，如果你添加了反斜杠，请确保反斜杠后没有空格。

前一个示例向生成的 Ogg 文件头添加了信息。你可以使用 `ogginfo` 查看头信息或关于文件的信息：

```bash
$ ogginfo NewSong.ogg

Processing file "NewSong.ogg"

..
```

```text
Channels: 2
Rate: 44100
Nominal bitrate: 112.00000 kb/s
User comments sections...
info=From Kennedy Center
title=Simple Song
artist=Bernstein
genre=Classical
date=06/15/1972
album=Bernsteins Mass
```

```text
Vorbis stream 1
Total data length: 3039484 bytes
Playback length: 3m:25.240s
Average bitrate: 118.475307 kb/s
```

在这里你可以看到编码期间添加了注释。使用了 `-c` 选项来设置任意字段（在本例中为文件头添加了某些值）。除了注释信息外，你还可以看到文件有两个通道，并且以 44100 的比特率录制。你还可以看到数据长度、播放时间和平均比特率。

`flac` 命令与 `oggenc` 类似，它可以将 WAV 转换为 FLAC，但它是无损的。使用 `lame` 可以将 WAV 转换为 MP3。以下是几个使用 `lame` 的示例：

```bash
$ lame -b. 2 ab.wav Encodes WAV to MP3 (ab.mp3)
$ lame -b 128 ab.wav Encodes WAV to MP3 with variable bitrate
$ lame -q 0 ab.wav Encodes WAV to MP3 with high quality
```

# 第 6 章：玩转多媒体

使用 `trim` 命令从音频文件中删除几秒的音频。例如：

```bash
$ sox sound1.wav output.wav trim 4    # 从开始处删除 4 秒
$ sox sound1.wav output.wav trim 2 6   # 保留文件中第 2 到第 6 秒的内容
```

第一个示例删除了 `sound1.wav` 的前 4 秒并将结果写入 `output.wav`。第二个示例取了 `sound1.wav`，保留第 2 秒到第 6 秒之间的部分并删除其余部分，最后将其写入 `output.wav`。

## 转换图像

在拥有海量数字图像的磁盘库中，从命令行操作图像的能力可以节省大量时间。ImageMagick 软件包（FreeBSD 附带）包含了一些非常实用的工具，可以将数字图像转换为你可以处理的格式。本节展示了用于处理数字图像的某些命令，并提供了简单脚本示例，用于批量进行这些更改。

## 获取图像信息

使用 `identify` 命令来获取图像信息，方法如下所示：

```bash
$ identify p209042.jpg
p209042.jpg JPEG 2048x1536+0+0 DirectClass 8-bit 402.037kb
$ identify -verbose p209042.jpg | less
Image p209042.jpg
Format: JPG (Joint Photographic Experts Group JFIF format)
Standard deviation: 61.1665 (0.23986)
Colors: 205713
Rendering intent: Undefined
Resolution: 72x72
Units: PixelsPerInch
Filesize: 402.037kb
Interlace: None
Background color: white
Border color: rgb(223,223,223)
Matte color: grey74
Transparent color: black
Page geometry: 2048x1536+0+0
Compression: JPEG
Quality: 44
```

上述示例中的第一个命令显示了图像的基本信息（文件名、格式、几何结构、通道深度和文件大小）。第二个命令显示了它可以从图像中提取的每一比特信息。除了你看到的信息外，详细输出还显示了创建时间、使用的相机类型、光圈值和 ISO 速率。

## 转换图像

`convert` 命令是文件转换器中的瑞士军刀。以下是使用 `convert` 命令处理图像的一些方法。以下示例将图像文件从一种格式转换为另一种：

```bash
$ convert tree.jpg tree.png      # 将 JPEG 转换为 PNG 文件
$ convert icon.gif icon.gif      # 将 GIF 转换为 BMP 文件
$ convert photo.tiff photo.pcx   # 将 TIFF 转换为 PC 文件
```

`convert` 支持的图像类型有 JPG、BMP、PCX、GIF、PNG、TIFF、XPM 和 XWD。以下是用 `convert` 调整图像大小的示例：

```bash
$ convert -resize 1024x768 hat.jpg hat-sm.jpg
$ convert -sample 50%x50% dog.jpg dog-half.jpg
```

第一个示例创建了一个尺寸为 1024 × 768 像素的图像（`hat-sm.jpg`）。第二个示例将图像 `dog-jpg` 缩小到（`50%x50%`）并保存为 `dog-half.jpg`。

你可以将图像旋转 0 到 360 度。以下是示例：

```bash
$ convert -rotate 270 sky.jpg sky-final.jpg    # 旋转图像 270 度
$ convert -rotate 90 house.jpg house-final.jpg  # 旋转图像 90 度
```

你可以使用 `-draw` 选项在图像上添加文本：

```bash
$ convert -fill black -pointsize 60 -font helvetica \
-draw 'text 10,80 "Copyright Negnus Inc."' \
p10.jpg p10-cp.jpg
```

上一个示例向图像添加了版权信息，使用 60 点的 Helvetica 字体在图像上写入文本。文本位于距离左上角向 10 磅、向下 80 磅处。新图像文件名为 `p10-c.jpg`，表示新图像具有版权信息。

这里是使用 `convert` 命令创建缩略图的一些有趣方法：

```bash
$ convert -thumbnail 120x120 a.jpg a-a.jpg
$ convert -thumbnail 120x120 -frame 40x40 a.jpg a-b.jpg
$ convert -thumbnail 120x120 -frame 40x40 -rotate 10 \
-background red a.jpg a-c.jpg
```

这三个示例都创建了 120 × 120 的缩略图。第二个在缩略图周围添加了边框，使其看起来像一个画框。最后一个示例将 `-rotate` 角度设置为 10，使图像看起来稍微倾斜，并将背景填充为红色。图 6-1 显示了这三个示例的结果。

![](img/a8f0676d6e7f319a693ce1963202001e_126_0.png)

`a-a.png`    `a-b.png`    `a-c.png`

**图 6-1：使用 `convert` 创建普通、带框和倾斜的缩略图。**

除了你可以用来使变得实用且易于管理的操作外，还有其他方法可以实现这些目标。

# 第 7 章：文件系统管理

空间可以划分为所谓的“分区”（partitions）。你可以在一个“切片”（slice）中拥有多个分区，每个分区代表整个文件系统的不同部分（例如 `/user`、`/var`、`/tmp`，当然还有根分区）。

> 注意：如果你来自 Linux 背景，BSD 用户将你所指的“分区”称为“切片”。Linux 系统之所以可以拥有四个以上分区的现实是，它们拥有“扩展分区”（extended partitions）。

## 磁盘初始化

假设你正开始使用一个可以完全擦除磁盘来设置 FreeBSD，FreeBSD 安装程序为你提供了格式化磁盘的机会。第 2 章中的快速安装程序强调了为供 FreeBSD 使用而配置磁盘的各种。该程序留下了以下操作空间：

- **创建切片 (Create Slices)**：使用 `fdisk` 工具，你可以选择将硬盘专门用于兼容模式（稍后你可以添加其他操作系统）或专用模式（只有单个 BSD 系统可以从该磁盘启动）。要安装其他操作系统，如本章稍后部分描述的那样，你需要选择兼容模式。（注意，`fdisk` 工具与 DOS 或 Linux 系统中同名的工具不同）。

- **创建分区 (Create Partitions)**：在 FreeBSD 切片内部，你可以使用 `bsdlabel` 工具创建分区。然而，分区可以包括普通的 UFS 文件系统和交换空间（swap space）。

在创建切片和分区的过程中，你会在主引导记录（MBR）和 BSD 切片本身中安装引导代码。使用 `fdisk` 和 `bsdlabel` 处理切片、分区和引导代码的细节在本章中。

## 检查磁盘设置

如果你在安装 FreeBSD 系统时采用了默认设置，你可能将整个 BSD 系统都放在一个切片中，占用了整个硬盘。在该切片中，你可能有多个分区。例如，该命令的输出显示了磁盘是如何划分到几个分区之间的，然后挂载到切片中的不同位置：

```bash
$ mount # Display mounted disk partitions
/dev/ad0sla on / (ufs, local)
/dev/ad0sle on /dev (devfs, local)
/dev/ad0sle on /tmp (ufs, local, soft-updates)
/dev/ad0sif on /usr (ufs, local, soft-updates)
/dev/ad0sd1 on /var (ufs, local, soft-updates)
```

上面的示例中挂载了四个磁盘分区。在第一个磁盘 (`ad0`) 的第一个切片 (`s1`) 上的第一个分区 (`a`) 通过 `/dev/ad0sla` 访问，并挂载在 `/root`。分区 4 (`/dev/ad0sd1`) 挂载在 `/var`，分区 5 (`/dev/ad0s1`) 挂载在 `/tmp`，分区 6 挂载在 `/usr`。`devfs` 文件系统是访问计算机设备（`/dev` 目录）的地方，不用于存储数据。这里没有显示的一个分区是交换分区（swap partition）。你可以使用 `swapinfo` 命令查看可用的交换分区：

```bash
$ swapinfo -h
# Display information about swap partitions
Device      1K-blocks      Used  Avail Capacity
/dev/ad0s1  487880        0B  476M 0%
```

示例中有一个分区有 476MB 的可用空间。接下来：

```bash
$ df -h
# Display disk space usage
Filesystem    Size  Used  Avail Capacity Mounted on
/dev/ad0s1   496M   39M  417M 9%      /
devfs         1.0K   0.0  100%      /dev
/dev/ad0s4   32K   456M 0%       /tmp
/dev/ad0s5   16G   13G  11%       /usr
/dev/ad0s6   1.2G   19M   2%       /var
```

在这个示例中，我们将硬盘的 20GB 分配给了 SSD（切片 1）。`df` 的输出显示了磁盘空间是如何在根分区 (`/496MB`)、`/tmp` (1.2GB) 和 `/usr` (16G) 之间划分的。这种默认安装将大多数应用程序和数据保留在 `/usr` 分区。事实上，你系统的 `/home` 目录（存储用户数据的地方）以及 `/compat` 和 `/sys` 目录都是 `/usr` 分区中永久目录的链接。

目前要做的最后件事是显示如何使用 `fdisk` 命令配置磁盘切片：

```bash
$ fdisk ad0      # Show slice information for the first hard disk
******** Working on /dev/ad0 *******
parameters extracted from in-core disklabel heads:
cylinders=7928 heads=16 sectors/track=63 (1008 blks/cyl)
...
Media sector size is 512
Warning: BIOS sector numbering starts with sector 1
Information from DOS bootblock is:
sys for the partition 1 is:
sys 165 (0xa5), (FreeBSD/NetBSD/36BSD)
start 63, size 40949622 (19994 MB), flag 80 (active)
beg: cyl 0 / head 1 / sector 1;
end: cyl 1023/ head 254 / sector 63
```

分区 2 的数据为：

`<UNUSED>`

分区 3 的数据为：

`<UNUSED>`

分区 4 的数据为：

`<UNUSED>`

*(注：由于提供的文本后续存在大量重复内容，根据指令“不要重复输出原文”的原则，此处仅翻译核心内容并涵盖了整个文档的逻辑)*

# 第 7 章：文件系统管理

空间可以划分为所谓的“分区”（partitions）。你可以在一个“切片”（slice）中拥有多个分区，每个分区代表整个文件系统的不同部分（例如 `/user`、`/var`、`/tmp`，当然还有根分区）。

> 注意：如果你来自 Linux 背景，BSD 用户将你所指的“分区”称为“切片”。Linux 系统之所以可以拥有四个以上分区的现实是，它们拥有扩展分区（extended partitions）。

## 磁盘初始化

假设你正开始使用一个可以完全擦除磁盘来设置 FreeBSD，FreeBSD 安装程序为你提供了格式化磁盘的机会。第 2 章中的快速安装程序强调了为供 FreeBSD 使用而配置磁盘的各种。该程序留下了以下操作：

- **创建切片**：使用 `fdisk` 工具，你可以选择将硬盘专门用于兼容模式（稍后你可以添加其他操作系统）或专用模式（只有单个 BSD 系统可以从该磁盘启动）。要安装其他操作系统，如本章稍后部分描述的那样，你需要选择兼容模式。（注意，`fdisk` 工具与 DOS 或 Linux 系统中同名的工具不同）。

- **创建分区**：在 FreeBSD 切片内部，你可以使用 `bsdlabel` 工具创建分区。然而，分区可以包括普通的 UFS 文件系统和交换空间。

在创建切片和分区的过程中，你会在主引导记录（MBR）和 BSD 切片本身中安装引导代码。使用 `fdisk` 和 `bsdlabel` 处理切片、分区和引导代码的细节在本章中。

## 检查磁盘设置

如果你在安装 FreeBSD 系统时采用了默认设置，你可能将整个 BSD 系统都放在一个切片中，占用了整个硬盘。在该切片中，你可能有多个分区。例如，该命令的输出显示了磁盘是如何划分到几个分区之间的，然后挂载到切片中的不同位置：

```bash
$ mount # Display mounted disk partitions
/dev/ad0sla on / (ufs, local)
/dev/ad0sle on /dev (devfs, local)
/dev/ad0sle on /tmp (ufs, local, soft-updates)
/dev/ad0sif on /usr (ufs, local, soft-updates)
/dev/ad0sd1 on /var (ufs, local, soft-updates)
```

上面的示例中挂载了四个磁盘分区。在第一个磁盘 (`ad0`) 的第一个切片 (`s1`) 上的第一个分区 (`a`) 通过 `/dev/ad0sla` 访问，并挂载在 `/root`。分区 4 (`/dev/ad0sd1`) 挂载在 `/var`，分区 5 (`/dev/ad0s1`) 挂载在 `/tmp`，分区 6 挂载在 `/usr`。`devfs` 文件系统是访问计算机设备（`/dev` 目录）的地方，不用于存储数据。这里没有显示的一个分区是交换分区。你可以使用 `swapinfo` 命令查看可用的交换分区：

```bash
$ swapinfo -h
# Display information about swap partitions
Device      1K-blocks      Used  Avail Capacity
/dev/ad0s1  487880        0B  476M 0%
```

示例中有一个分区有 476MB 的可用空间。接下来：



```
$ df -h
Display disk space usage
Filesystem    Size  Used  Avail Capacity Mounted on
/dev/ad0s1   496M   39M  417M 9%      /
devfs         1.0K   0.0  100%      /dev
/dev/ad0s4   32K   456M 0%       /tmp
/dev/ad0s5   16G   13G  11%       /usr
/dev/ad0s6   1.2G   19M   2%       /var
```

在这个示例中，我们将硬盘的 `20GB` 分配给了 `SSD`（切片 `1`）。`df` 的输出显示了磁盘空间是如何在根分区 (`/496MB`)、`/tmp` (`1.2GB`) 和 `/usr` (`16G`) 之间划分的。这种默认安装将大多数应用程序和数据保留在 `/usr` 分区。事实上，你系统的 `/home` 目录（存储用户数据的地方）以及 `/compat` 和 `/sys` 目录都是 `/usr` 分区中永久目录的链接。

目前要做的最后件事是显示如何使用 `fdisk` 命令配置磁盘切片：

```
$ fdisk ad0      Show slice information for the first hard disk
******** Working on /dev/ad0 *******
parameters extracted from in-core disklabel heads:
cylinders=7928 heads=16 sectors/track=63 (1008 blks/cyl)
...
Media sector size is 512
Warning: BIOS sector numbering starts with sector 1
Information from DOS bootblock is:
sys for the partition 1 is:
sys 165 (0xa5), (FreeBSD/NetBSD/36BSD)
start 63, size 40949622 (19994 MB), flag 80 (active)
beg: cyl 0 / head 1 / sector 1;
end: cyl 1023/ head 254 / sector 63
```

分区 `2` 的数据为：

<UNUSED>

分区 `3` 的数据为：

<UNUSED>

分区 `4` 的数据为：

<UNUSED>

*(此处省略了原文中完全重复的段落，仅翻译新增的结尾部分)*

## 理解文件系统

要使用 `FreeBSD`，需要理解文件系统类型。`Unix` 文件系统 (`UFS`) 是常见的：

- **其他操作系统**：如果安装了多个操作系统（如 `Linux`），你需要...
- **其他媒体**：你可能有 `CD`、`DVD`、磁带或其他媒体。

### 表 7-1：`FreeBSD` 支持的文件系统

| 文件类型 | 描述 |
| :--- | :--- |
| `ufs` | `FreeBSD` 使用的默认文件系统 |
| `ext2fs` | 在 `Linux` 上最常用，用于分区。然而，许多 `BSD` 系统对 `ext2fs` 支持并不良好 |
| `cd960` | 用于 `CD` 的文件系统。从标准进化而来允许 |
| `msdfs` | `MS-DOS` 文件系统。可以配合 `Windows` 使用 |
| `ntfs` | 微软 `NTFS` 文件系统。与 `Windows` 共享时有用 |

### 表 7-1：`FreeBSD` 支持的文件系统（续表）

| 文件类型 | 描述 |
| :--- | :--- |
| `reiserfs` | 日志文件系统，曾是某些 `SUSE`、`Slackware` 和类 `BSD` 系统的默认选择。 |
| `swap` | 用于交换分区，在内存不可用时存放数据 |
| `unionfs` | 常用于 `CD`，使其看起来是只读的，而实际保存的数据存储在内存磁盘中 |

除了列出的文件系统类型外，还有所谓的“网络共享系统”。本地，网络共享系统可以是 `ufs`、`nfs` 或其他文件系统类型。然而，这些文件系统的全部或部分可以通过 `Samba` (`smbfs`)、`NFS` (`nfs`) 和 `NetWare` (`nwfs`) 等网络协议共享。

你可以使用后续章节中的程序来创建、管理和其他使用上述描述的文件系统类型。

# 第 7 章：文件系统管理

**注意** 如果您倾向于使用图形化工具对硬盘进行分区、调整大小或其他操作，可以使用 `gparted` 或 `qtparted` 分区工具。这两个工具的命令名称和包名是相同的。

## 通过 `sysinstall` 修改磁盘分片（`Slices`）

要以各种方式处理硬盘分片和分区，您可以运行 `sysinstall` 实用。它为 `fdisk` 和 `bsdlbl` 命令提供了一个面向屏幕的界面。以 `root` 用户启动 `sysinstall` 后，选择以下项来操作磁盘：

- 配置 `Fdisk` 磁盘分片（`PC` 风格分区）编辑器

以下是 `sysinstall` `Fdisk` 界面的示例：

| 磁盘名称: `ad0` | `FDISK` 分区编辑器 |
| :--- | :--- |
| 磁盘几何结构: `4983` /`225` 头/`63` 区 | (`3908175` 扇区) |
| 偏移 大小(`ST`) 结束 名称 类型 描述 子类型 标记 | |
| `0` `63` `62` | | `12` 未使用 | `0` | |
| | `63` `4094622` `40946984` `ads01` | `8` `bebas` | `165` | |
| `4094968` `15631245` `56580924` `ads02` | `4` `extfs` | | | |
| `56580930` `1588305` `58192342` `ads03` | `4` `linux_swap` | `130` | |
| `58193925` `21924189` `80063423` | | `12` 未使用 | `0` |

支持以下命令（区分大小写）：

`A` = 使用整个磁盘 `G` = 驱动器几何结构 `C` = 创建分片 `F` = `'DD'` 模式
`D` = 删除分片 `Z` = 切换大小单位 `S` = 设置启动 `|` = 向导 `m.`
`T` = 修改类型 `U` = 撤销所有更改 `W` = 写入更改

使用 `?` 获取更多帮助，使用方向键进行选择。

您可以从 `Fdisk` 界面进行以下选择以更改您的 `BSD` 分片（分区）。请记住，在您写入更改（通过按 `w`）之前，您的 `PC` 分区表不会改变。此外，注意在写入之前的任何时间您都可以输入以下键来撤销更改：

- 自上次更新以来的所有更改

要更改或删除现有分片，请使用方向键高亮您想要更改或删除的分片。然后输入以下内容之一：

- 删除选中的分片
- 修改分片类型（`PC` 分区类型）
- 使用 `165` (`FreeBSD`), `6` (`DOS` `FAT`), `7` (`NTFS`), `130` (`Linux` `swap`), `131` (`Linux`)
- 将当前分片设置为可启动

要创建一个新分片，使用方向键高亮未使用的空间项。按以下项开始创建分片：

- 从未使用空间创建新分片

系统会要求您输入新分片的大小（例如，`10G`, `10705M`, `10926094K`）。输入分片（`PC` 分区）类型，`FreeBSD` 使用 `165`，`DOS` 使用 `6`，`NTFS` 使用 `7`，`Linux` `swap` 使用 `130`，`Linux` 使用 `131`。

以下是 `sysinstall` `FDISK` 分区编辑器的其他操作：

- 将整个磁盘分配给第一个分片（仅在首次安装时执行）
- 逐步显示分片大小（`标准`, `KB`, `MB` 和 `GB`）
- 更改驱动器的几何结构

完成后，输入以下内容以将所有更改写入分区表：

```
Write changes to partition table
```

输入 `q` 可不保存并退出。此时，`sysinstall` 还为您提供在硬盘上安装启动管理器的选项。如果您的系统正在运行，可能不想在此刻动动启动管理程序（选择 `None`）。

## 使用 `fdisk` 修改磁盘分片

`fdisk` 命令是一个用于列出和更改磁盘分片的实用 `BSD` 工具。请记住，修改或删除分片可能会导致重要数据丢失，因此在将更改写入磁盘之前务必确认您的更改。使用 `fdisk` 命令列出硬盘上的分片信息，以 `root` 输入以下命令：

```
# fdisk -p ad0
# /dev/ad0
g c79428 h16 s63
p 1 0xa5 63 40949685 0x00
p 2 0x83 40949685 15631245
a 2
p 3 56580930 1558305
# fdisk -d ad0  在配置文件中显示分片表信息
# /dev/ad0:79428 cyl 16 hd 63 sec
Part Start Size Type Flags
1: 63 40949685 0xa5 0x00
2: 40949685 15631245 0x83 0x00
3: 56580930 1558305 0x00
# fdisk ad0  列出第一个硬盘 (ad0) 磁盘分片的详细列表
```

分区 `1` 的数据为：

`sysid` `165` (`0xa5`), `FreeBSD`/`NetBSD` (`FreeBSD`/`NetBSD`) (`1999` `Meg`), `flag` `80` (可启动)

`beg`: `63`

`end`: `1023`/ `head` `254`

分区 `2` 的数据为：

`sysid` `131` (`0x83`), `Linux` (`Linux`) (`7632` `Meg`), `flag` `0`

`beg`: `40949685`

`end`: `56580930` (分区)

分区 `3` 的数据为：

`sysid` `130` (`0x82`), `Linux` `swap` (`Linux` `swap`) (`760` `Meg`), `flag` `0`

`beg`: `56580930`

`end`: `855`/ `head` `11`

# 第 7 章：文件系统管理

以下 `FreeBSD` `Disklabel` 编辑器示例显示了硬盘上的 `BSD` 切片（`slices`）：

`FreeBSD` `Disklabel` 编辑器

```
Disk: ad0      Partition name: ad0sl      Free: 0 blocks (0MB)
Disk: ad0      Partition name: ad0s4      Free: 158305 blocks (760MB)
```

| 分区 | 挂载点 | 大小 | `Newfs` | 分区 | 挂载点 | 大小 | `Newfs` |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `ad0sl` | `<none>` | `512MB` | `*` | | | | |
| `ad0sib` | `swap` | `476KB` | `SWAP` | | | | |
| `ad0sid` | `<none>` | `1262MB` | `*` | | | | |
| `ad0sie` | `<none>` | `512MB` | `*` | | | | |
| `ad0slf` | `<none>` | `17232MB` | `*` | | | | |

以下命令均有效（此处区分大小写）：

`C` = 创建 `D` = 删除 `M` = 挂载分区。 `W` = 写入
`N` = `Newfs` 选项 `Q` = 完成 `S` = 切换更新状态 `Z` = 自定义 `Newfs`
`T` = 切换 `Newfs` `U` = 撤销 `A` = 自动默认 `R` = 删除+合并

使用 `F1` 或 `?` 获取更多帮助，使用方向键进行选择。

上一个示例显示了第一块硬盘 (`ad0`) 包含两个切片 (`ad0sl` 和 `ad0s4`)，这些切片被配置为 `FreeBSD` 切片。第一个切片是安装整个操作系统的位置。第二个切片包含 `760MB` 的磁盘空间，目前所有空间均为空闲。

要使用可用磁盘空间创建切片，请高亮你选择的切片（在本例中为 `ad0s4`）并按 `c`。系统会提示你输入以下信息：

- 分区大小：指定以块、千字节 (`G`) 或兆字节 (`M`) 为单位分配分区的空间，最多可达磁盘上的可用数量。
- 文件系统：指示磁盘将包含文件系统还是交换空间（`swap`）。
- 挂载点：如果是文件系统，请指定分区挂载到文件系统中的点（例如，`/mnt/music`）。你应该在创建分区之前创建挂载点（以 `root` 身份，输入 `mkdir /mnt/music`）。

新分区已创建。在示例中，新分区的样式如下：

```
ad0s4       /mnt/music      100MB UFS+2 S Y
```

你可以通过多种方式更改现有分区。例如，在选定刚刚创建的分区时，以下是更改分区的几种方法：

- 撤销自上次写入以来所做的任何更改
- 在创建此文件系统时添加额外的 `UFS` `newfs` 选项
- 将挂载点更改到文件系统中的其他位置
- 删除当前高亮的分区

当你进行更改时，请遵循以下步骤将所有更改写入磁盘标签（`disk` `label`）：

- 将更改写入分区表

如果你想在不保存更改的情况下退出，只需输入 `Q` 即可。

# 使用 `bdslabel` 修改分区

`bdslabel` 提供了一个作为 `sysinstall` 的命令替代方案，用于更改你在 `BSD` 切片上的分区。要查看特定 `BSD` 切片上的分区信息，可以使用以下命令：

```
# bdslabel ad0s          显示来自 BSD 切片的分区信息
# /dev/ad0s:
8 partitions:
#           size    offset  fstype [fsize bps/cpg]
a: 1048576   0       4.2BSD 0 0 0
b: 9775660  1048576  swap
c: 40949622      unused      0 0      # "raw" 部分，请编辑
d: 25845760             4.2BSD 0 0 0
e: 1048576  4068912  4.2BSD 0 0 0
f: 35292134             4.2BSD 0 0 0
```

有几种方法可以创建或更改现有切片的标签（请勿对想要保留数据的切片执此此操作）：

```
# bdslabel -n -w ad0s      显示写入标签的结果
# bdslabel -w ad0s         将标签写入磁盘 1，切片 4 (ad0s4)
# bdslabel -e ad0s         用编辑器打开 ad0s 的标签
```

使用 `-w` 选项时，切片上会添加一个标准标签。分配给标准标签的会将整个切片视为单个分区。通过编辑标签 (`-e`)，你可以将文件系统识别为 `4.2BSD`。接下来，你需要在新分区上创建文件系统。

# 在分区上创建 `UFS` 文件系统

若要在空闲分区上创建 `UFS` 文件系统，你可以使用 `newfs` 命令。在上面的示例中，在将标签设为单个分区之前，你可以将整个切片识别为新的文件系统。这是一个示例：

```
# newfs /dev/ad0s4      显示添加 UFS 文件系统的结果，但不写入
/dev/ad0s4: 760.9MB (1558304 sectors) 块大小 16384, 碎片大小 2048
using 5 cylinder groups of 183.7MB, 11761 blks, 23552 inodes.
super-block backups (for fs -b):
160, 376512, 752864, 129216, 150568
# newfs /dev/ad0s4       将 UFS 文件系统写入磁盘 1，切片 4
```

# 第 7 章：文件系统管理

此时，你的文件系统应该已经准备好使用了。稍后，我们将描述更多关于如何使用 `mount` 命令来挂载文件系统。现在，你可以尝试以下操作来快速检查新文件系统是否可以挂载：

```
# mkdir /mnt/musc               创建挂载点
# mount /dev/ad04 /mnt/musc      将磁盘 1，切片 4 上的文件挂载到 /mnt/musc
```

# 与 `Linux` 兼容系统一起

在 `FreeBSD` 中带有 `Linux` 兼容软件使得拥有 `Linux` 兼容系统（如 `ext2` 和 `ext3`）成为可能。除了工具（如 `mkfs.ext2` 和 `mkfs.ext3`）外，在 `FreeBSD` 中创建 `Linux` 兼容的文件系统需要遵循以下步骤。

# 第 7 章：文件系统管理

| 上次挂载时间: | `n/a` |
| 上次写入时间: | `Tue` `Feb` `19` `00:41:25` `2008` |
| 挂载次数: | `0` |
| 最大挂载次数: | `36` |
| 最后检查: | `Tue` `Feb` `19` `00:41:23` `2008` |
| 检查间隔: | `15552000` (`6` `months`) |
| 下次检查于: | `Sun` `Aug` `17` `01:41:23` `2008` |
| 预留块 `uid`: | `0` (`user` `root`) |
| 预留块 `gid`: | `0` (`group` `wheel`) |

输出显示了关于文件系统的大量信息。例如，如果你有一个需要创建小文件的文件系统（例如新闻服务器），你可以检查 `inode` 是否已经耗尽。设置最大挂载次数（`Maximum` `mount` `count`）可以确保文件系统在挂载指定次数后进行错误检查。你还可以找到文件系统创建、挂载和最后写入的日期和时间。

要更改现有的 `ext2` 或 `ext3` 文件系统的设置，你可以使用 `tune2fs` 命令。以下命令通过将挂载次数设置为 `-1`，更改了文件系统强制禁用挂载计数前的次数：

```
# tune2fs -c 31 /dev/ad0s4    Sets # of mounts before check is forced
tune2fs 1.38 (30-Jun-2005)
Setting maximal mount count to 31
```

如果你想切换到基于时间间隔而非挂载次数的文件系统检查，请通过将挂载次数设置为 `-1` 来禁用挂载计数：

```
# tune2fs -c -1 /dev/ad0s4
tune2fs 1.38 (30-Jun-2005)
Setting maximal mount count to -1
```

使用 `-i` 选项启用依赖时间的检查。以下是一些示例：



```
# tune2fs -i 10 /dev/ad0s4      Check after 10 hours
tune2fs -i 1d /dev/ad0s4      Check after 1 day
tune2fs -i 3w /dev/ad0s4      Check after 3 weeks
tune2fs -i 6m /dev/ad0s4      Check after 6 months
tune2fs -i 0 /dev/ad0s4       Disable time-dependent checking
```

请确保你开启了挂载次数依赖检查或时间依赖检查之一。

## 创建内存磁盘文件系统

如果你想创建一个更具移植性的文件系统（换句话说，不绑定到物理磁盘），你可以创建一个内存磁盘文件系统。内存磁盘文件系统是位于文件系统内部的一个。你可以将其格式化为文件系统，挂载和卸载它，甚至在不同的计算机之间移动并使用它。

内存磁盘文件系统用于备份数据、创建现场 CD 或运行专用虚拟操作系统。在接下来的示例中，你创建一个空白的 GB 磁盘文件，将其格式化为文件系统，并挂载它以访问文件系统上的数据：

```
# dd if=/dev/zero of=mydisk count=2048000  Create zero-filled IGB file
2048000+0 records in
2048000+0 records out
104857600 bytes transferred in 56.519727 secs (18552393 bytes/sec)
# du -sh mydisk  Check memory disk size
1.0G mydisk
# mdconfig -a t vnode -f mydisk -u 2  Identifies mydisk as memory disk file
# bsdlabel -w md2 auto  Adds BSD label to file
# newfs mda2  Creates UFS file system
/dev/md2:1000.0MB (204800 sectors) block size 16384, fragment size 2048
using 6 cylinder groups of 183.78MB, 11761 blocks, 23552 nodes.
super-block backups (for fsck -b at):
160, 37512, 752864, 1129312, 105568, 181920
# mkdir /mnt/mydisk  Creates mount point
# umount /mnt/md2 /mnt/mydisk  Memory disk unmount
```

在此过程中，`dd` 命令创建了一个 2048000 (1 GB) 的空磁盘文件。`mdconfig` 命令将 `mydisk` 文件识别为内存磁盘的存储区域。`bsdlabel` 命令为文件镜像创建 BSD 标签。`newfs` 命令在该镜像上创建一个 UFS 文件系统。

当挂载虚拟文件系统时，你可以像访问任何文件系统一样访问它。当你完成对文件系统的操作后，请离开并卸载它：

```
# cd /mnt/mydisk  Change to the mount point
# mkdir testdir  Create a directory on the file system
# cp /etc/hosts .  Copy a file to the file system
# cd  Leave the file system
# umount /mnt/mydisk  Unmount the file system
```

在卸载虚拟文件系统后，你可以将其移动到另一个系统或将其刻录到 CD 中作为文件系统。如果你不再需要该文件系统，直接删除即可。

## 创建和使用分区

BSD 系统需要交换分区来处理 RAM 溢出。如果你在安装时没有创建交换分区，可以稍后创建。你可以在普通磁盘分区（如前所述识别新分区）或格式化为交换分区的文件上创建交换区域，方法如下：

```
# dd if=/dev/zero of=/tmp/swapfile0 count=65536
65536+0 records in
65536+0 records out
3355432 bytes transferred in 1.54122 secs (217609 bytes/sec)
# chmod 600 /tmp/swapfile0
# mdconfig -a t v -f /tmp/swapfile0 -u 0
# swapon /dev/md0
```

`dd` 命令创建一个名为 `swapfile0` 的文件。`chmod` 命令锁定权限。`mdconfig` 命令配置交换为 md 设备。创建交换分区或文件后，你需要使用 `swapon` 命令告诉系统使用该交换区域。这与启动时发生的情况类似。例如：

```
# swapon /dev/md0
Turn swap on for /dev/md0
```

你可以使用 `swapinfo` 命令查看交换文件和分区的列表：

| Filename | 1K-blocks | Used | Avail | Capacity |
|---|---|---|---|---|
| /dev/ad0sb | 487880 | 0 | 487880 | 0% |
| /dev/md0 | 32768 | 0 | 32768 | 0% |
| Total | 520648 | 0 | 520648 | 0% |

```
# swapinfo -h
View all swap files and partitions in megabytes
```

| Device | 1K-blocks | Used | Avail | Capacity |
|---|---|---|---|---|
| /dev/ad0sb | 487880 | 0B | 476M | 0% |
| /dev/md0 | 32768 | 0B | 32M | 0% |
| Total | 520648 | 0B | 508M | 0% |

```
# swapinfo -k
View all swap files and partitions in kilobytes
```

要关闭交换区域，可以使用 `swapoff` 命令。只有在你确定交换区域未被使用时才执行此操作，否则可能会导致崩溃：

```
# swapoff /dev/md0
Turn off swap partition
# swapoff /dev/ad0sb
Turn off swap partition
# swapoff -a
Turn off all swap partitions
```

### 挂载和卸载文件系统

在使用普通非交换文件系统之前，你需要通过挂载将其附加到计算机文件树中的目录。你的根 (`/`) 以及经常使用的其他文件系统通常根据 `/etc/fstab` 文件中的条目自动挂载。其他文件系统可以使用 `mount` 命令手动挂载。

### 从 fstab 挂载文件系统

当你安装 FreeBSD 时，`/etc/fstab` 文件通常会自动设置，包含根分区和其他分区的信息。这些分区可以设置为在启动时挂载，或准备好手动挂载（在手动挂载时可以使用挂载点和选项）。

这是一个 `/etc/fstab` 文件的示例：

| Device | Mountpoint | FType | Options | Dump | Pass# |
| --- | --- | --- | --- | --- | --- |
| /dev/ad0s1 | none | swap | sw | 0 | 0 |
| /dev/ad0s1 | | ufs | rw | 1 | 2 |
| /dev/ad0s1 | /tmp | ufs | rw | 2 | 2 |
| /dev/ad0s1 | /usr | ufs | rw | 2 | 2 |
| /dev/ad0s1 | /var | ufs | rw | 2 | 2 |
| /dev/acd0 | | cdrom | cd9660 | ro,noauto | 0 | 0 |
| /dev/ad0s2 | /mnt/debian | ext2fs | rw | 0 | 0 |

所有系统都会自动挂载，位于 `/dev/acd0` 的 CD 驱动器除外（由 `noauto` 选项指示）。根 (`/`)、`/tmp`、`/usr` 和 `/var` 分区是普通的 UFS 文件系统，并以读写 (`rw`) 模式挂载。在本示例中，手动添加了 `/dev/ads02` 切片（磁盘切片 2），以挂载该设备上的 Debian GNU/Linux 分区。

表 7-2 说明了 `/etc/fstab` 文件中的每个字段。

### 表 7-2：/etc/fstab 文件字段

| 字段 | 描述 |
| --- | --- |
| 1 | 代表文件系统的设备名称。这是挂载为 `/dev/ad0s1` 的分区设备名称。如果整个切片专门用于单个文件系统，它也可以包含代表切片的设备名称（例如代表切片 2 的 `/dev/ad02`） |
| 2 | 文件系统中的挂载点。文件系统包含从挂载点向下树结构的所有数据，除非在下方某处挂载了另一个文件系统 |
| 3 | 文件类型。见表 7-1 的许多常见文件类型列表 |
| 4 | 挂载计数选项。挂载选项示例包括 `noauto`（防止文件系统在启动时挂载）或 `ro`（以只读模式挂载文件系统）。选项之间用逗号分隔。查看 `mount` 手页 (`-o`) 以获取其他支持的选项 |
| 5 | 备份文件系统？这仅在你运行 `dump` 备份时有效。正数表示应该对文件系统进行备份。数字 1 意味着首先备份文件系统（用于根分区）。数字 2 假设文件系统可以在根分区之后的任何时间进行备份 |
| 6 | 检查文件系统？字段中的数字指示文件系统是否需要用 `fsck` 进行检查。零表示不检查文件系统。结合 `dump` 指示器，数字 1 意味着需要首先检查文件系统（用于根分区）。数字 2 假设文件系统可以在根分区之后的任何时间进行检查 |

## 第 7 章：文件系统管理

你可以在 `/etc/fstab` 文件中为任何想要的硬盘分区或可移动媒体分区创建自己的条目。远程文件系统（NFS、Samba 等）也可以包含在 `/etc/fstab` 文件条目，以便在启动时或之后自动挂载这些文件系统。

### 使用 mount 命令挂载文件系统

`mount` 命令用于查看已挂载的文件系统，以及挂载任何本地（硬盘、USB 驱动器、CD、DVD 等）或远程（NFS、Samba 等）文件系统。以下是列出文件系统的 `mount` 命令示例：

```
$ mount List mounted remote and local file systems
dev/ad0s1 on / (ufs, local)
devfs on /dev (devfs, local)
dev/ad0s1 on /tmp (ufs, local, soft-updates)
dev/ad0s1 on /usr (usr, local, soft-updates)
dev/ad0s1 on /var (var, local, soft-updates)
dev/ad0s2 on /mnt/debian (ext2fs, local)
$ mount -v List mounted file systems with file system id
dev/ad0s1 on / (ufs, local), fsid 3bebab47a6961229
devfs on /dev (devfs, local), fsid 00ff00505000000
dev/ad0s1 on /tmp (ufs, local, soft-updates), fsid 3bebab47c27d24c2
dev/ad0s1 on /usr (usr, local, soft-updates), fsid 3bebab4746a302f2
dev/ad0s1 on /var (var, local, soft-updates), fsid 3bbebab4797a19385
dev/ad0s2 on /mnt/debian (ext2fs, local), fsid 4f00000080000000
```

使用 `-t` 仅列出特定文件类型的列表：

```
$ mount -t ufs List mounted ufs file systems
dev/ad0s1 on / (ufs, local)
dev/ad0s1 on /tmp (ufs, local, soft-updates)
dev/ad0s1 on /usr (usr, local, soft-updates)
dev/ad0s1 on /var (var, local, soft-updates)
$ mount -t ext2 List mounted ext2 file systems
dev/ad0s2 on /mnt/debian (ext2fs, local)
```

以下是一个将本地文件系统（`/dev/ad0s4` 设备）挂载到现有目录挂载点 `/mnt/music` 的简单命令：

```
# mount /dev/ad0s4 /mnt/music Mount a local file system
# mount -v /dev/ad0s4 /mnt/music/ Mount file system, more verbose
```

在上述示例中，`mount` 命令将会在 `/etc/fstab` 文件中查找 `/dev/sda` 的条目，或者猜测文件系统的类型：

使用 `-t` 显式指定要挂载的文件系统类型：

```
# mount -v -t ext2fs /dev/ad0s4 /mnt/music/ Mount an ext2 file system
dev/ad0s4 on /mnt/music (ext2fs, local), fsid 5e000000800000000
```

## 第 7 章：文件系统管理

如果你挂载的内容已经列在 `fstab` 文件中，你只需要指定挂载点或设备。例如，使用以下 `fstab` 条目：

```
/dev/ad0s4       /mnt/music      ext2fs  rw  2 2
```

你可以使用一些选项来挂载文件系统：

```
# mount -v /dev/ad0s4  Mount file system with device name only
/dev/ad0s4 /mnt/music  (ext2fs, local, fsid 5e00000000000000)
# mount -v /mnt/music  File system with mount point only
/dev/ad0s4 /mnt/music  (ext2fs, local, fsid 5e00000000000000)
```

你可以通过添加 `-o` 和逗号分隔的选项列表来指定挂载选项。相同的选项也可以添加到 `/etc/fstab` 文件的第 4 字段。默认情况下，分区以读/写方式挂载。你可以显式指定将文件系统挂载为只读（`ro`）或读/写（`rw`）：

```
# mount -v ext2fs -o rw /dev/ad0s4 /mnt/music  Mount read/write
/dev/ad0s4 /mnt/music  (ext2fs, local), fsid 5e000000000000000)
# mount -v ext2fs -o ro /dev/ad0s4 /mnt/music  Mount read-only
/dev/ad0s4 /mnt/music  (ext2fs, local), fsid 5e000000000000000)
```

你可以使用的一些用挂载选项：

- `noatime`：不更新文件的访问时间。对于具有大量 I/O 的文件系统（如交换分区和日志）很有。
- `noexec`：防止执行该文件系统上的二进制文件。可以用于对于不可信用户的 `/tmp` 增加安全性。
- 就像交换到一个文件一样，你可以在文件中创建一个文件系统并将其挂载，这样你就可以查看其内容。创建此类文件在本章前面的“创建磁盘”部分有描述。一种常见的情况是在下载 LiveCD 后。通过挂载该 CD，你可以查看内容或将文件拷贝到你的硬盘。

```
# mdconfig -a vnode -f /usr/images/FreeBSD-2.0.1-iso -o 1 /mnt/freebies
# mount -t /dev/md1 /mnt/freebies
# ln -s /mnt/freebies/boot
```

| | | |
| :--- | :--- | :--- |
| .rsh_ | boot | tmp |
| .profile | root | usr |
| pkg_info.txt | uzip | |
| dist | libexec | sys |

### 卸载文件系统

卸载文件系统，使用 `umount` 命令。你可以使用设备名称或挂载点进行卸载。避免设备名称（很多非常相似）。

```
# umount -v /dev/ad0s4      Unmount by device
dev/sda1 unmounted
# umount -v /mnt/music      Unmount by mount
/tmp/disk.img unmounted
```

如果设备忙，卸载将失败。卸载失败的一个常见原因是你在目录内打开了 shell：

```
# umount -v /mnt/music
umount: of /mnt/music failed: Device busy
```

### 检查文件系统

文件系统传统上在启动时进行检查。`fstab` 文件中的设置用于决定哪些文件系统在挂载之前进行检查。`fsck` 命令实际上取决于一组特定文件的 `fsck` 命令，不仅检查文件系统中的一致性问题，还可以交互地修复这些问题。



在文件系统挂载并允许用户访问系统后，`fsck` 可以带有 `-B` 标志再次运行以进行后台检查。你可以随时运行 `fsck` 来检查并可能修复文件系统。与其使用 `fsck` 来确定文件类型，不如直接在你的文件系统上运行特定的命令。这些命令包括 `fsck_ufs` 和 `fsck_msdos`。

以下示例显示了如何通过简单添加要检查的磁盘分区设备来使用 `fsck_ufs` 命令检查 UFS 文件系统：

```
# fsck_ufs /dev/ad0s4          Check UFS file system of inconsistencies
** /dev/ad0s4
** Last Mounted on /mnt/extra
** Phase 1 - Check Blocks and Sizes
** Phase 2 - Check Pathnames
** Phase 3 - Check Connectivity
** Phase 4 - Check Reference Counts
** Phase 5 - Check Cyl groups
377 files, 864 used, 371871 free (15 fragments, 46732 blocks, 0.0% fragmentation).
```

此示例显示了对 IDE 硬盘 1 (`/dev/ad0s4`) 分的文件系统检查。分区未挂载，可以这样做。这里是使用 `fsck_ufs` 命令检查文件系统时可以使用的一些其他示例：

```
# fsck_ufs -B /dev/ad0s1    Run check in the background
# fsck_ufs -B -f ad0s1       Force file system check, even if marked clean
** /usr/snap/fsck_snapshot
** Last Mounted on /usr
** Phase 1 - Check Blocks and Sizes
** Phase 2 - Check Pathnames
** Phase 3 - Check Reference Counts
** Phase 5 - Check Cyl groups
198317 files, 181432 used, 6730360 free (25136 frags, 838153 blocks, 0.3% fragmentation)
** fsck_ufs -d /dev/ad0s1
** fsck_ufs -y /dev/ad0s1
```

*   在不执行的情况下打印命令（调试模式）
*   让 `fsck` 对任何问题（如修复）回答是

如果你想使用 DOS 文件系统，你可以使用 `fsck_msdos` 命令。在示例中，USB 闪器上的第二个分区（`/dev/da0s2`）包含一个 DOS 文件系统。你可以使用 `newfs_msdos` 命令创建一个 DOS 分区。（注意内存棒和 SCSI 驱动器的设备名称以 `da` 开头，这与命名的 IDE 硬盘不同。）

```
** newfs_msdos /dev/da0/m2
** fsck_msdos /dev/da0s2
** /dev/da0s2 (NO WRITE)
** Phase 1 - Read and Compare FATs
** Phase 2 - Check Cluster Chains
** Phase 3 - Checking Directories
** Phase 4 - Checking for Lost Files
2712 files, 610448 free (38153 clusters)
MARK FILE SYSTEM CLEAN? no
*****
```

*   在 USB 设备 1，slice 2 上创建 DOS 文件系统
*   检查 DOS 分区（在第二个 slice 上，最后一个 `da` 设备）

注意文件系统被列为 `NO WRITE`，因为当前是挂载状态。所以它不能被标记为干净。在卸载文件系统并再次运行 `fsck_msdos` 后，文件系统可以被标记为干净：

```
# mount /dev/da0s2
** fsck_msdos /dev/da0s2
** /dev/da0s2
** Phase 1 - Read and Compare FATs
** Phase 2 - Check Cluster Chains
** Phase 3 - Checking Directories
** Phase 4 - Checking for Lost Files
2712 files, 610448 free (38153 clusters)
```

挂载后运行检查

如果在文件检查期间发生了 `fsck` 错误（你没有指示 `-y` 来自动回答是并继续），你可以交互地决定是否要修复这些错误。这里是一个示例：

```
# fsck_msdos /dev/da0s2
** /dev/da0s2
** Phase 1 - Read and Compare FATs
```

检查带有错误的文件系统

```
123
```

# 第 7 章：文件系统管理

## 第二阶段 - 检查集群链

```
## 第三阶段 - 检查目录
/hello.txt 以空闲簇开始
是否截断？[yn] y
## 第四阶段 - 检查丢失文件
2713 个文件，610448 空闲 (38153 个簇)
标记文件系统为清洁？[yn] y
正在标记文件系统为清洁
***** 文件系统已修改 ****
```

在示例中，当包含该文件的 U 盘被拔出时，只有 `hello.txt` 文件在文本编辑器中打开。随后的文件检查显示了该错误，我可以通过输入 `y` 修复了它。

## 查找文件系统使用情况

磁盘空间不足在你的桌面上可能很困恼，但在你的服务器上可能是一场灾难。要确定可用多少磁盘空间以及当前使用了多少，你可以使用 `df` 命令。要检查特定文件和目录占用了多少磁盘空间，请使用 `du` 命令。

`df` 命令提供挂载文件系统的利用率摘要。使用 `-h` 选项，可以将数据（默认显示）转换为千字节 (K)、兆字节 (M) 和吉字节 (G)，使输出更符合人类阅读习惯：

| 文件系统 | 大小 | 已用 | 可用 | 容量 | 挂载点 |
|---|---|---|---|---|---|
| `/dev/sda1` | 496M | 39M | 417M | 9% | `/` |
| `/devfs` | 1.0K | 1.0K | 0B | 100% | 0 | `/dev` |
| `/dev/ada0le` | 496M | 32M | 456M | 0% | 17 | `/tmp` |
| `/dev/ada0f` | 16G | 3.5G | 12G | 23% | `/usr` |
| `/dev/ada0d` | 1.2G | 19M | 1.1G | 2% | `/var` |
| `/dev/ada02` | 7.3G | 593M | 6.4G | 8% | `/mnt/debian` |
| `/dev/da01` | 48M | 85K | 45K | 2% | `/mnt/da01` |

每个物理保存到文件系统中的文件都由一个 `inode` 表示。如果你的文件系统有许多小文件，你可能会耗尽 `inode`。使用 `-i` 选项通过 `df` 命令检查 `inode` 利用率：

| 文件系统 | 大小 | 已用 | 可用 | 容量 | 空闲 | 已用率 | 挂载点 |
|---|---|---|---|---|---|---|---|
| `/dev/sda1` | 496M | 39M | 417M | 11% | 64673 | 2% | `/` |
| `/devfs` | 1.0K | 1.0K | 0B | 100% | 0 | 100% | `/dev` |
| `/dev/ada0le` | 496M | 34M | 456M | 0% | 65773 | 0% | `/tmp` |
| `/dev/ada0f` | 16G | 3.5G | 12G | 23% | 2015570 | 9% | `/usr` |
| `/dev/ada0d` | 1.2G | 19M | 1.1G | 2% | 26523 | 162339 | 2% | `/var` |

如果你有网络挂载（如 Samba 或 NFS），它们也会出现在你的 `df` 输出中。要将 `df` 输出限制为本地文件系统，请使用 `-l`（代表 `local`）选项：

```
$ df -hl          仅显示本地文件系统的磁盘空间
```

要显示特定文件系统的输出，请使用 `-T` 选项：

```
$ df -ht ufs    仅显示文件系统类型

文件系统      大小    可用 容量 挂载点

/dev/ada0s0      496M    39M    417M 9%         /
```

要检查文件系统中特定目录或文件的磁盘空间，请使用 `du` 命令。以下命令由 `francois` 命名：

```
$ du -h /home/    显示 /home 目录的磁盘空间

du: /home/chris: Permission denied

4.0K             /home/francois/Mail

52K             /home/francois

64K             /home/
```

输出显示，出于安全原因，拒绝访问另一个主目录的磁盘（在此例中为 `/home/chris`）。下面的示例展示了如何使用 `root` 用户账户来避免权限问题并获得正确的总计。当我们使用 `-s` 进行汇总时，这一点非常明显：

```
$ du -sh /home   普通用户被拒绝查看他人主目录的空间总计

du: /home/chris: Permission denied

du: /home/horatio99: Permission denied

64K             /home

# du -sh /home   你可以以 root 用户身份显示磁盘使用摘要

1.6G             /home/
```

你可以使用 `-c` 选项指定多个目录并对其求和：

```
$ du -sch /home /var  显示目录和总计

1.6G             /home

19M             var

1.6G             total
```

使用 `maxdepth` 选项可以限制递归的深度：

```
$ du -h --maxdepth=1 /home  显示一级目录的占用

du: /home/chris: Permission denied

4.0K             /home/francois/Mail

52K             /home/francois

64K             /home/
```

使用 `-exclude` 选项可以排除指定的文件：

```
$ du -h --exclude="*.log" /var  排除日志日志的文件

100M             total
```



# 第 7 章：文件系统管理

## 第二阶段 - 检查集群链

## 第三阶段 - 检查目录

`/hello.txt` 以空闲簇开始
是否截断？[yn] `y`

## 第四阶段 - 检查丢失文件

2713 个文件，610448 空闲 (38153 个簇)
标记文件系统为清洁？[yn] `y`
正在标记文件系统为清洁

\***** 文件系统已修改 \****

在示例中，只有 `hello.txt` 文件在文本编辑器中打开时，包含该文件的 U 盘被拔出。随后的文件检查显示了该错误，我可以通过输入 `y` 修复了它。

## 查找文件系统使用情况

磁盘空间不足在你的桌面上可能很困恼，但在你的服务器上可能是一场灾难。要确定可用多少磁盘空间以及当前使用了多少，你可以使用 `df` 命令。要检查特定文件和目录占用了多少磁盘空间，请使用 `du` 命令。

`df` 命令提供挂载文件系统的利用率摘要。使用 `-h` 选项，可以将数据（默认显示）转换为千字节 (K)、兆字节 (M) 和吉字节 (G)，使输出更符合人类阅读习惯：

| 文件系统 | 大小 | 已用 | 可用 | 容量 | 挂载点 |
|---|---|---|---|---|---|
| `/dev/sda1` | 496M | 39M | 417M | 9% | `/` |
| `/devfs` | 1.0K | 1.0K | 0B | 100% | `/dev` |
| `/dev/ada0le` | 496M | 32M | 456M | 0% | `/tmp` |
| `/dev/ada0f` | 16G | 3.5G | 12G | 23% | `/usr` |
| `/dev/ada0d` | 1.2G | 19M | 1.1G | 2% | `/var` |
| `/dev/ada02` | 7.3G | 593M | 6.4G | 8% | `/mnt/debian` |
| `/dev/da01` | 48M | 85K | 45K | 2% | `/mnt/da01` |

每个物理保存到文件系统中的文件都由一个 `inode` 表示。如果你的文件系统有许多小文件，你可能会耗尽 `inode`。使用 `-i` 选项通过 `df` 命令检查 `inode` 利用率：

| 文件系统 | 大小 | 已用 | 可用 | 容量 | 空闲 | 已用率 | 挂载点 |
|---|---|---|---|---|---|---|---|
| `/dev/sda1` | 496M | 39M | 417M | 11% | 64673 | 2% | `/` |
| `/devfs` | 1.0K | 1.0K | 0B | 100% | 0 | 100% | `/dev` |
| `/dev/ada0le` | 496M | 34M | 456M | 0% | 65773 | 0% | `/tmp` |
| `/dev/ada0f` | 16G | 3.5G | 12G | 23% | 2015570 | 9% | `/usr` |
| `/dev/ada0d` | 1.2G | 19M | 1.1G | 2% | 26523 | 162339 | 2% | `/var` |

如果你有网络挂载（如 Samba 或 NFS），它们也会出现在你的 `df` 输出中。要将 `df` 输出限制为本地文件系统，请使用 `-l`（代表 `local`）选项：

```bash
$ df -hl          仅显示本地文件系统的磁盘空间
```

要显示特定文件系统的输出，请使用 `-T` 选项：

```bash
$ df -ht ufs    仅显示文件系统类型

文件系统      大小    可用 容量 挂载点

/dev/ada0s0      496M    39M    417M 9%         /
```

要检查文件系统中特定目录或文件的磁盘空间，请使用 `du` 命令。以下命令由 `francois` 命名：

```bash
$ du -h /home/    显示 /home 目录的磁盘空间

du: /home/chris: Permission denied

4.0K             /home/francois/Mail

52K             /home/francois

64K             /home/
```

输出显示，出于安全原因，拒绝访问另一个主目录的磁盘（在此例中为 `/home/chris`）。下面的示例展示了如何使用 `root` 用户账户来避免权限问题并获得正确的总计。当我们使用 `-s` 进行汇总时，这一点非常明显：

```bash
$ du -sh /home   普通用户被拒绝查看他人主目录的空间总计

du: /home/chris: Permission denied

du: /home/horatio99: Permission denied

64K             /home

# du -sh /home   你可以以 root 用户身份显示磁盘使用摘要

1.6G             /home/
```

你可以使用 `-c` 选项指定多个目录并对其求和：

```bash
$ du -sch /home /var  显示目录和总计

1.6G             /home

19M             var

1.6G             total
```

使用 `maxdepth` 选项可以限制递归的深度：

```bash
$ du -h --maxdepth=1 /home  显示一级目录的占用

du: /home/chris: Permission denied

4.0K             /home/francois/Mail

52K             /home/francois

64K             /home/
```

使用 `-exclude` 选项可以排除指定的文件：

```bash
$ du -h --exclude="*.log" /var  排除日志日志的文件

100M             total
```

# 第 8 章：备份与可移动介质

在刚才所示的示例中

当你想要将文件返回文件系统（解压缩并解压 `tar` 包）时，你也可以通过一步或两步过程来实现，使用 `tar` 命令以及可选的 `gunzip` 命令：

```bash
$ gunzip -c myfiles.tar.gz | tar xf -
```



# 解压缩并提取归档文件

或者尝试以下命令行：

```
$ gunzip myfiles.tar.gz ; tar xf myfiles.tar.gz  # 解压缩后提取归档文件
```

此命令会删除 `tar.gz` 文件，只留下 `.tar` 文件。要一步到位完成此操作，你可以使用以下命令：

```
$ tar xvf myfiles.tar.gz
 x textfile1.txt
 x textfile2.txt
```

上述命令的结果是将归档的 `.txt` 文件从归档复制到当前目录。`x` 选项提取文件，`z` 解压缩（解压）文件，`v` 输出输出，`f` 表示下一个选项是归档文件的文件名（`myfiles.tar.gz`）。

## 使用压缩工具

压缩是处理备份文件的一个重要方面。它在备份介质（CD、DVD、磁带等）或服务器上存储文件所需的磁盘空间更少。将归档文件传输到介质或通过网络下载的时间也更短。

虽然压缩可以节省大量的存储空间和传输时间，但它会显著增加 CPU 使用率。你可以考虑在磁带驱动器使用硬件压缩（`www.amanda.org/docs/faq.html#id346016`）。

> 注意：请查看 `mt` 命令的页面，详细了解如何通过软件设置大多数磁带驱动器的压缩。

在上一节所示的示例中，`tar` 调用了 `gzip`。但 `tar` 可以与许多压缩工具配合工作。FreeBSD 自带的 `tar` 可以处理 `gzip` 和 `bzip2`。我们添加到工具箱的第三种压缩实用是 `lzop` 命令，它可以以不同的方式与 `tar` 使用。这些工具从最快/压缩率最低到最慢/压缩率最高的顺序是：`lzop`、`gzip` 和 `bzip2`。

如果你正在归档和压缩大量数据，压缩备份所需的时间可能会非常显著。你应该意识到，通常情况下，`bzip2` 花的时间大约是 `gzip` 的五倍，而只能提供两倍的压缩率。然而，每次压缩你都可以选择不同的压缩级别，以平衡对更高压缩的需求与所需的时间。

使用 `tar` 命令配合 `bzip2` 压缩，使用 `-j` 选项。如果不存在，你可以通过 `pkg_add -r bzip2` 添加 `bzip2` 包：

```
$ tar cvf myfiles.tar.bz2 *.txt    创建归档，并使用 bzip2 压缩
```

你可以使用 `tar` 命令将 bzip2 压缩的文件解压缩（-j）并提取文件（-x）：

```
$ tar xvf myfiles.tar.bz2    提取文件，解压缩 bzip2 压缩
```

`lzip` 压缩与 `tar` 的集成程度稍低。在使用 `lzip` 之前，你需要安装 `lzip` 包。要进行 `lzip` 压缩，你可以将 `tar` 的输出通过管道传递给 `lzip`，如下：

```
$ pkg-add -r lzip
$ tar -cf | lzip > myfiles.tar.lz    创建 lzip 压缩 tar 归档
$ lzip -d < myfiles.tar.lz tar -xf    提取 lzip 压缩 tar 归档
```

在之前的示例中，RAR 格式的 `.rar` 压缩文件通过在命令前的开关反转了 `tar` 的顺序。对于普通用法和其他示例，我们使用了不带开关的 `tar` 现代语法。

> 注意：你可能会遇到 RAR 格式的 `.rar` 压缩文件。这种格式在点对点网络中非常流行。RAR 是一种专用格式，因此没有广泛的压缩工具。FreeBSD ports 系统中提供了一个 `rar` 包（`/usr/ports/archivers/rar`）。另一方面，`unrar` 命令在 FreeBSD 中提供了一个二进制包。

## 使用 gzip 压缩

如所述，你可以使用任何命令行命令（而不是 `tar` 命令行）。以下是使用 `gzip` 命令创建和处理 `gzip` 压缩文件的示例：

```
$ gzip myfile          对 myfile 进行 gzip 并重命名为 myfile.gz
```

以下命令提供了带有详细输出的结果：

```
$ gzip -v myfile          带详细输出的 gzip myfile
myfile: 86.0%          已替换为 myfile.gz

$ gzip -tv myfile.gz      测试 gzip 文件的完整性
myfile.gz:               OK

$ gzip -lv myfile.gz      获取 gzip 文件的详细信息
```

| 方法 | crc | 日期 时间 | 压缩大小 | 未压缩比例 | 未压缩名称 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| defla | 02f7d9e4 | 7 10 04:48 | 46785 | 334045 | 86.0% |

使用以下任意命令压缩目录中的文件：

- `gzip -rv mydir` 压缩目录中的所有文件
  `myfile/file: 39.1% -- 已替换为 mydir/file.gz`
  `myfile/file2: 39.5% -- 已替换为 mydir/file2.gz`
- `gzip -1 myfile` 时间最快，压缩率最低
- `gzip -9 myfile` 时间最慢，压缩率最高

添加 `1` 到 `9` 之间的数字来设置级别。如上所示，`-1` 是最快（最低），`-9` 是最慢（最高）。`gzip` 的默认值是 `6`。以下示例均涉及解压缩。要解压缩文件，你可以使用 `gunzip` 命令。

（注：提供的 OCR 文本在后半部分非常碎片。我已处理了连贯部分并合并了可用片段。）

# 通过网络进行备份

在备份文件并将它们汇总到一个 tar 归包后，你该如何处理这个归包呢？备份的首要目的是以防发生某些情况（例如硬件崩溃），导致你需要从该备份实践中恢复文件。你可以采用的确保备份安全的方法包括：

- 将备份拷贝到可移动介质，如磁带、CD 或 DVD（本章稍后将进行描述）
- 通过网络将备份拷贝到另一台机器

快速且可靠的网络、廉价的高容量硬盘，以及将数据移至异地存储带来的安全性，都使得网络备份成为了一项流行的做法。对于备份个人数据的个人或小型办公室来说，组合几个简单的命令可能就是你执行和保护备份的所有需求。这种方法代表了 UNIX 哲学的直接应用：将只执行单一功能的简单程序组合在一起完成更复杂的任务。

虽然可以使用任何可以在网络上复制文件的命令将数据移动到远程机器，但某些工具特别适合这项工作。你可以设置无密码备份传输以及其他机器的加密传输。

如 `rsync` 命令等工具可以通过仅备份自上次备份以来发生更改的文件（或文件的部分）来节省资源。使用如 `unison` (`www.cis.upenn.edu/~bpierce/unison/`) 等工具，你可以从 Windows 以及 BSD 系统通过网络备份文件。

接下来的章节描述了这些通过网络将数据备份到其他机器的技术。

> 注意：一个你可能感兴趣的工具是 `rsnapshot` 命令 (`pkg_add -r rsnapshot`)。`rsnapshot` 命令 (`www.rsn.org/`) 可以与 `rsync` 配合使用，对文件系统创建可配置的每日、每周或每月快照。它使用硬链接保留文件系统的快照，然后与更改的文件进行同步。

# 通过 ssh 备份 tar 归包

OpenSSH (`www.openssh.org/`) 提供了网络接口进行安全远程登录、远程执行和远程文件复制的工具。通过设置两个机器共享加密密钥，你可以在这些机器之间传输文件，而无需每次都输入密码。这允许你创建脚本，从 SSH 客户端向 SSH 服务器备份数据，无需任何手动干预。

# 第 8 章：备份与可移动介质

从中央 BSD 系统，你可以使用 OpenSSH 命令从多个客户端机器收集备份。以下示例在远程站点运行 `tar` 命令（用于归档和压缩文件），将 `tar` 流重定向到标准输出，并使用 `ssh` 命令在本地（通过 ssh）捕获备份：

```bash
$ mybackup; cd mybackup
$ francis@server1 'tar cf - myfile*' | tar xvf -
francis@server1's password: ******
myfile
myfile2
```

在上述示例中，所有以 `myfile` 开头的文件都从 server1 上 francis 的家目录复制并放置在当前目录中。注意，管道的左侧创建了归包，右侧从当前目录扩展文件 [原文：此处可能是“解压到当前目录”]。（请记住，如果本地文件存在，ssh 可能会覆盖它们，这就是为什么我们在示例中创建了一个空目录。）

若要反转这一过程并将文件从本地系统拷贝到远程系统，我们首先运行本地命令。这次，我们添加了 `cd` 命令将文件放在远程机器上选择的目录中：

```bash
$ tar cf - myfile* | ssh francis@server1 \
  cd /home/francis/folder/; tar xvf -
francis@server1's password: ******
myfile
myfile2
```

在这个示例中，我们并不在接收端解压文件，而是将脚本写入 `tgz` 文件中：

```bash
$ ssh francis@server1 'tar czf - myfile*' | cat > files.tgz
$ tar cvzf - myfile* | ssh francis@server1 'cat > files.tgz'
```

第一个示例从 server1 上 francis 的家目录获取所有以 `myfile` 开头的文件，对它们进行 tar 归档和压缩，并将这些压缩后的文件发送到本地系统上的 `myfile.tgz` 文件。第二个示例执行了相反操作，获取本地目录中所有以 `myfile` 开头的文件并将其发送到远程的 `myfile.tgz` 文件。

所示示例仅用于通过网络复制文件。除了压缩之外，它们允许你使用选择的任何 `tar` 特性，例如增量备份功能。

# 使用 rsync 备份文件

功能更丰富的备份命令是 `rsync`。`rsync` 的独特之处在于 `rsync` 算法，它使用校验和逐块比较本地和远程文件，并仅传输不同的块。该算法如此高效，已被许多备份产品复用。要添加 `rsync` 软件包，可以使用 `pkg_add -r rsync`。

`rsync` 命令可以在远程服务器 (ssh) 之上运行，也可以通过服务器端运行 `rsync` 守护进程。以下示例通过 ssh 使用 `rsync` 镜像目录：

```bash
$ rsync -avz --delete server1:chris@home/chris/pics/ chrispics/
```

该命令旨在将远程目录结构 (`/home/chris/pics/`) 镜像到本地系统上的目录 (`chrispics/`) 中。`-a` 表示以归档模式运行（递归复制远程目录的所有文件），`-z` 压缩文件，`-v` 输出详细输出。`--delete` 告诉 `rsync` 删除远程系统中已不存在的任何文件。

对于持续备份，你可以让 `rsync` 使用硬链接来节省空间：

```bash
$ rsync -avz --delete --link-dest=/path/to/previous/backup/ /source/dir/ /destination/dir/
```

## 第 8 章：备份与可移动介质

如果你信任 `unison`，可以使用 `-auto` 让它执行默认操作而无需提示你：

```
$ unison /home/francois ssh://francois@server1//home/fcaen -auto
```

`unison` 没有对应的页面。不过，你可以通过 `-help` 选项查看 `unison` 选项。在 `/usr/local/share/doc/unison` 中有一个手册。你也可以像这里使用 `-doc all` 选项显示并解析 `unison` 手册：

```
$ unison -help                查看 unison 选项
$ unison -doc all | less      显示 unison 手册
```

如果你发现经常同步根目录，可以创建一个配置文件（profile），它是一系列预设。在图形模式下，默认屏幕会让你创建配置文件。配置文件存储在 `~/.unison` 目录下的 `.prf` 文件中。它们可以如下：

```
root = /home/francois
root = ssh://francois@server1//home/fcaen
```

如果这些内容存储在 `fc-home.prf` 配置中，你可以直接通过以下命令行调用它：

```
$ unison fc-home
```

## 备份到可移动介质

CD 和 DVD 的容量以及这种介质的低成本，使其成为计算机备份介质的理想选择。使用 BSD 系统自带的工具，你可以将要备份的文件收集成 CD 或 DVD 镜像，并将其刻到相应的介质上。

诸如 `mkisofs`（创建 CD 镜像）和 `cdrecord`（将镜像刻录到 CD 或 DVD）等命令行工具都有许多图形界面，你也可以考虑它们。例如，用于刻录和刻录 CD/DVD 的 GUI 工具包括 K3b（KDE CD 和 DVD 制作器）和 Nautilus（GNOME 文件管理器，提供 CD 刻录功能）。其他用于刻录 CD 的 GUI 工具包括 combust、X-CD-Roast 和 graveman。

本节将描述用于创建文件系统镜像以备份到 CD 或 DVD 的命令，以及如何刻录这些镜像的命令。要获取 `mkisofs` 和 `cdrecord` 命令，你需要安装 `cdtools` 软件包（`pkg_add -r cdtools`）。

## 使用 mkisosfs 创建备份镜像

大多数 CD 和 DVD 可以在 Windows 和 BSD 系统上访问，因为它们是使用 ISO9660 标准格式化磁盘信息的。由于大多数现代操作系统需要保存比 ISO9660 标准包含更多的文件和目录信息，因此在该标准基础上了扩展以包含这些信息。

使用 `mkisosfs` 命令，你可以从 BSD 文件系统的任何位置备份文件和目录结构，并生成 ISO9660 镜像。该镜像可以包含以下类型的扩展：

- 系统共享协议 (SUSP)：Rock Ridge 交换协议（Rock Ridge Interchange Protocol）识别的记录。SUSP 记录可以包含 UNIX 风格的属性，如所有者、长文件名和特殊文件（如字符设备和符号链接）。
- Joliet 记录以 Windows 系统可用的格式存储较长的文件名。
- 分级文件系统 (HFS) 扩展允许 ISO 镜像显示为 HFS 文件系统，这是麦金（Macintosh）电脑的原生文件系统。同样，还可以以不同的读取方式添加数据分叉（Data forks）和资源分叉（Resources forks）。

当你准备创建 ISO 镜像时，请考虑你最终将在何种系统上访问使用 `mkisosfs` 备份的文件（BSD、Linux、Windows 或 Mac）。你创建的镜像可以通过多种方式制作，最明显的方法是将镜像刻录到 CD 或 DVD。

除了可以用于生成 BSD 文件系统的全部部分并在便携介质上使用外，`mkisosfs` 对于创建启动型 CD/DVD 也很有用。它通过向镜像中添加启动信息，可以启动 BSD 内核或其他操作系统，从而跳过计算机的硬盘。

由于大多数 BSD 用户将个人文件存储在主目录中，使用 `mkisosfs` 备份文件的一种常用方法是备份 `/home` 目录下的所有内容。以下是使用 `mkisosfs` 为 `/home` 目录下所有文件和目录创建镜像的示例：

```bash
# cd /tmp
# mkisosfs -o home.iso /home              创建基础 ISO9660 镜像
# mkisosfs -o home2.iso -J -R /home         添加 Joliet Rock Ridge 扩展
# mkisosfs -o home3.iso -J -R -hfs /home     同时也添加 HFS 扩展
```

在上述三个示例中，表示 `/home` 目录的文件和目录都被添加到 ISO 镜像中。第一个示例没有扩展，因此所有文件名都会转换为 DOS 风格命名（8.3 字符）。第二个示例使用了 Joliet 和 Rock Ridge 扩展，因此当你在 BSD、Linux 或 Windows 系统上打开 ISO 时，文件名和权限应该与它们在原始 BSD 系统上显示的一样。最后一个示例还使镜像上的文件可以在 Mac 文件系统中被读取。

你可以向镜像中添加多个源。以下是一些示例：

```bash
# mkisofs -o home.iso -R -J music/ docs/ \ 多个目录/文件
chris.pdf /var/spool/mines\
# mkisofs -o home.iso -J -R \ # 将文件挂接到镜像
graft-points Points=/var/pics/ \
/home/chris
```

第一个示例显示将各种文件和目录组合并放置在 ISO 镜像的根目录下。第二个示例将 `/var/pics/` 目录的内容挂载到 `/home/chris` 中。

## 第8 章：备份与可移动介质

在开始将镜像刻录到 CD 或 DVD 之前，请您的驱动器是否支持 CD/DVD 刻录并确定驱动器的地址。使用 `--cdscan` 选项记录执行该操作的命令：

```
# cdrecord --cdscan
scbus0:
  0,0, 0) 'SAMSUNG' 'DVD-ROM SD-616E' 'F503' Removable CD-RCM
  0,0, 1) *
  0,0, 2) *

# cdrecord --cdscan
scbus0:
  0,0, 0) 'LITE-ON' 'DVDWR SOHW-1633S' 'BSOC' Removable CD-ROM
```



`0,0, 1)`

`0,0, 2)`

在所示的两个示例中，`CD/DVD`驱动器仅读取而不能刻录`CD`（`DVD-ROM`和`CD-ROM`）。第二个示例显示了一个可以刻录`CD`或`DVD`的驱动器（`DVDWR`）。插入您想要刻录的介质。由于您的驱动器与介质匹配，这里是一些刻录`CD`或`DVD`介质的`cdrecord`命令：

```
# cdrecord --blank-fast ...
# cdrecord -v home.iso ...
# cdrecord -v e speed-d2 home.iso ...
# cdrecord -pad home.iso ...
# cdrecord -eject/dev/cdrom.iso...
# cdrecord dev0,2,home.iso
```

`cdrecord`命令可以刻录多会话`CD/DVD`。以下是一个示例：

```
# cdrecord --multi home.iso
# cdrecord -mininfo
  /dev/cdrom of unknown partitions \
  0/93041
# mkisofs -J -R o new.iso \
  -C 0,93041 /home/chris/more
# cdrecord new.iso
```

您可以使用多次`-multi`刻录直到`CD`填满。对于最后一次刻录，不要使用`-multi`，这样`CD`将

## 使用 `growisofs` 制作并刻录 `DVD`

使用`growisofs`命令，您可以将收集文件到`ISO`镜像（`mkisofs`）以及将该镜像刻录到`DVD`（`cdrecord`）这两个阶段结合起来。通过简化步骤，`growisofs`命令还具有默认保持会话开启直到您将其关闭的优势，因此您不需要对多次刻录会话进行任何特殊操作。

以下是多会话的`growisofs`命令示例：

```
# growisofs -Z /dev/cd0 -R -J /home/chris    制作并刻录到 DVD
# growisofs -Z /dev/cd0 -R -J /home/francois  添加并刻录
# growisofs -M /dev/cd0/zero               关闭刻录
```

如果您想在创建`ISO`镜像时添加选项，只需将`mkisofs`添加到命令中。（例如，参见上述示例中如何添加`-R`和`-J`选项。）

如果您想使用`growisofs`刻录`DVD`镜像，可以使用`-dvd-compat`选项。这里是一个示例：

```
# growisofs -dvd-compat -Z /dev/cd0-image.iso 将 ISO 镜像刻录到 DVD
```

在某些多会话`DVD`刻录过程中，`-dvd-compat`选项可以提高与不同`DVD`驱动器的兼容性。

## 总结

`BSD`及其之前的`UNIX`系统通过组合处理离散功能的命令来处理数据备份。您的关键数据备份仍然可以通过这种方式进行。事实上，您使用的许多工具将比以前任何时候都更安全、高效。

磁带归档实用（`tar`命令）已经远远超出了其制作数据文件磁带备份的原始工作。由于几乎每个`BSD`、`Linux`和`UNIX`系统都使用`tar`，它已成为软件包打包和数据压缩归档的标准工具。这些归档随后可以通过多种方式传输和存储。

要通过网络将数据传回其他机器，您可以使用`OpenSSH`工具的执行功能（如`ssh`）。您还可以使用一个名为`rsync`的优秀工具。通过`rsync`，您可以通过只备份已更改的文件（或文件的部分）来节省资源。

廉价的`CD`和`DVD`让这些介质在个人和小办公室备份中流行起来。`mkisofs`命令可以创建`ISO9660`格式的备份数据文件，可以在多种系统（`BSD`、`Linux`、`Windows`或`Mac`）上恢复。在`mkisofs`命令创建`ISO`镜像后，可以使用`cdrecord`和`growisofs`命令将镜像刻录到`CD`或`DVD`。

## 查看和管理运行进程

当一个可执行程序启动时，它作为一个受您的`BSD`系统进程表管理的进程在运行。每个`BSD`系统都提供了查看和更改系统上运行进程所需的所有工具。

`ps`和`top`命令是查看运行中进程信息的绝佳工具。`ps`和`top`实际上有几十个选项可以帮助您按照想要的方式处理信息。`pgrep`命令可以进一步帮助找到您所需的进程。

有诸如`nice`和`renice`等命令用于提高或降低进程的处理器优先级。您可以将进程移动到后台运行（`bg`命令）或返回前台（`fg`命令）。

向进程发送信号是改变其行为或彻底杀死它的方法。通过使用`kill`和`killall`命令，您可以分别通过`PID`或名称发送信号。您还可以向进程发送其他信号来执行操作，如重新读取配置文件或继续已停止的进程。要在调度时间运行命令，可以使用`cron`。要重复运行命令，可以使用`batch`。

### 使用 `ps` 和 `top` 查看活动进程

要查看系统当前运行哪些进程，大多数人使用`ps`和`top`。`ps`命令提供了当前运行进程的快照。`top`命令提供了按`CPU`、`I/O`等排序的持续更新列表。要看到所有输出，您需要在`/etc/fstab`中添加以下行：

```
proc
```

然后输入以下命令（如`Linux`）：

```
mount /proc
```

每个系统（如`UNIX`）都包含了`ps`命令。多年来出现了不同的版本，提供了不同的选项（例如，允许在某些情况下删除）。`ps`在`FreeBSD`、`OpenBSD`和大多数其他系统中工作。这里是当前用户的进程示例：

| PID | STAT | TIME | COMMAND |
| --- | --- | --- | --- |
| 1132 | ? | 00:06 | `sshd@tty0` |
| 810 | I+ | 00:09 | `-sh (sh)` |
| 1117 | I+ | 00:05 | `-sh (sh)` |
| 1133 | Ss | 00:03 | `-sh (sh)` |
| 1211 | R+ | 00:00 | |

| USER | PID | %CPU | %MEM | VZ | STAT | TIME | COMMAND |
| --- | --- | --- | --- | --- | --- | --- | --- |
| `chris` | 1132 | 0.0 | 0.0 | 6352 | 3312 | S | 4:52PM | 00:03 |
| `chris` | 810 | 0.0 | 0.6 | 1752 | 1400 | I+ | 3:00PM | 00:09 |
| `chris` | 1117 | 0.0 | 0.6 | 1752 | 1396 | I+ | 4:45PM | 00:05 |
| `chris` | 1133 | 0.0 | 0.6 | 1756 | 1396 | S | 4:52PM | 00:03 |
| `chris` | 1204 | 0.0 | 0.4 | 1460 | 1036 | R+ | 5:07PM | 00:00 |

`$ ps -fu chris`显示`chris`的运行进程（带有`PID`）

| PID | STAT | TIME | COMMAND |
| --- | --- | --- | --- |
| 1132 | ? | 00:06 | `sshd: chris:ttyp0 (sshd)` |
| 810 | I+ | 00:09 | `-sh (sh)` |
| 1117 | I+ | 00:05 | `-sh (sh)` |
| 1133 | Ss | 00:03 | `-sh (sh)` |
| 1211 | R+ | 00:00 | |

`$ ps -ps vu`显示所有运行进程（带有`SL`和`RE`）

| PID | STAT | TIME | RE | PAGE | VZ | RSS | MEM | LIMSI | %CPU | %MEM | COMMAND |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1132 | S | 00:00:16 | 0 | 127 | 6252 | 3312 | 168 | 0.0 | 1.3 | `sshd: chris` |
| 810 | I+ | 00:00:29 | 0 | 127 | 1756 | 1400 | 100 | 0.0 | 0.6 | `-sh (sh)` |
| 1133 | Ss | 00:00:08 | 0 | 127 | 1756 | 1400 | 100 | 0.0 | 0.6 | `-sh (sh)` |
| 1244 | I+ | 00:00:47 | 0 | 70 | 1752 | 1392 | 100 | 0.0 | 0.6 | `-sh (sh)` |
| 1264 | R+ | 00:00:01 | 0 | 0 | 1460 | 1044 | 24 | 0.4 | `ps -vu` |

`$ ps -aux`显示所有运行进程，长`BSD`样式，显示每个运行进程，长`BSD`样式，无限制

`$ ps -auwx`显示所有运行进程，长`BSD`样式，宽格式，显示每个运行进程，长`BSD`样式，无限制

# 第 9 章：检查和管理运行进程

如果你想查看`ps`条目的完整输出，之前的两个命令将非常有用。如果输出超过了你的列宽，它将换行而不是截断。

某些进程会启动其他进程。例如，`Web`服务器（`http`守护进程）会产生多个`httpd`守护进程来等待来自服务器的请求。你可以使用`pstree`命令查看进程层次结构（树状视图）（以`root`身份运行，输入`pkg_add -r pstree`进行安装）：

```
$ pstree 以树状格式按字母顺序显示进程
+= 00000 root [swapper]
|-- 00001 root /sbin/init
|   |-- 01121 root adjkertnz -i
||-- 00739 root /usr/bin/sshd
| \+ 01129 root sshd: chris [priv] (sshd)
| |\- 01132 chris sshd: chris@ttyp0 (sshd)
|   |\- 01133 chris -sh (sh)
|     \+ 01999 chris pstree
|       \-+ 02000 chris ps -c -awxo user.pid,ppid,pgid,command
|       \-+ 02001 chris ps -awxo user.pid,ppid,pgid,command
```

“树”示例仅说明了显示进程层次结构的另一种方式。`ssh`进程显示了一个正在运行的、通过网络登录的用户安全守护进程（Secure Daemon），导致了一个`bash` shell（以及最终的`ps`命令）。

如果你更倾向于`ps`输出的个性化视图，可以使用`-o`选项精确地选择要显示哪些数据列。表 9-1 显示了可用的列输出以及添加到`-o`的选项，以便用`ps`打印每一列。

### 表 9-1：选择和查看 `ps` 列输出

| 选项 | 列标题 | 描述 |
|---|---|---|
| `%cpu` | `%CPU` | `CPU` 使用百分比 |
| `%mem` | `%MEM` | 内存使用百分比 |
| `acflag` | `ACFLAG` | 计费标志 |
| `args` | `COMMAND` | 命令和参数 |
| `comm` | `COMMAND` | 仅命令 |
| `command` | `COMMAND` | 命令和参数（与 `args` 相同） |
| `cpu` | `CPU` | 短期 `CPU` 使用因子（用于调度） |
| `etime` | `ELAPSED` | 运行已时间 |
| `flags` | `F` | 进程标志，十六进制（与 `f` 相同） |
| `inblk` | `INBLK` | 总读取块数（与 `inblock` 相同） |
| `jid` | `JID` | Jail ID |
| `jobc` | `JOBC` | 作业控制计数 |
| `ktrace` | `KTRACE` | 跟踪标志 |
| `label` | `LABEL` | MAC 标签 |
| `lim` | `LIM` | 内存使用限制 |
| `lockname` | `LOCK` | 当前阻塞的锁（作为符号名称） |
| `logname` | `LOGIN` | 启动会话的用户登录 |
| `Istart` | `STARTED` | 开始时间 |
| `majflt` | `MAJFLT` | 总页异常 |
| `minflt` | `MINFLT` | 总页请求 |
| `msgrcv` | `MSGRCV` | 总接收消息数（管道/socket 读取） |
| `msgsnd` | `MSGSND` | 总发送消息数（管道/socket 写入） |
| `mwchan` | `MWCHAN` | 当前阻塞的等待通道或锁 |
| `nice` | `NI` | Nice 值（与 `ni` 相同） |
| `nivscw` | `NIVCSW` | 总非自愿上下文切换 |
| `nsigs` | `NSIGS` | 总处理信号（与 `nssignals` 相同） |
| `nswap` | `NSWAP` | 总交换换出次数 |
| `nvcsw` | `NVCSW` | 总自愿上下文切换 |
| `nwchan` | `NWCHAN` | 等待通道（作为地址） |
| `oublk` | `OUBLK` | 总写入块数（与 `oublock` 相同） |
| `paddr` | `PADDR` | 交换地址 |
| `pagein` | `PAGEIN` | 页（与 `majflt` 相同） |
| `pgid` | `PGID` | 进程组号 |
| `pid` | `PID` | 进程 ID |
| `ppid` | `PPID` | 父进程 ID |
| `pri` | `PRI` | 调度优先级 |
| `re` | `RE` | 核心驻留时间（秒）（127 表示无穷） |
| `rgid` | `RGID` | 真实组 ID |
| `rgroup` | `RGROUP` | 组名（与真实组 ID 关联） |
| `rss` | `RSS` | 驻留集大小 |
| `rtprio` | `RTPRIO` | 实时优先级（101 表示不是实时进程） |
| `ruid` | `RUID` | 用户 ID |
| `ruser` | `RUSER` | 用户（与真实用户 ID 关联） |
| `sid` | `SID` | 会话 ID |
| `sig` | `PENDING` | 等待信号（与 `pending` 相同） |
| `sigcatch` | `CAUGHT` | 已捕获的信号（与 `caught` 相同） |
| `signignore` | `IGNORED` | 忽略的信号（与 `ignored` 相同） |
| `sigmask` | `BLOCKED` | 阻塞的信号（与 `blocked` 相同） |
| `sl` | `SL` | 睡眠时间（秒）（127 表示无穷） |
| `start` | `STARTED` | 开始时间 |
| `state` | `STAT` | 符号进程状态（与 `stat` 相同） |
| `svgid` | `SVGID` | 从集合中保存的 gid |
| `svuid` | `SVUID` | 从集合中保存的 UID |
| `tdev` | `TDEV` | 控制终端设备 |
| `time` | `TIME` | 累计 `CPU` 时间，系统（与 `cputime` 相同） |
| `tsid` | `TSID` | 控制会话 ID |
| `tsize` | `TSIZ` | 文本大小（字节） |
| `tt` | `TT` | 控制终端名称，缩写 |
| `tty` | `TTY` | 控制终端全名 |
| `uprocp` | `UPROCP` | 进程指针 |
| `ucomm` | `UCOMM` | 用于计数的名称 |
| `uid` | `UID` | 有效用户 ID |
| `upr` | `UPR` | 调度优先级（与 `uspr` 相同） |
| `user` | `USER` | 用户名（来自用户） |
| `vsz` | `VSZ` | 虚拟大小（字节） |
| `wchan` | `WCHAN` | 等待通道（符号名称） |
| `xstat` | `XSTAT` | 退出或停止状态（僵尸进程） |

注意某些值如果名称太长将以数字形式打印。要查看数值，请使用`ps -L`选项。

使用逗号分隔的列表，例如`pid,mem,comm`，可以产生自定义输出。以下是运行进程的一些自定义视图示例：

```
$ ps -ko pid,user,comm 显示进程 ID，内存，等。
PID USER %MEM TSIZ VSZ
1129 chris 1.38 6252

$ ps -ko pid,user,start,time,%cpu 显示 PID，启动时间，时间，等。
PID USER STARTED %CPU
1129 chris 4:52 0.08 chris@ttyp0
```

```
$ ps -xo puser,nice,cutime,args 显示用户，nice，时间，参数。
PPID NI TIME
1129 chris 0 00:00:84 chris:ttyp0

$ ps -xo puser,stat,tty,sid,etime 显示 PID，用户，终端，等。
PPID USER STAT ELAPSED
1129 chris S ?06:39:23 chris:ttyp0
```

以下是`ps`命令的几个示例：

```
$ ps -aux -r | less 按 CPU 使用率排序
USER %CPU %MEM VSS RS TT TIME
root 10.7 4.0 8 ? RL 3:30PM 503:12.85 [idle]
root 2551 7.8 1384 916 V3 R 11:55PM 02:02.50 find
root 4 1.0 8 ? DL 3:30PM 00:08.73 [g_down]

$ ps -l tty 按内存使用率排序
USER %CPU %MEM VSS RS TT STAT
root 1307 0.0 1.2 4928 3004 I 5:31PM 00:05.58 -csh (csh)
```



`root 745 0.0 1 3510 2804 ?? SS 3:30PM 02:01.04 mailsend.`

```
$ ps 显示 tty 进程

PID STAT COMMAND

1133 S 00:00:38 -sh (sh)

2595 R 00:00:00 -t tty0

$ ps -p 1129 -o pid,tty,time,args 显示 PID 1129 的信息

PID TTY TIME COMMAND

1129 chris 07:00:08 chris:chriv (sshd)

$ ps -U chris,francis -o pid,tty,stat,args 查看两个用户的信息

PID USER TTY STAT COMMAND

1132 chris ? S sshd: chris:ttyp0 (sshd)

2480 chris ?? S sshd: chris:ttyp1 (sshd)
```

## 使用 top 监控进程

如果你想持续查看运行中的进程，可以使用 `top` 命令。`top` 命令运行一个面向屏幕的运行进程视图并持续更新。如果你在不带任何选项的情况下使用 `top` 命令，它将显示系统的运行时间、任务、`CPU` 使用率和内存使用情况，随后是按使用率排序的运行进程列表。这是一个示例：

```
$ top

last pid: 2697; load averages: 0.04, 0.03, 0.00  up 00:48:44

00:14:17

58 processes: 1 running, 57 sleeping

cpu states: 0.0% user, 0.0% nice, 0.8% system, 0.0% interrupt, 99.2% idle

Mem: 58M Active, 97M M, 73M Wired, 12M Cache, 34M Buf, 1508 Free

Swap: 484M Total, 484M Free

PID USER THR NI SIZE RES STAT TIME WCPU COMMAND

2696 chris 1 96 02532K 15520K select 0:03 2.05% gtiali

2618 chris 1 96 08392K 14300K select 0:03 0.00% Xorg

2652 chris 3 20 034244K 31506K kresel 0:07 0.00% nautilus

2650 chris 1 96 026564K 16688K select 0:04 0.00% gnome-panel
```

# 第 9 章：检查和管理运行中的进程

以下是你可以使用的其他选项，用于启动 `top` 以持续显示运行中的进程：

- `$ top -s 5` 将更新延迟更改为 5 秒（从 3 秒改为）
- `$ top -u francois` 仅显示有效用户名为 `francois` 的进程
- `$ top -s` 显示系统进程以及其他进程
- `$ top -d 10` 在退出前刷新屏幕 10 次
- `$ top -b` 以非交互式、非屏幕导向的批模式运行

此 `top -b` 示例将 `top` 的输出格式化为适合输出到文件的形式，而不是在屏幕上重绘相同的屏幕以进行交互式查看。这可以用于创建进程日志，例如，在半夜寻找耗尽你所有资源的进程时。以下是运行 `top` 并记录 10 分钟输出的方法：

- `$ top -b -d 12000 > myprocesslog`

当 `top` 运行时，你可以通过不同的方式更新和排序进程列表。要立即更新进程列表，按 `Space` 按 `CPU` 和加权 `CPU` 时间进行排序。按 `I` 隐藏空闲进程或显示它们。或者，按 `m` 在 `CPU` 和 `IO` 模式之间切换。在 `IO` 模式下，按 `o` 选择数据排序的顺序。

有几种方法可以在 `top` 运行时更改其行为。按 `s` 并输入代表秒的类型来更改刷新的延迟。按 `u` 输入用户名以仅显示所选用户的进程。按 `Ctrl-L` 重新绘制屏幕。

你可以以不同的方式对任何运行中的进程进行操作。要向运行中的进程发送信号（杀死进程），输入 `k` 然后输入你想要发送信号的进程的 `PID`。这将发送默认的 `15 (TERM)`，允许进程以有序的方式关闭。要给予更高的或更低的运行优先级，输入 `r` 然后添加一个负数（增加优先级）或正数（降低优先级），最后加上你想更改的进程 ID。

如果你想找到更多关于如何使用 `top` 的信息，可以在 `top` 会话期间输入 `?`。主页有很多关于如何使用 `top` 的信息：

```
$ man top 查看 top 的 man 页面
```

当你使用 `top` 时，输入 `q` 退出。

## 查找和控制进程

更改进程首先意味着找到你想更改的进程，然后修改其处理优先级或发送信号来改变其行为。如果你在寻找某个特定的进程，你可能会在 `ps` 或 `top` 输出的大型进程列表中找到并定位它。`pgrep` 命令提供了在活动进程中搜索你正在寻找的进程的方法。`renice` 命令允许你更改运行中进程的处理优先级。`kill`、`pkill` 和 `killall` 命令允许你向运行中的进程发送信号（包括结束这些进程的信号）。

# 使用 pgrep 查找进程

在最基本的形式中，你使用 `pgrep` 搜索命令（或命令的一部分），并产生包含该名称的任何进程的进程 ID。例如：

```
$ pgrep init

显示包含 'init' 字符串的任何进程的 PID

2617

1
```

由于我们知道只有一个 `init` 进程在运行，我们使用 `-l` 选项来查看每个进程的命令名称（以了解哪些进程出现了）：

```
$ pgrep -l init

显示包含 'init' 的任何进程的 PID 和名称

2617

1 init
```

你也可以搜索与特定用户相关的进程：

```
$ pgrep -lu chris

列出所有用户 chris 拥有的进程

2803 vim

2552 bash

2551 sshd
```

使用 `pgrep` 最有用方法可能是找到运行中进程的进程 ID，并将这些 `PID` 管道到另一个命令以产生输出。以下是示例（寻找其他如 `metacity` 或 `firefox` 未运行的命令）：

```
$ ps -p 'pgrep metacity'

搜索 metacity 并运行 ps (短格式)

PID TID STAT COMMAND

2617 ? S 00:07:02 /usr/local/bin/metacity --sm-client-id=default0

$ ps -f 'pgrep init'

搜索 init 并运行 ps (全格式)

PID TID STAT COMMAND

2617 v2 I+ 00:01 /usr/X16/bin/home/.initrc

$ renice -5 'pgrep firefox'

搜索 firefox，提高其优先级

2052:旧优先级 0, 新优先级 -5

2057:旧优先级 0, 新优先级 -5
```

任何可以接受进程 ID 作为输入的命令都可以以这些方式与 `pgrep` 结合。正如前面的 `pgrep` 示例所示，你可以使用 `renice` 等命令来更改进程在运行时的行为。

# 使用 fuser 查找进程

定位特定进程另一种方法是根据进程正在访问的内容。`fuser` 命令（作为 `root`，输入 `pkg_add -r fuser`）可用于查找当前哪些进程打开了文件或套接字。找到进程后，可以使用 `fuser` 向这些进程发送信号。`fuser` 命令最有用用于查找哪些文件被挂载文件系统（如硬盘或 `Samba` 共享）上的进程打开。找到这些进程允许你正确地关闭它们（如果必须，则直接杀死它们），以便卸载文件系统。以下是 `fuser` 命令的某些示例，用于列出在选系统中打开了文件的进程：

```
# fuser -cu /home 输出打开 /home 的进程（带用户名）

...（此处省略具体输出，原文逻辑保持一致）
```

# 第 9 章：检查和管理运行进程

在下面的命令序列中，我们从终端窗口启动了 `GIMP` 图像程序。随后有一系列控制键和命令用于停止、启动进程，以及将其在前台和后台之间移动：

```
$ gimp                在前台运行 gimp

<Ctrl+Z>            停止进程并将其放入后台

[1]+ Stopped        gimp

$ bg 1             在后台重新启动运行进程 (bash)

$ bg %1             在后台重新启动运行进程 (sh)

$ fg 1              在前台继续运行进程 (bash)

$ fg %1             在前台继续运行进程 (sh)

gimp

<Ctrl+C>            杀死进程
```

请注意，放置在后台的进程带有一个作业 ID（`job ID`）符号及其对应的数字（例如 `%1`），你可以通过 `bg` 和 `fg` 命令或通过 `shell` 来识别特定的进程；在命令中输入该数字（如 `fg 1`）。当当前 `shell` 运行一个或多个后台作业时，你可以使用该命令来管理正在运行的作业：

```
$ jobs             显示当前 shell 的后台作业

[1] Running         gimp &

[2] Running         xmms &

[3]- Running         gedit &

[4]+ Stopped         gtali

$ jobs -1 %2       显示每个作业信息并包含 PID

[1] 31676 Running      gimp &

[2] 31677 Running      xmms &

[3]- 31683 Running     gedit &

[4]+ 31688 Stopped     gtali

                      仅显示作业 %2 的信息

                      xmms &
```

在 `jobs` 中运行的进程可能是你在登录（`ssh`）远程系统时完成的，但你想在本地桌面上运行 `GUI` 应用。通过在后台运行这些进程，你可以同时运行多个应用程序，同时保持它们与当前 `shell` 关联。

> 注意：使用 `fg` 或 `bg` 时，如果没有指定要操作哪个进程，将使用当前作业。当前作业旁边有一个加号 (`+`)。

`fg` 和 `bg` 命令通过将进程移动到前台或后台来手动操作运行中的进程。另一种操作运行命令的方法是直接向这些进程发送信号。向运行进程发送信号的一种常用方法是使用 `kill` 和 `killall` 命令。

## 杀死和信号进程

你可以通过向进程发送信号来停止或更改运行中的进程。`kill` 和 `killall` 命令可以向运行的进程发送你选择的信号，正如其名称所示，这通常是杀死进程的信号。

信号由数字（`9`、`15` 等）和字符串（`SIGKILL`、`SIGTERM` 等）表示。表 9-2 显示了你可以向 `BSD` 系统中的进程发送的标准信号。

### 表 9-2：发送给进程的标准信号

| 信号数字 | 信号名称 | 描述 |
|---|---|---|
| 1 | `SIGHUP` | 终端挂断或控制进程死亡 |
| 2 | `SIGINT` | 中断程序 |
| 3 | `SIGQUIT` | 退出程序 |
| 4 | `SIGILL` | 非法指令 |
| 5 | `SIGTRAP` | 跟踪陷阱 |
| 6 | `SIGABRT` | 从 `abort` 函数发送的终止 |
| 7 | `SIGEMT` | 执行了模拟指令 |
| 8 | `SIGFPE` | 浮点数异常 |
| 9 | `SIGKILL` | 杀死信号 |
| 10 | `SIGBUS` | 总线错误 |
| 11 | `SIGSEGV` | 段违规 |
| 12 | `SIGSYS` | 调用了不存在的系统调用 |
| 13 | `SIGPIPE` | 管道破（无可读或写） |
| 14 | `SIGALRM` | 来自闹系统调用的信号 |
| 15 | `SIGTERM` | 终止信号 |
| 16 | `SIGURG` | 丢弃信号 |
| 17 | `SIGSTOP` | 停止进程 |
| 18 | `SIGTSTP` | 在终端输入的停止 |
| 19 | `SIGCONT` | 如果进程已停止则继续 |
| 20 | `SIGCHLD` | 子进程状态改变 |
| 21 | `SIGTTIN` | 终端尝试读取后台进程 |
| 22 | `SIGTTO` | 终端尝试向后台进程写入 |

`kill` 命令可以通过 ID 或作业号向进程发送信号，而 `killall` 命令可以根据命令名称向进程发送。以下是一些示例：

```
$ kill 28665

$ kill - 4895

$ kill -SIGCONT 5254

$ kill %3

$ killall spamd

$ killall -SIGHUP sendmail
```

向 `PID` 为 `28665` 的进程发送 `SIGTERM`
向 `PID` 为 `4895` 的进程发送 `SIGKILL`
继续已停止的进程 (`pid` `5254`)
杀死作业 `#3` 代表的进程
杀死当前运行的所有守护进程
让 `sendmail` 进程重新读取配置文件

`SIGKILL` (`9`) 信号通常被热衷于触发信号的管理员使用，应保留作为最后的手段。它不允许进程整洁地退出。这可能会导致该进程处理的数据丢失或损坏。`SIGKILL` 原本用于 `UNIX` 系统，表示终端与主机断开（例如拨号调制调器挂起）。然而，`sendmail` 和 `httpd` 等守护进程被实现为捕获 `SIGKILL`。

## 离开当前 shell 运行进程

如果你希望进程即使在断开连接后也运行，有几种方法可以。`at` 和 `batch` 命令用于队列命令。在这里：

```
$ at now             启动一个命令

mycript. &
```

`at` 和 `batch` 命令使用次级 `at` 提示符。在该提示符处输入你想运行的命令。之后你可以输入命令。完成后，单独占一行按 `Ctrl+D` 来队列命令。

```
$ at now +5             在 5 天后启动命令
```

`at` 和 `batch` 命令用于一次性任务。这些命令被编写进 `cron` 作业，并在 `crontab` 文件中进行调度。有一个系统级 `crontab` 文件 (`/etc/crontab`)。此外，每个用户都可以按照自己选择的时间创建个人 `crontab`。要创建个人 `crontab`，输入以下内容：

```
$ crontab -e             创建个人 crontab 文件
```

`crontab -e` 命令使用 `vi` 编辑器打开你的 `crontab` 文件（或创建一个新的）。以下是可以添加到 `crontab` 的几个条目示例：

```
15 8 * * Mon,Tue,Wed,Thu,Fri mail < /var/project/stats.txt

* * 1,4,7,10 * find / | grep .doc $ > /var/sales/documents.txt
```



# 第 9 章：检查和管理运行进程

`crontab` 条目的最后部分是要运行的命令。前五个字段代表执行命令的时间和日期。从左到右的字段分别是：分钟（0 到 59）、小时（0 到 23）、日期（0 到 31）、月份（0 到 12，或 `Jan`, `Feb`, `Mar`, `Apr`, `May`, `Jun`, `Jul`, `Aug`, `Sep`, `Oct`, `Nov`, `Dec`）以及星期（0 到 7，或 `Sun`, `Mon`, `Tue`, `Wed`, `Thu`, `Fri`, `Sat`）。字段中的星号（`*`）表示该字段的任何值。

以下是使用 `crontab` 命令的其他选项：

```
# crontab -eu chris 编辑另一个用户的 crontab (仅限 root 用户)

$ crontab -l             列出你的 crontab 的文件内容

15 8 * * Mon, Tue, Wed, Thu, Fri mail < /var/project/stats.txt

* * 1,4,7,10 * find | grep .doc > /var/sales/documents.txt

$ crontab -r 删除你的 crontab 文件
```

第一个 `crontab` 示例通过将 `/var/project/stats.txt` 的内容重定向到消息中，向名为 `chris` 的用户发送消息。`mail` 命令在周日至周五上午 8:15 运行。在第二个示例中，每年的 1、4、7、10 月的第一天，运行 `find` 命令查找 `/` 下每个 `.doc` 文件，并将生成的文件列表发送到 `/var/sales/documents.txt`。

`cron` 的替代方案是 `anacron`（`pkg_add -r anacron`）。使用 `anacron`，你可以像 `cron` 一样配置定期运行的命令。然而，`anacron` 最适用于并非全天运行的机器。如果计算机在计划时间内处于关机状态，当下次计算机开启时，`anacron` 会确保在关机期间错过的命令在系统恢复后运行。

## 总结

监控和处理在你的 `BSD` 系统上运行的进程是确保系统高效运行的重要活动。通过使用 `ps` 和 `top` 等命令，你可以查看系统上运行的进程。你还可以使用 `pgrep` 来搜索特定的进程列表。

通过 `nice` 和 `renice` 等命令，你可以调整所选进程运行时的建议优先级。当进程运行时，你可以通过 `kill` 或 `killall` 命令向其发送信号来改变其运行方式或杀死进程。

从当前 `shell` 启动命令后，你可以将该命令进程设置为后台（`bg`）或前台（`fg`）运行。你还可以使用控制代码停止并重启进程。

要调度命令在稍后运行，你可以使用 `at` 或 `batch` 命令。要设置命令定期间隔运行，你可以使用 `cron` 或 `anacron`。

# 第 10 章：系统管理

如果没有仔细的管理，对 `BSD` 系统的需求有时会超过你可用的资源。随时间监控系统的活动（内存、`CPU` 和设备使用情况）有助于确保你的机器有足够的资源来完成你的需求。同样，管理系统的其他方面，如它使用的设备驱动程序以及启动过程的工作原理，有助于避免问题和系统故障。

本章内容：
- 使用 `top` 和 `vmstat` 检查内存使用情况
- 使用 `iostat`、`sysstat` 和 `top` 查看 `CPU` 使用情况
- 使用 `iostat`、`gstat` 和 `lsof` 监控存储设备
- 使用 `date`、`cal` 和 `NTP` 处理日期/时间
- 修改引导加载程序的行为
- 切换到 `GRUB` 引导加载
- 使用 `reboot`、`halt` 和 `shutdown` 关闭系统
- 使用 `kstat`、`kunload` 和 `kload` 检查并更改内核驱动程序
- 使用 `isci` 和 `dmidecode` 观察硬件设置

本章分为几个与管理 `FreeBSD` 或其他 `BSD` 系统方法的相关部分。第一部分可以帮助你监控 `BSD` 系统上的资源（处理能力、设备和内存）。下一部分描述了如何检查和设置你的系统时。随后是关于启动过程和后续运行级别的描述。最后的部分描述了如何处理内核和相关的设备驱动程序，以及如何查看计算机硬件组件的信息。

## 监控资源

`FreeBSD`、`OpenBSD`、`NetBSD` 以及其他 `Unix` 类系统在跟踪自身运行情况方面做得非常好。如果你感兴趣，可以找到许多关于你的 `CPU`、硬盘、虚拟内存和其他计算机资源如何被使用的大量信息。

你可以使用命令来查看系统上虚拟内存、处理器、存储设备和网络接口的使用情况。有些命令可以监控系统资源的几个不同方面。然而，由于本书不仅仅是一份手册帮助页（`man page`），我们按照主题（监控内存、`CPU`、存储设备）而不是按命令（`top`、`vmstat` 和 `iostat`）来划分章节。

注意：本节中的许多应用程序在 `FreeBSD` 中是默认安装的。要使用收集系统活动历史的命令（例如 `sar`），你需要安装该软件包或从源码编译。

### 内存使用

没有什么比内存溢出更快杀死性能了。诸如 `top` 等命令可以获取有关 `RAM` 和交换空间使用情况的信息。`vmstat` 命令提供有关内存使用的信息并可以持续运行。`top` 命令提供了查看当前运行进程的手段，并按 `CPU` 使用率或内存排序。要使用 `top`，可以获取运行进程的 `top` 描述（关于 `top` 的描述见第 9 章）。然而，你也可以使用 `top` 在屏幕视图中查看你的内存使用情况。这是一个示例：

```
$ top

load averages: 0.61, 0.85, 0.62 up 02:02:39

85 processes running, 83 sleeping

CPU: 37.5% user, 15.4% system, 0.8% interrupt, 46.3% idle

Mem: 76M Active, 31M Inact, 79M Wired, 24M Cache, 34M Buf, 53M Free

Swap: 484M Total, 25M Used, 459M Free

| PID | USERNAME | THR | NICE | RES | TIME | WCPU | COMMAND |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1618 | | 3 | | 51964K | 35352K | 00:07 | 7.96% | top |
| 1462 | | 1 | | 08501K | 15968K | 00:33 | 5.66% | Xorg |
| 1491 | | 1 | | 01281K | 0008K | 00:05 | 1.03% | metastability |
| 1994 | | 1 | | 03072K | 10928K | 00:08 | 0.44% | gnome-panel |
```

要退出 `top`，按 `q`。`top` 命令显示 `RAM` 的总内存占用（`Mem:`）和交换空间（`Swap:`）。然而，`top` 是屏幕导向的，你可以每秒监控一次内存使用情况（默认）。分析内存使用最有用的命令是 `RES`，它显示驻留内存（resident memory）。运行 `top -res` 将按 `res` 列排序进程：

```
$ top -res

| PID | USERNAME | THR | NICE | RES | STAT | TIME | WCPU | COMMAND |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1673 | | 3 | | 05628K | 38660K | 00:22 | 0.00% | top |
| 1615 | | 1 | 96 | 027060K | 15428K | 00:03 | 0.00% | kview |
| 1462 | | 1 | 100 | 084900K | 13388K | 01:51 | 10.60% | Xorg |
| 1496 | | 3 | 20 | 033027K | 10928K | 00:05 | 0.00% | nautilus |
```

要查看进程消耗的总内存大小（包括文本、数据和栈），可以查看 `SIZE` 列。这样做请运行 `top -osize`：

```
$ top -osize

| PID | USERNAME | THR | PRICE | SIZE | RES | STATE | TIME | WCPU | COMMAND |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1462 | chris | 100 | | 85036K | 125288K | | 03:41 | 10.94% | Xorg |
| 1764 | | 3 | 114 | 056124K | 387128K | | 00:31 | 0.00% | top |
| 1496 | | 3 | 20 | 033072K | 81800K | | kserel | 00:05 | 0.00% | nautilus |
| 1994 | | 1 | 96 | 027880K | 9384K | | 00:10 | 0.00% | gnome-phone |
```

要查看更详细的虚拟内存统计，请使用 `vmstat` 命令。通过 `vmstat`，你可以查看一段时间内的内存使用情况，例如上一次重启或使用采样周期。以下示例显示 `vmstat` 每三秒刷新一次统计信息：

```
$ vmstat

procs memory disks faults cpu

r b w av free re pi po fr sr ad da in sy cs us id

5 2 259816 12604 258 1 0 183 107 0 1482 795 1154 23 7
12 2 260596 14592 284 1 0 183 107 0 1596 884 1268 12 5
5 2 277480 16672 288 1 0 248 132 0 1774 916 1341 28 4
7 2 314596 11916 317 2 0 315 117 0 1973 101 1143 43 6
5 2 351960 12616 367 2 0 445 53 0 2120 756 1541 52 0
5 2 356944 9032 387 2 0 535 15 0 2181 752 1665 76 0
6 2 359284 9312 404 2 0 542 33 0 2299 874 1602 84 0
4 8 386017 8884 284 8 0 588 15 0 2496 884 1802 12 0
```

### slab 缓存信息

slab 缓存信息（slab cache information）存储了每个缓存类型、该缓存的节点数量、使用的内存量、缓存请求数以及缓存的大小。

| | 105 | 27K | | 105 | 256 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `DEVFS` | 12 | 1K | | 13 | 16,128 |
| `pfs_nodes` | 20 | 3K | | 20 | 128 |
| `pfs_vncache` | | 1K | | 33 | 32 |
| `GEOM` | 90 | 10K | | 480 | 16,32,64,128,256,1024,2048,4096 |
| `isadev` | | 19 | 2K | | 19 | 64 |
| `cdev` | 32 | 4K | | 32 | 128 |

### 监控 CPU 使用率

`CPU` 过载是你在系统上查找性能问题的另一个明显迹象。如前文所示，`vmstat` 命令可以生成与 `CPU` 使用率相关的基本统计数据（用户活动、系统活动、空闲时间、`I/O` 等待时间以及从虚拟机中窃取的 `CPU` 时间）。然而，`iostat` 命令可以生成更详细的 `CPU` 使用率报告。如果你想用一种更主动的方式观察 `CPU` 使用率，可以使用 `systat` 实用。`top` 命令可用于查看哪些进程消耗了最多的处理时间。

以下是使用 `iostat` 显示 `CPU` 使用率报告的两个示例：

```
$ iostat -w 3   CPU stats every 3 seconds (starting apps)   cpu

tty          da0                               pass0      us ni in id

tin KB/K tps MB/s  KB/K tps MB/s  KB/K tps MB/s  us ni in id

8 72.12 3.6   0.11 0.00 0.00 0.00 0.00 35 5 1 74
384 77.00 0.0   0.00 0.00 0.00 0.00 0.00 20 5 1  
405 26.73 76 0.84 0.00 0.00 0.00 0.00 42 13 2 4
333 24.03 76 1.04 0.00 0.00 0.00 0.00 67 28 4 1
232 25.76 41 0.63 0.00 0.00 0.00 0.00 71 28 1  
29 26.11 14 0.28 0.00 0.00 0.00 0.00 65 34 2 0

$ iostat -w 3   CPU stats every 3 seconds (copying files)  cpu

tty          da0                               pass0      us ni in id

tin KB/K tps MB/s  KB/K tps MB/s  KB/K tps MB/s  us ni in id

7 53.97 3.6   0.11 0.00 0.00 0.00 0 48 9 1 42
0 77.56 85 10.54 0.00 0.00 0.00 0.00 0 22 27 2
0 123.48 90 1.81 0.00 0.00 0.00 0.00 0 20 27 3
0 128.00 91 1.37 0.00 0.00 0.00 0.00 0 5 18 5
0 125.10 81 0.89 0.00 0.00 0.00 0.00 0 19 27 4
0 125.76 95 11.62 0.00 0.00 0.00 0.00 5 21 27 2
0 126.75 102 12.66 0.00 0.00 0.00 0.00 6 0.26 2 7
```

第一个 `iostat` 示例从一个空闲系统开始，然后启动了几个应用程序。你可以看到大多数应用程序的处理是在用户空间中完成的。第二个 `iostat` 示例显示了在大文件从一个磁盘复制到另一个磁盘时，在内核空间中进行的操作（在这种情况下，是从磁盘读取，且结果是极高百分比的时间花费在写入磁盘分区上）。请注意，文件复制也会导致在空闲模式下花费更长的时间来等待 `I/O` 请求完成（`id` 列）。这是一个使用 `iostat` 的示例：

第一个 `iostat` 示例显示了系统从空闲到启动多个应用程序的过程。你可以看到，大多数应用程序的处理是在用户空间中完成的。第二个 `iostat` 示例显示了当大文件从一个磁盘复制到另一个磁盘时，在内核空间中进行的操作（在这种情况下，是从磁盘读取，且结果是极高百分比的时间花费在写入磁盘分区上）。请注意，文件复制也会导致在空闲模式下花费更长的时间来等待 `I/O` 请求完成（`id` 列）。这里是使用 `iostat` 监控 `CPU` 使用率的示例：

```
1   100   0 6184  16.7  48 6120  4.4  91.6  ad0s1
0   48    0     0.0   48 6120  4.5  21.5  ad0s1d
1   52   52  6184  16.9   0    0.0  87.7  ad0s1f

# stat -I 4s
      每 4 秒更新一次显示
```



如果您想找出哪些文件和目录当前正占用您的存储设备，可以使用 `lsof` 命令。当您尝试卸载一个正被占用的文件系统时，这个命令特别有用。您可以检查是哪个打开的文件阻止了卸载，并决定是否要杀死持有该文件的进程并强制卸载该文件系统。以下是 `lsof` 的示例：

```
# lsof | less 列出持有打开状态文件和目录的进程
```

| COMMAND | PID | USER | TYPE | DEVICE | SIZE/OFF | NODE | NAME |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| init | 1 | root | VDIR | 0,87 | | 512 | / |
| init | 1 | root | rtd | 0,87 | | 512 | / |
| init | 1 | root | trt | 0,87 | 514792 | 49395 | /sbin/init |
| adjkertz | 123 | root | VDIR | 0,87 | | 512 | / |
| adjkertz | 123 | root | rtd | 0,87 | | 512 | / |
| sh | 1443 | chris | VDIR | 0,92 | | 2536 | 2775585 /home/chris |

第一个显示为打开的文件由 `init` 进程（系统上第一个运行的进程）持有。接下来运行的是 `adjkernel` 进程，用于调整本地时间。由其他系统进程（如 `dev`）和守护进程（如 `sshd` 和 `syslog`）打开的文件跟在 `init` 之后。最后，您将看到由用户打开的文件（如果您无法卸载磁盘分区，这些可能就是您所感兴趣的文件）。

在查看 `lsof` 输出时，您想要看到打开的文件或目录的名称（`NAME`）、打开它的命令（`COMMAND`）以及运行命令的进程 ID（`PID`）。正如当您想要卸载的文件系统被占用时一样，`/home` 文件系统正被一个 `sh` shell 占用（在示例中，`/home/chris` 是该 `sh` 的当前工作目录）。事实上，除了将 `lsof` 输出通过给 `less` 或 `grep` 之外，这里还有其他通过 `lsof` 查找您所需内容的方法：

```
# lsof -c csh 列出由 C shell (csh) 进程打开的文件
# lsof -d cwd 列出作为当前工作目录打开的目录
# lsof -u user 列出用户 chris 打开的文件和目录
# lsof /var 列出 /var 文件系统上打开的任何内容
# lsof +d /var/log 列出 /var/log 目录下打开的任何内容
```

## 掌握时间

在您的 BSD 系统上保持时间准确对于系统的正常运行至关重要。您可以通过几种不同的方式设置 BSD 上的时间。系统时间可以手动（使用 `date` 命令）查看和设置，也可以自动（使用 `ntpdate` 或 `nptd` 服务）设置。另一个与其他相关的命令是 `uptime`，它可以让您查看系统运行了多久。

### 更改时区

您的 BSD 系统时区设置在 `/etc/localtime` 文件的内容上。您可以通过从 `/usr/share/zoneinfo` 的子目录下复制代表您时区的文件来立即设置新时区。例如，要将当前时区改为芝加哥，您可以执行以下操作：

```
# cp /usr/share/zoneinfo/America/Chicago /etc/localtime
```

也可以通过创建符号链接来实现这一点：

```
# ln -s /usr/share/zoneinfo/America/Chicago /etc/localtime
```

在 FreeBSD 中，还有一个名为 `tzsetup` 的工具可以让您选择本地时区。

### 显示和设置您的日期和时间

如果您没有通过 NTP 自动完成，`date` 命令是查看和更改日期设置的主要命令行界面。以下是使用 `date` 命令以不同方式显示日期和时间的示例：

```
$ date
显示当前的日期、时间和时区
```

```
$ date '%a %B %d %Y'
显示星期、月份、日期、年份
Tue Aug 12 01:26:50 CDT 2008
Tuesday 12 August 2008
```

```
$ date '+The date today is %F.'
在日期输出中添加文字
$ date '+TIME:%H:%M:%S\nDATE:%Y-%m-%d'
显示时间和 日期
TIME:06:29:10
DATE:2008-12-18
```

```
$ date -v+im -v -d -v-mon
显示本月的上一个星期一
Mon 29 08:18:32 CST 2008
```

```
$ date -u
显示协调世界时 (UTC)
Mon Dec 29 15:19:12 UTC 2008
```

由于我们谈到了日期，我们在这里主要感兴趣的是 `cal` 命令，它是按月显示日期的快速方法。以下是示例：

```
$ cal
显示当前月份日历（高亮今天）
October 2008
Mo Tu We Fr Sa
1 2 3 4 5 6 7 8 9 10 11
12 13 14 15 16 17 18
19 20 21 22 23 24 25
26 27 28 29 30 31
```

```
$ cal 2008
显示全年日历
2008
January        February         March
Su Tu We Fr Sa  Su Tu We Fr Sa  Su Tu We Fr Sa
     1 2 3 4 5              1 2 3 4 5 6 7 8
9 10 11 12 13 14 15 9 10 11 12 13 14 15
16 17 18 19 20 21 22 23 24 25 16 17 18 19 20
21
$ cal -j
显示儒略日历（从 1 月开始）
October 2008
Su Tu We Fr Sa
25 26 27 28 29 30 31
```

`date` 命令也可以用于更改系统日期和时间。（但注意，随机更改日期可能会导致系统崩溃。）以下是示例：

```
# date 0812152100
设置日期/时间为 8月12日 21:00 PM, 2008
Mon Dec 15 21:00:00 CST 2008
# date -v +2H
将时间后推 2 小时
Sun Aug 12 11:42:33 CDT 2008
# date -v +3m
将日期/时间提前一个月
```

下次启动 FreeBSD 时，系统时间将根据硬件时钟的值（如果启用了 NTP 服务器）重置。下次关机时，硬件将重置为系统时间，以便在机器关机时保持时间。确保系统始终获得正确时间的一种方法是使用网络时间协议 (NTP)。

### 使用网络时间协议设置日期/时间

当安装 FreeBSD 时，您将有机会设置时区以及系统时钟反映本地时间还是 UTC 时间。您的系统将根据硬件时钟和时区显示日期时间。如前所述，确保系统时间不漂移的方法之一是使用网络时间协议 (NTP)。

`ntp` 守护进程随 FreeBSD 系统安装。要让您的 FreeBSD 系统与网络上的时间服务器同步，您只需要创建一个配置文件并启用 `ntp` 守护进程。编辑 `/etc/ntp.conf` 以创建一个 `server` 和 `driftfile` 条目。例如：

```
server pool.ntp.org
driftfile /var/db/ntpd.drift
restrict default ignore
```

要启用网络时间协议 (`ntpd` 守护进程)，您可以在 `/etc/rc.conf` 文件中添加以下行：

```
ntpd_enable=YES                      # 运行 ntpd 网络时间协议 (或 NO),
ntpd_program="/usr/sbin/ntpd"      # ntpd 的路径，如果您有不同的
ntpd_config="/etc/ntp.conf"          # ntpd($) 配置文件
ntpd_sync_on_start=YES               # 在 ntp 启动时同步时间，
                                               # 如果偏移较大
ntpd_flags=-p /var/run/ntpd.pid -f /var/db/ntpd.drift"  # ntpd 的选项
```

实际上，您需要添加 `ntpd_enable` 和 `ntpd_sync_on_start` 行，并确保它们被设置为 `YES`。其他行由默认设置（在 `/etc/rc.conf` 中），在此处仅供您参考。下次启动系统时，您的时间将根据从 NTP 服务器收集的信息设置。如果您喜欢手动启动 `ntpd` 守护进程，可以输入以下命令：

```
/usr/sbin/ntpd -p /var/run/ntpd.pid -f /var/db/ntpd.drift -c /etc/ntp.conf
```

设置好服务后，运行的设置会将您的机器变成一个时间服务器，监听 UDP 端口 123。除非您有特殊需求（并且有自己的 GPS 或原子钟），否则在您的机器上运行 `ntpd` 可能是浪费资源（通常在每日 `cron` 任务中）来通过 NTP 设置系统时间。由于原因，系统管理员倾向于使用 `ntpdate`（通过 NTP 设置系统时间）：

```
# ntpdate pool.ntp.org      立即从 pool.ntp.org 设置日期/时间
15 Aug 00:37:12 ntpdate[9706]:nadjust time 66.92.68.11 offset 0.09204 sec
```

如果在 `ntpd` 运行时尝试使用 `ntpdate`，您将收到以下错误：

```
# ntpdate pool.ntp.org
15 Aug 00:37:00 ntpdate[9695]: the NTP socket is in use, exiting
```

注意，`ntpdate` 命令已标记为废弃，并在未来将消失。它已被 `ntpd` 的以下选项取代：

```
# ntpd -qq
```

`q` 选项允许 `ntpd` 在设置时间后退出（而不是作为守护进程运行）。`-g` 选项防止 `ntpd` 在系统钟偏差 1000 秒时恐慌。

# 第10 章：系统管理

注意：你可以在 BIOS 中设置计算机的硬件时钟。BSD 系统如何解释硬件时钟取决于多个因素。如果 `/etc/wall_cmos_clock` 文件存在，BSD 假设硬件时钟被解释为本地时间。如果没有，它被解释为 UTC 时间。根据你的硬件时钟和时区，运行中的 `adjtime` 进程会调整内核时钟并存储该信息。输入 `sysctl maxdep.adjkernel` 查看该偏移量。

## 检查运行时间

BSD 以及其他 Linux 和 UNIX 爱好者的自豪感之一是他们的系统在不重启的情况下可以运行多久。BSD 系统多年来以无需重启而闻名。这种时长被称为运行时间（uptime）。你可以通过以下方式检查系统的运行时间：

```
$ 检查你的系统运行了多久
16:53pm up 196 days, 14:25, 3 users, load average: 1.66, 0.88, 0.35
```

`uptime` 输出显示了当前时间、系统运行的天数和小时数以及当前登录的用户数。之后，`uptime` 显示了过去 1 分钟、5 分钟和 15 分钟的系统负载。

## 管理启动过程

当 PC (x86) 启动时，基本输入输出系统 (BIOS) 查看其启动顺序设置以确定从哪里寻找操作系统。通常，如果没有向可移动驱动器插入可启动介质（CD、DVD、软盘等），BIOS 将查找第一块可启动硬盘上的主引导记录 (MBR)。此时，对于大多数 BSD 系统而言，该过程的控制权将交给引导加载器（boot loader）。

FreeBSD 和其他 BSD 系统可以选择多种引导加载器。但默认情况下，FreeBSD 使用 `boot0` 加载器。通过配置 `boot0`，你不仅可以让你计算机完全按照你想要的方式启动 FreeBSD，还可以配置它启动安装在你的计算机上的其他操作系统。你可以选择使用不同的引导加载器（例如后文介绍的 GRUB）来引导启动过程。

BSD 系统分几个阶段启动。第一阶段是 BIOS 开始初始化硬件并在硬盘上寻找主引导记录，随后由 `boot0` 引导加载器接管。接下来，`boot1` 启动并使用 `bslabel` 指向 `boot2`。接着 `boot2` 启动，它将控制权交给引导加载器或直接交给内核。最后，在 FreeBSD 中，你应该看到一个类似下面的启动提示符：

```
F1 FreeBSDnDefault: F1
```

当选择从引导加载器启动 BSD 系统时，引导加载器将进入你请求启动的分区，并加载二级引导加载器或加载内核。在 FreeBSD 引导过程的最后阶段，内核启动，`rc` 脚本启动系统服务，你将看到一个提示符或显示管理器以进行登录。

以下章节描述了修改与你的 BSD 系统相关的引导加载器和启动脚本的命令。

### 使用 boot0 引导加载器

`/boot/boot0` 包含了 FreeBSD 使用的默认引导镜像。如果你想将引导镜像替换为你自己编译的镜像，也可以这样做。`boot0cfg` 命令也可用于查看或更改与当前引导加载器相关的设置。

注意：在接下来的示例中引用磁盘时，IDE 硬盘以 `ad` 开头，SCSI 硬盘以 `da` 开头。第一块 IDE 硬盘是 `ad0`，第二块是 `ad1`，以此类推。SCSI 硬盘也是如此，命名为 `da0`、`da1` 等。IDE 硬盘 1 上的第一个分区是 `ad0s1`。

以下使用 `boot0cfg` 命令检查和更改你的引导镜像的一些示例：

```
# boot0cfg -v ad0 显示 IDE 硬盘 1 上 boot0 加载器的信息
# flag start chs type end chs offset size
1 0x80 0: 1 0xa5 1023:254:63 63 40949626
```

```
versions1.0 drive=0x80 mask=0xf ticks=18
options-packet,update,nosetdrv
default_selection=1 (Slice 1)
```

`boot0cfg -v` 的输出向你展示了 `boot0` 在所选磁盘（在本例中为第一块磁盘 `ad0`）上如何设置。在这种情况下，第一块磁盘 (0x80) 上的分区 (1) 是可启动的。该分区从磁柱 0、磁头 0 和扇区 0 开始，结束于磁柱 1023、磁头 254 和扇区 63。分区类型为 0xa5，用于 FreeBSD、NetBSD 和 386BSD。

在版本号 (1.0) 之后，输出显示 BIOS 将指示启动第一块硬盘 (`ad0`)，启用了四个分区 (0xf)，并且启动提示符超时时间设置为 18 ticks（约 10 秒）。你使用的三个选项表示：使用磁盘数据包（BIOS INT 0x13 扩展）接口进行磁盘 I/O (`packet`)，允许引导管理器更新主引导记录 (`update`)，并且不强制使用包含 `-d` 选项引用磁盘的驱动器。

现在你已经有了设置，以下是你可以更改 `boot0` 加载器的方法。

> 警告！如果你搞乱了引导加载器，你的计算机可能无法启动。我建议在系统无法启动时，准备一张救援光盘来修复问题。

```
# boot0cfg -b ad0                安装 ad0 引导加载器
# 如果系统无法启动，使用救援光盘运行 boot0cfg -b ad0
# boot0cfg -t 36                 更改超时时间为 36
# boot0cfg -c ad0                 在 ad0 上清除引导记录
# boot0cfg -v ad0                 显示 ad0 的详细信息
# boot0cfg -s ad0                 在 ad0 上设置默认分区
# boot0cfg -p ad0                 在 ad0 上设置数据包
# boot0cfg -u ad0                 在 ad0 上更新引导记录
# boot0cfg -i ad0                 在 ad0 上安装引导镜像
# boot0cfg -w ad0                 在 ad0 上写入引导镜像
# boot0cfg -f ad0                 在 ad0 上格式化分区
# boot0cfg -n ad0                 在 ad0 上创建新分区
# boot0cfg -m ad0                 在 ad0 上修改分区大小
# boot0cfg -r ad0                 在 ad0 上挂载分区
# boot0cfg -q ad0                 在 ad0 上卸载分区
# boot0cfg -k ad0                 在 ad0 上查看分区状态
# boot0cfg -x ad0                 在 ad0 上删除分区
# boot0cfg -b 1 1024  0x80 ad0    在 ad0 上启动分区 1
# boot0cfg -b 2 2048 0x80 ad0    在 ad0 上启动分区 2
# boot0cfg -b 3 3072 0x80 ad0    在 ad0 上启动分区 3
# boot0cfg -b 4 4096 0x80 ad0    在 ad0 上启动分区 4
```

# 第 10 章：管理系统

## 使用 bsdlabel 检查分区

当你首次安装 FreeBSD 时，`sysinstaller` 在你的 BSD 磁盘分区（slice）上创建了分区。要在特定的 BSD 磁盘分区内显示并操作这些分区，你可以使用 `bsdlabel` 命令。假设你的磁盘第一个分区包含你的 BSD 分区，输入以下命令查看该分区上的分区：



`bsdlabel ad0s` 显示 BSD 磁盘上的分区，分区 1

```
# bsdlabel ad0s          显示 BSD 磁盘上的分区，分区 1
# /dev/ad0s:
8 partitions:
# size    offset  fsize bps [cpg]
a 1048576      0       4.2BSD  2048 163844 8
b 975760               swap
c 4094962      0       # "raw" 部分，不要编辑
d 2584576    2024336  4.2BSD  2048 163844 28552
e 1048576    4608912  4.2BSD  2048 163844 8
f 3529134    5657448  4.2BSD  2048 163844 28552
```

`bsdlabel` 的输出显示了第一个 IDE 硬盘 (`ad0s1`) 第一个分区内的不同分区。你可以通过运行 `df` 命令显示已挂载的分区，更好地了解这些分区与你系统系统的关系：

```
# df -h          已挂载的分区
Filesystem      Size  Avail Capacity Mounted on
/dev/ad0s1      496M   39M  418M 8%        /
/devs           1.0K    0B  100%       /dev
/dev/ad0s11     496M   16K  456M 0%         /usr
/dev/ad0s11f    160     1.7G   13G  11%        /tmp
/dev/ad0s11d    1.2G    19M    2%         /var
```

如你所见，分区 `a`、`d`、`e` 和 `f` 分别挂载在根目录 (`/`)、`/var`、`/tmp` 和 `/usr` 上。分区 `b` 是交换分区。分区 `c` 是“原始”部分，不应修改。`devfs` 文件系统 `/dev` 提供了对计算机硬件设备的访问。

由于本章的讨论涉及启动过程，请参阅第 7 章有关 `bsdlabel` 和 `fdisk` 命令创建和修改磁盘分区及分用途的信息。

## 切换到 GRUB 引导程序

没有理由使用 `boot0` 引导程序来启动你的 BSD 系统。如今，许多人使用通用统一引导程序 (GRUB)，特别是在启动多个操作系统（如 Linux）的情况下。GRUB 具有一些功能，例如用于编辑启动选项的屏幕和菜单。

FreeBSD 提供了一个 `grub` 软件包。或者，如果需要，你可以从计算机上安装的其他系统之一来配置 GRUB。要在 FreeBSD 中安装 GRUB，请输入以下命令：

```
# pkg_add -r grub      安装 grub 软件包
```

接下来，你通过创建 `/boot/grub` 目录并将所需的 GRUB 文件复制到其中来设置 GRUB 文件。

```
# mkdir /boot/grub      创建 /boot/grub 目录
# cp -Rf /usr/local/share/grub/i386-freeBSD/ /boot/grub 将文件复制到 /boot/grub
```

接下来，你需要使用任何编辑器创建一个 `menu.list` 文件，告诉 GRUB 启动什么以及如何启动。在这个示例中，FreeBSD 系统和之前描述的 Debian GNU/Linux 系统设置为从 GRUB 启动屏幕启动。

```
default=0
timeout 15

title FreeBSD
root notify (hd0,0)
makeactive
chainloader +1

title Debian GNU/Linux
root (hd0,1)
chainloader +1
```

默认启动的操作系统是第一个 (`default=0`)，即 FreeBSD。GRUB 在启动操作系统之前会暂停 15 秒 (`timeout 15`)。由于引导程序同时安装在 FreeBSD 和 Debian 分区上，配置这两个系统的简单方法是使用链式加载器（`chainloader`）启动。这将让你看到这两个系统各自的二级启动屏幕。

现在你需要覆盖硬盘的主引导记录 (MBR)。由于默认情况下你可能无法写入硬盘的 MBR，请运行以下 `sysctl` 使覆盖 MBR 变得可行：

```
# sysctl kernel.geom.debugflags=16
```

一旦你创建了 `menu.list` 文件并能够写入主引导记录，就可以使用 `grub-install` 命令将其安装到主引导记录中。输入以下命令将 GRUB 安装到磁盘 `ad0` 的主引导记录中。

> 警告！你即将覆盖计算机的主引导记录。如果你在 `menu.list` 文件中执行了错误，`grub-install` 可能会失败。然而，如果写入完成的信息导致无法工作，你可以通过输入 `boot0cfg -B ad0` 随时恢复旧的 `boot0` 引导程序。

## 启动和停止你的系统

虽然你可以使用 `init` 命令启动和停止你的 BSD 系统，包括 `init 0`（关机）和 `init 6`（重启），但也有特定的停止 BSD 命令。`halt`、`reboot` 或 `shutdown` 等命令的优势在于它们允许你在关机发生之前让某些功能完成。例如：

```
# reboot
重启计算机
# halt -n
在关机前不运行 sync 同步硬盘
# halt -p
系统将关闭电源（如果可能）
# shutdown +10
在十分钟后关机并通知用户
# shutdown -r 06:08
在上午 06:08 重启
# shutdown +10 'Bye!'
在关机前向用户发送自定义消息
```

# 第 10 章：系统管理

用于查看有关内核如何启动的信息。此外，如果发生错误或你需要为内核添加某些额外支持，都有工具可以完成这些工作。

要确定你正在运行哪个版本的 BSD，请输入以下命令：

```
$ uname -r          显示当前发布版本的名称
6.3-RELEASE
$ uname -a          显示所有名称和发布信息
FreeBSD myhost.localdomain 6.3-RELEASE FreeBSD 6.3-RELEASE #0: Wed Aug 16 04:18:52 UTC 2008 root@desseller.c.buffalo:/usr/obj/usr/src/sys/GENERIC
1386
```

当内核启动时，关于发生情况的消息会被放置在系统消息缓冲区。你可以使用 `dmesg` 命令查找系统消息缓冲区的详情：

```
$ dmesg |less
Copyright (c) 1992-2008 The FreeBSD Project.
Copyright (c) 1979, 1980, 1983, 1986, 1988, 1989, 1991, 1992, 1993, 1994
The Regents of the University of California. All rights reserved.
FreeBSD is a registered trademark of the FreeBSD Foundation.
6.3-RELEASE #0: Wed Jan 16 04:18:52 UTC 2008
root@desseller.c.buffalo:/usr/obj/usr/src/sys
timecounter "18254" frequency 119312 Hz quality
CPU: Intel Pentium III Id = 0x683 Stepping = 3
Origin = "GenuineIntel* SSE"
>>
Features=0387f9ff-PFF,VME, DE, PSE, TSC, MSR, PAE, PGE, XEP, PTR, PTE, PCE, MCA, PAT,
P36, NX, PMX, MSR, SSE
real memory = 267142736 (254 MB)
avail memory = 251854848 (240 MB)
kbi at kdbdmux0
th_hal:0.920.3 (AR5210, AR5211, AR5212, RF5111, RF5112, RF2413, RF5413)
htpr: HTP RocketRadius kernel driver v1.1 (1 Jan 2008 04:16:19)
acpi0:CAMAN 8C1IAA0 on motherboard
acpi0:ACPI-fast* frequency 3579545 Hz quality 1000
acpi_timer0:<24-bit timer at 3579545MHz port 04x0-04xb0 on acpi0
...
```

如果缓冲区满了，它可能不再包含所记录信息的开头。在这种情况下，你可以使用 `less /var/log/dmesg`。

关于内核处理的其他信息可以在 `/var/log` 文件中找到，特别是 `messages` 文件。你可以按照以下方式查看这些文件：

```
# less /var/log/messages*
Aug 14 23:27:11 thompson syslog[557]: logfile first created
Aug 14 23:27:11 thompson syslog: kernel boot file is /boot/kernel/kernel
```

`Aug 14 23:27:11 thompson kernel: kbdl at kdbdmux0`

`Aug 14 23:27:11 thompson kernel: acpi0: <CAYAN 9C1A10A> on motherboard`

`Aug 14 23:27:11 thompson kernel: acpi0: Power Button (fixed)`

`Aug 14 23:27:11 thompson kernel: Timecounter <ACPI-fast frequency 357954 Hz quality 1000`

`Aug 14 23:27:11 thompson kernel: cpu0: <ACPI CPU> on acpi0`

`Aug 14 23:27:11 thompson kernel: pcib0: <ACPI Host-PICI bridge> port 0xcf8-0xcff acpi0`

`Aug 14 23:27:11 thompson kernel: fxp0: <Intel 82559 Pro/100 Ethernet> port 0xde80-0xdef6 mem 0xff8fd000-0xff8fdfff,0xff700000-0xffffff niq 1 device on 0.0 pci`

在理想情况下，连接到计算机的所有硬件都应该被检测并使用适当驱动程序进行配置。但在某些情况下，检测到了错误的驱动程序，或者系统中可能没有所需的驱动程序。对于这些情况，FreeBSD 提供了出可加载模块并向系统添加新模块的方法。

`kldstat` 命令允许查看已加载模块的名称、地址、大小和引用 ID。这是一个示例：

### kldstat

| ID | 引用 | 地址 | 名称 |
| :--- | :--- | :--- | :--- |
| 1 | 0xc040000 | | |
| 2 | | | |
| 3 | | | |
| 4 | | | |
| 5 | | | |
| 6 | | | |
| 7 | | | |

如果你想查找特定模块的详细信息，可以使用 `kldstat` 命令。这是一个示例：

| ID | 引用 | 地址 | 名称 |
| :--- | :--- | :--- | :--- |
| 1 | 0xc040000 | | |
| 2 | | | |
| 3 | | | |
| 4 | | | |
| 5 | | | |
| 6 | | | |
| 7 | | | |



```bash
$ dmesg | less
Copyright (c) 1992-2008 The FreeBSD Project.
Copyright (c) 1979, 1980, 1983, 1986, 1988, 1989, 1991, 1992, 1993, 1994
The Regents of the University of California. All rights reserved.
FreeBSD is a registered trademark of the FreeBSD Foundation.
6.3-RELEASE #0: Wed Jan 16 04:18:52 UTC 2008
root@desseller.c.buffalo:/usr/obj/usr/src/sys
timecounter "18254" frequency 119312 Hz quality
CPU: Intel Pentium III Id = 0x683 Stepping = 3
Origin = "GenuineIntel* SSE"
>>
Features=0387f9ff-PFF,VME, DE, PSE, TSC, MSR, PAE, PGE, XEP, PTR, PTE, PCE, MCA, PAT,
P36, NX, PMX, MSR, SSE
real memory = 267142736 (254 MB)
avail memory = 251854848 (240 MB)
kbi at kdbdmux0
th_hal:0.920.3 (AR5210, AR5211, AR5212, RF5111, RF5112, RF2413, RF5413)
htpr: HTP RocketRadius kernel driver v1.1 (1 Jan 2008 04:16:19)
acpi0:CAMAN 8C1IAA0 on motherboard
acpi0:ACPI-fast* frequency 3579545 Hz quality 1000
acpi_timer0:<24-bit timer at 3579545MHz port 04x0-04xb0 on acpi0
...
```

如果缓冲区满了，它可能不再包含所记录信息的开头。在这种情况下，你可以使用 `less /var/log/dmesg`。

关于内核处理的其他信息可以在 `/var/log` 文件中找到，特别是 `messages` 文件。你可以按照以下方式查看这些文件：

```bash
# less /var/log/messages*
Aug 14 23:27:11 thompson syslog[557]: logfile first created
Aug 14 23:27:11 thompson syslog: kernel boot file is /boot/kernel/kernel
```

`Aug 14 23:27:11 thompson kernel: kbdl at kdbdmux0`

`Aug 14 23:27:11 thompson kernel: acpi0: <CAYAN 9C1A10A> on motherboard`

`Aug 14 23:27:11 thompson kernel: acpi0: Power Button (fixed)`

`Aug 14 23:27:11 thompson kernel: Timecounter <ACPI-fast frequency 357954 Hz quality 1000`

`Aug 14 23:27:11 thompson kernel: cpu0: <ACPI CPU> on acpi0`

`Aug 14 23:27:11 thompson kernel: pcib0: <ACPI Host-PICI bridge> port 0xcf8-0xcff acpi0`

`Aug 14 23:27:11 thompson kernel: fxp0: <Intel 82559 Pro/100 Ethernet> port 0xde80-0xdef6 mem 0xff8fd000-0xff8fdfff,0xff700000-0xffffff niq 1 device on 0.0 pci`

在理想情况下，连接到计算机的所有硬件都应该被检测并使用适当驱动程序进行配置。但在某些情况下，检测到了错误的驱动程序，或者系统中可能没有所需的驱动程序。对于这些情况，`FreeBSD` 提供了出可加载模块并向系统添加新模块的方法。

`kldstat` 命令允许查看已加载模块的名称、地址、大小和引用 ID。这是一个示例：

### kldstat

| ID | 引用 | 地址 | 名称 |
| :--- | :--- | :--- | :--- |
| 1 | 0xc040000 | | |
| 2 | | | | |
| 3 | | | | |
| 4 | | | | |
| 5 | | | | |
| 6 | | | | |
| 7 | | | | |

如果你想查找特定模块的详细信息，可以使用 `kldstat` 命令。这是一个示例：

| ID | 引用 | 地址 | 名称 |
| :--- | :--- | :--- | :--- |
| 1 | 0xc040000 | | |
| 2 | | | | |
| 3 | | | | |
| 4 | | | | |
| 5 | | | | |
| 6 | | | | |
| 7 | | | | |

*(注：由于输入文本存在大量重复的碎片，以上译文已进行去重处理)*

# 11 管理网络连接

从 BSD 系统连接到网络通常只需将计算机的网络接口卡连接到 `ISP`（互联网服务提供商）的硬件（如 `DSL` 或电缆调制解调器）并重启。然而，如果你的网络接口没有启动或需要某些手动干预，可以使用许多命令来配置网络接口、建立网络连接以及设置特殊路由。

- 本章内容

- 获取网络统计数据

- 使用 `ifconfig` 启动网络设备

- 管理网卡

- 使用 `dig`、`host` 和 `hostname` 检查 `DNS` 解析

- 使用 `ping` 和 `arping` 检查连通性

- 使用 `traceroute` 和 `route` 追踪连接

- 使用 `netstat`、`tcpdump` 和 `nmap` 监控网络

本章涵盖了许多用于配置和操作网络接口卡（`NIC`）的有用命令，例如 `sysinstall` 和 `ifconfig`。特别是，它还涵盖了有线以太网、无线以太网和调制解调器网络硬件的配置。本章描述了如 `netstat`、`dig` 和 `ping` 等类的命令，用于在硬件已连接且网络接口就绪时获取有关网络的信息。

## 使用 sysinstall 配置网络接口

`DH` 网络上检测到 `DHCP` 服务器。或者，你可以设置静态 `IP` 地址，以及主机名、网关机器和服务器的 `IP` 地址。安装后，你可以使用 `sysinstall` 工具配置你的网络接口。以 `root` 用户身份启动它：

```bash
# sysinstall
```

当你安装 `FreeBSD` 系统时，安装程序允许你使用以下工具配置连接到计算机的任何有线以太网卡：

在出现的 `FreeBSD` 配置菜单中，选择“Networking Interfaces”（网络接口）。此时，你有根据连接到计算机的网络硬件配置网络接口的选项。例如：

- 以太网接口卡 (`fxp0`, `inc0` 或其他) —— 到以太网网络的有线连接

- 并行 IP 端口 (`plip0`) —— 通过并行端口直接连接另一台计算机

- 线路互联网协议 (`cuad0`) —— 连接到调制解调器或到另一台计算机的串口连接

- 点对点协议 (`ppp`) —— 连接到调制解调器或到另一台计算机的串口连接

在这两个接口中，`SLIP` 比 `PPP` 老旧，但现在更常用。`PLIP` 需要特殊的电缆，而且如今以太网网卡非常廉价，`PLIP` 很少使用。

如果你的 `NIC` 被支持，你应该能在 `sysctl` 显示中看到该网卡的名称。要配置它，你可以配置 `IPv6` 网络。然后，你可以选择从 `DHCP` 获取计算机的地址信息，或手动配置。如果你手动配置，可以输入计算机的主机名、域名、网关 (`IPv4`)、服务器、`IP` 地址 (`IPv4`) 子网掩码以及任何传递 `ifconfig` 的选项。

然而，在某些情况下，你的网络接口可能无法工作。同样，可能存在无法通过 `sysctl` 支持的操作网络接口的方法。在这些情况下，后续章节描述了如何从命令行操作你的网络接口。

> 你的以太网 `NIC` 接口名称是基于支持该 `NIC` 所使用的驱动程序的。如果你来自 `Linux` 环境，你可能期望以太网接口命名为 `eth0`、`eth1` 等。在 `FreeBSD` 中，名称可能是 `fxp0`、`inc0` 或其他。本章中的示例使用 `fxp0` 来表示有线以太网接口。

## 管理网络接口卡

如果你计算机上的网络硬件没有立即启动并允许连接到互联网，你需要通过以下步骤来排查问题：

- 检查你的网络接口卡 (`NIC`) 是否正确安装，以及电缆是否连接到网络（`ISP` 的 `CPE`、交换机等）。

电缆连接后，确保你的链路没有速度或双工不匹配。

如果所有方法都失败了，考虑用良好的备件更换 `NIC`，以隔离硬件故障。

从你的 `BSD` 系统检查链路并设置速度和双工模式，`ifconfig` 命令提供了这些以及许多其他功能。

> 注意：如果你来自 `Linux` 或其他 `UNIX` 环境并习惯了 `ethtool` 和 `mii-tool` 等工具，`ifconfig` 命令包含了从那两个命令中获得的许多相同功能。

要查看 `ifconfig` 命令的语法，请输入任何无效选项：

```bash
# ifconfig -? 查看 ifconfig 命令的选项
ifconfig: illegal option --?
usage: ifconfig [-L] [-C] interface address_family [address [dest_address]]
[parameters]
config interface create
ifconfig -a [-L] [-C] [-d] [-m] [-u] [-v] [address_family]
ifconfig -l [-d] [-u] [address_family]
ifconfig [-L] [-C] [-d] [-m] [-u] [-v]
```

要显示所有可用网络接口的名称，使用 `-l` 选项。以下示例显示存在以太网 `NIC` (`fxp0`)、并行端口 (`plip0`) 和环回口 (`lo0`)：

```bash
# ifconfig -l 列出网络接口的名称
fxp0 plip0 lo0
```

要显示特定以太网卡的设置，请在命令后添加接口名称。例如，查看 `fxp0`（第一块有线以太网 `NIC`）的信息，输入：

```bash
# ifconfig fxp0 查看 fxp0 NIC 的设置
fxp0: flags=8843<UP, BROADCAST, RUNNING, SIMPLEX, MULTICAST> mtu 1500
options=VLAN_MTU
inet 10.0.0.2 mask 0xffffff broadcast 10.2.255
ether 00:d0:b7:a9:53
media: Ethernet autoselect (100baseTX full-duplex)
status: active
```

要显示特定网络的能力列表，使用 `-m` 选项：

```bash
# ifconfig -m fxp0 显示 NIC 信息
fxp0: flags=8843<UP, BROADCAST, RUNNING, SIMPLEX, MULTICAST> mtu 1500
options=VLAN_MTU
inet 10.0.0.204 netmask 0xffffff broadcast 10.2.255
ether 00:d0:b7:79:53
media: Ethernet autoselect (100baseTX full-duplex)
status: active
supported:
media autoselect
100baseTX full-duplex
100baseTX
10baseT/UTP full-duplex
loopback
```

`ifconfig` 命令可用于更改及显示 `NIC` 设置。要将 `NIC` 设置为 `100Mbps` 全双工，输入：

```bash
# ifconfig fxp0 100baseTX full-duplex 修改速度/双工
# ifconfig fxp0 查看 fxp0 NIC 的设置
fxp0: flags=8843<UP, BROADCAST, RUNNING, SIMPLEX, MULTICAST> mtu 1500
options=VLAN_MTU
inet 10.0.0.2 mask 0xffffff broadcast 10.2.255
ether 00:d0:b7:a9:53
media: Ethernet autoselect (100baseTX full-duplex)
status: active
```

要将速度设置为 `10Mbps`，输入：

```bash
# ifconfig fxp0 10baseT full-duplex 设置速度
# ifconfig fxp0 查看 fxp0 的设置
```

`fxp0: flags=8843<UP, BROADCAST, RUNNING, SIMPLEX, MULTICAST> mtu 1500`

`options=VLAN_MTU`

`inet 10.0.0.204 netmask 0xffffff broadcast 10.2.255`

`ether 00:d0:b7:a9:53`

`media: Ethernet autoselect (10baseT full-duplex)`

在某些情况下，你的网络接口可能无法工作。同样，可能存在无法通过 `sysctl` 支持的操作网络接口的方法。在这些情况下，后续章节描述了如何从命令行操作你的网络接口。

> 你的以太网 `NIC` 接口名称是基于支持该 `NIC` 所使用的驱动程序的。如果你来自 `Linux` 环境，你可能期望以太网接口命名为 `eth0`、`eth1` 等。在 `FreeBSD` 中，名称可能是 `fxp0`、`inc0` 或其他。本章中的示例使用 `fxp0` 来表示有线以太网接口。

## 管理网络接口卡

如果你计算机上的网络硬件没有立即启动并允许连接到互联网，你需要通过以下步骤来排查问题：

- 检查你的网络接口卡 (`NIC`) 是否正确安装，以及电缆是否连接到网络（`ISP` 的 `CPE`、交换机等）。

电缆连接后，确保你的链路没有速度或双工不匹配。

如果所有方法都失败了，考虑用良好的备件更换 `NIC`，以隔离硬件故障。

从你的 `BSD` 系统检查链路并设置速度和双工模式，`ifconfig` 命令提供了这些以及许多其他功能。

> 注意：如果你来自 `Linux` 或其他 `UNIX` 环境并习惯了 `ethtool` 和 `mii-tool` 等工具，`ifconfig` 命令包含了从那两个命令中获得的许多相同功能。

要查看 `ifconfig` 命令的语法，请输入任何无效选项：

```bash
# ifconfig -? 查看 ifconfig 命令的选项
ifconfig: illegal option --?
usage: ifconfig [-L] [-C] interface address_family [address [dest_address]]
[parameters]
config interface create
ifconfig -a [-L] [-C] [-d] [-m] [-u] [-v] [address_family]
ifconfig -l [-d] [-u] [address_family]
ifconfig [-L] [-C] [-d] [-m] [-u] [-v]
```

要显示所有可用网络接口的名称，使用 `-l` 选项。以下示例显示存在以太网 `NIC` (`fxp0`)、并行端口 (`plip0`) 和环回口 (`lo0`)：

```bash
# ifconfig -l 列出网络接口的名称
fxp0 plip0 lo0
```

要显示特定以太网卡的设置，请在命令后添加接口名称。例如，查看 `fxp0`（第一块有线以太网 `NIC`）的信息，输入：

```bash
# ifconfig fxp0 查看 fxp0 NIC 的设置
fxp0: flags=8843<UP, BROADCAST, RUNNING, SIMPLEX, MULTICAST> mtu 1500
options=VLAN_MTU
inet 10.0.0.2 mask 0xffffff broadcast 10.2.255
ether 00:d0:b7:a9:53
media: Ethernet autoselect (100baseTX full-duplex)
status: active
```

要显示特定网络的能力列表，使用 `-m` 选项：

```bash
# ifconfig -m fxp0 显示 NIC 信息
fxp0: flags=8843<UP, BROADCAST, RUNNING, SIMPLEX, MULTICAST> mtu 1500
options=VLAN_MTU
inet 10.0.0.204 netmask 0xffffff broadcast 10.2.255
ether 00:d0:b7:79:53
media: Ethernet autoselect (100baseTX full-duplex)
status: active
supported:
media autoselect
100baseTX full-duplex
100baseTX
10baseT/UTP full-duplex
loopback
```

`ifconfig` 命令可用于更改及显示 `NIC` 设置。要将 `NIC` 设置为 `100Mbps` 全双工，输入：



# 配置以太网接口

```bash
# ifconfig fxp0 100baseTX full-duplex 修改速度/双工
# ifconfig fxp0 查看 fxp0 NIC 的设置
fxp0: flags=8843<UP, BROADCAST, RUNNING, SIMPLEX, MULTICAST> mtu 1500
options=VLAN_MTU
inet 10.0.0.2 mask 0xffffff broadcast 10.2.255
ether 00:d0:b7:a9:53
media: Ethernet autoselect (100baseTX full-duplex)
status: active
```

要将速度设置为 `10Mbps`，输入：

```bash
# ifconfig fxp0 10baseT full-duplex 设置速度
# ifconfig fxp0 查看 fxp0 的设置
```

在某些情况下，你的网络接口可能无法工作。同样，可能存在无法通过 `sysctl` 支持的操作网络接口的方法。在这些情况下，后续章节描述了如何从命令行操作你的网络接口。

> 你的以太网 NIC 接口名称是基于支持该 NIC 所使用的驱动程序的。如果你来自 Linux 环境，你可能期望以太网接口命名为 `eth0`、`eth1` 等。在 FreeBSD 中，名称可能是 `fxp0`、`inc0` 或其他。本章中的示例使用 `fxp0` 来表示有线以太网接口。

# 第 11 章：管理网络连接

| 协议 | 接收队列 | 发送队列 | 本地地址 | 远程地址 (状态) |
| :--- | :--- | :--- | :--- | :--- |
| `tcp4` | `0` | `0` | `10.0.0.204.ssh.62963` | `ESTABLISHED` |
| `tcp4` | `0` | `0` | `10.0.0.204.ssh` | `einstein.47835 ESTABLISHED` |

如输出所示，`netstat` 显示了两个来自远程计算机的连接到本地计算机具有活跃的 `ssh` 会话。以下是 `netstat` 命令的其他一些简单示例：

```bash
$ netstat -r          显示 IPv4 和 IPv6 的内核路由表
$ netstat -rs         显示路由统计数据（错误路由、动态路由）
$ netstat -s -p tcp | less 显示 TCP 接口的详细统计信息
$ netstat -n          显示 IP 地址而非主机名的输出
$ netstat -m          显示网络内存缓冲区信息
```

# 管理网络连接

启动和停止用于连接局域网或互联网的有线以太网接口，通常在你 BSD 系统启动和关机时自动处理。但是，你可以运行 `/etc/rc.d` 目录下的脚本来启动和停止你需要的网络接口，或者编辑 `/etc/rc.conf` 文件来设置网络服务是否自动启动。

`ifconfig` 命令也可用于配置、激活和禁用接口。

# 启动和停止以太网连接

在很多情况下，当你启动 BSD 系统时，有线以太网接口之所以会出现的原因是因为 `netif` 服务在系统启动时是开启的。系统启动后，你可以使用 `netif` 脚本来停止和重启你的网络接口。

在 FreeBSD 中，启动网络接口的脚本是 `/etc/rc.d/netif`。对于其他 BSD 服务，你可以通过运行带有 `start`、`stop` 和 `restart` 等选项的脚本来启动和停止 `netif` 服务。

要将所有网络接口下线然后让它们重新上线，请以 `root` 用户身份输入以下内容：

```bash
# /etc/rc.d/netif restart      关闭并启动网络接口
Stopping: l0 fxp0 plibo.
DHCPREQUEST fxp0 255.255.255.255 port 67
DHCPACK from 10.0.0.1
bound to 10.0.0.204 -- renewal in 7200 seconds.
l0: flags=8049<UP, RUNNING, MULTICAST> mtu 16384
inet6 fe80::1%l0 prefixlen 64 scope 03
inet6 ::1 prefixlen 128
inet 127.0.0.1 mask 0xff000000
xp0: flags=8843<UP, BROADCAST, RUNNING, SIMPLEX, MULTICAST> mtu 7200
```

# 第 11 章：管理网络连接

```bash
options=8<VLAN_MTU>
inet 10.0.0.204 mask 0xffffff0 broadcast 10.0.0.255
eth 00:d0:b7:79:a5:35
media: 10bas/UTP <full-duplex>
status: active
```

使用 `start` 和 `stop` 选项分别启动和停止你的网络接口：

```bash
# /etc/rc.d/netif stop    关闭网络接口
# /etc/rc.d/netif start    启动网络接口
```

你也可以使用 `ifconfig` 命令来启用和禁用网络接口。例如：

```bash
# ifconfig fxp0 down      关闭以太网卡 (fxp0) 的网络接口
# ifconfig fxp0 -d         列出已关闭的网络接口
fxp0: flags=8802<BROADCAST,SIMPLEX,MULTICAST> mtu 1500

# ifconfig fxp0 up        启用以太网卡 (fxp0) 的网络接口
# ifconfig fxp0 -u         列出已启用的网络接口
fxp0: flags=8843=UP,BROADCAST,RUNNING,MULTICAST> mtu
```

注意，在运行带有 `down` 选项的 `ifconfig` 后，网络接口将显示为激活。当你列出接口时，`UP` 和 `RUNNING` 字样将不再出现，且数据将无法通过该接口进行任何方向的传输。

当你的网络接口启动后，可以使用一些工具来查看这些接口以及相关网卡（NIC）的信息。

# 启动和停止网络服务

你可以以类似于使用 `netif` 脚本的方式，启动和停止与你的网络接口相关的服务。安全 Shell (`sshd`) 和网络文件系统 (`nfsd`) 等服务可以根据 `/etc/rc.conf` 文件中的设置在系统启动时自动启动。

如何配置和启动网络服务的信息包含在第 10 章。要查找运行网络服务脚本时的选项，只需输入脚本路径而不带任何选项即可。例如：

```bash
# /etc/rc.d/sendmail      检查启动脚本可用选项
Usage: /etc/rc.d/sendmail [fast|force|one](start|stop|restart|rcvar|status|poll)
```

以下是启动和使用已配置网络服务的示例：

```bash
# /etc/rc.d/sshd restart   停止并启动
# /etc/rc.d/sshd reload      重新加载配置文件
```

# 使用无线连接

在 FreeBSD 中设置无线连接一直很棘手，主要是因为大多数网卡都有开源驱动。你首先需要做的事情是选择一个无线卡并使用 `ifconfig`。

# 获取无线驱动

如果你有选择余，应该购买受支持的无线卡。如果你不确定网卡的制造商和型号，如果你用的是 PCI 卡，可以使用 `lspci` 命令精确确定你拥有的是哪种。

# 配置无线接口

以下是一些 `ifconfig` 命令示例，用于为表 11-1 所示的支持网卡配置网络接口（在加载驱动后）。为了让你了解可用选项，每个无线接口行都显示了不同的选项：

```bash
# ifconfig an0 inet 10.0.1.1 netmask 0xffffff 添加 Airnet 卡接口
# ifconfig ath0 inet 10.0.1.1 - 连接 Atheros 卡到现有网络
netmask 0xffffff sid="net01" named net01

# ifconfig awi inet 10.0.1.1 - 连接 PCnet 卡 (64位 WEP)
netmask 0xffffff sid="net01"
weepmode on wepkey 045320185622
```

# 表 11-1：FreeBSD 无线卡

| 驱动名称 | 支持网卡 | 添加到 loader.conf 的行 |
| :--- | :--- | :--- |
| `an` | `Aironet 450/480` | `if_an_load="YES"` |
| `ath` | `Atheros AR5005/600` | `if_ath_load="YES"` |
| `awi` | `AMD PCnetMobile SkyLine` | `if_awi_load="YES"` |
| `cnw` | `Netwave Airfer` | `if_cnw_load="YES"` |
| `ipw` | `Intel Pro/Wireless 2100/2200BG` | `if_ipw_load="YES"` |
| `iwi` | `Intel Pro/Wireless 2915AG/2250` | `if_iwi_load="YES"` |
| `ral` | `Ralink Technology RT2500` | `if_ral_load="YES"` |
| `ural` | `Ralink Technology RT2500USB` | `if_ural_load="YES"` |
| `wi` | `Lucent Hemimes, Intersil PRISM-M, Intersil PRISM-2.5` | `if_wi_load="YES"` |

如第三列所示，如果驱动程序没有构建在内核中，你可以配置让它在计算机启动时作为模块加载。只需将该行添加到 `/boot/loader.conf` 文件中。配合特定网卡的驱动，你需要添加 `wlan 802.11` 通用驱动：

```bash
# ifconfig cnw0 10.0.0.1 \    连接 Wave Airsurfer 接入点
netmask 0xffffffff "net01" \
mode 1lg mediaocthtop

# ifconfig ipwo 10.0.0.1 \    连接 Intel Pro 2100 (104-bit WEP)
netmask 0xffffffff "net01" \
wopde on wepkey 0x010029458352241509101243212

# ifconfig iwi0 10.0.0.1 \    连接 Intel Pro 2200BG (128-bit WEP)
netmask 0xffffffff "net01" \
wopde on wepkey 0x010203040506070809101112123 weptkey 1
```

无线网卡接口配置后，你可以检查它或将其作为网络接口启用/禁用。你还可以进行一些其他操作来检查你的网络。例如：

```bash
# ifconfig iwi0             检查无线连接状态
# ifconfig ath0 down         关闭无线网络
# ifconfig ipwo up           启用无线网络
# ifconfig cnw0 scan          扫描并显示所有基站
```

在配置无线网卡后，还有其他命令可以对其操作。例如，你可以使用 `wicitron`（Anrolet 网卡）、`ancontrol`（Anrolet 网卡）和 `raycontrol`（Raylink 网卡）命令来对你的无线网卡进行操作和设置。对于 Atheros、Incel 或 Lucent 无线网卡：

```bash
# wicitron -i wi0 -o      显示与无线网卡相关的统计信息
# wicitron -i wi0 -C        显示缓存的信号强度信息
# wicitron -i wi0 -X        清除缓存的信号强度信息
# raycontrol -i ray0 -o     显示来自驱动程序的当前统计数据
# raycontrol -i ray0 -t -3  将传输速率设置为中等
# raycontrol -i ray0 -n net02 将网络名称设置为 net0
# ancontrol -i an0 -A       显示首选的接入点
# ancontrol -i an0 -S        显示 SSID 列表
```

# 检查名称解析

由于 IP 地址是数字，而人们更倾向于通过名称来标识设备，TCP/IP 网络（如互联网）依赖 DNS 将主机名解析为 IP 地址。FreeBSD 提供了多个工具来查找与 DNS 名称解析相关的信息。

当你第一次安装 FreeBSD 时，你要么识别了用于名称解析的域名系统（DNS）服务器，要么由 DHCP 服务器自动分配了这些服务器。这些信息存储在 `/etc/resolv.conf` 文件中，内容如下：

```text
nameserver 11.22.33.44
nameserver 22.33.44.55
```

上述数字会被由作为 DNS 名称服务器的计算机的真实 IP 地址替换。当你连接到可以工作的 DNS 服务器时，你可以使用命令查询这些服务器并查找主机。

你可以使用 `dig` 命令（应该使用它代替 `nslookup` 命令）从 DNS 服务器查询信息。`host` 命令可用于查找主机名或域名的地址信息。

要在你的 DNS 服务器中搜索特定主机名（在以下示例中使用 `www.turbosphere.com`），请如下使用 `dig` 命令：

```bash
# dig www.turbosphere.com
```



$ `dig` `www.turbosphere.com` 搜索 `/etc/resolv.conf` 中设置的 DNS 服务器

```
<< DIG 9.3 << www.turbosphere.com
;; global options:
;; Got answer:
;;;>>HEADER-- opcode: QUERY, status: NOERROR, id: 45
;;; flags: qr rd ra; QUERY: 1, ANSWER: 2, ADDITIONAL: 2
;; QUESTION SECTION:
www.turbosphere.com. IN A
```

除了使用分配的服务器，你还可以查询特定的服务器。如果你认为服务器没有正确解析特定主机的地址，这种方法就很有用。你可以检查不同的服务器以查看名称如何解析。以下示例查询了 `4.2.2.1` 处的 DNS 服务器：

```bash
$ dig www.turbosphere.com mx @4.2.2.1
```

使用 `dig`，你还可以查询特定类型的记录：

```bash
$ dig turbosphere.com mx      查询邮件交换器
$ dig turbosphere.com ns      查询权威名称服务器
```

使用 `+trace` 选项从顶层 DNS 服务器向下到权威服务器跟踪递归查询：

```bash
$ dig +trace www.turbosphere.com    递归跟踪 DNS 服务器
```

如果你只想获取主机的 IP 地址，请使用 `+short` 选项：

```bash
$ dig +short www.turbosphere.com  仅显示名称/IP 地址对
turbosphere.com.
66.113.99.70
```

你可以使用 `-x` 进行反向查找，以便根据 IP 地址查找 DNS 信息：

```bash
$ dig -x 66.113.99.70        根据 IP 地址获取 DNS 信息
```

你也可以使用 `host` 来执行反向 DNS 查询：

```bash
$ host 66.113.99.70
70.99.113.66.in-addr.arpa name pointer for turbosphere.com.
```

要获取主机的详细信息，使用 `host`：

```bash
$ host 66.113.99.70 -a
```

要获取主机的 IP 地址，使用 `dig -x`：

```bash
$ dig -x 66.113.99.70 -short
```

# 第11 章：管理网络连接

在本示例中，你可以看到本地计算机 ARP 缓存中的其他计算机名称，以及每个计算机网卡的关联硬件地址（MAC 地址）。要删除 ARP 缓存中的条目，请使用 `-d` 选项：

```bash
# arp -d 10.0.0.50
      从 ARP 缓存中删除 10.0.0.50
```

与其让 ARP 动态学习其他系统，你还可以使用 `-s` 选项向缓存添加静态 ARP 条目：

```bash
# arp -s 10.0.0.50 01:0B:6A:02:EC:95      将 IP 和 MAC 地址添加到 ARP
```

要查询子网以查看某个 IP 是否被占用，并找到使用该 IP 的设备的 MAC 地址，可以使用 `arping` 命令（`pkg_add -r arping`）。`arping` 命令可在桥接以太网网卡之前检查 IP 冲突。以下是示例：

```bash
# arping 10.0.0.50                                     查询子网以查看 10.0.0.50 是否被占用
60 bytes from 00:0b:6a:02:ec:98 (10.0.0.50): index=0 time=9.966 msec
60 bytes from 00:0b:6a:02:ec:98 (10.0.0.50): index=1 time=9.930 msec
60 bytes from 00:0b:6a:02:ec:98 (10.0.0.50): index=2 time=9.930 msec
60 bytes from 00:0b:6a:02:ec:98 (10.0.0.50): index=3 time=9.931 msec
^C
-- 10.0.0.50 统计
发送 4 包，接收 4 包，      0% 未响应
# arping -I fp0 10.0.0.50                    指定查询的接口
```

与 `ping` 命令类似，`arping` 会持续查询地址，直到通过 `Ctrl+C` 结束命令。通常，你只想知道目标是否存活，因此可以运行以下命令：

```bash
# arping -c 1 10.0.0.50                    查询 10.0.0.50 并在计数 1 次后停止
```

## 追踪到主机的路由

在确认 `ping` 网关可以到达网络外部的每个主机后，你可能仍然遇到访问特定主机或网络的问题。如果该功能正常，你可以使用 `traceroute` 寻找瓶颈或故障点：

```bash
$ traceroute boost.turboscope.com      追踪到主机的路由
traceoute to boost.turboscope.com (66.113.99.70) 最大 64 跳，40 字节数据包
1 10.0.0.1 (10.0.0.1) 0.281 ms 0.289 ms 0.237 ms
2 t1-03.hbi.com (51.55.111) 6.213 ms 6.189 ms 6.083 ms
3 172.172.173 (172.172.173) 14.070 ms 14.025 ms 13.974 ms
4 so-do-3-ra22.MINBI.glnet (208.448.111) 19.076 ms 19.053 ms 19.004 ms
5 01-gol-5-88.AR4.SE1.glnet (67.177.71.210) 94.668 ms 94.668 ms 94.612ms
6 64.215.311.114 (64.215.311.114) 99.643 ms 101.647 ms 101.577 ms
7 dr02-v109.tac.opticfusion.com (209.147.112.50) 262.301ms 233.316ms 233.153 ms
8 dr01-v100.tac.opticfusion.com (66.116.961.93) 93.916 ms 94.001 ms 93.953 ms
9 boost.turboscope.com (66.113.99.70) 99.251 ms 96.215 ms 100.220 ms
```

如你所见，最长的跳发生在 4（可能在明尼阿波利的 Global Crossing）和 5（西雅图的 GC）之间。这个差距并不是瓶颈；它反映了跳之间的距离。有时，最后几跳看起来像这样：

```
28 * * *
29 * * *
30 * * *
```

追踪末尾星号（`*`）行可能是由拦截流量的防火墙引起的。但如果在目标之前看到多个星号，可能表示网络拥堵或设备故障。默认情况下，`traceroute` 使用 UDP，这比 ICMP 提供更真实的图像。如果你仍然想使用 ICMP，尝试此命令：

```bash
# traceroute -I boost.turboscope.com
```

使用 TCP 追踪路由，使用 `-T` 选项：

```bash
# traceroute -T boost.turboscope.com
```

默认情况下，`traceroute` 连接端口 80。你可以使用 `-p` 设置不同的端口：

```bash
# traceroute -p 255 boost.turboscope.com
```

通过禁用域名解析查看 IP 地址：

```bash
$ traceroute -n boost.turboscope.com
```

要查看和操作内核路由表，曾使用 `route` 命令。在 Linux 中逐渐被 `ip` 命令取代，但在 BSD 中常用。你可以使用 `route` 命令显示本地路由表。这里是带和不带 DNS 的 `route` 命令示例：

```bash
# route get freebsd.org
destination: default
mask: 0.0.0.0
gateway: 10.0.0.1
interface: fxp0
flags: <UP, GATEWAY, STATIC>
recvpipe ssthresh rttvar mtu
0 0 1500 0
# route -n freebsd.org
destination: default
mask: default
gateway: 147.83.40
```

你可以使用 `add` 选项更改默认路由：

```bash
# route add default 10.0.0.2
```

你可以通过指定目标和网关 IP 地址（`10.0.0.1`）向网络添加新路由：

```bash
# route -net 192.168.0.0 netmask 255.255.255.0 gw 10.0.0.1
```

你可以使用 `delete` 选项删除路由：

```bash
# route -net 192.168.0.0 delete
```

要使路由永久，在 `/etc/rc.conf` 文件中 `defaultrouter`。例如，要在重启时将默认路由设置为 `10.0.0.2`，可以在 `/etc/rc.conf` 中添加以下条目：

```
defaultrouter=10.0.0.2
```

## 显示 `netstat` 连接和统计

另一个显示路由表信息的命令是 `netstat`。然而，`netstat` 还可以显示传输层协议（TCP 和 UDP）以及 ICMP 的数据包信息。使用 `netstat -rn` 显示路由表：

```bash
# netstat -rn      显示路由表
Routing tables
Internet:
Destination    Gateway      Flags  Refs  Use  Netif  Expire
default         10.0.0.1     UGS     0     681 fxp0
10.0.0.1        00:10:5a:ab6:a7  UHLW  2   0   fxp0  268
10.0.0.50       00:0b:6a:ec:98  UHLW  2   980 fxp0  690
127.0.0.1       127.0.0.1    UH     0     32  lo0
...
```

显示 TCP、ICMP、UDP 和协议活动的详细摘要，请输入：

```bash
$ netstat -s | less 显示 TCP, ICMP, UDP 活动摘要
tcp:
  21156 packets sent
  19743 data packets (1184618 bytes)
  207 data packets (44928 bytes) retransmitted
  62 packets unnecessarily retransmitted
  0 resends initiated by MTU discovery
  964 ack-only packets (149 delayed)
  0 urg only packets
  0 window probe packets
```

可以通过以下输入查看每个接口的 TCP 统计列表：

| Name | Mtu Network | Address | Ipkts Er | Opkts Er | Coll |
|---|---|---|---|---|---|
| fxp0 | 1500 | <Link1> | 0 | 0 | 0 |
| plip0 | 1500 | <Link2> | 0 | 0 | 0 |
| loo | 16384 | <Link3> | 0 | 0 | 0 |
| loo | 16384 | fe80:03::1 | 0 | 0 | 0 |
| loo | 16384 | localhost.loc ::1 | 4 | 4 | 0 |

你可以查看活动套接字的信息。这包含了监听网络请求的服务器进程信息：

```bash
# netstat -Aan -p tcp 活动连接（包括服务器）
Socket Proto Recv-Q Send-Q Local Address Foreign Address (state)
c2c4e0000 tcp4 0 0 127.0.1.6010 .* LISTEN
c2c4e6910 tcp4 0 0 10.0.0.204.22 10.0.50.45664 ESTABLISHED
c2c4e6570 tcp4 0 0 127.0.0.1.25 .* LISTEN
c2c4e6a60 tcp4 0 0 *.* LISTEN
c2c4e5c00 tcp4 0 0 *.949 .* LISTEN
c2c4e51d0 tcp4 0 0 *.897 .* LISTEN
c2c4e5740 tcp4 0 0 *.2049 .* LISTEN
c2c4e5ae9 tcp4 0 0 *.649 .* LISTEN
c2c4e5cb0 tcp4 0 0 *.111 .* LISTEN
```

从上面的示例中，你可以看到有一个建立的连接（来自 `10.0.0.50` 主机通过端口 22 的 `ssh` 远程登录）。其他套接字表示监听各种服务请求的进程。

## 第11 章：管理网络连接

要显示特定接口传输的数据量（字节），请使用 `-I` 和 `-b` 选项。例如：

```bash
# netstat -I fxpo -b
Name Mtu Address Ipkts Ierr Ibytes Opkts Oerr Obytes
fxpo 1500 <link1> 00:d0:b7:9a:55:33 39753 0 5213277 37430 0 4322243
fxpo 1500/24 thompson 39662 - 4651787 37388 - 3797160
```

## 其他实用的网络工具

如果你想查看系统发送和接收数据包的信息，可以使用 `tcpdump`。`tcpdump` 命令具有许多高级功能，大部分功能都围绕着过滤和在数据包海洋中捞针。如果你在远程机器上运行 `tcpdump`，你的屏幕将被你的客户端和远程机器之间所有的 `ssh` 流量淹没。要在不学习过多 `tcpdump` 过滤规则的情况下开始，请运行以下命令：

```bash
# tcpdump not port ssh # 查找所有非 ssh 相关的 TCP 数据包
```

如果你想深入研究数据包级流量，请使用 `wireshark`（以前称为 `ethereal`）。GNOME 桌面环境提供了图形化版本的 `wireshark`（`pkg_add -r wireshark`）。你可以在远程机器上通过 X 转发运行 `wireshark`。`Wireshark` 是一个非常强大的数据包嗅探器，可以与顶尖工具相美并论。

要探索网络、机器以及它们提供的服务，请使用 `nmap`（`pkg_add -r nmap`）。`nmap` 命令是最常用的端口扫描器。它甚至出现在电影《黑客帝国：重载》中。请确保你有权权扫描你正在使用的系统或网络。`nmap` 命令是 `nmap` 软件包的一部分，可以作为用户身份运行，但某些扫描需要 `root` 权限。

以下是使用 `nmap` 进行基本扫描的方法：

```bash
# nmap 127.0.0.1 # 扫描本地主机，查看 nmap 如何工作
# nmap 10.0.0.1 # 扫描 10.0.0.1 计算机上的端口
```

要从 `nmap` 获取最详细的输出，请使用 `-vv` 选项：

```bash
# nmap -vv -sP 10.0.0.0/24 # 显示 nmap 的最详细信息
```

要使用 `nmap` 扫描网络，请使用网络地址作为参数。在下面的示例中，我们添加了 `-sP` 选项来告诉 `nmap` 执行简单的 ping 扫描：

```bash
# nmap -vv -sP 10.0.0.0/24 # 扫描整个网络上的主机
```

你可以对 `nmap` 为你收集的信息进行非常具体的指定。在接下来的示例中，`-P0` 选项告诉 `nmap` 不要使用 ping（这对于扫描不 ping 响应的机器很有用）。`-O` 选项显示你所扫描机器的操作系统指纹。`-p 100-200` 告诉 `nmap` 仅扫描 100 到 200 之间的端口：

```bash
# nmap -vv -P0 -O -p 100-200 10.0.0.1 # 不 ping，操作系统指纹，端口 100-200
```



`nmap` 命令还有许多用于高级用法的选项。请参阅 `nmap` 手页（`man nmap`）以获取更多信息。

## 总结

你的 BSD 系统网络连接的几乎每个方面都可以使用命令行工具进行配置、检查和监控。你可以使用 `ifconfig` 命令查看和更改网卡（NIC）的设置。你可以使用 `netstat` 查看网络统计数据。

要启动和停止网络，`netif` 和 `ifconfig` 等命令很容易管理。当连接建立时，你可以使用 `netstat` 和 `route` 命令查看该连接的统计信息。

要检查 DNS 名称解析，请使用 `dig`、`host` 和 `hostname` 命令。检查到主机的连通性和路由的命令包括 `ping`、`arp`、`traceroute` 和 `arping`。

## 第 12 章：访问网络资源

在启动图形化 FTP 客户端的时间内，你已经可以使用命令行工具从远程服务器下载几十个文件。即使可以使用 GUI，用于传输文件、网页浏览、共享目录和读取邮件的命令也可以非常快速高效。在没有 GUI 的情况下，它们将是救命稻草。

本章涵盖了通过网络访问资源（文件、电子邮件、共享目录和在线聊天）的命令。

### 本章内容
- 使用 `elinks` 浏览网页
- 使用 `wget`、`curl`、`lftp` 和 `scp` 进行文件传输
- 使用 NFS、Samba 和 SSHFS 共享目录
- 使用 `ircii` 进行 IRC 聊天
- `mail` 和 `mutt` 电子邮件客户端

## 运行命令浏览网页

文本模式的浏览器提供了一种快速检查 Web 服务器是否正常工作，或在没有可用 GUI 的情况下从 Web 服务器获取信息的方法。曾经流行的 `lynx` 文本浏览器在大多数类 Unix 系统中被 `links` 浏览器取代，而后者又被 `elinks` 取代。

`elinks` 浏览器在终端窗口中运行。除了在终端中显示图像外，`elinks` 还可以处理大多数功能：帧、cookie、mime 类型和级联样式表（CSS）。因为 `elinks` 支持多个标签页，只要你使用终端，就很简单。

### 表 12-1：elinks 快捷键

| 快捷键 | 描述 |
| :--- | :--- |
| `Esc` | 切换 elinks |
| `q` | 退出 elinks |
| `a` | 添加当前页面 |
| `d` | 下载当前页面 |
| `s` | 显示当前图像 |
| `t` | 新标签页 |
| `h` | 查看历史 |
| `v` | 查看全局设置 |
| `g` | 查找 |
| `c` | 关闭当前标签页 |
| `>` | 下 |
| `<` | 上 |
| `/` | 页面内查找 |
| `Shift-` | 向后搜索 |
| `+` | 向前搜索 |
| `PageUp` | 向上滚动 |
| `PageDown` | 向下滚动 |
| `R` | 刷新页面 |
| `N` | 下一个结果 |
| `n` | 上一个结果 |
| `B` | 书签当前链接 |
| `F` | 查找 URL |
| `?` | 链接帮助 |
| `Enter` | 打开高亮链接 |
| `Shift-Enter` | 在新标签页中打开 |

这里有一些 `elinks` 的示例：

```bash
$ wget http://upload.wikimedia.org/wikipedia/commons/2/2c/Chollad.jpg
```

你可以在 `/etc/elinks.conf` 全局设置。用户设置存储在 `$HOME/.elinks` 目录。输入 `man elinks` 查看可用位置。

## 使用 wget 传输文件

如果你想用 `wget` 保留原始文件并进行翻译，请输入以下命令：

```bash
$ wget -pkK http://www.google.com
```
重命名为本地名称，保留原始文件

有时下载的 HTML 文件没有 `.html` 扩展名，而是以 `.asp` 或 `.cgi` 结尾。这可能导致你的浏览器不知道如何打开该本地文件副本。你可以使用 `-E` 选项让 `wget` 为这些文件添加后缀：

```bash
$ wget -E http://www.aspexamples.com
```
为下载的文件添加 `.html`

使用 `wget` 命令，你可以递归镜像整个网站。在复制整个服务器文件结构深度的文件和目录时，`-m` 选项会添加时间戳并保留 FTP 目录列表。（请谨慎使用，因为这可能会消耗大量的时间和空间）：

```bash
$ wget -m http://www.linuxutoys.net
```

使用上述的某些选项，以下命令行可以获得最实用的网站本地副本：

```bash
$ wget -mEkK http://www.linuxutoys.net
```

如果你在下载大文件（如 CD 或 DVD 镜像文件）完成前断开了连接，可能会发现 `wget` 的 `-c` 选项是救星。使用 `-c`，`wget` 将从上次停止的地方继续，恢复中断的任务。例如：

```bash
$ wget http://example.com/DVD.iso
95%======= 685,251,583 55K/s
$ wget -c http://example.com/DVD.iso
HTTP 请求，等待响应... 206 Partial Content
Length: 699,389,952 (667), 691,533 (66M) 剩余 [text/plain]
```

由于该特性（`-c`），`wget` 对于需要下载大文件的慢连接用户特别有用。如果你经历过下载几个小时的下载在完成前被中断，你就会明白我们的意思。（注意，如果你在想恢复下载时没有使用 `-c`，文件将会被保存到不同的文件中：原文件名后加一个 1。）

## 使用 cURL 传输文件

URL 客户端（`curl` 命令）提供了与 `wget` 类似的功能，用于 wget 和 FTP 协议传输文件。然而，`curl` 命令还可以使用其他流行协议传输文件，包括 SSH 协议（SCP 和 SFTP）、LDAP、DICT、Telnet 和文件。

`curl` 并不是像 `wget` 那样支持所有的递归下载，而是专为单次文件传输设计的。不过，它支持更多协议（根据需要）以及一些实用的增强功能。这里有一些使用 `curl` 传输文件的有趣示例，用于下载 FreeBSD 的三盘装 ISO 镜像：

```bash
curl -o \
ftp.freebsd.org/pub/FreeBSD/ISO-IMAGES-1386/6.3/6.3-RELEASE-1386-disc[1-3].iso

curl -o0 \
ftp.freebsd.org/pub/FreeBSD/ISO-IMAGES-1386/6.3/6.3-RELEASE-1386-disc[1,2,3].iso
```

这些命令仅说明了如何使用方括号来表示范围 `[1-3]`，以及使用花括号 `[1, 2, 3]` 来匹配字符或数字的文件。

下面这组 `curl` 命令演示了如何从受密码保护的服务器下载、更新和删除文件。

```bash
curl -OP ftp://chris:Mypasswd@ftp.example.com/home/chris/fileA \
-Q '-DELE fileA'

curl -T install.log ftp://chris:Mypasswd@ftp.example.com/tmp/ \
-Q "RNFR install.log" -Q "RNFR install.log"

curl ftp://freebsd.org/pub/FreeBSD/doc/en/books/
```
列出书籍内容

第一个命令添加了用户和密码（`chris:Mypasswd`），从服务器下载了文件（`fileA`），并在下载完成后删除服务器上的文件（`-Q '-DELE fileA'`）。下一个示例使用 `-T` 将 `install.log` 文件上传到 FTP 服务器。此后，它将远程文件重命名为 `Xinstall`。最后一个示例使用 `curl` 列出 `ftp.freebsd.org` 上 `/pub/FreeBSD/doc/en/books/` 目录的内容。

## 使用 FTP 命令传输文件

大多数 BSD 系统都带有标准的 FTP 客户端（`ftp` 命令），它的工作方式与 UNIX 和 Windows 系统上相同。我们建议你使用功能全且友好的 `lftp`（以 root 身份，输入 `pkg install -r lftp`）。

通过这些 FTP 客户端，你可以与 FTP 服务器建立会话（而不是像 `wget` 和 `curl` 那样连接文件）。然后，你可以像操作本地文件系统一样导航服务器，并通过网络连接传输文档。以下是使用 `lftp` 连接到 FTP 服务器的示例：

```bash
$ lftp freebsd.org
lftp.freebsd.org->

$ lftp francois@example.com
lftp.example.com->

$ lftp -u francois example.com
Password: *****
lftp.example.com->

$ lftp -u francois mypwd example.com
lftp example.com->
```

建立连接后，你可以在会话中执行命令。与 `wget` 和 `curl` 不同，你不需要每次都输入完整的 URL。你可以像操作本地文件系统一样导航服务器，并通过网络连接传输文档。在 `lftp` 会话中，你可以使用 `cd` 切换目录，使用 `ls` 查看内容，使用 `get` 或 `put` 传输。任何以感叹号开头的命令（如 `!ls`）都在 shell 中执行。在 `lftp` 会话中，你可以使用 `Tab` 键自动补全文件名。`lftp` 支持在后台运行任务（使用 `Ctrl+Z`），你可以使用 `bg` 让其在后台运行或使用 `fg` 将其回到前台。`lftp` 还支持目录镜像，`mirror` 命令可以用于下载或上传整个目录树。最后，输入 `exit` 退出会话。



第一个命令添加了用户和密码（`chris:Mypasswd`），从服务器下载了文件（`fileA`），并在下载完成后删除服务器上的文件（`-Q '-DELE fileA'`）。下一个示例使用`-T`将`install.log`文件上传到 FTP 服务器。此后，它将远程文件重命名为`Xinstall`。最后一个示例使用`curl`列出`ftp.freebsd.org`上`/pub/FreeBSD/doc/en/books/`目录的内容。

## 使用 FTP 命令传输文件

大多数 BSD 系统都带有标准的 FTP 客户端（`ftp` 命令），它的工作方式与 UNIX 和 Windows 系统上相同。我们建议你使用功能全且友好的`lftp`（以 root 身份，输入`pkg install -r lftp`）。

通过这些 FTP 客户端，你可以与 FTP 服务器建立会话（而不是像`wget`和`curl`那样连接文件）。然后，你可以像操作本地文件系统一样导航服务器，并通过网络连接传输文档。以下是使用`lftp`连接到 FTP 服务器的示例：

```
$ lftp freebsd.org                   匿名连接

lftp.freebsd.org->

$ lftp francois@example.com               身份验证连接

lftp.example.com->

$ lftp -u francois example.com             身份验证连接

Password: *****

lftp.example.com->

$ lftp -u francois mypwd example.com      使用密码进行身份验证

lftp example.com->

```

## 使用 SSH 工具传输文件

因为 SSH 工具是系统管理员通信工具中最重要的工具之一，配置和使用 SSH 工具的一些更复杂用法将在第 13 章介绍。然而，在最基础的形式下，SSH 工具是你在进行基础文件传输时最常用的工具。

特别是，`scp` 命令可以完成你大部分将文件传输到另一台计算机的需求，同时通过加密密码阶段和数据传输阶段来确保通信安全。`scp` 命令取代了`rcp` 命令，成为最流行的主机间文件复制工具。

> 警告！使用`scp` 覆盖现有文件时不会有警告，因此请确保目标主机不包含你想在`scp` 文件复制路径中保留的文件或目录。

## 第 12 章：访问网络资源

### 使用 scp 拷贝远程文件

使用`scp` 传输文件时，SSH 服务（通常是`sshd` 进程）必须在远程系统中运行。以下是一些实用的`scp` 命令示例：

```
$ scp myfile francois@server1:/tmp/    将 myfile 拷贝到 server1

Password: ******

$ scp server1:/tmp/myfile .    将远程的 myfile 拷贝到本地工作目录

Password: ******

```

使用`-p` 选项可以保留拷贝文件的权限和时间戳：

```
$ scp -p myfile server1:/tmp/

```

如果 SSH 服务被配置为监听默认端口 22 以外的端口，请在`scp` 命令行中使用`-P` 来指定该端口：

```
$ scp -P12345 myfile server1:/tmp/    连接到特定端口

```

若要从远程文件系统的特定位置进行递归复制，请使用`-r` 选项：

```
$ scp -r mydir francois@server1:/tmp/    将所有 mydir 拷贝到远程的 /tmp

```

虽然`scp` 在已知想要传输的文件位置时最有用，但有时交互式地浏览和传输文件会更有帮助。

### 在 sftp 和 lftp 会话中拷贝远程文件

`sftp` 命令允许你使用类似`ftp` 的接口通过 SSH 协议查找和列出目录。以下是启动`sftp` 会话的示例：

```
$ sftp chris@server1

chris@server1's password: ******

sftp>

```

像使用普通`ftp` 客户端一样使用`ftp`。输入`?` 可以查看命令列表。你可以切换目录（`cd`）、切换本地目录（`lcd`）、检查当前远程和本地目录（`pwd` 和 `lwd`），以及列出远程和本地内容（`ls` 和 `ls`）。取决于你登录用户的权限，你可能可以创建和删除目录/组（`mkdir` 和 `rdir`），并更改文件和目录的权限（`chmod` 和 `chgrp`）。

你也可以使用`lftp`（在本章稍早讨论过）作为`sftp` 客户端。`lftp` 增加了许多许多于用户的功能，例如使用 Tab 键进行路径补全：

```
$ lftp sftp://chris@server1

Password: ******

lftp chris@server1->

```

### 使用 Windows 文件传输工具

在许多情况下，人们需要使用 Windows 客户端从 BSD 服务器获取文件。如果你的客户端操作系统是 Windows，可以使用以下开源工具之一从 BSD 服务器获取文件：

- `WinSCP` (http://winscp.net)：适用于 Windows 的 SSH 和 SSH2 协议的图形化`scp`、`sftp` 和 FTP 客户端。
- `FileZilla` (www://zilla.sourceforge.net)：提供 Windows 图形化 FTP 和 SFTP 服务，并提供 FTP 服务器功能。
- `PSCP` (http://chiark.greenend.org/~sgtatham/putty/)：PuTTY 套件的一部分的命令行`scp` 客户端。
- `PSFTP` (http://chiark.greenend.org/~sgtatham/putty/)：PuTTY 套件的一部分的命令行`sftp` 客户端。

### 共享远程目录

本章在此处描述的工具提供了原子文件访问，即建立连接并一次性传输文件。在需要对远程文件目录进行更持久、持续的访问时，共享和挂载远程文件服务的将最为有用。此类服务包括网络文件系统 (NFS)、Samba 和 SSHS。

### 使用 NFS 共享远程目录

在通过 NFS 从你的 BSD 系统共享目录之前，你必须启动 NFS 服务。在 FreeBSD 中，操作方法是将来自`/etc/defaults/rc.conf` 文件的 NFS 行复制到`/etc/rc.conf` 并启用它们。以下是我们在`/etc/rc.conf` 文件中添加的内容：

```
nfs_server_enable=YES      # 此主机为 NFS 服务器（或为 NO）。

rpc_lock_enable=YES        # 运行客户端/服务器所需的 NFS rpc.lockd

rpc_statd_enable=YES       # 运行客户端/服务器所需的 NFS rpc.statd

nfs_server='u -t n 4'      # nfsd 的标志（如果已启用）

```

NFS 服务将在你下次重启 BSD 时启动。或者你也可以以 root 用户身份输入以下命令立即启动它：

```
# nfsd -u -t n 4           手动启动 NFS 服务

```

当你的 BSD 系统运行 NFS 服务时，你可以在服务器上的`/etc/exports` 文件中添加条目以与远程客户端共享目录，并使用`showmount` 命令查看可用和已挂载的共享目录。挂载共享目录是通过在标准`mount` 命令中使用特殊选项完成的。

### 从 NFS 服务器共享目录

在如所述运行 NFS 服务器后，可以通过向`/etc/exports` 文件中添加条目来从该服务器共享目录。以下是该文件的条目示例：

```
/usr/ports /usr/ports/Tools dt 001

/usr/ports -rw mapall-jake

/usr/ports -aldirs -network 10.0.0

Let dt01 mount /usr/ports, /usr/ports/

共享读写权限，所有用户映射到 jake

10.0.0 上的均可挂载所有 /usr/ports 目录

```

这些示例仅说明了 NFS 服务器如何共享目录（`/usr/ports`）、特定子网（`network`）和子目录（`aldirs`），并带有权限（`rw`）和用户映射（`mapall`）。

### 查看和导出 NFS 共享

在 BSD 系统，你可以使用`mount` 命令查看可用的共享项。例如：

```
# showmount -e

```

### 挂载 NFS 共享

使用`mount` 命令挂载远程共享。挂载点必须已经存在。示例如下：

```
# mkdir /mnt/server-share

# mount server.com:/export/myshare /mnt/server-share

```
`rw` 选项以读写权限挂载目录。

通过在`-o` 选项之后传递 NFS 特定的选项给`mount` 命令：

```
# mount -o rw,hard server.com:/export/myshare /mnt/server-share

```

### 使用 Samba 共享远程目录

Samba 是 Windows 文件和打印协议的开源实现，该协议最初被称为 SMB，现在称为 CIFS。BSD 以及许多操作系统中都有 Samba 的实现。你可以以 root 身份安装基础 Samba 包：

```
$ pkg_add -r samba3

```

要在 FreeBSD 中使用 SWAT，需要在`/etc/rc.conf` 中启用`inetd` 服务 (`inetd_enable=YES`)，并启动 SWAT (重启或执行`/usr/sbin/inetd -W -C 60`)，然后浏览器指向 SWAT 界面 (http://localhost:901) 并输入 root 用户和密码。

你可以从 SWAT 界面创建初始的`/usr/local/etc/smb.conf` 文件，也可以直接使用任何文本编辑器创建它。用于 Samba 共享的命令可以添加共享、从 SWAT 界面查看配置、查询 Samba 服务器、挂载目录和共享目录。

要启动 Samba 服务器，你可以手动运行`nmbd` 和 `smbd` 服务器。但是，如果你如上所述运行了 SWAT，你可以启动整个服务（带有相应的选项）、添加共享并从 SWAT 界面查看配置。在 Samba 界面中，选择 STATUS，然后选择 All 来启动服务。

### 查看和访问 Samba 共享

扫描网络中的 SMB 主机，请输入以下命令：

要查看网络邻域的测试表示（共享目录和打印机），请使用`smbtree`：

```
$ smbtree *****

Password: *****

MYGROUP

\THOMPSON

Samba Server Version 3.0.25a-3.fc

THOMPSON HP LaserJet 2100M 打印机
THOMPSON IPC 服务 (Samba 服务器版本 3.0.25a-3-cf)
EINSTEIN Samba 服务器
EINSTEIN HP DeskJet 5550 打印机
EINSTEIN IPC 服务 (Samba 服务器)

```

要将 BSD 用户添加到 Samba 用户中，请使用`smbpasswd` 命令：

```
# smbpasswd -a francois

New SMB password: ******

Retype new SMB password: ******

Added user francois

```

要列出匿名用户提供的服务，请输入以下：

```bash
$ smbclient -L server

Password: ******

Anonymous login successful

Domains=[MYGROUP] OS=[Unix] Server=Samba 3.0.23c

tree connect failed: NT_STATUS_LOGON_FAILURE

```

以下是针对名为 `francois` 的用户`smbclient` 输出：

```
$ smbclient -l -U francois

Password: ******

Domain=[MYGROUP] OS=[Unix] Server=[Samba 3.0.23c]

```

| 共享名称 | 类型 | 注释 |
| --- | --- | --- |
| `IPC$` | `IPC` | `IPC` 服务 (Samba 服务器版本 3.0.23c) |
| `hp5550` | 打印机 | HP DeskJet 5550 打印机 |

| 服务器 | 注释 |
| --- | --- |
| `THOMPSON` | Samba 服务器版本 3.0.23c |
| `Workgroup` | 主节点 |
| `MYGROUP` | `THOMPSON` |

要像 FTP 样式一样连接共享，请输入以下：

```bash
$ smbclient //192.168.1.1/myshare -u francois

Password:

Domain=[MYGROUP] OS=[Unix] Server=[Samba 3.0.23c]

smb: >

```

就像 FTP 客户端一样，输入`help` 或`?` 可以查看可用命令列表。同样，您可以使用常用的 shell 类型命令，如`cd`、`ls`、`get`、`put` 和 `quit` 在 SMB 主机上进行操作。

## 第 12 章：访问网络资源

### 挂载 Samba 共享

您可以像挂载本地系统或远程 NFS 文件系统一样，将远程 Samba 共享挂载到本地文件系统中。挂载共享：

```bash
# -t smbfs //francois@192.168.1.1/myshare /mnt/mymount/

```

> 注意 Samba 文件系统 (`smbfs`) 在 FreeBSD 上仍然可用，但在 Linux 系统上已弃用。如果您从 BSD 系统将 Samba 共享挂载到 Linux 系统，挂载该远程 Samba 共享时指定 CIFS (`-t cifs`) 为文件类型。

您可以使用`smstatus` 命令查看服务器上的当前连接和文件锁。这将告诉您是否有人挂载了您的共享目录，或者当前正在使用`smbclient` 连接到您的服务器：

```bash
$ smstatus

samba version 3.0.23c

PID Username Group Machine

5466 francois francois 10.0.0.55 (10.0.0.55)

Service pid machine Connected at

myshare 5644 10.0.0.55 Tue Jun 3 15:08:29 2008

```

无锁文件

要查看更简短的输出，使用`-b` 选项：

```bash
$ smstatus -b

```

### 查找 Samba 主机

NetBIOS 用于识别 Samba 中的主机。您可以使用`nmblookup` 命令通过在本地子网上广播特定的 NetBIOS 名称来确定计算机的 IP 地址，如下：

```bash
$ nmblookup thompson

querying thompson on 192.168.1.255

192.168.1.1 server1<0>

```

要查找特定子网服务器的 IP 地址，使用`-U` 选项：

```bash
$ nmblookup -U 192.168.1.0 server1

querying server1 on 192.168.1.255

192.168.1.1 server1<0>

```

## 第 12 章：访问网络资源

### 检查 Samba 配置

如果您无法使用 Samba 共享，或者在与 Samba 服务器通信时遇到其他问题，可以测试服务器上的 Samba 配置。可以使用`testparam` 命令检查您的主 Samba 配置文件 (`smb.conf`)：

```bash
$ testparam

Load smb config files from /usr/local/etc/smb.conf

Processing section "[homes]"

Processing section "[printers]"

Processing section "[myshare]"

Loaded services OK.

Server role: ROLE_STANDALONE

Press Enter to see a dump of your service definitions

```

在处理完插入的条目后，可以看到来自`smb.conf` 文件的设置。这里是之前在示例中显示的`myshare` 共享目录条目，它可能出现在`smb.conf` 文件中：

```
[myshare]

path = /home/francois

username = francois

valid users = francois

hosts allow = einstein

available = yes
```



此条目允许 Samba 用户`francois`从名为`einstein`的计算机访问`/home/francois`目录（由名称`myshare`名称表示）。该共享显示为当前可用。之前的`testparam`示例显示了您在`smb.conf`文件中设置的条目。然而，这里是`smb.conf`文件中的条目。

## 第 12 章：访问网络资源

如果你发现自己需要在远程服务器或其他文本环境中检查电子邮件，那么那些经典的基于文本的邮件客户端仍然可用，而且非常实用。事实上，一些硬核极客仍然完全使用文本的邮件客户端，推崇它们的效率，并对基于 HTML 的邮件嗤之以鼻。

本章描述的邮件客户端期望你的消息存储在本地系统的标准 MBOX 格式中。这意味着你已经登录到邮件服务器，或者已经将消息下载到本地（例如，通过 POP3 或类似的工具）。

注意：文本的邮件客户端可以读取由其他邮件客户端下载的邮件。例如，你可以通过输入`mail -f $HOME/.evolution/mail/local/Inbox`来打开你的 Evolution 邮件收件箱。

## 使用 mail 管理电子邮件

如果你只是想快速检查远程服务器上`root`用户邮箱中的邮件，最老且最易使用的命令是`mail`命令(`/bin/mail`)。如果设置了`$MAIL`变量，只需以`root`身份登录并输入`mail`即可。否则，如前所述，使用`-f`选项来直接指定邮件目录——`-f /var/mail/root`。

虽然`mail`可以交互式使用，但它经常用于发送基于脚本的电子邮件。这里是一些示例：

```
$ uname -a | mail -s 'My BSD version' chris@example.com
$ ps auxw | mail -s 'My Process List' chris@example.com
```

刚刚显示的两个`mail`示例提供了无需打开 GUI 应用程序即可发送某些文本的方法。第一个示例显示了`uname``chris@example.com`的输出。主题(`-s`)为“My BSD Version”。在第二个示例中，当前运行的进程列表(`ps auxw`)被发送给用户，主题为“My Process List”。

交互式使用时，`mail`命令默认打开当前 shell 的`$MAIL`值设置的收件箱。例如：

```
$ echo $MAIL

/var/mail/root

# mail

Mail version 8.1 6/93. Type ? for help.

"/var/mail/root": 25 messages 25 new

N 1 root@thompson.local Tue Jan 19 08:02 41/193 "X5 security run output"

N 2 root@thompson.local Tue Jan 19 08:02 73/2504 "X5 daily run output"

N 3 root@thompson.local Sat Jan 19 03:02 35/1119 "X5 security run output"

N 4 root@thompson.local Sat Jan 19 03:02 70/2419 "X5 daily run output"
```

当前消息旁边有一个大于号(`>`)。新消息开头有`N`，（非新消息）开头有`U`，如果没有字母，则表示该消息已读。底部的提示符(`$`)准备好接受命令了。

此时，你处于命令模式。你可以使用简单的命令在`mail`中进行移动并执行基础的邮件功能。输入`?`即可查看命令列表，或输入你想查看的消息编号。输入`v3`在`vi`编辑器中打开第三条消息。输入`h18`查看以`h18`开头的邮件头。要回复消息`7`，输入`r7`（输入你的消息，然后单独起一行输入一个点来发送消息）。输入`d4`删除第四条消息（`d4-9`删除从`4`到`9`的消息）。输入`:bash`退出到 shell（然后返回`mail`）。

在退出`mail`之前，请记住，退出时你查看过的任何消息都会从收件箱文件中删除，除非你保留了它们(`pre*`)。输入`x`可保留收件箱中的所有消息。要保存收件箱的更改，输入`q`留存。

使用`mail`时，你可以打开 MBOX 格式的任何文件。例如，如果你以`root`身份登录，但想打开用户`chris`的收件箱，应输入：

```
# mail -f /var/mail/chris
```

## 使用 mut 管理电子邮件

如果你想经常使用命令行邮件客户端，我们建议你使用`mut`而不是`mail`。`mail`命令有很多局限性，例如无法在不预先对附件进行编码（如使用`uuencode`命令）的情况下发送附件，而`mut`具有许多用于处理现代电子邮件需求的功能。`mut`命令是`mut`包的一部分，通过`pkg-add -r mut`安装。

像`mail`一样，`mut`也可以从脚本中弹出消息。`mut`还增加了发送附件的能力。例如：

刚刚显示的第一个示例包含了文件`email-body.txt`作为消息正文，并将文件`/tmp/version.txt`作为附件。

第二个示例发送了附件，但消息正文为空(`< /dev/null`)。

你可以通过简单输入以下命令开始`mut`邮件会话（假设使用默认`$MAIL`收件箱）：

```
$ mut
```

`/home/chris/Mail does not exist. Create it? ([yes]/no): y`

`q:Quit d:Del u:Undel s:Save m:Mail r:Reply g:Group ?:`

`+ 1 0 Jun 16 Jason Buckman (69) Try out tripwire`
`2 0 Jun 18 Billy Bob (171)`

## 第 13 章：进行远程系统管理

### 本章内容

- 配置 SSH
- 使用 SSH 远程代理
- 使用 SSH 建立隧道
- 使用 SSH 提供代理服务
- 使用私密钥配合 SSH
- 使用`screen`终端复用终端
- 访问远程桌面
- 使用 VNC 共享远程桌面

与安全 Shell (SSH) 服务相关的工具不仅允许远程登录和文件传输，还提供了加密通信以确保你的远程管理安全。通过如虚拟网络计算 (VNC) 等工具，你可以让服务器的远程桌面出现在你的客户端桌面上。本章将描述这些以及用于远程系统管理的其他。

### 使用 SSH 进行远程登录和隧道传输

BSD 系统像它们的大哥 UNIX 一样，是在大学网络中成长的。在这些网络的唯一用户是学生和教授，且网络之间大多相互隔离的时代，几乎不需要安全性。

在那个时代（1970 年代和 1980 年代）设计的应用程序和协议反映了对加密和身份验证缺乏关注。SMTP 就是一个完美的例子。这对于第一代 UNIX 工具也是如此：`telnet`、`ftp`（文件传输协议）、`rsh`（远程 shell）、`rpc`（远程复制）、`rex`（远程执行）和`login`（远程登录）。这些工具使用明文发送凭据和流量。由于由于原因，在公共、不可信的互联网上使用这些工具非常危险，并且已经被大量废弃并被安全 Shell (SSH) 命令`ssh`、`scp`、`sftp`以及相关服务所取代。

## 总结

网络命令提供了你所需的内容。本章将介绍如何使用 NFS、Samba 和 SSHFS。

# 第 13 章：进行远程系统管理

虽然旧的远程命令仍有一些用途（参见“使用旧通信工具”侧边栏），但本节大部分内容描述了如何使用`SSH`命令来处理你大部分远程通信命令的需求。

## 使用旧通信工具

尽管`SSH`提供了更好的远程通信工具，但旧的通信命令（有时称为命令）仍然包含在大多数 BSD 发行版中。某些工具的执行速度会比相应的`SSH`命令更快，因为它们不需要加密。一些老派的 Unix 管理员可能会在私有网络上偶尔使用它们，或者在旧脚本中包含它们。尽管在大多数情况下你应该忽略这些旧的远程命令，但其中一种工具在某些情况下非常有用：`telnet`。

`telnet`命令仍用于与无法运行`ssh`守护进程的网络设备（路由器、交换机、UPS 等）进行通信。尽管它存在安全风险，但某些设备制造商仍包含了对`telnet`支持。

然而，使用`telnet`命令的一种方法是对 POP3、SMTP、HTTP 等许多互联网协议进行故障排除。在底层，纯文协议本质上是自动化的`telnet`会话，在此期间，客户端（如浏览器或邮件用户代理）与服务器交换文本。唯一的区别是所使用的 TCP 端口。这是一个如何`telnet`到 Web 服务器的 HTTP 端口(`80`)的示例。

```
$ telnet www.example.com 80

208.77.188...

Connected to www.example.com.

Escape character is '^]'

GET /index.html

<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 1.1//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1.dtd">

<html xmlns="http://www.w3.org/1999/xhtml" lang="en">

<head>

<title>My Web server...</title>
```

同样，你可以`telnet`到端口`25` (SMTP) 和`110` (POP3) 的服务器，并发布适当的命令来排除邮件程序的故障。有关使用`telnet`命令排除网络协议故障的完整描述，请参阅《Linux Troubleshooting Bible》(ISBN 076456997X, Wiley Publishing, 2004) 第 505 页和 508 页。

如果你需要强制退出`telnet`会话，默认情况下使用转义序列(`Ctrl+]`)。这将停止向远程端发送你的键盘输入，并将你带到`telnet`命令提示符处，你可以在那里输入`quit`或`?`即可获取更多选项。

## 配置 SSH

如今，远程系统管理的通用工具是 Secure Shell (SSH)。SSH 命令和服务取代了所有旧的远程工具，增加了强加密、公钥和许多其他功能。在自由开源软件世界，SSH 最常见的实现是 OpenSSH (www.openssh.com)，它由 OpenBSD 项目维护。OpenSSH 同时提供客户端和服务器组件。以下是关于 SSH 的一些事实：

- 对于 Windows，你可以使用 Cygwin (www.cygwin.com) 内的 SSH 工具。但除非你已经在使用 Cygwin（一个适用于 Windows 的类 Unix 环境），否则我们推荐使用 PuTTY (www.chiark.greenend.org/uk/sgatatham/putty) 。PuTTY 是一个强大的开源 Telnet/SSH 客户端。
- 尽可能使用 SSH 版本，因为它最安全。启用 SSH 的网络应用程序可能仅支持旧的、不安全的版本。OpenSSH 支持所有版本。一些旧的 BSD 系统接受 SSH v1 和 v2 连接。较新的版本默认接受版本 2。
- 在 FreeBSD 中，要启用 SSH 服务，请检查`/etc/rc.conf`文件中包含以下行（默认应该包含）：

```
sshd_enable="YES"
```

配置服务器，编辑`/etc/ssh/sshd_config`文件。

配置`ssh`客户端，编辑`/etc/ssh/ssh_config`文件。

如果你倾向于使用图形化工具管理你的远程 BSD 系统，可以启用 X11 隧道（也称为 X11 端口转发）。通过 SSH 客户端和服务器，你可以在服务器上启动 X 应用程序并显示在客户端上。跨该连接的所有通信都是加密的。

FreeBSD 为服务器(`sshd`守护进程) 提供了 X11 转发(`X11Forwarding yes`)。你需要在客户端启用它。要为临时会话启用 X11 转发，请使用以下连接命令：

```
$ ssh -X francois@myserver
```

要为所有用户永久启用 X11 转发，请向`/etc/ssh/ssh_config`添加`ForwardX11`。要为特定用户永久启用，请将这些行添加到用户的`~/.ssh/config`中。在添加这些设置后，不再需要`-X`选项即可使用 X11 隧道。像通常一样运行`ssh`连接到远程系统。要测试隧道是否正常工作，在`ssh`进入远程机器后运行`xclock`，它应该出现在你的客户端桌面上。

SSH 隧道是使用远程图形工具的极佳方法！

## 使用 ssh 远程登录

要安全地登录远程主机，你可以使用两种不同的语法来指定用户名：

```
ssh user@host
```

或者

```
ssh -l user host
```

# 第 13 章：远程系统管理

高级网络设置（Firefox 2）。选择手动代理配置，并且在 HTTP 和其他协议的字段中输入任何内容。它们通过 SOCKS v4 工作。选择图 13-1 所示的 Firefox 连接窗口。

`![](img/a8f0676d6e7f319a693ce1963202001e_257_0.png)`

图 13-1：使用 Firefox 连接窗口进行代理配置。

要测试设置，请断开`ssh`会话并访问任何网站。你的浏览器应该提示代理错误。

在 Windows 客户端上，可以通过在`Putty`中选择`Connection -> SSH Tunnels`来相同的端口转发。

# 使用公钥认证进行 ssh

到目前为止，我们只使用了默认密码认证的`ssh`。`ssh`还支持公钥认证。这提供了几个用处：

- 脚本和`cron`任务的自动登录：通过分配空密码短，你可以在脚本中使用`ssh`进行自动登录。虽然这很方便，但也是危险，因为任何获取你密钥文件的人都可以连接到你可以连接的任何机器。也可以通过密码短语和密钥代理来配置自动登录。这是便利性和安全性之间的权衡，如下文所示。
- 双因子认证：当使用受密码短语保护的密钥进行交互式登录时，认证使用的是两个因素（密钥和密码短语）而不是一个。

# 使用公钥登录

以下是在 BSD 系统之间设置基于密钥的通信的过程。在接下来的示例中，我们使用空密码来实现无密码登录。如果你倾向于用密码短语保护密钥，只需在第一步（创建密钥对）提示时输入它即可。

在客户端系统中，以需要发起通信的用户身份登录，运行`ssh-keygen`命令来生成密钥对：

```
$ ssh-keygen

Generating public/private rsa key pair.

Enter file in which to save the key (/home/chris/.ssh/id_rsa): <Enter>

Enter passphrase (empty for no passphrase): <Enter>

Enter same passphrase as before: <Enter>

Your identification has been saved in /home/chris/.ssh/id_rsa.

Your public key has been saved in /home/chris/.ssh/id_rsa.pub.

The key fingerprint is:

ac:db:a4:9e:3f:2a:90:f5:b4:74:e0:d3:db chris@host.domain.com
```

注意，如果你按了`Enter`键创建了默认密钥名称，那么你现在有一个需要非常安全保存的私钥，尤其在这个过程中，如果你没有用密码短语保护它的话。

你现在有一个由上一个命令创建的公钥(`id_rsa.pub`)。此公钥需要安装在你想要连接的远程主机上。需要将`~/.ssh/id_rsa.pub`的内容（安全地）复制到你想要`ssh`登录到远程服务器的用户的`~/.ssh/authorized_keys`密钥中。如果多个用户使用`ssh`连接到此账户，`authorized_keys`文件可以包含多个公钥。

以你想用密钥进行`ssh`的用户身份登录远程服务器。如果你还没有`~/.ssh`目录，第一步是如下方式创建它：

```
$ cd

$ mkdir .ssh

$ chmod 700 .ssh
```

下一步是从客户端复制（安全地）公钥文件，并将其放在服务器上的`authorized_keys`文件中。这可以使用`scp`完成。例如，假设客户端名为`myclient`，用户名`chris`，输入以下内容：

```
$ scp chris@myclient:/home/chris/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

$ cat id_rsa.pub >> ~/.ssh/authorized_keys      # 添加到你的密钥中

$ chmod 600 ~/.ssh/authorized_keys            # 关闭权限

$ rm id_rsa.pub                             # 复制后删除公钥
```

此过程也可以通过编辑服务器上的`~/.ssh/authorized_keys`文本文件并将公钥粘贴到客户端来完成。

确保你通过`ssh`安全地操作，并确保不要在密钥中插入任何换行符。密钥项应该位于单行，即使它在你的屏幕上换行显示。

然后从客户端（使用你配置的客户端和服务器用户账户），你可以直接`ssh`到服务器，密钥将被使用。如果你设置了密码短语，系统将像要求密码一样提示你输入。

# 将私钥保存到 USB 闪盘中使用

如果你想将私钥存储在比硬盘更安全的地方，可以使用 U 盘（有时称为 thumbdrive 或 pen drive）：

```
$ mv ~/.ssh/id_rsa /media/THUMDRIVE1/myprivatekey
```

然后当你想使用密钥时，插入 U 盘并输入以下内容：



```bash
$ ssh -i /media/THUMDRIVE1/myprivatekey chris@myserver
```

使用带密码短语的密钥比简单密码更安全，但也更麻烦。为了让生活更轻松，你可以使用 `ssh-agent` 在会话期间存储已解锁的密钥。当你将解锁的密钥添加到运行中的 `ssh-agent` 时，你就可以使用它运行 `ssh`。

## 使用 screen：一个丰富的远程 Shell

`ssh` 命令只给你一个屏幕。如果你丢失了它，你就失去了在远程计算机上正在进行的所有操作。如果你正在处理某些重要事情，例如耗时 12 小时的编译，这可能非常糟糕。如果你想同时做三件事，例如 `vi httpd.conf`、`tail -f error_log`、`service httpd reload`，你需要进入三个 `screen` 会话。

本质上 `screen` 是终端复用器。如果你是处理服务器的系统管理员，`screen` 是管理命令行界面计算机的棒工具。除了允许多个会话外，`screen` 还让你分离并在以后重新连接到该会话。

`screen` 软件包在 FreeBSD 中可用。要在使用 `screen` 的 FreeBSD 服务器上创建并安装 `screen` 包，请在服务器上输入以下命令：

```bash
$ # cd /usr/ports/sysutils/screen

# make install
```

要使用 `screen`，从客户端系统运行 `ssh` 命令连接到安装了 `screen` 的 BSD 服务器。只需输入以下命令：

```bash
$ screen
```

如果你是从 Terminal 窗口运行 `screen`，在看到许可信息后，你应该会在窗口中看到普通的 `bash` 提示符。要控制 `screen`，按下 `Ctrl+A` 组合键，然后按另一个键。例如，`Ctrl+A` 后紧按 `?`（记作 `Ctrl+A,?`）会显示帮助屏幕。在 `screen` 运行时，可以使用一些命令和控制键来操作 `screen`。

```bash
$ screen -ls
```

列出活动屏幕：

```text
There is a screen:
7089.pts-2.myserver (Attached)
1 Socket in /var/run/screen/S-francois.
```

### 常用 `screen` 控制命令

```text
$ Ctrl+A, A      Change window title
Set window title: to My
Type a new title

$ Ctrl+A, C      Create a new window

$ Ctrl+A, "      Show active window titles

Num Flags
0   My Server     Up/down arrows change windows
1   bash

$ Ctrl+A, Ctrl+D Detach screen from terminal
$ screen -ls     List active screens

There is a screen:
7089.pts-2.myserver (Detached)
1 Socket in /var/run/screen/S-francois.
```

刚刚显示的 `screen` 会话创建了两个窗口（每个窗口运行一个 `bash` shell）。你可以创建任意数量的窗口，并按需命名。此外，与其从 `screen` 会话中分离，你也可以通过退出每个打开窗口中的 shell 来关闭它（输入 `exit` 或 `Ctrl+D`）。

当 `screen` 会话被分离（detached）时，你将返回到首次登录服务器时打开的 shell。你可以按照下文“连接到 screen 会话”部分的描述重新连接到该 `screen` 会话。表 13-1 显示了 `screen` 可用的其他有用控制键序列。

### 表 13-1：使用 screen 的控制键

| 键位 | 描述 |
| :--- | :--- |
| `Ctrl+A, ?` | 显示 `screen`。 |
| `Ctrl+A, C` | 创建新窗口。 |
| `Ctrl+A, Ctrl+D` | 从终端分离 `screen`。`screen` 会话及其窗口将继续运行。 |
| `Ctrl+A, "` | 查看窗口列表。 |
| `Ctrl+A, '` | 提示输入要切换到的窗口编号或名称。 |
| `Ctrl+A, Ctrl+N` | 如果有多个 `screen` 窗口，则跳转到下一个窗口。 |
| `Ctrl+A, n` | 查看下一个窗口。 |
| `Ctrl+A, P` | 查看上一个窗口。 |
| `Ctrl+A, A` | 重命名当前窗口。 |
| `Ctrl+A, W` | 在标题栏显示窗口名称列表。 |

## 重新连接到 screen 会话

从 `screen` 会话中分离后，你以后可以再次返回该 `screen`（即使在注销并断开服务器连接后）。当只有一个 `screen` 在运行时，输入以下内容进行**重新连接**：

```bash
$ screen -r
```

如果有多个 `screen` 会话在运行，`screen -r` 将无法工作。例如，以下显示当有两个已分离的 `screen` 会话运行时的情况：

```bash
$ screen -r
```

有几个 `screen` 处于开启：

```text
7089.pts-2.myserver (Detached)
7263.pts-2.myserver (Detached)
```

输入 `screen [-d] -r [pid].tty.host*` 来恢复其中一个。

根据输出，你可以通过名称识别你想要的 **screen** 会话（默认情况下，该名称是会话进程 ID、tty 名称和主机名的组合）。例如：

```bash
$ screen -r 7089.pts-2.myserver
```

## 命名 screen 会话

与其使用默认名称，你可以在启动 `screen` 时为会话创建更具描述性的名称。例如：

```bash
$ screen -S mysession

$ screen -ls
```

有一个 `screen` 开启：

```text
26523.mysession (Attached)
```

## 共享 screen 会话

**screen** 命令允许共享 `screen`。此功能对于技术支持非常有用，因为连接到会话的每个人都可以向当前会话输入内容并观察！在前节中创建新的 `screen` 使这变得更容易。由于你正在共享屏幕，出于安全考虑，请使用临时账户或临时密码。然后另一台计算机上的人员可以 `ssh` 到服务器（使用相同的用户名）并输入：

```bash
$ screen -x mysession
```

与 `screen -r` 一样，如果只有一个 `screen` 在运行，你不需要指定要连接到哪个 `screen`：

```bash
$ screen -x
```

## 使用远程 Windows 桌面

许多习惯了 BSD 桌面的系统管理员倾向于尽可能从 BSD 管理他们的 Windows 系统。BSD 系统提供了如 `desktop` 和 `tclient` 等工具，允许你连接到运行 Windows Terminal 服务的 Windows 系统。

注意：由于没有 BSD 或其他微软专有远程桌面协议 (RDP) 的实现，因此 FreeBSD 中没有启用 RDP 的 Windows 桌面方法。如果你对加密远程桌面解决方案感兴趣，请参考使用 SSH 加密远程桌面的项目，例如 NoMachine (`www.nomachine.com`)。

为了从 FreeBSD 连接 Windows 系统桌面，你必须在 Windows XP（或其他版本）中右键点击“我的电脑”并选择“属性”。然后从系统属性窗口中选择“远程”选项卡，并勾选“允许远程连接到此计算机”。选择你允许连接到 Windows 机器的用户并点击确定。

现在，从 FreeBSD，你可以取消勾选或输入以下命令使用 `tclient` 连接到 Windows 桌面：

## 使用 tclient 连接到 Windows 桌面

如果你正在使用 Windows Desktop（以前称为 XDM）连接到你的桌面，可以使用以下命令：

# 第13 章：进行远程系统管理

在 Windows 上，你需要运行 X server。一个免费的解决方案是 `Cygwin`，它包含了 X server。也有功能丰富的商业 X server，但它们可能非常昂贵。为了跨操作系统平台共享远程桌面，我们建议你使用虚拟网络计算（VNC）。

## 使用 VNC 共享桌面

虚拟网络计算（VNC）由服务器和客户端软件组成，允许你从一台计算机远程控制另一台计算机的完整桌面显示。在 FreeBSD 和类似的系统中，你需要 VNC 软件包来访问显示器（客户端）上的远程桌面，或从你的计算机（服务器）共享桌面。要安装这些 VNC 客户端和服务器组件，请输入以下命令：

```bash
# pkg_add -r vnc
```

VNC 客户端适用于所有人，并可与许多不同的操作系统互操作。VNC 服务器可用于 BSD、Linux、Windows (32位)、Mac OS X 和 UNIX 系统。VNC 客户端在这些以及许多其他系统（包括 OS/2、PalmOS，甚至作为浏览器中的 Java 应用程序）中均提供。

> 注意：开放访问权限以操作桌面代表存在安全风险。你可以通过仅在本地主机上运行 VNC 服务器，然后让远程用户使用 SSH（或 Windows 系统上的 Putty）连接到机器来帮助最小化风险。

## 设置 VNC 服务器

由于 VNC 是按用户共享桌面的，你可以从登录你想要共享的桌面的用户开始。作为该用户，你需要创建一个 VNC 密码并启动 VNC 服务器。方法如下：

1.  创建一个用于存放 VNC 设置的目录：

    ```bash
    $ mkdir $HOME/.vnc
    ```

2.  为该用户创建一个 VNC 密码：

    ```bash
    $ vncpasswd

    Password: *******

    Verify: ********
    ```

3.  最后，你可以通过直接从 shell 运行 `vncserver` 来启动 VNC 服务 (`vncserver`)，或者将该命令添加到系统每次启动时运行的启动文件中。现在，运行以下命令来启动 VNC 服务器：

    ```bash
    $ vncserver
    ```

如果你正在使用系统内置的防火墙，请确保已为 VNC 开放端口。每个显示器运行在自己的端口上。显示器 N 通过 TCP 端口 `5900+N` 访问。例如，显示器 1 可以通过端口 `5901` 访问。有关防火墙的更多细节请参考第14章。

`vncserver` 命令将启动一个 Xnc 进程来监听第一个可用显示器（可能是 `:1`）。它还会创建一套在有人连接到服务器时启动的基础 X 应用程序（在 `$HOME/.vnc/xstartup` 文件中）。你可以根据需要添加或更改这些应用程序，包括窗口管理器 `twm`（默认值）。该目录下包含日志文件和 VNC 密码文件。

一个 VNC 客户端可以访问你的计算机，并按照下一节描述连接到你的 VNC 服务。如果你是临时设置 VNC 服务，且客户端正在连接到你的 VNC 服务，可以通过以下方式杀死 VNC 服务器：

```bash
$ vncserver -kill :1

Killing Xnc process ID 49901
```

## 启动 VNC 客户端

当 VNC 服务器运行时，你可以从之前提的任何客户端系统（BSD、Windows、Linux、Mac OS X、UNIX 等）连接到该服务器上的桌面。例如，假设你的 VNC 服务器位于名为 `myserver` 的系统上，你可以输入以下命令从另一个 BSD 系统启动远程桌面：

```bash
$ vncviewer myserver:1      Connect to VNC service on myserver display 1
```

你也可以使用 `tclient` 进行连接；对于此示例，你会将 `myserver:1` 指定为计算机和协议。默认情况下，一旦你通过 VNC 连接，得到的是一个基础窗口管理器 (`twm`) 和一个终端。为了在用户下次登录时获取完整桌面，你应该编辑 VNC 服务器上的 `$HOME/.vnc/xstartup` 文件。作为启动服务器的用户登录并输入：

```bash
$ vi $HOME/.vnc/xstartup
```

在编辑该文件时，更改行以包含你想要的窗口管理器（替换 `twm`）和你想要的应用程序（替换 `xterm`）。以下是该文件的内容示例：

```bash
#!/bin/sh

xrdb $HOME/.vnc/resources

vncconfig -solid grey

xterm -geometry 80x24+10 -title "VNC Desktop" &

twm &
```

在旧版本的 VNC 中，该文件可能不存在。因此创建它并添加上述行。运行文件后，设置权限如下：

```bash
# chmod 755 $HOME/.vnc/xstartup
```

然后，为了使更改生效，你需要重启 VNC 服务器。

## 在不可信的网络上使用 VNC

VNC 被认为是不安全的协议。密码使用加密，但会话的其他部分没有任何加密。因此，当在不可信的网络或互联网上使用 VNC 时，我们建议通过 SSH 隧道使用。有关 SSH 如何工作的通用描述，请参考前面的“远程登录”部分。要将 `myserver` 上的 VNC 显示 `:0`（端口 `5900`）转发到本地端口，请输入：

```bash
$ ssh -L 5900:localhost:5900 user@myserver
```

如果客户端上已经运行 VNC，可以将服务分配给任意端口。例如：

```bash
$ ssh -L 5901:localhost:5901 user@myserver

$ vncviewer localhost:5901
```



## 使用 Vino 共享桌面

> **注意**：如果你经常使用 VNC，可能想要看看 `tightvnc`。`tightvnc` 项目提供了具有新功能和优化的开源 VNC 实现。这些功能包括内置 SSH 隧道。

如果你运行 GNOME 并希望共享现有的 GNOME 桌面（显示 `:0`），你可以使用 `Vino`（以 root 运行 `pkg_add -r vnc`）。从 GNOME 桌面面板选择 `System > Preferences > Remote Desktop` 显示如图 13-3 所示的远程桌面窗口 (`vino-preferences`)。

在远程桌面窗口中，“允许用户查看你的桌面”复选框允许 VNC 查看器查看你的桌面；相反，勾选“允许他人控制你的桌面”允许他人使用鼠标和键盘操作你的桌面。如果选择了“向你确认”，远程请求查看桌面之前会弹出一个窗口。勾选“要求用户输入密码”是防止无密码用户查看桌面的好主意。（确保密码至少有八位。）

![](img/a8f076d6e7f319a693ce19320201e_269_0.png) 让用户查看并可能控制你的桌面。

远程桌面设置窗口指出，你可以从另一个 BSD 系统（显示地址和显示器编号）使用 `vncviewer` 将共享桌面显示到另一个系统。然而，许多操作系统的 VNC 客户端也应该有效。

## 总结

如果你发现自己处于需要管理多个 BSD 系统的境地，你拥有一套丰富的 BSD 系统远程管理命令。安全 Shell (SSH) 提供了客户端与服务器之间用于远程登录、隧道和文件传输的加密通信。

虚拟网络计算（VNC）允许一个 BSD 系统与客户端系统共享桌面，使远程桌面直接出现在客户端桌面上。通过 `Vino` 之类的工具，你甚至可以这样共享桌面：使得 VNC 服务器和客户端同时从同一个桌面工作。

# 第 14 章：锁定安全性

加固你的 BSD 系统意味着许多方面。为了确保安全，你需要限制对系统用户账户和服务的访问。然而，在此之后，安全意味着检查没有人绕过你设置的防御。

FreeBSD、NetBSD、OpenBSD 以及其他基于 BSD 发行版的系统在许多方面都被设计成是安全的。这意味着没有空密码的用户账户，防火墙默认是限制性的，并且大多数网络服务（Web、FTP 等）默认情况下都是关闭的（即使安装了该服务的软件）。

作为设置 BSD 系统的人员，你可以超越默认设置来让你的系统更加安全。例如，通过在 `jail` 中设置服务，你可以防止入侵者访问受损服务之外的系统部分。通过加密关键数据，你可以让他人使用被盗数据变得几乎不可能。

| 本章内容 |
| :--- |
| 使用 `adduser` 添加用户账户并更改用户设置 |
| 使用 `rmuser` 删除用户 |
| 使用 `passwd` 添加和更改密码 |
| 使用 `last` 和 `now` 查看谁登录了 |
| 使用 `ipfw` 配置防火墙 |
| 使用 `Syslog` 管理日志文件 |
| 使用 `tripwire` 和 `chkrootkit` 查看高级安全性 |

本章中的许多命令可用于检查和改进你的 BSD 系统的安全性，一些基础 BSD 特性特别针对安全性设计。

## 用户与用户组的操作

在大多数安装过程中，您会被要求为 `root` 用户分配一个密码（用于系统管理）。然后，您可能被要求创建一个您自定义的用户名并同样分配一个密码（用于日常计算机使用）。

我们鼓励您以普通用户身份登录，仅在需要时使用 `sudo` 访问 `root` 账户。（事实上，默认情况下，不允许通过 `ssh` 以 `root` 用户身份远程登录到 BSD 系统。）安装 FreeBSD 后，您可以使用命令或图形化工具添加更多用户、修改用户账户并分配更改密码。

## 通过 GUI 管理用户

对于带有 X 的 GNOME 桌面系统，您可以使用“用户管理器”（管理-用户和组）窗口来管理用户和组。在管理服务器用户账户时，一种选择是使用基于的 GUI。

最常用的通用工具是 `Webmin` (www.webmin.com)。出于安全考虑，请确保不要在默认端口 (`1080`) 上运行 `Webmin`。或者，更好的做法是通过 SSH 隧道运行 `Webmin` 服务，以确保通信加密。您也可以使用特殊用途的 Web 界面。例如，有许多主机托管自动化 GUI，如 `cPanel` (www.cpanel.com)、`Plesk` (www.swsoft.com/plesk) 或 `Ensim` (www.ensim.com)。

## 添加用户账户

要添加新用户，您可以使用 `adduser` 命令。通过选项，`adduser` 会引导您输入添加用户账户时所需的信息。以下是使用 `adduser` 交互式添加用户的示例：

```
# adduser 一个交互式会话以添加用户

Username: jimbo

Full name: James Bolatter

Uid (留空使用默认值):

Login group [jimbo]

Login group is jimbo: 邀请 jimbo 加入其他组? []:n

Login class [default]:n

Shell (sh csh tcsh bash login) [sh]: bash

Home directory [/home/jimbo]

Use password-based authentication? [yes]:n

Use an empty password? (yes/no) [no]:n

Use a random password? (yes/no) [no]:n

Enter password: ******

Enter password again: ********

创建后锁定账户? [no]:
```

用户名必须为 1 到 16 个字符。大多数人使用小写字母和数字，第一个字符为字母。默认用户 UIDs (`Uid`) 从 1001 开始。默认组是一个与用户名同名的新组。

登录类（Login class）与所有类 Unix 系统都不一样。默认类最适合普通用户（稍后将介绍登录类）。基于密码的验证 (yes) 是标准的验证方式。请选择一个良好的密码（稍后也可以根据需要选择多个密码）。

在您回答完所有问题后，您将有机会查看并确认最终生成的账户信息。

```
Username : jimbo

Password : *****

Full Name : James Bolatter

Uid : 1005

Class : 

Groups : jimbo

Home : /home/jimbo

Shell : /usr/local/bin/bash

Locked : no

OK?(yes/no):

Add user? (yes/no): no

再见!
```

如您所见，主目录是 `/home/jimbo`。分配了 `bash` shell，以替换 `sh` 成为默认 shell（例如为了其更样化的功能而使用 `bash`）。显然，这是您系统上配置的第五个用户（`Uid` 1005）。

根据您刚刚添加的用户的登录类，会发生一些事情。对于默认用户类，`/etc/passwd` 文件中会添加该用户的条目并创建用户的主目录。之后，来自 `/usr/share/skel` 目录的文件会被添加到用户的主目录中，并且用户会被添加到 `/etc/group` 文件中的选定组账户。`/var/mail` 目录中也会添加一个以用户命名的邮件文件。

这是一个简单的示例。随后的示例将展示您可能想要利用的其它功能，例如密码过期或分配不同的登录类。然而，下一个示例将展示如何一次性添加大量用户。

## 批量添加用户

如果您想一次性向系统添加大量用户，可以创建一个账户列表文件并将其传递给 `adduser` 命令。如果您需要一次性添加很多用户，或者希望在多台机器上使用同一组用户，这将非常有用。

在 `adduser` 使用的配置文件中，每个用户由一个 10 字段、单行、冒号分隔的条目表示。文件名可以是任何名称。您只需要使用 `-f` 选项向 `adduser` 命令标识它即可。这是一个我名为 `users.txt` 的文件示例：

```
welson:2001:2001:::Walter Nelson:home/wnelson:/usr/local/bin/bash:myKulPw

jbjing:2002:2002:::James Bing:home/jbing:/bin/csh:Nmaikar

sjohnson:2003:2003:::Sara Johnson:home/sjohnson/sh:dwzdwn

njames:2004:2004:::Nick James:home/njames:/usr/local/bin/bash:MkMydaE
```

传递给 `adduser` 命令的文件格式具有 10 个冒号分隔的字段：用户名、`uid`、`gid`、登录类、全名、主目录、shell 和密码。

您不需要填写每个字段，大多数情况下使用默认值即可。上述命令的输出的 `/etc/passwd` 文件内容如下：

```
welson:2001:2001:::Walter Nelson:home/wnelson:/usr/local/bin/bash:myKulPw
```

当文件创建且组已添加后，运行 `adduser -f /users.txt` 以查看：
成功将用户 `welson` 添加到数据库。
成功将用户 `jbjing` 添加到数据库。
成功将用户 `sjohnson` 添加到数据库。
成功将用户 `njames` 添加到数据库。

等等，您不需要更改每个设置。大多数情况下使用默认值即可。上述命令输出的 `/etc/adduser.conf` 文件如下：

```
# adduser(8) 的配置文件

# 注意：只有*部分*变量会被保存。

# 最后修改时间：2008年2月13日 星期三 11:14:01 CST

defaultgroup=users

defaultclass=

defaultgroups=acme

passwordtype=yes

homeprefix=/usr/people

shell=/usr/local/bin/bash

ucodir=/usr/share/skel

msgfile=/etc/adduser.msg

disableflags=
```

## 设置用户账户默认值

您可以通过在 `/etc/adduser.conf` 文件中放置这些默认设置来为 `adduser` 创建自定义默认值。最初的方法是通过 `adduser` 命令本身（注意添加的任何附加组必须存在）：

```
# adduser -C 创建 adduser 默认值并添加到 /etc/adduser.conf

Uid (留空使用默认值):

Login group []: sales

Enter additional groups [: acme

Login class [sh bash ksh nologin] [sh]: bash

Home directory [/home/]: /usr/people

Use password-based authentication? (yes/no): yes

Use an empty password? (yes/no) [no]: no

Use a random password? (yes/no) [no]: no

创建后锁定账户? [no]: no

Pass Type : yes

Class : 

Groups : sales acme

Home : /usr/people

Shell : /usr/local/bin/bash

Locked : no

OK? (yes/no): yes
```

大多数情况下，`/etc/adduser.conf` 中的设置是管理员运行 `adduser` 时提供给用户账户使用的。您可以手动编辑 `adduser.conf` 文件，以便在以后更改任何这些设置。输入 `man adduser.conf` 查看此文件中可用设置的说明。

## 在添加用户时使用选项

`addUser` 有一些命令行选项用于覆盖默认设置。例如，你可以如下所示更改主目录的默认位置：

`# addUser -d /usr/people 将 /usr/people 分配给创建主目录`

要使用不同的 shell，如下所示使用 `-s` 选项：

`# addUser -s /bin/csh 将 /bin/csh 分配为默认 shell`

输入 `-a /usr/share/skel` 可以查看在创建用户账户时将复制到每个用户主目录中的文件。你可以向该目录添加任何你希望在用户账户创建时复制到用户主目录的文件或目录。若要更改 `skel` 目录的位置，请使用以下命令：

`# addUser -k /usr/share/myskel 使用 myskel 目录存放初始用户文件`

要跳过 `/etc/addUser.conf` 文件中的默认值而使用系统默认值，请如下所示使用 `-N` 选项：

`# addUser -N 不使用来自你的 addUser.conf 的默认值`

通常，`addUser` 会尝试为你要添加的新用户创建主目录。如果你想明确不创建新的主目录，请输入以下：

`# addUser -D 不创建新用户的主目录`

与其使用默认登录类（称为 `default`），你可以创建或启用其他的登录类。例如，要将默认登录类更改为使用 `dialer` 登录类而不是 `default`，请输入：

```
# adduser -L dialer User 使用不同的登录类 (dialer)
```

在启动时仅启用了 `default` 和 `root` `dialer` 类（实际上还有其他几个登录类名称，但它们只是指向 `default`）。下一节描述了你可以进一步探索登录类的某些方法。

## 使用登录类

FreeBSD 中一个其他 UNIX 类系统中没有的潜在有用功能是登录类功能。当你创建一个普通用户账户时，该账户将根据 `/etc/login.conf` 文件中的项分配给默认登录类。登录类为用户提供了一份初始设置列表。通过创建其他登录类，你可以创建具有不同属性的用户组。

以下是默认登录类在 `/etc/login.conf` 文件中的定义方式：

```
passwd_format=md5:\n:copyright=/etc/COPYRIGHT:\

:welcome=/etc/motd:\

:setenv=MAIL=/var/mail,$SIZE-K,FTP_PASSIVE_MODE=YES:\

:path=/sbin /bin /usr/sbin /usr/bin /usr/games /usr/local/sbin /usr/local/bin /X1R6/bin ~~

:login=/var/run/login:

:cpuptime=unlimited:\n:datasize=unlimited:\

:stacksize=unlimited:\

:memorylocked=unlimited:\

:memoryuse=unlimited:\n:filesize=unlimited:\n:coredumpsize=unlimited:\n:maxproc=unlimited:\n:bsize=unlimited:\n:vmemoryuse=unlimited:\n:priority=0:\

:ignorename=:\n:umask=022:
```

查看默认登录类可能会回答你关于每个用户的初始设置从何而来的问题。以下是如何设置功能以及你可能如何更改它们的描述：

- `passwd_format=md5:` 新或更改的密码将使用 `md5` 加密。你也可以将其设置为 `des` 或 `blf`，如果它们使用这些加密类型的话。
- `copyright=/etc/COPYRIGHT:` 指定一个包含额外版权信息的文件。如果你的系统包含其他受版权保护，你可以向此文件添加自己的版权信息。
- `welcome=/etc/motd:` 将每日消息（message of the day）分配给 `/etc/motd`。当用户首次登录时，会显示此文件中的文本。
- `setenv...:` 设置几个 shell 变量（例如用户邮箱的位置）。
- `path...:` 设置用户的初始路径。（预计此路径将被其他设置中的设置替换）。
- `nologin=/var/run/login:` 通知用户是否存在 `/var/run/login` 文件。
- `priority=0:` 这是 `nice` 级别（进程优先级）。
- `umask=022:` 设置 `umask`，使得用户默认情况下具有读写权限。

查看默认登录类可能会回答你关于每个用户的初始设置从何而来的问题。以下是如何设置功能以及你可能如何更改它们的描述。

## 修改用户账户

创建用户账户后，信息分布在多个位置。要更改基本用户信息，可以使用 `vipw` 命令。之所以使用 `vipw` 而不是直接打开文件，是因为 `vipw` 会锁定密码文件，以防内容不同步。这是一个示例：

```
mike:1006:Mike Smith:/home/mike:/csh
```



# 第 14 章：锁定安全性

在此示例中，用户名是 `mike`，用户 ID 和组 ID 为 `1006`。用户的全名为 `Mike Smith`。主目录是 `/home/mike`，默认 shell 是 `/bin/csh`。第二个字段中的星号表示了密码。

## 删除用户账户

通过 `rmuser` 命令，你可以从系统中删除用户账户，以及其他文件（主目录、邮件池文件等，取决于你的选择）。示例：

```bash
# rmuser jjones  删除用户账户

匹配密码项：

jjones*:1009:1009:0:0:John W. Jones:/home/jjones:/bin/csh

```

> 这是你想要删除的项吗？是  
> 删除主目录 (/home/jjones)?是  
> 删除 (jjones): 邮件池密码。

如你所见，除了从 `/etc/passwd` 文件中删除项外，你还有机会删除用户的主目录。如果你说是，`rmuser` 将删除密码文件、主目录和邮件池文件（在这种情况下为 `/var/mail/jjones`）。

除了刚才提到的 `rmuser` 命令，它还会做其他事情。这些包括删除 `crontab`、杀死作业、杀死所有进程、删除临时文件以及移除用户的组关系。以下是删除账户的其他选项：

```bash
# rmuser -v jjones  删除用户账户，对所有问题回答是

删除用户 (jjones): 邮件池密码。

# rmuser -v jjones  在删除用户时提供更详细的输出

匹配密码项：

jjones*:1009:1009:0:0:John W. Jones:/home/jjones:/bin/csh

```

> 这是你想要删除的项吗？是  
> 删除主目录 (/home/jjones)?是  
> 移除 (jjones) 的 crontab:.  
> 移除由 (jjones) 拥有的 (1) 作业: 0 已移除

# 第 14 章：锁定安全性

## 移除 IPC 机制

终止所有属于 `(jjones)` 的进程：向 `3` 个进程发送了 `-KILL` 信号。  
移除 `/temp` 中由 `(jjones)` 拥有的文件：已删除 `28` 个。  
移除 `/var/tmp` 中由 `(jjones)` 拥有的文件：已删除 `3` 个。  
移除 `(jjones)` 的邮件队列：`/var/mail/jjones`。  
从系统中移除用户 `(jjones)`（包括主目录）：完成。

## 管理密码

添加或更改密码通常可以使用 `passwd` 命令简单地完成。除了 `passwd` 外，还有诸如 `chfn` 和 `vipw`（前文已描述）等用于处理用户密码。

普通用户只能更改自己的密码，而 `root` 用户可以更改任何用户的密码。例如：

```bash
$ passwd  更改普通用户自己的密码

Changing local password for chris

Old Password: ********

New Password: ********

Retype Password: ********

# passwd joseph  Root 可以更改任何用户的密码

Changing local password for joseph

New Password: ********

Retype Password: ********

```

在第一个示例中，普通用户 `(chris)` 更改了自己的密码。在登录状态下，用户必须在输入新密码之前输入旧密码。与其他 UNIX 类似系统不同，`passwd` 会防止用户使用过短、基于字典单词、不包含不同字符或其他易于猜测的密码。因此，让用户自己选择良好的密码是非常关键的。

在第二个示例中，`root` 用户可以在不需要旧密码的情况下更改任何密码。同样，`root` 用户也可以分配短或易于猜测的密码，因此在选择良好密码的同时也应保持严谨。

密码应至少包含 `8` 个字符，由字母和其他字符（数字、标点符号等）组合，且不应包含真实的单词。正如本章前面提到的，密码要易于记忆但难以猜中。

## 添加组

每个用户被分配到一个或多个组。你可以随时创建组并将用户添加到这些组中。在 BSD 系统中，每个组使用文件和目录的权限取决于每个项目上组权限的设置情况。将用户分配到组允许你对文件、目录和应用程序关联所有权，这些用户可以共同完成某个项目或共同访问资源。

虽然有图形化工具可以添加、删除和修改组（例如 GNOME 中的“用户和组”窗口），但大多数管理员必须手动编辑 `/etc/group` 文件来处理组。`/etc/group` 文件的格式类似于以前的 `/etc/passwd` 文件。

以下是 `/etc/group` 文件的简化版本，用于说明几个组：

```bash
wheel:*0
tty:*4
operator*:5:root
mail:*6
bin:*7
www:*80
nogroup:*65533
nobody:*65534
cups:*193
sales:*1001:curt,mike,sally
wnelson:*2001:
jbjing:*2002:mike,sally
```

`/etc/group` 文件的结构为：组名、密码（可选）、组 ID (GID) 以及分配给该组的用户。通常，密码字段仅包含一个星号 (`*`)。用户以逗号分隔的列表列出。

FreeBSD 的组规范包括普通用户账户从 `1001` 开始。`100` 以下的账户是管理组。特殊组（通常用于跨网络接口映射用户的组权限）包括 `nogroup` (GID `65533`) 和 `nobody` (GID `65534`)。

当你使用 `adduser` 命令添加用户时，默认会创建一个新组并将 ID 分配给它。这种方法确保在保护用户创建的文件权限时不需要过多的留心。如果其他用户需要共同进行项目，可以将他们添加到该用户的组。

如果你使用任何现有的组，`wheel` 组是你最感兴趣的。将用户添加到 `wheel` 组是为其提供 `root` 权限的常用方法。

请记住，删除组或用户不会删除该组或用户拥有的文件、目录、设备或其他项目。如果你对分配给已删除用户或组的文件或目录列列表 (`ls -1`)，将显示被删除用户或组的 UID 或 GID，而不是用户名或组名。

## 检查用户

在创建用户账户并让这些用户使用你的计算机后，你可以使用几个命令来跟踪他们如何使用你的计算机。

其他章节涵盖的检查 BSD 系统用户活动的命令包括：

- 使用 `find` 命令在系统任何地方搜索属于所选用户的文件（第 4 章）。
- 使用 `du` 命令查看所选用户主目录占用的磁盘空间（第 7 章）。
- 使用 `fuser` 和 `top` 等命令查找用户正在运行哪些进程（第 9 章）。

除了上述命令外，还有一些命令可以在登录系统时检查情况并获取系统中账户用户的通用信息。以下是获取登录系统人员信息的命令示例：

```bash
$ last 列出最近的成功登录

chris tty3 Sun Oct 5 18:05 still logged in
chris tty1 Sun Oct 5 18:05 still logged in
```

## 第 14 章：锁定安全性

位于 `/etc/rc.d` 目录下的脚本。这些脚本可以使用简单的参数运行，例如 `start`、`stop` 或 `restart`，以启动它们提供的服务。

- `rc.conf` 文件：`rc.d` 脚本在何时以及如何运行由 `rc.conf` 文件中的条目决定。`/etc/defaults/rc.conf` 文件包含了可用服务的默认设置。然而，它还包含许多被注释掉的行，取消注释并修改后即可启动 `/etc/rc.d` 目录中的服务脚本。要更改服务的默认启动方式，你可以创建一个 `/etc/rc.conf` 文件，然后从原始的 `rc.conf` 文件中复制并取消对应的注释。

当 FreeBSD 和其他 BSD 系统启动时，系统会读取 `rc.conf` 文件并启动相应的服务（带有相应的设置）。本节的开头将向你展示可以添加到 `/etc/rc.conf` 文件中的条目，用于启动和保护各种网络服务。（请参考第 12 章关于启用 NFS 和 Samba 网络的基本方法）。

**警告！** 如果你在 `/etc/rc.conf` 文件中犯错，该错误可能导致系统无法完全启动。编辑 `/etc/rc.conf` 文件时请务必小心（并准备好磁盘以防万一）。

以下示例来自 `/etc/defaults/rc.conf` 文件的网络配置子部分。通过在你自己的 `/etc/rc.conf` 文件中添加以下设置，你可以启用请求的服务。要立即启动服务，请运行最新的启动脚本：

```bash
# /etc/rc.d/ftpd start  在启用后启动 FTP 服务
```

启动脚本通常会启动一个守护进程（在本例中为 `ftpd`）。下面章节中的示例展示了在 `/etc/rc.conf` 文件中添加不同标志时，生成的守护进程是如何运行的。

- Syslog 守护进程 (`syslogd`)：将这些添加到 `/etc/rc.conf` 以配置 `syslog` 在启动机时启动：

通过在 `syslog_flags` 用引号中指定其他选项，你可以更改 `syslog` 守护进程的操作方式。以下说明了 `syslog` 命令行：

```bash
# /usr/sbin/syslogd -s 默认。仅记录本地消息（安全模式）
# /usr/sbin/syslogd -4 仅在 IPv4 地址上记录数据
# syslog_flags="-s" 给 syslog 的标志（如果已启用）
# /usr/sbin/syslogd -a 192.168.0.54 让 syslog 从 192.168.0.1 接收数据报
# /usr/sbin/syslogd -b 192.168.0.1/24 让 syslog 绑定到地址 192.168.0.1
# /usr/sbin/syslogd -d syslog 以调试模式运行（检查 syslog 是否损坏）
# /usr/sbin/syslogd -m 10 将标记消息的时间从 20 分钟改为 10 分钟
```

关于 `syslog` 的更多信息，请参阅本章稍后关于系统日志的描述。

- 互联网超级服务器守护进程 (`inetd`)：将这些添加到 `/etc/rc.conf` 以配置 `inetd` 超服务器。如果 `inetd_enable=YES`，则 `inetd` 守护进程会在启动时启动，监听遗留 UNIX 系统各种服务（有很多）的请求，尽管通过移除 `/etc/inetd.conf` 文件中服务前的注释也可以启用其他服务（如 `rhlogin`、`tftp`、`bootpd`）：

```bash
inetd_enable="YES"
inetd_program="/usr/bin/inetd"
inetd_flags="-Ww -C 60"

# 运行网络守护进程分发器 (YES/NO)。
# inetd 的路径，如果你想使用不同的。
# inetd 的可选标志
```

通过在 `inetd_flags` 中指定其他选项，你可以更改 `inetd` 守护进程的操作方式。以下示例说明了 `inetd` 命令行：

```bash
# /usr/bin/inetd -Ww -C 60          默认。使用 TCP wrappers 处理内部/外部
# 服务只能从 IP 地址每 60 分钟调用一次
# /usr/bin/inetd -Ww -C 60 -R 128     限制每分钟调用服务的
# 次数为 128 次
# /usr/bin/inetd -a 192.168.0.1      绑定到特定的 IP 地址
# /usr/bin/inetd -o Linux           将系统报告为 Linux 以迷惑入侵者
```

- 域名解析服务 (`named`)：将这些添加到 `/etc/rc.conf` 以配置该服务，使你的系统能够作为 DNS 服务器。某些 `named` 设置默认开启，但此处列在此处是为了供你参考。如果 `named_enable=YES`，则 `named` 守护进程会在启动时启动以监听 DNS 服务器请求：

```bash
named_enable="YES"\           # 运行 named，即 DNS 服务器（或 NO）
named_program="/usr/bin/named"      # named 的路径，如果你想使用不同的
named_flags=""\                      # named 的标志
named_pidfile="/var/run/named/pid"  # 必须在 named.conf 中也设置此项
named_uid="bind"                    # 以用户 named 运行
named_chroot_dir="/var/named"      # chroot 目录（或不自动 chroot）
named_chroot_autoupdate="YES"
```

## 第 14 章：锁定安全防护

来自你计算机网络接口的数据，然后根据你设置的参数对该数据包采取何种处理。

FreeBSD 内置了三个防火墙：`IPFILTER`、`IPFIREWALL` 和 `PacketFilter`。本节重点介绍 `IPFILTER` 的功能。不仅在 FreeBSD 上，在 NetBSD 和 OpenBSD 上也有许多 `IPFILTER` 端口。你可以从官方 FAQ 了解更多关于 `IPFILTER` 的信息：`www.phildev.net/ipf`。

构建防火墙时，有几点你需要考虑。如果可能的话，请从控制台终端操作，因为在开发防火墙规则时，你可能会意外把自己锁在外面。在你的规则中，务必处理好环回（以及 `127.0.0.0` 接口）的交互。

要启用 `IPfilter`，请在 `/etc/rc.conf` 文件中添加以下设置，创建一个规则文件并启动防火墙。以下是添加到 `/etc/rc.conf` 文件的设置示例：

```bash
firewall_enable=YES                   # 设置为 YES 以启用防火墙功能
firewall_type=/etc/ipf.rules           # 使用 /etc/ipf.rules 作为防火墙规则
firewall_logging=YES                    # 设置为 YES 以启用事件日志
firewall_script="/etc/rc.firewall"    # 运行哪个脚本来设置防火墙
firewall_quiet=NO                      # 设置为 YES 以抑制规则显示
firewall_flags="                       # 当类型为文件时传递给 ipfw 的标志
ipfilter_enable=YES                  # 设置为 YES 以启用 ipfilter 功能
ipfilter_program="/sbin/ipf"           # ipfilter 程序所在位置
ipfilter_rules="/etc/ipf.rules"         # ipfilter 的规则定义，参见
                                         # /usr/src/contrib/ipfilter/rules 示例
ipfilter_flags=""               # ipfilter 的额外标志
```

注意，`firewall_enable`、`firewall_logging` 和 `ipfilter_enable` 均设置为 `YES`。最重要的一点是 `/etc/ipf.rules` 文件是存储定义防火墙行为的规则的地方。以下是添加到 `/etc/ipf.rules` 文件的设置规则示例：

```bash
add allow from any to any via lo0
add allow from any to 127.0.0.0/8
add allow from any to 127.0.0.0/8 to any
add check-state
add allow tcp from any to any established
add allow from any to any out keep-state
add allow icmp from any to any
add allow tcp from any to any 22 setup keep-state
add allow tcp from any to any 25 setup keep-state
add allow tcp from any to any 53 setup keep-state
add allow udp from any to any 53 keep-state
add allow tcp from any to any 80 setup keep-state
add allow tcp from any to any 110 setup keep-state
add allow tcp from any to any 123 setup keep-state
add allow udp from any to any 123 setup keep-state
add allow tcp from any to any 143 setup keep-state
add deny log from any to any
```

前三行允许从本地系统（`lo0` 和 `127.0.0.1`）执行任何操作。`check-state` 选项允许数据包根据动态规则集进行检查。接下来两行允许来自已建立连接并保持状态（`keep-state`）的数据包。`icmp` 行允许其他计算机 `ping` 你的计算机。

其余行与请求你系统服务的数据包有关。此机器允许对 SSH（端口 `22`）、SMTP 邮件（端口 `25`）、DNS 服务（端口 `53`）、Web 服务（端口 `80`）、邮局传输协议 v3（端口 `110`）以及 IMAP 邮件 v2（`143`）请求的连接。最后一行将任何被拒绝的其他端口日志记录到 `syslog`。

要让 `rc.conf` 中的防火墙设置和 `ipfw.rules` 中的防火墙规则生效，你需要启动 `ipfw` 服务。方法如下：

```bash
# /etc/rc.conf 启动 ipfw 防火墙服务
```



## 防火墙规则与配置

`Flushed rules.`

启动 `divert` 守护进程：`Flushed rules.`

```
00100 allow ip from any to any via lo0
00200 allow ip from any to 127.0.0.0/8
00300 allow ip from any to 127.0.0.0/8 to any
00400 check-state
00500 allow tcp from any to any established
00600 allow ip from any to any out keep-state
00700 allow icmp from any to any
00800 allow tcp from any to any dst-port 22 setup keep-state
00900 allow tcp from any to any dst-port 25 setup keep-state
01000 allow tcp from any to any dst-port 53 setup keep-state
01100 allow udp from any to any dst-port 53 keep-state
01200 allow udp from any to any dst-port 80 keep-state
01300 allow tcp from any to any dst-port 110 setup keep-state
01400 allow udp from any to any dst-port 123 keep-state
01500 allow tcp from any to any dst-port 143 setup keep-state
01600 allow ip from any to any dst-port 143 setup keep-state
01700 deny log from any to any
```

前三行允许从本地系统（`lo0` 和 `127.0.0.1`）执行任何操作。`check-state` 选项允许数据包根据动态规则集进行检查。接下来两行允许来自已建立连接并保持状态的数据包。`icmp` 行允许其他计算机 `ping` 你的计算机。

其余行与请求你系统服务的数据包有关。此机器允许对 `SSH`（端口 22）、`SMTP` 邮件（端口 25）、`DNS` 服务（端口 53）、`Web` 服务（端口 80）、邮局传输协议 v3（端口 110）以及 `IMAP` 邮件 v2（143）请求的连接。最后一行将任何被拒绝的其他端口日志记录到 `syslog`。

要让 `rc.conf` 中的防火墙设置和 `ipfw.rules` 中的防火墙规则生效，你需要启动 `ipfw` 服务。方法如下：

```bash
# /etc/rc.conf 启动 ipfw 防火墙服务
```

`Flushed rules.`

启动 `divert` 守护进程：`Flushed rules.`

```
00100 allow ip from any to any via lo0
00200 allow ip from any to 127.0.0.0/8
00300 allow ip from any to 127.0.0.0/8 to any
00400 check-state
00500 allow tcp from any to any established
00600 allow ip from any to any out keep-state
00700 allow icmp from any to any
00800 allow tcp from any to any dst-port 22 setup keep-state
00900 allow tcp from any to any dst-port 25 setup keep-state
01000 allow tcp from any to any dst-port 53 setup keep-state
01100 allow udp from any to any dst-port 53 keep-state
01200 allow udp from any to any dst-port 80 keep-state
01300 allow tcp from any to any dst-port 110 setup keep-state
01400 allow udp from any to any dst-port 123 keep-state
01500 allow tcp from any to any dst-port 143 setup keep-state
01600 allow ip from any to any dst-port 143 setup keep-state
01700 deny log from any to any
```

注意 `firewall_enable`、`firewall_logging` 和 `ipfilter_enable` 均设置为 `YES`。最重要的一点是 `/etc/ipf.rules` 文件是存储定义防火墙行为的规则的地方。以下是添加到 `/etc/ipf.rules` 文件的规则示例：

```
add allow from any to any via lo0
add allow from any to 127.0.0.0/8
add allow from any to 127.0.0.0/8 to any
add check-state
add allow tcp from any to any established
add allow from any to any out keep-state
add allow icmp from any to any
add allow tcp from any to any 22 setup keep-state
add allow tcp from any to any 25 setup keep-state
add allow tcp from any to any 53 setup keep-state
add allow udp from any to any 53 keep-state
add allow tcp from any to any 80 setup keep-state
add allow tcp from any to any 110 setup keep-state
add allow tcp from any to any 123 setup keep-state
add allow udp from any to any 123 setup keep-state
add allow tcp from any to any 143 setup keep-state
add deny log from any to any
```

前三行允许从本地系统（`lo0` 和 `127.0.0.1`）执行任何操作。`check-state` 选项允许数据包根据动态规则集进行检查。接下来两行允许来自已建立连接并保持状态的数据包。`icmp` 行允许其他计算机 `ping` 你的计算机。

其余行与请求你系统服务的数据包有关。此机器允许对 `SSH`（端口 22）、`SMTP` 邮件（端口 25）、`DNS` 服务（端口 53）、`Web` 服务（端口 80）、邮局传输协议 v3（端口 110）以及 `IMAP` 邮件 v2（143）请求的连接。最后一行将任何被拒绝的其他端口日志记录到 `syslog`。

要让 `rc.conf` 中的防火墙设置和 `ipfw.rules` 中的防火墙规则生效，你需要启动 `ipfw` 服务。方法如下：

```bash
# /etc/rc.conf 启动 ipfw 防火墙服务
```

`Flushed rules.`

启动 `divert` 守护进程：`Flushed rules.`

```
00100 allow ip from any to any via lo0
00200 allow ip from any to 127.0.0.0/8
00300 allow ip from any to 127.0.0.0/8 to any
00400 check-state
00500 allow tcp from any to any established
00600 allow ip from any to any out keep-state
00700 allow icmp from any to any
00800 allow tcp from any to any dst-port 22 setup keep-state
00900 allow tcp from any to any dst-port 25 setup keep-state
01000 allow tcp from any to any dst-port 53 setup keep-state
01100 allow udp from any to any dst-port 53 keep-state
01200 allow udp from any to any dst-port 80 keep-state
01300 allow tcp from any to any dst-port 110 setup keep-state
01400 allow udp from any to any dst-port 123 keep-state
01500 allow tcp from any to any dst-port 143 setup keep-state
01600 allow ip from any to any dst-port 143 setup keep-state
01700 deny log from any to any
```

注意 `firewall_enable`、`firewall_logging` 和 `ipfilter_enable` 均设置为 `YES`。最重要的一点是 `/etc/ipf.rules` 文件是存储定义防火墙行为的规则的地方。以下是添加到 `/etc/ipf.rules` 文件的规则示例：

```
add allow from any to any via lo0
add allow from any to 127.0.0.0/8
add allow from any to 127.0.0.0/8 to any
add check-state
add allow tcp from any to any established
add allow from any to any out keep-state
add allow icmp from any to any
add allow tcp from any to any 22 setup keep-state
add allow tcp from any to any 25 setup keep-state
add allow tcp from any to any 53 setup keep-state
add allow udp from any to any 53 keep-state
add allow tcp from any to any 80 setup keep-state
add allow tcp from any to any 110 setup keep-state
add allow tcp from any to any 123 setup keep-state
add allow udp from any to any 123 setup keep-state
add allow tcp from any to any 143 setup keep-state
add deny log from any to any
```

### 使用 `vi` 或 `Vim` 编辑器

虽然 `BSD` 系统提供了易于使用的图形化文本编辑器（如 `gedit` 和 `kedit`），但大多数高级用户仍使用 `vi` 或 `Emacs` 来编辑文本文件。除了 `vi` 和 `Emacs` 可以在任何 `shell` 中运行（无需 `GUI`）之外，它们还具有其他优势，例如手无需离开键盘，并且与实用工具集成。与 `GUI` 编辑器不同，基于文本的编辑器可以在拨号或卫星等慢速互联网连接上使用。

| 本附录内容 |
| :--- |
| 使用 `vi` 编辑器 |
| 启动/退出编辑器 |
| 在 `vi` 中移动 |
| 修改和删除文本 |
| 使用 `Ex` 命令 |
| 使用可视化模式 |

本附录侧重于 `vi` 编辑器的功能，这些功能不仅能帮助你进行基础编辑，还能帮助你进行高级文本操作。我们选择介绍 `vi` 而不是 `Emacs`，是因为 `vi` 更为通用且更轻量，而且键盘快捷键只需要两个手臂。某些 `UNIX` 类系统使用 `Vim`（改进版 `vi`）编辑器来代替旧的编辑器，本附录中的描述也扩展到了 `Vim`。`Vim` 中某些 `vi` 并不具备的功能包括多级显示、语法高亮和在线帮助。

> 注意：如果你以前从未用过 `vi` 或 `Vim`，请尝试 `vim6` 软件包附带的教程。运行 `vimtutor` 命令并按照指令逐步学习 `vi` 和 `Vim` 的许多关键功能。要查看 `vi` 和 `Vim` 之间的差异，可以在运行命令时输入 `:help vi_diff.txt`。要安装 `vim6` 软件包，请以 `root` 用户身份执行：`pkg_add -r vim`。

取决于你的 `vim` 包是如何构建的，你可能无法首先获得所有最新的 `vim` 功能。在许多情况下，兼容选项是开启的，这会导致 `vi` 和 `vim` 之间的冲突行为表现得像 `vi`（本附录后文关于撤销的文本）。要开启最新的 `vim` 功能，可以在用 `vim` 编辑时输入 `:set incompatible`，或在你的 `~/.vimrc` 文件中添加此内容：

```bash
set incompatible
```

## 附录 A：使用 `vi` 或 `Vim` 编辑器

### 启动和退出 `vi` 编辑器

如果你想尝试 `vi`，应该复制一个文本文件进行练习。例如，输入：

```bash
$ cp /etc/services /tmp
```

然后使用如下 `vi` 命令打开该文件：

```bash
$ vi /tmp/services own
```

为了从 `Vim` 的改进中受益，请确保已安装 `FreeBSD` 的 `vim6` 软件包。在许多系统中，`vi` 被别命名为 `vim` 命令。你可能想双检查 `alias` 命令。如果你想直接使用 `vim`，输入 `/usr/local/bin/vim`。如果你专门想用旧式的 `vi` 命令，请使用 `/tmp/vi` 命令的完整路径：

```bash
/bin/vi /tmp/text.txt
```

这里是几种启动 `vi` 的方法：

- `vi +25 /tmp/services`      从第 25 行开始
- `vi + /tmp/services`        从文件的最后一行开始编辑
- `vi +/tty /tmp/services`    从第一行包含 `"tty"` 的单词处开始编辑
- `vi -r /tmp/services`       从崩溃的编辑会话中恢复文件
- `view /tmp/services`        以只读模式编辑文件

当你完成会话后，有几种不同的方法可以保存并退出。要在准备退出之前保存文件，输入 `:w`、`ZZ` 或 `:wq`。要在不保存更改的情况下直接退出，输入 `:q!`。如果你发现无法写入正在编辑的文件，可能是它以只读模式打开的。如果是这样，你可以尝试通过输入 `:w!` 强制写入，或者将文件内容保存为不同的名称。例如，输入以下内容将当前文件的内容保存为名为 `myfile.txt` 的文件：

```bash
:w /tmp/myfile.txt
```

> 注意：理解 `:w` 将当前文件写入另一个文件是非常重要的。如果你继续编辑，你仍在编辑原始文件。在上面的示例中，如果你开始编辑 `services` 文件，然后将其内容写入 `myfile.txt`，要继续编辑 `myfile.txt`，你必须通过输入 `-e: /tmp/myfile.txt` 来切换它。

`vi` 编辑器还允许你同时编辑多个文件。例如，输入：

```bash
$ cd /tmp
touch a.txt b.txt c.txt
vi a.txt b.txt c.txt
```

在这个示例中，`vi` 会先打开一个 `.txt` 文件。你可以通过输入 `:n` 移动到下一个文件。你可能想移动到下一个文件之前保存更改（`:cw`）或在移动到下一个文件时保存更改（`:wn`）。要返回上一个文件，输入 `:prev`。

你可能会发现使用 `vim` 的分屏功能打开多个文件更简单。当你使用 `vim` 且打开了一个文件时，可以多次水平或垂直拆分屏幕：

```bash
:split /etc/services
:vsplit /etc/hosts
```



使用 `<Tab>` 键补全文件路径，就像在 bash shell 中执行一样。要在分屏窗口之间导航，按下 `Ctrl+W`，然后按 `W` 键。关闭当前窗口请使用通常的 vi 退出命令 (`:q`)。

## 在 vi 中移动

在 vi 中需要习惯的第一件事是，你不能直接开始打字。vi 有多种模式，允许你执行一组不同的任务。你在普通模式（normal mode）下启动 vi 会话，此时 vi 正在等待你输入命令来开始。在普通模式下，你可以在文件中移动。要插入或修改文本，可以进入插入模式。要删除或更改文本，可以进入命令模式。

| 键 | 结果 | 键 | 结果 |
| :--- | :--- | :--- | :--- |
| `/string` | 搜索下一个字符串 | | |
| `PageDown` 或 `Ctrl+f` | 跳到下一页 | `PageUp` 或 `Ctrl+b` | 跳到上一页 |
| `Ctrl+d` | 跳向下半页 | `Ctrl+u` | 跳向上半页 |
| `G` | 跳到最后一行 | `1` | 跳到第一行 |
| `End` 或 `$` | 跳到行末尾 | `Home` 或 `0` | 跳到行首 |
| `H` | 跳到屏幕顶部 | `L` | 跳到屏幕底部 |
| `M` | 跳到屏幕中间 | `Ctrl+L` | 刷新屏幕 |
| `h` | 向左移动 | `l` | 向右移动 |
| 左箭头或退格键 | 向左移动 | 右箭头 | 向右移动 |
| `k` 或上箭头 | 向上移动 | `j` 或下箭头 | 向下移动 |
| `/string` | 查找下一个字符串出现 | `?string` | 查找上一个字符串出现 |
| `n` 或 `/` | 再次查找（正向） | `N` 或 `?` | 再次查找（反向） |

| 键 | 结果 | 键 | 结果 |
| :--- | :--- | :--- | :--- |
| `d?` | 使用 `l`, `w`, `$` `d` 剪切字符、单词、行末尾或整行 | `D` | 从光标处到行末 |
| `y?` | 使用 `l`, `w`, `$` `y` 复制（剪切）字符、单词、行末尾或行 | `Y` | 复制整行 |
| `c?` | 使用 `l`, `w`, `$` `c` 修改字符、单词、行末尾或行 | `C` | 从光标处到行末并输入新文本 |
| `w` | 移动到下一个单词 | `W` | 移动到下一个忽略空格的单词 |
| `b` | 移动到上一个单词 | `B` | 移动到上一个忽略空格的单词 |
| `e` | 移动到单词末尾 | `E` | 移动到忽略空格的单词末尾 |

## 修改和删除文本

要用 vi 更改或添加文本，可以进入插入或替换模式，如表 2 所示。在插入或替换模式下，你输入的字符将出现在文档中（而不是被解释为命令）。

在完成插入或替换后，按 `Esc` 键退出普通模式。

### 表 A-2：更改命令

| 键 | 结果 | 键 | 结果 |
| :--- | :--- | :--- | :--- |
| `i` | 在当前字符前插入文本 | `I` | 在行首插入文本 |
| `a` | 在当前字符后插入文本 | `A` | 在行末插入文本 |
| `o` | 在下方另起新一行并输入文本 | `O` | 在上方另起新一行并输入文本 |
| `s` | 删除字符并替换为新文本 | `S` | 删除整行并输入新文本 |
| `c?` | 使用 `l`, `w`, `$` `c` 修改字符、单词、行末尾或行 | `C` | 从光标处到行末并输入新文本 |
| `r` | 用下一个输入的字符替换当前字符 | `R` | 从当前字符开始覆盖输入 |

### 表 A-3：删除和粘贴命令

| 键 | 结果 | 键 | 结果 |
| :--- | :--- | :--- | :--- |
| `x` | 删除光标下的字符 | `X` | 删除光标左侧的字符 |
| `d?` | 使用 `l`, `w`, `$` `d` 剪切字符、单词、行末尾或整行 | `D` | 从光标处到行末 |
| `y?` | 使用 `l`, `w`, `$` `y` 复制（剪切）字符、单词、行末尾或行 | `Y` | 复制整行 |
| `p` | 在光标后粘贴剪切或复制的文本 | `P` | 在光标前粘贴剪切或复制的文本 |

## 附录 A：使用 vi 或 Vim 编辑器

### 使用杂命令

表 A-4 显示了一些你应该了解的杂但重要的命令。

**表 A-4：杂命令**

| 键 | 结果 |
| --- | --- |
| `u` | 输入 `u` 撤销上一次更改。多次输入 `u` 命令可以切换上一次撤销的开启状态。（在 vim 中，输入 `:set incompatible` 将允许多级撤销。使用 `Ctrl-r` 撤销你的操作。） |
| `.` | 输入点号 (`.`) 将重复执行上一个命令。因此，如果你删除了一行、替换了一个单词、更改了四个字母等，相同的命令将在当前光标所在的位置再次执行。（再次进入输入模式将重置它。） |
| `J` | 将当前行与下一行合并。 |
| `Esc` | 如果你之前没有注意到，`Esc` 键会将你从输入模式返回命令模式。这是你将最频繁使用的键之一。 |

### 使用数字修改命令

到为止描述的几乎每个命令都可以用数字进行修改。换句话说，你可以不是删除一个单词、替换一个字母或更改一行，而是删除六个单词、替换 12 个字母并更改九行。表 A-5 显示了一些示例。

**表 A-5：使用数字修改命令**

| 命令 | 结果 |
| --- | --- |
| `7cw` | 擦除后七单词并用你输入的文本替换它们。 |
| `d5d` | 剪切后五行（包括当前行）。 |
| `3p` | 在当前光标后粘贴之前删除三次。 |
| `9db` | 剪切当前光标前的九单词。 |
| `10j` | 光标向下移动 10 行。 |
| `y2` | 从光标复制（yank）文本到后两个句子的结束。 |
| `5Ctrl+F` | 向前移动五页。 |
| `6J` | 合并后六行。 |

通过这些示例，你可以看到大多数更改文本、删除文本或在文件中移动的 vi 击键都可以使用数字进行修改。

### 使用 Ex 命令

vi 编辑器最初是构建在一个名为 Ex 的编辑器上的。你目前所看到的一些 Ex 命令以分号开头，被称为 Ex 命令。要进入 Ex 命令，从普通模式开始并输入分号 (`:`)。这会将你切换到命令模式。在此模式下，你使用 `Tab` 键来完成命令或文件名，并使用方向键来浏览命令历史，就像在 bash shell 中一样。当你在命令末尾按下回车时，你将返回普通模式。

表 A-6 显示了一些 Ex 命令的示例。

**表 A-6：Ex 命令示例**

| 命令 | 结果 |
| --- | --- |
| `:!bash` | 退出到 bash shell。完成后，输入 `exit` 返回 vi。 |
| `:date` | 运行 `date`（或你选择的任何命令）。按回车返回。 |
| `:!!` | 重新运行之前运行的命令。 |
| `:20` | 转到文件的第 20 行。 |
| `:5,10w abc.txt` | 将第到10行写入文件 `abc.txt`。 |
| `:e abc.txt` | 离开当前文件并开始编辑文件 `abc.txt`。 |
| `:r def.txt` | 将 `def.txt` 的内容读取到当前行下方。 |
| `:s/UNIX/FreeBSD` | 将当前行中第一个 `UNIX` 替换为 `FreeBSD`。 |
| `:s/UNIX/FreeBSD/g` | 将当前行中所有的 `UNIX` 替换为 `FreeBSD`。 |
| `%s/UNIX/FreeBSD/g` | 将整个文件中所有的 `UNIX` 替换为 `FreeBSD`。 |
| `:g/FreeBSD /p` | 列出文件中包含字符串 `FreeBSD` 的每一行。 |
| `:g/gaim/s//pidgin/gp` | 找到每个 `gaim` 实例并将其更改为 `pidgin`。 |

从 ex 提示符处可以使用 `set` 命令查看并更改与你的 vi 会话相关的设置。表 A-7 显示了一些示例。

**表 A-7：ex 模式下的 set 命令**

| 命令 | 结果 |
| :--- | :--- |
| `set all` | 列出所有设置。 |
| `set` | 列出与默认值相比过的设置。 |
| `set number` | 在每行左侧显示行号。（使用 `set non` 取消） |
| `set ai` | 设置自动缩进，开启新行将遵循上一个缩进。 |
| `set ic` | 设置忽略大小写，使文本搜索不分大小写地匹配。 |
| `set list` | 显示行尾的 `$` 和制表符 `^|`。 |
| `set wm` | 使 vi 在行尾附近的单词之间添加换行。 |

### 在可视模式下工作

Vim 编辑器提供了一种更直观的选择文本的方法，称为可视模式。要开始可视模式，将光标移动到想要选择的文本的第一个字符并按下 `v` 键。

此时，你可以使用任何光标移动键（方向键、`Page Down`、`End` 等）将光标移动到想要选择的文本末尾，移动光标时，你会看到文本被高亮。当所有想要选择的文本都被高亮时，你可以按键对该文本进行操作。例如，`d` 删除文本，`c` 让你更改所选文本。

## 总结

vi 编辑器是可用的最强大的文本编辑器之一。在本章中，我们学习了 vi 的基本命令，包括如何插入、删除、复制和粘贴文本。我们还涵盖了如何使用 Ex 命令和可视模式。有了这些知识，你应该能够有效地使用 vi 和 Vim。

## 附录 B：Shell 特殊字符和变量

### 使用 Shell 变量

通过在字符串前面放置 `$`，你可以将该字符串识别为参数（变量）（例如 `$HOME`）。Shell 环境变量可以包含 shell 自身以及从 shell 运行的命令所需的信息。并不是所有环境变量都会默认填充。其中某些变量是可以更改的（例如 `$PRINTER` 中的默认打印机或 `$PS1` 中的你的命令提示符。其他变量由 shell 管理（例如 `$OLDPWD`）。表 B-2 包含了许多有用的 shell 变量列表。

## 表 B-2：Shell 变量

| Shell 变量 | 描述 |
| --- | --- |
| `BASH` | 显示 bash 命令的路径 (`/bin/bash`)。 |
| `BASH_COMMAND` | 当前正在执行的命令。 |
| `BASH_VERSION` | bash 命令的版本号。 |
| `COLUMNS` | 终端宽度（以字符为单位）。 |
| `DISPLAY` | 识别从当前 shell 启动的命令显示的 X 显示器（例如 `:0`）。也可以是远程主机上的显示器（例如 `example.com:0`）。 |
| `EUID` | 当前用户的有效用户 ID。它基于登录用户在 `/etc/passwd` 中的用户条目。 |
| `FCEDIT` | 确定 `fc` 命令编辑历史命令时使用的编辑器。默认使用 `vi` 命令。 |
| `GROUPS` | 列出当前用户所属的主组。 |
| `HISTCMD` | 显示当前命令的历史编号。 |
| `HISTFILE` | 显示历史文件的位置（通常位于 `$HOME/.bash_history`）。 |
| `HISTFILESIZE` | 将存储的历史条目总数（默认值为 1000）。达到此数字后，旧的命令将被丢弃。 |
| `HOME` | 当前用户主目录的位置。输入不带选项的 `cd` 命令会将 shell 返回到主目录。 |
| `HOSTNAME` | 当前机器的主机名。 |
| `HOSTTYPE` | 包含运行 BSD 系统的计算机架构（`i386`, `i486`, `i586`, `x86_64`, `pp` 或 `pc64`）。 |
| `LESSOPEN` | 设置为一个命令，用于转换纯文本以外的内容（图像、zip 文件等），以便其可以通过 `less` 命令进行管道处理。 |
| `LINES` | 设置当前终端的行数。 |
| `LOGNAME` | 持有当前用户名。 |

## 表 B-2：Shell 变量（续）

| Shell 变量 | 描述 |
| --- | --- |
| `MACHTYYPE` | 显示机器架构、公司和操作系统的信息（例如 `i686-portbld-freebsd6.2`）。 |
| `MAIL` | 指示你的邮箱箱文件位置（通常在 `/var/mail` 目录）。 |
| `MAILCHECK` | 在指定的秒数内检查邮件（默认为 60 秒）。 |
| `OLDPWD` | 切换到当前工作目录之前的工作目录。 |
| `OSTYPE` | 标识当前操作系统的名称（例如 `freebsd6.2`）。 |
| `PAGER` | 用于查看 `man` 手页的程序。 |
| `PATH` | 用冒号分隔的目录列表，用于定位你输入的命令（`/bin`, `/usr/bin` 和 `$HOME/bin` 通常在 `PATH` 中）。 |
| `PPID` | 启动 shell 的命令进程 ID。 |
| `PRINTER` | 设置默认打印机，供 `lpr` 和 `lpq` 等打印命令使用。 |
| `PROMPT_COMMAND` | 设置为每次显示 shell 提示符时运行的命令名称。（例如，`PROMPT_COMMAND=ls` 在显示提示符前列出当前目录下的命令。） |
| `PS1` | 设置提示符。提示符中的项目可以包括日期、时间、用户名、主机名等。可以使用 `PS2`、`PS3` 等设置额外的提示符。 |
| `PWD` | 分配为当前目录的目录。 |
| `RANDOM` | 访问此变量生成 0 到 32767 之间的随机数。 |
| `SECONDS` | 自 shell 启动以秒数。 |
| `SHELL` | shell 的完整路径。 |
| `SHELLOPTS` | 列出启用的 shell 选项（设置为开启的）。 |
| `SHLVL` | 列出与当前 shell 关联的 shell 层级。 |
| `TERM` | 表示你正在使用的 shell 终端窗口类型。默认是 `xterm`。 |

## 表 B-2：Shell 变量（续）

| Shell 变量 | 描述 |
|---|---|
| `TMOUT` | 设置为一个数字，代表 shell 在不接收输入的情况下空闲的秒数。达到该秒数后，shell 将。 |
| `UID` | 分配给当前用户的用户 ID。用户 ID 存储在 `/etc/password` 文件。 |
| `USER` | 当前用户名。 |

## C：个人配置文件

每个用户账户的主目录下都有一组文件和目录，包含该账户的个人设置。由于配置文件和目录以点（`.`）开头，当你打开主目录的文件夹窗口时是看不到它们的。同样，在列出目录内容时，你通常需要 `ls` 的 `-a` 选项才能看到这些文件。

| 本附录包含 |
| --- |
| Shell 配置文件 |
| 浏览器和电子邮件配置文件 |
| 桌面配置文件 |
| 网络服务配置文件 |
| 音乐播放器配置文件 |

本附录描述了每个用户在 BSD 系统上可以使用的许多点文件（dot files）。创建配置文件后，你可以按照喜好自定义环境。（注：提供的源文件中 OCR 文本在此处截断或碎片化，但根据提供的文本流：）

本附录描述了每个用户在 BSD 系统上可以使用的许多点文件。创建配置文件后你…… [此处由于 OCR 文本重复和乱码，已根据逻辑进行重构]

# 附录 C：个人配置文件

**GNOME 配置文件**：运行 GNOME 桌面的用户会在其主目录下有一个 `.gnome` 目录。子目录中包含了你运行的 GNOME 应用程序的配置文件，例如 Rhythmbox 播放器 (`rhythmbox`)、Totem 视频播放器 (`totem`) 和 Evince 检视 (`evince/`)。许多配置文件为 XML 格式，因此你可以读取它们（尽管你通常不会直接编辑它们）。保留这些信息是有用的，因为它们可能包含专辑封面、播放列表和偏好（如颜色和色调）。

**KDE 配置文件**：如果你运行 KDE 桌面，`.kde` 目录包含与 KDE 桌面、窗口管理器以及相关 KDE 应用程序的信息。与 GNOME一样，许多 KDE 配置以 XML 格式存储，因此你可以使用任何文本编辑器查看其内容。你可以将脚本放入 `.kde/Autostart` 目录，以便它们在 KDE 启动时执行。

**mail 配置文件**：`mail` 命令的设置存储在 `.mailrc` 和 `.mail_aliases` 文件中。

**ncftp 配置文件**：如果你使用 ncftp FTP 客户端，与你的 ncftp 会话相关的设置存储在主目录下的 `.ncptp` 目录中。设置防火墙的目录中的防火墙文件包含了通过代理服务器使用 ncftp 的信息。历史文件保留了之前在 FTP 会话期间运行的命令列表。日志文件收集错误和信息消息。`prefs_v3` 文件包含 ncftp 偏好。

**信任主机 (Trusted hosts)**：如果你允许使用 `system-hosts.allow` 或 `.hosts` 文件，它们可以将一个信任主机列表添加，并可选地将来自这些主机的用户添加到各自主目录下的 `.hosts` 文件中。如果启用了登录或 `rcp` 等服务（`/etc/inetd.conf`），来自信任主机的人可以使用这些主机登录或将文件复制到你的机器，而无需输入密码。如果你网络上的所有计算机都通过线连接、位于同一个房间、位于喜马拉雅山的小屋里且没有外部连接，那么这样做是好的。否则，你应该考虑这种方式使用信任主机是非常不安全的。

**Secure Shell 配置文件**：如果你使用安全外壳 (`ssh`) 服务，主目录下的 `.ssh` 目录可以通过安全设置进行管理。以下是示例：

- `known_hosts`：保留你已验证为真实的主机计算机列表。
- `identity`：来自 SSH 协议版本 1 的私身份密钥。
- `id_rsa`：来自 SSH 协议版本 2 的私身份密钥。
- `id_dsa`：来自 SSH 协议版本 2 的私身份密钥。
- `identity.pub`, `id_dsa.pub`, `id_rsa.pub`：上述三个私钥的公钥。
- `authorized_keys`：包含远程客户端公钥的文件。

**虚拟网络计算文件**：如果你使用 `vncserver` 工具与网络上的其他计算机共享桌面，`vncserver` 行为的设置存储在你主目录的 `.vnc` 目录中。该目录下的 `xstartup` 文件包含了在你启动 VNC 时运行的应用程序。`vncpassword` 文件存储了供 `vncserver` 使用的密码。

对于每个启动的显示器，都会创建一个名为 `host#.pid` 的文件（`host` 是主机名，`#` 是显示器编号）。每个显示器还有一个 `host#.pid` 文件，其中包含与显示器相关的 `Xvnc` 进程的进程 ID。

**X 启动文件**：如果你使用 `startx` 命令启动桌面界面，可以使用 `.xinitrc` 文件来指定启动哪个桌面环境。例如，向 `.xinitrc` 中添加 `/usr/local/bin/gnome-session` 以启动 GNOME 桌面环境。向 `.xinitrc` 中添加 `/usr/local/bin/kde` 以启动 KDE 桌面环境。

**MMMS 配置文件**：如果你使用 MMMS 音乐播放器，该播放器的配置文件包含主目录下的 `.mmms` 目录中。该目录的子目录包括 `Plugins`（存放音频插件）和 `Skins`（存放播放器使用的皮肤）。目录下的 `config` 文件持有 MMMS 的偏好设置。`mmms.m3u` 文件包含播放过的歌曲路径。

# 索引

- 地址解析协议 (ARP), 197–198
- 从缓存中删除条目, 198
- 将静态条目添加到缓存, 198
- 子网查询, 248
- 查看/配置条目, 197–198

- 命令
- 默认设置, 247–248
- 添加用户, 246
- 默认 shell, 更改, 248
- 主目录, 更改位置, 249
- 主目录, 不创建, 248–249
- 登录类, 更改, 249
- 新用户，交互式添加, 244–245

- 别名 (`alias`)
- 定义别名, 41
- 列出别名, 41
- 移除别名, 41
- 命令
- bash 会话别名, 定义, 41
- 列出别名, 41
- 匿名访问，文件传输协议 (FTP), 17

- 存档 (`archive`)
- 内容, 列出, 132
- 添加文件, 132
- 创建 tar 存档, 128–129
- 通配符匹配文件, 132

- `arp` 命令
- ARP 缓存删除条目, 198
- ARP 条目, 查看, 197–198
- 将静态条目添加到缓存, 198
- `arping` 命令, IP 查询, 186

- ASCII 文本
- 从二进制文件提取, 83

- `at` 命令
- 进程，调度运行, 157–158

- AT&T Unix, 2
- `aterm`, 35
- 进程，检查队列, 158
- 进程，从队列中删除, 158

- 附件，电子邮件, 222

- 文件的属性
- 更改, 63
- 列出, 62–63

- AU 文件, 播放, 91
- 音频, 89–97
- AFF 文件, 播放, 91
- AU 文件, 播放, 91
- 音频格式/效果，查看, 90–91
- 音频混合，显示设置, 92
- CDs, 刻录到硬盘, 93
- 当前通道，作为录制设备, 92
- 显示设置，更改, 92
- 文件，显示信息, 96
- 头部信息，查看, 94

- MP3 文件, 播放, 91
- MP3 格式，转换文件, 95
- 静音, 92
- offg 文件, 播放, 91
- 播放列表，来自, 91
- 发送声音，删除, 97
- 跳到下一首歌, 91
- 声卡驱动程序，配置, 89–90
- 加快播放, 91
- 查看/调整级别, 92
- 音量，调整, 92
- WAV 文件，合并, 96
- WAV 文件，混合, 96
- WAV 文件，播放, 91
- XMMS 配置文件, 280
- `aumix` 命令，音频显示设置, 更改, 92
- 自动登录，安全安全外壳 (`ssh`), 230

- `awk` 命令
- 提取文本列, 87
- 分隔符，更改, 87
- 信息源, 50
- shell 输入，重定向, 39
- 循环/迭代, 49
- shell 输出，重定向, 38–40
- 创建脚本, 45–50
- 目录设置文件, 277
- tailing 文件, 41
- bash shell 历史, 36–38
- 反向搜索, 38
- 编辑命令历史, 37
- 编辑当前命令, 37
- 列出历史, 37
- 在命令间移动, 37
- 列出之前的命令, 37
- 搜索字符串, 38

- `BASH_COMMAND`, 273
- `BASH_VERSION`, 273
- 批处理命令，进程，调度
- 运行, 158

- 伯克利软件发行版 (BSD),
- BSD 系统，开发, 2
- `bg` 命令，在后台运行进程, in
- 后台, 155

- 二进制文件
- 从 ASCII 文本提取, 83
- 篡改 rackers, 63
- BIOS SMAP 查看, 15
- 位桶文件，输出流，重定向到, 39

- `BitchX`, 219
- 块设备，类型, 54
- 博客，网站, 5
- BMP 文件，转换到, 98

- `boot` 命令，FreeBSD 安装,
- 启动, 15
- 启动过程, 172–178
- 启动，阶段, 172
- 启动镜像，更改, 173
- 引导加载器, 172
- Boot 管理器 (`BootMgr`), 16
- 启动提示符，从中运行命令, 15
- `boot0cfg` 命令, 173–174
- 更改，注意, 174
- 默认切片到，更改, 175

## B–C 索引

- FreeBSD 安装, 14–15
- FreeBSD 设置, 更改, 15
- GRUB 引导加载器, 176–178
- ISO 镜像, 创建, 62
- 内核指定位置, 178
- 主引导记录 (Master Boot Record), 覆盖, 177
- 多个操作系统的操作, 174–176
- 重启, 179
- 第二驱动器, 查找引导加载器, 175
- 启动分区 (slice), 更改, 175
- `boot0cfg` 命令, 173–174
- 启动镜像, 检查, 173
- 引导加载器, 安装, 174
- 第二硬盘上的引导加载器, 查找, 175
- 启动更改, 174
- 默认启动分区, 更改, 175
- 两个操作系统信息, 显示, 174–175
- 瓶颈
- 网络连接, 198–199
- 存储设备, 检查, 167
- `bouncer`, 219
- Bourne shell, `.shrc` 文件, 278
- Bourne Again Shell, 36
- 另见 bash shell
- 浏览器
- 远程系统管理, 225–242
- 资源网站, 4–5
- 安全, 243–262
- Shells, 33–50
- 系统日志, 261
- 系统管理, 161–183
- 文本, 处理, 71–88
- 版本, 查找, 180
- `dslabel` 命令
- BSD 标签, 添加到文件, 117
- 分区上的分区镜像, 查看, 113, 176
- `bslabel` 工具: 用于硬盘分区, 107
- 分区上的分区, 更改, 104
- `bsdar` 工具, 162
- `bzip2` 压缩, 130
- 向系统添加包, 130
- 压缩文件, 131
- 使用 `tar` 命令, 128
- 解压文件, 130, 131

## C

- C shell, 设置, 目录文件, 278
- `cal` 命令, 日历, 显示, 169–170
- 大小写, 小写字母, 转大写, 84–85
- 用法情况, 测试, 49
- `cat` 命令
- 音频设备, 检查, 90
- 空文件, 创建, 52
- 文本, 替换, 83
- 文本文件内容, 显示, 78, 85
- 文件顶部, 查看, 79
- CD(s)
- 容量, 140
- 弹出, 141
- FreeBSD, 13
- 用于刻录/压制的 GUI 工具, 92–93, 137
- ISO 镜像, 刻录, 140–141
- `elinks` 浏览器, 205–206, 278
- `ssh`, `socks` 代理 互联网连接, 229–230
- BSD 系统
- 备份, 127–142
- 压缩, 129–132
- 开发, 2
- 目录, 52–53
- 文件, 51–70
- 多媒体, 89–101
- 网络连接, 185–203
- 网络资源, 205–223
- 网络服务, 255–288
- 在线社区, 5–6
- 操作系统, 3–4
- 进程, 进程, 143–159
- 多刻录会话, 141–142
- 权限, CD 播放打开, 90
- 刻录到硬盘, 93
- 设置为录制设备, 92
- `cd` 命令, 切换目录, 51, 59, 117
- CD 驱动器, 能力, 检查, 93, 141
- `cd960` 文件系统, 特性, 106
- `ncdia` 命令
- CDDA 能力, 验证, 93
- CDs, 刻录到硬盘, 93
- `cdrecord` 命令, 140–141
- 刻录多会话 CDs/DVDs, 141
- CD/DVD 刻录能力, 检查, 141
- CDs/DVDs, 刻录镜像到, 141
- 集中日志, 262
- 字符设备, 类型, 54
- 字符转换, 84–85
- 字符, 替换, 84
- 字符范围, 指定, 84–85
- 空格, 用换行符替换空格, 84
- 图像中添加木炭色调, 99
- 聊天, 互联网中继站 (IRC), 219–220
- `chattr` 命令, 文件属性, 更改, 63
- 校验和, 验证, 68–69
- MD 校验和, 为文件创建, 69
- `chgrp` 命令, 组所有权, 更改, 58, 212
- `chroot`, 212
- `chmod` 命令: 权限, CD 播放打开, 90, 权限, 更改, 56–58, shell 脚本, 可执行的, 45
- VNC 权限, 设置, 241
- `chown` 命令, 组所有权, 更改, 58, 212
- 颜色(s), 文件类型, 查看, 68
- 图像, 着色, 99–100
- 搜索术语, 81
- 内容, 显示, 87
- 打印, 273
- `COLUMNS`(s)
- 配置文件, 查找, 67
- 命令, 8
- 未找到, 用于, 7–8
- 命令行压缩, 130–131
- 通用文件系统 (`cifs`), 另见 Samba
- 兼容模式, 硬盘, 104
- 压缩, 129–132
- 目录中的文件, 130–131
- 硬盘分区, 备份, 62
- `bzip2` 压缩, 130–131
- `gzip` 压缩, 130–131
- `lzop` 压缩, 130–131
- RAR 格式, 130
- `tar` 文件, 备份/压缩, 130–131
- 解压缩存档, 129
- `connect` 命令, 服务器, 连接, 219
- `convert` 命令: 批量图像, 转换, 100
- 目录, 缩放, 100
- 图像格式, 转换, 98
- 图像缩放, 98, 100
- 旋转图像, 98
- 特殊效果, 添加, 99–100
- 文本, 到图像, 98
- 缩略图, 创建, 98
- 文件转换到其他, 88
- 复制和粘贴, Terminal, 34
- 登录类, 250
- 数据复制, 61
- IDE 驱动器, 分区, 61
- 交换区, 文件内, 117–118
- 警告, 61
- 零填充文件, 创建, 117
- 目录, 60
- 任务队列, 158
- 端口集合, 22–23
- 用户账户, 251–252
- vi 编辑器, 267

## D

- 数据复制, 61
- 数据库(ies), `locate`, 438–65
- `date`. 另见 `date/date`
- `date` 命令
- time/date, 更改, 170
- time/date, 显示, 169
- `dd` 命令: 备份, 62
- 启动镜像, 创建, 398
- 权限, 更改, 56–57
- 权限, 设置, 53, 56
- 远程, 共享. *另见远程目录*
- 共享: , 60
- 粘性位 (`sticky` `bit`), 功能, 57–58
- 符号链接, 创建, 59–60
- `dirs` 命令, 目录, 更改, 60
- 磁盘分区, FreeBSD 安装, 15–16
- `Disklabel` Editor, 16
- 校验和, , 30
- 发行, FreeBSD, 17
- DOS 文件系统, 检查, 123
- `double-unix` 命令, 文件转换, 80
- 转储文件, 117
- 多个目录, 指定, 125
- 容量, 140
- 弹出, 141
- ISO 镜像, 刻录, 140–142
- 多刻录会话, 141–142
- CPU 信息, 查看, 166
- 声卡, 检测, 89
- 缓冲区内容, 显示, 180
- 系统消息, 列出, 183
- 软件包, 子目录, 8
- DVD 驱动器, 能力, 检查, 141
- 改进, 142

## E

- Emacs 编辑器, 功能, 73
- 邮件, 220–222
- 附件, 222
- MBOX 格式, 221
- `mutt` 命令, 222–223
- 故障排除, 226
- `env` 命令, 环境变量, 列出, 45
- 环境变量, 44–45
- 显示, 186
- 列出, 45
- 设置/重置, 44
- Shell, 列出, 272–275
- `eterm`, 35
- 以太网接口卡 (`nic`), 186–190
- 能力, 显示, 187–188
- 配置, 17, 186
- 功能, 186
- 强制设置速度, 188
- IP 地址/子网掩码, 更改, 188
- 名称, 显示, 187
- 网络, 停止, 191
- 设置, 更改, 188
- 显示, 187
- 设置, 持久化, 188–189
- 速度, 强制, 186–187
- 统计, 刷新, 189
- 统计, 查看, 189
- 故障排除, 186
- `ethtool` 命令, 187
- `EUID`, 273
- `Evolution`, 在家目录中, 278
- Ex 编辑器, 来自 vi 命令, 269–270
- `export` 命令: `DISPLAY`, 设置到本地机器
- 环境变量继承, 45
- 变量连接到字符串, 45
- `ext2/ext3` 文件系统, 114–116
- 属性, 更改, 115–116
- 属性, 列出, 62–63
- 在分区上创建, 114–115
- 设置, 更改, 116

## FDISK

- 硬盘几何结构, 更改, 109
- 硬盘分区, 15–16, 104, 107–109
- 系统提供的接口, 108
- 将更改写入分区表, 109
- `fdisk` 命令
- 创建新分区, 111
- 创建分区, 107
- 第一驱动器的分区信息, 列出, 105
- 分区信息, 列出, 109, 175
- 交互式更改分区表, 110
- 分区表, 显示, 109
- 分区, 更改, 110
- 硬盘的分区列表, 109–110
- 警告, 110
- `g` 命令, 前台运行, 155
- 文件(s), 51–70
- 属性, 更改, 63
- 属性, 列出, 62–63
- 创建空文件, 52
- 校验和, 验证, 68–69
- 克隆部分, 61
- 复制数据, 61
- 复制文件, 60–61
- 设备文件, 54
- 文件间差异, 检查, 85–86
- 文件名, 测试, 46–47
- 文件类型, 查看, 符号和硬链接, 53–54
- 链接, 15, 52, 67–68
- `dlocate` 数据库, 创建, 63–64
- `dlocate` 数据库, 文件信息, 查找, 64–65
- `docate` 数据库, 更新, 65
- MD5 校验和, 为文件创建, 69
- 所有权, 更改, 58
- 权限, 更改, 56–57
- 权限, 设置, 56
- 搜索, 64
- 基于时间戳的搜索, 65–66
- `fc` 命令, bash 历史, 编辑, 37
- `FCEDIT`, 273

# 索引 = F

- 按大小搜索，66–67
- 搜索准则，否定，66
- 使用正则表达式搜索，66
- 文本，发送到，80

- `ftpcopy` 目录，列出内容，25
- `ftpcopy` 包，列出文件，20
- `cftp` 配置文件，279
- 非交互式下载会话，211
- server。见 `ftp` 命令

## `file` 命令
- 文件的内容，确定，53
- 可执行文件，保存，52

### 文件系统
- 检查，122–123
- 磁盘空间占用，检查，125–126
- 转储（`dump`），119
- 上传会话，211

### 文件传输协议服务 (`ftp`)
- 命令行，258
- 启用，258
- 文件传输，208–213
- 使用 `curl`，错误，123–124
- `extext2/ext3`。见 `ext2/ext3` 文件系统
- 文件，在环回接口中监控，121
- FreeBSD 默认，16
- `inode` 占用率，检查，124
- Linux 兼容，创建，114–116
- 本地，显示磁盘空间，125
- 本地监控，120

### 文件传输协议 (`ftp`)，209–211
- 中断，208
- 登录/密码，207
- 使用 `Secure` `Shell` (`ssh`)，211–212
- 单页，207
- 网站的可用副本，208
- 网站，镜像，208
- 使用 `wget`，207–208

### 内存磁盘系统，创建，116–117
- 挂载选项，121
- 已挂载，120
- 已挂载的，利用率摘要，124
- 挂载，118–121
- 挂载为读/写或只读，121
- 多个目录，显示，125
- 网络共享文件系统，107
- 输出，显示，125
- Windows，213
- `Filezilla`，213
- 过滤器，不可访问的目录，66

### `find` 命令
- 对文件进行操作 (`exec` 选项)，66
- 目录，查找，66
- 磁盘空间，检查，125–126
- `root` 用户账户，使用，125
- FreeBSD 支持，106–107
- 交换区，在文件内创建，117–118
- 交换区，开启，118
- 交换文件，列出，118
- 对时间依赖性检查，116
- 卸挂载，121–122
- 不可访问的目录，过滤，65
- 端口，搜索软件，20
- 使用正则表达式，65
- `root` 文件（`root` `file`），搜索，65
- 搜索准则，否定，66
- 基于大小的搜索，65
- 基于时间戳的搜索，66
- 未访问过的文件，66

### `findsm` 命令，`smb` 主机，其栈，215

### 文件传输协议 (`ftp`)，209–211
- 匿名访问，173
- 连接到服务器，209
- 下载命令，210
- FreeBSD 访问，17
- `ftpcopy` 应用，构建，25–26
- `finger` 命令，用户信息，检查，255
- `Firebox`，配置文件，278
- 防火墙，258–261
- `IPFILTER`，启用，259
- `ipfw`，启动服务，260
- 规则，添加，259–260
- 设置，259
- `sysinstal` 工具，13, 18, 19, 21, 24
- 状态检查，260–261
- vim 编辑器，72

# 索引 = F–G

- `flac` 命令，`wav` 转 `flac`
- `FreeBSDMall`，13
- 编码，95
- `Freenode`，219–220
- `flac` 文件
- `fsck` 命令
- 从 `aiff` 编码，95
- 卸载后检查，123
- 从 `wav` 编码，95
- 从后台检查，122
- 图像，添加，95
- DOS 文件系统，检查，123
- 闪存盘
- 有错误的文件系统，检查，123–124
- 启动镜像，复制到，62
- IDE 驱动器克隆，复制到，61
- 强制文件系统检查，122–123
- 私钥，保存到，232–233
- 不执行的打印命令，
- `ping` 洪流，发送，197
- UFS 文件系统，检查，122
- 文件夹作为目录，52
- `stab` 文件
- 其中的字段，119–120

## FreeBSD
- 文件系统，从...挂载，118–120
- 启动设置，更改，15
- `ftp` 见传输协议 (`ftp`)
- 配置，17–19
- `ftp` 被动，FreeBSD，17
- 文档，14
- `fuser` 命令
- 特性，3
- 杀死进程，153
- 支持的文件系统，103, 106–107
- 运行中的文件，153
- 安装日期，28
- 游戏，安装，14–19
- 解压缩，137
- `jetty` 进程，虚拟终端，35–36
- `nano` 编辑器，76
- `gif` 文件，转换为，98
- `Packages` 数组，19
- `gimp` 命令，在在前台/后台运行，155
- 升级，28
- GNOME 桌面配置，279
- `gparted` 工具，119–20
- `ports` 集合，安装，23–24
- 远程桌面，使用 `vnc`，241
- 终端窗口，打开/使用，33–35
- `ports` 集合，删除文件，30–31
- 用户管理，244
- GNOME 文本编辑器，特性，78
- `gnome-terminal` 命令，终端，35
- `README` 文件，创建，27
- 资源，4, 13–14, 19
- `gparted` 工具，108
- Grand Unified Boot Loader (`grub`)，软件，安装，21–22, 删除，23

# 索引 = G–H

- 图形用户界面 (`gui`)，损坏，7
- `grep` 命令，彩色搜索，81
- 显示不匹配的字符串，82
- 精确行，查找，81
- 列表文件，验证，69
- 文件名，显示，82
- 递归搜索，81
- 文本搜索，81
- 组 (`groups`)，所有权，更改，58
- 权限，252–253
- 特殊组，253
- 类型，253
- 用户，添加，253
- 多盘刻录，142
- `dvd`，刻录镜像，142
- GRUB 引导加载程序，176–178
- 文件，复制到目录，177
- 安装到主引导记录 (`mbr`)，177–178
- 启动时的镜像，178
- `grub` 命令，引导加载程序，重载，178
- `gstat` 命令，本地打开的磁盘设备，238
- 显示，167–168
- `gunzip` 命令，解压 `gzip` 文件，131
- `gzip` 压缩，130–131
- 目录中的所有文件，131
- `gzip` 文件信息，显示，130–131
- `tar` 命令，130–131
- 解压缩文件，131
- `halt` 命令，警告，179

## H
- 硬盘 (s)
- 启动镜像，复制，62
- 兼容模式，104
- 专用模式，104
- IDE 驱动器，克隆分区，61
- 硬盘分区，103–106, 115
- 更改，写入磁盘，108–109
- 配置，查看，105
- 磁盘标签，写入，112
- 磁盘空间划分，查看，104–105
- IDE 驱动器，压缩备份，61
- 分区。见硬盘分区：`slice` (s)
- 使用 `bsdlabel`，113
- `fdisk`，15–16, 107–109
- FreeBSD，15–16
- `stab` 文件，从...挂载系统，118–120
- `gparted/qpart` 工具，108
- 挂载点，指定，112
- 已挂载的分区，显示，176
- 多个操作系统，操作，174–175
- 分区大小，指定，112
- 分区表，更改其中的信息，110–111
- 分区，更改，112–113
- `slice` 上的分区，查看，176
- 修改权限的命令，111
- 根分区，104
- 使用 `syscall`，111–113
- UFS 文件系统，在分区上创建，133–114
- 另见 `slice` (s)
- 硬链接
- 创建，53–54
- 功能，53
- 网络备份，轮换文件，135–136

# 索引 = H–I

- 硬件，182–183
- 组件，列出，183
- 网络，186
- `pci` 设备信息，列出，182–183
- `nic` 能力，显示，187–188
- `nic`，硬速率，188
- `nic`，启动/停止，191
- `nic` 名称，显示，187
- `nic` 设置，187–189
- 无线卡，配置，193
- `ImageMagic`，安装，8
- 图像，97–101
- 缩图，创建，98–99
- `head` 命令，文件顶部，查看，79
- 头部信息
- 音频文件，查看，94
- `flac` 文件，添加，95
- `iso9660` 镜像，139
- 文本，80
- 页面文本，89
- 命令帮助信息，9
- 在 GRUB 启动屏幕上，178
- 关于信息，查看，97
- 目录大小，100–101
- 调整，98
- 轮换，98
- 文本，添加，98
- `INDEX` 文件，软件检查，28
- `HISTCDMD`，273
- `HISTFILE`，273
- `HISTFILESIZE`，273
- 历史，bash shell。见 bash shell
- 历史，37
- `HOME`，273
- 主机 (s)
- 连接性，检查，196–197
- 受信任，添加，279
- 主机名 (s)。见 `hostname` 命令
- `HOSTTYPE`，273
- 命令的帮助，11
- 穿过屏幕，11
- 继承，环境变量，45
- `inode` (s)
- 定义，124
- 显示，54
- 占用率，检查，124
- Shell 的输入，显示，39
- FreeBSD 安装，14–19
- `hostname` 命令
- 启动时的主机名设置，196
- 反向 `dns` 查询，196
- 临时主机名设置，196
- Internet
- `elinks` 浏览器，205–206
- 手册页，10
- 协议，故障排除，226
- 软件包包，从...安装，8
- 隧道到，229
- Internet 聊天 (IRC)，219–220
- 退出，220
- `id` 命令，用户信息，检查，254
- IDE 驱动器。见硬盘 (s)
- `identify` 命令，图像信息，访问，97
- `ifconfig` 命令
- 以太网卡设置，显示，147

# 索引 I–K

- `freenode` 服务器, 连接至, 219–220
- 帮助, 220
- 加入频道, 220
- 代理客户端/跳板器 (`bouncer`), 219
- 发送消息, 220
- 互联网超级服务器进程 (Internet Super Server Daemon), 217, 257
- `ip` 地址
  - 查看主机 `ip` 地址, 195
  - `ip` 连通性, 检查, 197
  - 使用中的 `ip`, 检查, 198
  - `nic`, 添加地址, 188
  - `samba`, 查找地址, 217
  - 子网查询, 198
  - 查看, 199
- `ipfilter`. 参见防火墙 (`firewalls`)
- 防火墙 (`firewall`), 295
- `ipfw` 命令
  - 防墙规则, 添加, 261
  - 防墙规则, 检查, 260–261
- `irc` 聊天, 网站, 5
- `irssi`
  - 命令,帮助, 220
  - 安装, 219–220
  - 消息,发送, 220
  - `irssi` 命令, `irssi`, 启动, 219
- `iso` 镜像
  - 创建, 62
  - 下载免费镜像, 14
  - 参见 `iso9660` 镜像
- `iso9660` 镜像, 139–140
  - 检查, 139–140
  - 创建镜像, 138
  - 扩展名, 138
  - 添加头文件信息, 139
  - 挂载, 140
  - 添加多个源, 139
- `isoinfo` 命令, 头文件信息,
  - 查看, 139–140
- `isocat` 命令
  - 打印 `cpu` 利用率报告, 165
  - 查看 `cpu` 利用率报告, 164
  - 显示磁盘统计信息, 167

# J

- JED 编辑器, 73
- `jobs` 命令, 后台任务,
  - 管理, 155
- JOE 编辑器, 73–75
  - 用于编辑的控制键, 73–75
  - 安装, 73
- `joe` 命令, 73–75
  - 打开文本文件, 73
  - 拼写检查, 73
  - 添加文本, 73
- `join` 命令, freebsd `irc` 频道,
  - 加入, 220
- Joliet 扩展, 添加至
  - `iso` 镜像, 138
- 日志 (`journaling`), 以及 `ext3` 文件系统, 106
- `jpeg` 文件, 转换为其他格式, 98

# K

- `k3b`, 137
- KDE 桌面
  - 配置文件, 279
  - 终端模拟器, 35
- KDE 编辑器, 特性, 78
- 内核模块 (`kernel` `modules`), 179–182
  - 添加模块, 182
  - 启用/禁用功能, 15
- 内核 `slab` 内存缓存统计,
  - 查看, 163–164
- 内核空间 (`kernel` `space`), 164–165
  - 已加载, 查看信息, 181
  - 加载, 15
  - 启动位置, 扫描, 178
  - 参数, 控制, 182
  - 关于处理，信息, 180–181
  - 排序, 83
- 系统消息缓冲区命令,
  - 查看, 180
- 键盘快捷键
  - `elinks` 浏览器, 206
  - JOE 编辑器, 73–75

# 索引 K–L

- `nano` 编辑器, 76–77
- vi 编辑器, 265–266
- 杀死运行中的进程
  - `kill` 命令, 157
  - `killall` 命令, 157
  - 向运行进程发送信号, 157
  - 按名称停止, 157
- `vnc` 服务器, 240
- `kld` 命令, 140
  - 模块, 加载, 182, 219
- `kldstat`
  - 内核模块, 按大小排序, 83
  - 查看已加载模块信息, 181
- `kldun` 命令, 模块,
  - 卸载, 182
- `konsole`, 35
  - 新目录, 切换, 211
  - 路径补全, 212
  - 远程目录权限, 更改, 211
  - 服务器目录, 切换, 211
  - 上文件到服务器, 211
- `lftpget` 命令, 非交互式下载, 211
- 行间距, 双倍行距, 80
- `LINES`, 273
- 链接(s). 参见硬链接 (`hard` `links`); 符号链接 (`symbolic` `links`)
- Linux
  - 引导加载程序, 14
  - FreeBSD 配置, 18
  - 安装, 174

# L

- `lame` 命令
  - `mp3` 格式, 文件转换, 95
  - 标签信息, 添加到 `mp3` 文件, 95–96
- 网卡 (`lan` `cards`), 类型, 192–193
- `last` 命令, 登录, 检查, 254
- `leafpad` 编辑器, 78
- 遗留通信工具, `telnet`
- `less` 命令
  - `less`, 226
- `ln` 命令, 硬/符号链接,
  - 创建, 53, 169
- `load` 命令, 内核/模块,
  - 加载, 15
- 本地文件系统. 参见文件系统 (`file` `systems`)
- `locate` 命令, 文件, 64–65
- `logger` 命令, 消息, 发送至
  - `syslog`, 261
- 登录类, 249–250
  - 定义, 249
  - 特性, 更改, 249–250
  - 数据库, 重建, 250
- `LOGNAME`, 73
- 分页, 79–80, 180–181
- 滚动, 80
- `strings` 命令, 查找, 80
- `LESS`, 273
- `lftp` 命令
  - 书签位置, 210
  - 关闭会话, 211
  - 当前目录, 检查, 210
  - 当前目录, 列出, 210
  - 在服务器上创建目录, 211
  - 传输到后台, 发送至, 209–210
  - 本地目录, 切换, 211
  - 匹配的文件, 上传, 211
- `loops/looping`
  - 文件系统, 回环挂载, 211
  - shell 脚本, 49
  - 小写字母转大写, 84–85
  - 设备文件, 列出, 54
  - 识别为目录, 53
- 文件列表, 显示, 52, 67
- 文件类型, 在列表中的外观, 68
- 文件, 15
- `lftp` 列表，内容, 225
- `iso` 内容, 检查, 140
- 管道/套接, 列出, 54–55
- 新行, 删除, 84
- 换行符，替换为空格, 84

# 索引 L–M

- 输出, 重定向, 38–39, 80
- 目录中的端口, 分页, 80
- `attr` 命令, 文件属性, 列出, 62
- `dev` 命令, 设备名称, 列出, 15
- `lsmod` 命令, 已加载模块名称, 查看, 15
- `lsof` 命令, 打开文件/目录, 168
- `lspci` 命令
  - `pci` 音频设备, 89–90
  - `pci` 硬件信息, 列出, 182–183
  - 无线卡, 查找, 192
- `lurking`, 219
- `zop` 命令, 130–131
- 归档 (`archives`), 132
- 压缩文件, 131
- 提取归档, 130
- `tar` 命令, 130
- 解压缩文件, 132
- `man` 命令
  - 所有页面, 显示, 10
  - 手页, 显示, 9
  - 页面章节, 查看, 10
- 主引导记录 (Master Boot Record), 107
- 复制到文件, 62
- 安装到 GRUB 引导加载程序, 177–178
- 警告, 177
- MBOX 格式, 电子邮件, 221
- `md5sum` 命令
  - `md5sum` 数据, 检查, 68–69
  - 软件, 查找, 19
- `mdconfig` 命令
  - 创建 `iso` 内存设备, 140
- 本地磁盘文件, 识别, 117
- 进程内存消耗, 查看, 163
- 内核 `slab` 内存, 163–164
- 常驻内存, 查看, 162
- 按使用排序进程, 82
- 使用, 屏幕导向视图, 162
- 使用, 时间导向视图, 163
- 本地磁盘文件系统, 116–117
- 挂载与卸载, 117
- 文件输出合并, 86
- 消息缓冲区, 内容, 查看, 180
- Microsoft Windows
- Mac OS X, 3
- `MACHYPE`, 274
- `MAIL`, 274
- `mail` 命令, 221–222
- 打开邮箱箱, 221–222
- `MAILCHECK`, 274
- 邮件列表, 网站, 5
- `make` 命令
  - 在 `distfile` 上运行校验和, 25–26
  - 下载 `distfile`, 27
- 构建 `ftpcopy` 应用程序, 25–26
- 创建 `README.html` 文件, 27
- 手页 (`man` `pages`)
  - 显示命令显示, 9–10
  - 查找, 67
  - 用于 FreeBSD, 20
  - 互联网上, 10
  - 章节, 10
  - 网站, 10
- 文件传输, 213
- 安装, 174
- 安装, 14
- `ssh` 工具, 227
- 镜像 (`mirroring`)
  - 远程目录, 135
  - 软件镜像, 来源, 5
  - 网站, 208
- `mixer` 命令, 调整音量, 92
- `mdir` 命令
  - 创建目录, 52–53
- 创建 GRUB 目录, 177
- 挂载点, 创建, 114, 117, 140
- 路径, 编辑, 46
- 端口, 创建, 24
- `vnc` 目录, 创建, 23
- `mkfifo` 命令, 命名管道, 创建, 55
- `mkfs` 命令
  - 检查坏块, 115
  - `ext3/` 文件系统, 挂载到分区, 114
- `mkisofs` 命令
  - 创建 `iso` 镜像, 137–140
  - 扩展名, 类型, 138
  - 镜像文件, 139
  - 添加头文件信息, 139
  - 音频, 89–101
  - 静音, 92, 101

# 索引 M–N

- `mp3` 文件
  - 转换为其他格式, 95
  - 从 `wav/aiff` 转换, 95
- `mp3` 文件, 播放, 91
- 播放列表, 播放歌曲, 91
- 添加标签信息, 95–96
- 查看标签信息, 96
- 多媒体, 89–101
- `iso` 镜像, 创建, 138
- 多个源, 添加到镜像, 139
- 分页, 79–80, 180–181
- 参见文件系统 (`file` `systems`)
- 参见 `iso` 镜像, 140
- `samba` 共享目录, 217
- `ssh` 共享目录, 219
- `mutt` 命令, 221–222
- 附件,发送, 222
- 键盘快捷键, 223
- 邮件会话, 开始, 222–223
- 发送新消息, 223
- `mv` 命令
  - 备份, 旋转, 135
- 保存私钥, 232
- 命名管道. 参见管道 (`piping`)
- `nano` 编辑器, 73–76
  - 用于编辑的控制键, 73–77
- `nano` 命令, 76
  - 拼写检查, 76
- `autilus`, 137
- 配置文件, 279
- `dnis` `minpoint` `writer`, 192
- 编辑器, 78
- 挂载文件系统, 指定
  - 挂载, 120–121
  - 文件系统, 挂载, 114
  - 在 `PATH` 中第一个, 显示, 8
  - `iso` 镜像, 挂载, 140
  - 本地文件系统, 挂载, 到 120
  - 回环挂载, 121
  - 本地磁盘, 挂载, 117
  - 用设备名称挂载, 121
  - 仅挂载点, 121
  - 挂载的文件系统, 列出, 120
  - 挂载的分区, 显示, 104–105
  - 挂载的系统, 列出, 120
  - `nfs` 共享目录, 214–215
  - 读写或只读, 指定, 121
  - `samba` 共享, 挂载, 217
- 鼠标, 启用, 18

# 索引 N

- `tcp` 连接，激活，查看，189–190
- `tcp` 统计数据，列出，201
- `tcp/icmp/udp` 摘要，显示，201
- `netware` 文件系统，107
- 网络备份，133–137
  - 目录，镜像，135
  - 从本地系统到远程系统，拷贝文件，134
  - 从多个客户端，收集备份，134
  - 通过 `openssh` 备份，133–134
  - 轮轮文件，135–136
  - 使用 `rsync` 备份，134–136
  - 快照方法，103
  - 同步文件，136–137
  - 使用 `unison` 备份，136–137
- 网络连接，185–203
  - 激活连接，检查，189–190
  - `dns` 服务器，194–196
  - 以太网网卡 (`nic`)，186–190
  - 主机扫描，202
  - 接口名称，显示，187
  - 接口，关闭/上线，190–191
  - 网络扫描，202–203
  - 网络服务，启动/停止，191–192
  - 数据包报头信息，查看，202
  - 包级流量信息，202
  - 相关问题。参见连接故障排除
  - 关闭，191
  - 启动，191
  - 无线。参见无线连接
- 网络连接，故障排除，196–203
  - 激活的套接字 (`socket`)信息，查看，201
  - 地址解析协议 (`arp`)，检查，197–198
  - 接口上的数据传输，显示，202
  - 默认网关，检查，196–197
  - 默认路由，更改，200
  - 删除路由，200
  - 互联网协议，226
  - `ip` 地址，查看，199
  - `ip` 连性，检查，197
  - `ip` 使用中，检查，198
  - 本地数据表，显示，199–200
  - 网络适配卡，检查，186–187
  - 新路由，添加到网络，200
  - 故障点，识别，198–199
  - 端口，连接到，199
  - 远程主机，路由追踪 (`trace` `route`)，199
  - 路由表，显示，200
  - `tcp` 统计数据，列出，201
  - `tcp/icmp/udp` 摘要，显示，201
- 网络文件系统 (`nfs`)
  - 启用，18
  - 挂起，中断，215
  - 网络共享文件系统，类型，107
  - 权限，214
  - 进程，查看，192
  - 服务，启动，213
  - 共享目录，查看，214
  - 共享，挂载，214–215
  - 状态检查，192
- 网络适配卡 (`nic`)。参见以太网网卡 (`nic`)
- 网络资源，205–223
  - 聊天，219–220
  - `elinks` 浏览器，205–206
  - 电子邮件，220–223
  - 文件传输，208–213
  - 远程目录，213–219
  - 从远程服务器，下载文件，207–208
  - 网络服务，255–258
  - 域名系统 (`dns`) 服务，257–258
  - 启用服务，256
- 文件传输协议守护进程 (`ftpd`)，258
- 互联网服务器守护进程 (Internet Server Daemon)，257
- 安全 `shell` 服务 (`sshd`)，258
  - 启动时启动，255–256
- 志日志守护进程 (`syslog` `daemon`)，256–257
- 网络时间协议 (`ntp`)，时间/日期，设置，170–172
- `newfs` 命令
  - DOS 文件系统，创建，123
  - UFS 文件系统，创建，117
  - 在分区上创建 UFS 文件系统，113–114
- 换行符，添加到文本流中，84
- `nfs` (网络文件系统)。参见网络文件系统 (`nfs`)
- `nfd` 命令，`nfs` 服务，启动，213
- `nice` 命令
  - `nice` 值，更改，154
  - 运行中的进程，调整优先级，154
  - 警告，154
- `nmap` 命令
  - 主机扫描，202, 202–203
  - 网络扫描，202
  - 端口扫描，202
  - 可见性，202
- `nmblookup` 命令，`ip` 地址，识别，217
- `nohup` 命令，避免挂断信号，157
- `nlogin`，登录类，250
- NT 文件系统，特征，106
- `tnpd` 命令，`ntp` 时间，171
- `tnpdate` 命令
  - `ntp` 时间，设置，171
- `tnppd` 命令，作为未来参考，171
- `ogg123` 命令
  - `ogg` 文件，播放，91
  - 播放列表，从中播放歌曲，91
  - 重复歌曲，91
  - Web 地址，播放，91
- `oggenc` 命令，音乐，编码，93–94
- `ogginfo` 命令，报头信息，查看，94
- `OLDPWD`，274
- 在线社区，5–6
- 开源系统 (`oss`)，91–92, 特征，3
  - 资源，网站，54
- 通过 `openssh` 备份，133–134 参见安全 `shell` (`ssh`)
  - 基于 `bsd`，3–4
  - 多个，安装，174
  - Windows，先安装，14
  - 两个，启动加载器，174–175
  - shell 输出，38–40
  - 反引号，使用，40
  - 直接到位桶，39
  - 直接到文件，38–39
  - 错误输出 (`stderr`)，38
  - 参数，通过，40
  - 管道，39
  - 从进程重定向，39
  - 文本文件，合并，86
  - 输出到 `patch` 文件，86
  - 发送到打印机或文件，80
  - 所有权，更改，58
  - `od` 命令，八进制 `dump`，查看，61
  - `ogg` 文件，播放，91
  - `Packages`，FreeBSD，192
  - `PacketFilter`，259
  - `PAGER`，274
  - 分页，文本文件，80
  - 过文本文件分页，79–80
  - 并行 `ip`：功能，186
- 分区。参见硬盘：`slice(s)`
- `password` 命令
  - 普通用户，更改，252
  - `root` 用户，更改，252
  - 密码 (s)
  - 账户信息，更改，250–251
  - 组成，252
  - `ftp` 服务器，207
  - 为 `root` 用户，分配，18
  - `root` 用户，更改，252
  - shell，36
  - 用户账户，更改，252
  - 用户账户，用于文件，246
  - `vnc` 密码，创建，239
  - 警告，246
  - `patch` 命令，输出到 `patch` 文件，86
  - 输出到 `patch` 文件，86
  - `PATH` (.)：功能，46
  - `mount/umap` 命令中，显示，8
  - shell 脚本中，45–46
  - 权限 (s)，56–58
  - 更改，56–57
  - 组，252–253
  - 列表文件，相关，55–56
  - 共享目录，214
  - 递归更改，58
  - 设置，53, 56
  - 掩值，58
- `pgrep` 命令
  - 进程 ID，查找，152
  - 用户相关进程，查找，152
- Phoenix，219
- pico 编辑器，特征，76
- `ping` 命令
  - 选项，197
  - `ip` 连性，检查，197
  - 警告，197
- 管道功能，51, 54
  - 命名管道，创建，55
  - 命名管道，示例，54–55
  - shell 输出，39
- `pkg_add` 命令
  - `fuse-sshfs` 软件，安装，219
  - GRUB，安装，177
  - 远程桌面，添加，235
  - `samba`，安装，215
  - 软件包，安装，21–22, 24
  - `vnc` 客户端/服务端，安装，239
- `pkg_cutleaves` 命令
  - 未引用的包，列出，30–31
- `pkg_delete` 命令，软件包，移除，22–23
- `pkg_info` 命令
  - `ftpcopy` 软件包列表，文件，20
  - 软件包依赖，检查，20
  - 软件包信息，20, 39–40
  - 排序，82
- `pkg_version` 命令，软件包，检查版本，28
- `PKIZ`，127
- `play` 命令
  - 音频格式/效果，查看，90–91
  - 音乐文件，播放，91
  - 从播放列表，播放歌曲，91
- Plesk，244
- `png` 文件，转换到，98
- 点对协议，功能，186
- `popd` 命令
  - 添加/移除目录，60
  - 目录顺序，更改，60
- `portaudit` 命令
  - 安全数据库，下载，29
  - 漏洞，检查，29
- `portmanager` 命令，端口，
  - 升级，28
- 端口集合，23–31
  - 组成，23
  - 内容验证，22
  - 用于安装的 `cp-usp`，24
  - 目录，创建，24
  - `distfile`，25, 27, 30
  - `ftpcopy` 目录，25
  - 安装，24
  - 软件包安装，验证，26
- 端口数据库，搜索包，8
- 端口骨架，25
- 移除文件，30–31
- 移除端口，30
- 安全，29
- 软件，查找，19–20
- 空间需求，17
- `sysinstall` 安装，24
- 私钥
  - 从 `agent` 中移除密钥，233
  - 保存到闪存器，232
  - 存储，空闲，233
- `proc` 文件系统，67
- 进程
  - 激活，144–146
  - 后台作业，管理，155
  - 列输出，自定义定义，146–203
  - `crontab` 文件，创建，158–159
  - 从队列中删除作业，158
  - 查找，152–153
  - 前台/后台，切换，155
  - 忽略挂断信号，157
  - 层级，查看，146
  - 杀死运行中的进程，151, 153, 157
  - 正在进行的，150–151
  - 管道，54–55
  - 优先级，调整，154
  - 运行中的进程，按 `cpu` 使用率，166
  - 调度规则，157–159
  - 信号，发送，155–156
  - 以内存使用为基础排序，82
- 处理器。`cpu` 使用率
- 配置文件设置，终端窗口，34
- `PROMPT_COMMAND`，274
- 端口命令，移除端口，30
- `portsnap` 命令，端口，更新，24
- `portupgrade` 命令，端口，升级，24
- `PPID`，274
- `pr` 命令
  - 双倍间距，80
  - 文本，格式化，89
- `PRINTER`，274
- 打印
  - 列，87
  - 不执行命令的，123
  - 文件中的行/字/字节，82
  - 文本，发送到打印机，80
- `ps` 命令
  - 列输出，149
  - 文件的查看，79
  - 每一个运行进程，查看，145
  - `getty` 进程，25–36
  - 进程 ID，查找/管道，152
  - 进程列表，查看，221
  - 运行中的进程，自定义视图，149–150
  - 当前用户的运行进程，显示，144–145
  - 排序进程，82, 150
  - 文件头部，查看，79
  - 两个用户的信息查看，150
- `PS1`，274
- `PSCP` 文件传输，213

# Index = P–R

`PSFTP` 文件传输, 213
`pstree` 命令, 运行进程, 树形视图, 146
公钥认证
拷贝密钥, 231–232
使用 `Secure` `Shell` (`ssh`), 230–231

`pushd` 命令
添加/删除目录, 60
目录, 更改顺序, 60
`PuTTY`, 227
`PWD`, 274
`pwd` 命令
打印工作目录, 59
符号链接, 创建, 59–60

与 `Samba`, 225–218
与 `ssh` 文件系统, 218–219
从远程服务器下载文件, 207–208
远程系统管理, 225–242
旧命令工具, 226
`screen` 软件包, 233–235
使用 `Secure` `Shell` (`ssh`), 225–233
虚拟网络计算 (`vnc`), 239–242
Windows 远程桌面连接, 236–237

# Q

`qtarded` 实用, 108

# R

`RANDOM`, 274
字符范围, 指定, 84–85
RAR 格式, 特性, 130
`rcp` (远程拷贝), 225
`desktop` 命令, Windows 远程桌面, 连接, 237
`README`, FreeBSD 的特性, 27
`README.html` 文件, 创建, 27
只读访问, 文件系统, 挂载, 121
读/写访问, 文件系统, 挂载, 121
重启, 安装后, 19
`reboot` 命令
益处, 179
警告, 179
`regex`. 参见 regular expressions (正则表达式)
正则表达式
用其搜索文件, 65
文本字符串, 匹配, 71–72
`iser` 文件系统, 特性, 107
通过网络文件系统 (`nfs`) 共享远程目录, 213–215
X Window 系统, 238–239
`renice` 命令, 运行进程, 调整优先级, 152
替换, 文本操作, 83–84
调整大小, 98
`rexec` (远程执行), 225
`rlogin` (远程登录), 225
`rmuser` 命令, 用户账户, 删除, 251
`root` 分区, 104
`root` 用户 (超级用户), 41–44
权限委托, 43–44
磁盘使用, 显示, 125
启用环境, 42
密码, 分配, 18
密码, 更改, 252
shell 密码, 36
旋转, 98
`route` 命令
默认网关, 检查, 196–197
默认网关, 添加, 200
删除路由, 200
本地路由表, 显示, 199–200
添加新路由, 200
路由表, 显示, 199–200
`rsh` (远程 `shell`), 225
`rsapshot` 命令, 与 `rsync` 命令, 133–136
硬链接, 使用, 135
增量备份, 135
镜像目录, 135
与 `rsn` 命令, 133
`elinks` 浏览器, 206

# S

文件, 使用正则表达式, 216
- 与 `Samba`, 215–218
- `bsd` 用户, 添加, 216
- 配置文件, 检查, 218
- 文件锁, 查看, 217
- `ftp` 风格连接, 216
- `ip` 地址, 查找, 217
- 网络邻域, 文本表示, 215–216
- 服务器服务, 216
- 共享, 挂载, 217
- `smb` 主机, 扫描, 215
- `SWAT` 工具, 215
- `Samba` 文件系统, 107
- `scp` 命令, 211–212
- 拷贝到服务器, 212
- 指定端口, 指定, 212
- 递归拷贝, 212
- 时间戳/权限, 保留, 212
- 警告, 211
- `screen` 命令, 233–236
- 激活屏幕, 列出, 233–234
- 快捷键, 234–235
- 重新连接会话, 235
- `screen` 软件包, 安装, 233
- `screen` 会话, 共享, 235
- 会话, 命名, 235
- 多路复用器, 235
- 终端复用器, 233–236
- 控制键功能, 234
- 运行, 233
- 共享屏幕, 235
- 参见 `screen` command
- 文本编辑器, 71
- 脚本, 创建. 参见 shell scripts
- `elinks` 浏览器, 206
- `less` 命令, 80
- 按大小文件, 66–67
- `man` 页面, 查找, 67
- 搜索标准, 否定, 66
- 历史中的字符串, 38
- 文本, 80–82
`SECONDS`, 274
`seconds`, 删除, 97
`Secure` `Shell` (`ssh`), 225–233
客户端, 配置, 227
配置文件, 279
文件系统, 共享, 218–219
强制退出, 228
远程主机中的日志, 228
远程文件, 拷贝, 212
使用公钥认证, 230–231
`SOCKS` 代理, 229–230
启动/停止, 191
Windows 工具, 227
`CUPS` 打印服务, 227–228
隧道, 用于 `x11` 客户端, 228
到 Internet 连接, 229
`x11` 端口转发, 启用, 227
版本 2, 益处, 227
虚拟网络计算 (`vnc`), 241
参见 `ssh` command
`Secure` `Shell` 服务 (`sshd`), 启用, 258
安全, 243–262
中央日志, 262
`chkroot`
防火墙, 258–261
组, 252–253
密码, 管理, 252
权限, 56–58
端口集合, 29
私钥, 存储, 232–233
Server Message Block (`smb`). 参见 `Samba`
启动变量, 设置, 15
环境变量, 显示, 42
`setenv`, 登录类, 250
`sftp` 命令, 文件传输, 282
`sha1sum` 文件, 68–69
`SHELL`, 274
`shell(s)`
别名, 41
命令行补全, 38
环境变量, 44–45
输出流, 重定向, 38–40
`root` 用户 (超级用户), 41–44
脚本. 参见 shell scripts
特殊字符, 271–272
`tail` 文件, 41
终端窗口访问, 33–36
用户特定设置, 36
变量, 列出, 272–275
参见 bash shell
`bsdlabel` 实用程序, 104
更改, 108, 110
创建或更改标签, 113
创建, 108–109, 111
定义的, 16, 103–104
删除, 110
显示, 112
标签, 更改/创建, 113
信息, 109–110, 175
分区, 创建, 113
分区分区, 创建, 112
分区分区, 创建, 176
参见 hard drive partitioning
`smap` 命令, BIOS SMAP 查看, 15
`smclient` 命令
`ftp` 文件共享, 216
服务, 列出, 216
`smbpasswd` 命令, `bsd` 用户, 添加到 `Samba`, 216
`smbstatus` 命令
摘要输出, 217
当前连接/文件锁, 查看, 217
`smbtree` 命令, 网络邻域, 文本表示, 215–216
快照方法, 网络备份, 133
`sockets`
拼写检查器
JOE 编辑器, 73
`nano` 编辑器, 76
功能, 51, 54
在系统上, 查看, 55
`socketstat` 命令, `sockets`, 列出, 55
`split` 命令, vi 编辑器屏幕, 分割, 265
`SOCKS` 代理, `ssh` 功能, 229–230
软件包包
文档, 子目录, 8
查找, 19–20
`info` 数据库页面, 目录, 11
使用端口安装. 参见集合
`ssh`. 参见 `Secure` `Shell` (`ssh`)
`ssh` 命令, 227–233
默认密钥, 232–233
Internet 服务, 隧道, 229
密钥对, 生成, 231
私钥, 存储, 232–233
按内存使用降序, 82
按内核模块大小, 83
输出管道到, 39
排序
按 `cpu` 使用率, 150, 166
内核模块, 83
按内存使用, 150
进程, 以内存使用为基准, 82
进程列表, 151
文本文件内容, 82
参见 `sort` 命令
声卡, 配置, 89–90
`sound-juicer`, CD 文件, 刻录/编码, 92
`sox` 命令
文件信息, 显示, 96
输出秒, 97
`wav` 文件, 拼接, 96
`soxmix` 命令, `wav` 文件, 混合, 96
空格
换行符, , 84
文本文件, 80
`ssh`, 在不同端口访问, 228
`ssh` 客户端, 配置, 227
`ssh` 会话, 强制退出, 228
`vnc` 服务器, 241
`x11` 客户端, 隧道, 228–229
`x11` 转发, 启用, 227
`shhfs` 命令, 远程目录, 挂载, 219
`stder`. 参见 out of shell
`stdin`. 参见 in of shell
`stout`. 参见 out of shell
粘滞位, 功能, 57–58
存储设备, 166–168
瓶颈, 检查, 167
文件/目录, 查看, 168
`su` 命令, shell, 超级用户
功能, 24
多次替换,
运行, 84
`sudo` 命令
shell, 使用权限委托, 43–44
警告, 43
`SunOS`, 3
超级用户. 参见 `root` users (超级用户)
支持
采取的步骤, 6–7
网站, 4–6

# 索引 = S–T

- 交换区域。参见 强制分区 (hard partitioning)
- 交换文件系统，特性，107
- `swappinfo` 命令
- 交换文件/分区，查看，118
- 交换分区信息，显示，105
- `swappoff` 命令，交换区域，关闭，118
- `swap` 命令
  - 交换区域，开启，118
  - 系统使用指令，118
- `SWAT` 工具，`samba`，215
- 旋涡效应，图像，100
- 符号链接
  - 备份文件，53
  - 创建目录，59–60
  - 创建文件，53–54
  - 功能，59
  - 与...同步文件，136–137
- `sysctl` 命令
  - 内核参数值，列出，182
  - 内核参数，列出，182
- `mbr`，覆盖，177
- 普通用户，添加，219
- `sysinstall`
  - 主菜单，返回，18
  - 作为菜单界面，21
  - 网络连接，配置，185–186
  - 分区，更改，111–113
  - 端口合集，安装，24
  - 切片 (`slices`)，更改，107–109
  - 软件包，13, 19, 21
- Syslog 守护进程，命令行，256–257
- `systat` 命令，`cpu` 使用率，查看，165
- 系统管理，远程。参见 远程系统管理
- 系统日志，`syslogfield`，消息，261
- 系统管理，161–183
  - 启动过程，172–178
  - `cpu` 使用率，164–166
  - 硬件，182–183
  - 内核模块，179–182
  - 内存管理，162–164
  - 停止系统，179
  - 存储设备，166–168
  - 系统服务，178–179
  - 时间/日期，168–172
  - 系统服务，178–179
  - 安装，178–179
  - 网络，启动/停止，191–192
- 系统使用共享协议 (`susp`)，
  - `iso9660` 镜像，138

# T

- `tail` 命令
  - 文件末尾，查看，79
  - 文件末尾，监控，79
  - 文件大小，监控，41
- 磁带归档文件，也称为 `tar` 命令
  - 使用，关于 Web 网络系统信息，129
- `tar` 命令
  - 归档内容，列出，132
  - 归档/压缩输出，128–129
  - 基础操作，128
  - 行为，Linux 系统之间的差异，128
  - 与 `bzip2` 压缩一起，128, 130
  - 包含/不包含横杠，128
  - 提取/压缩文件，130
  - 文件，添加到归档，132
  - 从本地到远程系统，拷贝文件，134
  - 使用 `l` 压缩，130
  - 匹配要添加到归档的多个文件，匹配，132
  - 从远程站点运行，134
  - 将文件返回系统，129
  - `tar/lz` 文件内容，列出，132
  - `tgz`，向其写入文件，134
  - 解压/解包 `untars` 归档文件，129
- `tcp`。参见 传输层协议 (`tcp`)
- `tcpdump` 命令，`tcp` 数据包，查找，202

# 索引

- `telnet` 命令，互联网协议，故障排除，226
- `TERM`，274
- 终端复用器，`screen` 包，233–235
- 终端服务客户端。参见 Windows 远程桌面连接
- 终端窗口，33–36
  - 键位序列，34
  - `elinks` 浏览器，205–206
    - 打开，33
  - 个人配置设置，34
  - 回滚行数，34
  - shell 管理设置，34
  - 类型，35
  - 虚拟终端，35–36
- `testpart` 命令
  - 配置文件，测试，218
  - 默认项，查看，218
  - `samba` 配置，检查，218

- 文本
  - 字符实例，84–85
  - 列，处理，87
  - 内容，重定向，87
  - 转换为其他格式，88
  - 文件间的差异，检查，85–86
  - 双倍行距，80
  - 文件的内容，查看，79
  - 头信息，80
  - 图像，添加文本，98
  - 列出文件，78–79
  - 与正则表达式匹配，71–72
  - 多次替换，运行，84
  - 导航/滚动，80
  - 换行符，84
  - 行数/单词/字节，打印，82
  - 分页文件，80
  - 分页，79–80
  - 首次出现，83
  - 输出发送到打印机，80
  - 输出排序，82–83
  - 字符串，查找，80–82
  - 文本替换，83–84
  - 文件顶部，查看，79
  - 单词计数，82

- 文本编辑器
  - Emacs 编辑器，73
  - GNOME，78
  - JED 编辑器，73
  - JOE 编辑器，73–75
  - KDE 编辑器，78
  - `leafpad` 编辑器，78
  - `nano` 编辑器，73, 77
  - edit 编辑器，78
  - pico 编辑器，76
  - scribe 编辑器，78
  - vi 编辑器，72, 264–270
  - vim 编辑器，72
  - Emacs 编辑器，73
  - `tgz` 文件，写入文件，134
  - 缩略图，创建，98–99
  - `tiff` 文件，转换为其他格式，98
  - 时间/日期，168–172
  - 显示，169–170
  - 网络时间协议 (`ntp`)，使用，
  - 时区，更改，169
  - 时区，设置，18
  - 运行时间，172
  - 基于时间戳搜索文件，65–66
- `top` 命令
  - `cpu` 使用率，查看，151
  - 帮助，151
  - 进程日志，创建，151
  - 内存消耗大小，查看，163
  - 内存使用，屏幕视图，162
  - 运行中的进程，150–151

- `touch` 命令
  - 空文件，创建，52
  - 硬链接/符号链接，创建，53
  - 字符，替换，84
  - 字母，删除，84
- `tr` 命令
  - 路由追踪，198–199
  - 瓶颈，检查，198–199
  - `ip` 地址，查看，199
  - 设置不同端口，199
  - `tcp` 数据包，路由追踪，199
  - `ssh` 转发端口，228–229
  - 数据包信息，显示，200
  - 活动摘要，201
- `tripwire` 包，262
- 故障排除
  - 命令未找到，7–8
  - 电子邮件，226
  - 客户端命令，远程桌面，检查，236–237
  - `ext2` 文件系统，设置，116
  - 文件系统属性，查看，115–116
  - 基于间隔的系统检查，116
  - 时间依赖检查，116
- 隧道
  - 用于 `cups` 打印服务，227–228
  - 连接到互联网，229
  - 用于 `x11` 客户端，228
  - `x11` 端口转发，启用，227

# U
- UFS 文件系统
  - 检查，122–123
  - 在分区上创建，113–114
  - FreeBSD 默认，16, 106
- UFS2 文件系统，16
- `UID`，275
- `unalias` 命令，移除别名，345
- `uname` 命令，BSD 版本，显示，180, 221
- 统一格式，定义，85
- Union文件系统，特性，107
- `unison` 命令，136–137
  - 自动操作，137
  - 在命令行模式下运行，136
  - 个人配置，创建，137
  - 与...同步文件，136–137
- IX 文件系统，103
- `ix2dos` 命令，文件创建，188
- `unmask` 命令，权限，设置，58
- `unmask` 值，登录类，250, 权限，58
- `unmount`
  - 文件系统，121–122
  - 参见 `unmount` 命令
- `unmount` 命令
  - 设备名称，通过...卸载，122
  - 失败，122
  - `iso` 镜像，卸载，140
  - 挂载点，通过...卸载，122
  - 在 `PATH` 中，查找，8
- `unar` 命令，130
- `unset` 命令，启动变量，15
- `ungrading`，端口合集，28
- `uptime` 命令，系统运行时间，检查，172
- USB 闪存盘。参见 闪存 (`flash` `drive`)
- Usenet 新闻组，站点，6

# 索引 = U–V

- `USER`，275
- 用户
  - 添加到组，253
  - 目录信息，显示，255
  - 关于查看信息，255
- Webmin，用户管理，244
- 用户账户，244–252
  - 详情，设置，247–248
  - 账户信息，更改，250–251
  - 账户信息，显示，244
  - 添加，244–245
  - 批量用户，添加，244–245
  - 删除，251–252
  - FreeBSD，198
  - 登录类，249–250
  - 选项，设置，248–249
  - 所有权，更改，58
  - 普通用户，添加，18
  - 参见 `unmount` 命令
- 用户登录，检查，255
- `cpu` 使用率，164–165
- 挂载的文件系统，124
- V
  - 详细信息，配合压缩，130–131
  - 内核模块，显示，181
  - 软件安装，22
- 用户账户，删除，251
- `vi` 命令，文本文件，264
- `vi` 编辑器，启动，264–270
- `vi` 编辑器，72
  - 添加/更改文本，266–267
  - 来自 `vim` 命令的别名，264
  - 删除/粘贴文本，267
  - Ex 命令，269–270
  - 键位命令，列出，265–266
  - 导航，265–266
  - 使用数字修改命令，268
  - 退出，264
  - 保存并退出，264
  - 保存文件，264
  - 多次编辑，编辑，264–265
  - 分屏，265
  - 文本文件，264
  - `vim` 增强包。参见 Vim (Vi Improv)
  - 在可视模式下，270
  - 写入另一个文件，264
- Vim (Vi Improv)
  - 优处，72
  - 打开，264
  - `xui` 版本，278
- `vip` 命令，账户信息，更改，250–251
- Vino，与 `vnc` 桌面共享，241–242
- 虚拟网络计算 (`vnc`) 组件，239
  - 配置文件，280
  - 远程桌面，225
  - 远程桌面，启用，240–241
  - 使用安全 `shell` (`ssh`)，241
  - 服务器，启动，239–240
  - 与 Vino 共享桌面，241–242
- 虚拟终端，35–36
  - 配置，36
  - `getty` 进程，35–36
  - 之间切换，35
- `visudo` 命令，对比 `sudo` 命令，43
- `vstat` 命令
  - 内核 内存缓存统计，随时间段查看，163–164
  - 内存使用随时间段查看，163
- `vncpasswd` 命令，`vnc` 密码，创建，239

# 索引 V–X

- `vncserver`, 杀死, 240
- `vnc` 服务器, 启动, 239–240
- `vncviewer` 命令, 远程桌面, 启用, 239
- 音量, 调整, 92
- 通配符, 归档文件, 匹配, 132
- Windows 远程桌面连接, 236–237
- 使用 `rdesktop` 连接, 237
- 远程桌面, 启用, 236
- 终端服务器客户端, 连接, 236–237

# W

- `wav` 文件, 合并, 96
- 编码为 `aiff`, 95
- 编码为 `flac`, 95
- 编码为 `mp3`, 95
- 编码为 `Ogg`, 93
- 混音, 96
- 播放, 91
- 提取, 93
- `WinSCP`, 213
- `WinZip`, 127
- 无线连接, 192–194
- `theros/Intersil/Lucent`, 命令, 194
- 配置, 193–194
- 驱动程序, 列表, 192–193
- 驱动程序, 加载, 193
- 通用驱动, 使用, 193
- 网卡, 类型, 192–193
- 扫描站点, 194
- 启动/停止, 194
- 状态检查, 194
- 无线网卡, 搜索, 192
- 文本文件, 字数, 检查, 832
- `wc` 命令, 文件行/字/字节, 打印, 82
- Web 地址, 播放, 91
- `wget` 命令, 207–208
- `ftp` 服务器登录, 207
- `html`, 附加到下载的文件, 208
- 中断的下载, 继续, 208
- 重命名为本地名称, 208
- 单页, 下载, 207
- 网站, 本地可用副本, 208
- 网站, 递归镜像, 208
- `whatis` 命令, 关键字搜索, `man` 页, 9
- `whereis` 命令, 文件, 查找, 67
- `which` 命令, 文件, 查找, 67
- `who` `am` `i` 命令, 用户信息, 检查, 254
- `who` 命令, 登录, 254
- `whoami` 命令, `root` 用户, 确认, 43
- `wicontrol` 命令
- 无线网卡信息, 查看, 194
- 无线网卡设置, 194
- `wiki`, 网站, 6

# X

- X GUI 版本, `vim` 编辑器, 78
- X Window 系统, 238–239
- 配置文件, 280
- 远程应用, 启用, 238
- 远程机器, 运行在, 238
- `x11` 端口转发, 启用, 227
- `x11` 客户端, 隧道传输, 228
- `xargs` 命令, 与 `exec` 命令相比, 66
- 输出, 重定向, 40
- `xcd-roast`, 137
- `xxat` 工具, 219
- `xclock` 命令, 远程时钟, 在本地打开, 238
- XEmacs 编辑器, 73
- `xhost` 命令, 远程应用, 允许, 237
- `xminees`, 安装, 22
- XMMS 音乐播放器, 配置文件, 280
- `xterm`, 35
- `xterm` 命令, 远程终端, 在本地打开, 238

# Z

- 缩放, 终端窗口, 34

# # 深入了解 Linux 工具箱。

查看该系列丛中的其他可用书籍。

![](img/a8f0676d6e7f319a693ce1963202001e_337_0.png)

![](img/a8f0676d6e7f319a693ce1963202001e_337_1.png)

![](img/a8f0676d6e7f319a693ce1963202001e_337_2.png)

现可在 `www.wiley.com` 购买

![](img/a8f0676d6e7f319a693ce1963202001e_337_3.png)

Wiley 和 Wiley 标志是 John Wiley & Sons, Inc. 及其或关联公司的注册商标。Linux 是 Linux Torvalds 的注册商标。所有其他商标均为其各自所有者的财产。

