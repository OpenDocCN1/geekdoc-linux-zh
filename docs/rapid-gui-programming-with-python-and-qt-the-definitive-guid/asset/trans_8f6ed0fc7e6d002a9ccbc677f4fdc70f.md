

# 分隔器

![](img/9bfe0a027fcc8793bb087287001100dd_295_0.png)

## 图 9.5 新闻阅读器应用程序模型

```python
self.messageSplitter = QSplitter(Qt.Vertical)
self.messageSplitter.addWidget(self.messageList)
self.messageSplitter.addWidget(self.messageView)
self.mainSplitter = QSplitter(Qt.Horizintal)
self.mainSplitter.addWidget(self.groupList)
self.mainSplitter.addWidget(self.messageSplitter)
self.setCentralWidget(self.mainSplitter)
```

现在我们创建两个分隔器。第一个是 `messageSplitter`；它在垂直方向上容纳消息列表和消息视图部件，一个在另一个的上方。第二个分隔器 `mainSplitter` 在水平方向上分割，其左侧是组列表部件，右侧是消息分隔器。与盒式布局一样，分隔器可以容纳超过两个部件，在这种情况下，它们会在每对部件之间放置一个分隔条。主分隔器容纳一个部件和另一个分隔器，而后者又容纳了其余两个部件。因此，主分隔器最终容纳了所有内容，并且由于分隔器也是部件（不像盒式布局，它们是布局对象），因此可以将分隔器作为主窗口的中央部件添加进来，就像我们在这里所做的那样。

有些用户觉得分隔器很烦人，因为他们只能通过鼠标来调整大小。我们将通过保存和恢复用户的分隔器大小来最大限度地减少这种不便。这很有帮助，因为用户只需设置一次大小，之后他们设置的大小将被保留。

![](img/9bfe0a027fcc8793bb087287001100dd_296_0.png)

**图 9.6** *新闻阅读器的分隔器和部件*

```python
settings = QSettings()
size = settings.value("MainWindow/Size",
		QVariant(QSize(600, 500))).toSize()
self.resize(size)
position = settings.value("MainWindow/Position",
		QVariant(QPoint(0, 0))).toPoint()

self.move(position)
self.restoreState(
	settings.value("MainWindow/State").toByteArray())
self.messageSplitter.restoreState(
	settings.value("MessageSplitter").toByteArray())
self.mainSplitter.restoreState(
	settings.value("MainSplitter").toByteArray())
```

保存用户的主窗口设置始于一些熟悉的代码，用于恢复窗口的大小、位置以及它可能拥有的工具栏和停靠窗口的状态。分隔器也有状态，并且该状态的恢复和保存方式与主窗口的状态相同。

```python
def closeEvent(self, event):
    if self.okToContinue():
        settings = QSettings()
        settings.setValue("MainWindow/Size", QVariant(self.size()))
        settings.setValue("MainWindow/Position",
            QVariant(self.pos()))
        settings.setValue("MainWindow/State",
            QVariant(self.saveState()))
        settings.setValue("MessageSplitter",
            QVariant(self.messageSplitter.saveState()))
        settings.setValue("MainSplitter",
            QVariant(self.mainSplitter.saveState()))
    else:
        event.ignore()
```

在主窗口的关闭事件中，代码再次以熟悉的方式开始，只是我们现在除了保存主窗口的大小、位置和状态外，还保存了分隔器的状态。

当新闻阅读器应用程序首次运行时，默认情况下，主分隔器将其宽度的整整一半分配给组列表部件，另一半分配给消息分隔器。同样，消息分隔器将其高度的一半分配给消息列表部件，另一半分配给消息视图部件。我们希望更改这些比例，使组列表更窄，消息查看器更高，我们可以通过应用拉伸因子来实现这一点。例如：

```python
self.mainSplitter.setStretchFactor(0, 1)
self.mainSplitter.setStretchFactor(1, 3)
self.messageSplitter.setStretchFactor(0, 1)
self.messageSplitter.setStretchFactor(1, 2)
```

`setStretchFactor()` 的第一个参数是部件的 0 基索引位置（从左到右，或从上到下），第二个参数是要应用的拉伸因子。在这种情况下，我们规定第 0 个部件（组列表部件）的拉伸因子为 1，第 1 个部件（消息分隔器）的拉伸因子为 3，从而将水平空间按 1:3 的比例划分。同样，对于消息分隔器，我们按 1:2 的比例划分垂直空间，偏向消息视图部件。由于我们保存和恢复分隔器的大小，拉伸因子仅在应用程序首次运行时起作用。

# 单文档界面 (SDI)

对于某些应用程序，用户希望能够处理多个文档。这通常可以通过运行应用程序的多个实例来实现，但这可能会消耗大量资源。使用多个实例的另一个缺点是，不容易提供一个公共的“窗口”菜单，供用户在各个文档之间导航。

有三种常用的解决方案。一种是在单个主窗口中使用选项卡部件，每个选项卡持有一个文档。这种方法在 Web 浏览器中很流行，但在编辑文档时可能会造成不便，因为不可能同时看到两个或更多文档。我们将不展示这种方法，因为本章第二部分对选项卡部件的涵盖已经足够，而且你将有机会在练习中自行尝试。另外两种方法是 SDI，我们将在本节中介绍，以及 MDI，我们将在下一节中介绍。

创建 SDI 应用程序的关键在于创建一个窗口子类，该子类处理所有事务，包括加载、保存和清理，使应用程序本质上成为此类窗口的一个或多个集合。

我们将首先查看 SDI 文本编辑器初始化程序中的一些摘录；应用程序本身如图 9.7 所示。

```python
class MainWindow(QMainWindow):
    NextId = 1
```

![](img/9bfe0a027fcc8793bb087287001100dd_298_0.png)

## 图 9.7 具有三个文档的 SDI 文本编辑器

```python
    Instances = set()

    def __init__(self, filename=QString(), parent=None):
        super(MainWindow, self).__init__(parent)
        self.setAttribute(Qt.WA_DeleteOnClose)
        MainWindow.Instances.add(self)
```

`NextId` 静态变量用于为新空白窗口提供编号：“Unnamed-1.txt”、“Unnamed-2.txt”，等等。

该应用程序由一个或多个 `MainWindow` 实例组成，每个实例都必须能够独立操作。然而，有三种常见情况需要在一个实例内部访问所有实例。一种是提供“全部保存”选项，另一种是通过“窗口”菜单让用户在窗口实例之间切换，还有一种是提供“退出”选项，用户可以使用该选项终止应用程序，并且必须隐式关闭每个窗口。`Instances` 静态变量是我们用于跟踪所有实例的工具。

当创建新的窗口实例时，我们设置其在关闭时自我删除。这意味着窗口可以由用户直接关闭，或由其他实例间接关闭（例如在应用程序终止时）。使用 `Qt.WA_DeleteOnClose` 的一个影响是，窗口应该负责保存未保存的更改并清理自身。我们还将窗口添加到窗口实例的静态集中，以便任何窗口实例都可以访问所有其他窗口。我们将在后面深入研究这些事项。

```python
self.editor = QTextEdit()
self.setCentralWidget(self.editor)
```

`QTextEdit` 是我们中央部件的理想选择，有些动作可以直接传递给它，我们将稍后看到。我们现在只查看其中的一些动作，跳过我们之前见过的 `createAction()` 方法。

```python
fileSaveAllAction = self.createAction("Save All",
    self.fileSaveAll, icon="filesave",
    tip="Save all the files")
```

此动作与几乎所有其他文件动作类似，连接到 `MainWindow` 子类的方法之一。

```python
fileCloseAction = self.createAction("&Close", self.close,
    QKeySequence.Close, "fileclose",
    "Close this text editor")
```

“关闭”动作与我们之前看到的类似。通常，我们不重新实现 `close()` 方法，而是重新实现 `closeEvent()` 处理器，以便我们可以拦截窗口的任何正常关闭。不同之处在于，此动作仅关闭当前唯一的窗口，而不是应用程序（除非这是应用程序唯一的窗口）。

```python
fileQuitAction = self.createAction("&Quit", self.fileQuit,
    "Ctrl+Q", "filequit", "Close the application")
```

“退出”动作终止应用程序，通过关闭 SDI 文本编辑器的每个窗口来实现，我们在审查 `fileQuit()` 方法时将会看到这一点。

```python
editCopyAction = self.createAction("&Copy", self.editor.copy,
    QKeySequence.Copy, "editcopy",
    "Copy text to the clipboard")
```

此动作连接到 `QTextEdit` 的相关插槽。“剪切”和“粘贴”动作也是如此。

菜单、工具栏和状态栏都是按照我们之前见过的方式创建的，除了“窗口”菜单，我们现在将查看它。

```python
self.windowMenu = self.menuBar().addMenu("&Window")
self.connect(self.windowMenu, SIGNAL("aboutToShow()"),
    self.updateWindowMenu)
```

我们完全没有向“窗口”菜单添加任何动作。相反，我们只是将菜单的 `aboutToShow()` 方法连接到我们自定义的 `updateWindowMenu()` 方法，正如我们将看到的，该方法会用所有 SDI 文本编辑器窗口填充该菜单。

