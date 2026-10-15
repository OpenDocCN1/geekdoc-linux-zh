
```
64 bytes from 192.168.1.1: icmp_seq=3 time=0.777 ms
64 bytes from 192.168.1.1: icmp_seq=4 time=0.659 ms

--- statistics ---

4 packets transmitted, 4 received, 0% packet loss, time 3003ms
rtt min/avg/max/mdev = 0.478/0.828/1.470/0.391 ms
```

`ping` 命令发送数据包并等待返回（平均 210ms）。如果你的 Linux 系统有多个接口，你必须小心使用本地链路地址：

```
$ ping6 -c 4 fe80::

PING fe80:: (fe80::1): 56 bytes of data

64 bytes from fe80::: icmp_seq=1 time=1.94 ms
64 bytes from fe80::: icmp_seq=2 time=0.203 ms
64 bytes from fe80::: icmp_seq=3 time=0.229 ms
64 bytes from fe80::: icmp_seq=4 time=0.217 ms

--- statistics ---

4 packets transmitted, 4 received, 0% packet loss, time 3003ms
rtt min/avg/max/mdev = 0.194/0.232/0.415/0.096 ms
```

通过 `ping` 本地和远程系统，你可以隔离网络问题。例如，如果你能 `ping` 本地计算机但不能 `ping` 远程系统，问题最可能出现在你的路由器配置上。如果你可以通过 IP 地址 `ping` 但不能通过名称 `ping`，问题出在你的 DNS 配置上。

## 追踪路由

高级 `ping` 是 `traceroute` 命令，它向你的系统和指定目标系统之间的每个计算机发送测试数据包。结果如下：

```
$ traceroute -n 10.1.0.43

traceroute 10.1.0.43 30 hops max, 52 byte packets

1 192.168.1.1 1.021 ms 36.519 ms 0.971 ms
2 10.18.8.1 17.250 ms 9.959 ms 9.637 ms
3 10.9.8.173 8.799 ms 19.501 ms 10.884 ms
4 10.9.8.133 21.059 ms 9.231 ms 103.068 ms
5 10.9.14.9 8.554 ms 12.982 ms 10.029 ms
6 10.1.0.44 10.273 ms 9.987 ms 11.215 ms
7 10.1.0.43 16.360 ms * 8.102 ms
```
