
# 代码示例与说明

## `cut` 方法

```python
def cut(self):
    item = self.selectedItem()
    if item is None:
        return
    self.copy()
    self.scene.removeItem(item)
    del item
```

此方法使用 `copy()` 复制选中的项目，然后将其从场景中移除。如我们在讨论移除边框矩形时提到的，`removeItem()` 仅将项目从场景中移除；它并不删除项目。我们可以让项目在引用超出作用域时被删除，但我们更倾向于显式删除它，以明确表明我们已获取所有权并确实删除了项目。

## `paste` 方法

```python
def paste(self):
    if self.copiedItem.isEmpty():
        return
    stream = QDataStream(self.copiedItem, QIODevice.ReadOnly)
    self.readItemFromStream(stream, self.pasteOffset)
```

如果项目已被剪切或复制到 `copiedItem`，我们只需创建一个数据流并从 `copiedItem` 字节数组中读取项目数据。`readItemFromStream()` 方法负责创建项目并将其添加到场景中。

## `writeItemToStream` 方法

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

此方法被 `copy()`、`cut()`（间接）和 `save()` 使用。对于每个项目，它写入一个描述项目类型的字符串，然后是项目的位置和变换矩阵，接着是任何额外的特定项目数据。对于文本项目，额外数据是项目的文本和字体；对于 pixmap 项目，额外数据是 pixmap 本身——这意味着 `.pgd` 文件可能会很大；对于框，额外数据是框的矩形和线条样式。

## `readItemFromStream` 方法

```python
def readItemFromStream(self, stream, offset=0):
    type = QString()
    position = QPointF()
```

* 在此上下文中，单位矩阵是指设置后不会引发任何变换的矩阵。

```python
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

该方法同时被 `paste()` 和 `open()`（用于加载 `.pgd` 文件）使用。它首先读取存储在每种项目中的类型、位置和矩阵。然后，它根据偏移量调整位置——这仅当项目是被粘贴时才会使用。接下来，读取特定于项目的数据，并使用收集到的数据创建合适的项目。

`TextItem` 和 `BoxItem` 的初始化方法以及 `createPixmapItem()` 方法，都会创建相应的图形项目并将其所有权传递给场景。

## `rotate` 方法

```python
def rotate(self):
    for item in self.scene.selectedItems():
        item.rotate(30)
```

如果用户点击 *旋转*，所有被选中的项目都会旋转 `30°`。本应用中不使用子项目，但如果旋转的项目有任何子项目，这些子项目也会随之旋转。

## `delete` 方法

```python
def delete(self):
    items = self.scene.selectedItems()
    if len(items) and QMessageBox.question(self, "Page Designer - Delete", "Delete %d item%s?" % (len(items), "s" if len(items) != 1 else ""), QMessageBox.Yes | QMessageBox.No) == QMessageBox.Yes:
        while items:
            item = items.pop()
            self.scene.removeItem(item)
            del item
            global Dirty
            Dirty = True
```

如果用户点击 *删除* 且至少有一个项目被选中，系统会询问他们是否想删除选中的项目，如果同意，则逐个删除每个被选中的项目。

## `print` 方法

```python
def print(self):
    dialog = QPrintDialog(self.printer)
    if dialog.exec_():
        painter = QPrinter(self.printer)
        painter.setRenderHint(QPainter.Antialiasing)
        painter.setRenderHint(QPainter.TextAntialiasing)
        self.scene.clearSelection()
        self.removeBorders()
        self.scene.render(painter)
        self.addBorders()
```

`QPrinter` 是一种绘制设备，就像 `QWidget` 或 `QImage` 一样，因此我们可以轻松地绘制到打印机上。这里我们利用了 `QGraphicsScene.render()` 这个便捷方法，它将整个场景（或其选定部分）绘制到绘制设备上。在绘制之前，我们移除边框（黄色矩形），在绘制之后恢复边框。此外，我们在绘制前清除选中状态，因为某些项目在选中时可能会以不同的方式渲染。类似的 `QGraphicsView.render()` 方法可用于将场景（或其选定部分）按所见渲染出来。

## 保存与加载 `.pgd` 文件

我们将省略保存和加载 `.pgd` 文件的代码，因为它与之前处理二进制文件时看到的非常相似。对于保存，我们创建一个 `QDataStream`，调用其 `setVersion()`，并写入一个魔数和文件版本。然后我们遍历场景中的所有项目，每次调用 `writeItemToStream()` 并传入数据流和项目作为参数。对于加载，我们同样创建一个 `QDataStream`。然后读取魔数和文件版本，如果它们是正确的，就删除所有现有项目。只要文件中还有数据，我们就调用 `readItemFromStream()` 并传入流作为参数。该方法读取项目数据并创建项目，在过程中将它们添加到场景。

## 自定义图形项目

我们已经了解了整个应用程序的工作方式，以及如何创建和使用两种预定义的图形项目类，即 `QGraphicsRectItem` 和 `QGraphicsPixmapItem`。现在我们将转向自定义图形视图项目。我们将首先查看 `TextItem` 子类；该类扩展了 `QGraphicsTextItem` 类并增加了额外行为，但将所有绘制工作留给基类。然后我们将查看 `BoxItem` 类；该类包含行为和绘制的代码。
