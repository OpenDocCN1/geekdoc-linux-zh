
由于信号和槽仅仅是通信消息，它们可以变得非常健壮。它们可以接受不同类型的不同数量参数，你可以将任意数量的信号连接到同一个槽。信号和槽可以使用任何继承自 `QObject` 类的类，例如 `QWidget`。任何对象都可以同时包含发送消息的信号和接收消息的槽。

当部件上发生事件时，它会发射一个信号。这就是它所做的全部。它不会建立到另一个对象的连接。为了能够从信号接收消息，对象必须设置一个槽。槽只是在对象接收到信号时执行的成员函数。从概念上讲，槽用于获取有关其他对象变化的信息。槽并不知道实际上是否有任何信号连接到它，而信号也不知道是否有任何槽可以接收它。

你使用 `connect` 函数在一个对象中的信号和另一个对象中的槽之间建立连接。你可以将任意数量的信号连接到单个槽，并且每个对象都可以有发送消息的信号和接收消息的槽。`connect` 函数将在两个对象之间建立连接，将一个对象的信号连接到另一个对象的槽上。

在下面的示例中，`mybutton` 对象的 `clicked` 信号连接到了 `myapp` 对象的 `quit` 槽：

```
QObject::connect(&mybutton, SIGNAL(clicked()), &myapp, SLOT(quit()));
```

当对象上发生事件时，`emit` 操作使用信号函数发送消息。当对象发射信号时，任何连接到它的槽都会立即执行。槽仅仅是类中的成员函数，区别在于它们可以连接到信号。它们也可以像普通函数一样调用。你可以将槽设置为保护、私有或公共，从而控制哪些对象可以拥有它们。

```
signals:
  void mySignal();
private slots:
  void myslot1();
  void myslot2();
```

# 窗口

你使用 `QMainWindow` 类来创建一个主窗口。下面的示例创建一个新窗口：

```
QMainWindow *mywin = new QMainWindow;
```

窗口包含多个功能。通过 `setCaption`，你可以设置窗口标题：

```
mywin->setCaption("Document");
```

为了在关闭窗口时关闭应用程序，你可以将窗口关闭信号连接到 `quit` 槽：

```
myapp.connect(&mywin, SIGNAL(windowClosed()), SLOT(quit()));
```

下面的程序显示窗口：

# 父子对象

你通过在层级结构中放置对象来构建 Qt 界面，并将较小对象指定为主要对象的依赖。例如，窗口是一个主要对象，它将包含菜单、工具栏和滚动条等较小对象。主要对象是父对象，而较小对象是子对象。当你创建一个主要部件（如窗口）时，你还可以创建附加到它的较小部件工具栏。这是通过将较小部件（如工具栏）设置为主要部件的子来实现。子部件也可以是自身子部件的父对象。在构建界面时，你将部件放在父部件及其子层级结构中。

要创建一个复杂的部件（例如带有依赖对象的窗口），你首先定义父部件。然后，当你定义父对象的部件时，将父对象的地址作为参数放在部件的定义中。

下面的示例定义了一个名为 `quit` 的按钮部件，并将其设置为窗口部件的子。窗口现在包含了该按钮。注意使用 `&` 运算符来获取父对象的地址：

```
QPushButton mybutton( "Quit", &mywin );
```

当你显示父部件时，所有的子部件都会自动显示。在下面的示例中，窗口部件的 `show` 成员函数也会“显示” `mybutton` 按钮：

```
myapp.setMainWidget(&mywin);
mywin.show();
```

下面的程序显示一个作为窗口子对象的按钮。图 10-4 显示了该程序显示的窗口以及 `Click Me` 按钮。

```cpp
#include <application.h>
#include <mainwindow.h>
int main(int argc, char **argv) {
    QApplication myapp(argc, argv);
    QMainWindow mywin;
    mywin.setCaption("Document");
    myapp.connect(&mywin, SIGNAL(windowClosed()), SLOT(quit()));
    myapp.setMainWidget(&mywin);
    mywin.show();
    return myapp.exec();
}
```

# 380 Linux 编程：入门指南

![](img/3cfc28f62e3fe98d5a49b453e25d689c_403_0.png)

**图 10-4** Qt application.h 窗口和按钮

```cpp
#include <application.h>
#include <mainwindow.h>
#include <qbutton.h>
#include <qfont.h>

int main(int argc, char **argv) {
    QApplication myapp(argc, argv);
    QMainWindow *mywin = new QMainWindow;
    QPushButton *mybutton("Click Me", mywin);

    mywin->setWindowTitle("My Document");
    mywin->connect(&myapp, SIGNAL(lastClosed()), &myapp, SLOT(quit()));
    mywin->setCentralWidget(mywin);
    mybutton->setFont(QFont("Times", 14, QFont::Bold));

    mywin->show();
    return myapp.exec();
}
```

## 布局部件 (Layout Widgets)

通过布局部件，你可以轻松地在父部件（如窗口）上定位子部件（如按钮或文本）。除了定位之外，布局部件还提供了部件显示的默认尺寸、调整大小和更新功能。有若干种易于使用的部件可用。`QHBoxLayout` 在水平行中排列部件，`QVBoxLayout` 在垂直列中按列对排列部件，而 `QGrid` 将它们排列在表格中。如需进行更详细的控制，你可以使用 `QGridLayout` 和 `QVBoxLayout`。

![](img/3cfc28f62e3fe98d5a49b453e25d689c_403_1.png)

## 1 分钟训练

- 你能仅使用 Qt 工具包创建一个用户界面吗？

- Qt 部件在程序中是以什么种的关系组织的？

- 是

- 分层级父子关系

## 创建你自己的部件

创建你自己的部件只是定义一个符合 Qt 标准的类，然后创建该类的对象的简单过程。此类类必须派生自 Qt 基类，例如 `QWidget`。你通过为你的新类指定 Qt 基类来指定这种派生。在接下来的示例中，用户创建了一个 `MyWidget` 类，它派生自 `QWidget` 类。`MyWidget` 将继承 `QWidget` 类的成员函数和变量。

```cpp
class MyWidget : public QWidget
{
};
```

你可以为你的类声明任何需要的公有和私有成员，包括函数和变量。成员函数的定义通常放在类定义之后。

大多数类中常见的常见的成员函数是构造函数。该函数的名称与类相同，并且每当定义该类的对象时，它就会自动调用。你可以将其认为一种初始化函数，负责处理你在该类的新对象上执行的任何初始设置任务。在接下来的示例中，`MyWidget` 类中声明了一个构造函数。

```cpp
class MyWidget : public QWidget
{
public:
    MyWidget(QWidget *parent=0, const char *name=0);
};
```

在你自己的 Qt 部件的构造函数中，你需要包含一个参数，作为你想作为父部件的部件的地址。默认值是 `NULL`，`0`。如果父部件为 `NULL`，它将自动成为顶层部件，而不是另一个部件的子部件。第二个参数是给正在创建的类的特定部件的名字。与其编写代码来处理父部件和名称，你只需将它们传递给你的类继承的 `QWidget` 构造函数。要做到这一点，你将带有参数的 `QWidget` 构造函数放在类的构造函数中，附加在参数之后。

```cpp
MyWidget::MyWidget(QWidget *parent, const char *name )
    : QWidget(parent, name)
```

在构造函数中，你会放置组成你部件的子对象的定义。例如，如果你正在创建一个窗口部件，你会为它编写一个构造函数，在其中定义菜单、工具栏或状态栏等组件。你可以为这些部件设置功能，如尺寸和颜色，并根据需要为它们设置任何信号和槽连接。

以下示例是 `mywidget` 的构造函数定义：
