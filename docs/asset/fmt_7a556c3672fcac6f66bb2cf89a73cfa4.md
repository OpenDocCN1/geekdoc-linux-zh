
```cpp
// 从服务数据库条目中返回服务协议。
char *sGetServiceProtocol() { return servicePtr->s_proto; }
```

```cpp
// 从服务数据库条目中返回服务端口号。
int iGetServicePort() { return servicePtr->s_port; }
```

## XPCGetService 重载构造函数 (UNIX 和 Windows NT)

`XPCGetService` 提供了两个重载构造函数。它们都指向匹配服务搜索标准的服务数据库条目中的私有数据成员。搜索标准包括协议（通常为 UDP 或 TCP）以及服务名称或端口号。协议默认设置为 `NULL`。如果未指定协议，则返回服务数据库中的第一个条目。构造函数如列表 5.11 所示，并标注了适用于 UNIX 和 Windows NT 的代码。

## 列表 5.11 XPCGetService 重载构造函数

```cpp
XPCGetService::XPCGetService(const char *_sServiceName, const char *_sProto)
{
    #ifdef UNIX
    // 如果操作系统是 UNIX，将数据库迭代器标志置为 false
    clIteratorFlag = 0;
    #endif

    if (_sProto != NULL)
    {
        // 如果向构造函数传递了协议，则根据协议名称实例化
        // XPCGetProtocol 。如果协议名称无效，则会抛出异常。
        // 异常被捕获后，XPCGetService 将使用 XPCGetProtocol 
        // 信息抛出一个新异常。
        try
        {
            XPCGetProtocol verifyProtocol(_sProto);
        }
        catch (XPCException &exceptObject)
        {
          char sMsg[512];

          sprintf(sMsg, "Error getting service using Protocol %s: %s\0",
              _sProto, exceptObject.sGetException());
          XPCException getServiceException(sMsg);
          throw getServiceException;
          return;
        }
    }

    // 根据服务名称和可选的服务协议返回服务数据库条目的指针。
    // 如果服务条目不存在，由 XPCGetService 抛出异常。
    if ((servicePtr = getservbyname(_sServiceName, _sProto)) == NULL) 
    {
      char sMsg[512];

#ifdef WINDOWS_NT
      // 如果操作系统是 Windows NT，在异常体中返回相关的
      // 错误号。
      sprintf(sMsg, "Can not find Service By Name: Error %#d",
          WSAGetLastError());
#else
      strcpy(sMsg, "Can not find Service By Name");
#endif

      XPCException getServiceException(sMsg);
      throw getServiceException;
      return;
    }
}

XPCGetService::XPCGetService(int _iPort, const char *_sProto)
{
#ifdef UNIX
  // 如果操作系统是 UNIX，将数据库迭代器标志置为 false
  cIteratorFlag = 0;
#endif

  if (_sProto != NULL)
  {
    // 如果向构造函数传递了协议，则根据协议名称实例化
    // XPCGetProtocol 。如果协议名称无效，则会抛出异常。
    // 异常被捕获后，XPCGetService 将使用 XPCGetProtocol 
    // 异常抛出一个新异常。
    try {
        XPCGetProtocol verifyProtocol(_sProto);
    } catch (XPCException &exceptObject) {
        char sMsg[512];

        sprintf(sMsg,
            "Error getting service using Protocol %s: %s",
            _sProto, exceptObject.sGetException());

        XPCException getServiceException(sMsg);
        throw getServiceException;
        return;
    }
  }

  // 根据 socket 端口号和可选的服务协议返回服务数据库条目的指针。
  // 如果服务条目不存在，由 XPCGetService 抛出异常。
  if ((servicePtr = getservbyport(_iPort, _sProto)) == NULL) {
    char sMsg[512];
#ifdef WINDOWS_NT
    // 如果操作系统是 Windows NT，在异常体中返回相关的
    // 错误号。
    sprintf(sMsg, "Can not Find Service By Name: Error %#d",
        WSAGetLastError());
#else
    strcpy(sMsg, "Can not Find Service By Name");
#endif
    XPCException getServiceException(sMsg);
    throw getServiceException;
    return;
  }
}
```

## cGetNextService() 成员函数 (仅限 UNIX)

UNIX 提供了一种遍历服务数据库的方法。此功能封装在 `cGetNextService()` 中。该函数返回 `true` (1) 或 `false` (0)。如果到达数据库末尾且无法再获取更多服务条目，或者数据库迭代器标志被设置为 `false`，则返回 `false`。如果成功获取条目且有更多条目可用，则返回 `true`。

## 列表 5.12 cGetNextService() 成员函数

```cpp
char XPCGetService::cGetNextService()
{
    // 如果数据库已打开，则获取下一个条目。
    if (cIteratorFlag)
    {
        // 如果有更多条目，返回 true。
        if (servicePtr = cNextService())
        {
            return 1;
        }
    }
    // 如果没有更多条目，返回 false。
    cIteratorFlag = 0;
    return 0;
}
```

## 5.7 使用 Socket 进行简单的跨平台通信

目前提供的信息已足够编写第一个跨平台通信应用程序。本书的目标之一是在一个面向对象的框架中展示所有代码。该框架将所演示的概念封装在类中。这些类可以直接在应用程序中使用，也可以作为基类被更专门的类继承。

`Socket` 为构建对象层次结构提供了良好的基础。如果你还记得图 5.4 和图 5.5，创建 UDP 和 TCP `socket` 的任务有一些相似之处。最基本的一点是，它们都是通过调用 `socket()` 返回的 `socket` 文件描述符定义的。传递给 `socket()` 的参数定义了打开的 `socket` 类型。UDP 和 TCP `socket` 通信的另一个共同特征是它们都会关闭自己的 `socket`

## 332 第5章：套接字——跨平台通信构建模块

Windows NT 中 `close() (closesocket())` 或 `shutdown()` 的文件描述符。这些系统是本书介绍的基类 `PSocket` 套接字的起点。`socket` 在构造函数中创建，并在析构函数中关闭。
