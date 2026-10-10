

FreeBSD。许多其他网卡也受 FreeBSD 支持，但未包含在 GENERIC 内核中；请参阅 /sys/i386/conf/NOTES（如第 16 章“内核配置”中“NOTES 文件和 LINT”部分所述），并重新编译内核以启用对这些网卡的支持。

> **注意**
> 请注意，受支持的以太网网卡列表变化相当频繁。设备列表位于你系统中的 GENERIC 内核配置文件 /sys/i386/conf/GENERIC 中。这将是你系统支持哪些网卡的权威来源。

表 22.1 默认（GENERIC）FreeBSD 内核支持的以太网网卡

| 设备名称 | 支持的网卡 |
|:------------|:----------------|
| **PCI 网卡** | |
| de | DEC/Intel DC21x4x (Tulip) |
| em | Intel PRO/1000 网卡千兆以太网卡 |
| txp | 3Com 3cR990 (Typhoon) |
| vx | 3Com 3c590, 3c595 (Vortex) |
| **PCI/MII 网卡** | |
| fxp | Intel EtherExpress Pro/100B (82557, 82558) |
| tx | SMC 9432TX (83c170 “EPIC”) |
| dc | DEC/Intel 21143 及各种兼容芯片 |
| pcn | AMD Am79C79x PCI 10/100 网卡 |
| r1 | RealTek 8129/8139 |
| sf | Adaptec AIC-6915 (Starfire) |
| sis | Silicon Integrated Systems SIS 900/SIS 7016 |
| ste | Sundance ST201 (D-Link DFE-550TX) |
| t1 | Texas Instruments ThunderLAN |
| vr | VIA Rhine, Rhine II |
| wb | Winbond W89C840F |
| x1 | 3Com 3c90x (Boomerang, Cyclone) |
| **ISA 网卡** | |
| ed | Novell NE1000/NE2000, 3Com 3c503, Western Digital/SMC 80xx |
| ex | Intel EtherExpress Pro/10 (82595) |
| ep | 3Com 3c509 |
| fe | Fujitsu MB86960A/MB86965A |
| lnc | Lance/PCnet 网卡 (iSolan, Novell NE2100, NE32-VL, AMD Am7990, 和 Am79C960) |
| cs | Crystal Semiconductor CS89x0 |
| sn | SMC 9000 |
| xe | Xircom PC 卡以太网 |
| **无线 (802.11) PCMCIA 网卡** | |
| wi | Lucent WaveLAN 802.11 |
| an | Aironet 4500/4800 802.11 |
| awi | BayStack 660 及其他 |

如今为 x86 硬件销售的大多数以太网网卡都是基于 PCI 的。这意味着 PCI 控制器会自动处理所有寻址，你不需要执行与 ISA 网卡相关的 IRQ/DMA/内存地址等复杂操作。不过，如果你使用的是这些较旧的网卡之一，还是有几件事需要你去做，例如通过 DOS 实用程序设置网卡的内存地址和 IRQ，并修改该网卡的设备提示。你将在本章稍后的侧边栏“与 ISA 以太网网卡打交道”中更多地了解这些适应性措施。

## 使用 sysinstall 配置网络设置

配置以太网网卡的最简单方法是使用 sysinstall。对于曾经在 Windows 或 Macintosh 机器上经历过此流程的人来说，sysinstall 的方法可能看起来很熟悉。首次要求 sysinstall 执行任何需要网络连接的操作（如进行系统的网络安装、浏览软件包以及各种其他任务）时，它会弹出网络配置窗口，你可以在其中直观地设置以太网网卡的 TCP/IP 选项。

如果你已经处于多用户模式运行中，并且不在初始系统安装过程中，可以通过运行 /stand/sysinstall，从主菜单选择“配置”（Configure），然后选择“介质”（Media）选项来轻松进入此屏幕。在此子菜单中，选择 FTP 和某个 FTP 服务器（具体是哪个并不重要；如果你正在这里操作，目的是触发网络配置过程，而不是安装任何软件）。对话框会询问“运行多用户，假设网络已配置？”选择“否”以进入网络配置屏幕；网络接口选择屏幕将打开，如图 22.1 所示。

![](img/48eec858cce7dfb89da36a4d40b7daf3_542_0.png)

网络接口选择屏幕向你展示了 FreeBSD 在你的系统中找到的接口列表。你可能会看到许多没有太多意义的选项。在该图中，你可以看到诸如 lp0（并行端口）以及各种 PPP 或 SLIP 选项，还有 gif0 和 faith0 等 IPv6 设备之类的选项。你可以忽略该屏幕上的大多数选项，因为你想要的选项很可能在顶部。本例中我们使用的是 fxp1，即 Intel EtherExpress Pro/100B PCI 网卡。

当你选择你的以太网网卡时，会弹出两个对话框：一个选项是让系统尝试使用 IPv6 自动配置网卡，另一个选项是让系统尝试使用 DHCP。对这两个问题都回答“否”。然后，你将看到可视化的网络配置屏幕，如图 22.2 所示。

![](img/48eec858cce7dfb89da36a4d40b7daf3_543_0.png)

**图 22.2** sysinstall 程序中的可视化网络配置屏幕。

此屏幕中的每个字段在窗口底部都有一个简短描述，但以下是关于它们的更多详细信息：

- **主机名**（Host）——这是主机名，即机器完全限定域名的一部分。例如，如果你的机器是 www.somewhere.com，则 Host 字段应设置为 www。

- **域名**（Domain）——这是域名的其余部分，例如 somewhere.com。对于具有命名子网的网络，这可以是复合域名，例如 cslab.ivyleague.edu。

- **IPv4 网关**（IPv4 Gateway）——这是网关路由器的 IP 地址。请使用离你的机器最近的下一跳路由器，或者你的网络管理员或 ISP 指定的网关地址。如果你通过 DSL“调制解调器”或类似设备连接到互联网，其 IP 地址（由 ISP 分配）应是你的网关。此路由器将负责传输你的机器与世界其他机器之间的任何流量。正如你在第 21 章“与 FreeBSD 进行网络通信”中学到的那样，网关路由器必须与你的 FreeBSD 机器的 IP 地址处于同一网络中，如子网掩码所定义。

- **名称服务器**（Name Server）——这是你网络中最可靠的域名服务器（DNS）的 IP 地址。如果可能，应使用由你的企业、ISP 或大学网络提供的 DNS；远程名称服务器可作为备份使用，但它们不一定可靠地服务于非本地请求。本章稍后你将学习如何根据需要分配多个名称服务器。

- **IPv4 地址**（IPv4 Address）——这是你分配给以太网网卡的 IP 地址。它需要与你的 IPv4 网关位于同一子网中，并匹配你的子网掩码。这一点在第 21 章中已有讨论。

- **子网掩码**（Netmask）——这用于确定数据包的目的地是否位于本地网络。对于 C 类网络，将字段设置为 **255.255.255.0**，这是大多数家庭配置中最常用的子网掩码。请咨询你的网络管理员以确定此数值应该是多少。

- **ifconfig 的额外选项**（Extra options to ifconfig）——除非你是想要调整接口卡性能的高级用户，否则你很可能不需要在此处填入任何内容。你在此处填入的任何内容，例如指定特定的介质类型或双工模式，都会添加到 sysinstall 在后台发出的 ifconfig 命令行之中。你将在本章稍后的“使用 ifconfig 应用网络设置”部分更多地了解此命令。

设置完所有这些选项后，选择“确定”（OK）。网络设置将即时应用于网卡。你在 sysinstall 中正在做的事情将继续进行——在本例中，sysinstall 将连接到你所选的 FTP 服务器。如果网络配置不成功，你输入的网络设置可能存在問題，你需要返回并排查你的设置。如果你在企业网络中，请让你的网络管理员为你提供正确的设置。

如果你正在安装 FreeBSD，此流程以非常相似的方式工作。在安装过程的早期，会向你展示此配置屏幕。如果你正在进行网络安装，它将使用这些设置来下载系统发行版。

## 与 ISA 以太网网卡打交道

大多数 PCI 以太网网卡都非常稳定，无故障。你真正需要做的，特别是如果你拥有一块受 GENERIC 内核支持的常用网卡之一，就是插上它，启动机器，并观察内核在启动过程中识别网卡：

```
fxp0: <Intel PLC 10/100 Ethernet> port 0xe000-0xe0ff mem
0xff8fe000-0xff8fefff irq 11 at device 8.0 on pci1
fxp0: Ethernet address 00:00:b7:c7:74:f1
fxp1: <Intel Pro 10/100B/100+ Ethernet> port 0xdf00-0xdf3f mem
0xff700000-0xff7fffff,0xff8f0000-0xff8fffff irq 11 at
device 9.0 on pci1
fxp1: Ethernet address 00:d0:b7:bd:5d:13
```

