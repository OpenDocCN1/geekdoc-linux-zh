
此示例在名为 `/test2` 的卷上创建了 `/ubuntu` 目录的精确副本，并在 `/root` 下保存了名为 `backup_log.txt` 的备份报告。

## 使用 MC 复制文件

Midnight Commander（可在 Universe 仓库中通过软件包 `mc` 获得；请参阅第 7 章“管理软件”以启用 Universe 和 Multiverse 仓库）是一个命令行文件管理器，用于复制、移动和归档文件及目录。Midnight Commander 的外观和感受与 DOS 时代的 Norton Commander 相似。通过在 shell 提示符处执行 `mc`，会显示文件的双窗格视图。它包含用于操作文件的下拉菜单选项和功能键。它使用自己的虚拟文件系统，能够挂载 FTP 目录并显示 tar 文件、gzipped tar 文件（`.tar.gz` 或 `.tgz`）、bzip 文件、DEB 文件和 RPM 文件的内容，并从中提取单个文件。不仅如此，`mc` 还包含一个针对 ext2/3 分区的“文件删除”虚拟文件系统。通过使用 `cd` 切换目录到 FTP 服务器的 URL，你可以使用 FTP 协议传输文件。Ubuntu 的默认字体使得 `mc` 在 tty 控制台（与 x 模式相比）中使用时显示得很难看，但不会影响其性能。

图 13.4 显示了默认双面板显示的截图。按下 F9 键会弹出菜单，按下 F1 键会显示帮助文件。默认 GNOME 终端中的一个“特性”会拦截用于退出 `mc` 的 F10 键，因此请使用 F9 访问菜单项，或者直接用鼠标点击栏上的菜单。配置文件有详尽的文档，如果你理解 shell 脚本和正则表达式，扩展 `mc` 的功能似乎轻而易举。对于未运行 X 的服务器的文件管理，这是一个极佳的选择。

![](img/10660b76df3ff0bf16a3b9e3a30edd9d_347_0.png)

> **提示：** 使用剪切粘贴可能需要按住 Shift 键

图 13.4 Midnight Commander 是一个功能多强大的文件工具。如果它在你的系统上显示异常，请使用 `-a` 启动以强制 ASCII。

## 系统救援

总会有需要进行系统救援的时候。这发生在系统无法启动 Linux 导致你无法恢复任何文件时。这个问题最常见于引导加载程序或分区表，但也可能是由于关键系统文件被无意删除或损坏导致的。如果你一直在进行备份，这类系统故障可以通过完整恢复来解决，尽管速度并不快。尽管如此，自上次计划备份以来，某些当前数据可能尚未被备份，且发现备份文件损坏、不完整或丢失。完整恢复还需要你可能没有的时间。如果导致系统故障的原因仅仅是损坏的引导加载程序、损坏的分区表、缺失库或配置错误，快速修复即可让系统恢复运行，然后就可以轻松检索数据。

## Ubuntu 救援盘

Ubuntu 在安装 DVD 中隐藏了一个救援盘。要使用它，请插入光盘并重启计算机，像你最初安装 Ubuntu 时一样从 DVD 启动。

如有必要，你可以在救援模式下执行本节讨论的所有操作。

## 备份和恢复主引导记录

主引导记录 (MBR) 是硬盘的前 512 字节。它在前 446 字节中包含引导加载程序，在接下来的 64 字节中包含分区表；最后两个字节识别引导签名。

## 使用恢复设施

当您的电脑启动时，Ubuntu 将显示一条消息，提示您按 Escape 键以查看 GRUB 菜单。如果您这样做，将会看到一个可启动操作系统的列表，其中包含您 Ubuntu 安装环境的恢复模式。如果您进入恢复模式，您将获得机器的自动 root 权限，可以在那里安全地解决问题。

或者，您可以插入 Ubuntu 安装光盘并从那里使用恢复模式。请记住，这些恢复模式是为了系统恢复目的而设计的纯文本系统；不要指望它们像手持设备那样方便，也不要对它们的易用性抱有太大期望！

## 相关的 Ubuntu 命令

以下命令在 Ubuntu 的备份、恢复和还原操作中非常有用：

- `amdump` — Amanda 是一个基于网络的备份系统，由 18 个独立的命令组成，用于 Linux 系统。
- `ark` — 一个 KDE 桌面 GUI 归档工具。
- `cp` — 复制命令。
- `scp` — 安全 shell 复制命令。
- `cpio` — 一个数据归档工具。
- `dd` — 一个数据复制和转换工具。
- `gzip` — GNU 压缩工具。
- `tar` — GNU 磁带归档工具。

## 引用

- [http://www.tldp.org/LDP/solrhe/Securing-Optimizing-Linux-RH-Edition-v1.3/whywhen.html](http://www.tldp.org/LDP/solrhe/Securing-Optimizing-Linux-RH-Edition-v1.3/whywhen.html) — 关于使用 dump 和 restore 进行备份的详细讨论及示例
- [http://www.tldp.org/LDP/solrhe/Securing-Optimizing-Linux-Edition-v1.3/chap29sec306.html](http://www.tldp.org/LDP/solrhe/Securing-Optimizing-Linux-Edition-v1.3/chap29sec306.html) — 使用 tar cron 任务进行自动备份
- [http://kmself.home.netcom.com/Linux/FAQs/backups.html](http://kmself.home.netcom.com/Linux/FAQs/backups.html) — Linux 备份小型 FAQ 包含了关于备份媒体、压缩、加密和安全的一些有用但简短的注释
- [http://www.tldp.org/](http://www.tldp.org/) — Linux 文档项目提供了若干实用的 HOWTO 文档，讨论了备份和磁盘恢复
- [http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html/single/Bootdisk-HOWTO.html#AEN1483](http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html/single/Bootdisk-HOWTO.html#AEN1483) — 这里有 LILO 启动错误代码列表，帮助您调试无法启动的顽固系统
- [http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html/single/Ftape-HOWTO.html](http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html/single/Ftape-HOWTO.html) — 这是用于软盘带驱动程序的
- [http://www.linux-usb.org/USB-guide/x498.html](http://www.linux-usb.org/USB-guide/x498.html) — 大存储设备的 USB 指南。如果您有 USB 设备并需要知道它是否被支持，请在此查看
- [http://www.backupcentral.com/amanda.html](http://www.backupcentral.com/amanda.html) — 这是《Unix 备份与恢复》中的一个章节（John R. Jackson 编写，O'Reilly and Associates 出版）。该章节在线可用，涵盖了使用 Amanda 的各个方面。该网站为章节提供了方便的搜索工具
- [http://wiki.org/cgi-bin/view/Wikilearn/RsyncingLargeFileBeginner](http://wiki.org/cgi-bin/view/Wikilearn/RsyncingLargeFileBeginner) — 使用 rsync 同步大文件以“修复”未通过 md5sum 的本地 ISO 镜像
- [http://www.lycoris.org/sections.php?op=viewarticle&art=8](http://www.lycoris.org/sections.php?op=viewarticle&art=8) — Lycoris ISO rsync 微型 HOWTO。关于使用 rsync 同步文件的逐步教程
- [http://www.mikerubel.org/computers/rsync-snapshots/](http://www.mikerubel.org/computers/rsync-snapshots/) — 使用 rsync 进行的自动化快照式备份
- [http://www.mondorescue.org/](http://www.mondorescue.org/) — Mondo Rescue 是一种独立于 Ubuntu 的裸机备份/救援工具，使用 CD、DVD、磁带或 NFS；它可以生成可引导的 CD 来恢复系统
- [http://www.ccp14.ac.uk/ccp14admin/linux-server/mondrescue/dvd-mondo.html](http://www.ccp14.ac.uk/ccp14admin/linux-server/mondrescue/dvd-mondo.html) — 使用 MondoRescue 在 DVD 上进行备份的 HOWTO
- [http://www.linuxorbit.org/modules.php?op=modload&Sections&file=index&req=viewarticle&partid=222&page=1](http://www.linuxorbit.org/modules.php?op=modload&Sections&file=index&req=viewarticle&partid=222&page=1) — 使用 split 和 mkisofs 手动将大型归档备份到 CD 的 HOWTO

# 第 14 章 网络

## 本章内容

- 奠基础：localhost 接口
- 使用 TCP/IP 网络
- 网络组织
- 网络硬件设备
- 使用网络配置工具
- 动态主机配置协议 (DHCP)
- 无线网络
- 越网络和互联网
- 常见配置信息
- 配置数字用户线路 (DSL) 接入
- 配置拨号上网接入
- 排除连接问题
- 引用

开源技术通用（特别是 Linux）的一个优点是，它可以毫不费力地应用于多个不同的网络环境以及互联网。由于对标准互联网协议 TCP/IP 的强大支持，Linux 还可以与所有 UNIX 变体通信，包括 Mac OS、Windows（通过 Samba 帮助）、NetWare (IPX) 以及 DECNET 和 Bantu Vines 等协议。许多组织使用 Linux 作为互联网网关，允许许多客户端通过 Linux 访问互联网，并通过电子邮件和即时消息进行通信。最重要的是它对 IPv6 的内置支持，这种支持应该在 2009 年期间开始被大量采用。可以说，无论你遇到什么种协议，Linux 都能以某种方式与之工作。

本章涵盖了网络连接，大多数情况下是以某种形式连接到互联网的。你将学习如何使用 Ubuntu 获取基础知识，包括网卡 (NIC) 和其他网络服务的配置和管理。你还会发现如何处理连接问题。

## 奠基础：localhost 接口

回环接口是你在连接到网络之前，在 Ubuntu 中需要设置的第一项，它通常被称为 `lo`。回环接口是用于本地通信的虚拟接口。

## 检查回环接口的可用性

## 手动配置回环接口

如果某些 Ubuntu 系统没有此接口，请编辑 `/etc/hosts` 文件添加 localhost 条目，并使用 `ifconfig` 和 `route` 命令使用您的 sudo 权限创建接口。

`/etc/hosts` 文件的第二行使用计算机的实际主机名，并将其分配给该计算机唯一的私有 IP 地址。在之前的代码示例中，你可以看到 `127.0.0.1` 被分配给 `hardy-laptop`，这是存放 `hosts` 文件的计算机。

其余行用于 IPv6，可以忽略，但以 `::1` 开头的行除外——它用于定义 IPv6 的本地回连接，你可以在终端使用 `ping6` 命令进行测试，如下：

```
$ ping6 ::1
PING ::1(::1) 56 data bytes
64 bytes from ::1: icmp_seq=1 ttl=64 time=0.037
64 bytes from ::1: icmp_seq=2 ttl=64 time=0.045
64 bytes from ::1: icmp_seq=3 ttl=64 time=0.048
::1 ping statistics
3 packets transmitted, 3 received, 0% packet loss, time 1998ms
rtt min/avg/max/mdev = 0.037/0.043/0.048/0.007
```

## 使用 TCP/IP 网络

任何基于 Unix 的网络的构建模块都是传输控制协议/互联网协议 (TCP/IP) 三种协议套件。该套件由互联网协议 (IP)、传输控制协议 (TCP) 和通用数据报协议 (UDP) 组成。IP 是基础协议。TCP/IP 是基于包的，这意味着数据在发送端被拆分成以传输到接收端。将数据拆分成可管理的包可以实现更快、更准确的传输。在 TCP/IP 中，所有数据都通过数据包传输，这就是地址被称为 IP 地址的原因。它是该套件的最低层。

TCP 也是基于连接的协议。在两台机器之间传输数据之前，它们之间会建立一个连接。一旦建立连接，数据流会被发送到 IP 分成数据包进行传输。在接收端，数据包会被按顺序排列并发送到相应的应用程序。TCP/IP 构成了互联网的基础；如果没有它，互联网将是一个完全不同的地方，如果它真的存在的话！

另一方面，UDP 是一种无连接协议。使用该协议的应用程序只需选择目标并开始发送。UDP 通常用于小量数据或在快速且可靠的网络上。如果你对 TCP/IP 的内部机制感兴趣，请参阅本章末尾的“参考”部分查找更多信息。

## Ubuntu 与网络

你的网卡可能在安装 Ubuntu 期间已经配置好了。你可以在 shell 提示符中使用 `ifconfig` 命令，或使用 Ubuntu 的图形化网络配置工具（如 `network-admin`）来编辑系统的网络设备信息，或在系统中添加或删除网络设备。Ubuntu 包含了数百个网络命令和工具——多到在本章中无法涵盖，甚至足够写两三本书。

几乎所有的以太网卡都可以 Linux 使用，许多 PCMCIA 有线和无线网络设备在 Linux 下运行良好，并将在未来的 Linux 内核中支持。访问 http://www.linux-usb.org/ 查看 USB 项目的最新进展或验证对你设备的支持。

阅读本章后，你可能想了解更多用于 Linux 的其他图形化客户端。例如，GNOME ethereal 客户端可以监控局域网 (LAN) 或特定类型的流量。另一个工具 NmapFE 可扫描特定主机的端口和其他运行的服务。

## TCP/IP 寻址

理解 Linux 网络，你需要了解 TCP/IP 寻址的基础知识。互联网 IP 地址（也称为公共 IP 地址）与局域网（LAN）内部使用的地址不同。互联网 IP 地址由美国互联网数字机构（地址为 http://www.arin.net/）为美国及其他某些主机分配。需要互联网地址的实体向该机构申请地址。该机构向互联网服务提供商 (ISP) 分配一个或多个 IP 地址块，ISP 可以将其分配给其用户。

你会很快熟悉当前的 TCP/IP 寻址形式，即 IPv4（IP 版本 4）。在这种方法中，TCP/IP 地址表示为四个十进制数字——以点分十进制格式表示的 32 位值，例如 `192.168.0.1`。每组数字被称为一个字节（由八个 1 和 0 组成，例如 `10000000` 表示 128），范围从 0 到 255。

第一个字节决定网络属于哪个类别。网络共有三类，这些类别为：

- **A 类** — 由第一个字节为 1 到 126 的网络组成。只有 126 个 A 类网络——每个网络最多包含 16,777,214 个主机。（如果你在计算，潜在地有 16,777,216 个地址，但地址的主机部分不能全为 0 或 255。“10.”网络预留给本地网络使用，“127.”网络预留给 127.0.0.1 回环地址。TCP/IP 使用回环寻址使 Linux 相关的网络客户端和服务器程序与同一主机通信。）

- **B 类** — 由第一个字节为 128 到 191 的网络组成。有 16 个 B 类网络——每个网络最多包含 65,534 个主机。（如果你在计算，潜在地有 65,536 个地址，但地址的主机部分不能全为 0 或 255。“172.”网络预留给本地网络使用。）

- **C 类** — 由第一个字节为 192 到 223 的网络组成。有 256 个 C 类网络——每个网络最多包含 262,142 个主机。（如果你在计算，潜在地有 262,144 个地址，但地址的主机部分不能全为 0 或 255。“192.168.”网络预留给本地网络使用。）

## 网络组织

在作为互联网网关的同时，还应该作为防火墙保护你的网络免受恶意数据和用户的侵害。

以这种方式使用的 PC 通常至少有两个网络接口。一个连接到互联网，另一个连接到局域网（LAN）上的计算机（集线器或交换机）。某些宽带设备还集成了四个或更多网络接口。数据通过网络地址转换（NAT）在局域网和互联网之间传输，这在 Linux 内核中通常被称为 IP 伪装。

> **注意**
> 不要对你的局域网仅依赖单点保护，特别是当你使用无线网络、提供拨号服务，或为移动（笔记本电脑或 PDA）用户提供网络内部或外部访问权限时。依赖“护城河心态”的公司、机构和个人往往会沮丧地发现，这种安全方法很容易被破解。请确保你的网络操作配有一项安全策略，该策略强调多级访问控制，并在每台服务器和工作站中构建保护功能——在使用 Linux 时这可以轻松实现。

## 端口

你网络上的大多数服务器都有多个任务。例如，Web 服务器必须同时提供标准页面和安全页面。出于此原因，应用程序提供了端口，用于为特定软件服务建立“直接”连接。这些端口帮助 TCP/IP 区分服务，以便数据能够到达正确的应用程序。如果你检查文件 `/etc/services`，你将看到常用端口及其用途。例如，对于 FTP、HTTP 和邮局协议（邮件检索），你会看到：

```
ftp 21/tcp
http 80/tcp http # WorldWideWeb HTTP
```
