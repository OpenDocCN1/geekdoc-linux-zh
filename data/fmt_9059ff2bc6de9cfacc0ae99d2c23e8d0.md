
```java
import java.io.*;
import java.util.zip.*;

public class ReadFile {
    static public void main(String [] args) {
        String file_name = "car.data";
        InputStream c1 = null, c2 = null;
        // 始终将文件 IO 包在 try/catch 语句中:
        try {
            FileInputStream f = new FileInputStream(file_name);
            GZIPInputStream gf = new GZIPInputStream(f);
            ObjectInputStream ois = new ObjectInputStream(gf);
            c1 = (Car)ois.readObject();
            c2 = (Car)ois.readObject();
            ois.close();
        } catch (Exception e) {
            System.out.println("Error: " + e);
        }
        System.out.println("Cars from file: " + c1.getName() + " and " + c2.getName());
    }
}
```

对象序列化在将对象保存到磁盘文件中非常有用，它是 Java 远程对象接口（RMI）技术用于 Java 程序间进程间通信的基础。RMI 超出了本短章节的范围，但我们将在本章稍后的部分看到使用 socket 的示例。

# 在 Java 中使用多线程

Java 语言使得多线程编程和 socket 编程都变得特别简单。在下一节中，我们将看到线程是 Java 中编写健壮 socket 程序的基本技术。在本节中，我们将查看一个短示例程序，该程序创建了一个新类 `MyThread` 并创建了它的 10 个实例。

列表 32.5 包含了两个 Java 类：`MyThread` 和 `ExampleThreads`。当一个类（如 `MyThread`）派生自 `Thread` 类时，它被期望会运行一个公共方法。当通过调用 `start` 方法启动线程时，该方法会被调用。

## 列表 32.5 ExampleThreads.java 文件

```java
// File: ExampleThreads.java
//
// 使用 Java 线程的示例
//
```

```java
import java.io.*;
import java.util.zip.*;

class MyThread extends Thread {
    public MyThread(String name) {
        super(name);
        this.name = name;
    }
    public MyThread() {
        this("no_name_thread');
    }
    private String name;

    public void run() {
        for (int i=0; i<5; i++) {
            System.out.println(name + " " + i);
            try {
                Thread.sleep(1000); // 休睡 1 秒
            } catch (Exception e) {
                System.out.println("Thread sleep: " + e);
            }
        }
    }
}
```

```java
public class ExampleThreads {
    public static void main(String[] args) {
        // 创建一个 MyThread 对象数组
        MyThread threads[] = new MyThread[10];
        for (int i=0; i<10; i++) {
            threads[i] = new MyThread("my_thread_" + i);
        }
        // 现在启动所有线程:
        for (int i=0; i<10; i++) {
            threads[i].start(); // 调用 'run' 方法
        }
    }
}
```

# 使用 Java 进行 GUI 编程

第32 章

`MyThread` 类没有声明为 `public`。Java 要求一个文件仅包含一个 `public` 类，且文件名必须是该 `public` 类名加上 `.java` 文件扩展名。

在这里我们看到线程是如何工作的：你从 `Thread` 派生一个类，并编写一个执行线程中工作的公共方法。调用 `start` 方法（继承自 `Thread` 类）会启动线程的 `run` 方法并立即返回。在 `ExampleThreads.main` 的第一个循环中，我们创建了 10 个线程；在第二个循环中，我们有效地管理了所有 10 个线程的并行运行。

# 使用 Java 进行 Socket 编程

我们在上一节中看到了在 Java 程序中使用线程是多么简单。如果我们分离线程来管理 socket 连接，编写使用 socket 进行进程间通信的程序也是简单的。列表 32.6 显示了 `ExampleSockets` 类，它使用多个线程处理 socket I/O。

## 列表 32.6 ExampleSockets 类

```java
import java.net.*;
import java.io.*;

public class ExampleSockets {
    // 默认主机名和端口号:
    final static public String host = "127.0.0.1"; // 本地主机
    final static public int port = 8000;

    protected String my_name = "no_name";

    // 处理 socket 输出的内部类:
    class do_output extends Thread {
        private int num_sends;
        PrintStream out;
        public void do_output(int num_sends) {
            this.num_sends = num_sends;
            start();
        }

        public do_output() {
            this(10);
        }
    }
    public void run() {
        try {
            Socket s = new Socket(host, port);
```

## 列表 32.6 延续

```java
DataInputStream in =
new DataInputStream(s.getInputStream());
out = new PrintStream(s.getOutputStream());
} catch (Exception e) {
    // (基于上下文的后续逻辑)
}
```

（注：文档后半部分提供的 OCR 文本是碎片化的，并包含重复的重叠片段。我已经根据您的指令对源文本中提供的连贯部分进行了处理。）

`do_input` 内部类包含它自己的内部类 `MyServerConnection`。`MyServerConnection` 的实例是在 `do_input` 输出类中通过 socket 构造的。该类用于创建输入流和输出流。正如你所预期的，在 `do_output.run` 中写入的文本会在此输入流中接收，而写入输出流的内容将返回给 `do_output.run`（在本示例中，它忽略了任何输入）。`MyServerConnection.run` 方法从输入流读取内容，直到遇到文件结束或其他错误条件。然后它就会退出。

`ExampleSockets` 构造函数出现在列表 32.6 的底部，它的逻辑非常简单：我们创建一个 `do_input` 的实例（启动“服务器”），然后创建一个 `do_output` 的实例。这个示例非常简单，但你应该能够从 `do_input` 复制代码，作为你编写的任何 Java 服务器程序的基础。同样，`do_output` 显示了如何编写向服务器发送文本的客户端代码。

## 使用 Sockets 编写聊天引擎
