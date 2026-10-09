
任何 Windows 用户都可以访问此共享，可用于用户之间以及 Linux 和 Windows 系统之间的文件交换。

### 更多信息

- SmoothWall Linux 发行版：`www.smoothwall.org`
- NdisWrapper：`http://ubuntu.com/community/WifiDocs/Driver/Ndiswrapper`
- NdisWrapper：`sourceforge.net/projects/ndiswrapper`
- HOWTOs Linux Wireless Lan HOWTO：`www.hpl.com/personal/Jean_Tourrliches/Linux Wireless HOWTO`
- Linux Hardware Compatibility HOWTO

## 章节总结

局域网（LAN）连接某处的计算机，并允许连接的计算机共享互联网连接、文件和打印机。局域网上的每个系统（或节点）必须有一个网络接口卡（`NIC`）。`NIC` 可以通过电缆（有线）或无线电（无线）连接到网络。

基于以太网的局域网每台计算机与中央集线器交换机之间连接。集线器通常比交换机慢，但对于小型局域网来说，两者都可以接受。无线访问点（`WAP`）将无线网络连接到有线网络。如果你设置的局域网连接到另一个网络（如互联网），则局域网需要一个路由器。路由器可以执行多个功能，其中大部分功能是允许多个系统共享单个互联网连接和 IP 地址；此功能称为 `NAT`。

在设置局域网时，有几个工具非常有用。网络连接窗口（`nm-connection-editor`）和 `nm-applet` 允许你配置 `NIC`（有线或无线）。`iwconfig` 工具配置无线 `NIC` 的元素。

你可以配置局域网上的系统使用 `NIS` 作为登录服务器，这样你就不需要在每个系统上都设置账户。你可以使用 `NFS`（它允许你挂载远程目录层次结构）来设置通用家目录。`Samba` 是许多局域网的重要部分：它允许 Linux 系统参与 Windows 网络，共享目录和打印机，并访问由 Windows 系统共享的目录和打印机。

# 练习

1. 交换机相比集线器有什么优势？
2. 你会设置哪种服务器来允许用户在局域网上的所有计算机上使用相同的用户名和密码登录？
3. 列举两个允许在系统之间共享目录的服务器。
4. 什么是 `WAP`？它有什么作用？
5. 什么是基于以太网的局域网？
6. 路由器可以执行哪些功能？
7. 在设置局域网时，哪些工具是有用的？
8. 你如何配置局域网上的系统使用 `NIS` 作为登录服务器？
9. 你如何使用 `NFS` 设置通用家目录？
10. `Samba` 是许多局域网的重要组成部分，它允许什么？

# OPENSSH 简介

密钥。在随后的连接中，客户端会将服务器提供的密钥与它存储的原始密钥进行比较。虽然此测试并非万无一失，但接下来的测试是非常安全的。

随后，客户端生成一个随机密钥，并使用服务器的公钥和会话密钥对其加密。客户端将此加密后的密钥发送给服务器。服务器随后使用其私钥来解密该加密密钥。此过程创建了一个只有客户端和服务器已知的密钥，并用于加密会话的其他部分。

# 文件

`OpenSSH` 客户端和服务器使用许多文件。全局文件存储在 `/etc/ssh`，用户文件存储在 `~/.ssh` 中。在本节中，每个文件描述中的第一个单词表示是客户端还是服务器使用该文件。

# rhost 认证是一种安全风险

尽管 `OpenSSH` 可以从 `/etc/hosts.equiv`、`/etc/hosts.equiv/~rhosts` 和 `~/.shosts` 获取认证信息，但本文未涵盖这些文件的使用，因为它们存在安全风险。`/etc/ssh/sshd_config` 配置文件的默认设置防止了它们的使用。

# /etc/ssh: 全局文件

本节列出的全局文件出现在 `/etc/ssh` 目录中。它们影响所有用户，但你可以通过 `~/.ssh` 目录中的文件来覆盖它们。

- `moduli` 客户端 服务器 包含 `OpenSSH` 用于建立安全连接的密钥交换信息。请修改此文件。
- `ssh_config` 客户端 全局 `OpenSSH` 配置文件（第 638 页）。这里的条目可以被用户 `~/.ssh/config` 文件中的条目覆盖。
- `sshd_config` 服务器 `sshd` 的配置文件（第 643 页）。
- `ssh_host_rsa_key`, `ssh_host_rsa_key.pub` 服务器 协议版本 2 的 DSA 密钥。这两个文件都应由 `root` 所有。`ssh_host_rsa_key.pub` 公钥文件应允许任何人可读，仅允许所有者写入（644 权限）。`ssh_host_rsa_key` 私钥文件除所有者外，任何人都不应读取或写入（600 权限）。
- `ssh_host_rsa_key`, `ssh_host_rsa_key.pub` 服务器 协议版本 2 的 RSA 密钥。这两个文件都应由 `root` 所有。`ssh_host_rsa_key.pub` 公钥文件应允许任何人可读，仅允许所有者写入（644 权限）。`ssh_host_rsa_key` 私钥文件除所有者外，任何人都不应读取或写入（600 权限）。
- `ssh_known_hosts` 客户端 包含本地系统可以连接的主机的公钥 RSA（默认）密钥。此文件包含的信息与 `~/.ssh/known_hosts` 中的信息相似，但它由管理员设置并供所有用户使用。此文件应由 `root` 所有，并允许任何人可读，仅允许所有者写入（644 权限）。
- `ssrc` 服务器 包含初始化例程。当客户端上的用户连接到服务器时，如果 `~/.ssh/rc` 不存在，`OpenSSH` 会在服务器上 `~/.ssh/environment` 之后、用户 shell 之前运行此脚本。

# ~/.ssh: 用户文件

当用户连接到远程系统时，`OpenSSH` 会创建 `~/.ssh` 目录以及其中的 `known_hosts` 文件。

- `authorized_keys` 服务器 允许用户在不提供登录密码的情况下登录或从一个系统向另一个系统拷贝文件（第 641 页）。然而，取决于密钥的设置方式，用户可能需要提供密码短。除所有者外，任何人都不应能写入此文件。
- `config` 客户端 用户的 `OpenSSH` 配置文件（第 638 页）。这里的条目会覆盖 `/etc/ssh/config` 中的条目。
- `environment` 包含赋值语句，用于在用户使用 `ssh` 登录时定义环境变量。
- `id_dsa`, `id_dsa.pub` 客户端 由 `ssh-keygen` 生成的用户认证 DSA 密钥（第 641 页）。两个 `id_dsa` 文件都应由出现在其所在家目录下的用户所有。`id_dsa.pub` 公钥文件应允许任何人可读，仅允许所有者写入（644 权限）。`id_dsa` 私钥文件除所有者外，任何人都不应读取或写入（600 权限）。
- `id_rsa`, `id_rsa.pub` 客户端 由 `ssh-keygen` 生成的用户认证 RSA 密钥（第 641 页）。两个 `id_rsa` 文件都应由出现在其所在家目录下的用户所有。`id_rsa.pub` 公钥文件应允许任何人可读，仅允许所有者写入（644 权限）。`id_rsa` 私钥文件除所有者外，任何人都不应读取或写入（600 权限）。
- `known_hosts` 包含用户连接过的主机的公钥 RSA（默认）。每当用户连接到新服务器时，`OpenSSH` 都会添加条目（第 632 页）。有关使用 DSA 密钥的信息请参考“`HostKeyAlgorithms`”（第 639 页）。如果 `HashKnownHosts`（第 633 页）设置为 `yes`，文件中的主机名和地址将被哈希处理以提高安全性。
- `rc` 服务器 包含初始化例程。当客户端上的用户连接到服务器时，`OpenSSH` 在用户 shell 启动之前的环境中运行此脚本。如果此文件不存在，`OpenSSH` 运行 `/etc/ssh/ssrc`；如果该文件不存在，`OpenSSH` 运行 `xauth`。

### 更多信息

- man pages：`ssh`, `scp`, `sftp`, `ssh-keygen`, `ssh_config`, `sshd`, `ssh_config`
- Web OpenSSH 页面：`www.openssh.com`
- 搜索 `ssh` 以查找各种 HOWTO

# 运行 ssh, scp 和 sftp OpenSSH 客户端

本节涵盖了设置和使用 `ssh`、`scp` 和 `sftp` 客户端。

# 前提条件

`OpenSSH` 默认安装了 `openssh-client` 软件包。你不需要安装任何包。

# 启动：使用 ssh 和 scp 连接到 OpenSSH 服务器

为了安全地连接并使用远程服务器，必须满足以下条件：`sshd` 服务正在运行，你在远程系统上有一个账户，并且服务器向客户端标识其身份。

以下示例显示了使用 `ssh` 连接到 `plum`，这在本地系统上显示为：

```
$ ssh@plum

plum@s password:

Last login Mon Jan 23 21:58 from 192.168.0.2
```

在响应上述查询之前，请确保你正在登录的是正确的系统而不是冒充者。如果你不确定，可以给本地的人打电话以帮助验证你是否所在的系统。当你回答 `yes`（必须）时，它将打开并将服务器的公钥（服务器上 `/etc/ssh/ssh_host_rsa.pub` 或 `/etc/ssh/ssh_host_dsa.pub` 中的单行）连接到本地系统的 `~/.ssh/known_hosts` 文件，必要时会创建 `~/.ssh` 目录。为了能够跟踪 `known_hosts` 中的哪行对应哪个服务器，`OpenSSH` 在行开头添加了服务器名称和服务器的 IP 地址。

当你随后使用 `OpenSSH` 连接到该服务器时，客户端将通过与服务器提供的密钥进行比较，验证其连接到了正确的服务器。你可以使用 `ssh-keygen` 显示本地系统的 RSA 密钥指纹：

```
$ ssh-keygen -f /etc/ssh/ssh_host_rsa_key.pub

2048 d1:9d:1b:5b:75:c8:e9:4b:41:a9:b7:ea:al /etc/ssh/ssh_host_rsa_key.pub (RSA)
```

当你第一次连接到 `OpenSSH` 服务器时，客户端会提示你确认你是否连接到正确的系统。此检查有助于防止中间人攻击（第 106 页脚注 3）：

> 无法验证主机 'plum (192.168.0.10)' 的真实性。
> RSA 密钥指纹为 d1:9d:1b:5b:75:c8:e9:4b:41:a9:b7:ea。
> 你确定要继续连接吗 (yes/no)?
> 警告：已将 'plum,192.168.0.10 [RSA]' 永久添加到主机列表中。

# 配置 OpenSSH 客户端

本节描述了如何在客户端侧设置 `OpenSSH`。

# 推荐设置

你可能想要更改的一个 `OpenSSH` 参数是 `StrictHostTrust`，默认设置为 `yes`。为了提高安全性，可以在 `/etc/ssh/config` 文件中将其设置为 `no`。

# 服务器认证/已知主机

`known_hosts` 文件使用一个或两行长行来识别它跟踪的每个主机。每行都以对应系统的主机名和 IP 地址开头，随后是使用的加密类型和服务器的公

主机密钥。当 `HashKnownHosts`（第 639 页）设置为 `yes`（默认值）时，`OpenSSH` 为了安全起会对系统名称和地址进行哈希。由于它分别对主机名和 IP 地址进行哈希，`OpenSSH` 为每个主机放置两行。以下几行是两个逻辑行，每一行都在多个物理（行）上运行。来自 `known_hosts` 的行用于连接到远程系统进行 RSA（第 1130 页）加密：

```bash
$ cat ~/.ssh/known_hosts

|1PrVuqXFVnVLRykmq1BCynmXaZc=IVRAwataq1529guFR5js3f1AR8=sssh-rsa

AAAAB3Nza1yc22AAAABiwAAQEA7eg4Ya00j5/JGGult3jqc5Rfc8/RUIXkZDAqJ5fe
```

```bash
|1Pnu8BB9UUqc2EAAWICI1UT8yq=Ldm5/7lK6gw84521mw29job8= ssh-rsa

AAAAB3Nza1yc2AAAABiwAAQEA7eg4Ya00j5/JGGult3jqc5Rfc8/RUIXkZDAqJ5fe
```

你可以使用 `ssh-keygen` 的 `-R` 选项通过名称删除主机名。`ssh-keygen` 的 `-F` 选项用于显示 `known_hosts` 文件中响应指定系统的行，即使该条目是如下的：

```bash
$ ssh-keygen -F plum

# Host plum found: line 1 type RSA

|1PrVuqXFVnVLRykmq1BCynmXaZc=IVRAwataq1529guFR5js3f1AR8= ssha-rsa

AAAAB3Nza1yc2AAAABiwAAQEA7eg4Ya00j5/JGGult3jqc5Rfc8/RUIXkZDAqJ5fe
```

`OpenSSH` 自动将连接过的服务器的密钥存储在用户私有文件（`~/.ssh/known_hosts`）中。这些文件仅对其所在目录的用户有效。通过 `root` 权限操作并使用文本编辑器，你可以将用户已知主机列表中的非哈希行复制到 `/etc/ssh/ssh_known_hosts` 中的公共列表中，以便使服务器在本地系统上全局可见。

以下示例显示了具有管理权限的 `Sam` 如何将他 `known_hosts` 中的一个哈希条目放入全局的 `ssh_known_hosts` 文件中。首先，`Sam` 以自己的身份运行，将 `ssh-keygen` 的输出通过 `tail` 剥离并重定向到 `tmp_known_hosts`。接下来，`Sam` 以 `root` 权限运行，将刚刚创建的文件内容追加到 `/etc/ssh/ssh_known_hosts`。如果该文件不存在，此命令将创建它。最后，`Sam` 删除了创建的临时文件并返回到自己的身份。

```bash
sam@:~$ ssh-keygen -F plum | tail -1 > tmp_known_hosts

sam@:~$ sudo -i

root@:$# cat ~/tmp_known_hosts >> /etc/ssh/ssh_known_hosts

root@:$# exit

sam@~$ rm ~/tmp_known_hosts
```

由于 `cat` 的输出被重定向了，`Sam` 创建了一个具有 `root` 权限（`sudo`）的 shell 来执行该命令。关于在 `sudo` 下运行命令输出的讨论，请参阅第 408 页。

# 第 18 章 OpenSSH：安全网络通信

如果在远程系统的公钥存储在 `known-hosts` 文件之一后，当系统连接时远程系统提供了不同的指纹，`OpenSSH` 将显示以下消息且不完成连接：

```
@ WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!

有人可能正在做某些坏事！
现在可能正在窃听你的（中间人攻击！）
也可能是 RSA 密钥已被更改。
由远程主机发送的 RSA 密钥指纹为

fi6f:ea:a7:bb:1bf:df:cd:a5:24:60:d3:25:b1:0a.

请联系你的系统管理员。
在 ~/.ssh/known_hosts 中添加正确的主机密钥以消除此消息。
~/.ssh/known_hosts:1 中的违规密钥：
plum 的 RSA 密钥已更改，且你请求了严格检查。
主机密钥验证失败。
```

如果你看到此消息，你可能是中间人攻击的目标。然而，更有可能的是远程系统上的某些内容发生了变化，导致它提供了新的指纹。向远程系统的管理员确认。如果一切正常，请从指定文件中删除违规密钥（倒数第三行）并尝试重新连接。你可以使用 `ssh-keygen` 的 `-R` 选项通过名称删除哈希条目。你将面临首次认证（第 632 页），因为 `OpenSSH` 会验证你正在连接到正确的系统。遵循与最初连接远程主机时相同的步骤。

# ssh：连接到远程系统或在其执行命令

`ssh` 命令行的格式为

```bash
ssh [options] [user@][host][command]
```

其中，要连接的 `OpenSSH` 服务器（远程系统）的 `host` 是唯一必需的参数。`host` 可以本地系统名称、互联网上系统的 `FQDN`（第 109 页）或 IP 地址。使用命令 `ssh host` 以你在本地系统上使用的用户名登录远程系统。当你想要使用本地系统上以外的用户名登录时，请使用 `user@`。根据服务器的设置方式，你可能需要提供密码。如果不带命令，`ssh` 会登录到 `host`。远程系统显示一个 shell 并提示你在 `host` 上运行命令。使用命令 `exit` 关闭到 `host` 的连接并返回本地系统的提示符。在下面的示例中，已登录到 `host` 的 `Sam` 使用 `ssh` 登录到 `plum`，使用显示系统 IP 地址的命令是

# ssh, scp, sftp 客户端

已登录，并使用 `exit` 关闭到 `plum` 的连接并返回到本地系统的提示符：

```bash
sam@dog:~$ ssh plum

sam@plum's password:

Linux 2.6.27-generic #1 SMP Aug 23 23:20 UTC 28

Last login: Jan 19 22:00 from 192.168.0.12

sam@plum~$ who am

sam

sam@plum~$ hostname -I

10.0.0.1

sam@plum~$ exit

Connection to plum closed.

sam@dog:~$
```
