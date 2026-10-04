
# Book VIII

# Internet Servers

The 5th Wave By Rich Tennant

![](img/d9230b719dc0efd80851f363d8c6f571_621_0.png)

"I'm sorry, but 'Arf', 'Bark', and 'Woof' are already registered domain names. How about 'Oink', 'Quack', or 'Moo'?"

# Contents at a Glance

- Chapter 1: Managing the Servers ................................................597
- Chapter 2: Running the Apache Web Server..................................................615
- Chapter 3: Setting Up the FTP Server ...................................................639
- Chapter 4: Serving Up Mail and News ................................................647
- Chapter 5: Setting Up DNS..................................................................675
- Chapter 6: Running Samba and NFS ................................................695

## Chapter 1: Managing the Servers

## In This Chapter

- Understanding Internet services
- Controlling servers through xinetd
- Using chkconfig to manage servers
- Using the service-configuration utility

The Internet is a world of clients and servers. Clients make requests to servers, and servers respond to the requests. For example, your Web browser is a client that downloads information from Web servers and displays it to you. Of course, the clients and servers are computer programs that run on a wide variety of computers. A Fedora Core system is an ideal system to run a wide variety of servers from a Windows server to a print server. In this chapter, I provide an overview of a typical Internet service, its client/server architecture, and how to manage the servers in Fedora Core. You can use the information in this chapter to manage any server running on your Fedora Core system.

## Understanding Internet Services

Internet services are network applications designed to deliver information from one system to another. By design, each Internet service is implemented in two parts — a server that provides information, and one or more clients that request information.

Such client/server architecture is the most common way to build distributed information systems. The clients and servers communicate through the network. The neat part is that you can be running a client at your desktop computer and access information from a server running on a computer anywhere in the world (as long as it's on the Internet).

The Web, e-mail, and FTP (File Transfer Protocol) are examples of Internet services that use the client/server model. For example, when you use the Web, you use the Web-browser client to download and view Web pages from the Web server.

### 598 Understanding Internet Services

![](img/d9230b719dc0efd80851f363d8c6f571_624_0.png)

Client/server architecture requires clients to communicate with the servers. That's where the Transmission Control Protocol/Internet Protocol — TCP/IP — comes in. TCP/IP provides a standard way for clients and servers to exchange packets data. In the next sections, I explain how TCP/IP-based services communicate.

### TCP/IP and sockets

Client/server applications such as the Web and FTP use TCP/IP for data transfers between client and server. Internet applications typically use TCP/IP communications using Berkeley sockets (so named because the socket interface was introduced in Berkeley around 1982). The sockets interface is nothing physical — it's simply some code that a computer programmer can use to create applications that communicate with other applications on the Internet.

![](img/d9230b719dc0efd80851f363d8c6f571_624_1.png)

Even if you don't write network applications using sockets, you may have to use them. Knowledge of sockets can help you understand how network-based applications work, which in turn helps you find and correct any problems.

### Socket definition

Network applications use sockets to communicate over a network. A socket represents one end of a connection. Because a socket is bidirectional, data can be sent as well as received through it. A socket has three attributes:

- The network address (IP address) of the system
- The port number, identifying the process running on the computer
- The type of socket, identifying the protocol for data exchange

Essentially, the IP address identifies a computer (host) on the network; the port number identifies a process (server); and the socket type determines the manner in which data is exchanged — connection-oriented (stream) or connectionless (datagram).

### Connection-oriented protocols

The socket type indicates the protocol being used to communicate through the socket. A connection-oriented protocol works like a normal phone conversation. When you want to talk to your friend, you have to dial your friend's number and establish a connection. In the same way, connection-oriented data exchange requires both the sending and receiving processes to establish a connection before data exchange can begin.

### 599 Understanding Internet Services

In the TCP/IP protocol suite, TCP — Transmission Control Protocol — supports connection-oriented data transfer between two processes running on two computers on the Internet. TCP provides reliable two-way data exchange between processes.

As the name TCP/IP suggests, TCP relies on IP — Internet Protocol — for delivery of packets. IP does not guarantee delivery of packets nor does it deliver packets in any particular sequence. IP efficiently moves packets from one network to another. TCP is responsible for arranging the packets in the proper sequence, detecting whether errors have occurred, and requesting retransmission of packets in case of an error.

TCP is useful for applications intended to exchange large amounts of data at a time. In addition, applications that need reliable exchange use TCP (for example, FTP uses TCP to transfer files). In the sockets model, a socket that uses TCP is referred to as a stream socket.

### Connectionless protocols

A connectionless data-exchange protocol does not require the sender and receiver to establish a connection. It's like shouting to your friend in a crowded room — you can't be sure that your friend hears you.

In the TCP/IP protocol suite, the Datagram Protocol (UDP) provides connectionless service for sending and receiving packets known as datagrams. Unlike TCP, UDP does not guarantee that datagrams reach their intended destination. UDP ensures that datagrams are delivered in the order they are sent.

UDP is used by applications that exchange small amounts of data at a time, and by applications that don't need reliability and sequencing of data delivery. For example, SNMP (Simple Network Management Protocol) uses UDP to transfer data. In the sockets model, a socket that uses UDP is referred to as a datagram socket.

### Sockets and the client/server model

Two sockets are needed to complete a communication path. When two processes communicate, they use the client/server model to establish the connection. Figure 1-1 illustrates the concept. The server application listens on a specific port on the system — the server is completely identified by the IP address of the system where it runs and the port number where it listens for connections. The client initiates a connection from any available port and tries to connect to the server (identified by the IP address and port number). When the connection is established, the client and the server can exchange data according to their own protocol.

### 600 Understanding Internet Services

Figure 1-1: Client and server processes use two sockets to communicate.

![](img/d9230b719dc0efd80851f363d8c6f571_626_0.png)

The sequence of events in socket-based data exchanges depends on whether the transfer is connection-oriented (TCP) or connectionless (UDP).

For a connection-oriented data transfer using sockets, the server “listens” on a specific port, waiting for clients to request connection. Data transfer begins after a connection is established.

For connectionless transfers, the server waits for a datagram to arrive at a specified port. The client does not wait to establish a connection; it simply sends a datagram to the server.

Regardless of whether it is a server or a client, each application first creates a socket. Then it associates (binds) the socket with the local computer’s IP address and a port number. The IP address identifies the machine (where the application is running), and the port number identifies the application using the socket.

> REMEMBER Servers typically listen to a well-known port number so clients can connect to that port on the server. For a client, the process of binding a socket to the IP address and port is the same as for a server, but the client can use 0 as the port number — the sockets library automatically uses an unused port number for the client.

> For a connection-oriented stream socket, the communicating client and server applications have to establish a connection. The exact steps for establishing a connection depend on whether the application is a server or a client.

> REMEMBER In the client/server model, the server has to be up and running before the client can run. After creating a socket and binding the socket to a port, the server application sets up a queue of connections, which determines how many clients can connect to the server. Typically, a server listens to anywhere
