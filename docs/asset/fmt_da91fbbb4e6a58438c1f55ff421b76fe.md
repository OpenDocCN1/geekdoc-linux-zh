
`paintEvent()` 在显示器需要刷新任何时候都会调用。窗口不会记住你绘制了什么并自动替换它。你的程序必须准备好反复绘制窗口——每当此调用时，它都应该从头开始绘制。通常情况下，即使只绘制控件的一部分，绘制整个内容也没有成本。在内部，绘图被缓冲并复制到显示器，这样在屏幕更新时就不会有闪烁。

从第 14 行开始的构造函数创建一个具有固定大小窗口的控件。构造函数没有进行任何绘图，因为图形只有在窗口实现（即它实际上有一个存储像素值的地方）后才能被显示。

这种限制被称为 `clipping`（裁剪）。

内部，`QPainter` 使用 `QPainter` 对象绘制像素和线条。默认 `QPainter` 是一个像素宽的。这种 `QPainter` 默认是黑色的，绘制了图 12-1 中的线条。

第 19 行的 `paintEvent()` 绘制了图 12-2 所示的矩形。这种 `QPainter` 对象不能用于绘画，因为它没有窗口。第 23 行的 `begin()` 传递给 `drawRect()` 的参数是角的 x 和 y 坐标，然后是它的宽度高度。

虽然必须调用 `begin()` 和 `end()` 方法，但你可以通过在构造函数中指定绘图目标并在析构函数中调用它们来实现（当 `QPainter` 离开作用域时会自动调用）。

每次调用 `begin()` 方法时，`Q` 对象都会完全初始化，无需重置 `QPainter` 的笔和画刷然后使用它绘制。

填充矩形与绘制有所不同。一个示例使用了与之前示例相同的基本尺寸，但产生了图 12-2 所示的填充矩形。

```cpp
/*fillrectangle.cpp */
#include <app.h>
#include <qpainter.h>
#include "fillrectangle.h"

int main(int argc, char *argv)
{
  KApplication app(argc, argv,"fillrectangle");
  DrawRectangle fillrectangle;
  fillrectangle.show();
  app.setMainWindow(&rectangle);
  return(app.exec());
}

DrawRectangle::DrawRectangle(QWidget *parent,
const char *name) : QWidget(parent,name)
{
  setFixedSize(400,200);
}

void DrawRectangle::paintEvent(QEvent *)
{
  QBrush brush(QColor("black"));
  QPainter p;
  p.begin(this);
  p.fillRect(50,50,300,100,brush);
  p.end();
}
```

![](img/c47d54674a4d92abc6eebed0dd05f5fb_282_0.png Figure 12-2: 窗口中心的填充矩形)

# 264 第二部分 ♦ 逐步步营

绘图从第 19 行开始的 `paintEvent()` 方法中执行。绘制是使用 `QPen` 对象完成的，默认是黑色笔；填充则使用 `brush` 完成，而默认画刷不进行任何绘制。因此，`paintEvent()` 方法的第 21 行创建了一个 `QBrush` 对象，可以使用它用黑色像素填充整个区域。

`QPainter` 对象在第 22 行创建，并在第 23 行附加到小部件上。第 24 行的 `fillRect()` 调用（之前的 `drawRect()`）需要矩形左上角的 x 和 y 坐标，以及矩形的宽度和高度。它还需要用于填充矩形的画刷。

可以同时对矩形进行绘制和填充。以下示例通过使用白色画刷进行填充矩形，然后用黑色画笔勾勒白色区域的轮廓：

```cpp
void Rectangle2::paintEvent(QEvent *) {
    QBrush brush(QColor("white"));
    QPainter p;
    p.begin(this);
    p.fillRect(50,50,300,100,brush);
    p.drawRect(50,50,300,100);
    p.end();
}
```

结果如图 12-3 所示。矩形在绘制之前必须先填充，因为绘制矩形的外边缘与填充后矩形的外边缘完全匹配，而且填充矩形的操作会擦除可能存在的任何内容。

![](img/c47d54674a4d92abc6eebed0dd05f5fb_283_0.png)

**图 12-3：** 矩形的填充与轮廓绘制

还有另一种方法。所有的绘制方法都可以用于勾勒形状并填充形状。轮廓使用画笔；填充使用画刷。图 12-3 所示的矩形也可以通过以下 `paintEvent()` 方法产生：

```cpp
void FillRectangle3::paintEvent(QPaintEvent *) {
    QBrush brush(QColor("white"));
    QPainter p;
    p.begin(this);
    p.setBrush(brush);
    p.drawRect(0,50,300,100);
    p.end();
}
```
