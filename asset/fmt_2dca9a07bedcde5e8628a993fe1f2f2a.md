
```bash
$ cat data5
130 120 135
160 113 140
145 170 215
$ gawk '{
> total = 0
> i = 1
> while (i < 4)
> {
>     total += $i
>     i++
> }
> avg = total / 3
> print "Average:",avg
> }' data5
Average: 128.333
Average: 137.667
Average: 176.667
$
```

`while` 语句遍历记录中的数据字段，将每个值加到 `total` 变量，然后递增计数器变量 `i`。当计数器值等于 4 时，`while` 条件变为 `FALSE`，循环终止，并落入脚本中的下一个语句。该语句计算平均值；然后打印平均值。此过程对数据文件中的每个记录重复执行。

`gawk` 编程语言支持在 `while` 循环中使用 `break` 和 `continue` 语句，允许你从循环中间跳出：

```bash
$ gawk '{
> total = 0
> i = 1
> while (i < 4)
> {
>     total += $i
>     if (i == 2)
>         break
>     i++
> }
> avg = total / 2
> print "The average of the first two data elements is:",avg
> }' data5
The average of the first two data elements is: 125
The average of the first two data elements is: 136.5
The average of the first two data elements is: 157.5
$
```

`break` 语句用于当 `i` 变量的值为 `2` 时跳出 `while` 循环。

### do-while 语句

`do-while` 语句与 `while` 语句类似，但在检查条件语句之前执行语句。以下是 `do-while` 语句的格式：

```bash
do
{
    statements
} while (condition)
```

此格式保证在评估条件之前至少执行一次语句。当需要在评估条件之前执行语句时，这非常方便：

```bash
$ gawk '{
> total = 0
> i = 1
> do
> {
>     total += $i
>     i++
> } while (total < 150)
> print total }' data5
250
160
315
$
```

该脚本读取每个记录的数据字段并求和，直到累积值达到 `150`。如果第一个数据字段超过 `150`（如第二条记录所示），脚本保证在评估条件之前至少读取第一个数据字段。

### for 语句

`for` 语句是许多编程语言中用于循环的常用方法。`gawk` 编程语言支持 C 风格的 `for` 循环：

```
for(variable assignment; condition; iteration process)
```

这有助于通过在一个语句中合并几个功能来简化循环：

```bash
$ gawk '{
> total = 0
> for( i = 1; i < 4; i++)
> {
>     total += $i
> }
> avg = total / 3
> print "Average:", avg
> }' data5
Average: 128.333
Average: 137.667
Average: 176.667
$
```

通过在 `for` 循环中定义迭代计数器，你不必像使用 `while` 语句时那样担心自己递增它。

### 格式化打印

你可能注意到 `print` 语句并没有让你对 `gawk` 如何显示数据有太多控制。你几乎只能控制输出字段分隔符 `OFS`。如果你正在创建详细的报告，通常你需要将数据放置在特定的格式和位置。

解决方案是使用格式化打印命令，称为 `printf`。如果你熟悉 C 编程，`gawk` 中的 `printf` 命令表现相同，允许你指定关于如何显示数据的详细指令。

以下是 `printf` 命令的格式：

#### printf 与格式字符串

```
printf "format string", var1, var2
```

*格式字符串* 是格式化输出的关键。它利用文本元素和*格式说明符*，精确指定了格式化输出应呈现的样子。格式说明符是一种特殊代码，用于指示显示的是哪种类型的变量以及如何显示。`gawk` 程序将每个格式说明符用作命令中列出的每个变量的占位符。第一个格式说明符匹配列出的第一个变量，第二个匹配第二个变量，依此类推。格式说明符使用以下格式：

```
%[*modifier*]control-letter
```

其中 *control-letter* 是一个单字符代码，指示将显示的数据值类型，而 *modifier* 定义了一个可选的格式化特性。**表 22.3** 列出了可在格式说明符中使用的控制字母。

##### 表 22.3 格式说明符控制字母

| 控制字母 | 描述 |
|---|---|
| c | 将数字显示为 ASCII 字符 |
| d | 显示整数值 |
| i | 显示整数值（与 d 相同） |
| e | 以科学计数法显示数字 |
| f | 显示浮点值 |
| g | 显示科学计数法或浮点数，取其中较短者 |
| o | 显示八进制值 |
| s | 显示文本字符串 |
| x | 显示十六进制值 |
| X | 显示十六进制值，但对 A 到 F 使用大写字母 |

因此，如果需要显示字符串变量，请使用格式说明符 `%s`。如果需要显示整数变量，请使用 `%d` 或 `%i`（`%i` 是 C 语言风格的十进制表示）。如果想以科学计数法显示一个大数值，请使用 `%e` 格式说明符：

```
$ gawk 'BEGIN{
> x = 10 * 100
> printf "The answer is: %e\n", x
> }
'
The answer is: 1.000000e+03
$
```

除了控制字母，还有三个你可以用来更精细控制输出的修饰符：

- `width`（宽度）：一个数值，指定输出字段的最小宽度。如果输出较短，`printf` 会使用空格填充输出，并对文本进行右对齐。如果输出长于指定宽度，则覆盖 `width` 值。
- `prec`（精度）：一个数值，指定浮点数小数点右侧的位数，或文本字符串中显示的最大字符数。
- `-`（减号）：减号表示在将数据放入格式化空间时，应使用左对齐而不是右对齐。

使用 `printf` 语句时，你可以完全控制输出的外观。例如，在“内置变量”部分，我们使用 `print` 命令来显示记录中的数据字段：

```
$ gawk 'BEGIN{FS="\n"; RS=""} {print $1,$4}' data2
Ima Test (312)555-1234
Frank Tester (317)555-9876
Haley Example (313)555-4938
$
```

你可以使用 `printf` 命令来帮助格式化输出，使其看起来更美观。首先，让我们将 `print` 命令转换为 `printf` 命令，看看会产生什么效果：

```
$ gawk 'BEGIN{FS="\n"; RS=""} {printf "%s %s\n", $1, $4}'
data2
  Ima Test    (312)555-1234
  Frank Tester  (317)555-9876
  HALEY Example  (313)555-4938
  $
```

这与 `print` 命令产生的输出相同。`printf` 命令使用 `%s` 格式说明符作为两个字符串值的占位符。

请注意，你必须手动在 `printf` 命令末尾添加换行符以强制换行。如果没有它，`printf` 命令将在后续的打印中继续使用同一行。

如果你需要在同一行打印多个内容，但使用单独的 `printf` 命令，这就很有用：

```
$ gawk 'BEGIN{FS=", "} {printf "%s  ", $1} END{printf "\n"}'
data1
  data11 data21 data31
  $
```

每个 `printf` 输出都出现在同一行上。为了能够终止该行，`END` 部分打印了一个单独的换行符。

接下来，让我们使用一个修饰符来格式化第一个字符串值：

```
$ gawk 'BEGIN{FS="\n"; RS=""} {printf "%16s  %s\n", $1, $4}'
data2
  Ima Test    (312)555-1234
  Frank Tester  (317)555-9876
  HALEY Example  (313)555-4938
  $
```
