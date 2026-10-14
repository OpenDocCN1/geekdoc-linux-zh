

> Note
> stdlib.h 声明了其他字符串到二进制的函数，例如 strtod()（字符串到双精度）、strtol()（字符串到长整型）和 strtoul()（字符串到无符号长整型），在 Linux 手册页中有在线描述。使用这些函数需要理解指针，在第 11 章“使用指针管理内存”中介绍。

## STIR-FRIED STRINGS

如果你喜欢炒蔬菜，你会喜欢 GNU C++ 的 strfry() 函数。它通过随机打乱来搅乱任意字符串中的字符。虽然这看起来似乎很无聊，但它可能被用于程序中混合字符串或其他缓冲区中的字节值——例如，为随机化测试数据做准备，或用于加密算法。清单 6.14，scramble.cpp，演示了 strfry() 函数。

> Note
> strfry() 函数可能仅限于 Linux 和 GNU C 标准库。

### LISTING 6.14 SCRAMBLE.CPP

```
#include <iostream.h>
#include <string.h>

// The following three lines may be required if strfry()
// is not declared in string.h.

extern "C" {
    char *strfry(char *string);
}

char alpha[] = "abcdefghjklmnopqrstuvwxyz";

main()
{
    cout << "before : " << alpha << endl;
    strfry(alpha);
    cout << "after  : " << alpha << endl;
    return 0;
}
```

编译并运行程序以打乱 alpha 字符字符串。多次运行它以测试系统的随机数生成器（但试验之间请等待一秒，因为生成器使用当前时间作为起始种子）。输入以下命令：

```
$ g++ scramble.cpp
$ ./a.out
before : abcdefghijklmnopqrstuvwxyz
after  : niaoldtpwqb kefajghvcruymx
```

由于 strfry() 被记录为仅限于 Linux 和 GNU C 和 C++，你可能在其他标准 C 库中找不到该函数。此外，它似乎没有在编译器随附的标准 string.h 头文件中声明，这是一个错误，导致调用 strfry() 的任何程序都会出现此警告：

```
warning: implicit declaration of function 'int strfry(...)'
```

> Note
> GNU C++ 的后续版本似乎已在 string.h 中正确声明该函数，因此你可能看不到此警告。

如果你收到警告，程序仍然能正确工作，因为 strfry() 位于编译库中，即使它没有在 string.h 中按应有的方式声明。然而，你可以使用以下行来声明该函数并消除警告：

```
extern "C" {
    char *strfry(char *string);
}
```

> Note
> extern "C" 指令将 C 函数声明封装起来以供 C++ 程序使用。这是因为 C++ 编译器在编译期间“破坏”函数名和其他标识符以创建唯一符号。extern "C" 指令禁用名称破坏，以便链接器可以找到声明的 C 函数的编译代码。

## ARRAYS AND STRUCTS

数组只是在内存中彼此相邻存储的一系列相同类型的对象。结构体是可能不同类型的对象集合，也存储在一起。以下各节介绍这些复杂数据类型。

## SINGLE-DIMENSIONAL ARRAYS

你已经见过一个单维数组的例子——声明为 C 风格字符串

```
char input[128];
```

这创建了一个名为 input 的变量，作为 128 个 char 值的数组。类似地，你可以创建其他数据类型的数组。这里有一个包含 10 个 double 对象的数组：

```
double values[10];
```

## PREINITIALIZING ARRAYS

初始化数组的另一种有用方法是直接在源代码中指定初始值。你已经见过该技术的例子，如下所示：

```
char title[] = "My Super Encryption Program";
```

这创建了一个名为 title 的 C 风格字符串变量。实际上，title 是一个单维 char 值数组，每个值都初始化为引号字符串中的一个字符。编译器创建的数组大小正好足以容纳字符串，外加一个字节用于其空终止符。你可以使用类似的声明来初始化其他类型的数组。例如，以下内容创建了一个包含 10 个整数的数组并为每个元素赋值：

```
int digits[] = {9, 8, 7, 6, 5, 4, 3, 2, 1, 0};
```

digits 数组的大小足以容纳 10 个整数值，每个都初始化为大括号中的字面值。因为方括号中未指定大小，编译器会根据初始值计算数组的大小。然而，你也可以使用如下声明指定不同的大小

```
int digits[10] = {5, 4, 3, 2, 1};
```

这创建了一个包含 10 个整数的数组，但只初始化前 5 个。下标 5 到 9 的剩余元素如果数组是全局的则会被清零，如果数组是函数本地的则会被设置为不可预测的值。

## INITIALIZING ARRAYS OF STRINGS

一种常见的结构存储 C 风格字符串的数组。例如，清单 6.15 使用一个数组来保存月份名称。

### LISTING 6.15 MONTHS.CPP

```
#include <iostream.h>

char months[12][4] = {
"Jan", "Feb", "Mar", "Apr",
"May", "Jun", "Jul", "Aug",
"Sep", "Oct", "Nov", "Dec"
};

int main()
{
for (int month = 0; month < 12; month++)
cout << months[month] << " ";
cout << endl;
return 0;
}
```

> Tip
> 声明为在任何函数外部的全局变量的数组会自动初始化为全零字节。

