```
seperator = QAction(self)
seperator.setSeparator(True)
self.addActions(editToolbar, (editInvertAction,
editSwapRedAndBlueAction, seperator, editUnMirrorAction,
editMirrorVerticalAction, editMirrorHorizontalAction()))
```

If we need more sophisticated context menu handling—for example, where the menu’s actions vary depending on the application’s state, we can reimplement the relevant widget’s contextMenuEvent() event-handling method. Event handling is covered in Chapter 10.

![](bbox=[0.89, 0.18, 0.97, 0.28])

When we create a new image or load an existing image, we want the user interface to revert to its original state. In particular, we want the “edit invert” and “edit swap red and green” actions to be “off”, and the mirror action to be “edit unmirrored”.

```
self.resettableActions = ((editInvertAction, False),
(editSwapRedAndBlueAction, False),
(editUnMirrorAction, True))
```

We have created an instance variable holding a tuple of pairs, with each pair holding an action and the checked state it should have when a new image is created or loaded. We will see resettableActions in use when we review the fileNew() and loadFile() slots.

In the Image Changer application, all of the actions are enabled all of the time. This is fine, since we always check for a null image before performing any action, but it has the disadvantage that, for example, “file save” will be enabled if there is no image or if there is an unchanged image, and similarly, the edit actions will be enabled even if there is no image. The solution is to enable or disable actions depending on the application’s state, as the sidebar shows.

![](bbox=[0.89, 0.5, 0.97, 0.65])

# Restoring and Saving the Main Window’s State

Now that the main window’s user interface has been fully set up, we are almost ready to finish the initializer method, but before we do we will restore the application’s settings from the previous run (or use default settings if this is the very first time the application has been run).

Before we can look at application settings, though, we must make a quick detour and look at the creation of the application object and how the main window itself is created. The very last executable statement in the imagechanger.pyw file is the bare function call:

```
main()
```

As usual, we have chosen to use a conventional name for the first function we execute. Here is its code: