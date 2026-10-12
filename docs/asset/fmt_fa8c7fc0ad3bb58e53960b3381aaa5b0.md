
```
4:46pm up 4 days, 9:15, 4 users, load average: 0.15, 0.06, 0.01
49 processes: 47 sleeping, 2 running, 0 zombie, 0 stopped
CPU states: 4.3% user, 2.3% system, 0.0% nice, 93.4% idle
Mem: 127764k av, 120352k used, 7412k free, 49432k shrd, 29732k buff
Swap: 120484k av, 0k used, 120484k free          99488k cached

PID USER PR NI SIZE RSS SHARE STAY IN CPU WCHAN TIME COMMAND
7941 kmem 20 0 4470 4396 4396 S 0 4.5 10.5 0:10.9
8015 root 6 0 728 728 564 S 0 1.1 1.5 0:00 top
7965 root 2 0 4183 4183 3264 S 0 0.7 5.2 0:00 kswapd
8601 root 1 0 3628 3628 2456 S 0 0.1 2.8 0:00 krotdae
1 root 0 0 404 404 358 S 0 0.0 0.0 0:03 init
2 root 0 0 0 0 S 0 0.0 0.0 0:00 kflushd
3 root -12 -12 0 0 S 0 0.0 0.0 0:02 kswapd
4 root 0 0 0 0 S 0 0.0 0.0 0:00 md_thread
5 root 0 0 0 0 S 0 0.0 0.0 0:00 wd_thread
935 root 0 0 896 896 554 S 0 0.0 0.7 0:00 bu
348 kdesktop 0 0 864 864 656 S 0 0.0 0.8 0:00 kpam
963 root 0 0 344 344 298 S 0 0.0 0.2 0:00 xps
83 root 0 0 384 384 312 S 0 0.0 0.2 0:00 xfsd
212 bin 0 0 320 320 255 S 0 0.0 0.2 0:00 kportap
223 root 0 0 428 428 382 S 0 0.0 0.3 0:00 syslogd
232 root 0 0 564 564 524 S 0 0.0 0.4 0:00 klogd
243 gdmroot 0 0 404 404 329 S 0 0.0 0.3 0:00 xdm
254 root 0 0 480 480 396 S 0 0.0 0.3 0:00 xpress
285 root 0 0 480 480 382 S 0 0.0 0.3 0:00 ifwatch
295 root 0 0 403 403 329 S 0 0.0 0.3 0:00 lpfd
323 root 0 0 576 576 548 S 0 0.0 0.6 0:00 xsvrswadn
347 root 0 0 276 276 248 S 0 0.0 0.7 0:00 xsngettty
331 root 0 0 728 728 532 S 0 0.0 0.5 0:00 xdbd
330 root 0 0 736 736 564 S 0 0.0 0.5 0:03 xmod
```

图 5.1

使用 `top` 检查正在运行的进程。

```
SECURE COMMAND REFERENCE
secure node off; cumulative node off; noclean node off

Interactive commands are:
space Update display
h/? Help. Re-draw the screen
q Quit and remove fields
oo Change order of displayed fields
h or ? Print this list
s Toggle cumulative mode
i Toggle display of idle processes
c Toggle display of command name/line
a Toggle display of pid ownerage
m Toggle display of memory information
t Toggle display of summary information
k kill a task (with any signal)
r Renice a task
S Sort by CPU usage
W Sort by resident memory usage
t Sort by time / cumulative time
H Show only a specific user
n or $ Set the number of processes to show
d Set the delay in seconds between updates
A Write configuration file "toprc"
q Quit

Press any key to continue
```

图 5.2

`top` 的帮助屏幕显示了用于更改显示的交互式命令。

### 关键概念

`ps` 命令用于列出系统中的当前进程。要获取更详细的信息，请使用 `-1` 选项。`-ef` 选项将以树状结构格式输出 `ps`，显示父进程和子进程之间的关系。

`top` 实用程序动态显示进程，而 `ps` 显示的是静态视图。`top` 可用于停止进程或重新确定它们的优先级。

### `nice`

`nice` 命令可用于降低正在运行的进程的优先级。超级用户也可以使用 `nice` 来提高进程的优先级。其语法为

```
nice [option] command-line
```

`command-line` 参数指的是您想要执行的命令。该命令可以是单个命令，也可以是包含参数和重定向的复杂命令。

如果没有提供选项，`nice` 使用 `10` 作为调整值。要使用不同的值，请使用 `-n value` 选项。可接受值的范围是 `-20`（最高优先级）到 `19`（最低优先级）。正值降低优先级，而负值提高优先级。

只有超级用户可以使用负值。以提高的优先级运行进程可能对系统以及其他任何进程（包括操作系统本身）产生重大影响。

### 后台和前台进程

当您发出命令时，外壳创建一个子进程，父进程（外壳）进入睡眠状态，直到该进程完成。例外情况是使用内置命令，它们不会创建子进程。

默认情况下，每次您发出命令时，它都在前台运行。您可以使用 `&` 使其在后台运行。例如，

```
pine &
```

将使一个进程（`pine`）在后台运行。

在 `Bash` 外壳中，`Ctrl+Z` 将挂起正在运行的程序并将其放入后台。使用 `fg` 将该程序调回前台，必要时您可以使用 `Ctrl+C` 来终止该进程。

## 作业

作业是由一个或多个命令组成的序列。每当你向 Linux 输入一条命令，即使该命令由通过一个或多个管道连接的多个命令组成，你都在创建一个新的作业。Shell 提供了控制作业的能力，并为每个作业分配一个编号。

作业控制指的是挂起进程并在稍后恢复其执行的能力。此功能由 Shell 控制——`bash` 支持作业控制。

你只能在前台运行一个作业，但可以在后台运行多个作业。要获取正在后台运行的命令列表以及已停止和挂起的程序，请使用 `jobs` 命令。

如果一个作业已被挂起，可以使用 `fg %`、`fg %n` 或 `fg %name` 将其带到前台。如果有多个作业被挂起或在后台运行，则可以使用 `fg %n`（其中 `n` 是作业编号）或 `fg %name`（其中 `name` 是进程名称）将其带到前台。

例如，如果 `vi` 的编辑会话已被挂起，`fg %vi` 会将其带回前台。

Shell 会维护一个当前运行作业的列表。当 `bash` 异步（在后台）启动一个作业时，它会打印一行看起来像这样的内容：

```
[2] 4356
```

这表明这是 `2` 号作业，且管道中最后一个进程的 `PID` 是 `4356`。管道是一行可以包含一个或多个管道的命令行，例如：

```
cat MyFile | sort | lpt
```

单个管道中的所有进程都是同一作业的成员。

程序被挂起后，可以使用 `bg` 命令在后台重新启动它。如果只有一个进程被挂起，那么 `bg`、`bg %name` 或 `bg %n` 将在后台重新启动该进程。如果有多个进程被挂起，则需要使用 `bg %n` 或 `bg %name` 才能在后台重新启动进程。

如果你尝试在作业停止时退出 `bash`，Shell 会警告你有已停止的作业。然后你可以使用 `jobs` 命令查看哪些作业已停止。但是，如果你再次尝试退出而不输入新命令，`bash` 允许你无警告地退出，已停止的作业将被终止。

`jobs` 命令的语法是：

```
jobs [options] [jobspec]
```
