
BoxLayout 布局管理器（位于 `javax.swing` 包中）沿容器的 x 轴水平排列 GUI 组件，或沿其 y 轴垂直排列。图 22–16–22 中的应用程序演示了 BoxLayout，并且容器类 `Box` 使用 BoxLayout 作为其默认布局管理器。

> // Fig. 22.16: BoxLayoutFrame.java

```java
// Demonstrating BoxLayout.
import java.awt.Dimension;
import javax.swing.JFrame;
import javax.swing.Box;
import javax.swing.JButton;
import javax.swing.BoxLayout;
import javax.swing.JPanel;
import javax.swing.JTabbedPane;

public class BoxLayoutFrame extends JFrame {
    // set up JFrame()
    public BoxLayoutFrame() {
        super( "Demonstrating BoxLayout" );

        // create Box containers with BoxLayout
        Box horizontal1 = Box.createHorizontalBox();
        Box vertical1 = Box.createVerticalBox();
        Box horizontal2 = Box.createHorizontalBox();
        Box vertical2 = Box.createVerticalBox();
        
        final int SIZE = 3; // number of buttons on each Box

        // add buttons to Horizontal1
        for ( int count = 0; count < SIZE; count++) {
            horizontal1.add(new JButton( "Button " + count ));
        }

        // create strut and add buttons to Box vertical1
        for ( int count = 0; count < SIZE; count++) {
            vertical1.add(Box.createVerticalStrut(25));
            vertical1.add(new JButton( "Button " + count ));
        }

        // create horizontal glue and add buttons to Box horizontal2
        for ( int count = 0; count < SIZE; count++) {
            horizontal2.add(Box.createHorizontalGlue());
            horizontal2.add(new JButton( "Button " + count ));
        }

        // create rigid area and add buttons to Box vertical2
        for ( int count = 0; count < SIZE; count++) {
        }
    }
```

Fig. 22.16 | 布局管理器。（2 部分中的第 I 部分。）

## 22.9 布局管理器：BoxLayout 和 GridBagLayout 1013

```java
vertical2d.add(Box.createRigidArea(new Dimension(12, 8)));
vertical2d.add(new JButton("Button " + count));
} // end for
// create vertical glue and add buttons to panel
JPanel panel = new JPanel();
panel.setLayout(new BoxLayout(panel, BoxLayout.Y_AXIS));
for (int count = 0; count < SIZE; count++) {
    panel.add(Box.createGlue());
    panel.add(new JButton("Button " + count));
}
// create a JTabbedPane
JTabbedPane tabbedPane = new JTabbedPane();
JTabbedPane.TOP, JTabbedPane.SCROLL_TAB_LAYOUT
// place each container on tabbed pane
tabs.add("Horizontal Box", horizontal1);
tabs.add("Vertical Box with Struts", vertical1);
tabs.add("Horizontal Box with Glue", horizontal2);
tabs.add("Vertical Box with Rigid Areas", vertical2);
tabs.add("Vertical Box with Glue", panel);

add(tabs); // // place tabbed pane on frame
} // end constructor
} // class BoxLayoutFrame
```

``` 22.16 | 布局管理器。（2 部分中的第 II 部分。）

第 19–22 行创建了 Box 容器。`horizontal1` 和 `horizontal2` 使用静态方法 `createHorizontalBox` 初始化，该方法返回一个容器。`vertical1` 和 `vertical2` 使用静态方法 `createVerticalBox` 初始化，该方法返回一个容器。

第 27–28 行的语句向 `horizontal1` 添加了三个 Button。第 31–35 行的语句向 `vertical1` 添加了三个 Button。在每个按钮之前，`vertical1` 添加了一个垂直间隙（strut）。第 38–42 行的语句向 `horizontal2` 添加了三个 Button。在每个按钮之前，`horizontal2` 添加了水平胶水（glue）。第 45–49 行的语句向 `vertical2` 添加了三个 Button。在每个按钮之前，`vertical2` 添加了一个刚性区域（rigid area）。第 52–53 行的语句创建了一个 `JPanel`。第 55–59 行的语句向 `panel` 添加了三个 Button。在每个按钮之前，`panel` 添加了胶水。第 62–63 行的语句添加了组件。
```

```java

// Fig. 22.17: BoxLayoutDemo.java

// Demonstrating BoxLayout.

import java.awt.Dimension;

import javax.swing.JFrame;

public class BoxLayoutDemo {

    public static void main(String[] args) {

        JFrame layoutFrame = new JFrame();

        layoutFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        layoutFrame.setSize(400, 220);

        layoutFrame.setVisible(true);

    }

 // end main

} // class BoxLayoutDemo
```
