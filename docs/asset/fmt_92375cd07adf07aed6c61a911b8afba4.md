
# `WSACleanup()` 函数

## 说明
应用程序在执行完毕后使用 `WSACleanup()` 函数终止所有后续套字的使用。在应用程序调用 `WSACleanup()` 之前，应使用 `closesocket()` 关闭打开的套字。在正常操作中，客户端终止但服务器持续运行。

## 参数
`WSACleanup()` 不接受任何参数。

## 返回值
`WSACleanup()` 成功时返回 0，返回 `SOCKET_ERROR` 表示发生错误。当发生错误时，可以调用 `WSAGetLastError()` 获取提供特定错误原因的代码。

# `WSAGetLastError()` 函数

## 头文件
```
#include <winsock.h>
```

## 用法
`retvalue = WSAGetLastError(void);`

## 说明
应用程序调用 `WSAGetLastError()` 函数获取套字失败后的错误代码。在多线程环境中，`WSAGetLastError()` 是全局变量 `errno` 的替代品。

## 参数
`WSAGetLastError()` 不接受任何参数。

## 返回值
`WSAGetLastError()` 返回套字函数的状态。

# `WSAStartup()` 函数

## 头文件
```
#include <winsock.h>
```
