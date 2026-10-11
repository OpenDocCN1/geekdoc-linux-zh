
根据 IP 版本过滤，使用 `-i4` (IPv4) 或 `-i6` (IPv6)。你可以将其作为单独选项添加，也可以通过更复杂的过滤器添加数字（例如 `-i6TCP:443`）。你可以指定 `/etc/services` 中的服务名称（如 `-iTCP:ssh`）而不是数字。

### 按连接状态过滤

特别方便的 `lsof` 过滤器是连接状态。例如，仅监听 TCP 端口的进程，输入：

`# lsof -iTCP -sTCP:LISTEN`

此命令让你对系统中运行的网络进程有一个良好的概述。然而，由于 UDP 服务器不监听也没有连接，你必须使用 `-udp` 来查看运行的客户端以及服务器。这不是问题，因为你的系统中不会有很多 UDP 服务器。

### 10.5.2 tcpdump

你的系统通常不理非指向其 MAC 地址的网络流量。如果你需要看到通过你的网络的流量，`tcpdump` 将你的网络网卡设置为混杂模式，并报告每一个通过的数据包。带参数输入 `tcpdump` 会产生如下输出，包含 ARP 请求和连接：

```
# tcpdump
tcpdump: listening on eth0
20:36:25.771304 arp who-has mikado.example.com tell duplex.example.com
20:36:25.774729 reply mikado.example.com is-at 0:2:2d:bee:e4
20:36:25.774796 duplex.example.com.48455: S
3200063165:3200063165(0) win 5840 <ms 1460,sackOK,timestamp 38815804[|tcp|] (DF)
20:36:25.779283 mikado.example.com.www > mikado.example.com.www: P
3497416463:3497416463(0) ack 3200063166 5792 <ms 1460,sackOK,timestamp 4620[:|tcp|] (DF)
20:36:25.779409 mikado.example.com.www > duplex.example.com.www: ack 1 win
5840 <nop,nop,timestamp 38815805 4620 (DF)
20:36:25.779877 duplex.example.com.48455 > mikado.example.com.www: P
1:427(426) ack 1 win 5840 <nop,nop,timestamp 38815805 4620 (DF)
```

# Linux 如何工作（早期）© 2021 Brian Ward 

win 6432 <nop,nop,timestamp 4620 38815805 (DF)

20:36:25.85465 mikado.example.com,ww > duplex.example.com,48455: P

1:773(772) ack 427 win 6432 <nop,nop,timestamp 4626 38815805 (DF)

20:36:25.84532 duplex.example.com,48455 > mikado.example.com,ww: . ack 773

win 6948 <nop,nop,timestamp 38815812 4626> (DF)

+   过滤器接收 9 个数据包

内核丢弃 0 个数据包

你可以通过添加过滤器使用 `tcpdump` 进行更精确的操作。你可以根据源和目的主机、网络、以太网地址、网络模型中不同层次的协议等进行过滤。在 `tcpdump` 识别的许多数据包协议中，包括 ARP、RARP、ICMP、TCP、UDP、IP、IPv6、AppleTalk 和 IPX 数据包。例如，要让 `tcpdump` 只输出 TCP 数据包，运行：

```bash
# tcpdump tcp
```

要查看 Web 数据包和 UDP 数据包，输入：

```bash
# tcpdump udp or port 80 or port 443
```

`or` 关键字表示左侧或右侧的条件任一为真即可通过过滤器。同样，`and` 关键字要求两个条件都为真。

> 如果你需要进行大量的数据包嗅探，请考虑使用 `tcpdump` 的 GUI 替代方案，例如 Wireshark。

## 原语 (Primitives)

在前面的示例中，`tcp`、`udp` 和 `port 80` 是原语的 Basic元素。最重要的原语列在表 10-3 中。

## 表 10-3：tcpdump 原语

| 原语 | 数据包规范 |
|---|---|
| `tcp` | TCP 数据包 |
| `udp` | UDP 数据包 |
| `ip` | IPv4 数据包 |
| `ip6` | IPv6 数据包 |
| `port port` | 往或自端口的 TCP 和/UDP 数据包 |
| `host host` | 往或自主机的数据包 |
| `net network` | 往或自网络的数据包 |

## 运算符 (Operators)

之前使用的 `or` 是一个运算符，`tcpdump` 可以使用多个运算符（如 `and`、`!`），并且你可以在括号中对运算符组合。如果你计划使用 `tcpdump` 执行任何正式工作，请确保阅读了 `pcap-filter(7)` 帮助页，特别是描述原语的章节。

使用 `tcpdump` 时要小心。本节之前显示的 `tcpdump` 输出仅包含 TCP（传输层）和 IP（网络层）头部，但你也可以让 `tcpdump` 打印整个数据包。尽管大多数重要的网络流量现在已通过 TLS 加密，除非你了解这些网络或获得许可，否则不应在网络上嗅探。

### 10.5.3 netcat

如果你需要像 `telnet` 那样更灵活地连接到远程主机，请使用 `netcat`（或 `nc`）。`netcat` 可以连接到远程 TCP/UDP 端口、指定本地端口、监听端口、扫描端口、将标准输入重定向到网络连接并从网络返回等。要使用 `netcat` 打开到端口的 TCP 连接，请运行：

```bash
$ netcat host port
```

当另一端结束连接时，`netcat` 会终止，如果你将标准输入重定向到 `netcat`，这可能会令人困惑，因为在发送数据后你可能无法返回提示符（与其他任何命令不同）。你可以随时通过 CTRL-C 结束连接。如果你想在特定端口上监听，运行：

```bash
$ netcat -l :port
```

如果 `netcat` 成功监听该端口，它将等待连接，并在建立连接后打印该连接的输出，并将任何标准输入发送到那里。以下是关于 `netcat` 的额外说明：

- 默认没有输出。如果某些操作失败，`netcat` 会返回相应的退出代码。如果你需要一些信息，请使用 `-v` ("详细模式"）。
- 默认情况下，`netcat` 尝试使用 IPv4 和 IPv6 连接。但在服务器模式下，`netcat` 默认使用 IPv4。要强制协议，使用 `-4` 指定 IPv4，使用 `-6` 指定 IPv6。
- `-u` 选项指定 UDP 而不是 TCP。

### 10.5.4 端口扫描

有时你不知道网络上的机器提供哪些服务，或者 IP 地址在何时被使用。网络映射器 `nmap` 会扫描机器或网络上的所有端口以寻找开放端口，并列出它找到的端口。大多数发行版都有 `nmap` 软件包，或者你可以从 http://www.nmap.org/ 获取它。在自己的机器上列出端口时，从至少两个点运行 `nmap` 有帮助：从你本机和另一个地方（可能在你的本地网络之外）。这样做可以让你了解防火墙拦截了哪些内容。

> 警告 如果其他人控制了你想要用 `nmap` 扫描的网络，请请求许可。网络管理员会监控扫描并禁用你运行的机器访问权限。

运行 `nmap` 对主机进行通用扫描。例如：
