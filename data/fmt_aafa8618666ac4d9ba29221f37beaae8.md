
`FNR` 和 `NR` 变量彼此相似，但略有不同。`FNR` 变量包含当前数据文件中已处理的记录数。`NR` 变量包含已处理的总记录数。让我们看几个例子来了解这种区别：

```
$ gawk 'BEGIN{FS=","}{print $1,"FNR="FNR}' data1 data1
data11 FNR=1
data21 FNR=2
data31 FNR=3
data11 FNR=1
data21 FNR=2
data31 FNR=3
$
```

在这个示例中，`gawk` 程序命令行定义了两个输入文件。（它指定了同一个输入文件两次。）脚本打印第一个数据字段值以及 `FNR` 变量的当前值。请注意，当 `gawk` 程序处理第二个数据文件时，`FNR` 的值重置为 1。

现在，让我们添加 `NR` 变量，看看会产生什么结果：

```
$ gawk '
> BEGIN {FS=","}
> {print $1, "FNR="FNR, "NR="NR}
> END{print "There were",NR,"records processed"}' data1 data1
data11 FNR=1 NR=1
data21 FNR=2 NR=2
data31 FNR=3 NR=3
data11 FNR=1 NR=4
data21 FNR=2 NR=5
data31 FNR=3 NR=6
There were 6 records processed
$
```

当 `gawk` 处理第二个数据文件时，`FNR` 变量的值被重置，但 `NR` 变量保持其对第二个数据文件的计数。结论是，如果你只使用一个数据文件作为输入，`FNR` 和 `NR` 的值将是相同的。如果你使用多个数据文件作为输入，`FNR` 的值将为每个数据文件重置，而 `NR` 的值将在所有数据文件中保持计数。

### 注意

> 你会注意到，在使用 `gawk` 时，`gawk` 脚本通常会变得比你的 shell 脚本的其余部分更大。在本章的示例中，为了简单起见，我们只是直接从命令行运行 `gawk` 脚本，利用 shell 的多行功能。当你在 shell 脚本中使用 `gawk` 时，你应该将不同的 `gawk` 命令放在单独的行上。这样做会让你更容易阅读和跟踪，而不是试图将所有内容挤在 shell 脚本的一行中。此外，如果你发现自己在不同的 shell 脚本中使用相同的 `gawk` 脚本，请记得

你可以将 `gawk` 脚本保存到一个单独的文件中，并使用 `-f` 参数来引用它（参见第 19 章）。

### 用户定义变量

就像其他任何受人尊敬的编程语言一样，`gawk` 允许你在程序代码中定义自己的变量。`gawk` 的用户定义变量名可以是任意数量的字母、数字和下划线，但不能以数字开头。同时记住 `gawk` 变量名是区分大小写也很重要。

#### 在脚本中为变量赋值

在 `gawk` 程序中为变量赋值类似于在 shell 脚本中进行，使用赋值语句：

```
$ gawk '
> BEGIN{
> testing="This is a test"
> print testing
> }'
This is a test
$
```

`print` 语句的输出是变量 `testing` 的当前值。与 shell 脚本变量类似，`gawk` 变量可以保存数值或文本值：

```
$ gawk '
> BEGIN{
> testing="This is a test"
> print testing
> testing=45
> print testing
> }'
This is a test
45
$
```

在这个例子中，`testing` 变量的值从文本值变为了数值。

赋值语句还可以包含数学算法来处理数值：

```
$ gawk 'BEGIN{x=4; x= x * 2 + 3; print x}'
11
$
```

正如你从这个例子中看到的，`gawk` 编程语言包含用于处理数值的标准数学运算符。这些可以包括取模符号 (`%`) 和指数符号（使用 `^` 或 `**`）。

#### 在命令行上为变量赋值

你还可以使用 `gawk` 命令行来为 `gawk` 程序中的变量赋值。这允许你在正常代码之外设置值，从而随时更改值。下面是一个使用命令行变量来显示文件中特定数据字段的示例：

```
$ cat script1
BEGIN{FS=",",}
{print $n}
$ gawk -f script1 n=2 data1
data12
data22
data32
$ gawk -f script1 n=3 data1
data13
data23
data33
$
```

此功能允许你改变脚本的行为，而不需要实际修改脚本代码。第一个示例显示文件中的第二个数据字段，而第二个示例显示第三个数据字段，只需在命令行中设置 `n` 变量的值即可实现。

使用命令行参数定义变量值存在一个问题。当你设置变量时，该值在代码的 `BEGIN` 部分中不可用：

```
$ cat script2
BEGIN{print "The starting value is",n; FS=","}
{print $n}
$ gawk -f script2 n=3 data1
The starting value is
data13
data23
data33
$ 
```

你可以通过使用 `-v` 命令行参数来解决这个问题。这允许你指定在代码 `BEGIN` 部分之前设置的变量。`-v` 命令行参数必须放置在命令行中脚本代码之前：

```
$ gawk -v n=3 -f script2 data1
The starting value is 3
data13
data23
data33
$ 
```

现在，`$n` 变量在代码 `BEGIN` 部分期间包含了在命令行中设置的值。

### 使用数组

许多编程语言提供数组，用于在单个变量中存储多个值。`gawk` 编程语言使用关联数组提供数组功能。

关联数组与数值数组不同，因为其索引值可以是任何文本字符串。你不需要使用连续数字来识别数组中包含的数据元素。相反，关联数组是由引用值的字符串集合组成的。每个索引字符串必须是唯一的，并唯一地标识分配给它的数据元素。如果你熟悉其他编程语言，这与哈希映射或字典的概念相同。

以下章节将带你了解如何在 `gawk` 程序中使用关联数组变量。

#### 定义数组变量

你可以使用标准赋值语句来定义数组变量。数组变量赋值的格式为 `var[index] = element`，其中 `var` 是变量名，`index` 是关联数组的索引值，`element` 是数据元素值。以下是 `gawk` 中一些数组变量的示例：

- `capital["Illinois"] = "Springfield"`
- `capital["Indiana"] = "Indianapolis"`
- `capital["Ohio"] = "Columbus"`

当你引用数组变量时，必须包含索引值以获取适当的数据元素值：

```
$ gawk 'BEGIN{
> capital["Illinois"] = "Springfield"
> print capital["Illinois"]
> }'
Springfield
$ 
```

当你引用数组变量时，显示数据元素值。这也适用于数值型数据元素值：

```
$ gawk 'BEGIN{
> var[1] = 34
> var[2] = 3
> total = var[1] + var[2]
> print total
> }'
37
$ 
```

正如你从这个例子中看到的，你可以在 `gawk` 程序中使用数组变量，就像使用任何其他变量一样。

#### 遍历数组变量

关联数组变量的问题在于你可能无法知道索引值是什么。与使用连续数字作为索引值的数值数组不同，关联数组的索引可以是任何东西。

如果你需要在 `gawk` 中遍历关联数组，你可以使用 `for` 语句的特殊格式：

```
for (var in array)
{
    statements
}
```

`for` 语句循环执行 `statements`，每次将变量 `var` 分配为数组关联数组中的下一个索引值。重要的是要记住，该变量是索引的值，而不是数据元素值。你可以轻松通过将变量作为数组索引来提取数据元素值：

```
$ gawk 'BEGIN{
> var["a"]  = 1
> var["g"]  = 2
> var["m"]  = 3
> var["u"]  = 4
> for (test in var)
> {
> print "Index:",test," - Value:",var[test]
> }
> }'
Index: u - Value: 4
Index: m - Value: 3
Index: a - Value: 1
Index: g - Value: 2
$
```

请注意，索引值不是以任何特定顺序返回的，但它们都引用适当的数据元素值。这在某种程度上是重要的，因为你不能指望返回的值以相同的顺序出现，只能保证索引和数据值相匹配。

#### 删除数组变量

从关联数组中删除数组索引需要一条特殊命令：

```
delete  array[index]
```

`delete` 命令从数组中删除关联索引值及其关联的数据元素值：
