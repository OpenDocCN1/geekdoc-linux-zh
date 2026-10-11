
注意，在 Ubuntu Linux 发行版上，别名被用于重写标准的 `ls` 命令。它自动提供了 `--color` 参数，表示终端支持彩色列表。

## 第一部分：Linux 命令行

你可以使用 `alias` 命令创建你自己的别名：

```
$ alias li='ls -li'

$ li

total 36

52981 drwxr-xr-x- 2 Christine Christine 4096 May 19 18:17 Desktop

52985 drwxr-xr-x- 2 Christine Christine 4096 Apr 25 16:59 Documents

52982 drwxr-xr-x- 2 Christine Christine 4096 Apr 25 16:59 Downloads

52986 drwxr-xr-x- 2 Christine Christine 4096 Apr 25 16:59 Music

52987 drwxr-xr-x- 2 Christine Christine 4096 Apr 25 16:59 Pictures

52984 drwxr-xr-x- 2 Christine Christine 4096 Apr 25 16:59 Public

52983 drwxr-xr-x- 2 Christine Christine 4096 Apr 25 16:59 Templates

532891 -rwxr-r-- 1 Christine Christine 36 May 30 07:21 test.sh

52988 drwxr-xr-x- 2 Christine Christine 4096 Apr 25 16:59 Videos

$
```

在定义别名值后，你可以在 shell 的任何时候使用它，包括在 shell 脚本中。请注意，由于命令别名是内置命令，别名仅在定义它的 shell 进程中有效：

```
$ alias li='ls -li'

$ bash

$ li

bash: li: command not found

$ exit

exit
```

幸运的是，你可以让别名值在跨子 shell 中持久化。下一章将介绍如何做到这一点，以及环境变量。

## 总结

本章讨论了复杂的交互式程序——GNU bash shell。它涵盖了理解 shell 进程及其关系，包括 shell 如何被产生以及它们与父 shell 的关系。我们还探索了创建进程的命令。

# 第五章：理解 Shell

`bash` shell 使用一种名为“环境变量”的特性来存储可以被任何程序轻松访问的信息。环境变量有两种类型：

- 全局变量
- 本地变量

## 第一部分：Linux 命令行

本节描述了每种环境变量并展示了如何使用它们。

> 注意：
> 尽管 `bash` shell 使用特定的环境变量，但不同的 Linux 发行版通常会添加自己的环境变量。本章中的环境变量示例可能与你特定发行版的可用情况有所不同。如果你遇到了此处未涵盖的环境变量，请检查你的 Linux 发行版文档。

### 查看全局环境变量

全局环境变量在 shell 会话和任何产生的子 shell 中都是可见。本地变量仅在创建它的 shell 中可用。这使得全局环境变量在创建子 shell 的应用程序中非常有用。

当你启动 `bash` 会话时，Linux 系统会设置几个全局环境变量。（有关此时启动的变量的详细信息，请参见本章后面的“定位系统环境变量”部分）。系统环境变量几乎始终使用大写字母，以区别于普通用户变量。

要查看全局环境变量，请使用 `env` 或 `printenv` 命令：

```
$ printenv

HOSTNAME=server01.class.edu

SELINUX_ROLE_REQUESTED=

TERM=xterm

SHELL=/bin/bash

HISTSIZE=1000

[...

HOME=/home/Christine

LOGNAME=Christine

[...

G_BROKEN_FILENAMES=1

_=/usr/bin/printenv
```

为 `bash` shell 设置了这么多全局环境变量，因此显示内容必须截取。不仅许多变量在登录过程中被设置，你也可以在某种程度上影响哪些变量被设置。

要显示单个环境变量的值，你可以使用 `printenv` 命令，但不能使用 `env` 命令：

```
$ printenv HOME

/home/Christine
```

```bash
$ env HOME

env: HOME: No such file or directory

$
```

你也可以使用 `echo` 命令来显示变量的值。在这种情况下，引用环境变量时，你必须在环境变量名称之前放置一个美元符号 `$` ：

```
$ echo $HOME

/home/Christine

$
```

在使用 `echo` 命令时，使用美元符号配合变量名起的作用不仅仅是显示其当前的定义。变量名前的美元符号允许其作为命令参数传递：

```
$ ls $HOME

Desktop Downloads Music Public test.sh

Documents junk.dat Pictures Templates Videos

$

$ ls /home/Christine

Desktop Downloads Music Public test.sh

Documents junk.dat Pictures Templates Videos

$
```

如前提到的，全局环境变量对于任何进程的子壳都是可见：

```
$ bash

$ ps -f

UID PID PPID C STIME TTY TIME CMD

501 2017 2016 0 16:00:00 -bash

501 2082 2017 0 16:08:00 bash

501 2095 2082 0 16:08:00 ps -f

$

$ echo $HOME

/home/Christine

$

$ exit

exit

$
```

在这个示例中，在使用 `bash` 命令创建一个子壳后，显示了 `HOME` 环境变量的当前值。设置与父壳中完全相同的值 `/home/Christine` 是可以的。

## 查看本地环境变量

局部环境变量正如其名所示，只能在定义它们的本地进程中可见。尽管它们是局部的，但它们与全局环境变量一样重要。事实上，Linux 系统默认也定义了标准的局部环境变量。然而，你也可以定义自己的本地变量。这些变量，正如你所预想的那样，被称为用户定义的本地变量。

在命令行界面（CLI）中尝试查看所有本地变量是一个棘手的小技巧。遗憾的是，没有命令可以只显示这些变量。`set` 命令显示为特定进程定义的所有变量，包括本地环境变量、全局环境变量以及用户定义的变量：

```
$ set

BASH=/bin/bash

...

BASH_ALIASES=()

BASH_ARGC=()\BASH_ARGV=()

BASH_CMDS=()\BASH_LINENO=()\BASH_SOURCE=()

...

colors=/etc/DIR_COLORS

my_variable='Hello World'

...

$
```

使用 `env` 或 `printenv` 命令显示的所有全局环境变量都会出现在 `set` 命令的输出中。额外的环境变量是本地环境和用户定义的变量。

> `env`、`printenv` 和 `set` 命令之间的区别是微妙的。`set` 命令同时显示全局、局部环境变量以及用户定义的变量。它还按字母顺序进行排序。`env` 和 `printenv` 与 `set` 的不同在于它们不进行排序，也不包含任何本地或用户定义的变量。在这种情况下，`env` 和 `printenv` 会产生重复的列表。然而，`env` 命令具有 `printenv` 不具备的附加功能，使其稍微更强大。

## 设置用户定义变量

你可以直接从 `bash` shell 中设置自己的变量。本节将向你展示如何创建自己的变量，并在交互式 shell 或脚本程序中引用它们。

### 设置本地用户定义变量

启动 `bash` shell（或产生 shell 脚本）后，你允许创建在 shell 进程内可见的本地用户定义变量。你可以通过等号将变量赋值一个值，为环境变量分配数值或字符串值：

```
$ echo $my_variable

$ my_variable=Hello

$

$ echo $my_variable

Hello
```

这很简单！现在，每当你需要引用用户定义变量 `my_variable` 的值时，只需通过名称 `$my_variable` 引用它。

如果你需要分配包含空格的字符串，你需要使用单引号或双引号来界定字符串的开始和结束：

```
$ my_variable=Hello World

-bash: World: command not found

$
```
