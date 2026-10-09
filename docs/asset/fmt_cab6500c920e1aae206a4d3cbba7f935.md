
# `$$` PID 编号

`shell` 在 `$$` 参数中存储执行它的进程的 PID 编号。在下面的 `echo` 中显示了变量的值，而 `ps` 工具确认了它的值。两个命令都显示 `shell` 的 PID 编号为 `5209`：

```bash
$ echo $$
5209
$ ps
TTY         COMMAND
5209 pts/1    00:00:00 bash
```

调用 `showhowards` 并带有四个参数的输出。在下面的调用中，`showhowards` 演示了一个在使用位置参数时（这些参数可能未设置或可能为空值）应该记住的微妙问题。

# `"$*"` 与 `"$@"`

`$*` 和 `$@` 参数的工作方式相同，除非它们被包含在双引号内。`"$*"` 会产生一个带有空格或 `IFS` 值（位于位置参数之间的分隔符）的单个参数，而 `"$@"` 则产生一个列表，其中每个位置参数都是一个独立的参数。这种差异通常使得 `"$@"` 在 `shell` 脚本比 `"$*"` 更实用。

以下脚本有助于解释这两个参数之间的区别。在脚本的第二行中，引号防止了对其中包含的特殊字符进行解释，使其能够按原样显示。设置 `"$"` 的 `bb1` 脚本将多个参数分配给第一个命令行参数：

`# cat bb1`

```
set "$@"
echo # parameters with "$@"
echo 1: $1
echo 2: $2
echo 3: $3
```

`# set bb1 a b c`

```
1: parameters with "$@"
1: a b c
2:
3:
```

`bb2` 脚本显示 `set "$@"` 将每个参数分配给一个不同的命令行参数：

`# cat bb2`

```
set # parameters with "$@"
echo 1: $1
echo 2: $2
echo 3: $3
```

`# set bb2 a b c`

```
3 parameters with "$@"
1: a
2: b
3: c
```

# `shift`: 提升命令行参数

内置命令 `shift` 会将每个命令行参数向前移动。第一个参数（原先 `$1`）被丢弃。第二个参数（原先 `$2`）变为第一个参数（现在是 `$1`），第三个变为第二个，依此类推。由于不存在 `"unshift"` 命令，你无法找回已丢弃的参数。`shift` 的可选参数指定了要移动的位数（以及要丢弃的参数数量）；默认值为 `1`。

以下 `demo_shift` 带有三个参数被调用。参数周围的双引号是为了保留输出的间隔。程序显示参数并反复移动它们，直到没有更多参数可以移动为止：

`# $ cat demo_shift`

```
echo "arg1=$1 $arg2=$2 $arg3=$3"
shift
echo "arg1=$1 $arg2=$2 $arg3=$3"
shift
echo "arg1=$1 $arg2=$2 $arg3=$3"
shift
echo "arg1=$1 $arg2=$2 $arg3=$3"
shift
```

`# $ demo_shift alice helen jenny`

```
arg1=alice arg2=helen arg3=jenny
arg1=helen arg2=jenny arg3=
arg1=jenny arg2= arg3=
arg1=
```

反复移动是在在期望任意数量参数的 `shell` 脚本中循环遍历所有命令行参数的方便方法。参见第 `883` 页查看使用 `shift` 的 `shell` 脚本。

# `set`: 初始化命令行参数

当你调用内置命令 `set` 并带有一个或多个参数时，它会将参数的值分配给位置参数 `$1, $2` 和 `$3`：

- `shell` 脚本使用 `set` 给位置参数 `$1, $2` 和 `$3` 分配值：

`# $ cat set_it`

```
set this is it
echo $3 $2 $1
```

`# $ set_it`

```
it is this
```

将替换（第 `334` 页）与内置命令 `set` 结合，可以在 `shell` 脚本中易于处理的格式获取命令的标准输出方便方法。以下脚本显示了如何使用 `date` 和 `set` 提供有用格式的日期。第一个命令显示 `date` 的输出。下一个命令显示日期设置 脚本。下一个命令 `echo *` 显示由上一个 `set` 产生的所有位置参数。随后的命令显示参数 `$1, $2, $3` 和 `$4` 的值。最后一个命令以你可以在信件或报告中使用的格式显示日期：

`# $ date`

```
Wed Jan 5 23:39:18 PST 2005
```

`# $ cat dateset`

```
set ($date)
echo $$
echo "Argument 1: $1"
echo "Argument 2: $2"
echo "Argument 3: $3"
echo "Argument 6: $6"
echo
echo "$2 $3, $6"
```

`dateset`

`Wed Jan 5 23:39:25 PST 2005`

`Argument 1: Wed`

`Argument 2: Jan`

`Argument 3: 5`

`Argument 6: 2005`

`Jan 5, 2005`

你也可以使用 `date` 的 `format` 参数来修改其输出格式。

当不带任何参数使用时，`set` 会显示已设置的 `shell` 变量列表，包括用户创建的变量关键字变量。在 `bash` 下，这是 `declare` 和 `typeset` 在不带参数调用时显示的列表。

内置命令 `set` 还接受选项，允许你自定义 `shell` 的行为。更多信息请参阅第 `325` 页的 [det opt: 开启和关闭 Shell 功能](325)。

# 扩展空和未设置的变量

表达式 `$(name)`（如果没有歧义则仅为 `$name`）展开为 `name` 变量的值。如果 `name` 为空或未设置，`bash` 将 `$(name)` 扩展为空字符串。

- `${name:-word}` 如果 `name` 设置且不为空，则扩展为 `name` 的值，否则扩展为 `word`。

- `${name:=word}` 如果 `name` 设置且不为空，则扩展为 `name` 的值，否则设置 `name` 为 `word` 并扩展为 `word`。

- `${name:?word}` 如果 `name` 设置且不为空，则扩展为 `name` 的值，否则显示 `word` 并退出 `shell`。

- `${name:+word}` 如果 `name` 设置且不为空，则扩展为 `word` 的值，否则扩展为空字符串。

- `${name#word}` 扩展为删除最短匹配 `word` 前缀后的 `name` 值。

- `${name##word}` 扩展为删除最长匹配 `word` 前缀后的 `name` 值。

- `${name%word}` 扩展为删除最短匹配 `word` 后缀后的 `name` 值。

- `${name%%word}` 扩展为删除最长匹配 `word` 后缀后的 `name` 值。

你还可以使用`参数扩展`语法来修改变量的值。例如，`${name/pattern/replacement}` 将第一个匹配的 `pattern` 替换为 `replacement`，而 `${name//pattern/replacement}` 将替换所有匹配项。

# 内置命令

内置命令是在第 `7` 章引入的。执行 `shell` 内置命令时，不会派生（`fork`）进程。本节讨论了 `type`、`read`、`exec`、`trap`、`kill` 和 `getopts` 内置命令，最后在第 `939` 页的表 `28-6` 列出了许多 `bash` 内置命令。

## `type`: 显示命令信息

`type` 内置命令提供有关命令的信息：

```
$ type cat echo who is it
cat is hashed (/bin/cat)
echo is a shell builtin
who is /usr/bin/who
if is a shell keyword
it is aliased to `ls -trh | tail`
```

前面的输出显示了在使用 `cat` 或 `who` 作为命令时执行的文件。由于 `cat` 已经从当前 `shell` 被调用，它在哈希表中，`type` 报告 `cat` 是哈希的。输出还显示调用 `echo` 运行的是内置命令，`if` 是一个关键字，而它是一个别名。

## `read`: 接受用户输入

在编写脚本时，你很快会发现，用户创建变量最常见的任务之一是存储用户响应提示而输入的信息。使用 `read`，脚本可以接受用户输入并存储在变量中。`read` 内置命令从标准输入读取一行，并将单词分配给一个或多个变量。

```
$ cat read1
echo -n "Go ahead:"
read firstline
echo "You entered: $firstline"
$ read1
Go ahead: This is a line.
You entered: This is a line.
```

`read1` 脚本的第一行使用 `echo` 为你提供一行文本。然后选项 `-n` 抑制随后的换行符（`NEWLINE`），允许你在提示的同一行输入文本。第二行将文本读入变量 `firstline` 中。第三行通过显示值来验证读取操作。在这个示例中，变量（连同字符串）被加了引号，因为作为脚本编写者，你无法预测用户响应提示会输入什么字符。考虑一下如果变量没有加引号且用户响应提示输入了内容会发生什么：

```
$ cat read1_no_quote
echo -n "Go ahead: "
read firstline
echo You entered: $firstline
$ read1_no_quote
Go ahead: *
You entered: read1 read1_no_quote script.1
$ ls
read1 read1_no_quote script.1
```

命令列出的单词与输入的单词相同，这表明 `shell` 将星号扩展成了工作目录中的文件列表。当变量 `firstline` 被双引号包围时，`shell` 不会扩展星号。因此 `read1` 脚本的行为是正确的：

```
$ read1 "*"
Go ahead: *
You entered: *
```

如果你想让 `shell` 解释特殊字符的特殊含义，请不要使用引号。

### `REPLY`

内置命令具有使其更容易使用的特性。当你没有为 `read` 的输入指定变量时，`bash` 将输入放入命名变量 `REPLY` 中。你可以使用 `-p` 选项来提示用户，而不是使用单独的 `echo` 命令。下面的 `read1a` 脚本执行了与 `read1` 完全相同的任务：

```
$ cat read1a
read -p "Go ahead: "
echo "You entered: $REPLY"
```

`read2` 脚本提示输入命令行并将用户的响应读入变量 `cmd` 中。脚本随后尝试执行由 `cmd` 变量扩展产生的命令行：

```
$ cat read2
read -p "Enter a command: " cmd
$cmd
echo "Thanks"
```

在接下来的示例中，`read2` 读取了一个调用 `who` 内置命令的命令行。`shell` 执行该命令并显示 `Thanks`。接下来 `read2` 读取了一个执行 `who` 工具的命令行：

```
$ read2
Enter a command: echo Please display this message.
Please display this message.
Thanks
$ read2
Enter a command: who
alex pts/4 Jun 17:07:50 (0)
scott pts/12 Jun 17 11:54 (bravo.example.com)
Thanks
```

如果 `cmd` 没有扩展为有效命令，`shell` 会发出错误消息：
