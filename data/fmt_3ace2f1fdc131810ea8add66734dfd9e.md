
在类的私有区域，我们声明了几个用于绘制小部件的函数、一个常量以及若干成员变量。`Margin`常量用于在图表周围留出间距。变量之一之一类型为`QPixmap`的`pixmap`。该变量持有整个小部件渲染的副本，与屏幕显示的内容完全相同。图表始终先绘制到离屏`pixmap`上；然后将该`pixmap`拷贝到小部件上。

```cpp
class PlotSettings {
public:
    PlotSettings();
    void scroll(int dx, int dy);
    void adjust();
    double spanX() const { return maxX - minX; }
    double spanY() const { return maxY - minY; }
private:
    double minX;
    double maxX;
    int numXTicks;
    double minY;
    double maxY;
    int numYTicks;
    static void adjustAxis(double &min, double &max, int &numXTicks);
};
```

`PlotSettings`类指定了 x 轴和 y 轴的范围以及这些轴的刻度数量。图 5.8 显示了`PlotSettings`对象与`Plotter`小部件之间的对应。根据约定，`numXTicks`和`numYTicks`是开启的；如果`numXTicks`为五，`Plotter`实际上会在 x 轴上绘制刻度线。这简化了后续计算。

图 5.8 `PlotSettings`的成员变量

现在让我们查看实现文件：

```cpp
#include <QtGui>
#include <cmath>
#include "plotter.h"
```

我们包含了预期的头文件，并将所有`std`命名空间的符号导入到全局命名空间。这允许在不加`std::`前缀的情况下访问`<cmath>`中声明的函数（例如，使用`floor()`而不是`std::floor()`）。

```cpp
Plotter::Plotter(QWidget *parent)
    : QWidget (parent)
    setBackgroundRole(QPalette::Dark)
{
    setAutoFillBackground(true);
    setSizePolicy(QSize::Expanding, QSizePolicy::Expanding);
    setFocusPolicy(Qt::StrongFocus);
    rubberBandShown = false;
    zoomIn = new ToolButton(this);
    zoomIn->setIcon(QIcon("/images/zoom.png"));
    zoomIn->adjustSize();
    connect(zoomIn, SIGNAL(clicked()), this, SLOT(zoomIn()));
    zoomOut = new ToolButton(this);
    zoomOut->setIcon(QIcon("/images/zoomout.png"));
    zoomOut->adjustSize();
    connect(zoomOut, SIGNAL(clicked()), this, SLOT(zoomOut()));
    setPlotSettings(PlotSettings());
}
```

注意：`setBackgroundRole()`调用`QWidget`使用调色板中的“dark”部分作为擦除小部件的颜色，而不是“window”部分。这是 Qt 的默认颜色，当小部件调整为更大的尺寸时，在`paintEvent()`有机会绘制新像素之前，可以使用它来填充任何新暴露的像素。我们还需要设置`setAutoFillBackground(true)`来启用此机制。（默认情况下，小部件继承其父小部件的背景。）

`setSizePolicy()`将小部件尺寸策略在两个方向上都设置为`QSizePolicy::Expanding`。这告诉任何负责该小部件的布局管理器，它非常乐于增长，也可以缩小。默认在两个方向都是`QSizePolicy::Preferred`，这意味着小部件倾向于保持其`size hint`大小，但在必要时可以缩小到其最小`size hint`或无限扩展。

`setFocusPolicy(Qt::StrongFocus)`让小部件能够通过点击或按 Tab 键来接受焦点。`Plotter`理解几个按键：`+`用于放大；`-`用于缩小；以及所有用于向下、向左和向右滚动的键。

# 双缓冲

同样在构造函数中，我们创建了两个`ToolButton`，每个带有一个图标。这些按钮允许我们放大和缩小。按钮图标存储在资源文件中，因此任何使用`Plotter`小部件的应用程序都需要在其`.pro`文件中包含此条目：

```
RESOURCES = plotter.qrc
```

资源文件与我们在电子表格应用程序中使用的类似：

```xml
<!DOCTYPE RCC><RCC version="1.0">
<resource>
  <file>images/zoomin.png</file>
  <file>images/zoomout.png</file>
</resource>
</RCC>
```

调整器调用按钮将它们的大小设置为`size hint`大小。按钮没有放在布局中；相反，我们在`Plotter`的`resize`事件中手动放置它们。由于我们没有使用任何布局，必须通过传递给`QPushButton`来显式指定按钮属性。

```cpp
void Plotter::setPlotSettings(const PlotSettings &settings) {
    zoomStack.clear();
    zoomStack.append(settings);
    curZoom = 0;
    zoomInButton->hide();
    zoomOutButton->hide();
    refreshPixmap();
}
```

`setPlotSettings()`函数用于为图表指定`PlotSettings`。每当用户放大时，都会创建一个新的`PlotSettings`实例并放入栈中。`curZoom`代表当前的缩放级别。

## 双缓冲缓冲

```cpp
refreshPixmap();
}
```

`clearCurve()`函数从曲线图中移除指定的曲线。

```cpp
QSize Plotter::minimumSizeHint() const
{
    return QSize(6 * Margin, 4 * Margin);
}
```

`minimumSizeHint()`函数与`sizeHint()`类似；就像`sizeHint()`指定了组件的理想尺寸一样，`minimumSizeHint()`指定了组件的理想最小尺寸。布局永远不会将组件的大小调整到其最小尺寸提示以下。

该值返回 300×200（因为`Margin`等于 50），以便为四边留出边缘并为图表本身留出空间。低于此尺寸，图表将太小而无法使用。

```cpp
QSize Plotter::sizeHint() const
{
    return QSize(12 * Margin, 8 * Margin);
}
```

在`sizeHint()`中，我们返回一个与`Margin`常数成比例的“理想”尺寸，并使用与`minimumSizeHint()`相同的 3:2 宽高比。

到此，`Plotter`公有函数和槽的审查结束。现在让我们查看受保护的事件处理程序。

```cpp
void Plotter::paintEvent(QEvent * /* event */)
{
    QStylePainter painter(this);
    painter.drawPixmap(0, 0, pixmap);
    if (rubberIsShow) {
        painter.setPen(palette().light().color());
        painter.drawRect(rubberBandRect.normalized()
            adjusted(0, 0, -1, -1));
    }
    if (hasFocus()) {
        QStyleFocusRect option;
        option.initFrom(this);
        option.backgroundColor = palette().dark().color;
        painter.drawPrimitive(QStyle::PE_FrameFocusRect, option);
    }
}
```

通常，`paintEvent()`是我们执行所有绘制的地方。但在这里，所有的绘制工作都在`refreshPixmap()`中提前完成，因此我们可以通过简单将`pixmap`复制到组件的`(0, 0)`位置来渲染整个图表。

如果橡皮筋（rubber）可见，我们在图表上层绘制它。我们使用组件当前颜色组中的“亮”部分作为画笔，以确保与“暗”背景形成良好对比。注意，我们直接在组件上绘制，而不触碰离屏的`pixmap`。使用`QRect::normalized()`确保橡皮筋矩形具有正宽度和高度（在必要时交换坐标），而`adjusted()`将矩形缩小一个像素，以留出其 1 像素宽的轮廓。

如果`Plotter`有一个使用样式`drawPrimitive()`函数绘制的焦点框，其中`QStyle::FrameFocusRect`是第一个参数，`QStyleOptionFocusObject`是第二个参数。矩形的绘制选项继承自`Plotter`组件（通过调用`initFrom()`）。必须显式地指定背景颜色。

当我们想要使用当前样式时，可以直接调用`QStyle`函数，例如：

```cpp
style()->drawPrimitive(QStyle::PE_FocusRect, &option, painter);
```

或者我们可以使用`QPainter`代替普通的`Painter`（正如我们在`Plotter`中做的那样），并利用它更方便地进行绘制。

`Widget::style()`函数返回用于绘制组件的样式。在 Qt 中，样式（style）是`QStyle`的子类。内置样式包括`WindowStyle`、`WindowsXPStyle`、`FusionStyle`、`QCStyle`、`QMacStyle`和`QPlasticStyle`。这些样式都重新实现了`QStyle`中的虚函数，以便为样式模拟的平台以正确的方式进行绘制。`Painter::drawPrimitive()`调用`QStyle`函数来绘制“原始元素”，如面板、按钮和焦点框。对于使用`Application::style()`的应用程序，所有组件的样式通常相同，但可以使用`Widget::setStyle()`基于单个组件进行重写。

通过派生`QStyle`可以定义自定义样式。这可以为应用程序或系列应用程序提供独特的视觉。虽然通常建议使用目标平台的原生外观和感受，但如果你想尝试冒险，Qt 提供了很大的灵活性。

Qt 的内置组件几乎完全依赖`QStyle`来绘制它们自己。这就是为什么它们在 Qt 支持的所有平台上看起来都像原生组件的原因。自定义组件可以通过使用`QStyle`自行绘制，或者通过使用 Qt 组件作为子组件来实现样式感知的。对于`Plotter`，我们结合了这两种方法：焦点框使用`QStyle`（通过`QPainter`）绘制，而放大/缩小按钮是内置的 Qt 组件。

```cpp
void Plotter::resizeEvent (QResizeEvent *event) { /* ... */
	int x = width() - (zoomInButton->width()
	+ zoomOutButton->width() + 10);
	zoomInButton->move(x, 5);
	zoomOutButton->move(x + zoomInButton->width() + 5, 5);
	refreshMap();
}
```

## 5. 创建自定义组件

每当`Plotter`组件调整大小时时，Qt 都会生成一个“调整大小”事件。在这里，我们重新实现了`resizeEvent()`，将放大和缩小按钮放置在`Plotter`组件的右上角。

我们将放大和缩小按钮并排移动，它们之间有 5 像素的间隙，并且距离父组件顶部和右边缘有 5 像素的偏移。

如果我们想让按钮留在左上角，我们将相应地调整坐标。然而，将它们放在右上角是绘图工具的一种常见 UI 模式。

# 双双缓冲

# 127

```cpp
settings.minX = prevSettings.minX + dx * rect.left();
settings.maxX = prevSettings.minX + dx * rect.right();
settings.minY = prevSettings.maxY - dy * rect.bottom();
settings.maxY = prevSettings.maxY - dy * rect.top();
settings.adjust();
zoomStack.resize(curZoom + 1);
zoomStack.append(settings);
zoomIn();
```

当用户释放鼠标按钮时，我们会擦除橡皮带并恢复标准的箭头光标。如果橡皮带的大小至少为 4 x 4，我们就执行缩放操作。如果橡皮带小于此尺寸，很可能是用户误点击了小部件或为了使其获取焦点，因此我们什么都不做。

执行缩放的代码有点复杂。这是因为我们需要同时处理小部件坐标和绘图器坐标。在这里执行的大部分工作是将`rubberBandRect`从小部件坐标转换为绘图器坐标。一旦完成转换，就可以调用`PlotSettings::adjust()`对数字进行四舍五入并并每个轴找到一个合理的刻度数量。图 5.10 和 5.11 展示了这种情况。

![](img/34bd675de80edd220dc2d53b429caf78_144_0.png)

**图 5.10.** 将橡皮带从小部件坐标转换为绘图器坐标

![](img/34bd675de80edd220dc2d53b429caf78_144_1.png)

**图 5.11.** 调整绘图器坐标并对橡皮带进行缩放

```cpp
void Plotter::wheelEvent(QWheelEvent *event)
{
    int degrees = event->delta() / 8;
    int numTicks = degrees / 15;
    if (event->orientation() == Qt::Horizontal) {
        zoomStack[curZoom].scroll(numTicks, 0);
    } else {
        zoomStack[curZoom].scroll(0, numTicks);
    }
    refreshPixmap();
}
```

# 双双缓冲

当滚动鼠标轮时会发生滚轮事件。大多数鼠标只提供垂直滚轮，但某些鼠标也有水平滚轮。Qt 支持这两种滚轮。滚轮事件发送到获得焦焦轮。`delta(int)`函数返回滚轮旋转的距离（以八分之一计）。鼠标通常以 15 度为步长工作。在这里，我们通过修改`dock`栈顶部的项目来按请求的刻度数进行滚动，并使用`refreshPixmap()`更新显示。

鼠标轮最常见的用途是滚动滚动条。当我们使用`QScrollArea`（第 6 章将介绍）提供滚动条时，`QScrollArea`会自动处理滚轮事件，因此我们不需要自己实现`wheelEvent()`。

事件处理程序的实现到此结束。现在让我们回顾私有函数：

```cpp
void Plotter::updateRubberBandRegion(
  QRect rect = rubberBand.normalized());
  update(rect.left(), rect.top(), rect.width(), 1);
  update(rect.left(), rect.top(), 1, rect.height());
  update(rect.left(), rect.bottom(), rect.width(), 1);
  update(rect.right(), rect.top(), 1, rect.height());
}
```

`updateRubberBand()`函数从`mousePressEvent()`和`mouseMoveEvent()`中调用，用于擦除或重绘橡皮带。它包含四次对`update()`的调用，为橡皮带覆盖的小矩形区域（两条垂直线和两条水平线）调度绘制事件。Qt 提供了`RubberBand`类来绘制橡皮带，但在这里，硬编码提供了最终的控制。

```cpp
void Plotter::refreshPixmap() {
  QPixmap pixmap = QPixmap(size());
  pixmap.fill(this, 0, 0);
  QPainter painter(&pixmap);
  painter.initFrom(this);
  drawGrid(&painter);
```
