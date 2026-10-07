
存储到一个名为 1 的变量中，第二个参数存储到一个名为 2 的变量中，依此类推。这些变量名称被 shell 保留，因此你不能用它们作为你定义的变量名。要访问存储在这些变量中的值，你必须像处理你定义的变量一样，在变量名前加上美元符号 ($)。

下面的 shell 程序期望被调用时带有两个参数。该程序获取这两个参数，先打印在命令行上输入的第二个参数，再打印在命令行上输入的第一个参数。

```
#program reverse, prints the command line parameters out in reverse order
echo "$2" "$1"
```

如果你输入以下命令来调用此程序：

```
reverse hello there
```

程序将返回以下输出：

there hello

在进行大量 shell 编程时，了解其他几个内置的 shell 变量非常重要。表 14.1 列出了这些变量，并简要说明了每个变量的用途。

### 表 14.1. 内置 SHELL 变量

| 变量 | 用途 |
|---|---|
| $# | 存储传递给 shell 程序的命令行参数数量。 |
| $? | 存储最后执行的命令的退出值。 |
| $0 | 存储输入命令的第一个单词（shell 程序的名称）。 |
| $* | 存储命令行输入的所有参数 ($1 $2 ...)。 |
| "$@" | 存储命令行输入的所有参数，分别引用（'$1' '$2' ...）。 |

## 引号的重要性

在 shell 编程中，使用不同类型的引号非常重要。三种类型的引号和反斜杠字符都被 shell 用于执行不同的功能。双引号（`"`）、单引号（`'`）和反斜杠（`\`）都用于隐藏特殊字符，使其不被 shell 解析。这些方法以不同程度隐藏特殊字符。

双引号是这三种方法中功能最弱的。当你用双引号包围字符时，所有空白字符对 shell 隐藏，但所有其他特殊字符仍会被 shell 解释。这种类型的引用在你将包含多个单词的字符串赋值给变量时最有用。例如，如果你要将字符串 `hello there` 赋值给变量 `greeting`，请输入以下命令：

```
greeting="hello there" (for bash and pdksh)
set greeting = "hello there" (for tesh)
```

该命令将 `hello there` 字符串作为一个单词存储到 `greeting` 变量中。如果你在不使用引号的情况下输入此命令，你将无法获得想要的结果。bash 和 pdksh 将不会理解该命令并会返回错误消息。tesh 会将值 `hello` 赋值给 `greeting` 变量并忽略命令行其余部分。

单引号是最强大的引用形式。它们隐藏所有特殊字符，使其不被 shell 解析。如果你输入的命令是 intended 给 shell 以外的其他程序，这将非常有用。

由于单引号最强大，你可以使用单引号来编写 `hello there` 变量赋值。但你并不总是希望这样做。如果赋值给 `greeting` 变量的字符串包含另一个变量，你必须使用双引号。例如，如果你想在问候语中包含用户名，请输入以下命令：

```
greeting="hello there $LOGNAME" (for bash and pdksh)
set greeting="hello there $LOGNAME" (for tesh)
```

> **提示**  
> 请记住，`LOGNAME` 变量是一个 shell 变量，它包含登录到系统的用户的 Linux 用户名。

如果你以 root 身份登录到 Linux，这会将值 `hello there root` 存储到 `greeting` 变量中。如果你尝试使用单引号编写此命令，它将不起作用，因为单引号会将美元符号从 shell 中隐藏，shell 不知道它应该执行变量替换。如果你使用单引号编写命令，`greeting` 变量将被赋值 `hello there $LOGNAME`。

使用反斜杠是隐藏特殊字符的第三种方法。与单引号方法一样，反斜杠隐藏所有特殊字符，但每次只能隐藏一个字符，而不是字符组。你可以使用以下命令，用反斜杠代替双引号重写问候示例：

```
greeting=hello\ there (for bash and pdksh)
set greeting=hello\ there (for tcshe)
```

在此命令中，反斜杠将空格字符从 shell 中隐藏，字符串 `hello there` 被赋值给 `greeting` 变量。

反斜杠引用最常在你只想隐藏单个字符时使用。这通常是在你想在字符串中包含特殊字符时进行的。例如，如果你要将一盒计算机磁盘的价格存储到名为 `disk_price` 的变量中，请使用以下命令：

```
disk_price=$5.00 (for bash and pdksh)
set disk_price = \$5.00 (for tcsh)
```

在此示例中，反斜杠将美元符号从 shell 中隐藏。如果没有反斜杠，shell 将尝试查找名为 5 的变量并执行变量替换。假设没有定义名为 5 的变量，shell 将为 `disk_price` 变量赋值 `.00`。这是因为 shell 将 `$5` 变量替换为 null 值。

> **注意**  
> `disk_price` 示例也可以使用单引号来将美元符号从 shell 中隐藏。

反引号（`` ` ``）执行不同的功能。当你想在另一个命令中使用命令的结果时使用它们。例如，如果你要将变量 `contents` 的值设置为当前目录中的文件列表，请输入以下命令：

```
contents='ls' (for bash and pdksh)
set contents = 'ls' (for tcshe)
```

此命令执行 `ls` 命令并将命令结果存储到 `contents` 变量中。正如你将在接下来的“迭代语句”部分中看到的那样，当你想编写一个 shell 程序，针对另一个命令的结果执行某些操作时，此功能会非常有用。

## test 命令

在 bash 和 pdksh 中，有一个名为 `test` 的命令用于评估条件表达式。通常，你使用 `test` 命令来评估用于条件语句的条件，或评估迭代语句的进入或退出标准。`test` 命令的语法如下：

```
test expression
or
[ expression ]
```

有几种内置运算符可以与 `test` 命令一起使用。这些运算符可分为四类：整数运算符、字符串运算符、文件运算符和逻辑运算符。

shell 整数运算符执行与字符串运算符类似的功能，但作用于整数参数。表 14.2 列出了 `test` 命令的整数运算符。

### 表 14.2. test 命令的整数运算符

| 运算符 | 含义 |
| :--- | :--- |
| int1 -eq int2 | 如果 int1 等于 int2，则返回 True。 |
| int1 -ge int2 | 如果 int1 大于或等于 int2，则返回 True。 |
| int1 -gt int2 | 如果 int1 大于 int2，则返回 True。 |
| int1 -le int2 | 如果 int1 小于或等于 int2，则返回 True。 |
| int1 -lt int2 | 如果 int1 小于 int2，则返回 True。 |
| int1 -ne int2 | 如果 int1 不等于 int2，则返回 True。 |

字符串运算符用于评估字符串表达式。表 14.3 列出了三种 shell 编程语言支持的字符串运算符。

![Image](img/e8e6b47ac20475e23d48b4c476f5d891_306_0.png)

### 表 14.3. test 命令的字符串运算符

| 运算符 | 含义 |
|---|---|
| str1 = str2 | 如果 str1 与 str2 相同，则返回 True。 |
| str1 != str2 | 如果 str1 与 str2 不相同，则返回 True。 |
| str | 如果 str 不为空，则返回 True。 |
| -n str | 如果 str 的长度大于零，则返回 True。 |
| -z str | 如果 str 的长度等于零，则返回 True。 |

`test` 命令的文件运算符用于执行诸如检查文件是否存在以及检查作为参数传递给 `test` 命令的文件类型等功能。表 14.4 列出了 `test` 命令的文件运算符。

### 表 14.4. test 命令的文件运算符

| 运算符 | 含义 |
|---|---|
| -d filename | 如果文件 filename 是目录，则返回 True。 |
| -f filename | 如果文件 filename 是普通文件，则返回 True。 |
| -r filename | 如果进程可以读取文件 filename，则返回 True。 |
| -s filename | 如果文件 filename 的长度不为零，则返回 True。 |
| -w filename | 如果进程可以写入文件 filename，则返回 True。 |
| -x filename | 如果文件 filename 可执行，则返回 True。 |

`test` 命令的逻辑运算符用于组合两个或更多整数、字符串或文件运算符，或否定单个整数、字符串或文件运算符。表 14.5 列出了 `test` 命令的逻辑运算符。

### 表 14.5. test 命令的逻辑运算符

| 命令 | 含义 |
|---|---|
| ! expr | 如果 expr 不为真，则返回 True。 |
| expr1 -a expr2 | 如果 expr1 和 expr2 均为真，则返回 True。 |
| expr1 -o expr2 | 如果 expr1 或 expr2 为真，则返回 True。 |

## tcsh 中 test 命令的等价物

tcsh 没有 `test` 命令，但它使用表达式支持相同的功能。tcsh 支持的表达式运算符与支持的运算符几乎相同
