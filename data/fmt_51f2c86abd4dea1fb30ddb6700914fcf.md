
如果你想弹出 CD-ROM 并加载新的光盘，必须通过 `umount` 命令卸载 CD-ROM 文件系统。输入 `umount /mnt/cdrom`。只有在当前没有进程正在访问它且没有用户将 CD-ROM 文件系统设置为默认目录时，你才能卸载 CD-ROM。如果你在响应 `umount` 命令时收到“device busy”（设备忙）的错误消息，你应该更改当前目录（例如，输入 `cd /`），然后重试 `umount` 命令。然后你就可以通过 CD-ROM 的弹出按钮将其弹出。

## 特定 CD-ROM 驱动器信息

以下章节总结了某些常用设备驱动程序的特定信息。这些信息包含了设备文件的名称（例如用于带有 Sound Blaster Pro 接口的 CD-ROM 驱动器的 `/dev/sbd`）、驱动程序接受的任何启动参数以及驱动程序的任何独特功能。更多信息请阅读涵盖你的 CD-ROM 接口的章节。

### SCSI CD-ROM 驱动程序

`scd` 驱动支持通过 SCSI 卡连接到 PC 的多个 CD-ROM 驱动器。`scd` 驱动具有以下特征：

- 允许多个 CD-ROM 驱动器：是

- 支持可加载模块：是

- 可以读取音频帧：否

- 执行自动探测：是

- 设备文件名：`/dev/scd0`，主设备号 = 11

- 设备配置文件：`/dev/scd0`

- 配置时的内核选项：SCSI

- 文档名称：SCSI

`scd` 驱动支持通过 SCSI 卡连接到 PC 的多个 CD-ROM 驱动器。SCSI 驱动程序支持 `/dev/scd0`。SCSI 设备名称包括 `/dev/scd1`、`/dev/scd2`。

### IDE CD-ROM 驱动程序

IDE 驱动支持通过 IDE 接口连接到 PC 的多个 CD-ROM 驱动器。IDE 驱动通过自动探测并将 `/dev/hda`、`/dev/hdb`、`/dev/hdc`、`/dev/hdd` 分配设备。EIDE 控制器上辅助 IDE 接口上的 ATAPI CD-ROM 驱动器。IDE 驱动程序具有以下特征：

- 允许多个 CD-ROM 驱动器：是

- 支持可加载模块：是

- 可以读取音频帧：否

- 执行自动探测：是

- 设备文件名：`/dev/hda`，主设备号 = 3

- 设备配置文件：`/dev/hda`

- 配置时的内核选项：IDE

- 文档名称：IDE

IDE 驱动程序支持通过 IDE 接口连接到 PC 的多个 CD-ROM 驱动器。IDE 驱动通过自动探测并将 `/dev/hda`、`/dev/hdb`、`/dev/hdc`、`/dev/hdd` 分配设备。

### Sound Blaster CD-ROM 驱动程序

`sbpcd` 驱动支持通过 Sound Blaster Pro 卡连接到 PC 的多个 CD-ROM 驱动器。`sbpcd` 驱动具有以下特征：

- 允许多个 CD-ROM 驱动器：是

- 支持可加载模块：是

- 可以读取音频帧：否

- 执行自动探测：是

- 设备文件名：`/dev/sbpcd`，主设备号 = 11

- 设备配置文件：`/dev/sbpcd`

- 配置时的内核选项：Sound Blaster

- 文档名称：Sound Blaster

## Red Hat Linux 7.3 秘密

此驱动程序接受以下启动参数：

`sonycd535=IOPORT`

`IOPORT` 是十六进制格式的设备 I/O 端口地址（例如 `0x320`）。

## atzcd 驱动

`atzcd` 驱动支持使用接口的 Aztech CD268-01A、Orchid CD-3110 以及 Okano/Wearnas CDD110 CD-ROM 驱动器。这些厂商的其他 CD-ROM 驱动器（如 Aztech CD269）具有 IDE 接口；这些驱动器必须使用 IDE 驱动。`atzcd` 驱动仅用于专用接口。

`atzcd` 驱动具有以下特性：

- 允许多个 CD-ROM 驱动器：否

- 支持可加载模块：是

- 能否读取音频帧：否

- 是否自动探测：否

- 设备文件名称：`/dev/atzcd`，主设备号 = 29

- 设备配置文件：`/usr/src/linux/drivers/cdrom/cdrom.h`

- 制作配置时的内核选项：是否支持 atzcd/Orchid/Okano/Wearnas/TXC/Cyrom？

- README 文件名称：`/usr/src/linux/Documentation/cdrom/atzcd`

此驱动程序接受以下启动参数：

`IOPORT` 是十六进制格式的设备 I/O 端口地址（例如 `0x340`）。

## mcd 驱动

`mcd` 驱动支持带有专用 Mitsumi 接口的 Mitsumi CRMC-LU005S 和 CRMC-FX001 CD-ROM 驱动器。许多新 PC 使用 Mitsumi CD-ROM 驱动器但并不使用专用接口；目前的趋势是使用带有 IDE（ATAPI）接口的 Mitsumi 驱动器。因此，在选择 `mcd` 驱动作为 CD-ROM 驱动之前，你应该仔细检查。如果你的 PC 有 Mitsumi CD-ROM 驱动器，它更有可能是一个 ATAPI 驱动，而不是具有专用 Mitsumi 接口的驱动。

`mcd` 驱动具有以下特性：

- 允许多个 CD-ROM 驱动器：否

- 支持可加载模块：是

- 能否读取音频帧：否

- 是否自动探测：否

- 设备文件名称：`/dev/mcd`，主设备号 = 23

- 设备配置文件：`/usr/src/linux/drivers/cdrom/mcd.h`

- 制作配置时的内核选项：是否支持 Mitsumi（标准）[no XA/Multisession] CDROM？

- README 文件名称：`/usr/src/linux/Documentation/cdrom/mcd`

## 附录 C：CD-ROM 驱动器 939

此驱动程序接受以下启动参数：

`mcd=IOPORT,IRQ`

`IOPORT` 是十六进制格式的 Mitsumi 接口卡的 I/O 端口地址（例如 `0x300`）。`IRQ` 是该卡使用的中断请求号（例如 `11`）。

Red Hat Linux 还带有另一个 Mitsumi 驱动 `mcdx`，它提供了额外功能。要包含此驱动程序，你应该在内核配置期间对以下问题回答 yes：

`Mitsumi [XA/MultiSession] CDROM support`

## cdu31a 驱动

`cdu31a` 驱动支持带有专用接口的 Sony CDU31A 和 CDU33A CD-ROM 驱动器。此驱动具有以下特性：

- 允许多个 CD-ROM 驱动器：否

- 支持可加载模块：是

- 能否读取音频帧：是

- 是否自动探测：否

设备文件名称：`/dev/cdu31a`，主设备号 = 15

设备配置文件：`/usr/src/linux/drivers/cdrom/cdu31a.h`

制作配置时的内核选项：是否支持 CDU31A/CDU33A CDROM？

README 文件名称：`/usr/src/linux/Documentation/cdrom/cdu31a`

`cdu31a` 驱动接受以下形式的内核命令：

`cdu31a=IOPORT,IRQ[PAS]`

`IOPORT` 是十六进制格式的接口卡的 I/O 端口地址（例如 `0x300`）。`IRQ` 是该卡使用的中断请求号（例如 `11`）。如果驱动程序连接到 Pro-Audio Spectrum 16 声卡，你必须指定可选的第三个参数（方括号所示）`PAS`。

## 附录 D

### 以太网卡

以太网是局域网（LAN）物理层传输机制的良好选择，原因如下：

- 以太网是经过验证的技术（自 20 世纪 80 年代一直在使用）。

- 以太网提供良好的数据传输率：通常为每秒100 万比特（10 Mbps），尽管现在有了 100 Mbps 以太网和千兆以太网（1000 Mbps）。

- 以太网硬件成本较低（PC 以太网卡售价 20 美元）。

通常，Linux 有效支持廉价硬件，以太网例外。本附录描述了以太网 LAN 的设置并列出了 Linux 支持的太网卡。

### 以太网基础

以太网是在连接到单个电缆的两个或计算机之间移动数据包的标准方法。（较大的网络通过网关连接多个段来构建。）由于使用了单线，发送和接收数据必须使用协议，因为在任何时候电缆上只能存在一个数据包。以太网 LAN 使用称为载波监听多接入/冲突检测（CSMA/CD）的数据传输协议，以确保多台计算机共享单个传输电缆。嵌入计算机中的以太网控制器遵循 CSMA/CD 协议传输和接收以太网数据包。

CSMA/CD 协议的思想类似于你在聚会中对话的方式。你倾听停顿（载波监听），并在没有人说话时说话。如果你和另一个人同时开始说话，你们都意识到了问题（冲突检测）并停顿一下；然后你们中的一个重新开始。正如你经验所知，一切都会解决。

在以太网 LAN 中，每个以太网控制器都会检查电缆信号——这就是载波感应部分。如果信号电较低，控制器在电缆上发送其数据包；数据包包含发送者和目标接收者的信息。LAN 上所有的以太网控制器都监听

## 红帽 Linux 7.3 秘密

信号，意味着接收者收到了数据包。如果两个控制器同时发送数据包，电缆中的信号电平将超过阈值，控制器就会知道发生了冲突（两个数据包同时被发送出去）。两个控制器在重新发送数据包之前都会等待随机的时间。

以太网是由罗伯特·梅特卡菲（Robert M. Metcalfe）在20世纪70年代初在施罗克斯帕洛托研究中心（PARC）发明的。在80年代，以太网通过三家公司的合作实现了标准化：数字设备公司（DEC）、英特尔（Intel）和西罗克斯（Xerox）。使用公司名称的首字母缩写，以太网标准被称为 DI 标准。后来，DI 标准被包含在由电气与电子工程师学会（IEEE）开发的 802 系列标准中。最终的规范正式名为 IEEE 802.3 CSMA/CD，但人们继续称之为以太网。

以太网以包（也称为帧）的形式发送数据，其标准格式由以下顺序组件组成：

- 8 字节前导码

- 6 字节目的地址

- 6 字节源地址

- 2 字节数据字段长度

- 46 到 1,500 字节数据字段

- 4 字节帧校验序列（用于错误检查）

你不需要过多了解以太网包的内部结构，只需注意 6 字节的源地址和目的地址。每个以太网控制器都有一个唯一的 6 字节（48 位）地址。在物理层，数据包必须使用这些 6 字节地址进行编号。

### 地址解析协议

在以太网局域网中，只有当两个以太网控制器彼此对方的 6 字节物理以太网地址时才能通信。你可能好奇 IP 地址是如何映射到物理地址的。这个问题通过地址解析协议（ARP）解决，它规定了如何获取与 IP 地址对应的物理地址。本质上，当数据包发送到一个 IP 地址时，TCP/IP 协议使用 ARP 来查找目的地的物理地址。

当数据包针对的是网络外部的 IP 地址时，该数据包会被发送到在你网络上物理存在的网关。因此，该网关可以对物理地址的 ARP 请求做出响应。

### 以太网电缆

原始的以太网使用直径近半英寸的粗同轴电缆。那种布线被称为厚线（thickwire）或粗以太网（thick Ethernet），尽管 IEEE 802.3 标准称之为 10Base5。该标记意味着几层意思：数据传输速率为每秒 10 兆比特（10 Mbps）；传输是基带的（这仅意味着电缆的信号容量专门用于传输以太网包）；且电缆总长度不超过 500 米。厚线价格昂贵，电缆相当笨重。

如今，其他两种形式以太网布线更流行。粗以太网线的第一种替代方案是细线（thinwire），或 10Base2，它使用纤细柔性的同轴电缆。一个细线段最长为 185 米。另一种较新的替代方案是基于非屏蔽双绞线（UTP）以太网，被称为 10BaseT。

要建立 10BaseT 以太网，你需要一个以太网集线器——一个带有 RJ-45 端口的硬件盒。你通过从每台 PC 的以太网卡连接到此集线器的双绞线（通常是 5 类，或 Cat5 线）来构建网络。你可以花费约 50 美元买到的 4 口 10BaseT 集线器。图 D-1 显示了一个典型的小型 10BaseT 以太网局域网，你可能会在小型办公室或家里设置。

图 D-1：使用集线器的 10BaseT 以太网局域网

细线具有一个特性，使其对于拥有多个 PC 的小型办公室或家庭办公室很有吸引力。你可以将细线缆从一台 PC 连接到另一台 PC，并构建如图 D-2 所示的小型以太网。**图 D-2：构建细线以太网局域网**

如图 D-2 所示，你需要以太网卡来构建细线以太网局域网。PC 应该具有 BNC 连接器，还需要细线缆（技术上称为 RG-58 同轴电缆，阻抗为 50 欧姆）。对于每个以太网卡的 BNC 连接器，你需要 BNC T 型头（看起来像一个 T 型），即使你只在 10Base2 局域网上连接两台 PC。你还可以使用具有 10Base2 和 10BaseT 端口的集线器连接 10Base2 局域网。一个问题是电缆的任何中断都会导致整个网络中断。

### 支持的以太网卡

要建立以太网局域网，每台 PC 需要一个以太网卡。Linux 支持多种以太网卡。表 D-1 列出了支持的以太网卡及其驱动程序。

#### 表 D-1 以太网卡及其 Linux 驱动

| 以太网卡 | 驱动名称 |
| :--- | :--- |
| 3Com 3501* (过时且慢) | `3c501` |
| 3Com Etherlink II, 3503, 3503 (16位) | `3c503` and `8390` |
| 3Com Etherlink Plus 3505* | `3c505` |
| 3Com Etherlink-13507* | `3c507` |
| 3Com Etherlink III, 3509 / 3509B (ISA) | `3c509` |
| 3Com 3515 Fast Ethercard (ISA) | `3c515` |
| 3Com 3523* | `3c523` |
| 3Com 3529 | `3c509` |
| 3Com 3579 (EISA) | `3c509` |
| 3Com 3562 PCMCIA 卡 | `3c589` |
| 3Com 3589*/3589B* PCMCIA 卡 | `3c589` |
| 3Com Etherlink III Vortex (3590, 3592, 3597) (PCI) | `3c59x` |
| 3Com Etherlink XL Boomerang (3C900, 3905) (PCI) | `3c59x` |
| 3Com 3985 | `acenic` |
| Accton MPX | `ne` and `8390` |
| Accton EN1203, EN1207, EtherDuo-PCI | `de4x5`, `tulip` |
| Allied Telesis AT1500 | `lance` |
| Allied Telesis AT1700 | `at1700` |
| Allied Telesis AT2450 | `pcnet32` |
| Allied Telesis AT2500* | `rtl8139` |
| Allied Telesis AT2540FX* | `eepro100` |
| AMD LANCE (7990, 79C96/960/961/961A, PCNet-ISA) | `lance` |
| AMD 79C965 (PCNet-32) and 79C970/970A (PCNet-PCI) | `pcnet32` |
| AMD 79C971 (PCNet-FAST), 79C72 (PCNet-FAST+) | `pcnet32` |
| AMD 79C974 (PCNet-SCSI) | `pcnet32` |
| Ansel Communications AC3200* (EISA) | `ac3200` |
| Apricot Xen-II* (82596) 板载以太网 | `apricot` |
| Boca BEN (ISA, VLB, PCI) | `lance`, `pcnet32` |

#### 表 D-1（续））

| 以太网卡 | 驱动名称 |
| :--- | :--- |
| Cabletron E21xx* | `ne` and `8390` |
| Cabletron E2100* | `e2100` and `8390` |
| Cabletron E22xx* | `lance` |
| Cogent EM100* ISA/EISA | `smc9194` |
| Cogent eMASTER+, EM100, EM400, EM960, EM964 | `de4x5`, `tulip` |
| Compaq Deskpro / Compaq XL (嵌入 AMD 芯片) | `pcnet32` |
| Compaq Nettelligent/NetFlex (嵌入 TI ThunderChip) | `tlan` |
| Danpex EN9400 | `de4x5`, `tulip` |
| D-Link DE-100, DE-200, DE-220-T, DE-250 | `ne` and `8390` |
| D-Link DE-520 | `pcnet32` |
| D-Link DE-528 | `ne`, `ne2k-pci`, and `8390` |
| D-Link DE-530 | `de4x5`, `tulip` |
| D-Link DE-600 | `de600` |
| D-Link DE-620 | `de620` |
| DFINET-300 and DFINET-400 | `ne` and `8390` |
| DEC DEPCA, DE100/1, DE200/1/2, DE210, DE422 | `depca` |
