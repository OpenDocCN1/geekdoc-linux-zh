
```
linux~$ mount
/dev/sda2 on / type ext4 (rw)
/proc on /proc type proc (rw)
/sys on /sys type sysfs (rw)
/dev/pts on /dev/pts type devpts (gid=5,mode=620)
/dev/sda1 on /home type ext4 (rw)
/dev/shm on /dev/shm type tmpfs (rw,nosatime)
/dev/loop0 on /dev/loop0 type squash (ro)
/dev/loop1 on /dev/loop1 type squash (ro)
/dev/loop2 on /dev/loop2 type squash (ro)
/dev/loop3 on /dev/loop3 type squash (ro)
/dev/loop4 on /dev/loop4 type squash (ro)
/dev/loop5 on /dev/loop5 type squash (ro)
/dev/loop6 on /dev/loop6 type squash (ro)
/dev/loop7 on /dev/loop7 type squash (ro)
/dev/loop8 on /dev/loop8 type squash (ro)
/dev/loop9 on /dev/loop9 type squash (ro)
/dev/loop10 on /dev/loop10 type squash (ro)
/dev/loop11 on /dev/loop11 type squash (ro)
/dev/loop12 on /dev/loop12 type squash (ro)
/dev/loop13 on /dev/loop13 type squash (ro)
/dev/loop14 on /dev/loop14 type squash (ro)
/dev/loop15 on /dev/loop15 type squash (ro)
```

## 提示

Ubuntu 用户会发现列表被“loop”设备占满了。要查看更整洁的列表，请尝试这些命令：`mount -v` 或 `mount | grep dev`。

列表格式如下：`设备 on 挂载点 type 类型 (选项)`。例如，第一行显示 `/dev/sda2` 挂载在根目录，类型为 `ext4`，且可读可写。该列表的底部还有两个有趣的条目。

对于我们的实验，我们将使用一个 4GB 的闪盘。首先，让我们在插入驱动器之前查看系统：

```
me@linuxbox~$ mount | grep dev
/dev/sda2 on / type ext4 (rw)
/dev/sda1 on /boot type vfat (rw,relatime,uid=1000,gid=1000,fmask=0022,dmask=0000)
/dev/sdb on / type ext4 (rw)
```

像许多 Linux 系统一样，该系统在插入后会自动挂载驱动器。在我们插入驱动器后，会看到：

```
me@linuxbox~$ mount | grep dev
/dev/sda2 on / type ext4 (rw)
/dev/sda1 on /boot type vfat (rw,relatime,uid=1000,gid=1000,fmask=0022,dmask=0000)
/dev/sdb on / type ext4 (rw)
/dev/sdc on /media/me/C911-C314 type vfat (rw,relatime,uid=1000,gid=1000,fmask=0022,dmask=0000)
```

# 警告

在接下来的示例中，你务必密切关注系统中的实际设备名称，不要使用本文中使用的名称！

现在我们已经知道了 U 盘的设备名称，让我们卸载该驱动并将其挂载到文件系统树中的另一个位置。要做到这一点，我们需要成为超级用户（使用适用于我们系统的命令），并使用 `umount` 命令（注意拼写）卸载驱动。

```
[me@linuxbox~]# sudo -i
[sudo] password for me:
[root@linuxbox~]# umount /dev/sdc
```

下一步是为磁盘创建一个新的挂载点。挂载点仅仅是文件系统树某处的一个目录。它没什么特别的。它不一定是一个空目录，但如果你将设备挂载到非空目录上，那么在卸载设备之前，你将无法看到该目录之前的内容。出于目的，我们将创建一个新目录。

```
[root@linuxbox~]# mkdir /mnt/flash
```

最后，我们将 U 盘挂载到新的挂载点上。`-t` 选项用于指定文件系统类型。

```
[root@linuxbox ~]# mount -t vfat /dev/sdc /mnt/flash
```

之后，我们可以通过新的挂载点查看 U 盘的内容。

```
[root@linuxbox ~]# cd /mnt/flash
[root@linuxbox cd]# ls
```

注意当我们尝试卸载驱动时的情况。

```
[root@linuxbox cd]# umount /dev/sdc
unmount: /mnt/flash: device is busy
```

这是为什么？原因是如果设备正在被某人或进程使用，我们就无法卸载它。在这种情况下，我们将工作目录更改为了 U 盘的挂载点，这导致设备处于忙状态。我们可以通过将工作目录更改挂载点以外的地方来轻松解决这个问题。

```
[root@linuxbox cd]# cd
[root@linuxbox ~]# umount /dev/sdc
```

现在设备成功卸载了。

![](img/58edd539af3a70704734cedc1ac0c271_196_0.png)

如果你查看 `free` 命令的输出（它显示内存使用的统计信息），你会看到一个名为 `buffers`（缓冲区）的统计数据。计算机系统的设计目标是尽可能快。影响系统速度的障碍之一是慢设备。打印机就是一个很好的例子。最快的打印机在计算机标准来看也极其缓慢。如果计算机必须停下来等待打印机完成一页的打印，它的速度将非常慢。在 PC 的早期时代（多任务处理之前），这是一个真实的问题。如果你正在处理电子表格或文本文档，计算机将以它能接受的最快速度将数据发送到打印机，由于打印机并不快，速度很慢。这个问题随着打印机缓冲出现得到了解决，缓冲区是一个包含一些 RAM 内存的设备，位于计算机和打印机之间。有了缓冲区，计算机会将打印机输出发送到缓冲区，数据会被快速存储在 RAM 中，这样计算机就可以不受干扰地继续工作。同时，打印机缓冲区会以打印机可以接受的速度从打印机内存中缓慢吐出数据。

这种缓冲思想在计算机中被广泛用于提高其运行速度。不要让偶尔读取或写入慢速设备的需求阻碍系统速度。操作系统会将从存储设备读取和要写入存储设备的数据尽可能长时间存储在内存中，而不是与较慢的设备进行交互。在 Linux 系统上，你会注意到系统运行时间越长，内存占用就越高。这并不意味着 Linux 正在“使用”所有内存；这意味着 Linux 正在利用所有可用内存来尽可能地进行缓冲。

这种缓冲允许向存储设备写入变得非常快，因为向物理设备的写入被推迟到了未来的某个时刻。在此期间，目标设备的数据会在内存中堆积。操作系统会不定期将这些数据写入物理设备。

卸载设备意味着将剩余数据写入设备，以便能够安全地移除。如果在未先卸载的情况下就移除设备，可能存在并非所有设备数据都已传输的情况。在某些情况下，这些数据可能包含关键的目录更新，这将导致文件系统损坏，这是计算机上可能发生的最糟糕的事情之一。

## 确定设备名称

有时确定设备名称是困难的。在过去，这并不困难。设备总是位于同一个位置且不会改变。类 Unix 系统就是这样工作的，但更换磁盘驱动器涉及到使用叉车从机房里移出一台洗衣机大小的设备。近年来，典型的桌面硬件配置已变得非常动态化，Linux 也已经进化得比其祖先更加灵活。

在之前的示例中，我们利用了现代 Linux 桌面“自动”挂载设备并在事后确定名称的能力。但如果我们正在管理服务器或其他不发生这种情况的环境呢？我们该如何找出它呢？

首先，让我们看看系统是如何命名设备的。如果我们列出 `/dev` 目录（所有设备所在地）的内容，我们可以看到非常多的设备。

```
[me@linuxbox ~]$ ls /dev
```

此列表的内容揭示了一些设备命名的模式。表 15-2 概述了这些模式之一。

### 表 15-2：Linux 存储设备

| 模式 | 设备 |
| :--- | :--- |
| `/dev/fd*` | 软盘驱动器。 |
| `/dev/bd*` | 旧系统上的 IDE (PATA) 磁盘。这些系统的主板有两个 IDE 连接器或通道，每个通道有两个连接点。第一个磁盘称为主设备（master），第二个是从设备（slave）。设备名称的顺序是：`/dev/hda` 指第一个通道的主设备，`/dev/db` 指第二个通道，以此此类推。数字表示设备分区号。例如，`/dev/sda1` 指硬盘的第一个分区，`/dev/sda` 指整个设备。 |
| `/dev/lp*` | 打印机。 |
| `/dev/sd*` | SCSI 磁盘。在现代 Linux 系统中，内核将所有磁盘设备（包括 PATA/SATA 硬盘、U 盘、USB 存储设备和数字相机）视为 SCSI 磁盘。其余的命名与之前的 `/dev/bd` 类似。 |
| `/dev/sr*` | 光学驱动器（CD/DVD 阅读器和刻字机）。 |

此外，我们经常看到如 `/dev/cdrom`、`/dev/dvd` 和 `/dev/floppy` 等符号链接，其目的是方便。如果我们工作的系统不自动管理热拔设备，可以使用以下技术确定设备在连接时的命名。首先，启动 `/var/log/messages` 或 `/var/log/syslog` 的实时视图（这可能需要超级用户权限）。

```
[me@linuxbox ~]$ sudo tail -f /var/log/syslog
```

在基于 systemd 的系统中，使用此命令跟踪 systemd 日志。

```
[me@linuxbox ~]$ sudo journalctl -f
```

显示几行后将暂停。接下来，插入热拔设备。在这个示例中，我们将卸载并重新插入 U 盘。内核几乎立即注意到并探测它。

```
Jul 25 13:15:07 kernel: mtp-probe[21318]: checking bus 3, device 8: "/sys/devices/pctl0000:00/0000:00:14.0/usb3-6"
Jul 25 13:15:07 kernel: mtp-probe[21318]: bus 3, device 8 is not an MTP device
Jul 25 13:15:07 kernel: mtp-probe[21321]: checking bus 3, device 8: "/sys/devices/pctl0000:00/0000:00:14.0/usb3-6"
Jul 25 13:15:07 kernel: mtp-probe[21321]: bus 3, device 8 is not an MTP device
Jul 25 13:15:08 kernel: scsi 0:0:0:0: Direct-Access General 5.00
Q: 0 ANSI: 2
Jul 25 13:15:08 kernel: sd 6:0:0:0: [sd] Attached scsi generic sg3 type 0
Jul 25 13:15:08 kernel: sd 6:0:0:0: [sd] 7084320 512-byte logical blocks: (4.03 GB/3.5 GB)
Jul 25 13:15:08 kernel: sd 6:0:0:0: [sd] Write Protect is off
Jul 25 13:15:08 kernel: sd 6:0:0:0: [sd] Mode Sense: 00 00 00 00
Jul 25 13:15:08 kernel: sd 6:0:0:0: [sd] No Caching cache found
Jul 25 13:15:08 kernel: sd 6:0:0:0: [sd] Assuming drive cache write through
Jul 25 13:15:08 kernel: sdc
Jul 25 13:15:08 kernel: sd 6:0:0:0: [sd] Attached SCSI removable disk
```

显示再次暂停后，按下 CTRL-C 回到提示符。反复出现的 `[sd]` 符号我们对 SCSI 设备名称的预期。通过这一点，这两行变得特别具有启发性：

```
Jul 25 13:15:08 kernel: sdc:
Jul 25 13:15:08 kernel: sd 6:0:0:0: [sd] Attached SCSI removable disk 
```

> 使用 `tail -f /var/log/syslog` 或 `journalctl -f` 技术是实时观察系统操作的极佳方法。

确定设备名称的方法还有一种（在 Linux 中总有多种方法）。我们可以使用 `lsblk` 命令。此命令列出所有连接到系统的块设备，无论它们是否已挂载。

假设我们已经卸载并移除了 U 盘，我们可以查看块设备列表。

```
[me@linuxbox ~]$ lsblk
NAME MAJ:MIN SIZE TYPE MOUNTPOINTS
sda 8:0 111.8G disk
└─sda1 8:1 976M /part/efi
```

```
sda3 8:3 0 14.9G 0 part [SWAP]
sdb 8:16 0 931.5G 0 disk
sdb1 8:17 0 922.2G 0 part /home
sdb2 8:18 0 9.3G 0 part
sr0 11:0 1 1024M 0 rom
```

接下来，我们将重新插入 U 盘并运行 `lsblk`。

```
[me@linuxbox-]$ df
NAME MIN RM SIZE TYPE MOUNTPOINTS
sda 8:0 0 111.8G 0 disk
sda1 8:1 0 976M 0 part /boot/efi
sda3 8:3 0 14.9G 0 part [SWAP]
sdb 8:16 0 931.5G 0 disk
sdb1 8:17 0 922.2G 0 part /home
sdb2 8:18 0 9.3G 0 disk
sdc 8:32 1 3.8G 0 disk
sr0 11:0 1 1024M 0 rom
```

我们看到列表中添加了一个新设备 (`sdc`)。由于该设备是物理连接到计算机的且计算机没有重启，其设备名称将保持不变。

拿到设备名称后，我们可以挂载 U 盘。

```
[me@linuxbox-]$ sudo mount /dev/sdc /mnt/flash
[me@linuxbox-]$ df
```

| Filesystem | K-blocks | Used | Available | % | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| tmpfs | 1624184 | 2144 | 1622040 | 1% | / |
| /dev/sda2 | 98403196 | 45133696 | 48285032 | 49% | / |
| tmpfs | 8128098 | 0 | 8128098 | 0% | /dev/shm |
| tmpfs | 5120 | 4 | 5116 | 1% | /root/lock |
| /dev/sda1 | 997456 | 6220 | 991236 | 1% | /boot/efi |
| /dev/sdb1 | 95090656 | 58574576 | 36174994 | 65% | /home |
| tmpfs | 1624180 | 0 | 1624180 | 1% | /run/user/120 |
| tmpfs | 1624180 | 0 | 1624180 | 1% | /run/user/1000 |
| /dev/sdc | 3924444 | 4 | 3924440 | 1% | /mnt/flash |

## 创建文件系统

假设我们有一个只有一个 FAT32 文件系统的外部 USB 硬盘，并想将硬盘划分为：一个 Linux 原生文件系统 (`ext4`) 和另一个格式化为 NTFS 以供 Windows 系统使用的分区。这涉及两个步骤：

- 1. 创建新的分区布局。
- 2. 在磁盘上创建新的空文件系统。

## 警告

在接下来的练习中，我们将格式化一个外部硬盘。请使用不包含任何重要数据的硬盘，因为它将被擦除！再次强调，确保你为系统指定了正确的设备名称，而不是文中显示的名称。不注意此警告可能会导致你格式化（即擦除）错误的硬盘！

### 使用 parted 操作分区

`parted` 是主机程序（包括命令行和图形界面）之一，它允许我们在非常底层上直接与磁盘类设备（如硬盘和 U 盘）进行交互。我们将挂载硬盘并使用 `parted` 获取它的名称。

```
NAME SIZE RM TYPE MOUNTPOINTS
sda 8:0 0 111.8G disk
|--sda1 8:1 0 976M part /boot/efi
|--sda3 8:3 0 14.9G part [SWAP]
sdb 8:16 0 931.5G disk disk
|--sdb1 8:17 0 922.2G part /home
|--sdb2 8:18 0 9.3G part
sdd 8:32 0 232.9G disk disk
|--sdd1 8:33 0 232.9G part /media/me/USB_DISK
sr0 10:0 1 1024M rom
```

如我们所见，USB 硬盘已挂载；它的名称为 `/dev/sdc`，并包含一个名为 `/dev/sda1` 的分区。
