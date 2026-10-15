

226 Directory send OK.
ftp> get kernel.txz
local: kernel.txz remote: kernel.txz
229 Entering Extended Passive Mode (|||61444||).
150 Opening BINARY mode data connection for kernel.txz (77467572 bytes).
100% |******************************************| 75651 KiB 174.60 KiB/s
00:00 ETA
226 Transfer complete.
7746752 bytes received in 07:13 (174.48 KiB/s)
ftp> ll s
kernel.txz
ftp> quit
421 Timeout.
%

一旦建立了 ftp 连接，大多数站点会将你置于二进制模式，以便你可以传输非 ASCII 文件，例如包含音频和视频剪辑的文件。你可以通过使用 binary 命令显式地将 ftp 会话置于二进制模式，这可确保正确的文件传输。你可以通过使用 ascii 命令恢复到 ASCII 模式。

在下面的章节练习中，你将使用 ftp 命令从 Internet 上的远程主机传输文件。

## EXERCISE 11.19

使用 mget 命令，通过匿名 ftp 会话连接到主机 ftp.FreeBSD.org 并将与 10.1 版本相关的所有文件传输到你的系统。

## 11.8.9 Remote Copy

你可以使用 ftp 命令在另一个网络上的远程主机之间传输文件，但这样做需要你登录到远程主机。你可以使用 rcp（remote copy）命令在同一局域网上的远程机器之间复制文件，而无需登录到远程主机。如果你在本地区域环境中使用基于网络的文件系统，例如网络文件系统（NFS），则不需要此命令。在这种情况下，你的文件存储对你完全透明，你可以从网络上的任何主机访问它们，而无需指定包含它们的主机名。以下是该命令的简要说明。

### SYNTAX

```
rcp [options] [host:]sfile [host:]dfile
rcp [options] [host:]sfile [host:]dir
```

Purpose: To copy sfile to dfile

### Commonly used options/features:

- **-p** Attempt to preserve file modify and access times; without this option, the command uses the current value of umask to create file permissions
- **-r** Recursively copy files at sfile to dir

从语法可以明显看出，你可以将文件从你的主机传输到远程主机，或从一个远程主机传输到另一个远程主机。如果远程主机不“信任”你的本地主机，rcp 命令将失败。你的本地主机名必须在远程机器上的 /etc/hosts.equiv 文件中，才能成为受信任的主机，并且才能使用 rcp、rsh 和 rlogin 命令。你还必须拥有有效的用户名和密码才能在远程主机之间传输文件。文件中一行的格式为：

```
hostname [username]
```

- 字符可以在主机名和用户名之前以拒绝访问。+ 字符可以用在主机名或用户名的位置以匹配任何主机或用户。以下是一些这样的条目。

```
uph pux  sarwar      Allows access to the user sarwar on the host uphpux
+ sarwar            Allows the user sarwar access from any host
upaix-sarwar        Denies access to the user sarwar on the host upaix
-pc1                Denies access to all users on the host pc1
pccvm               Allows access to all users on the host pccvm
```

如果你使用的主机不是受信任的主机——即未列在 /etc/hosts.equiv 文件中——你需要在远程主机上的主目录中创建一个名为 .rhosts 的文件，其中包含你将使用 rcp 命令的主机名以及你在该主机上的登录名。因此，如果远程主机是 upsun29 而你想在名为 upsun10 的主机上使用 rcp 命令，则 upsun29 上的 ~/.rhosts 文件中的条目将如下所示（假设你在 upsun10 上的登录名是 sarwar）。

```
upsun10    sarwar
```

此条目通知网络软件，即在 UNIX 内核中，sarwar 是 upsun10 主机上的受信任用户。

```
$ rcp ~/unixbook/Chapter[1-9].doc upsun29:unixbook.backup
$
```

下面的 rcp 命令将 upsun29 上的 ~/ece446/projects 目录中的所有 C 和 C++ 源文件复制到你的机器上的 ~/swprojects.backup 目录。

```
$ rcp upsun29:ecc446/projects/*.[c,C] ~/swprojects.backup
$
```

正如我们之前提到的，你也可以使用 rcp 命令将文件从一个远程主机复制到另一个远程主机。下面的 rcp 命令用于将 www1 主机的整个主目录复制到 www2 主机。注意使用 -r 选项递归复制子目录，并使用 -p 选项保留现有的修改时间和访问权限。

```
$ rcp -rp www1:* www2:
$
```

下面的章节练习让你在环境中练习使用 rcp 命令。

## EXERCISE 11.20

使用 rcp 命令将文件从你的机器复制到网络上的另一台机器。你使用了什么命令？它做了什么？

## 11.8.10 Secure Shell and Related Commands

源自 BSD 的 r 命令（rsh、rcp、rlogin 等）是不安全的，telnet 也是如此。Secure Shell（SSH）是它们的现代替代品，消除了对 .rhosts 和 hosts.equiv 文件的需求，并且可以通过加密密钥对用户进行身份验证；它还提高了其他基于 TCP/IP 的应用程序的安全性，例如 X Windows 转发，该转发通过 SSH 加密连接透明地“隧道传输”它们。处理安全连接协议的程序称为 Secure Shell daemon，sshd。

rsh 命令的安全版本称为 ssh。rsh 和其他 UNIX r 命令以明文（有时称为纯文本）与远程主机通信，而 ssh 使用强加密来传输数据，包括命令、密码和文件。每当你的数据传输到你的网络时，ssh 会自动对其进行加密，并在数据到达预期接收者时自动解密。结果是透明加密——即发送方和接收方都不知道加密/解密过程。

由于这些原因，ssh 已成为 LAN 或 Internet 中安全终端连接的事实标准。例如，ssh、scp 和 sftp 使用的加密会话可以防止任何人在嗅探数据包时理解正在进行的通信。此外，ssh 中使用的身份验证方法可以防止任何类型的欺骗，例如 IP 地址欺骗。

SSH 版本 2 是 PC-BSD 和 Solaris 的默认协议。它有三个组件：

- 1. SSH Transfer Protocol: Handles server identification, encryption algorithm and key encryption, and manages the channel between client and server

