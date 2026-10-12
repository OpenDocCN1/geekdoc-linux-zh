

// 名称小部件组
QLabel *l = new QLabel( "姓名:", this );
// 将标签添加到布局中
top->addWidget( l );
// 一个用于添加/编辑姓名的文本框
theName = new QLineEdit( this );
top->addWidget( theName );
// 增加一点额外的间距
top->addSpacing( 5 );

// 号码小部件组
l = new QLabel( "电话号码:", this );
top->addWidget( l );
theNumber = new QLineEdit( this );
top->addWidget( theNumber );
top->addSpacing( 5 );

// 地址小部件组
l = new QLabel( "地址:", this );
top->addWidget( l );
theAddr = new QLineEdit( this );
top->addWidget( theAddr );
top->addSpacing( 10 );

// 一个“确定”按钮
QPushButton *pb = new QPushButton( "确定", this );
top->addWidget( pb );

// 将按钮的 clicked 信号连接到
// 我们自己的 ok 槽
connect( pb, SIGNAL(clicked()), SLOT(ok()) );
}

// 当用户每次点击“确定”按钮时，该按钮会向此槽发送信号。
// 然后我们可以关闭小部件或退出，或者执行其他操作。
void
ContactUI::ok()
{

// 通过 Qt 全局 QApplication 引用
// 调用 QApplication 的 quit 槽。
qApp->quit();
}

// 设置姓名字段
void
ContactUI::setName( const QString &s )
{
theName->setText( s );
}

void
ContactUI::setNumber( const QString &s )
{
    theNumber->setText( s );
}

// 设置地址字段
void
ContactUI::setAddress( const QString &s )
{
    theAddr->setText( s );
}

// 让我们看看它的作用
int
main( int argc, char **argv )
{
    QApplication app( argc, argv ); // 在 main() 中使用栈是没问题的
    ContactUI *cui = new ContactUI();
    app.setMainWidget( cui );
    cui->show();
    return( app.exec() );
}

#include <cui.moc>

该示例的输出看起来如图 2.2 所示。

![](img/64220583cb3d8a303f33ac97f5433b04_40_0.png)

在 Linux 系统上，通过以下方式编译：

```
moc Cui.cpp -o cui.moc
g++ -I. Cui.cpp -o cui -L$QTDIR -lqt
```

在 Windows 系统上，通过以下方式：

```text
moc Cui.cpp -o cui.moc
cl -nologo -I%QTDIR%\include -I . -c Cui.cpp
link -nologo Cui.obj %QTDIR%\lib\qt.lib user32.lib gdi32.lib
comdlg32.lib ole32.lib uuid.lib m32.lib wsock32.lib
```

本示例引入了四个新对象和四个新概念（但它们彼此相关）。首先出现的是 QString 对象。QString 是 Troll 对字符串概念的封装。它提供了许多功能，包括“安全的”字符串存储、UNICODE 或 ASCII 字符串解释、搜索、分词等。接下来登场的是 QLineEdit 对象。这是 Qt 的标准“文本框”对象，允许用户输入和编辑单行文本。QPushButton 正如你可能猜测的那样——是带有文本或图片标签的按钮。QLayout 有助于管理界面的整体布局。

示例中引入的四个新概念是类定义顶部的 Q_OBJECT 行、类定义中间的“slot”关键字、构造函数末尾的 connect() 调用，以及最后一行包含的一个神秘的、不存在的文件 cui.moc。这四个都与 Qt 的信号/槽机制有关。

Qt 提供了一种相对独特的机制，将一个对象的行为连接到另一个对象。Troll 公司将其称为信号/槽机制，它在 Qt 及其衍生作品中得到广泛应用。该机制将在下一章中详细讨论，所以目前请假装它并不重要，但它以某种方式与示例中的四个奇怪引用相关。有两条简单的规则涵盖了几乎所有 Qt 编码情况：

- 如果你的类将发出或接收信号（通过槽），类定义必须包含顶部的 Q_OBJECT 术语。
- 任何包含 Q_OBJECT 术语的源文件都需要使用元编译器“moc”进行“元编译”，该编译器作为 Qt 工具包的一部分提供。生成的元代码必须通过平台编译器进行编译，并与最终二进制文件链接。

为了支持 Qt 信号/槽机制的使用，编译此示例涉及一个额外步骤。你必须使用 Qt 提供的工具对源文件进行预处理，以生成支持信号和槽的额外代码。这个新步骤在 Linux 或 Windows 上是相同的，看起来像这样：

```text
moc Cui.cpp -o cui.moc
```

moc 程序是在 Qt 构建过程中创建的，应位于 Linux 下的 $QTDIR/bin/moc，或 Windows 系统上的 %QTDIR%\bin\moc.exe。对于任一平台，将此目录添加到 PATH 环境变量是个好主意。

对于那些使用 VC++ 项目输入示例的人，我发现将“自定义生成步骤”添加到源文件中最方便。指定类似以下内容：

```text
moc $(InputDir)\file.cpp -o $(InputDir)\file.moc
```

其中“file”被源文件名替换。一旦你完成源的元编译，你就可以使用平台编译器编译源了。你可以平台编译“moc”的输出，或者像我在这个示例中所做的那样，你可以简单地将其包含在源中。我出于简洁使用了 #include 方法。

你可能注意到在这个示例中我在 QLabel 构造函数中使用了不同数量的参数。Qt 类通常为构造函数提供几个重载，以及任何有意义的 C++ 运算符。你也可以在实例化后设置或测试 Qt 类的大多数值设置。诸如以下语句：

```cpp
QLabel *myLabel = new QLabel(this);
myLabel->setText("Hello World");
QString ltext( myLabel->text());
cout << (const char *)ltext << "\n";
```

将像 Troll 魔法一样起作用。Motif 程序员可能会自问：“权衡在哪里？”对于 Motif 开发人员来说，存在权衡——你牺牲了难以编写的代码，而必须接受卓越的性能。唉。

## 栈与堆

极其重要的是，你要么始终在堆上实例化类（通过“new”关键字）*或者*对你的编译器如何处理在栈上或特定作用域内创建的对象有深入的了解。大多数编码者可能已经注意到我在两个示例中对 QApplication 类使用了这两种方法。这是故意的。两者都是合法的并且运行良好——除非有人创建了一个新的编译器或运行时，使得持久的 main() 函数变得不可靠。

我听到过关于栈实例化总是坏主意的争论。与其他任何事情一样，如果你不知道自己在做什么——或者在这种情况下，你的编译器在做什么——几乎一切都是坏主意。栈实例化可能导致一些难以调试的严重问题，但它也可以带来显著的可支持性和性能改进。如果你怀疑，请使用堆。一个真正讨厌的栈分配错误是一个极佳的学习机会——尽管大多数人没有时间和精力去承受。

## QT 工具包基础

如果你只学习以下基本原则，你就已经超过了成为一名熟练的 Qt 开发人员的半程之路。作为一个读者和 Qt-interest 邮件列表的常客，我经常看到发布的问题，如果这个人熟悉 Qt 基础知识，这些问题本可以避免。当有人回答这些问题时，你几乎可以想象某处有人因自我沮丧而拍打额头。

以下是你在继续之前应该熟悉的基本概念：

- QApplication——Qt 应用程序启动类处理大多数平台特定的初始化程序。
- Qt 使用信号/槽消息传递模型，而不是 X 工具包（Motif 的基础）或 Microsoft Foundation Class Library 使用的回调方法。
- QObject——任何发送信号或提供槽的 Qt 类都继承自 QObject，它是几乎所有 Qt 类的基础。这非常简短且易于消化，但极其重要，因为它是大多数 Qt 类的基础 CLASS。
- QWidget——所有 Qt 小部件都继承自 QWidget，它提供了 Qt 小部件大多数一致的功能和特性。

## QAPPLICATION 类

对于你创建的任何使用可视化组件，或处理*任何*类型输入或事件的 Qt 应用程序，你必须创建一个（*且仅一个*）QApplication 类实例，并且你必须在你创建其他界面组件之前创建此单一实例。如果你尝试创建多个 QApplication 实例，工具包会警告你。是 QApplication 执行所有繁琐的基础的、平台相关的图形和事件通知功能的初始化。默认字体、字体属性、窗口颜色和鼠标行为等全局桌面首选项都被复制到 Qt 应用程序的空间中，因此你的 Qt 应用程序将如用户所期望的那样显示，尽管桌面主题各异。QApplication 提供事件分派循环，允许你的应用程序从底层窗口管理器接收事件。

如果 Qt 没有使用定义的 **QT_NODEBUG** 标志编译，则以下调试选项可用：

- -nograb: Qt 永远不应抓取鼠标或键盘焦点。
- -dgrab: 这是 -nograb 选项的对应项，允许你的 Qt 应用程序抓取鼠标或键盘焦点。在调试器内执行 Qt 应用程序时，有时需要这样做。此选项仅在 X11 平台上有意义。
- -sync: 通常，X11 应用程序将请求排队到 X 服务器——它们被缓冲并按 FIFO 顺序处理。此标志会禁用目标应用程序的正常缓冲。这对于初始调试可能非常有用，但请注意，你的应用程序性能将极其低下。此选项仅在 X11 平台上有意义。

所有 Qt 应用程序都理解以下参数：

