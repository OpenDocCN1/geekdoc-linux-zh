
第 32 行使用 `ImageIcon paintIcon` 来显示图像。该方法需要四个参数——用于显示图像的 `Component` 引用、用于渲染图像的 `Graphics` 对象引用、图像左上角的 x 坐标以及图像左上角的 y 坐标。

## 21.3 序列图像的动画

下一个示例演示了存储在 `ImageIcons` 数组中的系列图像的动画。图 21.2–21.3 展示的动画是通过一个名为 `LogoAnimatorPanel` 的 `JPanel` 子类（图 21.2）实现的，该类可以附加到应用程序窗口或 JApplet。`LogoAnimator` 类（图 21.3）声明了一个 `main` 方法（图 21.3 的第 8–20 行）来执行动画。`main` 方法创建 `JFrame` 类的实例，并将 `LogoAnimatorPanel` 对象附加到 `JFrame` 上以显示动画。

图 21.2 一组图像的动画。（3 部分中的第一部分）

```java
private Timer animationTimer; // Timer 驱动动画
// 构造函数通过加载图像初始化 LogoAnimatorJPanel
public LogoAnimatorJPanel()
{
    images = new ImageIcon[TOTAL_IMAGES];
    // 加载 30 张图像
    for (int count = 0; count < images.length; count++) {
        images[count] = new ImageIcon(getClass().getResource("/images/" + IMAGE_NAME + ".gif"));
    }
    // 此示例假设所有图像具有相同的宽度和高度
    width = images[0].getWidth(); // 获取图像宽度
    height = images[0].getHeight(); // 获取图像高度
} // LogoAnimatorJPanel 构造函数结束

// 显示当前图像
public void paintComponent(Graphics g)
{
    super.paintComponent(g); // 调用父类的 paintComponent
    images[currentImage].paint(this, 0, 0);
}
// 仅当 Timer 运行时设置下一张要绘制的图像
if (animationTimer.isRunning()) {
    currentImage = (currentImage + 1) % TOTAL_IMAGES;
} // 方法 paintComponent结束

// 启动动画，或窗口重新部署时重启
public void startAnimation()
{
    if (animationTimer == null) {
        currentImage = 0; // 显示第一张图像
        // 创建定时器
        animationTimer = new Timer(ANIMATION_DELAY, new TimerHandler());
        animationTimer.start(); // 启动 Timer
    } // if结束
    else // animationTimer 已经存在，重启动画
    {
        if (!animationTimer.isRunning()) {
            animationTimer.restart();
        } // else结束
    } // 方法 startAnimation结束

// 停止动画 Timer
public void stopAnimation()
{
}
```

图 21.2 | 一组图像的动画。（3 部分中的第2 部分。）

```java
// animationTimer.stop();
} // 方法 stopAnimation结束
// 返回动画的最小尺寸
public Dimension getMinimumSize()
{
    return getPreferredSize();
} // 方法 getMinimumSize结束
// 返回动画的首选尺寸
public Dimension getPreferredSize()
{
    return new Dimension(width, height);
} // 方法 getPreferredSize结束

// 处理来自'timer'动作事件的内部类
private class TimerHandler implements ActionListener
{
    // 响应 Timer 的事件
    public void actionPerformed(ActionEvent actionEvent) {
        repaint(); // 重绘动画器
    } // 方法 actionPerformed结束
} // 类 TimerHandler结束
 // 类 LogoAnimatorJPanel结束
```

图. 21.2 | 一组图像的动画。（3 部分中的第三部分。）

```java
// Fig. 21.3: LogoAnimator.java
// 一组图像的动画。
import javax.swing.JFrame;
public class LogoAnimator
{
    // 在 JFrame 中执行动画
    public static void main(String[] args) {
        LogoAnimator animation = new LogoAnimatorJPanel();
        JFrame window = new JFrame("Animator test"); // 设置窗口
        window.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        window.add(animation); // 将面板添加到框架

        window.pack(); // 使窗口足够大以容纳 GUI
        window.setVisible(true); // 显示窗口
        animation.startAnimation(); // 开始动画
    }
} end 类 LogoAnimator
```

图 21.3 | 在 JFrame 上显示动画图像。（2 部分中的第一部分。）

![](img/1df0d1e8ac6007b95647eb8ea38390af_1010_0.png)

![](img/1df0d1e8ac6007b95647eb8ea38390af_1010_1.png)

![](img/1df0d1e8ac6007b95647eb8ea38390af_1010_2.png)

![](img/1df0d1e8ac6007b95647eb8ea38390af_1010_3.png)

图 21.3 | 在 JFrame 上显示动画图像。（2 部分中的第二部分。）

从第 11 章中了解到，任何 `paintComponent` 方法的第一条语句都应该是调用父类的 `paintComponent` 方法，以确保 Swing 组件能够被正确重绘。

如果动画更早开始，那么我们的 `Timer` 已经创建，且第 5 行的条件为 `false`。程序继续执行第 65–66 行，重启程序之前停止的动画。第 65 行的 `if` 条件使用 `Timer` 方法来判断 `Timer` 是否正在运行（即正在生成事件）。如果它没有运行，第 66 行调用 `Timer restart` 来指示 `Timer` 应该重新生成事件。一旦发生这种情况，`actionPerformed` 方法（Timer 的事件处理器）将以固定间隔被调用。每次都会调用 `repaint` 方法（第 94 行），导致 `paintComponent` 被调用并显示图像。

第 43 行绘制数组中元素 `currentImage` 存储的 `ImageIcon`。第 46–47 行判断动画是否正在运行，如果是，则通过将 `currentImage` 加 1 来确定下一个要显示的图像。取余计算确保了当 `currentImage` 超过 29（数组中的最后一个索引）时，其值被设置为 0（以重复动画序列）。`if` 语句确保了如果在 `Timer` 停止时调用 `paintComponent`，将显示相同的图像。这段代码允许用户启动和停止动画。例如，如果动画停止且用户用另一个窗口覆盖了它，然后取消覆盖，`paintComponent` 将被调用。在这种情况下，我们不希望动画显示下一张图像（因为动画已经停止了）。我们只想让窗口在动画重启之前显示相同的图像。
