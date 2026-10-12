![](bbox=[0.45, 0.1, 0.55, 0.13])

**Figure 6.5** *The File toolbar*

With the menus in place, we can now turn to the toolbars.

```
```python
fileToolBar = self.addToolBar("File")
fileToolBar.setObjectName("FileToolBar")
self.addActions(fileToolBar, (fileNewAction, fileOpenAction, fileSaveAction))
```

```

Creating a toolbar is similar to creating a menu: We call addToolBar() to create a QToolBar object and populate it using addActions(). We can use our addActions() method for both menus and toolbars because their APIs are very similar, with both providing addAction() and addSeparator() methods. We set an object name so that PyQt can save and restore the toolbar's position—there can be any number of toolbars and PyQt uses the object name to distinguish between them, just as it does for dock widgets. The resulting toolbar is shown in Figure 6.5.

The edit toolbar and the checkable actions (“edit invert”, “edit swap red and blue”, and the mirror actions) are all created in the same way. But as Figure 6.6 shows, the edit toolbar has a spinbox in addition to its toolbar buttons. In view of this, we will show the code for this toolbar in full, showing it in two parts for ease of explanation.

```
```python
editToolBar = self.addToolBar("Edit")
editToolBar.setObjectName("EditToolBar")
self.addActions(editToolBar, (editInvertAction,
    editSwapRedAndBlueAction, editUnMirrorAction,
    editMirrorVerticalAction,
    editMirrorHorizontalAction))
```

```

Creating a toolbar and adding actions to it is the same for all toolbars.

We want to provide the user with a quick means of changing the zoom factor, so we provide a spinbox in the edit toolbar to make this possible. Earlier, we put a separate “edit zoom” action in the Edit menu, to cater to keyboard users.

```
```python
self.zoomSpinBox = QSpinBox()
self.zoomSpinBox.setRange(1, 400)
self.zoomSpinBox.setSuffix(" %")
self.zoomSpinBox.setValue(100)
self.zoomSpinBox.setToolTip("Zoom the image")
self.zoomSpinBox.setStatusTip(self.zoomSpinBox.toolTip())
self.zoomSpinBox.setFocusPolicy(Qt.NoFocus)
self.connect(self.zoomSpinBox,
    SIGNAL("valueChanged(int)"), self.showImage)
editToolBar.addWidget(self.zoomSpinBox)
```

```