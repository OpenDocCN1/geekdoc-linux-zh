
`key` 参数允许你查看该接口可用的加密密钥。它还显示了当前可用的密钥大小。由于上一个示例中的网卡支持 64 位和 128 位加密，因此可用的密钥大小为 40 和 104 位（加密算法在数学上生成每个密钥的最后 24 位）。

如果你正在排查无线局域网连接故障，某些设置比其他设置更容易引起问题。正确设置以下无线局域网设置非常重要——否则它们可能会导致你的网络无法工作：

- 网络 ID (`ESSID`) —— 如果任何一台计算机上的网络 ID (`ESSID`) 不匹配，你可能无法在计算机之间进行通信。网络 ID 对大小敏感——例如，`Mylan` 与 `MyLAN` 不同。
- 加密密钥 — 加密密钥不匹配就像用错误的密码登录 Linux。检查所有节点是否使用相同的密钥。（如果节点无法连接，先检查加密密钥。）
- 模式 — 接口在通道 1（频率为 2.412 GHz）上以 `Ad hoc` 模式运行。传输速率为最大速度 1 Mbps。每个节点卡必须使用的加密密钥为 `7365-6375-31`。其他设置描述了链路和信号质量。
- 通道 — 通过专门请求某些频率（或通道）用于传输，你可以避免拥堵的通道。

## 适应接收不佳的情况

当你的电脑放在桌上时，无线局域网可能运行良好。但如果性能下降，你可能需要识别任何障碍物。对于桌面系统，一个小型室内天线可以将信号从桌下或柜子里引出。在城市或其他拥挤区域，许多人员和设备可能会竞争 2.4 GHz 频率。这些设置可能有所帮助：

- 降低传输速率 — 你可以轻松从 11 Mbps 降到 5、2 或 1 Mbps。较慢的速率可以在噪声环境中运行更高效。
- 使用更小的碎片大小 — 虽然将数据包传输成更小的碎片会有更大的开销，但在噪声环境中可以提供更好的整体性能。更改 `frag` 参数以减小碎片大小。
- 使用不同的频率 — 通过专门请求某些频率（或通道）。

## 使用调试工具

由于大多数无线局域网卡是为 Windows 设计的，制造商提供的调试工具仅在这些系统中可用。如果你的电脑是双系统（Windows 和 Linux），尝试启动 Windows 来测试无线网络的质量。

在 Fedora 和 RHEL 中，你可以使用许多用于用于以太网网络和其他 TCP/IP 网络接口的工具。这里有两个例子：

- `Wireshark` — `Wireshark` 窗口（在终端中以 root 用户运行 `wireshark`）允许你观察无线接口发送和接收的以太帧。例如，`Wireshark` 的输出可以告诉你连接失败是因为接收不到信号还是请求被拒绝。（`Wireshark` 将在下一节中介绍。）
- `/var/log/messages` 当无线局域网接口启动时，与启动相关的会被发送到 `/var/log/messages` 文件。在某些情况下，这些消息会反映无线局域网模块设置了不当选项。

## 使用 Wireshark 监控局域网流量

如果你真的想理解局域网中信息的进出，你需要一个分析网络流量的工具。`Wireshark`（原名为 `Ethereal`）是一种用于捕获和显示跨网络接口发送的数据包的图形化工具。使用过滤器

通过选择特定的主机、协议或数据方向，你可以监控网络活动并跟踪网络问题。

除了读取 `Wireshark` 收集的以太网包数据外，`Wireshark` 窗口还可以显示来自 `LanAnalyzer`、`Sniffer`、`Microsoft Network Monitor`、`Snoop` 以及其他工具的捕获文件。这些文件可以以原始格式读取，也可以在经过 `gzip` (`.gz`) 压缩后读取。

`Wireshark` 可以跟踪 100 多种类型的数据包（代表不同的协议）。它还可以显示与每个协议相关的特定字段，例如各种数据类型、源和目的地址、端口和其他值。

### 启动 Wireshark

要从应用程序菜单启动 `Wireshark`，选择 `Internet -> Wireshark Network Analyzer`。或者在终端窗口中（作为 root 用户）输入以下命令：

```
# wireshark &
```

出现如图 15-14 所示的 `Wireshark` 窗口。（如果找不到 `wireshark` 命令，可能未安装该包。你可以通过输入 `yum install wireshark wireshark-gnome` 来安装 `wireshark-wireshark-gnome` 包，或者可以使用 `rpc` 命令从安装 DVD 中安装它们。）

`Wireshark` 的主要功能是对流经网络接口的数据包进行快照，并在 `Wireshark` 窗口中显示这些数据。你可以根据各种过滤原语对数据进行过滤。捕获完成后，你可以根据不同的列对数据进行逐步查看和排序。你可以将捕获的数据保存到文件中，以便以后研究这些数据。

> 提示：如果你因为没有可用 GUI 而无法使用 `Wireshark`，可以使用 shell 中的 `tcpdump` 命令。它没有 `Wireshark` 那么友好，但它支持相同的过滤语法。由于 `tcpdump` 会产生大量输出，你可能希望使用某种形式的过滤或将命令输出重定向到文件。（输入 `man tcpdump` 获取过滤选项的信息。）

### 捕获以太网数据

在显示 `Wireshark` 窗口的情况下，可以通过以下步骤捕获与任何以太网网络接口相关的数据包活动数据：

1. 点击 `Capture -> Interfaces`。你将看到计算机上可用的网络接口列表。
2. 点击你想要捕获的接口旁边的 `Next`（有线网络可能是 `eth0`，无线接口可能是 `wlan0`）。将一个 `Wireshark Capture Options` 窗口。

![](img/ec54a77854df1c8d0311d04a1e6b8d3c_723_0.png)

| No. | Time | Source | Destination | Protocol | Info |
|---|---|---|---|---|---|
| 2 | 10:06:57 | Wireshark_02:ec98 | Broadcast | ARP | who has 10.0.0.107 |
| 3 | 10:11:43 | Wireshark_02:ec98 | Broadcast | ARP | who has 10.0.0.111 |
| 4 | 10:11:639 | Intel_79:a5:35 | Wireshark_02:ec98 | ARP | 10.0.0.111 is at d... |
| 5 | 10:11:792 | 10.0.0.50 | | ICMP | Echo (ping) reply |
| 6 | 11:12:004 | 10.0.0.50 | Broadcast | ICMP | Echo (ping) reply |
| 7 | 10:25:541 | Wireshark_02:ec98 | Broadcast | ARP | who has 10.0.0.107 |
| 8 | 10:22:738 | 10.0.0.50 | Broadcast | ICMP | Echo (ping) reply |
| 9 | 10:31:3366 | 10.0.0.550 10.0.0.55 | ICMP | Echo (ping) reply |
| 10 | 11:35:441 | 10.0.0.50 | 10.0.0.50 | ICMP | Echo (ping) reply |
| 11 | 12:5:27511 | 10.0.0.91 | 224.0.0.23 | DNS | Standard query aaa |
| 12 | 13:26:946 | 10.0.0.91 | 224.0.0.23 | DNS | Standard query aaa |

- Frame 1 (60 bytes on wire, 60 bytes captured)
- Ethernet II; Src: Wireshark_02:ec98; Dst: Broadcast (ff:ff:ff:ff:ff:ff); Type: IPv4 (0x0800) length 60

```
0000  ff ff ff ff ff ff 6a 02 ec 98 00 06 00 00
0010  08 00 45 00 00 3c 00 01 00 00 00 00
0020  6a 02 ec 98 00 06 00 00 40 00 40 06
0030  41 06 00 00 0a 00 00 32 0a 00 00 34
```

3. 选择你想要捕获的接口：

- **Limit of data**：默认情况下，`Wireshark` 将捕获数据直到你停止。
- **Promiscuous mode（混杂模式）**：开启后 `Wireshark` 将捕获接口上的所有数据包。关闭后它只捕获发送给你的机器的数据包。
- **Ring buffer（Number of files）**：使用此选项指定文件名并将捕获的数据写入一组文件。一旦文件满，`Wireshark` 将返回第一个文件。
