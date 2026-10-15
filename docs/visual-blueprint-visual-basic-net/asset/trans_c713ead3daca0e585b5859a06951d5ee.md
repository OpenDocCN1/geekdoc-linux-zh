

# 额外

要手动创建 DataRelation 对象，您需要创建该类的一个实例，并将关系的名称作为第一个参数传递。第二个参数传递要在父表中链接的列，第三个参数传递要在子表中链接的列。创建 DataRelation 对象后，使用 Add 方法将其分配给 DataSet.Relations 对象。

要手动检索子表中关联的条目，请调用 DataRow 的 GetChildRows 方法，并将关系名称作为参数。 该方法返回一个 DataRow 对象数组，其中包含与父记录关联的子数据。 您也可以反向操作，并使用 DataRow 的 GetParentRows 方法检索与特定子行相关的父行。

## 示例：

```
Dim parentCol As DataColumn = DeNorthwind1.Customers.CustomerID
Dim childCol As DataColumn = DeNorthwind1.Orders.CustomerID
Dim relCustOrder As DataRelation
relCustOrder = New DataRelation("CustomersOrders", parentCol, childCol)
DeNorthwind1.Relations.Add(relCustOrder)
```

![](img/d6f772854306e15fb6df39b861a7b541_242_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_242_1.png)

- 5 点击 [...] 并选择用作父表的表。
- 6 点击 [...] 并选择用作子表的表。
- 7 点击您希望在父表中充当键的字段。
- 如果对话框未正确选择充当子项的字段，请点击正确的字段。
- 8 点击确定。

- 架构编辑器创建关系。
- 您也可以保存并关闭架构，以及添加控件以显示关系。

> 注：请参阅“添加 DataGrid 控件”部分以添加 DataGrid 控件，该控件能够原生显示具有关系的数据。

## 添加 DataGrid 控件

DataGrid 控件允许您为表或数据库查询提供可编辑的类似表格的界面。 您可以使用 DataGrid 在窗体上轻松提供编辑或查看功能，而无需为每个数据字段创建单独的编辑控件。 然而，在某些情况下，对于包含许多字段或大量记录的表，使用全是简单控件的窗体更有意义。 有关 DataGrid Web Forms 控件的信息，请参阅第 10 章。

您可以在工具箱的 Windows Forms 部分找到 DataGrid 控件。 您可以使用 DataSource 属性将控件链接到 DataSet、DataView 或 DataSet 内部包含的表。 网格会自动为绑定的网格创建必要的列。 如果您将网格直接链接到包含多个表的 DataSet 组件，则每个表都将以超链接显示，用户可以点击以访问各个表。 包含关系的表还为每一行提供超链接，以便访问与显示记录相关的子记录。 根据需要，控件顶部会出现一个返回按钮，以便移动到父表。 当您移动到子关系时，控件还会在标题中以单行滚动方式显示有关父记录的信息。

您可以通过点击列标题自动对网格进行排序。 您无需绑定到 DataView 控件即可支持排序。 您可以使用 AllowSorting 属性禁用排序。 您可以使用自动格式对话框为网格的外观设置样式。

当用户在网格中更改项目时，网格会自动更新 DataSet 或 DataView 内部关联的 DataTable。 您必须手动保存对数据库的更改。 有关将更改的信息保存到数据库的更多信息，请参阅“在 DataSet 中移动”部分。

## 添加 DataGrid 控件

![](img/d6f772854306e15fb6df39b861a7b541_243_0.png)

- 1. 在窗体上设置数据库连接和数据集。

  注：请参阅“创建数据库连接”和“向窗体添加连接”部分以设置数据库。

- 2. 点击并拖动 DataGrid 控件从工具箱的 Windows Forms 部分到窗体。

- 3. 点击 DataSource 属性并选择要显示的 DataSet 控件或表。

- 4. 设置任何必要的属性。

  注：要设置属性，请参阅第 2 章。

- 5. 要格式化网格的外观，请右键单击窗体上的 DataGrid 控件。

- 6. 点击自动格式。

