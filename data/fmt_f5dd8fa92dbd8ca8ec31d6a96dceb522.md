
# 电子邮件服务器

从客户端下载电子邮件最常用的协议是邮局传输协议 (POP) 和互联网消息访问协议 (IMAP)。如果你将 Fedora 或 RHEL 配置为邮件服务器，你可以配置 `dovecot` 软件包来提供 POP 和 IMAP 服务。

`Dovecot` 是一个 IMAP/POP3 邮件服务器，支持 `maildir` 和 `mbox` 格式。如果你的用户从自己的桌面获取邮件，而不是在邮件服务器上运行客户端，则你使用 IMAP 或 POP3。默认情况下，所有 POP 或 IMAP 服务都是关闭的。从表 C-1 的电子邮件读取器列表中选择其中一个。

Fedora 和 RHEL 自带默认邮件传输代理是 `sendmail`。如果安装了 `sendmail` 软件，`sendmail` 服务将自动启动。然而，你必须配置 `/etc/mail` 目录中的各种文件以便该服务在本地之外工作。

`Postfix` 是 `sendmail` 的替代方案，`exim` 邮件传输代理也是如此。使用 `alternatives` 功能（在本附录早期和第 10 章描述），你可以轻松地将任何一个包设置为你的默认邮件传输代理。`postfix` 的配置文件位于 `/etc/postfix` 目录，而 `exim` 配置文件在 `/etc/exim` 目录。还要确保你关闭 `sendmail`（`chkconfig sendmail off`）并开启 `postfix` 或 `exim`（`chkconfig postfix on` 或 `chconfig exim on`）。

在 Fedora 和 RHEL 中可以开启 `cams` 服务来检查邮件何时到达用户的信箱。虽然 `cams` 默认关闭的，但如果你开启它，就可以可以使用 `biff` 或 `xbill` 命令在邮件到达信箱时提醒用户。要开启 `cams`，只需编辑 `/etc/inetd.d` 中的 `cams` 文件，将 `disable = yes` 条目改为 `disable = no`。

# 新闻服务器

Fedora 和 RHEL 带有互联网新闻服务器 (INN) 软件，让你可以将 Fedora 或 RHEL 系统设置为新闻服务器。INN 可以让你的用户访问成千上万个互联网新闻组。

# 录 C：运行网络服务

默认情况下，Fedora 和 RHEL 中的 INN 服务是关闭的。要启用它，请执行 `chkconfig inn on`。然后通过输入 `service inn start` 启动它。要使服务可用，你必须编辑 `/etc/news` 目录下的文件。

> 注意：由于新闻服务器可能会消耗大量的系统资源，你必须仔细考虑如何配置它。有关如何配置 INN 新闻服务器的详细信息，可以参考《Red Hat Fedora and Enterprise Linux 4 Bible》网站：www.wiley.com/go/fedorabible。

# 打印服务器

通用 打印系统 (`CUPS`) 打印服务器软件作为当前版本 Fedora 和 RHEL 的默认打印软件包含。作为替代方案，LPR 新一代 (`LPRng`) 软件仍然可用，但不再在 Fedora 或 RHEL 发行版中提供。

> 交叉引用：关于设置打印机的信息可以在第 17 章中找到。

通用 打印系统 (`CUPS`) 是最近开发的 `LPRng` 以及其他打印接口的替代方案，这些接口最初是基于 20 世纪 70 年代行字打印机的设施构建的。`CUPS` 基于 Internet 打印协议 (RFC 2616) 构建。尽管它与其他的 UNIX/Linux 打印设施兼容，但 `CUPS` 旨在让新的打印机、协议和其他设备在出现时更容易被支持。

`CUPS` 服务器 (`cupsd`) 默认已设置好。`CUPS` 的配置文件位于 `/etc/cups` 目录。

# 网络管理服务器

某些网络服务器提供监控或配置网络设置的服务。表 C-1 列出的其中几项服务在随后的章节中进行了了描述。

# 网络时间协议服务器

网络时间协议 (NTP) 同步网络上计算机之间的时间。

Fedora 和 RHEL 的首次启动允许你开启 NTP 服务。要调整 `ntp`，你必须编辑 `/etc/ntp.conf` 文件。`/etc/ntp.conf` 文件包含用于识别同步源地址和运行模式的信息。`/etc/ntp/keys` 文件可用于开启认证。

# Portmap 服务器

`portmap` 服务器将远程过程调用 (RPC) 编号转换为 TCP/UDP 端口号。某些网络服务（如 NFS (`nfs`) 和 Wall (`firewalld`)）只有在此服务器运行时才能正常工作。RPC 编号存储在 `/etc/rpc` 文件中。

# SWAT

Samba Web 管理工具 (`SWAT`) 提供了一个用于配置 Samba 文件和打印服务的 Web 界面。正确配置后，Web 浏览器可以访问 `SWAT` 服务（需要 root 用户密码）。尽管这是一个经过充分测试的界面，但 Samba 配置窗口是 Fedora 和 RHEL 中配置 Samba 的首选工具。

要启动该服务，编辑 `/etc/xinetd.d/swat` 文件，并将 `disable = yes` 条目修改为 `disable = no`。这使得本地主机上请求端口 `901`（例如 `http://localhost:901`）的 Web 浏览器可以使用该服务。你可以删除 `only_from = 127.0.0.1` 这一行，允许网络上任何可以访问你计算机的 Web 浏览器使用 `SWAT`。（当然，远程用户也需要知道你的密码。）

# Arpwatch 服务器

可以开启 `Arpwatch` 服务来监控网络上的以太网/IP 活动。任何潜在问题（例如两台不同的计算机使用相同的 IP 地址）都会记录到 syslog 设施中（通常到 `/var/log/messages` 文件）。

默认情况下，`Arpwatch` 服务是关闭的。要开启它，输入 `service chkconfig arpwatch start`。要启动该服务，你可以检查 `/var/log/messages` 文件查看 `Arpwatch` 服务是否成功启动，并观察网络上的变化。

# 简单网络管理协议服务器

简单网络管理协议 (SNMP) 允许你的 Fedora 或 RHEL 系统监听来自网络的 SNMP 请求。当此服务器运行时，其他使用 SNMP 工具的计算机就可以监控你计算机的活动（基于在你系统上设置的配置文件）。

默认情况下，SNMP 是关闭的。要开启它，输入 `chkconfig snmpd` 和 `chkconfig snmptrap on`。SNMP 配置可能非常复杂。请参考 `snmpd.conf` 的帮助页（输入 `man snmpd.conf`）。特别注意 SNMP 的安全问题。请参考 net-snmp 项目网站 (`http://net-snmp.sourceforge.net`) 获取教程和更多信息。

# 信息服务器

通过分发主机名、用户账户信息和网络地址等信息，管理员可以更容易地管理一组网络计算机。管理网络信息的流行服务器类型包括信息系统 (NIS)、动态主机配置协议 (DHCP) 和轻量级目录访问协议 (LDAP)。

# 网络信息系统服务器

网络信息系统 (NIS) 是由 Sun 开发的一种软件功能，用于管理配置网络上一组 UNIX（现在是 Linux）计算机所需的信息。通过 NIS，一组计算机可以共享公共 `passwd`、`groups`、`hosts` 以及其他配置文件。

默认情况下，NIS 服务是关闭的。你可以将 Linux 计算机作为 NIS 客户端（使用共享信息）或 NIS 服务器（分发共享信息）开启 NIS 服务。NIS 客户端计算机需要启动 `/etc/init.d/ypbind` 脚本并在 `/etc/yp.conf` 文件标识 NIS 服务器。

要将 Fedora 或 RHEL 作为 NIS 服务器，你必须收集想要共享的配置文件，启动 `/etc/init.d/ypserv` 脚本。该脚本运行 `/usr/sbin/ypserv` 守护进程，该守护进程负责向 NIS 客户端计算机分发信息。

# 动态主机配置协议服务器

动态主机配置协议 (DHCP) 用于自动配置网络上一组 UNIX（现在是 Linux）计算机所需的信息。通过 DHCP，一组计算机可以共享公共 IP 地址、网掩、网关等。

默认情况下，DHCP 是关闭的。为了让网络上的计算机自动获取配置，你可以在 Fedora 或 RHEL 上配置 DHCP 服务器。除了启动服务，你还需要配置 `/etc/dhcpd.conf` 文件。

# 轻量级目录访问协议服务器

如果你的组织使用轻量级目录访问协议 (LDAP) 数据库，运行 LDAP 服务器的 Fedora 或 RHEL 允许访问这些数据库。

默认情况下，LDAP 服务是关闭的。要开启它，输入 `ifconfig ldap`。要启动服务，输入 `service ldap`。除了启动脚本，你还需要配置 `/etc/ldap/`。

# 域名系统服务器

域名系统 (DNS) 服务器将 TCP/IP 网络上的主机名转换为 IP 地址。Fedora 和 RHEL 可以使用 `named` 守护进程配置 DNS 服务器。

默认情况下，DNS 服务器未在 Fedora 或 RHEL 中配置启动。要开启 DNS 服务器，输入 `chkconfig named`。要启动服务，输入 `service named`。除了启动服务，你必须配置 `/etc/named.conf` 文件和区域文件（位于 `/var/named` 目录）。

# 反向地址协议服务器

反向地址协议 (RARP) 守护进程响应请求 IP 地址的 RARP 客户端。今天，RARP 不经常使用。安装后，服务默认是关闭的。要开启 RARP 服务器，输入 `chkconfig rarpd on`。要启动服务，输入 `service rarpd`。当请求进入时，`/usr/sbin/rarpd` 守护进程会检查 `/etc/ethers` 或 NIS 数据库。

# 数据库服务

数据库服务器提供了访问和管理数据库数据库工具。Postgres 使用 `postmaster` 守护进程处理请求。MySQL 服务器运行 `mysqld` 守护进程来处理访问。这些守护进程通过 `/etc/init.d` 中的 `postgresql` 和 `mysql` 脚本分别启动。

> 交叉引用：第 24 章介绍了如何设置 MySQL 数据库服务器。

# 用户服务

Fedora 和 RHEL 可以为用户提供各种网络服务。这些服务允许运行远程程序、发送实时消息并获取活动用户的信息。

# 远程执行服务器

远程执行服务器响应其他计算机在本地计算机上运行命令的请求。这可能是一个安全问题，因此在配置这些服务时要小心。Fedora 和 RHEL 提供了三种远程执行服务守护进程：SSH、Rexec 和 Kshell。

- Rsh 服务 (`/usr/sbin/in.rsh`) 接受由 `rsh` 命令发起的远程执行请求。默认情况下，它是关闭的。在允许远程执行之前，主机用户（或双方）必须允许。访问通过 `/etc/hosts.equiv` 文件或每个用户家目录下的 `.hosts` 文件配置。

## 录 C：运行网络服务

- `rexec` 服务 (`/usr/sbin/in.rexcd`) 接受来自 `rexec` 命令（来自其他 Linux 或 UNIX 系统）的远程执行请求。默认情况下，该服务是关闭的。要允许远程执行，请求用户必须提供有效的用户名和密码。

- Kshell 服务 (`/usr/kerberos/kshd`) 接收来自 `rsh` 命令的远程执行请求。它使用 Kerberos 认证和加密，比 `rsh` 守护进程中的替代方案更安全。默认情况下，该服务是关闭的。但是，如果你开启它（通过编辑 `/etc/xinetd.d/kshd` 文件并将 `disable = yes` 条目改为 `disable = no`），它的优先级高于 `in.rsh` 守护进程。

之前描述的 OpenSSH（使用 `ssh` 守护进程）也可以用于远程执行。事实上，OpenSSH 被认为是比上述其他方法更安全的远程执行执行方式。

交叉引用：用于使用登录服务的登录命令在第 16 节中描述。

## Talk 服务器

`in.talk` 或 `in.ntalk` 服务器允许用户使用 `talk` 命令进行通信。`talk` 命令允许用户实时往返输入消息。`talk` 守护进程处理端口 517 的请求，`ntalk` 守护进程处理端口 518 的请求。

两个服务默认均关闭。要开启任一服务，请编辑 `/etc/xinetd.d/talk` 和/或 `/etc/xinetd.d/ntalk` 文件，并将 `disable = yes` 条目改为 `disable = no`。重启 `xinetd` 守护进程：`service xinetd restart`。

## Finger 服务器

`finger` (`/usr/sbin/in.fingerd`) 服务器允许人们使用 `finger` 命令请求有关 Linux 或 UNIX 系统或网络上活动用户的信息。该服务默认关闭的。如果 `in.finger` 服务器接受来自 `finger` 命令的请求，发送给请求用户的输出看起来如下所示：

```
