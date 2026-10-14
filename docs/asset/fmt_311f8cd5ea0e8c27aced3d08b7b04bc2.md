
```
127.0.0.1   localhost
::1         localhost
```

然后，你可以使用 `ifconfig` 和 `route` 命令创建接口：

```
$ sudo ifconfig lo 127.0.0.1
$ sudo route add 127.0.0.1 lo
```

这些命令将在内存中创建 localhost 接口（在 Linux 中，所有接口如 `eth0` 或 `pp0` 都是内存中创建的），并将 IP 地址 `127.0.0.1` 添加到内部（内存中）表中，以便 Linux 内核的网络代码能够跟踪路由。

使用之前所示的 `ifconfig` 命令来测试接口。

你应该能够使用 `ping` 来检查接口是否响应正常，如下（使用 localhost 或其 IP 地址）：

```
$ ping -c 3 localhost

PING localhost (127.0.0.1) 64 bytes of data.
64 bytes from localhost (127.0.0.1): icmp_seq=1 ttl=64 time=0.036 ms
64 bytes from localhost (127.0.0.1): icmp_seq=2 ttl=64 time=0.028 ms
64 bytes from localhost (127.0.0.1): icmp_seq=3 ttl=64 time=0.028 ms

```

--- localhost statistics

3 packets transmitted, 3 received, 0% packet loss, time 1999ms

rtt min/avg/max/mdev = 0.028/0.030/0.036/0.007 ms

```
`-c` 选项用于设置 ping 的次数，而该命令成功后（如之前）将返回向指定主机发送测试数据包的往返速度信息。

## 第 14 章 网络

`/etc/hosts` 文件的第二行使用计算机的实际主机名，并将其分配给与该计算机唯一的类似的 IP 地址。在之前的示例中，你可以看到 `127.0.0.1` 被分配给 `hardy-laptop`，即该 hosts 文件所在的计算机。

其余行用于 IPv6，除了以 `::1` 开头的行外，它们都可以忽略——该行用于定义 IPv6 的本地连接，你可以在终端通过 `ping6` 命令使用它，如下：

```bash
$ ping6 ::1

PING ::1(1) 56 data bytes

64 bytes from ::1: icmp_seq=1 ttl=64 time=0.037 ms

64 bytes from ::1: icmp_seq=2 ttl=64 time=0.045 ms

64 bytes from ::1: icmp_seq=3 ttl=64 time=0.048 ms

--- ::1 ping statistics

3 packets transmitted, 3 received, 0% packet loss, time 1998ms

rtt min/avg/max/mdev = 0.037/0.043/0.048/0.007
```
