
```
[root@wizard src]# cdrecord -v -isosize speed=4 dev=2,0 ksource.img
Cdrecord release 1.8a17 Copyright 1995-1998 Jörg Schilling
TOC Type: 1 = CD-ROM
scsidev: '2,0'
scsibus: 0 target: 2 lun: 0
atapi: 0
Device type : Removable CD-ROM
```

```
Version : 2
Response Format: 2
Capabilities :
Vendor_info :
Identifikation : 'CD-R/RW RW7040S '
Revision : '1.10'
ATIP info from disk:
Indicated writing power: 4
Is not unrestricted
Is not erasable
ATIP start of lead in: 23276 (15:39/01)
ATIP start of lead out: 72226 (116:05/01)
Disk type unknown
Manufacturer unknown (not in table)
Blocks total: 333226 Blocks current: 306013 Blocks remaining: 278956
Starting to write CD/DVD at speed 4 in write mode for single session.
Last chance to quit, starting real write in 1 seconds.
Waiting for reader process to fill input-buffer ... input-buffer ready.
Starting new track at sector: 0
Track 01: 52 of 52 MB written (fifo 100%).
Track 01: Total bytes read/written: 55420928/55420928 (27061 sectors).
Writing time: 94.725s
Fixating...
Fixating time: 61.882s
cdrecord: fifo had 1692 puts and 1692 gets.
cdrecord: fifo was 0 times empty and 1473 times full, min fill was 94%.
```

```
[root@wizard src]# mount -t iso9660 /dev/scd0 /mnt/cdrom
mount: block device /dev/scd0 is write-protected, mounting read-only

[root@wizard src]# cd /mnt/cdrom

[root@wizard cdrom]# ls
COPYING README drivers ipc net
CREDITS README.kernel-sources fs kernel pcmcia-cs-3.0.9
Documentation REPORTING-BUGS ibcs lib scripts
MAINTAINERS Rules.make include mm
Makefile arch init modules

[root@wizard src]# umount /mnt/cdrom

[root@wizard src]# eject scd0
```

为了构建合适的 ISO 命令行，我们首先使用 `-scanbus` 选项发出 `cdrecord` 命令。这为我们提供了要使用的适当设备条目。然后我们指定写入磁盘的写入速度。在本例中，附带的刻录机以 4 倍速写入，因此我们指定速度为 4。如果在刻录图像时机器完全空闲，有时可以将速度设置为高于设备指定的速度。然而，在实际刻录 CD-R 光盘之前，您可能希望使用 `-dummy` 选项先尝试一下，看看是否可行。`-dummy` 选项会执行刻录 CD-R 的所有步骤，只是不会激活激光。它是一个非常有用的调试工具，可以帮您避免制造太多金色 coaster。其他选项指定您想要详细输出并使用 ISO9660 文件系统大小作为下一轨道的大小。刻录完成后，您接下来应该做的是验证写入是否成功。为此，您只需挂载创建的 CD 并尝试从中读取即可。

现在您已经知道如何在 Linux 下向 CD-R 和 CD-RW 驱动器写入数据，您可以出于各种目的使用这些知识。其中一个用途可以是创建内核或其他软件构建的备份。其他用途包括专用备份；例如，您必须保留但不足以写入磁带的网站日志文件，或您希望快速访问的文件。另一个变得流行的用途是创建您不经常使用但在需要时希望快速访问的软件包映像。现在我们已经介绍了 CD 的创建，我们可以继续讨论其他可移动媒体设备，从连接到系统并口的设备开始。

## 并口存储设备

最近变得相当流行的其他可移动媒体设备是经由并口连接到计算机的存储设备。这些设备包括 Iomega 的驱动器，如 Zip 和 Jaz 驱动器，它们使用驱动程序使它们在 Linux 中表现为 SCSI 设备，以及 SyQuest 和 MicroSolutions 等其他制造商的 ATAPI/IDE 设备。本节将介绍为这些类型的设备向内核添加支持所需的条件，然后特别介绍 Zip 驱动器，因为它们是这些设备中较为流行的一种。本讨论仅涉及连接到并口的 Zip 驱动器。如果您的 Zip 驱动器连接到 IDE 控制器或 SCSI 控制器，它应作为另一个 SCSI 或 IDE 设备出现在系统中。

## 向内核添加支持

为并口存储设备向内核添加支持的第一步是确定您需要哪个驱动程序。基本上共有三种选择。其中第一个是 `ppa` 驱动程序，适用于较旧的并口 Zip 驱动器。对于较新的 Zip 驱动器，如 ZIP Plus 和 250 兆字节 Zip 驱动器，请使用 `imm` 驱动程序（Iomega MatchMaker）。这两个驱动程序都是 Linux SCSI 支持的一部分，并在内核配置中配置为低级 SCSI 驱动程序。对于并口 ATAPI 或 IDE 设备，有一个名为 `paride` 的驱动程序。该驱动程序适用于通过并口连接的多种外部存储设备，包括以下内容：

- MicroSolutions 背包 CD-ROM
- MicroSolutions 背包 PD/CD
- MicroSolutions 背包硬盘
- MicroSolutions 背包 8000t 磁带驱动器
- SyQuest EZ-135、EZ-230 & SparQ 驱动器
- Avatar Shark
- Imation Superdisk LS-120
- Maxell Superdisk LS-120
- FreeCom Power CD
- Hewlett-Packard 5GB 和 8GB 磁带驱动器
- Hewlett-Packard 7100 和 7200 CD-RW 驱动器

为 `ppa` 或 `imm` 驱动程序添加支持的步骤与为任何其他类型的 SCSI 设备添加支持的步骤相同。您必须首先选择 SCSI 设备的支持，然后选择特定类型的 SCSI 设备（磁盘、CD、磁带和通用），最后选择控制器的特定低级驱动程序。在低级驱动程序级别，您选择 `ppa` 或 `imm` 驱动程序。这些选项根据它们支持的 Zip 驱动器类型明确标记，如果您对哪个驱动程序合适还有进一步疑问，内核配置帮助包含有价值的信息。

`paride` 支持配置选项位于内核配置的块设备部分。您必须首先回答并口 IDE 设备支持问题，使用 M 构建为模块或 Y 编译到内核中。然后您将被提示选择要支持的设备类型，与 SCSI 设备配置类似。完成此操作后，您需要根据要支持的设备类型选择一个或多个协议模块。再次强调，配置帮助在这里是您的朋友，如果不确定，您可以启用所有协议作为模块，让驱动程序自行判断。

假设您使用的是 Red Hat 6.1 发行版提供的内核，并且使用的是随附的 2.2.12 内核，则无需执行上述任何步骤。内核已配置好，并将 `ppa`、`imm` 和 `paride` 驱动程序以及相关协议作为模块支持。

## Zip 驱动器

假设您使用的是默认的 Red Hat 内核，或已成功重新构建内核以支持第 35 章所述的您拥有的 Zip 驱动器类型，您实际上如何使用该驱动器？涉及两个基本步骤：

1. 加载适当的驱动模块。
2. 装入 Zip 磁盘并使用它。

加载模块只需使用 `insmod` 或 `modprobe` 并指定正确的驱动程序。为本示例的目的，我们假设使用 `imm` 驱动程序的现代 ZIP Plus 驱动器。在这种情况下，您将发出的命令和示例输出如下
