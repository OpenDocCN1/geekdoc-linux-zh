
```java
public class MakeShape {
    public static void main(String[] args[]) {
        Shape shapes[] = new Shape[2];
}
```

```java
shapes[0] = new Circle(100.0, 100.0, 50.0);
shapes[1] = new Rectangle(80., 40., 120., 60);
```

`main`方法创建了一个`Shape`对象数组并用不同的形状初始化该数组。然后调用了每个形状的`computeArea`和`draw`方法。

### 洞察

在 Java 中，你使用`new`关键字来创建对象的实例。没有对应的`delete`或`free`关键字来在你不再需要对象时将其移除。相反，Java 支持一种称为“垃圾收集”的技术来自动销毁不再的对象（Java 会跟踪所有指向对象的引用，并在没有更多引用指向它时移除该对象）。这意味着你永远不需要担心在 Java 中释放内存。因为内存管理是 C 和 C++ 程序中许多错误的根源，Java 对垃圾收集的支持有助于消除你应用程序中潜在错误的一个大源。

在这个示例中，`MakeShape`类就是 Java 应用程序。要编译该程序，输入以下命令：

```bash
javac MakeShape.java
```

这一步处理了编译`MakeShape.java`文件以及所有相关的类（`Shape.java`、`Circle.java`和`Rectangle.java`文件）。换句话说，Java 编译器（`javac`）类似于 UNIX 中的实用程序——`javac`确定类之间的依赖关系并编译所有必要的类。

要运行`MakeShape`程序，使用 Java 解释器，如下：

```bash
Java MakeShape
```

下面的列表显示了在 Red Hat Linux 窗口中运行`MakeShape`程序的结果：

```
Shape #0
Circle of radius 50.0 at (100.0, 100.0)
Area = 7853.98163394483
---------------------

Shape #1
Rectangle with corners (80.0, 40.0) and (120.0, 60.0)
Area = 800.0
--------------------
```

## Java 程序结构

一个 Java 程序由一个或多个类组成。对于独立应用程序，你必须有一个具有`public static void main`方法的类。Applet 只需要`Applet`类的子类。

Java 2 SDK 扩展了源文件使其与类具有同名，但带有`.java`扩展名（因此，名为`Circle`的类定义在`Circle.Java`文件中）。然而，其他 Java 开发环境可能会有不同的文件命名约定。

在每个源文件中，程序的部分按以下方式布局：

1. 文件开头会有一些注释，描述类的用途并提供其他信息，如作者和修订日期。Java 支持 C 和 C++ 风格的注释。在 ANSI C 中，注释以`/*`开始并以`*/`结束。或者也可以简单地用双斜杠`//`开始一行注释。一种特殊类型的注释，称为文档注释（doc comment），以`/**`开始并以`*/`结束。文档注释可以由`javadoc`工具提取，以为类创建在线文档。

2. 一个或多个`import`语句允许你使用抽象类。例如，如果你使用`java.applet.Applet`类，你可以通过提供的短名`Applet`来引用它，只需在源文件中包含`import`语句：

```java
import java.applet.*;
```

3. 类定义包含了实例变量和方法。所有变量和方法必须在类定义内部。

注意，`import`语句并没有真正向类中引入任何额外的代码；它是一种节省打字的简单方法，让你通过较短的名字引用类（例如用`Applet`代替`java.applet.Applet`）。

## Java 中的基本数据类型

Java 支持标准的 C 数据类型`char`、`short`、`int`、`long`、`float`、`double`。此外，Java 还引入了`byte`和`boolean`类型。然而，与 C 不同，Java 还规定了所有基本数据类型的精确大小。

| 类型 | 描述 |
| :--- | :--- |
| boolean | 一个包含 true 或 false 的 1 位值 |
| byte | 一个在 -128 到 127 之间的 8 位整数 |
| char | 一个在 -32768 到 32767 之间的 16 位 Unicode 字符 |
| short | 一个在 -32768 到 32767 之间的 16 位整数 |
| int | 一个在 -2147483648 到 2147483647 之间的 32 位整数 |
| long | 一个在 -9223372036854775808 到 9223372036854775807 之间的 64 位整数 |
| float | 32 位单精度浮点值 |
| double | 64 位双精度浮点值 |

尽管大多数基本类型对 C 来说很熟悉，但在 Java 中不允许以下用法：

- Java 中没有`unsigned`关键字；所有整数值都是符号的。
- 你不能写`short int`或`long int`（这些组合在 C 中经常使用）。

## Java 中的非基本数据类型

Java 中的基本类型是对象和数组。所有的非基本类型都通过引用处理——这意味着当你将非基本类型传递给方法时，传递的是对象的地址。然而，基本类型是按值传递的——这意味着传递给方法数据的拷贝。

与 C 不同，Java 没有任何指针类型。因此，你不能使用`*`和`&`运算符处理变量地址。通过消除指针，Java 消除了一个常见的错误源，并防止程序员通过指针技巧绕过 Java 的安全机制。

相反，你必须通过引用处理对象（引用是对象的地址）。你需要理解通过引用处理对象的以下影响：

- 当你将一个对象赋值给另一个时，Java 并没有真正复制对象的值。发生的是你得到了指向同一个对象的引用。考虑以下示例：

```java
Circle c1 = new Circle(0., 0., 20);
Circle c2 = new Circle(100.0, 60.0, 20.0);
c1 = c2; // c1 指向与 c2 相同的 Circle 对象
```

在这里，`c1`和`c2`都指向同一个`Circle`对象。当你将`c2`赋值给`c1`后，`c1`原本指向的对象就丢失了（Java 垃圾回收器会自动回收分配给丢失对象的内存）。

- 要实际将对象的值复制到另一个对象中，你需要调用对象的`clone`方法（这假设该对象支持`clone`方法）。这是一个示例：

# 第 26 章：Java 编程 853

```java
Vector x = new Vector();
Vector y = x.clone(); // Vector y 是 Vector x 的拷贝
```
当你使用`==`运算符时，你是在检查两个变量是否引用同一个对象。换句话说，`==`运算符检查两个对象是否完全相同（标识）。要检查两个独立对象是否包含相同的值，你必须使用该对象类型的特殊方法。例如，许多 Java 类都提供了`equals`方法来检查对象值的相等性

### String 类型

Java 包含一个内置的`String`类型，编译器几乎将`String`视为一种基本数据类型。Java 的`String`类是`java.lang`包的一部分，编译器默认使用该包。

Java 编译器会自动将双引号（"..."）内的文本转换为`String`。此外，`+`运算符用于用于连接（拼接）`String`对象。例如，你可以编写如下代码：

```java
String welcome = "Welcome to " + "Java.";
int numchars = welcome.length();
System.out.println("There are "+numchars+
 characters in: "+welcome);");
```

执行此代码时，将打印以下内容：

There are 16 characters in: Welcome to Java.

`String`类支持许多其他方法，提供了 C 语言字符串处理函数的功能（定义在 C 头文件`<string.h>`中）。Java 包含两个相关的类来处理文本字符串：

- `String`：用于存储无法单独操作的字符字符串（换句话说，你不能在字符串中插入或替换字符）
- `StringBuffer`：用于表示可以需要进行操作的字符字符串。你可以在`StringBuffer`对象中追加、插入和替换字符。

表 26-3 总结了`String`类的方法。

| 方法 | 描述 |
