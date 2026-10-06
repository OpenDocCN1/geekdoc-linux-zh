
`valid/25581sec preferred_inet/25581sec`

`inet6 fe80::bc3:3db0:591/64 scope link noprefix`

`valid valid preferred_inet forever`

`[server1 ~]#`

```
```

之前的输出显示 `eth` 网络接口具有 IPv4 地址 `3.4.5.6` 和 IPv6 地址 `fe80::bc3:3db0:591/64`，系统可以自动配置，因为特殊的环回适配器 `lo` 自动配置了 IPv4 地址 `127.0.0.1` 和 IPv6 地址 `::1`；这些地址代表本地计算机，是所有计算机所需要的。`ip` 命令还会显示每个网络接口的接收 `RX` 和发送 `TX` 统计数据。

> 注意 17
> 你可以使用 `netstat` 命令的 `-i` 选项来显示接口统计信息。

如果你重启计算机，为 `eth` 配置的 IP 信息将丢失。为了允许系统在启动时激活并配置接口的 IP 信息，你可以将条目放在配置文件中，网络守护程序会在激活网络时读取该文件。在 Ubuntu 系统上，你可以向 `/etc/network/interfaces` 添加 `eth0` 的条目；在 Fedora 系统上，你可以向 `/etc/sysconfig/network-scripts/ifcfg-eth0` 添加条目。之后，你可以运行 `ifconfig eth0 down` 或 `ifconfig eth0 up` 或 `ifdown` 或 `ifconfig link set eth0 down set up` 来在不编辑这些文件行的情况下停用和重新激活你的 IP 配置。在现代系统中，IP 配置通常在初始化期间由网络渲染服务（如 `NetworkManager` 或 `Systemd-network`）完成。在 Ubuntu 系统上，你可以向 `/etc/network/interfaces` 添加 `eth0` 的条目；在 Fedora 系统上，你可以向 `/etc/sysconfig/network-scripts/ifcfg-eth0` 添加条目。

# 图 12-2 GNOME 设置中的网络接口配置

![](img/12ad6df66c6622b4ab7acf53dfd7f646_509_0.png)

大多数面向工作站的 Linux 发行版使用 `NetworkManager` 作为网络渲染器。`NetworkManager` 设计用于跟踪便携式工作站可能随时连接的许多有线和无线网络，并支持所有允许使用图形工具在不同网络之间切换的桌面环境。如果你的系统正在运行 `NetworkManager`，你可以可以使用不带参数的 `nmcli` 命令来查找每个网络接口的信息，包括以下输出中的活动连接：

```
[root@server1]# nmcli

wlan0: connected to CLASSWIFI

"Qualcomm Atheros AR93x Wireless Network Adapter (Killer Wireless-N 1 Half-size Mini PCIe Card [AR9380])"

wifi (ath9k), B8:C6:3F:F9:F4, hw, mtu 1500

ip4 default

inet4 192.168.1.101/24

route4 0.0.0.0/0

routes 192.168.1.0/24

inet6 fe80::3157:d86d:5da1:2292/64

route fe80::

route fe80::

route fe80:

eth0: unavailable

"Qualcomm Atheros AR8151 v2.0 Gigabit Ethernet"

ethernet (atlc), B8:CA:3A:D5:61:A9, hw, mtu 1500

lo: unmanaged

"10"

loopback (unknown), 00:00:00.00:00:00, sw, mtu 65536

DNS configuration:

servers: 192.168.1.1

interface: wlan0

使用 "nmcli show" 获取有关已知设备的完整信息，使用 "nmcli connection show" 获取连接配置文件的概览。

参考 nmcli (1) 和 nmcli-examples(5) 手册以获取完整用法。

[root@server1]#
```

在在上例中，以太网接口 `wlan0` 连接到名为 `CLASSWIFI` 的网络。在 Fedora 系统上，`NetworkManager` 将将网络配置和 Wi-Fi 连接存储在名为 `/etc/NetworkManager/system-connections/CLASSWIFI.connection` 的单独文件中，如果系统将来连接到该网络，可以使用该文件。如果你为网络手动配置 IP 地址（例如家庭或工作网络），每次当你连接到网络管理器时，之前配置的 IP 地址将自动从关联的配置文件应用。要查看 `NetworkManager` 过去连接过的所有 wifi 和无线网络列表，你可以运行如下输出所示的 `nmcli show` 命令：

```
[root@server ~]# nmcli show

NAME UUID TYPE DEVICE

CLASSWIFI 56e2a0c7-709a-7944-8621-ac44d-3572f08b0ed wifi wlan0

Starbucks 59e63b8e-e5d1-405c-b88f-82889b6b0bd wifi

McDonalds 0dc8c4378-e404-44b3-a77c-2ce25cc2f940 wifi

HomeWiFi 1966c022-8c55-422c-9cf9-1fd8dc4ef4e wifi

Wired f1b3fab43-b621-bdd0-d32c6e4a95 ethernet

[root@server ~]#
```

`Systemd` 也可以用来提供与 `NetworkManager` 相同的功能。你可以使用 `networkctl` 命令来查看和修改 `Systemd-network` 的配置；它会显示有关每个网络接口的信息，包括活动连接。以下输出表示 `eth0` 已经连接并由 `Systemd-networkd` 托管。

```
[root@server ~]# networkctl

IDX LINK OPERATIONAL SETUP

1 lo loopback unmanaged

2 eth0 ether routable configured

3 wlan0 ether no-carrier unmanaged
```

> **注意 19**：`NetworkManager` 和 `Systemd-network` 都是可选的。如果使用，任何时间只能有一个处于激活状态。

在配置网络使用 IP 后，你应该使用 `ping`（数据数据包发生器）命令来测试配置。`ping` 命令向另一个 IP 地址发送 ICMP 包并等待响应。默认情况下，`ping` 命令会持续发送包直到 TTL 过期；要测试环回接口，你使用 `ping` 命令的 `-c` 选项发送五个数据包，如下例所示：

```
[root@server ~]# ping -c 5 127.0.0.1

PING 127.0.0.1 (127.0.0.1) 56(64) bytes of data.

64 bytes from 127.0.0.1: icmp_seq=1 time=0.064 ms

64 bytes from 127.0.0.1: icmp_seq=2 time=0.069 ms

64 bytes from 127.0.0.1: icmp_seq=3 time=0.060 ms

64 bytes from 127.0.0.1: icmp_seq=4 time=0.059 ms

64 bytes from 127.0.0.1: icmp_seq=5 time=0.061 ms

--- 127.0.0.1 ping statistics

5 packets transmitted, 0% packet loss, time 299ms

rtt min/avg/max/mdev = 59/60/61/0.0
```

> **注意 20**：如果 `ping` 命令无法从环回接口接收任何响应，则 IP 本身有问题。接下来，你需要测试 Linux 命令是否可以 ping 同一网络上的其他计算机；可以使用以下命令向 IP 地址 `127.0.0.2` 发送五个请求：

```
[root@server ~]# ping -c 5 127.0.0.2
PING 127.0.0.2 (127.0.0.2) 56(64) bytes of data.
64 bytes from 127.0.0.2: icmp_seq=0 time=0.448 ms
64 bytes from 127.0.0.2: icmp_seq=1 time=0.401 ms
64 bytes from 127.0.0.2: icmp_seq=2 time=0.403 ms
64 bytes from 127.0.0.2: icmp_seq=3 time=0.419 ms
64 bytes from 127.0.0.2: icmp_seq=4 time=0.439 ms
--- 127.0.0.2 ping statistics
5 packets transmitted, 0% packet loss, time 4000ms
rtt min/avg/max/mdev = 401/422/448/18.0
```

> **注意 21**：如果 `ping` 无法接收网络上其他计算机的任何响应，则是网络有问题。你可以使用 `ping6` 命令向 IPv6 地址发送 ICMP 消息。

## 配置 PPP 接口

与其在网络接口上配置 IP 以获取网络访问，不如使用 PPP 协议在串口线（如电话线）上运行 IP。PPP 连接计算机到互联网或其他网络的三个常用技术：

- 调制解调器 `Modems`
- 集成业务网络 `ISDN`
- `DSL`

调制解调器 `modulator-demodulator` 使用 PPP 通过电话线发送 IP 信息；它们是 1990 年代用户获取互联网访问的最常用方法。与许多其他技术相比，调制解调器连接被认为是慢的；大多数只能以 56 Kb/s 的速度传输数据。由于调制解调器仅在串口上传输，系统通常会创建一个指向正确串口设备（如 COM1 的 `/dev/ttyS0`）的符号链接。

`ISDN` 是一组通过普通线路传输语音、视频和数据的标准。它允许以 128 Kb/s 的速度传输数据。`ISDN` 使用调制解调器通过线路连接到不同类型的网络。

现在 `ISDN` 和 `DSL` 很少；许多家庭网络使用 `DSL` 连接互联网。`DSL` 有许多变体，例如异步 `DSL` `ADSL`，它是北美家庭中最常用的，以及高比特 `DSL` `HDSL`，`DSL` 的变体被称为 `xDSL`。如果你使用 PPP 以太网 `PPPoE`，因此基于 `DSL` 的连接可以以高达 100 Mbps 的速度通过普通线路传输流量。

由于调制解调器、`ISDN` 和 `DSL` 连接需要特定于 ISP 的额外配置信息，它们通常在 Linux 安装期间不配置，必须手动配置。

配置 PPP 连接需要链接到内核或作为模块的 PPP 支持、PPP 守护进程 `pppd` 以及一系列辅助工具（例如用于与调制解调器通信的 `chat` 程序）。过去的 PPP 配置最多也是繁琐的；你需要创建一个包含建立 PPP 连接所需信息（名称、密码等）的脚本，一个包含 PPP 守护进程使用的设备参数的连接脚本，以及一个启动网络连接的程序。由于 IP 配置通常由你连接的 ISP 分配，因此在过程中很少配置。

现在调制解调器和 `ISDN` 连接相对少见。然而，现代 Linux 发行版没有自带配置工具。默认情况下，你可以下载 `Modem Manager` 工具。在 Fedora 系统上，你可以以 root 用户运行 `dnf install modem-manager-gui` 安装此包，并导航到活动 -> 显示应用程序 -> Modem Manager GUI 来启动图 12-3 所示的 Modem Manager。`Modem Manager` 会自动检测计算机中的任何调制解调器或 `ISDN` 硬件，并允许你配置 IP 配置，包括 ISP 账户名称和密码。

# 图 12-3 Modem Manager GUI

![](img/12ad6df66c6622b4ab7acf53dfd7f646_512_0.png)

`DSL` 连接现在非常常见。因此，几乎所有现代 Linux 发行版都包含一个可以配置你的网络接口与调制解调器工作的工具。在 Fedora Workstation 上，你可以在桌面环境的终端中使用 `nm-connection-editor` 命令配置 `DSL` 连接。该命令启动图 12-4 所示的图形化网络连接工具，它是 `NetworkManager` 的组件。如果你点击 `+` 按钮并选择设备类型 `DSL/PPPPoE`，网络连接工具将尝试检测你的 `DSL` 调调器并提示你提供 ISP 账户名称和密码。

# 图 12-4 网络连接工具

![](img/12ad6df66c6622b4ab7acf53dfd7f646_512_1.png)

# 注意 22

除了 `DSL` 之外，网络连接 `Network Connections` 工具还可以用于配置许多网络技术：

- 叠加网络 `Overlay networks`，包括虚拟专用网络 `VPN` 连接，它在现有的未加密 IP 网络之上提供加密的 IP 网络。专用技术（如 `Infiniband`）允许网络接口通过远程内存访问 `RDMA` 直接相互通信。绑定 `Bonding`，也称为聚合，利用两个连接到同一网络的网络接口来提供容错（在主/备用配置下）或网络流量的负载均衡，以实现更高的传输速率。
- 桥接 `Bridging`，即两个连接到不同网络的网络接口在网络之间提供无缝连接。

若要在具有桌面环境的系统上配置 `DSL` 连接，请使用带有适当选项的 `NetworkManager` `nmcli` 命令。如果没有安装 `NetworkManager`，可以执行 `pppoeconf` 命令，它将在终端内打开一个基础的图形界面并扫描 `DSL` 设备，如图 12-5 所示。如果发现 `DSL` 设备，系统将提示你输入 ISP 账户名和密码以完成配置。

# 图形 12-5 使用 pppoconf 扫描 DSL 设备

![](img/12ad6df66c6622b4ab7acf53dfd7f646_513_0.png)

在配置 PPP 调制解调器、`ISDN` 或 `DSL` 连接后，它通常会在启动时像系统上的其他网络接口一样激活。在 Fedora Workstation 上，你会在 `/etc/NetworkManager/system-connections/` 下注意到一个对应的 `*.nmconnection` 文件。在 Ubuntu 服务器上，`/etc/netplan/` 下还有一个额外的 YAML 配置文件。PPP 进程使用的其他配置存储在 `/etc/ppp` 中，连接 ISP 所需的密码也存储在那里，因为密码错误是 PPP 连接中最常见的问题。这些密码存储在两个文件中：`/etc/ppp/pap-secrets`（密码认证密钥）和 `/etc/ppp/chap-secrets`（握手认证协议密钥）。如果 ISP 能够及时接受网络上的密码，则会查询 `/etc/ppp/pap-secrets` 文件获取正确密码；但是，如果 ISP 需要一种安全的方法来验证用户身份，则会使用 `/etc/ppp/chap-secrets` 文件中的密码。当你配置连接时，这些信息会自动添加到两个文件中，如如下输出所示：

```
[root@server ~]# cat /etc/ppp/pap-secrets

# Secrets for authentication PAP

# client server addresses

```

# CompTIA Linux+ 和 LPIC-1：Linux 认证指南

```

###### system-config-network 将覆盖此部分!!! (begin) ####

"user1"

  "isp"

  "secret"

###### system-config-network 将覆盖此部分!!! (end) #####

[root@server1 ~1]# cat /etc/ppp/chap-secrets

# Secrets for authentication using CHAP

# client server secret IP addresses

###### system-config-network 将覆盖此部分!!! (begin) ####

"user1"

  "isp"

  "secret"

###### system-config-network 将覆盖此部分!!! (end) ######

[root@server1 ~1]#
```
