
## 额外

![](img/6e977c6eee8c1535039c864d41da5ccf_240_0.png)
![](img/6e977c6eee8c1535039c864d41da5ccf_240_1.png)

- 6 定义一个表示步骤 6 中确定的当前行的变量。

注意：选择“处理数据行”以获取更多关于数据行的信息。

- 7 使用 `row.SetColumnError("CustomerID", errMsg)`，替换为列名和错误字符串。
- 8 在新行上，输入 `e.Cancel = True`。
- 9 在输入控件的 `Validated` 事件中，在步骤 6 之后输入此内容，将 `errMsg` 替换为 ""。

当您运行项目并输入无效值时，会出现带有适当描述的错误图标。

# VISUAL BASIC .NET

## 创建数据关系

大多数情况下，数据库的单个表并不存储构建应用程序所需数据的所有信息。不同的表存储信息的不同部分，您将来自表的数据组合，创建一个允许用户有效地修改所有数据的应用程序。您可以在您的 Visual Basic .NET 应用程序中使用 XSD 定义关系。

例如，如果您有一个包含 Orders（订单表）和 Customers（客户表）的数据库，Orders 表存储了用户使用的所有订单。您可以使用关系将订单附加到 Customers 表中的特定客户。VB .NET 允许您在应用程序中视觉化地设置 `DataRelation` 类，并编辑数据集以存储您添加到 `DataSet` 的各种表。

`DataSet` 对象，请参阅“向表单添加连接”章节。

当您访问“添加关系”对话框时，它允许您选择两个表以及表之间匹配的字段以创建关系。在您的示例中，将 Customers 表中的 `CustomerID` 字段链接到 Orders 表中的 `CustomerID` 字段。您还可以选择哪一个表作为父表（父表是允许接收子表中多条匹配记录的表）。例如，Customers 表是父表，因为多个订单匹配同一个客户。

一旦创建了关系，网格将显示父级记录和子记录。更多信息，请参阅“向表单添加连接”章节。

## 创建关系

![](img/6e977c6eee8c1535039c864d41da5ccf_241_0.png)

- 1. 选择父表和子表。
- 2. 链接表之间的匹配字段。
- 3. 使用 `DataView` 显示关系。
- 4. 定义关系名称。
- 5. 将关系添加到 `DataSet`。

## ADO.NET

与其验证 `ErrorProvider`，可以使用 `DataTable` 对象通过 `ColumnChanging` 事件对表的每条记录执行验证。因为 `DataSet` 组件没有手动事件处理器，您必须定义两个参数：一个 `Object` 变量和一个 `DataChangeEvent` 对象。您可以通过 `e.Column` 访问触发的事件。要引起验证错误，传递一个 `New Exception` 对象并传递错误消息的构造函数。然后使用 Command 传递异常对象。

示例：
```vb
Dim relOrder As DataRelation

Dim parentCol As DataColumn

Dim childCol As DataColumn

relOrder = New DataRelation("Orders", parentCol, childCol)

DataSet.Relations.Add(relOrder)
```
