
```
# tune2fs -i 10 /dev/ad0s4      Check after 10 hours
tune2fs -i 1d /dev/ad0s4      Check after 1 day
tune2fs -i 3w /dev/ad0s4      Check after 3 weeks
tune2fs -i 6m /dev/ad0s4      Check after 6 months
tune2fs -i 0 /dev/ad0s4       Disable time-dependent checking
```

请确保你开启了挂载次数依赖检查或时间依赖检查之一。

## 创建内存磁盘文件系统

如果你想创建一个更具移植性的文件系统（换句话说，不绑定到物理磁盘），你可以创建一个内存磁盘文件系统。内存磁盘文件系统是位于文件系统内部的一个。你可以将其格式化为文件系统，挂载和卸载它，甚至在不同的计算机之间移动并使用它。

内存磁盘文件系统用于备份数据、创建现场 CD 或运行专用虚拟操作系统。在接下来的示例中，你创建一个空白的 GB 磁盘文件，将其格式化为文件系统，并挂载它以访问文件系统上的数据：

```
# dd if=/dev/zero of=mydisk count=2048000  Create zero-filled IGB file
2048000+0 records in
2048000+0 records out
104857600 bytes transferred in 56.519727 secs (18552393 bytes/sec)
# du -sh mydisk  Check memory disk size
1.0G mydisk
# mdconfig -a t vnode -f mydisk -u 2  Identifies mydisk as memory disk file
# bsdlabel -w md2 auto  Adds BSD label to file
# newfs mda2  Creates UFS file system
/dev/md2:1000.0MB (204800 sectors) block size 16384, fragment size 2048
using 6 cylinder groups of 183.78MB, 11761 blocks, 23552 nodes.
super-block backups (for fsck -b at):
160, 37512, 752864, 1129312, 105568, 181920
# mkdir /mnt/mydisk  Creates mount point
# umount /mnt/md2 /mnt/mydisk  Memory disk unmount
```

在此过程中，`dd` 命令创建了一个 2048000 (1 GB) 的空磁盘文件。`mdconfig` 命令将 `mydisk` 文件识别为内存磁盘的存储区域。`bsdlabel` 命令为文件镜像创建 BSD 标签。`newfs` 命令在该镜像上创建一个 UFS 文件系统。

当挂载虚拟文件系统时，你可以像访问任何文件系统一样访问它。当你完成对文件系统的操作后，请离开并卸载它：

```
# cd /mnt/mydisk  Change to the mount point
# mkdir testdir  Create a directory on the file system
# cp /etc/hosts .  Copy a file to the file system
# cd  Leave the file system
# umount /mnt/mydisk  Unmount the file system
```

在卸载虚拟文件系统后，你可以将其移动到另一个系统或将其刻录到 CD 中作为文件系统。如果你不再需要该文件系统，直接删除即可。

## 创建和使用分区

BSD 系统需要交换分区来处理 RAM 溢出。如果你在安装时没有创建交换分区，可以稍后创建。你可以在普通磁盘分区（如前所述识别新分区）或格式化为交换分区的文件上创建交换区域，方法如下：

```
# dd if=/dev/zero of=/tmp/swapfile0 count=65536
65536+0 records in
65536+0 records out
3355432 bytes transferred in 1.54122 secs (217609 bytes/sec)
# chmod 600 /tmp/swapfile0
# mdconfig -a t v -f /tmp/swapfile0 -u 0
# swapon /dev/md0
```

`dd` 命令创建一个名为 `swapfile0` 的文件。`chmod` 命令锁定权限。`mdconfig` 命令配置交换为 md 设备。创建交换分区或文件后，你需要使用 `swapon` 命令告诉系统使用该交换区域。这与启动时发生的情况类似。例如：

```
# swapon /dev/md0
Turn swap on for /dev/md0
```

你可以使用 `swapinfo` 命令查看交换文件和分区的列表：

| Filename | 1K-blocks | Used | Avail | Capacity |
|---|---|---|---|---|
| /dev/ad0sb | 487880 | 0 | 487880 | 0% |
| /dev/md0 | 32768 | 0 | 32768 | 0% |
| Total | 520648 | 0 | 520648 | 0% |

```
# swapinfo -h
View all swap files and partitions in megabytes
```

| Device | 1K-blocks | Used | Avail | Capacity |
|---|---|---|---|---|
| /dev/ad0sb | 487880 | 0B | 476M | 0% |
| /dev/md0 | 32768 | 0B | 32M | 0% |
| Total | 520648 | 0B | 508M | 0% |

```
# swapinfo -k
View all swap files and partitions in kilobytes
```

要关闭交换区域，可以使用 `swapoff` 命令。只有在你确定交换区域未被使用时才执行此操作，否则可能会导致崩溃：

```
# swapoff /dev/md0
Turn off swap partition
# swapoff /dev/ad0sb
Turn off swap partition
# swapoff -a
Turn off all swap partitions
```

### 挂载和卸载文件系统

在使用普通非交换文件系统之前，你需要通过挂载将其附加到计算机文件树中的目录。你的根 (`/`) 以及经常使用的其他文件系统通常根据 `/etc/fstab` 文件中的条目自动挂载。其他文件系统可以使用 `mount` 命令手动挂载。

### 从 fstab 挂载文件系统

当你安装 FreeBSD 时，`/etc/fstab` 文件通常会自动设置，包含根分区和其他分区的信息。这些分区可以设置为在启动时挂载，或准备好手动挂载（在手动挂载时可以使用挂载点和选项）。

这是一个 `/etc/fstab` 文件的示例：

| Device | Mountpoint | FType | Options | Dump | Pass# |
| --- | --- | --- | --- | --- | --- |
| /dev/ad0s1 | none | swap | sw | 0 | 0 |
| /dev/ad0s1 | | ufs | rw | 1 | 2 |
| /dev/ad0s1 | /tmp | ufs | rw | 2 | 2 |
| /dev/ad0s1 | /usr | ufs | rw | 2 | 2 |
| /dev/ad0s1 | /var | ufs | rw | 2 | 2 |
| /dev/acd0 | | cdrom | cd9660 | ro,noauto | 0 | 0 |
| /dev/ad0s2 | /mnt/debian | ext2fs | rw | 0 | 0 |

所有系统都会自动挂载，位于 `/dev/acd0` 的 CD 驱动器除外（由 `noauto` 选项指示）。根 (`/`)、`/tmp`、`/usr` 和 `/var` 分区是普通的 UFS 文件系统，并以读写 (`rw`) 模式挂载。在本示例中，手动添加了 `/dev/ads02` 切片（磁盘切片 2），以挂载该设备上的 Debian GNU/Linux 分区。

表 7-2 说明了 `/etc/fstab` 文件中的每个字段。

### 表 7-2：/etc/fstab 文件字段

| 字段 | 描述 |
| --- | --- |
| 1 | 代表文件系统的设备名称。这是挂载为 `/dev/ad0s1` 的分区设备名称。如果整个切片专门用于单个文件系统，它也可以包含代表切片的设备名称（例如代表切片 2 的 `/dev/ad02`） |
| 2 | 文件系统中的挂载点。文件系统包含从挂载点向下树结构的所有数据，除非在下方某处挂载了另一个文件系统 |
| 3 | 文件类型。见表 7-1 的许多常见文件类型列表 |
| 4 | 挂载计数选项。挂载选项示例包括 `noauto`（防止文件系统在启动时挂载）或 `ro`（以只读模式挂载文件系统）。选项之间用逗号分隔。查看 `mount` 手页 (`-o`) 以获取其他支持的选项 |
| 5 | 备份文件系统？这仅在你运行 `dump` 备份时有效。正数表示应该对文件系统进行备份。数字 1 意味着首先备份文件系统（用于根分区）。数字 2 假设文件系统可以在根分区之后的任何时间进行备份 |
| 6 | 检查文件系统？字段中的数字指示文件系统是否需要用 `fsck` 进行检查。零表示不检查文件系统。结合 `dump` 指示器，数字 1 意味着需要首先检查文件系统（用于根分区）。数字 2 假设文件系统可以在根分区之后的任何时间进行检查 |

## 第 7 章：文件系统管理

你可以在 `/etc/fstab` 文件中为任何想要的硬盘分区或可移动媒体分区创建自己的条目。远程文件系统（NFS、Samba 等）也可以包含在 `/etc/fstab` 文件条目，以便在启动时或之后自动挂载这些文件系统。

### 使用 mount 命令挂载文件系统

`mount` 命令用于查看已挂载的文件系统，以及挂载任何本地（硬盘、USB 驱动器、CD、DVD 等）或远程（NFS、Samba 等）文件系统。以下是列出文件系统的 `mount` 命令示例：

```
$ mount List mounted remote and local file systems
dev/ad0s1 on / (ufs, local)
devfs on /dev (devfs, local)
dev/ad0s1 on /tmp (ufs, local, soft-updates)
dev/ad0s1 on /usr (usr, local, soft-updates)
dev/ad0s1 on /var (var, local, soft-updates)
dev/ad0s2 on /mnt/debian (ext2fs, local)
$ mount -v List mounted file systems with file system id
dev/ad0s1 on / (ufs, local), fsid 3bebab47a6961229
devfs on /dev (devfs, local), fsid 00ff00505000000
dev/ad0s1 on /tmp (ufs, local, soft-updates), fsid 3bebab47c27d24c2
dev/ad0s1 on /usr (usr, local, soft-updates), fsid 3bebab4746a302f2
dev/ad0s1 on /var (var, local, soft-updates), fsid 3bbebab4797a19385
dev/ad0s2 on /mnt/debian (ext2fs, local), fsid 4f00000080000000
```

使用 `-t` 仅列出特定文件类型的列表：

```
$ mount -t ufs List mounted ufs file systems
dev/ad0s1 on / (ufs, local)
dev/ad0s1 on /tmp (ufs, local, soft-updates)
dev/ad0s1 on /usr (usr, local, soft-updates)
dev/ad0s1 on /var (var, local, soft-updates)
$ mount -t ext2 List mounted ext2 file systems
dev/ad0s2 on /mnt/debian (ext2fs, local)
```

以下是一个将本地文件系统（`/dev/ad0s4` 设备）挂载到现有目录挂载点 `/mnt/music` 的简单命令：

```
# mount /dev/ad0s4 /mnt/music Mount a local file system
# mount -v /dev/ad0s4 /mnt/music/ Mount file system, more verbose
```

在上述示例中，`mount` 命令将会在 `/etc/fstab` 文件中查找 `/dev/sda` 的条目，或者猜测文件系统的类型：

使用 `-t` 显式指定要挂载的文件系统类型：

```
# mount -v -t ext2fs /dev/ad0s4 /mnt/music/ Mount an ext2 file system
dev/ad0s4 on /mnt/music (ext2fs, local), fsid 5e000000800000000
```

## 第 7 章：文件系统管理

如果你挂载的内容已经列在 `fstab` 文件中，你只需要指定挂载点或设备。例如，使用以下 `fstab` 条目：

```
/dev/ad0s4       /mnt/music      ext2fs  rw  2 2
```

你可以使用一些选项来挂载文件系统：

```
# mount -v /dev/ad0s4  Mount file system with device name only
/dev/ad0s4 /mnt/music  (ext2fs, local, fsid 5e00000000000000)
# mount -v /mnt/music  File system with mount point only
/dev/ad0s4 /mnt/music  (ext2fs, local, fsid 5e00000000000000)
```

你可以通过添加 `-o` 和逗号分隔的选项列表来指定挂载选项。相同的选项也可以添加到 `/etc/fstab` 文件的第 4 字段。默认情况下，分区以读/写方式挂载。你可以显式指定将文件系统挂载为只读（`ro`）或读/写（`rw`）：

```
# mount -v ext2fs -o rw /dev/ad0s4 /mnt/music  Mount read/write
/dev/ad0s4 /mnt/music  (ext2fs, local), fsid 5e000000000000000)
# mount -v ext2fs -o ro /dev/ad0s4 /mnt/music  Mount read-only
/dev/ad0s4 /mnt/music  (ext2fs, local), fsid 5e000000000000000)
```

你可以使用的一些用挂载选项：

- `noatime`：不更新文件的访问时间。对于具有大量 I/O 的文件系统（如交换分区和日志）很有。
- `noexec`：防止执行该文件系统上的二进制文件。可以用于对于不可信用户的 `/tmp` 增加安全性。
- 就像交换到一个文件一样，你可以在文件中创建一个文件系统并将其挂载，这样你就可以查看其内容。创建此类文件在本章前面的“创建磁盘”部分有描述。一种常见的情况是在下载 LiveCD 后。通过挂载该 CD，你可以查看内容或将文件拷贝到你的硬盘。

```
# mdconfig -a vnode -f /usr/images/FreeBSD-2.0.1-iso -o 1 /mnt/freebies
# mount -t /dev/md1 /mnt/freebies
# ln -s /mnt/freebies/boot
```

| | | |
| :--- | :--- | :--- |
| .rsh_ | boot | tmp |
| .profile | root | usr |
| pkg_info.txt | uzip | |
| dist | libexec | sys |

### 卸载文件系统

卸载文件系统，使用 `umount` 命令。你可以使用设备名称或挂载点进行卸载。避免设备名称（很多非常相似）。

```
# umount -v /dev/ad0s4      Unmount by device
dev/sda1 unmounted
# umount -v /mnt/music      Unmount by mount
/tmp/disk.img unmounted
```

如果设备忙，卸载将失败。卸载失败的一个常见原因是你在目录内打开了 shell：

```
# umount -v /mnt/music
umount: of /mnt/music failed: Device busy
```

### 检查文件系统

文件系统传统上在启动时进行检查。`fstab` 文件中的设置用于决定哪些文件系统在挂载之前进行检查。`fsck` 命令实际上取决于一组特定文件的 `fsck` 命令，不仅检查文件系统中的一致性问题，还可以交互地修复这些问题。
