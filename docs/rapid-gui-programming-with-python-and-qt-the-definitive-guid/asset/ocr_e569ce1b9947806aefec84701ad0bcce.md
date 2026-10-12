This method is the default one used for collision detection, unless we specify a coarser-grained approach that uses just the bounding rectangle. A painter path is a series of rectangles, ellipses, arcs, and other shapes (including painter paths) that together completely describe an item's shape. In this case, the path is just one ellipse.

Using a painter path for a graphics item's shape ensures that collisions are detected accurately. For example, two multipede heads may cross at the corners of their rectangles without colliding, since their ellipses don't occupy the corners.

```
```
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
```

The head in full detail is an ellipse, two eyes, each of which is two ellipses, one inside the other, and two tiny nostrils, again ellipses. The paint() method begins by getting rid of the pen and by setting a solid brush to the multipede's color. Then the basic head shape is drawn.

The option variable is of type QStyleOptionGraphicsItem, and it holds various useful information, including the item's transformation matrix, font metrics, palette, and state (selected, "on", "off", and many others). It also holds the "level of detail", a measure of how zoomed in or out the scene is. If the scene is not zoomed at all, the level of detail is 1.0; if it is zoomed in to twice the size, the level of detail will be 2.0, and if it is zoomed out to half the size, the level of detail will be 0.5.

If the scene is being shown at 50% of its natural size or larger, we draw the multipede's yellow outer eyes. We can hard-code the coordinates because graphics items use their own local logical coordinate system and any externally applied transformations are taken care of automatically for us. If the scene is being show at 90% of its natural size or larger, we also draw the inner eyes, and if the scene is zoomed in enough to be viewed at 130% or larger, we also draw the multipedes' tiny nostrils.