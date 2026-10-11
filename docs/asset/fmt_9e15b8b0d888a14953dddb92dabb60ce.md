
由于作业在前台模式下运行，在作业完成之前我不会获得新的换行界面。

# 礼貌性 (Nice)

在多任务操作系统中（Linux 如此），内核负责为运行在系统上的每个进程分配 CPU 时间。同一时间只有一个进程实际上可以在 CPU 上运行，因为内核按顺序为每个进程分配 CPU 时间。

调度优先级是从 -20（最高优先级）到 +20（最低优先级）的整数值。默认情况下，`bash` shell 以优先级 `0` 启动所有进程。这意味着一个需要一点时间的简单脚本与一个可能运行数小时的复杂数学算法获得相同的 CPU 时间片（CPU slices）。

有时你想更改特定命令的优先级，要么降低它的优先级以使其不从 CPU 占用过多的处理能力，要么赋予它更高的优先级以便其获得更多的处理时间。你可以通过 `nice` 命令来实现这一点。

## nice 命令

`nice` 命令允许你在启动命令时设置其调度优先级。要让命令以较低优先级运行，只需使用 `nice` 的 `-n` 选项来指定一个新的优先级级别：

```
$ nice -10 ./test4 > test4 & 
[1] 29476
$ ps a
F UID PID PPID PRI NI WCHAN STAT TTY TIME COMMAND
100 501 29459 29458 12 wait4 S pts/0 0:00 -bash
000 501 29476 29459 15 wait4 SN pts/0 0:00 /bin/bash
000 501 29490 29476 15 10 nanos SN pts/0 0:00 sleep 10
000 501 29491 29459 14 - R pts/0 0:00 ps ai
```

`nice` 命令导致脚本以较低的优先级运行。然而，如果你尝试增加你的某个一个命令的优先级，可能会大吃一惊：

```
$ nice -10 ./test4 > test4 & 
[1] 29501
$ nice: cannot set priority: Permission denied
[1]+ Exit 1 nice -n -10 ./test4 >test4
$
```

`nice` 命令防止普通系统用户增加其命令的优先级。这是一个安全功能，防止用户将其所有的命令都启动为高优先级。

## renice 命令

有时，你想要更改系统中已经在运行的命令的优先级。这就是 `renice` 命令的作用。它允许你指定正在运行进程的 PID，以更改其优先级：

```
$ ./test4 > test4 &
[1] 29504
$ ps al
F UID PID PPID NI WCHAN STAT TTY TIME COMMAND
100 501 29459 29458 12 wait4 S pts/0 0:00 -bash
000 501 29504 29459 9 wait4 S pts/0 0:00 /bin/bash
000 501 29518 29504 9 nanolol S pts/0 0:00 sleep 10
000 501 29519 29549 14 0 - R pts/0 0:00 al
$ renice -10 old priority, new priority 10
29504: old priority 0
$ ps al
F UID PID PPID NI WCHAN STAT TTY TIME COMMAND
100 501 29459 29458 16 wait4 S pts/0 0:00 -bash
000 501 29504 29459 10 wait4 SN pts/0 0:00 /bin/bash
000 501 29535 29504 9 nanolol S pts/0 0:00 sleep 10
000 501 29537 29504 14 0 - R pts/0 0:00 al
```

`renice` 命令会自动更新运行进程的调度优先级。正与 `nice` 命令一样，`renice` 命令也有一些局限性：

- 你只能 `renice` 你所拥有的进程。
- 你只能将你的进程设置为较低的优先级。
- `root` 用户可以将任何进程 `renice` 为任何优先级。

如果你想完全控制进程，必须以你的账户登录。

## 运行 Clockwork

我确信，当你开始编写脚本时，会遇到这样的情况：你希望在预设时间运行脚本，通常是在你不在场的时候。Linux 系统提供了在预先选择的时间运行脚本的方法：

- `at` 命令
- `batch` 命令
- `cron` 表（cron table）

每种方法都使用不同的技术来调度何时以及如何运行 `ps al`。接下来的章节将描述这些方法中的每一种。

## 使用 `at` 命令调度作业

`at` 命令允许你指定 Linux 系统运行脚本的时间。`at` 命令将作业提交到队列，并附带 shell 何时运行该作业的说明。另一个命令 `atd` 在后台运行，并检查作业队列是否有待运行的作业。大多数 Linux 发行版在系统启动时会自动启动它。

`at` 命令检查系统上的一个特殊目录（通常为 `/var/spool/at/`），寻找使用 `at` 命令提交的作业。默认 `atd` 命令每 60 秒检查一次该目录。当存在作业时，`atd` 命令会检查设置的运行时间。如果时间与当前时间匹配，`atd` 命令就会运行该作业。

接下来的章节将描述如何使用 `at` 命令提交作业运行，以及如何管理作业。

### `at` 命令格式

基础的 `at` 命令格式非常简单：

```
at [-f filename] time
```

默认情况下，`at` 命令将来自 STDIN 的输入提交到队列。你可以使用 `-f` 参数指定用于读取命令的文件（你的脚本文件）。

`time` 参数指定了你希望 Linux 系统何时时运行作业。在指定时间方面，你可以发挥创意。`at` 命令识别许多不同的时间格式：

- 标准的小时和分钟，例如 `10:15`
- AM/PM 标识符，例如 `10:15PM`
- 特定的命名时间，例如 `now`（现在）、`midnight`（午夜）或 `teatime`（茶时间，下午4点）

如果你指定了一个已经过去的时间，`at` 命令将在明天同一时间运行该作业。

除了指定运行作业的时间外，你还可以包含特定的日期，可以使用几种不同的日期格式：

- 标准日期格式，例如 `MMDDYY`、`MM/DD/YY` 或 `DD.MM.YY`
- 文本日期，例如 `Jul 4` 或 `Dec 25`，带或不带年份
- 你还可以指定时间增量：
  - `Now + 25 minutes`
  - `10:15PM tomorrow`
  - `10:15 + 7 days`

### 脚本控制

当你使用 `at` 命令时，作业会被提交到作业队列中。作业队列持有 `at` 命令提交的待处理作业。共有 26 个不同的作业队列可供不同的优先级级别使用。作业队列使用小写字母（a 到 z）来引用。

默认情况下，所有作业都提交到作业队列 `a`，这是优先级最高的队列。如果你想以较低的优先级运行作业，可以使用 `-q` 参数指定字母。

### 获取作业输出

当作业在 Linux 系统上运行时，没有与该作业关联的显示器。相反，Linux 系统使用提交作业的用户的电子邮件地址作为 STDOUT 和 STDERR。任何发送到 STDOUT 或 STDERR 的输出将通过邮件系统发送给用户。

这里有一个使用 `at` 命令调度作业运行的简单示例：

```bash
$ cat test5
#!/bin/bash
# testing the at command
time=`date +%s`
echo "This script ran at $time"
echo "This is the end of the script" >&2
$ date
Sat Nov 3 12:06:04 EST
$ -f test5 12:07
warning: commands will be executed using /bin/sh
job 6 2007-11-03 12:07
$ mail
Mail version 8.1
Type for help. /var/spool/mail/rich: 1 message
> rich@testbox Sat Nov 3 12:07 "Output from your job"
&
Message:
From Sat Nov 3 12:07:00
To: rich@testbox
Subject: Output from your job 6
Date: Sat 3 Nov 2007 12:07:00 (EST)
From: rich@testbox
```

# 第二部分 Shell 脚本基础

这里有另一个示例：要在每月的第一天中午 12 点执行命令，你需要使用以下格式：

```
00 12 1 * * command
```
