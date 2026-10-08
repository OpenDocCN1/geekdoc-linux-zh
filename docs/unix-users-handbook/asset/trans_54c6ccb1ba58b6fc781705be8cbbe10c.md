

该程序获取最后两个输入的颜色，并将它们赋给 *color2*。因此，你必须小心用户可能通过 read 命令输入的内容，以及你如何将这些信息映射到变量中。

你可能已经知道，**read** 有一个内置变量称为 *REPLY*。使用 *REPLY* 时，一行输入会被赋给变量 *REPLY*。我通常不经常使用它，因为我不喜欢将任何事情交给运气。我通常会显式地命名一个用于接收输入的变量。示例展示了 **readtest1** 的列表和运行过程，其中包含一行仅由 **read** 命令组成，其响应被赋给 *REPLY*：

![](img/75f39fc91296b889c0653851accdfd46_731_0.png)

```bash
marty $ cat readtest1
#!/bin/ksh
# program: readtest
echo "Please enter your name: \c"     # the \c leaves cursor on
                                        # this line.
read name         # I have no $ because we are doing an assignment
                  # of whatever the user enters into name.

echo "Hello, $name"

echo "Please enter your two favorite colors: \c"
read color1 color2        # first word entered goes into color1
                          # remainder of line goes into color2

echo "You entered $color2 and $color1"
echo "Where are you from?"
read                      # read response into $REPLY
echo "I'm sure $REPLY is great"

marty $ readtest1
Please enter your name: MARTY
Hello, MARTY
Please enter your two favorite colors: RED BLUE
You entered BLUE and RED
Where are you from?
MANY DIFFERENT PLACES
I'm sure MANY DIFFERENT PLACES is great
marty $
```

在这个例子中你可以看到，我输入的响应“MANY DIFFERENT PLACES”确实被读入到 *REPLY* 中。

虽然在本章中广泛使用了 **echo**，但你可能会看到使用 **print** 来在屏幕上显示行。

## Shell 程序的参数

Shell 程序可以像任何常规命令一样具有命令行参数。调用 Shell 程序时使用的命令行参数存储在一组特殊变量中。这些变量被称为位置参数。

命令行上的前十个词在 Shell 程序中可以通过特殊变量 **$0-$9** 直接访问。它们的工作方式如下：

- $0	命令名称
- $1	第一个参数
- $2	第二个参数
- $3	.
- .
- .
- $9	第九个参数

如果你不确定程序运行时可能接收多少个命令行参数，还有两个变量可以帮助：

- $#	命令行参数的数量
- $*	所有命令行参数的空格分隔列表（不包括命令名称）

变量 **$*** 通常与 **for** 循环（稍后将解释）一起使用，以处理具有任意数量参数的 shell 脚本命令行。

现在让我们拿之前处理过的 **myll** 进行修改，使其生成我们在运行程序时指定的目录的长列表。图 11-1 显示了修改后的 **myll**。

```bash
#!/bin/ksh
# This is a simple shell program that takes one command line
# argument (a directory name) and then displays the full pathname
# of that directory before doing a long file listing (ll) on
# it.
#
# The script name is myll
cd $1
echo "Long listing of the $(pwd) directory:"
echo
ls -l
```

图 11-1 **myll** Shell 程序

如果我们使用目录名运行 **myll**，脚本会更改目录，回显包含完整路径名的消息（注意命令替换），然后执行 **ls -l** 命令。

请注意，**myll** 程序中的 **cd** 只会更改脚本的工作目录；它不会影响我们从其中运行 **myll** 的 shell 的工作目录。

![](img/75f39fc91296b889c0653851accdfd46_733_0.png)

```bash
marty $ myll /tmp
Long listing of the /tmp directory:
total 2384
-rw-r--r--     1 root sys 265228 Feb 22 15:21 dtdbcache_:0
-rw-r--r--     1 root sys 70829 Feb 23 10:44 g
-rw-r--r--     1 root sys 13642 Feb 23 10:48 i
-rw-rw-rw-     1 root root 14071 May 24 06:10 license_log
-rw-x--x-r-x   1 chrish users 317 Apr 20 17:38 ls
-rw-rw-r--     1 root sys 4441 Mar 25 14:37 mwaps7454
-rw-rw-rw-  1 anne users 4341 May 20 13:56 ps23974
-rw-r--r--     1 root users 4218 Apr 14 11:17 ps3358
-rw-r--r--     1 root users 4763 Feb 24 07:23 ps6465
-rw-r--r--     1 root sys 4446 Mar 25 14:30 ps7036
-rw-rw-r--     1 root sys 4442 Mar 25 14:35 ps7138
-rw-rw-r--     1 root sys 4446 Mar 25 14:35 ps7215
-rw-rw-rw-  1 root sys 4498 Mar 25 14:36 ps7342
-rw-rw-r-- 1 root sys 4446 Mar 25 14:38 ps7622
-rw-rw-r-- 1 root sys 4615 Mar 25 15:30 ps7812
-rw-rw-r-- 1 root sys 5728 Feb 18 11:09 ps_data
-rw-r--r-- 1 root sys 0 Apr 26 10:50 sh20890.1
-rw-r--r-- 1 root sys 0 Apr 26 10:50 sh20891.1
-rw-f--r-- 1 root sys 0 Apr 26 10:51 sh20978.1
-rw-f--r-- 1 root sys 0 Apr 26 10:51 sh20979.1
-rw-f--r-- 1 chrisb users 5325 Mar 26 13:42 sman_9664
-rw-fw-r-- 1 root sys 295996 Mar 1 10:15 ups_data
drwx----- 2 root other 69 Mar 9 11:37 whatis.11526
drwx----- 2 root other 69 Mar 9 11:37 whatis.11686
drwx----- 2 root other 69 Mar 9 11:38 whatis.11853
drwx----- 2 root other 69 Mar 9 11:38 whatis.12014
-rw-f--r-- 1 root sys 354221 Feb 23 10:49 x
-rw-f--r-- 1 chrisb users 0 Feb 23 14:39 xx
martyp $
```

在这种情况下，我们可以不给 **myll** 任何参数，它仍能正常工作。如果我们不提供任何命令行参数，那么 $1 将为空，因此 **cd** 之后的命令行上没有任何内容。这将使 **cd** 将我们带回到主目录，并在那里执行长列表。

![](img/75f39fc91296b889c0653851accdfd46_734_0.png)

如果我们提供多个参数，只有第一个会被使用，其余的被忽略。

如果我们使用命令行参数，它*必须*是一个目录名；否则 **cd** 命令会失败，脚本会以“bad directory”错误消息终止。稍后，我将展示如何测试有效的目录名和文件名，以便你可以规避潜在错误。

可以使用更复杂的示例来构建 **ps** 命令的新版本。以下是两个使用命令行参数和命令替换来帮助你进行进程管理的示例。

![](img/75f39fc91296b889c0653851accdfd46_734_1.png)

图 11-2 中的 **psg** shell 程序对于在通常很长的进程状态列表中搜索仅某些命令或用户进程非常有用。这些示例使用了 **grep**。**grep** 查找包含你所搜索模式的所有行。

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

图 11-2 **psg** Shell 程序

下面是 **psg** 运行时的样子。在这个例子中，我们想要查看系统中运行的所有 Korn shell。

| martyp $ psg ksh |
|---|
| UID PID PPID C STIME TTY TIME CMD |
| root 2954 2936 0 Feb 22 ? 0:01 /bin/ksh /usr/dt/bin/Xsession |
| root 3002 2999 0 Feb 22 pts/2 0:01 -ksh -c unset DT; DISPLAYg |
| root 3067 1 0 Feb 22 ? 0:00 /bin/ksh /usr/dt/bin/sdtoolcheckm |
| jnola 11516 11514 0 May 11 pts/3 0:01 -ksh |
| martyp 29291 29289 0 09:30:04 pts/4 0:02 -ksh |

![](img/75f39fc91296b889c0653851accdfd46_735_1.png)

此程序也可以用于查找终端、进程 ID、父进程 ID、启动日期以及 **ps** 中的其他任何信息。

作为用户，你可能会启动一些希望停止的进程。例如，你可能启动了一个不会显示在你的显示器上的应用程序。你可以使用 **psg** 识别该进程，然后使用下一个程序停止该进程，前提是你有权停止该进程。

图 11-3 中的 **gkill** shell 程序在 **ps -ef** 列表中搜索模式（就像 **psg** 那样）；然后它终止所有列出的进程。

