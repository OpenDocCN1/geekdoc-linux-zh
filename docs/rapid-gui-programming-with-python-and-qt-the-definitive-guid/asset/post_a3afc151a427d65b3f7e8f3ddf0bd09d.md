
country = self.model.data(
    self.model.index(row, ships.COUNTRY)).toString()
if QMessageBox.question(self, "Ships - Remove",
        QString("Remove %1 of %2/%3%").arg(name).arg(owner) \
        .arg(country),
        QMessageBox.Yes|QMessageBox.No) == QMessageBox.No:
    return
self.model.removeRows(row)
self.resizeColumns()

If the user clicks the Remove button we retrieve the model index for the current table view’s current item. We extract the row from this model index and use it with the QAbstractTableModel.data() method to retrieve the ship’s name, owner, and country. The data() method takes a model index as a mandatory argument and returns a QVariant. We use QAbstractTableModel.index() to create model indexes for the row/column combinations we want, and use QVariant.toString() to convert the returned values to QStrings.

If the user confirms their deletion, we simply remove the relevant row from the model. The model will automatically notify the views, which in turn will update themselves. We have added a call to resizeColumns() since the maximum column widths may have changed after the deletion.

## Implementing the Custom Model

We have now seen some of the QAbstractTableModel’s API in use, along with some extensions of our own. The methods in a model subclass can be divided into three categories:

- Methods that are necessary for implementing read-only models
- Methods that are necessary for implementing editable models
- Methods that we need to extend the API for particular circumstances

The essential methods for read-only table models are data(), rowCount(), and columnCount(), although headerData() is almost always implemented too.

Editable models require reimplementations of the same methods as those needed for read-only models, and in addition, flags() and setData(). If the model is to support adding and removing rows as well as editing existing data, insertRows() and removeRows() must also be implemented.

Other methods can be implemented as well, but those listed in the two preceding paragraphs are the only essential ones.

For the ship model we store the ships in a list in memory and in a binary file on disk. To support this functionality we have extended the model API by adding sortByName(), sortByCountryOwner(), load(), and save().

The ShipTableModel is in chap14/ships.py.

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

We want to load and save the model's data from and to a binary file, so we keep an instance variable with the filename. The ships themselves are stored in a list which is initially unordered. We also keep two sets, one of owners and the other of countries: These will be used to populate comboboxes when we create a custom delegate in the next section.

```python
def rowCount(self, index=QModelIndex()):
    return len(self.ships)
```

```python
def columnCount(self, index=QModelIndex()):
    return 5
```

The row and column counts are easy to provide. It is very common for table models to have a fixed column count.

```python
def data(self, index, role=Qt.DisplayRole):
    if not index.isValid() or \
        not (0 <= index.row() < len(self.ships)):
        return QVariant()
    ship = self.ships[index.row()]
    column = index.column()
    if role == Qt.DisplayRole:
        if column == NAME:
            return QVariant(ship.name)
        elif column == OWNER:
            return QVariant(ship.owner)
        elif column == COUNTRY:
            return QVariant(ship.country)
        elif column == DESCRIPTION:
            return QVariant(ship.description)
        elif column == TEU:
            return QVariant(QString("%L1").arg(ship.teu))
```

The data() method has one mandatory argument—the model index of the item concerned—and one optional argument—the "role". The role is used to indicate what kind of information is required. The default role, Qt.DisplayRole, means that the data as displayed is wanted.

If the model index is invalid or if the row is out of range we return an invalid QVariant. PyQt’s model/view architecture does not raise exceptions or give error messages; it simply uses invalid QVariants. If the index is valid we retrieve the ship at the row corresponding to the index’s row. If the role is Qt.DisplayRole we return the data for the requested column as a QVariant. In the case of the TEU, instead of returning an integer, we return the number as a localized string.

```python
if role == Qt.TextAlignmentRole:
    if column == TEU:
        return QVariant(int(Qt.AlignRight | Qt.AlignVCenter))
    return QVariant(int(Qt.AlignLeft | Qt.AlignVCenter))
elif role == Qt.TextColorRole and column == TEU:
    if ship.teu < 80000:
        return QVariant(QColor(Qt.black))
    elif ship.teu < 100000:
        return QVariant(QColor(Qt.darkBlue))
    elif ship.teu < 120000:
        return QVariant(QColor(Qt.blue))
    else:
        return QVariant(QColor(Qt.red))
elif role == Qt.BackgroundColorRole:
    if ship.country in (u"Bahamas", u"Cyprus", u"Denmark",
                    u"France", u"Germany", u"Greece"):
        return QVariant(QColor(250, 230, 250))
    elif ship.country in (u"Hong Kong", u"Japan", u"Taiwan"):
        return QVariant(QColor(250, 250, 230))
    elif ship.country in (u"Marshall Islands",):
        return QVariant(QColor(230, 250, 250))
    else:
        return QVariant(QColor(210, 230, 230))
return QVariant()
```

If data() is being called with the Qt.TextAlignmentRole, we return a right-alignment for TEUs and a left-alignment for the other columns. QVariants cannot accept alignments, so we must convert them to an integer value.

For the Qt.TextColorRole, we return a color for the TEU column and ignore other columns. This means that the non-TEU columns will have the default text color, usually black. For the Qt.BackgroundColorRole, we provide different colored backgrounds depending on which group of countries the ship belongs to.

We can handle several other roles if we wish, including Qt.DecorationRole (the item’s icon), Qt.ToolTipRole, Qt.StatusTipRole, and Qt.WhatIsThisRole. And for controlling appearance, in addition to the alignment and color roles we discussed earlier, there is Qt.FontRole and Qt.CheckStateRole.

We return an invalid QVariant for all the cases we choose not to handle. This tells the model/view architecture to use a default value in these cases.

Some developers don't like mixing appearance-related information with the data, as we have done here in our data() implementation. PyQt is neutral on this issue: It gives us the flexibility to mix, but if we prefer data() to be purely concerned with data we can do that too, and leave all appearance-related issues to the delegate.

```python
def headerData(self, section, orientation, role=Qt.DisplayRole):
    if role == Qt.TextAlignmentRole:
        if orientation == Qt.Horizontal:
            return QVariant(int(Qt.AlignLeft|Qt.AlignCenter))
        return QVariant(int(Qt.AlignRight|Qt.AlignCenter))
    if role != Qt.DisplayRole:
        return QVariant()
    if orientation == Qt.Horizontal:
        if section == NAME:
            return QVariant("Name")
        elif section == OWNER:
            return QVariant("Owner")
        elif section == COUNTRY:
            return QVariant("Country")
        elif section == DESCRIPTION:
            return QVariant("Description")
        elif section == TEU:
            return QVariant("TEU")
    return QVariant(int(section + 1))
```

Although not essential, it is a good practice to provide a headerData() implementation. The section is a row offset when the orientation is Qt.Vertical, and a column offset when the orientation is Qt.Horizontal. Here, we provide column headers, and number the rows from 1.

Like data(), this method accepts a role, and we use this to make the row numbers right-aligned and the column headers left-aligned.

The methods we have looked at so far are enough to implement read-only table models. Now we will look at the additional methods that must be implemented to make a model editable.

```python
def flags(self, index):
    if not index.isValid():
        return Qt.ItemEnabled
    return Qt.ItemFlags(QAbstractTableModel.flags(self, index)|
           Qt.ItemIsEditable)
```

If we have a valid model index we return a Qt.ItemFlags that combines the existing item flags with the Qt.ItemIsEditable flag. We can use this method to make items read-only by applying the Qt.ItemIsEditable flag only when the model index is for a row and column that we want to be editable.
