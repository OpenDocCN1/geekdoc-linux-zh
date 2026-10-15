
FTL 设备的命名非常复杂。设备由三部分组成：卡号、该卡上的区域号，以及可选的区域内分区。一个区域可以被视为没有分区表的单个块设备（类似于软盘），也可以像硬盘设备一样进行分区。`ftl0c0` 设备是卡 `0`、通用内存区域 `0` 的整个区域。`ftl0c0p1` 到 `ftl0c0p4` 设备是如果区域已分区，主分区 `1` 到 `4`。

FTL 分区的配置选项可以在 `ftl.opts` 中给出，其结构与 `memory.opts` 相似。传递给 `ftl.opts` 的设备地址由三个或四个字段组成：方案，

# 4. 使用特性

插槽号（socket number）、区域号，以及可选的分区号。大多数闪卡只有一个内存区域，因此区域号通常为 `0`。

Intel 第 100 系列闪卡使用第一个 `128K` 闪存块来存储卡片的配置信息。为了防止这些信息被意外擦除，`ftl_format` 会自动检测此内容并在创建 FTL 分区时跳过该块。

## 4.8 PCMCIA ATA/IDE 卡驱动器

ATA/IDE 支持基于内核 IDE 驱动。这包括 SmartMedia 和 Compact-Flash 设备；这些内存卡的设置使其能够模拟 IDE 接口。驱动器中 PCMCIA 特有的部分是 `ide_cs`。在拔出卡片之前，务必使用 `cardctl` 或 `cardinfo` 关闭 ATA/IDE 卡片，因为该驱动器从未支持过“热插拔”。

传递给 `ide.opts` 的设备地址由三个或四个字段组成：当前方案、插槽号、设备序列号以及可选的分区号。可以使用 `ide_info` 命令获取 IDE 设备自身的编号。对于 SCSI 设备，`ide.opts` 在 `PARTS` 变量中返回分区列表，然后将为每个分区调用脚本。

## 4.8.1 ATA/IDE 固定式磁盘设备参数

可以在 `ide.opts:` 中指定以下参数：

- `DO_FSTAB`

  布尔值 (y/n) 设置：指定是否应为该设备在 `/etc/fstab` 中添加条目。

- `DO_FSCK`

  布尔值 (y/n) 设置：指定在挂载之前是否应该检查文件系统，命令为 `fsck -Ta`。

- `DO_MOUNT`

  布尔值 (y/n) 设置：指定在插入卡片时是否应自动挂载该设备。

- `FTYPE`, `TYPES`, `MOUNTOPT`

  用于 fstab 条目和挂载设备的文件系统类型、挂载选项和挂载点。

- `NO_CHECK`, `NO_USER`

  卡片拔出策略的布尔值 (y/n) 设置。如果 `NO_CHECK` 为 `true`，当设备忙时，`cardctl eject` 将关闭设备。如果 `NO_USER` 为 `true`，脚本将不会尝试杀死使用已拔出设备的进程。这里是一个 `ide.opts` 文件示例，将任何 ATA/IDE 卡的第一个分区挂载到 `/mnt`：

```
case "$ADDRESS" in
  *,.*1)
    DO_FSTAB="y" DO_FSCK="y" DO_MOUNT="y"
    FTYPE="msdos" OPTS="" MOUNT="mnt" ;;
  *,*)
    PARTS="1" ;;
esac
```

## 4.8.2 诊断 ATA/IDE 适配器问题

- IO 故障可能导致 IDE 驱动程序误判驱动器几何结构并报告“INVALID GEOMETRY: 0”。要修复此问题，尝试在 `/etc/pcmia/config.opts` 中排除选定的端口范围。

- 部分 IDE 驱动器违反了 PCMIA 规范，需要更多的时间来启动。这可能导致“timed out during reset”消息。调整 `pcimia_core` 的 `unset_delay` 和 `unset_limit` 参数以为驱动器留出更多启动时间；详情请参阅 `pcimia_core` 主页。

- 要使用 ATA/IDE CD-ROM 设备，你的内核在编译时必须启用 `CONFIG_BLK_IDE`。对于标准内核这通常是开启，但如果你编译了自定义内核，请注意这一点。

- 尝试挂载错误文件时的常见错误。通常情况下，你想挂载驱动器的分区，而不是整个设备（即 `/dev/ide1`, `/dev/ide2`）。

- 如果在插入时没有介质，Linux IDE 驱动程序可能会出现有问题的移除式介质驱动器。IBM Portable 就存在这个问题。

- 某些内核会在插入时报告“drive not ready”错误。这些错误可以被忽略；当可移动式 IDE 设备不接受命令时，它们会弹出。

```
CORE_OPTS="unset_delay=40"
```

## 4.9 多功能卡

单个中断可以被多个驱动程序共享，例如串行驱动程序和以太网驱动程序：事实上，PCMIA 规范要求所有卡片功能共享同一个中断。通常情况下，所有卡片功能都可以在无需共享驱动程序的情况下可用。

同时使用两个卡片功能是“棘手”的，不同的硬件供应商以各自不兼容的（有时是私有的）方式实现了中断共享。某些卡的驱动程序（Ositech Jack of、3Com 3c62 及相关卡、Linksys 卡）能够正确支持并发访问，但其他（旧卡）则不支持。如果你在激活两个功能的情况下使用卡片遇到困难，请尝试隔离地使用每个功能。这可能需要显式执行 `ifconfig down` 来关闭同一张卡片上的网络接口和调制解器。

# 5 高级主题

## 5.1 PCMCIA 设备的资源分配

理论上讲，将哪个中断分配给设备并不重要，只要没有两个设备被配置为使用同一个中断。在 `/etc/pcmia/config.opts` 中，你会找到一个用于排除非 PCMCIA 设备所用中断的地方。

同样，没有办法直接指定卡片使用的 I/O 地址充分`etc/pcmia/config.opts` 文件允许你指定适用于任何卡片的可用端口范围，或者排除与其他设备冲突的范围。

在修改 `/etc/pcmia/config.opts` 后，可以使用 `kill -HUP` 重启 `cardmgr`。用于监控卡片状态的中断由底层 socket 驱动模块（`i82365` 或 `tcicb`）选择；`cardmgr` 解析 `/etc/pcmia/config`，因此它不受该文件更改的影响。要设置此中断，当 socket 驱动程序是 `/etc/rc.d/rc` 中的 `PCIC_OPTS` 变量时，使用 `cs_irq_opts`。

所有客户端都有一个名为 `irq_list` 的参数，用于指定它们可能分配的中断。这些驱动选项应设置在你的 `/etc/pcmia/config` 中：

```
device "serial_cs"
module "serial_cs" opts "irq_list,8,12"
```

将指定驱动程序仅使用 irq 8 或 irq 12。无论 `irq_list` 如何设置，Card Services 都不会分配已被另一个设备占用的中断，或者文件中排除的中断。

## 5.2 PCI 中断配置问题与解决方案

大部分讨论适用于 `2.2` 及更早的内核。对于 `2.4` 及更新的内核，PCI 子系统负责大部分中断管理。以下提示可能有助于诊断问题，尽管此处描述的某些工作负载可能无效。

### 5.2.1 PCI 中断路由概述

每个插槽都有四个 PCI 中断引脚（`INTA` 到 `INTD`）。单功能将仅使用 `INTA`。PCI 子系统负责大部分中断管理。以下提示可能有助于诊断问题，尽管此处描述的某些工作负载可能无效。

# 5. 高级主题

即使你不知道路由器是如何工作的，也要了解 PCI 中断是按某种方式设置的。

如果你遇到了你认为可能与 PCI 中断配置有关的问题，应该首先验证你是否拥有一个足够较的 PCMCIA 驱动程序包。仔细查看 PCMCIA 内核模块加载时的启动信息。你应该能看到类似的内容：

```
Linux PCMCIA Card Services 3.1.18
kernel build: [2.2.14-5] #1 May 9 10:44:42 PDT 2000
options: [pci] [cardbus] [apm] [pnp]
pci routing table version 1.0 at 0xfdf30
Intel PCI probe
TI 1126 rev 02 PCI-CardBus at slot 00:07, mem 0x20000000
host opts: [ring] [serial peri & irq] [pci irq 11] ...
host opts: [ring] [serial peri & irq] [pci irq 11] ...
ISA irqs (scanned) = 3,4 PCI status changes
```

“routing table”（路由表）消息表示找到了有效的路由表。“host opts”（主机选项）行指示了中断交付模式，以及是否能为每个插槽确定 PCI 中断。最后几行显示了可用中断的扫描结果。

## 5.2.2 PCI BIOS 未检测到 CardBus 桥器

症状：

- `Intel PCI probe`：未找到。

- 桥器未在 `lpci` 或 `/proc/pci` 中显示。
