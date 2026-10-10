
# 电子邮件服务器

从邮件服务器下载电子邮件到客户端工作常用的协议是邮局协议 (`POP3`) 和互联网消息访问协议 (`IMAP4`)。如果你将 `Fedora` 或 `RHEL` 配置为你的邮件服务器，你可以配置 `dovecot` 包提供 `POP` 和 `IMAP` 服务。

`Dovecot` 是一个支持 `maildir` 和 `mailbox` 格式的 `IMAP`/`POP3` 邮件服务器。如果用户从自己的桌面获取邮件而不是在邮件服务器上运行邮件客户端，则使用 `IMAP` 或 `POP3`。默认情况下，所有 `POP` 或 `IMAP` 服务都是关闭的。请从表 `B-1` 中的电子邮件读取器列表中选择你想要使用的 `POP` 或 `IMAP` 服务器。

`Fedora` 和 `RHEL` 自带的默认邮件传输代理称为 `sendmail`。`sendmail` 软件已安装，`sendmail` 服务自动启动。然而，你必须配置 `/etc/mail` 目录中的各种文件以便服务超出主机工作。

`Postfix` 是 `sendmail` 的替代方案，`exim` 邮件传输代理也是。使用替代功能（在本附录较早部分和第 10 章中描述），你可以轻松地将任何邮件传输代理设置为默认。

## 1018 附录 B：运行网络服务

这些软件包是您的默认邮件传输代理。`postfix` 的配置文件位于 `/etc/postfix` 目录，而 `exim` 的配置文件位于 `/etc/exim` 目录。此外，请确保已关闭 `sendmail`（`chkconfig sendmail off`）并开启 `postfix` 或 `exim`（`chkconfig postfix off` 或 `chkconfig exim on`）。

> 交叉引用：第 19 章包含了如何配置 `sendmail` 和 `postfix` 的详细信息。

# 新闻服务器

`Fedora` 和 `RHEL` 附带互联网网络新闻服务器 (`INN`) 软件，让您将 `Fedora` 或 `RHEL` 系统设置为新闻服务器。`INN` 可以让您的用户访问成千上万个新闻组。它也可以作为企业存储库，供工作组共享项目信息。

默认情况下，`Fedora` 和 `RHEL` 中的 `inn` 服务是关闭的。要开启它，请输入 `chkconfig inn on`。然后通过输入 `service inn start` 启动。要使该服务可用，您必须编辑 `/etc/news` 目录中的文件。

> 注意：由于新闻服务器可能会消耗大量的系统资源，您必须仔细考虑如何配置它。有关如何配置 `INN` 新闻服务器的详情请访问 `Fedora 8` 和 `Red Hat Enterprise Linux` 网站：`www.wiley.com/go/fedora8bible`。

# 打印服务器

通用 Unix 打印系统 (`CUPS`) 打印服务器软件已作为 `Fedora` 和 `RHEL` 当前版本的默认打印软件包含在内。作为替代方案，新一代 `LPR` (`LPRng`) 仍然可用，但不再由 `Fedora` 或 `RHEL` 发行版提供。

> 交叉引用：有关设置打印机的信息可以在第 17 章中找到。

通用 Unix 打印系统 (`CUPS`) 是 `LPRng` 以及其他打印接口的替代方案，这些接口最初是为 20 世纪 70 年代的行打印设计的。`CUPS` 基于互联网打印协议 (`RFC 2616`)。尽管兼容其他 `Unix/Linux` 打印设施，但 `CUPS` 旨在更容易地支持随之出现的新打印机、协议和其他设备。

`CUPS` 服务器 (`cupsd`) 默认设置为运行。`CUPS` 的配置文件位于 `/etc/cups/` 目录。

# 网络管理服务器

某些网络服务器提供监控或配置网络设置的服务。表 `B-1` 中列出的这些若干服务在随后的章节中进行了描述。

## 附录 B：运行网络服务 1019

### 网络时间协议服务器

网络时间协议 (`NTP`) 服务器同步网络上计算机之间的时间。
`Fedora` 和 `RHEL` 的首次启动过程允许您开启 `NTP` 服务。要进一步调优 `ntp`，您必须编辑 `/etc/ntp.conf` 文件。`/etc/ntp.conf` 文件包含了标识同步源地址和运行模式的信息。`/etc/ntp/keys` 文件可用于开启身份验证。

### Portmap 服务器

`portmap` 服务器将远程过程调用 (`RPC`) 编号转换为 `TCP/IP` 和 `UDP` 端口号。某些网络服务（如 `NFS` (`nfs`) 和 `Wall` (`rwall`)）只有在当此服务器运行时才能正常工作。`RPC` 编号存储在 `/etc/rpc` 文件中。

### SWAT

`Samba Web` 管理工具 (`SWAT`) 为配置 `Samba` 文件和打印服务提供基于 Web 的界面。配置妥当时，可以使用 Web 浏览器访问 `SWAT` 服务（需要 `root` 密码）。尽管这是一个经过测试界面，但 `Samba` 服务器配置窗口是 `Fedora` 和 `RHEL` 中配置 `Samba` 的首选工具。

默认情况下，`Fedora` 和 `RHEL` 中的 `SWAT` 服务是关闭的。要开启它，请编辑 `/etc/xinetd.d/swat` 文件并将 `disable = yes` 更改为 `disable = no`。这使得本地主机上请求端口号 `901`（例如 `http://localhost:901`）的 Web 浏览器可以使用该服务。您可以删除 `only_from = 127.0.0.1` 行，以便允许任何访问您计算机的计算机 Web 浏览器使用 `SWAT`。（当然，远程用户也需要知道您的密码）

### Arpwatch 服务器

可以开启 `arpwatch` 服务来监控网络上的以太网/`IP` 活动。任何潜在问题（例如两个不同的计算机使用相同的 `IP` 地址）都会记录在 `syslog` 设施中（通常到 `/var/log/messages` 文件中）。

默认情况下，`arpwatch` 服务是关闭的。要开启它，请输入 `chkconfig arpwatch service start`。您可以检查 `/var/log/messages` 文件以查看 `arpwatch` 服务是否成功启动，并观察网络的变化。

### 简单网络管理协议服务器

简单网络管理协议 (`SNMP`) 服务器使您的 `Fedora` 或 `RHEL` 系统能够监听来自网络的 `SNMP` 请求。当此服务器运行时，使用 `SNMP` 工具的计算机可以监控您的计算机的活动（基于在系统上设置的配置文件）。

要使用 `SNMP`，您必须安装 `net-snmp` 软件包。默认情况下，`SNMP` 是关闭的。要开启它，请使用 `chkconfig snmp on` 和 `chkconfig snptrap on`。`SNMP` 配置可能相当复杂。参考 `snmpd.conf` 手页（输入 `man snmpd.conf`）。

### 信息服务器

通过发布主机名、用户账户信息和网络地址，管理员可以更容易地管理计算机组。管理网络信息的常用服务器类型包括网络信息系统 (`NIS`)、动态主机配置协议 (`DHCP`) 和轻量级目录协议 (`LDAP`)。

#### 网络信息系统服务器

通过发布主机名、用户账户信息和网络地址，管理员可以更容易地管理计算机组。管理网络信息的常用服务器类型包括网络信息系统 (`NIS`)、动态主机配置协议 (`DHCP`) 和轻量级目录协议 (`LDAP`)。

### 动态主机配置协议服务器

与其去网络上的每台计算机手动添加它们所需的 `IP` 地址、子网掩码、网关等，您可以将 `Fedora` 或 `RHEL` 配置为动态主机配置协议 (`DHCP`) 服务器来发布这些信息。

## 附录 B：运行网络服务 1054

### 动态主机配置协议服务器

动态主机配置协议 (`DHCP`) 服务器响应 `DHCP` 客户端获取 `IP` 地址的请求。

默认情况下，`DHCP` 是关闭的。要开启它，输入 `chkconfig dhcpd on`。然后通过输入 `service dhcpd start` 启动。在 `/etc/`。

### 目录服务器

如果您的组织使用轻量级目录协议 (`LDAP`) 数据库，运行 `LDAP` 服务可以让您访问这些数据库。同样，`LDAP` 服务可以让您使用启用 `LDAP` 的应用程序，如 `Netscape Roaming Access` 和 `sendmail`。

默认情况下，`ldap` 服务是关闭的。要开启它，输入 `chkconfig ldap on`。要使该服务可用，您必须编辑 `/etc/ldap/` 目录中的文件。

### 域名系统服务器

域名系统 (`DNS`) 服务器用于将 `TCP/IP` 网络上的主机名转换为 `IP` 地址。`Fedora` 和 `RHEL` 可以使用 `named` 进程配置为 `DNS` 服务器。

默认情况下，`DNS` 服务器未在 `Fedora` 或 `RHEL` 中配置为自动启动。要开启 `DNS` 服务器，输入 `chkconfig named on`。然后通过输入 `service named start` 启动。

### 反向地址解析协议服务器

反向地址解析协议 (`RARP`) 进程响应 `RARP` 客户端获取 `IP` 地址的请求。今天，`RARP` 并不常用。

默认情况下，`RARP` 软件包 (`rarpd-srv88107-18`) 未默认安装。安装后，该服务是关闭的。要开启 `RARP` 服务器，输入 `chkconfig rarpd on`。然后通过输入 `service rarpd start` 启动。

### 数据库服务

数据库服务提供了访问和管理信息数据库的工具。`Postgres` 服务使用 `postmaster` 进程处理其服务的请求。`MySQL` 服务器运行 `mysqld` 进程处理对其数据库的访问。这些进程通过 `/etc/init.d` 中的启动脚本启动（分别是 `postgresql` 和 `mysql` 脚本）。

## 目录 B：运行网络服务

交叉引用：第 24 章描述了如何设置 `MySQL` 数据库服务器。

## 用户服务

`Fedora` 和 `RHEL` 可以为用户提供各种网络服务。这些服务允许用户运行远程程序、发送实时消息并获取活动用户信息。

### 远程执行服务器

远程执行服务器响应来自其他计算机的请求并在本地计算机上运行命令。这可能会引发安全问题，因此在配置这些服务时要小心。`Fedora` 和 `RHEL` 提供了三个远程执行守护进程：`Rsh`、`Rexec` 和 `Kshell`。

- `Rsh` 服务 (`/usr/sbin/in.rsh`) 接受由 `rsh` 命令（来自其他 `Linux` 或 `UNIX` 系统）发起的远程执行请求。默认情况下，该服务是关闭的。在允许远程执行之前，必须允许主机或用户（或两者都允许）访问。访问权限在 `/etc/hosts.equiv` 文件或每个用户目录下的 `.hosts` 文件中配置。
- `Rexec` 服务 (`/usr/sbin/in.rexec`) 接受来自 `rexec` 命令（来自其他 `Linux` 或 `UNIX` 系统）的远程执行请求。默认情况下，该服务是关闭的。要允许远程执行，发起请求的用户必须提供有效的用户名和密码。
- `Kshell` 服务 (`/usr/kerberos/sbin/kshd`) 接收来自 `rsh` 命令的远程执行请求。它使用 `Kerberos` 认证和加密，比替代 `in.rsh` 守护进程更安全。默认情况下，该服务是关闭的。但是，如果你开启它（通过编辑 `/etc/inetd.kshell` 文件并将 `disable = yes` 改为 `disable = no`），它的优先级将高于 `in.rsh` 守护进程。

之前描述的 `OpenSSH` 服务（使用 `sshd`）也可以用于远程执行。与其他使用的方法相比，`OpenSSH` 是更安全的远程执行方式。因此，在大多数情况下，你应该跳过这些服务并使用 `OpenSSH` 进行远程执行。

交叉引用：用于登录服务的登录命令描述在第 16 章中。

### Talk 服务器

使用 `in.talk` 或 `in.ntalk` 服务器允许用户使用 `talk` 命令进行通信。`talk` 命令允许用户实时来回输入消息。`talk` 守护进程处理端口 `517` 上的请求，`ntalk` 守护进程处理端口 `518` 上的请求。

这两个服务默认都是关闭的。要开启每个服务，请编辑 `/etc/xinetd.d/talk` 和 `/etc/xinetd.d/ntalk` 文件，并将 `disable = yes` 条目改为 `disable = no`。然后重启 `xinetd` 守护进程：`service xinetd restart`。

### Finger 服务器

`finger` (`/usr/sbin/in.fingerd`) 服务器让人们可以使用 `finger` 命令在本地或通过网络请求 `Linux` 或 `UNIX` 系统上活动用户的信息。该服务默认关闭。如果 `finger` 服务器接受了来自 `finger` 命令的请求，向请求用户的输出看起来所示：

```
