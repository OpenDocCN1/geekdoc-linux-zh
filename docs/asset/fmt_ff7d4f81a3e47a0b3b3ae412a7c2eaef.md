
使用 `vi` 或 `nano` 编辑器创建本章所示示例 shell 脚本。这给了你一个练习它们的机会。`nl` 命令用于显示脚本内容以及相关的行号。以下示例脚本创建在 `/usr/local/bin` 目录下。

# 显示基本系统信息

让我们创建一个名为 `sys_info.sh` 的第一个脚本并检查它。进入目录 `/usr/local/bin` 并使用 `vi` 或 `nano` 构建脚本。输入你在下方看到的内容，不包括行号：

```
# nl sys_info.sh
1 #/bin/bash
2 # 此脚本的名为 sys_info.sh。
3 # 此脚本的作者是 Asghar Ghor。
4 # 此脚本创建于 2008 年 10 月 28 日。
5 # 此脚本由 Asghar Ghor 于 2008 年 11 月 28 日最后修改。
6 # 此脚本应位于 /usr/local/bin 目录。
7 # 此脚本的目的是解释一个小型 shell 程序的结构。
echo "Display Linux Kernel Information"
echo "--------------------------------------"
echo
echo "This machine running the following kernel:"
/bin/uname -s
echo "This machine is running the following release of Linux kernel:"
/bin/uname -r
```

![](img/3f35ec29a294974bc1a4fdae3ae46652_134_0.png)

在 `vi` 中，输入 `:nu`。

此脚本使用了注释和命令。

第一行指示脚本将使用的 shell。此行必须以 `#!` 字符组合开头，随后是 shell 文件的完整路径。

接下来的六行包含注释，包括脚本名称、作者、创建时间、最后修改时间、存储位置和目的。`#` 符号表示该字符右边的任何内容仅供参考，在脚本运行时不会执行。

第 8 行是脚本的第一个命令。`echo` 命令在屏幕上打印它的任何内容。在这种情况下，你将看到 "Display Linux Kernel Information"。

第 9 行为 "Display Linux Kernel Information" 标题下划线。

第 10 行 `echo` 命令后面没有任何内容。这意味着输出中将插入一个空行。

第 11 行在屏幕上打印 "This machine is running the following kernel:"。

第 12 行执行 `uname -s` 命令。该命令返回当前正在使用的 Linux 内核名称。

第 13 行在屏幕上打印 "This machine is running the following release of Linux kernel:"。

第 14 行执行 `uname -r` 命令。该命令返回正在运行的 Linux 内核版本。

## `chmod +x sys_info.sh`

现在你可以使用相对路径或全路径来运行脚本：

```
# ./sys_info.sh
# /usr/local/bin/bin/sys_info.sh
```

如果 `PATH` 变量中没有设置 `/usr/local/bin` 目录，请在 `/etc/profile` 文件中定义它，这样任何登录系统的用户都将拥有此路径。或者，可以将该目录路径添加到需要访问该目录的用户 `~/.bash_profile` 文件中。以下显示了如何在命令行提示符处设置路径：

```
# export PATH=$PATH:/usr/local/bin
```

让我们运行 `sys_info.sh` 并看看输出是什么样的：

```
# sys_info.sh
Display Linux Kernel Information
--------------------------------
```

此机器正在运行以下内核：

Linux

此机器正在运行 Linux 内核版本：

2.6.18-92.el5

## 调试 Shell 脚本

如果你发现脚本运行方式不符合预期，并想使用基本的调试技术，你可能想在脚本第一行的 `#!/bin/bash` 后面添加 `-x`，使其变为 `#!/bin/bash -x`。或者，你可以按照如下方式执行脚本：

```
# sh -x /usr/local/bin/sys_info.sh
echo 'Display Linux Kernel Information'
Display Linux Kernel Information
+ echo
------------------------------------------------
```

```
+ echo
echo 'This machine is running the following kernel:
This machine is running the following kernel:
+ /bin/uname -s
Linux
+ echo 'This machine is running the release of Linux kernel:
This machine is running the release of Linux kernel:
+ /bin/uname -r
2.6.18-92.el5
```

带有 `+` 符号，脚本中的实际行会被回显在屏幕上，其下一行是它产生的输出结果。

## 使用局部变量

你之前处理过变量并见过如何使用它们。回顾一下，变量有两种类型：局部（或私有）和全局（环境变量）。它们在脚本和命令行中的定义和使用方式完全相同。脚本中定义的局部变量在脚本执行完成后就会消失，而全局变量在执行完成后仍然存在。

在第二个脚本 `loc_var.sh` 中，定义了一个局部变量并显示了它的值。脚本执行完成后，检查该变量的值。

```
# nl loc_var.sh
# !/bin/bash
# The name of this script is loc_var.sh.
# The author of this script is Asghar Ghori.
# The script is created on October 28, 2008.
# This script is last modified by Asghar Ghori on November 28, 2008.
# This script should be located in /usr/local/bin/directory.
# The purpose of this script is to explain how a local variable is defined and used in a shell
# program.
echo "Setting a Local Variable"
echo "----------------------------------"
echo ""
echo SYS_NAME=rhel01
echo "The hostname of this system is $SYS_NAME".
```

当你执行此脚本时，结果将是：

```
# loc_var.sh
Setting a Local Variable.
----------------------------------
```

该系统主机名是 rhel01。

由于它是局部变量且脚本是在子 shell 中运行的，该变量在脚本执行完成后消失了。如果你尝试回显该变量，将看到如下：

```
# echo $SYS_NAME

```

## 使用预定义环境变量

在下一个脚本 `pre_env.sh` 中，显示了两个预定义环境变量 `SHELL` 和 `LOGNAME` 的值：

```
# nl pre_env.sh
# !/bin/bash
# The name of this script is pre_env.sh.
# The author of this script is Asghar Ghori.
# The script is created on October 28, 2008.
# This script is last modified by Asghar Ghori on November 28, 2008.
# This script should be located in /usr/local/bin/directory.
```

## 基础 Shell 脚本编写

# 此脚本的目的是解释如何在程序中使用预定义环境变量。

echo "The location of my shell command is:"

echo $SHELL

echo "You are logged in as $LOGNAME".

输出结果将是：

```
# pre_env.sh
The location of my shell command is:
/bin/bash
You are logged in as user1.
```

## 设置新的环境变量
