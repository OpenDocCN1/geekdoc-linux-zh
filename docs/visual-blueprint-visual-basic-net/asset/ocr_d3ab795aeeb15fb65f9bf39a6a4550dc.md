# VALIDATE DATA

Databases contain specific rules for the data they contain. When users enter data, they may not understand the requirements of the data source. You can prevent errors in Windows applications by validating the data before allowing the user to update it to the database table.

The ErrorProvider control manages DataSet errors. For information on adding the ErrorProvider control to a Windows Form, see Chapter 3. To validate data with the ErrorProvider control, set its DataSource property to the DataSet or DataTable you want to monitor. If you use a DataSet, you must also set the DataMember to the table to watch.

In the form code, you must set the ContainerControl property of the ErrorProvider control to the form for data validation to occur. To check for validation issues on a control the user edits, use the input control’s Validating event, which fires when the user leaves the input control.

When you detect an error, you set the event parameter e.Cancel to True and the control allows the user to reenter the data. You then alert the DataRow representing the row that the user made an error. Use the BindingContext’s Position property to determine the current row. For more information on the BindingContext object, see the section “Move through a Dataset.”

After you find the appropriate row, call the SetColumnError method of the DataRow object. Provide the column and the error message as the two parameters. For more information on the DataRow object, see the section “Work with Data Rows.”

You also need to respond to the control’s Validated event, where you enter code to run when validation is successful. This event runs only if you do not set Cancel = True in the Validating event. You remove the error message by using SetColumnError again with a blank string for the error message.

![](bbox=[0.05, 0.62, 0.95, 0.88])

1 Set up a form with input and movement controls, and add an ErrorProvider control on the form.

Note: To bind a control, see “Bind Controls to a Form.” To create movement controls, see “Move through a Dataset.” See Chapter 3 to add an ErrorProvider control.

2 For the ErrorProvider control, click the DataSource property and select the appropriate data set component. For DataSet, click the DataMember and select the appropriate table.

3 In the Form_Load event, type ErrorProvider1.ContainerControl = Me, replacing ErrorProvider1 with the name of the ErrorProvider control.

4 In the Validating event of an input control, create an If statement that performs the validation test.

5 Declare a variable to hold the current record index, assigning the Position property of the BindingContext to the variable. Note: See page the section “Move through a Dataset” to use BindingContext.