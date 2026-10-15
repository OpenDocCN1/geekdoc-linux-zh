
# 守护进程 (Daemons)

- `smbd` - SMB 守护进程
- `nbdd` - NetBIOS 节点服务器

# 管理工具

- `smbstr` - 监控 Samba
- `swat` - Web 配置工具
- `smpass` - 管理 SMB 密码
- `maker` - 多协议用户创建
- `testarm` - 验证你的配置文件
- `testpr` - 测试打印机配置

# 通用工具

- `nlookup` - NetBIOS 查询工具
- `smedit` - SMB 备份工具
- `smclient` - 命令行 SMB 客户端

# 配置文件

- `smb.conf` - Samba 主配置文件
- `hosts.txt` - NetBIOS 机文件

图 6.1: Samba SWAT 管理工具

## 全局变量

| | 更改 | 重置值 | 高级视图 |
| :--- | :--- | :--- | :--- |
| 基础选项 (Base Options) | | | |
| `workgroup` | EYRIE | | 设置默认值 |
| `netbios` | Opus Samba Server | 设置默认值 |
| `server string` | | | 设置默认值 |
| `interface` | | | |
| 安全选项 (Security Options) | | | |
| `security` | USER | | 设置默认值 |
| `encrypt passwords` | Yes | 设置默认值 |
| `update encrypted` | No | 设置默认值 |
| `guest account` | | | 设置默认值 |
| `hosts allow` | 148.12.118.127 | | |
| `hosts deny` | | | 设置默认值 |
| 日志选项 (Logging Options) | | | |
| `log level` | 1 | 设置默认值 |
| `log file` | UseFile:/var/log/swat.log | | |
| `max log size` | 0 | | |
| 调优选项 (Tuning Options) | | | |
| `socket options` | TCP_NODELAY | | 设置默认值 |
| 浏览选项 (Browse Options) | | | |
| `os level` | 0 | 设置默认值 |
| `preferred master` | No | 设置默认值 |
| `local master` | Yes | 设置默认值 |
| `domain master` | No | 设置默认值 |

**图 6.2:** SWAT 节配置表单示例

SWAT 默认安装在 `$(BASEDIR)/swat` 目录下，作为 Samba 通用构建和安装的一部分。在使用 SWAT 之前，你需要向 `/etc/services` 和 `/etc/inetd.conf` 中添加条目，向你的系统标识服务和名称（示例 6.2）。在做出更改后，不要忘记向 `inetd` 守护进程发送 HUP 信号。一旦在你的系统中配置了 SWAT，你就可以在你喜欢的窗口中调用该服务。访问以下 URL 时，SWAT 将提示你输入管理员用户名和密码。

> **警告：** SWAT 在重写你的 `smb.conf` 时会删除所有注释、`include=` 和 `copy`。如果你使用这些参数来从一个 `smb.conf` 支持多个 Samba 安装，请务必记住这一点。

# 示例 6.2 /etc/services:

```
/etc/services
    swat      901/tcp
```

`/etc/inetd.conf`:

```
swat stream now
/usr/local/samba/bin/swat
```

# 变量和文件替换

变量替换是一个有助于简化 `smb.conf` 配置的强大 Samba 特性。Samba 提供了一组固定的变量，这些变量以 `$` 符号为前缀，并在运行时处理期间获取值。变量替换可以用于 `smb.conf` 文件中任何字符串值有效的地方。例如，`%` 变量通常用于将请求客户端的 NetBIOS 名称与本地服务器资源（如文件）关联。

```
log file = /usr/local/samba/var/%m.log
```

某些变量位于共享节（share section）的上下文中。这些可能包括请求的服务名称或经过验证的帐户名称。其余变量集可用于所有节。表 6.3 列出了预定义的变量。

# 表 6.3 smb.conf 定义变量

- `%G` = 主组名称
- `%I` = 客户端的 NetBIOS 名称
- `%L` = 共享名称
- `%M` = Samba 机名
- `%R` = 协议版本
- `%T` = 当前日期和时间
- `%U` = 用户名
- `%A` = 架构
- `%d` = 服务的进程 ID
- `%h` = 运行 Samba 的主机
- `%m` = 客户端的主机
- `%p` = 变量路径
- `%v` = Samba 版本

# 共享上下文变量

- `%H` = 运行会话的用户名
- `%P` = 服务的会话
- `%S` = 共享名称
- `%g` = 主组名称
- `%u` = 会话用户名

## 自动化

`preexec` 和 `postexec` 参数提供了一种在访问和释放共享时分别调用命令、脚本或程序的机制，这些服务器在 root 权限下执行这些程序。在使用 root 版本的之前，请仔细考虑应用范围。在大多数情况下，可以找到 root 权限下的替代方案产生相同的结果。

```
preexec = <command or script path>
```

```
postexec = <command or script path>
```

```
root preexec = <command or script path>
```

```
root postexec = <command or script path>
```

这些参数对于管理公共资源非常有用。例如，`preexec` 可用于为公共实验室创建并设置权限。当用户在注销时从服务器时，`postexec` 可以被调用以移除工作目录以及浏览器缓存和其他清理活动。这些参数的其他用途包括在访问会话时在弹出窗口中显示系统或信息消息。

## 全局节

`smb.conf` 配置文件的 `[global]` 节描述了服务器在工作组或域中扮演的角色，定义了默认参数值，并设置了管理文件和网络选项的限制和控制。角色信息识别服务器的 NetBIOS 和域名称，如果需要，通过在各个节中分配新值来显式覆盖节默认值。

全局节是未在特定资源定义中明确声明的 Samba 函数的一个汇总。在第 7 到 10 章中，我们将仔细查看组成全局节的一些更复杂的函数定义。这些包括身份验证服务、浏览和域配置。为了测试目的，你可能会从示例 6.3 中列的一些通用参数开始。完整的全局节参数列在表 6.4 中。

## 示例 6.3 全局节参数示例

```
netbios name = 标识 NetBIOS 名称
```

```
workgroup =标识工作组或域
```

```
guest account = 用于访问标记为 "guest ok" 的服务的访客帐户
```

```
security = 指定登录安全设置为“user”、“share”、“server”或“domain”
```

`encrypt passwords` = 是否应为 Win9x 客户端协商加密密码。需要在 `smbpasswd` 文件中生成 NT 加密密码。请参阅 Samba 目录下的 `ENCRYPTION.txt`。

`load printers` = 从 `printcap` 文件加载可浏览的打印机列表。

`log file` = Samba 日志目录路径

`max log size` = 以字节（KB）为单位限制日志文件大小

`dns proxy` = 是否让 Samba 通过 DNS 查找解析 NetBIOS 名称？

## 表 6.4 全局参数列表

| 参数 |
| :--- |
| `add user script` | 添加用户脚本 |
| `allow trusted domains` | 允许信任域 |
| `announce as` | 发布为 |
| `announce version` | 发布版本 |
| `auto services` | 自动服务 |
| `bind interfaces only` | 仅绑定接口 |
| `browse list` | 浏览列表 |
| `change notify timeout` | 更改超时 |
| `character set` | 字符集 |
| `client code page` | 客户端代码页 |
| `coding system` | 编码系统 |
| `config file` | 配置文件 |
| `deadtime` | 空闲时间 |
| `debug timestamp` | 调试时间戳 |
| `debuglevel` | 调试级别 |
| `default` | 默认 |
| `default service` | 默认服务 |
