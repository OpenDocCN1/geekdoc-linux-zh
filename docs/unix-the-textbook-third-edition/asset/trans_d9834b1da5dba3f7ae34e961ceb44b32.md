

## 表 10.8 PC-BSD 下 top 的交互式按键简要说明

| 命令 | 含义 |
|---|---|
| H | 显示/切换线程统计信息在单独的行上 |
| P | 按 CPU 显示/切换 CPU 使用率统计信息 |
| S | 显示/切换系统进程 |
| ^L | 重绘屏幕 |
| h or ? | 显示交互式按键的摘要 |
| k | 终止其空格分隔的 PID 列表指定的进程 |
| n or # | 更改要显示的进程数 |
| o | 按 cpu、res、size、time 等排序显示 |
| r | 更改作为空格分隔 PID 指定的进程列表的 nice 值 |
| s | 更改周期性更新时间（以秒为单位） |
| t | 切换 top 进程的显示 |
| z | 切换空闲进程的显示 |

## SYNTAX

```
top [options]
```

Purpose: Display and periodically update information about processes currently running on the system

Output: The various attributes of processes currently running on the system, periodically updated

## 常用选项/功能：

- N Display status of N processes
- -H Display statistics for each thread of a multithreaded process, one line per thread
- -I Do not display idle processes
- -P Display CPU usage statistics on a per-CPU basis
- -S Display/toggle system processes
- -U username Display statistics for only those processes belonging to username
- -a Display full command line for each process
- -o field Sort display by field, a header of a column in output in lowercase—for example, cpu, pri, res, or time
- -s Update screen every time seconds; default is 5
- -t Do not display the top process
- -z Do not display idle system processes

The options -a, -H, -I, -P, -S, -t, and -z are really toggles.

The top command on Solaris supports all of the features that its PC-BSD counterpart supports. In most cases, even the options and interactive keystrokes are the same. In a few cases, the interactive command strokes and option letters are different. The following syntax box and Table 10.9 give a brief description of the interactive keystrokes of the top command on Solaris.

## 表 10.9 Solaris 下 top 的交互式按键简要说明

| 命令 | 含义 |
|---|---|
| H or t | 切换线程在单独行上显示。 |
| M | 按内存使用情况排序显示（相当于执行了 top -o size 命令） |
| N | 按 PID 排序显示（相当于执行了 top -o pid 命令） |
| P | 按 CPU 使用率排序显示（相当于执行了 top -o cpu 命令） |
| T | 按 CPU 时间排序显示（相当于执行了 top -o time 命令） |
| h or ? | 显示交互式按键的摘要 |
| k | 终止其空格分隔的 PID 列表指定的进程 |
| n or # | 更改要显示的进程数 |
| r | 更改作为空格分隔 PID 指定的进程列表的 nice 值 |
| s | 更改周期性更新时间（以秒为单位） |

## SYNTAX

```
top [options]
```

## 常用选项/功能：

The N, -I, -S, -U, -o, and -s options are common between the PC-BSD and Solaris versions of top.

- -a Display statistics for all processes to the extent possible
- -c Display full command line for each process
- -t Display statistics for each thread of a multithreaded process, one line per thread

We show some example sessions of the top command primarily under PC-BSD because most of the options and interactive keystrokes under the two systems are common. Almost all of the uncommon options and interactive keystrokes use different letters, but provide the same features. The following is a run of the command without any options. The command output shows that the system has been up and running for almost 33 days without crashing. The last PID assigned is 75597. Further, 106 processes are currently in the system, with one running, 104 sleeping, and one in the zombie state. At the top-right corner is the current time that is updated when top updates its output. The MySQL daemon (mysqld), owned by the user david, is the second-highest priority process after top. It has 41 threads, has a size of 207M bytes out of which 43.552M bytes is in the main memory, and has run

