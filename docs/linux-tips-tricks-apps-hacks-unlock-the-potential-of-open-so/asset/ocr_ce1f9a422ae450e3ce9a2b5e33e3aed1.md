# **Tips | Tricks | Hacks | Apps**

# # Program a client-server application

Each operating system provides its own set of networking APIs, but Qt gives a solution to simplify creating chatty applications

![](bbox=[0.09, 0.14, 0.34, 0.37])

**Modern computer networks are composed of multiple protocols.** Creating well-formed packets by hand is almost impossible – the protocol stack and its underlying network hardware affect the format.

**Engineers working on Unix** solved this problem by introducing an abstraction layer – so-called **sockets** acting as endpoints between two local or remote applications. Developers use the standardised interface in order to provide commands to the socket, which are then translated to the network.

When dealing with sockets, a basic understanding of networking is beneficial. For now, it shall suffice to define that messages can be transmitted by two high-level protocols.

**TCP** – short for Transmission Control Protocol, – provides confirmation when data has been delivered successfully. This is accomplished by a relatively complex sequence of packets which add overhead to the communication process. However, some applications don't require this. For them, **UDP** provides a sleeker communication protocol that forgoes delivery confirmation. On a network, computers are identified by their IP address. Individual services are then identified by their port numbers – consider them apartment door numbers inside a high-rise building.

**Developers working on communication software** tend to face a chicken-and-egg situation – if no server has been written, the client can't connect. On the other hand, the lack of a client means that the server can't be tested.

In practical projects you should start out by creating a rough mock-up of the messages that the client and server will exchange. You don't need to get this 100 per cent right on the first try; most protocols change as they get implemented.

Our finger exercise-level applications don't require this level of sophistication. It will suffice to begin by creating a command line project called ImagineITCPServer. Qt Creator does not add the networking module to newly created applications. This can easily be remedied by opening its .pro file and adjusting the QT directive so that network gets included at compile time.

```
QT += network
```

With that, it is time to create the server object. Its declaration can be placed inside the main() function responsible for program bring-up:

```
myServer=new QTcpServer();
if(myServer->listen(QHostAddress::Any, 1025)==false)
{
        qDebug() << "Server error" << myServer->serverError();
        return 0;
}
else
{
        qDebug() << "Server up" << myServer->serverAddress() << " ";
        myServer->serverPort();
}
```

In classic Berkeley socket programming, server and client logic are handled by instances of the socket class. Qt provides a dedicated server that contains helper methods for connectivity management. After start-up, we invoke the listen() method in order to make our QTcpServer wait for incoming connections.