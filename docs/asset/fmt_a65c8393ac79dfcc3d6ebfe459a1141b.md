
如果用户终止应用程序且存在未保存的更改，我们会在退出前给他们保存的机会。模型的 `dirty` 属性和其 `save()` 方法是我们对 `QAbstractTableModel` API 的扩展，使得模型可以从文件加载和保存数据。

模型的基础类是 `QAbstractItemModel`，但基于行/列的模型通常继承自 `QAbstractTableModel`，它是 `QAbstractItemModel` 的子类之一。

```python
def sortTable(self, section):
    if section in (ships.OWNER, ships.COUNTRY):
        self.model.sortByCountryOwner()
    else:
        self.model.sortByName()
    self.resizeColumns()
```

我们只提供了两种排序方式，但没有任何理由不能支持更多。同样，`sortBy*()` 方法是我们添加到标准 API 的扩展。当用户排序时，我们利用这个机会调整列宽。我们这样做是因为编辑可能会改变列所需的宽度，而且排序本来就会改变视图，所以在这里调整大小而不打扰用户似乎是个明智的做法。

```python
def resizeColumns(self):
    for tableView in (self.tableView1, self.tableView2):
        for column in (ships.NAME, ships.OWNER, ships.COUNTRY,
                       ships.TEU):
            tableView.resizeColumnToContents(column)
```

在这里，我们选择在两个表格视图中调整除描述列以外的所有列的大小。

```python
def addShip(self):
    row = self.model.rowCount()
    self.model.insertRows(row)
    index = self.model.index(row, 0)
    tableView = self.tableView1
    if self.tableView2.hasFocus():
        tableView = self.tableView2
    tableView.setFocus()
    tableView.setCurrentIndex(index)
    tableView.edit(index)
```

添加新船只与上一节所做的类似，但更整洁一些。我们在模型中插入一个新行作为最后一行。然后我们获取一个指向新行第一列的模型索引。接着，我们找出哪个表格视图具有（或最后具有）键盘焦点，并将焦点设置回该视图。我们将视图的索引设置为获取的模型索引，并启动编辑。

`rowCount()`、`insertRows()` 和 `index()` 方法是标准 `QAbstractTableModel` API 的一部分。

```python
def removeShip(self):
    tableView = self.tableView1
    if self.tableView2.hasFocus():
        tableView = self.tableView2
    index = tableView.currentIndex()
    if not index.isValid():
        return
    row = index.row()
    name = self.model.data(
        self.model.index(row, ships.NAME)).toString()
    owner = self.model.data(
        self.model.index(row, ships.OWNER)).toString()
```

`country = self.model.data(`

`    self.model.index(row, ships.COUNTRY)).toString()`

`if QMessageBox.question(self, "Ships - Remove",`

`        QString("Remove %1 of %2/%3%").arg(name).arg(owner) \`

`        .arg(country),`

`        QMessageBox.Yes|QMessageBox.No) == QMessageBox.No:`

`    return`

`self.model.removeRows(row)`

`self.resizeColumns()`

如果用户点击**删除**按钮，我们将获取当前表格视图中当前项目的模型索引。我们从该模型索引中提取行号，并将其与 `QAbstractTableModel.data()` 方法结合使用，以获取船名、所有者和国家。`data()` 方法需要一个模型索引作为必选参数，并返回一个 `QVariant`。我们使用 `QAbstractTableModel.index()` 为我们所需的行/列组合创建模型索引，并使用 `QVariant.toString()` 将返回值转换为 `QString`。

如果用户确认删除，我们只需从模型中移除相应的行。模型会自动通知视图，进而视图会更新自身。由于删除操作后最大列宽可能发生变化，我们添加了一个对 `resizeColumns()` 的调用。

### 实现自定义模型

我们现在已经看到了一些正在使用的 `QAbstractTableModel` 的 API，以及一些我们自己扩展的功能。模型子类中的方法可以分为三类：

- 实现只读模型所必需的方法
- 实现可编辑模型所必需的方法
- 我们需要针对特定情况扩展 API 的方法

只读表格模型的基本方法是 `data()`、`rowCount()` 和 `columnCount()`，尽管 `headerData()` 也几乎总是会被实现。

可编辑模型除了需要重新实现与只读模型相同的方法外，还需要 `flags()` 和 `setData()`。如果模型要支持添加和删除行以及编辑现有数据，还必须实现 `insertRows()` 和 `removeRows()`。

也可以实现其他方法，但前两段中列出的方法是唯一必需的。

对于船舶模型，我们将船舶存储在内存中的一个列表中，并存储在磁盘上的一个二进制文件中。为了支持此功能，我们通过添加 `sortByName()`、`sortByCountryOwner()`、`load()` 和 `save()` 扩展了模型 API。

`ShipTableModel` 位于 `chap14/ships.py` 中。

```python
class ShipTableModel(QAbstractTableModel):
    def __init__(self, filename=QString()):
        super(ShipTableModel, self).__init__()
        self.filename = filename
        self.dirty = False
        self.ships = []
        self.owners = set()
        self.countries = set()
```

我们希望从二进制文件加载和保存模型数据，因此我们保留一个包含文件名的实例变量。船舶本身存储在一个列表中，该列表初始时是无序的。我们还保留两个集合，一个是所有者集合，另一个是国家集合：这些将在我们下一节创建自定义委托时用于填充组合框。

```python
def rowCount(self, index=QModelIndex()):
    return len(self.ships)
```

```python
def columnCount(self, index=QModelIndex()):
    return 5
```

提供行数和列数很简单。表格模型具有固定的列数是很常见的。
