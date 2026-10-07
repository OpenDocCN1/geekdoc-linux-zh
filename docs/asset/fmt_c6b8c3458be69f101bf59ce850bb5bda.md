
> 提示：可以通过 `netfilter` 网站提供的内核补丁添加特殊的目标和选项。例如，`SAME` 补丁为所有连接返回相同的地址。`netfilter` `make` 的 `patch-o-matic` 选项可以补丁你的内核源代码，添加对新目标和选项的支持。然后你可以重新编译并安装内核。

### 防火墙和 NAT 链 (Firewall and NAT Chains)

内核使用三个链：`INPUT`、`OUTPUT` 和 `FORWARD`。当通过接口接收数据包时，使用 `INPUT` 链来确定如何处理它。内核随后使用其路由信息决定将其发送到哪里。如果内核将数据包发送到另一个主机，则检查 `FORWARD` 链。在数据包实际发送之前，还会检查 `OUTPUT` 链。此外，还实现了两个 NAT 链 `POSTROUT` 和 `PREROUTING`，用于处理伪装和数据包地址修改。`mangle` 表有其自己的 `POSTROUT`、`PREROUTING`、`INPUT` 和 `FORWARD` 版本，可以修改数据包。内置的 `netfilter` 链列表 20-4。

| 链 (Chain) | 说明 (Description) |
|---|---|
| `INPUT` | 入站数据包的规则 |
| `OUTPUT` | 出站数据包的规则 |
| `FORWARD` | 转发数据包的规则 |
| `PREROUTING` | 重定向或修改传入数据包的规则，仅限 NAT 和 mangle 表 |
| `POSTROUTING` | 重定向或修改传出数据包的规则，仅限 NAT 和 mangle 表 |

表 20-4 Netfilter 内置链

## 添加和修改规则 (Adding and Changing Rules)

你使用 `iptables` 命令添加和修改链规则，该命令由 `iptables` 命令本身以及一个表示要执行命令的参数组成。例如，`iptables -A` 添加新规则，而 `iptables -D` 删除规则。`iptables -I` 在链的开头插入规则。`iptables -R` 替换规则。`iptables -L` 列出规则。`iptables -F` 清空规则。`iptables -N` 创建一个新的用户定义链。`iptables -X` 删除用户定义链。`iptables -P` 修改链的策略。`iptables -Z` 计数清零。

```
iptables -L -n
Chain (input):
Chain (output):
Chain (forward):
```

使用 `-A` 添加规则。使用 `-D` 删除规则。使用 `-I` 在链开头插入规则。使用 `-R` 替换规则。使用 `-L` 列出规则。使用 `-F` 清空规则。使用 `-N` 创建用户定义链。使用 `-X` 删除用户定义链。使用 `-P` 修改策略。使用 `-Z` 清零。使用 `-t` 指定使用的表。

| 选项 (Option) | 功能 (Function) |
|---|---|
| `-A` | 在链末尾添加规则 |
| `-D` | 删除规则 |
| `-I` | 插入规则 |
| `-R` | 替换规则 |
| `-L` | 列出规则 |
| `-F` | 清空规则 |
| `-N` | 创建一个新的用户定义链 |
| `-X` | 删除用户定义链 |
| `-P` | 修改链的策略 |
| `-Z` | 计数清零 |
| `-t` | 指定使用的表 |

## 第20章：防火墙 468

| 选项 (Option) | 功能 (Function) |
|---|---|
| `-p` | 指定协议，如 TCP、UDP、ICMP 或 ALL |
| `-s` | 指定匹配的源地址 |
| `-d` | 指定匹配的目的地址 |
| `-i` | 指定输入接口 |
| `-o` | 指定输出接口 |
| `-j` | 指定规则的目标 |
| `-m` | 指定要使用的模块 |
| `--state` | 指定状态模块的选项 |
| `--syn` | SYN 数据包，新连接 |
| `--tcp-flags` | TCP 标志 |
| `--limit` | 用于控制匹配的速率 |
| `--limit-burst` | 指定在限制生效前的最大突发数 |

表 20-6 iptables 选项

## iptables 选项

`iptables` 软件包设计为可扩展，`iptables` 中可以包含许多具有选择标准的则的选项。例如，TCP 扩展包含了 `--syn` 选项，用于检查 SYN 数据包。ICMP 扩展提供了 `--icmp-type` 选项，用于指定在 ping 操作中使用的 ICMP 数据包。`limit` 扩展包含了 `--limit` 选项，你可以通过该选项限制在指定时间段（如一秒）内匹配的数据包的最大数量。

在下面的示例中，用户向 `INPUT` 链添加了一条规则，以接受所有源自地址 `192.168.0.55` 的数据包。任何接收（`INPUT`）源地址 (`-s`) 为 `192.168.0.55` 的数据包都将被接受并通过 (`-j ACCEPT`)：

```
iptables -A INPUT -s 192.168.0.55 -j ACCEPT
```

### 接受和拒绝数据包：DROP 和 ACCEPT

使用了两个内置目标：`DROP` 和 `ACCEPT`。其他目标可以是用户定义的链或添加的扩展，例如 `REJECT`。使用了两个特殊目标来管理链：`RETURN` 和 `QUEUE`。`RETURN` 表示链的结束并返回到启动它的链。`QUEUE` 用于将数据包发送到用户空间。

```
iptables -A INPUT -s my.junk.com -j DROP
```

你可以用 `!` 符号将规则转为反规则。例如，要接受除来自特定地址以外的所有数据包，可以在 `-s` 选项和该地址之前添加一个 `!`。下面的示例将接受除 IP 地址 `192.168.0.45` 以外的所有数据包：

```
iptables -A INPUT -j ACCEPT !s 192.168.0.45
```

你可以使用域名或 IP 数字来指定单个地址。对于地址范围，请使用其网络的 IP 数字和网络 IP 掩码。IP 掩码可以是 IP 数字，也可以是组成掩码的位数。例如，网络 `192.168.0` 中的所有地址都可以用 `192.168.0.0/255.255.255.0` 或 `192.168.0.0/24` 表示。要指定任何地址，你可以使用 `0.0.0.0.0/0.0.0.0`。默认情况下，如果没有指定 `-s` 或 `-d`，规则将引用任何地址。下面的示例接受来自整个 `192.168.0` 网络任何地方（源）或去往任何地方（目的）的消息，且完全不去（留空 `-d` 选项或可以写为 `-d 0/0`）：

```
iptables -A INPUT -s 192.168.0.0/24 -j ACCEPT
```

`iptables` 规则通常应用于特定的网络接口，例如用于连接到互联网的以太网接口。对于连接到互联网的单个系统，你将有两个接口：一个是你的互联网连接，另一个是用于系统内用户之间内部连接的环回接口 (`lo`)。互联网网络接口使用接口的设备名称引用。例如，设备名称为 `/dev/eth0/` 的以太网将通过名称 `eth0` 引用。使用 PPP 协议且设备名称为 `/dev/ppp0/` 的调制解调器将通过名称 `ppp0` 引用。在 `iptables` 规则中，使用 `-i` 选项来指示输入设备；它只能用于 `INPUT` 和 `FORWARD` 链。`-o` 选项指示输出设备，只能用于 `OUTPUT` 和 `FORWARD` 链。规则随后可以应用于进入和离开特定网络设备的数据包。在接下来的示例中，第一条规则引用了以太网设备 `eth0`，第二条引用了 `localhost`：

```
iptables -A INPUT -j DROP eth0 -s 192.168.0.45
iptables -A INPUT -j ACCEPT -i lo
```

### 用户自定义链

使用 `iptables` 时，`FORWARD` 和 `INPUT` 链是分别评估的，其中一个不馈给另一个。这意味着，如果你想阻止地址通过你的系统，你需要为它们同时添加一条 `FORWARD` 规则和一条 `INPUT` 规则：

```
iptables -A INPUT -j DROP eth0 -s 192.168.0.45
iptables -A FORWARD -j DROP eth0 -s 192.168.0.45
```

重复 `INPUT` 和 `FORWARD` 规则的常用方法是创建一个用户链，`INPUT` 和 `FORWARD` 链都馈入该链。你使用 `-N` 选项定义用户链。示例显示了这种安排的基本格式。创建了一个名为 `incoming` 的新链（你可以选择任何名称）。你随后为你的 `FORWARD` 和 `INPUT` 链定义的规则将使用 `incoming` 链作为目标，跳转到那里并使用它的规则处理它们收到的所有数据包：

```
iptables -N incoming
```

```
iptables -A incoming -j DROP eth0 -s 192.168.0.45
iptables -A incoming -j ACCEPT -i lo
```

```
iptables -A FORWARD -j incoming
iptables -A INPUT -j incoming
```

### ICMP 数据包

防火墙通常拦截某些互联网消息协议 (`ICMP`) 消息。特别是 `ICMP` 消息可以控制你的路由任务。你需要启用 `ICMP` 消息，例如 `ping`、`traceroute` 和目的不可达 (`destination-unreachable`) 所需的消息。在许多情况下，你需要启用 `ICMP` 消息。某些情况下，拦截的 `ICMP` 消息可能会导致问题。你需要允许 `ICMP` 消息以确保网络诊断正常。

## 442 第 VI 部分：安全

你通过 `-m state` 指定状态模块。然后你可以使用 `--state` 选项。在这里，你可以指定以下任何状态：

| 状态 | 描述 |
|---|---|
| `NEW` | 创建新连接的数据包 |
| `ESTABLISHED` | 属于现有连接的数据包 |
| `RELATED` | 与现有连接相关但不属于其一部分的数据包，例如 ICMP 错误包或建立 FTP 数据连接的数据包 |
