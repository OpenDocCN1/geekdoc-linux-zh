
| 参数 | 描述 |
| :--- | :--- |
| address | 显示或设置设备上的 IPv4 或 IPv6 地址。 |
| label | 定义配置标签。 |
| l2tp | 通过 IP 隧道传输以太网。 |
| link | 定义网络设备。 |
| madress | 定义系统要监听的多播地址。 |
| monitor | 监视 netlink 消息。 |
| mroute | 定义多播路由缓存中的条目。 |
| mrule | 定义多播路由策略数据库中的规则。 |
| neighbor | 管理 ARP 或 NDISC 缓存条目。 |
| netns | 管理网络命名空间。 |
| ntable | 管理邻居缓存操作。 |
| route | 管理路由表。 |
| rule | 管理路由策略数据库中的条目。 |
| tcprmetrics | 管理接口上的 TCP 指标。 |
| token | 管理分块接口标识符。 |
| tunnel | 通过 IP 隧道传输。 |
| tuntap | 管理 TUN/TAP 设备。 |
| xfrm | 管理安全连接的 IPsec 策略。 |

每个命令选项利用参数来定义要执行的操作，例如显示网络设置或修改现有网络设置：

```
$ ip address show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group
    default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
        valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
        valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast
    state UP group default qlen 1000
    link/ether 08:00:27:73:1c:6d brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global noprefixroute dynamic
        enp0s3
        valid_lft 84411sec preferred_lft 84411sec
    inet6 fe80::5432:edc0:51ea:fb44/64 scope link noprefixroute
        valid_lft forever preferred_lft forever
$
```

此示例显示 Linux 系统上的两个网络接口：

- `lo`：本地环回接口
- `enp0s3`：有线网络接口

本地环回接口是一种特殊的虚拟网络接口。任何本地程序都可以使用它与其他程序进行通信，就像它们在网络上一样。这简化了程序之间的数据传输。

`enp0s3` 网络接口是 Linux 系统的有线网络连接。`ip` 命令显示分配给接口的 IP 地址（同时分配了 IP 和 IPv6 链路本地地址）、子网掩码值以及关于接口上数据包的一些基本统计数据。

如果输出未显示分配给接口的网络地址，你可以使用 `ip` 命令指定接口的主机地址和子网掩码值：

```
# ip address add 10.0.2.15/24 dev enp0s3
```

然后使用 `ip` 命令设置网络接口的默认路由器：

```
# ip route add default via 192.168.1.254 dev enp0s3
```

最后，使用 `link` 选项激活网络接口：

```
# ip link set enp0s3 up
```

## IWCONFIG

在你可以使用 `ip` 命令为无线接口分配地址之前，必须使用 `iwconfig` 命令分配无线 SSID 和加密密钥值：

```
# iwconfig wlan0 essid "MyNetwork" key s:mypassword
```

`essid` 参数指定接入点 SSID 名称，`key` 参数指定连接该接入点所需的加密密钥。注意，加密密钥前带有 `s:`。这允许你使用 ASCII 文本字符指定加密密钥；否则你需要使用十六进制值指定密钥。

如果你不知道本地无线连接的名称，可以使用 `iwlist` 命令显示你的无线网卡检测到的所有无线信号。只需指定无线设备的名称，并使用 `scan` 选项：

```
$ iwlist wlan0 scan
```

## ROUTE

虽然 `ip` 命令是更改网络设置的一站式方法，但指定网络路由设置的另一种方式是 `route` 命令：

```
# route add default gw 192.168.1.254
```

你也可以单独使用 `route` 命令来查看系统当前配置的路由器。

```
$ route
Kernel IP routing table
Destination Gateway     Genmask         Flags Metric Ref Use Iface
default         192.168.1.254  0.0.0.0         UG    0      0     0     enp0s3
192.168.1.0     *              255.255.255.0  U       1      0     0     enp0s3
$
```

为 Linux 系统定义的默认路由器是 `192.168.1.254`，可通过 `enp0s3` 网络接口访问。输出还显示，要到达 `192.168.1.0` 网络不需要网关，因为那是 Linux 系统连接到的本地网络。

如果你的网络通过多个路由器连接到多个网络，你可以使用 `route` 命令的 `add` 或 `del` 命令行选项手动创建系统中的路由表。其格式为：

```
route [add] [del] target gw gateway
```

其中 `target` 是 *目标* 主机或网络，而 *gateway* 是路由器地址。

## 拨号连接

使用调制解调器拨号连接到你的 ISP 是一个两步过程。首先，你必须使用来自 ISP 的设置配置你的调制解调器。之后，你必须手动启动和停止互联网连接。（你大概不希望调制解调器整天占用你的电话线。）

GNOME 3 和 KDE Plasma 桌面环境各有自己的软件包用于配置调制解调器和连接 ISP：

- `GNOME-PPP`：适用于 GNOME 3 桌面
- `KDEPPP`：适用于 KDE Plasma 桌面

如果你的 Linux 发行版未包含这些程序，可以从大多数 Linux 发行版的标准安装 CD 安装这两个软件包。（参见第 15 章。）安装后，你可以一步步配置它们以配合你的调制解调器工作。

## 一切顺利直到某处出现问题

在理想世界中，前一部分中的网络配置步骤将 100% 有效。Linux 厂商确实隐藏了传统上围绕网络的所有神秘感。不幸的是，在许多情况下（主要与调制解调器和硬件相关），简化的配置无法正常工作。如果你按照这些步骤仍无法连接到互联网，一个寻找帮助的绝佳网站是 LinuxQuestions.org (`www.linuxquestions.org`)。是的，我知道——你将不得不使用另一台已经拥有互联网访问权限的计算机、智能手机或热点来获取该帮助。（这是个无解困境吗？）要预见人们可能遇到的广泛问题范围简直不可能，而 Linux 社区是你最好的选择；该网站以其乐于助人的社区成员而闻名。

此外，前往你喜欢的搜索引擎，搜索系统正在给出的错误信息——如果仅搜索错误信息不起作用，加上网络硬件的制造商型号和你的发行版名称也无妨。当你在试图弄清楚网络连接出了什么问题——或者试图收集信息以帮他人弄清楚问题所在时——你可以使用一个很酷的工具：方便的命令行程序 `ping`。

![](img/577d3bff979ee86b07f9836e0df274ce_185_0.png)

某些主机和防火墙会阻止通过 `pings` 发送的那类流量，因此即使连接良好，这些命令也不总是按预期工作。

Linux 中的 `ping` 命令类似于潜艇使用声呐检测海洋中的其他物体。声呐发出 `ping` 信号，该信号在硬表面上反射。通过测量发送 `ping` 和 `ping` 返回之间的时间量，潜艇工程师可以确定物体是否在那儿，以及物体距离潜艇有多远。
