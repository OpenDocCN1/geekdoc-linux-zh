

## 重启已停止的作业

在 Bash 作业控制下，你可以将任何已停止的作业重启为后台进程或前台进程。前台进程会接管你所操作的终端的控制权，因此使用此功能时请小心。

要在后台模式下重启作业，请使用 `bg` 命令以及作业编号：

```bash
$ bg 2
[2]+ ./test2.sh &
Test 2 Loop #2 output
Test 2 Loop #3 output
Test 2 Loop #4 output
$ jobs
[1]+ Stopped                 ./test2.sh
[2]- Running                 ./test2.sh &
Test 2 Loop #6 output
Test 2 Loop #7 output
Test 2 Loop #8 output
Test 2 Loop #9 output
Test 2 Loop #10 output
This is the end of the test2 program
[2]- Done . /test2.sh
$
```

由于我们是在后台模式下重启了该作业，命令行界面提示符会出现，从而允许我们继续执行其他命令。`jobs` 命令的输出现在显示该作业确实在运行（从现在出现在监视器上的输出可以看出）。

要在前台模式下重启作业，请使用 `fg` 命令以及作业编号：

```bash
$ jobs
[1]+ Stopped . /test2.sh
$ fg 1
. /test4
Loop #2
Loop #3
```

由于该作业在前台模式下运行，直到作业完成之前，我们不会得到新的命令行界面提示符。

# 像时钟一样精确运行

可以肯定的是，随着你开始使用脚本，会出现一种情况，你希望在一个预设的时间运行脚本，通常是在你不在场的时间。有两种常见的方法可以在预选定的时间运行脚本：

- `at` 命令
- `cron` 表

每种方法都使用不同的技术来安排脚本运行的时间和频率。以下各节将描述这些方法中的每一种。

## 使用 at 命令安排作业

`at` 命令允许你指定 Linux 系统运行脚本的时间。它将作业提交到队列中，并附带关于 shell 何时应运行该作业的指示。另一个命令 `atd` 在后台运行，并检查作业队列以查看是否有需要运行的作业。大多数 Linux 发行版在启动时会自动启动它。

`atd` 命令检查系统上的一个特殊目录（通常是 `/var/spool/at`）以查找使用 `at` 命令提交的作业。默认情况下，`atd` 命令每 60 秒检查一次此目录。当存在作业时，`atd` 命令检查该作业设定的运行时间。如果该时间与当前时间匹配，`atd` 命令就会运行该作业。

以下各节描述如何使用 `at` 命令提交要运行的作业以及如何管理这些作业。

## at 命令的格式

基本的 `at` 命令格式非常简单：

```bash
at [-f filename] time
```

默认情况下，`at` 命令将来自 STDIN 的输入提交到队列。你可以使用 `-f` 参数指定用于读取命令（你的脚本文件）的文件名。

time 参数指定你希望 Linux 系统运行该作业的时间。你在指定时间的方式上可以发挥很大的创造性。`at` 命令识别许多不同的时间格式。例如：

- 标准的小时和分钟，如 10:15
- 上午/下午指示符，如 10:15 p.m.
- 特定的命名时间，如 `now`（现在）、`noon`（中午）、`midnight`（午夜）或 `teatime`（4 p.m.）

如果你指定一个已经过去的时间，`at` 命令会在下一天的该时间运行该作业。

除了指定运行作业的时间外，你还可以使用几种不同的日期格式包含特定日期：

- 标准日期格式，如 MMDDYY、MM/DD/YY 或 DD.MM.YY
- 文本日期，如 Jul 4 或 Dec 25，可带或不带年份

你还可以使用不同的格式指定时间增量：

- 现在 + 25 分钟
- 明天 10:15 p.m.
- 明天 22:15
- 10:15 + 7 天

当你使用 `at` 命令时，该作业会被提交到一个*作业队列*。作业队列保存由 `at` 命令提交待处理的作业。有 26 个不同的作业队列可供不同的优先级级别使用。作业队列使用小写字母 a 到 z 进行引用。

默认情况下，所有 at 作业都提交到作业队列 `a`，这是最高优先级队列。如果你希望以较低优先级运行作业，可以使用 `-q` 参数指定字母。

## 检索作业输出

当作业在 Linux 系统上运行时，该作业没有关联的监视器。相反，Linux 系统使用提交该作业的用户的电子邮件地址。任何旨在发送到 STDOUT 或 STDERR 的输出都会通过邮件系统邮寄给用户。

列表 26.3 展示了一个使用 `at` 命令安排作业运行的简单示例。

### 列表 26.3：使用 at 命令启动作业

```bash
$ date
Thu Feb 24 18:48:20 EST 2022
$ at -f test3.sh 18:49
job 2 at Thu Feb 24 18:49:00 2022
$ mail
Heirloom Mail version 12.5 7/5/10. Type ? for help.
"/var/spool/mail/rich": 1 message 1 new
>N  1 Rich         Thu Feb 24 18:49   15/568   "Output from your job "
&
Message  1:
From rich@localhost.localhost   Thu Feb 24 18:49:00 2022
Return-Path: <rich@localhost.localhost>
X-Original-To: rich
Delivered-To: rich@localhost.localhost
Subject: Output from your job         2
To: rich@localhost.localhost
Date: Thu, 24 Feb 2022 18:49:00 -0500 (EST)
From: rich@localhost.localhost (Rich)
Status: R

"This script ran at 18:49:00"
"This is the end of the script"

&
```

如列表 26.3 所示，当我们运行 `at` 命令时，它产生了一个警告消息，指示系统使用哪个 shell 来运行脚本（分配给 `/bin/sh` 的默认 shell，对于 Linux 来说就是 Bash shell），以及分配给该作业的编号和作业计划运行的时间。

当作业完成时，监视器上不会出现任何内容，但系统会生成一条电子邮件消息。电子邮件消息显示了脚本生成的输出。如果脚本不产生任何输出，默认情况下它不会生成电子邮件消息。你可以通过在 `at` 命令中使用 `-m` 选项来改变这一点。这会生成一条电子邮件消息，指示作业已完成，即使脚本没有产生任何输出。

## 列出待处理作业

`atq` 命令允许你查看系统上有哪些待处理的作业：

```bash
$ at -f test3.sh 10:15
warning: commands will be executed using /bin/sh
job 7 at 2022-03-04 10:15
$ at -f test5 4PM
warning: commands will be executed using /bin/sh
job 8 at 2022-03-03 16:00
$ at -f test5 1PM tomorrow
warning: commands will be executed using /bin/sh
job 9 at 2022-03-04 13:00
$ atq
7	2022-03-04 10:15 a
8	2022-03-03 16:00 a
9	2022-03-04 13:00 a
$
```

作业列表显示作业编号、系统运行该作业的日期和时间，以及存储该作业的作业队列。

## 删除作业

在知道了作业队列中哪些作业是待处理的信息后，你可以使用 `atrm` 命令来删除待处理作业：

```bash
$ atrm 8
$ atq
7	2022-03-04 10:15 a
9	2022-03-04 13:00 a
$
```

只需指定你想要删除的作业编号。你只能删除你提交执行的作业。你不能删除其他人提交的作业。

## 安排定期脚本

使用 `at` 命令安排脚本在预设时间运行是很棒的，但如果你需要该脚本每天在同一时间运行，或者每周运行一次，或者每月运行一次怎么办？与其不断提交 at 作业，你可以使用 Linux 系统的另一个功能。

Linux 系统使用*cron*程序，允许你安排需要定期运行的作业。*cron*程序在后台运行，并检查称为*cron 表*的特殊表，以查找计划运行的作业。

