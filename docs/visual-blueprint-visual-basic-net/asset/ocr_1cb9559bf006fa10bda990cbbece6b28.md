# # CHANGE THE APPEARANCE OF A DATAGRID

A number of properties enable the DataGrid to display data effectively and attractively. You can use DataGrid properties to set up a color and border scheme, and modify the column it displays. For more information on adding a DataGrid server control to your Web Form, see the section “Add a DataGrid Control.”

The ItemStyle and AlternatingItemStyle determine how items look in the table. If you do not define AlternatingItemStyle, all items appear the same. If you set both properties, the items in the table switch between two styles. The HeaderStyle determines the appearance of the header and FooterStyle determines the appearance of the footer. You can easily edit these properties using the Property Page of the Property Builder for the control.

You can set borders for the grid using the BorderWidth and BorderStyle properties. The CellPadding property specifies the amount of space between the edge of a cell and its contents, and the CellSpacing property specifies the space between cells of the table. Alternately, you can also set these properties via the Borders page of the Property Builder.

To automatically add a style to the grid, you use the Auto Format dialog box, which provides a number of pre-made color-coordinated table styles. After you select a style, all properties of the control update to reflect the change.

Use the Columns page of the Property Builder dialog box to specify the columns the table displays. By default, the grid displays all of the columns. The dialog box provides the option “Create columns automatically at runtime” to disable this operation. You can also set the AutoGenerateColumns property to False in the property tool window. You can then add the columns you want to display. The control contains the list of columns to use in the Columns property.

# ## CHANGE THE APPEARANCE OF A DATAGRID

![](bbox=[0.05, 0.51, 0.475, 0.795])

![](bbox=[0.5, 0.51, 0.925, 0.795])

# ### SELECT DISPLAY COLUMNS

+   1. Configure a DataGrid on the Web Form.
+   2. Right-click the control.
+   3. Click Property Builder.
+      The DataGrid Property Builder dialog box appears.
+   4. Click Columns.
+   5. Click to remove the automatic column headers (changes to ☑).
+   6. Click a field from the list.
+   7. Click > to add columns.
+   8. Click OK.
+   9. Press F5.
+      The grid generates with the appropriate column headings.

> Note: See the section “Add a DataGrid Control” to add a DataGrid control.