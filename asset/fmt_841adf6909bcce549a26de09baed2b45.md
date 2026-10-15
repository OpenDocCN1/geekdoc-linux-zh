
# 额外章节

如果你能用位掩码（`bitmasks`）思维来思考，就可以从列表中咨询相应的内核头文件。个人而言，我通常认为 NFS 客户端和 NFS 服务器的输出最有用，并且通常从值 `1023` 开始，因为这可以激活每个服务最有用的调试功能，而不会真的变得无所完备。我经常在服务器上测试客户端和服务器：首先启动服务器，然后尝试在同一台主机的某处挂载其导出的目录之一。一旦本地运行正常，你就可以尝试让它们从远程客户端运行。

# 获取更多关于 NFS 的信息

并不意外，网络提供了许多关于 NFS 额外信息的优秀来源。要获取更多信息，请参考以下任意：

- [NFS FAQ](http://nfs.sourceforge.net)
- [NFS HOWTO](http://nfs.sourceforge.net/nfs-howto)
- [Ubuntu上的 NFS4](http://help.ubuntu.com/community/NFS4Howto)

### 总结

本章介绍了 NFS，即网络文件系统（Network File System），它是类 Unix 系统通过网络共享目录的事实标准。NFS 简单、轻量且快速——而且自 20 世纪 80 年代中期以来，几乎任何类 Unix 系统都有免费的实现。在介绍了一些背景之后，本章解释了如何在你的 Ubuntu 桌面、服务器或 Ubuntu 系统上安装和配置 NFS 服务器。

尽管存在 Microsoft Windows 系统的 NFS 实现，但它们大多数都是付费的，而且对于由运行 Linux、Mac OS 和 Microsoft Windows 的系统组成的异构网络用户来说，它们并不是开箱即用的替代方案。Mac OS 系统凭借其 Mach 和 BSD 基础，原生支持 NFS。有趣的是，所有类型系统之间共享文件的最“标准”方式是使用名为 Samba 的包，它允许 Ubuntu 和其他类 Unix 系统通过 Microsoft Windows 系统使用的专用服务器消息块（SMB）协议（Samba 的名称也源于此）在网络上共享目录和文件系统。第 14 章解释了如何快速方便地设置 Samba，以便你家庭网络中的每个人无论运行什么操作系统，都可以访问存储在你的 Ubuntu 和 Kubuntu 系统上的文件，并且（当然）是免费的。

# 额外章节 14

## 设置 Samba 服务器

无论你喜不不喜欢，地球上充斥着 Windows 机器。正如你所看到的那些言论，在涉及到 Windows 与 Linux 时，我可能比任何人都更倾向于传播那种“我们对他们”的心态。我个人觉得 Windows 和微软其实并不重要——例如双向自动打印机共享等功能，使得集成 Linux 和 Windows 文件系统变得简单。

如果你在过去的五年左右一直住在山洞里，可能没听说过 Samba，这无疑是为 Linux 和类 Unix 系统编写的最广流行的应用程序之一。简而言之，Samba 是一组应用程序，最初用于在 Linux 系统上支持微软的网络协议，现在已被移植到几乎所有其他具有网络能力的操作系统。

有大量的书籍专门讨论 Samba，解释了其配置文件、安装和使用的每一个细微差别。我在本章的目标不是在另一本关于 Ubuntu 的书中再塞进一个章节，而是提供一些关于 Windows 网络化和 Samba 的有趣背景信息，然后解释如何使用 Samba 在你的 Ubuntu 系统上共享目录和打印机，以便你家庭、学术或商业环境中的 Microsoft Windows 用户可以访问它们。

### 本章内容

- 安装 Samba 服务器
- 与 Windows 系统共享目录
- 与 Windows 系统共享打印机

## Microsoft Windows 文件共享概述

网络及路由等相关技术产生的缩写可能比计算机行业任何其他方面都多。MS-DOS 和 Microsoft Windows 网络贡献了自己的力量，这很大程度上是因为这些系统在现代计算环境中的使用。由于 DOS 系统（过去）和 Windows 系统（现在）的流行，如今的 Windows 系统为所有网络协议提供了支持。坦率地说，Windows 在保持与几乎每个 DOS 应用程序和网络协议向后兼容的同时，取得了令人赞叹的进展。Windows 支持 Novell 用于提供第一批 PC 服务器时使用的互联网数据包交换（IPX）和顺序数据包交换（SPX）网络协议。此外，与此相关的还有由微软开发的网络协议和缩写，它们可以在不需要任何第三方参与的情况下，在 PC 网络上提供文件和资源共享，非常感谢。

PC 的基本输入输出系统（Basic Input and Output System）对本地设备而言最好的名称是 PC 的 BIOS。随着网络开始运行，微软扩展了 BIOS 的功能以支持通过网络访问和共享信息。使用 BIOS 协议（或其更广为人知的 NetBIOS），BIOS 提供支持系统输入输出的基本功能，而 NetBIOS 提供使用和管理网络的基本功能。NetBIOS 命令和功能必须在网络化系统之间交换，并需要底层的网络传输机制将数据包从一个移动到另一个。如今在 PC 网络中仍然常见的底层协议是 IPX、NetBEUI（网络基础扩展接口）和 TCP/IP（传输控制协议/网络协议）。有趣的是，IPX 和 TCP/IP 全称中的“Internet”指的是网与网之间的通信（inter-network communications），而不是我们所知的互联网。

现代 Windows 系统通过使用 TCP/IP 作为传输协议来使用 NetBIOS。在 NetBIOS 层之上，Windows 为网络服务提供了一个更高级的接口，例如服务器消息块（SMB）协议，这是一种可以被应用程序使用的网络协议。SMB 是一种面向连接的协议，而不是广播协议，它依赖于与特定的网络服务建立连接。一旦建立连接，SMB 提供四种基本类型的功能：

- 会话功能：用于在机器之间协商并建立连接（通常称为虚拟电路）、身份验证，并验证每个伙伴对对方拥有的权限。
- 文件功能：允许应用程序打开、读取和写入远程文件、共享目录等。
- 打印机功能：允许应用程序将输出流化到远程设备。
- 消息功能：允许应用程序在网络上的不同系统之间发送和接收控制、状态和信息消息。

SMB 在 20 世纪 90 年代初成为网络互性的 Open Group 标准。Samba 的名字来自 SMB，这两个元音使其易于识别，并且比 YAA（Yet Another Acronym，又一个缩写）听起来稍微柔和。

在最近的发展中，微软将一种 SMB 协议的增强版本 CIFS（通用互联网文件系统）提交给了 IETF（互联网工程任务组），IETF 是一个对互联网通信架构和互联网顺利运行感兴趣的人组成的协会。CIFS 已被提议作为一个标准，通过将其关注点扩展到使用共享资源来扩展 SMB 的功能。

# 设置 Samba 服务器

# 介绍 Samba

说白了，Samba 更多用于为 Windows 用户提供对 Linux 的透明访问，这是最令人印象深刻的软件之一。对于任何 Windows 系统来说，由 Andrew Tridge 最初编写的 Samba 是为 Linux 和类 Unix 系统编写的最流行的应用程序之一。Samba 包含了客户端和服务器软件——换句话说，允许用户从 Linux 连接到 SMB 主机的客户端软件，以及为你的 Linux 提供 SMB 接口的服务器软件。使用 Samba 客户端将在书中讨论。本章重点介绍如何安装和设置 Samba 服务器。

一个 Samba 服务器由两个进程组成，它们都可以从命令行启动或自动集成到系统启动中。分别是 `smbd`（为 Windows客户端提供文件共享和打印服务的 Samba 守护进程）和 `nmbd`（将 NETBIOS 名称映射到 IP 地址）。Samba 守护进程允许配置其 `/etc/samba.conf`。在 Ubuntu 和 Ubuntu 系统上，配置你想通过 Samba 出的特定目录的最简单、标准的方法是手动修改 Samba 配置，稍将在“Samba 服务器基础”部分讨论。

Linux 和 Windows 系统之间的互操作性不仅仅需要 Samba。Linux 内核提供了访问 Windows 文件系统的内置支持，允许 Linux 用户通过 `/etc/fstab` 挂载 Windows 文件系统，就像其他任何文件系统一样。

> Ubuntu 仓库提供了当前的 Samba 版本以及下一个版本 Samba（Samba 3.x）的软件包，本章关注当前的 Samba 版本（Samba 3.x），因为它是完全稳定的。尽管 Samba 4 将带来性能、功能和灵活性，但它目前还没有准备好。请关注！

# 安装 Samba 服务器及朋友们

Samba 客户端包在 Ubuntu 和 Ubuntu 桌面系统上默认安装，使得任何 Ubuntu 或 Kubuntu 系统都能轻松连接并访问来自 Microsoft Windows 系统或 Samba 服务器的 SMB/CIFS 共享目录。要安装运行和监控 Samba 服务器所需的软件包以便从你的 Ubuntu 或 Kubuntu 系统共享目录，你必须安装

# 第四部分 附录

请使用你喜欢的包管理工具：Synaptic、Adept、`aptitude` 或 `apt-get`。有关安装这些包管理工具的详细信息，请参阅第 23 章。

在安装 `samba` 软件包时，你可能还想安装 `samba-doc` 和 `samba-doc-pdf` 软件包，它们分别提供了官方 Samba 文档的 HTML 和 PDF 版本，以及一本由 Samba 项目负责人之一 John Terpshtra 编写的名为 *Samba 3 By Example* 的在线书籍。

# Samba 服务器配置基础

虽然存在用于配置 Samba 的图形化工具，但它们在 Ubuntu 和 Kubuntu 系统上处于变化状态。之前的 Ubuntu 版本包含一个“共享文件夹”（Shared Folder），允许你识别想要通过 NFS 或 Samba 导出的 Linux 目录，但这已不再是 Ubuntu 的一部分。一个名为 `system-config-samba` 的程序最初为 Red Hat Linux 发行版开发，适用于 Ubuntu 系统，但它无法提供你在大多数情况下想要使用的所有配置选项。因此，除非你安装了窗口管理器或桌面环境，否则你无法使用它来配置 Samba 服务器。同样，基于 KDE 的系统（如 Kubuntu）曾提供 KDE 控制中心，但它尚未更新到新的“设置”（System Settings）框架。因此，本章将重点介绍如何在原生的 Linux 环境中通过配置文件配置 Samba 服务器——即使用文本编辑器编辑配置文件。Samba 的配置文件是 `/etc/samba/smb.conf`。该配置文件包含许多有用的注释，即以井号（`#`）为开头的行。它还包含许多未激活的命令，你可以通过删除开头的分号来激活它们。

正如你将在后续章节中看到的，编辑 `/etc/samba/smb.conf` 来配置 Samba 其实非常简单，但与 Ubuntu Linux 的其他系统管理工作相比，有些不方便。

> 注意
基于 Web 的系统管理工具，如 `swat`（Samba Web 管理工具）和 `webmin`（一个更通用的 Web 管理环境）可以从 Ubuntu 仓库获取，但在你配置的系统中使其正常工作之前，需要进行特殊配置。

接下来的章节将关注 Samba 配置文件中你可能需要在 Samba 环境中更新的特定条目，而不是讨论整个 Samba 文件。在官方 Samba 文档、`samba-doc` 和 `samba-doc-pdf` 软件包提供的在线文档以及许多关于 Samba 的书籍中，关于 Samba 每个细微之处的详细信息并不缺少——本章的其余部分专注于如何尽可能快速、方便地让一切运行。

# 识别你的工作组或域

Samba 配置文件分为几个部分，每个部分由方括号括起的部分名称标识。与你的 Samba 服务器网络身份以及你如何对其进行身份验证相关的条目位于 Samba 配置文件 `/etc/samba/smb.conf` 的 `[global]` 部分。

# 设置 Samba 服务器

必须设置以定义 Ubuntu 服务器如何与 Windows 系统交互的条目是 `workgroup`（工作组），它标识了 Samba 服务器所属的工作组或 Windows 域。我的示例系统中该条目看起来如下：
