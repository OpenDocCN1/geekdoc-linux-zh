

```pascal
ShowMessage('The query took ' + IntToStr(OP + 'ms and was executed on ' +
 DateToStr(TimeQueried) + ' at ' + TimeToStr(TimeQueried));
 end;
```

## 主从数据关系

在第二章“dbExpress 数据集”中，你学习了如何在两个或多个 dbExpress 数据集之间创建主从数据关系。

随后，在第四章中，你学习了如何创建嵌套的 TClientDataSet，从而在 TClientDataSet 层级上建立主从数据关系。

使用数据提供程序（providers），你将在服务端数据模块上建立主从数据关系，并使用 TSQLDataSet 组件。然后，你只需将一个 TDataSetProvider 组件连接到主数据集。在客户端数据模块上放置一个 TClientDataSet 组件，并将其连接到主数据集的提供程序。这将自动在客户端创建嵌套数据集。

良好的实践是创建两个数据模块：一个用于 dbExpress 组件和数据集提供程序，另一个用于客户端数据集。我将这些数据模块称为服务端数据模块和客户端数据模块。本章稍后“连接到本地数据库”部分会更详细地解释这一点。

随本书提供的下载资料中包含的 MasterDetail 示例应用程序展示了此技术。这里没有列出代码，因为几乎不需要代码——所有操作都在设计时完成。

图 7.4 展示了 MasterDetail 应用程序主窗体在设计时的状态。为了简单起见，我将数据库组件直接放在主窗体上，而不是为服务器和客户端创建独立的数据模块。

![](img/52a35759a0f10dade27a840504be5d82_314_0.png)

**图 7.4**
*建立主从数据关系所需的组件。*

## 从存储过程和连接中提供与解析数据

到目前为止，本章的示例侧重于使用简单的 select 语句（例如 `SELECT * FROM CONTACTS`）从单个表提供数据。通常，数据是从服务器上的存储过程提供的，或者是通过多表连接生成的，如下面的两个代码片段所示：

```sql
// 存储过程
SELECT * FROM CONTACTSBYSTATE('FL')

或

// 连接
SELECT CONTACTS.FIRST, CONTACTS.LAST, TODOS.SCHEDULED, TODOS.DESCRIPTION
FROM CONTACTS, TODOS
WHERE CONTACTS.ID = TODOS.CONTACTID;
```

## 从存储过程中提供与解析数据

在前面的示例中，存储过程返回给定州（在此例中为佛罗里达州）的所有联系人。TDataSetProvider 会尝试智能地确定在解析数据时要更新哪个数据库表，但在这种情况下，CONTACTSBYSTATE 是一个存储过程，而不是一个表。

TDataSetProvider 需要一点帮助才知道应该用数据变更更新哪个表。为此，你需要为提供程序的 OnGetTableName 事件提供事件处理程序。在事件处理程序中，指定要更新的表的名称，如下所示：

```pascal
procedure TFrm1.DataSetProvider1GetTableName(Sender: TObject;
  DataSet: TDataSet; var TableName: String);
begin
  TableName := 'CONTACTS';
end;
```

此外，你需要将存储过程数据集中所有不被更新的字段的 ProviderFlags 设置为 []。

## 从连接中提供与解析数据

根据定义，连接（join）会返回来自多个表的数据。在许多情况下，用户只能更新其中一个表的数据。例如，在之前显示的 select 语句中，数据从 CONTACTS 表和 TODOS 表中检索。在客户端，用户可以添加新的 TODO 项，但受影响的唯一表是 TODOS 表。（假设，如果用户想添加新联系人，他不会在查看 todos 的同一屏幕上这样做）。

如果是这种情况，你可以按照前面的说明，在 OnGetTableName 事件处理程序中指定 TODOS 表名。

然而，有时用户能够同时更新多个表。为了处理这种情况，你需要编写一些代码。再次回到 TDataSetProvider 的 BeforeUpdateRecord 事件处理程序。诀窍是在事件处理程序中自己应用必要的更新到各个表。

下面的代码片段展示了同时向多个表应用更新所遵循的大致轮廓。它不是可编译的代码。

```pascal
procedure TForm1.SQLClientDataSet1BeforeUpdateRecord(Sender: TObject; SourceDS: TDataSet; DeltaDS: TCustomClientDataSet; UpdateKind: TUpdateKind; var Applied Boolean);
var
SQL: string;
Connection: TSQLConnection;
begin
// 从源数据集获取连接指针
Connection := (SourceDS as TCustomSQLDataSet).SQLConnection;
case UpdateKind of
ukInsert: begin
// 插入到第一个表
SQL := // SQL INSERT 语句，用于表 1
Connection.Execute(SQL, nil, nil);
// 插入到第二个表
SQL := // SQL INSERT 语句，用于表 2
Connection.Execute(SQL, nil, nil);
end;
ukModify: begin
// 更新第一个表
SQL := // SQL UPDATE 语句，用于表 1
Connection.Execute(SQL, nil, nil);
// 更新第二个表
SQL := // SQL UPDATE 语句，用于表 2
Connection.Execute(SQL, nil, nil);
end;
ukDelete: begin
// 从第一个表删除
SQL := // SQL DELETE 语句，用于表 1
Connection.Execute(SQL, nil, nil);
// 从第二个表删除
SQL := // SQL DELETE 语句，用于表 2
Connection.Execute(SQL, nil, nil);
end;
Applied := True;
end;
```

从上面的列表中可以看出，一般思想是确定正在进行何种操作（插入、修改或删除），然后调用 TSQLConnection 组件直接执行相应的 SQL 语句。在方法结束时，将 Applied 设置为 True，让提供程序知道你已经手动处理了更新。

此过程同样适用于三方、四方或 n 方连接。

下面的示例展示了如何在简单的双表连接中解析更新。

列表 7.2 包含了 Joins 应用程序主窗体的源代码。

**列表 7.2** Joins—MainForm.pas

```pascal
unit MainForm;

interface

uses
    SysUtils, Types, Classes, QGraphics, QControls, QForms, QDialogs,
    QStdCtrls, DBXpress, FMTBcd, DB, SqlExpr, QGrids, ODGrids, Provider,
    DBClient, Variants;

type
    TfrmMain = class(TForm)
        DataSet1: TDataSource;
        DBGrid1: TDBGrid;
        SQLConnection1: TSQLConnection;
        SQLDataSet1: TSQLDataSet;
        DataSetProvider1: TDataSetProvider;
        ClientDataSet1: TClientDataSet;
        sqlIO: TSQLDataSet;
        btnApplyUpdates: TButton;
        procedure FormCreate(Sender: TObject);
        procedure DataSetProvider1BeforeUpdateRecord(Sender: TObject;
        SourceDS: TDataSet; DeltaDS: TCustomClientDataSet;
            UpdateKind: TUpdateKind; var Applied: Boolean);
        procedure btnApplyUpdatesClick(Sender: TObject);
        procedure ClientDataSet1NewRecord(DataSet: TDataSet);
    private
 { Private declarations }
 FNextID: Integer;
 function GetNextID: Integer;
public
 { Public declarations }
end;
var
 frmMain: TfrmMain;
implementation
($R *.xfm)
procedure TfrmMain.FormCreate(Sender: TObject);
begin
 ClientDataSet1.Open;
end;

procedure TfrmMain.ClientDataSet1NewRecord(DataSet: TDataSet);
begin
 Dec(FNextID);
 DataSet.FieldName('CONTACTID').AsInteger := FNextID;
end;

function TfrmMain.GetNextID: Integer;
begin
 sqlID.ExecSQL;
 Result := sqlID.ParamByName('AVALUE').AsInteger;
end;

procedure TfrmMain.DataSetProvider1BeforeUpdateRecord(Sender: TObject;
 SourceDS: TDataSet; DeltaDS: TCustomClientDataSet;
 UpdateKind: TUpdateKind; var Applied: Boolean);
var
 SQL: string;
 Connection: TSQLConnection;
 ID: Integer;
begin
 // 从源数据集获取连接指针
 Connection := (SourceDS as TCustomSQLDataSet).SQLConnection;

case UpdateKind of
 ukInsert: begin
 ID := GetNextID;

    // 插入到第一个表
    SQL := Format('INSERT INTO CONTACTS (CONTACTID, FIRST, LAST) ' +
           'VALUES (%d, %s, %s)',
           [ID, QuotedStr(DeltaDS.FieldNameByName('FIRST').NewValue),
            QuotedStr(DeltaDS.FieldNameByName('LAST').NewValue)]);
    Connection.Execute(SQL, nil, nil);

    // 插入到第二个表
    SQL := Format('INSERT INTO CONTACTS2 (CONTACTID, SPOUSE) ' +
           'VALUES (%d, %s)',
           [ID, QuotedStr(DeltaDS.FieldNameByName('SPOUSE').NewValue)]);
    Connection.Execute(SQL, nil, nil);
    end;

    ukModify: begin
    // 更新第一个表
    SQL := '';

    if not VarIsEmpty(DeltaDS.FieldNameByName('FIRST').NewValue) then
    SQL := SQL + Format('FIRST = %s',
           [QuotedStr(DeltaDS.FieldNameByName('FIRST').NewValue)]);

    if not VarIsEmpty(DeltaDS.FieldNameByName('LAST').NewValue) then begin
    if SQL <> '' then
    SQL := SQL + ', ';

    SQL := SQL + Format('LAST = %s',
           [QuotedStr(DeltaDS.FieldNameByName('LAST').NewValue)]);
    end;

    if SQL <> '' then begin
    ID := DeltaDS.FieldNameByName('CONTACTID').OldValue;
    SQL := Format('UPDATE CONTACTS SET %s ' +
           'WHERE CONTACTID = %d', [SQL, ID]);
    Connection.Execute(SQL, nil, nil);
    end;

    // 更新第二个表
    SQL := '';

    if not VarIsEmpty(DeltaDS.FieldNameByName('SPOUSE').NewValue) then begin
    ID := DeltaDS.FieldNameByName('CONTACTID').OldValue;

    if VarIsNull(DeltaDS.FieldNameByName('SPOUSE').OldValue) then
    SQL := Format('INSERT INTO CONTACTS2 (CONTACTID, SPOUSE) ' +
           'VALUES (%d, %s)',
           [ID, QuotedStr(DeltaDS.FieldNameByName('SPOUSE').NewValue)]);
    end;
    end;
end;
```

