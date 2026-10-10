
在成功连接到网络甚至互联网之前，需要做的第一件事是创建 `localhost` 接口，有时也称为环回接口，但更常见的称呼是 `lo`。`TCP/IP` 协议（参见本章稍后的“使用 TCP/IP 进行网络通信”）使用此接口为计算机分配 IP 地址，并且对于 Fedora 建立 `PPP` 接口也是必需的。

## 检查环回接口是否可用

通常你不需要手动创建环回接口，因为 Fedora 在安装过程中会自动为你创建一个。要检查是否已设置，你可以在以 root 用户操作时使用 `ifconfig` 命令，显示类似以下内容：

```
# ifconfig
lo
Link encap:Local Loopback
inet addr:127.0.0.1 Mask:255.0.0.0
UP LOOPBACK RUNNING MTU:16436 Metric:1
RX packets:12 errors:0 dropped:0 overruns:0 frame:0
TX packets:12 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:0
RX bytes:760 (760.0 b) TX bytes:760 (760.0 b)
```

在此示例中看到的证据表明环回接口存在且处于活动状态。它显示 `inet addr` 是分配给 `localhost` 的 IP 地址，通常是 `127.0.0.1`，并带有广播掩码 `255.255.255.0`，并且该接口上的活动很少（`RX` = 接收，`TX` = 发送）。如果你的输出与上述不同，则必须在完成本节其余内容后手动配置 `localhost` 接口。

## 手动配置环回接口

`localhost` 接口的 IP 地址在一个文本配置文件中指定，Fedora 使用该文件记录各种全网 IP 地址。该文件名为 `/etc/hosts`，即使为空，通常也存在于系统中。Linux 内核和其他网络工具使用此文件来访问本地 IP 地址和主机名。如果你没有配置其他网络接口，你可能会发现该文件仅包含一行：

```
127.0.0.1 localhost.localdomain localhost
```

这行代码定义了特殊的 `localhost` 接口，并将其 IP 地址分配为 `127.0.0.1`。你可能会听到或读到诸如 `localhost`、`loopback` 和 `dummy interface`（虚拟接口）等术语；所有这些术语都指代 IP 地址 `127.0.0.1` 的用途。术语 `loopback interface` 表示对于 Linux 网络驱动程序而言，这看起来就像机器正在与仅由一台机器组成的网络进行通信；内核在同一台计算机上向自身发送和接收网络流量。`虚拟接口` 表示从外部世界的角度来看，该接口实际上并不存在；它仅对本地机器存在。

局域网（LAN）中每台联网的 Fedora 计算机都将使用相同的 IP 地址作为其 `localhost`。如果由于某种原因 Fedora 计算机没有此接口，请编辑 `/etc/hosts` 文件以添加 `localhost` 条目，然后使用 `ifconfig` 和 `route` 命令以 root 身份创建该接口，操作如下：

```
# ifconfig lo 127.0.0.1
# route add 127.0.0.1 lo
```

这些命令在内存中创建了 `localhost` 接口（所有接口，例如 `eth0` 或 `ppp0`，都是在 Linux 中通过内存创建的），然后将 IP 地址 `127.0.0.1` 添加到一个内部（内存中）的表中，以便 Linux 内核的网络代码可以跟踪到不同地址的路由。

使用前面所示的 `ifconfig` 命令来测试该接口。此时你应该能够使用 `ping` 来检查接口是否正常运行，如下所示（使用 `localhost` 或其 IP 地址均可）：

```
$ ping -c 3 localhost
PING localhost.localhost (127.0.0.1) from 127.0.0.1: 56(84) bytes of data.
64 bytes from localhost.localhost (127.0.0.1): icmp_seq=0 ttl=255 time=212 \usec
64 bytes from localhost.localhost (127.0.0.1): icmp_seq=1 ttl=255 time=80 usec
64 bytes from localhost.localhost (127.0.0.1): icmp_seq=2 ttl=255 time=50 usec

--- localhost.localhost ping statistics ---
3 packets transmitted, 3 packets received, 0% packet loss
round-trip min/avg/max/mdev = 0.050/0.114/0.212/0.070 ms
```

`-c` 选项用于设置 `ping` 的次数，如果命令成功（如前所述），它将返回有关发送到指定主机的测试数据包往返速度的信息。

## 使用 TCP/IP 进行网络通信

任何基于 UNIX 主机的网络的基本构建模块都是由三个协议组成的 `传输控制协议/互联网协议（TCP/IP）` 套件。该套件由 `互联网协议（IP）`、`传输控制协议（TCP）` 和 `用户数据报协议（UDP）` 组成。`IP` 是基础协议。`TCP/IP` 套件是 `基于数据包的`，这意味着数据在发送端被分解成小块以便传输到接收端。将数据分解为可管理的数据包可以实现更快、更准确的传输。在 `TCP/IP` 中，所有数据都通过 `IP` 数据包传输，这就是为什么地址被称为 IP 地址的原因。它是该套件的最低层。

`TCP` 是一种基于连接的协议。在两台机器之间传输数据之前，必须先建立连接。建立连接后，数据流会被发送到 `IP`，进而被分解为数据包并进行传输。在接收端，数据包会被重新排序并发送到正确的应用程序端口。`TCP/IP` 构成了互联网的基础；没有它，互联网将会是完全不同的样子，甚至可能根本不存在！

另一方面，`UDP` 是一种无连接协议。使用该协议的应用程序只需选择其目标并开始发送即可。`UDP` 通常用于小量数据或在快速可靠的网络上。如果你有兴趣了解 `TCP/IP` 的内部机制，请参阅本章末尾的“参考文献”部分，寻找更多相关信息。

## Fedora 与网络

你的网卡很可能在 Fedora 安装过程中已经配置好了。然而，你可以使用 shell 提示符下的 `ifconfig` 命令或 Fedora 的图形化网络配置工具（例如 `system-config-network`）来编辑系统的网络设备信息，或添加/移除系统中的网络设备。Fedora 附带数百个网络命令和实用工具——本章无法涵盖所有这些内容，其数量足以编写两三卷书。

几乎所有以太网卡都可以与 Linux 一起使用，许多 PCMCIA 有线和无线网络卡也是如此。好消息是，许多 USB 无线网卡也能在 Linux 上正常工作，而且随着 Linux 内核新版本的出现，更多设备将获得支持。请访问 `http://www.linux-usb.org/` 查看 Linux USB 项目的最新进展或验证对你的设备的支持情况。

阅读完本章后，你可能想进一步了解用于 Linux 的其他图形化网络客户端。例如，GNOME `etherpeak` 客户端可用于监控局域网（LAN）上的所有流量或特定类型的流量。另一个客户端 `NmapFE` 可用于扫描特定主机的开放端口和其他运行中的服务。

## 高级无线网络

如前所述，自 1990 年代初制定第一项标准以来，Linux 就一直支持无线网络。随着计算机变得越来越小，无线网络的用途日益增加；同时，传输速度也一直在提高。创建无线网络有几种不同的方法。以下几节将介绍你可以在 Fedora 系统上用于初始化、配置和管理无线网络的若干 Linux 命令。

### Fedora 对无线网络的支持

Fedora 附带的 Linux 内核提供了对无线网络的广泛支持。用于配置、管理或显示无线连接信息的相关无线工具包括：

- `iwconfig`——设置无线网络接口的网络名称、加密、传输速率及其他功能
- `iwlist`——显示无线接口的信息，例如速率、功率级别或使用的频率
- `iwpriv`——使用 `i` 设置无线接口的可选功能，例如漫游
- `iwspy`——显示多个节点的无线统计信息

无线设备的兼容性各不相同——大多数情况下是以 PCMCIA 适配器的形式出现——尽管现在一些 USB 无线设备也能与 Linux 协同工作。通常，Linux 无线设备软件（通常以内核模块的形式存在）支持创建以太网设备，这些设备可以由传统的接口工具（例如 `ifconfig`）进行管理——而设备的无线功能则由各种无线软件工具管理。

例如，当首次识别并初始化无线网络设备以供使用时，驱动程序通常会报告一个新设备：
