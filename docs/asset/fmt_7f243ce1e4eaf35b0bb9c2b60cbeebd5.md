
```java
// SimpleMulticastDestination excerpt
//---------------------------------------------------------------------------
MulticastSocket ms = new MulticastSocket(16900); // 新套接字
ms.joinGroup(InetAddress.getByName("224.0.0.1")); // 加入组
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
ms.close(); // 关闭连接
```

Listing 12.5 创建了一个用于多播的套接字，并请求一个端口以接收数据报。加入 `224.0.0.1`（本地主机）组后，它创建了一个用于接收传入数据报的包。

## 通过 I/O 连接

到目前为止，示例使用了非常简单且常常笨拙的 I/O 接口。Java 套接字的强大之处在于其通过不同 I/O 类进行连接的能力。Java 有多个类提供不同形式的数据读写。

本节对您可能希望与套接字一起使用的 I/O 类进行分类并展示如何使用它们。由于 I/O 包功能众多，本文不会面面俱到。如果您想了解更多信息，不妨参阅其他 Macmillan 出版社的 Java 书籍（例如 Kenneth Litwak 的 `Pure Java 2` 或 Nathan Meyers 的 `Java Programming on Linux`）。

## 对 I/O 类进行分类

Java I/O 包包含多个类，每个类都定义为执行特定任务。它们都用于发送或接收信息。不幸的是，由于类数量众多，很难知道何时该使用哪一个。也许处理它们最简单的方式是根据其几种职责对它们进行分组。这样您可以轻松看出哪个类最适合套接字使用。

I/O 包基本上提供了六种主要的 I/O 类型。每种类型服务于特定目的，并且都派生自 `Reader`、`Writer`、`InputStream` 或 `OutputStream`：

- **内存**— 基于内存缓冲区的 I/O。该包不访问任何硬件设备；相反，RAM 中的数组充当虚拟 I/O 池。这有助于解析字符串，甚至为数据报创建缓冲区。示例包括 `ByteArrayInputStream`、`ByteArrayOutputStream`、`CharArrayReader`、`CharArrayWriter`、`StringReader` 和 `StringWriter`。

- **文件**— 读取、写入和操作文件系统。这些类为您提供在文件系统中创建、读取、写入、删除或操作文件的方法。示例包括 `FileInputStream`、`FileOutputStream`、`FileReader` 和 `FileWriter`。

- **过滤器**— 执行某些基于字符的转换或解释的 I/O。例如，将换行符视为记录结束，通过制表符或逗号识别字段，或将二进制值转换为可读数字。示例包括 `FilterReader`、`FilterWriter`、`PrintWriter` 和 `InputStream`（已弃用）。

- **对象**— 编码对象的发送和接收。这一点最令人印象深刻。Java 可以在您不编写任何代码的情况下发送和接收实例。在大多数情况下，您只需标记该类为 `Serializable`，就可以传输和接收对象实例。这些类是 `ObjectInputStream` 和 `ObjectOutputStream`。

- **管道**— 类似于 C 中的 IPC（进程间通信）。您创建一个管道并将其与另一个管道连接，然后两个线程互相发送消息。这些类是 `PipedInputStream`、`PipedOutputStream`、`PipedReader` 和 `PipedWriter`。

- **流**— 通用的缓冲 I/O 通信。这是套接字使用的形式。如果您想使用其他类型，需要将流类转换为另一种类型（参见下一节）。抽象类是 `InputStream` 和 `OutputStream`。基本的转换类是 `InputStreamReader` 和 `OutputStreamWriter`。

![](img/2591af4bdf00a0f382331fc9481f785e_292_0.png)

该包还有其他一些类，确实不符合此分类。例如 `SequenceInputStream`，它允许您将两个流合并为一个。

在这些类中，您可能最想熟悉的是用于发送和接收自定义类的 `ObjectInputStream` 和 `ObjectOutputStream`，或用于字符串 I/O 的 `BufferedReader` 和 `PrintWriter`。网络程序经常使用这些，因为它们最适合套接字编程。同样，您可以使用 `ByteArrayOutputStream` 或 `ByteArrayInputStream` 对象为数据报消息提供接口。

## 在 I/O 类之间转换

某些类拥有的功能在套接字交给您的 I/O 类中可能无法直接获取。`Socket` 类仅提供两个 I/O 类——`OutputStream` 和 `InputStream`。这些仅提供了非常基础的字节数组读写功能。要获取不同的功能，您需要转换这些类。

假设您想读取字符串，而不是字节数组。`BufferedReader` 拥有良好的 `String` 接口。您需要从 `InputStream` 抽象类转换到 `Reader` 抽象类。`InputStreamReader` 类充当此转换的中介：

```java
Socket s = new Socket(host, port);
InputStream is = s.getInputStream();
InputStreamReader isr = new InputStreamReader(is);
BufferedReader br = new BufferedReader(isr);
String l = br.readLine();
```

您也可以使用以下惯用的简写：

```java
BufferedReader br = new BufferedReader(new InputStreamReader(
s.getInputStream()));
```

通过通道发送字符串（而不实际转换字符串）稍微容易一些：

```java
String msg = new String( 
"<html><body>Welcome to my Java website</body></html>");
SocketServer ss = new SocketServer(9999);
Socket s = ss.accept();
PrintWriter pw = new PrintWriter(s.getOutputStream(), true);
pw.println(msg);
s.close();
```

第一个参数为新 `PrintWriter` 实例提供了对套接字流的引用。第二个参数告诉对象每当程序调用 `println()` 时自动刷新。通常，`PrintWriter` 中的 I/O 会缓冲数据，直到积累足够多数据以最小化带宽浪费。指定自动刷新意味着您希望指定何时发送缓冲区。

使用这些 I/O 类，您可以创建非基于 Java 的程序可以解释的 I/O 消息。然而，您仍然可以使用 `ObjectOutputStream`/`ObjectInputStream` 类向另一个 Java 程序发送/接收对象。您可以传输任何实现 `Serializable` 接口的对象。

```java
String msg = new String("Test");
Socket s = new Socket(hostname, port);
ObjectOutputStream oos = new ObjectOutputStream(
    s.getOutputStream());
oos.writeObject(msg);
```

接收端可以将消息作为对象接收，并将其转换为已知类型：

```java
Socket s = ss.accept();
ObjectInputStream ois = new ObjectInputStream(
    s.getInputStream());
String newMsg = (String)ois.readObject();
```

如果消息不匹配正在转换的类型，解释器将抛出 `ClassCastException`。因此，如果程序获取了您未预料到的类，您可以使用类反射来获取正确的类型。如果程序仍然不知道类型，您可以更深入地挖掘该类以获取方法、继承和实现。虽然这会使代码变得更复杂，但使用这种方法可以生成更具扩展性的产品。

## 配置 Java 套接字
