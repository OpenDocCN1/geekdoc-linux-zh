

## 互递归函数

由于它们直接调用自身，前一节中的阶乘函数等被称为包含式递归。另一种递归形式是当一个函数调用另一个函数，而后者最终又调用第一个函数时。如果将三面镜子放置成镜子1反射镜子2，镜子2反射镜子3，镜子3又反射镜子1，你就会得到互递归的图形说明。孩子们称之为万花筒。

互递归对于编写协同程序很有用。这些是相互依赖的函数，但并不一定要求一个函数必须在另一个函数之前被调用。清单10.11，onfirst.cpp，以一种有些轻浮的方式演示了互递归。它以艾伯特和科斯特洛著名的、具有喜剧性递归的“谁先上？”段子命名，onfirst.cpp 显示字母表。在继续之前，你能猜出它是如何工作的吗？

### LISTING 10.11 ONFIRST.CPP

```
#include <iostream.h>

// Function prototypes
void A(char c);
void B(char c);

int main()
{
    A('Z');
    cout << endl;
    return 0;
}

void A(char c)
{
    if (c > 'A')
        B(c);
    cout << c;
}

void B(char c)
{
    A(--c);
}
```

使用以下命令编译并运行程序。如图所示，程序以大写形式显示字母表：

```
$ g++ onfirst.cpp
$ ./a.out
ABCDEFGHIJKLMNOPQRSTUVWXYZ
```

主程序通过调用函数 A() 并传入参数 'Z' 启动递归。函数 A() 检查其参数 c。如果 c 在字母上大于 'A'，函数就会调用 B()，B() 立即调用 A()，并传入 c-- 作为参数。这导致 A() 再次检查 c，其值等于前一个值减一，然后再次调用 B()，直到 c 等于 'A'。此时，递归展开，执行输出语句26次，并逐个字符显示字母表。好吧，现在你可以笑了。

**Tip**  
使用 GNU 调试器的 next 和 step 命令逐步跟踪 onfirst.cpp，看看它是如何缓慢运行的。

## 函数与分离编译

将函数编译到单独的模块中通常很有用，这对于创建多个程序可以共享的函数库尤其有价值。为了说明这一点，以下清单创建了本章中 kilo.cpp 程序的模块化版本。清单10.12，kilos.h，是一个头文件，只包含一个元素：kilos() 函数原型。

### LISTING 10.12 KILOS.H

```
//==================================================
// kilos.h -- Function kilos() header file
// Copyright (c) 1999 by Tom Swan. All rights reserved.
//==================================================

// Function prototype
double kilos( double miles );
```

实际上，大多数头文件会声明多个函数原型以及其他项目，如常量。它们也可能声明全局变量。但在这种情况下，kilos.h 头文件仅声明了 kilos() 函数的原型。清单10.13，kilos.cpp，实现了该函数。

### LISTING 10.13 KILOTAB.CPP

```
//==================================================
// kilos.cpp -- Function kilos() implementation module
// Copyright (c) 1999 by Tom Swan. All rights reserved.
//==================================================

// Convert miles to kilometers
double kilos( double miles )
{
    return miles * 1.609344;
}
```

这与原始程序中的函数相同。然而，kilos.cpp 是一个没有 main() 函数的独立模块。头文件和独立模块文件使用相同名称是很常见且通常明智的做法——本例中为 kilos.h 和 kilos.cpp。这不是必需的，但有助于你跟踪模块及其相关的头文件。要完成程序，需要编写另一个包含 main() 函数的模块。清单10.14，kilotab.cpp，完成了这一工作。

### LISTING 10.14 KILOTAB.CPP

```
#include <iostream.h>
#include <iomanip.h>   // Need setw() manipulator
#include "kilos.h"     // Need kilos() function

int main()
{
    cout << "Miles    Kilometers" << endl;
    cout << "===========" << endl;
    for (int miles = 0; miles <= 200; miles += 20) {
        cout << setw(5) << miles << "   m   ";
        cout << kilos( miles ) << endl;
    }
    return 0;
}
```

完成的程序通过以下指令包含单独编译的 kilos() 函数：

```
#include "kilos.h"
```

引号告诉编译器 kilos.h 在当前目录中，或由选项 -I 指定的目录中（参见第5章“编译和调试 C++ 程序”）。包含头文件声明了 kilos() 原型，这就是程序编译所需的全部内容。在编译的最后阶段，GNU 链接器会搜索包含原型函数实现的 object-code 模块。链接器必须找到所有已声明函数的实现，否则会以错误结束。要编译单独的 kilos.cpp 模块和 kilotab 程序，并链接它们的独立 object-code 文件，请输入以下命令：

```
$ g++ -c kilos.cpp
$ g++ kilotab.cpp kilos.o
$ ./a.out
```

## 调试函数

最后在本章中，关于调试函数和参数的一些说明。正如以下各节所述，GNU 调试器提供了几个命令，这些命令对于跟踪函数语句特别有价值。

