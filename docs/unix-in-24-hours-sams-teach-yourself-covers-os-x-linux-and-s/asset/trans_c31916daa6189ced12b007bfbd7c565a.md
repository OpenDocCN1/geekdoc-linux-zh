

| Flag | 含义 |
|------|---------|
| -a | 显示与系统连接的终端关联的所有进程。 |
| -e | 显示系统上的所有进程。 |
| -l | 为每一行提供长列表格式。 |
| -t xx | 仅列出与指定的 ttyxx 关联的进程。 |
| -u | 生成面向用户的输出。 |
| -w | 使用宽输出格式。如果重复 (-ww)，它将尽可能显示每个命令。 |
| -x | 显示系统中的所有进程。 |

## TABLE 15.1 有用的 ps 命令标志，BSD 风格

-a 和 -x 标志会影响 ps 显示的信息量。要使用 -x 命令，您还必须使用 -a 命令。在大多数机器上，-ax 的输出比 -a 多得多。最常用的标志（和标志组合）是 -a，用于列出所有有趣的进程；-ax，用于查看机器上的所有内容（您几乎总是希望将其通过管道传输到 grep 或 more，否则您会被数百行信息淹没）；以及 -w tXX，用于以宽格式显示与 ttyXX 关联的所有进程。

### Note

ps 程序在 System V 和 Berkeley Unix 之间变化比任何其他命令都大。幸运的是，两个或三个最常见的标志在两个系统上是相似的。要探索您系统上 ps 命令的更多信息，您应该从阅读手册页开始。

- 1. 我在后台启动 vi：
- $ vi dickens.note &
- [1] 4352
- $
- 我再次启动那个 awk 作业：

```
$ !awk
awk -F: '{print $1" = "$5}' < /etc/passwd | awk -F, '{print $1}' | awk '{ if (NF > 2) print $0 }' | sort > ! who.is.who &
[2] 4532 4534 4536 4537
$
```

jobs 命令显示我正在运行的进程：

```
$ jobs
[1] + Stopped (tty output) vi dickens.note
[2] - Running awk -F: {print $1" = "$5} < /etc/passwd | awk -F, {print $1} | awk { if (NF > 2) print $0 } | sort > who.is.who
```

2. 现在我知道了作业编号（这里方括号中的数字），我可以轻松地通过指定以 % 为前缀的作业编号将特定作业移至前台或后台。为了说明这一点，我将再把几个 vi 作业放在后台：

```
$ vi buckaroo.confused &
[2] 13056
$ vi awk script csh.man cheryl mbox &
[3] 13144
$
```

现在我使用 jobs 命令查看正在运行的内容：

```
$ jobs
[1] Stopped (tty output) vi dickens.note
[2] - Stopped (tty output) vi buckaroo.confused
[3] + Stopped (tty output) vi awk script csh.man cheryl mbox
$
```

### Note

请注意 awk 作业已完成，不再显示为活动作业。

要编辑 buckaroo.confused 记事本，我只需输入 fg %2 即可将其拉到前台。要终止这些进程（您将在本小时后面了解更多），我可以使用 kill 命令：

```
$ kill %2 %3
$
```

什么也没发生。还是发生了？再次按下 Return 会显示操作系统中发生的情况：

```
$
[3] - Done vi awk script csh.man cheryl mbox
[2] - Done vi buckaroo.confused
$
```

3. 我使用 !awk 重新启动 awk 命令。对比 jobs 的输出与 BSD ps 命令的输出：

```
$ ps
 PID TT STAT TIME COMMAND
4352 Ah T 0:00 vi dickens.note
4532 Ah R 0:03 awk - : {print $1"}
4534 Ah R 0:02 awk - , {print $1}
4536 Ah S 0:01 -k { if (NF > 2) print $0 } (awk)
4537 Ah S 0:00 sort
4579 Ah R 0:00 ps
$
```

您可以看到，对于该管道，实际上有四个唯一的进程正在运行：三个 awk 进程和一个 sort 进程。此外，vi 和 ps 也被列为正在运行。请注意，我的登录 shell（bash）不在此列表中。

![](img/036fe100817eada43c999b050270081b_291_0.png)

## FIGURE 15.1 ps 默认进程输出。

| Value | 含义 |
| --- | --- |
| R | 运行中 |
| S | 睡眠（20 秒或更少） |
| I | 空闲（睡眠超过 20 秒） |
| T | 已停止 |
| Z | 僵尸进程 |

## TABLE 15.2 可能的进程状态值

还存在其他进程状态，但对于大多数用户来说很少出现。僵尸进程是指已结束但未释放其资源的进程。通常，系统需要一两秒钟才能完全回收程序使用的所有内存。有时，僵尸会因某种原因卡在进程表中。Unix 人称之为卡住的进程，这种进程有一个令人讨厌的习惯，会一直存在直到系统重新启动。有时这些僵尸进程在进程列表中会列为 <defunct>。任何以 sleep 命令为前缀的进程都被标记为睡眠中。

4. 添加一些标志可以显著改变 ps 的输出：

```
$ ps -x
  PID TT STAT TIME COMMAND
 4352 Ah T 0:00 vi dickens.note
 6171 Ah R 0:02 awk - : {print $1""
 6172 Ah R 0:01 awk - , {print $1}
 6173 Ah S 0:01 -k { if (NF > 2) print $0 } (awk)
 6174 Ah S 0:00 sort
 6177 Ah R 0:00 ps -x
19189 Ah S 0:06 -bash (bash)
19649 Ah I 0:02 newmail
$
```

这里出现了两个新进程：-bash（shell），终于，我的登录 shell；以及 newmail，一个程序，它在后台自动启动时我

