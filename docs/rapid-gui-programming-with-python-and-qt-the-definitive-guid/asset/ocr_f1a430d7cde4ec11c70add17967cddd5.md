or even both. The Image Changer application from the preceding chapter had two custom dialogs, the ResizeDlg, which was created purely in code (in the exercise), and the NewImageDlg, which was created using *Qt Designer*. We showed how to do things in code first so that you would get a strong sense of how the layout managers work. But in this chapter we are going to create dialogs using *Qt Designer*, which is shown in Figure 7.1.

*Qt Designer* can be used to create user interfaces for dialogs, custom widgets, and main windows. We will only cover dialogs; custom widgets are almost the same, only they are based on the “Widget” template rather than one of the “Dialog” templates. Using *Qt Designer* for main windows offers fewer advantages, apart from the convenience of a visual QAction editor. *Qt Designer* can also be used to create and edit resource files.

The user interfaces are stored in `.ui` files, and include details of a form's widgets and layouts. In addition, *Qt Designer* can be used to associate labels with their “buddies”, and to set the tab-order; that is, the order in which widgets get the keyboard focus when the user presses the Tab key. This can also be done in code with QWidget::setTabOrder(), but it is rarely necessary for hand-coded forms, since the default is the order of widget creation, which is usually what we want. *Qt Designer* can also be used to make signal–slot connections, but only between built-in signals and slots.

Once a user interface has been designed and saved in a `.ui` file, it must be converted into code before it can be used. This is done using the pyuic4 command-line program. For example:

```
C:\pyqt\chapter7>pyuic4 -o ui_findandreplacedlg.py findandreplacedlg.ui
```

As mentioned in the previous chapter, we can use either mkpyqt.py or Make PyQt to run pyuic4 for us. However, generating a Python module (*.py file) from a `.ui` file is not enough to make the user interface usable.* Note that the generated code (in the `ui_*.py` files) should never be hand-edited because any changes will be overwritten the next time pyuic4 is run.

From the end-user's perspective, it makes no difference whether a dialog's user interface is hand-coded or created with *Qt Designer*. However, there is a significant difference in the implementation of a dialog's interface, since we must create, lay out, and connect the dialog's widgets if hand coding, but only need to call a particular method to achieve the same thing with a dialog that uses a *Qt Designer* user interface.

One great benefit of using *Qt Designer*, in addition to the convenience of designing dialogs visually, is that if we change the design, we only have to regenerate the user interface module (using pyuic4 directly, or via mkpyqt.py or Make PyQt), and we do not need to change our code. The only time that we must change our code is if we add, delete, or rename widgets that we refer to in our code. This