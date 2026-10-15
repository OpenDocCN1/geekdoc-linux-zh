
注意 虽然 OpenSSH 可以从 `/etc/hosts`、`/etc/.hosts` 和 `~/.hosts` 获取认证信息，但本章不涵盖这些文件的使用，因为它们存在风险。`etc/ssh/sshd_config` 配置文件的默认设置阻止了它们的使用。

# `/etc/ssh`：全局文件

本节列出的全局文件出现在 `/etc/ssh` 目录。它们影响所有用户，用户可以使用 `~/.ssh` 中的文件覆盖它们。

## `ssh_config` 客户端
包含 OpenSSH 用于建立安全连接的密钥信息。不要修改此文件。

## `ssh_config` 服务器
全局 OpenSSH 配置文件（第 674 页）。这里的条目会被 `~/.ssh/config` 中的条目覆盖。

## `ssh_host_dsa_key`, 服务器
这两个文件都由 `root` 所有。`ssh_host_dsa_key` 公钥应允许所有者读取和写入（权限 `644`）。`ssh_host_dsa_key` 私钥不应允许 `root` 以外的用户读取或写入（权限 `600`）。

## `ssh_host_rsa_key`, 服务器
这两个文件都由 `root` 所有。`ssh_host_rsa_key` 公钥应允许所有者读取和写入（权限 `644`）。`ssh_host_rsa_key` 私钥不应允许 `root` 以外的用户读取或写入（权限 `600`）。

## `ssh_known_hosts` 客户端
包含本地系统可以连接的主机（默认）公钥。该文件包含与 `~/.ssh/known_hosts` 类似的信息，但由管理员设置并供所有用户使用。

此文件应由 `root` 所有，并且任何人都可以读取，但仅允许所有者进行写入（`644` 权限）。

- `ssh server` 包含初始化例程。当客户端上的用户连接到服务器时，如果 `~/.ssh/rc` 不存在，OpenSSH 会在 `~/.ssh/environment` 之后、用户 shell 启动之前在服务器上运行此脚本。

# `~/.ssh`: 用户文件

当用户连接到远程服务器时，OpenSSH 会创建 `~/.ssh` 目录以及位于创建的 `known_hosts` 文件。

- `authorized_keys` server 允许用户在不提供用户密码的情况下登录另一个系统，或在两个系统之间复制文件（见第 677 页）。然而，取决于密钥的设置方式，用户可能需要提供密码短。除了所有者外，无人可以

- `config` 用户的 OpenSSH 配置文件（见第 674 页）。此处的条目将覆盖 `/etc/ssh/ssh_config` 中的条目。

- `environment` 包含赋值语句，当用户使用 `ssh` 加载时，定义服务器上的环境变量。

- `id_rsa_pub` 由 `ssh-keygen` 生成的客户端身份认证 DSA 密钥（见第 677 页）。这两个文件都应由其所在家目录的用户所有。`id_rsa.pub` 公钥文件任何人都可以读取，但仅允许所有者写入（`644` 权限）。`dsa` 私钥文件除所有者外，任何人不能读取或写入（`600` 权限）。

- `id_rsa` 由 `ssh-keygen` 生成的客户端身份认证 RSA 密钥（见第 677 页）。`id_rsa.pub` 公钥文件任何人都可以读取，但仅允许所有者写入（`644` 权限）。`id_rsa` 私钥文件除所有者外，任何人不能读取或写入（`600` 权限）。

- `known_hosts` 包含（默认情况下）已连接主机的公钥。每当用户连接到新服务器时，OpenSSH 会自动添加条目（见第 668 页）。有关使用 DSA 密钥的信息，请参阅“KeyAlgorithms”（见第 675 页）。如果 `HashHosts`（见第 675 页）设置为 `yes`，此文件中的主机名和地址将进行哈希处理以提高安全性。

- `server` 包含初始化例程。当客户端上的用户连接到服务器时，OpenSSH 会在 `environment` 之后、用户 shell 启动之前在服务器上运行此脚本。如果此文件不存在，OpenSSH 将运行 `/etc/ssh/sshd`；如果该文件不存在，OpenSSH 将运行 `catch`。

## 更多信息

- 手页：`ssh`, `scp`, `sftp`, `ssh-keygen`, `config`, `sshd`, `ssh_config`

- OpenSSH 首页：`www.openssh.com`

- 在 `ssh` 上搜索以查找各种 HOWTO 其他文档：`tldp.org`

# 运行 `ssh`, `scp`, 和 `sftp` OpenSSH 客户端 667

书籍 *Implementing SSH: Strategies for Optimizing the Secure Shell*，Dwivedi 著；John Wiley & Sons (2003年10月)

*SSH, The Secure Shell: The Definitive Guide*，Barrett, Silverman, & Byrne 著；O'Reilly Media (2005年5月)

# 运行 `ssh`, `scp` 和 `sftp` OpenSSH 客户端

本节介绍了设置和使用 `ssh`、`scp` 和 `sftp` 客户端。

# 前提条件

默认安装了 `openssh-client` 包。运行 OpenSSH 客户端不需要安装任何包。OpenSSH 客户端没有初始化脚本。

# 快速入门：使用 `ssh` 和 `scp` 连接到 OpenSSH 服务器

`ssh` 和 `scp` 客户端除了安装必要的包之外不需要额外设置，你也可以创建和编辑它们使用的文件。要在远程系统之间安全地复制文件并运行一个安全 shell，必须满足以下条件：远程系统必须运行着 OpenSSH 守护进程 (`sshd`)，你在远程系统上有一个账户，并且服务器必须向客户端确认自身的身份。

以下示例显示了 Zach 如何使用 `ssh` 登录到名为 `plum` 的远程主机，并给出退出命令返回本地系统：

```
$ ssh zachplum
zachplum's password:
Linux plum 2.6.27-1-generic #1 SMP Sat Aug 23 23:20:09 UTC 2008 1686

Last login: Mon Jan 18 21:58:22 2010 from 192.168.0.12
zachplum:~$ exit
logout
Connection to plum closed.
```

如果你想以自己的身份登录并且两个系统上的用户名相同，可以从命令行中省略用户（在上面的示例中为 `zach@`）。第一次连接到远程 OpenSSH 服务器时，`ssh` 或 `scp` 会要求你确认你已连接到正确的系统。请参阅第 668 页的“首次身份验证”。

以下示例使用 `scp` 将 `tyl` 从本地系统的工作目录复制到 Zach 在 `plum` 上的家目录：

```
$ scp tyl zachplum:
zach@plum's password:
100% 162    0.2KB/s    00:00
tyl
```

# 配置 OpenSSH 客户端

本节介绍了如何在客户端侧设置 OpenSSH。

# 推荐设置

Ubuntu 提供的配置文件建立了一个最安全的系统，但可能无法满足你的需求。你可能想要更改的一个 OpenSSH 参数是 `ForwardX11Trusted`，它是默认开启的。为了增加安全性，并在某些情况下降低易用性，请在 `/etc/ssh/sshd_config` 文件中将 `ForwardX11Trusted`（见第 673 页）设置为 `no`。有关 X11 转发的更多信息，请参阅第 68 页。

# 服务器身份验证/KNOWN Hosts

`known hosts` 列出了已连接的主机。OpenSSH 自动在每次用户连接到新服务器时添加条目（见第 668 页）。有关使用 DSA 密钥的信息，请参阅“KeyAlgorithms”（见第 675 页）。如果 `HashHosts`（见第 675 页）设置为 `yes`，此文件中的主机名和地址将进行哈希处理以提高安全性。

# 运行 `ssh`, `scp`, 和 `sftp` OpenSSH 客户端

# 670 第 18 章 OpenSSH：安全网络通信

如果远程系统的公钥已存储在已知的 `known-hosts` 文件中，当系统连接时，远程系统提供了不同的指纹，OpenSSH 将显示以下消息且不完成连接：

```
警告：远程主机标识已更改！
可能有人正在进行某些不良操作！
```

现在可能有人监听你的通信（中间人攻击）！主机密钥可能刚刚发生了更改。

远程主机设置的 RSA 密钥指纹为：

nf16:fea87:bb1b:dcde3:4a24:66d3:25b1:8ba。

请联系您的系统管理员。

在 `/home/sam/ssh/known_hosts` 中添加正确的密钥以消除此消息。

`/home/sam/ssh/known_hosts` 中的违规密钥：

针对 `plum` 的 RSA 密钥已更改，且您请求了严格连接。

主机验证失败。
