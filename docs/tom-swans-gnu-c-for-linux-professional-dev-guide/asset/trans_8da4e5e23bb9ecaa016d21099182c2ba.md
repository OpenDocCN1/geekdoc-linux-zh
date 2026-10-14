
注意
Tdate.cpp 源代码文件并不是一个完整的程序。关于如何编译和使用独立模块的说明，请参阅下一节。

## 清单 13.7 TDATE.CPP

```
#include <iostream.h>
#include "tdate.h"  // Also includes time.h

// Buffer to hold date string. This buffer is used by all
// TDate objects, and is overwritten by calls to member
// functions.
// String format: Fri 14-May-2004 (15 characters)
#define BUF_SIZE 16
char cbuf[BUF_SIZE];

// Default constructor implementation
TDate::TDate()
{
    Update(); // Initialize object date to today
}

// Parameterize constructor implementation
TDate::TDate(int month, int day = 0, int year = 0)
{
    Update(); // Initialize object date to today

    // Create a tm struct using tv_time data member
    tm t = *localtime(&tv_time);

    // Assign argument values if specified to struct
    t.tm_mon = month - 1;
    if (day > 0) t.tm_mday = day;
    if (year > 0) t.tm_year = year - 1990;

    // Convert struct back into tv_time value
    tv_time = mktime(&t);
}

// Update time to "now"
void TDate::Update()
{
    time(&tv_time); // Calls the standard time() function
}

// Write date and time to the standard output
void TDate::Display()
{
    cout << AsString() << endl;
}

// Return date and time as a formatted string
const char *TDate::AsString()
{
```

```
tm t = *localtime(&tv_time);  // Convert tv_time to struct
strftime(cbuf, BUF_SIZE, "%a %d-%b-%Y", &t);  // Create cbuf
return (const char *)&cbuf;  // Return pointer to buffer
```

tdate.h 和 tdate.cpp 共同构成了 TDate 类的一个自包含模块。要编译该模块，请按如下方式使用 `-c` 编译器选项：

```
$ g++ -c tdate.cpp
```

这会在当前目录中创建目标代码文件 `tdate.o`。此时有必要理解：如果需要向 TDate 中构建新代码，程序可以将 TDate 类继承到一个新类中，而无需以任何方式修改原始模块。事实上，只需 `tdate.h` 头文件即可——使用和增强模块化的 TDate 类并不需要源代码。这是一个很好的例子，说明如何通过使用类和对象来创建真正模块化的程序，复用代码而不是重写代码。

新的 TDate 类还演示了类如何封装 GNU C 库中的标准函数和数据，这是将传统编程引入面向对象领域的好方法。例如，TDate 类的 `Update()` 成员函数调用标准 `time()` 函数，将当前日期和时间赋给类的私有 `tv_time` 数据成员：

```
time(&tv_time);
```

因为类的默认构造函数调用 `Update()`，使用此构造函数创建的对象会自动设置为今天的日期。利用这一特性，宿主程序可以用简单的语句创建并显示当前日期，例如：

```
TDate today;
today.Display();
```

多么简单！使用类来封装那些常常令人困惑的标准日期和时间函数，极大地简化了库的使用。

> 注意
> 标准库的 `time_t` 值等于从 1970 年 1 月 1 日 00:00:00 世界协调时间（UTC）起经过的秒数。此处展示的 TDate 类可以表示从那时开始的日期。

TDate 类的参数化构造函数允许程序使用如下语句构造具有显式日期的 TDate 对象：

```
TDate future(4, 3, 2005);
```

只有月份是必需的；年和日的值是可选的，如果未指定，则默认为今天的日期。在构造函数中，在调用 `Update()` 将对象初始化为当前日期之后，有一条语句调用标准 `localtime()` 函数。这会返回一个 `tm` 结构体，其中 `tv_time` 的值被转换为表示日、月、年和其他值的字段：

```
tm t = *localtime(&tv_time);
```

有了初始化后的结构体，构造函数会用 month、day 和 year 参数（如果提供的值大于零）替换选定的字段：

```
t.tm_mon = month - 1;
if (day > 0) t.tm_mday = day;
if (year > 0) t.tm_year = year - 1900;
```

最后，构造函数将修改后的结构体转换回 `time_t` 值，并将结果存储在对象的私有 `tv_time` 数据成员中：

```
tv_time = mktime(&t);
```

TDate 类中另一个有趣的成员函数是 `AsString()`。该函数调用标准库的 `strftime()` 函数，将对象的日期和时间转换为格式化字符串。由于这个类只关心日期，`strftime()` 获得的格式字符串会忽略 `tv_time` 值中的时间信息。以下语句在模块的字符缓冲区 `cbuf` 中创建字符串，并将其作为 `const char` 指针返回：

```
tm t = *localtime(&tv_time);    // Convert tv_time to struct
strftime(cbuf, BUF_SIZE, "%a %b-%d %Y", &t);  // Create string
return (const char *)&cbuf;     // Return pointer to buffer
```

使用此函数，宿主程序可以通过输出流语句显示时间，例如：

```
TDate today;
cout << "Today is " << today.AsString() << endl;
```

> 提示
> TDate 中的 `Display()` 成员函数不一定是将对象数据写入标准输出的最佳方式。一种更好、更面向对象的方法是重新编程 `<<` 和 `>>` 运算符，使其能够识别 TDate 类类型的对象。第 20 章“定制 I/O 流”说明了如何做到这一点。

## TDate 宿主程序

如前所述，前面几节中实现的 TDate 类模块并不是一个完整的程序。要使用这个类，需要一个带有 `main()` 函数的宿主程序。该程序包含 `tdate.h` 头文件，并与模块编译后的目标代码文件链接。清单 13.8（datetest.cpp）测试了 TDate 类模块，并展示了如何使用这个独立的类模块。

