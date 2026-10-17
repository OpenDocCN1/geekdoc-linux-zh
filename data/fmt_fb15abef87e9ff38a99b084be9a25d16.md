
如果你实现了一个接口的所有方法，你可以在类定义中使用 `implements` 关键字来声明这一事实。例如，如果一个类定义了 `run` 方法（这构成了 `Runnable` 接口），则类定义将如下所示指定这一事实：

## Java 中的线程 (Threads in Java)

Java 内置了对线程的支持。线程指的是单一的控制流——由 Java 虚拟机执行的单个字节码序列。就像操作系统可以执行多个进程（通过为每个进程轮流分配短时间的处理器时间），Java 虚拟机可以在单个应用程序内执行多个线程。你可以将线程认为是“单个进程内的多任务处理”。

线程非常有用，因为你可以针对不同的任务集灵活地调度单个线程。例如，一个线程可以监控 applet 的所有用户输入，而另一个线程可以定期更新显示内容。线程的问题在于它们都共享程序中的同一组变量。这意味着每个线程在访问和更新任何变量时都必须小心。当一个线程更改对象的部分时，它可能会失去它的时间片，而另一个线程变为激活状态并使用部分更新的对象。Java 包含了 `synchronized` 关键字，允许你标记不应被多个线程同时访问的对象和方法。例如，你编写以下代码以确保线程在执行大括号 `{...}` 内的语句之前获取 `myObject` 的锁：

```java
synchronized(myObject)
{
    // Some task that needs to be synchronized among threads
    // ...
}
```

![](img/b418dfc0d37b54b9876d5e801170c507_891_0.png)

## 在 Applet 中使用线程 (Using Threads in an Applet)

理解线程最好的方法是学习一个简单的示例。下面的列表显示了 `DigitalClock` applet，它使用线程来显示当前和时间：

```java
// File: DigitalClock.java
// Displays a digital clock using a thread.
import java.util.*;
import java.awt.*;
import java.applet.*;

public class DigitalClock extends Applet implements Runnable
{
    private volatile Thread clockThread;
    int interval = 1000;
    // The run method is required by the Runnable interface
    public void run()
    {
        Thread curThread = Thread.currentThread();
        while(curThread == clockThread) {
            try {
                curThread.sleep(interval);
            } catch(InterruptedException e) {}
        }
        // Repaint the clock.
        repaint();
    }
    public void start() {
        // Create and start the clock thread.
        clockThread = new Thread(this);
        clockThread.start();
    }
    public void stop() {
        // Get rid of the clock thread.
        clockThread = null;
    }
    // The paint method displays the date and time.
    public void paint(Graphics gc) {
        Font font = new Font("Helvetica", Font.ITALIC, 16);
        gc.setFont(font);
        gc.drawString(new Date().toString(), 4, 20);
    }
}
```

将此列表保存在 `DigitalClock.java` 文件中并并以下命令编译 applet：

```bash
javac DigitalClock.java
```

接下来，创建一个 HTML 文档 `DigitalClock.html`，并如下所示嵌入 applet：

```html
<html>
<body>
<applet width=200 height=240 code=DigitalClock>
a Java clock applet.
</applet>
</body>
</html>
```

现在，输入以下命令使用 `appletviewer` 运行 applet：

```bash
appletviewer DigitalClock.html
```

图 26-3 显示了带有 Clock applet 输出的 `appletviewer` 窗口。

![](img/b418dfc0d37b54b9876d5e801170c507_893_0.png)

图 26-3：在 appletviewer 中每秒运行一次 Clock Applet。

applet 运行后，它应该每秒更新一次时显示。

## 理解 Applet 中的线程用法 (Understanding Thread Usage in an Applet)

在看到 `DigitalClock` applet 运行后，你应该查看其列表了解线程是如何工作的。在查看 `DigitalClock` applet 的代码时，你应该注意以下几点：

- 要创建一个线程，你需要实现 `Runnable` 接口的类实例。然后你可以通过以下方式创建 `Thread` 对象：

```java
myThread = new Thread(this);
```

- 当 `Runnable` 线程启动时，Java 虚拟机 (JVM) 会调用 `run` 方法：

```java
thread.start();
```

- 当你想停止线程时，可以将其设置为 `null`：

```java
thread = null;
```

- 垃圾回收机制会清理线程。

- 为了同步对象，使用 `synchronized` 关键字：

```java
synchronized(object)
{
    // ...
}
```

- GUI 应用使用 `paint` 方法在屏幕上绘图。

## Java 中的 GUI 应用 (GUI Applications in Java)
