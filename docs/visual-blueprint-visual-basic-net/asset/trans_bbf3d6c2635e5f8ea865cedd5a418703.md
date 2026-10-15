

## VISUAL BASIC .NET

## WORK WITH DATA TABLES

DataTable 对象表示单个信息表。您可以使用 DataTable 对象来操作 DataSet 中的表。就像数据库中的表一样，DataTable 对象存储包含各种列的行表示。DataSet 控件将从数据库表加载的信息存储到 DataTable 对象中。这允许数据库表从数据库连接加载到内存中，以便数据库随后断开连接。

您可以使用 TableName 属性访问对象所代表的表的名称。Columns 属性返回一个 DataColumnCollection 对象，其中包含表中每个列可用的字段。PrimaryKey 属性获取或设置用作表主键的 DataColumn 对象数组。有关 DataColumn 对象的更多信息，请参阅“Work with Data Columns”部分。

Rows 属性返回一个 DataRowCollection 对象，允许您访问各个记录。有关 DataRow 对象的更多信息，请参阅“Work with Data Rows”部分。

ChildRelations 属性维护一个由作为此表的子表的表列表组成的 DataRelationCollection。ParentRelations 属性返回相同的对象列表，其中包含作为此表的父表的表。有关数据表关系的更多信息，请参阅“Create a Data Relationships”部分。Constraints 属性在 ConstraintCollection 对象中维护关系所遵守的约束列表。

当您创建 DataSet 组件并让它为您生成可访问的表时，VB .NET 会自动创建此类的继承版本。此继承版本包含与该表的实际字段和记录相关的属性和方法。有关绑定控件、添加记录以及使用生成的表和 DataSet 组件更新信息的更多信息，请参阅“Bind a Control on a Form”部分。

## WORK WITH DATA TABLES

![](img/d6f772854306e15fb6df39b861a7b541_225_0.png)

- 1 Set up a database connection on the form.
- Note: See the sections "Create a Database Connect" and "Add a Connection to a Form" to set up a database.

- 2 In a method of the form, declare a variable of type DataTable.
- 3 Assign an expression formed by the name of the DataSet followed by a period and the name of the table to the variable.

- 4 Type ListBox1.Items.Add(myTable.Rows(0)), replacing ListBox1.Items.Add() with a method to display the data, myTable with the name of the table, and 0 with the row index to access.

- 5 Following Rows(0), type .Item("CompanyName"), replacing CompanyName with the name of the field to access.
- Note: To work with a DataRow, see the section "Work with Data Rows."

## Apply It

A fully functioning standalone component, the DataTable object does not need a database adapter connection to an actual database provider. You can declare an instance of a DataTable, define its columns using DataColumn objects and add DataRow objects to the table. Then you can use the DataTable to bind to controls as you do with the visual DataSet and provider components. See the section “Bind a Control on a Form” for more information.

## TYPE THIS:

```
Private Sub Form1_Load(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles MyBase.Load
Dim dt As New DataTable("MyTable")
dt.Columns.Add("Name", System.Type.GetType("System.String"))
dt.Columns.Add("Address", System.Type.GetType("System.String"))
Dim values() As String = {"John Doe", "123 Anytown Rd."}
dt.Rows.Add(values)
values(0) = "Aaron Smith"
values(1) = "456 South Rd."
dt.Rows.Add(values)
TextBox1.DataBindings.Add("Text", dt, "Name")
TextBox2.DataBindings.Add("Text", dt, "Address")
End Sub
```

## RESULT:

TextBox1: John Doe
TextBox2: 123 Anytown Rd.

![](img/d6f772854306e15fb6df39b861a7b541_226_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_226_1.png)

- 6 Type ListBox1.Items.Add(myTable.Columns(0)), replacing ListBox1.Items.Add() with the method to display the data, myTable with the table name, and 0 with the column index.

- 7 Following Columns(0), type a period followed by a method or property of the DataColumn.
- Note: To work with a DataColumn, see the section "Work with Data Columns."

- 8 Press F5 to run your project.

The DataTable object provides the necessary information about the table contents.

