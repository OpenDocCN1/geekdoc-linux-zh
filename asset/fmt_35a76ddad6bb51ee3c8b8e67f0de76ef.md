
```
[root@server1]# kill -1
1) SIGHUP 2) SIGINT 3) SIGQUIT 4) SIGILL 5) SIGTRAP 6) SIGABRT 7) SIGBUS 8) SIGFPE 9) SIGKILL 10) SIGUSR1 11) SIGSEGV 12) SIGCHLD 13) SIGPIPE 14) SIGALRM 15) SIGTERM 16) SIGHTLD 18) SIGCONT 19) SIGSTOP 20) SIGTSTP 21) SIGTTIN 22) SIGTOU 23) SIGURG 24) SIGXCPU 25) SIGFSZ 26) SIGTLARM 27) SIGPROF 28) SIGWINCH 29) SIGIO 30) SIGPWR 31) SIGSYS 33) SIGRTMIN 34) SIGRTMIN+1 35) SIGRTMIN+2 36) SIGRTMIN+3 37) SIGRTMIN+4 38) SIGRTMIN+5 39) SIGRTMIN+6 40) SIGRTMIN+7 41) SIGRTMIN+8 42) SIGRTMIN+9 43) SIGRTMIN+10 44) SIGRTMIN+11 45) SIGRTMIN+12 46) SIGRTIN+13 47) SIGRTIN+14 48) SIGRTIN+15 49) SIGRTMAX-15 50) SIGRTMAX-14 51) SIGRTMAX-13 52) SIGRTMAX-12 53) SIGRTMAX-11 54) SIGRTMAX-10 55) SIGRTMAX-9 56) SIGRTMAX-8 57) SIGRTMAX-7 58) SIGRTMAX-6 59) SIGRTMAX-5 60) SIGRTMAX-4 61) SIGRTMAX-3 62) SIGRTMAX-2 63) SIGRTMAX-1 64) SIGRTMAX
```

某些进程有能力捕获发送给它们的某些信号。这被称为信号捕获（trapping）。唯一无法捕获的杀死信号是 `SIGKILL`。

如果你向一个具有子进程的进程发送杀死信号，该父进程会在终止自身之前终止所有子进程。因此，要杀死相关进程，只需向其父进程发送信号。此外，要杀死僵尸进程，通常需要向其父进程发送信号。

另一个向进程发送杀死信号的命令是 `killall` 命令。`killall` 命令的工作原理与 `kill` 命令类似，它接受名称而不是 PID。这允许在一个命令中杀死同名的多个进程。使用 `killall` 向多个 `sample` 发送 `SIGQUIT` 的示例所示：

```
[root@server1]# ps -ef | grep sample
root 1729 1 0 Jun30 tty3 00:00:00 /sbin/sample
root 20198 0 Jun30 tty4 00:00:00 /sbin/sample
[root@server1]# killall -3 sample
[root@server1]# ps -ef | grep sample
[root@server1]# _
```

> 同样，你可以使用命令 `killall -SIGQUIT sample` 来达到之前输出中使用的 `killall -3` 命令的效果。
> 
> 在 `kill` 命令中，如果你在使用 `killall` 命令时未指定杀死信号，它假设为 `SIGTERM` 信号。

## 执行

你可以执行三种类型的 Linux 命令：

- 二进制程序
- Shell 脚本
- Shell 函数

# 第 10 章 管理 Linux 进程

大多数命令（如 `ls`、`find` 和 `grep`）是在执行前存在于文件系统中的二进制程序。它们用特定的编程语言编写，并编译成只有计算机才能理解的二进制格式。其他命令如 `cd` 和 `exit` 是内置在运行于内存中的 BASH shell 里的，被称为 shell 函数。Shell 脚本也可以包含一组二进制程序、shell 函数以及供 shell 按照顺序执行的特殊构造结构。

在执行编译后的程序或 shell 脚本时，解释器解释你输入的命令的 BASH shell 会创建一个新的 BASH shell。这个过程被称为“分叉（forking）”，由 BASH shell 中的 `fork` 函数执行。这个新的子 shell 使用其 `exec` 函数执行二进制程序或 shell 脚本。在二进制程序或 shell 脚本完成后，新的 BASH shell 使用其 `exit` 函数终止自身，并将控制权交还给原始 BASH shell。原始 BASH shell 使用其 `wait` 函数等待新的 BASH shell 完成上述任务后，再返回给用户。图 10-3 描述了用户在命令行输入 `ls` 命令时的这一过程。

![](img/9ee5f91f3446575a1e6ce62c54cae5d2_467_0.png)

图 10-3 进程分叉过程

## 在后台运行进程

如在前节中讨论的，BASH shell 会分叉出一个子 shell 来执行 Linux 系统上的大多数命令。遗憾的是，原始 BASH shell 必须等待子 shell 中的命令完成后，才能显示 shell 提示符以接受新命令；以这种方式运行的命令被称为前台进程。

或者，你可以通过在命令末尾添加和符号（`&`）来省略图 10-3 中的 `wait` 函数。以这种方式运行的命令被称为后台进程。当命令在后台运行时，shell 会立即返回提示符，允许用户输入另一个命令。若要在后台运行示例命令，你可以输入以下命令：

```
[root@server1] # sample &
[1] 2583
[root@server1] #
```

> 命令与和符号（`&`）之间的空格字符是可选的；命令 `sample &` 等同于前述输出中使用的命令 `sample&`。

![](img/9ee5f91f3446575a1e6ce62c54cae5d2_468_0.png)

shell 返回 PID（上例中的 2583）和后台作业 ID（上例中的 1），这样你就可以在运行后对其进行操作。进程启动后，你可以使用 `ps` 命令查看 PID，或使用 `jobs` 命令查看后台作业 ID，如下所示所示：

```
[root@server1] # jobs
[1]+ Running sample &
[root@server1] # ps | grep sample
2583 tty2 00:00:00 sample
[root@server1] #
```

要终止后台进程，你可以像本章前面所示，向 PID 发送 `kill` 信号，或者向后台作业 ID 发送。后台作业 ID 必须以 `%` 字符为缀。要向之前创建的后台进程发送 `SIGINT` 信号，你可以使用以下 `kill` 命令：

```
[root@server1] # jobs
[1]+ Running sample &
[root@server1] # kill -2 %1
[root@server1] # jobs
[root@server1] #
```

你也可以使用 `killall -2 sample` 命令或 `top` 实用程序终止上例中的 sample 后台进程。

![](img/9ee5f91f3446575a1e6ce62c54cae5d2_468_1.png)

后台进程启动后，可以使用 `foreground (fg)` 命令加上后台作业 ID 将其移动到前台。同样，可以使用 `Ctrl+z` 组合键暂停前台进程，并使用 `background (bg)` 命令将其发送到后台。`Ctrl+z` 组合键会分配一个进程作业 ID，该 ID 将被作为 `bg` 命令的参数。若要在后台启动示例进程并将其移动到前台，然后暂停并再次移动到后台，你可以使用以下命令：

```
[root@server1 root]# sample & 
[1] 7519
[root@server1 root]# fg %1
sample

[Ctrl]-z
[1]+ Stopped sample
[root@server1 root]# bg %1
[1]+ sample & 
[root@server1 root]# jobs
[1]+ Running sample &
[root@server1 root]# _
```

当 shell 中有多个后台进程在执行时，`jobs` 命令用 `+` 符号表示最近的一个，用 `-` 符号表示次近的。如果你在命令中使用 `%` 符号而未指定作业 ID，则该命令将对最近的后台进程进行操作。以下输出显示了一个示例，其中启动了四个进程并使用 `%` 符号发送了 `SIGQUIT` 信号：
