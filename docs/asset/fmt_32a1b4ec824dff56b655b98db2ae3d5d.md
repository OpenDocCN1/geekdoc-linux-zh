
分号的这种简单用法可以提高你的 shell 程序的可读性，并值得作为你自己代码格式的一部分来考虑。

## getopts 命令

让我们通过添加 `-t` 选项来扩展 `waitfor` 程序，该选项指定执行检查的频率（以秒为单位）。现在 `waitfor` 接受 `-m` 和 `-t` 选项。我们允许在命令行上以任何顺序指定选项，只要它们出现在我们要监控的用户名称之前。因此，有效的 `waitfor` 命令如下：

```
waitfor ann
waitfor -m ann
waitfor -t 600 ann
waitfor -m -t 600 ann
waitfor -t 600 -m ann
```

而无效的命令如下：

```
waitfor
waitfor -t-600 ann
waitfor ann -m
waitfor -t ann
```

- 缺少用户名
- 需要一个空格 `-t`
- 选项必须先出现
- 缺少参数 `-t`

当你开始编写代码来允许命令行上具有这种灵活性时，你很快就会发现它可能会变得复杂！

不过，不要担心；shell 提供了一个名为 `getopts` 的内置命令，可以方便地处理命令行参数。该命令的通用格式是

```
getopts options variable
```

我们很快就会深入研究选项字符串。现在，只需知道，仅字母选项的指定方式是后面跟一个冒号，表示它们需要一个参数，因此 `"ab:c"` 意味着 `-a` 和 `-c` 是允许的，`-b` 也是，但它需要指定额外的参数。

然而，`getopts` 命令要在循环内部执行，因为它可以方便对每个指定的用户执行所需的操作。每次循环，`getopts` 都会检查命令行参数，并通过检查参数是否以减号开头且后跟任何指定为选项的字母，来确定它是否为有效选项。如果是，`getopts` 将匹配的选项存储在指定的变量中，并返回非零退出状态。你很快就会明白我的意思了……

如果减号后的字母未列在选项中，`getopts` 在返回零退出状态之前会在变量中存储一个问号。它会向标准错误输出一条关于用户指定的错误参数的错误消息。

如果命令行上没有更多参数，或者当前参数不以减号开头，`getopts` 将返回非零退出状态，允许 shell 处理任何后续参数。将该命令看作是……

`waitfor` 程序的其余部分保持不变；唯一的变化是使用间隔变量来指定睡眠的秒数。

如果你对 `getopts` 及其用法感到有些头疼，别担心，它会在随后的 shell 程序中不断出现，通过更多接触，你就会掌握它的。对于高级 shell 编程来说，学习它也是值得的，因为否则手动解析除单个命令标志以外的任何内容，效率将低到令人难以接受。

## 读取和打印数据

在本章中，你将学习如何使用 `read` 命令从终端或文件读取数据，以及如何使用 `printf` 命令向标准输出写入格式化数据。

### read 命令

`read` 命令的通用格式为：
`read variables`

当执行此命令时，shell 会从标准输入读取一行内容，并将第一个单词赋值给 `variables` 列表中列出的第一个变量，将第二个单词赋值给第二个变量，依此类推。如果一行中的单词比列出的变量多，则多余的单词将分配给最后一个变量。例如，命令

`read x y`
从标准输入读取一行，将第一个单词存储在变量 `x` 中，将行的剩余部分存储在变量 `y` 中。由此可以推出，命令
`read text`

读取并将整行内容存储到 shell 变量 `text` 中。

### 一个复制文件的程序

让我们通过编写一个 `cp` 命令的简化版本来让命令运行起来。我们将其命名为 `mycp`，它有两个参数：源文件和目标文件。如果目标文件已存在，程序将警告用户并询问他们是否要继续复制。如果答案是“yes”，我们将继续；否则程序将退出。

```
$ cat mycp
#
## Copy a file
#
```

```bash
if [ "$#" -ne 2 ]; then
    echo "Usage: mycp from to"
fi

from="$1"
to="$2"

# 检查目标文件已存在
if [ -e "$to" ]; then
    echo "$to already exists; (yes/no)?"
    read answer
if [ "$answer" != "yes" ]; then
    echo "Copy not performed"
    exit 0
fi

## 目标不存在或输入了 "yes"
cp $from $to # proceed with the copy
```

现在让我们对程序进行快速测试：

```bash
$ ls -C
```

```bash
$ mycp
names
stat
```

```bash
$ mycp
Usage: mycp from to
$ ls -1 names
```

```bash
$ mycp names
-rw-r-- steve 43 Jul 20:12
-rw-r-- steve 43 Jul 21:16
```

```bash
$ mycp names
Make a copy of names
Did it work?
$ mycp names
already exists; (yes/no)?
no
Copy not performed
$
```

注意，`then` 和 `else` 之后没有出现分号。

许多 shell 程序员使用混合结构，其中 `if` 语句结构如下：

```
if [ condition ]; then
  command
fi
```

分号的这种简单用法可以提高你的 shell 程序的可读性，并值得作为你自己代码格式的一部分来考虑。
