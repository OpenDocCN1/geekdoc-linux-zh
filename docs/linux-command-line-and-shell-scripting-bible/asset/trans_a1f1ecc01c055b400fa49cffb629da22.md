

# 第四部分 替代 Linux Shell

| 表格 20-4 (续) |
| 变量 | 描述 |
| :--- | :--- |
| MAIL | 用户邮箱文件的名称。 |
| MAILCHECK | 检查邮箱是否有新邮件的频率。 |
| MAILPATH | 多个邮箱文件名的用冒号分隔的列表。如果设置，此值将覆盖 MAIL 环境变量。 |
| OLDPWD | 上一个工作目录的值。 |
| PATH | 可执行文件的默认搜索路径。 |
| PPID |当前 shell 父进程的进程 ID。 |
| PS1 | 主 shell 命令行界面提示符。 |
| PS2 | 次级命令行界面提示符。 |
| PS4 | 当启用执行跟踪时，在每行之前打印的字符。 |
| PWD | 当前工作目录的值。 |
| TERM | shell 的默认终端设置。 |

你应该会注意到，dash 的环境变量与 bash 中使用的环境变量非常相似（见第 5 章）。这并非偶然。请记住，dash 和 bash shell 都是 Bourne shell 的扩展，因此它们都包含了它的许多功能。然而，由于其简单性，dash 包含的环境变量比 bash shell 少得多。在 ash 环境下创建 shell 脚本时，你需要考虑到这一点。

dash shell 使用 `set` 命令来显示环境变量：

``````
$set
COLORTERM=''
DESKTOP_SESSION='default'
DISPLAY='0.0'
DM_CONTROL='/var/run/xdmctl'
GS_LIB='/home/atest/.fonts'
HOME='/home/atest'
IFS='='
KDEROOTHOME='/root/.kde'
KDE_FULL_SESSION='true'
KDE_MULTIHEAD=false
KONSOLE_DCOP='DCOPCRef(console-5293,konsole)
KONSOLE_DCOP_SESSION='DCOPCRef(console-5293,session-1)'
LANG='en_US'
LANGUAGE='en'
```

```
LC_ALL='en_US'
LOGNAME='atest'
OPTIND='1'
PATH='/usr/local/sbin:/usr/local/bin:/sbin:/usr/bin:/sbin:/bin'
PPID='5293'
PS1='$ '
PS2='> '
PS4='+'
PWD='/home/atest'
SESSION_MANAGER='/local/textbox'
SHELL='/bin/bash'
TERM='xterm'
USER='atest'
```

你应该会注意到，dash 的环境变量与 bash 中使用的环境变量非常相似（见第 5 章）。这并非偶然。请记住，dash 和 bash shell 都是 Bourne shell 的扩展，因此它们都包含了它的许多功能。然而，由于其简单性，dash 包含的环境变量比 bash shell 少得多。在 ash 环境下创建 shell 脚本时，你需要考虑到这一点。

dash shell 使用 `set` 命令来显示环境变量：

``````
$set
COLORTERM=''
DESKTOP_SESSION='default'
DISPLAY='0.0'
DM_CONTROL='/var/run/xdmctl'
GS_LIB='/home/atest/.fonts'
HOME='/home/atest'
IFS='='
KDEROOTHOME='/root/.kde'
KDE_FULL_SESSION='true'
KDE_MULTIHEAD=false
KONSOLE_DCOP='DCOPCRef(console-5293,konsole)
KONSOLE_DCOP_SESSION='DCOPCRef(console-5293,session-1)'
LANG='en_US'
LANGUAGE='en'
```

```
LC_ALL='en_US'
LOGNAME='atest'
OPTIND='1'
PATH='/usr/local/sbin:/usr/local/bin:/sbin:/usr/bin:/sbin:/bin'
PPID='5293'
PS1='$ '
PS2='> '
PS4='+'
PWD='/home/atest'
SESSION_MANAGER='/local/textbox'
SHELL='/bin/bash'
TERM='xterm'
USER='atest'
```

你应该会注意到，dash 的环境变量与 bash 中使用的环境变量非常相似（见第 5 章）。这并非偶然。请记住，dash 和 bash shell 都是 Bourne shell 的扩展，因此它们都包含了它的许多功能。然而，由于其简单性，dash 包含的环境变量比 bash shell 少得多。在 ash 环境下创建 shell 脚本时，你需要考虑到这一点。

dash shell 使用 `set` 命令来显示环境变量：

``````
$set
COLORTERM=''
DESKTOP_SESSION='default'
DISPLAY='0.0'
DM_CONTROL='/var/run/xdmctl'
GS_LIB='/home/atest/.fonts'
HOME='/home/atest'
IFS='='
KDEROOTHOME='/root/.kde'
KDE_FULL_SESSION='true'
KDE_MULTIHEAD=false
KONSOLE_DCOP='DCOPCRef(console-5293,konsole)
KONSOLE_DCOP_SESSION='DCOPCRef(console-5293,session-1)'
LANG='en_US'
LANGUAGE='en'
```

```
LC_ALL='en_US'
LOGNAME='atest'
OPTIND='1'
PATH='/usr/local/sbin:/usr/local/bin:/sbin:/usr/bin:/sbin:/bin'
PPID='5293'
PS1='$ '
PS2='> '
PS4='+'
PWD='/home/atest'
SESSION_MANAGER='/local/textbox'
SHELL='/bin/bash'
TERM='xterm'
USER='atest'
```

你应该会注意到，dash 的环境变量与 bash 中使用的环境变量非常相似（见第 5 章）。这并非偶然。请记住，dash 和 bash shell 都是 Bourne shell 的扩展，因此它们都包含了它的许多功能。然而，由于其简单性，dash 包含的环境变量比 bash shell 少得多。在 ash 环境下创建 shell 脚本时，你需要考虑到这一点。

dash shell 使用 `set` 命令来显示环境变量：

## 位置参数

除了环境变量，dash 使用特殊的位置参数。这里：

- `$0`: 脚本的名称。
- `$1`: 第一个参数。
- `$n`: 第 n 个参数。
- `$@`: 所有参数。
- `$*`: 所有的参数。
- `$?`: 上一个命令的退出状态。
- `$`: 进程 ID。
- ``: 参数

你应该到注意到，dash 的环境变量与 bash 中使用的环境变量非常相似（见第 5 章）。这并非偶然。请记住，dash 和 bash shell 都是 Bourne shell 的扩展，因此它们都包含了它的许多功能。然而，由于其简单性，dash 包含的环境变量比 bash shell 少得多。在 ash 环境下创建 shell 脚本时，你需要考虑到这一点。

dash shell 使用 `set` 命令来显示环境变量：

``````
$set
COLORTERM=''
DESKTOP_SESSION='default'
DISPLAY='0.0'
DM_CONTROL='/var/run/xdmctl'
GS_LIB='/home/atest/.fonts'
HOME='/home/atest'
IFS='='
KDEROOTHOME='/root/.kde'
KDE_FULL_SESSION='true'
KDE_MULTIHEAD=false
KONSOLE_DCOP='DCOPCRef(console-5293,konsole)
KONSOLE_DCOP_SESSION='DCOPCRef(console-5293,session-1)'
LANG='en_US'
LANGUAGE='en'
```

```
LC_ALL='en_US'
LOGNAME='atest'
OPTIND='1'
PATH='/usr/local/sbin:/usr/local/bin:/sbin:/usr/bin:/sbin:/bin'
PPID='5293'
PS1='$ '
PS2='> '
PS4='+'
PWD='/home/atest'
SESSION_MANAGER='/local/textbox'
SHELL='/bin/bash'
TERM='xterm'
USER='atest'
```

## 用户自定义变量

dash shell 允许你定义自己的变量。你可以使用赋值运算符来实现：

```bash
VAR='value'
```

一旦定义了变量，你可以通过在前面加上美元符号来使用它：

```bash
echo $VAR
```

你还可以更改变量的值：

```bash
VAR='new value'
```

## 内置命令

dash shell 支持许多内置命令。以下是列表：

| 命令 | 描述 |
| :--- | :--- |
| alias | 创建别名 |
| bg | 在后台继续作业 |
| cd | 切换目录 |
| echo | 显示文本 |
| eval | 解释字符串 |
| exec | 用命令替换 shell. |
| exit | 退出 shell |
| export | 导出变量 |
| fc | 列出、编辑或重新执行 |
| fg | 在前台继续作业 |
| getopts | 获取选项 |
| hash | 维护命令的哈希表 |
| pwd | 显示当前工作目录 |
| read | 从 STDIN 读取行 |
| readonly | 使变量变为只读 |
| printf | 显示格式化字符串 |
| set | 设置变量 |
| shift | 移动参数 |
| test | 评估表达式 |
| times | 显示用户和系统时间 |
| trap | 在信号上执行操作 |
| type | 解释名称 |
| ulimit | 设置资源限制 |
| umask | 设置文件权限 |
| unalias | 移除别名 |
| unset | 移除变量 |
| wait | 等待作业完成 |

## printf 命令

echo 命令不是从命令行或 shell 脚本显示数据的唯一方法。第 10 章演示了如何在 gawk 程序中使用 C 语言的 `printf` 命令。

dash 同样包含了 `printf` 内置命令，允许你自定义输出。`printf` 命令使用特殊的格式标记，对数据的显示方式和位置提供了更大的控制。

`printf` 命令的格式为：

```
printf "format string" var2 ...
```

注意 dash 版本的 `printf` 命令在格式字符串和变量之间不使用逗号。与 gawk 版本一样，格式字符串是一个包含包含最多三个元素的字符串值：

- 标准文本字符
- 格式规范
- 字符转义序列

`printf` 命令使用独立的格式规范来显示命令行列出的每个参数。格式规范定义了要显示的数据类型以及如何显示它。dash 的 `printf` 命令使用了与第 19 章讨论的 gawk `printf` 命令相同的格式规范。

这是一个在 dash shell 脚本中使用 `printf` 命令的示例：

```bash
#!/bin/dash
# 测试 printf 命令

factorial=1
value=1
while [ $value -le 10 ]
do
```

