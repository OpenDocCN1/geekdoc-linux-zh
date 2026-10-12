# Table 11.2 Selected QPainter Methods (Excluding Drawing-Related Methods)

| Syntax | Description |
| --- | --- |
| p.restore() | Restores QPainter p's state to the last saved state |
| p.rotate(a) | Rotates QPainter p by int a° |
| p.save() | Saves QPainter p's state, including its transformation matrix, pen, and brush |
| p.scale(x, y) | Scales QPainter p horizontally by float x and vertically by float y; 1.0 is unscaled, 0.5 is half size, 3.0 is three times the size |
| p.setMatrix(m) | Sets QPainter p's transformation matrix to QMatrix m |
| p.setRenderHint(h) | Turns on the QPainter.RenderHint h. Hints include QPainter.Antialiasing, QPainter.TextAntialiasing, and QPainter.SmoothPixmapTransform. |
| p.setViewport(x, y, w, h) | Constrains QPainter p's viewport (physical coordinates) to the rectangle with top-left corner at point (x, y), and with width w and height h; all the arguments are ints |
| p.setWindow(x, y, w, h) | Sets QPainter p's logical coordinate system to the rectangle with top-left corner at point (x, y), and with width w and height h; all the arguments are ints |
| p.shear(x, y) | Shears QPainter p's coordinate system horizontally by float x and vertically by float y |
| p.translate(dx, dy) | Moves QPainter p's coordinate system horizontally by int dx and vertically by int dy |

We turn off the pen because we do not want an outline around the polygons we will draw for each part of the pipe. Instead, we will draw in the lines we want at the end of the paint event.

```
gradient = QLinearGradient(QPointF(0, 0), QPointF(0, 100))
gradient.setColorAt(0, Qt.white)
a = self.leftSpinBox.value()
gradient.setColorAt(1, Qt.red if a != 0 else Qt.white)
painter.setBrush(QBrush(gradient))
painter.drawPolygon(
    QPolygon([(ax, ay, bx, by, cx, cy, ix, iy)]))
```

For the left part of the “Y” shape representing the left spinbox—the shape (a, b, c, i)—we use a linear color gradient going from white to red.

```
gradient = QLinearGradient(QPointF(0, 0), QPointF(0, 100))
gradient.setColorAt(0, Qt.white)
b = self.rightSpinBox.value()
gradient.setColorAt(1, Qt.blue if b != 0 else Qt.white)
```