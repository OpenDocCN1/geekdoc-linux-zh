
Parent Class: Exception

Child Exceptions:

| Exception | Description |
|---|---|
| NetConversionException | Host (inet_ntop/inet_pton) address conversion exception. Used by HostAddress class. |
| NetDNSException | Could not resolve hostname exception. Used by HostAddress. |
| NetIOException | send()/recv() exception. Used by Socket. |
| NetConnectException | Exception when trying to use bind(), connect(), listen(), or accept(). Used by ServerSocket, ClientSocket, and MessageGroup. |
| NetConfigException | Exception when trying to set or get socket option. Used by all Socket classes. |

## C++ Support Classes

This section describes several classes that are related to the framework but are simpler than those of other class libraries. Feel free to replace these as desired with the standard C++ class libraries.

### SimpleString (Class)

Constructor:

```cpp
SimpleString(const char* s);
SimpleString(const SimpleString& s);
```

General Description: Very simple and lightweight string type.

Methods:

| Method | Description |
|---|---|
| operator+(SimpleString& ) | Append string to current instance. |
| const char* GetString() | Retrieve the string message. |

Exceptions Thrown: (none)

### HostAddress (Class)

Constructor:

```cpp
HostAddress(const char* Name=0, ENetwork Network=IPv4);
HostAddress(HostAddress& Address);
```

General Description: Class to manage host identification.

Methods:

- `void SetPort(int Port);` Set the port number.
- `int GetPort(void) const;` Get the port number.
- `ENetwork GetNetwork(void) const;` Get the network type.
- `struct sockaddr* GetAddress(void) const;` Get the actual socket address.
- `int GetSize(void) const;` Get socket address size.
- `int ==(HostAddress& Address) const;` Compare if equal.
- `int !=(HostAddress& Address) const;` Compare if not equal.
- `const char* GetHost(bool byName=1);` Retrieve the hostname.

Exceptions Thrown:

- Exception
- NetConversionException
- NetDNSException

## C++ Messaging Classes

This class hierarchy lets you define classes that self-package and self-unpackage the internal data. While not as simple or direct as the hierarchy in Java, it’s simple and direct.

### Message (Abstract Class)

Constructor: (none)

General Description: Message pattern for creating a specific message to send and receive.

Methods:

- `virtual char* Wrap(int& Bytes) const;` Interface for packaging object.
- `bool Unwrap(char* package, int Bytes, int MsgNum);` Interface for unpacking object.

Exceptions Thrown: (none)

### TextMessage (Class)

Constructor: (none)

General Description: Message pattern for creating a specific message to send and receive.

Parent Class: Message

Methods:

```cpp
operator= (const char* str);  Assign a new string to object.
operator= (const TextMessage& s);  
operator+= (const char* str);  Append string to object.
operator+= (const TextMessage& s);  
const char* GetBuffer(void) const;  Get the text.
char* Wrap(int& Bytes) const;  Wrap object to send.
bool Unwrap(char* package, int Bytes, int MsgNum);  Unwrap received object.
GetSize(void) const;  Get length of string.
void SetSize(int Bytes);  Set string length.
int GetAvailable(void) const;  Get available bytes in buffer.
```

Exceptions Thrown: (none)

## C++ Socket Classes

This hierarchy defines the classes that make up the socket interfaces. It contains effectively five different classes that you can instantiate: SocketServer, SocketClient, Datagram, Broadcast, and MessageGroup. You can easily expand this hierarchy with OpenSSL classes (SSLServer and SSLClient).

![](img/2591af4bdf00a0f382331fc9481f785e_500_0.png)

**FIGURE D.2**
*The C++ Socket class hierarchy.*

### Socket (Superclass)

Constructor:

```cpp
Socket(void);
Socket(int sd);
Socket(ENetwork Network, EPProtocol Protocol);
Socket(Sock& sock);
```

General Description: General socket class, not intended for direct instantiation.

Methods:

- `void Bind(HostAddress& Addr);` Bind socket to port/interface.
- `void CloseInput(void) const;` Close input stream.
- `void CloseOutput(void) const;` Close output stream.
- `int Send(Message& Msg, int Options=0) const;` Send message to connected site.
- `int Send(HostAddress& Addr, Message& Msg, int Options=0) const;` Send directed message.
- `int Receive(Message& Msg, int Options=0) const;` Receive message from connection.
- `int Receive(HostAddress& Addr, Message& Msg, int Options=0) const;` Receive directed message.
- `void PermitRoute(bool Setting);` Allow routable packets.
- `void KeepAlive(bool Setting);` Keep connection alive.
- `void ShareAddress(bool Setting);` Share port/interface address.
- `int GetReceiveSize(void);` Get/set receive buffer size.
- `void SetReceiveSize(int Bytes);`
- `int GetSendSize(void);` Get/set send buffer size.
- `void SetSendSize(int Bytes);`
- `int GetMinReceive(void);` Get/set minimum watermark for SIGIO receive signal.
- `void SetMinReceive(int Bytes);`
- `int GetMinSend(void);` Get/set minimum watermark for SIGIO send signal.
- `void SetMinSend(int Bytes);`
- `struct timeval GetReceiveTimeout(void);` Get/set time before aborting a receive.
- `void SetReceiveTimeout(struct timeval& val);`
- `struct timeval GetSendTimeout(void);` Get/set time before aborting a send.
- `void SetSendTimeout(struct timeval& val);`
- `ENetwork GetTType(void);` Get the socket type (network).
- `virtual int GetTTL(void);` Get/set the time-to-live.
- `virtual void SetTTL(int Hops);`
- `int GetError(void);` Get any pending errors.

Exceptions Thrown:

- NetException
- FileException
- NetConnectException
- NetIOException
- NetConfigException

### SocketStream (Class)

Constructor:

```cpp
SocketStream(void);
SocketStream(int sd);
SocketStream(ENetwork Network);
SocketStream(SocketStream& sock);
```

General Description: Streaming (SOCK_STREAM) socket.
Parent Class: Socket

Methods:

- `int GetMaxSegmentSize(void);` Get/set the segment size (MSS).
- `void SetMaxSegmentSize(short Bytes);`
- `void DontDelay(bool Setting);` Enable/disable Nagle algorithm.

Exception Thrown:
- NetConfigException

### SocketServer (Class)

Constructor:

```cpp
SocketServer(int port, ENetwork Network=IPv4, int QLen=15);
SocketServer(HostAddress& Addr, int QLen=15);
```

General Description: TCP server.
Parent Class: SocketStream

Methods:

- `void Accept(void (*Servlet)(const Socket& Client));` Accept a connection and call Servlet with Socket handle.
- `void Accept(HostAddress& Addr, void (*Server)(const Socket& Client));` Accept connection and capture host ID.

Exceptions Thrown:
- Exception
- NetConnectException

### SocketClient (Class)

Constructor:

```cpp
SocketClient(ENetwork Network=eIPv4);
SocketClient(HostAddress& Host, ENetwork Network=eIPv4); //auto-connect
```

General Description: TCP client.
Parent Class: SocketStream

Method:

- `void Connect(HostAddress& Addr);` Connect to host at Addr.

Exception Thrown:
- NetConnectException

### Datagram (Class)

Constructor:

```cpp
Datagram(HostAddress& Me, ENetwork Network=eIPv4, EProtocol Protocol=eDatagram);
Datagram(ENetwork Network=eIPv4, EProtocol Protocol=eDatagram);
```

General Description: General datagram (UDP) socket.
Parent Class: Socket

Methods:

- `void MinimizeDelay(bool Setting);` Request minimal packet delay.
- `void MaximizeThroughput(bool Setting);` Request maximum network throughput.
- `void MaximizeReliability(bool Setting);` Request maximum reliability.
- `void MinimizeCost(bool Setting);` Request minimal cost.
- `void PermitFragNegotion(EFrag Setting);` Set fragmentation negotiation.

Exception Thrown:
- NetConfigException

### Broadcast (Class)

Constructor:

```cpp
Broadcast(HostAddress& Me);
```

General Description: Broadcast socket for subnets.
Parent Class: Datagram

Methods: (none)

Exception Thrown:
- NetConfigurationException

### MessageGroup (Class)

Constructor:

```cpp
MessageGroup(HostAddress& Me, ENetwork Network=eIPv4);
```

General Description: Multicast socket.
Parent Class: Datagram

Methods:

- `Connect(HostAddress& Address);` Connect to multicast group address.
- `void Join(HostAddress& Address, int IFIndex=0);` Join multicast group.
- `void Drop(HostAddress& Address);` Drop multicast group.

Exceptions Thrown:

- NetConfigurationException
- NetConnectException
- RangeException

## Java Exceptions

This section describes all the relevant exceptions that a Java program may generate while working with its sockets.

![](img/2591af4bdf00a0f382331fc9481f785e_504_0.png)

**FIGURE D.3**
*The Java exceptions class hierarchy.*
