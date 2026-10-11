
```java
colorJList.setSelectionMode(ListSelectionModel.SINGLE_SELECTION);

// 将包含 colorJList 的 JScrollPane 添加到框架

add(new JScrollPane(colorJList));

colorJList.addSelectionListener(

    new ListSelectionListener() { // 匿名内部类

        public void valueChanged(ListSelectionEvent event) // 处理列表选择事件
            event.getContentPane().setBackground(colorJList.getSelectedIndex(0));

        } // 结束方法 valueChanged
    }); // 结束匿名类
); // 结束调用 addSelectionListener
} // // ListFrame 构造函数
}
```

图 11.23 显示对象列表的 JList。（20 部分第 2 部分）

第 29 行（图 11.23）显示 `JList` 对象。`JList` 构造函数的参数是用于在列表中显示的 `Objects` 数组（在此例为 `Strings`）。第 30 行使用 `JList` 方法 `setRowCount` 来确定列表中可见项目的数量。

第 33 行使用 `JList` 方法 `setMode` 来指定选择模式。`ListSelectionModel` 类（位于 `javax.swing` 包）声明了三个指定 `JList` 选择模式的常量——`SINGLE_SELECTION`（一次只能选择一个项目）、`SINGLE_SELECTION`（允许选择多个连续项目的多选择列表）和 `MULTIPLE_SELECTION`（不限制可选择项目的多选择列表）。

与 `JComboBox` 不同，如果列表中的项目多于可见行数，`JList` 不提供滚动条。在这种情况下，使用 `JScrollPane` 来提供滚动功能。第 36 行向 `JFrame` 添加了 `JScrollPane` 的新实例。`JScrollPane` 构造函数接受的参数是需要滚动功能的 `JComponent`（在此例中为 `colorList`）。注意屏幕，由 `JScrollPane` 创建的滚动条出现在 `JList` 的右侧。默认情况下，只有当 `JList` 中的项目数量超过可见项目时，滚动条才会出现。

第 38-49 行使用 `addSelectionListener` 注册一个实现 `ListSelectionListener` 的对象以处理 `JList` 的选择事件。再次，我们使用匿名类实例（第 39–47 行）作为监听器。当用户从 `colorlist` 中进行选择时，`valueChanged` 方法（第 42–46 行）应将列表的背景颜色更改为选中颜色。这在第 44–45 行完成。第 44 行使用了 `JFrame` 方法 `getContentPane`。每个 `JFrame` 实际上由三层组成：背景、内容面板（content pane）和玻璃面板（glass pane）。内容面板位于背景前面，是 `JFrame` 中 GUI 组件显示的地方。该面板用于显示工具提示等应该出现在屏幕上 GUI 组件前端的内容。内容面板完全隐藏了 `JFrame` 的背景；要更改内容面板的背景颜色，`getContentPane` 方法返回 `JFrame` 面板的引用（`Container` 类的对象）。在第 44 行中，我们使用该引用调用 `setBackground` 方法，将内容面板的背景颜色设置为颜色数组中的一个元素。该颜色通过选中项目的索引从数组中选择。`JList` 的 `getSelectedIndex` 返回选中项目的索引。与数组和 `JList` 一样，索引是从 0 开始的。

```java
// Fig. 11.24: ListTest.java
// 从 JList 选择颜色
import javax.swing.JFrame;
public class ListTest
{
    public static void main(String[] args) {
        ListFrame listFrame = new ListFrame();// 创建 ListFrame
        listFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        listFrame.setSize(350, 150); // 设置框架大小
        listFrame.setVisible(true); // 显示框架
    } // 结束 main
}// // 结束类 ListTest
```

**图 11.24** 用于 `ListFrame` 的 `List` 类。

与 `JComboBox` 不同，`JList` 允许用户通过按住 `Shift` 键进行连续选择，或按住 `Ctrl` 键进行杂非连续选择来选择多个项目。

## 556 第二章 GUI 组件：第一部分

```java
// Fig. 11.25: SelectionFrame.java
// 从一个到另一个拷贝项目。
import java.awt.FlowLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import javax.swing.event.ListSelectionEvent;
import javax.swing.event.ListSelectionListener;
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JList;
import javax.swing.JScrollPane;
public class SelectionFrame extends JFrame {
    private JList colorList;
    private JButton copyButton;
    private String[] colorNames = { "Black", "Blue", "Cyan", "Dark Gray", "Green", "Light Gray", "Magenta", "Orange", "Pink", "Red", "White", "Yellow" };
    public SelectionFrame() {
        super("Multiple Selection");
        setLayout(new FlowLayout()); // 设置布局
        colorList = new JList(colorNames); // 存储名称
        colorList.setVisibleCount(5); // 显示行
        colorList.setSelectionMode(ListSelectionModel.MULTIPLE_SELECTION);
        add(new JScrollPane(colorList)); // 添加滚动条
        copyButton = new JButton("Copy"); // 创建按钮
        copyButton.addActionListener(
            new ActionListener() {
                public void actionPerformed(ActionEvent event) {
                    // 将值放入 copyList
                    int[] indices = colorList.getSelectedIndices();
                    for (int i = 0; i < indices.length; i++) {
                        System.out.println(colorNames[indices[i]]);
                    }
                }
            }
        );
    }
}
```
