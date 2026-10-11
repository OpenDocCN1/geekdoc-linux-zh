
| `gensub(r, s, h[, t])` | 在变量 `$0` 或提供的目标字符串 `t` 中搜索正则表达式 `r` 的匹配项。如果 `h` 是以 `g` 或 `G` 开头的字符串，则将匹配文本替换为 `s`。如果 `h` 是一个数字，则表示替换 `r` 的第几次出现。 |

| `gsub(r, s[, t])` | 在变量 `$0` 或提供的目标字符串 `t` 中搜索正则表达式 `r` 的匹配项。如果找到，则全局替换字符串 `s`。 |

| `index(s, t)` | 返回字符串 `t` 在字符串 `s` 中的索引，如果未找到则返回 0。 |

| `length([s])` | 返回字符串 `s` 的长度，如果未指定，则返回 `$0` 的长度。 |

| `match(s, r[,a])` | 返回正则表达式 `r` 在字符串 `s` 中出现的索引。如果指定了数组 `a`，则包含与正则表达式匹配的 `s` 的部分。 |

| `split(s, a[, r])` | 使用 `FS` 字段分隔符字符或提供的正则表达式 `r` 将 `s` 分割到数组 `a` 中。返回字段数。 |

| `sprint(f(format, variables))` | 返回类似使用提供的格式和变量执行的 `print` 输出的字符串。 |

| `sub(r, s[,t])` | 在变量 `$0` 或目标字符串 `t` 中搜索正则表达式 `r` 的匹配项。如果找到，则用字符串 `s` 替换第一次出现。 |

| `substr(s, i[,n])` | 返回 `s` 中从索引 `i` 开始的第 `n` 个字符子串。如果未提供 `n`，则使用 `s` 的剩余部分。 |

| `tolower(s)` | 将 `s` 中的所有字符转换为小写。 |

| `toupper(s)` | 将 `s` 中的所有字符转换为大写。 |

![](img/0798d50a0e5dbf1265fbda3832b3e015_584_0.png)

## 第三部分：高级 Shell 脚本

一些字符串函数相对直观：

```
$ gawk 'BEGIN{x = "testing"; print toupper(x); print length(x)}'
TESTING
7
$
```

然而，一些字符串函数可能变得相当复杂。`asort` 和 `asorti` 函数是新的 `gawk` 函数，允许你基于数据元素值（`asort`）或索引值（`asorti`）对数组变量进行排序。以下是使用 `asort` 的示例：

```
$ gawk 'BEGIN{
> var["a"] = 1
> var["g"] = 2
> var["m"] = 3
> var["u"] = 4
> asort(var, test)
> for(i in test)
>     print "Index:" ,i," - value:" ,test[i]
> }
Index: 4 - value: 4
Index: 1 - value: 1
Index: 2 - value: 2
Index: 3 - value: 3
$
```

新数组 `test` 包含原始数组的新排序数据元素，但索引值现在更改为数字值，指示正确的排序顺序。

`split` 函数是将数据字段推送到数组中进行进一步处理的绝佳方式：

```
$ gawk 'BEGIN{ FS=","
> split($0, var)
> print var[1], var[5]
> }' data1
data11 data15
data21 data25
data31 data35
$
```

新数组使用连续数字作为数组索引，从索引值 1 开始，包含第一个数据字段。

### 时间函数

`gawk` 编程语言包含几个帮助处理时间值的函数，如表 22.6 所示。

**表 22.6 `gawk` 时间函数**

| 函数 | 描述 |
| :--- | :--- |
| `mktime(datespec)` | 将指定格式的日期 `YYYY MM DD HH MM SS [DST]` 转换为时间戳值 |
| `strftime(format [, timestamp])` | 使用 `date(1)` shell 函数格式，将当前时间时间戳或提供的时间戳格式化为格式化的日期和时间 |
| `systime()` | 返回当前时间的时间戳 |

当处理包含需要比较的日期的日志文件时，时间函数通常很有用。通过将日期的文本表示转换为纪元时间（自 1970 年 1 月 1 日午夜以来的秒数），你可以轻松比较日期。

以下是在 `gawk` 程序中使用时间函数的示例：

```
$ gawk 'BEGIN{ 
> data = systime( ) 
> day = strftime("%A, %B %d, %Y", data)
> print day 
> }' 
Monday, July 28, 2025
$ 
```

此示例使用 `systime` 函数从系统获取当前纪元时间戳，然后使用 `strftime` 函数将其转换为人类可读格式，使用 shell 命令的日期格式字符。

### 试用用户定义函数

你不仅限于使用 `gawk` 中可用的内置函数。你可以创建自己的函数用于 `gawk` 程序。本节展示如何在 `gawk` 程序中定义和使用自己的函数。

![](img/0798d50a0e5dbf1265fbda3832b3e015_586_0.png)

#### 定义函数

要定义自己的函数，必须使用 `function` 关键字：

```c
function name(variables) {
    statements
}
```

函数名称必须唯一标识你的函数。你可以从调用 `gawk` 程序向函数传递一个或多个变量：

```shell
function printhird() {
    print $3
}
```

此函数将打印记录中的第三个数据字段。

函数也可以使用 `return` 语句返回值：

```shell
return value
```

值可以是一个变量或评估为值的方程：

```c
function myrand(limit) {
    return int(limit * rand())
}
```

你可以将函数返回的值赋值给 `gawk` 程序中的变量：

```shell
x = myrand(100)
```

变量将包含函数返回的值。

#### 使用你的函数

当你定义函数时，它必须单独出现在你定义任何编程部分（包括 `BEGIN` 部分）之前。这起初可能看起来有点奇怪，但它有助于将函数代码与 `gawk` 程序的其他部分分开：

```shell
$ gawk '
> function myprint() 
> { 
>     printf "%-16s - %s\n", $1, $4 
> }
> 
> BEGIN{FS="\n"; RS=""}
> { 
>     myprint() 
> }', data2
Ima Test    - (312) 555-1234
Frank Tester- (317) 555-9876
Halee Example- (313) 555-4938
$
```

该函数定义了 `myprint()` 函数，用于格式化记录中的第一个和第四个数据字段以进行打印。然后 `gawk` 程序使用该函数显示数据文件中的数据。

一旦定义了函数，你可以在代码的程序部分中根据需要多次使用它。当使用长算法时，这可以节省大量工作。

#### 创建函数库

显然，每次需要 `gawk` 函数时都要重写它们并不是那么愉快的体验。然而，`gawk` 提供了一种方法，允许你将函数组合成单个库文件，以便在所有 `gawk` 编程中使用。

首先，你需要创建一个包含所有 `gawk` 函数的文件：

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

`funclib` 文件包含三个函数定义。要使用它们，需要使用 `-f` 命令行参数。不幸的是，不能将 `-f` 命令行参数与内联 `gawk` 脚本结合使用，但你可以在同一命令行上使用多个 `-f` 参数。

因此，要使用你的库，只需创建一个包含 `gawk` 程序的文件，并在命令行上指定库文件和你的程序文件：

```
$ cat script4
BEGIN{  FS="\n"; RS="#"}
{
    myprint()
}
$ gawk -f funclib -f script4 data2
Ima Test    -   (312)555-1234
Frank Tester   -   (317)555-9876
Halee Example  -  (313)555-4938
$
```

现在，你只需要在需要使用库中定义的函数时，将 `funclib` 文件添加到 `gawk` 命令行中。
