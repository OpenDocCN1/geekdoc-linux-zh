
# (1) Policies (default)

```
iptables -P INPUT DROP
iptables -P OUTPUT DROP
iptables -P FORWARD DROP
```

# (2) User-defined chain for ACCEPTed TCP packets

```
iptables -N okay
iptables -A okay -p TCP --syn -j ACCEPT
iptables -A okay -p TCP -m state --state ESTABLISHED,RELATED -j ACCEPT
iptables -A okay -p TCP -j DROP
```

# (3) INPUT chain rules

## Rules for incoming packets from LAN

```
iptables -A INPUT -p ALL -i eth1 -s 10.0.0.0/8 -j ACCEPT
iptables -A INPUT -p ALL -i lo -s 127.0.0.1 -j ACCEPT
iptables -A INPUT -p ALL -i lo -s 10.0.0.1 -j ACCEPT
iptables -A INPUT -p ALL -i lo -s 123.45.67.89 -j ACCEPT
iptables -A INPUT -p ALL -i eth1 -d 10.0.0.255 -j ACCEPT
```

## Rules for incoming packets from the Internet

### Packets for established connections

```
iptables -A INPUT -p ALL -d 123.45.67.89 -m state --state \
ESTABLISHED,RELATED -j ACCEPT
```

### TCP rules

```
iptables -A INPUT -p TCP -i eth0 -s 0/0 --destination-port 21 -j okay
iptables -A INPUT -p TCP -i eth0 -s 0/0 --destination-port 22 -j okay
iptables -A INPUT -p TCP -i eth0 -s 0/0 --destination-port 80 -j okay
iptables -A INPUT -p TCP -i eth0 -s 0/0 --destination-port 113 -j okay
```

## 示例 2：用于共享互联网连接（无服务器）的防火墙

在此场景中，防火墙保护着一台 Linux 系统（即防火墙本身）以及局域网（LAN）中若干仅需连接互联网的系统。由于该防火墙后方没有服务器，因此您希望阻止来自互联网用户请求服务。

您可以使用示例 1 中展示的相同脚本，但不要使用请求 TCP 服务的行。因此，您可以删除第 2 部分中用户定义的链，并删除第 3 部分中的 TCP 规则。如果不想让防火墙对 ping 请求（类型 8）保持不可见状态，并且也不关心接收有关数据包生存时间值（TTL）超时的消息（类型 11）——例如当数据包遇到故障路由器时——您也可以移除 ICMP 规则。

## 示例 3：用于单个具有互联网连接的 Linux 系统的防火墙

在本示例中，只有一个网络接口，它将我的 Red Hat Linux 系统连接到互联网。您并没有与其他计算机共享该连接，并且您的计算机也不提供任何服务。

在这种情况下，您可以删除第 2、4 和 6 部分。在第 3 部分中，您可以删除所有与来自局域网的入站请求以及所有 TCP 服务相关的规则。正如我在示例 2 中提到的，您也可以移除类型 8 的 ICMP 规则以使您的防火墙对来自互联网的 ping 请求保持不可见状态，并移除类型 11 的 ICMP 规则以不接收关于生存时间失败数据包的消息。

## 理解 iptables

现在，既然您已经了解了一些关于 `iptables` 规则的外观以及如何启动它们，请稍微退后一步，看看 `iptables` 是如何工作的。

`iptables` 功能通过让 IP 数据包（即网络数据）在进出防火墙计算机时，遍历一组定义数据包处理方式的链来实现。你添加的每条规则基本上执行以下操作：

- 检查是否满足特定条件（例如，数据包请求特定服务或来自特定地址），并且
- 执行一个动作（例如丢弃、接受或对数据包进行进一步处理）。

针对不同版本的表实现了不同的规则集。例如，存在用于过滤（filter）、网络地址转换（nat）以及更改数据包头部（mangle）的表。根据数据包的源和目的地，它会遍历不同的链。你创建的大多数规则将与 `filter` 表相关（如果未指定其他表，则默认隐含使用 `filter` 表）。

与 `filter` 表相关的链包括 `INPUT`、`OUTPUT` 和 `FORWARD`。你还可以添加用户定义的链。你很可能最感兴趣的是使用前面示例中显示的基本规则来添加或移除特定的 TCP 和 UDP 服务。将 `ACCEPT` 分配给你希望放行的数据包，将 `DROP` 分配给你希望丢弃的数据包。你还可以分配 `REJECT` 以丢弃数据包但向发送方返回一条消息，或者使用 `LOG` 既不丢弃也不接受消息，而是记录有关数据包的信息。

`iptables` 内置了许多强大的功能。以下描述将向你介绍一些使用 `iptables` 的酷炫功能，并提供一些使用技巧。

## 允许 FTP 和 IRC 服务通过 iptables 防火墙

在使用被动 FTP 时，FTP 客户端会将其 IP 地址以及它将监听数据所在的端口号发送给服务器。如果该客户端位于防火墙后方的计算机上，且你正在对其执行 NAT，则这些信息也必须进行转换，否则 FTP 服务器将无法与客户端通信。

`iptables` 使用连接跟踪模块来跟踪连接。利用此功能，它可以查看 FTP 数据本身（即不在 IP 数据包头部中）以获取执行 NAT 所需的信息（请记住，来自互联网的计算机无法直接与你的私有 IP 地址通信）。为了执行 FTP 连接跟踪（以允许来自局域网客户端的被动 FTP 连接），你需要加载以下模块：

- `ip_conntrack_ftp`
- `ip_nat_ftp`

对于聊天（IRC）和 DCC 发送也是如此。地址和端口号存储在 IRC 协议数据包中，因此这些数据包也必须进行转换。为了允许局域网上的客户端使用 IRC 服务，你需要加载以下模块：

- `ip_conntrack_irc`
- `ip_nat_irc`

IRC 连接的默认端口是 6667。如果你不想使用默认端口，可以在加载连接跟踪模块时添加不同的端口号：

```bash
insmod ip_conntrack_irc.o ports=6668,6669
```

## 使用 iptables 执行 NAT 或 IP 伪装

如 `iptables` 示例中所述，你可以使用源网络地址转换（SNAT）或 IP 伪装（MASQUERADE）来允许具有私有 IP 地址的局域网计算机通过你的 `iptables` 防火墙访问互联网。如果你的互联网连接具有静态 IP 地址，请选择 SNAT；如果 IP 地址是动态分配的，则选择 MASQUERADE。

创建 MASQUERADE 或 SNAT 规则时，它会添加到 NAT 表和 `POSTROUTING` 链中。对于 MASQUERADE，你必须提供接口名称（如 `eth0`、`ppp0` 或 `slip0`）以标识通往互联网或其他外部网络的路由。对于 SNAT，你还必须标识该接口的实际 IP 地址。以下是一个 MASQUERADE 规则的示例：

```bash
# iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

以下是一个 SNAT 规则的示例：

```bash
# iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source 12.12.12.12
```

如果你有多个提供通往互联网路由的地址，可以添加多个源地址（例如，`--to-source 12.12.12.1-12.12.12.254`）。虽然 MASQUERADE 会使用一些额外的开销，但如果你的互联网连接是拨号连接且每次连接时 IP 地址都会变化，你可能需要使用它代替 SNAT。

请记住，你需要确保内核中已开启 IP 转发。（默认情况下它是关闭的。）要临时开启它，你可以执行以下操作：

```bash
# echo 1 > /proc/sys/net/ipv4/ip_forward
```

如果你需要动态 IP 寻址，请开启该服务：

```bash
# echo 1 > /proc/sys/net/ipv4/ip_dynaddr
```

## 使用 iptables 作为透明代理

使用 `REDIRECT` 目标，你可以将防火墙计算机特定端口的流量引导至另一个端口。利用此功能，你可以将本地局域网上的主机计算机引导至防火墙计算机上的代理服务，而无需这些主机知情。

以下是一个 `iptables` 命令命令行选项集合的示例，它使得对 Web 服务（端口 80）的请求被引导至代理服务（端口 3128）：
