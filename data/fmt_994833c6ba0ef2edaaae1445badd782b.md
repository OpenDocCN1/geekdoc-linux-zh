
> 注意：`awk` 和 `sed` 允许你在搜索模式中指定正则表达式。

# Shell 变量

BASH shell 在任何时刻的内存中都有几个变量。请记住，变量仅仅是包含可能被访问的信息的预留内存区域。Shell 中的大多数变量被称为环境变量，因为它们通常由系统设置，并包含系统和程序经常访问的信息。用户也可以创建自己的自定义变量。这些变量被称为用户定义变量。除了这两两种变量外，还有在执行命令以及创建文件和目录时非常有用的特殊变量。

# 第 8 章 使用 BASH SHE 操作

## 环境变量

许多环境变量由 BASH shell 设置。要查看这些变量的列表及其当前值，请使用 `set` 命令，如下输出所示：

```
[root@server1 root]# set
BASH=/bin/bash
BASH_ENV=/root/.bashrc
BASH_VERSION=([0]="2" [1]="0b" [2]="0" [3]="1" [4]="release" [5]="i386-redhat-linux-gnu")
BASH_VERSION="2.05b.0(1)-release"
COLORS=/etc/DIR_COLORS.xterm
COLORERTERM=gnome-terminal
COLUMNS=80
DESKTOP_SESSION=default
DESKTOP_STARTUP_ID=
DIRSTACK=()
DISPLAY=:0.0
EUID=0
GDMESSESSION=default
GNOME_DESKTOP_SESSION_ID=Default
GNOME_KEYRING_SOCKET=/tmp/keyring-1rv68W/socket
GROUPS=()
GTK_RC_FILES=/etc/gtkc/gtkrc=/root/.gtkrc-1.2-gnome2
G_BROKEN_FILENAMES=1
HISTFILE=/root/.bash_history
HISTFILESIZE=1000
HISTSIZE=1000
HOME=/root
HOSTNAME=server1
HOSTTYPE='\t\n'
IFS=' \t\n'
INPUT=/etc/inputproc
DIR=/usr
LANG=en_US.UTF-8
LESSOPEN=*/usr/bin/lesspipe.sh %%
LINES=24
LOGNAME=root
LS_COLORS=*no=00:fi=00:01:34:ln=00:36:pi=40:33:so=00:35:bd=40:33:01:cd=40:33:01:or=00;05:37:41:mi=0:01:05:37:41:ex=00:32*.cmd=00:32*.exe=00:32*.btm=00:32*.bat=00;32*.sh=00:32*.csh=00:32*.tar=00:31*.tgz=00:31*.arj=00:31*.tz=00:31*.*.=00:31*.zip=00:31*.Z=00:31*.Z=00:31*.gz=00:31*.bz=00:31*.bz=00:31*.tz=00:31*.rpm=00:31*.cpio=00:31*.jpg=00:35*.gif=00:35*.bmp=00:35*.xbm=00:35*.xpm=00:35*.png=00:35
MACHTYPE=redhat-linux-gnu
MAIL=/var/mail/root
MAILCHECK=
OPTIND=1
OSTYPE=linux
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/usr/X11/bin:/root/bin
STATUS=0
PPID=$$
PROMPT_COMMAND=echo -e "\n\[\u@h \W]\$ "
PS1='[\u@h \W]$ '
PS2=''
PS4='+'
PWD=/root
QTDIR=
SESSION_MANAGER=
SHELL=/bin/bash
SHELLOPTS=
SHLVL=2
SSH_AGENT_PID
SSH_ASKPASS=
SUPPORTED_METHODS
TERM=xterm
UID=0
USERNAME=root
WINDOWSIZE=
XAUTHORITY
```

上述输出中的某些环境变量被需要系统信息的程序使用；`OSTYPE` 和 `SHELL` 是上述输出中的示例。其他变量用于设置用户环境；其中最常见的包括：

- `PS1`—默认 shell 提示符
- `HOME`—用户目录的绝对路径
- `PWD`—当前工作目录
- `PATH`—搜索可执行程序的目录列表

## 使用 BASH SHELL 操作

`PS1` 变量代表 BASH shell 提示符。要查看此变量的内容，可以使用 `echo` 命令并由 `$` 符号指定变量名，如下输出所示：

```
[root@server1]# echo $PS1
[\u@h \W]$
```

注意上述输出中用于定义提示符的特殊符号：`\u` 表示用户名，`\h` 表示主机，`\W` 表示当前目录名。可以通过查看 BASH shell 的手册页找到符号列表。

要更改变量的值，只需指定变量名、等号（`=`）以及新值。下面的输出演示了如何更改 `PS1` 变量。新提示符立即生效并允许你使用 `type`：

```
[root@server1]# PS1="This is the new prompt:"
this is the new prompt: #
this is the new prompt: # date
Fri May 27 10:15:56 EDT 2005
this is the new prompt: #
this is the new prompt: # who
pts/0 May 30 09:58 (3.0.2)
this is the new prompt: #
this is the new prompt: # PS1="[\u@h \W]"
[root@server1]#
```

`HOME` 变量被需要当前用户目录路径来搜索文件的程序使用，因此不应更改。如果 root 用户登录系统，`HOME` 变量设置为 `/root`；或者，如果名为 `user1` 的用户登录系统，`HOME` 变量设置为 `/home/user1`。记住波浪符 `~` 表示当前用户的家目录，它指向 `HOME` 变量，如下：

```
[root@server1]# echo $HOME
/root
[root@server1]# echo ~
/root
[root@server1]# HOME=/etc
[root@server1]# echo $HOME
/etc
[root@server1]# echo ~
/etc
[root@server1]#
```

与 `HOME` 变量一样，`PWD`（打印工作目录）变量对用户环境至关重要且不应更改。`PWD` 存储用户所在的目录。它受 `cd` 命令的影响，并在需要识别当前目录时被其他命令使用。下面的输出演示了该变量如何工作：

```
[root@server1 root]# pwd
/root
[root@server1 root]# echo $PWD
/root
[root@server1 root]# cd /etc
[root@server1 etc]# pwd
/etc
[root@server1 root]# echo $PWD
/etc
[root@server1 root]#
```

`PATH` 变量是 BASH shell 中最重要的变量之一，它允许用户通过输入命令名来执行命令。请记住，大多数命令由硬盘上的可执行文件表示，这些文件通常组织在 Linux 目录中名为 `bin` 或 `sbin` 的目录下。要执行 `ls` 命令，你可以输入绝对或相对路径（例如 `/bin/ls` 或 `../bin/ls`），或者只需输入 "`ls`" 并允许系统搜索 `PATH` 变量列出的目录。`PATH` 变量的示例内容如下输出所示：

```
[root@server1 root]# echo $PATH
/usr/kerberos/sbin:/usr/kerberos/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/usr/X11/bin:/root/bin
[root@server1]#
```

从上述输出可以看出，如果用户在命令提示符处输入命令并按回车，shell 会注意到路径中没有 `/`，并依次在 `/usr/kerberos/sbin` 目录、`/usr/kerberos/bin` 目录、`/usr/local/sbin` 目录、`/usr/local/bin` 目录、`/usr/sbin` 目录，然后 `/bin` 目录中搜索文件，直到找到可执行文件。如果在 `PATH` 变量的任何目录中未找到 `ls`，shell 将返回错误信息，如下所示（拼写错误的命令）：

```
[root@server1 root]# ls
bash: ls: command not found
[root@server1 root]#
```

因此，如果命令位于 `PATH` 变量列出的目录中，你只需在命令行上输入命令名即可执行它，因为 shell 能够在文件系统中找到相应的可执行文件。本书直到本节为止使用的所有命令都位于 `PATH` 变量列出的目录中。如何-

如果可执行文件不在 `PATH` 变量列出的目录中，用户必须指定可执行文件的绝对路径或相对路径。下面的示例展示了使用 `/root` 目录下的 `myprogram` 文件（该目录未列在 `PATH` 变量列表中）：

```
[root@server1]# pwd
/root
[root@server1]# ls -F
Desktop/ myprogram/
[root@server1]# myprogram
bash: myprogram: command not found
[root@server1]# /root/myprogram
This is a sample program.
[root@server1]# .myprogram
This is a sample program.
[root@server1]# cp myprogram /bin
[root@server1]# myprogram
This is a sample program.
[root@server1]# _
```

在上述输出中，将 `myprogram` 可执行文件复制到 `/bin` 目录后，用户只需输入其名称即可执行它，因为 `/bin` 目录已列在 `PATH` 变量中。

### 表 8-3 常见的 BASH 环境变量

| 变量 |  |

| :--- | :--- |

| `BASH` | BASH shell 的完整路径 |

| `BASH_VERSION` | 当前 BASH shell 的版本 |

| `DISPLAY` | 用于将 X Windows 输出重定向到另一台计算机或设备的变量 |

| `ENV` | BASH 运行时配置文件的位置（通常为 `~/.bashrc`） |

| `EUID` | 当前用户的有效 UID（用户 ID） |

| `HISTFILE` | 用于存储 BASH shell 中之前输入命令的字体（通常为 `~/.bash_history`） |

| `HISTFILESIZE` | 退出登录时存储在 `HISTFILE` 中以便在下次登录时使用的之前输入的命令数；通常为 1000 条命令 |

### 表 8-3 常见的 BASH 环境变量（续表）

| 变量 | 描述 |

| :--- | :--- |

| `HISTSIZE` | 在当前登录会话期间将存储在内存中的之前输入命令的条数；通常为 1000 条命令 |

| `HOME` | 当前用户主目录的绝对路径 |

| `HOSTNAME` | Linux 系统的主机名 |

| `LOGNAME` | 用户登录 shell 时的用户名 |

| `MAIL` | 邮箱文件的位置（存储电子邮件的地方） |

| `OLDPWD` | 最近一次之前的工作目录 |

| `OSTYPE` | 当前操作系统 |

| `PATH` | 在没有包含 `/` 字符的绝对或相对路径时，搜索可执行程序文件的目录 |

| `PS1` | 当前提示符 |

| `PWD` | 当前工作目录 |

| `RANDOM` | 访问时创建随机数的变量 |

| `SHELL` | 当前 shell 的绝对路径 |

| `TERM` | 用于确定终端设置的变量；在较新的 Linux 系统上通常设置为 "`linux`" 或 "`xterm`"，在较旧的 Linux 系统上设置为 "`console`" |

| `TERMCAP` | 用于确定使用 TERMC 数据库 (`/etc/termcap`) 的旧系统上终端设置的变量 |

## 用户定义变量

可以使用之前讨论过的相同方法设置任何变量，以更改现有环境变量的内容。要做到这一点，只需指定变量名（称为**变量标识符**），紧接着是等号 (`=`) 和新内容。在创建新变量时，注意以下变量标识符的特征很重要：

- 它们可以包含字母数字（0–9, A–Z, a–z）、连字符 (`-`) 或下划线 (`_`)。
- 它们不能以数字开头。
- 为了遵循惯例，它们通常大大写（例如 `HOME`、`PATH` 等）。

### 第 8 章 使用 BASH SHELL

要创建一个内容为 "`This is a sample variable`" 的变量 `MYVAR` 并显示其内容，可以使用以下命令：

```
[root@server1]# MYVAR="This is a sample variable"
[root@server1]# echo $MYVAR
This is a sample variable
[root@server1]# _
```

上述命令创建了一个当前 shell 可用的变量，子shell 由当前 shell 创建。当前 shell 创建的变量对于在子shell 中运行的命令不可用。因此，如果用户在编辑器等程序中创建一个变量，该变量应该通过 `export` 命令导出到所有子shell，以确保启动当前 shell 的程序能够访问该变量。并不是所有的环境变量都可以 `set` 命令列出；用户定义的变量也列在列表中。同样，要查看 shell 中所有导出的环境变量和用户定义的变量，可以使用 `env` 命令。由于 `set` 和 `env` 命令的输出通常很大，为了只显示某些行，可以执行以下命令：

```
[root@server1]# set | grep MYVAR
MYVAR='This is a sample variable.'
[root@server1]# env | grep MYVAR
[root@server1]# export MYVAR
MYVAR=This is a sample variable.
[root@server1]# _
```

并不是环境变量都导出到子shell；`PS1` 是一个不需要导出的变量示例。然而，导出用户定义变量很好，因为它们可能会被子shell 中的进程使用。因此，要创建一个名为 `MYVAR2` 的用户定义变量，可以单独使用 `export` 命令，如下：

```
[root@server1]# export MYVAR2="This is another sample variable"
[root@server1]# set | grep MYVAR2
MYVAR2='This is another sample variable.'
MYroot2
[root@server1 MY env |
 MY2
2VAR2= is another1 variable.
```

## 其他变量

其他变量不通过 `set` 或 `env` 命令显示；这些变量在 shell 中执行特殊功能。本文使用的 `UMASK` 变量是 BASH shell 中执行特殊函数的示例，必须由 `umask` 命令设置。此外回，当你输入 `cp` 命令时，你实际上是在运行指向 `cp -i` 命令的别名。别名是存储在 shell 中的命令的快捷方式。要创建多个命令的别名，可以使用：

```
[root@server1]# alias mf="date;who"
[root@server1]# alias
alias cp='cp -i'
alias dw='date;who'
alias l.*='ls -d --color=tty'
alias ll='ls --color=tty'
alias ls='ls --color=tty'
alias mc='/usr/share/mc/bin-wrapper.sh'
alias m*='mount -t ext2 /floppy'
alias mv='mv -i'
alias rm='rm -i'
alias vi='vim'
alias which='alias /bin/which --tty-only --read-alias --show-dot --tide'
[root@server1]# _
```

现在，你需要运行别名来查看，如下输出所示：

```
[root@server1]# mf
Sun Jun 5 10:25:45 EDT 2005
pts/0 Jun 1 08:44 (3.0.2)
root pts/1 Jun 1 11:54 (:0)
```

你也可以创建多个命令的别名，只要它们由第 2 章引入的元字符分隔。要创建一个运行 `date` 命令后接 `who` 命令的别名 `dw`，你可以执行以下操作：
