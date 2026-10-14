
## SSH 特性与架构

要理解 SSH 作为一种安全的远程传输协议可以提供什么，你需要了解：

- SSH 特性
- SSH 协议版本
- SSH 认证机制配置

### SSH 特性

在大多数情况下，安全 shell（secure shell）不仅提供了 Telnet、login、rsh 和 ftp 的所有功能，甚至包含了 FTP 的某些功能。

SSH 支持通过加密安全的通道路由保护 X11 和任何 TCP 连接。

以下列出了 SSH 提供的基本功能：

- 从远程主机登录
- 在远程主机上执行交互或非交互式命令
- 在不同的网络主机之间复制文件
- 在非安全网络上进行高性能认证和加密安全通信
- 对所有通信进行自动且透明的加密
- 完全替代“r”类工具：login、rsh 和 rcp
- 端口转发
- 隧道技术

除了基本的 SSH 功能外，以下是安全 shell 的特殊功能：

通过基于 RSA 的服务器认证，可以防止通过 IP、路由和 DNS 欺骗的安全漏洞。

你可以使用系统级和用户级的配置文件来控制客户端。通过这些设置，可以为普通用户简化工作。

- 客户端最多有六种程序用于服务器认证。

在 SUSE Linux Enterprise Server 中使用了 SSH 的开源实现 (`OpenSSH`)。在安装 SUSE Linux Enterprise Server 时，默认已经激活了 `OpenSSH` 服务器。

### 使用 OpenSSH 提供安全的远程访问

有关 `OpenSSH` 功能的更多详细信息，请访问 www.openssh.com。

### SSH 协议版本

以下是目前适用于 SSH 协议的版本：

- 协议版本 1 (`SSH1`)
- 协议版本 2 (`SSH2`)

在本节中，使用 `SSH1` 和 `SSH2` 是为了方便引用协议版本。它们并不是协议版本的正式名称。

#### 协议版本 1 (`SSH1`)

图 10-1 展示了 `SSH1` 在安全连接上进行传输的过程。

![](img/667acce1695f6403deb2b60e994760c8_628_0.png)

图 10-1

##### 610 第 10 节 管理远程访问

以下描述了该过程中的步骤：

- 1. 客户端与服务器建立连接（端口 22）。

在此阶段，SSH 客户端和服务器对协议版本和其他通信参数达成一致。

- 2. SSH 服务器配合两个 RSA 密钥对，并将公钥发送给客户端：

  - **持久性主机密钥对 (`HK`)**。该密钥对由一个标识计算机的主机公钥 (`/etc/ssh/ssh_host_key.pub`) 和主机私钥 (`/etc/ssh/ssh_host_key`)组成。这个持久密钥对对于主机上运行的所有 SSH 进程都是相同的。
  - **进程服务器密钥对 (`SK`)**。该密钥对在每个服务器进程启动时创建，包括一个公服务器密钥和一个私服务器密钥，密钥会在特定间隔（通常为每小时一次）更改。此对从不存储在文件中。这些动态密钥有助于防止攻击者解密录制的会话，即使攻击者能够入侵服务器并盗取持久性密钥对。

- 3. 客户端检查主机公钥是否正确。为此，它将主机密钥与 `/etc/ssh/ssh_known_hosts` 或 `~/.ssh/known_hosts` 文件中的密钥进行比对。

- 4. 客户端生成一个 256 位的随机数，使用 SSH 服务器的公钥对其加密并发送到服务器。

- 5. 服务器现在可以解密该随机数，因为它拥有私钥。

- 6. 该随机数是随后的对称加密的密钥。

该随机数也称为会话密钥。

客户端现在可以向服务器进行身份验证。

**协议版本 2 (`SSH2`)**

SSH 协议版本 1 缺乏确保连接完整性的机制。这允许攻击者向现有连接中插入数据包（插入攻击）。

`SSH2` 提供了避免此类攻击的功能。这些功能被称为 `HMAC`（密钥哈希消息认证码），并在 RFC 2104 中进行了详细描述。

只有在 `SSH2` 不可用时才应该使用 `SSH1`。

图 10-2 展示了 `SSH2` 在安全连接上传输数据的过程。

![](img/667acce1695f6403deb2b60e994760c8_630_0.png)

图 10-2

以下描述了该过程中的步骤：

- 1. 如 `SSH1` 所述，服务器和客户端之间建立了连接。
- 2. 服务器现在包含一个密钥对（DSA 或 RSA），即主机公钥和私钥。对应的文件称为 `/etc/ssh/ssh_host_rsa_key` (`RSA`) 和 `/etc/ssh_host_dsa_key` (`DSA`)。
- 3. 与 `SSH1` 一样，主机密钥与 `/etc/ssh/ssh_known_hosts` 和 `~/.ssh/known_hosts` 文件中的密钥进行比对。
- 4. 随后进行 Diffie-Hellman 密钥协商，客户端和服务器通过此达成秘密会话密钥。
- 5. 与 `SSH1` 一样，通信最终通过对称加密。

`SSH1` 和 `SSH2` 之间的基本区别在于保证连接完整性的机制（`HMAC`）以及会话密钥协商机制（Diffie-Hellman）。

要查看 SSH 服务器支持哪个版本，可以使用 Telnet 登录端口 22。表 10-1 显示了服务器可能的响应。

### 表 10-1

| 协议 | 服务器响应 |
|---|---|
| 仅限 SSH1 | SSH-1.5-OpenSSH... |
| SSH1 和 SSH2 | SSH-1.99-OpenSSH... |
| 仅限 SSH2 | SSH-2.0-OpenSSH... |

以下是端口 22 上 Telnet 连接的示例：

```
DA50:~ # telnet DA10 22
Trying 192.168.0.10...
Connected to DA10.
Escape character is '^'
SSH-1.99-OpenSSH_3.8p1
```

在服务器配置文件 `/etc/ssh/sshd_config` 中，`Protocol` 参数定义了支持的协议版本。

例如，配置文件中的 `Protocol 2,1` 意味着支持 `SSH2` 和 `SSH1`，但优先使用 `SSH2`。如果 `SSH2` 不可用，则使用 `SSH1`。

你可以在启动客户端时指定使用的版本（例如使用 `ssh -1` 用于 `SSH1`）。

### SSH 身份验证机制配置

SSH 服务器可以发现生成的会话密钥。

#### SSH 客户端命令

表 10-2 列出了常用的 SSH 客户端命令。

### 表 10-2

| 命令 | 描述 |
| --- | --- |
| `scp` | 该命令使用 `ssh` 在两台计算机之间安全地复制文件，并取代 `rcp` 和 `FTP`（用于纯文件传输）。 |
| `ssh` | 这是 `ssh` 客户端。`SSH` 可以作为 `login`、`rsh` 和 Telnet 的替代方案。每个用户都应该始终使用 `ssh` 而不是 Telnet。 |
| `ssh-add` | 该命令向 `ssh-agent` 注册新密钥。 |
| `ssh-agent` | 该命令可以处理私 RSA 密钥，响应服务器的挑战（挑战/响应）。这简化了身份验证。 |
| `ssh-keygen` | 该命令生成 RSA 密钥。 |

以下是使用 SSH 客户端命令的一些示例：

- `geeko@mars: ~ ssh earth.example.com`

在此示例中，用户 `geeko` 登录到计算机 `earth.example.com` 上。

- `geeko@mars: ~ ssh -l tux earth.example.com`
- `geeko@mars: ~ ssh tux@earth.example.com`

在这些示例中，计算机 `mars` 用户 `geeko` 以用户 `tux` 的身份登录到计算机 `earth.example.com`。

- `geeko@mars: ~ ssh root@earth.example.com shutdown -h now`

在此示例中，用户 `geeko` 关闭了计算机 `earth.example.com`。

- `geeko@mars: ~ scp earth.example.com:/etc/HOSTNAME ~`

在此示例中，用户 `geeko` 将文件 `/etc/HOSTNAME` 从计算机 `earth.example.com` 复制到本地目录。

- `geeko@mars: ~ scp /etc/motd earth.example.com:`

在此示例中，用户 `geeko` 将本地文件 `/etc/motd` 复制到他在计算机 `earth.example.com` 上的家目录。

- `geeko@mars: ~ ssh -X earth.example.com`

在此示例中，用户 `geeko` 通过 SSH 从 `mars` 登录主机。连接通过图形化的 X11 隧道建立，允许在 `earth` 上启动的 X11 应用程序在 `mars` 上显示。

- `geeko@mars:~ > ssh -L 4242:earth.example.com:110 geeko@example.com`
