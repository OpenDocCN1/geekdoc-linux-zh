
此代码接受以下任何一种等效形式。

```
cmd - aoarg filename1 filename2
cmd - a - o arg filename1 filename2
cmd - oarg - a filename1 filename2
cmd - a - oarg - filename1 filename2
```

# getoptcvt 437

> 注意 — 如果带有选项-参数的选项后面跟着的值与 `optstring` 中列出的选项之一相同，

```
cmd - o - a filename
```

`opt` 总是将 `- a` 视为 `o` 的选项-参数；它绝不会将 `- a` 识别为选项。对于这种情况，示例中的 `for` 循环将跳过文件名。

## 属性

参见 `attributes(5)` 获取以下属性的描述：

| 属性类型 | 属性值 |
|---|---|
| 可性 CSI | SUNWcsu Enabled |

## 参见

`intro(1)`, `sh(1)`, `shell_builtins(1)`, `getopt(3C)`, `attributes(5)`

## 诊断

当 `getopt` 遇到未包含在 `optstring` 中的选项字母时，会在标准错误上打印错误消息。

# getoptcvt — 转换为 getopt 以解析命令行选项

## 概要

`/usr/lib/getoptcvt [-b] filename`
`/usr/lib/getoptcvt`

## 描述

使用 `/usr/lib/getoptcvt` 将 `getopt` 输出转换为以便使用 `gets`。`getoptcvt` 读取 `filename` 中的 shell 脚本，将其转换为 `getopts` 而非 `gets`，并将结果写入标准输出。`gets` 是一个内置的 Bourne shell 命令，用于解析位置参数并检查有效选项。请参见 `sh(1)`。`gets` 支持命令语法标准的所有适用规则（参见 `intro(1)` 中的规则 3-10）。你应该使用 `gets` 代替 `getopt` 命令。shell 内置 `gets` 命令的语法为：

```
getopts optstring name [argument...]
```

`optstring` 必须包含使用 `getopts` 的命令识别的选项字母；如果字母后跟着一个冒号，则预计该选项有一个参数或一组参数，这些参数必须与选项被空格分隔。

每次调用它时，`getopts` 将下一个选项放在 shell 变量 `name` 中，并将下一个处理的参数索引放在 shell 变量 `OPTIND` 中。每当你调用 shell 或 shell 脚本时，`OPTIND` 初始化为 1。

当选项需要选项-参数时，`getopts` 将其放在 shell 变量 `OPTARG` 中。

如果 `getopts` 遇到非法选项，`name` 中将被 `?`。当遇到选项结束时，`getopts` 以非零状态退出。你可以使用特殊选项 `--` 来分隔选项的结束。

## getopts

由名称操作数 `OPTIND` 或 `OPTARG` 指定的 shell 变量会影响当前的 shell 执行环境。

如果应用程序将 `OPTIND` 设置为值 1，则可以使用一组新的参数：可以是当前的位置参数或新的 `arg` 值。在单次 shell 执行环境中，如果尝试多次调用 `getopts` 且传入的参数（位置参数或 `arg` 操作数）在所有调用中不相同，或者将 `OPTIND` 值修改为 1 以外的值，则会产生未定义的结果。

## Bourne Shell

`getopts` 是 Bourne shell 的内置命令，用于解析位置参数并检查有效选项。详参见 `sh(1)`。它支持命令语法标准的所有适用规则（参见 3-10, `intro(1)`）。你应该使用它而不是 `getopt` 命令。

`optstring` 必须包含使用 `getopt` 时的命令所识别的选项字母；如果字母后面跟着逗号，则预计该选项将有一个参数（或一组参数），这些参数必须用空格隔开。

每次调用 `getopts` 时，它会将下一个待处理的参数的索引放在 shell 变量 `OPTIND` 中。每当调用 shell 或脚本时，`OPTIND` 被初始化为 1。当某个选项需要选项参数时，`getopts` 将其放在 shell 变量 `OPTARG` 中。

如果遇到非法选项，`?` 会被放在 `name` 中。

当遇到选项结束时，`getopts` 以非零退出状态退出。你可以使用特殊选项 `--` 来分隔选项的结束。

默认情况下，`getopts` 解析位置参数。如果在命令行上提供了额外的参数 `(...)`，则 `getopts` 将解析它们。

```
/usr/lib/getoptcv 读取 filename 中的脚本，将其转换为 getops 而不是 getopt，并将结果写入标准输出。
```

为了让所有命令符合 `intro(1)` 中描述的命令语法标准，它们应该使用 `getopts` 或 `getopt` 来解析位置参数并检查适用于该命令的选项。

## Korn Shell

Korn 内置命令 `getopts` 检查 `arg` 的合法选项。如果省略 `arg`，则使用位置参数。选项以 `+` 或 `-` 开头。不以 `+` 开头的选项或参数 `--` 结束选项列表。`optstring` 包含 `getopts` 识别的字母。如果字母后面跟着逗号，则预计该选项将有一个参数。你可以用空格分隔选项。

每次调用 `getopts` 时，如果 `arg` 以 `+` 开头，它会将找到的选项放在变量 `name` 中，并在前面加上 `+`。下一个 `arg` 的索引存储在 `OPTIND` 中。如果找到任何选项，将其存储在 `OPTARG` 中。

`optstring` 开头的 `-` 将无效选项的字母存储在 `OPTARG` 中，并在缺少必要选项时将 `name` 设置为 `?`。否则，`getopt` 会打印错误信息。如果没有更多选项，退出状态为非零。

下面的 shell 程序片段显示了你如何处理一个接受选项 `a` 或 `b`，以及需要选项参数的选项 `o` 的命令的参数。

```
while getopts abo: c
  case $c in
    a | b)
      FLAG=$c;
      OARG=$OPTARG;      exit 2;
    \?) echo USAGE
  esac
done
shift `expr OPTIND - 1`
```

此代码接受以下任何内容作为等效项。

```
cmd -a -b -o "xxx z yy" filename
cmd -a -b -o "xxx z yy" -- use them
cmd -ab -o xxx,yy filename
cmd -ab -o "xxx z yy" v
cmd -o xxx,z,yy -b -a filename
```

当 `getopts` 遇到未包含在 `optstring` 中的选项字母时，它会在标准错误上打印错误信息。

在当前实现下，允许以下命令语法的放宽，但你不应该使用它们，因为它们在系统未来的版本中可能不再被支持。`a` 和 `b` 是选项，选项 `o` 需要一个选项参数。以下示例违反了规则 5：带有选项参数的选项不能与其他选项分组。

```
castle$ cmd -ab -oxxx filename
```

下例示例违反了规则 6：在需要选项参数的选项之后必须有空格。

```
castle$ cmd -ab -oxxx filename
```

更改 shell 变量 `OPTIND` 的值或解析不同的参数集可能会导致意外的结果。

## Operands

- **`optstring`**: 包含命令所识别的选项字符的字符串；如果字符后面跟着冒号 `:`，则预计该选项将有一个参数，该参数应作为独立参数提供。应用程序应将选项字符及其选项参数作为独立参数指定，但 `getopts` 会将需要参数的选项字符后面的字符解释为参数，无论是否执行了此此项规定。如果在调用 `getopts` 时作为独立参数提供显式的空参数，则不需要被识别为参数；详参见 `getopt(3C)`。应用程序不得使用 `?` 和 `=` 作为选项字符。使用其他非字母数字的选项字符会产生结果。如果选项参数没有作为与选项分离的独立参数提供，则 `OPTARG` 中的值将剥离选项字符和 `-`。剥离后的选项的第一个字符是未知的，或者缺少选项参数。

- **`name`**: 变量的名称，`getopts` 命令会将该变量设置为所找到的选项字符。

`getopts` 命令默认解析传递给调用调用的 shell 过程的位置参数。如果你指定了 `args`，则将解析它们而不是位置参数。

## Usage

因为 `getopts` 会影响 shell 变量，所以通常作为 shell 内置命令提供。如果在单独的执行环境中调用它，例如：

```
(getopts abc "$0"
find -exec getopts ... \;
```
