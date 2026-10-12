
```cpp
// 列表 4-18
// 一个保存用 QPainter 命令绘制图像的类

#include <qapplication.h>
#include <qpainter.h>
#include <qpen.h>
#include <qpicture.h>

class qt_window: public QWidget{
public:
    qt_window();
    void drawPicture(void);
protected:
    virtual void paintEvent(QPaintEvent*);
private:
    QPicture Picture;
};

qt_window::qt_window() {
    setBackground(Color(white));
    setGeometry(100,200,470,140);
}

void qt_window::drawPicture(void) {
    QPen Pen(red,10,DashLine);
    QFont Font("Helvetica",18,QFont::DemiBold);
    QPainter WindowPainter;
    WindowPainter.begin(&Picture);
    WindowPainter.setFont(Font);
    WindowPainter.drawText(100,60,
        "the Linux Revolution Is Here");
    WindowPainter.setPen(Pen);
    WindowPainter.drawLine(100,70,360,70);
    WindowPainter.end();
    Picture.save("message.pic");
}

void qt_window::paintEvent(QEvent *event)
{
    QPainter WindowPainter;
    Picture.load("message.pic");
    WindowPainter.begin(this);
    WindowPainter.drawPicture(Picture);
    WindowPainter.end();
}

int main(int argc, char *argv[])
{
    QApplication App(argc,argv);
    qt_window *Window = new qt_window();
    Window->drawPicture(Picture);
    App.setWidget(Window);
    Window->show();
    return App.exec();
}
```

### 列表 4-18：（接续）

图 4-25 显示了列表 4-18 中程序的输出。

![](img/859df50987094e32dd2f5bb576f82bce_161_0.png)

**图 4-25：列表 4-18 中程序的输出。**

`qt_window` 定义了三个方法：构造函数、`drawPicture()` 和 `paintEvent()`。方法 `qt_window.paintEvent()` 是重载的。`qt_window.drawPicture()` 在 `QPicture` 上绘制了消息 "The Linux Revolution Is Here"。`qt_window.paintEvent()` 在 `QPicture` 上绘制了图像。在 `Picture.save()` 方法后，`QPainter` 命令被保存。`message.pic` 文件被保存。`QPainter` 命令被加载。在 `WindowPainter.begin()` 方法后，`QPainter` 命令被调用。`QPainter.drawPicture()` 方法重放了 `QPainter` 命令。

```cpp
#include <kpopmenu.h>
#include <qpixmap.h>

int main(int argc, char *argv[]) {
    KApplication App(argc,argv,"KWindow Program");
    KMainWindow *Kpenguin = new KMainWindow();
    Qpixmap Picture1("Book.xpm");
    Qpixmap Picture2("Globe.xpm");
    Qpixmap Picture3("EscherCube.xpm");
    Qpixmap Picture4("Equation.xpm");
    KPopMenu Menu1 = new KPopMenu;
    Menu1->setTitle("List 1");
    KPopMenu Menu2 = new KPopMenu;
    KMenuBar *MenuBar = new KMenuBar(Kpenguin);
    Menu2->setTitle("List 2");
    Menu1->insertItem(Picture1,"Item 1");
    Menu1->insertItem(Picture2,"Item 2");
    Menu2->insertItem(Picture3,"Item 1");
    Menu2->insertItem(Picture4,"Item 2");
    MenuBar->insertItem("Menu 1",Menu1);
    MenuBar->insertItem("Menu 2",Menu2);
    App.setMainWindow(Kpenguin);
    return App.exec();
}
```

图 4-27 和 4-28 是列表 4-20 中程序的输出结果。

![](img/859df50987094e32dd2f5bb576f82bce_166_0.png)

![](img/859df50987094e32dd2f5bb576f82bce_166_1.png)

# 用于颜色、字体和图标选择及支持的 K 类

表 4-12 列出了提供颜色、字体和图标选择及支持的 K 类。这些部件类可以用于允许用户选择字体、颜色和图标的应用程序。

| K Widgets | 描述 |
|---|---|
| `KButton` | 定义了一个按钮，用于显示或允许用户选择颜色 |
| `KDialog` | 定义了一个对话框，用于从标准系统调色板选择颜色 |
| `KiconLoaderDialog` | 定义了一个对话框，用于交互式选择图标 |
| `KFontDialog` | 定义了一个对话框，用于交互式选择字体 |

## 需要记忆的重要要点

在本章中，你学习了以下内容：

- `Qt` 类库和 `K` 应用框架由许多类组成，这些类定义并支持用于开发图形用户界面的组件。

- 大多数部件用于输入和/或输出。每个部件类都定义了执行初始化、设置和插入值、删除值以及查询部件状态的方法。

- 所有 `Qt` 部件都继承自 `QWidget`，而 `QWidget` 继承自 `QObject` 和 `QPainter`。许多 `K` 部件也继承自 `QWidget`。

- 所有 `QWidget` 类都有一个构造函数，接受指向父部件的指针、对象的名称以及决定部件外观和感受的标志。没有父部件（`Parent=0`）的部件是顶级部件。

- 信号与槽（Signals and slots）是 `Qt` 提供的一种机制，允许对象通信其状态发生了变化。要连接信号与槽，请使用 `Object::connect()` 方法并确保参数匹配。

- 对话框是为了在有限的范围内进行交互而创建的窗口。模态对话框（Modal dialog box）在与对话框的交互完成之前，不允许与其他窗口进行任何其他交互。非模态对话框（Modeless dialog box）允许用户在与对话框的交互完成之前与其他对话框或窗口进行交互。

- `QPainter` 类定义了用于二维图形绘制和绘画的绘图区域。`QPixmap` 定义了一个用于向应用程序添加位图图像的类。

- **企鹅原则 #4：** 每一个作用都有相应的反作用，每一个信号都有相应的槽。

# 第 5 章

# X 窗口简介

窗口是你的应用程序开发中的一个重要概念。窗口是你的应用程序面向用户存在的地方。将在 `Qt` 工具包和 `K` 应用框架的背景下讨论 `X` 窗口。`Qt` 和 `K` 封装了窗口。

### 窗口的构造结构

在窗口系统中，窗口是屏幕上用于输入和/或输出的定义区域或部分。基础窗口具有背景颜色或图案、尺寸和形状。我们看到的大多数窗口都是矩形的，但 `X` 窗口也可以有其他形状。窗口还有一个边框，作为窗口的框架。此外，它还有颜色和尺寸。图 5-1 显示了 `X` 窗口的基本组成部分。在其他系统中，窗口还具有标题栏、滚动条等功能的额外属性。如图所示，基础 `X` 窗口没有尺寸。
