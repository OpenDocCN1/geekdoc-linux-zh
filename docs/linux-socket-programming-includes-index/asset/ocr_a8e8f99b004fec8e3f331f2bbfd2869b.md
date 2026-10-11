# Transaction TCP (T/TCP): A Connectionless TCP

The TCP three-way handshaking, as compared to the UDP protocol, requires up to 10 setup packets. This slow startup is very costly when the requester needs only a single transaction. During the startup process, the two ends of the connection verify each other's services and channel reliability. Similarly, the shutdown process requires an additional handshake (refer to Chapter 3).

TCPv3 [RFC1644] adds a new feature that provides some of the connection speed of UDP while retaining the reliability of TCP. Transaction TCP (T/TCP) does the connection, transmission, and shutdown all in one single sendto() system call. How does it do this?

TCP establishes your connections using the three-way handshake, and it closes or shuts down the connection using a particular handshake. These steps are necessary to ensure that the client and server get all sent data in the proper order. To meet that goal, the TCP packet has to use flags to indicate when to establish connection (SYN, acknowledge data (ACK), and close the channel (FIN).

Chapter 3 describes the format of the TCP packet. The packet header includes several fields that may appear to be mutually exclusive. For example, it has separate flags for SYN, ACK, and FIN. Why do you want to waste the precious space of the packet when only one bit of each field is likely to be active at the same time?

T/TCP uses these fields simultaneously. When the T/TCP client connects, it sends the message to the server while requesting the connection (SYN). It also sets the FIN flag to close the connection as soon as the server completes the transaction. See Figure 4.1.

The server replies with its own connection request, a close request, and an acknowledgment of the client's close. (The connection request acknowledgment is implied.) This section includes the data that the server generated. Lastly, the client acknowledges the server's close.

T/TCP can be very fast. There is one problem: All the information must be transmitted within TCP's MSS (Maximum Segment Size), which is only 540 bytes. However, we can change that setting up to 64KB. Also, the program is not limited to sending one message; it can send several messages.

The server program does not have to do any more work to support T/TCP. The algorithm for a normal TCP connection serves T/TCP as well, because all the server-side support is programmed in the network subsystem. All the work is on the client side. You may use the following algorithm in the client:

```
/********** ************* ************* ************* *************/
/*** T/TCP basic algorithm. **** ****
/******* ********* ************* ************* **************
int flag=1;
```

![](bbox=[0.88, 0.66, 0.97, 0.77])