
大多数 UNIX 变体允许你在几个 shell 中进行选择。我所使用的基于 Linux 的 UNIX 操作系统将 `Bash` 配置为默认 shell。`Bash` 拥有其他 shell 的许多优良特性，实际上它的名字来源于 Bourne Again SHell，这明显表明它至少拥有 Bourne shell 的一些特性。`Bash` 与其他 shell 相似，因为它提供了 UNIX 的用户界面。你可以按以下三种方式使用 `Bash` shell：

- 在命令行上交互式输入命令。
- 将常用执行的命令集组合到命令文件中，你可以通过键入文件名来执行它们。
- 使用 shell 的结构化编程技术创建 `Bash` shell 程序。

这三种技术按你很可能使用它们的顺序列出。首先，你登录并使用交互式命令。然后，你组合常用命令并用单个命令执行它们。最后，你可能想要创建复杂的 shell 脚本。

因此，按照列出的顺序描述 `Bash` shell 的这些方面。`Bash` shell 的命令文件和编程方面作为“Shell 编程”章节的一部分进行介绍。`Bash` 与 `KornShell` 非常相似，`KornShell` 是在 shell 编程章节中使用的 shell。因此，你也可以将 shell 编程章节作为使用 `Bash` 进行编程的入门介绍。但是请记住，使用一种 shell 与另一种 shell 进行编程时，总会存在差异。

### 发出命令

登录系统后执行的第一项活动就是在提示符处发出命令。你可能希望立即发出的一个命令是 `ls -al`。以下是我在以 root 身份登录并执行此命令以检查当前工作目录并生成所有文件的长列表时在我的系统上看到的内容：

![](img/75f39fc91296b889c0653851accdfd46_292_0.png)

```
#### pwd
# ls -al
total 46
drwxr-xr-x  5 root  root       1024 Nov 26 19:40 .
drwxr-xr-x 20 root  root       1024 Nov  8 20:10 ..
-rw-r--r--  1 root  root        964 Nov 26 19:40 .bash_history
-rw-r--r--  1 root  root        674 Feb  5 1997 .bashrc
-rw-r--r--  1 root  root        602 Feb  5 1997 .cshrc
-rw-r--r--  1 root  root       14815 Nov  8 20:09 .fvwmrc.menu$.$prep
-rw-r--r--  1 root  root        116 Feb  5 1997 .login
-rw-r--r--  1 root  root        234 Feb  5 1997 .profile
drwxr-xr-x  2 root  root       1024 Nov  8 14:10 .seyon
dr-xr-xr-x  1 root  root       4276 Nov  8 20:09 XF86Config
dr-xr-xr-x  1 root  root       13875 Nov  8 20:05 XF86Config.bak
drwxrwxrwx  2 root  root       1024 Nov 26 19:40 book
drwxr-xr-x  5 root  root       1024 Nov 14 18:12 lg
-rw-r--r--  1 root  root           0 Nov 26 19:40 typescript
#
```

![](img/75f39fc91296b889c0653851accdfd46_292_1.png)

在所有文件的长列表中生成的文件包含一个名为 `.bashrc` 的 `Bash` 启动文件。以下显示了 `.bashrc` 文件的内容：

![](img/75f39fc91296b889c0653851accdfd46_292_2.png)

```
# cat .bashrc
# ~/.bashrc --
# The individual per-interactive-shell startup file for bash
. /etc/profile
# try solve this tedious 'Backspace vs. Delete' problem...
if [ -z "$TERM" ]; then
echo ".bashrc: TERM empty: this shouldn't happen!" 1>&2
echo " Please contact 'support@lst.de'" 1>&2
else
case $TERM in
linux*)
stty erase '^?'
;;
*)
stty erase '^H'
;;
esac
fi

# general environment settings
#export GROFF_TYPESETTER=latin1
#export LC_CTYPE=iso-8859-1
export LESSCHARSET=latin1
#export METAMAIL_PAGER=less

HISTSIZE=100

alias which='type -path'
alias h=history
alias j="jobs -l"
alias l="ls -Fax"
alias ll="ls -Alg"
alias pd=pushd
alias z=suspend
#
```

![](img/75f39fc91296b889c0653851accdfd46_293_0.png)

`.bashrc` 文件中有一些有趣的内容。其中包括一个 `HISTSIZE` 的值，我们稍后会详细介绍，以及一组别名。这些别名是长命令的“快捷键”。例如，当我发出 `ll` 命令时，我实际上是在发出 `ls -Alg` 命令。

我可能会执行早期长列表中显示的本地 `.profile`，以及 `/etc/profile`。`/etc/profile` 通常执行为登录系统的所有用户进行的设置。以下是 `/etc/profile` 的列表：

![](img/75f39fc91296b889c0653851accdfd46_293_1.png)

```
# cat /etc/profile
# /etc/profile
# System wide environment and startup programs
# Functions and aliases go in $HOME/.bashrc

PATH="/bin:/usr/bin:/opt/bin:/usr/X11R6/bin:/usr/openwin/bin:/usr/TeX/bin:/usr/local/bin"

umask 022

if [ `id -gn` = `id -un` ] && [ `id -u` ! = 0 ]; then
umask 002
fi

if [ -z "$UID" ]; then
UID=`id -u`
fi

if [ "$UID" = 0 ]; then
PATH=/sbin:/usr/sbin:$PATH
else
PATH=$PATH:
fi
USER=`id -un`
LOGNAME=$USER

export PATH USER LOGNAME

HOSTNAME=`/bin/hostname`
MAIL="/var/spool/mail/$USER"

export HOSTNAME MAIL

if [ -n "$BASH_VERSION" ]; then
# (aliases now in $HOME/.bashrc, resp. /etc/skel/.bashrc)
export PS1="\u@\h \w\$ "
export HISTSIZE=100
fi
#
```

我们还将介绍 `/etc/profile` 中的一些内容。

### 在 `.bashrc` 中初始化历史记录列表

`Bash` shell 可以保存你发出的命令的历史记录列表。如果你希望重新发出某条命令或查看你之前发出的命令，你可以使用历史记录列表。

你可以指定要包含在历史记录列表中的任意数量的命令。`.bashrc` 中的以下行将历史记录列表设置为 100：

```
HISTSIZE=100
```

历史记录列表中将保存一百条命令。当你注销时，你发出的最后 100 条命令会存储在历史记录列表中。下次登录时，你可以查看这 100 条命令；然而，当你发出命令时，最旧的命令会从历史记录列表中移除。以下示例展示了这一事实：
