

# bash 命令快速指南

# 表 A-3

| 变量 | 描述 |
| --- | --- |
| $* | 包含所有命令行参数，作为一个文本值。 |
| $@ | 包含所有命令行参数，作为独立的文本值。 |
| %# | 命令行参数的数量。 |
| $! | 最近一次使用的前台进程的退出状态。 |
| $- | 当前的命令选项标志。 |
| $$ | 当前 shell 的进程 ID (PID)。 |
| $! | 最近执行的后台进程的 PID。 |
| $0 | 命令行中的命令名称。 |
| $_ | shell 的绝对路径。 |
| BASH | 用于调用 shell 的完整文件名。 |
| BASH_ARGC | 当前子程序中中参数的个数。 |
| BASH_ARGV | 一个包含所有指定命令参数的数组。 |
| BASH_COMMAND | 当前正在执行的命令名称。 |
| BASH_ENV | 设置后，每个 bash 脚本在运行之前会尝试执行由此变量定义的启动文件。 |
| BASH_EXECUTION_STRING | 在 -c 命令行选项中使用的命令。 |
| BASH_LINENO | 一个包含脚本中每个命令行号的数组。 |
| BASH_REMATCH | 一个包含匹配正则表达式的文本元素的数组。 |
| BASH_SOURCE | 一个包含 shell 中声明函数的源文件名的数组。 |
| BASH_SUBSHELL | 当前 shell 派生的子 shell 数量。 |
| BASH_VERSION | 当前 bash shell 实例的版本号。 |
| BASH_VERSINFO | 变量数组，包含当前 bash shell 实例的各个主版本和次版本号。 |
| COLUMNS | 包含用于当前 bash shell 实例的终端宽度。 |

# 表 A-3（续）

| 变量 | 描述 |
| --- | --- |
| COMP_CWORD | 变量 COMP_WORDS 的索引，该变量包含当前光标位置。 |
| COMP_LINE | 当前命令行。 |
| COMP_POINT | 当前光标位置相对于当前命令起始位置的索引。 |
| COMP_WORDBREAKS | 执行补全时用作单词分隔符的字符集。 |
| COMP_WORDS | 包含当前命令行中各个单词的变量数组。 |
| COMPREPLY | 包含 shell 函数生成的可能补全码的变量数组。 |
| DIRSTACK | 包含目录栈当前内容的变量数组。 |
| EUID | 当前用户的数值有效用户 ID。 |
| FCEDIT | fc 命令使用的默认编辑器。 |
| FIGNNORE | 执行文件名补全时要忽略的后缀列表，用冒号分隔。 |
| FUNCNAME | 当前执行的 shell 函数的名称。 |
| GLOBIGNORE | 用冒号分隔的模式列表，定义了文件名扩展时要忽略的文件名集。 |
| GROUPS | 包含当前用户所属组列表的变量数组。 |
| histchars | 控制历史扩展的最多三个字符。 |
| HISTCMD | 当前命令的历史编号。 |
| HISTCONTROL | 控制哪些命令会被输入到 shell 历史列表中。 |
| HISTFILE | 保存 shell 历史列表的文件名（默认是 .bash_history）。 |
| HISTFILES | 历史文件文件中要保存的最大行数。 |
| HISTIGNORE | 用冒号分隔的模式列表，用于决定哪些命令在历史文件中被忽略。 |
| HISTSIZE | 历史文件中存储的最大命令数。 |

# 表 A-3（续）

| 变量 | 描述 |
| --- | --- |
| HOSTFILE | 当 shell 需要完成主机名时应读取的文件名。 |
| HOSTNAME | 当前主机的名称。 |
| HOSTTYPE | 描述 shell 运行机器的字符串。 |
| IGNOREEOF | shell 退出前必须接收的连续 EOF 字符数。如果此值不存在，默认为一。 |
| INOPTRC | Readline 初始化文件的名称（默认是 .inputrc）。 |
| LANG | shell 的本地分类。 |
| LC_ALL | 覆盖 LANG 变量，定义一个本地分类。 |
| LC_COLLATE | 设置排序字符串值时使用的排序规则。 |
| LC_CTYPE | 决定用于文件名扩展和模式匹配的字符的解释方式。 |
| LC_MESSAGES | 决定在解释以美元符号 $ 前头的双引号字符串时使用的本地设置。 |
| LC_NUMERIC | 决定格式化数字时使用的本地设置。 |
| LINENO | 当前执行的脚本中的行号。 |
| LINES | 定义终端上可用的行数。 |
| MACHTYPE | 以 .cpu-company-system 格式定义系统类型的字符串。 |
| MAILCHECK | shell 检查新邮件的频率（秒），默认是 60）。 |
| OLPWD | shell 中使用的上一个工作目录。 |
| OPTERR | 如果设置为 1，shell 会显示由 getopts 命令生成的错误。 |
| OTYPE | 定义 shell 运行的操作系统的字符串。 |
| PIPESTATUS | 包含前台进程退出状态值列表的变量数组。 |
| POSIXLY_CORRECT | 如果设置，bash 将以 POSIX 模式启动。 |
| PPID | 父进程的进程 ID。 |
| PROMPT_COMMAND | 设置后执行的命令。 |
| PS1 | 主提示符字符串。 |
| PS2 | 次要提示符字符串。 |
| PS3 | 用于替换的命令。 |
| PS4 | 替换命令的值。 |
| PWD | 当前工作目录。 |
| RANDOM | 0 到 32767 之间的随机数。 |
| REPLY | 替换命令的值。 |
| SECONDS | 启动后的秒数。 |
| SHELLOPTS | 冒号分隔的启用选项。 |
| SHLVL | 每次启动 shell 时增加的级别。 |
| TIMEFORMAT | 显示时间的格式。 |
| UID | 当前用户的数值用户 ID。 |

# 附录 B

# sed 和 gawk 快速指南

如果你在 shell 脚本中处理任何类型的数据，可能需要使用 sed 或 gawk 程序。本附录提供了 sed 和 gawk 命令的快速参考。

## sed 编辑器

sed 编辑器根据你输入的命令行或存储在文件中的命令操作数据。它每次从输入读取一行数据，根据指定的命令更改数据，然后输出数据。

## 启动 sed 编辑器

使用 sed 命令的格式为：

```
sed options file
```

options 允许自定义 sed的行为，见表 B-1。

script 参数指定单个命令。如果需要多个命令，你必须使用 -e 选项在命令行中指定，或使用 -f 选项在单独的文件指定。

# 命令选项

| 选项 | 描述 |
| --- | --- |
| -e script | 在处理输入时将 script 中指定的命令添加到命令列表中。 |
| -f file | 在处理输入时将 file 中指定的命令添加到命令列表中。 |
| -n | 不为每个命令产生输出，而是等待 print 命令。 |

# sed 命令

sed 编辑器包含对输入流中的每行数据处理的命令。本节介绍了一些你在 shell 脚本中常用的 sed 命令。

# 替换

s 命令替换流中的文本。s 命令的格式为：

`s/pattern/replacement/flags`

其中 *pattern* 是要替换的文本，*replacement* 是 sed 将插入的新文本。

flags 参数控制替换如何发生。有四种类型的标志：

- 一个数字

在第一种替换类型中，你可以指定 sed 编辑器应该替换匹配模式的几次，例如 2 只替换第二个次数。

# 地址

默认情况下，你使用的 sed 命令适用于数据的所有行。如果你只想将命令应用到特定行或一组行，你必须使用行地址。

sed 编辑器有两种行地址的形式：

字体 行号范围
- 过滤掉行的模式

两种形式都使用相同的格式来指定地址：

`[address]command`

