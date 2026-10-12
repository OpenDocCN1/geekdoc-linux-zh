
# inetd

- □ Linux 手册页：inetd(8), inetd.conf(5), services(5)

程序 **xinetd**（“*扩展的 inetd*”）是 **inetd** 的一个流行替代品。它提供了广泛的日志记录、访问控制、子进程数量限制（以防止拒绝服务攻击）以及许多其他功能。参见：

- □ [http://www.xinetd.org/](http://www.xinetd.org/) *xinetd 主页*

# FTP

FTP 的规范是

- □ **RFC-959 1985年10月** *文件传输协议 (FTP)*

其早期章节易于阅读，并提供了一些有用的背景知识，其模块 4.2 列出了响应代码。

大多数可公开访问的 FTP 服务器允许你以用户 **anonymous** 的身份登录，并要求你提供完整的电子邮件地址作为密码。用户名 **ftp** 与 **anonymous** 相同，且*输入*起来要快得多。

目前越来越倾向于使用 HTTP 代替 FTP 进行文件下载，但有时仍优先使用 FTP 而非 HTTP，原因如下：

- • 对于服务器管理员来说，只需将文件复制到 FTP 目录比构建和维护包含指向该文件链接的 HTTP 页面更容易。（某些 HTTP 服务器允许你列出目录内容（如下所示），这削弱了这一优势。）

![](img/a2132b646d336d5f9a21102d6320e537_488_0.png)

- • FTP 支持多重传输。例如，你可以使用 FTP 命令 `mget *.pdf`（`mget` 意为“多重获取”）下载所有 PDF 文件
- • 如果 FTP 传输在会话中途断开，某些客户端和服务器允许你从断点处重新开始，而不是重新从文件开头开始，这对于正在传输非常大的文件时非常理想。

# netcat

- □ [http://freshmeeat.net/projects/netcat/](http://freshmeat.net/projects/netcat/)
- □ [http://www.attstake.com/research/tools/index.html](http://www.attstake.com/research/tools/index.html)
- □ [http://www.uit.co.uk/practcp/netcat.pdf](http://www.uit.co.uk/practcp/netcat.pdf) *Netcat 教程*

# X 窗口系统

关于 X 是什么以及它如何工作的详细描述，请参阅我们的书：

- Niall Mansfield *The Joy of X - An Overview of the X Window System* (1993, Addison-Wesley)

探索 Linux X 资源、Gnome 和 KDE 的良好起点是：

- http://www.linuxdoc.org/HOWTO/XWindow-User-HOWTO-11.html
- http://www.kde.org
- http://www.gnome.org
- http://www.linuxdoc.org/LDP/lame/LAME/linux-admin-made-easy/using-gnome.html *GNOME 安装与配置*
- http://www.linuxdoc.org/LDP/lame/LAME/linux-admin-made-easy/using-kde.html *KDE 安装与配置*
- http://www.gtk.org *The GIMP Toolkit*，这是一个用于创建图形界面的多平台工具包

X 现在也能在手持式计算机上运行：

- http://www.handhelds.org/

IBM 甚至已经让它在手表上运行（该手表运行 Linux！）。

一个相关的系统是 VNC（“虚拟网络计算”）：

- http://www.uk.research.att.com/vnc/

它被广泛用于远程管理 Microsoft Windows 系统。它允许你从另一个 Windows 系统或运行 X 的 Linux/UNIX 机器连接到 Windows 系统，并显示远程系统的完整屏幕，使用其所有功能。

# LDAP

- RFC-2251 *1997年12月 轻量级目录访问协议 (v3)*

LDAP 的许多原始工作是在密歇根大学完成的。他们的网站仍有一些历史信息：

- http://www.umich.edu/~dirsvc/ldap

但这已被 OpenLDAP 项目取代：

- http://www.openldap.org

我们的某些示例来自该发行版。

Microsoft 的活动目录（Active Directory）：

- http://www.microsoft.com/windows2000/techinfo/howitworks/activedirectory/adarch.asp *活动目录架构*
- http://www.labmice.net/ActiveDirectory/default.htm

Novell 的 eDirectory 或 NDS（Novell 目录服务）：

- ☐ http://developer.novell.com/nds/ndsldap.htm

关于 DEN（目录启用网络）和其他目录计划：

- ☐ http://www.dmtf.org/standards/standard_den.php
- ☐ http://www.opengroup.org/directory/ 目录互操作性论坛。请参见“白皮书”部分。

# SNMP

SNMP 的标准是：

- ☐ RFC-1157 1990年5月 *简单网络管理协议*

在加州大学戴维斯分校（UC Davis）进行了大量关于 SNMP 的工作。项目页面（以前位于 http://ucd-snmp.ucdavis.edu）已更名为 net-snmp，可在以下地址获取：

- ☐ http://net-snmp.sourceforge.net/

Stevens 的第 25 章提供了 SNMP 的良好概述。其他好书很难找到；许多书似乎正文内容很少，却拥有巨大的附录列出 MIB，而这些 MIB 最好保留在机器可读文件中。网络上可获取的“SNMP FAQ”不是一个好的介绍材料——你必须了解 SNMP 的内容，它才真正有用：

- ☐ ftp://rtfm.mit.edu/pub/usenet/comp.protocols.snmp/comp.protocols.snmp_SNMP_FAQ_Part_1_of_2
- ☐ ftp://rtfm.mit.edu/pub/usenet/comp.protocols.snmp/comp.protocols.snmp_SNMP_FAQ_Part_2_of_2

但上述 http://net-snmp.sourceforge.net/ 上关于 UC Davis 工具的 FAQ 很有帮助。这里有一个很棒的教程：

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

Windows-NT SNMP 工具包含在 NT 4.0 资源工具包中。这些包括基本但实用的 snmpmon 工具。它可以让你指定特定主机上的一组 SNMP 变量，并定期监控它们（获取其值）；你可以根据结果执行任意命令，例如发送警报或电子邮件，或者在机器磁盘空间不足时从目录中删除临时文件等。

许多系统和网络管理员从头编写自己的工具来监控和控制系统的各个方面（例如监控磁盘空间、检查网络连接等）。与其重新发明轮子，不如考虑使用 SNMP。最初这需要更多时间，但很快它就能为你节省大量时间，并使你的工具更具可移植性和更通用的实用性。

我们还没有涵盖 SNMP 陷阱（traps）。代理必须预先配置管理站的地址——没有发现机制使 SNMP“客户端”机器能够自动找到管理站。（但它可以通过 DHCP 进行配置。）在 NT 上，snmputil trap 监听陷阱消息。

SNMP 只有四个命令：get 和 set（我们已使用过），trap（我们在上文讨论过），以及最后的 get-next。get-next 返回指定变量之后的变量值（或 OID）。通过指定树的根节点并反复使用 get-next，你可以在不知道树中内容或结构的情况下检索整棵树。这是使 SNMP 如此强大的功能之一。它让你可以浏览 MIB 树并获取你感兴趣的任何信息。Linux 包含 snmpwalk 命令，它通过反复使用 get-next 来检索你指定的变量下方的子树中的所有值。下面，我们展示了 system 节点的 snmpwalk 输出。get-next 对于处理大小未知的数组也是必不可少的。

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

有一个名为 getif（“获取接口信息”）的图形化 SNMP 工具适用于 Microsoft Windows，可从以下地址获取：

- □ http://www.wtcs.org/snmp4tcp/

# Syslog

尽管 Syslog 非常古老，但它直到最近才被记录为 RFC：

- □ RFC-3164 2001年8月 BSD Syslog 协议

该协议提供了大量易于阅读的背景知识。syslog 及类似服务在日志记录和监控系统方面至关重要，但通过 UDP 传输的 Syslog 不会向发送者提供消息是否成功记录的反馈。最近的一个 RFC 规定了如何通过可靠的（TCP）连接运行 syslog，并增强数据完整性和安全性：

- □ RFC-3195 2001年11月 Syslog 的可靠传输

