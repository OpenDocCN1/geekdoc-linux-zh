
```bash
$ file=exec.o
$ lastchar=$(echo $file | sed 's/.*\(..)$$/1/')
$ echo $lastchar $
```

`sed` 命令将行中括号中的所有字符替换为最后一个（记住在这种情况下，周围的模式可以保存到寄存器中，此处为寄存器 1，然后通过 `\1` ）。`sed` 命令的结果存储在变量 `lastchar` 中。`sed` 命令周围的引号很重要，因为它们防止 shell 尝试解释反斜杠。（问题：使用双引号也可以吗？）

最后，命令替换是可以嵌套的。假设你想将变量中第一个字符的所有出现处更改为其他内容。在之前的示例中，`firstchar=$(echo $filename | cut -c1)` 获取了 `filename` 的第一个字符，但我们如何利用这个更改来改变 `filename` 中该字符的所有出现处呢？

两步法是一种方法：

```bash
$ filename=/users/steve/memos
$ firstchar=$(echo $filename | cut -c1)
$ filename=$(echo $filename | tr "$firstchar" "*") translate / to^
$ echo $filename
users/steve/memos $
```

但单个嵌套的命令替换可以执行相同的操作：

```bash
$ filename=/users/steve/memos
$ filename=$(echo $filename | tr "$(echo $filename | cut -c1)" "*")
$ echo $filename
users/steve/memos $
```

如果你很难理解这个示例，请将其与上一个进行比较：注意在前一个示例中 `firstchar` 变量是如何被嵌套命令替换替换的；否则，这两个示例是相同的。

## expr 命令

虽然通常 shell 支持内置整数算术，但旧版本的 shell 并不具备这种功能。在这种情况下，可以使用数学方程求解器 `expr`：

```bash
$ expr 1 + 2
3
$
```

它很容易使用，但 `expr` 不太擅长解析方程，因此给出的每个运算符和操作数之间必须用空格隔开才能被正确理解。这解释了以下内容：

```bash
$ expr 1+2
1+2
$
```

常用的算术运算符被 `expr` 识别：`+` 用于加法，`-` 用于减法，`/` 用于除法，`*` 用于乘法，`%` 用于取模（余数）。

```bash
$ expr 10 + 20 / 2
20
$
```

乘法、除法和取模的优先级高于加法和减法，标准数学也是如此。因此，在之前的示例中，先执行了除法。

但这个示例呢？

```bash
$ expr 17 * 6
expr: syntax error
$
```

shell 并替换了你目录中所有文件的名称，而 `expr` 完全不知道如何解释它们！特别是在乘法的情况下，传递给 `expr` 的表达式必须加引号以防止受到 shell 的干扰——但在这个示例中，不是作为一个单一参数：

```bash
$ expr "17 * 6"
17 * 6
$
```

记住 `expr` 必须将每个运算符和操作数视为独立的参数 [等待，这里的 OCR 文本似乎乱码了。提供的 138-140 页 OCR 文本存在严重的混乱和重复短语。我将处理可见的部分并保持逻辑连贯。*注：提供的 138-140 页 OCR 文本存在严重的损坏和重复。我清理了可见文本并尽可能修复了逻辑。]

## 传递参数

在学习如何处理传递给它们的参数后，shell 程序将变得有用得多。在本章中，你将学习如何编写接收参数的 shell 程序。回顾你在第 4 章编写的单行程序 `run`，它将 `sys.caps` 通过 `tbl`、`nroff` 和 `lp`：

```bash
$ cat run
tbl sys.caps | nroff -mm -Tlp | lp
$
```

假设你需要通过相同的命令序列运行 `sys.caps` 以外的文件。你可以为每个文件创建一个特殊的 `run` 版本；或者，你可以修改 `run` 程序，以便在命令行上指定文件名。也就是说，你可以修改 `run` 使得输入：

```bash
run new.hire
```

例如，指定通过此命令序列打印 `new.hire`，或者

run sys.caps

来指定 `sys.caps`。

每当你执行一个 shell 程序时，shell 会自动将第一个参数存储在特殊变量 1 中，将第二个参数存储在变量 2 中（为了方便起见，从现在起我们将这些引用为 `$1`、`$2` 等，尽管 `$` 实际上是变量引用的一部分，而不是变量名）。这些特殊变量——更正式地被称为位置参数，因为它们基于值在命令行中的位置——是在 shell 完成其常规的命令行处理（即 I/O 重定向、变量替换、文件名替换等）之后赋值的。

要修改 `run` 程序以接受参数作为文件名，你对程序做的只需更改对 `sys.caps` 文件的引用，使其改为引用命令行上输入的第一个参数：

```bash
$ cat run
tbl $1 | nroff -mm -Tlp | lp
$
```

$ 执行 new.hire，并将 new.hire 作为参数

请求 ID 为 laserl24 (标准输入)

$

每当你执行该程序时，无论命令行后面跟着什么单词，它都会被 shell 存储在第一个位置参数中，并传递给程序。在第一个示例中，new.hire 将存储在此参数中。

位置参数的替换与其他类型的变量替换完全相同，因此当 shell 看到 `$1` 时会将 `$1` 替换为提供给程序的第一个参数：new.hire。

再举一个例子，以下名为 `ison` 的程序可以让你知道指定的用户是否已登录：

```
$ ison
who | grep $1
$ who
root console t 7 Jul 8 12:37
barney tty03 Jul 8 12:28
fred tty04 Jul 8 13:24
joanne tty07 Jul 8 09:35
tony tty19 Jul 8 08:30
lulu tty23 Jul 8 09:55
$ ison
tony tty19 Jul 8 08:30
$ ison pat
```

> 查看谁在在线

> 未登录

## $ 变量

除了位置变量外，特殊 shell 变量 `$$` 会被设置为在命令行上输入的参数数量。正如你将在本章中看到的，变量经常被程序用于测试，以确定用户是否指定了正确数量的参数。

下一个名为 `args` 的程序是为了让你更熟悉参数传递给 shell 程序的方式。学习每个示例的输出，并确保你理解了它：

```
$ args
echo $$ arguments passed
echo arg 1 = $1; arg 2 = $2; arg 3 = $3;
$ args a b c
3 arguments passed
arg 1 = :a; arg 2 = :b; arg 3 = :c;
$ args a b
```

> 查看该程序

> 执行

> 尝试使用两个参数

## $ 变量

2 个参数传递

arg 1 = :a arg 2 = :b arg 3 = 

未分配的参数为空

如你所见，shell 在执行你的 shell 程序时会进行正常的命令行处理。这意味着在为你的程序指定参数时，你可以利用正常的便利特性，例如文件名替换和变量替换。

## $ 变量

该特殊变量引用所有传递给程序的参数。这在接收不确定或可变数量参数的程序通常有用。你稍后会看到更多示例。这是一个说明其用法的程序：

```
$ cat args2
echo $* arguments passed
echo they are $*
$ args2 a b c
3 arguments passed
they are :a b c:
$ args2 one two
2 arguments passed
they are :one two:
$ args2
0 arguments passed
they are ::
$ args2 * arguments passed
they are :args args2 names nu phonebook stat xact xtra
$
```

## 一个在电话录中查找某人的程序

这里是之前示例中的电话录文件：

```
$ cat phonebook
Alice Chebbe 973-555-2015
Barbara Swizzle 201-555-9257
Liz Stachiw 212-555-2298
Susan Goldberg 201-555-7776
Susan Topple 212-555-4932
Tony Iannino 973-555-1295
$
```

你已经如何使用 `grep` 在文件中查找某人：

```
$ grep Cheb phonebook
Alice Chebbe 973-555-2015
$
```

你也知道，如果你想按全名查找某人，需要在单词周围加上引号以保持参数的整体：
