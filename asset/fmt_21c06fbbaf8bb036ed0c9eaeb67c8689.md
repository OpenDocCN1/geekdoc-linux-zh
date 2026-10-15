
`GetFileAttributesEx()` 具有如下原型定义。

```c
BOOL GetFileAttributesEx(LPCTSTR FileName,
                         GET_FILE_INFO_LEVELS pinfoLevelID,
                         LPVOID lpFileInformation);
```

第一个参数 `FileName` 和第二个参数 `infoLevelID` 告诉 `GetFileAttributesEx()` 目录名以及返回的属性。此值目前限制为字面值 `GetFileInfoStandard`。最后一个参数 `lpFileInformation` 是一个指向 `WIN32_FILE_ATTRIBUTE_DATA` 结构的指针。

## 错误处理

大多数 Win32 函数在成功时返回非零值，在失败时返回零。失败后，调用 `GetLastError()` 会返回一个错误代码，调用 `FormatMessage()` 获取该错误代码的错误消息。此功能封装在 `XPCFileStat` 的私有成员函数 `sString` 中。每当 `XPCFileStat` 抛出异常时就会调用 `XPCFileStat.sString()`

## 内存管理

除了 C 运行时库中的内存函数外，Win32 还提供了内存分配函数。Win32 函数包括 `HeapAlloc()`、`VirtualAlloc()` 及其对应的释放函数等。C 运行时库中常用的函数是 `malloc()` 和 `free()`（以及 C++ 中的 `new()` 和 `delete`）。在 Windows 的早期版本中，内存管理器使用 16 位段内存模型，这对使用 `malloc()` 分配内存造成了巨大的限制。Windows 程序在 Windows SDK 中调用 `LocalAlloc()` 和 `GlobalAlloc()` 来规避这些限制。Windows NT 的出现和 32 位虚拟内存模型的引入消除了对 `LocalAlloc()` 和 `GlobalAlloc()` 的需求（尽管为了兼容，两者在 Win32 中仍然存在）。`HeapAlloc()` 和 `VirtualAlloc()` 被用作替代。结果是通过 `malloc(new())` 和 `HeapAlloc()` 创建的内存可以互换使用。遵循 Windows 编程社区的特设编码标准，本书中的示例使用 `HeapAlloc()` 来分配传递给 Win32 函数的内存。

## NT XPCFileStat 定义

NT 版本的 `XPCFileStat` 将路径名和等同于 stat 结构的内容（`WIN32_FILE_ATTRIBUTE_DATA`）作为私有成员变量。它还保留了几个用于确定应用程序访问权限的结构和变量。

### 列表 3.1 XPCFileStat 头文件

```c
#ifndef _XPCFileStat_h_

#define _XPCFileStat_h_

#include <windows.h>

#include <aclapi.h>

#include "XPCException.h"

// 为了简单起见重新定义的 Win 32 属性常量

#define FILE_TYPESWORD

#define ARCHIVEFILE_ATTRIBUTE_ARCHIVE

#define COMPRESSEDFILE_ATTRIBUTE_COMPRESSED

#define DIRECTORYFILE_ATTRIBUTE_DIRECTORY

#define HIDDENFILE_ATTRIBUTE_HIDDEN

#define NORMALFILE_ATTRIBUTE_NORMAL

#define OFFLINEFILE_ATTRIBUTE_OFFLINE

#define READONLYFILE_ATTRIBUTE_READONLY

#define SYSTEMFILE_ATTRIBUTE_SYSTEM

#define TEMPORARYFILE_ATTRIBUTE_TEMPORARY

class XPCFileStat {

private:

    char * sFileName; // 存储文件名或目录

    // 文件属性

    WIN32_FILE_ATTRIBUTE_DATA fileAttr;

    // 安全描述符

    SECURITY_DESCRIPTOR pSD;

    // 所有者和组信任人

    PTRUSTEE pOwner, pGroup;

    // 保持访问列表中的条目数量

    ULONG nAccess, nAudit;

    EXPLICIT_ACCESS pAccess, pAudit;

    // 进程句柄

    HANDLE hProcess;

    // 令牌句柄

    HANDLE hToken;

    // 进程组信息

    PGROUP pGroup;

    // 进程用户信息

    PUSER pUser;

    // 错误字符串

    char *sErr;

    // 访问列表

    void *pAccess;

    // 审计列表

    void *pAudit;

public:

    // 默认构造函数

    XPCFileStat();

    // 特定路径构造函数

    XPCFileStat(char*sFileName);

    // 拷贝构造函数

    XPCFileStat(const XPCFileStat &);

    // 析构函数

    ~XPCFileStat();

    // 工作函数

    void vGetStat(char *_sFileName);

    // 获取大小

    DWORD iGetSize();

    // 获取文件类型

    DWORD dwFileType();

    // 获取路径名

    const char *sFileName();

    // 创建时间

    FILETIME ftCreationTime();

    // 上次访问时间

    FILETIME ftAccessTime();

    // 上次写入时间

    FILETIME ftModTime();

};

#endif
```

### XPCFileStat 构造函数

三个构造函数用于创建 `XPCFileStat` 实例。默认构造函数没有参数并使用当前工作目录。稍后显示的的工作函数 `vGetStat()` 用于获取状态。

### 列表 3.2 XPCFileStat 默认构造函数

```cpp
XPCFileStat::XPCFileStat()

{

    // 首先获取所需的缓冲区大小

    int iBufSize=GetCurrentDirectory(0
```

### 列表 3.3 XPCFileStat 构造函数

```cpp
XPCFileStat::XPCFileStat(char * _sFileName)

{

    // 在堆上为路径名分配空间

    sFileName= new char[strlen(_sFileName)+1];

    if (!sFileName)

    {

        // 如果无法获取内存则抛出异常

        XPCException ex(CString("Could not allocate memory for sFileName"));

        throw ex;

    }

    // 拷贝路径名

    strcpy(sFileName, _sFileName);

    // 调用工作函数获取 stat

    vGetStat(sFileName);

}
```

## 列表 3.4 XPCFileStat 的 vGetStat() 方法，部分 1

```cpp
void XPCFileStat::vGetStat(char *_sFileName)

{

  if (!GetFileAttributesEx (_sFileName,

      GetFileInfoStandard,

      (LPVOID)&fileAttr))

  {

    XPCException ex((CString("GetFileAttributesEx failed.")));

    throw ex;

    return;

  }

}
```

`dwGetFileType()` 返回文件属性的位图。使用 `&` 运算符结合表 3.4（见第 151 页）中列出的属性常量与 `dwGetFileType()` 返回的值，可以获取文件类型。例如，接下来的测试将确定文件是否已归档。

```cpp
if (fs.dwGetFileType() | ARCHIVE)

{

}
```
