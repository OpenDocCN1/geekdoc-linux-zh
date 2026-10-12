

你可以在 Linux 上使用多种不同类型的 CD 驱动器，并且可以轻松地更换、添加或升级系统以使用新驱动器。成功配置的一部分包括正确安装硬件，并能够在 Linux 中确定驱动器的设备。

## 检查驱动器分配

如果 CD 和 DVD 驱动器通过正确的线缆连接到你计算机的主板，并且被分配为 IDE 通道上的主设备或从设备，Linux 在启动时就会识别这些驱动器。请查看内核启动消息中的驱动器设备分配，例如：

```
hdd: DVDRAM 10X, ATAPI CD/DVD-ROM drive
```

如果你拥有支持 DVD 的驱动器，通常还应该有一个名为 `/dev/cd` 的符号链接指向你的驱动器设备，因为许多 DVD 客户端（如 xine 或 vlc）默认查找 `/dev/dvd`。如果你拥有 CD-RW 驱动器，Fedora 安装程序会向引导加载器的配置文件中插入一个内核参数，指定使用 ide-scsi 内核。例如：

```
append="hdb=ide-scsi"
```

grub 引导加载器的 /etc/grub.conf 文件中类似的条目看起来是这样的：

```
kernel boot/vmlinuz-6.5.1-358 ro root=/dev/hda2 hdb=ide-scsi
```

第一个 CD-RW 驱动器被分配给设备 /dev/scd0（尽管在启动时它可能仍被识别为 IDE 设备），后续驱动器依次分配给 /dev/scd1 等。为了初始化你的驱动器以便使用，应加载以下模块：

| 模块 | 大小 使用者 未污染 |
|---|---|
| sg | 30244 0 (autoclean) |
| sr_mod | 15192 0 (autoclean) |
| cdrom | 27872 0 (autoclean) [sr_mod] |
| ide-scsi | 8128 0 |
| scsi_mod | 96572 2 [sr_mod ide-scsi] |

查找有关该设备的内核消息输出，例如：

```
Attached scsi CD-ROM sr0 at scsi0, channel 0, id 0, lun 0
sr0: scsi3-mmc drive: 0x/32x writer cd/rw xa/form2 cdda tray
Uniform CD-ROM driver Revision: 3.12
```

你的基于 ATAPI 的 CD-RW 驱动器随后将在仿真下作为 SCSI 设备工作，符号链接 /dev/cdrom 应指向 /dev/sed0。你还可以使用 cdrecord 命令（包含在红帽的多媒体软件包中）来获取驱动器的 SCSI 设备信息，以便在后续的刻录操作中使用，例如：

```
# cdrecord -scanbus
Cdrecord 1.10 (i686-pc-linux-gnu) Copyright (C) 1995-2001 Jörg Schilling
Linux sg driver version: 3.1.22
Using libscg version 'schily-0.5'
scsibus0:
    0,0,0  0) 'HL-DT-ST' 'RW/DVD GCC-4120B' '2.01' Removable CD-ROM
    0,1,0  1) *
    0,2,0  2) *
    0,3,0  3) *
    0,4,0  4) *
    0,5,0  5) *
    0,6,0  6) *
    0,7,0  7) *
```

相关信息——示例中的 0,0,0（SCSI 总线、设备 ID 和逻辑单元号，即 lun）——随后可以在如下的刻录操作中使用：

```
# cdrecord -v speed=8 dev=0,0,0 -data -eject file_name.img
```

在这个例子中，在 CD-R 或 CD-RW 介质上以 8 倍速创建了一个名为 file_name.img 的 CD-ROM 数据镜像，并且在写入操作完成后新光盘将被弹出。有关创建 CD-ROM 的其他方法，请参阅第 10 章“多媒体应用程序”中的“在 Fedora 中刻录 CD”。

> **注意**
> Fedora 还包含 dvdiscovery、dvd+rw-format 和 growisofs 命令，这些命令可用于 DVD-R 和 DVD-RW 驱动器。

## 初始化 FireWire CD 驱动器

本节提供了一些基本信息，如果你将 FireWire CD 驱动器连接到系统，可以使用这些信息。这些驱动器使用高速串行接口，即 IEEE 1394，其数据传输速度比第一版 USB 快 30 倍以上（速度最高可达 400Mbps），尽管 USB 2.0 设备稍快一些。

自 2.4 系列内核问世以来，Linux 就支持 FireWire，现在可以与许多不同的设备配合使用，例如摄像机、录像机、硬盘、扫描仪、PCMCIA 卡以及 CD、DVD 或 CD-RW 驱动器。Fedora 安装程序应能识别大多数 FireWire 接口硬件；如果识别成功，你就可以在 Linux 中使用该设备。Linux FireFire 组件之一，video1394 内核模块，目前支持超过 120 种不同的数字摄像机。对许多不同的硬盘以及 DVD 或 CD-RW 驱动器提供了一般性支持。

如果你在 Fedora 安装后安装 FireWire 接口，可以通过加载 ieee1394 和 ohci1394 内核模块来初始化对设备（如 CD-RW 驱动器）的支持，方法如下：

```
# insmod ieee1394
# insmod ohci1394
```

接下来，使用 dmesg 命令查找 Linux 内核中相关的设备信息：

```
ohci1394: $Revision: 1.00 $ Ben Collins <bcollins@debian.org>
PCI: Found IRQ 10 for device 00:0b.0
PCI: Sharing IRQ 10 with 00:07.5
ohci1394-0: [002-0] 1.0 (PCI: [R0=] [WIO= [ee000000 ee000080)]
        Max Packet=[2048]
ieee1394: Device added: node 2:1023, GUID 000010500007d8e
ieee1394: sbp2: Driver forced to serialize I/O (serialize_io = 1)
ieee1394: sbp2: Node 2:1023: Max speed [S400] - Max payload [2048]
SCSI: IEEE-1394 SBP-2 protocol driver
        Vendor: TEAC  Model: CD-W28E       Rev: 1.1A
        Type:  CD-ROM                 ANSI SCSI revision: 02
```

在这个例子中，FireWire 驱动程序识别出一个 CD-RW 驱动器（由于系统中还存在另一个 CD-RW，因此它将被分配给 /dev/sd0）。你还会发现 sbp2 内核模块已加载：

```
Module                  Size Used by  Not tainted
sbp2                   14400  0
ohci1394               15872  0 (unseqd)
ieee1394               25760  0 [sbp2 ohci1394]
```

> Fedora 的安装程序应在安装期间识别你 PC 中的任何 FireWire 硬件。
> 根据你的计算机硬件不同，你可能会在 /etc/modprobe.conf 中找到类似 alias ieee1394-controller ohci1394 的条目。

再次，使用 cdrecord 命令及其 -scanbus 选项来获取在 SCSI 仿真下使用驱动器所需的信息：

```
# cdrecord -scanbus
Cdrecord 1.10 (i686-pc-linux-gnu) Copyright (C) 1995-2001 Jörg Schilling
Linux sg driver version: 3.1.22
Using libscg version 'schily-0.5'
scsibus0:
    0,0,0  0) 'HL-DT-ST' 'RW/DVD GCC-4120B' '2.01' Removable CD-ROM
    0,1,0  1) *
    0,2,0  2) *
    0,3,0  3) *
    0,4,0  4) *
    0,5,0  5) *
    0,6,0  6) *
    0,7,0  7) *
scsibus1:
1,0,0  100)  'TEAC' 'CD-W28E' '1.1A' Removable CD-ROM
1,1,0  101)  *
1,2,0  102)  *
1,3,0  103)  *
1,4,0  104)  *
1,5,0  105)  *
1,6,0  106)  *
1,7,0  107)  *
```

FireWire 驱动器的相关信息——示例中的 1,0,0（连接到 SCSI 总线 1 的驱动器，分配设备 0 和 lun 0）——随后可以在如下的读取操作中使用：

```
# export CDDA_DEVICE=1,0,0
# cdda2wav -B
Type: ROM, Vendor 'TEAC' Model 'CD-W28E' Revision '1.1A' MMC+CDDA
724992 bytes buffer memory requested, 4 buffers, 75 sectors
# cdda2wav version 1.10_linux_2.4.17-0.13msp_l686 real time sched. soundcard support
AUDIOTrack pre-emphasis copy-permitted tracktype channels
1-8   no     no    audio 2
Table of Contents: total tracks:8, (total time 52:12.72)
1.( 5:25.67), 2.( 9:06.65), 3.( 5:50.68), 4.( 5:35.57), 5.( 7:28.35)
6.( 6:34.60), 7.( 6:07.15), 8.( 6:01.05),
Table of Contents: starting sectors
1.(    0), 2.( 24442), 3.( 65457), 4.( 91775), 5.( 116957)
6.( 150592), 7.( 180202), 8.( 207742), lead-out( 234822)
CDINDEX discid: S8RXDC1u_.D2S6uIMwgTksIY0UE.
CDDB discid: 0x5e0c3a08
CD-Text: not detected
CD-Extra: not detected
samplefile size will be 552301388 bytes.
recording 3130.09600 seconds stereo with 16 bits @ 44100.0 Hz ->'audio'...percent_done:
100% track 1 successfully recorded
100% track 2 successfully recorded
...
```

在这个例子中，创建了一个名为 CDDA_DEVICE 的环境变量，其中包含驱动器的 SCSI 信息，并使用 cdda2wav 命令将整个音频 CD 的内容提取为 .wav 文件格式，每个曲目保存为单独的文件。其他实用程序可能只需要知道设备名称，例如 `/dev/scd1`，如下所示：

```bash
# cdparanoia -d /dev/scd1 -B
cdparanoia 1.11 release 9.8 (March 23, 2001)
(C) 2001 Monty <monty@xiph.org> and Xiphophorous

Report bugs to paranoia@xiph.org
http://www.xiph.org/paranoia/

  Couldn't disable kernel command translation layer
Ripping from sector     0 (track 1 [0:00.00])
   to sector 234821 (track 8 [6:01.04])
```

输出到 `track01.cdda.wav`

> **注意**
> Fedora 还包含 `cdrdao` 命令，它可以创建磁盘一次性（DAO）音频和数据 CD-ROM。Linux 驱动程序和某些 CD 驱动器支持的其他 CD 刻录类型包括逐次轨道（Track-At-Once）和逐次会话（Session-At-Once），这些会在录制过程的各个阶段打开和关闭驱动器的激光。

在这个例子中，使用了 CD-RW 设备名称，同样，音频 CD 上的所有曲目将被提取并保存为 `.wav` 音频文件。Fedora 还包含其他图形客户端，如 **xine**、**grip** 和 **xcdroast**，可用于创建或复制音频和数据 CD。有关刻录 CD 的更多详细信息，请参阅第 10 章。

## 配置无线网络

过去，在 Linux 上配置无线网络非常麻烦，需要很多复杂的步骤才能连接到无线网络。然而，Fedora 5 包含了一个名为 NetworkManager 的出色实用程序，使连接和管理无线网络变得极其简单。得益于 Fedora Linux 内核中包含的几个无线芯片组驱动程序，现在连接 WEP 和 WPA 加密的无线网络变得非常容易。

如果你拥有基于 Intel Centrino 的系统，则需要从 `http://ipw2200.sourceforge.net` 获取最新固件，将其解包并将文件内容复制到 `/lib/firmware`。对于基于 Broadcom 的无线系统，你需要获取 **fwcutter** 程序从相关的驱动程序文件中提取固件。请访问 `http://tinyurl.com/ceemyd` 获取有关在哪里获取驱动程序文件以及如何使用 **fwcutter** 的完整说明。提取固件后，你需要将其放置在 `/lib/firmware` 目录中。拥有一套固件文件后，你需要在 `system-config-services` 中激活 NetworkManager 以及 NetworkManager Dispatcher。

