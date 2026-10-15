
```
$ ksh -x dbtest
[11] alias -x echo=print -
[12] alias -x vi=SHELL=/bin/sh vi
[13] PS0=:
[14] PS1=:/home/anatole/bin>
[15] typeset -fx cd md
[16] typeset -x EDITOR=vi
[1] X=ABC
[2] [ X = ABC ]
[4] print X is set to ABC
X is set to ABC
```

当不带任何调试选项直接运行 `dbtest` 脚本时，输出如下：

```
$ dbtest
X is set to ABC
```

# 使用 trap 调试

`trap` 命令对调试 Korn shell 脚本也有帮助。这种类型 `trap` 命令的语法为：

| 表 8.10: 某些常用信号 |
|---|---|---|---|---|

| 0 | shell exit | 3 | quit |
| 1 | hangup | 15 | terminate |
| 2 | interrupt | | | |

```
trap commands DEBUG
或
trap commands ERR
```

如果 `trap` 命令设为 `DEBUG`，则在脚本中的每个命令执行后执行 `trap` 命令。下面的 `trap` 命令会在变量 `DB_MODE` 设置为 `yes` 时在每个命令执行后执行 `pwd`，否则执行普通 `trap`。

```bash
if [[ $DB_MODE = yes ]]
then
    trap "pwd" DEBUG
else
    trap "rm -rf \$TMPFILE; exit 1 2 15
fi
```

如果设置为 `ERR` 并启用了 `errxit (-e)` 选项，则会在每个命令后执行 `trap`。`trap` 命令允许你优雅地处理错误。当命令以非零退出状态失败时，就会触发 `trap`。这对于清理临时文件或记录错误用。

`trap` 还可以捕获信号。shell 提供了可以捕获的信号，例如 `SIGINT` 和 `SIGTERM`。例如，你可以捕获 `SIGINT` 信号（由 Ctrl+C 触发），以确保脚本在退出前执行清理工作。

```bash
trap 'echo "Interrupted"; exit 1' SIGINT
trap 'echo "Terminating"; exit' SIG
```

通过使用 `trap`，你可以创建更健壮的能优雅处理意外情况的 Korn shell 脚本。

# Korn Shell 用户与编程手册

```bash
$ cat hmail
for i in terry larry mary
do
    mail $i <<-END
    $(date)
    Have a good holiday $i!
END
```

# 协进程 (Co-Processes)

协进程是通过 `|&` 字符终止的命令。它们在后台执行，但其标准输入和输出被附加到当前的 shell。`print -p` 命令用于向协进程的标准输入写入内容，而 `read -p` 用于从协进程的标准输出读取内容。在这里，使用 `read -p` 命令将 `date` 命令的输出读取到 `DATE` 变量：

```bash
$ date | &
[2] 241
$ read -p DATE
$ print $DATE
Thu Jul 18 12:23:57 PST 1996
```

协进程可以用于在 Korn 脚本内部编辑文件。在这个示例中，我们从文件 `co.text` 开始：

```bash
$ cat co.text
This is line 1
This is line 2
This is line 3
```

它通过协进程进行编辑，因此会返回作业号和进程 ID：

# 第 8 章：编写 Korn Shell 脚本

| 表 8.11: 协进程 |
| --- | --- |

| command |& | 在后台执行命令，并将其标准输入和输出附加到 shell。 |
| n<&p | 将输入从协进程重定向到文件描述符 $n$。如果未未指定 $n$，则使用标准输入。 |
| n>&p | 将协进程的输出重定向到文件描述符 $n$。如果未指定 $n$，则使用标准输出。 |
| print -p | 向协进程的标准输入写入内容。 |
| read -p | 从协进程的标准输出读取内容。 |

使用 `print -p` 向协进程写入命令（显示第 3 行）。然后使用 `read -p` 将 `ed` 命令的输出读取到 `LINE` 变量中：

接下来的命令删除第 2 行，然后通过协进程发送写入和退出指令：

```bash
$ print -p 3
$ read -p LINE
$ print $LINE
This is line 3
```

从协进程中编辑后，`co.text` 如下：

```bash
$ cat co.text
This is line 1
This is line 2
This is line 3
```

# 第 9 章：杂命令

以下章节涵盖了 Korn shell 命令。其中许多命令用于 Korn shell 脚本。其余命令则与你的环境和系统资源配合工作。

## : 命令

:` 命令是空命令（null command）。它通常被用作无操作（no-op），用于检查变量是否设置，或用于无限循环。如果在 Korn 脚本中提供，当变量未设置，它将导致脚本带错误退出。这里的 `:` 命令被用作无操作，因为我们只想在读取完整个文件的每一行后打印出总行数。

```bash
$ integer=0
while read line; do
  :
  ((NUM+=1))
done
print $NUM
```

## eval 命令

`eval` 命令按照以下格式读取并执行命令：对于简单命令，使用或不使用 eval 的执行没有区别。这里有一个更复杂的命令说明了 `eval` 的用法。我们希望 `$$#` 首先展开为参数个数，然后 `$n` 展开为最后一个参数的值。如果不使用 `eval` 命令，`eval_test` 的输出如下：

```bash
$ eval_test a b c
Total command-line arguments is 3
The last argument is $$
```

输出 3 是因为 `$$` 首先展开为进程 ID。通过 `eval` 命令两次展开 `print` 命令，我们得到了正确的结果。需要 `\` 是为了让 `$` 字符在第一次展开时被忽略。第一次展开后，`$(eval print$$)` 变为 c。

## export 命令

`export` 命令设置并导出变量。它等同于 `typeset -x`，但在函数内部使用除外。在这里，变量 `PATH` 被设置并导出：

```bash
$ export PATH=$usr/bin
```

`export` 命令可以接受多个变量。在这个示例中，变量 A、B、C 和 D 被设置并导出：

```bash
$ export A=1 C=2
```

如果没有指定参数，`export` 命令会列出导出变量名称和值：

```bash
$ export
EDITOR=vi
HOME=/home/anatole
LOGNAME=anatole
PATH=/usr/bin:/usr/bin
PWD=/home/anatole/asp/pubs/ksh/v2
SHELL=/bin/ksh
TERM=sun
USER=anatole
```

## false 命令

`false` 命令返回非零退出状态。仅此。它通常用于无限循环。在某些 Korn shell 版本中，`false` 是预定义的别名 0。无论哪种情况，它的作用相同。

## newgrp 命令

`newgrp` 命令更改组 ID，等同于 `exec /bin/newgrp group`。在这个示例中，组 ID 从 users 变为 networks：

```bash
$ id
uid=100 (anatole) gid=101 (users)
$ newgrp networks
uid=100 (anatole) gid=12 (networks)
```

如果不带参数，`newgrp` 将组 ID 重置为默认值：

```bash
$ newgrp
uid=100 (anatole) gid=101 (users)
```

## pwd 命令

`pwd` 命令打印当前工作目录。它是 Korn shell 的内置命令，等同于 `print -r - SPWD` 命令。

## readonly 命令

`readonly` 命令设置变量的值和/或属性。它等同于 `typeset -r`，但在函数内部使用时不会创建局部变量。此命令将 X 设置为只读并赋值为 1：

```bash
$ readonly X=1
```

`readonly` 命令可以接受多个变量：

```bash
$ readonly Y=1 Z=2
```
