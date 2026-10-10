
# 清单 16.15：使用 `rsync` 通过 SSH 安全传输文件

在第三章“管理文件、目录和文本”中介绍过的 `rsync` 实用工具，可以利用 SSH 通过加密隧道快速将文件复制到远程系统。若要在 `rsync` 命令中使用 OpenSSH，需要在目标文件位置前添加 `username@hostname`。清单 16.15 展示了一个示例。

```bash
$ ls -sh Project4x.tar
40K Project4x.tar
$
$ rsync Project4x.tar Christine@192.168.0.105:~
Password:
$
```

在清单 16.15 中，`Project4x.tar` 文件通过 `rsync` 命令和 OpenSSH 被发送到远程系统。请注意，远程系统的用户名和 IP 地址后面加了一个冒号（`:`）。这是为了指定文件正在传输到远程系统。如果没有添加冒号，`rsync` 命令将不会传输该文件。它只会将文件重命名为带有 `Christine@` 前缀加上 IP 地址的名称。

在冒号之后，指定了文件的目录目标位置。`~` 符号表示将文件放置在用户的主目录中。如果需要，您也可以为文件赋予一个新名称。

您还可以使用 `ssh` 命令向远程系统发送命令。只需在 `ssh` 命令的末尾，用引号将命令括起来即可。清单 16.16 展示了一个示例。

# 清单 16.16：使用 `ssh` 向远程系统发送命令

```bash
$ ssh Christine@192.168.0.105 "ls -sh Project4x.tar"
Password:
40K Project4x.tar
$
```

在清单 16.16 中，该命令检查我们的文件是否已成功传输到远程系统。`Project4x.tar` 文件已成功移动。

# 配置 SSH

审查各种 OpenSSH 配置文件及其指令是一个好主意。确保您的加密连接正确配置对于保护远程系统通信至关重要。表 16.7 列出了主要的 OpenSSH 配置文件。

| 配置文件 | 描述 |
| :--- | :--- |
| `~/.ssh/config` | 包含 OpenSSH 客户端配置。可能被 ssh 命令选项覆盖。 |
| `/etc/ssh/ssh_config` | 包含 OpenSSH 客户端配置。可能被 ssh 命令选项或 `~/.ssh/config` 文件中的设置覆盖。 |
| `/etc/ssh/sshd_config` | 包含 OpenSSH 守护进程 (sshd) 的配置。 |

如果您需要修改 SSH 配置，了解需要修改哪个配置文件至关重要。以下指南可以提供帮助：

- 对于个人用户连接到远程系统，创建和/或修改客户端侧的 `~/.ssh/config` 文件。
- 对于所有用户连接到远程系统，创建和修改客户端侧的 `/etc/ssh/ssh_config` 文件。
- 对于传入的 SSH 连接请求，修改服务器侧的 `/etc/ssh/sshd_config` 文件。

![](img/c0a399aca0d18f8822d714ad0a173123_554_0.png)

> 请记住，为了使 SSH 客户端连接成功，除了正确的身份验证外，客户端和远程服务器的 SSH 配置必须兼容。

OpenSSH 有多种配置指令。您可以通过 ssh_config 和 sshd_config 文件的 man 页面浏览所有指令。然而，sshd_config 文件中有几个重要的指令：

- `AllowTcpForwarding`: 允许 SSH 端口转发。（参见第八章，“比较 GULs”。）
- `ForwardX11`: 允许 X11 转发。（参见第八章。）
- `PermitRootLogin`: 允许 root 用户通过 SSH 连接登录。通常应设置为 no。
- `Port`: 设置 OpenSSH 守护进程 (sshd) 监听传入连接请求的端口号。（默认值为 22。）

您可能需要修改客户端的 `ssh_config` 或 `~/.ssh/config` 文件的一个例子是，当远程系统的 SSH 端口在 `sshd_config` 文件中被修改时。在这种情况下，如果客户端配置文件未更改以匹配新端口，远程用户将不得不修改其 `ssh` 命令的选项。清单 16.17 展示了一个片段示例。在此清单中，远程 Ubuntu 服务器的 OpenSSH 监听端口 1138，而不是默认端口 22，用户必须使用 `ssh` 命令的 `-p` 选项才能到达远程服务器。

# 清单 16.17：使用 `ssh` 连接到远程系统的非默认端口

```bash
$ ssh -p 1138 192.168.0.104
[...]
Christine@192.168.0.104's password:
Welcome to Ubuntu 18.04.1 LTS (GNU/Linux 4.15.0-36-generic x86_64)
[...]
Christine@Ubuntu1804:~$
Christine@Ubuntu1804:~$ ip addr show | grep 192.168.0.104
    inet 192.168.0.104/24
[...]
Christine@Ubuntu1804:~$
Christine@Ubuntu1804:~$ exit
logout
Connection to 192.168.0.104 closed.
$
```

为了解决 OpenSSH 客户端用户的这一麻烦，请为个人用户创建或修改 `~/.ssh/config` 文件，或者为所有客户端用户修改 `/etc/ssh/ssh_config` 文件。在配置文件中将 Port 设置为 1138。这会让远程用户和系统管理员都更轻松。

> 系统管理员经常将 OpenSSH 默认端口从端口 22 更改为其他端口。在面向公共网络的服务器上，该端口经常成为恶意攻击者的目标。但是，如果在系统上使用 SELinux 更改 OpenSSH 端口，您需要让 SELinux 知晓此更改。所需的更改通常记录在 SELinux 系统的 `/etc/ssh/sshd_config` 文件顶部。

# 生成 SSH 密钥

通常，OpenSSH 会查找其系统的公钥/私钥对。如果未找到，OpenSSH 会自动生成它们。这些密钥对，也称为*主机密钥*，存储在 `/etc/ssh/` 目录下的文件中。清单 16.18 显示了 Fedora 发行版上的密钥文件。

# 清单 16.18：查看 Fedora 系统上的 OpenSSH 密钥文件

```bash
$ ls -1 /etc/ssh/*key*
/etc/ssh/ssh_host_ecdsa_key
/etc/ssh/ssh_host_ecdsa_key.pub
/etc/ssh/ssh_host_ed25519_key
/etc/ssh/ssh_host_ed25519_key.pub
/etc/ssh/ssh_host_rsa_key
/etc/ssh/ssh_host_rsa_key.pub
$
```

在清单 16.18 中，显示了公钥和私钥文件。公钥文件以 .pub 文件扩展名结尾，而私钥没有文件扩展名。文件名遵循此标准：

`ssh_host_ KeyType_ key`

密钥文件名的 *KeyType* 对应于创建密钥时使用的数字签名算法。您在系统中可能看到的不同类型如下：

- dsa
- rsa
- ecdsa
- ed25519

![](img/c0a399aca0d18f8822d714ad0a173123_556_0.png)

> 妥善保护私钥文件至关重要。私钥文件应具有 0640 或 0600（八进制）权限设置，并由 root 拥有。然而，公钥文件需要任何人可读。文件权限在第十五章“应用所有权和权限”中有所介绍。

有时您可能需要手动生成这些密钥或创建新密钥。为此，需使用 ssh-keygen 实用工具。清单 16.19 在 Fedora 系统上展示了使用此工具的一个片段示例。

# 清单 16.19：使用 ssh-keygen 创建新的公钥/私钥对

```bash
$ sudo ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key
Generating public/private rsa key pair.
/etc/ssh/ssh_host_rsa_key already exists.
Overwrite (y/n)? y
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /etc/ssh/ssh_host_rsa_key.
Your public key has been saved in /etc/ssh/ssh_host_rsa_key.pub.
The key fingerprint is:
[...]
$
```

ssh-keygen 有几个选项。对于清单 16.19 中的命令，只使用了两个选项。`-t` 选项设置 KeyType，在此示例中为 `rsa`。`-f` 开关指定用于存储密钥的私钥文件。公钥存储在具有相同名称但添加了 .pub 文件扩展名的文件中。请注意，此命令会询问密码短语，该密码短语与私钥相关联。

# 使用 SSH 密钥进行身份验证

每次使用 SSH 的命令时输入密码可能会很麻烦。但是，您可以使用密钥而不是密码进行身份验证。设置此身份验证方法需要几个步骤：

1. 登录到 SSH 客户端系统。
2. 生成 SSH ID 密钥对。
3. 安全地将公钥 SSH ID 密钥传输到 SSH 服务器计算机。
4. 登录到 SSH 服务器系统。
5. 在服务器系统上将公钥 SSH ID 密钥添加到 ~/.ssh/authorized_keys 文件。

让我们更详细地看看这些步骤。首先，您应该通过您将要用作 SSH 客户端的账户登录到客户端系统。在该系统上，通过 ssh-keygen 实用工具生成 SSH ID 密钥对。您必须指定正确的密钥对文件名，即 id_TYPE，其中 TYPE 是 dsa、rsa 或 ecdsa。清单 16.20 在客户端系统上创建 SSH ID 密钥对的一个片段示例。

# 清单 16.20：使用 ssh-keygen 创建 SSH ID 密钥对

```bash
$ ssh-keygen -t rsa -f ~/.ssh/id_rsa
Generating public/private rsa key pair.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/Christine/.ssh/id_rsa.
Your public key has been saved in /home/Christine/.ssh/id_rsa.pub.
[...]
$ ls .ssh/
id_rsa  id_rsa.pub  known_hosts
$
```
