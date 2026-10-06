

# 第二部分 Shell 脚本基础

与普通的后台进程一样，shell 会为命令分配作业号，而 Linux 系统会分配 PID 号。区别在于，当你使用 `nohup` 命令时，如果你关闭会话，shell 将忽略终端会话发送的任何 SIGHUP 信号。

由于 `nohup` 命令将进程与终端分离，进程会丢失其 STDOUT 和 STDERR 链接。为了适应命令生成的任何输出，nohup 命令会自动将 STDOUT 和 STDERR 消息重定向到一个名为 `nohup.out` 的文件中。

nohup.out 文件包含了通常会发送到终端屏幕的所有输出。在进程运行完成后，你可以查看 `nohup.out` 文件的输出结果：

```
$ cat nohup.out
This is a test program
Loop #1
Loop #2
Loop #3
Loop #4
Loop #5
Loop #6
Loop #7
Loop #8
Loop #9
Loop #10
This is the end of the test program
$
```

输出出现在 `nohup.out` 文件中的方式就像进程在命令行中运行一样！

> 注意：如果你使用 `nohup` 另一个命令，输出将追加到现有的 `nohup.out` 文件中。在同一目录下运行多个命令时要小心，因为所有输出都将发送到同一个 `nohup.out` 文件，这可能会导致混淆。

# 作业控制

在本章前面的部分，你已经看到了如何使用 `Ctrl-Z` 组合键停止在 shell 中运行的作业。停止作业后，Linux 系统允许你杀死或重启它。你可以使用 `kill` 命令杀死进程。重启已停止的进程需要向它发送一个 `SIGCONT` 信号。启动、停止和恢复作业的功能被称为作业控制。通过作业控制，你对 shell 中运行的进程拥有完全控制权。本节描述了用于查看和控制 shell 中作业的命令。

# 查看作业

作业控制的关键命令是 `jobs` 命令。`jobs` 命令允许你查看 shell 处理的当前作业：

```bash
#!/bin/bash
echo "This is a test program"
count=1
while [ $count -le 10 ]
do
    echo "Loop #$count"
    sleep 10
    count=$((count + 1))
done
echo "This is the end of the test program"
```

```
$ ./test4
This is a test program
Loop #1
[1]+ Stopped ./test4
$ ./test4 > test4 &
$ jobs
[1]+ Stopped ./test4
[2]- Running ./test4 > test4 &
```

脚本使用 `$$` 变量来显示 Linux 系统分配给进程的 PID。在示例中，我从命令行启动了第一个脚本，然后使用 `Ctrl-Z` 停止它。接下来，我使用 `&` 符号启动另一个作业作为后台进程。为了方便，我将脚本的输出重定向到一个文件，这样它就不会显示在屏幕上。

在两个作业启动后，我使用 `jobs` 命令查看分配给 shell 的作业。`jobs` 命令显示了已停止和运行中的作业，以及它们的作业号。`jobs` 命令使用了几个不同的命令行参数，如表 13-2 所示。你可能注意到了输出中的加号和减号。带有加号的作业被视为默认作业。如果命令行中没有指定作业号，则任何作业命令都会引用它。带有减号的作业是在当前默认作业完成后将成为默认作业的作业。无论 shell 中运行了多少个作业，任何时候都只有一个加号作业和一个减号作业。

表 13-2
| 参数 | 描述 |
| :--- | :--- |
| -l | 列出进程的 PID 以及作业号。 |
| -n | 列出自 shell 上次通知以来状态发生变化的作业。 |
| -p | 仅列出作业的 PID。 |
| -r | 仅列出运行中的作业。 |
| -s | 仅列出停止的作业。 |

示例显示了当默认作业移除时，队列中的下一个作业如何接管默认状态：

```
$ ./test4
This is a test program 29075
Loop #1
[1]+ Stopped ./test4
$ ./test4
This is a test program 29090
Loop #1
[2]+ Stopped ./test4
$ ./test4
This is a test program 29105
Loop #1
[3]+ Stopped ./test4
$ jobs -1
[1] 29075 Stopped ./test4
[2]- 29090 Stopped ./test4
[3]+ 29105 ./test4
$ kill -9 29105
$ jobs -1
[1]- 29075 Stopped ./test4
[2]+ 29090 Stopped ./test4
$
```

在这个示例中，我启动了然后停止了三个独立的进程。`jobs` 命令列表显示了三个进程及其状态。注意，默认进程（带有加号列表的）是最后一个启动的进程。我使用 `kill` 命令向默认进程发送了 `SIGKILL` 信号。在下一个 `jobs` 列表中，之前带有减号的作业现在变成了默认作业。

# 重启停止的作业

在 bash 作业控制下，你可以将任何停止的作业作为后台进程或前台进程重启。前台进程会接管你正在工作的终端，使用该功能时要小心。

要在后台模式下重启作业，请使用 `bg` 命令配合作业号：

```
$ bg 2
[2]+ ./test4 &
Loop #2
$ Loop #3
Loop #4

$ Jobs             ./test4
[1]+ Stopped
[2]- Running      ./test4 &
$ Loop #6
Loop #7
Loop #8
Loop #9
Loop #10
This is the end of the test program

[2]- Done          ./test4
$
```

由于我以后台模式重启了作业，命令行界面出现了，允许我继续执行其他命令。`jobs` 命令的输出显示作业确实在运行（你可以从现在出现在屏幕上的输出判断出来）。

要在前台模式下重启作业，请使用 `fg` 命令配合作业号：

```
$ Jobs
[1]+ Stopped      ./test4
$ fg 1
./test4
Loop #2
Loop #3
```

由于作业在前台模式下运行，在作业完成之前我不会获得新的换行界面。

# 礼貌性 (Nice)

在多任务操作系统中（Linux 如此），内核负责为运行在系统上的每个进程分配 CPU 时间。同一时间只有一个进程实际上可以在 CPU 上运行，因为内核按顺序为每个进程分配 CPU 时间。

调度优先级是从 -20（最高优先级）到 +20（最低优先级）的整数值。默认情况下，bash shell 以优先级 0 启动所有进程。这意味着一个需要一点时间的简单脚本与一个可能运行数小时的复杂数学算法获得相同的 CPU 时间片（CPU slices）。

有时你想更改特定命令的优先级，要么降低它的优先级以使其不从 CPU 占用过多的处理能力，要么赋予它更高的优先级以便其获得更多的处理时间。你可以通过 `nice` 命令来实现这一点。

# nice 命令

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

