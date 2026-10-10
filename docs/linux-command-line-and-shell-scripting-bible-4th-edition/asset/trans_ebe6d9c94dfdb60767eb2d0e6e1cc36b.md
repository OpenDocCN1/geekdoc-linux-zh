

| asort( s [ , d ] ) | 对数组 `s` 中的数据元素值进行排序。生成的数组包含索引值，替换为表示新排序顺序的连续数字。或者，如果指定了参数，新排序的数组将存储在数组 `d` 中。 |
|---|---|
| asorti( s [ , d ] ) | 基于索引值对数组 `s` 进行排序。生成的数组以索引值作为数据元素值，并以表示排序顺序的连续数字作为索引。或者，如果指定了参数，新排序的数组将存储在数组 `d` 中。 |
| gensub( r , s , h [ , t ] ) | 搜索变量 `$0` 或（如果提供）目标字符串 `t`，查找正则表达式 `r` 的匹配项。如果 `h` 是字符串且以 `g` 或 `G` 开头，则用 `s` 替换匹配文本。如果 `h` 是数字，它代表要替换的 `r` 的第几次出现。 |
| gsub( r , s [ , t ] ) | 搜索变量 `$0` 或（如果提供）目标字符串 `t`，查找正则表达式 `r` 的匹配项。如果找到，则全局替换字符串 `s`。 |
| index( s , t ) | 返回字符串 `t` 在字符串 `s` 中的索引，如果未找到则返回 0。 |
| length([ s ] ) | 返回字符串 `s` 的长度，如果未指定，则返回 `$0` 的长度。 |
| match( s , r [ , a ] ) | 返回正则表达式 `r` 在字符串 `s` 中出现的索引。如果指定了数组 `a`，它将包含匹配正则表达式的 `s` 的部分。 |
| split( s , a [ , r ] ) | 使用字段分隔符（FS）字符或（如果提供）正则表达式 `r` 将 `s` 拆分到数组 `a` 中。返回字段的数量。 |
| sprintf( format , variables ) | 使用提供的格式和变量，返回类似 `printf` 输出的字符串。 |
| sub( r , s [ , t ] ) | 搜索变量 `$0` 或目标字符串 `t`，查找正则表达式 `r` 的匹配项。如果找到，则用字符串 `s` 替换第一次出现的位置。 |
| substr( s , i [ , n ] ) | 返回 `s` 中从索引 `i` 开始的第 `n` 个字符子串。如果未提供 `n`，则使用 `s` 的剩余部分。 |
| tolower( s ) | 将 `s` 中的所有字符转换为小写。 |
| toupper( s ) | 将 `s` 中的所有字符转换为大写。 |

其中一些字符串函数相对直观：

```
$ gawk 'BEGIN{x = "testing"; print toupper(x); print length(x) }'
TESTING
7
$
```

然而，某些字符串函数可能会变得相当复杂。`asort` 和 `asorti` 函数是新的 gawk 函数，允许你基于数据元素值（`asort`）或索引值（`asorti`）对数组变量进行排序。以下是使用 `asort` 的示例：

```
$ gawk 'BEGIN{
> var["a"] = 1
> var["g"] = 2
> var["m"] = 3
> var["u"] = 4
> asort(var, test)
> for (i in test)
> print "Index:" ,i," - value:" ,test[i]
> }'
Index: 4 - value: 4
Index: 1 - value: 1
Index: 2 - value: 2
Index: 3 - value: 3
$
```

新数组 `test` 包含原始数组中新排序的数据元素，但索引值现在已更改为数值，表示正确的排序顺序。

`split` 函数是将数据字段推送到数组中以供进一步处理的好方法：

```
$ gawk 'BEGIN{ FS=", " }{
> split($0, var)
> print var[1], var[5]
> }' data1
data11 data15
 data21 data25
 data31 data35
$
```

新数组使用连续数字作为数组索引，从索引值 1 开始，包含第一个数据字段。

## 时间函数

gawk 编程语言包含几个帮助你处理时间值的函数，如表 22.6 所示。

### 表 22.6 gawk 时间函数

| **函数** | **描述** |
| :--- | :--- |
| mktime( *datespec* ) | 将格式为 YYYY MM DD HH MM SS [DST] 指定的日期转换为时间戳值 |
| strftime( *format [*, *timestamp*] )* | 使用 `date()` shell 函数格式，将当前时间戳或提供的 `timestamp` 格式化为格式化的日期和时间 |
| systime() | 返回当前时间的时戳 |

当处理包含需要比较的日期的日志文件时，通常会使用这些时间函数。通过将日期的文本表示转换为纪元时间（自 1970 年 1 月 1 日午夜以来的秒数），你可以轻松比较日期。

以下是在 gawk 程序中使用时间函数的示例：

```
$ gawk 'BEGIN{ 
> date = systime() 
> day = strftime("%A, %B %d, %Y", date) 
> print day 
> }' 
 Friday, December 26, 2014 
$ 
```

此示例使用 `systime` 函数从系统获取当前纪元时间戳，然后使用 `strftime` 函数将其转换为人类可读的格式，使用 shell 命令的日期格式字符。

## 尝试使用用户定义函数

你不仅限于使用 *gawk* 中可用的内置函数。你可以创建自己的函数以在 *gawk* 程序中使用。本节展示如何在 *gawk* 程序中定义和使用你自己的函数。

### 定义函数

要定义你自己的函数，必须使用 *function* 关键字：

```
function *name*((*variables*))
{
   *statements*
}
```

函数 *name* 必须唯一标识你的函数。你可以从调用的 *gawk* 程序向函数传递一个或多个变量：

```
function printthird()
{
   print $3
}
```

此函数将打印记录中的第三个数据字段。函数还可以使用 *return* 语句返回值：

```
*return* *value*
```

*value* 可以是一个变量，或一个评估为值的表达式：

```
function myrand(limit)
{
   *return* int(limit * rand())
}
```

你可以将函数返回的 *value* 赋值给 *gawk* 程序中的变量：

```
x = myrand(100)
```

该变量将包含函数返回的值。

### 使用你的函数

当你定义函数时，它必须单独出现在你定义任何编程部分（包括 `BEGIN` 部分）之前。这一开始可能看起来有点奇怪，但它有助于将函数代码与 `awk` 程序的其余部分分开：

```
$ awk '
> function myprint()
> {
>	printf "%-16s - %s\n", $1, $4
> }
> BEGIN{FS="\n"; RS=""}
> {
>	myprint()
> }' data2
Ima Test      - (312)555-1234
Frank Tester  - (317)555-9876
Haley Example - (313)555-4938
$
```

该函数定义了 `myprint( )` 函数，它将记录中的第一和第四数据字段格式化以供打印。然后 `awk` 程序使用该函数显示数据文件中的数据。

一旦你定义了函数，就可以尽可能多次地在代码的程序部分中使用它。当使用长算法时，这会节省大量工作。

### 创建函数库

显然，每次需要时都要重写你的 `awk` 函数并不是那么愉快的体验。然而，`awk` 提供了一种方法，允许你将函数合并到一个单一的库文件中，该文件可用于所有的 `awk` 编程。

首先，你需要创建一个包含所有 `awk` 函数的文件：

```
$ cat funclib
function myprint()
{
	printf "%-16s - %s\n", $1, $4
}
function myrand(limit)
{
	return int(limit * rand())
}
function printthird()
{
    print $3
}
$
```

`funclib` 文件包含三个函数定义。要使用它们，你需要使用 `-f` 命令行参数。不幸的是，你不能将 -f 命令行参数与内联 `gawk` 脚本结合使用，但你可以使用多个 -f 参数在同一命令行上。

因此，要使用你的库，只需创建一个包含你 `gawk` 程序的文件，并在命令行上指定库文件和你的程序文件：

```
$ cat script4
BEGIN{ FS="\n"; RS=""}
{
    myprint()
}
$ gawk -f funclib -f script4 data2
Ima Test      - (312)555-1234
Frank Tester  - (317)555-9876
Haley Example - (313)555-4938
$
```

现在，你只需要在需要使用时，将 `funclib` 文件添加到你的 `gawk` 命令行中。

### 通过实际示例进行操作

如果你需要处理数据文件中的数据值，例如汇总销售数字或计算保龄球得分，高级 `gawk` 功能会很有用。当处理数据文件时，关键是首先将相关数据记录分组，然后对相关数据执行所需的计算。

例如，让我们处理一个包含两支队伍（每队两名球员）之间比赛的保龄球得分的数据文件：

```
$ cat scores.txt
Rich Blum,team1,100,115,95
```

