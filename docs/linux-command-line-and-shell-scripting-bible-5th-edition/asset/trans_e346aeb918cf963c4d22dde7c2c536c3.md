
## 第二部分：Shell 脚本基础

### Linux 信号

| 信号 | 值 | 描述 |
| :--- | :--- | :--- |
| 1 | SIGHUP | 挂断进程 |
| 2 | SIGINT | 中断进程 |
| 3 | SIGQUIT | 停止进程 |
| 9 | SIGKILL | 无条件终止进程 |
| 15 | SIGTERM | 尽可能终止进程 |
| 18 | SIGCONT | 继续一个被停止的进程 |
| 19 | SIGSTOP | 无条件停止（但不会终止）进程 |
| 20 | SIGTSTP | 停止或暂停进程，但不会终止它 |

默认情况下，Bash shell 会忽略它接收到的任何 SIGQUIT (3) 和 SIGTERM (15) 信号（因此交互式 shell 不会意外终止）。然而，Bash shell 不会忽略它接收到的任何 SIGHUP (1) 和 SIGINT (2) 信号。

如果 Bash shell 接收到 SIGHUP 信号，例如当你离开一个交互式 shell 时，它将退出。但在退出之前，它会向任何由该 shell 启动的进程传递 SIGHUP 信号，包括任何正在运行的 shell 脚本。

对于 SIGINT 信号，shell 仅被中断。Linux 内核停止向 shell 分配 CPU 处理时间。当这种情况发生时，shell 会将 SIGINT 信号传递给任何由该 shell 启动的进程，以通知它们当前的状况。

你很可能已经注意到，shell 会将这些信号传递给你的 shell 脚本程序进行处理。然而，shell 脚本的默认行为并不能控制这些信号，这可能会对脚本的运行产生不利影响。为了避免这种情况，你可以编程使脚本能够识别信号并执行命令，以应对信号带来的后果。

### 生成信号

Bash shell 允许你通过键盘上的按键组合生成两种基本的 Linux 信号。如果你需要停止或暂停一个失控的脚本，这个功能会非常有用。

### 中断进程

Ctrl+C 按键组合会产生 SIGINT 信号，并将其发送给当前在 shell 中运行的任何进程。你可以通过运行一条通常耗时较长的命令并按下 Ctrl+C 按键组合来测试这一点：

```bash
$ sleep 60
^C
$
```

`sleep` 命令会使 shell 的操作暂停指定的秒数，然后返回 shell 提示符。Ctrl+C 按键组合发送 `SIGINT` 信号，该信号仅停止当前在 shell 中运行的进程。如果在时间结束前（50 秒）按下 Ctrl+C 按键组合，你可以永久终止 `sleep` 命令。

### 暂停进程

除了终止进程，你还可以在进程执行操作的中途将其暂停。有时这可能很危险（例如，如果一个脚本对关键系统文件持有文件锁），但通常它允许你查看脚本正在做什么，而无需实际终止该进程。

Ctrl+Z 按键组合会产生 `SIGTSTP` 信号，停止在 shell 中运行的任何进程。停止进程与终止进程不同。停止进程会将程序保留在内存中，并且能够从中断处继续运行。在本章稍后的“控制作业”部分，你将学习如何重启被停止的进程。

当你使用 Ctrl+Z 按键组合时，shell 会通知你进程已被停止：

```bash
$ sleep 60
^Z
[1]+  Stopped            sleep 60
$
```

方括号中的数字是 shell 分配的*作业编号*。shell 将 shell 中运行的每个进程称为一个*作业*，并为当前 shell 中的每个作业分配一个唯一的编号。它为第一个启动的进程分配作业编号 1，第二个分配编号 2，等等。

如果你的 shell 会话中有被停止的作业，Bash 会在你第一次尝试退出 shell 时发出警告：

```bash
$ sleep 70
^Z
[2]+  Stopped            sleep 70
$
$ exit
logout
There are stopped jobs.
$
```

你可以使用 `ps` 命令查看被停止的作业：

```bash
$ ps -l
  F   UID     PID   PPID   %CPU      S      TTY    TIME    CMD
 0 S  1001   1509   1508   0.0  0 S  pts/0  00:00:00 bash
 0 T  1001   1532   1509   0.0  0 T  pts/0  00:00:00 sleep
 0 T  1001   1533   1509   0.0  0 T  pts/0  00:00:00 sleep
 0 R  1001   1534   1509   0.0  0 R  pts/0  00:00:00 ps
$
```

在 S 列（进程状态）中，`ps` 命令显示被停止的作业状态为 T。这表明该命令正在被跟踪或已被停止。

如果你确实想在仍有被停止作业（或多个作业）处于活动状态的情况下退出 shell，只需再次输入 `exit` 命令即可。shell 将退出并终止被停止的作业。

或者，既然你现在知道了被停止作业的 PID，你可以使用 `kill` 命令发送 `SIGKILL` (9) 信号来终止它：

```bash
$ kill -9 1532
[1]- Killed                 sleep 60
$ kill -9 1533
[2]+ Killed                 sleep 70
$
```

每次 shell 产生提示符时，它还会显示 shell 中任何状态发生变化的作业的状态。在你杀死一个作业后，shell 会显示一条消息，表明该作业在运行时被杀死，然后提供提示符。

> **注意**
> 在某些 Linux 系统上，当你杀死作业时，最初可能不会得到任何响应。然而，下次你执行产生 shell 提示符的操作（如按回车键）时，你会看到一条指示该作业已被杀死的消息。

### 捕获信号

除了让脚本对信号不进行管控，你还可以在信号出现时对其进行捕获并执行其他命令。`trap` 命令允许你指定 shell 脚本可以监视和拦截来自 shell 的哪些 Linux 信号。如果脚本接收到 `trap` 命令中列出的信号，它会阻止该信号被 shell 处理，而是将其在本地处理。

`trap` 命令的格式为

```bash
trap commands signals
```

在 `trap` 命令行中，你只需列出你希望 shell 执行的命令，以及以空格分隔的你希望捕获的信号列表。你可以使用信号的数值或 Linux 信号名称来指定信号。

下面是一个使用 `trap` 命令捕获 `SIGINT` 信号并控制信号发送时脚本行为的简单示例：

```bash
$ cat trapsignal.sh
#!/bin/bash
#Testing signal trapping
#
trap "echo ' Sorry! I have trapped Ctrl-C'" SIGINT
# echo This is a test script.
# count=1
while [ $count -le 5 ]
do
    echo "Loop #$count"
    sleep 1
    count=$(( $count + 1 ))
done
# echo "This is the end of test script."
exit
$
```

此示例中使用的 **trap** 命令每次检测到 SIGINT 信号时都会显示一条简单的文本消息。捕获该信号使得该脚本免受用户尝试使用 Bash shell 的 Ctrl+C 命令停止程序的影响：

```bash
$ ./trapsignal.sh
This is a test script.
Loop #1
Loop #2
^C Sorry! I have trapped Ctrl+C
Loop #3
^C Sorry! I have trapped Ctrl+C
Loop #4
Loop #5
This is the end of test script.
$
```

每次使用 Ctrl+C 按键组合时，脚本都会执行 **trap** 命令中指定的 **echo** 语句，而不是不处理该信号并允许 shell 停止脚本。

> **警告**
>
> 如果脚本中的某个命令被信号中断，使用带有指定命令的 **trap** 并不一定会允许被中断的命令从中断处继续执行。为了使脚本中的关键操作保持流畅，请使用空规格（null specification）和要捕获的信号列表一起使用 **trap**，例如：
>
> ```bash
> trap "" SIGINT
> ```
>
> 这样使用 **trap** 允许脚本完全忽略信号中断并继续其重要工作。

### 捕获脚本退出

除了在 shell 脚本中捕获信号，你还可以在 shell 脚本退出时捕获它们。这是一种在 shell 完成其工作时执行命令的便捷方式。

要捕获 shell 脚本的退出，只需将 `EXIT` 信号添加到 `trap` 命令中：

```bash
$ cat trapexit.sh
#!/bin/bash
#Testing exit trapping
#
trap "echo Goodbye..." EXIT
#
count=1
while [ $count -le 5 ]
do
    echo "Loop #$count"
    sleep 1
    count=$(( $count + 1 ))
done
#
exit
$
$ ./trapexit.sh
Loop #1
Loop #2
Loop #3
Loop #4
Loop #5
Goodbye...
$
```

当脚本到达正常退出点时，陷阱（trap）被触发，shell 执行你在 `trap` 命令行中指定的命令。即使你提前退出脚本，`EXIT` 陷阱也会生效：

```bash
$ ./trapexit.sh
Loop #1
Loop #2
Loop #3
^C Goodbye...
$
```

由于 `SIGINT` 信号不在 `trap` 命令列表中，当使用 Ctrl+C 按键组合发送该信号时，脚本将退出。然而，在脚本退出之前，由于 `EXIT` 被捕获，shell 会执行 `trap` 命令。

### 修改或删除陷阱

为了在 shell 脚本的不同部分以不同方式处理陷阱，你只需使用新的选项重新发出 `trap` 命令：

```bash
$ cat trapmod.sh
#!/bin/bash
#Modifying a set trap
#
```

