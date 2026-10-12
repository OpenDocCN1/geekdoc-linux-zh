
## 使用 dump 创建备份

使用 dump 命令进行文件系统备份时，必须提供指定转储级别、备份介质和要备份的文件系统的参数。您还可以提供可选参数来指定备份介质的大小、请求下一盘磁带的方法以及文件系统转储时间和状态的记录。

dump 的第一个参数始终是单字母选项代码的列表。随后是这些选项所需的任何参数的空格分隔列表。参数出现的顺序与需要它们选项的顺序相同。最后一个参数始终是正在备份的文件系统或目录。

```
# dump options arguments filesystem
```

表 13-3 列出了 dump 命令的各种单字母选项代码。

### 表 13-3：dump 的选项

| 转储选项 | 描述 |
| :--- | :--- |
| 0-9 | 转储级别。选择转储级别 0 会备份所有文件（完整转储）。较高的数字仅备份自上次相同或更低级别的转储以来修改过的文件（本质上是增量转储）。默认转储级别为 9。 |
| -B records | 每个卷的转储记录数。基本上是您可以在磁带上容纳的数据量。此选项需要一个数字参数。 |
| -b kbytesperdump | 每个转储记录的千字节数。与 -B 选项结合使用很有用。此选项需要一个数字参数。 |
| -h level | 文件可以标记为 nodump 属性。此选项指定 nodump 属性生效的转储级别或更高级别。此选项需要 1-9 的数字参数。 |
| -f file | 要写入转储的文件或设备名称。这甚至可以是远程机器上的文件或设备。 |
| -d density | 设置磁带密度。默认值为每英寸 1600 位。此选项需要一个数字参数。 |
| -n | 当转储需要注意（例如更换磁带）时，dump 会向 operator 组中的所有用户发送消息。此选项不带参数。 |
| -s feet | 指定转储磁带的英尺长度。此计算取决于磁带密度（选项 d）和转储记录（选项 B 和 b）。需要一个数字参数。 |
| -u | 将此备份记录在 /etc/dumpdates 文件中。使用此选项是个好主意，特别是如果您创建增量备份。 |
| -t date | 指定用于基于增量备份的日期和时间。之后修改或添加的任何文件都将被备份。此选项会导致 dump 忽略 /etc/dumpdates 文件。它接受一个参数，即 ctime 手册页中指定的格式的日期。 |
| -W | 此选项会导致 dump 列出需要备份的文件系统。它通过查看 /etc/dumpdates 文件和 /etc/fstab 文件来实现。 |
| -w | 这与 W 选项类似，但列出应备份的单个文件。 |

因此，一个典型的 dump 命令可能如下所示：

```
# dump 0uBf 500000 /dev/qft0 /dev/hda6
```

此命令会导致 dump 对 /dev/hda6 文件系统执行级别零（完整）备份，将备份存储在磁带驱动器 /dev/qft0 上，并在 /etc/dumpdates 中记录结果。B 选项用于将预期的磁带块计数增加到 500000；否则，dump 会过早地提示更换新磁带。dump 命令将状态消息打印到屏幕，让您知道备份的进展情况并估计完成所需的时间。输出如下所示：

```
DUMP: Date of this level 0 dump: Sat Aug 23 23:33:37 2003
DUMP: Dumping /dev/hda6 (/home) to /dev/qft0
DUMP: Exclude ext3 journal inode 8
DUMP: Label: /home
DUMP: mapping (Pass I) [regular files]
DUMP: mapping (Pass II) [directories]
DUMP: estimated 93303 tape blocks on 0.19 tape(s).
DUMP: Volume 1 started with block 1 at: Sat Aug 23 23:33:47
DUMP: dumping (Pass III) [directories]
DUMP: dumping (Pass IV) [regular files]
DUMP: Closing /dev/qft0
DUMP: Volume 1 completed at: Sat Aug 23 23:35:35 2003
DUMP: Volume 1 94360 tape blocks (92.15MB)
DUMP: Volume 1 took 0:01:48
DUMP: Volume 1 transfer rate: 873 kB/s
DUMP: 94360 tape blocks (92.15MB) on 1 volume(s)
DUMP: finished in 108 seconds, throughput 873 KBytes/sec
DUMP: Date of this level 0 dump: Sat Aug 23 23:33:37 2003
DUMP: Date this dump completed: Sat Aug 23 23:35:35 2003
DUMP: Average transfer rate: 873 kB/s
DUMP: DUMP IS DONE
```

## 理解 dump 级别

**dump** 命令可以备份文件系统上的所有文件，也可以选择性地仅备份最近更改过的文件。*dump level* 参数用于指定此行为。转储级别为 0 会导致对文件系统上的所有文件进行完整备份。指定较高的数字（1–9）仅备份自最近相同或更低转储级别的转储以来已更改或添加的文件。我建议您使用转储级别来实现与表 13-4 中所示类似的完整和增量备份计划。

### 表 13-4：推荐的 dump 计划

| 星期几 | 转储级别 |
| :--- | :--- |
| 星期日 | 级别 0（完整转储）。完成后弹出磁带。 |
| 星期一 | 级别 9（增量转储）。 |
| 星期二 | 级别 8（增量转储）。 |
| 星期三 | 级别 7（增量转储）。 |
| 星期四 | 级别 6（增量转储）。 |
| 星期五 | 级别 5（增量转储）。 |
| 星期六 | 级别 4（增量转储）。 |

请注意，在星期日的完整备份后，第二天会进行级别 9 的增量转储，此后每天都会进行更低的转储级别。这导致自星期日以来更改过的所有文件都在每次增量备份中备份。因此，每个增量备份都比前一个更大；备份包含前一个增量备份中的所有文件以及此后更改的任何文件。这可能看起来浪费了备份磁带上的存储空间，但在需要恢复文件系统时将节省大量时间和精力。

例如，假设您的硬盘在星期五崩溃。更换硬盘后，您可以分两步恢复整个文件系统：恢复上周日的完整备份，然后恢复星期四的最新增量备份。您可以这样做，因为星期四的备份包含星期一、星期二和星期三磁带上的所有文件以及此后更改的文件。如果转储级别按正向顺序进行（星期一为级别 1，星期二为级别 2，等等），则需要恢复*全部*增量备份才能将文件系统恢复到最新状态。

## 使用 cron 自动化备份

您可以使用 shell 脚本和 **cron** 守护进程自动执行大部分备份。使用 `su` 命令成为 root，然后 `cd` 到 `/usr/local/bin` 目录。使用任何文本编辑器创建一个名为 `backups.sh` 的 shell 脚本，其内容如下：

```
#!/bin/sh
#
# backups.sh - A simple backup script, by Thad Phetteplace
#
# This script takes one parameter, the dump level.
# If the dump level is not provided, it is
# automatically set to zero. For level zero (full)
# dumps, rewind and eject the tape when done.
#
if [ $1 ]; then
    level=$1
else
    #
    # No dump level was provided, so set it
    # to zero
    #
    level="0"
fi

/sbin/dump $level'uf' /dev/nrft0 /
/sbin/dump $level'uf' /dev/nrft0 /home
/sbin/dump $level'uf' /dev/nrft0 /var
/sbin/dump $level'uf' /dev/nrft0 /usr

#
# If we are doing a full dump, rewind and eject
# the tape when done.
#
if [ $level = "0" ]; then
    #
    # Note: We should replace this with the /bin/st command
    # instead if we ever switch to a SCSI tape drive.
    #
    /bin/mt -f /dev/nrft0 rewind
    /bin/mt -f /dev/nrft0 offline
fi
```

您可以根据自己的情况更改正在备份的分区，但此脚本在其他方面应该对您非常有用。保存并退出编辑器后，更改文件的权限，使其只能由 root 执行：

```
# chmod 700 backups.sh
```

现在，您可以通过在 root 登录时运行 backups.sh 脚本来备份整个系统。该脚本接受转储级别作为其唯一参数。如果省略参数，它将自动假定为级别零转储。因此，以下两个命令是等效的：
