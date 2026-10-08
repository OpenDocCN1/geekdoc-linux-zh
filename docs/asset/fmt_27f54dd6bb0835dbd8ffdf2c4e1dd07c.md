
在 Linux shell 中输入 `hosts.deny` 可以了解其详细语法。

### 启动时配置网络

你希望在每次启动系统时，网络都能自动启动。为了实现这一点，你必须将相应的命令放在一个或多个启动脚本中。`init` 进程在 Linux 启动后立即运行。该进程读取 `/etc/initab` 文件并根据运行级别执行不同的命令（通常是 shell 脚本）。

`/etc/initab` 指定 `init` 运行带有参数 3 的脚本文件 `/etc/rc.d/rc`。

核心启动脚本最终调用 `/etc/rc.d/init.d/network` 来激活所有网络接口。如果你查看 `/etc/rc.d/init.d/network` 文件，你会注意到网络初始化是通过使用 `/etc/sysconfig` 目录下的另一组文件完成的。网络激活脚本会检查 `/etc/sysconfig/network` 文件中定义的变量来决定是否激活网络。

在 `/etc/sysconfig/network` 中，你应该能看到一行如下所示 `NETWORKING` 变量：
`NETWORKING=yes`

只有当 `NETWORKING` 变量设置为 `yes` 时，网络才会激活。相应的，`/etc/rc.d/init.d/network` 脚本会执行 `/etc/sysconfig/network-scripts` 中的许多脚本来激活特定的网络接口。例如，要激活以太网接口 `eth0`，会执行 `/etc/sysconfig/network-scripts/ifup` 并将 `/etc/sysconfig/network-scripts/ifcfg-eth0` 作为配置文件。以下是一个典型的 `/etc/sysconfig/network-scripts/ifcfg-eth0` 文件内容：

```
DEVICE=eth0

IPADDR=192.168.0.200

NETMASK=255.255.255.0

BROCAST=192.168.0.255

ONBOOT=yes

BOOTPROTO=none
```

如你所见，此文件包含了网络设备名称、接口的 IP 地址以及其他几个 TCP/IP 参数。`ONBOOT` 变量指示 Linux 启动时是否应该激活此网络接口。如果你的 PC 有以太网卡，则在启动时会有接口；因此，`ONBOOT` 设置为 `yes`。

`/etc/sysconfig` 目录下的文件是由 Red Hat Linux 安装程序在安装 Linux 时，按照第 2 章概述的步骤创建的。

`/etc/sysconfig/network-scripts/ifup` 脚本本质上运行了以下命令：

- `/sbin/ifconfig`，用于配置指定的网络接口；在此例中为以太网卡（`eth0`）
- `/sbin/route`，用于为激活的网络接口设置路由表

### TCP/IP 网络诊断

在配置好以太网和 TCP/IP 之后（在 Red Hat Linux 安装期间或稍后运行 `netconfig`），你应该能够无任何问题地使用各种网络应用程序。TCP/IP 协议族包含了几个工具，可以帮助监控和诊断问题。

### 检查接口

使用 `/sbin/ifconfig` 命令查看当前配置的网络接口。`ifconfig` 命令用于配置网络接口（即将 IP 地址与网络设备关联）。如果你运行不带任何命令行参数的 `ifconfig`，该命令将显示当前网络接口的信息。以下是 `ifconfig` 的典型调用及其产生的输出：

```
/bin/ifconfig

eth0 Link encap:Ethernet Haddr 02:60:8C:8E:C6:A9

     addr:192.168.0.4 Bcast:192.168.0.255 Mask:255.255.255.0

     UP BROADCAST TRAILERS RUNNING MTU:1500 Metric:1

     RX packets:2738 errors:0 dropped:0 overruns:0 frame:0

     TX packets:1397 errors:0 dropped:0 overruns:0 carrier:0

     collisions:0

     RX bytes:638288 (623.3 Kb) TX bytes:575658 (562.1 Kb)
```

```
lo Link encap:Local Loopback

     addr:127.0.0.1 Mask:255.0.0.0

     UP LOOPBACK RUNNING MTU:16436 Metric:1

     RX packets:48 errors:0 dropped:0 overruns:0 frame:0

     TX packets:48 errors:0 dropped:0 overruns:0 carrier:0

     collisions:0

     RX bytes:3148 (3.0 Kb) TX bytes:3148 (3.0 Kb)
```

此输出显示系统上当前有两个接口——环回接口（`lo`）和以太网卡（`eth0`）——处于激活状态。对于每个接口，你可以看到 IP 地址以及数据包交付和发送的统计信息。如果 Red Hat Linux 系统有一个正在运行的拨号 PPP 链路，你还会在输出中看到一个 `ppp0` 接口。

### 检查 IP 路由表

另一个网络配置命令 `/sbin/route` 在不带任何命令行参数运行时也会提供信息。如果你在检查到另一个主机（由你通过 IP 地址指定的 host）的连接时遇到困难，请检查 IP 路由表查看是否指定了默认网关。然后检查网关的路由表，确保通往外部网络的路径出现在该路由表中。

来自 `/sbin/route` 命令的典型输出如下：

```
/sbin/route

Kernel IP routing table

Destination Gateway Genmask Flags Metric Ref Use Iface

192.168.0.0      *      255.255.255.0 U      0 0 0 eth0

127.0.0.0         *      255.0.0.0   U      0 0 0 lo

default           192.168.0.1    0.0.0.0   UG     0 0 0 eth0
```

如此路由表所示，本地网络使用 `eth0` 接口，且默认网关也是处理发往除 Linux 所在网络之外任何网络数据包的设备。在这个示例中，发往任何网络的数据包都以 `192.168.0.1` 开始。网关将这些数据包转发到其他网络（当然，假设网关连接到了另一个网络）。

## 检查与主机的连通性

要检查到特定主机的网络路径，请使用 `ping` 命令。`ping` 是一种广泛使用的工具，它通过 ICMP（互联网控制消息协议）回文来确定主机是否存活，并可以计算往返延迟。

```
ping 192.168.0.1

PING 192.168.0.1 (56 bytes of data):

64 bytes from 192.168.0.1: icmp_seq=1 ttl=64 time=0.452 ms

64 bytes from 192.168.0.1: icmp_seq=2 ttl=64 time=0.481 ms

64 bytes from 192.168.0.1: icmp_seq=3 ttl=64 time=0.468 ms

64 bytes from 192.168.0.1: icmp_seq=4 ttl=64 time=0.465 ms

64 bytes from 192.168.0.1: icmp_seq=5 ttl=64 time=0.472 ms

---

5 packets transmitted, 5 packet received, 0% packet loss, time 4005ms

rtt min/avg/max/mdev = 0.452/0.467/0.481/0.012 ms
```

按 Ctrl+C 停止 ping。

## 第 6 章：网络设置

- 传输控制协议和互联网协议（TCP/IP）源于 20 世纪 70 年代美国政府高级研究计划署（ARPA）的一项研究计划。现代互联网是由该时期开发的网络技术演变而来的。
- 所有互联网协议都记录在“意见请求”（RFC）文档中。可以通过互联网资源 `http://www.cis.ohio-state.edu/hypertext/information/rfc.html` 获取 RFC。所有标准都包含在 RFC 中，但许多 RFC 仅是为互联网社区提供信息。
- 互操作性是 TCP/IP 协议的核心；这正是一个互联网协议的目的。TCP/IP 协议使用 32 位的 IP 地址来标识主机，该地址包含两个部分：网络地址和主机地址。
- 通常，IP 地址使用点分十进制表示法，其中每个字节的值以十进制格式写入，并用点（`.`）与相邻的字节隔开。一个典型的 IP 地址是 `132.250.112.52`。
- IP 地址按类分组。A 类使用一个网络地址和三个字节的主机地址；B 类地址使用两个字节的网络和主机地址；C 类地址使用三个字节的网络地址和一个单字节的主机地址。第一个字节的值指示地址类型：1–126 为 A 类，128–191 为 B 类，192–223 为 C 类。
- IP 地址空间正在迅速耗尽。为了缓解这一问题，互联网工程任务组采用了一种新的 16 字节（128 位）地址方案，称为 IPv6（或 IP 第 6 版）。使用新 IPv6 地址的主机将与使用旧 IPv4（32 位）地址的主机协作。
- 在 Linux 上设置 TCP/IP 需要设置各种配置文件。Red Hat 网络配置工具提供了一种设置这些文件的方便方法。您需要一些信息——例如 IP 地址、网关地址和名称服务器地址——来在您的系统上设置 TCP/IP 网络。如果您不计划将本地网络连接到互联网，可以使用一组 IP 地址的范围（例如 `192.168.0.0` 到 `192.168.255.255`），而无需与任何机构协调。
- Linux 带有许多 TCP/IP 实用程序，例如 `ftp`（文件传输协议）和 `telnet`（用于登录网络上的另一个系统）。
- 要诊断 TCP/IP 网络问题，您可以使用 `ifconfig`、`ping`、`route` 和 `netstat` 命令。

## 第二部分
## 探索 Red Hat Linux

- 第 7 章：Red Hat Linux 基础
- 第 8 章：GNU 工具
- 第 9 章：GUI 桌面
- 第 10 章：Linux 应用和工具
- 第 11 章：文本处理
- 第 12 章：基础系统管理

## 第 7 章
## Red Hat Linux 基础

### 本章内容

- 首次运行 Red Hat Linux
- 查找在线文档
- 理解 Linux 目录结构
- 使用 Linux 命令处理文件
- 理解 Shell：Linux 的命令解释器
- 查看 Bash（Bourne Shell）

现在你已经从本书的附带 CD-ROM 中安装了 Red Hat Linux，你已经准备好探索并学习 Red Hat Linux 的基础知识。本章将向你展示如何登录、注销和关闭你的 Linux 系统。然后你再次启动并学习 Linux 命令。

尽管 Red Hat Linux 带有 GNOME 和 KDE 图形用户界面，但并不是所有工作都可以在图形环境中完成。设计一个能够让你执行大多数日常任务的图形界面并非不可能，但有时当图形环境不可用时，你必须执行系统管理任务。你可能通过终端会话登录，也可能在 X 上遇到问题。在这种情况下，你必须使用 Linux 命令来完成特定任务。

本章还向你展示如何在 Red Hat Linux 中处理文件和目录。要使用文件和目录，你需要理解分级系统的概念。本章提供了 Linux 文件系统的简要介绍。然后你学习使用 Nautilus 图形 Shell 探索文件系统。最后，你将学习几个可以用于处理文件和目录的 Linux 命令。

### 首次启动 Red Hat Linux

安装完成后，Red Hat Linux 安装程序会自动重启系统。PC 将经过正常的上电序列并加载引导程序——`GRUB` 或 `LILO`，取决于你在安装 Red Hat Linux 时选择了哪一个。屏幕上会出现一个图形界面，列出引导程序可以启动的分区名称。你可以按上下方向键选择系统从哪个分区启动。当你安装引导程序时，如果指定了 Linux 分区为默认分区，你只需等待；几秒钟后 Red Hat Linux 启动。

Linux 启动后，你应该看到一长串启动信息，包括 Linux 检测到的设备名称。最早几条消息之一是 `Calibrating delay loop... 398.13 BogoMIPS`，BogoMIPS 前面的数字取决于你系统的处理器类型。BogoMIPS 是 Linux 的术语，指的是……

# 第二部分：探索 Red Hat Linux

![](img/32dd492a14c1741062582e3caae7f04b_217_0.png)

图 7-2：初始 GNOME 桌面

花点时间查看图 7-2 所示所示初始 GNOME 桌面。GNOME 桌面与 Windows 桌面非常相似。GNOME 面板（Panel）类似于 Windows 任务栏，出现在屏幕底部。你可以通过 GNOME 面板访问各种菜单并启动应用程序。面板还包含如“时钟”等的小程序，它在面板右侧的一个小区域内显示时间。

你将在第 9 章中学习更多关于 GNOME 桌面的知识。现在，你只需要知道 GNOME 面板左侧的样式化脚图标就是主菜单按钮。这个按钮类似于 Microsoft Windows 中的“开始”按钮。你可以通过主菜单按钮（脚）访问许多程序。你也可以通过点击面板上的图标启动某些程序。例如，要启动 Nautilus 图形外壳和文件管理器，点击面板上的指南针和地图图标，或者双击桌面上标有“在此处”（Start Here）的相同图标。

你将在本章稍后的部分以及第 9 章中学习更多关于 GNOME 桌面的知识。接下来的章节将向你如何注销和关闭你的 Red Hat Linux 系统。

# 注销

既然你已经学会了如何登录，应该学习如何注销。要注销，请选择主菜单（脚图标） ↩ 注销（Log Out）。屏幕变灰，弹出的框询问你是否确定要注销。点击“是”（Yes）按钮注销。

几分钟后，会出现图形登录界面（参考图 7-1），以便其他用户登录并使用系统。

# 关闭 Linux

当你准备好关闭 Red Hat Linux 时，应该按顺序进行操作。如果你是唯一用户，那么通常会有几个其他程序在后台运行。此外，像 Linux 这样的操作系统会尝试优化数据写入磁盘的方式。由于磁盘访问相对缓慢（与访问内存位置所需的时间相比），数据通常保留在内存中，并大块地写入磁盘。因此，如果你简单地关闭电源，可能会面临某些文件无法正确更新的风险。

任何用户（无需登录）都可以从图形登录界面关闭系统。登录窗口中的“系统”（System）菜单提供了重启或停止系统的菜单选项。要关闭系统，只需选择“系统” ↩ 停止（Halt），如图 7-3 所示。

![](img/32dd492a14c1741062582e3caae7f04b_218_0.png)

图 7-3：选择菜单选项以停止你的 Red Hat Linux 系统

另一个对话框询问你是否确定要注销。点击“是”（Yes）按钮。系统将按顺序关闭。

当系统关闭时，你可能会看到关于进程正在关闭的消息。即使没有人在系统上显式地运行任何程序，这种情况也会发生。如果你的系统在关闭时没有自动电源，你可以手动关闭电源。

# 第二部分：探索 Red Hat Linux

如果你已经以 root 身份登录，可以使用 `shutdown` 命令来停止或重启系统。如果你已使用另一个用户名登录，可以通过输入以下命令成为超级用户（你的输入将以粗体显示；我的注释为*斜体*）：

```
su-

Password: (输入 root 密码并按回车)
```

成为超级用户后，输入以下命令停止系统：
几分钟后，你会看到许多关于进程正在停止的消息。在旧版系统上，你会看到关于系统已停止的消息。然后你可以关闭电源。在新系统中，关闭过程会自动关闭电源。

```
/bin/shutdown -h now
```

如果你想重启系统而不是停止它，请使用带有 `-r` 选项的 `shutdown` 命令，如下：
另一方面，你也可以直接输入 `reboot` 来重启系统。

```
/bin/shutdown -r now
```

# 查找在线文档

你应该熟悉 Red Hat Linux 中的一个重要信息源。每隔一段时间，你会看到要求输入 Linux 命令的指令。过了一段时间，你不可避免会遇到记得命令名称，但不记得应该输入的语法的时刻。在这种情况下，Linux 在线手册页（man pages）可以为你提供帮助。

![](img/32dd492a14c1741062582e3caae7f04b_219_0.png)

要尝试本节描述的命令，你必须在 GNOME 中打开终端窗口。点击 GNOME 桌面底部的终端图标（参考图 7-2）。这会打开一个终端窗口，你可以在其中输入 Linux 命令。

你可以使用 `man` 命令查看命令的手动页——通常称为 man 页。（你必须记住这个命令来访问在线帮助）。例如，要查看 `modprobe` 命令的手动页，请在终端窗口中输入以下命令：

```
man modprobe
```

`man` 命令逐页显示帮助信息。按空格键移动到下一页。按 b 向后移动。按 q 返回提示符。例如，要查看 `debug` 命令的手动页，请在终端窗口中输入以下命令：

```
man debug
```

`man` 命令逐页显示帮助信息。按空格键移动到下一页。按 b 向后移动。按 q 返回提示符。例如，要查看 `debug` 命令的手动页，请直接输入以下命令：

```
arp (8) - 操作 ARP 缓存
```
