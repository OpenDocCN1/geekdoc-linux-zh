
## 8.5 批处理作业

通常，当你输入命令时，其意图是它应立即执行。然而，有时用户希望在稍后的时间将命令作为批处理作业执行，甚至在用户注销之后。

### 8.5.1 cron

有一个名为 crond 的程序，大多数系统安排在启动序列中的某个时间运行。名称末尾的‘d’表示这是 cron 守护进程。与许多守护进程一样，该程序在机器运行时持续运行，其唯一功能是定期检查一组命令文件的内容，并在适当的时间执行这些文件中的命令。

命令文件各自包含一组命令行。命令行的一般格式为：

```
minutes hours days months day_names command
```

minutes、hours、days、months 和 day_names 字段允许你指定关联命令的执行时间。例如：

```
25 8 27 Jan * birthday
```

每天 1 月 27 日 08:25 am，crond 将执行用户名为 birthday 的程序。day_names 字段中的星号 (*) 表示‘在发生的任何一天’。

星号通常表示‘匹配任何可能的值’，它也可以用于其他日期和时间字段：

```
25 8 * * * appointments
```

这表示每天/每月/每周的 08:25 am 运行用户程序 appointments。

如果你只想在工作日（即周一至周五）运行 appointments，则可以在 day_names 字段中列出，用逗号分隔：

```
25 8 * * mon,tue,wed,thu,fri appointments
```

day_names 字段中那样的连续值列表也可以指定为简单的范围，含义相同：

```
25 8 * * mon-fri appointments
```

如果在同一命令行中指定 days 和 day_names，则两者都适用：

```
0,15,30,45 * 1 * mon oddtimes
```

此示例将在每个月的第一天以及每周一每 15 分钟执行一次用户命令 oddtimes。

每个用户登录都可以有自己的关联命令文件与 crond 一起使用。这些命令文件存储在目录中：

/usr/spool/cron/crontabs

然而，普通用户无法直接访问此目录，因此他们必须使用特殊命令来创建和修改其 crond 命令文件。该命令称为 crontab。有几个命令行开关可用于让 crontab 命令创建、修改和删除你的个人命令文件。crontab 的主要选项和命令行开关为：

- `file [-u user]` replace current command file with file;
- `- [-u user]` replace current command file from standard input;
- `-l [user]` list current command file;
- `-e [user]` edit current command file with vi;
- `-d [user]` delete current command file;
- `-c dir` specify a new command file directory.

只有 root 才能指定 -c 开关来更改保存命令文件的目录，只有 root 才能在命令行末尾给出用户名以将给定选项应用于指定用户的命令文件。请记住，这里方括号用于包含可选参数，不应输入。

### 8.5.2 at

使用 crontab 条目可以让给定命令定期执行。然而，可能出现你只有一个批处理作业希望提交给系统在指定时间仅执行一次的情况。

为了满足这一要求，还有另一个命令，称为 at，它仍然依赖 crond 运行，但提供了所需的‘一次性’功能。

为了让 at 工作，root 的 crontab 文件中有一个特殊的命令行。它显示为：

```
0,5,10,15,20,25,30,35,40,45,50,55 * * * *  /usr/lib/atrun
```

该行导致 /usr/lib/atrun 每五分钟执行一次。atrun 执行时，会检查 at 命令作业的待处理列表，找到当前时间需要运行的作业并运行它们。

提交 at 作业很容易。at 命令的一般形式为：

```
at [-f file] time
```

这将在指定时间执行文件中给出的所有命令。如果未给出可选的文件开关，则要执行的命令将从标准输入读取（默认为键盘）：

```
$ at 10:55
date >/tmp/at.job.test
Ctrl-d
Job c00cd3093.00 will be executed using /bin/sh
```

请记住，在单独一行上按 Ctrl-d 是从键盘生成文件结束的方式。请注意，at 命令在序列结束时通过分配唯一的作业引用号进行响应（本例中为 c00cd3093.00）。用户可以使用 atq 命令检查未决作业队列：

```
$ atq
Date          Owner  Queue  Job#
10:55:00 07/27/95  pc     c      c00cd3093.00
```

在 10:55 am 之后检查文件 /tmp/at.job.test 得到：

```
$ cat /tmp/at.job.test
Thu Jul 27 10:55:02 BST 1995
```

还可以使用 atrm 命令后跟作业引用号从队列中删除 at 作业。

at 命令允许你以相当复杂的格式指定作业运行时间，包括诸如：

```
10am Aug 20
6pm tomorrow
7:21 + 4 days
```

最后一个示例表示四天后 7:21 am。此外，日期也可以以多种格式给出，包括：

```
MM/DD/YY
DD.MM.YY
```

这允许按任一顺序指定日和月。

### 8.5.3 batch

还有另一个与 at 紧密相关的命令，执行类似功能，称为 batch。输入 batch 命令与 at 相同，只是无需指定时间。然后提交的作业将在取决于机器负载平均值的时间运行——当机器负载足够轻时，作业就会完成。使用 batch 命令取决于你是否安装了来自 Linux 发行版的 /proc 文件系统，因为它需要从文件读取机器的负载平均值：

/proc/loadavg

root 可以按用户单独允许或拒绝访问 at 和 batch 设施。规则如下：

- root 账户始终可以使用 at 和 batch。
- 对于其他用户，如果文件 /etc/at.allow 存在，则只有列在该文件中的用户登录名才能使用这些设施。
- 如果文件 /etc/at.allow 不存在但文件 /etc/at.deny 存在，则只有未列在该文件中的用户登录名才能使用这些设施。
- 如果两个文件都不存在，则普通用户无法使用 at 或 batch。

Slackware 发行版的默认设置是 /etc/at.deny 存在且为空，从而允许所有人访问这些设施。

## 8.6 归档

在某些系统上，root 可能需要为用户执行生产和维护归档和备份的服务。

存储备份最明显且最易获得的介质是软盘。如果要存储的材料量很小，则在软盘上创建一个 Linux 第二扩展文件系统，将磁盘挂载到根文件系统，然后只需复制文件即可，这是一个简单的任务。假设你从一盘未格式化的 1.44 Mb 软盘开始，保存给定目录（示例中的 src_dir）及其所有子目录和文件的过程为：

```
# fdformat /dev/fd0H1440
# mke2fs /dev/fd0 1440
# mount -t ext2 /dev/fd0 /mnt
# cp -a src_dir /mnt
# umount /mnt
```

此序列中的五个命令执行以下功能：

- 低级格式化软盘。命令行参数指定软盘位于驱动器 fd0（A:）中，并且应将其视为高密度，容量为 1440 Kb（1.44 Mb）。
- 在 /dev/fd0 上创建第二扩展文件系统。第二个命令行参数将设备的大小指定为 1440 个块。
- 将设备 `/dev/fd0` 上的第二扩展文件系统挂载在目录 `/mnt` 下。这是一个空目录，专门为 mount 这种方式使用而提供。
- `cp` 的 `-a` 命令行开关告诉它进行归档复制。这意味着 `src_dir` 下的所有子目录和文件都将被复制到 `/mnt`，保持与原始相同的名称和目录结构。
- 最后的命令将软盘从其余目录层次结构中卸载，以便你可以将其移至安全保存的地方。

### 8.6.1 gzip

在归档材料中包含一个或多个大文件的情况下，你可能希望尝试压缩它们以节省软盘空间。

Linux 发行版中用于文件压缩的标准命令是 GNU gzip 命令。该命令的一般形式为：

```
gzip [options] file
```

指定的文件将被压缩以生成一个新文件，其名称与原始文件相同，但后缀为 .gz。此新文件将替换原始文件。

gzip 有很多选项，最有用的有：

- -1 use fastest compression; output files not as small;
- -9 use maximum compression; takes longer to run;
- -l list some statistics about the files being compressed;
- -h display a help screen of information and options.

通常，大型文本文件会被压缩 60% 到 70%，这可以节省大量的磁盘空间。

对于由 gzip 压缩的文件，可以使用 gunzip 命令将其恢复到原始状态。

```
gunzip file
```

同样，输出文件将替换输入文件。它还将删除 .gz 文件名扩展名。

压缩文件也可以在保持压缩状态的同时读取，使用 zcat 命令。此命令类似于普通的 cat 命令，只是它对压缩文件操作。zcat 的输出发送到标准输出设备，这使得该命令特别适用于读取压缩文本文件，如以下示例所示：

```
$ zcat textfile.gz | more
```

该命令将文件 textfile.gz 的未压缩版本通过管道传输到 more 命令，以分页显示文件包含的文本。
