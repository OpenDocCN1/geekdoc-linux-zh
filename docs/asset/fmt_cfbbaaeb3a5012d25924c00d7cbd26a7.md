
```
64 bytes from pine (10.0.0.10): icmp_seq=7 ttl=255 time=0.351 ms

64 bytes from pine (10.0.0.10): icmp_seq=8 ttl=255 time=0.351 ms

64 bytes from pine (10.0.0.10): icmp_seq=9 ttl=255 time=0.351 ms

64 bytes from pine (10.0.0.10): icmp_seq=10 ttl=255 time=0.351 ms

--- ping statistics ---

10 packets transmitted, 10 packets received, 0% packet loss, time 901ms

rtt min/avg/max/mdev = 351/402/447/52 ms
```

每次发送和接收包时都会打印一行输出。它显示发送了多少数据以及花费了多久。观察此后，按 `Ctrl-C` 停止 `ping`。此时你会看到发送、接收和丢失包的统计信息。

如果你没有看到接收包，说明你没有联系上对方计算机。尝试验证 `/etc/hosts` 文件或 DNS 服务器是否可用。接下来确认其他计算机的名称和地址正确（IP 地址最为关键）。

# 你的以太网连接正常？

使用 `ifconfig` 命令可以判断你的以太网（或其他网络接口）是否已运行。输入以下命令：

```
# ifconfig
```

出现的输出是：

```
eth0 Link encap:Ethernet HWaddr 00:27:4E:67:35
  inet addr:10.0.0.10 Bcast:10.0.0.255 Mask:255.255.255.0
UP BROADCAST MULTICAST MTU:1500 Metric:1
RX packets:56 errors:0 dropped:0 overflows:0 frame:
tx packets:104 errors:0 dropped:0 overflows:0 carrier:0
collisions:0 txquelen:100
RX bytes:20179 (19.7 Kb) TX bytes:19960 (19.4 Kb)
Interrupt:1 Base address:0xe800 Memory:ff8ff0-ff808
lo encap:Local Loopback
  inet addr:127.0.0.1 Mask:255.0.0.0
UP LOOPBACK RUNNING MTU:3924 Metric:1
RX packets:56 errors:0 dropped:0 overflows:0 frame:
```

# 第四部分：Fedora 和 RHEL 网络与服务器设置

```
TX packets:56 errors:0 overflows:0 carrier:0
collisions:0 txqueuelen:0
RX bytes:3148 (3.0 Kb) TX bytes:3148 (3.0Kb)
```

在该网络接口已运行。第一部分显示你的以太网接口 `eth0` 以及它的以太网硬件地址、IP 地址 `inet addr`、广播地址和掩码。接下来的行提供了发送包的信息，以及发生的错误和冲突次数。

> 注意：`lo` 条目用于回环。这允许你在没有物理网络运行的情况下在本地系统中运行 TCP/IP 命令。

如果你的 `eth0` 接口没有出现，它可能仍然配置正确，但目前没有运行。尝试通过以下命令启动 `eth0` 接口：

```
# ifconfig eth0
```

此后，再次输入 `ifconfig` 查看 `eth0` 现在是否运行。如果是，可能是 `eth0` 没有配置为启动时自动启动。你可以使用本章之前描述的网络配置窗口设置以太网在启动时启动（我建议这样做）。

> 提示：如果你的网络接口完全没有运行，你可以从网络初始化脚本启动它们。该接口读取参数并基本上为计算机上的所有网络接口运行 `ifconfig`。输入以下命令重启网络：
>
> ```
> # /etc/init.d/network restart
> ```

查看以太网驱动程序统计信息的另一种方法是列出网络设备伪系统的内容。为此，输入以下命令：

```
# /proc/net/dev
```

输出应该如下：

| 接口 | 接收包 | 错误 | 丢弃 | fifo | 帧 | 压缩 | 多播 | 字节 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| lo | 5362 | 64 | 0 | 0 | 0 | 0 | 0 | 5362 |
| sit0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| eth0 | 3083 | 35 | 0 | 0 | 0 | 0 | 0 | 3876 |

# 第15章：建立局域网 639

注意：`sit` 网络接口（代表 Simple Internet Transition，即简单互联网转换）可将 IPv6 数据包封装到 IPv4 网络中。这允许 IPv6 网络通信跨 IPv4 网络进行路由。只有在你启用了 IPv6 网络功能时，才会使用此接口。

## 排除无线局域网故障

如果你设置了两个（或多个）无线局域网卡以启用 Fedora 和 RHEL 系统通信，但它们无法通信，你可以通过几种不同的方法对问题进行排除。

## 检查无线设置

你可以使用 `iwlist` 和 `iwconfig` 命令来检查无线设置。`iwconfig` 命令提供无线设置的快速概览，而 `iwlist` 命令则显示你指定的参数信息。

使用 `iwconfig` 命令配合无线局域网接口名称来查看该接口的信息。例如，如果无线接口是 `eth1`，你可以输入以下内容：

```
eth0 IEEE 802.11-DS ESSID:"Homelan" Nickname:"pine"
Mode:Ad-Off Frequency:2.412GHz Cell: 02:02:2D:2D:3B:30
Rate:11Mb/s Tx-Power:15 dBm Sensitivity:1/3
RTS thr:off Frag thr:off
Encryption key:7365-6375-31
Power Management:off
Link Quality:0/92 Signal level:-102 dBm Noise level:-102 dBm
Rx invalid:0 invalid cryptopt:0 invalid misc:0
```

通过 `iwconfig`，你可以看到以太网接口各个方面的细节。在这个示例中，网络名称（ESSID）是 Homelan，站名（Nickname）是 pine。该接口在信道 1（频率为 2.412 GHz）上以 Ad 模式运行。传输速率达到 11 Mbps 的最大速度。每个节点卡连接时使用的加密密钥为 7365-6375-31。其他设置描述了链路和信号质量。

`iwlist` 命令请求关于无线局域网接口的特定信息。语法是在 `iwlist` 命令后跟随接口名称以及你感兴趣的信息。例如：

```
eth 0 14 channels in total: available frequencies :
Channel 01 : 2.412 GHz
Channel 02 : 2.417 GHz
Channel 03 : 2.422 GHz
Channel 04 : 2.427 GHz
```

```
Channel 05 : 2.432 GHz
Channel 06 : 2.437 GHz
Channel 07 : 2.442 GHz
Channel 08 : 2.447 GHz
Channel 09 : 2.452 GHz
Channel 10 : 2.457 GHz
Channel 11 : 2.457 GHz
Channel 12 : 2.457 GHz
Channel 13 : 2.457 GHz
Channel 14 : 2.462 GHz
Current Frequency:2.412GHz (Channel 1)
```

`freq` 参数显示了可通信的频率（和信道）。注意所有频率都在 2.4 GHz 范围内。

```
# iwlist eth0 rate
eth0 6 available bit-rates :
1Mb/s
2Mb/s
5.5Mb/s
11Mb/s
28Mb/s
39.5Mb/s
Current Bit Rate=54Mb/s
```

前面的 `rate` 参数显示了无线接口的传输速率。你可以看到当前接口支持 1, 2, 5.5 和 11 Mbps 的速率。

```
# iwlist eth0 key
eth0 2 key sizes : 40, 104bits
4 keys available :
[1] 7365-6375-31 (40 bits)
[2] off
```
