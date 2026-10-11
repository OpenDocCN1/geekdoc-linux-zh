
同样，你也可以在 USB 闪存驱动器下创建子目录来存储文件；这些子目录将在挂载点目录下被引用。要在 `/etc/fstab` 文件中为其创建一个名为 `workflows` 的目录，你可以使用以下示例并复制命令：

```
[root@server1 USBdrive]# pwd

/media/USBdrive

[root@server1 USBdrive]# ls -F

lost+found/

[root@server1 USBdrive]# mkdir workfiles

[root@server1 USBdrive]# ls -F

issue lost+found/ workfiles

[root@server1 USBdrive]# cd workfiles

[root@server1 workfiles]# pwd

/media/USBdrive/workfiles

[root@server1 workfiles]# cp /etc/fstab
```

# 第 5 章 Linux 文件系统管理

```bash
[root@server1 workfiles]# ls

initabb

[root@server1 workfiles]#
```

尽管你可以在没有许可的情况下从系统中移除 USB 闪存，但这样做可能会导致终端屏幕上出现错误信息。在移除 USB 闪存之前，必须使用 `unmount` 命令对其进行正确的卸载。`unmount` 命令可以接受设备名称或挂载点作为参数。与挂载设备类似，卸载设备要求挂载目录没有用户正在使用它。如果你尝试在使用过程中卸载挂载到 `/media/USBdrive` 目录的 USB 闪存，你将收到一条类似于示例所示的错误消息：

```
[root@server1 USBdrive]# pwd

/media/USBdrive

[root@server1]# unmount /media/USBdrive

umount: media/USBdrive: target is busy. -u /tmp

[root@server1]# fuser -u /media/USBdrive

/media/USBdrive: 17368c(root)

[root@server1]# cd /root

[root@server1]-# unmount /media/USBdrive

[root@server1]# df -T
```

| Filesystem | Type | 1-blocks | Available | Use% | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| devtmpfs | devtmpfs | 2006860 | 0 | 2006860 | 0% | /dev |
| tmpfs | tmpfs | 2019492 | 0 | 2019492 | 0% | /dev/shm |
| tmpfs | tmpfs | 2019492 | 1208 | 2018284 | 1% | /run |
| tmpfs | tmpfs | 2019492 | 0 | 2019492 | 0% | /sys/fs/cgroup |
| /dev/sda3 | ext4 | 35862048 | 8845052 | 2516540 | 27% | / |
| tmpfs | tmpfs | 2019492 | 18720 | 2000772 | 1% | /tmp |
| /dev/sda1 | ext4 | 999320 | 151300 | 779208 | 17% | /boot |
| tmpfs | tmpfs | 403896 | 403896 | 1% | /run/user/42 |
| tmpfs | tmpfs | 403896 | 4 | 403892 | 1% | /run/user/0 |

从预测的输出可以注意到，你正在使用 `/media/USBdrive` 目录，因为它是当前的工作目录。`fuser` 命令表明 root 用户有一个进程正在使用该目录。在更改当前工作目录后，`unmount` 命令能够从 `/media/USBdrive` 目录卸载 USB 闪存内存，`mount` 命令的输出表明它已不再挂载。

回想一下，挂载仅仅是将磁盘设备附加到 Linux 目录树中，并作为一个包含文件和子目录的目录存在。设备可以挂载到任何现有目录。然而，如果目录包含文件，那么在卸载设备之前，这些文件是无法访问的。例如，假设你在以下输出中创建一个名为 `/USBdrive` 的目录用于挂载 USB 闪存设备，并创建一个名为 `samplefile` 的文件：

```bash
[root@server1 ~]# mkdir /USBdrive

[root@server1 ~]# touch /USBdrive/samplefile

[root@server1 ~]# ls /USBdrive

samplefile

[root@server1 ~]# 
```

如果之前使用的闪存驱动器挂载到 `/USBdrive` 目录，使用 `/USBdrive` 目录的用户将使用该 USB 闪存驱动器；但是，当没有内容挂载到 `/USBdrive` 目录时，之前的内容是用的：

```bash
[root@server1 ~]# mount /dev/sdb1 /USBdrive

[root@server1 ~]# df -T
```

| Filesystem | Type | 1-blocks | Available | Use% | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| devtmpfs | devtmpfs | 200860 | 0 | 200860 | 0% | /dev |
| tmpfs | tmpfs | 201942 | 0 | 201942 | 0% | /dev/shm |
| tmpfs | tmpfs | 201942 | 1208 | 2018284 | 1% | / |
| tmpfs | tmpfs | 201942 | 0 | 201942 | 0% | /sys/fs/cgroup |
| /dev/sda3 | ext4 | 3586248 | 8845052 | 2516564 | 27% | |
| tmpfs | tmpfs | 201942 | 18720 | 2000772 | 1% | /tmp |
| /dev/sda1 | ext4 | 999320 | 151300 | 779208 | 17% | /boot |
| tmpfs | tmpfs | 403896 | 403896 | 1% | /run/user/42 |
| tmpfs | tmpfs | 403896 | 4 | 403892 | 1% | /run/user/0 |

从预测的输出可以注意到，你正在使用 `/media/USBdrive` 目录，因为它是当前的工作目录。`fuser` 命令表明 root 用户有一个进程正在使用该目录。在更改当前工作目录后，`unmount` 命令能够从 `/media/USBdrive` 目录卸载 USB 闪存内存，`mount` 命令的输出表明它已不再挂载。

回想一下，挂载仅仅是将磁盘设备附加到 Linux 目录树中，并作为一个包含文件和子目录的目录存在。设备可以挂载到任何现有目录。然而，如果目录包含文件，那么在卸载设备之前，这些文件是无法访问的。例如，假设你在以下输出中创建一个名为 `/USBdrive` 的目录用于挂载 USB 闪存设备，并创建一个名为 `samplefile` 的文件：

```bash
[root@server1 ~]# mkdir /USBdrive

[root@server1 ~]# touch /USBdrive/samplefile

[root@server1 ~]# ls /USBdrive

samplefile

[root@server1 ~]# 
```

如果之前使用的闪存驱动器挂载到 `/USBdrive` 目录，使用 `/USBdrive` 目录的用户将使用该 USB 闪存驱动器；但是，当没有内容挂载到 `/USBdrive` 目录时，之前的内容是可以使用的：

```bash
[root@server1 ~]# mount /dev/sdb1 /USBdrive

[root@server1 ~]# df -T
```

## 第5章 Linux 文件系统管理

```
tmpfs           tmpfs           403896 4 403892 1% /run/user/0

/dev/sdb1      ext2            7687336 17168 7279668 1% /USBdrive

[root@server1]# umount /USBdrive

[root@server1]#
```
