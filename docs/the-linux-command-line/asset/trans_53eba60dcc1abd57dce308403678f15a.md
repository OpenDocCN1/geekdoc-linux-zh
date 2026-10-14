

fusectl on /sys/fs/fuse/connections type fusectl (rw)
/dev/sdd1 on /media/disk type vfat (rw,nosuid,nodev,noatime,
uhelper=hal,uid=500,utf8,shortname=lower)
twin4:/musicbox on /misc/musicbox type nfs4 (rw,addr=192.168.1.4)

列表的格式为：device on mount_point type file_system_type (options)。例如，第一行显示设备 /dev/sda2 被挂载为根文件系统，其类型为 ext3 且可读可写（选项“rw”）。该列表在底部还有两个有趣的条目。倒数第二个条目显示一个 2 GB 的 SD 存储卡在读卡器中挂载于 /media/disk，最后一个条目是挂载于 /misc/musicbox 的网络驱动器。

对于我们的第一个实验，我们将使用 CD-ROM。首先，让我们看一下在插入 CD-ROM 之前系统的状态：

```
[me@linuxbox ~]$ mount
/dev/mapper/VolGroup00-LogVol00 on / type ext3 (rw)
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
devpts on /dev/pts type devpts (rw,gid=5,mode=620)
/dev/hda1 on /boot type ext3 (rw)
tmpfs on /dev/shm type tmpfs (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
sunrpc on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw)
```

此列表来自 CentOS 5 系统，该系统使用 LVM（逻辑卷管理器）创建其根文件系统。与许多现代 Linux 发行版一样，该系统在插入后会尝试自动挂载 CD-ROM。插入光盘后，我们看到以下内容：

```
[me@linuxbox ~]$ mount
/dev/mapper/VolGroup00-LogVol00 on / type ext3 (rw)
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
devpts on /dev/pts type devpts (rw,gid=5,mode=620)
/dev/hda1 on /boot type ext3 (rw)
tmpfs on /dev/shm type tmpfs (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
sunrpc on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw)
/dev/hdc on /media/live-1.0.10-8 type iso9660 (ro,noexec,nosuid,
nodev,uid=500)
```

插入光盘后，我们看到与之前相同的列表，只多了一条条目。在

```
[root@linuxbox ~]# cd /mnt/cdrom
[root@linuxbox cdrom]# ls
```

注意当我们尝试卸载 CD-ROM 时会发生什么：

```
[root@linuxbox cdrom]# umount /dev/hdc
umount: /mnt/cdrom: device is busy
```

为什么会这样？原因是我们不能在设备正被某人或某个进程使用时卸载它。在本例中，我们将工作目录更改为 CD-ROM 的挂载点，这导致设备处于忙碌状态。我们可以通过将工作目录更改为挂载点之外的其他位置来轻松解决此问题：

```
[root@linuxbox cdrom]# cd
[root@linuxbox ~]# umount /dev/hdc
```

现在设备成功卸载。

## 为什么卸载很重要

如果查看 free 命令的输出，该命令显示内存使用统计信息，你会看到一个名为“buffers”的统计项。计算机系统旨在尽可能快地运行。系统速度的阻碍之一是慢速设备。打印机就是一个很好的例子。即使是最快的打印机，按计算机标准来说也极其缓慢。如果计算机必须停下来等待打印机完成打印一页，那么计算机将非常缓慢。在 PC 的早期时代（在多任务处理之前），这是一个真正的问题。如果你正在处理电子表格或文本文档，每次打印时计算机都会停止并变得不可用。计算机会尽可能快地将数据发送给打印机，但速度非常慢，因为打印机打印速度并不快。这个问题通过打印机缓冲区的出现得以解决，打印机缓冲区是一种包含一些 RAM 内存的设备，位于计算机和打印机之间。有了打印机缓冲区，计算机就会将打印机输出发送到缓冲区，并迅速存储在快速的 RAM 中，以便计算机可以返回工作而无需等待。与此同时，打印机缓冲区会以打印机能够接受的速度，从缓冲区的内存中缓慢地将数据传送到打印机。

