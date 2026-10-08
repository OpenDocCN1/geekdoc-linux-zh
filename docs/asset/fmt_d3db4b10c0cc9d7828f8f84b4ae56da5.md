
运行 `tcl` 需要一个 `tcl` shell (`tsh`) 或窗口 shell (`wish`)。`tsh` 和 `wish` 都与标准的 UNIX shell（如 `sh` 或 `c`）类似，它们允许交互式地执行命令或从文件中读取。在实践中，这些 shell 通常用于交互式操作，因为它们的交互能力非常有限。

` tcl ` 和 `wish` 之间的主要区别是 `tsh` 只理解 `tcl` 命令，而 `wish` 则同时理解 `tcl` 和 `tk` 命令。

# tcl 的交互式使用

本节简要介绍 `tcl` shell 的交互式使用，以说明其风险之一。

要开始交互式地使用 `tcl`，只需在 UNIX shell 提示符处输入 `tclsh`（或 `wish`）。应该出现以下提示符：

`%`

在本章中，交互式命令以百分号（`%`）开头。在提示符处，输入

`% echo "hello world"`

应该出现 `hello world` 单词，随后是一个新提示符。现在尝试

`% echo "hello world"`

应该出现相同的输出，但这两个者之间存在巨大差异。第一个命令是交互式运行的，这是使用 `tcl` shell 的风险之一。例如，如果你将命令

`% echo "hello world"`

放入文件并在从 `tclsh` 中 `source` 该文件，你将得到以下错误：

`invalid command name "echo"`

要正确使用 `tcl` 命令，请使用 `tcl` 命令：

`% echo "hello world"`

这在交互模式下执行了命令及其参数。这仅仅是一个例子

# 非交互式使用 tcl

通常，`tclsh` 和 `wish` 是非交互式使用的，这意味着它们从 UNIX 提示符调用，例如：

`$ tclsh myprog.cl`

`$ wish myprog.cl`

或者在脚本内部调用，其第一行类似于：

`#!/usr/bin/wish`

通常必须为每次安装更改第一行，因为 `wish` 或 `tcl` 位于不同的位置。为了避免每次安装都要编辑脚本，`tcl` 主页建议使用以下三行作为 `tcl/tk` 脚本的开头：

```tcl
#!/bin/sh
# 下一行使用 wish 重启
exec wish "$0"
```

这意味着用户只需要在路径中使用 `wish` 即可运行脚本。这种方法的取决于取决于 `sh` 版本。

`tcl` 非交互式使用的真正优势与 UNIX shell 的相同交互式式允许许多命令组合在一起，只需输入脚本名称即可执行，并加快大型程序的开发和调试。

# tcl 语言

本节介绍了 `tcl` 语言语法及其在脚本中的用法。下节的代码可以交互式地运行，也可以从脚本运行。输出的间距在交互模式下会有所不同。

# 命令结构

`tcl` 命令的基本结构是

`commandname arguments`

其中 `commandname` 是 `tcl` 要执行的命令，而 `arguments` 是给该命令的可选参数。整行（命令name 和参数）被称为命令。命令之间通过换行符或分号（`;`）隔开。如果一行中只有一个命令，则不需要分号。作为说明，两个命令可以每行写一个：

```tcl
set foo 0
set bar 1
```

或者在同一行上：

```tcl
set foo 0; set bar 1;
```

# tcl 和 tk 编程

第 33 章

## 注释

除了命令外，`tcl` 脚本中的其他行都是注释。与 UNIX shell 和 Perl 一样，注释行是以井号（`#`）开头的行：

```tcl
# this is a comment
```

但与 shell 不同，以下内容并不是注释：

```tcl
set foo @
```

这将导致一个错误，因为 `tcl` 解析器认为命令是以换行符或分号（`;`）结束的。要在与命令同一行内包含注释，需要用分号结束命令，如下所示：

```tcl
set foo @# initialize foo
```

将所有命令都以分号结尾可能是一个好主意，尽管这不是强制要求的。

## 数据类型

`tcl` 不支持如 `int`、`float`、`double` 或 `char` 等变量类型。这意味着一个变量在同一个程序中，可以在不同的时间被设置为数字、字符或字符串。

然而在内部，`tcl` 将所有变量都视为字符串。当需要操作变量时，`tcl` 允许以 ANSI C 能够理解的所有形式给出数字（实数和整数）。以下示例是变量的有效数值值：

| 值 | 类型 | 描述 |
| :--- | :--- | :--- |
| 74 | 整数 | |
| 0112 | 进制 | 以 0 开头 |
| 0x4a | 十进制 | 以 0x 开头 |
| 74. | 实数 | |
| 74.0 | 实数 | |
| 7.4e1 | 实数 | |
| 7.4e+1 | 实数 | |

其他值被视为字符串，如果在数学表达式中使用将产生错误。

## 变量

`tcl` 定义了两种类型的变量：标量和数组。要创建一个标量变量并为其赋值，请使用 `set` 命令。例如：

```tcl
set banana 1;
```

这会创建变量 `banana` 并赋予其数值为 1。若要将 `banana` 的值设置为其他内容，只需再次使用 `set`：

```tcl
set banana "Fresh from Brazil";
```

现在变量 `banana` 的值为 `"Fresh from Brazil"`。双引号告诉 `tcl` 包括空格在内的所有字符共同构成了该变量。（引用和替换将在本章稍后的“引用和替换”部分中介绍。）

要打印 `banana` 的值，使用 `puts` 命令：

```tcl
puts $banana;
```

这会将变量 `banana` 的值打印到标准输出（有时称为 STDOUT）。在变量名之前加上 `$` 告诉 `tcl` 访问分配给变量的值。这种约定被称为变量替换，类似于 UNIX shell 中使用的约定。

要创建一个一维数组，输入以下内容：

```tcl
set fruit(0) banana;
set fruit(1) orange;
```

这创建了数组 `fruit`，并将 `banana` 和 `orange` 分别赋予第一个和第二个元素（0 和 1）。

> 注意
> 记住，计算机从数字零 (0) 开始计数，而不是一 (1)。

对数组索引的赋值不需要顺序。以下命令：

```tcl
set fruit(100) peach;
set fruit(2) kiwi;
set fruit(87) pear;
```

在 `fruit` 数组中仅创建了三项。`tcl` 中的数组类似于关联数组，它将“键”与“值”关联。`tcl` 中的数组将给定的字符串与另一个字符串关联。这使得使用非数字作为数组索引成为可能。以下命令：

```tcl
set fruit(banana) 100
```

将数组 `fruit` 中项目 `banana` 的值设置为 100。分配的值不需要是数字的：

```tcl
set food(koala) eucalyptus;
set food(chipmunk) acorn;
```

要访问存储在一维数组变量中的值，请使用 `$` 约定：

```tcl
puts $food(koala);
```

这会打印出存储在 `food` 数组索引 `koala` 处的值。数组索引也可以是一个变量：

```tcl
set animal chipmunk;
puts $food(animal);
```

给定之前的赋值，这些命令将输出 `acorn`。

多维数组是一维数组的简单扩展，其设置方式如下：

```tcl
set array(1,1) 0;
```

这将 `myArray` 数组中 1,1 处的值的值设置为 0。通过逗号分隔索引，你可以创建三、四或更多维的数组：

```tcl
set array(1,1,1,1,1,1) "foo";
```

除了设置数组值外，`tcl` 还提供了 `array` 命令来获取有关数组的信息，以及 `parray` 命令来打印有关数组的信息。首先，来看 `parray` 命令。给定声明：

```tcl
set food(koala) eucalyptus;
set food(chipmunk) acorn;
set food(panda) bamboo;
```

命令：

```tcl
parray food
```

产生以下输出：

```
food(chipmunk) = acorn
food(koala) = eucalyptus
food(panda) = bamboo
```

现在看 `parray` 命令及其参数，它们被用于获取有关数组及其元素的信息。`array` 命令的基本语法如下：

```tcl
array option arrayname
```

支持的选项将在本节稍后部分讨论。

关于数组最频繁使用的信息之一是它的大小。给定声明：

```tcl
set fruit(0) banana;
set fruit(1) peach;
set fruit(2) pear;
set fruit(3) apple;
```

命令：

```tcl
array size fruit
```

返回 4。这个数字在循环中通常有用。

由于数组可以具有非数字索引，`array` 命令提供了一种查找元素的方法。例如：

```tcl
array search food string
```

返回 `string` 在 `food` 中首次出现的索引，或者如果 `string` 不在 `food` 中出现则返回 -1。要获取数组的后续元素，使用 `next` 选项：

```tcl
array next food index
```

`array` 命令的另一个在遍历数组时经常使用的选项是 `exists`。例如：

```tcl
array exists food
```

如果数组中有任何项目，则返回真（值为 1）。

要释放一个变量（标量或数组），请使用 `unset` 命令：

```tcl
unset banana;
```

这会销毁该变量。如果你使用 `unset $banana`（假设 `banana` 被设置为之前显示的值）而不是直接用 `banana`，你会得到如下错误：

`can't unset "0": no such variable`

这是因为 `$` 位于变量之前，变量的值在执行执行之前被替换。

## 字符串值的操作

字符串操作简单的形式是 `append` 命令，它可以连接多个字符串和变量。作为说明，以下命令：

```tcl
set str1 "Begin"
append str1 "a String"
set str2 "even more text"
append str1 "with some text and add $str2 to it;
puts $str1;
```

给出输出：

`Begin a String with some text and add more text to it.`

你可以通过以下命令获得相同的结果：

```tcl
set str1 "Begin"
set str1 "str1 a String"
set str2 "even more text"
set str1 "str1 with some text and add$str2 to it;
```

这将比使用 `append` 慢，因为 `append` 不像 `set` 那样进行字符拷贝。

对于更高级的字符串操作，`tel`提供了 `string` 命令，它包含了大量的选项。该命令的基本语法为：

```tcl
string option string2
```

其中 `string1` 和 `string2` 可以是字面量（`"this is a string"`）或变量，而 `option` 是以下之一：

| 选项 | 描述 |
| :--- | :--- |
| compare | 返回 -1、0 或 1，取决于 `string1` 在字典上小于、等于还是大于 `string2`（类似于 C 库函数 `strcmp`）。 |
| first | 返回 `string1` 在 `string2` 中首次出现的索引，或者如果 `string1` 不在 `string2` 中出现则返回 -1。 |
| last | 返回 `string1` 在 `string2` 中最后一次索引，或者如果 `string1` 不在 `string2` 中出现则返回 -1。 |

`string` 命令的以下选项将 `string2` 视为字符列表，用于从 `string1` 中修剪：

- `trim` 从 `string1` 中移除 `string2` 中存在的任何开头和结尾字符。
- `trimleft` 从 `string1` 中移除 `string2` 中存在的任何开头字符。
- `trimright` 从 `string1` 中移除 `string2` 中存在的任何结尾字符。

`string` 命令的以下选项仅接受 `string1` 作为参数：

- `length` 返回 `string1` 中的字符数量。
- `toulower` 返回一个新的字符串，将 `string1` 中的所有字符转换为小写。
- `toupper` 返回一个新的新字符串，将 `string1` 中的所有字符转换为大写。

现在我们来看几个例子。首先，创建一个字符串并获取它的长度：

```
set str "Here Is A Test string";
string length $str
```

这得到的长度是 23（`length` 选项会计算空格字符）。现在获取字符串 'st' 在 `$str` 中第一次和最后一次出现的位置：

```
string first "st" $str;
string last "st" $str
```

这得到的 'st' 第一次出现的值为 13（对应 Test 中的出现），以及 'st' 最后一次出现的值也为 13（Test again）。那么 String 中的 'st' 呢？大多数字符串比较函数是对大小写和空格是敏感，因此我们临时将 `$str` 转换为小写并重试一次：

```
string last "st" [string toulower $str];
```

这得到的值为16，对应于 String 中的 'st'。最后，去掉开头和结尾的空格并获取字符串的长度：

```
string length [string trim $str " "];
```

返回值为 21，这意味着开头和结尾的空格被删除了。

# 操作数值值

`tcl` 提供了两个用于操作数值变量和常量的命令：`incr` 和 `expr`。

`incr` 命令为 `tcl` 提供了等于 C 语言中运算符 `+=`、`-=`、`*=` 的功能。其基本语法为

```
incr variable integer
```

其中 `variable` 必须是一个整数。`incr` 命令将指定的整数加到变量上；因此，减法通过提供负整数来处理。我们可以演示一下它的用法。首先，创建一个变量并对它执行 `incr`：

```
set a 81;
incr a;
puts $a
```

`$a` 的值为 82。默认情况下，`incr` 等同于 `++`；如果没有提供整数参数，它会在指定的变量上加 1。现在将 `$a` 减 3：

```
incr a -3
puts $a
```

`$a` 的值为 79。最后一点是，该整数可以是一个变量的值：

```
set a 6;
set b 9;
incr a $b;
puts $a
```

`$a` 的值为 15。

对于更复杂的数学运算，`tcl` 提供了 `expr` 命令，它可以处理所有标准的 ANSI C 运算符。运算符优先级大部分与 ANSI C 相同。

当需要任何数学运算时，必须在前面加上 `expr` 命令。例如，以下命令

```
set a 20;
set b 4;
set c $a/$b;
puts $c
```

结果输出为

`20/4`

而不是预期的结果 5。要得到正确答案，请使用 `expr` 命令：

```
set c [expr $a / $b];
```

除了标准运算符 `+`、`*` 和 `/` 之外，`expr` 命令还可以给定几个选项，使其能够执行数学运算。其基本语法为

# 有用的编程语言概述

`expr function number`

`expr` 可理解的一些函数及其返回值如下：

| 函数 | 描述 |
| :--- | :--- |
| `abs(x)` | `x` 的绝对值 |
| `round(x)` | `x` 舍入后得到的整数值 |
| `cos(x)` | `x` 的余弦（弧度） |
| `cos(x)` | `x` 的双曲余弦 |
| `acos(x)` | `x` 的反余弦（0 到 pi） |
| `sin(x)` | `x` 的正弦（弧度） |
| `sinh(x)` | `x` 的双曲正弦 |
| `asin(x)` | `x` 的反正正弦（pi/2 到 pi/2） |
| `tan(x)` | `x` 的正切（弧度） |
| `tanh(x)` | `x` 的双曲正切 |
| `atan(x)` | `x` 的反正正切（pi/2 到 pi/2） |
| `exp(x)` | `e` 的 `x` 次方 |
| `log(x)` | `x` 的自然对数 |
| `log10(x)` | `x` 的以10为底的数 |
| `sqrt(x)` | `x` 的平方根 |

以下数学函数接受两个数字参数：

`pow(x,y)` `x` 的 `y` 次方

```
其用法如下：
set a 2;
set b [expr pow(a,3)];
puts $b;
```

输出将是 8.0，即 2 的三次。

# 引用与替换

引用和替换在与变量方面都被频繁使用。你在本章开头已经看过了最基础的引用（使用双引号创建字符串）和替换。`tcl` 支持另一种类型的引用，即大括号引用（brace quoting），以及另一种类型的替换。

引用和替换在与变量方面都被频繁使用。你在本章开头已经看过了最基础的引用（使用双引号创建字符串）和替换。`tcl` 支持另一种类型的引用，即大括号引用（brace quoting），以及另一种类型的替换。

# 流程控制—if 和 switch

`tcl` 提供了几个用于流程控制的命令，并对字符串和数值数据支持所有标准的 ANSI C 比较运算符。

本节从 `if/elseif/else` 命令开始。最简单的语句如下所示：

```
if {$x < 0} {
    set x 10;
}
```

此示例在 `if` 子句的主体中只有一行，但可以添加任意数量的行和子块。如果需要执行额外的测试，每个测试都将以括号的形式的形式给出：
