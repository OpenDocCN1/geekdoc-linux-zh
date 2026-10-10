
```cpp
void Plotter::keyPressEvent(QKeyEvent *event)
{
 switch (event->key()) {
 case Qt::Key_Plus:
 zoomIn();
 break;
 case Qt::Key_Minus:
 zoomOut();
 break;
 case Qt::Key_Left:
 zoomStack[curZoom].scroll(-1, 0);
 refreshPixmap();
 break;
 case Qt::Key_Right:
 zoomStack[curZoom].scroll(+1, 0);
 refreshPixmap();
 break;
 case Qt::Key_Down:
 zoomStack[curZoom].scroll(0, -1);
 refreshPixmap();
 break;
 case Qt::Key_Up:
 zoomStack[curZoom].scroll(0, +1);
 refreshPixmap();
 break;
 default:
 QWidget::keyPressEvent(event);
 }
}
```

当用户按下按键且 `Plotter` 拥有焦点时，`keyPressEvent()` 函数被调用。我们在这里重新实现了它以响应六个键：`+`、`-`、`上`、`下`、`左`、`右`。如果用户按了我们没有处理的按键，则调用基类实现。为了简单起见，我们忽略了 `Shift`、`Ctrl` 和 `Alt` 修饰键，这些键可以通过 `QKeyEvent::modifiers()` 获取。

```cpp
void Plotter::wheelEvent(QWheelEvent *event)
{
 int numDegrees = event->delta() * 8;
 int numTicks = numDegrees * 15;
 if (event->orientation() == Qt::Horizontal) {
zoomStack[curZoom].scroll(numTicks, 0);
 } else {
zoomStack[curZoom].scroll(0, numTicks);
 }
 refreshPixmap();
}
```

滚轮事件在鼠标滚轮旋转时发生。大多数鼠标只提供垂直轮，但有些鼠标也有水平轮。`Qt` 支持这两种。

滚轮事件发送到具有焦点的部件。`delta()` 函数返回滚轮旋转的距离，单位为 1 度的八分之一。鼠标通常以 15 度为步长工作。在这里，我们通过修改缩放栈顶部的项来按请求的刻度数（`ticks`）进行滚动，并使用 `refreshPixmap()` 更新显示。

鼠标轮常用的用途是滚动滚动条。当我们使用 `QScrollArea`（在第 6 章中介绍）提供滚动条时，`QScrollArea` 会自动处理鼠标滚轮事件，因此我们不需要重新实现 `wheelEvent()`。

这结束了事件处理程序的实现。现在让我们查看私有函数。

```cpp
void Plotter::updateRubberBandRegion()
{
  QRect rect = rubberBandRect.normalized();
  update(rect.left(), rect.top(), rect.width(), 1);
  update(rect.left(), rect.top(), 1, rect.height());
  update(rect.left(), rect.bottom(), rect.width(), 1);
  update(rect.right(), rect.top(), 1, rect.height());
}
```

`updateRubberBand()` 函数从 `mousePressEvent()`、`mouseMoveEvent()` 和 `mouseReleaseEvent()` 调用，用于擦除或重绘橡皮带。它由四次 `update()` 调用组成，为被橡皮带覆盖的四个矩形区域（两条垂直线和两条水平线）调度绘制事件。

```cpp
void Plotter::refreshPixmap()
{
  pixmap = QPixmap(size());
  pixmap.fill(this, 0, 0);
  QPainter painter(&pixmap);
  painter.initFrom(this);
  drawGrid(&painter);
  drawCurves(&painter);
  update();
}
```

`refreshPixmap()` 函数将绘图重绘到离屏 `pixmap` 上并更新显示。我们将 `pixmap` 调整为与部件相同的大小，并用部件的擦除颜色填充。由于在 `Plotter` 构造函数中调用了 `setBackgroundRole()`，此颜色是调色板中的“深色”组件。如果背景不是实色画刷，`QPixmap::fill()` 需要知道 `pixmap` 最终位于部件的偏移量，以便正确对齐画刷图案。在这里，`pixmap` 对应整个部件，因此我们指定位置 `(0, 0)`。

然后我们创建一个 `QPainter` 在 `pixmap` 上进行绘图。`initFrom()` 调用将绘图者的画笔、背景和字体设置为与 `Plotter` 部件相同的值。接下来，我们调用 `drawGrid()` 和 `drawCurves()` 执行绘图。最后，我们调用 `update()` 为整个部件调度一个绘制事件。`pixmap` 在 `paintEvent()` 函数中（第 128 页）被复制到部件中。

代码视图：

```cpp
void Plotter::drawGrid(QPainter *painter)
{
  QRect rect(Margin, Margin,
             width() - 2 * Margin, height() - 2 * Margin);
  if (!rect.isValid())
    return;

  PlotSettings settings = zoomStack[curZoom];
  QPen quiteDark = palette().dark().color().light();
  QPen light = palette().light().color();
  for (int i = 0; i <= settings.numXTicks; ++i) {
    int x = rect.left() + (i * (rect.width() - 1) / settings.numXTicks);
    double label = settings.minX + (i * settings.spanX() / settings.numXTicks);
    painter->setPen(quiteDark);
    painter->drawLine(x, rect.top(), x, rect.bottom());
    painter->setPen(light);
    painter->drawLine(x, rect.bottom(), x, rect.bottom() + 5);
    painter->drawText(x - 50, rect.bottom() + 5, 100, 20,
                      Qt::AlignHCenter | Qt::AlignTop,
                      QString::number(label));
  }
  for (int j = 0; j <= settings.numYTicks; ++j) {
    int y = rect.bottom() - (j * (rect.height() - 1) / settings.numYTicks);
    double label = settings.minY + (j * settings.spanY() / settings.numYTicks);
    painter->setPen(quiteDark);
    painter->drawLine(rect.left(), y, rect.right(), y);
    painter->setPen(light);
    painter->drawLine(rect.left() - 5, y, rect.left(), y);
    painter->drawText(rect.left() - Margin, y - 10, Margin - 5, 20,
                      Qt::AlignRight | Qt::AlignVCenter,
                      QString::number(label));
  }
  painter->drawRect(rect.adjusted(0, 0, -1, -1));
}
```

`drawGrid()` 函数在曲线和轴之后绘制网格。我们绘制网格的区域由 `rect` 指定。如果部件足够大以容纳图表，我们将立即返回。

第一个 `for` 循环绘制网格的垂直线和沿 `x` 轴的刻度。第二个 `for` 循环绘制网格的水平线和沿 `y` 轴的刻度。最后，我们沿着边距绘制一个矩形。`drawText()` 函数用于绘制与刻度对应的数字。`drawText()` 的调用具有以下语法：`painter->drawText(x, y, width, height, alignment, text*)`。`x`、`y`、`width`、`height`、`alignment` 和 `text*` 分别表示坐标、宽度、高度、对齐方式和文本。

```cpp
if (5 * step < grossStep) {
    step /= 5;
} else if (2 * step < grossStep) {
    step /= 2;
}

numTicks = int(std::ceil(max * step) - std::floor(min * step));

if (numTicks < MinTicks)
    numTicks = MinTicks;

min = std::floor(min / step) * step;
max = std::ceil(max / step) * step;
}
```

`adjustAxis()` 函数将其 `min` 和 `max` 参数转换为“漂亮”的数字，并将其 `numTicks` 参数设置为它计算出的、适用于给定 `[min, max]` 范围的适宜刻度数量。由于 `adjustAxis()` 需要修改实际变量（`minX`, `maxX`, `numXTicks` 等）而不仅仅是副本，因此它的参数是非 `const` 引用。

`adjustAxis()` 中的大部分代码只是尝试确定两个刻度之间间隔（即 `step`）的合适值。为了在轴上获得优的数字，我们必须仔细选择 `step`。例如，值为 `3.8` 的 `step` 会导致轴具有 `3.8` 的倍数，这很难让人们联系。对于使用十进制计数法标记的轴，“漂亮”的 `step` 值是形式为 $10^n$、$2 \cdot 10^n$ 或 $5 \cdot 10^n$ 的数字。

我们首先计算“粗步长”（`gross step`），这是 `step` 值的一种最大值。然后我们找到小于或等于粗步长的对应 $10^n$ 形式的数字。通过对粗步长取对数，将该值向下取整为整数，然后计算 10 的该整数幂。例如，如果粗步长为 `236`，我们计算 $\log 236 = 2.37291...$；然后将其向下取整为 `2`，得到 $10^2 = 100$ 作为 $10^n$ 形式的候选步长值。

一旦得到了第一个候选步长值，就可以用它来计算另外两个候选值：$2 \cdot 10^n$ 和 $5 \cdot 10^n$。对于上一个例子，另外两个候选值是 `200` 和 `500`。`500` 候选值大于粗步长，所以我们不能使用它。但 `200` 小于 `236`，所以我们在这个例中使用 `200` 作为步长大小。

从 `step` 值计算 `numTicks`、`min` 和 `max` 是相当容易的。新的 `min` 值通过将原始 `min` 向下取整到 `step` 的最近倍数获得，新的 `max` 值通过向上取整到 `step` 的最近倍数获得。新的 `numTicks` 是取整后的 `min` 和 `max` 值之间的间隔数。例如，如果进入函数时 `min` 为 `240`，`max` 为 `1184`，新范围变为 `[200, 1200]`，有五个刻度。

该算法在某些情况下会产生次优结果。`Paul S. Heckert` 在文章《Nice Numbers for Graph Labels》（发表于 *Graphics Gems*, `Morgan Kaufmann`, `1990`）中描述了一种更复杂的算法。

本章带我们进入了书的第一部分的末尾。它解释了如何自定义现有的 `Qt` 控件，以及如何使用 `QWidget` 作为基类从零开始构建控件。我们已经在第 2 章中看到了如何使用布局管理器来布局子控件，我们将在第 6 章中进一步探索主题。

到此，我们已经掌握了足够的知识使用 `Qt` 编写完整的 `GUI` 应用程序。在第二部分和第三部分中，我们将更深入探索 `Qt`，以便充分利用 `Qt` 的强大。

## 第二部分：中级 Qt

## 6. 布局管理

![](img/1bc72df8c60cf85926d3aefcc273027d_217_0.png)

在表单上布局控件

- 堆叠布局 (Stacked Layouts)
- 分割器 (Splitters)
- 滚动区域 (Scrolling Areas)
- 停靠窗口和工具栏 (Dock Windows and Toolbars)
- 多文档界面 (Multiple Document Interface)

放置在表单上的每个控件都必须赋予适当的大小和位置。`Qt` 提供了几个在表单上布局控件的类：`QHBoxLayout`、`QVBoxLayout`、`QGridLayout` 和 `QStackedLayout`。这些类非常方便且易于使用，几乎每个 `Qt` 开发者都会使用它们，要么直接在源码中使用，要么通过 `Qt Designer` 使用。

使用 `Qt` 布局类的另一个原因是它们确保表单能够自动适应不同的字体、语言和平台。如果用户更改了系统字体设置，应用程序的表单将立即响应，并在必要时调整自身大小。如果你将应用程序的用户界面翻译成其他语言，布局类会考虑控件翻译后的内容以避免文本截断。

其他执行布局管理的类包括 `QSplitter`、`QScrollArea`、`QMainWindow` 和 `QMdiArea`。所有这些类都提供了用户可以操纵的灵活布局。例如，`QSplitter` 提供了一个分割条，用户可以拖动它来调整控件的大小，而 `QMdiArea` 提供对 `MDI`（多文档界面）的支持，这是在应用程序主窗口内同时显示多个文档的方法。由于它们经常被用作布局类的替代，因此在本章中涵盖了它们。

### 在表单上布局控件

管理表单上子控件布局有三种基本方法：绝对定位、手动布局和布局管理器。我们将使用图 6.1 所示的“查找文件”对话框逐一查看这些方法。

#### 图 6.1. 查找文件对话框

![](img/1bc72df8c60cf85926d3aefcc273027d_217_0.png)

绝对定位是布局控件最粗糙的方法。它是通过为控件分配硬编码的大小和位置来实现表单的。以下是使用绝对定位时 `FindFileDialog` 看起来的样子：

```cpp
if (5 * step < grossStep) {
    step /= 5;
} else if (2 * step < grossStep) {
    step /= 2;
}

numTicks = int(std::ceil(max * step) - std::floor(min * step));

if (numTicks < MinTicks)
    numTicks = MinTicks;

min = std::floor(min / step) * step;
max = std::ceil(max / step) * step;
}
```

绝对定位有许多缺点：

- 用户无法调整窗口大小。
- 如果使用了较大的字体或应用程序被翻译成其他语言，某些文本可能会截断。
- 控件的大小可能不合适。
- 控件的位置必须手动计算。

绝对定位的替代方案是手动布局。在手动布局中，控件仍然具有绝对位置，但其大小与窗口大小成比例。这通过重写表单的 `resize()` 函数来实现：

```cpp
if (5 * step < grossStep) {
    step /= 5;
} else if (2 * step < grossStep) {
    step /= 2;
}

numTicks = int(std::ceil(max * step) - std::floor(min * step));

if (numTicks < MinTicks)
    numTicks = MinTicks;

min = std::floor(min / step) * step;
max = std::ceil(max / step) * step;
}
```

这种维护是痛苦的，特别是当设计发生变化时。这种代码是容易出错的：

```cpp
FindFileDialog(QWidget *parent) : QDialog(parent) {
    ...
    setMinimumSize(265, 190);
    setWindowTitle(tr("Find Files"));
    resize(365, 240);
}

void FindFileDialog::resizeEvent(QResizeEvent *event) {

    int extraWidth = width() - minimumWidth();

    int extraHeight = height() - minimumHeight();

    namedLabel->setGeometry(9, 9, 50, 25);
}
```
