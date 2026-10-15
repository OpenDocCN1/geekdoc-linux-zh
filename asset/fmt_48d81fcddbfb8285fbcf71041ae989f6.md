
## 8.16 时间类案例研究：创建包 401

在导入声明的末尾使用星号 (`*`) 告知编译器 `java.util` 包中的所有类都可以在程序中可用。这被称为“按需导入类型”（type-import-on-demand declaration）。JVM 只会加载程序中用到的来自 `java.util` 的类。之前的导入（import）允许你在程序中使用 `java.util` 包中任何类的简单名。在本书中，为了清晰起见，我们使用单类型导入声明。

![](img/1df0d1e8ac6007b95647eb8ea38390af_446_0.png)

## 常见编程错误 8.12

使用 `import java.*;` 会导致编译错误。你必须指定想要导入类的确切包名称。

## 在编译期间指定类路径 (Classpath)

在编译 `TimePackageTest` 时，`javac` 必须找到 `Time` 的 `.class` 文件，以确保类 `Time1` 正确使用了 `Time`。编译器使用一个名为类加载器（class loader）的特殊对象来定位类。类加载器首先搜索与 JDK 捆绑的标准 Java 类。然后它搜索可选包。Java 提供了一了一种扩展机制，允许将可选包添加到 Java 中以供开发和执行。[注意：扩展机制超出了本书的范围。欲需更多信息，请访问 java.sun.com/java/6/docs/technotes/extensions/]。如果不在标准 Java 类或存储的扩展类中找到该类，类加载器将搜索类路径。类路径由一系列目录或归档文件组成，在 Windows 上用分号 (`;`) 分隔，在 UNIX/Linux Mac OS 上用冒号 (`:`) 分隔。归档是包含其他文件目录的单个文件，通常为压缩格式。例如，你的程序使用的类包含在 `rt.jar` 归档文件中，它随 JDK 安装。扩展。类路径中指定的目录和归档文件包含了你希望让 Java 编译器和 JVM 可用的类。

默认情况下，类路径仅包含当前目录。然而，可以通过以下方式修改类路径：
- 1. 向 Java 编译器提供 `-classpath` 选项
- 2. 设置 `CLASSPATH` 环境变量（这是一个你和你操作系统维护的特殊变量，以便应用程序在指定位置搜索类）

有关类路径的更多信息，请访问 java.sun.com/javase/6/docs/technotes/tools/index.html。标题为“General Information”（常规信息）的部分包含了关于为 UNIX/Linux 和 Windows 设置类路径的信息。

## 常见编程错误 8.13

![](img/1df0d1e8ac6007b95647eb8ea38390af_446_1.png)

指定显式类路径会将当前目录从类路径中排除（包括当前目录中的包的加载）。如果必须从当前目录加载类，请在类路径中包含一个点 (`.`) 以指定当前目录。

## 第 8 章 类与对象：深入观察

### 软件工程观察 8.16

通常情况下，使用编译器的 `-classpath` 选项而不是 `CLASSPATH` 环境变量来指定程序的类路径是更好的做法。这使得每个应用程序都能拥有自己的类路径。

### 错误预防提示 8.3

使用 `CLASSPATH` 环境变量指定类可能会导致在使用不同版本相同包的程序中出现微妙且难以定位的错误。

对于图 8.18 和图 8.19 的示例，我们没有使用显式类路径。因此，为了为 `Next` 加载 `com.dete1.jht7.ch08` 包中的类，类加载器会在当前目录查找包中的第一个名称——`com.Next`，类加载器搜索目录结构。目录包含子目录 `dete1`。目录包含子目录 `jht7`。最后，目录 `jht7` 包含子目录 `ch08`。在 `ch08` 目录下有文件 `Time1.class`，它由类加载器加载以确保该类在我们的程序中被正确使用。

## 执行应用程序时指定类路径

当你执行一个应用程序时，JVM 必须能够定位该应用程序使用的类。与编译器一样，`java` 命令也使用类加载器首先搜索标准类和扩展类，然后搜索类路径（默认认为当前目录）。JVM 的类路径可以使用用于编译器的任一种技术来指定。对于编译器，最好通过 JVM 的命令行选项指定单个程序的类路径。你可以在 `java` 命令中通过 `-classpath` 或 `-cp` 命令行选项指定类路径，后跟一系列目录或归档文件，在 Windows 上用分号 (`;`) 分隔，在 UNIX/Linux/Mac OS 上用冒号 (`:`) 分隔。如果必须从当前目录加载类，请确保在类路径中包含一个点 (`.`) 以指定当前目录。

## 8.17 包访问

如果方法在类中声明时没有指定访问修饰符（public、private 或 protected——将在第9 章讨论），则该方法或变量被认为具有包访问权限（package access）。然而，在一个使用了同一包中多个类的程序中，这些类可以通过对适当类对象的引用直接访问彼此的包访问成员。

图 8.20 中的应用程序演示了包访问。该应用程序在一个源文件中两个类——`PackageDataTest` 类（第 5–21 行）和 `PackageData` 类（第 24–41 行）。当你编译此程序时，编译器会生成两个独立的文件——`PackageTestData.class` 和 `PackageData.class`。编译器将两个 `.class` 文件放在同一个目录下，因此这些类被认为是同一个包的一部分。由于它们属于同一个包，`PackageDataTest` 被允许修改 `PackageData` 对象的包访问数据。

在 `PackageData` 类声明中，第 26–27 行声明了实例变量 `number` 和 `string`——因此，这些是包访问实例变量。`PackageDataTest` 应用程序的 `main` 方法可以创建 `PackageData` 类的实例（第 9 行），以演示修改 `PackageData` 实例的能力

![](img/1df0d1e8ac6007b95647eb8ea38390af_447_0.png)

图 8.20 | 类包访问成员可以被同一包中的其他类访问。

## 第 8 章 类与对象：深入观察

### 8.18（可选）GUI 和图形案例研究：在图形中使用对象

到目前为止你看到大多数图形在每次执行程序时都是不一样的。然而，练习 6.2 要求你创建一个随机生成形状的程序。在那个练习中，绘图每次调用时都会变化。为了创建一个在每次绘制时保持一致的图形，我们必须存储关于显示形状的更多信息。为此，我们将创建一组形状类来存储每个形状的信息。通过提供一个 `Graphics` 对象让这些类能够自己绘制，使它们变得“智能”。图 8.21 定义了 `MyLine`，它具有所有这些能力。

```
// 图 8.21: MyLine.java

// MyLine 类的声明

import java.awt.Color;

import java.awt.Graphics;

public class MyLine {

    private int x1; // 起点的 x 坐标

    private int y1; // 起点的 y 坐标

    private int x2; // 终点的 x 坐标

    private int y2; // 终点的 y 坐标

    private Color color; // 形状的颜色

    // 带输入值的构造函数

    public MyLine(int x1, int y1, int x2, int y2, Color color) {

        this.x1 = x1; // 设置起点的 x 坐标

        this.y1 = y1; // 设置起点的 y 坐标

        this.x2 = x2; // 设置终点的 x 坐标

        this.y2 = y2; // 设置终点的 y 坐标

        this.color = color; // 设置颜色

    } // 结束 MyLine 构造函数

    // 使用指定的颜色绘制线条

    public void draw(Graphics g) {

        g.setColor(color);

        g.drawLine(x1, y1, x2, y2);

    } // 结束方法 draw

} // 结束类 MyLine
```
