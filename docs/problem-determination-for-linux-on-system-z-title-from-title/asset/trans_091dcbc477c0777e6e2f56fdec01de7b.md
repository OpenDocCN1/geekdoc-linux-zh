
## 4.2.2 Linux 下网络接口检测与激活流程

图 4-4 概述了 System z 上 Linux 的网络接口检测流程。热插拔（hotplug）或冷插拔（coldplug）脚本确保以正确的选项加载正确的模块。然后分配接口名称。一旦接口名称分配完毕，系统将读取相应的配置文件并配置网络参数。

![](img/f332344337ca8bf6846cb313a66ee0b3_131_0.png)

图 4-4 Linux 网络接口检测与激活流程

第 117 页的图 4-5 展示了系统启动时网络接口检测的时间顺序。如图所示，冷插拔系统调用 `hwup` 命令来启动设备。通常，每个网络接口会关联三个接口，而由 `ccwgroup.agent` 负责将这些设备组成一个接口并分配接口名称。一旦接口名称分配完毕，网络脚本将为接口分配 IP 地址及其他参数。根据配置情况，网络接口可能默认启动，也可能需要手动干预才能启动。

![](img/f332344337ca8bf6846cb313a66ee0b3_132_0.png)

图 4-5 Linux 网络接口检测顺序

第 118 页的图 4-6 展示了 Linux 系统在检测并启用网络接口时生成的示例启动消息。消息的上半部分表明 `qdio` 和 `qeth` 模块已加载到内存中。这些模块是 System z 上的 Linux 系统以 QDIO 模式与网络设备通信所必需的。接下来的行显示了检测到设备的详细信息。在第 118 页的图 4-6 中，从上往下数的第四行表明设备地址为 0.0.02dc、0.0.02dd 和 0.0.02de。同一行消息中的 OSD 表示 OSA 卡片配置为 QDIO 模式。随后的行显示了 MAC 地址、接口名称以及在该卡片上启用的功能列表。

```
load module
qeth: loading QETH base support version 2.3(Revision: 1.79.2.10.5)Revision: 1.37.9)Revision: 1.25.2.2.9)
qeth: loading qeth S/390 OSA-Express driver (SRevision: 1.77.2.73.8)Revision: 1.98.2.33.8)Revision: 1.77.2.9.5)Revision: 1.8.2.2.5)Revision: 1.7.2.3.5)Revision: 1.5.2.7.5)Revision: 1.19.2.18.5 IPv6 :VLAN)
qeth: Device 0.0.02dc0.00d0.00d2e is a QSD Express card (level: 0657)
with link type OSD_1000 (portname: )
qeth: Error in registering MAC address on device 0.0.02dc: <200s
qeth: Device 0.0.05a0.00.05a0.00.05a6 is a GuestLAN QDIO card (level: V52D)
with link type GuestLAN QDIO (portname: )
qeth: Hardware IP fragmentation not supported on eth1
qeth: VLAN enabled
qeth: Multicast enabled
qeth: IPv6 enabled
qeth: Broadcast enabled
qeth: Using SW checksuming on eth1.
qeth: Outbound TSO not supported on eth1
NET: Registered protocol family 17
qeth: MAC address 02:00:00:16:31:89 successfully registered on device eth0
```

图 4-6 System z 上 Linux 中与网络接口检测相关的启动消息

图 4-7 指示了与第三层配置相关的启动消息，以及第二层配置的消息。

![](img/f332344337ca8bf6846cb313a66ee0b3_134_0.png)

图 4-7 与网络第三层和第二层配置相关的启动消息

## 4.2.3 网络接口及其接口名称

在拥有多个网络接口的系统中，分配给 OSA 设备的接口名称在 Linux 系统重启后可能不一致。这是因为热插拔事件是异步的，多个驱动程序会并行初始化其设备。接口名称的这种不一致性可能会导致某些中间件（如 Oracle®）出现问题。此外，SNMP 和 Linux 监控工具 `sar` 也可能受到此问题的影响。

图 4-8 说明了热插拔事件的异步特性。如图所示，设备 3333 在设备 222 之前配置，因此它被分配了接口名称 eth1，而不是预期的 eth2。设备 2222 现在是 eth2。

![](img/f332344337ca8bf6846cb313a66ee0b3_135_0.png)

图 4-8 异步热插拔事件和不一致的接口命名

为避免此问题，可以通过编辑 `/etc/sysconfig/hotplug` 并添加以下条目来对网络接口的热插拔进行排队：

```
HOTPLUG_PCI_QUEUE_NIC_EVENTS=yes
```

另一种解决方案是使用 `udev`，并在文件 `/etc/udev/rule.d/30-net_persistent_names.rules` 中建立设备地址与接口名称之间的连接。示例 4-1 展示了如何将 eth6 永久分配给 0.0.05a2。

### 示例 4-1 将接口名称 eth6 永久分配给设备 0.0.05a2

```
SUBSYSTEM=="net", ACTION=="add", ENV{PHYSDEVPATH}=="*0.0.05a2",
IMPORT="/lib/udev/rename_netiface %k eth6"
```

当使用信道捆绑（channel bonding）时，这个问题不会发生，因为信道捆绑不使用热插拔。因此，设备名称在 Linux 系统重启后保持不变。

## 4.2.4 网络配置文件概述

在本节中，我们将快速浏览在 System z 上运行的 Linux 系统中网络设备的一些重要配置文件。如前所述，本文以 SuSE Linux Enterprise Server 的文件作为示例。

### /etc/sysconfig/hardware/hwcfg-qeth-ccw-0.0.xxxx 文件

该文件由 `hwup` 和 `hwdown` 命令引用。图 4-9 展示了一个示例 hwcfg-qeth-ccw-0.0.xxxx 文件。对于系统中的每个 OSA 设备，都会有一个唯一的 hwcfg-qeth 文件。在此情况下，设备为 0.0.02d4，因此确切的文件名为 hwcfg-qeth-ccw-0.0.02d4。

![](img/f332344337ca8bf6846cb313a66ee0b3_136_0.png)

图 4-9 网络设备在 /etc/sysconfig/hardware/hwcfg-qeth-ccw-xx 中定义

### /etc/sysconfig/network/ifcfg-qeth-ccw-0.0.xxxx 文件

此配置文件由 `ifup` 和 `ifdown` 命令使用。第 122 页的图 4-10 展示了一个示例 ifcfg-qeth-ccw-0.0.xxxx 文件。对于系统中的每个 OSA 设备，都会有一个唯一的 ifcfg-qeth 文件。在此情况下，设备为 0.0.02dc，因此确切的文件名为 ifcfg-qeth-bus-ccw-0.0.02dc。IP 地址、子网掩码、本地 MAC 地址、MTU、自动启动（STARTMODE）等都在此文件中配置。当 STARTMODE=onboot 时，接口在系统启动期间会自动激活。

![](img/f332344337ca8bf6846cb313a66ee0b3_137_0.png)

图 4-10 IP 地址在 /etc/sysconfig/network/ifcfg-qeth-bus-ccw-xxx 中配置

### /etc/sysconfig/network/routes 文件

此文件由 `ifup` 和 `ifdown` 命令使用。该文件用于配置静态网络路由。图 4-11 展示了一个示例网络路由文件。该文件的格式为：目标网络（在此情况下为 192.168.30.0）、下一跳（在此情况下为 172.16.3.131）、子网掩码（255.255.255.0）以及接口名称（在此情况下为 qeth-bus-ccw-0.005a4）。图 4-11 中显示的第二行是一个特殊条目，定义默认网关。关键字 `default` 将其标识为默认网关。两个减号（- -）表示它们假定使用默认值。

![](img/f332344337ca8bf6846cb313a66ee0b3_137_1.png)

图 4-11 网络路由在 /etc/sysconfig/network/routes 中配置

## 4.3 网络故障诊断

在快速介绍了 System z 上 Linux 的常见网络选项以及 Linux 下的网络接口检测和配置之后，本节将讨论网络故障诊断。前两节应作为本节的理论基础。

网络问题大致可分为两类：

-   与网络通信相关的问题
-   与网络性能相关的问题

与网络通信相关的问题将在本章中详细讨论。第 5 章“第 163 页的性能故障诊断”专门介绍 System z 上 Linux 的性能故障诊断，同时也讨论了网络性能问题。

### 4.3.1 与网络通信相关的问题

通信涉及多方。计算机系统也是如此。当计算机系统之间交换数据或消息时，我们说它们在进行通信。当这种消息交换中断时，我们说存在通信问题。因此，在高层级上，系统中的网络通信问题可以是该系统的本地问题，也可以是系统外部的问题（即本地机器网络运行正常）。在我们的讨论中，我们假设本地系统是运行在 System z 服务器上的 Linux 系统，并且我们正尝试从该系统与其他系统进行通信。

#### 本地机器上的故障诊断

当系统无法与其他系统通信时，我们需要问一些逻辑性的问题。你能与网络上的任何系统通信吗？在问题发生之前我们对系统做了哪些更改？我们能与部分系统通信吗？错误日志中是否有任何与问题相关的信息？我们将很快逐一查看这些问题。

#### System z 上 Linux 的网络通信层

第 124 页的图 4-12 展示了 System z 上 Linux 的网络通信层。这样的层次结构对于缩小问题范围非常有用。最底层是硬件（HW）层。OSA 设备属于此层。下一层是虚拟机（VM）层，z/VM 级别进行的虚拟化（例如 VSWITCH）属于此层。下一层，QDIO 和 QETH，代表设备驱动程序。MAC 地址表示

