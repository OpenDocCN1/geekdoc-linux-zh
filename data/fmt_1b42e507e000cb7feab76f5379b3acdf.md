
Starting`Nping`0.5.51(`http://nmap.org/nping`)at2016-11-1611:16GMT

```
(0.0145s) TCP 127.0.0.1:16463 > 127.0.0.1:80 ttl=64 id=0 58041

ipl=40 seq=278160024 win=140

RCVD (0.0148s) TCP 127.0.0.1:80 < 127.0.0.1:16463 SA ttl=64 id=0 ipl=44

seq=278160250 win=65535 options=6595

SENT (0.0148s) TCP 127.0.0.1:16463 > 127.0.0.1:433 ttl=64 id=0 58041

ipl=40 seq=278160014 win=140

RCVD (0.0150s) TCP 127.0.0.1:433 < 127.0.0.1:16463 RA ttl=64 id=0

ipl=40 seq=win=0

Max rtt: 0.079ms Min rtt: 0.055ms Avg rtt: 0.06ms

Raw packets sent: 2 (8B) Recvd: 2 (8B) Lost: 0 (0.00%)

Tx time: 0.01005s Bytes/s: 79.96 Tx pkts/s: 2.00

Rx time: 2.00171s Bytes/s: 41.96 Rx pkts/s: 1.00

pinging: 1 IP address pinged in 2.03 seconds
```

你可以在列表5.1中看到你收到了来自`tcp`端口80和`tcp`端口443的回复。根据`--c`选项，在每个端口发送数据（并收到返回）后，`ping`会自动停止。如果没有明显的有效响应，你可能会看到类似的内容：

```
nping_event_handler(): READ-PCAP killed: Resource temporarily unavailable

nping_event_handler(): TIMER: Resource temporarily unavailable
```

现在你已经了解了`Nping`如何工作以及如何对你的输入做出反应，那么你可以随地使用无分类域间路由(`CIDR`)网络（例如`10.10.10.0/24`），这应该并不令人意外。你现在将保持基础操作，并查看如何指定端口范围。

考虑“特权端口”(`privileged`ports)。这些端口过去被赋予了一些名称（如超级用户端口或原始端口），但本质上，只有`root`用户有权打开它们。这是一个安全特性，意味着如果你远程连接到这些端口之一，可以合理地确认该服务正在运行。在其他情况下，它是`root`用户启动的。这里是使用`Nping`检查所有特权端口的方法：

```
# nping -c1 --tcp -p 0-1024 localhost
```

使用这种方法与其他网络工具不同，`Nmap`处理多个主机和端口的方式。为了效率，如果指定了多个目标，`Nping`不会简单向列表中的第一个机器发送查询并等待响应。相反，它采用轮询(`round-robin`)方法，交替联系机器，这样在用户等待响应时就不会引入延迟。对于多个主机，这也适用于多个端口，让目标在响应下一个端口之前有一个恢复的机会。

## 解释器

`Nping`可以作为多种协议的解释器。如果你使用`--tcp`选项，那么你就在使用`Nping`的`connect`模式。你不需要特权来触发原始数据包；相反，`Nping`请求操作系统代表你完全创建连接。你可以看到入站或出站数据包的内容。

当你作为`root`用户运行时，`--tcp`选项允许你通过`TCP`数据包获得卓越的结果。例如，你可以通过部分完成`TCP`握手来操纵连接结果。文档讨论了这种可能性（实际上，使用“`evil`”词）来伪造`IP`地址。使用三个独立的命令操作`TCP`握手可能如下：

```
# nping -c1 --tcp -p 80 --flags RST

# nping -c1 --tcp -p 80 --flags syn

# nping -c1 --tcp -p 80 --flags ack
```

## UDP

你也可以通过`--udp`选项使用用户数据报协议(`UDP`)包。正常的`UDP`包嵌入在`IP`包中，但正如我所说，如果没有`root`权限，只要默认头没有更改，你就可以看到包的内容。`ping`有时可以发现其他协议失败的情况。`ping`可能绕过防火墙并报告设备是否在监听。这是你工具箱中非常有用的补充。一个简单的示例：

```
# nping --udp localhost
```

当我在没有`root`用户的情况下对本地机器运行此命令时，我看到：

```
SENT (0.0069s) UDP packet with 4 bytes to localhost:127.0.0.1:40

ERR: (0.0070s) to 127.0.0.1: Connection refused
```

然而，作为超级用户`Nping`，可以重复交易：

```
SENT (0.0161s) UDP 127.0.0.1:53 > 127.0.0.1:40 ttl=64 id=6474 ipl=28

RCVD (0.0163s) ICMP 127.0.0.1 > 127.0.0.1 Port unreachable (type=3/code=3) ttl=64 id=18756 ipl=56
```

如你所示，在两个例子中`ping`流量都是活跃的。

## ICMP

与标准`ping`一样，如果作为`root`用户执行且没有选择其他协议，`Nping`默认使用`ICMP`。文档大胆地声明可以创建任何`ICMP`消息。例如，你可以查询时间戳、生成“目标不可达”消息或重定向数据包为另一个系统或网络引起问题。在`root`用户和标准用户中尝试以下命令：

```
# nping localhost
```

你可以清楚地看到细节上的差异。这里没有`root`的标准用户：

```
SENT (0.0027s) Starting TCP Handshake > localhost:80 (127.0.0.1:80)

RECV (0.0028s) Handshake with localhost:80 (127.0.0.1:80) completed
```

在下一个示例中，作为`root`用户，你可以看到更多关于`ICMP`包内容的信息。根据`RFC`(`https://tools.ietf.org/html/rfc792`)，`type=8`代表“`Echo`”，这正是你预期的。

```
SENT (0.0152s) ICMP 127.0.0.1 > 127.0.0.1 Echo request (type=8/code=0) ttl=64 id=31032 ipl=28

RECV (0.0154s) ICMP 127.0.0.1 > 127.0.0.1 Echo reply (type=0/code=0) ttl=64 id=18763 ipl=28
```
