
```cpp
paint.begin(this);

QFontMetrics fm = paint.fontMetrics();

int x = 20;
int y = 20;

string = "Printer name: " + printer.name();
paint.drawText(x,y,string);
y += fm.height();

if(printer.outputFile()) {
  string = "Output to file: " + printer.outputFile();
  paint.drawText(x,y,string);
  y += fm.height();
}

string = "Page size: " + QString(printer.pageSizeRect().toString());
paint.drawText(x,y,string);
y += fm.height();

string = "Full page: " + QString(printer.fullPage() ? "true" : "false");
paint.drawText(x,y,string);
y += fm.height();

string = "Orientation: " + QString(printer.orientation() == QPainter::Portrait ? "portrait" : "landscape");
paint.drawText(x,y,string);
y += fm.height();

string = "Number of copies: " + QString(printer.numCopies());
paint.drawText(x,y,string);
y += fm.height();

string = "Color mode: " + QString(printer.colorMode() == QPrinter::GrayScale ? "gray scale" : "color");
paint.drawText(x,y,string);
y += fm.height();

string = "Number of colors (or shades of gray): " + QString(metrics.numColors());
paint.drawText(x,y,string);
y += fm.height();

string = "Number of bits per dot: " + QString(metrics.depth());
paint.drawText(x,y,string);
y += fm.height();

string = "Page width in millimeters: " + QString(metrics.pageSizeRect().width());
paint.drawText(x,y,string);
y += fm.height();

string = "Page height in millimeters: " + QString(metrics.pageSizeRect().height());
paint.drawText(x,y,string);
y += fm.height();

string = "Horizontal dots per inch: " + QString(metrics.logicalDPIX());
paint.drawText(x,y,string);
y += fm.height();

string = "Vertical dots per inch: " + QString(metrics.logicalDPIY());
paint.drawText(x,y,string);
y += fm.height();

string = "Left and right margin width: " + QString(printer.margins().width());
paint.drawText(x,y,string);
y += fm.height();

string = "Top and bottom margin height: " + QString(printer.margins().height());
paint.drawText(x,y,string);
y += fm.height();

paint.end();
}
```

*注：由于原文文本中代码块部分存在逻辑混乱和重复定义的错误，翻译时已根据“不要重复输出原文”的原则，对代码逻辑对应的翻译描述进行了整理和对齐，确保输出内容的逻辑一致性。*

# 306 第二部分 ♦ 逐步详解

每个点的颜色总数（或灰色的阶调数）通过第 118 行的 `numColors()` 调用返回。同样的信息通过第 123 行的 `depth()` 调用也作为每个点的位数进行报告。

## 将图形拟到窗口

你可以建立自己的坐标系，用它在窗口中绘制图形形，并让你的坐标系自动转换到实际窗口的坐标系。下面的示例展示了如何实现：

头文件

```cpp
/* fitwindow.h */
#ifndef FITWINDOW_H
#define FITWINDOW_H

#include <QWidget.h>

class FitWindow: public QWidget
(
protected:
    virtual void paintEvent(QPaintEvent);
    );
#endif
```

FitWindow

```cpp
/* fitwindow.cpp */
#include <qapp.h>
#include <qpainter.h>
#include "fitwindow.h"

int main(int argc,char **argv)
{
    Application app(argc,argv,"fitwindow");
    FitWindow fitwindow;
    fitwindow.show();
    app.setMainWindow(&fitwindow);
    return(app.exec());
}
void FitWindow::paintEvent(QPaintEvent *)
{
    QPainter p(this);

    p.drawRoundRect(50,50,200,200,30,30);
    p.setBrush(QColor("black"));
    p.drawEllipse(100,100,100,100);

    p.setBrush(QColor("white"));
    p.drawPie(50,50,100,270*16);
    p.drawPie(150,150,100,100*16);
}
```

第 18 行的 `setWindow()` 调用建立了坐标系的左上角。它同时也确定了窗口的高度和宽度，为了绘图尺寸假设大小为 300×300，但当绘制实际像素时，它们会被映射到实际的窗口大小。图 13-5 显示了该程序在两种不同方式调整大小后显示的窗口。

![](img/c47d54674a4d92abc6eebed0dd05f5fb_326_0.png)

**图 13-5：** 调整窗口大小会调整图形的大小。

## 将图形拟到子窗口

上一个示例中的 `setWindow()` 方法可以与 `setViewport()` 方法结合使用，将绘制和绘画缩放到窗口内的子窗口中。下面的示例将同一个图形映射到窗口内的四个子窗口，并导致如图 13-6 所示的显示。

![](img/c47d54674a4d92abc6eebed0dd05f5fb_326_1.png)

**图 13-6：** 同一个图形在同一个窗口中出现四次

# 308 第二部分 ♦ 逐步详解

FitSubWindow 头文件

```
/* fitsubwindow.h */
```
