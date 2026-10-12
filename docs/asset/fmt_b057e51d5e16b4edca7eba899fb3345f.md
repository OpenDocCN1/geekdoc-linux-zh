
前两个参数是应用程序名称及其命令行。两者都是以空结尾的字符串。`lpApplicationName` 是要执行的文件名。这可以包含完整路径，包括驱动器号。如果不存在 `.exe` 扩展名，会自动添加。如果给出的文件名没有路径信息，将按照以下顺序在几个不同位置搜索该文件：

- 当前运行的可执行文件所在的目录
- 父进程的当前目录
- 32 位 Windows 系统目录（通过调用 `GetSystemDirectory()` 获取），位于 windows 目录下的 `SYSTEM32`
- 16 位 Windows 系统目录（没有 Win32 调用可以返回此目录），位于 windows 目录下的 `SYSTEM`
- Windows 目录（通过调用 `GetWindowsDirectory()` 获取）
- `PATH` 环境变量中列出的目录

`lpApplicationName` 可以为 `null`，在这种情况下，使用 `lpCommandLine` 中第一个空格分隔的标记作为可执行文件名。通常，`lpApplicationName` 用于完整路径，`lpCommandLine` 用于传递给可执行程序的参数列表。子进程可以使用 `GetCommandLine()` 获取其命令行，或使用 C 运行库的 `argc/argv` 对。

第三个参数 `lpProcessAttributes` 是一个指向 `SECURITY_ATTRIBUTES` 结构的指针。在其他创建或打开对象的 Win32 调用中，安全结构包含一个 `bInheritHandle` 成员，指示句柄结果是否可以被子进程继承。它还包含安全描述符，其中包含访问控制列表（ACL），用于决定其他进程是否可以访问此对象。对于进程，访问控制列表中的条目允许或拒绝特定用户通过后文描述的 `OpenProcess()` Win32 调用访问你的进程。通常，安全描述符可以留空 `null`，此时子进程将拥有与父进程相同的描述符。

第四个参数 `lpThreadAttributes` 也是一个指向 `SECURITY_ATTRIBUTES` 结构的指针，但这一个用于子进程的主线程。`bInheritHandles` 指示父进程中的可继承句柄是否可以被子进程继承。当设置为 `true` 时，所有你希望子进程创建或打开的对象，其对象的 `bInheritHandle` 标志也将被设置为 `true`。

`dwCreationFlags` 是一个位图，结合了表 3.7 中列出的一个或多个属性。

### 表 3.7 进程创建标志

| 值 | 含义 |
| --- | --- |
| `CREATE_DEFAULT_ERROR_MODE` | 子进程不继承父进程的错误模式，而是由 `CreateProcess()` 赋予新的默认错误模式。 |
| `CREATE_NEW_CONSOLE` | 子进程获得一个新的控制台而不是继承父进程的控制台。此标志不能与 `DETACHED_PROCESS` 标志配合使用。 |
| `CREATE_NEW_PROCESS_GROUP` | 子进程是一个进程组的根。`GenerateConsoleEvent` 函数用于向组发送 `CTRL+C` 或 `CTRL-BREAK` 信号。 |
| `CREATE_SEPARATE_CWD` | 用于启动 16 位 Windows 应用程序。 |
| `CREATE_SUSPENDED` | 子进程的主线程挂起，直到调用 `ResumeThread()`。 |
| `CREATE_UNICODE_ENVIRONMENT` | 如果设置，指向的环境块使用 Unicode 字符。如果没有设置，环境块使用 ANSI 字符。 |
| `DEBUG_PROCESS` | 如果设置，父进程被视为调试器，NT 会通知调试器发生的所有调试事件。 |
| `DEBUG_ONLY_THIS_PROCESS` | 如果未设置且父进程不是被调试进程，则不会发生调试操作。 |
| `DETACHED_PROCESS` | 对于控制台应用程序，新进程无法访问父进程的控制台。新进程可以在需要时稍后调用 `AllocConsole()` 创建一个新的控制台。 |
| `HIGH_PRIORITY_CLASS` | 子进程执行关键任务。该优先级类使用几乎所有的 CPU 时间片。 |
| `IDLE_PRIORITY_CLASS` | 最低优先级。子进程仅在系统空闲时运行。 |
| `NORMAL_PRIORITY_CLASS` | 正常进程调度。 |
| `REALTIME_PRIORITY_CLASS` | 最高优先级。抢占所有其他优先级类的线程，包括许多操作系统进程。 |

`lpEnvironment` 是指向一组环境变量的指针。每个环境变量都是以空结尾的字符串，格式为 `var_name=value`。变量块本身也以空结尾——即最后一对有两个空终止符。如果此参数为 `null`，子进程将使用父进程的环境设置。

`lpCurrentDirectory` 是包含子进程当前目录设置的空结尾字符串。该字符串必须包含包含驱动器号的完整路径。如果此参数为 `null`，则使用父进程的当前目录。

`lpStartupInfo` 是指向 `STARTUPINFO` 结构的指针，该结构指定了子进程具有许多外观属性。这主要用于 Windows GUI 应用程序以及控制台的位置、大小和标题。调用 `GetStartupInfo()` 会将 `STARTUPINFO` 结构设置为调用进程的设置。这可以原样使用，也可以进行修改以满足子进程的需求。

## 创建 NT 进程

`lpProcessInformation` 是一个指向 `PROCESS_INFORMATION` 结构的指针，该结构在 `CreateProcess()` 返回之前由 NT 填充。该结构所示所示。

```c
typedef struct _PROCESS_INFORMATION
{
    HANDLE hProcess;
    HANDLE hThread;
    DWORD dwProcessId;
    DWORD dwThreadId;
} PROCESS_INFORMATION;
```

前两个成员是子进程及其主线程的句柄。所有 Win32 函数都使用句柄来操作对象。ID 成员用于唯一标识进程及其线程，但不能用于直接操作它们。如果你需要给另一个进程提供一个标识值，但又想防止其调用具有破坏性的函数（例如 `TerminateThread()` 或 `TerminateProcess()`），则可以使用这些 ID。

任何进程在退出时都会调用 `ExitProcess`。这是退出进程的优选方法，因为它可以实现进程及其所有线程的整洁关机。

```c
VOID ExitProcess (UINT uExitCode);
```

`uExitCode` 是该进程及其所有拥有线程的退出代码。`uExitCode` 中的值通过调用 `GetExitCodeProcess()` 获取。

```c
BOOL GetExitCode(HANDLE hProcess,
    LWORD lpExitCode);
```

`TerminateProcess()` 会强制终止进程及其所有线程，应谨慎使用，因为它不允许进程或线程在结束前清理所有已分配的资源。

```c
BOOL TerminateProcess (HANDLE hProcess,
    UINT uExitCode);
```

`GetStartupInfo()` 将调用进程的 `STARTUPINFO` 结构拷贝到目标结构中。

```c
VOID GetStartupInfo (LPSTARTUPINFO lpStartupInfo);
```

`OpenProcess()` 用于根据给定的进程 ID 打开一个现有进程。

```c
HANDLE OpenProcess (DWORD dwDesiredAccess,
    BOOL bInheritHandle,
    DWORD dwProcessId);
```
