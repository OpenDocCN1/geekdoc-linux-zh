
```
[root@lefty /root]# arp -n
Address       HWtype  HWaddress     Flags Mask Iface
192.168.1.1   ether   00:20:78:CF:3D:66  C       eth0
192.168.1.101 ether   00:40:D0:08:6A:72  C       eth0
```

## -d Host

有时有必要删除主机的 `arp` 条目以排查网络问题，例如地址解析未正确工作的情况，如两个节点配置了相同的 IP 地址，或网络接口卡似乎行为异常。`-d` 条目可用于删除特定条目。`-d` 后跟主机，可以是节点的 IP 地址或主机名。要从 `arp` 缓存中删除 `speedy` 的 MAC 地址，输入如下内容：

```
[root@lefty /root]# arp -d speedy
```

要查看其是否已被删除：

```
[root@lefty /root]# arp
Address          HWtype  HWaddress       Flags Mask Iface
192.168.1.1      ether   00:20:78:CF:30:66 C       eth0
```

在排查 ARP 相关问题时，通常需要清空完整的 ARP 缓存。以下脚本 `darpcache` 使用 `-d` 参数解析缓存并删除所有条目：

```
#!/bin/bash
# darpcache
# This script deletes all arp entries from the arp cache

for host in `arp -n | awk '{print $1}' | grep -v Address`
do
    echo "Deleted entry for host: $host"
    arp -d $host*
done
```

其输出看起来类似如下：

```
[root@lefty /root]# ./darpcache
Deleted entry for host: 192.168.1.1
Deleted entry for host: 192.168.1.101
```

一个相关的协议 `RARP` 与 `ARP` 工作方式类似；然而其目的是允许主机通过广播其 MAC 地址作为 `RARP` 请求来确定其 IP 地址。然后节点会以映射的 IP 地址进行响应。`RARP` 协议几乎已被动态主机控制协议 `DHCP` 取代，原因有几个，包括 `RARP` 倾向于在特定节点上静态映射，而 `DHCP` 能够提供超出 IP 地址之外的额外信息，包括 DNS 配置如名称服务器和域名后缀。`DHCP` 也在非 UNIX 系统上得到广泛支持。

`RARP` 支持必须在 Linux 内核中配置，并且 `RARP` 表使用 `rarp` 命令进行管理。

## traceroute

`traceroute` 可能仅次于 `ping` 命令，是使用最频繁的网络故障排除工具。`traceroute` 显示源主机与目标主机之间的路径，即执行命令的 Linux 节点与目标之间的路径。

`traceroute` 与 `ping` 不同，不依赖于路径上的路由器对特定路径的响应，而是组装一个带有目标地址的 UDP 数据包，但将第一个发送数据包的生存时间位设置为 1。`traceroute` 然后发送数据包，前往目标的第一个路由器接受数据包并递减生存时间。由于生存时间为 1，生存时间现在变为零，这会触发路径中的第一个路由器发送回 ICMP 超时消息并丢弃数据包。`traceroute` 为用户打印 ICMP 消息的源地址，增加其内部计数器以设置生存时间，并发送第二个数据包。

第一个路由器将生存时间从 2 递减到 1，第二个路由器将生存时间从 1 递减到零并返回 ICMP 消息计时器超时。`traceroute` 然后根据 ICMP 消息的源地址打印第二个路由器的 IP 地址，并继续到最终目标。最终目标没有监听该端口的服务，因此返回 ICMP 端口不可达。当 `traceroute` 收到此消息时，它会打印最终地址并退出。

现在 `traceroute` 已被解释，仔细查看 `traceroute` 的选项将显示 `traceroute` 的一些更高级用法。

## -d

要打开 `traceroute` 的额外调试信息，请使用 `-d` 参数。额外的信息，尤其是如果适用于内部管理控制下的网络，可能有助于确定网络问题。例如，使用 `-d` 选项的以下输出意味着可能存在路由问题，网络不可达，或网络应可达的接口问题：

```
[root@lefty /root]# traceroute -d host.anydomain.com
traceroute to host.anydomain.com (192.168.100.100), 30 hops max, 38 byte packets
 1 traceroute: sendto: Network is unreachable
 1 traceroute: wrote host.anydomain.com 38 chars, ret=-1
```

## -f ttl

`-f` 参数后跟生存时间告诉 `traceroute` 从 `ttl` 开始生存时间计数器，有效地不报告 `ttl - 1` 跳。这在 `traceroute` 穿过不会响应 `traceroute` 但会允许请求通过的防火墙时很有用。当已知前几个跳时也很有用。

## -F

不分割 `-F` 选项指示 `traceroute` 设置不分片位，这样如果 UDP 数据包会被转发到 MTU 大于 `traceroute` 所发送数据包的接口时，路径上的任何路由器都不应转发该 UDP 数据包。这对于排查与 MTU 或 MTU 发现相关的问题非常有用。

## -i 接口

在多宿主系统上，有时需要指定使用哪个接口来执行 `traceroute` 命令。通过使用 `-i` 参数，`traceroute` 将使用指定的接口——因此也就是该指定接口的 IP 地址——作为 `traceroute` 的源地址。

## -I

如前所述，`traceroute` 使用发往高端口的 UDP 数据包；但是，`-I` 告诉 `traceroute` 使用 ICMP 回显请求数据包而不是 UDP。如果防火墙不允许 UDP 但允许 ICMP 回显请求，这可能很有用。这也使 `traceroute` 的功能更类似于 Microsoft 版本的 `tracert`，后者是在 Microsoft Windows 上发挥与 `traceroute` 相同作用的工具。

除了使用 ICMP 数据包之外，`traceroute` 的功能完全相同——TTL 仍然被适当设置，以确保中间路由器产生相同的行为。一个关键区别在于最终目的地——它可能实际上会用回显应答来回应回显请求。

## -n

`-n` 参数关闭 `traceroute` 的名称解析。通常这用于加快 `traceroute` 的运行速度——尤其是在由于所分析的网络问题而导致名称服务器不可达时。通过使用 `-n`，沿途的每一跳都不必进行查找，因此用户无需等待 `traceroute` 的解析超时后再继续。

## -m 最大跳数

`-m` 选项告诉 `traceroute` 在达到最大跳数后停止：

```
[root@lefty /root]# traceroute -m 3 host.somedomain.com (192.168.50.50), 3 hops max, 38 byte packets
1 gw4.isp1.net (192.168.14.2) 39.331 ms 33.990 ms 51.079 ms
2 router3.isp2.net (10.1.1.254) 25.888 ms 31.675 ms 25.998 ms
router5.isp2.net (10.5.5.254) 25.296 ms 26.012 ms 26.335 ms
```

`-m` 可以与 `-f` 结合使用，以进一步限制输出和报告的路由器：

```
[root@lefty /root]# traceroute -f 2 -m 3 host.somedomain.com
traceroute to host.somedomain.com (192.168.50.50), 3 hops max, 38 byte packets
 2 router3.isp2.net(10.1.1.254) 22.868 ms 32.675 ms 27.887 ms
 3 router5.isp2.net(10.5.5.254) 25.186 ms 26.122 ms 26.322 ms
```

后文将介绍的 `tcpdump` 会在 `traceroute` 执行期间给出完整的分解信息。

## -t tos

`-t tos` 参数允许在 IP 数据包中指定服务类型位。随着语音分组技术的兴起，这个参数越来越流行。许多语音部署依赖 `tos` 位，或者更具体地说，依赖这些位的 DIFFSERV 实现，来确保带宽需求得到满足。然而，在这些下一代网络之外，`-t` 参数的用途非常有限。

## traceroute 注意事项

`traceroute` 是一个非常实用的工具，可以用来快速定位网络故障点；然而，鉴于其行为可能受到网络状况的影响，不应完全依赖它。以下是一些需要注意的事项。

### 非对称路由
