

# Nat 目标与链

此外，还有两种类型的 NAT 操作：源 NAT，指定为 SNAT 目标，以及目标 NAT，指定为 DNAT 目标。SNAT 目标用于更改源地址的规则，而 DNAT 目标用于更改目标地址的规则。

内核用于 NAT 操作的 NAT 表中有三条链。这些是 PREROUTING、POSTROUTING 和 OUTPUT。PREROUTING 用于目标 NAT（DNAT）规则。这些是到达的数据包。POSTROUTING 用于源 NAT（SNAT）规则。这些是离开的数据包。OUTPUT 用于本地生成数据包的目标 NAT 规则。

与数据包过滤一样，您可以指定源（-s）和目标（-d）地址，以及输入（-i）和输出（-o）设备。-j 选项将指定 MASQUERADE 等目标。您可以通过向 POSTROUTING 链添加 MASQUERADE 规则来实现 IP 伪装：

```
# iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

要更改离开系统的包的源地址，您将使用带有 SNAT 目标的 POSTROUTING 规则。对于 SNAT 目标，您使用 --to-source 选项指定源地址：

```
# iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source 192.168.0.4
```

要更改到达系统的包的目标地址，您将使用带有 DNAT 目标和 --to-destination 选项的 PREROUTING 规则：

```
# iptables -t nat -A PREROUTING -i eth0 \
-j DNAT --to-destination 192.168.0.3
```

指定端口可让您更改特定端口到达的数据包的目标。实际上，这使您可以实现端口转发。在下一个示例中，每个到达端口 80（Web 服务端口）的数据包都被重定向到 10.0.0.3，在本例中它将是运行 Web 服务器的系统。

```
# iptables -t nat -A PREROUTING -i eth0 -dport 80 \
-j DNAT --to-destination 10.0.0.3
```

使用 TOS 和 MARK 目标，您可以修改数据包以控制其路由或优先级。TOS 目标设置数据包的服务类型，可以使用正常服务、最小化成本、最大化吞吐量等标准来设置优先级。

仅对 NAT 表有效的目标如下所示：

| SNAT | 修改源地址，使用 --to-source 选项指定新的源地址。 |
| DNAT | 修改目标地址，使用 --to-destination 选项指定新的目标地址。 |
| REDIRECT | 重定向数据包。 |
| MASQUERADE | IP 伪装。 |
| MIRROR | 反转源和目标并发送回发送者。 |
| MARK | 修改 Mark 字段以控制消息路由。 |

## Nat 重定向：透明代理

NAT 表可用于实现任何类型的包重定向，该过程对用户是透明的。重定向通常用于实现透明代理。数据包的重定向是通过 REDIRECT 目标完成的。使用透明代理时，接收到的数据包可以自动重定向到代理服务器。例如，到达 Web 服务端口 80 的数据包可以重定向到 Squid 代理服务端口，通常为 3128。这涉及使用 PREROUTING 链上的 REDIRECT 目标重定向数据包的命令：

```
# iptables -t nat -A PREROUTING -i eth1 --dport 80 -j REDIRECT --to-port 3128
```

## 数据包修改：Mangle 表

数据包修改表用于实际修改数据包信息。专门应用于此表的规则通常旨在控制数据包的平凡行为，如路由、连接大小和优先级。实际修改数据包而不是简单地重定向或停止它的规则只能在 mangle 表中使用。例如，TOS 目标可直接在 mangle 表中使用以更改服务类型字段以修改数据包的优先级。TCPMSS 目标可以设置为控制连接的大小。ECN 目标可让您绕过 ECN 黑洞，DSCP 目标可让您更改 DSCP 位。ROUTE 扩展等多个扩展将更改数据包，在本例中重写其目标，而不是简单地重定向它。

mangle 表由 -t mangle 选项指示。使用以下命令查看 mangle 表中列出了哪些链：

```
iptables -t mangle -L
```

以下是几个 mangle 表目标。

| TOS | 修改服务类型字段以管理数据包的优先级。 |
| TCPMSS | 修改连接允许的数据包大小，从而实现更大的传输。 |
| ECN | 删除 ECN 黑洞信息。 |
| DSCP | 更改 DSCP 位。 |
| ROUTE | 扩展 TARGET 以修改数据包中的目标信息。 |

> 注意 iptables 包设计为可扩展，允许轻松添加自定义目标。这涉及对内核应用补丁并重新构建它。有关更多详细信息，请参阅 www.netfilter.org，同时列出扩展目标。

