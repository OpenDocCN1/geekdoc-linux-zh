
```python
self.ships = [ship for country, owner, name, ship in ships]
self.reset()
```

This uses the normal QString.compare(), so it might be better to have used unicode(ship.country), unicode(ship.owner), and unicode(ship.name). Of course, for very large datasets it is probably better to avoid sorting altogether and to use ordered containers instead.

The save() and load() methods are very similar to ones we have seen before for handling binary data using QDataStream, so we will just show an extract from the heart of each, starting with the save() method.

```python
for ship in self.ships:
    stream << ship.name << ship.owner << ship.country \
        << ship.description
    stream.writeInt32(ship.teu)
```

Thanks to using QDataStream we don't have to worry about how long the strings are or about encoding issues.

The ships are loaded in correspondingly: Here is an extract from the load() method:

```python
self.ships = []
while not stream.atEnd():
    name = QString()
    owner = QString()
    country = QString()
    description = QString()
    stream >> name >> owner >> country >> description
    teu = stream.readInt32()
    self.ships.append(Ship(name, owner, country, teu,
        description))
    self.owners.add(unicode(owner))
    self.countries.add(unicode(country))
```

As noted earlier, we keep sets of owners and countries to make them available in comboboxes when we add a custom delegate.

Implementing custom models, particularly list and table models, is quite straightforward. For read-only models we need to implement only three methods, although normally we implement four. For editable models, we normally implement a total of eight methods. Once you have created a couple of models, creating others will become easy, because all list and table models follow the same pattern. Implementing tree models is more challenging; the topic is covered in the last section of Chapter 16.

## Creating Custom Delegates

If we want to exercise complete control over the presentation and editing of data items, we must create a custom delegate. A delegate can be used purely to control appearance—for example, for read-only views—or to control editing by providing custom editors, or both.

![](img/9bfe0a027fcc8793bb087287001100dd_450_0.png)

Figure 14.4 A custom delegate in action

Figure 14.4 looks similar to earlier screenshots, with the only noticeable difference being that the description text is properly formatted rather than shown as raw HTML. However, the differences go much deeper. For example, if we edit the owner or country fields we will get comboboxes populated with the current owners and countries, and if we edit the TEU we will get a spinbox. All this control over the appearance and editing is achieved by using a delegate—and the delegate can be used with convenience views or with pure views, although in this case we have used the delegate with pure views.

For this section we are using the chap14/ships-delegate.pyw application. This is almost identical to ships-model.pyw, differing only in the window title, the fact that we resize all columns rather than skipping the description column, and the fact that we use a custom delegate. The delegate class, ShipDelegate, is in chap14/ships.py. Note that this class requires PyQt 4.1 or later.

Like model subclasses, delegates follow a fixed pattern. In the case of delegates for read-only models, the only method we must reimplement is paint(). For editable models, we must reimplement createEditor(), setEditorData(), and setModelData(). It is also common to reimplement commitAndCloseEditor() if we use QLineEdits or QTextEdits for editing. Finally, it is sometimes necessary to reimplement sizeHint(), as we will see.

It is quite common to create delegates that handle only some of the columns, particularly when it comes to painting, leaving the base class to handle columns where the default behavior is sufficient.

We will begin by looking at a small extract from the main form's constructor to see the creation of the first table:

```python
class MainForm(QDialog):
    def __init__(self, parent=None):
        super(MainForm, self).__init__(parent)

        self.model = ships.ShipTableModel(QString("ships.dat"))
        tableLabel1 = QLabel("Table 61")
        self.tableView1 = QTableView()
        tableLabel1.setBuddy(self.tableView1)
        self.tableView1.setModel(self.model)
        self.tableView1.setItemDelegate(ships.ShipDelegate(self))
```

The only difference from the preceding section is that we have called setItemDelegate(), passing it a newly constructed ship.ShipDelegate. The delegate must be given the form as a parent to keep it alive while the form is in use. The code for the second table is just the same, with the same model being set, but with its own ship.ShipDelegate. This is the only change that's necessary—and now all the work of presenting and editing the data will be handled by the delegates.

```python
class ShipDelegate(QItemDelegate):
    def __init__(self, parent=None):
        super(ShipDelegate, self).__init__(parent)
```

Quite often, a delegate's constructor does not need to do anything, beyond initializing the base class which is all that we do here. In fact, for cases like this we can omit the __init__() altogether.

```python
def paint(self, painter, option, index):
    if index.column() == DESCRIPTION:
        txt = index.model().data(index).toString()
        palette = QApplication.palette()
        document = QTextDocument()
        document.setDefaultFont(option.font)
        if option.state & QStyle.State_Selected:
            document.setHtml(QString("<font color=%2s/>").arg(palette.highlightedText().color().name()) \
                    .arg(txt))
        else:
            document.setHtml(txt)
        color = palette.highlight().color() \
        if option.state & QStyle.State_Selected \
        else QColor(index.model().data(index,
        Qt.BackgroundColorRole)
  painter.save()
  painter.fillRect(option.rect, color)
  painter.translate(option.rect.x(), option.rect.y())
  document.drawContents(painter)
  painter.restore()
else:
  QItemDelegate.paint(self, painter, option, index)
```

For plain text strings, numbers, dates, and so on, the base class QItemDelegate.paint() method works perfectly well, so it is very common not to reimplement it at all. However, in this example, the description column holds HTML, and this we must render ourselves.

The paint() method is called with a painter ready to draw on, a QStyleOptionViewItem which holds various pieces of information including the rectangle in which the painting should take place, and the model index of the item to be drawn.

We begin by retrieving the HTML text using the model's data() method, and relying on the Qt.DisplayRole default that we set in the model, for the second argument. Notice that a model index can give us a reference to the model it refers to with the QModelIndex.model() method.

We then retrieve the application's palette—this is based on the user's theme color preferences. If the item is selected, we apply the palette's highlighted text color to the HTML; otherwise, we use the HTML "as is". The QColor.name() method returns the color as a hexadecimal string; for example, red would be returned as the string "#FF0000", which is the same format used for HTML color specifications. Similarly, we use the palette's highlighted background color if the item is selected; otherwise, we use the background color that the model specifies by calling the data() method with the Qt.BackgroundColorRole.

The QTextDocument.drawContents() method draws relative to the painter's top-left (0, 0) coordinate. For this reason, we move (translate) the painter's top-left corner to the style option rectangle's (x, y) position, and then tell the document to paint itself on the painter.

In many cases, we don't have to bother saving and restoring the painter's state between paint events, but in this case we must. Some Qt programmers consider it a good practice to always save and restore the painter's state, whereas others prefer to do so only when necessary, that is, only when they apply a lasting change to the painter's state, such as applying a transformation, like translation, to it.

Unfortunately, this is not quite the end of the story for drawing HTML. When the view asks for the size hint of an HTML column, the default behavior will be to return a size hint based on the view's font and the number of characters.
