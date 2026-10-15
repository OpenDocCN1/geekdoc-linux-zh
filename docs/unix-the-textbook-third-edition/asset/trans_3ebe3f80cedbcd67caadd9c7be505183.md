

Solaris 版本的 ps 命令支持 PC-BSD 版本命令的以下选项：S、a、e、r、v、w 和 x。 但是，你在调用它们时不需要在前面加上连字符——例如 ps r。 同样，-o 选项在 Solaris 下也像在 PC-BSD 下一样工作，但并非与表 10.3 中列出的所有关键字或 PC-BSD 上 ps -L 命令显示的那些关键字一起工作。 它支持以下关键字，其中大多数与 PC-BSD 上的 ps 版本相同：user、ruser、group、rgroup、uid、ruid、gid、rgid、pid、ppid、pgid、sid、taskid、ctid、pri、opri、pcpu、pmem、vsz、rss、osz、nice、class、time、etime、stime、zone、zoneid、f、s、c、lwp、nlwp、psr、tty、addr、wchan、fname、comm、args、projid、project、pset 和 lgrp。

Solaris 上 ps 命令的输出显示四个字段，如下所示，其中 pts/1 是伪终端 1：

```
$ ps
  PID TTY      TIME CMD
 7243 pts/1    0:00 bash
 7247 pts/1    0:00 ps
$
```

以下会话中的示例运行展示了使用各种选项的 ps 命令。 请注意，ps -l 命令的输出包含已废弃的字段 F 和 ADDR，以及旧式（已废弃）的 PRI（在上一段显示的关键字列表中称为 opri），其中 PRI 值越低优先级越高。 你可以同时使用 -y 和 -l 选项来排除已废弃字段 F 和 ADDR 的列，包含 RSS 列，并以流行的方式显示 PRI 值。

```
$ ps -l
  F S   UID   PID   PPID  C PRI NI ADDR   SZ WCHAN    TTY TIME CMD
  0 O 1007  9784  9624  0  40 20    ? 2333       pts/2 0:00 ps
  0 S 1007  9624  9621  0  50 20    ? 2546       ? pts/2 0:00 bash
$ ps -ly
  S   UID   PID   PPID  C PRI NI  RSS SZ WCHAN    TTY TIME CMD
  S 1007 14081 14080 0  50 20 2284 10188 ? pts/5 0:00 bash
  O 1007 14116 14081 0  40 20 1472  9332       pts/5 0:00 ps
$ pagesize
4096
$
```

第一列 S 显示进程的状态。 Solaris 中的进程状态在表 10.4 中简要描述，同时还列出了一些与 PC-BSD 上 ps 命令显示的字段不同的字段。 请注意 ps 命令处于运行状态，而 bash 正在等待事件；本例中的事件是其子进程（即前台运行的 ps 命令）的终止。 NI 显示进程的 nice 值；值越高，进程的优先级越低。 你可以使用 -c 选项显示进程的优先级。 SZ 字段显示进程在虚拟内存中的大小（以页为单位）。 你可以通过运行 pagesize 命令来显示系统上的页面大小。 如前所示，我们系统上的页面大小为 4096（即 4k）字节。 我们已在本节前面讨论了 ps -ly 命令输出中的其余字段。

## 表 10.4 Solaris 上 ps 命令输出中某些字段的简要说明

| Field | Meaning |
|-------|---------|
| CLS | Scheduling class:
  FSS Fair share scheduling
  FX Fixed
  IA Interactive
  RT Real-time
  SYS System
  SDC System duty cycle
  TS Time-sharing |
| LTIME | Execution time for a reported LWP |
| NI | Nice value: The nice value of a process; another parameter used in the computation of a process's priority value |
| S | Process state:
  O Currently running on a CPU (or a core)
  R Ready to run but not scheduled yet
  S Sleeping for an event to complete
  T Stopped: background, suspended, or being traced
  W Waiting for the CPU usage to drop below the upper water mark
  Z Zombie process (finished/terminated but is still using some kernel resources) |
| STIME | Process start time |
| SZ | Size of the process in virtual memory in pages. You can use the pagesize command to determine the page size on your system. |
| TTY | Terminal: Shows the name of the terminal a process is attached to |

你可以通过运行以下命令来欣赏旧式和新式优先级显示之间的差异。 PRI 的第一列为新式，第二列为已废弃的 PRI。 请注意在旧式和新式中为这两个进程显示的优先级值。

```
$ ps -c -o pid,pri,opri,args
PID PRI PRI COMMAND
20041 59 40 ps -c -o pid,pri,opri,args
20033 49 50 -bash
$
```

你可以使用 -t 选项显示与特定终端关联的进程，如以下会话所示。 ps -eLP 命令显示正在运行

