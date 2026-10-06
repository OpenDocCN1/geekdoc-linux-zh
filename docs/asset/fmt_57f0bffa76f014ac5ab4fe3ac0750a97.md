
`QSlider` *z = new QSlider (0, 360, 60, 0, QSlider::Vertical, this );

`z->setGeometry(10, 200, 30, 75);`

`z->setTickMarks(QSlider::Left);`

// 将滑块连接到 GLBox 对象上对应的槽函数：

`connect(x, SIGNAL(valueChanged(int) ), glbox, SLOT(setRotation(int)));`

`connect(y, SIGNAL(valueChanged(int) ), glbox, SLOT(setRotation(int)));`

`connect(z, SIGNAL(valueChanged(int) ), glbox, SLOT(setRotation(int)));`

****** glwindow.cpp ******

****** Start main.cpp ******

```cpp
#include <application.h>
#include <qgl.h>
#include "glwindow.h"

int main(int argc, char *argv) {
    QApplication a(argc, argv);
    GLWindow w;
    a.setWidget(&w);
    w.show();
    return a.exec();
} // End main.cpp ******
```

尽管此列表中的每个函数都附有注释，但可能很难对整个程序有一个概述。不过，这其实非常简单。

`GLBox` 类（定义在第 7 到 29 行）负责活跃的 OpenGL 绘制工作。它绘制了三个静态方法：`paintGL()`（第 60 至 102 行）、`initializeGL()`（第 105 至 121 行）和 `resizeGL()`（第 127 至 152 行）。这些函数的用法与之前描述的相同。`GLBox` 还拥有 `makeObject` 函数（第 155 至 220 行），该函数创建一个 OpenGL 列表（从第 159 行开始）——显示列表是一组绘制操作——并将其返回（第 219 行）。`GLBox` 有三个槽函数：`setRotation()`（第 226 至 233 行）、`yRotation()`（第 236 至 243 行）和 `setZRotation()`（第 246 至 253 行）。这些函数都连接到 `QSlider` 对象的 `valueChanged()` 信号，这是在 `GLWindow` 的构造函数中完成的（具体来说，是在第 300 至 305 行）。

## 学习使用 Qt 的 OpenGL 类

这三个槽函数为 x、y 或 z 轴设置了新的角度值，然后调用 `updateGL()` 来绘制新图像（第 232、242 和 252 行）。

## 工作坊

鼓励你完成以下问题和练习，以帮助你记住在这一小时内学到的关于如何在 Qt 程序中使用 OpenGL 的内容。

## 测验

- 1. 什么是 OpenGL？
- 2. 什么是 MESA？
- 3. 什么是 libqgl？
- 4. 你应该什么时候使用 OpenGL？
- 5. OpenGL 的缺点是什么？
- 6. `QGLWidget` 类是做什么用的？

## 练习

- 1. 在 `www.opengl.org` 找一个良好的 OpenGL 教程。然后阅读并学习它。
- 2. 构建并测试在 `$QTDIR/extensions/opengl/examples` 目录下找到示例。同时研究源代码；它可以为你提供关于如何在 OpenGL 程序中使用 Qt（以及反之）的一些好主意。
- 3. 在列表 19.1 中添加一个函数，使用户能够更改视图距离。添加一个可以控制框在用户面前显示距离的控件。

## 第 20 小时

## 创建 Netscape 插件

在这一小时中，你将学习如何利用 Qt 轻松地编写浏览器插件。插件是用于许多类型程序的软件（在 UNIX 中是共享对象；在 Windows 中是 DLL 文件），可以轻松扩展这些程序的当前功能。一个例子是 Macromedia 流行的 Flash 插件，它让你的 Internet 浏览器能够处理使用 Flash 技术的网站（更多信息请参阅 `www.flash.com`）。如果你安装了这个插件，当浏览器发现该插件可以处理的文件或数据流时，它将简单地调用该插件寻求帮助。但请记住，为一个程序编写的插件与另一个程序的程序的插件是不兼容的。

![](img/ed4f2be9f0799d95b6f041531c9a1f14_338_0.png)

## 316

## 第 20 小时

在为 Netscape Navigator 创建插件时，你通常会使用 Plugin SDK（软件开发包），你可以从 Netscape 网站下载它，并使用 Plugin SDK 提供的 API（应用程序接口）编写插件。然而，Plugin SDK 提供的 API 被认为相当难用。这正是 Qt 发挥用场的地方。Qt 包含了几个你可以用来创建 Netscape 插件的类。通过使用这些类，你不需要处理标准的 Plugin API；因此，编写 Netscape 插件变得简单得多。

这一小时的重点是使用 Qt 插件开发 Netscape 插件。它不涵盖如何使用 Netscape Plugin SDK。

## 为插件开发准备你的系统

在开始使用 Qt 开发 Netscape 插件之前，你首先先做几件事。你需要采取的步骤将在本节中介绍。

## 获取 Netscape Plugin SDK

虽然你没有直接使用 Netscape 提供的 Plugin SDK，但 Qt 中的插件扩展使用了该 SDK 的部分；因此，你需要下载它。

```
# tar xvf unix-sdk-3.0b5.tar.z
```

这将解压存档并将文件放置在名为 `PluginSDK` 的目录中。

![](img/ed4f2be9f0799d95b6f041531c9a1f14_339_0.png)

一如既往，版本号很有可能发生了变化。在编写时，最新版本是 3.0。如果发生了变化，它将同时影响文件名和目录名。

现在，你需要将这些文件几个拷贝到 `$QTDIR/extensions/nsplugin/src` 目录。可以如下如下操作：

```
# cd PluginSDK/common
# cp unix.cpp $QTDIR/extensions/nsplugin/src
```

## 创建 Netscape 插件

```
# cd include
# cp win.cpp $QTDIR/extensions/nsplugin/src
```

完成后，你可以删除 `PluginSDK`——你将不再需要它了。

## 编译 Netscape 插件扩展

默认情况下，Qt 的扩展是不编译的——你需要手动进行。然而，你可以编译你在上一节中拷贝的文件。这并不难。使用 `cd` 将当前目录切换到 `$QTDIR/extensions/nsplugin/` 并在那里运行 `make`，如下所示：

```
## make
```

你将看到以下输出：

```
g++ -c /usr/local/qt/include -I/usr/local/qt/include -fPIC -o qnp.o qnp.cpp
g++ -c /usr/local/qt/include -I/usr/local/qt/include -fPIC -o moc_qnp.cpp qnp.h
g++ -c /usr/local/qt/include -I/usr/local/qt/include -fPIC -o moc_qnp.o moc_qnp.o
ar cs ../../../libqnp.a qnp.o
```

这将创建一个名为 `libqnp.a` 的静态库。将此文件拷贝到 `$QTDIR/lib`，这样你每次编译插件时就不需要需要指定该库所在的目录。

## 了解 Qt 的 Netscape 插件类

你需要了解 Qt 插件类是如何工作的。本节将介绍其中的每一个类，讨论它们如何以及何时被使用。请注意，本文只涵盖了每个类中最关键的成员函数。对于此处未提及的函数，你应该查阅 Qt 参考文档以获取信息。

## QPlugin: 插件的核心

`QPlugin` 是插件的核心。该类的对象永远只有一个。对于你用 Qt 创建的每个插件，你需要创建一个 `QPlugin` 的子类，并实现一个浏览器调用的函数以获取关于插件的各种信息。

![](img/ed4f2be9f0799d95b6f041531c9a1f14_340_0.png)

## 理解 getMimeType() 函数

当浏览器需要知道哪个 MIME 类型或数据流属于自己时，会调用 `QPlugin::getMimeType()`。MIME 类型用于 Internet 浏览器来确定它们正在处理什么类型的数据。浏览器检查其配置，查看是否为该类型定义了处理器（程序或插件）。如果存在处理器，浏览器将使用它进行工作。

一个 MIME 类型由一个主类型和一个子类型组成，用斜杠（/）分隔。例如，MIME 类型 `text/plain` 表示纯文本，MIME 类型 `image/gif` 表示 GIF 图像。

然而，要定义一个新的 MIME 类型，你需要访问 Web 服务器的配置，而你通常并不具备该权限。坦率地说，文件类型也可以通过查看文件名扩展名来确定。例如，文本文件通常以 `.txt` 结尾，GIF 图像以 `.gif` 结尾。

以下是 `QPlugin::getMimeType()` 的简单实现：

```
const char *getMimeType()
{
    return "image/gif";
}
```

## 理解 newStreamCreated() 函数

`QNInstance::newStreamCreated()` 用于浏览器告诉插件已有数据可供其使用。通过此函数，你还可以告诉浏览器你希望以文件还是流的形式获取数据。如果接受数据，`QNInstance::newStreamCreated()` 将返回 TRUE。以下是一个示例实现：

```cpp
bool newStreamCreated( QStream*, StreamMode &mode )
{
    smode = AsFileOnly;
    return TRUE;
}
```

在这个示例中，插件接受数据并告诉浏览器它希望以文件形式获取数据。在这种情况下，由于被告知提供文件格式的数据，稍后将调用 `QInstance::streamAsFile()` 函数。该函数包含了处理文件中数据的代码。

如果你将其设置为选择的其他三个值之一（Normal、Seek 或 AsFile），数据可能会以流的形式接收。这时，浏览器将必须调用 `QInstance::ready()` 来查询（询问）想要从流中接收的最小数据量，并调用 `QInstance::write()`，后者应该负责实际的处理（或调用负责处理的适当函数）。

`QInstance::streamAsFile()`、`QInstance::ready()` 和 `QInstance::write()` 中的代码取决于你处理的数据类型而差异很大。因此，本节将不再涵盖这些函数的任何示例实现。不过，Qt 参考文档包含了一些关于它们的有趣信息。

## QWidget：创建插件的视觉部分

你的 `QWidget` 子类应该包含插件的事件和绘图代码。`QWidget` 是 `QWidget` 的子类，应该被视为与任何其他部件对等。实际上，该类中的代码只是普通的 Qt 编程代码（你不需要这个示例，对吧？）。

## QStream：从浏览器接收数据流

只有当你使用文件流接收数据时，才应该实现 `QStream` 子类。`QStream` 是数据流的抽象，被 `QInstance::ready()` 和 `QInstance::write()` 函数用于流传输数据。然而，该类的实现也很大取决于你正在处理的数据类型。参考文档包含了关于该类及其成员的有用信息。

## 创建你的第一个 Netscape 插件

本节提供了一个非常简单的基于 Qt 的插件示例。你将学习如何编译此示例、如何让 Netscape 识别它，最后以及如何测试它。

## 研究代码

你现在应该准备好编写一个简单的插件了。列表 20.1 显示了一个非常基础的示例。

+ 列表 20.1 一个非常简单的基于 Qt 的 Netscape 插件

```cpp
1: //我们需要包含 qnp.h 来获取
2: //插件定义：
3: #include qnp.h
4: #include <qpainter.h>

6: //这是我们的 QNPWidget 子类。它将
7: //创建实际的插件部件：
8: class MyPluginWidget : public QNPWidget
9: {
10: public:
11:
12: //我们重新实现了 paintEvent( ) 函数
13: //来处理绘图：
14: void paintEvent(QEvent* event)
15: {
16:
17: QPainter p( this );
18: p.setClipRect( event->rect() );
19: int w = width();
20: p.drawText( w/8, 0, w/4, height(), AlignCenter,
    "* 你的第一个基于 Qt 的插件! ");
21: }
22:
23: };

25: //这是我们的 QNPInstance 子类。这个简单的
26: //版本只包含 newWindow() 函数
27: //它返回一个 MyPluginWidget
28: //类对象：
29: class MyPluginInstance : public QNPInstance
30: {
31: public:
32:
33: QNPWidget *newWindow()
34: {
35:     return new MyPluginWidget;
36: }
37:
38: };

40: //MyPlugin 是我们插件的核心。
41: //它的成员被浏览器调用
42: //以获取插件的各种信息
43: //并获取一个 MyPluginInstance
44: //类对象：
45: class MyPlugin : public QNPugin
46: {
47: public:
48:
49: QNPInstance *newInstance()
50: {
51:     return new MyPluginInstance;
52: }
53:
54: const char *getWIMDescription() const
55: {
56:     return "basic/very:bas A very basic plugin";
57:
58: const char *getPluginName() const
59: {
60:     return "A very basic Qt-based Plugin"
61:
62: const char *getPluginDescription() const
63: {
64:     return "A very simple Qt-based plugin that can't do anything useful";
65: }
66:
67: };

71: // 外部函数将为
72: //浏览器提供一个 MyPlugin 对象
73: //类：
74: QPlugin* QPlugin::create()
75: {
76:     return new MyPlugin;
77: }
```
*(注：原文文本中存在大量的 OCR 错误和重复描述，翻译时已根据要求对逻辑进行了清理和还原)*

## 创建 Netscape 插件

为了测试你的插件，你首先需要创建一个 HTML 文档。这里有一个示例：
```html
<HTML>
<HEAD>
<TITLE>A Very Basic Qt-Based Plugin Called With the EMBED Tag</TITLE>
</HEAD>
<BODY BGCOLOR="#ffffff">
<CENTER>
<EMBED TYPE=basic/very WIDTH=300 HEIGHT=100>
</EMBED>
</CENTER>
</body>
</HTML>
```

现在，如果你在 Netscape 中打开此文档，你的插件将绘制出一个 300 像素宽 100 像素高的矩形（由 `<EMBED>` 标签定义），并在其中显示“Your first Qt-based plugin!”的文本。这如图 20.2 所示。

## 20.2
使用 `<EMBED>` 标签嵌入到 HTML 文档中的插件。

![](img/ed4f2be9f0799d95b6f041531c9a1f14_348_0.png)

这个示例并没有什么用；它只是画了一个包含某些文本的矩形。然而，假设你创建了一个用于显示 AVI 电影的插件。你可以轻松地将 AVI 电影嵌入到 HTML 文档中，如下：
```html
<EMBED SRC="movie.avi" WIDTH=320 HEIGHT=200 AUTOSTART=true LOOP=true
