We have provided only two sorts, but there is no reason why more could not be supported. Again, the sortBy*() methods are extensions that we have added to the standard API. When the user sorts we take the opportunity to resize the columns. We do this because editing may have changed the widths that the columns need, and since the sort will change the view anyway, it seems a sensible place to resize without disturbing the user.

```
```
def resizeColumns(self):
    for tableView in (self.tableView1, self.tableView2):
        for column in (ships.NAME, ships.OWNER, ships.COUNTRY,
                       ships.TEU):
            tableView.resizeColumnToContents(column)
```
```

Here we have chosen to resize every column except the description column in both table views.

```
```
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
```

Adding a new ship is similar to what we did in the preceding section, but a little neater. We insert a new row as the last row in the model. Then we retrieve a model index that refers to the first column of the new row. We then find out which table view has (or last had) the keyboard focus, and we set the focus back to that view. We set the view's index to the model index we have retrieved and initiate editing on it.

The rowCount(), insertRows(), and index() methods are part of the standard QAbstractTableModel's API.

```
```
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
```