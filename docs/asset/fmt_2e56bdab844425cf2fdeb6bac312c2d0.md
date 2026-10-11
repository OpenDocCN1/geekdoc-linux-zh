
一些硬件解决方案，例如 RAID（`廉价磁盘冗余阵列`），可以提供一定程度的初始安全措施，但最好制定一个时间表，以便在发生数据丢失时仍有备份存在。例如，增量备份策略非常有益，可以缩短备份所需时间，因为该操作仅保存自上次备份以来发生更改的文件。

一种使用两组介质的方法是：
- 星期日。备份整个系统
- 星期一至星期六。备份所有已更改的文件

另一种方法需要七组介质：
- 星期日。备份整个系统
- 星期一至星期六。备份前一天所有已更改的文件

还有一种更全面的方法是：
- 星期日。备份整个系统
- 星期一至星期六。备份前一天所有已更改的文件
- 接下来的星期日。备份上周所有已更改的文件
- 接下来的三周。重复备份并重新开始该过程

选择经济实惠的备份介质也可能是关键因素。然而，由于 CD-R 的价格低廉、高速大容量磁带驱动器以及硬盘存储成本的持续下降，许多管理员选择了这些介质之一。

### 使用 gzip 命令

GNU `gzip` 命令是一种压缩和解压缩工具，类似于 Stuffit。然而，`gzip` 不具备保存 Mac OS 文件所使用的资源叉（resource fork）的能力。`gzip` 可用于文本或二进制文件，但它仅识别 Mac OS 文件的数据叉（data fork）。

`gzip` 命令用于压缩和解压缩文件和目录。你可以使用此命令在拥挤的文件系统中腾出更多空间，或者创建整个目录的归档。在某些情况下，特别是对于文本文档，压缩率可以优于 2:1。

> 大多数 Linux 发行版中包含的另一种压缩工具是 `bzip2` 命令，其压缩效果比 `gzip` 更好。然而，`gzip` 压缩仍然非常流行，已被证明是稳健的，甚至是其他压缩命令的一部分，例如 `archive` 命令 `tar`，以及 `zcat` 和 `zless` 分页器。

![](img/1ea833f5a3e3c1547e3dd2891f52804a_431_0.png)

使用 `gzip` 很简单。例如，要压缩文件，请使用 `gzip` 如下：

```bash
$ `gzip -v` usingthezshell.msg
usingthezshell.msg  67.6% -- replaced with usingthezshell.msg.gz
```

`v` 或 `verbose` 选项会打印压缩百分比和生成的文件名。你还可以使用此命令递归压缩整个目录。例如，以 root 身份：

```bash
# `du -b --summarize /usr/share/doc/howto`
51425280		/usr/share/doc/howto
# `gzip -r` /usr/share/doc/howto
# `du -b --summarize /usr/share/doc/howto`
27000832		/usr/share/doc/howto
```

在此示例中，`/usr/share/doc/howto` 目录的内容需要 50MB 以上的硬盘空间。在使用 `gzip` 命令进行压缩后，该目录需要的空间少于 28MB，为该目录节省了 22MB 以上的空间。（当然，通过删除 HOWTO 文档可以节省更多空间。）

`gzip` 命令也可以在 shell 管道中使用，以压缩标准输入。例如，如果你创建了大型安全日志，你可以按如下方式在流末尾添加压缩：

```bash
# `find / -mtime -1 -print -xdev | xargs ls -1 | gzip > /tmp/seclog.gz &`
```

你可以使用 `gzip` 命令及其 `-d` 选项来解压缩已压缩的文件。然而，许多 Linux 用户转向配套的 `gunzip` 命令，因为它可以处理传统的 DOS zip 压缩归档，如 .zip 文件，以及 UNIX compress 命令归档，如 .Z 文件。使用 gunzip 如下：

```bash
$ gunzip out.gz
gunzip: out already exists; do you wish to overwrite (y or n)? y
```

请注意，如果已存在与未压缩文件同名的文件，系统将询问你是否要覆盖该文件。gunzip 命令还可以根据通过标准输入提供的文件列表来解压缩文件。这意味着你可以轻松解压缩文件列表、目录中的文件以及系统上的所有文件！

Linux 包含相当多的压缩工具。你可以使用 apropos 命令找到其中许多，如下所示：

```bash
$ apropos compress
```

### 使用 tar 命令

磁带归档，或 GNU tar 命令，是现有最受欢迎的归档和压缩程序之一。与其他压缩工具类似，例如 Mac OS 的 StuffIt 或 Windows 的 WinZip，tar 被许多不同的 Linux 发行版和程序员用于分发程序、源代码和其他文档的归档。

作为系统管理员，你可以使用 tar 命令执行备份操作，将用户目录或整个文件系统复制到可移动介质，例如磁带驱动器、硬盘或远程存储设备。通过将 find 命令的输出与 tar 的归档构建相结合，你可以快速开发软件工具，根据文件时间戳、大小或所有权备份系统。

例如，要备份 /home 目录下的所有文件，你可以（以 root 身份）使用 tar 如下：

```bash
# tar cvzf /mnt/remotehd/home.tgz /home
```

该命令行将在 /mnt/remotehd 目录下创建一个名为 home.tgz 的 gzip 磁带归档。若要仅归档过去一天内发生更改的文件，请使用 find 命令向 tar 提供文件名列表，如下所示：

```bash
# find /home -mtime 1 -print | tar cT - ->mnt/remotehd/home01.tgz
```

在此示例中，find 命令返回过去 24 小时内所有已更改文件的列表。此列表通过管道传入 tar 命令，然后创建该目录内容的压缩归档，命名为 home01.tgz。

你可以使用 `zasc` 的选项列出归档文件中的路径名和文件，从而验证归档内容。例如，若要解压并查看新归档文件的内容，请使用如下命令：

```
# tar txf home01.tgz
home/bball/Xdefaults
home/bball/Xresources
home/bball/.bashrc
home/bball/.dayplan
home/bball/.dayplan.priv
home/bball/.dviprc
home/bball/.emacs
home/bball/.exrc
home/bball/.ginitrc
home/bball/.grok
...
```

请注意，此处并未显示所有输出，且行首的目录路径标识符（.）不存在。在将文件恢复到你文件系统的正确目录时，记住这一点非常重要。解压归档文件很简单。使用 `tar` 命令及其 `z` 或 `extract` 选项即可；如果从压缩归档文件中提取，请像这样包含 `z` 选项：

```
# tar xzvf home01.tgz
```

`v` 或 verbose（冗长）选项将列出正在提取的文件，否则操作会静默执行。

通过将 `tar` 命令的功能与 `tar` 的归档创建和压缩特性相结合，即使是新手系统管理员也能快速构建备份脚本，以完成执行备份操作的繁重工作。当加入自动化并在常规计划下独立执行这些任务时，这项工作将变得更加轻松。要了解如何做，请阅读下一节关于使用 cron 进行系统管理的内容。

### 使用 cron 进行调度

每个 Linux 发行版都包含 cron 守护进程，或某种用于执行定期计划任务的其他软件机制。虽然 `at` 命令有助于用户在指定时间执行特定任务，但 `cron` 守护进程通常用于需要重复执行的全系统管理任务。

与其他网络或服务器服务类似，`cron` 调度服务由系统 `/etc/rc.d/init.d` 或 `/etc/init.d` 目录下的启动脚本控制。由于该服务启动了对文件系统健康和完整性至关重要的预编程任务，因此它应始终在你的系统上运行。

`cron` 守护进程每分钟检查一次 `cron` 表（`/etc/crontab`），以获取有关在特定时间运行什么任务的说明。该表的格式在 `crontab` 手册页中有文档说明，看起来像这样（在 LinuxPPC 2000 Q4 系统上）：

```
SHELL=/bin/bash
PATH=/usr/sbin:/usr/bin:/sbin:/bin
MAILTO=root
HOME=/

# m h dom mon dow user  command
00 2  * * *  root run-parts /etc/cron-weekly
30 4 * *  1    root run-parts /etc/cron-monthly
50 4  * * 0   root run-parts /etc/cron-weekly
42 4 1 * *    root run-parts /etc/cron-monthly
```
