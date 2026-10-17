
- 10. 在左窗口中，使用 `ps` 命令配合 `jT` 查看剩余作业。挂起的作业和后台作业处于睡眠状态 (S)。

```
$student@servera ~] ps jT

PPID PGID TTY STAT TIME

27277 27278 27278 27278 pts/1 Ss 0:00 -bash

27278 28234 28238 28234 pts/1 T 1000 0:00 /bin/bash /home/student/bin/control technical

27278 28251 28251 27278 pts/1 S 1000 0:00 /bin/bash /home/student/bin/control database

28234 28316 28234 28234 pts/1 T 1000 0:00 sleep 1

28251 28701 28251 27278 pts/1 S 1000 0:00 sleep 1

27278 28702 28702 27278 pts/1 R+ 1000 0:00 ps jT
```

- 11. 从两个终端中退出 `servera`。

```
[student@servera ~]$ exit

logout

Connection to servera closed.
```

```
[student@servera ~]$ exit

logout

Connection to servera closed.
```

## 完成

在工作站上，运行 `lab processes-control finish` 脚本以完成本次练习。

```
[student@workstation ~]$ lab processes-control finish
```

此引导性练习结束。

# 杀死进程

## 目标

在完成本节后，你应该能够：

- 使用命令杀死并与进程通信。
- 定义守护进程（daemon process）的特征。
- 结束用户会话和进程。

## 使用信号控制进程

信号是传递给进程的软件中断。信号向执行程序报告事件。产生信号的事件可以是错误、外部事件（如 I/O 请求或过期的定时器），或者是显式请求（使用发送信号的命令或键盘序列）。

下表列出了用于常规进程管理的基础信号。可以通过其短名称（HUP）或正式名称（SIGHUP）引用信号。

### 基础进程管理信号

| 信号数字 | 短名称 | 定义 | 目的 |
|---|---|---|---|
| 1 | HUP | 挂断 (Hangup) | 用于报告终端控制进程的终止。也用于在不终止的情况下重新初始化进程（重新加载配置）。 |
| 2 | INT | 键盘中断 | 导致程序终止。可以被阻塞或处理。通过按下组合键 `Ctrl-C` 发送。 |
| 3 | QUIT | 键盘退出 | 与 SIGINT 类似，但在终止时还会产生进程转储。通过按下组合键 `Ctrl+\` 发送。 |
| 9 | KILL | 杀死，不可阻塞 | 导致程序终止。无法被阻塞、忽略或处理；始终允许。 |
| 15 默认 | TERM | 终止 | 导致程序终止。与 SIGKILL 不同，它可以被阻塞、忽略或处理。请求进程终止的“礼貌”方式；允许自清理。 |
| 18 | CONT | 继续 | 发送给进程以恢复运行（如果进程已停止）。无法被阻塞。即使被处理，也始终恢复进程。 |

## 监控和管理 Linux 进程

| 信号数字 | 短名称 | 定义 | 目的 |
|---|---|---|---|
| 19 | STOP | 停止，不可阻塞 | 挂起进程。无法被阻塞或处理。 |
| 20 | TST | 键盘停止 | 与 SIGSTOP 不同，可以被阻塞、忽略或处理。通过发送 SUSP 组合键（Ctrl+Z）发送。 |

> 注意：信号数字在不同的 Linux 平台上有所不同，但信号名称和含义是标准化的。在使用命令时，建议使用信号名称而不是数字。本节讨论的数字针对 x86_64 系统。

每个信号都有一个默认操作，通常是以下之一：

- Term - 导致进程立即终止（退出）。
- Core - 导致进程保存内存映像（核心转储），然后终止。
- Stop - 导致进程停止执行（挂起）并等待继续（恢复）。

程序可以通过实现处理程序（handler routines）来忽略、替换或扩展信号的默认操作，从而对预期事件信号做出反应。

## 通过显式请求发送信号的命令

你可以通过按下键盘序列向挂起（Ctrl+Z）、杀死（Ctrl+C）或转储（Ctrl+\）当前前台进程发送信号。然而，你将使用发送信号的命令向后台进程或不同会话中的进程发送信号。

信号可以通过名称（例如 -HUP 或 -SIGHUP）或数字（相关的 -1）指定。用户可以杀死自己的进程，但杀死他人拥有的进程需要 root 权限。

`kill` 命令向 PID 数字发送信号。尽管命名为 `kill`，但它可以用于发送任何信号，而不仅仅是终止进程。你可以使用 `kill -1` 列出所有可用信号的名称和数字。

```
[user@host ~] kill -1

1) SIGHUP 2) SIGINT 3) SIGQUIT 4) SIGILL 5) SIGTRAP

6) SIGART 7) SIGBUS 8) SIGPIPE 9) SIGKILL 10) SIGUSR1

11) SIGSEGV 12) SIGUSR2 13) SIGPIPE 14) SIGALRM 15) SIGTERM

16) SIGVTRT 17) SIGCHILD 18) SIGCONT 19) SIGSTOP 20) SIGTSTP

... omitted.

[user@host ~] ps aux | grep
5194 0.0 0.1 222448 2980 pts/1 S 16:39 0:00 /bin/bash /home/user/bin/controljob1
5199 0.0 0.1 222448 3132 pts/1 S 16:39 0:00 /bin/bash /home/user/bin/controljob2
5205 0.0 0.1 222448 3124 pts/1 S 16:39 0:00 /bin/bash /home/user/bin/controljob3
5430 0.0 0.0 221860 1096 pts/1 S+ 16:41 0:00 grep --color=auto job
```

## 监控和管理 Linux 进程

```
[user@host-$] kill 5194

[user@host-$] ps aux | grep job
user      5199 0.0 0.1 222448 3132 pts/1 S 16:39 0:00 /bin/bash /home/user/bin/controljob2
user      5205 0.0 0.1 222448 3124 pts/1 S 16:39 0:00 /bin/bash /home/user/bin/controljob3
user      5783 0.0 0.0 221860 964 pts/1 S+ 16:43 0:00 grep --color=auto job
[1] Terminated

[user@host-$] kill 5199

[user@host-$] ps aux | grep job
user      5205 0.0 0.1 222448 3124 pts/1 S 16:39 0:00 /bin/bash /home/user/bin/controljob3
user      5938 0.0 0.1 221860 1048 pts/1 S+ 16:44 0:00 grep --color=auto job
[2]- Killed

[user@host-$] kill -TERM 5205
user      5996 0.0 0.1 222448 1048 pts/1 S+ 16:45 0:00 grep --color=auto job
[3]+ Terminated
```

`kill` 命令可以根据进程名称向多个进程发送信号。

```
[user@host-$] ps aux | grep job
5194 0.0 0.1 222448 2980 pts/1 S 16:39 0:00 /bin/bash /home/user/bin/controljob1
5199 0.0 0.1 222448 3132 pts/1 S 16:39 0:00 /bin/bash /home/user/bin/controljob2
5205 0.0 0.1 222448 3124 pts/1 S 16:39 0:00 /bin/bash /home/user/bin/controljob3
5438 0.0 0.0 221860 1096 pts/1 S+ 16:41 0:00 grep --color=auto job

[user@host-$] kill
[1] Terminated controljob1
```
