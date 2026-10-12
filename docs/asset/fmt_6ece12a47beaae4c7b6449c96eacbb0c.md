
`Iptables` 提供的 `ToS` 数值如下所示：

`ToS` 可以以十进制数、十六进制数或（在某些情况下）作为名称给出。

在这种情况下，通过允许服务向正确的地址发送包，这种类型的攻击可以被防止：

```
iptables -A OUTPUT -p tcp -m ttl 1 -j
iptables -A OUTPUT -p tcp -m tos 0x2 -j
```

在使用这些功能时，这可能很棘手，因为 `TTL` 在通过路由器时会减少。例如：

```
iptables -A OUTPUT -p tcp -m ttl 1 -j
iptables -A OUTPUT -p tcp -m tos 0x2 -j
```

### `--ttl <number>`

数据包的生存时间（`TTL`）定义了数据包可以通过的路由器数量。由于不同的操作系统使用不同的值，这可以识别操作系统。例如，`Linux` 通常使用 64，而 `Windows` 通常使用 128。然而，这可能很棘手，因为 `TTL` 在通过路由器时会减少。

许多操作系统使用的 `TTL` 低于 64。对于源自局域网（`LAN`）的流量，该选项的用处非常有限。例如：

```
iptables -A OUTPUT -p tcp -m ttl 1 -j
iptables -A OUTPUT -p tcp -m tos 0x2 -j
```

许多远程漏洞利用缓冲区溢出在高位端口（受攻击守护的 `UID`）上启动 `shell`。通过只允许服务向正确的地址发送包（例如，`HTTP` 的 80 和 443），这种类型的攻击可以被防止。

这些匹配准则的示例如下：

```
iptables -A OUTPUT -m owner --uid-owner 0 -j
iptables -A OUTPUT -m owner --gid-owner 0 -j
iptables -A OUTPUT -m owner --pid-owner 2425 -j
iptables -A OUTPUT -m owner --sid-owner 2400 -j
```

要使用 `PID` 和 `SID` 匹配功能，用于加载防火墙的脚本可能包含从进程列表中提取特定进程 `PID` 的命令（许多服务会将 `PID` 写入 `/var/run` 目录的文件并在后续规则中使用该值）。记住，如果进程重启（在崩溃时可能会发生），`PID` 将不同，规则将不再生效。

此扩展允许你匹配源地址和目的端口。

### `mac -mac-source <mac address>`

此扩展用于匹配数据包的 `MAC` 地址。因此，它仅适用于 `802.x` 网络（如以太网、调制解调器、`WiFi` 和蓝牙），并且只能用于 `INPUT`、`FORWARD` 和 `PREROUTING` 链：

```
iptables -A INPUT -m mac --mac-source 00:02:A5:70:29 -j ACCEPT
```

### `mark --mark <number>`

`mark` 扩展允许你匹配之前使用 `MARK` 目标标记的数据包。请注意，这些标记由 `Iptables` 创建并维护，并且不会以任何方式更改数据包。

```
iptables -A INPUT -m mark --mark 1 -j LOG
```

### `state --state <options>`

`Iptables` 状态机在第 2 章查看连接跟踪和 `NAT` 时已经涵盖过。当使用连接跟踪时，连接入站和出站数据都存储在内存中（可以通过 `/proc/net/ip_conntrack` 查看），以及它们当前处于的状态：`NEW`（新建）、`ESTABLISHED`（已建立）、`RELATED`（相关）或 `INVALID`（无效）。此扩展允许你匹配这四个状态中的任何一种。例如：

```
iptables -A INPUT -m state --state INVALID -j LOG
```

### `-m limit --limit <rate> [--limit-burst <number>]`

限制规则用于根据数据包发送或接收的速率来匹配数据包。例如：

```
iptables -A INPUT -p icmp -m limit --limit 3/second -j ACCEPT
```

该规则匹配任意秒内接收的前三个 `ICMP` 消息（在此例中将接受它们）；该秒内随后的 `ICMP` 数据包不会被匹配，并将继续由链的其余部分处理。有效的单位有秒、分钟、小时和天；但请注意，以下示例与之前的规则不同：

```
iptables -A INPUT -p icmp -m limit --limit 180/minute -j ACCEPT
```

在这里我们匹配 1 分钟内接收的前 180 个 `ICMP` 消息。这与说 3/s（那是 180/min 的平均值）大不同：在 3 秒内可能会接收到 179 个 `ICMP` 数据包，在 50 秒后又接收一个，而它们仍然会匹配此规则。

限制速率也可以使用感叹号进行反转：

```
iptables -A INPUT -p icmp -m limit --limit 3/second -j LOG
```

这会导致仅在速率超过限制后才进行速率匹配。在示例中，如果我们在 1 秒内接收了三个 `ICMP`，额外的 `ICMP` 将被记录。

速率限制的一个常见用途是在 `DoS` 攻击期间防止日志文件变得过大（这本身也可能导致 `DoS` 攻击）；知道攻击已经发生是有用的，但用成千上万条目（大部分可能来自伪造地址）填充日志文件是没有意义的。

另一个用途（如前面的示例所示）是限制接受或发送出 `ICMP` 消息的速率。这允许你使用 `ICMP`，但防止了攻击者利用它们进行 `DoS` 攻击。

`--limit-burst` 选项提供了更精细的控制，允许你指定要匹配的初始数据包的最大数量。每当未达到速率限制时，该限制就会增加 1，直到达到 `--limit-burst` 指定的最大值；例如：

```
iptables -A INPUT -p icmp -m limit 10/second
--limit-burst 30/m
```

## 目标 (Targets)

目标（`Targets`）规定了规则匹配时要采取的操作。可以使用 15 个内置目标（`built-targets`），或者目标可以指定一个用户定义的链，执行流将传递到该链。在后一种情况下，如果用户定义的链中没有匹配的规则，执行流将传回调用链。

`-j` 选项用于命名目标，对于内置目标，它们全是大写字母。这些目标在随后的章节中进行了描述。

### `ACCEPT (-j ACCEPT)`

这会导致数据包被接受。在此链中不会对该数据包进行进一步处理，尽管如果数据包通过了其他链，则可能会进行处理。

### `DROP (-j DROP)`

在此目标中，数据包被丢弃，且不再发生进一步处理——无论是当前链还是数据包本应通过的其他链。如第 2 章所述（当我们比较 `DROP` 和 `REJECT` 的区别时），不会向数据包的发送者发送任何已丢弃的消息。

### `REJECT (-j REJECT)`

数据包应该被丢弃，并向发送者发送错误消息。默认情况下，会发送一个 `ICMP` 端口不可达（`port unreachable`）消息。可以通过 `--reject-with` 调整此行为：

```
iptables -A INPUT -p icmp -m limit --limit 180/minute -j ACCEPT
```

有效的参数包括：

- `icmp-unreachable`
- `icmp-prohibited`
- `host-unreachable`
- `host-prohibited`
- `net-unreachable`
- `net-prohibited`
- `tcp-rst`
- `tcp-prohibited`
