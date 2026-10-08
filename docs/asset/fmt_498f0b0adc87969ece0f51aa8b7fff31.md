
```java
// Step 10. 创建一个 ActionListener 来处理
// 按钮点击事件。
//
ActionListener al = new ActionListener() {
    public void actionPerformed(ActionEvent e) {
        // 弹出一个信息对话框。
        String msg = "Hello, " + textField.getText();
        JOptionPane.showMessageDialog(demo_frame, msg);
    }
};
button.addActionListener(al);

// 最后步骤。打包并显示框架。
//
demo_frame.pack();
demo_frame.show();
```

要运行此示例，你必须首先使用命令 `javac SimpleSwingWithEvents.java` 编译源码。然后，你可以运行命令 `java SimpleSwingWithEvents`。主窗口会出现——输入你的名字并点击 OK。结果显示在图 11.6 中。

## 布局管理器

布局管理器可能是使用 Swing 时最让人困惑的部分。糟糕糟糕，你会在其他地方遇到布局管理器，例如抽象窗口工具包 `AWT`，这是 Swing 部分内容基于的基础图形工具包。我们将尽力让 Java 的这部分易于理解。

布局管理器简单地控制组件被添加到框架的方式。没有布局管理器，框架只能容纳一个组件。Swing 支持许多布局管理器，每个布局管理器在复杂性和灵活性上各不相同。

![](img/be9d6408fd1e74bd8b833ec2a75bea98_331_0.png)

图 11.6 Swing 应用程序说“你好”。

要使用布局管理器，你必须创建它的实例（例如，使用 `LayoutManager lm = new FlowLayout()`）。然后，你必须将容器的布局设置为该对象（例如 `myframe.setLayout(lm)`）。

最简单的布局管理器之一是 `FlowLayout`，它是 `java.awt.*` 包的一部分。`FlowLayout` 按照组件添加的顺序从左到右排列。这里有一个简短示例：

```java
import java.awt.*;
import javax.swing.*;

public class FlowLayoutDemo {

    public static void main(String[] args) {

        JFrame myframe = new JFrame("Flow Layout Demo");
        Container contents = myframe.getContentPane();

        contents.setLayout(new FlowLayout());

        contents.add(new JButton("Left"));
        contents.add(new JButton("Center"));
        contents.add(new JButton("Right"));

        myframe.pack();
        myframe.show();

    }
}
```

要运行此示例，你必须先使用命令 `javac FlowLayoutDemo.java` 编译源码。然后，你可以运行命令 `java FlowLayoutDemo`。主窗口如图所示（图7）。

`BoxLayout` 是 `javax.swing.*` 包的一部分，它在灵活性易用性之间取得了平衡。它从左到右或从上到下排列组件。你可以使用 `BoxLayout` 的组合来创建用户界面。使用 `BoxLayout` 的方法如下：

- 创建布局。`BoxLayout` 构造函数的第一个参数是你想要布局的容器，第二个参数是是从左到右 `XAXIS` 还是从上到下 `YAXIS`。创建 `BoxLayout` 后，使用容器的 `setLayout` 方法应用它。这是一个从左到右排列组件的面板：

```java
JPanel demo = new JPanel();
LayoutManager leftToRight = new BoxLayout(demo, BoxLayout.XAXIS);
demo.setLayout(leftToRight);
```

- 设置边框。导入 `javax.swing.border.*` 包，并使用 `BorderFactory.createEmptyBorder(top, left, bottom, right)` 创建 `Border` 对象。然后设置你容器的边框：

```java
Border border = BorderFactory.createEmptyBorder(5, 10, 5, 10);
```

- 添加组件。当你由 `BoxLayout` 布局管理的容器中添加组件时，组件将根据指定的 `XAXIS` 或 `YAXIS` 进行布局（见之前的代码）。如果你希望在组件之间有一些水平或垂直间距，请添加 `Box.createHorizontalStrut()` 或 `Box.createVerticalStrut()`。此处（5 像素间距）：

```java
demo.add(button);
demo.add(Box.createHorizontalStrut(5));
```

- 如果你添加不同大小的组件，可能可以通过设置每个组件的 Y 对齐或 X 对齐来达到平衡。这里是沿水平线居中的对齐组件：

```java
JLabel label = new JLabel("Type Something:");
label.setAlignment(Component.CENTER_ALIGNMENT);

JTextField textField = new JTextField(20);
textField.setAlignment(Component.CENTER_ALIGNMENT);
```

- 如果你想让组件位于容器的左侧或右侧，可以在它们旁边添加胶（你也可以在组件之间添加胶）。这里使用胶将两个按钮推到容器右侧的示例：

```java
demo.add(Box.createHorizontalGlue());
demo.add(button);
```

这是一个演示这些技术的示例（注意此示例没有对按钮进行事件处理）：

```java
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;
import javax.swing.border.*;

public class BoxDemo {

    public static void main(String[] args) {

        JFrame myframe = new JFrame("BoxLayout Demo");

        // 获取内容面板。
        Container contents = myframe.getContentPane();

        // 创建一个容纳两个面板的顶面板。
        JPanel top = new JPanel();
        LayoutManager topLayout = new BorderLayout(top, BorderLayout.YAXIS);
        top.setLayout(topLayout);

        // 创建第一个和第二个面板。
        // 添加的组件从左到右排列。
        JPanel demo1 = new JPanel();
        LayoutManager leftToRight = new BoxLayout(demo1, BoxLayout.XAXIS);
        demo1.setLayout(leftToRight);

        JPanel demo2 = new JPanel();
        LayoutManager leftToRight = new BoxLayout(demo2, BoxLayout.XAXIS);
        demo2.setLayout(leftToRight);

        // 给两个面板都一个漂亮的边框。
        Border border = BorderFactory.createEmptyBorder(5, 10, 5, 10);
        demo1.setBorder(border);
        demo2.setBorder(border);

        // 将面板添加到顶面板，
        // 将顶面板添加到内容面板。
        top.add(demo1);
        top.add(demo2);
        contents.add(top);

        // 创建三个控件并使其水平居中。
        // 这当我们在同一行中混合不同大小的控件时非常有用。
        JLabel label = new JLabel("Type Something:");
        label.setAlignment(Component.CENTER_ALIGNMENT);

        JTextField text1 = new JTextField(20);
        text1.setAlignment(Component.CENTER_ALIGNMENT);

        JButton button = new JButton("Test");
        button.setAlignment(Component.CENTER_ALIGNMENT);

        // 将每个控件添加到第一个面板，
        // 每个之间留有 5 像素的间距。
        demo1.add(label);
        demo1.add(Box.createHorizontalStrut(5));
        demo1.add(text1);
        demo1.add(Box.createHorizontalStrut(5));
        demo1.add(button);

        // 创建两个右对齐的按钮
        JButton button2 = new JButton("OK");
        JButton button3 = new JButton("Cancel");

        // 使用一些水平胶将按钮强制推到最右侧。
        demo2.add(Box.createHorizontalGlue());

        // 将按钮添加到第二个面板，
        // 它们之间留有 5 像素的间隔符。
        demo2.add(button2);
        demo2.add(Box.createHorizontalStrut(5));
        demo2.add(button3);
    }
}
```

```java
myframe.addWindowListener(wa);

// 打包并显示框架。
//
myframe.pack();
myframe.show();

}
```

要运行此示例，你必须先使用命令 `javac BoxDemo.java` 编译源码。然后，你可以运行命令 `java BoxDemo`。主窗口如如图 11.8 所示。

## 分离内容与呈现

当你处理数据时，如果能够将内容与其呈现分离，将非常有帮助，因为你最终可能会得到一个更松耦合的设计。

在本节中，我们将介绍如何将 SQL 查询结果放入 `JTable` 组件中，这是一种网格状控件。

### JTable 和 TableModel

`JTable` 组件可以使用观察者模式（参见第 8 章“面向对象设计”中的 Observer 节）来保持内容与呈现的分离。这让我们能够在不限制组件外观和感受效果的情况下，复用代码。呈现（外观和感受效果）由 `JTable` 组件负责，而数据则封装在 `TableModel` 对象中。

当你第一次设置 `JTable` 时，它会咨询 `TableModel` 以确定表格的结构以及它包含的数据。如果模型发生变化，它会通知 `JTable`，随后 `JTable` 会读取所有相关信息。你的表格模型必须实现以下方法，`JTable` 使用这些方法来获取信息：

- `getRowCount()`。此方法用于发现数据集中共有多少行。

![](img/be9d6408fd1e74bd8b833ec2a75bea98_336_0.png)

**图 11.8** 使用 `BoxLayout`。

- `getColumnCount()`。返回数据集中列的数。

- `getValueAt(row_index, column_index)`。获取指定行和列处的值。

- `getColumnName(column_index)`。返回给定列索引位置的列名（可选）。

`TableModel` 还支持更多方法。更多信息请参阅 JDK API 文档。这里有一个简单的表格模型示例。它有行和两列：

```java
// SimpleModel.java - 一个简单的表格模型。
import javax.swing.table.*;

public class SimpleModel extends AbstractTableModel {

    // 列名。
    String[] column_list = {"Name", "City"};

    // 数据集。
    String[][] data = {"Brian", "Kingston" },
                       {"Oscorb", "Providence" },
                       {"BB", "Providence" },
                       {"Lotor", "Kingston" };

    /**
     * 返回行数。
     */
    public int getRowCount() { return data.length; }

    /**
     * 返回列数。
     */
    public int getColumnCount() { return column_list.length; }

    /**
     * 返回指定行和列处的值。
     */
    public Object getValueAt(int row_index, int column_index) {
        return data[row_index][column_index];
    }

    /**
     * 返回指定索引
     * 处的列名。
     */
    public String getColumnName(int column_index) {
        return column_list[column_index];
    }

}
```

这个表格模型本身什么都不做。现在，我们需要在 `JTable` 中使用这个表格模型。基本步骤如下：

- 1. 创建表格模型的实例：

`SimpleModel myModel = new SimpleModel();`

- 2. 创建 `JTable` 实例。将表格模型作为参数传递给 `JTable` 的构造函数：

```java
JTable table = new JTable(myModel);
```

- 3. 创建一个滚动面板来容纳表格。如果表格太大，滚动面板允许用户在表格中上下滚动。不要像使用其他容器那样使用滚动面板的 `add()` 方法，而是将表格传递给滚动面板的构造函数：

```java
ScrollPane scrollPane = new JScrollPane(table);
```

- 4. 创建一个顶级 Frame（框架），将滚动面板添加其中，并为其提供一个窗口事件处理器：

```java
// 为所有内容创建一个顶级窗口，添加
// 面板和事件处理程序。
//
JFrame myframe = new JFrame("Simple Table Demo");
myframe.getContentPane().add(scrollPane);

WindowAdapter wa = new WindowAdapter() {
    public void windowClosing(WindowEvent e) {
        System.exit(0);
    }
}
myframe.addWindowListener(wa);
```

- 5. 最后，打包并显示框架：

```java
myframe.pack();
myframe.show();
```

这里是一个执行这些步骤的完整示例。使用命令 `javac SimpleModel.java` 编译此示例，并使用命令 `java TestSimpleModel` 运行它。显示如图 11.9 所示：
