
# 第 37 章：网络安全：防火墙、加密与认证

在 `iptables` 命令中，链名必须大写，例如 `INPUT`、`OUTPUT` 和 `FORWARD` 链名。

数据包过滤规则与 `ipchains` 中使用的规则非常相似，只有少数例外。规则被组合在不同的链中。内核使用链来管理它接收和发送的数据包。链简单来说就是一个规则清单。这些规则规定了对于包含特定头部的数据包应采取什么操作。规则按照 if-then-else 结构运行。如果数据包不匹配第一条规则，将检查下一条规则，依此类推。如果数据包不匹配任何规则，内核将触发链策略（chain policy）。通常，此时数据包会被拒绝。如果数据包匹配某条规则，它将被传递给目标（target），由目标决定如何处理该数据包。标准目标列于表 37-2。如果数据包不匹配任何规则，它将传递给链的默认目标。

目标反过来可以是另一个规则链，甚至是一条用户定义的规则链。数据包在最终到达目标之前可能会经过多个链。对于用户定义的链，默认目标始终是调用它的链中的下一条规则。这建立了一个过程或函数调用——类似于编程语言中的控制流。当某条规则以用户定义的链作为目标时，一旦其被激活，就会执行该用户定义链。如果没有匹配到任何规则，执行将返回到原始链中的下一条规则。

| 目标 | 功能 |
| --- | --- |
| ACCEPT | 允许数据包通过防火墙 |
| DROP | 拒绝数据包的访问（同于 `ipchains` 中的 DENY） |
| REJECT | 拒绝访问并通知发送者 |
| QUEUE | 将数据包发送到用户空间 |
| RETURN | 跳到链的末尾并让默认目标进行处理 |

**表 37-2. iptables 目标**

可以通过 Netfilter 网站提供的内核补丁添加特殊的目标和选项。例如，`SAME` 补丁会为所有连接返回相同的地址。Netfilter Makefile 的补丁式选项（patch-omatic option）将补丁你的内核源码，添加对新目标和选项的支持。然后你可以按照第 31 章描述的方法重建并安装内核。

内核使用三个防火墙链：`INPUT`、`OUTPUT` 和 `FORWARD`。通过接口接收数据包时，使用 `INPUT` 链来决定如何处理它。内核使用路由信息决定将其发送到哪里。如果内核将包发送到另一个主机，则检查 `FORWARD` 链。在实际发送数据包之前，还会检查 `OUTPUT` 链。此外，实现了两个 NAT 表链 `POSTROUTING` 和 `PREROUTING`，用于处理伪装和数据包地址修改。内置的 Netfilter 链列于表 37-3。

| 链 | 描述 |
| --- | --- |
| INPUT | 入数据包的规则 |
| OUTPUT | 出数据包的规则 |
| FORWARD | 转发数据包的规则 |
| PREROUTING | 重定向或修改入站数据包的规则，仅限 NAT 表 |
| POSTROUTING | 重定向或修改出数据包的规则，仅限 NAT 表 |

**表 37-3. Netfilter 内置链**

你使用 `iptables` 命令添加和修改链规则。一个 `iptables` 命令由关键字 `iptables` 后面表示要执行命令的参数组成。例如，`iptables -A` 是添加新规则的命令，而 `iptables -D` 是删除规则的命令。`iptables` 命令列于表 37-4。以下命令简单列出了系统中当前定义的链及其规则。输出显示了由 `iptables` 命令创建的默认值。

```
iptables -L -n

Chain input (policy ACCEPT):

Chain forward (policy ACCEPT):

Chain output (policy ACCEPT):
```

向链中添加新规则，使用 `-A`。使用 `-D` 移除，使用 `-R` 替换它。在命令之后，列出规则所应用的链，例如 `INPUT`、`OUTPUT` 或 `FORWARD` 链，或者用户定义的链。接下来，你列出指定你想要的操作的不同选项。大多数与 `ipchains` 中使用的相同，仅有少数例外。

| 选项 | 功能 |
| --- | --- |
| -A | 在链末尾追加规则 |
| -D | 从链中删除规则 |
| -I | 在链开头插入规则 |
| -R | 替换中的规则 |
| -L | 列出链及其规则 |
| -E | 重命名链 |
| -F | 清空链中的所有规则 |
| -N | 创建一个新的用户定义链 |
| -X | 删除用户定义链 |
| -P | 修改链的策略 |

**表 37-4. iptables 命令**

数据包，`-d` 指定目的地址，`-j` 选项指定目标。`ACCEPT` 选项允许数据包通过。`-i` 选项指定输入设备，只能用于 `INPUT` 和 `FORWARD` 链。`-o` 选项指定输出设备，只能用于 `OUTPUT` 和 `FORWARD` 链。表 37-5 列出了几个基本选项。许多与 `ipchains` 选项相似，但某些（如 `-i`）不同，某些则缺失了（如 `-y`）。

| 选项 | 功能 |
| --- | --- |
| -p [] proto | 指定协议，如 TCP、UDP、ICMP 或 ALL |
| -s [] address[/mask] [] [port[:port]] | 匹配源地址。带有端口参数时，可以指定端口。 |
| --port [] [port[:port]] | 源端口指定。可以使用冒号 port:port 指定端口范围。 |
| -d [] address[/mask] [] [port[:port]] | 匹配目的地址。带有端口参数时，可以指定端口。 |
| --dport [] [port[:port]] | 目的端口指定 |
| --icmp-type [] typename | 指定 ICMP 类型 |
| -i [] name[+] | 使用名称指定输入接口（例如 eth0）。名称末尾的 + 号匹配所有具有该前缀的接口（eth+ 匹配所有网络接口）。只能用于 `INPUT` 链。 |
| -j target [port] | 指定规则的目标（为 REDIRECT 目标指定 [port]） |
| --to-source <ipaddr> [-< ipaddr>][: port-port] | 用于 SNAT 目标，重写数据包的新源 IP 地址 |
| --to-destination <ipaddr>[-< ipaddr>][: port-port] | 用于 DNAT 目标，重写数据包的新目的 IP 地址 |
| -n | 地址和端口的数字输出，与 -L 一起使用 |

**表 37-5. iptables 选项**

| Option | Function |
| --- | --- |
| -o [!] name[+] | 使用其名称指定输出网络接口（例如 eth0）。仅可用于 FORWARD 和 OUTPUT 链。 |
| -t table | 指定要使用的表，例如 `-t nat` 指定 NAT 表。 |
| -v | 详细模式，显示规则详情，与 -L 配合。 |
| -x | 扩展数字（显示精确值），与 -L 使用。 |
| [!] -f | 匹配分片数据包从第二个到倒最后一个分片。 |
| [!] -V | 打印包版本。 |
| ! | 取反选项或地址。 |
| -m | 指定要使用的模块，例如 state。 |
| --state | 指定状态模块的选项，如 NEW、INVALID、RELATED 和 ESTABLISHED。用于检测包的状态。NEW 引用 SYN 数据包（新连接）。 |
| --syn | SYN 数据包，新连接。 |
| --tcp-flags | TCP 标志：SYN, ACK, FIN, RST, URG, PS 和 ALL 用于标志。 |
| --limit | limit 模块的选项 (`-m limit`)。用于控制匹配速率，每秒匹配指定的次数。 |
| --limit-burst | limit 模块的选项 (`-m limit`)。在限制限制生效前指定最大突发数。用于控制拒绝服务攻击。 |

**表 37-5.** iptables 选项（续）

`iptables` 设计为具有可扩展性，有许多带有选择标准的选项可以包含在 `iptables` 中。例如，TCP 扩展包含了检查 SYN 数据包的 `--syn` 选项。ICMP 扩展提供了 `--icmp-type` 选项，用于指定 ICMP 数据包，如 ping 操作中使用的数据包。limit 扩展包含了 `--limit` 选项，通过该选项你可以限制在特定时间段匹配包的最大数量，例如 a。

在下面的示例中，用户向 `INPUT` 链添加了一条规则，以接受源自地址 `192.168.0.55` 的所有包。任何接收到的（`INPUT`）且源地址 (`-s`) 匹配 `192.168.0.55` 的包都将被接受并通过 (`-j ACCEPT`)。

```
iptables -A INPUT -s 192.168.0.55 -j ACCEPT
```

有两个内置目标，`DROP` 和 `ACCEPT`（`ACCEPT` 等同于 `ipchains` 的 DENY 目标）。其他目标可以是用户定义的链或添加的扩展，例如 `REJECT`。有两个用于管理链的特殊目标，`RETURN` 和 `QUEUE`。`QUEUE` 表示链的结束并返回其开始的链。`QUEUE` 用于将包发送给用户（替换了 `ipchains` 中的 `-o`）。

```
iptables -A INPUT -s my.junk.com -j DROP
```

你可以使用 `!` 符号将规则转为反规则。例如，要接受除特定地址以外的入站包，请在 `-s` 选项和该地址之前放置 `!` 符号。下面的示例将接受除 IP 地址 `192.168.0.45` 之外的所有包：

```
iptables -A INPUT -j ACCEPT ! -s 192.168.0.45
```

你可以使用域名或 IP 数字来指定单个地址。对于地址范围，你可以使用其网络的 IP 数字和网络 IP 掩码。IP 掩码可以是一个 IP 数字，也可以仅仅是组成掩码的位数。例如，网络 `192.168.0` 中的所有地址可以用 `192.168.0.255.255.255` 或 `192.168.0/24` 表示。要指定任何地址，可以使用 `0.0.0.0/0.0.0.0` 或简单地 `0/0`。如果不存在 `-s` 或 `-d` 指定，规则将引用任何地址。下面的示例接受传入的消息，这些消息来自（源自）`192.168.0.0` 网络中的任何主机，并去往（目的）任何地方（省略 `-d` 选项或可以写为 `-d 0/0`）：

```
iptables -A INPUT -s 192.168.0.0/24 -j ACCEPT
```

`iptables` 规则通常应用于特定的网络接口，例如用于连接互联网的以太网接口。对于连接到互联网的单个系统，你将有两个接口：一个用于互联网连接的接口和一个本地回环接口 (`lo`)，用于系统内用户之间的内部连接。用于互联网的网络接口使用该接口的设备名称进行引用。例如，设备名为 `/dev/eth0` 的以太网卡通过名称 `eth0` 引用。使用设备名为 `/dev/ppp` 的 PPP 协议将具有名称 `ppp0`。在 `iptables` 规则中，你使用 `-i` 选项来指示输入设备；它只能用于 `INPUT` 和 `FORWARD` 链。`-o` 选项指示输出设备，只能用于 `OUTPUT` 和 `FORWARD` 链。规则随后可以应用于特定网络设备上到达和离开的包。

## 用户定义链

通过 `iptables`，你可以创建自己的链来更有效地组织规则。这允许你将相关规则分组并作为一个单一实体应用。创建一个新链，使用 `-N` 命令：

```
iptables -N MY_CUSTOM_CHAIN
```

一旦创建了链，你就可以像使用内置链一样使用 `-A` 命令向其添加规则。要将流量重定向到自定义链，使用 `-j` 选项：

```
iptables -A INPUT -p tcp --dport 80 -j MY_CUSTOM_CHAIN
```

你还可以使用 `-D` 命令从链中删除规则，或使用 `-X` 命令删除链本身：

```
iptables -D MY_CUSTOM_CHAIN -p tcp --dport 80

iptables -X MY_CUSTOM_CHAIN
```

## ICMP 数据包

防火墙通常拦截 Internet Message Protocol (ICMP) 消息。特别是 ICMP 重定向消息可以控制你的路由。然而，你需要启用某些 ICMP 消息，即 ping、traceroute 特别是目标不可达的消息。你可以使用 `--icmp-type` 选项启用 ICMP 类型，其参数接受表示消息的数字或名称。下面的示例启用了 echo-reply、echo-request 和 destination-unreachable 消息，它们的数字分别为 0、8 和 3。

```
iptables -A INPUT -p icmp -i eth0 --icmp-type echo-reply -d 10.0.1
```
