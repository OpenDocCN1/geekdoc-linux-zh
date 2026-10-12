# ## The Static QMessageBox Methods

The **QMessageBox** class offers several static convenience methods that pop up a modal dialog with a suitable icon and buttons. They are useful for offering users dialogs that have a single **OK** button, or **Yes** and **No** buttons, and similar.

The most commonly used **QMessageBox** static methods are **critical()** , **information()** , **question()** , and **warning()** . The methods take a private widget (over which they center themselves), window title text, message text (which can be plain text or **HTML** ) , and zero or more button specifications. If no buttons are specified, a single **OK** button is provided.

The buttons can be specified using constants, or we can provide our own text. In **Qt 4.0** and **Qt 4.1** , it was very common to bitwise or **QMessageBox.Default** with **OK** or **Yes** buttons—this means the button will be pressed if the user presses **Enter** , and to bitwise or **QMessageBox.Escape** with the **Cancel** or **No** buttons, which will then be pressed if the user presses **Esc**. For example:

```
```
reply = QMessageBox.question(self,
"Image Changer - Unsaved Changes", "Save unsaved changes?" ,
QMessageBox.Yes|QMessageBox.Default ,
QMessageBox.No|QMessageBox.Escape)
```
```

The methods return the constant of the button that was pressed.

![](bbox=[0.06, 0.63, 0.11, 0.72])

From **Qt 4.2** , the **QMessageBox** API has been simplified so that instead of specifying buttons and using bitwise ors, we can just use buttons. For example, for a **yes/no/cancel** dialog we could write:

```
```
reply = QMessageBox.question(self,
"Image Changer - Unsaved Changes", "Save unsaved changes?" ,
QMessageBox.Yes |QMessageBox.No|QMessageBox.Cancel)
```
```

In this case, **PyQt** will automatically make the **Yes** (accept) button the default button, activated by the user pressing **Enter** , and the **Cancel** (reject) button the escape button, activated by the user pressing **Esc**. The **QMessageBox** methods also make sure that the buttons are shown in the correct order for the platform. We use the **Qt 4.2** syntax for the examples in this book.

The message box is closed by the user clicking the “accept” button (often **Yes** or **OK** ) or the “reject” button (often **No** or **Cancel** ) . The user can also, in effect, press the “reject” button by clicking the window’s close button, **X** , or by pressing **Esc** .

If we want to create a customized message box—for example, using custom button texts and a custom icon—we can create a **QMessageBox** instance. We can then use methods such as **QMessageBox.addButton()** and **QMessageBox.setIcon()** , and pop up the message box by calling **QMessageBox.exec()** .