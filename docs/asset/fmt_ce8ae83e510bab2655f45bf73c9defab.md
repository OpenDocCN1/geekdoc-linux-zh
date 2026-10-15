
```struct complexStruct {
    double aFloat;
    int anInt;
    char aString[8];
    char aChar;
    long aLong;
};
```

按照这里的声明，`complexStruct` 有五个成员：一个浮点值、一个整数、一个包含 8 个元素的 `char` 数组、一个字符和一个长整数。一个名为 `data` 的变量声明如下：

```complexStruct data;
```

该变量可以将这五种类型的成员值存储在一个方便的封装中。与所有结构体一样，你可以使用点号表示法在 `data` 的成员中存储值：

```data.aFloat = 3.14159;
data.aChar = 'X';
```

## 调试数据对象

当程序未能产生预期输出时，首先要检查的地方是任何对变量的赋值。在本节中，你将检查一个程序中一些故意植入错误的代码，该程序本应将华氏温度转换为摄氏温度。遗憾的是，该程序似乎无法正确工作。借助 GNU 调试器的数据检查命令，你可以快速定位并修复问题。

> 以下各节使用控制台调试器 `gdb`。如果你愿意，也可以使用其他界面，例如 X 下的 `xgdb`，或 Emacs 编辑器的调试命令。有关使用这些界面运行 GNU 调试器的基础知识，请参阅第 5 章“编译和调试 C++ 程序”。

## 找出错误

随书 CD-ROM 的 `src/c06` 子目录中有一个文件 `buggy.cpp`。它是同一目录下的 `celsius.cpp` 程序的副本，但包含两个故意植入的 bug。要查看问题，请使用常用命令编译并运行这个有 bug 的程序：

```$ g++ buggy.cpp
$ ./a.out
```

输入一个华氏温度，例如 `75.5`。程序本应将该温度转换为摄氏温度，但如下输出所示，它明显显示了错误的结果：

```
** Warning: This program has intentional bugs
Fahrenheit to Celsius conversion
Degrees Fahrenheit? 75.5
Degrees Celsius == -9.44444
```

显然，程序的公式有问题。让我们用调试器来定位问题所在。

## 加载代码

找到 bug 的第一步是使用调试信息编译程序。之后，将其加载到 `gdb` 中。要跟随操作，请输入以下两条命令：

```$ g++ -g -o buggy buggy.cpp
$ gdb -silent buggy
(gdb)
```

第一行选择默认级别的调试信息（`-g`）并指定输出文件名 `buggy`。第二行将编译后的代码加载到调试器中。`-silent` 选项会跳过调试器冗长的欢迎信息。最后一行是 `gdb` 的命令提示符。我们希望在程序暂停在合适位置时检查数据值，因此先输入 `L` 几次，列出程序的源代码（为了节省篇幅，这里只列出相关行）：

```
(gdb) l
...
22 cin >> input;
23 fdegrees = atol(input);
24 cdegrees = (fdegrees - 32.0 * 5.0) / 9.0;
```

由于程序报告了错误结果，最明显的检查位置是第 24 行的计算。因此，在那里设置断点，然后运行程序，使其在执行该语句之前暂停：

```
(gdb) break 24
Breakpoint 1 at 0x80487e7: file buggy.cpp, line 24.
(gdb) run
Starting program: /src/c06/buggy
*** Warning: This program has intentional bugs
Fahrenheit to Celsius conversion
Degrees Fahrenheit? 75.5
```

在你输入 `75.5` 并按回车后，调试器会在断点处暂停程序，并显示接下来要执行的语句：

`Breakpoint 1, main () at buggy.cpp:24`

`24 cdegrees = (fdegrees - 32.0 * 5.0) / 9.0;`

输入 `next` 并按回车，以执行这条可疑的语句，然后发出 `print` 命令检查 `cdegrees`：

```
(gdb) next
25     cout << "Degrees Celsius == " << cdegrees << endl;
(gdb) print cdegrees
$1 = -9.444444444444446
```

提示：除了输入 `next`，你还可以直接输入 `n` 并按回车。

`cdegrees` 的值显然表明程序没有计算出正确结果，但它并没有告诉我们原因。在这种情况下，查看表达式即可发现问题出在缺少一对括号：

```
(fdegrees - 32.0 * 5.0) / 9.0 //???
```

因为乘法的优先级高于减法，所以该表达式的第一部分会先计算 `32.0` 乘以 `5.0`，再从 `fdegrees` 中减去结果；但公式要求先将 `fdegrees` 减去 `32.0`，再相乘。不过，有时表达式中的问题并不那么明显。在这种情况下，将表达式拆分成几部分，并使用 `gdb` 的 `print` 命令检查中间结果，通常会很有帮助。例如，你可以注释掉 `cdegrees` 的计算，并用如下临时代码替换：

```
double t1 = fdegrees - 32.0;
double t2 = t1 * 5.0;
double t3 = t2 / 9.0;
```

然后你可以单步执行这些语句，并检查 `t1`、`t2` 和 `t3` 临时变量，从而进一步调查错误表达式的原因。现在你不必实际执行这些步骤，但请记住它们，以备将来排查问题。

如果你在跟随操作，请退出调试器（输入 `q`，并在提示是否要退出正在运行的程序时回答 `yes`）。通过添加括号来修复错误表达式，将其改为以下形式：

```
((fdegrees - 32.0) * 5.0) / 9.0
```

编译修改后的 `buggy.cpp` 并运行。你不必再将它加载到调试器中。在提示时再次输入 `75.5`：

```
$ g++ buggy.cpp
$ ./a.out
*** Warning: This program has intentional bugs
Fahrenheit to Celsius conversion
Degrees Fahrenheit? 75.5
Degrees Celsius == 23.8889
```

看起来好多了。但为了确保无误，请用普通计算器算一下，验证程序的结果。请在计算器中输入以下表达式：

```
((75.5 - 32.0) * 5.0) / 9.0
```

哎呀，这得到的是 `24.167` 度，而不是 `23.8889`。代码里还有另一个 bug，如果我们没有验证计算结果，很容易就会错过它。试试其他输入数据——比如 `80` 和 `90.7`。显然，只有小数值的输入才会让 bug 出现。程序能正确地将整数转换为摄氏度而不会出错。程序的浮点数据有问题。所以，重新编译用于调试并将程序载入 `gdb`：

```
$ g++ -g -o buggy buggy.cpp
$ gdb -silent buggy
```

在赋值给 `fdegrees` 的位置设置断点，`fdegrees` 是一个类型为 `double` 的浮点变量，然后运行代码直到该点：

```
(gdb) break 23
Breakpoint 1 at 0x80487cb: file buggy.cpp, line 23.
(gdb) run
Starting program: /src/c06/buggy
*** Warning: This program has intentional bugs
Fahrenheit to Celsius conversion
Degrees Fahrenheit? 75.5
```

Tip 你可以输入 `b 23` 代替 `break 23`，以及 `r` 代替 `run`。

在提示时输入 `75.5` 并按 Enter。调试器会在断点处暂停程序：

```
Breakpoint 1, main () at buggy.cpp:23
23      fdegrees = atol(input);
```

在执行该语句之前，确保 `input` 变量保存了输入的值。要检查字符串，输入 `print input`：

```
(gdb) print input
$1 = "75.5", '\000' <repeats 123 times>
```

调试器为表达式分配了一个伪名称 `$1`。从现在开始，你可以用 `print $1` 来重新检查这个值。或者，简单地输入 `p $1` 而不是完整命令。你也可以在其他表达式中使用 `$1`——例如，在 `display` 命令中（稍后会详细介绍）。在这种情况下，字符串 `"75.5"` 看起来没问题。它后面正确地跟着一个空字符（这里以八进制表示为 `\000'`）。调试器还告诉我们，这个空字符在字符串变量中重复了 `123` 次。这里没有 bug，所以让我们继续。

程序当前在为 `fdegrees` 赋值的语句处暂停。发出 `next` 命令来执行该语句。

```
23      fdegrees = atol(input);
(gdb) next
```
