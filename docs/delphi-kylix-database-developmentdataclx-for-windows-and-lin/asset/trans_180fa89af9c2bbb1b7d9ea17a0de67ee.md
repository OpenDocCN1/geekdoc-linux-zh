

字段列表在以下场景中非常有用。例如，如果你有结构相同的两个客户端数据集，可以使用以下代码将一个数据集的记录添加到另一个数据集中：

```pascal
var
    Index: Integer;
begin
    ClientDataSet2.Append;
    for Index := 0 to ClientDataSet1.Fields.Count - 1 do
        ClientDataSet2.Fields[Index].AsVariant :=
            ClientDataSet1.Fields[Index].AsVariant;
    ClientDataSet2.Post;
end;
```

接下来的章节将详细讨论如何向数据集中添加记录。

## 填充和操作客户端数据集

创建客户端数据集（无论是在设计时还是运行时）后，你需要用数据填充它。填充客户端数据集有几种方法：你可以通过代码手动填充，可以从另一个数据集加载记录，也可以从文件或流中加载数据集。以下章节将讨论这些方法，以及如何修改和删除记录。

### 手动填充

向客户端数据集输入数据最基本的方式是通过 Append 和 Insert 方法，这两种方法被所有数据集所支持。它们的区别在于，Append 在数据集的末尾添加新记录，而 Insert 则立即在当前记录之前放置新记录。

我总是使用 Append 来插入新记录，因为它比 Insert 稍快一些。如果数据集建立了索引，新记录无论如何都会自动按正确顺序排序。

以下代码片段演示了如何向客户端数据集添加记录：

```pascal
cdsEmployee.Append; // 这里也可以使用 cdsEmployee.Insert;
cdsEmployee.FieldName('ID').AsInteger := 5;
cdsEmployee.FieldName('FirstName').AsString := 'Eric';
cdsEmployee.Post;
```

### 修改记录

修改现有记录与添加新记录几乎相同。与其调用 Append 或 Insert 来创建新记录，你应当调用 Edit 将数据集置于编辑模式。以下代码将当前记录的名字改为 Fred。

```pascal
cdsEmployee.Edit; // 编辑当前记录
cdsEmployee.FieldName('FirstName').AsString := 'Fred';
cdsEmployee.Post;
```

### 删除记录

要删除当前记录，只需调用 `Delete` 方法，如下所示：

```pascal
cdsEmployee.Delete;
```

如果你想要删除数据集中的所有记录，可以改用 `EmptyDataSet`，如下所示：

```pascal
cdsEmployee.EmptyDataSet;
```

### 从另一个数据集填充

dbExpress 数据集是单向的，无法向前回退滚动。这使得它们与双向数据感知控件（如 `TDBGrid`）不兼容。然而，`TClientDataSet` 可以通过*提供者*从另一个数据集（包括 dbExpress 数据集、BDE 数据集或其他客户端数据集）加载其数据。利用此功能，你可以从单向的 dbExpress 数据集加载客户端数据集，然后将 `TDBGrid` 连接到该客户端数据集，从而提供双向支持。

事实上，这种能力如此强大且重要，以至于它构成了 Delphi 多术语数据库支持的基础。

### 从文件或流填充：持久化客户端数据集

虽然客户端数据集驻留在 RAM 中，但你可以将它们保存到文件或流中，并在稍后重新加载，从而实现持久化。这是填充客户端数据集的第三种方法。

要将数据集保存到文件，请使用 `SaveToFile` 方法，其定义如下：

```pascal
procedure SaveToFile(const FileName: string = '';
Format: TDataPacketFormat = dfBinary);
```

类似地，要将数据集保存到流，请调用 `SaveToStream`，其定义如下：

```pascal
procedure SaveToStream(Stream: TStream; Format: TDataPacketFormat = dfBinary);
```

`SaveToFile` 接受你正在保存到的文件的名称。如果文件名为空，则数据将使用客户端数据集的 `FileName` 属性进行保存。

`SaveToFile` 和 `SaveToStream` 都接受一个参数，指示保存数据时使用的格式。客户端数据集可以存储为三种文件格式之一：二进制格式，或任意一种 XML 变体。表 3.1 列出了可能的格式。

**表 3.1** 加载和保存客户端数据集的数据包格式

| 值 | 描述 |
| :---- | :---------- |
| dfBinary | 数据使用专有的二进制格式存储。 |
| dfXML | 数据以 XML 格式存储。扩展字符使用转义序列表示。 |
| dfXMLUTF8 | 数据以 XML 格式存储。扩展字符使用 UTF8 表示。 |

当客户端数据集存储到磁盘时，它们被称为 MyBase 文件。MyBase 在每个文件或每个流中存储一个数据集，除非你使用嵌套数据集。

**注意**

如果你熟悉 Microsoft ADO，你可能会记得 ADO 允许你使用 XML 格式持久化数据集。ADO 和 MyBase 使用的 XML 格式不兼容。换句话说，你不能将 ADO 数据集以 XML 格式保存到磁盘，然后再将其读入客户端数据集（反之亦然）。

有时，你需要确定存储客户端数据集中包含的数据需要多少字节。例如，你可能想在将数据保存到软盘之前检查是否有足够的空间，或者你可能需要为流预分配内存。在这种情况下，你可以检查 DataSize 属性，如下所示：

```pascal
if ClientDataSet1.DataSize > AvailableSpace then
  ShowMessage('没有足够的空间存储数据');
```

DataSize 始终返回以二进制格式（dfBinary）存储数据所需的空间量。XML 格式通常需要更多的空间，也许是两倍（甚至更多）。

**注意**

确定以 XML 格式保存数据集所需空间的一种方法是，将数据集保存到内存流，然后获取由此产生的流的大小。

# 示例：创建、填充和操作客户端数据集

以下示例说明了如何在运行时创建、填充和操作客户端数据集。还提供了将数据集保存到磁盘以及加载数据集的代码。

清单 3.1 展示了 CDS (ClientDataset) 应用程序的完整源代码。

# **清单 3.1** CDS—MainForm.pas

```pascal
unit MainForm;

interface
uses
  SysUtils, Types, IdGlobal, Classes, QGraphics, QControls, QForms, QDialogs,
  QStdCtrls, DB, DBClient, QExtCtrls, QGrids, QDBGriDs, QActnList;

const
  MAX_RECS = 10000;

type
  TfrmMain = class(TForm)
    DataSource1: TDataSource;
    pnlClient: TPanel;
    pnlBottom: TPanel;
    btnPopulate: TButton;
    btnSave: TButton;
    btnLoad: TButton;
    ActionList1: TActionList;
    btnStatistics: TButton;
    Populate1: TAction;
    Statistics1: TAction;
    Load1: TAction;
    Save1: TAction;
    DBGriD1: TDBGriD;
    lblFeedback: TLabel;
    procedure FormCreate(Sender: TObject);
    procedure PopulateExecute(Sender: TObject);
    procedure StatisticsExecute(Sender: TObject);
    procedure SaveExecute(Sender: TObject);
    procedure LoadExecute(Sender: TObject);
  private
    { Private declarations }
    FCDS: TClientDataSet;
  public
    { Public declarations }
end;

var
  frmMain: TfrmMain;

implementation

{$R *.xfm}

procedure TfrmMain.FormCreate(Sender: TObject);
begin
  FCDS := TClientDataSet.Create(Self);
  FCDS.FieldDefs.Add('ID', ftInteger, 0, True);
  FCDS.FieldDefs.Add('Name', ftString, 20, True);
  FCDS.FieldDefs.Add('Birthday', ftDateTime, 0, True);
  FCDS.FieldDefs.Add('Salary', ftCurrency, 0, True);
  FCDS.CreateDataSet;
  DataSource1.DataSet := FCDS;
end;

procedure TfrmMain.Populate1Execute(Sender: TObject);
const
  FirstNames: array[0 .. 19] of string = ('John', 'Sarah', 'Fred', 'Beth',
                                         'Eric', 'Tina', 'Thomas', 'Judy', 'Robert', 'Angela', 'Tim', 'Traci',
                                         'David', 'Paula', 'Bruce', 'Jessica', 'Richard', 'Carla', 'James',
                                         'Mary');
  LastNames: array[0 .. 11] of string = ('Parker', 'Johnson', 'Jones',
                                         'Thompson', 'Smith', 'Baker', 'Wallace', 'Harper', 'Parson', 'Edwards',
                                         'Mandel', 'Stone');
var
  Index: Integer;
  t1, t2: DWord;
begin
  RandSeed := 0;

  t1 := GetTickCount;
  FCDS.DisableControls;
  try
    FCDS.EmptyDataSet;
    for Index := 1 to MAX_RECS do begin
      FCDS.Append;
      FCDS.FieldByName('ID').AsInteger := Index;
      FCDS.FieldByName('Name').AsString := FirstNames[Random(20)] + ' ' +
```
