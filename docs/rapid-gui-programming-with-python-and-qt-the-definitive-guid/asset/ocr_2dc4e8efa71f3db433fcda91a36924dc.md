```
def setNewSize(self):  
    self.resize(self.sizeHint())  
    self.update()  
    self.updateGeometry()
```

This method resizes the view to its preferred size and calls update( ) to schedule a repaint and updateGeometry( ) to tell any layout manager that is responsible for the view that its size has changed. Because we put the view in a QScrollArea, the scroll area will respond to changes in size by adjusting the scrollbars it provides.

```
def minimumSizeHint(self):  
    size = self.sizeHint()  
    fm = QFontMetrics(self.font())  
    size.setHeight(fm.height() * 3)  
    return size
```

We calculate the view’s minimum size to be its preferred size’s width and three characters in height. In a layout this makes sense, but since a QScrollArea is used, the minimum size will, in practice, be whatever the scroll area decides.

```
def sizeHint(self):  
    fm = QFontMetrics(self.font())  
    size = fm.height()  
    return QSize(fm.width("9999-99-99 99:99 ") + (size * 4),  
               (size / 4) + (size * self.model.rowCount()))
```

We use the height of one character (including its interline spacing) as our unit of size for both vertical and horizontal measurements. The view’s preferred size is wide enough to show a timestamp plus four units of size to allow for the colored circles and the flow character, and it’s tall enough for all the rows in the model plus one-quarter of the unit of size to allow a tiny bit of margin.

The paint event isn’t too difficult, but we will look at it in three parts, and show the code for only one colored circle since the code for all three is almost identical.

```
def paintEvent(self, event):  
    if self.model is None:  
        return  
    fm = QFontMetrics(self.font())  
    timestampWidth = fm.width("9999-99-99 99:99 ")  
    size = fm.height()  
    indicatorSize = int(size * 0.8)  
    offset = int(1.5 * (size - indicatorSize))  
    minY = event.rect().y()  
    maxY = minY + event.rect().height() + size  
    minY -= size  
    painter = QPainter(self)
```