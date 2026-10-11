
# 第 2 章 ◆ 创建与显示窗口

图 2-6：计数器的槽接收按钮的信号。

![](img/c47d54674a4d92abc6eebed0dd05f5fb_44_0.png)

`Count` 小部件包含一个按钮和一个标签。标签用于显示当前的计数器值值：

```cpp
/* clickcount.h */

#ifndef CLICKCOUNT_H

#define CLICKCOUNT_H

#include <qbutton.h>

#include <qlabel.h>

class ClickCount: public QWidget

{

public:

  ClickCount(QWidget *parent=0, const char *name=0);

slots:

  void incrementCounter();

private:

  int counter;

  QLabel *label;

  QPushButton *button;

};

#endif
```

第 10 行的 `Q_OBJECT` 宏必须存在于任何带有槽的类中。（对于广播信号的类，也必须存在，正如你将在第 5 章中看到的那样）。`Q_OBJECT` 宏定义了一些方法。

# 摘要

只需几行代码即可创建一个运行的 Qt 或 KDE 应用程序。创建窗口的代码细节，以及监听用户输入的底层机制，都由 API 内部处理。

- Qt 程序的创建方式是让程序的主函数创建一个 `QApplication` 对象并使用它来控制窗口。KDE 程序以相同的方式形成，但使用的是 `KApplication` 对象。
- 应用程序的主窗口是一个单一组件（widget）。该组件通常包含一组其他组件，用于显示信息并提供用户界面。
- 一个对象可以被编写为广播一个或多个信号（signals）。一个对象也可以包含一个或多个用于接收广播信号的槽（slots）。槽和信号的实现细节通过使用宏和 MOC 编译器实现了自动化处理。

本章描述了如何创建和显示应用程序的主窗口。下一章将涉及显示弹出窗口和对话框。虽然有一些预定义的 KDE 和 Qt 对话框，但你也可以创建自己的。

# 在窗口中布局组件

本章完全关于控制窗口内一组组件的大小和位置。在对进行编程以响应按钮点击或读取用户输入的某些文本之前，必须以某种布局方式呈现按钮和文本输入组件。本章不仅解释了如何将组件放置在你需要的地方，还解释了如何指定其大小以及当窗口调整大时将采取的操作。

组件可以通过坐标值或使用布局（layout）来确定位置和调整大小。坐标值是硬编码的像素位置，用户无法调整。相反，布局对象相对于组件彼此以及相对于容器窗口的尺寸，在最大和最小限制范围内对组件进行定位和调整大小。

## 几何组件放置

你可以通过指定四个值：水平偏移、垂直偏移、宽度和高度来指定每个组件的精确位置和大小。坐标系是父窗口的——即包含这些组件的窗口。以下示例在应用程序窗口上放置推按钮。

## 本章内容

- 使用特定的 x 和 y 坐标值在显示器上定位组件
- 将组件附加到网格坐标系
- 拉伸和收缩组件以适应显示器
- 将组件堆叠到垂直框中进行显示
- 将组件插入水平框中进行显示
- 将一个组件的窗口包含另一个组件的窗口内

# 28 第一部分 入门

```cpp
/* main.cpp */
#include <kapp.h>
```

```cpp
#include "setxy.h"

int main(int argc,char **argv)
{
  KApplication app(argc,argv,"setxy");
  SetXY set;
  setxy.show();
  app.setWidget(&setxy);
  return(app.exec());
}
```

主循环非常简单。头文件在第 3 行被包含。组件在第 8 行创建，并在第 10 行通过 `setMainWidget()` 指定为作为主应用程序窗口显示的的组件。

## SetXY 头文件

```cpp
/* setxy.h */
#ifndef SETXY_H
#define SETXY_H

#include <qpushbutton.h>

class SetXY:public QWidget

public:
 SetXY(QWidget *parent=0,const char *name=0);
 ~SetXY();
private:
 QPushButton *button1;
 QPushButton *button2;
 QPushButton *button3;
};
#endif
```

类 `SetXY` 使用 `QWidget` 作为其基类。它的唯一数据是第 13 到 15 行定义的 `QPushButton` 指针。通常情况下，会有指定为槽的方法来响应按钮，但这是一个简单的放置演示，因此对按钮将没有响应。

由于 `qpushbutton.h` 头文件在 `setxy.h` 的第 5 行包含，它会被 `setxy.cpp` 和 `main.cpp` 自动包含。如果使用了任何其他组件，且该组件也包含了 `qpushbutton.h`，则同一个头文件会被包含两次。这就是为什么使用第 2、3 和 18 行的预处理器指令非常重要，它们可以防止头文件被编译多次。

# 第 3 章 ✦ 在窗口中布局组件

## SetXY

```cpp
/* * setxy.cpp */
#include "setxy.h"

SetXY::SetXY(QWidget *parent, const char *name)
: QWidget(parent,name)
{
  setMinimumSize(90,40);
  setMaximum(190,220);
  resize(190,220);

  button1 = new QPushButton("Upper Left",this);
  button1->setGeometry(0,0,90,40);

  button2 = new QPushButton("Middle Right",this);
  button2->setGeometry(90,70,100,50);

  button3 = new QPushButton("Bottom",this);
  button3->setGeometry(45,70,100,50);
}
{ }
```
