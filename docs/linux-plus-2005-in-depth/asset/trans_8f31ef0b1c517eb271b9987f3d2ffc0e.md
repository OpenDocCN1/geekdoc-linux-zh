
# 环境变量

许多环境变量在 BASH shell 中默认已设置。要查看这些变量及其当前值的列表，您可以使用 **set** 命令，如下面的输出所示：

```
[root@server1 root]# set
BASH=/bin/bash
BASH_ENV=/root/.bashrc
BASH_VERSINFO=[0]="2" [1]="05b" [2]="0" [3]="1" [4]="release" [5]="1386-redhat-linux-gnu"
BASH_VERSION='2.05b.0(l) -release'
COLORS=/etc/DIR_COLORS.xterm
COLORTERM=gnome-terminal
COLUMNS=80
DESKTOP_SESSION=default
DESKTOP_STARTUP_ID=
DIRSTACK=()
DISPLAY=:0.0
EUID=0
GDMSESSION=default
GNOME_DESKTOP_SESSION_ID=Default
GNOME_KEYRING_SOCKET=/tmp/keyring-lvr68W/socket
GROUPS=()
GTK_RC_FILES=/etc/gtk/gtkrc:/root/.gtkrc-1.2-gnome2
G_BROKEN_FILENAMES=1
HISTFILE=/root/.bash_history
HISTFILESIZE=1000
HISTSIZE=1000
HOME=/root
HOSTNAME=server1
HOSTTYPE=i386
IFS=$' \t\n'
INPUTRC=/etc/inputrc
KDEDIR=/usr
LANG=en_US.UTF-8
LESSOPEN='|/usr/bin/lesspipe.sh %s'
LINES=24
LOGNAME=root
LS_COLORS='no=00:fi=00:di=00;34:ln=00;36:pi=40;33:so=00;35:bd=40;33;01:cd=40;33;01:or=01;05;37:41:mi=01;05;37;41:ex=00;32:*.cmd=00;32:*.exe=00;32:*.com=00;32:*.btm=00;32:*.bat=00;32:*.sh=00;32:*.*.csh=00;32:*.tar=00;31:*tgz=00;31:*aj=00;31:*tz=00;31:*.lzh=00;31:*zip=00;31:*.z=00:*.Z=00;31:*gz=00;31:*bz2=00;31:*bz=00;31:*taz=00;31:*rpm=00;31:*.cpio=00;31:*.jpg=00;35:*gif=00;35:*.bmp=00;35:*.xbm=00;35:*.xpm=00;35:*.png=00;35:*.tif=00;35: '
MACHTYPE=i386-redhat-linux-gnu
MAIL=/var/spool/mail/root
MAILCHECK=60
OPTERR=1
OPTIND=1
OSTYPE=linux-gnu
PATH=/usr/kerberos/sbin:/usr/kerberos/bin:/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/usr/X11R6/bin:/usr/java/j2sdk1.4.2_04/bin:/root/bin
PIPESTATUS=[\[0\]=\"0\"
PPID=3177
PROMPT_COMMAND=\"echo -ne "\"\[\d\]\[\h\]:\[\u\]@\[\H\]:\[\w\]\$\u\$\nPROMPT_COMMAND=\"echo -ne "\"\[\d\]\[\h\]:\[\u\]@\[\H\]$(hostname\$\nPS1=\"\[\e0\[00m \\[W\\\$\] \\[\
PS2=\"\nPS4=\"+
PWD=/root
QTDIR=/usr/lib/qt-3.3
SESSION_MANAGER=local/server1:/tmp/.ICE-unix/2868
SHELL=/bin/bash
SHELLOPTS=braceexpand:emacs:hashall:histexpand:history:interactive:comments:monitor
SHLVL=2
SSH_AGENT_PID=2931
SSH_ASKPASS=/usr/libexec/openssh/gnome-ssh-askpass
SSH_AUTH_SOCK=/tmp/ssh-DuFw2868/agent.2868
SUPPORTED=en_US:UTF-8:en_US:en
TERM=xterm
UID=0
USER=root
USERNAME=root
WINDOWID=41943116
XAUTHORITY=/root/.Xauthority
=\"set\"
\[root@server1 root\] \$
```

上述输出中显示的一些环境变量被那些需要有关系统信息的程序使用；OSTYPE（操作系统类型）和 SHELL（到 shell 的路径名）变量就是上述输出中的例子。其他变量用于设置用户的工作环境；其中最常见的包括以下几个：

- PS1——默认的 shell 提示符
- HOME——用户主目录的绝对路径名
- PWD——目录树中的当前工作目录
- PATH——用于搜索可执行程序的目录列表

PS1 变量表示 BASH shell 的提示符。要仅查看此变量的内容，您可以使用 **echo command** 并指定以 `$` shell 元字符为前缀的变量名，如下面的输出所示：

```
[root@server1 root]# echo $PS1
[\u@\h \W]$ 
[root@server1 root]# _
```

请注意，上述输出中使用了一种特殊记法来定义提示符：\u 表示用户名，\h 表示主机名，\W 表示当前目录的名称。可以通过导航 BASH shell 的手册页找到 BASH 记法的列表。

要更改变量的值，您只需指定变量名，紧接着跟一个等号（=）和新值。下面的输出演示了如何更改 PS1 变量的值。新提示符立即生效，允许用户输入命令。

```
[root@server1 root]# PS1="This is the new prompt: #"
This is the new prompt: # _
This is the new prompt: # date 
Fri May 27 10:15:56 EDT 2005 
This is the new prompt: # _
This is the new prompt: # who 
root pts/0 May 30 09:58 (3.0.0.2)
This is the new prompt: # _ 
This is the new prompt: # PS1="[\u@\h \W]#"
[root@server1 root]# _
```

HOME 变量被那些需要当前用户主目录路径名来存储或搜索文件的程序使用，因此不应更改它。如果 root 用户登录到系统，HOME 变量设置为 `/root`；或者，如果名为 user1 的用户登录到系统，HOME 变量设置为 `/home/user1`。请记住，波浪号 `~` 元字符表示当前用户的主目录；如下一所示，此元字符是 HOME 变量的指针：

```
[root@server1 root]# echo $HOME 
/root 
[root@server1 root]# echo ~ 
/root 
[root@server1 root]# HOME=/etc 
[root@server1 root]# echo $HOME 
/etc 
[root@server1 root]# echo ~ 
/etc 
[root@server1 root]# _
```

与 HOME 变量一样，PWD（打印工作目录）变量对用户环境至关重要，也不应更改。PWD 存储用户在目录树中的当前位置。它受 cd 命令的影响，并在需要识别当前目录时由 pwd 等其他命令使用。下面的输出演示了该变量如何工作：

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

PATH 变量是 BASH shell 中最重要的变量之一，因为它允许用户仅通过输入命令名称来执行命令。请记住，大多数命令由硬盘上可执行文件表示，这些文件通常组织在名为 bin 或 sbin 的目录中，遍布整个 Linux 目录树。要执行 ls 命令，您可以输入该文件的绝对或相对路径名（即 /bin/ls 或 ../bin/ls），或者简单地输入字母 "ls"，让系统搜索 PATH 变量中列出的目录以查找名为 ls 的命令。PATH 变量的示例内容显示在下面的输出中：

```
[root@server1 root]# echo $PATH
/usr/kerberos/sbin:/usr/kerberos/bin:/usr/local/sbin:/usr/local/bin:
/sbin:/bin:/usr/sbin:/usr/bin:/usr/X11R6/bin:/root/bin
[root@server1 root]#
```

从上述输出中，如果用户仅在命令提示符处输入命令 ls 并按下 Enter，shell 会注意到路径名中没有 / 字符，并继续在 /usr/kerberos/sbin 目录中查找文件 ls，然后是 /usr/kerberos/bin 目录、/usr/local/sbin 目录、/usr/local/bin 目录、/sbin 目录，最后是 /bin 目录，以找到 ls 可执行文件。如果在 PATH 变量中的任何目录中都没有找到 ls 文件，shell 会返回一条错误消息，如下所示，其中使用了拼写错误的命令：

```
[root@server1 root]# lss
bash: lss: command not found
[root@server1 root]#
```

因此，如果某个命令位于 PATH 变量中列出的目录内，您可以简单地在命令行输入该命令的名称来执行它，因为 shell 将能够找到文件系统中相应的可执行文件。直到本节为止，本书中使用的所有命令都位于 PATH 变量中列出的目录中。然而，如果可执行文件不在 PATH 变量中列出的目录中，用户必须指定该可执行文件的绝对或相对路径名。下面使用 /root 目录（一个未列在 PATH 变量中的目录）中的 myprogram 文件对此进行了示例说明：

```
[root@server1 root]# pwd
/root
[root@server1 root]# ls -F
Desktop/ myprogram*
[root@server1 root]# myprogram
bash: myprogram: command not found
[root@server1 root]# /root/myprogram
This is a sample program.
[root@server1 root]# ./myprogram
This is a sample program.
[root@server1 root]# cp myprogram /bin
[root@server1 root]# myprogram
This is a sample program.
[root@server1 root]# _
```

在上面的输出中，当 myprogram 可执行文件被复制到 /bin 目录后，用户只需输入其名称即可执行它，因为 /bin 目录列在 PATH 变量中。

表 8-3 列出了大多数 BASH shell 中使用的环境变量列表。

### 表 8-3 常见的 BASH 环境变量

| 变量 | 描述 |
| :--- | :--- |
| BASH | BASH shell 的完整路径 |
| BASH_VERSION | 当前 BASH shell 的版本 |
| DISPLAY | 用于将 X Windows 输出重定向到另一台计算机或设备的变量 |
| ENV | BASH 运行时配置文件的位置（通常为 ~/.bashrc） |
| EUID | 当前用户的有效 UID（用户 ID） |
| HISTFILE | 用于在 BASH shell 中存储之前输入命令的文件名（通常为 ~/.bash_history） |
| HISTFILESIZE | 注销时可以在 HISTFILE 中存储并在下次登录时使用的之前输入命令的数量；通常是 1000 条命令 |

