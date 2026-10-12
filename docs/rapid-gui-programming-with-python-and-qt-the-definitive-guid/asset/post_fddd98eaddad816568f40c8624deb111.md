
This method is the default one used for collision detection, unless we specify a coarser-grained approach that uses just the bounding rectangle. A painter path is a series of rectangles, ellipses, arcs, and other shapes (including painter paths) that together completely describe an item's shape. In this case, the path is just one ellipse.

Using a painter path for a graphics item's shape ensures that collisions are detected accurately. For example, two multipede heads may cross at the corners of their rectangles without colliding, since their ellipses don't occupy the corners.

```python
def paint(self, painter, option, widget=None):
    painter.setPen(Qt.NoPen)
    painter.setBrush(QBrush(self.color))
    painter.drawEllipse(Head.Rect)
    if option.levelOfDetail > 0.5:
        painter.setBrush(QBrush(Qt.yellow)) # Outer eyes
        painter.drawEllipse(-12, -19, 8, 8)
        painter.drawEllipse(-12, 11, 8, 8)
        if option.levelOfDetail > 0.9:
            painter.setBrush(QBrush(Qt.darkBlue)) # Inner eyes
            painter.drawEllipse(-12, -19, 4, 4)
            painter.drawEllipse(-12, 11, 4, 4)
            if option.levelOfDetail > 1.3:
                painter.setBrush(QBrush(Qt.white)) # Nostrils
                painter.drawEllipse(-27, -5, 2, 2)
                painter.drawEllipse(-27, 3, 2, 2)
```

The head in full detail is an ellipse, two eyes, each of which is two ellipses, one inside the other, and two tiny nostrils, again ellipses. The paint() method begins by getting rid of the pen and by setting a solid brush to the multipede's color. Then the basic head shape is drawn.

The option variable is of type QStyleOptionGraphicsItem, and it holds various useful information, including the item's transformation matrix, font metrics, palette, and state (selected, "on", "off", and many others). It also holds the "level of detail", a measure of how zoomed in or out the scene is. If the scene is not zoomed at all, the level of detail is 1.0; if it is zoomed in to twice the size, the level of detail will be 2.0, and if it is zoomed out to half the size, the level of detail will be 0.5.

If the scene is being shown at 50% of its natural size or larger, we draw the multipede's yellow outer eyes. We can hard-code the coordinates because graphics items use their own local logical coordinate system and any externally applied transformations are taken care of automatically for us. If the scene is being shown at 90% of its natural size or larger, we also draw the inner eyes, and if the scene is zoomed in enough to be viewed at 130% or larger, we also draw the multipedes' tiny nostrils.

The last method we must consider is the timeout() method that is called every INTERVAL milliseconds by the timer. We will look at the method in two parts, since there are two aspects to what it does.

```python
def timeout(self):
    if not Running:
        return
    angle = self.angle
    while True:
        angle += random.randint(-9, 9)
        offset += random.randint(3, 15)
        x = self.x() + (offset * math.sin(math.radians(angle)))
        y = self.y() + (offset * math.cos(math.radians(angle)))
        if 0 <= x <= SCENESIZE and 0 <= y <= SCENESIZE:
            break
    self.angle = angle
    self.rotate(random.randint(-5, 5))
    self.setPos(QPoint(x, y))
```

If the global Running Boolean is False, we do nothing and return. Otherwise, we calculate a new position for the head based on a small random change to its angle of direction (±9°), and a small movement (3–15 logical units). To avoid the multipede wandering out of the scene, we keep moving and turning it until its new (x, y) position is within the scene’s boundaries.

Once we have the new coordinates, we record the angle that was used, rotate the head slightly, and set the head’s position. At this point, collisions may have occurred as a result of the movement.

```python
for item in self.scene().collidingItems(self):
    if isinstance(item, Head):
        self.color.setRed(min(255, self.color.red() + 1))
    else:
        item.color.setBlue(min(255, item.color.blue() + 1))
```

We ask the scene for all the items that the head has collided with. If it has hit another head, we make this head a bit redder, and if it has hit a segment, we make the segment it has hit a bit bluer. If a head’s red color component reaches 255, the head (and therefore the entire multipede, including all the segments) will be removed from the scene. The removals take place in the form’s timer event, as we saw earlier (page 372).

Now we will look at the Segment implementation. Its initializer is a bit longer than the Head’s initializer, but the boundingRect(), shape(), and paint() methods are much simpler as a result.

```python
class Segment(QGraphicsItem):
    def __init__(self, color, offset, parent):
        super(Segment, self).__init__(parent)
        self.color = color
        self.rect = QRectF(offset, -20, 30, 40)
        self.path = QPainterPath()
        self.path.addEllipse(self.rect)
        x = offset + 15
        y = -20
        self.path.addPolygon(QPolygonF([QPointF(x, y),
               QPointF(x - 5, y - 12), QPointF(x - 5, y)]))
        self.path.closeSubpath()
        y = 20
        self.path.addPolygon(QPolygonF([QPointF(x, y),
               QPointF(x - 5, y + 12), QPointF(x - 5, y)]))
        self.path.closeSubpath()
        self.change = 1
        self.angle = 0
        self.timer = QTimer()
        QObject.connect(self.timer, SIGNAL("timeout()"), self.timeout)
        self.timer.start(INTERVAL)
```

The first thing to notice is that we accept a parent parameter and pass it on to the base class. We did not do this for the Head because when an item is added to a scene, the scene automatically takes ownership of the item, so there was no need. But segments are not explicitly added to the scene since they are all children of other items. The first segment's parent is the multipede's head, the second segment's parent is the first segment, the third segment's parent is the second segment, and so on. When the head is added to the scene the segments are added too; but the scene takes ownership of only the head. Although we could have given the segments no parent and added them directly to the scene, it is much more convenient to make them child items. In particular, the parent-child relationship between graphics items is used to propagate transformations from parent to child.

The offset is an x offset relative to the head, no matter which segment we are initializing. The rectangle is used to draw the segment's ellipse, but unlike the head, it does not encompass the entire shape because segments have protruding legs. Because the segment's shape isn't simple, we create it using a painter path. We begin with the segment's "body", a simple ellipse. Then we draw one leg (a very flat triangle), and then the other leg. The addPolygon() method takes a QPolygonF(), which itself is constructed with a list of QPointF objects. After each leg is added, we call closeSubpath(); alternatively, we could simply have added an extra point at the end, a copy of the first point. The change and angle instance variables are used for movement; we will cover them in the time-out() event.

```python
def boundingRect(self):
    return self.path.boundingRect()
```

The bounding rectangle must account for the entire shape, including the legs, but it is easy to obtain using QPainterPath.boundingRect().

```python
def shape(self):
    return self.path
```

The shape isn’t straightforward, but thanks to the path being calculated in the initializer, this method is simple.

```python
def paint(self, painter, option, widget=None):
    painter.setPen(Qt.NoPen)
    painter.setBrush(QBrush(self.color))
    if option.levelOfDetail < 0.9:
        painter.drawEllipse(self.rect)
    else:
        painter.drawPath(self.path)
```

Thanks to precalculating the rectangle and painter path, the paint() method is much easier and faster than it would otherwise have been. If the scene is zoomed in to 90% or less, we just draw an ellipse; otherwise, we draw the shape in full detail using the painter path.

```python
def timeout(self):
    if not Running:
        return

    matrix = self.matrix()
    matrix.reset()
    self.setMatrix(matrix)

    self.angle += self.change

    if self.angle > 5:
        self.change = -1
        self.angle = 5
    elif self.angle < -5:
        self.change = 1
        self.angle = -5

    self.rotate(self.angle)
```

When a multipede’s head moves, its first (child) segment moves with it, and that segment’s child segment moves with it, and so on. This is fine, but it means that the multipede’s shape is rigid. We want the segments to gently sway from side to side as the multipede moves, and for this reason we have given the segments their own timers.

We retrieve the segment’s transformation matrix, clear any transformations (rotations) that have been applied, and then rotate the segment. The change variable starts out as 1 and the rotation angle starts out at 0°. At every time interval, the change is added to the angle. If the angle reaches 6 (or -6), we make it 5 (or -5) and negate the change value. This means that the angle has
