
可移动设备在连接时会被命名。首先，实时查看 `/var/log/messages` 文件（你可能需要超级用户权限）：

```
[me@linuxbox ~]$ sudo tail -f /var/log/messages
```

文件最后几行会显示出来，然后暂停。接下来，插入可移动设备。在本例中，我们将使用一个 16MB 的闪存盘。几乎立即，内核就会注意到该设备并对其进行探测：

```
Jul 23 10:07:53 linuxbox kernel: usb 3-2: new full speed USB device using uhci_hcd and address 2
Jul 23 10:07:53 linuxbox kernel: usb 3-2: new full speed USB device using uhci_hcd and address 2
Jul 23 10:07:53 linuxbox kernel: scsi3 : SCSI emulation for USB Mass Storage devices
Jul 23 10:07:58 linuxbox kernel: scsi scan: INQUIRY result too short (5), using 36
Jul 23 10:07:58 linuxbox kernel: scsi 3:0:0:0: Direct-Access Easy Disk 1.00 PQ: 0 ANSI: 2
Jul 23 10:07:59 linuxbox kernel: sd 3:0:0:0: [sdb] 3125 512-byte hardware sectors (16 MB)
Jul 23 10:07:59 linuxbox kernel: sd 3:0:0:0: [sdb] Write Protect is off
Jul 23 10:07:59 linuxbox kernel: sd 3:0:0:0: [sdb] Assuming drive cache: write through
Jul 23 10:07:59 linuxbox kernel: sd 3:0:0:0: [sdb] 3125 512-byte hardware sectors (16 MB)
Jul 23 10:07:59 linuxbox kernel: sd 3:0:0:0: [sdb] Write Protect is off
Jul 23 10:07:59 linuxbox kernel: sd 3:0:0:0: [sdb] Assuming drive cache: write through
Jul 23 10:07:59 linuxbox kernel: sdb: sdb1
Jul 23 10:07:59 linuxbox kernel: sd 3:0:0:0: [sdb] Attached SCSI removable disk
Jul 23 10:07:59 linuxbox kernel: sd 3:0:0:0: Attached scsi generic sg3 type 0
```

当显示再次暂停后，按下 CTRL-C 返回提示符。输出中值得注意的部分是反复出现的 [sdb]，这符合我们对 SCSI 磁盘设备名称的预期。知道了这一点，两行输出就显得格外清晰：

```
Jul 23 10:07:59 linuxbox kernel: sdb: sdb1
Jul 23 10:07:59 linuxbox kernel: sd 3:0:0:0: [sdb] Attached SCSI removable disk
```

这告诉我们，整个设备的名称是 /dev/sdb，而设备上的第一个分区是 /dev/sdb1。正如我们所见，使用 Linux 意味着大量有趣的侦探工作！

注意：使用 `tail -f /var/log/messages` 这个技巧是近乎实时观察系统动态的好方法。

知道了设备名称，我们现在就可以挂载闪存盘：

```
[me@linuxbox ~]$ sudo mkdir /mnt/flash
[me@linuxbox ~]$ sudo mount /dev/sdb1 /mnt/flash
[me@linuxbox ~]$ df
```

| 文件系统 | 1K块 | 已用 | 可用 | 已用% | 挂载点 |
|---|---|---|---|---|---|
| /dev/sda2 | 15115452 | 5186944 | 9975164 | 35% | / |
| /dev/sda5 | 59631908 | 31777376 | 2477640 | 57% | /home |
| /dev/sda1 | 1477564 | 172777 | 1222858 | 13% | /boot |
| tmpfs | 776808 | 0 | 776808 | 0% | /dev/shm |
| /dev/sdb1 | 15560 | 0 | 15560 | 0% | /mnt/flash |

只要设备保持物理连接到计算机，并且计算机未重启，设备名称就会保持不变。

## 创建新的文件系统

假设我们想用 Linux 原生文件系统重新格式化闪存盘，而不是它现在使用的 FAT32 系统。这涉及两步：首先，（可选地）如果现有分区布局不合意，就创建新的分区布局；其次，在驱动器上创建一个新的空文件系统。

**警告：** *在接下来的练习中，我们将格式化一个闪存盘。请使用一个你不在乎其中数据的驱动器，因为它将被擦除！再次强调，务必确保你指定的是你系统上正确的设备名称，而不是文中所示的那个。忽视此警告可能导致格式化（即擦除）错误的驱动器！*

## 使用 fdisk 操作分区

fdisk 程序允许我们在非常低的层次上直接与类磁盘设备（如硬盘驱动器和闪存驱动器）交互。利用此工具，我们可以编辑、删除和创建设备上的分区。要操作我们的闪存盘，必须先卸载它（如果需要），然后按如下方式调用 fdisk 程序：

```
[me@linuxbox ~]$ sudo umount /dev/sdb1
[me@linuxbox ~]$ sudo fdisk /dev/sdb
```

注意，我们必须指定整个设备，而不是按分区号来指定。程序启动后，我们将看到以下提示符：

```
Command (m for help):
```

输入 m 将显示程序菜单：

```
Command action
 a toggle a bootable flag
 b edit bsd disklabel
 c toggle the dos compatibility flag
 d delete a partition
 l list known partition types
 m print this menu
 n add a new partition
```
