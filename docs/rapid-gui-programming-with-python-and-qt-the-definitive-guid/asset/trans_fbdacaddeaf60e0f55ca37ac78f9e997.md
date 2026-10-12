

## 安装后续步骤

这应该比构建 Qt 快得多。一旦完成，你可以执行最后两个阶段：构建 SIP，然后构建 PyQt，过程与构建 Qt 和 Python 略有不同。

```
cd $HOME/packages
tar xvfz sip-4.6.tar.gz
cd sip-4.6
python configure.py
make
make install
```

这假设（正确版本的）Python 在你的 `$PATH` 中。如果不是这种情况（即因为你安装了两个或更多版本的 Python），请提供适当 Python 可执行文件的完整路径——例如，`$HOME/opt/python25/bin/python configure.py`。安装 SIP 后，你可以安装 PyQt。

```
cd $HOME/packages
tar xvfz PyQt-x11-gpl-4.2.tar.gz
cd PyQt-x11-gpl-4.2
python configure.py
make
make install
```

就像安装 SIP 一样，这假设正确版本的 Python 在你的 `$PATH` 中。同样，如果不是这种情况，在运行 `configure.py` 时请提供适当 Python 可执行文件的完整路径。make 阶段可能需要很长时间（但不会像构建 Qt 那样长）。

Qt、Python 和 PyQt 都附带 HTML 格式的文档。值得将其移动到永久位置，并为浏览器添加合适的书签。三者都附带许多示例；至少值得查看 PyQt 示例并运行演示。（例如，将目录更改为 `$HOME/PyQt-x11-gpl-4.2/examples/tools/qt` demo 并运行 `./qt` demo.py。）

如果你下载了本书的示例，你可能希望在 `$HOME` 中解压 pygtkbook.tar.gz，以获取包含本书所有示例的 `$HOME/pyqt` 目录，以及按章节分类的练习模型答案。在 `$HOME/pyqt` 目录本身中，你会发现 `mkpyqt.py` 和 `makepyqt.pyc`；你可能希望将这些（或软链接）移动到 `$PATH` 上的目录中——例如，`$HOME/bin`——以便更便捷地使用。一些示例依赖于 Qt Designer.ui 文件或 .qrc 资源文件。如何将这些转换为 Python 模块在第 207 页中有所介绍，但现在可能方便地直接执行转换：¹

```
cd $HOME/pyqt
./mkpyqt.py -r
```

这完成了基于 X11 形式的 Unix 和 Unix 克隆（包括 Linux 和 BSD）的安装。你现在已经准备好在你的 Unix 或类 Unix 平台上编写和运行 PyQt 应用程序——它们也可以在不加修改的情况下在 Mac OS X 和 Windows 上运行！

## B

### 精选 PyQt 小部件

这里显示的截图是在 Linux 上使用 KDE 拍摄的，以提供视觉上的一致性。在本书正文中，截图显示的是 Windows、Linux 和 Mac OS X，通常每章有所不同。

![](img/9bfe0a027fcc8793bb087287001100dd_589_0.png)

此小部件可用作显示小部件，尽管它最初是作为用户可以选择特定日期的输入小部件设计的。小部件的显示高度可配置；例如，可以显示或不显示周数，日名称可以用单个字母、简短或完整形式表示，可以设置使用的颜色和字体，还可以设置哪一天被视为一周的开始。还可以设置最小和最大允许日期。在 QDateEdit 或 QTimeEdit 上调用 setCalendarPopup(True) 将导致它们的旋转按钮被箭头按钮取代。如果用户点击箭头按钮，将弹出 QCalendarWidget。

![](img/9bfe0a027fcc8793bb087287001100dd_589_1.png)

复选框可用于向用户提供简单的“是/否”选择。如果调用 QCheckBox.setState(True)，复选框将具有三种状态：用户选中、用户未选中，或用户未更改其之前的状态。三态方法可能适用于表示允许 IS NULL 的布尔数据库字段。

![](img/9bfe0a027fcc8793bb087287001100dd_590_0.png)

截图显示了一个下拉列表已展开的 QComboBox。组合框用于在垂直空间不足以使用 QListView 的情况下向用户提供项目列表。调用 QComboBox.setEditable(True) 允许用户选择列表中的项目之一，或者输入自己的文本。每个组合框项都有文本、可选图标和可选数据。我们可以使用 QComboBox.addItem() 或 QComboBox.setItems() 填充组合框，或者可以使用 QComboBox.setModel() 使用自定义或内置的 QAbstractItemModel 子类。

![](img/9bfe0a027fcc8793bb087287001100dd_590_1.png)

QDateEdit 用于显示和输入日期，QTimeEdit 用于日期和时间，QTimeEdit 用于时间。默认情况下，小部件使用特定于区域设置的日期和时间格式——此处使用美国区域设置显示。格式可以更改，并且可以设置最小和最大允许的日期和时间。

![](img/9bfe0a027fcc8793bb087287001100dd_590_2.png)

此小部件可用于创建一行或一列按钮。按钮可以是具有预定义角色和文本的标准按钮，也可以按我们的选择添加角色和文本。此小部件会根据其角色和底层窗口系统的用户界面指南自动排列按钮。

![](img/9bfe0a027fcc8793bb087287001100dd_590_3.png)

PyQt 提供一个弹出字体对话框，在可用时使用原生字体对话框。如果我们想自己提供字体选择——例如在工具栏中——我们可以使用此处展开的 QFontComboBox。对于 Qt 4.0 和 Qt 4.1，最接近的等效方法（但没有字体预览）是使用普通的 QComboBox，并用 QFontDatabase.families() 返回的列表填充它。

![](img/9bfe0a027fcc8793bb087287001100dd_591_0.png)

分组框可以纯粹用作视觉分组设备，也可以如此处所示变为可检查的。如果可检查，则只有当分组框被选中时，才可以与其中包含的小部件进行交互。如果需要没有标题的框架，可以使用 QFrame 代替。当 QRadioButtons 放在分组框中时，它们会自动正确运行，即用户只能选择其中一个。QComboBoxes 和 QListViews 通常比 QRadioButtons 更方便。

![](img/9bfe0a027fcc8793bb087287001100dd_591_1.png)

此小部件用于查看 QGraphicsScene 中的 QGraphicsItems。任意数量的 QGraphicsViews 可以查看同一个场景，每个都有自己的变换（例如，缩放和旋转），实际上也是如此。如果需要，滚动条会自动出现。每个 QGraphicsView 可以提供自己的背景和前景，覆盖场景提供的背景和前景。

![](img/9bfe0a027fcc8793bb087287001100dd_591_2.png)

QLabel 小部件是一种显示小部件，可用于显示图像、纯文本字符串、QTextDocument 或 HTML。带有加速器（单个下划线字符）的标签可以与“buddy”小部件关联，当按下加速器时，将键盘焦点传递给 buddy。

![](img/9bfe0a027fcc8793bb087287001100dd_591_3.png)

这是一种用于以七段 LCD 样式显示数字的显示小部件。

![](img/9bfe0a027fcc8793bb087287001100dd_591_4.png)

此小部件可以从用户那里接受一行文本。文本可以通过使用验证器（例如，QIntValidator 或 QRegExpValidator）或设置输入掩码，或两者兼之来约束。回显模式可以设置为显示“#8”（或什么都不显示）而不是输入的文本。

#### QListView 和 QListWidget

通过这些小部件，用户可以选择一个项目，或者在适当的选中模式下，选择多个项目。小部件可以是列表模式（如所示），也可以是图标模式，其中图标更大，文本显示在图标下方。QListView 必须与自定义或内置的 QAbstractItemModel 子类配合使用，使用 QListView.setModel()。QListWidget 具有内置模型，因此可以使用 QListWidget.addItem() 和 QListWidget.addItems() 直接向其添加项目。当垂直空间紧张时，可以使用 QComboBox 代替。

#### QProgressBar

此小部件可用于向用户显示长时间运行操作的进度。它通常使用 QStatusBar.addWidget() 或 addPermanentWidget() 放在 QMainWindow 的状态栏中。另一种方法是弹出 QProgressDialog。

#### QPushButton

按钮用于调用操作。如果按钮点击将导致弹出对话框，通常会在按钮文本末尾添加省略号 (...)。按钮也可以设置为具有弹出菜单（在这种情况下，PyQt 会添加一个小三角形指示器），或者可以设置为切换按钮，在点击奇数次时保持按下状态，在点击偶数次时恢复上升状态。从 Qt 4.2 开始，大多数应用程序使用 QDialogButtonBoxes 而不是单独的 QPushButtons。

#### QSlider

滑块通常用于显示比例，并常与显示实际数量的 QLabel 或 QLCDNumber 配合使用。滑块可以垂直或水平对齐。QScrollBar 可用于类似的目的。

#### QDoubleSpinBox 和 QSpinBox

这些小部件用于接受和显示数字。数字可以带前缀或后缀，并具有特定的对齐方式。（此处显示的 QDoubleSpinBox 带有“$”前缀。）可以设置最小值和最大值，对于 QDoubleSpinBox，可以设置小数点后显示的数字位数。替代方法是使用 QLineEdit 配合 QIntValidator 或 QDoubleValidator。

