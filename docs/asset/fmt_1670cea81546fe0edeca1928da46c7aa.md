
**ssh-keygen** 命令提示你输入密码，它将将其作为一种密码来保护你的私钥。密码应该是几个单词长。你还会被提示为密钥输入文件名。如果你不输入，SSH 将使用默认值。公钥将赋予扩展名 `.pub`。`ssh-keygen` 命令生成公钥并将其放置在 `~/.ssh/dsa_key.pub` 或 `~/.id_rsa.pub` 文件中，

![](img/af27012edddcf42a8b40fad81183c10b_446_0.png)

图 19-1 SSH 设置与访问

取决于指定的密钥类型；它将私钥放在对应的 `.ssh/id_rsa` 或 `.ssh/id_rsa.pub` 文件中。

注意：`.ssh/identity` 文件名在 SSH 版本 1 中命名；它在旧版本的发行版中可能是默认安装。SSH 版本 2 使用不同的文件名，`ssh_id_rsa` 或 `.ssh/id_rsa`，取决于使用 RSA 还是 DSA 身份验证。

如果你需要更改密码，可以使用 `ssh-agent` 将你的密钥留在内存中，这样你就不需要每次都输入。`ssh-agent` 旨在会话开始时使用。对于 GNOME，你可以使用 `openssh-askpass` 工具，当输入密码时由 `ssh-add` 会调用。

# 第四部分：安全

然后发送要在该主机上执行的命令。`ssh` 命令还能够支持窗口系统（Window System）的连接。如果你从 X 系统环境（如 GNOME 或 KDE）建立 `ssh` 连接，此功能将自动启用。系统会为本地 X 服务器和远程 X 服务器建立连接。远程服务器会设置一个虚拟服务器，并将任何窗口系统数据发送到你的本地系统，由你自己的本地 X 服务器进行处理。

`ssh` 登录功能非常像 `login` 命令。你只需输入带有远程主机地址的 `ssh` 命令，后面跟着 `-l` 选项以及你正在登录的远程账户的登录名（用户名）。下面的示例登录到 `rabbit.mytrek.com` 主机上的 `aleina` 用户账户。

```
$ ssh rabbit.mytrek.com -l aleina
```

你也可以在 `ssh` 中使用地址格式的用户名，例如：

```
$ aleian@rabbit.mytrek.com
```

接下来的列表显示了 `george` 如何访问 `turtle.mytrek.com` 上的 `cecelia` 账户。

```
[george@turtlege]$ $ ssh turtle.mytrek.com -l cecelia

cecel@turtle.mytrek.com:password:

[cecel@turtle cecelia]$
```

有多种选项可以配置你的连接。大多数选项的配置项可以在配置文件中设置。例如，通过 `-c` 选项，你可以指定想要使用的加密方法，例如 `idea`、`des`、`blowfish` 或 `arcfour`。通过 `-l` 选项，你可以选择特定的私钥。`-c` 选项允许你按指定的级别对传输进行压缩（选项的完整列表请参阅 `ssh` 手册页）。

## scp

你使用 `scp` 将文件从网络上的一个主机复制到另一个主机。`scp` 设计用于取代 `rcp`，它实际上使用 `ssh` 来传输数据，并采用相同的身份身份验证和加密方法。如果身份验证需要，`scp` 会请求密码或密码短语。`scp` 程序的运行方式类似于 `ssh`。在文件名或目录之前，使用用户名和主机地址来指定目录和远程主机。用户名指定 `scp` 要连接的远程账户，而主机是账户所在的远程系统。你用 `@` 将用户名与主机地址隔开，用冒号将主机地址与文件或目录名隔开。下面的示例将 `party` 文件从用户目录复制到位于 `rabbit.mytrek.com` 主机上的 `aleina` 的生日目录：

```
$ party aleina@rabbit.mytrek.com:birthday/party
```

特别感兴趣的是 `-r`（递归）选项，它允许你复制目录。选项列表请参阅 `scp` 手册页。在下一个示例中，用户将 `reports` 复制到 `user` 的 `projects` 目录：

```
$ scp -r reports justin@rabbit.mytrek.com:projects
```

## 第 19 章：Secure Shell 与 Kerberos 413

在下一个示例中，用户 `george` 从用户 `celesia` 的家目录复制 `mydoc1` 文件：

```
[george@turtle]$]$ sc celesia@turtle.mytrek.com:mydoc1

celesia@turtle.mytrek.com's password:\mydoc1 0% | 0 ---

ETA

mydoc1 100% | ********************* 17 00:00

[george@turtle]$
```

在 Windows 系统上，你也可以使用像 `winscp` 这样的 `scp` 客户端，它可以与启用了 `scp` 的 Linux 系统交互。

## sftp 和 sftp-server

通过 `sftp`，你可以传输受加密保护的 FTP 文件。`sftp` 客户端仅适用于 `ssh` 版本 2，运行方式类似于 `ftp`，包含许多命令（见第 14 章）。我们使用 `sftp` 而不是 `ftp` 来调用 `sftp` 客户端。

```
$ sftp ftp.redhat.com
```

要使用 `sftp` 客户端连接到 FTP 服务器，该服务器需要运行 `sftp-server` 应用程序。`ssh` 服务器调用 `sftp` 为使用 `ssh` 客户端的用户提供加密的 FTP 传输。`sftp` 服务器和客户端使用 SSH 文件传输（SFTP）来执行 FTP 操作。

## 端口转发（隧道技术）

如果由于某种原因，你只能通过一个不安全的主机连接安全主机，`ssh` 提供了一项名为端口转发（port forwarding）的功能。通过**端口转发**，你可以保护连接中的不安全部分。这仅需指定不安全主机连接到安全主机的端口即可。这会在本地主机和远程主机之间通过中间的不安全主机建立直接连接。加密数据将直接通过。这被称为**隧道技术（tunneling）**，在网络中创建一个加密数据的安全隧道。

要将远程系统上的端口转发到你的本地系统，请使用带有 `-L` 选项的 `ssh`，后面跟着包含本地端口、远程主机地址和要转发的端口的参数，每个参数之间用冒号隔开。这通过分配一个 socket 来监听远程侧端口来实现。每当对此端口建立连接时，连接将通过安全通道转发，并从本地机器到远程端口建立连接。在下面的示例中，本地系统的 22 端口连接到 `rabbit.mytrek.com` 系统的 23 端口：

```
$ -R 22:rabbit.mytrek.com:23
```

要将你本地系统上的端口转发到远程系统，请使用带有 `-L` 选项的 `ssh`，后面跟着包含本地端口、远程主机地址和要转发的端口的参数，每个参数之间用冒号隔开。这通过分配一个 socket 来监听远程侧端口来实现。每当对此端口建立连接时，连接将通过安全通道转发，并从本地机器到远程端口建立连接。在下面的示例中，本地系统的 22 端口连接到 `rabbit.mytrek.com` 的 23 端口：

```
$ -L 22:rabbit.mytrek.com:23
```

你可以使用 `.ssh/config` 文件中的 `LocalForward` 和 `RemoteForward` 选项为特定主机设置转发，或为你连接的所有主机设置转发。

## SSH 配置

每个用户的配置文件位于 `.ssh/config`。`/etc/ssh/ssh_config` 文件用于全局默认设置。在配置文件中，你可以设置各种选项，详见 `ssh_config`。它被组织成段，每个段以关键字 `HOST` 开始，后面跟着主机的 IP 地址或名称。接下来的行包含了你为该主机设置的选项。在下一个 `HOST` 条目结束。特别感兴趣的是 `User` 和 `Cipher` 选项。你使用 `User` 选项指定允许访问远程系统的用户名。通过 `Cipher` 选项，你可以为特定主机选择使用的加密方法。加密方法包括 `IDEA`、`DES`（标准）、三重 `DES`（3DES）、`Blowfish`（128 位）、`Arfour`（RSA 的 RC4）和 `Twofish`。下面的示例允许 `larisa` 访问 `turtle.mytrek.com` 并使用 `Blowfish` 加密传输：

```
Host turtle.mytrek.com

User larisa

Compression no

Cipher blowfish
```

要为你连接的所有主机指定全局选项，请创建一个以星号作为主机的 `HOST` 条目，`HOST *`。此条目必须放在文件的末尾，因为选项仅在第一次设置时更改。后续的选项项将被忽略。由于主机同时匹配其自身的条目和全局条目，因此特定条目应放在全局条目之前。星号 (`*`) 和问号 (`?`) 是通配符匹配运算符，允许你指定具有相同后缀或前缀的主机组。

```
Host *

FallBackToRs yes

KeepAlive no

Cipher idea
```
