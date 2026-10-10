

```plain
[root@server1 floppy]# mkdir workfiles
[root@server1 floppy]# ls -F
issue lost+found/ workfiles/
[root@server1 floppy]# cd workfiles
[root@server1 workfiles]# pwd
/media/floppy/workfiles
[root@server1 workfiles]# cp /etc/inittab .
[root@server1 workfiles]# ls -F
inittab
[root@server1 workfiles]#
```

尽管你可以在没有系统授权的情况下将软盘从软驱中弹出，但这样做很可能导致终端屏幕上出现错误信息。在弹出软盘之前，必须使用 `umount` 命令正确卸载它。`umount` 命令可以接受要卸载的设备名称或挂载点目录作为参数。与挂载软盘类似，卸载软盘要求挂载点目录没有用户正在使用。如果你尝试在软盘正在被使用时卸载挂载到 `/media/floppy` 目录的软盘，你会收到一个类似于以下示例中的错误信息：

```plain
[root@server1 floppy]# pwd
/media/floppy
[root@server1 floppy]# umount /media/floppy
umount: /media/floppy: target is busy.
     (In some cases useful info about processes that use
     the device is found in lsof(8) or fuser(1). )
[root@server1 floppy]# fuser -u /media/floppy
/media/floppy:        17368(root)
[root@server1 floppy]# cd /root
[root@server1 ~]# umount /media/floppy
[root@server1 ~]# mount
/dev/sda1 on / type ext4 (rw)
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
devpts on /dev/pts type devpts (rw,gid=5,mode=620)
tmpfs on /dev/shm type tmpfs (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
sunrpc on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw)
[root@server1 ~]#
```

从上述输出中可以看出，由于 `/media/floppy` 目录是当前工作目录，你仍然在使用它。`fuser` 命令还表明 root 用户有一个进程正在使用该目录。在更改当前工作目录后，`umount` 命令能够成功将软盘从 `/media/floppy` 目录卸载，并且 `mount` 命令的输出表明软盘不再处于挂载状态。

回想一下，挂载只是将磁盘设备附加到 Linux 目录树，以便你可以将该设备像包含文件和子目录的目录一样处理。设备可以挂载到任何现有目录。但是，如果目录包含文件，那么在该设备卸载之前，这些文件是无法访问的。假设你创建了一个名为 `/flopper` 的目录用于挂载软盘，并在其中创建一个名为 `samplefile` 的文件，如以下输出所示：

```plain
[root@server1 ~]# mkdir /flopper
[root@server1 ~]# touch /flopper/samplefile
[root@server1 ~]# ls -F /flopper
samplefile
[root@server1 ~]# 
```

如果之前使用的软盘挂载到 `/flopper` 目录，那么使用该 `/flopper` 目录的用户实际上是在使用软盘；然而，当没有任何内容挂载到 `/flopper` 目录时，之前的内容即可供使用：

```plain
[root@server1 ~]# mount -t ext2 /dev/fd0 /flopper
[root@server1 ~]# mount
/dev/sda1 on / type ext4 (rw)
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
devpts on /dev/pts type devpts (rw, gid=5, mode=620)
tmpfs on /dev/shm type tmpfs (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
sunrpc on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw)
[root@server1 ~]# ls -F /flopper
issue lost+found/ workfiles/
[root@server1 ~]# umount /flopper
[root@server1 ~]# ls -F /flopper
samplefile
[root@server1 ~]# 
```

上述输出中使用的 `mount` 命令指定了文件系统类型、要挂载的设备以及挂载点目录。为了节省在命令行输入的时间，你可以选择只指定一个参数，让系统在 `/etc/fstab`（文件系统表）文件中查找剩余信息。`/etc/fstab` 文件有双重用途：它用于在启动时挂载设备，并且当用户使用 `mount` 命令时未在命令行上提供足够的参数时，系统也会参考该文件。

`/etc/fstab` 文件中有六个字段：

- <要挂载的设备> <挂载点> <类型> <挂载选项> <dump#> <fsck#>

要挂载的设备可以是设备文件的路径（即 `/dev/sda1`），或者是描述要挂载卷的引导加载器标签（例如 UUID=db545f1c-c1e2-4b70-acbe-3dc1614fd20）。挂载点指定挂载设备的位置。类型可以是特定值（如 ext4）或者自动检测。挂载选项是挂载卷时 `mount` 命令接受的额外选项（例如只读，或 ro）。任何挂载选项为 "noauto" 的文件系统都不会在启动时自动挂载；要查找 `mount` 命令接受的所有选项的完整列表，可以查看 `mount` 命令的手册页。

`dump#` 由 `dump` 命令（在第 11 章中讨论）在备份文件系统时使用；该字段中的 1 表示应该备份文件系统，而 0 表示不需要备份。`fsck#` 由本章稍后讨论的 `fsck` 命令在启动时检查文件系统错误时使用；该字段中带有 1 的文件系统会在带有数字 2 的文件系统之前进行检查，而带有数字 0 的文件系统则不进行检查。

![](img/c27875544958897d817484d558c208c8_230_0.png)

要挂载 `/etc/fstab` 文件中所有计划在启动时挂载的文件系统，你只需输入 `mount -a` 命令即可。

以下输出显示了一个示例 `/etc/fstab` 文件的内容：

```plain
[root@server1 ~]# cat /etc/fstab
#
# /etc/fstab
#
# Accessible filesystems, by reference, are maintained under '/dev/disk'
# See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for info
#
/dev/sda1        /                 ext4    defaults        1 1
/dev/sda2        swap              swap    defaults        0 0
tmpfs            /dev/shm          tmpfs   defaults        0 0
devpts           /dev/pts          devpts  gid=5,mode=620  0 0
sysfs            /sys              sysfs   defaults        0 0
proc             /proc             proc    defaults        0 0
/dev/fd0         /media/floppy     auto    noauto          0 0
[root@server1 ~]# 
```

因此，要将第一个软盘设备（/dev/fd0）挂载到 `/mnt/floppy` 目录并自动检测设备上的文件系统类型，只需提供足够的信息让 `mount` 命令在 `/etc/fstab` 文件中找到相应的行即可：

```plain
[root@server1 ~]# mount /dev/fd0
[root@server1 ~]# mount
/dev/sda1 on / type ext4 (rw)
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
devpts on /dev/pts type devpts (rw, gid=5, mode=620)
tmpfs on /dev/shm type tmpfs (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
sunrpc on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw)
/dev/fd0 on /media/floppy type ext2 (rw)
[root@server1 ~]# umount /dev/fd0
[root@server1 ~]# 
```

上述输出中的 `mount` 命令成功，是因为 `/etc/fstab` 中有一行描述了 `/dev/fd0` 设备的挂载。

| 命令 | 描述 |
| :--- | :--- |
| mount | 显示已挂载的文件系统 |
| mount -t <type> <device> <mount point> | 将特定 <type> 的 <device> 挂载到 <mount point> |
| fuser -u <directory> | 显示正在使用特定目录的用户 |
| umount <mount point> 或 umount <device> | 将 <device> 从其 <mount point> 卸载 |

表 5-4 在挂载和卸载文件系统时有用的命令

或者，你也可以将挂载点作为 `mount` 命令的参数来指定，从而通过 `/etc/fstab` 中的正确条目挂载相同的设备：

```plain
[root@server1 ~]# mount /media/floppy
[root@server1 ~]# mount
/dev/sda1 on / type ext4 (rw)
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
devpts on /dev/pts type devpts (rw,gid=5,mode=620)
tmpfs on /dev/shm type tmpfs (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
sunrpc on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw)
/dev/fd0 on /media/floppy type ext2 (rw)
[root@server1 ~]# umount /media/floppy
[root@server1 ~]# 
```

表 5-4 列出了在挂载和卸载软盘时有用的命令。

### 处理 CD、DVD 和 ISO 镜像

大多数未从互联网下载的软件都封装在 CD 和 DVD 上，因为它们的存储容量比软盘大得多；一张 DVD 可以存储的数据量是软盘的 3000 多倍。与软盘一样，CD 和 DVD 可以使用 `mount` 命令进行挂载，使用 `umount` 命令进行卸载，如表 5-4 所示；然而，这些命令使用的设备文件是不同的。CD 和 DVD 使用的设备文件取决于驱动器本身使用的技术。如果你的计算机有 PATA CD 或 DVD 驱动器，你可以使用以下四种标准 PATA 硬盘配置之一（在第 2 章中讨论）来引用它：

- 主盘主 (/dev/hda)
- 主盘从 (/dev/hdb)
- 副盘主 (/dev/hdc)
- 副盘从 (/dev/hdd)

