
然后我们使用 `ShipContainer.ship()` 方法来检索具有给定 ID 的船舶。这是快速的，因为船舶存储在一个以其 ID 为键的字典中。

```python
def addShip(self):
    ship = ships.Ship("Unknown", "Unknown", "Unknown")
    self.ships.addShip(ship)
    self.populateList()
    self.populateTree()
    self.populateTable(id(ship))
    self.tableWidget.setFocus()
    self.tableWidget.editItem(self.tableWidget.currentItem())
```

添加新船舶相对容易，部分原因是我们没有进行任何验证。我们只是创建了一个具有“unknown”值的新船舶（前导空格是为了使这些值突出），并将船舶添加到船舶字典中。然后我们重新填充列表、树和表格，它们都将检索所有船舶，包括我们刚刚创建的那个。我们将新船舶的 ID 传递给 `populateTable` 方法，以确保其第一列是当前且选中的表格项，并给予它键盘焦点。`editItem()` 调用是用户按 F2 或双击启动编辑的程序等效操作，结果是第一个字段，即船舶名称，变得可编辑。用户只需按 Tab 即可编辑其余字段，因为编辑状态将保留，直到他们离开该行或按 Enter（或通过按 Esc 取消）。

> `QString.simplified()` 方法也非常实用。它从两端去除空白，并将每个内部的一个或多个空白字符序列减少为单个空格。

```python
def removeShip(self):
    ship = self.currentTableShip()
    if ship is None:
        return
    if QMessageBox.question(self, "Ships - Remove",
        QString("Remove %1 of %2/63?").arg(ship.name) \
            .arg(ship.owner).arg(ship.country),
        QMessageBox.Yes|QMessageBox.No) == QMessageBox.No:
        return
    self.ships.removeShip(ship)
    self.populateList()
    self.populateTree()
    self.populateTable()
```

移除船只比添加船只更容易。我们获取当前船只，然后弹出一个消息框询问用户是否确定要移除该船只。如果用户点击“是”，我们将该船只从 `ShipContainer` 中移除，并重新填充视图小部件。

尽管像这里一样使用三种不同的视图是不常规的做法，但我们使用的技术，特别是针对 `QTableWidget` 的技术，是完全通用的。

便捷小部件对于小型和临时数据集非常有用，并且可以独立使用——无需单独的数据集，即可自行显示、编辑和存储数据。在本例中，我们选择将数据分离出来，以便为使用模型/视图技术做准备，特别是为下一节主题——自定义模型——铺平道路。

## 创建自定义模型

在本节中，我们将创建一个自定义模型来保存船只数据，并在两个不同的表格视图中显示同一个模型。一个使用此模型的应用程序示例如图 14.3 所示。用户可以独立滚动这两个表格，并可以在其中任何一个中编辑数据，放心地知道任何更改都会自动反映在两个视图中。

我们将首先展示应用程序主窗体的一些摘录。这将展示所使用的部分模型/视图 API。然后我们将查看模型本身的实现。PyQt5 模型/视图架构的一个重要好处是，相同的编码模式被反复使用，因此，一旦我们知道了如何创建一个表格模型，我们就知道了如何创建任何表格（或列表）模型。

该模型由 `chap14/ships.py` 中的 `ShipTableModel` 类提供，应用程序位于 `chap14/ships-model.pyw`。我们通过设置背景色和前景色改进了视图中数据的显示效果，但这也可以在便捷视图中通过调用表项目上的相应方法来完成。前一个例子中存在的问题，特别是所有者或国家没有组合框、TEU 没有数字框，以及原始显示 HTML 描述文本等问题，依然存在。这些问题只有通过使用委托（delegate）才能解决，而这将是下一节的内容。

![](img/9bfe0a027fcc8793bb087287001100dd_438_0.png)

### 实现视图逻辑

从表面上看，使用带有内置模型的便捷视图与使用独立模型的纯视图之间似乎没有区别。在前面的例子中，我们有三个视图呈现相同的基础数据，保持它们同步是我们的责任。在这个例子中，我们将使用两个视图展示相同的数据，并将同步工作交给 PyQt，因为两个视图使用同一个模型。另一个好处是，视图只获取或存储实际看到或编辑的数据，这在使用大型数据集时可以提供显著的性能提升。

我们将从窗体初始化的某些摘录开始。

```python
class MainForm(QDialog):
    def __init__(self, parent=None):
        super(MainForm, self).__init__(parent)
        
        self.model = ships.ShipTableModel(QString("ships.dat"))
        tableLabel1 = QLabel("Table 61")
        self.tableView1 = QTableView()
        tableLabel1.setBuddy(self.tableView1)
        self.tableView1.setModel(self.model)
        
        tableLabel2 = QLabel("Table 62")
        self.tableView2 = QTableView()
        tableLabel2.setBuddy(self.tableView2)
        self.tableView2.setModel(self.model)
```

首先我们创建一个新的模型。然后我们创建两个表格视图以及相应的标签以便于导航。每个表格视图都被赋予同一个模型进行处理。由于布局代码与此无关，我们在此省略了它。

```python
for tableView in (self.tableView1, self.tableView2):
    header = tableView.horizontalHeader()
    self.connect(header, SIGNAL("sectionClicked(int)"),
                 self.sortTable)
    self.connect(addShipButton, SIGNAL("clicked()"), self.addShip)
    self.connect(removeShipButton, SIGNAL("clicked()"),
                 self.removeShip)
    self.connect(quitButton, SIGNAL("clicked()"), self.accept)
    self.setWindowTitle("Ships model")
```

当我们使用自定义模型时，必须自行处理排序。我们将每个表格视图的水平（列）头部连接到一个 `sortTable()` 方法。其他连接与之前类似。但请注意，我们没有为表项目编辑建立连接：因为视图会自动为我们处理编辑，并将更改自动反映回模型，进而使两个视图保持最新状态。

```python
def accept(self):
    if self.model.dirty and \
            QMessageBox.question(self, "Ships - Save?",
                                 "Save unsaved changes?",
                                 QMessageBox.Yes|QMessageBox.No) == QMessageBox.Yes:
        try:
            self.model.save()
        except IOError, e:
            QMessageBox.warning(self, "Ships - Error",
                                "Failed to save: %s" % e)
    QDialog.accept(self)
```
