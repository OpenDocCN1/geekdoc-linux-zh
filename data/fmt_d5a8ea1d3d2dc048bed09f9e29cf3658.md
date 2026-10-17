
建议使用受密码保护的公私密钥对 SSH 传输进行身份验证。与 PGP 不同，SSH 仅在身份验证过程中使用公钥加密。一旦验证通过，参与者将约定一种共同算法来加密传输。身份验证将验证双方的身份。每个意图使用 SSH 访问远程账户的用户都需要创建带有密码保护的公钥和私钥用于身份验证过程。用户将其公钥发送到想要访问的远程账户并将其安装在该账户上。当用户尝试访问远程账户时，账户可以使用该用户的公钥来验证该用户确实是其所声称的。为了让用户访问账户，他们必须知道远程账户的密码。SSH 通常用于用户在不同系统上拥有两个或多个账户，并希望能够相互安全地访问它们的情况。

在这种情况下，用户已经拥有每个账户的访问权限并可以在每个账户上安装 SSH，并提供自己的私钥、公钥以及密码。

### 身份验证

SSH 版本 1 和版本 2 的身份验证机制略有不同。然而，用户端的操作步骤是相同的。本质上，用户创建公钥和私钥。为此此，你使用 `ssh-keygen` 命令。然后将用户的公钥用于分发给原始用户授予访问权限的人。这通常是用户在另一个主机上的账户。密码进一步保护了访问。原始用户需要知道另一个用户的密码才能访问它。

SSH 版本 1 使用 RSA 身份验证。当远程用户尝试登录账户时，将检查该账户是否具有远程用户的公钥。该密钥随后被用于加密一个挑战（通常是一个随机数），该挑战只有远程用户的私钥可以解密。当用户用私钥解密挑战时，SSH 版本 2 可以使用 RSA 或 DSA 身份验证。远程用户首先使用其密钥加密会话标识符并签名。加密后的会话标识符由账户使用远程用户的公钥解密。会话标识符此前由 SSH 为会话设置完毕。

SSH 身份验证首先对主机进行，然后对用户进行。每个主机都有自己的用于身份验证的公钥和私钥。一旦主机通过验证，将对用户进行查询。每个用户都有自己的公钥和私钥。在接收远程用户连接的 SSH 服务器上，必须保留这些远程用户的公钥列表。同样，SSH 主机将维护一个其他 SSH 主机的公钥列表。

### SSH 软件包、工具和服务器

Linux 系统通过 OpenSSH 实现 SSH。OpenSSH 全软件包包括 OpenSSH 元包 (`ssh`)、OpenSSH 服务器 (`openssh-server`) 和 OpenSSH 客户端 (`openssh-client`)。这些包还需要 OpenSSL (`openssl`)，它安装了 SSH 使用的加密库。

SSH 工具如表 13-2 所示。它们包括几个客户端程序如 `scp`、`ssh`，以及 `ssh` 服务器。`ssh` 服务器 (`sshd`) 允许任何人通过 ssh 客户端从外部建立安全连接。还包含了一些配置选项，例如 `ssh-add`，它将有效主机添加到身份验证代理中，以及 `ssh-keygen`，它生成用于加密的密钥。

对于版本 2，实际工具的名称带有 2 后缀。版本 1 的工具以 1 为后缀。在安装期间，如果你安装了版本 2，则每个工具都设置了链接，仅使用带后缀的名称。例如，如果你安装了版本 2，则会使用带后缀的名称。此。

# 第 13 章：SSH、Kerberos 和 IPsec

| 应用 | 描述 |
| --- | --- |
| ssh | SSH 客户端 |
| sshd | SSH 服务器（守护进程） |
| sftp | SSH 客户端，安全文件传输程序。仅限版本 2。使用 -l 列出命令（SFTP 协议） |
| sftp-server | SSH 服务器。版本2 |
| scp | SSH 拷贝命令客户端 |
| ssh-keygen | 生成密钥的工具。使用 -h 查看帮助 |
| ssh-keyscan | 用于自动收集主机密钥以生成 known_hosts 文件的工具 |
| ssh-add | 将 RSA 和 DSA 标识添加到身份验证代理 |
| ssh-agent | 持有公钥私钥的身份验证代理 |
| ssh-askpass | 用于询问密码的 X 系统，由 ssh-add 调用 |
| ssh-askpass-gnome | 用于询问密码的 GNOME 工具，由 ssh-add 调用 |
| ssh-signer | 签名主机身份验证包。仅限版本 2。由安装执行 |
| login | 远程登录 |

**表 13-3：SSH 工具**

你可以通过 **system-config-services**（系统 | 管理 | 服务）配置 Openssh 服务器 (`sshd`) 自动启动。你可以使用 **`/etc/init.d/sshd`** 脚本手动启动、停止和重启服务器。

```
sudo /etc/init.d/sshd restart
```

### SSH 设置

使用 SSH 涉及创建你的公钥和私钥，并将你的公钥分发给想要访问的其他用户。这些可以是不同的用户，也可以是你远程系统上的简单用户账户。人们经常从本地客户端远程登录到远程服务器上的账户，例如从家里电脑登录到公司电脑。你的家

# 318 第2 部分：安全

计算机将是你的客户端账户，而公司电脑上的账户将是你的服务器账户。在客户端账户上，你需要生成公钥和私钥，然后将公钥的副本放在服务器账户中。你可以简单通过电子邮件发送密钥或将副本保存在软磁盘上来实现。你服务器上的账户拥有你客户端公钥的副本，你可以从客户端账户访问服务器账户。系统会提示你输入服务器账户的短语。图 13-1 展示了允许用户 george 访问账户 cecelia 的 SSH 设置。

![](img/74df054815dc70d661e697bc3d5ff87a_319_0.png)

## 图 13-1：SSH 设置与访问

为了允许你使用 SSH 访问其他账户：

- 你必须在你的账户上创建公钥和私钥，并设置一个短语。你需要使用这个短语从另一个账户访问你的账户。
- 你必须将你的公钥分发到你想要访问的其他账户，将其放在 `~/.ssh/authorized_keys` 文件中。
- 其他账户也必须设置公钥、私钥以及短语。
- 你必须知道另一个账户的短语才能访问它。

### 使用 ssh-keygen 创建 SSH 密钥

你使用 `ssh-keygen` 命令创建公钥和私钥。你需要指定想要使用的加密类型。你可以使用 DSA 或 RSA 加密。使用 `-t` 选项指定类型，并使用小写的加密名称（dsa 或 rsa）。在下面的示例中，你使用 RSA 加密创建了一个密钥：

```
ssh-keygen -t rsa
```

`ssh-keygen` 命令会提示你输入短语，它将将其作为一种密码来保护你的私钥。短语长度应该是几个单词。系统还会提示你为密钥输入一个文件名。如果你不输入，SSH 将使用默认值。公钥将获得 `.pub` 扩展名。`ssh-keygen` 命令生成公钥并将其放在你的 `.ssh/id_rsa.pub` 或 `/ssh/id_dsa.pub` 文件中，取决于你指定的密钥类型；将私钥放在对应的 `.ssh/id_rsa` 或 `.ssh/id_dsa` 文件中。

如果你需要更改短语，可以使用 `ssh-keygen` 命令和 `-p` 选项。每个用户将有自己的 SSH 配置目录，称为 `.ssh`，位于他们自己的家目录中。公钥、私钥以及 SSH 配置文件都放在这里。如果你从源码编译，`make install` 操作将自动运行 `ssh-keygen`。表 13-3 列出了 SSH 配置文件。

| 文件 | 描述 |
| :--- | :--- |
| $HOME/.ssh/known_hosts | 记录用户登录过的所有主机的主机密钥（不在 `/etc/ssh/ssh_known_hosts` 中的）。 |
| $HOME/.ssh/random_seed | 为随机数生成器提供种子。 |
| $HOME/.ssh/id_rsa | 包含用户的 RSA 认证身份。 |
| $HOME/.ssh/id_dsa | 包含用户的 DSA 认证身份。 |
| $HOME/.ssh/id_rsa.pub | 包含用于认证的 RSA 公钥。此文件的内容应添加到所有你想要使用 RSA 认证登录的机器的 `$HOME/.ssh/authorized_keys` 中。 |
| $HOME/.ssh/id_dsa.pub | 包含用于认证的 DSA 公钥。 |
| $HOME/.ssh/config | 包含每个用户的配置文件。 |
| $HOME/.ssh/authorized_keys | 列出可以作为此用户登录的 RSA 或 DSA 密钥。 |
| /etc/ssh/ssh_known_hosts | 包含系统的已知主机密钥列表。 |
| /etc/ssh/ssh_config | 包含系统级配置文件。此文件为用户配置中未指定的值提供了默认值。 |
| /etc/ssh/sshd_config | 包含 SSH 服务器配置文件。 |
| /etc/ssh/ssshrc | 包含系统默认。此文件中的命令会在用户登录时，在其 shell（或命令）启动之前由 ssh 执行。 |
| $HOME/.ssh/rc | 包含在用户登录时，在其 shell（或命令）启动之前由 ssh 执行的命令。 |

表 13-3：SSH 配置文件

### 授权密钥 (Authorized Keys)

公钥用于验证用户及其主机。你在远程系统上使用公钥来允许该访问权限。公钥被放置在远程用户账户的 `.ssh/authorized_keys` 文件中。回想一下，公钥存储在 `.ssh/id_dsa.pub` 文件中。如果用户想从本地账户远程登录到远程系统上的账户，他们首先会将其公钥放在想要访问的远程系统账户的 `.ssh/authorized_keys` 文件中。如果 `turtle.mytrek.com` 上的用户 larisa 想要访问 `rabbit.mytrek.com` 上的 aleina 账户，那么 larisa 位于 `/home/larisa/.ssh/id_dsa.pub` 的公钥应该首先被放在 aleina 的 `authorized_keys` 文件 `/home/aleina/.ssh/authorized_keys` 中。

第 2 部分：安全（第 321 页）用户 larisa 可以发送密钥或让其复制过去。一个简单的 `cat` 操作可以将密钥添加到密钥文件中。在下一个示例中，用户将 `larisa.pub` 中的公钥添加到授权密钥文件中。`larisa.pub` 文件是用户之前收到的 `/home/larisa/.ssh/id_dsa.pub` 副本。

```
cat larisa.pub >> .ssh/authorized_keys
```

注意：你也可以使用 seahorse 创建并管理 SSH 密钥。注意：`.ssh/identity` 文件名用于 SSH 版本 1；它在旧发行版中可能是默认安装的。SSH 版本 2 使用不同的文件名 `.ssh/id_dsa` 或 `.ssh/id_rsa`，取决于使用的是 RSA  DSA 认证。

### 加载密钥

如果你经常连接到远程主机，使用 `ssh-agent` 命令将私钥放在内存中，以便快速访问并解密传输。`ssh-agent` 命令用于登录会话开始。对于 GNOME，你可以使用 openssh-askpass。

## 第 13 章：SSH、Kerberos 和 IPSec 319（第 320 页）

（注意：OCR 文本在 `ssh-agent` 部分有大量重复，已进行去重处理以便清晰。）

## 第2部分：安全

```bash
[george@turtle]$ scp cecelia@turtle.mytrek.com:mydoc
cecelia@turtle.mytrek.com's password: | 0 ---
ETA
mydoc 100% |************************* 17 00:00
[george@turtle]$
```

来自 Windows 系统，你可以使用如 winscp 等 scp 客户端，它们可以与启用了 scp 的 Linux 系统交互。

### sftp 和 sftp-server

通过 sftp，你可以传输受加密保护的 FTP 文件。sftp 程序使用与 ftp 相同的命令。该客户端仅适用于 ssh 版本 2，其工作方式与 ftp 类似，具有许多相同的命令。使用 sftp 代替 ftp 来调用 sftp 客户端。

```bash
sftp download.fedora.redhat.com
```

要使用 sftp 客户端连接到 FTP 服务器，该服务器需要运行 sftp-server 应用程序。ssh 服务器调用 sftp-server 以通过 sftp 客户端提供加密的 FTP 传输。sftp 服务器客户端使用 SSH 文件传输协议 (SFTP) 来安全地执行 FTP 操作。

### 端口转发（隧道技术）

由于某种原因，你只能通过一个不安全的主机连接到安全主机，此时 ssh 提供了一项名为端口转发的功能。通过端口转发，你可以保护连接中的不安全部分。这只需要指定不安全主机要连接到安全主机的端口即可。这通过中间主机在本地主机和远程主机之间建立直接连接。加密数据将直接通过。这被称为隧道技术（tunneling），即通过连接的服务器创建一个安全的数据隧道。

你可以设置端口转发到远程系统的端口或你的本地系统。要将远程系统的端口转发到本地系统的端口，请使用带有 -R 选项的 ssh，后面跟着一个包含本地端口、远程主机地址和要转发的远程端口的参数，参数之间用冒号分隔。通过分配一个套接字来监听远程端口。每当连接到此端口时，连接将安全通道转发，并从本地机器连接到远程端口。在以下示例中，本地系统的 22 端口连接到 rabbit.mytrek.com 远程系统的 23 端口：

```bash
ssh -R 22:rabbit.mytrek.com:23
```

要将本地系统的端口转发到远程系统的端口，请使用带有 -L 选项的 ssh，后面跟着一个包含本地端口、远程主机地址和要转发的远程端口的参数，参数之间用冒号分隔。分配一个套接字来监听本地侧端口。每当连接到此端口时，连接将通过安全通道转发，并连接到远程机器上的远程端口。在以下示例中，本地系统的 22 端口连接到 rabbit.mytrek.com 远程系统的 23 端口：

```bash
ssh -L 22:rabbit.mytrek.com:23
```

## 第13章：SSH、Kerberos 和 IPSec

你可以在 `.ssh/config` 文件中使用 `LocalForward` 和 `RemoteForward` 选项来为特定主机设置端口转发，或者为你连接的所有主机指定一个默认值。

### SSH 配置

每个用户的 SSH 配置文件位于你的 `.ssh/config` 文件中。`/etc/ssh/ssh_config` 文件用于设置 SSH 客户端全局默认值。在配置文件中，你可以设置 ssh_config 手册中列出的各种选项。该配置文件旨在为你可能连接的远程主机指定选项。它被组织成若干段，每个段以关键字 HOST 开头，后跟主机的 IP 地址。接下来的行包含了该段拥有的选项。一个段在下一个 HOST 条目处结束。特别感兴趣的是 User 和 Cipher 选项。使用 User 选项指定远程系统上允许访问的用户名称。通过 Cipher 选项，你可以为特定主机选择使用的加密方法。加密方法包括 IDEA、DES（标准）、三次 DES (3DES)、Blowfish (128 位)、Arcfour (RSA 的 RC4) 和 Twofish。以下示例允许来自 turtle.mytrek.com 的 larisa 访问，并使用 Blowfish 加密进行传输：

```text
Host turtle.mytrek.com
    User larisa
    Compression no
    Cipher blowfish
```

大多数标准选项（包括加密算法）已作为注释项列出。删除 # 即可激活。

```text
# Ciphers aes128-cbc, 3des-cbc, blowfish-cbc, cast128-cbc, arcfour, aes192-cbc, aes256-cbc
```

要指定适用于你连接的任何主机的全局选项，创建一个以星号作为主机的 HOST 条目，即 HOST *。此条目必须放在配置文件的末尾，因为选项仅在首次设置时更改。该选项的任何后续条目将被忽略。由于主机既匹配自身的条目也匹配全局条目，其特定条目应放在全局条目之前。星号 (*) 和问号 (?) 都是通配符匹配运算符，允许你指定具有相同后缀或前缀的主机组。

```text
Host *
    FallBackToRsh yes
    KeepAlive 30
    Cipher 3des
```

protocol 选项允许你指定使用的 SSH 版本，1、2 或两者。为了向后兼容，两种协议都是接受的。你可以将其限制为 2。

（注：此处原文中存在大量重复的 protocol 描述，已根据指令进行去重处理）

### Kerberos

## 第2部分：安全

### Kerberos

Kerberos 的关键是一个 Kerberos 服务器，所有对服务的请求都通过它进行。Kerberos 服务器随后验证客户端，识别并验证客户端使用特定服务器的权限。服务器维护一个授权用户数据库。然后 Kerberos 发放一个加密票据，客户端可以使用它访问服务器。例如，如果用户需要检查邮件，对邮件服务器使用的请求将发送到 Kerberos 服务器，服务器随后验证用户并发放用于访问邮件服务器的票据。没有 Kerberos 发的票据，无人能访问任何服务器。最初，此过程需要用户对每个服务器执行单独的验证程序。每个 Fedora 默认安装 Kerberos 支持库。你可以使用 kb5 包安装 Kerberos 服务器和多个客户端。服务器是 kb5-server，它还会安装 kde，而 kb5-workstation 将安装如 admin 等用于管理 Kerberos 服务器的应用程序。kb5-workstation-clients 包包含了 ssh、telnet 和 ftp 客户端的 Kerberos 安全替代品。针对 PAM、Python、LDAP、Perl 和 Ruby 也提供了 Kerberos 安全服务器插件。操作安全的 LDAP 服务器需要 LDAP 插件。
