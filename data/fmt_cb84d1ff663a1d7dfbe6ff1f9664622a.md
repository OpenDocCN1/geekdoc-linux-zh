
另一个流行的 FTP 服务器是 Trivial FTP 服务器 (`tftp`)。`Tftp` 经常用作 Linux 终端服务器等项目的启动服务器。

> 交叉引用：请参阅第 20 章获取有关如何配置 `vsftpd` FTP 服务器的信息。

> 注意：Fedora 和 RHEL 包含一个支持 Kerberos 5 的 FTP 服务器。`kerb5-workstation` 包包含带有 Kerberos 5 支持的 `ftppd` 守护进程。`wu-ftp` FTP 服务器软件不再包含于 Fedora 或 RHEL 发行版中。

## Samba 服务器

Samba 软件支持服务器消息块 (`SMB`) 和通用互联网文件系统 (`CIFS`) 文件和打印机共享协议。`SMB` 和 `CIFS` 通常用于在运行 Microsoft Windows 的计算机组成的本地网络共享资源。你通常不会通过互联网等公共网络共享 `SMB/CIFS` 文件和打印机。

Samba 服务在 Fedora 和 RHEL 中默认是关闭的。要让 Samba 在启动计算机时自动启动，只需在 root 用户上输入 `chkconfig smb`。要启动服务，输入 `samba smb`。

为了让 Samba 有用，请编辑 Samba 配置文件 `/etc/samba/smb.conf`。配置此文件的一种简单方法是使用 Samba 服务器配置窗口（在第 18 章描述）。

> 交叉引用：欲需有关配置 Samba 的更多信息，请参阅第 17 和 18 章。

## Netatalk 服务器

`netatalk` 软件使 Linux 可以作为 Macintosh 计算机的旧 AppleTalk 服务器。要使用 `netatalk`，你必须安装 `netatalk` 包并通过输入 `chkconfig atalk on` 开启服务。然后通过输入 `service netatalk start` 启动服务。配置通过 `/etc/atalk` 目录中的文件完成。

> 交叉引用：请参阅第 26 章获取有关设置 `netatalk` 的信息。

## 登录服务器

Fedora 和 RHEL 提供了多种登录服务器可以使用。`telnet` 和 `login` 服务均可用于允许用户从其他计算机通过网络登录到 Fedora 或 RHEL。如今，`sshd` 是首选的登录服务器。对于这些服务的大部分，你需要从防火墙中允许访问该服务。

如果安装了 `telnet-server` 包，`telnet` 服务默认是关闭的。如果启用了 `telnet`，`xinetd` 守护进程会将所有 `telnet` 服务的请求（默认端口 23）传递给 `in.telnet` 以显示登录提示。一旦开启，只有对计算机进行真实登录的用户才能登录计算机——不支持匿名用户。登录的用户将看到一个用于访问计算机的 shell 界面。

Fedora 和 RHEL 还包含提供 Kerberos 5 支持的登录守护进程。Kerberos 5 提供了其他登录服务器更高级别的安全性。启用 Kerberos 5 的登录服务器包括 `Klogin` (Kerberos 5) 和 `EKlogin` (带加密的 Kerberos 5)。

`login` 服务在 UNIX 系统中已存在很久，尽管它通常比这里描述的其他登录服务安全性低。你的 Fedora 或 RHEL 系统上的 `login` 服务默认是关闭的。

Fedora 和 RHEL 可用的登录服务器中，较新的新增是 OpenSSH 服务器。该服务默认是关闭的。要访问此服务，请使用带有 `openssh-client` 软件包的应用程序。

> 注意：由于 SSH 能够加密流量以保护密码和数据不被嗅探（而 `telnet` 和 `login` 以明文发送数据），此处原文不完整

```bash
# 示例配置

AllowLogin no
```
