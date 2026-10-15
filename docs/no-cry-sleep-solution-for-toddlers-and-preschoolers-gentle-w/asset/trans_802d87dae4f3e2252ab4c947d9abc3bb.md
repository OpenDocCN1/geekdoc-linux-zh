

对于这种简单的配置，ifconfig 会自动生成标准的广播地址和网络掩码。标准的广播地址是主机地址为数字 255 的网络地址。对于 C 类网络，标准网络掩码是 255.255.255.0，而对于 A 类网络，标准网络掩码是 255.0.0.0。然而，如果你连接到具有特定网络掩码和广播地址的网络，则在使用 ifconfig 时必须指定它们。指定广播地址的选项是 broadcast；对于网络掩码，则是 netmask。表 38-11 列出了不同的 ifconfig 选项。在下一个示例中，ifconfig 包含了网络掩码和广播地址：

```
# ifconfig eth0 192.168.0.1 broadcast 192.168.0.255 netmask 255.255.255.0
```

配置好接口后，你可以使用 ifconfig 配合 up 选项来激活它，并使用 down 选项来停用它。如果你在 ifconfig 操作中指定了 IP 地址，如前面的示例中那样，则 up 选项是隐含的。

```
# ifconfig eth0 up
```

点对点接口，如并行线路 IP（PLIP）、串行线路 IP（SLIP）和点对点协议（PPP）需要你包含 pointopoint 选项。PLIP 接口名称以 plip 标识并附带一个数字。例如，plip0 是第一个 PLIP 接口。SLIP 接口使用 slip0。PPP 接口以 ppp0 开始。点对点接口通常仅在两个主机之间运行，例如通过调制解调器连接的两台计算机。当你指定 pointopoint 选项时，需要包含主机的 IP 地址。在下一个示例中，一个 PLIP 接口被配置，用于连接 IP 地址为 192.168.1.72 的计算机和 IP 地址为 204.166.254.14 的计算机。如果这些系统的域名在 /etc/hosts 中列出，则可以使用域名代替 IP 地址。

```
# ifconfig plip0 192.168.1.72 pointopoint 204.166.254.14
```

如果需要，你也可以使用 ifconfig 来配置你的回环设备。回环设备的名称是 lo，其 IP 地址是特殊地址 127.0.0.1。以下示例显示了配置：

```
# ifconfig lo 127.0.0.1
```

ifconfig 命令对于检查接口的状态非常有用。如果输入 ifconfig 命令并加上接口名称，将显示有关该接口的信息：

```
# ifconfig eth0
```

要查看你的回环接口是否已配置，可以使用 ifconfig 并加上回环接口名称 lo：

```
# ifconfig lo
lo Link encap:Local Loopback
inet addr:127.0.0.1 Bcast:127.255.255.255 Mask:255.0.0.0
UP BROADCAST LOOPBACK RUNNING MTU:2000 Metric:1
RX packets:0 errors:0 dropped:0 overruns:0
TX packets:12 errors:0 dropped:0 overruns:0
```

## 路由

传输过程中数据包到达目的地需要经过一定的路由。在大型网络中，数据包从一台计算机传输到另一台计算机，直到到达目标计算机。路由决定了过程的起点，以及你的系统需要将数据包发送到哪台计算机才能到达目的地。在小型网络中，路由可能是静态的——也就是说，从一个系统到另一个系统的路由是固定的。一个系统知道如何通过固定路径到达另一个系统。然而，在大型网络和互联网上，路由是动态的。你的系统只需知道将数据包发送给的第一台计算机，然后该计算机再将数据包传递下去，传递给另一台计算机，后者再决定传递到哪里。对于动态路由，你的系统只需知道很少的信息。然而，静态路由可能变得复杂，因为你必须跟踪所有的网络连接。

你的路由列在 /proc/net/route 文件中的路由表中。要显示路由表，输入不带参数的 route（netstat -r 命令也会显示路由表）：

```
# route
Kernel routing table
Destination Gateway Genmask Flags Metric Ref Use Iface
loopback * 255.0.0.0 U 0 0 12 lo
pangol.train.com * 255.255.255.0 U 0 0 eth0
```

| Option | Description |
|---|---|
| Interface | Name of the network interface, such as eth0 for the first Ethernet device or ppp0 for the first PPP device (modem) |
| up | Activates an interface; implied if IP address is specified |
| down | Deactivates an interface |
| allmulti | Turns on or off the promiscuous mode; preceding hyphen (-) turns it off; this allows network monitoring |
| mtu n | Maximum number of bytes that can be sent on this interface per transmission |
| dstaddr address | Destination IP address on a point-to-point connection |
| netmask address | IP network mask; preceding hyphen (-) turns it off |
| broadcast address | Broadcast address; preceding hyphen (-) turns it off |
| point-to-point address | Point-to-point mode for interface; if address is included, it is assigned to remote system |
| hw | Sets hardware address of interface |
| Address | IP address assigned to interface |

**TABLE 38-11 The Ifconfig Options**

