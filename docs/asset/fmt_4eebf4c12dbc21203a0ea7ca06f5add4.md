
# 第 12 章 gawk 模式处理语言

## 正则表达式与模式匹配

```
$ gawk '/h/' cars
chevy malibu 1999 60 3000
chevy malibu 2000 50 3500
honda accord 2001 30 6000
```

正则表达式中的脱字符（`^`）强制在行开头匹配，在本例中，即在第一个字段的开头匹配：

```
$ gawk '$1 ~ /^h/' cars
honda accord 2001 30 6000
```

括号包围字符类定义（第 829 页）。在下一个示例中，`gawk` 选择第二字段包含 `t` 的行，并显示第三、第二字段、美元符号和第五字段。“$” 和 `$5` 之间没有逗号，`gawk` 在输出中它们之间没有留空格。

### 美元符号的三种角色

下一个示例显示了美元符号在 `gawk` 程序中可以扮演三个角色。美元符号后跟数字字段。在正则表达式中，美元符号强制在行尾或字段尾匹配（`$`）。在字符串中，美元符号代表自身。

```
$ gawk '$3 ~ /\$/// {print \$3, \$2, \$5}' cars
1999 malibu 3000
1965 mustang 100000
2003 thunder 105000
2000 malibu 3500
2004 taurus 17000
```

### 数值比较

在下一个示例中，等值关系运算符（`==`）导致 `gawk` 执行数值比较，在第三字段和数字 `1985` 之间。`gawk` 选择包含字符串 `chevy` 的输入行：

```
$ gawk '/chevy/' cars
chevy malibu 1999 60 3000
chevy malibu 2000 50 3500
```

下一个示例找到价格小于 `3000` 的汽车：

```
$ gawk '2000 <= $5' cars
plym fury 1970 73 2500
chevy malibu 1999 60 3000
chevy malibu 2000 50 3500
```

### 文本比较

当你使用双引号时，`gawk` 使用 ASCII（或其他本地）排序序列进行文本比较。在下面的示例中，`gawk` 显示位于字符串 `2000` 和 `9000` 之间的字符串，这可能不是预期的结果：

```
$ gawk "2000" <= $5 && "9000" cars
plym fury 1970 73 2500
chevy malibu 1999 60 3000
chevy malibu 2000 50 3500
```

虽然输入的第五行包含 `ford`，但 `gawk` 并没有选择它，因为在处理第五行时，它正在寻找 `chevy`。

```
$
```

## --file 选项

当你编写 `gawk` 程序时，将程序放在一个文件中并在命令行中引用该文件是非常方便的。使用 `-f` 或 `--file` 选项，后跟包含 `gawk` 程序的的文件名。

接下来的 `gawk` 程序存储在一个名为 `pr_header` 的文件中，它有两个动作并使用了 `BEGIN` 模式。`gawk` 工具在处理数据文件的任何行之前，会执行与 `BEGIN` 关联的动作：它显示一个表头。第二个动作 `[print]` 没有模式部分，它会显示输入的所有行。

```
$ gawk -f pr_header cars
```

| | Make Model Year Miles Price | |
| :--- | :--- | :--- | :--- | :--- |
| plym fury | 1970 | 73 | 2500 |
| chevy malibu | 1999 | 60 | 3000 |
| ford mustang | 1965 | 45 | 10000 |
| volvo s80 | 1998 | 102 | 9850 |

下一个示例扩展了与 `BEGIN` 模式关联的动作。在之前的和之后的示例中，表头中的空白是由单个制表符组成的，因此标题行与数据列对齐。

```
$ gawk -f pr_header2 cars
```

| | Make Model Year Miles Price | |
| :--- | :--- | :--- | :--- | :--- |
| plym fury | 1970 | 73 | 2500 |
| chevy malibu | 1999 | 60 | 3000 |
| ford mustang | 1965 | 45 | 10000 |
| volvo s80 | 1998 | 102 | 9850 |

## length 函数

当你不带参数地调用 `length` 函数时，它返回当前行中的字符数，包括字段分隔符。`$0` 变量始终包含当前行的值。在下一个示例中，`gawk` 在每行前面加上长度，然后通过管道将 `gawk` 的输出发送到 `sort`（`-n` 选项指定数值排序；见第 72 页），使得汽车行按长度顺序排列：

```
$ gawk 'print length, $0' cars | sort -n
21 bmw 325i 1985 115 450
22 plymy 1970 73 2500
23 volvo s80 1998 102 9850
24 ford explor 2003 25 9500
24 toyota rav4 2002 180 750
25 chevy impala 1985 85 1550
25 chevy malibu 1999 60 3000
25 chevy malibu 2000 50 3500
25 ford taurus 2004 10 17000
26 honda accord 2001 30 6000
26 ford mustang 1965 45 10000
26 ford thunddt 2003 15 10500
```

此报告的格式依赖于 `TAB` 进行水平对齐。每行开头的三个额外字符破坏了若干行的格式。很快将介绍此这种情况的解决方法。

## NR（记录行数）

`NR` 变量包含当前记录（行）数。接下来的模式选择所有超过 24 个字符的行。动作显示每个所选行的行号。

```
$ gawk 'length > 24 {print NR}'
2
3
5
6
8
9
11
```

你可以结合范围运算符 `,` 和 `NR` 变量根据行号显示文件的组行。下一个示例显示第 2 到 4 行：

```
$ gawk 'NR == 2, NR == 4' cars
chevy malibu 1999 60 3000
ford mustang 1965 45 10000
volvo s80 1998 102 9850
```

`END` 模式的工作方式与 `BEGIN` 模式类似，只是它在处理完输入的最后一行之后执行与其关联的动作。在 `gawk` 完成处理文件后，`NR` 变量保留其值，因此 `END` 模式的动作可以使用它：

```
$ awk 'END {print NR, "cars for sale."}' cars
4 cars sale.
```

下一个示例使用 `if` 结构来扩展某些缩写。只要 `awk` 不更改记录，整个记录就会保持不变。一旦对某记录进行更改，`awk` 将将该记录中的所有分隔符更改为输出分隔符的值。默认输出分隔符是空格。

```
$ cat separ_demo
{
  if ($1 ~ /ply/) $1 = "plymouth"
  if ($1 ~ /chevy/) $1 = "chevrolet"
  print
}
```

```
$ awk -f separ_demo cars
plymouth fury 1970 73 2500
chevrolet malibu 1999 60 3000
ford mustang 1965 45 10000
volvo s80 1998 102 9850
ford thundbd 2003 15 10500
chevrolet malibu 2000 50 3500
bmw 325i 1985 115 450
honda accord 2001 30 6000
taurus 2004 10 17000
toyota rav4 2002 180 750
chevrolet Impala 1985 85 1550
ford explor 2003 25 9500
```

## 独立脚本

与不是在命令行中使用 `-f` 选项和要运行的程序名调用 `awk`，下一个示例是一个与之前示例运行相同的独立脚本。使用 `/bin/awk -f` 命令直接运行该工具。你需要对文件具有读执行权限。

```
$ chmod+rx separ_demo
$ cat separ_demo
#!/bin/awk -f
{
  if ($1 ~ /ply/) $1 = "plymouth"
  if ($1 ~ /chevy/) $1 = "chevrolet"
  print
}
```

```
$ separ_demo cars
plymouth fury 1970 73 2500
chevrolet malibu 1999 60 3000
ford mustang 1965 45 10000
```

## OFS 变量

你可以通过给 `OFS` 变量赋值来更改输出分隔符的值。接下来的示例使用转义序列给 `OFS` 分配了一个 `TAB` 字符。这提高了报告的外观，但没有正确对齐列。

```
$ cat ofs_demo
BEGIN {
	OFS = "\t"
	if ($1 ~ /ply/) $1 = "plymouth"
	if ($1 ~ /chevy/) $1 = "chevrolet"
	print
}
```

```
$ gawk -f ofs_demo cars
plymouth fury 1970 73 2500
chevrolet malibu 1999 60 3000
ford mustang 1965 45 10000
volvo s80 1998 102 9850
ford thlund 2003 15 10500
chevrolet malibu 2000 50 3500
bmw 325i 1985 115 450
honda accord 2001 30 6000
ford taurus 2004 10 17000
toyota rav4 2002 180 750
chevrolet impala 1985 85 1550
ford explor 2003 25 9500
```

你可以使用 `print` 来细化输出格式。接下来的示例在几行的末尾使用反斜杠来引用换行符（`NEWLINE`）。你可以使用这种技术将长行跨越到更多行上，而不影响程序的输出。

```
$ cat printf_demo
BEGIN {
	print ""
	print "Make      Model      Year"
	print "----------------------"
	if ($1 ~ /ply/) $1 = "plymouth"
	if ($1 ~ /chevy/) $1 = "chevrolet"
	printf "%-10s%-8s%2d\n", \
	$1, $2, $3
}
```

```
$ gawk -f printf_demo cars
Make      Model      Year
----------------------
plymouth fury 1970
chevrolet malibu 1999
ford mustang 1965
volvo s80 1998
```

## 示例

| | Make Model Year Miles Price |
| :--- | :--- | :--- | :--- |
| ford thundbd | 2003 | 15 | 10500 |
| chevrolet malibu | 2000 | 50 | 3500 |
| bmw 325i | 1985 | 115 | 450 |
| honda accord | 2001 | 30 | 6000 |
| ford taurus | 2004 | 10 | 17000 |
| toyota rav4 | 2002 | 180 | 750 |
| chevrolet impala | 1985 | 85 | 1550 |
| ford explor | 2003 | 25 | 9500 |

### 重定向

下一个示例创建了两个文件：一个包含 `chevy` 的行，一个包含 `ford` 的行：

```
$ cat redirect_out
/chevy/ {print > "chevfile"}
/ford/ {print > "fordfile"}
END {print > "done."}
```

```
$ awk -f redirect_out cars
done.
```

`$ cat chevy`

| | Make Model Year Miles Price |
| :--- | :--- | :--- | :--- |
| chevy malibu | 1999 | 60 | 3000 |
| chevy malibu | 2000 | 50 | 3500 |
| chevy impala | 1985 | 85 | 1550 |

### summary

程序生成所有汽车和新汽车的摘要报告。虽然这些要求的，但程序开始时的初始化是良好的编程习惯；`awk` 在使用变量时会自动声明并初始化。在读取所有输入数据后，`awk` 计算并显示平均值。

`$ cat summary`

```
BEGIN {
  yearsum = 0 ; costsum = 0
  newcostsum = 0 ; newcount = 0
}
yearsum += $3
costsum += $5
$3 > 2000 {newcostsum += $5 ; newcount ++}
printf "Average age of cars is %4.1f\n",
	2006 - (yearsum/NR)
printf "Average cost of cars is %7.2f\n",
	costsum/NR
printf "Average cost of newer cars is %7.2f\n",
	newcostsum/newcount
```

`$ awk -f summary cars`

Average age of cars is 13.1 years

Average cost of cars is $6216.67

Average cost of newer cars is $8750.00.

546 第 12 章 awk 模式处理语言

### 查找最大 UID

下面的 `gawk` 命令显示了 `passwd` 文件中行的格式，下一个示例将使用它：

```
$ awk '/mark/ {print}' /etc/passwd
mark:x:107:100:ext 112:/home/mark:/bin/tcsh
```

下一个示例演示了在文件中查找最大数字的技术。由于处理的是 `passwd` 文件，该文件使用冒号 (:) 作为字段分隔符；示例在读取任何数据之前更改了输入字段分隔符 (FS)。它读取 `passwd` 文件并确定下一个可用的 UID（第 3 字段）。为了让程序运行，`passwd` 文件中的数字不需要按顺序排列。

模式 ($3 > save) 会导致 `gawk` 选择用户 ID 大于之前处理过的任何用户 ID 的记录。每当它选择一个记录时，`gawk` 就会将新用户 ID 的值赋予变量 `save`。然后，`gawk` 使用 `save` 的新值来测试所有后续记录的用户 ID。最后，`gawk` 将 `save` 的值加 1 并显示结果。

```
$ cat find_uid
BEGIN
  FS = ":"
  save = 0
  {save = $3}
  print "Next available UID is " save + 1}
$3 > save
END
```

```
$ gawk -f find_uid /etc/passwd
Next available UID is 192
```

### 价格区间报告

下一个示例根据 `cars` 文件生成另一个报告。该报告使用嵌套的 `if...else` 控制结构，根据价格字段的内容替换值。该程序没有模式部分；它处理每一个记录。

```
$ cat price_range
{
  if ($5 < 5000)
    $5 = "inexpensive"
  else if (5000 <= $5 && $5 < 10000)
    $5 = "please ask"
  else if (10000 <= $5)
    $5 = "expensive"
  # 此处为注释
  printf "%-10s %%-8s %%2d %%5d %%-12s\n",
  $1, $2, $3, $4, $5
}
```

```
$ gawk -f price_range cars
plym fury 1970 73 expensive
chevy malibu 1999 60 expensive
ford mustang 1965 45 expensive
volvo s80 1998 102 please ask
ford thundbird 2003 15 expensive
chevy malibu 2000 50 expensive
bmww 3251 1985 115 expensive
```

| honda | accord | 2001 | 30 | please ask |
|---|---|---|---|---|
| ford | taurus | 2004 | 10 | expensive |
| toyota | rav4 | 2002 | 180 | inexpensive |
| chevy | impala | 1985 | 85 | inexpensive |
| ford | explor | 2003 | 25 | please ask |

## 关联数组

下一个关联数组使用 `cars` 文件中每个记录第一个字段的内容作为索引。该数组由元素 `manuf[plym]`、`manuf[chevy]`、`manuf[ford]` 等组成。每个新元素在创建时都会被初始化为 0（零）。C 语言运算符 `++` 会增加其后随变量的值。
