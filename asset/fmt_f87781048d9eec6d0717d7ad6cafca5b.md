
```
ifconfig
eth0
Link encap:Ethernet HWaddr 00:AC:CC:40:98:A8
 addr:192.168.1.2 Bcast:192.168.1.255 Mask:255.255.255.0
UP BROADCAST MULTICAST MTU:1500 Metric:1
RX packets:268027 errors:0 dropped:0 overruns:0 frame:0
TX packets:28290 errors:0 dropped:0 overruns:0 carrier:0
collisions:17805 tqueuelen:100
Interrupt:9 Base address:0xec00
lo
Link encap:Local Loopback
 addr:127.0.0.1 Mask:255.0.0.0
UP LOOPBACK RUNNING MTU:3924 Metric:1
RX packets:51997 errors:0 dropped:0 overruns:0 frame:0
TX packets:51997 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 tqueuelen:0
```

当出现问题时，你最想知道的是接口是否处于激活状态。每个接口报告的第三行指示接口的状态和配置。在本示例中，`eth0`是激活的且处于`up`状态。

注意`ifconfig`还报告了你可能在某些感兴趣的其他状态信息。报告 MAC 硬件以太网地址`HWaddr`、IP 地址`inet addr`、广播地址`Bcast`以及网络子掩码。通常这些用用较小，还报告了默认最大帧大小`MTU`、接收数据包数`RX`和发送数据包数`TX`。

## 最大传输单元 (MTU) 与分片

将`MTU`保持为默认值`1500`是最好的。如今大多数网络都是以太网网络。`MTU`为`1500`字节。更大的链路层协议（例如`ATM`或令牌环）具有更大的建议`MTU`尺寸。将`MTU`设置为大于`1500`字节的值将确保数据包在跨越网络边界时在链路的某处发生分片。`TCP`连接在建立时会协商它们的`MTU`。

在当今的网络骨干中，由于分片技术得到了改进，带宽不再是大问题。分片所需的时间是一个重要的性能因素。与在传输过程中必须分片的少数大包相比，使用更多更小的包可以获得更好的性能。

![](img/65af6c8c09dbe707d567ca01d4bca008_273_0.png)

## 使用 ping 检查网络连接

对于测试基本的网络连通性，`ping`是首选工具。如果外部网络接口处于启用状态但你无法连接到远程主机，`ping`可以指示数据包是否通过了该接口。当然，必须在防火墙规则中启用`ping`流量。负面的`ping`响应并不证明远程站点已宕机，该站点可能没有回显`Echo ICMP`消息。正的`ping`响应证明数据包已传输且远程主机正在响应。

仅以主机名或`IP`地址作为参数，`ping`会无限发送数据包，直到你杀死该进程，此时`ping`会报告其最终统计信息：

> `<smtp.isp.domain>`

```
PING smtp.isp.domain (10.10.22.85): 56 bytes
64 bytes from 10.10.22.85: icmp_seq=0 ttl=253 time=4.2 ms
64 bytes from 10.10.22.85: icmp_seq=1 ttl=253 time=4.4 ms
64 bytes from 10.10.22.85: icmp_seq=2 ttl=253 time=4.1 ms
64 bytes from 10.10.22.85: icmp_seq=3 ttl=253 time=5.4 ms
64 bytes from 10.10.22.85: icmp_seq=4 ttl=253 time=3.9 ms
```

-- smtp.isp.domain ping statistics ---

5 packets transmitted, 5 packets received, 0% packet loss

round-trip min/avg/max = 3.9/4.4/5.4 ms

`ping`并不意味着该机器上的服务正在运行或可供你使用。它仅意味着`ping`数据包已经穿越网络，并且回复已找到返回。如果某个特定的网络服务不可用，或者特定的远程主机没有响应，只要某些东西有响应，你至少知道你的网络是正常运行的。

在这个示例中，你知道你`ISP`的邮件服务器机器正在运行。你不知道邮件服务器本身是否正在运行。也就是说，如果你的邮件服务挂起了，而你对你`ISP`的邮件服务器运行`ping`，你至少知道你的网络是通的。

## 260 第6章 验证系统正按预期运行

以下是`ps -ax`的典型示例输出：

> `ps -ax`

| PID | TTY | STAT | TIME | COMMAND |
| :--- | :--- | :--- | :--- | :--- |
| 1 | ? | S | 0:03 | init |
| 2 | ? | S | 0:02 | [kflushd] |
| 3 | ? | SW | 0:00 | [kpiod] |
| 4 | ? | SW | 0:01 | [kswapd] |
| 5 | ? | SW- | 0:00 | [mdrecoveryd] |
| 6 | ? | S | 0:00 | /sbin/hdcpcd |
| 8 | 521 | S | 0:03 | syslogd -m 0 |
| 9 | 632 | S | 0:00 | klogd |
| 10 | 546 | S | 0:00 | /usr/sbin/atd |
| 11 | 560 | S | 0:01 | crond |
| 12 | 574 | S | 0:01 | inet |
| 13 | 588 | S | 0:10 | named |
| 14 | 638 | S | 0:02 | httpd |
| 15 | 661 | ? | S | 0:07 | xfs |
| 16 | 893 | ? | S | 0:07 | /usr/local/sbin/sshd |
| 17 | 928 | tty2 | S | 0:00 | /sbin/getty tty2 |
| 18 | 938 | ? | S | 0:04 | update (bflush) |
| 19 | 1428 | tty1 | S | 0:00 | /sbin/getty tty1 |
| 20 | 3674 | ? | S | 0:00 | sendmail: accepting connections on port 25 |
| 21 | 17531 | ? | S | 0:00 | in.telnetd -n |
| 22 | 17532 | pty1/1 | S | 0:00 | login --bob |
| 23 | 17533 | pty1/1 | S | 0:00 | -ksh |
| 24 | 17542 | pty/1 | R | 0:00 | ps -ax |

第 1 行包含这些列标题：

- `PID`是唯一的进程`ID`。
- `TTY`是进程的控制终端，如果存在的话。
- `STAT`是进程的运行状态。在列表中，`ps`处于睡眠（Sleeping）状态，不在运行队列中，因为它们正在等待某些事件的发生或响应。
- `TIME`是该进程消耗的`CPU`时间。
- `COMMAND`是进程名称。

第 2 行显示`init`正在运行，它是所有进程的父进程。它始终运行。大多数`UNIX`变体在`init`死后会崩溃。

第 3 行显示`kflush`正在运行。`kflush`不是进程。它是一个内核线程，定期将文件系统缓冲区刷回磁盘。

第 4 行显示`kpiod`正在运行，`kpiod`不是进程。它是一个内核线程，用于选择物理内存页从内存交换到磁盘上的交换空间。

第 5 行显示`kswapd`正在运行，`kswapd`不是进程。它是一个内核线程，用于选择物理内存页从内存交换到磁盘上的交换空间，并为其他进程释放内存。

## 使用 ps -ax 所有进程

第 6 行显示`mdrecovery`正在运行，`mdrecovery`不是进程。它是一个内核驱动线程，用于将多个磁盘设备管理为单一单元，即`RAID`。

第 7 行显示`dhcpd`正在运行，它是`DHCP`客户端，从`DHCP`服务器接收动态`IP`分配。

第 8 行显示`syslog`正在运行，它是系统消息记录器。它收集程序消息并将其写入指定的日志文件、控制台等。

第 9 行显示`klog`正在运行，它是内核消息记录器。它从内核消息缓冲区收集消息，并与`syslog`协作将其写入指定的日志文件和控制台。

第 10 行显示`atd`正在运行，它是按定义时间调度程序的守护进程。`atd`是`cron`的用户级对应物。
