

# 列表 4.8 续

```delphi
type
TfrmChangeLog = class(TForm)
    pnlClient: TPanel;
    pnlBottom: TPanel;
    ClientDataSet1: TClientDataSet;
    DataSource1: TDataSource;
    DBGId1: TDBGid;
    btnClose: TButton;
    Label1: TLabel;
    procedure ClientDataSet1AfterScroll(DataSet: TDataSet);
private
    { Private declarations }
public
    { Public declarations }
    constructor Create(AOwner: TComponent;
        ADataSet: TCustomClientDataSet); reintroduce;
end;

implementation

{$R *.xfm}

{ TfrmChangeLog }

constructor TfrmChangeLog.Create(AOwner: TComponent;
    ADataSet: TCustomClientDataSet);
begin
    inherited Create(AOwner);

    ClientDataSet1.Data := ADataSet.Delta;
end;

procedure TfrmChangeLog.ClientDataSet1AfterScroll(DataSet: TDataSet);
begin
    case ClientDataSet1.UpdateDataSet of
        usUnmodified: Label1.Caption := 'Unmodified';
        usModified: Label1.Caption := 'Modified';
        usInserted: Label1.Caption := 'Inserted';
        usDeleted: Label1.Caption := 'Deleted';
    end;
end;

end.
```

图 4.6 展示了 ChangeLog 应用程序在运行时查看 EMPLOYEE.CDS 数据集变更日志的情况。

![](img/fe651f295b5f960d5463c4fb581d2281_197_0.png)

![](img/fe651f295b5f960d5463c4fb581d2281_198_0.png)

![](img/fe651f295b5f960d5463c4fb581d2281_198_1.png)

# 图 4.6

*ChangeLog 应用程序展示了如何高效存储对数据集的修改。*

请注意变更日志中的四行内容。第一行显示了新添加的员工数据。第二行显示了被删除的员工数据。第三行和第四行显示了对现有员工的修改。第三行包含了在任何修改之前员工的数据，但第四行只包含了被修改的那些字段的数据。

# 从另一个客户端数据集克隆数据

客户端数据集具有从另一个客户端数据集克隆数据的独特能力。当你克隆一个数据集时，数据的物理副本只有一份，但有两个（或更多）不同的数据集访问同一份数据副本。对一个数据集的修改会立即影响另一个数据集对该数据的视图。

你为什么要这样做？在我的项目中，我遇到过几种克隆提供了优雅解决方案的情况，否则这些情况会很棘手。以下列表概述了其中一些好处：

- 你可以在不干扰原始数据集当前记录指针的情况下遍历数据集的克隆。
- 在网格中查看数据集时，你可以使用连接到克隆的数据感知控件在对话框中插入一条新记录（而无需在网格中临时打开一条新的空行）。
- 你可以对克隆应用范围或过滤器，而不会影响原始数据集的显示。

要克隆一个数据集，请创建一个第二个客户端数据集，然后调用第二个数据集的 CloneCursor 方法，如下所示：

```delphi
var
  cdsClone: TClientDataSet;
begin
  cdsClone := TClientDataSet.Create(nil);
  try
    cdsClone.CloneCursor(ClientDataSet1, False, False);

    // Perform some operations on the clone here.
  finally
    cdsClone.Free;
  end;
end;
```

此代码片段创建 ClientDataSet1 的一个克隆，在克隆上执行一些操作，然后释放克隆。在克隆上执行的任何插入、编辑或删除操作都会自动反映在 ClientDataSet1 中。

CloneCursor 定义如下：

```delphi
procedure CloneCursor(Source: TCustomClientDataSet; Reset: Boolean;
  KeepSettings: Boolean = False); virtual;
```

Source 指代你想要克隆的客户端数据集。你无法克隆非客户端数据集，例如 BDE 数据集或 dbExpress 数据集。

Reset 和 KeepSettings 协同工作，决定克隆如何处理以下属性：

- Filter, Filtered, FilterOptions, OnFilterRecord
- IndexName
- MasterSource, MasterFields
- ReadOnly
- RemoteServer, ProviderName

如果 Reset 和 KeepSettings 都设置为 False，则所有上述属性都会从原始数据集复制到克隆。如果 Reset 为 False 且 KeepSettings 为 True，则克隆的这些属性保持不变。如果 Reset 为 True（无论 KeepSettings 的值如何），克隆上的这些属性将被清除。表 4.5 描绘了这种关系。

# 表 4.5 Reset 和 KeepSettings 之间的关系

| Reset | KeepSettings | 行为 |
| :--- | :--- | :--- |
| False | False | 属性从原始数据集复制到克隆。 |
| False | True | 克隆的属性保持不变。 |
| True | N/A | 克隆的属性被清除。 |

如果你希望克隆从原始数据集复制某些列出的属性，但不复制其他属性，你必须编写一些代码。处理这种情况的一种方法是同时将 **Reset** 和 **KeepSettings** 设置为 **False**，将之前列出的所有属性从原始数据集复制到克隆。然后，重置克隆那些被原始数据集覆盖的属性。或者，你可以将 Reset 和 KeepSettings 设置为 True，然后设置克隆上的相应属性。

> **注意**
>
> 克隆客户端数据集后，克隆不包含任何持久字段类型。这意味着你通常使用 FieldByName 来访问克隆中的字段。此外，克隆不会从原始数据集继承任何标准计算字段（内部计算字段会被继承），因此请注意不要试图访问克隆中的任何计算字段。

以下示例程序展示了如何在本节开头列出的情况下有效使用克隆的数据集。列表 4.9 包含了 Clone 应用程序的完整源代码。

# 列表 4.9 Clone—MainForm.pas

```delphi
unit MainForm;

interface
uses
  SysUtils, Variants, Classes, QGraphics, QControls, QForms,
  QDialogs, QGrids, QDBGrids, DB, DBClient, ExtCtrls, QStdCtrls;

type
  TFormMain = class(TForm)
    pnlClient: TPanel;
    pnlBottom: TPanel;
    ClientDataSet1: TClientDataSet;
    DataSource1: TDataSource;
    DBGId1: TDBGid;
    btnUpdate: TButton;
    btnInsert: TButton;
    btnRange: TButton;
    btnInsert2: TButton;
    procedure FormCreate(Sender: TObject);
    procedure FormDestroy(Sender: TObject);
    procedure btnUpdateClick(Sender: TObject);
    procedure btnInsertClick(Sender: TObject);
    procedure btnRangeClick(Sender: TObject);
    procedure btnInsert2Click(Sender: TObject);
  private
    { Private declarations }
    FCloneDS: TClientDataSet;
  public
    { Public declarations }
  end;

var
  frmMain: TfrmMain;

implementation
{$R *.xfm}

procedure TfrmMain.FormCreate(Sender: TObject);
begin
  ClientDataSet1.LoadFromFile('C:\Employee.cds');
  ClientDataSet1.AddIndex('byID', 'ID', [ixPrimary, ixUnique]);
  ClientDataSet1.IndexName := 'byID';
  FCloneDS := TClientDataSet.Create(nil);
  FCloneDS.CloneCursor(ClientDataSet1, False, False);
end;

procedure TfrmMain.FormDestroy(Sender: TObject);
begin
  FCloneDS.Free;
end;

procedure TfrmMain.btnUpdateClick(Sender: TObject);
begin
  Screen.Cursor := crHourglass;
  try
    FCloneDS.First;
    while not FCloneDS.EOF do begin
      FCloneDS.Edit;
      FCloneDS.FieldName('Salary ').AsFloat :=
        FCloneDS.FieldName(' Salary ').AsFloat * 1.10;
      FCloneDS.Post;

      FCloneDS.Next;
    end;
  finally
    Screen.Cursor := crDefault;
  end;
end;

procedure TfrmMain.btnInsertClick(Sender: TObject);
begin
  if FCloneDS.State <> dsBrowse then
    Exit;

  FCloneDS.Append;
  FCloneDS.FieldName('ID').AsInteger := 99999;
  FCloneDS.FieldName('Name').AsString := 'Eric Harmon';
  FCloneDS.FieldName(' Birthday ').AsString := '1/1/1967';
  FCloneDS.FieldName('Salary ').AsFloat := 1.00;
end;

procedure TfrmMain.btnInsert2Click(Sender: TObject);
begin
  if FCloneDS.State <> dsInsert then
    Exit;

  try
    FCloneDS.Post;
    ClientDataSet1.GotoCurrent(FCloneDS);
  except
    FCloneDS.Cancel;
    raise;
  end;
end;

procedure TfrmMain.btnRangeClick(Sender: TObject);
begin
```

