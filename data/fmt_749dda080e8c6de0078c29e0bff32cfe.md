
```
#iptables -A INPUT -i eth0 -p udp -s any/0 1024:65535 -d MY.NET.IP.ADDR 53 -j ACCEPT
#iptables -A INPUT -i eth0 -p tcp -s any/0 1024:65535 -d MY.NET.IP.ADDR 53 -j ACCEPT
#iptables -A INPUT -i eth0 -p udp -s any/0 --port 1024:65535 -d MY.NET.IP.ADDR
--port 53 -j ACCEPT
#iptables -A INPUT -i eth0 -p tcp -s any/0 --port 1024:65535 -d MY.NET.IP.ADDR
--port 53 -j ACCEPT
```

## Telnet

使用此规则允许来自特定 IP 地址的入站 telnet 连接：

```
#ipchains -A input -i eth0 -p tcp -s 209.100.100.10 1024:65535
-d MY.NETWORK.IP.ADDR 23 -j ACCEPT
iptables -A INPUT -i eth0 -p tcp -s 209.100.100.10 --sport 1024:65535
-d MY.NETWORK.IP.ADDR --dport 23 -j ACCEPT
```

在此示例中，我们只允许使用 IP 地址 209.100.100.10 的客户端计算机通过 telnet 访问系统。你可以更改客户端计算机的 IP 地址并输入此命令，以便允许额外的客户端计算机 telnet 访问。

## SSH

使用此规则允许 SSH 连接：

```
iptchains -A input -i eth0 -p tcp -s 209.200.200.10 22:65535
-d MY.NETWORK.IP.ADDR 22 -j ACCEPT
iptables -A INPUT -i eth0 -p tcp -s 209.200.200.10 --sport 22:65535
-d MY.NETWORK.IP.ADDR --dport 22 -j ACCEPT
```

再次，将示例地址 209.200.200.10 替换为你想要允许的 IP 地址，并为每个需要 SSH 访问的 IP 地址重复该命令。SSH 守护进程（`sshd`）在端口 22 上监听传入请求。

## Email

使用此规则允许发送电子邮件消息：

```
iptchains -A input -i eth0 -p tcp ! -y -s EMAIL.IP.ADDR 25
-d MY.NETWORK.IP.ADDR 1024:65535 -j ACCEPT
iptables -A INPUT -i eth0 -p tcp ! -y -s EMAIL.IP.ADDR --sport 25
-d MY.NETWORK.IP.ADDR --dport 1024:65535 -j ACCEPT
```

此简单邮件传输协议 (SMTP) 规则用于我们连接到远程 SMTP 服务器进行外发邮件交付。此命令引入了 `! -y` 语法，这是一种额外的安全性，可以确认进入的数据包确实是我们发送出去的数据包。

`! -y` 语法表示数据包头中必须设置确认标志位，该数据包是对我们发送出去的数据包的确认。（我们正在发送电子邮件，所以我们启动了 SMTP 会话）。

此规则将不允许入站邮件消息到达服务器上的 `sendmail` 服务。如果你正在构建一个电子邮件服务器或能够处理入站邮件消息的服务器（例如执行邮件订单输入处理的集群节点），你必须允许进入端口 25 的入站数据包（不使用确认标志）。

## HTTP

使用此规则允许来自任何地方的入站 HTTP 连接：

```
#ipchains -A input -i eth0 -p tcp -d MY.NETWORK.IP.ADDR 80 -j ACCEPT
iptables -A INPUT -i eth0 -p tcp -d MY.NETWORK.IP.ADDR --dport 80 -j ACCEPT
```

要允许 HTTPS（安全）连接，你还需要以下规则：

```
#ipchains -A input -i eth0 -p tcp -d MY.NETWORK.IP.ADDR 443 -j ACCEPT
iptables -A INPUT -i eth0 -p tcp -d MY.NETWORK.IP.ADDR --dport 443 -j ACCEPT
```

## ICMP

使用此规则允许 Internet 控制消息协议（ICMP）响应：

```
ipchains -A input -i eth0 -p icmp -d MY.NETWORK.IP.ADDR -j ACCEPT
iptables -A INPUT -i eth0 -p icmp -d MY.NETWORK.IP.ADDR -j ACCEPT
```

此命令将允许所有 ICMP 消息，除非你在 Linux 机器和互联网之间具有正确定义 ICMP 过滤规则的防火墙，否则你不应该这样做。查看命令 `iptables -p icmp -h`（或 `ipchains icmp -help`）的输出以确定启用哪些 ICMP 消息。仅从你知道需要的开始。例如，你可能应该允许 MTU 发现。

## 检查并保存你的规则

要查看你创建的规则，输入：

```
ipchains -L -n
iptables -L -n
```

要将 Red Hat 上的 `iptables` 规则保存到 `/etc/sysconfig/iptables` 文件中，以便它们在每次系统启动时生效，请输入：

```
#/etc/init.d/iptables save
```

注意 命令 `service iptables save` 同样有效。

然而，如果你使用 Red Hat 提供的这种方法保存规则，你将无法将它们作为高可用资源使用。6 如果集群均衡器使用复杂的 `iptables` 来过滤网络数据包，或者更可能的，针对某些数据包头进行特殊处理。7 那么这些规则可能一次仅位于一台机器（负载均衡器）上。8 如果是这种情况，`iptables` 规则应该放在像本章末尾那样的脚本中，并按照书中第二部分所述配置为高可用资源。

## 使用 Linux 内核路由数据包

如图 2-2 和 2-3 所示，所有入站和出站网络数据包必须通过内核的路由规则。与 `iptables` 链中的规则列表一样，路由规则列表包含在一个有序列表中，该列表会被检查直到数据包匹配规则之一。

与 `iptables` 链中的规则一样，每条路由规则都包含：

- 用于匹配数据包的标准

- 告诉内核如何处理匹配此标准的数据包的指令

路由表的顺序很重要，因为当数据包匹配其中一条规则时，内核就会停止搜索。由于路由表中的最后一条规则通常会匹配任何数据包，因此它被称为默认路由（或默认网关）。

当你为其中一个网卡分配 IP 地址时，内核会自动为该接口添加路由规则。内核构建路由条目，以便匹配所有目的地址落在所连接网络或子网允许的 IP 地址范围内的数据包。

在典型配置中，构建的路由表条目将根据数据包的目的 IP 地址匹配数据包。这种类型的数据包通常匹配：

- 特定的目标网络

- 特定的目标主机

- 任何目标或主机

在以下章节中，`route` 命令的参数添加路由规则。要在添加后删除或移除路由规则，请使用相同的命令将参数更改为 `del`。

> 6 这种标准的 Red Hat `iptables` 脚本在带有状态参数运行时，不会返回 Heartbeat 程序可以理解的内容。有关此主题的进一步讨论，请参阅本章末尾的示例脚本。

> 7 使用 Netfilter 标记数据包将在第 14 章介绍。

> 8 这将位于 LVS-DR 集群中，该集群能够将负载均衡服务故障到集群内部的一个真实服务器上。参见第 15 章。

> 9 一个能够将负载均衡服务故障到集群内部的一个真实服务器上的 LVS-DR 集群。参见第 15 章。

## 匹配特定目标网络的数据包

如果我们必须输入命令为连接到 209.100.100.0 网络的 NIC 添加路由表条目，命令将如下（我们不需要，因为内核会自动为我们完成）：

```
#/sbin/route add --net 209.100.100.0 netmask 255.255.0.0 dev eth0
```

此命令添加路由表条目以匹配所有发往 209.100.100.0 网络的数据包，并将其通过 `eth` 接口发送。

如果我们有一个名为 `eth1` 的 NIC 连接到 172.24.150.0 网络，我们将使用以下命令：

```
#/sbin/route add --net 172.24.150.0 netmask 255.255.255.0 dev eth1
```

有了这两条规则，内核就可以向或从连接到这两个网络之一的任何主机发送和接收数据包。如果这台机器需要转发源自这些网络之一的数据包，你必须使用以下命令启用内核的转发：

```
echo 1 > /proc/sys/ipv4/ip_forward
```

## 匹配特定目标主机的数据包
