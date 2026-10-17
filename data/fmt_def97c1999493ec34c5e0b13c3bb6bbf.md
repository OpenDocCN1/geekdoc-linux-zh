
为了管理，IP 地址被分为若干类。IP 地址的类别定义了使用该地址的设备的默认子网掩码。所有的 IP 地址类都通过地址的第一个字节来识别，如表 14-1 所示。

表 14-1 IP 地址类

| 类别 | 子网掩码 | 第一个字节 | 最大网络数 | 最大主机数 | 示例 IP 地址 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| A | 255.0.0.0 | 1–127 | 127 | 16,777,214 | 3.4.1.99 |
| B | 255.255.0.0 | 128–191 | 16,384 | 65,534 | 144.129.188.1 |
| C | 255.255.255.0 | 192–223 | 2,097,152 | 254 | 192.168.1.1 |
| D | N/A | 224–239 | N/A | N/A | 224.0.2.1 |
| E | N/A | 240–255 | N/A | N/A | N/A |

A 类使用 8 位作为网络 ID，使用 24 位作为主机 ID。你可以从 `255.0.0.0` 的子网掩码识别出这一点。第一个字节的值范围在 1 到 127 之间。整个互联网只有 127 个潜在的 A 类网络可用。A 类网络分配给非常大的公司和互联网服务提供商。

B 类使用 16 位作为网络 ID，使用 16 位作为主机 ID。`255.255.0.0` 的子网掩码定义了这一点。第一个字节的值范围从 128 到 191 等。共有 16,384 个 B 类网络，每个网络有 65,534 个主机。B 类网络分配给较大的组织，例如政府、大学和拥有数千用户的公司。

C 类使用 24 位作为网络 ID，使用 8 位作为主机 ID。这是由子网掩码 `255.255.255.0` 定义的。第一个字节的值范围从 192 到 223 等。共有 2,097,152 个 C 类网络，每个网络有 254 个主机。虽然 C 类网络非常多，但它们的主机数量较少，因此适用于较小的组织。

D 类地址不分为网络，不能分配给计算机作为 IP 地址；相反，D 类地址用于组播（multicast）。组播地址传递给组播组中的每台计算机。这比广播消息更好，因为路由器可以配置为允许组播流量从一个网络移动到另一个网络。此外，网络上的所有计算机都会接收组播（注：原文逻辑略有混乱，此处意为组播组内成员接收）。

E 类地址未划分网络（注：原文在此处出现大量逻辑重复和断层，E 类通常用于实验目的）。

*注：由于提供的原文存在多处逻辑混乱、重复以及句子断裂的情况（特别是从 D 类开始之后），以下译文在保持原文结构的基础上，尽可能确保术语对齐，但无法修复原文本身的逻辑错误。*

（由于原文从 D 类之后开始出现大量重复且无意义的句子组合，根据指令“不要漏掉任何一行”且“不要重复输出原文”，译文将严格遵循原文的行数进行翻译，但原文内容本身存在严重的重复和错误。）

（注：由于原始文本后半部分存在严重的逻辑重复、乱码和句子断裂，此处译文保留了原文的结构，但内容反映了原文的质量问题。）

# 配置 NIC 接口

同样地，为了为 DEC Tulip 类型的第二个 NIC 加载驱动模块，你可以将配置行放置在 `/etc/modules.config` 中：

```
alias eth1 tulip
```

在 NIC 的驱动模块加载到 Linux 内核后，你就可以配置它使用 TCP/IP 了。可以使用 `ifconfig` 命令来为 NIC 分配 TCP/IP 配置，并查看计算机中所有网络接口的配置。要为 `eth0` 分配 IP 地址 3.4.5.6、子网掩码 255.0.0.0 和广播地址 3.255.255.255，你可以在命令行提示符下使用以下命令：

```
ifconfig eth0 3.4.5.6 netmask 255.0.0.0 broadcast 3.255.255.255
```

或者，你也可以从网络上的动态主机配置协议（DHCP）或启动协议（BOOT）服务器接收 TCP/IP 配置。要从服务器为第一个以太网适配器获取并配置 TCP/IP 信息，你可以在命令行提示符下使用 `dhclient eth0`。

要查看所有接口的配置，你可以不带任何参数使用 `ifconfig` 命令，如下如下输出所示：

```
[root@server1]# ifconfig
eth0 link:Ethernet Haddr 00:80:C6:F9:1B:8C
inet addr:3.4.5.6 Bcast:255.255.255 Mask:255.0.0.0
inet6 addr:fe80::280:cff:fef9:18bc/64 Scope:Link
UP BROAD RUNNING MULTICAST MTU:1500 Metric:1
RX packets:47 errors:0 dropped:0 overruns:0 frame:0
TX packets:13 errors:5 dropped:0 overruns:0 carrier:5
collisions:0 txqueuelen:1000
RX bytes:5560 (5.4 Kb) TX bytes:770 (770.0 b)
Interrupt:10 Address:0x08000
```

```
lo
link:Local Loopback
inet6 addr::1/128 Scope:Host
UP RUNNING MTU:16436 Metric:1
RX packets:3142 errors:0 dropped:0 overruns:0 frame:0
TX packets:3142 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:0
RX bytes:3443414 (3.2 Mb) TX bytes:3443414 (3.2 Mb)
```

```
[root@server1]#
```

`ifconfig` 命令的输出还显示了接口统计以及 IP 地址为127.0.0.1 的特殊环回适配器（lo）；此 IP 地址代表本地计算机，并注册在所有使用 TCP/IP 的计算机上。

> `netstat -i` 也可以用于显示接口统计信息。

![](img/d1e8c01c294d2086b6ec91cf5c9982c5_632_0.png)

# 第 14 章 网络配置

如果你重启计算机，`eth0` 的 TCP/IP 信息将会丢失。要允许系统在每次启动时激活并配置接口的 TCP/IP 信息，只需在 `/etc/sysconfig/network-scripts/ifcfg-interface` 文件中条目，其中 `interface` 是网络接口的名称。第一个以太网接口（`eth0`）的配置文件示例如下输出所示：

```
[server1 root]# cat /etc/sysconfig/network-scripts/ifcfg-eth0
DEVICE=eth0
BOOTPROTO=none
HWADDR=00:80:C6:F9:1B:8C
IPADDR=3.4.5.6
NETMASK=255.255.0.0
GATEWAY=3.0.0.1
ONBOOT=yes
IPV6INIT=none
```

上述输出中的条目表明，第一个以太网适配器（`eth0`）的 TCP/IP 配置将在启动时激活（`ONBOOT=yes`）。该 NIC 不从 DHCP 或 BOOTP 获取信息（`BOOTPROTO=none`）；它使用 IP 地址 3.4.5.6、子网掩码 255.0.0.0 和默认网关 3.0.0.1 进行配置。此处无法使用广播地址，因为系统可以根据子网掩码轻松计算出来。此外，你也可以将 `BOOTPROTO=none` 行改为 `dhcp` 或 `BOOTPROTO=bootstrap`，以从网络上的 DHCP 或 BOOTP 服务器获取所有的 TCP/IP 信息。

> `/etc/sysconfig/network-scripts/ifcfg-eth0` 还可以包含有关其他网络协议（如 IPX/SPX）配置的信息。

![](img/d1e8c01c294d2086b6ec91cf5c9982c5_633_0.png)

编辑 `/etc/sysconfig/network-scripts/ifcfg-eth0` 文件后，不需要重启系统即可使新的 TCP/IP 配置生效；只需运行 `ifdown eth0` 命令取消配置 `eth0` 接口，运行 `ifup eth0` 命令使用 `/etc/sysconfig/network-scripts/ifcfg-eth0` 中的设置配置 `eth0`。在 NIC 配置好 TCP/IP 后，应该使用 `ping` 测试配置。默认情况下，`ping` 命令向另一个 IP 地址发送小数据包，直到按下 Ctrl+c；使用 `ping` 命令的 `-c` 选项如下所示：

```
[server1 root]# ping -c 5 127.0.0.1
127.0.0.1 (127.0.0.1) 56 (84) bytes of data.
64 bytes from 127.0.0.1 icmp_seq=0 ttl=64 time=0.154 ms
64 bytes from 127.0.0.1 icmp_seq=1 ttl=64 time=0.109 ms
64 bytes from 127.0.0.1 icmp_seq=2 ttl=64 time=0.110 ms
64 bytes from 127.0.0.1 icmp_seq=3 ttl=64 time=0.119 ms
64 bytes from 127.0.0.1 icmp_seq=4 ttl=64 time=0.111 ms
127.0.0.1 ping statistics
5 packets transmitted, 5 received, 0% packet loss, time 399ms
rtt min/avg/max/mdev = 0.109/0.120/0.154/0.020 ms, pipe 2
[root@server1]#
```

![](img/d1e8c01c294d2086b6ec91cf5c9982c5_634_0.png)

如果 `ping` 命令没有从环回接口接收任何响应，说明 TCP/IP 本身有问题。

此外，要向之前配置的 IP 地址发送五个 `ping` 请求，可以使用以下命令：

```
[root@server1]# ping -c 5 3.4.5.6
3.4.5.6 (3.4.5.6) 56 (84) bytes of data.
64 bytes from 3.4.5.6 icmp_seq=0 ttl=64 time=0.157 ms
64 bytes from 3.4.5.6 icmp_seq=1 ttl=64 time=0.113 ms
64 bytes from 3.4.5.6 icmp_seq=2 ttl=64 time=0.106 ms
64 bytes from 3.4.5.6 icmp_seq=3 ttl=64 time=0.107 ms
64 bytes from 3.4.5.6 icmp_seq=4 ttl=64 time=0.115 ms
3.4.5.6 ping statistics
5 packets transmitted, 5 received, 0% packet loss, time 4000ms
rtt min/avg/max/mdev = 0.106/0.119/0.157/0.022 ms, pipe 2
[root@server1]#
```

> 如果 `ping` 命令没有从新配置的地址接收任何响应，说明 NIC 的 TCP/IP 配置有问题。

接下来，你需要测试 Linux 计算机是否可以 `ping` 同网络上的计算机；使用以下命令向配置 IP 地址 3.0.0.2 的计算机发送五个 `ping` 请求：

```
[root@server1]# ping -c 5 3.0.0.2
3.0.0.2 (3.0.0.2) 56 (84) bytes of data.
64 bytes from 3.0.0.2 icmp_seq=0 ttl=128 time=0.448 ms
64 bytes from 3.0.0.2 icmp_seq=1 ttl=128 time=0.401 ms
64 bytes from 3.0.0.2 icmp_seq=2 ttl=128 time=0.403 ms
64 bytes from 3.0.0.2 icmp_seq=3 ttl=128 time=0.419 ms
64 bytes from 3.0.0.2 icmp_seq=4 ttl=128 time=0.439 ms
3.0.0.2 ping statistics
5 packets transmitted, 5 received, 0% packet loss, time 4001ms
rtt min/avg/max/mdev = 0.401/0.422/0.448/0.018 ms, pipe 2
[root]@server1]# _
```

如果 `ping` 命令没有从其他计算机或网络上接收任何响应，说明网络介质有问题。

也可以在桌面环境中配置 NIC 接口，如图 14-2 所示。只需导航到 Red Hat、系统设置、网络。

![](img/d1e8c01c294d2086b6ec91cf5c9982c5_635_0.png)

**图 14-2** 配置网络接口

集成服务数字网络（ISDN）最初旨在取代普通电话线，并允许以 128KB/s 的传输数据。ISDN 使用 ISDN 调制解调器连接到与普通电话线不同的介质。尽管 ISDN 在欧洲很流行，但在北美并不普及。与其他许多设备一样，ISDN 调制解调器通常由 `kudzu` 或在安装期间进行检测和配置。

北美最流行的连接技术之一是 DSL。DSL 有许多变体，例如异步 DSL（ADSL），它是北美家庭中最常用的 DSL；以及高比特 DSL（HDSL），它在商业环境中很常见；为了简单起见，所有 DSL 变体统称为 xDSL。使用以太网卡（NIC）通过 TCP/IP 和 PPP 连接到 DSL 调制解调器；DSL 调制解调器通过普通电话线传输信息，速度可以超过 8MB/s。由于 DSL 调制解调器通过某种介质自动连接到 NIC，因此它们通常不在安装期间或通过 `kudzu` 程序进行配置；而是手动进行配置。

配置 PPP 连接需要内核中编译了 PPP 或作为模块可用（`pppd`），以及一系列支持程序，例如用于与调制解调器通信的 `chat` 程序。过去的 PPP 配置非常繁琐；你需要创建一个包含建立 PPP 连接所需的必要信息（用户名、密码等）的 `chat` 脚本，一个包含 PPP 守护进程所用设备参数的连接脚本，以及一个像 `minicom` 这样的用于启动网络通信的程序脚本。TCP/IP 配置通常由你连接的互联网服务提供商（ISP）分配，在过程中很少需要手动配置。

今天，各种图形化程序可以配置必要的文件并启动必要的实用程序以允许 PPP 网络通信。在 Red Fedora Linux 中，你只需导航到如图 14–2 所示的 Red Hat 按钮、系统设置、网络，然后点击“新建”（New）按钮并指定要添加的设备类型，如图 14–4 所示。

如果你从图 14–4 选择配置调制解调器连接或 ISDN 连接，系统会提示输入图 14-5 和图 14–6 所示的设备信息。

无论你是为调制解调器还是 ISDN 连接配置硬件，随后都会提示输入 ISP 和 TCP/IP 信息，如图 14-7 和图 14-8 所示。

或者，如果你从图 14–4 选择设置 xDSL 连接，系统会提示选择连接到 DSL 调制解调器的以太网接口以及 ISP 信息，如本章后面的图 14-9 所示。

## 配置 PPP 接口

![](img/d1e8c01c294d2086b6ec91cf5c9982c5_638_0.png)

**图 14-4** 添加网络接口

![](img/d1e8c01c294d2086b6ec91cf5c9982c5_638_1.png)

**图 14-5** 选择调制解调器硬件

类似于配置 NIC，关于每个 PPP 设备的信息存储在 `/etc/sysconfig/network-scripts` 目录下名为 `ifcfg-InternetServiceProviderName` 的文件中。例如，之前为 xDSL 连接配置的信息存储在 `/etc/sysconfig/network-scripts/ifcfg-isp` 中，如下所示所示：

```
[root@server1 root]# cat /etc/sysconfig/network-scripts/ifcfg-isp
# Please read /usr/share/doc/inits-scripts-*/sysconfig.txt
# for the documentation of these parameters.
IPV6INIT=no
ONBOOT=no
USERCTL=yes
PEERDNS=yes
TYPE=xDSL
DEVICE=pppp0
BOOTPROTO=dialup
PIDFILE=/var/run/pppoe-adsl.pid
FIREWALL=NONE
PING=
PPOE_TIMEOUT=80
LCP_FAILURE=3
LCP_INTERVAL=20
CLAMPMSS=1412
CONNECT_POLL=6
CONNECT_TIMEOUT=60
PERSIST=no
SYNCHRONOUS=no
DFROUTED=yes
USER=user1
ETH=eth0
PROVIDER=isp
DEMAND=no
[root@server1 root]#
```
