
# 应用程序代码概览

应用程序本身的代码位于文件 `chap09/texteditor.py` 中。我们将审查此代码，从 `MainWindow` 子类初始化器中的一些摘录开始。

```python
class MainWindow(QMainWindow):

    def __init__(self, parent=None):
        super(MainWindow, self).__init__(parent)
        self.mdi = QWorkspace()
        self.setCentralWidget(self.mdi)
```

## MDI 工作区

PyQt 的 MDI 控件被称为 `QWorkspace`。与选项卡控件或堆栈控件一样，可以向 `QWorkspace` 添加控件对话框。这些控件由工作区布局，有点像微型的桌面，控件在工作区区域内被平铺、层叠、最小化或由用户拖拽和调整大小。

> 从 Qt 4.3 开始，MDI 由 `QMdiArea` 类提供，其 API 与 `QWorkspace` 相似。

通过调用 `QWorkspace.setCtrlBarsEnabled(True)`，可以拥有一个比其窗口更大的工作区。可以通过指定背景画笔来设置工作区的背景。

## 文件操作

```python
fileNewAction = self.createAction("&New", self.fileNew, QKeySequence.New, "filenew", "Create a text file")
```

大多数文件操作的操作方式与我们之前看到的相同。但正如我们将看到的，MDI 编辑器与 SDI 编辑器一样，没有 `okToContinue()` 方法，因为每个文档窗口都自行处理。

```python
fileQuitAction = self.createAction("&Quit", self.close, "Ctrl+Q", "filequit", "Close the application")
```

如果我们关闭应用程序的窗口，应用程序将终止。所有文档窗口都将关闭，任何具有未保存更改的窗口都负责提示用户并在要求时保存。

## 编辑操作

```python
editCopyAction = self.createAction("&Copy", self.editCopy, QKeySequence.Copy, "editcopy", "Copy text to the clipboard")
```

在 SDI 编辑器中，我们将“复制”、“剪切”和“粘贴”操作传递给每个窗口的 `QTextEdit` 进行处理。这在 MDI 应用程序中是不可能的，因为当用户触发这些操作之一时，它必须应用于当前活动的 `TextEdit` 窗口。因此，主窗口必须自己做一些工作，当我们在审查这些操作的实现时将会看到。

我们没有展示其他文件和编辑操作的代码，因为它们都遵循前面展示的模式。

## 窗口操作

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

## 窗口菜单映射

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

## 构造函数收尾

```python
self.updateWindowMenu()
self.setWindowTitle("Text Editor")
QTimer.singleShot(0, self.loadFiles)
```

在构造函数末尾，我们调用 `updateWindowMenu()` 以强制创建窗口菜单。这可能看起来很奇怪；毕竟，当用户尝试使用菜单时它会被创建，那么为什么现在要这样做呢？原因是，如果我们自动在启动时加载一些文档，用户可能希望使用我们的键盘快捷键（F6 和 Shift+F6）在它们之间导航，但只有当菜单被创建后，快捷键才会生效。
