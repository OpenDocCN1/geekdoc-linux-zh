
## 配置新的网络接口

在做任何操作之前，运行 dmesg 程序（或查看 /var/log/dmesg 文件）以确定您的 NIC 是否被当前 Linux 内核识别。如果 Linux 内核识别到您的网卡，您应该会在 dmesg 输出中看到一些与内核发现网络设备的相关行。例如，当我在装有通用（NE2000 兼容）以太网卡的 Red Hat Linux 系统上运行以下命令时：

```
dmesg | grep -i eth
```

它显示以下输出：

```
NE2000 ethercard probe at 0x340: 00 c0 f6 98 37 37
eth0: NE2000 found at 0x340, using IRQ 5.
```

这告诉我我的 NE2000 兼容 NIC 已被内核找到，并且使用中断请求线（IRQ）5 以及从 0x340 开始的 I/O 地址空间。另请注意，此设备称为 eth0（以太网设备 0）。

在确认网络设备已被内核识别后，您就可以配置它了。本示例假定您想要配置第一个以太网设备 eth0，并且想要一个持久配置，即每次启动计算机时都会使用它。这是通过 /etc/rc.d/init.d/network 脚本完成的。当此脚本从默认运行级别目录（可能是 /etc/rc.d/rc3.d）链接（其中链接名为 Sxxnetwork；xx 可以是任意数字）时，/etc/rc.d/init.d/network 脚本会在启动时运行。此脚本使用存储在 /etc/sysconfig 目录中的文件加载网络接口。

现在，来看如何配置 eth0 使其在启动时自动启动。您必须修改的第一个文件是 /etc/sysconfig/network。清单 7-1 显示了此文件的示例。

### 清单 7-1 /etc/sysconfig/network 文件

```
NETWORKING=yes
FORWARD_IPV4=yes
HOSTNAME=picasso.nitec.com
DOMAINNAME=nitec.com
GATEWAY=206.171.50.49
GATEWAYDEV=eth0
```

以下列表解释了此文件中的各行：

- NETWORKING=yes 行表示您想要启用网络支持。
- FORWARD_IPV4=yes 应设置为 yes，如果您希望允许转发 IP 数据包到和来自您的 Red Hat Linux 服务器。这仅在 Red Hat Linux 计算机将充当网络的网关或路由器（将在后面的章节中讨论）时才需要。例如，如果您计划在计算机上安装代理服务器软件以允许 LAN 上其他计算机进行 Web 访问，您应该将此设置为 yes。相反，如果您计划仅将此计算机用作 ISP 网络上的共置 Web 服务器，则可以通过将其设置为 no 来关闭 IP 转发。
- 接下来的两行指定计算机的主机名和网络的域名。您指定的主机名必须包含您在 DOMAINNAME 行中指定的域名。换句话说，不要指定一个使用与 DOMAINNAME 行中所述不同域名的域名的主机名。
- 接下来的两行指定确定计算机默认网关所需的信息。默认网关是传输数据包到和来自您的计算机的计算机（或路由器）。例如，如果您的 Red Hat Linux 计算机将连接到您的 LAN，其中有一个 ISDN 路由器将 LAN 连接到 Internet，您指定 ISDN 路由器网络接口的 IP 地址作为默认网关。当您有多个网络接口时，GATEWAYDEV 很重要。如果您只有一个以太网设备，这始终应设置为 eth0。如果您有多个以太网设备（eth0、eth1 等），您必须使用连接到默认网关的接口名称。

配置完 /etc/sysconfig/network 文件后，您就可以在 /etc/sysconfig/network-scripts 目录中创建网络接口文件了。网络接口文件使用 ifcfg-interface 作为命名约定。例如，eth0 的网络接口文件名是 ifcfg-eth0。清单 7-2 显示了此文件的示例。

### 清单 7-2 /etc/sysconfig/network-scripts/ifcfg-eth0 文件

```
DEVICE=eth0
NETMASK=255.255.255.240
IPADDR=206.171.50.50
NETWORK=206.171.50.48
BROADCAST=206.171.50.63
ONBOOT=yes
```

在配置此文件中的信息之前，您必须从 ISP 处获取网络地址、网络掩码、主机上网络接口的 IP 地址以及广播地址。网络掩码和广播地址将在后面的章节中讨论。

以下是前述文件中条目的说明：

- 第一行指定设备名称。
- 第二行指定网络掩码（netmask）号码。
- 第三行指定计算机的 IP 地址。
- 第四行指定网络地址。
- 第五行指定广播地址。
- 第六行包含 ONBOOT 选项，如果您希望网络接口在启动后处于“up”（启动）状态，则应将其设置为 yes。

配置完这两个文件后，您就可以启动网络了。启动您刚刚配置的接口的最简单方法是运行以下命令：

```
/etc/sysconfig/network-scripts/ifup eth0
```

ifup 脚本以设备名称作为参数并启动它。它还为网络创建默认路由。运行此命令后，您可以使用 ifconfig 程序查看接口是否已启动并运行。要查看设备 eth0 是否已启动，请运行以下命令：

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

这里，ifconfig 报告网络接口设备 eth0 的 Internet 地址（inet addr）为 206.171.50.50，广播地址（Bcast）为 206.171.50.63，网络掩码为 255.255.255.240。其余信息显示此接口迄今接收了多少数据包（RX packets）、发送了多少数据包（TX packets）、迄今发生了多少种不同类型的错误、此设备使用哪个中断地址线、使用的 I/O 地址基址是什么等等。

您可以在不带任何参数的情况下运行 ifconfig 以获取所有已启动网络设备的完整列表。请注意，ifup 脚本使用 ifconfig 启动接口。例如，

```
ifconfig eth0 206.171.50.50 netmask 255.255.255.240 \
broadcast 206.171.50.63
```

启动 eth0 并使用 IP 地址 206.171.50.50。您也可以使用 ifconfig 命令快速关闭接口。例如，以下命令关闭 eth0 接口：

```
ifconfig eth0 down
```

接口启动并运行后，尝试联系网络中的一台计算机。您可以使用 ping IP 地址 命令查看新的接口是否可用于联系同一网络上的主机。

如果在安装期间 /etc/resolv.conf 文件未正确设置，您将无法使用主机名 ping 主机。/etc/resolv.conf 文件如下所示：

```
search nitec.com
nameserver 206.171.50.50
```

这是在 Red Hat Linux 安装期间设置的。如果您为名称服务器指定了无效的 IP 地址，您的计算机将无法联系名称服务器。因此，如果您的网络接口已启动但无法使用主机名 ping 主机，请尝试使用主机的 IP 地址（实际上是网络接口地址）。如果您可以 ping 网络上的其他主机，则您的接口已正确设置；只需通过修复名称服务器的 IP 地址来更正 name-server 行即可。

但是，如果您无法使用 IP 地址或主机名 ping 主机，则可能存在路由问题。如果您没有使用前面所示的 ifup 脚本，而是使用 ifconfig 启动接口，则需要手动创建到网络的默认路由和默认网关。要为网络创建默认路由，请按如下方式使用 route 命令：

```
route add -net network address netmask device
```

例如，要为 206.171.50.48 网络创建默认路由，网络掩码为 255.255.255.240，接口为 eth0，我可以运行：

```
route add -net 206.171.50.48 255.255.255.240 eth0
```

要设置默认网关，您可以按如下方式运行 route 命令：

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

在此阶段，使用 ping 程序 ping 网络内部和外部的主机。如果成功，则您的网络已启动。如果仍然没有收到 ping 尝试的任何回复，请返回本节开头并确保已按照建议执行了所有步骤。
