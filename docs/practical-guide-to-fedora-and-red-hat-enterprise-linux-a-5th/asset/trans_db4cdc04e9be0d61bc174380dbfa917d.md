

当把数组元素的索引放在 `*` 的位置传给同一个运算符时，它会返回该元素的长度：

```bash
$ echo ${#NAMES[1]}
5
```

你可以在赋值语句的左侧使用下标来替换数组中的选定元素：

```bash
$ NAMES[1]=alex
$ echo ${NAMES[*]}
max alex sam zach
```

## 变量的局部性

默认情况下，变量仅局部于声明它的进程。因此，除非你显式地将变量设为可用（全局），否则 Shell 脚本无法访问你在登录 Shell 中声明的变量。在 bash 中，`export` 使变量对子进程可用。

一旦你使用 `export` 内置命令并以变量名作为参数，Shell 就会将该变量的值放入子进程的调用环境中。这种按值调用为每个子进程提供了该变量的一份副本供其自身使用。

下面的 `extest1` Shell 脚本将变量 `cheese` 的值赋为 `american`，然后显示其文件名（`extest1`）以及 `cheese` 的值。接着，`extest1` 脚本调用 `subset`，后者尝试显示相同的信息。然后 `subset` 声明一个 `cheese` 变量并显示其值。当 `subset` 完成时，它控制返回到正在执行 `extest1` 的父进程。此时 `extest1` 再次显示原始 `cheese` 变量的值。

```bash
$ cat extest1
cheese=american
echo "extest1 1: $cheese"
subset
echo "extest1 2: $cheese"
$ cat subset
echo "subset 1: $cheese"
cheese=swiss
echo "subset 2: $cheese"
$ extest1
extest1 1:  american
subset 1:
subset 2:  swiss
extest1 2:  american
```

`subset` 脚本从未接收到来自 `extest1` 的 `cheese` 的值，而 `extest1` 也从未丢失该值。与现实世界不同，子进程永远无法影响父进程的属性。当某个进程尝试显示一个未声明的变量的值时（如 `subset` 中的情况），该进程不会显示任何内容；未声明变量的值是一个空字符串。

下面的 `extest2` 脚本与 `extest1` 相同，除了它使用 `export` 使 `cheese` 对 `substest` 脚本可用：

```bash
$ cat extest2
export cheese=american
echo "extest2 1: $cheese"
substest
echo "extest2 2: $cheese"
$ extest2
extest2 1: american
substest 1: american
substest 2: swiss
extest2 2: american
```

这里子进程继承 `cheese` 的值 `american`，在显示该值后，将其副本更改为 `swiss`。当控制返回给父进程时，父进程中 `cheese` 的副本保留其原始值：`american`。

`export` 内置命令可以选地包含一个赋值：

```bash
export cheese=american
```

前面的语句等价于以下两条语句：

```bash
cheese=american
export cheese
```

虽然很少这样做，但你可以在给变量赋值之前导出该变量。在你更改变量的值之后，你不需要第二次导出一个已经导出的变量。例如，当你将值赋给 `~/.bash_profile` 中的 `PATH` 时，你通常不需要导出 `PATH`，因为它通常已在 `/etc/profile` 全局启动文件中被导出。

## 函数

因为函数在与调用它们的 Shell 相同的环境中运行，所以变量由 Shell 及其调用的函数隐式共享。

```bash
$ function nam () {
> echo $myname
> myname=zach
> }
$ myname=sam
$ nam
sam
$ echo $myname
zach
```

在前面的示例中，`myname` 变量在交互式 Shell 中被设置为 `sam`。然后调用 `nam` 函数。它显示拥有的 `myname` 的值（`sam`）并将 `myname` 设置为 `zach`。最后的 `echo` 显示，在交互式 Shell 中，`myname` 的值已更改为 `zach`。

局部变量对于编写通用使用的函数非常有用。因为该函数可能被许多由不同程序员编写的脚本调用，你需要确保函数内部使用的变量名与调用该函数的程序中的同名变量不相互作用。局部变量消除了这个问题。在函数内部使用时，`typeset` 内置命令将变量声明为局部于其定义的函数。

下一个示例展示了函数中局部变量的使用。它使用了两个名为 `count` 的变量。第一个是在交互式 Shell 中声明并赋值为 10 的。其值从未改变，正如在运行 `count_down` 之后 `echo` 所验证的那样。另一个 `count` 使用 `typeset` 声明为函数的局部变量。其值在函数外部未知，取值范围从 4 到 1，正如函数内的 `echo` 命令所确认的那样。

示例展示了从键盘输入函数；它不是一个 Shell 脚本。（参见第 922 页的技巧“函数不是 Shell 脚本”）。

```bash
$ function count_down () {
> typeset count
> count=$1
> while [ $count -gt 0 ]
> do
> echo "${count}..."
> ((count=count-1))
> sleep 1
> done
> echo "Blast Off."
> }
$ count=10
$ count_down 4
4...
3...
2...
1...
Blast Off.
$ echo $count
10
```

`((count=count-1))` 赋值被双括号包围，这导致 Shell 执行算术求值（第 950 页）。在双括号内，你可以引用 Shell 变量而无需前导美元符号（$）。

## 特殊参数

特殊参数使你能够访问与命令行参数和 Shell 命令执行相关的有用值。你通过在特殊字符前加美元符号（$）来引用 Shell 特殊参数。与位置参数一样，不可能通过赋值修改特殊参数的值。

### $$: 进程 ID 号

Shell 在 `$$` 参数中存储执行它的进程的进程 ID（PID）号。在以下交互中，`echo` 显示该变量的值，`ps` 实用程序确认其值。两个命令都显示 Shell 具有 PID 号 209：

```bash
$ echo $$
5209
$ ps
  PID TTY           TIME CMD
 5209 pts/1    00:00:00 bash
 6015 pts/1    00:00:00 ps
```

由于 `echo` 内置于 Shell 中，当给出 `echo` 命令时，Shell 无需创建另一个进程。然而，无论 `echo` 是否为内置命令，结果都是相同的，因为 Shell 在分叉新进程执行命令*之前*就替换了 `$$` 的值。尝试使用 `echo` 实用程序（`/bin/echo`），它由另一个进程执行，看看会发生什么。在下面的示例中，Shell 替换 `$$` 的值，并将该值作为文件名的前缀传递给 `cp`：

```bash
$ echo $$
8232
$ cp memo $$.memo
$ ls
8232.memo memo
```

在文件名中包含进程 ID 号对于创建唯一文件名很有用，此时名称的含义并不重要；它常用于 Shell 脚本中创建临时文件的名称。当两个人运行相同的 Shell 脚本时，这些唯一文件名可防止他们无意中共享相同的临时文件。

下面的示例演示了 Shell 在运行 Shell 脚本时创建一个新的 Shell 进程。`id2` 脚本显示运行它的进程的 PID 号（而不是调用它的进程——`$$` 的替换是由分叉出来运行 `id2` 的 Shell 执行的）：

```bash
$ cat id2
echo "$0 PID= $$"
$ echo $$
8232
$ id2
./id2 PID= 8362
$ echo $$
8232
```

第一个 `echo` 显示交互式 Shell 的 PID 号。然后 `id2` 显示其名称（$0）以及它所在的子 Shell 的 PID。最后的 `echo` 显示交互式 Shell 的 PID 号没有改变。

### $!

你最后在后台运行的进程的 PID 号存储在 `$!` 中。下面的示例在后台执行 `sleep` 任务并使用 `echo` 显示 `$!` 的值：

```bash
$ sleep 60 &
[1] 8376
$ echo $!
8376
```

### $?: 退出状态

当进程因任何原因停止执行时，它会向父进程返回一个*退出状态*。退出状态也被称为*条件代码*或*返回代码*。`$?` 变量存储最后一个命令的退出状态。

按照惯例，非零退出状态表示*假*值，意味着命令失败。零表示*真*，表明命令成功。在下面的示例中，第一个 `ls` 命令成功，第二个失败：

```bash
$ ls es
es
$ echo $?
0
$ ls xxx
ls: xxx: No such file or directory
$ echo $?
1
```

你可以使用 `exit` 内置命令后跟一个数字来终止脚本，从而指定 Shell 脚本返回的退出状态。如果你不使用带数字的 `exit` 来终止脚本，那么脚本的退出状态就是脚本运行的最后一个命令的退出状态。

```bash
$ cat es
  echo This program returns an exit status of 7.
  exit 7
$ es
This program returns an exit status of 7.
$ echo $?
7
$ echo $?
0
```

`es` Shell 脚本显示一条消息，并以 `exit` 命令终止执行，该命令返回退出状态*7*，这是该脚本中用户定义的退出状态。然后第一个 `echo` 显示 `es` 退出状态的值。第二个 `echo` 显示第一个 `echo` 退出状态的值。值为 0，因为第一个 `echo` 成功。

## 位置参数

*位置*参数包括命令名称和命令行参数。它们被称为*位置*参数，因为在 Shell 脚本中，你通过
