
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

相关信息——示例中的 `0,0,0`（SCSI 总线、设备 ID 和逻辑单元号，即 `lun`）——随后可以在如下的刻录操作中使用：

```
# cdrecord -v speed=8 dev=0,0,0 -data -eject file_name.img
```

在这个例子中，在 CD-R 或 CD-RW 介质上以 8 倍速创建了一个名为 `file_name.img` 的 CD-ROM 数据镜像，并且在写入操作完成后新光盘将被弹出。有关创建 CD-ROM 的其他方法，请参阅第 10 章“多媒体应用程序”中的“在 Fedora 中刻录 CD”。

> **注意**
>
> Fedora 还包含 `dvdiscovery`、`dvd+rw-format` 和 `growisofs` 命令，这些命令可用于 DVD-R 和 DVD-RW 驱动器。

## 初始化 FireWire CD 驱动器

本节提供了一些基本信息，如果你将 FireWire CD 驱动器连接到系统，可以使用这些信息。这些驱动器使用高速串行接口，即 IEEE 1394，其数据传输速度比第一版 USB 快 30 倍以上（速度最高可达 400Mbps），尽管 USB 2.0 设备稍快一些。

自 2.4 系列内核问世以来，Linux 就支持 FireWire，现在可以与许多不同的设备配合使用，例如摄像机、录像机、硬盘、扫描仪、PCMCIA 卡以及 CD、DVD 或 CD-RW 驱动器。Fedora 安装程序应能识别大多数 FireWire 接口硬件；如果识别成功，你就可以在 Linux 中使用该设备。Linux FireFire 组件之一，`video1394` 内核模块，目前支持超过 120 种不同的数字摄像机。对许多不同的硬盘以及 DVD 或 CD-RW 驱动器提供了一般性支持。

如果你在 Fedora 安装后安装 FireWire 接口，可以通过加载 `ieee1394` 和 `ohci1394` 内核模块来初始化对设备（如 CD-RW 驱动器）的支持，方法如下：

```
# insmod ieee1394
# insmod ohci1394
```

接下来，使用 `dmesg` 命令查找 Linux 内核中相关的设备信息：

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

在这个例子中，FireWire 驱动程序识别出一个 CD-RW 驱动器（由于系统中还存在另一个 CD-RW，因此它将被分配给 `/dev/sd0`）。你还会发现 `sbp2` 内核模块已加载：

```
Module                  Size Used by  Not tainted
sbp2                   14400  0
ohci1394               15872  0 (unseqd)
ieee1394               25760  0 [sbp2 ohci1394]
```

> Fedora 的安装程序应在安装期间识别你 PC 中的任何 FireWire 硬件。

> 根据你的计算机硬件不同，你可能会在 `/etc/modprobe.conf` 中找到类似 `alias ieee1394-controller ohci1394` 的条目。

再次，使用 `cdrecord` 命令及其 `-scanbus` 选项来获取在 SCSI 仿真下使用驱动器所需的信息：

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

FireWire 驱动器的相关信息——示例中的 `1,0,0`（连接到 SCSI 总线 1 的驱动器，分配设备 0 和 `lun` 0）——随后可以在如下的读取操作中使用：

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
