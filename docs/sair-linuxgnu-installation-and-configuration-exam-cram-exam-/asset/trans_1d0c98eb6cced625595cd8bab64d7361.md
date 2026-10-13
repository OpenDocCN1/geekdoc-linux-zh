
## 问题 7

有多种工具可用于设置新用户。然而，它们在你的 Linux 系统上本质上执行相同的功能。设置新用户时，以下哪项操作不会执行？假设新用户名为 tr。

- a. 从 /etc/skel 目录复制类似 .bash_profile 的文件
- b. 将用户名和主目录添加到 /etc/passwd 文件
- c. 在 /home/tr/.bash_profile 中设置用户的 shell 配置文件
- d. 将 /home/tr 目录的所有权分配给 tr
- e. 将 tr 分配到特定组并为该组设置 /home/tr 目录

答案 c 正确。设置新用户时，无需编辑 .bash_profile 文件。因为像 .bash_profile 这样的文件是从 /etc/skel 复制到用户主目录的，因此答案 a 不正确。所有用户名及其主目录都必须是 /etc/passwd 文件的一部分；因此，答案 b 不正确。用户 tr 需要拥有自己的主目录才能使用它；因此，答案 d 不正确。因为你希望用户 tr 及其主目录属于同一组，因此答案 e 不正确。

## 问题 8

你的其中一个用户打电话给你说他的系统在 GIMP、一个图像编辑程序中卡住了。以下哪个命令可以帮助你找到 GIMP 的进程标识符？假设该用户是目前唯一在你的系统上使用 GIMP 的人。

- a. ps aux | grep gimp
- b. ps | gimp
- c. ps | grep gimp
- d. top

答案 a 正确。此命令列出所有当前正在运行的进程并将输出发送到 grep 命令，该命令查找文本字符串 gimp。因为 ps 命令本身仅列出你自己的当前正在运行的进程，所以答案 b 和 c 不正确。虽然 top 命令如果 GIMP 使用了你系统上的所有 CPU 或内存资源时会有效，但那可能不是问题。因此，答案 d 不正确。

## 问题 9

以下哪个命令适合从批处理文件设置大量用户和密码？

- a. linuxconf
- b. newusers
- c. useradd
- d. userbatch

答案 b 正确。newusers 命令设置为从用户名和密码的批处理文件创建用户。因为 linuxconf 只能一次创建一个用户，所以答案 a 不正确。虽然你可以在脚本中设置 useradd 来从批处理文件获取用户名，但你仍需要分配密码。因此，答案 c 不正确。没有 userbatch 命令；因此，答案 d 不正确。

## 问题 10

Netscape 似乎使你的系统卡住了。你无法在 X Window 中关闭它。你已登录到另一个虚拟控制台并运行了 top 命令。你知道 Netscape 的 PID 为 1436。你如何停止 Netscape？

- a. stop 1436
- b. kill 1436
- c. kill netscape
- d. stop netscape

答案 b 正确。此命令杀死 PID 为 1436 的进程，你已将其识别为 Netscape 的进程。没有 stop 命令；因此，答案 a 和 d 不正确。因为 kill 命令只识别 PID，所以答案 c 不正确。

## 需要了解更多？

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_244_0.png)

Volkering, Patrick, Kevin Reichard, and Eric Foster-Johnson. *Linux Configuration and Installation*. M&T Books, Foster City, CA, 1998. ISBN 0-76457-005-6. 一步一步的指南，涵盖本章中的配置命令，并基于 Slackware 发行版。

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_244_1.png)

The Linux System Administrators' Guide at www.tml.hut.fi/~viu/linux/sag is written for newer administrators. 你也可以通过 Linux Documentation Project 在 www.linuxdoc.org 找到该指南的副本。

## 网络配置

你需要了解的术语：

- LAN, WAN
- Domain, hostname
- Hardware address
- Address classes
- Network mask
- Gateway
- DNS, DHCP
- NFS, Samba
- Apache, sendmail
- Web browsers, FTP clients
- Telnet, mail manager

你需要掌握的技术：

- 描述局域网
- 理解域名、IP地址和硬件地址
- 列出五个 IP 地址类
- 使用网络掩码
- 理解网关和访问其他网络
- 描述网络地址服务：DNS 和 DHCP
- 详细说明其他网络服务：NFS、Samba、sendmail 和 Apache

Linux 网络是一个复杂的话题，值得拥有自己的考试。尽管如此，对于本次考试，你需要了解足够的网络知识来在局域网（LAN）上配置 Linux 计算机，该局域网还连接到外部网络，例如互联网。

你还需要了解一些可用的 Linux 网络服务，例如网络文件系统（NFS）、Apache 或 sendmail。然而，对于安装和配置考试，你不需要知道如何配置这些服务。

*Note: 本章提供了对 Linux 上 TCP/IP 的最简介绍，这对于 Sair Linux/GNU 安装和配置考试来说是足够的。其他网络协议栈未涵盖。本章中有许多“简化”，允许经验较少的读者快速理解基础知识。如果你要设置 Linux 网络，请参阅本章末尾“需要了解更多？”部分中的一些书籍。*

## 网络基础

网络由两个或多个设置为相互通信的计算机系统组成。在某种程度上，你使用的“媒体”并不重要。你可以使用并行电缆、电话调制解调器、以太网卡、无线适配器或任何允许你的计算机交换信息的其他媒体来设置网络。如果你可以直接或通过集线器连接这些计算机，你可以设置一个 LAN。每个 LAN 通常都有一个特殊的 IP 地址，称为网络地址。

LAN 连接彼此靠近的计算机，例如在办公室或建筑物内。互联网由两个或多个连接的 LAN 组成。一些互联网是广域网（WAN）。WAN 由两个或多个地理上分离的网络组成。最大的 WAN 是互联网。

*Note: 在相当小的地理区域内一起管理的两个或多个 LAN 有时被称为城域网（MAN）。*

由同一组管理的任何网络或网络组通常被称为域。

当你为网络配置计算机时，你会为其分配一个 IP 地址。在一台计算机能够真正与另一台计算机通信之前，它必须将此 IP 地址翻译为其网络卡的硬件地址。

## 局域网和广域网

Linux LAN 通常配置为一种标准，称为 IEEE 802.3，更流行地称为以太网。这种类型的网络比电话调制解调器快得多；以太网网络允许计算机以 10、100 或甚至 1,000 兆比特每秒（Mbps）的速度通信。

*Note: 普通以太网的最大速度为 10Mbps，快速以太网的最大速度为 100Mbps，而千兆以太网的最大速度为 1,000Mbps。*

但以太网上计算机之间的距离限制在几百米之内，具体取决于连接类型。从本质上讲，LAN 能够覆盖的区域有限，但 LAN 速度快。相比之下，WAN 中 LAN 之间的连接可以覆盖互联网的距离，但连接速度有限。即使是“高速”WAN 连接通常也限制在 1Mbps 或更低。

> 尽管你可以通过 LAN 连接甚至通过互联网安装 Linux，但通常从本地媒体（如 CD-ROM）安装 Linux 仍然更快，如第 5 章所述。

## 互联网

即使你从未设置过网络，从你使用互联网的经验来看，你很可能已经对网络有所了解。当连接到互联网时，大多数用户通过互联网服务提供商（ISP）工作。

*Note: 一些较大的公司拥有直接连接到互联网的连接并充当自己的 ISP。*

当你连接时，你的计算机成为该 ISP LAN 的一部分。你获得一个 IP 地址，它是一组由句点分隔的 0 到 255 之间的四个数字。例如，www.mommabears.com 的 IP 地址是 199.93.70.2。

> 如果你当前已连接到网络，你可以使用 `/sbin/ifconfig` 命令找到你的 IP 地址。

你通过 ISP 的网关连接到互联网，它是一台将该 ISP 连接到互联网其余部分的计算机。当你搜索域名，例如 mommabears.com 时，你的计算机必须通过你 ISP 的域名服务（DNS）服务器找到 mommabears 的 IP 地址。或者，你可能在你的 `/etc/hosts` 数据库文件中有 IP 地址。

## 域

当你安装 Linux 时，大多数安装程序会询问你的域名。程序期望的名称类似于 ilikelinux.now。除非你的计算机
