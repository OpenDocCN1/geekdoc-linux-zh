
人们经常从本地客户端远程登录到远程服务器上的账户，也许从家里电脑登录到公司电脑。你的家里电脑就是你的客户端账户，公司电脑上的账户就是你的服务器账户。在你的客户端账户上，你需要生成公钥和私钥。然后你必须将公钥的副本放在服务器账户中。你可以通过简单的发送密钥文件或从软磁盘上复制文件来实现。一旦服务器账户上有了你客户端公钥的副本，你就可以从客户端访问服务器账户。系统还会提示你输入服务器密码。图 19-1 展示了允许用户 `george` 访问账户 `cellia` 的 SSH 设置。

为了让你使用 SSH 访问其他账户，需要以下步骤：

- 在你的账户上使用公钥、私钥以及密码。你需要使用此密码从另一个账户访问你的账户。
- 将你的公钥分发到你想要访问的其他账户，将其存放在 `.ssh/authorized_keys` 文件中。
- 其他账户也必须设置公钥、私钥以及密码。
- 你需要知道其他账户的密码才能访问它。

## 使用 ssh-keygen 创建 SSH 密钥

你将使用 `ssh-keygen` 命令创建公钥和私钥。你需要指定想要使用的加密类型。你可以使用 DSA 或 RSA 加密。使用 `-t` 选项指定类型，并使用小写的加密名称 `dsa` 或 `rsa`。在以下示例中，用户使用 RSA 加密创建了密钥：

```
ssh-keygen -t rsa
```

`ssh-keygen` 命令会提示你输入密码，它将作为一种密码来保护你的私钥。密码应该是几个单词。系统还会提示你为密钥输入文件名。如果你不输入，SSH 将使用默认值。公钥将具有 `.pub` 扩展名。`ssh-keygen` 命令生成公钥并将其放置在 `~/.ssh/id_rsa.pub` 或 `~/.ssh/id_dsa.pub` 中，取决于你指定的密钥类型；它将私钥放置在相应的 `.ssh/id_rsa` 或 `.ssh/id_dsa` 文件中。

如果你需要输入密码，可以使用 `ssh-keygen` 命令和 `-p` 选项。每个用户将有自己的 SSH 配置目录，称为 `.ssh`，位于其主目录下。公钥、私钥以及 SSH 配置文件都存放在这里。如果你从源码编译，`make install` 操作将自动运行 `ssh-keygen`。

![](img/70a65fc8f3408711ddea7ea368f31720_410_0.png)

图 19-1 SSH 设置与访问

| 文件 | 描述 |
|---|---|
| `.ssh/random_seed` | 用于为随机数生成器的种子 |
| `.ssh/id_rsa` | 包含 RSA 私钥 |
| `.ssh/id_rsa.pub` | 包含 RSA 公钥 |
| `.ssh/id_dsa` | 包含 DSA 私钥 |
| `.ssh/id_dsa.pub` | 包含 DSA 公钥 |
| `.ssh/authorized_keys` | 允许登录的公钥列表 |
| `.ssh/known_hosts` | 已知主机密钥列表 |
| `.ssh/config` | SSH 配置 |
| `/etc/ssh/sshd_config` | SSH 服务器配置 |
| `/etc/ssh/ssh_config` | SSH 客户端配置 |

表 19-3 SSH 配置

你正在连接的。实际上，你从本地系统连接到远程网络主机。它被设计用于替代 `login`（执行远程登录）、`rsh`（执行远程命令）等。通过 `ssh`，你可以从本地站点登录到网络上的远程主机，然后发送命令并在该主机上执行。`ssh` 命令还能够支持 X Window 系统连接。如果你从 X Window 系统环境（如 GNOME 或 KDE）建立 `ssh` 连接，此功能将自动启用。系统会在本地 X 服务器和远程 X 服务器之间为你建立一个连接。远程主机会设置一个虚拟的 X 服务器，并将任何 X Window 系统数据发送到你的本地系统，由你自己的本地 X 服务器进行处理。

`ssh` 登录操作功能与 `login` 命令非常相似。你输入 `ssh` 命令并带有远程主机的地址，随后是 `-l` 选项以及你要登录的远程账户的登录名（用户名）。以下示例登录到 `rabbit.mytrek.com` 主机上的 `aleina` 用户账户：

```
ssh rabbit.mytrek.com -l aleina
```

你也可以在 `ssh` 中使用地址格式的用户名，例如：

```
ssh aleina@rabbit.mytrek.com
```

以下列表显示了用户如何访问 `.mytrek.com` 上的 `kecelia` 账户：

```
[george@turtle] ssh rabbit.mytrek.com -l celecia
celecia@turtle.mytrek.com:password:
Last login: Fri Sep 19 15:13:05 2003 from turtle.mytrek.com
[celecia@turtle]$
```

## scp

你使用 `scp` 将文件从网络上的一个主机复制到另一个主机。`scp` 设计用于替代 `rcp`，它实际上使用 `ssh` 来传输数据，并采用相同的身份验证和加密方法。如果身份验证需要，`scp` 会请求密码或密码。`scp` 程序的运行方式类似于 `rcp`。远程主机上的目录和文件通过文件名前的用户名和主机地址来指定。用户名指定了 `scp` 访问的远程账户，而主机是该账户所在的远程系统。你用 `@` 将用户名与主机地址分开，用 `:` 将主机地址与文件或目录名分开。以下示例将用户当前目录下的 `party` 文件复制到位于 `rabbit.mytrek.com` 主机上的 `aleina` 的生日目录下：

```
scp party aleina@rabbit.mytrek.com:/birthday/party
```

## 第 19 章：Secure Shell 与 Kerberos 373

特别值得关注的是 `-r`（递归）选项，它允许你复制整个目录。请参阅 `scp` 手页获取完整的选项列表。在下一个示例中，用户将整个 `reports` 目录复制到 Justin 的 `projects` 目录：

```
scp -r reports justin@rabbit.mytrek.com/projects
```

在下一个示例中，用户 `george` 从 `celesia` 的家目录复制 `mydocl` 文件：

```
[george@turtle]$ scp celesia@mytrek.com:mydocl
celesia@mytrek.com:~password:
mydocl 0% | 0----
ETA
mydocl 100% |************************| 17 00:00
[george@turtle]$
```

对于 Windows 系统，你也可以使用如 `winscp` 等 `scp` 客户端，它可以与启用了 `scp` 的 Linux 系统进行交互。

## sftp sftp-server

通过 `sftp`，你可以通过加密传输 FTP 文件。`sftp` 程序使用与 `sftp` 命令（见第 14 章）。该客户端仅适用于 SSH 版本 2，运行方式与 `ftp` 类似，具有许多相同的命令。使用 `sftp` 代替 `ftp` 来调用 `sftp` 客户端。

```
sftp ftp.redhat.com
```

要使用 `sftp` 客户端连接到 FTP 服务器，服务器端需要运行 `sftp-server` 应用程序。SSH 服务器调用 `sftp` 为使用 `sftp` 客户端的用户提供加密的 FTP 传输。`sftp` 服务器和客户端使用 SSH 文件传输协议（SFTP）安全地执行操作。

## 端口转发（隧道）

如果由于某种原因，你可以通过一个不安全的主机连接到安全主机，`ssh` 提供了一种名为“端口转发”的功能。通过端口转发，你可以保护连接中的不安全部分。这涉及指定不安全主机连接到安全主机的端口。这在本地主机和远程主机之间通过中间的不安全主机建立了一个直接连接。加密数据直接通过。这一过程被称为“隧道化”，在连接的服务器之间创建一条加密数据的安全隧道。

你可以将端口转发到远程系统上的端口或本地系统上的端口，使用带有 `-R` 选项的 `ssh`，随后是包含本地端口、远程主机地址和要转发端口的参数，每个参数之间用冒号隔开。这是通过在远程端分配套接字来监听该端口实现的。每当建立到该端口的连接时，连接将通过安全通道转发，并从本地机器到远程端口

## 第四部分：安全

在以下示例中，本地系统的 22 端口连接到 `rabbit.mytrek.com` 远程系统的 23 端口：

```
ssh -R 22:mytrek.com:23
```

要将本地系统上的端口转发到远程系统的端口，使用 `ssh -L` 选项，随后是包含本地端口、远程主机地址和要转发端口的参数，每个参数之间用冒号隔开。这是通过在远程端分配套接字来监听该端口实现的。每当建立到该端口的连接时，连接将通过安全通道转发，并从本地机器到远程端口。

在以下示例中，本地系统的 22 端口连接到 `rabbit.mytrek.com` 远程系统的 23 端口：
