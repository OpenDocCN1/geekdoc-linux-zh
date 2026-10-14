
更改 shell 变量 `OPTIND` 的值或解析不同的参数集可能会导致意外的 `result`。

## 456

# getopts

## Attributes

关于以下属性的描述，请参见 `attributes(5)`：

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUNwcu |
| CSI | Enabled |

## See Also

`intro(1)`, `getopts(1)`, `sh(1)`, `shell_builtins(1)`, `getopt(3C)`, `attributes(5)`

## Diagnostics

当 `getopts` 遇到未包含在 `optstring` 中的选项字母时，会在标准错误输出上打印错误信息。

# getopts — 解析实用选项

### Synopsis

```
/usr/bin/getopts optstring name [arg...]
sh getopts optstring name [argument...]
sh getopts optstring name [arg...]
```

### Description

`//usr/bin/getopts`

你可以使用 `getopts` 命令处理命令行参数并检查合法选项。你在 shell 循环中使用 `getopts` 命令是为了确保命令行选项的标准语法。

每次当调用时，`getopts` 命令会将下一个选项的值放在由 `name` 操作数指定的 shell 变量中，并将下一个要处理的参数索引放在 shell 变量 `OPTIND` 中。每当调用时，`OPTIND` 被设置为 1。当选项需要选项参数时，`getopts` 命令将其放入 shell 变量 `OPTARG` 中。如果没有找到选项，或者找到的选项没有选项参数，则 `OPTARG` 未被设置。

如果在预期选项的地方发现未包含在 `optstring` 操作数中的选项字符，则由 `name` 指定的 shell 变量被设置为问号（`?`）。如果 `optstring` 的第一个字符是冒号（`:`），则 shell 变量为找到的选项字符，但不会向标准错误写入任何内容；否则，会将 shell 变量 `OPTARG` 和诊断信息写入标准错误。这种情况被认为是在传递给调用程序的参数的方式检测到的错误，而不是 `getopts` 处理过程中的错误。

如果缺少选项参数，`getopts` 按如下方式处理它：
- 如果 `optstring` 的第一个字符是冒号，则由 `name` 指定的 shell 变量设置为冒号，shell 变量 `OPTARG` 设置为找到的选项
- 否则，由 `name` 指定的 shell 变量设置为问号，shell 变量 `OPTARG` 未被设置，并将诊断信息写入标准错误。这种情况被认为是在传递给调用程序的参数的方式检测到的错误，而不是 `getopts` 处理过程中的错误；如所述写入诊断信息，但退出状态为 0。

当遇到选项结束符时，`getopts` 命令以大于零的返回值退出；shell 变量 `OPTIND` 被设置为第一个非选项参数的索引，如果在第一个 `--` 之前没有出现其他非选项参数，则第一个 `--` 被视为选项参数；如果有非选项参数，则设置为 `$ +1`；`name` 变量被设置为

## 458

# getopts

`getopts` 遇到未包含在 `optstring` 中的选项字母时，它会在标准错误输出上打印错误信息。

尽管在当前实现中允许放宽以下命令语法规则（参见 `intro(1)`），但你不应该使用这些规则，因为它们在系统未来的版本中可能不再被支持。

注意 `a` 和 `b` 是选项，而选项 `o` 需要一个选项参数。以下示例违反了规则 5：带有选项参数的选项不能与其他选项分组。

```
castle$ cmd abox filename
```

以下示例违反了规则 6：在选项之后必须有空格，例如

```
castle$ ab ox filename
```

更改 shell 变量 `OPTIND` 的值或解析不同的参数集会导致意料之外的结果。

### Korn Shell

Korn 内置命令 `getopts` 检查 `arg` 的合法选项。如果你省略了 `arg`，则位置参数将被赋值 `+` 或 `-`。以 `--` 开头的选项或命令 `--` 将结束选项。`optstring` 包含 `getopts` 识别的字母。如果字母后面跟着冒号，则预计该选项有一个参数。你可以通过空格将选项与参数分开。

`getopts` 每次被调用时会将找到的下一个选项放入变量中，如果以 `+` 开头则会加上前缀。下一个参数的索引被设置为 `OPTIND`。如果有选项，则存储在 `OPTARG` 中。

以 `:` 开头的 `optstring` 将无效选项的字母存储在 `OPTARG` 中，并对于未知选项将 `name` 设置为 `?`，在缺少必要选项时将其设置为 `:`。否则，`getopts` 会打印错误信息。当没有更多选项时时，其退出状态为非零。

- 关于 Korn 内置命令的进一步讨论，请参见上方的 Bourne 部分。

### 操作数

`optstring`

包含调用 `getopts` 的命令所识别的选项字符的字符串。如果字符后面跟着冒号，则预计该选项有一个参数，该参数应作为单独参数提供。应用程序应该将选项字符及其选项参数作为单独参数指定，但 `getopts` 会解释需要参数的选项字符之后的字符是否为参数，这取决于该规范是否已定义。如果在调用 `getopts` 时没有作为单独参数提供显式参数，则不需要被识别；参见 `optopt(3)`。应用程序不得使用 `?` 或 `:` 作为选项字符。使用非字母数字的其他选项字符会产生未指定的的结果。如果选项参数没有作为选项字符的单独参数提供，则 `OPTARG` 中的值将剥离选项字符和 `-`。字符串中的第一个字符决定了当选项字符未知或缺少选项参数时 `getopts` 的行为。

# getopts

`name` 被 `getopts` 命令设置为找到的选项字符的 shell 变量名。

`getopts` 命令默认解析传递给调用该 shell 过程的位置参数。如果你指定了 `args`，则将解析它们而不是位置参数。

# 用

由于 `getopts` 会影响当前执行环境，它通常作为 shell 内置命令提供。如果它在 shell 或单独的命令执行环境中调用，例如以下之一：

```
(getopts abc "$@"
hup getopts...
find . -exec getopts... \
```

它将不会影响调用者环境中的 shell 变量。

> 注意 — 尽管位置参数发生了变化，但 Shell 函数与调用的 shell 共享 `OPTIND`。使用 `getopts` 解析其参数的函数通常希望在进入时保存 `OPTIND` 的值并在返回前恢复它。然而，在某些情况下，函数希望为调用 shell 修改 `OPTIND`。

### 示例

以下示例脚本解析并显示其参数。

```
aflag=
bflag=
while getopts ab: name
do
  case $name in
    a)
      aflag=1;
    b)
      bval="$OPTARG";
      printf " Usage: %s [-a] [-b] args\n"
  ?)
    exit 2;
  esac
done
if [ -z "$aflag" ]; then
  printf "Option -a specified\n"
fi
if [ -z "$bflag" ]; then
  printf 'Option -b %s specified\n' "$bval"
fi
shift $((OPTIND - 1))
printf "Remaining arguments: %s\n" "$*"
```

以下 shell 程序片段显示了你如何处理一个接受选项 `-a` 或 `-b`，以及需要选项参数的选项 `-o` 的命令参数。

```
while getopts abo: c
do
  case $c in
    a | b) FLAG=$c;
    o) OARG=$OPTARG;
    *) echo $USAGE
  esac
done
shift `expr $OPTIND - 1`
```

此代码接受以下任何等效形式：

```
cmd -a -b -o "xxx z yy" filename
cmd -a -b -o "xxx z yy" -- filename
cmd -ab -o "xxx,z,yy" filename
cmd -ab -o "xxx z yy" filename
cmd -o xxx,z,yy -b -a filename
```

## 环境变量

参见 `getopts(5)` 以获取影响 `getopts` 执行的变量描述：`LC_TYPE`、`LC_MESSAGES` 和 `LC_PATH`。

- `OPTIND` 该变量被 `getopts` 用作下一个处理参数的索引。
- `OPTARG` 该变量被 `getopts` 用作下一个处理参数的索引。

## 退出状态
