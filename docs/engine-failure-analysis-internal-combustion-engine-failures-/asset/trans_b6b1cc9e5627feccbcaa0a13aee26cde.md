

# cat

```
cat [ option ] [ filename ]
```

在标准输出中显示指定的文件名。如果未指定文件名，该命令将从标准输入读取。您也可以单独使用一个减号（-）来指定从标准输入获取。您可以在空格分隔的列表中指定多个文件名，或者使用 shell 模式（参见第 4 章中的“Shell 模式”部分）。如果您将输出重定向到一个文件，此命令将连接输入文件（参见本节中的示例表）。

> 提示 要查看占据多屏显示空间的文本文件，请将输出通过管道传递给 `less`，例如，`cat README | less`。

## OPTIONS

| 使用此选项 | 执行此操作 |
| :--- | :--- |
| -e | 显示控制字符和非打印字符（换行符和制表符除外），并在每行末尾显示 $（与 -vE 相同） |
| -E, --show-ends | 在每行末尾显示 $ |
| --help | 显示可用选项 |
| -n, --number | 为所有输出行编号，包括空行 |
| -s, --squeeze-blank | 只显示一行空行 |
| -t | 显示控制字符和非打印字符（换行符除外）（与 -vT 相同） |
| -T, --show-tabs | 将制表符显示为 \^I |
| -v, --show-nonprinting | 显示控制字符和非打印字符（换行符和制表符除外） |
| --version | 显示版本号 |
| --b, --number-nonblank | 为输出行编号，除非它们是空行 |

## EXAMPLES

| 此命令 | 执行以下操作 |
| :--- | :--- |
| `cat example.txt` | 显示指定的文件（example.txt）。如果文件太长而无法在一屏中方便地查看，请使用 less 或 more，如下例所示。 |
| `cat example.txt \| less` | 使用 less 实用程序显示指定的文件（example.txt）。 |
| `cat example.txt \| more` | 使用 more 实用程序显示指定的文件（example.txt）。 |
| `cat -s example.txt \| less` | 使用 less 实用程序显示指定的文件（example.txt）并抑制空行。 |
| `cat -n example.txt \| less` | 使用 less 实用程序显示指定的文件（example.txt）并为行编号。 |
| `cat file1.txt file2.txt > file3.txt` | 连接两个输入文件（file1.txt 和 file2.txt）并将输出写入第三个文件（file3.txt）。 |

# cksum

```
cksum [ filename ]
```

对指定的文件名执行循环冗余检查（CRC），以确定文件是否已被修改或损坏。您可以在空格分隔的列表中指定多个文件名，或者使用 shell 模式（参见第 4 章中的“Shell 模式”部分）。此命令的输出由唯一标识文件内容的标识代码组成；文件中任何一个字符的变化都会导致代码不同。

## EXAMPLES

| 此命令 | 执行以下操作 |
| :--- | :--- |
| `cksum *.txt` | 对工作目录中的所有 .txt 文件执行 CRC 检查；输出由 CRC 代码和以列形式列出的文件名组成。 |
| `cksum article.doc > article.crc` | 将指定文件（article.doc）的校验和写入文件（article.crc）。 |

# cmp

`cmp [ option ] filename1 filename2`

快速比较两个指定文件（filename1 和 filename2），以确定是否存在差异。如果文件相同，程序将退出而不显示任何消息。

另请参阅 `diff`。

## OPTIONS

| 使用此选项 | 执行此操作 |
| :--- | :--- |
| `-l, --verbose` | 打印每个差异的字节编号，并显示不同的值（以八进制表示法） |
| `-s, --silent, --quiet` | 除了生成以下退出代码外，不指示任何内容：0（文件相同）或 1（文件不同） |
| `-c, --char` | 将不同的字节作为字符打印 |

## EXAMPLE

| 此命令 | 执行以下操作 |
| :--- | :--- |
| `cmp first-draft.txt second-draft.txt` | 显示两个文件之间遇到的第一个差异（如果有）。 |

# column

```
column [ option ] [ filename ]
```

将 *filename* 指定的输入文本格式化为五列列表，优先填充行。您可以使用 *-c* 选项更改列数，并使用 *-x* 选项优先填充列。默认分隔符是空白字符。输入文件必须是已排序的文本文件（参见 *sort*）。默认情况下，实用程序写入标准输出。使用输出重定向将其写入文件。

## OPTIONS

| 使用此选项 | 执行此操作 |
| :--- | :--- |
| -cn | 输出格式化为宽度为 *n* 列的显示 |
| -s character | 指定一个字符，用于在 -t 选项中分隔列 |
| -t | 创建一个表格，列由空白或 -s 选项指定的字符分隔 |
| -x | 在填充行之前填充列 |

## EXAMPLES

| 此命令 | 执行以下操作 |
| :--- | :--- |
| `column list.txt > list-table.txt` | 将 *list.txt* 中的行组织成列，并将结果写入 *list-table.txt*。 |
| `column -x list.txt > list-table.txt` | 与上述相同，但在填充行之前填充列。 |

# comm

```
comm [ option ] filename1 filename2
```

比较 **filename1** 和 **filename2** 中常见的行。输出显示三列。在第 1 列中，您会看到 **filename1** 特有的行。在第 2 列中，您会看到 **filename2** 特有的行。在第 3 列中，您会看到两个文件共有的行。

另请参阅 `cmp`、`diff`、`diff3`、`uniq`。

## OPTIONS

| 使用此选项 | 执行此操作 |
| :--- | :--- |
| `--1` | 省略第 1 列 |
| `--2` | 省略第 2 列 |
| `--3` | 省略第 3 列 |
| `--help` | 显示可用选项 |
| `--version` | 显示版本号 |

## EXAMPLE

| 此命令 | 执行以下操作 |
| :--- | :--- |
| `comm file-1.txt file-2.txt \| less` | 显示 `file-1.txt` 和 `file-2.txt` 特有的行以及两个文件共有的行。在屏幕上显示结果。 |

# cut

```
cut [ option ] [ filename ]
```

显示指定文件名中一定范围内的字符。您可以在空格分隔的列表中指定多个文件名，或者使用 shell 模式（参见第 4 章中的“Shell 模式”部分）。如果省略文件名，实用程序将从标准输入获取输入。

## OPTIONS

| 使用此选项 | 执行此操作 |
| :--- | :--- |
| -b range, --bytes=range | 仅输出由 range 指定的字节（参见本节的 Ranges 表）。 |
| -c range, --characters=range | 仅输出由 range 指定的字符（参见本节的 Ranges 表）。 |
| -d, --delimiter=character | 使用 character 而不是制表符作为字段分隔符。 |
| -f range, --fields=range | 仅输出由 range 指定的字段（参见本节的 Ranges 表）。 |
| --help | 显示此帮助并退出。 |
| --output-delimiter=string | 使用 string 作为输出分隔符。默认是使用输入分隔符。 |
| -s, --only-delimited | 仅打印包含分隔符的行。 |
| --version | 显示版本号。 |

## RANGES

| 范围 | 描述 |
| :--- | :--- |
| n | 第 n 个字节、字符或字段 |
| -m | 从第一个到第 m 个字节、字符或字段的范围 |
| n- | 从第 n 个字节、字符或字段到行末尾的范围 |
| n-m | 从第 n 个到第 m 个字节、字符或字段的范围 |

# diff

`diff [ option ] filename1 filename2`

比较 *filename1* 和 *filename2* 指定的两个文本文件。默认情况下，输出以上下文形式显示每个更改，*filename1* 的文本前有一个 <，*filename2* 的文本前有一个 >。您也可以比较目录。如果指定两个目录而不是文件，diff 仅比较具有相同名称的文件。

另请参阅 `cmp`、`diff3`。

## OPTIONS

| 使用此选项 | 执行此操作 |
| :--- | :--- |
| -p, --show-c-function | 显示每个更改所在的 C 编程函数。 |
| -t, --expand-tabs | 在输出文件中将制表符扩展为空格。 |
| -e, --ed | 生成一个脚本，可以使用 ed 编辑器将第一个文件转换为第二个文件。 |
| -b, --ignore-space-change | 忽略空白数量的变化。 |
| -i, --ignore-case | 忽略大小写变化。 |
| -B, --ignore-blank-lines | 忽略插入或删除空行的变化。 |
| -I regexexp | 忽略插入或删除 regexexp（正则表达式）的变化。 |
| -w, --ignore-all-space | 在比较行时忽略空白。 |
| -N, --new-file | 在目录比较中，如果文件仅在一个目录中找到，则将其视为存在于但为空在另一个目录中。 |

