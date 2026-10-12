```
self.setMinimumHeight(h)
self.setMaximumHeight(int(h * 1.2))
self.setToolTip("Press <b>Ctrl+4K</b> for the text effects "
                "menu and <b>Ctrl+K</b> for the color menu")
```

We begin by setting some default font families. Nowadays, every platform can be expected to provide Courier, Helvetica, and Times fonts (or fonts for which these names are aliases). Since the widget is a single line, we switch off line wrapping and scrollbars. We also ensure that Tab causes a change of focus rather than the insertion of a Tab character. Calculating a minimum and maximum height will help when we implement the size hint methods, but it is complicated slightly by differences in font metrics across platforms. The tooltip is there to give users a hint that the widget has some special key presses.

Notice that the conditional expression is enclosed in parentheses. They are essential in this case, since without them, on non-Windows platforms, h would always be set to 1 instead of the 20 or 30 or so that we would expect.

```
def sizeHint(self):
    return QSize(self.document().idealWidth() + 5,
                 self.maximumHeight())
```

The preferred size is the "ideal" width of the text (taking into account font sizes and attributes like bold and italic), with a bit of padding to give a little margin, and the maximum height. The QTextDocument.idealWidth() method was introduced with Qt 4.2.

```
def minimumSizeHint(self):
    fm = QFontMetrics(self.font())
    return QSize(fm.width("WWWW"), self.minimumHeight())
```

For the minimum size, we take the width of four "W" characters in the widget's default font. Alternatively, we could have simply used an arbitrary amount, say, 40 pixels.

One thing that distinguishes the RichTextLineEdit from a QLineEdit is the user's ability to change the format and color of words and characters. To support this we must provide some means by which the user can apply such changes. We have done this by providing a text effects menu and a color menu, and by supporting some key sequences for formatting. Both menus are invoked by particular key sequences, and the text effects menu is also popped up when a context menu event occurs.

```
def contextMenuEvent(self, event):
    self.textEffectMenu()
```

A context menu event occurs when the user right-clicks on some platforms, or presses a particular key or key sequence on others. In this case, we simply call the custom textEffectMenu() method, which will pop up a suitable menu. By