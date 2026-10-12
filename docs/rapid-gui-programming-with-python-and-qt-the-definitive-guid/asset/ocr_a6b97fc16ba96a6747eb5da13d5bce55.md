```
matrix = QMatrix()
stream >> type >> position >> matrix
if offset:
    position += QPointF(offset, offset)
if type == "Text":
    text = QString()
    font = QFont()
    stream >> text >> font
    TextItem(text, position, self.scene, font, matrix)
elif type == "Box":
    rect = QRectF()
    stream >> rect
    style = Qt.PenStyle(stream.readInt16())
    BoxItem(position, self.scene, style, rect, matrix)
elif type == "Pixmap":
    pixmap = QPixmap()
    stream >> pixmap
    self.createPixmapItem(pixmap, position, matrix)
```

This method is used both by paste() and by open() (which loads a .pgd file). It begins by reading in the type, position, and matrix which are stored for every type of item. Then, it adjusts the position by the offset—this is used only if the item is being pasted. Next, the item-specific data is read and a suitable item created using the data that has been gathered.

The TextItem and BoxItem initializers, and the createPixmapItem() method, all create the appropriate graphics items and pass ownership to the scene.

```
def rotate(self):
    for item in self.scene.selectedItems():
        item.rotate(30)
```

If the user clicks Rotate, any selected items are rotated by 30° . There are no child items used in this application, but if any of the rotated items had child items, these too would be rotated.

```
def delete(self):
    items = self.scene.selectedItems()
    if len(items) and QMessageBox.question(self, "Page Designer - Delete", "Delete %d item%s?" % (len(items), "s" if len(items) != 1 else ""), QMessageBox.Yes | QMessageBox.No) == QMessageBox.Yes:
        while items:
            item = items.pop()
            self.scene.removeItem(item)
            del item
            global Dirty
```