
```
eth0      Link encap:Ethernet  HWaddr 00:08:74:85:C1:60
          inet addr:192.168.0.7  Bcast:192.168.0.255  Mask:255.255.255.0
          inet6 addr: fe80::208:74ff:fe85:c160/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:612851 errors:0 dropped:0 overruns:0 frame:0
          TX packets:574197 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:99834031 (95.2 MiB)  TX bytes:76034821 (72.5 MiB)
          Interrupt:10 Base address:0x3000

eth1      Link encap:Ethernet  HWaddr 00:02:2D:8C:F8:C5
          inet addr:192.168.0.9  Bcast:192.168.0.255  Mask:255.255.255.0
          inet6 addr: fe80::202:2dff:fe8c:f8c5/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:0
          RX packets:3833 errors:0 dropped:0 overruns:0 frame:0
          TX packets:1242 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:560194 (547.0 KiB)  TX bytes:250287 (244.4 KiB)
          Interrupt:3 Base address:0x100

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:16436  Metric:1
          RX packets:2456 errors:0 dropped:0 overruns:0 frame:0
          TX packets:2456 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:2891581 (2.7 MiB)  TX bytes:2891581 (2.7 MiB)
```

该输出表明，当前系统上有三个网络接口处于活动状态——即回环接口（`lo`）和两块以太网网卡（`eth0` 和 `eth1`）。对于每个接口，您可以查看其 IP 地址，以及有关已交付和已发送数据包的统计数据。如果 Linux 系统已建立拨号 PPP 链路并正在运行，您还将在输出中看到 `ppp0` 接口的项目。

## 检查 IP 路由表

另一个网络配置命令 `/sbin/route`，在您不带命令行参数运行它时，也会提供状态信息。如果您在检查与另一台主机（通过 IP 地址指定）的连接时遇到问题，请检查 IP 路由表，查看是否指定了默认网关。然后，检查该网关的路由表，以确保通往外部网络的路径出现在该路由表中。

`/sbin/route` 命令的典型输出如下所示：

```
Kernel IP routing table
Destination    Gateway        Genmask     Flags Metric Ref  Use Iface
               *          0.0.0.0       0.0.0.0     U                   0     0     0 lo
192.168.0.0    *          255.255.255.0 U                   0     0     0 eth0
192.168.0.0    *          255.255.255.0 U                   0     0     0 eth1
169.254.0.0    *          255.255.0.0   U                   0     0     0 eth1
default      192.168.0.1  0.0.0.0       UG                  0     0     0 eth0
```

正如该路由表所示，本地网络使用 `eth0` 和 `eth1` 以太网接口，而默认网关是 `eth0` 以太网接口。默认网关是一种路由设备，它处理发往 Linux 系统所在网络以外的任何网络的数据包。在本例中，发往除以 192.168.0 开头的所有其他网络地址的数据包都会发送到网关——192.168.0.1。该网关将这些数据包转发到其他网络（当然，前提是网关连接到另一个网络，最好是互联网）。

## 检查与主机的连接

要检查与特定主机的网络连接，请使用 `ping` 命令。`ping` 是一个广泛使用的 TCP/IP 工具，它使用一系列互联网控制报文协议（`ICMP`，发音为 `EYE-comp`）消息。`ICMP` 提供一种回声消息，每台主机都会对此做出响应。通过 `ICMP` 消息和回复，`ping` 可以确定另一台系统是否存活，并计算与该系统通信的往返延迟。

以下示例展示了我如何运行 `ping` 以查看我网络上的某台系统是否存活：

```
ping 192.168.0.1
```

这是该命令在我的家庭网络上显示的内容：

```
PING 192.168.0.1 (192.168.0.1) 56(84) bytes of data.
64 bytes from 192.168.0.1: icmp_seq=1 ttl=63 time=0.256 ms
64 bytes from 192.168.0.1: icmp_seq=2 ttl=63 time=0.267 ms
64 bytes from 192.168.0.1: icmp_seq=3 ttl=63 time=0.272 ms
64 bytes from 192.168.0.1: icmp_seq=4 ttl=63 time=0.267 ms
64 bytes from 192.168.0.1: icmp_seq=5 ttl=63 time=0.275 ms
--- 192.168.0.1 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 3999ms
rtt min/avg/max/mdev = 0.256/0.267/0.275/0.016 ms
```

在 Linux 中，`ping` 会持续运行，直到您按下 `Ctrl+C` 停止它；然后它会显示汇总统计信息，表明在两个系统之间发送一个数据包所需的典型时间。在某些系统上，`ping` 仅报告远程主机处于活动状态。然而，您仍然可以通过使用适当的命令行参数获取计时信息。

![](img/11709a8f88c8cd03868a929dc94c0e2b_330_0.png)

`ping` 命令依赖于许多防火墙被配置为阻止的 `ICMP` 消息。因此，`ping` 并不总是有效，也不再是测试网络连接性的可靠方法。如果针对特定主机的 `ping` 失败，不要假设该主机已宕机或未连接到网络；通常可以使用 `ping` 成功检查局域网内的连接性。

## 检查网络状态

要检查网络状态，请使用 `netstat` 命令。该命令显示各种类型（如 TCP 和 UDP 连接）的网络连接状态。您可以通过输入 `netstat -i` 快速查看接口的状态，这将产生与以下类似的输出：

```
Kernel Interface table
Iface  MTU Met  RX-ERR RX-DRP RX-OVR  TX-ERR TX-DRP TX-DRP TX-OVR Flg
eth0 1500 0 63175 0 0 1 574695 0 0 0 BMRU
eth1 1500 0 4298 0 0 0 1375 0 0 0 BMRU
lo   16436 0 3255 0 0 0 3255 0 0 0 LRU
```

在此情况下，输出显示回环接口和以太网接口的当前状态。表 4-2 描述了各列的含义。
