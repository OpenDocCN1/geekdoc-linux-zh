
PyQt also provides some pure view widgets, including QListView, QTableView, and QTreeView. These must be used in conjunction with external models, either ones we create ourselves or one of the built-in models such as QStringListModel, QDirModel, or QSqlTableModel. In the second section, we will see how to create a custom model that can be used with a view widget.

All the convenience views and pure views use a default delegate that controls how data items are presented and edited. In this chapter’s last section, we will see how to create a custom delegate to exercise complete control over the editing and presentation of data items. Custom delegates can be used with any view, whether it is a convenience view or a pure view.

This chapter provides a foundation in using PyQt’s model/view classes. In Chapter 15, we will see how to use the model/view classes to work with databases, and in Chapter 16, we will cover more advanced uses, including the creation of custom views, improving code reuse in delegates, and presenting tabular data in trees.

We use the same dataset for all the examples in this chapter to make it easier to compare and contrast the techniques used. The dataset’s items are described in the first section.

## Using the Convenience Item Widgets

The convenience item widgets are view widgets that have built-in models. They use a default delegate for presenting and editing data, but this can be replaced by a custom delegate if we wish.

The screenshot in Figure 14.2 shows the same dataset in three different convenience view widgets. This means that the data is copied into each widget separately, so there is considerable data duplication. Another issue is that if we allow the user to edit the data, we must write code to ensure that all the views stay in sync. These problems would not exist if we used a custom model, as we will see in the next section.

![](img/9bfe0a027fcc8793bb087287001100dd_429_0.png)

Figure 14.2 *QListView*, *QTableView*, and *QTreeView* in action

The dataset we are using is a set of information about container ships. Each ship is represented by a Ship object, defined in the chap14/ships.py module.

```python
class Ship(object):
    def __init__(self, name, owner, country, teu=0, description=""):
        self.name = QString(name)
        self.owner = QString(owner)
        self.country = QString(country)
        self.teu = teu
        self.description = QString(description)

    def __cmp__(self, other):
        return QString.localeAwareCompare(self.name.toLower(),
                other.name.toLower())
```

The preceding code is the complete Ship class. The integer teu attribute stands for “twenty-foot equivalent units”, that is, how many 20-foot containers the ship can hold. (Nowadays most containers are 40 feet, so each counts as 2 TEUs.) The name, owner, and country attributes are all plain text, but the description attribute holds one line of HTML.

The `__cmp__()` special method provides a means of comparison for the purpose of sorting. The `QString.localeAwareCompare()` method does string comparisons in a locale-sensitive way—for example, correctly handling accented characters.

Since we are using convenience views with no custom delegates, we have only limited control over the editing of the data items. For example, we cannot offer drop-down combo boxes for editing owners and countries, or use spinboxes for editing TEUs. Also, the description text is shown raw, rather than being interpreted as HTML. We will, of course, solve all of these problems as the chapter progresses, but for now we will just focus on using the convenience views.

For the list, table, and tree items that are used with the convenience view widgets, it is possible to set their font, text alignment, text color, and background color, and to give them an icon or make them checkable. For the pure view widgets, we can exercise similar control over the appearance of items through the custom model; or exercise complete control over both the appearance and the editing of items by using a custom delegate.

The code for this section’s example is in chap14/ships-dict.pyw. The data is held in a Python dictionary that itself is wrapped in the ships.ShipContainer class. We will discuss only the code that is relevant to model/view programming here—the rest of the code uses ideas and idioms that we already saw earlier in the book—for example, in Chapter 8—and is not hard to follow.

```python
class MainForm(QDialog):
    def __init__(self, parent=None):
        super(MainForm, self).__init__(parent)
        listLabel = QLabel("&List")
        self.listWidget = QListWidget()
        listLabel.setBuddy(self.listWidget)
        tableLabel = QLabel("&Table")
        self.tableWidget = QTableWidget()
        tableLabel.setBuddy(self.tableWidget)
        treeLabel = QLabel("&Tree")
        self.treeWidget = QTreeWidget()
        treeLabel.setBuddy(self.treeWidget)
```

For each convenience view we create a label and set up a buddy to make keyboard navigation easier. The layout code is similar to what we have seen before, so we have omitted it and will concern ourselves only with the connections and with creating the data structure.

```python
self.connect(self.tableWidget, SIGNAL("itemChanged(QTableWidgetItem*)"), self.tableItemChanged)
self.connect(addShipButton, SIGNAL("clicked()"), self.addShip)
self.connect(removeShipButton, SIGNAL("clicked()"), self.removeShip)
self.connect(quitButton, SIGNAL("clicked()"), self.accept)
self.ships = ships.ShipContainer(QString("ships.dat"))
self.setWindowTitle("Ships (dict)")
```

By default, list widgets are not editable, so all users can do is select an item. This is also true of tree widgets. But table widgets are editable by default, with users able to initiate editing by pressing F2 or by double-clicking a cell. We can exercise full control over whether a view widget is editable using QAbstractItemView.setEditTriggers(); so, for example, we can make tables read-only or lists editable.

This application allows users to edit ship data in the table, and to add and remove ships. It also keeps all three views up-to-date by repopulating them after the data is loaded, and whenever a change occurs.

```python
def populateList(self, selectedShip=None):
    selected = None
    self.listWidget.clear()
    for ship in self.ships.inOrder():
        item = self.listWidget.item(QString("%1 of %2\3 (%4)") \
            .arg(ship.name).arg(ship.owner).arg(ship.country) \
            .arg(ship.teu))
        self.listWidget.addItem(item)
        if selectedShip is not None and selectedShip == id(ship):
            selected = item
    if selected is not None:
        selected.setSelected(True)
        self.listWidget.setCurrentItem(selected)
```

This method, like the other populating methods, is used both to populate the widget, and to select the item that corresponds to the selectedShip—a ship's id()—if one is passed in.

We begin by clearing the widget. Then we iterate over every ship in the ships container. The inOrder() method is provided by our custom ShipContainer class. For each ship we create a single list widget item that holds a single string. We use QString.arg() so that we can use `\,` to show the TEUs with the appropriate digit separators (e.g., commas).

![](img/9bfe0a027fcc8793bb087287001100dd_432_0.png)

If we reach a list widget item that is showing the selected ship, we keep a reference to the item in selected, and after the list widget has been populated, we make the selected item both current and selected.

```python
def populateTable(self, selectedShip=None):
    selected = None
    self.tableWidget.clear()
    self.tableWidget.setSortingEnabled(False)
    self.tableWidget.setRowCount(len(self.ships))
    headers = ["Name", "Owner", "Country", "Description", "TEU"]
    self.tableWidget.setColumnCount(len(headers))
    self.tableWidget.setHorizontalHeaderLabels(headers)
```

The populate table method is quite similar to the populate list method. We begin by clearing the table—this clears both the cells and the vertical and horizontal headers (the row numbers and column titles). We then set the number of rows and columns, as well as the column titles.

We want users to be able to click a column to have the table sort by that column's contents. This functionality is built into QTableWidget, but it must be switched off before populating the table. We will switch sorting back on once the table is populated.

```python
for row, ship in enumerate(self.ships):
    item = QTableWidgetItem(ship.name)
    item.setData(Qt.UserRole, QVariant(long(id(ship))))
    if selectedShip is not None and selectedShip == id(ship):
        selected = item

    self.tableWidget.setItem(row, ships.NAME, item)
    self.tableWidget.setItem(row, ships.OWNER,
        QTableWidgetItem(ship.owner))
```
