
The syntax for the ufsdump command is

```
/usr/sbin/ufsdump options arguments file systems to backup
```

where

| 术语 | 描述 |
|------|-------------|
| 选项 | 是一个由单字母选项名称组成的单个字符串。 |
| 参数 | 标识选项参数，可以是多个字符串。选项字母及其对应的参数必须保持相同的顺序。 |
| 要备份的文件系统 | 标识要备份的文件。此参数必须始终放在最后，指定备份的源或内容。它通常标识一个文件系统，但也可以标识单个文件或目录。 |

对于文件系统，请指定文件系统所在磁盘分片的原始设备文件。

表 11-8 描述了 ufsdump 命令的选项和参数。

## 表 11-8 ufsdump 命令的选项

| 选项 | 描述 |
|--------|-------------|
| 0-9 | 备份级别。指定级别 0 对由要备份的文件系统指定的整个文件系统进行完整备份。级别 1-9 用于自上次较低级别备份以来已更改的文件的增量备份。 |
| a archive-file | 指示 ufsdump 创建一个归档文件。将磁带内容的备份表存储在磁盘上的指定文件中。该文件只能被 ufsrestore 理解。ufsrestore 使用该表来确定要恢复的文件是否存在于备份文件中，如果存在，则位于介质的哪个卷上。 |
| b factor | 阻塞因子。指定每次操作写入磁带的 512 字节块数。 |
| c | 指示 ufsdump 备份到盒式磁带。当应用介质末端检测时，此选项将块大小设置为 126。 |
| d bpi | 磁带密度。仅当 ufsdump 无法检测到介质末端时才使用此选项。 |
| D | 磁盘。备份到软盘。 |
| f dump-file | 转储文件。指定备份的目的地。dump-file 参数可以是以下之一： |

- 本地磁带驱动器或磁盘驱动器
- 远程磁带驱动器或磁盘驱动器
- 标准输出

当目标不是默认的本地磁带驱动器 /dev/rmt/0 时使用此参数。如果使用 f 选项，则必须指定 dump-file 的值。

## 表 11-8 ufsdump 命令的选项（续）

| 选项 | 描述 |
|---|---|
| l | 自动装载。如果您有自动装载（堆栈装载器）磁带驱动器，请使用此选项。当磁带末端到达时，此选项将驱动器离线并等待最多两分钟以使磁带驱动器再次准备就绪。如果驱动器在两分钟内准备就绪，则继续。如果驱动器在两分钟后仍未准备就绪，自动装载会提示操作员装载另一盘磁带。 |
| n | 通知。需要干预时，向 sys 组中所有用户的所有终端发送消息。 |
| o | 离线。完成磁带或磁盘后，将驱动器离线，回卷（如果是磁带），并尽可能移除介质（例如弹出磁盘或移除 8 毫米自动装载磁带）。 |
| s size | 大小。指定磁带长度（以英尺为单位）或磁盘大小（以 1024 字节块数为单位）。仅当 ufsdump 无法检测到介质末端时才需要使用此选项。 |
| S | 估算备份大小。确定执行备份所需的空间量（而不实际执行备份），并输出一个数字表示备份的估计大小（以字节为单位）。 |
| t tracks | 轨道。指定 1/4 英寸盒式磁带的轨道数。仅当 ufsdump 无法检测到介质末端时才需要使用此选项。 |
| u | 更新转储记录。对于已完成的文件系统备份，将条目添加到文件 /etc/dumpdates。该条目指示文件系统磁盘分片的设备名称、备份级别（0-9）和日期。当不使用 u 选项或备份单个文件或目录时，不会写入记录。如果已存在同一级别备份的记录，则会被替换。 |
| v | 验证。写入每盘磁带或磁盘后，验证介质内容与源文件系统是否一致。如果出现任何差异，则提示操作员装载新介质，然后重复该过程。仅在未挂载的文件系统上使用此选项，因为文件系统中的任何活动都会导致报告差异。 |
| w | 警告。列出在 /etc/dumpdates 中出现且一天内未备份的文件系统。使用此选项时，所有其他选项将被忽略。 |
| W | 高亮警告。显示出现在 /etc/dumpdates 中的所有文件系统，并突出显示一天内未备份的文件系统。使用此选项时，所有其他选项将被忽略。 |

dump 命令默认使用以下选项：

```
ufsdump 9uf /dev/rmt/0 files-to-back-up
```

以下是 /users 文件系统完整备份的示例：

```
ufsdump 0ucf /dev/rmt/0 /users
DUMP: Writing 63 Kilobyte records
DUMP: Date of this level 0 dump: Sat Dec 12 13:13:22 1998
DUMP: Date of last level 0 dump: the epoch
DUMP: Dumping /dev/rdsk/c0t1d0s0 (pyramid1:) to /dev/rmt/0.
```

```
DUMP: Mapping (Pass I) [regular files]
DUMP: Mapping (Pass II) [directories]
DUMP: Estimated 10168 blocks (4.96MB)
DUMP: Dumping (Pass III) [directories]
DUMP: Dumping (Pass IV) [regular files]
DUMP: Tape rewinding
DUMP: 10078 blocks (4.92MB) on 1 volume at 107 KB/sec
DUMP: DUMP IS DONE
```

在以下示例中，Solaris 2.6 系统上的本地 /export/home 文件系统被备份到名为 sparc1 的远程 Solaris 2.x 系统上的磁带设备。

```
ufsdump 0ucf sparc1:/dev/rmt/0 /export/home
DUMP: Date of this level 0 dump: Sat Dec 12 11:50:01 1998
DUMP: Date of last level 0 dump: the epoch
DUMP: Dumping /dev/rdsk/c0t3d0s7 (/export/home) to /dev/rmt/0 on host sparc1
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

## 使用 ufsrestore 恢复文件系统

使用 ufsrestore 将数据从磁带恢复到磁盘。ufsrestore 命令从使用 ufsdump 命令创建的备份中复制文件。您可以使用 ufsrestore 从级别 0 转储及其后的增量转储中重新加载整个文件系统，或从任何转储磁带中恢复一个或多个单个文件。如果由 root 运行 ufsrestore，文件将以其原始所有者、最后修改时间和模式（权限）恢复。

ufsrestore 命令的语法是

```
ufsrestore options arguments filename(s)
```

其中

| 术语 | 描述 |
|---|---|
| 选项 | 您必须选择且只能选择以下其中一个选项：i、r、R、t 或 x。 |
| 参数 | 后跟与选项匹配的参数。 |
| 文件名(s) | 指定作为 x 或 t 选项参数的要恢复的文件，并且必须始终放在最后。 |

表 11-9 描述了 ufsrestore 命令的一些更常见的选项和参数。有关完整列表，请参阅 Solaris 在线手册页。

## 表 11-9 ufsrestore 命令选项

| 选项 | 描述 |
|---|---|
| i | 交互式。以交互模式运行 ufsrestore。在此模式下，您可以使用有限的 shell 命令集浏览介质内容并选择要恢复的单个文件或目录。有关可用命令列表，请参阅表 11-10。 |
| r | 递归。将介质的全部内容恢复到当前工作目录，该目录应为文件系统的顶层。用于在完整转储之上恢复增量转储的信息也包含在内。要完全恢复文件系统，请使用此选项恢复完整（级别 0）转储，然后对每个增量转储执行。这适用于刚刚使用 newfs 命令创建的新文件系统。 |
| x filename(s) | 提取。选择性地恢复 filename(s) 参数指定的文件。Filename(s) 可以是文件和目录的列表。除非您还使用 h 选项，否则指定目录下的所有文件都会被恢复。如果省略 filename(s) 或为根目录输入“.”，则会恢复介质（或来自标准输入）上所有卷上的所有文件。现有文件将被覆盖并显示警告。 |
| t filename(s) | 目录表。检查 filename(s) 参数指定的文件与介质是否匹配。对于每个文件，都会列出完整文件名和 inode 编号（如果找到文件）。如果未找到文件名，ufsrestore 会指示该文件不在“卷”上，即多卷转储中的任何卷。如果未输入 filename(s) 参数，则列出介质上所有卷上的所有文件，而不区分文件位于哪个卷上。当使用 h 选项时，仅检查并列出 filename(s) 中指定的目录文件，而不包括其内容。目录表从介质的第一卷读取，或（如果使用 a 选项）从指定的归档文件读取。此选项与 x 和 r 选项互斥。 |
| b factor | 阻塞因子。指定每次操作写入磁带的 512 字节块数。默认情况下，ufsrestore 会尝试确定写入磁带时使用的块大小。 |
| m | 将指定文件恢复到磁盘上的当前目录，而不考虑它们在备份层次结构中的位置，并使用其 inode 编号重命名它们。例如，如果当前工作目录是 /files，备份中名为 ./database/test 且 inode 编号为 156 的文件将被恢复为 /files/156。此选项在仅提取少数文件时很有用。 |
| s n | 跳转到介质上的第 n 个备份文件。当您将多个备份放在同一盘磁带上时，此选项很有用。 |
| v | 详细。显示每个文件在恢复时的名称和 inode 编号。 |

