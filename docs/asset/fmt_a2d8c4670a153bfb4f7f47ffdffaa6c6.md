
在此示例中，任何来自 `eth0` 并并发往 `eth1` 的包都会被接受。

`-f` 此选项指定数据包是否为 IP 分片。感叹号会反转此规则。例如：

```
[root@serverA ~]# iptables -A INPUT -f -j DROP
```

在此示例中，任何进入 `INPUT` 链的 IP 分片都会被自动丢弃。具有否定逻辑的相同规则为：

```
[root@serverA ~]# iptables -A INPUT ! -f -j ACCEPT
```

`-PKTS BYTES` 此选项允许你在向链中插入、追加或替换规则时设置特定规则的计数器值。计数器分别对应通过该规则的数据包数和字节数。对于大多数管理员来说，这是一个罕见事件。用法示例：

```
[root@serverA ~]# iptables -t filter -A FORWARD -c 10
```

在此示例中，任何进入 `INPUT` 链的 IP 分片都会被自动丢弃。具有否定逻辑的相同规则为：

```
[root@serverA ~]# iptables -A INPUT ! -f -j ACCEPT
```

# Linux 管理：入门指南

`-v` 此选项允许输出显示更多信息。
`-n` 此选项允许输出显示数字地址。
`-x` 此选项允许输出额外的标志位。
`--line-numbers` 此选项允许输出显示规则的行号。

## 使用 Match 进行规则扩展

Netfilter 最强大的方面之一是它提供了可插即的设计。对于开发者来说，这意味着一个扩展功能的应用程序接口 `API`。在本节中，我们将讨论一些扩展，截至本文，这些扩展已经过充分测试，并通常包含在 Linux 发行版中。

> 提示：要获取匹配项的帮助，只需在 `-m` 参数后指定扩展名称。例如，要获取 `ICMP` 模块的帮助，请使用：

```
[root@serverA ~]# iptables -m icmp
```

`icmp` 模块为 `ICMP` 协议提供了一个额外的匹配参数：

`icmp-type [!]typename`

其中 `typename` 是 `ICMP` 消息类型的名称或数字。例如，要阻止 `ping` 包，使用以下命令：

```
[root@serverA ~]# iptables -t filter -p icmp -A INPUT -m icmp --icmp-type echo-request
```

要查看完整的 `ICMP` 类型列表，请查看带 `-h` 的模块页面。

`limit` 此模块提供了一种限制包速率的方法。当数据包速率低于限制时，它将匹配。次要的“爆发”选项匹配瞬时流量激增，但如果激增持续将停止匹配。参数为：

- `limit rate`
- `limit-burst rate`

`rate` 是持续的每秒包数。第二个参数中的数字指定了在激增时允许连续包的数量。`number` 的默认值为 `5`。你可以使用此功能作为减缓 `SYN floods` 水的简单方法：

```
[root@serverA ~]# iptables -N syn_flood
[root@serverA ~]# iptables -A INPUT -p tcp --syn -j syn_flood
[root@serverA ~]# iptables -A syn_flood -m limit --limit 1/s -j RETURN
[root@serverA ~]# iptables -A syn_flood -j DROP
```

这将连接速率限制为平均每秒一次，最多允许五个并发连接。这种方法并不完美，通过这种方法 `SYN` 洪水仍然可能拒绝合法用户；但它将帮助你的服务器不失控。

`state` 此模块允许你通过连接跟踪 `conntrack` 模块的视角确定 `TCP` 连接的状态。它提供了一个额外的选项：

```
state state
```

其中 `state` 是 `INVALID`、`ESTABLISHED`、`NEW` 或 `RELATED` 之一。如果问题数据包无法与现有流关联，则状态为 `INVALID`。如果该数据包是部分的

# 第 13 章：Linux 防火墙

现有连接，状态为 `ESTABLISHED`（已建立）。如果数据包启动一个新的流，则被视为 `NEW`（新建）。最后，如果数据包与现有连接关联（例如 `FTP` 数据传输），则它属于 `RELATED`（相关）。

使用此功能确保新连接仅设置了 `TCP SYN` 位，我们执行：

```
[root@serverA ~]# iptables -A INPUT -p tcp --syn -m state --state NEW -j DROP
```

通过阅读此命令，我们看到对于 `INPUT` 链上 `TCP` 协议、未设置 `SYN` 标志且连接状态为 `NEW` 的数据包，我们将丢弃该数据包。
记住，合法的 `TCP` 连接必须以一个带有 `SYN` 位设置的数据包开始。

`tcp` 模块允许我们检查 `TCP` 数据包的多个方面。我们已经见过其中的一些选项（如 `--syn`）。以下是完整的选项列表：

- `source-port [!] port: [port]` 此选项检查 `TCP` 数据包的源端口。如果指定冒号后跟第二个数字，则检查端口范围。例如，“6000:6010”表示“包含 6000 到 6010 之间的所有端口”。感叹号反转此设置。
`--source-port ! 25` 意味着“所有不是 25 的端口”。该选项的别名为 `--port`。

- `destination-port [!] port: [port]` 与 `--source-port` 选项类似，它检查 `TCP` 数据包的目标端口。支持端口范围和表示法。例如，`--destination-port ! 9000:9010` 表示“所有不在 9000 到 9010 之间的所有端口”。该选项的别名为 `--dport`。

- `tcp-flags [!] mask comp` 此选项检查数据包中是否设置了 `TCP` 标志。`mask`（掩码）告诉选项要检查哪些标志，`comp`（比较）决定哪些标志必须被设置。`mask` 和 `comp` 都可以是逗号分隔的标志列表。有效的标志有 `SYN`, `ACK`, `FIN`, `RST`, `URG`, `PSH`, `ALL` 和 `NONE`，其中 `ALL` 表示所有标志，`NONE` 表示无标志。感叹号反转该设置。例如，使用 `--tcp-flags ALL SYN,ACK` 意味着该选项应检查所有标志，且 `SYN` 和 `ACK` 标志必须被设置。

- `[!] --syn` 检查 `SYN` 标志是否启用。它在逻辑上等同于 `--tcp-flags SYN,RST,ACK SYN`。感叹号反转该设置。
使用此模块的一个示例是检查到端口 53 的连接是否没有设置 `SYN` 位且设置了 `URG` 位，在这种情况下它将被丢弃。注意，当请求大于 512 字节时，`DNS` 会切换到 `TCP`。

```
[root@serverA ~]# iptables -A INPUT -p tcp --port 53 --tcp-flags ! URG -j DROP
```

# Linux 管理：入门指南

`mss` 此选项匹配具有特定最大分段大小 `MSS` 的 `TCP` 数据包。`IP` 的理想限制是 576，最大值为 1500。为连接设置 `MSS` 值的目标是避免两个端点之间的数据分段。拨号连接需要使用 576 字节的 `MSS`，而来自高速链路的用户需要使用 1500 字节的值。此内容的命令行选项是：

```
mss:[value]
```

其中 `value` 是要比较的 `MSS` 值。如果冒号后提供了第二个值，则检查整个范围。例如：

```
[root@serverA ~]# iptables -I INPUT -p tcp -m mss 576 -j ACCEPT
[root@serverA ~]# iptables -I INPUT -p tcp -m mss ! 576 -j ACCEPT
```

这将提供一种简单的方法来统计有多少来自 576 字节 `MSS` 连接的数据包。要查看计数器的状态，使用 `iptables -L -v`。

`udp` 与 `TCP` 模块类似，`UDP` 提供了额外的参数来检查数据包。提供了两个参数：

- `source-port [!] port:[port]` 此选项检查用户数据报协议 `UDP` 数据包的源端口。如果端口后面跟着另一个数字，则检查两者之间的范围。如果使用感叹号，逻辑则反转。

- `destination-port [!] port:[port]` 与 `source-port` 选项类似，此选项检查 `UDP` 目标端口。

例如：

```
[root@serverA ~]# iptables -I INPUT -p udp --destination-port 53 -j ACCEPT
```
