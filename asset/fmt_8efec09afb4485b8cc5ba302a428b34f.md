
答案 B 是正确的，因为 IPv6-over-IPv4 隧道用于允许 IPv6 主机通过 IPv4 网络相互通信。答案 A 是错误的，因为 IPv6-over-IPv4 隧道并不允许 IPv4 主机在为了辅助 IPv4 向 IPv6 过而引入的 IPv6 网络上通信。答案 C 是错误的，因为 IPv6-over-IPv4 隧道不是用于连接网络，而是用于允许 IPv6 主机在 IPv4 网络上通信。答案 D 是错误的；IPv4 主机不使用 IPv6- 隧道。隧道的目的是允许 IPv6 主机在现有的 IPv4 网络内相互通信。

## 问题 4

你正在创建一个名为 `ip.tun0` 的 IPv6-over-IPv4 隧道。为了使隧道配置在重启后持续，你会创建哪个配置文件？

- A. `/etc/hostname.ip.tun0`
- B. `/etc/hostname6.eth0`
- C. `/etc/hostname6.ip.tun0`
- D. `/etc/hostname.eth0`

答案 C 是正确的，因为配置文件 `/etc/hostname6.ip.tun0` 将用于创建一个名为 `ip.tun0` 的持久隧道。答案 A 是错误的，因为配置文件 `/etc/hostname.ip.tun0` 将指向一个 IPv4 接口。答案 B 是错误的，因为 `/etc/hostname6.eth0` 是用于配置 IPv6 主网络接口的文件。它不会用于 IPv6-over-IPv4 隧道。答案 D 是错误的，因为配置文件 `/etc/hostname.eth0` 用于配置用于 IPv4 主网络接口。

## 问题 5

哪条命令可以成功取消配置并移除 IPv6-over-IPv4 隧道 `ip.tun0`？

| A. `ifconfig inet6 down ip.tun0` |
| B. `ifconfig ip.tun0 inet6 down unplumb` |
| C. `ifconfig down unplumb ip.tun0 inet6` |
| D. `ifconfig inet6 ip.tun0 down unplumb` |

答案 B 是正确的，因为命令 `ifconfig ip.tun0 inet6 down unplumb` 将成功取消配置并移除隧道 `ip.tun0`。答案 A、C 和 D 是错误的，因为 `ifconfig` 命令的语法错误。

## 问题 6

关于 IPv6-over-IPv4 隧道，以下哪些陈是正确的？选择 2 项。

- 发送者和接收者支持 IPv4 和 IPv6，中间的路由器和主机只需要支持 IPv4。
- 从发送者到接收者的所有主机和路由器都支持 IPv6。
- IPv6 数据以特殊的 IPv6 数据包在网络上传输，这些数据包被 IPv4 网络识别。
- IPv6 数据被封装在 IPv4 数据包中并在网络上传。
- 发送者和接收者只需要支持 IPv4，因为数据被封装在 IPv4 数据包中。

答案 A 和 D 是正确的，因为发送者和接收者都支持 IPv4 和 IPv6。路径上的中间路由器和主机只需要支持 IPv4。答案 B 是错误的，因为路径上的主机和路由器只需要支持 IPv4，因为数据被封装在 IPv4 数据包中。答案 C 是错误的，因为 IPv6 数据在网络上是以 IPv4 数据包的形式传输的。答案 E 是错误的，因为发送者和接收者都需要支持 IPv4 和 IPv6——IPv6 数据被封装在 IPv4 数据包中进行网络传输。

## 想要了解更多？

![](img/b8864f367e279929da7f8395589b04dd_197_0.png)

Sun Microsystems, Solaris 9 9/02 及更高版本系统管理员集合—IPv6 管理指南。提供纸质版、通过网页 http://docs.sun.com 访问，以及在 Solaris 9 操作系统提供的在线文档中。

![](img/b8864f367e279929da7f8395589b04dd_197_1.png)

Sun Microsystems, Solaris 9 系统管理员集合—系统管理指南：IP 服务。提供纸质版、通过网页 http://docs.sun.com 访问，以及在 Solaris 9 操作系统提供的在线文档中。

![](img/b8864f367e279929da7f8395589b04dd_197_2.png)

Sun Microsystems 系统参考手册，第 1M 节——“系统管理命令”。提供纸质版、通过网页 http://docs.sun.com 访问，以及在 Solaris 9 操作系统提供的在线文档中。

![](img/b8864f367e279929da7f8395589b04dd_197_3.png)

## TCP 和 UDP

你需要理解的术语：

- 缓冲传输 `Buffered Transfer`
- 拥塞窗口 `Congestion Window`
- 全双工 `Full-Duplex`
- 大窗口 `Large Window`
- 寄路回 `Piggybacking`
- TCP 段 `TCP Segment`
- 三次握手 `Three-Way Handshake`
- 虚拟电路 `Virtual Circuit`
- 窗口确认 `Window Advertisement`

你需要掌握的概念：

- 区分传输层协议的特性
- 解释 TCP 和 UDP 的基础

## 第 9 章

TCP 和 UDP 是运行在 TCP/IP 模型传输层的两种主要协议。传输层为应用数据提供端到端的服务——即从源端到目的地。TCP 和 UDP 都作为 Solaris 操作系统内核的一部分交付。

![](img/b8864f367e279929da7f8395589b04dd_199_0.png)

### TCP

传输控制协议 `TCP` 是一种面向连接、有状态且可靠的协议，负责处理跨网络的数据包交付。数据包可以通过不同的目的地进行路由，`TCP` 还负责在目的端对数据包进行重组。它通常用于主机之间交换的大量数据。`TCP` 具有以下特性：

- 虚拟电路——在数据传输之前，发送和接收主机都必须建立连接。这种连接被称为虚拟电路，因为它是一个逻辑连接，而不是物理连接。
- 全双工——`TCP` 连接允许数据在两个方向上同时传输，增加了给定时间内网络上可以携带的数据量。应用程序将 `TCP` 连接视为两个向相反方向移动的路径。全双工还利用了“寄路回” `piggybacking` 技术，将确认等控制信息封装在向相反方向传输的数据段中。这减少了网络上的流量。
- 流——应用程序以字节流的形式将数据传递给 `TCP` 进行传输。`TCP` 将流划段，段包含一个包含控制信息和数据的头部。
- 缓冲区——`TCP` 同时使用输入和输出缓冲区来调节发送和接收主机之间的流量。缓冲区最大尺寸的默认值为 1MB `1048576` 字节。可以使用此处所示的 `ndd` 命令查看或调整此参数：

```
# ndd /dev/tcp tcp_max_buf
1048576
```

## TCP 和 UDP 165

当 `TCP` 建立连接时，会执行所谓的“三次握手”，其中发送主机发送一个 `syn` 消息，然后接收方发送 `syn` 的确认 `ACK`，并发送它自己的 `syn` 消息。发送者接收 `syn` 和 `ACK` 后发送最后的 `ACK`。发送者现在可以开始发送数据。图 9.1 显示了其工作原理。

![](img/b8864f367e279929da7f8395589b04dd_200_0.png)

**图 9.1** 三次握手。

使用 `TCP` 的应用程序示例包括 `Telnet`、`FTP`、`HTTP` 以及 Solaris `r` 命令（如 `login` 和 `rsh`）。

### TCP 头部

`TCP` 使用段作为基本传输单元，而 `IP` 使用数据报，以太网使用数据包。`TCP` 头部由若干 32 位字 `4` 字节组成。头部至少为 5 个字 `20` 字节，并包含多个控制跨网络数据交付的字段。`TCP` 段头部的格式如图 9.2 所示。

以下是 `TCP` 头部字段：

- 源端口——识别发送端的 `TCP` 应用程序。
- 目的端口——识别接收端的 `TCP` 应用程序。

## 166 第 9 章

- 序列号——识别数据在流中的位置。
- 确认号——识别已接收了流的量。
- 偏移量 `Offset`——识别头部的位置。
- 标志 `Flags`——每个位决定段的：
    - `URG`——该位置1时，表示紧急数据。
    - `ACK`——该位置1时，表示确认。
    - `PSH`——该位置1时，表示应立即交付段。
    - `RST`——该位置1时，表示重置连接。
    - `SYN`——该位置1时，表示建立连接。
    - `FIN`——该位置1时，表示发送结束。
    - 窗口——指定接收方可以接受多少数据。
    - 校验和——用于验证头部和数据完整性的 16 位整数。
    - 紧急指针——指定流中紧急数据的的位置；当 `URG` 位设置时有效。
    - 选项——`TCP` 使用此字段与对方通信。大小可变。
