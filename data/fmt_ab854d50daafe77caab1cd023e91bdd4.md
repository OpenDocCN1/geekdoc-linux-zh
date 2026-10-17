
这将用户名和密码设为空，大多数服务器是不接受的。

## 用于其他 Unix 的 SMBFS

`mount -ufs \TSERVER\MOUNT_DIR /mount_point`

`smbfs` 仅适用于 Linux。在 Samba 2.0 中，我们引入了一个名为 `smbfs` 的工具，它将提供类似的功能，并移植到广泛的 Unix 系统。

## SMBSH 与 GLIBC-2.1

`smbsh` 在 Linux 系统上不支持 `glibc-2.1`。这包括 Red-Hat 6.0 以及许多其他最近的 Linux 发行版。修复这个问题非常困难，因为 `glibc` 维护者故意删除了 `smbsh` 工作所需的钩子。他们不喜欢用户空间文件系统的想法。

我们目前唯一的建议是使用 `smbfs` 代替。

# SMB 块大小

早期版本的 `smbtar` 存在一个小错误，导致 `blocksize` 参数无法正常工作。该问题在 Samba 1.9.18 版本中已修复。

# 取消订阅

有关取消订阅或更改已订阅地址的信息，请参阅 http://lists.samba.org/ 上的说明。

# WIN98 运行变慢

- 续我之前的帖子，我有一个有趣的发现。这种特定的缓慢缓慢仅发生在运行 Windows 98 的客户端上。

Windows98 资源管理器（可能还有其他程序）在向网络共享发送写入请求时错误地设置了“sync”（同步）位。由于 Samba（非常正确）在每次写入后都会对文件执行 `fsync()`，这导致了极其缓慢。再加上 Windows98 资源管理器使用的写入大小非常小（约 1.5k），你得到的结果会非常糟糕。

在 Samba 1.9.18p10 及更高版本中，我们修改了 Samba，使其默认忽略错误的同步请求。这使得在使用 Windows 98 资源管理器时性能得到了极大的提升。

你可以使用“strict sync”（严格同步）选项恢复旧的（缓慢的）行为。

# 你的服务器软件不友好

当你尝试使用 `smclient` 连接服务器时，如果收到“your server software is being unfriendly”（你的服务器软件不友好），这意味着 `smclient` 虽然与服务器建立了 TCP 连接，但在打开的套接字上尝试进行 NBT “session request”（会话请求）时返回的是垃圾数据（或为空）。“不友好”位源于客户端期望获得规范（RFC1001/1002）中定义的多个可能错误代码之一，但它收到的是完全不同的内容。

这通常意味着你根本没有成功与 SMB 服务器通信，该套接字连接到了其他地方。对于 Samba 来说，常见原因是 `smbd` 未能正确启动并在到达回答会话请求之前之前退出。损坏/缺失的配置文件会导致这种情况，或者如果你启动了 `inetd`，那么可能是你的 `inetd.conf` 或 `/etc/services` 设置错误。

# 附录 D：Samba 文档

# 附录 D.3 到底什么是 SMB？

作者注：我为原本只有链接的项目添加了网址。除此之外，本文内容与 http://www.samba.org 提供的文档相同。

到底什么是 SMB？

V1.1
Richard Sharpe
1999年4月24日

版权 ©1996,1997,1998,1999 Richard Sharpe

# 复制

请参阅“复制本文文档”章节，了解我关于本文文档使用的政策详细说明。

# 免责声明

本文尝试以某种方式为参与 SMB（即将变为 CIFS）协议的人员提供服务。我们已尽一切确保信息的准确性，但不包含任何保证。Richard Sharpe 对你使用或误用这些信息而导致的任何损失或后果不承担责任。

如果你有任何意见，请发送邮件至 sharpe@ns.aus.com。

# 致谢

我要感谢 Andrew Tridjell，他建议我从 smblib 开始，引导我进入这一领域；感谢 Dan Shear 提供的许多鼓励和信息；感谢 Paul Blackman 帮助制作此页面，以及其他许多未获得许可提及姓名的人。

我还要感谢许多给我发送正面评论和建设性反馈的人士。

# 商标

Microsoft, MS, Windows, Windows 95 和 Windows NT 均为微软公司的注册商标或商标。微软公司不以任何方式认可本文，作者也以任何方式与微软公司关联。

所有其他商标均为其各自所有者的唯一财产。

# 目录

- 引言
- 新功能？
- 什么是 SMB？
- 目前可用的 SMB 客户端和服务器
- SMB 服务器
- SMB 客户端
- 网页上的更多资源
- 复制本文文档

## 引言

本文解释了什么是 SMB 协议，并讨论了目前提供的许多 SMB 客户端和服务器实现。本文档的产生源于我对实现 SMBlib 的兴趣，SMBlib 是一个可移植的 SMB 客户端例程序库。

SMB 是一项重要的协议，因为已经有大量的 PC 运行着客户端和服务器实现程序。所有的 Windows for Workgroups、Windows 95 和 Windows NT 系统都在（或能够）作为客户端、服务器或两者兼运行 SMB。

# 新功能

虽然有很多新事物，但就 SMB 协议而言，可能最感兴趣的是 CIFS，即通用互联网文件系统。

# 什么是 SMB？

SMB 代表 Server Message Block（服务器消息块），是一种用于计算机之间共享文件、打印机、串口端口以及通信抽象（如命名管道和邮件槽）的协议。

我关于 SMB 协议的最早的文档是 1985 年的 IBM 文档。它是 1985 年 5 月 IBM 个人电脑会议论文的副本。它包含了 IBM PC 网络 SMB 协议。我能访问的下一个文档是 1987 年的 Microsoft/Intel NetBIOS-FILE SHARING PROTOCOL。该协议随后由微软和其他人进行了进一步开发。定义 SMB 协议的许多文档可以在 ftp.microsoft.com 的 SMB 文档区域找到。

SMB 是一种客户端-服务器的请求-响应协议。左侧的图表说明了 SMB 的工作方式。SMB 请求-响应性质（即客户端请求，服务器返回响应）的唯一例外是：当客户端请求了机会性锁（oplocks），而由于另一个客户端请求以与已授予的 oplock 不兼容的模式打开文件，服务器必须打破已授予的 oplock。在这种情况下，服务器会向客户端发送一个未请求的消息来信号 oplock 的释放。

服务器为网络上的客户端提供文件系统和其他资源（打印机、邮件槽、命名管道、API）的可用性。客户端计算机可能有自己的硬盘，但它们也想要访问服务器上的共享文件系统和打印机。

客户端使用 TCP/IP（实际上是 RFC1001 和 RFC1002 指定的 NetBIOS over TCP/IP）、NetBEUI 或 IPX/SPX 连接到服务器。一旦建立连接，客户端就可以向服务器发送命令（SMBs），允许它们访问共享、打开文件、读取和写入文件，并通常可以执行你想要对文件系统所做的任何操作。然而，在 SMB 的情况下，这些操作是在网络上完成的。

如前所述，SMB 可以运行在多种协议上。以下图表显示：

SMB 可以运行于 TCP/IP、NetBEUI 和 IPX/SPX。如果使用 TCP/IP 或 NetBEUI，则正在使用 NetBIOS API。

# NetBIOS 名称

如果 SMB 使用在 TCP/IP 或 NetBEUI 上，则在许多情况下必须使用 NetBIOS 名称。NetBIOS 名称长度可达 15 个字符，通常是运行 NetBIOS 的计算机名称。微软和其他其他实现者坚持要求 NetBIOS 名称使用大写，特别是当作为 CALLED NAME 向服务器呈现时。

# SMB 协议变体

自 SMB 诞生以来，开发了许多协议变体，以处理其所采用的日益复杂的环境。

客户端和服务器将使用的实际协议变体是通过 `negprot` SMB 进行协商的，该命令必须是连接上发送的第一个 SMB。

第一个变体是核心协议（SMB 实现中称为 PC NETWORK PROGRAM 1.0）。它可以处理一组相当基础的操作，包括：

- 连接和断开文件和打印共享
- 打开和关闭文件
- 打开和关闭打印文件
- 读取和写入文件
- 创建和删除文件及目录
- 搜索目录
- 获取和设置文件属性
- 锁定和解锁文件字节范围

随着需求的增加，随后引入了变体。其中一些变体以及相关的 LAN Manager 版本包括：

## 278 附录 D：Samba 文

| SMB 协议变体 | 协议名称 | 注释 |
| --- | --- | --- |
| PC NETWORK PROGRAM 1.0 | 核心协议 | IBM PC 网络程序中定义的 SMB 原始版本。某些版本被称为 PCLAN1.0 |
| MICROSOFT NETWORKS 1.03 | 核心+ 协议 | 包含了 Lock&Read 和 Write&Unlock SMB，以及具有不同版本的原始读/写 SMB |
| MICROSOFT NETWORKS 3.0 | DOS LAN Manager 1.0 | 与 LANMAN1.0 相同，但必须将 OS/2 错误转换为 DOS 错误。 |
| LANMAN1.0 | LAN Manager 1.0 | 完整的 LANMAN1.0 协议。 |
| DOS LM1.2X002 | LAN Manager 2.0 | 与 LM1.2X002 相同，但必须将错误转换为 DOS 错误。 |
| LM1.2X002 | LAN Manager 2.0 | 完整的 LANMAN2.0 协议。 |
| DOS LANMAN2.1 | LAN Manager 2.1 | 与 LANMAN2.1 相同，但必须将错误转换为 DOS 错误。 |
| LANMAN2.1 | LAN Manager 2.1 | 完整的 LANMAN2.1 协议。 |
| Windows for Workgroups 3.1a | LAN Manager 2.1? | Windows for Workgroups 1.0? |
| NT LM 0.12 | NT LAN Manager 1.0? | 包含用于 NT 的特殊 SMB |

## 附录 D：Samba 文 279

Samba NT LAN Manager 1.0? Samba 版本的 NT LM 0.12?

CIFS 1.0 NT LAN Manager 1.0 真的只是 NT LM 0.12 加上了一点东西吗？

某些变体引入了新的 SMB，有些仅仅更改了现有 SMB 或响应的格式，而另一些变体则两者兼顾。

**安全** SMB 模型定义了两个级别的安全策略：

- **共享级（Share level）**。保护程序应用于服务器上的共享级别。每个共享都可以设置密码，客户端只需要密码即可访问该共享下的所有文件。这是 SMB 拥有的第一个安全模型，也是 Core 和 CorePlus 协议中唯一的安全模型。Windows for Workgroups 的 vserver.exe 默认实现共享级安全，Windows 95 也是。

- **用户级（User Level）**。保护应用于每个共享中的单个文件，并基于用户访问权限。每个用户（客户端）必须登录服务器并经过服务器验证。验证通过后，客户端将获得一个 UID，在后续对服务器的所有访问中都必须提供该 UID。该模型自 LAN Manager 1.0 起起一直可用。

**网络浏览（Browsing the network）** 如果用户找不到网络中的大量服务器，那将大不方便。当然，客户端可以简单地配置为识别其环境中的服务器，但这在引入新服务器或移除旧服务器时并没有帮助。

为了解决这个问题，引入了浏览功能。每台服务器都会广播其存在的信息。客户端监听这些广播并构建浏览列表。在 NetBEUI 环境中，这是可以的，但在 TCP/IP 环境中会出现问题。TCP/IP 广播通常不会发送到源子网之外（尽管某些路由器可以选择性地将广播传输到其他子网）。

微软引入了浏览服务器和 Windows 命名服务（WINS）来帮助克服这些问题。

**CIFS：最新的化身？** 微软和一组其他供应商（Digital Equipment, Data General, SCO, Network Appliance Corp 等）正在开发 SMB 协议的公开版本。它是

## 280 附录 D：Samba 文

预计 CIFS 1.0 本质上是 NT LM 0.12，并进行了一些修改以便在互联网上更容易使用。

SMB 交换示例 客户端和服务器之间交换的协议元素（请求和响应）被称为 SMB。它们具有特定的格式，请求和响应的格式非常相似。每个元素由一个固定大小的头部部分以及一个变长度的参数和数据部分组成。

在连接到 NetBIOS 级别（通过 NBF、NetBT 等）后，客户端准备好向服务器请求服务了。然而，客户端和服务器必须首先识别它们都理解哪种协议变体。

客户端向服务器发送一个 `negprot` SMB，列出它理解的协议方言。服务器响应它想要使用的方言索引，或者如果其中一种方言是可以接受的则返回 0FFFF。

除了 Core 和 CorePlus 协议之外，方言在 `negprot` 响应中提供信息以指示其能力（最大缓冲区大小、规范文件名等）。

一旦建立了协议。如果需要，客户端就可以继续登录服务器。它们通过一个 `sesset` SMB 执行此操作。响应表明它们是否提供了有效的用户名/密码对，如果是，则可以提供额外信息。响应中最重要的方面之一是已登录用户的 UID。该 UID 必须在连接到服务器的所有后续 SMB 请求中提交。

一旦客户端登录成功（在较旧的协议——Core 和 CorePlus 中——你无法登录），客户端就可以继续连接到树（tree）。

客户端发送一个 `tcon` 或 `tconX` SMB，指定它们想要连接的共享的网络名称，如果一切无误，服务器将返回一个 TID，客户端将在以后所有与该共享相关的 SMB 中使用该 TID。

连接到树后，客户端现在可以使用 SMB 打开文件，然后使用 `read` SMB 进行读取。

## 可用的 SMB 客户端和服务器

今天有几个客户端，服务器较多。

- 来自 Samba 的 Sambaclient
- Linux 的 `smbfs`
- SMBLib（一个开发中的 SMB 库）

服务器实现来自许多：

- 微软的 Samba
- 微软的 Windows for Workgroups 3.x
- 微软的 Windows 95
- 微软的 Windows NT
- Digital 的 LAN Manager for OS/2
- SCO 的 Open Server
- SCO 的 VisionFS
- AT&T 的 Advanced Server for UNIX
- IBM 的 Advanced Server for OS/2

接下来的部分将讨论上述每一个实现。

## SMB 服务器

## 307 附录 D：Samba

工作组（Workgroups）工作组是一组每台机器都维护自身安全信息的计算机。在 Windows for Workgroups 中，每个服务器采用共享级安全。Windows 95 可以将认证传递给 NT 或 LAN Manager 服务器。

然而，工作组的特点是安全是分布式的而不是集中的。

域（Domain）是一个集中安全的计算机集合。每个域有一个多个域控制器。通常有一个主控制器和一个多个备份控制器。域控制器维护与用户（客户端）相关的账户信息，如账户名称、加密密码、授权时间、用户所属组等。

Samba 是一个免费提供的 UNIX、OpenVMS 服务器（集中发布且可能不稳定），由 Andrew Trigdell 开发并由全球的松散小组维护。Samba 运行在许多 UNIX 变体上（Linux, Solaris, SunOS, HP-UX, ULTRIX, DEC OSF/1, Digital UNIX, Dynix (Sequent), IRIX (SGI), SCO Open Server, DG-UNIX, UNIXWARE, AIX, BSDI, NetBDS, NEXTSTEP, A/UX, 等）。

Samba 实现 NT LM 0.12 协议方言。Samba 现在可以参与域（作为 PDC 和域成员），并且可以参与浏览并成为浏览主。Samba 还可以处理 Windows 系统的登录请求。

Samba 实现用户安全，但共享可以是公开的。

## 附录 D：Samba 文档 283

Windows for Workgroups 3.11 实现了 Windows for Workgroups 3.0a 协议变体，并实现了共享级安全。

Windows 95 实现了 NT LM 0.12 协议级别，并同时实现了共享和用户级安全。

Windows NT 实现了 NT LM 0.12 协议级别，并实现了共享用户安全。

LAN Manager 和 LAN Manager for UNIX (LM/X)，微软和 AT&T GIS 将多个 LAN Manager 版本移植到 UNIX 操作系统。这些代码形成了许多供应商提供的适用于 UNIX 操作系统的 SMB 服务器的基础。

示例包括：
- 适用于 SCO 的 LM/X
- 适用于 HP-UX (Advanced Server/9000) 的 LM Server 等

该软件最新版本似乎是 LAN Manager for UNIX Version 2.2，它实现了 LANMAN2.1 协议变体。

VisionFS 是一个由 SCO 从头编写的 SMB 服务器。它适用于 Solaris 2.x、HP-UX 和 SCO（包括 SCO OpenServer 和 UNIXWare）。

TotalNET Advanced Server 该产品来自 Syntax。它是一个完全独立编写的 SMB 服务器，可能是第一个用于 UNIX 的 SMB 服务器。如今，它带有额外的模块，在整个产品中提供 AppleShare 和 NetWare 服务。

Advanced Server for UNIX 在 LM/X 之后，NCR（曾为 ATT GIS）（可能在微软的帮助下）移植了 Windows NT 服务器代码，以提供与 Windows 相同的功能。

PATHWORKS 是数字设备公司（Digital Equipment Corporation）的一个产品系列名称。它包含了服务器和客户端，其中服务器运行在：

- VAX 和 Alpha VMS
- VAX 和 MIPS ULTRIX 
- DEC OSF/1 用于 AXP 和 Digital UNIX (DEC OSF/1 重命名为 OS/2)

## 附录 D：Samba 文档

运行在 DOS、Windows、Windows for Workgroups、Windows NT 和 Windows 95 客户端说明如下。

Digital 的客户端和服务器实现了基于 DECnet 的 SMB，同时也支持 TCP/IP 以及最近的 NetBEUI。SMB over DECnet 规范从未发布过。

Digital 最初用于 VAX/VMS 的 PATHWORKS 服务器实现了 CorePlus 协议（MICROSOFT NETWORKS 1.03 方言）。该产品经历了多个版本，并在版本 4.2 达到顶峰。一段时间后，为 ULTRIX 开发了一个版本，称为 PATHWORKS for ULTRIX V1，其最高版本为 1.3。这两个产品线均为内部开发。

随后，Digital 使用了 AT&T 和微软的 LAN Manager for UNIX (LM/X) 代码。它发布为适用于 OpenVMS 的 PATHWORKS V5.0 (LAN Manager) 和适用于 Digital UNIX 的 PATHWORKS V5.0 (LAN Manager)。后者产品实现了 LAN Manager for UNIX V2.2，其识别的最高 SMB 方言是 LANMAN2.1（以及 DOS LANMAN2.1）。每个产品名称末括号内 LAN Manager 的原因是这些产品也支持 NetWare 功能。

PATHWORKS V5 能够参与基于 Windows NT 的域，尽管仅作为备份域控制器或成员服务器。

最近，Digital 宣布了适用于 UNIX 的 PATHWORKS V6.0 (Advanced Server)，它基于 AT&T 的 ASU (Advanced Server for UNIX) 产品。

## OS/2 的 LAN Server

这是一个 IBM 产品，似乎在某种程度上源自微软的 LAN Manager 代码。

## SMB 客户端

目前有多个 SMB 客户端：

- 微软客户端
  - Windows NT
  - Windows 95
  - Windows for Workgroups 3.11
- Digital 的 PATHWORKS 客户端
- Samba 的 `smbclient`
- Linux 的 `smbfs`
- SMBlib

## 上的上的资源

以下是你可以访问的与 SMB 协议相关的其他网页：

- Samba: http://samba.anu.edu.au/samba
- SMBlib: http://samba.anu.edu.au/samba/smblib
- SCO 的 VisionFS: http://www.sco.com/products/visionfs
- Syntax 的 TotalNET Advanced Server: http://www.syntax.com/totalnet/tasbody2.htm
- Digital 的 PATHWORKS 产品: http://www.digital.com/info/pathworks
- 微软的 Windows NT 产品: http://www.microsoft.com/NTSServer
- IBM 的 LAN Server 产品: http://www.austin.ibm.com/pspspinfo/lsinfo.html
- IBM 与 AIX 的集成: http://www.austin.ibm.com/resource/technology/aixpcint.
- Data General 对 Advanced Server for UNIX 的支持: http://www.dg.com/products/html/dg_ux.html
- `smbfs`: http://www.boutell.com/lsmbyid.cgi/000948 LSM entry (以及 `smbfs` ftp http://ftp.gwdg.de/pub/linux/smbfs location)
- CIFS 主页: http://www.microsoft.com/intdev/cifs
- Network Appliance 对 CIFS 的支持: http://www.netapp.com/news/level3b/news_rel_960613.html
- HP 在企业级 HP-UX 平台上出货 NT Server 网络操作系统: http://www.hp.com/pressrel/apr96/08apr96d.htm
- AT&T GIS 宣布 Advanced Server

## 290 附录 E: Samba 手页

查看 `samba (7)` 以获取贡献者完整列表以及提交错误报告、注释等的详细信息。

## 附录 E.2 NMBD

# NMBD

# SAMBA

1998年10月23日

# 名称

`nmbd`—NetBIOS 名称服务器，为客户端提供基于 IP 的 NetBIOS 命名服务

# 概要

```
nmbd [-D] [-o] [-a] [-H Imhosts file] [-d debuglevel] [-l log filename] [-n primary NetBIOS name] [-p port number] [-s configuration file] [-i NetBIOS scope] [-h]
```

# 描述

此程序是 Samba 套件的一部分。

`nmbd` 是一个能够理解并响应基于 IP 的 NetBIOS 名称服务的服务器，例如由 Windows 95/98、Windows NT 和 LanManager 客户端等 SMBD/CIFS 客户端产生的请求。它还参与组成 Windows “网络邻域”视图的浏览协议。

SMB/CIFS 客户端在启动时可能希望定位 SMB/CIFS 服务器。也就是说，它们想要知道特定主机正在使用哪个 IP 号。

在其他服务中，`nmbd` 会监听此类请求，如果指定了它自己的 NetBIOS 名称，它将响应其所运行主机的 IP 号。它的“自己的 NetBIOS 名称”默认是其所运行主机的主 DNS 名称，但可以通过 `-n` 选项对其进行覆盖（见下文“选项”部分）。因此，`nmbd` 将响应对其自身名称（们）的广播查询。可以通过 `smb.conf(5)` 配置文件中的参数设置 `nmbd` 响应的额外名称。

`nmbd` 还可以用作 WINS（Windows 网上命名服务器）服务器。这基本上意味着它将作为一个 WINS 数据库服务器工作，从接收到的名称注册请求创建数据库，并响应客户端对这些名称的查询。

此外，`nmbd` 可以充当 WINS 代理，将不理解如何使用 WINS 协议的客户端的广播查询中继到 WIN 服务器。

# 选项

- `-D`: 如果指定，此参数使 `nmbd` 以守护进程运行。它会脱离并在后台运行，在适当的端口上处理请求。默认情况下，`nmbd` **不会**作为守护进程运行。`nmbd` 也可以由 `inetd` 元守护进程操作，尽管不建议这样做。
- `-a`: 如果指定此参数，每个新连接都将日志消息追加到日志文件中。这是默认。
- `-o`: 如果指定此参数，日志文件在打开时将被覆盖。默认情况下，日志文件将会被追加。
- `-H filename`: NetBIOS 主机

`hosts` 文件是一个从 NetBIOS 名称到 IP 地址的列表，由 `nmbd` 服务器加载，并通过 `smb.conf (5)` 中描述的名称解析顺序解析机制来解析服务器所需的任何 NetBIOS 查询。请注意，该文件的内容**不会**被 `nmbd` 用于回答任何名称查询。在此文件中添加行**仅**会影响从此主机的 NetBIOS 名称解析。

该文件的默认路径作为构建过程的一部分被编译到 Samba 中。常见的默认路径有 `/usr/local/samba/lib/lmhosts`、`/usr/samba/lib/lmhosts` 或 `/etc/lmhosts`。有关此文件内容的详情请参 `lmhosts (5)` 页。
- `-d debuglevel`: `debuglevel` 是一个 0 到 10 的整数。

如果未指定此参数，默认值为零。

值越高，日志文件中关于服务器活动的详细信息就越多。在级别 0 下，仅会记录严重错误和严重的警告。级别 1 是日常运行的合理级别——它会生成有关执行操作的少量信息。

1 以上的级别将产生大量的日志数据，应仅在调查问题时使用。3 以上的级别仅供开发者使用，并产生海量的日志数据，其中大部分内容极其晦涩。

请注意，在此处指定此参数将覆盖 **`smb.conf (S)`** 文件中的日志级别参数。

- `-l logfile`: `-l` 参数指定一个路径和基本文件名，运行中的 `nmbd` 服务器的操作数据将记录到该文件中。实际的日志文件名通过在指定的基名称后添加扩展名 ".nmb" 生成。例如，如果指定的名称为“log”，则 `log.nmb` 文件将包含调试数据。

默认日志文件路径作为构建过程的一部分被编译到 Samba 中。常见的默认路径有 `/usr/local/samba/var/log.nmb`、`/usr/samba/var/log.nmb` 或 `/var/log/log.nmb`。

- `-n NetBIOS name`: 此选项允许你覆盖 Samba 自身使用的 NetBIOS 名称。这相当于在 **`smb.conf`** 文件中设置 NetBIOS 名称参数，但它会覆盖 **`smb.conf`** 文件中的设置。

- `-p UDP port number`: UDP 端口号是一个正整数。

此选项更改 `nmbd` 响应名称查询的默认 UDP 端口号（通常为 137）。除非你是专家，否则不要使用此选项，如果是的话我们就不提供帮助！

- `-s configuration file`: 默认配置文件文件名在构建时设置，通常为 `/usr/local/samba/smb.conf`。详情请参见 `smb.conf (5)`。

- `-i NetBIOS scope`: 这指定 `nmbd` 将使用的 NetBIOS 范围。有关范围的详情，请参见 **`smb.conf (5)`**。

- `-h`: 打印帮助信息（用法）。

# 文件

# /ETC/INETD

如果服务器由 `inetd` 运行，此文件必须包含适当的初始化。

# /ETC/RC

如果作为守护进程运行服务器，此文件需要适当的序列。

# /USR/LOCAL/SAMBA/LIB/SMB.CONF

这是 `smb.conf` 的默认位置。其他常见的安装位置有 `/usr/local/samba/smb.conf` 和 `/etc/smb.conf`。

当作为 WINS 服务器运行时（参见 `smb.conf (5)` 手页中的 `wins` 参数），`nmbd` 将 WINS 数据库存储在 `wins.dat` 文件。

如果 `nmbd` 充当浏览主（参见 `smb.conf` 中的 `local master` 参数），`nmbd` 将浏览数据库存储在 `browse.dat` 文件。

# 信号

关闭 `nmbd` 进程建议**不要**使用 SIGKILL (-9)，除非是最后的手段，因为这可能导致名称数据库处于不一致状态。终止 `nmbd` 的正确方法是向它发送 SIGTERM (-15) 并等待它自行退出。

`nmbd` 会接受 SIGHUP，这将导致它将名称列表导出 `namelist.debug` 文件。此外，可以通过发送 SIGUSR1 (`kill -USR1 <nmbd-pid>`) 提高 `nmbd` 的调试级别，通过发送 SIGUSR2 (`kill -USR2 <nmbd-pid>`) 降低级别。这允许在正常日志级别运行时诊断问题。

## 附录 E: Samba 手册

## 说明

Samba 软件套件是一个实现了 UNIX 系统服务器消息块（通常缩写为 SMB）的程序集合。该协议有时被称为通用 Internet 文件系统 (CIFS)、LanManager 或 NetBIOS 协议。

## 组件

Samba 套件由多个组件组成。每个组件在单独的手册页中描述。强烈建议你阅读 Samba 自带的文档以及你所使用的组件的手册页。如果手册页不够清晰，请向 `samba-bugs@samba.org` 发送补丁或错误报告。

- `smbd`
- `smbd (8)` 守护进程为 SMB 客户端提供文件和打印服务，例如 Windows 95/98、Windows NT、Windows 工作组或 LanManager。该守护进程的配置文件在 `smb.conf (5)` 中描述。
- `nmbd`
- `nmbd (8)` 守护进程提供 NetBIOS 名称服务器和浏览支持。该守护进程的配置文件在 `smb.conf (5)` 中描述。
- `smbclient`
- `smbclient (1)` 程序实现了一个类似 ftp 的客户端。这对于访问其他兼容服务器（如 Windows NT）上的 SMB 共享非常有用，也可以用于允许 UNIX 终端打印到连接到任何 SMB 服务器（如运行 Windows NT 的 PC）的打印机。
- `testparam`
- `testparam (1)` 工具允许你测试你的 `smb.conf (5)` 配置文件。
- `testprns`
- `testprns (1)` 工具允许你测试你的 `printcap` 文件中定义的打印机。
- `smbdystatus`
- `smbdystatus (1)` 工具允许你列出到 `smbd (8)` 服务器的当前连接。
- `nmlookup`
- `nmlookup (1)` 工具允许从 UNIX 机器进行 NetBIOS 名称查询。
- `make_smbcodepage`
- `make_smbcodepage (1)` 工具允许你为你的 `smbd (8)` 服务器创建 SMB 代码页定义文件。
- `smbpasswd`
- `smbpasswd (8)` 工具允许你更改 Samba 和 Windows NT(tm) 服务器上的 SMB 加密密码。

## 可用性

Samba 软件套件根据 GNU 公共许可 (GPL)get。软件包中的 COPYING 文件应包含该许可协议的副本。我们鼓励你分发 Samba 套件的副本，但请遵守此许可的条款。

可以通过从 `samba.org` 的 `pub/samba/` 目录通过匿名 ftp 获取最新版本的 Samba 套件。它在世界各几个镜像站点上也可用。

你还可以在新闻组 `comp.protocols.smb` 和 Samba 邮件列表找到有关 Samba 的有用信息。有关如何加入邮件列表的详情请参见 Samba 自带的 README 文件。

如果你可以访问 WWW 浏览器（如 Netscape 或 Mosaic），那么你还可以在 http://samba.org/samba/ 找到大量信息，包括 Samba 邮件列表的历史期存档。

## 版本

本手册页适用于 Samba 套件的 2.0 版本。

## 贡献

如果你想为 Samba 项目做出贡献，我建议你加入 `samba@samba.org` 的 Samba 邮件列表。访问网页 http://samba.org/listproc 了解有关如何操作的详情。

如果你有补丁要提交或错误要报告，可以直接邮寄到 `samba-bugs@samba.org`。但请注意，由于该软件包极其受欢迎，Samba 团队可能需要一些时间来回复邮件。我们倾向于使用 `diff -u` 格式的补丁。

## 鸣谢

项目的贡献者现在多到无法在此列出，但他们值得所有 Samba 用户的感谢。查看完整列表，请访问 http://samba.org/pub/samba/alpha/change-log 查看预-CVS 更改，访问 ftp://samba.org/pub/samba/alpha/cv.log 查看 Samba-CVS 的贡献者。CVS 是 Samba 团队开发 Samba 使用的开源代码控制系统。没有它，项目将无法管理。

此外，几个商业机构现在通过资金和设备为 Samba 团队提供支持。详情请见 http://samba.org/samba/samba-thanks.html 上的 Samba 网页。

## 作者

原始 Samba 软件和相关工具由 Andrew Tridgell (`samba-bugs@samba.org`) 创建。Samba 现在由 Samba 团队作为一个开源项目开发，类似于 Linux 内核的开发方式。

原始 Samba 手册页由 Karl Auer 编写。手册页源码转换为 YODL（另一项优秀的开源软件，可在 ftp://fpt.icce.rug/pub/unix/ 获取），并由 Jeremy Allison (`samba-bugs@samba.org`) 为 Samba 2.0 发布进行了更新。

## 附录 E.4 SMB.CONF

```
