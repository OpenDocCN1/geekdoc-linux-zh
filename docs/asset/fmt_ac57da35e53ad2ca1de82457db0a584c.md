
```
root@ubuntu:~# ip --colorauto address
1: lo: <LOOPBACK,UP,LOWER> mtu 65536 disc no ownque state UNKNOWN default qlen 1000
    link/loopback 00:00:00:00:00:00 br 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host
        valid forever preferred left forever
    inet6 ::/128 scope host
        valid_ forever preferred left forever
2: enps0: <BROADCAST,UP,LOWER> mtu 1500 qdisc default group qlen 1000
    link/ether 25:54:00:ae:00:b8 ff:ff:ff:ff:ff:ff
    inet 192.168.122.101/24 br 192.168.122.255 scope dynamic enp10
        valid forever preferred left forever
    inet6 fe80::50f4:ff:fecc:8b84/64 scope link
        valid forever preferred left forever
3: enp0s31ff6: <BROADCAST,MULTICAST,UP,LOWER> mtu 1500 qdisc noep state DOWN group qlen 1000
    link/ether 25:54:02:07:3a:f8 ff:ff:ff:ff:ff:ff
```

图 7.6：`ip address` 命令的输出示例

该接口始终分配并配置了上述的 IP `127.0.0.1`，网络掩码为 `255.0.0.0/(8)`。参考图 7.6，显示了接口 `enp1s0` 配置了 IP `192.168.122.101`，网络掩码为 `255.255.255.0/(24)`，广播 IP 为 `192.168.122.255`。

名为 `enp1s0` 的接口已分配了 IPv6 本地地址（以 `fe80::/64` 开）。图 7.7 显示了一个配置了 IPv6 地址的接口示例：

```
root@#: ip --color -6 address show dev eth
2: eth0: <BROADCAST,UP,MULTICAST,LOWER> mtu 1500 state UP qlen 1000
    inet6 2006:41d0:1ee6:e26:1/128 scope global
        valid forever preferred left forever
    inet6 fe80::225:90ff:fe22:424a/64 scope link
        valid forever preferred left forever
```

图 7.7：带有 IPv6 地址的 `ip address` 命令的输出示例

## 网络层（第三层）

第三层需要访问非本地网络的信息。这包括用于访问网络外部的默认网关，以及访问其他网络所需的特定网关。带有 `route` 参数的 `ip` 命令列出了目的地和网关表。图 7.8 显示了一个示例：

```
root@ubuntu:~# ip -- route
default via 192.168.122.1 dev enp1s0 proto dhcp src 192.168.122.101 metric 100
    192.168.122.0/24 dev enp1s0 proto kernel scope link src 192.168.122.101 metric 100
```

图 7.8：`ip route` 命令的输出示例

在图 7.8 所示示例中，默认网关为 `192.168.122.1`。它将作为所有目的地不是 `192.168.22.0/24` 的通信的跳数。如果通信的是本地网络中的 IP，则不涉及网关，通信是直接的。图 7.9 显示了一个 IPv6 的示例：

```
root@lub:~# ip --color -6 route
2001:48d0:1ee26:1 dev eth0 proto kernel metric 256 pref medium
2001:48d0:1eeff:ff:ff dev eth0 metric 1024 pref medium
fe80::64 dev eth0 proto kernel metric 256 pref medium
default via 2001:48d0:1eeff:ff:ff dev eth0 metric 1024 pref medium
```

图 7.9：`ip route` 命令的输出示例

`route` 命令允许使用名为 `get` 的有用参数来获取访问它的信息。图 7.10 显示了两个示例，第一个是关于网络之外的 IP，第二个是本地网络中的 IP：

```
root@ubuntu:~# ip --color route get 8.8.8.8
8.8.8.8 via 192.168.122.1 dev enp0 src 192.168.122.101 uid 0
root@ubuntu:~# ip --color route get 192.168.122.251
192.168.122.251 via 192.168.122.1 dev enp1s0 proto dhcp src 192.168.122.101 metric 100
```

图 7.10：`ip route get` 的输出示例

如第 6 节所述，有很多工具可以检查本地网络流量，例如 `traceroute`、`tracepath` 和 `mtr`。ICMP 协议（第三层）用于检查网络跳数。

## 传输层（第四层）

传输层依赖于端口。例如，传输控制协议（TCP）和用户数据报协议（UDP）。传输层负责在端到端之间传输数据。传输层可以是可靠的（如 TCP），也可以是不可靠的（如 UDP）。

### 传输层

传输层可以分配和配置端口。端口是用于标识特定进程的符号。这些端口分为三类：已知端口（0-1023）、注册端口（1024-49151）和动态端口（49152-65535）。

显示了 `ifcfg-ens3` 文件的内容示例，使用 DHCP 配置接口 `ens3`：

```
TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=dhcp
DEFROUTE=yes
IPV4_FAILURE_INIT=none
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=none
NAME=ens3
UUID=02cc87e6-dc7c-4c9e-a530-f908611c7f5e
DEVICE=ens3
ONBOOT=
```

在较新的版本中，`NetworkManager` 使用 `/etc/NetworkManager/system-connections` 目录来存储配置。以下代码显示了一个名为 `enp1s.nmconnection` 的文件示例，使用 DHCP 配置接口 `enp1s`：

```
[connection]
id=enp1s
uid=320f6572-672b-33c8-9014-b0fb087aela2
type=ethernet
autoconnect-priority=999
interface-name=enp1s
tim=1656276248
[ethernet]
[ipv4]
method=auto
[ipv6]
addr-gen-mode=e64
method=auto
[proxy]
```

`NetworkManager` 包含了几个用于查询、管理设备和连接配置的命令。`nmcli` 命令用于在命令行中执行操作，而 `nmui` 命令用于在控制台的用户界面中执行操作。

## 命令 nmcli

该命令行工具用于控制 `NetworkManager` 并查询状态。该命令允许通过第一个参数来指示要管理的组件，配置网络的的常用选项描述在表 7:2 中：

| 参数 | 描述 |
| --- | --- |
| `general` | 通用状态和设置主机名 |
| `connection` | 管理连接 |
| `device` | 管理由 `NetworkManager` 管理的设备 |
| `monitor` | 监控 `NetworkManager` 变化 |

表 7:2：`nmcli` 命令的第一个参数选项

参数 `general` 显示系统的通用状态，如图 7:14 所示：

```
[root@rhel ~] nmcli general
STATE CONNECTIVITY WIFI-HW WIFI WWAN-HW WWAN
connected full enabled enabled enabled
```

图 7:14：`nmcli` 命令的输出示例。
