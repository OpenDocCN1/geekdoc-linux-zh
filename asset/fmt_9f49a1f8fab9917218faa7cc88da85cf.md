
```
#include <iostream.h>
#include <sys/times.h>    // need times() function
#include <time.h>        // need CLOCKS_PER_SEC
#include <math.h>        // need fabs() function

// Function prototypes
clock_t mark_time();
double elapsed_time(clock_t start_time, clock_t end_time);

// Main program
int main()
{
    clock_t start, stop;  // Variables for mark_time() function

    cout << "Press enter to start timing...";
    cin.get();
    start = mark_time();  // Mark starting time
    cout << "Press enter to stop timing...";
    cin.get();
    stop = mark_time();   // Mark stopping time
    cout << "Elapsed time was "
         << elapsed_time(start, stop)
         << " seconds" << endl;
    return 0;
}

// Returns current processor time (mark)
clock_t mark_time()
{
    return times(NULL);
}

// Calculate elapsed time in seconds
double elapsed_time(clock_t start_time, clock_t end_time)
{
    double t = fabs(end_time - start_time);  // Processor elapsed time
    return t / (CLOCKS_PER_SEC / 10000);     // Elapsed time in seconds
}
```

编译并运行 `stopwatch.cpp`。提示时，按 Enter 开始计时，等待几秒钟，然后再次按 Enter 停止计时并显示结果，如以下测试运行所示：

在函数作用域之外持续存在。换句话说，函数不能返回对局部变量或参数的引用。声明为

```
double &ref();
```

的函数返回一个指向 double 对象的引用，很可能是在其他地方声明的。在你不希望函数的调用者有权更改被引用值的情况下，可以像这样声明函数为 const：

```
const double &ref();
```

你可以在赋值运算符的两侧使用引用函数。以下这样的语句将 3.14159 存储在 `ref()` 函数所引用的任何 double 对象中：

```
ref() = 3.14159;
```

`ref()` 函数本身可能写成如下形式：

```
double d;
double &ref()
{
    return d; // Return reference to d
}
```

由于 `ref()` 只是返回对全局变量 `d` 的引用，引用函数在某种意义上是该对象的同义词。如果 `d` 隐藏在库模块中，所有对它的引用都可以通过强制数据使用者调用 `ref()` 来控制。这隐藏了全局数据的内部本质，同时也有助于调试。

前面的示例代码仅用于说明。类似但更复杂的编程对于在提供对其信息的安全访问的同时隐藏数据结构的内部表示非常宝贵。例如，引用函数可能从数组中返回一个选定的值。引用函数在面向对象编程中也发挥着重要作用，这是本书第三部分的主题。

## RETURNING POINTERS TO DATA

与指针参数一样，本章如果不提及函数也可以返回指针值就不完整。但有关此主题的更多信息，请参阅第 11 章“使用指针管理内存”。

## OTHER FUNCTIONALITIES

以下是关于函数的一些额外主题，包括仅在 C++ 中可用的一些功能。

### 默认函数参数

一个有用的 C++ 创新为函数参数提供了默认值。这可以在你只需要提供部分参数，而非全部参数时帮助清理代码。为了说明，考虑一个返回四个 int 值之和的函数：

```
int sum(int a, int b, int c, int d)
{
    return a + b + c + d;
}
```

要仅用两个参数调用该函数——我们称它们为 `v1` 和 `v2`——你需要向未使用的参数提供零以避免编译器错误：

```
cout << sum(v1, v2, 0, 0);
```

这并不是什么大问题，但确实要求你查阅 `sum()` 的文档以确定向哪些未使用参数提供什么值。使用默认参数，就不再需要这样的语句：

```
int sum(int a, int b, int c = 0, int d = 0);
```

这样声明后，`sum()` 现在只需要两个参数，但最多可有四个。默认值必须位于函数参数列表的最后。在使用新的 `sum()` 函数时，如果未为 `c` 或 `d` 指定参数，则这些参数将赋予默认值。以下语句现在都是允许的：

```
cout << sum(1, 2);        // a == 1, b == 2, c == 0, d == 0
cout << sum(1, 2, 3);     // a == 1, b == 2, c == 3, d == 0
cout << sum(1, 2, 3, 4);  // a == 1, b == 2, c == 3, d == 4
```

在某些 C++ 方言中，只有函数原型才允许声明默认函数参数。GNU C++ 在两个地方都允许。给定 `sum()` 的前述声明，像这样实现该函数：

```
int sum(int a, int b, int c = 0, int d = 0)
{
    return a + b + c + d;
}
```

注意

> 原型中默认参数值与函数实现中的默认值之间存在任何差异都会产生 "default argument..." 编译错误。

列表 10.7，`center.cpp`，展示了默认函数参数的实用示例。该程序通过将输入字符串复制到输出字符串缓冲区，并在其周围加上一个或两个填充字符来居中输入字符串——这对于创建错误消息和分隔行很有用。使用示例程序的 `center()` 函数来准备如下两个示例字符串：

```
**** Error: You goofed big time! ****
<<<<<<< Press any key to continue >>>>>>>
```

#### LISTING 10.7 CENTER.CPP
