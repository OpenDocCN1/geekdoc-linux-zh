
这几乎是一个理想的情况。我们不再需要在 `main` 函数中，或者代码中任何作为 `ProcessList` 实例的地方这样放置 `#ifdef` 了。更好的是，我们现在有一个合适的地方来放置通用代码了。为了给出一个简单的例子，假设我们需要在其中写入关于 `Scan()` 被调用的事实的日志。我们显然不希望要求调用者这样做，因为这可能被遗漏。但我们可以如下所示重写 `Scan()`（假设 `LOG` 是一个知道如何正确处理日志记录的宏，例如添加时间戳）：

```cpp
int
ProcessList::Scan()
{
    LOG("Scan was called!");
    #if defined(WIN32)
        return ScanWindows();
    #endif
    #if defined(DARWIN)
        return ScanMacOS();
    #endif
    #if defined(LINUX)
        return ScanLinux();
    #endif
    return -1;
}
```

## 项目 2：来自通用代码库的代码

然而，这里有一个小问题。我们需要为 `ProcessList` 类添加平台特定的函数。例如，让我们添加一个更改进程优先级的函数。在 UNIX 中，你通过调用 `nice()` 来实现，它接受一个整数优先级作为参数。在 Windows 中，你可以打开一个进程然后调用名为 `SetPriorityClass()` 的函数。（你可以在 http://msdn.microsoft.com 找到更多关于 `SetPriorityClass()` 函数的信息）。UNIX 的实现在返回值上有所不同；在 Linux 上，返回值为 0 表示成功，-1 表示失败。在 Darwin 等 BSD 系统上，返回值为进程优先级（这并无法可靠地用来表示失败或成功）。

为了实现此新功能，我们可以采取同样的技巧。我们可以为 `ProcessList` 添加一个抽象 API——我们称其为 `SetPriority()`——然后使用 `#ifdef` 在其体内部隔离对平台特定辅助函数的调用。在这里你可以看到这会导致什么结果。随着越来越多的平台特定功能的添加，`#ifdef` 的数量将会增加。为了管理这一点，我们使用了工厂。在至少一种工厂实现中，`#ifdef` 并没有被完全消除，但它们被减少到了单一位置，使得代码更具读性。

本质上，工厂允许我们在 `Scan()`（或 `ProcessList` 中定义的其他抽象 API 函数）的体内部请求并获取一个可以提供所需平台特定实现的对象。该对象继承自一个基类，该基类定义了指向平台特定实现的 API；此 API 通常镜像了我们寻求支持的 API。我们的类 `ProcessList` 维护一个指向该类的指针，而工厂是为我们提供这个指针的对象。有了该对象的指针，`Scan()` 的结构如下：

```cpp
int ProcessList::Scan()
{
  if (m_processesImpl)
    return m_processesImpl->Scan();
  return -1;
}
```

在这里，`m_processesImpl` 是指向工厂提供的对象的指针。我们可以在 `ProcessList` 的构造函数中按需从工厂获取此对象，如下所示：

```cpp
#include "processesfactory.h"

ProcessList::ProcessList(): m_processesImpl(NULL)
{
    ProcessesFactory *factory = GetProcessesFactory();

    if (factory)
        m_processesImpl = factory->MakeProcesses();
}
```
上述代码是条件编译的，并且构建系统保证设置一个定义（例如 `HAVE_WIN32`）。通常情况下，你需要在 Makefile 中这样做，以便在编译 `GetProcessesFactory()` 时作为编译器参数传递（例如 `g++ -DHAVE_WIN32`）。从这里开始假设 `HAVE_WIN32` 已定义。

```cpp
ProcessesFactory GetProcessesFactory()
{
    static ProcessesFactory *processesFactory = 0;
#if defined(HAVE_WIN32)
    processesFactory = WindowsFactory::GetFactoryInstance();
#endif
#if defined(HAVE_MACOS)
    processesFactory = CocoaFactory::GetFactoryInstance();
#endif
#if defined(HAVE_LINUX)
    processesFactory = LinuxFactory::GetFactoryInstance();
#endif
  return processesFactory;
}
```

## 平台工厂实现

每个平台都提供一个可以创建并返回平台特定实现指针的类（例如 `WindowsFactory`）。该类被编译到链接到平台的库中。每个支持的平台都有该库的实例。当平台无关代码拥有此指针后，可以使用它创建提供平台特定功能的对象。

## WindowsFactory

`WindowsFactory` 实现了一个单一的静态函数 `GetFactoryInstance()`，它创建并返回平台特定的实现单例：

```cpp
#if !defined(__WINDOWS_FACTORY_H__)
#define __WINDOWS_FACTORY_H__

#include "../processesfactory.h"
#include "../processesimpl.h"
```

```cpp
class WindowsFactory : public ProcessesFactory
{
public:
  static WindowsFactory *GetFactoryInstance()
  {
    static WindowsFactory *factory = 0;
    if (!factory)
      factory = new WindowsFactory();
    return factory;
  }
};
```

## 30 第1章 策略与管理

```cpp
}
virtual ~WindowsFactory();
  virtual ProcessesImpl *MakeProcesses();
private:
  WindowsFactory();
};
```

#endif

这里发生了两件事。首先，我们有一个静态函数 `GetFactoryInstance()`，它允许我们创建并获取 `WindowsFactory` 的单例实例。我们在上面已经看到它是如何使用的。另一个需要注意的关键点是工厂实现了一个名为 `MakeProcesses()` 的函数，它返回我们所需的 `ProcessesImpl` 对象的指针。`WindowsFactory` 并不限于创建支持进程的对象；通常情况下，工厂（也应该被用于）用于创建各种对象，每个对象都提供与特定领域相关的平台功能。在这里，我们看到 `WindowsFactory` 能够创建一个提供处理进程支持的对象，但假设我们需要提供能够处理文件读写的平台无关代码。为了做到这一点，我们可以创建一个新的抽象类 `FilesFactory`，并如下所示扩展 `WindowsFactory`（加粗部分为更改内容）：

```cpp
#if __WINDOWS_FACTORY_H__
#define __WINDOWS_FACTORY_H__

#include "../processesfactory.h"
#include "../processesimpl.h"
#include "../filesfactory.h"
#include "../filesimpl.h"
```

```cpp
class WindowsFactory : public ProcessesFactory,
  public FilesFactory
public:
  static WindowsFactory *GetFactoryInstance()
  {
    static WindowsFactory *factory = 0;
    if (!factory)
        factory = new WindowsFactory;
    return factory;
  }
```

## 项目 2：来自通用代码库的代码

```cpp
virtual ~WindowsFactory();
virtual ProcessesImpl *MakeProcesses();
virtual FilesImpl *MakeFiles();
private:
    WindowsFactory();
};
#endif
```

注意，`GetFactoryInstance()` 应该是线程安全的。请参见 Andrei Alexandrescu 写的《Modern C++: Generic Programming and Design Patterns Applied》（Addison-Wesley, 2001）第 6 章，获取更多关于使单线程线程安全的详细信息。

在继续之前，让我们总结一下目前的情况，在过去的几页中已经提供了大量信息。我们在 `ProcessList` 中拥有平台无关的代码，它实现了一个抽象函数 `Scan()`。从应用程序的角度来看，`Scan()` 可以用于获取进程名称和 ID 的列表。`Scan()` 并不知道具体如何执行平台特定的工作，因此需要帮助。为了获得帮助，`Scan()` 获取了一个工厂对象的指针，该对象是平台无关的。这个工厂对象可以创建进一步的对象，这些对象本身是抽象的，但提供了我们所寻求的功能；例如，工厂支持的某种对象支持进程，另一种对象支持文件访问，以此此类推。当应用程序获取到工厂时，它会调用这些函数之一（例如 `MakeProcesses()`）来获取一个实现了所需功能的对象指针。

## 实现类

现在让我们看看平台特定的代码是如何实现的。我们看到 `MakeProcesses()` 返回类型为 `ProcessesImpl` 的对象的指针。`ProcessesImpl` 是一个带有纯虚函数的基类，我们必须为这些函数提供平台特定的实现。（纯虚函数是 C++ 强制派生自基类的类在派生类中实现该函数的方法。基类不为该函数提供任何实现。）它也可以包含所有平台可以共享的平台无关代码。以下是 `ProcessesImpl` 的定义：

## 32 第1章 策略与管理

```cpp
#include "processes.h"
#include <vector>

class ProcessesImpl {
public:
    ProcessesImpl() {};
    virtual ~ProcessesImpl();
    virtual int Scan() = 0;
    int GetCount();
    const char* GetName(const int which);
    int GetPID(const int which);
protected:
    std::vector<Process> m_processList;
};
#endif
```

该类的大部分内容恰好实现了所有平台共享的代码。进程名称和 ID 列表存储在标准模板库 (STL) `vector` 中，该 具有高度的可移植性。`GetCount()`、`GetName()` 和 `GetPID()` 等函数与此 `vector` 交互并仅依赖于它，因此自然也在基类中实现。

## 平台特定的 ProcessesImpl 类

另一方面，`Scan()` 函数是平台特定的，必须在派生类中实现，在 Windows 上，该派生类是 `WindowsProcessesImpl`：

```cpp
#if defined(_WIN3PROCESSESIMPL_H_)
#define _WIN3PROCESSESIMPL_H_

#include "../processesimpl.h"

#include <windows.h>
#include <stdio.h>
#include <tchar.h>
#include <psapi.h"

class WindowsProcessesImpl : public ProcessesImpl {
public:
    WindowsProcessesImpl();
    virtual ~WindowsProcessesImpl();
```

## 项目 2：来自通用代码库的代码

```cpp
virtual int Scan();
private:
    void ScanProcesses();
    void PrintProcessNameAndID(DWORD processID);
#endif
```

包含了 Windows 特有的头文件（例如 `windows.h`）。由于这段代码只会在 Windows 上编译，因此在这里头文件中包含此代码或任何其他平台特定的代码是可以的。`Scan()` 函数使用了两个 `WindowsProcessesImpl` 私有的辅助辅助函数：`ScanProcesses()` 和 `PrintProcessNameAndID()`。只要 `Scan()` 按照基类的要求声明，任何方式都可以。以下代码显示了 `WindowsProcessesImpl` 类的大部分内容：

```cpp
#include "windowprocessesimpl.h"

int
WindowsProcessesImpl::Scan()
{
    m_processList.clear();

    ScanProcesses();

    return m_processList.size();
}

void WindowsProcessesImpl::PrintProcessNameAndID(DWORD processID)
{
    TCHAR szProcessName[MAX_PATH] = TEXT("unknown");

    // 获取进程的句柄
    HANDLE hProcess = OpenProcess(PROCESS_QUERY_INFORMATION | PROCESS_VM_READ, FALSE, processID);

    if (NULL != hProcess)
    {
        // 获取进程名称
        HMODULE hMod;
        if (EnumModules(hProcess, hMod, szProcessName, sizeof(szProcessName)))
        {
            // 打印名称和标识符
            Process proc;
            proc.SetPID(processID);
            proc.SetName(szProcessName);
            m_processList.push_back(proc);
        }
        CloseHandle(hProcess);
    }
}

void WindowsProcessesImpl::ScanProcesses()
{
    // 获取标识符列表
    DWORD aProcesses[1024], cbNeeded, cProcesses;
    unsigned int i;

    if (!EnumProcesses(aProcesses, sizeof(aProcesses), &cbNeeded))
        return;

    // 计算返回了多少标识符
    cProcesses = cbNeeded / sizeof(DWORD);

    // 打印每个进程的名称和标识符
    for (i = 0; i < cProcesses; i++)
        if (aProcesses[i] != 0)
            PrintProcessNameAndID(aProcesses[i]);
}
```

## 34 第1章 策略与管理

加粗的代码是我写的；其余部分是微软在 msdn.microsoft.com 上使用 Win32 API提供的示例代码。我的代码只需要提供 `Scan()` 接口的实现。（因为 `Scan()` 在基类中是纯虚拟。）并且，每个扫描到的进程都需要推入基类中维护的 vector 末尾。但此而已。

## Linux

如果你查看 Linux 和 BSD/Darwin 实现，你会发现它们遵循相同的基本方法。这里是 Linux 的实现，它使用 proc 文件系统获取进程信息。

首先是头文件：

```cpp
#if defined__LINUXPROCESSESIMPL_H__
#define LINUXPROCESSESIMPL_H_

#include "../processes.h"
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
```

```cpp
int
LinuxProcessesImpl::Scan()
{
    DIR *dir;
```
