
## 列表 6-9 netstat 输出，显示已配置的 IP 地址。

```
bass:/>netstat -in

| 名称 | Mtu | 网络 | 地址 | Ikpnts | Ierrs | Okpnts | Oerrs | Coll |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| lo0 | 4136 | 127.0.0.0 | 127.0.0.1 | 4693211 | 0 | 4693219 | 0 | 0 |
| lan3 | 1500 | 15.13.168.0 | 15.13.168.61 | 30925479 | 0 | 7106611 | 0 | 0 |
| lan2 | 1500 | 192.5.1.0 | 192.5.1.61 | 873225 | 15 | 1555027 | 382 | 20374 |
| lan2:1 | 1500 | 192.5.1.0 | 192.5.1.3 | 16 | 0 | 0 | 0 | 0 |
| lan2:2 | 1500 | 192.5.1.0 | 192.5.1.9 | 16 | 0 | 0 | 0 | 0 |
| lan2:3 | 1500 | 192.5.1.0 | 192.5.1.7 | 16 | 0 | 0 | 0 | 0 |
| lan2:4 | 1500 | 192.5.1.0 | 192.5.1.5 | 16 | 0 | 0 | 0 | 0 |
| lan2:5 | 1500 | 192.5.1.0 | 192.5.1.19 | 16 | 0 | 0 | 0 | 0 |
| lan2:6 | 1500 | 192.5.1.0 | 192.5.1.15 | 16 | 0 | 0 | 0 | 0 |
| lan2:7 | 1500 | 192.5.1.0 | 192.5.1.13 | 16 | 0 | 0 | 0 | 0 |
| lan2:8 | 1500 | 192.5.1.0 | 192.5.1.17 | 16 | 0 | 0 | 0 | 0 |
| lan2:9 | 1500 | 192.5.1.0 | 192.5.1.29 | 16 | 0 | 0 | 0 | 0 |
| lan1* | 1500 | none | none | 0 | 0 | 0 | 0 | 0 |

bass:/>
```

## 列表 6-10 使用 netstat 显示 IP 统计数据。

```
# netstat -p ip
ip:
	112231915 total packets received
	0 bad header checksums
	0 with size smaller than minimum
	0 with data size < data length
	0 with header length < data size
	0 with data length < header length
	0 illegal ip source address
	178 ip version unsupported
	193 fragments received
	0 fragments dropped (dup or out of space)
	1 fragment dropped after timeout
	0 packets forwarded
	2382091 packets not forwardable
	0 redirects sent
```

## 列表 6-11 使用 netstat 显示 ICMP 统计数据。

```
# netstat -p icmp
icmp:
	7368 calls to generate an ICMP error message
	0 errors not generated because old message was ICMP
	0 errors not generated 'cuz old message was broadcast
	Output histogram:
	echo reply: 215963
	destination unreachable: 7368
64 messages with bad code fields
21 messages < minimum length
0 messages with a bad checksum
0 messages with bad length
Input histogram:
echo reply: 12231
destination unreachable: 182468
source quench: 35
routing redirect: 108
echo: 215963
time exceeded: 18
address mask request: 124
215963 responses sent
```

源抑制（source quench）是向系统发出的请求，要求其因拥塞而降低传输速率。路由重定向（Routing redirect）消息用于请求系统使用替代路径到达目标网络。

## 列表 6-12 使用 netstat 显示 TCP 统计数据。

```
#netstat -p tcp
tcp:
275906 packets sent
7346 data packets (948597 bytes)
0 data packets (0 bytes) retransmitted
12967 ack-only packets (1627 delayed)
0 URG only packets
22 window probe packets
1 window update packet
255570 control packets
523932 packets received
14736 acks (for 912101 bytes)
3299 duplicate acks
0 acks for unsent data
12785 packets (854136 bytes) received in-sequence
3 completely duplicate packets (0 bytes)
0 packets with some dup. data (0 bytes duped)
2837 out-of-order packets (0 bytes)
2 packets (0 bytes) of data after window
0 window probes
55 window update packets
0 packets received after close
0 discarded for bad checksums
0 discarded for bad header offset fields
0 discarded because packet too short
249910 connection requests
2842 connection accepts
5677 connections established (including accepts)
255585 connections closed (including 14 drops)
247075 embryonic connections dropped
15772 segments updated rtt (of 265683 attempts)
0 retransmit timeouts
		0 connections dropped by rexmit timeout
0 persist timeouts
0 keepalive timeouts
		0 keepalive probes sent
		0 connections dropped by keepalive
```

您可以随时间监控 TCP 统计数据，以查看是否正在建立新的连接，例如。

`netstat -a` 可用于显示 TCP 连接和 UDP 套接字的状态。例如，您可以确定连接是否已完全建立，或者服务器是否仍在等待客户端的连接请求。如果网络服务已在 `/etc/services` 中注册，输出将显示该服务的名称。

`netstat` 命令还可以用于显示正在使用以及专门用于网络数据包的记忆数量。如果在目的地或中间系统上用于 IP 分片重组的可用内存不足，网络性能可能会受到影响。数据将需要重新传输。您可以使用 `netstat -sp ip` 检查被丢弃的分片数量。`ndd` 命令可用于显示和更改 `ip_reass_mem_limit` 值。

## nettl

`nettl` 是 HP-UX 的主机端设施，用于跟踪进出系统的网络数据包。可以跟踪 IEEE802.3 和 FDDI 等链接，以及 TCP/IP 和 OSI 传输层等上层协议。`nettl` 还会记录有关网络事件的信息。

要使用 `nettl`，您首先需要启动跟踪设施。然后，您需要使用 `nettl -tn` 启动特定跟踪。您可以列出希望包含在跟踪中的特定网络子系统，例如网络层或传输层。

## 列表 6-13 使用 netstat 显示 UDP 统计数据。

```
# netstat -p udp
udp:
	0 incomplete headers
	0 bad data length fields
	0 bad checksums
	2217 socket overflows
	0 data discards
```

在启动跟踪时指定跟踪文件。根据输出的大小，`nettl` 会创建两个跟踪文件。最新的跟踪文件会添加 `.TRC0` 后缀，而较旧的文件将具有 `.TRC1` 扩展名。列表 6-14 展示了如何启动和停止对用于 ping 请求的 ICMP 流量进行的跟踪。

收集跟踪数据后，您可以使用 `netfmt` 格式化输出。格式化后的数据也可以写入文件。列表 6-15 展示了由前述跟踪生成的格式化文件的一部分。

由于对系统性能的影响，您应仅在无法通过其他工具诊断问题或系统具有显著过剩容量时使用 `nettl`。

## 列表 6-14 ICMP/ping 跟踪示例。

```
# nettl -start
# nettl -tn pduin pduout -e ns_ls_icmp -f pingtrc
# ping hoffman
PING hpssc16.cup.hp.com: 64 byte packets
64 bytes from 15.13.169.233: icmp_seq=0. time=2. ms
64 bytes from 15.13.169.233: icmp_seq=1. time=2. ms
64 bytes from 15.13.169.233: icmp_seq=2. time=2. ms

---hpssc16.cup.hp.com PING Statistics----
3 packets transmitted,  3 packets received, 0% packet loss
round-trip (ms)   min/avg/max = 2/2/2
# nettl -tf -e all
# netfmt -Nnl -f pingtrc.TRC0 > pingfmt
# nettl -stop
```

## 列表 6-15 ICMP/ping 格式化跟踪输出。

```
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^ARPA/9000 NETWORKING^^^^^^^^^^^^^^^^^^@#%
 Timestamp          : Tue Jan 26 PST 1999 10:41:05.634676
 Process ID         : [ICS]                     Subsystem        : NS_LS_ICMP
 User ID ( UID )   : -1                        Trace Kind       : PDU IN TRACE
 Device ID          : -1                        Path ID          : -1
 Connection ID      : 0
 Location           : 00123
------------------------ ICMP Header ------------------------------
type: ECHOREPLY          cksum: 0xffe3          .id: 10715        seq: 1
code: none
------------------------- User Data --------------------------------
        0: 36 ae 0c 41 00 09 a8 44 08 09 0a 0b 0c 0d 0e 0f  6..A..D........
       16: 10 11 12 13 14 15 16 17 18 19 1a 1b 1c 1d 1e 1f  ................
       32: 20 21 22 23 24 25 26 27 28 29 2a 2b 2c 2d 2e 2f  !"#$%&'()*+,-./
       48: 30 31 32 33 34 35 36 37 -- -- -- -- -- -- -- --  01234567.........
```

## 监控网络服务

各种应用程序可以通过互联网或企业内网进行访问。例如，客户端应用程序可能使用网络访问服务器系统上的应用程序。在服务器系统上运行的应用程序被称为网络服务。

用户关心的是网络服务的可用性和响应时间。本节讨论用于监控网络服务的工具。讨论了一些更常见的网络服务，如域名系统（DNS）、网络信息服务（NIS）和网络文件系统（NFS）。其他应用程序将在第 7 章中讨论。

许多网络服务是由*守护进程*在响应客户端请求时启动的。该守护进程被称为*inetd*。您可以使用*ps*查看该守护进程是否正在运行。如果没有运行，您应尝试通过以*超级用户*身份执行 `/usr/sbin/inetd` 来重新启动它。您可以使用*netstat* –a 列出当前在系统上运行的网络应用程序。与每个服务相关的 TCP 或 UDP 套接字端口列在文件 `/etc/services` 中。如果某个服务没有运行，您可能需要检查此文件以查看该服务是否已配置。该服务还应列在文件 `/etc/inetd.conf` 中。*inetd* 守护进程在新服务启动或停止时会将错误和信息消息写入 `/var/adm/syslog/syslog.log`。

还有其他重要的网络服务始终处于激活状态（或应该处于激活状态）。这些服务包括 NFS 和 HTTP。本节其余部分列出了特定于每个网络服务的监控工具。

## 监控 DHCP/BOOTP 服务器

引导协议（BOOTP）允许系统从远程服务器系统获取其网络配置信息，例如其 IP 地址。BOOTP 服务 *bootpd* 可能使用 trivial file transfer protocol（TFTP）将数据传回客户端。确保两者都已在 `/etc/services` 和 `/etc/inetd.conf` 中配置为 Internet 服务。

在收到 BOOTP 请求时，服务会检查其数据库中是否包含客户端的信息。如果包含，它会回复该信息；否则，它可能会将请求转发到另一台系统。您可能需要一个分析器来确保客户端在 BOOTP 请求中设置的关键参数是正确的。

客户端信息放在文件 `/etc/bootptab` 中。如果 BOOTP 总体上工作正常，但对特定系统不起作用，您应检查此文件以确保配置信息是正确的。您可能想要通过服务器使用 *bootquery* 发出测试，它可以用于向 BOOTP 服务器发送测试 BOOTP 请求。这样，您可以验证该服务是否在响应查询时启动。通过在查询中指定客户端地址，并启用向此客户端广播回复——这是 `/etc/bootptab` 中的一个配置选项——您可以看到由该 BOOTP 服务器发送的实际回复。

动态主机配置协议（DHCP）是 BOOTP 的一个超集。*bootpd* 和 DHCP 都可以将一些错误消息写入系统日志文件。如果您正在排查问题，请确保 *bootpd* 是带 `–d 2` 命令选项启动的，以便将信息性日志消息写入系统日志文件。

