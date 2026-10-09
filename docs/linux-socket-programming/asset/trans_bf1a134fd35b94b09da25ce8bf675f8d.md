
## 分类 I/O 类

Java I/O 包包含多个类，每个类都定义为执行特定任务。它们都用于发送或接收信息。不幸的是，由于类数量众多，很难知道该使用哪个以及何时使用。也许处理它们最简单的方法是根据它们的几种职责进行分组。这样你就可以轻松看出哪个类最适合套接字使用。

I/O 包本质上提供六种主要的 I/O 类型。每种类型都服务于特定目的，并且都派生自 `Reader`、`Writer`、`InputStream` 或 `OutputStream`：

- **内存** — 基于内存缓冲区的 I/O。该包不访问任何硬件设备；相反，RAM 中的数组充当虚拟 I/O 池。这在解析字符串甚至创建数据报缓冲区时非常有用。示例包括 `ByteArrayInputStream`、`ByteArrayOutputStream`、`CharArrayReader`、`CharArrayWriter`、`StringReader` 和 `StringWriter`。
- **文件** — 文件系统读取、写入和操作。这些类提供了在文件系统中创建、读取、写入、删除或操作文件的方式。示例包括 `FileInputStream`、`FileOutputStream`、`FileReader` 和 `FileWriter`。
- **过滤器** — 进行某种基于字符的转换或解释的 I/O。例如，将换行符视为记录结束，通过制表符或逗号识别字段，或将二进制值转换为可读数字。示例包括 `FilterReader`、`FilterWriter`、`PrintWriter` 和 `PrintStream`（已弃用）。
- **对象** — 完整对象的发送和接收。这是最令印象深刻的一点；Java 可以在你无需编写代码的情况下发送和接收实例。在大多数情况下，你只需标记类为 `Serializable`，即可传输和接收对象实例。相关的类是 `ObjectInputStream` 和 `ObjectOutputStream`。
- **管道** — 类似于 C 语言中的进程间通信（IPC）。你创建一个管道并将其与另一个管道链接，然后两个线程互相发送消息。相关的类是 `PipedInputStream`、`PipedOutputStream`、`PipedReader` 和 `PipedWriter`。
- **流** — 通用缓冲 I/O 通信。这是套接字使用的形式。如果你想使用其他类型，需要将流类转换为另一种类型（参见下一节）。抽象类是 `InputStream` 和 `OutputStream`。基本的转换类是 `InputStreamReader` 和 `OutputStreamWriter`。

该包还有几个其他类，实际上并不适合这种分类。例如，`SequenceInputStream` 允许你将两个流合并为一个。

在所有这些类中，你可能最想熟悉的是用于发送和接收自定义类的 `ObjectInputStream` 和 `ObjectOutputStream`，或者用于字符串 I/O 的 `BufferedReader` 和 `PrintWriter`。网络程序经常使用这些，因为它们最适合套接字编程。同样，你可以使用 `ByteArrayInputStream` 或 `ByteArrayOutputStream` 对象来为数据报消息提供接口。

## 在 I/O 类之间转换

某个类拥有的某些功能可能在套接字提供给你的 I/O 类中不可直接获得。`Socket` 类仅提供两个 I/O 类——`OutputStream` 和 `InputStream`。这些功能提供了非常基础的字节数组读取和写入。要获取不同的功能，你需要转换这些类。

假设你想读取字符串，而不是字节数组。`BufferedReader` 具有良好的 `String` 接口。你需要从 `InputStream` 抽象类转换到 `Reader` 抽象类。`InputStreamReader` 类充当此转换的中介：

```java
Socket s = new Socket(host, port);
InputStream is = s.getInputStream();
InputStreamReader isr = new InputStreamReader(is);
BufferedReader br = new BufferedReader(isr);
String l = br.readLine();
```

你也可以使用以下惯用的简写：

```java
BufferedReader br = new BufferedReader(new InputStreamReader(s.getInputStream()));
```

通过通道发送字符串（而不实际转换字符串）要容易一些：

```java
String msg = new String("<html><body>Welcome to my Java website</></body></html>");
SocketServer ss = new SocketServer(9999);
Socket s = ss.accept();
PrintWriter pw = new PrintWriter(s.getOutputStream(), true);
pw.println(msg);
s.close();
```

第一个参数为新的 `PrintWriter` 实例提供了套接字流的引用。第二个参数告诉对象每当程序调用 `println()` 时执行*自动刷新*。通常，`PrintWriter` 中的 I/O 会缓冲数据，直到积累足够数据以最小化带宽浪费。指定自动刷新意味着你希望指定何时发送缓冲区。

使用这些 I/O 类，你可以创建非 Java 程序能够解释的 I/O 消息。然而，你仍然可以使用 `ObjectOutputStream`/`ObjectInputStream` 类与另一个 Java 程序进行对象的发送/接收。你可以传输任何实现了 `Serializable` 接口的对象。

```java
String msg = new String("Test");
Socket s = new Socket(hostname, port);
ObjectOutputStream oos = new ObjectOutputStream(s.getOutputStream());
oos.writeObject(msg);
```

接收端可以将消息作为对象接收，并将其转换为已知类型：

```java
Socket s = ss.accept();
ObjectInputStream ois = new ObjectInputStream(s.getInputStream());
String newMsg = (String) ois.readObject();
```

如果消息与强制转换的类型不匹配，解释器将抛出 `ClassCastException`。因此，如果程序获取了一个你未预料的类，你可以使用类反射来获取正确的类型。如果程序仍然不知道类型，你可以深入该类以获取方法、继承和实现。虽然这种方法会使代码更复杂，但使用它可以产生更具扩展性的产品。

## 配置 Java 套接字

第 9 章列出了几种你可以配置套接字以执行不同操作的方法，这些配置使用套接字选项。Java 1.3 及更早版本已在 API 中公开了一些这些功能。请注意，如果操作系统不支持某些套接字选项，Java 无法公开它们。本节描述了这些已公开的选项。

### 共享的 Java 套接字配置

所有 Java 套接字共享配置套接字的方法。以下内容确定读取等待数据的时间。这些方法公开了 `SO_TIMEOUT` 套接字选项，该选项确定读取等待的时间。`SO_TIMEOUT` 选项已过时，Linux 使用 `fcntl()`、`poll()` 或 `select()` 代替。

```java
getSoTimeout()
setSoTimeout(int timeout)
```

以下代码指定内部发送缓冲区的大小（以字节为单位）。这些方法公开了 `SO_SNDBUF` 套接字选项：

```java
getSendBufferSize()
setSendBufferSize(int size)
```

下一段代码行指定内部接收缓冲区的大小（以字节为单位）。这些方法公开了 `SO_RCVBUF` 套接字选项。

```java
getReceiveBufferSize()
setReceiveBufferSize(int size)
setKeepAlive(boolean on)
```

以下方法确定套接字关闭后是否保留以及保留多长时间。这些调用公开了 IP `SO_LINGER` 套接字选项。

```java
getSoLinger()
setSoLinger(boolean on, int linger)
```

下一段代码启用或禁用 Nagle 算法，该算法在发送下一个数据包之前等待网络交付数据包。这些调用公开了 `TCP_NODELAY` 套接字选项。

```java
getTcpNoDelay()
setTcpNoDelay(boolean on)
```

## Java 组播特定配置

本节列出了你可以在 `MulticastSocket` 对象上设置的选项。这些功能决定了数据包在应该终止前允许经过多少个路由器跳数。

以下方法公开了 `IP_MULTICAST_TTL` 套接字选项。（奇怪的是，Java 不允许你为其他套接字类型指定 TTL。）

```java
getTimeToLive()
setTimeToLive(int ttl)
```

下一组方法通过公开 `IP_MULTICAST_IF` 套接字选项来设置组播传输的主要网络接口。

```java
getInterface()
setInterface(InetAddress inf)
```

## 程序多任务处理

Java 使多种编程技术变得简单而直接。除了大幅减少编程工作量和复杂度的网络包和 I/O 包外，它还拥有一致的多线程结构。Java 线程简单到只需声明一个接口。

在进行网络编程时，你肯定需要充分利用系统提供的所有多任务处理能力。本节总结了一些如果你想在自己的 Java 程序中使用线程时需要了解的事项。

## 类线程化

要创建可线程化的类，你可以从 `Thread` 类派生或实现 `Runnable` 接口。在这两种情况下，你必须定义 `run()` 方法，线程实际在那里开始运行。在第一种情况下，你可以简单地编写以下代码：

```java
public class TestThread extends Thread
{
  public void run()
  {
    /*** thread runs here ***/
```

