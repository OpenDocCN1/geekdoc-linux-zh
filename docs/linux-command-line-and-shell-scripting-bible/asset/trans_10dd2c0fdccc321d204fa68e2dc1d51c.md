

你可以在 shell 脚本中任何需要显示额外信息的地方添加 `echo` 语句：

```bash
$ cat test1
#!/bin/bash
# 此脚本显示日期和登录系统的用户
echo "The time and date are: "
date
echo "Let's see who's logged into the system"
who
```

当你运行这个脚本时，它会产生如下输出：

```bash
$ chmod u+x test1
./test1
The time and date are:
Mon Sep 24 20:09:35 EST 2007
Let's see who's logged into the system:
rich :0 2007-09-24 18:23 (console)
rich pts/1 2007-09-24 18:24
rich pts/0 2007-09-24 18:42
barbara pts/2 2007-09-24 19:30
katie pts/3 2007-09-24 19:39
$
```

这很棒，但如果你想在命令输出的同一行上输出文本字符串怎么办？你可以使用 `echo` 语句的 `-n` 选项来实现。只需将第一行 `echo` 语句更改为：

```bash
echo -n "The time and date are: "
```

你需要在字符串周围使用引号，以确保输出的字符串末尾有一个空格。命令输出将从字符串结束的地方立即开始。输出看起来如下：

```bash
$ ./test1
The time and date are: Mon Sep 24 20:11:35 EST 2007
Let's see who's logged into the system:
rich :0 2007-09-24 18:23 (console)
rich pts/1 2007-09-24 18:24
rich pts/0 2007-09-24 18:42
barbara pts/2 2007-09-24 19:30
katie pts/3 2007-09-24 19:39
$
```

太完美！`echo` 命令是 shell 脚本与用户交互的关键组成部分。你会发现自己在很多情况下都会使用它，特别是当你想要显示脚本变量的值时。让我们来看一下。

## 使用变量

仅仅在 shell 脚本中运行单个命令是有用的，但它有其局限性。通常你可能想在 shell 命令中结合其他数据以处理信息。你可以通过使用变量来实现。变量允许你在 shell 脚本中临时存储信息，供脚本中的其他命令使用。本节将介绍如何在 shell 脚本中使用变量。

## 环境变量

你已经见过一种类型的 Linux 变量运行了。第 5 章描述了 Linux 系统中的环境变量。你也可以从 shell 脚本中访问这些值。

shell 维护着环境变量来跟踪特定的系统信息，例如系统名称、登录系统的用户名、用户系统 ID（称为 UID）、用户的默认主目录以及 shell 查找程序时使用的搜索路径。你可以通过 `set` 命令显示活动环境变量的完整列表：

```bash
$ set
BACKSPACE=Delete
BASH=/bin/bash
EID=1000
HISTFILE=/home/rich/.bash_history
HISTFILESIZE=1000
HISTSIZE=1000
HOME=/home/rich
HOSTNAME=testing
HOSTTYPE=i586
LANG=en
LANGUAGE=en_US
LINES=24
LOGNAME=rich
```

你可以通过在变量名前前加上美元符号 `$` 在脚本内部调用这些环境变量。下面的脚本演示了这一点：

```bash
$ cat test2
#!/bin/bash
# 显示系统用户信息。
echo "User info for userid: $USER"
echo "UID: $UID"
echo "HOME: $HOME"
$
```

环境变量 `$USER`、`$UID` 和 `$HOME` 用于显示有关登录用户的相关信息。输出应该大致如下：

```bash
$ chmod u+x test2
$ ./test2
User info for userid: rich
UID: 501
HOME: /home/rich
$
```

注意，当运行脚本时，`echo` 命令中的环境变量会被替换为它们的当前值。同时请注意，我们能够在第一个字符串的双引号内放置 `$USER` 系统变量，且 shell 脚本仍然能够理解我们的意图。不过，这是这种方法的一个缺点。看看这个例子中发生了什么：

```bash
$ echo "The cost of the item is $15"
The cost of the item is 5
```

这显然不是我的本意。每当脚本在引号内的美元符号时，它都会认为你正在引用变量。在这个例子中，脚本尝试显示变量 `$1`（未定义），然后是数字 5。要显示真正的美元符号，必须在它前面加上一个反斜杠字符：

```bash
$ echo "The cost of the item is \$15"
The cost of the item is $15
```

这样好多了。反斜杠允许 shell 脚本将美元符号解释为普通字符。你还可以使用花括号来清晰地定义变量名，这在变量后面跟着其他字符时非常有用：

```bash
$ echo "The cost of the item is ${variable}15"
```

