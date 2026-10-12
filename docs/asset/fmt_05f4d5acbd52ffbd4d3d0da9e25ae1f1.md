
`which line`

响应应该类似于 `/usr/bin/line`。否则，你将看到被搜索的 `$PATH` 列表，随后是 `"line" not found`。

`line` 命令用于一次抓取一行文本。如果你在 `read` 语句只使用一个变量，`read` 命令也会执行相同的操作，否则文本将被分散在 `read` 语句使用的不同变量之间。

在每次循环迭代中，`LINE` 变量通过命令替换被赋值一行文本。这是通过 `LINE=\`line\`` 语法实现的。执行 `line` 命令，并将结果赋值给 `LINE` 变量。当然，我可以使用任何变量名，例如：

```bash
MY_LINE=`line`
TEXT=`line`
```

注意单引号是反引号（`command`），它们位于键盘 ESC 键下方的左上角。执行命令并将输出赋值给变量被称为命令替换。当你运行计时脚本时，对于该技术的计时数据，这种额外的变量赋值可能会对计时结果产生影响。

## 方法 4：while_LINE_line_bottom

再次，这是我在任何 shell 脚本中看到的较晦涩的技术之一。这次我们将从底部向 `while` 循环提供数据，但我们将使用 `line` 命令而不是 `read` 语句将文本赋值给 `LINE` 变量。这种方法与上一种技术类似，但我们删除了到管道的 `cat $FILENAME`，取而是在 `done` 循环终止符之后从底部重定向输入。

查看列表 2-7 中的函数，你将看到它最后是如何运行的。

```bash
function while_LINE_line_bottom
(
# Method 4

# Zero out the $OUTFILE

>$OUTFILE

while LINE=`line`
do
    echo "$LINE" >> $OUTFILE
    :
done < $INFILE
}
```

**列表 2-7** while_LINE_line_bottom 函数，正如我们在之前的方法中所做的那样将文件文本赋值给 LINE 变量。唯一的区别是我们通过对 `$FILENAME` 文件的输入重定向从底部向 `while` 循环提供数据。到目前，你应该熟悉我们在做什么了。正如你所看到的，解析文件有许多方法，但你会发现并不是所有这些技术都是很好的选择。这是其中一个较糟糕的选择。

接下来我们将查看命令替换的另一种方法。最后两种方法使用了 `LINE=\`line\`` 语法的 `line` 命令。我们也可以使用 `LINE=$(line)` 技术。是否存在速度差异？

## 方法 5：cat_while_LINE_line_cmdsub2

眼眼吗？这与方法 3 是相同的方法，除了我们使用命令替换的方式。正如我在开始时说的，我们需要一个足够大的文件进行解析以获得准确的计时结果。当我们进行计时测试时，可能会看到两种命令替换技术之间的差异。记住，`line` 命令并不是在所有的 UNIX 操作系统上可用。

学习列表 2-8 中的函数，我们将在最后介绍该函数。

```bash
function cat_while_LINE_line_cmdsub2
(
# Method 5

# Zero out the $OUTFILE

>$OUTFILE
```

**列表 2-8** cat_while_LINE_line_cmdsub2 函数

```bash
cat $INFILE | while LINE=$(line)`
do
    echo "$LINE" >> $OUTFILE
done
```

列表 2-8（续）

列表 2-6 中的函数很有意思。因为我们没有使用 `read` 命令将文本行赋值给变量，我们需要其他技术。如果你的机器支持 `line` 命令，那么这就是一个选项。要检查你的 UNIX 机器是否具有 `line` 命令，请输入以下命令：

`which line`

响应应该类似于 `/usr/bin/line`。否则，你将看到被搜索的 `$PATH` 列表，随后是 `"line" not found`。

`line` 命令用于一次抓取一行文本。如果你在 `read` 语句只使用一个变量，`read` 命令也会执行相同的操作，否则文本将被分散在 `read` 语句使用的不同变量之间。

在每次循环迭代中，`LINE` 变量通过命令替换被赋值一行文本。这是通过 `LINE=\`line\`` 语法实现的。执行 `line` 命令，并将结果赋值给 `LINE` 变量。当然，我可以使用任何变量名，例如：

```bash
MY_LINE=`line`
TEXT=`line`
```

注意单引号是反引号（`command`），它们位于键盘 ESC 键下方的左上角。执行命令并将输出赋值给变量被称为命令替换。当你运行计时脚本时，对于该技术的计时数据，这种额外的变量赋值可能会对计时结果产生影响。

## 方法 6：while_LINE_line_bottom

```bash
function while_LINE_line_bottom
{
    # Method 6

    # Zero out the $OUTFILE

    >$OUTFILE

    while LINE=$(line)`
    do
        echo "$LINE" >> $OUTFILE
        :
    done < $INFILE
}
```

**列表 2-9** while_LINE_line_bottom 函数

列表 2-6 中的函数很有意思。因为我们没有使用 `read` 命令将文本行赋值给变量，我们需要其他技术。如果你的机器支持 `line` 命令，那么这就是一个选项。要检查你的 UNIX 机器是否具有 `line` 命令，请输入以下命令：

`which line`

响应应该类似于 `/usr/bin/line`。否则，你将看到被搜索的 `$PATH` 列表，随后是 `"line" not found`。

`line` 命令用于一次抓取一行文本。如果你在 `read` 语句只使用一个变量，`read` 命令也会执行相同的操作，否则文本将被分散在 `read` 语句使用的不同变量之间。

在每次循环迭代中，`LINE` 变量通过命令替换被赋值一行文本。这是通过 `LINE=\`line\`` 语法实现的。执行 `line` 命令，并将结果赋值给 `LINE` 变量。当然，我可以使用任何变量名，例如：

```bash
MY_LINE=`line`
TEXT=`line`
```

注意单引号是反引号（`command`），它们位于键盘 ESC 键下方的左上角。执行命令并将输出赋值给变量被称为命令替换。当你运行计时脚本时，对于该技术的计时数据，这种额外的变量赋值可能会对计时结果产生影响。

## 方法 7：for_while_LINE_bottom

```bash
function for_while_LINE_bottom
{
    # Method 7

    # Zero out the $OUTFILE

    >$OUTFILE

    while LINE=$(line)`
    do
        echo "$LINE" >> $OUTFILE
        :
    done < $INFILE
}
```

**列表 2-10** for_while_LINE_bottom 函数

列表 2-6 中的函数很有意思。因为我们没有使用 `read` 命令将文本行赋值给变量，我们需要其他技术。如果你的机器支持 `line` 命令，那么这就是一个选项。要检查你的 UNIX 机器是否具有 `line` 命令，请输入以下命令：

`which line`

响应应该类似于 `/usr/bin/line`。否则，你将看到被搜索的 `$PATH` 列表，随后是 `"line" not found`。

## 第一部分 Shell 脚本基础

标准错误（或称为 stderr）被指定为文件描述符 2。标准错误是系统和脚本发送或抑制错误信息的方式。

你可以结合使用这些文件描述符。我确定你见过某些 shell 脚本将所有输出重定向到“黑洞”，即 `/dev/null`。查看以下命令：

```bash
my_shell_script.Bash >/dev/null 2>&1
```

上述命令的结果是完全静默运行。换句话说，没有产生外部输出。脚本可能会从文件中读写，并将输出发送到特定的终端，例如 `/dev/console`。当你作为 cron 任务运行 shell 脚本，或者你并不感兴趣查看任何输出时，可能需要使用这种技术。

上一个示例使用了两个文件描述符。我们也可以使用其他描述符来处理文件输入和存储。在本章的剩余部分中，我们将使用文件描述符 3 配合标准输入（stdin，描述符 0），并通过文件描述符 0 重定向输入。对于输出重定向，我们将文件描述符 4 与标准输出（stdout，描述符 1）关联，然后将输出重定向到 `$OUTFILE`。在我们的 UNIX 系统中，文件描述符范围从 0 到 19。在本文中，我们将使用文件描述符 3，但也可以同样轻松使用文件描述符 5。稍后我们将使用相同的文件描述符技术通过文件描述符 4 进行输出重定向。
