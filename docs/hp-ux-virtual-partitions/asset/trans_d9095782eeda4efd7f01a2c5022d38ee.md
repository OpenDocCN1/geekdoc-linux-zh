

# 虚拟分区主机相关信息

```
# ROUTE_ARGS[0]=""

# 动态路由守护进程配置。参见 gated(1m)
# GATED: 设置为 1 以启动 gated 守护进程。
# GATED_ARGS: 传递给 gated 守护进程的参数。

GATED=0
GATED_ARGS=""

# 路由器发现协议守护进程配置。参见 rdpd(1m)
# RDPD: 设置为 1 以启动 rdpd 守护进程

RDPD=0

# 逆 ARP 守护进程配置。参见 rarpd(1m)
# RARP: 设置为 1 以启动 rarpd 守护进程

RARP=0

ROUTE_GATEWAY[0]=172.16.14.1
ROUTE_COUNT[0]=1
ROUTE_DESTINATION[0]=default
```

我们也可以在 SAM 中查看和配置与网络相关的信息。图 13-1 展示了 SAM 中第二个 vPar（*cable2*）上 *lan1* 的与网络相关的信息：

![](img/eff8b9287a5f38c5adf538f24aacf29e_857_0.png)

这些窗口显示了我们之前在各个文件和命令行中查看到的信息。一些系统管理员更喜欢在 SAM 中修改和查看信息，而另一些则更喜欢在命令行中操作。

# 使用两张网卡配合 Telnet

分配给虚拟分区的局域网卡可以像在非 vPar 系统上那样用于多种用途。当两个不同 vPar 中的用户或应用程序进行通信时，它们是通过局域网进行的。在正常操作中，vPar 并没有为通信提供任何特殊的机制。（然而，vPar 之间确实存在特殊的系统管理通信，例如虚拟分区数据库的同步，这是以特殊方式进行的。）当在两个 vPar 之间建立通信会话时，即使它们位于同一台服务器上，也会使用两个 vPar 上的局域网接口。这包括 `telnet`、`ftp` 以及 Berkeley 的“r”命令，如 `rlogin`。以下示例展示了书中许多示例中使用的两个 vPar 之间的 `telnet` 会话。在此示例中，vPar `cable1`（主机名 `cvhdcon3`）发起与 vPar `cable2`（主机名 `cvhdcon4`）的 `telnet` 会话：

```
# hostname cvhdcon3
# telnet cvhdcon4
Telnet3 - <--- 在 cable1 上开始
已连接到 cvhdcon4。 <--- telnet 到 cable2
转义字符是 `^]'.
本地流量控制已开启
Telnet TERMINAL-SPEED 选项已开启
HP-UX cvhdcon4 B.11.11 U 9000/800 (tc)

login: root
Password:
请稍候...正在检查磁盘配额
(c) Copyright 1983-2000 Hewlett-Packard Co., All Rights Reserved.
(c) Copyright 1973, 1980, 1983, 1985-1993 The Regents of the Univ. of California
(c) Copyright 1980, 1984, 1986 Novell, Inc.
(c) Copyright 1986-1992 Sun Microsystems, Inc.
(c) Copyright 1985, 1986, 1988 Massachusetts Institute of Technology
(c) Copyright 1989-1993 The Open Software Foundation, Inc.
(c) Copyright 1986 Digital Equipment Corp.
(c) Copyright 1990 Motorola, Inc.
(c) Copyright 1990, 1991, 1992 Cornell University
(c) Copyright 1989-1991 The University of Maryland
(c) Copyright 1998 Carnegie Mellon University
(c) Copyright 1991-2000 Mentor Inc.
(c) Copyright 1996 Morning Star Technologies, Inc.
(c) Copyright 1996 Progressive Systems, Inc.
(c) Copyright 1991-2000 Isoftex Corporation, All Rights Reserved.

RESTRICTED RIGHTS LEGEND
美国政府的使用、复制或披露受 DFARS 252.227-7013 中技术数据和计算机软件权利条款子段 (c)(1)(ii) 中规定的限制。

Hewlett-Packard Company
3000 Hanover Street
Palo Alto, CA 94304 U.S.A.

非国防部的美国政府部门和机构的权利如 FAR 52.227-19(c)(1,2) 中所述。

TERM 的值已设置为 "hp"。
警告：您是超级用户 !!

# hostname
cvhdcon4    <--- 已连接到 cable2
#
```

只有当您的系统中有两张网络卡——每个 vPar 一张——时，您才能使用 **telnet**、**rlogin** 或其他类似的连接方法。对于其他功能也是如此，例如从 vPar 备份到另一个具有本地磁带驱动器的 vPar 或系统，这要求两个系统都必须有网卡。我认为为每个 vPar 配备一张专用网卡是必要的。

本章剩余部分包含大量的网络背景信息。

网络配置因安装环境而异。一些安装环境，例如高度集中且隔离的系统，仅连接 ASCII 终端，系统管理员只需很少关注网络。而其他安装环境，例如高度分布式的环境，其中成千上万台系统连接到可能跨越多个地理位置的网络，系统管理员可能需要大量关注网络。在后一种场景中，系统管理员用于网络的时间可能超过用于所有其他系统管理功能时间的总和！而不是像第一位系统管理员那样完全忽略网络，或像第二位系统管理员那样可能需要涵盖网络管理的所有方面，我将在本章中介绍适用于大多数 UNIX 系统的网络方面。这些内容基于我在各种新的 UNIX 安装环境中工作的经验。如果您需要的网络背景知识超出了本章涵盖的范围，我推荐以下书籍作为出色的网络信息来源：Bruce H. Hunter 和 Karen Bradford Hunter 著的 *UNIX Networks*（Prentice Hall，ISBN 0-13-08987-1）。

在本章中，我主要提供许多网络主题的背景知识，而非设置信息，因为设置工作主要由系统管理员执行。我所涵盖的大部分内容有时被称为“互联网服务”。总的来说，我将在本章中介绍网络的基础知识。这包括 ARPA 和 Berkeley 服务。以下是我涵盖的主题列表：

-   通用 UNIX 网络背景
-   互联网协议 (IP) 寻址（A、B 和 C 类）
-   子网掩码
-   ARPA 服务
-   Berkeley 命令
-   主机名映射
-   网络文件系统 (NFS) 背景
-   UNIX 网络命令

我在本章中提供了许多 UNIX 命令的摘要和示例。关于这些命令的更多详细信息可以在您的 HP-UX 系统的联机手册页中找到。虽然 vPars 仅运行在 HP-UX 上，但我在本章的示例中使用了多种系统，包括 Solaris、AIX 和 HP-UX。由于 HP-UX 系统管理员通常管理许多 UNIX 变体，因此我希望提供尽可能全面的示例集。

# UNIX 网络

连接到其他机器是每个 UNIX 网络的重要组成部分。这意味着既连接其他 UNIX 机器，也连接非 UNIX 机器。机器必须在物理上相互连接，并在功能上相互连接，以便您可以执行诸如传输文件和登录其他系统之类的任务。您的 UNIX 系统上存在许多命令，为您提供在系统之间登录和传输文件的功能。这些被称为 ARPA 命令，即 telnet 和 ftp。

telnet 命令允许在异构环境中进行远程登录。例如，从您的 UNIX 系统，您可以 telnet 到非 UNIX 系统并登录。在远程系统上登录后，您需要了解正在该系统上运行的操作系统。如果您需要连接另一台计算机只是为了在系统之间传输文件，那么您可以使用 ftp。此命令允许您在任意两个系统之间传输文件，而无需了解远程系统上运行的操作系统。

与可以在 UNIX 系统之间发出的命令相比，这些命令相对原始。对于 UNIX 系统而言，网络不是事后需要添加到系统中的附加部分。ftp 和 telnet 命令随您的 UNIX 系统提供，以及您可以用来在您的 UNIX 系统和其他 UNIX 系统之间通信的更高级命令和功能。这些更高级的命令被称为 Berkeley 命令，允许您远程执行许多命令，例如复制文件和目录以及登录。这种功能-

