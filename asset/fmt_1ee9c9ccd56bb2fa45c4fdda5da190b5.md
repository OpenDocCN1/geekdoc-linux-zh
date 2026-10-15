
要查看此归档的详细目录列表，可以使用以下命令：

```
[root@server1 ~]# cpio -vitB -I /dev/st0

drwx-xr-x 2 root root 0 Jul 27 13:40 /root/sample

-rw-r--r-- 1 root root 20239 Jul 21 08:15 /root/sample/samplefile

-rw-r--r-- 1 root root 574 Jul 21 08:18 /root/sample/samplefile2

5 blocks

[root@server1 ~]#
```

之后，你可以使用以下命令从 `/dev/st0` 提取归档，根据需要创建目录并覆盖文件：

```
[root@server1 ~]# cpio -vicduB -I /dev/st0

/root/sample

/root/sample/samplefile

/root/sample/samplefile2

5 blocks

[root@server1 ~]#
```

像 `tar` 一，`cpio` 命令也可以用于在文件系统的文件上创建归档；对此，在 `-O` 选项后指定文件名。要创建一个名为 `/root/sample.cpio` 包含 `/root/sample` 目录内容的归档，使用

## 第 11 章 压缩、系统备份与软件安装

使用 5KB 的块大小以及公共文件头，要查看结果，可以执行以下命令：

```
[root@server1 ~]# find /root/sample | cpio -vocB -O

/root/sample.cpio

/root/sample

/root/sample/samplefile

/root/sample/samplefile2

5 blocks

[root@server1 ~]# ls -1 sample.cpio

-rw-rw-rw- 1 root root 25600 Jul 27 13:45 sample.cpio

[root@server1 ~]# _
```

与 `dump` 工具一样，`cpio` 归档文件不需要扩展扩展名来识别其内容，但使用扩展名是一个良好的习惯，如前一个示例中的 `/root/sample.cpio` 所示。

### 使用 dump/restore

与 `tar` 和 `cpio` 一样，`dump` 命令可以将文件和目录备份到设备或文件系统上的文件，而 `restore` 命令可用于恢复这些文件和目录。然而，`dump` 和 `restore` 只能在 ext2、ext3 和 ext4 文件系统上工作。

> Fedora 28 或 Ubuntu Server 默认没有安装 `dump` 和 `restore` 命令。若要从互联网上的软件仓库安装它们，你可以在 Fedora 28 上以 root 用户身份运行 `dnf install dump`，或在 Ubuntu Server 上以 root 用户身份运行 `apt-get install dump`。

虽然 `dump` 可备份某些文件和目录，但它的设计初衷是将整个文件系统备份到归档中，并在 `/etc/dump` 文件中跟踪这些文件。由于备份文件系统上的所有数据（称为全备）可能需要很长时间，你可以选择仅在周末进行全备，并在每周的每天傍晚进行增量备份。增量备份仅备份自上次备份以来更改的数据。在系统故障时，你可以按顺序从所有随后的增量备份中恢复信息。你可以使用 `dump` 执行多达九次增量备份；数字代表全备，而数字 1 到 9 代表——

例如，假设你在周日对 `/dev/sda3` 文件系统进行了全备，从周一到周三进行了增量备份，并在周四 `/dev/sda3` 文件系统损坏了，如图 11-1 所示。

图 11-1 示例备份策略

文件系统重建后，你应该先恢复全备 (0)，然后依次恢复第一个增量备份 (1)、第二个增量备份 (2) 和第三个增量备份 (3)，以确保数据已得到正确恢复。

> 差异备份是增量备份的替代方案；它们仅备份自上次备份以来更改的数据。这允许你通过先恢复全备，然后仅恢复最近的差异备份来恢复数据。虽然 `dump/restore` 无法执行差异备份，但许多第三方软件套装可以。

`dump` 和 `restore` 命令有许多可用选项；表 11-8 提供了这些选项的列表。

### 表 11-8 dump/restore 常用选项

| 选项 | 描述 |
| :--- | :--- |
| -# | 与 `dump` 命令配合时指定备份类型；如果 # 为 0，则执行全备。如果 # 为 1 到 9，则执行相应的增量备份。 |
| -b SIZE | 与 `dump` 命令配合时，指定以千字节（KB）为单位的块大小；默认块大小为 10KB。 |
| -f FILENAME | 指定归档文件的路径；`FILENAME` 可以是文件或设备文件。 |
| -u | 指定在备份成功后更新 `/etc/dump` 文件。 |
| -n | 与 `dump` 命令配合时，当发生任何错误或备份完成时会通知用户。 |
| -r | 与 `restore` 命令配合时，提取整个归档。 |
| -x FILENAME | 与 `restore` 命令配合时，提取 `FILENAME` 代表的特定文件或多个文件。 |
| -i | 与 `restore` 命令配合时，恢复文件并对所有操作提示用户进行确认。 |
| -t | 与 `restore` 命令配合时，列出现有归档的文件名内容（目录）。 |
| -v | 在操作归档时显示详细输出（文件和目录信息）。 |

例如，来自以下 `df` 命令的输出：

```
[root@server1 ~] df

Filesystem      1-blocks    Used Available Use% Mounted on

/dev/sda1       30237648   6885728 21815920  24% /

tmpfs            480640         272     480368   1% /dev/shm

/dev/sda3       15481840   1694984 14525924  24% /
```

要将分区 (`dev/sda3`) 全备到第一个可回写的 SCSI 设备磁带，并在完成后更新 `/etc/dump` 文件，你可以使用以下命令：

```
[root@server1 ~]# dump -0uf /dev/st0 /dev/sda3

DUMP: Date of this level 0: Sat Aug 28 10:39:12 2019

DUMP: Dumping /dev/sda3 (data) to /dev/st0

DUMP: Label: none

DUMP: Writing 10 Kilobyte records

DUMP: mapping (Pass I) [regular]

DUMP: mapping (Pass II) [directories]

DUMP: mapping (Pass III) [directories]

DUMP: mapping (Pass IV) [regular files]

DUMP: Writing 10 Kilobyte records

DUMP: mapping (Pass I) [regular]

DUMP: mapping (Pass II) [directories]

DUMP: mapping (Pass III) [directories]

DUMP: mapping (Pass IV) [regular files]

DUMP: Writing 10 Kilobyte records

DUMP: mapping (Pass I) [regular]

DUMP: mapping (Pass II) [directories]

DUMP: mapping (Pass III) [directories]

DUMP: mapping (Pass IV) [regular files]

DUMP: Writing 10 Kilobyte records

DUMP: mapping (Pass I) [regular]

DUMP: mapping (Pass II) [directories]

DUMP: mapping (Pass III) [directories]

DUMP: mapping (Pass IV) [regular files]

DUMP: Writing 10 Kilobyte records

DUMP: mapping (Pass I) [regular]

DUMP: mapping (Pass II) [directories]

DUMP: mapping (Pass III) [directories]

DUMP: mapping (Pass IV) [regular files]

DUMP: Writing 10 Kilobyte records

DUMP: mapping (Pass I) [regular]

DUMP: mapping (Pass II) [directories]
```
