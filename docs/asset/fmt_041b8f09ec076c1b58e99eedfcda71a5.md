
## 注释

- 每个子进程向其管道的写端写入一个小字符串，然后休眠一小段时间，以免过快地占满屏幕。
- 父进程使用 `select()` 调用来查询标准输入和每个子进程管道的读端。用户可以在键盘上输入字符串，父进程将检测到标准输入已就绪。在 `while` 循环中，每个描述符都会被测试，如果它被设置，就可以执行 `read()`，因为输入正在等待。这样，父进程永远不会阻塞任何正在等待其消息被读取的子进程。

在介绍套接字之后，还会有另一个更有趣的 `select()` 用法。

### 8.7 小结

相关进程可以使用匿名管道交换数据。运行在同一主机上的无关进程可以使用命名管道交换数据。与匿名管道不同，命名管道是文件系统中的实体。只要写入的数据量不超过 `PIPE_BUF` 字节，内核就保证命名管道和匿名管道的读写都是原子的。

服务器可以是迭代式的，也可以是并发式的。并发服务器创建一个子进程来处理每个不同的客户端。迭代服务器在单个进程内处理每个客户端，在它们之间共享时间。并发服务器为客户端提供更可靠的响应时间。

当进程需要处理来自多个文件描述符的 I/O 时，可以通过 `select()` 系统调用来多路复用 I/O。这只是诸多方案中的一种，但它提供了一个相对简单的解决方案。其他替代方案包括异步 I/O 和 `poll()` 调用。

## 第9章 进程间通信，第二部分

## 涵盖的概念

Sockets
fifo, mknod, pipe, pclose, popen, select, setsid,
API: dup, dup2, fpathconf, gethostname, mkfifo, shutdown, syslog, tee.

### 9.1 Sockets

Pipes are a good segue into sockets. Sockets are used like pipes in many ways but, unlike pipes, they can be used across networks. Sockets allow unrelated processes on different computers on a network to exchange data through a channel, using ordinary `read()` and `write()` system calls. We call this remote interprocess communication. Formally, a socket is an endpoint of communication between processes. Although sockets are used primarily across networks, they can also be used on a single host in place of pipes.

#### 9.1.1 Background

The development of sockets derives from the Berkeley distributions of UNIX in the early 1980's, having first appeared in 4.2BSD. In 1987, AT&T developed a different API for remote interprocess communication in their System V Release 3 (SVR3), called the Transport Level Interface (TLI). The Transport Layer Interface was the System V answer to the BSD sockets programming interface. TLI was later standardized as XTI, the X/Open Transport Interface.

In many ways, TLI has advantages over sockets. TLI and XTI were widely used and preferred over the POSIX Sockets API. They are still supported in SVR4-derived operating systems and systems such as Solaris and Mac OS. Today, the UNIX 03 Single UNIX Specification declares POSIX Sockets as the preferred API for new transport protocols.

Because sockets can be accessed like files and work the same whether on a local machine or across a network, programming them is easier than TLI programming, which requires many more structures. For this reason we focus on sockets here. In order to understand how to use sockets, you need to know the basics of networks.

#### 9.1.2 Connections

There are two ways in which sockets can be used, corresponding roughly to the difference between making a telephone call and having an email conversation with someone. When you make a telephone call to someone, you have a conversation over a dedicated communication channel, the telephone line, and you stay connected with the person on the other end for the duration of the call. In socket parlance this is called a connection oriented model. When you have an email conversation with someone, the messages are sent to the other person across different paths, and there is no dedicated connection. In fact there is no guarantee that the messages that you send will arrive in the order you send them, and the only way for the person who receives them to know who sent them is for them to have a return address in their message header. In socket parlance this is the connection-less model.

The connection oriented model uses the Transmission Control Protocol, known as TCP. The connection-less model uses the User Datagram Protocol, or UDP. There are many important differences between TCP and UDP, or equivalently, between connection oriented and connection-less models, but we will not go into them at length here. The most important differences are that TCP provides a reliable, full-duplex, sequenced channel with flow control. (Flow control is the process of managing the rate of data transmission so that senders and receivers can operate at different speeds without loss of data or retransmissions.) UDP can be full-duplex but it is not reliable (no guarantee of packet delivery), not sequenced (packets can arrive in different order than they were sent), and has no flow control (a sender can send faster than the receiver can receive).

#### 9.1.3 Communication Basics

In order to understand how to program with sockets, you need to have a basic understanding of the important concepts that underlie their use. This includes network addresses, communication domains (not internet domains), protocol families, and socket types.

Network Addresses, Ports, and Socket Addresses

For two processes to communicate, they need to know each other's network addresses. At the level of socket programming, a network address consists of two parts: an internet (IP) address and a port number. The IP address, if 32 bits, consists of four 8-bit octets, and is expressed in the standard dot-notation as in "146.95.2.131". These 32-bit address are known as IPv4 addresses. In 1995, a 128-bit address was developed, known as IPv6. Some computers have multiple network interface cards and therefore may have multiple internet addresses. It used to be the case that internet addresses had a specific structure and were divided into address classes. That is no longer the case. They are now just flat addresses.

The kernel does not represent IP addresses as strings of octets – that would be inefficient. It uses the `in_addr_t` data type, defined in `<arpa/inet.h>`, to represent an IP address. However, we will see that there are functions to convert from one format to the other.

Each server on a machine has to have a specific port that to use. There are many analogies that we could use, but if you think of an IP address as specifying a specific company's main telephone line, then the port is like a telephone extension within the company. The server uses a specific port for its services and the clients have to know the port number in order to contact the server. A port is a 16-bit integer.

Certain port numbers are well-known and reserved by particular applications and services. For example, port 7 is for echo servers, 13 for daytime servers, 22 for SSH, 25 for SMTP, and 80 for HTTP. Port numbers from 1 to 1023 are the well-known ports. To see a list of the port numbers in use, take a look at the file `/etc/services`.

Ports 1024 through 49151 are registered ports. These numbers are not controlled and a service can use one if it is not already in use.

Ports 49152 through 65536 cannot be used. They are called ephemeral ports, which are assigned automatically by TCP or UDP for client use.

`lsof` 命令可用于查看当前打开的端口。实际上，该命令的功能更为通用——它可以用来查看所有打开的文件。要查看打开的端口列表，可以使用

```
