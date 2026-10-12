
`rsync` 比 `scp` 更强大得多。`rsync` 比 `scp` 更易配置且默认使用 `ssh`。它有许多选项；最常用的是 `-a` 和 `-v`。`-a` 选项让 `rsync` 复制目录文件，保留所有权、组和修改时间。通常不需要指定 `-a` 选项，这很有帮助。`-v` 选项在复制文件时列出文件。例如，Sam 可能会给出以下命令：

（注：原文中存在大量重复的 `rsync` 描述段，译文已根据“不要重复输出原文”的原则进行了整合处理）

# 运行 ssh, scp 和 sftp OpenSSH 客户端 687

## HashKnownHosts

当设置为 `yes` 时，OpenSSH 会对 `~/.ssh/known_hosts` 中的主机名和地址进行哈希处理。当设置为 `no` 时，主机名和地址将以明文形式写入。默认值为 `no`。关于 `known_hosts` 文件的更多信息，请参阅第 679 页。

`Host` `hostnames` 指定以下声明，在下一个 `Host` 声明之前，这些声明仅适用于匹配 `hostnames` 的主机。`hostnames` 是一个由空格分隔的列表，可以包含 `?` 和通配符。单个星号 `*` 表示所有主机。如果没有此关键字，则所有声明都适用于所有主机。

## HostBasedAuthentication

当设置为 `yes` 时，尝试 `ssh` 身份验证。为了系统的安全，请将其设置为 `no`。默认值为 `no`。

## HostKeyAlgorithms

这些算法是客户端按偏好顺序使用的算法列表，并用逗号分隔。请从 `ssa-rsa` 或 `ssh-dss` 中选择算法。默认值为 `ssa-rsa,ssh-dss`。

## Port

当设置为 `no` 时，OpenSSH 将连接到远程系统。默认值为 `22`。

## StrictHostKeyChecking

决定 OpenSSH 是否以及如何将密钥添加到用户的 `known_hosts` 文件中。将此选项设置为 `ask`，则在连接到新系统时询问是否添加主机密钥；设置为 `no` 则自动添加主机密钥；设置为 `yes` 则要求手动添加密钥。`yes` 和 `ask` 参数将导致 OpenSSH 拒绝连接到主机密钥已更改的系统。为了增强系统安全性，请将其设置为 `yes` 或 `ask`。默认值为 `ask`。

## TCPKeepAlive

当设置为 `yes` 时，定期检查连接是否存活。检查会导致当服务器崩溃或由于其他原因失效（即使是暂时的），`ssh` 或 `scp` 也会被断开。此选项在传输层（TCP）测试连接（第 371 页）。将此参数设置为 `no` 会导致客户端不检查连接是否存活。默认值为 `yes`。

此声明使用了 TCP keepalive 选项，该选项未加密且容易受到 IP 伪装攻击（第 1171 页）。请参阅第 693 页的 `ClientAliveInterval` 以获取基于服务器的不可伪造替代方案。

## User

指定登录系统时使用的用户名。您可以在 `Host` 声明中指定用户名。此选项意味着当您使用的用户名与本地系统上的用户名不同时，无需在命令行中输入用户名。

## VisualHostKey

当设置为 `yes` 时，除了显示密钥的十六进制表示外，还会显示远程系统密钥的 ASCII 表示。当设置为 `no` 时，此声明仅显示十六进制密钥。更多信息请参阅第 691 页的“Randomart”。默认值为 `no`。

## 设置 OPENSSH 服务器 (sshd)

本节描述了如何设置 OpenSSH 服务器。

### 前提条件

安装以下软件包（两者默认均已安装）：

- `openssh`
- `openssh-server`

在 Fedora（而非 RHEL）下，您必须运行 `chkconfig` 以确保系统在进入多用户模式时启动 `sshd`：

```bash
# chkconfig sshd on
```

在 Fedora（而非 RHEL）中，在配置好 `sshd` 服务器后（您可能不需要执行任何操作），调用 `sshd` init 脚本来启动 `sshd` 守护进程：

```bash
# service sshd start
```

更改 `sshd` 配置文件后，使用 `reload` 代替 `start` 来重新加载 `sshd` 配置文件。

在 Fedora 下，当您首次启动守护进程时，它会在 `/etc/ssh` 中创建主机密钥文件（第 675 页）（RHEL `sshd` 在安装 RHEL 后的系统启动时创建这些文件）。OpenSSH 使用它创建的文件来识别服务器。

### Notes

OpenSSH 服务器通常使用 TCP 端口 `22`。在 RHEL 下，当系统启动时该端口是开启的。如果 OpenSSH 服务器正在运行且防火墙是开启的，使用图形化工具（第 893 页）打开此端口。使用图形化工具选择 SSH 以打开此端口。`yes` 和 `ask` 参数会导致 OpenSSH 拒绝连接到主机密钥已更改的系统。为了安全，请设置为 `yes` 或 `ask`。

SELinux: 当 SELinux 设置为 `targeted` 策略时，`ssh` 受到保护。如需更多信息，请参阅第 463 页的“Setting the Targeted Policy”。

## JUMPSTART：启动 OpenSSH 服务器

安装必要的软件包并启动 OpenSSH (`sshd`) 守护进程（默认已安装）（第 688 页）。

## 推荐设置

Fedora 提供的配置文件可能满足您的需求。RHEL `/etc/ssh/ssh_config` 开启了端口转发（第 696 页）。将 `PermitLogin` 设置为 `no`（第 694），防止特权账户暴露。

## AUTHORIZED KEYS：自动登录

为了在不提供密码的情况下登录另一个服务器或复制文件，必须从客户端（本地）将 `~/.ssh/id_rsa.pub` 文件复制到服务器（远程系统）名为 `~/.ssh/authorized_keys` 的文件中。`ssh-copy-id` 工具在必要时会在服务器上创建 `~/.ssh` 目录，复制 `id_rsa.pub` 并确保权限正确。以下示例显示了 Sam 在名为 `plum` 的系统上设置自动登录：

```bash
$ ssh-copy-id sam@plum
plum's password:
```

现在尝试通过 "`ssh sam@plum`" 登录，并检查 `~/.ssh/authorized_keys` 以确保我们没有添加意外的密钥。

Sam 必须提供密码来复制文件。执行 `ssh-copy-id` 后，Sam 无密码即可登录 `plum`。为了提高服务器安全性，请禁用身份验证（见相邻提示）。如果除所有者以外的人有权读取或写入服务器上的 `~/.ssh` 目录，则自动登录将失败。

设置自动登录的第一步是生成身份验证密钥。首先检查 `~/.ssh` 查看这些密钥是否已存在于本地系统（client）：`idrsa`。如果存在这些文件中的之一，请跳过下一步。

```bash
$ ssh-keygen
Generating public/private key.
Enter file in which to save the key (/home/sam/.id_rsa):
Enter passphrase (empty for no):
Enter passphrase again:
Identity saved in /home/sam/.id_rsa
Public key saved in /home/sam/.id_rsa.pub
```

SSH：安全通信

将 `rsa` 替换为 `dsa` 以生成 DSA 密钥。在本示例中，用户在查询时按回车。您可以指定密码（10–30 个字符是理想长度）来加密私部分。没有恢复密码的方法。有关密码的更多信息，请参阅第 691 页的安全提示。

`ssh-keygen` 工具生成两个密钥：位于 `~/.ssh/id_rsa` 的私密钥和位于 `~/.ssh/id_rsa.pub` 的公密钥。除所有者外没人能写入或编辑这些文件，只有所有者才能读取私密钥文件。

您可以使用 `ssh-keygen` 显示本地服务器的 RSA 指纹：

```bash
$ ssh-keygen -f /etc/ssh/ssh_host_key
2048 SHA256:d19d1fb5b57c80e9a494b7c388ea1ae5...
...
/etc/ssh/ssh_host_key.pub (RSA)
```

或者您可以显示您创建的公密钥指纹：

```bash
$ ssh-keygen -f ~/.ssh/id_rsa.pub
2048 SHA256:83f99e2433693e638fe404612728...
/home/sam/.id_rsa.pub (RSA)
```
