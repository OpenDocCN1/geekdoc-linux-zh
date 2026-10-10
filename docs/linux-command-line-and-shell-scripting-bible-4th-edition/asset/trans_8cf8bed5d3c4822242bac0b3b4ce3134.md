

当然，`sleep` 和 `echo` 命令的进程列表仅仅是为了举例说明。使用 `tar` 创建备份文件（参见第 4 章）是有效使用后台进程列表的一个更实用的例子：

```
$ (tar -cf Doc.tar Documents ; tar -cf Music.tar Music)&
[1] 2567
$
$ ls *.tar
Doc.tar  Music.tar
[1]+  Done    (tar -cf Doc.tar Documents;
tar -cf Music.tar Music )
$
```

将进程列表置于后台模式并不是在命令行界面（CLI）中创造性地使用子 shell 的唯一方法。协同处理（Co-processing）是另一种方法。

## 探索协同处理

协同处理同时执行两项任务。它以后台模式生成一个子 shell，并执行该子 shell 内的命令。

要进行协同处理，需要使用 `coproc` 命令，并结合要在子 shell 中执行的命令：

```
$ coproc sleep 10
[1] 2689
$
```

协同处理的操作几乎与将命令置于后台模式相同，区别在于它会创建一个子 shell。你会注意到，当输入 `coproc` 命令及其参数时，启动了一个后台任务。后台任务编号（1）和进程 ID（2689）显示在屏幕上。

`jobs` 命令允许你查看协同处理的状态：

```
$ jobs
[1]+  Running     coproc COPROC sleep 10 &
$
```

从前面的例子中，你可以看到在子 shell 中执行的后台命令是 `coproc COPROC sleep 10`。COPROC 是 `coproc` 命令赋予该进程的名称。你可以使用该命令的扩展语法自行设置名称：

```
$ coproc My_Job { sleep 10; }
[1] 2706
$
$ jobs
[1]+  Running            coproc My_Job { sleep 10; } &
$
```

通过使用扩展语法，协同处理的名称被设置为 My_Job。请注意，扩展语法有点棘手。确保你在第一个大括号（{）后面和命令开始之前放置一个空格。此外，命令必须以分号（;）结尾。并且，你必须在分号后面和闭大括号（}）前面放置一个空格。

> **注意**
> 协同处理允许你执行非常花哨的操作，向在子 shell 中运行的进程发送/接收信息。只有当你有多个协同进程正在运行且需要与它们全部通信时，才需要为协同进程命名。否则，只需让 coproc 命令将名称设置为默认值 COPROC 即可。

你可以非常巧妙地结合协同处理和进程列表，创建嵌套的子 shell。只需输入你的进程列表，并在其前面加上 coproc 命令即可：

```
$ coproc ( sleep 10; sleep 2 )
[1] 2750
$
$ jobs
[1]+  Running            coproc COPROC ( sleep 10; sleep 2 ) &
$
$ ps --forest
  PID TTY          TIME CMD
2367 pts/0    00:00:00 bash
2750 pts/0    00:00:00 \_ bash
2751 pts/0    00:00:00 | \_ sleep
2752 pts/0    00:00:00 \_ ps
$
```

请记住，生成子 shell 可能会带来高昂的代价并导致速度变慢。创建嵌套的子 shell 更是如此！

使用子 shell 可以提供灵活性和便利性。理解其行为对于实现这些目标至关重要。理解命令操作也很重要。在下一节中，我们将探讨内置命令和外部命令之间的行为差异。

## 理解外部命令和内置命令

在学习 GNU Bash shell 时，你可能已经听过 *内置命令* 这一术语。理解 shell 内置命令和非内置（外部）命令非常重要。内置命令和非内置命令的工作方式截然不同。

### 观察外部命令

*外部命令*，有时也称为文件系统命令，是存在于 Bash shell 之外的程序。换句话说，它不是内置于 shell 程序中的。外部命令程序通常位于 /bin、/usr/bin、/sbin 或 /usr/sbin 目录中。

ps 命令是一个外部命令。你可以使用 `which` 和 `type` 命令来查找其文件名：

```
$ which ps
/usr/bin/ps
$ type ps
ps is /usr/bin/ps
$ ls -l /usr/bin/ps
-rwxr-xr-x. 1 root root 142216 May 11  2019 /usr/bin/ps
$ 
```

每当执行外部命令时，都会创建一个子进程。这种操作称为 *fork（分叉）*。 conveniently，外部命令 ps 会显示其当前父进程以及它自身的分叉子进程：

```
$ ps -f
UID   PPID  C STIME  TTY        TIME CMD
christi+ 2367 2363  0 10:47 pts/0    00:00:00 -bash
christi+ 4242 2367  0 13:48 pts/0    00:00:00 ps -f
$
```

由于它是一个外部命令，当 `ps` 命令执行时，会创建一个子进程。在这种情况下，`ps` 命令的 PID 是 4242，父进程 PID 是 2367。Bash shell 进程在这种情况下是父进程，其 PID 为 2367。**图 5-3** 展示了当外部命令执行时发生的 fork（分叉）过程。

![](img/a5025f22e05b92f409563a958cac7312_192_0.png)

### 图 5-3 外部命令的 fork（分叉）

每当进程必须 fork（分叉）时，设置新子进程的环境都需要时间和 effort（努力）。因此，外部命令可能会稍显昂贵。

> **注意**
> 如果你 fork（分叉）一个子进程或创建一个子 shell，你仍然可以通过 signaling（信号发送）与其通信，这在命令行和编写 shell 脚本中都极其有用。Signaling（信号发送）允许通过信号进行进程间通信。信号和 signaling（信号发送）在第 16 章“脚本控制”中进行了介绍。

### 观察内置命令

*内置命令* 的不同之处在于，它们不需要子进程即可执行。它们被编译到 shell 中，因此是 shell 工具包的一部分。不存在运行它们的外部程序文件。`cd` 和 `exit` 命令都内置于 Bash shell 中。你可以通过使用 `type` 命令来判断一个命令是否为内置命令：

```
$ type cd
cd is a shell builtin
$
$ type exit
exit is a shell builtin
$
```

由于它们不需要 fork（分叉）子进程来执行或打开程序文件，内置命令更快且更高效。[附录 A](appendix#a "Appendix A") 中提供了 GNU Bash shell 内置命令的列表。

请注意，某些命令具有多种变体。例如，`echo` 和 `pwd` 都有内置命令变体和外部命令变体。这些变体略有不同。要查看命令的多种变体，请使用 `type` 命令的 `-a` 选项：

```
$ type -a echo
echo is a shell builtin
echo is /usr/bin/echo
$
$ which echo
/usr/bin/echo
$
$ type -a pwd
pwd is a shell builtin
pwd is /usr/bin/pwd
$
$ which pwd
/usr/bin/pwd
$
```

使用 `type -a` 命令可以显示这两个命令的两种类型（内置和外部）。注意，`which` 命令只显示外部命令文件。

> **提示**
> 要使用具有多种变体的命令中的外部命令，直接引用该文件即可。例如，要使用 `pwd` 外部命令，请输入 `/usr/bin/pwd`。

## 使用 *history* 命令

Bash shell 会记录你最近使用的命令。你可以调用这些命令，甚至重新使用它们。一个有用的内置命令，允许你浏览和管理这些先前发出的命令，是 `history` 命令。

要查看最近使用的命令列表，请输入不带选项的 `history` 命令：

```
$ history
  1  ps -f
  2  pwd
  3  ls
  4  coproc ( sleep 10; sleep 2 )
  5  jobs
  6  ps --forest
  7  ls
  8  ps -f
  9  pwd
 10  ls -l /usr/bin/ps
 11  history
 12  cd /etc
 13  pwd
 14  ls
 15  cd
 16  type -a pwd
 17  which pwd
 18  type -a echo
 19  which echo
 20  ls
[...]
$
```

在这个例子中，列表被截断，只显示了前 20 条命令。通常，历史中保留的是最后 1,000 条命令。这是很多命令！

> **提示**
> 你可以设置保留在 Bash 历史中的命令数量。为此，你需要修改一个名为 `HISTSIZE` 的环境变量（参见第 6 章）。

你可以调用并重新使用历史记录列表中的上一条命令。这可以节省时间和输入。要调用并重新使用上一条命令，请输入 `!!` 并按下 Enter 键：

```
$ ps --forest
PID TTY TIME CMD
2367 pts/0 00:00:00 bash
5240 pts/0 00:00:00 \_ ps
$
$ !!
ps --forest
PID TTY TIME CMD
2367 pts/0 00:00:00 bash
5241 pts/0 00:00:00 \_ ps
$
```

当输入 `!!` 时，Bash shell 首先显示它正在从 shell 历史中调用的命令。在显示该命令后，它被执行了。

命令历史保存在隐藏的 `.bash_history` 文件中，该文件位于每个用户的家庭目录中：

```
$ pwd
/home/christine
$
$ ls .bash_history
.bash_history
$
```

请注意，在你的 CLI 会话期间，`bash` 命令历史存储在内存中。只有当……时，它才会写入历史文件

