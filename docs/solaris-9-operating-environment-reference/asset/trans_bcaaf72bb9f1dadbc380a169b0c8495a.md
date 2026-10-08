

# 458

# getopts

getopts 遇到未包含在 optstring 中的选项字母时，它会在标准错误输出上打印错误信息。

尽管在当前实现中允许放宽以下命令语法规则（参见 intro(1)），但你不应该使用这些规则，因为它们在系统未来的版本中可能不再被支持。

注意 `a` 和 `b` 是选项，而选项 `o` 需要一个选项参数。以下示例违反了规则 5：带有选项参数的选项不能与其他选项分组。

```
castle$ cmd abox filename
```

以下示例违反了规则 6：在选项之后必须有空格，例如

```
castle$ ab ox filename
```

更改 shell变量 `OPTIND` 的值或解析不同的参数集会导致意料之外的结果。

# Korn Shell

Korn 内置命令 `getopts` 检查 `arg` 的合法选项。如果你省略了 `arg`，则位置参数将被赋值 `+` 或 `-`。以 `--` 开头的选项或命令 `--` 将结束选项。`optstring` 包含 `getopts` 识别的字母。如果字母后面跟着冒号，则预计该选项有一个参数。你可以通过空格将选项与参数分开。

`getopts` 每次被调用时会将找到的下一个选项放入变量中，如果以 `+` 开头则会加上前缀。下一个参数的索引被设置为 `OPTIND`。如果有选项，则存储在 `OPTARG` 中。

以 `:` 开头的 `optstring` 将无效选项的字母存储在 `OPTARG` 中，并对于未知选项将 `name` 设置为 `?`，在缺少必要选项时将其设置为 `:`。否则，`getopts` 会打印错误信息。当没有更多选项时时，其退出状态为非零。

- 关于 Korn 内置命令的进一步讨论，请参见上方的 Bourne 部分。

# 操作数

optstring

包含调用 `getopts` 的命令所识别的选项字符的字符串。如果字符后面跟着冒号，则预计该选项有一个参数，该参数应作为单独参数提供。应用程序应该将选项字符及其选项参数作为单独参数指定，但 `getopts` 会解释需要参数的选项字符之后的字符是否为参数，这取决于该规范是否已定义。如果在调用 `getopts` 时没有作为单独参数提供显式参数，则不需要被识别；参见 `optopt(3)`。应用程序不得使用 `?` 或 `:` 作为选项字符。使用非字母数字的其他选项字符会产生未指定的的结果。如果选项参数没有作为选项字符的单独参数提供，则 `OPTARG` 中的值将剥离选项字符和 `-`。字符串中的第一个字符决定了当选项字符未知或缺少选项参数时 `getopts` 的行为。

# getopts 

name 被 `getopts` 命令设置为找到的选项字符的 shell 变量名。

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

# 示例

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

# 环境变量

参见 `getopts(5)` 以获取影响 `getopts` 执行的变量描述：`LC_TYPE`、`LC_MESSAGES` 和 `LC_PATH`。

- OPTIND 该变量被 `getopts` 用作下一个处理参数的索引。

- OPTARG 该变量被 `getopts` 用作下一个处理参数的索引。

# 退出状态

- 0 找到了（由 `optstring` 指定或未指定的）选项。

- >0 遇到了选项结束标志或发生了错误。

# 属性

参见 `attributes(5)` 以获取以下属性的描述：

| 属性类型 | 属性值 |
| --- | --- |
| 可性 | SUNWcsu, ksh |

# 参见

getopt(1), getoptcvt(1), intro(1), ksh(1), sh(1), getopt(3C), attributes(5), environ(5)

# 诊断

当检测到错误且 `optstring` 操作数的第一个字符不是冒号 (`:`) 时，诊断信息将以未指定的格式写入标准错误，如下：

# gettext

- 消息中识别了调用程序名。调用程序名是调用 `gettext` 命令时 shell 特殊参数 0 的值。可以使用等于 `basename "0"` 的名称。

- 如果找到未在 `optstring` 中指定的选项，则会识别此错误，并在消息中识别无效的选项字符。

- 如果找到需要选项参数的选项但未找到选项参数，则会识别此错误并在消息中识别无效的选项字符。

# gettext — 从消息数据库检索文本字符串

概要

```
/usr/bin/gettext [-d textdomain] [--domain=textdomain] [textdomain]
msgid
/usr/bin/gettext [-s] [-e] [-n] [-d textdomain | --domain=textdomain]
msgid
```

# 描述

`gettext` 从用 `msgid()` 生成的消息对象检索与字符串 `msgid` 对应的翻译字符串。消息对象源自可选参数 `textdomain`（如果存在）；否则通常 `gettext` 在 `/usr/lib/local/lang/LC_MESSAGES` 中查找其消息对象，其中 `lang` 是语言。如果存在，`TEXTDOMAIN` 环境变量将替换直到 `lang` 的路径名部分。此命令解释如 `\t`（制表符）之类的转义序列。使用 `\n` 打印反斜杠。要在单独的一行产生消息，可以在 `msgid` 末尾放置 `\n`，或结合 `printf(1)` 使用此。

当带有 `-s` 选项时，`gettext` 的行为类似于 `echo (1)`。然而，它并不是简单地将参数复制到标准输出。相反，所选类别中的这些消息会被翻译。`-s` 选项是 Solaris 9 版本中引入的。

> 注意 — 此命令等于库例 `gettext(3C)`。

# 选项

```
-d textdomain
--domain=textdomain
```

- 如果没有将 `textdomain` 指定为操作数，则从领域 `textdomain` 检索翻译消息。Solaris 9 版本新引入。

- -e 如果与 `-s` 选项一起使用，则对某些转义序列进行扩展。Solaris 9 版本新引入。

- -n 如果与 `-s` 选项一起使用，则抑制末尾换行的打印。Solaris 9 版本新引入。

