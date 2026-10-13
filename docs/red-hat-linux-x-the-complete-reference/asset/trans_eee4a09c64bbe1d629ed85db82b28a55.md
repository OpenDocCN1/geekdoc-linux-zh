
## 虚拟专用网络

虚拟专用网络让您能够在物理网络连接（例如互联网）之上创建自己的私有逻辑网络。使用加密技术，您的私有网络传输可免受物理网络的窥探。虽然虚拟专用网络（VPN）本身没有物理连接，也不是一个实际的网络，但其发送的安全传输具有如同网络作为独立实体存在一样的效果。VPN 使用隧道技术，在像互联网这样的大型网络上的互连系统之间直接发送安全传输，而不会被拦截，并在任何一点被翻译。要实现 VPN，每个节点都必须使用相同的加密支持软件。在 Red Hat 上，您可以选择使用更新的 IPSec 工具或较旧的第三方加密 IP 封装（CIPE）工具。要使用 IPSec 设置 VPN，您可以在 redhat-config-network 中点击 IPSec 面板并创建一个新的连接。此过程在第 17 章中有详细描述。CIPE 仍可使用 Internet 配置向导进行配置，您可以在其中输入本地和远程主机的 IP 地址。

## 接口配置脚本：/etc/sysconfig/network-scripts

由 Internet 配置向导和 redhat-config-network 实现的网络配置保存在位于 /etc/sysconfig/network-scripts 目录中的接口配置脚本中（参见第 38 章）。您可以直接编辑这些脚本，修改特定参数，如之前关于无线连接所讨论的那样。接口配置文件以当前配置的网络接口的名称命名，例如第一个以太网设备的 ifcfg-eth0，或第一个 PPP 调制解调器设备的 ifcfg-ppp0。这些文件定义了 shell 变量，其中包含有关接口的信息，例如是否在启动时启动。例如，ifcfg-eth0 文件保存了 NETWORK、BROADCAST 和 IPADDR 的定义，它们被分配设备使用的网络、广播和 IP 地址。您也可以手动编辑这些接口配置文件，进行与无线连接时所做的更改。以下是使用 DHCP 地址的 ifcfg-eth0 文件示例。

/etc/sysconfig/network-scripts/ifcfg-eth0

```
DEVICE=eth0
BOOTPROTO=DHCP
HWADDR=00:00:00:EF:AF:00
ONBOOT=yes
TYPE=Ethernet
```

## 命令行 PPP 访问：wvdial

如果由于某种原因，您无法在 X Window 系统上设置调制解调器连接，您可能需要改为从命令行界面设置，而不是桌面。对于拨号 PPP 连接，您可以使用 wvdial 拨号器。wvdial 是一个智能拨号器，它不仅拨号到 ISP 服务，还执行登录操作，提供您的用户名和密码。wvdial 首先从 /etc/wvdial.conf 文件加载其配置。在这里，您可以放置调制解调器和账户信息，包括调制解调器速度和串行设备，以及 ISP 电话号码、用户名和密码。wvdial.conf 文件按节组织，以方括号括起来的节标签开头。一个节保存为不同参数分配值的变量，例如 username = chris。默认节保存由其他节继承的默认值，因此您无需重复它们。表 5-2 列出了 wvdial 变量。

表 5-2：wvdial 的变量

| 变量 | 描述 |
|---|---|
| Inherits | 显式地从指定的节继承。默认情况下，节从 [Dialer Defaults] 节继承。 |
| Modem | wvdial 应用作调制解调器的设备。默认值为 /dev/modem。 |
| Baud | wvdial 与调制解调器通信的速度。默认值为 57,600 波特。 |
| Init1 ... Init9 | 指定调制解调器使用的初始化字符串。wvdial 最多可使用 9 个。Init1 的默认值为 "ATZ"。 |
| Phone | wvdial 要拨号的电话号码。 |
| Area Code | 指定区号（如有）。 |
| Dial Prefix | 指定所需的拨号前缀，例如 70 以禁用呼叫等待或 9 以获取外线。 |
| Dial Command | 指定拨号操作。默认值为 "ATDT"。 |
| Login | 指定您在 ISP 使用的用户名。 |
| Login Prompt | 如果您的 ISP 有不寻常的登录提示，可在此指定。 |
| Password | 指定您在 ISP 使用的密码。 |
| Password Prompt | 如果您的 ISP 有不寻常的密码提示，可在此指定。 |
| Force Address | 指定要使用的静态 IP 地址（适用于向用户提供静态 IP 地址的 ISP）。 |
| Remote Name | 对于 PAP 或 CHAP 认证，您可能需要将其更改为 ISP 的认证名称。默认值是 *。 |
| Carrier Check | 将此选项设置为 No 会禁用调制解调器的载波检查。用于报告载波线路始终处于断开状态的调制解调器。 |
| Stupid Mode | 在 Stupid Mode 模式下，wvdial 不会尝试解释终端服务器的任何提示，并在调制解调器连接后启动 pppd。 |
| Auto Reconnect | 如果启用，当另一方随机断开连接时，wvdial 会尝试自动重新建立连接。此选项默认开启。 |

您可以使用 wvdialconf 实用程序自动为您创建一个默认的 wvdial.conf 文件。wvdialconf 将检测您的调制解调器并为基本功能设置默认值。然后您可以编辑 wvdial.conf 文件并使用您的 ISP 拨号信息修改 Phone、Username 和 Password 条目。删除前面的分号（;）以取消注释该条目。任何以分号开头的行都将被忽略为注释。

```
$ wvdialconf
```

您还可以创建一个命名拨号器，例如以下示例中的 myisp。如果您登录到不同的 ISP，这很有帮助。以下示例显示了 /etc/wvdial.conf 文件：

/etc/wvdial.conf
[Modem0]

Modem = /dev/ttyS0
Baud = 57600
Init1 = ATZ
SetVolume = 0
Dial Command = ATDT

[Dialer Defaults]
Modem = /dev/ttyS0
Baud = 57600
Init1 = ATZ
SetVolume = 0
Dial Command = ATDT

[Dialer myisp]
Username = chris
Password = mypassword
Modem = /dev/ttyS0
Phone = 555-5555
Area Code = 555
Baud = 57600
StupidMode = 0

要启动 wvdial，输入命令 wvdial，然后它会从 /etc/wvdial.conf 文件读取连接配置信息。wvdial 拨号 ISP 并启动 PPP 连接，在请求时提供您的用户名和密码。

```
$ wvdial
```

您可以在 /etc/wvdial.conf 文件中为任意数量的连接设置连接配置。要选择一个，请将其标签作为参数传递给 wvdial 命令，如下所示：

```
$ wvdial myisp
```

![](img/32a48d8db4c23e6e2eb70d1e5034c976_97_0.png)

## ABC Amber CHM Converter Trial version

请注册以移除此横幅。

http://www.processestext.com/abcchm.html

## 无线工具

为了避免为每种型号的无线设备提供不同的配置选项，目前大多数无线设备都支持 Wireless Extensions。这些扩展提供了一种标准格式来配置所有无线设备。使用相同的配置选项集，您可以配置任何支持 Wireless Extensions 的无线设备。Wireless Tools 包是一组安装在 Linux 系统上用于无线设备的网络配置和报告工具。它们目前作为 Linux Wireless Extension 和 Wireless Tools 项目的一部分得到支持和开发，这是一个由 Hewlett-Packard 维护的开源项目。

Wireless Tools 由此处列出的配置和报告工具组成：

| 工具 | 描述 |
|------|-------------|
| iwconfig | 为大多数无线设备设置基本无线配置选项 |
| iwlist | 显示设备的当前状态信息 |
| iwspy | 设置无线网络中的 IP 地址列表并检查其连接质量 |
| iwpriv | 访问特定设备的配置选项 |

无线局域网设备将具有与以太网卡一样的以太网名称。适当的模块将自动加载，其别名列在 /etc/modules.conf 文件中（参见第 32 章）。

### iwconfig

iwconfig 命令的工作方式类似于 ifconfig，用于配置网络连接。它是 Internet 连接向导和 redhat-config-network 用于配置无线卡的工具。或者，您可以直接在命令行上运行 iwconfig，指定某些参数。添加的参数让您设置无线特定功能，例如网络名称（nwid）、卡使用的频率或信道（freq 或 channel）以及传输的比特率（rate）。请参阅 iwconfig 手册页以获取完整接受的参数列表。一些常用的参数列在表 5-3 中。

表 5-3：常用参数

| 参数 | 描述 |
|-----------|-------------|
| essid | 网络名称 |
| freq | 连接的频率 |
| channel | 使用的信道 |
| nwid or domain | 网络 ID 或域 |
| mode | 设备使用的操作模式，例如 ad hoc、managed 或 auto。Ad Hoc = 无接入点的单个单元，Managed = 具有多个接入点并支持漫游的网络，Master = 节点是接入点，Repeater = 节点将数据包转发给其他节点，Secondary = 备份主节点或中继器，Monitor = 仅接收数据包 |
| sens | 灵敏度，可接收数据的最低信号电平 |
| key or enc | 使用的加密密钥 |
| frag | 将数据包切割成更小片段以提高传输质量 |
| bit or rate | 比特传输速度。auto 选项会在嘈杂信道上自动回退到更低速率 |

