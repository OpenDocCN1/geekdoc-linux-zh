
# 第 12 章：使用 awk 进行过滤和编程

```
$ $3 == "director" && $6 > 12000 {
    printf "%4d %-20s-12s %d\n", count, $2, $3
}
```

注意我们没有使用任何引号来包裹 `awk` 程序。你可以使用 `-f filename` 使用 `awk`：

```
awk -F: empawk.awk empn.lst
```

如果你使用 `-f` 选项使用 `awk`，确保文件中存储的程序没有被引号。`awk` 只有在命令行中指定程序或整个 `awk` 命令位于 shell 脚本中时使用引号。

> **注意**: `BEGIN` 和 `END` 部分

如果你想在第一行之前打印内容（例如标题），可以有效使用 `BEGIN` 部分。同样，`END` 部分在处理完成后打印总和很有用。

`BEGIN` 和 `END` 部分是可选的，形式如下：

```
BEGIN { action }
END { action }
```

都需要大括号。存在时，这些部分由 `awk` 程序体分隔。可以使用它们在开头打印合适的标题，在结尾打印平均工资。将此 `awk` 程序存储在单独的文件 `empawk.awk` 中（图 12.2）。

像 shell 一样，`awk` 使用 `#` 提供注释。`BEGIN` 部分打印带有制表符 `\t\t` 的合适标题，而 `END` 部分打印所选行的平均工资 (`tot/count`)：

```
$ awk -F empawk.awk empn.lst
Employee abstract
```

| | | |
| :--- | :--- | :--- |
| 1 bill johnson | director | 130000 |
| 2 berry wood | chairman | 160000 |
| 3 gordon longterm | director | 140000 |
| 4 deryk o'bryen | director | 125000 |

平均工资是 138750

### 图 12.2 empawk2.awk

```
BEGIN {
    printf "\t\tEmployee abstract\n\n"
    $6 > 12000 {      # 增加序号和工资的变量
        count++; tot+=$6  # 一行中的多次赋值
        printf "%3d-20s%-12s %d\n", count, $2, $3, $6
    }

END {
    printf "\n\tThe average salary is %6d\n", tot/count
}
```

和所有的过滤器一样，省略文件名时 `awk` 读取标准输入。我们可以通过在 `BEGIN` 部分完成所有工作，让 `awk` 的行为像一种简单的脚本语言。这就是你执行浮点算术的方法：

```
$ awk 'BEGIN { printf "%f\n", 22/7 }'
3.142857
```

这是你可以用 `bc` (13.10.2) 做但不能用 `expr` (13.10.1) 做的事。取决于你的 `awk` 版本，提示符可能返回或不返回，这意味着 `awk` 可能仍在读取标准输入。使用 `Ctrl-d` 返回提示符。

始终在与部分（`BEGIN` 或 `END`）相同的行开始左大括号。如果不这样做，`awk` 将产生一些奇怪的消息！

## 12.8 位置参数

如果将 `empawk2.awk` 中的 `120000` 替换为变量，程序就有更通用的形式。shell 脚本使用特殊参数 `$1`、`$2` 等表示传递给脚本的命令行参数。当你运行带参数的 shell 脚本时，该参数在脚本内部通过 `$1` 访问。放置在脚本中的 `awk` 程序通过 `'$1'` 访问它，但只有当整个 `awk` 命令（而不只是程序）存储在脚本中时（例如 `empabs.sh`）。让我们对包含整个 `awk` 命令的脚本做一个微改：

```
$6 > '$1' 代替 $12000
```

你现在能够构建一个设施来查询数据库，选择符合特定筛选标准的行，例如工资超过某个数字的行。通过少量的 `awk` 编程，你还可以计算所选人员的平均工资。你无法使用 `grep` 或 `sed` 完成所有这些操作；它们无法执行计算。

## 12.9 数组

数组也是一种变量，区别在于该变量可以存储一组值或元素。每个元素通过一个称为索引（index）的下标来访问。`awk` 中的数组与其他编程语言中的数组不同之处在于以下方面：

- 它们没有正式定义。数组在被使用的一刻被认为存在。
- 除非显式初始化，否则数组元素被初始化为零或空字符串。
- 数组会自动扩展。
- 索引可以是几乎任何内容；甚至可以是一个字符串。

我们将在第 12.10 节讨论最后一点。现在，我们将使用 `BEGIN` 部分在打印这些值之前，设置三个下标为 1、2 和 1000 的数组元素。我们使用一个较大的索引值向数组中插入一个元素，并删除了一个数组元素：

```
$ awk BEGIN {
    mon[1] = "jan"; mon[2] = "feb"; mon[1000] = "illegal month";
    printf("Month 1 is %s and month 1000 is %s\n", mon[1], mon[1000]);
    printf("Month 500 is %s and month 5000 is %s\n", mon[500], mon[5000]);
}
```

```
# delete mon[1]
delete mon[1]
printf("Month 2 remains %s\n", mon[2]);
```

Month 1 is jan and month 1000 is illegal month

Month 500 is feb

Month 2 remains feb

注意 `mon[]` 数组的下标 500 和 5000 指向空字符串。删除数组元素只会将其设置为空字符串，而不会重新排列元素。

在程序 `awk3.awk`（图 12.3）中，我们使用数组来存储销售和营销人员的工资总和佣金（工资的 20%）总和。该程序输出了工资两个元素的平均值：

```
$ -f empawk3.awk empn.lst
```

| 工资 | 佣金 |
| :--- | :--- |
| 平均值 105625 | 21125 |

程序员发现这个程序非常易用，因为 `awk` 简化了许多在 C 中需要显式指定的内容。没有类型声明，没有初始化，也没有语句终止符。

### 图 12.3 empawk3.awk

```
BEGIN { FS = "; printf "%-44s\n", "Salary", "Commission" }
$4 ~marketing/ { commission += $6; tot[1] += $6; tot[2] += commission; count++ }
END { printf "\tAverage %5d\n", tot[1]/count, tot[2]/count }
```

### 12.9.1 关联数组（哈希数组）

尽管我们在 `mon[]` 和 `tot[]` 数组中使用了整数作为下标，但 `awk` 并不将索引视为整数。`awk` 数组是关联的，信息以键值对的形式存储。索引是键，在内部被保存为字符串。当我们使用 `mon[1] = "January"` 设置数组元素时，`awk` 将数字 1 转换为字符串。数组元素的存储没有指定的顺序。如下所示，索引 "1" 来自 "01"：

```
$ awk BEGIN {
    direction["N"] = "North"; direction["S"] = "South"
    direction["E"] = "East"; direction["W"] = "West";
    printf("N is %s and W is %s\n", direction["N"], direction["W"]);

    mon[1] = "January"; mon[01] = "JAN"
    printf("mon[1] is %s\n", mon[1]);
    printf("mon[01] is also %s\n", mon["1"]);
    printf("mon[\001] is also %s\n", mon["01"])
}
```

N is North and W is West

mon[1] is January

mon[01] is also January

But mon[01] is JAN

从这个输出中可以学习到两个重要的点。首先，索引为 "1" 的设置覆盖了索引为 1 的设置。访问数组元素下标 1 和 01 实际上定位到为 "1" 的元素。另外注意 `mon["1"]` 不同于 `mon["01"]`。

### 12.9.2 ENVIRON[]：环境变量数组

你有时需要知道运行程序的用户名或主目录。`awk` 维护着关联数组 `ENVIRON[]` 来存储所有的环境变量。最近版本的 `awk`（包括 `awk` 和 `gawk`）满足了这一 POSIX 要求。我们就是这样从 `awk` 程序中访问 shell 变量 `HOME` 和 `PATH` 的：

```
$ awk BEGIN {
    print "HOME" "=" ENVIRON["HOME"]
    print "PATH" "=" ENVIRON["PATH"]
}
```

HOME=/users1/home/staff/sumit

PATH=/usr/bin::/usr/local/bin:/usr/ccs/bin

## 12.10 内置变量

`awk` 有几个内置变量（表 12）。
