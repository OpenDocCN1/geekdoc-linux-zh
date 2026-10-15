
此规则将允许所有通过 `FORWARD` 链且目标为 `10.100.93.0/24` 网络的数据包。

- `-j target` 此选项指定要“跳转”到的动作。在 `iptables` 术语中，这些动作被称为目标（targets）。我们目前为止看到的目标有 `ACCEPT`、`DROP` 和 `RETURN`。前两个分别是接受和丢弃数据包。第三个与创建额外的链有关。

正如我们在上一节中看到的，可以创建自己的链来保持结构整洁并容纳更多规则。如果 `iptables` 正在评估一个非内置链中的规则集，`RETURN` 目标将告诉 `iptables` 回到父链。使用早先的 `to-net10` 示例，当 `iptables` 到达 `-j RETURN` 时，它将返回到之前停止的 `FORWARD` 链继续处理。如果 `iptables` 在其中一个内置链中看到 `RETURN` 动作，它将执行该链的默认规则。

可以通过 Netfilter 模块加载额外的目标。例如，可以使用 `ip_REJECT` 加载 `REJECT` 目标，它将丢弃数据包并向发送者返回 ICMP 错误。另一个用的目标是 `ipt_REDIRECT`，如果数据包的目标是其他地方，它可以使其目标变为 NAT 主机本身。

- `-i interface` 此选项指定接收数据包的接口名称。这对于从物理位置（如 DMZ 接口）到达时应用特殊规则的情况非常方便。如果 `eth1` 是你的 DMZ 接口，且你想允许它向主机 `10.4.3.2` 发送包，你可以：

```
[root@serverA]# iptables -A FORWARD -i eth1 -d 10.4.3.2 -j ACCEPT
```

- `-o interface` 此选项指定数据包离开系统的接口名称。例如：

```
[root@serverA]# iptables -A FORWARD -i eth0 -o eth1 -j ACCEPT
```

在此示例中，来自 `eth0` 并离开 `eth1` 的任何包都会被接受。

- `-f` 此选项指定数据包是否为 IP 分片。感叹号取反此规则。例如：

```
[root@serverA]# iptables -A INPUT -f -j DROP
```

在此示例中，进入 `INPUT` 链的任何 IP 分片都会被自动丢弃。相同的反逻辑规则为：

```
[root@serverA]# iptables -A INPUT !f -j ACCEPT
```

- `-PKTS BYTES` 允许在链上插入、追加或替换规则时设置计数器。计数器分别对应通过规则的数据包和字节数。对于大多数管理员来说，这种需求很少见。其用法的示例是：

```
[root@serverA]# iptables -I FORWARD -f -j ACCEPT -c 10
```

在此示例中，允许分片的规则规则被插入到 `FORWARD` 链，且计数器设置为 10 个包和 10 字节。

- `-v` 此选项显示 `iptables` 输出的额外数据（通常与 `-L` 选项结合），例如：

```
[root@serverA]# iptables -L -v
```

- `-n` 此选项以数字形式显示任何主机名或端口名。通常 `iptables` 会为你进行域名系统（DNS）解析，显示主机名而不是 IP 地址，显示协议名（如 `SMTP`）而不是端口号（`25`）。如果你的 DNS 系统宕机，或者你不想产生额外的流量，这是一个非常有用的选项。示例为：

```
[root@serverA]# iptables -L -n
```

- `-x` 此选项将显示计数器的精确值。`iptables` 会尝试以“人类友好”的术语打印值，从而进行舍入处理。例如，与其显示“10k”，`iptables` 将显示“10310（此处原文为 10310）”。

- `-line-numbers` 此选项将在链中的每个规则旁边显示行号。当你需要在链中间插入规则并需要规则及其对应的快速列表时非常有用。示例为：

```
[root@serverA]# iptables -L --line-numbers
```

对于 IPv6 防火墙规则，使用：

```
[root@serverA]# ip6tables -L --line-numbers
```

# Match 规则扩展

Netfilter 最强大的方面之一是它提供了一种“可插拔”的设计。对于开发者来说，这意味着可以使用应用程序编程接口（API）对 Netfilter 进行扩展，而不是深入内核代码进行硬改。对于 Netfilter 用户来说，这意味着除了基本功能外还有许多扩展。

这些扩展通过 `iptables` 命令行中的 Match 功能实现。通过在 `-m` 参数后指定模块名，`iptables` 将负责加载必要的模块并提供规则集。在本节中，我们将讨论其中一些扩展，截至本文为止，它们经过了充分测试，通常包含在 Linux 发行版中。

> **提示** 获取匹配扩展的帮助，只需在 `-m` 参数后指定扩展名称。例如，要获取 ICMP 模块的帮助，使用：

```
[root@serverA ~]# iptables -m icmp
```

`icmp` 此模块为 ICMP 协议提供额外的匹配参数：

```
icmp-type [!]typename
```

其中 `typename` 是 ICMP 类型的名称或数字。例如，要阻止 ping 包，请使用：

```
[root@serverA]# iptables -t filter -p icmp -A INPUT -m icmp --icmp-type echo-request
```

支持 ICMP 数据包类型的完整列表，请查看带有 `-h` 选项的页面。

`limit` 此模块提供限制包速率的方法。它将匹配数据包速率低于限制。次要“burst”选项匹配流量的瞬时高峰，但如果高峰持续，将停止匹配。参数为：

- `limit rate`
- `limit-burst rate`

`rate` 是持续的每秒包计数。`number` 指定在突发情况下接受多少个连续包。`number` 的默认值为 5。你可以使用此功能作为放缓 SYN 水的简单方法：

```
[root@serverA]# iptables -N syn-flood
[root@serverA]# iptables -A INPUT -p tcp --syn -j syn-flood
[root@serverA]# iptables -A syn-flood -m limit --limit 1/s -j RETURN
[root@serverA]# iptables -A syn-flood -j DROP
```

这将连接速率限制为每秒平均一个，爆发最多五个连接。这并不完美，这种方法 SYN 洪水仍然丢弃合法用户；但它可以帮助防止服务器失控。

`state` 此模块允许你通过 `conntrack` 模块的视角判断 TCP 连接的状态。它提供了一个额外的选项：

```
state state
```

其中 `state` 是 `INVALID`、`ESTABLISHED`、`NEW` 或 `RELATED`。如果问题数据包无法与现有流关联，则状态为 `INVALID`。如果数据包是某个

# 第13 章：Linux 防火墙

对于现有连接，状态为 `ESTABLISHED`（已建立）。如果数据包启动了一个新流，它被视为 `NEW`（新建）。最后，如果数据包与现有连接（例如 FTP 数据传输）相关，则它是 `RELATED`（相关）。

使用此功能来确保新连接仅设置了 TCP SYN 位，我们执行以下操作：

```
[root@serverA ~]# iptables -A INPUT -p tcp ! -m state --state NEW -j DROP
```
