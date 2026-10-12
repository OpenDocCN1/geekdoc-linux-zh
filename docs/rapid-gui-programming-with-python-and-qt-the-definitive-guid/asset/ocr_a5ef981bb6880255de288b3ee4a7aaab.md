# Dialog Button Layout

In some of our early examples, we have put the buttons on the right of the dialogs, with the OK button first and then the Cancel button next. This is the most common layout on Windows, but it is not always correct. For example, for Mac OSX or for the GNOME desktop environment, they should be swapped.

If we want our applications to have the most native look and feel possible and expect to deploy them on different platforms, issues like button ordering and positioning will matter to us. Qt 4.2 (PyQt 4.1) provides a solution for this particular problem: the QDialogButtonBox class.

Instead of creating OK and Cancel buttons directly, we create a QDialogButtonBox. For example:

```
buttonBox = QDialogButtonBox(QDialogButtonBox.Ok | QDialogButtonBox.Cancel)
```

To make a button the “default” button, that is, the one that is pressed when the user presses Enter (assuming that the widget with keyboard focus does not handle Enter key presses itself), we can do this:

```
buttonBox.button(QDialogButtonBox.Ok).setDefault(True)
```

Since a button box is a single widget (although it contains other widgets), we can add it directly to the dialog’s existing layout, rather than putting it in its own layout and nesting that inside the dialog’s layout. Here is what we would do in the PenPropertiesDlg example’s grid layout:

```
layout.addWidget(buttonBox, 3, 0, 1, 3)
```

And instead of connecting from the buttons’ clicked() signals, we can make connections from the button box, which has its own signals that correspond to user actions:

```
self.connect(buttonBox, SIGNAL("accepted()"), self, SLOT("accept()")) 
self.connect(buttonBox, SIGNAL("rejected()"), self, SLOT("reject()"))
```

We are still free to connect to individual buttons’ clicked() signals, though, and often do so for dialogs that have many buttons.

The QDialogButtonBox defaults to using a horizontal layout, but can be set to use a vertical layout by passing Qt.Vertical to its constructor, or by calling setOrientation().

We use QDialogButtonBox for most of the examples, but it could always be replaced by individual QPushButtons if backward compatibility was an issue.

![](bbox=[0.9, 0.22, 0.97, 0.28])

![](bbox=[0.9, 0.29, 0.97, 0.35])