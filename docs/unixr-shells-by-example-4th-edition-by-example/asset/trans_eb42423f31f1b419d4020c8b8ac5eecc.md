

创建变量的 shell 称为父 shell。如果从父 shell 启动一个新的 shell，则称为子 shell。某些环境变量，例如 HOME、LOGNAME、PATH 和 SHELL，是由 /bin/login 程序在您登录前设置的。通常，环境变量是在用户主目录中的 .profile 文件中设置的。

## 设置环境变量。

要设置环境变量，使用 export 命令在为其分配值之后或在变量被设置时使用。可以通过打开 set 命令的 allexport 选项来导出脚本中的所有变量（例如，set -o allexport）。

### EXAMPLE 11.37

```
1  $ TERM=wyse ; export TERM
2  $ export NAME ="John Smith"
   $ print $NAME
   John Smith
3  $ print $$ 
   319
4  $ ksh
5  $ print $$
   340
6  $ print $NAME
   John Smith
7  $ NAME="April Jenner"
   $ print $NAME
   April Jenner
8  $ exit
9  $ print $$
   319
10 $ print $NAME
    John Smith
```

### EXPLANATION

- 1 TERM 变量被赋值为 wyse。变量被导出。现在从此 shell 启动的进程将继承该变量。
- 2 变量在同一步骤中被导出并定义。（Korn shell 的新功能。）
- 3 打印此 shell 的 PID 值。
- 4 启动一个新的 Korn shell。新的 shell 是子 shell，原来的 shell 是其父 shell。
- 5 打印新的 Korn shell 的 PID，存储在 $$（340）变量中。
- 6 变量已导出到新 shell 并显示出来。
- 7 变量被重置为 April Jenner 并显示。
- 8 退出此 Korn 子 shell。父 shell 将返回。
- 9 再次显示父 shell 的 PID，319。
- 10 变量 NAME 包含其原始值。变量在从父 shell 导出到子 shell 时会保留其值。子 shell 不能更改其父 shell 的变量值。

## 特殊环境变量。

Korn shell 为环境变量 PATH、PS1、PS2、PS3、PS4、MAILCHECK、FCEDIT、TMOUT 和 IFS 分配默认值。SHELL、LOGNAME、USER 和 HOME 由 /bin/login 程序设置。您可以更改默认值并设置表 11.9 中列出的其他变量。

### Table 11.9 Korn Shell Environment Variables

| Variable Name | Meaning |
|---|---|
| _ (underscore) | 上一个命令的最后一个参数。 |
| CDPATH | cd 命令的搜索路径。以冒号分隔的目录列表，用于在路径名开头没有 /、./ 或 ../ 时查找目录。 |
| COLUMNS | 如果设置，定义 shell 编辑模式和 select 命令的编辑窗口宽度。 |
| EDITOR | 内置编辑器的路径名：emacs、gmacs 或 vi。 |
| ENV | 设置为包含函数和别名的文件名称的变量，Korn shell 在调用 ksh 程序时会调用该文件。在 1988 年之后的新版本中，此文件仅在 ksh 以交互方式调用时执行，而非交互式 shell 不执行。如果打开了特权选项，该变量不会被展开。 |
| ERRNO | 系统错误号。其值是最新的失败系统调用的错误号。 |
| FCEDIT | fc 命令的默认编辑器名称。在 1988 年之后的新版本中，此变量称为 HISTEDIT，fc 命令为 hist。 |
| FPATH | 以冒号分隔的目录列表，定义包含自动加载函数的目录的搜索路径。 |
| HISTEDIT | 对于 1988 年之后版本的 Korn shell，FCEDIT 的新名称。 |
| HISTFILE | 指定用于存储命令历史的文件。 |
| HISTSIZE | 可以访问的历史命令的最大数量；默认为 128。 |
| HOME | 主目录；cd 在未指定目录时使用。 |
| IFS | 内部字段分隔符，通常为空格、制表符和换行符，用于命令替换结果的字段分割、循环结构中的列表以及读取输入。 |
| LINENO | 脚本中的当前行号。 |
| LINES | 用于 select 循环中垂直显示菜单项；默认为 24。 |

