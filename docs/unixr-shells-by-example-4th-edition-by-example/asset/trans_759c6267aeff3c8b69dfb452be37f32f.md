

![](img/60a0b5d254bd6007403850f972cbfad8_792_0.png)

## 图 13.1 启动 bash shell

## 在命令行更改 shell

如果你想临时从命令行启动另一个 shell（而不更改 /etc/passwd 文件），只需输入该 shell 的名称。例如，如果你当前正在使用标准 Bourne shell，并希望 bash 作为你的 shell，只需在命令行输入 bash 即可更改 shell。

## 示例 13.3

```
1 $ ps
 PID TTY TIME CMD
 1574 pts/6 0:00 sh

2 $ bash
 bash-2.05$

3 bash-2.05$ ps
 PID TTY TIME CMD
 1574 pts/6 0:00 sh
 1576 pts/6 0:00 bash
```

## 说明

-   1 ps 命令的输出显示当前正在运行的进程。目前，sh（Bourne shell）正在运行。
-   2 在 Bourne shell 提示符下，用户输入 bash 启动 Bourne Again shell。出现一个新的提示符。
-   3 在 bash 提示符下，执行 ps 命令。输出显示两个 shell 正在运行，当前 shell 现在是 bash。

## 13.2 环境

进程的环境由变量、打开的文件、当前工作目录、函数、资源限制、信号等组成。它定义了从一个 shell 继承到下一个 shell 的特性，以及工作环境的配置。用户 shell 的配置在 shell 初始化文件中定义。

### 13.2.1 初始化文件

bash shell 有许多启动文件会被 source。source 一个文件会使文件中的所有设置成为当前 shell 的一部分；也就是说，不会创建子 shell。（source 命令在“source 或 dot 命令”一节（第 773 页）中讨论。）初始化文件是否被 source 取决于 shell 是登录 shell、交互式 shell（非登录 shell）还是非交互式 shell（shell 脚本）。

当你登录时，用户主目录中的 .bash_profile 会被 source。它设置用户的别名和函数，然后设置用户特定的环境变量和启动脚本。

如果用户没有 .bash_profile，但有名为 .bash_login 的文件，那么该文件将被 source；如果没有 .bash_login，但有 .profile，则 .profile 将被 source。

## /etc/profile 文件

/etc/profile 文件是系统级初始化文件，由系统管理员设置，用于在用户登录时执行任务。它在 bash 启动时被执行。它也可供系统上所有 Bourne 和 Korn shell 用户使用，通常执行诸如检查邮件假脱机（mail spooler）是否有新邮件以及从 /etc/motd 文件显示每日消息等任务。（完成本章后，以下示例将更有意义。）

## 示例 13.4

```
(Sample /etc/profile)
# /etc/profile
# Systemwide environment and startup programs
# Functions and aliases go in /etc/bashrc
1 PATH="$PATH:/usr/X11R6/bin"
2 PS1="[\u@\h \W]\$ "
```

## 示例 13.4（续）

```
3 ulimit -c 1000000
4 if [ `id -gn` = `id -un` -a `id -u` -gt 14 ]; then
5   umask 002
else
  umask 022
fi
6 USER=`id -un`
7 LOGNAME=$USER
8 MAIL="/var/spool/mail/$USER"
9 HOSTNAME=`/bin/hostname`
10 HISTSIZE=1000
11 HISTFILESIZE=1000
12 export PATH PS1 HOSTNAME HISTSIZE HISTFILESIZE USER LOGNAME MAIL
13 for i in /etc/profile.d/*.sh ; do
14   if [ -x $i ]; then
15     . $i
fi
16 done
17 unset i #
```

## 说明

-   1 PATH 变量被赋予了 shell 搜索命令时应查找的位置。
-   2 设置了主提示符。它将在 shell 窗口中显示为用户名（\u）、@ 符号、主机名（\W）和美元符号。
-   3 ulimit 命令（shell 内建命令）被设置为将创建的 core 文件的最大大小限制为 1,000,000 字节。核心文件是崩溃程序的内存转储，占用大量磁盘空间。
-   4 这行的意思是：如果用户的组名等于用户名，且用户 ID 号大于 14……（参见第 5 行）
-   5 ……那么将 umask 设置为 002。创建目录时，目录将获得 775 权限，文件将获得 664 权限。否则，umask 设置为 022，目录获得 755，文件获得 644。
-   6 USER 变量被赋予用户名（`id -un`）。
-   7 LOGNAME 变量被设置为 $USER 中的值。
-   8 MAIL 变量被赋予用户邮件保存到的邮件假脱机路径。
-   9 HOSTNAME 变量被赋予用户宿主机器的名称。
-   10 HISTSIZE 变量设置为 1000。HISTSIZE 控制记住的历史项数量（来自存储在 shell 内存中的历史列表），并在 shell 退出后保存到历史文件中。

