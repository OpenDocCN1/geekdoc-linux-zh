# java.net.DatagramSocket (Class)

Constructor:
DatagramSocket();
DatagramSocket(int port);
DatagramSocket(int port, InetAddress bindAddr);

General Description: This is the general datagram (UDP) socket for message passing.

Parent Class: Object

Methods:

+   - `void close();`
+     Close the socket.
+   - `void connect(InetAddress addr, int port);`
+     Connect peers for implicit sending.
+   - `void disconnect();`
+     Disconnect connected peers.
+   - `InetAddress getInetAddress();`
+     Get the host address of the peer.
+   - `InetAddress getLocalAddress();`
+     Get the local address the socket is connected to.
+   - `int getLocalPort();`
+     Get the local port.
+   - `int getPort();`
+     Get the peer's port number.
+   - `int getReceiveBufferSize();`
+     Get/set receive buffer's size.
+   - `void setReceiveBufferSize(int size);`
+   - `int getSendBufferSize();`
+     Get/set send buffer's size.
+   - `void setSendBufferSize(int size);`
+   - `int getSoTimeout();`
+     Get/set the timeout for I/O.
+   - `void setSoTimeout(int timeout);`
+     If enabled, reading the pipe aborts after specified time.
+   - `void receive(DatagramPacket p);`
+     Receive message.
+   - `void send(DatagramPacket p);`
+     Send message.

Exceptions Thrown:
IOException
SocketException

# java.net.MulticastSocket (Class)

Constructor:
MulticastSocket();
MulticastSocket(int port);