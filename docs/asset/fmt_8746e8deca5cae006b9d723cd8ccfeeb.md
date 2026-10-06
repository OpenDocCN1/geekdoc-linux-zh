
# 658 awk

| Make | Model | Year | Miles | Price |
|---|---|---|---|---|
| ford | mustang | 65 | 45 | 10000 |
| volvo | gl | 78 | 102 | 9850 |
| ford | ltd | 83 | 15 | 10500 |
| chevy | nova | 80 | 50 | 3500 |
| fiat | 600 | 115 | 450 |
| honda | accord | 81 | 30 | 6000 |
| ford | thundbd | 84 | 10 | 17000 |
| toyota | tercel | 82 | 180 | 750 |
| chevy | impala | 65 | 85 | 1550 |
| ford | bronco | 33 | 25 | 9500 |

在下面的示例中，标题中的空白是由 TAB 组成的，这样行就能对齐。

```bash
$ cat pr2
```
```awk
BEGIN {
  print "Make      Year Miles Price"
  print "------------------"
}
```

```bash
$ awk -f prheader cars
```
```
Make      Year Miles Price
plym fury 77 73 2500
chevy nova 79 60 3000
ford mustang 65 45 10000
volvo gl 78 102 9850
ford ltd 83 15 10500
chevy nova 80 50 3500
fiat 600 115 450
honda accord 81 30 6000
ford thundbd 84 10 17000
toyota tercel 82 180 750
chevy impala 65 85 1550
ford bronco 33 25 9500
```

当你不带参数调用 `length` 函数时，它返回当前行的字符数，（内联字段分隔符。在下一个示例中，`awk` 倾向于打印每行的长度，并通过管道将 `awk` 的输出发送到 `sort`，这样 `cars` 文件的行按长度排序。报告的格式取决于 TAB 的水平对齐。每行开头的三个额外字符破坏了几行的格式，包括列表。这种情况的解决方法已涵盖。

```bash
$ awk 'print length, $0' cars | sort
```
```
19 fiat 600 65 115 450
20 ford ltd 83 15 10500
20 plym fury 77 73 2500
21 volvo gl 78 102 9850
21 chevy nova 79 60 3000
21 chevy nova 80 50 3500
22 ford bronco 33 25 9500
```

# awk 659

| 23 | chevy impala | 65 | 1550 |
| 23 | honda accord | 81 | 3000 |
| 24 | ford mustang | 45 | 10000 |
| 24 | ford thunderbd | 84 | 10 | 17000 |
| 24 | toyota tercel | 82 | 180 | 750 |

`NR` 变量包含当前行（记录）的内容。接下来的*模式*（pattern）选择所有包含超过 23 个字符的行。*动作*（action）打印所有选中行的行号。

```bash
$ awk 'length' > 23 {print NR}'
```
```
3
9
10
```

你可以将范围（,）和 `NR` 变量结合，根据行号显示一组文件。下一个示例显示了 2 到 4 行。

```bash
$ awk 'NR == 2, NR == 4' cars
```
```
chevy nova 79 60 3000
ford mustang 45 10 10000
volvo g1 78 102 9850
```

`*END*` 模式的工作方式与 `*BEGIN*` 模式类似，不同之处 `awk` 在处理完所有输入行后才会执行与其关联的动作。下面的报告仅在处理完整个数据文件后显示信息。在 `awk` 完成数据文件的处理后，`NR` 变量仍保留其值，因此与 `*END*` 模式关联的*动作*可以使用它。

```bash
$ awk 'END {print NR, "cars for sale."}' cars
```
```
12 cars for sale.
```

下一个示例使用 `*if*` 命令来更改第一个字段的值。只要 `awk` 不对记录进行任何更改，它就会保持该记录（包括分隔符）完好无。一旦它对记录进行了更改，它就会将记录中的所有分隔符更改为输出字段分隔符的值。默认的输出分隔符是空格（SPACE）。

```bash
$ cat separ_demo
```
```awk
{
if ($1 ~ /ply/) $1 = "plymouth"
if ($1 ~ /chevy/) $1 = "chevrolet"
print
}
```

```bash
$ awk -f separ_demo cars
```
```
plymouth fury 77 23 2500
chevrolet nova 79 60 3000
ford mustang 65 45 10000
volvo g1 78 102 9850
ford ltd 83 15 10500
chevrolet nova 80 50 3500
```

# 660 awk

| fiat | 600 | 65 | 115 | 450 |
| honda accord | 81 | 30 | 6000 |
| ford thunderbd | 84 | 180 | 17000 |
| toyota tercel | 82 | 180 | 750 |
| chevrolet impala | 65 | 85 | 1550 |
| ford bronco | 83 | 25 | 9500 |

你可以通过给 `OFS` 变量赋值来更改输出字段分隔符的默认值。下面的示例使用常用的序列表示法将 TAB 字符赋值给 `OFS`。此修复改进了报告的外观，并正确地对齐了列。

```bash
$ cat ofs_demo
```
```awk
BEGIN {OFS = "\t"}
{
    if ($1 ~ /plymouth/) $1 = "plymouth"
    if ($1 ~ /chev/) $1 = "chevrolet"
    print
}
```

```bash
$ awk -f ofs_demo cars
```
| plymouth fury | 77 | 73 | 2500 |
| chevrolet nova | 79 | 60 | 3000 |
| ford mustang | 65 | 45 | 10000 |
| volvo gl | 78 | 102 | 9850 |
| ford ltd | 83 | 15 | 10500 |
| chevrolet nova | 80 | 50 | 3500 |
| fiat | 600 | 115 | 450 |
| honda accord | 81 | 30 | 6000 |
| ford thunderbd | 84 | 10 | 17000 |
| toyota tercel | 82 | 180 | 750 |
| chevrolet impala | 65 | 85 | 1550 |
| ford bronco | 83 | 25 | 9500 |

你可以使用 `printf`（第 653 页）来精炼输出格式。下一个示例在程序行末尾使用反斜杠来掩盖 `awk` 中随后的换行（NEWLINE）。你可以使用这种技术将长行跨越一个或多行继续，而不影响程序的输出。

```bash
$ cat printf_demo
```
```awk
BEGIN {
    print ""
    print "Make Model Year (000) Price"
    print "--------------------------------------------------"
}
{
    if ($1 ~ /plymouth/) $1 = "plymouth"
    if ($1 ~ /chev/) $1 = "chevrolet"
    printf "%-10s %-8s %19d %5d$%2f\n",
    $1, $2, $3, $4, $5
}
```

```bash
$ awk -f printf_demo
```
| Make | Model | Year | Price |
|---|---|---|---|
| plymouth | fury | 77 | 73 | $2500.00 |
| chevrolet | nova | 79 | 60 | $3000.00 |
| ford | mustang | 65 | 45 | $10000.00 |
| volvo | gl | 78 | 102 | $9850.00 |
| ford | ltd | 83 | 15 | $10500.00 |
| chevrolet | nova | 65 | 115 | $4500.00 |
| fiat | | 81 | 30 | $6000.00 |
| honda | accord | 84 | 10 | $17000.00 |
| toyota | tercel | 82 | 180 | $750.00 |
| chevrolet | impala | 65 | 85 | $1550.00 |
| ford | bronco | 83 | 25 | $9500.00 |

下一个示例创建两个文件，一个包含 chevy 的行，另一个包含 ford 的行：

```bash
$ cat redirect_out
```
```awk
/chevy/ {print > "chevfile"}
/ford/ {print > "fordfile"}
END {print "done."}
```

```bash
$ cat chevfile
```
```
chevy nova 79 60 3000
chevy nova 80 50 3500
chevy impala 65 85 1550
```

**summary** 程序生成所有汽车的摘要。不需要前行声明； `awk` 会自动初始化它们。在 `awk` 读取所有输入数据后，它进行计算并显示。

```bash
$ cat summary
```
```awk
BEGIN {
yearsum = 0
costsum = 0
newcount = 0
}
{
yearsum += $3
costsum += $5
}
$3 > 0 {costsum += $5
newcount++}
END {
printf "Average age of cars is %.1f years\n",
yearsum/NR
printf "Average cost of cars is $%2f\n",
costsum/NR
printf "Average of newer cars is $%2f\n",
costsum/newcount
}
```

```bash
$ awk -f summary cars
```
```
Average age of cars is 13.2 years
Average cost of cars is $6216.67
Average of newer cars is $8750.00
```

下面的 `grep` 显示下一个示例使用的 `passwd` 文件格式：

```bash
$ grep 'mark' /etc/passwd
```
```
mark:x:107:100:/home/mark
```

下一个示例演示了查找字段最大值的方法。由于它处理的是用冒号（:）限制字段的 `passwd` 文件，在读取任何数据之前更改了输入分隔符（`FS`）（也可以在命令行上使用 `-v` 对 `FS` 进行赋值）。此示例读取 `passwd` 文件并确定下一个可用用户名（字段 3）。为了使此程序工作，`passwd` 文件中的数字不需要是有序的。`awk` 模式选择包含比处理过的用户 ID 大的记录。每选择一条记录，它会将新的用户数赋值给 `save` 变量。然后 `awk` 使用 `save` 的值测试后续记录的用户 ID。最后，`awk` 加上 `save` 的值并显示结果。

```bash
$ cat find_uid
```
```awk
{FS = ":"}
BEGIN
{saveit = 0}
$3 saveit {saveit = $3}
END {print "Next available UID is " saveit + 1}
```

```
Next Next available UID is 192
```

下一个示例显示了另一个基于 `cars` 文件的报告。该报告使用嵌套的 `if else` 语句根据 `price` 文件的内容替换值。程序具有模式部分——它提供了每条记录。

```bash
$ cat price_range
```
```awk
{
if ($5 < 5000) $5 = "inexpensive"
else if ($5 > 5000 && $5 < 10000) $5 = "please ask"
else if ($5 >= 10000) $5 = "expensive"
printf "%-10s %-8s   %19d %5d   %-12s\n",
$1, $2, $3, $4, $5
}
```

```bash
$ awk -f price_range cars
```
```
plym fury 1977 73 inexpensive
chevy nova 1979 60 expensive
ford mustang 1965 45 expensive
volvo g1 1978 102 please ask
ford ltd 1983 15 expensive
chevrolet nova 1980 50 inexpensive
```

| fiat | 600 | 1965 | 115 | inexpensive |
| honda accord | 1981 | 30 | 6000 | please ask |
| ford thunderbd | 84 | 180 | 17000 | expensive |
| toyota tercel | 82 | 180 | 750 | inexpensive |
| chevrolet impala | 65 | 85 | 1550 | inexpensive |
| ford bronco | 83 | 25 | 9500 | please ask |

（注：此处表格翻译内容根据上下文对齐，保持了结构）

**manuf.sh** 程序是一个更完整的 shell 脚本，包含了错误检查。此脚本列出并统计文件中列的出现次数，并在命令行上指定列数和文件名。

第一个 *awk action*（以 `{count}` 开头的那个）使用 shell 变量 `$1$` 在 `awk` 程序的中间解析数组索引。因为引号是成对的，看起来在单引号内的 `$1$` 实际上并没有被引用：`awk` 程序中的两个引号字符串包围了但不包含 `$1$`。由于 `$1$` 没有被引号，shell 用第一个命令行参数的值替换 `$1$`，从而使得 `$1$` 被被调用的 *awk* 命令解释。该行开头的符号（该行第一个单引号之前的那个符号）导致 `awk` 解释 shell 替换的内容为字段号。

```bash
$ cat manuf.sh
if [ $# -ne 1 ]; then
		echo "Usage: manuf.sh field file"
	exit 1
fi
awk '$2 
{count['$$1'']++}
{for (item in count) printf "%-20s-%20s\n",
	item, count[item]}' |
sort
```

## 644 awk

```bash
$ manuf.sh
```
```
Usage: manuf.sh field
```
```bash
$ manuf.sh 1 cars
```
```
chevy 3
fiat 1
ford 4
honda 1
plym 1
toyota 1
volvo 1
```
```bash
$ manuf.sh 3 cars
```
```
65 3
77 1
78 1
79 1
80 1
81 1
82 1
83 2
84 1
```

`word_usage` 脚本会为命令行中指定的的文件显示单词使用列表，每行一个。`tr` 工具列出标准输入中的单词，`sort` 工具将文件按使用频率最高的单词排在列表顶部。它会将使用次数相同的单词组按字母顺序进行排序。更多信息请参考 `sort`（第 856 页）和 `tr`（第 889 页）。

```bash
$ cat word_usage
```
```bash
tr -cs 'a-zA-Z' '[:\n]*' $1 |
awk
  {count[$1]++}
END {for (item in count) printf"-%15s%3s\n", item, count[item]'" |
sort +1nr -f -1
```

```bash
$ word_usage textile
```
```
the 42
file 29
fsck 27
system 22
you 22
to 21
it 17
SIZE 14
and 13
MODE 13
```

下面是一个不同格式的类似程序。该风格模仿 C 语言程序，对于更复杂的 `awk` 程序可能更容易阅读和处理。

```bash
$ cat word_count
```
```bash
tr -cs 'a-zA-Z' '[
*]' < $1 |
awk '{
  count[$1]++
}
END {
  for (item in count) {
    if (count[item] > 4) {
      printf "%-15s%3s\n", item, count[item]
    }
  }
}' |
sort -nr +0f -1
```
