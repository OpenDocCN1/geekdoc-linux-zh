
![](img/6e977c6eee8c1535039c864d41da5ccf_270_0.png)

- 源编辑器加载 `Page_Load` 事件。
- 10 填充 `DataGrid`。
- 11 输入 `If Not IsPostBack Then` 并回车。
- 12 `DataGrid` 的类型名称后接 `DataBind()` 是索引。
- 13 按 F5 运行你的项目。

`DataGrid` 显示相应的表格。

注意：要绑定控件，请参见第 9 章。请参见“更改 DataGrid 外观”章节以自定义网格。

# VISUAL BASIC .NET

## 修改 DATAGRID 的外观

有许多属性使 `DataGrid` 能够有效地显示数据，你可以使用 `DataGrid` 属性来设置列和边框方案以修改列的显示。有关如何向你的 Web 表单添加 `DataGrid` 服务器的更多信息，请参阅“添加 DataGrid 控制”章节。

以及其内容，`CellSpacing` 属性指定表格单元格之间的间距。或者，你也可以通过属性生成器的 Borders 页面来设置这些属性。

`ItemStyle` 和 `AlternatingStyle` 决定了网格中项的外观。如果不定义 `AlternatingStyle`，项将显示相同。如果你同时设置了这两个属性，表格中的项将在两种样式之间切换。`HeaderStyle` 定义了标题的外观，`FooterStyle` 定义了页脚的外观。你可以使用控件的属性生成器格式轻松编辑这些属性。

要自动为网格添加样式，请使用 Auto Format 对话框，它提供了许多预设的颜色编码设置。选择样式后，所有属性都将自动更新以反映更改。

你可以使用 `BorderWidth` 和 `BorderStyle` 为网格设置边框。`CellPadding` 属性指定单元格边缘的距离大小。

使用属性生成器对话框的 Columns 页面来指定表格显示的列。默认情况下，网格显示所有列。如果你想显示特定的列，可以将对话框中的“自动创建列”选项设置为 `False`。你也可以将 `AutoGenerateColumns` 属性设置为 `False` 以不生成列。控件包含了在 `Columns` 属性中要使用的列列表。

### 修改 DATAGRID 的外观

![](img/6e977c6eee8c1535039c864d41da5ccf_271_0.png)

- 1 在 Web 表单上配置 `DataGrid`。
- 2 右键点击列。
- 3 点击属性生成器（Property Builder）。
出现 `DataGrid` 属性对话框。
- 4 点击 Columns（列）。
- 5 点击 [x] 自动列标题
- 6 从列表中点击一个字段
- 7 点击 >> 添加列。
- 你可以编辑每列的显示属性。
- 8 点击 OK。
- 9 按 F5。
网格将生成相应的列标题。

注意：请查看“添加 DataGrid 控制”章节以添加 DataGrid 控件。

256

### 额外

在具有大量记录的表格中，你可能希望将记录分到多个页面。`DataGrid` 提供了分页功能，允许你指定每次显示的记录数。`DataGrid` 会自动生成一组分页链接。你通过 `AllowPaging` 属性指定每页显示的项数。`PageSize` 属性的默认页大小为 10。你可以使用 `PagerStyle` 属性修改分页器按钮的行为。你可以使用 `PagerStyle.Mode` 显示页码列表和上一页按钮。要使分页生效，必须由 `PageIndexChanged` 事件设置选定的页面并更新数据网格。

示例：
```vb
Private Sub DataGrid_SortCommand(ByVal source_ As Object, ByVal e As System.UI.Web.Controls.DataGridSortCommandEventArgs_)
Handles DataGrid.SortCommand
    DataView.Sort = e.SortExpression
    DataGrid.DataBind()
```

![](img/6e977c6eee8c1535039c864d41da5ccf_272_0.png)

### 选择自动格式样式

- 1. 执行上一页的第 2 和第 3 步，但在第 3 步点击 Autoformat（自动格式）。
- 2. 点击一个方案进行预览。
- 3. 按 F5 运行你的项目。

网格生成所选的样式。

# VISUAL BASIC .NET

## 在 DATAGRID 中编辑数据

你可能想向用户提供信息表，并让他们直接在 Web 上编辑数据库中的信息。`DataGrid` 可以自动提供控件来添加、编辑和更新数据库记录。由于 Web Forms 中的数据库绑定仅用于从数据库读取信息，你必须添加自己的代码来执行单独的编辑、更新和操作。

编辑行（Edit row）为用户更新记录的方法。当用户点击按钮时，网格会触发 `EditCommand` 事件，它不会自动启动。你必须设置 `DataGrid` 的 `EditItemIndex` 属性来聚合事件内部的项目。你可以使用事件参数的 `e.ItemIndex` 属性检索该项。你必须调用 `DataBind` 方法来更新网格。

你可以向 `DataGrid` 添加按钮以允许用户编辑记录。在属性生成器的可用列列表中，选择 Column。此选择为每列提供一个控件，一个编辑列和一个删除列，这些列作为网格中每个记录的超链接或按钮。

当你调用编辑时，用于记录更改的代码将显示取消（Cancel）和更新（Update）按钮。表格中每列的 VB .NET 控件。当用户选择其中按钮时，VB 会触发 `CancelCommand` 和 `UpdateCommand` 事件。要取消，将 `EditItemIndex` 属性设置为负数。要访问值，使用网格的 `Cell` 集合。.NET 在表格 `Controls` 集合的位置零定位每个单元格的 `TextBox`。

你可以为 `DataGrid` 添加 Select（选择）列以允许用户选择一行。`DataGrid` 会自动更新 `SelectedIndex` 属性并引发 `SelectedChanged` 事件。它显示 `SelectItemStyle`。

### 在 DATAGRID 中编辑数据

![](img/6e977c6eee8c1535039c864d41da5ccf_273_0.png)

- 1 配置 `DataGrid` 控件并打开属性生成器。
- 2 点击 Columns。
- 3 点击 Button Column 打开可用列。
- 4 点击 Edit、Update、Cancel 项。
- 5 点击 >
- 6 点击 OK。
- 5 输入 `DataGrid` 的名称，后跟 `DataBind(Data)`。
- 10 处理 `CancelCommand` 事件。

注意：查看“添加 DataGrid”控件以添加该控件。

注意：第 2 步用于创建事件程序。

- 8 输入 `DataGrid` 的名称，后跟 `e.Item.ItemIndex`。

258

### 额外

你可以使用 Delete（删除）列允许用户从数据库中删除项。当用户点击特定行的 Delete 时，网格会触发 `Delete` 事件，传递参数列表中的 `e.Item` 对象以确定要删除的项。如果你将 `DataKeyField` 设置为记录的唯一 ID，你可以通过 `DataGrid.DataKeys` 访问用户想要删除的条目的数据。示例：
```vb
Dim custID As String = DataGrid.DataKeys(e.Item.Index)
Dim rowID As DataRow = DataSet1.Customers.FindBy(custID)
DataSet1.Customers.Remove(rowID)
DataGrid.DataBind()
```
