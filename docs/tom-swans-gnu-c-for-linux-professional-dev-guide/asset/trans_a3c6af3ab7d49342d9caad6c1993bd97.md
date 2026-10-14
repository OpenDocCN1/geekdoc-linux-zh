

## 表 8.1 I/O 流操纵符

| Manipulator | I/O | Effect |
|---|---|---|
| dec | I/O | Convert to decimal |
| endl | O | Start new line and flush stream |
| ends | O | Write null terminator |
| flush | O | Flush output stream |
| hex | I/O | Convert to hexadecimal |
| oct | I/O | Convert to octal |
| setbase(int n) | I/O | Set radix (number base) to n (0, 8, 10, or 16) |
| setfill(int c) | O | Set the fill character to c |
| setprecision(int n) | I/O | Set floating point precision to n |
| setw(int w) | O | Set column width to w |
| ws | I | Extract whitespace (input) |

你已经使用过表 8.1 中的一些操纵符。endl 操纵符如你所知，在如下语句中开始输出的新行

```
cout << "Start a new line" << endl;
```

同样，ends 操纵符在输出中插入一个空字符（字符串结束）。下面的语句写入三个字符串，每个字符串以空字符和新行结尾：

```
cout << "First string" << ends << endl;
<< "Second string" << ends << endl;
<< "Third string" << ends << endl;
```

你不会通常以这种方式编写代码来显示字符串，但你可能会用它来创建一个包含空字符结尾格式字符串的文件。使用 setw() 来设置下一个写入对象的列宽。这对于对齐列很有用。例如，要将列宽设置为 10 并在该列空间内右对齐写入一个字符串，使用如下语句

```
cout << setw(10) << s << endl;
```

宽度操纵符是短暂的，它仅影响下一个输出对象。将 setw() 与 setfill() 结合使用，用除空格以外的字符填充列。下面的语句在用 # 字符填充的 40 字符列中写入错误消息：

```
cout << setfill('#') << setw(40)
<< "Error: very dumb mistake" << endl;
```

使用 flush 操纵符刷新输出流，通常只有在检测到错误条件后才有必要：

```
if (!cout.good())
{
    cout << flush;
    cout.clear();
}
```

你可以用 setbase(n) 设置输入或输出的数字基数或基底，尽管使用 hex、dec 和 oct 可能同样好。下面的两个语句将输入基数设置为八进制（基数 8）并将值读入整数变量 n：

```
cin >> setbase(8) >> n;
cout << "n == " << n << endl;
```

如果用户输入 10，程序会显示 n == 8。你可以在输出和输入语句中使用 hex、oct、dec 和 setbase()。下面的语句以十六进制和十进制读取整数值 n，然后以十六进制（基数 16）显示 n 的值，并在前面加上 "0x"：

```
cout << "Enter hex value: ";
cin >> hex >> n;
cout << "Value == 0x" << setbase(16) << n << endl;
```

要格式化浮点值，无论是输入还是输出，使用 setprecision() 操纵符。括号中的值表示允许的输入或输出位数。结果值根据需要进行舍入。如果 double 变量 f 等于 3.14159，下面的语句显示 3.1416：

```
cout << "f == " << setprecision(5) << f << endl;
```

你也可以在输入语句中这样使用 setprecision()：

```
cin >> setprecision(5) >> f;
```

最后，使用 ws（吃掉空白）操纵符来吞噬空格。此语句忽略输入中的任何前导空格：

```
cin >> ws >> s;
```

然而，由于输入语句似乎无论如何都会忽略空白，ws 操纵符很少使用。

## 使用 sprintf() 系列进行格式化

本章迄今为止描述的 C++ 输出格式化方法对于许多程序来说已经足够，但基本技术提供的格式化控制不如有时所需的那样多。幸运的是，标准 C 库提供了一组函数，可以处理任何可想象的复杂性的格式化要求。为此演示，列表 8.7，convert2.cpp，使用标准库函数 sprintf() 为输出流语句准备一个字符串。

### 列表 8.7 CONVERT2.CPP

```
#include <iostream.h>
#include <stdio.h>
#include <stdlib.h>

#define BUFSIZE 128

char in_buffer [BUFSIZE];  // User input
char out_buffer [BUFSIZE];  // Formatted output string
int value;  // Input buffer converted to int

int main()
{
    cout << "Enter an integer value: ";
    cin.getline(in_buffer, BUFSIZE);  // Get input from user
    value = atoi(in_buffer);  // Convert to integer

    // Format output string in out_buffer using value
    sprintf(out_buffer,
        "Decimal=%d Hexadecimal=%#x Octal=%#o",
        value, value, value);

    cout << out_buffer << endl;  // Write formatted string
    return 0;
}
```

convert2.cpp 程序运行相同并产生与 convert.cpp 相同的输出（参见列表 8.6）。在新程序中，对标准库函数 sprintf()（打印格式化字符串）的调用执行了原始代码中 dec、hex 和 oct 操纵符的工作。格式化后，一个相对简单的输出流语句打印格式化的缓冲区（out_buffer）并开始新行。然而，这个简单程序并没有揭示 sprintf() 和相关函数的能力。许多 C++ 程序员使用这些标准 C 库函数来格式化他们的程序输出，学习如何使用它们是有用的。

sprintf() 函数在 stdlib.h 中声明，使用各种符号规则准备一个格式化值的字符字符串。对该函数，语句通常传递至少三个以逗号分隔的参数。这些参数是

- 一个输出 char 缓冲区，如 out_buffer（参见 convert2.cpp），足够大以容纳函数的结果
- 一个包含一个或多个嵌入式格式化指令的字面字符串，每个指令前面都有 %
- 每个嵌入在字面字符串中的格式化指令的一个对象或值

一个简单的例子演示了如何使用 sprintf()。考虑这个语句：

```
sprintf(out_buffer, "Decimal == %d", value);
```

