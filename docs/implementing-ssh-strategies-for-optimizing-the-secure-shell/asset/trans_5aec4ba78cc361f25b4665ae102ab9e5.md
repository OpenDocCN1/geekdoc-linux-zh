
## 表 3.1 配置文件位置

| 客户端 | Windows 操作系统 | UNIX 操作系统 |
| :--- | :--- | :--- |
| OpenSSH | \Program Files\OpenSSH\etc | /etc/ssh_config |
| SSH Communications | \Program Files\SSH Secure Shell\ssh2_config | /etc/ssh2/ssh2_config |

### 常规设置

配置文件的常规部分列出了一般标志和开关，这些选项可以限制终端用户尝试访问 SSH 服务器时需要输入的命令数量。诸如 `VerboseMode`、`QuietMode`、`Compression`、`GoBackground` 和 `EscapeChar` 等字段允许直接从配置文件启用定制的一般设置，而无需在命令行中输入。表 3.2 提供了常规部分中部分选中字段的说明，以及每个字段的简要描述。

### 网络

配置文件中的网络部分列出了建立连接所需的网络设置。网络设置的一个示例是 SSH 客户端在尝试连接到 SSH 服务器时应使用的特定端口。表 3.3 简要描述了网络部分中部分选中字段的信息。

## 表 3.2 常规部分中的字段

| 字段 | 描述 |
| :--- | :--- |
| VerboseMode | 显示 SSH 会话的详细信息 |
| QuietMode | 显示警告消息 |
| DontReadStdin | 禁用标准输入 |
| BatchMode | 启用/禁用批处理模式 |
| Compression | 启用/禁用压缩 |
| GoBackground | 将连接发送到后台 |
| EscapeChar | 为会话设置 ESC 字符 |
| PasswordPrompt | 密码提示类型 |
| AuthenticationSuccessMsg | 登录成功后显示成功消息 |
| SetRemoteEnv | 为会话设置环境变量 |

## 表 3.3 网络部分中的字段

| 字段 | 描述 |
| :--- | :--- |
| Port | 设置要连接的端口 |
| NoDelay | 启用/禁用延迟处理 |
| KeepAlive | 保持连接活跃 |
| SocksServer | SOCKS 服务器的网络 ID |
| UseSocks5 | 支持 SOCKS 版本 5 |

### 加密

配置文件中的加密部分列出了可以为 SSH 客户端设置的密码学类型。当不同的 SSH 服务器需要不同类型的加密算法时，这部分很有用。例如，可以为备份设置不同的 SSH 配置文件，启用对带宽影响最小且启用 MAC 进行数据验证的特定类型加密。表 3.4 简要描述了加密部分中部分选中字段的信息。

## 表 3.4 加密部分中的字段

| 字段 | 描述 |
| :--- | :--- |
| Ciphers | 指定可以使用哪些密码算法 |
| MACs | 指定可以使用哪些 MAC 算法 |
| StrictHostKeyChecking | 启用主机密钥检查以验证服务器 |
| RekeyIntervalSeconds | 会话重新密钥间隔长度 |

### 用户公钥认证

配置文件中的公钥认证部分仅指定用于认证的**用户公钥**的位置和名称。表 3.5 描述了公钥认证部分的字段。

## 表 3.5 公钥认证部分中的字段

| 字段 | 描述 |
| :--- | :--- |
| IdentityFile | 身份识别文件名称 |
| RandomSeedFile | 随机种子文件名称 |

### 隧道

配置文件中的隧道部分指定了在 SSH 客户端上应使用的本地和远程隧道选项。当客户端启用了多个本地和远程端口转发时，这部分会增加很大的价值。表 3.6 描述了隧道部分中选中的字段。

## 表 3.6 隧道部分中的字段

| 字段：隧道 | 描述 |
| :--- | :--- |
| GatewayPorts | 允许接口充当网关 |
| ForwardAgent | 启用/禁用数据包转发 |
| ForwardX11 | 启用/禁用 X11 仿真 |
| TrustX11Applications | 信任/不信任 X11 的选项 |
| 登录时建立的隧道 | |
| LocalForward | 本地端口转发设置 (143:IP:143) |
| LocalForward | 本地端口转发设置 (25:IP:25) |
| RemoteForward | 远程端口转发设置 (22:IP:23) |

### SSH1 兼容性

配置文件中的 SSH1 兼容性部分指定了要与 SSH1 版本兼容所使用的选项。为了使 SSH2 客户端与 SSH1 服务器兼容，必须设置以下字段（见表 3.7）。

## 表 3.7 SSH 兼容性

| 字段 | 描述 |
| :--- | :--- |
| Ssh1Compatibility | 启用/禁用 SSH1 支持 |
| Ssh1Path | 用于 SSH1 的路径。默认为 /usr/local/bin/ssh1 |
| Ssh1MaskPasswordLength | 启用/禁用密码长度掩码 |

### 认证

配置文件中的认证部分指定了支持的认证选项。此部分允许客户端了解使用哪种类型的认证，例如，是否使用密码和公钥组合而不仅仅是密码进行认证。表 3.8 是认证部分中选中字段的简要列表。

## 表 3.8 认证

| 字段 | 描述 |
| :--- | :--- |
| AllowedAuthentication | 指定允许的认证类型，例如 *password*（密码）、*public key*（公钥）或 *all of the above*（以上所有） |

## GUI SSH 客户端

Secure Shell Communications (www.ssh.com)、VanDyke Software、PuTTY、AppGate 和 WinSCP 是提供 SSH 客户端图形用户界面（GUI）的几个供应商之一。由于市场上有几种 GUI 客户端，以下部分将研究 GUI SSH 客户端的一些最佳特性。此外，由于 GUI 客户端主要适用于 Windows，以下部分将重点介绍 Windows 2000 和 Windows XP。表 3.9 显示了可以在哪里购买和/或下载 SSH 客户端。

## 表 3.9 提供 SSH 客户端的网站

| 客户端 | URL |
| :--- | :--- |
| SSH Communications | www.ssh.com |
| VanDyke Software | www.vandyke.com/ |
| Putty | www.chiark.greenend.org.uk/ ~sgtatham/putty/ |
| WinSCP | winscp.net/eng/ |
| Mindterm | www.appgate.com/mindterm/ |
| MacSSH | pro.wanadoo.fr/chombier/ |

### Windows 安装

安装基于 Windows 的 SSH 客户端相对简单。我不描述表 3.9 中列出的每个 SSH 客户端的安装过程，但每个客户端的向导都会引导您完成安装过程。

### SSH Communications

我将首先讨论 SSH Communications 的 SSH 客户端。打开 SSH 客户端并通过执行以下步骤发起简单的 SSH 连接：

- 1. 启动程序 SSH Secure Shell Secure Shell Client
- 2. 文件 打开 快速连接

如图 3.1 所示，**主机名**字段是 SSH 服务器的完全限定 DNS 名称（例如 `sshserver.aum.com`），或者是 SSH 服务器 IP 地址的点分表示法（例如 `172.16.11.17`）。**用户名**字段是远程 SSH 服务器上的用户名。根据 SSH 服务器的实现方式，用户名可以是 Windows 机器上的本地帐户，也可以是 Windows 域上的域帐户。在 Unix 环境中，用户名与 `/etc/passwd` 文件中的用户名相同。**端口号**字段用于指定端口号。如果 SSH 服务器正在监听非标准端口（即 22 端口以外的端口），则应在端口框中输入适当的端口号，例如 202。最后，**认证方法**指定在尝试连接到远程 SSH 服务器时应使用的认证类型。可能的值及其描述见表 3.10。

![](img/c99d6f526a5f9fa62f2c34daada85ad7_127_0.png)

**图 3.1** “快速连接”菜单。

## 表 3.10 认证类型

| 认证类型 | 描述 |
| :---------------- | :---------------- |
| Password | 用户名和密码组合 |
| Public Key | 公钥和私钥认证 |
| SecureID | 用于认证的 RSA SecureID 令牌* |
| PAM | 可插拔认证模块** |

* 需要 RSA ACE 服务器。
** 可插拔认证模块是一种 Unix 认证方法，它将各种认证方法集成在一起。

SSH Communications 为 SSH 客户端提供不同的设置。使用菜单栏，通过选择“编辑设置”打开设置菜单。在设置菜单下，应该有两个部分：配置文件设置（Profile Settings）和全局设置（Global Settings）。在配置文件设置和全局设置下，应该还有更多选项。在以下各部分中，将单独检查每个选项并描述其目的和用法。

### 配置文件设置

配置文件设置类似于前面使用命令行工具讨论的 `ssh2_config` 文件。配置文件设置部分下的所有选项直接对应于尝试连接 SSH 服务器时默认使用的设置。表 3.11 提供了这些设置的描述和用法。

## 表 3.11 配置文件设置部分下的选项

| 设置 | 描述和用法 |
| :---------------- | :---------------- |
| 连接 | 以下描述了左侧各部分的选项。这些部分中的选项也已解释。 <br>- 主机名：远程 SSH 服务器的 DNS 名称或 IP 地址。 <br>- 用户名：用于登录的帐户用户名。 <br>- 端口号：SSH 服务器正在监听的端口号。 <br>- 认证方法：可用于登录 SSH 服务器的认证类型。选项可以是密码、公钥、SecureID 和 PAM。 <br>- 加密算法：设置会话使用的密码学类型。 <br>- MAC 算法：设置对网络上传输的数据进行哈希处理时使用的哈希类型。选项可以是 MD5 或 SHA1。（所选选项必须受到 SSH 服务器支持。） <br>- 压缩：在连接上启用压缩。压缩的有效选择仅为 zlib。 |

