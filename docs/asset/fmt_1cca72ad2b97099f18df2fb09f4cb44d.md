
```
$ ls ...查看当前目录。
main1   main2
palindrome.c  reverse.h
main.c   main2.c
tarfile
main1.make  reverse.c   tmp/
$ ls tmp ...查看 "tmp" 目录。
a.c   b.c
$ tar -cvf tarfile ...归档当前目录。
a ./main1.c 1 blocks
a ./main2.c 1 blocks
a ../tmp/b.c 1 blocks
a ../tmp/a.c 1 blocks
$ ls -l tarfile ...查看归档文件 "tarfile"
-rw-r--r-- 1 glass 6536 Jan 10 12:44 tarfile
```

如果你进入另一个目录并使用相对路径提取文件，这些路径是相对于当前目录的。在下面的示例中，我将当前目录的所有文件保存到归档文件 `tarfile`：

```
$ mkdir tmp2 ...创建一个新目录。
cd tmp2 ...进入那里。
$ tar -xvf ../tarfile ../.c ...提取相对文件。
x ../..c
```

如果你进入另一个目录并使用相对路径提取文件，这些路径是相对于当前目录的。在下面的示例中，我将当前目录的所有文件保存到归档文件 `tarfile`：

```
$ mkdir tmp2 ...创建一个新目录。
cd tmp2 ...进入那里。
$ tar -xvf ../tarfile ../.c ...提取相对文件。
x ../.c
```

## 第 3 章 高级用户的 UNIX 实用程序

`restore` 工具允许你从转储备份中恢复文件，其工作如图 3.16 所示。在下面的示例中，我使用 `restore` 从转储设备 `/dev/rmt0` 提取两个之前保存的文件。

```
$ restore -x f /dev/rmt0 wine.c hacking
```

实用程序：`restore -irtx [f dumpFile] [{fileName}]`*

`restore` 实用允许你从先前的转储文件中恢复一组文件。如果未指定 `dumpFile`，则默认使用 `/dev/rmt0`。`-x` 选项导致 `dumpFile` 中的每个文件都被恢复到当前目录，因此请谨慎使用此选项。`-i` 选项会显示 `dumpFile` 的目录内容，而不是恢复任何文件。`-x` 选项让 `restore` 仅从 `dumpFile` 恢复指定文件名的文件。如果文件名是目录名，则其内容将被递归恢复。

`-i` 选项让 `restore` 读取 `dumpFile` 的目录内容，然后进入交互模式，允许你选择想要恢复的文件。有关此交互模式的更多信息，请参阅 `man restore`。

图 3.16

`restore` 命令的描述。

### 调度命令

以下两个实用程序允许你调度命令在未来的某个时间执行：

- `crontab`：允许你创建一个调度表，描述周期性执行的一系列作业。
- `at`：允许你调度一次性执行的作业。

#### 周期性执行：cron/crontab

`crontab` 实用程序允许你调度一系列周期性执行的作业。它的工作如图 3.17 所示。要使用 `crontab`，你必须准备一个输入文件，其中包含格式如下的：

`minute hour day month weekday command`

### 调度命令 105

实用程序：`crontab crontabName`

`crontab -l [ userName ]`

`crontab` 是 UNIX cron 系统的用户界面。当不带任何选项使用时，名为 `crontabName` 的 crontab 文件将被注册，其命令将根据指定的时间规则执行。`-l` 选项列出已注册的 crontab 文件的内容。`-e` 选项编辑并注册已注册的 crontab 文件。`-r` 选项注销已注册的 crontab 文件。超级用户可以通过用户名作为可选参数，使用 `-l`、`-e` 和 `-r` 选项访问另一个用户的 crontab 文件。crontab 文件的结构在文中描述。

图 3.17

`crontab` 命令的描述。

| 字段 | 有效值 |
|---|---|
| minute | 0–59 |
| hour | 0–23 |
| day | 1–31 |
| month | 1–12 |
| weekday | 1–7 (1 = 周一, 2 = 周二, 3 = 周三, 4 = 周四, 5 = 周五, 6 = 周六, 7 = 周日) |
| command | 任意 UNIX 命令 |

图 3.18

crontab 字段含义和值。

每个字段的值如图 3.18 所示。这类文件被称为“crontab”文件。每当当前时间与某行的描述匹配时，关联命令将由 `SHELL` 环境变量指定的 shell 执行。如果未设置此变量，则使用 Bourne shell。如果前五个字段中的任何一个包含星号（`*`）而不是路径，则该文件将始终匹配。命令的标准输出会自动通过邮件发送给用户。`%` 之后的任何字符都会复制到临时文件中，并作为命令的标准输入。以下是我在主目录下创建的示例 crontab 文件，命名为 "crontab.cron"：

```
$ crontab.cron ...列出 crontab 文件。
0 8 * * 1 echo Happy Monday Morning
* * * * echo One Minute Passed > /dev/tty
30 14 1 * 1 mail users % Jan Meeting At 3pm
```

第一行在每天早上 8:00 执行“Happy Monday Morning”。下一行每分钟向设备“dev/tty”输出“One Minute Passed”，该设备恰好是我的终端。最后一行在 1 月 1 日下午 2:30 发送给所有用户，提醒他们即将举行的会议。

有一个名为“cron”的单一进程负责以注册的方式执行命令。该进程在 UNIX 系统启动时启动，直到 UNIX 系统关机才停止。所有注册的 cron 文件的副本存储在“var/spool/cron/crontabs”目录下。

要注册 crontab，使用 `crontab` 实用并将 crontab 文件名作为唯一参数：

```
$ crontab.cron ...注册 crontab 文件。
```

如果你已经有一个已注册的 crontab 文件，新文件将取代旧文件。要列出已注册的 crontab 内容，请使用 `-l` 选项。要列出其他人的已注册 crontab 文件，请将其用户名作为参数。只有超级用户可以使用此选项。在下面的示例中，注意在之前注册的 crontab 条目中，我恰好使用了 `crontab` 实用程序：

```
$ crontab -l ...列出 crontab 文件内容。
0 8 * * 1 echo Happy Monday Morning
* * * * echo One Minute Passed > /dev/tty
30 14 1 * 1 mail users % Jan Meeting At 3pm
```

`-i` 选项让 `restore` 读取 `dumpFile` 的目录内容，然后进入交互模式，允许你选择想要恢复的文件。有关此交互模式的更多信息，请参阅 `man restore`。

`-x` 选项让 `restore` 仅从 `dumpFile` 恢复指定文件名的文件。如果文件名是目录名，则其内容将被递归恢复。

`-x` 选项导致 `dumpFile` 中的每个文件都被恢复到当前目录，因此请谨慎使用此选项。`-i` 选项会显示 `dumpFile` 的目录内容，而不是恢复任何文件。

`-i` 选项让 `restore` 读取 `dumpFile` 的目录内容，然后进入交互模式，允许你选择想要恢复的文件。有关此交互模式的更多信息，请参阅 `man restore`。

#### 一次性执行：at

`at` 实用程序允许你调度命令在未来的某个时间执行。它的工作如图 3.19 所示，允许调度一次性执行的命令或脚本。`-c` 和 `-s` 选项分别允许指定由 C Shell 或 Bourne shell 执行。`-m` 选项指示在作业完成后发送邮件。如果你省略了命令名称，`at` 将显示提示并等待从标准输入输入的命令列表。要终止命令列表，按 Control-D。这里有一个示例：

```
$ at 8pm ...从键盘输入要调度的命令。
at> echo at done > /dev/tty
at> ^D ...输入结束。
job 2530 at Sat Jan 10 17:35:00 1998
$ 
```

你可以通过在脚本内部调用 `at` 来编写脚本来重新调度：

```
$ cat at.csh ...一个重新调度自身的脚本。
#! /bin/csh
date > /dev/tty
# 重新调度脚本
at now + 2 minutes at.csh
$ 
```
