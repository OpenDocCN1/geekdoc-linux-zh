
更多信息请参阅 `man nsswitch.conf`。

## 网络配置命令

### ip 命令

特定于发行版的脚本和图形化工具是 `ip`（或旧版系统上的 `ifconfig` 和 `route`）的前端，用于显示和配置内核的网络配置。

`ip` 命令用于为接口分配 IP 地址、设置通往互联网和其他网络的路由、显示 TCP/IP 配置等。

以下命令显示了 IP 地址和路由信息：

```
benny@home benny> ip addr show
```

```
1: lo: <LOOPBACK,UP> mtu 16384 qdisc queueing
link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
inet 127.0.0.1/8 brd 255.255.255 scope host
inet6 ::/128 scope host
2: eth0:  <BROADCAST,MULTICAST,UP> mtu 1500 qdisc piffo_fast qlen 1000
link/ether 00:50:5f:7e:49:4a brd ff:ff:ff:ff:ff:ff
inet 192.168.1.24/25 brd 255.255.255 scope global
inet6 ::80::bff:fe7d:54a/10 scope link
```

```
benny@home benny> ip addr show
```

```
benny@home benny> ip route show
default via 192.168.1.1 dev eth0 proto static metric 100
192.168.1.0/24 dev eth0 scope link dhcp
```

以下是关于网络配置信息：

你的系统文档提供了许多关于工具可用性和使用的建议和信息。

你需要的信息：

- 连接到局域网（例如连接你的家庭电脑或工作电脑）：主机名、域名名和 IP 地址。如果你想最好地配置网络，请先进行更多阅读。在工作场所，这些信息可能在系统启动时自动提供给你的计算机。如果不确定，最好不要指定任何信息，而不是随意编造。
- 连接互联网：你的 ISP 用户名和密码，使用调制解调器时的电话号码。你的 ISP 通常会自动为你分配 IP 地址以及让你的互联网应用程序工作所需的所有其他内容。

### 使用 netstat 检查主机配置

除了显示网络配置的 `ip` 命令外，还有一个常用的命令 `netstat`，它有很多选项，并且在任何 UNIX 系统上都有用。

可以通过 `netstat` 命令的 `-nr` 选项显示路由信息：

```
bob~ netstat -nr
Kernel IP routing table
| Destination | Gateway | Genmask | Flags | MSS | Window | irtt | Iface |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 192.168.4.0 | 0.0.0.0 | 255.255.255.0 | U | 40 | 0 | 0 | eth0 |
| 127.0.0.0 | 0.0.0.0 | 255.0.0.0 | U | 40 | 0 | 0 | lo |
| 0.0.0.0 | 192.168.1.42 | 0.0.0.0 | UG | 40 | 0 | 0 | eth0 |
```

这是一个 IP 网络中的典型客户端机器。它仅有一个网络设备 `eth0`。`lo` 接口是本地回环地址。

### 现代方法

从系统中获取这些信息的新颖方法是使用 `ip` 命令：

```
ip route show
```

当这台机器连接到位于另一个网络的主机时（以 `0.0.0.0` 开头的行表示），它会将请求发送到 IP 地址为 `192.168.42.1` 的机器（路由器），并使用其主接口 `eth0` 执行此操作。

位于同一网络的主机（以 `192.168.42.0` 开头的行）也将通过主接口进行连接，但不需要路由器，数据直接发布到网络上。

机器的路由表可能比这个复杂得多，有许多不同的“目标地址-网关”对来连接不同的网络。如果你有机会连接到应用程序服务器（例如在工作期间），检查路由信息将很有益。

## 其他主机

有许多工具专注于 Linux 机器的网络管理和远程管理。你的 Linux 软件提供了许多此类工具。在本文中我们就不详细讨论它们了，请参考特定程序的文档。

我们在本节中只讨论一些 UNIX/Linux 文本工具。

### host 命令

要显示主机或域的信息，请使用 `host` 命令：

```
[emmy@pc10 emmy]$ host www.uenet.be
www.uenet.be. has address 193.74.208.157
```

```
[emmy@pc10 emmy]$ host -t any uenet.be
uenet.be. SOA dns.uenet.be. hostmaster.Belgium.EU.
2002021300 28800 7200 60480 86400
uenet.be. mail is handled by 50 pohost.uenet.be.
uenet.be. name server ns.EU.net.
```

### 网络

`eunet.be` 名称服务器为 `dns eunet.be`。

可以使用 `dig` 命令显示类似的信息，它提供了更多关于记录如何在名称服务器中存储的额外信息。

### ping 命令

要检查主机是否在线，请使用 `ping`。如果你的系统配置为发送多个数据包，请使用 `Ctrl+C` 组合中断 `ping`：

```
[emmy@pc10 emmy]$ ping a.host.be
PING a.host.be (1.2.8.3) : 56(64) bytes of data.
64 bytes from a.host.be (1.2.8.3) : 1icmp_seq=0 ttl=224 time=99.977msec
-- a.host.be ping statistics
1 packets transmitted, 1 packets received, 0% packet loss
round-trip min/avg/max/mdev = 99.977/99.977/0.000 msec
```

### traceroute 命令

要检查到网络主机的路由，请使用 `traceroute` 命令：

```
[emmy@pc10 emmy]$ /usr/bin/traceroute www.eunet.be
troute to www.eunet.be(193.74.208.177) 30 hops max, 38 packets
1 blob (10.0.0.1)
0.297ms 0.275ms 0.174ms
2 adsl-65.myprovider.be (217.136.111.1)
12.120ms 13.058ms 13.009ms
3 194.728.257 (194.788.257)
13.845ms 14.308ms 12.756ms
4 gigabitether-2.int12.gamms.skynet.be (195.238.2.226)
13.123ms 13.164ms 12.527ms
5 pebcru2.car.lebone.be (194.788.255.118)
16.536ms 13.889ms 15.028ms
6 ser-2-110-ias-be-vil-a01.kpgium.be (194.219.224.9)
14.602ms 15.546ms 19.950ms
7 unknown-195.207-93.eunet.be (195.207.93.49)
16.514ms 17.661ms 18.889ms
8 SO-0-1.Leuven.EU.net (195.207.129.1)
22.714ms 19.193ms 18.432ms
9 dukat.EU.net (193.74.208.178)
22.758ms 25.263ms
```

在某些系统中，`traceroute` 被重命名为 `tracepath`。

### whos 命令

可以使用 `whos` 命令查询特定的域信息，如下面的 `whos` 服务器所示：
