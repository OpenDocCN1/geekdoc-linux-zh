
# 故障排除与网络配置指南

## 队列计数器

**输入队列（Input Queues）**

如果丢弃计数器增加，说明传输到路由器的流量超过了它的处理能力。如果此值持续较高，需要确定这些计数器具体何时增加的，以及这些事件如何与 `CPU` 使用率相关。请注意，你还会看到被忽略（`ignored`）和被节流（`throttled`）的计数器。

**输出队列丢弃（Output Queue Drops）**

此计数器指示接口拥塞导致数据包被丢弃。

## 错误计数器

**输入错误（Input Errors）**

输入错误指示高层错误，如 `CRC`。这可能指向布线问题、硬件问题或双工冲突。

**输出错误（Output Errors）**

此问题等于端口在发生冲突问题时尝试传输的帧总数。

这些错误也可能由线路本身的干扰引起，这意味着你必须联系 `ISP` 来解决。

## 串行接口检查

在串行接口上，首先检查到路由器的物理连接。你是否收到了时钟信号（`clocking`）？这来自 `CSU/DSU`。查看输出以确认这一点：

```
Router>sh controllers s0/0
Interface Serial/0
Hardware is PowerQUICC MPC860
TE V.35 TX and RX clocks detected.
```

好了，我们已经验证了收到了时钟信号，现在让我们看看接口告诉了我们什么：

```
Router#sh int s0/0
Serial0/0 is up, line protocol is
Hardware is PowerQUICC Serial
Description: Connection to CR1
Internet address is 192.168.11.1/24
MTU 1500 bytes, BW 1000 Kbit, DL 20000 use,
reliability 255/255, txload 1/255, rxload 1/255
Encapsulation PPP, LCP, loopback not set
Keepalive set (10 sec)
CRC checking enabled
Last input never, output never, output hang never
Last clearing of "show interface" counters 00:02:58
Input queue: 75/0/0 (size/max)/drops/flushes); Total output drops: 0
Queuing strategy: fifo
Output queue: 0/40 (size/max)
5 minute input rate 0 bits/sec, 0 packets/sec
5 minute output rate 0 bits/sec, 0 packets/sec
0 packets input, 0 bytes, 0 buffer
Received 0 broadcasts, 0 runs, 0 giants, 0 throttles
156789 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored, 0 abort
0 packets output, 0 bytes, 0 underruns
0 output errors, 0 collisions, 2 interface resets
0 output buffer failures, 0 buffer swapped out
0 carrier transitions
```

```
DCD=up D=up DTR=up CTS=up
```

`BR1#`

我们可以直接在第一行输出中看到该接口存在的问题。

`Serial/0` 是 `up`，但链路协议是 `down`，这告诉我们连接到 `CSU/DSU` 的本地接口工作正常，但我们仍然看不到远程路由器。这表明远程路由器有问题，但通常是 `ISP` 问题。再次，如果你收到此错误，意味着你必须联系 `ISP`。以及所有输入错误！这说明线路有问题——可能是某种干扰，需要报告。

## 水平分割线（Split Horizon）

水平分割线通常发生在使用 `Frame Relay` 的环境中，且你有多个 `PVC` 接入单个串行接口时。这种配置会让路由协议认为它正在从发送路由的同一个接口接收路由，在这种情况下会导致路由被丢弃。解决此问题的一种简便方法是在串行接口上创建子接口（逻辑接口），这样每个网段都会接收路由通告。配置看起来如下：

```
interface Serial/0
ip address 10.1.12.1 255.255.255.0
no ip directed-broadcast
encapsulation frame-relay
```

或者是：

```
interface Serial/0
（注意物理接口没有 IP 地址！）
no ip directed-broadcast
encapsulation frame-relay
```

或者是：

```
!
interface Serial/0 point-to-point
ip address 10.1.12.1 255.255.255.0
no ip directed-broadcast
frame-relay interface-ci
```

或者是：

```
!
interface Serial/0 point-to-point
ip address 10.1.12.1 255.255.255.0
no ip directed-broadcast
frame-relay interface-ci
```

## DNS 问题

另一个可能导致互联网连接看起来已中断的问题涉及 `DNS`。如果用户无法解析域名，解决 `DNS` 问题的第一步是准确了解你的特定网络中是如何设置 `DNS` 的。你是有本地 `DNS` 服务器，还是在使用 `ISP` 的 `DNS` 服务器？如果你可以 `ping` 通 `74.128.50` 但无法 `ping` 通 `www.google.com`，你就知道正在处理 `DNS` 问题。首先验证本地 `DNS` 服务器，如果正常，联系 `ISP`。

## 路由器配置

当 `WAN` 服务无法工作时，路由器配置也可能是罪魁祸首。由于路由信息错误，在故障排除连接到互联网的路由器时，第一步总是验证你的默认路由。通过在路由器上使用 `ip route` 命令，可以看到路由器用于转发决策的路由表：

```
Router#sh ip route
Codes: L - local, C - connected, S - static
10.0.0.0/8 is variously subnetted, masks
10.0.0.0/8 is directly connected, FastEthernet/3
10.0.0.1/32 is directly connected, FastEthernet/3
10.0.0.0/16 is directly connected, FastEthernet/2
10.0.0.1/32 is directly connected, FastEthernet/2
10.0.10/24 is directly connected, FastEthernet/1
10.0.10/32 is directly connected, FastEthernet/1
10.0.0.0/8 is directly connected, FastEthernet/0
```

验证默认路由，如果它指向错误的下一跳或出口接口，你将面临一些严重的问题！

## 安全策略

另一个导致 `WAN` 相关问题的罪魁祸首是公司安全策略。例如，如果防火墙阻止了需要访问互联网的应用程序端口，`WAN` 问题的根源实际上是你的防火墙配置。另一个常见故障源与响应缓慢有关，这再次会让 `WAN` 链路看起来出现问题。但同样，可能是安全策略阻止了网站，特别是社交媒体或流媒体内容，人们通常将这些面向安全的限制称为访问策略或利用限制，这些限制由于某些原因强加于某些活动，但通常是为了保留带宽。

## 总结

在本章中，你学习了在地理隔离的位置之间提供 `WAN` 连接涉及的重要问题，以及不同类型的 `WAN` 连接，包括点对点连接、电路交换服务提供网络和包交换服务提供网络。你还意识到不同传输介质和距离参数对 `WAN` 连接的影响。此外，你还学习了通过 `DSL` 和电缆调制调器等宽带技术进行租线连接的选择。你研究了用于连接今天高速 `WAN` 的 `WAN` 协议和技术，包括 `ISDN`、`Frame Relay`、`ATM` 和 `MPLS`，并具备了排除和解决常见 `WAN` 问题的有用策略。

## 考试要点

- 能够区分各种 `WAN` 技术。你必须能够识别不同的远程访问和 `WAN` 技术的速率和容量，以及实现这些技术的介质。
- 识别各种互联网接入技术的基本特征。这些包括 `DSL`、宽带、`POTS` 和入户光纤（`PON`）。了解这些技术的区分特征是重要的。了解它们的优缺点，以便你识别每种技术的最佳用途。
- 熟悉电路交换和包交换技术之间的差异，以及哪些协议使用每种。`Frame Relay` 是一种包交换技术，`ISDN` 是一种电路交换数字解决方案。`ATM` 被视为单元交换技术，因为它包含了 53 字节的单元。`MPLS` 和 `ATM` 都是面向连接的技术，因为建立了连接。
