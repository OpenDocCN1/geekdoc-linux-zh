
```
collisions:0 txuelen:10000

RX bytes:260914 (244.4 KIB)  TX bytes:2891581 (2.7 MIB)

Interrupt: 1 Base address:0x0000

lo Link:Local Loopback

inet addr:127.0.0.1/8  mask:255.0.0.0

inet6 addr:::1/128  Scope:Host

UP LOOPBACK RUNNING MTU:16436 Metric:1

TX packets:24256 errors:0 dropped:0 overruns:0 frame:0

RX packets:24256 errors:0 dropped:0 overruns:0 carrier:0

collisions:0 txuelen:10000

RX bytes:2891581 (2.7 MIB)  TX bytes:2891581 (2.7 MIB)
```

这显示三个网络——环回接口（`lo`）和两个以太网卡（`eth0` 和 `eth1`）——当前在系统中处于激活状态。对于每个接口，您可以看到 IP 地址以及数据包交付和发送的统计信息。如果 Linux 系统运行拨号 PPP 链路，您还会在输出中看到 `/pp0` 接口的项目。

## 检查 IP 路由表 `/sbin/route`，同样

另一个网络配置在您不带命令行参数运行时它会提供状态信息。如果您在检查与另一个主机（通过 IP 地址指定）的连接时遇到问题，请检查 IP 路由表查看是否指定了默认网关。然后检查网关的路由表，以确保通往目的的路径是通的。典型的输出如下：

```
Kernel IP table

Destination Gateway Genmask Metric Use Iface

0.0.0.0 0.0.0.0 0.0.0.0 0 eth0

192.168.1.0 0.0.0.0 255.255.255.0 0 eth0

127.0.0.0 0.0.0.0 255.0.0.0 0 lo
```

在这种情况下，以太网和环回接口路径是通的。

## 223 检查 TCP/IP 网络

### 检查网络

要检查到主机的连通性，`ping` 命令使用互联网控制消息协议（ICMP）消息。这里是 `ping` 命令显示的示例：

```
PING 1.1

64 bytes from 192.168.1.1: icmp_seq=1 ttl=64 time=0.452 ms

PING 192.168.1.

64 bytes from 192.168.1.1: icmp_seq=2 ttl=64 time=0.436 ms

---

4 packets transmitted, 4 received, 0% packet loss

rtt min/avg/max/mdev = 0.436/0.441/0.452/0.008 ms
```

`ping` 命令依赖 ICMP 消息。然而，某些防火墙被配置为拦截它们。如果 `ping` 失败，可能是主机关闭或被拦截。

## 224 检查 TCP/IP 网络

### 检查网络状态

要检查网络状态，使用 `netstat` 命令。它显示各种类型的网络连接（如 TCP）。通过输入 `netstat -a` 查看接口状态，可以得到类似的输出：

```
Kernel Interface table

iface MTU RX-OK RX-ERR RX-DRP TX-OK TX-ERR TX-OVR Flg

eth0 1500 613175 0 174695 0 0 BMRU

el 1500 42298 0 1375 0 0 BMRU

lo 16436 32255 0 32255 0 LR
```

在这种情况下，输出显示了环回和以太网接口的状态。表 4-2 描述了列的含义。

| 表 4-2 内核接口表列的含义 |
| 列 | :--- |
| Iface | 接口名称 |
| MTU | 最大传输单元——数据包可以包含的最大字节数 |
| Met | 接口的指标值——软件在决定通过哪个接口发送数据包时使用的距离（跳数） |
| RX-OK, TX-OK | 接收（RX）或发送（TX）无错误包数量 |
| RX-ERR, TX-ERR | 错误包数量 |
| RX-DRP, TX-DRP | 丢弃包数量 |
| RX-OVR, TX-OVR | 因溢出丢失的数据包 |

> A = 接收组播；B = 广播；D = 开启调试；L = 环回接口（注意 `lo` 上的标记），M = 接收所有；N = 此接口无 ARP；P = 点对点接口；R = 接口运行；U = 接口启用

另一个实用的选项形式是 `netstat -t`，它显示所有活跃的 TCP 连接。以下是在某台 Linux PC 上输入 `netstat -t` 的典型结果：

### 检查 TCP/IP 网络

活跃的 Internet 连接（不含服务器）

| 协议 (Proto) | 接收队列 (Recv-Q) | 发送队列 (Send-Q) | 本地地址 (Local Address) | 远程地址 (Foreign Address) | 状态 (State) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| tcp | 0 | 0 | localhost:2654 | localhost:1024 | 已建立 (ESTABLISHED) |
| tcp | 0 | 0 | localhost:1024 | localhost:2654 | 已建立 (ESTABLISHED) |
| ... | |

在这种情况下，输出列显示了协议（Proto）、接收队列和传输队列中的字节数（Recv-Q, Send-Q）、以 `hostname:service` 格式显示的本地 TCP 端口（Local Address）、远程端口（Foreign Address）以及连接状态。

使用 `netstat -ta` 查看所有连接——包括已建立的连接和你的 Linux 系统正在监听（尚未建立连接）的连接。例如，这里是 `netstat -ta` 命令的典型输出：

```
Active Internet connections (servers and established)

| Proto | Recv-Q | Send-Q | Local Address | Foreign Address | State |

| :--- | :--- | :--- | :--- | :--- | :--- |

| tcp | 0 | 0 | *:3279 | * | LISTEN |

| tcp | 0 | 0 | * | * | LISTEN |

| tcp | 0 | 0 | *:sunprpc | * | LISTEN |

| tcp | 0 | 0 | *:localhost.domainip | * | LISTEN |

| tcp | 0 | 0 | *:localhost.domainip:5315 | * | LISTEN |

| tcp | 0 | 0 | 192.168.0.9:45678 | www.redhat.com:http | ESTABLISHED |

| tcp | 0 | 0 | 192.168.0.9:45875 | www.redhat.com:http | ESTABLISHED |

| tcp | 0 | 0 | *:ffff:192.168.0.3:4932 | * | ESTABLISHED |
```

## 嗅探网络包

嗅探网络包听起来像某种非法行为，不是吗？嗅探简单是指查看 TCP/IP 网络数据包。其概念是捕获所有网络数据包以便对它们进行检查。

## 管理网络

如果你需要嗅探 TCP/IP 数据包，可以使用 `tcpdump`，这是一个在 Linux 下的命令行工具。正如其名称所示，它会转储（打印）TCP/IP 网络数据包的头部。

要使用 `tcpdump`，请以 root 身份登录并在终端窗口中输入 `tcpdump` 命令。你可能希望将输出保存到文件中，并在稍后检查该文件。否则，`tcpdump` 会在窗口中显示飞闪而过的数据包。例如，为了在一个名为 `tdout` 的文件中捕获 1000 个数据包并尝试将 IP 地址转换为名称，请输入以下命令：

```bash
tcpdump -c 1000 > tdout
```

捕获 1000 个数据包后，`tcpdump` 就会退出。然后你可以检查输出文件 `tdout`。它是一个文本文件，因此你可以直接用文本编辑器打开它，或者输入 `tcpdump -r` 来查看捕获的数据包。

为了满足你的好奇心，这里是 `tcpdump` 典型输出的几行：

```
20:05:57.723621 arp who-has 192.168.0.1 tell LNBECAN.nrockv01.md.com.net
```
