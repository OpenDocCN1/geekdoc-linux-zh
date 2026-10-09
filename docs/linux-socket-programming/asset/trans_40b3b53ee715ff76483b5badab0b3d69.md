
### 异常 (Exception) (基类)

构造函数:

```
Exception(SimpleString s);
```

通用描述: 带有 SimpleString 类型参数的通用异常消息。

方法:

| 方法 | 描述 |
| :--- | :--- |
| `const char* GetString()` | 获取字符串消息。 |

子类异常:

| 异常 | 描述 |
| :--- | :--- |
| `RangeException` | 任何范围异常。由 MessageGroup 类使用。 |
| `FileException` | 任何文件异常。由 Socket 类使用。 |

### NetException (类)

构造函数:

```
NetException(SimpleString s);
```

通用描述: 通用网络异常。

父类: `Exception`

子类异常:

| 异常 | 描述 |
| :--- | :--- |
| `NetConversionException` | 主机 (inet_ntop/inet_pton) 地址转换异常。由 HostAddress 类使用。 |
| `NetDNSException` | 无法解析主机名的异常。由 HostAddress 使用。 |
| `NetIOException` | send()/recv() 异常。由 Socket 使用。 |
| `NetConnectException` | 尝试使用 bind()、connect()、listen() 或 accept() 时发生的异常。由 ServerSocket、ClientSocket 和 MessageGroup 使用。 |
| `NetConfigException` | 尝试设置或获取套接字选项时发生的异常。由所有 Socket 类使用。 |

## C++ 支持类

本节描述了一些与框架相关的类，但它们比其他类库中的类更简单。您可以随意用标准 C++ 类库替换这些类。

### SimpleString (类)

构造函数:

```
SimpleString(const char* s);
SimpleString(const SimpleString& s);
```

通用描述: 非常简单的轻量级字符串类型。

方法:

| 方法 | 描述 |
| :--- | :--- |
| `operator+=(const char* s), operator+=(SimpleString& s)` | 将字符串追加到当前实例。 |
| `const char* GetString()` | 获取字符串消息。 |

抛出异常: (无)

### HostAddress (类)

构造函数:

```
HostAddress(const char* Name=0, ENetwork Network=eIPv4);
HostAddress(HostAddress& Address);
```

通用描述: 用于管理主机标识的类。

方法:

| 方法 | 描述 |
| :--- | :--- |
| `void SetPort(int Port)` | 设置端口号。 |
| `int GetPort(void) const` | 获取端口号。 |
| `ENetwork GetNetwork(void) const` | 获取网络类型。 |
| `struct sockaddr* GetAddress(void) const` | 获取实际的套接字地址。 |
| `int GetSize(void) const` | 获取套接字地址大小。 |
| `bool operator==(HostAddress& Address) const` | 比较是否相等。 |
| `bool operator!=(HostAddress& Address) const` | 比较是否不相等。 |
| `const char* GetHost(bool byName=1)` | 获取主机名。 |

抛出异常:
- `NetConversionException`
- `NetDNSException`

## C++ 消息类

该类别体系结构允许您定义能够自打包和自解包内部数据的类。虽然不如 Java 中的体系结构那么简单直接，但它的处理方式简单直接。

### Message (抽象类)

构造函数: (无)

通用描述: 用于创建特定消息以进行发送和接收的消息模式。

方法:

| 方法 | 描述 |
| :--- | :--- |
| `virtual char* Wrap(int& Bytes) const` | 对象打包接口。 |
| `bool Unwrap(char* package, int Bytes, int MsgNum)` | 对象解包接口。 |

抛出异常: (无)

### TextMessage (类)

构造函数: (无)

通用描述: 用于创建特定消息以进行发送和接收的消息模式。

父类: `Message`

方法:

| 方法 | 描述 |
| :--- | :--- |
| `operator+=(const char* str), operator+=(const TextMessage& s)` | 将新字符串赋值给对象。 |
| `operator#=(const char* str), operator#=(const TextMessage& s)` | 将字符串追加到对象。 |
| `const char* GetBuffer(void) const` | 获取文本。 |
| `char* Wrap(int& Bytes) const` | 封装对象以便发送。 |
| `bool Unwrap(char* package, int Bytes, int MsgNum)` | 解封装接收到的对象。 |
| `int GetSize(void) const` | 获取字符串长度。 |
| `void SetSize(int Bytes)` | 设置字符串长度。 |
| `int GetAvailable(void) const` | 获取缓冲区中可用的字节数。 |

抛出异常: (无)

## C++ 套接字类

该体系结构定义了构成套接字接口的类。它实际上包含五个可以实例化的不同类：`SocketServer`、`SocketClient`、`Datagram`、`Broadcast` 和 `MessageGroup`。您可以轻松地使用 OpenSSL 类（`SSLServer` 和 `SSLClient`）扩展此体系结构。

![](img/03334662da8fdfb8d95a02f270c522f6_355_0.png)

### Socket (基类)

构造函数:

```
Socket (void);
Socket (int sd);
Socket (ENetwork Network, EProtocol Protocol);
Socket (Socket& sock);
```

通用描述: 通用套接字类，不打算直接实例化。

方法:

| 方法 | 描述 |
| :--- | :--- |
| `void Bind (HostAddress& Addr)` | 将套接字绑定到端口/接口。 |
| `void CloseInput (void) const` | 关闭输入流。 |
| `void CloseOutput (void) const` | 关闭输出流。 |
| `int Send (Message& Msg, int Options=0) const` | 向连接站点发送消息。 |
| `int Send (HostAddress& Addr, Message& Msg, int Options=0) const` | 发送定向消息。 |
| `int Receive (Message& Msg, int Options=0) const` | 从连接接收消息。 |
| `int Receive (HostAddress& Addr, Message& Msg, int Options=0) const` | 接收定向消息。 |
| `void PermitRoute (bool Setting)` | 允许可路由数据包。 |
| `void KeepAlive (bool Setting)` | 保持连接活跃。 |
| `void ShareAddress (bool Setting)` | 共享端口/接口地址。 |
| `int GetReceiveSize (void); void SetReceiveSize (int Bytes)` | 获取/设置接收缓冲区大小。 |
| `int GetSendSize (void); void SetSendSize (int Bytes)` | 获取/设置发送缓冲区大小。 |
| `int GetMinReceive (void); void SetMinReceive (int Bytes)` | 获取/设置 SIGIO 接收信号的最小水位线。 |
| `int GetMinSend (void); void SetMinSend (int Bytes)` | 获取/设置 SIGIO 发送信号的最小水位线。 |
| `struct timeval GetReceiveTimeout (void); void SetReceiveTimeout (struct timeval& val)` | 获取/设置终止接收之前的超时时间。 |
| `struct timeval GetSendTimeout (void); void SetSendTimeout (struct timeval& val)` | 获取/设置终止发送之前的超时时间。 |
| `ENetwork GetType (void)` | 获取套接字类型（网络）。 |
| `virtual int GetTTL (void); virtual void SetTTL (int Hops)` | 获取/设置生存时间 (time-to-live)。 |
| `int GetError (void)` | 获取任何待处理错误。 |

抛出异常:
- `NetException`
- `FileException`
- `NetConnectException`
- `NetIOException`
- `NetConfigException`

### SocketStream (类)

构造函数:

```
SocketStream(void);
SocketStream(int sd);
SocketStream(ENetwork Network);
SocketStream(SocketStream& sock);
```

通用描述: 流式 (SOCK_STREAM) 套接字。

父类: `Socket`

方法:

| 方法 | 描述 |
| :--- | :--- |
| `int GetMaxSegmentSize(void); void SetMaxSegmentSize(short Bytes)` | 获取/设置分段大小 (MSS)。 |
| `void DontDelay(bool Setting)` | 启用/禁用 Nagle 算法。 |

抛出异常:
- `NetConfigException`

### SocketServer (类)

构造函数:

```
SocketServer(int port, ENetwork Network=eIPv4, int QLen=15);
SocketServer(HostAddress& Addr, int QLen=15);
```

通用描述: TCP 服务器。

父类: `SocketStream`

方法:

| 方法 | 描述 |
| :--- | :--- |
| `void Accept(void (*Servlet)(const Socket& Client))` | 接受连接并使用 Socket 句柄调用 Servlet。 |
| `void Accept(HostAddress& Addr, void (*Server)(const Socket& Client))` | 接受连接并捕获主机 ID。 |

抛出异常:
- `Exception`
- `NetConnectException`

### SocketClient (类)

构造函数:

```
SocketClient (ENetwork Network=eIPv4);
SocketClient(HostAddress& Host, ENetwork Network=eIPv4); //自动连接
```

通用描述: TCP 客户端。

父类: `SocketStream`

方法:

| 方法 | 描述 |
| :--- | :--- |
| `void Connect(HostAddress& Addr)` | 连接到 Addr 处的主机。 |

抛出异常:
- `NetConnectException`

### Datagram (类)

构造函数:

```
Datagram(HostAddress& Me, ENetwork Network=eIPv4, EProtocol Protocol=eDatagram);
Datagram(ENetwork Network=eIPv4, EProtocol Protocol=eDatagram);
```

通用描述: 通用数据报 (UDP) 套接字。

父类: `Socket`

方法:

| 方法 | 描述 |
| :--- | :--- |
| `void MinimizeDelay(bool Setting)` | 请求最小数据包延迟。 |
| `void MaximizeThroughput(bool Setting)` | 请求最大网络吞吐量。 |
| `void MaximizeReliability(bool Setting)` | 请求最大可靠性。 |
| `void MinimizeCost(bool Setting)` | 请求最小成本。 |
| `void PermitFragNegotiation(EFrag Setting)` | 设置分片协商。 |

