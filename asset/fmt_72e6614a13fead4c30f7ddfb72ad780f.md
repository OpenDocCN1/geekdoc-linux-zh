
开放系统管理员会将 OpenSSH 默认端口从 22 更改为另一个端口。在面向公共的服务器上，此端口经常是恶意攻击者的目标。然而，如果您在使用 SELinux 的系统上更改 OpenSSH 端口，将需要让 SELinux 知道此更改。所需的更改通常记录在 SELinux 系统 `/etc/ssh/sshd_config` 文件的顶部。

# 生成 SSH 密钥

通常，OpenSSH 会搜索您系统的公钥/私钥对。如果没有找到，OpenSSH 会自动生成它们。这些密钥对（也称为热密钥）存储在 `/etc/ssh/` 目录的文件。列表 16.18 显示了 Fedora 发行版上的密钥文件。

# 列表 16.18：查看 Fedora 系统上的 OpenSSH 密钥文件

```
$ ls -1 /etc/ssh/*key*
/etc/ssh/ssh_host_ecdsa_key
/etc/ssh/ssh_host_ecdsa_key.pub
/etc/ssh/ssh_host_ed25519_key
/etc/ssh/ssh_host_ed25519_key.pub
/etc/ssh/ssh_host_rsa_key
/etc/ssh/ssh_host_rsa_key.pub
$
```

在列表 16.18 中，显示了私钥和公钥文件。公钥以 `.pub` 文件扩展名结尾，而私钥没有文件扩展名。文件名遵循此标准：

```
ssh_host_KeyType_key
```

密钥文件名中的 `KeyType` 对应创建密钥时使用的数字签名算法。您在系统上可能看到的不同类型如下：

- `dsa`
- `rsa`
- `ecdsa`
- `ed25519`

![](img/0c1e7d2699b9d354c8d2f84669d18d73_516_0.png)

适当保护私钥文件至关重要。私钥文件应具有 `0640` 或 `0600`（八进制）权限设置并归 `root` 所有。然而，公钥文件需要全局可读。权限在第 15 章中介绍。您可能需要手动生成这些密钥或创建新密钥。为了实现这一点，使用了 `ssh-keygen` 工具。列表 16.19 显示了 Fedora 系统上使用该工具的示例片段。

# 列表 16.19：使用 ssh-keygen 创建新的公/私密钥

```
$ sudo ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key
Generating public/private key pair.
/etc/ssh/ssh_host_rsa_key already exists.
Overwrite (y/n)? y
Enter passphrase:
Enter same passphrase:
Your identification has been saved in /etc/ssh/ssh_host_rsa_key.
Your public key has been saved in /etc/ssh/ssh_host_rsa_key.pub.
The key fingerprint is:
$
```

`ssh-keygen` 有许多选项。列表 16.19 中使用了两个。`-t` 选项设置了 `KeyType`，在本示例中为 `rsa`。`-f` 切换指定了存储私钥的文件。公钥存储在相同名称的文件但带有 `.pub` 扩展名。注意此命令请求与私钥相关的短语。

# 使用 SSH 密钥进行验证

每次使用 SSH 命令都输入密码可能很麻烦。但是您可以使用密钥代替密码。设置此方法需要几个步骤：

1. 登录 SSH 客户端系统。
2. 生成密钥对。
3. 安全地将公钥传输到 SSH 服务器。
4. 登录 SSH 服务器。
5. 将公钥添加到服务器上的 `~/.ssh/authorized_keys` 文件。

让我们详细查看这些步骤。首先，应通过作为 SSH 客户端的账户登录客户端系统。在该系统中，通过 `ssh-keygen` 工具生成密钥对。您必须指定正确的密钥文件名，`TYPE` 为 `dsa`、`rsa` 或 `ecdsa`。列表 16.20 显示了在客户端系统创建 SSH 密钥对的示例。

# 列表 16.20：使用 ssh-keygen 创建 SSH 密钥对

```
$ ssh-keygen -t rsa -f ~/.ssh/id_rsa
Generating public/private rsa key pair.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/Christine/.ssh/id_rsa.
Your public key has been saved in /home/Christine/.ssh/id_rsa.pub.
$ ls ~/.ssh/
id_rsa id_rsa.pub known_hosts
$
```

注意列表 16.20：密钥文件名。在此情况下，`ssh-keygen` 命令生成存储在 `~/.ssh/id_rsa` 中的私钥和存储在 `~/.ssh/id_rsa.pub` 中的公钥。如果需要，您可以输入短语。在本情况下没有输入。

一旦在客户端生成了这些密钥，必须将公钥复制到服务器系统。使用安全方法是，`ssh-copy-id` 工具允许您这样做。它不仅复制您的公钥，还将其存储在服务器系统的 `~/.ssh/authorized_keys` 文件中。本质上，它通过一个命令完成了第 3 到第 5 步。列表 16.21 显示了使用该工具的示例片段。

# 列表 16.21：使用 ssh-copy-id 复制 SSH 公钥

```
$ ssh-copy-id -n Christine@192.168.0.104
Would have added the following key(s):
ssh-rsa AAAAB3NaZyc2EAAAADAQABAAAAACAQC8WJRWAXN...==
```

```
$ ssh-copy-id Christine@192.168.0.104
Source of key(s) to be installed: /home/Christine/.ssh/id_rsa.pub
Christine@192.168.0.104's password:
Number of key(s) added: 1
$
```

注意列表 16.21 中首先使用了 `ssh-copy-id -n` 命令。`-n` 选项允许您在不实际执行的情况下查看哪些密钥将被复制和安装到远程系统（空运行）。

下次在列表 16.21 中执行命令时，删除了 `-n` 切换。因此，`id_rsa.pub` 密钥被安全地复制到服务器，并且密钥被安装在 `~/.ssh/authorized_keys` 文件中。注意当使用 `ssh-copy-id` 命令时，用户必须输入密码以允许公钥被复制到服务器。

现在公钥密钥已复制到 SSH 服务器，可以使用 `ssh` 命令从客户端系统连接到服务器系统，而无需输入密码。注意在用 `scp` 命令复制文件时，必须在 IP 地址后添加冒号（`:`）。

# 列表 16.22: 测试无密码 SSH 连接（续）

```
Connection to 192.168.0.104 closed.
$ scp Project4x.tar Christine@192.168.0.104
Project4x.tar 100% 40KB 6.3MB/s 00:00
$ ssh Christine@192.168.0.104
Welcome to Ubuntu 18.04.1 LTS (GNU/Linux 4.15.0-36-generic x86_64)
[-]
Christine@Ubuntu1804:-$ ls
Desktop Downloads Music Project4x.tar Templates
Documents examples.desktop Pictures Public Videos
Christine@Ubuntu1804:-$ exit
Connection to 192.168.0.104 closed.
$ 
```

> 如果你的 Linux 发行版中没有 `ssh-copy-id` 命令，你可以使用 `scp` 命令来复制公密钥。在这种情况下，你必须手动将密钥添加到 `~/.ssh/authorized_keys` 文件的底部。要此操作，请使用 `cat` 命令和 `>>` 符号将公密钥的标准输出重定向并追加到授权密钥文件中。

# 使用身份验证代理（Authentication Agent）认证

另一种通过 SSH 连接到远程系统的方法是通过身份验证代理。使用代理，你只需要输入密码即可启动连接。之后，代理会在代理会话期间记住该密码。设置这种身份验证方法只需要几个步骤：

1. 登录到 SSH 客户端系统。
2. 生成 SSH 密钥对并设置密码短。
3. 将公钥 SSH 密钥安全地传输到 SSH 服务器计算机。
4. 登录到 SSH 服务器系统。
5. 将公钥 SSH 密钥添加到服务器系统上的 `~/.ssh/authorized_keys` 文件。
6. 启动代理会话。
7. 将 SSH 密钥对添加到代理会话中。

步骤 1 到 5 与使用 SSH 密钥对而非密码进行身份验证的设置步骤相同。需要注意的一个例外是，在生成用于代理的 SSH 密钥对时，必须创建一个密码短。设置用于 SSH 代理的 ECDSA 密钥的示例位于列表 16.23 中。

# 列表 16.23: 生成并设置用于 SSH 代理的密钥

```
$ ssh-keygen -t ecdsa f ~/ssh/id_ecdsa
Generating public/private ecdsa key pair.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/Christine/.ssh/id_ecdsa
[--]
$ ssh-copy-id -i ~/ssh/id_ecdsa Christine@192.168.0.104
[--]
Number of key(s) added: 1
[$]
```

一旦你在远程系统上正确创建了带有密码短的密钥对、安全地传输了并安装在服务器的授权密钥文件中，你就可以使用 `ssh-agent` 实用程序启动 SSH 代理会话。会话启动后，通过 `ssh-add` 命令将私钥添加到会话中。此操作示例见列表 16.24。

# 列表 16.24: 启动 SSH 代理会话并添加密钥

```
$ ssh-agent /bin/bash
[Christine@localhost ~]
[Christine@localhost ~]$ ssh-add ~/ssh/id_ecdsa
Enter passphrase for /home/Christine/.ssh/id_ecdsa:
Identity added: /home/Christine/.ssh/id_ecdsa (home/Christine/.ssh/id_ecdsa)
[Christine@localhost ~]
[Christine@localhost ~]$ ssh Christine@192.168.0.104
Welcome to Ubuntu 18.04.1 LTS (GNU/Linux 4.15.0-3-generic x86_64)
[--]
Christine@Ubuntu1804:-$ exit
logout
Connection to 192.168.0.104 closed.
[Christine@localhost ~]
[Christine@localhost ~]$ exit
exit
[$]
```

注意列表 16.24 中的 `ssh-agent` 命令后面跟着的是 `/bin/bash`，这是 Bash Shell。该命令启动了一个运行着 Bash Shell 的新会话，即代理会话。一旦使用 `ssh-add` 命令并输入私密码添加了私钥 SSH 密钥，你就可以连接到远程系统而无需再次输入密码或密码短。然而，如果你退出会话并重新启动，则必须重新添加密钥并重新输入密码短。

> `ssh-add` 命令允许你在需要时从代理会话中删除密钥。包含 `-d` 选项来实现此操作。

SSH 代理会话允许你输入一次会话用户名，然后通过加密的 SSH 方法根据需要连接到远程系统，而无需反复输入密码或密码短。这不仅提供了安全性，还提供了便利性，这是一种罕见的结合。

# 安全地使用 SSH

你可以采取以下措施来增强系统上 SSH 的安全性：

- 使用不同于默认端口 22 的 SSH。
- 禁用通过 SSH 进行 `root` 登录。
- 管理 TCP Wrappers。

本章之前提到的一项内容是不使用 22 端口作为面向公共系统的 SSH 端口。你可以更改它。对于面向公共系统，不使用 22 端口作为 SSH 端口是一项内容。你可以更改它。禁用通过 SSH 进行 `root` 登录是一项内容。对于面向公共系统，不使用 22 端口作为 SSH 端口是一项内容。你可以更改它。

IPSec 互联网协议安全协议（Internet Protocol Security）并不是一种加密协议，而是一个运行在网络层上的框架。它本身并不强制执行特定的密钥方法或加密算法。它通常位于 VPN 应用的核心。

它采用认证头（AH）协议进行身份验证。IPSec 同样使用封装安全负载（ESP）进行身份验证、数据加密、数据完整性等。对于密钥管理，通常使用互联网安全关联和密钥管理协议（ISAKMP），但并非强制要求。

IPSec 有两种模式：隧道模式（tunnel mode）和传输模式（transport mode）。在隧道模式下，数据及其为了传输目的而添加的相关头部（称为`数据报文`）受到保护。因此，没有人能看到任何数据或路由信息，因为整个连接都是安全的。在传输模式下，只有数据受到保护，并由 `ESP` 确保安全。

![](img/0c1e7d2699b9d354c8d2f84669d18d73_524_0.png)

OpenVPN 软件包使用自定义协议，有时被称为 OpenVPN 协议。然而，它确实使用 `SSL/TLS` 进行密钥交换。该软件包是跨平台支持，并且在通过防火墙和 `NAT` 建立 VPN 时没有问题，而 `IPSec` 已知会遭受此类困扰。因此，OpenVPN 软件包非常流行。

安全的 VPN 客户端有很多很好的选择。从为你的环境所需的功能创建一个检查清单是一个很好的开始。

## 总结

评估系统和用户对适当访问和身份验证方法的需求对于确保系统安全至关重要。使用正确的协议并进行正确配置不仅有助于保持系统安全，还能减少用户的挫败感。这也会让你的工作变得更容易。

## 考试要点

总结各种 `PAM` 模块和功能。`PAM` 是应用程序实现身份验证服务的一站式解决方案。应用程序要使用 `PAM`，必须与 `libpam.so` 模块一起编译，并关联相应的 `PAM` 配置文件。配置文件位于 `/etc/pam.d/` 目录。应用程序可以使用三种 `PAM` 模块之一执行强密码——`pam_unix.so`、`pam_pwhistory.so` 以及 `pam_pwquality.so`（后者以前是 `pam_cracklib.so`）。

# 第 16 章 ■ 查看访问和身份验证方法

以及 `pam_pwquality.so`。`PAM` 还可以提供账户锁定以防止暴力攻击。这是通过 `pam_tally.so` 或 `pam_faillock.so` 模块实现的，取决于系统的发行版本。如果你的环境包含 `LDAP`，它也可以与 `PAM` 集成。对应的 `PAM` 模块是 `pam_ldap.so`。
