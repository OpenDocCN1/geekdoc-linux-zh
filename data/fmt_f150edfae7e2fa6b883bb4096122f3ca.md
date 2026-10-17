
`collisions:0 txqueuelen:1000`

`RX bytes:3443414 (3.2 Mb) TX bytes:3443414 (3.2 Mb)`

```
[root@server1]# _
```

`ifconfig` 命令的输出还显示了接口统计以及 IP 地址为 127.0.0.1 的特殊环回适配器（lo）；此 IP 地址代表本地计算机，是所有使用 TCP/IP 的计算机所需的。

`netstat -i` 命令也可用于显示接口统计。

![](img/8fe037bf1ed016dccb79dbd1a27184f2_632_0.png)

# 第14 章 网络配置

如果你重启计算机，为 eth0 配置的 TCP/IP 信息将会丢失。为了允许系统在每次启动时激活并配置接口的 TCP/IP 信息，只需在 `/etc/sysconfig/network-scripts/ifcfg-interface` 文件中放置条目，其中 `interface` 是网络接口的名称。第一个太网（eth0）的配置文件示例如下输出所示：

```
[server1 root]# cat /etc/sysconfig/network-scripts/ifcfg-eth0

DEVICE=eth0

BOOTPROTO=none

HWADDR=00:80:C6:F9:1B:8C

IPADDR=3.4.5.6

NETMASK=255.0.0.0

GATEWAY=

ONBOOT=yes

IPV6_INIT=no

[server1 root]#
```

提供输出中的条目表明，第一个太网适配器（eth0）的 TCP/IP 配置将在启动时激活（`ONBOOT=yes`）。该 NIC 不从 DHCP 或 BOOT 服务器获取信息（`BOOTPROTO=none`）；而是使用 IP 地址 3.4.5.6、子网掩码 255.0.0.0 和默认网关 3.0.0.1 进行配置。此文件中不会包含广播地址，因为系统可以根据子网掩码轻松计算出它。此外，你也可以将 `BOOTPROTO=none` 行改为 `BOOTPROTO=dhcp` 或 `BOOTPROTO=bootp`，分别从网络上的 DHCP 或 BOOT 服务器获取所有的 TCP/IP 配置信息。

> `etc/sysconfig/network-scripts/ifcfg-eth0` 也可以包含关于 IPX/SPX 等其他网络协议配置的信息。

在编辑 `/etc/sysconfig/network-scripts/ifcfg-eth0` 后，你不需要重启系统即可让新的 TCP/IP 配置生效；只需运行命令 `ifdown eth0` 取消 eth0 接口的配置，然后运行 `ifup eth0` 使用 `/etc/sysconfig/network-scripts/ifcfg-eth0` 文件中的设置配置 eth0 接口。

在 NIC 配置为使用 TCP/IP 后，你应该通过数据分组分组控制程序（ping）测试配置。`ping` 命令向另一个 IP 地址发送较小的 TCP/IP 数据包并等待响应。默认情况下，ping 命令每秒发送一次包，直到按下 Ctrl+c；要向环回接口发送五个请求，请在 ping 命令中使用 `-c` 选项，如下所示：

```
[server1 root]# ping -c 5 127.0.0.1

PING 127.0.0.1 (127.0.0.1) 56 (84) bytes of data.

64 bytes from 127.0.0.1: icmp_seq=0 ttl=64 time=0.154
64 bytes from 127.0.0.1: icmp_seq=1 ttl=64 time=0.109
64 bytes from 127.0.0.1: icmp_seq=2 ttl=64 time=0.110
64 bytes from 127.0.0.1: icmp_seq=3 ttl=64 time=0.119
64 bytes from 127.0.0.1: icmp_seq=4 ttl=64 time=0.111
----
127.0.0.1 statistics
5 packets transmitted, 5 received, 0% packet loss, time=399ms
rtt min/avg/max/mdev = 0.109/0.120/0.154/0.020 ms
```

## 配置 NIC 接口 615

> 如果命令未能从环回接口接收任何响应，说明 TCP/IP 本身有问题。此外，向之前配置的 IP 地址发送五个 ping 请求，你可以使用以下命令：

```
[root@server1]# ping -c 5 3.4.5.6

PING 3.4.5.6 (3.4.5.6) 56 (84) bytes of data.

64 bytes from 3.4.5.6: icmp_seq=0 ttl=64 time=0.157

64 bytes from 3.4.5.6: icmp_seq=1 ttl=64 time=0.113

64 bytes from 3.4.5.6: icmp_seq=2 ttl=64 time=0.106

64 bytes from 3.4.5.6: icmp_seq=3 ttl=64 time=0.107

64 bytes from 3.4.5.6: icmp_seq=4 ttl=64 time=0.115

---

3.4.5.6 statistics

5 packets transmitted, 5 received, 0% packet loss, time=4000ms

rtt min/avg/max/mdev = 0.106/0.119/0.157/0.022 ms
```

> 如果命令未能从新配置的 IP 地址接收任何响应，说明 NIC 的 TCP/IP 配置有问题。

接下来，测试 计算机是否可以 ping 同网络上的其他计算机；可以使用以下命令向 IP 地址 3.0.0.2 的计算机发送五个 ping 请求：
