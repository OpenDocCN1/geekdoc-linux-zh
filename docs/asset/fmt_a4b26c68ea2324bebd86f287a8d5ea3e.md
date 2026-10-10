
除了 `ADD` 和 `SUBTRACT`，该枚举还有一个 `DONE` 值，告诉服务器客户端已完成。接收到该值后，服务器可以关闭流。

`Command` 类非常直接：

```java
import java.io.*;

class Command implements Serializable {
    private Operation operation;
    private float[] operands;

    Command(Operation operation) {
        this.operation = operation;
    }

    Command(Operation operation, float[] operands) {
        this.operation = operation;
        this.operands = operands;
    }

    Operation getOperation() {
        return operation;
    }

    float[] getOperands() {
        return operands;
    }
}
```

幸运的是，枚举是可序列化的，因此 `Command` 类的整个图都是可序列化的。`Server` 类是一个在 `7654` 端口创建服务器套接字的应用程序。（端口号是随机分配的。`1024` 以下的数字留给标准委员会分配。`1024` 以上的数字不受控制，可以自由使用。）建立一个客户端连接，然后产生一个线程来处理该连接，然后等待新的连接。我们将首先查看 `Server` 类，然后提供服务的线程类。这里是 `Server` 类：

```java
import java.io.*;
import java.net.*;

public class Server {

    public static void main(String[] args) throws IOException {

        ServerSocket ss = new ServerSocket(7654);

        while (true) {

            Socket sock = ss.accept();

            ServiceGiver sg = new ServiceGiver(sock);

            sg.start();

        }

    }
}

class ServiceGiver extends Thread {
    private Socket socket;

    public ServiceGiver(Socket socket) {
        this.socket = socket;
    }

    @Override
    public void run() {
        try (ObjectInputStream in = new ObjectInputStream(socket.getInputStream());
             ObjectOutputStream out = new ObjectOutputStream(socket.getOutputStream())) {
            while (true) {
                Command cmd = (Command) in.readObject();
                if (cmd.getOperation() == Operation.DONE) {
                    break;
                }
                float[] operands = cmd.getOperands();
                float result = 0;
                if (cmd.getOperation() == Operation.ADD) {
                    for (float f : operands) result += f;
                } else if (cmd.getOperation() == Operation.SUBTRACT) {
                    for (float f : operands) result -= f;
                }
                out.writeObject(result);
            }
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        } finally {
            try {
                socket.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}

class Client {
    public static void main(String[] args) throws IOException {
        try (Socket socket = new Socket("localhost", 7654);
             ObjectOutputStream out = new ObjectOutputStream(socket.getOutputStream());
             ObjectInputStream in = new ObjectInputStream(socket.getInputStream())) {
            
            out.writeObject(new Command(Operation.ADD, new float[]{10.5f, 20.0f}));
            System.out.println("Addition result: " + in.readObject());

            out.writeObject(new Command(Operation.SUBTRACT, new float[]{50.0f, 10.0f}));
            System.out.println("Subtraction result: " + in.readObject());

            out.writeObject(new Command(Operation.DONE));
        }
    }
}
```

```java
} catch (IOException x) {
    System.out.println("Server Stress: " +
    x.getMessage());
}
```

`Server` 类并没有什么困难。它的 `main()` 方法结构与本章早些“Java 中的 Sockets”部分中 `ServerSocket` 讨论的示例相同。代码中没有任何内容指示执行的是哪种服务，这是一个很好的信号：它表明功能被很好地划分了。`Server` 类负责建立连接，而 `ServiceGiver` 类则在这些连接上提供服务。以下是 `ServiceGiver` 的代码：

```java
import java.io.*;
import java.net.*;

class ServiceGiver extends Thread {
    private Socket sock;

    ServiceGiver(Socket sock) {
        this.sock = sock;
    }

    public void run() {
        try {
            // Build object streams.
            OutputStream os = sock.getOutputStream();
            ObjectOutputStream oos = new ObjectOutputStream(os);
            InputStream is = sock.getInputStream();
            ObjectInputStream ois = new ObjectInputStream(is);

            // Provide service.
            while (true) {
                Command command = (Command)ois.readObject();
                float[] operands = command.getOperands();
                switch (command.getOperation()) {
                    case ADD:
                        Float result = operands[0] + operands[1];
                        oos.writeObject(result);
                        break;
                    case SUBTRACT:
                        result = operands[0] - operands[1];
                        oos.writeObject(result);
                        break;
                    case DONE:
                        oos.close();
                        ois.close();
                        os.close();
                        is.close();
                        sock.close();
                        return;
                }
            }
        } catch (IOException x) {
            System.out.println("IO Stress: " + x.getMessage());
        } catch (ClassNotFoundException x) {
            System.out.println("Class Stress: " + x.getMessage());
        }
    }
}
```

这个 `catch` 遵循了本章早些“Java 中的 Server Sockets”部分给出的示例结构。建议提供服务的类应该实现 `Runnable`。在示例中代码非常简单，因此扩展 `Thread` 就足够了。构造函数创建了要接收服务的 socket。所有服务都在 `run()` 方法中进行，该方法循环从输入流中读取 `Command` 对象，从 `Command` 对象中提取 `Operation` 并采取适当的操作。记住 `Operation` 是一个枚举（enum），所以在这里你看到了对枚举值进行 `switch` 的示例。

让我们通过观察一个简单的客户端来完成这个示例，它连接到服务器并命令服务器执行它的每个操作：

```java
import java.io.*;
import java.net.*;

public class Client {
    public static void main(String[] args) {
        try {
            test(args[0]); // server name
        } catch (IOException x) {
            System.out.println("IO Stress: " + x.getMessage());
        } catch (ClassNotFoundException x) {
            System.out.println("Class Stress: " + x.getMessage());
        }
    }

    private static void test(String serverName)
        throws IOException, ClassNotFoundException {
        // Connect to server.
        Socket sock = new Socket(serverName, 7654);

        // Build object streams.
        OutputStream os = sock.getOutputStream();
        ObjectOutputStream oos = new ObjectOutputStream(os);
        InputStream is = sock.getInputStream();
        ObjectInputStream ois = new ObjectInputStream(is);

        // Test addition.
        float[] addUs = {12.3f, 56.7f};
        Command command = new Command(Operation.ADD, addUs);
        oos.writeObject(command);
        Float result = (Float)ois.readObject();
        System.out.println("Addition result: " + result);

        // Test subtraction.
        float[] subtractUs = {3.14159f, 1.11111f};
        command = new Command(Operation.SUBTRACT, subtractUs);
        oos.writeObject(command);
        result = (Float)ois.readObject();
        System.out.println("Subtraction result: " + result);

        // Done.
        command = new Command(Operation.DONE);
        oos.writeObject(command);
        oos.close();
        ois.close();
        os.close();
        is.close();
        sock.close();
    }
}
```

`Client` 假设服务器的主机名在命令行提供。`main()` 方法调用 `test()`，它命令服务器执行加法、减法，然后结束。

服务器和客户端能够共同工作，是因为它们都了解对方的要求和行为。这些定义了一个小协议，可以总结如下：

1. 客户端通过向服务器发送 `Command` 实例来启动通信。
2. 当服务器接收 `ADD` 或 `SUBTRACT` 命令时，它响应一个 `float`。
3. 当服务器接收 `DONE` 命令时，它关闭连接而不作响应。

如果你决定在项目中使用对象流，你的项目将比你选择的复杂得多，但其结构是类似的：客户端将启动通信向服务器发送某些内容，服务器对数据库进行某些操作然后发送响应。

到目前为止你已经看到对象流对于客户端下达指令的系统是一个很好的基础。

每个步骤都将在下方的章节中单独描述。我们将开发一个简单的示例，模拟你在在本章较早看到的对象流示例。

## 第 1 步：创建远程接口（Remote Interface）

远程接口是一个描述远程对象可访问方法的接口。远程对象和与其通信的存根（stub）都实现了该远程接口。

记得 `RMI` 客户端使用远程引用（remote references），这些引用指向存根。远程引用的类型就是远程接口。因此，客户端通过调用远程引用上的远程接口方法来调用 `RMI`。稍后你将看到如何实现。现在，第一步是创建一个接口，列出远程对象的可远程访问方法。

所有接口都必须继承 `java.rmi.Remote`，这是一个标记接口（tagging interface）。记住，标记接口有一个空的方法列表，因此类可以实现 `Remote` 而无需实际提供任何方法实现。

接口中的所有方法除了任何指定的异常外，必须抛出 `RemoteException`。如果与服务器的连接出现问题，存根将抛出 `RemoteException`。这意味着在所有的客户端代码中，所有的 `RMI` 调用必须捕获 `RemoteException` 或通过其他方式处理它。

`RMI` 使用序列化对象（serialized objects）将方法参数从客户端发送到服务器，并将返回值和异常从服务器返回客户端。因此，所有参数、返回值和异常必须是可序列化的。不需要担心异常，因为 `java.lang.Exception` 实现了 `Serializable`，但你需要关注参数和返回值。`RMI` 可以处理基本类型的参数和返回值，所以关于远程接口方法你真正需要记住的是：所有对象类型的参数和返回值必须是可序列化的。
