
## 加载密钥

如果你经常连接远程主机，可以使用 `ssh-agent` 命令将私钥保留在内存中，以便可以快速解密传输。`ssh-agent` 命令旨在登录会话开始时使用。对于 GNOME，你可以使用由 `ssh-add` 用的 `openspass-gnome` 工具，它允许你在登录 GNOME 时输入密码。每当你使用 SSH 客户端时，GNOME 自动提示。

虽然 `ssh-agent` 命令允许在内存中使用私钥，但你必须专门使用 `ssh-add` 命令将私钥加载到内存中。不带参数的 `ssh-add` 会从 `.id_dsa` 或 `.id_rsa` 文件加载私钥。系统会提示你输入该私钥的口令。使用带有 `-l` 的从内存中移除密钥。如果你有多个私钥，可以将它们全部加载到内存中。

## SSH 客户端

SSH 最初设计用于替代远程访问操作，如 `login`、`rcp` 和 `Telnet`（见第 15 章），这些操作没有加密，会引入诸如明文传输密码等安全风险。你还可以

使用 `ssh` 将服务器会话编码为 FTP 传输 (`sftp`)。`ssh-client` 包包含了相应的 SSH 客户端用以替换这些应用程序。通过 `slog` 或 `ssh`，你可以从远程主机登录并执行命令以及运行应用程序，就像使用 `login` 和 `ssh` 一样。通过 `scp`，你可以在远程主机和网络主机之间复制文件，就像使用 `rcp` 一样。通过 `ssh`，你可以传输受加密保护的 FTP 文件。

### SSH 配置文件

表 18-2：SSH 配置文件

| 文件 | 描述 |
| --- | --- |
| `$HOME/.ssh/known_hosts` | 记录用户登录过的所有主机的主机密钥（不在 `/etc/ssh/ssh_known_hosts` 中的主机密钥）。 |
| `$HOME/.ssh/random_seed` | 用于初始化随机数生成器的种子。 |
| `$HOME/.ssh/id_rsa` | 包含用户的 RSA 认证身份。 |
| `$HOME/.ssh/id_dsa` | 包含用户的 DSA 认证身份。 |
| `$HOME/.ssh/id_rsa.pub` | 包含用于认证的 RSA 公钥。该文件的内容将通过添加到所有你希望使用 RSA 认证登录的机器上的 `$HOME/.ssh/authorized_keys` 中。 |
| `$HOME/.ssh/id_dsa.pub` | 包含用于认证的 DSA 公钥。该文件的内容将通过添加到所有你希望使用 DSA 认证登录的机器上的 `$HOME/.ssh/authorized_keys` 中。 |
| `$HOME/.ssh/config` | 用户的配置文件。 |
| `$HOME/.ssh/authorized_keys` | 列出可以用于此用户登录的 RSA 或 DSA 密钥。 |
| `/etc/ssh/ssh_known_hosts` | 系统级已知主机密钥列表。 |
| `/etc/ssh/ssh_config` | 系统级配置文件。该文件为用户配置文件未指定的值提供了默认值。 |
| `/etc/ssh/sshd_config` | SSH 服务器配置文件。 |
| `/etc/ssh/shrc` | SSH 默认设置。当用户登录时，`ssh` 会在用户 shell（或命令）启动之前执行此文件中的命令。 |
| `$HOME/.ssh/rc` | 当用户登录时，`ssh` 会在用户 shell（或命令）启动之前执行此文件中的命令。 |

## ssh

通过 `ssh`，你可以从本地客户端远程登录到网络上作为 SSH 服务器的远程系统。“本地客户端”指的是网络外部的设备，例如你的家用电脑，而“远程”指的是你正在连接的网络上的某个主机系统。实际上，你从本地系统连接到远程主机。它被设计用于替代执行登录的 `login` 以及用于执行命令的 `rish`。通过 `ssh`，你可以从本地系统登录到网络上的远程主机，并发送命令在主主机上执行，它还能够支持 Windows 系统的连接。如果你从 Windows 系统环境（如 GNOME 或 KDE）建立连接，此项功能将自动启用。你的本地 X 服务器和远程 X 服务器之间将建立一个连接。远程主机设置一个虚拟终端并将任何 Windows 系统数据发送到你的本地系统，由你自己的本地 X 服务器进行处理。

`ssh login` 选项的功能与 `login` 命令相似。你输入 `ssh` 命令并带有远程主机的地址，然后是 `-l` 选项和要登录的远程账户登录名（用户名）。以下示例在 `rabbit.mytrek.com` 主机上登录 `aleina` 账户：

```
ssh rabbit.mytrek.com -l aleina
```

你也可以在 `ssh` 中使用地址格式的用户名，例如：

```
ssh aleina@rabbit.mytrek.com
```

以下列表显示了用户 `george` 如何访问 `turtle.mytrek.com` 上的 `celelia` 账户：

```
[george@turtlege]$ ssh turtle.mytrek.com -l celelia
celelia@turtle.mytrek.com's password:
Login: Fri Sep 19 15:13:05 2003 turtle.mytrek.com
[celelia@turtlege]$]
```

提供了多种选项供你配置连接。大多数具有配置选项的可以在配置文件中设置。例如，通过 `-c` 选项，你可以指定想要使用的加密方法，例如 `idea`、`des`、`blowfish` 或 `arcade`。通过 `-l` 选项，你可以选择一个特定的私钥来使用。`-c` 选项允许你以指定的级别对传输进行压缩（完整选项列表请参考 `ssh` man 手页）。

## scp

你使用 `scp` 将文件从网络上的一个主机复制到另一个主机。`scp` 设计用于替代 `rcp`，它实际上使用 `ssh` 传输数据，并采用了一些认证和加密方法。如果认证需要，`scp` 会请求密码或短语；`scp` 的工作方式类似于 `rcp`。远程主机上的目录和文件通过文件名目录之前的用户名和主机地址来指定。用户名指定了访问的远程用户账户，主机是该账户所在的远程系统。你用 `@` 符号分隔用户，并用冒号从文件或目录名指定主机地址。以下示例将用户当前目录的文件复制到 `rabbit.mytrek.com` 主机上远程 `aleina` 的生日目录：

```
scp party aleina@rabbit.mytrek.com:/birthday/party
```

在下一个示例中，用户从用户 `celelia` 的家目录复制 `mydoc` 文件：

```
[george@turtlege]$ scp celelia@turtle.mytrek.com:mydoc
```

```
celelia@turtle.mytrek.com's password:
mydoc
```

在 Windows 系统上，你也可以使用 `scp`，它可以与 Linux 交互。

## sftp

通过 `ssh`，你可以传输受加密保护的 FTP 文件。

SSH 文件传输协议 (`SFTP`) 提供了一种通过 SSH 连接安全传输文件的方法。它是运行在 SSH 子系统上的 FTP 协议扩展。`SFTP` 允许文件访问、文件传输和文件管理（如删除或重命名文件）。

使用 `sftp` 时，使用 `sftp` 命令后跟远程主机的地址：

```
sftp user@host
```

要使用 `sftp` 客户端连接到 FTP 服务器，该服务器需要运行 `sftp-server`。该客户端与 `ssh` 版本 2 工作，其操作方式与 `ftp` 命令类似。请使用 `sftp` 替代 `ftp`。

```
sftp example.com
```

## SSH 配置

每个用户的 SSH 配置文件位于其 `.ssh/config` 文件中。`/etc/ssh/sys_config` 文件设置了全局默认值。在配置文件中，你可以选择 `ssh-config` 文档中列出的各种选项。该文件用于为你连接的远程主机指定选项。它被组织成多个段，每个段以 `HOST` 开始，随后是该主机的 IP 地址。接下来的行包含你设置的选项。一个段在下一个 `HOST` 条目处结束。特别关注的是 `User` 和 `Cipher` 选项。使用 `User` 选项指定远程系统上允许访问的用户名。通过 `Cipher` 选项，你可以为特定主机选择使用的加密方法。加密方法包括 `dea`、`des (standard)`、`triple-des (3des)`、`blowfish (128 bit)`、`arcfour (RSA's RC4)` 和 `twofish`。以下示例允许 `larisa` 访问 `turtle.mytrek.com`，并使用 Blowfish 加密进行传输：

```
Host turtle.mytrek.com

User larisa

Compression no

Cipher blowfish
```

要指定适用于你连接的任何主机的全局选项，请创建一个以星号作为主机的 `HOST` 条目，即 `HOST *`。此条目必须放在配置文件的末尾，因为选项仅在第一次出现时会被更改。任何后续的相同选项条目都会被忽略。由于主机会同时匹配自身的条目和全局条目，因此其特定条目应放在全局条目之前。星号 `*` 和问号 `?` 都是通配符匹配运算符，允许你指定具有相同后缀或前缀的主机组。

```
Host *

FallbackToRsh yes

KeepAlive

Cipher idea
```

# Kerberos

本章将讨论如何通过 Kerberos 服务器（Kerberos servers）控制某些服务的用户身份验证。Kerberos 认证提供了另一个级别的安全保障，可以对单个服务进行保护，仅允许经过授权的用户使用该服务。所有 Kerberos 服务器均已通过 `authconfig-gtk`（“系统设置”菜单或窗口中的“身份验证”）进行启用和配置。

Kerberos 是一种网络认证协议，它在客户端和服务器之间提供加密保护的认证连接。作为一种认证协议，Kerberos 要求客户端在访问服务器之前使用加密方法证明其身份。一旦通过验证，客户端和服务器就可以使用加密进行所有通信。防火墙防止来自外部的攻击，而 Kerberos 旨在防范来自网络内部的攻击。已经在网络中的用户可能会尝试入侵本地服务器。Kerberos 为服务器本身提供保护，而不是整个网络或计算机。你可以从马萨诸塞理工学院的 `web.mit.edu/kerberos` 获取免费版本，该版本遵循 MIT 公开许可证，该许可证类似于 GNU 公开许可证。Kerberos 的名字源于希腊神话，是地冥王国的三头神犬的名字。请务必检查 `web.mit.edu/kerberos` 网站以获取最新的更新和详细文档，包括常见问题解答（FAQs）、手册和教程。

### 提示

Kerberos V5 软件包包含了其特定版本的网络工具，如 `Telnet`、`RCP`、`FTP` 和 `RSH`。这些工具为远程用户提供了经过验证的访问。这些工具的操作方式与第 15 章中描述的原始对应相同。该软件包还包含 Kerberos 版本的 `su` 管理登录命令 `ksu`。

# Kerberos 服务器

Kerberos 的关键在于 Kerberos 服务器，所有对任何服务器服务的请求都通过该服务器进行。Kerberos 服务器随后对客户端进行身份验证，识别并验证客户端使用特定服务器的权限。服务器维护着授权用户数据库。Kerberos 向客户端颁发一个加密票据，客户端可以使用该票据获取服务器访问。例如，如果用户需要检查邮件，则向 Kerberos 服务器发送使用邮件服务器的请求，服务器随后验证用户并颁发票据，然后使用该票据访问邮件服务器。没有由 Kerberos 颁发的票据，任何人无法访问任何服务器。最初，此过程要求用户对他们想要访问的每个服务器都要单独的身份验证程序。然而，现在用户只需要执行一次对所有服务器有效的初始身份验证。

### 提示

在 Red Hat 上，你使用 Kerberos 票据管理器（“额外应用程序”菜单）来管理 Kerberos 票据，并使用 `authconfig-gtk` 工具（“系统设置”窗口）来指定并启用 Kerberos 域（realms）。

此过程实际上涉及两个服务器：认证服务器 (`AS`) 和票据授予服务器 (`TGS`)。它们共同组成了密钥分发中心 (`KDC`)。实际上，使用分布式密钥来解锁服务的访问。认证服务器首先验证用户身份。`AS` 颁发票据授予票据 (`TGT`)，允许用户访问票据授予服务器。随后，`TGS` 给用户另一个票据以用于实际访问服务。在身份验证过程中，用户从未对服务器进行任何形式的直接访问。该过程比描述的要复杂一些。使用当前时间、校验和和可选加密密钥等信息进行的身份验证会随票据一起发送，并由会话密钥解密。服务使用此验证器（authenticator）验证你的身份。

# 注意

你可以使用 `klist` 命令查看当前票据列表。

# 身份验证过程

认证服务器使用其用户数据库中的用户信息。每个用户都需要在认证服务器数据库中注册。数据库将包含用户密码和其他用户信息。要访问认证服务器，用户提供用户名和密码。密码用于生成用户密钥，通过该密钥与 `AS` 的通信将被加密。用户将拥有自己的用户密钥副本，用于解密通信。身份验证过程如图 18-2 所示。

![](img/fb7d950d2a0e9d9b3c4e6f8ab3930.png) 图 18-2：Kerberos 认证

使用 Kerberos 访问服务涉及以下步骤：

1. 用户必须通过认证服务器的验证，并获得票据授予服务器的访问权限。你通过执行 `kinit` 命令来实现此，它会要求输入 Kerberos 用户名（通常与你的用户名相同）。

```
kinit
```

`AS` 颁发票据授予票据 (`TGT`)，允许你访问票据授予服务器。该票据将包含一个会话密钥，用于访问 `TGS`。

`kinit` 程序提示你输入 Kerberos 密码，然后使用该密码解密 `TGT`。你可以使用 `kpasswd` 命令管理你的 Kerberos 密码。现在你使用客户端程序（例如邮件客户端）访问邮件服务器。当你这样做时，`TGT` 被用于访问 `TGS`，随后 `TGS` 生成一个访问邮件服务器的票据。`TGS` 将生成一个新的会话密钥用于该票据。这包含在发送给你的访问邮件服务器的票据中。实际上，有一个访问 `TGS` 的 `TGS` 会话密钥和一个访问邮件服务器的邮件会话密钥。邮件服务器的票据使用 `TGS` 会话密钥加密发送给你。

客户端随后使用从 `TGS` 获取的邮件票据访问邮件服务器。

如果你想使用 `FTP` 等其他服务，当你的 `FTP` 客户端向 `TGS` 请求票据时，`TGS` 将自动从认证服务器获取授权并颁发带有 `FTP` 会话密钥的 `FTP` 票据。这种支持持续一段时间，之后你必须再次运行 `kinit` 以通过验证过程并访问 `TGS`。你可以使用 `kdestroy` 命令手动销毁任何现有票据。

> 注意
>
> Kerberos V5（第五代）提供了一种 Kerberos 登录工具，使用户在正常登录时会自动获得票据授予票据。这避免了手动使用 `kinit` 获取 `TGT` 的需求。

# Kerberos 化服务

设置特定服务使用 Kerberos（称为 Kerberos 化）可能是一个复杂的过程。Kerberos 化服务需要检查用户的身份和凭据、检查用于服务的票据，如果没有票据则获取一个。一旦设置完成，使用 Kerberos 化服务对用户来说几乎是透明的。票据会自动颁发，身份验证无需用户额外操作即可完成。

# 配置 Kerberos 服务器

安装和配置 Kerberos 服务器也是一个复杂的过程。请仔细查阅当前版本的安装文档。这里列出了一些关键项。在 Kerberos 配置文件 `kb5.conf` 中，你可以设置诸如使用的加密方法和数据库名称等功能。在安装 Kerberos 时，务必仔细遵循管理员访问的说明。`/etc/services` 文件应包含所有 Kerberos 服务的列表。这些服务如 `kptf` 或 `login` 等，它们提供了 Kerberos FTP 和登录服务。

要运行 Kerberos，你需要使用 `service` 命令以及 `kr5kdc`、`kadmin` 和 `kr524` 脚本启动 Kerberos 服务器。

### 提示

参考《Red Hat Linux Reference Manual》，获取有关在系统上设置 Kerberos 服务器和客户端的详细说明。

参考《Red Hat Linux Reference Guide》，获取有关如何在 Red Hat 上安装和配置 Kerberos 的详细说明。你需要为你的网络配置服务器，并为每个主机配置客户端。要配置你的服务器，首先指定你的 Kerberos 领域（realm），并手动将 `/etc/krb5.conf` 和 `/var/kerberos/krb5kdc/krb5kdc` 文件中的小写 `example.com` 和大写 `EXAMPLE.COM` 条目替换为你自己的域名。保持每个条目的的大小写一致。领域使用大写，而简单的主机名和域名使用小写。使用 `kdb5_util` 命令和 `create` 选项创建一个数据库。系统会提示你输入主密钥。

```
kdb5_util create -s
```
