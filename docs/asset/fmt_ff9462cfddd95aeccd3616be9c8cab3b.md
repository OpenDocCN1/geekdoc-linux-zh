
## 结论

在第一个命令中，我们指定 1472 为数据长度，因为如果加上 ICMP 回显请求（8 字节）和 IP 头部（20 字节），我们得到 1500，即以太网的 MTU。通过在第二个命令中增加一个字节（1473），我们超过了以太网 MTU 并收到了 ICMP 错误消息。您可以在 HP-UX 中使用 `-s` 参数指定数据包大小。
- 在 Windows 2000 中，`-t` 选项意味着 ping 将持续。在 HP-UX 中，它设置生存时间。
- 在 Windows 2000 中，`-a` 选项将地址解析为主机。HP-UX 没有 `-a` 选项。
- Windows 2000 有 `-i` 选项设置生存时间。HP-UX 使用 `-t` 选项。
- Windows 2000 的 `-v` 选项将服务类型字段（tos）设置为指定值；在 HP-UX 中，它指定详细输出，显示除 Echo 外的 ICMP 包。
- Windows 2000 的 `-r` 选项记录发送的数据包和返回的数据包。在 HP-UX 中，`-r` 指定跳过正常路由表并发送到连接的主机。
- Windows 2000 有 `-s` 选项，指定跳数。HP-UX 没有 `-s` 选项。
- 在 Windows 2000 中，`-j computer-list` 按松散模式路由到主机列表，而 `-k computer-list` 按严格模式路由到主机列表。HP-UX 的等效选项是 `-o`，它在命令结束时向发送的数据包插入 IP 。
- Windows 2000 有 `-w` 选项，指定毫秒超时。HP-UX 没有此选项。
- 最后，如果你从 HP-UX 系统 ping 且不使用 `-n` 选项指定 ping 数，ping 将持续发送直到被中断（`Ctrl-C`）。Windows 2000 ping 仅。

## 4.3 结论

网络层围绕 IP true。如果微软重写了 TCP/IP 栈，它将与 HP-UX 互操作。`arp` 和 `ping` 等命令的行为存在许多差异，但 Windows 2000 支持 NetUI 和 IPX/SPX，Unix 的互操作性从标准化 TCP/IP 开始。

# 参考文献

1. W. Richard Stevens, *TCP/IP Illustrated, Volume 1*. (Addison-Wesley Publishing Company, 1994).
2. Microsoft Corporation, *Microsoft Windows 2000 Server TCP/IP Core Guide*. (Microsoft Press, 2000).

# 第5 章：传输层

在传输层，我们有面向连接的传输控制协议（TCP）和无连接的用户数据报协议（UDP）。虽然 HP-UX 和 Windows 2000 的 TCP/IP 实现互操作，但它们的调优参数差异很大。本章将介绍了这些参数。

## 5.1 TCP

HP-UX 和 Windows 2000 之间的 TCP 连接建立遵循标准：
1. 客户端向服务器发送同步（SYN）段，指定端口和初始序列号（ISN）。
2. 服务器响应一个包含其 ISN 和包含客户端 ISN 加一的确认（ACK）段。
3. 客户端通过确认服务器 ISN 加一来确认服务器的 SYN 段。

TCP 端口定义明确且标准化。常用的 TCP 端口见表 5–1。Windows 2000 网络服务通常基于 NetBIOS，使得 TCP 端口 139 是一个重要的端口。

### 表 5–1 常用 TCP 端口

| 服务名称 | 端口 |
| :--- | :--- |
| FTP (数据通道) | 20 |
| FTP (控制通道) | 21 |
| Telnet | 23 |
| HTTP | 80 |
| NetBIOS 会话 | 139 |

### 5.1.1 调优参数

#### 5.1.1.1 最大段大小 (MSS) 和路径 MTU 发现

在第四章“互联网层”中，我们讨论了路径传输单元（MTU）发现，其中发送 IP 头部中的不分片位，以检查路径上的任何路由器是否返回互联网控制消息协议（ICMP）错误。TCP 在连接建立期间处理 MTU 发现，此时双方都可以宣布其最大段大小（MSS）。如果接收端不宣布其 MSS，发送站的 TCP 将使用 536 字节。到那时，TCP 将发送设置了不分片位的数据。如果路由器返回 ICMP “目标不可达-需要分片”，TCP 将开始调整其 MSS 直到不再收到消息。

默认情况下，Windows 2000 发送在 IP 头部设置不分片标志的 TCP 段。因此，由 Windows 2000 发起的 TCP 会话会自动参与 MTU 发现。Windows 2000 将 TCP MSS 调整为 ICMP “目标不可达-需要分片”消息中指定的路由器 MTU。

HP-UX 上的 TCP 也会根据 ICMP “目标不可达-需要分片”消息调整其 MSS。这是默认设置。要禁用此行为，请使用以下命令：

```
# ndd -set /dev/tcp tcp_ignore_path_mtu 1
```

如果运行上述命令，TCP 将默认使用 576 字节的 MTU（536 字节的 MSS 加上 40 字节的 IP 和 TCP 头部）。

#### 5.1.1.2 接收窗口大小

Windows 2000 TCP 没有接收窗口大小的值；相反，它使用一种算法动态设置。该算法摘自《Microsoft Server TCP/IP Core Networking Guide》第 95 页，如下：
1. 向远程主机发起的首次连接请求指定的接收窗口大小为 16 千字节（KB）或 16,384 字节。
2. 建立连接后，接收窗口大小将向上取整为连接建立期间的 TCP MSS（最大段大小）的整数倍。
3. 如果向上取整后的值小于 MSS 的四倍，则将其调整为 4 × MSS，最大尺寸为 64 KB，除非启用了窗口放大选项（RFC 1323）。

要覆盖此过程并手动设置窗口大小，请编辑以下注册表项：

```
HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\nInterface\<interface>\TcpWindowSize
```

HP-UX：时间接收窗口的默认最大大小为 32,768 字节。要指定另一个值，请使用以下命令，window_size 的单位为：

```
# ndd -set /dev/tcp tcp_rec_hiwater_window_size
```

您还可以使用 `ndd -set /dev/tcp tcp_rec_hiwater_lfp` 命令设置“长肥管道”（Lfp，如光纤）接收窗口的最大大小。该值的默认值为 65,536 字节。对于“长窄管道”（Inp，如 PPP）的接收窗口，请使用 `ndd-set /dev/tcp tcp_rec_hiwater_inp` 命令。这里的默认值为 8,192 字节。

### 5.1.1.3 TCP Keep活 消息

您可以通过以下注册表参数设置 Windows 2000 在非活动连接上发送 TCP 保活消息的时间：

```
HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\KeepAliveTime
```

默认间隔为 7,200,000 毫秒（两小时）。通常是 Telnet 等应用程序而非用户来设置保活消息。

在 HP-UX 中，以下内核参数影响用于保活包的 TCP 行为：
- `tcp_keepalive_interval`
- `tcp_ip_abort_interval`
- `tcp_ip_abort_cinterval`
- `tcp_keepalive_detached_interval`

参数 `tcp_keepalive_interval` 决定了 TCP 在发送保活包之前等待无未确认数据的空闲连接的时间。默认值为两小时。您可以使用 `ndd` 命令重置默认值。该命令的参数单位为毫秒。例如，要将保活间隔设置为三小时，您需要输入：

```
# ndd -set /dev/tcp tcp_keepalive_interval 10800000
```
