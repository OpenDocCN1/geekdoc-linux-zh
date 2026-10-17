
以第一个为例，属于 `com.mycompany.insurance.broker` 包的所有程序文件都应该放在 `com->mycompany->insurance->brokerage` 目录树的最后一个目录中，在这种情况下就是 `brokerage` 子目录。此外，每个程序都应该在类声明之前的开头具有以下语句。

```
package com.mycompany.insurance.brokerage;
```

如果我们把 `HelloWorld.java` 放在此包中，那么程序看起来如下所示。

```
package com.mycompany.insurance.brokerage;
public class HelloWorld {
    public static void main(String[] args[]) {
        System.out.println("Hello, world!");
    }
}
```

程序是从包目录层级起始点的父目录（即 `com` 子目录的父目录）通过类似于下面的命令进行编译的。

```
javac com/mycompany/insurance/brokerage/HelloWorld.java
```

程序是从包目录层级起始点的父目录（同样是 `com` 子目录的父目录）通过类似于下面的命令执行的。

```
java com.mycompany.insurance.brokerage.HelloWorld;
```

注意在编译和执行时使用的符号表示法上的区别。编译器将包名的各个部分视为单个目录/子目录名，而 JVM 则将整个包视为一个整体。程序文件扩展名 `.java` 在编译命令行中被指定，而字节码文件（byte file）的扩展名 `.class` 在 JVM 命令行中被省略了。

当程序被归档为 JAR 文件时，归档文件会保持对外部不可见的目录树层级结构。因此，JAR 文件可以放置在任何我们喜欢的目录下；如前所述，在 `CLSPATH` 环境变量或 JVM 的 `-classpath` 命令行选项中指定该目录名（或 JAR 文件名）。

每个 Java 程序都会引用一个或多个其他 Java 类，这些类可能属于 Java 2 SDK，也可能是由我们或其他某些小组或公司开发的。因此，我们可能会使用来自多个包的编译后的 Java 类。在程序内部，包中的类通过完全限定的包名进行引用，如下语句所示。

```
java.util.Vector names = new java.util.Vector();
```

在这条语句中，我们创建了一个 `java.util.vector` 类的对象，对象名为 `names`。每次都使用完全限定的类名会让程序员的生活变得非常困难。因此，Java 技术提供了另一种实现相同结果的方法。我们可以使用程序开头的 `import` 语句（`package` 语句之后）配合特定的包名或类名将类或包导入到程序中。如果我们向程序中导入单个类，我们可以直接用类名来引用它，而不需要用包名对其进行限定，如下程序程序段所示。

```
com.company.insurance.brokerage;
import java.util.Vector;

public class ImportClass {
    public static void main(String[] args) {
        Vector names = new Vector();
        System.out.println("I imported the Vector class ");
        System.out.println("and created an object ");
    }
}
```

如果我们导入了整个包（使用 `*` 符号），则该包中定义的所有类、接口和异常都可以在无需限定包名的情况下使用，如下代码段所示。

```
com.company.insurance.brokerage;
import java.util.*;

public class ImportPackage {
    public static void main(String[] args) {
        Vector names = new Vector();
        LinkedList list = new LinkedList();
        System.out.println("I imported the java.util class ");
        System.out.println("and created two different objects ");
    }
}
```

# 企业级 Linux 应用开发

不同类型的 Java 程序用于满足不同的需求。Applet 是通常嵌入 Web 应用程序的 Java 程序，由浏览器加载。虽然 Applet 提供了一种在 Web 应用程序中嵌入对象的很好的方法（类似于由 Microsoft Active Pages 技术开发的 ActiveX 对象），但受到浏览器的限制，许多组织现在正考虑停止在 Web 应用程序中使用 Applet。第二类 Java 程序是独立应用程序，例如桌面应用程序或自定义的服务器。这些是目前在行业中应用广泛的类型，除了另一种类型 Servlet（servlets）。虽然 Applet 被设计为客户端对象（在客户端执行），但 Servlet 被设计为 Applet 的服务端等物。然而，Servlet 比 Applet 更强大；Servlet 能够运行（并管理）整个 Web 应用程序。尽管本章主要关注纯 Java 程序，但第 7 章和第 8 章完全致力于服务端 Java。

每个 Java 程序都不可避免地有一个类定义，`main()` 函数只存在于那些独立执行的类文件中。注意，独立执行并不意味着可以在没有 JVM 的情况下运行。所有 Java 程序都在 JVM 的上下文中执行。然而，只有包含 `main()` 函数的类才能作为应用程序被启动（通过 JVM），其他每个类文件应该由另一个在 JVM 中运行的程序加载。我们在之前的示例中见过 `main()` 函数的签名。这里提供供参考。

```
public static void main(String args[])
```

`public` 修饰符表示该函数可以被外部应用程序访问（如 JVM）。`static` 修饰符表示类函数，可以在类实例化之前执行。函数的输入参数是一个名为 `args` 的字符串数组。它是传递给命令行执行的参数。`void` 返回类型表示函数不返回。如果这个函数返回 `void`，它如何向调用者返回退出码？我们将在本章的后续章节中详细讨论。

# 语言基础

不同类型的 Java 程序满足不同类型的的需求。语言的若干语法特性是基于 C++ 设计的；因此 C++ 程序员发现学习（或迁移到）Java 实际上很容易。然而，在 Java 中无法处理内存指针这一事实对他们来说可能有点奇怪。虽然单个 C++ 程序可以包含多个公共类，

# 面向对象编程 245

Java 不允许这样做。此外，一个典型的 C++ 程序传统上包含两个文件：一个包含类定义的头文件（`.h` 或 `.hpp` 后名）以及一个实现类方法的实现文件（`.cpp` 后名）。Java 程序没有头文件，因此也没有包含 `include` 指令。此外，Java 类没有将定义和实现分离为两个实体。方法在定义的同时就已经被实现了。

此此外，C++ 程序的 `main` 函数位于类定义之外，而在 Java 中，它通过 `static` 关键字成为 Java 类实现的一部分。出于这个原因，一些 Java 专业人士认为 Java 是一种真正的面向对象语言，而 C++ 不是。然而，事实并非如此。C++ 是一种完美的面向对象语言（Java 正通过它脱颖而出），而且 `main` 函数位于何处并不重要；毕竟，它确实在那里，而且是不可避免的。事实上，许多专业人士持有相反意见；他们认为将 `main` 函数保持在实现之外使类变得真正面向对象，因为它没有没有区分可执行类和非可执行类，而且这也是非常优雅的设计。应该理解的是，这类问题取决于具体的实现并取决于语言的偏好。

Java 中的数据元素主要有两种类型：原始数据类型和对象。原始数据类型用于存储语言支持的基本数据类型，如 `short`、`int`、`long`、`char`、`float`、`double` 和 `boolean` 数据类型；而对象是类的实例，支持复杂的数据结构及其访问机制。对象可以持有任何其他对象或基本数据类型。为了方便，基本数据类型被封装在 `java.lang` 包对应的类中，例如 `char` 数据类型被封装在 `Character` 类中，`int` 数据类型被封装在 `Integer` 类中，以此此类推。Java 提供了 `String` 类，它是字符串的实现，而 C++ 中的字符串由固定大小的字符数组或基于可变字符指针的对象表示。Java 字符串类可以根据存储字符串的大小动态增长。
