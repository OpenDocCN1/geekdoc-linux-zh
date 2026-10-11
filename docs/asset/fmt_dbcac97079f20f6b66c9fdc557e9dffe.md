
# Fig. 24.11: Client.java
// 与服务器发送和接收数据包的客户端。
```java
import java.io.IOException;
import java.net.DatagramPacket;
import java.net.DatagramSocket;
import java.net.InetAddress;
import java.net.SocketException;
import java.awt.BorderLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import javax.swing.JFrame;
import javax.swing.JScrollPane;
import javax.swing.JTextArea;
import javax.swing.JTextField;
import javax.swing.SwingUtilities;

public class Client extends JFrame {
    private JTextField textField; // 用于输入消息
    private JTextArea displayArea; // 用于显示消息
    private DatagramSocket socket; // 连接服务器的 socket
    
    // 设置 GUI 和 DatagramSocket
    public Client() {
        super("Client");
        textField = new JTextField("Type message here");
        textField.addActionListener(
            new ActionListener() {
            {
```

**图 24.11** 使用数据报的无连接客户端/服务器计算的客户端侧。（3 部分中的第 1。）

## 24.7 基于数据报的无连接客户端/服务器交互

```java
public void actionPerformed(ActionEvent event) {
    try // 创建并发送数据包
        // 从 getActionCommand() 获取消息
        String message = event.getActionCommand();
        displayArea.append("\nSending packet containing: " +
            message + "\n");
        byte[] data = message.getBytes(); // 转换为字节
        // 创建 sendPacket
        DatagramPacket packet = new DatagramPacket(data,
            data.length, InetAddress.getLocalHost(), 5000);

        socket.send(packet); // 发送数据包
        displayArea.append("Packet sent\n");
        displayArea.setCaretPosition(displayArea.getText().length());
    } catch (IOException exception) {
        displayMessage(exception.toString() + "\n");
        exception.printStackTrace();
    } // end catch
} // end actionPerformed
} // end inner class
);
add(textField, BorderLayout.NORTH);
displayArea = new JTextArea();
add(new JScrollPane(displayArea), BorderLayout.CENTER);

setSize(400, 300); // 设置窗口大小
setVisible(true); // 显示窗口

try // 创建用于发送和接收数据包的 DatagramSocket {
    socket = new DatagramSocket();
} // end try
catch (SocketException socketException) {
    socketException.printStackTrace();
    System.exit(1);
} // end catch
} // end Client constructor

// 等待来自服务器的数据包，显示数据包内容
public void waitForPackets() {
    while (true) {```

图 24.11 | 使用数据报的无连接客户端/服务器计算侧。（3 部分中的第 2。）

```java
try // 接收数据包并显示内容
{
    byte data[] = new byte[100]; // 设置数据包
    DatagramPacket receivePacket = new DatagramPacket(
        data, data.length);

    socket.receive(receivePacket); // 等待数据包

    // 显示数据包内容
    displayMessage("\nPacket received: " +
    "\nFrom: " + receivePacket.getAddress() +
    "\ost: " + receivePacket.getPort() +
    "\nlength: " + receivePacket.getLength() +
    "\nContaining: " + new String(receivePacket.getData(
        0, receivePacket.getLength()));
} catch (IOException exception) {
    displayMessage(exception.toString() + "\n");
    exception.printStackTrace();
} // end catch
} // end while
} // end method waitForets

// 在事件线程中操作 displayArea
private void displayMessage(final String messageToDisplay) {
    SwingUtilities.invokeLater(
        new Runnable() {
            public void run() // 更新 displayArea
{
                displayArea.append(messageToDisplay);
            } // end method run
        } // end inner class
    }); // end call to SwingUtilities
} // end method displayMessage
} // end class
```

**图 24.11** 使用数据报的无连接客户端/服务器计算侧。注意此应用程序中的 `DatagramSocket` 构造函数调用（第 71 行）没有指定任何参数。此无参数构造函数允许客户端选择可用端口。客户端不需要特定的端口号，因为服务器从客户端发送的 `DatagramPacket` 中接收端口号。`waitForPackets` 方法（第 81–107 行）等待服务器数据包的无限循环。第 91 行在数据包到达之前阻塞，因为 GUI 事件在事件线程中处理。它阻止循环继续直到数据包到达。当数据包到达时，第 91 行将其存储在 `receivePacket` 中，第 94–99 行

# Fig. 24.12: ClientTest.java
// 测试 Client 类
```java
import javax.swing.JFrame;
public class ClientTest {
    public static void main(String args[]) {
        Client application = new Client(); // 创建客户端
        application.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        application.waitForPackets(); // 运行应用程序
    } // end main
} // end class
```
