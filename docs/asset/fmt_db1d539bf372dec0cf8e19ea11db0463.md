
在这个示例中，进度条的槽函数 `set()` 被连接到了滑块的 `valueChanged()` 信号。通过这种方式，你可以拖动滑块来控制进度条的进度。注意，这并不是一个真实的示例。但是，如果你在实际应用程序中实现此功能，原理是相同的。你只需要在达到某个点时带参数调用 `setProgress()` 函数即可。

> `ProgressBar` 构造函数的第一个参数表示进度条在达到 100% 之前等待的步数。例如，如果你想复制五个文件，并希望每复制一个文件进度条走一步，那么这个值应该是 5。

该程序在图 8.5 和 8.6 中演示。在图 8.5 中，滑块尚未被拖动，因此进度条没有达到任何步骤。在图 8.6 中，滑块向右移动了一部分，因此进度条也发生了变化。

## 图 8.5

这是进度条程序最初出现在屏幕上的样子。

## 图 8.6

这是你将滑块向左移动时发生的情况。此时，给 `setProgress()` 函数的最后一个值是 73。

## 测验

1. `QLineEdit` 和 `QMultiLineEdit` 之间有什么区别？

2. 你应该使用哪个类来向用户显示文本文件？

3. 如果只看成员函数，`QLineEdit` 和 `QMultiLineEdit` 之间最本质的区别是什么？

4. 如果不使用 `insertItem()` 函数向列表视图插入项，应该使用哪种方法？

5. 在列表视图中双击项时，会发射哪个信号？

6. 在列表视图中按下 Return（回车）或 Enter（回车）键时，会发射哪个信号？

7. 什么是进度条？

8. 你应该在应用程序的什么时候实现进度条？

## 练习题

1. 搜索 Qt 参考文档，找到一个 `QMultiLineEdit` 成员函数，该函数可以使 `QMultiLineEdit` 对象设为只读状态。该函数的名称是什么？你该如何调用它来将 `QMultiLineEdit` 对象设为只读？

2. 创建带有列表视图（list view）的程序。列表视图应该从左到右包含三行：国家、首都和人口。然后，为每个大洲创建一个顶级项目，并创建子项目来描述每个大洲的几个国家，以及关于首都和人口的信息。

3. 你可能想使用进度条，但发现实现起来很困难。也许你觉得不清楚何时调用 `setProgress()` 函数。一种解决方案（尽管可能不是最佳方案）是测量任务所需的时间，然后创建一个 `for` 循环（或类似结构），并此计算出一个你认为适合任务的时间。例如，假设你的程序将执行一个大约需要 30 秒的任务；尝试编写一个在适当时机调用 `setProgress()` 函数的循环。

# 第 9 小节

## 创建简单的 GUI 图形

当你第一次编写你崭新且闪丽的 GUI 程序时，你可能没有意识到该程序实际上是由大量的底层图形代码组成的。幸运的是，这些代码是由 GUI 库（在本例中为 Qt）生成的；因此，你永远不需要担心它们。

你可能会好奇什么是底层图形代码。这些代码是 Qt 使用你系统中最简单的函数（仅用于绘制线条、矩形等的函数）在屏幕上绘制你的程序的代码。

正如前面提到的，Qt 处理底层代码，这些代码创建了预定义的 Qt 控件（widgets）。然而，有时你可能需要创建 Qt 无法为你创建的图形对象。在这种情况下，你需要某种底层图形生成器，可以使用它可以创建自定义图形。Qt 提供了 `QPainter` 类来实现此目的。

在本节中，你将学习如何开始使用 `QPainter`。你还将学习如何在程序中实现打印功能。

## 使用 QPainter 类

如所述，`QPainter` 是用 Qt 创建自定义图形的类。它非常直观，且不易使用。你将通过学习如何创建一个 `QPainter` 对象并绘制一个简单的矩形来开始 QPainter 章节。

## 从 QPainter 开始

为了使用 `QPainter` 创建自定义图形，你需要采取一些预防措施以确保你不会干扰 Qt 处理的绘图。你需要将将绘图代码放置在一个名为 `paintEvent()` 的特殊函数中，并通过调用 `QPainter::begin()` 和 `QPainter::end()` 函数来开始和停止绘制。列表 9.1 提供了一个简单的示例。

### 9.1 绘制一个简单的矩形

```
1: #include <application.h>
2: #include <widget.h>
3: #include <painter.h>
4:
5: class MainWindow : public QWidget
6: {
7: public:
8:
   MainWindow();
9: private:
10:  void paintEvent(QEvent *);
11:  QPainter *paint;
12: };
13:
14: //这里是我们 paintEvent() 的实现：
15: void MainWindow::paintEvent(QEvent *)
16: {
17:   paint = new QPainter();
18:   // 开始绘制：
19:   paint->begin(this);
20:   // 绘制矩形：
21:   paint->drawRect(20, 20, 160, 160);
22:   // 结束绘制：
23:   paint->end();
24: }
25:
26: MainWindow::MainWindow()
27: {
   setGeometry(100, 100, 200, 200);
29: }
30:
31: void main(int argc, char **argv)
```

```
32: {
33:   QApplication a(argc, argv);
34:   MyMainWindow w;
35:   a.setMainWindow(&w);
36:   w.show();
37:   return a.exec();
38: }
```

`QPainter` 对象在第 17 行被创建。然后，在第 19 行通过调用 `QPainter::begin()` 开始绘制。在第 21 行，绘制了矩形。这是通过 `QPainter::drawRect()` 函数完成的。该函数接受参数。前两个参数定义了矩形左上角的位置（相对于窗口），最后两个定义了宽度和高度。最后，在第 23 行通过调用 `QPainter::end()` 结束绘制。该程序将创建一个 200x200 的窗口，其中包含一个 160x160 的黑色矩形（见图 9.1）。

## 图 9.1

一个包含矩形的程序。

如你所见，列表 9.1 的结果是一个简单的矩形。这个示例一点也不花哨（注：原文为 fancy, 译为花丽），但它向你引入了 `QPainter` 类，这就是本节的意义。

## 设置绘图样式

在开始实际绘图过程之前，你需要选择你希望 `QPainter` 如何绘制线条、矩形等。这是通过几个 `QPainter` 成员函数实现的。

## 选择画笔

通过带上适当参数调用 `QPainter::setPen` 函数，你可以选择想要使用的画笔样式。你将通过更改列表 9.1 中的程序，使其使用一种 4 像素宽、绘制虚线的蓝色画笔来尝试一下。只需在 `begin()`（列表 9.1 的第 19 行）和 `end()`（列表 9.1 的第 23 行）之间添加以下代码行：

```
painter->setPen(QPen(blue, 4, QPen::DashLine));
```

结果如图 9.2 所示。

## 图 9.2

使用 `QPainter::setPen()` 函数更改画笔类型。

如你所见，你只需要一行代码就能剧地改变绘图样式。

## 选择填充样式

你可以选择用图案或纯色填充你的矩形。这是通过“画刷”（brush）实现的。例如，如果你想用纯色填充列表 9.1 中的矩形，在调用 `begin()`（列表 9.1 的第 19 行）和 `end()`（列表 9.1 的第 23 行）之间添加以下代码行。

```
paint->setBrush(QBrush(red, SolidPattern));
```

该函数调用的结果如图 9.3 所示。

# 图 9.3

将填充样式设置为纯色。

然而，通过更改 `SolidPattern`，可以用其他方式填充矩形。例如，如果你将其改为 `Dense6Pattern`，填充样式将从 100% (SolidPattern) 变为 12% (Dense6Pattern)。图 9.4 显示了此示例。

## 图 9.4

将填充样式从 100% 更改为 12%。

## 创建简单图形

不同填充样的完整描述可以在表 9.1 中找到。

**表 9.1** 填充样式

| 填充样式 | 描述 |

| :--- | :--- |

| SolidPattern | 纯色填充（见图 9.3）。 |

| Dense1Pattern | 94% 填充样式。 |

| Dense2Pattern | 88% 填充样式。 |

| Dense3Pattern | 63% 填充样式。 |

| Dense4Pattern | 50% 填充样式。 |

| Dense5Pattern | 37% 填充样式。 |

| Dense6Pattern | 12% 填充样式（见图 9.4）。 |

| Dense7Pattern | 6% 填充样式。 |

| HorPattern | 用水平线填充图形。 |

| VerPattern | 用垂直线填充图形。 |

| CrossPattern | 用交叉线填充图形（网格图案）。 |

| BDiagPattern | 一种斜线样式，指向左上角。 |

| FDiagPattern | 交叉的斜线。 |

| CustomPattern | 当使用位图（pixmap）时应使用此填充样式 |

## 更改字体

你可以用 `QPainter` 绘制文本。当你这样做时，你可能想更改字体。这很简单——只需调用 `setFont()` 函数。列表 9.2 显示了一个处理文本的示例程序。

# **列表 9.2** 使用自定义字体绘制文本

```
1: #include <application.h>
2: #include <widget.h>
3: #include <painter.h>
4: #include <qfont.h>
5: 
6: class MyMainWindow : public QWidget
7: {
8: public:
9:     MyMainWindow();
10: private:
11:     void paintEvent(QPaintEvent* event );
```

# 列表 9.2 续

```cpp
12: QPainter *paint;
13: };
14:
15: void MyMainWindow::paintEvent(QEvent *)
16: {
17:     paint = new QPainter;
18:     paint->begin(this);
19:     //设置字体、大小和样式
20:     paint->setFont(QFont("Arial", 16, QFont::Bold));
21:     //绘制文本:
22:     paint->drawText(20, 20, 260, 60, AlignCenter, "Font: Arial, Size: 16, Style: Bold");
23:     
24: }
25: }
26:
27: MainWindow::MainWindow()
28: {
29:     setGeometry(100, 100, 300, 100);
30: }
31:
32: void main(int argc, char **argv)
33: {
34:     QApplication a(argc, argv);
35:     MainWindow w;
36:     a.setWidget(&w);
37:     w.show();
38:     a.exec();
39: }
```

在这里，你看到了第 15 到 25 行中 `paintEvent()` 的定义。它通过创建一个 `QPainter` 对象开始（第 17 行）。然后，绘制工作从第 18 行开始。通过调用 `QPainter::setFont()` 函数设置字体和大小。在第 22 和第 23 行，通过 `QPainter::drawText()` 函数绘制文本。该函数接受六个参数。前两个参数定义绘制文本的矩形的左上角。后续两个参数代表矩形的宽度和高度。通过第五个参数，你可以设置文本的对齐方式。最后一个参数（理所当然）是你想要绘制的文本。该程序创建了一个窗口，并在窗口中心绘制了以下文本：

Font: Arial, Size: 16, Style: Bold

图 9.5 显示了程序的运行情况。

## 创建简单图形

图 9.5

使用 Painter 绘制的文本。

![](img/ed4f2be9f0799d95b6f041531c9a1f14_170_0.png)

你也可以通过标签（label）轻松实现这一点。然而，本节是关于图形的，你还需要学习 `QPainter` 提供的文本函数。

![](img/ed4f2be9f0799d95b6f041531c9a1f14_170_1.png)

![](img/ed4f2be9f0799d95b6f041531c9a1f14_170_2.png)

在使用 `QPainter` 时，你拥有与 `QLabel` 相同的对齐选项。

![](img/ed4f2be9f0799d95b6f041531c9a1f14_170_3.png)

# 了解 QPainter 绘制函数

`QPainter` 提供了更多绘制文本和矩形的函数。在本节中，将涵盖其他一些有趣的绘制函数（尽管不是全部）。请查看 Qt 参考文档中的 `QPainter` 章节以获取 `QPainter` 成员函数的完整介绍。

![](img/ed4f2be9f0799d95b6f041531c9a1f14_170_4.png)

> 请记住，后续章节中的代码示例始终会被插入在 `paintEvent()` 函数中 `begin()` 和 `end()` 调用之间。

## 绘制圆和椭圆

要使用 `QPainter` 绘制圆和椭圆，你应该使用 `drawEllipse()` 函数。它接受四个整数。前两个参数代表圆/椭圆与窗口左侧和上侧之间的像素数。第三和第四参数代表圆/椭圆的宽度和高度。看下面的示例：

```cpp
paint->setPen(QPainter::blue, 4, QPainter::SolidLine );
paint->drawEllipse( 20, 20, 210, 160 );
```

这段代码的结果如图 9.6 所示。

## 图 9.6

用实蓝色线绘制的椭圆。

![](img/ed4f2be9f0799d95b6f041531c9a1f14_171_0.png)

# 绘制圆角矩形

要绘制带圆角的矩形，你使用 `QPainter::drawRoundRect` 函数。参考下面的代码段和图 9.7：

```cpp
paint->setPen( QPen(red, 4, QPen::SolidLine ));
paint->drawRoundRect( 20, 20, 210, 160, 50, 50 );
```

最后两个参数决定了角的圆润程度。该值可以在 0 到 99 之间（99 代表最大圆度）。

## 图 9.7

一个带圆角的矩形。

![](img/ed4f2be9f0799d95b6f041531c9a1f14_171_1.png)

## 绘制圆扇形

要绘制圆的一部分，你应该使用 `QPainter::drawPie()` 函数。这是一个示例：

```cpp
paint->setPen( QPen(green, 4, QPen::SolidLine ));
paint->drawPie( 20, 20, 210, 160, 0, 500 );
```

前四个参数定义圆（类似于 `drawEllipse()`）。最后两个参数定义圆的样式。0 是起始角度（实际上角度的分分之一），500（也是角度的分分之一）是扇形的长度。如果你不熟悉三角函数，可能会发现这很难理解。测试几个值后，你就能理解它的原理了。图 9.8 显示了这个程序。

## 创建简单图形

图 9.8

绿色圆扇形。

![](img/ed4f2be9f0799d95b6f041531c9a1f14_172_0.png)

> 最后两个参数都不代表完整的角度；而是代表角度的分分之一。因此，在这种情况下，360 代表一个完整的圆。

![](img/ed4f2be9f0799d95b6f041531c9a1f14_172_1.png)

## 绘制圆的弦

要获取圆的弦，在圆内部绘制一条直线。这条线就是弦。然而，由 `QPainter` 绘制的是圆外的部分。你需要使用 `QPainter::drawChord()` 函数。

```cpp
paint->setPen( QPen(green, 4, QPainter::SolidLine );
paint->drawChord( 20, 20, 210, 160, 500, 1000 );
```

`drawChord()` 函数的参数与 `drawPie()` 完全相同。图 9.9 显示了代码的结果。

图 9.9

绿色圆弦。

![](img/ed4f2be9f0799d95b6f041531c9a1f14_172_2.png)

# 绘制弧

使用 `QPainter` 绘制弧很容易——只需使用 `QPainter::drawArc()` 函数。该函数的参数与 `drawPie()` 和 `drawChord()` 相同。示例如下：

```cpp
paint->setPen( QPen(green, 4, QPainter::SolidLine );
paint->drawArc( 20, 20, 210, 160, 500, 1000 );
```

查看图 9.10 获取代码的结果。

## 图 9.10

绿色圆弧。

![](img/ed4f2be9f0799d95b6f041531c9a1f14_173_0.png)

## 绘制贝塞尔曲线
