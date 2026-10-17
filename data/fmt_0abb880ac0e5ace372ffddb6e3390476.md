
另一个流行的 FTP 服务器是 Trivial FTP (`tftp`)。`tftp` 通常用作如 Linux Terminal 服务器等项目的启动服务器。

交叉引用：有关如何配置 `vsftpd` FTP 服务器的信息，请参见第 20 节。

注意：Fedora 和 RHEL 还包含一个支持 Kerberos 5 的 FTP 服务器。`krb5-workstation` 包包含 Kerberos 5 支持的 `ftpd` 守护进程。`wu-ftp` 服务器不再于 Fedora 或 RHEL 发行版中。

## Samba 服务器

Samba 服务器支持 Server Message Block (`SMB`) 和 CIFS 文件及打印机共享协议。`SMB` 和 CIFS 通常用于运行 Microsoft Windows 的计算机本地网络共享资源。你通常不会在互联网等公共网络上使用 `SMB/CIFS` 文件和打印机。

## Web 服务器

大多数情况下，你使用 Apache 项目 (`httpd`) 在 Fedora 或 RHEL 中创建 Web 服务器。如果安装了 `httpd`，你必须开启服务并启动它。除非你为 Web 服务器有一个有效的名称（IP 地址），否则启动将失败。要定义服务器名称，需要在 `http.conf` 文件中添加 `ServerName` 条目并重启服务器。

默认情况下，从网络访问你的系统的用户将查看 `/var/www/html` 目录的内容。替换 `index.html` 文件并添加自己的内容。如果安装了 `httpd-manual` 包，`/var/www/manual` 包含 apache 手册。

交叉引用：有关配置 Apache Web 服务器的信息，请参见第 21 节。

# 附录 B：运行网络服务

在 Fedora 和 RHEL 中，Samba 服务默认禁用。要让 Samba 在计算机启动时自动启动，只需以 root 用户身份运行 `chkconfig smb as`。要立即启动服务，请使用 `service smb`。

为了让 Samba 可用，请编辑 Samba 配置文件 `/etc/samba/sm.conf`。配置此文件的简单方法是使用 Samba 服务器配置窗口（在第 18 节中描述）。

> 交叉引用：有关配置 Samba 的更多信息，请参阅第 17 节和第 18 节。

## Netalk 服务器

`netalk` 软件让 Linux 可以作为 Macintosh 计算机的 AppleTalk 使用。你必须安装 `netalk` 包并通过输入 `chkconfig atalk on` 来运行该服务。然后通过输入 `service netalk start` 启动服务。配置通过 `/etc/atalk` 目录下的文件完成。

> 交叉引用：有关设置 `netalk` 的信息请参阅第 26 节。

## 登录服务器

Fedora 和 RHEL 多种登录服务器。可以使用 `login` 和 `rlogin` 允许来自其他计算机的用户通过网络登录 Fedora 或 RHEL。如今，网络更倾向于使用 `sshd`（默认端口 22），你需要在防火墙中允许访问该服务。

如果安装了 `telnet-server` 包，`telnet` 服务默认禁用。如果启用它，`xinetd` 守护进程会将所有请求传递给 `telnet` 服务（默认端口 23），然后由 `telnetd` 守护进程显示 `telnet` 登录提示。一旦开启，只有对计算机拥有真实登录权限的用户才能登录——不支持匿名用户。使用登录服务器的用户将获得一个用于访问计算机的 shell 接口。

Fedora 和 RHEL 还包含提供 Kerberos 5 支持的登录守护进程。Kerberos 5 比其他登录服务器提供了更高级别的安全性。启用 Kerberos 5 的登录服务器包括 `Klogin` (Kerberos 5) 和 `EKlogin` (带加密的 Kerberos 5)。

登录服务在 UNIX 系统已已可用，尽管通常比上述描述的其他登录服务安全性低。在你的 Fedora 或 RHEL 系统上，登录服务默认禁用。

Fedora 和 RHEL 提供的登录服务器中较新的新增是 OpenSSH 服务器。它默认禁用。要访问此服务，请使用带有 `openssh-client` 软件包的应用程序，如 `ssh`、`sftp` 和 `login` 命令。许多 Linux 管理员使用 OpenSSH 工具，而不是 `telnet` 等远程登录工具。OpenSSH 更安全，因为它加密了网络流量以保护密码和数据不被嗅探（而 `telnet` 和 `login` 以明文发送数据）。

> 警告：不仅 SSH 会话默认是开启的，而且与其他登录服务不同，它允许通过网络进行 root 登录。如果你对此感到不安，应该按照如下所示修改 `/etc/ssh/sshd_config` 文件中的 `PermitRootLogin` 行：
```
PermitRootLogin no
```

## 电子邮件服务器

从邮件服务器到客户端工作站下载电子邮件的最常用协议是邮局传输协议 (`POP3`) 和互联网消息访问协议 (`IMAP4`)。如果你将 Fedora 或 RHEL 配置为你的邮件服务器，可以配置 `dovecot` 包来提供 POP 和 IMAP 服务。

`Dovecot` 是一个与 `maildir` 和 `mbox` 格式配合的 IMAP/POP3 邮件服务器。如果你的用户从自己的桌面端获取邮件，而不是在邮件服务器上运行客户端，则应使用 IMAP 或 POP3。默认情况下，所有 POP 和 IMAP 服务都是禁用的。从 B-1 列出的邮件阅读器服务器列表中选择你想要使用的 POP 或 IMAP 服务器。

Fedora 和 RHEL 自带的默认邮件传输代理是 `sendmail`。如果安装了 `sendmail`，`sendmail` 服务将自动启动。然而，你必须配置 `/etc/mail` 目录中的各种文件，该服务才能在本地之外工作。

`Postfix` 是 `sendmail` 的替代方案，它是导出邮件传输代理。通过替代方案功能（在本附录之前和第 10 节中描述），你可以轻松地将任何这些包设为你的默认邮件传输代理。`postfix` 的配置文件位于 `/etc/postfix` 目录，而配置文件位于 `/etc/exim` 目录。此外，确保你关闭 `sendmail`（`chkconfig sendmail off`）并开启 `postfix` 或 `exim`（`chkconfig postfix on` 或 `chkconfig exim on`）。

> 交叉引用：第 19 节包含了有关如何配置 `sendmail` 和 `postfix` 的细节。

## 新闻服务器

Fedora 和 RHEL 带有互联网网络新闻服务器 (`INN`) 软件，让你可以将 Fedora 或 RHEL 系统设置为新闻服务器。`INN` 可以让你的用户访问数以万个互联网新闻组。它也可以用作企业电子邮件存储库，以便工作组共享有关项目的信息。

默认情况下，Fedora 和 RHEL 中的 `INN` 服务是禁用的。要开启它，输入 `chkconfig inn on`。然后通过输入 `service inn start` 启动它。要使该服务可用，你必须编辑 `/etc/news` 目录中的文件。

> 警告：由于新闻服务器可能会消耗大量的系统资源，你必须仔细考虑如何配置它。有关如何配置自己的新闻服务器的详细信息可以从 Fedora 9 和红帽企业级 Linux 网站获取：`www.wiley.com/go/fedora9bible`。

## 打印服务器

通用 UNIX 打印系统 (`CUPS`) 打印服务器软件被作为当前 Fedora 和 RHEL 版本的默认打印软件包含在。作为替代方案，LPR 新一代 (`LPRng`) 服务器仍然可用，但不再由 Fedora 或 RHEL 发行版提供。

> 交叉引用：有关设置打印机的信息请参阅第 17 节。

通用 UNIX 打印系统 (`CUPS`) 是 `LPRng` 的替代方案，它是为了让打印机、协议和其他设备变得更容易设计的，基于 1970 年代的打印接口。`CUPS` 随着它们可用而变得可用。

`CUPS` 服务器是默认设置的。`CUPS` 的配置文件位于 `/etc/cups` 目录。

## 网络管理服务器

某些网络服务器监控或配置网络。表 B-1 中的这些服务将在后续章节中描述。

## 网络时间协议服务器

网络时间协议 (`NTP`) 服务器同步网络计算机之间的时间。

Fedora 和 RHEL 启动让你运行 `NTP` 服务。要进一步调整 `ntp`，你必须使用 `/etc/ntp.conf` 文件。`ntp.conf` 识别同步源和模式。`ntp/keys` 文件可用于认证。

## 端口映射服务器

`portmap` 服务器将远程过程调用 (`RPC`) 数字转换为 TCP/IP 数字。某些网络服务，如 NFS (`nfs`) 以及 Wall (`walld`)，只有当此服务器存储在 `/etc/rpc` 文件时才能正常工作。

## SWAT

Samba Web 管理工具 (`SWAT`) 提供了一个用于配置 Samba 和打印服务的 Web 接口。尽管这是一个测试良好的接口，但 Samba 配置窗口是首选工具。

默认情况下，`SWAT` 在 Fedora 和 RHEL 中是禁用的。要开启它，编辑 `/etc/inetd/swat` 文件并将 `disable = yes` 项改为 `disable = no`。这使得服务可以通过本地主机上的端口 901 访问（例如 `http://localhost:901`。（当然，远程用户需要知道你的 root 密码。）

## Arpatch 服务器

可以开启 Arpatch 服务以监控网络上的以太网/IP 活动。任何问题（例如两个计算机使用相同的 IP 地址）都会记录到 syslog 文件（通常是 `/var/log/messages` 文件）。

默认情况下，Arpatch 服务是禁用的。要开启它，输入 `chkconfig arpatch on`。然后通过输入 `service inn start` 启动它。你可以检查 `/var/log/messages` 文件查看 Arpatch 服务是否成功启动，并观察网络的变化。

## 网络管理协议服务器

简单网络管理协议 (`SNMP`) 服务器让你的 Fedora 或 RHEL 系统能够监听来自网络的 SNMP 请求。当此服务器运行时，使用 SNMP 工具的其他计算机可以监控你计算机的活动（基于系统上的配置文件）。

要使用 SNMP，请安装 `net-snmp` 包。默认情况下，SNMP 是禁用的。要开启它，输入 `chkconfig snmpd on`，`sntrap` 配置可能非常复杂。从参考 `snmpd.conf` 手册（输入 `man snmpd.conf`）。

## 信息服务器

通过分发主机名、用户帐户信息和网络地址，管理员可以轻松管理网络计算机。管理网络信息的常用服务器类型包括网络信息系统 (`NIS`)、动态主机配置协议 (`DHCP`) 和轻量级目录访问协议 (`LDAP`)。

## 网络信息系统服务器

网络信息系统 (`NIS`) 是由 Sun Microsystems 开发的一项软件功能，用于管理配置网络上一组 UNIX（现在是 Linux）计算机的配置。使用 `NIS`，一组计算机可以共享通用的 `passwd`、`groups`、`hosts` 以及其他配置文件。

默认情况下，`NIS` 服务是关闭的。你可以将你的 Linux 计算机的 `NIS` 服务配置为 `NIS` 客户端（共享信息）或 `NIS` 服务器（分发信息）。`NIS` 客户端需要启动 `/etc/init.d/ypbind` 脚本，并通过 `/etc/yp.conf` 文件识别 `NIS` 服务器。

要将 Fedora 或 RHEL 作为 `NIS` 服务器，你必须收集所有想要共享的配置文件，启动 `/etc/init.d/ypserv` 脚本。该脚本运行 `/usr/sbin/ypserv` 守护进程，由该进程负责向 `NIS` 客户端计算机分发信息。

## 动态主机配置协议服务器

你不需要访问局域网上的每台计算机并依次配置它们所需的所有 TCP/IP 信息（IP 地址、子网掩码、网关等），你可以将 Fedora 或 RHEL 配置为动态主机配置协议 (`DHCP`) 服务器，这样客户端在启动网络连接时只需识别 DHCP 服务器的 IP 地址，DHCP 服务器就会自动分配其网络地址。

默认情况下，`DHCP` 是关闭的。要开启它，输入 `chkconfig dhcp on`。然后输入 `service dhcpd start` 启动服务。除了启动服务外，你必须配置 `/etc/dhcpd.conf` 文件。

> 交叉引用：第 23 章描述了如何设置 DHCP 服务器。

## 轻量级目录访问协议服务器

如果你的组织使用轻量级目录访问协议 (`LDAP`) 数据库，运行 Fedora 或 RHEL 自带的 LDAP 服务器即可访问这些数据库。同样，LDAP 服务器允许使用支持 LDAP 的应用程序，例如 Netscape Roaming Access 和 `sendmail 8`。

默认情况下，LDAP 服务器是关闭的。要开启它，输入 `chkconfig ldap on`。输入 `service ldap start` 服务。除了运行启动脚本，还需要配置 `/etc/ldap/` 目录下的文件。

> 交叉引用：第 22 章展示了如何使用 LDAP 设置电子邮件地址簿。

## 域名服务器

域名系统 (`DNS`) 服务器用于将 TCP/IP 网络上的主机名翻译为 IP 地址。Fedora 和 RHEL 可以使用 `named` 守护进程配置为 DNS 服务器。

默认情况下，Fedora 或 RHEL 中的 DNS 服务器未配置为自动启动。要开启 DNS 服务器，输入 `chkconfig on`。输入 `service named start` 服务。除了启动服务外，你必须配置 `/etc/named.conf` 文件并配置区域（在 `/var/named` 目录中）。

## 反向地址解析协议服务器

反向地址解析协议 (`RARP`) 守护进程响应 RARP 客户端获取 IP 地址的请求。如今，RARP 不经常使用。

默认情况下未安装 RARP 包 (`rarp-ss98107`)。安装后，该服务是关闭的。要开启 RARP 服务器，输入 `chkconfig rarpd on`。输入 `service rarpd start` 启动服务。当地址请求进入时，`/usr/sbin/rarpd` 守护进程会检查 `/etc/ethers` 或 NIS+ 数据库。

## 数据库服务

数据库服务提供了访问和管理信息数据库的工具。`Postgresql` 使用 `postmaster` 守护进程处理其服务的请求。`MySQL` 服务器运行 `mysqld` 守护进程来处理对其数据库的访问。这些守护进程从 `/etc/init.d` 中的启动脚本启动，分别是为 `postgresql` 和 `mysql` 脚本。

> 交叉引用：第 24 章描述了如何设置 MySQL 数据库服务器。

## 用户服务

Fedora 和 RHEL 可以为终端用户提供各种网络服务。这些服务可以运行远程程序、实时发送消息并获取活动用户的信息。

## 远程执行服务器

远程执行服务器响应其他计算机在本地计算机上运行命令的请求。这可能引发安全问题，因此在配置这些服务时要小心。Fedora 和 RHEL 提供了三种远程执行守护进程：Rsh、Rexec 和 Shell。

- Rsh 服务 (`/usr/bin/in.rsh`) 接受由 `rsh` 命令（来自其他 Linux 或 UNIX 系统）发起的远程执行请求。默认情况下，该服务是关闭的。在允许远程执行之前，必须允许主机或用户（或两者都）访问。访问在 `/etc/hosts.equiv` 文件或每个用户家目录下的 `.rhosts` 文件中配置。

- Rexec 服务 (`/usr/sbin/in.rexec`) 接受来自 `rexec` 命令（来自其他 Linux 或 UNIX 系统）的远程执行请求。默认情况下，该服务是关闭的。要允许远程执行，请求的用户必须提供有效的用户名和密码。

- Kshell 服务 (`/usr/kerberos/sbin/kshd`) 接收来自 `rsh` 命令的远程执行请求。它使用 Kerberos 认证和加密，比 `.rshd` 守护进程的替代方案更安全。该服务是关闭的。但如果你通过编辑 `/etc/xinetd.d/ksh` 将 `disable = yes` 条目改为 `no`，它的优先级高于 `.rshd` 守护进程。

之前描述的 OpenSSH 服务（使用 `sshd` 守护进程）也可以用于远程执行。

## Talk 服务器

`talk` 服务允许用户进行实时通信。`talk` 守护进程处理端口 51 消息。默认情况下，该服务是关闭的。要开启它，输入 `chkconfig on`。输入 `service talk start` 服务。除了启动服务外，你必须配置 `/etc/motd` 文件。

## Finger 服务器

`finger` 服务 (`/usr/sbin/in.finger`) 让用户获取 Linux 或 UNIX 系统上活动用户的信息。默认情况下，该服务是关闭的。输出如下：
