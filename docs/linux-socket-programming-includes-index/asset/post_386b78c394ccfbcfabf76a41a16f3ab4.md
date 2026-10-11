
- ***Streaming***—The packaging and unpackaging of data requires knowledge about the data and the ability to cast data types. Identification of unknown structures is not possible because the methods would not be shipped along with the data.
- ***Overloading***—Not available.
- ***Interfaces***—You can use implicit interfaces, but that only assumes a dynamic-loading environment. This is not likely to be available.
- ***Events and Exceptions***—You can simulate some event programming and exception catching, but you would need to use an inter-function jump (such as C's `setjmp()`) to duplicate it. This is not a good idea.

You are not left out of the object programming loop. The good practices listed here can help you in whatever condition you work.

### Summary: Object-Oriented Thinking

Object technology stands on top of a lot of good research and innovation in programming. The foundation of objects (abstraction, polymorphism, inheritance, and encapsulation) helps the programmer design and write good solid programs that others can leverage or reuse. The features define the parts of how object technology implements part of the foundation, and the extensions let the programmer grow into other capabilities.

When used carefully and with discipline, the result of object-oriented analysis and design is easier to reuse. It is also easier to maintain and extend than conventional programming. Lastly, it lets the programmer focus more on the problem than on the programming.

## Using Java’s Networking API

### CHAPTER 12

### IN THIS CHAPTER

- Exploring Different Java Sockets 264
- Connecting Through I/O 272
- Configuring the Java Socket 275
- Multitasking the Programs 276
- Implementation Limitations 280
- Summary: Java-Style Network Programming 280

Up to this point, the book has covered sockets and network programming in C. The advantages of C-style programming is very clear to operating systems designers— the power without overhead is a real bonus. However, it does not always result in reusable or portable programs.

Alternatively, you could use an object-enabled language and create a set of reusable tools. Java is a great example of excellent reuse and even portability. The whole foundation of Java is to provide two levels of portability—source level and code level. Source-level portability means that all programs must be able to compile on any platform. (You may note that Sun Microsystems reserves the right to expire or *deprecate* certain interfaces, methods, or classes.) This is very powerful because you can reuse code on any platform that supports Java.

Code-level portability is not really new. The idea “Compile once, run everywhere” is easy to implement with the right tools. Java compiles to a byte code on which a virtual machine runs. The Java Virtual Machine (JVM) executes each command sequentially, acting somewhat like a microprocessor. Of course, interpreting the byte code cannot ever approximate the speed of native machine language (which C compiles into), but because of the speed of modern microprocessors, the performance degradation is less noticeable.

Java is a very powerful, simple, and fun language. If you know how to program in C/C++ and understand Object Technology, you’ve got a good start in programming in Java. The libraries in Java are expansive, covering many, many operations. You can easily get lost in all the available classes. Even if you learn Java and become thoroughly familiar with the class libraries, you may probably keep the Java Developers Kit (JDK) documents and a few printed references close at hand.

The last chapter introduced the purpose of Object Technology and how to design using it. This chapter covers one socket implementation in Java; the next chapter defines a custom C++ socket framework. Because a topic on Java is so vast, the topics in this chapter primarily assume that you already know Java and want to move into network programming. Likewise, some of the examples on the companion Web site contain Abstract Windowing Toolkit (AWT) program code—discussing GUIs and events is beyond the scope of this chapter.

The following sections discuss the classes that Java offers for sockets, relevant I/O, and threading. This chapter also discusses some of the newer methods that support socket configuration (as found in Chapter 9, “Breaking Performance Barriers”).

### Exploring Different Java Sockets

Like C, Java offers ways to access the Internet. In fact, some programmers say that the true benefits of Java arise from GUI independence and the inherent network programming. Java offers a few Internet protocols for your use, these primarily being TCP and UDP.

The Java-preferred networking channel is the TCP channel. It, as noted in the first part of the book, has the most reliability. Also, it’s easier to use than the datagram-style of communication. Java still offers a UDP connection, but the I/O library does not offer any direct support for it.

### Programming Clients and Servers

Streaming (or TCP) channels match Java’s interface the best. Java tries to abstract the details and simplify interfaces. You can easily understand the decisions behind placing support for TCP in the I/O library. Java’s approach to creating sockets really reduces the steps to a couple of objects and methods.

#### Java TCP Clients

For example, if you want a client socket, you just create it:

```java
Socket s = new Socket(String Hostname, int PortNum);
Socket s = new Socket(InetAddress Addr, int PortNum);
```

A common implementation may look like the following:

```java
Socket s = new Socket("localhost", 9999);
```

That’s it. You don’t have to do anything else to connect to a server. When the JVM creates the object, it assigns a local port number, does the network-byte order conversion, and connects to the server. You can even specify which local network interface and port to use with the following extensions:

```java
Socket s = new Socket(String Hostname, int PortNum,
                      InetAddress localAddr, int localPort);
Socket s = new Socket(InetAddress Addr, int PortNum,
                      InetAddress localAddr, int localPort);
```

The InetAddress class converts the hostname or IP address into the binary address. Most of the time, you won’t use the InetAddress object directly in the call unless you begin with it. Instead, the constructor that passes Hostname is a more common use. Most programs connect using the information a user provides to the program. This typically is by hostname or IP address.

#### Java’s IPv4/IPv6 Support

Java currently and directly supports IPv4 and, according to project Merlin (see java.sun.com), IPv6 support should be available when the operating system supports it. Classes like InetAddress, which manages the names and conversion, should easily adapt to other protocols. Be aware, however, that the version you have may not support it yet. Some interfaces, such as InetAddress.getAddresses(), need to change to support the extended address and new format.

### Sending/Receiving Messages

After creating the socket, the program cannot directly send or receive data through this class, however. You must get the InputStream or OutputStream from the class instance:

```java
InputStream i = s.getInputStream();
OutputStream o = s.getOutputStream();
```

Using these methods, you can read or write arrays of bytes:

```java
byte[] buffer = new byte[1024];
int bytes_read = i.read(buffer);  //--Read block from socket
o.write(buffer);  //--Transmit byte array through socket
```

You can even use InputStream to determine if data is waiting in the kernel’s buffers with InputStream.available(). This method returns the number of bytes that the program can read without blocking.

```java
if (i.available() > 100 )//--Don't read unless 100 bytes await
    bytes = i.read(buffer);
```

When you are done, you can close the socket (and all the I/O channels as well) with a single call to Socket.close():

```java
//--Clean up
s.close();
```

### Manual Versus Garbage Collection

Java uses new for all calls. The JVM passes everything (except scalars) as pointers, and the pointers are never exposed to your program. Everything must point to some data or null. The JVM calls a garbage collection process when resources begin to get scarce. All loose memory references during this process file back into the available pool. This means that you never have to release any of the memory you allocate. However, this does not apply to sockets. You must manually close all sockets. If the program does not close a dependent socket, the program may run out of available file descriptors eventually. The resulting program behavior may not be entirely predictable.

With these calls and objects, you can create an echo client as shown in Listing 12.1.

**LISTING 12.1** An Example of a Simple Echo Client in Java

```
//*******************************
// SimpleEchoClient  excerpt
```
