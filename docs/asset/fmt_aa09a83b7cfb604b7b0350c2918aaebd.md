
如果您使用 `system-config-date` 更改时区，此文件将会改变。

## 管理 PCMCIA

移动 Linux 用户利用笔记本的 PCMCIA 插槽添加 70 针、信用卡大小的设备，以支持以太网局域网连接、无线操作、FireWire 设备、Compact Flash 硬盘、外部存储设备、串口和调制解调器。Linux 内核和 David Hinds 的 Card Services 软件支持许多不同类型的 PCMCIA 卡和位于 PCMCIA 托架中的 Compact Flash 外形卡。

PCMCIA 设备和适配器直接通过卡槽供电，尽管某些外部硬件可能需要额外的电源。PCMCIA 支持在启动时启用和配置。然而，在较新的 Linux 内核中，支持是通过内核模块或直接的 Linux 内核支持提供的。

### 使用 PCMCIA

PCMCIA Card Services 软件在插入卡片时通过一个或多个高或低蜂鸣声提供诊断信息。一声高和一声低蜂鸣表明卡片已被识别，但配置失败。单声蜂鸣表明卡片仅被识别。两声高蜂鸣表明卡片已被识别并配置成功。

例如，如果您使用 Compact Flash 存储设备并在运行 Fedora 时将其插入笔记本，您应该会听到两声高蜂鸣。然后，您可以使用 `dmesg` 命令检查哪个设备被分配给该卡片：

```
$ dmesg
...
hde: SunDisk SDCF8-8, ATA DISK drive
hde2 at 0x100-0x107,0x10e on irq 3
ide-floppy driver 0.99.newide
hde: 15680 sectors (8 MB) w/1KiB Cache, CHS=245/2/32
hde: hde1
```

这里没有显示所有输出（您的可能看起来不同），但这个示例表明该卡片已被识别并配置为 `/dev/hde` 设备（包含一个分区 `/dev/hde1`）。然后您可以像使用任何其他存储介质一样使用该设备（有关使用硬盘的更多信息，请参阅第 58 章“管理文件系统”）。

其他设备也可以类似地被识别和配置。例如，如果您有一张以太网和调制解调器组合的 PCMCIA 卡并将其插入笔记本，您应该听到两组高蜂鸣（表示网络接口和调制解调器的识别和配置成功）。Linux 内核将报告接口和设备信息：

```
$ dmesg
...
eth0: NE2000 (DL10019 rev 05): 10BaseT, irq 3, hw_addr 00:E0:98:06:84:C5
ttyS04 at port 0x0af8 (irq = 3) is a 16450
```

在这里，网络接口被识别为 `eth0`（请参阅第 18 章“网络连接”，了解如何连接到网络）。调制解调器被配置为使用 `/dev/ttyS04`。

再次说明，PCMCIA 卡的问题排查可能很困难，特别是随着 802.11b/g 无线网卡在普及度和类型上的爆发式增长。此类故障排除可能需要下载、构建和安装新的驱动程序。

幸运的是，几乎所有串行、调制解调器和 Compact Flash 存储卡都能轻松识别和配置。许多以太网卡也得到支持。若要检查许多卡片的当前支持状态，请阅读 `SUPPORTED.CARDS` 文件。如果您安装了 `pcciacs` RPM 包，会在 `/usr/share/doc/kernel-pcciacs-3.X.XX/` 目录（其中 `X.XX` 是包的版本）下找到其副本。

## 注意

如果在配置和使用 PCMCIA 卡时遇到困难，请浏览 Linux PCMCIA 主页 `http://kernel.org/pub/linux/utils/kernel/pcmcia/pcmcia.html/`。点击“已知问题”链接，查看拥有相同卡片的其他用户是否遇到问题，或者该卡片是否未获得完全支持。如果有新版本的 PCMCIA 内核驱动程序可用，并且您卡片的驱动程序已更改（或已开发出新驱动程序），请下载并安装较新的软件。有关安装新 PCMCIA 模块的信息，请参阅第 39 章，或遵循随 PCMCIA 软件提供的说明。

## 控制 PCMCIA 服务

虽然在使用 Fedora 时可以插入或移除 PCMCIA 卡，但在使用这些卡片时请小心。例如，不要在连接到远程计算机时移除网络卡。不要在卡片的文件系统挂载和使用中拔出 Compact Flash 卡或其他存储介质卡（如 IBM microdrive）——这样做可能会损坏介质的文件系统并导致数据丢失。

您可以从命令行控制 PCMCIA 设备，并在不物理移除和插入卡片的情况下插入和移除卡片。使用 `cardctl` 命令来控制笔记本或带有 PCMCIA 适配器的台式 PC 上一个或多个卡槽的 PCMCIA 服务。`cardctl` 命令用于获取和打印有关已插入卡片的信息，挂起或恢复卡片的电源，重置卡片，执行软件插入或移除，或根据特定的预定义方案（如使用办公室或家庭网络）配置卡片。命令格式为 `cardctl <command> <slot_number>`（例如 0 或 1）。

例如，如果您已插入 Compact Flash 卡，请在卸载其文件系统后使用 `cardctl` 命令及其 `eject` 选项，加上卡槽号来弹出卡片，方法如下：

```
# cardctl eject 0
```

这可以在运行笔记本时节省电力。当再次需要该卡片时，您可以随后像这样“插入”卡片：

```
# cardctl insert 0
```

## 配置和使用 CD、DVD 及 CD-RW 驱动器

Linux 支持使用各种 CD 和 DVD 设备及介质。本节介绍如何确定分配给 CD 驱动器的设备以及获取额外的驱动器信息（如果驱动器支持在光介质上录制）。

AT Attachment Packet Interface，即 ATAPI，基于 IDE 的 CD 驱动器在安装期间被识别，并通过 `ide-cd` 内核模块工作。将创建一个名为 `/dev/cdrom` 的符号链接，指向您的 CD 设备（可能是 `/dev/hdb` 或

你可以在 Linux 上使用多种不同类型的 CD 驱动器，并且可以轻松地更换、添加或升级系统以使用新驱动器。成功配置的一部分包括正确安装硬件，并能够在 Linux 中确定驱动器的设备。

### 检查驱动器分配

如果 CD 和 DVD 驱动器通过正确的线缆连接到你计算机的主板，并且被分配为 IDE 通道上的主设备或从设备，Linux 在启动时就会识别这些驱动器。请查看内核启动消息中的驱动器设备分配，例如：

```
hdd: DVDRAM 10X, ATAPI CD/DVD-ROM drive
```

如果你拥有支持 DVD 的驱动器，通常还应该有一个名为 `/dev/cd` 的符号链接指向你的驱动器设备，因为许多 DVD 客户端（如 xine 或 vlc）默认查找 `/dev/dvd`。如果你拥有 CD-RW 驱动器，Fedora 安装程序会向引导加载器的配置文件中插入一个内核参数，指定使用 ide-scsi 内核。例如：

```
append="hdb=ide-scsi"
```

grub 引导加载器的 `/etc/grub.conf` 文件中类似的条目看起来是这样的：

```
kernel boot/vmlinuz-6.5.1-358 ro root=/dev/hda2 hdb=ide-scsi
```

第一个 CD-RW 驱动器被分配给设备 `/dev/scd0`（尽管在启动时它可能仍被识别为 IDE 设备），后续驱动器依次分配给 `/dev/scd1` 等。为了初始化你的驱动器以便使用，应加载以下模块：

| 模块 | 大小 使用者 未污染 |
|---|---|
| `sg` | 30244 0 (autoclean) |
| `sr_mod` | 15192 0 (autoclean) |
| `cdrom` | 27872 0 (autoclean) [sr_mod] |
| `ide-scsi` | 8128 0 |
| `scsi_mod` | 96572 2 [sr_mod ide-scsi] |

查找有关该设备的内核消息输出，例如：

```
Attached scsi CD-ROM sr0 at scsi0, channel 0, id 0, lun 0
sr0: scsi3-mmc drive: 0x/32x writer cd/rw xa/form2 cdda tray
Uniform CD-ROM driver Revision: 3.12
```

你的基于 ATAPI 的 CD-RW 驱动器随后将在仿真下作为 SCSI 设备工作，符号链接 `/dev/cdrom` 应指向 `/dev/sed0`。你还可以使用 `cdrecord` 命令（包含在红帽的多媒体软件包中）来获取驱动器的 SCSI 设备信息，以便在后续的刻录操作中使用，例如：
