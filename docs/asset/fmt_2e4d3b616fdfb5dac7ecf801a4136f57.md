
要自动挂载和挂载 NFS 文件系统，首先将所有这些文件系统添加到 `/etc/fstab`，但在挂载选项中包含 `noauto`。在 `network.opts` 中，将挂载点列在 `MOUNTS` 变量中。当这样配置 NFS 挂载时，使用 `cardctl` 或 `cardinfo` 来关闭网卡尤为重要。如果网卡在没有某种的情况下直接拔出，是无法干净地挂载 NFS 文件系统的

## 使用与特性

除了通常的网络配置参数外，`network.opts` 脚本还可以指定在接口配置之后或接口关闭之前采取的任何操作。如果 `network.opts` 定义了一个名为 `start.fn` 的函数，它将在 `network` 脚本配置接口后被调用，接口名称将作为其第一个也是唯一的 参数传递给它。同样，如果定义了 `stop.fn`，它将在关闭接口之前被调用。

### 3.3.1 收发器选择

在 `network.opts` 中可以使用 `IF_PORT` 设置来选择收发器。这在先前的 PCMCIA 中可以是一个数值值，也可以是识别收发器的关键字。所有网络驱动程序默认尽可能自动检测接口，否则使用 `0baseT`。可以使用 `ifport` 命令来选择或设置收发器类型。例如：

```bash
# ifport eth0 10base2

#
# ifport eth0
eth0 2 (10base2)
```

`3c589` 驱动的当前版本尝试自动检测网络连接，但这似乎并未完全正常工作。为了成功，在配置网卡时，网卡应该连接在卡上。或者，一旦网络连接，你可以强制驱动程序连接该连接：

```bash
ifconfig eth0 down up
```

### 3.3.2 关于特定卡的说明

- 对于 IBM CCAE 和 Socket EA 卡，在配置网络设备时，你需要选择收发器类型（10base2、10baseT、AUI）。请确保系统日志中报告的收发器类型与你的连接匹配。
- SMC、Megahertz、Orthis 和 3Ccm 的驱动程序应自动检测连接的网络类型（10base2 或 10baseT）。在驱动程序加载时设置收发器类型用于定义卡的“首次猜想”。
- Fall EtherWave 实际上位于 `3c5589` 上，具有特殊的收发器。EtherWave 使用 10baseT 风格连接，其收发器要求 `3c5589` 配置为 10base2 模式。
- 如果你在 IBM CCAE、NE4100、Conrad 或 Kingston 适配器上遇到问题，可以使用 `pcnet` 模块上的 `med_speed` 选项增加访问时间。`config` 文件中提供了如何操作的示例。速度设置为 1000（纳秒）。
- 对于 New Media Ethernet 适配器，当加载 `pcmia_core` 模块时，可能需要使用 `io_speed` 增加访问时间。编辑启动脚本中的 `CORE_OPTS` 获取此设置。
- New Media Ethernet 驱动的多播支持是不完整的。最新的驱动可以使用多播，但会正确忽略数据包。
- IBM 和 3Ccm 使用的驱动程序在卡初始化时未连接到网络时似乎表现糟糕。在通电前始终连接这些卡。
- Linksys 和 D-Link 卡具有 Linux 驱动不支持独特选择方法。在获得 Linksys 的文档之前，唯一的解决方法是进入 DOS 并使用供应商提供的工具设置收发器，然后热启动。

### 3.3.3 网络适配器问题诊断

- 你的卡被识别为以太网卡吗？检查系统日志并确保 `cardmgr` 正确识别了卡并启动了 `serial.cs` 驱动。如果没有，如果它是支持的卡，可能仍然可用，除非它声称为“NE2000”。
- 卡配置正确吗？如果你使用的是支持的卡并被 `cardmgr` 识别但仍然无法工作，可能与其他设备存在中断或端口冲突。找出卡使用的资源（通过系统日志），并在 `/etc/pcmia/config.opts` 中排除这些。
- 如果卡配置正确但有时出现循环（特别是在负载下），你可能需要尝试更改驱动程序的定时设置。更多信息请参见第 2.5 节。
- 如果你尝试访问网络时收到类似“网络不可达”的消息，你可能正确设置了 `/etc/pcmia/network.opts`。另一方面，配置错误的卡通常会静失败。
- 要诊断 `/etc/pcmia/network.opts` 中的问题，从 ping 你子网上的其他系统开始。尝试 ping 网关，然后是其他子网的机器。在这些测试后按名称 ping 机器。
- 确保你的结果是 PCMCIA 的。查看卡在供应商驱动下是否工作可能会帮助。双击你对 `/etc/pcmia/network.opts` 的修改。

## 3.4 PCMCIA 和调制调器设备

Linux 串口设备通过 `/dev/cua` 和 `/dev/ttyX*` 特殊设备访问。`ttyX*` 设备用于接入连接或直接连接的终端。每个物理串口都有一个 cua 文件：为应用程序选择合适的设备取决于你。对于串口设备的配置，可以使用 `setserial` 命令。

当检测到 PCMCIA 卡或调制调器时，它将被分配到第一个可用串口槽。这通常是 `/dev/tty1 (cua)` 或 `/dev/tty2 (cua2)`，取决于内置串口的数量。`ttyS*` 设备是 `/var/run/stab` 中的。`/etc/pcmia.opts` 中的默认串口设备选项将连接的 `cua` 文件链接到 `/dev/modem` 以方便。

不要使用 `/etc/rc.d` 配置 PCMCIA 调制调器。此脚本应仅用于配置不可移动的设备。如果你想对你的调制调器进行任何设置，请修改 `/etc/pcmia/serial.opts`。此外，不要使用 `setserial` 修改 PCMCIA 串口设备的 IO 和中断设置。这将告诉串口驱动程序设备的位置，但不会更改卡的实际配置方式。

`serial.opts` 中的设备地址有三个逗号分隔的字段：第一个是方案，第二个是插字号，第三个是实例。对于支持多个串口的卡，设备实例可以取多个值，对于卡为 0。如果你经常使用多个 PCMCIA 调制调器，你可能想根据插字号指定不同的设置，如下：

```bash
case $ADDRESS in
0,*) # 插字号 0 调制调器的选项
;;
*,1,*) # 插字号 1 调制调器的选项
;;
esac
```

如果 Linux 启动时已配置 PCMCIA 调制调器，可能会被错误识别为普通的内置串口。然而，如果 PCMCIA 驱动接管了调制调器，它将被分配到一个不同的设备槽。让 `/var/run/stab` 使用 `/dev/modem` 比于期望 PCMCIA 调制调器始终具有相同的设备分配。

如果你配置内核加载 Linux 串口驱动程序作为模块，你必须编辑 `/etc/pcmia/config` 指明该模块必须加载。要读取的串口设备条目是：

```
device serial_cs
class 'serial' module char/serial, 'serial_cs'
```

### 3.4.1 串口设备问题诊断

- 你的卡被识别为调制调器吗？检查系统日志并确保 `cardmgr` 正确识别卡并启动了 `serial.cs` 驱动。如果没有，你可能需要向你的 `/etc/pcmia/config` 文件添加一个新条目以便其正确识别。详情请参见第 4.1 节。

- `serial.cs` 是否成功配置了调制调器？再次检查系统日志中是否有来自 `serial.cs` 的消息。如果你与其他设备存在 I/O 端口冲突。冲突的另一个提示是，如果设备被报告给 8250；大多数 PCMIA 模块应被识别为 1650A UART。如果你认为你遇到了端口冲突，请编辑 `/etc/pcmia/config.opts` 并排除为调制调器分配的端口。

- 是否存在中断冲突？如果系统日志正常，但调制调器似乎无法工作，尝试设置 `serial` 将中断更改为 0，看调制调器是否能工作。这将导致串口驱动程序使用轮询模式（polled mode）而不是中断。如果这解决了问题，很可能是系统中的其他设备正在使用 `serial.cs` 选择的中断。你应该向 `/etc/pcmia/config.opts` 中添加一行来排除此中断。

- 如果调制调器看起来运行速度非常、非常缓慢，这几乎确定是中断冲突的指示。

- 确保你的问题确实是 PCMIA 的问题。查看该卡在 DOS 或厂商驱动程序下是否工作可能会帮助。另外，在确定可以建立简单连接之前，不要使用像 SLIP 的工具测试该卡。如果简单功能可以工作但 SLIP 不行，那么你的问题可能出在 SLIP，而不是 PCMIA。

## 3.5 PCMIA SCSI

所有支持的 PCMIA SCSI 卡都与以下 ISA 卡之一功能相似：Qlogic、Adaptec HAH-152X 或 Future TMC-160X。PCMIA 设备是通过使用 PCMIA 特有的代码（在 `qlogic.cs`、`toaster.cs` 或 `fdomain.cs` 中）结合标准的 Linux SCSI 驱动程序构建的。

当检测到新的 SCSI 主机适配器时，SCSI 驱动将探测设备。检查系统日志以确保你的设备被正确检测。新的 SCSI 设备将分配给第一个 SCSI 设备文件。第一个磁盘将是 `/dev/sda`，第一个 SCSI 分区将是 `/dev/st0`，第一个光驱将是 `/dev/scd0`。

在 1.2X 内核中，PCMIA 驱动程序能够发现内核 SCSI 设备连接到了 SCSI 适配器。它们将位于 `/var/run/stab` 中，并且对于每个连接的设备，都会调用 SCSI 配置文件 `/etc/pcmia/scsi` 来配置或关闭该设备。默认脚本不会采取任何配置 SCSI 设备的动作，但在移除卡时，会在 SCSI 设备上正确地挂载文件系统。

PCMIA 驱动程序无法自动推出哪些设备与特定的 SCSI 适配器相关。相反，如果你有一个标准的 SCSI 设备配置，你可以在 `/etc/pcmia/scsi.opts` 中列出这些设备。例如，如果你有一个 SCSI 磁盘和一个光驱，你将使用：

```
# 针对 1.2 内核：已连接设备列表
SI_DEVICES=sda scd0
```

传递给 `scsi.opts` 的设备地址非常复杂，因为连接到 SCSI 适配器的事物种类很多。适配器由六或七个逗号分隔的字段组成：当前系统、设备类型、插槽号、SCSI 通道、ID、逻辑单元号以及分区号。设备类型对于磁盘为 "sd"，对于磁带为 "st"，对于光驱设备为 "scd"，通用 SCSI 设备为 "sg"。对于大多数设置，对于具有多个分区的磁盘设备，SCSI 通道和逻辑单元号将 0。`scsi.opts` 首先会调用整个设备并带有五个字段地址。脚本应使用 `PARTS` 变量来列出分区。这里有一个配置位于 SCSI ID 3 具有两个分区的设备以及 SCSI ID 6 处光驱的示例：

```
case "ADDRESS"
 *sd,0,3,0
  # 此设备有两个分区...
  PARTS= "1 2"
  ;
 *sd,0,3,0,1
  # 分区 1 的选项
  # 更新 /etc/stab，并在 /usr1 上挂载一个 ext2 文件系统
  DO_FSTAB="y"; DO_FSCK='y'; DO_MOUNT="y"
  FSTYPE="ext2"
  OPTS=""
```

```
MOUNTPT="/usr1"
;
*sd,*,0,3,0)
# 分区 2 的选项：
# 更新 /etc/fstab，并在 /usr2 上挂载一个 MS-DS
DO_FSTAB='y'; DO_FSCK='y'; DO_MOUNT='y'
STYPE="msdos"
OPTS=""
MOUNTPT="/usr2"
;
*sr,*,0,6,0)
# SCSI ID 6 处光驱的选项
PARTS=""
DO_FSTAB='y'; DO_FSCK='n'; DO_MOUNT='y'
STYPE="iso9660"
OPTS=""
MOUNTPT="/cdrom"
;
esac
```

如果你的内核没有针对 `/var/scsi` 设备的顶层驱动（磁盘、磁带等），则该设备将不会被 PCMIA 驱动程序配置。作为副作用，`/var/run/stab` 中的设备名称将类似于 "#nnnn"，其中 "nnnn" 是四位十六进制数。这发生在 `cardmgr` 无法将 SCSI ID 翻译为对应的 Linux 设备名时。

将顶层 scsi 模块化是可能的。相反，如果你有一个标准的 SCSI 设备配置，你可以在 `/etc/pcmia/scsi.opts` 中列出这些设备。

## 3.7 PCMCIA ATA/IDE 卡驱动器

传递给 `fixed.opts` 的设备地址由三个或四个字段组成：设备、插槽号、驱动程序的序列号以及可选的分区号。对于 SCSI 设备，`fixed.opts` 首先针对整个设备进行调用。如果 `fixed.opts` 在 `PARTS` 变量中返回分区列表，脚本将为每个分区调用一次。

这是一个 `fixed.opts` 文件示例，用于将任何 ATA/IDE 卡的第一个分区挂载到 `/mnt/`。

```
case $ADDRESS in
  *,*)
    PARTS='1'
    ;
  *,*1)
    DO_FSTAB='y'; DO_FSCK='y'; DO_MOUNT='y'
    FSTYPE='msdos'
    OPTS=''
    MOUNTPT='/mnt'
    ;
esac
```

注意，默认的 `fixed.opts` 文件包含这些行，但被注释掉了。如果你需要，可以根据序列号为特定的卡分离配置。要查找驱动器的序列号，请使用 `ide_info` 工具。那么 `fixed.opts` 的部分内容可能如下：

```
case $ADDRESS in
  *,Z24360542)
    # 这是我的 DOS 配置
    PARTS='1'
    ;
  *,*Z24360542,1)
    DO_FSTAB='y'; DO_FSCK='y'; DO_MOUNT='y'
    FSTYPE='msdos'
    OPTS=''
    MOUNTPT='/mnt'
    ;
esac
```

## 3.8 多功能卡

从 1.3.73 内核开始，单个中断可以被多个驱动程序共享，例如串口驱动和以太网驱动。在较新的内核下使用多功能卡时，可以在不加载和卸载驱动程序的情况下使用所有功能。

同时使用两块卡是“棘手”的，不同的硬件厂商以各自不兼容的（有时是私有的）方式实现了中断共享。某些卡的驱动程序（Orisitech Jack of Diamonds, 3Com 562; Linksys）能够很好地支持同时访问，但其他（特别是 Megahertz）则不支持。

早期的内核不支持不同设备之间的中断共享，因此 PCMCIA 驱动程序无法配置同时访问以太网和调制调器。以太网驱动和串口驱动都会自动加载。然而，以太网驱动默认拥有该卡。要使用调制调器，你可以通过执行如下操作卸载以太网驱动并重新配置串口端口：

```
ifconfig eth down
rmmod 3c89_cs
setserial /dev/modem autoconfig auto_irq
setserial /dev/modem
```

## 使用

第二个串口应该验证该端口是否已配置为以太网驱动之前使用的的中断。

### 如何控制设备使用哪些资源？

理论上来说，将哪个中断分配给哪个设备并不重要，只要没有两个设备被配置为使用同一个中断。在 `/etc/pcmia/config.opts` 中，你可以找到排除非 PCMCIA 设备所用中断的地方。

注意，用于监控状态更改的中断是由低级驱动模块（i8236 或 tcbi）通过 `cardmgr /etc/pcmia/config` 选择的，因此它不受此文件影响。要设置此项，请在加载驱动程序时在 `/etc/rc.d/rc.pcmia` 中使用 `irqmask` 或 `cs.irq` 选项。

所有客户端驱动程序都有一个名为 `irqmask` 的参数用于指定尝试分配的中断。每个 `irqmask` 对应一行：如果位 0 为 0，则位 1 为 1，依此类推。最大 0x120 对应 irq 9 和 irq 12。要限制设备仅使用一个中断，其 `irqmask` 应该只设置一位。这些驱动程序选项应该在 `/etc/pcmia/config` 文件中设置。例如：

```
device 'serial_cs'
module 'serial_cs' opts irqmask=0x100
```
