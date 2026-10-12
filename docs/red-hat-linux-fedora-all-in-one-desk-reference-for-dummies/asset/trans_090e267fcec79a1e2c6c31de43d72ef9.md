
/sbin/ifconfig
eth0  Link encap:Ethernet HWaddr 02:60:8C:8E:C6:A9
      inet addr:192.168.0.5  Bcast:192.168.0.255 Mask:255.255.255.0
      UP BROADCAST NOTRAILERS RUNNING MULTICAST  MTU:1500  Metric:1
      RX packets:8104  errors:0  dropped:0  overruns:0  frame:1
      TX packets:1273  errors:0  dropped:0  overruns:0  carrier:0
      collisions:4  txqueuelen:100
      RX bytes:869342 (848.9 Kb)  TX bytes:232276 (226.8 Kb)
      Interrupt:5  Base address:0x300

lo    Link encap:Local Loopback
      inet addr:127.0.0.1  Mask:255.0.0.0
      UP LOOPBACK RUNNING  MTU:16436  Metric:1
      RX packets:94  errors:0  dropped:0  overruns:0  frame:0
      TX packets:94  errors:0  dropped:0  overruns:0  carrier:0
      collisions:0  txqueuelen:0
      RX bytes:6184 (6.0 Kb)  TX bytes:6184 (6.0 Kb)

此输出显示，当前系统上有两个网络接口处于活动状态——回环接口（lo）和以太网卡（eth0）。对于每个接口，都可以看到 IP 地址，以及发送和接收数据包的统计信息。如果 Red Hat Linux 系统上有拨号 PPP 链接正在运行，则输出中还会看到 ppp0 接口的条目。

## 检查 IP 路由表

另一个网络配置命令 /sbin/route，在不带任何命令行参数运行时也会提供状态信息。如果您在检查到另一个主机（使用 IP 地址指定）的连接时遇到问题，请检查 IP 路由表，查看是否指定了默认网关。然后检查网关的路由表，以确保通往外部网络的路径出现在该路由表中。

/sbin/route 命令的典型输出如下：

/sbin/route
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
192.168.0.0     *               255.255.255.0   U     0      0      0     eth0
127.0.0.0       *               255.0.0.0       U     0      0      0     lo
default         192.168.0.1     0.0.0.0         UG    0      0      0     eth0

如该路由表所示，本地网络使用 eth0 以太网接口，默认网关也是该以太网接口。默认网关是处理发往 Red Hat Linux 系统所在网络以外任何网络的数据包的路由设备。在此示例中，发往除以 192.168.0 开头的网络地址之外的任何网络地址的数据包都会发送到网关——192.168.0.1。网关会将这些数据包转发到其他网络（当然，前提是网关已连接到另一个网络，最好是 Internet）。

## 检查主机连通性

要检查到特定主机的网络连接，请使用 ping 命令。ping 命令是广泛使用的 TCP/IP 工具，它使用一系列 Internet 控制消息协议（ICMP，读作 eye-comp）消息。ICMP 提供了 Echo 消息，每台主机都会对其作出响应。利用 ICMP 消息和回复，ping 可以确定另一系统是否存活，并计算与该系统通信的往返延迟。

以下示例展示了我如何运行 ping 来查看网络上的系统是否存活：

```
ping 192.168.0.1
```

这是在我的家庭网络上该命令的显示内容：

```
PING 192.168.0.1 (192.168.0.1) from 192.168.0.7: 56(84) bytes of data.
64 bytes from 192.168.0.1: icmp_seq=1 ttl=254 time=1.36 ms
64 bytes from 192.168.0.1: icmp_seq=2 ttl=254 time=1.23 ms
64 bytes from 192.168.0.1: icmp_seq=3 ttl=254 time=1.36 ms
64 bytes from 192.168.0.1: icmp_seq=4 ttl=254 time=1.34 ms

--- 192.168.0.1 ping statistics ---
4 packets transmitted, 4 received, 0% loss, time 3026ms
rtt min/avg/max/mdev = 1.338/1.352/1.366/0.038 ms
```

在 Red Hat Linux 中，ping 会一直运行，直到您按 Ctrl-C 停止它；然后它会显示摘要统计信息，显示在两个系统之间发送数据包的典型时间。在某些系统上，ping 只是报告远程主机是否存活。但是，您仍可使用适当的命令行参数获取时序信息。

## 检查网络状态

要检查网络状态，请使用 netstat 命令。该命令显示各种类型网络连接的状态（例如 TCP 和 UDP 连接）。可使用 netstat -i 快速查看接口状态，如下所示：

netstat -i
Kernel Interface table
Iface MTU Met RX-OK RX-ERR RX-DRP RX-OVR TX-OK TX-ERR TX-DRP TX-OVR Flg
eth0 1500 0 1678 0 0 0 651 0 0 0 BMNRU
lo 16436 0 50 0 0 0 50 0 0 0 LRU

在此情况下，输出显示了回环和以太网接口的当前状态。表 4-2 描述了各列的含义。

**表 4-2 内核接口表中各列的含义**

| 列 | 含义 |
|---|---|
| Iface | 接口名称 |
| MTU | 最大传输单元 — 数据包可包含的最大字节数 |
| RX-OK, TX-OK | 接收（RX）或发送（TX）的无错误数据包数量 |
| RX-ERR, TX-ERR | 带有错误的数据包数量 |
| RX-DRP, TX-DRP | 被丢弃的数据包数量 |
| RX-OVR, TX-OVR | 因溢出而丢失的数据包数量 |
| Flg | A = 接收多播；B = 允许广播；D = 调试已打开；L = 回环接口（注意 `lo` 上的标志）；M = 接收所有数据包，N = 避免尾部；O = 此接口上无 ARP，P = 点对点接口；R = 接口正在运行；U = 接口已启动。 |

netstat 的另一个有用选项形式是 -t，它显示所有活动的 TCP 连接。以下是某台 Red Hat Linux PC 上 netstat -t 的典型结果：

```
netstat -t
Active Internet connections (w/o servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State
tcp   0    0 dhcpcp4:1031    www.redhat.com:http     ESTABLISHED
tcp   0    126 dhcpcp4:telnet  192.168.0.6:1238        ESTABLISHED
tcp   0    0 dhcpcp4:1032    www.redhat.com:https    ESTABLISHED
tcp   0    0 dhcpcp4:1033    www.redhat.com:https    ESTABLISHED
tcp   0    0 dhcpcp4:telnet  192.168.0.6:1238        ESTABLISHED
tcp   0    0 dhcpcp4:ftp     192.168.0.6:1548        TIME_WAIT
```

在此情况下，输出列显示协议（Proto）；接收和发送队列中的字节数（Recv-Q、Send-Q）；本地 TCP 端口，格式为主机名:服务（Local Address）；远程端口（Foreign Address）；以及连接状态。

输入 netstat -la 可查看所有 TCP 连接——包括活动连接以及 Red Hat Linux 系统正在监听但尚未建立连接的连接。例如，以下是 netstat -ta 命令的典型输出：

```
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State
tcp   0    0 *:1024                *:*                     LISTEN
tcp   0    0 localhost.localdom:1025 *:*                     LISTEN
tcp   0    0 *:sunrpc              *:*                     LISTEN
tcp   0    0 *:x11                 *:*                     LISTEN
tcp   0    0 *:ftp                 *:*                     LISTEN
tcp   0    0 *:ssh                 *:*                     LISTEN
tcp   0    0 *:telnet              *:*                     LISTEN
```

```
tcp 0 0 localhost.localdom:smtp *: * LISTEN
tcp 0 138 dhcppc3:telnet dhcppc4:1037 ESTABLISHED
tcp 0 0 dhcppc3:ftp dhcppc4:1060 ESTABLISHED
```

## 嗅探网络数据包

嗅探网络数据包——听起来像是非法行为，对吧？并非如此。嗅探只是指查看 TCP/IP 网络数据包。概念是捕获所有网络数据包以便稍后检查。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_368_0.png)

如果您想嗅探 TCP/IP 数据包，可以使用 tcpdump，这是一个随 Red Hat Linux 提供的命令行实用程序。顾名思义，它会“转储”（打印）TCP/IP 网络数据包的头部。

要使用 tcpdump，请以 root 身份登录并在终端窗口中输入 tcpdump 命令。通常，您希望将输出保存到文件中以便稍后检查。否则，tcpdump 会开始输出结果，瞬间闪过窗口。例如，要捕获 1,000 个数据包到名为 tdout 的文件中并尝试将 IP 地址转换为名称，请输入以下命令：

```
tcpdump -a -c 1000 > tdout
```

捕获 1,000 个数据包后，tcpdump 会退出。然后您可以检查输出文件 tdout。它是一个文本文件，因此您可以直接在文本编辑器中打开它，或输入 more tdout 来查看捕获的数据包。

为了满足您的好奇心，以下是 tcpdump 典型输出中的几行：

```
20:39:56.929241 dhcppc3.telnet > 192.168.0.6.4272: P 3225722544:3225722572(28)
 ack 1449012018 win 5840 (DF) [tos 0x0]
20:39:57.120308 192.168.0.6.4272 > dhcppc3.telnet: . ack 28 win 16199 (DF)
20:39:57.155930 arp who-has 192.168.0.1 tell dhcppc6
20:39:57.166515 arp reply 192.168.0.1 is at 0:0:c5:e1:3e:ae
20:39:57.169596 dhcppc6.1025 > 192.168.0.1.domain: 33598+ PTR? 6.0.168.192.in-addr.arpa. (42) (DF)
20:39:57.838984 192.168.0.1.domain > dhcppc6.1025: 33598 NXDomain* 0/1/0 (119) (DF)
20:39:57.840892 dhcppc6.1025 > 192.168.0.1.domain: 33599+ PTR? 1.0.168.192.in-addr.arpa. (42) (DF)
20:39:57.885757 192.168.0.1.domain > dhcppc6.1025: 33599 NXDomain 0/1/0 (119) (DF)
20:40:05.513863 192.168.0.1.router > 192.168.0.255.router: RIPV1-resp [items 2]:
 (0.0.0.0)(1) [68.49.48.0](1) [ttl 1]
... lines deleted...
```

输出确实提供了一些线索——每一行显示一个网络数据包的信息。每一行以时间戳开头，后跟数据包的详细信息，例如其来源和去向。我不会在这里尝试解释细节，但您可以输入
