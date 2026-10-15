
`./configure --with-x \

--without-rsh \

--with-rsaref`

如果你需要使用 RSAref，你需要遵循本段中的说明。虽然配置帮助建议你可以告诉 SSH 在哪里找到 RSAref 库，但 `# 第三部分：防火墙和特殊用途软件` 那部分脚本是损坏的。从你运行 `./config --help` 的目录创建“`rsfare2`”目录（`mkdir rsfare2`）。不要更改此名称；它必须完全一致。然后 `cd` 进入 `rsfare2` 并执行 `tar xzv /path/to/rsfare2.tar.Z`。现在只需回到配置目录并运行你的配置脚本，然后继续。

执行配置文件后，注意并纠正任何缺陷（库缺失或路径错误是正常的）。一旦你的配置脚本运行完成，就可以执行 `make` 命令。该命令将需要一段时间才能完成，完成后，切换（`su`）到 root 用户并执行 `make install`。这将安装所有运行所需的准备工作，包括创建的系统私钥。

一旦安装了所有内容，你需要确保 `ssh` 二进制文件在系统启动期间运行。做到此最简单的方法是使用以下行：

```bash
echo /usr/local/sbin/sshd > /etc/rc.d/rc.local
```

默认情况下，这将使用 768 位的默认 RSA 密钥启动 Secure Shell 服务器守护。如果你想使用更大的密钥（这将需要更多的计算时间并可能减慢连接，但提供了更高的安全性），添加 `-b 1024`，并将 1024 替换为任何所需的位数。不要降低 768 位的默认值，因为今天的技术可以轻松解密 512 位及以下的密钥，甚至 768 位也不可靠。不建议从 `inetd` 并在每次 `sshd` 启动时生成所需的密钥。要在不重启的情况下启动 `sshd`，请从命令行使用 `sshd` 命令。

> 注意：不需要，但确保 `/etc/services` 将端口 22 列为 `sshd:` 是一个好主意：

```
ssh 22/tcp
ssh 22/udp
```

在安装期间，`sshd` 会在 `/etc` 中创建几个文件：

- `ssh_config`: 默认 SSH 服务器守护配置
- `ssh_config`: 默认守护进程配置文件
- `ssh_host_key`: 主机的私钥，应仅允许 root 读写，不允许其他访问
- `ssh_host_key.pub`: 主机的公钥
- `ssh_random_seed`: 在每次 `sshd` 启动期间创建（仅允许 root 读写，不允许其他访问）
- `ssh_config`: 默认 SSH 服务器守护配置

## 第 21 章：使用 Secure Shell 和 VPN

`ssh_host_key` 将由安装程序创建为 768 位的密钥。如果你想增加此密钥的大小，例如增加到 1024 位，你需要使用命令 `ssh-keygen -b 1024`。当生成密钥时，将其保存为 `/etc/ssh_host_key`。这将创建新的 `ssh_host_key` 和 `ssh_host_key.pub` 文件。当询问密码时，不要输入。如果你输入了密码，`ssh` 程序将等待启动直到你输入密码为止。

一旦安装了所有内容，你需要确保 `ssh` 二进制文件在系统启动期间运行。做到此最简单的方法是使用以下行：

```bash
echo /usr/local/sbin/sshd > /etc/rc.d/rc.local
```

默认情况下，这将使用 768 位的默认 RSA 密钥启动 Secure Shell 服务器守护。如果你想使用更大的密钥（这将需要更多的计算时间并可能减慢连接，但提供了更高的安全性），添加 `-b 1024`，并将 1024 替换为任何所需的位数。不要降低 768 位的默认值，因为今天的技术可以轻松解密 512 位及以下的密钥，甚至 768 位也不可靠。不建议从 `inetd` 并在每次 `sshd` 启动时生成所需的密钥。要在不重启的情况下启动 `sshd`，请从命令行使用 `sshd` 命令。

> 注意：不需要，但确保 `/etc/services` 将端口 22 列为 `sshd` 是一个好主意：

```
ssh 22/tcp
ssh 22/udp
```

在安装期间，`sshd` 会在 `/etc` 中创建几个文件：

- `ssh_config`: 默认 SSH 服务器守护配置
- `ssh_config`: 默认守护进程配置文件
- `ssh_host_key`: 主机的私钥，应仅允许 root 读写，不允许其他访问
- `ssh_host_key.pub`: 主机的公钥
- `ssh_random_seed`: 在每次 `sshd` 启动期间创建（仅允许 root 读写，不允许其他访问）
- `ssh_config`: 默认 SSH 服务器守护配置

## 第 21 章：使用 Secure Shell 和 VPN

`ssh_host_key` 将由安装程序创建为 768 位的密钥。如果你想增加此密钥的大小，例如增加到 1024 位，你需要使用命令 `ssh-keygen -b 1024`。当生成密钥时，将其保存为 `/etc/ssh_host_key`。这将创建新的 `ssh_host_key` 和 `ssh_host_key.pub` 文件。当询问密码时，不要输入。如果你输入了密码，`ssh` 程序将等待启动直到你输入密码为止。

一旦安装了所有内容，你需要确保 `ssh` 二进制文件在系统启动期间运行。做到此最简单的方法是使用以下行：

```bash
echo /usr/local/sbin/sshd > /etc/rc.d/rc.local
```

默认情况下，这将使用 768 位的默认 RSA 密钥启动 Secure Shell 服务器守护。如果你想使用更大的密钥（这将需要更多的计算时间并可能减慢连接，但提供了更高的安全性），添加 `-b 1024`，并将 1024 替换为任何所需的位数。不要降低 768 位的默认值，因为今天的技术可以轻松解密 512 位及以下的密钥，甚至 768 位也不可靠。不建议从 `inetd` 并在每次 `sshd` 启动时生成所需的密钥。要在不重启的情况下启动 `sshd`，请从命令行使用 `sshd` 命令。

> 注意：不需要，但确保 `/etc/services` 将端口 22 列为 `sshd` 是一个好主意：

```
ssh 22/tcp
ssh 22/udp
```

在安装期间，`sshd` 会在 `/etc` 中创建几个文件：

- `ssh_config`: 默认 SSH 服务器守护配置
- `ssh_config`: 默认守护进程配置文件
- `ssh_host_key`: 主机的私钥，应仅允许 root 读写，不允许其他访问
- `ssh_host_key.pub`: 主机的公钥
- `ssh_random_seed`: 在每次 `sshd` 启动期间创建（仅允许 root 读写，不允许其他访问）
- `ssh_config`: 默认 SSH 服务器守护配置

# 第 21 章：使用 Secure Shell 和 VPN

```bash
# RhostsAuthentication yes
# RhostsRSAAuthentication yes
# RSAAuthentication yes
# TISAuthentication no
# PasswordAuthentication yes
# FallBackToRsh yes
# UseRsh no
# BatchMode no
# StrictHostChecking no
# IdentityFile ~/.ssh/identity
# Port 22
# Cipher idea
# EscapeChar ~
```

尽管所有的配置都被注释掉了，但如果在此处或其他地方未对其进行修改，SSH 仍然会使用这些配置。修改可以是针对主机的。如果需要针对主机的修改，应将它们添加到“所有其他”`Host` 部分之前的某个 `Host` 部分中。关于 `ForwardX11` 的一些说明：

有几个选项值得注意。`X11` 选项允许将 `X11` 显示透明且自动地回传到本地主机。实际上，这等于在本地主机上运行 `xhost +remote`，然后在远程主机上将 `DISPLAY` 环境变量设置为本地主机（`export DISPLAY=CLIENTHOST`）。此功能的使用取决于 SSH 能否在远程主机上找到 `xauth` 程序（这在某些非 Linux 系统上可能会成为问题）。如果请求并启用了 `X11` 转发，则 `X11` 连接将通过加密隧道接收消息。如果你执行 `ssh foo`，然后在 `foo` 上运行 `xtrm`，你将在本地系统上接收到一个 `xtrm`（假设你已登录 `X` 会话）。主机 `foo` 不需要正在运行即可使客户端程序可用。请注意，在慢速连接（模拟调制解调器）上，此选项可能并不理想。

另请注意，SSH 默认将使用 `IDEA` 作为加密算法。如果你想使用三重 DES（`triple DES`），请取消 `Cipher` 行并将 `idea` 更改为 `3des`，或者在启动 `ssh` 时使用 `-c 3des` 选项。

服务器守护进程的默认配置文件如列表 21–3 所示。

列表 21-3：默认的 `/etc/ssh/config` 文件

```bash
Port 22
ListenAddress 0.0.0.0
```
