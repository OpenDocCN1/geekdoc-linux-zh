
```
    public static void main(String[] args) {

        new ChatAWT();

    }
```

![](img/681a495129beb6adf91e7ff7f87e7dd4_600_png)

# 使用 Java 进行 GUI 编程

## JFC 简介

当 Java 语言从 1.1 更新到 1.2（现在称为 2.0）时，基础类（JFC）作为标准库添加到 `javax.swing` 中。JFC API 也称为 Swing。如果你在使用 Java 开发工具包，你需要从 Sun 网站下载 JFC。JFC 提供了比 AWT 更丰富的组件集。JFC 提供了以下类：

| 类 | 描述 |
| --- | --- |
| `JButton` | 命令按钮。 |
| `JLabel` | 用于显示不可编辑文本（尽管可以通过程序更改文本）。 |
| `JTextPane` | 用于显示文本。 |
| `JEditorPane` | 用于用户编辑文本。 |
| `JTextArea` | 用于用户编辑多行文本。 |
| `JList` | 用于显示列表。 |

这些图形组件放置在容器中，例如：

| 组件 | 描述 |
| --- | --- |
| `JPanel` | 用于持有其他 Panel 或图形组件的最简单容器。 |
| `JFrame` | 带标题栏的顶层窗口。Frame 通常包含一个 Panel。 |
| `JTabbedPane` | 创建多标签页区域。当将 `JPanel` 对象添加到 `JTabbedPane` 时，你还会指定显示在该 `JPanel` 标签中的文本或图标。 |
| `JScrollPane` | 提供一个可以添加其他组件的滚动区域。 |

尽管，我通常使用 AWT，因为使用 Swing 的程序启动较慢，且响应没那么快。尽管如此，JFC 提供了许多酷的功能，例如编辑文本、显示 HTML 等。本章的示例没有演示线条、形状或其他图形。

有几种可用的布局管理器用于在 Panel 中定位图形组件。在书中 GUI 示例中，我们不会使用任何布局管理器；我们将使用 `setBounds` 方法来指定图形组件的 X-Y 位置及其宽度和高度。这在 Java 程序中非常不寻常，但我认为这会让我们的示例程序更容易理解。

# 编程界面

列表 32.11 中的示例程序实现了一个 `JFCSample` 类。该类继承自 JFC `JFrame` 类，因此当我们创建一个 `JFCSample` 的新实例时，将得到一个应用程序窗口。类构造函数使用 `super` 关键字调用父类（`JFrame`）的构造函数。使用 `JPanel`、`JLabel` 和 `JButton` 类了三个对象。

# 列表 32.11 JFCSample.java 文件

```
// import javax.swing.*;           // swing 1.1

// import com.sun.java.swing.*; // swing 1.0

import java.awt.*;

import java.awt.event.*;

public class JFCSample extends JFrame {

    private int count = 0;

    JLabel countLabel;

    public JFCSample() {

        super("JFC Sample Program");

        JPanel panel1 = new JPanel();

        countLabel = new JLabel();

        JButton countButton = new JButton();

        panel1.setLayout(null);

        getContentPane().setLayout(null); // different than AWT

        setBounds(50

countButton.setBounds(40, 65, 100, 30);

    static public void main(String [] args) {

    new JFCSample();

    }

}
```

我们使用 `setLayout` 来设置帧对象的布局（请记住，`JFCSample` 类的实例也是一个 `null`。对于 JFC，我们需要在调用 `setLayout` 之前使用 `getContentPane` 方法来获取内部容器；这与列表 32.9 中的 AWT 示例程序不同）。

此示例中使用了以下几个实用的方法：

| 方法 | 说明 |
| --- | --- |
| `getContentPane` | JFC 容器有一个内部的内容面板（content pane）；此方法获取该对象，我们向其中添加组件。 |
| `setVisible` | 设置帧（Frame）和面板（Panel）可见。 |
| `setSize` | 设置组件的宽度和高度。 |
| `setLabel` | 设置 Label 实例、Button 等对象的标签文本。 |
| `setText` | 设置 Label 对象的文本，用于指定按钮点击的次数。 |
| `setBounds` | 设置图形组件的 X Y 位置以及宽度和高度。 |
| `add` | 将标签和按钮添加到面板，并将面板添加到帧中。 |

图 32.3 显示了 `JFCsample.java` 程序的运行情况。

# 图 32.3
`JFCsample` 程序演示了使用 JFC API 通过匿名内部类进行事件处理。

![](img/681a495129beb6adf91e7ff7f87e7dd4_604_0.png)

# 编写用户界面

这个示例中唯一复杂的地方是处理与点击按钮对象相关的事件。然而，处理这些事件与我们在列表 32.9 AWT 示例中处理事件的方式，仅需几行代码。

```
JButton.addMouseListener(

    new java.awt.event.MouseAdapter() {

        public void mouseClicked(MouseEvent e) {

            countLabel.setText("button clicked " +

                ++count + " times");

        }

    }

);
```

`addMouseClicked` 方法用于将 `MouseListener` 实例与按钮（或其他任何组件）关联。现在，可以定义一个实现 `MouseListener` 接口的独立类（需要定义五个方法：`mouseClicked`、`mouseEntered`、`mouseExited`、`mousePressed` 和 `mouseReleased`）。然而，有一个 `MouseAdapter` 工具类，提供了这五个方法的“什么都不做”的版本。在这些代码中，我们创建一个匿名类（例如，它是一个没有关联的内部类），并重写了 `mouseClicked`。我们的 `mouseClicked` 方法使用 `setText` 来更改标签显示的文本。在列表 32.13 中，我们从 `java.awt` 包（用于图形组件和容器）和 `java.awt.event` 包（用于事件处理类和接口）以及 `javax.swing` 包导入了 Swing（或 JFC）类。

在列表 32.11 中，我们定义了一个静态 `main` 方法，当我们通过以下命令编译并运行此示例程序时会执行该方法：

```
javac JFCample.java
java JFCample
```

`JFCample` 程序没有处理窗口关闭事件，因此必须在运行程序的终端中输入 `Ctrl+C` 来终止它。

# 使用 JFC 编写聊天程序

我们将在本节中开发 `ChatJFC` 程序。它与 `ChatAWT` 程序几乎完全相同，只是使用了 JFC 类而不是 AWT 类。两个程序都显示在图 32.2 中。

列表 32.12 中的示例程序使用 JFC 实现了一个聊天客户端，这有点复杂，因为用户界面有多个组件。每个组件都通过面板中的 X-Y 位置进行定位，并使用 `setBounds` 方法设置特定的宽度和高度。在查看列表 32.12 的代码之前，你应该先查看图 32.2 的底部，那里显示了 `ChatJFC` 程序的运行情况。`ChatJFC` 程序使用了 `ChatEngine` 类。`ChatEngine` 的接口非常简单，在之前的节中介绍过。`ChatJFC` 类实现了 `Listener` 接口并将其注册到 `ChatEngine` 实例。这种注册允许引擎调用 `ChatJFC` 类中的 `receive` 方法。

# 列表 32.12 ChatJFC.java

```java
import javax.swing.*; // swing 1.1
import com.sun.java.swing.*; // swing 1.0
import java.awt.*;
import java.awt.event.*;
```
