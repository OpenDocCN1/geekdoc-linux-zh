
将复杂命令嵌入 `if` 命令中会使脚本难以阅读和调试；应避免这样做。在这种情况下，`rm` 命令不如它单独出现在一行上时那样突出。同样，可以在 `if` 命令内部声明变量，但这使得很难确定哪些变量存在，哪些不存在。

### `case` 命令

`case` 命令将变量与一系列值或模式进行比较。如果值或模式匹配，则执行相应的语句。之所以命名为 `case`，是因为变量是逐个（case-by-case）进行测试的。

与测试单个命令状态码的 `elif` 命令不同，`case` 测试变量的值。在测试字符串值时，`case` 命令优于冗长的 `elif` 组。

每个单独的 `case` 必须以一对分号结尾。如果没有分号，Bash 将尝试执行下一个 `case` 指定并报告错误。

```bash
printf "%s -> %s 1= delete, 2= archive. Please choose one"
read REPLY
case "$REPLY" in
    1) rm "STEMPFILE" ;;
    2) mv "STEMPFILE" "STEMPFILE.old" ;;
    *) printf "ss\n" "$REPLY was not one of the choices" ;;
esac
```

模式星号（`*`）是全匹配 `case`；它匹配之前所有 `case` 未处理的所有值。虽然这个 `case` 是可选的，但始终包含一个全匹配 `case` 是良好的设计，即使它只包含一个空语句（`:`）。

模式匹配规则遵循前一章讨论的文件通配规则。例如，垂直线可以分隔多个模式。

`case` 不会像某些计算机语言（尤其是 `C`）那样“贯穿执行”。当选择了一个 `case` 时，仅执行该 `case` 中的命令。后续 `case` 中的命令不会被执行。

### `while` 循环

有几个命令用于重复一组命令。

`while` 命令在所测试的命令成功时重复执行封装的命令。如果命令在第一次尝试时失败，则封装的命令永远不会被执行。

`while` 循环以 `done` 命令结束，而不是像你可能预期的那样使用 `elihw`。

可以使用 `true` 命令创建一个*无限*循环。因为 `true` 总是成功，所以循环将无限期地继续。

```bash
printf "%s\n" "Enter the names of companies or type quit"
while true ; do
    read -p "Company ?"  COMPANY
    if [ "$COMPANY" = "quit" ] ; then
        break
    elif test -f "orders_$COMPANY.txt" ; then
        printf "%s\n" "There is an order file from this company"
    else
        printf "%s\n" "There are no order files from this company"
    fi
done
```

`while` 循环可以通过 `break` 命令提前停止。当遇到 `break` 时，Bash 停止执行命令并“跳出”循环，开始执行循环*之后*的*第一个*命令。

`break` 后面可以跟一个数字，指示要跳出多少层嵌套循环。例如

`break 2` 会跳出当前循环以及包含当前循环的上一层循环。

`break` 的对应命令是 `continue`，它使被包含的语句的剩余部分被忽略；循环在顶部重新开始。`continue` 后面也可以跟一个数字，指示在继续之前要跳出多少层包含的语句。

### `until` 循环

`while` 循环的对应形式是 `until` 循环。`until` 命令与 `while` 命令相同，除了它重复执行被包含的语句，直到条件*成功*，本质上等同于 `while !`。

```bash
until test -f "$INVOICE_FILE" ; do
    printf "%s\n" "Waiting for the invoice file to arrive..."
    sleep 30
done
```

将 `until` 与 `false` 命令结合使用会创建一个无限循环。

`break` 和 `continue` 命令可用于 `until` 循环。

### `for` 循环

标准的 Bourne `for in 循环` 是 here file 的一种变体。`for` 命令将一系列值读入变量，并对每个值重复执行一次被包含的命令。

```bash
for FILE_PREFIX in order invoice purchase order; do
    if test -f "$FILE_PREFIX"_vendor1.txt" ; then
        printf "%%s\n" "There is a $FILE_PREFIX file from vendor l..."
    fi
done
```

如果缺少 `in` 部分，`for` 命令将为 shell 脚本的每个参数执行被包含的语句。

`break` 和 `continue` 命令可用于 `for` 循环。

由于其他 shell 特性的存在，这种 `for` 循环并不常用。

### 嵌入式 `let( ( . . . ) )`

`let` 命令在表达式为零时返回状态码 1，如果表达式值为非零则返回 0。正如 `test` 命令可以用一对方括号表示以便在复合语句中更容易阅读一样，`let` 命令也有一个更容易阅读的形式：双括号。

其他编程语言中常见的 `for` 循环，是通过嵌入式 `let` 创建的，如清单 7.1 所示。

**清单 7.1 `forloop.sh`**

```bash
#!/bin/bash
# forloop.sh: Count from 1 to 9
for (( COUNTER=1; COUNTER<10; COUNTER++ )) ; do
    printf "The counter is now %d\n" $COUNTER
done
exit 0
```

双括号中的第一个表达式在循环开始时执行。每次循环重新开始，执行第三个表达式，并检查第二个表达式。当第二个表达式返回 `false` 时，循环结束。

```bash
$ bash forloop.sh
The counter is now 1
The counter is now 2
The counter is now 3
The counter is now 4
The counter is now 5
The counter is now 6
The counter is now 7
The counter is now 8
The counter is now 9
```

### 命令分组 `{...}`

可以使用花括号 `{...}` 将命令分组在一起。

```bash
ls -1 | {
    while read FILE ; do
        echo "$FILE"
    done
}
```

在这个例子中，`ls` 命令的结果成为组内所有语句的输入。

```bash
$ test -f orders.txt && { ls -l orders.txt ; rm orders.txt; } \
    || printf "no such file"
```

如果文件 `orders.txt` 存在，该文件将被列出并删除；否则，将打印 “no such file”。只有当花括号在同一行上时，最后一个花括号命令后面的分号才是必需的。

也可以使用子 shell 对命令进行分组。子 shell 在第 9 章“参数和子 shell”中描述。

### `report.bash`: 报表格式化程序

`report.bash` 是一个读取销售数字列表并创建简单报表的脚本。销售数字文件包含产品名称、本地国家销售额和外国国家销售额。例如，`report.bash` 将此转换：

```text
binders 1024 576
pencils 472 235
rules 311 797
stencils 846 621
```

为以下报表：

```text
Report created on Thu Aug 22 18:27:07 EDT 2002 by kbutrch

Sales Report
```

| 产品 | 国家 | 外国 | 总计 | 平均 |
|:----------|--------:|--------:|------:|--------:|
| binders | 1024| 576| 1600| 800|
| pencils | 472| 235| 707| 353|
| rules | 311| 797| 1108| 554|
| stencils | 846| 621| 1467| 733|

产品总数：4

报表结束

### 清单 7.2 `report.bash`
