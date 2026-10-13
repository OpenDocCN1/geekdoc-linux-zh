
看一些如何使用 iptables 命令配置防火墙的示例。 一个不错的入门步骤是查看当前配置，使用以下命令：

```
# iptables -L
```

如果 iptables 配置正确，它应返回三个不同类别的链规则：INPUT、FORWARD 和 OUTPUT。

以下规则拒绝来自 192.168.75.0 子网的所有流量，并向尝试连接的该网络地址的任何客户端发送“目标不可达”错误消息：

```
# iptables -A INPUT -s 192.168.75.0/24 -j REJECT
```

此规则阻止 IP 地址为 192.168.25.200 的计算机上的用户“ping”你的系统，因为 ping 命令使用 ICMP 协议：

```
# iptables -A INPUT -s 192.168.25.200 -p icmp -j DROP
```

以下命令可防止来自本地系统外部的 TCP SYN 攻击，与数据包洪泛和拒绝服务攻击相关。 假设待保护的局域网的 IP 地址为 192.168.1.0。 感叹号 (!) 会反转含义； 在这种情况下，该命令适用于所有 IP 地址，除了具有 192.168.1.0 网络地址（以及 255.255.255.0 子网掩码）的地址。

> SYN 并不是缩写，而是一种由客户端使用 TCP 发送的数据包类型。 响应是 SYN-ACK 数据包，即确认。 然后客户端向服务器发送 ACK 消息。 相关的 iptables 规则在 SYN 级别阻止潜在攻击。

```
# iptables -A INPUT -s !192.168.1.0/24 -p tcp -j DROP
```

然后，如果你想删除此列表中与 ping 命令相关的规则，请使用以下命令：

```
# iptables -D INPUT -s 192.168.25.200 -p icmp -j DROP
```

INPUT、OUTPUT 和 FORWARD 的默认规则是接受所有数据包。 停止数据包转发的其中一种方法是添加以下规则：

```
# iptables -A FORWARD -j DROP
```

## 默认防火墙

现在你已经看到了各种防火墙规则的效果，是时候查看 RHEL 6 的默认防火墙了，该防火墙基于第 1 章和第 2 章中安装的 VM 系统。 虽然你可以使用 iptables -L 命令来实现该目的，但在启动过程中实现的防火墙规则存储在 /etc/sysconfig/iptables 文件中。 （对于 IPv6 网络，对应的防火墙配置文件是 /etc/sysconfig/ip6tables。） 这些行的含义在第 4 章中描述。

## 来自 NSA 的建议

简单的防火墙通常是最安全的。 在考试中，最好将一切，包括防火墙，保持尽可能简单。 但 NSA 会更进一步。 它对默认规则、ping 命令的限制以及来自可疑 IP 地址组的阻止提出了建议。 对于这些建议，我还添加了几条以降低 SSH 系统的风险，这些建议可能适用于其他服务。 虽然这些建议超出了 RHCE 目标的建议，但请阅读本节。 如果你对 iptables 命令不太熟悉，本节可以帮助你。

要在多个系统上实施这些更改，最有效的方法是直接编辑 /etc/sysconfig/iptables 文件。 虽然你可以使用防火墙配置工具中的自定义规则选项来实现这些更改，但这不如直接编辑所述文件的脚本高效。 不幸的是，防火墙配置工具会覆盖任何此类更改。 因此，如果你使用脚本在多个系统上管理防火墙，请务必备份该 /etc/sysconfig/iptables 文件。 然而，如果你只是为一两个系统更改防火墙，防火墙配置工具中的自定义规则选项是极好的选择。

> **考试提示**
> 
> *对基于 iptables 的防火墙的建议更改只是建议。 然而，由于“实现数据包过滤”的要求是通用的，因此研究各种示例是有用的。*

然后，你可以在像第 2 章中创建的 server1.example.com VM 这样的系统上测试这些建议中的任何一个。 为此，请编辑 /etc/sysconfig/iptables 文件。 然后要使这些更改生效，请运行以下命令：

```
# /etc/init.d/iptables restart
```

## 对默认规则的建议更改

它建议对堡垒服务器（如本书早期配置的 VM）适当的默认规则更改。 默认值为

```
:INPUT ACCEPT [0:0]
:FORWARD ACCEPT [0:0]
```

NSA 的建议会将其更改为

```
:INPUT DROP [0:0]
:FORWARD DROP [0:0]
```

虽然允许网络流量进入系统的规则仍然适用，但这些更改为进入系统的流量以及可能转发到另一系统的流量提供了另一层限制。

只是要小心。 当我在网关系统上尝试这些更改时，具体来说是我的 VM 的物理主机系统，它通过丢弃 VM 与外部网络之间的数据包来停止通信。 我本应将此类更改限制在 VM 上。 因此，在生产系统上实施任何更改之前，请先测试它们。

## 限制 ping 命令

针对各种互联网系统的早期攻击之一涉及 ping 命令。 从 Linux 开始，可以使用 -f 开关泛洪另一个系统。 它可能每秒传输数千个数据包。 能够防御此类攻击非常重要，因为它们可能会阻止其他人访问你的网站等。

![](img/9139201cfcaf4292284a0eed074928e5_571_0.png)

> 对 ping 命令的 -f 开关的描述仅是为了指出网络上的主要风险之一。 在许多情况下，在他人的系统上或针对他人的系统运行此类命令是非法的。 例如，一篇维基百科文章建议此类攻击可能违反英国的警察和司法法，最高可判处十年监禁。 其他国家也存在类似法律。

默认防火墙中一个可能有问题的规则是

```
-A INPUT -p icmp -j ACCEPT
```

然而，ICMP 消息是双向的。 如果你在远程系统上运行 ping 命令，远程系统会使用 ICMP 数据包进行响应。 因此，如果你想限制 ICMP 消息，以下规则允许对 ping 的“可接受”响应：

```
-A INPUT -p icmp --icmp-type echo-reply -j ACCEPT
-A INPUT -p icmp --icmp-type destination-unreachable -j ACCEPT
-A INPUT -p icmp --icmp-type time-exceeded -j ACCEPT
```

以下规则限制了 ping 命令可应用于系统的速率：

```
-A INPUT -p icmp --icmp-type echo-request -m limit --limit 1/s -j ACCEPT
```

虽然本章后面讨论的防火墙配置工具可以在大多数相同的方式下限制 ICMP 消息的影响，但它没有调节系统接受的 ping 网络数据包速率的能力。

## 阻止可疑 IP 地址

想要入侵系统的黑客可能会隐藏其源 IP 地址。 由于没有人应该在公共互联网上使用私有、多播或实验性 IPv4 地址，因此此类地址是隐藏的一种方式。 以下对 /etc/sysconfig/iptables 文件的添加将丢弃来自指定 IPv4 网络地址块的数据包：

```
-A INPUT -i eth0 -s 10.0.0.0/8 -j DROP
-A INPUT -i eth0 -s 172.16.0.0/12 -j DROP
-A INPUT -i eth0 -s 192.168.0.0/16 -j DROP
-A INPUT -i eth0 -s 224.0.0.0/4 -j DROP
-A INPUT -i eth0 -s 240.0.0.0/5 -j DROP
```

## 限制对 SSH 的访问

由于 SSH 是管理远程系统的重要手段，保护此类服务需要额外的措施。 当然，可以为 SSH 通信设置非标准端口。 这种措施可以作为分层安全策略的一部分。 然而，像 nmap 这样的工具可以检测此类非标准端口上的 SSH 使用情况。 因此，通常最好按照第 11 章中讨论的方式设置 SSH 服务器的配置，并配合以下防火墙规则。 这里显示的第一个规则为所有到端口 22 的 TCP 流量创建一个新的链 SSH_CHAIN：

```
-A INPUT -i eth0 -p tcp -m tcp --dport 22 -m state --state NEW -j SSH_CHAIN
```

下一条规则启动 SSH_CHAIN，通过将访问请求限制为每分钟三次。

```
-A SSH_CHAIN -i eth0 -p tcp -m tcp --dport 22 -m state --state NEW -m recent
--update --seconds 60 --hitcount 3 --rttl --name SSH -j DROP
```
