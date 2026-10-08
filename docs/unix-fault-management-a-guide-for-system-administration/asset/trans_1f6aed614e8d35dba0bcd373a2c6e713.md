
## 监控 DHCP

DHCP 允许客户端从可用地址池中获取 IP 地址。/etc/bootptab 文件用于 BOOTP 客户端以及具有固定 IP 地址的 DHCP 客户端。属于某个池的客户端在 /etc/dhcpdtab 中配置。

在 HP-UX 上，可以使用 dhcpools 来跟踪 DHCP 数据包或检查 DHCP 守护程序的内部状态。例如，这可用于查找配置问题。操作员可以确定是否有 IP 地址可供分配给客户端，以及可用的 IP 地址总数。dhcpools 还有一个选项，允许对 DHCP 请求和响应进行数据包跟踪。

请注意，监控服务器状态是困难的，因为当 DHCP 无事可做时，它可能会自行关闭。

## 监控 DNS/NIS 名称服务器

域名系统（DNS）和网络信息服务（NIS）是提供名称解析的两个服务。NIS 具有额外的功能，例如在多个系统之间维护一致的配置信息。

检查这些服务的一种简单方法是向服务器应用程序发送查询。除了检查服务可用性外，你还可以获得响应时间的快照。请注意，在此例及其他示例中，服务监控是从客户端系统进行的。

配置文件 /etc/resolv.conf 包含本地系统正在使用的名称服务器的 IP 地址。示例如图 6-16 所示。如果你在名称解析方面遇到问题，可能需要 ping 该文件中列出的服务器。

### 名称服务切换

名称服务切换允许你指定使用哪种名称服务进行名称解析和其他查询。你可能需要检查 /etc/nsswitch.conf 文件，以查看系统中名称解析是如何进行的。nsquery 命令可用于测试名称服务切换的行为。

### nslookup

nslookup 可用于确定某个名称服务器是否知道某个特定的主机名。图 6-17 显示名称服务器成功将系统名称解析为 IP 地址。

## 监控 FTP

文件传输协议（FTP）用于在系统之间高效地传输文件。检查 FTP 是否正常工作的一种简单方法是使用 ftp 传输任意文件。除了指示请求是否成功外，ftp 还会告诉你传输速率。在连接期间，你可以使用 status FTP 命令来检查远程 FTP 会话的状态，如图 6-18 所示。

**图 6-16** 检查 /etc/resolv.conf 中的名称服务器。

```
# more /etc/resolv.conf
domain cup.hp.com
nameserver 15.27.217.36  # cup44ux
nameserver 15.13.168.63  # hpperfl
```

**图 6-17** 使用 nslookup 获取系统的 IP 地址。

```
# nslookup gsyview1
Name Server: cup44ux.cup.hp.com
Address: 15.27.217.36

Name: gsyview1.cup.hp.com
Address: 15.13.174.132
```

ftp 会拒绝访问 /etc/ftpusers 中列出的本地用户账户，因此如果 ftp 对某些用户不起作用，请确保检查此文件。

## 监控 NFS

网络文件系统旨在为用户提供远程文件系统的透明视图，并使这些远程文件系统看起来像是本地挂载的。NFS 可以是共享文件系统以节省磁盘空间并简化管理的有用工具。所有 NFS 客户端共享存储在 NFS 服务器上的单个文件副本。透明性的缺点是，客户端可能意识不到通过读取简单文件所引起的网络流量。此外，客户端可能不知道其他人正在同时访问这些文件。

NFS 可能会出现许多问题。进程可能会死亡或挂起。NFS 的关键进程包括 nfsd、automount、lockd、statd 和 portmap。这些进程的状态可以使用 ps 命令检查。

NFS 请求由 NFS 服务器守护程序（nfsd）处理。这些守护程序从单个 UDP 套接字读取请求。守护程序的数量是可调整的，最佳数量取决于系统负载和 NFS 活动。如果没有运行足够的守护程序，内核可能会在请求到达时丢弃一些 NFS 请求，以避免溢出为这些数据包保留的存储区域。你可以通过使用 netstat -s 检查 UDP 套接字溢出数量来检测此问题。增加守护程序数量应能减少套接字溢出并提高 NFS 性能。然而，目前尚无工具帮助你确定需要增加多少守护程序。过多的 NFS 守护程序可能通过服务器负载平均值的增加来识别。此外，由于溢出数量是一个系统范围内的统计数据，问题可能是由另一个 UDP 应用程序引起的。在假设任何问题都是由 NFS 引起之前，你可能希望使用 netstat 显示当前的 UDP 活动。

**图 6-18** 来自 FTP status 命令的输出，显示远程机器的状态。

```
ftp> status
Connected to hpssc16.cup.hp.com.
No proxy connection.
Mode: stream; Type: binary; Form: non-print; Structure: file
Verbose: on; Bell: off; Prompting: on; Globbing: on
Store unique: off; Receive unique: off
Case: off; CR stripping: on
Ntrans: off
Nmap: off
Hash mark printing: off; Use of PORT cmds: on
ftp>
```

如果你负责监控 NFS，你还应该检查导出文件系统和磁盘的状态，查看它们是否已满或不可用。应检查 NFS 统计数据，以查看是否已报告 NFS 超时。MeasureWare 收集有关时间间隔内 NFS 请求数量和速率的统计数据。BMC PATROL 提供与其 UNIX KM 一起使用的工具，用于监控 NFS 活动和远程过程调用（RPC）。

### nfstat

nfstat 的输出可以让你了解环境中发生的 NFS 负载类型。如果你想建立基准来测量典型的服务器负载，这会很有用。

nfstat 可以报告 NFS 客户端、NFS 服务器或两者的信息。图 6-19 中的示例显示了 NFS 客户端的统计数据。

坏事务标识符（XID）指标表示在未发出请求的情况下收到响应的次数。这可能表明客户端请求超时过快并被重发。如果客户端有大量坏 XID 数据包和超时，你应该使用 mount 实用程序增加超时值。

服务器上大量的符号链接解析可能表明客户端将不合适的名称配置为挂载点。

图 6-19 显示客户端 NFS 统计数据的输出。

```
# nfstat -c

Client rpcs:

calls   badcalls retrans  badxid   timeout   wait   newcred
200     0        0        0        0        0     0

Client nfs:

calls   badcalls ncget   nclsleep
200     0      200    0
null   getattr  setattr  root   lookup  readlink read
0 0%   133 66% 0 0%    0 0%   0 0%    0 0%   0 0%
wrache  write    create   remove  rename  link  symlink
0 0%   0 0%     0 0%    0 0%   0 0%    0 0%   0 0%
mkdir  rmdir    readdir  statfs
0 0%   0 0%     0 0%    67 33%
#
```

## NFS 的 NetMetrix

NetMetrix 提供扩展用于监控 NFS 服务。监控器用于捕获网络流量，然后可以计算 NFS 服务性能。图表可以显示负载、响应时间、重传次数和错误数量等信息。

## HA NFS

HA NFS 工具包作为 MC/ServiceGuard 产品的附加组件提供。可以检测并报告 NFS 服务器故障，并在另一个节点上重新启动 NFS 服务。故障转移期间不维护 NFS 锁。

## 监控远程连接

rlogin 和 telnet 提供远程登录功能，使客户端能够访问 UNIX 系统。对于 rlogin，由 inetd 启动的应用程序称为 logind，而对于 telnet，守护程序是 telnetd。who 命令可以显示已登录到系统的用户。使用 ps -f | grep logind 来查看有多少用户远程连接，以及他们已连接了多长时间。

## 监控 Web 服务器

监控互联网服务是一种新现象，监控 Web 服务器的工具才刚刚开始出现。Netscape 的 SuiteSpot 服务器软件与 HP OpenView 技术捆绑在一起，为高端、企业级 HP-UX 用户提供互联网监控和故障管理。

HP OpenView Internet Service Manager 提供工具来管理 Web 资源利用率和性能。监控是从 IT/O 管理站进行的。为以下基于 UNIX 的互联网服务提供管理：

- Netscape Enterprise Server
- Netscape Fasttrack Server
- Netscape News
- Netscape Proxy Server
- Netscape Mail
- NCSA Web Server
- Apache Web Server

Internet Service Manager 还可以识别损坏的 HTML 链接。

CompuWare 也有一些工具，如 EcoScope 和 Single View，可用于监控 Web 服务器。可以在协议级别分析网络流量以捕获 HTTP 数据包。然后 Single View 可以报告流量负载，并包含针对 Web（HTTP）、安全 Web（HTTPS）和其他协议的专门互联网利用率报告。

## 监控网络主机

在共享网络介质上，仅监控客户端和服务器系统是不够的。其他网络设备可能对网络连通性至关重要。前面已经讨论了名称服务器；如果名称服务不可用，你的应用程序可能无法连接到服务器，因为它无法确定服务器的 IP 地址。负责将你的数据包传输到服务器 LAN 段的 routers 也可能已宕机。

除了网络故障外，还可能出现性能问题。共享 LAN 上的拥塞可能会阻止你的数据传输。性能监控工具将在下一节中讨论。
