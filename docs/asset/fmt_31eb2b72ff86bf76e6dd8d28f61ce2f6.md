
`iptables -L -n`

Chain input (ACCEPT):

Chain forward (ACCEPT):

Chain output (ACCEPT):

```
要向链中添加新规则，使用 `-A`。使用 `-D` 移除，使用 `-R` 替换。在命令之后，列出规则适用的链，例如 `INPUT`、`OUTPUT` 或 `FORWARD` 链，或者用户定义的链。接下来，你列出指定你所采取操作的不同选项（大部分与 `iptables` 使用的相同，有少数例外）。`-s` 选项指定附加数据包上的源地址，`-d` 指定目的地址，`-j` 选项指定规则的目标。`ACCEPT` 目标将允许数据包通过。`-i` 选项现在指示输入设备，且只能用于 `INPUT` 和 `FORWARD` 链。`-o` 选项指示输出设备，只能用于 `OUTPUT` 和 `FORWARD` 链。列出几个基本选项。

| Option | 功能 |
| --- | --- |
| -A chain | 在链末尾追加规则。 |
| -D chain [ruleenum] | 从链中删除匹配的规则。从链中删除 `ruleenum`（1 = 第一条）。 |
| -I chain [ruleenum] | 在链中作为 `ruleenum` 插入规则（默认 1 = 第一条）。 |
| -R chain ruleenum | 替换链中的 `ruleenum`（1 = 第一条）。 |
| -L [chain] | 列出链或所有链中的规则。 |
| -E [chain] | 重命名链。 |
| -F [chain] | 删除（清空）链或所有链中的所有规则。 |
| -R chain | 替换规则；规则从 1 开始编号。 |
| -Z [chain] | 链或所有链中的计数器零。 |
| -N chain | 创建新的用户定义的链。 |
| -X chain | 删除用户定义的链。 |
| -P chain target | 更改链目标的策略。 |

**表 19-4 iptables 命令**

### iptables 选项

`iptables` 包被设计为可扩展的，有许多带有筛选标准的选项可以包含在 `iptables` 中。例如，TCP 扩展包含了 `--syn` 选项，用于检查 SYN 数据包。ICMP 扩展提供了 `--icmp-type` 选项，用于指定 ping 操作中使用的 ICMP 数据包。limit 扩展包含了 `--limit` 选项，通过你可以限制指定时间段（如一秒）内匹配数据包的最大数量。

| Option | 功能 |
| --- | --- |
| -p [!] proto | 指定协议，例如 TCP、UDP、ICMP 或 ALL。 |
| -s [!] address[/mask] [!] [port:] | 源地址和端口。 |
| -d [!] address[/mask] [!] [port:] | 目的地址和端口。 |
| -i [!] interface | 输入设备。 |
| -o [!] interface | 输出设备。 |
| --syn | 检查 SYN 数据包。 |
| --icmp-type | 指定 ICMP 类型。 |
| --limit | 在时间段内限制匹配的数据包。 |

# 334 第四部分：安全

例如，网络 192.168.0/ 下的所有地址都可以被表示为 192.168.0.0/255.255.255.0 或 192.168.0.0/24。要指定任何地址，你可以使用 0.0.0.0/0 或直接使用 0/0。默认情况下，如果没有使用 `-s` 或 `-d` 指定，规则将引用任何地址。接下来的示例接受来自（源自）192.168.0.0 网络中任何主机、且发往（目的为）未留空 `-d` 选项或写为 `-d 0/0` 的任何地方的消息包：

```
iptables -A INPUT -s 192.168.0/24 -j ACCEPT
```

`iptables` 规则通常应用于单个网络接口，例如用于连接到 Internet 的以太网接口。对于一个连接到 Internet 的单一系统，你有两个接口：一个是用于 Internet 连接的接口，另一个是用于系统用户之间内部连接的本地回环接口 `lo`。Internet 网络接口使用设备名称 `eth0` 进行引用。例如，设备名称为 `/dev/eth0` 的以太网卡将通过名称 `eth0` 被引用。使用 PPP 协议且设备名称为 `/dev/ppp0` 的现代设备将名为 `ppp0`。在 `iptables` 规则中，你使用 `-i` 选项来指定输入设备；它只能与 `INPUT` 和 `FORWARD` 链配合使用。规则可以应用于在特定网络设备上到达和离开的数据包。在下面的示例中，第一条规则引用以太网 `eth0`，第二条引用本地回环：

```
iptables -A INPUT -j DROP -i eth0 -s 192.168.0.45
iptables -A INPUT -j ACCEPT -i lo
```

### 用户定义链 (User-Defined Chains)

在 `iptables` 中，`FORWARD` 和 `INPUT` 链是分开评估的。它们互不影响。这意味着如果你想完全阻止地址通过你的系统，你需要为它们同时添加一个 `FORWARD` 规则和一个 `INPUT` 规则。

```
iptables -A INPUT -j DROP -i eth0 -s 192.168.0.45
iptables -A FORWARD -j DROP -i eth0 -s 192.168.0.45
```

重复 `INPUT` 和 `FORWARD` 规则的一种常用方法是创建一个用户链，用于定义 `INPUT` 和 `FORWARD` 链的输入。你使用 `-N` 选项定义一个用户链。接下来的示例显示了这种安排的基本格式。创建了一个名为 `incoming` 的新链，而你的 `FORWARD` 和 `INPUT` 链现在被定义为指向 `incoming` 链。`INPUT` 和 `FORWARD` 链随后将 `incoming` 链作为目标，直接跳转到那里，并使用它的规则处理它们接收到的任何数据包。

```
iptables -N incoming
iptables -A incoming -j DROP -i eth0 -s 192.168.0.45
iptables -A incoming -j ACCEPT -i lo
iptables -A FORWARD -j incoming
iptables -A INPUT -j incoming
```

## 第 19 章：网络防火墙：Netfilter 335

### ICMP 包

防火墙经常拦截 Internet 控制消息协议 `ICMP` 消息。特别是 ICMP 重定向消息，可能会接管你的路由表。然而，你需要启用某些 ICMP 消息，例如 ping、traceroute 特别是目的不可达 `destination-unreachable` 操作所需的消息。在大多数情况下，你总是需要确保允许目的不可达的数据包；否则名称查询将挂起。一些常见的 ICMP 包类型列如表 19-6 所示。你可以使用 `--icmp-type` 选项启用某种 ICMP 类型的数据包，其参数是代表消息的名称或数字。接下来的示例使用了类型 `echo-reply`、`echo-request` 和 `destination-unreachable` 的消息，它们的数字分别为 0、8 和 3。

```
iptables -A INPUT -ACCEPT -p icmp -i eth0 --icmp-type echo-reply -d 10.0.0.1
iptables -A INPUT -ACCEPT -p icmp -i eth0 --icmp-type echo-request -d 10.0.0.1
iptables -A INPUT -ACCEPT -p icmp -i eth0 --icmp-type destination-unreachable -d 10.0.0.1
```

它们的规则看起来如下：

```
ACCEPT icmp --0.0.0.0/0 10.0.0.1 icmp type 0
ACCEPT icmp --0.0.0.0/0 10.0.0.1 icmp type 8
ACCEPT icmp --0.0.0.0/0 10.0.0.1 icmp type 3
```

需要控制 ping 操作以避免“死亡 ping” `ping-of-death` 安全威胁。你可以通过几种方法实现。一种方法是拒绝任何 ping 分片。Ping 包通常很小。你可以使用 `-f` 选项通过拒绝任何是分片的 ICMP 包来阻止死亡 ping 攻击。

```
iptables -A INPUT -p icmp -j DROP -f
```
