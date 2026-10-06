

## C.2 使用 ping 测试可连性

-allmulti 禁用多路模式。
irq, io_addr 和 mem_start 分别设置网络适配器的中断号、I/O 地址和内存地址。

## 使用 PING 测试可连性

当计算机无法访问时，ping 通常是第一个用于检查网络连接的工具。ping 向指定的计算机发送一个 ECHO_REQUEST 数据包并期望收到 ECHO_REPLY。（参见第 24.4 节）。此外，ping 还会输出关于连接的统计值。还可以使用 IP 选项记录路由来跟踪数据包的路由。

## 语法

```
ping [-DdfLnqRrv] [-c number] [-I address] [-i time]
  [--l number] [-p pattern] [-s size] [-t ttl] [-w time]
  computer
```

ping 有以下选项：

- -c number：ping 只发送指定的数据包后终止。通常情况下，ping 会一直运行直到进程停止。
- -f：运行所谓的洪洪模式 ping（flood ping）。这意味着 ping 发送数据包的数量与其收到的回复相同，或者至少每秒发送一百个。此选项可检查网络或系统在高负载下的行为。
- -i address：指定用于发送回显数据包的网络设备（通过 IP 地址）。
- -i time：指定两个回显请求包之间的等待时间。该值通常为一秒。
- -l number：以最大速度发送指定数量的数据包。随后，ping 将切换到普通传输模式。
- -n：防止解析和输出 DNS 名称。IP 地址以十进制形式写入。
- -p pattern：用指定的模式填充回显包。这允许你检查具有特定内容数据包的行为。
- -q：静默模式，仅在程序关闭时输出统计信息。
- -r：启用 IP 选项记录路由。（参见第 14.4 节）。它会输出经过的所有路由器，这些路由器必须支持记录路由选项。
- -s size：设置 ICMP 数据包的大小为字节数。通常，回显数据包的大小为 6 字节。加上 ICMP 头（8 字节），大小即为 64 字节。
- -t ttl：将数据包头中的生存时间（Time-Live）字段值设置为 ttl，这允许你限制回显请求的到达范围。
- -w time：设置等待回显请求回复的最大等待时间为 time 秒。等待回显请求回复的正常等待时间为十秒。

## 示例

```
root@tux # ping www.Linux-netzwerkarchitektur.de
PING.Linux-netzwerkarchitektur.de (192.67.198.52): 56 data bytes
64 bytes from 192.67.198.52: icmp_seq=0 ttl=224 time=4.589 ms
64 bytes from 192.67.198.52: icmp_seq=1 ttl=224 time=3.481 ms
64 bytes from 192.67.198.52: icmp_seq=2 ttl=224 time=3.271 ms
64 bytes from 192.67.198.52: icmp_seq=3 ttl=224 time=3.785 ms
--- www.Linux-netzwerkarchitektur.de ping statistics ---
4 packets transmitted, 4 packets received, 0% packet loss
round trip min/avg/max = 3.271/3.781/4.589 ms
```

## C3 使用 NETSTAT 查看网络状态

netstat 是一个查看网络状态的强大工具。例如，你可以使用 netstat 显示路由表和当前创建的 socket 状态。

### 显示路由表 如果使用 -r 选项启动它，netstat 会输出内核的路由表。这对应于 route 命令的结果。-n 用于输出计算机的 IP 地址而不是其 DNS 名称。

```
root@tux # netstat -nr
Kernel routing table
```

| Destination | Gateway | Genmask | Flags | MSS | Window | Use | Iface |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 129.13.42.0 | 0.0.0.0 | 255.255.255.0 | U | 0 | 0 | 478 | eth0 |
| 127.0.0.0 | 0.0.0.0 | 255.0.0.0 | U | 0 | 0 | 50 | lo |
| 0.0.0.0 | 129.13.42.233 | 0.0.0.0 | UG | 0 | 0 | 238 | eth0 |

此输出的第一列显示路由目的。Flags 显示目的地的类型（例如，网关 (G) 或主机 (H)），以便更好地解释第一列中的条目。

如果存在网关（路由器），第二列显示该路由器的 IP 地址（更准确地说，是数据包到达路由器时的适配器 IP 地址）。如果路由不跨越网关，则第二列显示值 0.0.0.0。

第三列显示路由的范围。在以（子）网络为目的地的路由中，第三列显示路由的范围。

