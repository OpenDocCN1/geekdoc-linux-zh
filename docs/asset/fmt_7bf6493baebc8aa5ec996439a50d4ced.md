
| Compaq Netelligent 10/100 TX PCI UTP | `tlan.o` | `tlan=io_port,IRQ,aui,debug` |
| Compaq Netelligent 10 T PCI UTP |  | `tlan io=io_port irq=IRQ` |
| Compaq Integrated NetFlex 3/P |  | 其他模块选项： |
| Compaq Netelligent Dual 10/100 TX PCI UTP |  | `speed=10Mbs,100Mbs` |
| Compaq Netelligent Integrated 10/100 TX UTP |  | `debug=0x0[1,2,4,8]` |
| Compaq Netelligent 10/100 TX Embedded UTP |  | `aui=1` |
| Compaq Netelligent 10 T/2 PCI UTP/Coax |  | `duplex=[1,2]` |
| Compaq Netelligent 10/100 TX UTP |  |  |
| Compaq NetFlex 3/P |  |  |
| Olicom OC-2325, OC-2183, OC-2326 |  |  |
| Digital 21x4x Tulip PCI 以太网卡 | `tulip.o` |  |
| SMC EtherPower 10 PCI(843T/8432BT) |  |  |
| SMC EtherPower 10/100 PCI(9332DST) |  |  |
| DEC EtherWorks 100/10 PCI(DE500-XA) |  |  |
| DEC EtherWorks 10 PCI(DE450) |  |  |
| DEC QSILVER's, Znyx 312 etherarray |  |  |
| Allied Telesyn LA100PCI-T |  |  |
| Danpex EN-9400, Cogent EM110 |  |  |
| 具有 VIA VT86c100a Rhine-II PCI 或 3043 Rhine-I 的 VIA Rhine PCI 快速以太网卡 D-Link DFE-930-TX PCI 10/100 | `via-rhine.o` |  |
| AT&T GIS（前身为 NCR）WaveLan ISA 卡 | `wavelan.o` | `wavelan=[IRQ,0],io_port,NWID` |
| 设备 | 模块 | 参数 |
|---|---|---|
| WD8003 和 WD8013 “兼容” 卡 | `wd.o` | `wd=io_port,IRQ,mem,mem_end` `wd=io=io_port,irq=IRQ,mem=mem,mem_end=end` |
| Packet Engines Yellowfin | `yellowfin.o` |  |
| G-NIC PCI 千兆以太网适配器 |  |  |
| 用于 AX.25 的基于 Z8530 的 HDLC 卡 | `z85230.o` |  |

以下是这些模块使用的一些示例：

| 配置 | 示例 |
|---|---|
| IO 地址为 300 且 IRQ 为 11 的 NE2000 ISA 卡 | `ne=0x300,11` |
|  | `ether=0x300,11,eth0` |
| IO 为 390、自动探测 IRQ 并使用 NWID 为 0x4321 的 Wavelan 卡 | `wavelan=0,0x390,0x4321` |
|  | `ether=0,0x390,0x4321,eth0` |

## 使用多个以太网卡

您可以在一台机器中使用多个以太网卡。如果每张卡使用不同的驱动程序（例如 3c509 和 DE425），您只需为每张卡在 `/etc/conf.modules` 中添加 `alias`（以及可能的 `options`）行即可。有关更多信息，请参阅第 8.2.2 节。如果任意两张以太网卡使用相同的驱动程序（例如两张 3c509 或一张 3c595 和一张 3c905），您需要将两个卡地址放在驱动程序的 `options` 行上（对于 ISA 卡而言），或（对于 PCI 卡）只需为每张卡添加一行 `alias`。有关使用多于一个以太网卡的更多信息，请参阅 Linux Ethernet-HOWTO。如果您在安装 Red Hat Linux 时安装了 howto 包，您可以在文件 `/usr/doc/HOWTO/Ethernet-HOWTO` 中找到它。

# 附录 E

## 术语表

### Alpha

由数字设备公司开发的一种 RISC（精简指令集计算机）架构。

### ATAPI

AT Attachment Packet Interface 的缩写。ATAPI 是 CD-ROM 驱动器通过 IDE 接口与计算机系统通信的协议。

### Binary

虽然计算机使用的基数为二的数字系统被称为二进制，但该词通常指的是程序的可执行形式。对比“源代码”。

### BIOS

Basic Input/Output System 的缩写。在 PC 兼容系统上，BIOS 用于在首次通电时执行启动系统硬件所需的所有必要功能。BIOS 还控制引导过程，提供低级输入/输出例程（因此得名），并且（通常）允许用户修改系统硬件配置的细节。

### Boot

“bootstrap”的简称。计算机在通电时启动操作系统所经历的过程。

### Boot Diskette

用于启动许多 Red Hat Linux 安装的软盘。

### Bootstrap

参见“Boot”。

### CISC

Complex Instruction Set Computer 的缩写。计算机的一种设计理念，即处理器被设计为执行相对大量的不同指令，每条指令的执行时间不同（取决于指令的复杂性）。对比 RISC。

### CMOS

最初是 Complementary Metal Oxide Semiconductor 的缩写——一种用于许多集成电路的半导体技术。现在常用来描述包含个人计算机 BIOS 设置和计算机硬件时钟的低级硬件。

### Cylinder

在指代磁盘驱动器时，磁盘驱动器的读写磁头在驱动器的磁盘盘片上可以占据的不同位置的数量。从上方看盘片，每个磁头位置在盘片表面上描述了一个不同直径的想象圆，但从侧面看，这些圆可以被视为彼此嵌套的一系列圆柱体，因此得名。另见 Geometry。

### Daemon

守护进程是在无需人工干预的情况下运行以完成给定任务的程序。例如，`lpd` 是一个控制打印作业流向打印机的守护进程。

### Dependencies

在指代软件包时，依赖关系是软件包之间存在的依赖要求。例如，软件包 `foo` 可能需要由软件包 `bar` 安装的文件。在此示例中，必须安装 `bar`，否则 `foo` 将有未解决的依赖关系。RPM 通常不允许安装具有未解决依赖关系的软件包。

### Device Driver

控制连接到计算机或成为计算机一部分的设备的软件。

### Disk Drive

参见 Hard Disk。

### Disk Druid

Disk Druid 是 Red Hat Linux 安装程序的一个组件，用于在安装过程中对磁盘驱动器进行分区。

### Diskette

一种小型可移动存储设备，置于可移除盒中，旨在由兼容的驱动器进行读写。

### Distribution

一种通常为 Linux 的操作系统，已被打包以便易于安装。

### Domain Name

域名用于标识计算机属于特定组织。域名具有层次结构，每个层级之间用句点（读作“点”）分隔。例如，Foo 公司的财务部门可能使用域名 “finance.foo.com”。

### Driver

参见 Device Driver。

### Dual Boot

将计算机系统配置为引导多个操作系统的行为。该名称有些名不副实，因为可以引导的系统数量可能超过“双”所暗示的两个。

### EIDE

Enhanced Integrated Drive Electronics 的缩写，是 IDE 接口标准的新版本，也是 IDE 接口的一种特定实现的另一名称。EIDE 使更大、更快的磁盘驱动器成为可能；大多数今天销售的系统都使用 EIDE。

### Errata

Errata 在拉丁语中意为“哎呀”。当发现软件存在错误时，通常会修复软件并作为勘误发布。Red Hat Linux 也不例外；我们在 http://www.redhat.com/errata 上有一个勘误网页。

### Extended Partition

包含其他分区的磁盘驱动器段。参见 Partition。

### FAQ

Frequently Asked Questions 的缩写。Linux 信息通常以问答列表的形式呈现，称为常见问题解答。

### fdisk

`fdisk` 是一个实用程序，用于创建、删除或修改磁盘驱动器上的分区。

### Filesystem
