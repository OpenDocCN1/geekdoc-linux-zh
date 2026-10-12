
## 5.5 Smart Dialogs

Third, its signal and slot connections are slightly different than before. Here are the connection calls:

```python
self.connect(self.thousandsEdit,
             SIGNAL("textEdited(QString)"), self.checkAndFix)
self.connect(self.decimalMarkerEdit,
             SIGNAL("textEdited(QString)"), self.checkAndFix)
self.connect(self.decimalPlacesSpinBox,
             SIGNAL("valueChanged(int)"), self.apply)
self.connect(self.redNegativesCheckBox,
             SIGNAL("toggled(bool)"), self.apply)
```

As before, we can rely on the decimal places spinbox to ensure that only a valid number of decimal places is set, and similarly the "red negatives" checkbox can only be in a valid state, so changes to either of these can be applied immediately.

But for the line edits, we now connect their `textEdited()` signals. These signals are emitted whenever the user types in a character or deletes a character from them. The `checkAndFix()` slot will both ensure that the line edits hold valid text and apply the change immediately. There are no buttons in this dialog: The user can close it by pressing Esc, which will then hide it. The dialog will be deleted only when its calling form is deleted, because at that point the caller's `self.numberFormatDlg` instance variable will go out of scope, and with no other reference to the dialog, it will be scheduled for garbage collection.

```python
def apply(self):
    self.format["thousandsseparator"] = \
        unicode(self.thousandsEdit.text())
    self.format["decimalmarker"] = \
        unicode(self.decimalMarkerEdit.text())
    self.format["decimalplaces"] = \
        self.decimalPlacesSpinBox.value()
    self.format["rednegatives"] = \
        self.redNegativesCheckBox.isChecked()
    self.callback()
```

The `apply()` method is the simplest we have seen so far. This is because it is called only when all the editing widgets hold valid data, so no post-mortem validation is required. It no longer emits a signal to announce a state change—instead, it calls the method it was given and this applies the changes directly to the caller's form.

```python
def checkAndFix(self):
    thousands = unicode(self.thousandsEdit.text())
    decimal = unicode(self.decimalMarkerEdit.text())
    if thousands == decimal:
        self.thousandsEdit.clear()
        self.thousandsEdit.setFocus()
    if len(decimal) == 0:
        self.decimalMarkerEdit.setText(".")
        self.decimalMarkerEdit.selectAll()
        self.decimalMarkerEdit.setFocus()
    self.apply()
```

This method applies preventative validation as the user types in either of the line edits. We still rely on the line edit validators, maximum length properties, and in the case of the decimal marker line edit, an input mask, with all of these combining to provide almost all the validation that we need. But it is still possible for the user to set the same text in both—in which case we delete the thousands separator and move the focus to its line edit, or (if the user tries hard) for the decimal place marker to be empty—in which case we set a valid alternative, select it, and give it the keyboard focus. At the end we know that both line edits are valid, so we can call `apply()` and apply the changes.

One benefit of using the show/hide approach is that the dialog’s state is maintained automatically. If we have to create the dialog each time it is used we must populate it with data, but for this dialog, whenever it is shown (after the first time), it already has the correct data. Of course, in this particular example we have three dialogs that are all used to edit the same data, which means that this dialog could become out of sync; we ignore this issue because having multiple dialogs editing the same data is not something we would do in a real application.

By passing in both the data structure (the format dictionary) and the caller’s update method (`refreshTable()`, passed as `self.callback`), we have made this dialog very smart—and very tightly coupled to its caller. For this reason, many programmers prefer the “middle way” of using standard dialogs—dumb dialogs are too limited and can be inconvenient to use, and smart dialogs can be more work to maintain because of the tight coupling their knowledge of their callers’ data structures implies.

## Summary

We categorized dialogs into three “intelligences,” dumb, standard, and smart, and showed that they can be used modally or modelessly. Dumb dialogs are easy to create, and are perfectly adequate for doing widget-level validation. Dumb dialogs are normally used modally, and if we are careful they can be generalized since they can be very loosely coupled to the application’s logic. Nonetheless, using dumb dialogs usually ends up leading to programmer frustration and the need to rewrite in the form of a standard or smart dialog, so it is often best to avoid them except for those very simple cases where just one or two values are required and the built-in QInputDialog static dialogs are not suitable.

The most common choice is between a standard modal dialog and a smart modeless dialog, and in the latter case between the “apply” and “live” styles.

Modal dialogs are the easiest to program because they block any other interaction with the dialog’s parent windows and their sibling windows, thereby reducing the risk that the data they are working on is changed from under them. But modeless dialogs are preferred by some users, and are particularly convenient when users want to try out various options before deciding which ones they want. Modal dialogs can also be used for this purpose if they provide some kind of preview; for example, font dialogs are often modal, and show sample text that reflects the user’s font settings as they change them.

The two validation strategies that we have looked at, post-mortem and preventative, can be used on their own or in combination. From a usability point of view, preventative is often considered to be superior, although it can lead to user frustration. For example, a user might complain (“I want to set this to five but it won’t let me”) when the setting is invalid because of another setting elsewhere on the form.

It is possible to design a dialog so that it can be used both for adding and for editing items. These add/edit dialogs are no different from other kinds of dialogs when it comes to the creation, layout, and connection of their widgets. The key difference is that they may need to behave in different ways depending on whether they are adding or editing. When editing, the widgets are populated from the item passed in, and when adding, the widgets are populated with default values. If the dialog is accepted, it may simply provide accessors through which the values set can be retrieved, leaving the work to the caller; or it may be smart, able to update edited items directly, and to create new items if the user is adding. See the AddEditTextViewDlg class in `chap08/additemmodel.py` (its user interface design is in `chap08/additemmodelVUI.ui`), and the TextItemDlg class in `chap12/pagesdesigner.pwy`, for examples of add/edit item dialogs.

Another possibility is to avoid using a dialog at all and to allow the user to edit data in-place—for example, in a list or table. This approach is covered in the chapters on model/view programming.

## Exercise

Write a stand-alone string list editing dialog. The dialog should use `if __name__ == "__main__":` so that it can be run and tested independently. It should look like the dialog shown in Figure 5.8.

The strings should be held in a `QListWidget`. The Sort button is easy to implement since we can connect its `clicked()` signal directly to the `QListWidget.sortItems()` method.

The dialog should work on its own string list, either a copy of one passed in, or one it creates itself, and when accepted should emit a signal containing the list (as a `QStringList`), and also have a publicly accessible data attribute, `stringlist`.

The `reject()` slot should be implemented like this:
