
# **列表 2.1** 续

```pascal
conn: TSQLConnection;   
SQLTable1: TSQLTable;   
SQLQuery1: TSQLQuery;   
SQLStoredProc1: TSQLStoredProc;   
SQLDataSet1: TSQLDataSet;   
Label1: TLabel;   
lvResults: TListView;   
procedure btnConnectClick(Sender: TObject);   
private   
{ Private declarations }   
procedure OpenTable;   
procedure OpenQuery;   
procedure OpenStoredProcedure;   
procedure OpenDataset;   
procedure LoadResults(DataSet: TDataSet);   
public   
{ Public declarations }   
end;   
var   
frmMain: TfrmMain;   
implementation   
uses DataSetTypeForm;   
{$R *.xfrm}   
procedure TfrmMain.btnConnectClick(Sender: TObject);   
var   
frmDataSetType: TfrmDataSetType;   
begin   
// Ask the user whether to open the table, query, stored procedure,   
// or general-purpose dataset   
frmDataSetType := TfrmDataSetType.Create(nil);   
try   
if frmDataSetType.ShowModal = mrOk then begin   
case frmDataSetType.DatasetType of   
dtTable:    OpenTable;   
dtQuery:    OpenQuery;   
dtStoredProc: OpenStoredProcedure;   
dtDataset:    OpenDataset;   
end;
```

conn.Close;
end;
finally
  frmDataType.Free;
end;
end;

procedure TfrmMain.OpenTable;
begin
  SQLTable1.TableName := 'CONTACTS';
  SQLTable1.IndexName := 'IX_CONNNAME';
  SQLTable1.Open;

  LoadResults(SQLTable1);
end;

procedure TfrmMain.OpenQuery;
begin
  SQLQuery1.SQL_Text := 'SELECT * FROM CONTACTS ' +
    'WHERE COUNTRY = "United States"';
  SQLQuery1.Open;

  LoadResults(SQLQuery1);
end;

procedure TfrmMain.OpenStoredProcedure;
begin
  SQLStoredProc1.StoredProcedureName := 'CONTACTSBYSTATE';
  SQLStoredProc1.ParamByName('ASTATE').Value := 'FL';
  SQLStoredProc1.Open;

  LoadResults(SQLStoredProc1);
end;

procedure TfrmMain.OpenDataset;
begin
  SQLDataset1.CommandType := ctQuery;
  SQLDataset1.CommandText := 'SELECT FIRST, LAST, PHONE FROM CONTACTS ' +
    'ORDER BY LAST, FIRST';
  SQLDataset1.Open;

  LoadResults(SQLDataset1);
end;

procedure TfrmMain.LoadResults(DataSet: TDataSet);
var
  ListItem: TListItem;
begin
  lvResults.Items.BeginUpdate;
  try
    lvResults.Items.Clear;

    while not DataSet.EOF do begin
      ListItem := lvResults.Items.Add;
      ListItem.Caption := DataSet.FieldByName('FIRST').AsString;
      ListItem.SubItems.Add(DataSet.FieldByName('LAST').AsString);
      ListItem.SubItems.Add(DataSet.FieldByName('PHONE').AsString);
      DataSet.Next;
    end;
  finally
    lvResults.Items.EndUpdate;
  end;
end;
```

如代码所示，当用户点击“连接”按钮时，程序会创建一个 `TfrmDataType` 的实例（如列表 2.2 所示），提示用户选择要打开的数据集类型：表、查询、存储过程或通用数据集。用户选择数据集类型后，程序会调用四个方法之一：`OpenTable`、`OpenQuery`、`OpenStoredProcedure` 或 `OpenDataset`。这些方法分别设置所选数据集的属性，并调用 `LoadResults`。

请注意，`LoadResults` 以 `TDataSet` 作为参数，如前文所述，`TDataSet` 是所有数据集的基类。这意味着 `LoadResults` 实际上可以处理任何数据集，无论是 dbExpress 数据集、BDE 数据集，还是某些第三方数据集。

`LoadResults` 遍历数据集中的记录，将联系人的名字、姓氏和电话号码加载到 `TListView` 中。

# **列表 2.2** 基础示例—DataTypeForm.pas

```pascal
unit DataTypeForm;

interface

uses
SysUtils, Variants, Classes, QGraphics, QControls, QForms,
QDialogs, QExtCtrls, QStdCtrls;

type
	TDataSetType = (dtTable, dtQuery, dtStoredProc, dtDataset);

	TfrmDatasetType = class(TForm)
		pnlClient: TPanel;
		pnlBottom: TPanel;
		btnOk: TButton;
		btnCancel: TButton;
		grpDatasetType: TRadioGroup;
		procedure btnOkClick(Sender: TObject);
	private
		{ Private declarations }
		FDataSetType: TDataSetType;
	public
		{ Public declarations }
		property DatasetType: TDataSetType read FDataSetType;
	end;

implementation

{$R *.xfm}

procedure TfrmDatasetType.btnOkClick(Sender: TObject);
begin
	FDataSetType := TDataSetType(grpDatasetType.ItemIndex);
end;

end.
```

图 2.2 展示了基础示例应用程序在运行时的界面。

## BLOB 支持

与大多数数据集类似，dbExpress 数据集支持 BLOB 数据。BLOB 是二进制大对象（Binary Large Object）的缩写，用于存储自由格式数据（如图像、备忘录等）。

BLOB 的大小可能会变得很大，因此为了提高查询性能，您通常希望限制从数据库检索的 BLOB 数据的大小。例如，假设您有一个用于存储联系人图像的 BLOB 字段。执行返回大量结果集的查询（如 `SELECT * FROM CONTACTS`）可能会从数据库中检索数千条记录。如果每个联系人的图像平均大小为 100K，那么从服务器返回的数据量将非常庞大。当数据库连接跨越局域网，甚至更糟糕的是跨越互联网时，这个问题会进一步加剧。

![](img/fe651f295b5f960d5463c4fb581d2281_82_0.png)

# **图 2.2**
`TSQLDataSet` 用于从数据库检索数据。

在这种情况下，您可能希望从结果集中移除 BLOB 列。您可以有两种方法来实现这一点。首先，如果您正在执行预定义的查询，只需从查询中省略 BLOB 字段即可。例如，如果您正在执行查询 `SELECT FIRST, LAST, PHONE, IMAGE FROM CONTACTS`，请将 SQL 语句修改为 `SELECT FIRST, LAST, PHONE FROM CONTACTS`。

其次，虽然上述解决方案在您确切知道要从数据库检索哪些列时效果很好，但对于通用的数据库实用工具该怎么办呢？如果您不知道列名或字段类型，可以执行如下语句：

```sql
SELECT * FROM CONTACTS
```

在这种情况下，您可以设置 `TSQLDataSet` 的 `BlobSize` 属性，以确定每个 BLOB 字段要检索的最大数据量。如果此参数为 0（默认值），则最大 BLOB 大小由关联的 `TSQLConnection` 的 `BlobSize` 参数决定。如果此参数为 –1，则数据集将检索整个 BLOB，无论其大小如何。其他任何值均构成要检索的 BLOB 的最大字节数。

# **注意**

无论您在连接级别还是在数据集级别设置 `BlobSize`，它都应用于数据集中返回的所有 BLOB 字段。没有办法只检索一个 BLOB 字段的前 100 个字节，同时检索另一个 BLOB 字段的全部内容。

## 参数化查询

在本章迄今为止展示的大多数示例中，在查询数据库时，整个查询语句都是明确指定的。例如，`SELECT * FROM CONTACTS WHERE COUNTRY = 'United States'`

虽然这样可行，但如果您打算多次执行相同的通用查询，则效率较低。例如，假设您想先检索美国的所有联系人，然后检索加拿大的所有联系人，最后检索墨西哥的所有联系人。您可以编写如下代码：

```delphi
SQLOleDataSet1.CommandType := ctQuery;
SQLOleDataSet1.CommandText := 'SELECT * FROM CONTACTS '
    + 'WHERE COUNTRY = "United States"';
SQLOleDataSet1.Open;
ProcessDataSet;
SQLOleDataSet1.Close;
```

```delphi
SQLOleDataSet1.CommandText := 'SELECT * FROM CONTACTS WHERE COUNTRY = "Canada"';
SQLOleDataSet1.Open;
ProcessDataSet;
SQLOleDataSet1.Close;
```

```delphi
SQLOleDataSet1.CommandText := 'SELECT * FROM CONTACTS WHERE COUNTRY = "Mexico"';
SQLOleDataSet1.Open;
ProcessDataSet;
```

在此示例中，`ProcessDataSet` 是一个虚构的方法，它以某种方式对查询结果进行操作。

虽然上述代码工作正常，但远非最优。每次设置 `SQLOleDataSet1.CommandText` 时，后端数据库引擎都必须解析和准备 SQL 语句。实现相同结果的一种更好方法是参数化查询，如下所示：

```delphi
SQLOleDataSet1.CommandText := 'SELECT * FROM CONTACTS WHERE COUNTRY = :Country';
```

这设置了一个名为 `Country` 的参数，它在 SQL 语句中充当占位符。通过为此参数设置不同的值，您可以针对不同的国家发出相同的 SQL 语句，如下所示：

```delphi
SQLOleDataSet1.CommandType := ctQuery;
SQLOleDataSet1.CommandText := 'SELECT * FROM CONTACTS WHERE COUNTRY = :Country';
SQLOleDataSet1.ParamByName('Country').AsString := 'United States';
SQLOleDataSet1.Open;
ProcessDataSet;
```

