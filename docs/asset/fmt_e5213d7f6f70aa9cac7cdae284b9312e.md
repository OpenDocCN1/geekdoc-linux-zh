
原因是这样的：如果你只指定了 `/etc/hosts.allow` 条目，那么只有 `techsupport.mycompany.net` 被拒绝了。

作为一个一般原则，你应该先在 `/etc/hosts.deny` 文件中添加 `ALL:`。这允许所有人访问。从那里开始，你可以添加授权的主机。之所以这样做是因为，指定“不允许的被拒绝”比指定“哪些允许的”更容易且更安全。这样，你就考虑到了意外情况。

但不仅如此。`hosts_options` 允许你进入深入、细微的细节。例如，假设 `/etc/hosts.deny` 包含以下条目：

```
ALL: .aol.com, .msn.com
```

```
ALL EXCEPT in.telnet:techsupport.mycompany.net
```

在这里来自 AOL 和 MSN 的人被完全屏蔽，但来自 `techsupport.mycompany.net` 的人可以访问 `telnet` 服务。

# hosts_options 通配符、运算符和 Shell 函数

考虑到你可能想应用一些范围性的规则，Venema 还在 `hosts_options` 中引入了多个通配符语句。这些总结在表 18.1 所示。

# Linux 与防火墙

# 第 18 章

# 表 18.1 hosts_options 通配符

| 通配符 | 功能 |
| --- | --- |
| ALL | 用于泛指匹配，包括所有（ALL）服务和所有（ALL）远程主机。例如，在 `/etc/hosts.deny` 中 `ALL: ALL` 拒绝所有主机访问所有服务。（反之，`/etc/hosts.allow` 中的 `ALL: ALL` 允许所有主机访问所有服务，这是你绝对不希望允许的）。 |
| KNOWN | 当你想对在访问控制规则中显式命名的用户和主机应用规则时，请使用此项。 |
| LOCAL | 用于不包含点的主机名（例如你的本地主机）。 |
| PARANOID | 如果你想在主机名与其 IP 地址不匹配时丢弃主机，请使用此项。 |
| UNKNOWN | 当你想拒绝访问未知主机或用户名时，使用此项。换句话说，如果这些用户和主机没有在访问控制规则中显式命名，它们将被拒绝访问。 |

# EXCEPT 运算符

最后，`hosts_options` 支持一个运算符：`EXCEPT`。你可以使用 `EXCEPT` 为此守护进程或客户端列表中的特定规则创建异常。例如，假设你在 `/etc/hosts.deny` 中输入了这一行：

`ALL EXCEPT in.telnet:techsupport.mycompany.net`

在这里，你拒绝除了 `telnet` 之外的所有服务对 `techsupport` 主机的访问。但你也可以堆叠 `EXCEPT` 声明，如下所示：

- `list except list except list`
- `tcpdchk`—TCP Wrappers 配置检查器
- `tcpmatch`—TCP Wrappers 预测器

正如你所预期的，如果不添加条件执行的 shell 命令，这可能会变得复杂。因此，TCP Wrappers 自带了你可以用于验证规则的工具：

让我们现在快速概述它们。

# tcpdchk: TCP Wrappers 配置检查器

`tcpdchk` 是一个验证你的 TCP Wrappers 设置的工具。正如 `tcpden` 手册页中所述：

`tcpdchk` 检查你的 TCP Wrappers 配置并报告它能发现的所有潜在和实际问题。该程序检查 tcp 访问控制文件（默认是 `/etc/hosts.allow` 和 `/etc/hosts.deny`），并将条目与 `inetd` 或 `xinetd` 网络配置文件中的条目进行比较。

![](img/238ef1f85709de12ba67e71734ee1e37_518_0.png)

## Linux 网络安全
第四部分

`tcpdchk` 分析你的配置以检查以下问题：

- 语法错误
- 错误的路径名
- 错误的主机名或 IP 地址
- 与 IP 地址不对应的主机名（`PARANOID` 通配符功能的扩展）
- 你在规则中指定但实际上未被 `tcpdchk` 封装的服务

`tcpdchk` 支持多个命令行选项，总结在表 18.2 中。

# 18.2 tcpdchk 命令行选项

| 选项 | 功能 |
| --- | --- |
| -a | 使用此项指定 `tcpdchk` 报告没有伴随显式 `ALLOW` 通配符的允许规则。 |
| -d | 使用此项指定 `tcpdchk` 测试当前目录下的 `.hosts.allow` 和 `hosts.deny` 规则，而不是 `/etc`。这在你部署规则之前在另一个目录中构建规则时有用。 |
| -i [inetd.conf] | 使用此项指定你正在使用的替代 `inetd.conf` 或 `tcpdchk.conf`（如果不是默认值），因为它会测试你是否已将访问控制规则应用于实际被封装的服务。 |
| -v | 使用此项获取详细且格式整齐的输出。 |

# tcpmatch: TCP Wrappers 预测器

`tcpmatch` 检查你的规则以确保它们是合理的，而 `tcpmatch` 实际上向你展示部署后会发生什么。正如 `tcpmatch` 手册页中所述：

`tcpmatch` 预测 TCP Wrappers 如何处理特定的服务请求。

语法为 `tcpmatch [daemon] [host]`，如下：

`tcpmatch in.telnet techsupport.theircompany.net`

# TCP Wrappers 总结

TCP Wrappers 是你在无需实际部署全规模包过滤器（或更多）的情况下可以获得的最接近防火墙的功能。当你无法使用防火墙但仍需要网络访问控制时，它是完美的选择。

# Linux 与防火墙
第 18 章

例如，假设你有一个主机，你想阻止除 HTTP 流量以外的所有流量。你可以这样做，但仍为端口 22 上的 SSH 连接留一个口，以便开发者可以上传文件、更改权限、配置脚本等。对于这些任务，TCP Wrappers 绰绰有余。

另一方面，你可能需要更多功能，例如真实的包过滤。如果是这样，请使用 `ipfwadm`（用于内核2之前的内核）或 `iptables`。

# ipfwadm

`ipfwadm` 是一个用于 Linux 的包过滤工具。正如手册所示：

`ipfwadm` 用于在内核中设置、维护和检查防火墙规则。这些规则可以分为四类：计数、输入防火墙、输出防火墙和转发防火墙。对于这些每一类，都维护着单独的列表。对于这样一个小型实用程序，`ipfwadm` 本身就是一个强大的防火墙。

# ipfwadm 基础

`ipfwadm` 允许你对传入和流出的流量设置规则。基础 `ipfwadm` 语法为：

```
ipfwadm [rule_category] [policy_action] [policy] [interface] [target]
```
