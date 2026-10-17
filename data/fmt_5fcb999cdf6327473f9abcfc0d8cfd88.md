
`file.bak=/home/jody/ellie/junk`: not found

### EXPLANATION

- 1 变量 `round` 被赋值为 `world`。当 shell 遇到变量名前面的美元符号时，它会执行变量替换。变量的值将被显示。
- 2 变量 `name` 被赋值为 `"Peter Piper"`。需要引号来隐藏空白，以便 shell 在解析命令行时不会将字符串拆分为单独的单词。变量的值将被显示。

### EXPLANATION (CONTINUED)

- 3 变量 `x` 未被赋予值。shell 将分配 `null` 值。`null` 值，即空字符串，被显示。
- 4 变量名中的句点是非法的。变量名中允许的唯一字符是数字、字母和下划线。shell 尝试将字符串作为命令执行。

本地变量的作用域。本地变量仅对其创建的 shell 已知。它不会传递给子 shell。双美元符号变量是一个特殊变量，包含当前 shell 的 PID。

# EXAMPLE 7.19

```
1 $ echo $$
1313
2 $ round=world
$ echo $round
world
3 $ sh   # Start a subshell
4 $ echo $$
1326
5 $ echo $round
6 $ exit   # Exits this shell, returns to parent shell
7 $ echo $$
1313
8 $ echo $round
world
```

### EXPLANATION

- 1 双美元符号变量的值计算为当前 shell 的 PID。此 shell 的 PID 为 1313。
- 2 本地变量 `round` 被赋值为字符串 `world`，并且显示变量的值。
- 3 启动一个新的 Bourne shell。这称为子 shell 或子进程 shell。
- 4 此 shell 的 PID 为 1326。父 shell 的 PID 为 1313。
- 5 在此 shell 中未定义变量 `round`。打印一个空行。
- 6 `exit` 命令终止此 shell 并返回到父 shell。`Ctrl-D` 也会退出此 shell。
- 7 父 shell 返回。显示其 PID。
- 8 显示变量 `round` 的值。

# 设置只读变量。只读变量不能被重新定义或取消设置。

### EXAMPLE 7.20

```
1  $ name=Tom
2  $ readonly name
$ echo $name
Tom
3  $ unset name
name: readonly
4  $ name=Joe
name: readonly
```

### EXPLANATION

- 1 局部变量 `name` 被赋值为 `Tom`。
- 2 该变量被设为只读。
- 3 只读变量不能被取消设置。
- 4 只读变量不能被重新定义。

## 7.6.2 环境变量

环境变量可供创建它们的 shell 以及从该 shell 启动的任何子 shell 或进程使用。按照惯例，环境变量使用大写字母。环境变量是已被导出的变量。

创建变量的 shell 称为父 shell。如果从父 shell 启动新的 shell，则称为子 shell。某些环境变量，例如 `HOME`、`LOGNAME`、`PATH` 和 `SHELL`，在登录时由 `/bin/login` 程序设置。通常，环境变量在用户主目录中的 `.profile` 文件中定义和存储。有关环境变量的列表，请参阅表 7.3。

### Table 7.3 Bourne Shell Environment Variables

| Variable | Value |
|---|---|
| PATH | 命令的搜索路径。 |
| HOME | 主目录；当未指定目录时由 `cd` 使用。 |
| IFS | 内部字段分隔符，通常为空格、制表符和换行符。 |
| LOGNAME | 用户的登录名。 |
| MAIL | 如果将此参数设置为邮件文件的名称且未设置 `MAILPATH` 参数，则 shell 会通知用户指定文件中邮件的到达。 |
| MAILCHECK | 此参数指定 shell 检查 `MAILPATH` 或 `MAIL` 参数指定的文件中邮件到达的频率（以秒为单位）。默认值是 600 秒（10 分钟）。如果设置为零，shell 将在发出每个主提示符之前进行检查。 |

### EXPLANATION

- 1 `TERM` 变量被赋值为 `wyse`。该变量被导出。现在，从此 shell 启动的进程将继承该变量。
- 2 该变量被定义并导出，以便使其可用于从该 shell 启动的子 shell。
- 3 打印此 shell 的 PID 值。
- 4 启动一个新的 Bourne shell。新的 shell 称为子 shell。原始 shell 是其父 shell。
- 5 新 Bourne shell 的 PID 存储在 `$$` 变量中并被回显。
- 6 在父 shell 中设置的变量已导出到此新 shell 并被显示。
- 7 该变量被重置为 `April Jenner`。它被导出到所有子 shell，但不会影响父 shell。导出的值不会向上传播到父 shell。
- 8 退出此 Bourne 子 shell。
- 9 再次显示父 shell 的 PID。
- 10 变量 `NAME` 包含其原始值。变量在从父 shell 导出到子 shell 时会保留其值。子 shell 不能更改其父 shell 的变量值。

## 7.6.3 列出已设置的变量

有两个内置命令可以打印变量的值：`set` 和 `env`。`set` 命令打印所有变量，本地和全局。`env` 命令仅打印全局变量。

### EXAMPLE 7.22

```
1 $ env  (Partial list)
LOGNAME=ellie
TERMCAP=sun-cmd
USER=ellie
DISPLAY=:0.0
SHELL=/bin/sh
HOME=/home/jody/ellie
TERM=sun-cmd
LD_LIBRARY_PATH=/usr/local/Ow3/7lib
PWD=/home/jody/ellie/perl
2 $ set
DISPLAY=:0.0
FMHOME=/usr/local/Frame-2.1X
FONTPATH=/usr/local/Ow3/7lib/fonts
HELPPATH=/usr/local/Ow3/7lib/locale:/usr/local/Ow3/7lib/help
```

### EXAMPLE 7.22 (CONTINUED)

```
HOME=/home/jody/ellie
HZ=100
IFS=
LANG=C
LD_LIBRARY_PATH=/usr/local/0W3/lib
LOGNAME=ellie
MAILCHECK=600
MANPATH=/usr/local/0W3/share/man:/usr/local/0W3/man:/usr/local/man:/usr/local/doctools/man:/usr/man
OPTIND=1
PATH=/home/jody/ellie:/usr/local/0W3/bin:/usr/ucb:/usr/local/doctools/bin:/usr/bin:/usr/local:/usr/etc/etc:/usr/spool/news/bin:/home/jody/ellie/bin:/usr/lo
PS1=$
PS2=>
PWD=/home/jody/ellie/kshprog/joke
SHELL=/bin/sh
TERM=sun-cmd
TERMCAP=sun-cmd:te=\E[4:tfi=\E[7:tfc=sun:
USER=ellie
name=Tom
place="San Francisco"
```

### EXPLANATION

- 1. `env` 命令列出所有环境（已导出）变量。这些变量按照惯例使用全大写字母命名。它们从创建它们的进程传递到其任何子进程。
- 2. `set` 命令在不带选项的情况下打印所有已设置的变量，本地和已导出的（包括设置为 `null` 的变量）。

## 7.6.4 取消设置变量

本地变量和环境变量都可以使用 `unset` 命令取消设置，除非变量被设为只读。

### EXAMPLE 7.23

```
unset name; unset TERM
```
