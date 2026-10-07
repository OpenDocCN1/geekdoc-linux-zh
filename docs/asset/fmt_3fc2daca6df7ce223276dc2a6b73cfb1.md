
### 调试服务器
你通过带有 `-de` 选项运行 `sshd` 从服务器端进行调试。服务器将在前台运行，其显示内容可能帮助你解决问题。

## 隧道/端口转发

`ssh` 工具可以通过它建立的加密连接转发端口（端口转发；第 1165 页）。由于通过转发端口发送的数据使用加密连接作为其链路层（第 380 页），因此隧道技术（第 1178 页）被应用于此连接：“连接通过 `ssh` 隧道传输。”你可以保护协议——包括 POP、X、IMAP、VNC 和 WWW。

`X11Forwarding` 设置为 `yes` 时进行转发。默认是 `no`，但 Ubuntu Linux 将 `X11Forwarding` 设置为 `yes`。要使 X11 转发工作，必须在 `~/.ssh/config` 或 `/etc/ssh/ssh_config` 配置文件（第 675 页）中将 `ForwardX11` 和 `ForwardX11Trusted` 声明也设置为 `yes`。更多信息请参阅第 681 页的“转发 X11”。

## 第18 章 OpenSSH：安全网络通信

上一个命令将从外部到防火墙 1678 端口的连接转发到 Web 服务器。通过这种方式转发连接，允许你在连接到本地系统上的 Web 服务器时，使用 Web 浏览器连接到防火墙上的 1678 端口。如果你在本地系统上运行 Web 程序（第 731 页），这种设置将非常有用，因为它允许你通过 Internet 连接从任何地方检查邮件。

压缩通过 `-C` 选项开启的压缩功能可以提高低带宽连接连接的通信速度。该选项通常与端口转发配合使用。压缩可能会增加延迟，对于通过高带宽连接转发的 X 会话来说，这可能不是理想的。

## 本章总结

`OpenSSH` 是一个安全网络连接工具包，它可以加密所有流量（包括密码），从而帮助阻止可能进行窃听、劫持连接和窃取密码的恶意用户。本章中讨论的组件包括 `sshd`（服务器守护进程）、`ssh`（在另一个系统上或内部运行命令）、`scp`（在另一个系统之间复制文件）、`sftp`（安全的替代 `ftp`）和 `ssh-keygen`（创建、管理和转换身份验证密钥）。

为了确保通信安全

`OpenSSH` 还支持 X11 转发。通过此功能，你可以在远程系统上安全地运行图形化程序，并将显示在本地系统上。

## 练习题

- 1. `scp` 和 `sftp` 工具之间有什么区别？
- 2. 你如何使用 `ssh` 查找谁登录了远程系统？
- 3. 你如何使用 `scp` 将从名为 `plum` 的系统中的 `~/.bashrc` 文件复制到本地系统？
- 4. 你如何使用 `ssh` 在 `plum` 上运行 `xterm` 并显示在本地系统上？
- 5. 当你使用 `ssh` 在本地显示器运行远程 X 应用时，开启压缩可能会什么问题？
- 6. 当你尝试使用 OpenSSH 客户端连接到另一个系统并看到警告远程主机身份识别已更改的消息时，发生了什么？你应该怎么办？

## 高级练习题

- 7. 你会使用哪个 `scp` 命令将你的家目录 `plum` 复制到本地系统？
- 8. 如果 `plum` 解锁了 root 账户并禁用了远程 root 登录，你可以提供哪个单一命令以 root 身份登录名为 `plum` 的远程系统？
- 9. 你如何使用 `ssh` 比较 `plum` 和本地系统上 `~/memos` 目录的内容？

## 19

## FTP：跨网络传输文件

# 本章内容
- FTP 客户端 ................................................ 689
- 快速入门 I: 使用 `ftp` 下载文件 ................... 690
- 匿名 FTP .......................................................................... 694
- 自动登录 ........................................................ 694
- 二进制与 ASCII 传输模式 ................................... 694
- 设置 FTP 服务器 (`vsftpd`) ...................................... 699
- 快速入门 II: 启动 `vsftpd` FTP 服务器. ....................... 700
- 配置 `vsftpd` 服务器 . . . . . 701

文件传输协议（File Transfer Protocol）是一种通过网络上的 TCP/IP 从一个系统下载或上传文件到另一个系统的方法。文件传输协议是一个客户端/服务器协议（FTP）以及调用该协议的客户端工具（`ftp`）的名称。除了原始的 `ftp` 工具外，还有许多运行在不同操作系统下的文本和图形 FTP 客户端程序。也有许多 FTP 服务器程序。

## FTP 简介

本章从 FTP 介绍开始，讨论了安全性，描述了 FTP 连接的类型，并列出了 FTP 客户端列表。第一个快速入门部分涵盖了 `ftp` 命令并包含了 `ftp` 客户端的教程。接下来的部分提供了 `ftp` 的更多详细信息。最后一部分描述了如何设置 `vsftpd` 服务器。

FTP 最初在 4.2BSDDD 下实现，在 Linux 的传播中起了至关重要的作用；该协议/程序经常用于发布免费软件。FTP 站点指的是连接到网络（Internet）的 FTP 服务器。FTP 站点可以是公共的，允许匿名用户登录并下载软件和文档。相比之下，私人 FTP 站点需要你使用用户名和密码登录。某些站点允许你上传程序。

大多数 FTP 客户端都很相似，但服务器差异很大。本章描述了 `ftp` 客户端，并引用了 `sftp`（一种安全的 FTP 客户端）。它涵盖了 Ubuntu 下提供的 FTP 服务器，名为 `vsftpd`（非常安全的 FTP 守护进程）。

`ftp` 工具是 FTP 的用户界面，FTP 是用于在网络通信系统之间传输文件的标准协议。

## 安全性

FTP 不是一种安全协议：建立 FTP 连接时交换的所有用户名和密码都是以明文发送的，通过 FTP 连接交换的数据未加密，且连接容易被劫持。鉴于这些事实，FTP 最好用于下载公共文件。在大多数情况下，OpenSSH 客户端 `ssh`（第 670 页）、`scp`（第 672 页）和 `sftp`（第 674 页）提供了 FTP 的安全替代方案。

## 仅使用 FTP 下载公共信息

FTP 是不安全的。除了允许匿名用户下载信息外，`sftp` 工具为所有 FTP 连接提供了更好的安全性。因为 `sftp` 使用加密连接，所以当你使用此工具时，密码和数据不会被嗅探窃获。你可以将本章中所有的 `ftp` 替换为 `sftp`，因为 `sftp` 使用的是加密连接。

`ftp` 工具是 FTP 的用户界面，FTP 是用于在网络通信系统之间传输文件的标准协议。

## FTP 连接

FTP 使用两个连接：一个用于控制（你登录时建立此连接），另一个用于数据传输（你请求传输文件）。

## FTP 简介

被动连接与主动连接
被动连接和主动连接的区别在于由客户端还是服务器发起数据连接。在被动模式下，客户端发起连接到服务器（默认端口 21）；在主动模式下，服务器发起连接（默认端口 20；见第 708 页“连接参数”）。哪种方法本质上都不更安全。被动连接更常见，因为位于 NAT 后的客户端可以连接到被动服务器。

## FTP 客户端

Ubuntu 提供了多个 FTP 客户端，包括 `ftp`（旧版本的 BSD 工具）。本节讨论 `ftp`，是因为大多数其他 FTP 客户端（包括 `sftp` 和 `lftp`）提供了 `ftp` 命令子集。

`sftp` OpenSSH 套件的一部分，`sftp`（`openssh-client` 包）是 `ftp` 的安全且功能等替代。`sftp` 工具不是真正的 FTP 客户端——它理解 FTP 协议。它将 `ftp` 命令映射到 SSH 命令。更多信息请见第 674 页。

`lftp` 工具（`lftp` 包）提供了与 `sftp` 相同的安全性，但提供了更多功能。更多信息请参阅 `lftp` 手册页。

`gFTP` `gftp` 工具（`gftp` 包）是一个与 FTP、SSH 和 HTTP 服务器协作的图形化客户端。该客户端具有许多实用功能，包括恢复中断的文件传输。更多信息请访问 www.gftp.org 和 freshmeat.net/projects/gftp。

`NcFTP` `ncftp` 工具（`ncftp` 包）是一个文本客户端，提供了比 `ftp` 更多的功能，包括文件名补全和命令行编辑。详情请见 www.ncftp.com 和 freshmeat.net/projects/ncftp。

# 更多信息

在 `ftp>` 提示符处输入 `help` 或 `?` 可以显示命令列表。在 `?` 后加空格并使用 `use/share ftp` 命令可以显示关于该命令的信息。
`man` 页面：`ftp`, `sftp`, `lftp`, `vsftpd.conf`。

Web `vsftpd` 首页：`vsftpd.beasts.org`

FTP HOWTO 迷你型 HOWTO

# 运行 `ftp` 和 `sftp` FTP 客户端

本节将介绍如何使用 `ftp` 和 `sftp` FTP 客户端。下面列出的命令适用于这两个实用程序。

## 前提条件

大多数 Ubuntu 系统都安装了 `ftp` 和 `sftp` 实用程序。你可以通过输入任一个实用工具的名称作为命令来检查它们是否存在：

```
$ ftp
```
```
sftp quit
```

```
$ sftp
usage: sftp [-Cv] [-B buffer_size] [-b batchfile] [-F ssh_config]
[-o ssh_option] [-P sftp_server_path] [-R num_requests]
[-S program] [-s subsystem | sftp_server] host
sftp [[user]@host[:file]]
sftp [[user]@host[:dir/]]
sftp -b batchfile [user]@host
```

如果需要，请安装 `ftp`（包含 `ftp` 和 `pftp`）或 `openssh-client`（包含 `sftp`）包。

## 快速上手：使用 `ftp` 下载文件

此快速上手章节分为两个部分：基本命令的描述以及一个展示用户如何操作 `ftp` 的教程。在开始之前，请确保按照上一节的说明，本地系统已安装 `ftp` 或 `sftp`。

### 基本命令

输入命令：

```bash
$ ftp hostname
```

其中 `hostname` 是你想要连接的 FTP 服务器的名称。如果你在服务器上有一个账户，请使用你的用户名和密码登录。如果是公共系统，请以 `anonymous`（或 `ftp`）用户身份登录，并将你的电子邮件地址作为密码。像在 shell 中使用相应的工具一样在服务器上使用 `ls` 和 `cd` 命令。`get` 命令将文件从服务器复制到本地系统，`put` 命令将文件从本地系统复制到服务器，`status` 显示 FTP 连接的信息，`help` 显示命令列表。

除了 `status` 外，上述命令在 `sftp`、`lftp` 和 `ncftp` 中也可用。

### 教程演示

以下是两个 `ftp` 会话，其中 Sam 在一个名为 `dog` 的 `vsftp` 服务器之间传输文件。当 Sam 给出 `pftp dog` 命令时，本地 `ftp` 客户端以被动模式 (PASV) 连接到服务器，该模式会要求输入用户名和密码。由于他已经在本地系统中以 `sam` 身份登录，`ftp` 建议 Sam 以 `sam` 身份登录。要以 `sam` 登录，他只需按回车。由于他的用户名是 `dog sls`，他在响应 `Name (dog:sam):` 提示时输入了 `sls`。在 Sam 用他的普通系统密码响应 `Password:` 提示后，`vsftp` 服务器向他表示欢迎，并告知他正在“使用二进制模式传输文件”。在 `ftp` 的二进制模式下，Sam 可以传输 ASCII 和二进制文件（见第 694 页）。

连接并登录

```
sam@lum:-$ ftp login
Connected to dog.bonus.com.
220 (vsFTPD 2.2.2)
Name (dog:sam): sls
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp>
```

登录后，Sam 使用 `ftp` 命令查看他远程工作目录（即服务器上的家目录）中的内容。然后他使用 `cd` 进入 `memos` 目录并显示那里的文件。

#### ls 和 cd

```ftp
ftp ls
227 Entering Passive Mode (192,168,0,12,130,201)
150 Here comes the directory listing.
drwxr-xr-x 2 1001 1001 4096 Jan 25 04:51 expenses
drwxr-xr-x 2 1001 1001 4096 Jan 25 04:53 memos
drwxr-xr-x 2 1001 1001 4096 Jan 25 04:51 memos
226 Directory send OK.
```

```ftp
ftp cd memos
250 Directory successfully changed.
```

```ftp
ftp ls
227 Entering Passive Mode (192,168,0,12,48,84)
150 Here comes the directory listing.
-rw-r--r-- 1 1001 1001 3430 Jan 25 04:52 memo.0514
-rw-r--r-- 1 1001 1001 6581 Jan 25 04:52 memo.0628
-rw-r--r-- 1 1001 1001 2801 Jan 25 04:52 memo.0905
-rw-r--r-- 1 1001 1001 7351 Jan 25 04:55 memo.0921
-rw-r--r-- 1 1001 1001 14703 Jan 25 04:53 memo.1102
226 Directory send OK.
ftp>
```

接下来，Sam 使用 `get` 命令将 `memo.1102` 从服务器复制到本地系统。他使用二进制模式确保了无论文件是二进制还是 ASCII 格式都能获得良好的副本。服务器确认文件复制成功，并报告了其大小和复制所需的时间。Sam 接着将本地文件 `memo.1114` 复制到远程系统。该文件被复制到他的远程工作目录 `memos` 中。

#### get 和 put

```ftp
ftp > get memo.1102
local: memo.1102 remote: memo.1102
227 Entering Passive Mode (192,168,0,12,53,74)
150 Opening BINARY mode connection for memo.1102 (14703 bytes).
226 File OK.
14703 bytes received in 0.00 secs (1192.5 kB/s)
ftp > put memo.1114
local: memo.1114 remote: memo.1114
227 Entering Passive Mode (192,168,0,12,182,182)
150 send data.
226 File OK.
11903 bytes sent in 0.00 secs (2394.6 kB/s)
```

现在 Sam 决定要将 `memos` 目录中的所有文件复制到本地系统的一个新目录中。他给出 `ls` 命令以确保我们复制了正确的文件，但 `ftp` 已经超时。他没有退出 `ftp` 并从 shell 给出另一个命令，而是给出了 `open` 命令来连接服务器。登录后，他使用 `ftp` 命令将目录切换到服务器上的 `memos`。

#### Timeout 和 open

```ftp
ftp > ls
No control connection for Success.
Passive mode refused.
```

```ftp
ftp > open dog
Connected to dog.bonus.com.
220 (vsFTPD 2.2.2)
Name (dog:sam): ls
ftp > cd memos
250 Directory successfully changed.
```
