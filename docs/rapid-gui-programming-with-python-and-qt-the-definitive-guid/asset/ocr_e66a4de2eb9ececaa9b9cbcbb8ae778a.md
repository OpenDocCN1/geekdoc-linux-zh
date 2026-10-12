```
self.editor = QTextEdit()
self.setCentralWidget(self.editor)
```

The QTextEdit is the ideal widget for our central widget, with some actions being able to be passed directly to it, as we will see in a moment. We will now look at just a few of the actions, skipping the createAction() method that we have seen before.

```
fileSaveAllAction = self.createAction("Save All",
self.fileSaveAll, icon="filesave",
tip="Save all the files")
```

This action is similar to almost all the other file actions, with a connection to one of the MainWindow subclass's methods.

```
fileCloseAction = self.createAction("&Close", self.close,
QKeySequence.Close, "fileclose",
"Close this text editor")
```

The "close" action is similar to those we have seen before. As usual, we do not reimplement the close() method, but instead reimplement the closeEvent() handler so that we can intercept any clean closure of the window. What is different is that this action closes the only current window, not the application (unless this is the application's only window).

```
fileQuitAction = self.createAction("&Quit", self.fileQuit,
"Ctrl+Q", "filequit", "Close the application")
```

The "quit" action terminates the application, and does so by closing each of the SDI Text Editor's windows, as we will see when we review the fileQuit() method.

```
editCopyAction = self.createAction("&Copy", self.editor.copy,
QKeySequence.Copy, "editcopy",
"Copy text to the clipboard")
```

This action connects to the QTextEdit's relevant slot. The same is true of the "cut" and "paste" actions.

The menus, toolbars, and status bar are all created in ways that we have seen previously, except for the Window menu, which we will look at now.

```
self.windowMenu = self.menuBar().addMenu("&Window")
self.connect(self.windowMenu, SIGNAL("aboutToShow()"),
self.updateWindowMenu)
```

We do not add any actions to the Window menu at all. Instead, we simply connect the menu's aboutToShow() method to our custom updateWindowMenu() method which, as we will see, populates the menu with all the SDI Text Editor windows.