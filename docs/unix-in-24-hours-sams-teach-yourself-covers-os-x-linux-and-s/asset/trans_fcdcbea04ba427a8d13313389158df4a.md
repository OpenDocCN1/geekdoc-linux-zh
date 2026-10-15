

# 备注

尽管一个作业可以被停止，但它通常仍然会消耗资源，因此你应该注意不要让周围有太多停止的程序，以免影响系统的其他用户。要释放资源，请杀死或终止这些作业。

另一种策略是让程序在后台启动并让 Unix 管理它。如果程序需要用户输入或有输出要显示，它就会停止，就像你用 bg 将其放到后台后，进程在已经开始运行后停止的那样。要让程序（或管道！）自动在后台启动，只需在命令行末尾输入一个 & 即可。

1. 这是一个复杂的 awk 命令序列的示例，它处理文件而不需要任何输入或提供任何输出：

Click here to view code image

```
$ awk -F: '{print $1 " "$5}' < /etc/passwd | \
awk -F, '{print $1}' | \
awk '{ if (NF > 2) print $0 }' | \
sort > who.is.who
```

大约 10 秒后，$ 提示符返回；花费这么长时间是为了将密码文件通过三部分 awk 过滤器，排序整个输出并将其保存到文件 who.is.who 中。

## 警告

当你处理长命令时，了解你可以随时移动到下一行是有用的——即使在输入中间——方法是使用单个反斜杠结束当前行。请注意，反斜杠必须是该行上的最后一个字符。

有了这个新文件，我可以轻松查找一个账户以查看该用户的全名：

Click here to view code image

```
$ alias lookup='grep -i !* who.is.who'
$ who | head
root      console  Dec  6 18:02
maritanj  ttyAa    Dec  8 21:20
efb       ttyAb    Dec  8 12:12
wifey     ttyAc    Dec  8 19:41
phamt u   ttyAe    Dec  8 21:14
curts     ttyAf    Dec  8 21:14
seifert   ttyAg    Dec  8 21:11
taylor    ttyAh    Dec  8 21:09
halcyon   ttyAi    Dec  8 18:34
jamilrr   ttyAj    Dec  8 20:25
Broken pipe
$ lookup maritanj
maritanj = Jorge Maritan
$ lookup efb
efb = Edward F. Billiard
$
```

## 2. 要让构建过程在后台运行，我可以在启动后立即停止该进程，使用 ^Z：

Click here to view code image

```
$ !awk
awk -F, '{print $1" = "$5}' < /etc/passwd | awk -F, '{print $1}'
| awk '{ if (NF > 2) print $0 }' | sort > who.is.who
Stopped
$
```

## 备注

请注意，我使用历史机制重复的命令被列为全部在一行上，即使我最初是在多行中输入的。

此时，bg 将继续该程序，在后台运行它：

Click here to view code image

```
$ bg
[1] awk -F, {print $1" = "$5} </etc/passwd | awk -F, {print $1} | awk
{ if (NF > 2) print $0 } | sort > who.is.who &
$
```

方括号中的数字是 shell 中此作业的控制号。片刻之后，你将了解到为什么记下这个数字很方便。

在某些系统上，完成后后台作业会立即通知你它已完成，但在大多数系统上，完成的后台作业在运行完毕后会等待你按 Return 获取新的系统提示符，然后才会通知你。大约 30 或 40 秒后，我按 Return 并看到以下内容：

Click here to view code image

```
$
[1] Done awk -F:
{print $1" = "$5} </etc/passwd | awk -F,
{print $1} | awk { if (NF > 2) print $0 } | sort > who.is.who
$
```

## 3. 将程序移入后台的更好策略是自动将进程移至后台，只需在末尾添加一个 &：

```
```sh
$ 
[1]    Done                    awk -F: '{print $1" = "$5}' < /etc/passwd | awk
-F, '{ print $1 }' | awk '{ if (NF > 2) print $0 }' | sort > who.is.who
$
```
```

## 4. 如果我尝试自动将一个有输入或输出的程序移至后台会发生什么？

```
```sh
$ vi &
[1] 28258
$
```
```

这看起来没问题。按下 Return 后情况就不同了：

[Click here to view code image](#)

```
```sh
$ 
[1]  + Stopped (tty output) vi
$
```
```

你可以看到这个程序已停止，因为它想要显示一些信息（输出）。如果程序期望输入，消息将是 `Stopped (tty input) program name`。

我可以使用 `fg` 将此程序带回前台。

由于 Unix 设计的很大一部分侧重于通过过滤器运行数据流并将输出保存到文件，你可以在后台运行各种命令，从而在它处理时腾出时间做其他工作。请记住，你可以将需要大量处理时间然后在屏幕上显示信息的作业放到后台。当后台作业需要向屏幕写入内容时，程序将自动停止，直到你输入 `fg` 将其拉回前台。

还请记住，当你希望程序在后台运行时，你也可以重定向其输出。一个常见的命令会像 `longcmd > longcmd.output &` 这样。

# 任务 15.3：查找正在运行的任务

有两种方法可以跟踪 Unix 系统上正在运行的程序。较简单的方法是使用 `jobs`，它显示当前 shell 中你停止并移入后台的进程。输入 `jobs`，系统会告诉你是否有任何程序处于停止或运行状态。

另一种方法是使用一个复杂的命令 `ps`，它显示整个计算机的处理器状态。处理器是计算机本身的另一个名称。幸运的是，不带任何参数时，它只显示与当前登录会话关联的活动或停止的程序。不要被欺骗：`ps` 程序的标志甚至比 `ls` 还多。其中绝大多数永远不会对你或任何普通 Unix 用户有价值。令人困惑的是，BSD 系统和 System V 之间的标志也非常不同。[Table 15.1](#) 总结了最有帮助的 `ps` 标志。

