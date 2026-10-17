
```cpp
void PlotSettings::scroll(int dx, int dy)

{

    double stepX = spanX() / numTicks;

    minX += dx * stepX;

    maxX += dx * stepX;

    double stepY = spanY() / numTicks;

    minY += dy * stepY;

    maxY += dy * stepY;

}
```

`scroll()` 函数根据给定次数增加（或减少）`minX`、`maxX`、`minY` 和 `maxY` 两个刻度之间的间隔。该函数用于实现 `Plotter::keyPressEvent()` 中的滚动。

```cpp
void PlotSettings::adjust()

{

    adjustAxis(minX, maxX, numTicks);

    adjustAxis(minY, maxY, numTicks);

}
```

`adjust()` 函数从 `mouseEvent` 调用，将 `minX`、`maxX`、`minY` 和 `maxY` 舍入为“漂亮数值”，并确定合适的刻度数。私有函数 `adjustAxis()` 每次处理一个轴。

```cpp
void PlotSettings::adjustAxis(double min, double max, int &numTicks)

{

    const int minTicks = 4;

    double grossStep = (max - min) / minTicks;

    double step = std::pow(10.0, std::floor(std::log10(grossStep)));

    if (5 * step < grossStep) {

        step *= 5;

    } else if (2 * step < grossStep) {

        step *= 2;

    }

    numTicks = int(std::ceil(max / step) - std::floor(min / step));

    if (numTicks < minTicks)

        numTicks = minTicks;

    min = std::floor(min / step) * step;

    max = std::ceil(max / step) * step;

}
```

`adjustAxis()` 将其 `min` 和 `max` 参数转换为“漂亮数字”，并设置计算出的适用于 `[min, max]` 范围的刻度数。由于 `adjustAxis()` 需要修改变量（`minX`, `maxX`, `numTicks` 等）而不是副本，因此参数是非 `const` 引用。`adjustAxis()` 中的大部分代码只是尝试确定两个刻度之间的合适值。为了获得轴上的漂亮数字，我们必须仔细选择步长。例如，对于十进制标记的轴，漂亮的步长值是 $10^n$、$2\cdot10^n$ 或 $5\cdot10^n$ 形式的。我们开始计算“总步长”，即步长值。然后我们找到小于或等于总步长的 $10^n$ 形式的数字。通过对总步长取对数并向下取整，然后将 10 幂该幂来实现。

# 5. 创建自定义组件

例如，如果总步长为 236，我们计算 $\log236 = 2.372$，然后将其向下取整为 2，并获得 $10^2 = 100$ 作为 $10^n$ 形式的候选步值。

一旦我们有了第一个候选步值，就可以用它计算另外两个候选：$2\cdot10^n$ 和 $5\cdot10^n$。对于前面的示例，另外两个候选是 200 和 500。500 候选大于总步长，因此我们无法使用。但 200 小于 236，因此我们在示例中使用 200 作为步长。

这种算法在某些情况下会得到次优的结果。更复杂的算法 Paul S. Heckbert 发表在《Graphics Gems》（Morgan Kaufmann, 1990）上的文章“Nice Numbers for Graph Labels”。

本文解释了如何自定义已有的 Qt 组件，以及如何使用 `QWidget` 作为基类从零构建组件。我们已经在第 2 章看到了如何使用布局管理器布局子组件，并将在第 6 章进一步探讨该主题。

到这里，我们已经掌握了足够使用 Qt 编写完整的 GUI 程序。在第二部分和第三部分中，我们将深入探索 Qt，以便充分利用 Qt 的功能。

# 第二部分

# 中级 Qt

本页特留空

- 在表单上布局组件
- 堆栈布局
- 分割器
- 滚动区域
- 停靠窗口和工具栏
- 多文档界面

![](img/930c1c6fda99d42528450ebcbc940ea_163_0.png)

# 6. 布局管理

放置在表单上的每个组件必须赋予合适的大小和位置。Qt 提供了几个在表单上布局组件的类：`QHBoxLayout`、`QVBoxLayout`、`QGridLayout` 和 `QStacked`。这些类既方便又易用，以至于几乎每个 Qt 开发者都在源码或通过 Qt Designer 使用它们。

使用 Qt 类的另一个原因是确保表单能够自动适应不同的字体、语言和平台。如果用户更改了系统字体设置，应用程序的表单将立即响应，并在必要时调整大小。如果你将应用程序的用户界面翻译成其他语言，布局类会考虑组件翻译后的内容，以避免文本截断。

其他执行布局管理的类还包括 `QSplitter`、`QScrollArea`、`QMainWindow` 和 `QMdiArea`。所有这些类都提供了用户可以操作的灵活布局。例如，`QSplitter` 提供了一个用户可以拖动以调整组件大小的分割条，而 `QMdiArea` 提供 MDI（多文档界面）支持，这是一种在应用程序主窗口内同时显示多个文档的方法。因为它们经常被作布局类的替代方案，我们在本章中介绍了它们。

## 在表单上布局组件

管理表单子组件布局有三种基本方法：绝对定位、手动布局和布局管理器。我们将以图 6.1 所示的查找文件对话框为例，逐一查看这些方法。

绝对定位是布局组件最原始的方法。它是通过为表单子分配硬编码的大小和位置，并为表单分配固定大小来实现的。

```cpp
FindFileDialog::FindFileDialog(QWidget *parent)
 : QDialog(parent)
{
  namedLabel->setGeometry(9, 9, 50, 25);
  namedLineEdit->setGeometry(65, 9, 200, 25);
  lookInLabel->setGeometry(9, 40, 50, 25);
  lookInEdit->setGeometry(65, 40, 200, 25);
  subfoldersCheckBox->setGeometry(9, 71, 256, 23);
  tableWidget->setGeometry(9, 100, 256, 100);
  messageLabel->setGeometry(9, 206, 256, 25);
  findButton->setGeometry(271, 9, 85, 32);
  stopButton->setGeometry(271, 47, 85, 32);
  closeButton->setGeometry(271, 84, 85, 32);
  helpButton->setGeometry(271, 199, 85, 32);
  setWindowTitle(tr("Find Files or Folders"));
  setFixedSize(365, 240);
}
```

绝对定位有很多缺点：

- 用户无法缩调整窗口大小。
- 如果用户选择了异常大的字体，或者应用程序被翻译成其他语言，某些文本可能会截断。
- 控件在某些样式下尺寸可能不合适。
- 位置和大小必须手动计算。这既繁琐又容易出错，并且维护起来非常痛苦。

绝对定位的替代方案是手动布局。通过手动布局，控件仍然被赋予绝对位置，但它们的大小与窗口的大小成比例，而不是完全硬编码。这可以通过

![](img/930c1c6fda99d425284503ebcbc940ea_164_0.png)

图 6.1. 查找文件对话框

# 在表单上布局控件

通过重新实现表单的 `resizeEvent()` 函数来设置其子控件的几何形状来实现：

```cpp
FindFileDialog::FindFileDialog(QWidget *parent)
    : QDialog(parent)
{
    ...
    setMinimumSize(265, 190);
    resize(365, 240);
}

void FindFileDialog::resizeEvent(QResizeEvent * /* an resize event */)
{
    int extraWidth = width() - minimumWidth();
    int extraHeight = height() - minimumHeight();
    namedLabel->setGeometry(9, 9, 50, 25);
    namedLineEdit->setGeometry(65, 9, 100 + extraWidth, 25);
    lookInLabel->setGeometry(9, 40, 50, 25);
    lookInLineEdit->setGeometry(65, 40, 100 + extraWidth, 25);
    subfoldersBox->setGeometry(9, 71, 156 + extraWidth, 23);
    tableWidget->setGeometry(9, 100, 156 + extraWidth,
        50 + extraHeight);
    messageLabel->setGeometry(9, 156 + extraHeight, 156 + extraWidth,
        25);
    findButton->setGeometry(171 + extraWidth, 9, 85, 32);
    stopButton->setGeometry(171 + extraWidth, 47, 85, 32);
    closeButton->setGeometry(171 + extraWidth, 84, 85, 32);
    helpButton->setGeometry(171 + extraWidth, 149 + extraHeight,
        32);
}
```

在 `FindFileDialog` 构造函数中，我们将表单的最小尺寸设置为 265 x 190，初始尺寸设置为 365 x 240。在 `resizeEvent()` 处理程序中，我们对我们想要放大的控件处理任何额外空间。这确保了表单在用户缩调整窗口大时能够平滑缩放。

就像绝对定位一样，手动布局需要程序员计算许多硬编码常量。编写这样的代码非常劳累，特别是当设计发生变化时。而且仍然存在文本截断的风险。我们可以通过考虑子控件的尺寸提示（size hints）来避免这种风险，但这会使代码更加复杂。

在表单上布局控件最方便的解决方案是使用 Qt 的布局管理器。布局管理器为每种控件提供了合理的默认值，并考虑了每个控件的尺寸提示，而尺寸提示通常取决于控件的字体、样式和内容。布局管理器还尊重最小和最大尺寸，并根据字体变化、内容变化和窗口缩放自动调整布局。图 6.2 显示了一个可缩放的查找对话框。

三个最重要的布局管理器是 `QHBoxLayout`、`QVBoxLayout` 和 `QGridLayout`。这些类派生自 `QLayout`，`QLayout` 提供了布局的基本框架。

# 6. 布局管理

![](img/930c1c6fda99d425284503ebcbc940ea_166_0.png)

图 6.2. 调整可缩放对话框的大小。这三个类都受到 Qt Designer 完全支持，也可以直接在代码中使用。这里是使用布局管理器的 `FindFileDialog` 代码：

```cpp
FindFileDialog::FindFileDialog(QWidget *parent)
  : QDialog(parent)
{
    GridLayout *leftLayout = new QGridLayout;
    leftLayout->addWidget(namedLabel, 0, 0);
    leftLayout->addWidget(namedLineEdit, 0, 1);
    leftLayout->addWidget(lookInLabel, 1, 0);
    leftLayout->addWidget(lookInLineEdit, 1, 1);
    leftLayout->addWidget(subFoldersCheckBox, 0, 2);
    leftLayout->addWidget(tableWidget, 3, 2);
    leftLayout->addWidget(messageLabel, 4, 2);
    QVBoxLayout *rightLayout = new QVBoxLayout;
    rightLayout->addWidget(findButton);
    rightLayout->addWidget(stopButton);
    rightLayout->addWidget(closeButton);
    rightLayout->addStretch();
    rightLayout->addWidget(helpButton);
    QHBoxLayout *mainLayout = new QHBoxLayout;
    mainLayout->addLayout(leftLayout);
    mainLayout->addLayout(rightLayout);
    setLayout(mainLayout);
    setWindowTitle(tr("Find Files or Folders"));
}
```

布局由一个 `QHBoxLayout`、一个 `QGridLayout` 和一个 `QVBoxLayout` 处理。左侧的 `QGridLayout` 和右侧的 `QVBoxLayout` 由外层 `QHBoxLayout` 并排放置。对话框周围的边距和控件之间的间距由样式设置默认值；可以使用 `Layout::setMargins()` 和 `Layout::setSpacing()` 进行更改。

# 在表单上布局控件

| | |
|---|---|
| `QLabel` | `QLineEdit` |
| `QLabel` | `QPushButton` |
| `QCheckBox` | `QPushButton` |
| `QTreeWidget` | `QPushButton` |
| `QLabel` | `QPushButton` |

相同的对话框可以在 Qt Designer 中通过视觉方式创建：将控件放置在大致的位置；将它们组合；并点击水平布局、垂直布局或网格布局。使用 `QBoxLayout` 和 `QHBoxLayout` 相当直接，但使用 `QGridLayout` 稍微复杂一些。`QGridLayout` 在二维单元格上工作。`QLabel` 位于 (0, 0)，对应的 `QLineEdit` 位于 (0, 1)。`QCheckBox` 跨越两列；它占据 (2, 0) 和 (2, 1) 单元格。`QTreeWidget` 和其下方的 `QLabel` 跨越两列。`QGridLayout::addWidget()` 的调用具有以下语法：

```cpp
layout->addWidget(widget, row, column, rowSpan, columnSpan);
```
