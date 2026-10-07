
```
PING (10.0.0.10) : data bytes
64 bytes from ping (10.0.0.10): icmp_seq=1 ttl=255 time=0.351 ms
64 bytes from ping (10.0.0.10): icmp_seq=2 ttl=255 time=0.445 ms
64 bytes from ping (10.0.0.10): icmp_seq=3 ttl=255 time=0.409 ms
64 bytes from ping (10.0.0.10): icmp_seq=4 ttl=255 time=0.457 ms
64 bytes from ping (10.0.0.10): icmp_seq=5 ttl=255 time=0.401 ms
64 bytes from ping (10.0.0.10): icmp_seq=6 ttl=255 time=0.405 ms
64 bytes from ping (10.0.0.10): icmp_seq=7 ttl=255 time=0.443 ms
64 bytes from ping (10.0.0.10): icmp_seq=8 ttl=255 time=0.384 ms
64 bytes from ping (10.0.0.10): icmp_seq=9 ttl=255 time=0.365 ms
64 bytes from ping (10.0.0.10): icmp_seq=10 ttl=255 time=0.367 ms
```

```
--- ping statistics ---
10 packets transmitted, 10 packets received, 0% packet loss, time 901ms
rtt min/avg/max/mdev = 0.351/0.402/0.457/0.042 ms
```

每当发送并接收返回包时，都会打印一行输出。它显示了发送了多少数据以及接收每个包花费的时间。观察一段时间后，按下 `Ctrl+C` 停止 `ping`。此时，你将看到关于传输、接收和丢失数据包数量的统计。

如果你没有看到显示已接收包的输出，意味着你没有连接到另一台电脑。尝试验证你想要访问的电脑名称和地址是否在 `/etc/hosts` 文件中，或者你的 DNS 服务器是否可以访问。接下来，确认你尝试访问的其他电脑的名称和 IP 地址是正确的（IP 地址是最关键的）。

### 你的以太网连接正常吗？

使用 `ifconfig` 命令，你可以判断以太网（以及其他网络接口）是否处于运行状态。输入以下命令：

```bash
# ifconfig
```

出现的输出类似于所示：

```
eth0 Link encap:Ethernet HWaddr 00:90:24:E:67:35
inet addr:10.0.0.10 Bcast:10.0.0.255 Mask:255.255.255.0
UP BROADCAST,156 RUNNING MULTICAST MTU:1500 Metric:1
RX packets:16 errors:0 dropped:0 overruns:0 frame:0
TX packets:104 errors:0 dropped:0 overruns:0 carrier:0 txqueuel:100
RX bytes:20179 (19.7 Kb) TX bytes:19960 (19.4 Kb)
Interrupt:11 Base address:0xe000 Memory:ff000-ff038
lo encap:Loopback
inet addr:127.0.0.1 Mask:255.0.0
UP RUNNING MTU:3924 Metric:1
RX packets:56 errors:0 dropped:0 overruns:0 frame:0
TX packets:56 errors:0 dropped:0 overruns:0
```

在此示例中，当前有两个网络接口处于开启状态。第一部分显示你的以太网接口（`eth0`）以及它的硬件地址、IP 地址和网络掩码。下一行提供了发送的数据包以及错误和冲突的数量。

> 注意：`lo` 项是回环接口。这允许你在没有物理网络的情况下在本地系统运行 TCP/IP 连接。

如果 `eth0` 接口没有出现，它可能已正确配置但尚未运行。尝试通过以下命令启动 `eth0` 接口：

```bash
# ifconfig eth0 up
```

之后，使用 `ifconfig` 查看 `eth0` 是否正在运行。如果是的话，它可能没有配置为在启动时自动启动。你可以使用本文介绍的网络配置窗口来更改它。

> 提示：如果你的网络接口完全没有运行，尝试从网络初始化脚本启动它们：

```bash
# /etc/init.d/network restart
```

获取以太网驱动统计信息的另一种方法是列出 `/proc/net/dev` 文件的内容。输入：

```bash
# cat /proc/net/dev
```

输出应该如下所示：

| Interface | Receive | Transmit |
|---|---|---|
| lo | 5362 64 0 0 5362 64 0 0 |
| sit0 | 0 0 0 0 0 0 0 0 |
| eth0 | 3083 35 0 0 3876 31 0 |

输出有点难读（宽度不足以显示完整内容）。通过此输出，你可以看到通信中发生的接收和发送错误。

要更详细地查看你的网络，可以使用 Wireshark。Wireshark 在本文后面的“使用 Wireshark 观察 LAN 流量”章节介绍。

> 注意：`sit0` 接口（代表 Simple Internet Transition）可将 IPv6 数据包封装进 IPv4 网络。这允许 IPv6 网络通信跨越 IPv4 网络。如果你启用了 IPv6，可以使用此接口。

### 无线局域网故障

如果你设置了两个（或多个）无线网卡让 Fedora 系统通信，但它们无法通信，你可以通过几种方法排除故障。

#### 检查配置设置

你可以使用 `iwconfig` 和 `ifconfig` 命令检查你的无线设置。`ifconfig` 命令提供无线设置的概述，而 `iwconfig` 命令显示你指定的参数信息。

使用带有无线局域网接口名称的 `ifconfig` 命令查看该接口的信息。例如，如果是无线接口你可以输入：

```bash
# ifconfig eth0
eth0      IEEE 802.11-DS ESSID:"Homelan" Nickname:"pine"
          Mode:AdHoc Frequency:2.412GHz Cell: 02:02:2D:2D:3B:30
          Bit Rate=11Mbps/s Tx-Power=15 dbm Sensitivity:1/3
          RTS:off Fragment:off
          Encryption key:7365-6375-31
          Power Management:off
          Link Quality:0/92 Signal level:-102 dB Noise level:-102 dB
          RX invalid:0 invalid crypto:0 invalid misc:0
```

通过 `ifconfig`你可以看到以太网接口无线方面的细节。在此示例中，网络名称（ESSID）是 Homelan，站名（Nickname）是 pine。该接口在通道1（频率2.412 GHz）上以 Ad hoc 模式运行。传输速率为11 Mbps的最大速度。每个节点网卡必须使用的加密密钥为7365-6375-31。其他设置描述了链路和信号质量。

`iwconfig` 命令允许你请求无线局域网接口的特定信息。语法是在 `iwconfig` 命令后跟随接口名称和你感兴趣的信息。例如：

```bash
# iwconfig eth0 freq
eth 0  14 channels in total; available frequencies :
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

`freq` 参数显示了用于通信的可用频率（通道）。注意，所有可用频率都在2.4 GHz 范围内。

```bash
# iwconfig eth0 rate
```

# 第四部分：Fedora 网络与服务器设置

| eth0 | 4 个可用比特率： |
| :--- | :--- |
| | 1 Mb/s |
| | 2 Mb/s |
| | 5.5 Mb/s |
| | 11 Mb/s |

上述速率参数决定了无线接口可用的传输速率。你可以看到当前接口支持 1、2、5.5 和 11 Mbps 的速率。

```
# iwlist eth keys
eth0 2 key sizes : 40, 104bits
4 keys available :
[1] 7365-6375-31 (40 bits)
[2] off
[3] off
[4] off
Current Transmit Key: [1]
```

这些关键参数可以让你看到该接口可用的加密密钥。它还显示了当前可用的密钥大小。由于上一个一个示例中的网卡支持 64 位和 128 位加密，可用的密钥大小为 40 位和 104 位。加密算法会自动生成每个密钥的最后 24 位。

如果你正在排查无线局域网连接，某些设置比其他设置更容易引起问题。正确设置以下无线局域网设置非常重要——如果不这样做，可能会导致你的网络无法工作：

- **网络 ID (ESSID)** —— 如果每台电脑上的网络 ID (ESSID) 不匹配，节点计算机之间可能无法通信。网络 ID 是敏感的——例如，Mylan 和 MyLAN 是不同的。

- **加密密钥** —— 使用不匹配的加密密钥就像使用错误的密码登录 Linux。检查所有节点是否都使用了相同的密钥。

- **模式 (Mode)** —— 如果你通过接入点进行通信，你的模式应设置为 Managed（托管模式），并且必须提供该接入点的 MAC 地址。在大多数单小区网络中，你应该将所有节点设置为 Ad hoc（自组织模式）。Ad hoc 模式允许所有节点作为对等节点直接通信。

- **通道或频率** —— 通道和频率选项是设置相同值的两种不同方法。例如，将通道设置为 1 等同于将频率设置为 2.412G (GHz)。确保你网络上的节点能够在相同的频率上通信。

# 检查 TCP/IP

为了确保你的无线局域网正在与其节点通信，请使用 `ping` 命令（如本章前面的描述）。如果你认为你的网卡工作正常，但 `ping` 命令持续返回“Network Unreachable”（网络不可达）消息，那么你的 TCP/IP 配置可能存在问题。你可以从 `/Network Configuration` 窗口检查以下项目：

- **IP 地址** —— 知道你尝试访问的节点的正确 IP 地址。

- **主机名 (Host name)** —— 如果你通过名称 `ping` 节点计算机，请确保你的计算机可以将该名称解析为正确的 IP 地址，或者节点的主机名和 IP 地址正确列在本地的 `/etc/hosts` 文件中。前者选项可能需要你识别一个或多个 DNS 服务器来解析名称。

如果你可以访问无线局域网上的另一台电脑，但无法访问该局域网外的电脑（如互联网地址），请检查你是否正确识别了网关的位置。如果网关地址正确且你可以到达该网关，可能是网关本身没有配置为允许数据包转发。

如果你发现上述任何信息需要更改并已进行了更改，你应该重启无线局域网接口。其中一种方法是按照如下方式重启 PCMCIA 接口和网络接口：

```
# /etc/init.d/pcmcia restart
# /etc/init.d/network restart
```

# 适应不良信号接收

当电脑在同一张桌子上分开时，你的无线局域网可能运行良好。但如果性能下降，你可能需要识别任何潜在的障碍物。然后你必须决定如何绕过它们：对于桌面级系统，小型室内天线可以将信号从桌子下或柜子里引出来。对于相邻建筑，屋顶天线可能是解决方案。

在城市或拥挤区域，许多人员和设备可能会竞争 2.4 GHz 频段。你可能需要离开微波炉或高端远程电话，这些设备可能会干扰你的无线局域网。这些设置可能有助于适应不良信号接收：

- **降低传输速率** —— 与其使用 11 Mbps，你可以显式地降到 5.5、2 或 1 Mbps。较慢的速率意味着在嘈杂环境中运行更高效。

- **使用更小的分片大小** —— 虽然传输分成更小分片的数据包会有总开销，但在嘈杂环境中它们通常能提供更好的性能。更改 `frag` 参数以减小分片大小。

- **使用不同的频率** —— 通过专门请求使用某些频率（或通道）进行传输，你可以避开拥堵通道。

# 使用调试工具

由于大多数无线局域网卡是为 Windows 系统设计的，制造商提供的调试工具仅在这些系统上可用。如果你的电脑是双系统（Windows 和 Linux），请尝试进入 Windows 来测试你的无线网络质量。

在 Fedora 中，你可以使用许多用于以太网网络和其他 TCP/IP 网络接口的工具。这里有几个例子：

- **Ethereal** —— `Ethereal` 窗口（在终端窗口中以 root 用户输入 `ethereal`）可以让你观察无线局域网接口发送和接收的 Ethereal 帧。例如，Ethereal 的输出可以告诉你连接失败是因为缺乏拒绝还是请求被拒绝。（Ethereal 在下节中描述。）

- **/var/log/messages** —— 当网络接口启动时，相关消息设置在 `/var/log/messages` 中。在某些情况下，这些消息会反映错误的设置。

# 使用 Ethereal 观察局域网流量

如果你真的想了解局域网进出的信息，你需要一个分析流量的工具。Ethereal 是一个用于捕获和显示跨越你的网络接口的数据包的图形工具。通过过滤器选择特定的主机、协议或数据方向，你可以监控网络问题。

除了读取 Ethereal 获取的以太网数据外，Ethereal 窗口还可以显示来自 LanAnalyzer、Sniffer、Microsoft Network Monitor、Snoop 等工具的文件。这些文件可以以原始格式读取，也可以在压缩 (.gz) 后读取。

Ethereal 可以跟踪超过 100 种数据类型（代表不同的协议）。它还可以显示与每个类型相关的字段，如源地址和端口号。

# 启动 Ethereal

要启动 `ethereal`，请在终端窗口输入以下命令：

```
# ethereal &
```

出现如图 15-1 所示窗口（如果找不到 `ethereal` 命令，可能未安装该包）。Ethereal 的主要功能是对跨接口的数据包拍摄快照。你可以根据各种列对数据进行过滤。显然，你可以将数据保存到文件中以便稍后研究。

> **提示：** 如果由于没有 GUI 而无法使用 Ethereal，可以在 shell 中使用 `tcpdump` 命令。它没有 Ethereal 那么友好，但支持一些基础过滤。（过滤信息请参见 `man tcpdump`。）

# 捕获以太网数据

在显示 Ethereal 窗口时，可以通过以下步骤捕获与任何以太网网络接口数据包活动相关的数据：

1. 点击 Capture

2. 点击 Start。出现 Ethereal Capture Options 窗口。

3. 点击 Interface 框旁的向下箭头查看哪些接口可用，并选择一个。如果你只有一个以太网卡，选择 `eth0` 以捕获跨越该卡的数据。你还可以选择监控接口以观察环回设备。

## 4. 选择其他与数据采集相关的选项：

- **限制每个数据包 (Limit each packet to)**：将每个数据包的大小限制为最大字节数。

- **以混杂模式采集数据包 (Capture packets in promiscuous mode)**：局域网上的任何计算机都可以看到通过局域网的所有包，但交换部分除外。开启此项后，网络接口看到的所有包都将被采集。关闭此项后，只有专门发送你的网络接口的数据包（包括组播和广播包）会被采集。换句话说，开启混杂模式可以监控整个局域网，关闭则仅监控你的接口。

- **过滤器 (Filter)**：此可选字段允许你输入一个过滤器来过滤采集的数据。你可以单独输入过滤器，或点击 Filter 按钮使用之前存储的过滤器。

**交叉引用**：过滤是 Ethereal 最强大的功能之一。有关如何在 Filter 字段中输入过滤器的更多信息，请参阅侧栏的“Using Ethereal Filters”。

- **采集文件 (Capture file(s))**：输入你想要存储采集数据的文件名。如果不输入文件名，信息将显示在 Ethereal 窗口中，而不会保存到文件中。

- **使用环形缓冲区（文件数量）（Use ring buffer (Number of files))**：选择此选项可以在多个文件中采集数据包。要使用此功能，你必须指定文件名（如 `/tmp/abc`）和文件大小。数据将存放在以你提供的根文件名命文件中。一旦文件满了，Ethereal 将返回重新写入第一个文件并继续填充。当你停止采集时，将保留你所选择的数量采集文件，其中包含了最新数据。
