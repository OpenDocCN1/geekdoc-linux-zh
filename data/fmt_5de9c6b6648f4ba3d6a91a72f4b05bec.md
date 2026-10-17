
```cpp
void XPCService::installService ()
{
    // 获取服务管理器句柄
    SC_HANDLE hServiceManager=OpenSCManager(NULL, // local PC
        NULL, // active services database
        SC_MANAGER_ALL_ACCESS);

    // 如果无法获取，则抛出异常
    if (!hServiceManager) {
        XPCEException ex(ErrorString("OpenSCManager failed"));
        throw ex;
    }

    // 如果已经安装，无需操作
    if (!iiServiceInstalled()) {
        // 创建服务
        SC_HANDLE hService=CreateService(hServiceManager,
            sServiceName,
            sServiceName,
            SERVICE_ALL_ACCESS,
            SERVICE_WIN32_OWN_PROCESS,
            SERVICE_DEMAND_START,
            SERVICE_ERROR_NORMAL,
            sAppPath,
            NULL,
            NULL,
            NULL,
            NULL);

        if (!hService) {
            CloseServiceHandle(hServiceManager);
            XPCEException ex(ErrorString("CreateService failed"));
            throw ex;
        }
        // 退出前关闭所有句柄
        CloseServiceHandle(hService);
    }
    CloseServiceHandle(hServiceManager);
}
```

`iiServiceInstalled()` 通过打开并关闭句柄来测试服务是否已安装。如果打开失败，说明服务未安装。

## 列表 3.48 `XPService::iiServiceInstalled()`

```cpp
int XPService::iiServiceInstalled() {
    int iRet= FALSE;

    // 首先获取服务管理器句柄
    SC_HANDLE hServiceControlManager= OpenSCManager(NULL, // local PC
        NULL, // active services database
        SC_MANAGER_ALL_ACCESS);

    // 如果无法获取，则抛出异常
    if (!hServiceControlManager) {
        XPCEException ex (ErrorString("OpenSCManager failed"));
        throw ex;
    }

    // 打开服务句柄
    SC_HANDLE hService=OpenService(hServiceControlManager, sServiceName, SERVICE_QUERY_STATUS);
    if (hService) {
        iRet = TRUE;
        CloseServiceHandle(hService);
    }
    CloseServiceHandle(hServiceControlManager);
    return iRet;
}
```

## 248 第 3 章：NT 基础

```cpp
// 以查询模式打开服务
SC_HANDLE hService = OpenService(hServiceControlManager,
    sServiceName,
    SERVICE_QUERY_CONFIG);

// 如果没有获取到句柄，说明服务未安装
if (hService)
{
    iRet = TRUE;
    CloseServiceHandle(hService);
}

// 关闭所有句柄并返回结果
CloseServiceHandle(hServiceControlManager);
return iRet;
```

### `XPCService::RemoveService()`

`RemoveService()` 从本地机器上删除服务。

列表 3.49 `XPCService::RemoveService()`

```cpp
void XPCService::RemoveService()
{
    // 获取服务器的句柄
    SC_HANDLE hServiceControlManager = OpenSCManager(NULL, // 本地 PC
    NULL, // 活动服务数据库
    SC_MANAGER_ALL_ACCESS);

    // 如果无法获取，则抛出异常
    if (!hServiceControlManager)
    {
        XPCException ex(ErrorString("OpenSCManager failed"));
        throw ex;
    }

    // 打开服务，所有访问权限
    SC_HANDLE hService = OpenService(hServiceControlManager,
    sServiceName,
    SERVICE_ALL_ACCESS);
```

```cpp
// 如果我们获取了服务的句柄，
if (hService)
{
    // 则向 ServiceMain 发送停止停止的消息
    if (ControlService(hService,
        SERVICE_CONTROL_STOP,
        &ServiceStatus))
    {
        XPCException ex
            (CString("ControlService failed"));
        throw ex;
    }
    // 并删除服务
    if (!DeleteService(hService))
    {
        XPCException ex
            (CString("DeleteService failed"));
            throw ex;
    }
    CloseServiceHandle(hService);
}

CloseServiceHandle(hServiceControlManager);
```

### `XPCService::vSetControl()`

`vSetControl` 向服务的 `ServiceMain()` 函数发送一个控制字。`dwCtrl` 可以是表 3.16 中列出的值之一（参见第 243 页）。

## 列表 3.50 `XPCService::vSetControl()`
