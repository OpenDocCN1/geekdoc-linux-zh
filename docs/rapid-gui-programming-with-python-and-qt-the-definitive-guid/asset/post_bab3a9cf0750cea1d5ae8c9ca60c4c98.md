
```python
if rect is None:
    rect = QRectF(-10 * PointSize, -PointSize,
                20 * PointSize, 2 * PointSize)

self.rect = rect
self.style = style
self.setPos(position)
self.setMatrix(matrix)
scene.clearSelection()
scene.addItem(self)
self.setSelected(True)
self.setFocus()
global Dirty
Dirty = True
```

Box items must be able to receive keyboard focus, because we want users to be able to resize boxes by using the arrow keys. If no explicit size is given—for example when the user clicks Add Box, rather than when a box is being re-created from file or being pasted from the copied item—we provide a default size which gives a letterbox shape. We also provide a default line style of a solid line, and a default identity matrix. The rest of the initializer is the same as we used before for text items.

We will omit the code for parentWidget() and itemChange() because their implementations are the same as the ones we used for the TextItem class.

```python
def setStyle(self, style):
    self.style = style
    self.update()
    global Dirty
    Dirty = True
```

This method is used to set the box's line style. It notifies the scene that the item needs repainting, and it sets the dirty flag since we record box line styles when we save into .pgd files.

```python
def contextMenuEvent(self, event):
    wrapped = []
    menu = QMenu(self.parentWidget())
    for text, param in (
        ('$Solid"', Qt.SolidLine),
        ('$Dashed"', Qt.DashLine),
        ('$Dotted"', Qt.DotLine),
        ('$DashDotted"', Qt.DashDotLine),
        ('$DashDotDotted"', Qt.DashDotDotLine)):
        wrapper = functools.partial(self.setStyle, param)
        wrapped.append(wrapper)
    menu.addAction(text, wrapper)

    menu.exec_(event.screenPos())
```

If the user invokes the context menu on the item (for example, by right-clicking on some platforms), this method will be called. This context menu uses partial function application to wrap a method to be called, `setStyle()`, and a parameter to call it with, one of PyQt’s built-in line styles. The wrappers must stay alive long enough for the menu to finish, since it is only at that point that one of them will be called. For this reason we keep a local list of the wrappers; the list will go out of scope only after the menu’s `exec()` call has finished, when the `contextMenuEvent()` itself completes.

```python
def keyPressEvent(self, event):
    factor = PointSize / 4
    changed = False
    if event.modifiers() & Qt.ShiftModifier:
        if event.key() == Qt.Key_Left:
            self.rect.setRight(self.rect.right() - factor)
            changed = True
        elif event.key() == Qt.Key_Right:
            self.rect.setRight(self.rect.right() + factor)
            changed = True
        elif event.key() == Qt.Key_Up:
            self.rect.setBottom(self.rect.bottom() - factor)
            changed = True
        elif event.key() == Qt.Key_Down:
            self.rect.setBottom(self.rect.bottom() + factor)
            changed = True
    if changed:
        self.update()
        global Dirty
        Dirty = True
    else:
        QGraphicsItem.keyPressEvent(self, event)
```

If the user presses the arrow keys and the view has scrollbars, the view will scroll appropriately. This method intercepts arrow key presses that occur with a Shift key press when the item has the keyboard focus, to give the user a means of resizing the box. The `QRect.setRight()` and `QRect.setBottom()` methods change the size of the rectangle because they change the width and height. If we handled the key press event, we call `update()` to schedule a paint event, and mark the page as dirty; otherwise, we call the base class implementation.

Now that we have seen how the box’s behavior is implemented, we are ready to turn our attention to how the box is drawn. When subclassing `QGraphicsItem` we must at least provide implementations of `boundingRect()` and `paint()` methods. It is also common to reimplement `shape()`, but we will defer that to the example in the next section.

> \* Note that this method will not be called if the view has been told to handle context menu events—for example, by having its context menu policy set to `Qt.ActionsContextMenu`.

## Table 12.2 Selected QGraphicsItem Methods #1

| Syntax | Description |
| :--- | :--- |
| `g.boundingRect()` | Returns QGraphicsItem g's bounding QRectf; subclasses should reimplement this |
| `g.collidesWith(Path(pp))` | Returns True if QGraphicsItem g collides with QPainterPath pp |
| `g.collidingItems()` | Returns a (possibly empty) list of the QGraphicsItems that QGraphicsItem g collides with |
| `g.contains(pt)` | Returns True if QGraphicsItem g contains QPointF pt |
| `g.isObscured()` | Returns True if QGraphicsItem g is obscured by its colliding items, providing their z values are larger |
| `g.isSelected()` | Returns True if QGraphicsItem g is selected |
| `g.itemChange(c, v)` | Does nothing; subclasses can reimplement this method to detect changes—for example, in selected status or position. Do not call QGraphicsItem.setPos() directly or indirectly in this method. |
| `g.moveBy(dx, dy)` | Moves QGraphicsItem g by float dx horizontally and by float dy vertically in scene coordinates |
| `g.paint(p, o)` | Does nothing; subclasses should reimplement this to draw themselves on QPainter p and with the option QStyleOptionGraphicsItem o; painting is done in local logical coordinates, by default centered at (0,0) |
| `g.pos()` | Returns QGraphicsItem g's position as a QPointF. If g is a child of another QGraphicsItem, the point is in terms of the parent item's local logical coordinates; otherwise, it is in terms of scene coordinates. |
| `g.resetMatrix()` | Resets QGraphicsItem g's transformation matrix to the identity matrix; for PyQt 4.3, use resetTransform() instead |
| `g.rotate(a)` | Rotates QGraphicsItem g by float a° |
| `g.scale(x, y)` | Scales QGraphicsItem g horizontally by float x and vertically by float y; 1.0 is unscaled, 0.5 is half size, and 3.0 is three times the size |
| `g.scene()` | Returns QGraphicsItem g's QGraphicsScene, or None if it has not been added to a scene |
| `g.sceneBoundingRect()` | Returns QGraphicsItem g's bounding QRectf in scene coordinates—this accounts for transformations |
| `g.setCursor(c)` | Sets g's cursor to c, a QCursor or a Qt.CursorShape |
| `g.setEnabled(b)` | Sets g to be enabled or disabled depending on b |
| `g.setFocus()` | Gives the keyboard focus to QGraphicsItem g |
| `g.setFlag(f)` | Sets the given QGraphicsItem.ItemFlag f on g |

## Table 12.3 Selected QGraphicsItem Methods #2

| Syntax | Description |
| :--- | :--- |
| `g.setMatrix(m)` | Sets QGraphicsItem g's matrix to QMatrix m; for PyQt 4.3, use setTransform() with a QTransform argument |

```python
def boundingRect(self):
    return self.rect.adjusted(-2, -2, 2, 2)
```

This method should return the bounding rectangle of the item, plus half the pen width if the item has an outline. Here we have cheated and made the bounding rectangle a bit larger. This makes it much easier for the user to click the box, even if they have reduced it to being a line with a height or width of just 1 pixel.

We have not implemented the shape() method, so the base class's shape() method will be used, and will produce a shape that is based on the bounding rectangle. Since we have given a larger rectangle than is really the case, the shape will also be larger. The shape is used when determining collision detection, but it does not matter here because we don't use collision detection in this application; we will in the next one, though.

```python
def paint(self, painter, option, widget):
    pen = QPen(self.style)
    pen.setColor(Qt.black)
    pen.setWidth(1)
    if option.state & QStyle.State_Selected:
        pen.setColor(Qt.blue)
    painter.setPen(pen)
    painter.drawRect(self.rect)
```

Painting the box is quite easy. We begin by creating a pen with the line style the user has set, and with a fixed width of 1 logical unit. We change the pen's color if the rectangle is selected, and then we set the pen and draw the rectangle.

Using the graphics view classes and painting graphics items is often easier than reimplementing paint events. This is because each item has its own paint() method, and because the items use a local logical coordinate system whose center is (0,0), which is especially convenient for rotation.

In this section, we have seen the use of predefined graphics items, and custom items, both of which provide custom behavior and the second of which, BoxItem, also does custom drawing. In the example covered in the next section, we will see more sophisticated item painting, as well as collision detection and a simple form of animation.

# Animation and Complex Shapes

In the preceding section, we looked at a graphics view application in which user interaction was central. In this section, we will look at a very different kind of application, one where we simulate a population of creatures, "multipedes", by visualizing each member of the population using a set of graphics items, as shown in Figure 12.4. Each multipede has internal timers. At each time interval the multipede moves, and if it has collisions, its coloring is changed slightly, and eventually it disappears.

We will begin by looking at an extract from the main form's initializer. Then we will review the form's populate() method, which is used to create and position the multipedes. Next we will look at the action of the Pause/Resume button and at the implementation of the zoom slider. Then we will look at the form's timer event, a kind of event handler we have not used before. Once we can see how the application works as a whole, we will look at the implementations of the graphics item subclasses that are used to visualize the multipedes.

```python
class MainForm(QDialog):
    def __init__(self, parent=None):
        super(MainForm, self).__init__(parent)
        self.scene = QGraphicsScene(self)
        self.scene.setSceneRect(0, 0, SCENESIZE, SCENESIZE)
        self.view = QGraphicsView()
        self.view.setRenderHint(QPainter.Antialiasing)
        self.view.setScene(self.scene)
```
