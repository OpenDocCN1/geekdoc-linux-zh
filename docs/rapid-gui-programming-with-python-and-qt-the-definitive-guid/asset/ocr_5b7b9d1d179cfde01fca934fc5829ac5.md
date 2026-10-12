can access its `QLabel` as `LabelledLineEdit.label` and its `QLineEdit` as `LabelledLineEdit.lineEdit`. The `LabelledTextEdit` has the same `label`, and has a `textEdit` for its `QTextEdit`. The `ABOVE` is just a module constant; there is also a corresponding `LEFT`.

```
```python
class LabelledLineEdit(QWidget):
    def __init__(self, labelText=QString()), position=LEFT,
                 parent=None):
        super(LabelledLineEdit, self).__init__(parent)
        self.label = QLabel(labelText)
        self.lineEdit = QLineEdit()
        self.label.setBuddy(self.lineEdit)
        layout = QBoxLayout(QBoxLayout.LeftToRight \\
            if position == LEFT else QBoxLayout.TopToBottom)
        layout.addWidget(self.label)
        layout.addWidget(self.lineEdit)
        self.setLayout(layout)
```
```

The preceding code is the complete `LabelledLineEdit` class. If we want to connect signals and slots to its `label` or `lineEdit`, we can do so by accessing them directly since they are held as public instance variables. Instead of using a `QBoxLayout` or a `QHBoxLayout`, we have used their base class so that we can set the layout direction when the labelled line edit is created. We won't show the code for the `LabelledTextEdit` since it differs only in that we create a `QTextEdit` instead of a `QLineEdit` and call it `textEdit` instead of `lineEdit`.

Although we have created the composite labelled editing widgets purely in code, it is possible to create composite widgets using **Qt Designer**, basing them on the “Widget” template.

Creating composite widgets that are used repeatedly can save time in large projects. They are also useful when we want to create a main-window-style application whose central widget must consist of two or more widgets, and where using an MDI workspace, splitters, or dock windows is not a suitable solution.

# ## Subclassing Built-in Widgets

Sometimes we need a widget that is similar in appearance and behavior to an existing widget, but with more customization required than can be achieved by using a style sheet or by setting other widget properties.* In these cases, we can subclass the similar widget and customize it to our needs.*

To show how to subclass an existing widget, let us imagine that we need a spinbox that works on Roman numerals rather than on decimals, like the one shown in Figure 11.3. Providing we know how to convert integers to Roman

> \*Appendix B provides screenshots and brief descriptions of selected PyQt widgets, and Appendix C shows selected PyQt class hierarchies.