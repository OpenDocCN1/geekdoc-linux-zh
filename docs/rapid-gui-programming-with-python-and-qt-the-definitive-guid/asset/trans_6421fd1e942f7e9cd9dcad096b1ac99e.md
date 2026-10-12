
## SDI 文本编辑器：实例管理与文件操作

当用户关闭窗口时，得益于 `Qt.WA_DeleteOnClose` 标志，该窗口将被删除。但由于我们在静态 `Instances` 集合中持有对该窗口的引用，因此该窗口无法被垃圾回收。为此，我们将窗口的 `destroyed()` 信号连接到一个槽函数，该槽函数通过移除已关闭的窗口来更新 `Instances` 集合。我们将在讨论 `updateInstances()` 方法时对此进行更详细的说明。

由于每个窗口负责处理单个文件，因此每个窗口都可以关联一个文件名。该文件名可以传递给窗口的初始化器，默认为空的 `QString`。初始化器的最后几行代码处理文件名。

```python
self.filename = filename
if self.filename.isEmpty():
    self.filename = "Unnamed-%d.txt" % MainWindow.NextId

MainWindow.NextId += 1
self.editor.document().setModified(False)
self.setWindowTitle("SDI Text Editor - %s" % self.filename)
else:
    self.loadFile()
```

如果窗口没有文件名（例如应用程序刚启动，或者用户调用了“新建文件”操作），我们会创建一个合适的窗口标题；否则，加载指定的文件。

`closeEvent()`、`loadFile()`、`fileSave()` 和 `fileSaveAs()` 方法与我们之前见过的非常相似，因此我们不再赘述。（当然，它们都在源代码 `chap09/sditexteditor.pyw` 中。）相反，我们将重点关注 SDI 应用程序特有的功能。

```python
def fileNew(self):
    MainWindow().show()
```

当用户调用“新建文件”操作时，会调用此方法。该类的一个新实例会被创建，并调用其 `show()` 方法（因此它以非模态方式显示）。在方法结束时，我们预期该窗口会超出作用范围并被销毁，因为它没有 PyQt 父对象，也不是实例变量。但在主窗口的初始化器内部，窗口会将自己添加到静态 `Instances` 集合中，因此对该窗口的对象引用仍然存在，从而导致窗口不被销毁。

```python
def fileOpen(self):
    filename = QFileDialog.getOpenFileName(self, "SDI Text Editor -- Open File")
    if not filename.isEmpty():
        if not self.editor.document().isModified() and \
            self.filename.startswith("Unnamed"):
            self.filename = filename
            self.loadFile()
        else:
            MainWindow(filename).show()
```

此方法与之前见过的类似方法略有不同。如果用户提供了文件名，且当前文档既未修改也未命名（即新的空白文档），我们将文件加载到现有窗口中；否则，创建一个新的窗口，并将要加载的文件名传递给该新窗口。

```python
def fileSaveAll(self):
    count = 0
    for window in MainWindow.Instances:
        if isAlive(window) and \
            window.editor.document().isModified():
            if window.fileSave():
                count += 1
    self.statusBar().showMessage("Saved %d of %d files" % (
        count, len(MainWindow.Instances)), 5000)
```

为了便于用户操作，我们提供了一个“全部保存”菜单选项。调用该选项时，我们会遍历 `Instances` 集合中的每个窗口，并保存每个“存活”且已修改的窗口。

如果窗口未被删除，则被视为“存活”。不幸的是，这并没有看上去那么简单。`QWidget` 有两个生命周期：指向该小部件的 Python 变量的生命周期（在本例中，是 `Instances` 集合中的 `MainWindow` 实例），以及作为计算机窗口系统所感知的底层 PyQt 对象的生命周期。

通常，PyQt 对象及其 Python 变量的生命周期是完全相同的。但在这里可能并非如此。例如，假设我们启动了应用程序，点击几次 文件➡新建，从而拥有三个窗口，然后导航到其中一个窗口并将其关闭。此时，被关闭的窗口（得益于 `Qt.WA_DeleteOnClose` 属性）将被删除。

在底层，PyQt 实际上会在被删除的窗口上调用 `deleteLater()` 方法。这给了该窗口一个机会，使其能够完成正在处理的操作，从而可以干净地删除。这通常会在不到一毫秒内完成，此时底层 PyQt 对象从内存中删除并不再存在。但 `Instances` 集合中的 Python 引用仍然存在，只是现在指向一个已不存在的 PyQt 对象。因此，在访问 `Instances` 集合中的任何窗口之前，我们必须始终检查其是否存活。

```python
def isAlive(obj):
    import sip
    try:
        sip.unwrapInstance(obj)
    except RuntimeError:
        return False
    return True
```

`sip` 模块是 PyQt 的支持模块之一，我们通常不需要直接访问它。但在需要深入挖掘的情况下，它会很有用。在这里，该方法尝试访问变量的底层 PyQt 对象。如果对象已被删除，则会抛出 `RuntimeError` 异常，此时返回 `False`；否则，对象仍然存在，返回 `True`。

> *`isAlive()` 函数基于 Giovanni Bajo 在 PyQt（当时的 PyKDE）邮件列表上的帖子，“如何检测对象是否已被删除”。该列表同时用于 PyQt 和 PyKDE。*

```python
@staticmethod
def updateInstances(qobj):
    MainWindow.Instances = set([window for window \
        in MainWindow.Instances if isAlive(window)])
```

每当窗口被关闭（因此被删除）时，它会发出 `destroyed()` 信号，我们在初始化器中将其连接到 `updateInstances()` 方法。此方法用一个仅包含仍存活的窗口实例的集合覆盖 `Instances` 集合。

那么，为什么我们在遍历 `Instances` 时需要检查是否存活——例如在 `fileSaveAll()` 方法中——既然该方法确保 `Instances` 集合保持最新状态并且只持有存活窗口？原因是从理论上讲，在窗口关闭与 `Instances` 集合更新之间，该窗口可能会在某个其他方法中被遍历。

每当用户点击任何 SDI 文本编辑器窗口中的“窗口”菜单时，都会出现一个列出当前所有窗口的菜单。这是因为 `windowMenu` 的 `aboutToShow()` 信号连接到了填充该菜单的 `updateWindowMenu()` 槽函数。

```python
def updateWindowMenu(self):
    self.windowMenu.clear()
    for window in MainWindow.Instances:
        if isAlive(window):
            self.windowMenu.addAction(window.windowTitle(), self.raiseWindow)
```

首先，清除现有的菜单项；始终至少存在一个，即当前窗口。接下来，我们遍历所有窗口实例，并为任何存活的窗口添加一个操作。该操作具有简单的窗口标题（文件名）作为文本，以及一个在用户调用该菜单选项时要调用的槽函数——`raiseWindow()`。

```python
def raiseWindow(self):
    action = self.sender()
    if not isinstance(action, QAction):
        return
    for window in MainWindow.Instances:
        if isAlive(window) and \
            window.windowTitle() == action.text():
            window.activateWindow()
            window.raise_()
            break
```

此方法可以由“窗口”菜单的任何项调用。我们以一个健全性检查开始，然后遍历窗口实例，查看哪个实例的标题文本与操作的文本匹配。如果找到匹配项，我们将相关窗口设为“活动”窗口（应用程序顶层的拥有键盘焦点的窗口），并将其提升到所有其他窗口之上，以便用户可以看到它。

在随后的 MDI 部分中，我们将学习如何创建更复杂的窗口菜单，包括加速器以及一些额外的菜单选项。

```python
def fileQuit(self):
    QApplication.closeAllWindows()
```

PyQt 提供了一种方便的方法来关闭应用程序的所有顶层窗口。此方法对所有窗口调用 `close()`，进而触发每个窗口的 `closeEvent()`。在此事件中（此处未展示），我们检查 `QTextEdit` 的文本是否有未保存的更改，如果有，则弹出一个消息框询问用户是否想要保存。

```python
app = QApplication(sys.argv)
app.setWindowIcon(QIcon(":/icon.png"))
MainWindow().show()
app.exec_()
```

在 `sditexteditor.pyw` 文件的末尾，我们创建一个 `QApplication` 实例和一个 `MainWindow` 实例，然后启动事件循环。

使用 SDI 方法非常流行，但它有一些缺点。由于每个主窗口都有自己的菜单栏、工具栏以及可能的停靠窗口，与单个主窗口相比，资源开销更大。

> *在 Mac OS X 上，只有一个菜单栏，位于屏幕顶部。它会根据当前拥有焦点的窗口发生变化。*

