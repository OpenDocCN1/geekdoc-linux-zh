
self.setMinimumHeight(h)
self.setMaximumHeight(int(h * 1.2))
self.setToolTip("Press <b>Ctrl+4K</b> for the text effects "
                "menu and <b>Ctrl+K</b> for the color menu")

We begin by setting some default font families. Nowadays, every platform can be expected to provide Courier, Helvetica, and Times fonts (or fonts for which these names are aliases). Since the widget is a single line, we switch off line wrapping and scrollbars. We also ensure that Tab causes a change of focus rather than the insertion of a Tab character. Calculating a minimum and maximum height will help when we implement the size hint methods, but it is complicated slightly by differences in font metrics across platforms. The tooltip is there to give users a hint that the widget has some special key presses.

Notice that the conditional expression is enclosed in parentheses. They are essential in this case, since without them, on non-Windows platforms, h would always be set to 1 instead of the 20 or 30 or so that we would expect.

```python
def sizeHint(self):
    return QSize(self.document().idealWidth() + 5,
                 self.maximumHeight())
```

The preferred size is the "ideal" width of the text (taking into account font sizes and attributes like bold and italic), with a bit of padding to give a little margin, and the maximum height. The QTextDocument.idealWidth() method was introduced with Qt 4.2.

```python
def minimumSizeHint(self):
    fm = QFontMetrics(self.font())
    return QSize(fm.width("WWWW"), self.minimumHeight())
```

For the minimum size, we take the width of four "W" characters in the widget's default font. Alternatively, we could have simply used an arbitrary amount, say, 40 pixels.

One thing that distinguishes the RichTextLineEdit from a QLineEdit is the user's ability to change the format and color of words and characters. To support this we must provide some means by which the user can apply such changes. We have done this by providing a text effects menu and a color menu, and by supporting some key sequences for formatting. Both menus are invoked by particular key sequences, and the text effects menu is also popped up when a context menu event occurs.

```python
def contextMenuEvent(self, event):
    self.textEffectMenu()
```

A context menu event occurs when the user right-clicks on some platforms, or presses a particular key or key sequence on others. In this case, we simply call the custom textEffectMenu() method, which will pop up a suitable menu. By default, QTextEdit provides its own context menu, but by reimplementing the context menu event handler, our code takes precedence.

```python
def keyPressEvent(self, event):
    if event.modifiers() & Qt.ControlModifier:
        handled = False
        if event.key() == Qt.Key_B:
            self.toggleBold()
            handled = True
        elif event.key() == Qt.Key_I:
            self.toggleItalic()
            handled = True
        elif event.key() == Qt.Key_K:
            self.colorMenu()
            handled = True
        elif event.key() == Qt.Key_M:
            self.textEffectMenu()
            handled = True
        elif event.key() == Qt.Key_U:
            self.toggleUnderline()
            handled = True
        if handled:
            event.accept()
            return
        if event.key() in (Qt.Key_Enter, Qt.Key_Return):
            self.emit(SIGNAL("returnPressed()"))
            event.accept()
        else:
            QTextEdit.keyPressEvent(self, event)
```

Since users are typing in text, it is natural to provide a keyboard interface for changing the text's format. We have set Ctrl+B to toggle bold, Ctrl+I to toggle italic, and Ctrl+U to toggle underlining. In addition, Ctrl+K invokes the color menu, and Ctrl+M invokes the text effects menu (in addition to being invoked by a context menu event). By calling accept() on the key presses we handle ourselves, we are indicating that no further event handling of these key presses is necessary.

If the user presses Return we emit a returnPressed() signal since this can be useful; no newline is inserted into the text. Any other key presses are passed on to the base class. The QTextEdit class supports its own key sequences—for example, Ctrl+Left Arrow for move left one word, Ctrl+Del for delete the word to the right, Ctrl+C to copy any selected text to the clipboard, and, of course, simple letters, such as a, b, Shift+A, and Shift+B, that are inserted literally.

```python
def toggleBold(self):
    self.setFontWeight(QFont.Normal \
if self.fontWeight() > QFont.Normal else QFont.Bold)
```

PyQt supports several levels of boldness, but we have chosen to take a simple bold on or off approach. The `QTextEdit.fontWeight()` method returns the font weight at the current insertion point, and similarly the `setFontWeight()` method is applied at the current insertion point or to the selected text. The `QTextEdit` is quite smart about formatting, at least on Linux. For example, if text is selected the formatting is applied only to the selection, whereas if there is no selection and the insertion point is at the end of the text, the formatting is applied from that point onward, and if there is no selection and the insertion point is in the middle of a word the formatting is applied to the whole word.

```python
def toggleItalic(self): 
    self.setFontItalic(not self.fontItalic())

def toggleUnderline(self): 
    self.setFontUnderline(not self.fontUnderline())
```

Both *italic* and *underline* are simple on/off settings, and on Linux, toggling them works in the same smart way as applying bold or other formatting.

```python
def colorMenu(self): 
    pixmap = QPixmap(22, 22) 
    menu = QMenu("Color") 
    for text, color in (("$Black", Qt.black), ("$Blue", Qt.blue), 
                        ("$Dark Blue", Qt.darkBlue), ("$Cyan", Qt.cyan), 
                        ("$Dark Cyan", Qt.darkCyan), ("$Green", Qt.green), 
                        ("$Dark Green", Qt.darkGreen), 
                        ("$Magenta", Qt.magenta), 
                        ("$Dark Magenta", Qt.darkMagenta), 
                        ("$Red", Qt.red), ("$Dark Red", Qt.darkRed)): 
        color = QColor(color) 
        pixmap.fill(color) 
        action = menu.addAction(QIcon(pixmap), text, self.setColor) 
        action.setData(QVariant(color)) 
    self.ensureCursorVisible() 
    menu.exec_(self.viewport(), mapToGlobal(self.cursorRect().center())) 
```

The color menu is invoked by Ctrl+K. To create the menu we iterate over a list of text and color constants, adding a new menu option for each one. We set the data for each action to the relevant color; we use this in the `setColor()` implementation.

We want the menu to pop up at the insertion point, that is, at the text cursor position. This is not necessarily straightforward, because it is possible for the RichTextLineEdit to have more text than it is wide enough to show, and the insertion point could be outside the visible area.

We solve this problem by doing two things. First, we call the base class's `QTextEdit.ensureCursorVisible()` method; this has the effect of scrolling the editor so that the insertion point is in the visible area—and it does nothing if the insertion point is already visible. Second, we pop up the menu at the center of the insertion point's rectangle. The `cursorRect()` method returns a `QRect` that is in widget coordinates, so we must convert the coordinates of the `QPoint` we get from `QRect.center()` accordingly. We do this by calling `viewport()`, which effectively returns a widget that has the exact dimensions of the visible area, and that knows what region of the editor it represents. We then use the viewport widget's `mapToGlobal()` method to convert the point from the widget coordinate system to the global (screen) coordinate system that is used by `QMenu.exec_()` to position itself.

```python
def setColor(self):
    action = self.sender()
    if action is not None and isinstance(action, QAction):
        color = QColor(action.data())
        if color.isValid():
            self.setTextColor(color)
```

If the user chooses a color the `setColor()` method is called. We retrieve the color that was stored in the calling action's user data, and apply that color to the text. Again, the same logic used for *bold*, *italic*, and underlining is used to apply the color to the selected text, or to the current word, or from the end of the text onward.

```python
def textEffectMenu(self):
    format = self.currentCharFormat()
    menu = QMenu("Text Effect")
    for text, shortcut, data, checked in (
        ("$Bold", "Ctrl+B", RichTextLineEdit.Bold,
         self.fontWeight() > QFont.Normal),
        ("$Italic", "Ctrl+I", RichTextLineEdit.Italic,
         self.fontItalic()),
        ...
        ("$Subscript", None, RichTextLineEdit.Subscript,
         format.verticalAlignment() == \
         QTextCharFormat.AlignSubScript),
    ):
        action = menu.addAction(text, self.setTextEffect)
        if shortcut is not None:
            action.setShortcut(QKeySequence(shortcut))
        action.setData(QVariant(data))
        action.setCheckable(True)
        action.setChecked(checked)
    self.ensureCursorVisible()
    menu.exec_(self.viewport().mapToGlobal(
        self.cursorRect().center()))
```

The text effects menu method, invoked by `Ctrl+M` or by a context menu event, is similar in structure to the color menu method, but slightly more involved.
