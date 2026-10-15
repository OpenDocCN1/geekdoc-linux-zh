
```vb
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

### 结果：

5 of 36

![](img/d6f772854306e15fb6df39b861a7b541_236_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_236_1.png)

7 对于下一条记录按钮，键入 `Me.BindingContext (DsNorthwind1, "Customers").Position += 1`，将 `DsNorthwind1`、`"Customers"` 替换为 DataSet 和表。

8 对于最后一条记录按钮，键入 `Me.BindingContext (DsNorthwind1,"Customers").Position = DsNorthwind1.Customers.Count -1`，将 `DsNorthwind1`、`"Customers"` 替换为 DataSet 和表，并将 `.DsNorthwind1.Customers` 替换为数据表。

9 按 `F5` 运行你的项目。

你可以单击按钮在表中存在的记录之间移动。

## 使用绑定控件编辑数据

要使你的数据库应用程序真正有用，可以允许用户不仅浏览记录，还可以更新其内容。使用绑定控件允许用户轻松地向数据库添加、编辑和更新记录。

`DataSet` 将用户对记录所做的所有更改保存在内存中。因此，要更新实际数据库，需要将更改写回数据库。`OleDbDataAdapter` 或 `SqlDataAdapter` 控件访问数据库并维护执行更新所需的 SQL 命令。调用 `DataAdapter.Update` 方法以保存 `DataSet` 中的更改。对于 `Update` 方法的两个参数，将 `DataSet` 对象作为第一个参数传递，然后将要更新的表的名称作为字符串传递。参阅“验证数据”部分以了解如何检查 `DataSet` 中的错误。

当你使用设计器将表添加到 `DataSet` 时，`DataSet` 会生成自定义类来表示表，创建与实际表和字段名称匹配的方法和属性。在本节的方法和对象中，将 `Table` 文本替换为要使用的表的实际名称。要向 `DataSet` 中的表添加新记录，请插入表的 `AddTableRow` 方法。对于参数，你可以指定一个 `TableRow` 对象，也可以为方法指定每个字段的单独参数。`NewTableRow` 方法返回一个使用数据库中的适当默认值设置的行，因此你可以使用它传递给 `AddTableRow` 方法。

例如，如果你的表称为 `Customers`，设计器会在 `DataSet` 内创建一个名为 `Customers` 的类以匹配表名。然后，`Customers` 类的方法包括 `NewCustomersRow`、`AddCustomersRow` 等。

![](img/d6f772854306e15fb6df39b861a7b541_237_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_237_1.png)

- 1. 设置一个具有适当输入和移动控件的窗体。
- 2. 在窗体上放置一个按钮，供用户添加和更新数据库行。
- 3. 双击按钮进入代码编辑器并指定事件处理程序。
- 代码编辑器窗口出现。
- 4. 要更新数据库，键入 `SqlDataAdapter1.Update(DsNorthwind1)`，将 `SqlDataAdapter1` 替换为窗体上的数据适配器名称，将 `DsNorthwind1` 替换为绑定控件的 `DataSet`。
- 5. 在新行上，键入 `DsNorthwind1.AcceptChanges()`，将 `DsNorthwind1` 替换为 `DataSet` 的名称。

> 注意：要绑定控件，请参阅“将控件绑定到窗体”部分。要创建移动控件，请参阅“遍历数据集”部分。

## 附加内容

要从 `DataSet` 中的表删除记录，请访问表对象并使用 `RemoveTableRow` 方法，将 `Table` 替换为表的名称。你必须传递要删除的行。可以使用表对象的 `Rows` 属性按索引号访问某一行。在括号中将要删除行的索引（从零开始）传递给 `Rows` 属性，它将返回一个 `DataRow` 对象。有关 `DataTable` 对象的更多信息，请参阅“使用数据表”。由于该行已不存在，你需要更新窗体显示的位置。有关使用 `BindingContext` 的更多信息，请参阅“在数据集中移动”。

#### 示例：

```vb
Dim pos As Integer = Me.BindingContext(DeNorthwind1, "Customers").Position
Dim row As DataRow = DeNorthwind1.Customers.Rows(pos)
DeNorthwind1.Customers.RemoveCustomersRow(row)
Me.BindingContext(DeNorthwind1, "Customers").Position -= 1
```

![](img/d6f772854306e15fb6df39b861a7b541_238_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_238_1.png)

- 要添加新行，请声明一个 `DataRow` 类型的变量。
- 键入 `DsNorthwind1.Customers.NewCustomersRow()`，将 `DsNorthwind1` 替换为 `DataSet` 的名称，将 `Customers` 替换为表的名称。
- 为不接受 null 值的字段赋值。
- 键入表名，后跟 `.AddTableRow(row)`，将 `Table` 替换为表名，将 `row` 替换为第 5 步中声明的变量。

当运行项目时，你可以添加、编辑和更新数据库中的信息。

## 验证数据

数据库包含针对其所含数据的特定规则。当用户输入数据时，他们可能不了解数据源的要求。你可以在允许用户将数据更新到数据库表之前验证数据，从而防止 Windows 应用程序中出现错误。

`ErrorProvider` 控件管理 `DataSet` 错误。有关将 `ErrorProvider` 控件添加到 Windows 窗体的信息，请参阅第 3 章。要使用 `ErrorProvider` 控件验证数据，请将其 `DataSource` 属性设置为你希望监视的 `DataSet` 或 `DataTable`。如果使用 `DataSet`，还必须将 `DataMember` 设置为要监视的表。

在窗体代码中，必须将 `ErrorProvider` 控件的 `ContainerControl` 属性设置为该窗体，数据验证才会发生。若要检查用户编辑的控件是否存在验证问题，请使用输入控件的 `Validating` 事件，该事件在用户离开输入控件时触发。

检测到错误时，请将事件参数 `e.Cancel` 设置为 `True`，控件将允许用户重新输入数据。然后，你可以向表示用户出错行的 `DataRow` 发出警报。使用 `BindingContext` 的 `Position` 属性确定当前行。有关 `BindingContext` 对象的详细信息，请参阅“在数据集中移动”一节。

找到相应的行后，调用 `DataRow` 对象的 `SetColumnError` 方法。将列和错误消息作为两个参数提供。有关 `DataRow` 对象的详细信息，请参阅“处理数据行”一节。

你还需要响应控件的 `Validated` 事件，在该事件中输入验证成功时要运行的代码。仅当未在 `Validating` 事件中将 `Cancel` 设置为 `True` 时，此事件才会运行。若要移除错误消息，请再次使用 `SetColumnError`，并将错误消息设置为空字符串。

![](img/d6f772854306e15fb6df39b861a7b541_239_0.png)

- 设置一个包含输入控件和移动控件的窗体，并在窗体上添加一个 `ErrorProvider` 控件。

注意：若要绑定控件，请参阅“将控件绑定到窗体”。若要创建移动控件，请参阅“在数据集中移动”。若要添加 `ErrorProvider` 控件，请参阅第 3 章。

- 对于 `ErrorProvider` 控件，单击 `DataSource` 属性并选择相应的数据集组件。对于 `DataSet`，单击 `DataMember` 并选择相应的表。
