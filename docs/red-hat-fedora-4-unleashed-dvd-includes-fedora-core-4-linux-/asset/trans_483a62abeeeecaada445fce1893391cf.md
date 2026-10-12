
IBM微型驱动器），而卡的文件系统当前仍处于挂载并使用状态——这可能会损坏介质的文件系统并导致数据丢失。

你可以从命令行控制PCMCIA设备，并在不物理取出和插入卡的情况下对卡进行插入和移除操作。使用 `cardctl` 命令来管理你的笔记本电脑或带有PCMCIA适配器的台式电脑上一个或多个卡槽的PCMCIA服务。`cardctl` 命令用于获取并打印关于已插入卡的信息，挂起或恢复卡的供电，重置卡，执行软件插入或移除，或根据特定的预定义“方案”（例如在办公室或家庭使用网络）来配置卡。该命令的格式为 `cardctl command slot_number`（例如 0 或 1）。

例如，如果你插入了一张紧凑闪存卡，在使用 `cardctl` 命令及其 `eject` 选项并配合卡的插槽编号（如以下所示）弹出卡（在卸载其文件系统之后）：

```bash
# cardctl eject 0
```

这在运行笔记本电脑时可以为电池省电。当再次需要该卡时，你可以随后像这样“插入”该卡：

```bash
# cardctl insert 0
```

## 配置和使用 CD、DVD 及 CD-RW 驱动器

Linux 提供对使用各种 CD 和 DVD 设备及介质的支持。本节展示了如何确定分配给你的 CD 驱动器的设备，以及如果驱动器支持在光学介质上进行录制，如何获取额外的驱动器信息。

AT 附加接口包（AT Attachment Packet Interface，或称 ATAPI）基于 IDE 的 CD 驱动器在安装过程中被识别，并通过 `ide-cd` 内核模块工作。将创建一个名为 `/dev/cdrom` 的符号链接，指向你的 CD 设备（可能是 `/dev/hdb` 或 `/dev/hdc`）。你可以使用许多不同类型的 CD 驱动器配合 Linux 工作，并且可以轻松地替换、添加或升级你的系统以使用新的驱动器。成功配置的一部分涉及硬件的正确安装，以及在 Linux 中能够确定驱动器的设备。

### 检查驱动器分配

如果 CD 和 DVD 驱动器通过适当的线缆连接到计算机主板，并且在 IDE 通道上被分配为主设备或从设备，Linux 在启动时会识别它们。查看内核启动消息以了解驱动器设备分配，例如：

```text
hdd: DVDRAM 10X, ATAPI CD/DVD-ROM drive
```

如果你有一个支持 DVD 的驱动器，通常你也应该有一个指向你的驱动器设备的、名为 `/dev/dvd` 的符号链接，因为许多 DVD 客户端（如 `xine` 或 `vlc`）默认会寻找 `/dev/dvd`。如果你有一个 CD-RW 驱动器，Fedora 安装程序会将一个内核参数插入到你的引导装载器配置文件中，指定使用 `ide-scsi` 内核模块。例如：

```text
append="hdb=ide-scsi"
```

grub 引导装载器的 `/etc/grub.conf` 文件中类似的条目如下所示：

```text
kernel boot/vmlinuz-6.5-1.358 ro root=/dev/hda2 hdb=ide-scsi
```

第一个 CD-RW 驱动器将被分配给设备 `/dev/scd0`（尽管在启动时它可能最初仍被识别为 IDE 设备），后续驱动器依次分配给 `/dev/scd1`，以此类推。为了初始化你的驱动器以供使用，应加载以下模块：

| 模块 | 大小 | 使用者 | 未污染 |
|---|---|---|---|
| sg | 30244 | 0 | (autoclean) |
| sr_mod | 15192 | 0 | (autoclean) |
| cdrom | 27872 | 0 | (autoclean) [sr_mod] |
| ide-scsi | 8128 | 0 | |
| scsi_mod | 96572 | 2 | [sr_mod ide-scsi] |

寻找内核关于该设备的消息输出，例如以下内容：

```text
Attached scsi CD-ROM sr0 at scsi0, channel 0, id 0, lun 0
sr0: scsi3-mmc drive: 0x/32x writer cd/rw xa/form2 cdda tray
Uniform CD-ROM driver Revision: 3.12
```

你的基于 ATAPI 的 CD-RW 驱动器随后将作为 SCSI 设备在模拟模式下工作，符号链接 `/dev/cdrom` 应指向 `/dev/scd0`。你还可以使用 `cdrecord` 命令（随红帽多媒体软件包提供）来获取关于驱动器的 SCSI 设备信息，供后续在刻录操作中使用，例如：

```bash
# cdrecord -scanbus
cdrecord 1.10 (i686-pc-linux-gnu) Copyright (C) 1995-2001 Jörg Schilling
Linux sg driver version: 3.1.22
Using libscg version 'schily-0.5'
scsibus0:
	0,0,0   0) 'HL-DT-ST' 'RW/DVD GCC-4120B' '2.01' Removable CD-ROM
	0,1,0   1) *
	0,2,0   2) *
	0,3,0   3) *
	0,4,0   4) *
	0,5,0   5) *
	0,6,0   6) *
	0,7,0   7) *
```

相关信息——例如示例中的 `0,0,0`（SCSI 总线、设备 ID 和逻辑单元号，即 lun）——可以在刻录操作中像这样使用：

```bash
# cdrecord -v speed=8 dev=0,0,0 -data -eject file_name.img
```

在此示例中，一个名为 `file_name.img` 的 CD-ROM 数据映像被创建在 CD-R 或 CD-RW 介质上，速度为 8，并且在写入操作完成后新光盘将被弹出。有关创建 CD-ROM 的其他方法，请参见第 10 章“多媒体应用”中的“在 Fedora Core Linux 中刻录 CD”。

> **注意**
> Fedora 还包含 `dvdrecord`、`dvd+rw-format` 和 `growisofs` 命令，这些命令可用于 DVD-R 和 DVD-RW 驱动器。

## 初始化 FireWire CD 驱动器

本节提供了一些基本信息，如果你将 FireWire CD 驱动器连接到系统，可以使用这些信息。这些驱动器使用高速串行接口，也称为 IEEE 1394，其数据传输速度比第一代 USB 快 30 倍以上（速度可达 400Mbps），尽管 USB 2.0 设备稍快一些。

Linux 自 2.4 系列内核问世以来就支持 FireWire，现在可以与许多不同的设备一起工作，例如摄像机、录像机、硬盘、扫描仪、PCMCIA 卡，以及 CD、DVD 或 CD-RW 驱动器。Fedora Core 安装程序应能识别大多数 FireWire 接口硬件；如果是这样，你将能够在 Linux 中使用该设备。Linux FireWire 组件之一，`video1394` 内核模块，目前支持 120 多种不同的数字摄像机。对许多不同的硬盘以及 DVD 或 CD-RW 驱动器都有通用支持。

如果在 Fedora 安装完成后才安装 FireWire 接口，你可以通过加载 `ieee1394` 和 `ohci1394` 内核模块来初始化对设备（如 CD-RW 驱动器）的支持，例如：

```bash
# insmod ieee1394
# insmod ohci1394
```

接下来，使用 `dmesg` 命令从 Linux 内核中寻找相关的设备信息：

```text
ohci1394: $Revision: 1.80 $ Ben Collins <bcollins@debian.org>
PCI: Found IRQ 10 for device 00:0b.0
PCI: Sharing IRQ 10 with 00:07.5
ohci1394_0: OHCI-1394 1.0 (PCI): IRQ=[10] MMIO=[ee000000-ee008000] \
  Max Packet=[2048]
ieee1394: Device added: node 2:1023, GUID 00d0010500007d8e
ieee1394: sbp2: Driver forced to serialize I/O (serialize_io = 1)
ieee1394: sbp2: Node 2:1023: Max speed [S400] - Max payload [2048]
scsi1 : IEEE-1394 SBP-2 protocol driver
 Vendor: TEAC  Model: CD-W28E  Rev: 1.1A
 Type:  CD-ROM        ANSI SCSI revision: 02
```

在此示例中，FireWire 驱动器已识别出一个 CD-RW 驱动器（该驱动器将被分配给 `/dev/scd1`，因为系统中还存在另一个 CD-RW 驱动器）。你也可能会发现 `sbp2` 内核模块已加载：

| 模块 | 大小 | 使用者 | 未污染 |
|---|---|---|---|
| sbp2 | 14400 | 0 | |
| ohci1394 | 15872 | 0 | (unused) |
| ieee1394 | 25768 | 0 | [sbp2 ohci1394] |

> **注意**
> Fedora 安装程序在安装过程中应能识别你的 PC 中的任何 FireWire 硬件。
> 根据你电脑的硬件情况，你可能会在 `/etc/modprobe.conf` 中发现这样的条目，例如 `alias ieee1394-controller ohci1394`。

再次使用 `cdrecord` 命令及其 `-scansbus` 选项来获取在 SCSI 模拟下使用驱动器所需的信息：

```bash
# cdrecord -scansbus
Cdrecord 1.10 (1686-pc-linux-gnu) Copyright (C) 1995-2001 Jörg Schilling
Linux sg driver version: 3.1.22
Using libscg version 'schily-0.5'
scsibus:0:
	0,0,0	0) 'HL-DT-ST ' 'RW/DVD GCC-4120B ' '2.01' Removable CD-ROM
	0,1,0	1) *
	0,2,0	2) *
	0,3,0	3) *
	0,4,0	4) *
	0,5,0	5) *
	0,6,0	6) *
	0,7,0	7) *
scsibus:1:
	1,0,0	100) 'TEAC ' 'CD-W28E ' '1.1A' Removable CD-ROM
	1,1,0	101) *
	1,2,0	102) *
	1,3,0	103) *
	1,4,0	104) *
	1,5,0	105) *
	1,6,0	106) *
	1,7,0	107) *
```
