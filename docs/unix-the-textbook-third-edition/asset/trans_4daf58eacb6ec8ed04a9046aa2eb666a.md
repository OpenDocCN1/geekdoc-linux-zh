

# 第 1 步：Shell 使用 fork 创建子进程

# 第 2 步：子进程使用 exec 用对应于 sort 命令的可执行文件覆盖自身。

# 第 3 步：sort 开始执行，而 "sh" 等待命令完成。当 sort 完成时，子进程终止，"sh" 重新开始执行，等待用户输入另一个要执行的命令。

![](img/02e070097d401d3bf7de4bf1c470b267_381_0.png)

图 10.3 UNIX shell 执行二进制程序 sort 的步骤。

# 第 1 步

# 第 2 步

# 第 3 步

![](img/02e070097d401d3bf7de4bf1c470b267_381_1.png)

图 10.4 UNIX shell 执行 shell 脚本的步骤。

它执行的命令。当子 shell 在脚本文件中执行命令时，父 shell 等待子进程终止。当子 shell 在脚本文件中遇到 eof 标记时，它会终止。子 shell 的唯一目的，就像任何其他 shell 一样，是执行命令，而 eof 表示“没有更多命令”。当子 shell 终止时，父 shell 退出等待状态并恢复执行。此事件序列如图 10.4 所示，该图还显示了脚本文件中 find 命令的执行。

除非在包含 shell 脚本的文件中另有指定，否则子 shell 的类型与父 shell 相同。也就是说，如果父 shell 是 Bourne shell，则子 shell 也是 Bourne shell。因此，默认情况下 shell 脚本由父 shell 的“副本”执行。然而，为任何 shell 编写的 shell 脚本（C、TC、Bourne、Bash、Korn 等）都可以执行，而不管当前 shell 的类型如何。为此，只需在包含 shell 脚本的文件的第一行中指定应执行脚本的子 shell 类型，格式为 #!full-path-name-of-the-shell。例如，以下行规定子 shell 为 C shell，因此此行之后的脚本在 C shell 下执行。

```
#!/bin/csh
```

此外，你可以通过将该 shell 作为当前 shell 的子进程运行、在其下执行命令并终止该 shell 来在另一个 shell 中执行命令。子 shell 也称为子 shell。请记住，运行各种 shell 的命令为 Bourne shell 的 sh、C shell 的 csh、TC shell 的 tcsh、Korn shell 的 ksh，以及 Bourne Again shell 的 bash。要启动新的 shell 进程，只需运行你想要运行的 shell 对应的命令即可。

在下面的会话中，当前 shell 是 C shell，Bourne shell 作为其子进程运行。echo 命令在 Bourne shell 下执行。然后启动 Bash shell，并在其下执行 echo 命令。ps 命令显示正在运行的三个 shell。最后，当连续按下 <Ctrl+D> 时，Bash 和 Bourne shell 都被终止，控制权返回到原始 shell，即 C shell。第一个 <Ctrl+D> 终止 Bash shell，将控制权交还给 Bourne shell。你也可以通过运行 exit 命令退出 shell。图 10.5 说明了涉及的所有步骤，显示了进程之间的父子关系。

![](img/02e070097d401d3bf7de4bf1c470b267_382_0.png)

图 10.5 在子 shell（也称为子 shell）下执行命令。

```
% ps
PID TT STAT TIME COMMAND
44387 5 Ss 0:00.97 -csh (csh)
45878 5 R+ 0:00.01 ps
% /bin/sh
$ echo "This is Bourne shell."
This is Bourne shell.
$ bash
[sarwar@pcbsd-srv ~]$ echo "This is Bourne Again SHell."
This is Bourne Again SHell.
[sarwar@pcbsd-srv ~]$ ps
PID TT STAT TIME COMMAND
44387 5 Is 0:00.97 -csh (csh)
45910 5 I 0:00.02 /bin/sh
45935 5 S 0:00.07 bash
46008 5 R+ 0:00.01 ps
[sarwar@pcbsd-srv ~]$ <Ctrl+D>
$ <Ctrl+D>
%
```

# 10.5 进程属性

每个 UNIX 进程都有多个属性，包括所有者 ID（在 UNIX 术语中称为用户 ID [UID]）、进程 ID（PID）、父进程的 PID（PPID）、进程名称、进程状态、启动进程所执行的命令、进程优先级、进程启动时间、进程消耗的 CPU 时间百分比、进程消耗的主内存百分比、进程在虚拟内存中的大小、进程当前在主内存中的大小、进程状态、进程正在等待的事件（如果它未运行），以及进程已运行的时间长度。从用户和程序员的角度来看，这些属性中最有用之一是 PID，它用作本章后面讨论的多个进程控制命令的参数。

UNIX 提供了多个工具，允许你监视当前在系统上运行的进程的属性、更改你的进程的状态，并在它们上执行各种操作，包括停止/重新启动它们、向它们发送特定消息、让它们相互通信以及终止它们。在本章中，我们将讨论一些命令和工具，这些命令和工具允许我们静态和动态地监视进程的属性，以及执行上面所述的对进程的各种操作。

# 10.5.1 进程属性的静态显示

ps 命令可用于查看系统中当前进程属性的快照。PC-BSD 和 Solaris 都有自己的带多个选项的该命令版本。然而，其中几个命令是通用的。首先，我们详细讨论 PC-BSD 版本的命令，然后讨论 Solaris 版本的附加功能。以下是 PC-BSD 版本 ps 命令的简要说明。

