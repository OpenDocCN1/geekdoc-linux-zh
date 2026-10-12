
```
$ date
Wed Aug 14 17:35:29 PDT 2010
cat dateset
set $(date)
echo $$
echo
echo "Argument 1: $1"
echo "Argument 2: $2"
echo "Argument 3: $3"
echo "Argument 6: $6"
echo
echo "$2, $6"
$ dateset
Wed Aug 14 17:35:34 PDT 2010
```

`Argument 1:` `Wed`

`Argument 2:` `Aug`

`Argument 3:` `14`

`Argument 6:` `2010`

`Aug, 2010`

# 1002 第27章 编程 Bourne Again Shell

Shell 扩展表达式 `${name:=default}` 的方式与扩展 `${name:-default}` 相同，并将 `name` 的值设置为 `default` 扩展后的值。如果脚本包含如下行，且在使用时 `LIT` 未设置或为空，则 `LIT` 被赋值为 `/home/max/literature`：

```bash
ls ${LIT:-/home/max/literature}
```

`(null)` 内置脚本通常以 `:` `(null)` 开头，并在同一行后面跟随扩展修饰符，用于设置任何可能为空或未设置的变量。`:` 会评估命令行剩余部分的每个标记，但不会执行任何命令。如果没有开头的冒号 (`:`)，shell 将评估并尝试执行评估结果产生的“命令”。

使用以下语法为 shell 脚本中为空或未设置的变量设置默认值（冒号后有一个空格）：

```bash
${name:=default}
```

当脚本需要一个临时目录并使用 `TMPDIR` 作为该目录的名称时，以下行会在 `TMPDIR` 未设置时对其赋值：

```bash
${TMPDIR:=tmp}
```

## :? 显示错误消息

有时在编写脚本时，你无法为使用的变量提供合理的默认值。如果变量为空或未设置，`?` 会修改脚本以显示错误消息并以状态码 1 退出：

```bash
${name:=message}
```

如果省略了 `message`，shell 将显示默认错误消息（parameter null or unset）。在交互式 shell 中使用 `?` 时并不会退出。在以下命令中，`TESTDIR` 未被设置，因此 shell 在标准输出上显示了 `?` 之后字符串的扩展值。在这种情况下，该字符串包含了对日期 `%T` 的替换，紧接着是字符串 "error, variable not set"。

```bash
cd ${date=$+S} error, variable not set.
```

```bash
bash: TESTDIR:16:16:14 error, variable not set.
```

## 内置命令

在第7章中引入的内置命令在执行时不会派生新进程。本节讨论了 `type`、`read`、`exec`、`trap`、`kill` 和 `getopts` 内置命令。第1015页的表 27-6 列出了许多 bash 内置命令。

### type: 显示命令信息

`type` 内置命令提供有关命令的信息：

```bash
$ type cat
echo (/bin/cat)
cat is hashed (/bin/cat)
echo is a shell builtin
who is /usr/bin/who
if is a shell builtin
it is aliased to 'ls -ltr | tail'
```

上述输出显示了提供 `cat` 或 `echo` 作为命令时将执行的文件。由于 `cat` 已经从当前 shell 被调用，它位于哈希表中（type 1151），`type` 报告 `cat` 已哈希。输出还显示调用 `echo` 运行的是内置命令，`if` 是关键字，而它是一个别名。

### read: 接受用户输入

用户创建变量的用途之一是存储用户响应提示输入的信息。通过 `read`，脚本可以接受用户输入并将输入存储在变量中。`read` 内置命令从标准输入读取一行并将单词分配给一个或多个变量：

```bash
$ cat -n
echo -n "Go ahead:"
read firstly
echo "You entered: $firstline"
$ ./read
Go ahead: This is a line.
You entered: is a line.
```

`read` 脚本的第一行使用 `echo` 提示输入文本。`-n` 选项抑制了随后的 `echo` 输出，允许你在同一行读取一行文本作为提示。第二行将文本读入变量 `firstly` 中。第三行通过显示 `firstly` 的值来验证 `read` 的操作。在这个示例中，变量（以及文本）加了引号，因为脚本编写者无法预测用户可能会针对提示输入哪些字符。考虑一下如果变量没有加引号且用户在提示处输入 `*` 会发生什么：

```bash
$ cat -n_no_quote
echo -n "Go ahead:"
read firstly
echo You entered: $firstline
$ ./read_no_quote
Go ahead: *
You entered: read1_no_quote script.1
$ ls
read1 read_no_quote script.1
```

`read` 命令列出的单词与脚本中的相同，这证明了 shell 将星号 `*` 扩展为工作目录中的文件列表。当变量 `firstline` 被双引号括起来时，shell 不会扩展星号。因此 `read` 脚本的行为是正确的：

```bash
$ ./read1
Go ahead:
You entered: *
```

`REPLY` 内置命令包含了一些可以使其更易使用的特性。例如——当没有指定变量来接收输入时，bash 会将输入放入名为 `REPLY` 的变量中。你可以使用 `-p` 选项来提示用户，而不是使用单独的 `echo` 命令。以下 `read2` 脚本执行与 `read` 完全相同的任务：

```bash
$ cat read2
read -p "Go ahead: " REPLY
echo "$REPLY"
```

`read2` 脚本提示命令，读取用户的响应并将其赋值给变量 `cmd`。然后脚本尝试执行 `cmd` 变量扩展后的命令行行：

```bash
$ cat read2
read -p "Enter a command: " cmd
echo "$cmd"
```

（参见第 992 页的“变量的局部性”）。相比之下，exec 在当前进程中直接执行（覆盖）一个命令。

# exec：执行命令

用于运行命令的 `exec` 具有以下语法：

```
exec command arguments
```

`exec` 与 `(.dot)` 的区别：由于 `exec` 在原始进程的环境中运行命令，它与 `(.dot)` 命令（第 296 页）相似。与可以运行 shell 脚本的 `.command` 不同，`exec` 既可以运行脚本也可以运行编译后的程序。此外，`.command` 在运行完成后会将控制权返回给原始脚本，而 `exec` 不会。最后，`.command` 让新程序访问本地变量的权限，而 `exec` 则没有。

使用 `exec` 时，它不会创建新进程，因此命令运行得更快速。然而，由于 `exec` 不会将控制权返回给原始程序，因此它只能作为脚本中的最后一个命令。以下脚本展示了控制权不会返回给脚本：

```
$ exec_demo
who
exec date
echo "This line is never displayed."
```

```
$ ./exec_demo
zach pts/7 May 20 7:58 (bravo.example.com)
hls pts/1 May 20 6:59 (:0.0)
Mon May 24 11:42:56 PDT 2010
```

下一个示例是 `out` 脚本（第 959 页）的修改版本，它使用 `exec` 执行脚本运行的最后一个命令。由于 `out` 运行 `cat` 或 `less` 然后终止，新版本 `out2` 同时对 `cat` 和 `less` 使用 `exec`：

```
$ cat out2
if [ $ -eq 0 ];
then
echo "Usage: out2 [-v] filenames" 1>&2
exit 1
```

```
fi
if [ "$1" = -v ]
then
shift
exec less "$@"
else
exec cat -- "$@"
```

## exec：重定向输入和输出

`exec` 的第二个主要用途是在脚本内部重定向文件描述符——包括标准输入、输出或错误。下一个命令将脚本后续所有本应来自标准输入的输入，重定向为来自名为 `infile` 的文件的输入：

```
exec < infile
```

同样，以下命令将标准输出和标准错误分别重定向到 `outfile` 和 `errfile`：
