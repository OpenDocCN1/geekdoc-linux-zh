
## vSuspend() 和 vResume()

`vSuspend()` 和 `vResume()` 分别调用 `SuspendThread()` 和 `ResumeThread()`。

列表 3.29 `XPCThread::vSuspend()` `XPCThread::onResume()`

```cpp
void XPCThread::onResume()
{
    if (ResumeThread(hThread) == (DWORD)-1)
    {
        XPCException ex
            (ErrorString("ResumeThread failed"));
        throw ex;
    }
}

void XPCThread::vSuspend()
{
    if (SuspendThread(hThread) == (DWORD)-1)
    {
        XPCException ex
            (ErrorString("SuspendThread failed"));
        throw ex;
    }
}
```

## iGetPriority() 和 vSetPriority()

`iGetPriority()` 和 `vSetPriority()` 分别调用 `GetPriority()` 和 `SetPriority()`。

列表 3.30 `XPCThread::vSetPriority()` `XPCThread::iGetPriority()`

```cpp
int XPCThread::iGetPriority()
{
    int nPriority;
    if (GetPriority(hThread, &nPriority))
    {
        return nPriority;
    }
    else
    {
        XPCException ex
            (ErrorString("GetPriority failed"));
        throw ex;
    }
}

void XPCThread::vSetPriority(int nPriority)
{
    if (!SetPriority(hThread, nPriority))
    {
        XPCException ex
            (ErrorString("SetPriority failed"));
        throw ex;
    }
}
```

## vDisablePriorityBoost() 和 iIsPriorityBoostDisabled()

`vDisablePriorityBoost()` 和 `iIsPriorityBoostDisabled()` 分别调用 `DisablePriorityBoost()` 和 `GetPriorityBoost()`。

## 206 第3章：NT 模块

列表 3.31 `XPCThread::vDisablePriorityBoost()` `XPCThread::iIsPriorityBoostDisabled()`

```cpp
void XPCThread::vDisablePriorityBoost(BOOL bDisable)
{
    if (!DisablePriorityBoost(hThread, bDisable))
    {
        XPCException ex
            (ErrorString("DisablePriorityBoost failed"));
        throw ex;
    }
}

int XPCThread::iIsPriorityBoostDisabled()
{
    BOOL bDisableBoost;
    if (GetPriorityBoost(hThread, &bDisableBoost))
    {
        return bDisableBoost ? 1 : 0;
    }
    else
    {
        XPCException ex
            (ErrorString("GetPriorityBoost failed"));
        throw ex;
    }
}
```

## vSetProcessorMask() 和 vSetIdealProcessor()

`vSetProcessorMask()` 和 `vSetIdealProcessor()` 都调用相应的 Win32 函数。

列表 3.32 `XPCThread::vSetProcessorMask()` `XPCThread::vSetIdealProcessor()`

```cpp
void XPCThread::vSetProcessorMask(DWORD dwMask)
{
    if (!SetAffinityMask(hThread, dwMask))
    {
        XPCException ex
            (ErrorString("SetAffinityMask failed"));
        throw ex;
    }
}

void XPCThread::vSetIdealProcessor(DWORD dwProc)
{
    if (SetIdealProcessorMask(hThread, dwProc) == -1)
    {
        XPCException ex
            (ErrorString("SetIdealProcessor failed"));
        throw ex;
    }
}
```

## vGetThreadTimes()

`vGetThreadTimes()` 主要用于调试和微调。用它来确定哪个线程使用了大部分系统资源。

列表 3.33 `XPCThread::vGetThreadTimes()`

```cpp
void XPCThread::vGetThreadTimes(LPFILETIME lpCreationTime,
    LPFILETIME lpExitTime,
    LPFILETIME lpKernelTime,
    LPFILETIME lpUserTime)
{
    if (!GetThreadTimes(hThread,
        lpCreationTime,
        lpExitTime,
        lpKernelTime,
        lpUserTime))
    {
        XPCException ex
        (XPCThread::ErrorString("GetThreadTimes failed"));
        throw ex;
    }
}
```

## NT 生产者-消费者程序

在 2.5 节关于 UNIX 线程中介绍的多生产者-单消费者示例在这里重新构建，并进行了修改以使用本节介绍的 NT `XPCThread` 类。我们需要两个额外的类来编写我们的生产者-消费者应用程序。其中一个是

## 第 3 章：NT 构建模块

一个通过其 `LPVOID` 参数向线程传递信息的类，`XPCThreadInfo`。另一个用于将数据从线程传回程序主循环的消息对象，`XPCMessage`。两者都定义在 `MultiProducer.h` 中，并在列表 3.34 中所示。

### 列表 3.34 `XPCThreadInfo` 和 `XPCMessage` 类

```cpp
XPCThreadInfo
private:
    char* sProdFilename;
    char* sSemName;
    XPCsemaphore* semFile;
    XPCsemaphore* semThread;
    XPCsemaphore* semMain;
    XEvent evExit;
public:
    // 构造函数 - 所有参数均为必需
    XPCThreadInfo(char* _sFilename, char* _SemName, XPCsemaphore* _threadSem, XPCsemaphore* _mainSem) : semFile(_SemName)
    {
        sProdFilename = new char[strlen(_sFilename)+1];
        sSemName = new char[strlen(_SemName)+1];
        strcpy(sProdFilename, _sFilename);
```
