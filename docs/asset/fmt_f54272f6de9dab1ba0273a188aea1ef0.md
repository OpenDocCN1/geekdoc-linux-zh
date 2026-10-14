
如果主机应转发到两个网络接口，请将此变量设置为 `yes`。这通常适用于路由器或“伪装”。脚本 `/etc/init.d/boot.proc` 通过 `/proc` 文件系统中的条目启用 IP 转发。

`DISABLE_ECN`="yes"

如果在使用 2.4 内核连接互联网上的某些机器时遇到问题，但 2.2 版本没有问题，可能是由于损坏的防火墙丢弃了带有 ECN（早期拥塞）标志的网络包。将其设置为 `yes` 以在启动时禁用 ECN。

`ENABLE_SYRQ`="no"

如果你将其设置为 `yes`，即使在系统崩溃时也能对系统进行某些控制，例如在内核调试期间。更多信息请参阅 `/usr/src/Documentation/sysrq.txt`。

# syslog 配置 syslog 守护进程。

`SYSLOG_ADDITIONAL_SOCKET_DHCP`="/var/lib/dhcp/log"

此变量的内容由 dhcp 包添加。此处引用的 `/etc/permissions.local` 在 `SYSLOG_PARAMS` 启动时会被添加。在 SuSEConfig 重启时需要此套接字。

`SYSLOG_ADDITIONAL_SOCKET_FROX`="/var/lib/frox/log"

此变量的内容由 frox 包添加。此处引用的 `/etc/permissions.local` 在 `SYSLOG_PARAMS` 启动时会被添加。在 SuSEConfig 重启时需要此套接字。

`SYSLOG_ADDITIONAL_SOCKET_STUNNEL`="/var/lib/stunnel/log"

此变量的内容由 stunnel 包添加。此处引用的 `/etc/permissions.local` 在 `SYSLOG_PARAMS` 启动时会被添加。在 SuSEConfig 重启时需要此套接字。

`KERNEL_LEVEL`="1"

klogd 的默认级别。

`SYSLOG_PARAMS`=""

用于 syslog 的参数，例如 `-s my.domain.com`。

`KLOGD_PARAMS`="-2"

klogd 的参数。

# syslog-ng 配置 syslog-ng。

`SYSLOG_REPLACE`="yes"

替换默认 syslog-ng。

`SYSLOG_NG_PARAMS`=""

syslog-ng 的参数。

`DEFAULT_WM`="kde"

默认窗口管理器。

`INSTALL_EXTENSIONS`="yes"

安装扩展。

`KDE_USE_FAM`="no"

是否 是否使用 fam？

`KDE_USE_MALLOC`="yes"

使用改进的 malloc？

`SUSE_UPDATE`="yes"

SUSE 是否更新？

`SUSE_WM`="all"

应生成文件的窗口管理器列表。

`SUSE_XPM`="yes"

将 SUSE XPM 设置为 yes。

`NTP_INITIALDATE`="yes"

NTP 之前的日期。

`NTP`="AUTO"

默认值为 AUTO，仅查询第一个服务器。

ypbind 配置 NIS 客户端。域名通过 YaST 直接设置在 `/etc/defaultdomain`。

`YPBIND_OPTIONS`="1"

ypbind 的额外选项。

`YBIND_LOCAL_ONLY`="no"

如果设置此选项，ypbind 将绑定到环回接口，主机无法查询。

`YBIND_BROADCAST`="no"

如果将此选项设置为 `yes`，ypbind 将忽略 `/etc/yp.conf` 并使用广播查找子网内的 NIS 服务器。请避免这样做，因为存在安全风险。

`YBIND_BROKEN_SERVER`="no"

如果你的网络中有绑定到 1024 以上高端口的 NIS 服务器，请将此设置为 `yes`。由于存在安全风险，你应该考虑用其他实现替换 NIS 服务器。

ypserv 配置 NIS 服务器。

`YPPWD_SRCDIR`="etc"

指定 YP 源目录，YP 将在该处搜索 passwd 和 group 表源文件。默认为 /etc

`YPPWD_CHFN`="no"

是否允许用户通过 ypchfn 更改其 GECOS 字段？

`YPPWD_CHSH`="no"

是否允许用户通过 ypchsh 更改其默认登录 shell？

tope 配置 ZOPE 系统。

`ZOPE_FTP`="yes"

可以通过 FTP 访问 ZOPE？

`ZOPE_FTP_PORT`="8021"

如果是，在哪个端口？

`ZOPE_HTTP_PORT`="8080"

如果你作为独立服务器运行 ZOPE，它应该占用哪个端口？

## 网络中的 Linux

Linux 真正是互联网的产物，它提供了各种网络工具和功能，以集成到所有类型的网络结构中。接下来介绍常用的 Linux 协议 TCP/IP。本文将讨论该协议的各种服务和特殊功能。可以使用 YoST2 配置使用网卡进行网络访问。文中讨论了中心配置文件并描述了一些最核心的工具。本章仅讨论了基本机制和相关的网络配置文件。通过调制解调器、ISDN 或连接使用 PPP 访问互联网可以通过 YoST2 完成，这在《用户指南》中会有描述。

- TCP/IP — Linux 使用的协议 . . . . . . . . . . 334
- IPv6 — 下一代互联网 . . . . . . . . . . 342
- 网络集成 . . . . . . . . . . . . . . . . . . . 346
- 手动网络配置 . . . . . . . . . . . . . . . . . . . 349
- SuSE Linux 中的路由 . . . . . . . . . . . . . . . . . . . 356
- DNS — 域名服务 . . . . . . . . . . . . . . . . . 358
- NIS — 网络信息服务 . . . . . . . . . . . . . . . . . . 367
- NFS — 共享文件系统 . . . . . . . . . . . . . . . . . 371
- DHCP . . . . . . . . . . . . . . . . . . . . . . 375

## 13 TCP/IP — Linux 使用的协议

Linux 和其他 Unix 操作系统使用 TCP/IP 协议。它不是单一的网络协议，而是一个提供各种服务的网络协议族。TCP/IP 基于一种用于军事目的的应用开发，并在 1981 年的一份 RFC 中定义了现在的形式。RFC 代表“意见征求”（Request for Comments）。这些文档描述了各种互联网协议以及操作系统及其应用程序的实现程序。从那时起，TCP/IP 协议经过了完善，但基本协议几乎保持没有不变。

> **提示**
>
> RFC 文档描述了互联网协议的设置。要扩展你对任何协议的知识，请参考相应的 RFC 文档。它们可以在线上获取：http://www.ietf.org/rfc.html

表 13.1 中列出的服务是为了通过 TCP/IP 在两台 Linux 机器之间交换数据。组成全球性的网络也被整体称为“互联网”。

| 协议 | 描述 |
| :--- | :--- |
| TCP | 传输控制协议：一种面向连接的安全协议。要传输的数据首先由应用程序作为数据流发送，然后由操作系统转换为适当的格式。数据到达目标主机上的相应应用程序时，保持最初发送时的原始数据流格式。TCP 确定在传输过程中是否丢失了任何数据，并确保没有混乱。在数据顺序重要的地方都实现了 TCP。 |

表 13.1: 续（跨页显示）...

### UDP

数据报文协议：一种无连接的、不安全的协议。要传输的数据以应用程序已经生成的包的形式发送。数据到达接收者处的顺序无法保证，并且存在数据丢失的可能性。UDP 适用于面向记录的应用程序。它具有比 TCP 更小的延迟周期。

### ICMP

互联网控制消息协议：本质上，这不是一个用户友好的协议，而是一种特殊的控制协议，用于发布错误报告并控制参与 TCP/IP 数据传输的机器。此外，ICMP 还提供了一种特殊的回显（echo），可以使用 `ping` 程序查看。

### IGMP

互联网组管理协议：该协议控制实现 IP 多组播时的机器行为。由于空间限制，后续章节不包含 IP 多组播的信息。

## 表 13.1: TCP/IP 协议族中的若干协议

几乎所有硬件都是基于数据包运行的。要传输的数据被封装在“束”中，因为它们无法一次性发送。这就是为什么 TCP/IP 只与小数据包一起。TCP/IP 包的最大大小约为 64KB。数据包实际上要小得多，因为网络软件可能是限制因素。数据包的最大尺寸约为一千四百百字节。

## 网络中的 Linux

### IP（互联网协议）

IP（互联网协议）是数据发生的地方。图为每一层提供了一个示例。见图 13.1

| 主机 | |
| :--- | :--- |
| 应用层 | |
| 传输层 | TCP |
| 通信层 | IP |
| 安全层 | FDDI |
| 比特传输层 | |

图 13.1: 简化层结构
