
当使用一次此选项时，元组中的 LUN（在每个设备的开头）将以“T10”格式显示，该格式最高可达十六进制。它的前缀是“0x”。此外，分级 LUN 用一个字符分隔级别显示。例如，两个 LUN: 0x35500660000000 将显示为 0x355-0066。如果给出此选项（例如使用‘0x355-0066’），则为每个 LUN 显示完整的 16 位数字。

- `-p`, `--protection`

输出目标 (DIF) 和初始化器 (DIX) 保护。

- `-P`, `--protmode`

输出每个设备的有效保护信息。

- `-i`, `--scsi_id`

输出在 `/dev/by-id/` 中找到的 udev 匹配。这仅适用于磁盘类设备。如果没有匹配，则输出 `/sys/class/block/`。

- `-s`, `--size`

以人类可读格式打印磁盘容量。

- `-t`, `--transport`

输出传输信息。如果给出此选项，则列出 SCSI 设备。当使用 `--list` 时，输出目标信息或主机信息。对于设备，通常是传输类型，前面留有两个空格。输出 `attribute_name=value` 对。

- `-v`, `--verbose`

输出详细信息。

- `-V`, `--version`

输出版本信息。

- `-w`, `--wwn`

输出磁盘的全球名称 (WWN)，通常为 64 位，但也可以是 128 位。为了指示 WWN，前缀为“0x”。

- `-y`, `--sysfsroot=PATH`

假设 sysfs 挂载在 PATH。如果给出此选项，PATH 应该是绝对路径。

# 传输方式

此工具列出作为逻辑单元 (LU) 的 SCSI 设备，位于 SAM-4 架构（https://www.t10.org）。当给出 `--hosts` 选项时，它是初始化器。SAM-4。通过传输到达目标，并延伸到逻辑单元。目标设备可能包含多个端口。如果 FC 或 SAS 磁盘是可见的，lsscsi 将显示两个端口。初始化器（即主机）也具有多个端口，而 HBA 则每个初始化器有一个条目。对于设备，则每个初始化器有一个条目。

通常此工具为每个“设备”或主机提供一行输出。通过添加 `--list` 选项可以获得显著更多信息。在设备上提供的传输信息是 SAM-4 架构。当配合 `--transport` 选项时，在摘要行之后以 `attribute_name=value` 的格式输出传输信息，前面留有两个空格。当给出 `--list` 选项时，输出目标信息。如果存在设备列表，使用过滤参数可以减少输出量。

目前识别的传输方式包括：IEEE 1394, ATA, FC, iSCSI, SAS, SATA, SPI 和 USB。

对于 IEEE 1394（也称为 Firewire，当涉及存储时为 SBP），在给出 `--transport` 且没有 `--hosts` 选项的情况下，输出基于 EUI64 的目标端口。给出 `--hosts` 选项时，输出 EUI64 初始化器端口。特定 IEEE 1394 传输的摘要行前缀为“sbp”。

为了检测 ATA 和 SATA，在耗尽其他传输检查后对名称进行粗略检查。根据驱动名称选择 ATA 或 SATA 传输类型。摘要行的输出为“ata”或“sata”。没有给出其他属性。标记为“ata”的设备和主机将使用并行 ATA (PATA)。对于光纤 (FC)，在给出传输时输出端口名称和端口标识符。在没有 `--hosts` 选项的情况下，这些 ID 是与列出的设备（逻辑单元）关联的目标端口。给出 `--hosts` 选项时，这些 ID 是主机使用的初始化器端口。特定 FC 传输的摘要行前缀为“fc”：如果检测到 FCoE（通过以太网），则前缀改为“fcoe”。

对于 iSCSI，在给出 `--transport` 且没有 `--hosts` 选项的情况下，输出目标端口。这由 iSCSI 名称和目标端口组组成。

由于 iSCSI 名称以 "iqn" 开头，因此不使用前缀。当给出 `--*hosts*` 选项时，摘要行将输出 "iscsi:"。

对于串行连接 SCSI（SAS），它将输出目标端口的 SAS 地址（如果也给了 `--*hosts*` 选项，则输出初始化器端口）。这将是一个 naa-5 地址。对于 HBA 和 SAS 目标设备（如 SAS 磁盘和磁带驱动器），SAS 地址是唯一的。对于连接到 SAS 扩展器的 SATA 磁盘，扩展器通过在其自身的 SAS 地址上加上一个非零值（即扩展器的 SAS 地址）来提供 SAS 地址（例如 `expander_sas_address+ phys_id+1`）。直接连接到 SAS HBA 的 SATA 磁盘似乎具有不确定的 SAS 地址。摘要行中特定于 SAS 传输的输出前缀为“sas:”

对于 SCSI 并行接口（SPI），在给出 `--*transport*` 且没有 `--*hosts*` 选项的情况下，将输出目标端口标识符（通常为 0 到 15 之间的数字）。当给出 `--*hosts*` 选项时，摘要行中仅输出 “spi:”。

当检测到 USB 传输时，摘要行将包含 “usb:” 后跟一个 USB 设备名称。USB 设备名称的格式为 “<b>-<p1>.<p2>.<p3>:<>,<>,,<i>”，其中 <b> 是 USB 总线号，<p1> 是端口，<p2> 是存储设备，<p3> 指配置号，而 <i> 是接口号。每个 USB 目标都有一个独立的 SCSI 主机。一个 USB SCSI 目标可能包含多个逻辑单元。因此，USB SCSI 主机和属于该 USB 主机的所有逻辑单元将显示相同的“device_name”字符串。

## LUN

出于历史原因以及多个 Unix 系统的习惯，Linux 使用一个整数元组来描述 SCSI 设备（也称为逻辑单元 LU）。该元组的最后一个元素是所谓的逻辑单元数（LUN）。最初 SCSI LUN 最初是 3 位的整数，后变为 8 位。如今的 SCSI LUN（SAM-5 第 4.7 节）是 64 位，但 SCSI 标准现在将 LUN 视为 8 字节的整数。

在 2013 年之前，Linux 通过取 SCSI LUN 的前 4 个字节并忽略后 4 个字节将 SCSI LUN 映射为 32 位整数。Linux 将 SCSI LUN 的两个字节视为一个单元（字），并使其成为 LUN 整数中的低 16 位。SCSI LUN 的后两个字节成为 LUN 整数中的高 16 位。这样做的理由通常是为了常用的较小 LUN 整数。在 SCSI LUN（十六进制）表示法中，常见的 LUN 是 00 00 00 00 00 00 00 00，这变为 Linux LUN 0。下一个常见的 LUN 是 00 01 00 00 00 00，这变为 Linux LUN 1。

2013 年，有人提议通过扩展上述映射将 Linux LUN 增加到 64 位整数。在这种情况下，SCSI LUN 中可以表示的所有信息都将映射到一个 LUN（64 位）整数中。且该映射是可以反向的，不会丢失信息。

此版本的实用程序支持 32 位和 64 位 LUN 整数。默认情况下，每行开头元组结尾显示的 LUN 是十进制整数格式的 LUN。当给出 `--lunhex` 选项时，LUN 以 SCSI LUN 格式显示，8 个字节连接在一起，以十六进制输出并带有前缀 ‘0x’。LUN 根据 SAM-5 的描述进行解码，且不显示末尾的零（即右侧数字）。LUN 0（即 00 00 00 00 00 00 00 00）显示为 0x0，LUN 65（即 41 00 00 00 00 00 00 00）显示为 0x041。如果给出两次 `--lunhex` 选项，则显示完整的 64 位（即十六进制数字）。

如果命令行上没有给出 `--lunhex` 选项，则会检查环境变量 `SCSI_LUNHEX_OPT`。如果存在 `SCSI_LUNHEX_OPT`，则其关联值将成为内部设置 `--lunhex` 的次数。例如，`SCSI_LUNHEX_OPT=2 lscsi` 和 ‘`lscsi -xx`’ 是等效的。

## EXAMPLES

关于此实用程序的信息（示例也可以此处找到：http://sg.danny.cz/scsi/lscsi.html

## NOTES

此命令的信息源自 sysfs 文件系统，除非用户另有指定，否则假设其挂载在 `/sys`。被 SCSI 中层检测到的 SCSI（伪）设备，即使所需的上层驱动程序（即 sd, sr, st, sg 或 ch）未加载，也会列出。如果未加载相应的上层驱动，设备文件名将显示为 而不是类似 `/dev/sto0`。请注意，某些设备（例如扫描仪和介质库器）没有主上层驱动，只能通过 SCSI 通用 (sg) 设备名称访问。

还可以通过 Linux 中的 bsg 驱动访问通用 SCSI 设备。默认情况下，bsg 驱动的设备节点名称格式为 `/dev/bsg/H:C:T:L`。因此，此实用程序在以 ‘6:0:1:2’ 开头的行中显示的 SCSI 设备，可以通过 `/dev/bsg/6:0:1:2’ 设备节点名通过 bsg 驱动进行访问。

在 Linux 内核 2.6.26（及可能的后续版本）未定义 CONFIG_SYSFS_DEPRECATED_V2 内核选项的情况下，需要 iscsi 版本 0.21 或更高版本才能正确显示 SCSI 设备。

## AUTHOR

Doug Gilbert 编写

## REPORTING BUGS

向 <dgilbert at interlog dot com> 报告 bug。

## COPYRIGHT

Copyright © 2003-2013 Gilbert 本软件根据 GPL 分发；即使对于特定适用性也不提供任何保证。

## SEE ALSO

lspci, lsusb

## lsusb

- NAME

lsusb - 列出 USB 设备

## LVCHANGE

- NAME

lvchange – 修改逻辑卷属性

- DESCRIPTION

lsusb 是一个用于显示 USB 总线和连接设备信息的实用程序。

- OPTIONS

- `-v`, `--verbose`

告诉 usb 输出详细信息并显示信息。

- `-s [[bus]:devnum]`

仅显示指定总线和设备号的设备。

- `-d [vendor]:[product]`

仅显示指定厂商和产品的设备。

- `-t`

以树形形式导出 USB 层次结构。

- `-V`, `--version`

在标准输出打印版本信息并退出。

- RETURN VALUE

如果未找到设备，则返回非零退出码。

- FILES

```
/usr/share/hwdata/usb.ids
```

已知 USB ID 列表（厂商、产品、类、子类）。

- SEE ALSO

lspci(8), usbview(8).

- AUTHOR

Thomas Sailer, <sailer@ife.ee.ethz.ch>.

# 说明

lvchange 允许你更改逻辑卷的属性，包括使其被内核感知并准备就。

## 选项

常用选项请参阅 lvm [aeisls]{1n}。

- `-a,--activate` 控制逻辑卷的可用性。通过 libdevmapper 与内核设备映射器驱动通信，以激活 (-ay) 或取消激活 (-an) 逻辑卷。

激活逻辑卷会创建一个指向设备节点的符号链接 `/dev/VolumeGroupName/LogicalVolumeName`。所有软件和脚本都应该通过此符号链接访问设备，并将其呈现为设备名称。底层设备节点的位置和名称可能取决于发行版和配置（例如 udev），并可能随版本的发布而变化。

如果使用了自动激活 (-aay)，则只有当逻辑卷匹配 `lvm.conf` 中的 `activation/auto_activation_volume_list` 列表时才会被激活。如果未设置列表，则所有卷都将进入激活考虑。在系统启动期间应使用 `-ay` 选项，可以通过 `activation/auto_activation_volume_list` 设置来选择要激活哪些卷。

在集群卷组（VG）中，使用 `clvmd` 进行激活，可能的选项有：

- `-aey`，clvmd 在独占模式（带有独占锁）下激活逻辑卷（LV），允许单个节点激活该 LV。

- `-sy`，clvmd 在共享模式（带有共享锁）下激活 LV，允许多个节点并发激活该 LV。如果 LV 类型禁止共享访问（例如带有快照的 LV），则忽略 's' 选项并使用独占锁。

- `-ay`（未指定模式），如果 LV 类型允许并发访问（例如线性逻辑卷 LV），`clvmd` 将以共享模式激活 LV。否则，`clvmd` 将以独占模式激活 LV。

- `-aey`, `-asy`, 和 `-ay`，clvmd 尝试在所有节点上激活 LV。如果使用独占模式，则只有其中一个节点会执行成功。

- `-an`，clvmd 尝试在所有节点上取消激活 LV。

- `-aly`，clvmd 仅在本地节点激活 LV，而 `-aln` 仅在本地节点取消激活。如果 LV 类型允许并发访问，则使用共享模式，否则使用独占模式。

带有快照的 LV 始终以独占方式激活，因为它们同时只能在一个节点上。

对于本地卷组（VG），-aey, -asy, 和 -asy 都是等效的。

- `-activationmode {complete|degraded|partial}` 激活模式决定了在物理卷（PV）缺失（例如由于设备故障）时是否允许激活逻辑卷。`complete` 是最严格的；仅激活未受缺失 PV 影响的逻辑卷。`degraded` 允许在 PV 缺失的情况下激活 RAID 逻辑卷。（注意，“镜像分段类型”不被视为逻辑卷。应使用 raid1 分段类型。）最后，`partial` 允许在 PV 缺失或失败导致分区缺失的情况下激活任何逻辑卷。此选项应仅在执行恢复或修复操作时使用。默认模式为。要更改它，请参阅 `llvm.conf(5)` 中的 `activation_mode`。

- `-K`, `--ignoreactivations` 忽略在激活期间跳过逻辑卷的标记。

- `-cachepolicy`, `--cachesettings key=value` 仅适用于缓存的 LV；另请参阅 `llvmcache(7)`。设置缓存策略及其可调设置。在大多数用例中，默认值已经足够。

- `-C`, `--contiguous {y|n}` 尝试设置或重置逻辑卷的连续分配策略。只有当所有分配的物理范围区（extents）都是相邻的时，才可以将非连续逻辑卷的分配策略更改为连续。

- `-detachprofile` 卸载任何附加到逻辑卷的元数据配置方案。有关元数据配置更多信息请参阅 `llvm.conf(5)`。

- `-discards {ignore|nopass|passdown}` 设置此项以忽略精简池（thin pool）卷接收到的任何丢弃。设置为在精简池内部处理此类丢弃，并允许长时间需要的区域被新数据覆盖。设置为 passdown（默认值）则在精简池内部处理并将其传递给底层设备。

- `-errorwhenfull {y|n}` 设置数据空间耗尽时精简池的行为。信息请参阅 `lvcreate(8)`。

- `-resync` 强制镜像进行完全重同步。在正常情况下，你不需要此选项，因为同步会自动发生。数据从主镜像设备读取并复制到其他镜像中，因此这可能花费大量时间——在此期间，你将没有数据的完整冗副本。

- `-metadataProfileName` 使用并将 ProfileName 配置方案附加到逻辑卷元数据中。每当下次处理该逻辑卷时，该方案将自动应用。如果卷组附加了另一个方案，则优先使用逻辑卷方案。有关元数据方案的更多信息请参阅 `llvm.conf(5)`。

- `--minor minor` 设置次号。

- `--major major` 设置主号。此选项仅在旧系统（内核 2.4）上支持，在动态分配主号的现代 Linux 系统上会被忽略。

- `--monitor {y|n}` 如果安装了 dmevent，则启动或停止对镜像或快照逻辑卷的监控。

- `--poll {y|n}` 如果被监控的卷所使用的设备报告错误，则对其进行处理。

- `--writmost {y|n}` 将设备标记为只写。使用 `auto_activation_volume_list` 设置。

- `--raidmaxrecoveryrate {y|n}` 设置卷的最大恢复率。

- `--raidminrecoveryrate {y|n}` 设置卷的最小恢复率。

- `--raidrecoveryrate {y|n}` 设置卷的恢复率。

- `--raidwritebehind {y|n}` 指定允许的最大待处理写入数。

- `--raidwriteount {y|n}` 设置允许的最大待处理写入数。

- `--udev` 禁用 udev 同步。

- `--ignoremonitoring` 除非指定 `--monitor`，否则不尝试与 dmevent 交互。

- `--persistent {y|n}` 设置 y 使指定的次号持久化。

- `--permission {r|w}` 更改访问权限为只读或读写。

- `--readahead {ReadAheadSector|auto}` 设置此逻辑卷的预读扇。

- `--raidsync {check|repair}` 此参数用于启动同步操作。

- `--zero {y|n}` 设置精简池的置零模式。注意：当将 zero 设置为 y 时，从池中从非零模式分配的块在重写部分不会被清除。

# 环境变量

LVM_SUPPRESS_LOCKING_FAILURE_MESSAGES

抑制锁定失败信息的输出。

## 示例

将卷组 vg00 中卷 lvol1 的权限更改为只读：

```
lvchange -pr vg00/lvol1
```

# 另见参见

lvm(8), lvmcache(7), lvmthin(7), lvcreate(8), vgchange(8)

# LVCONVERT

+ > 名称

lvconvert – 将逻辑卷从线性转换为镜像或快照

# 语法

lvconvert -m|mirrors Mirrors [--type SegmentType] [--mirrorlog

{disk<mirrored}] [--corelog] [-R]-resize MirrorLogRegionSize] [---

stripes Stripes [-I--stripize Stripe] [-A--alloc AllocationPolicy] [-b-
