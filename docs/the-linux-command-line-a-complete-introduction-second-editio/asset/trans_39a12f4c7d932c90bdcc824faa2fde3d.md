

| 字段 | 内容 | 描述 |
|---|---|---|
| 5 | Frequency | 一个数字，用于指定是否以及何时使用 dump 命令备份文件系统。 |
| 6 | Order | 一个数字，用于指定应以何种顺序使用 fsck 命令检查文件系统。 |

## 查看已挂载文件系统列表

mount 命令用于挂载文件系统。不带参数输入该命令将显示当前已挂载的文件系统列表。

```
[me@linuxbox ~]$ mount
/dev/sda2 on / type ext4 (rw)
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
devpts on /dev/pts type devpts (rw,gid=5,mode=620)
/dev/sda5 on /home type ext4 (rw)
/dev/sda1 on /boot type ext4 (rw)
tmpfs on /dev/shm type tmpfs (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
sunrpc on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw)
fusectl on /sys/fs/fuse/connections type fusectl (rw)
/dev/sdd1 on /media/disk type vfat (rw,nosuid,nodev,noatime,uhelper=hal,uid=500,utf8,shortname=lower)
twin4:/musicbox on /misc/musicbox type nfs4 (rw,addr=192.168.1.4)
```

列表的格式如下：device on mount_point type filesystem_type (options)。例如，第一行显示设备 /dev/sda2 已挂载为根文件系统，类型为 ext4，且可读可写（选项 rw）。该列表在底部还有两个有趣的条目。倒数第二个条目显示一个 2GB SD 存储卡在读卡器中挂载在 /media/disk，而最后一个条目是挂载在 /misc/musicbox 的网络驱动器。

在我们的第一个实验中，我们将使用 CD-ROM。首先，让我们查看在插入 CD-ROM 之前系统的状态。

```
[me@linuxbox ~]$ mount
/dev/mapper/VolGroup00-LogVol00 on / type ext4 (rw)
```
```
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
devpts on /dev/pts type devpts (rw,gid=5,mode=620)
/dev/sda1 on /boot type ext4 (rw)
tmpfs on /dev/shm type tmpfs (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
sunrpc on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw)
```

此列表来自 CentOS 系统，该系统使用 LVM（逻辑卷管理器）创建其根文件系统。像许多现代 Linux 发行版一样，该系统在插入后会尝试自动挂载 CD-ROM。插入光盘后，我们看到以下内容：

```
[me@linuxbox ~]$ mount
/dev/mapper/VolGroup00-LogVol00 on / type ext4 (rw)
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
devpts on /dev/pts type devpts (rw,gid=5,mode=620)
/dev/hda1 on /boot type ext4 (rw)
tmpfs on /dev/shm type tmpfs (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
sunrpc on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw)
/dev/sdc on /media/live-1.0.10-8 type iso9660 (ro,noexec,nosuid,nodev,uid=500)
```

插入光盘后，我们看到与之前相同的列表，只多了一个条目。在列表末尾我们看到 CD-ROM（在此系统上设备为 /dev/sdc）已挂载在 /media/live-1.0.10-8，类型为 iso9660（CD-ROM）。对于我们的实验目的，我们感兴趣的是设备名称。当你自己进行此实验时，设备名称很可能不同。

## 警告

在下面的示例中，至关重要的是你必须密切注意系统上实际使用的设备名称，不要使用本文中使用的名称！另请注意，音频 CD 与 CD-ROM 不同。音频 CD 不包含文件系统，因此通常意义上无法挂载。

现在我们已经知道了 CD-ROM 驱动器的设备名称，让我们卸载光盘并将其重新挂载到文件系统树中的另一个位置。为此，我们成为超级用户（使用适用于我们系统的命令）并使用 umount（注意拼写）命令卸载光盘。

```
[me@linuxbox ~]$ su -
Password:
[root@linuxbox ~]# umount /dev/sdc
```

下一步是为磁盘创建新的挂载点。挂载点只是在文件系统树中的某个目录。没有什么特别之处。它甚至不必是空目录，尽管如果你在非空目录上挂载设备，在卸载设备之前将无法看到该目录之前的內容。为了我们的目的，我们将创建一个新目录。

```
[root@linuxbox ~]# mkdir /mnt/cdrom
```

最后，我们将 CD-ROM 挂载到新的挂载点。-t 选项用于指定文件系统类型。

```
[root@linuxbox ~]# mount -t iso9660 /dev/sdc /mnt/cdrom
```

之后，我们可以通过新的挂载点检查 CD-ROM 的内容。

```
[root@linuxbox ~]# cd /mnt/cdrom
[root@linuxbox cdrom]# ls
```

注意当我们尝试卸载 CD-ROM 时会发生什么。

```
[root@linuxbox cdrom]# umount /dev/sdc
umount: /mnt/cdrom: device is busy
```

为什么会这样？原因是我们不能在设备正被某人或某个进程使用时卸载设备。在这种情况下，我们将工作目录更改为 CD-ROM 的挂载点，

