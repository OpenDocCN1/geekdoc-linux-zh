
源代码在 `chap08` 目录中，并包含一个使用 Qt Designer 设计的用于添加和编辑电影记录的用户界面。图 8.2 显示了应用程序的 Python 模块。

我们选择区分保存和导出，以及加载和导入。当我们加载文件时，我们使用的文件名将成为应用程序的当前文件名，以便在保存时使用。如果我们保存文件，我们使用应用程序的当前文件名，因此后续保存将指向同一个文件。我们可以通过使用“另存为”操作来更改当前文件名。当我们导入文件时，我们清除当前文件名；这意味着如果用户想要保存数据，必须为其指定一个新的文件名。如果用户导出数据，系统会要求提供新的文件名，且当前文件名不受影响。

现在我们可以查看主窗口的文件处理功能了。我们将通过查看主窗口初始化器的开头开始

![](img/9bfe0a027fcc8793bb087287001100dd_244_0.png)

### 图 8.2 “我的电影”应用程序的模块、类与函数

创建用于持有数据的电影容器以及用于展示数据的 `QTableWidget`。

```python
class MainWindow(QMainWindow):
    def __init__(self, parent=None):
        super(MainWindow, self).__init__(parent)
        self.movies = moviedata.MovieContainer()
        self.table = QTableWidget()
        self.setCentralWidget(self.table)
```

在调用 `super()` 之后，我们创建一个新的空电影容器。（我们将稍后讨论 `Movie` 和 `MovieContainer` 类。）然后我们创建一个 `QTableWidget`。该部件用于展示并可选地编辑表格数据。表格在 `updateTable()` 中进行初始化和填充。由于我们已经在第 6 章中了解如何设置状态栏、创建文件、编辑和帮助操作、填充菜单和工具栏，以及如何从上一个会话的设置中恢复应用程序状态，因此我们省略了初始化程序的其余部分。

为了完整性，我们现在稍作停顿，回顾一下 `updateTable()`，看看表格部件是如何设置和填充的。（如果你更喜欢专注于纯粹的文件处理，可以跳至第 232 页的 `fileNew()` 方法。）我们所采用的方法非常简单直接。PyQt 还提供了一种更复杂的方法来填充和编辑基于项的部件（如列表、表格和树），使用 PyQt 的模型/视图架构——我们将在第 14 章中学习这一点。

```python
def updateTable(self, current=None):
    self.table.clear()
    self.table.setRowCount(len(self.movies))
    self.table.setColumnCount(5)
    self.table.setHorizontalHeaderLabels(["Title", "Year", "Mins", "Acquired", "Notes"])
    self.table.setAlternatingRowColors(True)
    self.table.setEditTriggers(QTableWidget.NoEditTriggers)
    self.table.setSelectionBehavior(QTableWidget.SelectRows)
    self.table.setSelectionMode(QTableWidget.SingleSelection)
    selected = None
```

这个方法相当长，因此我们将分三部分进行回顾。它可以在不带参数的情况下调用，此时仅填充表格；或者可以在传入当前 *电影* 的 `id()` 的情况下调用，此时在填充表格后，会使指定电影的行被选中并可见（如有必要则进行滚动）。如果刚刚添加或编辑了电影，则会传入当前电影。

我们首先清空表格；这会移除所有数据和标题。接下来，我们设置行数和列数，以及列标题。我们设置表格的属性，使得用户无法就地编辑任何内容，因为在这个特定应用程序中，我们偏好使用独立的添加/编辑对话框。我们还确保用户每次只能选择一行。`selected` 变量持有保存当前电影标题和 `id()` 的 `QTableWidgetItem`（如果有的话）。

```python
for row, movie in enumerate(self.movies):
    item = QTableWidgetItem(movie.title)
    if current is not None and current == id(movie):
        selected = item
    item.setData(Qt.UserRole, QVariant(long(id(movie))))
    self.table.setItem(row, 0, item)
    year = movie.year
    if year != movie.UNKNOWNYEAR:
        item = QTableWidgetItem("%d" % year)
        item.setTextAlignment(Qt.AlignCenter)
        self.table.setItem(row, 1, item)
    minutes = movie.minutes
    if minutes != movie.UNKNOWNMINUTES:
        item = QTableWidgetItem("%d" % minutes)
        item.setTextAlignment(Qt.AlignRight|Qt.AlignCenter)
        self.table.setItem(row, 2, item)
    
    item = QTableWidgetItem(movie.acquired.toString(
        QDate.DATEFORMAT))
    
    item.setTextAlignment(Qt.AlignRight|Qt.AlignVCenter)
    self.table.setItem(row, 3, item)
    
    notes = movie.notes
    if notes.length() > 40:
        notes = notes.left(39) + "..."
    self.table.setItem(row, 4, QTableWidgetItem(notes))
```

`QTableWidget` 中的每个单元格都由一个 `QTableWidgetItem` 表示。这些项可以持有可显示的文本以及“用户”数据。我们遍历电影容器中的每一部电影，为每部电影创建一行项。我们将电影的标题存储在每行的第一个单元格（项）中，并设置该用户数据以保存电影的 `id()`。我们必须将 ID 转换为 `long` 类型，以确保它在 `QVariant` 内部被正确保存。一旦项被创建并设置好，我们就将其放置在表格中相应的行和列中。

我们仅在拥有年份和分钟数的数据时才填充这些单元格。对于备注，如果数据过长，我们会将其截断并添加省略号，因为备注可能长达多个段落。

```python
self.table.resizeColumnsToContents()
if selected is not None:
    selected.setSelected(True)
    self.table.setCurrentItem(selected)
    self.table.scrollToItem(selected)
```

当所有表格项添加完成后，我们会调整表格列的大小以匹配其内容。

当我们遍历电影容器中的电影时，电影按字母顺序返回（但忽略开头的 “A”、“An” 和 “The” 等词）。如果用户添加新电影或编辑现有电影，我们希望确保用户刚刚添加或编辑的电影既被选中又可见。这是通过在添加或编辑后调用 `updateTable()` 来实现的，并传入用户添加或编辑的电影 ID。在 `updateTable()` 结尾处，如果传入了电影 ID，`selected` 变量将持有对应于电影标题单元格的项，且该项（因此也是该行）将被设为当前并选中，如有必要，表格部件将滚动以确保该行对用户可见。

```python
def fileNew(self):
    if not self.okToContinue():
        return
    self.movies.clear()
    self.statusBar().clearMessage()
    self.updateTable()
```

该方法与图像切换器应用程序中同名方法相似。关键区别在于，不再是主窗口负责数据，而是将工作委托给保存在 `self.movies` 中的电影容器。当调用 `updateTable()` 时，由于没有电影记录，部件将只显示列标题而没有其他内容。
