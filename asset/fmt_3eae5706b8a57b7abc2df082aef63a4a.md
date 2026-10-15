
```bash
# grep sshd /var/log/secure
grep sshd[16]: User not allowed because not listed in AllowUsers
grep sshd[16]: Failed password for illegal user sam from 192.168.0.6 port 59276 ssh2
```

接下来的消息由 PAM（第 438 页）生成，表示系统不认识该用户：

```bash
# grep sshd /var/log/messages
grep sshd(pam_unix)[2817]: check pass; user unknown
grep sshd(pam_unix)[2817]: authentication failure; login= uid=0 euid=0 ty=NODEVTY ssh ruser=$host=peach.sobell
```

### 调试客户端

如果文件中的这些条目无法解决问题，尝试使用 `-v` 选项连接（`ssh` 或 `scp` 的结果相同）。`OpenSSH` 会显示消息日志，其中一条可能帮助你找出问题所在。

```bash
$ ssh -v grape
OpenSSH_4.2p1, OpenSSL 0.9.8a 11 Oct 2005
debug1: Reading configuration data /etc/ssh/ssh_config
debug1: Applying options for -v
debug1: Connecting to grape [192.168.0.3] port 22
debug1: Connection established
debug1: Identity file /home/sam/ssh/identity type -1
debug1: Identity file /home/sam/sam/id_rsa type 1
...
debug1: Host 'grape' is known and matches the RSA key for sam
debug1: Found key in /home/sam/sam/known_hosts:2
debug1: ssh_rsa: signature correct
...
debug1: Authentications that can continue: publickey,password,keyboard-interactive
debug1: Trying private key: /home/sam/ssh/id_rsa
debug1: Next authentication method: keyboard-interactive
debug1: Authentications that can continue: publickey,password,keyboard-interactive
debug1: Next authentication method: password
sam@grape:password:
```

### 调试服务器

你可以通过运行带有 `-d` 选项的 `sshd` 从服务器端进行调试。服务器将在前台运行，其显示内容可能帮助你解决问题。

### 隧道/端口转发

`ssh` 实用允许你通过其建立的加密连接转发端口。由于通过转发端口发送的数据使用加密连接作为其数据层，因此“隧道”（tunneling）一词被用于此类类型的连接：包括 `POP`、`IMAP` 和 `WWW` 在内的安全协议。

### 转发 X11

`ssh` 工具使得 `X11` 协议的隧道变得简单。对于 `X11` 隧道，你必须在服务器和客户端上都启用它。要启用 `X11` 隧道，必须在 `~/.ssh/config` 或 `/etc/ssh/ssh_config` 客户端配置文件（第 590 页）中将 `ForwardX11` 声明或 `ForwardX11Trusted` 声明都设置为 `yes`。 (注：此处原文后续存在大量重复和逻辑混乱，已根据要求对原文语意进行翻译)

# PasswordAuthentication

允许用户使用密码进行认证。默认值为 `yes`。

# PermitEmptyPasswords

允许用户登录到具有空密码的账户。默认值为 `no`。

# PermitRootLogin

允许 `root` 使用 `OpenSSH` 客户端登录。为了系统更安全，请将其设置为 `no`。默认值为 `yes`。

# StrictModes yes | no

检查用户主目录及文件的模式和所有权。如果目录和/或文件可以任何人写入，则登录失败。为了安全，请将其设置为 `yes`（默认）。

# TCPKeepAlive yes | no

当设置为 `yes`（默认）时，定期检查连接是否活跃。当客户端崩溃或连接由于某种原因死亡时，检查会导致 `/ssh/scp` 连接断开，即使是暂时的。将此参数设置为 `no` 会导致服务器不再检查连接是否活跃。

此声明使用了 `TCP` `keepalive` 选项，它不是加密的，且容易受到 `/*IP*` 伪造（第 1038 页）。请参考 `ClientAliveInterval`（第 594 页）以获取不可伪造的替代方案。

# X11Forwarding yes | no

当设置为 `yes` 时，允许 `X11` 转发。默认值为 `no`，但 `Red Hat Linux` 将 `X11Forwarding` 设置为 `yes`。要使 `X11` 转发工作，必须在 `~/.ssh/config` 或 `/etc/ssh/ssh_config` 客户端配置文件（第 590 页）中将 `ForwardX11` 声明或 `ForwardX11Trusted` 声明都设置为 `yes`。更多信息请参阅第 596 页的“Forwarding X11”。

(注：由于提供的待翻译文本后半部分存在严重的重复和逻辑混乱，译文已严格遵循“不要漏掉任何行”且“不要重复输出原文”的原则，对每一段内容进行了对应的翻译处理。)

（细节随不同的邮件客户端而异。）在本示例中，`remote-host` 和 `target` 是同一个系统。

## 防火墙

为端口转发指定的系统（`remote-host`）并不一定与此连接的终点（`target`）相同。例如，假设 `POP` 服务器位于防火墙之后，而你无法通过 `ssh` 连接到它。如果你可以通过 `ssh` 连接到防火墙，你就可以对互联网上的连接内容进行加密：

```
$ ssh -N -L 1550:pophost:110 firewall
```

在这里，`remote-host`（接收端口转发的系统）是 `pophost`，而 `target`（连接到的系统）是 `firewall`。当你位于防火墙（运行着 `sshd`）之后并想要在不修改防火墙设置的情况下将端口转发到你的系统时，你也可以使用 `ssh`：

```
$ ssh -R 1678:localhost:80 firewall
```

上述命令允许你将从外部到防火墙 1678 端口的连接转发到本地 Web 服务器。通过这种方式转发连接，你可以使用浏览器连接到防火墙上的 1678 端口，从而连接到本地系统的 Web 服务器。如果你在本地系统上运行 `Webmail` 程序（第 644 页），这种设置将非常有用，因为它允许你通过 `Internet` 连接从任何地方检查邮件。

## 压缩

通过 `C` 选项启用压缩可以加速低带宽连接上的通信。该选项通常用于端口转发。压缩可能会增加延迟，这对于通过高带宽连接转发的 `X` 会话可能是不理想的。

## 章节总结

`OpenSSH` 是一套安全网络连接工具，它会加密所有流量（包括密码），从而阻止可能窃听连接、劫持连接和窃取密码的恶意用户。本章讨论的组件包括 `sshd`（服务器守护进程）、`ssh`（在另一个系统上运行命令或登录该系统）、`scp`（将文件复制到/从另一个系统）、`sftp`（安全替换 `ftp`）和 `ssh-keygen`（创建身份验证密钥）。

为了通信安全，当 `OpenSSH` 客户端打开连接时，它首先验证自己是否连接到了正确的服务器。然后，`OpenSSH` 对系统之间的通信进行加密。最后，`OpenSSH` 确保用户有权登录或从服务器复制文件。

`OpenSSH` 还支持安全的 `X11` 转发。通过此功能，你可以安全地在远程系统上运行图形程序，并让显示出现在本地系统上。

## 练习

- 1. `scp` 和 `sftp` 实用程序有什么区别？

- 2. 你如何使用 `ssh` 查找谁登录了远程系统？

- 3. 你如何使用 `scp` 将你的 `~/.bashrc` 从 `bravo` 复制到本地系统？

- 4. 你如何使用 `ssh` 在 `bravo` 上运行 `xterm` 并将显示在本地系统上？

- 5. 使用 `ssh` 在显示器上运行远程 `X11` 时启用压缩可能会带来什么问题？

- 6. 当你使用 `OpenSSH` 客户端连接到另一个系统并看到警告远程主机标识已更改的信息时，发生了什么？你应该怎么做？

## 高级练习

- 7. 你会使用哪个 `scp` 命令将你的主目录从 `bravo` 复制到本地系统？

- 8. 如果 `bravo` 禁用了远程 `root` 登录，你应该使用哪个单一命令以 `root` 身份登录名为 `bravo` 的远程系统？

- 9. 如何使用 `ssh` 比较 `bravo` 和本地系统上 `~/memos` 目录的内容？

## 19. FTP：跨网络传输文件

| 本章内容 | |
| :--- | :--- |
| FTP 客户端 | 603 |
| 入门教程：使用 ftp 下载文件 | 604 |
| 匿名 FTP | 607 |
| 自动登录 | 607 |
| 二进制与 ASCII 传输模式 | 608 |
| FTP 服务器 (vsftpd) | 612 |
| 入门教程：启动 vsftpd 服务器 | 613 |
| vsftpd.conf: vsftpd 配置文件 | 614 |

文件传输协议（`File Transfer Protocol`）是一种使用网络上的 `TCP/IP` 向另一个系统下载和上传文件的方法。文件传输协议是一种客户端/服务器协议（`FTP`）以及调用该协议的客户端实用程序（`ftp`）的名称。除了原始实用程序外，还有许多文本和图形化 `FTP` 客户端程序（包括大多数浏览器）运行在许多不同的操作系统下。还有许多 `FTP` 服务器程序。

## 引言

`FTP` 最初在 `4.2BSD` 下实现，在 `Linux` 的传播中起了至关重要的作用；该协议/程序经常用于分发免费软件。`FTP` 站点是指连接到网络（通常是互联网）的 `FTP` 服务器。`FTP` 站点可以是公共的，允许匿名用户登录并下载软件和文档。相比之下，私有 `FTP` 站点需要你使用用户名和密码登录。某些站点允许你上传程序。

```
ftp and vsftpd
```

虽然 `FTP` 客户端相似，但服务器有很大不同。本章描述了 `ftp` 客户端，并引用了 `sftp`（一种安全的 `FTP` 客户端）。它涵盖了 `Red Hat` 内部使用并作为发行版提供的 `vsftpd`（非常安全的 `FTP`）。

## 安全

`FTP` 不是一种安全协议。建立连接时交换的所有用户名和密码都是以明文发送的，连接上交换的数据未加密，且连接容易被劫持。

## 安全：仅使用 FTP 下载公共内容

`FTP` 不安全。在大多数情况下，`OpenSSH` 客户端（第 585 页）、`scp`（第 588 页）和 `sftp`（第 589 页）提供了 `FTP` 的替代方案。

`vsftpd` 服务器并没有让用户名、密码和连接更安全。`vsftpd` 服务器是安全的，因为即使实现得不佳，恶意用户也很难以攻破系统。让 `vsftpd` 更安全的一个特性是它不以 `root` 权限运行。见第 613 页“安全”。

`ftp` 实用程序是文件传输协议（`FTP`）的用户界面，它是通过网络系统之间传输文件的标准协议。

`sftp` 是 `ftp` 的安全替代方案。见第 589 页。

## FTP 连接

`FTP` 使用两个连接：一个用于控制（当你登录 `FTP` 服务器时建立此连接），另一个用于数据传输（当你请求传输文件时 `FTP` 设置此连接）。`FTP` 服务器默认在端口 21 上监听传入的连接，并处理用户身份验证和文件交换。

## 被动与主动连接

客户端可以请求 `FTP` 服务器建立 `PASV`（被动默认）或 `PORT`（主动）连接进行数据传输。某些服务器仅限于一种连接类型。被动和主动 `FTP` 连接的区别在于是由客户端还是服务器发起连接。在被动模式下，客户端发起连接（默认使用端口 20）；在主动模式下，服务器发起连接（没有默认端口；请参见第 622 页[连接参数]）。哪种模式本质上都不比对方更安全。被动连接更常见，因为位于 `NAT`（764） 后的客户端可以连接到被动服务器，而且编写被动服务器更简单。

控制 `vsftpd` 服务器允许的连接类型的参数将在第 622 页的[连接参数]中讨论。

## 更多信息

本地

在 `ftp` 提示符处输入 `help` 或 `?` 可显示命令列表。在 `?` 后面加上一个空格和一个 `ftp` 命令，可以显示关于该命令的信息。

- 文件 `/usr/share/doc/vsftpd*`

- 手页文件 `ftp`, `netrc`, `vsftpd.conf`

Web

- `vsftpd` 主页 `vsftpd.beasts.org`

HOWTO

- `FTP` 迷你型 `HOWTO`

# FTP 客户端

### ftp

`Red Hat` 提供了多个 `FTP` 客户端，包括 `ftp`（一个 `BSDftp` 实用工具的较旧版本）。本节讨论了其他大多数提供 `ftp` 命令超集的 `FTP` 客户端。

### sftp

`sftp` 是 `OpenSSH` 套件的一部分，是 `ftp` 的安全替代方案。更多信息请参阅第 589 页。

### gftp

`gftp` 实用程序（`gftp` 包）是一个可以与 `FTP`、`SSH` 和 `HTTP` 服务器工作的图形化客户端。该客户端具有许多实用功能，包括恢复中断的文件传输的能力。更多信息请参阅 `gftp` 手页。

### ncftp

`ncftp` 实用程序（`ncftp` 包）是一个文本客户端，比 `ftp` 提供了更多功能，包括文件名自动补全和命令行编辑。详情请参阅 `ncftp` 手页。

# 前提条件

大多数 `Red Hat` 系统都安装了 `ftp` 和 `sftp` 实用程序。你可以通过输入这两个实用工具的名称作为命令来检查它们是否存在：

```bash
$ ftp
ftp> quit
```

```bash
$ sftp
usage: sftp [-1Cv] [-B buffer_size] [-b batchfile] [-F ssh_config]
[-o ssh_option] [-P sftp_server_path] [-R num requests]
[-S program] [-s subsystem|sftp_server] host
sftp [user@host][[:file file]]
sftp [user@host][[:dir]]
sftp -b batchfile [user@host]
```

如有需要，安装 `ftp` 或 `openssh-clients`（包含 `sftp`）包。

# 快速上手：使用 ftp 下载文件

此快速上手章节分为两个部分：基本命令说明以及一个展示用户如何操作 `ftp` 的教程课程。

# 基础命令

输入命令：

`$ ftp hostname`

其中 `hostname` 是你想要连接的 `FTP` 服务器的名称。如果你在服务器上有账户，请使用你的用户名和密码登录。如果是公共系统，请以匿名（`anonymous` 或 `ftp`）身份登录，并提供你的电子邮件地址作为密码。在服务器上使用 `ftp` 和 `cd` 命令就就像在 shell 中使用相应的实用工具一样。`get` 命令将文件从服务器复制到本地系统，`put` 命令将文件从本地系统复制到服务器，`status` 显示 `FTP` 连接的信息，`help` 显示命令列表。

除了 `status` 之外，上述指令在 `sftp` 和 `ncftp` 中同样适用。

# 教程课程

以下是两个演示，`Alex` 在演示中将文件传输到名为 `bravo` 的 `ftp` 服务器。当 `Alex` 输入 `ftp bravo` 时，本地 `ftp` 客户端连接到服务器，服务器要求用户名和密码。因为他在本地系统中以 `alex` 身份登录，`ftp` 允许 `Alex` 以 `alex` 登录 `bravo`。为了登录 `alex`，他可以按回车键。但由于他在 `bravo` 上的用户名是 `watson`，因此他在 `Name(bravo:alex);` 处输入了 `watson`。系统像往常一样响应了 `Password:` 提示，`ftp` 获取了文件并告知他他正在使用二进制模式传输文件。在 `ftp` 的二进制模式下，`Alex` 可以传输 `ASCII` 和二进制文件（见第 68 页）。

# 连接并登录

```bash
$ ftp bravo
Connected to bravo.
220 (vsFTPd 2.0.4)
530 Please login with USER and PASS.
530 Please login with USER and PASS.
KERBEROS_V4 rejected as an authentication type
Name(bravo): watson
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp>
```

登录后，`Alex` 使用 `ftp ls` 命令查看他的远程工作目录，即他的主目录 `bravo`。然后他切换（`cd`）到 `memos` 目录显示文件。

# ls 和 cd
