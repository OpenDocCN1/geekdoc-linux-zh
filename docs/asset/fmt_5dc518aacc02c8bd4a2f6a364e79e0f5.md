
![](img/52a35759a0f10dade27a840504be5d82_128_0.png)

```pascal
if RecNoJohn < RecNoFred then
// 再次定位到 John 的记录
ClientDataSet1.RecNo := RecNoJohn;

for Index := 1 to Abs(RecNoJohn - RecNoFred) + 1 do
  ClientDataSet1.Delete;
end;
```

该代码片段首先定位到这两个边界记录，并记住它们的绝对记录号。然后，它将数据集定位到较小的记录号。如果 `Fred` 出现在 `John` 之前，数据集此时已经位于较小的记录号上。

由于记录是按顺序编号的，我们可以减去这两个记录号（并加上一）来确定要删除的记录数。删除一条记录会使下一条记录成为当前记录，因此一个简单的 `for` 循环即可处理记录的删除。

请记住，`RecNo` 通常不是你在数据集中进行导航的首选方法，但记住它可用是个好习惯，以防你偶尔需要用到它。

### 清单 3.2 Navigate—MainForm.pas

```pascal
unit MainForm;

interface

uses

  SysUtils, Classes, QGraphics, QControls, QForms, QDialogs, QStdCtrls,

  DB, DBClient, QExCtrls, QActnList, QRids, QDBGirids, QDBCtrls;

type

  TfrmMain = class(TForm)

    DataSource1: TDataSource;

    pnlClient: TPanel;

    pnlBottom: TPanel;

    btnFirst: TButton;

    btnLast: TButton;

    btnNext: TButton;

    btnPrior: TButton;

    DBGIrid1: TBGrid;

    ClientDataSet1: TClientDataSet;

    btnSetRecNo: TButton;

    DBNavigator1: TDBNavigator;

    btnGetBookmark: TButton;

    btnGotoBookmark: TButton;

  procedure FormCreate(Sender: TObject);

  procedure btnNextClick(Sender: TObject);

  procedure btnLastClick(Sender: TObject);

  procedure btnSetRecNoClick(Sender: TObject);

  procedure btnFirstClick(Sender: TObject);

  procedure btnPriorClick(Sender: TObject);

  procedure btnGetBookmarkClick(Sender: TObject);

  procedure btnGotoBookmarkClick(Sender: TObject);

private

  { Private declarations }
  FBookmark: TBookmark;

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
end;

procedure TfrmMain.btnFirstClick(Sender: TObject);
begin
  ClientDataSet1.First;
end;

procedure TfrmMain.btnPriorClick(Sender: TObject);
begin
  ClientDataSet1.Prior;
end;

procedure TfrmMain.btnNextClick(Sender: TObject);
begin
  ClientDataSet1.Next;
end;

procedure TfrmMain.btnLastClick(Sender: TObject);
begin
  ClientDataSet1.Last;
end;

procedure TfrmMain.btnSetRecNoClick(Sender: TObject);
var
  Value: string;
begin
  Value := '1';
  if InputQuery('RecNo', 'Enter Record Number', Value) then
    ClientDataSet1.RecNo := StrToInt(Value);
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
    ShowMessage('No bookmark set!');
end;

end.
```
