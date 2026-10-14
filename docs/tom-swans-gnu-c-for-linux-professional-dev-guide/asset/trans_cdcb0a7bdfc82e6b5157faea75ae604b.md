

abort() 函数在 totem pole 上处于最低位置。如果程序在异常处理中到达此阶段，它会立即结束并将内存写入核心转储文件。为了防止这种情况，你可以重写 unexpected() 和 terminate() 函数，从而捕获在 catch 语句中未处理的任何异常。

## 替换 unexpected() 和 terminate()

你可以用新代码替换 unexpected() 和 terminate()，以你想要的任何方式处理未处理的异常。例如，在程序开发期间，将 unexpected() 替换为仅通知你任何未处理异常可能是有意义的。然后你可以添加适当的 catch 语句，在异常变得致命之前捕获它们。你也可以用诊断信息替换 terminate()，用于调试损坏的堆栈或在对象处置期间抛出的异常的原因（这可能表明内存管理存在问题）。

通常情况下，替换 unexpected() 就足以确保程序永远不会因未处理的异常而意外停止。terminate() 函数最好用于关闭关键服务、保存打开的文件，并在结束程序之前执行其他灾难恢复操作。如果程序最终进入 terminate()，你应该假设最坏的情况，尽可能清理，然后优雅地结束。你永远无法替换 abort()。

包含异常头文件提供了两个可以调用的函数来替换默认的异常处理程序。这些函数声明为

```
terminate_handler set_terminate (terminate_handler func);
unexpected_handler set_unexpected (unexpected_handler func);
```

在每种情况下，将一个返回 void 且不声明参数的函数传递给 set_terminate() 和 set_unexpected() 函数。例如，像这样编写自己的处理程序：

```
void MyHandler()
{
    // ... statements in your handler
}
```

要使用处理程序捕获意外异常，将函数名作为参数传递给 set_unexpected()：

```
set_unexpected(MyHandler);
```

或者，你可以用如下代码保存原始处理程序的地址

```
unexpected_handler saved_handle; // Variable
saved_handle = set_unexpected(MyHandler);
```

然后你可以恢复原始处理程序的地址——如果多个模块安装自己的自定义处理程序，这是一种很好的技术。类似地，通过调用以下内容设置默认的 terminate() 函数：

```
set_terminate(MyHandler);
```

## 捕获所有异常

编写能够安全处理所有可能异常的自定义异常处理程序并不像基本技术所暗示的那样容易。本节展示了一个模拟多种类型错误并使用自定义处理程序安全捕获它们的示例。列表 16.4，unexpect.cpp，演示了如何用自定义函数替换默认的异常处理程序，以捕获所有可能的程序错误。它处理未知类型的异常，并演示了如何在结束程序之前获得最后一次执行关键措施的机会。

```
LISTING 16.4 UNEXPECT.CPP
#include <iostream.h>
#include <exception>

#define MAXERR 10

// Exception class used when errors exceed limit
class MaxError { };

// Normal error exception class
class Error {
private:
    static int count;  // Count of Error objects
public:
    Error();           // Constructor
    void Say();        // Report static error count
};

// Prototype for function that throws an exception
void run() throw(Error);

// Prototypes for custom exception handlers
void custom_unexpected();
void custom_terminate();

// Global static counter for Error class objects
int Error::count;

void main()
{
    set_unexpected( custom_unexpected );
    set_terminate( custom_terminate );
    for (;;) {
        try {
            run();  // Throws an exception
        }
        catch (Error e) {
            e.Say();
        }
    }
    return 0;
}
```

### LISTING 16.4 CONTINUED

```
// Function that throws an exception
void run() throw(Error)
{
    throw Error();
    // throw "An unknown exception object";
}

// Our unexpected exception handler
void custom_unexpected()
{
    cout << "Inside custom_unexpected function" << endl;
    throw Error(); // Continues program
}

// Our terminate exception handler
void custom_terminate()
{
    cout << "Inside terminate function" << endl;
    cout << "Exiting program" << endl;
    exit(1); // Exits program
}

// Error class constructor
Error::Error()
{
    count++;
    if (count > MAXERR)
        throw MaxError(); // Abort object construction!
}

// Error class reporting function
void Error::Say()
{
    cout << "Error: count = " << count << endl;
}
```

unexpect.cpp 程序列出了捕获所有可能异常所需的所有元素。该程序并不能防止异常终止，但它确实接管了调用 abort() 及其不可避免的核心转储的默认操作。通过使用类似的代码，你可以捕获每种类型的异常，至少在有必要提前结束程序时，有机会以有序的方式关闭程序。使用以下命令编译并运行程序：

```
$ g++ unexpect.cpp
$ ./a.out
Error: count = 1
Error: count = 2
...
Error: count = 10
Inside custom_unexpected function
Inside terminate function
Exiting program
```

