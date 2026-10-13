
其中 `mailbox` 是将代替默认 `INBOX` 箱进行检查的邮箱箱（或文件夹）名称。

> 注意在使用此选项时要小心，因为 `fetchmail` 将其检索到的任何消息转发到你 Linux PC 上的普通本地邮箱箱。曾经在不同邮箱箱中的消息现在将合并到一个地方。

# 邮件服务与 Linux 简介

第一部分

第 8 行显示客户端发出 `CAPABILITY` 命令，第 9 到 11 行显示了服务器的响应，列出了该特定 IMAP 服务器软件支持的功能。

## NOOP

`NOOP` 命令顾如其名——什么都不做。它可以用于向服务器发送自动命令，以防止空闲注销计时器过期。`NOOP` 命令的响应应该总是正向的。由于服务器允许从任何命令返回状态信息，`NOOP` 命令可以触发服务器生成状态报告。如果邮箱箱在客户端空闲期间发生了某些变化（例如，服务器由于邮件管理员设置的邮箱箱规则删除了消息），则新的状态可以作为 `NOOP` 命令的响应返回。

## LOGOUT

`LOGOUT` 命令用于注当前用户退出邮件服务器并关闭所有打开的邮箱箱。如果任何消息被标记为 `\DELETED`，它们将在此时从邮箱箱中移除。

# Linux IMAP 实现

目前已经为 Linux 平台编写了几个 IMAP 软件软件包，涵盖了 IMAP 客户端和 IMAP 服务器。随着 IMAP4 的日益流行，我们预计在 Linux 世界的这一软件开发领域看到更多活动。本节将介绍最常用的 IMAP 服务器软件和 IMAP 客户端软件的 Linux 软件包。

# Linux 作为 IMAP 服务器

`imap` 软件包是一个在华盛顿大学开发的流行的 IMAP4 服务器实现。它以二进制软件包的形式包含在许多 Linux 发行版中。如果你没有二进制发行或想安装最新版本，可以从华盛顿大学的 FTP 站点（`ftp.cac.washington.edu`）获取源代码。最新版本命名为 `imap.tar.z`。在编写此时，该版本为 `imap-4.6.beta`。

`IMAP` 程序由 Internet `inetd` 调用，默认情况下在标准的 IMAP TCP 端口 `143` 上监听连接请求。`etc/inetd.conf` 文件中运行 `imap` 需要的配置行是

```
imap stream tcp nowait root /usr/sbin/tcpd imapd
```

`IMAP` 客户端的默认邮件目录是 `/etc/passwd` 文件中为用户 ID 指定 Linux `$HOME` 目录。有关如何安装 IMAP 服务器软件的详细信息，请参见第 12 章“安装和配置 POP3 和 IMAP”。

# Linux 作为 IMAP 客户端

`fetchmail` 程序可以配置为使用 IMAP 协议从 IMAP 服务器上的多个邮箱箱中检索邮件。你可以使用 `fetchmailconf` 来配置 IMAP 服务器的基本设置，将 IMAP 指定为邮件传输协议（参见第 6 章“POP3 协议”）。`fetchmailconf` 会为用户的默认邮箱箱创建一个 `.fetchmailrc` 文件。这通常是特殊的 `INBOX` 邮箱箱。如果你想检查 IMAP 服务器上配置的其他邮箱箱，可以使用 `fetchmail` 中的 `-r` 选项：

```
fetchmail -r mailbox
```
