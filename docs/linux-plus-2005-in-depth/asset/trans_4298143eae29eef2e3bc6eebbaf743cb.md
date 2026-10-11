
> **注意**
> 命令与 `&` 符号之间的空格字符是可选的；命令 `sample &` 等价于前面输出中使用的命令 `sample&`。

Shell 会返回 **PID**（在前面的示例中为 2583）以及后台作业 ID（在前面的示例中为 1），以便你可以在后台作业运行后对其进行管理。在进程启动后，你可以使用 `ps` 命令查看 **PID**，或使用 `jobs` 命令查看后台作业 ID，如下面的输出所示：

```
[root@server1 root]# jobs
[1]+  Running        sample &
[root@server1 root]# ps | grep sample
2583 tty2    00:00:00 sample
[root@server1 root]# _
```

要终止后台进程，你可以像本章前面所示的那样向 PID 发送 kill 信号，或者向后台作业 ID 发送。后台作业 ID 必须以 `%` 字符作为前缀。若要向前面创建的 sample 后台进程发送 SIGINT 信号，可以使用以下 `kill` 命令：

```
[root@server1 root]# jobs
[1]+  Running        sample &
[root@server1 root]# kill -2 %1
[root@server1 root]# jobs
[root@server1 root]# _
```

> **注意**
> 你还可以使用 `killall -2 sample` 命令或 `top` 实用工具来终止前面示例中使用的 sample 后台进程。

后台进程启动后，可以通过使用 **前台 (fg) 命令** 加上后台作业 ID 将其移至前台。同样，可以使用 Ctrl+z 键组合暂停前台进程，并使用 **后台 (bg) 命令** 将其发送到后台。Ctrl+z 键组合会为前台进程分配一个后台作业 ID，然后该 ID 用作 `bg` 命令的参数。要在后台启动 sample 进程并将其移至前台，然后暂停它并再次将其移至后台，你可以使用以下命令：

```
[root@server1 root]# sample &
[1] 7519
[root@server1 root]# fg %1
sample
[Ctrl]-z
[1]+  Stopped                 sample
[root@server1 root]# bg %1
[1] sample &
[root@server1 root]# jobs
[1]+  Running                  sample &
[root@server1 root]# _
```

当 Shell 中正在执行多个后台进程时，**jobs** 命令会用 + 符号指示最近的进程，用 – 符号指示次新的进程。如果在命令中使用 % 符号而未指定后台作业 ID，该命令将作用于最近的后台进程。此示例如下面的输出所示，其中启动了四个 sample 进程，并使用 % 符号发送 **SIGQUIT** kill 信号：

```
[root@server1 root]# sample &
[1] 7605

[root@server1 root]# sample2 &
[2] 7613

[root@server1 root]# sample3 &
[3] 7621

[root@server1 root]# sample4 &
[4] 7629

[root@server1 root]# jobs
[1]   Running                  sample &
[2]   Running                  sample2 &
[3]-  Running                  sample3 &
[4]+  Running                  sample4 &

[root@server1 root]# kill -3 %
/sbin/sample4: 7629 Quit
[4]+  Exit 131                 sample4

[root@server1 root]# jobs
[1]   Running                  sample &
[2]-  Running                  sample2 &
[3]+  Running                  sample3 &

[root@server1 root]# kill -3 %
/sbin/sample3: 7621 Quit
[3]+  Exit 131                 sample3

[root@server1 root]# jobs
[1]-  Running          sample &
[2]+  Running          sample2 &
[root@server1 root]# kill -3 %
/sbin/sample2: 7613 Quit
[2]+  Exit 131             sample2
[root@server1 root]# jobs
[1]+  Running          sample &
[root@server1 root]# kill -3 %
/sbin/sample: 7605 Quit
[1]+  Exit 131           sample
[root@server1 root]# jobs
[root@server1 root]#
```

## 进程优先级

回想一下，Linux 是一个多任务操作系统；它可以同时执行多个不同的任务。由于大多数计算机只包含一个 CPU，Linux 在处理器上串行执行每个进程的一小部分；这使得用户感觉进程是在同时执行。进程使用 CPU 的时间量被称为**时间片**；进程拥有的时间片越多，它在 CPU 上执行的时间就越长，执行速度也就越快。时间片通常以毫秒为单位衡量；因此，在单秒内可以有数百个进程在处理器上执行。

`ps -l` 命令列出进程的 Linux 内核优先级（**PRI**）；此值直接相关于进程在 CPU 上拥有的时间片数量。PRI 为 0 最有可能获得 CPU 时间片，而 PRI 为 127 则最不可能获得 CPU 时间片。此命令的示例如下：

```
[root@server1 root]# ps -l
  F S   UID   PID  PPID  C PRI  NI ADDR SZ WCHAN    TTY          TIME CMD
  4 S     0  3194  3192   0  75   0 -  1238 wait4    pts/1      00:00:00 bash
  4 S     0  3896  3194   0  76   0 -   953 -        pts/1      00:00:00 sleep
  4 S     0  3939  3194  13  75   0 -  7015 -        pts/1      00:00:01 gedit
  4 R     0  3940  3194   0  77   0 -   632 -        pts/1      00:00:00 ps
[root@server1 root]#
```

`bash`、`sleep`、`gedit` 和 `ps` 进程具有不同的 PRI 值，因为内核根据多个因素自动分配时间片。你无法直接更改 PRI，但可以通过为进程分配特定的 nice 值来间接影响它。负的 nice 值会增加进程获得更多时间片的可能性，而正的 nice 值则相反。nice 值的范围如图 10-4 所示。

### 进程优先级

![](img/09bf13b782f71165e17bb3839040c96a_410_0.png)

所有用户都可以通过提高其 nice 值来降低自身进程的优先级，从而对同一台计算机上的其他用户“友好”。然而，只有 root 用户有能力通过降低其 nice 值来提高进程的优先级。

进程默认以 0 的 nice 值启动，如之前 `ps -l` 输出的 NI 列所示。要以 +19（低优先级）的 nice 值启动进程，你可以使用 `nice` 命令，并使用 `-n` 选项指定 nice 值和要启动的命令。如果省略 `-n` 选项，则默认为 nice 值 +10。要以 +19 的 nice 值启动 `ps -l` 命令，可以发出以下命令：

```
[root@server1 root]# nice -n 19 ps -l
F S UID PID PPID C PRI NI ADDR SZ WCHAN TTY TIME CMD
4 S 0 3194 3192 0 75 0 - 1238 wait4 pts/1 00:00:00 bash
4 S 0 3896 3194 0 76 0 - 953 - pts/1 00:00:00 sleep
4 S 0 3939 3194 0 76 0 - 7015 - pts/1 00:00:02 gedit
4 R 0 3946 3194 0 99 19 - 703 - pts/1 00:00:00 ps
[root@server1 root]#
```

从前面的输出可以看出，ps 命令的 NI 为 19，而 bash、sleep 和 gedit 命令的 NI 为 0。此外，ps 命令的 PRI 为 99，导致其获得的时间片少于 sleep 和 gedit 命令的 PRI 76 以及 bash shell 的 PRI 75。

相反，若要提高 `ps -l` 命令的优先级，可以使用以下命令：

```
[root@server1 root]# nice -n -20 ps -l
F S UID PID PPID C PRI NI ADDR SZ WCHAN TTY TIME CMD
4 S 0 3194 3192 0 75 0 - 1238 wait4 pts/1 00:00:00 bash
4 S 0 3896 3194 0 76 0 - 953 - pts/1 00:00:00 sleep
4 S 0 3939 3194 0 76 0 - 7015 - pts/1 00:00:02 gedit
4 R 0 3947 3194 0 60 -20 - 687 - pts/1 00:00:02 ps
[root@server1 root]#
```

注意前面的输出中，ps 命令的 nice 值为 -20，导致其 PRI 为 60，这比 sleep 和 gedit 命令的 PRI 76 以及 bash shell 的 PRI 75 更有可能获得时间片。

> **注意**
> 在某些 Linux 系统中，后台进程默认会被赋予 4 的 nice 值，以降低其获得时间片的机会。

进程启动后，你可以使用 `renice` 命令更改其优先级，并指定 nice 值的变更以及要更改的进程的 PID。例如，假设当前终端上有三个 sample 进程正在执行：

```
[root@server1 root]# ps -l
F S  UID   PID  PPID C  PRI  NI ADDR SZ WCHAN TTY            TIME CMD
4 S    0   1229  1228  0   71   0  -  617 wait4 pts/0     00:00:00 bash
4 S    0   1990  1229  0   69   0  -  483 nanosl pts/0     00:00:00 /bin/sample
4 S    0   2180  1229  0   70   0  -  483 nanosl pts/0     00:00:00 /bin/sample
4 S    0   2181  1229  0   71   0  -  483 nanosl pts/0     00:00:00 /bin/sample
4 R    0   2196  1229  0   75   0  -  768 -           pts/0     00:00:00 ps
[root@server1 root]# 
```

要将前两个 sample 进程的优先级降低（将 nice 值从 0 更改为 +15）并查看新值，你可以执行以下命令：

```
[root@server1 root]# renice +15 1990 2180
1990: old priority 0, new priority 15
2180: old priority 0, new priority 15
[root@server1 root]# ps -l
F S  UID   PID  PPID C  PRI  NI ADDR SZ WCHAN TTY            TIME CMD
4 S    0   1229  1228  0   71   0  -  617 wait4 pts/0     00:00:00 bash
4 S    0   1990  1229  0   73  15  -  483 nanosl pts/0     00:00:00 /bin/sample
4 S    0   2180  1229  0   76  15  -  483 nanosl pts/0     00:00:00 /bin/sample
4 S    0   2181  1229  0   71   0  -  483 nanosl pts/0     00:00:00 /bin/sample
4 R    0   2196  1229  0   75   0  -  768 -           pts/0     00:00:00 ps
[root@server1 root]# 
```

> **注意**
> 你还可以使用 `top` 实用工具来更改正在运行的进程的 nice 值；只需按 `r` 键，并在提示时输入 PID 和 nice 值即可。

与 `nice` 命令一样，只有 root 用户才能使用 `renice` 命令将 nice 值更改为负值。

