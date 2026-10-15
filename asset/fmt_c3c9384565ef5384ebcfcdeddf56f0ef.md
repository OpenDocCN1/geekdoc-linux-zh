
`ZeroMemory(&startup_info, sizeof(startup_info));`

`startup_info.cb = sizeof(startup_info);`

// 启动子进程

`CreateProcess(NULL, memory, 0, 0, true, 0, 0, &startup_info, &process_info);`

`WaitForSingleObject(process_info.hProcess, INFINITE);`

`UnmapViewOfFile(memory);`

`CloseHandle(filehandle);`

}
else
{
`handle = (HANDLE)wtoi(argv[1]);` // 从 `argv[1]` 获取句柄
`memory = (wchar_t*)MapViewOfFile(handle, FILE_MAP_ALL_ACCESS, 0, 0, 0);`
`printf("Second process memory: %S %i\n", memory, handle);`
`UnmapViewOfFile(memory);`
`CloseHandle(handle);`
}

`getchar();`
`return 0;`
```

第一个更改是在创建映射对象时使用了 `SECURITY_ATTRIBUTES`。这些安全属性的 `bInheritHandle` 属性被设置为 `true`，这将允许映射被任何子进程继承。
用于创建子进程的命令行由进程进程名（即 `argv[0]`）和映射对象的句柄组成。
创建子进程的最后一个更改是 `CreateProcess()` 调用传递了 `true` 参数，这决定了子进程是否应该继承父进程的句柄。
子进程的代码与之前的代码相似，不同在于是从命令行 `argv[1]` 中提取映射句柄。

# 命名互斥量并在进程间共享

在进程之间共享互斥量的最简单方法是在创建互斥量时命名。其他进程可以使用 `OpenMutex()` 或 `CreateMutex()` 函数获取互斥量句柄。这涉及到几个复杂性：

- 只有一个进程可以创建互斥量。其他进程只能打开现有的互斥量。
- 互斥量的名称必须是唯一的。如果存在同名对象，互斥量将创建失败。
- 互斥量的名称需要传递给其他进程。

这些问题都可以解决，如列表 29 所示。

## # 列表 6.29 进程间共享互斥量

```cpp
#include <Windows.h>
int _tmain(int argc, TCHAR* argv[])
{
    HANDLE sharedmutex;
    STARTUPINFO startup_info;
    PROCESS_INFORMATION process_info;
    ZeroMemory(&startup_info, sizeof(startup_info));
    ZeroMemory(&process_info, sizeof(process_info));
    startup_info.cb = sizeof(startup_info);
    sharedmutex = CreateMutex(NULL, FALSE, L"MyMutex");
    if (sharedmutex == NULL)
    {
        printf("Error creating mutex: %d\n", GetLastError());
        return 1;
    }
    if (argc==1)
    {
        // 父进程
        printf("First process creating child...\n");
        if (!CreateProcessW(argv[0], NULL, 0, 0, FALSE, 0, NULL, NULL, &startup_info, &process_info))
        {
            printf("Error creating process: %d\n", GetLastError());
        }
        else
        {
            // 等待子进程完成工作...
        }
    }
    else
    {
        // 子进程
        HANDLE handle = (HANDLE)wtoi(argv[1]);
        wchar_t* memory = (wchar_t*)MapViewOfFile(handle, FILE_MAP_ALL_ACCESS, 0, 0, 0);
        printf("Second process memory: %S %i\n", memory, handle);
        UnmapViewOfFile(memory);
        CloseHandle(handle);
    }
    CloseHandle(sharedmutex);
    getchar();
    return 0;
}
```

# 第6 章 Windows 线程

## 表 6.7 传递给 CreateNamedPipe() 的参数

| 参数类型 | 注释 |
|---|---|
| `LPCWSTR` | 管道的名称。格式需要为 `\\.\pipe\name`，其中 `name` 替换为所希望管道名称。本地机器上的管道使用 `\\.\` 指定。管道的下一部分是 'pipe' 声明，随后是所选管道的实际名称。 |
| `DWORD` | 管道的访问模式。此标志的典型值为读取或写入；`PIPE_ACCESS_DUPLEX`（创建一个可读的管道）、`PIPE_ACCESS_INBOUND`（创建一个只能读取的管道）、或 `PIPE_ACCESS_OUTBOUND`（创建一个只能写入的管道）；`PIPE_ACCESS_OUTBOUND` 和 `PIPE_ACCESS_INBOUND` 需要作为管道使用以建立连接。 |
| `DWORD` | 管道运行模式。它们可以允许管道携带数据流或消息流。 |
| `DWORD` | 允许管道的实例数。值 `PIPE_UNLIMITED_INSTANCES` 表示最大实例数受系统资源限制。 |
| `DWORD` | 输出缓冲区的大小。输入缓冲区的大小。 |
| `DWORD` | 读取或写入的超时时间。值为0时使用默认的50ms超时时间。 |
| `SECURITY_ATTRIBUTES` | 可选指向安全属性的指针，如果管道句柄应被子进程继承，可以设置该属性。 |

一旦创建了管道，可以使用 `WriteFile()` 调用通过管道发送数据，并使用 `ReadFile()` 调用从管道读取数据。这两个调用使用的参数相似，如表 6.8 所示。

## 表 6.8 传递给 ReadFile() 和 WriteFile() 的参数

| 参数类型 | 注释 |
|---|---|
| `HANDLE` | 管道的句柄 |
| `LPVOID` | 如果调用 `ReadFile()`，则是存储数据的缓冲区地址；如果调用 `WriteFile()`，则是发送数据的地址。 |
| `DWORD` | `ReadFile()` 的缓冲区大小，或 `WriteFile()` 要发送的数据量。 |
| `LPDWORD` | 指向变量的指针，记录读取的数据量或写入的数据量。 |
| `LOVERAPPED` | 指向 `OVERLAPPED` 结构的指针，这将允许函数调用立即返回，并稍后完成读取或写入的处理。 |

一旦应用程序完成对管道的使用，必须调用 `CloseHandle()` 关闭管道。

## 列表 6.30 使用匿名管道在两个线程间通信

```c
#include <windows.h>
#include <process.h>
HANDLE readpipe,writepipe;
unsigned int _stdcall stage1(void * param)
{
    char buffer[200];
    DWORD length;
    for (int i=0; i<10; i++) {
        printf(buffer, "Text %i", i);
        WriteFile(writepipe, buffer, strlen(buffer)+1, &length, 0 );
    }
    CloseHandle(writepipe);
    return 0;
}
unsigned int _stdcall stage2(void * param)
{
    char buffer[200];
    DWORD length;
    while ( ReadFile(readpipe, buffer, 200, &length, 0 )) {
