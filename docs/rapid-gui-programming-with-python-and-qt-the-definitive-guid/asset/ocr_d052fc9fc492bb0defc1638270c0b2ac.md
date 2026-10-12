```
color = QColor(int(255 * temperature / 100), 0, 0)
else:
    color = QColor(0, int(255 * temperature / 100), 0)
painter.setPen(Qt.NoPen)
painter.setBrush(color)
painter.drawEllipse(x, y + offset, indicatorSize,
                     indicatorSize)

x += size
```

We iterate over every row in the model, but paint only those with a *y* coordinate that is in range. Once we have a row to paint, we set the pen (used for drawing text) to the palette’s text color. If the row is selected (something we will explain after covering the paint event), we paint the background in the palette’s highlight color and set the pen to the palette’s highlighted text color.

Having set up the text color, and possibly painted the background, we then retrieve and draw the row’s timestamp. For each row we keep an *x* coordinate that tells us how far across we are, and that we increment by the font metrics timestamp width we calculated earlier.

The first colored circle is used to indicate the water’s temperature in °C. If the water is too cool we use a color with a blue tint; if it is too warm we use a color with a red tint; otherwise, we use a green tint. Then we switch off the pen and set the brush to the color we have set up and paint an ellipse to the right of the timestamp. The drawEllipse() method will draw a circle because the width and height of the rectangle in which the ellipse is drawn are the same.

We then increment the *x* coordinate. Now we repeat the process for the other two colored circle indicators, using the same tinting approach we used for temperature. We have omitted the code for these, since it is structurally identical to the code used for the temperature circle.

```
flow = self.model.data(
                    self.model.index(row, INLETFLOW))
flow = flow.toDouble()[0]
char = None
if flow <= 0:
    char = WaterQualityView.FLOWCHARS[0]
elif flow < 3:
    char = WaterQualityView.FLOWCHARS[1]
elif flow > 5.5:
    char = WaterQualityView.FLOWCHARS[2]
if char is not None:
    painter.setFont(self.flowfont)
    painter.drawText(x, y + size, char)

painter.restore()

y += size
if y > maxy:
    break
```