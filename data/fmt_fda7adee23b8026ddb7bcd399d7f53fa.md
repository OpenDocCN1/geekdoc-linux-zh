
重复 `INPUT` 和 `FORWARD` 规则的常用方法是创建一个 `INPUT` 和 `FORWARD` 链都会进入的用户链。使用 `-N` 选项定义用户链。下一个示例显示了这种安排的基本格式。新链名为 `incoming`。现在为 `FORWARD` 和 `INPUT` 链定义规则。`INPUT` 和 `FORWARD` 链使用 `incoming` 链作为目标，直接跳转到那里并使用规则处理它们接收到的任何数据包。

```
iptables -N incoming

iptables -A INPUT -j incoming -i eth0 -s 192.168.0.45

iptables -A FORWARD -j incoming -i eth0 -s 192.168.0.45

iptables -A incoming -j DROP

iptables -A incoming -j ACCEPT -i lo
```

## ICMP 数据包

防火墙通常拦截某些 Internet 消息协议（`ICMP`）消息。特别是重定向消息可能会控制你的路由任务。然而，你需要启用某些 `ICMP` 消息，例如用于 `ping`、`traceroute` 和目的不可达。在大多数情况下，始终需要允许目的不可达数据包，否则查询将挂起。一些常见的 `ICMP` 包类型列在表 37-6 中。接下来的示例启用了 `echo-reply`、`echo-request` 和目的不可达消息，它们的数字为 `0`、`8` 和 `3`。它们的规则将如下：

```
ACCEPT icmp -- 0.0.0.0/0 10.0.1 icmp type 0

ACCEPT icmp -- 0.0.0.0/0 10.0.1 icmp type 8

ACCEPT icmp -- 0.0.0.0/0 10.0.1 icmp type 3
```

`Ping` 操作需要进一步控制以避免死亡攻击。你可以通过几种方法实现。一种是拒绝任何分片。`Ping` 数据包通常小。你可以通过拒绝任何分片的 `ICMP` 数据包来阻止死亡攻击。使用 `-f` 选项来指示分片。

```
iptables -A INPUT -p icmp -j DROP -f
```

另一种方法是限制接收到的 `ping` 数据包的匹配次数。使用 `limit` 模块来控制 `ping` 操作上的匹配次数。

| 数字 | 名称 | 所需 |
|---|---|---|
| 0 | `echo-reply` | `ping` |
| 3 | `destination-unreachable` | 任何 `TCP`/`UDP` 流量 |
| 5 | `redirect` | 路由 |
| 8 | `echo-request` | `ping` |
| 11 | `time-exceeded` | `traceroute` |

表 37-6 常见 `ICMP` 包

使用 `m limit` 使用 `limit` 模块，并 `--limit` 指定允许的匹配次数。`1/s` 将每秒允许一次匹配。

```
iptables -A FORWARD -p icmp --icmp-type echo-request -m limit --limit 1/s -j ACCEPT
```

## 端口

如果你的系统托管服务（例如 `Web` 或 `FTP` 服务器），你可以使用 `iptables` 控制访问。你可以使用源端口 (`--sport`) 或目的端口 (`--dport`) 配合服务使用的端口来指定特定服务。`iptables` 允许命名端口，例如 `Web` 服务器端口。服务的名称及其使用的端口列在 `/etc/services` 文件中，该文件将端口映射到特定服务。对于域名，你可以使用域名。如果你想，也可以使用端口号，在数字前加冒号。接下来的示例接受所有到位于 `192.168.0.43` Web 服务器的消息：

```
iptables -A INPUT -d 192.168.0.43 --dport www -j ACCEPT
```

你也可以使用端口引用来保护服务并拒绝其他服务。如果你正在设计一个对开放更大的防火墙，允许用户自由连接互联网，通常使用这种方法。你知道某些服务是有害的，例如 `Telnet` 和 `NTP`，可以选择性拒绝。例如，要拒绝防火墙上的任何类型 `Telnet` 操作，你可以丢弃进入 `Telnet` 端口 `23` 的所有包。为了保护 `NFS` 操作，你可以拒绝访问映射器端口 `111`。你可以使用端口号或端口名称。

```
# 拒绝外部访问防火墙上的 portmapper 端口

iptables -A arriving -j DROP -p tcp -i eth --dport 111

# 拒绝外部访问防火墙上的 telnet 端口

iptables -A arriving -j DROP -p tcp -i eth --dport telnet
```

规则列表将如下所示：

```
DROP      tcp      0.0.0.0/0    0.0.0.0/0    dpt:111

DROP      tcp      0.0.0.0/0    0.0.0.0/0    dpt:23
```

一个端口相关的安全问题是访问 `XFree6` 端口从 `6000` 到 `6009` 的 `X` 服务器。在相对开放的防火墙上，这些端口可能被用于通过 `X` 服务器非法访问你的系统。端口范围可以使用冒号指定，例如 `6000:6009`。你也可以使用 `x11` 作为第一个端口，`x11:6009`。

## 第 37 章：网络安全：防火墙、加密与身份验证

`X` 服务器可以通过 `SSH` 来保护安全，`SSH` 通常通过端口 `6010` 访问 `X` 服务器。

```
iptables -A arriving -j DROP -p tcp -i eth0 --dport 6000:6009
```

这里显示了常见的检查端口及其标签：

| 服务 | 端口号 | 端口标签 |
|---|---|---|
| `Auth` | `113` | `auth` |
| `Finger` | `79` | `finger` |
| `FTP` | `21` | `ftp` |
| `NTP` | `123` | `ntp` |
| `Portmapper` | `111` | `sunrpc` |
| `Telnet` | `23` | `telnet` |
| `Web server` | `80` | `www` |
| `XFree86` | `6000:6009` | `x11:6009` |

![](img/95726952b50a5b7113b49b7e63a39779_878_0.png)

## 状态

最有用的扩展之一是状态扩展（`state extension`），它可以轻松检测数据包的跟踪信息。你需要先使用 `-m state` 指定状态模块。然后你可以使用 `--state` 选项。在这里，你可以指定以下任何状态：

| 状态 | 描述 |
|---|---|
| `NEW` | 创建新连接的数据包 |
| `ESTABLISHED` | 属于现有连接的数据包 |
| `RELATED` | 与现有连接相关但不是其一部分的数据包，例如 `ICMP` 错误或建立 `FTP` 数据连接的包包 |
| `INVALID` | 出某些原因无法识别的数据包 |
| `RELATED+REPLY` | 与已建立的连接相关但不是直接属于其的数据包 |

如果你正在设计一个防火墙来保护本地网络免受来自外部网络的任何渗透尝试，你可能想要限制传入的数据包。简单地拒绝所有数据包的访问是不可行的，因为连接到外部服务器（例如互联网）的用户必须从那里接收信息。相反，你可以拒绝用于发起连接的特定类型数据包的访问。其理念是攻击者必须从外部发起连接。此类数据包的头部 `SYN` 位被设置，而 `ACK` 位为空。状态模块的 `NEW` 状态匹配任何 `SYN` 数据包。通过为此类数据包指定 `DROP` 目标，你拒绝了任何尝试与你的系统建立连接的数据包。任何尝试连接到你系统的人都无法成功。你本地系统中已向外部主机发起连接的用户仍然可以与它们通信。以下示例将丢弃任何在 `eth0` 接口上尝试创建新连接的数据包，尽管它们在任何其他接口上会被接受：

```
iptables -A INPUT -m state --state NEW -i eth0 -j DROP
```

你可以在 `eth0` 设备上使用 `!` 运算符并结合 `ACCEPT` 目标，组合成一条规则，接受除 `eth0` 设备上的数据包之外的所有新数据包。如果 `eth0` 设备是连接到互联网的唯一设备，这有效地阻止了外部访问。同时，其他设备（如本地主机）的输入操作可以自由建立新连接。这种条件条件 `INPUT` 规则用于允许整体访问的同时存在例外情况。它通常假设随后的规则（如链策略）将丢弃数据包。

```
iptables -A INPUT -m state --state NEW ! -i eth0 -j ACCEPT
```

下一个示例将接受 `eth0` 接口上任何属于已建立连接或此类连接相关的数据包：

```
iptables -A INPUT -m state --state ESTABLISHED, RELATED -j ACCEPT
```
