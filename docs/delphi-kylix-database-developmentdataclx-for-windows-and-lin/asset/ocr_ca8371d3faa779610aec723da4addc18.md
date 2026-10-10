Let's add a field named **ID** to our dataset. In the field editor, enter **ID** in the Name edit control. Tab to the Type combo box and type *Integer*, or select it from the drop-down list. (The component name has been created for you automatically.) The Size edit control is disabled because *Integer* values are a fixed-length field. The *Field* type is preset to *Data*, which is what we want. Figure 3.2 shows the completed dialog.

![](bbox=[0.325, 0.26, 0.65, 0.38])

# Figure 3.2

*The New Field dialog after entering information for a new field.*

Click **OK** to add the field to the client dataset. You'll see the new **ID** field listed in the field editor.

Now add a second field, called **LastName**. Right-click the field editor to display the New Field dialog and enter **LastName** in the Name edit control. In the Type combo, select *String*. Then, set *Size* to 30——the size represents the maximum number of characters allowed for the field. Click **OK** to add the **LastName** field to the dataset.

Similarly, add a 20-character **FirstName** field and an *Integer* **Department** field. Finally, let's add a **Salary** field. Open the New Field dialog. In the Name edit control, type **Salary**. Set the Type to *Currency* and click **OK**. (The currency type instructs Delphi to automatically display it with a dollar sign.)

If you have performed these steps correctly, the field editor looks like Figure 3.3.

![](bbox=[0.535, 0.715, 0.565, 0.885])

# Figure 3.3

*The field editor after adding five fields.*