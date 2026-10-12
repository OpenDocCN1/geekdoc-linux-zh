The first import is the regular expression module that we will use in the code. The second and third imports are the usual ones for PyQt programming. The last import is of the generated user interface module. Now we can look at our subclass.

```
```
class FindAndReplaceDlg(QDialog,
                         ui_findandreplacedlg.Ui_FindAndReplaceDlg):
    def __init__(self, text, parent=None):
        super(FindAndReplaceDlg, self).__init__(parent)
        self._text = unicode(text)
        self._index = 0
        self.setupUi(self)
        if not MAC:
            self.findButton.setFocusPolicy(Qt.NoFocus)
            self.replaceButton.setFocusPolicy(Qt.NoFocus)
            self.replaceAllButton.setFocusPolicy(Qt.NoFocus)
            self.closeButton.setFocusPolicy(Qt.NoFocus)
            self.updateUi()
```
```

We inherit from both `QDialog` and from `ui_findAndReplaceDlg`. We rarely need to use multiple inheritance in Python programming, but for this situation it makes things much easier than would otherwise be the case. Our FindAndReplaceDlg subclass is, in effect, the union of the two classes it inherits from, and can access their attributes directly, prefixed with `self`, of course.

We have set our initializer to accept text that is the data the dialog will work on, and a parent widget. The `super()` call is made on the first inherited class, `QDialog`. We keep a copy of the text, and also an index position, in case the user clicks Find more than once to find subsequent occurrences of the same text.

The call to the `setupUi()` method is something we have not seen before. This method is provided by the generated module. When called it creates all the widgets specified in the user interface file, lays them out according to our design, sets their buddies and tab order, and makes the connections we set. In other words, it re-creates the form we designed in *Qt Designer*.

In addition, the `setupUi()` method calls `QtCore.QObject.connectSlotsByName()`, a static method that creates signal-slot connections between form widget signals and methods in our subclass that follow a particular naming convention. Any method whose name is of the form on_widgetName_signalName will have the named widget's named signal connected to it.

For example, our form has a widget called findLineEdit of type `QLineEdit`. One of the signals emitted by a `QLineEdit` is `textEdited(QString)`. So, if we want to connect this signal, without calling the `connect()` method in the initializer, we can leave the job to `setupUi()`. This will work as long as we call the slot we want the signal to connect to, on_findLineEdit_textEdited. This is the approach we have used for all the connections in the form, apart from the Close button's `clicked()` signal that we connected visually in *Qt Designer*.