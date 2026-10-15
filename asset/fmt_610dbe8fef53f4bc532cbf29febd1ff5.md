
```c
#include <windows.h>
#include <stdio.h>
#define BUFFER_LEN ... // 读取/写入的字节数
/* 缓冲区 */

int main(int argc, char *argv[]) {
    // 本地变量
    char buffer[BUFFER_LEN+1];
    // CreateFile 参数
    DWORD dwShareMode = 0; // 共享模式
    LPSECURITY_ATTRIBUTES lpFileSecurityAttributes = NULL; // 指向属性的指针
    HANDLE hTemplateFile = NULL; // 要复制的文件句柄
    // ReadFile 参数
    HANDLE sourceFile; // 源
    DWORD numberOfBytesRead; // 读取的字节数
    OVERLAPPED overlapped = NULL; // 此处未使用
    // WriteFile 参数
    HANDLE sinkFile; // 源
    DWORD numberOfBytesWritten; // 写入的字节数
    // 打开源文件
    sourceFile = CreateFile (
        "in_test",
        GENERIC_READ,
        dwShareMode,
        lpFileSecurityAttributes,
        OPEN_ALWAYS,
        FILE_ATTRIBUTE_READONLY,
        hTemplateFile
    );
    if (sourceFile == INVALID_HANDLE_VALUE) {
        fprintf(stderr, "文件打开失败\n");
        ExitProcess(1);
    }
    // 打开目标文件
    sinkFile = CreateFile (
        "out_test",
        GENERIC_WRITE,
        dwShareMode,
        lpFileSecurityAttributes,
        CREATE_ALWAYS,
        FILE_ATTRIBUTE_NORMAL,
        hTemplateFile
    );
    if (sinkFile == INVALID_HANDLE_VALUE) {
        fprintf(stderr, "文件打开失败\n");
        ExitProcess(1);
    }
    // 复制文件的主循环
    while (
        // ReadFile(
        sourceFile, buffer,
        BUFFER_LEN, &numberOfBytesRead,
        &overlapped
    ) > 0) {
        // WriteFile(
        sinkFile, buffer,
        numberOfBytesRead, &numberOfBytesWritten,
        &overlapped);
    }
    CloseHandle(sourceFile);
    CloseHandle(sinkFile);
    return 0;
}
```

```c
)
if (lpoverlapped && numberOfBytesRead > 0)
{
    WriteFile(sinkFile, buffer, BUFFER_LEN,
               &numberOfBytesWritten, lpoverlapped);
}
// 终止。关闭目标和源文件
CloseHandle(sourceFile);
CloseHandle(sinkFile);
ExitProcess(0);
```

### 使用其他资源

资源是指任何抽象机器组件（包括文件），进程在执行程序之前必须显式分配的这种组件。如果进程/线程请求了不可用的资源，线程通常会继续执行，并保持挂起，直到资源变得可用。

每个操作系统除了文件外，还提供了许多资源的访问权限，包括处理器、内存、键盘和显示器。如果所有资源的接口都是相同的，那么程序员就很容易知道如何使用所有这些资源；如果接口根据资源类型而不同，这就会变得困难。

在 UNIX 中，文件抽象被用于管道和设备。设备（如键盘和显示器）在第 5 章中详细描述。现在，只需说设备在驱动程序中实现了对应的 `open()`、`close()`、`read()`、`write()`、`seek()` 和 `fcntl()` 命令，即可对应文件接口。`read()` 和 `write()` 操作看起来就像文件 `read()` 操作。管道是一种抽象资源，用于允许两个不同的进程相互进行通信。它们在第 9 章中描述。

### 2.3 进程与线程

计算是一个进程、至少一个（隐式或显式）线程以及一组资源的组合。进程组件由以下部分组成（见图 2.2）：

- 一个一个待执行的二进制程序（或对象代码）。
- 进程将要在其执行的数据（通过从文件获取或通过进程进程的交互方式获取）。
- 执行所需的资源，包括包含运行进程将处理的数据的文件。

请注意，进程是一个抽象机器框架，计算可以在该框架内发生，而执行的活动元素由**执行引擎**提供。在图 2.2 所示的单线程计算中，进程中只有一个执行引擎。在传统上，操作系统（如经典的 Unix 系统）只允许每个进程中有一个执行引擎，因此我们把这种进程/线程组合称为经典进程。在 Windows 等现代操作系统中，进程组件能够像图 2.6 所示包含多个执行引擎。每个执行引擎组件被称为线程（或轻量级进程），我们称这种方法为现代进程和线程方法。无论哪种情况，线程由以下部分组成：

- 线程私有的数据。这些数据通常分配在线程特定的栈上。每个线程可能还有自己的私有数据工作空间。
- 线程状态，这是一个持有所有线程特有的 OS 数据结构。例如，状态包括线程将执行的下一条指令的地址、关于线程是否阻塞等待资源的数据、如果线程被阻塞则关于它正在等待哪种资源的信息等。

图 2.6 表示一个多线程计算，其中 3 个不同的线程在一个进程内执行。这三个线程使用相同的程序、全局进程数据、文件和其他资源，但它们每个都有自己的本地数据和状态。

## 图 2.6 带有多个线程的进程

进程为线程定义了一个执行环境。该环境提供了一个通用的二进制程序、数据和资源（包括文件）。每个线程使用它自己的栈和状态执行程序，因此不同的线程通常在并发地执行二进制程序的不同部分。

线程（执行引擎）

![](img/65fa32f8b1eb09c8c688a77a880941bf_90_0.png)

# 第二章 使用操作系统

尽管多线程计算模型是一个明显的趋势，但某些操作系统仍然仅支持经典进程模型。在这些情况下，没有单独的线程——执行引擎是进程的内置部分。尽管经典进程听起来像是一个古老的概念，但值得注意的是，Linux 2.0 版本曾使用过它（2.2 版本提供了对线程的内核级支持）。即使 UNIX 系统提供了内核线程支持，它仍然在传统的系统调用接口下导出经典进程模型，并在带有 POSIX 线程扩展的接口下导出线程模型。

经典进程模型使用了超过四分之一的世纪，直到 20 世纪 90 年代后期它才开始被现代模型所取代。将经典进程演进为新的进程和线程模型的动机是创建一个简单的 OS 抽象，在该抽象中可以有多个入口使用相同的文件和设备执行相同的程序。在 20 世纪 90 年代，程序员们开始想要能够共享设施的、不同的计算单元（例如，请参见 [Bershad, et al., 1988; Hauser, et al., 1993]）。线程的一个常见动机示例是管理共享文件系统的服务器，但它需要一个独立的线程来服务每个使用该服务器的客户端。另一个示例是使用线程范式在物理终端背景下管理终端会话的窗口系统。假设一个窗口系统是使用物理屏幕管理器构建的，带有几个虚拟屏幕线程（见图 2.7）。所有线程运行相同的代码，并且都共享物理屏幕，但每个线程只管理窗口集合中的一个窗口。

## 图 2.7 使用线程

进程提供了一个处理窗口操作的程序。进程提供了一个处理窗口操作程序，例如窗口及其大小。每个线程使用它自己的栈和状态执行程序，因此不同的线程通常在并发地执行二进制程序的不同部分。

线程（执行引擎）

![](img/65fa32f8b1eb09c8c688a77a880941bf_90_0.png)

*(注：由于原文中存在大量文本重复，翻译时已根据要求进行了去重处理)*

# 第二章 使用操作系统

`count` 是一个共享变量，被所有进程使用。在任何时刻，只有一个进程可以执行 `JOIN()` 语句。一旦某个进程开始执行 `JOIN()` 系统调用，在执行该进程完成之前，其他进程无法获得处理器的控制权。
