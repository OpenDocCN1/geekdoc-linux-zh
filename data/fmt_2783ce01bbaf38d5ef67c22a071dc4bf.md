
1.  `import java.swing.*;`

2.

3.  `public class FrameDemo {`

4.      `public static void main(String[] args) {`

5.          `JFrame f = new JFrame("Frame Demo");`

6.          `f.setSize(350, 250);`

7.          `f.setVisible(true);`

8.      }

9.  }

```java
import java.swing.*;

public class FrameDemo {
    public static void main(String[] args) {
        JFrame f = new JFrame("Frame Demo");
        f.setSize(350, 250);
        f.setVisible(true);
    }
}
```

第 5 行演示了一个构造函数，其参数是字符串，新 `JFrame` 的宽度和高度为零，必须给定大小。你可以在第 6 行显式设置，或者调用`pack()`，它尊重组件的大小和布局。第 7 行是必要的，因为新创建的 `JFrame` 是不可见的。如果你在某个时刻想从屏幕上移除可见的帧，可以调用`setVisible(false)`。

图 11.3 显示了该应用程序创建的帧。

空帧没有用。`Frame` 设计是为了填充组件。熟悉 Java AWT 的读者知道 `Frame` 的实现允许直接添加组件。`JFrame` 类的不同在于它不是一个容器。你通过调用 `JFrame` 的`getContentPane()`方法访问帧的内容部分。以下应用程序显示了一个包含三个按钮的帧。为了演示应用程序内容，我们必须领先一步，使用布局管理器和 `JButton` 类。我们很快会解释这些。

基础 Swing 组件 365

```java
import java.awt.*;
import javax.swing.*;

public class ContentDemo {
    public static void main(String[] args) {
        JFrame f = new JFrame("Content Pane Demo");
        f.setSize(350, 250);
        Container cont = f.getContentPane();
        cont.setLayout(new FlowLayout());
        for (int i=1; i<=3; i++) {
            cont.add(new JButton("Button #" + i));
        }
        f.setVisible(true);
    }
}
```

# 第 11 章 - Swing 组件

第 9 行为内容面板（content pane）而不是框架（frame）设置了布局管理器，第 11 行将按钮添加到内容面板而不是框架中。图 11.4 显示了运行此应用程序的结果。

`JFrame` 会发出窗口监听器（Window listeners），以便在框架最小化、还原、首次显示和被点击时进行通知。点击“关闭”按钮（Windows 平台上右上角的 X 按钮）不会自动导致框架关闭。相反，点击操作会向框架的所有窗口监听器调用`windowClosing()`方法。此时，必须由其中一个监听器显式地将框架从屏幕上移除；否则用户的点击将不会产生任何效果。

## `JPanel`

`JPanel` 是一个空白的矩形组件，可以包含其他组件。每个面板都使用布局管理器来确定其子组件的位置和大小。以下代码向框架添加了两个按钮。每个面板包含三个按钮。为了视觉效果更好，上方面板是浅灰色，下方的面板是白色。该应用程序使用了 `Grid` 布局管理器，这将在下一章中介绍：

```java
import java.awt.*;
import javax.swing.*;

public class PanelDemo {
    public static void main(String[] args) {
        JFrame f = new JFrame("Content Pane");
        f.setSize(350, 250);
        Container cont = f.getContentPane();
        cont.setLayout(new GridLayout(2,1));
        for (int i = 0; i < 2; i++) {
            JPanel pan = new JPanel();
            pan.setBackground(i == 0 ? Color.lightGray : Color.white);
            for (int j = 0; j < 3; j++) {
                pan.add(new JButton("Button"));
            }
            cont.add(pan);
        }
        f.setVisible(true);
    }
}
```

图 11.5 显示了此应用程序的框架。

### 图 11.5 `JPanel` 示例
`img/09f8389b7ae2705d1ab142d5e8573_401.png`

`JPanel` 不发出任何事件。

## 普通组件

在本节中，我们将讨论普通组件。与容器（`containers`）不同，普通组件是指用户输入数据的组件。我们将回顾以下组件：
- `JLabel`
- `JButton`
- `JCheckBox`
- `JRadioButton`
- `JTextField`
- `TextArea`
- `JComboBox`

### `JLabel`

最简单的组件类型是 `JLabel`，用于显示单行文本或图像。标签（`Labels`）不响应用户输入，也不发出事件。以下应用程序在框架中显示了一个标签，如图 11.6 所示。

```java
import java.awt.*;
import javax.swing.*;

public class LabelDemo {
    public static void main(String[] args) {
        JFrame f = new JFrame("Label Demo");
        f.setSize(350, 250);
        Container cont = f.getContentPane();
        cont.setLayout(new FlowLayout());
        cont.add(new JLabel("This is a Label"));
        f.setVisible(true);
    }
}
```

### 图 11.6 `JLabel` 示例
`img/09f8389b7ae2705d1ab142d5e8573_402.png`

### `JButton`

`JButton` 类实现了一个简单的推动按钮。按钮可以显示文本标签、图标或两者兼有。当用户点击按钮时，`Action` 事件会发送给所有注册的监听器。以下应用程序构建了一个包含两个按钮的框架：

```java
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

public class ButtonDemo extends JFrame {
    private JButton helloBtn, goodbyeBtn;

    public static void main(String[] args) {
        new ButtonDemo().setVisible(true);
    }

    ButtonDemo() {
        super("Button Demo");
        setSize(350, 250);
        Container cont = getContentPane();
        cont.setLayout(new FlowLayout());
        helloBtn = new JButton("Hello");
        goodbyeBtn = new JButton("Goodbye");
        cont.add(helloBtn);
        cont.add(goodbyeBtn);

        ButtonListener listener = new ButtonListener();
        helloBtn.addActionListener(listener);
        goodbyeBtn.addActionListener(listener);
    }
}

class ButtonListener implements ActionListener {
    public void actionPerformed(ActionEvent e) {
        if (e.getSource() == helloBtn)
            System.out.println("Hello");
        else
            System.out.println("Goodbye");
    }
}
```

`JButtons` 发送 `Action` 事件。`ActionListener` 接口仅包含一个方法：`public void actionPerformed(ActionEvent)`。这创建了一个的 Action 监听器并将其注册到两个按钮中的每一个中。将 `ButtonListener` 定义为内部类的方便之处在于：它的功能是隔离的，但它可以访问创建它的外部类实例的`helloBtn`私有变量。这使得监听器很容易判断是哪个按钮被按了。

### 图 11.7 `JButton` 示例
`img/09f8389b7ae2705d1ab142d5e8573_403.png`

### `JCheckBox`

`JCheckBox` 类实现了一个可以选中和取消选择的复选框。以下代码创建了一个包含两个复选框的框架：

```java
import java.awt.*;
import javax.swing.*;

public class CheckBoxDemo {
    public static void main(String[] args) {
        JFrame frame = new JFrame("Checkbox Demo");
        frame.setSize(350, 250);
        Container cont = frame.getContentPane();
        cont.setLayout(new FlowLayout());
        cont.add(new JCheckBox("Charge acct"));
        cont.add(new JCheckBox("Gift wrap"));
        cont.add(new JButton("Submit"));
        frame.setVisible(true);
    }
}
```

`JCheckBox` 会发送 `Action` 事件。然而，与复选框一样，监听这些事件通常是不恰当的。一组复选框通常出现在提交按钮附近；适当的方法是在用户点击提交时通过按钮的`actionPerformed`方法来读取复选框的状态。图 11.8 显示了该应用程序构建的 GUI。

### 图 11.8 `JCheckBox` 示例
`img/09f8389b7ae2705d1ab142d5e8573_404.png`

### `JRadioButton`

单选按钮通常成组用于提供互斥选择。该名称源于在任何时刻只有一个按钮被选中。`JRadioButton` 类通常与`ButtonGroup`一起使用，后者有一个`add(AbstractButton)`方法。以下应用程序创建了单选按钮：

```java
import java.awt.*;
import javax.swing.*;

public class RadioDemo {
    public static void main(String[] args) {
        JFrame frame = new JFrame("Radio Demo");
        frame.setSize(350, 250);
        Container cont = frame.getContentPane();
        cont.setLayout(new FlowLayout());
        ButtonGroup btnGroup = new ButtonGroup();
        JRadioButton r1 = new JRadioButton("Rare");
        btnGroup.add(r1);
        cont.add(r1);
        JRadioButton r2 = new JRadioButton("Medium");
        btnGroup.add(r2);
        cont.add(r2);
        JRadioButton r3 = new JRadioButton("Well Done");
        btnGroup.add(r3);
        cont.add(r3);
        frame.setVisible(true);
    }
}
```

单选按钮像复选框一样可以发送 `Action` 事件。然而，与复选框一样，监听这些事件通常是不恰当的。单选按钮组通常位于应用按钮附近；适当的方法是在点击应用时读取单选按钮的状态。

### 图 11.9 `JRadioButton` 示例
`img/09f8389b7ae2705d1ab142d5e8573_405.png`

### `JScrollBar`

`JScrollBar` 是一个允许用户输入可调整的模拟模拟值的组件。滚动条可以是水平方向或垂直方向；可以在各种构造函数形式中传入`JScrollBar.HORIZONTAL`和`JScrollBar.VERTICAL`常量来确定方向。以下应用程序创建了一个水平滚动条。我们到本章为止使用的 `Flow` 布局管理器在显示滚动条方面并不理想，因此我们将使用更复杂的 `Border` 布局管理器。如果你不熟悉它，请关注第 12 章：

## 基础 Swing 组件 373

```java
class BarListener implements AdjustmentListener {
  public void adjustmentValueChanged(AdjustmentEvent e) {
    System.out.println("Val = " + e.getValue());
  }
}
```

滚动条向已注册的 `Adjustment` 监听器发送事件。在这个示例中，监听器是`BarListener`内部类的一个实例。`ScrollDemo`应用程序生成如图 11.10 所示的 GUI。

### 图 11.10 `JScrollBar` 示例
![](img/09f8389b7ae2705d1ab14be2d5e857e3_407_0.png)

## `JTextField` 和 `JTextArea`

`JTextField` 和 `JTextArea` 组件支持单行和多行文本输入。这两个类都继承自`javax.swing.text.JComponent`，该父类提供了访问和修改组件文本的方法。`JComponent` 的 API 页面对文本功能有很好的描述。

`JTextField` 和 `JTextArea` 在接收键盘输入时都会发送事件。此外，当用户按下 Enter 键时，`JTextField` 会发送 `Action` 事件。以下应用程序包含组件中的每一个；`JTextArea` 显示关于 `JTextField` 中事件的信息。再次，`Flow` 布局管理器对于我们想要演示的组件来说是不恰的，因此我们使用了 `Border` 布局：

```java
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

public class TextDemo extends JFrame
  implements ActionListener, KeyListener {
  private JTextField field;
  private JTextArea area;

  public static void main(String[] args) {
    (new TextDemo()).setVisible(true);
  }

  TextDemo() {
    super("TextDemo");
    setSize(350, 250);
    Container cont = getContentPane();
    field = new JTextField("Type here");
    field.addKeyListener(this);
    field.addActionListener(this);
    cont.add(field, BorderLayout.NORTH);
    area = new JTextArea();
    cont.add(area, BorderLayout.CENTER);
  }

  public void keyPressed(KeyEvent e) { }

  public void keyReleased(KeyEvent e) { }

  public void keyTyped(KeyEvent e) {
    area.append("KEY: " + e.getKeyChar() + '\n');
  }

  public void actionPerformed(ActionEvent e) {
```
