# **LISTING 12.3**  Continued

```
InetAddress dest =        // Convert hostname
InetAddress.getByName("127.0.0.1");
DatagramPacket pkt =        // Create message packet
new DatagramPacket(line, len, dest, 9998);
s.send(pkt);               // Send message
s.close();                 // Close connection
```

This listing sends the message and immediately closes the socket. While seemingly an error, all sockets allow you to send anything and then close—even before the message leaves your local host. The socket's message queue stays around until all the messages are gone.

Peer-destination essentially does the same as the client, only it reads the message instead of sending it. Listing 12.4 shows simple peer destination.

# **LISTING 12.4**  Receive the Datagram Message and Display It

```
/********************
// SimplePeerDestination excerpt
//
DatagramSocket s = new DatagramSocket(9998); // Create socket
byte[] line = new byte[100];
DatagramPacket pkt =    // Create buffer for incoming message
new DatagramPacket(line, line.length);
s.receive(pkt);        // Get message
String msg = new String(pkt.getData());    // Convert data
System.out.print("Got message: "+msg);
s.close();             // Close connection
```

Java supports the datagram socket to the extent that you can create sockets and send messages, but that's about it. If you want more robust I/O capability, Java really does not offer it directly. Instead, you can use the memory I/O classes to build the messages in an array (described in the section "Classifying the I/O Classes," later in this chapter).

The advantages of sending directed messages instead of an open pipe are essentially the same advantages UDP offers. (For more details on these differences, please refer to Chapter 3, "Different Types of Internet Packets," and Chapter 4.) Java provides a simple wrapper over the datagram protocols.