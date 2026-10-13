
| 设备 | 启动 | 开始 | 结束 | 块 | Id | 系统 |
|---|---|---|---|---|---|---|
| `/dev/sda1` | * | 1 | 505 | 524916 | 83 | Linux 原生 |
| `/dev/sda2` |  | 506 | 1014 | 529105+ | 5 | 扩展 |
| `/dev/sda5` |  | 506 | 886 | 396018 | 83 | Linux 原生 |
| `/dev/sda6` |  | 887 | 1011 | 129906 | 82 | Linux swap |

`/dev/sda1` 在 Boot 列中有 “*”，表示该分区可引导。

## mkfs

语法：

```
mkfs [-t fstype] [-cv] device-or-mount-point [blocks]
```

`mkfs` 命令允许您创建新的文件系统。例如，`mkfs -t ext2 /dev/hda3` 在第一块 IDE 硬盘的 `/dev/hda3` 分区上创建 `ext2` 类型文件系统。`-c` 选项可指示 `mkfs` 在构建文件系统前检查坏块。`-v` 选项产生详细输出。

## mount

语法：

```
mount -a [-t fstype] [-o options] device directory
```

`mount` 命令挂载文件系统。通常，常用文件系统的挂载选项存储在 `/etc/fstab` 中。例如，如果

```
/dev/hda6  /intranet  ext2  defaults  1  2
```

在 `/etc/fstab` 中找到，则可以按如下方式挂载存储在分区 `/dev/hda6` 中的文件系统：

```
mount /intranet
```

也可以按如下方式挂载同一文件系统：

```
mount -t ext2 /dev/hda6 /intranet
```

`-t` 选项用于指定文件系统类型。要挂载 `/etc/fstab` 中指定的所有文件系统，请使用 `-a` 选项。例如，以下命令挂载所有 `ext2` 文件系统：

```
mount -a -t ext2
```

`-o` 选项的常用参数是 `ro`（只读）和 `rw`（读写）。例如，以下命令将 `/dev/hda6` 以只读文件系统的方式挂载到 `/secured`：

```
mount -t ext2 -o ro /dev/hda6 /secured
```

## quota

要了解特定用户使用了多少磁盘空间，请按如下方式运行 `quota` 命令：

```
quota -u username
```

例如：

```
quota -u kabir
Disk quotas for user kabir (uid 500):
Filesystem blocks quota limit grace files quota limit grace
/dev/sda5  0  1024  4096  1  128  512
```

你可以使用相同的命令来监控组的磁盘使用情况，如下所示：

```
quota -g group
```

当你发现超出限制的用户或组时，可以向他们发送电子邮件消息，以便将磁盘使用量降至可接受的限制。

### swapoff

Syntax:

```
swapoff -a
```

`swapoff` 命令允许你禁用交换设备。`-a` 选项允许你禁用 `/etc/fstab` 中指定的所有交换分区。

### swapon

Syntax:

```
swapon -a
```

`swapon` 命令允许你启用交换设备。`-a` 选项允许你启用 `/etc/fstab` 中指定的所有交换分区。

### umount

Syntax:

```
umount -a [-t fstype]
```

`umount` 命令将文件系统从当前系统卸载。例如，

```
umount /cdrom
```

卸载挂载点为 `/cdrom` 且其挂载点详细信息在 `/etc/fstab` 中指定的文件系统。

`-a` 选项允许你卸载 `/etc/fstab` 文件中指定的所有文件系统（除 `proc` 文件系统外）。你也可以使用 `-t` 选项指定要卸载的特定文件系统类型。例如，

```
umount -a -t iso9660
```

卸载所有 `iso9660` 类型的文件系统，通常是 CD-ROM。

## DOS-Compatible Commands

如果你需要从 Linux 系统访问 MS-DOS 文件，则需要安装 `Mtools` 软件包。`Mtools` 以 RPM 软件包的形式随 Red Hat 提供，因此安装起来相当简单。有关如何安装 RPM 软件包的详细信息，请参阅上一节“File Compression and Archive-Specific Commands”中 `rpm` 命令的说明。

`Mtools` 是一组实用程序的集合，允许你读取、写入和移动 MS-DOS 文件。它还支持 Windows 9x 风格的长文件名、OS/2 Xdf 磁盘和 2m 磁盘。本节介绍 `Mtools` 软件包中常见的实用程序。

### mcopy

Syntax:

```
mcopy [-tm] source-file-or-directory destination-file-or-directory
```

`mcopy` 实用程序用于在 MS-DOS 和 Linux 之间复制文件。例如，

```
mcopy /tmp/readme.txt b:
```

### mdel

Syntax:

```
mdel msdosfile
```

`mdel` 实用程序允许你删除 MS-DOS 文件系统上的文件。

### mdir

Syntax:

```
mdir [-/] msdos-file-or-directory
```

`mdir` 实用程序允许你查看 MS-DOS 目录。`- /` 选项还允许你查看所有子目录。

### mformat

Syntax:

```
mformat [-t cylinders] [-h heads] [-s sectors]
```

`mformat` 实用程序允许你格式化软盘以容纳最小的 MS-DOS 文件系统。然而，使用 MS-DOS 机器格式化磁盘比指定柱面、磁头、扇区等要容易得多。我的建议是使用 MS-DOS 机器来完成这项工作，而不是使用 `mformat`。

### mlabel

Syntax:

```
mlabel [-vcs] drive:[new label]
```

`mlabel` 实用程序显示指定驱动器的当前卷标（如果有），如果在命令行中在 `drive:` 之后未输入新卷标，则会提示输入新卷标。`-v` 选项打印指定驱动器引导扇区的十六进制转储。`-c` 选项清除现有的卷标。`-s` 选项显示驱动器的现有卷标。

## System Status-Specific Commands

本节讨论的命令涉及系统资源的状态信息。

### dmesg

Syntax:

```
dmesg
```

`dmesg` 程序打印内核在启动期间显示的状态消息。

### free

Syntax:

```
free
```

`free` 程序显示内存使用统计信息。输出示例如下所示：

```
total used free shared buffers cached
Mem: 127776 124596 3180 30740 2904 107504
-/+ buffers/cache: 14188 113588
Swap: 129900 84 129816
```

### shutdown

Syntax:

```
shutdown [-r] [-h] [-c] [-k] [-t seconds] time [message]
```

要关闭系统，请将 `-r` 替换为 `-h`。`-k` 选项允许你在不实际执行的情况下模拟关机事件。例如，

```
shutdown -r -k now System going down for maintenance
```

向所有用户发送虚假的关机消息。`-t` 选项允许你指定警告消息与实际关机事件之间的延迟时间，以秒为单位。在这种情况下，如果你决定中止关机，请使用 `-c` 选项并再次运行 `shutdown` 以取消它。

请注意，你可以使用 `HH:MM` 格式指定时间。例如，

```
shutdown -r 12:55
```

将在 12:55 重启系统。你也可以使用 `+minutes` 来指定时间。例如，

```
shutdown -r +5
```

将在警告消息打印后五分钟开始关机过程。

### uname

Syntax:

```
uname [-m] [-n] [-r] [-s] [-v] [-a]
```

`uname` 命令显示有关当前系统的信息。例如，

```
uname -a
```

```
Linux picaso.nitec.com 2.0.36 #1 Tue Oct 13 22:17:11 EDT 1998 i586 unknown
```
