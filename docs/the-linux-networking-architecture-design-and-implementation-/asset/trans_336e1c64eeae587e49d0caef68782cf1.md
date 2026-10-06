

## C.6 使用 traceroute 追踪数据包 583

你可以使用 `traceroute` 来识别数据包到达指定计算机（主机）实际经过的路由。在局域网内，路径只有一跳，因为通信节点本身就在该局域网内——它仅仅是下一跳。相比之下，较大网络（例如互联网）中的通信关系可以使用更长的路由路径（如随后的示例所示）。

`traceroute` 的另一个优点是它适用于分析连接问题。例如，如果互联网上的某台计算机无法访问，你可以使用 `traceroute` 列出通往该计算机路径上所有可用路由器。如果中间某个系统没有响应，很容易找到错误源头。

为了识别通往目标计算机路径上的路由器，`traceroute` 使用了一种技巧而不是使用 IP 选项记录路由。具体来说，它创建了目标地址为指定计算机的 IP 数据包，并将这些数据包发送到该计算机。技巧在于 IP 头部中的 TTL 值最初设置为 1。该包会在第一个路由器处被丢弃，因为其最大生存时间（TTL）已过期。根据 IP 标准，路由器向发送者返回一个 ICMP 消息。通过这个 ICMP 消息，发送者可以获取路由器的 IP 地址并识别出第一个交换节点。这种方法不断重复——每次 TTL 值都为 1——直到到达目的地。

示例：局域网中的连接——直接连接的工作站

```
root@tux # traceroute www
troute to www.linux-netzwerkarchitektur.de (129.13.42.100),
30 hops max, 40-byte packets
1 www.linux-netzwerkarchitektur.de (129.13.42.100) 13 ms 9 ms 9 ms
```

示例：互联网中的连接

```
root@tux # traceroute www.tux.org
troute to www.tux.org (207.96.122.8), 30 hops max. 40 Byte packets
1 router1.linux-netzwerkarchitektur.de (129.13.42.244) 20 ms 20 ms 20 ms
2 141.3.1.1 (141.3.1.1) 10 ms 10 ms 10 ms
3 Karlsruhe.Belwue.de (129.143.167) 10 ms 10 ms 10 ms
4 ZR-Karlsruhe.Win-IP.DFN.de (188.1.174.1) 30 ms 30 ms 30 ms
5 ZR-Hannover1.Win-IP.DFN.de (188.144.177) 30 ms 30 ms 30 ms
6 IR-York-1.Win-IP.DFN.de (188.144.186) 80 ms 130 ms 290 ms
7 dfn.ny1.dyante.net (212.1.200.65) 60 ms 120 ms 270 ms
8 * * *
9 A0ITM3-0.XR2.NYC4.ALTER (152.63.22.6) 280 ms 270 ms 120 ms
10 ATM2-0-00.BR1.EWR1.ALTER (146.188.176) 260 ms 280 ms 290 ms
11 UUET-EWR-1-PEER.cw.net (137.39.23.66) 280 ms 140 ms 130 ms
12 corouter1.WestOrange.cw.net (204.70.9.138) 290 ms 290 ms 130 ms
13 core4.Washington.cw.net (204.70.4.105) 290 ms 290 ms 230 ms
14 fe0-1-0.gwl.spa.rcn.net (207.172.0.5) 140 ms 300 ms 270 ms
15 gwyn.tux.org (207.96.122.8) 160 ms 270 ms 270 ms
```

## 附录 C 网络操作工具和命令

当 `traceroute` 未收到被查询系统的响应时，它会输出 `*`：如果无法建立到该系统的连接，会出现多个 `*`，`traceroute` 最终停止。这提供了一个假设，即电缆被切断，或者尽管出现了星号但收到了被查询系统的响应，这可能意味着该系统或连接的链路负载过重。如果指定了参数，`traceroute` 向目标发送长度为 38 字节的数据包。在假设数据包未到达之前，具有限制 TTL 值的数据包会被`traceroute` 使用在 30 个站点之间。在正常情况下，对于每个站点，最多尝试三次以获取响应，每次最多等待三秒。

## 参数

- `host`：要识别的计算机的 DNS 名称或 IP 地址。使用了常用的网络解析机制。
- `maxttl`：设置请求包的 TTL 值为最大 TTL。
- `-1`：指定每个包的剩余生存时间（TTL）。
- `-n`：指定点进制表示法（即不进行名称解析）。
- `-p`：设置发送数据包的基础端口（默认为 3344）。端口范围取决于参与站点的数量。
- `-q`：获取响应的尝试次数（默认 3）。
- `-r`：忽略路由表。如果本地计算机不可用，则输出错误。此选项可测试路由情况或计算机。
- `-s hostaddr`：指定的 IP 地址作为具有 IP 地址的的发送地址。
- `-t`：设置 IP 包头部中 TOS 字段的值。
- `-w`：每次尝试地址的等待秒数（默认 3）。
- `-s`：指定数据包的大小（默认 38 字节）。

## C.7 其他工具 585

除了 Linux 早期就有的前面的工具外，还有几个新程序可以检查和监控网络。我们将介绍其中三个工具。关于这些工具的详细信息可以在手册页或 URL 中找到。

`ping` 是识别计算机之间可用带宽的工具。`ping` 使用不同大小的 ICMP 包，并尝试从识别的往返中计算当前带宽。`ping` 使用许多选项，可以在手册页（man ping）中描述。以下示例显示了如何测量 54-kbps 的调制解调器线路。

```
root@tux # ping 213.7.6.95 
ping 213.7.6.95 (213.7.6.95) 54 bytes data
64 bytes from 213.7.6.95: icmp_seq=1 ttl=54 time=10.2 ms
64 bytes from 213.7.6.95: icmp_seq=2 ttl=54 time=10.5 ms
64 bytes from 213.7.6.95: icmp_seq=3 ttl=54 time=10.3 ms
64 bytes from 213.7.6.95: icmp_seq=4 ttl=54 time=10.4 ms
64 bytes from 213.7.6.95: icmp_seq=5 ttl=54 time=10.6 ms
64 bytes from 213.7.6.95: icmp_seq=6 ttl=54 time=10.4 ms

---
213.7.6.95 ping statistics ---
6 packets transmitted, 6 received, 0% packet loss, time 50.4ms
rtt min/avg/max/mdev = 10.211/10.413/10.632/0.158 ms
```

`ntop` 显示有关连接网络当前利用率的信息。它记录通过网络适配器接收的数据包并创建各种统计数据。图 C-1 显示了所用协议当前的分布示例。我们可以看到 `ntop` 是基于浏览器的（即以 Web 页的形式表示其信息）。还有一个基于文本的版本，类似于用于显示当前进程及其计算负载的 `top` 工具。使用 `ntop` 的信息可以在手册页或访问 http://www.ntop.org 获取。

`ethereal` 是另一种用于研究局域网数据流量的工具。与适用于创建统计数据和研究局域网负载分布的 `ntop` 不同，`ethereal` 用于对数据流进行详细分析。它捕获局域网内的当前数据流并解释数据包内容及相关的协议过程。图 C-2 显示了 `ethereal` 如何捕获到 Web 服务器的 HTTP 请求示例。http://www.tux.org。

关于 `ethereal` 的信息可以在手册页（man ethereal）或访问 http://www.ethereal.com 获取。

