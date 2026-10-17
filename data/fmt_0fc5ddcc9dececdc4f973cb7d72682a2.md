
当你登录时，会执行一个 shell 并为你提供一个 shell 提示符。你在提示符的右侧输入命令。根据你之前的经验，你知道你需要一个用户名来登录并与操作系统交互。然而，当创建一个用户账户时，它会被赋予一个默认 shell，这使得你能够访问操作系统。对于 Red Hat Linux，默认 shell 是 `bash`。

正如你在第 1 章中所学到的那样，有多种不同的 shell。本书重点关注 `bash` shell。

![](img/72e8a95d2755ff2622521b6d924baa27_101_0.png)

`bash` shell 是由自由软件基金会开发的电气与电子工程师学会 `IEEE` 可移植性操作系统接口标准 `POSIX`。这意味着它是一项随操作系统免费提供的标准。

## /etc/profile 脚本文件

在 `/etc` 目录层次结构中存在启动文件，用于设置用户环境的默认设置。当用户登录时，启动文件按照特定的顺序被读取和执行。当用户注销时，注销文件会被读取和执行。

如果存在 `/etc/profile` 文件，shell 会读取并执行其中的命令。图 3-1 显示了文件中包含的内容。该文件实际上是一个脚本。它之所以重要是因为因为它为每个用户执行。然而，你的 `profile` 文件可能有所不同。如果你想让所有用户登录时执行一个脚本，或者想显示一条所有用户登录时都能看到的消息，你可以相应地修改此文件。你通常将语句放在此文件的末尾，以免干扰其中已包含的任何语句。该文件的权限对于 `root` 用户和其他所有用户来说都是可读可写的；因此，你必须以 `root` 身份登录才能修改此文件。用户无法修改它。如果你可能不此路径中的所有代码，随着你对该文件的处理，这些将会变得清晰。

让我们来看 `/etc/profile` 脚本中的一条语句，让你对该脚本中发生的情况有所了解。回想第 1 章，`history` 命令允许你保留最多 1,000 条命令。如果你查看图 3-1，你会注意到 `HISTSIZE=1000` 状态——这把 `history` 命令保留的命令数量设置为 1,000。作为 `root` 用户，你可以将其更改为 10,000 甚至仅为 100。如果你增加它，你会在历史列表中保留更多的命令。这很有帮助，因为在需要验证命令的的确切语法时，你可以查看之前的命令。然而，如果你增加了此文件（即保存历史列表的文件 `~/.bash_history`）的大小，该文件也会随着时间推移而增大。这意味着你将使用更多的磁盘空间来存储更大的历史列表。

## 理解 shell 登录和注销文件

```
# /etc/profile
## 系统级环境和启动程序
## 函数和别名存放在 /etc/bashrc
if echo $PATH | /bin/grep -q "usr/X11R6/bin"; then
PATH=$PATH:/usr/X11R6/bin
fi
uulimit -s -C 1000000 > /dev/null 2>&1
if [ "id -gn" = "id -un" -a "id -u" -gt 14 ]; then
  umask 002
else
  umask 022
fi
USER=`id -un`
LOGNAME=$USER
MAIL=`var/spool/$USER`
HOSTNAME=`bin/hostname`
HISTSIZE=1000
REPLY="Y"
if [ -z "$INPUTRC" ] || [ -f "$HOME/.inputrc" ]; then
  INPUTRC=/etc/inputrc
fi
```

**图 3-1** `/etc/profile` 脚本文件

你也可以在此文件中定义变量 `$LOGNAME`。`$LOGNAME` 等于当前登录用户的用户账户。作为系统管理员，你可能会将此信息用于审计目的。

## ~/.bash_profile 脚本文件

在 shell 为所有用户执行 `/etc/profile` 脚本文件后，另一个脚本执行，它被称为 `~/.bash_profile`。然而，这个文件位于每个用户的家目录下，它是隐藏的（注意文件名前的点）。隐藏该文件是为了防止你不意外删除。该文件的权限对于所有其他用户都是可读可写的；这意味着每个用户都可以自定义此文件。图 3-2 显示了文件中包含的内容。再次，你的内容可能会有所不同。用户可以自定义自己的登录过程。他们可以修改此脚本并将自己的命令放在文件中。例如，如果你想让所有用户登录时执行一个脚本，或者想显示一条所有用户登录时都能看到的消息，你可以相应地修改此文件。你通常将语句放在此文件的末尾，以免干扰其中已包含的任何语句。该文件的权限对于 `root` 用户和其他所有用户来说都是可读可写的；因此，你必须以 `root` 身份登录才能修改此文件。用户无法修改它。如果你可能不此路径中的所有代码，随着你对该文件的处理，这些将会变得清晰。

```
# /etc/profile
## 系统级环境和启动程序
## 函数和别名存放在 /etc/bashrc
if echo $PATH | /bin/grep -q "usr/X11R6/bin"; then
PATH=$PATH:/usr/X11R6/bin
fi
uulimit -s -C 1000000 > /dev/null 2>&1
if [ "id -gn" = "id -un" -a "id -u" -gt 14 ]; then
  umask 002
else
  umask 022
fi
USER=`id -un`
LOGNAME=$USER
MAIL=`var/spool/$USER`
HOSTNAME=`bin/hostname`
HISTSIZE=1000
REPLY="Y"
if [ -z "$INPUTRC" ] || [ -f "$HOME/.inputrc" ]; then
  INPUTRC=/etc/inputrc
fi
```

**图 3-1** `/etc/profile` 脚本文件（注：此处原文示例编号可能有误，已按逻辑保留）

你也可以在此文件中定义变量 `$LOGNAME`。`$LOGNAME` 等于当前登录用户的用户账户。作为系统管理员，你可能会将此信息用于审计目的。

## ~/.bash_profile 脚本文件

在 shell 为所有用户执行 `/etc/profile` 脚本文件后，另一个脚本执行，它被称为 `~/.bash_profile`。然而，这个文件位于每个用户的家目录下，它是隐藏的（注意文件名前的点）。隐藏该文件是为了防止你不意外删除。该文件的权限对于所有其他用户都是可读可写的；这意味着每个用户都可以自定义此文件。图 3-2 显示了文件中包含的内容。再次，你的内容可能会有所不同。用户可以自定义自己的登录过程。他们可以修改此脚本并将自己的命令放在文件中。例如，如果你想让所有用户登录时执行一个脚本，或者想显示一条所有用户登录时都能看到的消息，你可以相应地修改此文件。

```
# /etc/profile
## 系统级环境和启动程序
## 函数和别名存放在 /etc/bashrc
if echo $PATH | /bin/grep -q "usr/X11R6/bin"; then
PATH=$PATH:/usr/X11R6/bin
fi
uulimit -s -C 1000000 > /dev/null 2>&1
if [ "id -gn" = "id -un" -a "id -u" -gt 14 ]; then
  umask 002
else
  umask 022
fi
USER=`id -un`
LOGNAME=$USER
MAIL=`var/spool/$USER`
HOSTNAME=`bin/hostname`
HISTSIZE=1000
REPLY="Y"
if [ -z "$INPUTRC" ] || [ -f "$HOME/.inputrc" ]; then
  INPUTRC=/etc/inputrc
fi
```

**图 3-2** `~/.bash_profile` 脚本文件

让我们来看 `/etc/profile` 脚本中的一条语句，让你对该脚本中发生的情况有所了解。回想第 1 章，`history` 命令允许你保留最多 1,000 条命令。如果你查看图 3-1，你会注意到 `HISTSIZE=1000` 状态——这把 `history` 命令保留的命令数量设置为 1,000。作为 `root` 用户，你可以将其更改为 10,000 甚至仅为 100。如果你增加它，你会在历史列表中保留更多的命令。这很有帮助，因为在需要验证命令的的确切语法时，你可以查看之前的命令。然而，如果你增加了此文件（即保存历史列表的文件 `~/.bash_history`）的大小，该文件也会随着时间推移而增大。这意味着你将使用更多的磁盘空间来存储更大的历史列表。

## 学习 Shell 变量

Shell 变量是 shell 为特定用途设置的关键字。它们通常以大写字母输入。这与大多数以小字母输入的命令不同。每个 shell 变量都有不同的用途。请注意图 3-1 和 3-2 中的某些 shell 变量，例如 `PATH` 和 `HOSTNAME`。

你可以使用 `echo` 命令并在变量名前前加一个美元符号（`$`）来显示单个变量的内容。例如，`echo $HOME` 会显示主目录。请注意，`echo` 也会显示主目录。
