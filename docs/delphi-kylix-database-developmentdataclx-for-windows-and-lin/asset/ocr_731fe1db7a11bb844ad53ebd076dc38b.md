+   Place a TSQLConnection component on a form and connect it to the ConMan database.
+   Drop a TSQLDataSet on the form and set its TSQLConnection property to the TSQLConnection component that you created in step 1. Set the Name property to sqlContacts and the CommandText property to SELECT * FROM CONTACTS. This is the master dataset.
+   Drop a TDataSource on the form, set its Name property to dsContacts, and set its DataSet property to sqlContacts.
+   Drop another TSQLDataSet on the form. Set the Name property to sqlActivities and the DataSource property to dsContacts. This is the detail dataset.
+   Set sqlActivities.CommandText to SELECT * FROM ACTIVITIES WHERE ContactID = :ContactID.

That’s all that’s required to establish a master/detail relationship in your program code. You should note the following points:

+   The detail dataset’s CommandText property is always a parameterized query. The parameter names actually refer to column names in the master dataset.
+   Whenever the master dataset changes records, the detail dataset automatically retrieves the records that are associated with the current master record.

The first point deserves a little more explanation.

You’ll recall from the section titled “Parameterized Queries” that when using parameterized queries, you typically make calls to TSQLDataSet.ParamByName to set the parameters.

With a detail dataset, parameter substitution is a bit more automated. VCL/CLX notices that the detail dataset’s DataSource parameter is assigned, so it looks to the data source’s dataset as the source of parameter values.

For example, in the CONTACT/ACTIVITIES example, sqlActivities.CommandText contains a single parameter: ContactID. When Delphi assigns the value of the ContactID parameter, it looks to the master dataset for a column named ContactID. Because the master dataset does, indeed, contain a column named ContactID, the value of the parameter is taken from that column.

# Note

You can create a detail dataset that gets only some of its parameter values from the master dataset. In this case, you must set the values of the other parameters manually.

For example, given the SQL statement SELECT * FROM ACTIVITIES WHERE (ContactID = :ContactID) AND (SCHEDULED > :Earliest), the detail dataset would get the value for the ContactID parameter from the master dataset. You would make a call to sqlActivities.ParamByName to set the Earliest parameter.





![](bbox=[0.85, 0.28, 0.96, 0.42])