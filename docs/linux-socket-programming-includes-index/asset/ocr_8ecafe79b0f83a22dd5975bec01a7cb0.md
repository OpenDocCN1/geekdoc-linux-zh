Parent Class: Message

# Methods:

```
= (const char* str);  Assign a new string to object.
= (const TexitMessage& s);  
+= (const char* str);  Append string to object.
+= (const TexitMessage& s);  
const char* GetBuffer(void) const;  Get the text.
char* Wrap(int& Bytes) const;  Wrap object to send.
bool Unwrap(char* package, int Bytes, int MsgNum);  Unwrap received object.
GetSize(void) const;  Get length of string.
void SetSize(int Bytes);  Set string length.
int GetAvailable(void) const;  Get available bytes in buffer.
```

Exceptions Thrown: (none)

# C++ Socket Classes

This hierarchy defines the classes that make up the socket interfaces. It contains effectively five different classes that you can instantiate: SocketServer, SocketClient, Datagram, Broadcast, and MessageGroup. You can easily expand this hierarchy with OpenSSL classes (SSLServer and SSLClient).

![](bbox=[0.27, 0.62, 0.7, 0.68])

# FIGURE D.2

*The C++ Socket class hierarchy.*

# Socket (Superclass)

Constructor:

```
Socket(void);
Socket(int sd);
Socket(ENetwork Network, EPProtocol Protocol);
Socket(Sock& sock);
```