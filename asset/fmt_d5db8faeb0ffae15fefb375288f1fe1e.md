
```
RX packets:47 errors:0 dropped:0 overflows:0 frame:0

TX packets:13 errors:5 dropped:0 overflows:0 collisions:0 txqueuelen:1000

RX bytes:5560 (5.4 Kb) TX bytes:770 (770.0 b)

Interrupt:10 Base:0x8000
```

```
lo            Link encap:Local Loopback

               inet6 addr:::1/128 Scope:Host

               UP BACK RUNNING MTU:1636 Metric:1

               RX packets:3142 errors:0 dropped:0 overflows:0 frame:0

               TX packets:3142 errors:0 dropped:0 overflows:0 collisions:0 txqueuelen:1000

               RX bytes:3443414 (32.2 Mb) TX bytes:3443414 (32.2 Mb)
```

`ifconfig` 命令的输出显示 `eth0` 网卡具有 `IPv4` 地址 `3.4.5.6` 和 `IPv6` 地址 `fe80::280:cff6:fef9:1b8c`，该地址是由系统自动配置的，因为 `IPv6` 地址与硬件地址的后半部分（`Ethernet hwaddr:00:C6:F9:19:1B:8C`）相同。它还显示了接口统计信息以及 `IP` 地址为 `127.0.0.1` 的特殊环回适配器（`lo`）;此 `IP` 地址代表本地计算机，并且在所有使用 `TCP/IP` 的计算机上都是必需的。

```
stat -i 命令也可以用于显示接口统计信息。
```

如果您重启计算机，为 `eth0` 配置的 `TCP/IP` 信息将丢失。要让系统在每次启动时激活并配置接口的 `TCP/IP` 信息，只需在 `/etc/sysconfig/network-scripts/ifcfg-interface` 文件中（其中 `interface` 是网络接口的名称）放置条目。第一个以太网接口（`eth0`）的配置文件示例输出输出所示：

```
[server1]# cat /etc/sysconfig/network-scripts/ifcfg-eth0

DEVICE=eth0

BOOTPROTO=none

HWADDR=00:80:60:C9:F9:1B:8C

IPADDR=3.4.5.6

NETMASK=255.0.0.0

GATEWAY=3.0.0.1

ONBOOT=yes

TYPE=Ethernet

IPV6_INIT=yes

USERCTL=none

DEFROUTE=yes

IPV4_FAILURE_FATAL=yes

NAME="eth0"

UUID=5f06b5d-0bb0-7ffb-45f1-d66dd65f3e03

PEERNS=yes

PEERROUTES=yes

IPV6_AUTOCFIG=yes

IPV6_DEFAULTROUTE=yes

IPV6_PEERNS=yes

IPV6_PEERROUTES=yes

IPV6_FAILURE_FATAL=no
```

以下输出中的条目表示，如果存在配置了 `IPv6` 的路由器（`IPV6_AUTOCFIG=yes`），则第一个以太网适配器（`eth0`）的 `TCP/IP` 配置将在启动时激活（`ONBOOT=yes`）。网卡不从 `DHCP` 或 `BOOT` 服务器获取信息（`BOOTPROTO=none`）。相反，网卡使用 `IP` 地址 `3.4.5.6`、子网掩码 `255.0.0.0` 和默认网关 `3.0.0.1` 进行配置。可以使用 `BOOTPROTO=none` 行更改 `BOOTPROTO=dhcp` 或 `BOOTPROTO=bootcp`，从网络上的 `DHCP` 或 `BOOT` 服务器获取任何 `TCP/IP` 配置信息。

> `/etc/sysconfig/network-scripts/ifcfg-eth0` 文件也可以包含有关其他协议（如 `IPX/SPX`）配置的信息。编辑 `/etc/sysconfig/network-scripts/ifcfg-eth0` 文件后，不需要重启系统即可使新的 `TCP/IP` 配置生效。只需运行命令 `ifconfig down eth0` 卸载 `eth0` 网络接口，然后运行 `ifconfig up eth0` 配置 `eth0` 网络接口。或者，您可以使用 `ifconfig down` 和 `ifconfig up` 来禁用和激活网络接口。在网卡配置为使用 `TCP/IP` 后，您应该使用 `ping` 命令测试配置。

## 配置接口

默认情况下，`ping` 命令每秒发送一次数据包，直到按下 `Ctrl+c` 键。要向环回接口发送五个请求，如下例所示：如果 `ping` 命令未能从环回接口接收任何响应，则 `TCP/IP` 本身存在问题。要向之前配置的 `IP` 地址发送五个请求，可以使用以下命令：

```
[server1]# ping -c 5 3.4.5.6

PING 3.4.5.6 (3.4.5.6) : 56 (84) bytes of data.

64 bytes from 3.4.5.6: icmp_seq=0 ttl=64

64 bytes from 3.4.5.6: icmp_seq=1 ttl=64

64 bytes from 3.4.5.6: icmp_seq=2 ttl=64

64 bytes from 3.4.5.6: icmp_seq=3 ttl=64

64 bytes from 3.4.5.6: icmp_seq=4 ttl=64

--- 3.4.5.6 ping statistics

5 packets transmitted, 5 received, 0% packet loss, time 4004ms

rtt min/avg/max/mdev = 0.106/0.119/0.157/0.022 ms
```

如果 `ping` 命令未能从新配置的 `IP` 地址接收任何响应，则 `TCP/IP` 配置存在问题。接下来，您需要测试 `Linux` 是否可以 `ping` 网络上的其他计算机。可以使用以下命令向 `IP` `3.0.0.2` 发送五个请求：

```
[server1]# ping -c 5 3.0.0.2

PING 3.0.0.2 (3.0.0.2) : 56 (84) bytes of data.

64 bytes from 3.0.0.2: icmp_seq=0 ttl=128

64 bytes from 3.0.0.2: icmp_seq=1 ttl=128

64 bytes from 3.0.0.2: icmp_seq=2 ttl=128

64 bytes from 3.0.0.2: icmp_seq=3 ttl=128

64 bytes from 3.0.0.2: icmp_seq=4 ttl=128

--- 3.0.0.2 ping statistics

5 packets transmitted, 5 received, 0% packet loss, time 400ms

rtt min/avg/max/mdev = 0.401/0.422/0.448/0.018 ms
```
