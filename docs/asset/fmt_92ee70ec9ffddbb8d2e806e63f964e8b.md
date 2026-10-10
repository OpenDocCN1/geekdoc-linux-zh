
## 第 13 章 对象流与 RMI

在我们对对象流的讨论中，你看到过示例代码，其中服务器可以相加或减两个浮点数（`float`），并以数组的形式向服务器返回一个浮点数值。在这里，我们开始将其转换为 RMI。以下是描述远程服务的远程接口：

```java
import java.rmi.*;
public interface MathServices extends Remote {
    public float add(float[] addUs)
    throws RemoteException;
    public float subtract(float[] subtractUs)
    throws RemoteException;
}
```

注意，这个接口满足了它的要求：它继承了 `Remote`，并且它的方法抛出 `RemoteException`。现在让我们看看如何使用该远程接口。

### 第 2 步：创建远程类（Remote Class）

远程接口由远程类和存根实现。在这里我们将查看远程类。类由服务器构造，然后供远程调用使用。

对远程类有两个要求：

- 它必须继承 `java.rmi.server.UnicastRemoteObject`。
- 它必须实现该远程接口。

远程类是 RMI 系统的核心工作单元。它是其方法为客户端提供服务的类。这里有一个提供我们数学示例中服务的远程类：

```java
import java.rmi.*;
import java.rmi.server.*;
public class Mathematician
    extends UnicastRemoteObject
    implements MathServices {

    public Mathematician() throws RemoteException {
    }

    public float add(float[] addUs)
        throws RemoteException {
        return addUs[0] + addUs[1];
    }

    public float subtract(float[] subtractUs)
        throws RemoteException {
        return subtractUs[0] - subtractUs[1];
    }
}
```

该类唯一棘手的部分是构造函数。`java.rmi.server.UnicastRemoteObject` 抛出 `java.rmi.RemoteException`，因此子类必须显式提供一个也抛出此异常的构造函数，即使构造函数体什么都不做。

现在让我们如何制作存根。

### 第 3 步：创建存根（Stub）

对于每个方法要用于 RMI 用的类，必须创建一个存根。存根和远程类都实现了远程接口。在客户端侧，远程引用指向存根的实例。存根也用于服务器端。

存根是使用 `rmic` 工具创建的，而不是通过编写和编译 Java 源代码。`rmic` 位于 JDK 的 `bin` 目录下，如果你可以编译和执行，它就已经在你的路径中了。要创建存根，输入 `rmic remote_class_name`。

> 要学习 `rmic` 的所有命令行参数，请输入 `rmic`。

在我们案例中，远程类名是 `Mathematician`，因此相应的存根通过输入 `rmic Mathematician` 创建。

如果远程类在一个包中，则必须提供全名。例如，如果 `Mathematician` 在一个名为 `services` 的包中，那么你应该输入 `rmic services.Mathematician`。

`rmic` 的输出是一个类文件名，其中远程类名后面附加了 `_Stub`。在我们的示例中，存根被称为 `Mathematician_Stub`。

现在核心部分已经创建完成：远程接口、远程类和存根。下一步是创建服务器和客户端代码。

### 第 4 步：创建服务器（Server）

RMI 服务器是一个创建一个或多个远程对象并使其对客户端可用的应用程序。创建 RMI 服务器并不完全易事，因为需要与 RMI 注册表（RMI registry）交互。

RMI 注册表是一个将名称与 RMI 服务关联的程序。服务为它提供的每个远程对象提供一个名称。客户端通过指定服务器和对应名称来访问远程对象。通常，注册表中的名称是对它们所代表服务的描述。选择良好的服务名称与选择变量名一样重要。

RMI 注册表是一个独立于任何 JVM 的进程。它必须在任何 Java 之前运行。要启动注册表，在命令行输入 `rmiregistry`。该程序位于 Java `bin` 目录下。单台机器上，多个 Java 应用程序可以通过注册表提供服务。应用程序通过 `java.rmi.Naming` 类访问注册表，该类所有方法都是静态的。要将名称与对象关联，服务器应调用 `Naming.rebind()`，其签名如下：

```java
public static void rebind(String name, Remote obj)
```

参数是访问远程对象的名称。参数是远程对象本身；它的类型是 `Remote` 而不是 `Object`，因为远程对象实现了继承 `Remote` 的接口。你可以取消绑定名称（即告诉注册表该名称不再对应该对象）。只要有一个远程对象绑定，服务器就会运行。

服务器执行两个任务：

1. 创建远程对象的实例。
2. 将远程对象绑定到名称。

这是我们示例的服务器。服务名称为 `brainiac`。

```java
import java.io.*;
import java.rmi.*;
public class MathServer {
    public static void main(String[] args) {
        try {
            Mathematician m = new Mathematician();
            Naming.bind("brainiac", m);
        } catch (RemoteException x) {
            System.out.println("Remote Exception stress " + x);
        } catch (IOException x) {
            System.out.println("Other IOException stress " + x);
        }
    }
}
```

记得远程对象继承 `UnicastRemoteObject`，因此它们的构造函数抛出 `RemoteException`。`Naming.bind()` 调用 `IOException` 的各种子类。

### 第 5 步：创建客户端（Client）

客户端通过连接服务器机器上的 RMI 注册表获取远程引用。这是通过调用 `Naming` 类的静态方法 `lookup()` 实现。`lookup()` 的签名如下：

```java
public static Remote lookup(String name)
```

签名中似乎缺少了什么。提供了对象名称，但没有提供服务器主机名。RMI 基础设施如何知道要连接哪个主机？

`name` 参数实际上指定了服务器主机名和对象名称，采用 URL 格式。该字符串的格式为：

```
rmi://server_hostname/object_name
```

对象名称必须是绑定到服务器注册表（registry）对象的名称。除了对象名称外，省略其他部分是允许的。在这种情况下，RMI 基础设施将使用本地主机作为服务器。这对于调试非常方便，因为你可以在单台机器上开发代码。

`Naming.lookup()` 的返回类型是 `Remote`，它是远程接口的子类。返回的值应该强制转换为远程接口类型。

获取远程引用后，对该远程引用的调用将自动发送到服务器。从程序员的角度来看，普通调用与 RMI 调用之间的唯一区别是所有 RMI 调用都会抛出 `RemoteException`。这里有一个使用 RMI 远程调用 `brainiac` 服务 `add()` 和 `subtract()` 方法的客户端：

```java
import java.io.*;
import java.rmi.*;
public class MathClient {
    public static void main(String[] args) {
        try {
            // 获取远程引用。
            String url = "rmi://" + args[0] + "/brainiac";
            MathServices ms = (MathServices)Naming.lookup(url);

            // 加法。
            float[] addUs = { 12.34f, 56.78f };
            float sum = ms.add(addUs);
            System.out.println("Sum = " + sum);

            // 减法。
            float[] subtractUs = { 99.99f, 76.54f };
            float difference = ms.subtract(subtractUs);
            System.out.println("Difference = " + difference);
        } catch (NotBoundException x) {
            System.out.println("Name stress * " + x);
        } catch (RemoteException x) {
            System.out.println("Remote Exception stress * " + x);
        } catch (IOException x) {
            System.out.println("Other IOException stress " + x);
        }
    }
}
```

用户在命令行上提供所有远程服务器主机名。此时，所有必要的代码已编写完毕。剩下的就是部署并执行客户端和服务器应用程序。

### 第 6 步：启动程序

在启动构成 RMI 程序的程序之前，你需要确保正确的文件存在正确的机器上。记住，远程接口和存根（stub）必须同时部署在服务器和客户端上。各种程序必须按照以下顺序启动：

1. 服务器的 RMI 注册表
2. 服务器
3. 客户端或多个客户端

RMI 注册表必须首先启动。如果服务器应用程序调用 `Naming.rebind()` 时它尚未运行，则会抛出异常。接下来应该启动服务器，这样当客户端调用 `Naming.lookup()` 时，远程对象将可用。客户端应该是最后启动的应用程序。

## 总结

本章讨论了客户端/服务器通信的两种方案：对象流和 RMI。对象流使用 Java 的 `Socket` 和 `Server` 类。虽然它们使用起来简单，但选择这种设计会迫使你创建一个协议和某种命令类。构建在对象流之上的 RMI 让你免于处理许多低级任务，包括协议设计和命令类的维护。然而，通过 RMI，你承担了一些高级任务，包括与 RMI 注册表的交互，以及存根类的创建和部署。

这两种方法各有优劣。如果你熟悉所有的成本和收益，那么在决定在项目中使用哪种策略时，你将能够做出明智的决策。

## 现实世界场景

## 章节练习

在本次练习中，你将创建一个生成天气报告的气象站客户端/服务器应用程序。当客户端连接服务器时，它们可以请求预报或温度。当然，本次练习的重点是练习 Java 网络编程，所以天气报告不需要基于现实。可以随心从一组字符串中随机选择预报——不要表现得像雨天（Rainy）、晴天（Sunny）或粘液体（Oobleck）。为温度生成随机数。

实现两个解决方案：一个使用对象流，另一个使用 RMI。这项工作将让你接触到这两种技术，因此当你决定在项目中使用哪一个时，你将能够做出良好的选择。

可能的解决方案集出现在你 CD-ROM 的 `solutions\Chapter_13` 文件夹中。

# 第 14 章 整合一切

![](img/09f8389b7ae2705d1ab14be2d5e857e3_495_0.png)

![](img/09f8389b7ae2705d1ab14be2d5e857e3_496_0.png)

到此时，你已经有了全局观。你了解如何创建一个访问磁盘文件中数据的服务器。你了解如何创建一个 Swing GUI 客户端。你了解如何使用对象流或 RMI 连接服务器和客户端。本章讨论了许多微小的、无关的问题，这些问题可能会极大影响你在开发者考试（Developer's Exam）中的成绩。这些是 Javadoc、线程以及额外问题。

## Javadoc

Javadoc 处理源文件为你的类生成 API。要创建页面，请确保所有公共方法都附有 Javadoc 注释。默认情况下，`javadoc` 会记录类的所有公共和保护特性，即使它们没有注释。然后对你的源码运行 `javadoc`。结果是专业的 HTML 文件，包括索引、包概览（如果包中有其他内容）以及类页面。类页面显示类层次结构、实现的接口列表、字段/方法摘要以及字段/方法详情。事实上，`javadoc` 生成了人们对类所需的一切，除了类描述以及字段、构造函数和方法的详细信息。这些信息必须由程序员以 Javadoc 注释的形式提供。Javadoc 注释以 `/**` 开始，到下一个 `*/` 结束。紧邻类定义的 Javadoc 注释成为 API 页面上的描述。紧邻字段或方法的 Javadoc 注释成为该字段或方法的描述。这里是我们带有类描述的类：

```java
package xyz;
import java.util.*;
import java.io.*;

/**
一个包含字符串且提供有限的 Vector。
 */
public class VectorOfStrings extends Vector<String> {
    public int x;
    public int y;

    public String getString(int n) throws IOException {
        if (Math.random() > 0.5)
            throw new IOException();
        return "VectorOfStrings";
    }
}
```

可以通过添加标签让类描述更加丰富。这些是出现在 Javadoc 注释内部的特殊代码。例如，你可能希望某些文本以等宽字体显示；这通常用于引用代码时。在我们的示例中，`Vector` 应该使用程序字体。为了实现这一点，在文本之前插入 `<code>`，在文本之后插入 `</code>`：

```java
/**
一个 <code>Vector</code> 包含字符串且提供有限的。
 */
```

你可以通过在运行文本之前插入 `<i>`，在运行之后插入 `</i>` 来将某些文本渲染为斜体。因此，如果 `VectorOfStrings` 类确实提供非常有限的内容，你可以这样注释：

```java
/**
一个 <code>Vector</code> 包含字符串且提供<i>very</i>有限的。
 */
```

另一组以 @ 开头的标签一直延伸到行尾。这些 @tags 如下：

- `@author`
- `@version`
- `@see`
- `@return`
- `@param`
- `@throws`

这些标签中的前三个用于注释类。后三个出现在方法注释中。这里有一个经过完整注释的 `VectorOfStrings` 类，它使用了你到目前为止见过的每种标签：

```java
package xyz;
import java.util.*;
import java.io.*;

/**
 * @author   Philip Heller
 * @version  1096.1
 * @see      java.util.List
 */
public class VectorOfStrings extends Vector<String> {
  /**
  仅仅是一个 int。
  */
  public int x;

  /**
  仅仅是另一个 int。
  */
  public int y;

  /**
  @return  返回一个与类名不完全相同的常量字符串。
  @param   <code>n</code> 被忽略了。
  @throws IOException 大约一半的概率随机抛出 IOException。
  */
  public String getString(int n) throws IOException {
    if (Math.random() > 0.5) {
      throw new IOException();
    }
    return 'Vector-o-Strings';
  }
}
```

如你所见，`@return` 用于记录方法的返回值，`@param` 用于记录参数，`@throws` 用于记录异常。使用这些代码为所有公共方法中的所有返回值、所有参数和所有异常提供描述。由于你的作业不需要你记录受保护的字段或方法，请使用 `-public` 标志来告诉 `javadoc` 忽略所有非公共特性。

## 线程问题

你的服务器要求是多线程的。这意味着，在服务于多个同时客户端时，它必须表现恰当。在设计项目的这部分时，有几个问题是你应该留意的。
