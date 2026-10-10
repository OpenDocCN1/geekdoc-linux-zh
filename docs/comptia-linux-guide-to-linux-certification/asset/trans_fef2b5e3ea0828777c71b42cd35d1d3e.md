

![](img/c27875544958897d817484d558c208c8_429_0.png)

图 9-3 进程分叉

提示用户输入另一条命令。要在后台运行 `sample` 命令，您可以输入以下命令：

```
[root@server1 ~]# sample &
[1] 2583
[root@server1 ~]# _
```

![](img/c27875544958897d817484d558c208c8_429_1.png)

命令与和号（&）之间的空格字符是可选的。换句话说，命令 `sample&` 等同于上述输出中使用的命令 `sample &`。

Shell 会返回 PID（在前例中为 2583）和后台作业 ID（在前例中为 1），以便您可以在进程运行后操作该后台作业。进程启动后，您可以使用 `ps` 命令查看 PID，或使用 `jobs` 命令查看后台作业 ID，如下面的输出所示：

```
[root@server1 ~]# jobs
[1]+ Running    sample &
[root@server1 ~]# ps | grep sample
2583 tty2   00:00:00 sample
[root@server1 ~]# _
```

若要终止后台进程，您可以向 PID 发送 kill 信号（如本章前面所示），或者向后台作业 ID 发送 kill 信号。后台作业 ID 必须以 % 字符作为前缀。要向先前创建的 sample 后台进程发送 SIGINT 信号，您可以使用以下 kill 命令：

```
[root@server1 ~]# jobs
[1]+ Running sample &
[root@server1 ~]# kill -2 %1
[1]+ Interrupt sample
[root@server1 ~]# jobs
[root@server1 ~]# _
```

![](img/c27875544958897d817484d558c208c8_430_0.png)

后台进程启动后，您可以使用 foreground（fg）命令加上后台作业 ID 将其移至前台。同样，您可以使用 Ctrl+z 键组合暂停前台进程。然后，您可以使用 background（bg）命令将进程发送到后台。Ctrl+z 键组合会为前台进程分配一个后台作业 ID，随后该 ID 用作 bg 命令的参数。要在后台启动一个 sample 进程并将其移至前台，然后暂停它并再次移至后台，您可以使用以下命令：

```
[root@server1 ~]# sample &
[1] 7519
[root@server1 ~]# fg %1
sample
Ctrl+z
[1]+ Stopped sample
[root@server1 ~]# bg %1
[1] + sample &
[root@server1 ~]# jobs
[1]+ Running sample &
[root@server1 ~]# _
```

当 Shell 中有多个后台进程正在执行时，jobs 命令用 + 号表示最近的进程，用 - 号表示次近进程。如果在命令中使用 % 符号但不指定后台作业 ID，该命令将作用于最近的后台进程。下面的输出展示了一个示例，其中启动了四个 sample 进程，并使用 % 符号发送 SIGQUIT kill 信号：

```
[root@server1 ~]# sample &
[1] 7605
[root@server1 ~]# sample2 &
[2] 7613
[root@server1 ~]# sample3 &
[3] 7621
[root@server1 ~]# sample4 &
[4] 7629

[root@server1 ~]# jobs
[1]  Running     sample &
[2]  Running     sample2 &
[3]- Running      sample3 &
[4]+ Running     sample4 &

[root@server1 ~]# kill -3 %
[root@server1 ~]# jobs
[1]  Running     sample &
[2]- Running      sample2 &
[3]+ Running     sample3 &

[root@server1 ~]# kill -3 %
[root@server1 ~]# jobs
[1]- Running      sample &
[2]+ Running      sample2 &

[root@server1 ~]# kill -3 %
[root@server1 ~]# jobs
[1]+ Running      sample &

[root@server1 ~]# kill -3 %
[root@server1 ~]# jobs
[root@server1 ~]# _
```

## 进程优先级

回想一下，Linux 是一个多任务操作系统。这意味着它可以同时执行多个不同的任务。由于大多数计算机仅包含单个 CPU，Linux 以串行方式在处理器上执行每个进程的一小部分。这使用户感觉进程似乎在同时执行。进程使用 CPU 的时间量称为时间片；一个进程拥有的时间片越多，它在 CPU 上执行的时间就越长，执行速度也就越快。时间片通常以毫秒为单位进行测量。因此，在一秒钟内，处理器上可以有几百个进程在执行。

`ps -l` 命令列出 Linux 内核的进程优先级（PRI）。该值直接与进程在 CPU 上拥有的时间片数量相关。PRI 为 0 的进程最有可能在 CPU 上获得时间片，而 PRI 为 127 的进程最不可能在 CPU 上接收到时间片。该命令的一个示例如下所示：

```
[root@server1 ~]# ps -l
  FS   UID   PID  PPID  C  PRI   NI   ADDR SZ WCHAN  TTY      TIME     CMD
  4 S     0 3194  3192  0   75    0 -     1238 wait4  pts/1    00:00:00 bash
  4 S     0  3896  3194  0   76    0 -    -953 -     pts/1    00:00:00 sleep
  4 S     0  3939  3194 13   75    0 -    7015 -     pts/1    00:00:01 gedit
  4 R     0  3940  3194  0   77    0 -    632 -     pts/1    00:00:00 ps
[root@server1 ~]# _
```

*bash*、*sleep*、*gedit* 和 *ps* 进程具有不同的 PRI 值，因为内核根据多个因素自动分配时间片。您不能直接更改 PRI，但可以通过为进程分配特定的 nice 值来间接影响它。负 nice 值会增加进程获得更长时间片的可能性，而正 nice 值则相反。nice 值的范围如图 9–4 所示。

所有用户都可以通过提高自身进程的 nice 值来降低其优先级，从而对同一台计算机上的其他用户表现出“友善”（nice）。然而，只有 root 用户有能力通过降低进程的 nice 值来提高其优先级。

进程默认以 nice 值 0 启动，如之前 *ps -l* 输出中的 NI 列所示。要以 +19（低优先级）的 nice 值启动进程，您可以使用 *nice 命令*，并使用 -n 选项指定 nice 值以及要启动的命令。如果省略 -n 选项，则默认 nice 值为 +10。要以 +19 的 nice 值启动 *ps -l* 命令，您可以发出以下命令：

```
[root@server1 ~]# nice -n 19 ps -l
F S UID PID PPID C PRI NI ADDR SZ WCHAN TTY TIME CMD
4 S 0 3194 3192 0 75 0 – 1238 wait4 pts/1 00:00:00 bash
4 S 0 3896 3194 0 76 0 – 953 – pts/1 00:00:00 sleep
4 S 0 3939 3194 0 76 0 – 7015 – pts/1 00:00:02 gedit
4 R 0 3946 3194 0 99 19 – 703 – pts/1 00:00:00 ps
[root@server1 ~]# _
```

请注意，根据上述输出，*ps* 命令的 NI 值为 19，而 *bash*、*sleep* 和 *gedit* 命令的 NI 值为 0。此外，*ps* 命令的 PRI 为 99，导致其获得的时间片少于 *sleep* 和 *gedit* 命令（PRI 为 76）以及 *bash* Shell（PRI 为 75）。

相反，若要提高 *ps -l* 命令的优先级，您可以使用以下命令：

```
[root@server1 ~]# nice -n -20 ps -l
F S UID PID PPID C PRI NI ADDR SZ WCHAN TTY TIME CMD
4 S 0 3194 3192 0 75 0 – 1238 wait4 pts/1 00:00:00 bash
4 S 0 3896 3194 0 76 0 – 953 – pts/1 00:00:00 sleep
4 S 0 3939 3194 0 76 0 – 7015 – pts/1 00:00:02 gedit
4 R 0 3947 3194 0 60 -20 – 687 – pts/1 00:00:00 ps
[root@server1 ~]# _
```

![](img/c27875544958897d817484d558c208c8_432_0.png)

请注意，根据上述输出，`ps` 命令的 nice 值为 -20，导致其 PRI 为 60，这比 `sleep` 和 `gedit` 命令（PRI 为 76）以及 `bash` Shell（PRI 为 75）更有可能获得时间片。

![](img/c27875544958897d817484d558c208c8_433_0.png)

在某些 Linux 系统中，后台进程默认会被赋予 4 的 nice 值，以降低其获得时间片的可能性。

进程启动后，您可以使用 **renice** 命令更改其优先级，并指定 nice 值的变化以及要更改的进程的 PID。例如，假设当前有三个 sample 进程正在终端上执行：

```
[root@server1 ~]# ps -l
  F S   UID   PID  PPID  C  PRI  NI ADDR SZ WCHAN     TTY          TIME     CMD
  4 S     0  1229  1228  0   71   0    -  617 wait4     pts/0  00:00:00 bash
  4 S     0  1990  1229  0   69   0    -  483 nanosleep pts/0  00:00:00 sample
  4 S     0  2180  1229  0   70   0    -  483 nanosleep pts/0  00:00:00 sample
  4 S     0  2181  1229  0   71   0    -  483 nanosleep pts/0  00:00:00 sample
  4 R     0  2196  1229  0   75   0    -  768     -     pts/0  00:00:00 ps
[root@server1 ~]# _
```

若要通过将 nice 值从 0 更改为 +15 来降低前两个 sample 进程的优先级并查看新值，您可以执行以下命令：

```
[root@server1 ~]# renice +15 1990 2180
1990 (process ID) old priority 0, new priority 15
2180 (process ID) old priority 0, new priority 15
[root@server1 ~]# ps -l
  F S   UID   PID  PPID  C  PRI  NI ADDR SZ WCHAN     TTY          TIME     CMD
  4 S     0  1229  1228  0   71   0    -  617 wait4     pts/0  00:00:00 bash
  4 S     0  1990  1229  0   93  15    -  483 nanosleep pts/0  00:00:00 sample
  4 S     0  2180  1229  0   96  15    -  483 nanosleep pts/0  00:00:00 sample
  4 S     0  2181  1229  0   71   0    -  483 nanosleep pts/0  00:00:00 sample
  4 R     0  2196  1229  0   75   0    -  768     -     pts/0  00:00:00 ps
[root@server1 ~]# _
```

![](img/c27875544958897d817484d558c208c8_433_1.png)

您还可以使用 `top` 实用程序来更改运行中进程的 nice 值。只需按 `r` 键，然后在提示时提供 PID 和 nice 值即可。

![](img/c27875544958897d817484d558c208c8_433_2.png)

与 `nice` 命令一样，只有 root 用户才能使用 `renice` 命令将 nice 值更改为负值。

root 用户可以使用 `renice` 命令更改由特定用户或组拥有的所有进程的优先级。要将由用户 mary 和 bob 拥有的所有进程的 nice 值更改为 +15，您可以在命令提示符下执行命令 `renice +15 -u mary bob`

