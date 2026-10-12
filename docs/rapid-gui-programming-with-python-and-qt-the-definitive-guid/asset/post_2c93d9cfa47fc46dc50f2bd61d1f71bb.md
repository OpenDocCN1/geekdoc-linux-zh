
truncated on the form; once the label is laid out the layout manager will make sure that the text is displayed in full.

Now drag a Line Edit (from the Input Widgets group), and put this to the right of the Label. Go to the property editor and change the Line Edit's "objectName" (the very first property of all widgets) to "findLineEdit". We are giving it a sensible name because we want to refer to this line edit in our code.

Now drag another Label and another Line Edit below the first two. The second Label should have the text "Replace with" and the second Line Edit should be called "replaceLineEdit". The form should now look very similar to Figure 7.4.

![](img/9bfe0a027fcc8793bb087287001100dd_225_0.png)

**Figure 7.4 Two Labels and two Line Edits**

At any time we can save the form by pressing Ctrl+S or File→Save. When we save we will use the filename, findandreplace1g.ui.

Every editable property (and some read-only properties) are shown in the property editor. But in addition, Qt Designer provides a context menu. The first option in the context menu is normally one that allows us to change the widget's most "important" property (e.g., a Label's or a Line Edit's "text" property), and a second option that allows us to change the widget's object name. If we change a checkbox, radio button, or push button's text using the context menu, the editing is done in-place, in which case we must press Enter to finish. We will always talk of changing properties in the property editor; but you can, of course, use the context menu if you prefer.

We will now add the two checkboxes. Drag a Check Box from the Buttons group (near the top of the Widget Box) and put it underneath the second Label. Change its object name to "caseCheckBox" and its text to "&Case sensitive", by using the property editor or the context menu. Drag a second Check Box to the right of the first: Change its object name to "wholeCheckBox" and its text to "Wh&ole words", and set its "checked" state to "true". The form should now be similar to the one shown in Figure 7.5.

![](img/9bfe0a027fcc8793bb087287001100dd_226_0.png)

**Figure 7.5 Two Labels, Two Line Edits, and two Checkboxes**

Now we will add the Syntax label and combobox. Drag a Label below the case-sensitive checkbox and set its text to “&Syntax:”. Now drag a Combo Box (from the Input Widgets group) to the right of the Syntax Label. Change the Combo Box’s object name to “syntaxComboBox”. Right-click the Combo Box and choose the first menu option, Edit Items. Click the “+” icon, and type in “Literal text”. Repeat this to add “Regular expression”. Click the OK button to finish.

If the user resizes the form we want the widgets to stay neatly together rather than spreading out, so drag a Vertical Spacer (from the Spacers group near the top of the Widget Box) and put it below the Combo Box. When we design forms using code we use stretches, but when we design them visually we use spacers: They both expand to fill empty space. Adding a stretch to a layout is essentially the same as inserting a QSpacerItem into a layout, but is less to type.

To make the buttons visually separate from the widgets we have just created, we will put a vertical line between them and the other widgets. Drag a Vertical Line (actually a QFrame with shape QFrame_VLine) from the Display Widgets group (near the bottom of the Widget Box) and put it to the right of all the widgets in the form, but leaving space to the right of it for the buttons. Now the form should look like Figure 7.6.

We are now ready to create the buttons. Drag a Push Button (from the Buttons group near the top of the Widget Box) to the top right of the form. Change its object name to “findButton” and its text to “&Find”. Drag another button beneath the Find button, and give it the object name “replaceButton” and set its text to be “&Replace”. Create a third button, below the Replace button. Give it an object name of “replaceAllButton” and change its text to “Replace &All”. Now drag a Vertical Spacer under the Replace All button. Finally, drag a fourth button below the spacer. Give this button the object name “closeButton” and change its text to “Close”.

Now we have all the widgets and spacers we need and we have set all their properties appropriately. The form should look like that shown in Figure 7.7.

![](img/9bfe0a027fcc8793bb087287001100dd_227_0.png)

**Figure 7.6 A Find and Replace dialog without buttons**

![](img/9bfe0a027fcc8793bb087287001100dd_227_1.png)

**Figure 7.7 A Find and Replace dialog that is not laid out**

What is the best way to lay out this form? What is the best design for this form? The answers to these questions are matters of taste and practice. Here, we simply show the mechanics, and leave the aesthetics to you.

We will begin by laying out the first two Labels and their Line Edits. Click the form to deselect everything, then Shift+Click the Find what Label and its Line Edit, and the Replace with Label and its Line Edit. Once these four widgets are selected, click Form→Lay Out in a Grid (or click the corresponding toolbar button). The layout is indicated by a red line—layout lines are not visible at runtime.

Now deselect everything (by clicking the form), and select the two Check Boxes. Click Form→Lay Out Horizontally. Again, deselect everything, and this time lay out the Syntax Label and Combo Box using a horizontal layout. There should now be three layouts—a grid and two horizontal layouts, like those shown in Figure 7.8.

We can now lay out the layouts on the left-hand side of the form. Click the form to deselect everything. It can be tricky to select layouts (rather than widgets), so instead of selecting by using Shift+Click, we will use a selection rectangle. Click near the bottom left of the form, and drag the selection rectangle: This rectangle only needs to touch an object to select it, so drag up and right so that it touches the left-hand Vertical Spacer and the three layouts—and nothing else (not the Vertical Line, for example). Now, release and click Form→Lay Out Vertically.

![](img/9bfe0a027fcc8793bb087287001100dd_228_0.png)

**Figure 7.8 A *Find and Replace* dialog with some layouts**

We can use the same selection technique to lay out the buttons. Click the form to deselect everything. Now click near the bottom right of the form and drag so that the selection rectangle touches the Close button, the right-hand Vertical Spacer, and the other three buttons—and nothing else. Now, release and click Form→Lay Out Vertically. We should now have a form with every widget in the left- or right-hand layout and a Vertical Line in the middle, as shown in Figure 7.9.

![](img/9bfe0a027fcc8793bb087287001100dd_228_1.png)

**Figure 7.9 A *Find and Replace* dialog almost laid out**

We are now ready to lay out the form itself. Deselect everything by clicking the form. Now click Form→Lay Out Horizontally. The form will now look a bit too tall, so just drag the bottom of the form up until the form looks better. If you drag a lot, the spacers may “disappear”; they are still there, but just too small to be seen.

We can now preview the form to see what the layout really looks like, and during the preview we can drag the form's corner to make it smaller and larger to check that its resizing behavior is sensible. To preview, click Form→Preview (or press Ctrl+R). It is also possible to preview in different styles using the Form→Preview in menu option. The form should now look like the one in Figure 7.10. If this is not the case, use Edit→Undo to unwind your changes, and then lay things out again. If you have to redo a layout, it sometimes helps to resize and reposition some of the widgets to give Qt Designer more of a clue about how you want the layout to go, especially when using grid layouts.

![](img/9bfe0a027fcc8793bb087287001100dd_229_0.png)

We are now ready to set the labels' buddies, set the form's tab order, do any connections we need, and name and save the form.

We will start with buddies. Click Edit→Edit Buddies to switch on buddy mode. To set up buddy relationships we click a Label and drag to the widget we want to be its buddy. So in this example, we must click the Find what Label and drag to its Line Edit, and then do the same for the Replace with Label and its Line Edit, and then for the Syntax Label and the Combo Box. To leave buddy mode, press F3. Now, no ampersands (&) should be visible in the Labels.

Next we will set the form's tab order. Click Edit→Edit Tab Order, and then click each numbered box in turn, in the tab order that you want. To leave tab order mode, press F3.

The Find, Replace, and Replace All buttons will need to be connected to our own custom methods; we will do this outside of Qt Designer. But the Close button can be connected to the dialog's reject() slot. To do this, click Edit→Edit Signals/Slots, and then drag from the Close button to the form. When you release, the Configure Connection dialog will pop up. Click the (no-argument) clicked() signal from the list of signals on the left, and the reject() slot from the list of slots on the right, and then click OK. To leave signal–slot mode, press F3.

Click the form to deselect everything. This also has the effect of making the property editor show the form's properties. Set the dialog's object name (which will be used in its class name) to “FindAndReplaceDig”, and set the “windowTitle” property to “Find and Replace”. Now click File→Save to save the user interface, giving it a filename of findandreplaceig.ui.
