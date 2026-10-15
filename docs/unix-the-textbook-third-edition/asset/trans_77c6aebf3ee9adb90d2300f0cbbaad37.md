

# 语法

```
(cmd1; cmd2; ...; cmdN)
```

目的：按顺序执行命令 cmd1、cmd2、...、cmdN，但作为一个进程

因此在下面的会话中，date 和 echo 命令按顺序执行，但作为一个进程。

```
% (date; echo Hello, World!)
Sat Sep 20 22:14:52 PKT 2014
Hello, World!
%
```

你可以通过用其他命令或命令组分隔命令组，将命令分组与顺序执行结合起来。在下面的会话中，date 和 echo 命令作为一个进程执行，然后 who 命令作为单独的进程执行。

```
% (date; echo Hello, World!); who
Sun Sep 21 08:05:55 PKT 2014
Hello, World!
root          pts/0    Aug 14 09:45 (:0)
sarwar        pts/1    Sep 21 08:05 (39.59.18.169)
malik         pts/2    Sep 20 10:59 (:0)
%
```

命令组可以嵌套。因此，((date;echo Hello, World!);who) 和 ((date;echo Hello, World!);(who; uname)) 都是有效命令并产生预期结果。当组作为单独的进程执行时，命令分组更有意义，如下面的会话所示。

```
% (date ; echo Hello, World!)&
[1] 40563
% Sun Sep 21 08:08:42 PKT 2014
Hello, World!
[1] Done
( date; echo Hello, World! )
```

```
malik                 pts/2        Sep 20 10:59  (:0)
sarwar
[1]  - Done                     ( date; echo Hello, World )
FreeBSD
% <Enter>
[2]     Done                    ( who; uname )
%
```

在第二个命令组中，(date; echo Hello, World) 和 (who; uname) 在后台执行，而 whoami 命令在前台执行；这三个命令并行执行。同样，输出的顺序取决于这些命令的调度。

在下面的章节练习中，你将练习 UNIX 命令的顺序和并行执行。

## 练习 10.5

在你的系统上运行本节中提供的会话，以练习 shell 命令的顺序和并行执行。

## 练习 10.6

以下哪些命令按顺序运行，哪些并行运行？有多少个进程并行运行？(who; date) & (cat temp; uname & whoami)

### 10.6.4 命令和进程的异常终止

当你运行一个命令时，它在成功完成任务后正常终止。一个命令（进程）可能因你传递给它的错误参数而过早终止，例如将目录参数作为 cp 命令的源文件，或因运行时错误而终止。有时，你可能还需要异常终止一个进程。异常终止的需求出现在你使用合法但错误的參數运行进程时（例如 find 命令的错误文件名），或当命令花费太长时间完成时，也许是由于无限循环。在这里，我们讨论与前台和后台进程相关的异常终止。

你可以通过按 <Ctrl+C> 或从另一个 shell 使用 kill 命令来终止前台进程。你可以通过以下两种方式之一终止后台进程：（1）使用 kill 命令，或（2）先通过使用 fg 命令将进程带到前台，然后按 <Ctrl+C>。kill 命令的主要目的是向进程发送信号（也称为软件中断）。UNIX 操作系统使用信号来引起进程的注意。你可以向你拥有或有权操作的进程发送 UNIX 系统支持的任何一种信号类型。进程在接收到信号后可以采取以下三种操作之一：

+   1. 接受 UNIX 内核确定的默认操作
+   2. 忽略信号
+   3. 拦截信号并采取用户定义的操作

对于大多数信号，默认操作除了其他一些事件外，总是导致进程终止。忽略信号对进程没有任何影响。用户定义的操作被指定为程序语句（通常是函数调用），它将控制权转移到进程中的特定代码段。在 shell 脚本中，你可以使用 Bourne shell 中的 trap 命令指定这些操作。C shell 通过 onintr 命令提供有限的信号处理。在 C 程序中，你可以使用库调用 signal 指定这些操作。我们将在第 13 章和第 15 章分别详细讨论 trap 和 onintr 命令。我们将在第 19 章详细描述 signal(2) 系统调用。快速查看时，可在 PC-BSD 或 Solaris 系统上使用 man signal 或 man 3 signal 命令查看其手册页。PC-BSD 上也可以使用 man -S3 signal 命令。

信号可以因各种原因而产生。这些原因中的一些由进程本身引起，而另一些则与进程外部有关。由进程内部事件引起的信号称为内部信号，或陷阱（不要与 Bourne shell 中的 trap 命令混淆）。例如，进程中执行除零指令会产生陷阱。由进程外部事件或计算机系统中的硬件设备引起的信号称为外部信号。如果外部信号是针对 CPU 或磁盘控制器等硬件设备，则称为硬件中断或中断。旨在引起一个或多个进程注意的外部事件在 UNIX 术语中称为软件中断或信号。例如，当进程尝试执行不存在的指令或访问其不允许访问的内存区域（例如属于其他进程或 UNIX 内核的内存）时，会为该进程生成内部信号。你可以通过按 <Ctrl+C>、注销或使用 kill 命令生成外部信号。kill 命令可用于向进程发送任何类型的信号。以下是 kill 命令的简要说明。

# 语法

```
kill [-s signal_name] proc-list
kill [-signal_number] proc-list
kill [-signal_number] proc-list
kill -l [exit_status]
```

目的：语法 1-3：将 signal_number 或符号 signal_name 的信号发送到其 PID 或 jobID 在以空格分隔的 proc-list 中指定的进程；jobID 必须以 % 开头。

