
rlogin 服务长期以来一直可以在 UNIX 系统上使用，尽管它通常比这里描述的其他登录服务安全性低。`rlogin` 服务在你的 Fedora Linux 系统上默认是关闭的。

Fedora Linux 可用登录服务器中一个较新的新增项是 OpenSSH 服务器。该服务默认开启。要访问此服务，请使用带有 `openssh-client` 软件软件包的应用程序，例如 `ssh`、`sftp` 和 `login remote` 命令。许多 Linux 管理员使用 OpenSSH 工具，而不是较旧的远程登录工具（如 `rlogin` 和 `telnet`），因为人们认为 OpenSSH 更安全。

> **警告：** SSH 服务不仅默认是开启的，而且与其他登录服务不同的是，它将允许通过网络进行 root 登录。如果你对这感到不安，你应该按照如下所示更改 `/etc/ssh/sshd_config` 文件中的 `PermitRootLogin` 行：

```
PermitRootLogin no
```

## 邮件服务器

从邮件服务器下载电子邮件到客户端工作站最常用的协议是邮局协议 (POP) 和互联网邮件组访问协议 (IMAP)。如果你将 Fedora Linux 配置为你的邮件服务器，你可以配置 `dovecot` 软件包来提供 POP 和 IMAP 服务。

`Dovecot` 是一个支持 `maildir` 和 `mbox` 格式的 IMAP/POP3 邮件服务器。如果你的用户从自己的桌面端获取邮件，而不是在邮件服务器上运行邮件客户端，则应使用 IMAP 或 POP。默认情况下，所有 POP 或 IMAP 服务都是关闭的。请从表 C-1 的邮件阅读器服务器列表中选择你想要使用的 POP 或 IMAP 服务器。

Fedora Linux 附带的默认邮件传输代理称为 `sendmail`。如果安装了 `sendmail`，`sendmail` 服务将自动启动。然而，为了让服务在本地之外运行，你必须配置 `/etc/mail` 中的各种文件。

`Postfix` 是 `sendmail` 的替代方案，以及 `Exim` 邮件传输代理。使用 `alternatives` 功能（在本附录前面的部分和第 10 章中描述），你可以轻松地将其中任何一个软件包设置为你的默认邮件传输代理。`postfix` 的配置文件位于 `/etc/postfix` 目录，而 `exim` 配置文件位于 `/etc/exim` 目录。此外，确保你关闭 `sendmail` (`chkconfig sendmail off`) 并开启 `postfix` (`chkconfig postfix` 或 `chkconfig on`)。

> 交叉引用：第 19 章包含了有关如何配置 `sendmail` 和 `postfix` 的详情。

可以开启 `conrad` 服务来检查电子邮件何时到达 Fedora Linux 用户的信箱。虽然 `conrad` 默认是关闭的，但如果你开启了它，就可以使用 `buff` 或 `xbind` 命令在邮件到达用户信箱时提醒用户。要开启 `conrad`，只需编辑 `/etc/xinetd` 中的 `conrad` 文件，将 `disable = yes` 更改为 `disable = no`。

## 新闻服务器

Fedora Linux 附带互联网新闻服务器 (`INN`)，让你可以将 Fedora Linux 系统设为新闻服务器。`INN` 可以为你的用户提供访问数千个新闻组的权限。

默认情况下，Fedora Linux 中的 `INN` 服务是关闭的。要开启它，执行 `chkconfig inn on`。要使该服务可用，你必须编辑 `/etc/news` 目录下的文件。

> 警告：由于新闻服务器可能会消耗大量的系统资源，你必须仔细考虑如何配置它。有关 `INN` 新闻服务器的详情可以在 Red Hat 网站获取。

## 打印机服务器

通用打印系统 (`CUPS`) 打印机软件作为当前 Fedora Linux 版本的默认打印软件包含在内。作为替代方案，新 LPR (`LPRng`) 仍然可用，但不再由 Fedora Linux 提供。

> 交叉引用：在第 17 章可以找到设置打印机的信息。

通用打印系统 (`CUPS`) 是 `LPRng` 以及其他为 20 世纪 70 年代行打印机构建的打印接口最近开发的替代方案。`CUPS` 基于互联网打印协议 (RFC 2616)。尽管它与其他 UNIX/Linux 打印设施兼容，但 `CUPS` 旨在更方便地支持不断出现的新打印机、协议和其他设备。

`CUPS` 服务器 (`cups`) 设置为默认运行。由于 `CUPS` 默认被配置为打印服务，如果你想将 `LPRng` 设置为计算机的默认打印机，请运行 `system-switch-printer` 命令。`CUPS` 的配置文件位于 `/etc/cups` 目录。

## 网络管理服务器

某些网络服务器提供监控或配置网络设置的服务。表 C-1 中列出的这些服务中的几种将在接后的章节中描述。

## 网络时间协议服务器

网络时间协议 (`NTP`) 服务器同步网络上计算机之间的时间。

Fedora Linux 引导过程允许你开启 `NTP` 服务。要进一步调整 `ntp`，你必须编辑 `/etc/ntp.conf` 文件。`/etc/ntp.conf` 文件包含标识同步资源地址和运行模式的信息。`/etc/ntp/keys` 文件可用于认证。

## 端口映射服务器

`portmap` 服务器将远程过程调用 (RPC) 数字转换为 TCP/IP 和 UDP 端口号。某些网络服务，如 NFS (`nfs`) 和 Wall (`rwall`)，只有在此服务器运行时才能正常工作。RPC 数字存储在 `/etc/rpc` 文件中。

## SWAT

Samba 网页管理工具 (`SWAT`) 为配置 Samba 文件和打印服务提供了基于 Web 的界面。在配置适当的情况下，可以使用 浏览器访问 `SWAT` 服务（需要 root 密码）。尽管这是一个经过测试的界面，但 Samba 服务器配置窗口是 Fedora Linux 中配置 Samba 的首选工具。

## 附录 C：运行网络服务 1023

在 Fedora Linux 中，默认 `SWAT` 服务是关闭的。要启用它，请编辑 `/etc/xinetd/swat` 文件并将 `disable = yes` 改为 `disable = no`。这将使得本地主机上请求端口 901 的 Web 浏览器（例如 `http://localhost:901`）可以使用该服务。你可以删除 `onlyfrom=127.0.0.1` 这一行，以便允许任何通过网络访问你计算机的计算机上的 Web 浏览器访问 `SWAT`。（当然，远程用户也需要知道你的 root 密码。）

## Arpwatch 服务器

可以开启 `Arpwatch` 服务来监控网络上的以太网/IP 活动。任何潜在的问题（例如，两台不同的计算机使用相同的 IP 地址）都会记录在 `syslog` 中（通常是 `/var/log/messages` 文件）。

默认情况下，`arpwatch` 服务是关闭的。要启用它，请使用 `chkconfig arpwatch on`。你可以检查 `/var/log/messages` 文件来查看 `Arpwatch` 服务是否成功启动，并观察网络的变化。

## 简单网络管理协议服务器

简单网络管理协议 (`SNMP`) 服务器允许你的 Linux 系统监听来自网络的 SNMP 请求。运行此服务器后，其他使用 SNMP 工具的计算机就可以监控你计算机的活动（基于在你系统上设置的配置文件）。

默认情况下，`SNMP` 是关闭的。要启用它，请使用 `chkconfig snmpd on` 和 `chkconfig snmptrap on`。`snmpd.conf` 配置可能非常复杂。请从参考 `snmpd.conf` 手页开始（输入 `man snmpd.conf`）。请特别注意 SNMP 的安全问题。参考 `net-snmp` 项目网站 (`http://net-snmp.sourceforge.net`) 获取教程和更多信息。

## 信息服务器

通过分发主机名、用户账户信息和网络地址，管理员可以轻松地管理一组网络计算机。管理网络信息的流行服务器类型包括网络信息系统 (`NIS`)、动态主机配置协议 (`DHCP`) 和轻量级目录访问协议 (`LDAP`)。

### 网络信息系统服务器

网络信息系统 (`NIS`) 是 Sun Microsystems 开发的一项软件功能，用于管理配置网络上组 UNIX（现在是 Linux）计算机所需的信息。使用 `NIS`，一组计算机可以共享通用的 `passwd`、`groups`、`hosts` 和其他配置文件。

默认情况下，`NIS` 服务是关闭的。你可以将 Linux 计算机配置为 `NIS` 客户端（使用共享信息）或 `NIS` 服务器（分发共享信息）来开启 `NIS` 服务。`NIS` 客户端计算机需要启动 `/etc/init.d/ypbind` 并在 `/etc/yp.conf` 文件中标识 `NIS` 服务器。

将 Fedora Linux 作为 `NIS` 服务器，你必须收集想要共享的配置文件，启动 `/etc/init.d/ypserv` 脚本。该脚本运行 `/usr/sbin/ypserv` 守护进程，该进程负责向 `NIS` 客户端计算机分发信息。

交叉引用：第 23 章描述了 `NIS` 客户端和服务器软件。

### 动态主机配置协议服务器

与其访问本地网络上的每台计算机并添加它们工作所需的所有 TCP/IP 信息（IP 地址、子网掩码、网关等），你可以将 Fedora Linux 配置为动态主机配置协议 (`DHCP`) 服务器来分发这些信息。客户端在启动网络连接时，只需识别 `DHCP` 服务器的 IP 地址，`DHCP` 服务器就会自动分配其网络地址。

默认情况下，`DHCP` 是关闭的。要启用它，输入 `chkconfig dhcpd on`。除了启动服务外，你必须配置 `/etc/dhcp.conf` 文件。

交叉引用：第 23 章描述了如何设置 `DHCP` 服务器。

### 轻量级目录访问协议服务器

如果你的组织使用轻量级目录访问协议 (`LDAP`) 数据库，运行 Fedora Linux 自带的 `LDAP` 服务器允许访问访问数据库。同样，`LDAP` 服务器允许你使用启用 `LDAP` 的应用程序，例如 Netscape Roaming Access 和 `sendmail 8`。

默认情况下，`LDAP` 服务是关闭的。要启用它，输入 `chkconfig ldap on`。除了运行启动脚本外，你必须配置 `/etc/ldap/` 目录下的文件。

交叉引用：第 22 章展示了使用 `LDAP` 设置电子邮件地址示例。

## 域名系统服务器

域名系统 (`DNS`) 服务器用于将 TCP/IP 网络上的主机名翻译为 IP 地址。可以使用 `named` 守护进程将 Fedora Linux 配置为 `DNS` 服务器。

默认情况下，Fedora Linux 中的 `DNS` 服务器未配置为自动启动。要启动 `DNS` 服务器，输入 `chkconfig named on`。除了启动服务外，你必须配置 `/etc/named.conf` 文件并在 `/var/named` 目录中配置区域文件。

## 反向地址解析协议服务器

反向地址解析协议 (`RARP`) 守护进程响应必须获取自身 IP 地址的 `RARP` 客户端请求。`RARP` 不经常使用。

默认情况下，`RARP` 服务是关闭的。要启动 `RARP` 服务器类型，输入 `chkconfig rarpd on`。当地址请求进来时，`/usr/sbin/rarpd` 守护进程会检查 `/etc/ethers` 或 `NIS` 数据库中的地址。

## 数据库服务

数据库服务器提供访问和管理信息数据库的工具。`Postgresql` 服务使用 `postmaster` 守护进程处理其服务的请求。`MySQL` 服务器使用 `mysqld` 守护进程处理对其数据库的访问。

## 用户服务

Fedora Linux 可以为用户提供各种网络服务。这些服务可以提供活动用户的信息。

### 远程执行服务器

远程执行服务器响应来自其他计算机命令请求。这些服务包括 `Rsh`、`Rexec` 和 `Kshell`。

- `Rsh` 服务 (`/usr/sbin/in.rsh`) 接受 Linux 或 UNIX 系统的请求。默认情况下服务是关闭的。要允许远程执行，必须许可主机。
- `Rexec` 服务 (`/usr/sbin/in.rexec`) 接受 Linux 或 UNIX 系统的请求。默认情况下服务是关闭的。提出请求的用户必须提供有效的用户名和密码。
- `Kshell` 服务 (`/usr/sbin/kshell`) 接收来自 `sh` 命令的请求。它使用 Kerberos 认证和加密，使其更安全。默认情况下服务是关闭的。但是如果你开启它（通过编辑 `/etc/xinetd/shell` 文件并将 `disable = yes` 改为 `disable = no`），之前介绍的 OpenSSH（使用 `sshd` 守护进程）也可以用于远程执行。`OpenSSH` 被认为是远程执行更安全的方法。

交叉引用：第 16 章描述了登录命令。

## Talk 服务器

使用 `in.talk` 或 `in.ntalk` 服务器允许用户使用 `talk` 命令通信。`talk` 命令允许用户实时打字。`talk` 守护进程处理端口 517，`ntalk` 守护进程处理端口 518。

两个服务器默认都关闭。要启用任何服务，编辑 `/etc/xinetd.d/talk` 和/或 `/etc/xinetd.d/ntalk` 文件，并将 `disable = yes` 条改为 `disable = no`。

## Finger 服务器

`finger` (`/usr/sbin/in.fingerd`) 服务器允许使用 `finger` 命令请求本地或网络上 Linux 或 UNIX 系统的活动用户信息。该服务默认关闭的。如果 `in.fingerd` 服务器接受来自 `finger` 命令的请求，向请求用户的输出如下：

```
[maple]

Login: jake             Name: Jake W. Jones

Directory: /home/jake    Shell: /bin/bash

Last login Mon Oct 14 13:34 (PDT) on pts/2 from maple

Mail last read Mon Oct 14 12:10 2000 (PDT)
```

输出显示用户的登录名、姓名、主目录和 shell。它还显示用户上次登录和访问邮箱的时间。

## 远程用户识别

`rusers` (`/usr/sbin/rpc.rusersd`) 允许从远程计算机查询系统列出当前登录到 Linux 系统的用户。可以使用 `rusers` 命令查询 `rpc.rusersd` 服务器。

默认情况下，`rusers` 服务是关闭的。要启动该服务，输入 `chkconfig rusersd on`。

# 全局广播服务器 (Write-to-All)

全局广播 (`rwall`) 服务器 (`/user/sbin/rpc.rwall`) 接受向当前登录到 Fedora Linux 或其他 UNIX 系统的所有用户屏幕广播文本消息的。该请求通过 `rwall` 命令发出。默认情况下，`rwall` 服务是关闭的。要启动 `rwall` 服务器，请输入 `chkconfig on rwall`。

# 安全服务

Fedora Linux 提供了某些服务来保护您的本地网络免受外部攻击。这些服务包括系统日志、虚拟专用网络服务器和缓存服务器。接下来的章节将介绍这些服务。

# 系统日志

虽然系统日志不是专门的网络服务，但系统日志设施 (`syslogd` 软件包）会记录计算机上大多数网络服务（以及其他服务）的运行和错误消息。系统日志守护进程 (`/sbin/syslogd`) 应该始终运行。

`syslog` 守护进程默认在所有多用户运行运行级别（2, 3, 4 和 5）下启动。你可以通过重新配置 `/etc/syslogd.conf` 文件来更改记录的消息类型或将消息重定向到不同的文件。你可以通过编辑 `/etc/sysconfig/syslog.file` 来更改 `syslog` 守护进程使用的选项。

# 虚拟专用网络服务器

通过对跨公共网络传输的数据进行加密，虚拟专用网络 (`VPN`) 可以为用户从远程位置访问本地网络提供安全方法。Fedora Core 1 带有 Crypto IP 封装 (`CIPE`) 虚拟专用网络软件。Fedora Core 2 包含了 IPSEC 虚拟专用网络服务。

> 交叉引用：有关 IPSEC 的更多信息请参见第 16 章。

# 代理/缓存服务器

`Squid` 服务器 (`/usr/sbin/squid`) 可同时用代理服务器和缓存服务器。代理服务器可以通过将所有请求通过代理服务器，允许本地网络上的计算机与互联网通信。缓存服务器将本地用户访问过的 Web 内容存储在物理位置比源计算机更用户的计算机上。

默认情况下，`Squid` 服务器是关闭的。要启动 `Squid` 服务器，请输入 `chkconfig squid on`。你还必须设置 `/etc/squid/squid.conf` 文件以识别谁可以访问服务器以及他们可以访问哪些服务。

> 交叉引用：第 16 章提供了配置 `Squid` 的详细信息。

# 1028 附录

| 特性 | Web 服务器 | Web 服务器 (Apache) | 文件服务器 | FTP 服务器 (Vs-ftpd) | 支持 Kerberos 的 FTP 服务器 (Gss-Ftp) | Samba Windows 文件和打印机 (SMB) | UNIX 网络文件系统 (NFS) | Apple Talk 文件和打印服务器 (Nettalk) | 网络服务器 (Mars-Iwe) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| | 软件包名称 | 启动脚本(s) | 守护进程 | 配置文件(s) | | | | | | |
| | | `/etc/init.d/httpd` | `/usr/sbin/httpd` | `/etc/httpd/conf/httpd.conf` | | | | | | |
| | `http-manual` | `/etc/init.d/tux` | `/usr/sbin/tux` | `/etc/sysconfig/conf/tux` | | | | | | |
| | `devel` | `/etc/init.d/tux` | `/usr/sbin/tux` | | | | | | | |
