
## The Methods of Communication

Connectionless-oriented communication, as you might have surmised, requires no connection to be established before communication begins. This is like a person with a megaphone shouting to a specific person of his choice in a crowd. With each new shout, the person sending the message can address his statement to another person without any prior agreement.

In a similar manner, after you create a connectionless socket, you will be able to send messages to any socket that is willing to receive your messages. There will be no connection establishment, and each message can be directed to a different receiving socket.

### Understanding the Advantages

Connectionless-oriented communications offer some advantages over connection-oriented protocols. Some of these include the following:

- **Simpler**—No connection to establish.
- **Flexible**—Can send messages to a different recipient with each message-sending operation.
- **Efficient**—Requires no connection establishment or tear down, which can add a significant number of overhead message packets to the network.
- **Fast**—Since there is no connection establishment or tear-down, only the message itself is sent.
- **Broadcast capability**—The capability to direct one message to many recipients.

Many of the advantages of a connectionless-oriented protocol have to do with efficiency and speed. To establish a connection requires a number of packets to be exchanged between the two endpoints before any data can be exchanged. The tear-down of an established communication channel requires that additional packets be exchanged. Again, this results in additional overhead and elapsed time.

One other advantage of a connectionless protocol is its broadcast capability. It is possible to address one message to several recipients. This makes very efficient use of the network bandwidth.

In this chapter, you will study the UDP protocol (User Datagram Protocol), which is a connectionless-oriented protocol. This protocol enjoys all of the advantages that were just presented.

### Understanding the Disadvantages of Connectionless Communications

With all of the advantages that connectionless-oriented protocols offer, you might wonder why they aren't always used. As with most things, even connectionless communication has its disadvantages.

The UDP protocol is a very simple transport-layer protocol, and it is connectionless as noted previously. In the context of the UDP protocol, there exist the following disadvantages:

- The protocol is not reliable.
- There is no sequencing of multiple datagrams.
- There are message size limitations.

The problem of reliability is the most serious limitation for most applications. The UDP datagram can be written out to the network by your application, but there is no assurance that the intended recipient will ever receive it. The message could be garbled and not received by the receiver on the same network. Alternatively, the message could be lost because one of many routers in the network path failed to receive the message without checksum errors. When a packet is received with an error, the UDP packet is quietly discarded and lost forever.

**NOTE**

A datagram is simply a unit of data that is sent and received over the network. It can be compared to a telegram in the sense that it represents one complete message.

Other problems can cause UDP packets to be lost. If the receiving host or router is unable to allocate enough buffer space to hold the UDP packet, it will be quietly discarded. It follows, then, that if your UDP packet must travel longer distances, there is a greater chance of it being dropped along the way.

Another problem must be considered before you decide to use UDP for your applications. If you send two or more datagrams to your destination in quick succession, there is a possibility that some datagrams will arrive out of sequence. The UDP protocol uses the Internet Protocol (IP) to deliver the final datagram. IP packets can be routed differently with each transmission, and routes vary according to current network conditions. This often results in some packets arriving at the destination before earlier packets. The bottom line is that UDP packets can arrive out of sequence.

Finally, there is the issue of datagram size. The theoretical maximum size of a UDP datagram is slightly less than 64KB. However, many UNIX hosts will only support a maximum near 32KB. Other UNIX kernel built-in restrictions limit the size even further. This is often as low as 8KB. Finally, the receiving socket program will restrict this to the maximum size of its receiving buffer. For this reason, some programs restrict themselves to UDP messages of 512 bytes or less.

If a large UDP packet is sent, it will have to be broken up into several smaller IP fragments and later re-assembled at the receiving end. The re-assembly process requires buffers to be allocated in order to hold the received fragments. This is only done for a given timeout period, until the entire packet can be re-assembled. Competition for buffers may cause the re-assembly to be abandoned, with the effect that your UDP packet will be quietly dropped. The UDP datagram must endure a number of perils before it successfully arrives at its destination.

For some applications, these caveats will steer you toward the more reliable connection-oriented protocols such as TCP/IP. These might not be serious limitations for other applications. Only you can decide whether UDP is appropriate for use in your application.

## Performing Input/Output of Datagrams

In the example program shown in Listing 1.3 of Chapter 1, “Introducing Sockets,” you saw the functions read(2) and write(2) being used when reading from and writing to sockets. While it was not pointed out at the time, the socketpair(2) function call shown created a pair of sockets using a connection-oriented protocol. Consequently, it was possible to use the familiar read(2) and write(2) functions to perform I/O on those sockets.

When sending and receiving datagrams, however, a different pair of functions is required. This is because each message being sent is potentially sent to a different destination address. The function used for sending a datagram must allow you to specify the address of the intended recipient. Likewise, when you receive a datagram, you need to find out whom it came from. This new function must provide you with a convenient way to determine the address of the sender.

## Introducing the sendto(2) Function

The sendto(2) function allows you to write a datagram and specify the destination address of the recipient at the same time. The function synopsis is as follows:

```c
#include <sys/types.h>
#include <sys/socket.h>

int sendto(int s,
           const void *msg,
           int len,
           unsigned flags,
           const struct sockaddr *to,
           int tolen);
```

Don't let the number of arguments intimidate you about this function. They are quite easy to understand, after they are described:

1. The first argument s is the socket number. You received this value from the socket(2) function.
2. Argument msg is a pointer to the buffer holding the datagram message that you wish to send.
3. Argument len is the length, in bytes, of the datagram that starts at the pointer given by msg.
4. The flags argument allows you to specify some option bits. In many cases, you will simply supply a value of zero.
5. The argument to is a pointer to a generic socket address that you have established. This is the address of the recipient of the datagram.
6. Argument tolen is the length of the address argument to.

The value returned by the function sendto(2), when successful, is the number of bytes sent (note that this is no guarantee that they were received at the remote end.) When an error occurs, the function returns a value of -1 and the value errno can be consulted to find out why.

The second-to-last function argument allows you to identify where the datagram must be sent. The argument to must point to a valid socket address, and the argument tolen should contain the correct length of the address. You have become an expert at forming addresses in the preceding chapters, so you should feel right at home here.

Table 6.1 lists the values that the flags argument can have, though most of the time you will simply supply the value zero instead.

### Table 6.1: The flags Values for the sendto(2) Function

| Flag | Hexadecimal | Meaning |
| :--- | :--- | :--- |
| 0 | 0x0000 | Normal—no special options |
| MSG_OOB | 0x0001 | Processes out-of-band data |
| MSG_DONTROUTE | 0x0004 | Bypasses routing; uses direct interface |
| MSG_DONTWAIT | 0x0040 | Does not block; waiting to write |
| MSG_NOSIGNAL | 0x4000 | Does not raise SIGPIPE when the other end has disconnected |
