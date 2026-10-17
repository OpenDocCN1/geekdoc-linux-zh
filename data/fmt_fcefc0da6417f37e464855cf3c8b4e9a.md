
阅读这个示例，我们看到对于 `INPUT` 链上的 `TCP` 数据包，如果它没有设置 `SYN` 标志，且连接状态为 `NEW`，我们就会丢弃该数据包。（记住，合法的新 `TCP` 连接是以一个设置了 `SYN` 位的数据包开始的。）

`tcp` 模块允许你检查 `TCP` 数据包的多个方面。我们已经见过其中一些选项（例如 `--syn`）。以下是选项列表：

### `--source-port` [1] port: [port]
此选项检查 `TCP` 数据包的源端口。如果指定了冒号后跟第二个数字，则会检查端口范围。例如，`6000:6010` 意味着“6000 到 6010 之间的所有端口”。感叹号表示否定此设置。例如，`--source-port ! 25` 意味着“所有不是 25 的源端口”。该选项的别名是 `--sport`。

### Linux 管理：初学者指南

### `--destination-port` [1]
与 `--source-port` 选项类似，它检查 `TCP` 数据包的目的端口。支持端口范围和否定。例如，`--destination-port ! 9000:9010` 意味着“所有不在 9000 到 9010 之间的端口”。它的别名是 `--dport`。

### `--tcp-flags mask comp`
此项检查数据包中设置的 `TCP` 标志。`mask` 告诉选项要检查哪些标志标志位，而 `comp` 参数告诉选项哪些标志必须被设置。有效的标志有 `SYN`, `ACK`, `FIN`, `RST`, `URG`, `PSH`, `ALL` 和 `NONE`，其中 `ALL` 表示所有标志，`NONE` 表示其中一个都不设置。感叹号设置否定。例如，使用 `--tcp-flags ALL SYN, ACK` 意味着该选项应该检查所有标志，并且必须设置 `SYN` 和 `ACK` 标志。

### `--syn`
这表示 `SYN` 标志是否启用。它在逻辑上等同于 `--tcp-flags SYN, RST, ACK SYN`。感叹号设置否定。

使用此模块的一个示例检查到 `DNS` 端口 `53` 的连接是否源自端口 `53`，没有设置 `SYN` 位但设置了 `URG` 位，如果是，它将被丢弃。注意，当请求大于 512 字节时，`DNS` 将自动切换到 `TCP`。

```
[root@server ~#] iptables -A INPUT -p tcp --port 53 \
--dport 53 ! --tcp-flags SYN URG -j MSS
```

`tcpmss` 检查具有特定最大段大小 (`MSS`) 的 `TCP` 数据包。`IP` 的最低限制为 576，最高值为 1500。为连接设置 `MSS` 值的目标是避免两个端点之间的数据包分段。拨号连接倾向于使用 576 字节的 `MSS` 设置，而来自高速链路的用户倾向于使用 1500 字节的值。以下是该设置的命令行选项：

`mss value: [value]`

在这里，`value` 是要比较的 `MSS` 值。冒号后跟第二个值会被检查，即检查整个范围。这里有一个示例：

```
[root@server ~#] iptables -I INPUT -p tcp -m tcpmss --mss 576 -j ACCEPT
[root@server ~#] iptables -I INPUT -p tcp -m tcpmss ! --mss 576 -j ACCEPT
```

这将提供一种简单的方法来计算来自具有 576 字节 `MSS` 的连接连接的数据包数量（以及字节数）。要查看计数器的状态，使用 `iptables -L -v`。

`udp` 与 `TCP` 模块一样，`UDP` 模块提供了额外的参数来检查数据包。

- `--source-port` [1] port: [port] 此选项检查用户数据报协议 (`UDP`) 数据包的源端口。
- `--destination-port` [1] 对于 `--source-port` 选项，它检查 `TCP` 数据包的目的端口。支持端口范围和否定。例如，`--destination-port ! 9000:9010` 意味着“所有不在 9000 到 9010 之间的端口”。它的别名是 `--dport`。

```
[root@server ~#] iptables -A INPUT -p tcp --destination-port 53 -j ACCEPT
```

这将提供一种简单的方法来计算来自具有 576 字节 `MSS` 的连接的数据包数量（以及字节数）。要查看计数器的状态，使用 `iptables -L -v`。

`udp-udp` 与 `TCP` 模块一样，`UDP` 模块提供了额外的参数来检查数据包。

- `--source-port` [1] port: [port] 此选项检查用户数据报协议 (`UDP`) 数据包的源端口。
- `--destination-port` [1] 对于 `--source-port` 选项，它检查 `TCP` 数据包的目的端口。支持端口范围和否定。例如，`--destination-port ! 9000:9010` 意味着“所有不在 9000 到 9010 之间的端口”。它的别名是 `--dport`。

```
[root@server ~#] iptables -A INPUT -p tcp --destination-port 53 -j ACCEPT
```

这将提供一种简单的方法来计算来自具有 576 字节 `MSS` 的连接的数据包数量（以及字节数）。要查看计数器的状态，使用 `iptables -L -v`。

## 第13 章：Linux 防火墙 (Netfilter) 353

`(eth1)` 和互联网 `(eth0)`。请注意，我们所说的“服务器”是指任何需要连接到它的设备。例如，这可能意味着运行 `ssh` 守护进程的 Linux 系统，或者运行 Web 服务器的 Windows 系统。

让我们先从没有服务器需要支持的情况开始。

首先，我们需要确保 `NAT` 模块已加载，并且 `NAT` 的 `FTP` 支持也已加载。我们通过 `modprobe` 命令来实现这一点：

```
[root@server ~ -# modprobe iptables_nat
[root@server ~ -# modprobe ip_nat_ftp
```

在加载了必要的模块后，我们为所有链（`chains`）定义默认策略。对于 `filter` 表中的 `INPUT`、`FORWARD` 和 `OUTPUT` 链，我们将目标目标分别设置为 `DROP`、`DROP` 和 `ACCEPT`。对于 `POSTROUTING` 和 `PREROUTING` 链，我们将它们的默认策略设置为 `ACCEPT`。这是 `NAT` 正常运行的必要条件。

```
[root@server ~ -# iptables -P INPUT DROP
[root@server ~ -# iptables -P FORWARD DROP
[root@server ~ -# iptables -P OUTPUT ACCEPT
[root@server ~ -# iptables -t nat -P POSTROUTING ACCEPT
[root@server ~ -# iptables -t nat -P PREROUTING ACCEPT
```

设置好默认策略后，我们需要定义防火墙规则。允许内网 `(eth1)` 的用户连接到互联网，但不允许互联网反向连接。为了实现这一点，我们定义了一个名为“`block`”的新链，用于将我们的状态跟踪规则分组在一起。该链中的第一条规则简单地规定：任何属于已建立连接或与已建立连接的数据包都是允许的。第二条规则规定，数据包要创建一个新连接，其源不能来自 `eth0`（面向互联网的接口）。如果数据包不符合上述两条规则之一，防火墙将强制丢弃该包。

```
[root@server ~ -# iptables -A block
[root@server ~ -# iptables -A block -m state \
    -- ESTABLISHED, RELATED -j ACCEPT
[root@server ~ -# iptables -A block -m state \
    -- NEW ! -i eth0 -j ACCEPT
[root@server ~ -# iptables -A block -j DROP
```

设置好阻断链后，我们需要在 `INPUT` 和 `FORWARD` 链中调用它。我们不需要担心 `OUTPUT` 链，因为那里产生的数据包只源自防火墙本身。相反，`INPUT` 和 `FORWARD` 链需要进行检查。记住，在进行 `NAT` 时，`INPUT` 链不会被触发，因此我们需要对 `FORWARD` 进行检查。如果数据包的目标是防火墙本身，我们需要从 `INPUT` 链处理。

```
[root@server ~]# iptables -A INPUT -j block
[root@server ~]# iptables -A FORWARD -j block
```

最后，当数据包离开系统时，我们在 `NAT` 表的 `POSTROUTING` 链中执行 `MASQUERADE` 转换。所有离开 `eth0` 接口的数据包都会通过这条链。
