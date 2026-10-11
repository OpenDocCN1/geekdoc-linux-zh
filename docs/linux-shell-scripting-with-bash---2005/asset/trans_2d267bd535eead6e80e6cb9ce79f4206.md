

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

### until 循环

`while` 循环的对应形式是 `until` 循环。`until` 命令与 `while` 命令相同，除了它重复执行被包含的语句，直到条件*成功*，本质上等同于 `while !`。

```bash
until test -f "$INVOICE_FILE" ; do
    printf "%s\n" "Waiting for the invoice file to arrive..."
    sleep 30
done
```

将 `until` 与 `false` 命令结合使用会创建一个无限循环。
`break` 和 `continue` 命令可用于 `until` 循环。

### for 循环

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

### 嵌入式 let( ( . . . ) )

`let` 命令在表达式为零时返回状态码 1，如果表达式值为非零则返回 0。正如 `test` 命令可以用一对方括号表示以便在复合语句中更容易阅读一样，`let` 命令也有一个更容易阅读的形式：双括号。

其他编程语言中常见的 `for` 循环，是通过嵌入式 `let` 创建的，如清单 7.1 所示。

**清单 7.1 forloop.sh**

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

### 命令分组 ( {...} )

可以使用花括号 ( {...} ) 将命令分组在一起。

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

### report.bash: 报表格式化程序

report.bash 是一个读取销售数字列表并创建简单报表的脚本。销售数字文件包含产品名称、本地国家销售额和外国国家销售额。例如，report.bash 将此转换：

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

### 清单 7.2 report.bash

```bash
#!/bin/bash
#
# report.bash: simple report formatter
#
# Ken O. Burtch
# CVS: $header$
#
# The report is read from DATA_FILE. It should contain
# the following columns:
#
# Column 1: PRODUCT = Product name
# Column 2: CSALES = Country Sales
# Column 3: PSALES = Foreign Sales
#
# The script will format the data into columns, adding total and
# average sales per item as well as a item count at the end of the
# report.

# Some Linux systems use USER instead of LOGNAME
if [ -z "$LOGNAME" ] ; then # No login name?
declare -rx LOGNAME="$USER" # probably in USER
fi
shopt -s -o nounset

# Global Declarations

declare -rx SCRIPT=$0###/ # SCRIPT is the name of this script
declare -rx DATA_FILE="report.txt" # this is raw data for the report
declare -i ITEMS=0 # number of report items
declare -i LINE_TOTAL=0 # line totals
declare -i LINE_AVG=0 # line average
```

**清单 7.2 续**

```bash
declare PRODUCT        # product name from data file
declare -i CSALES         # country sales from data file
declare -i FSALES          # foreign sales from data file
declare -rx REPORT_NAME="Sales Report" # report title
# Sanity Checks

if test ! -r "$DATA_FILE" ; then
       printf "$SCRIPT: the report file is missing-aborting\n" >&2
       exit 192
fi

# Generate the report

printf "Report created on %s by %s\n" "$DATE" "$LOGNAME"
printf "\n"
printf "%s\n" "$REPORT_NAME"
printf "\n"
printf "%-12s12s12s12s12s\n" "Product" "Country" "Foreign" "Total" "Average"
printf "%-12s12s12s12s12s\n" "___" "___" "___" "___" "___"

{ while read PRODUCT CSALES FSALES ; do
      let "ITEMS+=1"
      LINE_TOTAL=$(CSALES+FSALES)
      LINE_AVG=$((CSALES+FSALES)/2)
      printf "%-12s12d12d12d12d\n" "$PRODUCT" "$CSALES" "$FSALES" \
      "$LINE_TOTAL" "$LINE_AVG"
done } < $DATA_FILE
# Print report trailer

printf "%-12s12s12s12s12s\n" "___" "___" "___" "___" "___"
printf "Total number of products: %d\n" "$ITEMS"
printf "\n"
printf "End of report\n"

exit 0
```

# 8 调试和版本控制

当我在布鲁克大学（Brock University）时，麦克夸里实验室里塞满了从已经不再使用它们的教授那里传下来的二手 Macintosh Plus 计算机。有一天，我正在为我的三年级操作系统课程编写一个程序。我当时正在处理的一个简短的 C 程序被报告为没有错误。当我运行它时，单色桌面上出现了垂直条，我的软盘弹出，计算机重启了。仔细观察后，我注意到我在一个 `if` 语句中使用了 `!=` 而不是 `==`。那个小错误造成了不可预见的结果。从那时起，我将 C 语言视为一个精神不稳定的室友；我们可能一起生活和工作，但我永远不放松警惕，以免它试图在背后捅我一刀。

不幸的是，shell 脚本几乎和 C 程序一样难以调试。与 C 语言类似，shell 命令通常假设你知道自己在做什么，并且只在有问题的行实际运行时才发出错误。除非对 shell 脚本进行彻底测试，否则错误可能潜伏数月甚至数年，直到有故障的命令最终被执行。扎实的 shell 调试工具知识对于专业脚本开发至关重要。

### Shell 调试特性

有几个有用的 Bash 开关和选项可用于追踪脚本中的问题。

`-n`（*不执行*）开关检查脚本的语法错误，而不运行它。在开发期间使用此开关来检查脚本。

```bash
$ bash -n bad.sh
bad.sh: line 3: syntax error near unexpected token `fi`
bad.sh: line 3: `fi'
```

在这个例子中，脚本的第 3 行或之前有错误。术语*token*（标记）指的是源错误附近的关键词或另一段文本。

`-o errxit` 选项在命令返回错误代码时终止 shell 脚本。例外情况是循环，因此如果命令不能返回非零状态，`if` 命令无法正常工作。仅在没有其他错误处理的最简单脚本上使用此选项；例如，如果子 shell 中发生错误，它不会终止脚本。

