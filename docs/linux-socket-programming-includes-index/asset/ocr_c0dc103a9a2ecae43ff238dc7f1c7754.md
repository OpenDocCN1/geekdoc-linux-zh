# Sending to Multiple Destinations

The datagram protocol lets you send a single message to an unconnected destination. An advantage to datagrams is being able to send to several destinations at once using broadcasting and multicasting. Chapter 15, “Network Encapsulation with Remote Procedure Calls (RPCs),” discusses in detail both of these methods of sending messages.

# Current Java-Multicasting Support

At the time of this writing, the multicasting socket options are not working correctly. This support should be fixed soon. This was tested on the 1.3 beta version for WinNT and Linux.

Java offers multicasting in its networking wrapper, but it excludes broadcasting. Multicasting lets a program join a special IP address reserved for multicasting groups. Every program in this group gets messages sent to the address. To create a `MulticastSocket`, you can use one of two constructors:

```
MulticastSocket ms = new MulticastSocket();
MulticastSocket ms = new MulticastSocket(int localPort);
```

Even though you can create a multicast socket with no specified port, your program must select a port before you can expect any messages. The reason is that all multicast datagrams use the port to filter out unwanted messages.

After you have created the socket, it acts just like a `DatagramSocket`. That is, you can send and receive directed messages. To get the extended multicast functionality, you need to join a group. IPv4 has set aside a range of legal multicasting addresses: **224.0.0.0**~**239.255.255.255**.

```
MulticastSocket ms = new MulticastSocket(16900);
ms.joinGroup(InetAddress.getByName("224.0.0.1"));
ms.joinGroup(InetAddress.getByName("228.58.120.11"));
```

From this point on, your socket gets messages sent to the **224.0.0.1:16900** and **228.58.120.11:16900** addresses. Like other datagrams, the program can take each message and respond directly to the sender, or the program can reply to the group.

You don’t have to join a group to send messages. Because the multicast socket is still a UDP socket, you can send messages to the group without actually joining the group. To receive multicast messages, however, the socket must join the group.

12  USING JAVA’S NETWORKING API