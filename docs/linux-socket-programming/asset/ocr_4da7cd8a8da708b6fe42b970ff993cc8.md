From this point on, your socket gets messages sent to the 224.0.0.1:16900 and 228.58.120.11:16900 addresses. Like other datagrams, the program can take each message and respond directly to the sender, or the program can reply to the group.

You don't have to join a group to send messages. Because the multicast socket is still a UDP socket, you can send messages to the group without actually joining the group. To receive multicast messages, however, the socket must join the group.

# NOTE

Objects and Planning for the Future

IPv6 supports a UDP-based multicast and intends to support a TCP-based multicast. This extension removes the unreliability of the UDP protocol. But because the MulticastSocket derives from DatagramSocket, the current hierarchy cannot support the IPv6 plans for reliable datagrams. This design is a good example of not planning for the future. When you design and write any object framework, try to look ahead a little. Leaving a few places that need to be upgraded or extended is easier than fixing a hierarchy. MulticastSocket cannot support a IPv6 T/TCP socket simply because it inherits from a datagram.

Listing 12.5 gives you an example of how to create and configure a multicast socket.

# Example 12.5. Create a Multicast Socket and Assign Port #16900 to It, Join Group, and Wait for Messages

```
```
/*************************************************************************
 // SimpleMulticastDestination excerpt
/*———————————————————————————————*/
MulticastSocket ms = new MulticastSocket(16900);  // New socket
ms.joinGroup(InetAddress.getByName("224.0.0.1")); // Join group
String msg;
do
{
    byte[] line = new byte[100];
    DatagramPacket pkt = new DatagramPacket(line, line.length);
    ms.receive(pkt);
    msg = new String(pkt.getData());
    System.out.println("From "+pkt.getAddress()+":"+msg.trim());
}while (!msg.trim().equals("close"));
ms.close();                // Close connection
```
```

Listing 12.5 creates a socket for multicasting and requests a port through which it can get the packets. After joining the 224.0.0.1 (local host) group, it creates a packet for incoming packets.

# Connecting Through I/O

Up to this point, the examples use very simple and often clumsy I/O interfaces. The power of Java's sockets is in its capability to connect through different I/O classes. Java has several classes that offer different forms of reading and writing data.

This section classifies and shows you how to use the I/O classes you may want to use with sockets. The coverage is not exhaustive because the I/O package has a lot of features. If you would like to know more, you may want to pick up other Macmillan books on Java (such as Pure Java 2 by Kenneth Litzak or Java Programming on Linux by Nathan Meyers).