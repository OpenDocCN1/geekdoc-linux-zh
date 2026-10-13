
```
eepro1000.c:v1.09-t 2/29/99 Donald Becker http://cesdis.gsfc.nasa.gov/linux/drive/eepro1000.html
schokin>
PCI: Found IRQ 10 for device 00:0d.0
eth0: Intel Corporation 82557 [Ethernet Pro 100], 00:90:27:91:B2:B5, IRQ 10.
Board assembly 721833-007, Physical connectors present: RJ45
Primary interface chip:test PHY #1
General self-test: passed.
Serial sub-system self-test: passed.
Internal registers self-test: passed.
ROM checksum self-test: passed (0x04f4518b).
```

# 使用网络配置工具

对于 Linux 新手来说，使用命令行配置工具可能看起来很困难。`system-config-network` 图形化工具是更好的选择。手动方法和图形化方法都需要网络的 root 权限。如果你没有权限，请在尝试这些操作之前先获取权限。你不应该编辑系统上供图形化网络管理工具使用的任何脚本或设置。当你下次运行该工具（如 `system-config-network`）时，你的更改将会丢失！请使用手动方法并编写你自己的网络设置脚本，或者坚持使用图形化配置。

> 注意
>
> 本节中描述的网络配置过程是针对客户端主机的。你无法在安装期间执行服务器级网络配置，例如域名系统 (DNS) 和 DHCP。（有关配置 DNS 的更多信息，请参阅第 14 章“管理 DNS”；有关该项的更多信息，请参见本章节稍后的“DHCP”部分。）

# 命令行网络接口配置

你可以使用基础 Linux 网络工具从命令行配置网络接口。你可以通过命令更改当前设置或通过编辑多个系统文件来通过命令行配置网络客户端主机。`ifconfig` 和 `route` 两个命令用于网络配置。`netstat` 命令显示网络连接的信息。

```
/sbin/ifconfig
```
`ifconfig` 用于配置你的网络接口。你可以用它来

- 激活或禁用你的网卡 (NIC) 或更改网卡模式
- 更改你机器的 IP 地址、子网掩码或广播地址
- 创建 IP 别名以允许网卡上出现多个 IP 地址
- 为点对点连接设置目标地址

你可以通过一个命令根据需要更改尽可能多或尽可能少的选项。该命令的基本结构如下：

```
/sbin/ifconfig [network device] options
```

表 13.1 显示了 `ifconfig` 选项的子集及其用法示例。

# 表 13.1 ifconfig 选项

| 用途 | 选项 | 示例 |
| --- | --- | --- |
| 创建别名 | `[network device]:[number]` | `ifconfig eth0:0 10.10.10` |
| 更改 IP 地址 | | `ifconfig eth0 10.10.12` |
| 更改掩码 | `netmask [netmask]` | `ifconfig eth0 netmask 255.255.255.0` |
| 更改广播 | `broadcast [address]` | `ifconfig eth0 10.10.25` |
| 禁用接口 | `down` | `ifconfig eth0 down` |
| 启用接口 | `up` (添加 IP 地址) | `ifconfig eth0 up` (`ifconfig eth0:10.10.10`) |
| 在 `[设备]`上开启/关闭 混杂模式 | `[-]promisc` | `ifconfig eth0 promis` [`ifconfig eth0 -promisc`] |
| 在 `[设备]`上开启/关闭多播模式 | `[-]allmulti` | `ifconfig eth0 allmulti` [`ifconfig eth0 -allmulti`] |
| `[启用][禁用]`点对点地址 | `[-]pointpoint [address]` | `ifconfig eth0 pointpoint 10.10.20` |

`ifconfig` 帮助页显示了其他选项，使你的机器能够与 AppleTalk、Novell、IPv6 等多种网络类型进行交互。再次，请阅读页面以获取这些网络类型的详情。

> 注意
>
> 混杂模式会导致网卡接收网络上的所有数据包。它通常用于嗅探网络。多播模式允许网卡接收网络上的所有多播流量。

如果没有给出参数，`ifconfig` 会显示活动接口的状态。例如，在不带参数且有一个已激活并配置的网卡的情况下，`ifconfig` 的输出类似于：

```
# /sbin/ifconfig
```

```
eth0      Link encap:Ethernet Haddr:00:30:1B:0B:07:0D
inet addr:192.168.2.70 Bcast:192.168.2.255 Mask:255.255.255.0
UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
RX packets:127948 errors:0 dropped:0 overflows:0 frame:
```TX packets:127675 errors:0 overflows:0 carrier:0

collisions:7874 txqueelen:100

RX bytes:19098389 (18.2 MB) TX bytes:73768657 (70.3 MB)

Interrupt:11 Base address:0x2000 Link encap:Local Loopback

inet addr:127.0.0.1 Mask:255.0.0

UP LOOPBACK RUNNING MTU:16384 Metric:1

RX packets:215214 errors:0 overflows:0 frame:0

TX packets:215214 errors:0 overflows:0 carrier:0

collisions:txqueelen:0

RX bytes:6837080 (65.5 MB) TX bytes:6837080 (65.5 MB)
```

输出易于读取。该条目显示了接口的 IP 地址。`UP` 表示接口已就绪，`BROADCAST` 表示接口已连接到网络，`RUNNING` 接口正在运行，而 `LOOPBACK` 显示哪个设备 (`lo`) 是环回地址。`eth0` 上的最大传输单元 (MTU) 为 1500。`Metric` 决定了路由的优先级。`ifconfig` 命令可以显示关于接口的 IP 地址。`UP` 表示接口已就绪，`BROADCAST` 表示接口已连接到网络，`RUNNING` 意味着接口正在运行，`LOOPBACK` 显示哪个设备 (`lo`) 是环回地址。`eth0` 上的最大传输单元 (MTU) 为 1500。`Metric` 决定了路由的优先级。`ifconfig` 命令可以显示关于接口的 IP 地址。`UP` 表示接口已就绪，`BROADCAST` 表示接口已连接到网络，`RUNNING` 意味着接口正在运行，`LOOPBACK` 显示哪个设备 (`lo`) 是环回地址。

`route` 命令最常见的用途是为主机添加默认网关、为丢失路由表的主机或网关地址更改时添加。例如，要添加具有特定 IP 地址的网关，可以使用以下命令：

```
# /sbin/route add default gw 149.112.50.65
```

注意，如果需要，可以使用主机名代替 IP 地址。另一个常见用途是在使用 `ifconfig` 命令配置接口后，立即将网络添加到路由表中。假设之前的示例中缺少了 `208.54.243.0` 条目，请使用以下命令进行替换：

```
# /sbin/route add -net 208.54.243.0 netmask 255.255.255.0 eth0
```

你还可以使用 `/sbin/route` 为特定主机配置直接（点对点）连接。例如，假设你家里有一个由两台电脑组成的家庭网络。其中一台电脑通过调制解调器连接到你的业务网络。你通常在另一台电脑上工作。你可以使用以下命令在特定主机之间建立连接：

```
# /sbin/route add -host 198.135.62.25 gw 149.112.50.65
```

前面的示例将带有调制解调器的电脑作为你正在使用的电脑的网关。如果你连接到互联网的网关或防火墙，这种命令非常有用。`route` 命令还有许多其他用途，例如操作默认数据包大小。这些用途请帮助页（man page）。

```
/bin/netstat
```
