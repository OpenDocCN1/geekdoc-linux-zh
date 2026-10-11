

为了避免跺脚和愤怒的目光，无论遇到什么问题，都要计划让你的系统尽可能平稳地运行。在系统上线之前，就要提前规划好应急方案；此时，良好的日志记录和系统追踪将再次发挥作用。

一旦出现服务中断，指责往往立刻开始——而且无可避免地（无论是否合理）都指向系统管理员。你可能需要为自己（或更多利益相关者）挽回颜面，指出市场副总裁每十分钟就和朋友们互发电影文件，从而堵塞带宽并导致拒绝服务；或者指出相邻两个办公区那位才华横溢的程序员写了新代码，却在数据库机器上派生无限进程，使其不堪重负。

无论如何，你可能需要实施一项使用策略。根据你的具体情况和环境，这种策略可以是口头传达的（“别在我的系统上运行 *screen*，否则你的磁盘空间会被没收。”），也可以是像互联网服务提供商所采用的可接受使用政策（AUP）那样的书面文件。许多大型企业使用 AUP；而在较小企业中，策略可能采取非正式的、“心照不宣”的期望形式。

你需要制定一套策略来应对系统上愤怒的用户。务必提供大量可供阅读的文档，并让他们方便地访问可用资源。拥有多种选择的感觉有助于让他们保持满意（同时让你能够专注于处理其他事务，例如搭建备份系统或学习 Perl）。然而，有时你确实需要面对愤怒的用户。如果是这样，请保持冷静，不要对事不对人。查明具体问题所在；尽可能消除投诉中的情绪成分。

## 建立安全性

当一切正常运行时，尽你所能防止系统遭到攻击。这包括采取一切可行措施防止入侵、定期备份系统以应对入侵发生的情况，以及在遭到攻击后进行清理。

## 防止入侵

为防止入侵，请尝试攻击你自己的系统。这并不意味着通过手动暴力破解密码来获取 root 权限（那将非常愚蠢）。相反，请运行那些精于算计且狡诈的黑客会用来攻击你系统的相同工具。这些工具包括：

- ◆ SATAN – 基于 HTML 的界面扫描器
- ◆ TAMU Tiger – COPS 的更新版本
- ISS 的互联网安全扫描器 – 如果你在本地主机上运行则免费
- nmap – 来自 http://www.insecure.org/nmap/index.html 的免费软件
- Crack – 这个密码破解器可以帮助发现弱密码

根据你的具体情况，你最好在将上述任何工具用于你自己的网络之前通知同事和经理。（你不想让他们产生误解，对吧？）

![](img/8ad518fddafc7f5e73715a2604b61d50_70_0.png)

你可以在以下网站找到这些工具：http://www.tigerair.com/security.html。

首先，你可能想要运行 `nmap`，这是一个非常好的端口扫描器，它可以向你展示你系统中哪些端口对你域内的所有人开放（这个域可以是 ISP 或 LAN）。以下是如果在你自己的系统上运行它时可能显示的一个示例：

```
Starting nmap V. 1.49 by Fyodor (fyodor@dhp.com, www.dhp.com/~fyodor/nmap/)
Open ports on mysystem.lifcorp.com (40.49.7.9):
Port Number Protocol Service
11 tcp systat
15 tcp netstat
21 tcp ftp
23 tcp telnet
25 tcp smtp
37 tcp time
79 tcp finger
80 tcp www
110 tcp pop3
111 tcp sunrpc
113 tcp auth
143 tcp imap2
513 tcp login
514 tcp shell
515 tcp printer
704 tcp unknown
```

![](img/8ad518fddafc7f5e73715a2604b61d50_71_0.png)

请记住，这里列出的 IP 地址并不是实际测试所用的 IP 地址。（你觉得我会让别人在我的系统上尝试这种操作吗？）

由于该示例中大多数端口未被使用，它们应当被关闭。你使用的端口应反映系统的用途——不多也不少。例如，如果我运行 Web 服务器，我会保持 FTP 和 HTTP 端口开放；如果我运行邮件服务器，我会保持 25 端口开放。

请注意，上面给出的示例代码列表显示了存在已知可利用弱点的服务（包括 imap2、login、shell 和 SMTP）。黑客可能会利用这些协议将你的 Web 服务器变成涂鸦艺术家的地盘。

![](img/8ad518fddafc7f5e73715a2604b61d50_71_1.png)

Finger 端口绝不应该开放。虽然展示一条有趣的 plan 文件消息并让人看到你最后一次在线的时间很可爱，但事实是，黑客可以通过这个端口从你的系统中获取过多的信息——包括那些可能拥有弱密码的用户名。

当你准备审查主机安全性时，TAMU Tiger 和 Crack 是最佳使用的工具。尽管你已采取当前的安全措施，它们仍能轻松揭示你的主机资源中哪些是可被利用的。

互联网安全扫描器（ISS）的功能与 SATAN 类似，但其报告功能强大得多——不过同时对你的系统运行两者始终是个好主意。这些工具会展示你的网络漏洞，例如 NFS、Berkeley “r” 命令以及任何可被利用的开放端口。

列表 2-3 显示了 ISS 扫描的部分结果。虽然 ISS 早期版本存在性能问题，但 5.1 版本拥有出色的日志记录和报告功能，可提供被扫描主机的信息。从列表 2-3 中可见的日志文件部分，你可以看到 ISS 试图探测了多少信息。

![](img/8ad518fddafc7f5e73715a2604b61d50_71_2.png)

第九章将详细介绍 ISS 的报告功能。

### 列表 2-3：查看 ISS 扫描结果

```
# Time Stamp(13924): Beginning Host Scan: (899851221) Tue Jul  7 15:40:21
# Time Stamp(13924): Querying DNS for hostname: (899851222) Tue Jul 7 15:40:22
127.0.0.1: Hostname: Could not resolve hostname
# Time Stamp(13924): Ping Host: (899851227) Tue Jul 7 15:40:27
# Pinging Host.
127.0.0.1: Round Trip Time: 0s 899us
# Time Stamp(13924): Service check: (899851227) Tue Jul 7 15:40:27
# Scanning Known Services
# Services Scanned for:
# tcp-mux echo discard systat daytime netstat chargen ftp-data
# ftp ssh telnet smtp time whois domain mtp
# gopher rje finger httpd link sudup hostnames iso-tap
# x400 x400-snd csnet-ns pop pop3 sunrpc ident sftp
# uucp-path nntp ntp stasrv netbios-rpc netbios-ns netbios-dgm netbios-ssn
# imap NewS SNMP SNMPTRAP print-srv xdmcp imap2 https
# snnp tserver exec login shell private talk ntalk
# courier conference netnews uucp uucp-login whoami remotefs ipcservers
# doom webster phonexobk CODatBase oid-finger SOCKS IngresLock oracle
# pppp tcp-id-port callbook cfinder dls-monitor netrek[game] unknown unknown
# fax unknown netrek[game] X irc-serv irc a5serv or dos backdoor?
# backdoor? httpd unknown unknown crossfire[game]
# Scanning services (no source routing).
127.0.0.1:Service Failure 1 ("tcp-mux" service): Transport endpoint is not connected.
127.0.0.1:Service Failure 7 ("echo" service): Transport endpoint is not connected.
127.0.0.1:Service Failure 9 ("discard" service): Transport endpoint is not connected.
127.0.0.1:Port 11 ("systat" service) opened.
127.0.0.1: systat service running
127.0.0.1:Service Failure 13 ("daytime" service): Transport endpoint is not connected.
127.0.0.1:Port 15 ("netstat" service) opened.
127.0.0.1: netstat service running
127.0.0.1:Service Failure 19 ("chargen" service): Transport endpoint is not connected.
127.0.0.1:Service Failure 20 ("ftp-data" service): Transport endpoint is not connected.
127.0.0.1:Port 21 ("ftp" service) opened.
127.0.0.1: ftp service running
127.0.0.1:Port 22 ("ssh" service) opened.
127.0.0.1: ssh service running
127.0.0.1:Port 23 ("telnet" service) opened.
127.0.0.1: telnet service running
127.0.0.1:Port 25 ("smtp" service) opened.
127.0.0.1: smtp service running
127.0.0.1:Port 37 ("time" service) opened.
127.0.0.1: time service running
# Done Scanning Services
# Time Stamp(13924): half open scan: (899851227) Tue Jul 7 15:40:27
# HalfScan: Known Services
#
# HalfScan Legend:
#
# The HalfScan test is a protocol probe to test what information may be
# obtained covertly through packet filters and other obscuring mechanisms.
#
# Flag Definitions:
# zero: Test packet bearing no TCP Header (TH_) flags (Illegal)
# TH_ACK: Test pack bearing only TH_ACK flag (Connection on Session)
# TH_SYN: Test packet bearing only TH_SYN flag (Connection Request)
# TH_FIN: Test packet bearing TH_FIN and TH_ACK flags (Close Connect)
#
# Return Attributes on Active Port:
# a - Received a Reset on a TH_ACK packet
# A - Received an ACK on a TH_ACK packet
# f - Received a Reset on a TH_FIN packet
# F - Received an ACK on a TH_FIN packet
# s - Received a Reset on a TH_SYN packet
# S - Received an ACK on a TH_SYN packet
# Z - Received no return on a zero flags packet
#
# Active Port: Any port returning an ACK for any combination of flags in
# a probe packet or any port returning a Reset for some but not all
# combinations of flags in a probe packet. This implies some sort
# of active use of that port or connection. An ACK to anything other
# than a TH_SYN probe would imply a protocol violation.
#
# Because the HalfScan test runs below the TCP protocol layer it lacks
# guaranteed delivery of packets and responses. This makes individual
# packet returns non-deterministic and subject to network conditions.
# especially when packets are routed over multiple hops. For that reason,
# the HalfScan test runs multiple phases and accumulates results. The
# test nominally runs 5 phases (0-4) but may be extended for noisy or
# slow networks
# HalfScan done: Known Services
# Time Stamp(13924): Telnet banner check: (899851227) Tue Jul 7 15:40:27
127.0.0.1: -- telnet begin output --
```

