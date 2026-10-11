
# Objects and Planning for the Future

IPv6 supports a UDP-based multicast and intends to support a TCP-based multicast. This extension removes the unreliability of the UDP protocol. But because the `MulticastSocket` derives from `DatagramSocket`, the current hierarchy cannot support the IPv6 plans for reliable datagrams. This design is a good example of not planning for the future. When you design and write any object framework, try to look ahead a little. Leaving a few places that need to be upgraded or extended is easier than fixing a hierarchy. `MulticastSocket` cannot support a IPv6 TCP socket simply because it inherits from a datagram.

Listing 12.5 gives you an example of how to create and configure a multicast socket.

## Listing 12.5 Create a Multicast Socket and Assign Port #16900 to It, Join Group, and Wait for Messages

```java
// SimpleMulticastDestination excerpt
//---------------------------------------------------------------------------
MulticastSocket ms = new MulticastSocket(16900); // New socket
ms.joinGroup(InetAddress.getByName("224.0.0.1")); // Join group
String msg;
do
{
    byte[] line = new byte[100];
    DatagramPacket pkt = new DatagramPacket(line, line.length());
    ms.receive(pkt);
    msg = new String(pkt.getData());
    System.out.println("From " + pkt.getAddress() + ":" + msg.trim());
}
while (!msg.trim().equals("close"));
ms.close(); // Close connection
```

Listing 12.5 creates a socket for multicasting and requests a port through which it can get the packets. After joining the 224.0.0.1 (local host) group, it creates a packet for incoming packets.

# Connecting Through I/O

Up to this point, the examples use very simple and often clumsy I/O interfaces. The power of Java’s sockets is in its capability to connect through different I/O classes. Java has several classes that offer different forms of reading and writing data.

This section classifies and shows you how to use the I/O classes you may want to use with sockets. The coverage is not exhaustive because the I/O package has a lot of features. If you would like to know more, you may want to pick up other Macmillan books on Java (such as Pure Java 2 by Kenneth Litwak or Java Programming on Linux by Nathan Meyers).

# Classifying the I/O Classes

The Java I/O package includes several classes, each defined to perform a specific task. All of them send or receive information. Unfortunately, because it has so many classes, it is difficult to know which to use and when. Perhaps the easiest way to work with them is to group them according to their several responsibilities. Then you can easily see which class is best for socket use.

The I/O package essentially offers six primary types of I/O. Each type serves a specific purpose, and all derive from Reader, Writer, InputStream, or OutputStream:

- **Memory**— I/O based on memory buffers. The package accesses no hardware devices; instead, arrays in RAM serve as virtual I/O pools. This helps in parsing strings or even creating a buffer for datagrams. Examples include ByteArrayInputStream, ByteArrayOutputStream, CharArrayReader, CharArrayWriter, StringReader, and StringWriter.

- **File**— Reading, writing, and manipulating the file system. These classes provide you ways to create, read, write, delete, or manipulate files in a file system. Examples include FileInputStream, FileOutputStream, FileReader, and FileWriter.

- **Filters**— I/O that does some character-based translation or interpretation. For example, treating a newline like an end of record, recognizing fields by tabs or commas, or converting binary values into readable numbers. Examples include FilterReader, FilterWriter, PrintWriter, and InputStream (deprecated).

- **Objects**— Sending and receiving of coding objects. This is most impressive. Java can send and receive instances without any coding on your part. In most cases, you only need to flag the class Serializable, and you can transmit and receive object instances. The classes are ObjectInputStream and ObjectOutputStream.

- **Pipes**— IPC (Inter-Process Communications) as you find in C. You create a pipe and link it with another pipe, and then two threads send each other messages. The classes are PipedInputStream, PipedOutputStream, PipedReader, and PipedWriter.

- **Stream**— Generalized buffered I/O communications. This is the form that sockets use. If you want to use the others, you need to convert the streaming class to another (see the next section). The abstract classes are InputStream and OutputStream. The basic conversion classes are InputStreamReader and OutputStreamWriter.

![](img/2591af4bdf00a0f382331fc9481f785e_292_0.png)

The package has several other classes that really don't fit in this classification. An example is SequenceInputStream, which allows you to merge two streams into one.

Of all these classes, you may want to familiarize yourself most with ObjectInputStream and ObjectOutputStream for sending and receiving custom classes or BufferedReader and PrintWriter for string I/O. Network programs often use these because they suit socket programming the best. Similarly, you can use the ByteArrayOutputStream or ByteArrayInputStream objects to provide interfaces for datagram messages.

# Converting Between I/O Classes

Some features that one class owns may not be directly available in the I/O class that the socket hands you. The Socket class only offers two I/O classes—OutputStream and InputStream. These offer pretty much bare bones reading and writing of byte arrays. To get the different features, you need to convert these classes.

Suppose you want to read in strings, not byte arrays. The BufferedReader has a good String interface. You need to convert from the InputStream abstract class to the Reader abstract class. The InputStreamReader class acts as the go-between for this conversion:

```java
Socket s = new Socket(host, port);
InputStream is = s.getInputStream();
InputStreamReader isr = new InputStreamReader(is);
BufferedReader br = new BufferedReader(isr);
String l = br.readLine();
```

You can also use the following customary shorthand:

```java
BufferedReader br = new BufferedReader(new InputStreamReader(
s.getInputStream()));
```

Sending a string (without actually converting the string) through a channel is a little easier:

```java
String msg = new String( 
"<html><body>Welcome to my Java website</body></html>");
SocketServer ss = new SocketServer(9999);
Socket s = ss.accept();
PrintWriter pw = new PrintWriter(s.getOutputStream(), true);
pw.println(msg);
s.close();
```

The first parameter gives the new PrintWriter instance a reference to the socket's stream. The second parameter tells the object to auto-flush whenever the program calls println(). Normally, the I/O in PrintWriter buffers up the data until it has enough to minimize bandwidth waste. Specifying auto-flush says that you want to specify when a buffer is sent.

Using these I/O classes, you can create I/O messages that non-Java-based programs can interpret. However, you can still send/receive objects to/from another Java program using the ObjectOutputStream/ObjectInputStream classes. You can transmit any object that implements the Serializable interface.

```java
String msg = new String("Test");
Socket s = new Socket(hostname, port);
ObjectOutputStream oos = new ObjectOutputStream(
    s.getOutputStream());
oos.writeObject(msg);
```

The receiving end can take the message as an object and convert it into a known type:

```java
Socket s = ss.accept();
ObjectInputStream ois = new ObjectInputStream(
    s.getInputStream());
String newMsg = (String)ois.readObject();
```

If the message does not match the type being cast, the interpreter throws a ClassCastException. So if the program gets a class that you did not anticipate, you can use class reflection to get the correct type. If the program still does not know the type, you can dig deeper in the class and get the methods, inheritance, and implementations. While making the code more complicated, using this approach can result in a more extensible product.

# Configuring the Java Socket

Chapter 9 lists several ways you can configure your socket to do different operations using socket options. Java versions up to 1.3 have exposed some of these capabilities in the API. Please note that if the operating system does not support certain socket options, Java cannot expose them. This section describes these exposed options.

# Shared Java-Socket Configurations

All Java sockets share methods to configure the socket. The following determines how long a read waits for data. These methods expose the SO_TIMEOUT socket option, which determines how long a read waits. The SO_TIMEOUT option is archaic, and Linux uses fcntl(), poll(), or select() instead.

```
getSoTimeout()
setSoTimeout(int timeout)
```

The following code specifies the size of the internal send buffers in bytes. These methods expose the SO_SNDBUF socket option:

```
getSendBufferSize()
setSendBufferSize(int size)
```
