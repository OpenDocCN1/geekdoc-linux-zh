

这里我们看到了本地主机与远程主机之间的 20 台路由器。输出的每一行代表通往远程主机路径上的一个跃点。对于每个跃点，我们会看到主机名（如果有）、网关路由器的 IP 地址，以及到达该主机的三个采样往返时间。这三个时间是通过发送三个数据包并报告直到收到返回的错误数据包所经历的时间而得到的。如果没有错误数据包返回，则在相应位置显示一个星号：

```
# traceroute ftp.is.co.za
traceroute to ftp.is.co.za (196.4.160.12), 30 hops max, 40 byte packets
 1 cstr001 (10.0.25.4) 1.906 ms 1.677 ms 1.657 ms
 2 atcr001 (10.0.2.1) 1.720 ms 1.644 ms 1.608 ms
 3 fw-nat (10.0.0.1) 1.014 ms * *
 4 rtgate (192.115.144.181) 3.561 ms 3.327 ms 3.342 ms
 5 tlv-fe10.netvision.net.il (199.203.4.200) 15.325 ms 19.331 ms 15.053 ms
 6 nyc-s4-0-4.n0002.netvision.net.il (194.90.0.85) 367.383 ms 336.807 ms 374.334 ms
 7 nj-nyc0-H5-0-1.netvision.net.il (194.90.0.89) 387.460 ms 375.801 ms 369.297 ms
 8 serial0-1-1.gw2.har1.alter.net (157.130.25.245) 374.683 ms 393.632 ms 374.661 ms
 9 422.ATM9-0-0.GW1.HAR1.ALTER.NET (137.39.30.249) 377.170 ms 373.443 ms 448.300 ms
10 136.Hss19-0.HR2.NYC2.ALTER.NET (137.39.69.49) 401.138 ms 392.110 ms 441.235 ms
11 442.ATM3-0.XR1.NYC1.ALTER.NET (146.188.177.34) 397.832 ms 391.710 ms 398.259 ms
12 195.ATM6-0.XR1.NYC4.ALTER.NET (146.188.178.82) 417.984 ms 394.524 ms 389.993 ms
13 189.ATM9-0-0.GW4.NYC4.ALTER.NET (146.188.179.161) 398.030 ms 399.579 ms 393.061 ms
14 iscoza-gw.customer.alt.net (157.130.22.182) 388.323 ms 399.139 ms 393.250 ms
15 168.209.0.129 (168.209.0.129) 956.494 ms 966.903 ms 969.841 ms
16 168.209.100.8 (168.209.100.8) 973.092 ms 963.411 ms 945.400 ms
17 * * *
18 * * *
19 * * *
20 * * *
```

这一连串的星号表示无法到达远程主机，且跟踪已经中断。这表明在成功跃点列表中的最后一个网关之后存在路由问题或网络故障。如果最后一个路由器在你的控制之下，那么你已经找到了一个问题点，可以由此开始查找通信问题的根源。

## 使用 netstat

netstat 命令显示当前的网络状态。它有许多选项可用于过滤状态数据。最有用的 netstat 选项在表 13.5 中概述。

### 表 13.5 选定的 netstat 选项

| 选项 | 描述 |
|---|---|
| `-a` | 显示所有活动的网络连接及其状态 |
| `-i` | 显示每个网络接口的摘要信息 |
| `-s` | 按协议排序显示数据包摘要 |
| `-r` | 显示路由表及其状态的信息 |
| `-c` | 每秒更新并显示连续输出 |
| `-N` | 显示有关接口或路由创建或删除的消息 |

netstat 的默认操作是列出打开的套接字来显示网络连接的状态。下面的示例输出显示了协议、发送和接收队列、本地主机名或 IP 地址、远程主机名或 IP 地址，以及每个打开连接的状态：

```text
# netstat
Active Internet connections (w/o servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State
tcp        0      0 cstlx001.bwc.org:8083  mcpsw099.bwc.org:4185  TIME_WAIT
tcp        0      0 cstlx001.bwc.org:8083  allws025.bwc.org:3533  TIME_WAIT
tcp        0      0 cstlx001.bwc.org:8083  sjwjs159.bwc.org:1669  TIME_WAIT
tcp        0      0 cstlx001.bwc.org:8083  allws057.bwc.org:2542  TIME_WAIT
tcp        0      0 cstlx001.bwc.org:8083  allws057.bwc.org:2541  TIME_WAIT
tcp        0      0 cstlx001.bwc.org:8083  allws057.bwc.org:2540  TIME_WAIT
tcp        0      2 cstlx001.bwc.org:telnet 192.115.144.86:1034   ESTABLISHED
tcp        0      0 cstlx001.bwc.org:telnet 192.115.144.72:1030   ESTABLISHED
tcp        0      0 cstlx001.bwc.org:telnet 192.115.144.76:1028   ESTABLISHED
tcp        0      0 localhost:3410          localhost:3411          ESTABLISHED
tcp        0      0 localhost:3411          localhost:3410          ESTABLISHED
tcp        0      0 localhost:3408          localhost:3409          ESTABLISHED
tcp        0      0 localhost:3409          localhost:3408          ESTABLISHED
tcp        0      0 localhost:3406          localhost:3407          ESTABLISHED
tcp        0      0 localhost:3407          localhost:3406          ESTABLISHED
tcp        0      0 localhost:3404          localhost:3405          ESTABLISHED
tcp        0      0 localhost:3405          localhost:3404          ESTABLISHED
tcp        0      0 localhost:3402          localhost:3403          ESTABLISHED
tcp        0      0 localhost:3403          localhost:3402          ESTABLISHED
Active UNIX domain sockets (w/o servers)
Proto RefCnt Flags       Type       State     I-Node Path
unix  1      [ ]         STREAM     CONNECTED 606442 @0000000d
unix  1      [ ]         STREAM     CONNECTED 486    @0000001d
unix  1      [ ]         STREAM     CONNECTED 606860 @0000007e
unix  1      [ ]         STREAM     CONNECTED 566507 @0000000a
unix  1      [ ]         STREAM     CONNECTED 606804 @000000e2
unix  1      [ ]         STREAM     CONNECTED 767    @00000030
unix  0      [ ]         STREAM     CONNECTED 134    @00000015
unix  1      [ ]         STREAM     CONNECTED 564    @00000023
unix  1      [ ]         STREAM     CONNECTED 608661 /dev/log
unix  1      [ ]         STREAM     CONNECTED 606805 /dev/log
unix  1      [ ]         STREAM     CONNECTED 606443 /dev/log
unix  1      [ ]         STREAM     CONNECTED 566508 /dev/log
unix  1      [ ]         STREAM     CONNECTED 768    /dev/log
unix  1      [ ]         STREAM     CONNECTED 623    /dev/log
unix  1      [ ]         STREAM     CONNECTED 487    /dev/log
```

-i 选项可用于提供有关本地网络的有用诊断信息：

```text
# netstat -i
Kernel Interface table
Iface  MTU   Met  RX-OK  RX-ERR  RX-DRP  RX-OVR  TX-OK  TX-ERR  TX-DRP  TX-OVR  Flg
eth0   1500  0    4253182  0      0       0       4355313  0       0       0       BRU
lo     3924  0    48448    0      0       0       48448   0       0       0       LRU
```

在此示例中，为每个网络接口显示了输出。对于每个接口，发送和接收错误的数量分别显示在 TX-ERR 和 RX-ERR 列中。通常，这两个值应为零或接近零。如果你看到任何一列中出现较大数字或不断增长的值，这很可能是网络问题的强烈迹象，例如本地网络饱和、网络接口故障或线缆缺陷。

在 Linux 和大多数其他 Unix 系统上，-r 选项会使 netstat 显示有关路由表的信息：

```text
$ netstat -r
Kernel IP routing table
Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface
10.2.0.244      *               255.255.255.255 UH      0   0        0    eth0
10.2.0.0        *               255.255.0.0     U       0   0        0    eth0
127.0.0.0       *               255.0.0.0       U       0   0        0    lo
default         cstrt001        0.0.0.0         UG      0   0        0    eth0
```

在此示例输出中，Destination 列指示为其定义路由的主机或网络。Gateway 列指示与该主机或网络通信时需要使用的网关（如果有）。

最后一行显示默认路由。默认路由是一个兜底路由。每当没有到某个目标的具体路由时，数据包就会被发送到默认路由器或网关。在上面的示例中，cstrt001 是默认路由器。请注意，此条目的 Flags 列的值为 UG。U 表示该路由是启用的（即可用的），G 表示该路由使用网关。

## 使用 `ifconfig`

如前文关于手动网络配置一节所述，`ifconfig` 用于配置网络接口。在启动时，脚本 `/etc/rc.d/init.d/network` 会调用 ifconfig 来按需设置接口。之后，它可以用于故障排除和调试。它还可以用于调整某些网络接口参数。

当不带任何参数调用时，`ifconfig` 会显示当前活动网络接口的状态。如果给定一个接口参数，则仅显示该接口的状态。如果使用 -a 选项调用，则显示所有接口的状态，包括已停用的接口。

下面显示了 `ifconfig -a` 的示例输出：

```text
# /sbin/ifconfig -a
eth0      Link encap:Ethernet  HWaddr 00:80:5F:6D:CF:C2
          inet addr:10.2.0.244  Bcast:10.2.255.255  Mask:255.255.0.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:4261292 errors:0 dropped:0 overruns:0 frame:0
          TX packets:4363313 errors:0 dropped:0 overruns:0 carrier:0
```

