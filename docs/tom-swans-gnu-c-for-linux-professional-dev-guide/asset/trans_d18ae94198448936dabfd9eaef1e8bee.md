

回到 `main()` 中，另一条语句可以检查 `error`，并将其用作标志，以选择两种结束程序的方式之一：

```
int main()
{
    if (error)
        return 1;
    else
        return 0;
}
```

你还没有见过 `if` 语句，但这段代码的作用应该很明显。如果 `error` 变量为真，程序返回 `1` 作为错误码；否则返回 `0`，表示没有错误。

> **注意**
> C 程序使用整数变量来表示真（任何非零值）和假（0）。在 C++ 中你也可以这样做，但使用 `bool` 类型会更加清晰。另外，`bool` 变量的大小为一个字节，`int` 则占用四个字节，相对比较浪费。

## 字面量

你可以使用十进制、十六进制或八进制基数来指定整数字面值。除 `0` 以外，十进制常量必须以非零数字开头。以 `0` 开头的常量是八进制值，只能包含 `0` 到 `7` 的数字。以 `0x` 或 `0X` 开头的常量是十六进制，可以包含 `0` 到 `9` 的数字以及大写或小写的 `A` 到 `F`。清单 6.6（`literal.cpp`）声明了用十六进制、八进制和十进制字面值初始化的 `int` 变量。

### 清单 6.6 LITERAL.CPP

```
#include <iostream.h>

int main()
{
    int hexValue = 0xF9AC;
    int octalValue = 0724;
    int decimalValue = 255;

    cout << "hexValue == " << hexValue << endl;
    cout << "octalValue == " << octalValue << endl;
    cout << "decimalValue == " << decimalValue << endl;

    return 0;
}
```

编译并运行 `literal.cpp` 实际上会将示例程序中的八进制和十六进制值转换为十进制。输入以下命令来编译并运行程序：

```
$ g++ literal.cpp
$ ./a.out
hexValue == 63916
octalValue == 468
decimalValue == 255
```

如输出所示，默认输出格式为十进制。虽然字面值 `0xF9AC` 以十六进制表示，但在内部它只是一个与其他整数值一样的整数。由于整数的默认输出格式是十进制，将十六进制和八进制值写入 `cout` 时，会以十进制显示它们。

> **注意**
> 第8章“控制输入与输出”将说明如何使用十六进制、八进制和十进制输出格式来显示整数值。

## 字面常量范围

除了基数之外，你还可以指定字面值的数据类型，这有时对于确保 GNU C++ 在内部按照你想要的方式表示字面值是必要的。例如，要确保编译器将 `100` 视为 `long int`，可以添加后缀 `L`。下面的声明将长整数值 `1234L` 赋给名为 `bigValue` 的变量：

```
long bigValue = 1234L;
```

若要指定 `unsigned long` 值，请添加 `uL`。例如，下面将无符号长整数值 `1234UL` 赋给 `bigValue`。这些值相同，但在内部会根据其特定类型在内存中进行表示：

```
unsigned long bigValue = 1234UL;
```

> **注意**
> 由于 GNU C++ 通常将整数常量表示为 `long` 或 `unsigned long` 值，因此很少需要后缀 `L` 和 `UL`。但是，其他将整数常量表示为 `int` 类型的 C 和 C++ 编译器可能需要它们。为了提高可移植性，最好为所有应被视为 `long` 或 `unsigned long` 的常量加上 `L` 或 `UL`。

## 双宽整数

GNU C++ 允许一种名为 `long long` 的特殊“双宽”整数类型，它可以存储真正巨大的值。清单 6.7（`verybig.cpp`）演示了如何声明 `long long` 整数，并确定它们可以表示的最小值和最大值。

### 清单 6.7 VERYBIG.CPP

```
#include <iostream.h>

long long min_signed, max_signed;
unsigned long long max_unsigned;

main()
{
    // Assign minimum and maximum values to var1 and var2
    // Assign maximum value to unsigned var3
    min_signed = 0x8000000000000000LL;
    max_signed = 0x7FFFFFFFFFFFFFFFLL;
    max_unsigned = 0xFFFFFFFFFFFFFFFFULL;

    cout << "Signed long long range" << endl;
    cout << " " << min_signed << " ... ";
    cout << max_signed << endl;
    cout << "Unsigned long long range" << endl;
    cout << "0 ... " << max_unsigned << endl;
    cout << "long long size in bytes == ";
    cout << sizeof(max_unsigned) << endl;

    return 0;
}
```

使用以下命令编译并运行 `verybig.cpp` 程序时，它会报告有符号和无符号 `long long` 整数值的最小值和最大值，并显示 `long long` 变量的大小（以字节为单位）：

```
$ g++ verybig.cpp
$ ./a.out
Signed long long range
-9223372036854775808 ... 9223372036854775807
Unsigned long long range
0 ... 18446744073709551615
long long size in bytes == 8
```

程序的输出表明，有符号 `long long` 整数能够表示巨大的数值，范围为正负 9 千万亿左右。无符号 `long long` 整数将最大值扩大到超过 1.8 亿亿。这对我来说绝对足够大，足以容纳我的银行存款，而且不会有溢出的危险。

### 提示

> 通过假定一个小数点，`long` 和 `long long` 整数适用于会计和电子表格软件。（参见第8章“控制输入与输出”，了解如何将值格式化为字符串——例如，在 `long` 或 `long long` 整数值中插入小数点。）

由于 GNU C++ 将整数字面常量表示为 `long` 或 `unsigned long` 类型，示例程序中的十六进制赋值必须以 `LL` 和 `ULL` 结尾，以防止出现超出范围的警告。虽然从表面上看，第三个常量并不是以单词“FULL”结尾的。那是一个十六进制的 `F` 后跟 `ULL`，表示 `unsigned long long`：

```
min_signed = 0x8000000000000000LL;
max_signed = 0x7FFFFFFFFFFFFFFFLL;
max_unsigned = 0xFFFFFFFFFFFFFFFFULL;
```

