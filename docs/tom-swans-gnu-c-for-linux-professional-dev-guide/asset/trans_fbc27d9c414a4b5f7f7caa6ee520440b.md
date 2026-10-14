

哎呀，这得到的是 24.167 度，而不是 23.8889。代码里还有另一个 bug，如果我们没有验证计算结果，很容易就会错过它。试试其他输入数据——比如 80 和 90.7。显然，只有小数值的输入才会让 bug 出现。程序能正确地将整数转换为摄氏度而不会出错。程序的浮点数据有问题。所以，重新编译用于调试并将程序载入 gdb：

```
$ g++ -g -o buggy buggy.cpp
$ gdb -silent buggy
```

在赋值给 fdegrees 的位置设置断点，fdegrees 是一个类型为 double 的浮点变量，然后运行代码直到该点：

```
(gdb) break 23
Breakpoint 1 at 0x80487cb: file buggy.cpp, line 23.
(gdb) run
Starting program: /src/c06/buggy
*** Warning: This program has intentional bugs
Fahrenheit to Celsius conversion
Degrees Fahrenheit? 75.5
```

Tip 你可以输入 b 23 代替 break 23，以及 r 代替 run。

在提示时输入 75.5 并按 Enter。调试器会在断点处暂停程序：

```
Breakpoint 1, main () at buggy.cpp:23
23      fdegrees = atol(input);
```

在执行该语句之前，确保 input 变量保存了输入的值。要检查字符串，输入 print input：

```
(gdb) print input
$1 = "75.5", '\000' <repeats 123 times>
```

调试器为表达式分配了一个伪名称 $1。从现在开始，你可以用 print $1 来重新检查这个值。或者，简单地输入 p $1 而不是完整命令。你也可以在其他表达式中使用 $1——例如，在 display 命令中（稍后会详细介绍）。在这种情况下，字符串 "75.5" 看起来没问题。它后面正确地跟着一个空字符（这里以八进制表示为 \000'）。调试器还告诉我们，这个空字符在字符串变量中重复了 123 次。这里没有 bug，所以让我们继续。

程序当前在为 fdegrees 赋值的语句处暂停。发出 next 命令来执行该语句。

```
23      fdegrees = atol(input);
(gdb) next
```

程序再次暂停后，打印 fdegrees 的值：

```
(gdb) print fdegrees
$2 = 75
```

同样，调试器分配了一个伪名称 ($2)，你可以用它在其他时间检查 fdegrees。变量的值是 75，但应该是 75.5。有什么东西截断了浮点值的分数部分。对有问题的行再看一眼就能发现问题：

```
23  fdegrees = atol(input);
```

程序调用了 atol()（ASCII 转 long），而它本应调用 atof()（ASCII 转 float）。由于 long int 值赋给 double 类型变量在语法上是允许的，编译器没有将其报告为错误。要修复这个问题，退出调试器并将 atol() 改为 atof()。现在程序能正确地将 75.5 华氏度转换为宜人的 24.1667 摄氏度。清单 6.16，celsius.cpp，展示了修复了故意 bug 后的完整程序。

## LISTING 6.16 CELSIUS.CPP

```
#include <iostream.h>
#include <stdlib.h>

double fdegrees, cdegrees;
char input[128];

int main()
{
    cout << "Fahrenheit to Celsius conversion" << endl;
    cout << "Degrees Fahrenheit? ";
    cin >> input;
    fdegrees = atof(input);
    cdegrees = ((fdegrees - 32.0) * 5.0) / 9.0;
    cout << "Degrees Celsius == " << cdegrees << endl;
    return 0;
}
```

Tip 要修复 bug，你首先必须找到它们。在这种情况下，只有浮点输入才会让 celsius.cpp 中的 bug 出现，而一次单一的测试运行可能会错过这个问题。需要吸取的教训是：始终使用多种输入数据来测试你的程序。

## OTHER DATA DEBUGGING COMMANDS

以下是一些用于检查程序变量的有用的 GNU 调试器命令。要跟上进度，使用 -g 选项编译本章中的 tax.cpp 程序并用以下命令将结果载入调试器

```
$ g++ -g -o tax tax.cpp
$ gdb -silent tax
```

设置断点并运行程序。提示时，输入此处显示的值：

```
(gdb) break 28
Breakpoint 1 at 0x8048737: file tax.cpp, line 28.
(gdb) run
Starting program: /src/c06/tax
```

