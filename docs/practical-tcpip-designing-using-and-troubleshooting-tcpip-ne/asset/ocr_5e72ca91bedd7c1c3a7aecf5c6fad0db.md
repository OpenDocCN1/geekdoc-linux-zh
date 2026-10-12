+   • UDP *is connection-less*. The client doesn't establish a connection to the server before it sends its data – it just sends the data straight away

+   • UDP is “unreliable” in the formal network sense:

+   - packets can get lost. UDP itself can't detect this, so …

+   - the application program – client or server – (as opposed to the TCP/IP stack itself) has to detect lost packets and handle retransmission, etc. Applications often just wait until a timeout elapses, and then try again

+   - packets can get corrupted. UDP packets contain a checksum of all the data in the packet. This lets UDP detect when a packet has been corrupted. If this happens, the packet is dropped, and as usual it's the application that has to detect this and retransmit as necessary.
+   This checksum operation can be switched off, and some applications do this for performance reasons. However, as this means either that corrupted packets aren't detected, or the application layer must perform its own data integrity checks, it's a false economy.

A less derogatory term than “unreliable” is “best effort.” UDP does its best to deliver the packets but delivery is not guaranteed.

+   • because UDP is datagram-oriented and at the protocol level each packet stands alone, it has no concept of out-of-order packets, which in turn means it doesn't need sequence numbers on packets

+   • since it was first developed, TCP has been enhanced with very sophisticated mechanisms for controlling the rate of flow over its connections, to avoid congestion and excessive packet loss. Because UDP only sends single, stand-alone packets, it doesn't need any of the elaborate control mechanisms. That makes it easier and smaller (in terms of lines of code, and memory) to implement, but also makes it unsuitable for transferring large amounts of data.

If an application is implemented using UDP instead of TCP, the application itself must provide lost-packet detection, retries, etc.

UDP inherits its connection-less and unreliability properties from IP. You can think of UDP as a very thin transport layer placed above IP to give applications access to IP's basic networking facilities, without adding very much extra functionality other than ports and checksums. (By contrast, TCP is also a transport layer but it does very much more than basic IP packet communication.)

In the next module we explain why some applications use UDP, in spite of its apparent deficiencies.