
```
mainLayout->addWidget(label3, 1, 0);
mainLayout->addWidget(label4, 1, 1);
mainLayout->addWidget(label5, 2, 0);
mainLayout->addWidget(label6, 2, 1);
```

```
window.show();

return a.exec();
}
```

此程序与之前的示例类似：不是使用 `QVBoxLayout`，而是使用 `QGridLayout` 作为“容器”，用于六个 `QLabel` 对象。`addWidget()` 函数需要三个参数：要分配的控件，它应该所在的网格行和列。网格的第一个单元坐标为 (0,0)，位于左上角。结果见图 1.5。

如果文本显示异常，通常原因是编辑器以 UTF-8 编码保存了源文件。在这种情况下，需要将其转换为 ISO-8859-1 或 ISO-8859-15 格式。在 KDE 编辑器 Kate 中，可以在另存为对话框中找到此选项。

图 1.5：使用 GridLayout 的程序

| 一 | 二 |
|---|---|
| 三 | 四 |
| 五 | 六 |

将在第 5 节中找到关于该主题的更多细节，该节介绍了如何设计复杂的布局，例如通过嵌套，以及手动布局、分割器和 `QStackedLayout` 类。

分割窗口器的行为类似于垂直或水平布局，但在另一个空白区域显示句柄。用户可以向任何方向拉动这些句柄，为对面的控件留出更多空间。当拉动句柄时，向句柄方向拉伸的控件会缩小。

`QStackedLayout` 类另一方面则管理具有多个“面板”的布局，每个面板包含一组控件，但只有一个面板是可见的。可以使用该类创建配置对话框。例如，当用户在配置对话框的左侧面板选择一个类别时，会导致右侧面板显示用于更改所选配置的控件。当用户更改左侧的左侧的 `QStackedLayout` 对象知道它应该在右侧显示不同的“页面”。

## 1.3 信号与槽

到目前讨论的程序只产生输出。但如果我们我们需要处理用户输入，没有对象之间的通信就无法进行管理。许多 GUI 工具包使用回调函数或事件监听器来管理对象之间的通信，但 Qt 使用了**信号/槽的概念**。与回调函数相比，这种机制的优势在于，如果两个通信对象中的其中一个被删除，Qt 会自动断开连接。这避免了崩溃，并使编程变得更。

### 1.3.1 最简单的用：槽响应信号

解释信号和槽如何允许对象通信的最简单方法是使用简单的示例。考虑以下程序，它显示了一个文本为“Quit”（退出）的按钮。如果用户点击此按钮，应用程序将结束。

```cpp
// signal/main.cpp

#include <QApplication>
#include <QPushButton>

int main(int argc, char *argv[])
{
    QApplication a(argc, argv);

    QPushButton button("Quit");
    button.show();

    QObject::connect(&button, SIGNAL(clicked()),
                     &a, SLOT(quit()));

    return a.exec();
}
```

与第25页第1.1节的“Hello, world!”程序相比，只有两个发生了变化。首先，那里使用的 `QLabel` 对象被 `QPushButton` 取替。

> 7 Qt 中也有事件和事件处理函数。信号和事件之间的区别在于，信号可以根据需要连接到许多槽，包括来自不同对象的槽。相比之下，事件处理器处理为其他对象确定的事件。它是一种事件拦截器。第7章提供了事件的更多细节。

#### QPushButton

此类用于显示按钮以及在该按钮上的鼠标点击事件。

第二个区别在于对 `QObject::connect()` 的调用，它是 `QObject` 类的一个静态函数，用于创建一个从一个对象到目标对象中某个槽的连接。前两个参数指定发送信号的对象以及我们想要绑定到接收槽的信号。最后两个参数指定信号的接收者对象以及接收槽。Qt 字符`&`）是必要的，因为该函数期望将发送和接收对象的地址作为参数。此函数用于确定当用户按下按钮时应用程序执行的操作：应用程序终止。

槽是类的普通函数，经过特殊标记以便它们能对信号做出反应。另一方面，信号是由信号“发送”的。来自对象的信号可以连接到单个接收对象的一个或多个槽，也可以多个不同接收对象的槽。如果一个对象发送信号，那么所有连接到该信号的槽都会触发。如果没有匹配的链接，什么都不会发生。

示例中的 `QObject::connect()` 函数调用将 `QPushButton` 对象的`clicked()`信号与 `QApplication` 对象的`quit()`槽连接起来。当用户按下按钮时，按钮发送`clicked()`信号，导致按钮的`clicked()`函数被调用。作为对该信号的响应，调用应用程序的`quit()`函数。调用此槽结束事件循环，从而结束整个应用程序。

在用 `QObject::connect()` 函数链接信号和槽时，必须像所示使用 `SIGNAL()` 和 `SLOT()` 宏。对于它的第二个（信号）和第四个（槽）参数，`connect()` 函数期望接收传递包含描述类型（信号或槽）的前缀且其他符合 Qt 规范的字符串，我们不需要担心这些。使用这两个宏将确保正确生成预期的字符串。

### 1.3.2 携带附加信息的信号及其处理方式

信号与槽之间的链接也可以用于传输控制槽的精确反应的附加信息。例如，图1.6所示的应用程序。该程序由三个控制元素组成：显示数值的标签（label）；可以通过键盘或鼠标更改值（同时也显示该值）的计数器框（spin box）；以及以图形方式显示当前值并通过操作来更改值的滑块（slider）。

## 1.3 信号与槽

![](img/b663c93885d7333a091a433460ee647f_38_0.png)

目标是让三个控件始终显示相同的值。如果用户通过滑块更改值，则计数器框和标签中的值也必须调整。同样的情况也适用于滑块，如果用户在计数器框中调整值。这通过以下代码实现：

图1.6：所有三个元素应该显示相同的可变值。

```cpp
// signalSlot2/main.cpp

#include <QApplication>
#include <QVBoxLayout>
#include <QLabel>
#include <QSpinBox>
#include <QSlider>

int main(int argc, char *argv[])
{
// ... (注意：代码在原始OCR文本中截断)
```

我们将三个控件依次（即从上到下）放入一个垂直布局中。为了这一点，`QSpinBox` 类提供了计数器框元素，而 `QSlider` 相应地负责滑块。

为了确保控件的同步，我们使用了四个 `connect()` 调用（图1.7）：如果计数器框的值改变，则标签和滑块必须更新；如果滑块的状态发生变化，标签和计数器框需要更新。（注：源文本中未提供图1.7）。

当用户按下按钮时，按钮发送`clicked()`信号，导致按钮的`clicked()`函数被调用。作为对该信号的响应，调用应用程序的`quit()`函数。调用此槽结束事件循环，从而结束整个应用程序。

## 基础、工具与第一个代码

Qt 类以 `QObject` 为基类。因此，所有小部件（即在屏幕上显示内容的元素）都派自 `Widget` 类，而 `Widget` 类又派自 `QObject`。布局类也继承自 `QObject`，这样它们的对象也可以形成层次结构，从而从自动内存管理中获益。然而，作为非视觉对象，它们并没有派自 `QWidget`。

其他非图形类也源自 `QObject`，例如用于轻量处理的 `QString`（见第12章）或 `QSocket`（一个通过套接字提供网络通信对象的类）。这些类以 `QObject` 为基类，以便它们可以通过信号和槽进行通信。

## 4.1.2 QString 以及未继承自 QObject 的类

然而，Qt 也有许多类并不继承自 `QObject`，因为它们既不需要信号和槽，也不需要自动内存管理。这些类包含了最重要的类之一 `QString`，它负责处理字符串。`QString` 中的字符串由 Qt 以 Unicode 格式存储和处理，使得世界上几乎所有系统的文本都能被使用；也就是说，不仅是欧洲字符，还包括西尔字母、阿拉伯语、希伯来语、中文等等。由于这个原因，Qt 可以非常高效地用于必须处理不同语言的程序——即 `QString` 提供了操作用户可能看到的文本。`QImage`（用于加载和保存图像）、`QColor`（保存颜色）以及许多其他类都没有继承自 `QObject`；它们都以基于值的方式工作。

图 1.8：使用两个 QString 实例的隐式共享

![](img/b663c93885d7333a091a433460ee647f_41_0.png)

Qt 确保在使用这些类时，两个实例的内容永远不会相同。例如，对于字符串 "value" 和 "Hello, world!"，拥有不同的副本将是浪费的，不如在该对象的所有客户端之间共享一个副本。然而，为了避免不必要的复制，需要特殊的管理。图 1.8 通过以下代码示例展示了字符串 "Hello, world!" 上运行的基于值的对象管理过程：

```cpp
QString str1 = "Hello, world";
QString str2 = str1;
str2.replace("world", "Qt");
```

## 1.4.3 Qt 继承层次结构

图 1.9 显示了 Qt 继承层次结构的一个小片段。注意，`Label` 不仅继承 `QObject` 和 `QWidget` 的所有属性，还继承了 `QFrame` 的属性。这是所有可以有视觉框围绕在周围的小部件的基类。

图 1.9：并非所有的 Qt 类都继承自 QObject。

![](img/b663c93885d7333a091a433460ee647f_42_0.png)

# 1 基础、工具与第一个代码

基类 `QAbstractButton` 也继承自 `QWidget`。它作为所有显示按钮的类（即用户可以通过鼠标点击操作的元素）的基类。除了我们过的 `QPushButton` 类外，它还包括 `QCheckBox` 和 `QRadioButton`。

布局类位于一个独立的分支，该分支不回到 `QWidget`，且 `QLayout` 是其基类。`QGridLayout` 直接继承自此，而 `QVBoxLayout` 和 `QHBoxLayout` 则派生自 `QBoxLayout` 类。

`QFrame`、`QAbstractButton`、`QLayout` 和 `QBoxLayout` 类在极少数情况下被直接使用。它们仅仅在基类中总结了其“子类”的共同属性和函数。另一方面，`QString` 和 `QColor` 类没有基类（自身除外）。如果你想实现自己的小部件，通常会派自 `QWidget` 的类。

## 1.5 Qt Qt

实际上，Qt 4 不仅仅是一个单一的编程库，而是七个库，并辅以若干实用程序。`qmake` 是这些实用程序之一。

## 1.5.1 Qt 库

今天，GUI 工具包的常见用法仅体现了此类系统提供的一小部分。Qt 特别包含了用于应用程序开发各个方面的相当丰富的类。其中许多与图形界面编程有关，但也有用于网络编程、OpenGL 支持、数据库和 XML 开发等的类。贯穿始终的重点是类的平台无关性：除了极少数例外，相同的类在所有支持的操作系统上都是可用的，具有相同的功能和相同的行为。

Qt 4.0 由以下程序库组成：

- `QtCore` 包含不产生任何 GUI 输出的基类。
- `QtGui` 包含基础 GUI 类。
- `QtNetwork` 包含网络类。
- `QtOpenGL` 包含 OpenGL 支持。
- `QtSql` 包含 SQL 数据库类。
- `QtXml` 包含 XML 和 DOM 类（见第 45 页）。
- `QtAssistantClient` 允许你在应用程序中使用 Qt assistant 作为文档浏览器。
- `Qt3Support` 包含确保与 Qt 3 兼容的类。

Qt 4.1 增加了 `QtSvg` 库，它提供了对 SVG 矢量图形格式的支持，以及 `QtTest` 库（即 QtTestLib），它包含一个用于编写单元测试的框架。

最后在 Qt 4.2 中，Trolltech 增加了 `QtDBus` 模块，它提供了来自 Freedesktop.org 的消息系统¹⁰。

你可能需要将你的应用程序链接到几个库，通常包括 `QtCore`。默认情况下，`qmake` 使用 core 和 gui。要创建一个支持网络的 GUI 程序，你需要向该变量添加 network。要创建一个支持 XML 的命令行程序，你必须向该变量添加 xml。使用 Qt 4.0 的所有库：

```pro
QT += network opengl
```

在非图形程序中，`QCoreApplication` 类承担了 GUI 应用程序中的 `QApplication` 角色：它提供了事件循环。如果你需要不同线程之间或通过套接字进行异步通信，这将非常有用。

除了指定项目文件，还有一个对库知识特别感兴趣的话题。除了与库名相同的类头文件外，Qt 还提供了其库的头文件。这些文件包含了所有类的接口定义；因此，在目前为止使用 `QtGui` 类的示例中，我们可以简单写

```cpp
#include <QtGui>
```

然而，这些库头文件非常长，这大大增加了编译过程的时间。如果编译器支持预编译头文件，这不会是一个问题（例如 3.4 以后版本的 GCC）。

## 基础库 QtCore

`QtCore` 是每个 Qt 程序所需的库。除此之外，它还提供了以下内容：

- 基础数据类型，如 `QString` 和 `QByteArray`
- 基础数据结构，如 `QList`、`QVector` 和 `QHash`
- 输入输出类，如 `QIODevice`、`QTextStream` 和 `QFile`
- 可以进行多线程编程的类（包括 `QWaitCondition` 和 `QThread`）
- `QObject` 和 `QCoreApplication` 类（`QApplication` 的基类）

这些类都不依赖 GUI 组件。

## GUI 库 QtGui

Qt 包含了编程图形界面所需的所有类，包括：

- `QWidget` 类以及派生自它的类，如 `QLabel` 和 `QPushButton`
- 布局类（包括 `QVBoxLayout`、`QHBoxLayout` 和 `QGridLayout`）
- 类如 `QMainWindow` 和 `QMenu` 类，如果你想给应用程序添加菜单，就需要这些类
- 用于绘图的类，例如 `QPainter`、`QPen` 和 `QBrush`
- 提供即用对话框的类（包括 `QFileDialog` 和 `QDialog`）
- `QApplication` 类

`QtGui` 需要 `QtCore` 库。

## 网络库 QtNetwork

部分库 `QtNetwork` 提供了编写网络应用程序的类。除了支持通过 `QTcpSocket` 和 `QUdpSocket` 进行简单的套接字通信外，该库还通过 `QHttp` 和 `QFtp` 实现了客户端 HTTP 和 FTP 功能。

与 `QtGui` 不同，`QtNetwork` 需要 `QtCore` 库，但当然，它也可以与 `QtGui` 以及其他库一起使用。

## OpenGL 库 QtOpenGL

OpenGL 库允许在 Qt 程序中使用 OpenGL。它提供了 `QGLWidget` 类——这是一种可以在其内部使用 OpenGL 命令进行绘图的控件。OpenGL 使用 `QtCore` 和 `QtGui` 库。

## 数据库库 QtSql

`QtSql` 类提供了 Qt 程序中访问 SQL 数据库的能力。该库包含了用于与 SQL 数据库建立连接以及查询和修改数据的类。Qt 支持多种 SQL 数据库，包括开源数据库 PostgreSQL、MySQL 和 SQLite。

`QtSql` 需要 `QtCore`，将在第 9 章（第 257 页）进行详细讨论。

## XML 库 QtXml

部分库 `QtXml` 提供了一个简单的、非校验的 XML 解析器。可以通过 SAX2 接口（XML 简单 API）直接对其处理。

`QtXml` 还包含 DOM 标准（文档对象模型）的实现。相应的类允许你解析 XML 文档、操作其树形结构、将修改后的文档再次作为 XML 文档发布，或者使用 DOM 创建新的 XML 文档。

此库只需要 `QtCore` 库，将在第 13 章（第 353 页）进行更深入的讨论。

## 兼容库 Qt3Support

与前身 Qt 3 相比，Qt 4 经过了巨大的开发：某些类包含了与 Qt 3 版本不兼容的更改，另一些类在 Qt 4 中被具有不同名称的新类完全取代。为了简化将 Qt 3 程序迁移到 Qt 4，Trolltech 在 `Qt3Support` 库中包含了相应的 Qt 3 类。然而，你不应该在新程序中使用此库，因为这些类的开发已经停止。由于此本书解释的是如何使用 Qt 4 进行编程，我们将不再使用这些类，也不对其进行进一步讨论。

## 图形库 QtSvg

SVG 矢量图形格式由 W3 联盟发布并基于 XML 规范。从 Qt 4.1 版本开始，`QtSvg` 库支持 SVG 配置文件 SVG Basic 和 SVG Tiny，可以用于显示 SVG 文件和动画，尽管目前还无法创建它们或在 XML 中通过 DOM 树对其进行操作。

## QtAssistantClient 库
