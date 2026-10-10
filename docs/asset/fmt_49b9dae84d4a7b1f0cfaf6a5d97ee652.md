
```bash
#!/bin/bash
# (1) Policies
iptables -P INPUT DROP
iptables -P OUTPUT DROP
iptables -P FORWARD DROP

# (2) User-defined chain
iptables -N okay
iptables -A okay -p tcp --syn -j ACCEPT
iptables -A okay -m state --state ESTABLISHED,RELATED -j ACCEPT

# (3) INPUT chain rules
iptables -A INPUT -i lo -m state --state RELATED -j ACCEPT
iptables -A INPUT -i lo -s 127.0.0.1 -j ACCEPT
iptables -A INPUT -i lo -s 10.0.0.1 -j ACCEPT
iptables -A INPUT -i eth0 -s 123.45.67.89 -j ACCEPT
iptables -A INPUT -i eth1 -s 10.0.0.2/24 -j ACCEPT
iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT
iptables -A INPUT -p icmp --icmp-type echo-reply -j ACCEPT
iptables -A INPUT -j okay

# (4) FORWARD chain rules
iptables -A FORWARD -i eth1 -m state --state ESTABLISHED,RELATED -j ACCEPT

# (5) OUTPUT chain rules
iptables -A OUTPUT -s 127.0.0.1 -j ACCEPT
iptables -A OUTPUT -s 10.0.0.1 -j ACCEPT
iptables -A OUTPUT -s 123.45.67.89 -j ACCEPT

# (6) POSTROUTING chain rules
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

(注：由于原文文本在示例部分似乎出现了截断或重复，上述译文已根据您提供的逻辑结构进行了对齐和翻译，确保逻辑通顺)

# 第14章：计算机安全问题 585

* *来自局域网（LAN）的包 — 因为你需要使用局域网上的用户和防火墙本身来访问互联网，这组规则允许从这些计算机发出的包。第一行允许 `iptables` 接受源地址为局域网内有效地址的所有协议（`10.0.0.0/24`，代表 IP 地址 `10.0.0.1` 到 `10.0.0.254`）。接下来的三行允许来自防火墙本身所有有效地址的包（`-s 127.0.0.1`、`-10.0.0.1` 和 `123.45.67.89`）。最后一行接受局域网上的广播包（`-d 210.0.0.255`）。

* *来自互联网（已连接）的包 — 这一行被分成了两部分（我只是使用了反斜杠来连接这些行，因为页面宽度不足以将其单行显示）。它接受既与已建立的连接关联（`--state ESTABLISHED,RELATED`），又直接请求防火墙 IP 地址（`123.45.67.89`）的包。

* *TCP 规则（新连接） — 这里是你为你想要向互联网上的任何人提供的 TCP 服务开放端口的地方。在这些行中，为 FTP 服务（`--destination-port 21`）、安全外壳服务（`22`）、Web 服务（`80`）和 IDENT 身份验证（`113`）开放端口，最后一种对于 IRC 等协议可能是必须的。我们没有立即接受这些请求，而是跳转到你定义的 `okay` 链（chain），以检查数据包的格式是否正确。

> 注意：在允许数据包访问端口之前，你想要确保你所允许访问的端口上的服务已经过正确配置。

* *UDP 规则（新连接） — 这些行定义了接受来自互联网的 UDP 服务连接包的端口。在示例中，我选择接受 DNS 服务的请求（`--destination-port 53`），因为该计算机被设置为了 DNS 服务器。该示例还说明了接受其他几个潜在端口请求的行。端口 20的4 是由于于你局域网上的用户可能想要使用的某些多媒体应用程序所需的，而端口 4000 则由 ICMP 协议（用于在线聊天）使用。

* *ICMP 规则 — ICMP 消息更多是为了报告服务器的状态而非提供服务。在我们的示例中，接受 ICMP 协议请求的包对应 ICMP 类型 8 和 11。类型 8 服务允许你的计算机接受回显请求消息，使得人们能够 ping 你的计算机以检查其是否可用。类型 11 与在传输过程中超过生存时间（TTL）的包包有关，你接受返回给你的时间超时（Time Exceeded）消息。（你需要接受 11 消息才能使用 `traceroute` 命令找到通往目标主机的损坏路径）。

* (4) FORWARD 链规则 — 因为此防火墙同时也充当路由器，所以需要 FORWARD 规则来限制防火墙在两个网络（互联网和本地局域网）之间通过和不通过的内容。第一行转发来自本地局域网的所有内容（`-A -i eth1`）。第二行转发来自互联网的任何与已建立连接关联（`--state ESTABLISHED, RELATED`）的包。

* (5) OUTPUT 链规则 — 这些规则基本上是为了防止来自你本地计算机的任何人伪造 IP 地址（即，谎称数据包来自它们并非来自的地方）。根据这三条规则，从你的防火墙输出的每个包源地址必须是防火墙计算机接口的地址之一（`127.0.0.1`、`10.0.0.1` 或 `123.45.67.89`）。

* (6) PREROUTING 链规则 — PREROUTING 链为已接受但尚未进行额外处理的数据包定义规则。这是执行实际网络地址转换（NAT）工作的地方。对于 NAT 表（`-t nat`），在 PREROUTING 链中，所有发往互联网的包都翻译为防火墙外部接口的地址（`--to-123.45.67.89`）。在这种情况下，我使用了源网络地址转换（SNAT）链，因为我与互联网连接关联了一个静态 IP 地址（`123.45.67.89`）。如果我使用动态 IP 地址（通过 DHCP），我将使用 `MASQUERADE` 代替 SNAT。我还必须更改任何对 `-d 123.45.67.89 -i eth0` 的引用（当然，你将使用不同的 IP 地址并可能使用不同的以太网接口）。

## 示例 2：共享互联网连接的防火墙（无服务器）

在这种场景下，防火墙保护着一个 Linux 系统（防火墙）和局域网上的几个仅用于连接互联网的系统。此防火墙后面没有服务器，因此你想要防止人们请求服务。

你可以使用示例 1 中所示的脚本，但不使用请求 TCP 服务的行。你可以丢弃第 2 部分中的自定义链，并丢弃第 3 部分的 TCP 规则。如果你不想让你的防火墙对 ping 请求（类型 8）可见，也可以移除 ICMP 规则。

## 示例 3：带有互联网连接的单系统防火墙

在例示例中，有一个接口将 Fedora 系统连接到互联网。你没有将该连接与其他计算机共享。

# 第三部分：管理 Fedora 和 RHEL

## 理解 iptables

现在你已经看到了一些关于 `iptables` 规则以及如何获取它们的内容，请后退一步，看看 `iptables` 是如何工作的。

`iptables` 功能通过让进入或离开防火墙的 IP 包（即网络数据）遍历一组定义了对数据包处理方法的链（chains）来实现。你创建的每条规则本质上都执行以下两个操作：

- 检查是否满足特定标准（例如数据包请求特定服务或来自特定地址）

- 采取动作（例如丢弃、接受或进一步处理）

不同的规则适用于不同的规则。例如，存在过滤（filter）、网络地址转换（nat）和修改数据包头部（mangle）表。根据数据包的源和目的，它遍历不同的链。你创建的大多数规则关联 filter 表（如果没有指定其他表，则隐含）。

与 filter 表相关的链有 `INPUT`、`OUTPUT` 和 `FORWARD`。你也可以添加自定义链。你可能对使用示例所示的基础规则添加或移除特定的 TCP 和 UDP 服务感兴趣。对于想要通过的分配 `ACCEPT`，对于想要丢弃的分配 `DROP`。你还可以分配 `REJECT` 以丢弃包但向发送者返回消息，或分配 `LOG` 既丢弃也不接受消息，而是记录数据包的信息。

`iptables` 内置了许多强大的功能。以下描述将介绍你使用 `iptables` 可以进行的一些酷操作，并提供一些使用技巧。

## 通过 iptables 防墙允许 FTP 和 IRC 服务

在被动 FTP 中，FTP 客户端会将其 IP 地址和它监听数据的端口号发送给服务器。如果该客户端位于你防火墙后的计算机上，且你正在对其进行 NAT，那么这些信息也必须被翻译，否则 FTP 服务器将无法与客户端通信。

`iptables` 使用连接跟踪模块来跟踪连接。利用此功能，它可以查看每个 FTP 包的数据区域（即不是在 IP 数据包头部中），以获取执行 NAT 所需的信息。为了进行 FTP 连接跟踪（以允许到局域网内客户端的被动 FTP 连接），你需要加载以下模块：
