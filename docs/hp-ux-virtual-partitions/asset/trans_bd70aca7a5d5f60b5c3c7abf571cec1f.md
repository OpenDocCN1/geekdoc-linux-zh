

/usr/sbin/fbackup -f device [-0-9] [-u] [-i path] [-e path] [-g graph]

- `-f device`
  备份使用的磁带驱动器，例如本地磁带驱动器为 `/dev/rmt/0m`。
- `[-0-9]`
  这是备份的级别。如果你在周日执行级别 0 的完全备份，那么在其他工作日你应执行级别 1 的增量备份。增量备份会备份自较低级别备份以来所有更改的信息。你可以在周日执行级别 0，周一执行级别 1，周二执行级别 2，以此类推。然而，为了恢复系统，你需要依次加载周日的磁带，然后周一的磁带，再周二的磁带，等等，才能完全恢复。
- `[-u]`
  此选项更新过去备份的数据库，使其包含诸如备份级别、备份会话的开始和结束时间以及用于备份会话的图形文件（如下所述）等信息。此选项仅在配合 `-g (graph)` 选项时有效。
- `[-i path]`
  指定的路径将包含在备份中。此选项可以指定任意次数。
- `[-e path]`
  指定的路径将从备份中排除。此选项也可以指定任意次数。
- `[-g graph]`
  图形文件包含要包含或排除在备份之外的文件和目录列表。

尽管 fbackup 非常彻底且易于使用，但它并未内置全量备份和增量备份运行的日期和时间。你必须创建一个 cron 条目来自动运行 fbackup。SAM 会为你创建一个 cron 条目，从而让你可以随时运行 fbackup。（cron 在第 11 章中有详细介绍。）

在最简单形式下，我们可以运行 fbackup，并通过 f 选项指定磁带驱动器，通过 i 选项指定要备份的目录，如下例所示：

由于未包含用于详细模式的 v 选项，fbackup 未生成包含在备份中的文件列表。

要查看磁带的内容，我们运行带有 `r`（读取）、`N`（防止磁带内容恢复到系统）和 `v`（详细）选项的 `frecover`，如下面的命令所示：

```bash
# frecover -rNv -f /dev/rmt/0m
drwxr-xr-x    root    root    /
dr-xr-xr-x    bin     bin     /var
drwxrwxrwx    bin     bin     /var
drwxr-xr-x    root    sys     /var/tmp/OBAMFBAa01630
-rw----root    sys     /var/tmp/OBAMHBAa01020
-rw----root    sys     /var/tmp/OBAMHBAa01540
-rw----root    sys     /var/tmp/OBAMHBAa07762
-rw-rw-rw-     root    sys     /var/tmp/aaa01112
...
-rw-rw-rw-     root    sys     /var/tmp/eaa01487
-rwxr-xr-x     root    root    /var/tmp/envd.action2
-rwxr-xr-x     root    root    /var/tmp/envd.action5
-rw-rw-rw-     root    sys     /var/tmp/exclude.temp
dr-xr-xr-x     bin     bin     /var/tmp/ntp
-rw-rr-xr-x     sys     /var/tmp/swagent.log
-rw-rw-rw-     root    sys     /var/tmp/tmf_cfg.file
#
```

现在让我们从系统中删除一个作为备份一部分包含在内的文件。然后我们将只恢复我们删除的那个文件。我们将使用 `x` 选项表示提取，并使用 `i` 选项指定要包含的文件，配合 `frecover` 使用，如下例所示：

```bash
# cd /var/tmp
# ls -1 aa*
-rw-fw-rw- 1 root sys      102 Jul 11 15:20 aaaa01112
-rw-fw-rw- 1 root sys      102 Jul 11 15:37 aaaa01299
-rw-fw-rw- 1 root sys      102 Jul 11 15:37 aaaa01333
-rw-fw-rw- 1 root sys      102 Jul 11 15:38 aaaa01354
-rw-fw-rw- 1 root sys       99 Jul 11 15:40 aaaa01380
-rw-fw-rw- 1 root sys       99 Jul 11 15:40 aaaa01405
-rw-fw-rw- 1 root sys      102 Jul 11 15:47 aaaa01426
-rw-fw-rw- 1 root sys       99 Jul 11 15:45 aaaa01487
-rw-fw-rw- 1 root sys      102 Jul 11 14:24 aaaa01558
# rm aaaa01487
# cd /
# frecover -x -i /var/tmp/aaaa01487 -f /dev/rmt/0m
# cd /var/tmp
# ls -1 aa*
-rw-fw-rw- 1 root sys      102 Jul 11 15:20 aaaa01112
-rw-fw-rw- 1 root sys      102 Jul 11 15:37 aaaa01299
-rw-fw-rw- 1 root sys      102 Jul 11 15:37 aaaa01333
-rw-fw-rw- 1 root sys      102 Jul 11 15:38 aaaa01354
-rw-fw-rw- 1 root sys       99 Jul 11 15:40 aaaa01380
-rw-fw-rw- 1 root sys       99 Jul 11 15:40 aaaa01405
-rw-fw-rw- 1 root sys      102 Jul 11 15:47 aaaa01426
-rw-fw-rw- 1 root sys       99 Jul 11 15:45 aaaa01487
-rw-fw-rw- 1 root sys      102 Jul 11 14:24 aaaa01558
#
```

在上面的示例中，我们使用 frestore 成功地从磁带上恢复了文件 /var/tmp/aaaa01487。

备份有一些强大的功能，我们在示例中并未使用。这些包括备份级别、图形文件和索引文件。backup 支持 0-9 的备份级别，0 用于完全备份，其他数字表示各种增量备份级别。

图形文件用于指定包含在备份中的文件。索引文件包含作为备份一部分生成的文件列表。让我们看一个使用所有这些功能的示例。首先，我们创建一个图形文件，其中包含我们要包含 (i) 或排除 (e) 作为备份一部分的文件。在我们的情况下，该文件将仅包含以下一行：

```text
i /var/tmp
```

现在让我们运行 fbackup，使用 u 更新备份数据库，O 进行完全备份，f 指定我们要写入备份的文件（在此示例中，我们将使用文件而不是磁带），g 指定我们的图形文件，I 指定索引文件的名称，最后，我们将消息重定向到一个包含备份日志的文件。我们还会在索引和备份日志文件的末尾添加日期和时间。

```bash
# fbackup -Ou -f /tmp/testbackup -g /tmp/backupgraph \
-I /tmp/backupindex.`date '+%y%m%d.%H:%M'` 2> /tmp/backuplog.`date '+%y%m%d.%H:%M'`
#
```

现在我们来看看执行此命令后生成了哪些文件。首先让我们查看备份索引和备份日志文件：

```bash
# ls /tmp/backup*
backupgraph
backupindex.000712.15:04
backuplog.000712.15:04
# 
# cat /tmp/backupindex000712.15:04
1024          1 / 
1024          1 /var
2048          1 /var/tmp
0             1 /var/tmp/OBAMFEA01630
0             1 /var/tmp/OBAMHBAO1020
0             1 /var/tmp/OBAMHBAo1540
336           1 /var/tmp/OBAMHBAo7762
102           1 /var/tmp/aaa01112
            .
            .
            .
28            1 /var/tmp/aaaa1487
28            1 /var/tmp/envd.action2
28            1 /var/tmp/envd.action5
4608          1 /var/tmp/exclude.tmp
96            1 /var/tmp/stmp
1595          1 /var/tmp/swagent.log
205           1 /var/tmp/tmp_cfg_file
# 
# cat /tmp/backupgraph000712.15:04
1/var/tmp
# 
# cat /tmp/backuplog000712.15:04

fbackup(1004): session begins on Wed Jul 12 14:56:19 2000
fbackup(3024): writing volume 1 to the output file /tmp/testbackup
fbackup(1030): warnings encountered during backup
fbackup(3055): total file blocks read for backup: 3614
fbackup(3056): total blocks written to output file /tmp/testbackup:3876
#
```

带有日期附加在文件名末尾（7/12/00 时间 15:04）的三个文件是由之前发出的 **fbackup** 命令生成的。附加在文件末尾的日期有助于组织备份文件。我们可以使用 **frestore** 从包含备份信息的文件（*`/tmp/testbackup`*）中恢复其中任意或所有文件，如前所示。

我们并不局限于对连接到本地系统的磁带驱动器进行备份。我们可以通过指定系统名称和磁带驱动器或文件来使用 **fbackup** 备份到远程磁带，将文件存储到我们想要的位置。下面的示例使用了之前介绍的 **fbackup** 选项，并且包含了带有磁带驱动器的系统名称：

```bash
# fbackup -f tapesys:/dev/rmt/0m -i /var/tmp -v
fbackup(1004): session begins on Wed Jul 12 15:56:22 2000
fbackup(3507): volume 1 has been used 1 time(s) (maximum: 100)
fbackup(3024): writing vol 1 to output file tapesys:/dev/rmt/0m
1: /
2: /var
3: /var/tmp
4: /var/tmp/AAAA1812 0
5: /var/tmp/AAAA1992 0
6: /var/tmp/BEQ19522 19
7: /var/tmp/DCB19522 0
8: /var/tmp/DBC19522 0
9: /var/tmp/ISPX19522 0
.
.
.
73: /var/tmp/eaaa13306 1
74: /var/tmp/ems_inittab.old 2
75: /var/tmp/envd.action2 1
76: /var/tmp/envd.action5 1
77: /var/tmp/inet.conf.old 9
78: /var/tmp/net19522 1799
79: /var/tmp/swagent.log 16
fbackup(1005): run time: 43 seconds
fbackup(3055): total file blocks read for backup: 1974
fbackup(3056): total blocks written to output file ori:/dev/rmt/0m: 0
#
```

此命令通过系统将文件发送到系统 *tapesys* 上的磁带驱动器，从而在系统 *or1* 上执行 */var/tmp* 的备份。我们可以使用许多其他选项给 **fbackup**，如前面的示例所示，但我希望保持示例简单，以便容易看出远程磁带驱动器的指定方式。

