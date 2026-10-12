
`password.` 使用 `salt-key` 方法，`crypt` 可以加密某些 4096。遗憾的是，这并不足够。使用 `password` 字典，攻击者可以强制执行相同的操作。最终，所有 4096 组合都将被尝试，密码可能会被破解。因此，你的密码应该始终受到保护。`shadowing` 被用于这种技术，向未授权的用户隐藏密码。要了解更多信息，请参见第 5 章“密码攻击”，以及附录中的 `password` 帮助页。

# ctrlaltd

**Description:** 设置 Ctrl+Alt+Delete 功能。
**Security Relevance:** `ctrlaltd` 允许你指定 Ctrl+Alt+Delete 序列。正常情况下，这将在系统同步同步数据。由于这种操作可能会导致数据丢失，在执行之前，请格外小心验证你的选择。磁盘分区错误可能会导致你的系统无法运行，你将被迫重新安装。要了解更多信息，请参见第 21 章“灾难恢复”，或 `ctrlaltd` 帮助页![](img/238ef1f85709de1ba6734ee37600.png)

# Dante (An Add-On)

**Description:** SOCKS 工具。
**Security Relevance:** `Dante` 是一个免费的电路级防火墙/代理实现。SOCKS 是一种防止外部人员与内部人员直接连接的协议。相反，SOCKS 服务器以间接的方式转发流量，从而防止渗透网络。要了解更多信息，请参见第 18 章“防火墙”。

# Deception Toolkit (An Add-On)

**Description:** 用于欺骗攻击者的工具。
**Security Relevance:** 近年来，关于欺骗有许多研究——通过模拟其他操作系统和并不存在的漏洞来欺骗攻击者。`Deception Toolkit` 提供了实现这些工具。要了解更多信息，请参见第 20 章“入侵检测”。

# DOC (Domain Obscurity)

**Description:** DNS 扫描器。
**Security Relevance:** `DOC` 扫描可能的配置错误或故障。要了解更多信息，请参见第 8 章。

# dns_lint (An Add-On)

**Description:** DNS 数据库调试器。
**Security Relevance:** `dns_lint` 自动检查 DNS 数据库的一一致性、配置问题和可疑条目。要了解更多信息，请参见第 8 章。

# dnswalk (An Add-On)

**Description:** DNS 数据库调试器。
**Security Relevance:** `dnswalk`（一个 Perl 脚本）自动遍历你的 DNS 数据库，检查一致性、配置问题和可疑条目。要了解更多信息，请参见第 8 章。

# Ethereal (An Add-On)

**Description:** 网络协议分析器。
**Security Relevance:** `Ethereal` 是一个基于 GUI 的数据嗅探器，支持 ARP、BOOTP/DHCP、DNS、Ethernet、ICMP、IGMP、IP/TCP/UDP、IPX、LPR/LPD、OSPF、PPP 和 Token Ring。要了解更多信息，请参见第 7 章“嗅探器与窃听”。

# exports

**Description:** 导出的文件系统。
**Security Relevance:** NFS 代表网络文件系统，允许你从远程主机导入文件。这些文件就像安装在本地机器上一样。通常，你应该尽可能少地导出文件系统。除非运行 NFS，否则将其关闭。NFS 引入了许多安全问题，因为攻击者可以轻松获取导出文件系统的列表。要了解更多信息，请参见第 3 章“安装问题”。此外，参见附录中的 `showmount` 帮助页。

# exscan (An Add-On)

**Description:** 识别特定发行版的端口扫描器。
**Security Relevance:** `exscan` 扫描 TCP/IP 端口以寻找可用服务。然而，与简单的端口扫描器不同，`exscan` 不仅识别监听服务，还能识别远程主操作系统。要了解更多信息，请参见第 8 章。

# FakeBO (An Add-On)

**Description:** 欺骗工具。
**Security Relevance:** `FakeBO` 是一个让人们认为你很糟糕（但实际上并没有）的工具。它误导攻击者，认为你的系统被植入了 BackOrifice 或 NetBUS 木马。要了解更多信息，请参见第 6 章“恶意代码”。

## fdisk

**Description:** Linux 分区表操作器。
**Security Relevance:** 虽然 `fdisk` 不是一个安全相关的命令，但你应该谨慎使用它。在对磁盘进行分区时，在提交之前要格外小心验证你的选择。分区错误可能导致系统无法运行，你将被迫重新安装。要了解更多信息，请参见第 3 章“安装问题”，或 `fdisk` 帮助页。此外，请与附录中的 `cfdisk` 进行对比。

# finger

**Description:** `finger` 报告目标的用户名、最后登录日期、主目录、办公室电话、真实姓名以及目标阅读邮件。语法通常为 `finger user@host`（除非你在 localhost 上，此时语法为 `finger user`）。以下是示例输出：

Login name: unown In real life: U. N. Owen
Directory: /home/owner
Shell: /bin/sh
On since Feb 3 18:13:14 on pts/15 from ppp-199
Mail last read Feb 3 18:01:22

**Security Relevance:** 遗憾的是，`finger` 还会返回特殊用户的信息。你不希望外部人员获取这些信息，因为他们可以使用它收集情报。禁用 `finger` 或运行一个安全的 finger 服务器。要了解更多信息，请参见第 3 章“安装问题”、第 14 章“服务器安全”，以及 `finger` 帮助页。此外，参见附录中的 `finger`。

# fingerd

**Description:** `fingerd` 为本地和远程用户提供信息，包括目标的用户名、最后登录日期、主目录、办公室电话、shell、真实姓名等。
**Security Relevance:** 你应该禁用 `finger`，因为它向外部人员泄露用户信息。要了解更多信息，请参见第 3 章“安装问题”、第 14 章“服务器安全”，以及 `finger` 帮助页。此外，参见附录中的 `finger`。

# fthosts

**Description:** `ftpd` 个用户主机访问文件。
**Security Relevance:** `fthosts` 是一个基于允许/拒绝原则的 `ftpd` 访问控制文件。根据用户名、主机名和 IP 地址允许或拒绝用户访问。（支持通配符和掩码。）要了解更多信息，请参见第 11 章“FTP 安全”，或 `fthosts` 帮助页。此外，参见附录中的 `ftpd` 和 `ftpusers`。

# ftpass

**Description:** `ftpd` 配置文件。
**Security Relevance:** `ftpass` 文件用于指定允许的 FTP 会话数、基于源地址的用户类别、允许失败登录次数以及欢迎信息（根据用户类别动态显示）。要了解更多信息，请参见第 11 章“FTP 安全”，或 `ftpass` 帮助页。此外，参见附录中的 `ftpd`、`fthosts` 和 `ftpusers`。

# ftputsh

**Description:** 在指定时间关闭 FTP 服务器。
**Security Relevance:** `ftputsh` 允许你按需要关闭 FTP 服务器并向当前登录的 FTP 用户发送警告。默认情况下，该过程在实际关闭前 10 分钟开始。此时，所有新的 FTP 流量将被拒绝。五分钟后，登录的 FTP 用户将被断开。要了解更多信息，请参见第 11 章“FTP 安全”，或 `ftputsh` 帮助页。

# GNU Privacy Guard (插件)

描述：一种 PGP 工具。
安全相关性：GNU Privacy Guard 是一个免费、无限制的 PGP（良好的隐私）工具，提供可以插入脚本和应用程序中的高级加密功能。

# halt

描述：停止系统。
安全相关性：`halt`（类似于 `reboot`）将停止或重启系统。这由你决定。通常情况下，你应该使用 `shutdown`。更多信息，请参阅第 4 章“Linux 基础系统管理”或 `halt` 手册页。此外，请对比本附录中的 `shutdown`。

# hosts_access

描述：`hosts_access` 是一种用于控制访问服务器访问的系统和语言。
安全相关性：`hosts_access` 规则基于允许/拒绝原则。你可以在 `/etc/hosts.allow`（允许访问）和 `/etc/hosts.deny`（拒绝访问）中编写你的规则。使用这些规则，你可以根据主机名或 IP 地址（支持通配符掩码）授予或拒绝客户端的访问。更多信息，请参阅第 14 章“Web 服务器安全”和第 18 章“Linux 与防火墙”。另见本附录中的 `tcpd`、`tcpchk`、`tcpdmatch` 和 `hosts_options`，或 `hosts_access` 手册页。

# hosts_options

描述：`hosts_options` 提供了控制服务器访问的可选扩展。
安全相关性：`hosts_options` 是 `hosts_access` 的扩展，`hosts_access` 是一种控制 Linux 服务器访问的语言。扩展功能包括执行 shell 命令、操作环境变量等。更多信息，请参阅第 14 章“Web 服务器安全”和第 18 章“Linux 与防火墙”。另见本附录中的 `tcpd`、`tcpchk`、`tcpdmatch` 和 `hosts_access`，或 `hosts_options` 手册页。

# hosts.equiv

描述：受信远程主机和用户数据库。
安全相关性：`hosts.equiv` 文件是你指定受信远程主机和用户条目的地方。一旦这些人在 `hosts.equiv` 中有了条目，他们就可以在无需密码的情况下 `rlogin`。

# 附录
第五部分

文件看起来大致如下：

hacker1 bozo
hacker2
hacker3 dominari

格式为 `host/user`。除非你有充分理由允许通过 r 命令（本附录中的 `rsh, login`）进行访问，否则你不应该维护 `hosts.equiv` 条目。它们存在安全风险。然而，如果你需要允许此类访问，请将其限制在你的域内的主机上。此外，确保该文件没有元字符（-,, !, 1, @, #, S, %, &, *, +, -）并由 `root` 所有。更多信息，请参阅第 14 章“Web 服务器安全”。另见本附录中的 `rsh, login` 或 `hosts.equiv` 手册页。

# HUNT 插件

**描述：**一种通用攻击工具。
**安全相关性：**`HUNT` 是一个提供丰富攻击手段的工具，包括会话劫持、ARP Relay、DoS 等。更多信息请参阅第 17 章“拒绝服务攻击”。

# htpasswd

**描述：**操作 HTTP 服务器密码文件。
安全相关性：使用 `htpasswd` 建立 Web 用户名和密码。`htpasswd` 对用户密码应用 UNIX 风格加密并将这些加密值输出到纯文本文件 `.htpasswd` 中。要在你的网站上实现 `htpasswd` 密码保护，你必须首先配置 `.htaccess` 中的选项，`.htaccess` 是一个包含有效用户名、`.htaccess` 路径、身份验证方法以及允许/拒绝方法的纯文本文件。每次访问受保护页面时，服务器都会查询 `.htaccess` 和 `.htpasswd`。更多信息，请参阅第 14 章“Web 服务器安全”、本附录中的 `htpasswd` 和 `.htaccess` 或 `htpasswd` 手册页。

# httpd

**描述：**Apache 超文本传输协议服务器。
安全相关性：`httpd` 是你的 Web 服务器，默认在启动时运行。`httpd` 配置涉及多个文件，包括：

* `access.conf`—访问配置文件，你在其中指定谁可以访问服务器、他们可以访问哪些目录，以及他们可以使用什么方法来保护该访问。
- `httpd.conf`—服务器配置文件，你在其中指定 `httpd` 的端口、用户 ID、组、根目录和管理员电子邮件地址，以及服务器是独立运行还是由 `inetd` 启动。

## Linux 安全命令参考

# 附录 A

- `srm.conf`—服务器资源映射，你在其中指定根文档目录扩展名（通常为 `/var/http/mydomain`）、用户目录、脚本目录、mime 类型和扩展、重定向（称为移动的页面）等。

你可以使用随附的实用程序通过基础认证或加密认证来控制用户访问。更多信息，请参阅第 14 章“Web 服务器安全”或 `http` 手册页。另见本附录中的 `httppasswd`。

# icmpinfo (插件)

描述：一种 icmp 分析器。
安全相关性：攻击者可以使用控制消息协议（CMP）对你的主机进行轰炸并暂时切断网络连接。要检测、捕获并记录此类攻击，请使用 `icmpinfo`。更多信息请参阅第 7 章“嗅探与电子窃听”。

# inetd

描述：TCP/IP IDENTENT 协议服务器。
安全相关性：`inetd` 实现标识协议（Identification Protocol），它可以识别特定 TCP 连接的用户。它会提取请求方的用户名，这在跟踪进程顺序时非常有用。`inetd` 并不完全可靠——攻击者可以报告错误或误导信息——但在某些情况下非常有帮助。

# inetpscan (插件)

描述：一种识别守护进程的扫描器。
安全相关性：大多数简单的扫描器都能识别守护进程，但 `inetpscan` 可以。更多信息请参阅第 8 章“扫描器”。

# inetd.conf

描述：Internet 服务器数据库。
安全相关性：`inetd.conf` 包含了默认启动的服务器列表。以下是一个精简的 `inetd.conf` 示例：

```
