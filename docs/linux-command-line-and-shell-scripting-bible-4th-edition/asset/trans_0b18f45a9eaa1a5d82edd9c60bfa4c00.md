
准备脚本以应对信号带来的后果。

## 生成信号

Bash shell 允许你通过键盘上的按键组合来生成两种基本的 Linux 信号。如果你需要停止或暂停一个失控的脚本，这项功能会非常实用。

### 中断进程

Ctrl+C 按键组合会产生 SIGINT 信号，并将其发送给当前在 shell 中运行的任何进程。你可以通过运行一个通常需要较长时间才能完成的命令，然后按下 Ctrl+C 按键组合来测试这一点：

```
$ sleep 60
^C
$
```

sleep 命令会暂停 shell 的操作，持续指定的秒数，然后返回 shell 提示符。Ctrl+C 按键组合会发送 SIGINT 信号，该信号会直接停止当前在 shell 中运行的进程。通过在时间耗尽（60 秒）之前按下 Ctrl+C 按键组合，你永久终止了 sleep 命令。

### 暂停进程

你可以暂停正在执行某些操作中途的进程，而不仅仅是终止它。有时候，这可能是一件危险的事情（例如，如果一个脚本对一个关键系统文件持有文件锁），但它通常允许你窥视脚本正在执行的操作，而无需实际终止该进程。

Ctrl+Z 按键组合会产生 SIGTSTP 信号，停止在 shell 中运行的任何进程。停止进程与终止进程不同。停止进程会将程序保留在内存中，并使其能够从暂停的地方继续运行。在本章后面的“控制作业”部分，你将学习如何重启已被停止的进程。

当你使用 Ctrl+Z 按键组合时，shell 会通知你该进程已被停止：

```
$ sleep 60
^Z
[1] + Stopped sleep 60
$
```

方括号中的数字是 shell 分配的作业号。shell 将在 shell 中运行的每个进程称为一个作业，并为每个作业在当前 shell 中分配一个唯一的编号。它将第一个启动的进程分配为作业号 1，第二个为作业号 2，以此类推。

如果你的 shell 会话中有已停止的作业，Bash 会在你第一次尝试退出 shell 时发出警告：

```
$ sleep 70
^Z
[2] + Stopped sleep 70
$
$ exit
logout
There are stopped jobs.
$
```

你可以使用 ps 命令查看已停止的作业：

```
$ ps -l
F S UID PID PPID [ ... ] TTY TIME CMD
F S 1001 1509 1508 [ ... ] pts/0 00:00:00 bash
0 T 1001 1532 1509 [ ... ] pts/0 00:00:00 sleep
0 T 1001 1533 1509 [ ... ] pts/0 00:00:00 sleep
0 R 1001 1534 1509 [ ... ] pts/0 00:00:00 ps
$
```

在 S 列（进程状态）中，ps 命令显示已停止作业的状态为 T。这表明命令正在被跟踪或已被停止。

如果你确实想要在仍有活动停止作业的情况下退出 shell，只需再次输入 exit 命令。shell 将退出，并终止已停止的作业。

或者，既然你已经知道了停止作业的 PID，你可以使用 kill 命令发送 SIGKILL (9) 信号来终止它：

```
$ kill -9 1532
[1]- Killed sleep 60
$ kill -9 1533
[2]+ Killed sleep 70
$
```

每次 shell 产生提示符时，它还会显示任何在 shell 中状态发生变化的作业的状态。在你杀死一个作业后，shell 会显示一条消息，表明该作业在运行时被杀死，然后提供提示符。

> **注意**
> 在某些 Linux 系统上，当你杀死作业时，最初可能不会得到任何响应。然而，下一次你执行导致 shell 提示符的操作时（例如按下 Enter 键），你将看到一条表明作业已被杀死的消息。

# 捕获信号

你可以捕获出现时的信号并执行其他命令，而不是让脚本对信号不加管理。trap 命令允许你指定 shell 脚本可以监视和从 shell 中截获的 Linux 信号。如果脚本接收到 trap 命令中列出的信号，它会阻止该信号被 shell 处理，而是进行本地处理。

trap 命令的格式为

```
trap commands signals
```

在 trap 命令中，你只需列出希望 shell 执行的命令，以及你希望捕获的信号的空格分隔列表。你可以通过信号的数值或其 Linux 信号名称来指定信号。

以下是一个使用 trap 命令捕获 SIGINT 信号并控制脚本在信号发送时行为的简单示例：

```
$ cat trapsignal.sh
#!/bin/bash
#Testing signal trapping
#
trap "echo ' Sorry! I have trapped Ctrl-C'" SIGINT
# echo This is a test script.
#
count=1
while [ $count -le 5 ]
do
	echo "Loop #$count"
	sleep 1
	count=$[ $count + 1 ]
done
#
echo "This is the end of test script."
exit
$
```

此示例中使用的 `trap` 命令每次检测到 `SIGINT` 信号时都会显示一条简单的文本消息。捕获此信号使脚本能够抵御用户尝试使用 Bash shell 键盘 Ctrl+C 命令停止程序的企图：

```
$ ./trapsignal.sh
This is a test script.
Loop #1
Loop #2
^C Sorry! I have trapped Ctrl-C
Loop #3
^C Sorry! I have trapped Ctrl-C
Loop #4
Loop #5
This is the end of test script.
$
```

每次使用 Ctrl+C 按键组合时，脚本都会执行 `trap` 命令中指定的 `echo` 语句，而不是不管理该信号并允许 shell 停止脚本。

> **警告**
> 如果你的脚本中的某个命令被信号中断，使用带有指定命令的 trap 并不一定能使被中断的命令从停止处继续执行。为了保持脚本中关键操作的流畅进行，使用空规格与要捕获的信号列表一起使用 trap，例如

```
trap "" SIGINT
```

以这种方式使用 trap 允许脚本完全忽略信号中断，并继续其重要工作。

### 捕获脚本退出

除了在 shell 脚本中捕获信号外，你还可以在 shell 脚本退出时捕获它们。这是一种在 shell 完成其工作时执行命令的便捷方式。

要捕获 shell 脚本退出，只需在 trap 命令中添加 `EXIT` 信号：

```
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
    count=$[ $count + 1 ]
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

当脚本到达正常退出点时，trap 被触发，shell 执行你在 `trap` 命令行中指定的命令。如果你过早退出脚本，`EXIT` trap 也会起作用：

```
$ ./trapexit.sh
Loop #1
Loop #2
Loop #3
^C Goodbye...
$
```

由于 `SIGINT` 信号不在 `trap` 命令列表中，当使用 Ctrl+C 按键组合发送该信号时，脚本会退出。然而，在脚本退出之前，由于捕获了 `EXIT`，shell 会执行 `trap` 命令。

# 修改或移除 trap

为了在 shell 脚本的不同部分以不同方式处理 trap，你只需使用新选项重新发出 `trap` 命令：

```
$ cat trapmod.sh
#!/bin/bash
#Modifying a set trap
#
trap "echo ' Sorry...Ctrl-C is trapped.'" SIGINT
#
count=1
while [ $count -le 3 ]
do
       echo "Loop #$count"
       sleep 1
       count=$[ $count + 1 ]
done
#
trap "echo ' I have modified the trap!'" SIGINT
#
count=1
while [ $count -le 3 ]
do
       echo "Second Loop #$count"
       sleep 1
       count=$[ $count + 1 ]
done
#
exit
$
```

修改信号 trap 后，脚本将以不同方式管理信号。然而，如果在 trap 被修改前收到信号，脚本将根据原始的 `trap` 命令处理该信号：

```
$ ./trapmod.sh
Loop #1
^C Sorry...Ctrl-C is trapped.
Loop #2
Loop #3
Second Loop #1
Second Loop #2
^C I have modified the trap!
Second Loop #3
$
```

> **提示**
> 如果你在交互式 shell 会话中试用 `trap` 命令，可以通过发出 `trap -p` 来查看正在捕获哪些信号。如果没有显示任何内容，说明你的 shell 会话正在以默认方式处理信号。

你也可以移除已设置的 trap。在 `trap` 命令后添加两个破折号，并列出你希望恢复为默认行为的信号：

```
$ cat trapremoval.sh
#!/bin/bash
#Removing a set trap
#
trap "echo ' Sorry...Ctrl-C is trapped.'" SIGINT
#
count=1
while [ $count -le 3 ]
do
    echo "Loop #$count"
    sleep 1
    count=$(( count + 1 ))
```

