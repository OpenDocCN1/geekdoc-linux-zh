
## SDI Text Editor: Instance Management and File Operations

When the user closes a window, thanks to the `Qt.WA_DeleteOnClose` flag, the window will be deleted. But because we have a reference to the window in the static `Instances` set, the window cannot be garbage-collected. For this reason, we connect the window's `destroyed()` signal to a slot that updates the `Instances` by removing any windows that have been closed. We will discuss this in more detail when we look at the `updateInstances()` method.

Since each window is responsible for a single file, we can have a single filename associated with each window. The filename can be passed to the window's initializer, and it defaults to an empty `QString`. The last lines of the initializer handle the filename.

```python
self.filename = filename
if self.filename.isEmpty():
    self.filename = "Unnamed-%d.txt" % MainWindow.NextId

MainWindow.NextId += 1
self.editor.document().setModified(False)
self.setWindowTitle("SDI Text Editor - %s" % self.filename)
else:
    self.loadFile()
```

If the window has no filename, either because the application has just been started or because the user has invoked the “file new” action, we create a suitable window title; otherwise, we load the given file.

The `closeEvent()`, `loadFile()`, `fileSave()`, and `fileSaveAs()` methods are very similar to ones we have seen before, so we will not describe them here. (They are in the source code in `chap09/sditexteditor.pyw`, of course.) Instead, we will focus on those things that are special for an SDI application.

```python
def fileNew(self):
    MainWindow().show()
```

When the user invokes the “file new” action, this method is called. Another instance of this class is created, and `show()` is called on it (so it is shown modelessly). At the end of the method, we would expect the window to go out of scope and be destroyed since it does not have a PyQt parent and it is not an instance variable. But inside the main window's initializer, the window adds itself to the static `Instances` set, so an object reference to the window still exists, and therefore, the window is not destroyed.

```python
def fileOpen(self):
    filename = QFileDialog.getOpenFileName(self, "SDI Text Editor -- Open File")
    if not filename.isEmpty():
        if not self.editor.document().isModified() and \
            self.filename.startswith("Unnamed"):
            self.filename = filename
            self.loadFile()
        else:
            MainWindow(filename).show()
```

This method is slightly different from similar ones we have seen before. If the user gives a filename, and the current document is both unmodified and unnamed (i.e., a new empty document), we load the file into the existing window; otherwise, we create a new window, passing it the filename to load.

```python
def fileSaveAll(self):
    count = 0
    for window in MainWindow.Instances:
        if isAlive(window) and \
            window.editor.document().isModified():
            if window.fileSave():
                count += 1
    self.statusBar().showMessage("Saved %d of %d files" % (
        count, len(MainWindow.Instances)), 5000)
```

As a courtesy to users, we provide a Save All menu option. When it is invoked we iterate over every window in the `Instances` set, and for each window that is “alive” and modified, we save it.

A window is alive if it has not been deleted. Unfortunately, this is not quite as simple as it seems. There are two lifetimes associated with a `QWidget`: the lifetime of the Python variable that refers to the widget (in this case, the `MainWindow` instances in the `Instances` set), and the lifetime of the underlying PyQt object that is the widget as far as the computer’s window system is concerned.

Normally, the lifetimes of a PyQt object and its Python variable are exactly the same. But here they may not be. For example, suppose we started the application and clicked File➡New a couple of times so that we had three windows, and then we navigated to one of them and closed it. At this point the window that is closed (thanks to the `Qt.WA_DeleteOnClose` attribute) will be deleted.

Under the hood, PyQt actually calls the `deleteLater()` method on the deleted window. This gives the window the chance to finish anything it is in the middle of doing, so that it can be cleanly deleted. This will normally be all over in less than a millisecond, at which point the underlying PyQt object is deleted from memory and no longer exists. But the Python reference in the `Instances` set will still be in place, only now referring to a PyQt object that has gone. For this reason, we must always check any window in the `Instances` set for aliveness before accessing it.

```python
def isAlive(obj):
    import sip
    try:
        sip.unwrapInstance(obj)
    except RuntimeError:
        return False
    return True
```

The `sip` module is one of PyQt’s supporting modules that we do not normally need to access directly. But in cases where we need to dig a bit deeper, it can be useful. Here, the method tries to access a variable’s underlying PyQt object. If the object has been deleted, a `RuntimeError` exception is raised, in which case we return `False`; otherwise, the object still exists and we return `True`.

> *The `isAlive()` function is based on Giovanni Bajo’s PyQt (then PyKDE) mailing list posting, “How to detect if an object has been deleted”. The list is used for both PyQt and PyKDE.*

```python
@staticmethod
def updateInstances(qobj):
    MainWindow.Instances = set([window for window \
        in MainWindow.Instances if isAlive(window)])
```

Whenever a window is closed (and therefore deleted), it emits a `destroyed()` signal, which we connected to the `updateInstances()` method in the initializer. This method overwrites the `Instances` set with a set that contains only those window instances that are still alive.

So why do we need to check for aliveness when we iterate over the `Instances`—for example, in the `fileSaveAll()` method—since this method ensures that the `Instances` set is kept up-to-date and is holding only live windows? The reason is that it is theoretically possible that between the time when a window is closed and the `Instances` set is updated, the window is iterated over in some other method.

Whenever the user clicks the Window menu in any SDI Text Editor window, a menu listing all the current windows appears. This occurs because the windowMenu’s `aboutToShow()` signal is connected to the `updateWindowMenu()` slot that populates the menu.

```python
def updateWindowMenu(self):
    self.windowMenu.clear()
    for window in MainWindow.Instances:
        if isAlive(window):
            self.windowMenu.addAction(window.windowTitle(), self.raiseWindow)
```

First, any existing menu entries are cleared; there will always be at least one, the current window. Next we iterate over all the window instances and add an action for any that are alive. The action has text that is simply the window's title (the filename) and a slot—`raiseWindow()`—to be called when the menu option is invoked by the user.

```python
def raiseWindow(self):
    action = self.sender()
    if not isinstance(action, QAction):
        return
    for window in MainWindow.Instances:
        if isAlive(window) and \
            window.windowTitle() == action.text():
            window.activateWindow()
            window.raise_()
            break
```

This method could be called by any of the Window menu's entries. We begin with a sanity check, and then we iterate over the window instances to see which one has a title whose text matches the action's text. If we find a match, we make the window concerned the “active” window (the application's top-level window that has the keyboard focus), and raise it to be on top of all other windows so that the user can see it.

In the MDI section that follows we will see how to create a more sophisticated Window menu, with accelerators and some additional menu options.

```python
def fileQuit(self):
    QApplication.closeAllWindows()
```

PyQt provides a convenient method for closing all of an application's top-level windows. This method calls `close()` on all the windows, which in turn causes each window to get a `closeEvent()`. In this event (not shown), we check to see whether the `QTextEdit`'s text has unsaved changes, and if it has we pop up a message box asking the user if they want to save.

```python
app = QApplication(sys.argv)
app.setWindowIcon(QIcon(":/icon.png"))
MainWindow().show()
app.exec_()
```

At the end of the `sditexteditor.pyw` file, we create a `QApplication` instance and a single `MainWindow` instance and then start off the event loop.

Using the SDI approach is very fashionable, but it has some drawbacks. Since each main window has its own menu bar, toolbar, and possibly dock windows, there is more resource overhead than for a single main window.

> *On Mac OS X there is only one menu bar, at the top of the screen. It changes to reflect whichever window currently has the focus.*
