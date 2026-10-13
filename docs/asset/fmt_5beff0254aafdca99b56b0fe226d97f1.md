
- 第四行指定网络地址。

- 第五行指定广播地址。

- 第六行包含 `ONBOOT` 选项，如果您希望网络接口在启动后处于“up”（启动）状态，则应将其设置为 `yes`。

配置完这两个文件后，您就可以启动网络了。启动您刚刚配置的接口的最简单方法是运行以下命令：

```
/etc/sysconfig/network-scripts/ifup eth0
```

`ifup` 脚本以设备名称作为参数并启动它。它还为网络创建默认路由。运行此命令后，您可以使用 `ifconfig` 程序查看接口是否已启动并运行。要查看设备 `eth0` 是否已启动，请运行以下命令：

```
ifconfig eth0
```

您应该会看到类似以下的输出：

```
eth0 Link encap:Ethernet HWaddr 00:C0:F6:98:37:37
inet addr:206.171.50.50 Bcast:206.171.50.63
Mask:255.255.255.240
UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
RX packets:9470 errors:0 dropped:0 overruns:0 frame:0
TX packets:7578 errors:0 dropped:0 overruns:0 carrier:0
collisions:0
Interrupt:5 Base address:0x340
```

这里，`ifconfig` 报告网络接口设备 `eth0` 的 Internet 地址（`inet addr`）为 206.171.50.50，广播地址（`Bcast`）为 206.171.50.63，网络掩码为 255.255.255.240。其余信息显示此接口迄今接收了多少数据包（`RX packets`）、发送了多少数据包（`TX packets`）、迄今发生了多少种不同类型的错误、此设备使用哪个中断地址线、使用的 I/O 地址基址是什么等等。

您可以在不带任何参数的情况下运行 `ifconfig` 以获取所有已启动网络设备的完整列表。请注意，`ifup` 脚本使用 `ifconfig` 启动接口。例如，

```
ifconfig eth0 206.171.50.50 netmask 255.255.255.240 \
broadcast 206.171.50.63
```

启动 `eth0` 并使用 IP 地址 206.171.50.50。您也可以使用 `ifconfig` 命令快速关闭接口。例如，以下命令关闭 `eth0` 接口：

```
ifconfig eth0 down
```

接口启动并运行后，尝试联系网络中的一台计算机。您可以使用 `ping` `IP 地址` 命令查看新的接口是否可用于联系同一网络上的主机。

如果在安装期间 `/etc/resolv.conf` 文件未正确设置，您将无法使用主机名 `ping` 主机。`/etc/resolv.conf` 文件如下所示：

```
search nitec.com
nameserver 206.171.50.50
```

这是在 Red Hat Linux 安装期间设置的。如果您为名称服务器指定了无效的 IP 地址，您的计算机将无法联系名称服务器。因此，如果您的网络接口已启动但无法使用主机名 `ping` 主机，请尝试使用主机的 IP 地址（实际上是网络接口地址）。如果您可以 `ping` 网络上的其他主机，则您的接口已正确设置；只需通过修复名称服务器的 IP 地址来更正 name-server 行即可。

但是，如果您无法使用 IP 地址或主机名 `ping` 主机，则可能存在路由问题。如果您没有使用前面所示的 `ifup` 脚本，而是使用 `ifconfig` 启动接口，则需要手动创建到网络的默认路由和默认网关。要为网络创建默认路由，请按如下方式使用 `route` 命令：

```
route add -net network address netmask device
```

例如，要为 206.171.50.48 网络创建默认路由，网络掩码为 255.255.255.240，接口为 `eth0`，我可以运行：

```
route add -net 206.171.50.48 255.255.255.240 eth0
```

要设置默认网关，您可以按如下方式运行 `route` 命令：

```
route add default gw gateway address device
```

例如，要将默认网关地址设置为 206.171.50.49，我可以运行以下命令：

```
route add default gw 206.171.50.49 eth0
```

您可以使用以下命令验证网络路由和默认网关是否已正确设置在路由表中：

```
route -n
```

以下是前述命令输出的示例：

内核 IP 路由表

| 目标 | 网关 | 掩码 | 标志 | 度量 | 引用 | 使用 | 接口 |
|---|---|---|---|---|---|---|---|
| 206.171.50.48 | 0.0.0.0 | 255.255.255.240 | U | 0 | 0 | 6 | eth0 |
| 127.0.0.0 | 0.0.0.0 | 255.0.0.0 | U | 0 | 0 | 5 | lo |
| 0.0.0.0 | 206.171.50.49 | 0.0.0.0 | UG | 0 | 0 | 17 | eth0 |

在此阶段，使用 `ping` 程序 `ping` 网络内部和外部的主机。如果成功，则您的网络已启动。如果仍然没有收到 `ping` 尝试的任何回复，请返回本节开头并确保已按照建议执行了所有步骤。

## 使用单个网络接口为多个 IP 地址创建别名

创建 IP 别名的第一步是确定内核是否已加载 IP 别名模块。检查此问题的最简单方法是运行 `lsmod` 命令并查看输出中是否列出了 `ip_alias.o`。如果没有看到该模块，并且没有自定义编译内核以将该模块作为内核的一部分包含在内，你可以尝试使用以下命令加载模块：

```
/sbin/insmod /path/to/ip_alias.o
```

其中 `/path/to/ip_alias.o` 是 `ip_alias.o` 模块的实际路径。你可以使用 `locate ip_alias.o` 来定位系统中的路径。通常，路径为 `/lib/modules/kernel version number/ipv4/ip_alias.o`。加载 `ip_alias.o` 模块后，运行 `lsmod` 以确保它已加载。现在，要为 `eth0` 设备创建别名，请执行以下操作：

- 1. 将现有的 `/etc/sysconfig/network-scripts/ifcfg-eth0` 文件复制到 `/etc/sysconfig/network-scripts/ifcfg-eth0:0` 以创建名为 `eth0:0` 的别名设备。

- 2. 修改文件，使其具有与清单 7-3 中所示类似的行。当然，你的网络、子网掩码和 IP 地址会有所不同。请确保只更改 `DEVICE` 和 `IPADDR` 行。`DEVICE` 行应设置为 `eth0:0`，而 `IPADDR` 应设置为你希望用作 `eth0` 已分配地址的别名的 IP 地址。

### 清单 7-3 `/etc/sysconfig/network-scripts/ifcfg-eth0:0` 文件

```
DEVICE=eth0:0
USERCTL=no
ONBOOT=yes
BOOTPROTO=
BROADCAST=206.171.50.63
NETWORK=206.171.50.48
NETMASK=255.255.255.240
IPADDR=206.171.50.58
```

- 3. 要启动别名设备，运行 `ifconfig eth0:0 up`，你应该会看到类似以下内容的输出：
