
如图 12-2 所示，您需要在 PC 中安装以太网卡。这些卡应具有 ThinWire 连接器，称为 *BNC 连接器*。您还需要 ThinWire 电缆段（技术上称为具有 50 欧姆阻抗的 RG-58 薄同轴电缆）。对于每个以太网卡的 BNC 连接器，您需要一个 BNC *T 连接器*（之所以这样称呼是因为连接器看起来像 T 字形），并且您需要两个 50 欧姆终端，分别用于以太网网络的两个端点。然后，您只需按照图 12-2 所示的方式连接部件，即可完成自己的以太网 LAN。我用这种方法在家用办公室中连接了几台 PC 和一台工作站。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_166_0.png)

## 图 12-2
*一个小型 ThinWire 以太网 LAN*

ThinWire 设置起来很容易，但用这种方式连接大量 PC 并不是很方便。一个问题是，电缆的任何断裂都会导致整个网络崩溃。

您还可以使用具有一个 10Base2 端口和多个 10BaseT 端口的集线器将 10Base2 LAN 与 10BaseT LAN 连接起来。

您不能简单地用一根电缆将两个以太网卡连接起来。请记住，即使您只是在 10Base2 LAN 上连接两台 PC，也必须使用 BNC T 连接器和 50 欧姆终端。

当您从本书的附带 CD-ROM 在连接到以太网 LAN 的 PC 上安装 Red Hat Linux 时，只要安装程序成功检测到以太网卡，安装程序就应为该卡安装适当的驱动程序。否则，您可以按照第 4 节所述以专家模式安装 Linux。

正确安装后，Linux 在每次启动时都应加载以太网卡的驱动程序。要验证以太网驱动程序是否已加载，请按如下方式使用 dmesg 命令：

```
dmesg | grep eth0
```

此命令会在启动消息中搜索包含字符串 eth0 的任何行。（正如本节后面所讨论的，eth0 是 Linux 系统中第一块以太网卡的设备名称。）我的 PC 上安装了 3Com 3C503 以太网卡。当我在系统上输入 dmesg | grep eth0 时，得到以下输出：

```
eth0: 3c503 at i/o base 0x300, node 02 60 8c 8e c6 a9, using internal xcvr.
eth0: 3c503-PIO, 16kB RAM, using programmed I/O (REJUMPER for SHARED MEMORY).
```

您应该会看到类似的内容，显示以太网卡的名称和其他相关参数。如果 dmesg 命令未显示任何以太网设备，请键入 grep eth0 /var/log/messages 以在存储在 /var/log/messages 文件中的启动消息中查找 eth0 设备名称。

## 配置 TCP/IP 网络

在 Red Hat Linux 中，TCP/IP 设置与其他几乎所有内容一样，是准备一批配置文件（可以用任何文本编辑器编辑的文本文件）的问题。其中大多数配置文件位于 /etc 目录中。Red Hat Linux 包含一个网络配置实用程序，可用于配置网络。首先，您需要学习如何引用网络设备。

### 学习网络设备名称

对于大多数设备，Linux 使用 /dev 目录中的文件。然而，网络设备具有在内核内部定义的名称；/dev 目录（或任何目录）中都不存在这些设备的任何文件。以下是 Linux 中常见的网络设备名称：

- lo — 回环设备。该设备有效地处理从系统发送到自身（例如，当 X 客户端与同一系统上的 X 服务器通信时）的网络数据包。
- eth0 — 第一块以太网卡。如果您有更多以太网卡，它们将获得设备名称 eth1、eth2，依此类推。
- ppp0 — 使用点对点协议（PPP）配置为与另一台计算机点对点链接的第一个串行端口。如果您有更多配置为 PPP 网络的串行端口，它们将被分配设备名称 ppp1、ppp2，依此类推。
- sl0 — 配置为使用串行线路互联网协议（SLIP）网络的第一个串行端口。SLIP 建立到 TCP/IP 网络的点对点链接。如果您使用第二个串行端口进行 SLIP，它将获得设备名称 sl1。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_168_0.png)

无论您是否有任何网络，您始终都有一个回环设备（lo）。它在无需外出到网络的情况下将数据从一个进程传递到另一个进程。事实上，只要通信进程在同一系统上，回环设备就能使网络应用程序正常工作。

如果您想查看系统上安装的网络设备名称，请以 root 身份登录并键入以下命令：

```
cat /proc/net/dev
```

此命令显示当前安装的网络设备名称，以及特定设备的发送和接收数据包数量的统计信息。

### 运行 Red Hat 的网络配置工具

在 Red Hat Linux 安装期间设置 TCP/IP 网络时，安装程序会使用您提供的信息准备所有适当的配置文件。然而，Red Hat Linux 附带了 netcfg 图形网络配置工具，您可以使用它来添加新的网络接口或更改名称服务器和主机名等信息。

要启动网络配置工具，请以 root 身份登录并在终端窗口中键入 netcfg 以启动该程序。网络配置工具会显示一个对话框，如图 12-3 所示。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_169_0.png)

## 图 12-3

*使用 netcfg 网络配置工具配置 TCP/IP 网络*

您可以通过对话框顶部的四个按钮配置网络的各个方面。单击每个按钮以探索可以添加或编辑的条目。具体来说，这些按钮使您能够执行以下操作：

- *Names.* 允许您输入系统的主机名并输入名称服务器的 IP 地址。名称服务器地址存储在 `/etc/resolv.conf` 文件中。主机名存储在 `/etc/sysconfig/network` 文件中的一个变量中。
- *Hosts.* 显示 `/etc/hosts` 文件的当前内容，并允许您添加、删除或编辑条目。该文件包含每个主机的主机名和相应的 IP 地址。
- *Interfaces.* 允许您添加新的网络接口，指定接口的 IP 地址并激活接口。这些信息存储在 `/etc/sysconfig` 目录中的各种文件中。
- *Routing.* 允许您添加静态路由（每条路由列出用于到达指定网络的网关）。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_169_1.png)

要配置网络接口，您需要为每个接口分配 IP 地址。如果您运行的是私有网络，您可以使用 192.168.0.0 到 192.168.255.255 范围内的 IP 地址。（还有其他范围的地址保留用于私有网络，但此范围应足以满足大多数需求。）例如，我使用 192.168.1.0 地址用于小型私有网络。

## 使用 TCP/IP 诊断命令

假设网络已配置，您应检查网络是否已启动并运行，以及 Red Hat Linux 系统是否已正确配置为 TCP/IP 网络。当然，您可以使用 TELNET 和 FTP 等网络应用程序来验证网络是否已启动并运行，但 Red Hat Linux 还包含许多实用程序，可帮助您监视和诊断问题。

### 检查接口

键入 /sbin/ifconfig 命令以查看当前配置的网络接口。ifconfig 命令还在系统启动期间配置网络接口（将 IP 地址与网络设备关联）。但是，如果您在没有任何命令行参数的情况下运行 ifconfig，该命令将显示有关当前网络接口的信息。以下是 ifconfig 典型调用的结果：

```
/sbin/ifconfig
eth0      Link encap:Ethernet  HWaddr 02:60:8C:8E:C6:A9
          inet addr:192.168.1.200  Bcast:192.168.1.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:3007  errors:0  dropped:0  overruns:0  frame:0
          TX packets:1140 errors:0  dropped:0  overruns:0  carrier:0
          collisions:0 txqueuelen:100
          Interrupt:5  Base address:0x300

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          UP LOOPBACK RUNNING  MTU:3924  Metric:1
          RX packets:54 errors:0 dropped:0 overruns:0 frame:0
          TX packets:54 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
```

此输出显示两个接口——回环接口（lo）和以太网卡（eth0）——当前在此系统上处于活动状态。对于每个接口，您可以看到 IP 地址，以及发送和接收数据包的统计信息。对于以太网卡，ifconfig 还报告 IRQ（显示为 Interrupt: 5）和基 I/O 端口地址（0x300）。如果 Red Hat Linux 系统的拨号 PPP 链接已启动并运行，您还会在输出中看到 ppp0 接口的项目。

### 检查 IP 路由表

另一个网络配置命令 /sbin/route，在您在没有任何命令行参数的情况下运行它时，也会提供状态信息。如果您正在
