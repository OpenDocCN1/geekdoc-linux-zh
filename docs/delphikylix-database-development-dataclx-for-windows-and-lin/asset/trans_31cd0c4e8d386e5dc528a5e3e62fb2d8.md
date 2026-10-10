

## **LISTING 2.1**（续）

```pascal
conn.Close;
end;
finally
  frmDatasetType.Free;
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
  SQLQuery1.SQL.Text := 'SELECT * FROM CONTACTS ' +
    'WHERE COUNTRY = 'United States'';
  SQLQuery1.Open;

  LoadResults(SQLQuery1);
end;

procedure TfrmMain.OpenStoredProcedure;
begin
  SQLStoredProc1.StoredProcName := 'CONTACTSBYSTATE';
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
```

![Image](img/52a35759a0f10dade27a840504be5d82_80_0.png)

## **LISTING 2.1**（续）

```pascal
procedure TfrmMain.LoadResults(DataSet: TDataSet);
var
 ListItem: TListItem;
begin
 lvResults.Items.BeginUpdate;
 try
 lvResults.Items.Clear;
 while not DataSet.EOF do begin
 ListItem := lvResults.Items.Add;
 ListItem.Caption := DataSet.FieldName('FIRST').AsString;
 ListItem.SubItems.Add(DataSet.FieldName('LAST').AsString);
 ListItem.SubItems.Add(DataSet.FieldName('PHONE').AsString);
 DataSet.Next;
 end;
 finally
 lvResults.Items.EndUpdate;
 end;
 end;
```

从代码中可以看出，当用户点击连接按钮时，程序会创建 `TfrmDataTypeType` 的一个实例（如 LISTING 2.2 所示），该实例提示用户选择要打开的数据集类型：表、查询、存储过程或通用数据集。用户选择数据集类型后，程序会调用四个方法中的一个：`OpenTable`、`OpenQuery`、`OpenStoredProcedure` 或 `OpenDataset`。这些方法分别设置所选数据集的属性，并调用 `LoadResults`。

请注意，`LoadResults` 接受一个 `TDataSet` 作为参数，正如前面所指出的，`TDataSet` 是所有数据集的根类。这意味着 `LoadResults` 实际上可以处理任何数据集，无论是 dbExpress 数据集、BDE 数据集，还是某些第三方数据集。

`LoadResults` 遍历数据集中的记录，将联系人姓名、姓氏和电话号码加载到 `TListView` 中。

## **LISTING 2.2** Basic—DatasetTypeForm.pas

```pascal
unit DataTypeForm;
interface
uses
SysUtils, Variants, Classes, QGraphics, QControls, QForms,
QDialogs, QExtCtrls, QStdCtrls;

type
 TDataType = (dtTable, dtQuery, dtStoredProc, dtDataset);

TFrmDataType = class(TForm)
 pnlClient: TPanel;
 pnlBottom: TPanel;
 btnOk: TButton;
 btnCancel: TButton;
 grpDataType: TRadioGroup;
 procedure btnOkClick(Sender: TObject);
private
 { Private declarations }
 FDataType: TDataType;
public
 { Public declarations }
 property DataType: TDataType read FDataType;
end;

implementation

{$R *.dfm}

procedure TFrmDataType.btnOkClick(Sender: TObject);
begin
 FDataType := TDataType(grpDataType.ItemIndex);
end;
end.
```

图 2.2 展示了 Basic 演示应用在运行时的状态。

### BLOB 支持

与大多数数据集一样，dbExpress 数据集支持 BLOB 数据。BLOB 是 Binary Large Object（二进制大对象）的缩写，用于存储自由格式的数据（如图像、备忘录等）。

BLOB 数据很容易变得很大，因此您通常需要限制从数据库检索的 BLOB 数据的大小，以提高查询性能。例如，假设您有一个用于存储联系人图像 BLOB 字段。执行返回大量结果集的查询（如 `SELECT * FROM CONTACTS`）可能会从数据库中检索成千上万条记录。如果每个联系人的图像平均大小为 100K，那么从服务器返回的数据量将非常巨大。当数据库连接跨越局域网，甚至互联网时，这个问题会更加严重。

![Image](img/52a35759a0f10dade27a840504be5d82_83_0.png)

> 图 2.2
> *TSQLDataset 用于从数据库检索数据。*

在这种情况下，您可能希望从结果集中排除 BLOB 列。有两种方法可以实现这一点。首先，如果您执行的是预定义查询，只需从查询中省略 BLOB 字段即可。例如，如果您执行查询 `SELECT FIRST, LAST, PHONE, IMAGE FROM CONTACTS`，请将 SQL 语句修改为 `SELECT FIRST, LAST, PHONE FROM CONTACTS`。

其次，虽然如果知道从数据库检索的确切列，上述解决方案效果很好，但如果是通用的数据库工具该怎么办？如果您不知道列名或字段类型，可以执行以下语句：

```sql
SELECT * FROM CONTACTS
```

在这种情况下，您可以设置 `TSQLDataSet` 的 `BlobSize` 属性来确定每个 BLOB 字段检索的最大数据量。如果此参数为 0（默认值），则最大 BLOB 大小由关联的 `TSQLConnection` 的 `BlobSize` 参数决定。如果此参数为 -1，数据集将检索整个 BLOB，无论其大小如何。其他任何值都构成检索 BLOB 的最大字节数。

**NOTE**

无论您在连接级别还是数据集级别设置 `BlobSize`，它都适用于数据集中返回的所有 BLOB 字段。没有办法仅检索一个 BLOB 字段的前 100 字节，同时检索另一个 BLOB 字段的全部内容。

### 参数化查询

在本章迄今为止展示的大多数示例中，查询数据库时指定了完整的查询。例如，

```sql
SELECT * FROM CONTACTS WHERE COUNTRY = "United States"
```

虽然这行得通，但如果您要多次执行相同的通用查询，其效率较低。例如，假设您想先检索所有美国联系人，然后是加拿大所有联系人，最后是所有墨西哥联系人。您可以编写如下代码：

```pascal
SQLDataSet1.CommandType := ctQuery;
SQLDataSet1.CommandText := 'SELECT * FROM CONTACTS ' +
'WHERE COUNTRY = "United States"';
SQLDataSet1.Open;
ProcessDataSet;
SQLDataSet1.Close;

SQLDataSet1.CommandText := 'SELECT * FROM CONTACTS WHERE COUNTRY = "Canada"';
SQLDataSet1.Open;
ProcessDataSet;
SQLDataSet1.Close;

SQLDataSet1.CommandText := 'SELECT * FROM CONTACTS WHERE COUNTRY = "Mexico"';
SQLDataSet1.Open;
ProcessDataSet;
SQLDataSet1.Close;
```

在此示例中，`ProcessDataSet` 是某个虚构的方法，它会对查询结果进行某种操作。

虽然上述代码运行正确，但远非最佳。每次设置 `SQLDataSet1.CommandText` 时，后端数据库引擎都必须解析并准备 SQL 语句。实现相同结果的一种更好方法是参数化查询，如下所示：

```pascal
SQLDataSet1.CommandText := 'SELECT * FROM CONTACTS WHERE COUNTRY = :Country';
```

这会建立一个名为 `Country` 的参数，它在 SQL 语句中充当占位符。通过为此参数设置不同的值，您可以为不同国家发出相同的 SQL 语句，如下所示：

```pascal
SQLDataSet1.CommandType := ctQuery;
SQLDataSet1.CommandText := 'SELECT * FROM CONTACTS WHERE COUNTRY = :Country';
SQLDataSet1.ParamByName('Country').AsString := 'United States';
SQLDataSet1.Open;
ProcessDataSet;
SQLDataSet1.Close;

SQLDataSet1.ParamByName('Country').AsString := 'Canada';
SQLDataSet1.Open;
ProcessDataSet;
SQLDataSet1.Close;

SQLDataSet1.ParamByName('Country').AsString := 'Mexico';
SQLDataSet1.Open;
ProcessDataSet;
```

在此场景中，SQL 语句仅准备一次——即第一次执行时。之后，无需再次准备该语句，因为唯一变化的只是 `Country` 参数。

**NOTE**

请注意，参数名称不需要与其引用的列名称相同。在前面的示例中，该参数可以命名为 `ACountry`、`CountryParam` 或 `Fred`。

还有一个额外的属性控制参数的处理方式：`ParamCheck` 属性。当 `ParamCheck` 设置为 True 时，参数会自动由 dbExpress 创建（如前面的示例所示）。但是，如果您将 `ParamCheck` 设置为 False，则您需要自己创建参数。以下代码片段展示了如何这样做：

```pascal
SQLDataSet1.CommandType := ctQuery;
SQLDataSet1.ParamCheck := False;
SQLDataSet1.CommandText := 'SELECT * FROM CONTACTS WHERE COUNTRY = :Country';
SQLDataSet1.Params.CreateParam('Country', ftString, ptInput);
SQLDataSet1.ParamByName('Country').AsString := 'United States';
SQLDataSet1.Open;
```

请注意，通常只有在发出创建接受参数作为存储过程一部分的 DDL 语句时，您才会将 `ParamCheck` 设置为 False。因为这听起来有些混淆，我们来看一个例子：

```pascal
SQLDataSet1.CommandType := ctQuery;
SQLDataSet1.ParamCheck := False;
SQLDataSet1.CommandText :=
'CREATE PROCEDURE CONTACTSBYTITLE(ATITLE VARCHAR(20)) ' +
'RETURNS (      INTEGER, ' +
'FIRST      VARCHAR(20) ' +
```

