
```
usb 2-1.2: USB device strings: Mfr=1,Product=2, SerialNumber=3
usb 2-1.2: Flash Disk
usb 2-1.2: Manufacturer: Usb2
usb 2-1.2: SerialNumber: 0000565851111ED
usb 2-1.2: configuration #1 chosen from 1 choice
Initializing USB Mass Storage driver...
scsi 6s0:00 emulation for USB Mass Storage devices
usbcore: registered new interface driver usb-storage
USB Mass Storage registered.
usb-storage: device found at 3
usb-storage: waiting for device to settle before scanning
usb-storage: device scan complete
scsi 6:0:0:0: Direct-Access Us 2.0 Flash Disk 2.10 PQ: 0 ANSI: 2
sd 6:0:0:0: Attached scsi gq2 type 0
sd [sdb]: 4072448 512-byte logical blocks: (2.08 GB/1.94 GiB)
sd 6:0:0:0: [sdb] Write Protect is off
sd 6:0:0:0: [sdb] Mode Sense: 00 00 08
sd 6:0:0:0: [sdb] Assuming drive cache: write through
sd 6:0:0:0: [sdb] Assuming drive cache: write through
sdb:
sd 6:0:0:0: [sdb] Assuming drive cache: write through
sd 6:0:0:0: [sdb] Attached removable disk
SELinux: initialized (dev sdb, type vfat), uses genfs_contexts
[root@h ~]#
```

## 挂载设备

在找到 USB 驱动器的设备名称后，你还需要确定该设备上是否有分区。`fdisk -l` 命令将帮助你完成。假设你的 USB 驱动器在服务器上标识为 `/dev/sdb`，你必须使用 `fdisk -l /dev/sdb` 来查看 USB 驱动器的当前分区情况。列表 3.2 显示了它的样子。

**列表 3.2:** 使用 `fdisk -l` 显示分区信息

```
[root@hnl]# fdisk -l /dev/sdb
Disk /dev/sdb: 4127 MB, 427195136 bytes
94 heads, 600 sectors/track, 1429 cylinders, total 8060928 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x84556ad2
```

| Device | Boot | Start | End | Blocks | Id | System |
|---|---|---|---|---|---|---|
| `/dev/sdb1` | | 2048 | 806927 | 402940 | 83 | Linux |

在列表 3.2 中，你可以看到 `/dev/sdb` 上只有一个分区，它被称为 `/dev/sdb1`。现在你已经知道了分区的名称，可以将其挂载到目录上。如果你只想临时挂载一次分区，`/mt` 目录是一个托管临时内存的极佳选择。如果你打算多次使用该挂载点，可能希望使用 `mkdir` 为你的设备创建一个目录。要将设备 `/dev/sdb` 挂载到目录 `/mt`，你可以使用以下命令：

`mount /dev/sdb /mt`

此时，如果你使用 `cd` 进入了 `/mt` 目录，你将看到 USB 驱动器的内容。现在你可以通过挂载来使用 USB 驱动器。

**3.3:** 使用 `mount` 显示已挂载的设备

```
usb 2-1.2: USB device strings: Mfr=1,Product=2, SerialNumber=3
usb 2-1.2: Flash Disk
usb 2-1.2: Manufacturer: Usb2
usb 2-1.2: SerialNumber: 0000565851111ED
usb 2-1.2: configuration #1 chosen from 1 choice
Initializing USB Mass Storage driver...
scsi 6s0:00 emulation for USB Mass Storage devices
usbcore: registered new interface driver usb-storage
USB Mass Storage registered.
usb-storage: device found at 3
usb-storage: waiting for device to settle before scanning
usb-storage: device scan complete
scsi 6:0:0:0: Direct-Access Us 2.0 Flash Disk 2.10 PQ: 0 ANSI: 2
sd 6:0:0:0: Attached scsi gq2 type 0
sd [sdb]: 4072448 512-byte logical blocks: (2.08 GB/1.94 GiB)
sd 6:0:0:0: [sdb] Write Protect is off
sd 6:0:0:0: [sdb] Mode Sense: 00 00 08
sd 6:0:0:0: [sdb] Assuming drive cache: write through
sd 6:0:0:0: [sdb] Assuming drive cache: write through
sdb:
sd 6:0:0:0: [sdb] Assuming drive cache: write through
sd 6:0:0:0: [sdb] Attached removable disk
SELinux: initialized (dev sdb, type vfat), uses genfs_contexts
[root@h ~]#
```

### 练习 3.5: 挂载 U 盘

在此练习中，你将学习如何挂载 U 盘。

1. 打开终端，确保你有 root 权限。
2. 插入 U 盘。
3. 使用 `dmesg` 找到 U 盘的名称。
4. 使用 `fdisk -l` 查看 U 盘的分区。
5. 使用 `mount` 将分区挂载到某个目录。
6. 使用 `cd` 进入该挂载目录。
7. 使用 `ls -l` 查看 U 盘的内容。
8. 使用 `umount` 卸载 U 盘。
9. 尝试在未挂载的情况下使用它，你会看到“设备忙”错误。
10. 使用 `cd` 退出目录。

### 现实场景：理解设备命名

在服务器上，通常没有图形界面。这意味着你需要手动完成挂载。如果服务器连接了许多存储设备（这在数据中心很常见），你的设备可能不会是 `/dev/sdb`，而可能是 `/dev/sdc`（当字母表用完 `/dev/sdz` 后，下一个设备是 `/dev/sda`）。要找出你刚刚连接的设备名称，`dmesg` 是非常有用的。

## 使用链接

在 Linux 文件系统中，从不同的位置访问同一个文件是非常有用的。这可以防止你将文件复制到不同的位置，从而在那些位置产生该文件的多个版本。在 Linux 文件系统中，你可以使用链接来实现这一目的。链接看起来像是一个普通文件，但它更像是一个指向另一个位置的指针。

对于符号链接，原始文件和链接之间存在区别。如果你删除了原始文件，符号链接将无法工作并失效。硬链接可以指向位于同一设备上的文件。

在 Linux 中，有两种链接类型。符号链接是你可以使用的最灵活的链接类型。硬链接可以指向位于同一设备上的文件。

### 练习 3.6

### 创建链接

在本次练习中，你将学习如何创建链接。你将为 `/etc/hosts` 文件创建一个硬链接和一个符号链接，并看到它们的行为有何不同。

1. 打开终端，并确保你拥有 root 权限。
2. 使用命令 `ln -s /etc/hosts ~/symhosts`。这会在你的主目录下创建一个名为 `symhosts` 的符号链接。
