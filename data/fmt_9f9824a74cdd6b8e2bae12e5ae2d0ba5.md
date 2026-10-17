
添加 `;;&` 语法允许 `case` 继续进行下一个测试，而不是简单地终止。

## Summing Up

`case` 命令是我们编程技巧包中的一个方便的补充。正如我们将在下一章看到的，它是处理某些类型问题的完美工具。

## Further Reading

- *Bash Reference Manual* 关于条件构造的部分详细描述了 `case` 命令：  
  http://tiswww.case.edu/php/chet/bash/bashref.html#SEC21
- *Advanced Bash-Scripting Guide* 提供了 `case` 应用的进一步示例

http://tldp.org/LDP/abs/html/testbranch.html

## 32 – 位置参数

我们程序中一直缺少的一个功能是接受和处理命令行选项和参数的能力。在本章中，我们将研究 shell 的特性，这些特性允许我们的程序访问命令行内容。

### 访问命令行

shell 提供了一组称为位置参数的变量，其中包含命令行上的各个单词。变量命名为 `0` 到 `9`。它们可以这样演示：

```bash
#!/bin/bash

# posit-param: script to view command line parameters

echo "
\$0 = $0
\$1 = $1
\$2 = $2
\$3 = $3
\$4 = $4
\$5 = $5
\$6 = $6
\$7 = $7
\$8 = $8
\$9 = $9
"
```

一个非常简单的脚本，用于显示变量 `$0-$9` 的值。执行时不带命令行参数：

```text
[me@linuxbox ~]$ posit-param
$0 = /home/me/bin/posit-param
$1 =
$2 =
$3 =
$4 =
$5 =
$6 =
$7 =
$8 =
$9 =
```

即使不提供参数，`$0` 也始终包含出现在命令行上的第一项，即正在执行的程序的路径名。当提供参数时，我们看到结果：

```text
[me@linuxbox ~]$ posit-param a b c d
$0 = /home/me/bin/posit-param
$1 = a
$2 = b
$3 = c
$4 = d
$5 =
$6 =
$7 =
$8 =
$9 =
```

> 注：你实际上可以使用参数扩展访问超过九个参数。要指定大于九的数字，请用大括号括住该数字。例如 `${10}`、`${55}`、`${211}` 等。

### 确定参数数量

shell 还提供了一个变量 `$#`，它给出命令行上的参数数量：

```bash
#!/bin/bash
# posit-param: script to view command line parameters
echo "
```

```bash
$8 = Desktop
$9 = dirlist-bin.txt
```

在这个示例系统中，通配符 `*` 展开为 82 个参数。我们如何处理这么多？shell 提供了一种方法，尽管有点笨拙，可以做到这一点。`shift` 命令每次执行时都会使所有参数“向下移动一位”。事实上，通过使用 `shift`，只需一个参数（加上永远不变的 `$0`）即可：

```bash
#!/bin/bash
# posit-param2: script to display all arguments
count=1
while [[ $# -gt 0 ]]; do
    echo "Argument $count = $1"
    count=$((count + 1))
    shift
done
```

每次执行 `shift` 时，`$2` 的值会移动到 `$1`，`$3` 的值会移动到 `$2`，依此类推。`$#` 的值也会减少一。

在 `posit-param2` 程序中，我们创建一个循环来评估剩余参数的数量，只要至少有一个参数就继续。我们显示当前参数，用 `count` 变量在每次循环迭代时递增以提供已处理参数的运行计数，最后执行 `shift` 以将下一个参数加载到 `$1` 中。以下是程序运行情况：

```text
[me@linuxbox ~]$ posit-param2 a b c d
Argument 1 = a
Argument 2 = b
Argument 3 = c
Argument 4 = d
```

### 简单应用

即使没有 `shift`，也可以使用位置参数编写有用的应用程序。举例来说，这里有一个简单的文件信息程序：

```bash
#!/bin/bash
# file_info: simple file information program
PROGNAME=$(basename $0)
if [[ -e $1 ]]; then
    echo -e "\nFile Type:"
    file $1
    echo -e "\nFile Status:"
    stat $1
else
    echo "$PROGNAME: usage: $PROGNAME file" >&2
    exit 1
fi
```

此程序显示指定文件的类型（由 `file` 命令确定）和文件状态（来自 `stat` 命令）。该程序的一个有趣特性是 `PROGNAME` 变量。它被赋予 `basename $0` 命令的结果值。`basename` 命令删除路径名的前导部分，只留下文件的基本名称。在我们的示例中，`basename` 删除了 `$0` 参数中包含的路径名的前导部分，即我们示例程序的完整路径名。此值在构建诸如程序末尾的用法消息之类的消息时很有用。通过这种方式编码，脚本可以重命名，消息会自动调整为包含程序的名称。

### 使用位置参数与 shell 函数

正如位置参数用于向 shell 脚本传递参数一样，它们也可以用于向 shell 函数传递参数。为了演示，我们将 `file_info` 脚本转换为 shell 函数：

```bash
file_info () {
    # file_info: function to display file information
    if [[ -e $1 ]]; then
        echo -e "\nFile Type:"
        file $1
        echo -e "\nFile Status:"
        stat $1
    else
        echo "$FUNCNAME: usage: $FUNCNAME file" >&2
        return 1
    fi
}
```

现在，如果一个脚本包含 `file_info` shell 函数并用文件名参数调用该函数，参数将被传递给函数。

借助此功能，我们可以编写许多有用的 shell 函数，这些函数不仅可以在脚本中使用，也可以在 `.bashrc` 文件中使用。

注意 `PROGNAME` 变量已更改为 shell 变量 `FUNCNAME`。shell 会自动更新此变量以跟踪当前执行的 shell 函数。请注意 `$0` 始终包含命令行上的第一个项目的完整路径名（即程序的名称），并且不包含我们可能期望的 shell 函数名称。

## 批量处理位置参数

有时将所有位置参数作为一组进行管理很有用。例如，我们可能想要为另一个程序编写一个“包装器”。这意味着我们创建一个脚本或 shell 函数来简化另一个程序的执行。包装器提供了一组神秘的命令行选项，然后将一组参数传递给底层程序。

shell 为此目的提供了两个特殊参数。它们都扩展为完整的位置参数列表，但在某些微妙之处上有所不同。它们是：

表 32-1：`*` 和 `@` 特殊参数

| 参数 | 描述 |
|---|---|
| `$*` | 扩展为位置参数列表，从 1 开始。当被双引号包围时，它扩展为一个双引号字符串，包含所有位置参数，每个参数由 `IFS` shell 变量的第一个字符分隔（默认为空格字符）。 |
| `$@` | 扩展为位置参数列表，从 1 开始。当被双引号包围时，它将每个位置参数扩展为一个单独的被双引号包围的词。 |

下面是一个展示这些特殊参数的脚本：

```bash
#!/bin/bash
# posit-params3 : script to demonstrate $* and $ @
print_params () {
    echo "$S1 = $1"
    echo "$S2 = $2"
    echo "$S3 = $3"
    echo "$S4 = $4"
}
pass_params () {
    echo -e "\n" "$* :";  print_params $*
    echo -e "\n" "$*" :";  print_params "$*"
    echo -e "\n" "$@ :";  print_params $@
    echo -e "\n" "$@" :";  print_params "$@"
}
```
