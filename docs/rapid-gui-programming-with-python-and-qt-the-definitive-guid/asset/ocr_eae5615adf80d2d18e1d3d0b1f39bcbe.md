# Example: A Flow-Mixing Widget

It is sometimes appropriate to create custom widgets for particular applications. For this example, we will assume that we have an application in which we are modeling the flow of fluid through a “Y”-shaped pipe, as depicted in Figure 11.6.

![](bbox=[0.25, 0.22, 0.75, 0.54])

Figure 11.6 A YPipe widget

The widget must draw three gradient-filled polygons and three black outlines (to give a clear border to the pipe shapes), and must allow the user to set the left and right flows, as well as show the combined flow. We have chosen to provide spinboxes for the user to set the flows and to use a label to show the resultant flow. The advantages of using these built-in widgets include that we need concern ourselves only with their positioning and connections; we can leave PyQt to provide mouse and keyboard interaction and to display them properly. An-other benefit is that we can paint our custom widget using a “window”, that is, using logical rather than device (viewport) coordinates, and do not have to worry about scaled text because the text appears only in widgets that are overlaid on top of the custom widget, and are not affected by the window settings.

We will start by looking at the initializer, taking it in two parts.

```
class YPipeWidget(QWidget):
    def __init__(self, leftFlow=0, rightFlow=0, maxFlow=100, parent=None):
        super(YPipeWidget, self).__init__(parent)

        self.leftSpinBox = QSpinBox(self)
        self.leftSpinBox.setRange(0, maxFlow)
        self.leftSpinBox.setValue(leftFlow)
        self.leftSpinBox.setSuffix(" l/s")
```