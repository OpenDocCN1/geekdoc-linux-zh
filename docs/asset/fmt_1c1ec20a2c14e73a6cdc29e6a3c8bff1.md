
如果你不想从 PowerPC Linux 供应商处购买盒装 CD-ROM 套装，你可以下载并创建自己的 CD-ROM，无论是通过供应商网页上的链接还是通过 Linux CD-ROM 映像网站（例如，`http://www.linuxiso.org`）。请注意，在某些情况下（例如，使用 LinuxPPC 2000 时），你需要能够创建 HFS 格式的 CD-ROM，和/或确定 CD 映像实际上是 Mac OS 磁盘拷贝映像格式。（这需要从当前的启动磁盘引导以进行安装。）

选择要安装的发行版可能取决于个人偏好、品味、经济因素或偏见。如果你是使用特定 Linux 发行版（例如 SuSE）的基于 Intel PC 的用户，请选择兼容的 PowerPC 发行版。如果你完全是 Linux 新手，每个发行版都有很多可提供的东西。选择发行版的最佳方法是阅读 `comp.os.linux.powerpc` Usenet 新闻组，并提问以确定哪种发行版最适合你的计算机。

## 选择工作站或服务器

在安装 Linux 之前，你必须决定如何在你的 Mac 上使用 Linux。安装会根据你希望分配给 Linux 的硬盘空间量以及你计划如何使用计算机而有所不同。好消息是，随着兼容当今 PC 的日益增大的硬盘的出现，你应该有充足的空间。然而，如果你使用 PowerPC 进行视频编辑，即使有一块或多块 30GB 的硬盘，你的硬盘空间也可能有限。即使是在主驱动器上，也应该有足够的额外存储空间来安装完整的 Linux 系统。

当你安装 Linux 作为服务器运行时，你不需要安装那么多软件。Linux 及其众多的网络软件只需要几百兆字节。除非你计划托管一个活跃的 Web 站点或拥有大量软件和文档的 FTP 服务器集群，否则两 GB 的硬盘空间就绰绰有余了。另一方面，如果你希望将 Linux 用作开发平台或工作站，你需要额外的存储空间用于临时磁盘空间、软件库、文档和编程工具。如果你有存储空间并且希望学习 Linux，请安装所有软件。这将为你省去返回 Linux CD-ROM 安装额外软件或搜索所需包的工作。

安装要求因发行版而异。例如，在安装 SuSE PPC 7.1 时，你将提供几种自动化安装选项：

- 最小系统。此 150MB 安装提供了运行 Linux 所需的最少软件，并且不包括 Linux 的图形界面，即 X Window System 或 XFree86。维护和运行像这样的小型系统可能需要高级的管理技能和关于 Linux 的知识。
- 标准系统。这个 900MB 的安装提供了一个极简主义的 Linux 系统，包含 XFree86、打印支持、互联网访问软件以及其他工具。这是你可以安装并仍能高效地将 Linux 用作工作站的最低系统。
- 带办公套件的标准系统。这个 1.4GB 的安装包含一些更高级的编辑工具以及 XFree86 的附加软件包或*客户端*。建议使用少量硬盘空间开始使用是一个不错的选择。你以后总是可以安装额外的软件。
- 几乎包含所有内容。你需要超过 6GB 的硬盘存储空间，以及一个多小时甚至两个多小时的时间来安装所有的软件包。如果你有硬盘空间，想要进行软件开发，并且喜欢丰富的游戏和其他软件选择，这被强烈推荐。

请注意，这些需求是针对 SuSE Linux 的！其他发行版，如 Yellow Dog 或 LinuxPPC 2000，可能只需要 1.5GB 进行完整安装。你还需要考虑为文档、图形或其他个人项目预留的硬盘空间数量。例如，电子邮件文件在一年内可能会迅速增长到数百兆字节，尤其是如果你拥有高速互联网连接并发送和接收大型文档。

## 替代方案

基于 Intel 的 Linux 用户可以利用许多模拟其他操作系统的商业软件程序。例如，你可以使用 VMware 的模拟器在 Windows 下的窗口中运行 Linux，或者在 Linux X 会话期间的窗口中运行 Windows。

基于 Intel 的 Linux 用户还可以使用 Ardi 的 Executor 客户端在运行 Linux 时在 X 窗口中运行一些遗留的 Macintosh 应用程序。Ardi 的 CarbonIce Copies 应用程序也可以用于将模拟器的引擎捆绑到 Mac OS 应用程序中，使其能够在 Windows、Linux、DOS 或 OS/2 下运行。幸运的是，Mac 用户可以在使用 Mac OS 的同时在窗口中运行 Linux。Connectix 的 Virtual PC 3.0 配合 Red Hat Linux 提供了其他模拟器不具备的几种功能。其中一个功能是“保存状态”，它可以保存系统的状态，并允许你在不关机或重启的情况下停止或重启你的 Linux 会话。复制和粘贴，以及几个 USB 设备，也得到了支持。

这是一种在不分区 Mac 硬盘的情况下运行 Linux 的好方法，因为模拟器使用虚拟文件系统，或者硬盘上的一个大文件，来支持外部操作系统。

即使有了 Mac OS X，其核心使用 BSD UNIX 和新的 Mach 内核，并支持 XFree86 的选择性移植，你仍会发现针对 PowerPC 的 Linux 是一个可行的替代计算环境和平台。它拥有数量庞大的应用程序可供立即使用。

## 资源

- `http://devworld.apple.com/technotes/tn/tn1167.html#Section3`. Apple Computer 关于 Mac 的 NewWorld 架构的描述。
- `http://penquinppc.org/~benh/`. Ben Herrenschmidt 的 Linux 页面，其中包含指向 PowerPC 上 Linux 一些最新引导加载程序的链接。
- `http://www.yellowdoglinux.com`. Terra Soft, Inc. 发布的 Yellow Dog Linux 发行版的主页。
- `http://www.suse.com`. SuSE Linux 发行版的主页。
- `http://www.linuxppc.com`. 商业 LinuxPPC 2000 发行版的主页。
- `http://www.linuxppc.org`. Linux PPC 移植版的主页。
- `http://www.debian.org`. GNU/Linux 的高僧们的据点，也是 Debian 版 Linux 移植到 PowerPC 的圣地。
- `http://www.vmware.com`. 支持 DOS、Win3.1/9x/32、FreeBSD 和 Linux 的首屈一指的基于 Intel 的模拟器主页。
- `http://www.connectix.com/products/vpc3_advanced.html`. Connectix 的 Virtual PC 3.0 产品页面，详细说明了运行 Red Hat Linux 的方法。
- `http://www.ardi.com/xecutor/`. Ardi 的 Xecutor 客户端主页，该客户端在基于 Intel 的 Linux 下提供 Mac OS 6.0.7 和 7.0 的模拟功能。
- `http://www.xfree86.org`. XFree86 项目公司的主页，其中包含一个 X Window System 移植版的链接，该移植版可以代替或并排运行于 Mac OS X 的图形界面。

# 第 2 章：在 Mac 上安装 Linux

- 初步考虑事项
- 分区
- 安装 Yellow Dog Linux 2.0
- 安装 LinuxPPC 2000 Q4
- 安装 SuSE PPC Linux

![](img/1ea833f5a3e3c1547e3dd2891f52804a_42_0.png)

你准备好迈出这一步了吗？如果是的话，本章将帮助你入门。在 Power Mac 上使用 Linux 和 X Window 系统是一种美妙的体验。到达那里不一定是一个痛苦的过程，但在你到达第一个登录之前，需要采取一些步骤。

本章探讨了关于安装过程的初步考虑事项以及理想的候选安装平台。你将获得一些关于基本要求的初步指导，并了解如何执行在 Mac OS 中很少需要的过程——硬盘分区。最后，你将获得一份安装三种不同 Linux 发行版所需的步骤清单：Yellow Dog Linux、LinuxPPC 2000 和 SuSE PPC Linux。

安装 Linux 并不难，在少量指导下，你可以轻松执行以下基本步骤：

1. 使用系统恢复 CD-ROM 启动你的 Power Mac。
2. 分区你的硬盘。
3. 重新启动并恢复 Mac OS。
4. 重新启动并安装 Linux。
5. 重新启动到 Mac OS 并配置你的引导加载程序。

大多数用户创建一个支持 Mac OS 和 Linux 的双启动系统。如果你计划使用 Mac OS、Mac OS X 和 Linux，你可能希望将每个操作系统安装在自己的分区上。本章仅涵盖 Mac OS 和 Linux 双启动配置的安装。

## 初步考虑事项
