
# 配置 TCP/IP

因为它将根据输入的 IP 地址推断出正确的值。如果你想显式地提供网络掩码值，可以使用关键字 `netmask` 将其添加到命令行中：

```
ifconfig eth0 147.123.20.1 netmask 255.255.255.0
```

此命令显式地将网络掩码设置为 255.255.255.0。然后你可以使用接口名称通过 `ifconfig` 命令检查该接口：

```
$ ifconfig eth0
Link encap 100Mps: Ethernet Hwaddr
inet 147.123.20.1 Bcast 147.123.1.255 Mask 255.255.255.0
UP BROADCAST RUNNING MTU 1500 Metric 1
RX packets:0 errors:0 dropped:0 overruns:0
TX packets:0 errors:0 dropped:0 overruns:0
```

你可能在输出中注意到，广播地址是根据本地机器的 IP 地址设置的。这就是为什么你尝试通过 TCP/IP 同时访问本地局域网上的所有机器。数据传输单元（MTU）通常设置为最大值 1500（对于以太网网络）。

接下来，你需要向内核路由表添加一个条目，让内核知道本地机器的网络地址。此项信息允许它将数据发送到同一网络上的其他机器。在使用 `route` 命令时带的 IP 地址不是你本地机器的 IP 地址，而是整个网络的一个本地标识符。要一次性设置整个局域网，可以使用 `route` 命令的 `-net` 选项。在之前所示的 IP 地址情况下，命令为：

```
route add -net 147.123.20.0
```

此命令将由网络地址 147.123.20.0 识别的网络上的所有机器都添加到内核的可访问机器列表中。如果不这样做，你就必须手动输入网络上每台机器的 IP 地址。另一种方法是使用 `/etc/networks` 文件，该文件可以包含网络名称及其 IP 地址的列表。如果你在 `/etc/networks` 文件中有一个名为 `foobar_net` 的网络条目，你可以使用以下命令将该条目添加到路由表：

```
route add foobar_net
```

一旦路由已添加到内核路由表中，你就可以尝试以太网接口了。当然，这一步假设你已经连接到其他机器，并且知道其中一台机器的 IP 地址。如果你的网络尚未安装，或者你没有连接到另一台运行 TCP/IP 的机器，你就无法尝试此操作。要 ping 另一台机器，你需要它的 IP 地址或它的本地名称。假设你知道 IP 地址并想 ping 机器 142.12.130.12。该命令和输出如下所示：

```
64 bytes from 142.12.130.12: icmp_seq=2, time=10 ms
64 bytes from 142.12.130.12: icmp_seq=3, time=20 ms
64 bytes from 142.12.130.12: icmp_seq=4, time=10 ms
64 bytes from 142.12.130.12: icmp_seq=5, time=10 ms
64 bytes from 142.12.130.12: icmp_seq=6, time=10 ms
^C
-- 142.12.130.12 PING Statistics ---
7 packets transmitted, 7 packets received, 0% packet
round-trip (ms) min/avg/max = 10/12/20
```

再次，路由在七次尝试后中断。当 `ping` 向远程机器发送请求并等待回复时，你可以看到诊断信息和摘要。

如果你没有从远程机器收到任何回复，请验证该机器是否已连接以及你使用的是否正确的 IP 地址。如果那边一切正常，请检查 `ifconfig` 和 `route` 命令。如果检查通过，尝试 ping 另一台机器。如果失败，你可以求 `netstat` 工具，该工具将在第 32 章中详细讨论。

# 配置 PLIP

PLIP（并行端口 IP）接口仅用于通过其并行端口连接两台机器。（第 29 节简要查看了 PLIP）。配置 PLIP 与配置 TCP/IP 不同，特别是该接口不是标准的 TCP/IP 接口，且仅涉及两台机器。

假设你的本地 Linux 机器名为 `darkstar`，你兄弟的机器名为 `x-wing`，之间有一个简单的 PLIP 接口。它们通过一根空并行线连接（接线规范请参见前一章）。两台机器都只有一个用于 PLIP 的并行端口。当按照第 29 节所示方式配置 PLIP 时，两台机器上的设备均被设置为 `/dev/plip0`。

要配置两台机器之间的 PLIP 接口，使用 `ifconfig` 命令，尽管它使用了一个名为 `pointoint` 的特殊关键字（point-to-point 的缩写，用于描述网络类型）。连接所需的 `ifconfig` 命令为：

```
ifconfig plip0 x-wing pointoint
```

注意设备为 `/dev/plip0`，远程机器是 `x-wing`。一旦路由已添加到内核路由表中，你就可以尝试以太网接口了。

# SLIP 与 PPP

## 第 31 章

### 本章内容

- 设置虚拟接口 482
- 设置 SLIP 483
- 设置 PPP 486
- 为 SLIP 和 PPP 使用 DNS 493

## 网络
第四部分

本章将介绍在你的 Linux 系统上使用 SLIP（串行链路协议）或 PPP（点对点协议）时所需的配置和设置。这紧接在上一章中执行的通用 TCP/IP 配置之后。SLIP 和 PPP 均通过拨号调制调制器工作，本质上是先与远程系统建立一个标准的调制调制器链路，然后调用 SLIP 或 PPP 协议。在许多方面，SLIP 和 PPP 类似于 PLIP 接口；尽管 SLIP 和 PPP 使用串行调制调制器端口，但它们实际上是涉及两台机器的点对点接口。的是，SLIP 和 PPP 的配置比 PLIP 更复杂。

你可以在配置通用 TCP/IP 文件时进行 SLIP 和 PPP 配置，也可以等到需要为 SLIP 或 PPP 访问设置它们时进行。由于并非所有安装都需要 SLIP 或 PPP，你可以很轻松地等待。然而，大多数互联网服务提供商倾向于从小型系统使用 SLIP 或 PPP，因为它们提供了快速高效的传输。

## 设置虚拟接口

什么是虚拟接口（dummy interface）？这是一种技巧，让你的机器在仅使用 SLIP 和 PPP 接口时也能有一个 IP 地址可以工作。虚拟接口解决了独立机器（没有网卡连接到其他机器）的问题，这种机器唯一可以发送数据的有效 IP 地址是环回驱动程序（127.0.0.1）。虽然 SLIP 和 PPP 可能用于将你的机器连接到外部，但当接口未激活时，你没有应用程序可以使用的内部 IP 地址。

问题出现在某些需要有效 IP 地址才能运行的应用程序上。例如，某些处理器和桌面布局工具要求 TCP/IP 系统运行，并为目标机器提供一个 IP 地址。虚拟接口本质上为你的本地机器设置了一个 IP 地址，该地址从 TCP/IP 的角度来看是有效的，但除了欺骗应用程序外，不会被实际使用。

使用环回驱动程序创建虚拟接口非常简单。如果你的机器已经在 `/etc/hosts` 文件中为其分配了 IP 地址，你只需要设置接口并创建路由即可。需要以下两条命令：

```
ifconfig 127.0.0.1
route add 127.0.0.1
```

`ifconfig` 的 `lo` 部分表示该行指的是环回驱动程序。这将创建一个到 IP 地址 127.0.0.1 的链接。如果你在 `/etc/hosts` 文件中尚未为 localhost 设置 IP 地址，你应该在创建虚拟接口之前添加一个。要创建环回接口，编辑 `/etc/hosts` 文件，使其包含如下行：

```
127.0.0.1       localhost
```

这使得你的本地机器使用 IP 地址 127.0.0.1 作为 localhost 接口。在使用 `ifconfig` 命令后，你可以通过带有接口名称的 `ifconfig` 命令显示统计信息来验证环回接口是否正常：

```
merlin $ ifconfig lo
Link encap:Local Loopback inet addr:127.0.0.1 Bcast:127.255.255.255 Mask:255.0.0.0
UP BROADCAST LOOPBACK RUNNING MTU:2000 Metric:1
RX packets: errors:0 dropped:overruns:0
TX packets: errors:0 dropped:overruns:0
```

这显示环回接口正在运行，并已分配了 IP 127.0.0.1 和广播掩码 255.0.0.0。

在使用 `route` 命令将环回驱动程序添加到路由表后，你可以使用 `ping` 命令检查接口是否正常响应：

```
merlin $ ping localhost
PING localhost (127.0.0.1): 56 data bytes
64 bytes from 127.0.0.1: icmp_seq=0 ttl=255 time=0.8 ms
64 bytes from 127.0.0.1: icmp_seq=1 ttl=255 time=0.7 ms
64 bytes from 127.0.0.1: icmp_seq=2 ttl=255 time=0.7 ms
64 bytes from 127.0.0.1: icmp_seq=3 ttl=255 time=0.7 ms
64 bytes from 127.0.0.1: icmp_seq=4 ttl=255 time=0.7 ms
-- localhost ping 统计 ---
5 packets transmitted, 5 packets received, 0% packet loss
round-trip min/avg/max = 0.7/0.7/0.8 ms
```

你必须通过 `Ctrl+C` 中断 `ping` 命令来停止它。输出显示用于 localhost 机器的数据包已正确送达，且回复几乎立即。如果你收到任何这样的输出，说明你的接口设置正确。如果你收到未知主机（unknown host）消息，说明你的主机名未被识别。检查 `/etc/hosts` 文件。

## 设置 SLIP

专用 SLIP 最简单的方法是使用 `slattach` 程序。它将串口端口的设备名称作为参数。例如，为了专用串口端口（`/dev/cua1`），你会执行此命令：

```
slattach /dev/cua1 &
```

一旦连接成功，端口将设置为第一个 SLIP 设备 `/dev/s0`。如果你使用多个串口端口，需要为每条线路执行命令。后续的 SLIP 设备（`/dev/s1`、`/dev/s2` 等）将由 `slattach` 分配。大多数 Linux 版本支持八条 SLIP 线路。

默认情况下，Linux 系统将端口设置为 `csplip`。如果你想覆盖设置，使用 `-p` 选项和 slip 名称：

```
slattach -p slip /dev/cua1 &
```

你可以使用 `slip` 和 `csplip` 以外的模式遵循 `-p` 选项（SLIP 的 slip 版本）和 adaptive（用于适应另一端的自适应 SLIP）。

你必须确保连接的两端使用相同的 SLIP 形式。例如，你不能将你的设备设置为 `csplip` 并与运行 SLIP 的机器通信。如果 SLIP 版本不匹配，如 `ping` 等命令将失败。

## 配置 SLIP

一旦串口端口已设置为 SLIP 使用，你可以使用与普通网络连接相同的步骤（包括虚拟接口）来配置接口。例如，如果你的机器名为 merlin 而你正在连接 arthur，执行以下命令：

```
ifconfig s0 merlin-slip pointpoint arthur
route add arthur
```

上面的 `ifconfig` 命令将接口 `merlin-slip`（SLIP 接口的本地地址）配置为到 arthur 的点对点连接。`route` 命令将远程机器 arthur 添加到路由表中。你还可以执行另一个命令将默认路由设置为 gateway arthur：

```
route add default gw arthur
```

如果你想使用 SLIP 端口访问互联网，它必须有一个 IP 地址并且在 `/etc/hosts` 文件中有条目。这使得 SLIP 系统在互联网上有一个有效的条目。更好的方法是使用 DNS，但配置更为复杂。

一旦执行了 `ifconfig` 和 `route` 命令，你就可以测试并使用你的 SLIP 网络了。如果你将来决定移除 SLIP 接口，你必须移除 SLIP 条目，使用 `ifconfig` 禁用 SLIP 接口，然后杀死 `slattach` 进程。前两个步骤通过这些命令完成：

```
route del arthur
ifconfig slip0 down
```
