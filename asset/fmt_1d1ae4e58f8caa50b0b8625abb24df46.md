
```cpp
#include <iostream.h>
#include <string.h>
#include <fstream.h>
#include <iostream.h>
#include "FileStat.h"
#include "Semaphore.h"

main (int argc, char* argv[])
{
    // 用于存储来自文件消息的缓冲区
    char sMessage[512];

    // 生产者-消费者模型在第 2 章介绍的是使用信号量控制共享对象的示例。
    // 生产者-消费者模型在第 2 章介绍的是使用信号量控制共享对象的示例。
    
    FileStat *checkConsumerFile;

    // 检查参数数量
    if (argc < 3)
    {
        cerr << "USAGE: <semaphore name> <pathname>" << endl;
        return 0;
    }

    // 打开命名信号量
    try
    {
        XPCSemaphore consumerSemaphore(argv[1], 0, );

        // 无限循环
        while (1)
        {
            // 等待锁
            consumerSemaphore.vWait();

            // 我们已经获取了锁，创建一个
            // FileStat 来检查文件是否存在
            try
            {
                checkConsumerFile = new FileStat(argv[2]);
            }
            catch (XPCException &ex)
            {
                cerr << ex.getException() << endl;
                return 0;
            }

            if (!checkConsumerFile->nCheckRead() ||
                !checkConsumerFile->nCheckWrite())
            {
                cerr << "Access to file is not allowed" << endl;
                consumerSemaphore.vUnlock();
                return 0;
            }

            // 如果信号量大小为0
            if (checkConsumerFile->Size() == 0)
            {
                cerr << "The producer/consumer file contains no data." << endl;
                cerr << "Restarting loop." << endl;
                delete checkConsumerFile;

                // 释放信号量让生产者有机会
                consumerSemaphore.vUnlock();
                Sleep(1);
                continue;
            }
            // 打开文件读取消息
            ifstream producerConsumerFile(argv[2]);
            producerConsumerFile >> sMessage;
            producerConsumerFile.close();

            // 释放信号量，打印消息
            consumerSemaphore.vUnlock();
            cout << "Received: " << sMessage << endl;
            if (strcmp(sMessage, "QUIT") == 0)
            {
                consumerSemaphore.vUnlock();
                return 0;
            }

            // 让生产者获取锁
            Sleep(1);

        }
    }
    catch (XPCException &ex)
    {
      cout << ex.getException() << endl;
      return 0;
    }
}
```

信号量提供了控制进程间共享资源的方法。`XPCSemaphore` 类封装了 Win32 信号量功能，包含了操作信号量所需的方法。

### 3.5 NT 线程

进程启动时有一个主线程——主线程——并根据需要创建额外的线程。所有线程共享地址空间和其他资源。每个线程维护自己的优先级和一组 NT 用于保存该线程上下文的结构。

NT 是一个抢占式多任务操作系统。这允许同时执行多个进程的线程。在具有多个处理器的计算机上，NT 可以同时执行与处理器数量相同的线程。线程共享资源有缺点。这些缺点是当一个线程在读写同一个资源时意外产生的错误。如果一个线程独立运行两个线程，该错误可能在程序运行数百小时后才会出现。这类错误被称为竞态条件。列出的 `XPCSsemaphore` 和 `XPCevent` 类可用于同步线程，以防止竞态条件的发生。如果使用不当，信号量和事件可能会产生其他编程错误，如死锁。当两个线程都锁定了共享资源时，就会发生死锁。由于另一个线程锁定了资源（可能是错误的），哪个线程都无法访问资源。

线程通过 Win32 调用 `CreateThread()` 创建，并在该线程调用 `ExitThread()` 时终止。线程也可以被另一个线程通过 `TerminateThread()` 终止。`TerminateThread()` 不允许线程清理其在退出之前释放的资源，因此不建议使用它。线程可以设置许多属性，包括其执行优先级、运行的处理器以及栈大小。

创建线程的调用函数 `CreateThread()` 已经有了原型。它会创建一个线程并返回其句柄（`handle`）。该句柄用于其他 Win32 调用以操作该线程。如果调用失败，句柄将为空，调用 `GetLastError()` 将返回扩展的错误信息。

```
HANDLE CreateThread(LPSECURITY_ATTRIBUTES lp,
               DWORD dwStackSize,
               LPTHREAD_START_ROUTINE lpStartAddress,
               LPVOID lpParameter,
               DWORD dwCreationFlags,
               LWORD *lpThreadId);
```

第一个参数是安全属性结构，包含安全描述符和磁盘权限访问控制列表（`ACL`）。这些结构控制了哪些进程可以访问该线程（更准确地说，是进程的所有者可以访问该线程），以及该线程是否可以被其可能创建的子进程继承。如果不使用这些功能，可以将此参数设为空。

第二个参数是栈的初始大小。如果需要，NT 会增加栈的大小，但必须指定初始大小。如果指定为零，则使用调用线程的栈大小。

`lpStartAddress` 是线程开始时将调用的函数地址。`lpParameter` 是传递给线程函数的参数。如果你的应用程序需要向线程传递多个参数，它可以作为指向结构体的指针。

`dwCreationFlags` 有两个属性——`CREATE_SUSPENDED` 或零。如果使用 `CREATE_SUSPENDED`，你的线程将被创建但不会立即执行。稍后调用 `ResumeThread()` 将调度你的线程执行。这在线程运行之前对其进行初始化非常有用。值为零将立即调度该线程执行。`lpThreadID` 是一个指向双字的指针，将其中返回线程的唯一标识符。`threadID` 来自于句柄，它用于标识线程，但不能用于操作线程。如果另一个线程或进程需要标识该线程，但不需要调用任何可能破坏线程的函数（例如 `TerminateThread()`），请使用 `threadID`。

执行线程的函数在此处所示。

```
DWORD WINAPI ThreadFunc(LPVOID lpData);
```

`lpData` 的值与传入 `CreateThread()` 的 `lpParameter` 相同。使用这些参数向 `ThreadFunc()` 传递单个参数或结构体。
