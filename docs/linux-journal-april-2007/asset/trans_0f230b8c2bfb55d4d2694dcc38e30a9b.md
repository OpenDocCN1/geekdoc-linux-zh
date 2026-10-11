
## INDEPTH
## 从零开始构建 Linux 防火墙
关于入门 iptables 的初步步骤。
**DINIL DIVAKARAN**

### 构建防火墙
在 Linux 机器上构建防火墙是一件很容易完成的事情。本文描述了使用 Linux 工具从零开始开发防火墙的基本步骤。本文面向对（Linux）防火墙感兴趣的新手。更重要的是，本文面向所有希望亲自动手并尽快让防火墙投入运行的新管理员，但同时又不会错过途中涉及的重要概念。我在印度理工学院（IIT）马德拉斯分校计算机科学与工程系的 DON（分布式与光网络）实验室从事基于 Linux 的防火墙工作的经验，是撰写本文的最主要动力。

在本文中，我们将探讨开发一个位于边缘的防火墙，它将你的私有网络与世界其他部分隔离开来；因此，该防火墙还将充当网关。

![](img/3c4d8a97b5d96c835281dc0dacbc8551_79_0.png)

首先，你为什么需要这样的防火墙？最重要的是，你需要限制对你网络中机器的访问，这个网络可能由各种服务器组成。其中一台可能是邮件服务器，另一台可能是 DNS 服务器，但只有这些特定服务（*由这些服务器提供*）需要被访问，而不是网络中的一切。简而言之，防火墙用于保护私有网络免受世界其他部分的侵犯——称之为公共网络（在大多数场景下即互联网）。

拥有防火墙的一个不那么明显的原因是你有必要阻止所有进入或通过你网络的不想要的流量，这些流量否则可能会消耗带宽。理想情况下，这类流量应在网关处（网关或防火墙）被拦截。一个好的例子是存在许多子网络的情况，例如在大学校园中。子网络中的一台机器可能会感染病毒，并可能泛洪或广播 ARP 数据包。同样，来自私有网络外部的某些 Windows 电脑可能会广播 netbios（netbios-ns/netbios-dgm）数据包，这些对你的网络毫无意义，因此应被防火墙阻止。

但是，一些 ARP 数据包可能是针对你网络（或子网）中机器的合法请求。如果你阻止了这些合法的 ARP 广播请求，那么没有任何数据包（无论是好是坏）会到达你的网络；因为私有网络外部的机器将无法获得你网络中机器 IP 地址对应的以太网地址。为了解决这个问题，你应该配置防火墙作为 ARP 请求的代理——也就是说，你的防火墙应回复这些 ARP 请求。

现在，让我们进入实施细节。假设你的私有网络是 192.168.9.0/24。你的防火墙，也是网关，必须有两个接口：一个指向你的网络（eth0），另一个连接到公共网络（eth1）。

首先，为这两个接口配置 IP。这可以使用网络配置工具或通过 ifconfig 命令完成。理想情况下，最好使用系统网络配置工具（Fedora Core 2–5 中的 *system-config-network*）或编辑配置文件（FC 2–5 中位于 *at /etc/sysconfig/network-scripts*），以便在网络启动（作为启动过程的一部分）或重启（手动）时配置得以保留。你也可以通过在 */etc/rc.d/rc.local* 末尾追加 ifconfig 命令来配置 IP（因为该文件在启动过程结束时执行）。如果你这样做，请确保这些命令在网络手动重启时也能被执行。

我们使用 ifconfig 以保持发行版无关性（由于缺乏更好的术语）。

关于接口使用的 IP 地址没有硬性规定，但通常，子网中的最后两个 IP 地址用于此类用途。现在，将 192.168.9.253 分配给 eth0，将 192.168.9.254 分配给 eth1：

```bash
echo "Configuring eth0"
/sbin/ifconfig eth0 192.168.9.253 up

echo "Configuring eth1"
/sbin/ifconfig eth1 192.168.9.254 up
```

充当网关角色的防火墙最重要的功能是转发数据包。这是我们实现的方法：

```bash
echo "Enabling IP forwarding"
echo "1" > /proc/sys/net/ipv4/ip_forward
```

早先我们说过，防火墙还应作为 ARP 请求的代理。这意味着防火墙将回复查询你网络（192.168.9.0/24）中任何机器以太网地址的 ARP 请求。防火墙会发送被广播查询的机器（例如 192.168.9.8）的 MAC 地址吗？不会。相反，它会发送它自己的 MAC 地址，然后，当它收到发往 192.168.9.8 的数据包时，它会将数据包转发给 192.168.9.8（当然，前提是规则允许该数据包通过）。在新发行的系统中启用代理 ARP 相当容易：

```bash
echo "Enabling Proxy ARP"
echo "1" > /proc/sys/net/ipv4/conf/eth1/proxy_arp
```

接下来，在防火墙中设置路由条目。私有网络可以通过 eth0 访问，但发往公共网络的数据包应通过 eth1：

```bash
echo "Route to 192.168.9.0/24 is through eth0"
/sbin/route add -net 192.168.9.0/24 dev eth0
```

```bash
echo "The default gateway is eth1"
/sbin/route add default via eth1
```

同样，你必须告诉网络中的所有机器使用 192.168.9.253 作为默认网关（因为你必须通过网关才能访问网络外部的任何机器）。可以直接访问 LAN 机器。在你的网络中的所有机器上（显然是除了防火墙之外）执行以下操作：

```bash
echo "Add default route through the gateway"
/sbin/route add default gw 192.168.9.253 eth0
```

```bash
echo "192.168.9.0/24 is directly reachable"
/sbin/route add -net 192.168.9.0/24 dev eth0
```

接下来是防火墙规则——保护网络的规则。规则使用 iptables 工具编写。这是一个非常有用的工具，虽然有点复杂，且有一个关于各种选项的详细 man 页。iptables Netfilter 使用三个不同的内置链：INPUT、FORWARD 和 OUTPUT。数据包通过这些链遍历，因此规则是为特定链编写的。就你的防火墙而言，任何发往你的防火墙（192.168.9.253 或 192.168.9.254）的数据包都进入 INPUT 链。如果数据包旨在被转发（也就是说，它不是发给你的防火墙，且你的防火墙中有到目的地的路由），它将通过 FORWARD 链。由你的防火墙生成的任何数据包都将从该机器通过 OUTPUT 链发出。（这个简要说明适用于任何 Linux 机器。）虽然你永远不会希望防火墙转发所有通过它的数据包，但你可能想要测试上述配置下的网关功能是否正常工作。为此，将 FORWARD 链的默认策略设为 ACCEPT（使用 -P 选项）——也就是说，任何通过 forward 链的数据包都被接受：

来自网络 192.168.9.0/24 中任何机器（除了防火墙）发往网络外部任何（在线）机器的 ping 请求现在将返回 ICMP echo reply 数据包。如果外部机器不可达，可能是电缆或网卡存在问题，或者你可能错误配置了某些内容。

现在，让我们构建“墙”。设置防火墙最简单的方法是拒绝（DROP）所有类型的数据包，然后编写规则来允许（ACCEPT）那些你希望通过的数据包。所以，让我们将每个链的默认策略设置为丢弃数据包。

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

至此，你可能已经注意到，规则基本上规定了数据包必须具备的一些条件。如果匹配这些条件，则执行规则中指定的操作；否则检查链中的下一条规则，如此继续直到匹配某条规则为止。如果链中的规则均未匹配，则执行默认操作或策略（此处为 DROP）。

让我们编写第一条规则——一条允许从私有网络发出 SSH 数据包出去的规则：

```bash
echo "Allow outgoing SSH"
/sbin/iptables -A FORWARD -p TCP -i eth0 \
-s 192.168.9.0/24 -d 0.0.0.0/0 --dport 22 -j ACCEPT
```

这条规则几乎不言自明。选项 -A 指定规则要追加到的链，-p 指定协议（UDP、TCP、ICMP 等）。选项 -i 指定接收数据包的接口名称。因为发出的 SSH 数据包来自 192.168.9.0/24 网络（-s 指定源地址），它们将通过防火墙的 eth0 接口进来。SSH 流量的目标端口（-dport）是 22。目标地址由 -d 选项指示，0/0 表示任何地址。最后，匹配此类数据包的动作是 ACCEPT（由 -j 选项指定），这意味着允许匹配的数据包通过。

现在，我们编写了一条规则，允许来自 192.168.9.0/24 的 SSH 流量去往任何地方。但这行得通吗？你能从私有网络 SSH 登录到公共网络中的机器吗？我们在哪里允许来自 SSH 服务器（在公共网络中）返回到客户端（在私有网络中）的数据包？以下规则实现了这一点：

```bash
/sbin/iptables -A FORWARD -p TCP -i eth1 -s 0.0.0.0/0 \
--sport 22 -d 192.168.9.0/24 -j ACCEPT
```

这看起来很好，但我们随后需要为每种服务编写这样的规则。更糟糕的是，上面的规则做了超出需求的事情。它允许任何机器使用源端口 22 连接到私有网络。我们应该做的是追加一条规则，仅允许来自公共网络且属于由 192.168.9.0/24 网络中的机器发起的 SSH 连接的一部分的数据包。

iptables 维护状态信息以进行此类连接跟踪。维护的四种状态是 NEW、ESTABLISHED、RELATED 和 INVALID。我们在这里不详细讨论这些状态。暂时请记住，状态 NEW 表示数据包是新连接的一部分。当在相反方向看到响应数据包时，连接变为 ESTABLISHED。注意这与 TCP 连接建立过程中的状态无关。对于相应请求的 ICMP 或 UDP 回复也将标记连接为 ESTABLISHED。请参阅 iptables-tutorial.frozentux.net/iptables-tutorial.html#STATEMACHINE 以了解连接跟踪机制的确切工作原理。现在（在移除上述规则后），为了转发所有组成 ESTABLISHED 连接的一部分的数据包，我们编写以下规则：

```bash
echo "Allowing ESTABLISHED connections"
/sbin/iptables -A FORWARD -m state --state \
ESTABLISHED -j ACCEPT
```

这条规则确保只有属于 ESTABLISHED 连接的数据包才会被接受；发往 192.168.9.0/24 的新连接请求将不会被接受。理想情况下，为了访问任何服务（如 HTTP 或 FTP），我们需要仅允许 NEW 和 ESTABLISHED 连接出去（NEW 将允许第一个数据包，ESTABLISHED 将允许同一连接的所有后续数据包），并且仅允许 ESTABLISHED 连接进入私有网络。同样，如果你的网络中有一个 DNS 服务器，且需要允许外部访问（查询）它，以下规则可以做到（假设 198.168.9.1 是 DNS 服务器）：

```bash
echo "Allowing incoming DNS requests"
/sbin/iptables -A FORWARD -p TCP -i eth1 \
```

![](img/3c4d8a97b5d96c835281dc0dacbc8551_81_1.png)

