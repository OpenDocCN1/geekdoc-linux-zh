```
_exit(), FD_CLR(), FD_ISSET(), FD_SET(), FD_ZERO(), accept(), bind(), bzero(), close(), connect(), exit(), gethostbyaddr(), gethostname(), getservbyname(), gettablesize(), htonl(), htons(), inet_addr(), inet_aton(), inet_ntoa(), inet_ntop(), inet_pt on(), listen(), memcpy(), memset(), mkfifo(), mknod(), ntohl(), ntohs(), open(), perror(), pipe(), read(), recvfrom(), sendto(), select(), shutdown(), signal(), sizeof(), socket(), strtol(), system(), wait(), wait3(), waitpid(), write()
```

# 20.1 INTRODUCTION

UNIX interprocess communication (IPC) facilities exist so that processes and threads may communicate with one another and synchronize their actions. The three functional facilities into which IPC can be divided are communication, synchronization, and signals. Communication provides functionality to exchange data between processes or threads, synchronization provides for the synchronization of processes or threads, and signals are a communication technique where the signal number itself is a form of communication information. Although some of these facilities fundamentally exist for communication and synchronization, the term IPC is used to describe them all.

The IPC facilities provide similar functionality because of the following reasons:

+   1. Similar facilities evolved on different UNIX families, and then migrated between families. For example, FIFOs were developed on System V and (stream) sockets were developed on BSD.

+   2. New facilities have been developed to make up for deficiencies of similar earlier facilities. For example, the POSIX IPC facilities (message queues, semaphores, and shared memory) were designed to improve on the older System V IPC facilities. In particular, whereas POSIX IPC is thread safe, System V IPC is not.

Some facilities, which on the surface seem similar, are actually significantly different in terms of the methods and functionality they provide. For example, stream sockets can be used to communicate over a network, while FIFOs can be used only for communication between processes on the same machine. Of all of the IPC methods, only sockets permit processes to communicate over a network. Sockets are generally used in one of two domains: that which allows communication between processes on the same system, and on the Internet, which allows communication between processes on different hosts connected via a Transmission Control Protocol/Internet Protocol (TCP/IP) network. Often, only minor changes can convert a program that uses sockets between the two domains.

Our coverage of the topic is broadly divided into three types: (a) IPC between related processes on the same computer, (b) IPC between unrelated processes on the same computer, and (c) IPC between related or unrelated processes on the same or different