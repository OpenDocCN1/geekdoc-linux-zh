
## 监控 Linux 防火墙

### 配置 iptables 策略

```bash
$ sudo iptables -P OUTPUT DROP
$
$ ping -c 3 192.168.0.105
PING 192.168.0.105 (192.168.0.105) 56(84) bytes of data.
sendmsg: Operation not permitted
[...
$ sudo iptables -P OUTPUT ACCEPT
$
$ ping -c 3 192.168.0.105
PING 192.168.0.105 (192.168.0.105) 56(84) bytes of data.
64 bytes from 192.168.0.105: icmp_seq=1 ttl=0.062 ms
[...]
$ 
```

在列表 18.7 中，将默认 `OUTPUT` 链改回 `ACCEPT` 策略后，`ping` 数据包是被允许的。

`iptables` 服务防火墙仅对 IPv4 数据包由 `iptables` 命令管理。如果你有 IPv6 数据包通过网络，你还必须使用 `ip6tables` 命令。

要更改链规则，你需要在 `iptables` 命令中使用额外的命令行选项。这些规则选项见表 18.3。

## 表 18.3 `iptables` 命令的常用链选项

| 选项 | 描述 |
| :--- | :--- |
| `-d address` | 仅适用于此目的地址的数据包 |
| `-s address` | 仅适用于此源地址的数据包 |
| `-i name` | 仅适用于通过 `name` 网络接口进入的数据包 |
| `-o name` | 仅适用于通过 `name` 网络接口输出的数据包 |
| `-p protocol` | 仅适用于使用此协议的数据包 |
| `-j target` | 指定规则的目标 |

如果你需要保存当前的 `iptables` 规则，请使用 `iptables-save` 命令。该工具需要将其输出重定向到文件，因为默认情况下会将规则发送到标准输出（`STDOUT`）。

要恢复 `iptables` 规则，请使用 `iptables-restore` 命令。该工具需要从文件重定向输入。因此，如果你正在测试一个效果不佳的 `ACL` 更改，可以快速恢复 `iptables` 规则。在旧版本的 `Fedora` 发行版上，请使用超级用户权限并执行 `iptables-restore < /etc/sysconfig/iptables` 命令来恢复原始 IPv4 规则。

## 理解 UFW

`Uncomplicated Firewall`（简单防火墙）是 `Ubuntu` 发行版上的默认防火墙服务。它可以通过 `ufw` 命令行工具或用于图形界面的 `Gufw` 进行配置。

![](img/0c1e7d2699b9d354c8d2f84669d18d73_555_0.png)

默认情况下，`UFW` 服务是禁用的。你通过使用 `sudo ufw enable` 命令启动服务并将其设置为开机启动，但请勿使用系统初始化工具（如 `systemctl`）。这是因为此处介绍的防火墙服务不是传统的 `SysV` 或 `systemd` 服务，而是 `netfilter` 防火墙的接口服务。因此，如果你选择启动 `UFW`，请注意 `iptables` 或防火墙服务本身都不能处于运行状态。

有几个 `UFW` 命令可以控制防火墙的状态并查看其状态。这些命令如表 18.4 中。每条命令都需要超级用户权限。

## 表 18.4 控制状态和查看状态的 `ufw` 命令

| 命令 | 描述 |
| --- | --- |
| `ufw enable` | 启动 `UFW` 防火墙并允许在系统启动时启动 |
| `ufw disable` | 停止 `UFW` 防火墙并禁用其开机启动 |
| `ufw reset` | 禁用 `UFW` 防火墙并将其重置为安装默认值 |
| `ufw reload` | 重新加载 `UFW` 防火墙 |
| `ufw status` | 显示 `UFW` 防火墙的当前状态 |

要查看 `UFW` 服务的当前状态，如果需要比状态提供的更多信息，请使用 `sudo ufw status verbose`。启用 `UFW` 防火墙服务并查看其当前状态见列表 18.10。

### 列表 18.10：启用 `UFW` 并查看其状态

```bash
$ sudo ufw enable
[...
Firewall is active and enabled on system startup
$

$ sudo ufw status verbose
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), disabled (routed)
New profiles: skip
$
```

查看 `UFW` 防火墙的详细状态可以提供有助于解释其配置的信息：

- `Status`（状态）：`UFW` 服务正在运行并将在系统启动时启动（`active`），或者服务已停止且系统启动不会改变此状态（`disabled`）。
- `Logging`（日志）：服务的日志功能可以设置为关闭（`off`）；记录所有被阻止的数据包（`Low`），这是默认值；记录所有被阻止的、无效的、无策略匹配以及新连接的数据包（`medium`）并带有速率限制；记录中级日志包及所有其他数据包（`high`）并带有速率限制；无速率限制地记录所有内容（`full`）。
- `Default`（默认）：显示入站、出站和路由数据包的默认策略，可以设置为允许数据包（`allow`）、丢弃数据包（`drop`/`deny`）或拒绝数据包（`reject`）并返回拒绝消息。
- `New profiles`（新配置文件）：显示自动将新配置文件加载到防火墙的默认策略，可以设置为 `ACCEPT`、`DROP`、`REJECT` 或 `SKIP`，其中 `ACCEPT` 被认为存在安全风险。

各种默认 `UFW` 策略存储在 `/etc/default/ufw` 文件中。安装时，这些设置允许所有出站连接并阻止所有入站连接。你可以使用 `ufw` 命令及其各种参数对防火墙进行修改。表 18.5 显示了其中一些较常用的参数。

## 表 18.5 `ufw` 命令的常用参数

| 参数 | 描述 |
| --- | --- |
| `allow Identifiers` | 设置由 `Identifiers` 标识的规则以允许数据包 |
| `deny Identifiers` | 设置由 `Identifiers` 标识的规则以拒绝（丢弃）数据包 |
| `reject Identifiers` | 设置由 `Identifiers` 标识的规则以拒绝数据包 |
| `delete RULE NUM` | 删除由 `RULE` 或 `NUM` 标识的规则 |

### 表 18.5 `ufw` 命令的常用参数（续）

| 参数 | 描述 |
| --- | --- |
| `insert NUM RULE` | 在索引 `NUM` 处插入 `RULE` |
| `default DIRECTION` | 修改默认 `DIRECTION` 策略，其中 `POLICY` 为 `allow`、`deny` 或 `reject`，`direction` 为 `incoming`、`outgoing` 或 `routed` |
| `logging LEVEL` | 设置日志级别，其中 `LEVEL` 为 `on`、`off`、`low`（默认）、`medium`、`high` 或 `full` |

在创建新的 `UFW` 规则时，可以使用简单语法或完整语法。简单语法涉及仅使用端口号或其服务名来指定规则。你也可以如列表 18.11 所示向端口号上添加协议。

### 列表 18.11：使用 `ufw` 简单语法添加 `ACL` 规则

```bash
$ sudo ufw allow 22/tcp
Rule added
Rule added (v6)
$
$ sudo ufw status
Status: active
```

| 目标 | 动作 | 来源 |
| --- | --- | --- |
| `22/tcp` | `ALLOW` | `Any` |
| `22/tcp (v6)` | `ALLOW` | `Any` |

注意，使用完整语法时，你可以指定协议和端口。例如，`ufw allow 22/tcp` 允许端口 `22` 上的 `TCP` 流量。

各种默认 `UFW` 策略存储在 `/etc/default/ufw` 文件中。安装时，这些设置允许所有出站连接并阻止所有入站连接。你可以使用 `ufw` 命令及其各种参数对防火墙进行修改。

你也可以如列表 18.15 所示，查看这些配置文件的详细信息。

这些配置文件不仅提供了应用程序文档，还允许你修改应用程序使用的端口和协议，并根据你的系统需求创建非典型的应用程序配置。

> 不要修改 `/etc/ufw/applications.d/` 目录下的配置文件。

相反，请在该处创建一个子目录并将其命名为 `custom.d`。这将防止你的自定义配置被 `UFW` 软件包的更新所覆盖。关于配置规范的更多信息，请参考 `ufw` 手页。

一旦你创建了新配置或更新了旧配置，请使用 `ufw app update all` 命令更新配置更改。此外，当使用配置指定规则的端口和协议时，在创建新规则的语法中必须使用 `app` 而不是 `port`。

## 转发 IP 数据包
