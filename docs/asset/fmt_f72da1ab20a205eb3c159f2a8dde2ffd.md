
// 为命令行列出的每个生产者创建一个线程信息对象和一个线程

for (int count = 1; count < argc; count += 2)

{

    consumerThreadInfo[iConsumerThreadCount] =

        new XPCThreadInfo(argv[count], argv[count+1], &threadSem, &mainSem);

    consumerThread[iConsumerThreadCount] =

        new XPCThread(ConsumerThreadProc, (void*)consumerThreadInfo[iConsumerThreadCount]);

    XPCThread waitThread(WaitForConsumerThreadProc, consumerThread[iConsumerThreadCount]);

    // 活跃线程计数

    iConsumerThreadCount++;

}

while (1)

{

    // 等待某个线程从生产者读取了数据

    mainSem.vLockWait();

    // 处理该线程的数据

    std::cout << "接收消息: " << globalMsg.sMessage() << std::endl;

    std::cout << "消息队列: " << globalMsg.sFileName() << std::endl;

}

return 0;

}

```cpp
if (strcmp(globalMsg.sMessage(), "QUIT") == 0)

{

    int iThreadCount = 0;

    // 首先找到正确的线程

    for (int count = 1; count < argc; count += 2)

    {

        // 如果文件名匹配，则我们找到了

        // 正确的线程

        if (strcmp(globalMsg.sFilename(), argv[count]) == 0)

        {

            cout << "Kill thread: " << iThreadCount << endl;

            // 发送杀死线程的事件

            consumerThreadInfo[iThreadCount].vEvent().SendEvent();

            break;

            iThreadCount++;

        }

    }

    // 解锁保护全局变量

    // （由线程锁定）的信号量

    threadSem.vUnlock();

}

return 0;
```

线程允许进程同时执行多项任务。与进程相比，线程的启动和终止速度更快。它们还与其父线程共享资源。这些特性使得线程非常解决各种编程问题，特别是当需要阻塞系统调用并继续处理时。通过创建一个线程并在线程中调用阻塞函数，主线程可以继续处理。需要信号量和事件来保护共享资源。这里介绍的 `XPThread` 类将 NT Win32 线程功能封装在一个简洁、易于使用的对象中。

## 3.6 创建 NT 进程

NT 为每个进程提供了完成工作所需的所有资源。这些资源包括线程、带有数据和栈的地址空间、可执行代码、环境变量、调度优先级和对象句柄等。进程启动时带有一个主线程，并根据需要创建额外的线程。进程可以创建额外的进程。这些生成的进程被称为子进程，调用它的进程被称为父进程。子进程在创建时会获得它自己的一组资源——主线程、地址空间等。子进程独立于其父进程运行，并在父进程死亡后仍可以继续运行。

子进程可以继承父进程创建的部分（但不是全部）NT 对象。可继承对象的列表包括以下内容：

- 由 `CreateFile()` 返回的句柄，包括文件、命名管道、串行通信设备和邮件槽的句柄
- 进程、线程、互斥锁和信号量的打开句柄
- 环境变量
- 当前目录

控制台及其 I/O 缓冲区，除非进程已分离或创建了新的控制台。创建对象时，必须将可继承属性设置为 `true`，并且在使用该属性创建进程时，该属性是可以继承的（参见 `CreateProcess`）。子进程通过与父进程相同的句柄来引用被继承的对象。NT 没有提供从父进程向子进程传递数值的机制——这两个进程必须通过命令行、环境变量内部或其他进程间通信手段来实现这一点。

## 编程 NT 进程

用于创建进程的 Win32 系统调用是 `CreateProcess()`，此处列出如下：

```cpp
BOOL CreateProcess(LPSTR lpApplicationName,

                LPTSTR lpCommandLine,

                LPSECURITY_ATTRIBUTES lpProcessAttributes,

                LPSECURITY_ATTRIBUTES lpThreadAttributes,

                BOOL bInheritHandle,

                DWORD dwCreationFlags,

                LPVOID lpEnvironment,

                LPTSTR lpCurrentDirectory,

                LPSTARTUPINFO lpStartupInfo,

                LPPROCESS_INFORMATION lpProcessInformation);
```
