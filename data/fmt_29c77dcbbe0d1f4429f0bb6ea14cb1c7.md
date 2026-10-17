
```java
package udsockets;
import java.io.*;
import java.net.*;
import java.util.*;

public class UDPClient {
    int port = 6040;
    public UDPClient() {
    }
    public void startClient() {
        try {
            InetAddress inetAddr = InetAddress.getByName("localhost");
            DatagramSocket dgSocket = new DatagramSocket(port);
            System.out.println("Message reception started ...");

            byte buff[] = new byte[1000];
            String message;
            try {
                DatagramPacket dgPacket = new DatagramPacket(buff, buff.length);
                dgSocket.receive(dgPacket);
                while (dgPacket.getData().length > 0) {
                    message = new String(dgPacket.getData(), 0, dgPacket.getLength());
                    System.out.println(message);
                    dgSocket.receive(dgPacket);
                }
            }
            catch (IOException sx) {
                System.out.println("IO Exception ...");
                System.exit(-1);
            }
            catch (UnknownHostException sx) {
                System.out.println("Host unknown ...");
                System.exit(-1);
            }
            catch (SocketException sx) {
                System.out.println("Socket Exception ...");
                System.exit(-1);
            }
        }
    public static void main(String[] args) {
        UDPClient udpClient1 = new UDPClient();
        udpClient1.StartClient();
    }
}
```

# 远程方法调用 (REMOTE METHOD INVOCATION)

远程方法调用 (`RMI`) 是企业级（`Enterprise JavaBeans`）背后健壮架构的基础，它是最流行的企业级 Java 开发框架。在本节中，将详细讨论 `RMI` 的概念，为后续主题奠定必要的基础。要使用 `RMI` 框架创建分布式服务器对象，第一步是定义一个扩展 `java.rmi.Remote` 接口的接口（通常称为远程接口）。应该供客户端访问的服务器对象应该远程实现此（应用程序特定的）远程接口，并扩展 `java.rmi.server.UnicastRemoteObject` 以为服务器对象提供远程行为。服务器对象中所有供客户端访问每个方法都应该定义在远程接口中，`RMI` 框架会暴露服务器对象实现的方法。虽然远程接口使用 Java 编译器（`javac` 程序）编译，但服务器对象是使用 `RMI` 编译器（`rmic` 程序）编译的。这个过程会创建一个存根（`stub`）类文件，该存根类文件应提供给客户端应用程序，而服务器对象包含相应的骨架（`skeleton`）代码，该代码与客户端存根代码一起对数据对象进行序列化和反序列化，并在服务器端实例化。在 Java 2 SDK 发布之前，`rmic` 编译器会创建两个文件：客户端存根代码和服务器端骨架类。自 Java 2 SDK 发布以来，`rmic` 不再创建服务器端骨架类，因为服务器端的序列化/反序列化是由服务器对象本身处理的。

# 构建分布式 Java 应用程序 .399

命名服务与指定的 `RMI` 对象的 `RMI` 注册表交互（第 5 步）。

在成功识别 `RMI` 对象后，命名服务将 `RMI` 对象的远程接口引用返回给客户端应用程序（第 6 步）。

客户端调用远程接口上的方法，从而触发关联存根对象（`stub object`）上的对应方法（第 7 步）。

存根对象将方法参数序列化到相应的骨干（`skeleton`），该骨干嵌入在 `RMI` 框架中（第 8 步），并将执行结果反序列化返回给客户端应用程序（第 9 步）。

现在让我们遍历创建和使用 `RMI` 对象的流程。如之前所述，第一步是创建一个扩展 `java.rmi` 包中定义的 `Remote` 接口的接口。`Remote` 接口是一个标记接口，因此不包含任何需要实现的方法，这与之前章节中讨论过的 `Serializable` 接口非常相似。新继承的接口应该包含 `RMI` 对象应该实现的所有方法。此接口中定义的每个方法都是远程方法，并抛出 `RemoteException`。`RMI` 客户端-服务器模型通过一个简单的示例进行了演示：该服务器实现了一个方法，将服务器当前的系统时间作为 `java.util.Calendar` 对象返回；另一个方法以 `String` 对象返回相同的信息；以及一个以 `java.util.Calendar` 对象作为参数设置服务器系统时间的方法。列表 7.10 显示了 `RMI` 对象的远程接口定义。该列表可在随附的 CD-ROM 上。

![](img/1c052d580a194876cd94f43b32c39cf4_414_0.png)

## 列表 7.10 CurrTime.java

```java
import java.rmi.*;
import java.util.*;

public interface CurrTime extends Remote {
    public Calendar getCurrentTime() throws RemoteException;
    public String getCurrentTimeString() throws RemoteException;
    public void setCurrentTime(Calendar currTime) throws RemoteException;
}
```

定义远程接口后，应对其进行编译——使用普通的 `javac` 编译器，语法与此处所示类似——以生成接口的 `.class` 文件。

```
$ javac CurrTime.java
```

# 企业级 Linux 应用开发

现在我们应该在服务器对象中实现此接口定义的方法。列表 7.11 显示了服务器对象的实现。从列表中可以注意到，服务器对象扩展了 `java.rmi.server.UnicastRemoteObject` 类，并实现了列表 7.10 中定义的接口。在实例化 `RMI` 服务器对象后，应该使用由 `java.rmi.Naming` 类提供的命名服务将其注册到 `rmireistry` 中。这也被称为将 `RMI` 对象绑定到注册表。只有在 `rmireistry` 中注册了的对象才能供客户端通过 `RMI` 框架进行访问。这可以通过两种方式实现：实例化远程服务器对象的服务器主程序可以执行此绑定，或者远程服务器对象也可以可以在其构造函数中将自己绑定到 `rmireistry`。无论使用哪种方法绑定远程对象，都应该为其提供一个名称，以便 `rmireistry` 通过名称识别该对象。在当前示例中，`RMI` 服务器对象在其构造方法中自行注册到 `rmireistry`。此时，非常重要的一点是将 `rmireistry` 与 Microsoft Windows 操作系统上实现的注册表（`registry`）概念混淆。`rmireistry` 是运行在 Java 虚拟机环境中的控制台应用程序，并在其内部内存中维护远程对象的名称；而 Microsoft Windows 注册表是关于计算机上安装的所有应用程序（此外还有 COM/ActiveX 相关信息）的某种信息数据库，并存储在磁盘上。`rmireistry` 没有任何此类开销。它非常简单的 Java 程序。列表 7.11 可用在

## 列表 7.11 CurrTimeImpl.java
