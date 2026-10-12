
```
27061 extents written (52 Mb)

[root@madmax linux-2.2.5]# mount -t iso9660 -o loop=/dev/loop0,ro ../ksource.img /mnt/cdrom

[root@madmax linux-2.2.5]# cd /mnt/cdrom

[root@madmax cdrom]# ls -a
.  MAINTAINERS  Rules.make  include  mm
..  Makefile  arch  init  modules
COPYING  README  drivers  ipc  net
CREDITS  README.kernel.sources  fs  kernel  pcmcia-cs-3.0.9
Documentation  REPORTING-BUGS  ibcs  lib  scripts

[root@madmax cdrom]# cd

[root@madmax /root]# umount /mnt/cdrom
```

正如你所见，内核源代码树中的长文件名已被转换为 ISO9660 标准规定的 8.3 格式。然而，由于我们指定了 -r 选项，并且 Linux 支持 ISO9660 的 Rock Ridge 扩展，当映像被挂载时，文件名显示起来就像原始源代码树中一样。通常最好挂载你创建的映像以验证文件系统映像是否正确创建。你可以通过使用 loop 设备和 mount 命令的 loop 选项来实现这一点。另一个有趣的选项是使用多个 -m 选项来排除对象文件、库存档以及如果在源代码树中构建了内核就会存在的其他文件。

现在映像已经创建，你可以使用 cdwrite 或 cdrecord 命令将映像传输到 CD-R 或 CD-RW 介质。这两个命令中，只有 cdrecord 包含在 Red Hat 安装介质中。选择使用这两个命令中的哪一个取决于你，选择取决于对硬件和其他你可能需要的功能的支持。请注意 cdrecord 正在积极维护，而 cdwrite 则没有。如果没有你需要的特定功能仅在 cdwrite 中受支持，我建议你坚持使用 cdrecord。如果想从源码构建，这些软件包可从以下 FTP 站点获取，或者如果你更喜欢预编译的二进制文件，也可以从 Red Hat contrib 镜像获取：

ftp://ftp.fokus.gmd.de/pub/unix/cdrecord/ (cdrecord)
ftp://sunsite.unc.edu/pub/Linux/utils/disk-management/ (cdwrite)

确保获取适合你的硬件的相应命令。为了我们的示例，我们将使用 cdrecord 命令，因为它支持 ATAPI 以及 SCSI 设备。cdrecord 命令支持大量命令行选项，其中一些最常见的选项在表 10.3 中描述。选项类型指示选项可能出现在命令行上的位置。所有通用选项必须在任何轨道选项或轨道文件名之前指定。

## 表 10.3 cdrecord 命令行选项

| 选项 | 类型 | 描述 |
|---|---|---|
| -version | 通用 | 打印 cdrecord 版本信息并退出。 |
| -v | 通用 | 增加通用详细程度级别 1。 |
| -V | 通用 | 增加 SCSI 命令传输详细程度 1。 |
| -debug | 通用 | 打印额外的调试信息。 |
| -dummy | 通用 | 在激光关闭的情况下执行刻录的所有步骤。 |
| -multi | 通用 | 允许创建多会话 CD。此选项必须用于磁盘的所有会话中，除最后一个外。 |
| -msinfo | 通用 | 以适合 mkisofs 命令与 -c 选项一起使用的格式检索多会话信息。 |
| -toc | 通用 | 显示 CD 的目录或 PMA 信息。 |
| -fix | 通用 | 仅固定磁盘。 |
| -nofix | 通用 | 不固定磁盘。用于分步创建音频盘。 |
| speed=# | 通用 | 将写入过程的速度因子设置为 #。 |
| blank=type | 通用 | 擦除 CD-RW 磁盘并退出，或在写入前擦除磁盘。要获取擦除类型列表，将 type 设置为 help。 |
| dev=target | 通用 | 写入由 target 指定的设备。target 的格式为 devicename:scsibus, scsid, lun。可缩短为唯一标识驱动器所需的部分。（示例：dev=0,2,0 表示总线 0，ID 2，Lun 0） |
| -checkdrive | 通用 | 检查当前驱动器的驱动程序是否存在并退出。退出状态 0 表示成功。 |
| -scanbus | 通用 | 显示总线上所有 SCSI 设备的查询字符串。 |
| -inq | 通用 | 显示设备查询信息并退出。 |

### 表 10.3 继续

| 选项 | 类型 | 描述 |
|---|---|---|
| -prcap | 通用 | 显示 SCSI-3/mmc 驱动器的驱动能力。 |
| -audio | 轨道 | 所有后续轨道以 CD-DA 音频格式写入磁盘。 |
| -data | 轨道 | 所有后续轨道以 CD-ROM 模式 1 格式写入磁盘。 |
| -mode2, -xa1, -xa2, -cdi | 轨道 | 所有后续轨道以指定格式写入磁盘（CD-ROM 模式 2、CD-ROM XA 模式 1、CD-ROM XA 模式 2 或 CDI 格式）。 |
| -swab | 轨道 | 假定音频数据为字节交换（小端）顺序。 |
| -isosize | 轨道 | 使用 ISO9660 文件系统大小作为下一个轨道的大小。 |

为了继续我们的示例，我们现在将使用 cdrecord 将使用 mkisofs 创建的映像写入 CD-R 磁盘。由于刻录过程的敏感性，最好在机器相对空闲时执行此操作。此过程需要持续的数据流，如果设备总线负载或系统负载中断此流，将发生缓冲区欠载。然后正在写入的磁盘将变得无用，除非你碰巧正在创建移动或类似金色的杯垫。以下是将我们的 ISO9660 映像写入磁盘然后挂载并验证写入是否成功的命令示例。

```
[root@wizard src]# cdrecord -scanbus
Cdrecord release 1.8a17 Copyright 1995-1998 Jörg Schilling
scsibus0:
0) *
1) *
2) * 'CD-R/RW RW7040S ' '1.10' Removable CD-ROM
3) *
4) *
5) *
6) *
7) *
```

```
[root@wizard src]# cdrecord -dummy -v -isosize speed=4 dev=2,0 ksource.img
Cdrecord release 1.8a17 Copyright 1995-1998 Jörg Schilling
TOC Type: 1 = CD-ROM
scsidev: '2,0'
scsibus: 0 target: 2 lun: 0
atapi: 0
```

```
Device type : Removable CD-ROM
Version : 2
Response Format: 2
Capabilities :
Vendor_info :
Identifikation : 'CD-R/RW RW7040S '
Revision : '1.10'
Device seems to be: Generic mmc CD-RW.
Using generic SCSI-3/mmc CD-R driver (mmc_cdr).
Driver flags : SWABAUDIO
Track 01: data 52 MB
Total size: 60 MB (06:00.84) = 27063 sectors
Lout start: 61 MB (06:02/63) = 27063 sectors
Current Secsize: 2048
ATIP info from disk:
Indicated writing power: 4
Is not unrestricted
Is not erasable
ATIP start of lead in: 23276 (15:39/01)
ATIP start of lead out: 72226 (116:05/01)
Disk type unknown
Manufacturer unknown (not in table)
Blocks total: 333226 Blocks current: 333226 Blocks remaining: 306163
Starting to write CD/DVD at speed 4 in dummy mode for single session.
Last chance to quit, starting dummy write in 1 seconds.
Waiting for reader process to fill input-buffer ... input-buffer ready.
Starting new track at sector: 0
Track 01: Track 01: 52 of 52 MB written (fifo 100%).
Track 01: Total bytes read/written: 55420928/55420928 (27061 sectors).
Writing time: 93.369s
Fixating...
WARNING: Some drives don't like fixation in dummy mode.
Fixating time: 0.013s
cdrecord: fifo had 1602 puts and 1692 gets.
cdrecord: fifo was 0 times empty and 1530 times full, min fill was 96%.
```

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
