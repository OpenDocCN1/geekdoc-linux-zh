
通常不建议在公共网络（如互联网）上共享 SMB/CIFS 文件和打印机。

Fedora 中的 Samba 服务默认是关闭的。若要让 Samba 在计算机启动时自动运行，请以 root 用户身份输入 `chkconfig smb on`。若要立即启动该服务，请输入 `service smb start`。

为了让 Samba 发挥作用，需要编辑 Samba 配置文件 `/etc/samba/smb.conf`。配置此文件的一个简便方法是使用 Samba 服务器配置窗口（在第 17 章中有详细描述）。

**交叉引用：** 有关配置 Samba 的更多详细信息，请参阅第 16 章和第 17 章。

## 登录服务器

Fedora 可以使用多种登录服务器。telnet 和 rlogin 服务均可用于允许来自其他计算机的用户通过网络登录到 Fedora。然而，由于这些服务存在安全顾虑，如今更推荐的登录服务是 `sshd`。对于其中任何一种服务，您都需要记得在防火墙中允许对该服务的访问。

如果已安装 telnet-server 软件包，则 telnet 服务默认处于关闭状态。如果启用了 telnet，`xinetd` 守护进程会将所有针对 telnet 服务的请求（默认为端口 23）传递给 `in.telnetd` 守护进程，以显示 telnet 登录提示。一旦开启，只有拥有真实登录账户的用户才能登录计算机——不支持匿名用户。使用 telnet 登录的用户将获得一个 shell 界面以访问计算机。

Fedora 还包含支持 Kerberos 5 的登录守护进程。与其他登录服务器相比，Kerberos 5 提供了更高程度的安全性。启用 Kerberos 5 的登录服务器包括 Klogin（Kerberos 5）和 ELKlogin（带加密的 Kerberos 5）。

rlogin 服务在 UNIX 系统上已经可用很长时间了，尽管它的安全性低于此处描述的其他登录服务。在您的 Fedora 系统上，rlogin 服务默认是关闭的。

Fedora 可用的登录服务器中较新的一个增加项是 OpenSSH 服务器。该服务默认是开启的。要访问此服务，请使用随 openssh-client 软件包一起提供的应用程序，例如 `ssh`、`sftp` 和 `rlogin` 远程登录命令。许多 Linux 管理员倾向于使用 OpenSSH 工具，而非 `rlogin` 和 `telnet` 等较旧的远程登录工具。OpenSSH 更加安全，因为它加密网络流量，以保护密码和数据不被嗅探（而 `telnet` 和 `rlogin` 以明文形式发送数据）。此外，`ssh` 提供了比 `telnet` 或 `rlogin` 更健壮的认证方式。您可以按组限制登录，或使用共享密钥以获得更多控制。

> **注意：** SSH 服务不仅默认是开启的，而且与其他登录服务不同，它允许通过网络进行 root 登录。如果您对这一点感到不安，应修改 `/etc/ssh/sshd_config` 文件中的 `PermitRootLogin yes` 一行，如下所示：
>
> `PermitRootLogin no`

## 电子邮件服务器

从邮件服务器下载电子邮件到客户端工作站最常用的协议是邮局协议（POP3）和互联网消息访问协议（IMAPv4）。如果您将 Fedora 配置为邮件服务器，可以配置 dovecot 软件包以提供 POP 和 IMAP 服务。

Dovecot 是一个支持 maildir 和 mbox 格式的 IMAP/POP3 邮件服务器。如果用户是从他们自己的桌面获取邮件，而不是在邮件服务器上运行邮件客户端，则使用 IMAP 或 POP3。默认情况下，所有 POP 或 IMAP 服务都是关闭的。请从表 B-1 中的电子邮件阅读器服务器列表中，选择您要使用的 POP 或 IMAP 服务器。

Fedora 自带的默认邮件传输代理（Mail Transfer Agent, MTA）称为 sendmail。如果安装了 sendmail 软件，sendmail 服务会自动启动。但是，为了让该服务在 localhost 之外工作，您必须配置 /etc/mail 目录中的各种文件。

Postfix 是 sendmail 的替代方案，exim 邮件传输代理也是如此。使用替代方案功能（在本附录和第 9 章中均有描述），您可以轻松地将这些软件包中的任何一个设置为您默认的邮件传输代理。postfix 的配置文件位于 /etc/postfix 目录，而 exim 的配置文件位于 /etc/exim 目录。此外，请确保关闭 sendmail（`chkconfig sendmail off`）并开启 postfix 或 exim（`chkconfig postfix on` 或 `chkconfig exim on`）。（如果用 postfix 替换 sendmail，请考虑完全移除 sendmail 软件包。）

> **交叉引用：** 第 18 章包含有关如何配置 sendmail 和 postfix 的详细信息。

## 新闻服务器

Fedora 附带互联网新闻服务器（INN）软件，让您可以将 Fedora 系统设置为新闻服务器。INN 是 inn 软件包的一部分，它可以为您的用户提供访问成千上万个互联网新闻组的机会。它也可以用作企业电子邮件存储库，以便工作组可以共享有关项目的信息。

默认情况下，Fedora 中的 INN 服务是关闭的。要开启它，请输入 `chkconfig innd on`。然后输入 `service innd start` 来启动它。为了使该服务可用，您必须编辑 /etc/news 目录中的文件。

## 打印服务器

通用 UNIX 打印系统（CUPS）打印服务器软件作为当前版本 Fedora 的默认打印机软件包含在内。作为替代方案，LPR 新一代（LPRng）软件仍然可用，但不再随 Fedora 发行版提供。

通用 UNIX 打印系统（CUPS）是 LPRng 和其他基于 1970 年代最初为行式打印机设计的功能构建的打印接口的替代方案。CUPS 基于互联网打印协议（RFC 2616）。尽管它与其他 UNIX/Linux 打印功能兼容，但 CUPS 旨在使支持新打印机、协议和其他设备变得更加容易，随着这些设备的出现。

CUPS 服务器（`cupsd`）默认设置为运行。CUPS 的配置文件位于 /etc/cups 目录中。

## 网络管理服务器

一些网络服务器提供监控或配置网络环境的服务。表 B-1 中列出的这些服务中有几个将在以下部分中描述。

### 网络时间协议服务器

网络时间协议（NTP）服务器在计算机网络中的计算机之间同步时间。

Fedora 的 firstboot 过程允许您开启 NTP 服务。为了进一步调整 ntp，您必须编辑 `/etc/ntp.conf` 文件。`/etc/ntp.conf` 文件包含标识同步源地址和运行模式的信息。`/etc/ntp/keys` 文件可用于开启身份验证。

### Portmap 服务器

portmap 服务器将远程过程调用（RPC）编号转换为 TCP/IP 和 UDP 端口号。某些网络服务，如 NFS（`nfs`）和 Wall（`walld`），只有在该服务器运行时才能正常工作。RPC 编号存储在 `/etc/rpc` 文件中。

### SWAT

Samba Web 管理工具（SWAT）提供了一个基于 Web 的界面，用于配置 Samba 文件和打印服务。安装 `samba-swat` 软件包以使用此界面。正确配置后，Web 浏览器可以访问 SWAT 服务（需要 root 用户密码）。尽管这是一个经过良好测试的界面，但 Samba 服务器配置窗口是 Fedora 中配置 Samba 的首选工具。

默认情况下，Fedora 中的 SWAT 服务是关闭的。要开启该服务，请编辑 `/etc/xinetd.d/swat` 文件并将 `disable = yes` 条目更改为 `disable = no`。这使得本地主机上请求端口号 901 的 Web 浏览器可以使用该服务（例如，`http://localhost:901`）。您可以删除 `only_from = 127.0.0.1` 这一行，以允许网络上任何能够访问您计算机的计算机上的 Web 浏览器使用 SWAT。（当然，远程用户还需要知道您的 root 密码。）

### Arpwach 服务器

Arpwach 服务（`arpwatch` 软件包的一部分）可以开启以监控您网络上的以太网/IP 活动。任何潜在问题（例如两台不同的计算机使用相同的 IP 地址）都会记录到 `syslog` 设施（通常是 `/var/log/messages` 文件）。

默认情况下，Arpwach 服务是关闭的。要开启它，请输入 `chkconfig arpwach on`。要启动该服务，请输入 `service arpwach start`。您可以检查 `/var/log/messages` 文件以查看 Arpwach 服务是否成功启动，并观察您网络上的变化。

> **注意：** 由于 Arpwach 希望监控网络活动，因此会产生 SELinux 错误。您可以决定是否启用 arpwach 运行。

### 简单网络管理协议服务器

简单网络管理协议（SNMP）服务器使您的 Fedora 系统能够监听来自网络的 SNMP 请求。有了这个服务器，其他使用 SNMP 工具的计算机可以监控您计算机的活动（基于在您系统上设置的配置文件）。

要使用 SNMP，必须安装 `net-snmp` 软件包。默认情况下，SNMP 是关闭的。要开启它，请输入 `chkconfig snmpd on` 和 `chkconfig snmptrapd on`。SNMP 配置可能相当复杂。首先请参考 `snmpd.conf` 手册页（输入 `man snmpd.conf`）。请注意，SNMP 可以揭示关于 Linux 系统的很多信息，包括哪些进程正在运行、磁盘空间的大小、挂载了哪些磁盘等。请务必小心 SNMP 的安全问题。

## 信息服务器

通过分发光如主机名、用户账户信息和网络地址等信息，管理员可以更轻松地管理一组联网计算机。用于管理网络信息的流行服务器类型包括网络信息系统（NIS）、动态主机配置协议（DHCP）和轻量级目录访问协议（LDAP）。

