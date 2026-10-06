

# Linux 命令行

```bash
BASH_VERSION=[0]="3" [1]="2" [2]="9" [3]="1" [4]="release"
[5]="1686-redhat-linux-gnu"
BASH_VERSION='3.2.9(1-release'
COLORS=${DIR_COLORS:-/etc/DIR_COLORS.xterm}
COLUMNS=80
CVS_RSH=ssh
DIRSTACK=()
UEID=500
GROUPS=()
G_BROKEN_FILENAMES=1
HISTFILE=/home/rich/.bash_history
HISTFILESIZE=1000
HISTSIZE=1000
HOME=/home/rich
HOSTNAME=testbox.localdomain
HOSTYPE=i686
IFS='\t\n'
INPUTRC=/etc/inputrc
LANG=en_US.UTF-8
LESSOPEN='|/usr/bin/lesspipe.sh %'
LINES=24
LOGNAME=rich
LS_COLORS='no=00:fi=00:di=00:dn=34:ln=36:mi=40:pi=43:so=00:bd=44;35:30;
01:cd=00:33:01:or=01:05:37:41:mi=01:05:37:ex=02:cmd=00:32;
*.exe=00:32:*.cmd=00:32:*.bat=00:32:*.sh=00:32;
csz=00:32:*.tar=00:31:.tgz.arj=00:31:*.tar.gz=00:31;
lzh=00:31:*.zip=00:31:*.z=00:31:*.gz=00:31:*.bz2=00:31;
*.bz2=00:31:*.tar.xz=00:31:.rpm=00:31:.cpio=00:31:*.jpg=00:35;
*.gif=00:35:*.bmp=00:35:*.x=00:35:*.png=00:35;
*.tif=00:35
MACHYPE=i686-redhat-linux-gnu
MAIL=/var/spool/mail/rich
MAILCHECK=60
OPTERR=1
OPTIND=1
OSTYPE=linux-gnu
PATH=/kerberos/bin:/usr/lib/ccache:/usr/local/bin:/bin:/usr/bin:
/home/rich/bin
PIPESTAS=[0]="0"
PID=3702
PROMPT_COMMAND=echoecho -ne '\u0033[${USER}@${HOSTNAME} \$${PWD#${HOME~}}\\$'; echo -ne '\u0027'
PS1='\u@\h \W\$ '
PS2='>$ '
PS4='+'
PWD=/home/rich
SHELL=/bin/bash
SHELLOPTS=braceexpand:emash:histext:history:
```

# 使用 Linux 环境变量

```bash
interactive-comments:monitor
SHLV=2
SSH_ASKPASS=/usr/libexec/openssh/gnome-ssh-askpass
SSH_CLIENT='192.168.1.2 1358 22'
SSH_CONNECTION='192.168.1.2 1358 192.168.1.4 22'
SSH_TTY=/dev/pts/0
TERM=xterm
UID=500
USER=rich
--H
consoleletype=pty
$
```

你会注意到，在 `set` 命令的输出中可以看到 `printenv` 命令显示的所有全局环境变量。现在出现了许多额外的环境变量。这些是本地环境变量。

# 设置环境变量

你可以直接从 bash shell 设置你自己的环境变量。本节将展示如何创建你自己的环境变量，并并在交互式 shell 或 shell 程序中引用它们。

# 设置本地环境变量

一旦你启动了 bash shell（或产生了一个 shell 脚本），你就可以创建在 shell 进程中可见的局部变量。你可以通过等号将变量赋值一个值来为环境变量分配数值或字符串值：

```bash
$ test=testing
$ echo $test
testing
$
```

这很简单！每当你需要引用 `test` 环境变量的值时，只需通过名称 `$test` 引用即可。

如果你需要分配一个包含空格的字符串值，你需要使用单引号来界定字符串的开始和结束：

```bash
$ test=testing a long string
-bash: a: command not found
$ test='testing a long string'
$ echo $test
testing a long string
$
```

# 第一部分 Linux 命令行

如果没有单引号，bash shell 会认为下一个字符是另一个要处理的命令。注意，对于我定义的本地环境变量，我使用了小写字母，而我们目前为止看到的系统环境变量都使用了大写字母。

这是 bash shell 中的标准约定。如果你创建了新的环境变量，建议（但不是必须）使用小写字母。这有助于将你的个人环境变量与大量的系统环境变量区分开。

> 注意：环境变量名、等号和值之间绝对不能有空格，这一点极其重要。如果你在赋值中放入任何空格，bash shell 将把该值解释为独立的命令：

```bash
$ test2 = test
$bash: test2: command not found
$
```

一旦你设置了本地环境变量，它在你的 shell 进程中的任何地方都可以使用。然而，如果你产生了另一个 shell，它在子 shell 中是不可用的：

```bash
$ bash
$ echo $test

$ exit
$ echo $test
testing a long string
$
```

在这个示例中，我启动了一个子 shell。如你所见，`test` 环境变量在子 shell 中是不可用的（它包含空值）。当我退出子 shell 并返回原始 shell 后，本地环境变量仍然可用。

同样，如果你在子进程中设置了本地环境变量，一旦你离开该进程，该本地环境变量就不再可用：

```bash
$ bash
$ test=testing
$ echo $test
testing
$
```

# 设置全局环境变量

一旦你设置了本地环境变量，它在你的 shell 进程中的任何地方都可以使用。然而，如果你产生了另一个 shell，它在子 shell 中是不可用的：

```bash
$ bash
$ echo $test

$ exit
$ echo $test
testing a long string
$
```

在这个示例中，我启动了一个子 shell。如你所见，`test` 环境变量在子 shell 中是不可用的（它包含空值）。当我退出子 shell 并返回原始 shell 后，本地环境变量仍然可用。

同样，如果你在子进程中设置了本地环境变量，一旦你离开该进程，该本地环境变量就不再可用：

```bash
$ bash
$ test=testing
$ echo $test
testing
$
```

# 删除环境变量

当然，如果你创建了全局环境变量，你是可以将其删除的。这是通过使用 `unset` 命令实现的：

```bash
$ echo $test
testing long string
$ unset test
$ echo $test
$
```

当在 `unset` 命令引用环境变量时，记住不要使用美元符号。处理全局变量时，情况会变得有点复杂。如果你在子进程中删除全局变量，它只影响该子进程。当你回到父 shell 时，全局变量仍然可用。

```bash
$ test=testing
$ export test
$ bash
$ echo $test
testing long string
$
```

# 默认环境变量

特定的环境变量由 bash 用来定义系统环境。你可以认为这些变量在你的 Linux 系统上已经设置。由于 bash shell 是原始 Unix Bourne shell 的派生版本，它包含了最初定义在那个 shell 中的环境变量。

表 5-1 显示了 bash 提供的与原始 Bourne shell 兼容的环境变量。

列表中最重要的环境变量是 PATH。当你在 shell命令行界面 (CLI) 输入命令时，shell 必须搜索系统以查找程序。PATH 环境变量定义了查找命令的目录。在我的 Linux 系统上，PATH 环境变量如下：

```bash
$ $PATH
/usr/kerberos/bin:/usr/lib/ccache:/usr/local/bin:/bin:/usr/bin:
home/rich/bin
```

这显示 shell 有六个目录查找命令。PATH 中的每个目录都用冒号分隔。PATH 的末尾没有指示目录列表的结束。你可以通过添加另一个冒号并添加新目录向 PATH 添加额外的目录。PATH 还显示了它查找命令的顺序。

