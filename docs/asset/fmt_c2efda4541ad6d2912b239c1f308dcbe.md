
`PATH`=`/bin:/usr/bin:/opt/bin:/usr/X11R6/bin:/usr/openbin/bin:/usr/TeX/bin:/usr/local/bin`

`umask` `022`

```bash
if [ id -gn = '$(id -un' ] && [ -id -u -ne 0 ]; then
  umask 022
fi

if [ -z "$SUID" ]; then
  UID=`id -u'
fi

if [ "$SUID" = 0 ]; then
  PATH=/usr/sbin:$PATH
else
  USER=`id -un'
  LOGNAME=$USER
fi

export PATH USER LOGNAME

hostname=`bin/hostname'

MAIL="var/spool/mail/$USER"

export HOSTNAME
```

```bash
if [ -n "$BASH_VERSION" ]; then
  # ... (省略部分)
fi
```

## 在 `.bashrc` 中初始化历史记录

Bash 启动可以保留你发布过的命令的历史列表。如果你想在启动时指定要包含的命令数量，可以使用 `HISTORYSIZE`。`.bashrc` 中的以下行会将历史记录数量设置为 100：

```
HISTORYSIZE=100
```

当你登录时，历史记录会包含你发布过的命令。以下是示例：

```
# history
```
（此处省略了原文中重复的命令列表，以符合注意事项不重复输出原文）

## 从历史记录列表中回溯

所有这些命令（`cp`、`more`、`find`）对应的编号。你可以使用 `!!` 重复上一个命令，使用 `!89` 重复第 89 条命令，或者使用 `!m` 重复以 "m" 开头的最后一个命令，这些在以下示例所示：

```
# !!
history
```
（此处省略了原文中重复的命令列表）

注意在这个示例中，命令编号 100 是上一个会话的退出命令。命令编号 101 是我在建立下一个会话后立即执行的 `history` 命令。

# 1456 第 22 章 KornShell、C Shell 和 Bash 简介

```bash
* ]
stty erase 'H'
;;
esac
fi
# 通用环境设置
#export GROUP TYPESETTER=latin
#export LC_TYPE=iso-8859-1
export LC_CHAR=latin
#export METAMAIL PAGER=less
HISTSIZE=100
alias which='type' -path
alias bh=history
alias j='jobs -1'
alias l='ls -F'
alias j1='ls -Alq'
alias pd=pushd
alias z='suspend
[root@nycaldi:/root]# 脚本执行于 1998年11月26 周四 19:39:51
```

表 22-8 包含了一些最常用的历史列表回溯命令：

# 表 22-8 从历史列表中回溯

| 命令 | 说明 | 示例 |
| --- | --- | --- |
| !N | 执行命令 N | !2 |
| !! | 执行上一个命令 | !! |
| !-N | 执行上一次执行的倒数第 个命令 | !-N |
| !str | 执行以 str 开头的上一个命令 | !c |
| !str? | 执行命令行中任何包含 str 的上一个命令 | !cat? |
| ![1]str2 | 在包含 str1 的上一个命令后追加 str2 | ![cd]/tmp |
| ^str1^str2^ | 在上一个命令中将 str1 替换为 str2 | ^cat^more^ |

# Bash 简介

### 命令行编辑

使用历史列表是查看和重新发送命令的极佳方法。Bash 还支持命令行编辑。你可以使用向上箭头键返回历史列表中的上一个命令。当你按下向上箭头键时，历史列表中的最后一个命令会出现在命令行上。每当你按下向上箭头键，你就会在历史列表中后移一个命令。当命令出现在命令行上时，你可以按“回车”键来执行该命令。你可以通过左、右箭头键移动到命令行的某一点并输入额外信息来修改命令，或者使用“退格（backspace）”和“删除（delete）”键从命令行中删除信息。

### .bashrc 中的别名 (Aliases)

别名（alias）是你为经常使用的命令或系列命令选择的名称。你可以将 `.bashrc` 文件作为存储别名的地方，并在每次登录时读取它们。在较早的 `.bashrc` 文件中，已经设置了七个别名。你可以在 `.bashrc` 文件中添加额外的别名，也可以在命令行提示符处定义别名，但这些别名会在注销时被清除。

以下是 `.bashrc` 文件中已经为设置好的别名列表，以及运行别名 I 和 II 的示例：

```bash
# alias
alias i='history'
alias j='jobs -l'
alias l='ls -F'
alias ll='ls -Aig'
alias pd='cd ~/github'
alias which='type -path'
alias z='suspend'
```

# 第 22 章 KornShell、C Shell 和 Bash 简介

```bash
# 1
ls -l .bash_history
.bashrc .fvwmrc.menus.prep .bashrc
.xinit/.login
XF86Config.bak .profile
typescript
# 11
total 44
-rw-r--r-- 1 root root 970 Nov 26 21:35 .bash_history
-rw-r--r-- 1 root root 674 Feb 5 1997 .bashrc
-rw-r--r-- 1 root root 602 Feb 5 1997 .bashrc
-rw-r--r-- 1 root root 14815 Feb 8 2009 .fvwmrc.menus.prep
-rw-r--r-- 1 root root 116 Feb 5 2009 .login
-rw-r--r-- 1 root root 234 Feb 5 2009 .profile
drwxr-xr-x 2 root root 1024 Feb 8 14:10 .xinit
-rw-r--r-- 1 root root 472 .XF86Config
-rw-r--r-- 1 root root 13875 Feb 8 2005 XF86Config.bak
drwxr-xr-x 2 root root 1024 Nov 26 19:41 book
drwxr-xr-x 5 root root 1024 Nov 14 18:12 lg
-rw-r--r-- 1 root root 0 Nov 26 21:35 typescript
```

![](img/6969df54e516231f8e64fd1177ac1127_1501_0.png)

这些都非常有用，但让我们设置自己的别名吧。我们想知道系统上有多少进程运行。我们将创建一个名为 "procs" 的别名来为我们完成此工作。`ps` 命令产生进程列表。我们将使用 `ps` 和管道 (`|`) 将此输出定向到带有 `-l` 选项的 `wc`，以告诉我们有多少行。管道 (`|`) 将 `ps` 的输出作为 `wc` 的输入。`wc` 命令产生输出并告诉我们行数。以下是运行别名后的输出示例：

```text
PID TTY STAT COMMAND
1234 ? S / bash
5678 ? S sleep 0
```
