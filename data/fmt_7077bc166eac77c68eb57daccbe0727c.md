
# 第 27 章 BOURNE AGAIN SHELL 编程

## $$: PID 数字

shell 存储了执行它的进程的 PID 数字。在以下交互中，`echo` 显示了该变量的值，`ps` 工具确认了它的值。这两个命令都显示 shell 的 PID 数字为 5209：

```
$ echo $$
5209
$ ps
PID TTY             TIME  CMD
5209 pts/1         00:00:00 bash
6015 pts/1         00:00:00 ps
```

由于 `echo` 是 shell 内置的，当你输入 `echo` 命令时，shell 不会创建另一个进程。然而，无论 `echo` 是否内置，结果都是相同的，因为 shell 在派生进程运行命令之前会替换 `$$` 的值。通过使用由另一个进程运行的工具 `/bin/echo` 看看会发生什么。在下面的示例中，shell 替换了 `$$` 的值，并将该值作为文件名前缀传递给 `cp`：

```
$ echo $$
8232
$ cp memo $$$.memo
$ ls
8232.memo memo
```

在文件名中包含 PID 数字对于在名称含义不重要时创建唯一文件名非常有用；这种技术通常用于 shell 脚本中创建临时文件的名称。当两个人在运行同一个 shell 脚本时，拥有唯一的文件可以防止用户无意中共享同一个临时文件。

下面的示例演示了 shell 在运行脚本时会创建一个新进程。`id2` 显示了运行它的进程的 PID 数字（而不是调用它的进程——`$$` 的替换是由派生来运行 `id2` 的 shell 执行的）：

```
$ cat id2
echo "$0 PID= $$
$ echo $$
8232
$ id2
./id2 PID= 8362
$ echo $$
8232
```

第一个 `echo` 显示了交互式 shell 的 PID 数字。然后 `id2` 显示了它的名称 `$0` 以及它正在运行的子 shell 的 PID 数字。最后一个 `echo` 显示交互式 shell 的 PID 数字没有改变。

`$!` shell 将上一个在后台运行的进程的 PID 数字存储在 `$!` 中。下面的示例将 `sleep` 作为后台任务执行，并使用 `echo` 显示 `$!` 的值：

```
$ sleep 60 &
[1] 8376
$ echo !$ 
```

## $? : 退出状态

当进程因任何原因停止执行时，它会向父进程返回一个退出状态。退出状态也被称为状态码或返回码。`$?` 变量存储了上一个命令的退出状态。

按照惯例，非零退出状态表示假值并意味着命令失败。零表示真，表示命令执行成功。在下面的示例中，第一个 `ls` 成功了，第二个失败了，如退出状态所示：

```
$ ls es
es
$ echo $?
$ ls xxx
ls: xxx: No such file or directory
$ echo $?
1
```

你可以通过使用内置的 `exit` 后跟一个数字来指定 shell 脚本返回的退出状态并终止脚本。如果你没有使用带数字的 `exit` 来终止脚本，脚本的退出状态就是脚本运行的最后一个命令的退出状态。

```
$ cat es
echo This program returns an exit status of 7.
7
$ es
This program returns an exit status of 7.
$ echo $?
7
$ echo $?
0
```
