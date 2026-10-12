
return
        self.createPixmapItem(QPixmap(fname), self.position())

When the user clicks the `AddPixmap` button this method is called. We simply obtain the name of the image file the user wants to add to the page, and pass the work on to a `createPixmapItem()` method. We don't do everything in one method because splitting the functionality is more convenient—for example, for when we load pixmaps from a Page Designer .ppd file. The `position()` method is used to get the position where an item should be added; we will review it shortly.

```python
def createPixmapItem(self, pixmap, position, matrix=QMatrix()):
    item = QGraphicsPixmapItem(pixmap)
    item.setFlags(QGraphicsItem.ItemIsSelectable | QGraphicsItem.ItemIsMovable)
    item.setPos(position)
    item.setMatrix(matrix)
    self.scene.clearSelection()
    self.scene.addItem(item)
    item.setSelected(True)
    global Dirty
    Dirty = True
```

The graphics view classes include `QGraphicsPixmapItem` which is perfect for showing images in scenes. `QGraphicsItem`'s have three flags in Qt 4.2, ItemIsMovable, ItemIsSelectable and ItemIsFocusable. Qt 4.3 adds ItemClipsToShape, ItemClipsChildrenToShape, and ItemIgnoresTransformations, this last particularly useful for showing text that we don't want the view to transform.

Having created the item, we set its position in the scene. The `setPos()` method is the only item method that works in terms of scene coordinates; all the others work in item local logical coordinates. We do not have to set a transformation matrix (and the one returned by `QMatrix()` is the identity matrix), but we want an explicit matrix so we can use it when we come to save and load (or copy and paste) the scene's items.\*

The `QMatrix` class holds a 3 × 3 matrix and is specifically designed for graphical transformations, rather than being a general matrix class. As such, it is a rare example of a poorly named Qt class. From Qt 4.3, `QMatrix` has been superseded by the more sensibly named `QTransform` class, which is also capable of more powerful transformations since it uses a 4 × 4 matrix.

Once the item is set up, we clear any existing selections and add the item to the scene. Then we select it, ready for the user to interact with it.

```python
def position(self):
    point = self.mapFromGlobal(QCursor.pos())
    if not self.view.geometry().contains(point):
        coord = random.randint(36, 144)
        point = QPoint(coord, coord)
    else:
        if point == self.prevPoint:
            point += QPoint(self.addOffset, self.addOffset)
            self.addOffset += 5
        else:
            self.addOffset = 5
            self.prevPoint = point
    return self.view.mapToScene(point)
```

This method is used to provide a position in the scene where a newly added item should go. If the mouse is over the view, we use the mouse position provided by `QCursor.pos()`—"cursor" in this context means mouse cursor—but add an offset if an item has just been added at the same place. This means that if the user repeatedly presses an Add button, each successive item will be offset from the one before, making it easier for the user to see and interact with them. If the mouse is outside the view, we put the item at a semirandom position near the top left of the scene.

The `mapFromGlobal()` method converts a screen coordinate into a physical widget coordinate as used by the view. But scenes use their own logical coordinate system, so we must use `QGraphicsView.mapToScene()` to convert the physical coordinate into a scene coordinate.

```python
def addText(self):
    dialog = TextItemDlg(position=self.position(),
                         scene=self.scene, parent=self)
    dialog.exec_()
```

This method is called when the user clicks the Add Text button. It pops up a smart add/edit item dialog, shown in Figure 12.3. If the user clicks OK, a new item is added with the text and font of their choice. We won’t discuss the dialog, since it isn’t relevant to graphics programming; its source code is in chap12/pagedesigner.pyw.

We do not need to keep a reference to the added item because we pass ownership of it to the scene inside the smart dialog.

```python
def addBox(self):
    BoxItem(self.position(), self.scene)
```

This method is called when the user clicks the Add Box button. The user can resize the box, even turning it into a line (by reducing the width or height to 1 pixel) by using the arrow keys, as we will see.

Again, we don’t need to keep a reference to the added box item, because ownership is given to the scene.

We want the user to be able to cut, copy, and paste items inside Page Designer, but since the items are not meaningful for other applications we will not use the clipboard.

```python
def copy(self):
    item = self.selectedItem()
    if item is None:
        return
    self.copiedItem.clear()
    self.pasteOffset = 5
    stream = QDataStream(self.copiedItem, QIODevice.WriteOnly)
    self.writeItemToStream(stream, item)
```

If the user invokes the copy action we start by seeing whether there is exactly one selected item. If there is, we clear the copied item byte array, and create a data stream to write to the byte array. There is no need to use QDataStream.setVersion() because the data stream is used only for cutting, copying, and pasting during a single run of the application, so using whatever happens to be the current version is fine. We will look at the writeItemToStream() and the corresponding readItemFromStream() methods later.

```python
def selectedItem(self):
    items = self.scene.selectedItems()
    if len(items) == 1:
        return items[0]
    return None
```

This method returns the one selected item, or None if there are no selected items or if there are two or more selected items. The QGraphicsScene.selectedItems() method returns a list of the selected items. There are also items() methods that return lists of the items that intersect a particular point or are inside a particular rectangle or polygon, and there is a collidingItems() method to report collisions.

![Figure 12.3](img/9bfe0a027fcc8793bb087287001100dd_372_0.png)

> **Figure 12.3** *Adding a new text item*

```python
def cut(self):
    item = self.selectedItem()
    if item is None:
        return
    self.copy()
    self.scene.removeItem(item)
    del item
```

This method copies the selected item using copy(), and then removes it from the scene. As mentioned when we discussed removing the border rectangles, removeItem() only removes an item from the scene; it does not delete the item. We could leave the item to be deleted when the item reference goes out of scope, but we prefer to explicitly delete it to make it clear that we have taken ownership and are really deleting the item.

```python
def paste(self):
    if self.copiedItem.isEmpty():
        return
    stream = QDataStream(self.copiedItem, QIODevice.ReadOnly)
    self.readItemFromStream(stream, self.pasteOffset)
```

If an item has been cut or copied to the copied item, we simply create a data stream and read the item's data from the copied item byte array. The readItemFromStream() method takes care of creating the item and adding it to the scene.

```python
def writeItemToStream(self, stream, item):
    if isinstance(item, QGraphicsTextItem):
        stream << QString("Text") << item.pos() << item.matrix() \
            << item.toPlainText() << item.font()
    elif isinstance(item, QGraphicsPixmapItem):
        stream << QString("Pixmap") << item.pos() \
            << item.matrix() << item.pixmap()
    elif isinstance(item, BoxItem):
        stream << QString("Box") << item.pos() << item.matrix() \
            << item.rect
    stream.writeInt16(item.style)
```

This method is used by copy(), cut() (indirectly), and save(). For each item it writes a string that describes the item's type, then the item's position and transformation matrix, and then any extra item-specific data. For text items, the extra data is the item's text and font; for pixmap items, the extra data is the pixmap itself—which means that the .pgd file could be quite large; and for boxes, the extra data is the box's rectangle and line style.

```python
def readItemFromStream(self, stream, offset=0):
    type = QString()
    position = QPointF()
```

\* An identity matrix in this context is one that, when set, causes no transformations to occur.
