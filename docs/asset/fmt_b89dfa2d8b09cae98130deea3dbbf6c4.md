
```pascal
procedure TForm1.DBCtrlGrid1PaintPanel(DBCtrlGrid: TDBCtrlGrid;
Index: Integer);
begin
if Index > DBCtrlGrid.PanelIndex then
DBCtrlGrid1.Canvas.Draw(0, 0, Image1.Picture.Graphic);
end;
```

此代码检查传入方法的索引，以查看是否正在绘制当前窗格。`PanelIndex`公共属性包含当前窗格的编号。所有非当前窗格都使用背景图形进行绘制。

列表 6.4 包含 `CtrlGrid` 演示应用程序的完整源代码，该应用程序允许您试用 `TDBCtrlGrid` 的一些属性。

### 列表 6.4 CtrlGrid—MainForm.pas

```pascal
unit MainForm;

interface

uses
Windows, Messages, SysUtils, Variants, Classes, Graphics, Controls, Forms,
Dialogs, dbctrlgrids, ExtCtrls, DB, DBClient, StdCtrls, Mask, DBCtrls,
ComCtrls;

type
TForm1 = class(TForm)
ClientDataSet1: TClientDataSet;
DataSource1: TDataSource;
pnlClient: TPanel;
DBCtrlGrid1: TDBCtrlGrid;
ecID: TDBEdit;
ecName: TDBEdit;
ecSalary: TDBEdit;
Label1: TLabel;
Label2: TLabel;
Label3: TLabel;
Label4: TLabel;
ecBirthday: TDBEdit;
pnlBottom: TPanel;
cbAllowInsert: TCheckBox;
cbAllowDelete: TCheckBox;
ecRowCount: TEdit;
ecColCount: TEdit;
cbShowFocus: TCheckBox;
Label5: TLabel;
Label6: TLabel;
Label7: TLabel;
cbOrientation: TComboBox;
Image1: TImage;
procedure FormCreate(Sender: TObject);
procedure cbAllowInsertClick(Sender: TObject);
procedure cbAllowDeleteClick(Sender: TObject);
procedure cbShowFocusClick(Sender: TObject);
procedure ecRowCountChange(Sender: TObject);
procedure ecColCountChange(Sender: TObject);
procedure cbOrientationClick(Sender: TObject);
procedure DBCtrlGrid1PaintPanel(DBCtrlGrid1: TDBCtrlGrid;
             Index: Integer);
private
 { Private declarations }
public
 { Public declarations }
end;

var
 Form1: TForm1;

implementation

{$R *.dfm}

procedure TForm1.FormCreate(Sender: TObject);
begin
 ClientDataSet1.LoadFromFile('C:\Employee.cds');
end;

procedure TForm1.cbAllowInsertClick(Sender: TObject);
begin
 DBCtrlGrid1.AllowInsert := cbAllowInsert.Checked;
end;

procedure TForm1.cbAllowDeleteClick(Sender: TObject);
begin
DBCtrlGrid1.AllowDelete := cbAllowDelete.Checked;
end;

procedure TForm1.cbShowFocusClick(Sender: TObject);
begin
DBCtrlGrid1.ShowFocus := cbShowFocus.Checked;
end;

procedure TForm1.ecRowCountChange(Sender: TObject);
begin
try
DBCtrlGrid1.RowCount := StrToInt(ecRowCount.Text);
except
DBCtrlGrid1.RowCount := 1;
end;
end;

procedure TForm1.ecColCountChange(Sender: TObject);
begin
try
DBCtrlGrid1.ColCount := StrToInt(ecColCount.Text);
except
DBCtrlGrid1.ColCount := 1;
end;
end;

procedure TForm1.cbOrientationClick(Sender: TObject);
begin
DBCtrlGrid1.Orientation := TDBCtrlGridOrientation(cbOrientation.ItemIndex);
end;

procedure TForm1.DBCtrlGrid1PaintPanel(DBCtrlGrid: TDBCtrlGrid;
Index: Integer);
begin
if Index < DBCtrlGrid.PanelIndex then
DBCtrlGrid.Canvas.Draw(0, 0, Image1.Picture.Graphic);
end;
```
