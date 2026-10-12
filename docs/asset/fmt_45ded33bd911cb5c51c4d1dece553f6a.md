
在互联网上出售你的旧硬盘之前，擦除它可能是个主意。通过简单的重新分区、使用`Windows`格式工具，甚至在执行`mkfs`命令后，某些`Debian`用户仍然能够读取磁盘上的大部分数据。

```
root@debian6~# aptitude search foremost sleuthkit | tr -s ' ''
p autopsy - Sleuthkit 的图形界面
p foremost - 用于恢复数据的应用程序
p sleuthkit - 用于取证分析的工具集
```

虽然`/bin/badblocks`工具上是为了查找坏块，但你可以使用它完全擦除磁盘上的所有数据。由于这确实是在写入磁盘的每个扇区，这可能需要很长时间！

```
root@RHELVau2:~# badblocks -ws /dev/sdb
Testing with pattern 0xaa: done
Reading and comparing: done
Testing with pattern 0x55: done
Reading and comparing: done
Testing with pattern 0xff: done
Reading and comparing: done
Testing with pattern 0x00: done
Reading and comparing: done
```

之前的截图覆盖了磁盘每个扇区四次。使用`dd`这样的工具擦除一次就足以破坏所有数据。

警告，此截图显示了如何永久破坏块设备上的所有数据。

```
root@rhel65 ~]# dd if=/dev/zero of=/dev/sdb
```

## 4.5. 高级硬盘设置

硬盘设置的调优（`dma`, `gap`, ...）不在本课程的范围内。有几个工具可用，`hdparm`和`sdparm`就是其中两个。

`hdparm`可用于显示或设置关于`ATA`（或`SATA`）硬盘设备的信息和参数。`-i`和`-l`选项将为你提供有关设备物理属性的更多信息。

```
root@laika:~# hdparm /dev/sdb

dev/sdb:
Io_support = 0 (default 16-bit)
readonly = 0 (off)
readahead = 256 (on)
geometry = 12261/255/63, sectors = 195371568, start = 0
```

以下是关于一个`200GB` `IDE`硬盘的`hdparm`信息。

```
root@barry:~# hdparm /dev/hdd

dev/hdd:
multcount = 0 (off)
Io_support = 0 (default)
umaskirq = 0 (off)
using_dma = 1 (on)
keepsettings = 0 (off)
readonly = 0 (off)
readahead = 256 (on)
geometry = 24321/255/63, sectors = 390721968, start = 0
```

这里是`Ubuntu` `10.10`上`sdparm`的截图。

```
root@ubulu010:~# aptitude install sdparm
...
root@ubulu010:~# sdparm /dev/sda | head -1
/dev/sda: ATA FUJITSU MJA2160B 0081
root@ubulu010:~# man sdparm
```

谨慎使用`hdparm`和`sdparm`。

## 4.6. 练习：硬盘设备

**关于本实验：** 为了练习操作硬盘，你需要一些硬盘。当没有物理硬盘可用时，你可以使用`vmware`或`VirtualBox`中的虚拟磁盘。老师将帮助你将几个`ATA`和/或`SCSI`磁盘附加到虚拟机。本实验的结果可以用于接下来的实验（分区、文件系统、挂载）。

建议在虚拟机上附加三个`1GB`磁盘和三个`2GB`磁盘。这将为本章节以及后续章节（`raid`, `svm`, `lscsi`）的练习提供灵活性。

1. 使用`dmesg`列出启动时检测到的硬盘设备列表。
2. 使用`fdisk`查找系统中所有硬盘设备的总大小。
3. 停止虚拟机，添加三个虚拟`1GB` `scsi`硬盘设备和一个虚拟`400MB` `ide`硬盘设备。如果可能，再添加另一个虚拟`400MB`的`ide`磁盘。
4. 使用`dmesg`验证所有新硬盘在启动时均已被正确检测。
5. 验证你可以在`/dev`中看到磁盘设备。
6. 使用`fdisk`（配合`grep`和`/dev/null`）显示新硬盘的总大小。
7. 使用`badblocks`完全擦除其中一个较小的硬盘。
8. 查看`/proc/scsi/scsi`。
9. 如果可能，安装`sscsi`、`lshw`并使用它们列出磁盘。

## 4.7. 硬盘设备

1. 使用`dmesg`列出启动时检测到的硬盘设备列表。

一些可能的答案...

```
dmesg | grep -i disk

查找 ATA 磁盘：dmesg | grep -i "ata disk"

查找 SCSI 磁盘：dmesg | grep -sd[a-f]

查找 SCSI 磁盘：dmesg | grep -i "scsi disk"
```

2. 使用`fdisk`查找系统中所有硬盘设备的总大小。

```
fdisk -l
```

3. 停止虚拟机，添加三个虚拟`1GB` `scsi`硬盘设备和一个虚拟`400MB` `ide`硬盘设备。如果可能，再添加另一个`400MB`的`ide`磁盘。

此练习在`vmare`或`VirtualBox`的设置中完成。

4. 使用`dmesg`验证所有新硬盘在启动时均已被正确检测。

参见第 1 点。

5. 验证你可以在`/dev`中看到磁盘设备。

```
SCSI+SATA: ls -l /dev/sd*

ATA: ls -l /dev/hdv*
```

6. 使用`fdisk`（配合`grep`和`/dev/`）显示新硬盘的大小。

```
roothel53 ~ # fdisk -l 2>/dev/null | grep [MGT]B
Disk /dev/hda: 21.4 GB, 2298648480 bytes
Disk /dev/hdb: 1073 MB, 1125417712 bytes
Disk /dev/sda: 217 MB, 227483648 bytes
Disk /dev/sdb: 217 MB, 227483648 bytes
Disk /dev/sdc: 217 MB, 227483648 bytes
```

7. 使用`badblocks`完全擦除其中一个较小的硬盘。

```
# 在输入前确认要擦除的设备 (/dev/sdX?)
roothel53 ~ # badblocks /dev/sdc
Testing with pattern 0aa:
Reading and comparing: done
Testing with pattern 0x55:
Reading and comparing: done
Testing with pattern 0xff:
Reading and comparing: done
Testing with pattern 0x00:
Reading and comparing: done
Reading and comparing: done
```

8. 查看`/proc/scsi/scsi`。

```
roothel53 ~ # cat /proc/scsi/scsi
Attached devices:
Host: scsi: 00 Id: 02
Vendor: VBOX HARDDISK: 1.0
Type: Direct-Access SCSI 05
Host: scsi: 00 Id: 03
Vendor: VBOX HARDDISK: 1.0
Type: Direct-Access SCSI 05
Host: scsi: 00 Id: 06
Vendor: VBOX HARDDISK: 1.0
Type: Direct-Access SCSI 05
```

9. 如果可能，安装`lsscs`、`lshw`并使用它们列出磁盘。

`Debian`: `aptitude install lshw`

`Fedora`: `yum install lshw`

```
root@rhel53 # lsscs
[0:0:2:0] disk VBOX HARDDISK: 1.0 /dev/sda
[0:0:3:0] disk VBOX HARDDISK: 1.0 /dev/sdb
[0:0:6:0] disk VBOX HARDDISK: 1.0 /dev/sdc
```

## 5. 分区

本章继续上一节的硬盘设备。我们将在这些设备上进行分区。本章为下一节（在分区上创建文件系统）做准备。

## 5.1. 关于分区

### 5.1.1. 主、扩展和逻辑分区
