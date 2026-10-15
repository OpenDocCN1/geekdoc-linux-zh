
a class. 也请记住作用域解析运算符指定右侧的标识符属于左侧的数据类型或类。

静态的 QObject::connect() 函数负责将槽连接到信号。SIGNAL() 和 SLOT() 是两个宏，它们接收要连接的信号和槽的函数签名。我们还需要提供应发送和接收信号的对象的指针。

第 12 行创建了一个 QVBoxLayout。如前所述，控件可以包含其他控件。可以直接设置子控件的边界（位置和大小），但通常使用布局更容易。布局管理控件子控件的边界。QVBoxLayout 将子控件放置在垂直行中。

第 13 行和第 14 行将文本编辑和按钮添加到布局中。

第 17 行在控件上设置布局。

第 19 行显示窗口。

第 21 行启动事件循环。

## Qt EXERCISE 22.4: CONNECTING SIGNALS AND SLOTS

以下 Qt 代码在一个窗口中放置了三个控件，并定义了这些控件的信号元素和槽元素之间的互连。

```
// signalSlot2/main.cpp
#include <QApplication>
#include <QVBoxLayout>
#include <QLabel>
#include <QSpinBox>
#include <QSlider>
int main(int argc, char *argv[])
{
    QApplication a(argc, argv);
    QWidget window;
    QVBoxLayout* mainLayout = new QVBoxLayout(&window);
    QLabel* label = new QLabel("0");
    QSpinBox* spinBox = new QSpinBox();
    QSlider* slider = new QSlider(Qt::Horizontal);
    mainLayout->addWidget(label);
    mainLayout->addWidget(spinBox);
    mainLayout->addWidget(slider);
    QObject::connect(spinBox, SIGNAL(valueChanged(int)), label, SLOT(setNum(int)));
    QObject::connect(spinBox, SIGNAL(valueChanged(int)), slider, SLOT(setValue(int)));
    QObject::connect(slider, SIGNAL(valueChanged(int)),
label, SLOT(setNum(int));
QObject::connect(slider, SIGNAL(valueChanged(int)),
spinBox, SLOT(setValue(int)));
window.show();
return a.exec();
}
```

## SUMMARY

从用户角度来看，UNIX 的可操作性通过部署图形用户界面（GUI）得到了极大改善。一种常见的 GUI 系统建立在名为 X Window System 的网络协议之上。该 GUI 系统可分为集成或非集成。非集成系统通常仅利用窗口管理器的功能。集成系统通常将窗口管理器与其他更高级别的程序耦合在一起，以实现桌面管理和会话管理。KDE4 就是集成系统的示例。

X Window System 是一个网络协议，并包含针对基于 Intel 的 PC 硬件的设备特定驱动程序。X Window System 用于在用户与运行 UNIX 的一个或多个计算机系统之间进行网络化图形交互。用户与计算机系统之间交互对话的主要仲裁者是窗口管理器。FVWM 窗口管理器提供了其他流行窗口系统的所有便利功能，并且还允许您管理来自 UNIX 应用程序的图形输出。用户界面有两个基本部分：应用程序用户界面（AUI），即每个客户端应用程序如何在服务器屏幕显示上以一个或多个窗口呈现自身，以及窗口管理器或管理界面，它控制显示并组织所有客户端窗口。

X Window System 中交互性的基本模型是应用程序客户端与图形服务器之间的事件-请求循环。对于为 X Window System 编写的应用程序，客户端应用程序可以处理输入事件，完成形成对事件响应的必要工作，然后将响应作为图形输出请求输出到服务器。

X Window System，尤其是 FVWM，可以高度定制以满足各种用户的交互需求。在本章中，我们介绍了两种改变非集成窗口系统外观和功能的方法，以及窗口管理器本身。第一种方法涉及通过指定命令行选项来更改在 X Window System 下运行的应用程序的特性。第二种方法涉及修改窗口管理器 FVWM 的预定义示例初始化文件 ~/.fvwm/config，然后调用该初始化文件。

我们介绍了占主导地位的开源集成桌面管理系统 KDE4 的功能。我们展示了如何使用该系统在 UNIX 环境中加快您的工作，特别是在个人生产力和文件管理操作方面。我们特别展示了该系统中可能的定制，以使用户能够更高效地工作。
