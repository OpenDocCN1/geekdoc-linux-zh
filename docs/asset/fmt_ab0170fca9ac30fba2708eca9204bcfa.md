
- ☐ http://www.netcom-sys.com/techdocs.html *SNMP 入门*

尽管它大量提到了 Nortel Networks 的 Opitivity 网络管理软件。

关于所有 SNMP 节点编号（即所有 1.3.6.2. ... 之类的东西）的解释，请参见：

- ☐ http://www.iana.org/assignments/smi-numbers

关于私有企业编号列表，请参见：

- ☐ http://www.isi.edu/in-notes/iana/assignments/enterprise-numbers

MIB-II 定义于：

- ☐ RFC-1213 1991年3月 *基于 TCP/IP 互联网的网络管理信息库：MIB-II*

MIB 模块使用 *ASN.1（抽象语法记法 1）* 编写，该标准描述于：

- ☐ RFC-2578 1999年4月 *管理信息结构版本 2 (SMIv2)*

Windows-NT SNMP 工具包含在 NT 4.0 资源工具包中。这些包括基本但实用的 `snmpmon` 工具。它可以让你指定特定主机上的一组 SNMP 变量，并定期监控它们（获取其值）；你可以根据结果执行任意命令，例如发送警报或电子邮件，或者在机器磁盘空间不足时从目录中删除临时文件等。

许多系统和网络管理员从头编写自己的工具来监控和控制系统的各个方面（例如监控磁盘空间、检查网络连接等）。与其重新发明轮子，不如考虑使用 SNMP。最初这需要更多时间，但很快它就能为你节省大量时间，并使你的工具更具可移植性和更通用的实用性。

我们还没有涵盖 SNMP 陷阱（traps）。代理必须预先配置管理站的地址——没有发现机制使 SNMP“客户端”机器能够自动找到管理站。（但它可以通过 DHCP 进行配置。）在 NT 上，`snmputil` `trap` 监听陷阱消息。

SNMP 只有四个命令：`get` 和 `set`（我们已使用过），`trap`（我们在上文讨论过），以及最后的 `get-next`。`get-next` 返回指定变量之后的变量值（或 OID）。通过指定树的根节点并反复使用 `get-next`，你可以在不知道树中内容或结构的情况下检索整棵树。这是使 SNMP 如此强大的功能之一。它让你可以浏览 MIB 树并获取你感兴趣的任何信息。Linux 包含 `snmpwalk` 命令，它通过反复使用 `get-next` 来检索你指定的变量下方的子树中的所有值。下面，我们展示了 system 节点的 `snmpwalk` 输出。`get-next` 对于处理大小未知的数组也是必不可少的。

```
alice% snmpwalk -On bob public system
1.3.6.1.2.1.1.1.0 = Hardware: x86 Family... Software: Windows NT Version 4.0
1.3.6.1.2.1.1.2.0 = OID: 1.3.6.1.4.1.311.1.1.3.1.3
1.3.6.1.2.1.1.3.0 = Timeticks: (663334843) 76 days, 18:35:48.43
1.3.6.1.2.1.1.4.0 =
1.3.6.1.2.1.1.5.0 = BOB
1.3.6.1.2.1.1.6.0 = Server rack no. 4
1.3.6.1.2.1.1.7.0 = 76
alice%
```

有一个名为 `getif`（“获取接口信息”）的图形化 SNMP 工具适用于 Microsoft Windows，可从以下地址获取：

- □ http://www.wtcs.org/snmp4tcp/

# Syslog

尽管 Syslog 非常古老，但它直到最近才被记录为 RFC：

- □ RFC-3164 2001年8月 BSD Syslog 协议

该协议提供了大量易于阅读的背景知识。syslog 及类似服务在日志记录和监控系统方面至关重要，但通过 UDP 传输的 Syslog 不会向发送者提供消息是否成功记录的反馈。最近的一个 RFC 规定了如何通过可靠的（TCP）连接运行 syslog，并增强数据完整性和安全性：

- □ RFC-3195 2001年11月 Syslog 的可靠传输

Syslog 可以收集大量信息，为了充分利用这些信息，你需要某种形式的自动处理，例如，当出现特定警告消息或记录到特定类型的事件时，发出警报。一种易于配置的此类工具是 `Xlogmaster`：

- http://www.gnu.org/software/xlogmaster/

虽然该软件仍可供下载，但已不再进一步开发。即便如此，它目前仍然非常有用。一款具有额外分析功能的 *syslog* 服务器 Windows 版本由以下机构提供：

- http://www.kiwi-enterprises.com

这是商业软件，但他们也提供免费的版本。

其他日志分析工具：

- http://www.cert.dfni.de/eng/logsurfl Logsurfer 主页

- http://www.counterpane.com/log-analysis.html 日志分析资源

- http://www.oit.ucsb.edu/~eta/swatchl SWATCH：简单的监视器（Simple WATCHer）

- http://www.psionic.com/products/logsentry.html LogSentry（原名 Logcheck）

# Ipr

- RFC-1179 1990年8月 行式打印机守护进程协议（Line Printer Daemon Protocol）

Ipr 是 Linux 上的标准打印系统。它也作为 Microsoft TCP/IP 打印网络服务在 Windows-NT 上可用。

# NTP

NTP 的标准为：

- RFC-1305 1992年3月 网络时间协议（版本 3）规范、实现与分析

该文本版本中的一些图表和表格格式混乱。一个更易读的版本是

- ftp://ftp.isi.edu/in-notes/rfc1305.pdf

NTP 的一个轻量级版本，适用于要求较低的应用程序，称为 *SNTP*（简单网络时间协议），描述如下：

- RFC-2030 1996年10月 适用于 IPv4、IPv6 和 OSI 的简单网络时间协议（SNTP）版本 4

NTP 的大部分工作由特拉华大学的 David Mills 完成：

- http://www.eecs.udel.edu/~mills/database/brief/overview/overview.htm

- http://www.ntp.org

遗憾的是，我们发现许多关于 NTP 的文档难以理解，且从未见过好的教程或概述。然而，上述概述相对来说是能够理解的。

要查找你可以使用的 NTP 服务器，请咨询你的 ISP 或访问 http://www.ntp.org。

关于其他时间相关信息，包括一些实时显示，请参阅：

- http://tycho.usno.navy.mil 美国海军天文台时间服务部门 美国国防部和美国时间标准的官方来源

仅对于 Windows 系统，你可以使用 `net time` 命令将一台机器与另一台机器（例如 masterbox）进行同步。在“客户端”上，输入命令

```
net time \\masterbox /set /yes
```

# NFS

描述 NFS 的原始 RFC 提供了关于其设计的一些有趣背景信息：

- RFC-1094 1989年3月 NFS：网络文件系统协议规范

- RFC-3010 2000年12月 NFS 版本 4 协议

关于文件句柄作为安全隐患的问题，请参阅书籍：

- William Cheswick 和 Steven Bellovin《防火墙与互联网安全：抵御狡猾的黑客》（1994年，Addison-Wesley 出版社）

为了允许文件以受控方式更新，在更新期间它们必须被“锁定”。NFS 使用“NFS 锁定管理器”服务器（通常称为 `lockd` 或 `rpc.lockd`）来处理此问题。

NFS 已被移植到各种机器和操作系统上，大约在 1990 年，它是跨异构网络共享文件和数据的方式。在仅使用 UNIX/Linux 的网络中，NFS 仍然是首选的共享文件系统。然而，要在 Linux/UNIX 和 Windows 之间共享文件，一个免费且优秀的替代方案是 Samba（模块 22.4）。

# 附录

- 附录 19：`nc` (netcat) 手册页全文

- 附录 20：控制网络服务

- 网络附录 22：RPC 端口映射器服务

# 第三部分

## 在 TCP/IP 网络上的 Microsoft Windows 网络

### 引言

大多数实际网络都包含 Microsoft Windows 机器，并且越来越多地包含 Linux 和 UNIX 机器。Windows 网络与我们之前涵盖的 TCP/IP 网络有很大不同。它是独立开发的，并在很大程度上使用自己的协议和机制（分层于 TCP/IP 之上且独立于 TCP/IP）进行基本操作，包括：

- 1. 名称解析

- 2. 登录和用户身份验证

- 3. “浏览”网络以自动查找可用机器和资源列表。
