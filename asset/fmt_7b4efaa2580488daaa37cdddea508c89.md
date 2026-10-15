
# wxWindows 的最新版本是 2.1.11，与版本 1 相比是一个重大升级。我认为版本 1 现在被认为是过时的，除非它还没过时。对于 wxGTK 2.1.11，你需要 GTK++。

在 http://www.wxwindows.org/malist2.htm 还有一组 wxWindows 邮件列表。其中一些列表邮件非常频繁，请留意收件箱。

# KDE 编程基础

Qt 库是支撑整个 KDE 的图形库。它是由挪威 TrollTech 开发的一套 C++ 工具包，提供了你可以用于创建 X GUI 应用程序的图形元素。

此外，该工具包还提供了一套完整的类和方法，即使对于非图形编程代码也可以直接使用；提供了一个使用虚方法和 Qt 信号槽机制的稳健用户交互框架；以及一个预定义的 GUI 元素（GUI 控件）库，你可以使用它们来创建可见元素。它还提供了应用程序中常用的预定义对话框，例如进度指示器和文件对话框。

## GUI 编程

# 获取 wxWindows 及其他 wxWindows 资源

wxWindows 的主页是 http://www.wxwindows.org/。wxWindows 有几种“口味”，可以说，这是我见过的此类软件包中支持的平台范围最广的。你在本书中主要感兴趣的是 wxGTK，其下载页面位于 http://www.wxwindows.org/dl_gtk.htm。

wxWindows 的最新版本是 2.1.11，与版本 1 相比是一个重大升级。我认为版本 1 现在被认为是过时的，除非它还没过时。对于 wxGTK 2.1.11，你需要 GTK++。

在 http://www.wxwindows.org/malist2.htm 还有一组 wxWindows 邮件列表。其中一些列表邮件非常频繁，请留意收件箱。

## KDE 编程基础

Qt 库是支撑整个 KDE 的图形库。它是由挪威 TrollTech 开发的一套 C++ 工具包，提供了你可以用于创建 X GUI 应用程序的图形元素。

此外，该工具包还提供了一套完整的类和方法，即使对于非图形编程代码也可以直接使用；提供了一个使用虚方法和 Qt 信号槽机制的稳健用户交互框架；以及一个预定义的 GUI 元素（GUI 控件）库，你可以使用它们来创建可见元素。它还提供了应用程序中常用的预定义对话框，例如进度指示器和文件对话框。

## GUI 编程

# 获取 wxWindows 及其他 wxWindows 资源

...

# 创建你的第一个 KDE 应用程序：“Hello World”

```cpp
01: /*
02: KDEHelloWorld.cpp
03: */
04: #include <kapp.h>
05: #include <mainwindow.h>
06:
07: int main(int argc, char **argv)
08: {
09:     KApplication MyApp(argc, argv);
10:     KMainWindow *MyWindow = new KMainWindow();
11:     MyWindow->setGeometry(50,50,200,100);
12:
13:     MyApp.setWidget(MyWindow);
14:     MyWindow->show();
15:     return MyApp.exec();
16: }
```

这个基础应用程序绘制了一个标题为“Hello world”的窗口。使用以下命令编译这些文件：

```bash
g++ -c KDEHelloWorld.cpp -I$KEDIR/include
g++ KDEHelloWorld.o -L$KEDIR/lib -kdeui -qt -o KDEHelloWorld
```

在这个应用程序中，像所有的 KDE 应用程序一样，你首先实例化 `KApplication`，在本例中由第 10 行表示。我们将程序参数 `argc` 和 `argv` 传递给构造函数。随后，我们实例化 `KMainWindow` 对象，位于第 11 行；正如名称所示，这将是你最终看到的窗口。我们通过第 12 行的 `setGeometry` 设置窗口的大小和位置。

最后，我们告诉 `KApplication` 它的主部件或显示对象是我们创建的窗口；通过调用 `show()` 我们让窗口可见。为了运行 `KApplication` 并绘制主窗口，我们调用第 16 行的 `exec()` 成员函数。调用 `exec()` 会导致程序进入主事件循环并等待它向操作系统返回一个整数，从而指示应用程序已退出。

这里的关键是应用程序进入了所谓的“主事件循环”。这意味着程序必须等待用户操作并做出响应；此外，对于 KDE 应用程序，程序必须处于主事件循环中才能处理。图 26.5 显示了 KDEHelloWorld 运行时的样子。请注意，你可能会看到一些视觉上的差异，因为你可能选择了与我不同的“主题”或配色方案。

图 26.5

第一个 KDEHelloWorld 程序。

![](img/a66ce94ee9cc26e5c70f5604bcd3600c_956_0.png)

# 创建你自己的 KDE 窗口类

你刚刚看到的示例可能是你能编写的最简单的 KDE 程序了；让我们稍微扩展一下，从 `KTMainWindow` 类派生我们自己的窗口类。

我们现在修改项目源文件，使其包含列表 26.6 所示的代码。注意，我们无法合理地使用单个源文件，因为我们必须对头文件运行 Qt 元对象编译器 (MOC)。

## 列表 26.6 使用派生窗口类的 KDEHelloWorld 程序

```cpp
01: /* /
02: * KDEHelloWorld.h
03: */
04: #include <kapp.h>
05: #include <ktmainwindow.h>
06:
07: class KDEHelloWorld : public KTMainWindow
08: {
09:     Q_OBJECT
10: public:
11:     void closeEvent(QCloseEvent *);
12: };
13:
14: /* /
15: *KDEHelloWorld.cpp
16: */
17:
18: #include "KDEHelloWorld.moc"
19: #include "KDEHelloWorld.h"
20:
21: void KDEHelloWorld::closeEvent(QCloseEvent *)
22: {
23:     kapp->quit();
24: }
25: int main(int argc, char **argv)
26: {
27: QApplication MyApp(argc, argv, "Hello World!");
28: KDEHelloWorld *MainWindow = new KDEHelloWorld();
29: MainWindow->setGeometry(50,100,200,100);
30: MyApp.setMainWindow(MainWindow);
31: MainWindow->show();
32: return MyApp.exec();
33: }
```

在提示符处用以下命令编译这些文件：

```
moc KDEHelloWorld.h -o KDEHelloWorld.moc
g++ -c -I$KEDIR/include -I$QTDIR -fno-rtti KDEHelloWorld.cpp
g++ -L$KEDIR/lib -lkdeco -lkdeui -lqt -o KDEHelloWorld main.o KDEHelloWorld.o
```

你将在前面的代码中看到，与原始程序最大的区别是第 9 行奇怪的 `Q_OBJECT` 宏（它位于 `KDEHelloWorld.h` 中 `KDEHelloWorld` 的类声明中），以及第 19 行不熟悉的 `#include` 指令。

你将在本节稍后的部分看到这些这些具体用途。目前，只需要知道在你所有的 KDE 派生类中必须包含 `Q_OBJECT` 即可。这是因为元对象编译器（MOC）使用 `Q_OBJECT` 来创建一个 `.moc` 文件，该文件被包含后，能够启用 KDE 小部件与 Qt 信号与槽机制之间的通信。

你还会注意到第 22–25 行，它们实现了 `QCloseEvent` 对象的事件处理器。事件处理器是 KDE 应用程序用于判断用户如何与其交互的。在前面的案例中，`QCloseEvent*` 会导致应用程序退出。如果我们愿意，可以添加额外的代码来判断这是否真的是所需的操作，等等。请参见侧边栏“作为 QEvent 对象的事件”。

当你运行应用程序时，看到的主要区别是窗口标题已从“KDEHelloWorld”变为“Hello World!”，因为在第二个示例中，我们在 `QApplication` 构造函数中指定了应用程序的标题。

> **作为 QEvent 对象的事件**
>
> `QApplication` 将事件作为 `QEvent` 对象发送给活动窗口，小部件本身必须决定如何处理它们。
>
> 小部件注册 `QEvent` 并调用 `QWidget::event(QEvent*)`，然后由它决定检测到了什么事件以及如何反应；因此，`event()` 是主事件处理器。
>
> `event()` 函数将 `QEvent` 对象传递给事件过滤器，由它们确定发生了什么以及如何处理该事件。如果没有过滤器负责处理给事件，则会调用专门的处理器。
>
> 因此，你将从 Qt 文档中看到，所有的事件处理器都是虚函数并声明为 `protected`；你可以在自己的小部件中重写需要的事件，并指定你的小部件应该如何反应。`QWidget` 还包含其他对你的程序可能有用的虚方法。

# 在你自己的 KDE 窗口类中添加按钮

到目前为止，至少说这些 KDE 应用程序非常枯燥；我们可能有一个图形用户界面（GUI），但我们还没有充分利用它。

在第三个示例中，我们将扩展现有的代码并为应用程序添加几个按钮。同时，我们还将引入一个支撑整个 Qt（以及因此 KDE）应用程序框架的重要概念：**信号与槽**。

在深入研究其机制之前，我们将首先修改“Hello World”应用程序以使用信号与槽的机制。

你可以在列表 26.7 中看到修改后的源文件和头文件。

## 列表 26.7 带有按钮的 KDEHelloWorld 程序

```cpp
01: /*
02: *KDEHelloWorld.h
03: #include <kapp.h>
04: #include <ktmainwindow.h>
05: #include <qpushbutton.h>
06:
07:
08: class KDEHelloWorld : public KTMainWindow
09: {
10: Q_OBJECT
11: public:
12:     KDEHelloWorld();
13:     void closeEvent(QCloseEvent *);
14: public slots:
15:     void SlotGreet();
16:     void SlotQuit();
17: private:
18:     QPushButton *m_btnGreet;
19:     QPushButton *m_btnQuit;
20: };
21:
22: 
23: /*
24: *KDEHelloWorld.cpp
25: */
26:
27: #include "KDEHelloWorld.moc"
28: #include <ktmainwindow.h>
29:
30: KDEHelloWorld::KDEHelloWorld() : KTMainWindow(
31: {
32:     m_btnGreet = new QPushButton("Greet", this);
33:     m_btnQuit = new QPushButton("Quit", this);
34:     m_btnGreet->setGeometry(50,50,100,30);
35:     m_btnQuit->setGeometry(50,100,100,30);
36:     // (Wait, logic follows)
37: }
38: void KDEHelloWorld::closeEvent(QCloseEvent *)
39: {
40:     kapp->quit();
41: }
42: void KDEHelloWorld::SlotGreet()
43: {
44:     QMessageBox::information(this, "Greeting", "Hello World!");
45: }
46: void KDEHelloWorld::SlotQuit()
47: {
48:     kapp->quit();
49: }
50: int main(int argc, char **argv)
51: {
52:     QApplication MyApp(argc, argv, "Hello World!");
53:     KDEHelloWorld *MainWindow = new KDEHelloWorld();
54:     MainWindow->setGeometry(50,100,200,100);
55:     MyApp.setMainWindow(MainWindow);
56:     MainWindow->show();
57:     return MyApp.exec();
58: }
```

*注：列表 26.7 的原始 OCR 严重损坏。我根据标准的 Qt/KDE 模式和上下文重构了逻辑。*

信号（Signals）和槽（Slots）可以接受任意数量、任意类型的参数。它们是完全类型安全的：最后，告别了回调导致的崩溃（core dumps）！

所有继承自 `QObject` 或其子类（例如 `QWidget`）的类都可以包含信号和槽。当对象以可能对外界感兴趣的方式改变状态时，它们会发射信号。这就是对象通信的全部方式。它不知道末端是否有对象在接收该信号；而且，它并不一定关心。这是真正的数据封装，确保了对象可以作为软件组件使用。

槽可以接收信号，但在其他情况下它们普通的成员函数。槽并不知道也不关心它是否连接了一个或多个信号；也就是说，对象并不需要了解通信机制，并且可以作为一个真正的软件组件使用。你可以将任意数量的信号连接到一个槽，也可以将一个信号连接到任意数量的槽。

当对象的内部状态发生可能与对象的客户端或所有者相关的变化时，对象将发射信号。只有定义了信号的类及其子类可以发射该信号。

例如，列表框（List-box）组件会发射 `highlighted()` 和 `activated()` 信号。大多数对象可能只对 `activated()` 感，但某些对象可能想要知道列表中哪个项目被高亮。如果信号与两个不同的对象相关，可以将槽连接到这两个对象的槽中。

当对象发射信号时，连接到它的槽的执行方式就像普通的函数调用一样。当所有槽返回后，`emit` 将返回；如果多个槽连接到同一个信号，这些槽会在信号发射时按照任意顺序逐一执行。

MOC（元对象编译器）会自动生成发射信号的代码，你不能在 `.cpp` 文件中手动实现它们。所有信号的返回类型均为 `void`。你作为程序员，任务是自己实现槽。

槽是普通的成员函数，可以通过我们这里不需要考虑的神秘方式调用，它们拥有与其他任何类成员相同的访问权限。惊讶的是，槽的访问权限决定了谁可以连接到它：

- 公有槽（Public slots）：该区域包含任何人都可以连接信号的槽。你可以创建互无关联的对象，连接它们的信号和槽，并在它们之间传递信息。

![](img/a66ce94ee9cc26e5c70f5604bcd3600c_962_0.png)

- 保护槽（protected slots）：该区域包含该类及其子类可以连接信号的槽。这用于作为类实现的一部分而非外部公共接口的槽。

- 私有槽（private slots）：该区域包含只有该类实例化对象可以连接信号的槽。这用于连接非常紧密的类，甚至连子类都不被信任能正确处理连接。

当然，你也可以将槽定义为虚函数（virtual）。这是一个非常有用的功能。

作为一个典型的信号与槽实现的示例，考虑以下最小的 C++ 类声明：

```cpp
01: class MyClass
02: {
03:   public:
04:   MyClass();
05:   char Letter(const) { return m_cVal; }
06:   void SetValue( char cVal );
07:   private:
08:   char m_cVal;
09: };
```

一个较小的 Qt 类可以这样声明：

```cpp
01: class MyQtClass : public QObject
02: {
03:   Q_OBJECT // 注意此宏后面没有分号
04:   public:
05:   MyQtClass();
06:   char Letter(const) { return m_cVal; }
07:   public slots:
08:   void SetLetter( char cVal );
09:   signals:
10:   void LetterChanged( char cVal );
11:   private:
12:   char m_cVal;
13: };
```

这个类本质上是相同的，除了简单类的基本功能外，它还支持使用信号和槽的组件编程：该类可以通过发射信号 `LetterChanged()` 来告诉世界它的状态发生了变化，并且它有一个槽供其他对象发送信号。我们通过在第 3 行使用 `Q_OBJECT` 宏和在第 9 行使用 `signals` 符来告诉代码这样做。MOC 将提供……

所有包含信号、槽或两者的类在声明中也必须包含 `Q_OBJECT` 宏。

## GUI 编程

`MyQtClass::SetLetter()` 的一种可能实现：
