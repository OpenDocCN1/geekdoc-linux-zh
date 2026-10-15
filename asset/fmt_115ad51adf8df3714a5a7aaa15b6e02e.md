
# 第 13 章：客户端数据管理

上述代码展示了如何通过姓氏或员工 ID 执行员工搜索。变量 `SearchFields` 指定了应搜索结果集中的哪个字段。注意变量的名称是 `SearchFields` 而不仅仅是 `Field`。这是因为 `Locate` 方法的 `KeyFields` 参数可以接受一个由分号分隔的字段列表以进行搜索。如果要在多字段索引上执行搜索，这特别有帮助。要传递多个待搜索的值，你必须创建一个这些值的变体数组（variant array）。例如，要在给定部门中搜索所有姓为 "Smith" 的员工，使用 `Locate` 方法的方式如下：

```php
if not clntdstEmployee.Locate('Last_Name;Dept_No', ArrayOf(['Smith',600]),SearchValue,[CaseInsensitive, loPartialKey]) then MessageDlg('未找到员工', '找不到指定的员工。',mtError,[mbOK],0);
```

`Locate` 方法的第三个参数是 `LocateOptions` 参数。`LocateOptions` 是一组 `TLocateOption` 值，共有两个。`loInsensitive` 导致搜索不区分大小写。`loPartialKey` 允许搜索进行部分匹配。它的行为与 `FindNearest` 方法相同。默认情况下搜索是区分大小写且精确匹配的。开发者必须包含其中一个或两个选项来更改搜索行为。

## 编辑数据

大多数情况下，数据是从数据库检索以用于编辑的。持有客户端侧数据的 `ClientDataSet` 始终处于几种状态之一（即 `dsEdit`）。可以随时检查只读属性 `State` 来确定数据集的状态。虽然有很多种状态，但开发者最常用的三个状态是 `dsBrowse`、`dsEdit` 和 `dsInsert`。当数据集提交（post）或取消（cancel）时，表将进入浏览模式（browse mode）。在进行编辑或正在插入记录时，数据集分别处于 `dsEdit` 或 `dsInsert` 状态。（有关数据集状态 `State` 的更多信息，请参阅 Kylix 帮助文件）。

Kylix 中的数据感知控件通常控制着数据集的变化。当 `AutoEdit` 设置为 `true`（这是默认值）时，对数据感知控件的任何更改都会自动将表置于 `dsEdit` 状态（如果尚未处于该状态）。这减轻了开发者手动通过方法（如 `insert`、`edit` 等）切换表状态的负担。

在某些应用程序中，要求用户通过击键或点击按钮显式将数据集置于编辑模式。要通过编程更改状态，请使用 `Insert`、`Append` 或 `Edit` 方法。一旦数据集处于 `dsInsert` 或 `dsEdit` 状态，开发者可以调用 `Post` 或 `Cancel` 方法将数据集返回浏览模式。

提示：如果必须在后台添加记录（而不让用户显式添加值），可以使用 `InsertRecord` 方法。`InsertRecord` 方法接受一个表示新记录值的数组参数。该记录被插入数据集中并执行一次 `post`。`procedure InsertRecord(const values: array of const);`

## 解决数据更新

### 缓存更新 (Cached Updates)

当编辑提交到 `ClientDataSet` 时，更改会被存放在客户端的本地缓存中。`ClientDataSet` 的 `Delta` 属性跟踪对数据的每次更改。要永久将更改应用到 `ClientDataSet` 缓存，请调用 `ApplyUpdates` 方法。`ApplyUpdates` 尝试将缓存的内容保存到数据库。它接受一个参数 `MaxErrors`，决定在停止更新过程之前允许多少错误。要在更新期间允许无限数量的错误，将 `MaxErrors` 设置为 -1。

注意：缓存更新数据集。它们将一组语句视为逻辑单元；要么全部成功，要么全部失败。与 BDE 的 `TTable` 和 `TQuery` 组件不同，ClientDataSets 始终使用缓存更新。一旦对 `ClientDataSet` 进行了更改，可以使用两种方法取消。调用 `CancelUpdates` 后，`ClientDataSet` 的 `Delta` 属性为空。要取消某条记录，调用 `RevertRecord` 方法。`RevertRecord` 只影响缓存中存在的更改。一旦记录被提供程序应用或合并到 `ClientDataSet`，将无法影响它。

#### 应用多个缓存

当应用程序同时编辑多个表（例如，用户从 GUI 编辑两个不同的表）时，会更新多个缓存。如果必须作为逻辑单元应用缓存，则需要事务。在此示例中，销售人员返回时输入新客户。要作为逻辑单元应用多个缓存，请在单个事务中调用每个缓存的 `ApplyUpdates`。

```php
procedure TfrmSalesEntry.ApplyChanges;
begin
sqlSqctMain.StartTransaction(Trans)
try
tdstCustomers.Applyupdates(0);
clstSales.ApplyUpdates(0);
sqlSqctMain.Commit(Trans)
except on EDatabaseException do
sqlSqctMain.Rollback(Trans)
end;
end;
```

注意：在 BDE 中，`TDatabase` 组件包含一个 `ApplyUpdates` 方法，接受一组可能应用的数据集。`SQLConnection` 组件不包含此类。需要显式事务。

## 传递更新参数

在数据解析过程中，Kylix 允许 `ClientDataSet` 和提供程序在交互时传递自定义信息。提供程序和数据集为 `Before/After GetParams`、`GetRecords`、`RowRequest`、`ApplyUpdates` 和 `Execute` 生成事件（提供程序还会生成 `AfterUpdateRecords` 事件）。这些方法的每个处理程序都指定了 `OwnerData` 参数。`OwnerData` 是一个 `OleVariant`，可以持有各种数据类型。通过 `OwnerData`，开发者可以在组件之间来回地传递自定义信息。

例如，`ClientDataSet` 可能希望随更新一起传递当前用户 ID，以协助提供程序确定如何应用更新。一旦更新完成，提供程序可能希望通知 `ClientDataSet` 某些自定义信息，例如操作影响的行数。

```php
procedure Tform1.ClientDataSet1BeforeApplyUpdates(Sender: TObject; var OwnerData: OleVariant);
begin
OwnerData := GetCurrentUserId;
end;
```

```pascal
procedure TForm1.DataProvider1BeforeApplyUpdates(Sender: TObject; var OwnerData: OleVariant; var RowsAffected:Integer;
begin
  if OwnerData = 'ewhipple' then
    { 实现用户特定的逻辑 ... }
  OwnerData := RowsAffected;
end;
```

```pascal
procedure TForm1.DataProvider1AfterApplyUpdates(Sender: TObject; var OwnerData: OleVariant;
begin
  MessageDlg(OwnerData + 'rows affected'; [mbOk], 0);
end;
```
