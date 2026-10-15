

| 姓名 | 部门 | GPA |
|---|---|---|
| Jason Kim | ECE | 3.97 |
| Jim Davis | CS | 2.71 |
| John Doe | ECE | 3.54 |
| Pam Meyer | CS | 3.61 |

$
有时，你可能需要连接多个命令。下面的命令行演示了多管道的使用，形成了命令管道。在此命令行中，我们使用了 grep 和 sort 过滤器。

```
$ who | sort | grep "john" | mail -s "John's Terminal" doe@coldmail.com
$
```

该命令对 who 的输出进行排序，并将包含字符串 "john" 的行（如果存在）作为电子邮件消息发送给 doe@coldmail.com，主题行为 "John's Terminal"。就输入和输出重定向而言，该命令行等价于以下命令序列。

```
$ who > temp1
$ sort < temp1 > temp2
$ grep "john" temp2 > temp3
$ mail -s "John's Terminal" doe@coldmail.com < temp3
$ rm temp1 temp2 temp3
$
```

使用管道的命令不使用任何磁盘文件，但前面的命令序列需要三个临时磁盘文件和六次磁盘 I/O（读和写）操作。I/O 操作的数量可能更高，这取决于这些文件的大小、系统负载（即当前使用系统的用户数量）以及系统上运行的其他进程的运行时行为。

因此，管道是 UNIX 的一个特性，允许两个 UNIX 命令（进程）相互通信。因此，管道在 UNIX 中提供了一种进程间通信（IPC）机制。更具体地说，它可以用作同一系统上两个相关进程之间的通道，使它们能够相互通信。通常，进程具有父子关系（参见第 10 章），但具有共同祖先（父进程、祖父进程等）的进程也可以使用管道进行通信。从程序员的角度来看，我们将在第 19 章详细讨论使用管道的 IPC。进程之间的通信是单向的。例如，在 ls | more 中，ls 的输出被 more 作为输入读取。因此，单向通信是从 ls 到 more。对于进程之间的双向通信，至少需要使用两个管道。这在命令 shell 级别无法实现，但在 C/C++ 中可以通过使用 pipe() 系统调用来实现。我们也在第 19 章探讨这一主题。

I/O 重定向和管道可以在单个命令中使用，如下所示：

```
$ grep "John" < Students | lpr -P spr
$
```

![](img/02e070097d401d3bf7de4bf1c470b267_359_0.png)

图 9.13 grep "John" < Students | lpr -Pspr 命令的语义。

![](img/02e070097d401d3bf7de4bf1c470b267_359_1.png)

图 9.14 egrep 'A$' < ece446.grades | sort > ece446.As.sorted 命令的语义。

在这里，grep 命令搜索 Students 文件中包含字符串 "John" 的行，并将这些行发送给 lpr 命令，以便在名为 spr 的打印机上打印。图 9.13 说明了此命令的语义。

在下面的命令中，egrep 从 ece446.grades 读取输入，并将其输出（以字符 A 结尾的行）发送给 sort 实用程序，sort 对这些行进行排序并将它们存储在当前目录中名为 ece446.As.sorted 的文件中。最终结果是，获得 ECE446 课程 A 等级的学生的姓名、成绩和等级存储在当前目录中的 ece446.As.sorted 文件中。图 9.14 说明了此命令的语义。

```
$ egrep 'A$' < ece446.grades | sort > ece446.As.sorted
$
```

假设在第 9.4 节运行 ssh server sort < datafile 命令之前，你想确保本地系统上的 datafile 与服务器上名为 ~/research/pvm/datafile.server 的更新副本一致。你可以复制 datafile.server 并将其与本地副本 datafile 进行比较。但这样你将有三个副本，如果不小心可能会删除错误的副本。在这种情况下，你可以运行以下命令，在不将 datafile.server 复制到你的（本地）计算机的情况下查看本地副本与服务器上副本之间的差异。

```
$ ssh server cat ~/research/pvm/datafile.server | diff datafile -
$
```

在这种情况下，cat 命令在服务器端运行，其输出作为输入提供给在本地机器上执行的 diff 命令。diff 命令的输出也发送到本地机器的显示屏上。图 9.15 说明了此命令的语义。

## 9.12 重定向与管道组合

你不能单独使用重定向运算符和管道将命令的 stdout 重定向到文件并同时将其连接到另一个命令的 stdin 在单个命令行中。然而，你可以使用 tee 实用程序来实现这一点。你可以使用此实用程序告诉命令 shell 将命令的 stdout 发送到作为 tee 参数指定的一个或多个文件，

