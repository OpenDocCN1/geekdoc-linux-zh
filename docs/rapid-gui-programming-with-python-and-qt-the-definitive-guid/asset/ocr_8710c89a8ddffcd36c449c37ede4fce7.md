```
```python
        else:
            self.key = "PageDown"
        elif Qt.Key.A <= event.key() <= Qt.Key.Z:
            if event.modifiers() & Qt.ShiftModifier:
                self.key = "Shift+"
                self.key += event.text()
        if self.key:
            self.key = QString(self.key)
            self.update()
        else:
            QWidget.keyPressEvent(self, event)
```
```

If the user presses a key, we are informed through the keyPressEvent(). There is also a corresponding keyReleaseEvent(), but that is rarely reimplemented. The QKeyEvent parameter provides several useful methods, including key(), which returns the key code for the key that was pressed, and modifiers(), which returns a bit flag indicating the state of the Shift, Ctrl, and Alt keys.

We have chosen to handle the Home, End, PageUp, Ctrl+PageUp, PageDown, and Ctrl+PageDown key sequences, and the alphabetic keys A...Z as well as Shift+A...Shift+Z. We store a textual representation of what was pressed in the key variable and call update() to schedule a paint event. If the user pressed a key that we do not handle, we pass on the key press to the base class implementation, a practice that is common when handling key events.

```
```python
    def contextMenuEvent(self, event):
        menu = QMenu(self)
        oneAction = menu.addAction("\"One\"")
        twoAction = menu.addAction("\"Two\"")
        self.connect(oneAction, SIGNAL("triggered()"), self.one)
        self.connect(twoAction, SIGNAL("triggered()"), self.two)
        if not self.message:
            menu.addSeparator()
            threeAction = menu.addAction("\"Three\"")
            self.connect(threeAction, SIGNAL("triggered()"),
                        self.three)
        menu.exec_(event.glo\t\tb\ta\tl\tPos())
```
```

The easiest way to create a context menu is to add actions to a widget using QWidget.addAction(), and to set the widget's context menu policy to Qt.Actions\u2013ContextMenu; we saw how this was done in Chapter 6 on page 180. But if we want fine control over what happens as a result of a context menu event\u2014for example, offering different options depending on the application's state\u2014we can reimplement the context menu event handler as we have done here.

The globalPos() method returns the mouse position at the time the context menu was invoked; we pass the position to QMenu.exec\u2009() to ensure that the menu is popped up where the user expects it.