# Apply It

You can enable users to view their current position in a data set using the following procedure. You call this procedure when the data loads initially, and after the user presses a button and you alter the Position property.

# TYPE THIS:

```
Private Sub ShowPosition()
Dim recordCount As Integer
Dim currentPosition As Integer
recordCount = Me.BindingContext (DsNorthwind1, "Customers").Count
If recordCount = 0 Then
    Label1.Text = "(No records)"
Else
    currentPosition = Me.BindingContext (DsNorthwind1, "Customers").Position + 1
    Label1.Text = currentPosition.ToString & " of " & recordCount.ToString
End If
End Sub
```

# RESULT:

5 of 36

![](bbox=[0.07, 0.47, 0.48, 0.8])

![](bbox=[0.52, 0.47, 0.95, 0.8])

7 For the next record button, type Me.Binding Context (DsNorthwind1, "Customers").Position += 1, replacing DsNorthwind1, "Customers" with the DataSet and table.

8 For the last record button, type Me.BindingContext (DsNorthwind1,"Customers").Position = DsNorthwind1.Customers.Count -1, replacing DsNorthwind1, "Customers" with the DataSet and table, and .DsNorthwind1.Customers with the data table.

9 Press F5 to run your project.

You can click the buttons to move through the records present in the table.