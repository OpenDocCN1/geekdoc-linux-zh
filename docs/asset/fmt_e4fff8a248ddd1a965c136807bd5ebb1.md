
或者你可以在文件内部插入 `set -x` 命令。事实上，你可以在程序中插入任意数量的 `set -x` 和 `set +x` 命令，按需开启或跟踪模式。

# 不带参数的 set

如果你不给 `set` 任何参数，你将获得环境中所有变量（无论是本地还是导出的）的字母列表：

```bash
$ set
show all variables
CDPATH=/users/steve/usr/spool
EDITOR=/bin/vi
HOME=/users/steve
IFS=
LOGNAME=steve
MAIL=/users/steve/mail/steve
MAIL_RECEIVED=
PATH=/users/steve/bin:
PHONEBOOK=/users/steve/phonebook
PS1=
PWD=/users/steve/misc
SHELL=/bin/sh
TERM=xterm
TTY=
TEST=
```

# 使用 set 重新分配位置参数

没有办法可以直接给位置参数赋值；例如：

```
1=100
```

Unix Shell Programming, Third Edition. Unix Shell Programming, Third Edition, ISBN: 0-672-32490-3

为 architect@open-source.com, Terry Smith 准备。Copyright © 2009 by Global Publishing. 此下载文件仅供个人使用，并受服务条款限制。任何其他用途均需获得版权所有者的事先书面许可。严禁未经的使用、复制和/或发行，违反法律。保留所有权利。

# 关于参数更多

这些参数在执行 Shell 程序时初始设置。改变它们的唯一方法是使用 `shift` 或 `set` 命令。如果在命令行将单词作为参数给 `set`，这些单词将被分配给位置参数 `$1`、`$2` 等。之前存储在位置参数中的值将永久丢失。

```bash
set a b
```

将 `a` 分配给 `$1`，`b` 分配给 `$2`，`$33`。`$#` 也变为 3。

```bash
set one two four
echo $1:$2:$3
one:two:four
set echo
$#
```

这应该是 4。现在 `$#` 引用的是什么？

```bash
one two four
done
```

所以在执行 `set` 之后，一切看起来都运行是一致的：`# $`，以及没有列表的 `for` 循环。`set` 经常以此方式用于从文件或终端“解析”数据。这里有一个名为 `words` 的程序：它统计在行中输入的单词数（使用 Shell 对“单词”的定义）：

```bash
+ cat words
# 统计一行的单词
#
read line
set line
echo $$
words
```

这里有一行供你计数。

运行它！

该程序将行存储在 Shell 变量 `line` 中，然后执行命令：

```bash
set line
```

这会导致存储在 `line` 中的每个单词都被分配给位置参数。变量 `$@` 也设置为已分配的单词数，即该行中的单词数。

# --

尝试向 `words` 输入一个以 `-` 开头的行并看看发生什么：

```bash
+ words
-1 + 5 = 4
words: -1: bad option(s)
```

Unix Shell Programming, Third Edition. Unix® Shell Programming, Third Edition, ISBN: 0-672-32490-3

为 architect@openservices.com 准备。此下载文件仅供个人使用，并受服务条款限制。任何其他用途均需获得 Copyright © 2003 by Wiley Publishing 的事先书面许可。严禁未经的使用、复制和/或发行，违反法律。保留所有权利。

已执行。在 Shell 执行替换后，命令行看起来是这样：

```
set -i + 5 = 4
```

当 `set` 执行时，它看到 `-` 并认为选择了一个选项，这解释了错误信息。

`words` 的另一个问题是如果你给它一个完全由空白字符组成的行，或者行为空：

```bash
$ words Just Enter is pressed
CPATH=/users/steve:usr/bin
EDITOR=/bin/vi
HOME=/users/steve
IFS=
LOGNAME=steve
MAIL=/users/steve/mail/steve
MAILSIZE=600
PATH=/usr/bin:/users/steve/bin:
PROFILE=/users/steve/phonebook
PS1=$
STTY=
PWD=/users/steve/misc
SHELL=/bin/sh
TERM=xterm
TMOUT=
TZ=US-EAST-EDT
cd=~
*$
$
```

为了防止这两个问题发生，你可以对 `set` 使用 `--` 选项。这告诉 `set` 不要命令行上的后续参数解释为选项。它防止了在输入空行时 `set` 显示所有变量。

因此 `words` 中的 `set` 命令应该改为：

```bash
set -- $line
```

通过添加 `while` 循环和整数算术，`words` 程序可以轻松修改为统计标准输入中的总单词数，从而让你拥有自己的 `wc` 版本：

```bash
$ cat words
#
# 统计标准输入中的所有单词
#
```

```bash
count=0
while read line
do
	set -- $line
	count=$(( count + 1 ))
done
echo $count
#
```

# 关于参数的更多信息

在读取每行后，都会执行 `set` 命令，以利用 `$#` 会被赋值为行单词数这一特点。为 `set` 提供了 `--w` 选项，以防某些行以 `-` 开头或完全由空白字符组成。

然后将 `$#` 的值加到变量 `count` 中，并读取下一行。当退出循环时，显示 `count` 的值。这代表读取的单词总数。

- * words < /etc/passwd

567

- wc -w < /etc/passwd

567

与 wc 进行比对

（我们的版本比 `wc` 慢得多，因为后者是用 C 语言编写的。）

这里有一种统计目录中文件数量的快速方法：

- * set a

- echo $#n0

这比 `ls | wc` 快得多，因为第一种方法使用了内置命令。通常情况下，如果你尝试尽可能使用 shell 的内置命令，你的 shell 程序运行速度会快得多。

# set 的其他选项

`set` 接受其他几个选项，每个选项都通过在选项前加加 `-` 来启用，通过在选项前加减 `+` 来禁用。我们在这里描述的 `-x` 选项是最常用的。其他的总结在附录 A 中的表 A.9 中。

# IFS 变量

有一个特殊的变量叫做 `IFS`，代表内部字段分隔符（Internal Field Separator）。shell 在解析来自 `read` 命令的输入、命令替换输出（反引号机制）以及执行变量替换时，会使用该变量的值。如果将其输入命令行，它会被视为一个普通的空白字符（即单词分隔符）。

查看设置了什么：

```bash
$ echo "IFS"
```

嗯，这并不怎么启发！要确定其中存储的实际字符，可以将 `echo` 的输出管道到 `od`（八进制转储）命令，并带有 `-b`（字节显示）选项：

> 这种技术在大型目录上可能不起，因为你可能会超过命令行的限制（具体取决于不同的 Unix 系统）。对于此类目录，当在其他命令中进行文件名替换时也会导致问题，例如 `echo` 或 `for file in *`。

Unix® Shell Programming, Third Edition. Unix® Shell Programming, Third Edition, ISBN: 0-672-32490-3

Copyright © 2006 O'Reilly Media. 此下载文件仅供个人使用，受服务条款限制。任何其他用途都需要版权所有者的事先书面许可。

# 关于参数的更多信息

```bash
$ echo 'IFS' | ed -b
000000 040 011 012 012
000004
```

显示的数字列是相对于输入开始的偏移量。接下来的数字是 `od` 读取的字符的八进制等值。第一个数字是 `040`，它是空格字符的 ASCII 值。后面跟着 `011`（制表符），然后是 `012`（换行符）。下一个字符是另一个换行符；这是由 `echo` 写入的。这些 IFS 的字符并不意外；它们就是我们在整本书中讨论过的“空白”字符。

你可以将 `IFS` 改为任何你单个或多个字符。当你想要解析字段不是由普通空白字符分隔的数据行时，这非常有用。例如，我们注意到 shell 会从你使用 `read` 命令读取的任何行开头删除任何空白字符。你可以在执行 `read` 之前将 `IFS` 改为仅换行符，这样就能保留前导空格（因为 shell 不将其视为分隔符）：

```bash
$ read line                尝试这种“旧”方法
$ echo '$Line'
$ Here's a line
$ IFS=-
设置为仅换行符
$ read line                再次尝试
$ Here's a line
$ echo '$Line'            领先空格被保留
```

要将 `IFS` 改为仅换行符，输入左引号，然后按回车键，在下一行输入右引号。在这些引号内无法输入额外的字符，因为它们会被存储在 `IFS` 中，然后供 shell 使用。

现在让我们将 `IFS` 改为更可见的内容，比如冒号：

```bash
$ IFS=
$ read x y z
123:345:678
$ echo $x
123
$ echo $y
678
$ list=one:two:three
$ for x in $list; do echo $x;
done
two
tree
$ var=a:b:c
$ echo $var
abc
```

因为 `IFS` 被改为冒号，当读取该行时，shell 将行分为三个单词：123，345 和 678，它们分别存储在变量 `x`、`y` 和 `z` 中。在下一个示例中，shell 在 `for` 循环中替换 `list` 值时使用了 `IFS`。最后一个示例显示，shell 在执行变量赋值时不使用 `IFS`。

更改 `IFS` 通常与执行 `set` 命令配合使用：

# 关于参数的更多信息

```bash
$ x=100
$ echo $x
100
$ unset x
从环境中移除 x
$ echo $x
```

# unset 命令

有时你可能想从环境中移除变量的定义。要做到这一点，你输入 `unset` 后后跟变量名：

```bash
$ x=100
$ echo $x
100
$ unset x
```

# readonly 命令

你不能取消只读变量。此外，变量 `IFS`、`MAILCHECK`、`PATH`、`PS1` 和 `PS2` 无法取消。此外，某些变量也不支持 `unset` 命令。

## 练习

- 1: 给定以下变量赋值：

```bash
$ EDITOR=/bin/vi
$ DB=
$ EDITTAG=yes
$ POSHERDX=
```

> *默认情况下，Bash 产生如 `declare -r variable` 的输出。要获得 POSIX 兼容的输出，必须带有 `-posix` 命令行选项运行 Bash，或者使用 `-o posix` 选项运行命令。*

## 关于参数的更多内容

以下命令的结果是什么？

```
echo $EDITOR
echo $EDITOR:-/bin/ed
echo $IFS:-/usr/pat/db
echo ${IFS:-/usr/users/pat/db}
echo ${PROBOOK:-}
echo ${EDITTLAG:+${EDITOR:-/bin/ed}
```

2: 重写第 5 到 7 章中的主程序，使用 `set` 命令从 `/etc/passwd` 中提取主目录。如果行中的某个字段为空，程序会发生什么？例如：

```
steve:123::/users/usr:/bin/ksh
```

在这里，第一个字段为空（:）。

3: 利用 shell 构造 `$(var)` 返回存储在 var 中的字符数 这一事实，用 shell 重写 `wc`。务必使用整数算术！（注意：将你的 `IFS` 变量更改为仅换行符，以便保留输入中的空白字符，并使用 shell `read` 命令的 `-c` 选项来忽略输入结尾的反斜杠）。

4: 写一个名为 `rightmatch` 的函数，接受如下所示的两个参数：

```
rightmatch value pattern
```

```
$ rightmatch test .c
test
$ rightmatch /usr/spool:/uocpublic/*
/usr/spool
$ rightmatch /usr/spool:/uocpublic *
/usr/spool/uocpublic
$
```

最后一个示例显示，如果 `rightmatch` 函数不以指定的模式结尾，它应该直接输出它的第一个参数。

5: 写一个名为 `leftmatch` 的函数，其工作原理与练习 4 中开发的 `rightmatch` 函数类似。它的两个参数应如下：

```
leftmatch pattern value
```

以下是一些示例用法：

```
$ leftmatch /usr/spool:/usr/spool:/uocpublic
uocpublic
$ leftmatch s.main.c
main.c
$
```

6: 写一个名为 `substring` 的函数，该函数使用练习 4 和 5 中开发的 `leftmatch` 和 `rightmatch` 函数来从值的左右侧移除模式。它应该接受如下三个参数：

```
$ substring /usr/spool:/usr/spool:/uocpublic /uocpublic
spool
$ substring s.main.c .e
main
$ substring s.main.c .e
Only left match
```

```
main.c
$ substring x. s.main.c .e  No matches
s.main.c
$
```

7: 修改之前练习中开发的 `substring`、`leftmatch` 和 `rightmatch` 函数，使其能够接受选项，允许你从指定值的左侧或右侧移除尽可能可能的模式匹配。

## 第13 章：遗留问题

## 本章内容

- eval 命令

- Wait 命令

- trap 命令

- 关于 I/O 的更多内容

- 函数

- type 命令

- 练习题

我们将一些由于某种原因在逻辑上不适合前面章节的命令和功能放在了本章中。它们的呈现顺序没有特殊的理由。

## eval 命令

本节描述了 shell 中另一个比较不寻常的命令：`eval`。它的格式如下：

```
eval command-line
```

其中 `command-line` 是你在终端上输入的普通命令行。然而，当你在它前面加上 `eval` 时，效果是 shell 会扫描两次命令行并执行它。对于简单的情况，这实际上没有影响：

```
$ eval echo hello
hello
$
```

但考虑以下不使用 `eval` 的示例：

```
$ pipe|1
$ ls Pipes wc -l
ii: No such file or directory
wc: No such file or directory
l-1: No such file or directory
$
```

这些错误来自 `ls`。shell 在变量替换之前会处理管道和 I/O 重定向，因此它永远不会识别 `pipe` 内部的管道符号。`1`、`wc` 和 `-1` 这三个参数被作为参数传递给 `ls`。

> 实际上，发生的情况是 `eval` 仅仅执行传递给它的参数的命令；shell 处理命令行并将参数传递给 `eval`，然后在 `eval` 执行命令时再次执行该操作。结果是 shell 扫描了两次命令行。

## 在命令序列前面加上 eval 可以得到想要的结果：

```
eval ls | wc -l
16
```

当 shell 第一次扫描命令行时，它会将 `|` 替换为 `pipe` 的值。然后 `eval` 导致它解析该行，此时 `|` 被 shell 识别为管道符号。

`eval` 命令经常用于在在一个或多个变量内部构建命令行的 shell 程序。如果变量包含任何 shell 必须在命令行上直接看到的字符（即不是替换的结果），`eval` 就会非常有用。命令终止符（`;`）、I/O 重定向（`<`、`>`）和引号字符都是必须直接出现在命令行上才能对 shell 具有特殊意义的字符。

对于下一个示例，考虑编写一个脚本，其目的是显示传递给它的最后一个参数。你在第 10 章“读取和打印数据”中的 `mycp` 程序中需要获取最后一个参数。你是通过位移参数来实现的。

## 遗留问题

### Wait 命令

如果你将一个命令提交到后台，它将与你的当前 shell 异步运行。有时，你可能希望等待进程完成。例如，你可能发送了一个大型 `sort` 到后台，现在想等待它。你可以在终端中尝试 `wait` 命令：

```
# sort big-data &
$ date
# Oct 2 15:05:42 EDT 2002
$ wait
```

## $ 变量

如果你只有一个进程在后台运行，那么不带参数的 `wait` 就足够了。然而，如果你在后台运行多个命令并想等待其中一个，你可以利用这样一个事实：shell 将最后执行的后台命令的进程 ID 存储在特殊变量 `$!` 中。因此命令是：

```
wait
```

如前提到的，如果你发送了多个命令到后台，可以保存该变量的值以便以后使用：

# prog1

pid1=$!

# prog2

pid2=$!
