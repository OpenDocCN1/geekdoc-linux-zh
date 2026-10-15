
这些方法的目的从方法名上一而易见，但参数需要简短的解释。`QMouseEvent`类具有以下（部分）公共接口：

```cpp
class QMouseEvent : public QEvent { // 鼠标事件
public:
int x(); // widget 中的 x 位置
int y(); // widget 中的 y 位置
int globalX(); // 相对于 X server 的 x 坐标
int globalY(); // 相对于 X server 的 y坐标
int button(); // 按钮索引（从零开始）
int state(); // 鼠标状态标志
// 构造函数，以及保护/私有接口未显示
```

本节的示例显式地使用了鼠标事件。我们将捕获按下和移动事件的鼠标 x-y 位置。在本章中，我们不会直接使用`KeyEvent`、`QEvent`、`QFocusEvent`、`QPushButton`、`QMouseEvent`、`ResizeEvent`、`QCloseEvent`类，但你可以在 Qt 分发版中`src/kernel`子目录下的`qevent.h`文件中查看它们的头文件。涵盖 Qt 使用的所有事件类型超出了这个简短介绍章节的范围，但你可以快速在`qevent.h`中找到类头文件作为参考。

`QSize`类具有以下（部分）公共接口：

```cpp
class QSize {
public:
QSize() { width = -1; }
QSize(int w, int h);
int width() const;
int height() const;
void setWidth(int w);
void setHeight(int h);
// 大部分类定义未显示
// 请参见 Qt 分发版中的 src/kernel/qsize.h 文件
```

`QSize`的接口定义在 Qt 分发版的`src/kernel`目录下的`qsize.h`文件中。`QWidget`类用于控制 widget的状态或查询其状态（来自 Qt 分发版中的`qwidget.h`文件），如下：

```cpp
int x();
int y();
```

# 使用 Qt 进行 GUI 编程

第 31 章

```cpp
QSize size();
int width();
int height();
QSize minimumSize();
QSize maximumSize();
void setMinimumSize(const QSize&);
void setMinimumSize(int min, int min);
void setMinimumSize(const QSize&);
void setMaximumSize(int max, int max);
void setMinimumWidth(int min);
void setMinimumHeight(int min);
void setMaximumWidth(int max);
void setHeight(int max);
```

这些公共方法可以用于：

- 获取容器内 Qt widget 的 x-y 位置。
- 获取宽度和高度。
- 获取 widget 的最小和最大首选尺寸。（也可以指定最小和最大尺寸及形状。）

# 实现 DrawWidget 类

我们将分两个步骤实现示例程序。在本节中，我们将编写`DrawWidget` C++ 类。在下一节中，我们将编写一个使用`DrawWidget`的简短主程序。光光盘中`src/qt/events`目录下的`Draw.h`文件包含了`DrawWidget`的 C++ 类接口。该文件衍生自 Qt 分发版`examples`目录下的`connect.h`文件。类定义需要`QWidget`、`QPainter`和`QApplication`类的定义：

```cpp
#include <qwidget.h>
#include <qpainter.h>
#include <application.h>
```

`QPainter`封装了绘图属性，如画笔和画刷、背景颜色、前景和颜色区域。`QPainter`还提供了原始绘图操作，如绘制点、线和形状。`QPainter`提供了高级绘图操作，如曲线、文本和图像。`QPainter`的 C++ 类接口可以在 Qt 分发版的`src/kernel`目录下的`painter.h`文件中找到。

`QApplication`类封装了数据并提供了 Windows 应用程序的行为。该类跟踪添加到应用程序的顶层 widget。所有的 Windows 事件都由`QApplication`类的`exec`方法处理。

# 用户界面编程

第四部分

我们的示例`DrawWidget`类派自`QWidget`，并重写了三个保护方法`paintEvent`、`mousePressEvent`和`mouseMoveEvent`：

```cpp
class DrawWidget : public QWidget {
public:
    DrawWidget(QWidget *parent=0, const char *name=0);
    ~DrawWidget();
protected:
    void paintEvent(QPaintEvent *);
    void mousePressEvent(QMouseEvent *);
    void mouseMoveEvent(QMouseEvent *);
private:
    QPoint *points;        // 点数组
    QColor *color;         // 颜色
    int count;              // 点的数量
};
```

数组`points`将用于存储鼠标事件的坐标。类变量`color`将用于定义自定义颜色。变量`count`用于计数点。

`draw.cxx`文件包含了`DrawWidget`类的实现。`draw.hxx`包含以下类头：

```cpp
#include "draw.hxx"
```

我们将使用一个 3000 个点的数组记录 widget 内部的鼠标位置。数组在类构造函数中初始化，存储点的计数被设置为零，如下：

```cpp
const int MAXPOINTS = 3000; // 最大点数
DrawWidget::DrawWidget(QWidget *parent, const char *name)
    : setBackgroundColor(white)
    count = 0;
    points = new QPoint[MAXPOINTS];
    color = new QColor(white);
```

```cpp
DrawWidget::~DrawWidget() {
    delete[] points;
    delete color;
}
```

```cpp
void DrawWidget::paintEvent(QPaintEvent *) {
    QPainter painter(this);
    for (int i = 0; i < count; i++) {
        painter.drawPoint(points[i]);
    }
}
```

```cpp
void DrawWidget::mousePressEvent(QMouseEvent *event) {
    if (count < MAXPOINTS) {
        points[count] = event->pos();
        count++;
    }
}
```

```cpp
void DrawWidget::mouseMoveEvent(QMouseEvent *event) {
    // 鼠标移动实现
}
```

# 使用 Qt 进行 GUI 编程

第 31 章

`Makefile`是从标准 Qt 分发中编程教程的`Makefile`示例复制并编辑而来的。这些教程`Makefile`在编译和安装 Qt 发行版时会自动构建。如果因为 X 库或头文件位置不同导致`Makefile`在你的系统上损坏，请将示例`Makefile`的前 20 行与你 Qt 发行版中的任何教程`Makefile`进行对比。

当你安装 Qt 时（无论是从你的 Linux 发行版，还是通过从 www.troll.no 下载最新的 Qt 发行版），环境变量`QTDIR`都会被设置为已安装的库、二进制工具等。在我的系统中，`QTDIR`被设置为值`/usr/local/qt`，它为 C++ 语言和`moc`（元对象编译器）提供了一些示例，其中`moc`位于你的`QTDIR/bin`目录。请注意，`$QTDIR`目录应该在你的搜索路径`PATH`中。为了使用本章的内容，我假设你已经遵循了 Qt 发行版包含的安装说明。我们将在本章稍后介绍`moc`是如何工作的，但在下一节中，我们将展示其用法的一个简单示例。

## 派生 StateWidgetItem 类
