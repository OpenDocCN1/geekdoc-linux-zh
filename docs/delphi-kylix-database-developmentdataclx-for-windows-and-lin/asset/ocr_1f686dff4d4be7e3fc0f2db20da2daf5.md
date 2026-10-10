The simplest aggregate that you can create is one that totals or averages over the entire dataset. The aggregates that we created previously aggregate across the whole dataset. Many times, however, you want to calculate an aggregate based on a part of the dataset.

To create a grouped aggregate, you first need to make sure that there is at least one index defined on the dataset. For purposes of the EMPLOYEE.CDS dataset, we'll create an index named byBirthday on the Birthday field.

+   1. Drop a TClieniDataSet on the main form of your application.
+   2. Right-click the dataset, and select Load from MyBase Table... on the pop-up menu.
+   3. Select the file C:\EMPLOYEE.CDS and click Open.
+   4. Create an index named byBirthday on the Birthday field. (If you've forgotten how to create an index, please refer to Chapter 3, "Client Dataset Basics.")
+   5. Go into the field editor and create persistent fields for all dataset fields by selecting Add All Fields from the field editor pop-up menu.
+   6. Create a persistent aggregate field, named NumSameBirthday, using the expression `Count(Birthday)`. Delphi will create a component named ClientDataSet1NumSameBirthday.
+   7. Drop a TDataSource, TDBGrid, and TLabel on the main form and connect the data source and grid to the client dataset.
+   8. In the data source's OnDataChange event, write the following code:

```
Label1.Caption := ClientDataSet1NumSameBirthday.Value;
```

Now we have our starting application. If you run it, you should see the value **10000** appear in the label (indicating that there are 10,000 records with a non-NULL birthday in the dataset).

Now that we've established our baseline, let's change the aggregate so that it calculates the number of employees who have the same birthday.

To do this, go back into the field editor and click the NumSameBirthday aggregate field. In the Object Inspector, set the IndexName to byBirthday. This tells the aggregate field to calculate its value using the byBirthday index. Next, set the GroupingLevel property to 1. (GroupingLevel is a one-based value that tells Delphi which portion of the index to use when calculating the aggregate value.)

For example, say that you have an index on the fields LastName;FirstName. If GroupingLevel is set to 1, only the first field in the index is used to calculate the aggregate. For an expression of Avg(Salary), the aggregate calculates the average salary for all employees having the same last name as the current record.