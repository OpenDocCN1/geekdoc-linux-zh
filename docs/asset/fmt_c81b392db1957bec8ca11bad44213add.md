
## 编译 TCP 支持

当 TCP wrappers 使用 `-DPARANOID` 选项编译时，它们将丢弃任何正向和反向 DNS 条目不匹配的机器的连接。这让许多无法修复其 DNS 条目的系统管理员警觉。然而，拥有匹配的记录是你开始相信主机确实是其声称的身份的唯一方法。毕竟，如果管理员不能保持其记录同步，你如何信任这些系统呢？

如果你自己编译 TCP wrappers，请指定 `-DPARANOID` 选项。大多数发行版默认如此。

# 编写不当的 TCP Wrapper 规则滥用

| 流行度 | 4 |
| --- | --- |
| 简单性 | 6 |
| 影响 | 8 |
| 风险等级 | 6 |

你已经实现了 TCP wrappers 并向 `/etc/hosts.deny` 和 `/etc/hosts.allow` 添加了规则，但 TCP wrappers 似乎并没有正常工作。希望你确定这一点的是因为你正在手动检查允许的连接，但通常你是在通过惨痛的方式发现的——当攻击者开始攻击本应被阻止的网络服务时。

TCP wrappers 无法正确拒绝访问通常是因为某个配置文件中存在拼写错误。

# 检查 TCP Wrapper 的有效性

`tcpdchk` 和 `tcpdmatch` 程序是用于验证 `/etc/inetd.conf`、`/etc/hosts.allow` 和 `/etc/hosts.deny` 中定义的 TCP wrapper 规则的工具。

### 使用 tcpdchk 验证你的 TCP Wrappers
`tcpdchk` 程序检查 TCP wrapper 配置，并报告它能找到的所有真实和潜在问题。`tcpdchk` 程序检查 `/etc/hosts.allow` 和 `/etc/hosts.deny`，并将其条目与 `/etc/inetd.conf` 进行比较。

```
tcpdchk [-a] [-d] [-i inetd.conf]
```

`tcpdchk` 报告的问题包括：

- 不存在的路径
- 出现在 `/etc/hosts.allow` 和 `/etc/hosts.deny` 中但未受 `tcpd` 控制的服务（例如 `httpd`）
- 不应被封装的服务
- 不存在的主机名
- 错误的 IP 地址格式
- 具有名称/地址冲突的主机
- 通配符使用语法错误

# 破解 Linux Linux：Linux 安全秘密与解决方案

此外，`tcpdchk` 经常提供有关如何修复问题的信息。
`tcpdchk` 的选项包括：

| 选项 | 定义 |
| --- | --- |
| -a | 报告在没有显式 ALLOW 的情况下允许访问的访问控制规则（仅在编译 TCP wrappers 时使用了 -PROCESS_OPTIONS 时使用）。 |
| -d | 使用当前目录下的 `/etc/hosts.allow` 和 `/etc/hosts.deny` 文件。 |
| -i inet_conf | 使用 `inet_conf` 代替 `/etc/inetd.conf`。 |
| -v | 使用详细模式。 |

### 使用 tcpdmatch 检查 TCP Wrapper 配置
`tcpdmatch` 程序检查 TCP wrapper 配置并预测服务请求将如何被处理。`tcpdmatch` 检查访问控制表 `/etc/hosts.allow` 和 `/etc/hosts.deny` 以及 `/etc/inetd.conf`。当 `tcpdmatch` 找到匹配时，它会打印匹配的规则以及任何相关的 shell 命令。`tcpdmatch` 的语法为

```
tcpdmatch [-d] [-i inet_conf] daemon client
```

`tcpdmatch` 的选项包括：

| 选项 | 定义 |
| --- | --- |
| -d | 使用当前目录下的 `/etc/hosts.allow` 和 `/etc/hosts.deny` 文件。 |
| -i inet_conf | 使用 `inet_conf` 代替 `/etc/inetd.conf`。 |

以下是当 localhost 尝试 telnet 时检查 TCP wrapper 配置的示例：

```
machine# tcpdmatch in.telnet localhost

client: hostname localhost

client: address 127.0.0.1

server: process in.telnet

matched: /etc/hosts.allow line 7

access: granted
```

以下是当 123.266.7.8 尝试 SSH 时检查 TCP wrapper 配置的示例：

```
machine# tcpdmatch sshd 123.266.7.8

warning: sshd: no such process name in /etc/inetd.conf

client: address 123.266.7.8

server: process sshd

matched: /etc/hosts.deny line 11

access: denied
```

第二个示例中的“no such process name”是因为 `sshd` 是一个独立的守护进程，不是由 `inetd` 用的。因此，这是预期的。你可以使用 `sshd -i` 从 `inetd` 运行 sshd，但这会导致巨大的性能影响，因为每个 ssh 服务器必须使用自己的随机数生成器并创建临时密钥。这是一项大量的工作，并且花费相当长的处理时间；大多数人倾向于在守护模式中使用 `sshd`。

# 第 13 章：访问控制与防火墙

# 针对 inetd 的资源耗尽攻击

| 流行度 | 6 |
| --- | --- |
| 简单性 | 6 |
| 影响 | 8 |
| 风险等级 | 6 |

使用 TCP wrappers 为 telnet 提供了主机控制。然而，黑客可以访问一台允许连接到你机器的机器。在没有用户名/密码的情况下，黑客决定通过向你的机器发起数千次 telnet 连接来启动资源耗尽攻击。这些连接消耗了资源和进程，导致你的机器过载，从而无法响应 HTTP 或 FTP 等有效连接。

# 使用 tcpserver 防御耗尽

如果你没有使用 `inetd`，可以使用 `tcpserver` 限制到服务的连接数。该程序允许你执行主机控制，并提供与 TCP wrappers 相同的控制。与 `inetd` 不同，你为你想要支持的每个连接运行一个 `tcpserver`。你可以在 http://www.hackinglinuxexposed.com/tcpserver.html 找到 `tcpserver`。

# 使用 inetd 防御耗尽

`inetd` 有两个内置功能可以帮助解决资源耗尽问题：

- 限制每个服务的并发连接总数。
- 限制每个 IP 地址到单个服务的总连接数。

# 破解 Linux Linux 安全秘密与解决方案

这两个功能在章节的早些时候当我们把 `/etc/inetd.conf` 转换为 `/etc/xinetd.conf` 时自动配置了。当我们运行此程序时，它将这些行放在了默认部分：

```
instances = 25

per_source = 5
```
