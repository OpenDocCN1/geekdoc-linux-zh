
当目标不是默认的本地磁带驱动器 `/dev/rmt/0` 时使用此参数。如果使用 `f` 选项，必须为 `dump-file` 指定值。

| `l` | 自动加载。如果您有自动加载（堆栈加载器）磁带驱动器，请使用此选项。当磁带末端到达时，此选项将驱动器离线并等待最多两分钟以使磁带驱动器再次准备就绪。如果驱动器在两分钟内准备就绪，则继续。如果驱动器在两分钟后仍未准备就绪，自动加载会提示操作员加载另一盘磁带。 |

| `n` | 通知。当需要干预时，此选项向 `sys` 组所有用户的所有终端发送消息。 |

| `o` | 离线。当 `ufsdump` 完成对磁带或磁盘的操作后，它会将驱动器离线，倒带（如果是磁带），并在可能的情况下移除介质（例如，它弹出磁盘或移除 8mm 自动加载磁带）。 |

| `s` `<size>` | 大小。指定磁带的长度（以英尺为单位）或磁盘的大小（以 1024 字节块数为单位）。仅当 `ufsdump` 无法检测到介质末端时才需要使用此选项。 |

| `s` | 估算备份大小。确定执行备份所需的空间量（而不实际执行备份）并输出一个数字，表示备份估计大小（以字节为单位）。 |

| `t` `<tracks>` | 轨道。指定 1/4 英寸盒式磁带的轨道数。仅当 `ufsdump` 无法检测到介质末端时才需要使用此选项。 |

| `u` | 更新转储记录。对于已完成的文件系统备份，将条目添加到文件 `/etc/dumpdates`。该条目指示文件系统磁盘切片的设备名称、备份级别（0 到 9）以及日期。当不使用 `u` 选项或备份单个文件或目录时，不会写入记录。如果已存在同一级别备份的记录，则会被替换。 |

| `v` | 验证。每次写入磁带或磁盘后，验证介质的内容是否与源文件系统一致。如果出现任何差异，提示操作员装载新介质然后重复该过程。仅在未挂载的文件系统上使用此选项；文件系统中的任何活动都会导致其报告差异。 |

| `w` | 警告。列出 `/etc/dumpdates` 中出现且一天内未备份的文件系统。使用此选项时，所有其他选项将被忽略。 |

| `W` | 带高亮的警告。显示 `/etc/dumpdates` 中出现的所有文件系统，并突出显示一天内未备份的文件系统。使用此选项时，所有其他选项将被忽略。 |

`ufsdump` 命令默认使用以下选项：

```
ufsdump 9uf /dev/rmt/0 <files-to-back-up>
```

## ufsdump 示例

以下示例说明了 `ufsdump` 命令的使用。

以下是 `/users` 文件系统的完整备份示例：

```
ufsdump 0ucf /dev/rmt/0 /users
DUMP: Writing 63 Kilobyte records
DUMP: Date of this level 0 dump: Sat Dec 12 13:13:22 1998
DUMP: Date of last level 0 dump: the epoch
DUMP: Dumping /dev/rdsk/c0t1d0s0 (pyramid1:/users) to /dev/rmt/0.
DUMP: Mapping (Pass I) [regular files]
DUMP: Mapping (Pass II) [directories]
DUMP: Estimated 10168 blocks (4.96MB).
DUMP: Dumping (Pass III) [directories]
DUMP: Dumping (Pass IV) [regular files]
DUMP: Tape rewinding
DUMP: 10078 blocks (4.92MB) on 1 volume at 107 KB/sec
DUMP: DUMP IS DONE
```

在以下示例中，Solaris 8 系统上的本地 `/export/home` 文件系统备份到名为 `sparc1` 的远程 Solaris 8 系统上的磁带设备：

```
ufsdump 0ucf sparc1:/dev/rmt/0 /export/home
DUMP: Date of this level 0 dump: Sat Dec 12 11:50:13 1998
DUMP: Date of last level 0 dump: the epoch
DUMP: Dumping /dev/rdsk/c0t3d0s7 (/export/home) to \
/dev/rmt/0 on host sparc1
DUMP: mapping (Pass I) [regular files]
DUMP: mapping (Pass II) [directories]
DUMP: estimated 19574 blocks (9.56MB)
DUMP: Writing 63 Kilobyte records
DUMP: dumping (Pass III) [directories]
DUMP: dumping (Pass IV) [regular files]
DUMP: level 0 dump on Tue Oct 25 10:30:53 1994
DUMP: Tape rewinding
DUMP: 19574 blocks (9.56MB) on 1 volume
DUMP: DUMP IS DONE
```

如果您想查看备份将需要多少空间，请发出以下命令：

```
ufsdump 0s <filesystem>
```

执行 level 0 备份所需的磁带上估计的字节数将被显示。

## ufsrestore

`ufsr restore` 命令从使用 `ufsdump` 命令创建的备份中复制文件。您可以使用 `ufsrestore` 从 level 0 转储及其后的增量转储重新加载整个文件系统，或从任何转储磁带恢复一个或多个单个文件。如果由 `root` 运行 `ufsrestore`，文件将以其原始所有者、最后修改时间和模式（权限）恢复。

`ufsrestore` 命令的语法如下：

```
ufsrestore <options> <arguments> <filename(s)>
```

`ufsrestore` 命令的选项在表 11.12 中描述。

### 表 11.12

#### ufsrestore 选项

| 选项 | 描述 |
|---|---|
| `<options>` | 为您提供以下选项中仅一个的选择：`i`、`r`、`R`、`t` 或 `x`。 |
| `<arguments>` | 随后是与选项匹配的参数。 |
| `<filename(s)>` | 指定作为 `x` 或 `t` 选项参数要恢复的文件，并且必须始终放在最后。 |

表 11.13 描述了 `ufsrestore` 命令的一些更常见的选项和参数。

### 表 11.13

#### ufsrestore 的命令选项

| 选项 | 描述 |
|---|---|
| `i` | 交互式。以交互模式运行 `ufsrestore`。在此模式下，您可以使用有限的 shell 命令集浏览介质的内容并选择要恢复的单个文件或目录。有关可用命令列表，请参阅表 11.14。 |
| `r` | 递归。将介质的全部内容恢复到当前工作目录，该目录应为文件系统的顶层。用于在完整转储之上恢复增量转储的信息也包含在内。要完全恢复文件系统，请使用此选项恢复完整（level 0）转储，然后恢复每个增量转储。这适用于刚刚使用 `newfs` 命令创建的新文件系统。 |
| `x` `<filename(s)>` | 提取。选择性地恢复您使用 `filename(s)` 参数指定的文件。`filename(s)` 可以是文件和目录的列表。除非您还使用 `h` 选项，否则指定目录下的所有文件都会被恢复。如果省略 `filename(s)` 或为根目录输入 `.`，则介质（或来自标准输入）的所有卷上的所有文件都会被恢复。现有文件将被覆盖，并显示警告。 |

继续

### 表 11.13 继续

#### ufsrestore 的命令选项

| 选项 | 描述 |
|---|---|
| `t` `<filename(s)>` | 目录表。检查介质中指定的 `<filename(s)>` 参数中的文件。对每个文件，列出完整文件名和 inode 编号（如果找到文件）。如果未找到文件名，`ufsrestore` 会指示该文件不在“卷”上，指多卷转储中的任何卷。如果未输入 `<filename(s)>` 参数，则列出介质上所有卷中的所有文件，而不区分文件位于哪个卷上。当使用 `h` 选项时，仅检查并列出 `<filename(s)>` 中指定的目录文件——而不是其内容。目录表从介质的第一卷读取，或（如果使用 `a` 选项）从指定的归档文件读取。此选项与 `x` 和 `r` 选项互斥。 |
| `b` `<factor>` | 阻塞因子。指定每次操作从磁带读取的 512 字节块数。默认情况下，`ufsrestore` 会尝试确定写入磁带时使用的块大小。 |
| `m` | 将指定的文件恢复到磁盘上的当前目录，而不考虑它们在备份层次结构中的位置，并使用其 inode 编号重命名它们。例如，如果当前工作目录是 `/files`，备份中名为 `./database/test` 且 inode 编号为 156 的文件将被恢复为 `/files/156`。此选项在仅提取少数文件时很有用。 |
