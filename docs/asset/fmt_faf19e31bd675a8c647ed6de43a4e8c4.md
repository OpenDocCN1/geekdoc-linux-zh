
CreateProcess 支持的参数（如前一个示例所示）让你对新创建的进程具有相当程度的控制权。这与 `spawn` 函数形成对比，后者没有提供设置进程优先级、安全属性或调试状态的选项。

下一个示例展示了使用 `_spawnlp` 函数对相同代码的移植。

```c
#include <windows.h>
#include <process.h>
#include <stdio.h>

void main()
{
    printf("Running Notepad with spawnlp\n");
    _spawnlp(_P_NOWAIT, "notepad", "notepad", NULL );

    printf("Done.\n");
    exit(0);
}
```

# 第 9 章：Win32 代码转换

运行上述任何一个示例都会产生一个类似于所示的控制台窗口：

![](img/a92ad9df7b0b951660ea67fa842644c1_272_0.png)

### 9.1 spawn 示例代码的输出

## 替换进程映像 (exec)

UNIX 应用程序通过使用 `exec` 函数之一将执行中的映像替换为另一个应用程序的映像。如前所述，`fork` 后接 `exec` 与 `CreateProcess` 相似。

Windows 支持 `exec` 函数的六种 POSIX 变体外另外两个（`exclpe` 和 `execve`）。这些函数签名相同，并作为标准 C 运行时的一部分提供。移植使用 Win32 的 UNIX 代码很容易理解的。以下是一个简单的 UNIX 示例，展示了 `exec` 函数的使用。

> 注意：有关 Win32 上对 `exec` 支持的更多信息，请参阅 Microsoft Visual Studio® 开发系统附带的标准运行时库文档。

### 在 UNIX 中使用 exec 替换进程映像

```c
#include <unistd.h>
#include <stdio.h>

int main()
{
    printf("Running ps with execcl\n");
    execclp("ps", "ps", "-1", 0);
    printf("Done.\n");
    exit(0);
}
```

前面的示例在 Windows 上仅需细微修改即可编译并运行。然而，它需要一个名为 `ps.exe` 的可执行文件（Interix 产品包含其中一个）。

在 Windows Windows 时，`<unistd.h>` 包含文件不是有效的头文件。要在使用 Windows 时使用此示例，你需要将头文件改为 `<process.h>`。这样做允许你编译、链接并运行这个简单的应用程序。

## 等待派生进程

在上一节中，示例展示了如何创建一个异步进程，其中父进程和子进程同时执行。还没有同步机制说明如何修改之前的示例，以包含允许父进程在继续之前等待子进程完成或终止的功能。

为了在 UNIX 中实现这一点，开发者将使用 `wait` 函数之一来挂起父进程，直到子进程终止。在 Windows Windows 时，也提供相同的语义。使用的函数不同，但结果是相同的。

当你查看示例时，请记住这并不是两个平台之间的详尽比较。这里描述了一个非常简单的场景，但如果你需要扩展场景以包含等待多个子进程，则 `spawn` 示例无法充分映射，因为它不包含对该功能的支持。在这种情况下，你需要考虑 `CreateProcess` 方法和 `WaitMultipleObjects`。

如需查看此示例的代码，请参见“附录 9.7：等待派生进程”。

## 进程 vs 线程

在下一个示例中，UNIX 代码正在 `fork` 一个进程，但没有执行独立的运行时映像。这在应用程序内部创建了一个独立的执行路径。在使用 Windows 时，这通过使用线程而不是进程来实现。如果你的 UNIX 应用程序以这种方式创建独立的执行线程，你应该使用 Win32 API `CreateThread`。

UNIX 代码正在 `fork` 一个进程，但没有执行独立的运行时映像。这在应用程序内部创建了一个独立的执行路径。在使用 Windows 时，这通过使用线程而不是进程来实现。如果你的 UNIX 应用程序以这种方式创建独立的执行线程，你应该使用 Win32 API `CreateThread`。

### 使用 fork 的代码

```c
#include <unistd.h>
#include <stdio.h>
#include <sys/types.h>

int main() {
    pid_t pid;
    printf("Running ps with fork and execlp\n");
    pid = fork();
    switch(pid) {
        case -1:
            perror("fork failed");
            exit(1);
        case 0:
            if (execlp("ps", NULL) < 0) {
                perror("execlp failed");
                exit(1);
            }
            break;
        default:
            break;
    }
    printf("Done.\n");
    exit(0);
}
```

## 管理资源限制

开发者经常想要创建不使用所有内存、CPU周期或磁盘空间的进程。在 UNIX 中，`getlimit` 函数检索资源限制，`getrusage` 函数检索使用情况，`setrlimit` 函数设置新限制。常见限制名称和含义见表 9.1。

### 表 9.1 常见限制名称

| 限制 | 描述 |
| --- | --- |
| `RLIMIT_CORE` | 创建的核心文件的最大大小（字节）。如果核心文件大于 `RLIMIT_CORE`，写入将在该处终止。如果限制设置为 0，则不创建核心文件。 |
| `RLIMIT_CPU` | 进程可以使用的 CPU 时间最大值（秒）。如果进程超过此时间，系统将向进程发送 `SIGXCPU`。 |
| `RLIMIT_DATA` | 进程数据段的最大大小（字节）。如果数据段超过此值，函数 `brk`、`malloc` 和 `sbrk` 将失败。 |
| `RLIMIT_FSIZE` | 进程创建的文件最大大小（字节）。如果限制为 0，进程无法创建文件。如果写入或截断超过限制，后续尝试将失败。 |
| `RLIMIT_NOFILE` | 文件描述符的最大值加一。这限制了进程可以分配的文件描述符数量。如果分配了 `RLIMIT_NOFILE` 文件，分配新文件描述符的函数可能会错误 `EMFILE` 失败。 |
| `RLIMIT_STACK` | 进程栈的最大大小（字节）。栈不会自动超过此限制；如果进程尝试超过此限制，系统将向进程发送 `SIGSEGV`。 |
| `RLIMIT_AS` | 进程可用内存的最大大小（字节）。如果超过此限制，内存函数 `brk`、`malloc`、`mmap` 和 `sbr` 将失败，并将 `errno` 设置为 `ENOMEM`，且自动栈增长将如 `RLIMIT_STACK` 所述的那样失败。 |

## Windows 作业对象

Windows 使用作业对象来设置作业限制（而不是进程限制）。类似于 UNIX 的，一旦作业对象填充了目标进程，就可以对整个组进行各种操作，从终止到实施资源限制等。与 UNIX 不同，Windows 作业对象没有文件输入输出（I/O）源限制。如果你的应用程序需要文件 I/O 限制，你需要创建自己的代码来处理此问题。

### 表 9.2 作业对象

| 成员 | 说明 | 注意事项 |
| --- | --- | --- |
| `PerProcessUser-TimeLimit` | 分配每个进程的最大用户模式时间（单位为 100 纳秒）。 | 系统会自动终止任何超过其分配时间的进程。要设置此限制，请在 `Flags` 成员中指定 `JOB_OBJECT_LIMIT_PROCESS_TIME` 标志。 |
| `PerJobUser-TimeLimit` | 指定此作业中的进程可以使用多少用户模式时间（单位为 100 纳秒）。 | 默认情况下，达到此时间限制时，系统会自动终止所有进程。你可以在作业运行时定期更改此值。要设置此限制，请在 `Flags` 成员中指定 `JOB_OBJECT_LIMIT_JOB_TIME` 标志。 |
| `LimitFlags` | 指定应用于作业的限制。 | 更多信息请参阅作业对象 API 参考。 |
| `MinimumWorkingSetSize`/`MaximumWorkingSetSize` | 指定作业内所有进程的最小和最大工作集大小。 | 通常情况下，进程的工作集可以增长到其最大值：`MaximumWorkingSetSize` 强制执行硬限制。一旦进程的工作集达到此限制，进程将进行自我分页交换。单个进程对 `SetProcessWorkingSize` 的调用将被忽略，除非该进程只是试图清空其工作集。要设置此限制，请在 `Flags` 成员中指定 `JOB_OBJECT_LIMIT_WORKINGSET` 标志。 |
| `ActiveProcessLimit` | 指定作业中可以并发运行的最大进程数量。 | 任何超过此限制的尝试都会导致新进程因“配额不足”错误而被终止。要设置此限制，请在 `Flags` 成员中指定 `JOB_OBJECT_LIMIT_ACTIVE_PROCESS` 标志。 |
| `Affinity` | 指定可以运行进程的 CPU 子集。 | 单个进程可以进一步限制此项。要设置此限制，请在 `Flags` 成员中指定 `JOB_OBJECT_LIMIT_AFFINITY` 标志。 |
| `PriorityClass` | 指定所有进程使用的优先级类。 | 如果进程成功调用了 `SetPriorityClass`，即使实际上执行失败，调用也会返回。如果进程调用 `GetPriorityClass`，函数将返回进程已设置优先级类，尽管这可能不是进程的实际优先级类。此外，`SetThreadPriority` 无法将线程提升到普通优先级以上，但可以用于降低优先级。要设置此限制，请在 `Flags` 成员中指定 `JOB_OBJECT_LIMIT_PRIORITY_CLASS` 标志。 |
| `SchedulingClass` | 指定分配给作业中线程的相对时间差。 | 值可以从 0 到 9；5 是默认值。更多信息请参阅此表后的文本。要设置此限制，请在 `Flags` 成员中指定 `JOB_OBJECT_LIMIT_SCHEDULING_CLASS` 标志。 |

正如你在查看 `setrlimit` 和作业对象的表格时可能观察到的，作业对象强制的限制在除一个领域外都是具有可比性的：文件 I/O。

## 使用 Windows 时限制文件 I/O

在 UNIX 中创建进程时，内核空间中的进程控制块 (`PCB`) 包含一个用默认值初始化的限制数组。对于 `RLIMIT_SIZE` 文件，内核中的写入程序会感知 `PCB` 中的限制结构，这些函数会进行检查以执行限制。Windows 操作系统没有对文件实现类似的限制。为了解决这个问题，你必须编写自己的解决方案并将其构建到应用程序中。

本节介绍了一种你可以在应用程序中使用的解决方案。该解决方案模拟了 UNIX 文件资源限制：

- 作为一个静态变量持有的限制数组。这类似于 C 运行时函数使用静态变量的方式。
- UNIX 函数 `getrlimit()` 和 `setrlimit()` 的版本。这些函数操纵限制数组。
- 每个磁盘写入函数的包装器（Wrappers）。这些包装器是具有资源感知的。

该解决方案由三个文件实现。其中两个文件 `resource.h` 和 `resource.c` 实现了 `getrlimit()`、`setrlimit()`、`rwrite()` 和 `_write()` 函数。仅对 `fwrite()` 和 `_write()` 进行了封装，因为它们是 UNIX 世界中最常见的磁盘写入函数。第三个文件是 `rlimit.c`，它是一个简单的测试程序，用于确认在达到限制时 `rfwrite()` 将失败。

欲需更多信息，请参阅“附录 9.2：限制文件 I/O”。

## 进程计数

Win32 API 有几个函数用于收集进程计数信息：

- `GetProcessShutdownParameters`
- `GetProcessTimes`
- `GetProcessWorkingSetClass`
- `SetPriorityClass`
- `SetProcessShutdownParameters`
- `SetProcessWorkingSetSize`

另一种，获取进程信息的更好方法是通过 Windows 管理规范 (`WMI`) API。

关于 WMI 的更多信息，请参阅 `http://msn.microsoft.com/downloads/default.asp?URL=/code/sample.asp?url=msdn-027/001/566/msdncompositedoc.xml`。

## 信号与信号处理

UNIX 操作系统支持广泛的信号。UNIX 信号是捕获或指示不同类型事件的软中断。相反，Windows 只支持一组仅限于异常事件的少量信号。因此，将 UNIX 代码转换为 Win32 需要使用新技术来替代某些 UNIX 信号。

Windows 信号实现限于以下信号（表 9.3）。

### 表 9.3 Windows 信号

| 信号 | 含义 |
| --- | --- |
| `SIGABRT` | 异常终止 |
| `SIGFPE` | 浮点错误 |
| `SIGILL` | 非法指令 |
| `SIGINT` | 终端中断 |
| `SIGSEGV` | 无效引用 |
| `SIGTERM` | 终止 |
| `SIGTSTP` | 终端停止 |
| `SIGTTIN` | 从 tty 读取 |
| `SIGTTO` | 写入 tty |
| `SIGUSR1` | 用户定义信号 |
| `SIGUSR2` | 用户定义信号 |

## 254 UNIX 应用程序指南

正如你在查看 `setrlimit` 和作业对象的表格时可能观察到的，作业对象强制的限制在除一个领域外都是具有可比性的：文件 I/O。

## 使用 Windows 时限制文件 I/O

在 UNIX 中创建进程时，内核空间中的进程控制块 (`PCB`) 包含一个用默认值初始化的限制数组。对于 `RLIMIT_SIZE` 文件，内核中的写入程序会感知 `PCB` 中的限制结构，这些函数会进行检查以执行限制。Windows 操作系统没有对文件实现类似的限制。为了解决这个问题，你必须编写自己的解决方案并将其构建到应用程序中。

本节介绍了一种你可以在应用程序中使用的解决方案。该解决方案模拟了 UNIX 文件资源限制：

- 静态变量持有的限制数组。这类似于 C 运行时函数使用静态变量的方式。
- UNIX 函数 `getrlimit()` 和 `setrlimit()` 的版本。这些函数操纵限制数组。
- 每个磁盘写入函数的包装器。这些包装器是具有资源感知的。

该解决方案由三个文件实现。其中两个文件 `resource.h` 和 `resource.c` 实现了 `getrlimit()`、`setrlimit()`、`rwrite()` 和 `_write()` 函数。仅对 `fwrite()` 和 `_write()` 进行了封装，因为它们是 UNIX 世界中最常见的磁盘写入函数。第三个文件是 `rlimit.c`，它是一个简单的测试程序，用于确认在达到限制时 `rfwrite()` 将失败。

欲需更多信息，请参阅“附录 9.2：限制文件 I/O”。
