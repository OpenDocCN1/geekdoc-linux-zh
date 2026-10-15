
> 交叉引用：有关如何配置 vsftpd 服务器，请参阅第 20 章。

> 注意：Fedora 和 RHEL 还包含支持 Kerberos 5 的 FTP 服务器。`krbs-workstation` 软件包包含支持 Kerberos 5 的 `ftppd` 守护进程。`wu-ftp` 服务器软件不再存在于 Fedora 或 RHEL 发行版中。

## 附录 B：运行网络服务

### Samba 服务器

Samba 服务器软件支持服务器消息块（SMB）文件和打印机协议。SMB 主要用于在由运行 Microsoft Windows 的计算机组成的本地网络上共享资源。你通常不会在公共网络（如互联网）上共享 SMB 文件和打印机。

在 Fedora 和 RHEL 中，Samba 服务默认是关闭的。要让 Samba 在启动计算机时自动启动，只需在 root 用户下输入 `chkconfig smb on`。要启动服务，请输入 `service smb start`。

为了让 Samba 发挥作用，请编辑 Samba 配置文件 `/etc/samba/smb.conf`。配置此文件的一种简单方法是使用 Samba 服务器配置窗口（在第 18 章中描述）。

交叉引用：有关配置 Samba 的更多信息，请参阅第 17 章和第 18 章。

### Netatalk 服务器

`netatalk` 服务器让 Linux 成为 Macintosh 的 AppleTalk 服务器。要使用 `netatalk`，你必须安装 `netatalk` 包并通过输入 `chkconfig atalk on` 开启服务。然后通过输入 `service netatalk start` 启动服务。配置是在 `/etc/atalk` 目录下的文件中完成的。

交叉引用：设置 `netatalk` 的信息请参阅第 26 章。

### NetWare 服务器

NetWare 是 Novell, Inc. 提供的一款操作系统，为网络用户提供专门的文件和打印服务。`mars-nwe` 包将你的计算机设置为模拟 NetWare 文件服务器。虽然 `mars-nwe` 不再随 Fedora 或 RHEL 分发，但可以在各种软件仓库中获取该包。

如果你安装了 `mars-nwe`，默认情况下 NetWare 文件和打印服务是关闭的。要开启它们，请输入 `chkconfig mars_nwe on`。然后输入 `service mars_nwe` 启动服务。要使该服务可用，你必须编辑 `/etc/nwswerv.conf` 文件。

### 登录服务器

Fedora 和 RHEL 提供了多种登录服务器供使用。`login` 和 `login` 服务均可允许用户从其他计算机通过网络登录到 Fedora 或 RHEL。然而，如今 `sshd` 是首选的登录服务。对于这些服务中的中的大多数，你需要从你的防火墙中允许访问该服务。

如果安装了 `telnet-server` 包，`telnet` 服务默认是关闭的。如果启用了 `telnet`，`xinetd` 守护进程会将所有 `telnet` 服务请求（默认端口 23）传递给 `intelnetd` 守护进程，后者显示 `telnet` 登录提示符。它仅对对计算机进行真实登录的用户开启——不支持匿名用户。使用 `telnet` 登录的用户将看到一个用于访问计算机的 shell 接口。

Fedora 和 RHEL 还包含了提供 Kerberos 5 支持的登录守护进程。Kerberos 5 比其他登录服务器提供的安全级别更高。启用 Kerberos 5 的登录服务器包括 `Klogin`（Kerberos 5）和 `EKlogin`（带加密的 Kerberos 5）。

`login` 服务在 UNIX 系统中已存在很长时间了，它通常比这里描述的其他登录服务安全性低。在你的 Fedora 或 RHEL 系统中，`login` 服务默认是关闭的。

Fedora 和 RHEL 登录服务器的一个新特性是 OpenSSH 服务器。该服务默认是开启的。要访问此服务，请使用带有 `openssh-client` 软件包的应用程序，例如 `ssh`、`sftp` 和 `login` 远程命令。许多 Linux 管理员使用 OpenSSH 工具，而不是使用 `rlogin` 和 `telnet` 等远程登录工具，因为 SSH 更安全。因为它通过加密网络流量来保护密码和数据不被嗅探（而 `telnet` 和 `rlogin` 数据是明文传输的）。

注意：与其他登录服务不同，不仅 SSH 服务默认是开启的，它还允许 root 通过网络登录。如果你对这感到不适，你应该如下更改 `/etc/ssh/sshd_config` 文件中的 `PermitRootLogin` 行：

```
PermitRootLogin no
```
