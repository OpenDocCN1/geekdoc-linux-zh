

# 表 9.6 继续

| Media | Hardware Types Abbreviations |
|---|---|
| Frame Relay Access Device | frad |
| Frame Relay DLCI | dlci |
| High-Performance Parallel Interface | hppi |
| IP in IP Tunneling | tunnel |
| IPv6 in IPv4 Tunneling | sit |
| IrLAP | irda |
| LAPB | lapb |
| Local Loopback | loop |
| Point-to-Point Protocol | ppp |
| Serial Line IP | slip |
| Serial Line IP 6 bit | slip6 |
| Token Ring | tr |

## -i 接口

arp 还可以使用 -i 参数显示特定接口的所有条目。要查看 righty 的第二块接口卡上学习到的所有 ARP 条目，应使用以下 arp 命令：

```
[root@righty /root]# arp -i eth1
Address       HWtype  HWaddress     Flags Mask Iface
10.1.1.4      ether   00:40:68:0F:33:22  C       eth1
blue          ether   00:40:D7:08:6A:52  C       eth1
```

## -n

-n 会关闭 arp 命令的名称解析功能，使 IP 地址不会被解析为主机名。请注意不带 -n 的 arp 命令：

```
[root@lefty /root]# arp
Address       HWtype  HWaddress     Flags Mask Iface
192.168.1.1   ether   00:20:78:CF:3D:66  C       eth0
speedy        ether   00:40:D0:08:6A:72  C       eth0
```

speedy 的 IP 地址正在被解析，arp 打印的是 speedy 而不是 IP 地址。以下是关闭名称解析后的同一 arp 表：

```
[root@lefty /root]# arp -n
Address       HWtype  HWaddress     Flags Mask Iface
192.168.1.1   ether   00:20:78:CF:3D:66  C       eth0
192.168.1.101 ether   00:40:D0:08:6A:72  C       eth0
```

## -d Host

有时有必要删除主机的 arp 条目以排查网络问题，例如地址解析未正确工作的情况，如两个节点配置了相同的 IP 地址，或网络接口卡似乎行为异常。-d 条目可用于删除特定条目。-d 后跟主机，可以是节点的 IP 地址或主机名。要从 arp 缓存中删除 speedy 的 MAC 地址，输入如下内容：

```
[root@lefty /root]# arp -d speedy
```

要查看其是否已被删除：

```
[root@lefty /root]# arp
Address          HWtype  HWaddress       Flags Mask Iface
192.168.1.1      ether   00:20:78:CF:30:66 C       eth0
```

在排查 ARP 相关问题时，通常需要清空完整的 ARP 缓存。以下脚本 darpcache 使用 -d 参数解析缓存并删除所有条目：

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

一个相关的协议 RARP 与 ARP 工作方式类似；然而其目的是允许主机通过广播其 MAC 地址作为 RARP 请求来确定其 IP 地址。然后节点会以映射的 IP 地址进行响应。RARP 协议几乎已被动态主机控制协议 DHCP 取代，原因有几个，包括 RARP 倾向于在特定节点上静态映射，而 DHCP 能够提供超出 IP 地址之外的额外信息，包括 DNS 配置如名称服务器和域名后缀。DHCP 也在非 UNIX 系统上得到广泛支持。

RARP 支持必须在 Linux 内核中配置，并且 RARP 表使用 rarp 命令进行管理。

## traceroute

traceroute 可能仅次于 ping 命令，是使用最频繁的网络故障排除工具。traceroute 显示源主机与目标主机之间的路径，即执行命令的 Linux 节点与目标之间的路径。

traceroute 与 ping 不同，不依赖于路径上的路由器对特定路径的响应，而是组装一个带有目标地址的 UDP 数据包，但将第一个发送数据包的生存时间位设置为 1。traceroute 然后发送数据包，前往目标的第一个路由器接受数据包并递减生存时间。由于生存时间为 1，生存时间现在变为零，这会触发路径中的第一个路由器发送回 ICMP 超时消息并丢弃数据包。traceroute 为用户打印 ICMP 消息的源地址，增加其内部计数器以设置生存时间，并发送第二个数据包。

第一个路由器将生存时间从 2 递减到 1，第二个路由器将生存时间从 1 递减到零并返回 ICMP 消息计时器超时。traceroute 然后根据 ICMP 消息的源地址打印第二个路由器的 IP 地址，并继续到最终目标。最终目标没有监听该端口的服务，因此返回 ICMP 端口不可达。当 traceroute 收到此消息时，它会打印最终地址并退出。

现在 traceroute 已被解释，仔细查看 traceroute 的选项将显示 traceroute 的一些更高级用法。

## -d

要打开 traceroute 的额外调试信息，请使用 -d 参数。额外的信息，尤其是如果适用于内部管理控制下的网络，可能有助于确定网络问题。例如，使用 -d 选项的以下输出意味着可能存在路由问题，网络不可达，或网络应可达的接口问题：

```
[root@lefty /root]# traceroute -d host.anydomain.com
traceroute to host.anydomain.com (192.168.100.100), 30 hops max, 38 byte packets
 1 traceroute: sendto: Network is unreachable
 1 traceroute: wrote host.anydomain.com 38 chars, ret=-1
```

## -f ttl

-f 参数后跟生存时间告诉 traceroute 从 ttl 开始生存时间计数器，有效地不报告 ttl -1 跳。这在 traceroute 穿过不会响应 traceroute 但会允许请求通过的防火墙时很有用。当已知前几个跳时也很有用。

