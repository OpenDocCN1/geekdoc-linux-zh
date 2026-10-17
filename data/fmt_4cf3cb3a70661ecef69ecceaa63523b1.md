
## 绘制

```cpp
void MyWidget::paintEvent(QPaintEvent *event)
{
    QPainter painter(this);
    // ...
}
```

我们可以使用 `QPainter` 的 `draw...()` 函数来绘制各种形状。图 8.1 列出了最重要的函数。绘制的执行方式受 `QPainter` 设置的影响。其中某些设置采用自设备，而另一些则初始化为默认值。三个主要的画家设置是画笔（pen）、画刷（brush）和字体（font）：

**图 8.1. `QPainter` 最常用的 `draw...()` 函数**

![](img/1bc72df8c60cf85926d3aefcc273027d_296_0.png)

画笔（pen）用于绘制线条和形状轮廓。它由颜色、宽度、线样式、线端样式（cap style）和连接样式（join style）组成。画笔样式如图 8.2 和 8.3 所示。

**图 8.2. 线端和连接样式**

![](img/1bc72df8c60cf85926d3aefcc273027d_296_1.png)

**图 8.3. 线样式**

![](img/1bc72df8c60cf85926d3aefcc273027d_297_0.png)

画刷（brush）是用于填充几何形状的模式。它通常由颜色和样式组成，但也可以是纹理（无限重复的位图映射）或渐变。画刷样式如图 8.4 所示。

**图 8.4. 预定义的画刷样式**

[查看全尺寸图像]

![](img/1bc72df8c60cf85926d3aefcc273027d_297_1.png)

字体（font）用于绘制文本。字体有许多属性，包括族（family）和字号（point size）。

可以通过调用 `setPen()`、`setBrush()` 和 `setFont()` 并传入 `QPen`、`QBrush` 或 `QFont` 对象来随时修改这些设置。

让我们来看几个实际中的示例。以下是绘制图 8.5 (a) 所示椭圆的代码：

```cpp
QPainter painter(this);
painter.setRenderHint(QPainter::Antialiasing, true);
painter.setPen(QPen(Qt::black, 12, Qt::DashDotLine, Qt::RoundCap));
painter.setBrush(QBrush(Qt::green, Qt::SolidPattern));
painter.drawEllipse(80, 80, 400, 240);
```

**图 8.5. 几何形状示例**

![](img/1bc72df8c60cf85926d3aefcc273027d_298_0)

`setRenderHint()` 调用启用了抗锯齿，告诉 `QPainter` 在边缘处使用不同的颜色强度，以减少形状边缘转换为像素时通常发生的视觉失真。结果是在支持此特性的平台和设备上获得更平滑的边缘。以下是绘制图 8.5 (b) 所示扇形的代码：

```cpp
QPainter painter(this);
painter.setRenderHint(QPainter::Antialiasing, true);
painter.setPen(QPen(Qt::black, 12, Qt::DashDotLine, Qt::RoundCap));
painter.setBrush(QBrush(Qt::green, Qt::SolidPattern));
painter.drawEllipse(80, 80, 400, 240);
```

以下是绘制图 8.5 (c) 所示贝塞尔曲线的代码：

```cpp
QPainter painter(this);
painter.setRenderHint(QPainter::Antialiasing, true);
painter.setPen(QPen(Qt::black, 12, Qt::DashDotLine, Qt::RoundCap));
painter.setBrush(QBrush(Qt::green, Qt::SolidPattern));
painter.drawEllipse(80, 80, 400, 240);
```

绘制图 8.5 (c) 路径路径 路径的代码：

```cpp
QPainter painter(this);
painter.setRenderHint(QPainter::Antialiasing, true);
painter.setPen(QPen(Qt::black, 12, Qt::DashDotLine, Qt::RoundCap));
painter.setBrush(QBrush(Qt::green, Qt::SolidPattern));
painter.drawEllipse(80, 80, 400, 240);
```

`setRenderHint()` 调用启用了抗锯齿，告诉 `QPainter` 在边缘处使用不同的颜色强度，以减少形状边缘转换为像素时通常发生的视觉失真。结果是在支持此特性的平台和设备上获得更平滑的边缘。

## 坐标系变换

在 `QPainter` 的默认坐标系中，点 `(0, 0)` 位于绘图设备的左上角，`x` 坐标向右增加，`y` 坐标向下增加。在默认坐标系中，每个像素占据 1 x 1 的面积。

从概念上讲，像素的中心位于“半像素”坐标上。例如，小部件左上角的像素覆盖了点 `(0, 0)` 和 `(1, 1)` 之间的区域，其中心位于 `(0.5, 0.5)`。如果我们告诉 `QPainter` 在例如 `(100, 100)` 处绘制一个像素，它将通过在两个方向上平移 `+0.5` 来近似结果，从而绘制出中心在 `(100.5, 100.5)` 的像素。

这种区别起初看起可能很学术化，但在实践中它具有重要的影响。首先，`+0.5` 的偏移只在禁用抗锯齿（默认设置）时发生；如果启用了抗锯齿且我们尝试在 `(100, 100)` 处绘制一个黑色像素，`QPainter` 实际上会将四个像素 `(99.5, 99.5)`、`(99.5, 100.5)`、`(100.5, 99.5)` 和 `(100.5, 100.5)` 涂成浅灰色，以产生像素正好位于四个像素交汇点的印象。如果这种效果是不需要的，我们可以通过指定半像素坐标或通过将 `QPainter` 平移 `(+0.5, +0.5)` 来避免它。

在绘制线、矩形和椭圆等形状时，也适用类似的规则。图 8.7 显示了在关闭抗锯齿的情况下，`drawRect(2, 2, 6, 5)` 调用结果如何根据画笔宽度而变化。特别地需要注意的是，使用宽度为 1 的画笔绘制的 6 x 5 矩形实际上覆盖了 7 x 6 的面积。这与旧的工具包（包括 Qt 的早期版本）不同，但对于实现真正可缩的、与无关的矢量图形至关重要。图 8.8 显示了开启抗锯齿时 `drawRect(2, 2, 6, 5)` 的结果，图 8.9 显示了当我们指定半像素坐标时发生的情况。

**图 8.7. 无抗锯齿时 `drawRect(2, 2, 6, 5)` 的结果**

![](img/1bc72df8c60cf85926d3aefcc273027d_301_0.png)

**图 8.8. 开启抗锯齿时 `drawRect(2, 2, 6, 5)` 的结果**

![](img/1bc72df8c60cf85926d3aefcc273027d_301_1.png)

**图 8.9. 开启抗锯齿时 `drawRect(2.5, 2.5, 6, 5)` 的结果**

![](img/1bc72df8c60cf85926d3aefcc273027d_302_0.png)

现在我们已经理解了默认坐标系，可以仔细查看如何使用 `QPainter` 的视口（viewport）、窗口（window）和世界变换（world transform）来更改它。（在此上下文中，“窗口”不是指顶层小部件意义上的窗口，“视口”与 `QScrollArea` 的视口无关。）

视口和窗口是紧密结合的。视口是用物理坐标指定的任意矩形。窗口指定相同的矩形，但使用的是逻辑坐标。当我们进行绘图时，我们指定逻辑坐标中的点，这些坐标将根据当前的窗口–视口设置，以线性代数的方式转换为物理坐标。

默认情况下，视口和窗口被设置为设备的矩形。例如，如果设备是一个 320 x 200 的小部件，那么视口和窗口都是 320 x 200 的矩形，其左上角位于位置 `(0, 0)`。在这种情况下，逻辑物理坐标系是相同的。

窗口–视口机制对于使绘图代码独立于绘图设备的尺寸或分辨率非常有用。例如，如果我们希望逻辑坐标从 `(-50, -50)` 扩展到 `(50, 50)`，且 `(0, 0)` 在中间，我们可以这样设置窗口：

```cpp
painter.setWindow(-50, -50, 100, 100);
```

`(-50, -50)` 对指定原点，`(100, 100)` 对指定宽度和高度。这意味着逻辑坐标 `(-50, -50)` 现在对应于物理坐标 `(0, 0)`，而逻辑坐标 `(50, 50)` 对应于物理坐标 `(320, 200)`。如图 8.10 所示。在这个例子中，我们没有更改视口。

**图 8.10. 将逻辑坐标转换为物理坐标**

![](img/1bc72df8c60cf85926d3aefcc273027d_303_0.png)

现在是世界变换。世界变换是一个在窗口–视口转换之外应用的变换矩阵。它允许我们对绘制的项目进行平移、缩放、旋转或倾斜（shear）。例如，如果我们想以 45° 的角度绘制文本，将使用以下代码：

```cpp
QTransform transform;
transform.rotate(+45.0);
painter.setWorldTransform(transform);
painter.drawText(pos, tr("Sales"));
```

传递给 `drawText()` 的逻辑坐标通过世界变换转换，然后使用窗口–视口设置映射到物理坐标。

如果我们指定多个变换，它们将按照给出的顺序应用。例如，如果我们想使用点 `(50, 50)` 作为旋转中心，可以通过将窗口平移 `(+50, +50)`，执行旋转，然后将窗口移回原始位置：

```cpp
QTransform transform;
transform.translate(+50.0, +50.0);
transform.rotate(45.0);
transform.translate(-50.0, -50.0);
painter.setWorldTransform(transform);
painter.drawText(pos, tr("Sales"));
```

指定变换的另一种简单方法是使用 `QPainter` 的 `translate()`、`scale()` 和 `shear()` 便利函数：

```cpp
painter.translate(-50.0, -50.0);
painter.rotate(45.0);
painter.translate(+50.0, +50.0);
painter.drawText(pos, tr("Sales"));
```

如果我们反复使用相同的变换，更高效的方法是将它们存储在 `QTransform` 对象中，并在需要变换时为 painter 设置世界变换。

为了说明变换，我们将回顾图 8.11 和 8.12 所示的 `OvenTimer` 小部件代码。`OvenTimer` 是模仿内置时钟的烤箱设计的。用户可以点击刻度来设置时长。指针逆时针旋转直到到达 0，此时 `OvenTimer` 发出 `timeout()` 信号。

**图 8.11. `OvenTimer` 小部件**

![](img/1bc72df8c60cf85926d3aefcc273027d_304_0.png)

**图 8.12. 不同尺寸的 `OvenTimer` 小部件**

![](img/1bc72df8c60cf85926d3aefcc273027d_304_1.png)

```cpp
class OvenTimer : public QWidget
{
    Q_OBJECT

public:
    OvenTimer(QWidget *parent = 0);
    void setDuration(int secs);
    int duration() const;
    void draw(QPainter *painter);

signals:
    void timeout();

protected:
    void paintEvent(QPaintEvent *event);
    void mousePressEvent(QMouseEvent *event);

private:
    QDateTime finishTime;
    QTimer *updateTimer;
    QTimer *finishTimer;
};
```

`OvenTimer` 类派自 `QWidget` 并重新实现了两个虚函数：`paintEvent()` 和 `mousePressEvent()`。

```cpp
const double DegreesPerMinute = 7.0;
const double DegreesPerSecond = DegreesPerMinute / 60;
const int MaxMinutes = 45;
const int MaxSeconds = MaxMinutes * 60;
const int UpdateInterval = 5;
```

在 `oventimer.cpp` 中，我们首先定义控制烤箱计时器外观的常量。

```cpp
OvenTimer::OvenTimer(QWidget *parent)
    : QWidget(parent)
{
    finishTime = QDateTime::currentDateTime();
    updateTimer = new QTimer(this);
    connect(updateTimer, SIGNAL(timeout()), this, SLOT(update()));

    finishTimer = new QTimer(this);
    finishTimer->setSingleShot(true);
    connect(finishTimer, SIGNAL(timeout()), this, SIGNAL(timeout()));

    connect(finishTimer, SIGNAL(timeout()), updateTimer, SLOT(stop()))

    QFont font;
    font.setPointSize(8);
    setFont(font);
}
```

在构造函数中，我们创建两个 `QTimer` 对象：`updateTimer` 用于每五秒刷新一次小部件的外观，`finishTimer` 在烤箱计时器达到 0 时发射小部件的 `timeout()` 信号。`finishTimer` 只需要触发一次，因此我们调用了 `setSingleShot(true)`；默认情况下，计时器会反复触发直到停止或销毁。最后一个 `connect()` 调用是在计时器闲闲时停止更新优化。

在构造函数的结束处，我们将用于绘制小部件的字体大小设置为 9 磅。这样做是为了确保计时器上显示的数字在任何地方都基本相同。

```cpp
void OvenTimer::setDuration(int secs)
{
    secs = qBound(0, secs, MaxSeconds);
    finishTime = QDateTime::currentDateTime().addSecs(secs);
    if (secs > 0) {
        updateTimer->start(UpdateInterval * 1000);
        finishTimer->start(secs * 1000);
    } else {
        updateTimer->stop();
        finishTimer->stop();
    }

    update();
}
```

`setDuration()` 函数将烤箱计时器的时长设置为给定的秒数。使用 Qt 的全局 `qBound()` 函数意味着我们可以避免编写如下代码：

```cpp
if (secs < 0) {
    secs = 0;
} else if (secs > MaxSeconds) {
    secs = MaxSeconds;
}
```

我们通过将时长加上当前时间（从 `QDateTime::currentDateTime()` 获取）来计算结束时间，并存储在 `finishTime` 私有变量中。最后，调用 `update()` 根据新时长重绘小部件。

`finishTime` 变量是 `QDateTime` 类型。由于该变量持有日期和

并且在某些情况下，我们避免了当前时间在午夜之前而结束时间在午夜之后的产生的回绕错误。

```cpp
int OvenTimer::duration() const
{
  int secs = QDateTime::currentDateTime().secsTo(finishTime);
  if (secs < 0)
    secs = 0;
  return secs;
}
```

`duration()` 函数返回计时器到结束前剩余的秒数。如果计时器未激活状态，我们返回 0。

```cpp
void OvenTimer::mousePressEvent(QMouseEvent *event)
{
  QPointF point = event->pos() - rect().center();
  double theta = std::atan2(-point.x(), -point.y()) * 180.0 * M_PI;
  setDuration(duration() + int(theta * DegreesPerSecond));
}
```
