
命令之间的分号只是命令分隔符。这样做的效果相同：

```bash
VARIABLE_NAME=value
export VARIABLE_NAME
```

### 14.3.2 显示环境变量

显示环境变量再次与本地 shell 变量相同。以下是一些示例：

```
$ CONSOLE=tty; export CONSOLE
$ echo $CONSOLE
tty1
```

```
$ MYAPPS=/usr/local/application; export MYAPPS
$ echo $MYAPPS
/usr/local/application
```

要查看所有全局定义的环境变量，使用 `env` 命令。

```
$ env
HISTSIZE=1000
HOSTNAME=localhost.localdomain
LOGNAME=dave
MAIL=/var/spool/mail/root
TERM=vt100
HOSTTYPE=i386
PATH=/bin:/sbin:/usr/sbin:/usr/bin:/usr/X11R/bin:/root/bin:
CONSOLE=tty
HOME=/home/dave
ASD=sdf
SHELL=/bin/sh
PS1=$
USER=dave
```

### 14.3.3 清除环境变量

要清除变量，再次使用 `unset` 命令。

```
$ unset MYAPPS
$ echo $MYAPPS
```

## 14.3.4 内置 shell 变量

Bourne shell 预留了一些名称用于环境变量。你不能将这些变量名用于任何其他地方。它们通常在你的 `/etc/profile` 中设置，但并不总是如此，因此需要你来为它们设置一个值。以下是内置 shell 变量的列表。

### CDPATH

切换目录路径变量包含一系列由冒号分隔的路径名。它与 `cd` 命令配合使用。如果设置了 `CDPATH`，当执行 `cd` 时，会首先搜索 `CDPATH`。如果目录位于 `CDPATH` 内部，它将成为新的工作目录。这里有一个示例。

```
$ CDPATH=:home/dave/usr/local/apps; export CDPATH
```

如果你想执行

```
$ cd apps
```

那么 `cd` 命令将搜索 `CDPATH` 中提供的目录列表。如果找到，它将成为你的当前工作目录。

### EXINIT

`EXINIT` 变量保存了在使用 `vi` 编辑器时的初始化选项。例如，在使用 `vi` 时让所有行显示行号并将制表符设置为 10 个空格：

```
$ EXINIT='set nu tab=10'; export EXINIT
```

### HOME

`HOME` 目录通常位于 `passwd` 文件中倒数第二个字段中，是你存放所有个人文件的地方。设置后，你可以使用快捷方式回到家目录

```
$ HOME=/home/dave; export HOME
$ pwd
$ /usr/local
$ cd
$ pwd
$ /home/dave
```

你也可以使用

```
$ cd $HOME
```

### IFS

`IFS` 被 shell 用默认字段分隔符。内部字段分隔符可以设置为任何值，但默认通常设置为空格、换行符或制表符。`IFS` 在分离文件或变量中的字段非常有用。将 `IFS` 设置为冒号然后是 `PATH` 变量，将得到一个更可读的冒号分隔路径。

```
$ export IFS=
$ echo $PATH
/sbin /bin /usr/sbin /usr/bin /X11R6 /root/bin
```

要恢复其原始设置请使用：

```
$ IFS=<space><tab> export IFS
```

其中 `<space><tab>` 表示按下空格键和制表键。

### LOGNAME

此变量保存你的登录名。这本应该由默认设置，但如果你无法通过此命令设置它：

```
$ LOGNAME=whoami; export LOGNAME
$ echo $LOGNAME
dave
```

### MAIL

`MAIL` 变量保存你邮箱的路径和文件。默认情况下，这是 `/var/spool/mail/<login name>`。shell 会定期检查新邮件。如果你有邮件，它将显示在你的命令行上。如果你有不同的信箱路由，请通过 `MAIL` 设置它：

```
$ MAIL=/usr/mail/ave; export MAIL
```

### MAILCHECK

用于检查新邮件的 `MAILCHECK` 默认值为 60 秒。但如果你希望不那么频繁地检查邮件，例如每 2 分钟一次，请使用此命令：

```
$ MAILCHECK=120; export MAILCHECK
```

### MAILPATH

如果你有多个邮箱，请使用 `MAILPATH`。此变量将覆盖变量 `MAIL`：

```
$ MAILPATH=/var/spool/ave:/var/spool/admin; export MAILPATH
```

在上面的示例中，`MAIL` 现在将会检查 dave 和 admin 两个邮箱。

### PS2

```
$ PS2="@"; export PS2
$ for loop in *
@:
do
@:echo $loop
...
```

### SHELL

`SHELL` 包含你的默认 shell，通常从 `/etc/passwd` 获取，但如果你觉得需要使用另一个 shell，可以对其进行覆盖。

```
$ echo $SHELL
/bin/sh
```

### TERMINFO

终端初始化变量保存了终端配置文件的位置。通常位于 `/usr/lib/terminfo` 或 `/usr/share/terminfo` 中。

```
$ TERMINFO=/usr/lib/terminfo; export TERMINFO
```

### TERM

`TERM` 变量保存你的终端类型名称。这样做是为了让应用程序知道你的终端对屏幕和键盘理解什么类型的控制序列。最常见的终端类型有 vt100, vt220, vt220-8, wysec

```
$ TERM=vt100; export TERM
```

### TZ

时区变量保存时区值。这是系统管理员的工作。但由于你可能为你的 shell 更改它，这里有几个示例：

```
$ echo $TZ
GMT2EDT
```

返回的值意味着我们正在使用格林尼治标准时间，与 GMT 有 0 个本地时差，且夏令时间正在运行。

### 14.3.5 其他环境变量

还有其他预留的环境变量名；其他系统或命令应用程序会获取这些变量。以下是最常见的。记住这些值可能未被设置；由你来设置它们。

### EDITOR

将此变量设置为你最喜欢的编辑器。

```
$ EDITOR=vi; export EDITOR
```

### PWD

包含你当前目录的路径。通常使用 `cd` 命令设置。

### PAGER

保存屏幕分页器命令，例如 `pg`, `more`。当查看 `man` 页时，如果设置了此变量，系统将使用它。

```
$ PAGER='pg -f -p&d'; export PAGER
```

### MANPATH

保存系统中包含 `man` 页的目录。每个目录之间应该用冒号分隔。

```
$ MANPATH=/usr/apps/man:/usr/local/man; export MANPATH
```

### LPDEST 或 PRINTER

保存你的默认打印机名称。它可以避免在打印打印任务时手动指定打印机名称。

```
$ LPDEST=hp3si_systems
```

### 14.3.6 使用 set 命令

在你的 `$HOME/.profile` 中设置环境变量时，有另一种导出方法。使用带有 `-a` 选项的 `set` 命令。`set -a` 表示所有变量应立即导出。不要在 `/etc/profile` 中使用这种方法，只在你的 `$HOME/.profile` 文件中使用。

```
$ pg .profile
#.profile
set -a
MAIL=/usr/mail/${LOGNAME?:}
PATH=$PATH:$HOME:bin
#EDITOR=vi
TERM vt220
ADMIN=/usr/adm
PS1="hostname`
```

## 14.3.7 将变量导出到子进程

shell 新手面临的问题之一是关于将变量导出到子进程的概念。由于我们已经讨论了环境变量是如何工作的，现在让我们通过一个调用另一个脚本的脚本付诸实践，这在实际上创建了一个子进程。

下面是两个短脚本的列表。父脚本设置了一个名为 'film' 的变量，值为 'A Few Good Men'。它回显变量，然后调用另一个名为 'child' 的脚本。该脚本显示第一个脚本中的变量 film。在显示在屏幕之前，变量 film 的值被更改为 'Die Hard'。随后返回父脚本，然后再次显示该变量。

```
$ pg father
#!/bin/sh
# father script
film='A Few Good Men'
echo $film
./child
echo $film
```

```
$ pg child
#!/bin/sh
# child script
echo $film
film='Die Hard'
echo $film
```

## 14.4 位置变量

在本章的开头，我提到有四种变量，本地和环境，另外两种被认为是特殊的只读类型：位置变量和特殊变量。让我们来看看位置变量。

数字引用传递给脚本的每个参数。你可以传递任意数量的参数，但只能访问前九个参数，你可以使用 `shift` 命令来绕过这个限制。我们将在书的后面介绍 `shift` 的实际用法。

当你想要向 shell 脚本传递信息时，可以使用位置参数来访问这些信息。参数从 1 开始到每个结束；每个想要访问的参数都应该带有美元符号 `$` 前缀。第一个参数 0 保留用于存储实际的脚本名称；无论是否有参数，这个值都可以使用。

下表展示了如何访问每个参数。如果你想将以下字符串 ‘Did You See The Full Moon’ 传递给脚本：

| 参数 | 值 |
| :--- | :--- |
| `$0` | scriptname |
| `$1` | Did |
| `$2` | You |
| `$3` | See |
| `$4` | The |
| `$5` | Full |
| `$6` | Moon |

## 212 环境与 变量

| `$0` | `$1` | `$2` | `$3` | `$4` | `$5` | `$6` | `$7` | `$8` | `$9` |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 脚本 你看到满月亮吗 | | | | | | | | | |

### 14.4.1 在脚本中使用位置参数

让我们在下面的脚本中使用上面的示例。

```bash
$ param
#!/bin/sh
# param
echo "This is the script name": $0"
echo "This is the first parameter": $1"
echo "This is the second parameter": $2"
echo "This is the third parameter": $3"
echo "This is the fourth parameter": $4"
echo "This is the fifth parameter": $5"
echo "This is the sixth parameter": $6"
echo "This is the seventh parameter": $7"
echo "This is the eighth parameter": $8"
echo "This is the ninth parameter": $9"
```

```bash
$ param Did You See The Full Moon
This is the script name : ./param
This is the first parameter : Did
This is the second parameter : You
This is the third parameter : See
This is the fourth parameter : The
This is the fifth parameter : Full
This is the sixth parameter : Moon
This is the seventh parameter : :
This is the eighth parameter : :
This is the ninth parameter : :
```

我们只传递了六个参数，第七、八、第九参数是空的，这正是我们预期的。注意第一个参数提取了脚本名称。当你处理脚本返回的错误信息时，这可以非常好用。这里是另一个示例，仅返回脚本的名称。

```bash
$ param2
#!/bin/sh
echo "Hello world this is $0 calling"
```

```bash
$ param2
Hello world this is ./param2 calling
```

你会发现 `$0` 还会返回从当前目录的路径。如果你只需要脚本名称，可以在 `$0` 前面加上 `basename` 命令。这样你将只得到脚本名称。

```bash
$ param2
#!/bin/sh
echo "Hello world this is `basename $0` calling"
```

```bash
$ param2
Hello world this is param2 calling
```

### 14.4.2 向系统命令传递参数

你可以在脚本内部向系统命令传递参数。在下面的示例中，我们使用 `find` 命令，使用参数 `$1` 来指定我们要查找的文件。

```bash
$ findfile
#!/bin/sh
# findfile
find / -name $1 -print
```

```bash
$ datafile passwd
/etc/passwd
/etc/uucp/passwd
/usr/bin/passwd
```

这里另一个示例，以 `$1` 的形式将用户 ID 传递给 `grep`；`grep` 使用它来搜索任何 `passwd` 文件中该用户的全名。

```bash
$ who_is
#!/bin/sh
# who_is
grep $1 passwd | awk -F: {print $4}
```

```bash
$ who_is seany
Seany Post
```

### 14.4.3 特殊变量参数

现在我们知道如何访问和使用 shell 脚本参数了，那么关于它们的更多信息将会很有帮助。你确实需要对脚本如何处理这些参数有更多的控制。总共有一些特殊变量。让我们来看它们（见表 14.2）。

#### 表 14.2 传递给脚本的特殊 shell 变量。

| 变量 | 说明 |
| :--- | :--- |
| `$#` | 传递的参数个数 |
| `$*` | 将传递的所有参数显示在一个字符串中 |
| `$$` | 脚本运行的进程 ID |
| `$!` | 最后一个后台进程的 PID |
| `$@` | 每个参数都以带引号的形式显示，传递的参数类似于 `$*`，但每个参数都带引号 |
| `$-` | 当前 shell 的选项 |
| `$?` | 上一个命令的退出状态 |

既然我们已经知道如何访问和使用 shell 脚本参数了，那么关于它们的更多信息将会很有帮助。你确实需要对脚本如何处理这些参数有更多的控制。总共有一些特殊变量。让我们来看它们（见表 14.2）。

让我们修改脚本并替换一些特殊变量，然后带有不同的文本运行脚本。

```bash
$ param
#!/bin/sh
# param
echo "This is the script name": $0"
echo "This is the first parameter": $1"
echo "This is the second parameter": $2"
echo "This is the third parameter": $3"
echo "This is the fourth parameter": $4"
echo "This is the fifth parameter": $5"
echo "This is the sixth parameter": $6"
echo "This is the seventh parameter": $7"
echo "This is the eighth parameter": $8"
echo "This is the ninth parameter": $9"
echo "The number of arguments passed": "$@"
echo "Show all arguments": $*
echo "Show me process ID": $$
echo "Show me the arguments in quotes": "$@"
echo "Did my script go with any errors : $?"
```

```bash
$ param Merry Christmas Mr Lawrence
This is the script name : ../param
This is the first parameter : Merry
This is the second parameter : Christmas
This is the third parameter : Mr Lawrence
This is the fourth parameter : :
This is the fifth parameter : :
This is the sixth parameter : :
This is the seventh parameter : :
This is the eighth parameter : :
This is the ninth parameter : :
```

#### 位置变量参数

传递的参数个数 : 3
