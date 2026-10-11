

此文件系统将自动在挂载 36 次或 180 天（以先发生者为准）时进行检查。请使用 tune2fs -c 或 -i 来覆盖此设置。  
[root@server1 root]#

随后，您可以选择使用 **tune2fs 命令**将此文件系统转换为 ext3，以在该文件系统上创建日志文件：

```bash
[root@server1 root]# tune2fs -j /dev/hdc5
tune2fs 1.35 (28-Feb-2004)
Creating journal inode: done
This filesystem will be automatically checked every 36 mounts or
180 days, whichever comes first. Use tune2fs -c or -i to override.
[root@server1 root]#
```

或者，您也可以使用 **mke2fs -j /dev/hdc5** 或 **mkfs.ext3 /dev/hdc5** 命令来创建 ext3 文件系统。要将此 ext3 文件系统挂载到名为 /data 的新挂载点目录并查看其内容，您可以使用以下命令：

```bash
[root@server1 root]# mkdir /data
[root@server1 root]# mount -t ext3 /dev/hdc5 /data
[root@server1 root]# mount
/dev/hdc1 on / type ext3 (rw)
none on /proc type proc (rw)
none on /sys type sysfs (rw)
none on /dev/pts type devpts (rw,gid=5,mode=620)
usbdevfs on /proc/bus/usb type usbdevfs (rw)
none on /dev/shm type tmpfs (rw)
/dev/hdc5 on /data type ext3 (rw)
[root@server1 root]# ls -F /data
lost+found/
[root@server1 root]#
```

若要让系统在每次启动时自动挂载此文件系统，只需编辑 **/etc/fstab** 文件，使其包含针对 /dev/hdc5 的以下条目即可：

```bash
[root@server1 root]# cat /etc/fstab
LABEL=/                    ext3                 defaults    1 1
none                       /dev/pts             gid=5,mode=620 0 0
none                       /dev/shm             defaults    0 0
none                       /proc                proc         defaults 0 0
none                       /sys                 sysfs        defaults 0 0
/dev/hda2                  swap                 defaults     0 0
/dev/cdrom                 /mnt/cdrom           udf,iso9660 noauto,owner,kudzu 0 0
/dev/fd0                   /mnt/floppy          auto         noauto,owner,kudzu 0 0
/dev/hdc5                  /data                ext3         defaults   0 0
[root@server1 root]#
```

## 监控文件系统

在磁盘设备上创建文件系统并将这些磁盘设备挂载到目录树后，应定期检查错误、磁盘空间使用情况和 inode 使用情况。这可以最大程度地减少因文件系统损坏而引发的问题，并降低因磁盘空间不足而导致无法保存文件的可能性。

### 磁盘使用情况

可以将多个文件系统挂载到目录树上。如前所述，使用的文件系统越多，损坏的文件系统干扰正常系统操作的可能性就越低。相反，更多的文件系统通常意味着每个文件系统的硬盘空间更少，如果某些文件系统被数据填满，可能会导致系统错误。许多用户在安装过程中为 `/`、`/usr` 和 `/var` 目录创建文件系统。`/usr` 目录包含 Linux 系统中大多数实用程序和已安装的程序，并且应为未来的软件安装预留足够的空间。`/var` 目录会随着日志文件的存储而不断增大。应定期删除旧的日志文件，以为新文件腾出空间。在这些文件系统中，`/` 文件系统最为关键，并且始终保留大量空闲空间作为操作系统的临时工作空间。因此，应频繁监控 `/` 文件系统。如果 `/` 文件系统的空闲空间低于 10%，系统可能会出现性能下降或停止运行的问题。

监控已挂载文件系统空闲空间的最简单方法是使用 **df (disk free space) 命令**，如下面的输出所示：

```
[root@server1 root]# df
Filesystem            1k-blocks      Used Available Use% Mounted on
/dev/hdc1               4032092  2848744   978524  75% /
none                     192232        0   192232   0% /dev/shm
[root@server1 root]#
```

从上述输出可以看出，唯一使用的文件系统是 `/` 文件系统；`/usr` 和 `/var` 目录仅仅是 `/` 文件系统上的目录，这增加了监控 `/` 文件系统的重要性。由于上述输出中 `/` 文件系统的已用比例为 75%，因此暂无需立即担心。然而，未来的日志文件和安装软件会增加这一数字，可能需要购买额外的硬盘来存放数据。

或者，您可以使用 `-h` 选项以更方便用户（或人类可读）的格式查看 `df` 命令的输出，该选项会以最合适的格式打印大小（G = 吉字节，M = 兆字节），如下所示：

```
[root@server1 root]# df -h
Filesystem Size Used Avail Use% Mounted on
/dev/hdc1 3.8G 2.8G 958M 75% /
none 188M 0 187M 0% /dev/shm
[root@server1 root]#
```

请记住，df 命令仅查看已挂载的文件系统；因此，若要获取软盘文件系统的磁盘空闲空间统计信息，应在查看 df 命令输出之前先挂载它：

```
[root@server1 root]# mount /dev/fd0
[root@server1 root]# df
Filesystem             1k-blocks      Used Available Use% Mounted on
/dev/hdc1               4032092    2848756    978512  75% /
none                     192232         0    192232   0% /dev/shm
/dev/fd0                    1412        17      1323   2% /mnt/floppy
[root@server1 root]# umount /dev/fd0
[root@server1 root]# df
Filesystem             1k-blocks      Used Available Use% Mounted on
/dev/hdc1               4032092    2848756    978512  75% /
none                     192232         0    192232   0% /dev/shm
[root@server1 root]#
```

如果文件系统接近满容量，查看该文件系统中哪些目录占用了最多的磁盘空间可能很有用，这样您可以从该目录中删除或移动文件到空间充足的其他文件系统。要查看目录及其内容的大小（以千字节为单位），可以使用 du (directory usage) 命令。如果目录较大，应使用 more 或 less 命令逐页查看输出，如以下 /usr 目录所示：

```
[root@server1 root]# du /usr | more
4      /usr/local/share/man/man5
4      /usr/local/share/man/man2
4      /usr/local/share/man/man6
4      /usr/local/share/man/man9
4      /usr/local/share/man/man
4      /usr/local/share/man/man8
4      /usr/local/share/man/man4
4      /usr/local/share/man/man7
4      /usr/local/share/man/man3
4      /usr/local/share/man/man1
44     /usr/local/share/man
4      /usr/local/share/info
52     /usr/local/share
4      /usr/local/src
4      /usr/local/bin
4      /usr/local/etc
4      /usr/local/include
4      /usr/local/libexec
4      /usr/local/sbin
4   /usr/local/games
4   /usr/local/lib
88   /usr/local
32   /usr/share/idl/bonobo-activation-2.0
--More--
```

若要仅查看目录总大小的摘要，只需对 du 命令使用 -s 开关，如以下 /usr 目录示例所示：

```
[root@server1 root]# du -s /usr
2633772 /usr
[root@server1 root]#
```

与 df 命令一样，du 命令也接受 -h 选项以使视图更易于人类阅读；以下表明 /usr 目录的总大小为 2.6 吉字节：

```
[root@server1 root]# du -hs /usr
2.6G /usr
[root@server1 root]#
```

请记住，每个文件系统都有一个 inode 表，其中包含文件系统中文件和目录的 inode；此 inode 表在创建文件系统时生成，通常与文件系统的大小成正比。每个文件和目录使用一个 inode；因此，包含许多小文件的文件系统可能会用尽 inode 表中的所有 inode，从而阻止在文件系统中创建新文件。要查看 ext2 或 ext3 文件系统的 inode 总数和空闲 inode 数，可以使用带有 -h 开关的 dumpe2fs 命令，如下面的输出所示：

```
[root@server1 root]# df
Filesystem 1k-blocks Used Available Use% Mounted on
/dev/hdc1 4032092 2848756 978512 75% /
none 192232 0 192232 0% /dev/shm
[root@server1 root]# dumpe2fs -h /dev/hdc1
dumpe2fs 1.35 (28-Feb-2004)
Filesystem volume name: <none>
Last mounted on: / not available>
Filesystem UUID: 419890df-6ee5-47b1-a891-a84462625e45
Filesystem magic number: 0xEF53
Filesystem revision #: 1 (dynamic)
Filesystem features: has_journal dir_index filetype needs_recovery sparse_super
Default mount options: (none)
Filesystem state: clean
Errors behavior: Continue
Filesystem OS type: Linux
Inode count: 1151904
```

