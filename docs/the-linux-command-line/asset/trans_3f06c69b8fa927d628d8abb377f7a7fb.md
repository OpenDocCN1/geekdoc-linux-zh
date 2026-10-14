

Jul 23 10:07:53 linuxbox kernel: usb 3-2: new full speed USB device using uhci_hcd and address 2
Jul 23 10:07:53 linuxbox kernel: usb 3-2: configuration #1 chosen from 1 choice
Jul 23 10:07:53 linuxbox kernel: scsi3 : SCSI emulation for USB Mass Storage devices
Jul 23 10:07:58 linuxbox kernel: scsi scan: INQUIRY result too short (5), using 36
Jul 23 10:07:58 linuxbox kernel: scsi 3:0:0:0: Direct-Access      Easy Disk               1.00 PQ: 0 ANSI: 2
Jul 23 10:07:59 linuxbox kernel: sd 3:0:0:0: [sdb] 31263 512-byte hardware sectors (16 MB)
Jul 23 10:07:59 linuxbox kernel: sd 3:0:0:0: [sdb] Write Protect is off
Jul 23 10:07:59 linuxbox kernel: sd 3:0:0:0: [sdb] Assuming drive cache: write through
Jul 23 10:07:59 linuxbox kernel: sd 3:0:0:0: [sdb] 31263 512-byte hardware sectors (16 MB)
Jul 23 10:07:59 linuxbox kernel: sd 3:0:0:0: [sdb] Write Protect is off
Jul 23 10:07:59 linuxbox kernel: sd 3:0:0:0: [sdb] Assuming drive cache: write through
Jul 23 10:07:59 linuxbox kernel: sdb: sdb1
Jul 23 10:07:59 linuxbox kernel: sd 3:0:0:0: [sdb] Attached SCSI removable disk
Jul 23 10:07:59 linuxbox kernel: sd 3:0:0:0: Attached scsi generic sg3 type 0

显示再次暂停后，输入 Ctrl-c 以返回提示符。输出中有趣的部分是对 “[sdb]” 的重复引用，这与我们对 SCSI 磁盘设备名称的预期相符。已知这一点，以下两行变得特别有启发性：

```
Jul 23 10:07:59 linuxbox kernel: sdb: sdb1
Jul 23 10:07:59 linuxbox kernel: sd 3:0:0:0: [sdb] Attached SCSI removable disk
```

这告诉我们整个设备的设备名为 /dev/sdb，而设备上第一个分区的设备名为 /dev/sdb1。正如我们所见，使用 Linux 充满了有趣的侦探工作！

提示：使用 tail -f /var/log/messages 技术是实时观察系统正在做什么的绝佳方法。

有了设备名，我们现在可以挂载闪存盘：

```
```text
[me@linuxbox ~]$ sudo mkdir /mnt/flash
[me@linuxbox ~]$ sudo mount /dev/sdb1 /mnt/flash
[me@linuxbox ~]$ df
Filesystem              1K-blocks      Used Available Use% Mounted on
/dev/sda2                 15115452   5186944   9776508  35% /
/dev/sda5                 59631908  31777376  24776480  57% /home
/dev/sda1                   147764    172777     122858  57% /boot
tmpfs                       776808         0    776808   0% /dev/shm
/dev/sdb1                    15560         0     15560   0% /mnt/flash
```
```

只要设备保持物理连接到计算机并且计算机未重新启动，设备名就会保持不变。

## 创建新的文件系统

假设我们想用 Linux 原生的文件系统重新格式化闪存盘，而不是它现在使用的 FAT32 系统。这涉及两个步骤：1. （可选）如果现有分区布局不合我们意，则创建新的分区布局，以及 2. 在驱动器上创建新的、空的文件系统。

> **警告！** 在下面的练习中，我们将格式化一个闪存盘。请使用其中没有任何你关心的数据的驱动器，因为它将被擦除！再次强调，**务必确保你为系统指定的设备名是正确的，而不是文中所示的名称。忽视此警告可能会导致你格式化（即擦除）错误的驱动器！**

## 使用 `fdisk` 操作分区

`fdisk` 程序允许我们以非常低的级别直接与类似磁盘的设备（如硬盘驱动器和闪存盘）交互。使用此工具我们可以编辑、删除和创建设备上的分区。要操作我们的闪存盘，我们必须先卸载它（如果需要），然后按如下方式调用 `fdisk` 程序：

```
```text
[me@linuxbox ~]$ sudo umount /dev/sdb1
[me@linuxbox ~]$ sudo fdisk /dev/sdb
```
```

请注意，我们必须指定整个设备，而不是按分区号。程序启动后，我们将看到以下提示：

```
Command (m for help):
```

输入 “m” 将显示程序菜单：

```
Command action
 a  toggle a bootable flag
 b  edit bsd disklabel
 c  toggle the dos compatibility flag
 d  delete a partition
 l  list known partition types
 m  print this menu
 n  add a new partition
 o  create a new empty DOS partition table
 p  print the partition table
 q  quit without saving changes
 s  create a new empty Sun disklabel
 t  change a partition's system id
 u  change display/entry units
 v  verify the partition table
 w  write table to disk and exit
 x  extra functionality (experts only)

Command (m for help):
```

我们想做的第一件事是检查现有的分区布局。我们通过输入 “p” 来打印设备的分区表来实现这一点：

```
Command (m for help): p

Disk /dev/sdb: 16 MB, 16006656 bytes
1 heads, 31 sectors/track, 1008 cylinders
Units = cylinders of 31 * 512 = 15872 bytes

     Device Boot     Start        End      Blocks   Id  System
/dev/sdb1               2       1008      15608+   b  W95 FAT32
```

在此示例中，我们看到一个 16 MB 的设备，有一个分区（1），使用了设备上 1008 个可用柱面中的 1006 个。分区被标识为 Windows 95 FAT32 分区。一些程序会使用此标识符来限制可以对磁盘执行的操作类型，但大多数情况下更改它并不是关键的。然而，在

