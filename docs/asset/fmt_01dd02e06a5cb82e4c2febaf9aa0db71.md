
该文件中有两个需要注意的重要元素。第一个是 `DEVICE` 选项，它指定了你正在工作的接口。这里指定了第一个接口，通过查看下一行，你可以看到使用的协议。此接口使用 DHCP 协议，这意味着 IP 地址是从网络上的 DHCP 服务器租得的（在启动期间自动获取）。假设你想将其更改为静态 IP 地址呢？你可以手动编辑此文件，但对于基础配置，有一种更快的方法。

# 考试提示

如果你手动编辑网络接口文件，你有更多可用选项可以使用。你可以自定义想要使用的选项；但是，自定义这些选项需要时间，而且 Red Hat 考试并不是要求的。

# 静态 IP 地址

配置网络接口的快速方法是使用 `system-config-network-tui` 命令。它启动一个菜单驱动界面，允许你动态配置接口。让我们使用此工具将第二个接口 `eth1` 设置为静态 IP 地址。

- 步骤 1. 启动工具：
```
# system-config-network-tui
```

- 步骤 2. 选择想要编辑的网络接口（参见图 5-1）。

**图 5-1** 需要编辑的网络接口。

- 步骤 3. 编辑接口的详情（参见图 5-2）。

- 步骤 4. 完成后保存并退出。

在这里，你可以对接口进行任何需要的更改，包括将其更改为静态 IP 地址而不是使用 DHCP 协议。现在你已经更改了网络接口，你需要重启网络服务使更改生效。与其通过重启网络服务来关闭系统上的所有接口，不如你只需要关闭你所更改的单个接口。因为你只对 `eth1` 进行了更改，所以你只需要关闭这一个接口。要做到这一点，你使用 `ifdown` 和 `ifup` 命令。这两个命令实际上是 `ifconfig` 命令的简写格式。

**图 5-2** 接口详情可以编辑。

- 步骤 1. 要关闭单个接口，使用 `ifdown`：
```
# ifdown eth1
```

- 步骤 2. 要恢复你刚刚关闭的接口，使用 `ifup`：
```
# ifup eth1
```

如果接口是静态的，不应该有输出。如果接口配置为使用 DHCP，你只会看到一行，你知道该接口正在从 DHCP 服务器获取必要信息。使用 `ifconfig` 命令可以确保你的工作是正确的。

语法：`ifconfig [options] [interface]`

- 选项：
- `netmask`: 指定接口的子网掩码。
- `hw`: 设置 MAC 地址。
- `up`: 启用接口。
- `down`: 关闭接口。

要查看 `eth0` 的当前 IP 地址，使用以下命令：

```
# ifconfig eth0

Link encap:Ethernet Haddr 08:00:27:30:74:AA

inet addr:172.168.1.1 Broadcast:172.168.1.255 Mask:255.255.255

inet6 addr:fe80::a00:27ff:30:7aa/64 Scope:Link

UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1

RX packets:2140 errors:1 dropped:0 overflows:0 frame:0

TX packets:7085 errors:0 dropped:0 overflows:0

collisions:0
```

现在你已经验证 IP 地址是正确的，你应该查看系统中其他接口的 IP 地址。不带参数使用 `ifconfig` 命令显示所有接口及其当前详情。

```
# cat /etc/sysconfig/network-scripts/ifcfg-eth1

DEVICE=eth1

BOOTPROTO=none

HWADDR=08:00:27:DB:D0:F5

ONBOOT=yes

IPADDR=172.168.1.1

NETMASK=255.255.255

TYPE=Ethernet
```

```
# ifconfig

eth0

Link encap:Ethernet Haddr 08:00:27:30:74:AA

inet addr:172.168.1.1 Broadcast:172.168.1.255 Mask:255.255.255

inet6 addr:fe80::a00:27ff:30:7aa/64 Scope:Link

UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1

RX packets:2140 errors:1 dropped:0 overflows:0 frame:0

TX packets:7085 errors:0 dropped:0 overflows:0

collisions:0

eth1

Link encap:Ethernet Haddr 08:00:27:DB:D0:F5

inet addr:172.168.1.1 Broadcast:172.168.1.255 Mask:255.255.255

inet6 addr:fe80::a00:27ff:edb:0f5/64 Scope:Link

UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1

RX packets:0 errors:0 dropped:0 overflows:0 frame:0

TX packets:243 errors:0 dropped:0 overflows:0

collisions:0
```

# Red Hat® 考试实战指南：RHCSA™ 和 RHCE® 指南与实验手册

```
inet addr:127.0.0.1  Mask:255.0.0.0

inet6 addr ::1/128  Scope:Host

UP LOOPBACK errors:0 dropped:0 MTU:16436 Metric:1

RX packets:2735 errors:0 dropped:0 overflows:0 frame:0

TX packets:2735 errors:0 dropped:0 overflows:0 carrier:0

collisions:0 txqueue:0

RX bytes:4258081 (4.0 MiB)  TX bytes:4258081 (4.0 MiB)
```

在这里，你可以看到三个接口：`eth0`；`eth1` 以及环回适配器（loopback adapter）。每当你对接口设置进行更改时，都需要先关闭该接口，然后重新启动它。如果编辑了多个接口，也可以重启整个网络服务。

> 警告：重启网络服务会中断所有网络连接以及任何当前连接的客户端。

按照以下方式重启网络服务：

```
# service network restart

Shutting down interface eth0:      [ OK ]

Shutting down interface eth1:      [ OK ]

Shutting down loopback interface:  [ OK ]

Bringing up loopback interface:     [ OK ]

Bringing up interface eth0:

Determining IP information for eth0... done.  [ OK ]

Bringing up interface eth1:          [ OK ]
```

从此输出中你可以判断 `eth0` 配置为使用 DHCP 协议，因为它必须确定自己的 IP 地址。

还有另一种方法可以设置 IP 地址。`ifconfig` 命令除了显示网络接口信息外，还可以设置 IP 地址。假设你想将 `eth1` 接口的 IP 地址设置为静态地址。因为你希望 IP 地址保持不变，只需使用 `ifconfig` 命令设置静态 IP 地址即可：

```
# ifconfig eth0 172.168.1.1 netmask 255.255.255.0
```

此命令获得的结果与使用菜单式选项相同。不要忘记先关闭网络再重新启动（重启网络服务）。请确保你始终使用 `ifconfig` 命令来验证你的 IP 地址已正确设置。

**警告：** 对于 Linux 许多命令和更改，有多种方法可以实现相同的结果。请确保选择你最熟悉的方法，以便在考试中节省时间。

# 路由

当你的系统有两个或多个网络接口（例如 RHEL01 主机）时，它们被称为双宿主（dual-homed）或多宿主（multibomed）系统。你需要确保每个接口都有可以通过路由的网关。使用 `route` 命令，你可以显示系统当前的路由，并在需要时添加额外的路由。

语法：`route [options]`

选项：

| 命令 | 说明 |
| :--- | :--- |
| add | 添加网络路由 |
| del | 删除现有路由 |
| flush | 清除任何临时路由 |

**警告：** 作为一个良好的故障排除提示，请注意用于检测网关或路由问题的关键词。如果你收到关于无法连接主机或特定域名的错误消息，应该始终检查默认网关是否设置正确。

让我们查看系统上的当前路由：

```
# route

Kernel IP routing table

Destination    Gateway         Genmask         Flags Ref Use Iface

192.168.1.0     *               255.255.255.0  U      0 0 0 eth0

172.168.1.0     *               255.255.255.0  U      0 0 0 eth1

169.254.0       *               255.255.255.0  U      0 0 0 eth1

default         192.168.1.1     0.0.0.0         UG     0 0 0 eth0
```

前面的输出显示，主路由实际上是该系统的默认网关（如果需要进一步说明，请参考引言中的布局）。如果你没有设置默认网关，可以使用 `route` 命令选择默认网关。

- 步骤 1. 假设默认网关尚未设置，你可以使用以下命令为 RHEL01 主机设置：
```
# route add default gw 192.168.1.1 eth0
```

- 步骤 2. 你现在可以通过再次调用 `route` 命令来验证你添加的新默认网关：

```
# route

Kernel IP routing table

Destination      Gateway         Genmask Flags Metric Ref Use Interface

192.168.1.0     *               255.255.255.0  U       0  eth0

192.168.1.0                     255.255.255.0  U       0  eth1

169.254.0.0     *               255.255.0.0   U       0  eth1

default         192.168.1.1     0.0.0.0         UG     0  eth0
```

前面的输出显示，主路由实际上是该系统的默认网关（如果需要进一步说明，请参考引言中的布局）。如果你没有设置默认网关，可以使用 `route` 命令选择默认网关。

# Red Hat® 考试实战指南：RHCSA™ 和 RHCE® 指南与实验手册

# 创建静态路由

在某些时刻你可能需要创建静态路由。要创建静态路由，需要在 `/etc/sysconfig/network` 文件中添加条目。看看它可能是什么样子：

```
# ping -c 2 172.168.1.1

PING 172.168.1.1 (172.168.1.1) 56(84) bytes of data.

64 bytes from 172.168.1.1: icmp_seq=1 ttl=64 time=0.055 ms

64 bytes from 172.168.1.1: icmp_seq=2 ttl=64 time=0.074 ms
```

# 故障排除：网络连接

可以使用几个命令来排除网络问题：

- `ping`：测试主机之间的连接。
- `traceroute`：显示数据包到达目的地的路径。
- `netstat`：显示网络连接、路由表和接口统计。

让我们从 `ping` 命令开始，可以用它测试主机之间的连接。

语法：`ping [options] destination`

当你 ping 某个目标时，与 Windows 不同，Linux 会持续直到你取消。你可以通过前缀 `-c` 来限制请求数量。

- 步骤 1. 在 RHEL01 上，验证你可以看到 RHEL02：

```
# ping -c 2 172.168.1.2

PING 172.168.1.2 (172.168.1.2) 56(84) bytes of data.

64 bytes from 172.168.1.2: icmp_seq=1 ttl=64 time=0.055 ms

64 bytes from 172.168.1.2: icmp_seq=2 ttl=64 time=0.074 ms
```

网络世界中的通信是双向的，所以你还需要确保 RHEL02 可以访问 RHEL01。

- 步骤 1. 在 RHEL02 上，使用以下命令：

```
# ping -c 2 172.168.1.1

PING 172.168.1.1 (172.168.1.1) 56(84) bytes of data.

64 bytes from 172.168.1.1: icmp_seq=1 ttl=64 time=0.055 ms

64 bytes from 172.168.1.1: icmp_seq=2 ttl=64 time=0.074 ms
```

- 步骤 2. 现在你已经可以在外部网络上看到路由器了：

```
# ping -c 2 172.168.1.1

PING 172.168.1.1 (172.168.1.1) 56(84) bytes of data.

64 bytes from 172.168.1.1: icmp_seq=1 ttl=64 time=0.055 ms

64 bytes from 172.168.1.1: icmp_seq=2 ttl=64 time=0.074 ms
```

# 红帽®考试实操指南：RHCSA™ 和 RHCE® 指南与实验手册

第 2 。在 RHEL02 上，使用以下命令：

```
# ping -c 2 192.168.1.1

PING 192.168.1.1 (192.168.1.1) 56(84) bytes of data.

From 172.168.1.1 icmp_seq=2 Destination Unreachable

From 172.168.1.1 icmp_seq=3 Destination Unreachable
```

在这里，无法无法 192.168.1.0 网络，系统通过“Destination Unreachable”（目标主机不可达）消息告知了你。收到此消息的原因是从 RHEL02 到 192.168.1.0 网络没有路由。哪些可用路由？让我们查看 `route` 命令来查找。

在 RHEL02 上，使用 `route` 命令查看可用网络：

```bash
# route
```

内核 IP 路由表

| Destination | Gateway | Genmask | Flags | Metric | Ref | Use | Iface |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 172.168.1.0 | * | 255.255.255.0 | U | 0 | 0 | eth0 |
| 169.254.0.0 | * | 255.255.255.0 | U | 0 | 0 | eth0 |

你可以看到只能到达 172.168.1.0，这解释了为什么你无法到达 192.168.1.0 网络。

现在你已经知道如何检查接口和路由，还应该查看如何使用 `netstat` 命令查看监听或已建立的端口。你也可以使用 `netstat` 命令获取有关路由表、监听套接和已建立连接的信息。

语法：`netstat [options]`

选项：

- `-r` 显示路由表
- `-i` 显示接口统计数据
- `-t` 显示 tcp 连接
- `-u` 显示 udp 连接
- `-a` 显示所有套接字（tcp、udp 或本地）
- `-p` 显示进程 ID
- `-e` 显示扩展信息

例如，假设你想检查 SSH 服务器是否正确地在端口 22 上进行监听。你可以使用 `netstat` 检查该连接对你的客户端来说是否是可用的：

```bash
# netstat -tupe | grep ssh
```

```
tcp      0      *:ssh   *:      LISTEN root     8627
2674/sshd
```
