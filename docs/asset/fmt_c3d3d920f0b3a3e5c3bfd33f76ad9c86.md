
```pascal
Log('TClientDataSet.AfterGetRecords');
end;

procedure TfrmMain.ClientDataSet1AfterRefresh(DataSet: TDataSet);
begin
    Log('TClientDataSet.AfterRefresh');
end;

procedure TfrmMain.ClientDataSet1AfterRowRequest(Sender: TObject;
    var OwnerData: OleVariant);
begin
    Log('TClientDataSet.AfterRowRequest');
end;

procedure TfrmMain.ClientDataSet1BeforeApplyUpdates(Sender: TObject;
    var OwnerData: OleVariant);
begin
    Log('TClientDataSet.BeforeApplyUpdates');
end;

procedure TfrmMain.ClientDataSet1BeforeExecute(Sender: TObject;
    var OwnerData: OleVariant);
begin
    Log('TClientDataSet.BeforeExecute');
end;

procedure TfrmMain.ClientDataSet1BeforeGetParams(Sender: TObject;
    var OwnerData: OleVariant);
begin
    Log('TClientDataSet.BeforeGetParams');
end;

procedure TfrmMain.ClientDataSet1BeforeGetRecords(Sender: TObject;
    var OwnerData: OleVariant);
begin
    Log('TClientDataSet.BeforeGetRecords');
end;

procedure TfrmMain.ClientDataSet1BeforeRefresh(DataSet: TDataSet);
begin
    Log('TClientDataSet.BeforeRefresh');
end;

procedure TfrmMain.ClientDataSet1BeforeRowRequest(Sender: TObject;
    var OwnerData: OleVariant);
begin
    Log('TClientDataSet.BeforeRowRequest');
end;

procedure TfrmMain.btnClearEventLogOnClick(Sender: TObject);
begin
  lbEvents.Items.Clear;
end;
end.
```

在您的计算机上运行两个该应用程序的实例。在第一个实例中，将 John 的名更改为 Eddie 并应用更新。在第二个实例中，请注意记录中仍然显示名为 John。将 John 的姓更改为 Smith 并应用更新。`OnReconcileError` 事件将触发，指示记录在期间已被其他人修改（参见图 7.3）。

![](img/52a35759a0f10dade27a840504be5d82_302_0.png)

## 图 7.3

*Delphi 的协调错误处理程序允许用户决定如何处理记录冲突。*

默认情况下，此对话框仅显示冲突的值——换句话说，即被其他用户修改的字段。取消勾选`仅显示冲突字段`复选框以显示所有字段值。如果这样做，您将看到此应用程序将 `LAST` 字段从 Lombardo 更改为 Smith。另一个应用程序将 `FIRST` 字段从 John 更改为 Eddie。

对话框的右上角包含一组选项按钮，用户可以使用它们来指示 Delphi 如何处理错误。这些选项按钮对应于 `TReconcileAction` 的 `raSkip`、`raCancel`、`raCorrect`、`raRefresh` 和 `raMerge` 值。列表中不包含 `raAbort` 选项，但单击取消按钮会导致事件处理程序返回 `raAbort` 值。

与本书中介绍的其他几个示例应用程序一样，Updates 应用程序包含一个事件日志列表框，它显示数据集提供者和客户端数据集何时以及以什么顺序触发有趣的事件。这些事件在本章稍后标题为“提供者事件”的部分中进行了讨论。

### 解决 BLOB 字段的更改

`TDataSetProvider` 不会自动检查 BLOB 字段（包括备忘录）的冲突。如果两个用户更改了 BLOB 字段或备忘录的内容，第二个用户的更改将无声无息地覆盖第一个用户的更改。

处理这种情况的最佳方法可能是为每个 BLOB 字段在数据库中增加一个相应的整数字段。整数字段包含 BLOB 字段的“更新编号”。例如，如果数据库表包含名为 `IMAGE` 的列，则添加一个名为 `IMAGEUNIQUE` 或类似名称的整型列。为 `IMAGE` 列创建一个触发器，使得每当 `IMAGE` 列的值发生变化时，`IMAGEUNIQUE` 列的值都会递增。

使用这种技术，您的应用程序可以检测 `IMAGEUNIQUE` 列的变化，这表明 `IMAGE` 列也发生了更改。

### 从服务器刷新数据

前面的章节讨论了 `TDBNavigator` 组件，除了一个按钮——刷新按钮除外。

`TDBNavigator` 的刷新按钮（调用 `TDataSet.Refresh` 方法）用于从基础数据库刷新数据集。对于 `TClientDataSet`，`Refresh` 通过数据集提供程序重新获取所有行来刷新数据。

**注意**

如果数据集的更改日志不为空，`Refresh` 将引发异常。在直接调用 `TClientDataSet.Refresh` 之前，应检查 `ChangeCount` 属性以查看其是否为零。如果非零，请先应用或取消更新（使用 `ApplyUpdates` 或 `CancelUpdates`），或者避免调用 `Refresh`。

从提供程序刷新数据在发生协调错误且您希望从基础数据库获取最新数据的情况下非常有用。您还可以在其他时间调用它，以确保本地数据副本是最新的。

您可以调用 `TClientDataSet.RefreshRecord` 来仅刷新当前记录，而不是调用 `Refresh` 来刷新整个数据集。即使数据集的更改日志不为空，`RefreshRecord` 也不会引发异常。相反，它将保持整个更改日志完整，包括可能对已刷新记录所做的任何更改。

> `RefreshRecord` 要求主键中的所有字段都设置了 `pfInKey`（如下一节所讨论）。此外，通常只在当前记录的 `UpdateStatus` 为未修改时才调用 `RefreshRecord`。
> ```pascal
> if ClientDataSet1.UpdateStatus = usUnmodified then
>   ClientDataSet1.RefreshRecord;
> ```

### 更新模式

在将数据解析到数据库时，`TDataSetProvider` 自动构建必要的 SQL 语句以发送到服务器执行更新。此类 SQL 语句的一个示例是

```sql
UPDATE CONTACTS SET LAST = 'Smith' WHERE ID = 5
```
