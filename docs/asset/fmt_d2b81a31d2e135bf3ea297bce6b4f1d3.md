
- `f1 -ot f2` —— （较旧）如果文件 `f1` 比 `f2` 旧，则为真

- `f1 -ef f2` —— （等效文件）如果文件 `f1` 是 `f2` 的硬链接，则为真

文件测试通常用于脚本开头的健全性检查。它们可用于检查所有文件是否存在且可读（如有必要还可写）。所有命令必须可执行（见清单 6.1）。

# 清单 6.1 `archive.bash`

```
#!/bin/bash
#
# archive.bash - 归档旧订单文件
#
# Ken O. Burtch
# CVS: $Header$
shopt -s -o nounset
## 全局声明
declare -rx SCRIPT=${0##*/}           # SCRIPT 是该脚本的名称
declare -rx who="/usr/bin/who"       # who 命令 - man 1 who
declare -rx TMP="/tmp/temp.$$"       # TMP 是一个临时文件
## 健全性检查
if test ! -x "$who" ; then
        printf "${SCRIPT}:$LINENO: the command $who is not available - aborting" >&2
        exit 192
fi
if test -f "$TMP" ; then
        if test ! -w "$TMP" ; then
                printf "${SCRIPT}:$LINENO: the temp file $TMP exists and cannot "\
"be overwritten - aborting" >&2
                exit 192
        fi
fi
```

此脚本片段确保 `who` 命令可执行，且 `TMP` 中指定的临时文件要么不存在，要么存在但可被覆盖。

## 多个测试

单个测试可以通过 `-a`（与）和 `-o`（或）开关组合在一起。前一部分中的临时文件测试可以重写为：

```
if test -f "$TMP" -a ! -w "$TMP" ; then
printf "${SCRIPT}:${LINENO}: the temp file $TMP exists and cannot "\
"be overwritten - aborting" >&2
exit 192
fi
```

这与以下写法并不完全相同

```
if test -f "$TMP" && test ! -w "$TMP" ; then
printf "${SCRIPT}:${LINENO}: the temp file $TMP exists and cannot "\
"be overwritten - aborting" >&2
exit 192
fi
```

使用 `&&` 的版本执行 `test` 命令两次，可能比使用 `-a` 开关的版本运行得更慢，因此在 `if` 表达式中优先选择 `-a` 开关而不是使用 `&&`。

只要用反斜杠转义，也可以使用括号。括号对 `shell` 有特殊含义。在某些情况下，它们是必需的。

一种往往使 `shell` 程序员困惑的情况是当 `not` 运算符与 `-a` 或 `-o` 开关混合使用时。在大多数计算机语言中，`not` 作为一元运算符具有优先级并首先执行。在 `Bash` 中，`-a` 和 `-o` 的优先级高于 `not` 运算符，导致以下测试始终为假：

```
if test ! -f "$TMP" -o -f "$TMP" ; then
```

`Bash` 将此命令解释为“如果文件既不存在又不存在”。这种怪异行为符合 `POSIX` 标准。要获得预期结果，必须使用括号。

```
if test \( ! -f "$TMP" \) -o -f "$TMP" ; then
```

方括号是 `test` 命令的另一种形式。使用方括号可以使你的 `if` 命令更易读。

```
if [ -f "$TMP" -a ! -w "$TMP" ] ; then
printf "${SCRIPT}:${LINENO}: the temp file $TMP exists and cannot "\
"be overwritten - aborting" >&2
exit 192
fi
```

方括号版本在各方面都与普通的 `test` 命令相同。`Korn shell` 引入了 `test` 命令的一种变体，使用双方括号。`Bash` 为了兼容性支持这种变体。`Korn shell` 的 `test` 不会在括号之间执行单词拆分或路径名扩展，使得变量替换周围的双引号变得不必要。

```
if [ [ -f $FILE ] ] ; then
printf "%s\n" "The file exists"
fi
```

它还增强了模式匹配功能，但缺乏 `Bash` `test` 命令的许多特性。除非你正在将 `Korn shell` 脚本移植到 `Bash`，否则强烈建议不要使用 `Korn shell` 的 `test` 命令。

## 字符串

`test` 命令可以比较两个字符串。

- `-z s`—*(零长度)* 如果字符串为空，则为真
- `-n s`（或仅 `s`）—*(非空)* 如果字符串不为空，则为真
- `s1 = s2`—如果字符串 `s1` 等于 `s2`，则为真
- `s1 != s2`—如果字符串 `s1` 不等于 `s2`，则为真
- `s1 < s2`—如果字符串 `s1` 小于 `s2`，则为真
- `s1 > s2`—如果字符串 `s1` 大于 `s2`，则为真

```bash
DAY=`date '+%a'`
if [ "$DAY" = "Mon" ] ; then
    printf "The weekend is over...get to work!\n"
fi
```

`-z`（*零长度*）和 `-n`（*非零长度*）选项分别是 `=` 和 `!=` 的简写形式。请注意，没有大于等于或小于等于运算符。你可以通过结合两个测试并使用 `-a` 选项来模拟这些运算符。

如果你习惯使用其他计算机语言，请记住 `test` 命令中使用的引号并非用于字符串界定，而是用于特殊字符处理。

由于小于号和大于号运算符也用于 `shell` 的重定向，因此必须将这些运算符加上引号，以防止 `Bash` 将其解释为重定向符号，而不是传递给 `test` 命令。

```bash
COMPANY="Athabasca"
if [ "$COMPANY" \< "M" ] ; then
    printf "The company name begins with a letter less than M\n"
fi
```

字符串比较的一个常见用途是测试 `shell` 标志变量。*标志*是用于指示特定条件是否为真的变量。它们提供了一种记住先前测试的方法。

可以使用任意一对值来表示标志的状态，例如 `true` 和 `false`，或者 `yes` 和 `no`。然而，当标志包含诸如 `"NO"` 这样的意外字符串时，这可能会导致条件歧义。传统上，如果变量包含除空字符串以外的任何内容，该条件被视为真。

```bash
WEEKEND=
DAY=`date '+%a'`
if [ "$DAY" = "Sat" -o "$DAY" = "Sun" ] ; then
    WEEKEND=1
fi

# 要确定是否为周末，使用 -n（非空）和 -z（空）。
if [ -n "$WEEKEND" ] ; then
    printf "The weekend is here\n"
else
    printf "It isn't the weekend\n"
fi
```

## 算术表达式

内置的 `let` 命令执行数学计算。`let` 期望一个包含变量、等号和待计算表达式的字符串。结果将被赋值给该变量。

```bash
$ let "SUM=5+5"
$ printf %d "$SUM"
10
```

在字符串中扩展变量名时不需要使用 `$`。`let` 理解等号右侧出现的任何变量都需要将其值代入表达式中。

```bash
$ let "SUM=SUM+5"
$ printf %d "$SUM"
15
$ let "SUM=SUM-5"
$ printf %d "$SUM"
10
```

可选的美元符号是 `let` 命令的一个特殊功能，不适用于其他命令。

如果变量使用 `-i` 选项声明为整数，则 `let` 命令是可选的。

```bash
$ declare -i SUM
$ SUM=SUM+5
$ printf %d "$SUM"
15
```

如果 `SUM` 是一个字符串变量，它将被赋值为字符串 `"SUM+5"`：

```bash
$ unset SUM
$ declare SUM=0
$ SUM=SUM+5
$ printf %s "$SUM"
SUM=5
```

出现在 `let` 表达式中的任何特殊字符都必须加上引号，以防止 `Bash` 对其进行扩展。

`let` 命令提供四个基本数学运算符，外加一个取模运算符。只允许整数表达式（不允许小数点）。
