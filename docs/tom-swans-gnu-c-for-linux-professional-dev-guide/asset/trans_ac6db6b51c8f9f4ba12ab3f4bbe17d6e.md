

```
{
    cin >> s;
}
```

使用以下命令编译并运行程序，然后如图所示，输入一个字符串，在按下 Enter 后它会显示在最后一行：

```
$ g++ getstr.cpp
$ ./a.out
Enter a string: abcdefg
You entered: abcdefg
```

示例程序原型化了一个函数，用于将字符串输入到全局字符缓冲区中。该函数的原型展示了如何声明指针参数：

void getstr(char *s);

参数 s 是一个指向 char 的指针。由于 C 语言的一个古老规范，指针和数组在程序上是等价的，因此通常使用指针将输入字符数组传递给 getstr()。要使用该函数，程序按如下方式声明 input 并将其传递给函数以填充用户输入：

```
char input[128];
...
getstr(input);
```

## FUNCTION RETURN VALUES

正如你在本书的示例中所见，函数可以不返回任何内容，也可以返回任何有效的 C++ 类型的值。以下各节将更详细地解释函数返回值。作为一个实际示例，本节中的一个示例列表展示了如何使用标准 GNU C 库的时间函数创建一个经过事件计时器。

## RETURNING SIMPLE VALUES

正如你在本书的许多示例程序中所见，函数可能不返回任何内容，也可能返回任何有效的 C++ 数据类型的值，例如 int 或 double。要表示函数不返回任何内容，请在其声明前加上 void：

```
void f();
```

尽管允许这种技术，但它很少有用，通常你会将函数的返回值保存在变量中，或在语句中使用它，如以下示例所示：

```
double saved_value = f();
cout << "Value == " << f() << endl;
```

返回值对于构建模块化程序至关重要。作为一个实际演示，列表 10.6 stopwatch.cpp 使用系统时钟创建一个计时器，准确度为 1/10 秒（当然取决于系统时钟的准确度），独立于计算机处理器速度。

### LISTING 10.6 STOPWATCH.CPP

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

编译并运行 stopwatch.cpp。提示时，按 Enter 开始计时，等待几秒钟，然后再次按 Enter 停止计时并显示结果，如以下测试运行所示：

在函数作用域之外持续存在。换句话说，函数不能返回对局部变量或参数的引用。声明为

```
double &ref();
```

的函数返回一个指向 double 对象的引用，很可能是在其他地方声明的。在你不希望函数的调用者有权更改被引用值的情况下，可以像这样声明函数为 const：

```
const double &ref();
```

你可以在赋值运算符的两侧使用引用函数。以下这样的语句将 3.14159 存储在 ref() 函数所引用的任何 double 对象中：

```
ref() = 3.14159;
```

ref() 函数本身可能写成如下形式：

```
double d;
double &ref()
{
    return d; // Return reference to d
}
```

由于 ref() 只是返回对全局变量 d 的引用，引用函数在某种意义上是该对象的同义词。如果 d 隐藏在库模块中，所有对它的引用都可以通过强制数据使用者调用 ref() 来控制。这隐藏了全局数据的内部本质，同时也有助于调试。

前面的示例代码仅用于说明。类似但更复杂的编程对于在提供对其信息的安全访问的同时隐藏数据结构的内部表示非常宝贵。例如，引用函数可能从数组中返回一个选定的值。引用函数在面向对象编程中也发挥着重要作用，这是本书第三部分的主题。

## RETURNING POINTERS TO DATA

与指针参数一样，本章如果不提及函数也可以返回指针值就不完整。但有关此主题的更多信息，请参阅第 11 章“使用指针管理内存”。

## OTHER FUNCTIONALITIES

以下是关于函数的一些额外主题，包括仅在 C++ 中可用的一些功能。

