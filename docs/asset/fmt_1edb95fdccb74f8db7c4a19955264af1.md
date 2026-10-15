
Again, the confirmation is odd, but ignore it—the command seems to work fine. Use the command `set input-radix` to alter debugger input values to accept a different radix. Use `set radix` to alter both the input and output radix.

> Note

> Changing the radix does not affect the input or output of floating point values, only integers.

## FINDING A VARIABLE'S TYPE

To verify the type of an object, use the `ptype` command. For example, to find the type of the `tax` variable, enter the command:

```
(gdb) ptype tax
type = double
```

This is useful for verifying that an object is of an expected type—an array element, for example—and avoids having to hunt for a declaration in a lengthy source code file.

## DEBUGGING WITH THE `assert()` MACRO

Another great way to catch bugs that doesn't require using the GNU debugger is a macro defined in the `assert.h` standard header file. The macro performs a simple task—halting a program with an error message upon the failed assertion of any expression. To use `assert()`, add this directive to your program's source file:

```
#include <assert.h>
```

Use `assert()` to test any true or false condition. For example, suppose that you suspect an `int` variable named `waterLevel` is falling below a defined high value. To test for that condition, insert a statement such as

```
assert(waterLevel < 1000);
```

At this place in the program, if `waterLevel` is less than 1000, the expression is true, and the program continues normally. But if `waterLevel` is greater than or equal to 1000, `assert()` halts the program with the following error message:

```
a.out: x.cpp:9: int main(): Assertion 'waterLevel < 1000' failed.
Aborted (core dumped)
```

> Warning

> If `assert()` fails, it creates a core dump file. Unless you need that file, remove it as soon as possible to avoid wasting disk space.

The `assert()` macro expands into an `if` statement, in this case, something like this:

```
if (!(waterLevel < 1000))
    abort();
```

The reason for using `assert()` instead of writing statements like that is so that you can easily remove all such tests. To do that, insert the following definition above the `#include` directive that refers to `assert.h`:

```
#define NDEBUG
#include <assert.h>
```

Defining the symbol `NDEBUG` causes the `assert.h` header to declare `assert()` as a do-nothing macro. Because the macro now expands to nothing, the compiler effectively removes all `assert()` statements from the code. If problems develop later, simply comment-out `#define NDEBUG` and recompile to enable all assertions.

## DEBUGGING VARIABLES ROUNDUP

Following is a roundup of suggestions for debugging variables in C++ programs. Also examine the help information in `gdb` for additional commands you can use (type `help data` at a `gdb` prompt). When your code shows incorrect results, try these tips:

- Test your code using a wide range of data. In the case of the buggy Celsius converter, testing with only whole numbers such as 80 degrees gave correct results. Various fractional values aggravated the bug. Just because one test produces no errors does not mean that the code is bug free!

- Examine input and output variables. Often, a problem appears to be in a calculation when the true cause is an error in the input data. That old rule, garbage in; garbage out, remains as true today as ever.

- If you can't find the error in a complex expression, break it into pieces with temporary statements and use `gdb` to inspect the expression's intermediate results.

- 使用手持计算器检查所有表达式的结果。需要注意的是，你的系统和计算器内部的二进制格式可能不同，用于显示舍入值的算法也可能不同，因此不要期望结果完全相同。例如，我的计算器显示 75.5 华氏度等于 24.166666 摄氏度。而`celsius.cpp`程序报告的舍入值为 24.1667。

- 不要在会计软件中使用浮点变量来存储货币金额。使用`long`或`long long`值并假设值中有两位小数。（换句话说，以美分为单位存储货币值，以及你货币中最低的实际面额。）第 8 章“控制输入和输出”中“幸运便士”部分列出了一个示例程序`money.cpp`，展示了一种使用`long`和`long long`值的方法。

- 调用函数时——尤其是操作 C 风格字符串的函数——请确保不要混淆任何参数的顺序。语句`strcpy(A, B)`并不会将`A`复制到`B`，如直觉上可能认为的那样。它会将字符串`B`复制到`A`。首次使用标准函数时，请查阅在线信息和 man-page 文档。

### SUMMARY
