
```java
// Fig. 24.9: Server.java
// 接收和向客户端发送包的服务器。
import java.io.IOException;
import java.net.DatagramPacket;
import java.net.DatagramSocket;
import java.net.SocketException;
import java.awt.BorderLayout;
import javax.swing.JFrame;
import javax.swing.JScrollPane;
import javax.swing.JTextArea;
import javax.swing.SwingUtilities;

public class Server extends JFrame {
    private JTextArea displayArea; // 显示接收到的包
    private DatagramSocket socket; // 连接客户端的 socket

    public Server() {
        super("Server");
        displayArea = new JTextArea(); // 创建 displayArea
        add(new JScrollPane(displayArea), BorderLayout.CENTER);
        setSize(400, 300); // 设置窗口大小
        setVisible(true); // 显示窗口

        try { // 创建用于发送和接收包的 DatagramSocket
            socket = new DatagramSocket(5000);
        } catch (SocketException socketException) {
            socketException.printStackTrace();
            System.exit(1);
        } // 结束 catch
    } // 等待包到达，向客户端显示数据和每个包
    public void waitForPackets() {
        while (true) {
            try { // 接收包，显示内容，返回副本给客户端
                byte data[] = new byte[100]; // 设置包
                DatagramPacket receivePacket = 
                    new DatagramPacket(data, data.length);
                socket.receive(receivePacket); // 等待接收包

                // 显示从接收的包中获取的信息
                displayMessage("\nPacket received:" +
                    "\nFrom host: " + receivePacket.getAddress() +
                    "\nHost port: " + receivePacket.getPort() +
                    "\nLength: " + receivePacket.getLength() +
                    "\nContaining:\n" + new String(receivePacket.getData(), 0, receivePacket.getLength()));

                sendPacketToClient(receivePacket); // 发包到客户端
            } catch (IOException ioException) {
                ioException.printStackTrace();
            }
        }
    }

    private void displayMessage(String messageToDisplay) {
        // 更新 displayArea 的实现
        SwingUtilities.invokeLater(() -> {
            displayArea.append(messageToDisplay);
        });
    }

    private void sendPacketToClient(DatagramPacket receivePacket) throws IOException {
        // 向客户端回包的实现
        DatagramPacket sendPacket = new DatagramPacket(
            receivePacket.getData(),
            receivePacket.getLength(),
            receivePacket.getAddress(),
            receivePacket.getPort()
        );
        socket.send(sendPacket);
    }
}
```

图. 24.9 | 使用数据文进行无连接客户端/服务器计算的服务端。（部分 I/2）。

> 常见编程错误 24.2
>
> 在创建 `DatagramSocket` 时指定已占用的端口或无效的端口号会导致 `SocketException`。

## 24.7 基于数据文的无连接客户端/服务器交互

```java
// Fig. 24.10: ServerTest.java
// 测试 Server 类。
import javax.swing.JFrame;

public class ServerTest {
    public static void main(String args[]) {
        Server application = new Server(); // 创建服务器
        application.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        application.waitForPackets(); // 运行服务器应用程序
    }
}
```

接收包数据后的服务器窗口

## 第 24 章 网络

向 `Packet` 构造函数传递四个参数。第一个参数指定要发送的字节数组。第二个参数指定要发送的字节数数量。第三个参数指定客户端的 Internet 地址，数据包将发送到该地址。第四个参数指定客户端等待接收数据包的端口。第 81 行通过网络发送数据包。`DatagramSocket` 的 `send` 方法在发送数据包时发生错误会抛出 `IOException`。

### Client 类

`Client` 类（图 24.11）的工作原理与 `Server` 类类似，不同之处在于，`Client` 仅在用户在文本框中输入消息并按下回车键时才发送数据包。当这种情况发生时，程序调用 `actionPerformed()` 方法（第 32–57 行），该方法将输入的字符串转换为字节数组（第 41 行）。第 44–46 行创建一个 `DatagramPacket`，并用字节数组、用户输入的字符串长度、数据包要发送的 IP 地址（在本例中为 `InetAddress.getLocalHost()`）以及服务器等待数据包的端口（5000）对其进行初始化。第 47 行发送数据包。注意，此示例中的客户端必须知道服务器正在端口 5000 接收数据包——否则服务器将无法接收数据包。
