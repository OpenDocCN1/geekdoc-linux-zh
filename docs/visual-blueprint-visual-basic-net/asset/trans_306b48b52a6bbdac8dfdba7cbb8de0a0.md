

## Extra

当用户在列表控件中选择一个项目时，SelectedIndexChanged 事件会触发。您可以处理此事件以根据用户选择的项目加载信息。ListBox.SelectedItem.Value 属性包含数据库分配的值 ID。SelectedIndexChanged 事件不是四个控件中的任何一个的回发事件。您可以通过将 AutoPostBack 属性设置为 True 来使列表控件回发到服务器并立即触发 SelectedIndexChanged 事件。

### Example:

```
Private Sub ListBox1_SelectedIndexChanged(ByVal sender As Object, _
ByVal e As System.EventArgs) Handles ListBox1.SelectedIndexChanged
Dim custID As String              ' get the selected item's value
custID = ListBox1.SelectedItem.Value   ' to find the entry in the database
' search the database for the selected ID
Dim rs As DataRow = DataSet1.Customers.FindByCustomerID(custID)
Label1.Text = rs("Address")       ' display the information from
Label2.Text = rs("City")         ' the database
Label3.Text = rs("State")
Label4.Text = rs("Zip")
End Sub
```

![](img/d6f772854306e15fb6df39b861a7b541_268_0.png)

6 源编辑器加载 Page_Load 事件。

7 输入代码以填充 DataSet。
注意：要使用 DataSet 对象，请参阅第 9 章。

8 输入 If Not IsPostBack Then 并按 Enter。

9 在 If 块内输入列表控件的名称后跟 .DataBind()。

10 按 F5 运行您的项目。

列表 Web 服务器控件显示表的适当字段。

## ADD A DATAGRID CONTROL

您可能想要创建一个显示信息表的 Web 应用程序项目，如产品列表或杂志中的文章列表。您可以使用 DataGrid 控件轻松显示来自数据集的完全自定义的信息表。

Web Forms DataGrid 控件呈现一组数据的标准 HTML 表格。您使用 DataSource 属性将 DataSet 或 DataView 组件链接到网格。您必须在使用之前填充数据集。请参阅第 9 章以了解如何创建数据库连接。

Web DataGrid 服务器控件只有在您调用其 DataBind 方法时才会填充。否则，它使用缓存的数据。如果您在回发时调用该方法，例如，如果用户选择一个项目，则在调用 DataBind 时事件会丢失。因此，请确保仅在 Page 的 IsPostBack 为 False 时在 Page_Load 事件中调用 DataBind，这意味着页面首次加载。

您使用 DataGrid 的 Property Builder 对话框，该对话框有五个页面，来设置其所有主要属性。第一页 General 设置数据源。您需要将 DataSource 属性设置为包含要绑定的表的 DataSet 或 DataView 组件。DataMember 指定要显示的表。将 DataKeyField 设置为数据库的键字段，即记录中唯一的字段。您可以使用键字段轻松找到用户选择的数据库中的记录。

其他属性页面使您可以更改网格的外观和功能。有关设置控件的外观和列的更多信息，请参阅“更改 DataGrid 的外观”部分。

![](img/d6f772854306e15fb6df39b861a7b541_269_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_269_1.png)

- 1. 创建新的 Web 应用程序项目或打开现有项目。
- 2. 添加适当的 DataSet 或 DataView。
- 3. 在工具箱中单击 DataGrid 控件并将其添加到窗体。
- 4. 右键单击控件然后单击 Property Builder。
- 注意：请参阅第 9 章以添加数据库连接。请参阅“使用 Web 表单”部分以添加控件。
- 5. 对于 DataSource，单击并选择数据控件。
- 6. 如果您使用 DataGrid，请为 DataMember 选择正确的表。
- 7. 为 Data key field 选择适当的唯一 ID 字段。
- 8. 单击 OK。
- 9. 在网格外部双击 Page。

## Extra

在大多数现代应用程序和网站中，用户期望对表中的不同列进行排序。DataGrid 可以在标题中的每个字段名称上提供超链接以启用排序。您可以通过在 Property Builder 中的 General 属性页上选中 Allow sorting 复选框来排序。或者，您可以在属性工具窗口中启用 AllowSorting 属性。排序的字段会自动返回到 SortCommand 事件中，该事件在用户单击其中一个列标题时触发。事件对象传递一个包含要排序字段的 SortExpression 属性。您可以在 Property Builder 中更改特定列使用的排序字段。为了提供排序功能，您必须将网格绑定到 DataView 组件，该组件不执行任何排序或筛选功能。要创建 DataView 组件，请参阅第 9 章。

### Example:

```
Private Sub DataGrid1_SortCommand(ByVal source As Object, _
    ByVal e As System.Web.UI.WebControls.DataGridSortCommandEventArgs) _
    Handles DataGrid1.SortCommand

    DataView1.Sort = e.SortExpression
    DataGrid1.DataBind()

End Sub
```

![](img/d6f772854306e15fb6df39b861a7b541_270_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_270_1.png)

源编辑器加载 Page_Load 事件。

10 填充 DataSet。
注意：要绑定控件，请参阅第 9 章。

11 输入 If Not IsPostBack Then 并按 Enter。

12 在 If 块内输入 DataGrid 的名称后跟 .DataBind()。

13 按 F5 运行您的项目。

DataGrid 显示适当的表。

注意：请参阅“更改 DataGrid 的外观”部分来自定义网格外观。

