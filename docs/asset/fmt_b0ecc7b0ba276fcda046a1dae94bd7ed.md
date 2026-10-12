
将命令替换（第 348 页）与 `set` 内建命令结合使用，是在 Shell 脚本中轻松获取命令标准输出的便捷方式。以下脚本展示了如何使用 `date` 和 `set` 以有用格式提供日期。第一条命令显示 `date` 的输出。然后 `cat` 显示 `dataset` 脚本的内容。该脚本的第一条命令使用命令替换将位置参数设置为 `date` 实用工具的输出。下一条命令 `echo $*` 显示由前一次 `set` 生成的所有位置参数。后续命令显示参数 `$1`、`$2`、`$3` 和 `$4` 的值。最后一条命令以可在信件或报告中使用的格式显示日期：

```
$ date
  Sat Jan  9 23:39:18 PST 2010
  $ cat dataset
  set $(date)
  echo $*
  echo
  echo "Argument 1: $1"
  echo "Argument 2: $2"
  echo "Argument 3: $3"
  echo "Argument 6: $6"
  echo
  echo "$2 $3, $6"
  $ dataset
  Sat Jan  9 23:39:25 PST 2010
  
  Argument 1: Wed
  Argument 2: Jan
  Argument 3: 9
  Argument 6: 2008
  
  Jan 9, 2010
```

你也可以使用 `date` 的 `+format` 参数来修改其输出格式。在不带任何参数的情况下使用 `set` 时，它会显示已设置的 Shell 变量列表，包括用户创建的变量和关键字变量。在 bash 中，此列表与在不带任何参数调用 `declare` 和 `typeset` 时显示的列表相同。

`set` 内建命令还接受用于定制 Shell 行为的选项。更多详情请参考第 339 页的“Set ±0: 开启和关闭 Shell 功能”。

## 变量扩展修饰符

表达式 `${name}`（如果不产生歧义，也仅写为 `$name`）扩展为变量 `name` 的值。如果 `name` 为空或未设置，bash 将 `${name}` 扩展为空字符串。Bourne Again Shell 提供了以下替代方案，以避免将扩展后的空字符串作为变量的值接受：

- 使用变量的默认值。
- 使用默认值并将该值分配给变量。
- 显示错误。

你可以通过使用变量名和修饰符来选择这些替代方案之一。此外，你可以使用 `set -o nounset`（第 341 页）使 bash 在引用未设置变量时显示错误并退出脚本。

### `:-` 修饰符

`:-` 修饰符使用默认值来替代空或未设置的变量，同时允许非空变量代表自身：`${name:-default}`。Shell 将 `:-` 解释为“如果 `name` 为空或未设置，扩展 `default` 并使用扩展后的值替代 `name`；否则使用 `name`。”。以下命令列出由 `LIT` 变量命名的目录内容。如果 `LIT` 为空或未设置，则列出 `/home/alex/literture` 的内容：

```
$ ls ${LIT:-/home/alex/literture}
```

默认值本身也可以包含会被扩展的变量引用：

```
$ ls ${LIT:-$HOME/literture}
```

### `:=` 修饰符

`:=` 修饰符不会改变变量的值。然而，你可能希望在脚本中将空或未设置变量的值改变为其默认值。你可以使用 `:=` 修饰符来实现：`${name:=default}`

Shell 会像展开 `$(name:=default)` 一样展开表达式 `$(name:=default)`，但同时将 `name` 的值设置为 `default` 展开后的值。如果脚本包含如下所示的一行，且在该行执行时 `LIT` 未设置或为空，则 `LIT` 将被赋值为 `/home/alex/literature`：

```bash
$ ls $(LIT:=/home/alex/literature)
```

- **:`builtin** Shell 脚本通常以 `:`（冒号）内置命令开头，并在同一行后跟随 `:=` 展开修饰符，以设置任何可能为空或未设置的变量。`:` 内置命令会评估命令行剩余部分的每个标记，但不会执行任何命令。如果没有前面的冒号 `(`)（注：此处原文可能有误，通常指冒号 `:`），Shell 会评估并尝试执行评估结果所形成的“命令”。

使用以下语法可以在 shell 脚本中为空或未设置的变量设置默认值（第一个冒号后有一个空格）：

```bash
: $(name:=default)
```

当脚本需要用于临时文件的目录，并使用 `TEMPDIR` 的值作为该目录的名称时，以下行会将 `TEMPDIR` 的默认值设为 `/tmp`：

```bash
: $(TEMPDIR:=/tmp)
```

## `:?` 显示错误消息

有时脚本需要某个变量的值，但你在编写脚本时无法提供合理的默认值。如果变量为空或未设置，`?` 修饰符会导致脚本显示错误消息并以退出状态 1 终止：

```bash
$(name:?message)
```

如果 `message` 包含空格，必须将其加引号。如果省略 `message`，Shell 将显示默认错误消息（`parameter null or not set`）。交互式 Shell 在使用 `:?` 时不会退出。在以下命令中，由于 `TESTDIR` 未设置，Shell 会在标准错误输出中显示 `:?` 后面字符串的展开值。在这种情况下，该字符串包含对 `date` 的命令替换，其中 `%T` 格式后面跟随字符串 `error, variable not set`。

```bash
cd $(TESTDIR:?'date +%T) error, variable not set.}
bash: TESTDIR: 16:16:14 error, variable not set.
```

# 内置命令

内置命令在第 7 章中介绍。Shell 内置的命令在你执行时不会创建新的进程。本节讨论 `type`、`read`、`exec`、`trap`、`kill` 和 `getopt` 内置命令，并以第 949 页的表 2.7-6 结尾，该表列出了许多 `bash` 内置命令。

## `type`：显示命令的信息

`type` 内置命令提供关于命令的信息：

```bash
$ type cat echo who if lt
cat is hashed (/bin/cat)
echo is a shell builtin
who is /usr/bin/who
if is a shell keyword
lt is aliased to 'ls -ltrh | tail'
```

前面的输出显示了如果你将 `cat` 或 `who` 作为命令执行时会运行的文件。由于 `cat` 已经从当前 Shell 中 `called`（调用），它存在于 *bash table*（第 1085 页）中，因此 `type` 报告 `cat` 是 `hashed`（已哈希）。输出还显示，调用 `echo` 会运行 `echo` 内置命令，`if` 是一个关键字，而 `lt` 是一个别名。

## `read`：接受用户输入

当你开始编写 Shell 脚本时，你会很快意识到，用户创建的变量最常见用途之一是存储用户响应提示符输入的信息。使用 `read`，脚本可以接受用户输入并将该输入存储在变量中。`read` 内置命令从标准输入读取一行，并将该行中的单词分配给一个或多个变量：

```bash
$ cat read1
echo -n "Go ahead: "
read firstline
echo "You entered: $firstline"
$ read1
Go ahead: This is a line.
You entered: This is a line.
```

`read1` 脚本的第一行使用 `echo` 提示你输入一行文本。`-n` 选项抑制随后的 **NEWLINE**（换行符），允许你在提示符所在的同一行输入文本。第二行将文本读取到变量 `firstline` 中。第三行通过显示 `firstline` 的值来验证 `read` 的操作。在这个例子中，变量（连同文本字符串一起）被加引号，因为作为脚本编写者，你无法预测用户可能响应提示符输入哪些字符。请考虑一下，如果变量没有加引号，而用户响应提示符输入了 `*` 会发生什么：

```bash
$ cat read1_no_quote
echo -n "Go ahead: "
read firstline
echo You entered: $firstline
$ read1_no_quote
Go ahead: *
You entered: read1 read1_no_quote script.1
$ ls
read1    read1_no_quote    script.1
```
