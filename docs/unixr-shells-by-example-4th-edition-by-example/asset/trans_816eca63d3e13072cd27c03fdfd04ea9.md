

# EXPLANATION (CONTINUED)

+   11 HISTFILESIZE 被设置为限制历史文件中存储的命令数为 1000，即历史文件在达到 1,000 行后会被截断。 (参见第 785 页的“History”。)
+   12 这些变量被导出，以便在子 shell 和子进程中可用。
+   13 对于 /etc/profile.d 目录中每个以 .sh 结尾的文件…… (参见第 14 行)
+   14 ……检查该文件是否可执行，如果可执行…… (参见第 15 行)
+   15 ……使用点命令执行（source）该文件。/etc/profile.d 目录中的文件（分别为 lang.sh 和 mc.sh）设置字符集和字体集，并创建一个名为 mc 的函数，该函数启动一个名为 Midnight Commander 的可视化/浏览器文件管理器程序。要查看文件管理器如何工作，请在 bash 提示符下输入 mc。
+   16 done 关键字标记 for 循环的结束。
+   17 变量 i 被 unset，即从 shell 的命名空间中移除。i 的值是在 for 循环中分配给它的值，如果有分配的话。

The ~/.bash_profile File. 如果在用户的主目录中找到 ~/.bash_profile，则在 /etc/profile 之后对其进行 source。如果 ~/.bash_profile 不存在，bash 会查找另一个用户定义文件 ~/.bash_login 并对其进行 source，如果 ~/.bash_login 也不存在，则会 source ~/.profile（如果存在）。三个文件（~/.bash_profile、~/.bash_login 或 ~/.profile）中只有一个会被 source。Bash 还会检查用户是否具有 ~/.bashrc 文件，然后对其进行 source。

## EXAMPLE 13.5

```
(Sample .bash_profile)
# .bash_profile
# The file is sourced by bash only when the user logs on.

# Get the aliases and functions
1 if [ -f ~/.bashrc ]; then
2   . ~/.bashrc
fi

# User-specific environment and startup programs
3 PATH=$PATH:$HOME/bin
4 ENV=$HOME/.bashrc   # or BASH_ENV=$HOME/.bashrc
5 USERNAME="root"
6 export USERNAME ENV PATH
7 mesg n
8 if [ $TERM = linux ]
then
    startx  # Start the X Window system
fi
```

# EXPLANATION

+   1 如果用户主目录中存在名为 .bashrc 的文件…… (参见第 2 行)
+   2 ……为登录 shell 执行（source） .bashrc 文件。
+   3 PATH 变量被追加了用户 bin 目录的路径，通常是存放 shell 脚本的地方。
+   4 BASH_ENV（ENV）文件被设置为 .bashrc 文件的路径名，这是一个初始化文件，仅当 BASH_ENV（ENV）变量被设置时，才会对交互式 bash shell 和脚本进行 source。.bashrc 文件包含用户定义的别名和函数。
+   5 变量 USERNAME 被设置为 root。
+   6 变量被导出，以便子 shell 可用，其他进程也会知道它们。
+   7 mesg 命令使用 n 选项执行，禁止他人向终端写入。
+   8 如果 TERM 变量的值为 linux，则 startx 将启动 X Window 系统（允许多个虚拟控制台的图形用户界面），而不是在 Linux 控制台窗口中启动交互式会话。由于 ~/.bash_profile 仅在登录时被 source，登录 shell 是启动 X Windows 会话的最佳位置。

a. BASH_ENV 从 bash 2.0 版本开始使用。

## The BASH_ENV (ENV) Variable.

在 bash 2.0 版本之前，BASH_ENV 文件仅称为 ENV 文件（与 Korn shell 相同）。BASH_ENV（ENV）变量在 ~/.bash_profile 中设置。它被赋予一个文件名，该文件将在每次启动交互式 bash shell 或 bash 脚本时执行。BASH_ENV（ENV）文件将包含特殊的 bash 变量和别名。名称通常为 .bashrc，但你可以随意命名。当特权选项打开时（bash -p 或 set -o privileged）或使用 --norc 命令行选项时（bash --norc 或使用 bash 2.x+ 时的 bash --norc），BASH_ENV（ENV）文件不会被处理。

## The .bashrc File.

BASH_ENV（ENV）变量按惯例被赋予名称 .bashrc。此文件在每次启动新的或交互式 bash shell 或 bash 脚本时自动被 source。它包含仅与 bash shell 相关的设置。

## EXAMPLE 13.6

```
(Sample .bashrc)
# If the .bashrc file exists, it is in the user's home directory.
# It contains aliases (nicknames for commands) and user-defined functions.

# .bashrc
# User-specific aliases and functions
```
