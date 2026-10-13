
`ifconfig`

你会看到两个不同接口的列表，如下代码所示；如果你配置了 PPP，则会有三个接口。`ifconfig` 命令告诉 Linux 内核你有一个网络适配器，并为其分配一个 IP 地址和网络掩码。这是将你的 Linux 连接到网络的第一步：

| eth0 | Link encap:10Mbps Ethernet Hwaddr 00:A0:24:2F:30:69 inet addr:192.168.1.1 Bcast:192.168.1.255 Mask:255.255.255.0 UP BROADCAST MULTICAST MTU:1500 Metric:1 RX packets:16010 errors:18 dropped:18 overruns:23 TX packets:7075 errors:0 dropped:0 overruns:0 Interrupt:10 Base address:0x300 |
| lo | Link encap:Local Loopback inet addr:127.0.0.1 Bcast:127.255.255.255 Mask:255.255.255.0 UP BROADCAST LOOPBACK RUNNING MTU:3584 Metric:1 RX packets:115 errors:0 dropped:0 overruns:0 TX packets:115 errors:0 dropped:0 overruns:0 |

| | wireless extensions |
| eth0 | IEEE 802.11-DS ESSID:"linky" Nickname:"..."..." Mode:Ad-Hoc Frequency:2.437GHz Cell:"..." Bit Rate:11MB/s Tx-Power:15dBm Sensitivity:1/3 Retry limit:4 RTS thrloff Fragment throff Encryption key:A654-6277-A3D6-ACC3-E6ED-1C12-98 Power Management:off Link Quality:0 Signal level:0 Noise level:0 Rx invalid:0 Rx invalid crypt:0 Rx invalid ... Tx retries:0 Rx invalid misc:0 Missed ... |

需要检查的重要选项：

- **Mode（模式）：** 当连接到自适应网络（ad hoc network）时，你需要将此值设置为 Ad-Hoc。（有关此方法的更多信息，请参阅第 7 章。）你可以使用任何在某些情况下对自适应网络有效的值；然而，详细描述这些情况超出了本书的范围，请在必要时使用 Ad-hoc 模式。
- **ESSID：** 你需要在连接到 ad hoc 局域网的每台机器上使用相同的名称。例如，我们网络上的每台机器都分配了 ESSID link。
- **Encryption key（加密密钥）：** 你需要在连接到你无线网络的每台机器上使用相同的加密密钥。密钥有两种类型：40 位和 128 位。40 位密钥几乎是无用的，因为黑客可以使用广泛使用的软件轻易破解它。

只要你正确设置了这些参数，并且你的电脑在局域网上其他设备的范围内，你的无线网络就能正常工作。其他参数要么是生成的，要么对于让网卡工作并不重要。

# 检查你的无线网卡 (NIC)

Linux 提供了几个工具来处理 Wi-Fi 接口。Red Hat 默认安装了 `wireless-tools` RPM 包。这些工具包括 `iwconfig`、`iwspy` 和其他实用。我们将描述如何使用 `iwconfig` 来检查你的 Wi-Fi 接口配置。

# 第 17 章：引入 Red Hat Linux 维修

以 root 身份登录，打开 GNOME 终端（更多信息请参阅第 4 章），并运行 `ifconfig` 命令。如果你的网卡配置正确，你会看到类似于示例的输出：

| | wireless extensions |
| eth0 | IEEE 802.11-DS ESSID:"linky" Nickname:"..." Mode:Ad-Hoc Frequency:2.437GHz Cell:"..." Bit Rate:11MB/s Tx-Power:15dBm Sensitivity:1/3 Retry limit:4 RTS thrloff Fragment throff Encryption key:A654-6277-A3D6-ACC3-E6ED-1C12-98 Power Management:off Link Quality:0 Signal level:0 Noise level:0 Rx invalid:0 Rx invalid crypt:0 Rx invalid ... Tx retries:0 Rx invalid misc:0 Missed ... |

需要检查的重要选项：

如果你没有看到包含 `lo`（回环接口）或 `eth0`（你的网络适配器）的行，说明你的物理连接没有设置好。回环接口不是物理设备；它用于软件的内部运行。为了让网络适配器配置，回环接口必须存在。如果回环接口不存在，输入此命令：

```
ifconfig lo 127.0.0.1
```

如果网络适配器（通常是以太网卡）不存在，输入此命令：

```
ifconfig eth0 192.168.1.1
```

由于这是 C 类网络，`ifconfig` 自动默认为 255.255.255.0。如果你有不的子掩码，你不应该输入此命令：

```
ifconfig eth0 192.168.1.1 netmask 255.255.255.0
```

输入 `ifconfig`，你应该能看到正确显示的你的网络适配器。如果不是，通过输入此命令并按回车查看手册页：

```
man ifconfig
```

你可以通过几种方式翻页文档：按空格键向前翻一页，按 Ctrl+B 向后翻，或按 Q 退出。输入 `ifconfig`，你应该看到正确显示的你的网络适配器。如果不是，通过输入此命令并按回车查看手册页：

```
man ifconfig
```

你可以通过几种方式翻页文档：按空格键向前翻一页，按 Ctrl+B 向后翻，或按 Q 退出。

## 第 17 章：请红帽 Linux 维修人员 273

下一步是确保你的网络路由配置正确。这也是一个非常容易混淆的地方。你暂时不需要在局域网（LAN）之外设置路由，但 Linux 需要知道在自己的网络上将数据包发送到哪里。输入以下命令查看路由表：

```
netstat -nr
```
