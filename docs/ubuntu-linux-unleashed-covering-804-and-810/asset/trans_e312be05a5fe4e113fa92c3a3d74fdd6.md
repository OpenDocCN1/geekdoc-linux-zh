

如果你的系统中 /etc/hosts 文件中定义了主机（请参阅本章后面的“网络配置文件”部分），你可以按照定义的 hostname 来配置并激活接口，如下所示：

```
$ sudo ifconfig eth0 dogdog.hudson.com up
```

阅读下一节，了解如何配置系统以便与你的局域网协同工作。

## /sbin/route

用于配置网络的第二个命令是 route 命令。route 用于构建路由表（在内存中），用于路由数据包以及显示路由信息。它在 ifconfig 初始化接口之后使用。route 通常用于通过网关或到其他主机设置到其他网络的静态路由。命令配置如下：

```
$ route [options] [commands] [parameters]
```

要显示路由表，请使用不带选项的 route 命令。显示结果看起来类似这样：

```
$ route
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
192.168.2.0     *               255.255.255.0   U     0      0          0 eth0
default         .               0.0.0.0         UG    0      0          0 eth0
```

在第一列中，Destination 是接收主机的 IP 地址（或，如果主机在 /etc/hosts 或 /etc/networks 中，则为主机名）。default 条目是此机器的默认网关。Gateway 列列出了数据包必须经过的网关才能到达目的地。星号 (*) 表示数据包直接发送到主机。Genmask 是网络掩码。Flags 列可能有多个条目。在我们的示例中，U 验证路由已启用，G 指定 Destination 需要使用网关。Metric 列显示到 Destination 的距离。某些守护进程使用它来确定到达 Destination 的最简单路由。Ref 列由某些 UNIX 变体用于传达对路由的引用。Linux 不使用它。Use 列指示此条目被查找的次数。最后，Iface 列是对应条目的接口名称。

使用 route 命令的 -n 选项将给出相同的信息，用 IP 地址代替名称和星号 (*)，看起来像这样：

```
# /sbin/route -n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
192.168.2.0     0.0.0.0         255.255.255.0   U     0      0          0 eth0
0.0.0.0         192.168.2.1     0.0.0.0         UG    0      0          0 eth0
```

route 命令可以使用 add 选项向表中添加条目。使用 add 选项时，你可以指定主机 (-host) 或网络 (-net) 作为目标。如果未使用选项，route 命令假定你正在配置发出命令的主机。route 命令最常见的用途是为一台丢失路由表的主机添加默认网关，或网关地址已更改时。例如，要添加具有特定 IP 地址的网关，可以使用以下命令：

```
$ sudo route add default gw 149.112.50.65
```

请注意，如果需要，你也可以使用主机名代替 IP 地址。另一个常见用途是在使用 ifconfig 命令配置接口后立即将网络添加到路由表中。假设之前的示例中缺少 208.59.243.0 条目，请使用以下命令替换它：

```
$ sudo route add -net 208.59.243.0 netmask 255.255.255.0 dev eth0
```

你也可以使用 route 为直接（点对点）连接配置特定主机。例如，假设你有一个由两台计算机组成的家庭网络。其中一台计算机通过调制解调器连接到你的业务网络。你通常在另一台计算机上工作。你可以使用 route 命令通过特定主机建立连接，使用以下命令：

```
$ sudo route add -host 198.135.62.25 gw 149.112.50.65
```

前面的示例使具有调制解调器的计算机成为你正在使用的计算机的网关。如果你的网关或防火墙连接到 Internet，这种类型的命令行很有用。route 命令还有许多其他用途，例如操作默认数据包大小。请参阅手册页了解这些用途。

## /bin/netstat

netstat 命令用于显示网络状态。它有几个参数，可以显示你喜欢的任意多或任意少的信息。服务按套接字列出（两台计算机之间应用程序到应用程序的连接）。你可以使用 netstat 来显示表 14.2 中的信息。

### TABLE 14.2 netstat Options

| Option | Output |
|---|---|
| -g | Displays the multicast groups configured |
| -i | Displays the interfaces configured by ifconfig |
| -s | Lists a summary of activity for each protocol |
| -v | Gives verbose output, listing both active and inactive sockets |
| -c | Updates output every second (good for testing and troubleshooting) |
| -e | Gives verbose output for active connections only |
| -C | Displays information from the route cache and is good for looking at past connections |

