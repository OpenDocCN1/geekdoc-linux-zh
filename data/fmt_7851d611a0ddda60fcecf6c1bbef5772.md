
你应该能看到类似下面的输出：

```
eth0 Link encap:Ethernet HWaddr 00:C0:F6:98:37:50

inet addr:206.171.50.50 Bcast:206.171.50.63 Mask:255.255.255.240

UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1

RX packets:9470 errors:0 dropped:0 overflows:0 frame:0

TX packets:7578 errors:0 dropped:0 overflows:0 carrier:0 collisions:0

Interrupt:5 address:0x3400
```

此处 `ifconfig` 报告网络接口设备 `eth0` 有一个 Internet 地址 (inet addr) 206.171.50.50，广播地址 (Bcast) 206.171.50.63 以及网络掩码 (255.255.255.240)。其余信息显示了该接口到为止接收了多少个数据包 (RX packets)、到为止传输了多少个数据包 (TX packets)、发生了多少种错误、该设备使用了哪个中断地址线、使用了哪个 I/O 地址基等。

你可以不带任何参数运行 `ifconfig`，以获取所有网络设备的完整列表。
你可以使用 `ifconfig` 来启用一个接口。例如：

```
ifconfig eth0 206.171.50.50 255.255.255.240 206.171.50.63
```
此处 `ifconfig` 显示 IP 206.171.50.50，掩码 255.255.255.240，广播地址 206.171.50.63。

你可以不带参数运行 `ifconfig` 来启用一个接口。例如：

```
ifconfig eth0 up
```
这将 `eth0` 接口。例如：

```
ifconfig eth0 down
```
该命令将关闭 `eth0` 接口。

## netcfg

语法：

```
netcfg
```

第 9 节使用 `netcfg` 来配置网络。

## netstat

语法：

```
netstat [-a]
```

此程序显示网络连接、路由表和接口统计信息。例如：

```
netstat -r
```
该命令将显示路由表。

## nslookup

语法：

```
nslookup [域名]
```

该命令允许你执行 DNS 查询。例如：

```
nslookup google.com
```
该命令将查询 `google.com` 的 DNS。

## ping

语法：

```
ping [-c count] host
```

`ping` 命令向目标发送 ICMP 请求包并等待 Echo 回应。它用于测试网络上的可达性并测量往返时间。

这是一个输出示例：

```
PING blackhole.nitec.com (206.171.50.50) 56(84) bytes of data

206.171.50.50: icmp_seq=0 ttl=64 time=145.2 ms

206.171.50.50: icmp_seq=1 ttl=64 time=138.5 ms

206.171.50.50: icmp_seq=2 ttl=64 time=139.1 ms

206.171.50.50: icmp_seq=3 ttl=64 time=142.8 ms

206.171.50.50: icmp_seq=4 ttl=64 time=137.4 ms

206.171.50.50: icmp_seq=5 ttl=64 time=136.9 ms

206.171.50.50: icmp_seq=6 ttl=64 time=138.7 ms

206.171.50.50: icmp_seq=7 ttl=64 time=140.2 ms

206.171.50.50: icmp_seq=8 ttl=64 time=139.5 ms

206.171.50.50: icmp_seq=9 ttl=64 time=138.8 ms

206.171.50.50: icmp_seq=10 ttl=64 time=137.1 ms

--- blackhole.nitec.com ping statistics ---

11 packets sent, 11 received, 0% packet loss

round-trip min/avg/max = 136.9/140.3/145.2 ms
```

上面的输出显示了对 `blackhole.nitec.com` 主机的 10 次 ping 请求。由于程序在第 11 次请求后被中断，统计数据显示 `ping` 发了 11 个数据包并接收了所有数据包，因此没有数据包丢失。

其他有趣的统计数据是往返最小 (min) 时间、平均 (avg) 时间和最大 (max) 时间。这些数字越小，相关主机之间的路由情况越良好。例如，如果你 ping 同局域网 (LAN) 上的主机，你应该看到往返时间在毫秒级。

如果你想让 `ping` 在传输指定数量的数据包后自动停止，请使用 `-c` 选项。例如：

```
ping -c 10 blackhole.nitec.com
```

## 第 5 章：常用命令

143

这将向指定的主机发送 10 次 ping 请求。默认情况下，ping 会发送一个 64 字节（56 字节数据 + 8 字节头文件）的报文数据包。如果你也对控制发送的数据包大小感兴趣，可以使用 `-s` 选项。例如：

```
ping -c 1024 -s 1016 reboot.nitec.com
```

此命令将向远程主机发送一个长度为 1024 (1016 + 8) 字节的数据包。

![](img/cbfef09f620ba4100baa62876f6f02b1_172_0.png)

> 通过向运行操作系统的远程主机（你知道它们是什么）发送大型数据包，可能会导致该主机对远程用户来说变得非常不可用。这可能被视为一种攻击，因此在世界上大多数地区极有可能是非法的。因此，当你开始使用 ping 实验他人的计算机时，请务必非常小心。

## route

语法：

```
route add -net network address netmask dev device
route add -host hostname or IP device
route add default gw hostname or IP
```

此命令允许你控制进入和离开计算机的路由。例如，要为你的网络创建默认路由，可以使用如下的 route 命令：

```
route add -net network address netmask device
```

例如，要为掩码为 255.255.255.240 的 206.171.50.48 网络创建默认路由，并使用 eth0 作为接口，我可以运行：

```
route add -net 206.171.50.48 255.255.255.240 eth0
```

要设置默认网关，你可以运行如下 route 命令：

```
route add default gw gateway address device
```

例如，要将默认网关地址设置为 206.171.50.49，我可以运行以下命令：

```
route add default gw 206.171.50.49 eth0
```

你可以使用以下命令在路由表中验证你的网络路由和默认网关是否已设置：

```
route -n
```

以下是上述命令的输出示例：

| Destination | Gateway | Genmask | Flags | Metric | Ref | Use | Iface |
|---|---|---|---|---|---|---|---|
| 206.171.50.48 | 0.0.0.0 | 255.255.255.240 | U | 0 | 0 | 6 | eth0 |
| 127.0.0.0 | 0.0.0.0 | 255.255.0.0 | U | 0 | 0 | 5 | lo |
| 0.0.0.0 | 206.171.50.49 | 0.0.0.0 | UG | | 0 | 0 | eth0 |

- 确保已在 `/etc/sysconfig/network` 以及在内核中开启了 IP 转发，以便在两个不同的网络接口之间路由数据包。

## tcpdump

语法：

```
tcpdump expression
```

这是一个非常强大的网络调试工具。例如，要追踪 brat.nitec.com 和 reboot.nitec.com 之间所有数据包，你可以使用以下命令：

```
tcpdump host brat.nitec.com and reboot.nitec.com
```
