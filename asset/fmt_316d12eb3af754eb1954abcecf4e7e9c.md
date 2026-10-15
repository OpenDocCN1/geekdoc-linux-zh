
# 第 34 章：管理 TCP/IP 网络

```
DEVICE=eth0
BOOTPROTO=static
BROADCAST=192.168.0.255
IPADDR=192.168.0.1
NETMASK=255.255.255.0
NETWORK=192.168.0.0
ONBOOT=yes
```

```
cd /etc/sysconfig/network-scripts
ifconfig ifcfg-eth0
```

`ifconfig` 命令的参数是接口名称和 IP 地址，以及选项。`ifconfig` 命令随后将 IP 地址分配给接口。你的系统现在知道这样一个接口存在，它指向特定的 IP 地址。此外，你可以指定该 IP 地址是主机地址还是网络地址。你可以使用域名名作为 IP 地址，前提是该域名已列在 `/etc/hosts` 文件中。`ifconfig` 命令的语法如下：

```
# ifconfig interface -host_net_flag address options
```

`host_net_flag` 可以是 `-host` 或 `-net` 以指示主机或网络 IP。`-host` 是默认值。`ifconfig` 命令可以多个选项，设置接口的不同功能，例如它可以传输的最大字节数（`mtu`）或广播地址。`up` 和 `down` 选项激活和禁用接口。在下一个示例中，`ifconfig` 命令配置了一个以太网接口：

```
ifconfig eth0 192.168.0.1
```

对于这种简单的配置，`ifconfig` 会自动生成标准的广播地址和子掩码。标准广播地址是主机地址部分为 255 的网络地址。对于 C 类网络，标准子掩码是 255.255.255.0，而对于 A 类网络，标准的网络掩码是 255.0.0.0。然而，如果你连接到一个具有特定网络掩码和广播地址的网络，在使用 `ifconfig` 时必须指定它们。指定广播地址的选项是 `broadcast`；网络掩码的选项是 `netmask`。表 34-9 列出了 `ifconfig` 选项。在下一个示例中，`ifconfig` 包含了网络掩码和广播地址：

```
# ifconfig eth0 192.168.0.1 broadcast 192.168.0.255 netmask 255.255.255.0
```

配置好接口后，可以使用 `ifconfig` 的 `up` 选项激活它，使用 `down` 选项将其禁用。如果你在 `ifconfig` 操作中指定了 IP 地址（如上例所示），则隐含了 `up` 选项。

```
# ifconfig eth0 up
```

点对点接口如并行 IP (`PLIP`)、串行线路 IP (`SLIP`) 和点对点协议 (`PPP`) 要求你包含 `pointpoint` 选项。`PLIP` 接口名称通过带有数字的 `plip` 名称识别。例如，`plip0` 是第一个 `PLIP` 接口。`SLIP` 接口使用 `slip0`。`PPP` 接口以 `pp0` 开头。点对点接口通常在两个主机之间运行，例如通过调制解调器连接的两台电脑。当你指定 `pointpoint` 选项时，需要包含主机的 IP 地址。在下一个示例中，配置了一个 `PLIP` 接口，连接 IP 地址为 192.168.1.72 的计算机与 204.166.254.14 之一。如果 `/etc/hosts` 中列出了这些系统的域名地址，则可以使用这些域名来代替 IP 地址。

```
# ifconfig plip0 192.168.1.72 pointpoint 204.166.254.14
```

如果有需要，你还可以使用 `ifconfig` 配置你的环回设备。环回设备的设备名称为 `lo`，其 IP 地址是特殊地址 127.0.0.1。以下示例显示了配置：

```
# ifconfig lo 127.0.0.1
```

`ifconfig` 命令可用于检查接口状态。如果你输入 `ifconfig` 命令并加上接口名称，将显示该接口的信息：

```
# ifconfig eth0
```

| 选项 |  |

| --- | --- |

| Interface | 网络接口名称，例如第一个以太网设备的 `eth0`，或第一个 PPP 设备（调制解调器）的 `ppp0` |

| up | 激活接口；如果指定了 IP 地址，则隐含 |

| down | 禁用接口 |

| allmulti | 开启或关闭混杂模式；前面的连字符 `-` 表示关闭；这允许进行网络监控 |

| mtu | 在此接口上可以发送的传输的最大字节数 |

| dstaddr address | 点对点连接上的目的 IP 地址 |

| netmask address | IP 网络掩码；前面的连字符 `-` 表示关闭 |

| broadcast address | 广播地址；前面的连字符 `-` 表示关闭 |

| point-to-point address | 接口的点对点模式；如果包含地址，则将其分配给远程系统 |

| hw | 设置接口的硬件地址 |

| Address | 分配给接口的 IP 地址 |

表 34-9. `ifconfig` 选项

要查看你的环回接口是否已配置，可以使用带有环回接口名称 `lo` 的 `ifconfig`：

```
# ifconfig lo
lo Link encap:Local Loopback
inet addr:127.0.0.1 Bcast:127.255.255.255 Mask:255.0.0.0
UP BROADCAST LOOPBACK RUNNING MTU:2000 Metric:1
RX packets:0 errors:0 dropped:0 overflows:0
TX packets:12 errors:0 dropped:0 overflows:0
```

## 路由

作为传输的一部分的数据包通过特定的路由到达目的地。在大网络中，数据包从一台计算机传输到另一台计算机，直到到达目的地。路由决定了过程从哪里开始，以及你的系统需要将数据包发送到哪台电脑才能到达目的地。在小型网络中，路由可能是静态的——也就是说，从一个点到另一个点的路由是固定的。一个系统知道如何通过固定路径到达另一个系统。在规模较大的网络和互联网上，路由是动态的。你的系统知道首先将数据包发送给哪台计算机，然后从那里获取数据包，将其传递给另一台计算机，再由该计算机决定传递到哪里。对于动态路由，你的系统需要知道很少。然而，静态路由可能会变得复杂，因为你必须跟踪所有的网络连接。

你的路由列在 `/proc/net/route` 文件的路由表中。要显示路由表，输入不带参数的 `route`（`netstat -r` 命令也会显示路由表）。

```
# route
Kernel routing table
Destination Gateway Genmask Flags Metric Ref Use Iface
loopback * 255.0.0.0 U 0 0 12 lo
pangol.train.com * 255.255.255.0 U 0 0 0 eth0
```

路由表中的每个条目都有多个字段，提供如路由目的地和所使用的接口类型等信息。不同的字段列在表 34-10 中。

你的路由表中至少应该有一个关于环回接口的条目。如果没有，你必须使用 `route` 命令对环回接口进行路由。在使用接口之前，必须将接口的 IP 地址添加到路由表中。你使用 `route` 命令和 `add` 选项来添加地址：

```
route add address
```

下一个示例将环回接口的 IP 地址添加到路由表中：

```
route add 127.0.0.1
```

| 字段 | 描述 |

| --- | --- |

| Destination | 路由的目的 IP 地址 |

| Gateway | 网关路由使用的网关 IP 地址或主机名；`*` 表示不使用网关 |

| Genmask | 路由的网络掩码 |

| Flags | 路由类型：U = 启用，H = 主机，G = 网关，D = 动态，M = 已修改 |

| Metric | 路由的代价 |

| Ref | 依赖于此路由的路由数量 |

| Window | AX.25 网络的 TCP 窗口 |

| Use | 使用次数 |

| Iface | 此路由使用的接口类型 |

表 34-10. 路由表条目

使用 `add` 参数，你可以为带有 `-net` 选项的网络或带有 `-host` 选项的 IP 接口（主机）添加路由。`-host` 选项是默认选项。此外，你还可以为信息指定几个参数，例如网络掩码（`netmask`）、网关（`gw`）、接口设备（`dev`）和默认路由（`default`）。如果你的系统上有多个接口（例如多个以太网卡），你必须使用 `dev` 参数指定接口名称。如果你的网络有一个网关主机，你使用 `gw` 参数来指定它。如果你的系统连接到网络，你的路由表中至少应该有一个指定默认路由的条目。当没有其他路由条目通向目的地时，这就是数据包所采取的路由。以下示例是以太网接口的路由：
