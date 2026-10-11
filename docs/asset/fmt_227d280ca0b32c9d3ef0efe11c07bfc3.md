
与 `tar` 工具一样，`cpio` 归档不需要扩展名来识别其内容。但是，使用扩展名是一个良好的习惯，如上面的示例 `/root/sample.cpio` 所示。

## dump/restore 工具

与 `tar` 和 `zip` 工具一样，`dump/restore` 工具可用于将文件和目录备份到设备或文件系统的文件中。然而，`dump/restore` 工具只能用于 `ext2` 和 `ext3` 文件系统上的文件。

尽管 `dump/restore` 工具可以仅备份某些文件和目录，但它的设计目的是将整个文件系统转储到归档，并在名为 `/etc/dumpdates` 的文件中跟踪这些文件系统。由于备份文件系统上的所有数据（称为全备）可能需要很长时间，你可以选择在周末进行全备，而在工作周期间进行增量备份。增量备份仅备份自上次备份以来更改的数据。发生系统故障时，你可以从全备中恢复信息，然后按顺序从所有后续增量备份中恢复信息。你可以使用 `dump/restore` 工具执行最多九种不同的增量备份；数字 `0` 代表全备，而数字 `1` 到 `9` 代表增量备份。

例如，假设你在周日对 `/dev/hda3` 文件系统进行了全备，从周一到周三进行了增量备份，并在周四 `/dev/hda3` 文件系统发生损坏，如图 13-1 所示。图 13-1 备份策略：一旦文件系统重建，你应该恢复全备 (`0`)，然后是第一个增量备份 (`1`)、第二个增量备份 (`2`) 和第三个增量备份 (`3`)，以确保数据已恢复。

`dump/restore` 工具拥有许多类似于 `tar` 和 `cpio` 工具的选项。其列表见表 13-7。

### 表 13-7 在 dump/restore 工具中使用的常用选项

| 选项 | 描述 |
| --- | --- |
| `-n` | 指定 `dump` 命令使用的备份类型（如果 `#` 是 `0`，则执行全备；如果 `#` 是 `1` 到 `9`，则执行相应的增量备份） |
| `-b NUM` | 指定块大小（千字节）；默认大小为 10 千字节 |
| `-f FILENAME` | 指定归档路径；`FILENAME` 是文件或设备 |
| `-u` | 指定备份完成后更新 `/etc/dumpdates` 文件 |
| `-n` | 在发生错误或备份完成后通知用户 |
| `-r` | 在 `restore` 命令中使用，提取整个归档 |
| `-x FILENAME` | 在 `restore` 命令中使用，提取由 `FILENAME` 指定的文件 |
| `-i` | 在 `restore` 命令中使用，以交互方式恢复文件并提示用户操作 |
| `-t` | 在 `restore` 命令中使用，列出现有归档的文件名内容（目录） |
| `-v` | 在操作归档时显示详细输出（文件和目录信息） |

例如，取 `df` 命令的输出：

```
[root@localhost]# df

Filesystem     1k-blocks Used% Mounted on

dev/hda3       4032124 284060  75% /

dev/hda2       101170  10550  12% /boot

none             192232       0% /dev/shm

[root@localhost]#
```

要将 `/boot` 分区 (`/dev/hda2`) 全备到第一个 SCSI 设备并在完成后更新 `/etc/dumpdates` 文件，你可以执行以下命令：

```
[root@localhost]# dump -f /dev/st0 /dev/hda2

DUMP: Date of this level 0 dump: Sat Jul 27 16:43:09 2003

DUMP: Dumping /dev/hda2 (/boot) to /dev/st0

DUMP: Exclude ext3 inode 8

DUMP: Label: /boot

DUMP: mapping (Pass I) [regular files]

DUMP: mapping (Pass II) [directories]
```

```
DUMP: estimated 6485 tape blocks.

DUMP: Volume 1 started with block 1 at: Sat Jul 27 16:43:10 2003

DUMP: dumping (Pass III) [directories]

DUMP: dumping (Pass IV) [regular files]

DUMP: Closing/dev/st0

DUMP: Volume 1 completed at: Sat Jul 27 16:43:11 2003

DUMP: Volume 1 6470 tape blocks (6.32MB)

DUMP: Volume 1 took 00:00:01

DUMP: Volume 1 transfer rate: 640 KB/s

DUMP: 6470 tape blocks (6.32MB) in 1 volume(s)

DUMP: finished in 1 seconds, throughput 6470 kBytes/sec

DUMP: Date of this level 0 dump: Sat Jul 27 16:43:09 2003

DUMP: Date of this dump completed: Sat Jul 27 16:43:11 2003

DUMP: Average transfer rate: 6470 kB/s

DUMP: DUMP IS DONE

[root@localhost]# _
```

或者，在使用命令时指定文件系统挂载点；命令 `dump -f /dev/st0 /boot` 等于上述示例中的命令。

`/etc/dumpdates` 文件的内容现在将显示已进行全备：

```
[root@localhost]# cat /etc/dumpdates

/dev/hda2 0 Sat Jul 27 16:43:09 2003

[root@localhost]# _
```

要执行第一次增量备份并查看 `/etc/dumpdates` 的内容，可以在 SCSI 磁设备中放置名称并使用以下命令：

```
[root@localhost]# dump -l /dev/st0 /dev/hda2

DUMP: Date of this level 1 dump: Sat Jul 27 16:50:57 2003

DUMP: Date of last level 0 dump: Sat Jul 27 16:43:09 2003

DUMP: /dev/hda2 (/boot) to /dev/st0

DUMP: Exclude journal inode 8

DUMP: Label: /boot

DUMP: mapping (Pass I) [regular files]

DUMP: mapping (Pass II) [directories]

DUMP: estimated 6485 tape blocks.

DUMP: Volume 1 started with block 1 at: Sat Jul 27 16:50:58 2003

DUMP: dumping (Pass III) [directories]

DUMP: dumping (Pass IV) [regular files]

DUMP: Closing/dev/st0

DUMP: Volume 1 completed at: Sat Jul 27 16:50:58 2003

DUMP: Volume 1 6470 tape blocks (6.32MB)

DUMP: Volume 1 took 00:00:01

DUMP: Volume 1 transfer rate: 640 KB/s

DUMP: 6470 tape blocks (6.32MB) in 1 volume(s)

DUMP: finished in less than a second, throughput 6470 kBytes/sec

DUMP: Date of this level 1 dump: Sat Jul 27 16:50:57 2003

DUMP: Date of this dump completed: Sat Jul 27 16:50:58 2003

DUMP: Average transfer rate: 6470 kB/s

DUMP: DUMP IS DONE

[root@localhost]# _
```

# 系统备份 613

```
[root@localhost root]# cat /etc/dumpdates

/dev/hda2 0 Sat Jul 27 16:43:09 2003

/dev/hda2 1 Sat Jul 27 16:50:57 2003

[root@localhost root]# -
```

要查看归档的内容，你可以为 `restore` 命令指定 `-t` 选项，后跟归档信息。要查看之前生成的完整备份内容，可以将相应的磁带放入磁带机并执行以下命令：

```
