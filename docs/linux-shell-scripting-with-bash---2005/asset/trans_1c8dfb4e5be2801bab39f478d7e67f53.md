

- `\f` — 换页符
- `\n` — 换行符
- `\r` — 回车符
- `\t` — 水平制表符
- `\v` — 垂直制表符
- `\\` — 字面意义的反斜杠
- `\'` — 单引号
- `\nnn` — 字符的 ASCII 八进制值（最多三位数字）
- `\xnnn` — 字符的 ASCII 十六进制值（最多三位数字）

## 7 复合命令

**除了最简单的脚本，** 你很少想要执行所有命令。执行一组命令而忽略另一组命令，或者将一组命令重复执行几次，会非常有用。*复合命令* 是封装一组其他命令的命令。

为了提高可读性，封装的命令会被缩进，以明确其执行依赖于复合命令。我的一位主管曾抱怨我偶尔每行缩进的空格数比他所坚持的标准少一个空格。（我不得不把尺子抵在屏幕上查看是否属实。）我认为这是个次要问题，因为他转向另一位程序员指出，该程序在输入零时就会崩溃。

复合命令始终由两条括住内部命令的命令组成。结束命令通常是第一条命令名称的倒序拼写。听起来神秘的 **case** 命令实际上是复合命令 *case* 的结束命令。

### 命令状态码

每个 Linux 命令都返回一个 *状态码*（或退出状态），这是一个 0 到 255 之间的数字，指示命令遇到了什么问题。状态码为零表示最后一个命令成功运行。任何其它状态码都表示某种错误。

状态码包含在变量 `$?` 中

```
$ unzip no_file.zip
unzip:  cannot find no_file.zip, no_file.zip.zip or no_file.zip.ZIP.
$ printf "%d\n" " $?"
9
```

当 **unzip** 命令找不到要解压缩的文件时，返回的状态码为 9（表示错误）。

非正式的 Linux 惯例使用 127 及以下的代码作为 Linux 标准错误代码。在这种情况下，`ls` 返回了状态码 9，即 Linux 中“无效文件号”的错误代码。完整的 Linux 错误代码列表见附录 D，“错误代码”。

如果命令被信号中断，Bash 会返回状态码 128 加上信号编号。因此，用户定义的错误代码应在 191 以上，且不应与 Bash 为最后一个 Linux 信号（编号 63）返回的代码冲突。信号代码列表见附录 E，“信号”。

```
if test ! -x "$who" ; then
    printf "${SCRIPT}:${LINE#}o: the command $who is not available - \
          "aborting\n" >&2
    exit 192
fi
```

不幸的是，大多数 Linux 命令仅仅返回 1 或 0 来表示失败或成功。如果脚本在发生错误时立即停止，这通常就是所需的全部信息。特定的错误消息仍会显示在标准输出上。

```
$ ls po_1473.txt
po_1473.txt
$ printf '%d\n' $?
0

$ ls no_file
no_file not found
$ printf '%d\n' $?
1
```

状态码不同于第 6 章“逻辑表达式”部分中讨论的由 `let` 命令返回的真值。在 `let` 中，`false`（比较失败）的值为 0。这遵循 C 等计算机语言的惯例。然而，状态码 0 表示成功，而不是失败。

```
$ let "RESULT=1>0"
$ printf '%d %d\n' "$RESULT" $?
1 0

$ test 1 -gt 0
$ printf '%d\n' $?
0
```

`let` 将 1 赋值给 RESULT，表示 1 大于 0。`test` 命令返回状态码 0，表示 1 大于 0。此外，`let` 命令本身的状态码为 0，表示 `let` 命令成功执行了比较。

这些相反的代码和惯例可能导致难以调试的错误。Bash 有两个内置命令，称为 `true` 和 `false`。这些命令返回的是状态码，而不是 `let` 的真值。

```
$ true
$ printf "%d\n" "$?"
0
$ false
$ printf "%d\n" "$?"
1
```

true 分配成功状态码（0）。false 分配错误状态码（1）。
感到困惑了吗？

如果你需要保存逻辑比较的成功结果，最好使用 test 命令以保持一致性。大多数 shell 命令期望的是状态码，而不是真值。

在管道中，可以同时运行几个命令。从管道返回的状态码是最后一个命令的状态码。在下面的示例中，状态码对应的是 wc 命令，而不是 ls。

```
$ ls badfile.txt | wc -l
ls: badfile.txt: No such file or directory
0
$ printf "%d\n" "$?"
0
```

尽管 ls 报告了错误，但管道的结果为零，因为 wc 成功计数了零行。

Bash 还定义了一个名为 PIPESTATUS 的数组，它包含最后一个管道中每个命令的单独状态码。

```
$ ls badfile.txt | wc -l
ls: badfile.txt: No such file or directory
0
$ printf "%d %d\n" "${PIPESTATUS[0]}" "${PIPESTATUS[1]}"
1 0
```

$? 基本上是 PIPESTATUS 最后一个值的别名。

命令或管道前可以加 ! 来否定状态码。如果状态为 0，它变为 1。如果状态大于 0，它变为 0。

### if 命令

if 命令根据其他命令返回的状态码，执行两个或更多替代命令系列中的一个。

通常，if 语句与 test 命令配合使用。

```
NUM_ORDERS=`ls -l | wc -l`
if [ "$NUM_ORDERS" -lt "$CUTOFF" ]; then
    printf "%s\n" "Too few orders...try running again later"
    exit 192
fi
```

这个示例统计以文件形式存储在目录中的客户订单数量。如果当前目录中的订单文件数量不足，脚本将执行 `then` 和 `fi` 关键字之间的语句，打印消息并停止脚本。

`then` 前的分号是必需的。虽然 `then` 实际上是一个独立的命令，但它与 `if` 配合使用。因为它们在同一行上，所以需要分号来分隔命令。

`if` 命令可以有一个 `else` 部分，该部分仅在条件失败时执行。

```
NUM_ORDERS=`ls -l | wc -l`
if [ "$NUM_ORDERS" -lt "$CUTOFF" ]; then
    printf "\n\n" "Too few orders...but will process them anyway"
else
    printf "\n\n" "Starting to process the orders"
fi
```

`if` 命令可以嵌套在其他 `if` 命令内部。

```
NUM_ORDERS=`ls -l | wc -l`
if [ [ "$NUM_ORDERS" -lt $TOOFEW ]]; then
    printf "\n\n" "Too few orders...but will process them anyway"
else
    if [ [ "$NUM_ORDERS" -gt $TOOMANY ]]; then
        printf "\n\n" "There are many orders.  Processing may take a long time"
    else
        printf "\n\n" "Starting to process the orders"
    fi
fi
```

命令不能交叉嵌套；内部 `if` 必须始终在外部 `if` 之前完成。

为了在一组替代项中选择，`if` 命令可以有一个 `elif` 部分。`elif` 是 `else if` 的简写，减少了不必要的 `if` 嵌套。`elif` 部分后面可以跟随一个最终的 `else` 部分，如果存在该部分，它仅在没有替代项时执行。结合这些想法，你可以将前面的示例重写如下。

```
NUM_ORDERS=`ls -l | wc -l`
if [ "$NUM_ORDERS" -lt "$TOOFEW" ]; then
    printf "\n\n" "Too few orders...but will process them anyway"
elif [ "$NUM_ORDERS" -gt "$TOOMANY" ]; then
    printf "\n\n" "There are many orders.  Processing may take a long time"
else
    printf "\n\n" "Starting to process the orders"
fi
```

`if` 命令不一定非要与 `test` 命令一起使用。它可以运行并测试任何命令的状态码。

```
if rm "STEMPFILE" ; then
    printf "%s\n" "SSCRIPT:temp file deleted"
else
    printf "%s - status code $d\n" \
    "SSCRIPT:$LINENO: unable to delete temp file" $2
fi
```

将复杂命令嵌入 if 命令中会使脚本难以阅读和调试；应避免这样做。在这种情况下，rm 命令不如它单独出现在一行上时那样突出。同样，可以在 if 命令内部声明变量，但这使得很难确定哪些变量存在，哪些不存在。

### case 命令

case 命令将变量与一系列值或模式进行比较。如果值或模式匹配，则执行相应的语句。之所以命名为 case，是因为变量是逐个（case-by-case）进行测试的。

与测试单个命令状态码的 elif 命令不同，case 测试变量的值。在测试字符串值时，case 命令优于冗长的 elif 组。

每个单独的 case 必须以一对分号结尾。如果没有分号，Bash 将尝试执行下一个 case 指定并报告错误。

```
printf "%s -> %s 1= delete, 2= archive. Please choose one"
read REPLY
case "$REPLY" in
    1) rm "STEMPFILE" ;;
    2) mv "STEMPFILE" "STEMPFILE.old" ;;
    *) printf "ss\n" "$REPLY was not one of the choices" ;;
esac
```

模式星号 (\*) 是全匹配 case；它匹配之前所有 case 未处理的所有值。虽然这个 case 是可选的，但始终包含一个全匹配 case 是良好的设计，即使它只包含一个空语句 (:)。

模式匹配规则遵循前一章讨论的文件通配规则。例如，垂直线可以分隔多个模式。

case 不会像某些计算机语言（尤其是 C）那样“贯穿执行”。当选择了一个 case 时，仅执行该 case 中的命令。后续 case 中的命令不会被执行。

### while 循环

有几个命令用于重复一组命令。

while 命令在所测试的命令成功时重复执行封装的命令。如果命令在第一次尝试时失败，则封装的命令永远不会被执行。

