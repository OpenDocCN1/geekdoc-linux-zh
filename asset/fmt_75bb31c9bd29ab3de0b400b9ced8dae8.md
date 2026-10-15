
```java
private JLabel statusBar; // 底部显示的 JLabel

// 构造函数设置标题并注册鼠标监听器

public MouseFrame() {

    super("Mouse clicks and buttons");

    statusBar = new JLabel("Click the mouse");

    add(statusBar, BorderLayout.SOUTH);

    addMouseListener(new MouseHandler());

}

// 处理鼠标事件的内部类

private class MouseHandler extends MouseAdapter {

    // 处理点击事件并确定按了哪个按钮

    public void mouseClicked(MouseEvent event) {

        int xPos = event.getX(); // 获取鼠标 x 坐标

        int yPos = event.getY(); // 获取鼠标 y 坐标

        details = String.format("Clicked %d time(s)",

            event.getClickCount());

        if (event.isMouseDown()) // 右键
            details += " with right button";

        else if (event.isAltDown()) // 中键
            details += " with center button";

        else // 左键
            details += " with left button";

        statusBar.setText(details); // 在 statusBar 中显示消息

    } // 结束方法 mouseClicked

} // 结束内部类 MouseHandler

} // 结束类 MouseFrame
```

图 11.31 | 左键、中键和右键点击。（部分/2）

```java
// 图 11.32: MouseDetails.java
// 测试 MouseDetailsFrame.

import javax.swing.JFrame;

public class MouseDetails
{
    public static void main(String args[])
    {
        MouseDetailsFrame mouseDetailsFrame = new MouseDetailsFrame();
        mouseDetailsFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        mouseDetailsFrame.setSize(400, 150); // 设置帧大小
        mouseDetailsFrame.setVisible(true); // 显示帧
    } // 结束 main
} // 结束类 MouseDetails
```
