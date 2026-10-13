
```java
void registerChatListener(ChatChangeListener cl) {
    this.chatListener = cl;
}
protected ChatListener chatListener = null;

// 处理套字输入的内部类：
class HandleInputSocket extends Thread {
    int listenPort = 8191;
    public HandleInputSocket(int port) {
        super();
        listenPort = port;
        start();
    }
    public void run() {
        try {
            serverSocket = new ServerSocket(listenPort, 2000);
        } catch (IOException e) {
            System.out.println("Error in handling socket " + e + ", port: " + port);
        }

        try {
            while (true) {
                Socket socket = serverSocket.accept();
                new MyServerConnection(socket);
            }
        } catch (IOException e) {
            System.out.println("Error socket connection: " + e);
        }
        finally {
            try {
                serverSocket.close();
            } catch (IOException e) {
                System.out.println("I/O exception: " + e);
            }
        }
    }
}
```

# 32 使用 Java 编程

## 继续

### 编写用户界面

#### 列表 32.8 续
```java
}
    // 一个用于处理
    // 传入套接字连接的内部类
public class MyServerConnection extends Thread {
    protected transient Socket client_socket;
    protected transient DataInputStream input_strm;
    protected transient PrintStream output_strm;

    public MyServerConnection(Socket client_socket) {
        this.client_socket = client_socket;
        try {
            input_strm = new DataInputStream(client_socket.getInputStream());
            output_strm = new PrintStream(client_socket.getOutputStream());
        } catch (IOException io_exception) {
            try {
                client_socket.close();
            } catch (IOException io_ex2) {
                System.err.println("Exception 2: " + socket streams + " * " + io_exception);
            }
        }
        return;
        // 启动线程（即调用 'run' 方法）：
        this.start();
    }

    public void run() {
        String input_buf;
        try {
            while (true) {
                input_buf = input_strm.readLine();
                if (input_buf == null) {
                    logout();
                    break;
                }
                System.out.println("*received on socket: " + input_buf);
            }
            if (chatListener != null) {
                chatListener.receiveText(input_buf);
            }
        }
        catch(Exception exception) { }
        finally {
          try {
            client_socket.close();
          } catch (Exception exception) {
          }
        }
    }
}
```

此示例与我们在上一节看到的处理基于套接字的 IPC（进程间通信）示例非常相似。`ChatEngine` 使用内部类来处理来自套接字的读写操作。`ChatEngine` 中的两个内部类是：

- `HandleInputSocket`（与上一节中同名的类几乎相同）
- `MyServerConnection`

在此类中，主类 `ChatEngine` 有一个方法可以将文本写入为连接另一个 `ChatEngine` 实例的套接字连接打开的输出流。以下是 `ChatEngine` 类中的公共方法：

| 方法 | 说明 |
| --- | --- |
| `ChatEngine` | 类构造函数（无任何操作）。 |
| `startListening` | 开始在指定的端口上监听聊天引擎。 |
| `connect` | 使用指定的主机名（或绝对 IP 地址）和端口连接到远程引擎的套接字。 |
| `logout` | 断开与远程引擎的连接。 |
| `send` | 向远程引擎发送指定的字符串。 |
| `registerChatListener` | 注册实现 `ChatListener` 接口的类实例，以接收来自远程聊天引擎的传入文本。 |

列表 32.8 中的 `HandleInputSocket` 内部类与上一节中的 `do_input` 内部类相似。该内部类派生自 `Thread`，`run` 方法监听传入的套接字连接，并创建 `MyServerConnection` 类实例来处理来自远程聊天引擎的传入文本。此示例比所需的通用：`HandleInputSocket` 类中的代码适用于任何（合理的）数量的套接字连接，但在本示例中，我们仅支持两个聊天引擎之间的“点对点”。

### AWT 简介

当 Sun Microsystems 最初发布 Java 语言时，抽象窗口工具包（AWT）被用于编写图形用户界面（GUI）程序。当 Java 语言从 1.0 更新到 1.1 时，包含了一个新的事件模型和对 AWT 的改进。本书编写时，Sun 已发布 Java 1.2 版本（现在称为 2.0 版本），但 AWT 的 API 并没有改变。AWT 提供了几个类用于向程序添加特定组件，例如：

| 类 | 说明 |
|---|---|
| `Button` | 命令按钮或“推”按钮。 |
| `Label` | 用于不可编辑的文本。 |
| `TextField` | 用于用户编辑单行。 |
| `TextArea` | 用于用户编辑多行。 |
| `List` | 用于显示列表。 |

这些组件放置在容器中，例如：

| 容器 | 说明 |
|---|---|
| `Panel` | 用于持有其他对象。 |
| `Frame` | 带有标题的顶层窗口。 |

## 编写用户界面

### 第四部分

#### 列表 32.9
*(注：此处原文代码块不完整，已根据上下文保留了标题结构)*

# 使用 AWT 编写聊天程序
