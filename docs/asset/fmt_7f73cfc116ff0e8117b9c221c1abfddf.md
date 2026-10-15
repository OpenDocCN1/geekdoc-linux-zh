
```
iptables - INPUT -p icmp --icmp-type 8 -j ACCEPT
iptables - INPUT -p icmp --icmp-type 3 -j ACCEPT
iptables - INPUT -p icmp --icmp-type 5 -j ACCEPT
iptables - INPUT -p icmp --icmp-type 6 -j ACCEPT
iptables - FORWARD -d 10.1.1.2 -p icmp --icmp-type 0 -j ACCEPT
iptables - FORWARD -d 10.1.1.2 -p icmp --icmp-type 3 -j ACCEPT
iptables - FORWARD -d 10.1.1.2 -p icmp --icmp-type 5 -j ACCEPT
iptables - FORWARD -d 10.1.1.2 -p icmp --icmp-type 8 -j ACCEPT
```

我们在 `nat` 表的 `PREROUTING` 链中添加了规则。虽然 `nat` 表不是用于包过滤的，但 `PREROUTING` 对于反伪欺骗特别有用。如果我们丢弃了 `PREROUTING` 链中的条目，它们就不出现在 `INPUT` 和 `FORWARD` 链中，因为 `PREROUTING` 链应用于所有进入防火墙的包。将条目放在一个地方比重复它们更整洁。但是，你必须注意为了性能重新排序规则不会修改功能。

```
iptables -t nat -A PREROUTING -i eth1 -s 10.0.0.0/8 -j DROP
iptables -t nat -A PREROUTING -i eth1 -s 172.16.0.0/12 -j DROP
iptables -t nat -A PREROUTING -i eth1 -s 192.168.0.0/16 -j DROP
iptables -t nat -A PREROUTING -i eth1 -s 127.0.0.0/8 -j DROP
iptables -t nat -A PREROUTING -i eth1 -s 224.0.0.0/4 -j DROP
```

最后，我们用一条禁止未显式允许的包的规则结束 `INPUT` 和 `FORWARD` 链。虽然我们已经通过 `iptables -P` 命令强制了这种行为，但 `LOG` 目标告诉我们谁在敲门。

Netfilter 为 Linux 带来的最强大的功能之一。与其允许传入的服务，连接互联网的防火墙需要允许客户端请求的传入响应。下面的有状态 `FORWARD` 链允许所有流量离开我们的网络，但仅允许由主机发起的传入流量。

```
iptables -A INPUT -i eth0 -j ACCEPT
iptables -A FORWARD -m state ESTABLISHED,RELATED -j ACCEPT
```

加载某些内核模块以便 `iptables` 跟踪 FTP 等复杂会话。如果没有加载这些模块，`iptables` 只会拒绝这些连接。虽然有状态包过滤器可以增加站点的安全性，但也增加了网络的复杂性。在防火墙中实现它之前，确保你使用了有状态功能。

调试 `iptables` 规则的最佳方法可能是使用 `iptables -v`。这些选项可以告诉你链中每条规则匹配包的次数。当我们想要有关匹配规则的包的信息时，我们通常会添加带有 `LOG` 目标的临时 `iptables` 规则。你也可以使用像 `tcpdump` 这样的包嗅探器来解决棘手的问题。

# UNIX 系统的 IPFilter

允许入站流量通过 TCP 端口 80 和 443 以及 UDP 端口 53 访问 `10.0.0.0/24` 网络。

```
block out quick all
pass in quick proto tcp from any to 10.0.0.0/24 port = 80 keep state
pass in quick proto tcp from any to 10.0.0.0/24 port = 443 keep state
pass in quick proto udp from any to 10.0.0.0/24 port = 53 keep state
block in all
```

`state`（状态）关键字值得特别关注。IPFilter 通过记录新会话的第一个包来跟踪连接。例如，当一个新包发送到 `10.0.0.10` 的 `80` 端口时，IPFilter 会在状态表中创建一个条目并允许数据包通过。它还允许来自服务器的回复，尽管第一条规则显式地阻止了所有流量。

`keep state` 对于那些不提供服务但必须发起连接的设备也有用。下面的规则集允许所有由 `192.168.10.10` 发起的会。它阻止了除已发起的连接以外的所有入站包。

```
block in quick
pass out quick from 192.168.10.10/32 to any keep state
```

`state` 关键字也适用于 UDP 和 ICMP 数据包，但由于这些协议是无状态的，其机制略显临时：IPFilter 在看到入站数据包后，会在 60 秒内允许对 UDP 或 ICMP 数据包的响应。例如，如果一个来自 `10.0.0.10`（端口 `32000`）的 UDP 包目标是 `192.168.10.10`（端口 `53`），则 UDP 回复在 60 秒内将是允许的。同样，在回显请求进入状态表后，ICMP 回显应答（ping 响应）也将是允许的。

网络地址转换 (`NAT`) 是 IPFilter 提供的另一个功能。`NAT` 让具有 RFC1918 私有 IP 地址的大型网络能够通过一组较小的互联网可路由 IP 地址连接到互联网。`NAT` 设备将私有网络映射到一个多个公共地址，跨越互联网发送请求，并拦截响应根据 IP 地址对其进行重写。

IPFilter 使用 `map` 关键字（代替 `pass` 和 `block`）来提供 `NAT` 服务。在以下规则中，`10.0.0.0/24` 网络映射到 `e1000g` 接口上的当前地址。

```
map e1000g 10.0.0.0/24 -> 0/32
```

如果 `e1000g` 的地址发生变化，必须重新加载过滤器，例如当 `e1000g` 通过 DHCP 租用动态 IP 地址可能会发生这种情况。因此，IPFilter 的 `NAT` 功能最好在面向互联网接口具有静态 IP 地址的站点使用。

有关私有地址和 `NAT` 的更多信息，请参阅第 462 页。

# 第22 章 安全

IPFilter 规则灵活且可配置。宏（macros）等高级功能可以显著简化规则文件。关于这些高级功能的详细信息，请访问 IPFilter 官方网站：`coombs.anu.edu.au/~avalon`。

IPFilter 软件包包含几个命令，如表 22.5 所示。

# 表 22.5 IPFilter 命令

| Cmd | Function |
| --- | --- |
| `ipf` | 管理规则和过滤器列表 |
| `ipstat` | 获取数据包过滤统计信息 |
| `ipmon` | 监控记录的过滤器信息 |
| `ipnat` | 管理 NAT 规则 |

表 22.5 中的命令中，`ipf` 是最常用的。`ipf` 接受规则作为输入，并将正确解析的规则添加到内核列表中。`ipf` 将规则添加到文件的末尾，除非使用 `-f`，它会刷新所有现有规则。例如，为了刷新内核现有的过滤器并加载来自 `ipf.conf` 的规则，使用以下语法：

```
solar$ ipf -f /etc/ipf.conf
```

IPFilter 依赖于伪文件进行访问控制，默认情况下只有 root 可以编辑列表。我们建议使用 `ipf -s -v` 标志在加载规则时调试错误和其他问题。

![](img/579efec8c6772f31ecf3484bbb990.png)

# 22.14 虚拟专用网络 (VPN)

在最简单的形式下，VPN 是让远程网络看起来像直接连接的一样的连接，即使它们物理上相隔数千英里。为了增加安全性，连接不仅通过某种方式身份验证（通常是共享密码），而且端端流量还被加密。这种安排通常被称为“安全隧道”。

这是一个 VPN 有用的良好例子：假设一家公司在芝加哥、波尔德和迈阿密设有办公室。如果每个办公室都有本地 ISP 连接，公司可以使用 VPN 透明地（在大多数情况下是安全地）跨越互联网连接办公室。

## 需要 VPN 吗？

公司通过租用专用线路连接办公室也可以获得类似的结果，但会贵得多。

由于 VPN 的便利性和流行，每个人都从路由器供应商处购买某种 VPN 解决方案，让操作系统看起来是直接连接到公司网络。根据你的预算和扩展性需求，你可能需要考虑商业 VPN 解决方案。

## IPsec 隧道
