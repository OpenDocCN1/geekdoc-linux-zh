
## 程序变量

除了用户变量外，`gawk` 还维护程序变量。你可以同时使用用户变量和程序变量进行 12-2 模式处理。

| 变量 | 含义 |
| :--- | :--- |
| `$0` | 当前行 |
| `$1`-`$n` | 字段 |
| `FILENAME` | 文件名 |
| `FS` | 输入字段分隔符（默认为空） |
| `NF` | 字段数 |
| `NR` | 行号 |
| `OFS` | 输出字段分隔符（默认空格） |
| `ORS` | 输出分隔符（默认换行符） |
| `RS` | 输入分隔符（默认换行符） |

## 表 12-5 数值转换（续）

| | |
|---|---|
| `f` | 浮点数 |
| `g` | 使用 `f` 或 `e`，以较短的为 |
| `0` | 无符号八进制 |
| `s` | 字符字符串 |
| `x` | 无符号十六进制 |

# 控制结构

控制（流）语句会改变 `gawk` 程序中命令的执行顺序。本节将详细介绍了 `if...else`、`while` 和 `for` 控制结构。此外，`break` 和 `continue` 语句与控制结构配合使用，用以改变命令的执行顺序。有关控制结构的更多信息，请参阅第 436 页。当指定单个简单命令时，不需要在命令周围使用大括号。

## if...else

`if...else` 控制结构测试由条件返回的状态，并根据该状态转移控制权。`if...else` 结构的语法所示。`else` 部分是可选的。

- `if (condition)`
  [commands]
- `else`
  [commands]

这里展示的简单 `if` 语句没有使用大括号：

```
if ($5 <= 5000) print $0
```

接下来是一个使用简单 `if...else` 结构的 `gawk` 程序。同样，没有使用大括号。

```
$ cat if1
BEGIN {
  nam="sam"
  if (nam == "max")
    print "nam is max"
  else
    print "nam is not max, it is", nam
}
$ gawk -f if1
nam is not max, it is sam
```

## while

`while` 结构只要条件为真，就会循环并执行命令。`while` 结构的语法是：

```
while (condition)
{commands}
```

下一个 `gawk` 程序使用简单的 `while` 结构来显示 2 的幂。此示例使用了大括号，因为 `while` 循环包含多个条语句。

```
$ cat while1
BEGIN{
  n = 1
  while (n <= 5)
  {
    print n "^2", 2*n
    n++
  }
}
$ gawk -f while1
1^2 2
2^2 4
3^2 8
4^2 16
5^2 32
```

## for

`for` 控制结构的语法是：

```
for (init; condition; increment)
{commands}
```

`for` 结构通过执行 `init` 语句开始，该语句通常将计数器设置为 0 或 1。只要条件为真，它就会循环执行命令。每次循环后，它都会执行 `increment` 语句。这个 `for` `gawk` 程序与之前的 `while` 程序功能相同，但它使用了 `for` 语句，这使得程序更简单：

```
$ cat for1
BEGIN{
  for (n=1; n <= 5; n++)
    print n "^2", 2*n
}
$ gawk -f for1
1^2 2
2^2 4
3^2 8
4^2 16
5^2 32
```

`gawk` 工具支持用于关联数组的另一种 `for` 语法：

```
for (var in array)
  commands
```

该 `for` 结构遍历名为 `array` 的关联数组的元素，每次循环时，将 `array` 中每个元素的索引值赋值给 `var`。

```
END {for (name in manuf) print name, manuf[name]}
```

## break

`break` 语句将控制转移出 `for` 或 `while` 循环，终止其所在的内层循环的执行。

## continue

`continue` 语句将控制转移到 `for` 或 `while` 循环的末尾，使其所在的内层循环继续执行下一次迭代。

# 示例

## `cars` 数据文件

本节中的许多示例都适用于 `cars` 数据文件。从左到右，文件中的列包含汽车的品牌、型号、制造年份、数千英里里程和价格。文件中的所有空白都是制表符（`TABS`）。

```
$ cat cars
plym	fury	1970	73	2500
chevy	malibu	1999	60	3000
ford	mustang	1965	45	10000
volvo	s80	1998	102	9850
ford	thunder	2003	15	10500
chevy	malibu	2000	50	3500
bmw	3251	1985	115	450
honda	accord	2001	30	6000
ford	taurus	2004	10	17000
toyota	rav4	2002	180	750
Chevy	impala	1985	85	1550
ford	explorer	2003	25	9500
```

## 缺失模式

一个简单的 `gawk` 程序包含一行：一个操作。由于缺失模式，`gawk` 选择所有输入行。在不带参数使用时，命令显示选中的整行。该程序将输入复制到标准输出。

```
$ gawk '{print $0}' cars
plym fury 1970 73 2500
chevy malibu 1999 60 3000
ford mustang 1965 45 10000
volvo s80 1998 102 9850
```

## 缺失操作

下一个程序有模式，但没有显式操作。斜杠表示 `chevy` 是正则表达式。在这种情况下，`gawk` 选择包含字符串 `chevy` 的输入行：

```
$ gawk '/chevy/' cars
chevy malibu 1999 60 3000
chevy malibu 2000 50 3500
```

## 单引号

`gawk` 或 `shell` 语法都不要求在命令行加引号，但使用它们仍然是一个好主意，因为可以防止问题。如果你在命令行创建的 `gawk` 程序包含特殊字符，必须对它们加引号。始终用单引号包裹程序是确保引号了所需的字符的方法。

## 字段

下一个示例从文件中选择所有行（它没有模式）。大括号包裹操作；以便 `gawk` 将其与模式区分开。此示例显示每个选中行的第三字段（`$3`）、空格（由逗号指示）和第一字段（`$1`）：

```
$ gawk '{print $3, $1}' cars
1970, plym
1999, chevy
1965, ford
1998, volvo
2003, ford
2000, chevy
```

## 字段与模式

下一个示例包含模式和操作，选择包含字符串 `chevy` 的所有行，并显示选中的行的第三和第一字段：

```
$ gawk '/chevy/ {print $3, $1}' cars
1999, chevy
2000, chevy
```

## 正则表达式匹配

接下来 `gawk` 选择包含正则表达式匹配的行。由于没有显式操作，`gawk` 显示它选中的所有行：
