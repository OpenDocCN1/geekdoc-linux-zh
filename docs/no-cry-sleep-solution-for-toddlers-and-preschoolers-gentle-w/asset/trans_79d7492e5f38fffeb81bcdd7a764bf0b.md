
从用户的当前目录到位于 rabbit.mytrek.com 主机上的用户 aleina 的 birthday 目录：

```
scp party aleina@rabbit.mytrek.com:/birthday/party
```

特别值得关注的是 `-r`（递归）选项，它允许你复制整个目录。完整的选项列表请参见 scp 手册页。在下一个示例中，用户将整个 reports 目录复制到用户 justin 的 projects 目录：

```
scp -r reports justin@rabbit.mytrek.com:/projects
```

在下一个示例中，用户 george 从用户 cecelia 的主目录复制 mydoc1 文件：

```
[george@turtle george]$ scp cecelia@turtle.mytrek.com:mydoc1
cecelia@turtle.mytrek.com's password:
mydoc1      0% |                    |   0 --:--:--
ETA
mydoc1    100% |********************************|  17 00:00
[george@turtle george]$
```

在 Windows 系统上，你也可以使用 scp 客户端，如 winscp，它可以与支持 scp 的 Linux 系统交互。

## sftp 与 sftp-server

使用 sftp，你可以传输经过加密保护的 FTP 文件。sftp 使用与 ftp 相同的命令（参见第 21 章）。这个客户端仅适用于 ssh 版本 2，其操作方式与 ftp 非常相似，并包含许多相同的命令。使用 sftp 而不是 ftp 来调用 sftp 客户端。

```
sftp ftp.redhat.com
```

要使用 sftp 客户端连接到 FTP 服务器，该服务器需要运行 sftp-server 应用程序。ssh 服务器会调用 sftp-server 为使用 sftp 客户端的用户提供加密的 FTP 传输。sftp 服务器和客户端使用 SSH 文件传输协议（SFTP）来安全地执行 FTP 操作。

## 端口转发（隧道）

如果出于某种原因，你只能通过不安全的中间主机连接到安全主机，ssh 提供了一个称为端口转发（port forwarding）的功能。通过端口转发，你可以保护连接中不安全的段。这只需指定不安全主机连接到安全主机的端口即可。这将通过中间的不安全主机在本地主机和远程主机之间建立直接连接。加密数据会直接通过。这个过程被称为隧道（tunneling），即在相连的服务器之间创建一条加密数据的安全隧道。

连接通过安全通道进行转发，并从本地机器建立到远程端口的连接。在以下示例中，本地系统上的端口 22 连接到 rabbit.mytrek.com 远程系统上的端口 23：

```
ssh -R 22:rabbit.mytrek.com:23
```

要将本地系统上的端口转发到远程系统上的端口，请使用 ssh -L 选项，后跟一个包含本地端口、远程主机地址和要转发的远程端口的参数，每个参数用冒号分隔。系统会分配一个套接字来监听本地端的端口。每当有连接建立到此端口时，连接会通过安全通道转发，并在远程机器上建立到远程端口的连接。在以下示例中，本地系统上的端口 22 连接到 rabbit.mytrek.com 远程系统上的端口 23：

```
ssh -L 22:rabbit.mytrek.com:23
```

你可以在你的 `.ssh/config` 文件中使用 LocalForward 和 RemoteForward 选项，为特定主机设置端口转发，或为你连接的所有主机指定默认设置。

## SSH 配置

每个用户的 SSH 配置文件位于其 `.ssh/config` 文件中。`/etc/ssh/sys_config` 文件用于设置站点范围的默认值。在配置文件中，你可以设置各种选项，如 `ssh_config` 手册文档中所列。配置文件旨在为你可能连接的不同远程主机指定选项。它被组织成多个段，每个段以关键字 HOST 开始，后跟主机的 IP 地址。接下来的行保存你为该主机设置的选项。一个段在下一个 HOST 条目处结束。特别值得关注的是 User 和 Cipher 选项。使用 User 选项指定远程系统上允许访问的用户名。使用 Cipher 选项，你可以为特定主机选择要使用的加密方法。加密方法包括 idea、des（标准）、triple-des（3des）、blowfish（128 位）、arcfour（RSA 的 RC4）和 twofish。以下示例允许来自 turtle.mytrek.com 的 larisa 访问，并使用 Blowfish 加密进行传输：

```
Host turtle.mytrek.com
  User larisa
  Compression no
  Cipher blowfish
```

要指定适用于你所连接的任何主机的全局选项，请创建一个以星号作为其主机的 HOST 条目，即 `HOST *`。该条目必须放在配置文件的末尾，因为一个选项只在第一次设置时才会被更改。该选项的任何后续条目都会被忽略。由于主机同时匹配其自身条目和全局条目，因此其特定条目应放在全局条目之前。星号（`*`）和问号（`?`）都是通配符匹配运算符，使你可以指定具有相同后缀或前缀的一组主机。

```
Host *
  FallBackToRsh yes
  KeepAlive no
  Cipher idea
```
