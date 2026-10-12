![](bbox=[0.14, 0.1, 0.86, 0.48])

It is possible to have a workspace that is larger than its window by calling `QWorkspace.setCtrlBarsEnabled(True)`. The workspace's background can be set by specifying a background brush.

```
fileNewAction = self createAction("&New", self fileNew, QKeySequence New, "filenew", "Create a text file")
```

Most of the file actions are created as we have seen before. But as we will see, the MDI editor, like the SDI editor, does not have an `okToContinue()` method because each document window takes care of itself.

```
fileQuitAction = self createAction("&Quit", self close, "Ctrl+Q", "filequit", "Close the application")
```

If we close the application's window, the application will terminate. All the document windows will be closed, and any with unsaved changes are responsible for prompting the user and saving if asked to do so.

```
editCopyAction = self createAction("&Copy", self editCopy, QKeySequence Copy, "editcopy", "Copy text to the clipboard")
```

In the SDI editor we passed on the “copy”, “cut”, and “paste” actions to each window's `QTextEdit` to handle. This is not possible in the MDI application because when the user triggers one of these actions, it must be applied to whichever