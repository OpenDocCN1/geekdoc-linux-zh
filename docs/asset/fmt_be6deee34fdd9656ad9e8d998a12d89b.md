
`CloseHandle()` 用于在事件完成后关闭事件。`SetEvent()` 和 `ResetEvent()` 用于设置事件状态，`PulseEvent()` 也是如此。`PulseEvent()` 的行为类似于 `SetEvent()`，取决于创建事件时 `bManualReset` 的值。如果 `bManualReset` 为 `true`，`PulseEvent()` 会释放所有等待该事件的线程并重置事件。如果 `bManualReset` 为 `false`，如果有多个线程在等待，`PulseEvent()` 仅释放一个等待线程，并重置事件。

## 等待事件

当事件发生且等待进程处于等待状态时，事件会向该进程发出信号。这种等待状态通过调用此处所示 `WaitSingleObjectEx()` 实现。

```
DWORD WaitSingleObjectEx(HANDLE hHandle,
    DWORD dwMilliseconds,
    BOOL bAlertable);
```

`hHandle` 是指向事件的句柄，`dwMilliseconds` 是等待事件的时间，`bAlertable` 指定了之前是否通过调用 `QueueUserAPC()` 指定了一个待调用的程序。`WaitSingleObjectEx()` 用于等待许多类型的 NT 对象，包括信号量、线程和进程。Win32 提供了一个用于等待对象列表的调用 `WaitMultipleObjectsEx()`。

```
DWORD WaitMultipleObjectsEx(DWORD nCount,
    CONST HANDLE *pHandles,
    BOOL bWaitAll,
    DWORD dwMilliseconds,
    BOOL bAlertable);
```

`pHandles` 是指向句柄数组的指针，`nCount` 是数组中句柄的数量。如果 `bWaitAll` 为 `true`，`WaitMultipleObjectsEx()` 将在所有句柄都发出信号时返回；如果为 `false`，则在其中一个发出信号时返回。

Win32 提供了另外两个等待函数，用于调用线程创建了窗口且必须处理窗口消息的情况。如果你的应用程序创建并管理窗口，则优选 `MsgWaitForObjectsEx()` 和 `MsgWaitForObjectEx()`。由于此处展示的所有示例都是控制台应用程序，因此使用了 `WaitForObjectEx()`。

## 处理事件

等待事件发生会挂起程序的进程，这并不总是如人所意的。你可能希望在等待事件发生时执行其他处理。解决方案是调用 `QueueUserAPC()`，它描述了一个在事件发生时被调用的回调程序。`QueueUserAPC()` 的用法在 `XPEvent` 类的实现中描述。

```
DWORD QueueUserAPC(APCFUNC pfnAPC,
    HANDLE hThread,
    DWORD dwData);
```

`pfnAPC` 是指向回调函数的指针。`hThread` 是等待事件的线程的句柄。`dwData` 是传递给回调函数的值。

## XPEvent 实现

`XPEvent` 类定义如列表 3.10 所示。注意，微软基础类 (MFC) 中的 `CEvent` 类封装了事件的创建和操作函数。

## 174 第 3 章：NT 模块

MFC 的 `XPEvent` 与此处介绍的 `XPEvent` 相同。值得注意的是，MFC `XPEvent` 缺少一个设置回调函数的方法。

## 列表 3.10 XPEvent 头文件

```
#include <windows.h>
#include "XPException.h"

class XPEvent {
private:
    // 事件的句柄
    HANDLE hEvent;

    // 回调函数的地址，如果
    // 提供了的话。否则为空。事件发生时
    // 调用的用户提供的函数。
    PAPCFUNC pfnAPC;
    // 安全属性
    SECURITY_ATTRIBUTES pSA;
    // 指向线程的句柄
    HANDLE hThread;
    // 线程 ID
    DWORD dwThread;

    static WINAPI dwThreadProc(LPVOID);

public:
    // 构造函数
    XPEvent(char *sEventName, PAPCFUNC pfnAPC=NULL);
    // 拷贝构造函数
    XPEvent(const XPEvent&);
    // 析构函数
    virtual ~XPEvent();

    // 返回事件句柄
    HANDLE GetHandle();
    // 返回回调函数地址
    PAPCFUNC GetFunc();
};
```

## 175 事件

```
// 封装 SetEvent
void SetEvent();
// 封装 PulseEvent
void PulseEvent();
// 封装 WaitSingleObjectEx
void WaitSingleObjectEx(DWORD, INFINITE);
// 封装 ResetEvent
void ResetEvent();
static char* ErrorString(char*)
```

安全属性结构被创建、初始化并传递给 `CreateEvent()`。如果提供了回调函数，则调用 `CreateThread()` 来监控事件，并在事件发生时将其加入队列。参见 195 页的“编程 Win32 线程”。`this` 指针随后传递给线程，以便访问成员。如果在静态函数中尝试访问非成员函数，编译器会报错。通过 `this` 指针访问成员函数的规避方法见。

## 176 第 3 章：NT 模块

```
// 首先分配安全属性结构
// 并初始化它
pSA=(SECURITY_ATTRIBUTES) HeapAlloc(GetProcessHeap(), 0, sizeof(SECURITY_ATTRIBUTES));

pSA->nLength=sizeof(SECURITY_ATTRIBUTES);
pSA->lpSecurityDescriptor=NULL;
pSA->bInheritHandle=TRUE;

// 创建事件，手动重置，初始状态为重置
if ((hEvent = CreateEvent(pSA, TRUE, FALSE, sEventName)) == NULL)
{
    XPCException ex(ErrorString("CreateEvent failed"));
    throw ex;
}
```

## 列表 3.11 XPEvent 构造函数

```
XPEvent(char *sEventName, PAPCFUNC pfnAPC)
{
    // 首先分配安全属性结构
    // 并初始化它
    pSA=(SECURITY_ATTRIBUTES) HeapAlloc(GetProcessHeap(), 0, sizeof(SECURITY_ATTRIBUTES));

    pSA->nLength=sizeof(SECURITY_ATTRIBUTES);
    pSA->lpSecurityDescriptor=NULL;
    pSA->bInheritHandle=TRUE;

    // 创建事件，手动重置，初始状态为重置
    if ((hEvent = CreateEvent(pSA, TRUE, FALSE, sEventName)) == NULL)
    {
        XPCException ex(ErrorString("CreateEvent failed"));
        throw ex;
    }

    // 如果提供了用户定义的回调
    // 创建一个线程来监控事件
    // 在事件发生时将其加入队列。
    // 见下文 dwThreadProc。
    if ((pfnAPC=pfnAPC) != NULL)
    {
        if ((hThread=CreateThread(pSA, 0, dwThreadProc, this, 0, &dwThreadID)) == NULL)
        {
            IPcexception exception(ErrorString("CreateThread failed"));
            throw;
        }
    }
    else
        hThread= NULL;
}
```

## 列表 3.12 线程进程
