

```
        fi
}
```

现在，如果一个脚本包含了 `file_info` shell 函数并用文件名参数调用该函数，参数将被传递给函数。

有了这种能力，我们可以编写许多有用的 shell 函数，这些函数不仅可以在脚本中使用，也可以在 `.bashrc` 文件中使用。

注意 PROGNAME 变量被更改为 shell 变量 FUNCNAME。shell 会自动更新此变量以跟踪当前执行的 shell 函数。请注意 `$0` 总是包含命令行上第一个项目的完整路径名（即程序的名称），并且不包含我们可能期望的 shell 函数名称。

## 批量处理位置参数 *En Masse*

有时将所有位置参数作为一组进行管理是有用的。例如，我们可能想要为另一个程序编写一个“包装器”。这意味着我们创建一个脚本或 shell 函数来简化另一个程序的执行。包装器提供了一组神秘的命令行选项，然后将参数列表传递给底层程序。

shell 为此目的提供了两个特殊参数。它们都扩展为完整的位置参数列表，但在某些微妙方面有所不同。它们是：

**Table 33-1: The `$*` And `$@` Special Parameters**

| Parameter | Description |
|---|---|
| `$*` | 扩展为位置参数列表，从 1 开始。当被双引号包围时，它扩展为一个双引号字符串，包含所有位置参数，每个参数由 IFS shell 变量的第一个字符分隔（默认为空格字符）。 |
| `$@` | 扩展为位置参数列表，从 1 开始。当被双引号包围时，它将每个位置参数扩展为一个单独的被双引号包围的词。 |

下面是一个展示它们实际效果的脚本：

```
#!/bin/bash

# posit-params3 : script to demonstrate $* and $@

print_params () {
    echo "$1 = $1"
    echo "$2 = $2"
    echo "$3 = $3"
    echo "$4 = $4"
}

pass_params () {
    echo -e "\n" '$* :' ;  print_params $*
    echo -e "\n" "$*" ':' ; print_params "$*"
    echo -e "\n" '$@ :' ; print_params $@
    echo -e "\n" "$@" ':' ; print_params "$@"
}

pass_params "word" "words with spaces"
```

在这个相当复杂的程序中，我们创建了两个参数：“word”和“words with spaces”并将它们传递给 pass_params 函数。该函数反过来使用特殊参数 `$*` 和 `$@` 可用的四种方法中的每一种将它们传递给 print_params 函数。执行时，脚本揭示了差异：

```
[me@linuxbox ~]$ posit-param3

$* :
$1 = word
$2 = words
$3 = with
$4 = spaces

"$*" :
$1 = word words with spaces
$2 =
$3 =
$4 =

$@ :
$1 = word
$2 = words
$3 = with
$4 = spaces

"$@" :
$1 = word
```

```
$2 = words with spaces
$3 =
$4 =
```

使用我们的参数，`$*` 和 `$@` 都产生了一个四词结果：

```text
word words with spaces
```

`"$*"` 产生一个一词结果：

```text
"word words with spaces"
```

`"$@"` 产生一个两词结果：

```text
"word" "words with spaces"
```

这与我们的实际意图相符。从中可以得到的教训是，尽管 shell 提供了四种获取位置参数列表的不同方法，但 `"$@"` 对于大多数情况来说是最有用的，因为它保留了每个位置参数的完整性。

## 33 – Positional Parameters

## 更完整的应用程序

经过长时间的中断，我们将继续进行 `sys_info_page` 程序的工作。我们下一个添加的功能将向程序添加几个命令行选项，如下所示：

- **输出文件。** 我们将添加一个选项来指定包含程序输出的文件名。它将指定为 `-f file` 或 `--file file`。
- **交互模式。** 此选项将提示用户输入输出文件名，并确定指定的文件是否已存在。如果存在，将在覆盖现有文件之前提示用户。此选项将通过 `-i` 或 `--interactive` 指定。
- **帮助。** 指定 `-h` 或 `--help` 可使程序输出信息性的使用消息。

以下是实现命令行处理的所需代码：

```
usage () {
        echo "$PROGNAME: usage: $PROGNAME [-f file | -i]"
        return
}

# process command line options

interactive=
```

