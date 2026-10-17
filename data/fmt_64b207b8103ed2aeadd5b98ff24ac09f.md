
如果你想查找邮件交换器 (MX)，使用 `mx` 查询：

```bash
$ dig www.turbosphere.com mx
```

要查看域名的名称服务器，使用 `ns` 查询：

```bash
$ dig www.turbosphere.com ns
```

要查找域名的所有可用记录，使用 `any` 查询：

```bash
$ dig www.turbosphere.com any
```

## 排除网络故障

网络故障排除通常从底部开始。正如开头提到的，第一步是确保物理组件（电缆、网卡和等）已连接。当建立链路后，下一步是检查默认网关。

使用 `ip` 命令检查默认网关：

```bash
# ip route
10.0.0.0/24 dev eth0 proto kernel scope src 10.0.0.15
169.254.0.0/16 dev eth0 scope
default via 10.0.0.1 dev eth0
```

默认网关是 `10.0.0.1`。确保到网关的 IP 连通性，如下使用 `ping` 命令：

```bash
$ ping 10.0.0.1
PING 10.0.0.1 (1) 56(84) bytes of data.
64 bytes from 10.0.0.1: icmp_seq=1 ttl=64 time=0.382 ms
64 bytes from 10.0.0.1: icmp_seq=2 ttl=64 time=0.313 ms
64 bytes from 10.0.0.1: icmp_seq=3 ttl=64 time=0.360 ms
64 bytes from 10.0.0.1: icmp_seq=4 ttl=64 time=1.43 ms
```
-- 10.0.0.1 ping statistics
4 packets transmitted, 4 received, 0% packet loss, time 2999ms
rtt min/avg/mdev = 0.313/0.621/1.432/0.469 ms
```

默认情况下，`ping` 会一直持续直到你按下 `Ctrl+c`。其他选项包括：

```bash
$ ping -a 10.0.0.1
在 ping 进行时添加发声 ping
$ ping -c 4 10.0.0.1
ping 4 次并退出（Windows 默认）
$ ping -q -c 5 10.0.0.1
显示 ping 摘要（配合 -c 效果最佳）
# ping -f 10.0.0.1
发送洪水泛洪 ping（需要 root 权限）
```

# 第11章：管理网络连接

```bash
$ ping -i 3 10.0.0.1      每隔3秒发送一次数据包
$ ping -i eth0 10.0.0.1       将源设置为eth0（当有多个网卡时使用）
PING 10.0.0.1 (10.0.0.1) from 10.0.0.155 eth0: 56(84) bytes of data.
$ ping -i 10.0.0.155 10.0.0.155  将源设置为10.0.0.155
PING 10.0.0.1 (10.0.0.1) from 10.0.0.155 : 56(84) bytes of data.
$ ping -s 1500 10.0.0.1       将数据包大小设置为1500字节
PING 10.0.0.1 (10.0.0.1) 1500(1528) bytes of data.
```

请谨慎使用 `ping` 选项。默认情况下，`ping` 发送的是小数据包（56字节）。大数据包（如刚才所示的1500字节字节设置）有助于让故障的网卡或连接显现出来。

## 检查地址解析协议 (ARP)

如果你无法 `ping` 通你的网关，可能以太网 MAC 层上存在问题。地址解析协议 (ARP) 可用于查找 MAC 层的信息。使用 `arp` 或 `ip neighbor` 命令可以查看和配置 ARP 条目。此示例显示了按主机名列出的 ARP 缓存条目：

| arp -v | 按名称列出 ARP 缓存条目 |

| Address | Hwtype | HAddress | Flags | Mask | Iface |

| :--- | :--- | :--- | :--- | :--- | :--- |

| ritchie | ether | 00:10:A5:FB:A6:A7 | C | | eth0 |

| einstein | ether | 00:0B:6A:02:EC:98 | C | | eth0 |

条目: 1 跳过: 0 发现: 1

在此示例中，你可以看到本地计算机 ARP 缓存已知的的其他计算机名称，以及每台计算机网卡的关联硬件类型和硬件地址。你可以通过禁用名称解析来解析这些计算机的 IP 地址：

| arp -vn | 按 IP 地址列出 ARP 缓存条目 |

| Address | Hwtype | HAddress | Flags | Mask | Iface |

| :--- | :--- | :--- | :--- | :--- | :--- |

| 10.0.0.1 | ether | 00:10:A5:FB:A6:A7 | C | | eth0 |

| 10.0.0.50 | ether | 00:0B:6A:02:EC:98 | C | | eth0 |

条目: 1 跳过: 0 发现: 1

要从 ARP 缓存中删除条目，请使用 `-d` 选项：

```
$ arp -d 10.0.0.50      从 ARP 缓存中删除地址 10.0.0.50
```

与其让 ARP 动态学习其他系统，不如使用 `-s` 选项向缓存中添加静态 ARP 条目：

```
$ arp -s 10.0.0.51 00:0B:6A:02:EC:95  向 ARP 添加 IP 和 MAC 地址
```

使用 `ip` 命令执行与你刚才对 `arp` 命令执行相同的的操作，使用 `neighbor` 对象（注意 `neighbor`、`nei` 和 `n` 可以互换使用）：

```
# ip neighbor
10.0.0.1 dev eth0 laddr 00:10:5a:ab:f6:a7 DEL
10.0.0.50 dev eth0 laddr 00:0b:6a:02:98 REACHABLE
# ip nei 10.0.0.50 dev eth0
# ip add 10.0.0.51 laddr 00:0B:6A:02:EC5 dev eth0
```

使用 `arping` 命令查询子网以查看 IP 是否已占用，并找到使用它的设备的 MAC 地址。`arping` 命令被 `ifup` 用于在绑定以太网网卡时避免 IP 冲突。以下是示例：

```
# arping 10.0.0.50                查询子网查看 10.0.0.50 是否被占用
ARPING 10.0.0.50 from 10.0.195 eth0
Unicast reply from 10.0.0.50 [00:0B:6A:02:EC:98] 0.694ms
Unicast reply from 10.0.0.50 [00:0B:6A:02:EC:98] 0.683ms
# arping -i eth0 10.0.0.50        指定要查询的接口
```

像 `ping` 一样，`arping` 命令持续查询地址，直到按下 `Ctrl+C` 命令。通常，你想知道目标是否存活。如果是这样，可以使用 `tracer` 寻找瓶颈或故障点：

```
# arping -f 10.0.0.50             查询 10.0.0.50 在第一个回复时停止
# arping -c 2 10.0.0.51           查询 10.0.0.50 在计数2次后停止
```

## 追踪主机路由

在确保你可以 `ping` 通网关并到达网络外的机器后，可能仍然存在访问特定主机或网络的问题。如果是这样，可以使用 `traceroute` 寻找瓶颈或故障点：

```
traceroute boost.turbosphere.com 追踪到主机的路径
to boost.turbosphere.com (66.113.99.70), 30 hops max,40 byte packets
```

| Hop | Host | ms 1 | ms 2 |

| :--- | :--- | :--- | :--- |

| 1 | 10.0.0.1 (10.0.0.1) | 0.289 ms | 0.237 ms |

| 2 | tl-03.hbci.com (64.211.141) | 6.213 ms | 6.189 ms |

| 3 | 172.17.2.153 (172.17.2.153) | 14.027 ms | 14.025 ms |

| 4 | so-0-3-2.1.gbix (208.448.111) | 19.076 ms | 19.053 ms |
