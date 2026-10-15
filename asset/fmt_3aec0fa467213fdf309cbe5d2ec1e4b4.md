
```bash
ping www.example.com
64 bytes of data from 93.184.216.34: icmp_seq=0 ttl=54 time 8.2 ms
64 bytes of data from 93.184.216.34: icmp_seq=1 ttl=54 time 7.5 ms
64 bytes of data from 93.184.216.34: icmp_seq=2 ttl=54 time 8.1 ms
64 bytes of data from 93.184.216.34: icmp_seq=3 ttl=54 time 7.9 ms
64 bytes of data from 93.184.216.34: icmp_seq=4 ttl=54 time 8.0 ms

--- www.example.com ping statistics ---
5 packets sent, 5 received, 0% packet loss, time 4005ms
round-trip min/avg/max/mdev = 7.5/7.94/8.2/ms
```

`ping` 命令使用 DNS 将主机名 `www.example.com` 解析为 IP 地址 `93.184.216.34`。`icmp_seq` 字段用于对发送的数据包编号。`TTL` 字段用于确定传输过程中应经过的最大跳数。给出的毫秒数是数据包到达主机并返回的时间。这被称为往返时间（RTT）。

以下选项可以使用 `ping` 命令：

- `-t`: 设置每个数据包的超时
- `-c`: 设置发送的数据包数量
- `-i`: 设置数据包之间的间隔
- `-s`: 设置数据包大小
- `-W`: 设置等待响应的超时
- `-u`: 不解析主机名
- `-a`: 解析 IP 地址

例如，以下命令：

```bash
ping -c 4 www.example.com
64 bytes of data from 93.184.216.34: icmp_seq=0 ttl=54 time 8.2 ms
64 bytes of data from 93.184.216.34: icmp_seq=1 ttl=54 time 7.5 ms
64 bytes of data from 93.184.216.34: icmp_seq=2 ttl=54 time 8.1 ms
64 bytes of data from 93.184.216.34: icmp_seq=3 ttl=54 time 7.9 ms

--- www.example.com ping statistics ---
4 packets sent, 4 received, 0% packet loss, time 4005ms
round-trip min/avg/max/mdev = 7.5/7.94/8.2/ms
```

## 解析输出

`ping` 命令使用 DNS 将主机名 `www.example.com` 解析为 IP 地址 `93.184.216.34`。`icmp_seq` 字段用于对发送的数据包编号。`TTL` 字段用于确定传输过程中应经过的最大跳数。给出的毫秒数是数据包到达主机并返回的时间。这被称为往返时间（RTT）。

以下示例显示了主机不可访问时的 `ping` 输出：

```bash
ping 192.168.1.200
Request timeout for 192.168.1.200
Request timeout for 192.168.1.200
Request timeout for 192.168.1.200
Request timeout for 192.168.1.200

--- 192.168.1.200 ping statistics ---
4 packets sent, 0 received, 100% packet loss, time 3005ms
```

## traceroute

`traceroute` 命令用于跟踪数据包从计算机到主机的路径。它通过增加数据包的 `TTL`（生存时间）值，直到它们到达目的地。路径上的每个路由器都会递减 `TTL`，并在 `TTL` 达到 0 时返回 ICMP 超时消息。这允许你看到路径上的每一个跳数。

```bash
traceroute www.example.com
1  192.168.1.1 (192.168.1.1)  0.523 0.456 0.410 ms
2  10.0.0.1 (10.0.0.1)  2.150 2.200 2.300 ms
3  172.16.0.1 (172.16.0.1)  10.500 10.600 10.700 ms
4  93.184.216.34 (93.184.216.34)  12.100 12.200 12.300 ms
```

`traceroute` 命令显示路径上每个路由器的 IP 地址以及数据包到达那里的时间。

## 网络基础命令

根据网络的协议设置，需要某些工具和命令来执行系统检查。像 `ping` 和 `traceroute` 这样的简单命令非常有用，因为它们可以分析网络。它们对于本地设置内的系统或全球范围内的网络都有效。

## ping

用于故障排除或检查互联网上其他计算机的状态。`ping` 命令向被测试主机发送互联网控制消息协议（ICMP）`ECHO_REQUEST` 包，并等待主机返回 `ICMP_RESPONSE` 包。尽管某些数据包在网络中丢失，但如果主机处于激活状态，`ping` 的输出将显示至少收到了一些响应。如果主机离线，`ping` 的输出将显示主机不可访问。执行命令时，输出将显示互联网控制消息协议（ICMP）数据包的以下统计信息：

```bash
ping www.example.com
64 bytes of data from 93.184.216.34: icmp_seq=0 ttl=54 time 8.2 ms
64 bytes of data from 93.184.216.34: icmp_seq=1 ttl=54 time 7.5 ms
64 bytes of data from 93.184.216.34: icmp_seq=2 ttl=54 time 8.1 ms
64 bytes of data from 93.184.216.34: icmp_seq=3 ttl=54 time 7.9 ms
64 bytes of data from 93.184.216.34: icmp_seq=4 ttl=54 time 8.0 ms

--- www.example.com ping statistics ---
5 packets sent, 5 received, 0% packet loss, time 4005ms
round-trip min/avg/max/mdev = 7.5/7.94/8.2/0.285 ms
```

`ping` 命令使用 DNS 将主机名 `www.example.com` 解析为 IP 地址 `93.184.216.34`。`icmp_seq` 字段用于对发送的数据包编号。`TTL` 字段用于确定传输过程中应经过的最大跳数。以下选项可以使用 `ping` 命令：

- `-t`: 设置每个数据包的超时
- `-c`: 设置发送的数据包数量
- `-i`: 设置数据包之间的间隔
- `-s`: 设置数据包大小
- `-W`: 设置等待响应的超时
- `-u`: 不解析主机名
- `-a`: 解析 IP 地址

例如，以下命令：

```bash
ping -c 4 www.example.com
64 bytes of data from 93.184.216.34: icmp_seq=0 ttl=54 time 8.2 ms
64 bytes of data from 93.184.216.34: icmp_seq=1 ttl=54 time 7.5 ms
64 bytes of data from 93.184.216.34: icmp_seq=2 ttl=54 time 8.1 ms
64 bytes of data from 93.184.216.34: icmp_seq=3 ttl=54 time 7.9 ms

--- www.example.com ping statistics ---
4 packets sent, 4 received, 0% packet loss, time 4005ms
round-trip min/avg/max/mdev = 7.5/7.94/8.2/0.285 ms
```

## 解析输出

`ping` 命令使用 DNS 将主机名 `www.example.com` 解析为 IP 地址 `93.184.216.34`。`icmp_seq` 字段用于对发送的数据包编号。`TTL` 字段用于确定传输过程中应经过的最大跳数。给出的毫秒数是数据包到达主机并返回的时间。这被称为往返时间（RTT）。

以下示例显示了主机不可访问时的 `ping` 输出：

```bash
ping 192.168.1.200

Request timeout for 192.168.1.200

Request timeout for 192.168.1.200

Request timeout for 192.168.1.200

Request timeout for 192.168.1.200

--- 192.168.1.200 ping statistics ---

4 packets sent, 0 received, 100% packet loss, time 3005ms
```

## traceroute

`traceroute` 命令用于跟踪数据包从计算机到主机的路径。它通过增加数据包的 `TTL`（生存时间）值，直到它们到达目的地。路径上的每个路由器都会递减 `TTL`，并在 `TTL` 达到 0 时返回 ICMP 超时消息。这允许你看到路径上的每一个跳数。

```bash
traceroute www.example.com

1  192.168.1.1 (192.168.1.1)  0.523 0.456 0.410 ms

2  10.0.0.1 (10.0.0.1)  2.150 2.200 2.300 ms

3  172.16.0.1 (172.16.0.1)  10.500 10.600 10.700 ms

4  93.184.216.34 (93.184.216.34)  12.100 12.200 12.300 ms
```

`traceroute` 命令显示路径上每个路由器的 IP 地址以及数据包到达那里的时间。

```bash
$ ping -c 10 www.phantommemory.com

PING from phantommemory.com (64.41.207.50): icmp_seq=0 ttl=51 time=77.6 ms

64 bytes from 64.41.207.50: icmp_seq=1 ttl=51 time=77.8 ms

64 bytes from 64.41.207.50: icmp_seq=2 ttl=51 time=77.1 ms

64 bytes from 64.41.207.50: icmp_seq=3 ttl=51 time=77.3 ms

64 bytes from 64.41.207.50: icmp_seq=4 ttl=51 time=76.9 ms

64 bytes from 64.41.207.50: icmp_seq=5 ttl=51 time=76.9 ms

64 bytes from 64.41.207.50: icmp_seq=6 ttl=51 time=77.3 ms

64 bytes from 64.41.207.50: icmp_seq=7 ttl=51 time=77.7 ms

64 bytes from 64.41.207.50: icmp_seq=8 ttl=51 time=77.0 ms

64 bytes from 64.41.207.50: icmp_seq=9 ttl=51 time=77.1 ms

---

www.phantommemory.com ping statistics

10 packets transmitted, 10 packets received, 0% packet loss

round-trip min/avg/max = 76.9/77.2/77.8 ms
```

在上面的示例中，用户不需要输入任何键序列即可退出 `ping`：`-c` 选项会在发送 10 个数据包后关闭 `ping` 并显示统计信息。在这种情况下，用户收到了 0% 的丢包率。如果主机极其繁忙，或者用户计算机与主机之间出现问题，使用 `ping` 命令时可能会遇到问题，数据包可能会被丢弃或丢失。

### traceroute

`traceroute` 是一种网络实用，用于追踪从一台计算机到另一台计算机的路径，这在尝试确定路径是否存在中断时非常有帮助。`traceroute` 命令通过发送数据并附加存活时间（TTL）值来跟踪每个路由器。对于第一个路由器，TTL 字段被设置为 0，因此路由器会生成一个 ICMP 错误消息；`traceroute` 会判断往返时间（RTT）并确定源计算机。一旦发送了第一批包且 `traceroute` 接收到 ICMP 错误消息，它会将 TTL 字段加一并重新发送数据包。通过这种方式，`traceroute` 会接收路径上下一个路由器的输出，直到达到最大跳数（默认值为 30）。在 `traceroute` 发送包并增加 TTL 字段的同时，它还将信息输出到屏幕上，以便路径可见。

## 解析输出

`traceroute` 的输出包含路由器的 IP 地址和屏幕上显示的 TTL 值。每个 IP 地址都有三个 TTL 值，表示发送到该特定路由器的数据包。这些参数表示数据包回到发送者处往返所需的时间，即 RTT。如果 TTL 值处出现星号，则表示数据包未能到达目的地。使用 `traceroute` 命令的示例为：

```
traceroute [URL or IP address of host] [-d] [-f] [-g] [-iface] [-m max_ttl] [-p port] [-q] [-s src_addr] [-t tos] [-w waitime] [packetlen]
```

URL 或 IP 地址指向目标主机，括号中的字母是 `traceroute` 命令可用的标志。可以在手册找到选项列表。以下演示了使用 `traceroute` 确定从用户计算机到 `www.com` 的路径。

注意：带有星号的行包含与上下行相同的星号。

traceroute to www.starwars.com (64.21.207.50), 30 hops max, 38 byte packets

| 跳数 | IP 地址 | RTT | RTT | RTT |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 192.168.1.1 | 0.195 ms | 0.129 ms | 0.64 ms |
| 2 | rtr165.rtr165.com | 64.89.172.160 | 0.399 ms | 0.380 ms | 0.354 ms |
| 3 | rtr192.rtr149.com | 64.89.172.490 | 3.765 ms | 3.239 ms | 3.44 ms |
| 4 | 172.16.1.238 | 17.658 ms | 17.162.238 ms | 34.40 ms |
| 5 | 202.226.105.101 | 22.229 ms | 26.501 ms | 18.073 ms |
| 6 | fortwo-tx-1-ad12-0-6.esper.net | 206.222.100.129 | 39.971 ms | |
| 7 | 202.226.105.777 | 47.004 ms | 33.502 ms | 37.798 ms |
| 8 | el-chi-ad-12-0.esper.net | 206.222.97.133 | 59.522 ms | 57.663 ms |
| 9 | 202.226.103.264 | 118.556 ms | 98.908 ms | 96.431 ms |
| 10 | ltr03-s83-1-0.esper.net | 209.185.249.117 | 169.192 ms | |
| 11 | btr01-g6-0.esper.net | 216.33.147.35 | 104.793 ms | 99.849 ms |
| 12 | btr01-p1-0.esper.net | 209.185.249.182 | 112.852 ms | |
| 13 | dcr01-g2-0.esper.net | 216.34.23.33 | 109.022 ms | 95.6 ms |
| 14 | csr23-ve243-0.esper.net | 216.34.23.114 | 119.190 ms | 110.6 ms |
| 15 | 64.211.211.142 | 121.782 ms | 127.829 ms | 139.883 ms |
| 16 | * | * | * |
| 17 | * | * | * |
| 29 | * | * | * |
| 30 | * | * | * |

## 网络基础命令

该示例还显示了路由器在不同时间的性能特征。为了说明这一点，可以观察第 13 和 14 点：

```
13 dcr01-g2-0.esper.net (216.34.23.3) 109.022 ms 95.6 ms 99.83 ms

14 csr23-ve243-0.esper.net (216.34.23.114) 119.190 ms 110.6 ms 102.97 ms
```
