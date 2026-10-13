
`ifconfig interface up`

这些形式的 `ifconfig` 命令只能由 root 使用。

## 检查接口状态

如果你想知道网络接口的状态，只需执行命令 `ifconfig interface`。如果你想知道所有活动接口的状态，请使用 `ifconfig -a`。这些这些版本的 `ifconfig` 命令可以由任何用户使用。它们显示接口的所有配置信息，包括其 IP 地址、子网掩码、广播地址和物理（硬件）地址。（硬件地址由网卡制造商设置。）它们还显示接口状态，例如它是否处于启用（up）状态或是否为环回接口（loopback interface），还会显示其他信息：最大传输单元（通过该接口发送的最大数据包大小）、网卡的 I/O 地址和 IRQ 编号、接收和发送的数据包数量以及冲突数。

你也可以使用 `ifconfig -a` 命令检查接口状态。这会打印出当前活跃的所有接口及其参数。以下是 `ifconfig -a` 的输出示例：

```
$ ifconfig -a

lo Link:Local Loopback\inet addr:127.0.0.1 Bcast:127.255.255.255 Mask:255.0.0.0 UP BROADCAST LOOPBACK RUNNING MULTICAST MTU:3584 Metric:1

RX packets:16000 errors:0 dropped:0 overflows:0 frame:0

TX packets:16000 errors:0 dropped:0 overflows:0 carrier:0

Collisions:
```

```
eth0 Link:Ethernet Hwaddr 00:20:87:3E:F0:61

net addr:10.0.1.1 Bcast:10.0.1.255 Mask:255.255.255

UPCAST RUNNING MULTICAST MTU:1500 Metric:1

RX packets:90506 errors:0 dropped:0 overflows:0 frame:0

TX packets:92691 errors:0 dropped:0 overflows:0 carrier:1

Collisions:667

Interrupt:3 Base address:0x310
```

## 网络别名——一个接口，多个地址

有时，让单个网络接口拥有多个 IP 地址是有用的。例如，一个服务器可能运行着多个服务，但你可能希望客户端为每个服务访问不同的 IP 地址，以便将来更容易重新配置（例如，你需要将某些服务拆分到另一个服务器）。

### TCP/IP 网络管理
第17 章

Linux 与其他 UNIX 变一样提供了一种名为“网络别名”（network aliasing）的功能，其功能顾如其名。要使用网络别名，你必须重新配置并编译内核，并在网络选项配置部分启用“网络别名支持”和“IP 别名支持”选项。这些选项既可以编译到内核中，也可以作为模块存在。

一旦运行了启用了别名功能的内核，创建别名就像执行标准的 `ifconfig` 命令一样简单。你只需要在接口名称后面加上一个冒号和一个别名数字。这是一个示例：

```
ifconfig eth0:10.1.1.1 netmask 255.255.255.0 broadcast 10.1.1.255
```

这为以太网接口 `eth0` 创建了一个带有提供参数的别名 `eth0:`。

为了在每次主机启动时自动创建别名，你可以将创建别名的命令添加到 `/etc/init.d/network`。

## 其他 ifconfig 选项

针对某些特殊情况，`ifconfig` 还有其他选项：

`ifconfig interface local-address pointoint remote-address` 将启用一个点点接口（Point-to-Point interface）——该接口仅连接到另一个主机，而不是连接到网络。该接口必须在远程主机上启用，并交换 `local-address` 和 `remote-address` 参数。

`ifconfig interface local-address tunnel remote-address` 将在两个 IPv6 网络之间创建一个 IPv4 隧道。IPv4 是目前互联网上的 TCP/IP 标准。IPv6 是下一代标准。如果有两个需要通过互联网连接的 IPv6 网络，则必须创建一个使用 IPv4 协议的隧道。

## 操作路由表：route

`/sbin/route` 命令用于操作内核的路由表。内核使用此表来确定对离开主机的每个数据包需要做什么——是直接发送到目标主机还是网关，以及通过哪个接口发送。`route` 命令的通用格式如下：

```
route [options] [parameters]
```

### 查看路由表

该命令最简单的形式（无选项和命令）直接输出路由表。这种形式的命令可以由任何用户使用：

```
$ /bin/route

Kernel IP routing table

Destination Gateway Genmask Flags Metric Use Interface

local 255.255.255.0 U 0 0 eth0

127.0.0.0 255.0.0.0 U 0 0 lo

default router 0.0.0.0 UG 0 0 eth0
```

输出包含几列：

1. 第一列（Destination，目标）指示路由目的。如果 `/etc/hosts` 中存在对应的条目，则会替换名称。
2. 第二列（Gateway，网关）指示默认路由的网关。
3. 第三列（Genmask，子网掩码）指示掩码。
4. 第四列（Flags，标志）可以有多个值。常见的标志有：U（启用）、G（网关）、H（主机）。
5. 第五列（Metric，度量）指示路由的距离。
6. 第六列（Use，使用）指示内核查找的次数。
7. 第七列（Iface，接口）显示该路由的接口名称。

### TCP/IP 网络管理
第17 章

`-n` 选项稍微修改显示方式。它不进行主机或网络查找，而是显示数字地址：

```
$ /bin/route -n
```

| Destination | Gateway | Genmask | Flags | Metric | Use | Iface |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| local | 255.255.255.0 | U | 0 | 0 | eth0 |
| 127.0.0.0 | 255.0.0.0 | U | 0 | 0 | lo |
| 0.0.0.0 | 10.0.1.254 | 0.0.0.0 | UG | 0 | 0 | eth0 |

在这种情况下，默认目标和 `*` 网关被 `0.0.0.0` 替换。

## 提示

如果你选择了一个路由但它挂住了，请按 Ctrl+C 中断并执行 `route -n`。没有 `-n` 参数的 `route` 会尝试对路由表中的每个 IP 进行反查。

## 操作路由表

`route` 命令向路由表中添加和删除路由。通过以下命令完成：

```
route add|del [-net |host] <target> [gw <gateway>] [-netmask <netmask>] [dev <interface>]
```

`add` 或 `del` 命令分别指示你想添加还是删除路由。

可选的 `-net` 或 `-host` 选项指示你想对网络路由还是主机路由进行操作。（更多信息请参见本章的“静态主机路由”）。提供任何明确信息以消除歧义通常是最好的。（例如，地址 `10.0.1.0` 可以是 C 类网络的网络地址，也可以 A 类或 B 类网络中的主机地址。）

`target` 参数是目标的主机地址或网络编号。设置或删除默认路由时，你会使用关键字 `default` 作为目标。

可选的 `gw` 参数指示为该路由使用哪个网关。如果省略，`route` 命令假设主机或网络直接连接到此

# 系统管理与维护
第三部分

host。在用 `ifconfig` 配置接口后，为本地网络添加路由是有关重要的：

```
# /sbin/ifconfig eth0@ 10.1.1.1 netmask 255.255.255.0 broadcast 10.0.1.255

# /sbin/route add -net 10.1.1.0
```
