

# 杀死进程

## 目标

在完成本节后，你应该能够：

- 使用命令杀死并与进程通信。
- 定义守护进程（daemon process）的特征。
- 结束用户会话和进程。

## 使用信号控制进程

信号是传递给进程的软件中断。信号向执行程序报告事件。产生信号的事件可以是错误、外部事件（如 I/O 请求或过期的定时器），或者是显式请求（使用发送信号的命令或键盘序列）。

下表列出了用于常规进程管理的基础信号。可以通过其短名称（HUP）或正式名称（SIGHUP）引用信号。

## 基础进程管理信号

| 信号数字 | 短名称 | 定义 | 目的 |
|---|---|---|---|
| 1 | HUP | 挂断 (Hangup) | 用于报告终端控制进程的终止。也用于在不终止的情况下重新初始化进程（重新加载配置）。 |
| 2 | INT | 键盘中断 | 导致程序终止。可以被阻塞或处理。通过按下组合键 **Ctrl-C** 发送。 |
| 3 | QUIT | 键盘退出 | 与 SIGINT 类似，但在终止时还会产生进程转储。通过按下组合键 **Ctrl+\** 发送。 |
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
[2]- Terminated controljob2
[3]+ Terminated controljob3
```

使用 `kill` 向一个或多个进程发送信号。`kill` 命令的选择标准包括：

- Command - 匹配模式的进程。
- UID - Linux 用户拥有的进程。
- GID - Linux 组拥有的进程。
- Parent - 特定父进程的进程。
- Terminal - 在特定终端运行的进程。

```
[user@host-$] ps aux | grep job
5992 0.0 0.1 222448 3040 pts/1 S 16:59 0:00 /bin/bash /home/user/bin/controljob1
5996 0.0 0.1 222448 3048 pts/1 S 16:59 0:00 /bin/bash /home/user/bin/controljob2
6884 0.0 0.1 222448 3048 pts/1 S 16:59 0:00 /bin/bash /home/user/bin/controljob3
```

## 监控和管理 Linux 进程

```
[user@host ~] kill kill1
[1] Terminated controlkill1
[2]- Terminated controljob2
[user@host ~] ps aux | grep kill
user      6219 0.0 0.1 221860 1052 pts/1 S+ 17:00 0:00 grep --color=auto kill1
[3]+ Terminated controljob3
[user@host ~] ps aux | grep test
user      6281 0.0 0.1 222448 3012 pts/1 S 17:04 0:00 /bin/bash /home/user/bin/controltest1
user      6285 0.0 0.1 222448 3128 pts/1 S 17:04 0:00 /bin/bash /home/user/bin/controltest2
user      6290 0.0 0.1 222448 3064 pts/1 S 17:04 0:00 /bin/bash /home/user/bin/controltest3
user      6318 0.0 0.1 221860 1080 pts/1 S+ 17:04 0:00 grep --color=auto test
[user@host ~] kill -u user
[user@host ~] ps aux | grep test
user      6870 0.0 0.1 221860 1048 pts/1 S 17:07 0:00 grep --color=auto test
[user@host ~]
```

## 管理性注销用户

你可能因为各种原因需要注销其他用户。列举几种可能的情况：用户违反了安全规定；用户可能耗尽了资源；系统可能无响应；或者他们访问了敏感材料。在这种情况下，你可能需要使用信号管理性地终止他们的会话。

要注销用户，首先识别要终止的会话。使用 `w` 命令列出登录用户和当前运行的进程。注意 TTY 和 FROM 列，以确定要关闭的会话。

所有用户登录会话都关联到一个终端设备（TTY）。如果设备名称格式为 **pts/N**，则它是与图形终端或远程登录会话相关的伪终端。如果格式为 **ttyN**，则用户位于系统控制台、备用控制台或直接连接的终端。

