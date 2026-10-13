
这正是我们想要的。因为这台服务器主要是 Web 服务器，我们现在已将所有 Web 请求（Apache 是 Web 服务器，其守护进程是 httpd）的优先级提高（nice 值更低），使其高于常规登录 shell 和其他进程。

在 Unix 系统上能够调整和微调任务的优先级是一种强大——而且危险——的能力。就像任何超能力一样，你必须明智且谨慎地使用它。例如，永远不要更改任何内核任务的优先级，并且要谨慎降低任何普通用户任务的优先级。

另一方面，能够进行微调也可能带来显著的好处。例如，在我的 Mac OS X 系统上，我发现使用 renice 将 iTunes 的优先级设置为 1，将 Virtual PC 设置为 -1，可以显著提高整体性能，而不会对音乐播放产生任何不利影响。

## 清除游离进程

本小时还要讨论的另一个主题是 kill。renice 命令可以降低你希望其消耗更少 CPU 和系统资源的任务的优先级，但如果想彻底杀掉进程怎么办？

这正是同名 kill 命令的作用。指定一个 PID，你就可以让它在一阵油腻的黑烟中消失。

## 任务 14.5：kill 命令

无论进程是否卡住、失控、无法响应常规交互，还是来自无权运行它的其他用户，都有时候能够消除一个进程非常有价值。

- 1. 从上一节来看，仍有一些正在运行的作业应该被移除，正如 ps 所提醒的那样：

```
# ps -al
F S UID PID PPID C PRI NI ADDR SZ WCHAN TTY TIME CMD
000 S 0 14539 14369 0 70 1 . 589 wait4 pts/0 00:00:00 su
100 S 0 14540 14539 0 72 0 . 642 wait4 pts/0 00:00:00 bash
000 S 0 14566 14540 0 69 -1 . 414 nanosl pts/0 00:00:00 tail
100 T 0 14575 14540 0 68 0 . 505 do_sig pts/0 00:00:00 vi
100 R 0 14701 14540 0 75 0 . 773 . pts/0 00:00:00 ps
```

首先我们先杀掉 tail，因为我们不再需要它了——我们决定改为每天早上查看一次 syslog 文件本身的内容：

```
# kill 14566
#
```

kill 命令永远没有任何输出，因此传统上系统管理员会再次运行该命令：如果它再次没有任何报告，意味着应用程序正在阻塞或忽略信号，但如果它报告 No such pid，则说明第一次 kill 已完成任务：

```
# kill 14566
bash: kill: (14566) - No such pid
[1]- Terminated nice tail -f /var/log/messages
```

在这种情况下，第一次 kill 终止了 tail，而 shell 只是礼貌地等到另一个作业结束才报告作业已终止。

2. 你之前是否注意到 vi 作业的状态是 T，而不是 S 或 R？这意味着它已停止——要么因 I/O 被阻塞，要么由用户使用 ^Z 控制序列停止。无论它处于停止、睡眠还是运行状态，向进程发送信号都会使其唤醒足够长的时间来处理信号，要么忽略它，要么接受它并执行特定操作。

也可以向作业发送大量信号：kill -l 列出了所有可能性：

```
# kill -l
1) SIGHUP 2) SIGINT 3) SIGQUIT 4) SIGILL
5) SIGTRAP 6) SIGABRT 7) SIGBUS 8) SIGFPE
9) SIGKILL 10) SIGUSR1 11) SIGSEGV 12) SIGUSR2
13) SIGPIPE 14) SIGALRM 15) SIGTERM 17) SIGCHLD
18) SIGCONT 19) SIGSTOP 20) SIGTSTP 21) SIGTTIN
22) SIGTTOU 23) SIGURG 24) SIGXCPU 25) SIGXFSZ
26) SIGVTALRM 27) SIGPROF 28) SIGWINCH 29) SIGIO
30) SIGPWR 31) SIGSYS 32) SIGRTMIN 33) SIGRTMIN+1
34) SIGRTMIN+2 35) SIGRTMIN+3 36) SIGRTMIN+4 37) SIGRTMIN+5
38) SIGRTMIN+6 39) SIGRTMIN+7 40) SIGRTMIN+8 41) SIGRTMIN+9
42) SIGRTMIN+10 43) SIGRTMIN+11 44) SIGRTMIN+12 45) SIGRTMIN+13
46) SIGRTMIN+14 47) SIGRTMIN+15 48) SIGRTMAX-15 49) SIGRTMAX-14
50) SIGRTMAX-13 51) SIGRTMAX-12 52) SIGRTMAX-11 53) SIGRTMAX-10
54) SIGRTMAX-9 55) SIGRTMAX-8 56) SIGRTMAX-7 57) SIGRTMAX-6
58) SIGRTMAX-5 59) SIGRTMAX-4 60) SIGRTMAX-3 61) SIGRTMAX-2
62) SIGRTMAX-1 63) SIGRTMAX
```

其中几乎所有信号都可以安全地忽略，但有三个值得强调，因为它们最常被使用：如果未指定信号，则发送 SIGTERM（如之前对 tail 进程的 kill），SIGHUP 是“挂断”信号，通常是终止忽略 SIGTERM 的进程非常优雅的方式，而 SIGKILL 是信号世界中的“大杀器”——它是一种进程无法捕获或忽略的 kill 信号。如果你懒惰，也可以直接使用信号编号，如 kill -9 pid。

就像冷战可怕的日子一样，信号存在一种升级的感觉，基于进程对前一个信号的响应。可以这样想：如果手枪不起作用，就试试步枪。如果那也不起作用，就是战术核弹的时候了。好吧，也许这有点夸张，但你明白我的意思。

3. 要杀掉 vi 会话，我将指定 SIGTERM 并看看会发生什么：

```
# kill -TERM 14575
# kill -TERM 14575
#
```

啊……vi 忽略 SIGTERM 信号，所以我们必须尝试更强一点的东西：
SIGHUP。

```
# kill -HUP 14575
# kill -HUP 14575
#
```

正如你所见，一些应用程序相当顽强，能够接受并忽略许多常见信号。tail 命令在收到第一个 SIGTERM 时优雅地退出了，但 vi 仍在运行。这意味着是时候使用 SIGKILL（又名 -9）了：

```
# kill -9 14575
# kill -9 14575
bash: kill: (14575) - No such pid
[2]+ Killed nice -5 vi testme
```

这招奏效了。请注意，你可以通过名称（例如 -KILL）或其编号指定信号。许多系统管理员使用一段时间后，kill -9 已经刻在手指上了，甚至不去想信号名称。

4. 如果你发现自己处于需要暂时停止作业然后稍后恢复的情况，值得知道你可以向进程发送相当于 ^Z 的信号，然后发送恢复信号使其重新启动并开始运行：

```
# ps -lU taylor
F S UID PID PPID C PRI NI ADDR SZ WCHAN TTY TIME CMD
100 S 502 14369 14368 0 70 1 . 618 wait4 pts/0 00:00:00 bash
000 S 0 14539 14369 0 70 1 . 589 wait4 pts/0 00:00:00 su
100 S 502 14717 14716 0 71 0 . 618 read_c pts/1 00:00:00 bash
000 R 502 14757 14717 27 78 0 . 445 do_sig pts/1 00:00:00 find
```

你可以看到用户 taylor 有一个 find 正在运行，目前占用了 27% 的 CPU。暂时停止这个 find，运行几个系统管理员命令，然后再启动它会很有帮助：

```
# kill -STOP 14757
# ps -lU taylor
F S UID PID PPID C PRI NI ADDR SZ WCHAN TTY TIME CMD
100 S 502 14369 14368 0 70 1 . 618 wait4 pts/0 00:00:00 bash
000 S 0 14539 14369 0 70 1 . 589 wait4 pts/0 00:00:00 su
100 S 502 14717 14716 0 71 0 . 618 read_c pts/1 00:00:00 bash
000 T 502 14757 14717 0 78 0 . 445 do_sig pts/1 00:00:00 find
```

现在作业已停止，我们可以做其他事情一段时间

```
# kill -CONT 14757
# ps -lU taylor
```

```
F S UID PID PPID C PRI NI ADDR SZ WCHAN TTY TIME CMD
100 S 502 14369 14368 0 70 1 - 618 wait4 pts/0 00:00:00 bash
000 S 0 14539 14369 0 70 1 - 589 wait4 pts/0 00:00:00 su
100 S 502 14717 14716 0 71 0 - 618 read_c pts/1 00:00:00 bash
000 R 502 14757 14717 0 78 0 - 445 do_sig pts/1 00:00:00 find
```

一些系统守护进程在接收到特定信号时也会重新读取其配置文件并重新启动自己。如果是这种情况，通常像 kill -1 pid 这样的方法就能轻松解决问题，但在对系统造成太多破坏之前，请务必对照文档仔细检查。

作为系统管理员，在一个典型的工作周中，你可能不需要杀掉超过一两个进程，但非常重要的一点是，作为系统管理员，你拥有影响系统上运行作业的工具和能力。无论是通过 renice 更改其优先级，还是通过 kill 发送 -STOP 或 -HUP 等特定信号，你都在掌控之中。

权力越大，责任越大。如果你随意更改优先级或杀掉进程，你的用户社区会像夏日野餐时的黄蜂一样愤怒！

## 摘要

本小时揭开了引擎盖，深入探讨了 Unix 进程管理的神秘世界，首先学习如何使用 ps 命令了解正在运行的进程，然后讨论任务优先级，最后考虑终止不应该运行的进程的不同方法。在此过程中，我们还探讨了如何解决一个常见的系统管理难题：识别正在运行的每个任务以确定它们是否需要。

## 问答

Q init 程序是否总是 PID 1？
A 我见过的每个 Unix 系统上都是如此。init 进程管理计算机启动的顺序，因此它是启动时启动的第一个应用程序。

Q 为什么 nice 值与你预期的相反，即较小的数字比较大的数字更重要？
A 这是个非常好的问题！

Q 如果有 nice 命令，是否也有 naughty 命令呢？
A 我想我们必须查阅 SCUR1（当然是圣诞老人 Unix，版本 1！）Linux 手册页来确认这一点。或者，答案可能取决于你对命令 shell 的使用方式。
