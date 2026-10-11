
![](img/1df0d1e8ac6007b95647eb8ea38390af_611_0.png)

图 11.32 | `MouseDetailsFrame` 的测试类

Java 应用程序可能运行在具有单键、双键或三键鼠标的系统中。Java 提供了一种区分鼠标按钮的机制。`MouseEvent` 类继承了 `InputEvent` 类的几个方法，可以区分多键鼠标上的按钮，或者通过组合键模拟多键鼠标。

## 11.15 用于鼠标绘图的 JPanel 子类

按键和鼠标按钮点击。图 11.33 显示了用于区分鼠标点击的 `InputEvent` 方法。Java 假设所有的鼠标点击都是左键点击。因此，测试左键点击非常简单。然而，对于使用单键或双键鼠标的用户，必须同时使用按键组合和鼠标按钮点击来模拟鼠标上的动作。在单键或双键鼠标的情况下，如果用户按住 `Alt` 键并点击双键鼠标上的左键或单键鼠标上的唯一按钮，Java 应用将认为点击了鼠标中键（中间键）。在单键鼠标的情况下，如果用户按住 `Meta` 键并点击鼠标按钮，Java 应用将认为点击了右键。

图 11.31 的第 22 行为 `MouseDetailsFrame` 注册了一个 `MouseListener`。该事件监听器是 `MouseClickHandler` 类的对象，它继承自 `MouseAdapter`。这使得我们能够只声明 `clicked` 方法（第 29–45 行）。该方法捕获事件发生的坐标并将其存储在局部变量 `x ypos` 中（第 31–32 行）。第 34–35 行创建了一个字符串 `details`，其中包含鼠标点击的次数，该次数由第 35 行的 `MouseEvent getClickCount` 返回。第 37–42 行使用 `isMetaDown` 和 `isAltDown` 来确定用户点击了哪个鼠标按钮，并在每个情况下向 `details` 追加相应的字符串。生成的字符串显示在状态栏 `statusBar` 中，并决定了执行应用程序的 `main` 方法。尝试重复点击鼠标的任何按钮以查看点击计数递增。

| InputEvent 方法 | 描述 |
|---|---|
| `isMetaDown()` | 当用户在双键或三键鼠标上点击右键时，返回 `true`。为了在单键鼠标上模拟右键点击，用户可以按住键盘上的 `Meta` 键并点击鼠标按钮。 |
| `isAltDown()` | 当用户在三键鼠标上点击中键时，返回 `true`。为了在单键或双键鼠标上模拟中键点击，用户可以按下键盘上的 `Alt` 键并分别点击唯一按钮或左键。 |

**Fig. 11.33** | 有助于区分左键、中键和右键点击的 `InputEvent` 方法。

## 11.15 用于鼠标绘图的 JPanel 子类

第 11.13 节展示了如何在 `JPanel` 中跟踪鼠标事件。在本节中，我们使用 `JPanel` 作为专用绘图区域，用户可以通过拖动鼠标进行绘制。此外，本节演示了一个扩展自适配器（adapter）的事件监听器。

### paintComponent 方法

扩展 `JComponent` 的轻量级 Swing 组件（如 `JPanel`）包含 `paintComponent` 方法，该方法在轻量级 Swing 组件绘制时被调用。通过重写此方法，你可以指定如何使用 Java 功能绘制形状。在自定义 `JPanel` 作为专用绘图区域时，子类应该重写 `paintComponent`，并在重写方法的体的第一行调用父类的 `paintComponent` 版本，以确保组件显示正确。此的原因是 `JComponent` 类支持透明度。为了正确显示组件，程序必须确定组件是否位于父类 `JComponent` 的 `paintComponent` 实现中。当组件是透明时，当程序显示组件时，`paintComponent` 不会清除其背景。当组件是不透明时，`paintComponent` 在组件显示之前会清除背景。如果没有调用父类版本的 `paintComponent`，GUI 组件通常将无法在用户界面上正常显示。此外，如果在执行完自定义绘图后才调用父类版本，结果通常会被擦除。Swing 轻量级组件的透明度可以通过 `setOpaque` 方法进行设置（传递 `false` 参数表示组件是透明的）。

### 视图外观观察 11.13

大多数 Swing 组件可以是透明的或不透明的。如果一个 Swing GUI 组件是不透明的，当调用其 `paintComponent` 方法时，它的背景会被清除。只有不透明的组件才能显示自定义的背景颜色。`JPanel` 对象默认是不透明的。

### 错误预防提示 11.1

在 `JComponent` 的 `paintComponent` 方法中，第一行始终应该是对父类 `paintComponent` 方法的，以确保子类对象显示正确。

### 常见编程错误 11.5

如果重写的 `paintComponent` 方法没有调用父类版本，子类组件可能无法正常显示。如果重写的 `paintComponent` 方法在绘制完成后调用父类版本，则绘图结果将被擦除。

### 定义自定义绘图区域

图 11.34–1.35 的画家展示了一个自定义的 `JPanel` 子类，它被用于创建一个专用绘图区域。应用程序使用鼠标拖动事件来处理简单的绘图区域。用户可以通过在 `JPanel` 上拖动鼠标来画画。我们的事件监听器类（第 22 行的匿名内部类）继承自 `MouseAdapter`。由于该类明确声明了 `mouseMoved` 和 `mouseDragged`，我们可以重写 `mouseDragged` 来提供事件处理。第 3–7 行导入了 `PaintPanel` 类中使用的类。`Point` 类 (`java.awt`) 表示 x-y 坐标。在本中，我们使用一个包含 10000 个 `Point` 的数组（第 14 行）来存储每个拖动事件发生的位置。正如你所看到的，`paintComponent` 方法使用这些 `Point` 进行绘制。实例变量 `count`（第 11 行）维护到目前从拖动事件中捕获的 `Point` 总数。

```java
// Fig 1134: PaintPanel.java

// 使用类 MouseAdapter.

import java.awt.Point;

import java.awt.Graphics;

import java.awt.event.MouseEvent;

import java.awt.event.MouseAdapter;

import javax.swing.JPanel;

public class PaintPanel extends JPanel {

    // 点的总数

    private int pointCount = 0;

    // Point 数组

    private Point[] points = new Point[10000];

    // 设置 UI 并注册事件处理器

    public PaintPanel() {

        // 处理移动事件

        addMotionListener(new MouseAdapter() {

            // 匿名内部类

            public void mouseDragged(MouseEvent event) {

                // 找到点

                if (pointCount < points.length) {

                    // 存储坐标

                    points[pointCount] = event.getPoint();

                    // 增加点数

                    pointCount++;

                    // 刷新

                    repaint();

                }

            } // end mouseDragged

        } // end 匿名内部类

        ); // end addMotionListener

    } // end PaintPanel 构造函数

    // 绘制区域

    public void paintComponent(Graphics g) {

        // 清除背景

        super.paintComponent(g);

        // 绘制所有点

        for (int i = 0; i < pointCount; i++) {

            // 绘制椭圆

            g.fillOval(points[i].x, points[i].y, 4, 4);

        }

    } // end paintComponent

} // end class
```
