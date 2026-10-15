
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

排版后：

[content]
### `lpStartAddress` 和 `lpParameter` 参数

要创建一个线程，必须为操作系统提供新线程应该开始执行的当前地址空间。在传统的编程语言（如 C）中，计算通常无法直接从某个过程的中间开始；到新逻辑上下文的跳转是通过将新代码封装在一个过程中，然后在其入口处调用它来处理的。`lpStartAddress` 是一个函数的入口点地址，该函数的原型类型为：

```
DWORD WINAPI ThreadFunc(LPVOID);
```

也就是说，在会检查调用入口与函数类型匹配的语言（如 ANSI C 和 C++）中，在入口点作为参数使用之前，必须有一个函数原型。当然，这意味着还必须有一个函数来实现该原型——即新线程在创建后开始执行的函数。

这种场景中的一个复杂情况与向新线程执行的函数传递参数有关。由于存在调用和原型，如果要设置参数，则其类型必须已知并声明，或者必须使用 `void` 类型（以告诉编译器线程函数的参数类型在编译时未知）。`CreateThread` 使用了后一种方法，这就是为什么函数原型使用 `LPVOID`（定义为 `void *`）。当新线程开始执行该函数时，`lpParameter` 值将传递给该函数。

对于示例案例，假设有一个原型如下的函数：

```
DWORD WINAPI myFunc(LPVOID);
```

新线程正在执行它。此外，假设“父线程”打算将一个整数参数 `thArg` 传递给新的“子线程”。现在示例案例可以采用形式：

```
CreateThread(NULL, 0, myFunc, &thArg, ...);
```

### `dwCreationFlags` 参数

`dwCreationFlags` 参数用于控制新线程的创建方式。目前该参数只能传递一个标志值 `CREATE_SUSPENDED`。这将导致新线程创建后被挂起，直到另一个线程在目标线程上执行

```
ResumeThread(targetThreadHandle);
```

（`targetThreadHandle` 是新线程的句柄）。默认值为 0，这会导致线程在创建时处于激活状态。添加此参数后，示例变为：

```
CreateThread(NULL, 0, myFunc, &hArg, ...);
```

### `lpThread` 参数

最后一个参数是一个指向系统级线程标识的指针：

```
WORD:
WORD targetThreadID;
```

...

```
CreateThread(NULL, 0, myFunc, &theArg, 0, &targetThreadID);
```

## 使用 `CreateThread` 的复杂性

上一节解释了如何创建线程，除非你正在使用 C 运行时库（为了书中的练习，你确实在使用它）。C 库开发于 UNIX 环境，在那个环境下进程和线程之间没有区别。在 Windows 操作系统的背景下，许多线程可以在单个地址空间中执行。所有线程都可以访问地址空间中的信息——毕竟，这意味着线程很容易通过写入进程变量来相互共享信息。从好的方面来说，这意味着“一个地址空间”（未分配在单个线程栈中的空间）。从负面方面来说，这意味着栈之外的变量都可以被任何线程读取或写入——即使该变量可能只包含与一个线程相关的信息。

> [Richter 1997] 提供了此类变量 `error` 的绝佳示例。如果你从未使用过 `error`，可以将其想象为一个全局变量，如果调用恰好发生错误，运行时函数会设置它。在 UNIX 环境下，进程-线程库读取 `error` 来确定在 C 库调用上可能发生的错误类型。

只要有一个线程在执行该进程，这就是好的。但在 Windows 中会发生竞态条件：假设有两个线程 R 和 S 在一个进程中执行，并且它们都决定并发调用 C 运行时函数。这意味着在单个处理器上，要么是 R 要是 S 调用该函数并返回。示例假设 R 的调用导致了错误，但 `error` 没有被设置以反映错误的性质（也就是说，R 应该在检测到调用失败后立即检查 `error`）。现在假设线程调度程序在 R 返回之后但在检查 `error` 之前中断了 R。调度程序派发了 S，S 调用了它的运行时函数。这覆盖了 R 如果没有被中断本应拥有的旧值。S 检测到错误并读取了 `error` 但没有输出。最终 R 获得了处理器并恢复执行；它做的第一件事就是检查 `error`——看到的却是 S 调用的结果，而不是它自己的结果。

这种情况会在某些情况下发生，因此错误将是偶发性的且极难发现。如何避免这个问题呢？ 微软为 `CreateThread()` 提供了一个额外的函数。

# 第二章 使用操作系统

尽管 `CreateThread()` 与运行时库之间存在明显的差异（注：此处原文似乎有逻辑衔接上的漏词，意为*Despite the apparent differences... and...*），由于我们使用运行时库，我们可以使用如下原型：

```
DWORD WINAPI myFunc(LPVOID);
```

这意味着我们可以使用以下调用：

```
CreateThread(NULL, 0, myFunc, &thArg, ...);
```

这种方法很简陋但有效；可以通过合理使用来改进。

## 解决问题

该练习要求你编写一个程序执行以下操作：

- 读取命令行参数 N。
- 从 1 到 N，创建一个新线程来执行工作。
- 在所有线程完成后终止程序。

以下是代码框架：

```
#include <windows.h>
#include <math.h>
#include <stdio.h>
#include <stdlib.h>
static int runFlag = TRUE;
void main(int argc, char *argv[]) {
    unsigned int runTime;
    SYSTEMTIME now;
    WORD stopMinute, stopSecond;
    // 获取命令行参数 N
    // 获取线程应该运行的时间 runTime
    // 计算停止时间（学习更好的方法）
    GetSystemTime(&now);
    printf("thread: Suite starting at system time %d:%d:%d\n", now.wHour, now.wMinute, now.wSecond);
    stopSecond = (now.wSecond + (WORD)runTime) % 60;
    stopMinute = now.wMinute + (now.wSecond + (WORD)runTime) / 60;
    // 从 1 到 N
    for (i = 0; i < N; i++) {
        // 创建新线程执行模拟工作
        Sleep(100); // 让新创建的线程
    }
    // 当子线程工作时循环
    while (runFlag) {
        GetSystemTime(&now);
        if ((now.wMinute >= stopMinute) && (now.wSecond >= stopSecond)) {
            runFlag = FALSE;
        }
        Sleep(1000);
    }
    Sleep(5000);
}
```

# 第二章 • 使用操作系统

测量当前时间，计算线程池应当停止的时间。在创建了执行模拟工作的工作线程后，协调线程会检查当前时间以判断是否到了停止时间；如果不需要停止，协调线程将睡眠 1,000 毫秒（一秒），然后醒来并再次检查时间。当足够的时间过去后，协调线程会将全局标志 `runFlag` 设置为 `FALSE`，等待五秒钟然后终止。在理解这种奇怪的协议之前，请查看工作线程使用的代码骨架：

```cpp
// 由每个工作线程执行的代码（模拟工作）
DWORD WINAPI threadWork(LPVOID threadNo) {
    // 局部变量
    double y;
    const double x = 3.14159;
    const double e = 2.71828;
    int i;
    const int napTime = 1000; // 毫秒
    const int busyTime = 40000;
    DWORD result = 0;
    // 创建负载
    while(runFlag) {
        // 参数化处理器突发阶段
        for(i = 0; i < busyTime; i++)
            y = pow(x, e);
        // 参数化睡眠阶段
        Sleep(napTime);
        // 写消息到 stdout
    }
    // 终止
    return result;
}
```
