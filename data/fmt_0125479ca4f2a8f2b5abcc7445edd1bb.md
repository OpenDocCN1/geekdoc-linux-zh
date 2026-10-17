
大多数网络服务器与你系统上的其他守护进程（daemons）类似，但它们与网络端口交互。这与第 7 节介绍的 `syslog` 等守护进程不同，除非它们在带有 `-r` 选项启动时接收 UDP 数据包。以下是你的系统中可能运行的一些常见网络服务器：

```
httpd, apache, apache2, nginx  Web 服务器
sshd                          安全外壳守护
postfix, qmail, sendmail      邮件服务器
nfs, mount-network           网络文件系统
smbd, nmbd                   Windows 文件共享守护进程（见第 12 章）
rpcbind                       RPC 端口映射服务
```

大多数网络服务器的一个共同特征是它们通常作为多个进程运行。至少有一个进程监听网络端口，并在接收到接入连接时，监听进程使用 `fork()` 创建子进程，然后由后者负责网络。子进程在连接关闭时终止。与此同时，原始监听进程继续监听网络端口。这种进程允许服务器轻松处理许多连接。

这种模型也有例外。调用 `fork()` 会增加大量的系统开销。为了避免这种情况，高性能 TCP 服务器（如 Apache Web 服务器）可能会在启动时创建若干工作进程以便处理所需的连接。接受 UDP 数据包的服务器根本不需要 `fork()`，它们没有需要监听的连接；它们只需接收数据并做出反应。

### 10.3.1 安全外壳

每个网络服务器的工作方式都有些不同。为了获得服务器配置和操作的实践经验，让我们来看看独立的安全外壳（SSH）服务器。作为常用的网络服务应用之一，SSH 是远程访问 Unix 机器的事实标准。SSH 用于安全的 shell 登录、远程程序执行、简单的文件共享，并使用公钥加密进行身份验证、使用简单的加密算法处理会话数据，以取代旧的、不安全的 `telnet` 和远程访问系统。大多数 ISP 和云提供商都要求通过 SSH 访问其服务，许多基于 Linux 的网络设备（如网络附属存储或 NAS 设备）也通过 SSH 提供访问。`OpenSSH` 是 Unix 上流行的免费 SSH 实现，几乎所有 Linux 发行版都预装了它。`OpenSSH` 客户端程序是 `ssh`，服务器是 `sshd`。SSH 有两个主协议：1 和 2。`OpenSSH` 只支持版本 2，由于漏洞和缺乏使用已废弃了版本 1。

# Linux 的工作原理（早期访问） © 2021 Brian Ward

注意：隧道技术（Tunneling）是将一个网络连接封装并传输在另一个连接中的过程。*使用 SSH 隧道 X Window 连接的优点是 SSH 会为你设置显示环境，并加密隧道内部的 X 数据。*

SSH 有一些缺点。首先，为了建立 SSH 连接，你需要远程主机的公钥，而且你无法以一种安全的方式获取它（尽管你可以手动验证它以确保自己没有被欺骗）。要了解多种密码学方法的概述，请阅读 Jean-Philippe Auasson 编写的《严肃加密：现代加密实战介绍》（Serious Cryptography: A Practical Introduction to Modern Encryption，No Starch Press, 2017）。关于 SSH 的两本深度书籍是 Michael W. Lucas 写的《SSH 精通：OpenSSH, PuTTY, 隧道与密钥》（第2版，Tilted Windmill Press, 2018）以及 Daniel J. Barrett、Richard E. Silverman 和 Robert G. Byrne 编写的《SSH，安全外壳终极指南》（SSH, The Secure Shell: The Definitive Guide，第2版，O'Reilly, 2005）。

# 公钥加密

我们一直在没有语境的情况下使用“公钥”这个词，所以让我们退一步，简要讨论一下，以防你不熟悉。直到20 世纪 70 年代，加密算法是对称的，要求发送者和接收者拥有相同的密钥。破解代码是窃取密钥的问题，拥有的人越多，泄露的机会就越大。但使用公钥加密，有两个密钥：公钥和私钥。公钥可以加密消息但不能解密它；因此，谁访问此密钥并不重要。只有私钥可以解密来自公钥的密。在大多数情况下，保护私钥更容易，因为只需要一份副本，而且不需要传输。

除了加密之外的另一个应用是身份验证；有方法可以在不传输任何内容的情况下验证某人持有特定公钥的私钥。

# 10.3.2 sshd 服务

运行 `sshd` 服务以允许远程连接到你的系统需要一个配置文件和主机密钥。大多数发行版将配置保存在 `/etc/ssh` 配置目录中，如果你安装了它们的 `sshd` 软件包，它们会尝试为你配置好一切。（服务器配置文件名 `sshd_config` 很容易与客户端的 `ssh_config` 设置文件混淆，请小心。）

你不应该更改 `sshd_config` 中的任何内容，但检查一下总无坏处。该文件由键值对组成，如下片段所示。

```
# Port 22
#AddressFamily any

#ListenAddress 0.0.0.0
#ListenAddress : :
#HostKey /etc/ssh/ssh_host_rsa_key
#HostKey /etc/ssh/ssh_host_ecdsa_key
#HostKey /etc/ssh/ssh_host_ed25519_key
```

以 `#` 注释开头的行以及你 `ssh_config` 中的许多注释表示各种参数的默认值，正如你从这段摘录所示。`ssh_config(5)` 手册页包含参数描述和可能值的说明，但这些是最重要的：

- `HostKey file` 作为主机密钥使用。（主机密钥将在下文中描述。）
- `PermitRootLogin value` 如果该值设置为 `yes`，则允许超级用户通过 SSH 登录。将值设置为 `no` 以防止此操作。
- `Loglevel level` 使用 `syslog` 级别记录消息（默认为 `INFO`）。
- `SyslogFacility name` 使用 `syslog` 设施名称记录消息（默认为 `AUTH`）。
- `XForwarding value` 启用你系统上 `xauth` 工具的 X 系统客户端隧道。
- `Authentication path` 指定 `xauth` 系统的位置。没有此路径，隧道将无法工作。如果 `xauth` 不在 `/usr/bin` 中，请将路径设置为 `bauth` 的完整路径。

# 创建主机密钥

`OpenSSH` 拥有几组密钥。每组都包含一个公钥（扩展名为 `.pub`）和一个私钥（无扩展名）。

> 不要让任何人看到私钥，即使在你自己的系统上也是如此，因为如果有人获得了它，你就会面临入侵者的风险。

SSH 版本 2 拥有 RSA 和 DSA 密钥。RSA 和 DSA 是公钥算法。密钥文件名见表 10-1。

# 表 10-1：OpenSSH 密钥文件

| 文件名 | 密钥类型 |
| :--- | :--- |
| `ssh_host_rsa_key` | RSA 私钥 |
| `ssh_host_rsa_key.pub` | RSA 公钥 |
| `ssh_host_dsa_key` | DSA 私钥 |
| `ssh_host_dsa_key.pub` | DSA 公钥 |

创建密钥涉及一种同时生成公钥和私钥的数值计算。通常情况下，你不需要创建密钥，因为 `OpenSSH` 安装程序或你发行版的安装脚本会为你完成；但如果你计划使用像 `ssh-agent` 这样提供无密码身份服务的程序，你就需要知道如何这样做。创建 SSH 协议版本 2 密钥，使用 `ssh-keygen` 程序创建：

```
# ssh-keygen -t rsa -N "" -f /etc/ssh/ssh_host_rsa_key
# ssh-keygen -t dsa -N "" -f /etc/ssh/ssh_host_dsa_key
```

服务器和客户端也使用名为 `ssh_known_hosts` 的文件来存储其他主机的公钥。如果你打算使用基于远程客户端的身份验证，可以在不传输任何内容的情况下进行。当你需要导入其他主机的公钥时，在连接 SSH 服务器时可能会有用。从零开始安装新机器时，主机密钥文件非常有用。

# 启动 SSH 服务器

大多数发行版默认安装了 `sshd`，但处于关闭状态。要启用 `sshd`：

```
# systemctl enable sshd
```

如果你想立即启动：

```
# systemctl start sshd
```

在 Fedora 中，`sshd` 有两种启动模式：独立（standalone）和按需（demand）。独立模式更为常见，`sshd` 进程将其 PID 写入 `/var/run/sshd.pid`。作为替代方案，`systemd` 可以通过 socket 启动 `sshd`。正如你在第 6 章所看到的，在某些情况下可能需要重启。由于 SSH 密钥在首次连接请求时会生成，这通常是不错的。

# 10.3.3 fail2ban
