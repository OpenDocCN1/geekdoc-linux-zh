
## 自定义和交互式图形项

通过调用预设图形项的 setFlags() 方法并传入合适的常量，可以使其成为可移动、可选择和可聚焦的。用户可以使用鼠标拖动可移动的图形项，点击可选择图形项以选择它们，并通过 Ctrl+点击 来选择多个项目。可聚焦的图形项会接收键盘事件，但如果我们创建一个带有键盘事件处理器的图形项子类，它们就会忽略这些事件。类似地，我们可以通过子类化并实现适当的鼠标事件处理程序，使图形项响应鼠标事件。

在本节中，我们将使用两个预设的图形项，并创建两个自定义的图形项子类，以展示如何使用图形项，以及如何控制其行为和外观。我们还将了解如何加载和保存场景，以及如何打印它们。为了完成这些事情，我们将查看图 12.2 中所示的页面设计器应用程序。该程序允许用户创建包含文本、图像和方框的页面。用户还可以创建线条——这些只是宽度或高度为 1 像素的方框。用户创建的图像可以保存和加载为 .pgd 文件，这是一种特定于该应用程序的自定义文件格式，并且可以使用打印对话框进行打印（或保存为 PDF 文件）。

对于文本项，使用 QGraphicsTextItem 的子类，并扩展以允许用户通过双击来设置项的字体和文本。对于方框（和线条）项，使用 QGraphicsItem 的子类。它带有一个上下文菜单，以及支持调整大小的键盘操作，并且处理自身的所有绘制。位图项简单地使用内置的 QGraphicsPixmapItem 类，而页面和页边距参考线使用内置的 QGraphicsRectItem 类。显示场景的视图是 QGraphicsView 的子类，支持橡皮筋选择和鼠标滚轮缩放。

我们将首先查看 QGraphicsView 的子类。然后我们将审查主表单，最后我们将审查自定义的 QGraphicsItem 子类。

```python
class GraphicsView(QGraphicsView):
    def __init__(self, parent=None):
        super(GraphicsView, self).__init__ (parent)
        self.setDragMode(QGraphicsView.RubberBandDrag)
        self.setRenderHint(QPainter.Antialiasing)
        self.setRenderHint(QPainter.TextAntialiasing)

    def wheelEvent(self, event):
        factor = 1.41 ** (-event.delta() / 240.0)
        self.scale(factor, factor)
```

上面的代码是完整的 GraphicsView 子类。在初始化器中，我们设置拖动模式：这意味着在视图上拖动会导致 PyQt 给我们一个橡皮筋，并且被橡皮筋接触到的每个项目都会被选中。渲染提示会传播到在视图内部绘制的所有项目，因此我们不需要为每个单独的图形项设置提示。

每当用户滚动鼠标滚轮时，都会触发滚轮事件，它会导致视图根据滚轮滚动的方向变大或缩小。其效果是改变页面的表观大小——底层的场景完全没有改变。此事件处理器中使用的数学运算相当棘手，但这不是问题，因为该方法可以原样复制和粘贴。

![](img/9bfe0a027fcc8793bb087287001100dd_366_0.png)

**图 12.2** 页面设计器应用程序

在 chap12/pagedesigner.pyw 的顶部附近，我们有一些全局声明。

```python
PageSize = (612, 792)
PointSize = 10

MagicNumber = 0x70616765
FileVersion = 1

Dirty = False
```

![](img/9bfe0a027fcc8793bb087287001100dd_367_0.png)

页面尺寸以点为单位，适用于美国信纸尺寸。（源代码中还包含 A4 页面尺寸，已注释掉。）魔术数和文件版本用于 QDataStream，正如我们在第 8 章和其他地方所看到的。我们还有一个全局脏标志。

我们还没有展示导入内容，但其中包括 functools。这是必需的，因为在上下文菜单中，我们使用 functools.partial( ) 函数来包裹要调用并带有合适参数的方法。

主表单的初始化器相当长，因此我们将分部分查看它，但省略与我们在其他地方看到的相似的代码——例如，创建和布局表单按钮的地方。

```python
class MainForm(QDialog):
    def __init__(self, parent=None):
        super(MainForm, self).__init__(parent)

        self.filename = QString()
        self.copiedItem = QByteArray()
        self.pasteOffset = 5
        self.prevPoint = QPoint()
        self.addOffset = 5
        self.borders = []

        self.printer = QPrinter(QPrinter.HighResolution)
        self.printer.setPageSize(QPrinter.Letter)
```

复制的项本质上是一团描述最近被剪切或复制的项目的二进制数据。我们将此数据存储在应用程序内部，而不是剪贴板上，因为它对任何其他应用程序都没有用。粘贴偏移量在用户重复粘贴相同的项目时使用，而前一个点和添加偏移量在用户重复添加相同类型的图形项时使用。在这两种情况下，新添加的项都被添加在偏移位置，而不是正好在前一个项的顶部。这使得用户更容易看到他们所在的位置。

边框列表将包含两个图形项，都是黄色矩形：一个表示页面轮廓，另一个表示页面内部的轮廓，留出一定的边距空间。它们用作参考线，并且不会被保存或打印。

虽然可以在需要时创建 QPrinter 对象，但通过创建一个并作为实例变量保存，我们确保用户设置（如页面大小）在同一会话内的使用中得以保留。

```python
self.view = QGraphicsView()
self.scene = QGraphicsScene(self)
self.scene.setSceneRect(0, 0, PageSize[0], PageSize[1])
self.addBorders()
self.view.setScene(self.scene)
```

| 语法 | 描述 |
| :--- | :--- |
| s.addEllipse(r, pn, b) | 向 QGraphicsScene s 添加一个由 QRect r 包围、由 QPen pn 勾勒轮廓并由 QBrush b 填充的椭圆 |
| s.addItem(g) | 将 QGraphicsItem g 添加到 QGraphicsScene s。其他 add*() 方法是为创建和添加一些内置图形项提供便利的方法。 |
| s.addLine(l, pn) | 将用 QPen pn 绘制的 QLine l 添加到 s |
| s.addPath(pp, pn, b) | 向 QGraphicsScene s 添加一个由 QPen pn 勾勒轮廓并由 QBrush b 填充的 QPainterPath pp |
| s.addPixmap(px) | 将 QPixmap px 添加到 QGraphicsScene s |
| s.addPolygon(pg, pn, b) | 向 QGraphicsScene s 添加一个由 QPen pn 勾勒轮廓并由 QBrush b 填充的 QPolygon pg |
| s.addRect(r, pn, b) | 向 QGraphicsScene s 添加一个由 QRect r 包围、由 QPen pn 勾勒轮廓并由 QBrush b 填充的矩形 |
| s.addText(t, f) | 使用 QFont f 将文本 t 添加到 QGraphicsScene s |
| s.collidingItems(g) | 返回 QGraphicsItem g 与其发生碰撞的 QGraphicsItems 列表（可能为空） |
| s.items() | 返回 QGraphicsScene s 中的所有 QGraphicsItems；使用不同的参数，可以返回位于特定点、在给定矩形内或与其相交、或与给定多边形或绘制路径相交的项目 |
| s.removeItem(g) | 从 QGraphicsScene s 中移除 QGraphicsItem g；所有权转移给调用者 |
| s.render(p) | 在 QPainter p 上渲染 QGraphicsScene s；可以使用额外参数来控制源矩形和目标矩形 |
| s.setBackgroundBrush(b) | 设置 QGraphicsScene s 的背景为 QBrush b |
| s.setSceneRect(x, y, w, h) | 设置 QGraphicsScene s 的矩形到位置 (x, y)，宽度为 w，高度为 h；参数为浮点数 |
| s.update() | 为 QGraphicsScene s 安排一个绘制事件 |
| s.views() | 返回显示 QGraphicsScene s 的 QGraphicsViews 列表（可能为空） |

我们创建了一个自定义 GraphicsView 类的实例，以及一个标准的 QGraphicsScene。我们在场景上设置的矩形是“窗口”，即场景将使用的逻辑坐标系——在这种情况下，是一个左上角点为 (0,0)，宽度和高度对应于页面尺寸（以点为单位）的矩形。

初始化器的其余部分创建并连接按钮，并布局按钮和视图。

```python
def addBorders(self):
    self.borders = []
    rect = QRect(0, 0, PageSize[0], PageSize[1])
    self.borders.append(self.scene.addRect(rect, Qt.yellow))
    margin = 5.25 * PointSize
    self.borders.append(self.scene.addRect(
        rect.adjusted(margin, margin, -margin, -margin),
        Qt.yellow))
```

此方法创建两个 QGraphicsRectItems，第一个对应于页面的大小，第二个（指示边距）在第一个内部。QRect.adjusted() 方法返回一个矩形，其左上角和右下角点由两组 dx 和 dy 对进行调整。在这种情况下，左上角向右和向下移动（每个坐标都增加了 margin 量），右下角向左和向上移动（每个坐标都减少了 margin 量）。

```python
def removeBorders(self):
    while self.borders:
        item = self.borders.pop()
        self.scene.removeItem(item)
        del item
```

当我们打印或保存时，我们不想包含边框。此方法破坏性地从 self.borders 列表中逐个获取项目（顺序随机），并从场景中移除这些项目。当项目从场景中移除时，场景会自动通知其视图，以便它们可以重绘未覆盖的区域。删除的替代方法是调用 setVisible(False) 来隐藏边框。

调用 QGraphicsScene.removeItem() 会从场景中移除项目（及其子项），但不会删除项目，而是将所有权转移给调用者。因此，在调用 removeItem() 之后，项目仍然存在。我们可以让每个项目引用超出作用域时自动删除项目，但我们更喜欢显式删除项目，以明确表示我们已经接管所有权并且确实要删除它们。

```python
def addPixmap(self):
    path = QFileInfo(self.filename).path() \
    if not self.filename.isEmpty() else "."
    fname = QFileDialog.getOpenFileName(self,
        "Page Designer - Add Pixmap", path,
        "Pixmap Files (*.bmp *.jpg *.png *.xpm)")

    if fname.isEmpty():
```

