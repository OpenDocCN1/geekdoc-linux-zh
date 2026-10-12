
Chain INPUT (policy ACCEPT)

target prot source

```
# 第四部分 在 SUSE Linux 中实现网络服务

Chain FORWARD (policy ACCEPT)
target prot opt source destination
Chain OUTPUT (policy ACCEPT)
target prot opt source destination

对于每个链，`iptables -L`（列出规则）的输出包含关于目标（`ACCEPT`、`DROP`、`REJECT` 是最常见的目标）、TCP/IP 协议以及数据包的源和目的的信息。

## iptables 目标

当对 TCP/IP 数据包进行分析时，将根据该数据包是否匹配规则做出处理的决定。如果数据包匹配规则，它将被发送到 netfilter 目标，最可能是 `ACCEPT`、`DROP` 或 `REJECT`。

我们将使用连接到防火墙的入站 SSH 连接作为示例。它最少将与 INPUT 规则上的 TCP 连接端口 22 匹配。如果你有一条描述此数据包的规则，你需要告诉 netfilter 系统 `ACCEPT` 此数据包进入 TCP/IP 协议栈，以便由内核进一步处理。

然而，你可以告诉 netfilter `DROP` 或 `REJECT` 数据包：

- 当数据包被发送到 `DROP` 目标时，它会直接消失，发送者将...
- 当数据包被发送到 `REJECT` 目标时，发送者会收到拒绝通知

- 该场景的重要部分是，任何非本地数据包（目标为或源自该机器）都会被传递到转发链（用于转发！）！

- 当我使用 SSH 从互联网连接到我的防火墙时，一个 TCP/IP 数据包尝试为我打开 SSH 连接。与转发示例中数据包到达防火墙的方式一样，内核分析数据包以查看它的去向。我的机器是数据包的最终地，它被插入到 INPUT 链中进行进一步处理。如果允许数据包通过，它将传递给内核并交给用户空间（这在未启用防火墙时是正常的）。

- `OUTPUT` 链略有不同，因为它不处理网络。只有当数据包源自机器本身时，才会触发 `OUTPUT` 链。例如，如果你登录到机器并向外部世界发起 FTP 连接，这被视为一个通过了 `OUTPUT` 链的数据包。

## 状态防火墙

状态防火墙跟踪连接的状态，这允许它根据数据包是现有连接的一部分还是新连接的一部分做出决策。这比简单的数据包过滤安全得多，因为它可以阻止不属于已建立连接的数据包。

要使用状态检测，你需要使用 `iptables` 中的 `-state` 模块。该模块允许你为不同的链启用或禁用状态跟踪。例如，你可以使用以下命令允许已建立和相关的连接：

```
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
```

此命令将允许任何属于已建立连接或与已建立连接相关的包。这是允许发起的连接的返回流量的常用方法。

## 设置你的第一条规则

在尝试设置更多规则之前，你需要为防火墙设置默认策略并启用一些规则（参见列表 24-2）。

### 列表 24-2

```
设置初始防火墙规则

iptables -P INPUT DROP

iptables -P OUTPUT DROP

iptables -P FORWARD DROP

iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

iptables -A FORWARD -m state --state ESTABLISHED,RELATED -j ACCEPT

iptables -A OUTPUT -m state --state NEW,ESTABLISHED,RELATED -j ACCEPT
```

## 在 SUSE Linux 中实现网络服务

你可能希望能够在机器与其他主机之间进行“跳转”，而无需背负为想要连接的每个协议或 TCP 端口设置新规则的负担，这是非常实用的。

此时，你的防火墙已经处于锁定状态，仅允许出站连接。

现在，假设你想允许防火墙接受一个入站的 SSH 连接。

### 添加规则

当你使用正确的规则时，你需要尽可能指定详细信息，以便对你允许进入受信网络的 TCP/IP 数据包进行完全控制。

至少，你需要指定链（chain）、协议和目的端口。仅凭这些信息，你无法建立一个很好的规则，因为你没有指定允许 SSH 连接的接口。你还可以指定链的类型：

- **NEW**：这是一个新连接；没有流量与此数据包关联。
- **ESTABLISHED**：此数据包来自你已经建立连接的机器（记住，当连接存在时，你会发送和接收数据）。
- **RELATED**：此数据包与现有连接有关。例如，FTP 协议，到 FTP 服务器的连接，而 FTP 服务器实际上会向客户端建立单独的连接。从客户端发起的这个单独连接就是 RELATED 连接。

```
iptables -A -p tcp --dport ssh -i eth0 -j ACCEPT
```

在这个示例中，你告诉 netfilter 你想向 INPUT 链中追加（`-A`）一条规则，指定 TCP 协议（`-p tcp`）、目的端口（`--dport`）为 ssh（端口 22）、在 eth0 接口（`-i eth0`）上入站（`-i`），并且你希望接受（`ACCEPT`）该数据包（`-j ACCEPT`）。`-j` 参数意味着“跳转到目标”。记住，netfilter 规则是在链中执行，所以你所说的是“停止这条链，因为你已经有了匹配项并跳转到目标”。这里的 `ACCEPT` 就是目标。

> `--dport` 参数 既可以接受数字形式的端口号，也可以接受在 `/etc/services` 中指定的服务名称。

在为连接设置规则时，你真的需要了解该协议的工作原理。对于 SSH 来说，众所周知它是一种 TCP 协议，运行在 22 端口。基于此，为它编写规则相对容易。

如何编写关于连接状态的规则取决于你，但由于初始 INPUT 规则已经允许了所有 `ESTABLISHED` 和 `RELATED` 连接，因此你不需要显式将状态设置为 `NEW`，因为通过不显式说明，你实际上已经允许了 SSH 的所有连接类型。

> 当你没有在 `iptables` 规则中显式指定某些内容时，假设你定义了默认设置。例如，如果你没有为入站连接设置接口，netfilter 将允许 SSH 连接通过所有网络接口。

### 在 SUSE Linux 中实现防火墙

这在协议类型和目的端口上确实是相同的。编写规则时要务非常小心，并确保显式地设置你想要控制的所有内容；否则，你可能会允许比想象中更多的流量进入。

对于你希望在防火墙开启的任何入站连接，你都可以像处理 SSH 连接一样相同地追加规则。

### 规则顺序

你必须非常注意在链中设置规则的顺序，因为 netfilter 按照 TCP/IP 数据包被插入内核的顺序来通过规则。如果你想在列表顶部插入规则（即使其成为第一个执行的规则），你可以使用 `iptables` 的 `-I`（insert）参数。

例如，如果你允许从互联网访问 SSH 防火墙，但已知某些 IP 地址不能访问 SSH，则你必须在通用 SSH 规则之前插入 `REJECT`/`DROP` 规则。

```
iptables -A INPUT -p tcp --dport ssh -i eth0 -j ACCEPT

iptables -I INPUT -p tcp --dport ssh -i eth0 10.32.1.4 -j DROP
```

在这个示例中，通过使用 `-s` 选项指定源 IP 地址，我们在通用 SSH 规则之前插入了 `DROP` 规则。

当 TCP/IP 数据包插入链时，它将依次检查链中的每个规则。如果某条规则匹配了数据包，它将立即被指定的目标（`ACCEPT`, `DROP`, `REJECT`）。在我们插入 SSH 规则的情况下，它在到达 `ACCEPT` 规则之前会被定向到 `DROP` 目标。

本质上，所有 TCP/IP 数据包顺序通过链中的每个规则，直到它们被定向到目标。如果没有规则匹配数据包，将由默认策略处理。

### 网络地址转换

netfilter 的主要用途之一是数据包过滤功能，另一个非常重要的方面是其 NAT 功能。

网络地址转换（NAT）是在数据包通过防火墙时，其源地址或目的 IP 地址发生改变的过程。

### 源地址转换 (SNAT)

源地址转换（SNAT）作用于通过防火墙并离开外部网络的数据包。对于这项工作，你必须在路由决策之前处理数据包，并且必须使用 `POSTROUTING` 链来实现。

SNAT 的主要目的是通过具有公 IP 的防火墙隐藏私有网络。这极大地降低了获取公 IP 地址的成本，并允许你在内部网络中使用不可路由的地址。

## 第四部分 在 SUSE Linux 中实现网络服务

为此，请启用从私有网络到互联网的流量转发。

```
bible:~ iptables -A FORWARD -s 192.168.1.0/24 -i eth0 -j ACCEPT
```
