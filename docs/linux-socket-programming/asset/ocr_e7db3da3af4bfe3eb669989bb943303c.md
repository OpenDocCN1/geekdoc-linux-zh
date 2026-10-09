```
```
channel->CloseInput();          // Close input channel
HostAddress peer(strings[2]);   // Define peer addr
TextMessage msg(1024);          // Create msg space
do
{
    char line[100];
    fgets(line, sizeof(line), stdin); // Read line
    msg = line;                 // Place in message
    channel->Send(peer, msg);   // Ship it.
}while ( !done );
delete channel;
```
```

The implementation for `receiver()` looks a lot like the `SocketServer`'s `Echoer` call.

If you want to use multitasking with the framework, you need to remember a couple of rules:

+   * **Follow Rules**— Review the notes and advice in [Chapter 7, "Dividing the Load: Multitasking."](http://#) In particular, be sure to capture the child-termination signals. Also, threads share their I/O channels; closing one end closes it for all threads.
* **Memory Sharing**— Be aware that memory resource contention is an almost intractable problem. Share as little as possible.
* **C++ Limitations**— Employing multithreading in C++ is hazardous. So much is going on behind the scenes that you must be very careful what thread owns what data. Creating objects on the stack before firing a new thread can cause unpredictable results.

Multitasking has its advantages, and you can still use C++, but be very careful.

# ## Implementation Limitations

The framework is just a functional—but incomplete—example of how you could implement sockets in a C++ library. This should give you a few ideas of how to adapt it (or write your own) to meet your programming needs.

As it stands, you can create client, server, datagrams, and multicast/broadcast sockets. It allows you to configure the sockets using socket options. It includes a messaging abstraction so that you can write your own message formats. The following sections list a couple of ideas for feature enrichment.

# ## Sending Unknown/Undefined Messages

The current framework lets you derive your own message type from `Message`. This is very handy if you work exclusively with the `Message` component or have known types. However, you may not have the flexibility to solely derive from a single class—especially if you are integrating a legacy system.

Multiple inheritance is sometimes a necessary evil, particularly when you are trying to merge different and often conflicting frameworks. Java has the advantage of interfaces, but that does not seem like an option for C++ in the near future.

Likewise, you do not always know the data itself. This often happens when you have a newer client interfacing with a legacy server. The server does not know what extensions the client may support, so the performance can suffer. Writing an abstract messaging protocol would solve this problem.