

# 第5章：理解 Shell

## 子 Shell

为了指示是否生成了子 Shell，这里需要使用一个包含环境变量的命令。*（环境变量在第6章中详细介绍。）* 需要的命令是 `echo $BASH_SUBSHELL`。如果返回 *0*，则没有子 Shell。如果返回 *1* 或更多，则表示创建了子 Shell。

首先，执行仅包含命令列表的示例，并在末尾加上 `echo $BASH_SUBSHELL`：

```
$ pwd ; ls test* ; cd /etc ; pwd ; cd ; pwd ; ls my* ; echo $BASH_SUBSHELL
/home/christine
test_file test_one test_two
/etc
/home/christine
my_file my_scrypt my_sscript my_sscript
0
$
```

在命令输出的最后，可以看到显示了数字零（*0*）。这表明没有创建子 Shell 来执行这些命令。

使用进程列表时结果不同。列表在执行时在末尾加上了 `echo $BASH_SUBSHELL`：

```
$ (pwd ; ls test* ; cd /etc ; pwd ; cd ; pwd ; ls my* ; echo $BASH_SUBSHELL)
/home/christine
test_file test_one test_two
/etc
/home/christine
my_file my_scrypt my_sscript my_sscript
1
$
```

在这种情况下，输出末尾显示了数字一（*1*）。这表明确实创建并使用了子 Shell 来执行这些命令。

因此，进程列表是用括号括起来的命令分组，它创建一个子 Shell 来执行这些命令。你甚至可以通过在进程列表内部嵌入括号来创建孙级子 Shell：

```
$ (pwd ; echo $BASH_SUBSHELL)
/home/christine
1

$ (pwd ; ( echo $BASH_SUBSHELL))
/home/christine
2
$
```

请注意，在第一个进程列表中，显示了数字一（*1*），表示你预期的子 Shell。然而，在示例的第二个进程列表中，在 `echo $BASH_SUBSHELL` 命令周围包含了额外的括号。这些额外的括号导致了另一个子 Shell 的创建，以执行该命令。因此，显示了数字二（*2*），表示子 Shell 中的子 Shell。

子 Shell 经常用于 Shell 脚本中的多处理。然而，进入子 Shell 是一种*昂贵的*方法。（在这种情况下，*昂贵*意味着消耗更多的资源，如内存和处理器性能。）它还可能显著减慢任务的完成速度。对于交互式 CLI Shell 会话，也存在着子 Shell 问题，它并不是真正的多处理，因为终端会被子 Shell 的 I/O 占用。

## 创造性地使用子 Shell

在交互式 Shell CLI 中，你有更 productive 的方法使用子 Shell。进程列表、协作进程和管道（在第11章中介绍）都使用子 Shell。每个都可以在交互式 Shell 中有效地使用。

在交互式 Shell 中一种 productive 的子 Shell 方法使用后台模式。在你学习如何将后台模式和子 Shell 一起使用之前，你需要理解后台模式。

### 探索后台模式

在后台模式下运行命令允许处理该命令并释放你的 CLI 以便其他用途。展示后台模式的一个经典命令是 `sleep` 命令。

`sleep` 命令接受一个参数，即你希望进程等待（睡眠）的秒数。此命令通常用于在 Shell 脚本中引入暂停。`sleep 10` 命令使会话暂停10秒，然后返回一个 Shell CLI 提示符：

```
$ sleep 10
$
```

要将命令放入后台模式，需要在末尾加上 & 字符。将 `sleep` 命令放入后台模式可以使用 `ps` 命令进行一点调查：

```
$ sleep 3000&
[1] 2542
$
$ ps -f
$
  UID   PID   PPID  C STIME TTY      TIME CMD
christi+ 2356 2352 0 13:27 pts/0  00:00:00 -bash
christi+ 2542 2356 0 13:44 pts/0  00:00:00 sleep 3000
christi+ 2543 2356 0 13:44 pts/0  00:00:00 ps -f
$
```

`sleep` 命令在后台（&）被指示睡眠 `3000` 秒（50分钟）。当它被放入后台时，在返回 Shell CLI 提示符之前显示了两项信息。第一项信息是后台任务的编号（1），显示在括号中。第二项是后台任务的进程 ID（2542）。

使用 `ps` 命令显示各种进程。请注意，列出了 `sleep 3000` 命令。还要注意，其在第二列中的进程 ID（PID）与命令进入后台时显示的 PID 相同，即 2542。

除了 ps 命令，你还可以使用 jobs 命令显示后台任务信息。jobs 命令显示当前在后台模式下运行的进程（任务）：

```
$ jobs
[1]+  Running                 sleep 3000 &
$
```

jobs 命令在括号中显示任务编号（1）。它还显示任务的当前状态（Running）以及命令本身（sleep 3000 &）。

通过在使用 jobs 命令时使用 -l（小写 L）参数，你可以看到更多信息。-l 参数除了其他信息外还显示命令的 PID：

```
$ jobs -l
[1]+  2542 Running                  sleep 3000 &
$
```

> **提示**
> 当有多个后台进程在运行时，有一些额外的有用信息可以显示哪个后台任务最后启动。最近启动的任务在 jobs 命令的显示中，其任务编号旁边有一个加号（+）。而次新的进程会有一个减号（-）以提供额外信息。

当后台任务完成时，其完成状态会在你下一次在命令行按下回车键时显示：

```
$
[1]+  Done                  sleep 3000
$
```

后台模式非常方便。它提供了一种在 CLI 上创建有用子 Shell 的方法。

### 将进程列表放入后台

通过将进程列表放入后台，你可以在子 Shell 中进行大量的多处理。一个附带的好处是你的终端不会被子 Shell 的 I/O 占用。

如前所述，进程列表是在子 Shell 中执行的单个或一系列命令。使用包含 sleep 命令的进程列表并显示 BASH_SUBSHELL 变量，其操作正如你所预期的：

```
$ (sleep 2 ; echo $BASH_SUBSHELL ; sleep 2)
1
$
```

在前一个示例中，发生2秒暂停，显示数字一（1）表示单个子 Shell 级别（子 Shell），然后另一个2秒暂停发生后才返回提示符。这里没什么特别。

将相同的进程列表放入后台模式可能会导致命令输出有稍微不同的效果：

```
$ (sleep 2 ; echo $BASH_SUBSHELL; ; sleep 2 ) &
[1]  2553
$ 1

[1]+  Done    ( sleep 2; echo $BASH_SUBSHELL; ; sleep 2 )
$
```

将进程列表放入后台会导致显示任务编号和进程 ID，并且返回提示符。然而，奇怪的事情是，显示的数字一（1），表示单级子 Shell，显示在提示符旁边！不要为此感到困惑。只需按下回车键，你就会得到另一个提示符。

在后台模式下使用进程列表是在 CLI 上使用子 Shell 的一种创造性方法。这允许你用更少的击键次数提高生产率。

当然，`sleep` 和 `echo` 命令的进程列表只是为了示例目的。使用 `tar` 创建备份文件（参见第4章）是有效使用后台进程列表的更实际示例：

```
$ (tar -cf Doc.tar Documents ; tar -cf Music.tar Music) &
[1]  2567
$ 
$ ls *.tar
Doc.tar   Music.tar
[1]+  Done    ( tar -cf Doc.tar Documents ;
               tar -cf Music.tar Music )
$
```

在 CLI 上创造性地使用子 Shell 不仅仅是在后台模式下使用进程列表。协作进程是另一种方法。

### 观察协作进程

协作进程同时做两件事。它在后台模式下生成一个子 Shell，并在那个 Shell 中执行一个命令。

为了执行协作进程，使用 `coproc` 命令连同要在子 Shell 中执行的命令：

```
$ coproc sleep 10
[1]  2689
$
```

协作进程几乎与将命令放入后台模式完全相同，只是它创建了一个子 Shell。你会注意到，当输入 `coproc` 命令及其参数时，启动了一个后台任务。屏幕上显示了后台任务编号（1）和进程 ID（2689）。

