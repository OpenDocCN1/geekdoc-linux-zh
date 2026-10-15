
- 示例使用筛选器 `ContactName LIKE 'A%'` 来检索以 A 开头的联系人。

### 额外

您可以使用提供的方法和属性修改与 `DataView` 关联的表。`AllowEdit`、`AllowNew` 和 `AllowDelete` 属性分别指定 `DataView` 是否允许您编辑字段值、添加新记录和删除记录。您可以使用 `AddNew` 方法向 `DataView` 的底层表添加记录。该方法返回一个新的 `DataRowView` 对象。使用此对象编辑新行的各个记录。`Delete` 方法删除您作为方法唯一参数指定的行。当您删除该行时，其状态更改为 `DataViewRowState.Deleted`。

您可以使用 `DataViewRowState` 枚举中的常量与 `RowStateFilter` 属性一起使用以筛选 `DataView` 中的记录。

| CONSTANT | DESCRIPTION |
|---|---|
| Added | 自上次保存或接受更改以来您添加的行。 |
| CurrentRows | 当前行，包括未更改、新建和已修改的行。 |
| Deleted | 自上次保存或接受更改以来您删除的行。 |
| ModifiedCurrent | 您已修改的行的当前版本。 |
| ModifiedOriginal | 您已修改的行的原始版本。 |
| OriginalRows | 所有原始行，包括未更改和已删除的行。 |
| Unchanged | 一个未更改的行。 |

![](img/d6f772854306e15fb6df39b861a7b541_232_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_232_1.png)

6 添加查看 `DataView` 中包含的数据的适当方式。

注：要向窗体添加绑定控件，请参阅“在窗体上绑定控件”部分。

示例添加了一个数据绑定到 `DataView` 组件的 `ListBox` 控件。

`DataView` 在使数据可用之前执行适当的排序或筛选。

## 在窗体上绑定控件

在访问数据时，通常需要允许用户编辑这些数据。VB .NET 在每个控件中都提供了可将其属性自动连接到数据字段的功能。通过绑定，你可以非常快速地将窗体连接到数据库，而无需编写大量代码。

绑定主要有两种类型：简单绑定和复杂绑定。大多数控件支持其中一种类型。简单绑定将单条记录中的单个字段连接到控件属性。例如，可以将数据库中的 `LastName` 字段链接到文本框，以便查看和编辑。复杂绑定则绑定整个数据集，无论是记录列表中的单个字段，还是整个数据表。

简单绑定通过支持该绑定的控件中的 `DataBindings` 属性发挥作用。该属性存储一组 `Binding` 对象，这些对象将控件中的属性链接到 `DataSet` 字段。Visual Basic .NET 允许你通过控件的属性页创建相应的 `Binding` 对象。你只需选择要绑定到控件的字段即可。

若要通过复杂绑定处理记录列表，可以使用 `ListBox`、`ComboBox` 或 `CheckedListBox`。这些控件都会显示 `DataSet` 提供的记录列表。将 `DataSource` 属性设置为有效的 `DataSet`，并将 `DisplayMember` 属性设置为要显示的字段。通常，可以使用 `ListBox` 和 `ComboBox` 控件显示要编辑的记录列表。有关选择活动记录的信息，请参阅“在数据集中移动”一节。

`ErrorProvider` 控件也使用复杂绑定来监视 `DataSet` 中的错误。该控件监视字段中的数据，并自动在包含该字段绑定的控件旁边显示错误图标。有关 `ErrorProvider` 的更多信息，请参阅“验证数据”一节。

![](img/d6f772854306e15fb6df39b861a7b541_233_0.png)

### 创建窗体

- 在窗体上设置数据库连接和数据库…
- 向窗体添加合适的控件。

> 注意：有关设置数据库的信息，请参阅“创建数据库连接”和“向窗体添加连接”两节。有关向窗体添加控件的更多信息，请参阅第 3 章。

### 绑定简单控件

- 在“属性”窗口中，单击 `(DataBindings)` 左侧的 `+`。
- 在 `DataBindings` 部分中，单击要绑定数据的属性。
- 单击 `...`，然后选择要绑定的相应字段。

### 补充

如果通过代码创建 `DataSet`、`DataView` 或 `DataTable` 组件，而不使用可视化设计器，你可能仍希望将其绑定到控件。你可以使用本主题中讨论的属性将组件绑定到控件。对于简单对象，向 `DataBindings` 集合属性添加 `Binding` 类的新实例。

**示例：**

```vbnet
Dim myDataTable As New DataTable("MyTable")
myDataTable.Columns.Add("MyField")
Dim myData As DataRow = myDataTable.NewRow()
myData.Item("MyField") = "Test"
myDataTable.Rows.Add(myData)
Dim bindText As New Binding("Text", _
    myDataTable, "MyField")
TextBox1.DataBindings.Add(bindText)
```

可以将 `DataGrid` 等复杂控件绑定到数据组件，而无需使用设计器。

**示例：**

```vbnet
Dim myDataTable As New DataTable("MyTable")
myDataTable.Columns.Add("MyField")
Dim myData As DataRow = _
    myDataTable.NewRow()
myData.Item("MyField") = "Test"
myDataTable.Rows.Add(myData)
Dim myData2 As DataRow = _
    myDataTable.NewRow()
myData2.Item("MyField") = "Test Item 2"
myDataTable.Rows.Add(myData2)
DataGrid1.DataSource = myDataTable
```

### 绑定复杂控件

- 单击控件的 `DataSource` 属性，然后选择适当的表。
- 单击 `DisplayMember` 属性以显示列表。
- 按 `F5` 运行项目。

控件将绑定到数据集并显示第一条可用记录。

注意：请参阅“在数据集中移动”一节，以允许更改并提供控件的移动功能。

![](img/d6f772854306e15fb6df39b861a7b541_234_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_234_1.png)

## 遍历数据集

要有效地使用绑定的控件，必须让用户能够在 `DataSet` 中的可用记录之间移动。通常，窗体包含单个记录的信息，而前后控件通常使用户能够遍历记录。例如，客户数据库可能存储有关客户的所有信息。屏幕提供文本框来显示数据并允许更改数据。

要在窗体上添加移动控件，需要使用窗体上提供的 `BindingContext` 对象。要访问窗体的 `BindingContext`，请使用 `Me.BindingContext` 属性。该对象保存窗体上所有绑定数据集的列表。你将 `DataSet` 的名称和表的名称作为两个参数传递给该方法。它返回一个与参数匹配的 `BindingManagerBase`。`BindingManagerBase` 对象同步引用同一数据源的所有 `Binding` 对象。`Position` 属性控制绑定控件显示的位置。该属性以零为基准，这意味着使用 `Position = 0` 访问第一个可用记录。`Count` 属性返回绑定中可用的记录数，因此要移动到列表末尾，将 `Position` 设置为 `Count - 1`。

![](img/d6f772854306e15fb6df39b861a7b541_235_0.png)

- 1. 在窗体上设置数据库连接。
- 2. 在窗体上放置必要的绑定输入控件。
- 3. 包含一个按钮以转到第一条记录、后退一条记录、向前一条记录以及转到最后一条记录。
- 4. 双击适当的按钮以添加事件处理程序。

> 注意：请参阅“在窗体上绑定控件”部分以绑定控件。

- 5. 对于第一条记录按钮，键入 `Me.BindingContext(DsNorthwind1, "Customers").Position = 0`，将 `DsNorthwind1`、`"Customers"` 替换为 `DataSet` 和表。
- 6. 对于上一条记录按钮，键入 `Me.BindingContext(DsNorthwind1, "Customers").Position -= 1`，将 `DsNorthwind1`、`"Customers"` 替换为 `DataSet` 和表。

## 应用它

你可以使用以下过程让用户查看其在数据集中的当前位置。你在数据初始加载时调用此过程，并在用户按下按钮并更改 `Position` 属性后调用。

### 输入以下内容：
