

文件扩展名为 .cpp——例如，exercise1.cpp，其中包含 Qt 客户端应用程序程序代码。

步骤 1：在 shell 提示符下，输入 qmake-qt4 -project。

步骤 2：在 shell 提示符下，输入 qmake-qt4。

步骤 3：在 shell 提示符下，输入 make。

步骤 4：在目录中你现在将拥有五个文件：exercise1.cpp、Makefile、exercise1.o、qtprogs1.pro 和 qtprogs1。

步骤 5：在 shell 提示符下，输入 ./qtprogs1。

步骤 6：你输入到 exercise1.cpp 中的 Qt 程序中的图形现在显示在屏幕上。使用关闭窗口按钮关闭此 Qt 窗口。

## 22.4.5.2 Qt 示例

下面是最简单的 Qt 客户端应用程序程序你可以输入。注意它比前面各节中所示的 XCB 或 Xlib 代码短得多。按照第 22.4.5.1 节中的说明步骤创建程序并执行它。

## Qt 练习 22.1：最简单的 Qt 程序

```
// helloWorld/main.cpp
#include <QApplication>
#include <QLabel>
int main(int argc, char *argv[])
{
    QApplication a(argc, argv);
    QLabel label("Hello World");
    label.show();
    return a.exec();
}
```

## Qt 练习 22.2：带 GUI 的简单 Qt 程序

```
4       int main(int argv, char **args)
5       {
6           QApplication app(argv, args);
7
8       QTextEdit textEdit;
9       textEdit.show();
10
11      return app.exec();
12      }
```

解释和描述的对话框：

第 1 行和第 2 行包含 QApplication 和 QTextEdit 的头文件，它们是 Qt 使用的两个类。Qt 是一种面向对象的编程语言，使用 C++ 类和对象描述及功能。所有 Qt 类都有以其命名的头文件。

第 4 行声明变量并打开程序。

第 6 行创建一个 QApplication 对象。此对象管理应用程序范围的资源，并且是运行任何具有 GUI 的 Qt 程序所必需的。它需要 argv 和 args，因为 Qt 接受此对象的几个命令行参数。

第 8 行创建一个 QTextEdit 对象。文本编辑是 GUI 中的视觉元素。在 Qt 中，我们称此类元素为小部件，取自窗口小工具的简称。其他 Qt 小部件的示例有滚动条、标签、旋转框、滑块和单选按钮。小部件也可以是其他小部件的容器、对话框区域或主应用程序窗口。

第 9 行在自己的窗口框架中将文本编辑显示在屏幕上。由于小部件也充当容器（例如 QMainWindow，它具有工具栏、菜单、状态栏和一些其他小部件），因此可以单独显示一个小部件在其自己的窗口中。小部件默认不可见；函数 show() 使小部件可见。

第 11 行使 QApplication 对象进入其事件循环，类似于 XCB 和 Xlib 客户端应用程序程序。当 Qt 客户端应用程序运行时，会生成事件并发送到应用程序的小部件。事件的示例，如 XCB 和 Xlib 中所见，是鼠标按钮按下、鼠标光标移动以及键盘上按下的键。当你在文本编辑小部件中输入文本时，它会接收按键事件并通过绘制所输入的文本来响应。

## Qt 练习 22.3：添加退出按钮

在实际应用程序中，你通常会创建不止一个小部件，以允许客户端应用程序数据生成代码与 Qt 代码之间丰富多样的对话。我们现在将展示一个简单的示例，即在 Qt Exercise 22.2 中创建的文本编辑窗口下方放置一个 QPushButton。按钮将在被按下时（即用鼠标点击）退出 QTextEdit 应用程序。同样，忽略所示的行号，因为它们仅用于引用代码后对话框中的代码。
以下是代码。

```
1   #include <QtGui>
2
3   int main(int argv, char **args)
4   {
5       QApplication app(argv, args);
6
7       QTextEdit *textEdit = new QTextEdit;
8       QPushButton *quitButton = new QPushButton("&Quit");
9
10      QObject::connect(quitButton, SIGNAL(clicked()), qApp,
11                      SLOT(quit()));
12
13      QVBoxLayout *layout = new QVBoxLayout;
14      layout->addWidget(textEdit);
15      layout->addWidget(quitButton);
16
17      QWidget window;
18      window.setLayout(layout);
19
20      window.show();
21
22      return app.exec();
23  }
```

解释和描述的对话框：

第 1 行包含 QtGui，其中包含 Qt 的所有 GUI 类。

第 7 行和第 8 行创建两个指针对象，用于引用下面的对象类。

下一行说明了最重要的 Qt 调用之一。

第 10 行使用 Qt 的信号和槽机制使应用程序在按下 Quit 按钮时退出。槽是在运行时使用其名称（作为字面字符串）调用的函数。信号是一个函数，当被调用时会调用与其注册的槽；我们称之为将槽连接到信号并发出信号。因此，quit() 是 QApplication 的槽，用于退出应用程序；clicked() 是 QPushButton 在被按下时发出的信号。

作为 C++ 编程的提醒，:: 称为（二元）作用域解析运算符。通过使用作用域解析运算符，你可以在

