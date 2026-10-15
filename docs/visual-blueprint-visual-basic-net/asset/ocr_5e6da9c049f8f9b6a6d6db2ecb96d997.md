# Apply It

Context menus are an easy way to make your program more functional. Many users expect to see the functionality of an item when they right-click it. In most cases, you must place the same functionality located in the context menu as buttons on the form or in the main menu. To do this poorly, you replicate the code in both a context menu item’s click event and the button or main menu’s click event.

It pays to make your main code sections in separate procedures instead of simply locating the code directly in events. This way, if you have a button on the form and a context menu with the same function, you can reuse the code. For this code to work, use the example presented below in the steps, and add a button to the form. For more information on handling events, see Chapter 2.

# TYPE THIS:

```
Private Sub RemoveSelectedListItems()
    If ListBox1.SelectedItem Is Nothing Then
        MsgBox("Select an item to remove.")
    Else
        ListBox1.Items.Remove(ListBox1.SelectedItem)
    End If
End Sub

Private Sub MenuItem1_Click(...)
    RemoveSelectedListItems()
End Sub

Private Sub Button1_Click(...)
    RemoveSelectedListItems()
End Sub
```

# RESULT:

Both the button and the context menu function properly.

![](bbox=[0.06, 0.49, 0.48, 0.78])

![](bbox=[0.52, 0.49, 0.94, 0.78])

+   6 Add the control to the form.
+   The example adds a control to the form.
+   Note: To add controls to the form see the section "Add a Control to the Form."

+   7 Set the ContextMenu property of the ListBox to context menu you just created.
+   8 Press F5 to run your project.

+   9 Right-click your control to see your context menu appear.

The ContextMenu control provides the menu you create when you right-click the appropriate control.