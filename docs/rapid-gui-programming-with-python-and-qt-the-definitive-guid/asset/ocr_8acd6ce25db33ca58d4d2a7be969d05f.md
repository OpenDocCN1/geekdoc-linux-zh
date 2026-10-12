```
self.connect(lineEdit, SIGNAL("textEdited(QString)"),
            self.updateUi)
```

The preceding code is from the form's initializer. It adds a "mandatory" property to those line edits that we do not want the user to be able to leave blank. All Qt properties are held as QVariants. The signal-sIot connections are discussed shortly.

We have created a style sheet for the widget as a class static variable, and set it on the form toward the end of the constructor. We could just as easily have read the style sheet from a file (since it is simply plain text), or from a PyQt resource.

```
StyleSheet = ""
    QComboBox { color: darkblue; }
    QLineEdit { color: darkgreen; }
    QLineEdit[mandatory="true"] {
        backgrround-color: rgb(255, 255, 127);
        color: darkblue;
    }
    """
...
self.setStyleSheet(ContactDlg.StyleSheet)
```

The style sheet syntax essentially consists of "selectors" and property name: value pairs. In the preceding snippet, the first line has a selector of QComboBox, which means that its property values will apply to any QComboBox or QComboBox subclass that is a child of the widget on which the style sheet is set. In this case, the effect is to set the text color to dark blue. The second selector is a QLineEdit, and this works similarly.

The third selector is more specific: It specifies both a class, and a property of that class whose state must be matched. In other words, this third selector will apply only to QLineEdit and QLineEdit subclasses that have a "mandatory" property, and where that property's value is True. For such cases, the background color is set to yellow (specified as an RGB triple), and the text color is set to dark blue.

The dialog is slightly subtler than it may at first appear. This is because the company line edit is mandatory only if the category combobox is set to "Business". To achieve this we need the signal-sIot connections shown earlier, and one other connection:

```
self.connect(self.f.categoryComboBox, SIGNAL("activated(int)"),
            self.updateUi)
```

All the connections are to the updateUi() method: