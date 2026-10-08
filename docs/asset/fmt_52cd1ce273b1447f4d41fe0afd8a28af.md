
- 扩展线程函数，提升了多处理器硬件性能和应用吞吐量
- 与最新的 POSIX 标准对齐

单 UNIX 规范第二版包含 1,434 个编程接口，而原始单 UNIX 规范有 1,170 个。

# UNIX 98

开放小组将 UNIX 98 指定为符合单 UNIX 规范第二版本的系统标志。UNIX 98 是一系列针对不同类型计算机的标准，如基础系统、工作站和服务器：

- UNIX 98 工作站，基础产品标准以及通用桌面环境
- UNIX 98 服务器，基础产品标准以及互联网协议族、Java 软件和支持网络计算的能力

UNIX 98 服务器设计用于满足高可靠互联网应用程序的需求。HP、IBM、Micros 和富士胶拥有 UNIX 98 注册产品。

基础规范（Base Specifications）的修订目标是尽可能减少对符合早期版本标准的现有实现所需的修改，使其符合新标准。

除了基础规范，《单一 UNIX 规范第三版》（Single UNIX Specification, Version 3）包含了更新后的 X/Open Curses 规范。

# UNIX 03

UNIX 98 产品标准已得到增强，产生了 UNIX 03 产品标准。最重要的增强是与《单一 UNIX 规范第三版》保持一致，包括了新版本的《Open Group 基础规范》（与 IEEE Std 1003.1-2001 和 ISO/IEC 9945:2002 相同）。

在 UNIX 98 产品标准之外的强制增强包括接口与 ISO 9899:1999（涉及 C 语言）的对齐以及为了该对齐而新增的新功能；根据最新版本的 XNS 和 IEEE Standard 1003.1g-2000 添加了新的网络功能；以及对核心 POSIX 系统接口和工具的添加和修正。这些添加和修正源自 P1003.1 和 P1003.2 标准。

UNIX 03 产品标准中包含的可选增强包括支持 Internet Protocol 6 (`IPv6`) 的网络功能、用于实时支持的额外 API 集合，以及源自 IEEE Standard 1003.2d-1994 的批处理工具（Batch Utilities）扩展。

IBM 和 Sun 都有通过 UNIX 03 产品标准认证的产品。

# 流行的 UNIX 变体

如前所述，并没有单一的操作系统。相反，是一个巨大的 UNIX 变体集合。所有这些变体共享许多特征。此外，在这些流行的变体之间迁移软件相对简单。这些变体之间的许多差异对用户是隐藏的，其他差异则源于这些变体的演进方式。最显著的差异在于插件，这些插件使得特定的 UNIX 变体适用于特定的目的和任务。

我们将简要描述不同 UNIX 变体共享的一些共同特征，后续章节也将讨论它们之间的一些差异。它们还将介绍一些最常用的 UNIX 变体的特定方面，包括 Linux、Solaris、HP-UX、Mac OS X 和 AIX。

# Linux

Linux 是 UNIX 系统一个极其流行的变体。其受欢迎的原因之一是它可以免费使用，此外其能力的深度和广度，以及由于大型 Linux 开发社区的专业知识和奉献而在 Linux 上运行量软件。这种普及也有助于许多商业计算机公司（包括 IBM、HP、Sun 和 Novell）对 Linux 的支持。Linux 受 GNU 通用公共许可证（GNU General Public License）条款保护，这防止人们在不允许买者自由复制和分发的情况下销售它。Linux 内核可以在网上数百个 FTP 站点获取。Linux 现在适用于许多处理器，包括 Intel x86 家族、Motorola 68k、Sparc 和 Power PC。

今天，Linux 广泛应用于桌面和服务器、家庭、小型企业和企业。尽管 Linux 不符合 POSIX.1 标准，但有许多不同的发行版表现出高度的 POSIX 兼容性。开发者目标是使其尽可能符合 Open Group 的标准。Linux 共享 UNIX System V 的许多特征和增强。它成为了个人计算机上广流行的 UNIX 版本。多个桌面环境（包括 GNOME 和 KDE）运行在 Linux 上，使得用户如果需要使用 Windows PC，就可以轻松使用 Linux。此外，Linux 的应用程序软件随处可用。在过去的五年里，它已被广泛用于服务器应用程序，现在大量运行在网页邮件、文件服务器和防火墙上。

要开始使用 Linux，你需要获取 Linux 发行版。（你也可以购买预配置了 Linux 发行版的 PC。）Linux 发行版包含 Linux 内核、一组运行在 Linux 上的程序和应用程序，以及一个安装程序。Linux 发行版可以从商业供应商、非营利组织、团队和个人处获得。只要不限制软件的重新发行，就可以销售 Linux 发行版。有许多不同的 Linux 发行版（计数列表超过 450 个——http://en.wikipedia.org/wiki/List_of_distributions）。某些发行版是用于桌面或服务器的通用型，设计用于从嵌入式系统到实时计算特定特定。大多数人将 Linux 视为一个单一的操作系统，但每个发行版实际上都是一个独立的操作系统。UNIX 有许多不同的变体。

流行的通用型 Linux 发行版（可以通过互联网下载或在 CD-ROM 上获得）来自 Red Hat（http://www.redhat.com/）、Caldera（由 SCO Group 所有）（http://www.caldera.com/）、Debian（http://www.debian.org/）、SuSE（由 Novell 所有）（http://www.novell.com/linux/suse/）、Mandriva（http://www.mandriva.com/）、TurboLinux（http://www.turbolinux.org/）和 Slackware（http://www.slackware.org/）。有时，Linux 发行版供应商通过下载提供其发行版的免费版本，并通过介质和支持销售发行版。Linux 发行版在许多方面不同，包括 Linux 内核的版本、它们包含的程序以及安装程序。许多 Linux 发行版包含的应用程序包括 浏览器、Apache Web 服务器、安全工具以及如 Open Office（一套办公套件）之类的办公应用程序。由于[图像裁剪]

# BSD 变体：FreeBSD、NetBSD 和 OpenBSD

伯克利软件发行（Berkeley Software Distribution）一直是几个 UNIX 变体的基础，包括 FreeBSD、NetBSD 和 OpenBSD。调查显示，在变体用户中，FreeBSD 使用最多，其次是 OpenBSD，然后是 NetBSD。

## FreeBSD

FreeBSD 1.0 于 1993 年引入。最初基于 4.3BSD。FreeBSD 2.0 于 1994 年发布，基于 4.4BSD。FreeBSD 5.0 于 2003 年初发布。FreeBSD 5 引入了多处理器（SMP）支持。FreeBSD 6.0 于 2005 年底发布，7-CURRENT 正在开发中。这些版本继续在 SMP 和线程优化方面工作，并在安全方面进行了额外工作。

FreeBSD 提供了一种易于安装移植软件的方法，称为端口集合（Ports Collection）。使用端口集合可以使用 `make` 命令安装软件，几乎不需要额外工作。特别是大多数应用程序从网上下载，根据需要进行补丁和配置、编译、安装并在包数据库中注册。目前端口集合中有 14000 软件包。FreeBSD 还提供了 Linux 的二进制兼容性，使得 FreeBSD 用户可以运行仅以二进制形式分发的 Linux 应用程序。

更多 FreeBSD 信息请访问 http://www.freebsd.org/。

## NetBSD

NetBSD 生于 1993 年；其多平台版本 NetBSD 1.0 于 1994 年引入。NetBSD 取代了基于 4.3BSD-lite 的源代码，使其无限制发行。NetBSD 以设计和实现的质量著称。它是使用 4.3BSD/NET 2 和 386BSD 作为基础开发的。NetBSD 的名称来源于互联网在其开发方式中的重要。

NetBSD 以其可移植性以及这种移植性的易用性著称。为了强调这一点，NetBSD 的格号是“它当然运行 NetBSD”。在 1998 年，NetBSD 1.3 引入了包集合（pkgsrc），它提供了所需的更改，使得大量免费软件可以在 NetBSD 上运行。NetBSD 2.0 于 2004 年发布。随着该版本的发布，NetBSD 引入了对称

# 第1章：背景 21

针对多种 CPU 架构的多处理器处理（SMP）以及原生线程实现。在 2.0 版本发布时，支持了大约 50 个不同的平台。

当前的发行版本 NetBSD 3.0 于 2005 年底发布。NetBSD 3.0 支持 Xen 虚拟机监视器，这使得 NetBSD 能够以高水平的性能和资源隔离支持多个客机操作系统的运行。由于 NetBSD 的可移植性，人们一直说 NetBSD 除了可能的厨房烤面包机之外，可以移植到任何类型的机器上。随着这个新版本的发布，NetBSD 现在可以通过将操作系统移植到可用于烤面包机空隙的嵌入式系统板计算机上来控制烤面包机。`pkgsrc` 现在已支持 5,700 个第三方软件包。

NetBSD 还提供了与 Linux、FreeBSD、Darwin、Solaris、HP-UX、Solaris 和 UniWare 的系统级二进制兼容。这使得 NetBSD 用户能够运行许多仅以二进制形式分发的其他 UNIX 变体的应用程序。

如需更多关于 NetBSD 的信息，请访问 http://www.NetBSD.org/。

## OpenBSD

OpenBSD 由其创始人 Theo De Raadt 于 1994 年从 NetBSD 中拆分出来。OpenBSD 的初始版本发布于 1996 年。该项目每六个月发布一个新版本，维护并支持一年。它以对安全的强支持而闻名，提供了其他 UNIX 变体中未发现的安全功能和能力。OpenBSD 完全基于源代码并可以在免费限制下获得许可。OpenBSD 的开发者付出了额外努力，对源代码进行漏洞和安全问题审计。与其他基于 BSD 的 UNIX 变体一样，OpenBSD 的内核和用户程序是在单个源码仓库中共同开发的。

最新版本是 OpenBSD 3.8，于 2005 年底发布。OpenBSD 目前运行在 16 种不同的硬件平台上。第三方软件以二进制包的形式提供，或者可以使用其端口集合（ports）从源码编译。

如需更多关于 OpenBSD 的信息，请访问 http://www.openbsd.org/

## Solaris

Microsystems 的原始操作系统是 SunOS。它基于 UNIX System V Release 2 和 4.BSD。1991 年，Microsystems 将 SunSoft 设为一个独立的子公司，负责软件（包括操作系统）的开发和营销。在成立之初，Sun 开始从 SunOS 迁移到基于 SVR4 的新 UNIX 版本。Sun 的第一个 UNIX 版本 Solaris 1.0 拥有增强版的 SunOS。

随着 Solaris 2.0 的推出，SunSoft 了基于 SVR4 的操作系统。尽管 2.0 是 Solaris 的第一个“官方”版本，但由于其支持的工作站数量有限，它并没有被广泛使用。第一个运行在所有基于 SPARC 的和基于 x86 的工作站上的版本是 Solaris 2.1，它于 1992 年底发布。

下一个重大版本是 Solaris 2.3，于 1993 年 11 月发布，它为 Solaris 环境引入了许多变化，包括最新版本的 X Window 系统，并开始在某些图形系统中使用 Display PostScript。Solaris 2.3 同样符合 POSIX 标准。Solaris 2.4 于 1994 年发布；包含了 Motif。Solaris 2.5 于 1995 年发布，包含了许多新功能，如通用桌面环境（CDE）、POSIX 线程和基于 TCP 的 NFS。

Solaris 2.6 是第一个支持 Java 的 Solaris 版本，于 1997 年发布。Solaris 2.6 还符合 X/OPEN 的 UNIX95 标准，并包含了 Y2K 修复。

Solaris 7（弃用了数字 2，直接称为 7）于 1998 年发布；它包含了许多提高可用性和可靠性的新功能。其中一些改进针对 64 位应用程序以及基于 Web 的管理和配置。

Solaris 8 于 2000 年引入。它包含了许多性能和管理增强，集成了一个用于提供网页服务的网络缓存加速器、支持进程聚类、用于重新分配资源的自动重新配置、热补丁（hot-patching）能力、操作系统的即时更新（live updating）以及集中化管理功能。它还提供了安全增强，包括内置防火墙、对 Kerberos 支持、基于角色的访问控制以及对 IPsec（IP 安全）的支持，后者实现了互联网上经过验证的连接。它引入了对 IP 6 的支持，并集成到其 NFS/RPC（网络文件系统/远程调用）和 NIS/NIS（网络信息服务）中。Solaris 8 还包含 StarOffice 5，它提供了文字处理器、电子表格、演示文稿、数据库等。随着该版本的发布，Sun 开始免费提供 Solaris。

Solaris 9 于 2002 年发布；它对系统管理进行了增强，使管理员能够在系统上分配资源、监控使用情况并生成系统使用统计报告的能力。它为系统管理引入了名为 Web Start 的新用户界面。Solaris 9 还支持用于进程的 Secure Shell（安全外）以及一个面向企业级用户的目录。

2005 年，Sun 发布了其最新的 Solaris 版本。Solaris 10 已被 Open Group 注册为认证 UNIX 产品。此外，为了应对 Linux 的流行，Sun 设计了 Solaris 10 以供在 Intel x86 和 AMD 系统上使用。对于服务器和企业级使用，Solaris 10 提供了资源管理增强。可以对资源使用设置限制，以防系统过载。它允许将系统在逻辑上划分为区域（zones），每个区域通过容器（containers）拥有自己的功能。Solaris 10 引入了对 IP 6 的支持，集成到其 NFS/RPC 和 NIS/NIS 中。如需更多关于 Solaris 的信息，请访问 http://www.sun.com/solaris/。如需更多关于免费 Solaris 的信息，请访问 http://www.sun.com/solaris/。

## OpenBSD

OpenBSD 由其创始人 Theo De Raadt 于 1994 年从 NetBSD 中拆分出来。OpenBSD 的初始版本发布于 1996 年。该项目每六个月发布一个新版本，维护并支持一年。它以对安全的强支持而闻名，提供了其他 UNIX 变体中未发现的安全功能和能力。OpenBSD 完全基于源代码并可以在免费限制下获得许可。OpenBSD 的开发者付出了额外努力，对源代码进行漏洞和安全问题审计。与其他基于 BSD 的 UNIX 变体一样，OpenBSD 的内核和用户程序是在单个源码仓库中共同开发的。

最新版本是 OpenBSD 3.8，于 2005 年底发布。OpenBSD 目前运行在 16 种不同的硬件平台上。第三方软件以二进制包的形式提供，或者可以使用其端口从源码编译。

如需更多关于 OpenBSD 的信息，请访问 http://www.openbsd.org/

## Solaris

Microsystems 的原始操作系统是 SunOS。它基于 UNIX System V Release 2 和 4.BSD。1991 年，Microsystems 将 SunSoft 设为一个独立的子公司，负责软件（包括操作系统）的开发和营销。在成立之初，Sun 开始从 SunOS 迁移到基于 SVR4 的新 UNIX 版本。Sun 的第一个 UNIX 版本 Solaris 1.0 拥有增强版的 SunOS。

随着 Solaris 2.0 的推出，SunSoft 转向了基于 SVR4 的操作系统。尽管 2.0 是 Solaris 的第一个“官方”版本，但由于其支持的工作站数量有限，它并没有被广泛使用。第一个运行在所有基于 SPARC 的和基于 x86 的工作站上的版本是 Solaris 2.1，它于 1992 年底发布。

下一个重大版本是 Solaris 2.3，于 1993 年 11 月发布，它为 Solaris 环境引入了许多变化，包括最新版本的 X Window 系统，并开始在某些图形系统中使用 Display PostScript。Solaris 2.3 同样符合 POSIX 标准。Solaris 2.4 于 1994 年发布；包含了 Motif。Solaris 2.5 于 1995 年发布，包含了许多新功能，如通用桌面环境（CDE）、POSIX 线程和基于 TCP 的 NFS。

Solaris 2.6 是第一个支持 Java 的 Solaris 版本，于 1997 年发布。Solaris 2.6 还符合 X/OPEN 的 UNIX95 标准，并包含了 Y2K 修复。

Solaris 7（弃用了数字 2，直接称为 7）于 1998 年发布；它包含了许多提高可用性和可靠性的新功能。其中一些改进针对 64 位应用程序以及基于 Web 的管理和配置。

Solaris 8 于 2000 年引入。它包含了许多性能和管理增强，集成了一个用于提供网页服务的网络缓存加速器、支持进程聚类、用于重新分配资源的自动重新配置、热补丁（hot-patching）能力、操作系统的即时更新（live updating）以及集中化管理功能。它还提供了安全增强，包括内置防火墙、对 Kerberos 支持、基于角色的访问控制以及对 IPsec（IP 安全）的支持，后者实现了互联网上经过验证的连接。它引入了对 IP 6 的支持，并集成到其 NFS/RPC（网络文件系统/远程调用）和 NIS/NIS（网络信息服务）中。Solaris 8 还包含 StarOffice 5，它提供了文字处理器、电子表格、演示文稿、数据库等。随着该版本的发布，Sun 开始免费提供 Solaris。
