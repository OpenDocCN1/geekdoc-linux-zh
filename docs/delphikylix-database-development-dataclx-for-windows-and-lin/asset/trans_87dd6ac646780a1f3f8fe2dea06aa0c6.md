

**清单 1.2 续**

```pascal
btnConnect: TButton;
btnDisconnect: TButton;
Label4: TLabel;
Label5: TLabel;
OpenDialog1: TOpenDialog;
PageControl1: TPageControl;
tabTables: TTabSheet;
tabProcedures: TTabSheet;
cbProcedure: TComboBox;
Label12: TLabel;
Label13: TLabel;
cbTable: TComboBox;
lblFields: TListBox;
lblIndexes: TListBox;
Label1: TLabel;
Label6: TLabel;
Label7: TLabel;
lvParameters: TListView;
procedure btnConnectClick(Sender: TObject);
procedure cbTableClick(Sender: TObject);
procedure btnDisconnectClick(Sender: TObject);
procedure cbProcedureClick(Sender: TObject);
procedure connAfterConnect(Sender: TObject);
procedure connAfterDisconnect(Sender: TObject);
procedure FormClose(Sender: TObject; var Action: TCloseAction);
private
    { Private declarations }
public
    { Public declarations }
end;
var
    frmMain: TfrmMain;
implementation
{$R *.xfm}
procedure TfrmMain.btnConnectClick(Sender: TObject);
procedure CheckScope(Value: Boolean; TableScope: TTableScope);
begin
    if Value then
        conn.TableScope := conn.TableScope + [TableScope]
```

else
    conn.TableScope := conn.TableScope - [TableScope];
end;

begin
    if OpenDialog1.Execute then begin
        conn.Params.Values['Database'] := OpenDialog1.FileName;
        CheckScope(btnTable.Checked, tsTable);
        CheckScope(btnView.Checked, tsView);
        CheckScope(btnSynonym.Checked, tsSynonym);
        CheckScope(btnSystemTable.Checked, tsSysTable);
        conn.Open;
    end;
end;

procedure TfrmMain.btnDisconnectClick(Sender: TObject);
begin
    conn.Close;
end;

procedure TfrmMain.cbTableClick(Sender: TObject);
begin
    conn.GetFieldNames(cbTable.Items[cbTable.ItemIndex], lbFields.Items);
    conn.GetIndexNames(cbTable.Items[cbTable.ItemIndex], lbIndexes.Items);
end;

procedure TfrmMain.cbProcedureClick(Sender: TObject);
var
    listParams: TList;
    Params: TParams;
    Index: Integer;
    Param: TParam;
    ListItem: TListItem;
begin
    listParams := TList.Create;
    try
        conn.GetProcedureParams(cbProcedure.Items[cbProcedure.ItemIndex],
            listParams);
        Params := TParams.Create;
        try
            LoadParamListItems(Params, listParams);

            lvParameters.Items.BeginUpdate;
            try

ivParameters.Items.Clear;

for Index := 0 to Params.Count - 1 do begin
   Param := Params[Index];
   ListItem := ivParameters.Items.Add;
   ListItem.Caption := Param.Name;
   case Param.DataType of
      ftUnknown:
         ListItem.SubItems.Add('Unknown');
      ftString:
         ListItem.SubItems.Add('String');
      ftSmallInt:
         ListItem.SubItems.Add('SmallInt');
      ftInteger:
         ListItem.SubItems.Add('Integer');
      ftWord:
         ListItem.SubItems.Add('Word');
      ftBoolean:
         ListItem.SubItems.Add('Boolean');
      ftFloat:
         ListItem.SubItems.Add('Float');
      ftCurrency:
         ListItem.SubItems.Add('Currency');
      ftBCD:
         ListItem.SubItems.Add('BCD');
      ftDate:
         ListItem.SubItems.Add('Date');
      ftTime:
         ListItem.SubItems.Add('Time');
      ftDateTime:
         ListItem.SubItems.Add('DateTime');
      ftBytes:
         ListItem.SubItems.Add('Bytes');
      ftVarBytes:
         ListItem.SubItems.Add('VarBytes');
      ftAutoInc:
         ListItem.SubItems.Add('AutoInc');
      ftBlob:
         ListItem.SubItems.Add('Blob');
      ftMemo:
         ListItem.SubItems.Add('Memo');
      ftGraphic:
         ListItem.SubItems.Add('Graphic');
      ftFmtMemo:
         ListItem.SubItems.Add('FmtMemo');
      ftParadoxOle:
         ListItem.SubItems.Add('ParadoxOle');
      ftDBaseOle:
         ListItem.SubItems.Add('DBaseOle');
      ftTypedBinary:
         ListItem.SubItems.Add('TypedBinary');
      ftCursor:
         ListItem.SubItems.Add('Cursor');
      ftFixedChar:
         ListItem.SubItems.Add('FixedChar');
      ftWideString:
         ListItem.SubItems.Add('WideString');
      ftLargeInt:
         ListItem.SubItems.Add('LargeInt');
      ftADT:
         ListItem.SubItems.Add('ADT');
      ftArray:
         ListItem.SubItems.Add('Array');
      ftReference:
         ListItem.SubItems.Add('Reference');
      ftDataSet:
         ListItem.SubItems.Add('DataSet');
      ftOraBlob:
         ListItem.SubItems.Add('OraBlob');
      ftOraClob:
         ListItem.SubItems.Add('OraClob');
      ftVariant:
         ListItem.SubItems.Add('Variant');
      ftInterface:
         ListItem.SubItems.Add('Interface');
      ftIDispatch:
         ListItem.SubItems.Add('IDispatch');
      ftGuid:
         ListItem.SubItems.Add('Guid');
      ftTimeStamp:
         ListItem.SubItems.Add('TimeStamp');

ftFMTBcd: ListItem.SubItems.Add('FMTBcd');
end;
end;
finally
lvParameters.Items.EndUpdate;
end;
finally
Params.Free;
end;
finally
FreeProcParams(listParams);
end;
end;

procedure TfrmMain.connAfterConnect(Sender: TObject);
begin
btnTable.Enabled := False;
btnView.Enabled := False;
btnSynonym.Enabled := False;
btnSystemTable.Enabled := False;

lblConnection.Font.Color := clGreen;
lblConnection.Caption := conn.Params.Values['Database'];

conn.GetTableNames(cbTable.Items, btnSystemTable.Checked);
conn.GetProcedureNames(cbProcedure.Items);

cbTable.ItemIndex := 0;
cbTableClick(cbTable);
PageControl1.ActivePage := tabTables;
ActiveControl := cbTable;

cbProcedure.ItemIndex := 0;
cbProcedureClick(cbProcedure);
end;

procedure TfrmMain.connAfterDisconnect(Sender: TObject);
begin
btnTable.Enabled := True;
btnView.Enabled := True;
btnSynonym.Enabled := True;
btnSystemTable.Enabled := True;

lblConnection.Font.Color := clRed;

lblConnection.Caption := 'Not connected';

cbTable.Items.Clear;
cbProcedure.Items.Clear;
fbFields.Items.Clear;
lblIndexes.Items.Clear;
end;

procedure TfrmMain.FormClose(Sender: TObject; var Action: TCloseAction);
begin
conn.Close;
end;
```

图 1.4 显示了从 CONMAN 数据库返回的表、字段和索引名称。

![](img/52a35759a0f10dade27a840504be5d82_38_0.png)

**图 1.4**
*contacts 表的列和字段列表。*

图 1.5 显示了存储过程 CONTACTSBYSTATE 的过程参数列表。清单 1.2 中的大部分代码都相当直接明了。然而，有两点值得注意，我想指出它们。

首先，cbProcedureClick 方法展示了如何遍历存储过程的参数，以确定它们的名称、类型及其他属性。

![](img/52a35759a0f10dade27a840504be5d82_39_0.png)

**图 1.5**
CONNECTSTATE 过程输出的长参数列表中的参数名称和类型。

其次，VCL/DataCLX 中存在一个 bug，该 bug 实际上阻止你同时获取表、视图和系统表的元数据。如果你同时勾选了表、视图和系统表，GetTableNames（在 connAfterConnect 方法中）不会返回任何信息。请在你自己的应用中注意这一点。如果你需要获取所有三种类型的信息，可以执行以下类似的操作：

```pascal
var
  SL: TStringList;
begin
  SL := TStringList.Create;
  try
    SQLConnection1.TableScope := [tsTable, tsView];
    SQLConnection1.GetTableNames(ListBox1.Items, False);
    SQLConnection1.GetTableNames(SL, True);
    ListBox1.Items.AddStrings(SL);
  finally
    SL.Free;
  end;
end;
```

这段代码首先仅获取表和视图的信息，将结果放入列表框中。接下来，它仅获取系统表，将结果放入临时字符串列表中。最后，它将临时字符串列表中的字符串添加到列表框中。因此，列表框中包含表、视图和系统表。

正如你所见，TSQLConnection 返回的模式信息极其基础。除了存储过程参数外，TSQLConnection 为表、字段、索引和存储过程返回的唯一数据是它们的名称。在下一章中，我将向你展示如何从数据库获取更详细的模式信息。

## 执行 DDL 和 DML 语句

你对数据库执行的最常见操作是 DDL（数据定义语言）和 DML（数据操作语言）语句。你可以通过 TSQLConnection 直接执行 DDL 和 DML 语句。返回游标的 DML 语句（即 SQL SELECT 语句）除了需要 TSQLConnection 外，还需要一个数据集组件，正如你将在第 3 章“客户端数据集基础”中看到的。

## DDL 命令

DDL 命令是操作数据库模式而不是数据本身的语句。在前一节中，我向你展示了如何检索数据库模式的信息。在本节中，我将向你展示如何修改数据库模式。

TSQLConnection 提供了一种名为 `ExecuteDirect` 的方法，用于执行 DDL 命令。`ExecuteDirect` 接受一个参数，即要执行的 SQL 命令。成功时返回 0，失败时返回 dbExpress 错误代码。dbExpress 错误代码可以在随 Delphi 提供的文件 DBXExpress.pas 中找到。

`ExecuteDirect` 名称中的 Direct 部分源于该语句直接发送到数据库。该语句在执行前不会被准备（prepare），并且不能包含任何参数。（参数化 SQL 语句将在本章后面的“参数化 SQL 语句”部分中讨论。）

> **注意**
>
> 某些数据库不支持直接 SQL 执行。在这些数据库上，dbExpress 会在内部准备 SQL 语句，然后执行它。

## 创建表

你可以发出的最简单且最有用的 DDL 命令之一是创建数据库中一个新表的命令。假设你想创建一个名为 EMPLOYEE 的表，其结构如表 1.5 所示。你将发出以下语句：

```pascal
SQLConnection1.ExecuteDirect('CREATE TABLE EMPLOYEE (EMPNO INTEGER, '
  + 'NAME VARCHAR(30); 'HIREDATE DATE, SALARY DOUBLE PRECISION');
```

