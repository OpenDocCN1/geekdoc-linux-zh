
交叉引用：有关如何配置 vsftpd FTP 服务器的信息，请参见第 20 章。

> 注意：Fedora 和 RHEL 还包含一个带有 Kerberos 5 的 FTP 服务器。`kerbs-workstation` 软件包包含包含 Kerberos 5 支持的 `ftppd` 守护进程。`wu-ftp` FTP 服务器不再存在于 Fedora 或 RHEL 发行版中。

# Samba 服务器

Samba 服务器软件支持服务器消息块 (SMB) 文件和打印机共享协议。SMB 通常用于共享由运行 Microsoft Windows 的计算机组成的本地网络上的资源。你通常不会通过公共网络（如互联网）共享 SMB 文件和打印机。

Samba 服务在 Fedora 和 RHEL 中默认关闭。要让 Samba 在启动计算机时自动启动，只需作为 root 用户输入 `chkconfig sm on`。若现在启动服务，输入 `service sm start`。

为了让 Samba 有用，请编辑 `/etc/samba/smb.conf`。配置此文件的简单方法是使用 Samba 服务器配置窗口（在第 18 章描述）。

交叉引用：有关配置 Samba 的更多信息，请参见第 17 和 18 章。

# Netatalk 服务器

`netatalk` 服务器软件让 Linux 可以作为 Macintosh 的 AppleTalk 服务器。要使用 `netatalk`，你必须安装 `netatalk` 软件包并通过输入 `chkconfig atalk on` 开启服务。然后通过输入 `service netatalk start` 启动服务。配置通过 `/etc/atalk` 目录中的文件完成。

交叉引用：有关设置 `netatalk` 的信息，请参见第 26 章。

# NetWare 服务器

NetWare 是 Novell, Inc. 的一种操作系统，为网络用户提供专门的文件和打印服务。`mars-nwe` 软件包允许你设置计算机以模拟 NetWare 文件服务器。虽然 `mars-nwe` 不再随 Fedora 或 RHEL 分发，但该软件包可以通过各种软件仓库获取。

如果你安装了 `mars-nwe`，默认情况下 NetWare 文件和打印服务是关闭的。要开启它们，输入 `chkconfig mars_nwe on`。然后输入 `service mars_nwe start` 启动服务。要使该服务可用，你必须编辑 `/etc/nwserv.conf` 文件。

# 登录服务器

Fedora 和 RHEL 提供了多种登录服务器可以使用。`telnet` 和 `rlogin` 服务均可允许用户从其他计算机远程登录到 Fedora 或 RHEL。然而，如今 `ssh` 是首选的登录服务。对于这些服务中的大多数，你需要记住从防火墙允许该服务。

如果安装了 `telnet-server` 软件包，`telnet` 服务默认关闭。如果启用 `telnet`，`xinetd` 守护进程会将所有 `telnet` 请求（默认端口 23）传递给 `telnet` 登录提示符。一旦开启，只有具有真实登录名的用户才能登录计算机——不支持匿名用户。使用 `telnet` 登录的用户将获得访问计算机的界面。

Fedora 和 RHEL 还包含提供 Kerberos 5 支持的登录进程。Kerberos 5 提供了比其他登录服务器更高的安全性。启用 Kerberos-5 的登录服务包括登录 (Kerberos 5) 和登录 (Kerberos 5 加密)。

登录服务在 Unix 系统上已可用很长时间，但它通常比这里描述的其他登录服务不安全。在 Fedora 或 RHEL 系统上默认关闭。

Fedora 和 RHEL 还包含提供 Kerberos 5 支持的登录进程。Kerberos 5 提供了比其他登录服务器更高的安全性。启用 Kerberos-5 的登录服务包括登录 (Kerberos 5) 和登录 (Kerberos 5 加密)。

登录服务在 Unix 系统上已可用很长时间，但它通常比这里描述的其他登录服务不安全。在 Fedora 或 RHEL 系统上默认关闭。

Fedora 和 RHEL 还包含提供 Kerberos 5 支持的登录进程。Kerberos 5 提供了比其他登录服务器更高的安全性。启用 Kerberos-5 的登录服务包括登录 (Kerberos 5) 和登录 (Kerberos 5 加密)。

登录服务在 Unix 系统上已可用很长时间，但它通常比这里描述的其他登录服务不安全。在 Fedora 或 RHEL 系统上默认关闭。

（此处由于原文重复段落已按要求处理）

（注：文中将 "login demons" 称为 "demons"，下方已修正为 "daemons"）。

# 附录 C：运行网络服务

警告：默认不仅是 SSH 服务，而且与其他登录服务不同，它将通过网络允许 root。如果你对这感到不安，应该更改 `/etc/ssh/sshd_config` 文件中的 `PermitRoot` 如下：

```
PermitRoot no
```
