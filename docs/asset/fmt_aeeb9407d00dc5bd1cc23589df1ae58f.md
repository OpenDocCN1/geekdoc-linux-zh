
`stopAnimation`方法（71–74行）通过调用`Timer stop`停止动画，指示`Timer`应该停止生成事件。此动作是通过调用`repaint`来触发数组中图像的绘制而形成的。[注意：与重启动画一样，本示例定义但没有使用`stopAnimation`方法。我们提供此方法是为了演示之用，或者如果用户想要修改它以便用户可以启动和重启动画。]

## 软件工程观察 21.1

在为应用程序创建动画时，提供一种机制，当用户浏览与动画所在页面不同的新网页时能够禁用动画。

记住，通过扩展`JPanel`类，我们正在创建一个新的GUI组件。我们必须确保我们的新组件在布局目的上像其他组件一样工作。布局管理器通常使用GUI组件的`getPreferredSize`方法（继承自`java.awt.Component`类）来确定组件在作为GUI的部分进行布局时的首选宽度和高度。如果新组件有特定的首选宽度和高度，它应该重写`getPreferredSize`（第83–86行），以`Dimension`类对象（`java.awt`包）返回该宽度和高度。`Dimension`类返回GUI组件的宽度和高度。在本示例中，图像宽160像素，高80像素，因此`getPreferredSize`方法返回一个包含数字160和80的`Dimension`对象（在第34–35行确定）。

## 外观观察 21.1

`JPanel`对象的默认大小为宽10像素、高10像素。

## 外观观察 21.2

当子类`JPanel`（或任何其他`JComponent`）时，如果新组件具有特定的首选宽度和高度，请重写`getPreferredSize`方法。

第77–80行重写了`getMinimumSize`方法。该方法确定组件的最小宽度和高度。与`getPreferredSize`方法一样，新组件应该重写`getMinimumSize`方法（继承自`Component`类）。`getMinimumSize`方法仅调用`getPreferredSize`（一种常见的编程习惯），表示最小尺寸和首选尺寸是相同的。某些布局管理器忽略这些方法指定的维度。例如，`BorderLayout`的`NORTH`和`SOUTH`区域只使用组件的首选高度。

## 外观观察 21.3

如果新的GUI组件有最小宽度和高度（即较小的尺寸将导致组件在（显示器）无法工作），请重写`getMinimumSize`方法，以`Dimension`类实例返回最小宽度和高度。

## 外观观察 21.4

对于许多GUI组件，`getMinimumSize`的实现是返回调用组件`getPreferredSize`方法的结果。

## 21.4 图像映射

图像映射（Image maps）通常用于创建交互式网页。图像映射是一种带有热区域的图像，用户可以点击这些区域来完成任务，例如将不同的网页加载到浏览器中。当用户将鼠标悬停在热区域上时，通常浏览器状态栏或工具提示中会出现描述性消息。

图21.4加载了一张包含书中使用的几个编程提示图标的图像。程序允许用户将鼠标悬停在图标上，以显示与其相关的描述性消息`handlerMoved`（第39–43行）获取鼠标坐标并将其传递给`translationLocation`方法（第58–69行）。`translationLocation`方法将坐标设置为鼠标事件发生时鼠标定位在图标上的位置——该方法返回一条消息。

（基于片段重构的代码结构）

```java
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

public class ImageMap extends JPanel {
    private ImageIcon mapImage;
    private static final String captions[] = { "Common Error", "Good Programming", "Look and Feel Observation", "Performance Tip", "Software Engineering Observation", "Tip" };

    public void init() {
        mapImage = new ImageIcon("icons.png");
        addMouseListener(new MouseAdapter() {
            public void mouseExited(MouseEvent event) {
                showStatus("Pointer outside applet");
            }
        });
        addMouseMotionListener(new MouseAdapter() {
            public void mouseMoved(MouseEvent event) {
                showStatus(translateLocation(event.getX(), event.getY()));
            }
        });
    }

    public void paint(Graphics g) {
        super.paint(g);
        mapImage.paintIcon(this, g, 0, 0);
    }

    public String translateLocation(int x, int y) {
        if (x > mapImage.getWidth() || y >= mapImage.getHeight()) {
            return "";
        }
        double iconWidth = (double) mapImage.getIconWidth() / 7.0;
        int iconNumber = (int) (double) x / iconWidth;
        return captions[iconNumber];
    }
    
    private void showStatus(String message) {
        // Implementation for status bar
    }
}
```

![](img/1df0d1e8ac6007b95647eb8ea38390af_1015_0.png)

**图 21.4** | 图像映射。（4 个部分中的第 4 部分。）

点击图21.4中的applet不会产生任何动作。在第24章“网络”中，我们将讨论如何通过URL和`AppletContext`接口将另一个网页加载到浏览器所需的技巧。使用这些技术，此applet可以将每个图标与URL关联起来，当用户点击时浏览器将显示该URL。

## 21.5 加载和播放音频片段

Java程序可以处理和播放音频片段。用户可以捕制自己的音频片段，软件产品和互联网上也有许多音频片段可用。你的系统需要配备音频硬件（扬声器和声卡）才能播放音频片段。

Java提供了几种在applet中播放声音的机制。其中最简单的两种方法是Applet的`play`方法和`AudioClip`接口的`play`方法。Java Media Framework和Java Sound APIs提供了额外的音频功能。如果你想在程序中播放声音，Applet方法会加载并播放声音——声音在播放后会被标记为垃圾回收。Applet方法有两个版本：

```
public void play(URL location, String fileName);
public void play(URL soundURL);
```

第一个版本从`location`加载存储在文件`fileName`中的音频片段并播放声音。第一个参数通常是调用applet的`getDocumentBase`方法，`getDocumentBase`返回加载applet的HTML文件的位置。（如果applet在一个包中，该方法返回包或包含该包的JAR文件的位置。）方法`getDocumentBase`指明applet的`.class`文件的位置。该方法的第二个版本接收一个包含音频片段位置和文件名的`URL`。该语句

```
play( getDocumentBase(), "hi.au");
```

加载文件`hi.au`中的音频片段并播放一次该片段。
