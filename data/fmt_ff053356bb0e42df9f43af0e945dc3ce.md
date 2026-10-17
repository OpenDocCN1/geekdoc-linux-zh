
表 10.3 列出了这些选项以及其他选项，并解释了它们的作用。

# 传输中的数据保护
第 10 章

## 表 10.3 `/etc/sshd_config` 选项

| 选项 | 功能 |
| --- | --- |
| `AllowGroups [groups]` | 设置此选项以控制哪些组可以访问 `ssh` 服务。（示例：`AllowGroups sysadmin accounting.`）你可以显式指定组或使用通配符指定。使用空格分隔主机，而不是使用逗号。 |
| `AllowHosts [hosts]` | 设置此选项以控制哪些主机可以访问 `ssh` 服务。（示例：`AllowHosts shell.ourcompany.net.`）你可以显式指定主机或使用通配符、主机名或 IP 地址指定。使用空格分隔主机，而不是使用逗号。 |
| `AllowSHosts [hosts]` | 使用此选项指定 `.hosts` 或 `.rosts` 中的哪些主机可以访问 `ssh` 服务。你可以显式指定主机或使用通配符、主机名或 IP 地址指定。使用空格分隔主机，而不是使用逗号。 |
| `AllowTCPForwarding` | 使用此选项指定是否允许 TCP 转发。`AllowTCPForwarding` 默认设置为 `yes`。 |
| `CheckMail [yes\|no]` | 使用此选项指定 `ssh` 是否应该通知邮件。 |
| `DenyGroups [groups]` | 使用此选项以控制哪些组可以访问 `ssh` 服务。（示例：`AllowGroups sysadmin accounting.`）你可以显式指定组或使用通配符指定。使用空格分隔主机，而不是使用逗号。 |
| `DenyHosts [hosts]` | 设置此选项以控制哪些主机可以访问 `ssh` 服务。（示例：`AllowHosts shell.ourcompany.net.`）你可以显式指定主机或使用通配符、主机名或 IP 地址指定。使用空格分隔主机，而不是使用逗号。 |
| `FascistLogging [yes\|no]` | 使用此选项指定 `ssh` 是否应该记录日志。 |
| `HostKey [path]` | 指定用户使用 `ssh` 客户端登录时进入的路径。（默认情况下，用户进入其家目录。） |
| `LoginGraceTime [time]` | 使用此选项指定登录宽限时间。 |
| `IgnoreHosts [no]` | 设置此选项以控制哪些主机可以访问 `ssh` 服务。 |
| `KeepAlive [yes]` | 使用此选项指定 `ssh` 是否应该保持存活。 |
| `PermitEmptyPasswords [yes]` | 设置此选项以允许空密码。 |
| `PermitRootLogin [yes]` | 设置此选项以控制是否允许 `root` 登录。 |
| `PrintMotd [yes]` | 设置此选项以控制是否打印欢迎消息。 |
| `RhostsAuthentication [no]` | 设置此选项以控制是否使用 `rhosts` 认证。 |
| `RhostsRSAAuthentication [yes]` | 设置此选项以控制是否使用 `rhosts` RSA 认证。 |
| `RSAAuthentication [yes]` | 设置此选项以控制是否使用 RSA 认证。 |
| `StrictModes [yes]` | 设置此选项以启用严格模式。 |
| `SilentDeny [yes]` | 设置此选项以控制是否静默拒绝。 |
| `X11Forwarding [yes]` | 设置此选项以控制是否允许 X11 转发。 |
| `X11DisplayOffset [10]` | 设置此选项以控制 X11 显示偏移量。 |
| `UseLogin [no]` | 设置此选项以控制是否使用登录 Shell。 |

| 选项 | 功能 |
| --- | --- |
| `-h [host_key]` | 使用此选项指定备用主机密钥文件。（默认是 `/etc/ssh_host_key`）。在某些情况下你可能需要这样做。一种是你是以 `root` 以外的用户身份运行 `ssh`。（默认配置文件由 `root` 所有，且只有 `root` 才能读取或写入它。因此，如果你以另一个用户的身份启动 `ssh`，`ssh` 将无法读取该文件）。如果你通过在一天中不同时间执行不同选项的脚本启动 `ssh`，此选项也很有用。例如，也许你可能在白天允许外国网络或主机通过 `ssh` 访问，但想在晚上进行限制访问。为了实现这一点，你需要在脚本中编写两个不同的函数：一个在晚上将外国主机添加到 `DenyHosts` 列表中，另一个在黎明时将其从 `DenyHosts` 列表中剔除。自然而易见，每当发生这种变化时，你的脚本都必须停止 `ssh` 并使用备用配置文件重新启动。 |
| `-i` | 使用此选项通知 `ssh` 在 `inetd` 中运行。作者建议不要这样做，而且很有道理。当从 `inetd` 启动时，`ssh` 的性能可能会很缓慢，因为它必须为每个会话生成密钥。 |
| `-k [time]` | 使用此选项指定 `ssh` 重新生成密钥的频率。默认情况下，`ssh` 每小时重新生成一次。该时间单位为秒。注意，值 `0` 并不表示永久重新生成，而是完全不重新生成。 |
| `-p [port]` | 使用此选项指定运行 `ssh` 的备用端口。默认端口 `22`。注意，除非你从 `inetd` 运行 `ssh`，否则如果你更改了默认端口，可能需要通知用户。（默认情况下，`ssh` 客户端针对端口 `22`）。 |
| `-q` | 使用此选项指定 `ssh` 在静默模式下运行（即不进行任何日志记录）。 |

## `/etc/ssh_config`: `ssh` 客户端配置文件

`etc/ssh_config` 是 `ssh` 客户端配置文件。默认情况下，它看起来如下：

```
# 这是 ssh 客户端系统级配置文件。此文件

# 为用户提供了

# 默认值，可以在用户配置

# 文件或命令行中更改这些值。
```

```
# 配置数据的解析方式如下：

# 1. 命令行选项

# 2. 用户特定文件
```
