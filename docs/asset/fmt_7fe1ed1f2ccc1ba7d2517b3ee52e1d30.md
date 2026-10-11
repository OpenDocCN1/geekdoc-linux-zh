
同样，你必须告诉网络中的所有机器使用 `192.168.9.253` 作为默认网关（因为你必须通过网关才能访问网络外部的任何机器）。可以直接访问 LAN 机器。在你的网络中的所有机器上（显然是除了防火墙之外）执行以下操作：

```bash
echo "Add default route through the gateway"
/sbin/route add default gw 192.168.9.253 eth0
```

```bash
echo "192.168.9.0/24 is directly reachable"
/sbin/route add -net 192.168.9.0/24 dev eth0
```

接下来是防火墙规则——保护网络的规则。规则使用 `iptables` 工具编写。这是一个非常有用的工具，虽然有点复杂，且有一个关于各种选项的详细 `man` 页。`iptables` Netfilter 使用三个不同的内置链：`INPUT`、`FORWARD` 和 `OUTPUT`。数据包通过这些链遍历，因此规则是为特定链编写的。就你的防火墙而言，任何发往你的防火墙（`192.168.9.253` 或 `192.168.9.254`）的数据包都进入 `INPUT` 链。如果数据包旨在被转发（也就是说，它不是发给你的防火墙，且你的防火墙中有到目的地的路由），它将通过 `FORWARD` 链。由你的防火墙生成的任何数据包都将从该机器通过 `OUTPUT` 链发出。（这个简要说明适用于任何 Linux 机器。）虽然你永远不会希望防火墙转发所有通过它的数据包，但你可能想要测试上述配置下的网关功能是否正常工作。为此，将 `FORWARD` 链的默认策略设为 `ACCEPT`（使用 `-P` 选项）——也就是说，任何通过 forward 链的数据包都被接受：

来自网络 `192.168.9.0/24` 中任何机器（除了防火墙）发往网络外部任何（在线）机器的 `ping` 请求现在将返回 `ICMP` echo reply 数据包。如果外部机器不可达，可能是电缆或网卡存在问题，或者你可能错误配置了某些内容。

现在，让我们构建“墙”。设置防火墙最简单的方法是拒绝（`DROP`）所有类型的数据包，然后编写规则来允许（`ACCEPT`）那些你希望通过的数据包。所以，让我们将每个链的默认策略设置为丢弃数据包。

![](img/3c4d8a97b5d96c835281dc0dacbc8551_80_0.png)

![](img/3c4d8a97b5d96c835281dc0dacbc8551_81_0.png)

在此之前，清除所有现有规则：

```bash
echo "Flush existing rules"
/sbin/iptables -F
echo "Set the default policy to drop packets"
/sbin/iptables -P INPUT DROP
/sbin/iptables -P OUTPUT DROP
/sbin/iptables -P FORWARD DROP
```

至此，你可能已经注意到，规则基本上规定了数据包必须具备的一些条件。如果匹配这些条件，则执行规则中指定的操作；否则检查链中的下一条规则，如此继续直到匹配某条规则为止。如果链中的规则均未匹配，则执行默认操作或策略（此处为 `DROP`）。

让我们编写第一条规则——一条允许从私有网络发出 SSH 数据包出去的规则：

```bash
echo "Allow outgoing SSH"
/sbin/iptables -A FORWARD -p TCP -i eth0 \
-s 192.168.9.0/24 -d 0.0.0.0/0 --dport 22 -j ACCEPT
```

这条规则几乎不言自明。选项 `-A` 指定规则要追加到的链，`-p` 指定协议（`UDP`、`TCP`、`ICMP` 等）。选项 `-i` 指定接收数据包的接口名称。因为发出的 SSH 数据包来自 `192.168.9.0/24` 网络（`-s` 指定源地址），它们将通过防火墙的 `eth0` 接口进来。SSH 流量的目标端口（`-dport`）是 `22`。目标地址由 `-d` 选项指示，`0/0` 表示任何地址。最后，匹配此类数据包的动作是 `ACCEPT`（由 `-j` 选项指定），这意味着允许匹配的数据包通过。

现在，我们编写了一条规则，允许来自 `192.168.9.0/24` 的 SSH 流量去往任何地方。但这行得通吗？你能从私有网络 SSH 登录到公共网络中的机器吗？我们在哪里允许来自 SSH 服务器（在公共网络中）返回到客户端（在私有网络中）的数据包？以下规则实现了这一点：

```bash
/sbin/iptables -A FORWARD -p TCP -i eth1 -s 0.0.0.0/0 \
--sport 22 -d 192.168.9.0/24 -j ACCEPT
```

这看起来很好，但我们随后需要为每种服务编写这样的规则。更糟糕的是，上面的规则做了超出需求的事情。它允许任何机器使用源端口 `22` 连接到私有网络。我们应该做的是追加一条规则，仅允许来自公共网络且属于由 `192.168.9.0/24` 网络中的机器发起的 SSH 连接的一部分的数据包。

`iptables` 维护状态信息以进行此类连接跟踪。维护的四种状态是 `NEW`、`ESTABLISHED`、`RELATED` 和 `INVALID`。我们在这里不详细讨论这些状态。暂时请记住，状态 `NEW` 表示数据包是新连接的一部分。当在相反方向看到响应数据包时，连接变为 `ESTABLISHED`。注意这与 TCP 连接建立过程中的状态无关。对于相应请求的 `ICMP` 或 `UDP` 回复也将标记连接为 `ESTABLISHED`。请参阅 `iptables-tutorial.frozentux.net/iptables-tutorial.html#STATEMACHINE` 以了解连接跟踪机制的确切工作原理。现在（在移除上述规则后），为了转发所有组成 `ESTABLISHED` 连接的一部分的数据包，我们编写以下规则：

```bash
echo "Allowing ESTABLISHED connections"
/sbin/iptables -A FORWARD -m state --state \
ESTABLISHED -j ACCEPT
```

这条规则确保只有属于 `ESTABLISHED` 连接的数据包才会被接受；发往 `192.168.9.0/24` 的新连接请求将不会被接受。理想情况下，为了访问任何服务（如 `HTTP` 或 `FTP`），我们需要仅允许 `NEW` 和 `ESTABLISHED` 连接出去（`NEW` 将允许第一个数据包，`ESTABLISHED` 将允许同一连接的所有后续数据包），并且仅允许 `ESTABLISHED` 连接进入私有网络。同样，如果你的网络中有一个 `DNS` 服务器，且需要允许外部访问（查询）它，以下规则可以做到（假设 `198.168.9.1` 是 `DNS` 服务器）：

```bash
echo "Allowing incoming DNS requests"
/sbin/iptables -A FORWARD -p TCP -i eth1 \
```

![](img/3c4d8a97b5d96c835281dc0dacbc8551_81_1.png)

`-d 198.168.9.1 -i eth1 -j ACCEPT`

请注意，此处使用的接口是 `eth1`，因为来自公共网络的报文将在 `eth1` 上接收。（我们没有使用 `-s 0/0`，因为默认情况下已添加。）此外，请记住，`DNS` 查找之所以成功，仅因为我们已经添加了允许 `FORWARD` 列表中 `ESTABLISHED` 连接的规则（是的，`UDP` 流量也有关联的 `ESTABLISHED` 状态）。

到目前为止，除了 SSH 和 DNS 之外，我们已经阻止了所有协议。对于新的系统管理员来说，阻止 `ICMP` 报文是一种常见的做法。但这并不是一个好主意，因为 `ICMP` 报文在许多方面都有用，例如学习大型局域网中不同互连网络之间的路由，查看机器是否在线，进行路径 MTU 发现等。因此，假设我们是明智的管理员，让我们允许 `ICMP` 报文通过防火墙：

```bash
echo "Allowing ICMP packets"
/sbin/iptables -A FORWARD -p ICMP -j ACCEPT
```

之前，我们阻止了发往防火墙盒子以及从防火墙盒子发出的任何报文（使用 `INPUT` 和 `OUTPUT` 链）。为了诊断目的，我们可以允许 `ICMP` 报文通过这两个链——也就是说，允许 `ICMP` 报文进出防火墙：

```bash
echo "Allowing ICMP packets to the firewall"
/sbin/iptables -A INPUT -p ICMP -j ACCEPT

echo "Allowing packets from the firewall"
/sbin/iptables -A OUTPUT -p ICMP -j ACCEPT
```

`ICMP` 报文也可以进行速率限制（作为对基于 `ICMP` 攻击的预防措施）：
