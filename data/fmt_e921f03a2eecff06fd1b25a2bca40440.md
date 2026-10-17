
```
$ PS1="Please enter a command: "
Please enter a command: export PS1
Please enter a command: ls
mydata /reports
Please enter a command:
```

## 第12 章：Shell 配置

`PS2` 变量持有次提示符符号，用于需要几行才能完成的命令。默认的次提示符是 `>`。添加的命令以次提示符而不是主提示符开头。你可以像更改主提示符一样轻松地更改次提示符，如下：

```
$ PS2="@"
```

就像 TCSH 壳一样，BASH 壳提供了一组预定义的代码，你可以用它们来配置提示符。通过这些代码，你可以将时间、用户名或目录路径名成为提示符的一部分。你甚至可以让提示符显示你即将输入的当前命令的历史事件编号。每个代码前面都有一个反斜杠 `\` 符号。`\w` 表示当前工作目录，`\t` 表示时间，`\u` 表示用户名。`!` 显示下一个历史事件编号。在下一个示例中，用户将当前工作目录添加到了提示符中：

```
$ PS1="\w \$
/home/dylan $
```

代码必须包含在引号字符串中。如果没有引号，代码字符将不会被求值，并且本身将用作提示符。`PS1=\w` 将提示符设置为字符 `\w`，而不是工作目录。下一个示例将时间和历史事件编号结合并创建一个新的提示符中：

```
$ PS1="\t ! ->"
```

下表列出了配置提示符的代码：

| 提示符 | 说明 |
| :--- | :--- |
| `\!` | 当前历史编号 |
| `\$` | 用作 root 用户以外所有用户的提示符，root 用户使用 `#` 作为其提示符 |
| `\d` | 当前日期 |
| `\s` | 当前激活的 Shell |
| `\t` | 当天时间 |
| `\u` | 用户名 |
| `\w` | 当前工作目录 |

## Linux：完全参考指南

如果 `CDPATH` 未定义，当给 `cd` 命令给以一个目录名作为参数时，它只会在当前工作目录中搜索该名称。如果 `CDPATH` 已定义，`cd` 也会在 `CDPATH` 列出的目录中搜索该目录名。如果找到了目录，`cd` 就会切换到该目录。如果你正在运行一个必须经常在系统其他部分的目录的项目，这将非常有帮助。要切换到一个与你当前位置路径不同的目录，你需要知道该目录的完整路径。相反，你只需将该目录父目录的路径放在 `CDPATH` 中。然后 `cd` 就会自动搜索父目录，找到你想要的目录名称。

注意，你赋值给 `CDPATH` 的你想要切换的目录的父目录的路径，而不是目录本身的路径。

建议使用 `HOME` 变量在任何添加到 `CDPATH` 的新路径中指定用户的家目录。这是因为在文件系统重组期间，系统管理员可能会更改你家目录的路径。`HOME` 始终持有一个用户家目录的当前路径。在下一个示例中，路径 `/home/chris/letters` 被指定为 `$HOME/letters`：

```
$ CDPATH=$CDPATH:$HOME/letters
$ export CDPATH
$ echo $CDPATH
:/home/chris/letters
```

使用了几个特殊变量来设置网络应用程序（如 Web 浏览器或阅读器）使用的值。`NNTPSERVER` 用于设置可访问的远程新闻服务器的值……

## Linux：完全参考

### 获取别名和函数

```bash
if [ -f ~/.bashrc ]; then
  source ~/.bashrc
fi
```

### 用户特定环境变量和启动程序

```bash
PATH=$PATH:$HOME/bin
BASH_ENV=$HOME/.bashrc
USERNAME='/home/user'
```

```bash
export USERNAME BASH_ENV PATH
```

你的 Linux 系统还有一个它自己的配置文件，系统在任何用户登录时都会执行它。这个系统初始化文件被简单地称为 `profile`，位于 `/etc` 目录下，即 `/etc/profile`。该文件包含了系统需要为每个用户提供的特殊变量定义。下面是系统 `profile` 文件的副本。注意 `PATH` 如何被重新定义以包含 `/usr/X11R6/bin` 目录。该目录存放了你在使用桌面时执行的 X 命令。`HISTFILE` 也被重新定义，以包含更多数量的历史事件。这里为 `NNTPSERVER` 变量添加了一个条目。通常，新闻服务器地址是一个需要为所有用户的值。任何赋值都应该由系统管理员在系统的 `/etc/profile` 文件中进行，而不是在每个用户自己的 `.bash_profile` 文件中进行。`/etc/profile` 文件还会执行 `/etc/profile.d` 目录中的任何脚本。这种设计允许更模块化的结构。与其通过编辑 `/etc/profile` 文件来添加条目，你只需向 `profile.d` 目录添加脚本即可。这些脚本使用 BASH 扩展名 `.sh`。例如，`profile.d` 目录中的 `kde.sh` 脚本在 shell 中检查 `KDEDIR` 变量的定义，如果没有生效，则创建一个。

`/etc/profile`

```bash
## /etc/profile
```

### 全局环境变量和启动程序

### 函数和别名放在 `/etc/bashrc` 中

```bash
if echo $PATH | /bin/grep -q "/usr/X11R6/bin" ; then
  PATH=$PATH:/usr/X11R6/bin
fi
if [ "$(id -u)" = 0 ] && ! echo $PATH | /bin/grep -q "/sbin" ; then
  BASH_PATH=$sbin
fi
if [ "$(id -u)" = 0 ] && ! echo $PATH | /bin/grep -q "/usr/local/sbin" ; then
  PATH=$PATH:/usr/local/sbin
fi
PS1="\u@\h \W\$$"

USER="$(id -u)"
LOGNAME=$USER
```

## 第12 章：Shell 配置

```bash
MAIL="/var/spool/mail/$USER"
```

```bash
HOSTNAME='/bin/hostname'
HISTSIZE=1000
NNTPSERVER=nntp.myservice.com
```

```bash
if [ -z "$INPUTRC" ] && -f "$HOME/.inputrc" ]; then
  INPUTRC=/etc/inputrc
fi
```

```bash
export PATH PS1 HOSTNAME HISTSIZE MAIL NNTPSERVER
```

```bash
for i in /etc/profile.*.sh; do
  if [ -x $i ]; then
    $i
  fi
done
```

你的 `.bash_profile` 初始化文件是一个文本文件，像其他类型的文件一样可以通过文本编辑器进行编辑。你可以通过编辑 `.bash_profile` 并使用编辑命令向你的 `PATH` 添加新目录，通过在分配给 `PATH` 变量的路径列表中插入新的目录路径。你甚至可以添加新的变量定义。然而，如果你这样做，请确保将新变量名包含在 `export` 命令的参数列表中。例如，如果你的 `.bash_profile` 文件没有对 `EXIT` 变量的定义，你可以编辑该文件并添加一行为 `EXIT` 赋值。定义 `EXIT='set nu ai'` 将配置 Vi 编辑器以显示行号和自动缩进。当 `.bash_profile` 文件再次执行时，`EXIT` 变量将被设置为命令 `set nu ai`。当调用 Vi 编辑器时，`EXIT` 变量中的命令将被执行，自动设置行号和自动缩进选项。

在接下来的示例中，用户的 `.bash_profile` 经过了修改，包含了 `EXIT` 的定义以及对 `PATH`、`CPATH`、`PS1` 和 `HISTSIZE` 的重新定义。`PATH` 变量 `$=$HOME` 被添加到了其值中。`$HOME` 是一个求值为用户主目录的变量，结尾的列指定了当前工作目录，允许你执行可能位于主目录或工作目录的命令。`HISTSIZE` 的定义减少了保存的条目数量，从 `.profile` 文件中定义的 1000 个减少到。对特殊变量 `PS1` 的重新定义将提示符更改为包含当前工作目录的路径。你在 `.bash_profile` 中对特殊变量所做的任何更改都将覆盖系统 `profile` 文件早先做的更改。所有这些特殊变量都通过 `export` 命令导出。
