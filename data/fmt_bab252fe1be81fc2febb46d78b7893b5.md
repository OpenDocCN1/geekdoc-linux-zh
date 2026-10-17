
## 22. 用户验证方法（User authentication method）
通常，在用户方面，您将在独立模式下使用家用计算机。但在业务环境中，您可能使用 NIS、LDAP 或 Samba 来获取允许访问您的计算机以及 LAN 上其他计算机的帐户列表。如果是后者，请选择“网络客户端（Network Client）”并选择 NIS（UNIX 系统用于共享配置文件的常用设施）或 LDAP（标准目录服务，用于共享地址簿和其他信息，取决于公司支持）。Samba 允许您使用 Windows 文件和打印功能。点击“下一步”。

## 23. 新用户（New user）
在独立模式下，您通常会使用家庭计算机。根据提示添加至少一个账户，对于您的计算机。现在，您仅为独立机器设置了 root 帐户。

如果您在之前的安装中创建了账户并留下了自动登录，openSUSE 应该会自动登录。如果您看到的是登录界面，请使用该账户登录。以下是帮助您开始使用 openSUSE 的一些内容：

- 桌面应用程序（Desktop applications）——默认的 openSUSE 包含了易于访问的桌面应用程序。在桌面上，尝试 Office 图标打开 OpenOffice 处理文档、电子表格、演示文稿、绘图、网页或其他内容类型。桌面上的 openSUSE 图标让您可以在数十应用程序中进行尝试。
- 我的电脑（My Computer）——桌面上的计算机图标允许您保存可移动介质和挂载分区，还可以在 Konqueror 中访问桌面、文档和 public_html 文件夹。
- 重新配置您的计算机（Reconfigure your computer）——通过选择应用程序-系统-管理员设置进入 YaST 管理工具。您可以在出现的 YaST 控制中心中重新配置系统硬件和软件。

如果您想配置桌面（更改背景、屏幕保护程序或主题），请使用 KDE 控制中心，就像使用任何现代 KDE 控制中心一样。您可以通过 openSUSE 菜单启动控制中心（选择我的收藏）。

## 24. 硬件配置（Hardware configuration）
在此屏幕上，您可以选择保存您的设置。openSUSE 安装程序显示了检测到的所有硬件。您可以重新配置您的硬件、软件，或者对其进行测试。

## 25. 完成（Finish）
准备就绪后点击“完成”。设置将被写入硬盘。显示安装完成屏幕。

## 总结
SUSE 通常被认为是企业级 Linux 系统的最佳选择（仅次 Red Hat Linux）。其图形安装和管理工具（实现在名为 YaST 的设施）使其与面向技术用户的其他 Linux 发行版区别开。自从 SUSE 在 2003 年被 Novell 收购以来，SUSE Linux 已成为更大、企业级产品线的一部分。提供 SUSE Linux 盒装。提供多个级别的支持服务。凭借 Novell 全球的销售和培训组织，SUSE Linux 有了成为全球最受欢迎的商业 Linux 系统所需的支持。将 SUSE 发布给开源社区的 openSUSE 项目确保了最新、最强大的功能可用或处于 SUSE 的开发规划中。

# 第 11 章
## 运行 KNOPPIX

计算机的操作系统通常驻留在硬盘上——但并非必须如此。当计算机启动时，它通常会检查驱动器中是否有 CD、软盘或 DVD，并尝试从那里启动（取决于 BIOS 设置）。因此，既然这些介质上拥有高达 700MB（CD）或 8.4GB（双层 DVD）的空间，为什么不直接用它们来启动整个操作系统呢？

嗯，像 KNOPPIX 这样的可启动 Linux 发行版（也称为 *live CDs* 活动光盘）究竟是做什么的。在 KNOPPIX 的情况下，一张 CD 包含了高达 2GB 的压缩软件供你运行，这些软件会在运行时进行解压缩。启动它，你就可以尝试功能齐全的 Linux 系统的所有功能，而无需触碰你硬盘的内容。

KNOPPIX 包含在随书提供的 DVD 中。事实上，它是默认选项。将 DVD 插入电脑的驱动器，你将看到启动界面。进入 KNOPPIX 应该就会启动，你就可以像本章描述的那样开始使用它。

如果你从未用过 Linux，KNOPPIX 为你提供了一个非常安全的使用机会。如果你有 Linux 经验，KNOPPIX 可以作为一个工具，随随地携带 Linux，用于排除计算机故障，或检查计算机是否能运行 Linux。无论什么情况下，你都可以利用这一章来了解一下你可以用 Knopix 运行的一些很棒的 Linux 功能。

### Knopix 功能

KNOPPIX 的功能多到让人很难从何处开始。本文编写时 KNOPPIX 的最新官方版本（KNOPPIX 5.1.1）具有 X.Org 7.1、OpenOffice.org 2.1.0、KDE 3.5.5、GIMP 2.2.11、Linux 内核 2.6.19 以及许多多媒体应用。更多信息可以在 KNOPPIX 首页（www.knoppix.com）上找到。

最新版本的 KNOPPIX 最实用的功能之一是你可以轻松地创建自己的、个性化的 KNOPPIX 光盘。可用选项非常多，书中有足够的空间在书中涵盖它们。关于如何创建你自己的 KNOPPIX 更多信息，请参阅 www.knoppix.net。

![](img/d7f79c91d15076e71790c1b4e1d072d0_382_0.png)

KNOPPIX 包含了对 NTFS 文件系统的支持，因此你可以在安装了 Windows XP 的计算机上运行 KNOPPIX，并从硬盘访问你的文件。这是在 Windows Linux 应用中（在永久切换之前）尝试你的文档、音乐、电影或其他内容的一种好方法。KNOPPIX 5.0 已经很好支持的 NTFS 透明访问，据说能让向 KNOPPIX 分区写入数据比之前的版本更安全。

### 理解 KNOPPIX

如果你迫不及待想要开始，不必继续往下读了。在大多数情况下，你只需要将 DVD 插入电脑，重启计算机，然后开始使用 KNOPPIX。如果你有时间，可以多读一点。

KNOPPIX 是一个包含大量精选开源软件的可启动系统。最初，有一个 KNOPPIX 的 CD 版本（约 700MB 镜像）。现在，还有一个 DVD 版本（约 4GB 镜像）。随书提供的 DVD 中包含的是 KNOPPIX CD 镜像。

KNOPPIX 被认为最好的可启动 Linux。事实上，KNOPPIX 被用作许多专用 Live CDs 的基础，包括但不限于 KnopPIX（采用 GNOME 代替 KDE）、KnopPIX STD（安全）、KnopPIXMyth（MythTV 媒体播放器）和 KnopPIXAME（控制台游戏播放器）。要尝试最新功能，你应该从本章其余部分描述的最新版本 KNOPPIX 开始。

### KNOPPIX 新闻

随着 2006 年 6 月发布了 5.0.1 版本，KNOPPIX 变得更像一个完整的操作系统。添加了扩展功能，以便更方便地将 KNOPPIX 安装到硬盘。Live Update 功能添加了更新某些包的能力。总的来说，现在的打包侧重于保持与 KNOPPIX 基于的 Debian 软件包接近。5.1.1 版本继续增加了更多的硬件检测和配置能力。

### 探究 KNOPPIX 内部

在自动检测并配置你的计算机硬件后，KNOPPIX 会启动到一个功能齐全的桌面系统，带有数百个即插即用的桌面应用程序（无需登录）。它包含了一些强大的服务器和用户功能。事实上，功能太多了，我在这里甚至不会提到所有功能，但请看以下 KNOPPIX 的一些主要组件列表：

- KDE — 一个功能齐全的桌面（运行在 X 系统中），包含了用于配置桌面的工具。见第 3 章
- OpenOffice — OpenOffice 套件，你可以用它创建文档、演示文等强大的应用程序。见第 21 章
- 互联网 — Web 浏览器（Firefox）、即时消息（XChat）和电子邮件（Gmail）。见第 22 章
- 多媒体 — Audacity、Kaffeine、GIMP 和 ImageMagick。见第 20 章
- 游戏 — Cardoids、Quicks 和策略游戏。见第 23 章
- 管理工具 — 用于管理、调试和修复系统
- 服务器 — Apache、NFS、Samba、bind9 和 dhcpd。见第 19 章
- 编程 — 用于开发环境

## 第三部分选择和安装 Linux 发行版

KNOPPIX 基于 Debian，因此你可以使用 `apt` 和 `dpkg` 管理随 KNOPPIX 的软件包。关于使用 `apt` 和 `dpkg` 的信息，请参阅第 9 章。

### KNOPPIX 的酷之处

上述功能在许多 Linux 发行版中都是常见的。让它们在 KNOPPIX 中变得特别在于，你通常可以在几分钟内开始使用——无需分区磁盘、安装软件或进行配置。

然而，某些功能（与硬盘系统相比）是 KNOPPIX 特有的。特别是，KNOPPI 包括：
