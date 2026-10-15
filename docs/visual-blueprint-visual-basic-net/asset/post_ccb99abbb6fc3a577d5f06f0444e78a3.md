
## Extra

To delete a record from a table in the DataSet, access the table object and use the method RemoveTableRow, replacing Table with the name of the table. You must pass the row to delete. You can access a row by index number using the Rows property of the table object. Pass the index of the row you wish to delete in parentheses to the Rows property, starting from zero, and it returns a DataRow object. For more information on DataTable objects, see "Work with Data Tables." You need to update the position that the form displays since the row no longer exists. For more information on using BindingContext, see "Move through a Dataset."

### Example:

```
Dim pos As Integer = Me.BindingContext(DeNorthwind1, "Customers").Position
Dim row As DataRow = DeNorthwind1.Customers.Rows(pos)
DeNorthwind1.Customers.RemoveCustomersRow(row)
Me.BindingContext(DeNorthwind1, "Customers").Position -= 1
```

![](img/d6f772854306e15fb6df39b861a7b541_238_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_238_1.png)

- To add a new row, declare a variable of type DataRow.
- Type = DsNorthwind1.Customers.NewCustomersRow(), replacing DsNorthwind1 with name of the DataSet, and Customers with the table's name.
- Assign values to any fields that do not accept null values.
- Type the table name followed by .AddTableRow(row), replacing Table with the table name and row with the variable declared in step 5.

When you run the project, you can add, edit, and update information in the database.

## VALIDATE DATA

Databases contain specific rules for the data they contain. When users enter data, they may not understand the requirements of the data source. You can prevent errors in Windows applications by validating the data before allowing the user to update it to the database table.

The ErrorProvider control manages DataSet errors. For information on adding the ErrorProvider control to a Windows Form, see Chapter 3. To validate data with the ErrorProvider control, set its DataSource property to the DataSet or DataTable you want to monitor. If you use a DataSet, you must also set the DataMember to the table to watch.

In the form code, you must set the ContainerControl property of the ErrorProvider control to the form for data validation to occur. To check for validation issues on a control the user edits, use the input control’s Validating event, which fires when the user leaves the input control.

When you detect an error, you set the event parameter e.Cancel to True and the control allows the user to reenter the data. You then alert the DataRow representing the row that the user made an error. Use the BindingContext’s Position property to determine the current row. For more information on the BindingContext object, see the section “Move through a Dataset.”

After you find the appropriate row, call the SetColumnError method of the DataRow object. Provide the column and the error message as the two parameters. For more information on the DataRow object, see the section “Work with Data Rows.”

You also need to respond to the control’s Validated event, where you enter code to run when validation is successful. This event runs only if you do not set Cancel = True in the Validating event. You remove the error message by using SetColumnError again with a blank string for the error message.

![](img/d6f772854306e15fb6df39b861a7b541_239_0.png)

- Set up a form with input and movement controls, and add an ErrorProvider control on the form.

Note: To bind a control, see “Bind Controls to a Form.” To create movement controls, see “Move through a Dataset.” See Chapter 3 to add an ErrorProvider control.

- For the ErrorProvider control, click the DataSource property and select the appropriate data set component. For DataSet, click the DataMember and select the appropriate table.
- In the Form_Load event, type ErrorProvider1.ContainerControl = Me, replacing ErrorProvider1 with the name of the ErrorProvider control.
- In the Validating event of an input control, create an If statement that performs the validation test.
- Declare a variable to hold the current record index, assigning the Position property of the BindingContext to the variable. Note: See page the section “Move through a Dataset” to use BindingContext.
