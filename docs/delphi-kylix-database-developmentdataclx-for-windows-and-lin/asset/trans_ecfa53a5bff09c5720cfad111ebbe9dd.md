

如果索引由多个字段组成，只需在调用 `SetKey` 之后依次设置每个字段，如下所示：

```pascal
ClientDataSet1.IndexName := 'byName';
ClientDataSet1.SetKey;
ClientDataSet1.FieldName('First').AsString := 'John';
ClientDataSet1.FieldName('Last').AsString := 'Doe';
ClientDataSet1.GotoKey;
```

调用 `GotoKey` 后，您可以使用 `EditKey` 方法来编辑用于搜索的键值。例如，以下代码片段展示了如何搜索 John Doe，然后再搜索 John Smith。这两条记录的姓氏相同，因此在第二次搜索时，只需指定键的姓氏部分即可。

```pascal
ClientDataSet1.IndexName := 'byName';
ClientDataSet1.SetKey;
ClientDataSet1.FieldName('First').AsString := 'John';
ClientDataSet1.FieldName('Last').AsString := 'Doe';
ClientDataSet1.GotoKey;

// Do something with the record

// EditKey preserves the values set during the last SetKey
ClientDataSet1.EditKey;
ClientDataSet1.FieldName('Last').AsString := 'Smith';
ClientDataSet1.GotoKey;
```

### GotoNearest

`GotoNearest` 的工作原理与 `GotoKey` 类似，区别在于它会查找大于或等于传入值的第一条记录。具体行为取决于 `KeyExclusive` 属性的当前值。

如果 `KeyExclusive` 为 `False`（默认值），`GotoNearest` 会查找大于或等于在调用 `SetKey` 或 `EditKey` 后设置的字段值的第一条记录。如果 `KeyExclusive` 为 `True`，`GotoNearest` 会查找大于在调用 `SetKey` 或 `EditKey` 后设置的字段值的第一条记录。

如果 `GotoNearest` 未找到匹配的记录，它将当前记录指针移动到数据集末尾。

以下示例展示了如何在数据集上执行索引搜索和非索引搜索。清单 3.7 展示了 Search 应用程序的源代码，这是一个演示 `TClientDataSet` 所支持的各种索引和非索引搜索技术的示例程序。

### 清单 3.7 Search—MainForm.pas

```pascal
unit MainForm;

interface

uses
  SysUtils, Classes, Variants, QGraphics, QControls, QForms, QDialogs,
  QStdCtrls, DB, DBClient, QExtCtrls, QActnList, QRids, QBGrids;

type
  TfrmMain = class(TForm)
    DataSource1: TDataSource;
    pnlClient: TPanel;
    pnlBottom: TPanel;
    btnSearch: TButton;
    btnGetDBBookmark: TButton;
    btnGetBookmark: TButton;
    btnLookup: TButton;
    DBGrid1: TBDBGrid;
    ClientDataSet1: TClientDataSet;
    btnSetRecNo: TButton;
    procedure FormCreate(Sender: TObject);
    procedure btnGetBookmarkClick(Sender: TObject);
    procedure btnGetDBBookmarkClick(Sender: TObject);
    procedure btnSetRecNoClick(Sender: TObject);
    procedure btnSearchClick(Sender: TObject);
    procedure btnLookupClick(Sender: TObject);
  private
    { Private declarations }
    FBookmark: TBookmark;
  public
    { Public declarations }
  end;

var
  frmMain: TfrmMain;

implementation

uses SearchForm;

{$R *.xfm}

procedure TfrmMain.FormCreate(Sender: TObject);
begin
  ClientDataSet1.LoadFromFile('C:\Employee.cds');

  ClientDataSet1.AddIndex('byName', 'Name', []);
  ClientDataSet1.IndexName := 'byName';
end;

procedure TfrmMain.btnGetBookmarkClick(Sender: TObject);
begin
  if Assigned(FBookmark) then
    ClientDataSet1.FreeBookmark(FBookmark);

  FBookmark := ClientDataSet1.GetBookmark;
end;

procedure TfrmMain.btnGotoBookmarkClick(Sender: TObject);
begin
  if Assigned(FBookmark) then
    ClientDataSet1.GotoBookmark(FBookmark)
  else
    ShowMessage('No bookmark assigned');
end;

procedure TfrmMain.btnSetRecNoClick(Sender: TObject);
var
  Value: string;
begin
  Value := '1';
  if InputQuery('RecNo', 'Enter Record Number', Value) then
    ClientDataSet1.RecNo := StrToInt(Value);
end;

procedure TfrmMain.btnSearchClick(Sender: TObject);
var
  frmSearch: TfrmSearch;
begin
  frmSearch := TfrmSearch.Create(nil);
  try
    if frmSearch.ShowModal = mrOk then begin
      case TSearchMethod(frmSearch.grpMethod.ItemIndex) of
        smLocate:
          ClientDataSet1.Locate('Name', frmSearch.edName.Text,
            [loPartialKey, loCaseInsensitive]);
```

```pascal
        smFindKey:
          ClientDataSet1.FindKey([frmSearch.edName.Text]);

        smFindNearest:
          ClientDataSet1.FindNearest([frmSearch.edName.Text]);

        smGotoKey: begin
          ClientDataSet1.SetKey;
          ClientDataSet1.FieldName('Name').AsString :=
            frmSearch.edName.Text;
          ClientDataSet1.GotoKey;
        end;

        smGotoNearest: begin
          ClientDataSet1.SetKey;
          ClientDataSet1.FieldName('Name').AsString :=
            frmSearch.edName.Text;
          ClientDataSet1.GotoNearest;
        end;
      end;
    finally
      frmSearch.Free;
    end;
  end;
end;

procedure TfrmMain.btnLookupClick(Sender: TObject);
var
  Value: string;
  V: Variant;
begin
  Value := '1';
  if InputQuery('ID', 'Enter ID to Lookup', Value) then begin
    V := ClientDataSet1.Lookup('ID', StrToInt(Value), 'Name;Salary');
    if not VarIsNull(V) then
      ShowMessage(Format('ID %s refers to %s, who makes %s',
        [Value, V[0], FloatToStrF(V[1], ffCurrency, 10, 2)]));
  end;
end;

end.
```

清单 3.8 包含了搜索表单的源代码。该清单中唯一有趣的代码片段是 *TSearchMethod*，它定义在单元文件的顶部附近，用于确定调用哪种方法进行查找。

### 清单 3.8 Search—SearchForm.pas

```pascal
unit SearchForm;

interface

uses
  SysUtils, Classes, QGraphics, QControls, QForms, QDialogs, QExtCtrls,
  QStdCtrls;

type
  TSearchMethod = (smLocate, smFindKey, smFindNearest, smGotoKey,
                  smGotoNearest);

  TfrmSearch = class(TForm)
    pnlClient: TPanel;
    pnlBottom: TPanel;
    Label1: TLabel;
    edName: TEdit;
    grpMethod: TRadioGroup;
    btnOk: TButton;
    btnCancel: TButton;
  private
    { Private declarations }
  public
    { Public declarations }
  end;

implementation

{$R *.xfm}

end.
```

图 3.9 展示了 Search 应用程序在运行时的情景。

![](img/fe651f295b5f960d5463c4fb581d2281_157_0.png)

**图 3.9**
Search 演示了索引搜索和非索引搜索。

### 总结

`TClientDataSet` 是一个功能极其强大的内存数据集，支持多种高性能的排序和搜索操作。以下是本章的几个关键点：

- 您可以在设计时和运行时创建客户端数据集。本章展示了如何将它们保存到磁盘，以便在单层数据库应用程序中使用。
- 填充客户端数据集的三种基本方法是：
    - 使用 `Append` 或 `Insert` 手动填充
    - 从另一个数据集获取
    - 从文件或流获取（即通过持久化数据集）
- Delphi 中的数据集可以通过多种方式导航：顺序导航、通过书签、以及通过记录号。
- 您可以为数据集创建索引，从而快速、轻松地按特定顺序对记录进行排序，并定位符合特定条件的记录。
- 可以使用筛选器和范围来限制数据集中可见数据的数量。当相关数据存储在连续的记录序列中时，范围非常有用。与范围不同，筛选器在应用前不需要设置索引。
- `Locate` 和 `Lookup` 是用于在客户端数据集中定位特定记录的非索引搜索技术。`FindKey`、`FindNearest`、`GotoKey` 和 `GotoNearest` 是索引搜索技术。

在下一章中，我将讨论更高级的客户端数据集功能。

## 高级客户端数据集操作

# 第 4 章

## 本章内容

- 数据集事件 148
- 禁用数据感知组件 158
- BLOB（二进制大对象） 162
- 嵌套数据集 172
- 撤销支持 176
- 从另一个客户端数据集克隆数据 186
- 维护聚合 192
- 杂项属性 197

前一章介绍了 `TClientDataSet`，并详细讨论了其许多基本功能。在本章中，我将探讨更多高级的客户端数据集功能，包括：

- 数据集事件
- 禁用数据感知组件
- BLOB（二进制大对象）
- 嵌套数据集
- 撤销支持
- 从另一个客户端数据集克隆数据
- 维护聚合
- 杂项属性

### 数据集事件

客户端数据集支持大量事件。其中一些事件在单层应用程序（如本章正在开发的应用程序）中有用，而另一些则仅在多 tier（多层）应用程序中（我们将在后续章节中开发此类应用）有用。

本章讨论的数据集事件在所有应用程序（包括单层和多 tier 应用）中都有用。从广义上讲，这些事件分为三类：`Beforexxx` 通知事件、`Afterxxx` 通知事件以及其他事件。`Beforexxx` 和 `Afterxxx` 通知事件在 Delphi 中发生重要活动之前和之后触发。就本讨论而言，“重要”指的是数据集执行的日常常规活动——即您希望在发生时收到通知的活动。

一个例子有助于澄清最后一个说法：假设您想要验证对数据集的所有删除操作。一种方法是在程序中允许删除发生的每个位置向用户显示确认消息。然而，这种方法有三个缺点：

- 它是重复性的。
- 它容易出错。如果您在代码的一个位置更改了确认消息，很容易忘记在其他位置更改该消息。您可能甚至完全忘记实现确认功能。
- 当 VCL/CLX 隐式删除记录时，它不起作用。如果在数据感知网格中按下 `Ctrl+Delete`，VCL/CLX 会在无需您编写任何代码的情况下为您处理删除操作。

