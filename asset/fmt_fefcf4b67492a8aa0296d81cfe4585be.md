
`QLineEdit->setGeometry(65, 9, 100, 25);`

`lookInLabel->setGeometry(9, 40, 50, 25);`

`lookLineEdit->setGeometry(65, 40, 100, 25);`

`subfoldersCheckBox->setGeometry(9, 71, 156, 23);`

`tableWidget->setGeometry(9, 100, 156, 25);`

`messageLabel->setGeometry(9, 156, 200, 25);`

`findButton->setGeometry(271, 9, 85, 32);`

`stopButton->setGeometry(271, 47, 85, 32);`

`closeButton->setGeometry(271, 84, 85, 32);`

`helpButton->setGeometry(271, 149, 85, 32);`

```
}
```

在 `FindFileDialog` 构造函数中，我们将表单的最小尺寸设置为 265 x 190，初始大小设置为 365 x 240。在 `resizeEvent()` 处理程序中，我们将额外的空间分配给我们想要放大的控件。这确保了表单在用户调整大时能够平滑缩放。

```
: QDialog(parent)

{

 ...

 QGridLayout *leftLayout = new QGridLayout;
* leftLayout->addWidget(namedLabel, 0, 0);
* leftLayout->addWidget(namedLineEdit, 0, 1);
* leftLayout->addWidget(lookInLabel, 1, 0);
* leftLayout->addWidget(lookInLineEdit, 1, 1);
* leftLayout->addWidget(subfoldersCheckBox, 2, 0, 1, 2);
* leftLayout->addWidget(tableWidget, 3, 0, 1, 2);
* leftLayout->addWidget(messageLabel, 4, 0, 1, 2);

 QVBoxLayout *rightLayout = new QVBoxLayout;

 rightLayout->addWidget(findButton);

 rightLayout->addWidget(stopButton);
 rightLayout->addWidget(closeButton);

 rightLayout->addStretch();

 rightLayout->addWidget(helpButton);

 QHBoxLayout \*mainLayout = new QHBoxLayout;

 mainLayout->addLayout(leftLayout);

 mainLayout->addLayout(rightLayout);

 setLayout(mainLayout);

 setWindowTitle(tr("Find Files or Folders"));

}
```

布局由一个 `QHBoxLayout`、一个 `QGridLayout` 和一个 `QVBoxLayout` 处理。左侧的 `QGridLayout` 和右侧的 `QVBoxLayout` 由外层的 `QHBoxLayout` 并排放置。对话框周围的边距和子控件之间的间距根据当前的小部件样式设置为默认值；可以使用 `QLayout::setContentsMargins()` 和 `QLayout::setSpacing()` 进行进行修改。

**图 6.3. 查找文件对话框的布局**

[查看全尺寸图像]

![](img/1bc72df8c60cf85926d3aefcc273027d_222_0.png)

可以通过 Qt Designer 以可视化的方式创建相同的对话框：将子控件放置在它们的大致位置；选择那些需要一起布局的控件；然后点击“表单|水平布局”、“表单|垂直布局”或“表单|网格布局”。我们在第 2 章中使用了这种方法来创建了电子表格应用程序的“转到单元格”和“排序”对话框。

使用 `QHBoxLayout` 和 `QVBoxLayout` 非常简单，但使用 `QGridLayout` 稍微复杂一些。`QGridLayout` 工作在二维单元格网格上。布局左上角的 `QLabel` 位于位置 (0, 0)，对应的 `QLineEdit` 位于位置 (0, 1)。`QCheckBox` 跨越两列；它占据位置 (2, 0) 和 (2, 1) 的单元格。下方的 `QTreeWidget` 和 `QLabel` 也跨越两列。调用 `QGridLayout::addWidget()` 的语法如下：

`layout->addWidget(*widget*, *row*, *column*, *rowSpan*, *columnSpan*);`

在这里，`*widget*` 是要插入布局的子控件，`(*row*, *column*)` 是控件占据的顶部单元格，`*rowSpan*` 是控件占据的行数，`*columnSpan*` 是控件占据的列数。如果省略，`*rowSpan*` 和 `*columnSpan*` 参数默认为 1。

`addStretch()` 调用告诉垂直布局管理器在布局的该点消耗空间。通过添加一个伸缩项（stretch item），我们告诉布局管理器在关闭按钮和帮助按钮之间留出任何多余空间。在 Qt Designer 中，我们可以通过插入间距器（spacer）来实现相同的效果。间距器在 Qt Designer 中显示为蓝色的“弹簧”。

使用布局管理器为我们目前讨论的内容提供了额外的益处。如果我们向布局中添加控件或从布局中移除控件，布局将自动适应新情况。对子控件调用 `hide()` 或 `show()` 也是如此。如果子控件的尺寸提示（size hint）发生变化，布局将自动重新生成，并考虑新的尺寸提示。此外，布局管理器还会根据表单子控件的最小尺寸和尺寸提示，自动为整个表单设置一个最小尺寸。

在目前为止的示例中，我们只是简单地将控件放入布局中，并使用间距项（伸缩项）来消耗任何多余空间。在某些情况下，这不足以让布局看起来完全像我们想要那样。在这些情况下，可以通过更改被布局控件的尺寸策略（size policies）和尺寸提示来调整布局。

控件的尺寸策略（size policy）告诉布局系统它应该如何拉伸或缩小。Qt 为所有内置控件提供了合理的默认尺寸策略，但由于没有一个默认值可以适应所有可能的布局，开发者更改表单上一个或两个控件的尺寸策略仍然很常见。`QSizePolicy` 包含水平和垂直部分。以下是最有用的值：

`Fixed`（固定）意味着控件不能增长或缩小。控件始终保持其尺寸提示的大小。

`Minimum`（最小）意味着控件的尺寸提示是其最小尺寸。控件不能缩小到尺寸提示以下，但必要时它可以增长以填充可用空间。

`Maximum`（最大）意味着控件的尺寸提示是其最大尺寸。控件可以缩小到其最小尺寸提示。

`Preferred`（首选）意味着控件的尺寸提示是其首选尺寸，但必要时控件仍然可以缩小或增长。

`Expanding`（扩展）意味着控件可以缩小或增长，而且它特别倾向于增长。使用布局管理器总结了不同策略的含义，这里以一个显示“某些文本”的 `QLabel` 为例。

**图 6.4. 不同策略的含义**

![](img/1bc72df8c60cf85926d3aefcc273027d_224_0.png)

在图中，`Preferred` 和 `Expanding` 以相同的方式描述。那么，它们有什么区别？当表单包含 `Preferred` 和 `Expanding` 时，控件保持其尺寸提示。

还有两种尺寸策略：`MinimumExpanding` 和 `Ignored`。前者在旧版本的 Qt 中某些情况下是必要的，但现在已不再有用；首选的方法是使用 `Expanding` 并重写 `size()`。后者与 `Expanding` 类似，只是它忽略尺寸提示。

另一种影响布局的方法是在子控件上设置最小尺寸、最大尺寸或固定尺寸。布局管理器会在布局控件时尊重这些约束。如果这仍然不够，我们始终可以派生子控件类并重写 `sizeHint()` 来获取所需的尺寸提示。

**第二部分：中级 Qt**

**6. 布局管理**

![](img/1bc72df8c60cf85926d3aefcc273027d_225_0.png)

### 在表单上布局控件

每个放置在表单上的控件都必须具有适当的大小和位置。有三种基本方法可以管理控件的布局：绝对定位、手动布局和布局管理器。Qt 提供了几个在表单上布局的类：`QHBoxLayout`、`QVBoxLayout`、`QGridLayout` 和 `QStackedLayout`。这些类既方便又易用，几乎每个 Qt 开发者都会使用它们，无论是直接在代码中使用还是通过 Qt Designer 使用。

使用 Qt 布局类的另一个原因是它们确保表单能够适应不同的字体、语言和平台。如果用户更改系统字体设置，应用程序的表单将立即做出响应，并在必要时调整大小。如果你将应用程序的用户界面翻译成其他语言，布局类会考虑控件的翻译内容以避免文本截断。

执行布局管理的类还包括 `QSplitter`、`QScrollArea`、`QMainWindow` 和 `QMdiArea`。所有这些类都提供了可以操作的灵活布局。例如，`QSplitter` 提供了一个用户可以拖动以调整控件大小的分割条，`QMdiArea` 支持 MDI（多文档界面），这是一种在应用程序主窗口内同时显示多个文档的方法。由于它们通常被作为布局类的替代方案使用，我们在本章中介绍了它们。

我们将依次使用这些方法，以图6.1所示的“查找文件”对话框为例。

**图 6.1 查找文件对话框**

![](img/1bc72df8c60cf85926d3aefcc273027d_226_0.png)

### 绝对定位

绝对定位是布局部件最粗暴的方法。它是通过给表单子部件分配硬编码的大小和位置，并给表设置固定大小来实现的。以下是使用绝对定位的`FindFileDialog`构造函数的写法：

```cpp
FindFileDialog::FindFileDialog(QWidget *parent)

  : QDialog(parent)

{

  ...

namedLabel->setGeometry(9, 9, 50, 25);

namedLineEdit->setGeometry(65, 9, 200, 25);

lookInLabel->setGeometry(9, 40, 50, 25);

lookInLineEdit->setGeometry(65, 40, 200, 25);

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

- 用户无法调整窗口大小。
- 如果用户选择了异常大的字体，或者应用程序被翻译成其他语言，某些文本可能会截断。
- 部件的大小对于某些样式可能不合适。
- 位置和大小必须手动计算。这既枯燥又容易出错，并使维护变得痛苦。

### 手动布局

绝对定位的替代方案是手动布局。在手动布局中，部件仍然被赋予绝对位置，但它们的大小与窗口的大小成比例，而不是完全硬编码的。这可以通过重写表单的`resizeEvent()` 函数来设置其子部件的几何形状来实现：

代码视图：

```cpp
FindFileDialog::FindFileDialog(QWidget *parent)

  : QDialog(parent)

{

  ...

setMinimumSize(265, 190);

resize(365, 240);

}

void FindFileDialog::resizeEvent(QResizeEvent * /* event*/)

{

  int extraWidth = width() - minimumWidth();

  int extraHeight = height() - minimumHeight();

namedLabel->setGeometry(9, 9, 50, 25);

namedLineEdit->setGeometry(65, 9, 100 + extraWidth, 25);

lookInLabel->setGeometry(9, 40, 50, 25);

lookInLineEdit->setGeometry(65, 40, 100 + extraWidth, 25);

subfoldersCheckBox->setGeometry(9, 71, 156 + extraWidth, 23);

tableWidget->setGeometry(9, 100, 156 + extraWidth, 50 + extraHeight);

messageLabel->setGeometry(9, 156 + extraHeight, 156 + extraWidth, 25);

findButton->setGeometry(171 + extraWidth, 9, 85, 32);

stopButton->setGeometry(171 + extraWidth, 47, 85, 32);

closeButton->setGeometry(171 + extraWidth, 84, 85, 32);

helpButton->setGeometry(171 + extraWidth, 149 + extraHeight, 85, 32);

}
```

在`FindFileDialog`构造函数中，我们将表单的最小大小设置为 265 x 190，初始大小设置为 365 x 240。在`resizeEvent()`处理程序中，我们将任何额外的空间分配给想要增长的部件。这确保了当用户调整窗口大时，表单能够平滑地缩放。

就像绝对定位一样，手动布局需要程序员计算大量的硬编码的常量。编写这样的代码是非常累人的，特别是当设计发生变化时。仍然存在文本截断的风险。我们可以通过考虑子部件的尺寸提示（size hints）来避免这种风险，但这会使代码更加复杂。

### 布局管理器

在表单上布局部件最方便的解决方案是使用Qt的布局管理器（layout managers）。布局管理器为每种部件提供了合理的默认值，并考虑了每个部件的尺寸提示，而这通常取决于部件的字体、样式和内容。布局管理器还尊重最小和最大大小，并根据字体变化、内容变化和窗口大小调整来自动调整布局。图6.2显示了一个可调整大小的“查找文件”对话框。

**图 6.2 调整一个可调整大小的对话框**

[查看全尺寸图像]

![](img/1bc72df8c60cf85926d3aefcc273027d_228_0.png)

三个最重要的布局管理器是`QHBoxLayout`、`QVBoxLayout`和`QGridLayout`。这些类派生自`QLayout`，后者为布局提供了基本框架。这三个类都受Qt Designer的支持，并可以直接在代码中使用。以下是使用布局管理器的`FindFileDialog`代码：

代码视图：

```cpp
FindFileDialog::FindFileDialog(QWidget *parent)

  : QDialog(parent)

{

  ...

QGridLayout *leftLayout = new QGridLayout;

* leftLayout->addWidget(namedLabel, 0, 0);

* leftLayout->addWidget(namedLineEdit, 0, 1);

* leftLayout->addWidget(lookInLabel, 1, 0);

* leftLayout->addWidget(lookInLineEdit, 1, 1);

* leftLayout->addWidget(subfoldersCheckBox, 2, 2);

* leftLayout->addWidget(tableWidget, 3, 2);

* leftLayout->addWidget(messageLabel, 4, 2);

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
