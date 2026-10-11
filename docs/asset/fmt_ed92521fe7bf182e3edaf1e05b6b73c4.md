
输出中最重要的部分是 `icmp_seq` 号和往返时间。`ping` 每秒发送一次回显请求包。

注意在此示例中，2 和 4 之间存在空隙。这通常意味着某种类型的连接问题。数据包可能会乱序，但如果发生这种情况，仍然存在某种问题，因为 `ping` 每秒只发送一个数据包。如果响应超过一秒才到达，说明连接极其缓慢。

往返时间（round-trip time）是请求数据包发送到响应数据包到达之间的总持续时间。如果请求源和目的地之间存在不完整的路由，`ping` 会立即报告由于断开返回的 ICMP "host unreachable" 主机不可达）数据包。在有线局域网上，你应该预期完全没有丢包，且往返时间很低（上一个示例来自无线网络）。你还应该预期你的网络和 ISP（服务提供商）之间没有丢包，并且有合理、稳定的往返时间。

遗憾的是，互联网上并不是所有的主机都像以前那样响应 ICMP echo 回显数据包。因此，你可能会遇到这样的情况：你可以连接到某个主机上的网站，但得不到响应。

另一个基于 ICMP 的程序是 `traceroute`；当你学习本章中路由器的内容时它就会派上用场。使用 `traceroute host` 来查看数据包到达远程主机所经过的路径。`traceroute` 最好的功能之一是它会报告路由中每一步的返程时间，如下面的输出片段所示：

| 4 | 206.220.243.106 | 1.163 ms | 0.997 ms | 1.182 ms |
| 5 | 24.203.65 | 1.312 ms | 1.12 ms | 1.463 ms |
| 6 | 64.159.1.225 | 1.421 ms | 1.37 ms | 1.347 ms |
| 7 | 64.159.1.38 | 55.642 ms | 55.625 ms | 55.663 ms |
| 8 | 209.247.10.230 | 55.89 ms | 55.617 ms | 55.964 ms |
| 9 | 209.244.14.226 | 55.851 ms | 55.726 ms | 55.832 ms |
| 10 | 209.246.29.174 | 56.419 ms | 54.44 ms | 56.423 ms |

由于此输出显示在第 6 跳和第 7 跳之间存在巨大的延迟跳跃，该路由很可能是某种远距离链路。你可以在设置可工作接口时使用这些 ICMP 工具，接下来的章节将向你展示如何操作。

### 5.4 配置接口与主机到网络层

在 Linux 系统上，你通过网络接口将网络层连接到物理介质上，例如以太网网络或基于调制解调器的连接。常见的网络接口名称有 `eth0`（计算机中的第一块以太网卡）和 `ppp0`（PPP 接口）。

查看或手动配置网络接口设置最重要的命令是 `ifconfig`。要查看你当前接口的设置，运行此命令：

```
ifconfig -a
```

在 Linux 中你不需要 `-a`，但其他 Unix 变体需要此选项。输出看起来类似于所示：

```
+   - eth0 Link encap:Ethernet Hwaddr 00:40:05:A0:7F:96
  inet addr:10.1.2.2 Bcast:10.1.2.255 Mask:255.255.255.0
  UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
  RX packets:80961 errors:1 dropped:0 overflows:0 frame:
  TX packets:811658 errors:0 dropped:0 overflows:0 carrier:
  collisions:
- RX bytes:726765161 (693.0 Mb) TX bytes:110229902 (105.1 Mb)
- lo Link encap:Local loopback
  inet addr:127.0.0.1 Mask:255.0.0.0
  UP LOOPBACK RUNNING MTU:1636 Metric:1
  RX packets:44 errors:0 dropped:0 overflows:0 frame:0
  TX packets:44 errors:0 dropped:0 overflows:0 carrier:
  collisions:
  RX bytes:3569 (3.4 Kb) TX bytes:3569 (3.4 Kb)
```

左侧包含接口名称，右侧包含每个接口的设置。你可以看到每个接口都有一个 IP 地址（`inet addr`）和一个子网掩码（`Mask`），但你应该仔细注意包含 `UP` 和 `RUNNING` 的行，因为这些行告诉你接口正在工作。

`lo` 接口是一个虚拟网络接口，被称为环回（loopback），因为它“回环”自身。`127.0.0.1` 是 `localhost` 的 IP 地址，连接到这个地址等同于连接到你正在使用的机器。你的系统调用该地址。
