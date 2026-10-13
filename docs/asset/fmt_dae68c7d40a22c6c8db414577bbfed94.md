
iptables 包提供了对 IPv6 建模的支持。它与 IPTables 相同，不同之处在于允许使用 IPv6 地址而不是 IPv4 地址（见见第 37 章）。iptables 同时支持 `filter`（过滤）和 `mangle`（修改）表，但不支持 NAT 表。`filter` 表支持与 IPTables 相同的选项和命令。`mangle` 表允许专门的数据包更改，例如使用 `PREROUTING`、`INPUT`、`OUTPUT`、`FORWARD` 和 `POSTROUTING` 规则。扩展具有 `ipv6` 标签，例如 `ipv6-icmp`，它对应于 iptables `icmp` 扩展。`ipv6 headers` 用于选择 IPv6 头。

## 模块

与其前身 IP Chains 不同，Netfilter 设计为模块化和可扩展的。功能可以通过模块的形式添加，例如 `state` 模块，它添加了连接跟踪。大多数模块作为 IPTables 服务的一部分加载。其他模块是可选的；你可以选择在安装它们之前加载它们。Fedora Core 系统上的 IPTables 模块位于 `/usr/lib/kernel-version/kernel/net/ipv4/netfilter`，其中 `kernel-version` 是你的内核版本，例如 `2.6.9-167`。对于 IPv6 模块，检查 `ipv6/netfilter` 目录。自动带有 `ip_prefix` 的模块和可选模块仅有一个 `ip_prefix`。

可选模块可以指定为一个列表赋值给 `/etc/sysconfig/iptables-config` 文件中的 `IPTABLES_MODULES` 参数，该文件由 iptables 服务脚本使用。每当你使用 iptables 服务脚本启动 IPTables 时，它们将自动加载。

```
# service iptables start
```

如果你在编写自己的 iptables 脚本，而不是使用 Fedora Core 的 iptables 脚本，你必须添加 `modprobe` 来直接加载可选命令。

> 注意 IPTables 包包含了针对 ipfwadm 和 IP Chains 的向后兼容模块。事实上，IPTables 与 IP Chains 非常相似。通过加载 Netfilter 软件提供的 `ipchains.o` 或 `ipfwadm.o` 模块，可以实现早期的 ipfwadm 命令。这些模块提供了完全的向后兼容性。

## 数据包过滤

Netfilter 本质上是一个数据包管理框架，它可以检查特定网络协议的数据包并通知内核中监听这些数据包的各个部分构建在 Netfilter 框架之上的是 IPTables 实现的数据包选择系统。通过 IPTables，可以设置不同的规则表来根据不同的标准选择数据包。Netfilter 目前支持三张表：`filter`、`nat` 和 `mangle`。数据包过滤使用 `filter` 表实现，该表持有丢弃或接受数据包的规则。网络地址转换操作（如 IP 伪装）使用 NAT 表实现。`mangle` 表用于专门的数据包更改。更改可以在数据包发送前、接收时或转发时进行。这种结构是可扩展的，因为新模块可以定义自己的表。

IP 表规则使用 `iptables` 命令管理。对于此命令，你需要指定要管理的表。默认是 `filter` 表，不需要指定。你可以随时使用 `-L` 和 `-n` 选项列出你添加的规则，所示。`-n` 选项表示对地址和端口都使用数字输出，避免对主机名的 DNS 查询。然而，你可以使用 `-L` 选项查看端口标签和主机名：

```
iptables -Ln
```

> 注意在 IPTables 命令中，链名必须大写，例如链名 `INPUT`、`OUTPUT` 和 `FORWARD`。

## 链

规则组合不同的链。内核使用链来管理接收和发送的数据包。链简单来说规则列表。规则规定了对包含特定头部的数据包的操作。规则以 if-then-else 结构运行。如果数据包不匹配第一个规则，则检查下一个规则，依此类推。如果数据包不匹配任何规则，内核将查询链策略。通常，此时数据包会被拒绝。如果数据包匹配规则，它将被传递到目标（target），由目标决定对数据包进行什么。标准目标列在表 20-2 中。如果数据包不匹配任何规则，它将被传递到链的默认目标。

## 目标

目标反过来可以是另一个链，甚至是一个用户定义规则的链。数据包在最终到达目标之前可能会经过多个链。在用户定义的情况下，

| 表 20-2 | 功能 |
| --- | --- |
| IPTables 目标 | `ACCEPT` 允许数据包通过防火墙。 |
| `DROP` 拒绝数据包的访问。 |
| `REJECT` 拒绝访问并通知发送者。 |
| `QUEUE` 将数据包发送到用户空间。 |
| `RETURN` 跳到链的末尾并让默认目标处理它。 |

对于已定义的链（chains），默认程序始终是调用它的链中的下一条规则。这在编程语言中建立了类似于过程调用或函数调用的控制流。当某个规则以用户定义的链作为目标并被激活时，将执行用户定义的链。如果没有匹配到任何规则，执行流将返回到原始链中的下一条规则。

提示：可以通过 Netfilter 网站提供的内核补丁添加特殊的目标和选项。例如，`SAME` 补丁会为所有连接返回相同的地址。Netfilter make 的“补丁化（patch-omatic）”选项将补丁你的内核源代码，添加对新目标和选项的支持。然后你可以重新编译并安装内核。

# 防火墙和 NAT 链

内核使用三个链：`INPUT`、`OUTPUT` 和 `FORWARD`。当通过接口接收数据包时，使用 `INPUT` 链来确定对其如何处理。内核随后使用其路由信息决定将其发送到何处。如果内核将包发送到另一个主机，则会检查 `FORWARD` 链。在实际发送包之前，还会检查 `OUTPUT` 链。此外，还实现了两个 NAT 表链——`POSTROUTING` 和 `PRERUTING`，用于处理伪装（masquerading）和包地址修改。内置的 Netfilter 链如表 20-3 所示。

# 添加和修改规则

你使用 `iptables` 命令添加和修改链规则。一个 `iptables` 命令由关键字 `iptables` 组成，后跟着一个表示要执行命令的参数。例如，`iptables -A` 是添加新规则的命令，而 `iptables -D` 是删除规则的命令。`iptables` 命令如表 20-4 所示。以下命令简单列出了系统当前定义的链及其规则。输出显示了 `iptables` 命令创建的默认值。

```
iptables -L -n
Chain input (policy ACCEPT):
Chain forward (policy ACCEPT):
Chain output (policy ACCEPT):
```

| 表 20-3 Netfilter 内置链 | 链 | 描述 |
|---|---|---|
| | `INPUT` | 用于入站数据包的规则 |
| | `OUTPUT` | 用于出站数据包的规则 |
| | `FORWARD` | 用于转发数据包的规则 |
| | `PREROUTING` | 重定向或修改传入数据包的规则，仅限 NAT 表 |
| `POSTROUTING` | 重定向或修改出站数据包的规则，仅限 NAT 表 |

| 表 20-4 命令 | 功能 |
|--- |--- |
| IPTables 命令 | 向链中追加规则。 |
| `-A chain [denum]` | 从链中删除匹配的规则。删除链中的规则 rulenum（1 = 第一条）。 |
| `-I chain [denum]` | 在链中插入到 rulenum 处（默认 1 = 第一条）。 |
| `-R chain rulenum` | 替换链中的规则 rulenum（1 = 第一条）。 |
| `-L [chain]` | 列出链或所有链中的规则。 |
| `-E [chain]` | 重命名链。 |
| `-F [chain]` | 删除（清空）链或所有链中的所有规则。 |
| `-R chain` | 替换规则；规则从 1 开始编号。 |
| `-Z [chain]` | 将链或所有链中的计数器归零。 |
| `-N chain` | 创建一个新的用户自定义链。 |
| `-X chain` | 删除用户自定义链。 |
| `-P chain target` | 将链的策略更改为目标。 |

要向链添加新规则，请使用 `-A`。使用 `-D` 移除，使用 `-R` 替换。执行命令后，列出规则适用的链，例如 `INPUT`、`OUTPUT` 或 `FORWARD` 链，或用户自定义链。接下来，列出指定你想要执行的操作的不同选项（与 IP 链使用的选项相同，极少数例外）。`-s` 选项指定与数据包的源地址，`-d` 指定目的地址，`-j` 选项指定规则的目标。`ACCEPT` 目标允许包通过。`-i` 选项现在指示输入设备，只能用于 `INPUT` 和 `FORWARD` 链。`-o` 选项指示输出设备，只能用于 `OUTPUT` 和 `FORWARD` 链。表 20-5 列出了若干基本选项。

# IPTables 选项
