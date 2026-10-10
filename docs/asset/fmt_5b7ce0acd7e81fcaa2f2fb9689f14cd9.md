
不仅变量可以声明为静态的，方法也可以是静态的。可以通过在类名后加点和方法名来调用静态方法。

# Java 编程
第 25 章 805

当你调用 JVM 时，它期望接收类名作为参数。该类应该有一个名为 `main` 的静态方法，该方法必须是 `public` 的，并且接收一个字符串数组作为其唯一参数。

当我们使用 `Math.sqrt()` 时，我们是在调用 `Math` 类的一个静态方法。`System.out.println()` 的意思是访问 `System` 类中一个名为 `out` 的静态变量，该变量包含一个 `PrintStream` 对象的引用，我们调用了它的 `println()` 方法。

## 接口

如果你仔细分析继承，你会发现它将两种不同的特征合为了一个特征。其中之一是能够用通用术语描述一类对象的能力：所有的 `Points` 或继承自它的任何类都可以通过调用它们的 `print` 方法进行打印。另一个特征是它允许你复用实现（例如 `Location` 利用了在 `Point` 类中实现的 `distanceTo()` 方法）。

几年前，使用继承进行代码复用被认为是面向对象编程的最优秀特性之一，但现在许多人认为它更多地像是一个负担而不是资产，因为它可以使程序更难理解和维护。

另一方面，使用继承来将接口指定为方法的抽象列表，并使其能够应用于任何实现（继承）该接口的对象，这被广泛认为是现代面向对象编程的基石之一。

在 Java 中，你可以定义一个接口，它类似于一种类，你只对其定义可用的方法、参数和返回值，而永远不编写实现代码。

一个类可以实现任意数量它想要的（或需要的）接口。要实现一个接口，它只需要声明此项意图（使用 `implements` 关键字），并为接口中定义的每个方法提供实现。

作为一个示例，我们写了一个简单的命令解释器，它可以在运行时动态加载新命令。

命令的主要特征是它可以被执行。我们用 `Executable` 接口来表示这个概念：

```java
public interface Executable {
  void execute();
}
```

`Executable` 接口规定，一个对象要变为可执行，它的类必须实现一个无参数且返回 `void` 的 `execute()` 方法。这段代码单独存放在 `Executable.java` 文件中。

这里是 `Ex1.java`，`Executable` 的简单实现：

```java
public class Ex1 implements Executable {
    void execute() {
        System.out.println("I am Ex1!");
    }
}
```

为了给命令解释器增加一些变化，这里是 `Ex2.java`，`Executable` 的另一个实现：

```java
    void execute() {
        System.out.println("Ex2:");
        for (int i = 0; i < 3; i++)
            System.out.println(i);
    }
}
```

### 列表 25.13 示例10

```java
import java.io.*;
public class Example10 {
    public static void main(String[] args) throws IOException {
        BufferedReader reader =
            new BufferedReader(new InputStreamReader(System.in));
        MainLoop:
            while (true) {
                System.out.print("*>>>: ");
                String command = reader.readLine();
                if (command == null)
                    break MainLoop;
                command = command.trim();
                if (command.equalsIgnoreCase("end"))
                    break MainLoop;
                try {
                    Executable executable =
                        (Executable) Class.forName(command).newInstance();
                    executable.execute();
                } catch (Exception e) {
                    System.out.println("Command failed: " + e);
                }
            }
            System.out.println("Bye!");
    }
}
```

# Java 编程
第25 章

如果你感到有些困惑，不要担心。你只需要理解：`Class.forName("AnyClass").newInstance()` 会创建一个 `AnyClass` 类的实例。通过 `Class.forName("Point").newInstance()`，你创建了一个 `Point` 类的实例。

既然直接说 `new Point()` 那么简单，为什么还要用这么复杂的方法呢？当我们使用 `new` 算符时，我们必须在编译时就知道我们想要为哪个类创建实例。而使用这种方法，我们可以在运行时从用户指定的任何类创建对象。这正是我们在可扩展命令解释器中想要做的。

我们将所使用的命令类型作为类名。我们为该类创建一个实例。我们假设它实现了 `Executable` 接口（通过将 `newInstance()` 返回的对象强制转换为 `Executable`）。最后，我们告诉该执行对象去执行自身。

所有这些代码都在一个 `try-catch` 块中，这样如果用户输入的命令不是类、如果该命令是一个没有实现 `Executable` 的类，或者在执行 `Executable` 时抛出了异常，我们的解释器都不会崩溃。

退出循环后，让用户知道程序正在退出：

```
}
System.out.println("Bye!");
}
n
```

以下是我们编译这些类并运行程序后发生的情况：

```
$ java Example10
>>>Exe1
I am Ex1!
>>>Exe2
Exe2:
0
1
>>>Point
Command failed: java.lang.ClassCastException
>>>Exe3
Command failed: java.lang.ClassNotFoundException: Exe3
>>>
```

通过动态加载 `Exe1` 和 `Exe2`，“理解”了前两个命令。当你尝试执行 `Point` 时，错误信息表明 `Point` 没有实现 `Executable` 接口，因此无法转换为 `Executable`。

## 810 开发环境
第四部分

最后一个命令显示了尝试加载一个不存在的类时发生的情况。

现在，让我们尝试一些有趣的东西：在不退出解释器的情况下，打开另一个窗口来输入并编译 `Exe3.java`：
`public class Exe3 implements Executable {`

```java
    public void execute() {
        System.out.println("This is the new executable: Exe3");
}
```
