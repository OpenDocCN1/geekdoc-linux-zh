
在这种情况下，我们可以不给`myll`任何参数，它仍能正常工作。如果我们不提供任何命令行参数，那么`$1`将为空，因此`cd`之后的命令行上没有任何内容。这将使`cd`将我们带回到主目录，并在那里执行长列表。

![](img/75f39fc91296b889c0653851accdfd46_734_0.png)

如果我们提供多个参数，只有第一个会被使用，其余的被忽略。

如果我们使用命令行参数，它必须是一个目录名；否则`cd`命令会失败，脚本会以“bad directory”错误消息终止。稍后，我将展示如何测试有效的目录名和文件名，以便你可以规避潜在错误。

可以使用更复杂的示例来构建`ps`命令的新版本。以下是两个使用命令行参数和命令替换来帮助你进行进程管理的示例。

![](img/75f39fc91296b889c0653851accdfd46_734_1.png)

图 11-2 中的`psg` Shell 程序对于在通常很长的进程状态列表中搜索仅某些命令或用户进程非常有用。这些示例使用了`grep`。`grep`查找包含你所搜索模式的所有行。

![](img/75f39fc91296b889c0653851accdfd46_735_0.png)

```bash
#!/usr/bin/sh
# Program name: psg
# Usage: psg some_pattern
#
# This program searches through a process status (ps -ef)
# listing for a pattern given as the first command-line
# argument.
proc=`ps -ef`		# Get the process listing
head=`echo "$proc" | line`	# Take off the first line (the
			# headings)

echo "$head"		# Write out the headings
echo "$proc" | grep -i $1 | grep -v $0 # Write out lines
# containing $1 but not this program's command line

# Note that $proc MUST be quoted or the newlines in the ps
# -ef listing will be turned into spaces when echoed. $head
# must also be quoted to preserve any extra white space.
```

图 11-2`psg` Shell 程序

下面是`psg`运行时的样子。在这个例子中，我们想要查看系统中运行的所有 Korn shell。

| martyp $ psg ksh |
|---|
| UID PID PPID C STIME TTY TIME CMD |
| root 2954 2936 0 Feb 22 ? 0:01 /bin/ksh /usr/dt/bin/Xsession |
| root 3002 2999 0 Feb 22 pts/2 0:01 -ksh -c unset DT; DISPLAYg |
| root 3067 1 0 Feb 22 ? 0:00 /bin/ksh /usr/dt/bin/sdtoolcheckm |
| jnola 11516 11514 0 May 11 pts/3 0:01 -ksh |
| martyp 29291 29289 0 09:30:04 pts/4 0:02 -ksh |

![](img/75f39fc91296b889c0653851accdfd46_735_1.png)

此程序也可以用于查找终端、进程 ID、父进程 ID、启动日期以及`ps`中的其他任何信息。

作为用户，你可能会启动一些希望停止的进程。例如，你可能启动了一个不会显示在你的显示器上的应用程序。你可以使用`psg`识别该进程，然后使用下一个程序停止该进程，前提是你有权停止该进程。

图 11-3 中的`gkill` shell 程序在`ps -ef`列表中搜索模式（就像`psg`那样）；然后它终止所有列出的进程。

示例使用了`cut`命令，该命令允许你指定要保留的列范围。

```bash
#!/usr/bin/sh
# Program name: gkill
# Usage: gkill some_pattern
# This program will find all processes that contain the
# pattern specified as the first command line argument then
# kills those processes.
# get the process listing
procs=`ps -ef`
echo "The following processes will be killed:"
# Here we list the processes to kill. We don't kill this
# process
echo "$procs" | grep -i $1 | grep -v $0
# Allow the user a chance to cancel.
echo "\nPress Return to continue Ctrl-C to exit"
# If the user presses Ctrl-C the program will exit.
# Otherwise this read waits for the next return character and
# continue.
read junk
# find the pattern and cut out the pid field
pids=`echo "$procs" | grep -i $1 | grep -v $0 | cut -c9-15`
# kill the processes
kill $pids
```

## 图 11-3`gkill` Shell 程序

如果我们未提供任何命令行参数，`grep`会发出错误并继续执行程序。在下一节中，我们将学习如何检查`$1`是否已设置，以及如果未设置如何优雅地进行清理。

让我们现在在后台启动一个进程，使用`psg`程序识别进程号，然后使用`gkill`停止该进程：

```bash
marty $ find / -name .c > cprocs 2>&1 &
[1]      29683
marty $ psg find
          UID  PID  PPID C STIME TTY           TIME CMD
        marty 29683 29579 7 13:54:19 pts/4    0:02 find / -name .c
marty $ gkill 29683
The following processes will be killed:
        marty 29683 29579 10 13:54:19 pts/4   0:03 find / -name .c

Press Return to continue Ctrl-C to exit

marty $
```

当我们启动`find`命令时，我们会得到它的进程号。为了确保不会`kill`错误的进程，我使用`psg`检查了所有正在运行的`find`程序。当确定要`kill`的进程号后，我使用`psg`来`kill`该进程。

尽管本节的 Shell 程序很简单，但它们运用了许多重要的 Shell 编程技术。让我们现在进入测试和分支部分，这是 Shell 编程中最强大的方面之一。

![](img/75f39fc91296b889c0653851accdfd46_737_0.png)

![](img/75f39fc91296b889c0653851accdfd46_737_1.png)

### 测试与分支

决策是 Shell 最强大的功能之一。你有两种方法来检查条件并分支到处理该条件的代码部分。

例如，你可能想向用户提出一个问题，然后检查答案是“是”还是“否”。你还可能在操作文件之前检查该文件是否存在。在这两种情况下，你都可以使用`if`命令来完成该任务。下面是一些解释`if`命令各个部分的 Shell 脚本片段：

```bash
echo "Continue? \c"
read ans
if [ "$ans" = "n" ]
then
    echo "Goodbye"
    exit
fi
```

`echo`和`read`如往常一样提供提示和响应。`if`语句执行下一条命令，如果成功，则执行`then`和`fi`（拼写倒过来）之间的任何命令。
