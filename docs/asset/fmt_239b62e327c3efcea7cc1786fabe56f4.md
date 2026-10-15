
`-f` 参数应谨慎使用，因为它会使 Linux 尽可能多地发送 ICMP 回显请求，这在高负载网络上可能会迅速引发网络问题。该参数可用于产生模拟拥塞网络的负载，或为目标机器施加额外负载。

### -i 间隔

`ping` 的正常操作是在发送下一个 ICMP 回显请求之前等待一秒。通过使用 `-i` 间隔（以秒为单位），可以让 `ping` 在发送下一个回显请求前等待更长的时间。这在网络脚本中非常有用，因为在这些脚本中测试网络连通性很重要，但同时又需要脚本尽可能对网络友好。

## -s 数据包大小

`-s` 参数可用于发送比标准 64 字节数据包更小或更大的 ICMP 数据包。该选项与 `tcpdump`（后续会介绍）结合使用，可以判断 IP 数据报是否被分片，这在包含多种网络拓扑的网络中很常见。

## -I 接口 IP 地址

`-I` 参数强制 ICMP 回显请求从指定接口发出，这对于存在多条到达目的地的路由的多宿主主机非常有用。

## 地址解析协议（ARP）

地址解析协议（ARP）将第 3 层的 IP 地址映射到第 2 层的 MAC 地址。理解 ARP 的使用时机和工作方式，对于充分利用 `arp` 命令至关重要。每当某个节点希望向特定 IP 地址发送流量时，它会使用自身的 IP 地址和子网掩码来判断目的地是否位于直接连接的网络上。如果目的地址不是直接连接的，则会查询路由表。假设存在到达目的网络的路由（默认路由可以包含目的网络），主机随后会确定该路由条目的网关。确定网关后，主机会在适当的网络接口上广播一个以网关（路由器）地址为目标的 ARP `who-has` 请求，网关会以其 MAC 地址作为响应。然后主机会将发往目的地的流量引导至网关的 MAC 地址。

Linux 访问 ARP 表的工具是 `arp` 命令。与 `ifconfig` 命令一样，`arp` 也包含在 net-tools 发行版中，可从 `http://www.tazenda.demon.co.uk/phil/net-tools/` 获取。

与 `ifconfig` 类似，`arp` 不带任何参数时也非常有用：

```
[root@lefty /root]# arp
Address              HWtype  HWaddress           Flags Mask    Iface
192.168.1.1          ether   00:20:78:CF:3D:66   C              eth0
speedy               ether   00:40:00:08:6A:72   C              eth0
```

输出内容包括第 3 层（IP）地址、网络接口类型（HWtype）、MAC 地址（HWaddress）以及学习到该 MAC 地址的接口。Mask 在早期版本的 Linux 中使用过，但现在已不再使用。Flags 条目中的 `C` 表示该条目已完成——也就是说，IP 地址已被学习到。

`arp` 的输出并非完全一致：不完整的条目实际上会显示为 `(incomplete)` 条目，而不是在 ARP 表的 Flags 列中做任何标记：

```
[root@lefty /root]# arp
Address              HWtype  HWaddress           Flags Mask    Iface
192.168.1.5          (incomplete)                            eth0
192.168.1.1          ether   00:20:78:CF:3D:66   C              eth0
speedy               ether   00:40:D0:08:6A:72   C              eth0
```

`arp` 支持许多参数来辅助网络故障排查。

## -a 主机

`-a host` 参数将 `arp` 命令的输出过滤到所涉及的特定主机。

该主机可以是特定节点的主机名，也可以是节点的 IP 地址。

以下显示分配给 192.168.1.100 的 MAC 地址：

```
[root@lefty /root]# arp -a 192.168.1.100
Address       HWtype  HWaddress     Flags Mask Iface
192.168.1.100 ether   00:20:58:CC:66:3D C       eth0
```

将 `-a host` 与下一节讨论的 `-d` 选项结合使用，在同一网络的多个 Linux 节点上运行，可以帮助快速识别配置了相同 IP 地址的两台主机——IP 地址相同，但 MAC 地址不同。

## -H 硬件类型

`-H` 参数指定只打印特定接口类型的 ARP 条目。例如，要打印所有以太网条目，可使用：

```
[root@lefty /root]# arp -H ether
Address       HWtype  HWaddress     Flags Mask Iface
192.168.1.1   ether   00:20:78:CF:30:66 C       eth0
speedy        ether   00:40:D0:08:6A:72 C       eth0
```

或者查看任何令牌环网条目：

```
[root@lefty net]# arp -H tr
arp: in 2 entries no match found.
```

`arp` 命令支持的介质（硬件）类型如表 9.6 所示。

### 表 9.6 Linux `arp` 命令支持的网络介质类型

| 介质 | 硬件类型缩写 |
|---|---|
| 自适应串行线路 IP | Adaptive |
| 业余无线电 NET/ROM | Netrom |
| 业余无线电 ROSE | rose |
| 业余无线电 X.25 | ax25 |
| ARCnet | arcnet |
| Ash | ash |
| Cisco HDLC | hdlc |
| 压缩串行线路 IP | cslip |
| 压缩串行线路 IP（6 位） | cslip6 |
| Econet | ec |
| 以太网 | ether |
| 光纤分布式数据接口 | fddi |

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

`arp` 还可以使用 `-i` 参数显示特定接口的所有条目。要查看 righty 的第二块接口卡上学习到的所有 ARP 条目，应使用以下 `arp` 命令：

```
[root@righty /root]# arp -i eth1
Address       HWtype  HWaddress     Flags Mask Iface
10.1.1.4      ether   00:40:68:0F:33:22  C       eth1
blue          ether   00:40:D7:08:6A:52  C       eth1
```

## -n

`-n` 会关闭 `arp` 命令的名称解析功能，使 IP 地址不会被解析为主机名。请注意不带 `-n` 的 `arp` 命令：

```
[root@lefty /root]# arp
Address       HWtype  HWaddress     Flags Mask Iface
192.168.1.1   ether   00:20:78:CF:3D:66  C       eth0
speedy        ether   00:40:D0:08:6A:72  C       eth0
```

`speedy` 的 IP 地址正在被解析，`arp` 打印的是 `speedy` 而不是 IP 地址。以下是关闭名称解析后的同一 `arp` 表：
