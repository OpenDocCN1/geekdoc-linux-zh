
# 使用 Sockets 365 进行简单的跨平台通信

## 图 5.7 股票仓位跟踪系统的示例

传输包含新交易的 `CTransactionClass`

![](img/5c85d865d33d2c2c3c815331ae6c6f4a_376_0.png)

传输包含新仓位的 `CTransactionClass`

## 关于股票仓位跟踪系统 UDP 版本的结语

恭喜你！你刚刚完成了第一个跨平台通信系统的创建。请注意，执行实际通信的代码只是整个程序的一小部分。大部分代码用于处理和存储仓位及交易。需要记住的一点是待传输的 `XPCTTransaction` 对象需要特定操作系统的翻译。在 UNIX 和 Windows NT 系统之间传输数据时，需要克服的一个障碍是将大端（big-endian）数字转换为小端（little-endian）数字，反亦然。通过将交易金额和仓位值转换为 `XPEndian`，可以避免大和小端的转换问题。

另一个 Socket 通问题是字节对齐（byte packing）。通过将 `XPCTTransaction` 的数据组件保持为字符数组和 `XPCEndian` 对象，避免了字节对齐问题。UNIX 和 Windows NT 都将字节数对齐到最近字节。由于 `XPCTTransaction` 的数据成员都是字符数组（`XPCEndian` 对象可以视为字符数组），而一个字符是一个字节，因此 `XPCTTransaction` 被对齐到最近字节。

尽管已经开发了一个跨平台的仓位跟踪系统，但它仍然缺乏使其成为理想系统的要素。回想一下，理想的仓位跟踪系统允许多个客户端进行通信。规范还规定，多客户端通信不能影响仓位计算和传输的性能。列表 5.25 中开发的系统允许多个客户端连接。由于 UDP Socket 是无连接的，许多客户端可以向服务器传输数据。遗憾的是，连接的客户端越多，交易传输的可靠性越低。服务器一次只处理一次传输。在当前客户端传输完成之前，无法处理另一个客户端。如果客户端在另一个客户端正在处理时尝试传输，该客户端的传输消息可能会丢失，因为 UDP 数据包的传输不可靠的。仅仅发送了消息并不意味着它会被接收。事实上，由于消息传输是无连接的，即使只有一个客户端在通信，客户端和服务器都无法确保消息被接收。可靠的消息传输是股票仓位跟踪系统的核心组成部分。如果一笔交易从未被接收，股票交易员将不会高兴的。

遗憾的是，由于消息传输不可靠，UDP 不是创建股票仓位跟踪系统的正确协议。第 5.8 节讨论了 `XPCTcpSocket` 的创建并将其应用于股票仓位跟踪系统。使用 TCP Socket 解决了消息传输不可靠的问题，因为 TCP Socket 在客户端和服务器之间建立了真正的连接。

## 5.8 创建 TCP Socket 协议类

遗憾的是，UDP Socket 不提供可靠的数据传输。这是在第 5.7 节引入的股票仓位跟踪系统中一个不可接受的缺陷。当传输关键数据时，它必须到达目的地。TCP Socket 为消息问题提供了解决方案。TCP Socket 指定客户端-服务器之间的通信是面向连接的。在面向连接的通信中，必须存在真正的客户端-服务器连接才能传输数据。可以保证消息到达。如果连接不存在，客户端在发送数据时会收到错误。这与 UDP Socket 不同。UDP Socket 不存在客户端-服务器连接。UDP 客户端使用端口号和地址发送消息，但不知道服务器是否存在。由于无法获取对端是否存在，使用 UDP Socket 的应用程序对绑定（binding）是盲目的。发送消息的应用程序永远不会收到通知消息未接收的错误。回想一下，UDP 消息到达顺序并不与发送顺序相同。TCP Socket 协议保证消息按相同的顺序接收。

本文中引入的 TCP Socket 封装类是 `XPCTcpSocket`。`XPCTcpSocket` 与两个都继承自 `XPCSocket` 的类大不同，这两个类都通过使用协议名称和用于通信的端口构造 `HPCSocket` 来构造 socket 文件描述符。`XPCTcpSocket` 使用协议类型 TCP 构造 `XPCSocket`，这与 `XPCUdpSocket` 构造时使用的 UDP 不同。使用以下步骤创建 TCP Socket 服务器：

- 创建 socket 文件描述符（这在构造被自的基类 `XPCSocket` 时完成）
- 绑定到指定端口
- 监听传入的连接
- 接受新连接

当接受一个客户端连接时，会创建一个与原始器具有相同属性的新 socket 文件描述符，并用于客户端通信。只有在接受连接并创建新的 socket 文件描述符后，客户端才能发送和接收 socket 消息。相反，`XPCUdpSocket` 只需要一个 socket 绑定，同时也监听传入的连接并接受传入的连接。

当 TCP Socket 设置完成后，就可以接收消息。用于调用 `recv()` TCP Socket 消息的系统是 `recvv()`。UDP Socket 消息使用 `recvfrom()` 接收。`recvfrom()` 不检索 socket 消息，还捕获发送消息的应用程序地址。捕获的地址可以用于发送 UDP 回。对于 `XPCTcpSocket` 的 `ReceiveMessage()` 方法，不需要检索 IP 地址和端口号。`accept()`（`Accept()`）在客户端连接时捕获客户端地址，此时客户端和服务器已连接。由于客户端和服务器已连接，发送时不需要客户端的地址。

不仅 TCP 服务器接收消息的方式与 UDP 服务器不同，一旦创建了 socket 文件描述符，UDP 客户端就可以向指定的地址（IP 地址和端口号）发送消息。`XCUdpSocket` 内部 `iSendMessage()` 方法的参数不仅包含要发送的消息，还包含接收者的地址。要使用 `XPCTcpSocket` 发送消息，客户端必须通过 `connect()` 连接服务器。`connect()` 获取服务器的 IP 地址和端口号（有关 `connect()` 系统调用的更多信息请参见第 5.3 节）。一旦建立连接，就不需要包含服务器地址。因为 TCP Socket 不需要目标地址，`iSendMessage()` 代替了 `sendto()`。可以使用 `sendto()`，但它大材小用了。在发送 TCP 消息时，`sendto()` 的目标参数会被忽略。与 `sendto()` 不同，`send()` 不需要 socket 地址来确定消息目的地。（有关发送调用的更多信息请参见第 5.3 节）。

## `XPCTcpSocket` 类定义

列表 5.27 显示了 `XPCTcpSocket` 的定义。该类用于创建客户端和服务器 socket 应用程序。`XPCTcpSocket` 包含以下功能：

- Socket 创建
- Socket 绑定
- 监听传入的客户端连接
- 接受传入的连接并创建新的 socket 用于连接通信
- 连接到 TCP 服务器
- 向 TCP 客户端和服务器发送消息

`XPCTcpSocket` 包含了两个构造函数。第一个构造函数接受 socket 作为参数，并使用端口创建 TCP socket 文件。第二个构造函数用于创建用于客户端通信的 `XPCTcpSocket` 实例。当客户端连接并使用 `accept()` 创建新的 socket 文件描述符时，调用此构造函数。该构造函数接受 socket 文件描述符并将其存储在从 `XPSocket` 的私有变量 `iSocket` 中。由于两个构造函数都接受整数，通过将第一个构造函数设为 `short int` 而第二个设为 `long int` 消除了歧义。`XPCTcpSocket` 的所有方法在定义之后进行了详细讨论。特定操作系统的代码封装在 `#ifdef ... #endif` 块中。

# 列表 5.27 `XPCTcpSocket` 类定义

```cpp
#include <XPCSocket.h> // XPCSocket 的定义

class XPCTcpSocket : public XPCSocket
{
private:

#ifdef WINDOWS_NT

// Windows NT 特有的方法，用于获取指定
// 大小的完整消息。

int iReceiveMessage(void *_vMessage, int _iMessageSize);

#endif

public:

    // 构造函数。接受一个参数（套接字端口号），并创建一个 TCP 套接字文件描述符。

    XPCTcpSocket(short int _iPort) : XPCSocket("tcp", _iPort, _sSendToHost)
    ( _iConnect = 0);

    // 当客户端连接并因此创建一个新的文件
    // 描述符时调用的构造函数。

    XPCTcpSocket(long int _iSocket) : XPCSocket(_iSocket) { };

    // 将消息发送到已连接的主机应用程序。返回发送
    // 的字节数。
```
