
```bash
echo "Do you want to trash the dir $file? (y/n) n\b"
else
echo "Do you really want to trash $file? (y/n) n\b"
fi
read doit
# 如果用户回答 y，则执行移动操作。
# 否则打印一条文件未被触的消息。
if [ "${do:-n}" = y ]
then
mv -i $file $trash_dir
echo "$file was trashed to $trash_dir"
let count=count+1
else
# 用于 Bourne shell: count=$(expr $count + 1)
echo "$file was not trashed"
fi
else
# 我们不在交互模式下，所以直接执行。
mv -i $file $trash_dir
let count=count+1
# 用于 Bourne shell: count=$(expr $count + 1)
fi
echo "$0: trashed $count item(s)"
if [ -n "$bad_files" ]
then
echo "The following name(s) do not exist and \c"
echo "could not be trashed:"
echo "$bad_files"
fi
exit 0
```

### 图 23-4 trash Shell 程序（续）

现在让我们运行 `trash` 程序。下面的示例显示了仅运行名为 `trash` 的程序，下一个示例显示了运行 `trash -help`，再一个示例显示了交互式地运行 `trash -i` 移除垃圾文件，最后一个示例显示了运行 `trash -d` 来显示已 `trash` 移除并位于 `/home/martyp/trash` 目录下的文件：

```
martyp $ trash
Usage:
To trash files: trash [-i] file_names_to_trash ...
Display trashed files: trash -d
Remove all trashed files: trash -rm
Print this message: trash -help
martyp $ trash -help
Usage:
To trash files: trash [-i] file_names_to_trash ...
Display trashed files: trash -d
Remove all trashed files: trash -rm
Print this message: trash -help
martyp $ trash -i junk
Do you really want to trash junk? (y/n) y
mv: overwrite /home/martyp/.trash/junk (yes/no)? yes
junk was trashed to /home/martyp/.trash
trash: trashed 1 item(s)
martyp $ trash -d
```

```
/home/martyp/.trash:
total 1364
-rw------ 1 martyp staff 684808 May 30 05:31 core
-rwrwxrxr-x 1 martyp staff 631 May 30 06:45 filele
-rwrwxrxr-x 1 martyp staff 45 May 31 06:04 junk
```

注意，当我们移除文件 `junk` 时，`trash` 询问我们是否要覆盖一个同名文件，该文件之前已通过 `trash` 移除并放置在 `/home/martyp/trash` 目录中。

该程序使用了我们目前为止在这个 shell 编程章节中涵盖的每一个概念。你可能想仔细观察这个程序，以便在你编写的程序中使用这些技术。我还为需要更改的行添加了注释，以便该程序能够在 Bourne shell 中运行。

```
c9t0d0 c9t0d1 c9t0d2 c8t0d0 c8t0d1
c7t0d0 c7t0d1 c7t0d2 c1t0d0 c1t0d1
c9t0d3 c9t0d4 c9t0d5 c8t0d3 c8t0d4
c7t0d3 c7t0d4 c7t0d5 c1t0d3 c1t0d4
c9t0d6 c9t0d7 c9t1d0 c8t0d6 c8t0d7
c7t0d6 c7t0d7 c7t1d0 c1t0d0 c1t0d7
c9t1d1 c9t1d2 c9t1d3 c8t1d1 c8t1d2
c7t1d1 c7t1d2 c7t1d3 c1t1d1 c1t1d2
c9t1d4 c9t1d5 c9t1d6 c8t1d4 c8t1d5
c7t1d4 c7t1d5 c7t1d6 c1t1d4 c1t1d5
```

注意，在此列表中，磁盘以五个一组进行了分组。每五块磁盘将组成一个卷组（volume group）。总共有 10 组五块磁盘，将被放入卷组 `vgu01` 到 `vgu10` 中。还存在五块磁盘的备用组。在发生上述的磁盘控制器故障转移时，将使用这些备用磁盘。以下是文件 `alt` 的列表，包含五块一组的备用磁盘列表：

```
c8t8d0 c8t8d1 c8t8d2 c9t8d0 c9t8d1
c10t8d0 c10t8d1 c10t8d2 c7t8d0 c7t8d1
c8t8d3 c8t8d4 c8t8d5 c9t8d3 c9t8d4
c10t8d3 c10t8d4 c10t8d5 c7t8d3 c7t8d4
c8t8d6 c8t8d7 c8t9d0 c9t8d6 c9t8d7
c10t8d6 c10t8d7 c10t9d0 c7t8d6 c7t8d7
c8t9d1 c9t9d2 c8t9d3 c9t9d1 c9t9d2
c10t9d1 c10t9d2 c10t9d3 c7t9d1 c7t9d2
c8t9d4 c8t9d5 c8t9d6 c9t9d4 c9t9d5
c10t9d4 c10t9d5 c10t9d6 c7t9d4 c7t9d5
```

此列表中显示了共 10 组备用磁盘，它们也将成为卷组 `vgu01` 到 `vgu10` 的一部分。使用在 XP 256 上配置的这些主备用磁盘，我们将在主机系统上设置相应的卷。在本例中，主机系统是一个 V-Class 系统。

让我们了解手动创建其中一组磁盘的步骤。首先，我们将使用 `pvcreate` 命令为卷组中的每块磁盘创建一个物理卷（physical volume）。接下来，我们将使用 `mkdir` 为卷组创建一个目录，然后使用 `mknod` 在目录中为卷组创建一个设备特殊文件。这将为第一个卷组的设置准备所需的目录和特殊文件。接下来，我们将使用 `vgcreate` 创建包含五块主磁盘的卷组，在创建卷组时指定第一块磁盘，然后用 `vgxtend` 其他磁盘。然后通过 `vgxtend` 扩展卷组以包含五块备用磁盘。最后一步为整个卷组创建一个逻辑卷（logical volume）。在示例中，你可能想在一个卷组内创建多个逻辑卷，我们只需要创建一个消耗卷组全部容量（8755 个区块）的逻辑卷。创建第一个卷组的手动步骤如下，我们将通过一个程序来实现自动化：

```bash
# pvcreate /dev/rdsk/c9t0d0
# 为 5 块主磁盘运行
```

```bash
# mkdir /dev/vgu01
# 为第一个卷组创建目录
```

```bash
# mknod /dev/vgu01/group -c 64 0x0100
# 创建带有主次设备号的特殊文件
```

```bash
# vgcreate /dev/vgu01 /dsk/c9t0d0
# 将第一块磁盘放入卷组
```

```bash
# vgxtend /dev/vgu01 /dsk/c9t0d1
# 为剩余四块主磁盘扩展卷组
```

```bash
# vgxtend /dev/vgu01 /dsk/c8t8d0
# 卷组包含五块备用磁盘
```

```bash
# lvcreate -l 8755 /dev/vgu01
# 创建 lvol1（默认情况下）
# 消耗所有 8755 个区块
```
