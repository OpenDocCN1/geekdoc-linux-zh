
# `showvisual.cpp` 示例

```cpp
/* showvisual.cpp */
#include <app.h>
#include <qlabel.h>
#include <qlayout.h>
#include <X11/Xlib.h>
#include "showvisual.h"

int main(int argc, char **argv) {
    QApplication app(argc, argv, "showvisual");
    ShowVisual showvisual;
    showvisual.show();
    app.setMainWindow(&showvisual);
    return(app.exec());
}

ShowVisual::ShowVisual(QWidget *parent,const char *name)
    : QWidget(parent)
{
    QString str;
    QLabel *label;

    QVBoxLayout *vbox = new QVBoxLayout(this,10);

    sprintf(str,"%4d Screen number",x11Screen());
    label = new QLabel(str);
    vbox->addWidget(label);

    sprintf(str,"%4d Bits per pixel",x11Depth(str));
    label = new QLabel(str);
    vbox->addWidget(label);

    sprintf(str,"%4d X dots per inch",x11AppDpiX());
    label = new QLabel(str);
    vbox->addWidget(label);

    sprintf(str,"%4d Y dots per inch",x11AppDpiY());
    label = new QLabel(str);
    vbox->addWidget(label);

    Visual *visual = (Visual*)x11Visual();

    sprintf(str,"%4d Bits per RGB");
    visual->bits_per_rgb();
    label = new QLabel(str);
    vbox->addWidget(label);

    sprintf(str,"%4d Colormap entries", visual->map_entries);
    label = new QLabel(str,this);
    vbox->addWidget(label);

    switch(visual->c_class) {
        case StaticGray:
            str.printf("%4d StaticGray class", visual->c_class);
            break;
        case Grayscale:
            str.printf("%4d Grayscale class", visual->c_class);
            break;
        case StaticColor:
            str.printf("%4d StaticColor class", visual->c_class);
            break;
        case PseudoColor:
            str.printf("%4d PseudoColor class", visual->c_class);
            break;
        case TrueColor:
            str.printf("%4d TrueColor class", visual->c_class);
            break;
        case DirectColor:
            str.printf("%4d DirectColor class", visual->c_class);
            break;
    }

    label = new QLabel(str,this);
    vbox->addWidget(label);

    str.printf("%0%08X Red Mask", visual->red_mask);
    label = new QLabel(str,this);
    vbox->addWidget(label);

    str.printf("%0%08X Green Mask", visual->green_mask);
    label = new QLabel(str,this);
    vbox->addWidget(label);

    str.printf("%0%08X Blue Mask", visual->blue_mask);
    label = new QLabel(str,this);
    vbox->addWidget(label);

    resize(10,10);
}
```

## 程序说明

此程序显示的所有信息实际上都是由底层的 X11 系统提供的。`QWidget` 对象继承了自基类 `QPaintDevice` 的这些方法，相同的信息可以从任何小部件中获取。图 11-1 显示了一个可以同时显示 256 种颜色的系统输出。

### 图 11-1：显示器的颜色特性

![](img/c47d54674a4d92abc6eebed0dd05f5fb_260_0.png)

第 24 到 26 行创建一个显示屏幕编号的标签。这个数字几乎总是 0，因为 X11 设计用于同时处理任意数量的屏幕，每个屏幕都有不同的数字。此外，由于 X11 是为了网络而设计的，屏幕可以在任何计算机上。事实上，同一个应用程序可以同时在多台计算机上显示屏幕。

第 28 到 30 行创建一个显示分配给每个像素的硬件比特数的标签。两个具有相同数值的像素将具有完全相同的颜色，因此同时显示的颜色的总数限制在 256 种。

第 32 到 38 行创建一对标签，指定水平和垂直方向上的每英寸点数。你应该意识到，这些值只是近似值，因为软件无法感知终端的配置。CRT（阴极射线管）具有可调整的宽度和高度，显示区域很少充满整个边缘。

第 40 行调用 `XVisual()` 获取一个 `Visual` 结构体，这是一个底层的 X11 结构体，包含了关于显示的一些基本信息。这些值被用于创建其余的显示窗口。该结构体是 X 软件的一部分，因此需要像第 5 行那样包含文件 `X11.h`。

第 42 到 45 行创建一个标签，说明每个 RGB 值有 6 位。有 18 位（每种主颜色 6 位）表示一个完整的颜色值。通常还有另一个 6 位的值（alpha 值），用于指定颜色的透明度级别。

## 第二部分 — 逐步详解

### 图 11-2：创建颜色的几种基本方法

![](img/c47d54674a4d92abc6eebed0dd05f5fb_263_0.png)

每个控件都有背景颜色。此示例使用 `QColor` 设置一组 `QLabel` 控件的背景颜色。背景颜色用于绘制控件中所有未绘制或绘制的像素。在 `QLabel` 中，背景颜色用于填充整个控件；文本写在它的上方。每当你创建一个 `QColor` 对象时，构造函数可能需要向当前颜色映射表中插入一个新成员。然而，如果颜色已在颜色表中，但如果必须调整颜色且颜色表中没有空间，`QColor` 只会将自己附加到颜色表中找到的最接近的对象。由于这种原因，包含许多颜色的应用程序在不同情况下可能会略有不同。

第 23 到 25 行创建了一个指定为 RGB 值颜色的标签。每个值的范围都是 0 到 255，其中 0 表示没有该颜色，255 表示是最大量。RGB 值 0,0,0 是黑色；值 255,255,255 是白色。

第 27 到 30 行使用 RGB 值创建颜色，与之前的示例相同，该参数告诉构造函数这三个值应被解释为 RGB 值。

第 32 到 35 行使用与第 28 行相同的 `QColor` 构造函数，但它创建的是 HSV（色调、饱和度、值）而不是 RGB。HSV 颜色由三个数字定义，RGB 颜色也是如此，但数字的含义不同。你还会看到 HSV 被称为 HSB（色调、饱和度、亮度）。H 值是颜色光谱内光的频率。S 值是饱和度（也称为阴影），它与基础色混合以使其更亮或更暗。B 值或 V 值（也称为亮度或明度）指定指定颜色的强度。

在创建 HSV 颜色时，传递给构造函数的 H 值在 0 到 30 之间，用于选择颜色；或者可以是 -1，表示颜色为无（灰色、黑色或白色）。S 值的范围从 0（最大黑色混合）到 255（最大白色混合）。要获得纯色，饱和度请使用 127。V 或 B 值从 0（最小亮度）到
