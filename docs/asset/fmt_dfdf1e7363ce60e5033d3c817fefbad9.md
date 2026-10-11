
`gridLayoutFrame.setSize(300, 200); // 设置帧大小`

`gridLayoutFrame.setVisible(true); // 显示帧`

} // end main

} // end class GridLayoutDemo

![](img/1df0d1e8ac6007b95647eb8ea38390af_628_0.png)

图 11.44 | GridLayoutFrame 的测试类。

第 24–25 行创建了两个 `GridLayout` 对象。第 24 行使用的 `GridLayout` 构造函数指定了一个具有 2 行 3 列的 `GridLayout`，网格组件之间有 5 像素的水平间距和 5 像素的垂直间距。第 25 行使用的 `GridLayout` 构造函数指定了一个具有 3 行 2 列的 `GridLayout`，使用默认间距（1 像素）。

## 584 第二章 GUI 组件：第一部分

此示例中的 `JButton` 对象最初使用 `gridLayout` 进行布局（第 27 行通过 `setLayout` 设置于内容面板）。第一个组件被添加到第一行的第一列。下一个组件被添加到第一行的第二列，依此类推。当 `JButton` 被按下时，会调用 `actionPerformed` 方法（第 39–48 行）。每次调用 `actionPerformed` 都会在 `gridLayout2` 和 `gridLayout1` 之间切换布局，使用布尔变量 `toggle` 来决定下一次布局。
第 47 行显示了另一种重新格式化布局已更改的容器的方法。`Container.validate()` 根据容器的当前布局管理器和当前显示的 GUI 组件集重新计算容器的布局。

## 11.18 使用面板 管理更复杂的布局

GUI（如图 11.1 所示）要求每个组件都放置在精确的位置。它们通常由多个面板组成，每个面板的组件按特定的布局排列。`JPanel` 类继承自 `JComponent`，而 `JComponent` 继承自 `Container` 类，每个 `JPanel` 都是一个 `Container`。因此，每个 `JPanel` 都可以通过 `Container` 的 `add` 方法附加其他组件或其他面板。图 11.45–11.46 展示了如何使用 `JPanel` 创建更复杂的布局，将多个 `JButton` 放在 `BorderLayout` 的 `SOUTH` 区域。

在第 11 行声明 `JPanel buttonPanel` 并在第 19 行创建它后，第 20 行将 `buttonPanel` 的布局设置为一行五列的 `GridLayout`（数组 `buttons` 中有五个 `JButton`）。第 23–27 行将数组 `buttons` 中的五个 `JButton` 添加到 `JPanel` 中——与 `JFrame` 不同，`JPanel` 类没有内容面板。第 26 行将按钮直接添加到 `JPanel` 中——第 29 行使用默认的 `BorderLayout` 将 `buttonPanel` 添加到 `SOUTH` 区域。注意，`SOUTH` 区域的高度与 `buttonPanel` 上按钮的高度相同。`JPanel` 的大小是由它包含的组件决定的。随着更多组件的添加，`JPanel` 会增大（根据其布局管理器的限制）以容纳这些组件。调整窗口查看布局管理器如何影响 `JButton` 的大小。

![](img/1df0d1e8ac6007b95647eb8ea38390af_629_0.png)

```java
// 使用 JPanel 帮助布局组件。

import java.awt.GridLayout;

import java.awt.BorderLayout;

import javax.swing.JFrame;

import javax.swing.JPanel;

import javax.swing.JButton;

public class PanelFrame extends JFrame {

    private JPanel buttonPanel; // 用于存放按钮的面板

    private JButton buttons[]; // 按钮数组

    // 无参数构造函数

    public PanelFrame() {

        super("Panel Demo");

    }
```

图 11.45 | 带有五个 `JButton` 的 `GridLayout` `JPanel`，附加到 `BorderLayout` 的 `SOUTH` 区域（第 1/2 部分）。

## 11.19 JTextArea

```java
buttons = new JButton[ 5 ]; // 创建按钮数组

JPanel = new JPanel(); // 设置面板

JPanel.setLayout(new GridLayout( 1, buttons.length ));

// // 创建并添加按钮

for ( int count = 0; count < buttons.length; count++) {

    buttons[count] = new JButton("Button " + (count + 1));

    JPanel.add(buttons[count]); // 将按钮添加到面板

} // end for
```

`add(JPanel, BorderLayout.SOUTH); // 将面板添加到 JFrame`
} // end class constructor

**图 11.45** | 带有五个按钮的 `GridLayout` `JPanel`，附加到 `BorderLayout` 的 `SOUTH` 区域。（第 2/2 部分）。

```java
// PanelDemo.java

// 测试 PanelFrame.

import javax.swing.JFrame;

public class PanelDemo extends JFrame {

    public static void main(String[] args) {

        PanelFrame panelFrame = new PanelFrame();

        panelFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        panelFrame.setSize(450, 200); // 设置帧大小

        panelFrame.setVisible(true); // 显示帧

    } // end main

} // end class PanelDemo
```

![](img/1df0d1e8ac6007b95647eb8ea38390af_630_0.png)

**图 11.46** | `PanelFrame` 的测试类。

## JTextArea

A `JTextArea` 提供了一个用于处理多行文本的区域。与 `JTextField` 类一样，`JTextArea` 是 `JComponent` 的子类，声明了用于 `JTextField`、`JTextArea` 以及其他文本 GUI 组件的常用方法。

图 11.47–11.48 展示了 `JTextArea`。一个 `JTextArea` 显示用户可以选择的文本。另一个 `JTextArea` 是不可编辑的，用于显示第一个 `JTextArea` 中的选中文本。`JTextArea` 没有动作事件。与多选择 `JList`（节 11.12）一样，来自另一个 GUI 组件的外部事件指示何时处理 `JTextArea` 中的文本。例如，在输入消息时，我们通常点击发送按钮将消息发送给接收者。同样，在文字处理器中编辑时，我们通常通过选择保存或另存为菜单项来保存文件。在这个程序中，复制按钮产生事件，将左侧 `JTextArea` 的选中文本复制并显示在右侧 `JTextArea` 中。

```java
// TextArea.java

// 将文本从一个 textarea 到另一个

import java.awt.event.ActionListener

import java.awt.event.ActionEvent;

import javax.swing.Box;

import javax.swing.JFrame;

import javax.swing.JTextArea;

import javax.swing.JButton;

import javax.swing.JScrollPane;

public class TextArea extends JFrame {

    private JTextArea textArea1; // 显示演示字符串

    private JTextArea textArea2; // 选中的文本复制到这里

    private JButton copyButton; // 发起文本复制

    // 无参数构造函数

    public TextArea() {
```
