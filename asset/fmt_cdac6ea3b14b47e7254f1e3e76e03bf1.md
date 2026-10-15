
```
$ (sleep 10; echo done) & 
$ ps -f ...请求面向用户的输出.
UID PID PPID C TIME TTY TIME CMD
glass 24379 23708 0 16:41 pts0 00:00:00 ksh
glass 24382 24379 0 16:41 pts0 00:00:00 sleep 10
glass 24803 24382 0 17:28 pts0 00:00:00 ps -f
$ done ...上一个命令的输出
```

# 5.18 · 作业控制

如果你感兴趣跟踪系统上其他用户的移动情况，请尝试 `ps` 的 `-e` 和 `-f` 选项：

| UID PID PPID C STIME TTY TIME CMD |

| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |

| root 1 0 Aug 25 ? | | | 00:00:02 init [5] |

| root 2 1 Aug 25 ? | | | 00:00:00 [koftirqd/d] |

| root 3 1 Aug 25 ? | | | 00:00:00 [events/0] |

| root 4 1 Aug 25 ? | | | 00:00:01 [kblockd/0] |

| root 5 1 Aug 25 ? | | | 00:00:00 [kapmd] |

| root 7 1 Aug 25 ? | | | 00:00:00 [pdfflush] |

| root 8 1 Aug 25 ? | | | 00:00:05 [kswapd -m O] |

| 742 1 Aug 25 ? | | | 00:00:00 syslog -m O |

| 750 1 Aug 25 ? | | | 00:00:00 /usr/sbin/atd |

| daemon 1003 948 Aug 25 ? | | | 00:00:00 - |

| root 1078 1 Aug 25 ? | | | 00:00:00 crond |

| glass 1362 1282 0 Aug 25 ? | | | 00:03:01 magic |

| glass 1376 1 Aug 25 ? | | | 00:00:00 /usr/lib/gconf |

| glass 1463 1282 0 Aug 25 ? | | | 00:00:00 wrapper |

| glass 23708 23693 0 15:51 pts0 | | | 00:00:00 bash |

| root 24379 23708 0 16:41 pts0 | | | 00:00:00 su |

| root 24382 23779 0 16:41 pts0 | | | 00:00:00 bash |

| 24805 24382 0 17:28 pts0 | | | 00:00:00 ps -ef |

`shell` 在你退出时会自动终止后台进程，而 `Bash` `shell` 则允许它们继续。如果你正在使用 `shell` 并希望让后台进程不受此影响，请使用 `nohup` 工具来保护它（图 5–17）。`nohup` 工具执行命令并使其对挂（HUP）和终止（TERM）信号免疫。标准输出和错误通道被重定向到名为 `"nohup.out"` 的文件中，进程的优先级增加。该工具非常适合确保会话退出时后台进程不终止。

图 5–17 `nohup` 命令的描述。

如果你使用 `nohup` 执行命令、退出并重新登录，你将在普通的 `ps` 输出中看不到该命令。这是因为进程在你退出时失去了控制终端，但继续执行。要在 `ps` 输出中包含没有控制终端的进程列表，请使用 `-x` 选项。这是一个这种效果的示例：

```
$ nohup sleep 10000 & ..nohup a background process.
27406
nohup: appending output to 'nohup.out'...message from 'nohup'.
$ ps
PID TT STAT TIME COMMAND
27399 pts/3 00:00:00 bash
27406 pts/3 00:00:00 sleep 10000
27407 pts/3 00:00:00 ps
$ ^D ..log back in.
login: glass
Password: ..secret.
$ ps ..the background process is not seen.
PID TT STAT TIME COMMAND
27409 pts/4 00:00:00 bash
27411 pts/4 00:00:00 ps
$ ps -x ..the background process may be seen.
PID TT STAT TIME COMMAND
...along lots of other output
27406 ? S 00:00 sleep
27409 pts/4 Ss 00:00 bash
27412 pts/4 R+ 00:00 ps -x
$
```

关于控制终端的更多信息，请参阅第 12 章“系统编程”。

## 5.18.1 向进程发送信号：kill

如果你想在进程完成之前终止它，请使用 `kill` 命令。大多数 `shell` 除了标准工具外还包含一个内置的 `kill` 命令。两个版本的 `kill` 支持图 5–18 所示的可移植性功能。

工具/Shell 命令：`kill [-signal] { pid }`

`kill` 将信号代码发送给编号进程列表。`signalId` 可以是的数字或名称。默认情况下，`kill` 发送 `TERM` 信号，这会导致接收进程终止。要获取信号列表，请使用 `-l` 选项。要向进程发送信号，你需要进入该进程或是超级用户。关于信号的更多信息，请参阅第 12 章“系统编程”。

进程可以保护自己免受除 `KILL` 信号（数字9）之外的所有信号。因此，为了确保杀死，请发送信号 9（注意发送 `KILL` 不允许进程清理并正常终止，许多程序在接收到 `TERM` 信号时会这样做）。

图 5–18 `kill` 命令的描述。

### 5.18 作业控制

在接下来的示例中，我创建了一个后台进程并杀死了它。为了确认终止，我获取了 `ps`：

```
$ (sleep 10; echo done) &&   ...create background process.
27390                   ...process ID 号.
$ kill 27390             ...kill the process.
$ ps                     ...it's gone!
PID TT STAT TIME COMMAND
27355 pts/3 00:00:00 bash
27394 pts/3 00:00:00 ps
$ 
```

接下来的示例说明了 `-l` 选项和命名信号的使用。信号按数字顺序列表，从 #1 开始：

```
$ kill -7               ...list the signal.
1) SIGHUP
2) SIGINT
3) SIGQUIT
4) SIGILL
5) SIGRTAP
6) SIGAB
7) SIGBUS
8) SIGFPE
9) SIGKILL
10) SIGUSR1
11) SIGSEGV
12) SIGUSR2
13) SIGPIPE
14) SIGARM
15) SIGTERM
17) SIGCHLD
18) SIGCONT
19) SIGSTOP
20) SIGTSTP
21) SIGTTIN
22) SIGTOU
23) SIGUR
24) SIGCPU
25) SIGFSZ
26) SIGVTAL
27) SIGPROF
28) SIGWINCH
29) SIGIO
30) SIGPWR
31) SIGUSR1
35) SIGRTMIN
36) SIGRTMIN+1
37) SIGRTMIN+2
38) SIGRTMIN+3
39) SIGRTMIN+4
40) SIGRTMIN+5
41) SIGRTMIN+6
42) SIGRTMIN+7
43) SIGRTMIN+8
44) SIGRTMIN+9
45) SIGRTMIN+10
46) SIGRTMIN+11
47) SIGRTMIN+12
48) SIGRTMIN+13
49) SIGRTMIN+14
50) SIGRTMAX-15
51) SIGRTMAX-13
52) SIGRTMAX-12
53) SIGRTMAX-11
54) SIGRTMAX-10
55) SIGRTMAX-9
56) SIGRTMAX-8
57) SIGRTMAX-7
58) SIGRTMAX-6
59) SIGRTMAX-5
60) SIGRTMAX-4
61) SIGRTMAX-3
62) SIGRTMAX-2
63) SIGRTMAX-1
64) SIGRTMAX
```

## 5.18.3 等待子进程：wait

`shell` 可以通过执行内置的 `wait` 命令等待一个或多个子进程终止（图 5–19）。
