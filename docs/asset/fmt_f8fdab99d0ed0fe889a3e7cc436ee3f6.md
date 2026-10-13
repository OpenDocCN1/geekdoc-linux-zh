
```
mario@chaos:~$ ll /usr/sbin/tracroute www.umbral.com
tracroute to xnya.umbral.com (207.87.10.30), 30 hops max, 40 byte packets
1: master.spin.com.mx (200.13.60.123) 120.75 ms 126.74 ms 100.533 ms
2: octopus.spin.com.mx (200.13.61.32) 110.042 ms 104.654 ms 99.599 ms
3: 200.33.216.161 (200.33.216.161) 119.589 ms 105.897 ms 109.603 ms
4: rri1.memxfd.aventel.net.mx (200.33.209.1) 131.555 ms 112.566 ms 107.6103.6 ms
5: bordercore2-hss10-0Dallas.cw.net (166.48.77.249) 159.54 ms 155.378 ms 159.590 ms
6: core0.Dallas.cw.net (200.70.9.60) 159.493 ms 156.364 ms 159.620 ms
7: dfdz-core2-s1-0.atlas.digex.net (165.117.59.13) 169.595 ms 156.924 ms 149.620 ms
8: lax1-core1-s8-0.0.atlas.digex.net (165.117.58.25) 199.497 ms 194.896 ms 189.621 ms
9: sjc4-core2-s5-0.0.atlas.digex.net (165.117.53.74) 199.489 ms 199.460 ms
==> sjc4-core2-s5-1-0.atlas.digex.net [165.117.58.110] 191.825 ms
== sjc4-core2-s5-0-0.atlas.digex.net [165.117.53.74] 210.25 ms
10: sjc4-core6-posi-1.atlas.digex.net (165.117.59.69) 201.91 ms 196.195 ms 199.584 ms
11: sjc4-wscore-p2-0.wscq.digex.net (199.125.178.37) 360.488 ms 366.267 ms 199.461 ms
12: sjc4-wsc0e4-fa1-0.wscq.digex.net (199.125.178.28) 582.272 ms 207.535 ms 198.275 ms
13: xnya.umbral.com (207.87.10.30) 209.457 ms 3076.14 ms *
```

如果您知道如何查找信息，`tracroute` 可以提供相当多的信息。例如，您可以在列表 20.1 中看到以下几点：

- `www.umbral.com` 实际上是 `xnya.umbral.com` 的别名。`tracroute` 始终执行反向 DNS 查找，并报告其追踪的主机的官方主机名。
- `xnya.umbral.com` 通过域名是 `digex.net` 的服务提供商连接到互联网（可能是一家名为 Digex 的 ISP）。（第 7 行至第 12 行均属于最后一个网关所在的 IP 网络域。）
- 您通过一家名为 Spin 的 ISP 连接到互联网，该 ISP 位于墨西哥。（第 1 行和第 2 行是第一个网关。域名以 `.mx` 结尾。）
- 出现在第 9 行的 `digex` 主机实际上是具有相同 IP 地址的几台主机。这是为了冗余性而设计的。
- 主机 10、11 和 12 之间似乎存在某种瓶颈。请注意响应时间是如何在第 9 行之前稳步缓慢增长，然后突然从大约 200 毫秒跳到 300 多毫秒，再跳到 500 多毫秒。这可能是暂时的瓶颈（仅由当前流量负载引起），也可能是持续的问题（例如由物理介质问题或链路容量不足引起）。

## traceroute

如您所见，`traceroute` 可以是一个极其宝贵的工具。从 `traceroute` 的输出中还可以获取更多有用的信息；为了获得完整的讨论，最好阅读 `traceroute`(8) 手册页。

## tcpdump

`tcpdump` 是调试某些类型网络问题的另一个宝贵工具。它基本上作为一个`数据包嗅探器`运行——它监听网络，查看经过的任何数据包（无论是否发往其运行的主机），并对其进行处理。它可以保存看到的所有流量或仅有趣的部分，或者对其包含的信息进行基础分析。

`tcpdump` 通过将网卡设置为所谓的`混杂模式`（promiscuous mode）来工作。通常情况下，网卡只会看到为其`自己`准备的数据包。然而，在混杂模式下，它会看到通过网络传输的所有数据包，并将其传递给上层操作系统。然后操作系统将这些数据包传递给 `tcpdump`，由它进行过滤、显示或存储。由于它会修改网卡的配置，因此必须以 `root` 身份运行 `tcpdump`。

### 注意

> `tcpdump` 是一个潜在的安全漏洞。它属于被称为`嗅探器`的程序类别，这些程序监听网络，能够监听网络中的所有数据包并存储它们。如果用户使用像 `Telnet` 这样以明文发送密码的程序，攻击者可能会使用嗅探器来窃取他们的密码。因此，永远不要将 `tcpdump` 设置为 `setuid` `root`。

要检测网络接口是否处于混杂模式（即可能在其上运行嗅探器），请使用 `ifconfig` 命令显示接口的配置。如果接口处于混杂模式，将会显示 `PROMISC` 标志：

```
$ /sbin/ifconfig eth0
eth0      Link encap:Ethernet  Hwaddr 00:00:97:5E:F0:61
          inet addr:10.0.1.50  Bcast:10.0.1.255  Mask:255.255.255.0
          UP BROADCAST RUNNING PROMISC MULTICAST  MTU:1500  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:5 errors:0 dropped:0 overruns:0 carrier:5
          Collisions:0
          Interrupt:3 Base address:0x310
```

如果您不带任何参数运行 `tcpdump`，您将看到所有通过网络的数据包列表：

```
# /usr/sbin/tcpdump

tcpdump: listening on eth0
22:46:12.730048 renato.1445832987 > visionlu.nfs: 100 readlink [nfs]
22:46:12.734424 tunoloia.1012 > visionlu.800: uo2 92
22:46:12.746763 tunoloia.22 > atman.1023: P 1442999991:1423000355 (44) ack 3798274339 win 32120 <OF> [tos 0x10]
22:46:12.765084 atman.1023 > tunoloia.22: . ack 44 win 32120 <OF> [tos 0x10]
22:46:12.778100 visionlu.800 > tunoloia.1015: uo2 56
22:46:12.780084 renaro.144837013 > visionlu.nfs: 124 lookuo [nfs]
22:46:12.780153 tunoloia.22 > atman.1023: P 44:596(552) ack 1 win 32120 <OF> [tos 0x10]
```

当您按下 Ctrl+C 时，转储将停止。

如您所见，`tcpdump` 默认将 IP 地址转换为主机名，将端口号转换为服务名。它还尝试解释一些数据包（例如行尾以 `lookuo [nfs]` 结尾的数据包，这是 NFS 查找）。在某些情况下，`tcpdump` 查看的字节数（68）可能不足以完全解码数据包。在这种情况下，您可以使用 `-s` 选项来增加这个数值（参见表 20.5 中的 `-s` 选项）。

您并不总是希望看到所有数据包，尤其是在中大型网络中。有时您只想查看两个特定主机之间的所有数据包，甚至只想查看使用特定服务的数据包。`tcpdump` 接受一个可选的过滤表达式作为参数，该表达式将只选择特定的数据包。

`tcpdump` 的过滤表达式由一个或多个原语组成，这些原语通过关键字 `and`、`or` 和 `not` 连接。每个原语由一个限定符和一个 ID 组成。限定符由一个或多个关键字组成，其中最常见的是表 20.4 中所示的。ID 指定对应字段必须具有的值才能匹配过滤器。
