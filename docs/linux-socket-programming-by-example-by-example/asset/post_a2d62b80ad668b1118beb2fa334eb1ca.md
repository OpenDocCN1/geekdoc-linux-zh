
## Leaving Out bind(2) in Client Programs

Some observant readers might have noticed that no call to bind(2) was made in the client program for the socket that was created in Listing 6.2. If the bind(2) function call can be eliminated, then why bother with it at all?

You'll remember that in Chapter 5, "Binding Addresses to a Socket," there was a section titled "Interfaces and Addressing" which explained that the bind(2) function could be used to restrict the interfaces that would be used to perform communications. The example used in Figure 5.1 was a firewall application program that only wished to communicate with a trusted internal network. If this seems vague to you right now, you might want to turn back there and review how bind(2) accomplished this.

In Listing 6.2, the call to bind(2) was omitted. So what does this omission imply for the sending socket? As you know from Chapter 5, this actually indicates that the program will accept any outgoing interface, as required by the routing of the datagram to its destination. In effect, the socket is said to have a wild socket address. Later, when the program waits for a response, it will accept an input datagram from any incoming interface as well. Note also that this socket's port number is also wild. In this particular application, any client port number is acceptable.

You can explicitly request a wild address and port with a call to bind(2). Listing 5.6 showed you how this was done by using the wild address INADDR_NONE. To request a wild port number, the port number is given as zero. By combining INADDR_NONE for the IP number and a port number of zero, you have requested that bind(2) give you the same wild address explicitly that you would have used without a call to bind(2).

## Replying to a Wild Address

If the client program's address and port number are wild, you might wonder how the server was able to reply to that particular socket. After all, how do you write a response back to the client without a specific IP address and UDP port number?

The answer to this question lies in the fact that an IP number and port number are assigned at the time the datagram is sent. The previous session shown occurred on the host with an IP number of 192.168.0.2. When the client program called the sendto(2) function, the datagram was known to be destined for host IP number 192.168.0.1. The routing tables indicated that the Ethernet interface with IP number 192.168.0.2 would be used to send the datagram to that host. Consequently, the sending datagram had a “from” address of 192.168.0.2. This was the address seen at the server end. The port number, however, was wild and would have been chosen as any one of the free port numbers for the IP number chosen.

If another datagram is destined to a different network, then its "from" IP number will be different again. The "from" address will reflect the IP number of the network interface used to send the datagram.

This is an important concept to grasp and is perhaps one of the most difficult things for the beginner to grapple with. If your understanding is not yet complete on this, you should review Chapter 5 until you have a thorough understanding. As an exercise, you can add the following printf(3) statement to the server in Listing 6.1, immediately after the recvfrom(2) function call (after line 107):

![](img/961a0296fe36074690a9847b79332eff_172_0.png)

```
printf("Client from %s port %u;\n\n", inet_ntoa(addr_clnt.sin_addr), (unsigned)ntohs(addr_clnt.sin_port));
```

With this line added, perform the following steps:

- 1. Kill or take down the existing server(s) if it (they) are still running.
- 2. Recompile the server _dgramsrv_.
- 3. Restart the server (on 192.168.0.1, for example).
- 4. Run the client program again (from 192.168.0.2, for example).

The following line was displayed when the client on 192.168.0.2 sent the server on 192.168.0.1 a datagram:

![](img/961a0296fe36074690a9847b79332eff_172_1.png)

```
Client from 192.168.0.2 port 1026;
```

This confirms the fact that an IP number was assigned at the client end, and the port number assigned was 1026 in this example. This information enabled the server to direct its response back to the original requesting client.

If you lack a network, you can still perform this experiment on your standalone PC. First, start the server, using its default address:

![](img/961a0296fe36074690a9847b79332eff_172_2.png)

```
$ ./dgramsrv &
```

Now run your client program:

```
$ ./dgramclnt
```

The output of your server program and client program will mix if run from the same terminal window (you can, however, run them from separate windows if you like). The following session shows the server and client output, when they are run on a single standalone PC, within the same terminal window.

![](img/961a0296fe36074690a9847b79332eff_172_3.png)

```
$ ./dgramsrv &
[1] 733
$ ./dgramclnt

Enter format string: %D
Client from 127.0.0.1 port 1027;
Result from 127.0.0.1 port 9090 :
'08/15/99'

Enter format string: %A %D
Client from 127.0.0.1 port 1027;
Result from 127.0.0.1 port 9090 :
'Sunday 08/15/99'

Enter format string: QUIT
Client from 127.0.0.1 port 1027;

[1]+  Done        ./dgramsrv
$  
```

*Note: The IP address `127.0.0.23` in the OCR text was corrected to `127.0.0.1` as it is the standard loopback address and `.23` is likely an OCR error for `.1`.*

Notice that for all datagrams sent to the server, the datagram from address was reported as

```
Client from 127.0.0.1 port 1027;  
```

Again, this confirms that the correct IP address and a final port number are assigned upon demand, whenever bind(2) is not used on the client's sending socket.

## What's Next

This chapter introduced you to the concept of connectionless- and connection-oriented communication. The UDP protocol was used to explore and demonstrate this connectionless mode of communication.

You have demonstrated your ability to write a client and server program using the UDP network protocol. Don't stop here, however, because UDP isn't always the best choice for applications.

The next chapter will show you another mode of communication for client and server. There you will learn about the connection mode of communication using a TCP/IP client program. So, hang onto your red hat!

# Connection-Oriented Protocols for Clients

You'll recall from the last chapter that there are two basic modes of communication for sockets. They are connection and connectionless modes of communication. In the last chapter, you also saw how the UDP protocol could be used to communicate in a connectionless fashion. In this chapter, you'll put the TCP/IP protocol to use, using a connection-oriented form of communication.

This chapter will introduce you to

- The advantages of connection-oriented protocols
- The /etc/services file and its support routines
- The /etc/protocols file and its support routines
- The connect(2) function
- How to write a TCP/IP client program

Before you jump in and write your first client program, however, a quick review and an introduction to connection-oriented communications is in order. Additionally, you'll learn about some of the support functions that are often used by TCP/IP programs that locate service and protocol information.

It was also noted in the last chapter that connectionless-oriented communication is simpler and more flexible. But you'll see that connection-oriented communication is not really that much more difficult. It does require additional steps, however, and mostly on the server side. A connection is also much more rigid, because after the connection has been established, the socket can only communicate with the connected endpoint.

The selling point in favor of TCP/IP for most application writers is that the communication channel is transparently reliable and that data is delivered in the proper sequence. After the connection has been established, your application can read and write to the socket without worrying about any of the following problems:

- Lost packets
- Timeouts and retransmissions
- Duplicated packets
- Packets received out of sequence
- Flow control

Like opening a file, your program can

1. Establish a TCP/IP connection with a remote socket
2. Transmit large amounts of data
3. Close the socket

These simple steps are all that is necessary to deliver all of your data safely to the remote end. Proven error recovery software will take care of retransmitting lost packets until they can be successfully delivered to the remote host.

## TCP/IP Handles Lost Packets

TCP/IP will notice when packets are lost. This does not always happen with UDP. When packet errors are reported, the TCP/IP protocol can immediately respond with retransmissions. However, if an acknowledgement is missing, causing a timeout, the TCP/IP protocol takes steps to ensure that the data is retransmitted to its destination. Carefully crafted algorithms are used to make the transmission of the data nimble, without taxing the network capacity with retransmitted data.
