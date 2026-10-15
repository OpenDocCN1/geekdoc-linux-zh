
不同的变量定义在文件中。表 6.1 列出了这些变量。

# 表 6.1 常见的 ifcfg 配置变量

| 参数 | 值 |
| :--- | :--- |
| DEVICE | 指定设备在服务器上的名称。 |
| NM_CONTROLLED | 指定设备是否由 NetworkManager 控制，默认情况下如此。 |
| ONBOOT | 指示设备在服务器启动时启动。 |
| TYPE | 指示设备类型，通常为以太网。 |
| BOOTPROTO | 如果需要从 DHCP 服务器获取 IP 地址，则设置为 `dhcp`。设置为其他任何值均使用固定 IP 地址。 |

#### 理解 NetworkManager

| 参数 | 值 |
| :--- | :--- |
| DEFROUTE | 如果设置为 `yes`，此处指定的网关也将作为默认路由。 |
| IPV4_FATAL | 如果 IPv4 配置出现错误，指示设备是否应无法启动。 |
| IP6 | 如果你想使用 IPv6，则设置为 `yes`。 |
| NAME | 使用此设置设备名称。 |
| UUID | 由于设备名称会随硬件变化，可能会设置一个唯一 ID (`UUID`)。该 UUID 然后可以作为设备的唯一标识符。 |
| HWADDR | 指定要使用的 MAC 地址。如果你想使用与网卡配置的不同的 MAC 地址，应在这里进行更改。 |
| IPADDR | 定义在此接口上使用的 IP 地址。 |
| PREFIX | 此变量以 CIDR 格式定义子网掩码。CIDR 格式定义子网掩码的位数，而不是点进制数字，因此使用 24 代替 255.255.255.0。 |
| GATEWAY | 使用此设置用于网卡流量的网关。如果变量 `DEFROUTE` 也设置为 `yes`，此处指定的路由器也将作为默认路由。 |
| DNS1 | 此参数指定要使用的第一个 DNS 服务器 IP 地址。要使用额外的 DNS 服务器，请使用变量 `DNS2`，如果喜欢还可以使用 `DNS3`。 |
| USERCTL | 如果你想允许用户更改网络配置，则设置为 `yes`。这在服务器上通常不是一个好主意。 |

# 理解网络服务脚本

Red Hat Enterprise Linux 上的网络配置由 NetworkManager 服务管理。该服务不需要大量的管理，因为它是默认启用的。与你在 Linux 上可能使用的许多其他服务不同，它会自动获取配置的更改。虽然在更改配置后通常需要重启服务，但 NetworkManager 并非如此。

除了 NetworkManager 服务 (`/etc/init.d/NetworkManager`) 之外，还有一个网络服务 (`/etc/init.d/network`)。网络服务负责让你服务器上所有网卡能够正常工作。如果你停止了它，服务器上所有的网络连接都将停止。NetworkManager 服务用于管理网卡。停止 NetworkManager 服务不会停止网络连接；它停止的是 NetworkManager 程序，这意味着你需要退回到对服务器上的网络接口进行手动管理。

# 从命令行配置网络

在所有情况下，你的服务器都应该配置为自动启动网络接口。在许多情况下，如果你能手动为网卡创建配置，也是非常有用的。当你遇到问题并想在将配置写入配置文件之前测试特定配置是否有效时，这尤为有用。

用于手动网络配置和监控的经典工具是 `ifconfig`。该命令提供了所有网卡当前配置的概览，包括一些使用统计数据，显示网卡自激活以来处理了多少流量。列表 6.4 显示了 `ifconfig` 的典型输出。

### 列表 6.4：ifconfig 输出

```
[root@localhost ~]# ifconfig

lo Link encap:Local Loopback

    inet addr:127.0.0.1 Mask:255.0.0.0

    inet6 addr ::/128 Scope:Host

    UP LOOPBACK RUNNING MTU:16436 Metric:1

    RX packets:212 errors:0 dropped:0 overflows:0 frame:0

    TX packets:212 errors:0 dropped:0 overflows:0 carrier:0 collisions:0 txqueuelen:0

    RX bytes:16246 (15.8 KIB) TX bytes:16246 (15.8 KIB)

eth0 Link encap:Ethernet Hwaddr B8:AC:6F:C9:35:25
inet addr:192.168.0.70 Bcast:192.168.0.255 Mask:255.255.255.0
inet6 addr fe80::baac:6fff:fec9:3525/64 Scope:Link
UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
RX packets:4600 errors:0 overflows:0 frame:0
TX packets:3400 errors:0 overflows:0 carrier:0
collisions:0 txqueuelen:1000
RX bytes:45415 (443.4 KIB) TX bytes:40018 (39.0 KIB)
Interrupt:18

wlan0 Link encap:ethernet Hwaddr A0:88:B4:20:CE:24
UP MULTICAST MTU:1500 Metric:1
RX packets:0 errors:0 overflows:0 frame:0
TX packets:0 errors:0 overflows:0 carrier:0
collisions:0 txqueuelen:1000
RX bytes:0 (0.0) TX bytes:0 (0.0)
```

即使 `ifconfig` 的输出易于阅读，在像 Red Hat Linux 这样的现代 Linux 发行版上，你不应该再使用 `ifconfig` 了。大约 10 年来，`ip` 工具一直是手动网络配置和监控的默认工具。练习 6.2 向你展示了如何使用该工具，以及为什么你不应该再使用 `ifconfig`。

# 练习 6.2

## 使用 ip 配置网络接口

在本次练习中，你将使用 `ip` 工具为网卡添加 IP 地址。如果你在服务器上运行多个服务，并希望为这些服务中的每个服务提供唯一的 IP 地址，那么使用辅助 IP 地址是有益的。你将用 `ifconfig` 检查网络配置，并发现辅助 IP 地址是不可见的。你将使用 `ip` 工具显示当前的网络配置。你将看到该工具显示了你刚刚添加的辅助 IP 地址。

- 1. 打开终端，确保你拥有 root 权限。
- 2. 使用命令 `ip addr show` 显示当前的 IP 地址配置（参见列表 6.5）。找到网卡的名称。

### 列表 6.5：使用 ip addr show 显示当前网络配置

```
[root@hn1]# ip addr show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 16436 qdisc noqueue state UNKNOWN
link/loopback 00:00:00.00:00:00:00 brd 00:00:00.00:00:00:00
inet 127.0.0.1/8 scope host
inet6 ::1/128 scope host
valid_left preferred_left forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state up len 1000
link/ether b8:ac:6f:c9:35:25 brd ff:ff:ff:ff:ff
inet 192.168.0.70/24 brd 192.168.0.255 scope global
inet6 fe80::baac:6fff:fec9:3525/64 scope link
valid_left preferred_left forever
3: wlan0: <NOCARRIER,BROADCAST,MULTICAST,LOWER_UP> mtu 1500 qdisc noqueue state DOWN len 0
link/ether a0:88:b4:20:ce:24 brd ff:ff:ff:ff:ff
```

- 3. 如列表 6.5 所示，网卡是 `eth0`。知道这一点后，现在可以使用命令 `ip add dev eth0` 为此网卡添加 IP 地址。
- 4. 现在使用命令 `ping 192.168.0.72` 来检查你添加的 IP 地址的可用性。你应该看到 echo 回复。
- 5. 使用 `ipconfig` 显示当前配置。你将看到刚刚添加的辅助 IP 地址。
- 6. 使用 `ip addr` 显示当前的网络配置。这将显示你。
