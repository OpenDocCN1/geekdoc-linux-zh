

# 阻止外部发起的连接
```
iptables -A INPUT -m state --state NEW -i eth0 -j DROP
iptables -A FORWARD -m state --state NEW -i eth0 -j DROP
```

## 本地网络访问

要允许内部网络与防火墙进行交互，你允许在内部以太网连接 eth1 上的所有数据包输入。有效的内部网络地址被指定为输入源：

```
iptables -A INPUT -j ACCEPT -p all -i eth1 -s 192.168.0.0/24
```

## 伪装本地网络

为了实现伪装，使私有网络上的系统可以使用网关的 Internet 地址连接到 Internet 主机，你创建一个 NAT 表 (-t nat) POSTROUTING 规则，使用 MASQUERADE 目标：

```
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

## 控制 ICMP 数据包

此外，为了允许 ping 和目标可达 ICMP 数据包，你输入以防火墙为目的地的 INPUT 规则。为了启用 ping 操作，你同时使用 echo-reply 和 echo-request ICMP 类型，对于目标不可达，你使用 destination-unreachable 类型：

```
iptables -A INPUT -j ACCEPT -p icmp -i eth0 --icmp-type \
echo-reply -d 10.0.0.1
iptables -A INPUT -j ACCEPT -p icmp -i eth0 --icmp-type \
echo-request -d 10.0.0.1
iptables -A INPUT -j ACCEPT -p icmp -i eth0 --icmp-type \
destination-unreachable -d 10.0.0.1
```

最后，IP 转发再次打开：

```
echo 1 > /proc/sys/net/ipv4/ip_forward
```

## 列出规则

列出这些 iptables 选项会显示每个选项的不同规则，如下所示：

```
# iptables -L
Chain INPUT (policy DROP)
target     prot opt source               destination
LOG        all  --  !192.168.0.0/24      anywhere                   LOG level warning
DROP       all  --  !192.168.0.0/24      anywhere
DROP       all  --  192.168.0.0/24       anywhere
DROP       all  --  127.0.0.0/8          anywhere
ACCEPT     all  --  anywhere             anywhere
ACCEPT     tcp  --  10.0.0.2              anywhere                   tcp dpt:http
ACCEPT     tcp  --  10.0.0.2              192.168.0.0/24            state RELATED,ESTABLISHED
                                                                     tcp spt:http
ACCEPT     icmp --  anywhere             anywhere                   state RELATED,ESTABLISHED
DROP       all  --  anywhere             anywhere                   state NEW
ACCEPT  all  --  192.168.0.0/24  anywhere
ACCEPT  icmp --  anywhere  10.0.0.1  icmp echo-reply
ACCEPT  icmp --  anywhere  10.0.0.1  icmp echo-request
ACCEPT  icmp --  anywhere  10.0.0.1  icmp destination-unreachable
Chain FORWARD (policy ACCEPT)
target  prot opt source      destination
DROP    all  --  !192.168.0.0/24  anywhere
DROP    all  --  192.168.0.0/24  anywhere
DROP    all  --  127.0.0.0/8  anywhere
DROP    all  --  anywhere  anywhere  state NEW

Chain OUTPUT (policy ACCEPT)
target  prot opt source      destination
DROP    tcp  --  anywhere  192.168.0.0/24  state NEW tcp spt:http

# iptables -t nat -L
Chain PREROUTING (policy ACCEPT)
target  prot opt source      destination
Chain POSTROUTING (policy ACCEPT)
target  prot opt source      destination
MASQUERADE  all  --  anywhere  anywhere
Chain OUTPUT (policy ACCEPT)
target  prot opt source      destination
```

## 用户自定义规则

对于更复杂的规则，你可能希望创建自己的链以减少重复。常见的方法是为 INPUT 和 FORWARD 链同时定义一个用户链，这样你就不必为每个链重复 DROP 操作。相反，你将只有一个用户链，FORWARD 和 INPUT 链都将为 DROP 操作馈入该链。请记住，FORWARD 和 INPUT 操作除了它们共享的规则外，还可能有单独的规则。在下一个示例中，创建了一个名为 arriving 的用户定义链。该链在脚本顶部使用 -N 选项定义：

```
iptables -N arriving
```

用户链必须在用作其他规则的目标之前定义。因此，你必须先定义并添加该链的所有规则，然后再将其用作目标。arriving 链首先被定义并添加其规则。然后，在文件末尾，它被用作 INPUT 和 FORWARD 链的目标。INPUT 链列出用于接受数据包的规则，而 FORWARD 链具有 ACCEPT 策略，默认情况下将接受它们。

```
iptables -N arriving
iptables -F arriving
# IP 欺骗，拒绝内部网络上具有外部源地址的任何数据包。
iptables -A arriving -j LOG -i eth1 ! -s 192.168.0.0/24
iptables -A arriving -j DROP -i eth1 ! -s 192.168.0.0/24
iptables -A arriving -j DROP ! -i eth1 -s 192.168.0.0/24
................
# 脚本末尾的条目
iptables -A INPUT -j arriving
iptables -A FORWARD -j arriving
```
