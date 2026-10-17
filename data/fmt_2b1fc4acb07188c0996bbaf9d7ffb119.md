
```cpp
newTransaction.sGetTicker())) != NULL)

{

    individualPosition->vAddPosition(newTransaction.iGetAmount(),

newTransaction.cGetBS());

}

// 如果给定的 ticker 不存在位置，则向用户的

// 投资组合中添加新的 ticker 位置。

else

{

    individualPosition =

    userPositions[0].AddNewPosition(newTransaction.sGetTicker(),

newTransaction.iGetAmount()), newTransaction.cGetBS());

}

// 显示新位置，设置交易记录以反映

// 新位置，并将交易记录发送给

// 相应的客户端。

cout << "New Position: " << individualPosition->iGetPosition() << endl;
newTransaction.vSetAmount(individualPosition->iGetPosition());

// 使用 iSendMessage 方法将更新后的位置发送给
// 连接的客户端
_clientConnection->iSendMessage((void*)&newTransaction,
sizeof(newTransaction));

// 捕获由 TCP 套接字相关类引发引起的任何异常。以状态 0 退出子进程
catch(XPException &exceptObject)
{
    cout << exceptObject.sGetPosition() << endl;
    exit(0);
}
```

在此时，股票市场位置跟踪系统实现了原始应用程序规范的两个非常重要的目标。第一个是客户端-服务器通信是稳定的，并且保证了消息的传递。第二个是可以接受多个客户端连接，因此可以同时跟踪多个用户的股票仓。只有当客户端从服务器断开连接时，客户端当前的股票位置才会丢失。当与客户端通信的进程死亡时，进程中的所有内存都会被释放，包括所有位置信息。当客户端下次使用相同的用户名连接时，传输的位置信息仅反映当前连接的活动，而不反映之前的连接。

## 使用 TCP 套接字的多线程应用程序

当服务器进程死亡时，数据将会丢失，因为派生的进程不共享原始进程的资源。当一个进程死亡时，它的内存会被释放。在像股票市场位置跟踪系统这样的应用程序中，信息的丢失会导致系统变得不正确。创建客户端-服务器服务器线程可以克服数据丢失的问题。

应用程序中的线程共享原始应用程序的所有资源。共享的资源包括存储在堆上的内存。线程可以通过访问其全局变量或操作作为参数传递线程的内存来使用这些内存。通过允许线程访问原始进程的内存，当线程退出时，线程存储的数据不会丢失。

由于线程访问全局内存，因此必须保护全局内存免受多个执行线程的操控。如果两个线程同时访问全局内存，可能会发生内存损坏。当一个线程在内存中存储数据而另一个线程删除内存中存储的数据时，就会出现这种情况。读取内存的线程可能会尝试访问已不再存在的数据。

为了保护全局内存，使用了信号量。线程每次访问共享内存时，它都会锁定信号量。当线程完成其内存操作时，释放信号量。创建多线程 `TCP` 服务器的步骤与创建多进程 `TCP` 服务器相同，但多线程 `TCP` 服务器的架构不同。多线程 `TCP` 服务器的架构如图 `5.9` 所示。

# 392 第 5 章：套接字 — 跨平台通信的构建模块

图 `5.9` 多线程 `TCP` 套接字服务器架构

![](img/5c85d865d33d2c2c3c815331ae6c6f4a_403_0.png)

多线程 `TCP` 股票市场位置跟踪系统服务器显示在列表 `5.37`。

## 使用 TCP 套接字的多连接处理

### 列表 5.37 多线程 TCP 股票市场位置跟踪系统服务器

```cpp
#include <XPCTcpSocket.h>      // XPCTcpSocket 定义
#include <XPCemaphore.h>     // XPCSemaphore 定义
#include <XPCthread.h>         // XPCthread 定义
#include <iostream.h>
#include <errno.h>
#include <unistd.h>
#include <stdlib.h>

// XPCStockPosition 包含给定 ticker 符号的位置（完整类定义请见列表 5.23）。
class XPCStockPosition
{

};

// XPCUserPosition 类存储了给定用户的最多达 50 个不同股票 ticker 符号
//（完整类定义请见列表 5.23）。
class XPCUserPosition
{

};

// STcpThreadStruct 存储客户端通信所需的套接字信息，
// 以及指向匿名信号量的指针，该信号量用于保护对股票
// 投资组合数据结构的并行访问。该结构的实例被传递给
// 服务器线程。
struct STcpThreadStruct
{
    XPCTcpSocket *clientConnection;
    XPCSemaphore *positionSem;
};

// vStockTracker 函数的前声明。该函数与客户端
// 通信。服务器在接受客户端连接时
// 产生此线程。
void *vStockTracker(void *);

# 394 第 5 章：套接字 — 跨平台通信的构建模块

// STcpThreadStruct 指针，指向 Accept
// 方法实例
int iNumUsers; // 被跟踪的用户数
XPCUserPosition userPositions[50]; // 50 个投资组合
```

```cpp
int main() {
    // 创建处于“未锁定”状态的私有信号量。
    // 该信号量用于保护被多个线程访问的全局变量。
    XPCemaphore positionSem((int)1);

    // 初始化用户总数为
iNumUsers = 0;

try {
    // XPCTcpSocket 实例创建一个新的 TCP 套接字。
    // 此套接字实例用于接受连接
    XPCTcpSocket portfolioSocket(UNIX_PORT_NUM);

    // 套接字绑定到指定的端口并监听连接
    portfolioSocket.vBind();
    portfolioSocket.vListen();

// 无限循环接受客户端连接
while(1) {
    // 接受客户端连接。
    clientConnection = portfolioSocket.Accept();

// 创建一个新的 STcpThreadStruct 实例，并存储
// 由 Accept 创建的 CTcpSocket 实例的指针，
// 以及用于保护位置投资组合的匿名信号量的指针。
newTCPThreadStruct = new STcpThreadStruct;
newTCPThreadStruct->clientConnection = clientConnection;
newTCPThreadStruct->positionSem = &positionSem;

// 产生一个线程，它与客户端通信并
// 更新客户端的股票位置组合，并将更新后的
// ticker 位置返回给客户端。
XPCthread<int> newPositionKeeper(vStockTracker,
(void*)newTCPThreadStruct);

}
// 捕获并显示所有 XPC 相关的异常。
catch(XPCException &exceptionObject)
{
    cout << exceptObject.GetException() << endl;
    return 0;
}
```

```cpp
// 客户端线程接收客户端的股票交易消息，
// 更新用户投资组合中的 ticker 位置，并将更新后的
// ticker 位置返回给客户端。在处理客户端交易期间，
// 使用信号量保护投资组合数据结构。
void *vStockPositionTracker(void *vArg)
{
    // 线程参数被转换回 STcpThreadStruct 实例。
    STcpThreadStruct *newConnect = (STcpThreadStruct *)vArg;

    // 存储从客户端收到的交易记录。
    XPCTtransaction newTransaction;

    // 无限循环直到客户端断开。
    while(1)
    {
        try
        {
```
