# SocketClient (Class)

Constructor:
SocketClient(ENetwork Network=eIPv4);
SocketClient(HostAddress& Host, ENetwork Network=eIPv4); //auto-connect

General Description: TCP client.

Parent Class: SocketStream

Method:

void Connect(HostAddress& Addr); Connect to host at Addr.

Exception Thrown:
NetConnectException

# Datagram (Class)

Constructor:
Datagram(HostAddress& Me, ENetwork Network=eIPv4,
EProtocol Protocol=eDatagram);
Datagram(ENetwork Network=eIPv4, EProtocol Protocol=eDatagram);

General Description: General datagram (UDP) socket.

Parent Class: Socket

+   Methods:
+   
+   * void MinimizeDelay(bool Setting);
+   
+   Request minimal packet delay.
+   * void MaximizeThroughput(bool Setting);
+   
+   Request maximum network throughput.
+   * void MaximizeReliability(bool Setting);
+   
+   Request maximum reliability.
+   * void MinimizeCost(bool Setting);
+   
+   Request minimal cost.
+   * void PermitFragNegotion(EFrag Setting);
+   
+   Set fragmentation negotiation.

Exception Thrown:
NetConfigException

# Broadcast (Class)

Constructor:
Broadcast(HostAddress& Me);