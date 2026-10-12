harmlessly do nothing. However, to avoid confusing some users, it might be better to enable or disable actions depending on the application’s state; the sidebar in Chapter 13 shows how this can be done.

Layouts, splitters, tab widgets, stacked widgets, dock windows, SDI, and MDI together provide a wide range of user interface design options. In addition, it is possible to create our own layouts in code, or to create our own layout managers, so the possibilities really are limitless.

# ## Exercise

Modify the MDI Text Editor application (texteditor.pyw) so that instead of using MDI it uses a QTabWidget and becomes a tabbed editor.

The Window menu will not be required, so all the code associated with it can be removed. A new “file close tab” action will be needed, as will a corresponding method to handle it. Instead of using QWorkspace.windowList(), use a for loop to iterate from 0 to QTabWidget.count(), and use QTabWidget.widget() to access each window in turn.

The closeEvent() will need changing, and it is probably the trickiest to get right. Change loadFiles() to limit the number of files loaded on the command line to 10. fileNew() will need to create a TextEdit as before, and then add it to the tab widget using QTabWidget.addTab(), giving the widget and its window title as parameters. Instead of calling show() on the widget, use QTabWidget.setCurrentWidget(). The fileOpen(), loadFile(), fileSave(), fileSaveAs(), and fileSaveAll() methods will need small changes. The edit methods need to change only their first line of code to use QTabWidget.currentWidget() instead of QWorkspace.activeWindow().

Once everything is working, add two keyboard shortcuts, one for QKeySequence.PreviousChild and the other for QKeySequence.NextChild, along with suitable methods, prevTab() and nextTab(), to make their work.

The changes amount to about a dozen lines, plus an extra twenty lines or so for the shortcuts and their methods; as always the emphasis is on thought and understanding rather than on typing.

A model solution is provided in the file chap09/tabbededitor.pyw.

![](bbox=[0.84, 0.09, 0.93, 0.24])