
```bash
# grep sshd /var/log/secure | tail -6
guava sshd[10244]: Server listening on :: port 22.
guava sshd[10248]: User sam from 172.16.192.150 not allowed because not listed in AllowUsers
guava sshd[10249]: input_userauth_request: invalid user sam
guava sshd[10248]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=192.168.206.181 user=sam
guava sshd[10248]: Failed password for invalid user sam from 192.168.206.181 port 59088 ssh2
guava sshd[10249]: Connection closed by 192.168.206.181
```

**检查配置文件**

你可以使用 `sshd` 的 `-t` 选项来检查服务器配置文件的语法。

## 调试客户端

如果这些文件中的条目无法帮助解决问题，请尝试使用 `-v` 选项（`ssh` 或 `scp` 均可——结果应该相同）进行连接。OpenSSH 会显示大量的调试消息，其中一条可能会帮助你找出问题所在。你可以最多使用三个 `-v` 选项来增加 OpenSSH 显示的消息数量。

```bash
$ ssh -v plum
OpenSSH_5.2p1, OpenSSL 1.0.1e-fips  11 Feb 2013
debug1: Reading configuration data /etc/ssh_config
debug1: /etc/ssh/ssh_config line 50: Applying options for *
debug1: Connecting to plum [192.168.266.181] port 22.
debug1: Connection established.
debug1: identity file /home/sam/.ssh/id_rsa type 1
debug1: identity file /home/sam/.ssh/id_rsa-cert type -1
...
debug1: Host 'plum' is known and matches the RSA host key.
debug1: Found key in /home/sam/.ssh/known_hosts:1
debug1: ssh_rsa_verify: signature correct
...
debug1: Authentications that can continue: publickey,gssapi-keyex,gssapi-with-mic,password
debug1: Next authentication method: publickey
debug1: Offering public key: /home/sam/.ssh/id_rsa
debug1: Authentications that can continue: publickey,gssapi-keyex,gssapi-with-mic,password
debug1: Trying private key: /home/sam/.ssh/id_dsa
debug1: Next authentication method: password
sam@plum's password:
```

## 调试服务器

你可以通过使用 root 权限运行命令 `/usr/bin/sshd -de` 从服务器端进行调试。服务器将在前台运行，其显示信息可能会帮助你解决问题。

# LPI 隧道/端口转发

`ssh` 实用程序可以通过其建立的加密连接转发端口（*端口转发*；第 1266 页）。由于通过转发端口发送的数据使用加密的 `ssh` 连接作为其数据链路层（第 291 页），因此*隧道*（第 1278 页）这一术语适用于这种类型的连接：“连接通过 `ssh` 进行了隧道传输。”你可以通过通过 `ssh` 进行隧道传输来保护协议，包括 `POP`、`X`、`IMAP`、`VNC` 和 `WWW`。

# 转发 X11

`ssh` 实用程序使得隧道传输 X11 协议变得容易。为了使 X11 隧道传输正常工作，你必须在服务器和客户端上都启用它，并且客户端必须正在运行 X 窗口系统。

### 服务器

在 `ssh` 服务器上，通过将 `/etc/ssh/sshd_config` 文件中的 `X11Forwarding` 声明（第 706 页）设置为 `yes`（默认值），可以启用 X11 转发。

### 受信任的客户端

在客户端上，通过将 `/etc/ssh/ssh_config` 或 `~/.ssh/config` 文件中的 `ForwardX11`（默认值为 `no`；第 698 页）和 `ForwardX11Trusted`（默认值为 `no`，但安装时设置为 `yes`；第 698 页）声明设置为 `yes`，可以启用受信任的 X11 转发。或者，你可以在命令行中指定 `-Y` 选项（第 695 页）以在受信任模式下启动客户端。

当你在客户端上启用 X11 转发时，该客户端作为受信任客户端连接，这意味着客户端信任服务器，并获得对 X11 显示的全权访问。在拥有对 X11 显示的全权访问权限的情况下，在某些情况下，客户端可能会修改 X11 显示的其他客户端。只有当你信任远程系统时才建立受信任连接。（你并不希望有人干扰你的客户端。）如果这个概念令人困惑，请参见第 459 页的技巧“X 客户端和服务器的角色可能具有误导性”。

### 非受信任的客户端

在客户端上，通过将 `/etc/ssh/ssh_config` 或 `~/.ssh/config` 文件中的 `ForwardX11`（默认值为 `no`；第 698 页）声明设置为 `yes`，并将 `ForwardX11Trusted`（默认值为 `no`，但安装时设置为 `yes`；第 698 页）声明设置为 `no`，可以启用非受信任的 X11 转发。或者，你可以在命令行中指定 `-X` 选项（第 695 页）以在非受信任模式下启动客户端。

非受信任客户端获得对 X11 显示的有限访问权限，并且无法修改 X11 显示的其他客户端。少数客户端在非受信任模式下运行时无法正常工作。如果你在非受信任模式下运行 X11 客户端时遇到问题，请尝试在受信任模式下运行（假设你信任远程系统）。`Fedora/RHEL` 将 `ssh` 客户端配置为在受信任模式下运行。

### 运行 ssh

在启用 X11 转发后，`ssh` 会对 X11 协议进行隧道传输，设置其所连接系统的 `DISPLAY` 环境变量并转发所需的端口。通常你会从图形界面（GUI）运行，这通常意味着你正在终端模拟器窗口中使用 `ssh` 连接到远程系统。当你从 `ssh` 提示符下输入 X11 命令时，OpenSSH 会创建一个新的安全通道来承载 X11 数据，并且 X11 程序的图形输出会出现在屏幕上。通常你需要在受信任模式下启动客户端。

```bash
[sam@guava ~]$ ssh plum
[sam@plum ~]$ echo $DISPLAY
localhost:10.0
```

默认情况下，`ssh` 使用 X 窗口系统显示编号 10 及以上（端口号 6010 及以上）用于转发的 X 会话。使用 `ssh` 连接到远程系统后，你可以运行命令来执行一个 X 应用程序。该应用程序将在远程系统上运行，其显示出现在本地系统上，使其看起来像是在本地运行。

# 端口转发

你可以使用 `-L` 和 `-R` 选项转发任意端口。`-L` 选项将本地端口转发到远程系统，因此尝试连接本地系统上转发端口的程序会透明地连接到远程系统。`-R` 选项执行相反的操作：它将远程端口转发到本地系统。`-N` 选项防止 `ssh` 执行远程命令，通常与 `-L` 和 `-R` 一起使用。当你指定 `-N` 时，`ssh` 仅作为私有网络用于转发端口。使用 `-L` 或 `-R` 选项的 `ssh` 命令行具有以下格式：

```bash
$ ssh -N -L,|-R local-port:remote-host:remote-port target
```

其中 `local-port` 是被转发到 `remote-host` 或从 `remote-host` 转发的本地端口号，`remote-host` 是 `local-port` 被转发到或从中转发的系统名称或 IP 地址，`remote-port` 是 `remote-host` 上从本地系统转发或转发到本地系统的端口号，`target` 是 `ssh` 连接的系统的名称或 IP 地址。

例如，假设本地系统上有一个 POP 邮件客户端，而 POP 服务器位于远程网络上，名为 `pophost` 的系统上。POP 不是安全协议；每次客户端连接服务器时，密码都会以明文发送。你可以通过通过 `ssh` 隧道传输 POP 使其更加安全（POP-3 在端口 110 上连接；端口 1550 是本地系统上的一个任意端口）：

```bash
$ ssh -N -L 1550:pophost:110 pophost
```

执行上述命令后，你可以将 POP 客户端指向 `localhost:1550`。此时，客户端与服务器之间的连接将被加密。（在 POP 客户端上设置账户时，指定服务器位置为 `localhost`，端口 `1550`；具体细节因不同的邮件客户端而异。）

## 防火墙

在上面的示例中，`remote-host` 和 `target` 是同一个系统。但是，指定用于端口转发的系统（`remote-host`）不必与 `ssh` 连接的目标（`target`）相同。例如，假设 POP 服务器位于防火墙后面，且你无法通过 `ssh` 连接到它。如果你可以通过 Internet 使用 `ssh` 连接到防火墙，你可以加密 Internet 连接的部分：

```bash
$ ssh -N -L 1550:pophost:110 firewall
```

这里 `remote-host`（接收端口转发的系统）是 `pophost`，`target`（`ssh` 连接的 系统）是 `firewall`。

当你在防火墙后面（正在运行 `sshd`），并且希望在修改防火墙设置的情况下将端口转发到你的系统中时，也可以使用 `ssh`：

```bash
$ ssh -R 1678:localhost:80 firewall
```

上述命令将来自外部的连接到防火墙上的端口 1678 转发到本地 Web 服务器。以这种方式转发连接，允许你在连接到本地系统的 Web 服务器时，使用 Web 浏览器连接到防火墙上的端口 1678。如果你在本地系统上运行 Webmail 程序（第 758 页），这种设置将非常有用，因为它允许你使用 Internet 连接在任何地方检查邮件。

# 压缩

使用 `-C` 选项启用的压缩可以加快低带宽连接上的通信速度。此选项通常与端口转发一起使用。对于通过高带宽连接转发的 X 会话，压缩可能会增加延迟，而这可能不是所希望的。

# 章节摘要

OpenSSH 是一套安全的网络连通性工具，它加密所有流量（包括密码），从而有助于阻止可能窃听、劫持连接和窃取密码的恶意用户。`sshd` 服务器守护进程接受来自客户端的连接，这些客户端包括 `ssh`（在另一系统上运行命令或登录）、`scp`（在另一系统之间复制文件）和 `sftp`（安全地替代 `ftp`）。包括 `ssh-keygen`（创建、管理和转换身份验证密钥）、`ssh-agent`（在会话期间管理密钥）和 `ssh-add`（与 `ssh-agent` 配合使用）在内的辅助程序用于创建和管理身份验证密钥。

为了确保通信安全，当 OpenSSH 客户端打开连接时，它会验证是否连接到正确的服务器。然后 OpenSSH 加密系统之间的通信。最后，OpenSSH 确保用户有权登录服务器或从服务器复制文件。你可以通过通过 `ssh` 进行隧道传输来保护许多协议，包括 POP、X、IMAP、VNC 和 WWW。

如果配置正确，OpenSSH 还允许安全的 X11 转发。借助此功能，你可以在远程系统上安全地运行图形程序，并使显示出现在本地系统上。

## 练习

- `scp` 和 `sftp` 实用程序之间有什么区别？

- 如何使用 `ssh` 找出谁登录在远程系统上？

- 如何使用 `scp` 从名为 `plum` 的系统复制你的 `~/.bashrc` 文件到本地系统？

- 如何使用 `ssh` 在 `plum` 上运行 `xterm` 并在本地系统上显示？

## 进阶练习

- 你应使用哪个 `scp` 命令从 `plum` 将你的主目录复制到本地系统？

- 如果名为 `plum` 的远程系统禁用了远程 root 登录，你能下达哪条单一命令以 `root` 身份登录到该系统？

- 你如何使用 `ssh` 来比较 `plum` 和本地系统上 `~/memos` 目录的内容？

- 你如何使用带有 OpenSSH 认证的 `rsync` 将本地系统工作目录中的 `memos12` 文件复制到 `plum` 上的你的主目录？你如何将本地系统工作目录中的 `memos` 目录复制到 `plum` 上的你的主目录，并使 `rsync` 在复制文件时显示每个文件？

# 19 FTP：通过网络传输文件

### 本章内容

- FTP 客户端 ....... 715

- 快速入门 I：使用 `ftp` 下载文件 ............ 716

- 匿名 FTP ....... 719

- 自动登录 ....... 720

- 二进制与 ASCII 传输模式 ....... 720

- 设置 FTP 服务器 (vsftpd) ....... 724

- 快速入门 II：启动 vsftpd FTP 服务器 ....... 725

- 配置 vsftpd 服务器 ....... 726

### 学习目标

阅读完本章后，你应该能够：

- 从 FTP 服务器下载文件和上传文件

- 从匿名 FTP 服务器下载文件

- 使用 `.netrc` 文件自动化 FTP 登录

- 解释二进制传输和 ASCII 传输之间的区别

- 安装和配置 `vsftpd` 服务器

FTP（文件传输协议）是一种使用网络上的 TCP/IP 从其他系统下载文件和上传文件的方法。FTP 是一个客户端/服务器协议（FTP）和一个调用该协议的客户端实用程序（`ftp`）的名称。除了原始的 `ftp` 实用程序外，还有许多文本和图形 FTP 客户端程序，包括大多数浏览器，它们运行在许多不同的操作系统上。还有许多 FTP 服务器程序。

### FTP 简介

本章从 FTP 的介绍开始，讨论安全性，描述 FTP 连接的类型，并列出 FTP 客户端的列表。第一个快速入门部分涵盖基本的 `ftp` 命令，并包含使用 `ftp` 客户端的教程。接下来是一节介绍 `ftp` 更多细节的内容。最后一节描述了如何设置 `vsftpd` FTP 服务器。

**历史** 最初在 4.2BSD 下实现的 FTP，在 Linux 的传播过程中发挥了至关重要的作用；该协议/程序经常用于分发自由软件。

**FTP 站点** 术语 **FTP 站点** 指的是连接到网络（通常是互联网）的 FTP 服务器。FTP 站点可以是公开的，允许匿名用户登录并下载软件和文档。相反，私有 FTP 站点要求使用用户名和密码登录。一些站点允许你上传程序。

**ftp** 和 **vsftpd** 虽然大多数 FTP 客户端相似，但服务器差异较大。本章描述了 `ftp` 客户端，并参考了 `sftp`，这是一种安全的 FTP 客户端。它还涵盖了 Fedora/RHEL 内部使用并作为其发行版一部分提供的 `vsftpd`（非常安全的 FTP 守护进程）服务器。

**ftp 实用程序** `ftp` 实用程序是 FTP 的用户界面，FTP 是一种在通过网络通信的系统之间传输文件的标准协议。

### 安全性

FTP 不是一个安全的协议：在建立 FTP 连接时交换的所有用户名和密码都是以明文发送的，通过 FTP 连接交换的数据未经加密，并且连接容易受到劫持。鉴于这些事实，FTP 最好用于下载公开文件。为了宿主用例，OpenSSH 客户端 `ssh`（第 693 页）、`scp`（第 695 页）和 `sftp`（第 697 页）提供了比 FTP 更安全的替代方案。

**仅使用 FTP 下载公开信息**

**安全性** FTP 不安全。`sftp` 实用程序为除允许匿名用户下载信息外的所有 FTP 功能提供了更好的安全性。由于 `sftp` 使用加密连接，使用此实用程序时，用户密码和数据无法被嗅探。你可以将本章中所有 `ftp` 实例替换为 `sftp`，因为 `sftp` 使用与 `ftp` 相同的命令。有关 `sftp` 的更多信息，请参阅第 697 页。

`vsftpd` 服务器*不*使用户名、密码、数据和连接更加安全。然而，它是安全的，因为即使 `vsftpd` 实现不佳，恶意用户也会发现直接入侵运行该系统的系统更加困难。

使 `vsftpd` 比 `ftpd` 更安全的一个特点是，它不以 `root` 权限运行。另请参阅第 725 页的“安全性”。

### FTP 连接

- FTP 使用两个连接：一个用于控制（在登录到 FTP 服务器时建立此连接），另一个用于数据传输（当你要求传输文件时，FTP 设置此连接）。FTP 服务器默认在 21 端口监听传入连接，并处理用户身份验证和文件交换。
