

此外，通过将镜像分区直接转换为实际的 /home 分区，你可以更快地开始工作。只需编辑 /etc/fstab 文件，将 /home 的设备名称更改为与镜像目录匹配的名称。现在卸载并重新挂载 /home 分区（或重启计算机），镜像目录就会被挂载到 /home。用户对此毫不知情。你甚至可以考虑镜像主磁盘上的每个分区。这样，即使发生完整的磁盘故障，也能快速恢复。只需将辅助磁盘转换为主磁盘，系统即可恢复运行。

## 自动化镜像

为了自动化镜像过程，我建议创建一个小型脚本，该脚本用于挂载镜像分区，运行 mirror dir 命令，然后卸载分区。在不使用分区时保持其未挂载状态，可以减少数据被意外删除的可能性。创建一个名为 mirror.sh 的脚本，并将其放置在 /usr/local/sbin 目录中。类似以下内容应该就能解决问题：

```
#!/bin/sh
#
# mirror.sh: Mirror the /home partition to a second hard drive
#
/bin/mount /dev/hdb5 /mirror/home
mirror dir /home /mirror/home
/bin/umount /mirror/home
```

现在告诉 cron 定期运行此脚本。使用 -e 选项调用 cron 命令。这会打开一个包含 root 的 cron 任务的编辑器。在列表末尾添加类似以下的一行。

```
0 * * * * /usr/local/sbin/mirror.sh
```

保存并退出编辑器。这个 cron 条目会使 mirror.sh 脚本每小时运行一次。如果你决定镜像其他分区，你可以通过在 /mirror 中创建相应的挂载点，然后在 mirror.sh 脚本中添加相应的部分，轻松完成此操作。

## 使用 dump 备份文件

dump 命令是在 UNIX 系统上执行备份最常用的工具。该命令的历史可以追溯到 UNIX 的早期，因此几乎是每个 UNIX 版本的标准组成部分。同样，dump 软件包也包含在 Red Hat Linux 发行版中。如果在初始设置 Linux 系统时没有默认安装它，你可以从第二个 Red Hat Linux 安装光盘上位于 dump RPM 文件中安装它。

dump 软件包实际上由几个命令组成。你可以阅读它们的在线 man 页面以获取更多信息，但表 13-2 对这些程序进行了简短描述。

### 表 13-2：dump 软件包中的程序

| **命令** | **描述** |
| :--- | :--- |
| `dump` | 用于创建整个磁盘分区或单个目录的备份存档。 |
| `restore` | 可用于将存档中的整个内容或单个文件恢复到硬盘。 |
| `rmt` | `dump` 和 `restore` 命令使用的程序，用于通过网络复制文件。你绝不应该直接使用该命令。 |

### 使用 dump 创建备份

使用 dump 命令制作文件系统备份时，你必须提供指定转储级别、备份媒体和要备份的文件系统的参数。你还可以提供可选参数来指定备份媒体的大小、请求下一盘磁带的方法以及记录文件系统转储时间和状态。

dump 的第一个参数始终是一组单字母选项代码的列表。随后是那些选项所需的参数列表，参数之间用空格分隔。参数的顺序与需要它们的选项顺序相同。最后一个参数始终是正在备份的文件系统或目录。

```
dump <options> <arguments> <filesystem>
```

表 13-3 列出了 dump 命令的各种单字母选项代码。

### 表 13-3：dump 的选项

| **转储选项** | **描述** |
| :--- | :--- |
| 0-9 | 转储级别。选择转储级别 0 会备份所有文件（完整转储）。较高的数字仅备份自上次相同或更低级别转储以来已修改的文件（本质上，这是增量转储）。默认转储级别是 9。 |
| B | 每个卷的转储记录数。基本上，你可以在磁带上容纳的数据量。此选项接受一个数字参数。 |
| b | 每个转储记录的千字节数。与 B 选项配合使用时很有用。此选项接受一个数字参数。 |
| h | 文件可以标记为 nodump 属性。此选项指定尊重 nodump 属性的转储级别或更高级别。此选项接受 1-9 的数字参数。 |
| f | 写入转储的文件或设备名称。这甚至可以是远程机器上的文件或设备。此选项接受单个字母数字参数。 |
| d | 设置磁带密度。默认值为每英寸 1600 位。此选项接受一个数字参数。 |
| n | 当转储需要关注（例如更换磁带）时，dump 会向 operator 组中的所有用户发送消息。此选项不接受参数。 |
| s | 指定转储磁带的长度（以英尺为单位）。此计算取决于磁带密度（选项 d）和转储记录（选项 B 和 b）。此选项接受一个数字参数。 |
| u | 在 /etc/dumpdates 文件中记录此备份。这是一个好主意，特别是如果你创建增量备份。 |
| T | 指定基于增量备份的日期和时间。在此时间之后修改或添加的任何文件都将被备份。此选项导致 dump 忽略 /etc/dumpdates 文件。它接受单个参数，即 ctime man 页面中指定格式的日期。 |
| W | 此选项使 dump 列出需要备份的文件系统。它通过查看 /etc/dumpdates 文件和 /etc/fstab 文件来实现这一点。 |
| w | 这就像 W 选项，但列出应该备份的单个文件。 |

因此，典型的 dump 命令可能类似于以下内容：

```
# dump 0uBf 500000 /dev/qft0 /dev/hda6
```

该命令导致 dump 对 /dev/hda6 文件系统执行级别 0（完整）备份，将备份存储在磁带驱动器 /dev/qft0 上，并在 /etc/dumpdates 中记录结果。使用 B 选项将预期的磁带块计数增加到 500000；否则，dump 会在必要之前过早提示更换新磁带。dump 命令在屏幕上打印状态消息，让你知道备份的进度并估计完成所需的时间。输出类似于以下内容：

```
DUMP: Date of this level 0 dump: Thu May 16 23:33:37 2001
DUMP: Dumping /dev/hda6 (/home) to /dev/qft0
DUMP: Exclude ext3 journal inode 8
DUMP: Label: /home
DUMP: mapping (Pass I) [regular files]
DUMP: mapping (Pass II) [directories]
DUMP: estimated 93303 tape blocks on 0.19 tape(s).
DUMP: Volume 1 started with block 1 at: Thu May 16 23:33:47
DUMP: dumping (Pass III) [directories]
DUMP: dumping (Pass IV) [regular files]
DUMP: Closing /dev/qft0
DUMP: Volume 1 completed at: May Aug 16 23:35:35 2001
DUMP: Volume 1 94360 tape blocks (92.15MB)
DUMP: Volume 1 took 0:01:48
DUMP: Volume 1 transfer rate: 873 kB/s
DUMP: 94360 tape blocks (92.15MB) on 1 volume(s)
DUMP: finished in 108 seconds, throughput 873 kBytes/sec
DUMP: Date of this level 0 dump: Thu Aug 16 23:33:37 2001
DUMP: Date this dump completed: Thu Aug 16 23:35:35 2001
DUMP: Average transfer rate: 873 kB/s
DUMP: DUMP IS DONE
```

## 理解转储级别

dump 命令具有备份文件系统上所有文件的能力，或者它可以有选择地仅备份最近更改的文件。转储级别参数用于指定此行为。转储级别 0 会导致文件系统上所有文件的完整备份。指定较高的数字（1–9）仅备份自最近一次相同或更低转储级别以来已更改或添加的文件。我建议使用转储级别来实施类似于表 13-4 所示的完整和增量备份计划。

### 表 13-4：建议的转储计划

| 星期几 | 转储级别 |
| :--- | :--- |
| 星期日 | 级别 0（完整转储）。完成后弹出磁带。 |
| 星期一 | 级别 9（增量转储）。 |
| 星期二 | 级别 8（增量转储）。 |
| 星期三 | 级别 7（增量转储）。 |
| 星期四 | 级别 6（增量转储）。 |
| 星期五 | 级别 5（增量转储）。 |
| 星期六 | 级别 4（增量转储）。 |

请注意，在星期日的完整备份之后，第二天执行级别 9 的增量转储，之后的每天执行逐级降低的转储级别。这导致自星期日以来更改的所有文件在每个增量备份中都被备份。因此，每个增量备份都比前一个大；备份包含来自前一个增量备份的所有文件以及自那以后更改的任何文件。这可能看起来

