

其他典型的清理步骤包括关闭文件和注销处理程序。以下是 `Socket` 类的析构函数：

```cpp
/****** Socket destructor
Socket::~Socket(void)
{
    if ( close(SD) != 0 )
        throw FileException("Can't close socket");
}
```

你应该将所有析构函数声明为虚拟的（virtual），以便继承层次结构中的所有析构函数都能被执行。非虚拟析构函数表明你不希望在对对象执行 `delete` 操作时触发父类的析构函数。你可以仅仅指定父类（superclass）的析构函数为虚拟的——这会使所有继承的析构函数也变为虚拟的。然而，为了清晰起见，你可能希望显式地将它们声明为虚拟的。

## 测试 Socket 框架

Socket 框架是一个基于前几节所述标准的自定义实现。接下来的章节将通过几个示例展示如何使用它。随附本文的网站还有几个其他示例，展示了如何实现数据报、广播和多播套接字。

## 回显客户端/服务器

第一个示例（也是全书引用最多的）是回显客户端/服务器。使用回显客户端/服务器的真正原因是为了测试通信是否正常工作。一旦掌握了这部分，剩下的就很简单了。

**清单 13.1** 介绍了基本的客户端。

**清单 13.1** Echo-Client.cpp

```cpp
/**** Client main body
HostAddress addr(strings[1]);  // <address:port> format
try
{
    SocketClient client(addr);  // Create the socket & connect
    TextMessage msg(1024);  // Set aside the message space
    do  // Repeat until "bye"
    {
        char line[100];
        client.Receive(msg);  // Get the welcome or reply
        printf("msg=%s", msg.GetBuffer());  // Display it
        fgets(line, sizeof(line), stdin);    // Get line
        msg = line;                           // Place in message space
        client.Send(msg);                    // Send message to server
    }
    while ( strcmp(msg.GetBuffer(), "bye\n") != 0 );
}
catch (Exception& err)
{
    err.PrintException();
}
```

所有程序都使用相同的 `try...catch()` 格式。你希望使用它来捕获和恢复系统可能遇到的异常。以下是清单 13.1 中省略的一个 `catch()`，这是你始终应该放在调用树末端的一个：

```cpp
//***************************************
// Exception Catchall
catch(...)
{
    fprintf(stderr, "Unknown exception!\n");
}
```

此定义捕获所有你未曾预料到的情况。

服务器可以是内置的回显服务器、邮件服务器或 HTTP 服务器。`TextMessage` 类与这些服务器都兼容。尽管如此，清单 13.2 向你展示了回显服务器的对象版本。

**清单 13.2** Echo-Server.cpp

```cpp
//***************************************
// Server's main body
try
{
    SocketServer server(port);   // Create & config the socket
    do                           // Repeat forever
        server.Accept(Echoer);   // Connect & serve a client
    while ( 1 );
}
```

如你所见，服务器主体非常简单。`SocketServer` 为你完成所有的配置和设置。变量 `Echoer` 是过程的另一半（参见清单 13.3）。

**清单 13.3** Echo-Server.cpp, Part 2

```cpp
//*****************************************************
// Server's client service routine (Echoer)
try
{
    TextMessage msg(1024);  // Get a message buffer
    client.Send(welcome);  // Send "welcome" message
    do                         // Repeat until "bye"
    {
        client.Receive(msg);  // Get message
        client.Send(msg);     // Echo it back
    }
    while ( msg.GetSize() > 0 &&
            strcmp(msg.GetBuffer(), "bye\n") != 0 );
}
```

再次强调，算法很简单：接收消息并发送回去，直到客户端发送“bye”消息为止。你可能注意到，这个程序摘录拥有自己独立的 `try...catch()` 块。这是一个好主意。如果该连接发生错误，它仅与该连接相关，并且不应影响主套接字。如果缺少清单 13.3 中的专用 `try...catch` 块，当客户端突然断开连接时，整个服务器将会崩溃，因为主函数的 `try...catch` 块会捕获该异常。

## 放置异常处理程序

仔细规划在哪里以及何时放置异常处理程序。此外，你可能不希望处理所有类型的异常。相反，你可能只希望支持特定的类型。通常，不同的连接需要它们自己的 `try...catch()` 块，而灾难性异常应仅位于调用树的根部。

当前的服务器实现不提供多任务处理。该类包含实现多任务处理所需的一些挂钩。

## 对等网络多任务处理

你仍然可以使用进程或线程来进行多任务处理。即使当前框架未实现这一点，你可以在代码中创建任务。经典示例是数据报，它必须在发送消息的同时接受任意数量的消息（参见清单 13.4）。

**清单 13.4** Peer.cpp

```cpp
//**********************
// Datagram message sender
try
{
    HostAddress addr(strings[1]); // Define own address
    Socket *channel = new Datagram(addr); // Create socket
    if ( !fork() ) // Create process
        receiver(channel); // Call data receiver
    channel->CloseInput(); // Close input channel
    HostAddress peer(strings[2]); // Define peer addr
    TextMessage msg(1024); // Create msg space
    do
    {
        char line[100];
        fgets(line, sizeof(line), stdin); // Read line
        msg = line; // Place in message
        channel->Send(peer, msg); // Ship it.
    }
    while ( !done );
    delete channel;
}
```

`receiver()` 的实现看起来很像 `SocketServer` 的 `Echoer` 调用。

如果你希望在该框架中使用多任务处理，你需要记住几条规则：

- *遵循规则*—回顾第 7 章“划分负载：多任务处理”中的注意事项和建议。特别是，确保捕获子进程终止信号。此外，线程共享它们的 I/O 通道；关闭一端将对所有线程关闭。
- *内存共享*—意识到内存资源争用是一个几乎无解的问题。尽量少共享。
- *C++ 的局限性*—在 C++ 中采用多线程是危险的。幕后发生的情况太多，你必须非常小心哪个线程拥有哪些数据。在启动新线程之前在栈上创建对象可能会导致不可预测的结果。

多任务处理有其优势，你仍然可以使用 C++，但要非常小心。

## 实现局限性

该框架仅仅是一个功能性的——但不完整的——示例，展示了如何在 C++ 库中实现套接字。这应该给你一些想法，关于如何调整它（或编写你自己的）以满足你的编程需求。

就目前而言，你可以创建客户端、服务器、数据报以及多播/广播套接字。它允许你使用套接字选项来配置套接字。它包含一个消息抽象，因此你可以编写自己的消息格式。以下章节列出了几个用于功能增强的想法。

### 发送未知/未定义消息

当前框架允许你从 `Message` 派生自己的消息类型。如果你专门使用 `Message` 组件或拥有已知类型，这非常方便。然而，你可能没有灵活性仅从单个类派生——特别是在集成遗留系统时。

多重继承有时是一种必要的恶，特别是当你试图合并不同且经常冲突的框架时。Java 拥有接口的优势，但这看起来在可预见的未来对 C++ 来说并不是一个选项。

同样，你并不总是知道数据本身。这种情况经常发生，当你有一个较新的客户端与遗留服务器接口时。服务器不知道客户端可能支持哪些扩展，因此性能可能会受到影响。编写一个抽象的消息协议可以解决这个问题。

抽象的信使不仅持有数据，还持有数据结构。这类似于发送带有目录结构的文件。抽象的信使可以使主机之间的通信更有用且更具扩展性。

### 添加多任务处理

另一个局限性，如前所述，是缺乏多任务支持。大多数与网络交互的程序同时执行多个任务以提高性能。将进程和线程作为框架的内在功能提供，会使编程简单得多。

问题源于类的基本定义：某物所做的和所知的事情。因此，如果你定义一个套接字类，你会拥有多任务套接字和多线程套接字吗？此外，任务是一个对象吗？如果是，那么真正有两个可派生的类：`Socket` 和 `Process/Thread`。结果是多重继承问题（大多数面向对象原教旨主义者会对此皱眉）。

也许问题看起来比实际更简单。但将客户端、服务器、数据报、广播和多播与非多任务、线程和进程组合成 15 个类的想法并不是最优的。

