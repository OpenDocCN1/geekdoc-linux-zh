
## ADD A CONNECTION TO A FORM

After you set up a database connection, you must add the connection to your application so you can access the database. See the section "Create a Database Connection" for more on connecting to a database. The OleDbConnection and SqlConnection components hold a connection to a database for a particular form or class. Although the OleDbConnection component supports a variety of database connections through the OLEDB database specification, it does not perform as well as the SqlConnection due to its layers of compatibility. For that reason, this chapter uses the SqlAdapter combined with Microsoft SQL Server 2000. Although this chapter shows the use of SqlAdapter, the functionality of the OleDbAdapter is the same except for the name of the component.

The connection component provides no ability to access the database directly. Instead, a data adapter component bridges the gap. The SqlDataAdapter provides support for SqlConnection components. The data adapter component stores the appropriate SQL command text to retrieve, modify, add, and remove items from the database. With this, the adapter can provide two-way access to the database.

The DataSet component provides the final piece required to access the database. A DataSet uses the SqlDataAdapter to retrieve a set of tables from the database and store them into memory. Then your program can modify the data and write changes back when complete. The SqlDataAdapter provides a method, Fill, that loads a table of information into a DataSet. You provide the SqlDataAdapter's Fill method with the instance of the DataSet as the first parameter and the table to load as the second parameter.

Visual Basic .NET completes the sequencing of components automatically. When you add the database connection to the form, Visual Basic .NET creates both the connection and adapter components. A wizard enables you to provide the appropriate SQL command for the SqlDataAdapter. Another dialog box lets you select the appropriate tables to load into the DataSet.

![](img/d6f772854306e15fb6df39b861a7b541_223_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_223_1.png)

- 1 Click and drag a table listed in the Server Explorer from a connected database to the form.

Note: To create a database connection, see the section "Create a Database Connection."

VB .NET adds an SqlConnection control and an SqlDataAdapter control to the form.

- 2 Click Data ▸ Generate Dataset.

Note: If the menu item is disabled, click the form and try again.

The Generate Dataset dialog box appears.

- 3 Type a name for the dataset.

- 4 Click the tables to add to the dataset.

- 5 Verify that the "Add this dataset to the designer" options is checked.

- 6 Click OK.

## Apply It

You can create a dataset based on an XML file to bind to controls. You cannot bind controls visually when creating a dataset at runtime, but you can set the DataSource property of a DataGrid control or add a DataBindings object to a simple control. For more information on binding, see the section “Bind a Control on a Form.”

```
XMLTEST.XML
<root>
<Companies>
<CompanyName>Sample Company, Inc.</CompanyName>
<Products>
<ProductName>Sample Product 1</ProductName>
<ProductPrice>99.99</ProductPrice>
<ProductName>Sample Product 2</ProductName>
<ProductPrice>49.99</ProductPrice>
</Products>
</Companies>
</root>
```

### Bind XML To Grid

```
Dim XMLToGrid1 As New DataSet("Companies")
CompaniesXML.ReadXml("C:\COMPANIES.XML")
DataGrid1.DataSource = CompaniesXML
```

The DataGrid automatically displays the Companies table and provides a hyperlink to access the related products.

- 6. VB .NET adds a DataSet component to the form. The name consists of your entered name and a number.
- 7. Double-click the form to open the Form_Load event handler.
- 8. The Code Editor opens.
- 9. Type the name of the dataset followed by .Clear().
- 10. On a new line, type the data adapter's name followed by .Fill().

![](img/d6f772854306e15fb6df39b861a7b541_224_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_224_1.png)

Note: See the section “Bind a Control on a Form” to bind a control.
