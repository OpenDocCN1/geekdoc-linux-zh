

## ping

所有网络探测命令中最基本的一个，ping 向远程主机发送往返数据包并报告它们往返所需的时间。启动方式如下：

```
$ ping remote-host
```

按 CTRL-C 可停止它。终止时，ping 会报告平均时间和丢包百分比。并非所有远程主机都会响应 ping。

ping 的 -f（洪泛 ping）选项每秒发送至少 100 个数据包。通常负载正常的本地以太网连接应该能处理洪泛 ping，但当你有不稳定或性能不佳的连接时，会丢失大量洪泛 ping 数据包。在大多数 ping 版本中，只有以 root 身份登录时才能使用洪泛选项。

## netstat

此命令显示网络连接状态。如果你的网络出现问题，重要的是要知道机器连接了什么。典型用法是带一两个选项来过滤输出：-t 仅显示 TCP 连接（通常是你想要的），-n 禁用主机名查找（在网络如此缓慢导致查找挂起时很有用）。-a 选项列出每个活动端口。下面展示了 netstat 的使用示例。

## PROBLEM 14

症状：使用 ping -f 时，网络上丢失了许多数据包并发生过量冲突。
问题：较旧、优化不佳的网络或布线不良。
修复：尝试消除 10Mbps 网络上的细同轴以太网和级联集线器等硬件。在某些瓶颈处，以太网交换机可以改善情况，但即使是 100Mbps 共享集线器也有帮助。另外，注意布线是否不良，尤其是成对未正确对齐的五类双绞线。

```
$ netstat -t -u
Active Internet connections (w/o servers)
Proto Recv-Q Send-Q Local Address          Foreign Address        State
tcp    0      0 10.1.2.1:3128          mikado:4310            FIN_WAIT2
tcp    0      109 dialup-s229-8:1020    broadband.example.co:ssh ESTABLISHED
tcp    0      0 dialup-s229-8:1023    broadband.example.co:ssh ESTABLISHED
tcp    0      438 dialup-s229-8:2787    209.207.224.222:www    ESTABLISHED
tcp    0      0 dialup-s229-8:2786    209.207.224.222:www    ESTABLISHED
tcp 0 0 10.1.2.1:3128 mikado:2872 FIN_WAIT2
tcp 0 0 10.1.2.1:1912 mikado:6000 ESTABLISHED
udp 0 0 10.1.2.1:ntp *:* 
udp 0 0 localhost:ntp *:*
```

第一行显示 netstat 正在列出 TCP（-t 选项）和 UDP（-u 选项）连接（单独使用 netstat 会显示 Unix 域套接字——由于 syslogd 和其他一些项目，这会产生相当长的列表）。上面的列表来自家里的网关机器。此列表包括来自其中一个以太网接口（10.1.2.1）的连接——一个 PPP 拨号连接。该机器还运行了 3128 端口的 Web 代理服务器。机器 mikado 上的 Web 浏览器请求了一个网页，因此 mikado 连接到我们的 3128 端口，而我们又前往 209.207.224.222 的 www 端口（80）获取该页面。我们还向名为 broadway 的机器打开了两个 ssh 连接。倒数第二行显示正在运行一个 NTP（网络时间协议）守护进程，使用 UDP 而不是 TCP。

请注意，服务名称（如本例中的 ssh、www 和 ntp）是文件 /etc/services 中的对应端口。

## traceroute

此命令追踪到远程主机的路由并报告连接之间的时间。尝试使用 www.userfriendly.org——输出如下所示：

```
$ traceroute www.userfriendly.org
traceroute to www.userfriendly.org (207.6.140.17), 30 hops max, 40 byte packets
1 rsm-ryerson-v11 (128.135.11.210) 0.658 ms 0.731 ms 0.599 ms
2 vipernet-gw-a30-4.uchicago.edu (128.135.253.1) 2.382 ms 1.366 ms 1.281 ms
3 NChicago1-core0.nap.net (207.227.0.209) 32.673 ms 119.314 ms 18.613 ms
4 NChicago2-core0.nap.net (207.112.247.181) 8.337 ms 9.396 ms 8.287 ms
5 NSeattle1-core0.nap.net (207.112.247.169) 62.974 ms 62.059 ms 54.506 ms
6 * seo-0c3.bctel.net (207.227.3.154) 48.438 ms 50.563 ms
7 inetgw4.s1.bctel.net (209.53.75.93) 59.654 ms * 59.62 ms
8 204.239.129.205 (204.239.129.205) 55.683 ms 60.692 ms 61.28 ms
9 www.userfriendly.org (207.6.140.17) 59.601 ms 63.771 ms 67.636 ms
```

注意 NChicago2-core0.nap.net 和 NSeattle1-core0.nap.net 之间的延迟差距很大。主机和第一个网关之间的跳是快速的，数字反映了网络速度。在 1 和 2 之间，差距略有扩大。然后事情开始变得繁忙。在第 6 和第 7 跳，星号（*）表示该路由器相当繁忙，没有时间返回 traceroute 所依赖的其中一个 ICMP TIME_EXCEEDED 消息。

如果 traceroute 给出结果 23 * * *，则网关不可达（如果远程主机也不可达，这不足为奇）或它只是不想返回消息。你偶尔会收到其他消息，例如 !H（主机不可达）；traceroute（8）手册页概述了不同的 traceroute 消息。

