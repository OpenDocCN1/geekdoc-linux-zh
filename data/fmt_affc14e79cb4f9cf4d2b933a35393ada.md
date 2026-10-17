
# 第26章：Java 编程

- `javadoc`—Java API 生成器，从带有 `/**` 开头并以 `*/` 结尾的特殊注释源文件中提取文档。
- `javah`—Java C 代码生成器，为 Java 源码生成 `.h` 和 `.c` 文件。这些 C 文件用于实现使 API 在特定操作系统上运行的原生方法。
- `jav`—Java 文件反汇器，接收一个类名并打印该类的类可读描述。

在这些程序中，你将用到的三个程序如下：

- 你会频繁使用 `javac`，因为它是编译器程序。`javac` 程序将 Java 源文件（你将在下一节中看到一些示例）转换为包含 Java 字节码（Java 虚拟机的指令集）的二进制文件。
- 你会使用 `java` 来运行独立 Java 程序。
- 你会使用 `jdb` 来调试 Java 程序。

## 第26章：Java 841

```java
(
  String helvmsg = "Hello, World!";

//---
// paint
// Method that paints the image

  public void paint(java.awt.Graphics gc)
  {
    // Draw a rectangle around the applet's bounding box
    // so we can see the box.
    gc.drawRect(0, 0, getSize().width-1,
               getSize().height-1);

    // Create the font to be used for the message.
    Font font = new Font("Helvetica", Font.BOLD, 24);

    // Select the font into the Graphics object.
    gc.setFont(font);

    // Get the font metrics (details of the font size).
    FontMetrics fm = gc.getMetrics();
    int width = fm.getStringWidth(helvmsg);
    int ascent = fm.getAscent();
    int descent = fm.getDescent();

    // Compute starting (x,y) position to center string
    // The size() method returns size of applet's
    // bounding box.
    int xstart = getSize().width/2 - width/2;
    int ystart = getSize().height/2 + ascent/2 - descent/2;

    // Set the color to red.
    gc.setColor(Color.red);

    // Now draw the string.
    gc.drawString(helvmsg, xstart, ystart);
  }
)
```

通过浏览这段代码，你可以学习很多关于如何在 Java 中显示图形的知识。以下是关键点：

- `import` 语句列出了此程序使用的外部类。`import` 语句后的名称可以是类名，也可以是带有通配符 (`*`) 的名称，这告诉 Java 编译器导入包中的所有类。此示例使用了 `Applet` 类以及 `java.awt` 包中的许多图形类。
- `HelloWorld` applet 被为 `Applet` 类的扩展。这就是 `public class HelloWorld extends java.applet.Applet` 语句的含义。

## 第五部分：红帽 Linux 编程

- applet 的 `paint` 方法包含绘制输出的代码。`paint` 方法接收一个 `Graphics` 对象作为参数。你必须调用 `Graphics` 对象的方法来显示输出。
- `getSize` 方法返回 applet 绘制区域的大小。
- 要使用字体，首先要创建一个 `Font` 对象，然后调用 `Graphics` 对象的 `setColor` 方法。
- 要用特定颜色绘图，请使用合适的 `Color` 对象作为参数调用 `Graphics` 对象的 `setColor` 方法。
- 如果你熟悉 C++，你会发现 Java 的方法调用与调用 C++ 对象成员函数的方式相似。事实上，C++ 和 Java 之间有许多相似之处。

将代码列表保存为名为 `HelloWorld.java` 的文件。然后，使用命令进行编译：

```bash
javac HelloWorld.java
```

此步骤会创建 applet 类文件：`HelloWorld.class`。要测试 applet，你需要创建一个 HTML 文档并将 applet 嵌入该文档中，如下所示：

```html
<html>
<head>
  <title>Hello, World! from Java</title>
</head>
```

```html
<body>
<h3>"Hello, World! from Java"</h3>
```

applet 获得了一个用于显示其输出的区域。在例示例中，applet 在其分配的区域周围画了一个边界，然后在该框内居中显示“Hello, World!” 消息。

```html
<applet code=HelloWorld width=200 height=60>
如果你看到这条消息，说明你没有支持 Java 的浏览器。
</applet>
```

```html
Here is the applet!
</body>
</html>
```

如此 HTML 源码所示，你必须使用 `<applet>` 标签在 HTML 文档中插入 applet。在“使用 <applet>”部分，你将学习 `<applet>` 标签的语法。

你可以使用两个工具来测试 applet。第一个是 `appletviewer`，它随 JDK 提供。要查看 applet，你需要运行 `appletviewer` 程序并提供 HTML 文档名。假设 HTML 文名为 `hello.html`。然后使用以下命令运行 `appletviewer`：

```bash
appletviewer hello.html
```

图 26-1 显示了 `appletviewer` 如何显示 applet。`(img/b418dfc0d37b49876d5e801170c507_876_0.png)`

图 26-1：在 `appletviewer` 中运行“Hello, World!” Applet。注意 `appletviewer` 只显示 applet，HTML 文档中的其他文本会被忽略。然而，在支持 Java 的浏览器中外观会有所不同。

要在浏览器中查看 applet，启动 Mozilla 浏览器并从菜单选择“打开文件”（Open File）。在“打开文件”对话框中，进入 `hello.html` 文件和 `HelloWorld.class` 文件所在的目录。选择 `hello.html` 文件并点击“打开”。Mozilla 将渲染包含 HelloWorld applet 的 HTML 文档。

## 第26章：Java 编程 843

## 学习 Java

现在你已经看到了一些 Java 示例，本节将提供 Java 的概述。尽管 Java 主要与 applet 的创建相关，但许多人必须意识到 Java 也是开发通用应用程序的理想选择。Java 流行的原因之一是 Java 代码的可移植性。编译后的 Java 代码可以在任何提供了 Java 解释器和库的系统上运行。构建库并非易事，但一旦操作系统上有了 Java 解释器和库，你就可以原封不动地运行 Java。

## Java 中的对象

Java 是一种面向对象的语言。这种程度以至于 Java 完全不允许任何独立过程；所有数据和过程必须在对象内部。事实上，整个 Java 应用程序都是对象。

基于对象的编程的基本概念与面向对象的语言概念相同。有三个底层概念：

- 数据抽象
- 继承
- 多态

## 数据抽象

为了理解数据抽象，考虑 C 运行时库中的文件输入/输出 (I/O) 例程。这些例程允许将文件视为字节流，并允许你通过调用 I/O 例程对其执行各种操作。例如，你可以调用 `fopen` 打开文件，调用 `fclose` 关闭文件，调用 `fgets` 从文件中读取字符，以及调用 `fputc` 向文件中写入字符。这种文件的抽象模型通过定义 `FILE` 数据类型来实现，以包含文件的所有相关信息。在 C 中使用 `FILE` 数据类型时，不需要知道定义它的数据结构。事实上，`FILE` 的底层数据结构在不同系统之间可能有所不同。

# 第 26 章：Java 编程
