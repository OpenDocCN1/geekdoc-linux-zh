# VISUAL BASIC .NET

# WORK WITH DATA TABLES

The DataTable object represents a single table of information. You can use the DataTable object to work with the tables in a DataSet. Much like a table in a database, the DataTable object stores a representation of rows that contain various columns. A DataSet control stores the information it loads from a database table into a DataTable object. This allows the database table to load from the database connection into memory, so the database can then disconnect.

You can access the name of the table represented by the object using the TableName property. The Columns property returns the fields available for each column of the table in a DataColumnCollection object. The PrimaryKey property gets or sets an array of DataColumn objects that act as the primary keys for the table. For more information about the DataColumn object, see the section “Work with Data Columns.”

The Rows property returns a DataRowCollection object that allows you to access the individual records. For more information on the DataRow object, see the section “Work with Data Rows.”

The ChildRelations property maintains a DataRelationCollection made up of the list of tables that function as children to this table. The ParentRelations property returns the same object list containing the tables that function as parents to this table. For more information on data-table relationships, see the section “Create a Data Relationships.” The Constraints property maintains the list of constraints that the relationship abides by in a ConstraintCollection object.

When you create a DataSet component and have it generate tables for you to access, VB .NET automatically creates an inherited version of this class. This inherited version contains properties and methods that relate to the actual fields and records of that table. For more information on binding controls, adding records, and updating information using the generated tables and the DataSet component, see the section “Bind a Control on a Form.”

# WORK WITH DATA TABLES

![](bbox=[0.07, 0.62, 0.92, 0.85])

+   1 Set up a database connection on the form.
+   Note: See the sections "Create a Database Connect" and "Add a Connection to a Form" to set up a database.

+   2 In a method of the form, declare a variable of type DataTable.
+   3 Assign an expression formed by the name of the DataSet followed by a period and the name of the table to the variable.

+   4 Type ListBox1.Items.Add(myTable.Rows(0)), replacing ListBox1.Items.Add() with a method to display the data, myTable with the name of the table, and 0 with the row index to access.

+   5 Following Rows(0), type .Item("CompanyName"), replacing CompanyName with the name of the field to access.
+   Note: To work with a DataRow, see the section "Work with Data Rows."