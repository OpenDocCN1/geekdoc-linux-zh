```
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

```
def boundingRect(self):
    return self.path.boundingRect()
```