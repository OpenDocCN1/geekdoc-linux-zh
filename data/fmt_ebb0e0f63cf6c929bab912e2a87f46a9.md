
```
sys1 7: ls -al
total 10
drwxr-x---   2 martyp2    users      96 May  5 09:34 .
drwxr-xr-x  10 root       root      1024 May  5 10:38 ..
-rw-r--r--   1 martyp2    users      814 May  5 09:34 .cshrc
-rw-r--r--   1 martyp2    users      347 May  5 09:34 .exrc
-rw-r--r--   1 martyp2    users      341 May  5 09:34 .login
-rw-r--r--   1 martyp2    users      446 May  5 09:34 .profile
sys1 8:
```

C shell 提示符由系统名称（`sys1`）后跟命令编号和冒号组成。我稍后将介绍提示符。

`ls -al` 在此用户区域显示了两个与 C shell 相关的文件：

`.cshrc` 和 `.login`

图 7-1 是 `.cshrc` 的内容。

![](img/75f39fc91296b889c0653851accdfd46_396_0.png)

```
# Default user .cshrc file (/usr/bin/csh initialization).

# Usage: Copy this file to a user's home directory and edit it to
# customize it to taste. It is run by csh each time it starts up.

# Set up default command search path:
#
# (For security, this default is a minimal set.)
	set path=($path)

# Set up C shell environment:

if ($?prompt) then	# shell is interactive.
	set history=20		# previous commands to remember.
	set savehist=20		# number to save across sessions.
	set system=`hostname`	# name of this system.
	set prompt = "$system \!: "	# command prompt.

# Sample alias:

alias	status	`(date; bdf)`

# More sample aliases:

alias	d	dirs
alias	pd	pushd
alias	pd2	pushd +2
alias	po	popd
alias	m	more
endif
```

**图 7-1** `.cshrc` 示例

图 7-2 显示了 `.login` 的内容。

```
# @(#) $Revision: 72.3 $

# Default user .login file ( /usr/bin/csh initialization )

# Set up the default search paths:
set path=($path)

#set up the terminal
eval `tset -s -Q -m ':?hp'`
stty erase "^H" kill "^U" intr "^C" eof "^D" susp "^Z" hupcl ixon ixoff tostop
tabs

# Set up shell environment:
set nocllobber
set history=20
```

**图 7-2** `.login` 示例

### `.cshrc` 文件

登录后发生的事件序列因 UNIX 系统而异。在许多系统中，C shell 首先读取并执行 `.cshrc`。您可以修改 `.cshrc` 文件以指定您希望使用的命令行提示符，初始化历史记录列表，并定义别名。

接下来的部分描述了图 7-1 中所示的 `.cshrc` 文件定义这些内容的方式。让我们先快速看一下下一节中的 `.login` 文件。

### `.login` 文件

在许多 UNIX 系统中，`.login` 文件在 `.cshrc` 文件之后读取。示例中只有两个与设置相关的问题。第一个是 `tset` 命令，它设置 `TERM` 环境变量。`tset` 前面的 `eval` 意味着 C shell 执行 `tset` 及其参数而不创建子进程。这允许 `tset` 在当前 shell 中设置环境变量，而不是在子 shell 中设置，后者是没有用的。`stty` 命令用于设置终端 I/O 选项。两个 `set` 命令用于定义 shell 变量，我稍后将描述这些变量。`noclobber` 不允许重定向覆盖现有文件。如果您尝试覆盖现有文件，如下面的 `/tmp/processes`，您将收到文件已存在的消息：

![](img/75f39fc91296b889c0653851accdfd46_399_0.png)

```
sys1 1: ps -ef > /tmp/processes
/tmp/processes: File exists
```

`>` 表示获取 `ps` 的输出，而不是将其写入您的屏幕，而是将其写入 `/tmp/processes`。然而，由于 `/tmp/processes` 已经存在并且设置了名为 `noclobber` 的环境变量，因此 `/tmp/processes` 文件不会被 `ps -ef` 的输出覆盖。如果设置了 `noclobber`，则重定向输出到此文件将不会发生。这是一种防止现有文件被意外覆盖的有用技术。您会发现许多形式的重定向非常有用。重定向在本章后面介绍。

### 在 `.cshrc` 中初始化历史列表

C shell 可以保留您已发出的命令历史记录。如果您希望重新发出某条命令或查看之前发出的命令，可以使用历史列表。

发出的命令通过编号来引用，因此您希望系统名称后出现一个编号。`.cshrc` 中的以下行提供了系统名称后的一个编号：

```
set prompt = "$system \!: "
sys1 1:
```

我们稍后将讨论 shell 和环境变量，但现阶段只需知道 `$system` 对应系统名称 `sys1` 即可。

您可以指定在发出 `history` 命令时希望保存和查看的先前已发出命令的数量。`.cshrc` 中的以下行将历史列表设置为 20：

```
set history = 20
```

当发出 `history` 命令时，会显示最近发出的 20 条命令。

`savehist` 变量允许您在注销后保存指定数量的历史命令。默认情况下，当您注销时，历史列表会被清除。此变量的值为 20，这意味着在下一次登录时，将保存前一个会话的 20 条命令。

### 命令行历史

您可以通过多种方式查看历史列表。首先，让我们通过简单地发出 `history` 命令来查看最后 20 条命令：

```
sys1 23: history
        4 whoami
        5 pwd
        6 find / -name login -print &
        7 hostname
        8 who
        9 more /etc/passwd
       10 history
       11 history 5
       12 echo $PATH
       13 more .login
       14 cat .login
       15 exit
       16 exit
       17 history -h
       18 pwd
       19 whoami
       20 cd /tmp
       21 cat database.log
       22 cd
       23 history
sys1 24:
```

我们也可以在打印历史列表时省略行号，如下面的示例所示：

```
sys1 24: history -h
pwd
find / -name login -print &
hostname
who
more /etc/passwd
history
history 5
echo $PATH
more .login
cat .login
exit
exit
history -h
pwd
whoami
cd /tmp
cat database.log
cd
history
history -h
sys1 25:
```

接下来，让我们按反序打印历史列表：
