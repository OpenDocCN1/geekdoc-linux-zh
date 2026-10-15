
```
#include <iostream.h>

// A class that encapsulates data and functions
class TDate {
private:
    int dt_month;
    int dt_day;
    int dt_year;
public:
    TDate() {dt_month = 0; dt_day = 0; dt_year = 0;}
    TDate(int month, int day, int year)
    {
        dt_month = month;  // Assign values to private members
        dt_day = day;
        dt_year = year;
    }
    void display();
};

int main()
{
    TDate t1;
    TDate t2 = TDate(12, 31, 1999);  // Requires default ctor
    TDate t3(1, 1, 2000);             // Impractical, but allowed
    TDate t4(t3);                     // Uses parameterized ctor
    TDate t4(t3);                     // Makes t4 a copy of t3
    TDate t5 = t4;                    // Copies t4 into t5

    t1.Display();  // Call member function for each object
    t2.Display();
    t3.Display();
    t4.Display();
    t5.Display();

    return 0;
}

// The TDate class Display member function
void TDate::Display()
{
    cout << dt_month << "/" << dt_day << "/" << dt_year << endl;
}
```

修改后的 `TDate` 类的默认构造函数直接在类中声明和实现：

```
public:
    TDate() { dt_month = 0; dt_day = 0; dt_year = 0; }
```

这种格式起初可能看起来很奇怪，但它只是 C++ 源码的一种简写形式，你可以像下面这样写出它的长格式：

```
public:
    TDate()
    {
        dt_month = 0;
        dt_day = 0;
        dt_year = 0;
    }   // No semicolon here!
```

逐字符比较这两种版本，你会发现它们完全相同（除了注释）。要特别注意分号的位置，分号一如既往地结束语句，并且绝不会出现在复合语句块的右花括号之后。

第一条语句调用 `TDate()` 默认构造函数。第二条调用类的参数化构造函数。这种常见的类设计完全可接受，但你通常可以通过使用默认参数将这两种构造函数合并起来，如清单 12.5（`default.cpp`）所示。为了说明，新的 `TDate` 类也完整地以内联方式声明和实现了其构造函数和成员函数。

> 注意
>
> “constructor”一词常缩写为“ctor”。这不是保留字——你不能在程序中使用它——但你会在参考资料和注释中经常看到这个缩写。

### 清单 12.5 DEFAULT.CPP

```
#include <iostream.h>

// A fully implemented class
class TDate {
private:
    int dt_month;
    int dt_day;
    int dt_year;
public:
    TDate(int month = 0, int day = 0, int year = 0)
    {dt_month = month; dt_day = day; dt_year = year;}
    void Display()
    {cout << dt_month << "/"
         << dt_day
         << dt_year << endl;}
};

int main()
{
    TDate default_date;        // Calls default ctor
    default_date.Display();
    TDate tomorrow(4, 5, 2001);  // Calls parameterized ctor
    tomorrow.Display();
    return 0;
}
```

修订后的 `TDate()` 构造函数同时充当默认构造函数和参数化构造函数。该类像下面这样声明和实现构造函数：

```
TDate(int month = 0, int day = 0, int year = 0)
{dt_month = month; dt_day = day; dt_year = year;}
```

如果这看起来令人困惑，可以把这些语句分行写出来。由于新构造函数为所有三个参数——`month`、`day` 和 `year`——声明了默认值，因此它同时充当默认构造函数和参数化构造函数。当 `main()` 构造此对象时：

同样地，程序的第二个对象调用相同的构造函数，但这次使用的是字面量参数值：

```
TDate tomorrow(4, 5, 2001);
```

使用默认参数值来创建默认类构造函数是常见的 C++ 技术，你会经常遇到。当在自己的程序中使用该方法时，请务必理解，当所有参数都有默认值时，类可能也不能再声明一个不带参数的默认构造函数。以下代码无法编译：

```
public:
TDate();
TDate(int month = 0, int day = 0, int year = 0); // ???
```

这种常见错误会让编译器感到困惑，因为它无法决定应使用哪个构造函数来初始化声明为

```
TDate today; // ???
```

的对象。

这会失败，因为重载的构造函数和其他函数必须至少在一种参数类型上有所不同。为了解决冲突并恢复为两个独立的构造函数，一种解决方案是在备用构造函数中为除一个参数之外的所有参数指定默认值。例如，你可以通过将其更改为以下方式来修复前面的声明

```
public:
TDate();
TDate(int month, int day = 0, int year = 0);
```

在带参数的构造函数中，`month` 值现在是必需的，但 `day` 和 `year` 是可选的。默认构造函数和带参数的构造函数至少在一种参数上有所不同，并且使用以下语句构造 `TDate` 对象现在是可能的：

```
TDate t1;          // Calls default TDate constructor
TDate t2(4);       // Calls parameterized constructor
TDate t3(4, 5);    // Calls parameterized constructor
TDate t4(4, 5, 2000); // Calls parameterized constructor
```

## DEBUGGING CLASS OBJECTS

GNU 调试器可以显示类数据成员的值，并且可以跟踪成员函数，就像它对常规变量和函数执行这些任务一样好。以下是使用本章中的一个程序进行调试会话的示例运行。通过这里描述的命令来检查你自己的类对象，也可用于调查本书中的其他面向对象程序。

> Note
>
> 这里显示的行号可能与你在屏幕上看到的不同。

要为调试准备一个示例程序，请编译本章中的 `construct.cpp` 程序，然后使用以下命令将其加载到 GNU 调试器中：

```
$ g++ -g -o construct construct.cpp
$ gdb construct
```

## CHAPTER 12 INTRODUCING THE CLASS

输入 `L`（list）直到找到 `TDate t1` 的声明，并注意行号，可能为 27。在该行设置断点以在对象构造之前暂停代码。在 `(gdb)` 提示符下输入如下所示的命令：

```
(gdb) break 27
Breakpoint 1 at 0x80486ce: file construct.cpp, line 27.
```

接下来，运行程序直到断点。调试器会显示下一个要执行的语句（我删除了一些注释以使其适合本页）：

```
(gdb) run
Starting program: /src/c12/construct
Breakpoint 1, main () at construct.cpp:27
27  TDate t1;
```

使用 `print` 命令在构造之前检查 `t1` 的值：
