# *Subclassing QWidget*

We create a QPainter and set its render hints to give us antialiased drawing. Then we set the pen (which is used for shape outlines and for drawing text) and the brush (which is used for fills), and draw a rectangle over the entire widget. Because we used different shades for the pen and brush, this has the effect of giving the widget a border and a slightly contoured look.

The QApplication object has a QPalette that contains colors for various purposes, such as text foreground and background colors, button colors, and so on. The colors are identified by their roles, such as QPalette.Text or QPalette.Highlight, although we have used rather more obscure roles in this example. There are, in fact, three sets of these colors, one for each of the widget states: “active”, “disabled”, and “inactive”. Every QWidget also has a QPalette, with colors inherited from the QApplication palette—which in turn is initialized with colors from the underlying window system and therefore reflects the user’s preferences. PyQt tries very hard to ensure that the colors in a palette work well together, providing good contrast, for example. As programmers, we are free to use whatever colors we like, but especially for standard requirements such as text colors and backgrounds, it is best to use the palette.

```
```
segColor = QColor(Qt.green).dark(120)
segLineColor = segColor.dark()
painter.setPen(segLineColor)
painter.setBrush(segColor)
painter.drawRect(FractionSlider.XMARGIN,
                 FractionSlider.YMARGIN, span, fm.height())
```
```

We create a dark green color for the segments, and an even darker green for the vertical lines that mark them out. Then we draw a rectangle that encompasses all the segments.

```
```
textColor = self.palette().color(QPalette.Text)
segWidth = span / self.__denominator
segHeight = fm.height() * 2
nRect = fm.boundingRect(FractionSlider.WSTRING)
x = FractionSlider.XMARGIN
yOffset = segHeight + fm.height()
```
```

Here, we set the text color to use based on the user's palette. Then we work out the width and height of each segment, and set an initial x position and a yOffset. The nRect is a rectangle large enough to contain a number with some left and right margin space.

```
```
for i in range(self.__denominator + 1):
    painter.setPen(segLineColor)
    painter.drawLine(x, FractionSlider.YMARGIN, x, segHeight)
    painter.setPen(textColor)
    y = segHeight
    rect = QRectF(nRect)
```
```