
## Figure 6.3 QMainWindow's areas

![](img/9bfe0a027fcc8793bb087287001100dd_183_0.png)

Toolbars are suitable for holding toolbar buttons, and some other kinds of widgets such as comboboxes and spinboxes. For larger widgets, for tool palettes, or for any widget that we want the user to be able to drag out of the window to float freely as an independent window in its own right, using a dock window is often the right choice.

Dock windows are windows that can appear in the dock areas shown in Figure 6.3. They have a small caption, and restore and close buttons, and they can be dragged from one dock area to another, or float freely as independent top-level windows in their own right. When they are docked they automatically provide a splitter between themselves and the central area, and this makes them easy to resize.

In PyQt, dock windows are instances of the `QDockWidget` class. We can add a single widget to a dock widget, just as we can have a single widget in a main window's central area, and in the same way this is no limitation, since the widget added can be a composite.

```python
logDockWidget = QDockWidget("Log", self)
logDockWidget.setObjectName("LogDockWidget")
logDockWidget.setAllowedAreas(Qt.LeftDockWidgetArea |
    Qt.RightDockWidgetArea)

self.listWidget = QListWidget()
logDockWidget.setWidget(self.listWidget)
self.addDockWidget(Qt.RightDockWidgetArea, logDockWidget)
```

Dock widgets are not put into a layout, so when we create them, in addition to providing their window caption, we must give them a parent. By setting a parent, we ensure that the dock widget does not go out of scope and get garbage-collected by Python at the wrong time. Instead, the dock widget will be deleted when its parent, the top-level window (the main window), is deleted.

Every PyQt object can be given an object name, although up to now we have never done so. Object names can sometimes be useful in debugging, but we have set one here because we want PyQt to save and restore the dock widget's size and position, and since there could be any number of dock widgets, PyQt uses the object name to distinguish between them.

By default, dock widgets can be dragged into any dock area and are movable, floatable, and closable. Since our dock widget is going to be used to store a list—a widget that is usually tall and narrow—it only makes sense for it to be in the left or right dock areas (or to float), so we use `setAllowedAreas()` to restrict the areas. Dock widgets also have a `setFeatures()` method which is used to control whether the dock widget can be moved, floated, or closed, but we do not need to use it here because the defaults are fine.

Once the dock widget has been set up, we create the widget it will hold, in this case a list widget. Then we add the widget to the dock widget, and the dock widget to the main window. We did not have to give the list widget a parent because when it is added to the dock widget the dock widget takes ownership of it.

```python
self.printer = None
```

We want users to be able to print out their images. To do this we need to create a `QPrinter` object. We could create the printer whenever we need it and leave it to be garbage-collected afterward. But we prefer to keep an instance variable, initially set to `None`. The first time the user asks to print we will create a `QPrinter` and assign it to our printer variable. This has two benefits. First, we create the printer object only when it is needed, and second, because we keep a reference to it, it stays around—and keeps all its previous state such as the user's choice of printer, paper size, and so on.

```python
self.sizeLabel = QLabel()
self.sizeLabel.setStyleSheet(QFrame.StyledPanel | QFrame.Sunken)
status = self.statusBar()
status.setSizeGripEnabled(False)
status.addPermanentWidget(self.sizeLabel)
status.showMessage("Ready", 5000)
```

For the application's status bar, we want the usual message area on the left, and a status indicator showing the width and height of the current image. We do this by creating a `QLabel` widget and adding it to the status bar. We also switch off the status bar's size grip since that seems inappropriate when we have an indicator label that shows the image's dimensions. The status bar itself is created for us the first time we call the `QMainWindow`'s `statusBar()` method. If we call the status bar's `showMessage()` method with a string, the string will be displayed in the status bar, and will remain on display until either another `showMessage()` call supplants it or until `clearMessage()` is called. We have used the two-argument form, where the second argument is the number of milliseconds (5000, i.e., 5 seconds) that the message should be shown for; after this time the status bar will clear itself.

So far we have seen how to create the main window’s central widget, create a dock widget, and set up the status bar. Now we are almost ready to create the menus and toolbars, but first we must understand what PyQt actions are, and then take a brief detour to learn about resources.

## Actions and Key Sequences

Qt’s designers recognized that user interfaces often provide several different ways for the user to achieve the same thing. For example, creating a new file in many applications can be done via the File→New menu option, or by clicking the New File toolbar button, ![](img_placeholder_1), or by using the Ctrl+N keyboard shortcut. In general, we do not care how the user asked to perform the action, we only care what action they asked to be done. PyQt encapsulates user actions using the `QAction` class. So, for example, to create a “file new” action we could write code like this:

```python
fileNewAction = QAction(QIcon("images/filenew.png"), "&New", self)
fileNewAction.setShortcut(QKeySequence.New)
helpText = "Create a new image"
fileNewAction.setToolTip(helpText)
fileNewAction.setStatusTip(helpText)
self.connect(fileNewAction, SIGNAL("triggered()"), self.fileNew)
```

This assumes that we have a suitable icon and a `fileNew()` method. The ampersand in the menu item’s text means that the menu item will appear as **New** (except on Mac OS X or unless the windowing system is set to suppress underlines), and that keyboard users will be able to invoke it by pressing Alt+F, assuming that the File menu’s text is “&File” so that it appears as File. Alternatively, the user could use the shortcut that was created by `setShortcut()`, and simply press Ctrl+N instead.

Many key sequences are standardized, some even across different windowing systems. For example, Windows, KDE, and GNOME all use Ctrl+N for “new” and Ctrl+S for “save”. Mac OS X is similar, with Command+N and Command+S for these actions. The `QKeySequence` class in PyQt 4.2 provides constants for the standardized key sequences, such as `QKeySequence.New`. This is especially useful when the standardized key sequences differ across windowing systems, or where more than one key sequence is associated with an action. For example, if we set a shortcut to `QKeySequence.Paste`, PyQt will trigger a “paste” action in response to Ctrl+V or Shift+Ins on Windows; Ctrl+V, Shift+Ins, or F18 on KDE and GNOME; and Command+V on Mac OS X.

For key sequences that are not standardized (or if we want backward compatibility with earlier PyQt releases), we can provide the shortcut as a string, for example, `setShortcut("Ctrl+Q")`. This book uses the standardized key sequences that are available, and otherwise falls back to using strings.

![](img/9bfe0a027fcc8793bb087287001100dd_185_1.png)

### Table 6.1 Selected QAction Methods

| Syntax | Description |
| :--- | :--- |
| `a.data()` | Returns `QAction` `a`’s user data as a `QVariant` |
| `a.setData(v)` | Sets `QAction` `a`’s user data to `QVariant` `v` |
| `a.isChecked()` | Returns `True` if `QAction` `a` is checked |
| `a.setChecked(b)` | Checks or unchecks `QAction` `a` depending on `bool` `b` |
| `a.isEnabled()` | Returns `True` if `QAction` `a` is enabled |
| `a.setEnabled(b)` | Enables or disables `QAction` `a` depending on `bool` `b` |
| `a.setSeparator(b)` | Sets `QAction` `a` to be a normal action or a separator depending on `bool` `b` |
| `a.setShortcut(k)` | Sets `QAction` `a`’s keyboard shortcut to `QKeySequence` `k` |
| `a.setStatusTip(s)` | Sets `QAction` `a`’s status tip text to string `s` |
| `a.setText(s)` | Sets `QAction` `a`’s text to string `s` |
| `a.setToolTip(s)` | Sets `QAction` `a`’s tooltip text to string `s` |
| `a.setWhatIsThis(s)` | Sets `QAction` `a`’s What’s This? text to string `s` |
| `a.toggled(b)` | This signal is emitted when `QAction` `a`’s checked status changes; `bool` `b` is `True` if the action is checked |
| `a.triggered(b)` | This signal is emitted when `QAction` `a` is invoked; the optional `bool` `b` is `True` if `QAction` `a` is checked |

Notice that we give the `QAction` a parent of `self` (the form in which the action is applicable). It is important that every `QObject` subclass (except top-level windows) has a parent; for widgets this is usually achieved by laying them out, but for a pure data object like a `QAction`, we must provide the parent explicitly.

Once we have created the action, we can add it to a menu and to a toolbar like this:

```python
fileMenu.addAction(fileNewAction)
fileToolbar.addAction(fileNewAction)
```

Now whenever the user invokes the “file new” action (by whatever means), the `fileNew()` method will be called.

## Resource Files

Unfortunately, there is a small problem with the code we have written. It assumes that the application’s working directory is the directory where it is located. This is the normal case under Windows where the `.pyw` (or a shortcut to it) is clicked (or double-clicked). But if the program is executed from the command
