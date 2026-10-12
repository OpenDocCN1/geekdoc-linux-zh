```
def paint(self, painter, option, index):
    delegate = self.delegates.get(index.column())
    if delegate is not None:
        delegate.paint(painter, option, index)
    else:
        QItemDelegate.paint(self, painter, option, index)
```

The structure of this method is the key to how the GenericDelegate class works. We begin by getting the column delegate for the given column. If we get a delegate, we pass the work to it; otherwise, we pass the work to the base class.

```
def createEditor(self, parent, option, index):
    delegate = self.delegates.get(index.column())
    if delegate is not None:
        return delegate.createEditor(parent, option, index)
    else:
        return QItemDelegate.createEditor(self, parent, option,
                                           index)
```

This method follows the same pattern as the paint() method, except that it returns a value (the editor that was created for it).

```
def setEditorData(self, editor, index):
    delegate = self.delegates.get(index.column())
    if delegate is not None:
        delegate.setEditorData(editor, index)
    else:
        QItemDelegate.setEditorData(self, editor, index)
```

```
def setModelData(self, editor, model, index):
    delegate = self.delegates.get(index.column())
    if delegate is not None:
        delegate.setModelData(editor, model, index)
    else:
        QItemDelegate.setModelData(self, editor, model, index)
```

These last two GenericDelegate methods follow the same pattern as the paint() and createEditor() methods, using the column delegate if one has been set for the given column, and using the QItemDelegate base class otherwise.

Now that we have seen the GenericDelegate implementation, we can turn our attention to the column delegates that can be inserted into it. In chap16/gen- ericdelegates.py we provide the IntegerColumnDelegate, DateColumnDelegate, PlainTextColumnDelegate, and RichTextColumnDelegate classes. All of them have a similar structure, so we will look at the code for only two of them, Date- ColumnDelegate, and RichTextColumnDelegate. Once the implementation of these is understood (and it is easy, at least for the date column delegate), creating