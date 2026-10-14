

然而你也希望允许主机与外部世界进行连接。

```
# ipchains -A input -j ACCEPT -p tcp '! ' -y
```

表示允许响应数据包通过。

此规则允许使用 ICMP 工具如 ping 和 traceroute（以及其他）：

```
# ipchains -A input -j ACCEPT -p icmp
```

Linux 的某些部分如果机器无法与自身通信就会出现问题：

```
# ipchains -A input -j ACCEPT -d localhost
```

由于我们对 ssh 有一定信任，因此允许该端口的连接。

```
# ipchains -A input -j ACCEPT -p tcp -d 10.1.1.2 ssh
```

一切都已就位，只有一个例外，如果你使用 FTP 代理则不是必要的。由于其设计，FTP 会回连到 FTP 客户端机器。下一行提供到外部世界的直接 FTP 连接：

```
# ipchains -A input -j ACCEPT -p tcp -s any/0 ftp-data -d 10.1.1.2 1024:
```

由于你通常希望拒绝大部分内容，将默认策略设置为 DENY。你可能希望在放置其他规则之后再执行此操作，因为内核在你声明之后就会丢弃所有内容，而你可能需要 DNS 来处理其他一些规则。

```
# ipchains -P input DENY
```

然而，如果你感觉非常偏执，你会希望先设置此项并以 IP 地址或无需 DNS 的方式指定所有内容。

## Example 2: IP Firewall

现在让我们修改上面的示例，使其成为网络 10.1.20.0/255.255.255.0 的防火墙。假设你已经使接口正常工作。

如果尚未启用，请打开转发（你可能希望最后再做）：

```
# echo 1 > /proc/sys/net/ipv4/ip_forward
```

为转发设置默认策略为 DENY：

```
# ipchains -P forward DENY
```

接受来自 10.1.20.0 到外部世界的任何输入（包括防火墙机器本身）和转发：

```
# ipchains -A input -s 10.1.20.0/255.255.255.0 -d any -j ACCEPT
# ipchains -A forward -s 10.1.20.0/255.255.255.0 -d any -j ACCEPT
# ipchains -A forward -j ACCEPT -p tcp '! ' -y
```

然后允许从任何地方到防火墙内部的 ssh 连接：

```
# ipchains -A input -s any ssh -d 10.1.20.0/255.255.255.0 -j ACCEPT
# ipchains -A forward -s any ssh -d 10.1.20.0/255.255.255.0 -j ACCEPT
```

## PROBLEM 11

症状：你的防火墙机器容易受到攻击。
问题：虚假的安全感。
修复：不要让防火墙机器接受来自外部世界任何东西在任意端口上的连接。如果防火墙机器可以毫无问题地访问网络的任何部分，那么入侵者只需攻破防火墙即可进入“安全”网络。不要期望防火墙有完美的安全性（来自外部或内部的攻击）；保持所有机器更新到最新的安全修复。

## Example 3: IP Masquerading

IP 伪装是小型网络的便捷功能，例如家庭网络共享一条拨号连接而没有专用 IP 子网。其他系统称之为 NAT（网络地址转换）。在 IP 伪装中，一台连接互联网的机器充当本地网络上其他机器的默认互联网网关（即使它们使用 ISP 的动态地址分配）。当与代理服务（例如 squid，一种 Web 代理服务器——参见第 4 章）结合使用时，IP 伪装甚至可以通过高效缓存来提高性能。然而，它并不适用于所有协议；对 TCP 最有效。

以典型的家庭网络为例。其第一个本地子网是 10.1.1.0，子网掩码设置为 255.255.255.0。其主要网络硬件是一个 100BaseT 以太网集线器，Linux 工作站、笔记本、Power Mac G3 以及 Linux 路由器/网关都连接到该集线器。网关的以太网接口（eth0）设置为地址 10.1.1.1，并在 ppp0 接口上配置为 PPP。

命令

```
# ipchains -P forward DENY
# ipchains -A forward -i ppp0 -j MASQ
# echo 1 > /proc/sys/net/ipv4/ip_forward
```

启动了伪装——第一条命令拒绝通用路由，第二条命令表示所有通常通过 ppp0 接口路由的数据包应改为伪装，最后一条命令在内核中启用 IP 转发。

为了完成工作，我们将网络上其余机器的默认网关地址设置为 10.1.1.1（这些机器的地址例如为 10.1.1.4）。

### Adding Kernel Support

除了 ipchains 命令之外，你的系统还需要添加对 IP 伪装的内核支持，你可以在内核配置中（至少对于版本 2.2——有关如何构建内核的详细信息请参见第 7 章）找到它，位于几项之下。在配置内核时，请记住在配置菜单中按以下步骤操作：

- 1. 在 Networking options 下，选择 Network firewalls。
- 2. 向下移动几行并选择 IP: Firewalling（这仅在你选择 Network firewalls 后出现）。
- 3. 向下移动几行并选择 IP: Always defragment（伪装所需）。
- 4. 选择 IP: Masquerading（这应与 IP: Firewalling 一起弹出）。
- 5. 在你的选项中包含 IP: ICMP masquerading——它启用了一些诊断工具，如 ping 和 traceroute。

上述过程对于一个本地子网来说效果很好，但假设我们有两个。为了让我们的古老 NeXT 和一些其他玩具连接起来——并且因为我们太吝啬而不愿购买双速集线器——我们有一个用于子网 10.1.2.0（网络掩码 255.255.255.0）的 10BaseT 以太网集线器。网关有一个额外的以太网接口 eth1，插入较慢的集线器并运行在地址 10.1.2.1。在为该子网上机器设置默认网关为此地址后，我们使用 ipchains 命令：

```
# ipchains -I forward -b -s 10.1.1.0/255.255.255.0 -d 10.1.2.0/255.255.255.0 -j ACCEPT
```

此命令允许两个本地子网之间的流量无需额外设置。-b 选项添加两条规则；我们也可以使用以下方式实现相同效果

```
# ipchains -I forward -s 10.1.1.0/255.255.255.0 -d 10.1.2.0/255.255.255.0 -j ACCEPT
# ipchains -I forward -s 10.1.2.0/255.255.255.0 -d 10.1.1.0/255.255.255.0 -j ACCEPT
```

最终结果具有此列表（24 作为网络掩码与 255.255.255.0 相同；它是子网掩码中置为 1 的前导位数）。我们将使用 -L（list）如第 34 页所述的 ipchains 其他参数。

