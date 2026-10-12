
```python
self.emit (SIGNAL(" clicked (QModelIndex)"),
            self.model.index(self.selectedRow, 0))
        else:
            QWidget.keyPressEvent(self, event)
```

We have chosen to support just two key presses: Up Arrow and Down Arrow. If the user presses either of these, we increment or decrement the selected row, make sure that the selected row is in range, and then schedule a paint event.

If the user navigates to the row above the topmost visible row or below the bottommost visible row, we tell the scroll area to make sure that the row that has been scrolled to is visible—if necessary, the scroll area will scroll to achieve this. We also emit a clicked() signal with the newly selected row’s model index. It is quite conventional to use a clicked() signal in this circumstance, since in effect, the user is “clicking” using the keyboard—after all, the signals and slots mechanism is concerned with what the user wants rather than how they asked for it, and here they just want to select a row.

If we do not handle the key press ourselves, that is, for all other key presses, we pass the event on to the base class.

The water quality view widget is visually very different from the table view shown beside it, yet it did not require that much code to implement and was not too difficult to program. We made the widget fairly efficient by reducing the amount of unnecessary painting. We also made the painting code as simple as possible by ensuring that the widget was always exactly the size necessary to display the entire dataset. The disadvantage of this approach is that it pushes responsibility on to the programmer using our widget to use a QScrollArea, although this saves us from having to implement scrolling ourselves.

The water quality view visualizes the data in one-to-one correspondence with the data in the model, but we are not constrained to doing this. It is also possible to create custom views that show aggregated data. In this case, for example, we could have shown one entry per day, or per hour, perhaps by averaging each day or hour’s readings.

## Generic Delegates

As we have seen in earlier chapters, custom delegates allow us to exercise complete control over the appearance and behavior of the data items that appear in views. Although it is obvious that if we have many models, we are likely to want a custom delegate for most if not all of them, what is not so obvious, is that the custom delegates will very likely have a lot of duplicate code.

*This section is partly based on ideas from the author’s whitepaper, “Qt 4’s Model/View Delegates”, available at http://www.ics.com/developers/papers/f.

Imagine that we have just four models, each with an integer ID column, some string columns holding plain text, and a description column holding HTML text, and for some of the models, one or two floating-point columns. All the models have the ID as their first column, but the other columns don’t match up, so each one requires its own custom delegate. Providing the custom delegates is not a big undertaking, but the code dealing with the integer IDs might be the same in all of them; similarly for the strings, HTML strings, and floating-point numbers.

Now imagine that we have to write custom delegates for another half dozen new models; Much of the code will again be duplicated—and this will probably make maintenance more difficult.

What would be better, particularly for models that have one data type per column, like database tables, is if instead of creating a custom delegate for each model, we could compose a delegate from a set of generic components. This would mean that the maintenance would be confined to the generic components, and a bug fix in one would automatically benefit any view that used it.

In code, the effect we are after is something like this:

```python
self.table1 = QTableView()  
self.table1.setModel(self.model1)  
delegate1 = GenericDelegate(self)  
delegate1.insertColumnDelegate(1,  PlaintextColumnDelegate())  
delegate1.insertColumnDelegate(2,  PlaintextColumnDelegate())  
delegate1.insertColumnDelegate(3,  RichTextColumnDelegate())  
delegate1.insertColumnDelegate(4,  IntegerColumnDelegate())  
self.table1.setItemDelegate(delegate1)  

self.table2 = QTableView()  
self.table2.setModel(self.model2)  
delegate2 = GenericDelegate(self)  
delegate2.insertColumnDelegate(1,  IntegerColumnDelegate())  
delegate2.insertColumnDelegate(2,  FloatColumnDelegate())  
delegate2.insertColumnDelegate(3,  FloatColumnDelegate())  
delegate2.insertColumnDelegate(4,  FloatColumnDelegate())  
delegate2.insertColumnDelegate(5,  RichTextColumnDelegate())  
self.table2.setItemDelegate(delegate2)
```

Here we have two separate models, but both use generic delegates that are composed of predefined column delegates that are data-type-specific.

With this approach, we only ever have to create a single plain text column delegate, a single rich text column delegate, and so on, for each data type we want to handle, such as integers, floating-point numbers, dates, times, and date/times. In addition, we might create some project-specific column delegates to handle custom types, but for any given data type there would be only one column delegate, drastically cutting down on code duplication and ensuring that any model can have a “custom” delegate simply by using a generic delegate with suitable column delegates added.

In this section, we will see how to create a `GenericDelegate` class and a couple of example column delegates. Then we will see how they are used in the context of the application shown in Figure 16.2.

| License | Customer | Hired | Mileage #1 | Mileage #2 | Notes | Miles | Days |
|---|---|---|---|---|---|---|---|
| 37 | IT56 LNC | Ms Ingria | 2006-06-06 | 13199 | 2006-06-22 | 17055 | 3856 | 16 |
| 38 | NN07 ALP | Mr Berrich | 2006-06-07 | 18032 | 2006-06-26 | 20901 | Customer complained about the gears | 2869 | 19 |
| 39 | YR56 JRX | Ms Bostom | 2006-06-09 | 25000 | 2006-06-13 | 25540 | 540 | 4 |
| 40 | BO07 WRH | Mr Temhara | 2006-06-10 | 17015 | 2006-07-01 | 22769 | 5754 | 21 |
| 41 | UN06 DUE | Ms Havnil | 2006-06-11 | 14374 | | Sold | | |
| 42 | DV58 GEJ | Ms Jolly | 2006-06-11 | 17142 | 2006-06-21 | 18912 | 1870 | 10 |
| 43 | J57 TDP | Ms Clevy | 2006-06-12 | 23396 | 2006-06-20 | 28364 | Returned damaged | 2368 | 8 |
| 44 | QG06 XBO | Ms Courcia | 2006-06-12 | 17063 | 2006-06-15 | 17600 | 537 | 3 |
| 45 | SJ05 1AQ | Ms Garraway | 2006-06-12 | 12866 | 2006-06-14 | 13509 | Returned with empty fuel tank | 542 | 2 |
| 46 | JY56 RWW | Ms Vernet | 2006-06-14 | 22085 | 2006-06-28 | 26257 | Returned dirty | 4172 | 14 |

**Figure 16.2** A table view using generic delegates

The GenericDelegate class is simple, because it passes almost all the work to other classes.

```python
class GenericDelegate(QItemDelegate):
    def __init__(self, parent=None):
        super(GenericDelegate, self).__init__(parent)
        self.delegates = {}
```

The initializer calls super() as usual, and creates an empty dictionary. The keys will be column indexes and the values will be instances of QItemDelegate sub-classes.

```python
def insertColumnDelegate(self, column, delegate):
    delegate.setParent(self)
    self.delegates[column] = delegate
```

When a new column delegate is inserted into the generic delegate, the generic delegate takes ownership of it and inserts it into the dictionary.

```python
def removeColumnDelegate(self, column):
    if column in self.delegates:
        del self.delegates[column]
```

This method is included for completeness, but it is not likely to be used. If a column delegate is removed, the generic delegate will simply use the QItemDelegate base class for that column.

```python
def paint(self, painter, option, index):
    delegate = self.delegates.get(index.column())
    if delegate is not None:
        delegate.paint(painter, option, index)
    else:
        QItemDelegate.paint(self, painter, option, index)
```

The structure of this method is the key to how the GenericDelegate class works. We begin by getting the column delegate for the given column. If we get a delegate, we pass the work to it; otherwise, we pass the work to the base class.

```python
def createEditor(self, parent, option, index):
    delegate = self.delegates.get(index.column())
    if delegate is not None:
        return delegate.createEditor(parent, option, index)
    else:
        return QItemDelegate.createEditor(self, parent, option,
                                           index)
```

This method follows the same pattern as the paint() method, except that it returns a value (the editor that was created for it).

```python
def setEditorData(self, editor, index):
    delegate = self.delegates.get(index.column())
    if delegate is not None:
        delegate.setEditorData(editor, index)
    else:
        QItemDelegate.setEditorData(self, editor, index)
```

```python
def setModelData(self, editor, model, index):
    delegate = self.delegates.get(index.column())
    if delegate is not None:
        delegate.setModelData(editor, model, index)
    else:
        QItemDelegate.setModelData(self, editor, model, index)
```

These last two GenericDelegate methods follow the same pattern as the paint() and createEditor() methods, using the column delegate if one has been set for the given column, and using the QItemDelegate base class otherwise.

Now that we have seen the GenericDelegate implementation, we can turn our attention to the column delegates that can be inserted into it. In chap16/genericdelegates.py we provide the IntegerColumnDelegate, DateColumnDelegate, PlainTextColumnDelegate, and RichTextColumnDelegate classes. All of them have a similar structure, so we will look at the code for only two of them, DateColumnDelegate, and RichTextColumnDelegate. Once the implementation of these is understood (and it is easy, at least for the date column delegate), creating
