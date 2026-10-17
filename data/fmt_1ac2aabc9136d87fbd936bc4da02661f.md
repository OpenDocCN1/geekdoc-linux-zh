
其中 `local-port` 是正在被转发到 `remote-host` 的端口号，`remote-host` 是 `local-port` 被转发入或传出的系统名称或 IP 地址，`remote-port` 是 `remote-host` 上正在从系统传出或传向系统的端口号，而 `target` 是 `ssh` 连接到的系统名称或 IP 地址。

举例来说，假设本地系统上有一个 `POP` 邮件客户端，而 `POP` 服务器位于远程网络上的一个名为 `pophost` 的系统上。`POP` 不是安全协议；每当客户端连接到服务器时，密码都会以明文发送。你可以通过 `ssh` 隧道化 `POP` 来使其更安全（`POP-3` 连接到端口 `110`；`1550` 是本地系统上的任意端口）：

```
$ ssh -N -L 1550:pophost:110 pophost
```

执行上述命令后，你可以将 `POP` 客户端指向 `localhost:1550`。客户端与服务器之间的连接将是加密的。（当你在 `POP` 客户端上设置账户时，将服务器位置指定为 `localhost, 1550`；细节随不同的邮件客户端而异。）

在前面的示例中，`remote-host` 和 `target` 是同一个系统。然而，为端口转发指定的系统（`remote-host`）不必与 `ssh` 连接的终点（`target`）相同。例如，假设 `POP` 服务器位于防火墙后面，你无法通过 `ssh` 连接到它。如果你可以通过互联网通过 `ssh` 连接到防火墙，你就可以加密跨越互联网的连接部分：

```
$ ssh -N -L 1550:pophost:110 firewall
```

在这里 `remote-host` 是 `pophost`，而 `target` 是 `ssh` 连接到的系统 `firewall`。你也可以通过这种方式在修改防火墙设置时使用 `ssh`：

```
$ ssh -N -R 1678:localhost:80 firewall
```

# 684 第 18 章 OpenSSH：安全网络通信

上述命令将防火墙上的 `1678` 转发到本地系统。这种方式连接允许你在使用防火墙时使用 `ssh`。这对于在本地系统运行 Web 程序（第 731 页）非常有用。

## 本章总结

`OpenSSH` 是一套安全连接工具，它可以加密所有流量包括密码，有助于防止恶意用户窃听、劫持连接和窃取密码。本章讨论的组件有 `ssh`（守护进程）、`ssh`（在另一个系统运行命令或登录）、`scp`（从另一个系统复制文件）、`sftp`（安全替换 `ftp`）以及 `ssh-keygen`（创建、管理和转换密钥）。

为了确保通信安全，当 `OpenSSH` 客户端打开连接时，它会验证连接的是正确的服务器。然后 `OpenSSH` 对通信进行加密。最后 `OpenSSH` 确保用户有权登录或复制文件。你可以通过 `ssh` 隧道加密许多协议，包括 `POP`、`X`、`IMAP` 和 `WWW`。

`OpenSSH` 还启用 `X11` 转发。通过此功能，你可以安全地在远程系统上运行图形程序，并让显示出现在本地系统上。

# 练习题

- 1. `scp` 和 `sftp` 工具之间有什么区别？
- 2. 如何使用 `ssh` 查看远程系统上登录了哪些用户？
- 3. 你如何使用 `scp` 将 `plum` 上的 `~/.bashrc` 复制到本地系统？
- 4. 你如何使用 `ssh` 在 `plum` 上运行 `xterm` 并将其显示在本地系统上？
- 5. 当你使用 `ssh` 运行远程 `X` 应用时，启用压缩可能会什么问题？
- 6. 当你使用 `OpenSSH` 客户端连接另一个系统并看到警告远程主机标识已更改的提示时，发生了什么？你应该做什么？

# 高级练习题

- 7. 使用哪种 `scp` 命令可以将家目录从 `plum` 复制到本地系统？
- 8. 如果 `plum` 解锁了 `root` 但禁用了远程 `root` 登录，哪个单一命令可以以 `root` 身份登录远程系统 `plum`？
- 9. 你如何使用 `ssh` 比较 `plum` 和本地系统上 `~/memos` 目录的内容？

# FTP：跨网络传输文件

### 本章内容

- `FTP` 客户端 ............................................................ 689
- 快速入门 I：使用 `ftp` 下载文件 ................................... 690
- 匿名 `FTP` ................................................................ 694
- 自动登录模式 ........................................................ 694
- 二进制/ASCII 传输模式 ................................................ 694
- 设置 `FTP` 服务器 (`vsftpd`) ........................................ 699
- 快速入门 II：启动 `vsftpd` `FTP` 服务器 ................................... 700
- 配置 `vsftpd` 服务器 ................................................ 701

文件传输协议（File Transfer Protocol，简称 `FTP`）是一种通过网络上的 `TCP/IP` 从另一个系统下载文件或向其上传文件的方法。文件传输协议既是一种客户端/服务器协议（`FTP`）的名称，也是调用该协议的客户端工具（`ftp`）的名称。除了原始的 `ftp` 工具外，还有许多文本和图形 `FTP` 客户端程序（包括大多数浏览器），它们运行在许多不同的操作系统上。此外还有许多 `FTP` 服务器程序。

# FTP 简介

本章从 `FTP` 简介开始，讨论了安全性，描述了 `FTP` 连接类型，并列出了 `FTP` 客户端列表。第一个“快速入门”部分涵盖了 `ftp` 命令，并包含一个使用 `ftp` 客户端的教程。接下来的部分提供了更多关于 `ftp` 的细节。最后部分描述了如何设置 `vsftpd` 服务器。

`FTP` 最初在 `4.2BSD` 下实现，在 Linux 的传播中发挥了至关重要的作用；该协议经常用于分发免费软件。`FTP` 站点是指连接到网络（通常是互联网）的 `FTP` 服务器。`FTP` 站点可以是公开的，允许匿名用户登录并下载软件和文档。与之相反，某些 `FTP` 站点要求你使用用户名和密码登录。某些站点允许你上传程序。

## 历史

大多数 `FTP` 客户端都很相似，但服务器之间的差异很大。本章在描述 `ftp` 的同时引用了 `sftp`（一种安全的 `FTP` 连接）。它还涵盖了 Ubuntu 下可用的 `FTP` 服务器，其名为 `vsftpd`（非常安全的 `FTP` 守护进程）。

## ftp 和 vsftpd

`ftp` 工具是 `FTP` 的用户界面，是在通过网络通信的系统之间传输文件的标准协议。

### ftp 工具

# 安全性

`FTP` 不是一个安全的协议：在建立 `FTP` 连接时，交换的所有用户名和密码都没有加密，且连接可能会被劫持。鉴于这些事实，`FTP` 最好用于下载公共文件。在大多数情况下，`OpenSSH` 客户端 `ssh`（第 670 页）、`scp`（第 672 页）和 `sftp`（第 674 页）提供了 `FTP` 的安全替代方案。

## 仅使用 FTP 下载公共信息

`FTP` 不安全。`vsftpd` 工具为除允许匿名用户下载信息以外的所有 `FTP` 功能提供了更好的安全性。由于 `vsftpd` 使用加密连接，当你使用此工具时，用户密码和数据不会被嗅探。你可以将本章中的所有 `ftp` 实例替换为 `sftp`，因为 `vsftpd` 使用与 `ftp` 相同的命令。关于 `sftp` 的更多信息请参见第 674 页。

## 安全

`vsftpd` 服务器并没有让用户名、密码、数据和连接变得安全。然而，它的安全性在于，如果 `vsftpd` 实现不当，恶意用户很难攻破运行它的直接系统。一个使 `vsftpd` 比 `ftp` 更安全的特性是它不会以 `root` 权限运行。另见第 699 页的“安全性”部分。

# FTP 连接

`FTP` 使用两个连接：一个用于控制（当你登录 `FTP` 服务器时建立此连接），另一个用于数据传输（当你要求它传输文件时，`FTP` 会建立此连接）。`FTP` 服务器默认在端口 `21` 上监听入站的连接，并处理用户身份验证和文件交换。

## 被动连接与主动连接

客户端可以请求 `FTP` 服务器建立 `PASV`（被动——使用命令 `ftp -p` 或 `pasv`）或 `PORT`（主动——使用 `ftp` 时的默认设置）连接用于数据传输。某些服务器仅限于一种类型的连接。被动 `FTP` 和主动 `FTP` 连接的区别在于是由客户端还是服务器发起的数据连接。在被动模式下，客户端发起连接（默认不使用 `20` 端口）；在主动模式下，服务器发起连接（没有默认端口；决定服务器使用哪个端口的参数见第 708 页的“连接参数”）。这两种方法在本质上都不比对方更安全。被动连接更常见，因为位于 `NAT`（第 881 页）后的客户端可以连接到被动服务器，而且编写一个可扩展的服务器更为简单。

# FTP 客户端

- Ubuntu 提供了多个 `FTP` 客户端，包括 `ftp`（一个旧版本的 BSD `FTP` 工具）。本文讨论 `ftp`，是因为大多数 `FTP` 客户端（包括 `sftp` 和 `lftp`）都提供了 `ftp` 命令的超集。
- `OpenSSH` 套件的一部分（`openssh-client` 包）是 `sftp` 的安全且功能等效的替代方案。`sftp` 工具不是真正的 `FTP` 客户端——它不理解 `FTP` 协议。它将 `ftp` 命令映射到 `OpenSSH` 命令。更多信息请参见第 674 页。
- `lftp` 工具（`lftp` 包）提供了与 `sftp` 相同的安全性，但提供了更多功能。更多信息请参见 `lftp` 页面。
- `gftp` 工具（`gftp` 包）是一个可以与 `FTP`、`SSH` 和 `HTTP` 服务器工作的图形化客户端。该客户端具有许多实用的功能，包括恢复中断的文件传输的能力。更多信息请访问 `www.gftp.org` 和 `freshmeet.net/projects/gftp`。
- `ncftp` 工具（`ncftp` 包）是一个文本客户端，提供了比 `ftp` 更多的功能，包括文件名补全和命令行编辑。详情请见 `www.ncftp.com` 和 `freshmeet.net/projects/ncftp`。

### 更多信息

- 本地帮助：在 `ftp` 提示符输入 `?` 显示命令列表。
- 文件：`/usr/share/doc/vsftpd/vsftpd.conf`
- 手页：`ftp`, `sftp`, `lftp`, `netrc`
- `vsftpd` Web 主页：`vsftpd.beasts.org`
- `FTP` 使用指南

# 运行 ftp 和 sftp 客户端

本节描述了如何使用 `ftp` 和 `sftp` 客户端。这里描述的命令适用于这两个工具。

## 前提条件

`ftp` 和 `sftp` 工具安装在大多数 Ubuntu 系统上。你可以通过输入这些工具名称来检查它们是否存在：

```
$ ftp

ftp> quit

$ sftp

usage: sftp [-1V] [-B buffer_size] [-b batchfile] [-F ssh_config]

[-o ssh_option] [-P sftp_server_path] [-R num_requests]

[-S program [-s subsystem | sftp_server]] host

sftp [[user]@host[:file]]

sftp [[user]@host[:dir]]

sftp -b batchfile [user]@host
```

根据需要安装 `ftp`（包含 `ftp` 和 `pftp`）或 `openssh`（包含 `sftp`）包。

# 快速入门：使用 ftp 下载文件

本快速入门分为两部分：基础命令说明和一个展示用户使用 `ftp` 的教程演示。在开始之前，请确保如上一节所述，本地系统已安装 `ftp` 或 `sftp`。

## 基础命令

输入命令

```
$ ftp hostname
```

其中 `hostname` 是你想连接的 `FTP` 服务器名称。如果你在服务器上有账户，请使用你的用户名和密码登录。如果是公共系统，请以匿名（或 `ftp`）身份登录，并将你的电子邮件地址作为密码。在服务器上使用 `ls` 和 `cd` 命令，就像在 shell 中使用相应的工具一样。命令 `get file` 下载文件，`put file` 从本地系统上传文件到服务器，`status` 显示 `FTP` 连接的信息，`help` 显示命令列表。
上述命令除 `status` 外，也适用于 `sftp`、`ftp` 和 `ncftp`。

## 教程演示

以下是两个 `ftp` 会话，其中 Sam 将文件传输到名为 `dog` 的 `vsftpd` 服务器。当 Sam 输入命令 `pfftp` 时，本地 `ftp` 客户端连接到

# 运行 ftp 和 sftp 客户端

服务器处于被动（`PASV`）模式，该模式会请求用户名和密码。由于 Sam 在本地系统中以 `sam` 的身份登录，因此 `ftp` 对 Sam 的登录请求响应为 `sam`。要以 `sam` 的身份登录，他只需要按回车键。由于 `dog` 上的用户名是 `sls`，因此他对 `Name (dog):` 提示的响应是 `sls`。当 Sam 在 `Password:` 提示处输入其普通系统密码后，`vsftpd` 服务器向他提供了信息并告知它正在使用二进制模式传输文件。在 `ftp` 二进制模式下，`sam` 可以传输 ASCII 文件和二进制文件（见第 64 页）。

## 连接并登录

```
sam@opt:~$ ftp dog

Connected to dog.bogus.com.

220 (vsFtpd 2.2.2)

Name (dog:sam): sls

331 Please specify the password.

Password:

230 Login successful.

Remote system type is UNIX.

Using binary mode to transfer files.

ftp>
```

登录后，Sam 使用 `ftp ls` 查看其远程工作目录的内容，该目录是 `dog` 上的主目录。然后，他 `cd` 到 `memos` 目录并显示那里的文件。

## ls 和 cd

```
ftp ls

227 Entering Passive Mode (192,168,0,12,130,201)

150 Here comes the directory listing.

drwxr-xr-x 2 1001 1001 4096 Jan 25 04:51 expenses

drwxr-xr-x 2 1001 1001 4096 Jan 25 04:53 memos

drwxr-xr-x 2 1001 1001 4096 Jan 25 04:51 tech

226 Directory send OK.
```

## ftp memos

```
ftp ls

227 Entering Passive Mode (192,168,0,12,48,84)

150 Here comes the directory listing.

-rw-r--r-- 1 1001 1001 3430 Jan 25 04:52 memo.0514

-rw-r--r-- 1 1001 1001 6581 Jan 25 04:52 memo.0628

-rw-r--r-- 1 1001 1001 2801 Jan 25 04:52 memo.0905

-rw-r--r-- 1 1001 1001 7351 Jan 25 04:53 memo.0921

-rw-r--r-- 1 1001 1001 14703 Jan 25 04:53 memo.1102

226 Directory send OK.

ftp>
```

接下来，Sam 使用 `ftp get` 将 `memo.1102` 从服务器复制到本地系统。他使用二进制模式确保了无论文件是二进制的还是 ASCII 的，都能获得良好的文件副本。服务器确认文件已成功复制，并报告了其大小和复制所需的时间。Sam 随后将本地文件 `memo.1114` 复制到远程系统。该文件被复制了他的工作目录 `memos` 中。

## get 和 put

```
ftp> get memo.1102

local: memo.1102 remote: memo.1102

227 Entering Passive Mode (192,168,0,12,53,74)

150 Opening BINARY mode connection for memo.1102 (14703 bytes).

226 File sent OK.

14703 bytes received in 0.00 secs (11692.5 kB/s)

ftp> put memo.1114

local: memo.1114 remote: memo.1114

227 Entering Passive Mode (192,168,0,12,182,184)

150 OK to send data.

226 File receive OK.

11503 bytes sent in 0.00 secs (23294.6 kB/s)

ftp>
```

现在 Sam 决定将 `memos` 目录中的所有文件复制到本地系统上的一个新目录。他输入 `ls` 命令以确保复制了正确的文件，但 `ftp` 已经超时。他没有退出 `ftp` 并从 shell 执行另一个 `ftp` 命令，而是输入了 `open dog` 命令来连接到服务器。登录后，他使用 `ftp cd` 命令将目录切换到服务器上的 `memos`。

## 超时和 open

```
ftp> ls

No control connection for command: Success

Passive mode refused.

ftp> open dog

Connected to dog.bogus.com.

220 (vsFptd 2.2.2)
```
