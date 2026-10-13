
`-A INPUT -p icmp --icmp-type time-exceeded -j ACCEPT`

以下规则限制了 `ping` 命令可应用于系统的速率：

```
-A INPUT -p icmp --icmp-type echo-request -m limit --limit 1/s -j ACCEPT
```

虽然本章后面讨论的防火墙配置工具可以在大多数相同的方式下限制 ICMP 消息的影响，但它没有调节系统接受的 `ping` 网络数据包速率的能力。

## 阻止可疑 IP 地址

想要入侵系统的黑客可能会隐藏其源 IP 地址。 由于没有人应该在公共互联网上使用私有、多播或实验性 IPv4 地址，因此此类地址是隐藏的一种方式。 以下对 `/etc/sysconfig/iptables` 文件的添加将丢弃来自指定 IPv4 网络地址块的数据包：

```
-A INPUT -i eth0 -s 10.0.0.0/8 -j DROP

-A INPUT -i eth0 -s 172.16.0.0/12 -j DROP

-A INPUT -i eth0 -s 192.168.0.0/16 -j DROP

-A INPUT -i eth0 -s 224.0.0.0/4 -j DROP

-A INPUT -i eth0 -s 240.0.0.0/5 -j DROP
```

## 限制对 SSH 的访问

由于 SSH 是管理远程系统的重要手段，保护此类服务需要额外的措施。 当然，可以为 SSH 通信设置非标准端口。 这种措施可以作为分层安全策略的一部分。 然而，像 `nmap` 这样的工具可以检测此类非标准端口上的 SSH 使用情况。 因此，通常最好按照第 11 章中讨论的方式设置 SSH 服务器的配置，并配合以下防火墙规则。 这里显示的第一个规则为所有到端口 22 的 TCP 流量创建一个新的链 `SSH_CHAIN`：

```
-A INPUT -i eth0 -p tcp -m tcp --dport 22 -m state --state NEW -j SSH_CHAIN
```

下一条规则启动 `SSH_CHAIN`，通过将访问请求限制为每分钟三次。

```
-A SSH_CHAIN -i eth0 -p tcp -m tcp --dport 22 -m state --state NEW -m recent
--update --seconds 60 --hitcount 3 --rttl --name SSH -j DROP
```

## 确保防火墙正在运行

一旦将所需的更改保存到 `/etc/sysconfig/iptables` 配置文件中，就很重要确保防火墙正在运行，并使用新的规则。由于 `/etc/init.d/iptables` 脚本中没有 `reload` 选项，您需要使用以下命令执行此操作：

> exam Watch
> *了解如何保护 Red Hat Enterprise Linux 系统免受未经授权访问至关重要。*

```
# service iptables restart
```

如第 11 章所述，这在功能上等同于 `/etc/init.d/iptables restart` 命令。

## IP 伪装

Red Hat Enterprise Linux 支持一种称为 IP 伪装的 NAT 变体。IP 伪装支持多台计算机使用单个公共 IP 地址访问 Internet。IP 伪装将多个内部 IP 地址映射到该单个有效的外部 IP 地址。这有所帮助，因为所有公共 IPv4 地址现已分配完毕。虽然这些第三方通常仍以价格提供 IPv4 地址。这项成本是 IP 伪装的又一个原因。另一方面，IPv6 网络上的系统可能不需要伪装，因为对于许多请求用户来说，获取自己的公共 IPv6 地址子网相对容易。尽管如此，即使在 IPv6 网络上，伪装也有助于保持系统安全。

> exam Watch
> *RHCE 目标规定使用 iptables 配置网络地址转换。*

IP 伪装是一个相当直接的过程。它在网关或路由器上实现，该系统具有两个或多个网卡。一块网卡连接到外部网络，例如 Internet，第二块（以及额外的）网卡连接到局域网。连接到外部网络的卡可能通过电缆“调制解调器”或数字用户线 `DSL` 适配器等外部设备连接。

配置时做出以下假设：

- 公共 IP 地址分配给直接连接到外部网络的网卡。
- 局域网上的网卡获取与单个私有网络关联的 IP 地址。
- 网关或路由器系统上的一个网卡在同一私有网络上获取 IP 地址。
- 用于设置防火墙的相同 `iptables` 命令和配置文件也用于设置 IP 伪装。
- 如本章后面所述，路由器或网关系统上已启用 IP 转发。
- 局域网上的每个系统都配置为将路由器或网关系统的私有 IP 地址作为默认网关地址。

当局域网上的计算机想要 Internet 上的网页时，它会将数据包发送到防火墙。防火墙用防火墙的公共 IP 地址替换每个数据包上的源 IP 地址。然后它为数据包分配一个新的端口号。防火墙缓存原始源 IP 地址和端口号。

当数据包从 Internet 进入防火墙时，它应包含端口号。如果防火墙能够将端口号与特定传出数据包分配的端口号匹配的关联规则匹配，则过程会反转。防火墙用内部计算机的私有 IP 地址替换目标 IP 地址和端口号，然后将数据包转发回局域网上的原始客户端。

实际上，以下命令使用 `iptables` 启用伪装。所述命令假设 `eth1` 代表直接连接到 Internet 的网卡，私有 IP 网络为 `192.168.0.0/24`：

```
# iptables -t nat -A POSTROUTING -s 192.168.0.0/24 -o eth1 -j MASQUERADE
```

在大多数情况下，不需要私有 IP 网络地址，因为大多数受伪装保护的局域网都配置在单个私有 IP 网络上。

如果您使用单独的私有网络，例如第 1 章和第 2 章中配置的基于 KVM 的虚拟机，则这些网络的伪装可实现这些系统之间的通信。在这种配置中，伪装规则将应用于物理主机系统的防火墙。在我的系统上，我有以下伪装规则：

```
# iptables -t nat -A POSTROUTING -o wlan0 -j MASQUERADE

# iptables -t nat -A POSTROUTING -o virbr0 -j MASQUERADE

# iptables -t nat -A POSTROUTING -o virbr1 -j MASQUERADE
```

这些规则与接下来讨论的 IP 转发规则紧密配合。请注意，伪装会用路由器的 IP 地址替换源系统的 IP 地址。因此，如果您为两个虚拟机在物理主机系统上设置伪装，则来自一个虚拟机的通信似乎来自物理主机系统的 IP 地址。

## IP 转发

IP 转发通常被称为路由。路由对于 Internet 或任何 IP 网络的运行至关重要。路由器连接并促进多个网络之间的通信。当您设置计算机以查找外部网络上的站点时，它需要一个网关地址。这对应于局域网上的路由器的 IP 地址。

路由器查看每个数据包的目标 IP 地址。如果 IP 地址在其局域网之一上，它会将数据包直接路由到正确的计算机。否则，它会将数据包发送到更接近其最终目的地的另一个网关。要将 Red Hat Enterprise Linux 系统用作路由器，您应该通过更改 `/etc/sysctl.conf` 配置文件中的以下内容来启用 IP 转发

```
net.ipv4.ip_forward = 0
```

to

```
net.ipv4.ip_forward = 1
```

这些设置在下次重启时生效。在此之前，可以使用以下命令启用 IPv4 转发：

```
echo 1 > /proc/sys/net/ipv4/ip_forward
```

但这还不够。您还需要为与其他网络的通信启用防火墙的路由。例如，对于在两个虚拟网络上的基于 KVM 的虚拟机系统，它们在物理主机上的 `ifconfig` 命令输出中包含两个虚拟网络设备：`virbr0` 和 `virbr1`。我用来撰写本书的系统还包括本地无线网络设备 `wlan0`。对于具有普通有线以太网卡的物理主机，您可能需要将 `eth0` 替换为 `wlan0`。

```
# iptables -A FORWARD -o wlan0 -j ACCEPT

# iptables -A FORWARD -o virbr0 -j ACCEPT

# iptables -A FORWARD -o virbr1 -j ACCEPT
```
