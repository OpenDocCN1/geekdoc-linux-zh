
## 多文档界面 (MDI)

与 SDI 或运行多个应用程序实例相比，MDI 具有许多优势。MDI 应用程序对资源的需求较低，并且使得让用户能够安排其文档窗口之间的布局变得更加容易。然而，一个缺点是，你无法使用 Alt+Tab（在 Mac OS X 上是 Command+Tab）在 MDI 窗口之间切换，尽管在实际中这很少成为一个问题，因为对于 MDI 应用程序，程序员总是实现一个“窗口”菜单来在窗口之间进行导航。

创建 MDI 应用程序的关键在于创建一个控件子类，该子类处理所有事务，包括加载、保存和清理，同时应用程序将这些控件保留在一个 MDI“工作区”中，并将任何特定于控件的操作传递给它们。

在本节中，我们将创建一个文本编辑器，提供与前一节中 SDI 文本编辑器相同的功能，除了这次我们要将其做成一个 MDI 应用程序。该应用程序如图 9.8 所示。

![](img/9bfe0a027fcc8793bb087287001100dd_305_0.png)

每个文档都通过一个自定义 `TextEdit` 控件的实例来呈现和编辑，该控件是 `QTextEdit` 的子类。该控件设置了 `Qt.WA_DeleteOnClose` 属性，拥有一个文件名实例变量，并加载和保存其给定的文件名。如果控件被关闭（因此被删除），其关闭事件处理程序会给予用户保存任何未保存更改的机会。`TextEdit` 的实现很直接，与我们之前看到的代码非常相似，因此我们在此不再回顾它；其源代码位于模块 `chap09/textedit.py` 中。

应用程序本身的代码位于文件 `chap09/texteditor.py` 中。我们将审查此代码，从 `MainWindow` 子类初始化器中的一些摘录开始。

```python
class MainWindow(QMainWindow):

    def __init__(self, parent=None):
        super(MainWindow, self).__init__(parent)
        self.mdi = QWorkspace()
        self.setCentralWidget(self.mdi)
```

PyQt 的 MDI 控件被称为 `QWorkspace`。与选项卡控件或堆栈控件一样，可以向 `QWorkspace` 添加控件对话框。这些控件由工作区布局，有点像微型的桌面，控件在工作区区域内被平铺、层叠、最小化或由用户拖拽和调整大小。

> 从 Qt 4.3 开始，MDI 由 `QMdiArea` 类提供，其 API 与 `QWorkspace` 相似。

通过调用 `QWorkspace.setCtrlBarsEnabled(True)`，可以拥有一个比其窗口更大的工作区。可以通过指定背景画笔来设置工作区的背景。

```python
fileNewAction = self.createAction("&New", self.fileNew, QKeySequence.New, "filenew", "Create a text file")
```

大多数文件操作的操作方式与我们之前看到的相同。但正如我们将看到的，MDI 编辑器与 SDI 编辑器一样，没有 `okToContinue()` 方法，因为每个文档窗口都自行处理。

```python
fileQuitAction = self.createAction("&Quit", self.close, "Ctrl+Q", "filequit", "Close the application")
```

如果我们关闭应用程序的窗口，应用程序将终止。所有文档窗口都将关闭，任何具有未保存更改的窗口都负责提示用户并在要求时保存。

```python
editCopyAction = self.createAction("&Copy", self.editCopy, QKeySequence.Copy, "editcopy", "Copy text to the clipboard")
```

在 SDI 编辑器中，我们将“复制”、“剪切”和“粘贴”操作传递给每个窗口的 `QTextEdit` 进行处理。这在 MDI 应用程序中是不可能的，因为当用户触发这些操作之一时，它必须应用于当前活动的 `TextEdit` 窗口。因此，主窗口必须自己做一些工作，当我们在审查这些操作的实现时将会看到。

我们没有展示其他文件和编辑操作的代码，因为它们都遵循前面展示的模式。

```python
self.windowNextAction = self.createAction("&Next",
                self.mdi.activateNextWindow, QKeySequence.NextChild)
self.windowPrevAction = self.createAction("&Previous",
                self.mdi.activatePreviousWindow,
                QKeySequence.PreviousChild)
self.windowCascadeAction = self.createAction("Cascade",
                self.mdi.cascade)
self.windowTileAction = self.createAction("&Tile",
                self.mdi.tile)
self.windowRestoreAction = self.createAction("&Restore All",
                self.windowRestoreAll)
self.windowMinimizeAction = self.createAction("&Iconize All",
                self.windowMinimizeAll)
self.windowArrangeIconsAction = self.createAction(
                "Arrange Icons", self.mdi.arrangeIcons)
self.windowCloseAction = self.createAction("&Close",
                self.mdi.closeActiveWindow, QKeySequence.Close)
```

所有窗口操作都被创建为实例变量，因为我们将要在另一个方法中访问它们。对于某些操作，我们可以直接将工作交给 mdi 工作区实例，但对于最小化和恢复所有 MDI 窗口，我们必须自行处理。

```python
self.windowMapper = QSignalMapper(self)
self.connect(self.windowMapper, SIGNAL("mapped(QWidget*)"),
            self.mdi, SLOT("setActiveWindow(QWidget*)"))
```

在我们即将创建的窗口菜单中，我们需要一种方法来使用户选择的窗口成为活动窗口。我们在前一节中看到了一个简单的解决方案。另一种方法是使用偏函数应用，将每个窗口操作连接到 `QWorkspace.setActiveWindow()`，并将相关的 `TextEdit` 作为参数。在这里，我们采用了纯粹的 PyQt 方法，并使用了 `QSignalMapper` 类。当我们要审查 `updateWindowMenu()` 方法时，我们将解释其用法。

```python
self.windowMenu = self.menuBar().addMenu("&Window")
self.connect(self.windowMenu, SIGNAL("aboutToShow()"),
            self.updateWindowMenu)
```

对 `aboutToShow()` 的连接确保我们的 `updateWindowMenu()` 方法在菜单显示之前被调用。

```python
self.updateWindowMenu()
self.setWindowTitle("Text Editor")
QTimer.singleShot(0, self.loadFiles)
```

在构造函数末尾，我们调用 `updateWindowMenu()` 以强制创建窗口菜单。这可能看起来很奇怪；毕竟，当用户尝试使用菜单时它会被创建，那么为什么现在要这样做呢？原因是，如果我们自动在启动时加载一些文档，用户可能希望使用我们的键盘快捷键（F6 和 Shift+F6）在它们之间导航，但只有当菜单被创建后，快捷键才会生效。

```python
def closeEvent(self, event):
    failures = []
    for txtEdit in self.mdi.windowList():
        if txtEdit.isModified():
            try:
                txtEdit.save()
            except IOError, e:
                failures.append(str(e))

    if failures and \
        QMessageBox.warning(self, "Text Editor -- Save Error",
                            "Failed to save%s\nQuit anyway?" % \
                            "\n\t".join(failures),
                            QMessageBox.Yes(QMessageBox.No)) == QMessageBox.No:
        event.ignore()
        return

    settings = QSettings()
    settings.setValue("MainWindow/Size", QVariant(self.size()))
    settings.setValue("MainWindow/Position", QVariant(self.pos()))
    settings.setValue("MainWindow/State", QVariant(self.saveState()))

    files = QStringList()
    for txtEdit in self.mdi.windowList():
        if not txtEdit.filename.startsWith("Unnamed"):
            files.append(txtEdit.filename)
    settings.setValue("CurrentFiles", QVariant(files))
    self.mdi.closeAllWindows()
```

当应用程序终止时，我们给用户保存任何未保存更改的机会。然后我们保存主窗口的大小、位置和状态。我们还保存所有 MDI 窗口中所有文件名的列表。最后，我们调用 `QWorkspace.closeAllWindows()`，这将导致每个窗口接收一个关闭事件。

如果任何保存失败，我们会记录下来，在所有文件处理完毕后，如果存在错误，我们弹出一个消息框通知用户，并给予他们取消终止应用程序的机会。
