
```
root@barry:~# hdparm /dev/hdd
/dev/hdd:
multcount     = 0 (off)
Io_support    = 0 (default)
unmaskirq      = 0 (off)
using_dma     = 1 (on)
keepsettings  = 0 (off)
readonly      = 0 (off)
readhead     = 256 (on)
geometry      = 24321/255/63, sectors = 390721968, start = 0
```

这里是 `Ubuntu 10.10` 上 `sdparm` 的截图。

```
root@ubulu1010:~# aptitude install sdparm
...
root@ubulu1010:~# sdparm /dev/sda | head -1
/dev/sda: ATA  FUJITSU MJA2160B  0081
root@ubulu1010:~# man sdparm
```

请谨慎使用 `hdparm` 和 `sdparm`。

## 5.6. 练习：硬盘设备

**关于本实验：** 为了练习操作硬盘，你需要一些硬盘。当没有物理硬盘可用时，可以使用 `VMware` 或 `VirtualBox` 中的虚拟磁盘。老师将帮助你向虚拟机附加几个 `ATA` 和/或 `SCSI` 磁盘。本实验的结果可以用于接下来的三个实验（分区、文件系统、挂载）。

建议向虚拟机挂载三个 `1GB` 的磁盘和两个 `2GB` 的磁盘。这将为本章以及后续章节（`raid`, `lvm`, `iSCSI`）的练习提供一定的操作灵活性。

- 1. 使用 `dmesg` 列出启动时检测到的硬盘设备列表。
- 2. 使用 `fdisk` 查找系统中所有硬盘设备的总大小。
- 3. 停止虚拟机，添加三个虚拟 `1GB` `SCSI` 硬盘设备和一个虚拟 `400MB` `IDE` 硬盘设备。如果可能，再添加另一个虚拟 `400MB` 的 `IDE` 磁盘。
- 4. 使用 `dmesg` 验证所有新磁盘在启动时均已被正确检测。
- 5. 验证你是否可以在 `/dev` 中看到磁盘设备。
- 6. 使用 `fdisk`（配合 `grep` 和 `/dev/null`）显示新硬盘的总大小。
- 7. 使用 `badblocks` 完全擦除其中一块较小的硬盘。
- 8. 查看 `/proc/scsi/scsi`。
- 9. 如果可能，安装 `lsscsi`、`lshw` 并使用它们列出磁盘。

## 5.7. 答案：硬盘设备

- 1. 使用 `dmesg` 列出启动时检测到的硬盘设备列表。

一些可能的答案……

```
dmesg | grep -i disk
Looking for ATA disks: dmesg | grep -i "ata disk"
Looking for SCSI disks: dmesg | grep -sd[a-f]
Looking for SCSI disks: dmesg | grep -i "scsi disk"
```

- 2. 使用 `fdisk` 查找系统中所有硬盘设备的总大小。

```
fdisk
```

- 3. 停止虚拟机，添加三个虚拟 `1GB` `SCSI` 硬盘设备和一个虚拟 `400MB` `IDE` 硬盘设备。如果可能，再添加另一个虚拟 `400MB` 的 `IDE` 磁盘。

此操作在 `VMware` 或 `VirtualBox` 的设置中。

- 4. 使用 `dmesg` 验证所有新磁盘在启动时均已被正确检测。

见 1。

- 5. 验证你是否可以在 `/dev` 中看到磁盘设备。

```
SCSI: ls -l /dev/sd*
ATA: ls -l /dev/hd*
```

- 6. 使用 `fdisk`（配合 `grep` 和 `/dev/null`）显示新硬盘的总大小。

```
root@rhel53 # fdisk -l 2>/dev/null | [MGT]
Disk/dev/hda: 21.4 GB, 21447836480 bytes
Disk/dev/hdb: 1073 MB, 1125899912 bytes
Disk/dev/sda: 2147 MB, 2144783648 bytes
Disk/dev/sdb: 2147 MB, 2144783648 bytes
Disk/dev/sdc: 2147 MB, 2144783648 bytes
```

- 7. 使用 `badblocks` 完全擦除其中块较小的硬盘。

```
# 在输入此命令前验证你想擦除的设备 (/dev/sd?)
# nroot@rhel53 # badblocks -ws /dev/sdc
Testing with pattern 0xaa:
Reading and comparing: done
Testing with pattern 0x55:
Reading and comparing: done
Testing with pattern 0xff:
Reading and comparing: done
Testing with pattern 0x00:
Reading and comparing: done
```

- 8. 查看 `/proc/scsi/scsi`。

```
root@rhel53 ~ # cat /proc/scsi/scsi
```

### 已附加设备：

```
Host: scsi0 Channel: 00 Id: 02 Lun: 00
Vendor: VBOX Model: HARDDISK Rev: 1.0
Type: Direct-Access ANSI SCSI revision: 05
Host: scsi0 Channel: 00 Id: 02 Lun: 00
Vendor: VBOX Model: HARDDISK Rev: 1.0
Type: Direct-Access ANSI SCSI revision: 05
Host: scsi0 Channel: 00 Id: 02 Lun: 00
Vendor: VBOX Model: HARDDISK Rev: 1.0
Type: Direct-Access ANSI SCSI revision: 05
```

- 9. 如果可能，安装 `lsscsi`、`lshw` 并使用它们列出磁盘。

## 6.2.3. `parted` 以及其他

你可能对 `fdisk` 的替代方案感兴趣，如 `parted`、`cfdisk`、`sfdisk` 和 `gparted`。本课程主要使用 `fdisk` 对磁盘进行分区。

某些 Linux 发行版推荐使用 `parted` 来处理使用 `gpt` 而非 `mbr` 的存储。

下面是 `CentOS` 上运行 `parted` 的截图。

```
[root@centos65 ~]# rpm -q parted
parted-2.1.1-21.el16.x86_64
[root@centos65 ~]# parted /dev/sda
GNU Parted 2.1
Using /dev/sda
Welcome to GNU Parted! Type 'help' to view a list of commands.
(parted) print
Model: ATA VBOX HARDDISK (scsi)
Disk /dev/sda: 42.9GB
Sector size (logical/physical): 512B/512B
Partition Table: msdos

Number  Start   End     Size    Type    File system Flags
1       1049kB 525MB  524MB   primary  ext4      boot
2       525MB  42.9GB 42.4GB  primary                  lvm
```

`parted`

## 6.3. 磁盘分区

在下面的示例中，我们为系统购买了一块磁盘。新硬件已正确连接，你可以使用 `fdisk` 和 `parted` 创建必要的分区。此示例使用了 `fdisk`，但使用 `parted` 也没有问题。

### 6.3.1. 识别磁盘

首先，我们通过 `fdisk -l` 检查 `Linux` 是否能看到新磁盘。是的，可以看到新磁盘，被识别为 `/dev/sda`，但它还没有任何分区。

```
root@RHELvu2:~# fdisk -l

Disk /dev/sda: 12.8 GB, 1288490188 bytes

255 heads, 63 sectors/track, 1566 cylinders

Units = cylinders of 16065 * 512 = 8225280 bytes

Device Boot      Start         End  Id System

/dev/sda          *      13   104391 83 Linux

/dev/sda2                14   1556 12744742+  8e Linux LVM
```
