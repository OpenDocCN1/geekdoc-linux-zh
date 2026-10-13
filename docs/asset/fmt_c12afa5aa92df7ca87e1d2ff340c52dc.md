
UDP 允许应用程序从一个主机向另一个主机发送有限长度的消息。与 IP 一，UDP 的主要优点是开销低，这使其适用于短时间、频繁的主机间交互，以及那些偶尔丢失消息并不比快速发送数据更重要的交互。当需要错误检测和恢复时，则使用 TCP。

### TCP

TCP 允许应用程序从一个主机向另一个主机发送数据流。与 IP 和 UDP 不同，TCP 是一种面向连接的协议。在主机通过 TCP 交换数据之前，会建立会话。

### 应用协议

TCP/IP 提供了许多应用程序协议，称为服务。此外，程序员可以轻松基于 UDP 或 TCP 创建新服务。此类端口被称为已知端口。在 UNIX 下，文件 `/etc/services` 标识了这些已知端口。表 4.1 总结了重要的 TCP/IP 服务及其端口号。

### 表 4.1 重要的 TCP/IP 服务及其端口号

| 端口 | 底层协议 | 服务 | 描述 |
|---|---|---|---|
| 7 | UDP/TCP | echo | 确定远程主机可访问。 |
| 9 | UDP/TCP | discard | 提供对丢弃输入服务的访问。 |
| 11 | TCP | systat | 显示活动用户。 |
| 13 | UDP/TCP | daytime | 以 ASCII 字符串提供本地时间。 |
| 15 | TCP | netstat | 提供网络性能统计数据。 |
| 17 | TCP | qd | 提供“每日格言”。 |
| 18 | UDP/TCP | msp | 向用户发送一条简单消息。 |
| 19 | UDP/TCP | charger | 发送字符流。 |
| 20 | TCP | ftp-data | 用于文件传输协议 (FTP) 服务发送数据。 |
| 21 | TCP | ftp | 用于 FTP 服务发送控制信息。 |
| 22 | UDP/TCP | ssh | 提供对安全外壳服务的访问。 |
| 23 | TCP | telnet | 提供对 telnet 远程外壳服务的访问。 |

### 表 4.1 重要的 TCP/IP 服务及其端口号（续表）

| 端口 | 底层协议 | 服务 | 描述 |
|---|---|---|---|
| 25 | TCP | smtp | 提供对简单传输协议 (SMTP) 的访问。 |
| 37 | UDP/TCP | time | 提供二进制格式的时间。 |
| 43 | TCP | whos | 提供名称和地址信息。 |
| 53 | UDP/TCP | domain | 提供对域名服务 (DNS) 的访问。 |
| 67 | UDP/TCP | bootsp | 被启动协议 (boot)服务器使用。 |
| 68 | UDP/TCP | bootpc | 被启动协议 (boot)客户端使用。 |
| 69 | UDP | tftp | 提供对简单文件传输协议 (TFTP) 的访问。 |
| 70 | UDP/TCP | gopher | 提供对 Gopher 信息检索服务的访问。 |
| 79 | TCP | finger | 提供对 finger 服务的访问，用于描述用户。 |
| 80 | UDP/TCP | www | 提供对 HTTP (Web) 服务的访问。 |
| 88 | UDP/TCP | kerberos | 提供对 Kerberos 认证服务的访问。 |
| 109 | UDP/TCP | pop-2 | 提供对邮局服务（版本 2）的访问。 |
| 110 | UDP/TCP | pop-3 | 提供对邮局服务（版本 3）的访问。 |
| 111 | UDP/TCP | sunrpc | 提供对远程过程调用 (RPC) 服务的访问。 |
| 端口 | 底层协议 | 服务 | 描述 |
|---|---|---|---|
| 113 | TCP | auth | 提供对 BSD ident 认证服务的访问。 |
| 119 | TCP | nntp | 提供对网络新闻传输协议 (NNTP) 服务的访问。 |
| 123 | UDP/TCP | ntp | 提供对网络时间协议 (NTP) 服务的访问。 |
| 137 | UDP/TCP | netbios-ns | 提供对 NetBIOS 名称服务的访问。 |
| 138 | UDP/TCP | netbios-dgm | 提供对 NetBIOS 数据报文服务的访问。 |
| 139 | UDP/TCP | netbios-ssn | 提供对 NetBIOS 会话服务的访问。 |
| 143 | UDP/TCP | imap2 | 提供对交互式邮件访问服务（版本 2）的访问。 |
| 161 | UDP | snmp | 提供对简单网络管理协议 (SNMP) 服务的访问。 |
| 162 | UDP | snmp-trap | 提供对 SNMP 服务的访问。 |
| 177 | UDP/TCP | xdmcp | 提供对 X 显示管理器控制协议 (XDMCP) 服务的访问。 |
| 179 | UDP/TCP | bgp | 提供对边界网关协议 (BGP) 服务的访问。 |
| 194 | UDP/TCP | irc | 提供对互联网聊天 (IRC) 服务的访问。 |
| 213 | UDP/TCP | ipx | 提供对 IPX (Novell 网络家族) 服务的访问。 |
| 220 | UDP/TCP | imap3 | 提供对交互式邮件访问服务（版本 3）的访问。 |
| 443 | UDP/TCP | https | 提供对安全 HTTP (Web) 服务的访问。 |
| 512 | UDP | biff | 提供通知用户邮件到达的服务。 |
| 512 | TCP | exec | 提供对远程执行 (REGEX) 服务的访问。 |
| 513 | UDP | who | 提供对维护用户数据库服务的访问。 |
| 513 | TCP | login | 提供对远程登录 (rlogin) 服务的访问。 |
| 514 | UDP | syslog | 提供对系统日志 (SYSLOG) 服务的访问。 |
| 514 | TCP | shell | 提供对远程 shell (RSH) 服务的访问。 |
| 515 | TCP | printer | 提供对远程打印 (LPR/LPD) 服务的访问。 |
| 517 | UDP | talk | 提供对聊天服务的访问。 |
| 518 | UDP | ntalk | 提供对聊天服务的访问。 |
| 749 | TCP | kerberos-adm | 提供对 Kerberos 认证服务器管理服务的访问。 |

### 守护进程 (Daemons)

在 UNIX 下，TCP/IP 服务可以通过以下三种方式之一支持：

- 通过 UNIX 内核
- 通过持续运行的进程
- 每当客户端请求服务时，由 `inetd` 进程启动进程

只有少数服务由内核直接支持。大多数服务由持续运行的进程或由 `inetd` 根据需要启动的进程支持。这些进程被称为守护进程（daemons），因为它们在运行时没有与控制终端关联。有时守护进程也被称为后台进程。表 4.2 描述了通常持续运行的重要 Linux 守护进程，表 4.3 描述了通常仅由 `inetd` 启动运行的重要 Linux 守护进程。

### 表 4.2 重要的 Linux 守护进程

| 守护进程 | 描述 |
|---|---|
| amd | 自动挂载和卸载文件系统。 |
| apmd | 高级电源管理 (APM) 功能。 |
| arpwatch | 跟踪 IP 地址和以太网地址的对应。 |
| atd | 为调度执行的任务排队。 |
| autofs | 为无盘客户端自动挂载 NFS。 |
| bootparamd | 提供有关网络的启动信息。 |
| crond | 执行调度命令。 |
| dhcpd | 为主机提供动态 IP 地址。 |
| diald | 通过电话线建立远程连接。 |
| gated | 管理控制台。 |
| httpd | Web 服务器。 |
| innd | 处理传入的 USENet 馈送。 |
| linuxconf | Linux 系统管理工具。 |
| lpd | 缓存并处理远程打印作业。 |
| marswe | 与 Novell NetWare 兼容的文件管理器。 |
| mcserv | 午夜命令 (Midnight Commander)。 |
| named | 域名服务。 |
| nmbd | NetBIOS 名称服务器。 |
| nfs | 提供对文件的访问。 |
| nscd | 身份验证缓存服务。 |
| pcmcia | 管理 PC 设备。 |
| portmap | 管理远程过程调用 (RPC) 连接。 |
| postgresql | 提供对数据库的访问。 |
| routed | 管理网络路由。 |
| rstat | 在其他网络主机上查找用户。 |
| rusersd | 在活动终端上显示消息。 |
| rwhld | 提供活动用户列表。 |
