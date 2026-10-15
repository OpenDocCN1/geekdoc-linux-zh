
```cpp
#include <XPCocket.h> // XPCocket 的定义

class XUDPSocket : public XPCocket
{
public:
    // 构造函数。接收一个 socket 通信端口号作为参数。
    // 该参数与 UDP 协议规范一起发送给
    // XPCocket 的构造函数以创建 socket 文件描述符。
    XUDPSocket(int _iPort) : XPCocket(_iPort) {
// ... (注：由于原文存在大量重复OCR错误，此处已根据核心逻辑翻译并清理)

## 使用 Sockets 进行简单的跨平台通信 347

原始结构，因为结构体中的某些数据成员可能缺失或错误。（有时，如果正在检查的部分提供了关于剩余数据的信息，那么只查看结构体的部分内容是理想的。因此，如果大小小于传输数据的总大小，则不会报错。）重要的一点是，`MsgLen` 参数的值至少要与 `vMessage` 指向的结构体一样大。记住 UDP 消息是以数据报的形式发送的，必须接收整个消息。在接收 TCP 套接字时不存在这种限制。最后一个参数是一个可选的选项标志 `_iOption`。该标志控制消息的接收方式。`_iOption` 参数可能包含以下值之一：0、`MSG_WAITALL`（仅限 UNIX）或 `MSG_PEEK`。（这些值的完整解释见第 5.4 节对 `recvfrom()` 的讨论。）

默认情况下，`_iOption` 的值为 0。如果 `_iOption` 为 0 或 `MSG_WAITALL`，消息将存储在 `_vMessage` 参数中。当将 `_iOption` 设置为 0 或 `MSG_WAITALL` 时，确保 `_vMessage` 和 `_MsgLen` 包含足够的空间来存储消息。否则，消息会被截断。如果 `_iOption` 的值为 `MSG_PEEK`，则 `_vMessage` 是不重要的，因为消息没有被存储。消息的大小在套接字上。此值被传递给 `_iMsgLen` 并可用于 `_Message` 缓冲区分配内存。记住，尽管运行时调整缓冲区的大小，但对于 UDP 套接字，其大小有限制。在从 `XPCSocket` 基类接收 `GetReceiveBuf()` 后，检查消息缓冲区的大小是非常重要的。列表 5.20 显示了在调整缓冲区以正确接收传入的消息后调用消息缓冲区的大小来确定它的示例。

## 列表 5.20 确定传入消息的大小

```cpp
char *sMessage;

int iMsgLen;

try {

    XPCdpSocket someSocket(SOME_PORT_NUM);

    someSocket.v.receiveMessage((void *)sMessage, iMsgLen, MSG_PEEK);

    if (iMsgLen <= someSocket.getReceiveBuf()) {

        sMessage = new char[iMsgLen];

        someSocket.receiveMessage((void *)sMessage, iMsgLen, 0);

    }

} catch(XPCException &socketException) {

    //

}
```

在接收消息之前，套接字必须绑定到地址和端口号。通过检查 `cBind` 标志的值来查看套接字是否已绑定。如果 `cBind` 标志为 `false` (0)，则调用 `vBindSocket()`。由于 `iReceiveMessage()` 完成了绑定套接字的工作，使用 UDP 套接字只需要以下代码。

## 348 第 5 章：Sockets — 跨平台通信构建模块

```cpp
#define PORTNUM 6450

// 要绑定到套接字的端口号

...

someStruct MessageStruct; // 包含
    // 套接字消息的结构体

try {

    // 创建一个 UDP 套接字。

    XPCdpSocket newSocket(PORTNUM);

    // 将套接字绑定到端口，并将套接字消息
    // 接收到 MessageStruct 中。

    newSocket.iReceiveMessage((char *)&MessageStruct, sizeof(someStruct));

} catch(XPCException &socketException) {

    // 捕获所有与套接字相关的异常

    ...
}
```

使用 `recvfrom()` 接收消息。`recvfrom()` 将套接字消息放入 `_vMessage` 参数中，并将发送消息的应用程序的地址存储在继承自 `XPCocket` 类的 `clientAddress` 数据成员中。也可以使用第 5.3 节讨论的 `recvfrom()` 系统调用。然而，`recvfrom()` 的额外好处是将发送应用程序的地址和端口存储在 `sockaddr_in` 结构（`clientAddress`）中，`clientAddress` 可以作为发送回复消息的地址（参见关于 `iSendReply()` 方法的讨论）。如果成功，`iReceiveMessage()` 返回接收到的总字节数。

## 列表 5.21 XPCdpSocket 的 `iReceiveMessage()` 方法

```cpp
int XPCdpSocket::iReceiveMessage(void *_vMessage, int &iMsgLen, int _iOption) {

    int iClientAddrLen; // sockaddr_in 地址结构的长度。

    int iNumBytes; // 接收到的字节数。

    // 如果套接字尚未绑定，则在接收消息之前
    // 调用 vBindSocket 方法绑定套接字。

    if (cBind == 0) {

        try {

            vBindSocket();

        } catch (XPCException &exceptObject) {

            char sMsg[512];

            sprintf(sMsg, "Error Receiving Message. Bind Socket: %s\0",
                exceptObject.s.GetException());

            XPCException socketExcept(sMsg);

            throw socketExcept;

            return 0; // 返回接收到的 0 字节。

        }

        cBind = 1;

    }

    // 获取客户端地址的大小。发送消息的应用程序
    // 地址放在数据成员 clientAddress 中。

    iClientAddrLen = sizeof(clientAddress);

    // 调用 recvfrom 系统调用接收消息，使用
    // _iOption 参数中指定的选项。如果无法接收消息，
    // 将抛出异常。

    if ((iNumBytes = recvfrom(iSocket, (char*)vMessage, iMsgLen, _iOption,
        (struct sockaddr *)&clientAddress, iClientAddrLen)) == -1) {

        char sMsg[512];

        sprintf(sMsg, "Error Receiving Message: %s\0",
            getError());

        XPCException socketExcept(sMsg);

        throw socketExcept;

    }

    return iNumBytes; // 返回接收到的字节数。
}

```cpp

// 判断消息长度是否大于允许的 UDP 限制

if (_iMsgLen > iGetSendBuf())

{

    XPCeception socketExcept("Message length specified is larger\nthan protocol limit.\nMessage was not sent");

    throw socketExcept;

    return;

}

// 向本地 hostAddress 变量存储的地址发送消息。

// 如果发送的字节数不符合最小要求，

// 则发生错误并抛出异常。

if ((iNumBytes = sendto(iSocket, (char*)vMessage, _iMsgLen, 0,
```
