
```
64 bytes from pine (10.0.0.10): icmp_seq=10 ttl=255 time=0.367 ms
--- ping statistics ---
10 packets transmitted, 10 packets received, 0% packet loss, time 9011ms
rtt min/avg/max/mdev = 0.351/0.402/0.457/0.042 ms
```

每次发送数据包并收到返回时都会打印一行输出。它显示发送了多少数据以及每个数据包接收所需的时间。观察一段时间后，输入 Ctrl+C 停止 ping。此时，你将看到已传输、已接收和丢失的数据包数量统计信息。

如果你看不到显示数据包已接收的输出，说明你没有联系到另一台计算机。请尝试验证你想要访问的计算机的名称和地址是否在你的 /etc/hosts 文件中，或你的 DNS 服务器是否可访问。接下来，确认你用于尝试访问的其他计算机的名称和 IP 地址是否正确（IP 地址最为关键）。

## 你的以太网连接是否已启动？

使用 ifconfig 命令，你可以确定你的以太网（和其他网络接口）是否已启动并运行。输入以下命令：

```
# ifconfig
```

显示的输出类似于以下内容：

```
eth0 Link encap:Ethernet HWaddr 00:90:27:4E:67:35
    inet addr:10.0.0.10 Bcast:10.0.0.255 Mask:255.255.255.0
    UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
    RX packets:156 errors:0 dropped:0 overruns:0 frame:0
    TX packets:104 errors:0 dropped:0 overruns:0 carrier:0
    collisions:0 txqueuelen:100
    RX bytes:20179 (19.7 Kb)   TX bytes:19960 (19.4 Kb)
    Interrupt:11 Base address:0xe000 Memory:ff8ff000-ff8ff038

lo    Link encap:Local Loopback
    inet addr:127.0.0.1 Mask:255.0.0.0
    UP LOOPBACK RUNNING MTU:3924 Metric:1
    RX packets:56 errors:0 dropped:0 overruns:0 frame:0
    TX packets:56 errors:0 dropped:0 overruns:0 carrier:0
    collisions:0 txqueuelen:0
    RX bytes:3148 (3.0 Kb)    TX bytes:3148 (3.0Kb)
```

在此示例中，当前计算机上有两个网络接口处于启动状态。第一部分显示你的以太网接口（eth0），以及其以太网硬件地址、IP地址（inet addr）、广播地址和网络掩码。接下来的行提供了已发送数据包的信息，以及发生的错误和冲突数量。

> **NOTE:** `lo` 条目用于回环。这使你可以在没有物理网络运行的情况下，在本地系统上运行 TCP/IP 命令。

如果你的 `eth0` 接口没有出现，它可能仍然配置正确，但当前未运行。尝试通过输入以下内容启动 `eth0` 接口：

```
# ifconfig eth0 up
```

之后，再次输入 `ifconfig` 查看 `eth0` 是否已运行。如果是，可能是 `eth0` 只是未配置为在启动时自动启动。你可以使用本章前面描述的网络配置窗口将其更改为在启动时启动以太网（我建议这样做）。

> **TIP:** 如果你的网络接口完全未运行，你可以尝试从网络初始化脚本启动它们。该接口读取参数并基本上为计算机上的所有网络接口运行 `ifconfig`。输入以下内容重启你的网络：

```
# /etc/init.d/network restart
```

查看以太网驱动程序统计信息的另一种方法是列出网络设备进程伪文件系统的内容。为此，输入以下内容：

```
# cat /proc/net/dev
```

输出应如下所示：

| 接口 | 字节 | 数据包 | 错误 | 丢弃 | fifo | 帧 | 压缩 | 多播 | 字节 | 数据包 | 错误 | 丢弃 | fifo | 帧 | 压缩 | 多播 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| lo: | 5362 | 64 | 0 | 0 | 0 | 0 | 0 | 5362 | 64 | 0 | 0 | 0 |  |  |  |  |
| eth0: | 3083 | 35 | 0 | 0 | 0 | 0 | 0 | 3876 | 31 | 0 | 0 | 0 |  |  |  |  |

输出有点难以阅读（我们的书不够宽，无法在不换行的情况下显示，因此输出在右侧被截断）。通过此输出，你可以看到每个接口的接收和发送统计信息。此输出还显示了通信中发生的接收和发送错误数量。（在此示例中，发送信息被截断。）

要更详细地查看你的网络，你可以使用 Ethereal 窗口。Ethereal 在本章后面“使用 Ethereal 监视 LAN 流量”部分有描述。

## 故障排除无线局域网

如果你设置了两张（或更多）无线局域网卡以使 Red Hat Linux 系统能够通信，但它们无法通信，你可以通过几种不同方式进行故障排除。

### 检查无线设置

你可以使用 iwlist 和 iwconfig 命令检查无线设置。iwconfig 命令提供无线设置的快速概览，而 iwlist 命令显示你指定的参数信息。

使用 iwconfig 命令以及无线局域网接口的名称，可以查看该接口的信息。例如，如果无线接口为 eth1，你可以输入以下内容：

```
# iwconfig eth1
eth0    IEEE 802.11-DS  ESSID:"Homedlan"  Nickname:"pine"
      Mode:Ad-Hoc  Frequency:2.412GHz  Cell: 02:02:2D:2D:3B:30
      Bit Rate=11Mb/s  Tx-Power=15 dBm  Sensitivity:1/3
      RTS thr:off    Fragment thr:off
      Encryption key:7365-6375-31
      Power Management:off
      Link Quality:0/92  Signal level:-102 dBm  Noise level:-102 dBm
      Rx invalid nwid:0  invalid crypt:0  invalid misc:0
```

使用 iwconfig，你可以看到以太网接口的无线方面细节。在此示例中，网络名称（ESSID）为 Homedlan，站点名称（Nickname）为 pine。接口在 Ad hoc 模式下于频道 1（频率 2.412 GHz）运行。传输速率达到最大速度 11 Mbps。卡连接的每个节点必须使用的加密密钥为 7365-6375-31。其他设置描述了链路和信号质量。

iwlist 命令让你请求有关无线局域网接口的特定信息。语法是在 iwlist 命令后跟接口名称和你感兴趣的信息。例如：

```
# iwlist eth0 freq
eth0     14 channels in total; available frequencies :  
      Channel 01 : 2.412 GHz
      Channel 02 : 2.417 GHz
      Channel 03 : 2.422 GHz
      Channel 04 : 2.427 GHz
      Channel 05 : 2.432 GHz
      Channel 06 : 2.437 GHz
      Channel 07 : 2.442 GHz
      Channel 08 : 2.447 GHz
      Channel 09 : 2.452 GHz
      Channel 10 : 2.457 GHz
      Channel 11 : 2.462 GHz
```

freq 参数显示可用于通信的可用频率（和频道）。请注意，所有可用频率都在 2.4 GHz 范围内。

```
# iwlist eth0 rate
eth0    4 available bit-rates :
	1 Mb/s
	2 Mb/s
	5.5 Mb/s
	11 Mb/s
```

前面的 rate 参数显示无线接口可用的传输速率。你可以看到当前接口可用的速率为 1、2、5.5 和 11 Mbps。

```
# iwlist eth0 keys
eth0    2 key sizes : 40, 104bits
	4 keys available :
		[1] 7365-6375-31 (40 bits)
		[2] off
		[3] off
		[4] off
	Current Transmit Key: [1]
```

keys 参数让你查看接口可用的加密密钥。它还显示当前可用的密钥大小。由于前面示例中反映的卡支持 64 位和 128 位加密，因此可用的密钥大小为 40 和 104 位。（加密算法会自动生成每个密钥的最后 24 位。）

如果你正在故障排除无线局域网连接，其中一些设置比其他设置更可能导致问题。正确设置以下无线局域网设置非常重要——如果不这样做，它们可能会使你的网络无法工作：

- **网络 ID (ESSID)** — 如果每个对等计算机上的网络 ID (ESSID) 不匹配，你可能无法在它们之间通信。大写字母很重要——例如，Mylan 与 MyLAN 不同。
- **加密密钥** — 加密密钥不匹配就像使用错误的密码登录 Linux 一样。请检查所有节点是否使用相同的密钥。
- **模式** — 如果你通过接入点通信，你的模式应设置为 Managed，并且必须提供该接入点的 MAC 地址。在大多数单小区网络中，你应将所有节点设置为 Ad hoc。Ad hoc 模式允许所有节点作为对等方直接相互通信。
- **频道或频率** — 频道和频率选项只是设置相同值的两种不同方式。例如，将频道设置为 1 与将频率设置为 2.412G（GHz）相同。确保你的网络上的节点能够在同一频率上通信。

### 检查 TCP/IP

为确保你的无线局域网与其对等方通信，请使用 ping 命令（如本章前面所述）。如果你认为你的网卡工作正常，但
