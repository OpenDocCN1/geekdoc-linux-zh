

## 第 12 章 • 布局管理器

东（East）和西（West）区域与北（North）和南（South）几乎相反：在东部西部，组件获得其首选宽度，但高度受到限制。在这里，组件垂直向上延伸到北部组件的底部（如果存在）或容器的顶部（如果没有北部组件）。组件向下延伸到南部组件的顶部（如果存在）或容器的底部（如果没有南部组件）。图 12.14 到 12.17 显示了使用 `Border` 布局管理器来布局两个滚动条的框架，一个在东部，一个在西部。在图 12.14 中，没有北部或南部组件进行竞争。

在图 12.15 中，北部有一个标签（label）。

**图 12.14** 东部和西部

![](img/09f8389b7ae2705d1ab14be2d5e857e3_442_0.png)

**图 12.15** 东部和西部，带有北部

![](img/09f8389b7ae2705d1ab14be2d5e857e3_442_1.png)

**图 12.16** 东部和西部，带有南部

![](img/09f8389b7ae2705d1ab14be2d5e857e3_443_0.png)

**图 12.17** 东部和西部，同时带有北部和南部

![](img/09f8389b7ae2705d1ab14be2d5e857e3_443_1.png)

在图 12.16 中，南部有一个标签。该标签在黑色背景上使用白色文字，这样你可以清楚地看到南部区域在哪里。

在图 12.17 中，北部和南部都有标签。标签在黑色背景上使用白色文字，这样你可以清楚地看到北部和南部区域在哪里。

生成这四张图像的代码列在这里。只有一个应用程序。如所示，代码生成了图 12.17（同时包含北部和南部）；第 17 和第 24 行被谨慎地注释掉，以生成其他图形：

```java
1. import java.awt.*;
2. import javax.swing.*;
3.
4. public class EastWest extends JFrame {
5. public static void main(String[] args) {
6. JFrame frame = new JFrame();
7. Container cont = frame.getContentPane();
8.
9. cont.add(new JScrollPane(), BorderLayout.WEST);
10. cont.add(new JScrollPane(), BorderLayout.EAST);
11.
12. JLabel topLabel = new JLabel("This is North");
13. topLabel.setOpaque(true);
14. topLabel.setFont(new Font("Serif", Font.PLAIN, 36));
15. topLabel.setForeground(Color.white);
16. topLabel.setBackground(Color.black);
17. cont.add(topLabel, BorderLayout.NORTH);
18.
19. JLabel bottomLabel = new JLabel("This is South");
20. bottomLabel.setOpaque(true);
21. bottomLabel.setFont(new Font("Monospaced", Font.PLAIN, 18));
22. bottomLabel.setForeground(Color.white);
23. bottomLabel.setBackground(Color.black);
24. cont.add(bottomLabel, BorderLayout.SOUTH);
25.
26. frame.setSize(400, 375);
27. frame.setVisible(true);
28. }
29. }
```

布局管理器控制的第五个区域称为中心（Center）。中心只是容器在分配了北部、南部、东部和西部后剩余的部分。图 12.18 显示了一个在北部、南部、东部和西部有按钮、中心有文本区域的框架。

生成图 12.18 的代码如下：

```java
1. import java.awt.*;
2. import javax.swing.*;
3.
4. public class Center extends JFrame {
5. public static void main(String[] args) {
6. JFrame frame = new JFrame();
7. Container cont = frame.getContentPane();
8.
9. cont.add(new JButton('N'), BorderLayout.NORTH);
10. cont.add(new JButton('S'), BorderLayout.SOUTH);
11. cont.add(new JButton('E'), BorderLayout.EAST);
12. cont.add(new JButton('W'), BorderLayout.WEST);
13.
14. JTextArea ta = new JTextArea();
15. for (int i=0; i<10; i++)
16. ta.append("Center Area Line " + i + "\n");
17. cont.add(ta, BorderLayout.CENTER);
18.
19. frame.setSize(400, 375);
20. frame.setVisible(true);
22. }
```

在第 17 行中，区域被添加到 Center。在向 Center 添加组件时，省略第二个参数是合法的，但不明智。在 Java 平台上，布局管理器将假设你指的是 Center；但在旧版本中，这种行为是不可预测的，通常会导致组件不可见。通常，如果你显式指定区域（如第 17 行所示），其他人更容易理解你的代码。图 12.19 和 12.20 显示了在缺少某些区域时 Center 区域发生的情况。这些框架是通过注释掉第 9 行（对应图 12.19）和第 10–12 行（对应图 12.20）生成的。图形显示 Center（文本区域）只是在给其他区域分配空间后剩余的区域。

### 12.18 Center 区域

| | |
| :--- | :--- |
| Center Area Line 0 | |
| Center Area Line 1 | |
| Center Area Line 2 | |
| Center Area Line 3 | |
| Center Area Line 4 | |
| Center Area Line 5 | |
| Center Area Line 6 | |
| Center Area Line 7 | |
| Center Area Line 8 | |
| Center Area Line 9 | |
| W | E |

**图 12.19** Center，无北部

![](img/09f8389b7ae2705d1ab14be2d5e857e3_446_0.png)

**图 12.20** Center，无南部、东部或西部

![](img/09f8389b7ae2705d1ab14be2d5e857e3_446_1.png)

## 卡片布局 (Card Layout)

Card 布局管理器按照时间而非空间来布局其组件。在任何时刻，使用 Card 布局的容器都只显示它的一个组件；所有其他组件都是不可见的。对布局器的方法调用可以告诉它可以显示不同的组件。所有组件（通常是面板）都会调整大小以占据整个容器。其结果类似于一个没有标签的选项页面板。

当你使用 Card 布局时，你有几个选项来控制显示哪个组件以及何时显示。Card 布局为它管理的组件提供一个序列，你可以显式要求它显示该序列中的第一个或最后一个组件。此外，你可以要求它显示下一个组件。

Card 布局为它管理的组件提供一个序列，你可以显式要求它显示该序列中的第一个或最后一个组件。此外，你可以要求它显示下一个组件。

Card 布局为它管理的组件提供一个序列，你可以显式要求它显示该序列中的第一个或最后一个组件。此外，你可以要求它显示下一个组件。

Card 布局为它管理的组件提供一个序列，你可以显式要求它显示该序列中的第一个或最后一个组件。此外，你可以要求它显示下一个组件。

Card 布局为它管理的组件提供一个序列，你可以显式要求它显示该序列中的第一个或最后一个组件。此外，你可以要求它显示下一个组件。

Card 布局为它管理的组件提供一个序列，你可以显式要求它显示该序列中的第一个或最后一个组件。此外，你可以要求它显示下一个组件。

Card 布局为它管理的组件提供一个序列，你可以显式要求它显示该序列中的第一个或最后一个组件。此外，你可以要求它显示下一个组件。

Card 布局为它管理的组件提供一个序列，你可以显式要求它显示该序列中的第一个或最后一个组件。此外，你可以要求它显示下一个组件。

Card 布局为它管理的组件提供一个序列，你可以显式要求它显示该序列中的第一个或最后一个组件。此外，你可以要求它显示下一个组件。

Card 布局为它管理的组件提供一个序列，你可以显式要求它显示该序列中的第一个或最后一个组件。此外，你可以要求它显示下一个。

### 向卡片布局添加组件

当你使用 Card 布局时，有几个选项来控制显示哪个组件以及何时显示。Card 布局为它管理的组件提供一个序列，你可以显式要求它显示该序列中的第一个或最后一个组件。此外，你可以要求它显示下一个组件。

Card 布局为它管理的组件提供一个序列，你可以显式要求它显示该序列中的第一个或最后一个组件。此外，你可以要求它显示下一个组件。

Card 布局为它管理的组件提供一个序列，你可以显式要求它显示该序列中的第一个或最后一个组件。此外，你可以要求它显示下一个组件。

### 选择显示的组件

Card 布局管理器按照时间而非空间来布局其组件。在任何时刻，使用 Card 布局的容器都只显示它的一个组件；所有其他组件都是不可见的。对布局器的方法调用可以告诉它可以显示不同的组件。所有组件（通常是面板）都会调整大小以占据整个容器。

Card 布局为它管理的组件提供一个序列，你可以显式要求它显示该序列中的第一个或最后一个组件。此外，你可以要求它显示下一个组件。

让我们看一个例子。特别是带有下划线的行的，它们显示了添加和显示组件：

```java
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;
```

```java
public class CardDemo extends JPanel {
    private JPanel cardPanel = new JPanel();
    private BorderLayout cardLayout = new BorderLayout();

    private JPanel controlPanel = new JPanel();

    private JButton firstName = new JButton("First");
    private JButton lastName = new JButton("Last");
    private JButton nextButton = new JButton("Next");
    private JButton prevButton = new JButton("Prev");
    private JTextField selectText = new JTextField("*"); }
```

```java
public CardDemo() {
    setLayout(new BorderLayout());

cardPanel.setLayout(cardLayout);
```

要添加命名的组件，只需在 `add` 方法的第二个参数中使用字符串，如下：

```java
JPanel p = new JPanel();
p.setLayout(new CardLayout());
JButton b = new JButton("A");
p.add(b, "Button-B");
```

如果你检查 Container 类的 API，你会发现另一个方法，它接受字符串作为第一个参数，组件作为第二个参数。你可以使用这个方法，并且它是有效的。然而，API 说 `add(Component, Object)` 版本是“强烈建议的”。

