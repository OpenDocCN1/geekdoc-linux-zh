

## 终止进程

如前所述，大量的流氓进程和僵尸进程会消耗系统资源。当系统性能因这些进程而受到影响时，你应该向它们发送**终止信号**，以终止进程。用于发送终止信号的最常见命令是**kill 命令**。总的来说，`kill` 命令可以向进程发送 64 种不同的终止信号。这些终止信号中的每一个都以不同的方式工作。要查看不同的终止信号名称及其关联的数字，你可以使用 `kill` 命令的 -l 选项，如下面的输出所示：

```
[root@server1 ~]# kill -l
1) SIGHUP	2) SIGINT	3) SIGQUIT	4) SIGILL
5) SIGTRAP	6) SIGABRT	7) SIGBUS	8) SIGFPE
9) SIGKILL	10) SIGUSR1	11) SIGSEGV	12) SIGUSR2
13) SIGPIPE	14) SIGALRM	15) SIGTERM	17) SIGCHLD
18) SIGCONT	19) SIGSTOP	20) SIGSTP	21) SIGTTIN
22) SIGTTOU	23) SIGURG	24) SIGXCPU	25) SIGXFSZ
26) SIGVTALRM	27) SIGPROF	28) SIGWINCH	29) SIGIO
30) SIGPWR	31) SIGPWR	33) SIGRTMIN	34) SIGRTMIN+1
35) SIGRTMIN+2	36) SIGRTMIN+3	37) SIGRTMIN+4	38) SIGRTMIN+5
39) SIGRTMIN+6	40) SIGRTMIN+7	41) SIGRTMIN+8	42) SIGRTMIN+9
43) SIGRTMIN+10	44) SIGRTMIN+11	45) SIGRTMIN+12	46) SIGRTMIN+13
47) SIGRTMIN+14	48) SIGRTMIN+15	49) SIGRTMAX-15	50) SIGRTMAX-14
51) SIGRTMAX-13	52) SIGRTMAX-12	53) SIGRTMAX-11	54) SIGRTMAX-10
55) SIGRTMAX-9	56) SIGRTMAX-8	57) SIGRTMAX-7	58) SIGRTMAX-6
59) SIGRTMAX-5	60) SIGRTMAX-4	61) SIGRTMAX-3	62) SIGRTMAX-2
63) SIGRTMAX-1	64) SIGRTMAX
[root@server1 ~]# _
```

前面输出中列出的大多数终止信号对于系统管理员来说并不实用。表 9-2 列出了管理中最常用的五个终止信号。

要向进程发送终止信号，你需要将要发送的终止信号作为 `kill` 命令的选项指定，后接该进程的相应 PID。例如，要向名为 `sample` 的进程发送 SIGQUIT，你可以使用以下命令来定位并终止该进程：

```
[root@server1 ~]# ps -ef | grep sample
root		1199	1	0	Jun30 tty3	00:00:00 /sbin/sample
[root@server1 ~]# kill -3 1199
[root@server1 ~]# _

[root@server1 ~]# ps -ef | grep sample
[root@server1 ~]# _
```

![](img/c27875544958897d817484d558c208c8_426_0.png)

`kill -SIGQUIT 1199` 命令的作用与前面输出中显示的 `kill -3 1199` 命令相同。

![](img/c27875544958897d817484d558c208c8_426_1.png)

如果你在使用 `kill` 命令时没有指定终止信号，`kill` 命令将使用默认的终止信号，即 SIGTERM 信号。

| 名称 | 编号 | 描述 |
| --- | --- | --- |
| SIGHUP | 1 | 也称为挂起信号，它会停止一个进程，然后以相同的 PID 重启它。如果你编辑了一个正在运行的守护程序使用的配置文件，该守护程序可能会收到一个 SIGHUP 以重启进程；当守护程序再次启动时，它会读取新的配置文件。 |
| SIGINT | 2 | 此信号向进程发送中断信号。虽然这是最弱的终止信号之一，但它大多数时候都能起作用。当你使用 Ctrl+c 键组合来终止当前运行的进程时，实际上就是向该进程发送了 SIGINT。 |
| SIGQUIT | 3 | 也称为核心转储，quit 信号通过获取内存中的进程信息并将其保存为当前工作目录中名为 core 的文件来终止进程。你可以使用 Ctrl+\ 键组合向当前运行的进程发送 SIGQUIT。 |
| SIGTERM | 15 | 软件终止信号是程序用于终止其他进程的最常见的终止信号。它是 kill 命令使用的默认终止信号。 |
| SIGKILL | 9 | 也称为绝对终止信号，它强制 Linux 内核通过将该进程的资源发送到名为 /dev/null 的特殊设备文件来停止执行该进程。 |

表 9-2 常见的管理用终止信号

某些进程具有忽略或捕获（trap）发送给它们的某些终止信号的能力。唯一无法被任何进程捕获的终止信号是 SIGKILL。因此，如果 SIGINT、SIGQUIT 和 SIGTERM 无法终止一个顽固的进程，你可以使用 SIGKILL 来终止它。然而，你应该仅将 SIGKILL 作为最后的手段使用，因为它会阻止进程正确地关闭临时文件和其他资源。

如果你向一个拥有子进程的进程发送终止信号，父进程会在自身终止之前终止其所有子进程。因此，要终止几个相关的进程，你只需向其父进程发送终止信号即可。此外，要终止一个僵尸进程，通常有必要向其父进程发送终止信号。

另一个可用于向进程发送终止信号的命令是 killall 命令。killall 命令的作用与 kill 命令类似，它都接受终止信号作为选项；然而，它使用进程名而不是 PID 来终止进程。这使得可以在一条命令中终止多个同名的进程。以下输出展示了使用 killall 命令向多个 sample 进程发送 SIGQUIT 的示例：

```
[root@server1 ~]# ps -ef | grep sample
root 1729 1 0 Jun30 tty3 00:00:00 /sbin/sample
root 20198 1 0 Jun30 tty4 00:00:00 /sbin/sample
[root@server1 ~]# killall -3 sample
[root@server1 ~]#
[root@server1 ~]# ps -ef | grep sample
[root@server1 ~]# _
```

![](img/c27875544958897d817484d558c208c8_427_0.png)

或者，你可以使用命令 killall -SIGQUIT sample 来执行与前面输出中使用的 killall -3 sample 命令相同的操作。

![](img/c27875544958897d817484d558c208c8_428_0.png)

与 `kill` 命令一样，如果你在使用 `killall` 命令时没有指定终止信号，它将默认发送 SIGTERM 信号。

除了 `kill` 和 `killall` 命令外，`top` 命令也可以用于终止进程。在 `top` 实用程序中，只需按 k 键，并在提示时提供相应的 PID 和终止信号。

## 进程执行

你可以执行三种主要类型的 Linux 命令：

- 二进制程序
- Shell 脚本
- Shell 函数

大多数命令，如 `ls`、`find` 和 `grep`，是存在于文件系统中的二进制程序，直到被执行。它们是用某种编程语言编写的，并被编译成只有计算机才能理解的二进制格式。其他命令，如 `cd` 和 `exit`，是内置于正在内存中运行的 BASH shell 中的，它们被称为 shell 函数。Shell 脚本还可以包含一系列二进制程序、shell 函数和特殊结构，供 shell 按顺序执行。

在执行编译后的程序或 shell 脚本时，解释你输入的命令的 BASH shell 会创建一个新的 BASH shell。这种新子 shell 的创建被称为*分支*（forking），由 BASH shell 中的 *fork* 函数执行。新的子 shell 然后使用其 `exec` 函数执行二进制程序或 shell 脚本。在二进制程序或 shell 脚本完成后，新的 BASH shell 使用其 `exit` 函数终止自身并将控制权返回给原始的 BASH shell。原始的 BASH shell 使用其 `wait` 函数等待新的 BASH shell 完成上述任务，然后才向用户返回提示符。图 9-3 描绘了当用户在命令行输入 `ls` 命令时的这一过程。

## 在后台运行进程

如前一节所述，BASH shell 创建（或分支）一个子 shell 来执行 Linux 系统中的大多数命令。不幸的是，原始的 BASH shell 必须等待子 shell 中的命令完成，然后才能显示 shell 提示符以接受新命令。以这种方式运行的命令被称为**前台进程**。

或者，你可以通过在命令末尾添加一个 & 符号来省略图 9-3 中显示的等待功能。以这种方式运行的命令被称为**后台进程**。当在后台运行命令时，shell 立即返回 shell

