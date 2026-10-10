
```cpp
const char* GetName(const int which);

int GetPID(const int which);

protected:

    std::vector<Process> m_processList;

};

#endif
```

该类的大部分实现的是所有平台共享的代码。进程名称和 ID 列表存储在标准模板库（STL）`vector` 中，它具有良好的移植性。`GetCount()`、`GetName()` 和 `GetPID()` 等函数与此 `vector` 交互并仅依赖于它，因此自然实现在基类中。

## 平台特定的 ProcessesImpl 类

另一方面，`Scan()` 函数是平台特定的，必须在派生类中实现。在 Windows 上，该该类是 `WindowsProcessesImpl`：

```cpp
#if defined(__WINDSPROCESSESIMPL_H_)

#define _WINDSPROCESSESIMPL_H__

#include "../processesimpl.h"

#include <windows.h>

#include <stdio.h>

#include <tchar.h>

#include "psapi.h"

class WindowsProcessesImpl : public ProcessesImpl {

public:

    WindowsProcessesImpl();

    virtual ~WindowsProcessesImpl();

    virtual int Scan();

private:

    void ScanProcesses();

    void PrintProcessNameAndID(DWORD processID);

#endif
```

## 项目2：来自通用代码库的代码 33

包含了 Windows 特有的头文件（例如 `windows.h`）。由于这段代码只在 Windows 上编译，因此在此头文件中包含它或任何其他平台特定的代码是可以的。`Scan()` 函数使用了两个辅助函数，这两个函数是 `WindowsProcessesImpl::ScanProcesses()` 和 `PrintProcessNameAndID()` 的私有。只要 `Scan()` 根据基类的要求声明，任何实现都可以。以下代码展示了 `WindowsProcessesImpl` 实现的大部分。

```cpp
#include "windowsprocessesimpl.h"

int WindowsProcessesImpl::Scan()
{
    m_processList.clear();
    ScanProcesses();
    return m_processList.size();
}
```

```cpp
void WindowsProcessesImpl::PrintProcessNameAndID(
    DWORD processID)
{
    TCHAR szProcessName[MAX_PATH] =
        TEXT("unknown");
    // 获取进程句柄。
    HANDLE hProcess = OpenProcess(
        PROCESS_QUERY_INFORMATION | PROCESS_VM_READ,
        FALSE, processID);
    // 获取进程名。
    if (NULL != hProcess)
{
    if ( EnumProcessModules( hProcess, hMod,
        sizeof(hMod), &cbNeeded ))
    {
        GetModuleBaseName(hProcess, hMod,
        szProcessName,
        sizeof(szProcessName)/sizeof(TCHAR));
    }
    // 打印进程名称和标识符。
```

```cpp
Process proc;
proc.SetPID(processID);
proc.SetName(szProcessName);
m_processList.push_back(proc);
```

```cpp
CloseHandle( hProcess );
```

```cpp
void WindowsProcessesImpl::ScanProcesses()
{
    // 获取进程标识列表。
    DWORD aProcesses[1024], cbNeeded, cProcesses;
    unsigned int i;
    if (!EnumProcesses(aProcesses, sizeof(aProcesses),
        &cbNeeded)
        return;
    // 计算返回了多少个进程标识。
    cProcesses = cbNeeded / sizeof(DWORD);
    // 打印每个
    // 进程的名称和进程标识。
    for (int i = 0; i < cProcesses; i++) {
        if (aProcesses[i] != 0)
            PrintProcessNameAndID( aProcesses[i]);
    }
}
```

# 34 第1章 策略与管理

## 项目2：来自通用代码库的代码

粗体的代码是我写的；其余部分是微软在 http://msdn.microsoft.com 使用 Win32 API 生成的示例代码。我的代码只需要提供 `Scan()` 接口的实现。（由于 `Scan()` 在基类中是纯虚函数，因此这是强制要求的。）并且，每个被扫描到的进程都需要推入基类维护的 `vector` 的末尾。仅仅此而已。

如果你看 Linux 和 Darwin 的实现，你会发现它们遵循相同的方法。这里是 Linux 实现，它使用 `proc` 文件系统来获取信息。首先是头文件：

```cpp
#if defined(__LINUXESIMPL_H__)

#define __LINUXESIMPL_H__

#include "processesimpl.h"

#include <dirent.h>

class LinuxProcessesImpl : public ProcessesImpl {

public:

    LinuxProcessesImpl();

    virtual ~LinuxProcessesImpl();

    virtual int Scan();

};

#endif
```

然后是实现：

```cpp
#include "linuxprocessesimpl.h"

#include <unistd.h>

#include <sys/stat.h>

#include <fcntl.h>

#include <ctype.h>

int
LinuxProcessesImpl::Scan()
{
    DIR *dir;
    m_processList.clear();
    dir = opendir("/proc/");
    if (dir == NULL)
    if (!EnumProcesses(aProcesses, sizeof(aProcesses),
        &cbNeeded)
        return;
    // 计算返回了多少个
    // 进程标识。
    cProcesses = cbNeeded / sizeof(DWORD);
    // 打印每个
    // 进程的名称和标识符。
    for (int i = 0; i < cProcesses; i++) {
        if (aProcesses[i] != 0)
            PrintProcessNameAndID( aProcesses[i]);
    }
}
```
