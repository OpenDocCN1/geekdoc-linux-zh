textEdit. Then scroll down to find windowTitle, and change it to something like “Edit Example” maybe.

To add widgets to the form, just drag them from the Widget Box to the form. Scroll down to find the Text Edit widget, and drag it to the form. Scroll back up to find the Push Button widget, and drag one of those to the form. Notice that the Object Inspector shows the two new widgets as children of QWidget.

Select the Push Button in the Object Inspector, and change the objectName to “quitButton.” Now scroll down in the Property Editor to find the text property. Change that to “Quit.”

We are going to add one more feature to this example: a second button that will clear the text edit window. This will require us to provide the slot function to do the clearing. Drag another button on to the form, change the objectName to “clearButton,” and change the text to “Clear.”

Next we want to put our widgets into a vertical layout. With the Clear button selected, hold the Ctrl key and select the other two widgets. Now all three widgets are selected. In the Form menu, select Lay Out Vertically. Note that the widgets are now children of QVBoxLayout.

Now we need to connect a signal of the Quit button to a slot of the Text Edit window. In the Edit menu, select Edit Signals/Slots. Select the Quit button, and drag toward the Text Edit window. That brings up the dialog shown in Fig. 11.3. Check Show signals and slots inherited from QWidget, and select clicked(). The slot window now becomes active. Oddly, quit() is not one of the options. Select close() instead, and click OK. To see what the final form looks like, select Form > Preview... (Fig. 11.4).

![](bbox=[0.27, 0.59, 0.75, 0.83])

Signals/Slots dialog.