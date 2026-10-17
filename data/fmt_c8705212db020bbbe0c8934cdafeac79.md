
```
$ ./test2.sh
This is a test program 29075
Loop #1

[1]+ Stopped ./test2.sh
./test2.sh
This is a test program 29080
Loop #1

[2]+ Stopped ./test2.sh
./test2.sh
This is a test program 29105
Loop #1

[3]+ Stopped ./test2.sh
```

## 列表 26.2：继续演示作业控制

```
$ jobs -l
[1] 29075 Stopped ./test2.sh
[2]- 29090 Stopped ./test2.sh
[3]+ 29105 Stopped ./test2.sh
$ kill -9 29105
$ jobs -l
[1]- 29075 Stopped ./test2.sh
[2]+ 29090 Stopped ./test2.sh
```

在列表 26.2 中，我们启动并停止了三个进程。`jobs` 命令显示了三个进程及其状态。注意默认进程（带加号的）是最后一个作业 `29105`。我们使用 `kill` 命令向默认进程发送了 `SIGKILL`。在下一个列表中，之前带减号的作业 `29090` 现在是默认作业。

# 重启停止的作业

在作业控制下，你可以作为后台进程或前台进程重启任何停止的作业。前台进程会接管你正在工作的终端，所以请小心使用。要以后台模式重启作业，使用作业编号配合 `bg` 命令：

```
$ bg 2
[2]+ ./test2.sh &
Test Loop #2
Test Loop #3
```

由于我们以后台模式重启了作业，出现了命令行提示符，允许我们继续执行其他命令。`jobs` 命令的输出显示作业确实在运行（你可以从显示器上的输出判断出来）。

```
$ jobs
[1]+ Stopped
[2]- Running /test2.sh
Test Loop #6
Test Loop #7
Test Loop #8
Test Loop #9
Test Loop #10
This is the end of the test program
[2]- Done /test2.sh
$
```

要以前台模式重启作业，使用作业编号配合 `fg` 命令：

```
$ jobs
[1]+ Stopped ./test2.sh
$ fg 1
Loop #2
Loop #3
```

由于作业以前台模式运行，在作业完成之前我们不会获得新的命令行提示符。

# 按时钟运行

我们确定，当你开始编写脚本时，会遇到一种需要在预设时间运行脚本的情况，通常是你不在场的时候。在指定时间运行脚本有两种常用方法：

*   `at` 命令
*   `cron` 表

每种方法都使用不同的技术来调度运行脚本的时间和频率。接下来的章节将描述这些方法。

# 使用 at 命令调度作业

`at` 命令允许你指定 Linux 系统运行脚本的时间。它将作业提交到队列，并附带运行时间的指示。另一个命令 `atd` 在后台运行并检查作业队列是否有待运行的作业。大多数 Linux 发行版在启动时自动启动它。`atd` 命令检查系统上的特殊目录（通常为 `/var/spool/at/`）是否有通过 `at` 命令提交的作业。默认情况下，`atd` 每 60 秒检查一次该目录。当存在作业时，`atd` 检查作业设置的运行时间。如果时间匹配当前时间，`atd` 将运行该作业。

接下来的章节描述了如何使用 `at` 命令提交作业以及如何管理作业。

# at 命令格式

基本的 `at` 命令格式非常简单：

`at [-f filename] time`

默认情况下，`at` 命令将输入从 `STDIN` 提交到队列。你可以使用 `-f` 参数指定读取命令的文件（你的脚本文件）。`time` 参数指定你希望 Linux 系统何时运行作业。你可以在指定时间上发挥创意。`at` 命令识别许多不同的格式：

*   标准的小时和分钟，例如 `10:15`
*   `AM/PM` 指示符，例如 `10:15 p.m.`
*   特定的命名时间，如 `now`、`noon`、`midnight` 或 `teatime`（下午4点）

如果你指定了一个已经过去的时间，`at` 命令将在第二天运行作业。除了指定运行时间，你还可以包含特定的日期，可以使用不同的日期格式：

*   标准日期格式，例如 `MMDYY`、`MM/DD/YY` 或 `DD.MM.YY`
*   文本日期，例如 `July 4` 或 `Dec 25`，可以或不包含年份
*   你还可以指定不同格式的时间增量：
    *   `Now + 25 minutes`
    *   `10:15 p.m. tomorrow`
    *   `22:15 tomorrow`
    *   `10:15 + 7 days`

当你使用 `at` 命令时，作业会被提交到作业队列。作业队列持有由 `at` 命令提交的作业以便处理。有 26 个作业队列供不同的优先级级别使用。作业队列使用 `a` 到 `z` 的小写字母引用。

默认情况下，所有作业都提交到作业队列 `a`（最高优先级队列）。如果你想以较低的优先级运行作业，可以使用 `-q` 参数指定字母。

# 获取作业输出

当作业在 Linux 系统上运行时，没有与作业关联的显示器。Linux 系统使用提交作业的用户的电子邮件地址。任何指向 `STDOUT` 或 `STDERR` 的输出都会通过邮件系统发送给用户。列表 26.3 显示了使用 `at` 命令调度作业运行的示例。

## 列表 26.3：使用 at 命令启动作业

```
$ date
Feb 28 18:48:02 EST 2019
$ at -f test3.sh 18:49
```

2019年2月28日周四18:49:00 任务 `2`

`$ mail`

```
Heirloom Mail version 12.5 7/5/10. 输入 ? 获取帮助。

"/var/spool/mail/rich": 1 message 1 new

>N 1 Rich Thu Feb 28 18:49 15/568 "Output from your job "
```

```
Message 1:
From rich@localhost.localdomain Thu Feb 28 18:49:00 localdomain
Return-Path: <rich@localhost.localdomain>
X-Original-To: rich
Delivered-To: rich@localhost.localdomain
Subject: Output from your job 2
To: rich@localhost.localdomain
Date: Thu, Feb 28 2019 18:49:00 -0500 (EST)
From: rich@localhost.localdomain
Status: R
```

"此脚本于 18:49:00 运行"

"这是脚本的结束"

如列表 26.3 所示，当我们运行 `at` 命令时，它产生了一条警告消息，指示了系统用于运行脚本的程序（`/bin/sh`，在 Linux 中是 Bash shell），以及分配给任务的任务编号和计划运行的时间。

当任务完成后，显示器上不会出现任何内容，但系统会生成一封电子邮件。电子邮件显示了脚本生成的输出。如果脚本没有产生任何输出，默认情况下不会生成电子邮件。你可以通过使用 `at` 命令中的 `-m` 选项来更改。这将生成一封电子邮件，指示任务已完成，即使脚本没有产生任何输出。

## 查看待处理任务

`atq` 命令允许你查看系统中哪些待处理的任务：

```
$ at -f test3.sh 19:15
warning: commands will be executed using /bin/sh
job 7 at 2007-11-04 10:15
$ at -f test5 4PM
warning: commands will be executed using /bin/sh
job 8 at 2007-11-03 16:00
$ at -f test5 1PM tomorrow
warning: commands will be executed using /bin/sh
```

```
job 9 at 2007-11-04 13:00

$ atq
```

```
7 2007-11-04 10:15 a
8 2007-11-03 16:00 a
9 2007-11-04 13:00 a
$
```

任务列表显示了任务编号、系统运行该任务的日期和时间，以及任务存储的任务队列。

## 删除任务

在了解任务队列中哪些待处理任务的信息后，你可以使用 `atrm` 命令删除待处理的任务：

```
$ atrm 8

$ atq
```

```
7 2007-11-04 10:15 a
9 2007-11-04 13:00 a
$
```

只需输入你想删除的任务编号即可。你只能删除由自己提交执行的任务。你无法删除他人提交的任务。

## 调度常规脚本
