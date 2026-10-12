
在同一台计算机上的服务器。至少，您需要设置默认要使用的软件。

在 Red Hat Linux 7.3 中，操作系统内置了一个名为“alternatives（替代方案）”的功能。Alternatives 是 Debian GNU/Linux 替代方案功能的一种实现。本质上，alternatives 将您选择的软件（或保持默认的软件）链接到实现该服务被启动或提供服务的通用位置。

在 Red Hat Linux 中，首个通过 alternatives 实现的服务是打印和邮件服务器软件。然而，如果这一概念被广泛接受，未来预计会有其他类型的服务。目前，图形界面应用程序允许您在这两种服务之间进行切换：

- **切换邮件服务器** — 从 GNOME 菜单中选择 Programs \(\rightarrow\) System \(\rightarrow\) Red Hat Mail Transport Agent Switcher（或在终端窗口中输入 `redhat-switchmail`）。弹出的窗口允许您在 Sendmail（默认）和 Postfix 邮件传输代理之间进行选择。
- **切换打印服务器** — 从 GNOME 菜单中选择 Programs \(\rightarrow\) System \(\rightarrow\) `redhat-switch-printer`（或在终端窗口中输入 `redhat-switch-printer`）。在 LPRng（默认）或 CUPS 打印服务之间进行选择。

图 C-1 展示了 redhat-switchmail 窗口的示例：

![](img/1744bde8c889adfab3fc911e1687fecf_1050_0.png)

**图 C-1：** 使用 redhat-switchmail 更改默认的邮件传输代理。

## 引用网络服务

本节包含与 Red Hat Linux 网络服务相关的快速参考信息。列出这些服务的表格（本章末尾的表 C-1）包含以下信息：

- **功能：** 这是什么类型的服务？
- **软件包名称：** 为了让服务可用，必须安装哪些软件包？
- **启动脚本：** 哪些启动脚本用于启动服务？
- **守护进程：** 提供该服务的守护进程是哪个？
- **配置文件：** 您可以修改哪些配置文件来满足特定需求以定制该服务？

表格后的描述提供了关于该服务的额外信息。这些信息包括该服务是否默认启动，以及可以在哪里找到关于该服务的更多信息。

> **注意：** 当提到 `xinetd` 守护进程作为启动脚本时，也会注明服务被移交给的守护进程。

以下各节提供了关于表 C-1 中描述的服务的一些额外信息。

## Web 服务器

在大多数情况下，您使用 apache 软件包在 Red Hat Linux 中创建 Web 服务器。如果 apache 已安装，您需要开启该服务才能使用它（以 root 用户身份，输入 `chkconfig httpd on`）。但是，除非您的 Web 服务器有一个有效的名称（和 IP 地址），否则启动将会失败。要定义服务器名称，请在 `httpd.conf` 文件中添加一个 `ServerName` 条目，然后重启该服务。

默认情况下，能够从网络访问您系统的用户将能够查看 `/var/www/html` 目录的内容。内容中包含 apache 手册（如果安装了 apache-docs 软件包）。您需要用您自己的内容替换 `index.html` 文件。

> **交叉引用：** 有关配置 Apache Web 服务器的信息，请参见第 21 章。

apache 的一个替代方案是 TUX HTTP 服务器。TUX 是一个高性能的 Web 服务器。TUX 的整个协议栈都在 Linux 内核中运行。在 `/etc/sysconfig/tux` 文件中配置 TUX。TUX 服务默认是关闭的。要开启它，请输入 `chkconfig tux on`，它将在您下次启动计算机时启动。它将提供与 apache 相同的内容（来自 `/var/www/html` 目录）。

## 文件服务器

Red Hat Linux 中的文件服务可以使用 FTP 服务器、Samba（Windows）服务器、网络文件系统（NFS）服务器和 NetWare 服务器来提供。以下各节将描述这些服务器。

## FTP 服务器

Red Hat Linux 可用的 FTP 服务器包括 wu-ftpd 和 vsftpd。虽然 wu-ftpd 存在时间更长，但对于预计会经历极高负载的 FTP 服务器，更推荐使用 vsftpd 软件包。

华盛顿大学 FTP 软件包（wu-ftpd）包含配置 FTP 服务器所需的守护进程、配置文件和命令。如果安装了 wu-ftpd 软件包，`xinetd` 守护进程会将所有 FTP 服务请求（默认为端口 21）传递给 `in.ftpd` 守护进程，以显示 FTP 登录提示。

默认情况下，拥有真实登录名和密码的用户拥有与本地登录相同的权限。匿名用户只能访问 `/var/ftp` 目录结构（默认情况下，其中不包含任何共享文件）。（任何人使用名称 anonymous 并输入其电子邮件地址作为密码即可成为匿名用户。）

Very Secure FTP 守护进程（vsftpd）软件包是重新设计的，旨在非常可扩展且速度快。它面向需要支持大量同时用户的 FTP 站点。通过编辑 `/etc/vsftpd.conf` 和 `/etc/vsftpd.user_list` 文件来配置 vsftpd。与 wu-ftpd 一样，vsftpd 共享 `/var/ftp` 目录结构的内容，并监听端口 21 的服务请求（因此您不希望同时在同一系统上使用两个 FTP 服务器）。

要开启任一 FTP 服务，您必须编辑 `/etc/xinetd.d` 目录中的 vsftpd 或 wu-ftpd 文件（根据您想要开启的服务）。然后按如下方式更改 `disable =` 行：

```
disable = no
```

> **交叉引用：** 有关配置 wu-ftpd 和 vsftpd FTP 服务器的信息，请参见第 20 章。

> **注意：** Red Hat Linux 还包含支持 Kerberos 5 的 FTP 服务器。krb5-workstation 软件包包含支持 Kerberos 5 的 ftpd 守护进程。

## Samba 服务器

Samba 服务器软件支持服务器消息块（SMB）文件和打印机共享协议。SMB 通常用于在由运行 Microsoft Windows 的计算机组成的本地网络上共享资源。您通常不会在公共网络（如互联网）上共享 SMB 文件和打印机。

在 Red Hat Linux 中，Samba 服务默认是关闭的。要让 Samba 在启动计算机时自动启动，请将 run-level 目录（可能是 `/etc/rc3.d` 或 `/etc/rc5.d`）中的 kill 脚本（K30smb）更改为 start 脚本（S30smb）。或者，简单地以 root 用户身份输入 `chkconfig smb on`。

为了使 Samba 有用，请编辑 Samba 配置文件，`/etc/samba/smb.conf`。配置此文件的最佳方法是使用 SWAT 服务（在本附录后面描述）。

> **交叉引用：** 有关配置 Samba 的更多信息，请参见第 17 章和第 18 章。

## NetWare 服务器

NetWare 是 Novell, Inc. 开发的一个操作系统，为网络用户提供专用的文件和打印服务。随 Red Hat Linux 提供的 `mars-nwe` 软件包允许您将计算机设置为模拟 NetWare 文件服务器。

> **交叉引用：** 有关在 Red Hat Linux 中设置 NetWare 服务的信息可以在第 18 章找到。

默认情况下，Red Hat Linux 中的 NetWare 文件和打印服务是关闭的。要开启它们，请将 `kill` 脚本（`K60mars-nwe`）更改为启动脚本（`S60mars-nwe`）。通过更改您希望该服务运行的 run level 目录中的文件来实现（可能是 `/etc/rc3.d` 或 `/etc/rc5.d`）。为了让该服务可用，您需要编辑 `/etc/nwserv.conf` 文件。

## 登录服务器

Red Hat Linux 可以使用各种登录服务器。telnet 和 rlogin 服务都可以用于允许来自其他计算机的用户通过网络登录 Red Hat Linux。然而，如今 ssh 是首选的登录服务。

如果安装了 telnet-server 软件包，telnet 服务在 run level 3、4 和 5 下默认可用，并在 run level 0、1、2 和 6 下不可用。`xinetd` 守护进程将所有 telnet 服务请求（默认为端口 23）传递给 `inetd` 守护进程，以显示 telnet 登录提示。默认情况下，该服务是关闭的。一旦开启，只有拥有计算机真实登录的用户才能登录计算机——不支持匿名用户。使用 telnet 登录的用户将看到用于访问计算机的 shell 界面。

Red Hat Linux 还包含提供 Kerberos 5 支持的登录守护进程。Kerberos 5 提供的安全级别高于其他登录服务器。启用 Kerberos 5 的登录服务器包括 Klogin（Kerberos 5）和 EKlogin（带加密的 Kerberos 5）。

rlogin 服务在 UNIX 系统中已经存在了很长时间，但通常比其他描述的登录服务安全性低。您的 Red Hat Linux 系统默认不提供 rlogin 服务。

